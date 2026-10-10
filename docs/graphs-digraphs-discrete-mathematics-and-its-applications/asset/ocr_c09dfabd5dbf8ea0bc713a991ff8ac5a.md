if $\chi(H)<\chi(G)$ for every proper subgraph $H$ of $G$. If $G$ is a color-critical $k$-chromatic graph, then $G$ is called **critically $k$-chromatic** or simply **$k$-critical**.

The graph $K_2$ is the only 2-critical graph. In fact, $K_n$ is $n$-critical for every integer $n\geq 2$. The odd cycles are the only 3-critical graphs. There is no characterization of $k$-critical graphs for any integer $k\geq 4$.

Let $G$ be a $k$-chromatic graph, where $k\geq 2$, and suppose that $H$ is a $k$-chromatic subgraph of minimum size in $G$ having no isolated vertices. Then for every proper subgraph $F$ of $H$, $\chi(F)<\chi(H)$, that is, $H$ is a $k$-critical subgraph of $G$. From this observation, it follows that every $k$-chromatic graph, $k\geq 2$, contains a $k$-critical subgraph. By Corollary 14.5, every $k$-critical graph, $k\geq 2$, must be connected; while by Theorem 14.6, every $k$-critical graph, $k\geq 3$, must be 2-connected and therefore 2-edge-connected. The following theorem tells us even more.

# **Theorem 14.13** Every $k$-critical graph, $k\geq 2$, is $(k-1)$-edge-connected.

**Proof.** The only 2-critical graph is $K_2$, which is 1-edge-connected; while the only 3-critical graphs are odd cycles, each of which is 2-edge-connected. Since the theorem holds for $k=2,3$, we may assume that $k\geq 4$.

Suppose that there is a $k$-critical graph $G$, $k\geq 4$, that is not $(k-1)$-edge-connected. This implies by Theorem 4.2 that there exists a partition $\{V_1, V_2\}$ of $V(G)$ such that the number of edges joining the vertices of $V_1$ and the vertices of $V_2$ is at most $k-2$. Since $G$ is $k$-critical, the two induced subgraphs

```
$$G_1=G[V_1]\quad G_2=G[V_2]$$
```

are $(k-1)$-colorable. Let there be given colorings of $G_1$ and $G_2$ from the same set of $k-1$ colors and suppose that $E'$ is the set of edges of $G$ that join the vertices in $V_1$ and the vertices in $V_2$. It cannot occur that every edge in $E'$ joins vertices of different colors, for otherwise, $G$ itself is $(k-1)$-colorable. Hence, there are some edges in $E'$ joining vertices that are assigned the same color. We now show that there exists a permutation of the colors assigned to the vertices of $G$ that results in a proper coloring of $G$ in which every edge of $E'$ joins vertices of different colors, which again shows that $G$ is $(k-1)$-colorable, producing a contradiction.

Let $U_1, U_2, \ldots, U_t$ denote the color classes of $G_1$ for which there is some vertex in $U_i$ ($1\leq i\leq k-2$) adjacent to a vertex of $V_2$. Suppose that there are $k_i$ edges joining the vertices of $U_i$ and the vertices of $V_2$. Then each $k_i\geq 1$ and

```
$$\sum_{i=1}^{t} k_i\leq k-2.$$
```

If, for every vertex $u_i\in U_1$, the neighbors of $u_i$ are assigned a color different from that assigned to $u_1$, then the color of the vertices in $U_1$ is not altered. If, on the other hand, some vertex $u_i\in U_1$ is adjacent to a vertex in $V_2$ that is colored the same as $u_1$, then the $k-1$ colors used to color the vertices of $G_1$