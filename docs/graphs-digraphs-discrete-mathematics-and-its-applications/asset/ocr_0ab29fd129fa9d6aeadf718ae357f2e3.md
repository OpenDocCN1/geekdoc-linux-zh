1-factors for $1 \leq i \leq k-1$ and let $G_{k}$ be the $(s_{k}-2)$-regular spanning subgraph obtained from $s_{k}-2$ of these 1-factors. Since $\sum_{i=1}^{k-1}(s_{i}-1)+(s_{k}-2)=s-1$, it follows that $\{G_{1},G_{2},\ldots,G_{k}\}$ is a factorization of $K_{n}$. Assigning the color $i$ to the edges in $G_{i}$ for each $i$ ($1\leq i\leq k$) produces a $k$-edge coloring of $K_{n}$ having no subgraph $K_{1,s}$, all of whose edges are colored $i$ for all $i$ ($1\leq i\leq k$). Thus, $n \geq s+1$ and so $n=s+1$.

For example,

```
```
R(K_{1,3},K_{1,5},K_{1,7}) = (3-1)+(5-1)+(7-1)+2 = 14, where t=0
R(K_{1,4},K_{1,5},K_{1,7}) = (4-1)+(5-1)+(7-1)+2 = 15, where t=1
R(K_{1,4},K_{1,6},K_{1,7}) = (4-1)+(5-1)+(7-1)+1 = 14, where t=2
```
```

# **Corollary 20.14**

For integers $s,t\geq 2$,

```
```
R(K_{1,s},K_{1,t}) = { s + t - 1   if s and t are both even
                   { s + t        otherwise.
```
```