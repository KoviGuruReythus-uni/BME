## Vector.h
```c
#pragma once

struct Vector3 {
    double x, y, z;

    Vector3 operator+(const Vector3 &other) const;
    Vector3 operator-(const Vector3 &other) const;
    Vector3 operator*(double scalar) const;
    Vector3 operator+=(const Vector3 &other);
};
```

- Header file - so no full implementation, just prototyping.
- We are basically just doing operator overloading.
	- What is the syntax for operator overloading?

### Operator Overloading
#### Definition
Used to customise operators in cpp for operands of user defined types

_a better more intuitive version_
- Redefining operators for user defined types
- Operators that cannot be overloaded;
	- sizeof 
	- typeid 
	- scope resolution (::)
	- class member access (. _and_ .*)

#### Syntax
```c
[return type]operator[Symbol]([Parameters]) [Optional const]
```

#### Example
```c
vector operator+(vector &other) const;
```
- For the members of the class 'vector' we have overloaded the operator +.
- The input is also another member of the same class
	- _we are essentially setting up the framework to define the addition of vectors down the line in a .cpp file_
___
## Vector.cpp
```c
#include "vector.h"

Vector3 Vector3::operator+(const Vector3& other) const{
    return {x + other.x, y + other.y, z + other.z};
}

Vector3 Vector3::operator-(const Vector3 &other)const{
    return {x - other.x, y - other.y, z - other.z};
}

Vector3 Vector3::operator*(double scalar) const{
    return {x * scalar, y * scalar, z * scalar};
}

Vector3 Vector3::operator+=(const Vector3 &other) {
    x += other.x;
    y += other.y;
    z += other.z;
    return *this;
}

```

- The header file is included  (this tells the compiler to look for the framework over there)

- We now fully define what all the overloading (and all other methods) do 

```c
Vector3 Vector3::operator+=(const Vector3 &other){
	x+=other.x;
	y+=other.y;
	z+=other.z;
	return *this;
}
```

- What is that last `return *this`?
	- `*this` is a pointer to the specific object calling the method
_example:_
```
VectorA += VectorB
```
this just means that,
`VectorA = VectorA + VectorB`

What is the role of the `this` pointer here?
- After the addition and redefinition is done, we return the memory address of `VectorA` which is now modified.

