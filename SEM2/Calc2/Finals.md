# WRITTEN

## Topics to cover
- [x] Estimating change in specific direction
- [x] Searching for local extreme values
- [ ] Double integral to find the volume
- [ ] Double integral to find the area
- [ ] Double integral to find the moments and centre of mass
- [ ] Double integral to find the average value of f over R
- [ ] Double integral in polar form
- [ ] Substitutions in double and triple integrals
- [ ] Triple integral to find the volume
- [ ] Triple integral in cylindrical and spherical coordinates
___
## Estimating change in specific direction

$\boxed{D_uf(x,y) = \nabla f(x,y). {u}}$ 
- $\nabla f(x,y) = \langle f_x, f_y \rangle$ 
- $u$ - *unit* vector in the direction that we want

_EXPLANATION_: 
- It is the change in both x and y in the direction of $u$. We dot $u$ and $\nabla f$ and since $u$ is simply just a unit vector, we inherit its direction and nothing else. 
- Change of $x,y$ in the direction of $u$
___
## Searching for local extreme values
### First derivative test for local extrema
If $f(x,y)$ has a $M$ or $m$ at an interior point $(a,b)$ of its domain and *IF* the partial derivatives exist there, then $f_x(a,b) = f_y(a,b) = 0$

We look at *critical points* 
- $f_x,~f_y$ are either,
	- both zero
	- either one or both do not exist

At these critical points, we might end with the extrema, or a *saddle point* 

- To clearly differentiate between the extrema (either M or m) and the saddle point, we introduce the *Second derivate test*

### Second derivative test for local extrema
*quick interlude*

$$
\boxed{Hessian~=~H~=~f_{xx}f_{xy} - f_{xy}^2 ~=~
\begin{vmatrix}
f_{xx} & f_{xy} \\
f_{xy} & f_{yy}
\end{vmatrix}}
$$
- The Hessian is the transformation matrix we use (very interesting shit tbh)


- $f(x,y)$ is continuous
- $f_x(a,b)~ =~f_y(a,b)~=~0$ 
	1. $f$ has a local maxima ($M$) at $(a,b)$  
		- $f_{xx}<0$ 
		- $H>0$ at $(a,b)$ 
	2. $f$ has a local minima ($m$) at $(a,b)$ 
		- $f_{xx} > 0$  
		- $H>0$ at $(a,b)$ 
	3. Saddle point
		- $H<0$ 
	4. Inconclusive
		- $H=0$

| $H>0$ |              | Saddle |
| ----- | ------------ | ------ |
|       |              |        |
| $H<0$ |              |        |
|       | $f_{xx} < 0$ | Maxima |
|       | $f_{xx}>0$   | Minima |
|       |              |        |
| $H=0$ |              | idfk   |
___
## Double integral to find Volume
