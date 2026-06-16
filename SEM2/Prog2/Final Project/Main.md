## main.cpp
```c
#include <iostream>
#include <fstream>
#include <sstream>
#include <string>
#include "simulation.h"
#include "star.h"
#include "planet.h"

//struct to hold data loaded during calculation phase
struct StateData{
    std::string name;
    double mass;
    Vector3 pos;
    Vector3 vel;
};

int main()
{
    //SIMULATION
    std::cout << "Phase 1 : Simulation\n";

    // creating a simulation that can hold up to 10 bodies
    Simulation sim(10);

    //dynamically allocate a star and a planet 

    // star - 2 x 10^30 kg, at (0,0,0), initial veloctiy = 0
    Body *sun = new Star("Sun", 2.0e30, {0, 0, 0}, {0, 0, 0});

    // planet - 6e24 kg, 1.5e11 m away, 30000 m/s
    Body *earth = new Planet("Earth", 6.0e24, {1.5e11, 0, 0}, {0, 30000, 0});

    //Polymorphism
    sun->printType();
    earth->printType();

    sim.addBody(sun);
    sim.addBody(earth);

    //running the sim for roughly 30 days with timestep of 1 hour
    int daysToSimulate = 30;
    double dt = 3600;
    
	std::cout << "Enter the number of days to simulate: ";
    std::cin >> daysToSimulate;

    std::cout << "Enter time step (dt) in seconds (eg: 3600 for 1 hour): ";
    std::cin >> dt;
    
    int totalSteps = (daysToSimulate * 24 * 3600) / dt;

    std::cout << "Running simulation for " << daysToSimulate << "days...\n";
    for (int i = 0; i < totalSteps; i++){
        sim.step(dt);
    }

    std::string filename = "simulation_data.csv";
    sim.saveState(filename);
    std::cout << "Simulation complete. Data saved to " << filename << "\n\n";




    //CALCULATION
    std::cout << "Phase 2 : Calculator\n";

    //opening the file we just wrote
    std::ifstream inFile(filename);
    if(!inFile.is_open()){
        std::cerr << "Error: Could not open file for reading\n";
        return 1;
    }

    std::string line;
    std::getline(inFile, line); // skip the header line

    //memory alloc
    StateData data[10];
    int bodyCount = 0;

    //parse file into the array
    while(std::getline(inFile, line) && bodyCount < 10){
        std::stringstream ss(line);
        std::string token;

        //extract name
        std::getline(ss, data[bodyCount].name, ',');

        //extract mathematic data
        std::getline(ss, token, ',');
        data[bodyCount].mass = std::stod(token);
         std::getline(ss, token, ',');
         data[bodyCount].pos.x = std::stod(token);
         std::getline(ss, token, ',');
         data[bodyCount].pos.y = std::stod(token);
        std::getline(ss, token, ',');
        data[bodyCount].pos.z = std::stod(token);
         std::getline(ss, token, ',');
         data[bodyCount].vel.x = std::stod(token);
         std::getline(ss, token, ',');
         data[bodyCount].vel.y = std::stod(token);
         std::getline(ss, token, '\n');
         data[bodyCount].vel.z = std::stod(token);

         bodyCount++;
    }

    inFile.close();

    //maths eval
    Vector3 totalMomentum = {0, 0, 0};
    double totalKinetic = 0.0;
    double totalPotential = 0.0;
    const double G = 6.674e-11;

    for (int i = 0; i < bodyCount; i++){
        //individual momentum
        Vector3 p = data[i].vel * data[i].mass;
        totalMomentum += p;

        //individual kinetic energy
        double vSq = (data[i].vel.x * data[i].vel.x) + (data[i].vel.y * data[i].vel.y) + (data[i].vel.z * data[i].vel.z);
        totalKinetic += 0.5 * data[i].mass * vSq;

        //pairwise potential energy
        for (int j = i + 1; j < bodyCount; j++){
            Vector3 diff = data[j].pos - data[i].pos;
            double distSq = (diff.x * diff.x) + (diff.y * diff.y) + (diff.z * diff.z);

            if(distSq > 0){
                double dist = std::sqrt(distSq);
                totalPotential += -G * (data[i].mass * data[j].mass) / dist;
            }
        }
    }

    double totalEnergy = totalKinetic + totalPotential;

    //outputs
    std::cout << "\n--RESULTS--\n";
    std::cout << "Total System Momentum: " << totalMomentum.x << "," << totalMomentum.y << "," << totalMomentum.z << "kg*m/s\n";
    std::cout << "Total Kinetic Energy: " << totalKinetic << "J\n";
    std::cout << "Total Potential Energy: " << totalPotential << "J\n";
    std::cout << "Total System Energy: " << totalEnergy << "J\n"; 

    return 0;
}
```

