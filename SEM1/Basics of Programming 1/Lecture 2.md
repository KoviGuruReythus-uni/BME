### Programming in C:

```c
//this is a program that does nothing (no output or process) but is technically a working program in C

int main () //this is the way to start any C prgram. This marks the start of the prog
{ 
	return 0; //This marks the end of the prog. 
}
	//THis prog basically, starts and ends. 
```
The {} is called a _block_ and it encloses a "block" of code. 

#### Printing Hello World!

```c
#include <stdio.h> //this is the required compiler for printf function

int main()
{
	printf("Hello World! \n"); //this is the main function
	return 0; //prog ends
}
```
* The ```\n``` is called a _line feed_ or _new line_ it basically inserts ```enter``` key to get to a new line after completing the `printf` func. 

#### The /n
```c
#include <stdio.h>
int main()
{
	printf("Are you ");
	printf("blind? \n");
	printf("Go Bayern, go!");
	return 0;
}
```
OUTPUT: 
```
Are you blind? 
Go Bayern, go!
```

* You can see that even though there are 2 lines of code and 2 printf functions for "Are you " and "blind" they are printed in the same line. 
* This is the use of the \n. 

### Printing Variables: 
```c
#include <stdio.h>
int main()
{
	int n; //declaring an int var called 'n'
	n = 2; //assigning n a value of 2
	printf("The value is: %d\n", n); //printing the val of n
	n = -5; //assigning a new value of -5 for n
	printf("The value is: %d\n", n); //printing the current val of n
	return 0; //end prog

}
```
OUTPUT:
```
The value is: 2
The value is: -5
```

#### The "%d" confusion: 
* The %d is called a _format specifier_ as the name suggests, it tells the ```printf``` function what to expect. 
* ```d%\n``` tells the ```printf``` function to expect an integer, which is given at the end as 'n' 

* There are a lot of format specifiers in C, 
	1. %d - int
	2. %f - float or double 
	   * The difference between a int and float:
		   * int expects a whole number with no decimal
		   * whereas float can print integers or fractions upto 6 decimals (obviously, you can assign more memory to print numbers with higher accuracy)
	3. %c - character 
	4. %s - string (sentence)

* Now lets see an example using all these format specifiers to clarify;
```c 
#include <stdio.h>
int main()
{
printf("Letter: %c, Word: %s, Whole numb: %d, Fraction: %f\n", 'B', "Bomboclat", 3, 3.14);
}
```
OUTPUT:
```
Letter: B, Word: Bomboclat, Whole numb: 3, Fraction: 3.140000
```
REMARKS:
* You first use the format specifiers to tell the printf function what to expect, then after all the format specifiers specified, you give the placeholders for all the specifiers at the end. 
* And you see that the ```\n``` is added at the last, if we had added a ```\n``` after every single format specifier, we would have gotten the outputs in different lines. 

There is a simple way ```printf``` works, 
```c
printf(<format>, <what>);
```
* First you say what the format is and then specify what should be printed in the said format. 

### Structure of the block: 
```
{
	<declarations>
	<instructions>
}
```

```c
{
//here we declare just what the var is
int n;

//we give a value for the int and then instruct what to do with the var
n = 2;
	printf("%d\n", n);
}
```

#### Structure of declaration: 
```c
<type name> <identifier>  [= <initial value>] //this is optional 
```

```c
int n; //not initialized
int x = 2; //initialized
```

 ```c
  int n;
  ```
  here the var is undefined, so it is useless until we assign it some val

but for ```int x = 2``` it is not like that. We have given it a val of 2 right form the beginning. 

### Inputting data (user side):

Lets write a code to get a number from the user and output the square of it. 
```c
//Finding the square of a number
#include <stdio.h>
int main()
{
	int num; //declaring an int var 'num'
	printf("Please give an integer value: "); //printing the question 
	scanf("%d", &num); //scaning user input
	
	//printing user input and squared output
	printf("The square of %d is: %d\n", num, num*num); 
	return 0;
}
```

#### The usage of '&'
This is called the _address-of_ operator. 

* When the user inputs a data, we need to let it know _where_ to store that data. 
* And this '&' tells it where to go. Without this, it would be like delivering a pizza without an address. 
* There are cases where it is needed and where it isnt. 
  1. Basic format specifiers like ``` int, float, double, char``` need &
  2. But ``` strings and pointers``` dont because, a string is an array of chars

