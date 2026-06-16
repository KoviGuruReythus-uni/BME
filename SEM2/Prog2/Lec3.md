## Constructors and Destructor

### Constructor

```c
#include <stdio.h>
int main() {
Point p1; //we havent initialised this
p1.draw(); //this will simply just give out memory garbage
}
```

- A constructor is a class method which is called automatically *after* the object is created. 
- It is basically the _default_ settings for the object
- The name of the constructor is the same as the name of the Class.
- The constructor has no return value 

```c
class Point{
int x, int y, 
public
Point(int cx, int cy) //some point in the screen //2 PARAMETER CONSTRUCTOR
{x=cx; y=cy;}
Point() {x=y=0;} //DEFAULT CONSTRUCTOR <- it is called this
Point(int cx) {x=cx; y=0;} //CONVERSION CONSTRUCTOR<- because only the x is changed
}
```
- we can have multiple contructors with the same name in cpp because in cpp unlike C, functions are not only identified by their name but also their vars 


- Constructors NEED to have the same name as the class they are in because the complier has to identify in which class it has to call the constructor in. 


- Instead of writing all 3 constructors, it can be simplified into, 
```c
Point(int cx=0; int cy=0;) {x=cx; y=cy;} //This sums up everything
```

```c
int x; //declaration
x=2; //value assignment



int x=2; //definition
```

- Definition is better because modern CPUs can optimise it to happen in a single step. 
- Definition is the same as a constructor because it gives the object an initial value.
- Both of them are basically the same in assembly level

### Destructor
- When a destructor is not manually creates the conmpilor automatically assigns ones
- Destructors cannot have a parameter
- They do only when we need to do dynamic memory management

### Copy Constructor
```c
int main() {
Point p1(20,30);
Point p2(p1); //or Point p2 = p1;
}
```
- whenever a copy is created the copy constructor is called

```c
	Point (Point p){
	x = p.x;
	y = p.y
	}
```



___


- Defining the constructor in Rect.h and then implementing it in main.cpp and rect.cpp 
	- We all telling the complier that the structure called _xyz_ exists in rect.h
	- But when the header and the other .cpp files are "linked" the complier then "understands" what that previous definition meant. 
	- This is better than just implementing _xyz_ in rect.h because it uses lesser memory. And also makes it so that _xyz_ in rect.h is a "default" template that can be implemented in different ways across different .cpp files. 



$$
\\\begin{aligned}
/& 

\\\end{aligned}
	$$