- The simulator is split into 2 parts, 
	- Simulation
	- calculation

### Simulation
```c
    //SIMULATION
    std::cout << "Phase 1 : Simulation\n";

    // creating a simulation that can hold up to 10 bodies
    Simulation sim(10);

    //dynamically allocate a star and a planet 

    // star - 2 x 10^30 kg, at (0,0,0), initial veloctiy = 0
    Body *sun = new Star("Sun", 2.0e30, {0, 0, 0}, {0, 0, 0});

    // planet - 6e24 kg, 1.5e11 m away, 30000 m/s
    Body *earth = new Planet("Earth", 6.0e24, {1.5e11, 0, 0}, {0, 30000, 0});

    //Polymorphism
    sun->printType();
    earth->printType();

    sim.addBody(sun);
    sim.addBody(earth);

    //running the sim for roughly 30 days with timestep of 1 hour
    int daysToSimulate = 30;
    double dt = 3600;
    
	std::cout << "Enter the number of days to simulate: ";
    std::cin >> daysToSimulate;

    std::cout << "Enter time step (dt) in seconds (eg: 3600 for 1 hour): ";
    std::cin >> dt;
    
    int totalSteps = (daysToSimulate * 24 * 3600) / dt;

    std::cout << "Running simulation for " << daysToSimulate << "days...\n";
    for (int i = 0; i < totalSteps; i++){
        sim.step(dt);
    }

    std::string filename = "simulation_data.csv";
    sim.saveState(filename);
    std::cout << "Simulation complete. Data saved to " << filename << "\n\n";

```


```c
Simulation sim(10);
```

- Creating a member of `Simulation` class,

```c
//from Simulation.h
public:
    Simulation(int cap);
```
- This constructor is being called here

```c
Body *sun = new Star("Sun", 2.0e30, {0,0,0}, {0,0,0});
```

```c
//from Body.h
public:
    //constructors
    Body(std::string n, double m, Vector3 p, Vector3 v);
```
- This constructor is being called here after `new`
- We are creating a pointer of `Body` type called sun
	- And then we are dynamically allocating memory in space for a new `Star`
		- The star is called Sun
		- it is $2 \times 10^{30} g$ 
		- it is as origin
		- it is at rest
	- And the pointer `sun` points to the star called `Sun`

```c
    //Polymorphism
    sun->printType();
    earth->printType();
```
- deference the pointer called `sun` and then since it is a `Star` type, we have dedicated `printType()` functions written
```c
//FROM PLANET.H

class Planet: public Body{ //inheritance
public:
    Planet(std::string n, double m, Vector3 p, Vector3 v) : Body(n,m,p,v){}

    void printType() const override{ //overriding the pure virtual function in body.h
        std::cout << "Type: Planet | Name: " << name << "\n";
    }
};

```

```c
//running the sim for roughly 30 days with timestep of 1 hour
    int daysToSimulate = 30;
    double dt = 3600;
    
	std::cout << "Enter the number of days to simulate: ";
    std::cin >> daysToSimulate;

    std::cout << "Enter time step (dt) in seconds (eg: 3600 for 1 hour): ";
    std::cin >> dt;
    
    int totalSteps = (daysToSimulate * 24 * 3600) / dt;

    std::cout << "Running simulation for " << daysToSimulate << "days...\n";
    for (int i = 0; i < totalSteps; i++){
        sim.step(dt);
    }
```

