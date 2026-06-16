## Lecture 1

#### Proof of min search lower bound being $n-1$ number of searches
- For us to be sure that the other n-1 elements are all NOT the minimum, we need atleast n-1 comparisons. Each comparison eliminates one element, therefore, we need atleast n-1 comparisons to eliminate n-1 elements. 


#### $O$ informal explanation
- $f\in O(g)$ - There exists constants $c$ and $n_0$ such that $f(n)\leq c.g(n)$ for all $n\geq n_0$ 
- Under any circumstance, $f$ is smaller than $g$ multiplied by some constant $c$ and that this holds for all $n\geq n_0$

#### How to disprove $O$
- We use _contradiction_ to disprove $O$
- EXAMPLE: $100n\in O(n^2)$

$$
\\\begin{aligned}
&\ \implies 100n\leq c.n^2
\\&\ \implies 100\leq c.n
\\&\ \implies This\ in\ itself\ is\ a\ contradiction\ to\ what\ we\ are\ proving
\\\end{aligned}
$$
