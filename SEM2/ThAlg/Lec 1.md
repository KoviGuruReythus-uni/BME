## Practise
1. Compare the functions to $O(n^2)$, $\Theta(n^2)$ and $\Omega(n^2)$
	1. $f(n)=11n^2+10000$ 
		1. Exact same growth rate as $n^2$ so, $\Theta(n^2)$
	2. $f(n)=8n^2log_2n$ 
		1. At $n\to\infty$ (which is all we really care about) the function AT ITS WORST acts like $n^2$ which is more or less the definition of $\Omega(n^2)$
	3. $f(n)=1.5n+3\sqrt{n}$ 
		1. The function is no were nearly as big as $n^2$ at $n\to\infty$ so, $n^2$ is its _UPPER BOUND_ hence, $O(n^2)$ 
2. PROVE
	1. $n^2-4n+7\in\Theta(n^2)$ 
	2. 

