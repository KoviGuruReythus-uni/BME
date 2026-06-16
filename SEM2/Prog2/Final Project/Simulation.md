## Simulation.h
```c
#pragma once
#include "body.h"
#include <string>

class Simulation{
private:
    Body* *bodies; //pointer to an array of body pointers
    int capacity; //max allowed objects
    int count; //current number of objects
    const double G = 6.674e-11;

public:
    Simulation(int cap);
    ~Simulation();

    void addBody(Body *b);
    void step(double dt);

    void saveState(const std::string &filename) const; //save result to a file
};
```

### What is the key idea here?
- `private` holds an array of pointers? 
	- _i do not understand the syntax here_
- max number of allowed objects - this will be used to create the array
- `count` just a counter
- G - gravitational const

- constructor `Simulation` expects in an integer that sets the capacity

### `Body* *bodies`
there are a few problems that we have to work around
1. Body is an abstract class - meaning we cannot just create `Body` we need to make sure it is the children
2. The array meant to hold a `body` might not _fully_ hold a star or a planet, it might cut out parts that actually make the star a star
The solution?
- instead of an array with actually members inside, we have an array with pointers inside, the pointers - they point to whatever is needed, it could be a star, a planet and it will all abide by polymorphism.

#### There is one more part to this problem, deletion.
- If we just run `delete[]bodies` we run into a huge problem,
	- The array that we are deleting holds pointers, not the actual data, deleting the array will delete all the pointers, but the data will still just remain in memory.
	- We would be burning the bridges not the cities and we are also left with no way to reach the cities to correct our mistake either.
- For this, we run a `for` loop iterating from 0 to `count` and delete all the shit before finally running delete[]bodies

### Polymorphic VS Abstract classes

#### Polymorphic is the _base case_
- Any class with a virtual method is a polymorphic class
- This simply _allows_ for overriding if needed by the children.
	- if not, the children will just inherit the method, no strings attached. (simply a pass to, if needed, change things)

#### Abstract is one step above
- all abstract classes have a virtual method that ends in `= 0` this lil guy is called the _pure virtual modifier_
- this means that the parent (base) class itself simply CANNOT exist (useful in places where we want a template)
- The children of the class MUST redefine the method to their use case.

#### Summary
- polymorphic classes have a virtual method - this allows for overriding by its children if needed, if not the children will still just get the same method without any problem. But an abstract class mandates redefinition of a method by its children, the parent on its own simply cannot exist (useful in cases were we need a template). the `= 0` - the pure virtual specifier ensures that.

___
## Simulation.cpp
```c
#include "simulation.h"
#include <cmath>
#include <fstream>
#include <iostream>

Simulation::Simulation(int cap) : capacity(cap), count(0){
    bodies = new Body *[capacity]; //allocating array capable of holding "capacity" number of body pointers 
}

Simulation::~Simulation(){
    //iterate through the array and delete individual objects
    for (int i = 0; i < count; i++){
        delete bodies[i];
    }

    //delete the array itself
    delete[] bodies;
}

void Simulation::addBody(Body* b){
    if(count < capacity){
        bodies[count] = b;
        count++;
    }
}

void Simulation::step(double dt){
    for (int i = 0; i < count; i++){
        bodies[i]->resetAcceleration();
    }

    for (int i = 0; i < count; i++){
        for (int j = i + 1; j < count; j++){
            Vector3 diff = bodies[j]->getPosition() - bodies[i]->getPosition();
            double distSq = diff.x * diff.x + diff.y * diff.y + diff.z * diff.z;

            if(distSq < 1e-10) continue;

            double dist = std::sqrt(distSq);

            double forceMag = (G * bodies[i]->getMass() * bodies[j]->getMass()) / distSq;

            Vector3 dir = diff * (1.0 / dist);

            bodies[i]->addAcceleration(dir * (forceMag / bodies[i]->getMass()));
            bodies[j]->addAcceleration(dir * (-forceMag / bodies[j]->getMass()));
        }
    }

    for (int i = 0; i < count; i++){
        bodies[i]->applyEulerUpdate(dt);
    }
}

void Simulation::saveState(const std::string &filename) const{
    std::ofstream outFile(filename);
    if(!outFile.is_open()){
        std::cerr << "Error: Could not open file for writing.\n";
        return;
    }

    outFile << "Name,Mass,Px, Py,Pz,Vx,Vy,Vz\n";

    for (int i = 0; i < count; i++){
        outFile << bodies[i]->getName() << "," << bodies[i]->getMass() << "," <<bodies[i]->getPosition().x<<","<<bodies[i]->getPosition().y<<","<<bodies[i]->getPosition().z<<","<< bodies[i]->getVelocity().x << "," << bodies[i]->getVelocity().y << "," << bodies[i]->getVelocity().z << "\n";
    }
    outFile.close();
}


```