- `totalSteps` = $\frac{days~ \times ~ hours~per~day~ \times ~ seconds ~ per ~ day}{dt}$
- This is the same as $\frac{Total~seconds}{dt}$


- A loop is run for every 1 hour in 30 days (720 times) and `step` method from `simulation.cpp` is run here

- file handling is self explanatory tbh

### Calculation

```c
//CALCULATION
    std::cout << "Phase 2 : Calculator\n";

    //opening the file we just wrote
    std::ifstream inFile(filename);
    if(!inFile.is_open()){
        std::cerr << "Error: Could not open file for reading\n";
        return 1;
    }

    std::string line;
    std::getline(inFile, line); // skip the header line

    //memory alloc
    StateData data[10];
    int bodyCount = 0;

    //parse file into the array
    while(std::getline(inFile, line) && bodyCount < 10){
        std::stringstream ss(line);
        std::string token;

        //extract name
        std::getline(ss, data[bodyCount].name, ',');

        //extract mathematic data
        std::getline(ss, token, ',');
        data[bodyCount].mass = std::stod(token);
         std::getline(ss, token, ',');
         data[bodyCount].pos.x = std::stod(token);
         std::getline(ss, token, ',');
         data[bodyCount].pos.y = std::stod(token);
        std::getline(ss, token, ',');
        data[bodyCount].pos.z = std::stod(token);
         std::getline(ss, token, ',');
         data[bodyCount].vel.x = std::stod(token);
         std::getline(ss, token, ',');
         data[bodyCount].vel.y = std::stod(token);
         std::getline(ss, token, '\n');
         data[bodyCount].vel.z = std::stod(token);

         bodyCount++;
    }

    inFile.close();

    //maths eval
    Vector3 totalMomentum = {0, 0, 0};
    double totalKinetic = 0.0;
    double totalPotential = 0.0;
    const double G = 6.674e-11;

    for (int i = 0; i < bodyCount; i++){
        //individual momentum
        Vector3 p = data[i].vel * data[i].mass;
        totalMomentum += p;

        //individual kinetic energy
        double vSq = (data[i].vel.x * data[i].vel.x) + (data[i].vel.y * data[i].vel.y) + (data[i].vel.z * data[i].vel.z);
        totalKinetic += 0.5 * data[i].mass * vSq;

        //pairwise potential energy
        for (int j = i + 1; j < bodyCount; j++){
            Vector3 diff = data[j].pos - data[i].pos;
            double distSq = (diff.x * diff.x) + (diff.y * diff.y) + (diff.z * diff.z);

            if(distSq > 0){
                double dist = std::sqrt(distSq);
                totalPotential += -G * (data[i].mass * data[j].mass) / dist;
            }
        }
    }

    double totalEnergy = totalKinetic + totalPotential;

    //outputs
    std::cout << "\n--RESULTS--\n";
    std::cout << "Total System Momentum: " << totalMomentum.x << "," << totalMomentum.y << "," << totalMomentum.z << "kg*m/s\n";
    std::cout << "Total Kinetic Energy: " << totalKinetic << "J\n";
    std::cout << "Total Potential Energy: " << totalPotential << "J\n";
    std::cout << "Total System Energy: " << totalEnergy << "J\n"; 

    return 0;
```


```c
std::string line;
std::getline(inFile, line); // skip the header line
```

`std::string line;` - This is a standard variable declaration, this tell the compiler that we need a block of memory on the heap, formatted to hold text and to call it "line" (ques: how does the compiler know how much space we need? What exactly is one block?)

`std::getline(inFile, line);`
- go to the file and keep advancing the internal cursor until we hit a `\n` (this is the behaviour of `getline`)
- `inFile` is the _source_ for `getline`
- `line` is the location 
	- we take all the characters from `inFile` until a `\n` is hit and dump it all into `line` 

- "Execute the standard line-reading function. Connect the intake hose to the `inFile` object, connect the output hose to the `line` string and run the pump until a `\n` is hit"
