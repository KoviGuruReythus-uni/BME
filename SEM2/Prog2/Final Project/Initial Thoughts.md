
 ***The first thing is to parse all the things in the said in the documentation into smaller chunks to work on:***
 
 **Simulation:**
- I would assume we have to define all the objects that are being added. For this I would like to use a class system. Give them some default constructors and such. 
	- What could the constructors be?
		- mass
		- volume? (neutron star vs sun... where density is a main factor)
		- position vector
		- initial velocity vector
		- it might even be useful to have an object id thing going on with a global var (ik it is called something else... when there is a method/var in the class that is common for the whole class and its children)
- We also need a timer 
- We need to setup a base coordinate system (how much is the complexity difference between 2d and 3d, if 2d is much simpler for everything, i'd rather do that)
- We will have to define collision
	- Assuming all objects are spheres, 
		- From the database (where all the data is finally dumped) we will have to check if any outer circumference of 2 spheres are touching, if so, they have collided
		- Also, would it be better to kill off objects that have collided to avoid anomalies? I'd assume so
- I would first like to work on getting basic data out, after which integrating different formulas like momentum, kinetic energy and shit like that should be pretty simple (this will also need a class called _formula_ or some shit like that)
- Now comes the hard part, instead of brute forcing everything, we will have to use clever algorithms to make sure our shit doesnt go bonkers... (euler integration vs leapfrog vs verlet... I will first have to know about what are all the options and what they do - at least moderately before deciding on one)
- As we discussed before, there are 2 parts to this, one is simulation accuracy and the other is data storage. We will store data in a longer interval than the simulation... (does this mean we will need 2 timers, or we can tell storageTimer to trigger ever 5n of simulationTimer)
___

**_THE BODY CLASS_**

Variables:
- mass
- radius
- starting point vector 
	- x
	- y
	- z
- initial velocity vector
	- $\vec i$
	- $\vec j$
	- $\vec k$

Methods:
- Returning the data to a datasheet.
___

_**THE SIMULATION CLASS**_:
Insertion of object relative to other object
	1. Get `obj a` pos
	2. vector addition to get insertion coordinates with respect to the origin
	3. insert new object with presets
- Collision
	- Constantly have a function that checks the relative distance between 2 objects - this will be measured from their respective centres
	- If that distance is less than or equal to sum of their radii either
		- Kill them off
		- Or (i feel like this is better), assume perfectly inelastic collision every time and convert both objects into the same 
			- there is a problem here, what will the density of the new object be? Is there a way to find this out. Say a gaseous thingamabob and a solid thingamabob collide, they wont fucking get turned into a single state... Too much thinking
				- A simpler solution would be to consider inelastic collision only if the densities are same, if noe the objects despawn... 
	- Also, instead of constantly checking the distance between 2 objects during run time, we can just measure everything and then do this during the calculation step...

	- Okayyy... this is a big thing to think about.... 
	- Active calculationg during run time is simpy just stupid, if there are n objects we will have n(n-1) things to track... that is simply too much to do and is inefficient 
	- We will instead record all their positions and record them and then, 
		- If there is collision between 2 objects, any data recorded after this collision will be garbage, the physics wont be what we want. 
		- So we delete all the data after that point. 
		- Using that point as reference, we will calculate the momentum. 
			- (This is the most elegant approach i could think of)



1. Title page
	1. Neptun - i6sm8t
	2. lab group id - cs16b
	3. course id - Basics of programming 2, bmeviiiaa03
	4. name of instructor - ellabban hesham hesham mohamed
2.  Interface and exec
	1. I have included the main.md file and it contains the whole program as the first thing. But it is just the simple cout cin... not args
	2. ./nbody if on mac, idk about windows
3. testing and verif
	1. yup, it worked
	2. yes. 
4. improvements
	1. yes yes yes. Include everything, you can also go through initial_thoughts.md for my initial thoughts when I first had the idea of doing the project
	2. There are a bunch
		1. improve time complexity, using leap frog
		2. make it so that objects can be added by the user
			1. objects of different sizes 
			2. different initial velocities
			3. at different positions
				1. If objA is already placed, then all objects following it will have to ability to be placed relative to it...
		3. 3d - meh, maybe... But i would love to make it so that we display something on the tui itself, i have a thing for tui apps...
		4. it would be nice, if there was a way where the user to see a fastforward, recap of the simulation, visually... That would make it very interactive and nice
5. Tonality
	1. yes please, make it look very professional. Also output a doc file, not a pdf, so that I can later edit it.
	2. yes also.
	3. The lab assitant asked us to include inheritance charts to make skimming the document easy, let's take it a it further and make as many diagrams for things, make it as pictorial and visual as possible so that he can understand it without even having to read a bunch