### Constructor & Destructor

```c
Simulation::Simulation(int cap) : capacity(cap), count(0){
    bodies = new Body* [capacity];
}
```
- Reserve space for `Body*` type (body pointer, not body) and enough space such that we can fit `capacity` amount of them in there. 


```c
Simulation::~Simulation(){
    //iterate through the array and delete individual objects
    for (int i = 0; i < count; i++){
        delete bodies[i];
    }

    //delete the array itself
    delete[] bodies;
}
```

- the for loop goes through the array, from the 0th item to the `count`-th term and deletes the actual item itself.
- And then we delete the array itself

### addBody
```c
void Simulation::addBody(Body* b){
	if(count < capacity){
		bodies[count] = b;
		count++;
	}
}
```
- `Body* b` we have a pointer called b that is of type Body (from body.h)
- if the current count is lesser than max capacity, we have space for more, so we put the pointer there and then increase the counter by one.


### step (phy)

```c
void Simulation::step(double dt){
    for (int i = 0; i < count; i++){
        bodies[i]->resetAcceleration();
    }

    for (int i = 0; i < count; i++){
        for (int j = i + 1; j < count; j++){
            Vector3 diff = bodies[j]->getPosition() - bodies[i]->getPosition();
            double distSq = diff.x * diff.x + diff.y * diff.y + diff.z * diff.z;

            if(distSq < 1e-10) continue;

            double dist = std::sqrt(distSq);

            double forceMag = (G * bodies[i]->getMass() * bodies[j]->getMass()) / distSq;

            Vector3 dir = diff * (1.0 / dist);

            bodies[i]->addAcceleration(dir * (forceMag / bodies[i]->getMass()));
            bodies[j]->addAcceleration(dir * (-forceMag / bodies[j]->getMass()));
        }
    }

    for (int i = 0; i < count; i++){
        bodies[i]->applyEulerUpdate(dt);
    }
}
```

```c
 for (int i = 0; i < count; i++){
        bodies[i]->resetAcceleration();
    }
```
- go through the whole array and individually set all the accelerations of bodies to 0. 

#### $O(N^2)$ nested loop
```c
for (int i = 0; i < count; i++){
        for (int j = i + 1; j < count; j++){
            Vector3 diff = bodies[j]->getPosition() - bodies[i]->getPosition();
            double distSq = diff.x * diff.x + diff.y * diff.y + diff.z * diff.z;

            if(distSq < 1e-10) continue;

            double dist = std::sqrt(distSq);

            double forceMag = (G * bodies[i]->getMass() * bodies[j]->getMass()) / distSq;

            Vector3 dir = diff * (1.0 / dist);

            bodies[i]->addAcceleration(dir * (forceMag / bodies[i]->getMass()));
            bodies[j]->addAcceleration(dir * (-forceMag / bodies[j]->getMass()));
        }
    }
```

1. `int i`  and `int j` track adjacent bodies. `j` leads by one.
	- They track every unique pair of objects without double counting. 
	- [earth, moon, sun], each have indices 0,1,2 respectively. Count is 3.
		- LOOP 1 : i = 0, 
			- j = 1 : earth, moon
			- j = 2 : earth, sun
		- LOOP 2 : i = 1;
			- j = 2 : moon, sun 
		- LOOP 3 : i = 2;
			- j = 3 (impossible, loop ends here)

2. Find the difference in distance between them.
3. `distSq` is converted into actual relative distance 
4. `if(distSq < 1e-10) continue;` this is to check for collisions and potential cases where $R$ is tending to 0, which would break everything.
5. $F = \frac{Gm_1m_2}{R^2}$ 
6. direction - calculating unit vector from what we have
7. addAcceleration - $\vec{u}_0 \times \frac{F}{a}$ this works because $F=ma$ 
	1. A negative sign is required for `j` bodies because of equal and opposite forces. the direction of force we calculated is from i to j, and now j will also be pulled towards i, this accommodates that.


```c
 for (int i = 0; i < count; i++){
        bodies[i]->applyEulerUpdate(dt);
    }
```
- Velocity and position as calculated from the Force (and hence acceleration) that we just calculated.



