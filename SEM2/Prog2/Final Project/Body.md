## Body.h
```c
#pragma once
#include <string>
#include "vector.h"

class Body{
protected:
    std::string name; 
    double mass;
    Vector3 position;
    Vector3 velocity;
    Vector3 acceleration;

public:
    //constructors
    Body(std::string n, double m, Vector3 p, Vector3 v);
    //virtual destructor for polymorphism
    virtual ~Body() = default;
    
    virtual void printType() const = 0;

    //physics
    void resetAcceleration();
    void addAcceleration(const Vector3 &a);
    void applyEulerUpdate(double dt);

    //getx
    double getMass() const;
    Vector3 getPosition() const;
    Vector3 getVelocity() const;
    std::string getName() const;
};

```

### Notes
- header file
	- no full implementation, only prototypes

- protected class for inheritance 
	- children of this class will inherit the constructors and variables

- constructor
```c
Body(std::string n, double m, Vector3 p, Vector3 v);
//constructor with no defaults? A body class member will be constructed with a string for name, a double for mass and Vector3 type position and velocity
virtual ~Body() = default; 

```


```c
 virtual void printType() const = 0;
```
- The `=0` at the end is called the pure virtual specifier
	- _"I refuse to write the code for this function here. Therefore, it must be physically impossible to create a raw `body` object. Any children of the class will have to write their own function for this or they too cannot exist"_

```c
virtual ~Body() = default;
```
- if we delete Planet using Body pointer, if the destructor wasn't virtual, it would just delete Body and not its children.
- The virtual destructor makes sure that the deletion starts from the lowest possible child and makes it way up, thus ensuring there is no memory leak.

- `virtual ~Body() = default` is same as `virtual ~Body() = default`
	- it is cleaner to read
	- in modern cpp, this means that the compiler will generate a standard, boiler plate destructor for us.


- 3 void functions to manage the physics
	- reset acceleration
	- add acceleration to a specific member of the class when prompted to
	- apply euler update for integration

- getters
	- double getMass() const;  
		- gets mass, a function that will just return the mass of the member we need, also const because we are promising that we wont be changing anything also incase mass itself is unmodifiable (const)
	- other getters (self explnanatory)

___
## Body.cpp
```c
#include "body.h"

Body::Body(std::string n, double m, Vector3 p, Vector3 v) : name(n), mass(m), position(p), velocity(v), acceleration({0, 0, 0}) {}

void Body::resetAcceleration(){
    acceleration = {0, 0, 0};
}

void Body::addAcceleration(const Vector3 &a){
    acceleration += a;
}

void Body::applyEulerUpdate(double dt){
    //step velocity first and then position (standard euler integration)
    velocity += acceleration * dt;
    position += velocity * dt;
}

double Body::getMass() const { return mass; }
Vector3 Body::getPosition() const { return position; }
Vector3 Body::getVelocity() const { return velocity; }
std::string Body::getName() const { return name; }
```

```c
Body::Body(std::string n, double m, Vector3 p, Vector3 v) : name(n), mass (m), position(p), velocity(v), acceleration({0,0,0}) {}
```
- giving body to the constructor we defined in `body.h` 
- `Body::Body`
	- "in Body class, for a Body member"
- `name(n)....`
	- in the class, for name set n 
	- this is called the _member initialisation list_ 
		- this is better than just creating a blank string `name` and then replacing that with n because from the very first nanosecond they are born in the RAM, the compiler constructs the variables with the correct data.
			- (makes it more efficient, these are the smaller things that make cpp beautiful)
- `acceleration({0,0,0})`
	- set default acceleration to 0
	- this will later than be modified using addAcceleration

```c
void Body::applyEulerUpdate(double dt){
	velocity += acceleration * dt;
	position += velocity * dt;
}
```

_not 100% sure about the application here or about what we are doing_
- Velocity is first modified because position then depends on that

