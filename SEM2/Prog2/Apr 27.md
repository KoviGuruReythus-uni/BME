_PASSING BY POINTER VS REFERENCE_
- Pointer holds the memory address of the variable
- We have to dereference it `*ptr` to get the value 
- A reference _is_ the variable, it feels identical to using the original. 

	_what is a null pointer_
	- it is a pointer that points to nothing
	- holds the address `0` 
	- It is used as a 'no value' signal. `Return nullptr if...`

- References cannot be NULL but pointers can. 
- References cannot be rebound

- Pointers are necessary when you need optional values or when you need to reassign what you are point at or when dealing with arrays. For everything else references are preferred. 