### if Statement
Lets write a program that decides if the inputted int is <10 or >10. 
![[Screenshot 2025-09-18 at 2.54.58.png|250]]
```
Let x be an int
OUT: info
IN: x
IF x < 10
	OUT: small
OTHERWISE
	OUT: big
```

```c
#include <stdio.h>
int main()
{
	int x; //defining x is an int
	printf("Enter number: "); //dialog for user
	scanf("%d", &x); //scaning user input and placing it in x
	if(x<10)
		printf("small");
	else
		printf("big");
return 0;
}
```


#### Syntax of the if statement
```c
if(x<10) //condition
	printf("small"); //true branch
else
	printf("big"); //false branch
```

or, we can have no false branch and only have absolute values like,
```c
if (a<0) 
	a = -a;
// here we only care about the true branch, if the statement if false, we simply ignore it. 
```

### Top-test loop - While statement

^24655d

##### Square of the int numbers between 1 and 10. 

```
Let n be an int 
n <-- 1
WHILE n <= 10
	OUT: n*n
	n <-- n+1
```

![[Screenshot 2025-09-18 at 3.21.12.png|250]]

```c
#include <stdio.h>
int main()
{
	int n;
	n=1; //initialisation
	while(n<=10) //condition
	{
		printf("%d\n", n*n);
		n=n+1; //incrementing n by 1 each time the loop runs
		// you can also write n+=1;
	}
return 0;
}
```

##### Finding zero of a function
We are searching the zeros of the function f(x) = x^2 - 2 between points n = 0 and p = 2, with eps = 0.001 accuracy. 

![[Screenshot 2025-09-18 at 3.32.19.png|250]]

```c
#include <stdio.h>
int main()
{
	double n=0.0, p=2.0; //assigning values for doubles n and p
	while (p-n > 0.001) // defining the eps value
	{
		double k=(n+p)/2.0; //finding midpoint
		if (k*k-2.0 > 0.0) //substituting midpoint into function
			p=k;
		else
			n=k;
	// if k*k-2.0 > 0.0 it implies that our point if to the right of the root, so we move p towards the left
	// if k*k-2.0 , 0.0 it implies that out point is to the left of the root, so we move n towards to right. 
	// we keep doing this until we reach the defined eps interval of p-n > 0.001.
	}
printf("The zero is: %f", n); //we print the n value because it is a safe underestimate of the exact root. We could also print p, but it would be 0.001 more than the current value. 
return 0;
}
```

### Higher Structured elements
#### Better prog of find the square (for statement) ^forstatement
Instead of using 3 separate lines of code for, 
1. Initialising n 
2. while looping construct
3. increment: `n+=1`
We can do both using a `for` _looping construct_

```c
#include <stdio.h>
int main()
{
	int n;
	for (n=1 ; n<=10 ; n+=1)
		printf("%d\n", n*n);
return 0;
}
```

```c
#include <stdio.h>
int main()
{
	for(int n=1; n<=10; n+=1)
		printf("%d\n", n*n);
return 0;
}
```
This does the same, but the `int` is defined inside the `for` loop, which is arguably better in most cases. 

##### Syntax of the for statement
`for(<initialization exp>; <condition exp>; <post-operation exp>)`

#### Printing the Multiplication Table
```c
#include <stdio.h>
int main()
{
int row; 
for(row=1; row<=10; row+=1)
{
	int col;
	for(col=1; col<=10; col+=1)
	{
		printf("%4d", row*col); //printing with decimal size of 4, there are 4 digits
	}
	printf("\n");
}
}
```

Here, there are 2 for loops. 
* The first one (going from the inside) will be the `col` for loop. 
   * This takes the int `col` and +1 if <=10 and then multiplies with the int `row` 
   * Once the for loop of `col` goes from 1 through 10,
	   * it jumps out of the for loop and, 
 * The for loop for `row` +1 if <=10. 
	 * This will happen for all `col` 1 through 10, then it will +1 for `row` and happen again for all `col` 1 through 10.... until `row` = 10.

