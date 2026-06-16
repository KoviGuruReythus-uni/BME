B:
- I am not 100% sure what even the code does, i dont know the syntax, throiw, catch etc.
- but from what i can guess, there is nothing wrong with it. it gets a const exception type pointer and cout's it.

C:
- double f is meant to return a double
- it gets in a float
- so that could mean that we are using it to convert var types
- but in main, we then try to assign d2 (which is a float) the value of d3 but it has been turnt into a double... 
- the same at cout as well, we are now adding a float and a double, oh wait, we arent, d2 is also a float now?

D:
- nothing wrong with that, a class can access its privaate members as long as the method is inside the class itself. But outside memebers including children cannot

E:
- Let me first think out loud,
	- we have 2 classes A and B
	- class C is inheriting from both of them, nothing wwrong.
	- `B* pb = new C;` pb is a pointer of class B and we have assigneds it some space in memory and called it C 
	- `A* pa = (C*)pb;` pa is a pointer of A, and that is being given the value of (c*)pb - what is that? C* means that the we are pointing something to a member of class C, but we already said that pb is a class member of B, and we have allocated it space in the memory and called it C? I am getting confused here, idk what correct terms to use, what is happening ahhhhj shit... I am underprepared, fuck.

