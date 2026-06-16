## TOPIC 1: 
#### Divisibility: 

let $a,b$ $\in$ $\mathbb{Z}$ such that $a=bx$ where $x$ is some integer
	This is the definition of divisibility


If $a|b$ and $b|c$ it automatically implies that $a|c$ this is because, 
$a=bx$
$b=cy$
let $xy$ be some $z$ where $x,y,z \in \mathbb{Z}$ 
$\implies a=zc$
$\implies a|c$ 


#### Prime Numbers: 
$|p| \geq 1$ 

Whenever $p$ is written as a combination of 2 number $a,b$ they are nothing other than $\pm {1}$ and $p$ itself

0 is not a prime number because $|0|\leq 1$

#### Fundamental Theorem of Arithmetic:

Every integer different from $0$ and $\pm{1}$ can be written as a product of prime numbers

Every int $|n|> 1$ can be factored into primes

This representation is unique "upto" the order and sign of the factors, 
- All this means is that the order and the sign of the prime factors dont matter
- But the number of primes and the primes itself always form a unique combination for every-single-number!

## TOPIC 2:
#### Congruences: 

For integers $a,b$ and $m>0$,

$a\equiv b \pmod{m}$ iff $m|(a-b)$ 
_super simple,_

#### Operations with congruences:

let, $a\equiv b \pmod{m}$ and $c\equiv d \pmod{m}$ this now means, _NOTE THAT BOTH HAVE $\pmod{m}$_
1. $a+c\equiv b+d \pmod{m}$ 
2. $ac\equiv bd \pmod{m}$
3. $a-c\equiv b-d \pmod{m}$
4. $a^k \equiv b^k \pmod{m}$

But what about division? 
$40\equiv 64 \pmod{12}$
lets divide both sides by $8$
$5\equiv 8 \pmod{12}$
$\implies 12|-3$ 
- But this is not true!!

There is a special condition for division. 
Division is only allowed when $(c,m)=1$ ie, $c,m$ are _coprimes_

_"Division in congruences is only valid when the divisor is coprime to the modulus"_

#### Linear Congruences:

$ax\equiv b\pmod{m}$

this is a linear congruence. 

This has solutions iff, 
$gcd(a,m) | b$ 

Lets take, $gcd(a,m)=d$ where $d \in \mathbb{Z}$ then, the number of solutions to the linear congruence will be, $d$ and the solutions are, $x=x_0 + k\frac{m}{d}$ where $k=0,1,2,...,d-1$ (so it totals up to $d$ solutions cuh).

$ax\equiv b \pmod{m}$
$gcd(a,m)=d$ such that $d \in \mathbb{Z}$

$ax\equiv b\pmod{m}$ literally means, 
$ax-b=km$ for some $k \in \mathbb{Z}$
_this is the Diphantine relationship between congruences and linear equations_

W.K.T; $ax\equiv b \pmod{m}$ has a solution(s) iff $d|b$ 

Assuming $d|b$, 
$a=a'd$ ; $m=m'd$ ; $b=b'd$ where $gcd(a',m')=1$ 

now the linear congruence can be written as, 
$da'x\equiv db' \pmod{dm'} \implies m'|(a'x-b')$

which is the same as $a'x\equiv b' \pmod{m'}$ -->A
since $gcd(a',m')=1$ using _Bezout's_ identity; 
$a'u + m'v =1$

This reduce modulo $m'$,
$a'u=1 \pmod{m}$
this means $u$ is the inverse of $a'$ modulo $m'$

Which means, A can be reduced into,
$x\equiv b'u \pmod{m'}$
$x\equiv x_0 \pmod{m'}$

where $x$ has exactly 1 solution. 

$m=dm'$
$x=x_0 + tm'$ where $t \in \mathbb{Z}$

#### Extended Euclidean algo: 
EEA computes, $gcd(a,b)$ and integers $x,y$ such that $ax+by=gcd(a,b)$ 

What is Euclidean algorithm? 

Working basis: $a=qb+r$ where $q$ is the $Quotient$ and $r$ is the $Remainder$ it is implied that,
$$
gcd(a,b) = gcd(b,r)
$$

Lets take an example: $gcd(56,15)$
$$
56 = (3)15+11
$$
$$
15=(1)11+4
$$
$$
11=(2)4+3
$$
$$
4=(1)3+1
$$
$$
3=(3)1+0
$$

one we have reached $r=0$ we take a look at the $b$ and that is our GCD.

Hence, $gcd(56,15)=1$
___
Now lets come to EEA, 
this uses the principle, $gcd(a,b)=d\implies ax+by=d$
so, $56x+15y=1$. And, EEA also finds $x,y$ (_simple_)

#### Determinants: 
- It is the scaling effect of a transformation
- Measures the magnitude of the scaling and the final orientation. 
- _For a square linear system it tells us if there is a unique solution_

- if det(A) /= 0 => Ax = b has a unique sol for every b.
	- The matrix A is invertible 

CONNECTION BETWEEN DETERMINANTS AND GAUSSIAN ELIM: 
- if after gaus elim we end up with a row echelon form => the det is /= 0. 
	- This means that there is a pivot for every variable
	- this means that there is a unique solution


- Swapping 2 rows => Sign change
- Multiple by some scalar $\Lambda$ => det is also multiplied by $\Lambda$
- Addition of a multiple of a row to another => unchanged

COMPUTATION USING GAUS ELIM: 
- reduce into upper triangle form using row ops
- det is the prod of the diagonal entries

#### Matrix Operations: 
Addition: All normal and ONLY can be done for matrices of same size

MULTIPLICATION: 
- Order matters

TRANSPOSE: 
- Appling 2 times - same matrix out
- AB whole transpose = b transpose times A transpose

