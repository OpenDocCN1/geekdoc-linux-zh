18. For a given positive integer $n$, determine all graphs of order $n$ for which the two bounds in Theorem 14.9 are equal.

19. Let $k \geq 2$ be an integer. For each integer $i$ with $1 \leq i \leq 2k + 1$, let $G_i$ be a copy of $K_k$. The graph $G$ of order $2k^2 + k$ is obtained from the graphs $G_1, G_2, \ldots, G_{2k+1}, G_{2k+2} = G_1$ by joining each vertex in $G_i$ to every vertex in $G_{i+1}$ ($1 \leq i \leq 2k + 1$). Compute the bounds $n/\alpha(G)$, $n + 1 - \alpha(G)$ and $\omega(G)$ for $\chi(G)$ for an arbitrary $k \geq 2$. Determine $\chi(G)$.

20. Give an example of a graph $G$ of order $n$ for which $n/\alpha(G)$ is an integer and for which $\chi(G)$ is none of the numbers $n/\alpha(G), n-\alpha(G)+1$ and $\omega(G)$.

21. Give an example of a graph $G$ with $\chi(G) = \alpha(G)$ but no $\chi(G)$-coloring of $G$ results in a color class containing $\alpha(G)$ vertices.

22. Does there exist a $k$-chromatic graph $G$ in which no color class of a $k$-coloring of $G$ contains at least $\alpha(G) - 2$ vertices?

23. Let $k \geq 2$ be an integer. Prove that if $G$ is a $k$-colorable graph of order $n$ such that $\delta(G) > \left(\frac{k-2}{k-1}\right)n$, then $G$ is $k$-chromatic. Is the bound sharp?

24. Prove that a connected graph $G$ has chromatic number at least 3 if and only if for every vertex $v$ of $G$, there exist two adjacent vertices $u$ and $w$ in $G$ such that $d(u,v) = d(v,w)$.

25. Recall that an independent set $S$ of vertices in a graph $G$ is maximal if $S$ is not a proper subset of any other independent set of vertices in $G$. The **upper chromatic number** $\overline{\chi}(G)$ of a graph $G$ is the maximum number of maximal independent sets of vertices into which $V(G)$ can be partitioned.

+   - (a) Show that the upper chromatic number of a graph need not be defined.

+   - (b) Show that if the upper chromatic number $\overline{\chi}(G)$ of a graph $G$ is defined, then $\overline{\chi}(G) \geq \chi(G)$.

+   - (c) Give an example of a graph $G$ for which $\overline{\chi}(G)$ is defined and determine $\overline{\chi}(G)$ for this graph $G$.

26. (See Exercise 25 for the definitions of maximal independent sets of vertices and the upper chromatic number $\overline{\chi}(G)$ of a graph $G$.)

+   - (a) Let $G$ be a graph with $\overline{\chi}(G) = k$ and let $\{V_1, V_2, \ldots, V_k\}$ be a partition of $V(G)$ into $k$ maximal independent sets. Let each vertex of $V_i$ ($1 \leq i \leq k$) be assigned the color $i$. Show that if any vertex of $G$ is assigned a different color in $\{1, 2, \ldots, k\}$, then the resulting coloring is not proper.