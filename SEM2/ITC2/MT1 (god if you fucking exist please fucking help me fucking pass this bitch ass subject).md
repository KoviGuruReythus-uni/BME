# Rough Pass
_I am trying to solve the problems directly without doing the whole theory first and whatever I learn I write it here_
___
Sum of degree in a _tree_ is the double of the number of edges it has
- $\Sigma deg=2|E|$ (this is the handshake theorem)
___
A connected graph has a euler trail iff it has EXACTLY 0 or 2 vertices with odd degree
- O odd degree vertices - the trail starts and ends at the same vertex
- 2 odd degree vertices - the trail starts at one and ends at the other
- Anything else - no fucking trail
___
*Hamilton cycle* is a cycle that visits every vertex exactly once and returns to the start. 

_Existence_ - Dirac's theorem
- If every vertex has degree $\geq$ $\frac{n}{2}$ cycle exists

_Inexistence_ 
- find a set S of vertices whose removal leaves more than |S| components
___
Bipartite graph - a graph where you can split all the vertices into 2 sets such that there is no edge between the members of one set, all the edges go between the sets.

No odd cycles 

bipartite $\leftrightarrow$ no odd cycles $\leftrightarrow$ no hamilton cycle

Chromatic number of any bipartite graph = 2
- Set A gets one colour and B get another

if the graph is NOT bipartite then, $\chi \geq 3$ 
___
Complement ($G^-$) - The complement of $G$ has the same vertices but opposite edges, all the edges that existed now dont and the ones that didn't now do.
___
Matching - the set of edges that do not share a vertex

Vertex Cover - All the edges have atleast one endpoint with atleast one of the vertex in this set

Maximum matching - $v(G)$
Minimum vertex cover - $\tau(G)$

Always - $v(G) \leq \tau (G)$ 
___
## Summary for the summary?? idek what is going on anymore lol

TREES 
n vertices <-> n-1 edges 
Handshake theorem - $\Sigma d(G) = 2|E(G)|$ 

EULER TRAILS
Exists -> Exactly 0 or 2 odd degree vertices (and G is connected)

Minimum walk covering all the edges = |E| + (number of odd degree vertices -2)/2

BFS
