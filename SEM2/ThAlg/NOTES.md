# Lecture 1

*INVARIANT:* 
- Initialisation
	- Prove the statement is true before the loop starts
- Maintenance
	- Assume it is true at the start of iteration i, prove it is still true at the start of iteration i+1

- Prove that a statement is true for i
- Prove it is also true for i+1
- Since it is true for any i and i+1, it is true for everything

_ORDER NOTATION:_
- We always take the upper limit as the run time for the algorithm (the worst case)
- Order notations are used to strip the function of everything but their most dominant term (we also ignore all constants)

- $f(n) \in O(g(n))$ if there exists constants,
	- $c$
	- $n_0$
		- Such that $f(n) \leq c.g(n), \forall n \geq n_0$ 
- $f(n) \in \Omega(g(n))$ if, 
	- $c$
	- $n_0$
		- Such that $f(n) \geq c.g(n), \forall n \geq n_0$
- if a function $f(n) \in O(g(n))$ and $f(n) \in \Omega(g(n))$ then $f(n) \in \Phi(n)$

- $O$ - my function grows at _most_ this fast
- $\Omega$ - my function grows _at least_ this fast
- $\Phi$ - my function grows _exactly_ this fast

___
# Lecture 2

- Recursive - Algo calls itself
- Iterative - repeats a certain loop some number of times

_DIVIDE AND CONQUER_
- Divide the problems into disjoint subproblems

_DYNAMIC PROGRAMMING_
- similar to divide and conquer but the subproblems are _not_ disjoint
- A _bottom-up_ storage system is required for this. 
- The subproblems heavily overlap and build upon each other.

1. Subproblems - definition of the sub problems
2. Order - Order of solving he sub problems
3. Start - Base cases
4. Continue - Method for solving later subproblems when the solution to the earlier sub problems is known
5. End - Solution of the problem using all sub problems
6. Correctness.- we will check individually for base cases, method and final answer 
7. Running time
8. Optimal Object 
___

# Lecture 3

_GRAPH REPRESENTATION_
_Adjacency Matrix_
- We write all the vertices as 2 axes (kinda) and mark if there is an edge between them or no
- This can be inefficient because not all vertices will have an edge between then, there could be a 1000 vertices and just 10 edges, then the matrix is filled with stupid ass 0s.

- Example: 
- ![[Screenshot 2026-04-21 at 11.53.22.png|195]]
- The _adjacency matrix_ uses $O(n^2)$ space regardless of how many edges we actually have 
- This is preferred when, 
	- The graph is small
	- the graph is dense (a lot of edges)

_Adjacency List_
- We store, for each vertex, its neighbours 
- ![[Screenshot 2026-04-21 at 11.56.24.png|133]]


_Comparison between the both_
- SPACE
	- matrix - $n^2$ 
	- list - $n+m$, here m is the number of edges and n is the number of vertices
- EDGE LOOKUP
	- matrix - $O(1)$
		- if edge $i\to j$ exists, it does, we can directly see the coordinate $i,j$ to see if it is 0 or 1
	- list - $O(n)$ we have to scan the list of vertex i's neighbours - Worst case, the whole list which is $O(n)$
___

# PROBLEMS

_We are given a country's road network as the adjacency matrix of an undirected weighted graph: vertices are the cities (n cities), edges are the direct roads between cities, and the weight of the edges is the expected time taken to travel the road. Given that some cities in the country have an ambulance station, we want to decide whether it is true that any city in the country can be reached from at least one ambulance station in at most M minutes. Which algorithm can be used to solve this problem in $O(n^2)$ running time, and how?_

- Since the graph is weighted and the weights are positive, we need to find the shortest distance from ambulance stations to city, Dijkstra is the correct approach here
- We will create a new node, $v_0$ this will connect to all the ambulance stations with a weight of 0. This means that Dijkstra will discover all the ambulance stations in one go without having to rerun the algorithm from each station. 
	- Run time: $O(n^3)$ _vs_ $O(n^2)$
- After Dijkstra is run, we will have the shortest distance from all the ambulance stations to the cities, we can then just compare the weights to $M$ 
- If there is a path from any ambulance station to any city, Dijkstra will find it and will do so in such a way that the path is the shortest - "At least one ambulance station in at most M minutes"
- The time taken to traverse a $n \times n$ adjacency list is $O(n^2)$ here, since we have one more vertex it is $O((n+1)^2)$ which is nearly the same as $O(n^2)$ 