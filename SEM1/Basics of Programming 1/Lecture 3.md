### Arithmetic Types
- There is a way to represent all the ASCII characters in C, including the numbers and special chars... 
- We used the modifier `char` 
- ![[Screenshot 2025-10-08 at 23.43.47.png|500]]
- We print this using `%c` as the format code. 
- ```c
  char ch = 0x61; //hex 61 = dec 97
  printf("%d: %c\n", ch,ch); 
  ch += 1; //hex 62 = dec 98
  printf("%d: %c\n", ch,ch);
  ```
OUTPUT:
`97: a
`98: b`

- you dont need to learn the ASCII codes to type out the chars,
	- Any character placed between ' ' is interpreted as a char

```c
char ch = 'a';
printf("%d: %c\n", ch,ch);
ch = ch+1;
printf("%d: %c\n", ch,ch);
```
- this has the same output as the prev code block

![[Screenshot 2025-10-08 at 23.49.30.png]]

- this also allows us to print out special character constants, 
	- in fact, we have been using `\n` all this time, 
	- ![[Screenshot 2025-10-08 at 23.51.04.png|300]]


#### Quirk of C W.R.T characters
- According to C, both characters and integers are basically the same, the difference only occurs when using printf, `%d` or `%c`, this decides what the character is interpreted as. 
- And hence, you can perform the same arithmetic operations using chars that you would with int or float or double... 
	- although this seem pretty useless now, it is kinda useful in application like this,
```c
#include <stdio.h>
int main(){
	char c;
	int sum = 0;
	do{
		scanf("%c", &c);
		if(c >= '0' && c <= '9'){
			sum = sum + (c - '0');
		}
	while (c != '\n');
	}
	printf("The sum is: %d\n", sum);
return 0;
}
```
- This code gets input from the user and then adds all of the integer values from the input. 
- To convert the inputed numbers from the `char` group to `int`, we do,
	- ` c - '0'`
	- THIS IS EXTREMELY IMPORTANT TO REMEMBER*******

### Functions
- As it might be obvious, functions are used when a same code block or operation might be needed multiple times with different parameters inside the same project. 
	- Instead of copy pasta, we define a function in the beginning and keep reusing it whenever needed, this is much more elegant and makes the code more legible and obv, saves time too. 

Lets take an example, 

_calculate the sum of the square of all the numbers less than 12!, (1 + 4 + 9... + 121)_

```c
#include <stdio.h>
int main(void) {
	int i, sum;
	
	sum=0;
	for(i=1; i<12; i++){
		sum = sum + i*i;
	}
	printf("The square sum is: %d\n", sum);
	return 0;
}
```

This is perfectly fine, but in case we needed to find the same but for values other than 12... We can simply define a fucntion in the beginning and keep reusing it in the code, 

```c
#include <stdio.h>
int squaresum(int n){ //we define the function here. The int n is the part where we tell the function what to expect later on. 
	int i, sum=0;
	for(i=1; i<n; i++){
		sum = sum + i*i;
	}
	return sum; //this is the part where we tell the function what to return, what to remember from the process. 
}

int main(void){ //obviously, this is the main program
	int sum1, sum2, sum3;
	
	sum1 = squaresum(12);
	sum2 = squaresum(24);
	sum3 = squaresum(40);
	
	printf("%d,%d,%d\n", sum1,sum2,sum3);
	return 0;
}
```

```c
#include <stdio.h>
int main() {
}
```