[[Structogram; (Nassi-Shneiderman diagram)#^toptest]]

### Integer-value based selection
Execution of operations depending on the value of an integer expression
![[Screenshot 2025-09-18 at 9.43.24.png|500]]

This can also be structured as nestled selections, 
![[Screenshot 2025-09-18 at 9.44.00.png]]

#### The switch statement
lets write a prog that gives out grades from the given numbers, 
![[Screenshot 2025-09-18 at 9.53.22.png|600]]

This connects written evaluations to grades in numbers. 

```c
#include <stdio.h>
int main()
{
	int n;
	printf("Enter grade: ");
	scanf("%d", &n);
	switch (n)
	{
		case 1: printf("failed"); break;
		case 2: printf("poor"); break;
		case 3: printf("average"); break;
		case 4: printf("good"); break;
		case 5: printf("perfect"); break;
		default: printf("something wrong");
	}
return 0;
}
```

switch(n) looks at the value of n and tried to match it with one of the case labels, once it finds a match, execution jumps to that line. 

##### Syntax of switch statement
```
switch(<int exp>)
{
	case <const exp1>: <instruction 1>;
	case <const exp2>: <instruction 2>......
	default: <default instruction>
}
```


##### break;
this tells the switch () to break free from the execution after a case is met. 

This is better understood with an example. 
```c
#include <stdio.h>
int main()
{
	int n;
	printf("Enter grade ");
	scanf("%d", &n);
	switch(n)
	{
		case 1: 
		case 2: printf("Low grade\n"); break;
		case 3: printf("Average\n"); break;
		case 4:
		case 5: printf("High grade\n"); break;
		default: printf("Invaild\n"); break;
	}
return 0;
}
```
OUTPUT
1 - Low grade
2 - Low grade
3 - Average grade
4 - High grade 
5 - High grade

The constant exp are entry points, from this point on, all the instruction are executed until the first break or the end of the block. 

Without break; 
![[Screenshot 2025-09-18 at 10.06.31.png]]

### Arithmetic Types:
* In a real computer, the set of values of limited. 
* ie, you cannot represent,
	* arbitrary large num
	* arbitrary accuracy, pi != 3.1415
* You need to know the limits of what can rep to balance the minimise the loss of info while using reasonable amounts of memory


* void
* scalar
	* arithmetic
		* integer; int, char, enumerated
		* floating point
	* pointer
* function
* union
* compound
	* array
	* structure

- The binary representation of integers without any specification (`unsigned integers`) is stored in 8 bits. ![[Screenshot 2025-09-26 at 4.04.05.png|450]]
- So, in case of an unsigned int, if we have a value greater than 255, we get the remainder of it divided by 256, this is called `overflow`
	- We get _modulo 256 arithmetic_
	- 256 --> 0
	- 257 --> 1
	- 255+1 = 1
	- 255+2 = 2
	- *2 - 3 = 255*
![[Screenshot 2025-09-26 at 4.07.09.png|300]]

- so, instead of +ve numbers, if we wanted to represent -ve numbers in binary using *signed integers* as our arithmetic type, 
	- ![[Screenshot 2025-09-26 at 4.32.06.png|400]]
	- now lets see how the overflow is for this
		- The bounds are, 0, 127, -128, -1
			- 127 + 1= -128
			- 127 + 2 = -127
			- -127 - 3 = 126
			- 2 - 3 = -1
			- ![[Screenshot 2025-09-26 at 4.34.24.png|250]]

#### Signed vs Unsigned:
signed --> -ve 
unsigned --> +ve only, can't have any sign before the number

the sign of the int takes up 1 bit. 

#### Limits of the signed and unsigned int types
![[Screenshot 2025-09-26 at 4.42.05.png|650]]

```c
int i; //signed int
long int 1; //signed long int
```

```c
unsigned u; //unsigned int
short s; //signed short int
```

Here is what you need to notice here, 
	If there is a _sign_ or a _length modifier_ we can omit the `int` 


Now, here is an example program that runs for (585 000 years if the computer prints 1 million numbers per sec) using the table above
```c
#include <stdio.h> //for printf
#include <limits.h> //for integer limits

int main(void){
	long long 1; //almost all long long int
	
	for(i = LLONG_MIN ; i < LLONG_MAX ; i++)
		printf("%lld\n", i);

return 0;
}
```

#### Clever management of memory
say we need to find the selecting 12 out of 15 different chocolates, the math is 15!/(12.(15-12)!)

so, 15! = 1 307 674 368 000
12.3! = 2 874 009 600

None of these can be represented using int as they exceed 32 bits but a large margin... 

But just by doing some very simple math, we can obviously write it as, 
15.14.13 / 1.2.3

this becomes very simple now, all the numbers are super simple integers and hence the time taken for the algorithm, the memory used... everything decreases. 

#### Floating-point 

##### Normal Form

23.2457 = (-1)^0 . 2.3245700 . (10)^+001
-0.001822326 = (-1)^1 . 1.8223260 . (10)^-003 

The general form of a floating point is `sign bit` + `mantissa` + `exponent`
- sign bit represents the sign of the floating point, + or -
- mantissa is the unsigned int with the first digit always >=1
	- we basically write the number with 1 decimal point and 8 significant digits with a sign bit in the beginning. 

##### Binary Form

5.0 = 1.25 * 4 = (-1)^0 . 1.0100 (binary) . 2^(010) (binary)
Lets understnad, 

- First we need to write any number as a prod of the highest power of 2 possible, so for 5, it is 1.25 times 2^2 
- now, the first part is the sign bit
- the second part is the conversion of 1.25 to binary,
	- 1 --> 1
	- 0.25
		- 0.25 * 2= 0.5 --> 0
		- 0.5 * 2 = 1 --> 1
			- We keep repeating this until we reach, fractional part = 0
	- 1.25 --> 1.0100
		- We need to have 4 bits after the decimal
- the 3rd part is the 4 
	- 4 --> 2^2 --> 2^(010)
		- here we need to have 3 bits in the pow 
- ![[Screenshot 2025-09-26 at 6.24.51.png|300]]

- You can see that it is split into 3 parts,
	- Sign bit 
	- mantissa
	- exponent 
- The mantissa is important to understand,
	- we dont store 1.0100, instead we only store the 0100 because the leading 1 is _implied_ 
		- ==***This part is extremely important.***== 


- since we cannot represent irrational numbers, we give computers a place to stop. 
- We use E(epsilon), this is called the maximal error. 
	- by defining E to a very small number, we can get a very high accuracy. 


- now lets take a look at an example mantissa with 3 decimal places, but raised to 2 different exponents. 
	- This shows just how much difference there could be depending on the exponent.
	- And hence explains that there is no absolute accuracy in binary, only relative accuracy. 
		- You could have represented the mantissa to 3-4 decimal place accuracy, (this is generally a good accuracy for normal number system) but in binary, you simply cannot gauge that accuracy without knowing the exponent that mantissa is raised to. 
![[Screenshot 2025-09-30 at 11.17.25.png]]

- a simple way to understand floating point numbers is to think of them as scientific notation in the computer world. 

##### Chitty Chitty Bang Bang (recurrence in binary)
- The place where floating point inspite of all its insanely good optimisations and clever representation methods falls apart. 

- Lets take an example, 0.1 (decimal) 
	- This is represented in binary as: 0.000110011001100110011.....(binary) 
		- This is the problem, 0.1(decimal) is a finite number in the decimal system, but it is a recurring number in the binary system. 

- Computers dont understand recurrance, so they just represent it to the maximum number of digits possible, 
	- when dealing with the recurring binary numbers, computers will make very rudimentary mistakes, 
	- 0.1(decimal) + 0.2(decimal) = 0.3(decimal) 
		- but when doing this computationally, the computer will not output 0.3. 

- There is also a similar problem when dealing with v.large numbers and v.small numbers in the same go. 
- Since the mantissa can only represent the number (irrespective of its size) with a limited number of bits.

	- 10,000,000 + 1; lets take the bigger number to be A and the smaller to be a. 
		- 1.0000000 x 10^7 + 1 x 10^0 
		- Since the bigger number is 10^7 we also have to represent 1 as a product of 10^7 
		-  ![[Screenshot 2025-09-30 at 13.03.43.png|300]]
		- if our precision limit was just 7 digits, we would simply get 10,000,000 as the output. 

*==IMPORTANT IMPORTANT IMPORTANT IMPORTANT IMPORTANT IMPORTANT IMPORTANT==* 
- So, the important thing with floating point numbers is that, 
	- A + a - A != a
		- this is because the larger number _eats away_ at the smaller one. 


#### Floating point infinites

as we discussed earlier, 0.1(decimal) = 0.000110011... (binary)

```C
double d
for( d = 0.0 ; d < 1.0 ; d += 0.1)
{

}
```

_although this seems very very simple (just adding 0.1 to 0 until we reach 1) and you might think that this program has 10 steps, it actually has INFINITE steps due to the floating point rounding error_

And alternate for this would be, 
```c
double d;
double eps = 1e-3; //this is just 10^(-3)

for( d = 0.0 ; d< 1.0-eps ; d += 0.1) //now this program has 10 steps
{

}
```

_this is the extremely important use of epscillon_


