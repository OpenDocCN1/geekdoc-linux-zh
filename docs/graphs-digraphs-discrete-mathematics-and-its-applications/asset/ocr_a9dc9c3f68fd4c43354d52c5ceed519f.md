# The Nordhaus–Gaddum Theorem

We have seen that $\chi(K_n)=n$ and $\chi(\overline{K_n})=1$. So, $\chi(K_n)+\chi(\overline{K_n})=n+1$. By Theorem 14.1, if $G$ is a graph such that $\overline{G}$ is a nonempty bipartite graph, then $\chi(\overline{G})=2$, while $\chi(G)\leq n-1$. Thus, $\chi(G)+\chi(\overline{G})\leq n+1$. Edward A. Nordhaus and Jerry W. Gaddum [178] showed that this inequality holds for all graphs $G$ of order $n$ when they established two pairs of inequalities involving the sum and product of the chromatic numbers of a graph and its complement. Such inequalities established for any parameter have become known as **Nordhaus–Gaddum inequalities**. The following proof is due to Hudson V. Kronk (see [49]).

**Theorem 14.23 (The Nordhaus–Gaddum Theorem)** If $G$ is a graph of order $n$, then

+   (i) $2\sqrt{n} \leq \chi(G)+\chi(\overline{G}) \leq n+1$  
+   (ii) $n \leq \chi(G) \cdot \chi(\overline{G}) \leq \left(\frac{n+1}{2}\right)^2$.

**Proof.** Suppose that $\chi(G)=k$ and $\chi(\overline{G})=\ell$. Let a $k$-coloring $c$ of $G$ and an $\ell$-coloring $\bar{c}$ of $\overline{G}$ be given. Using these colorings, we obtain a coloring of $K_n$. With each vertex $v$ of $\overline{G}$ (and of $G$), we associate the ordered pair $(c(v), \bar{c}(v))$. Since every two vertices of $K_n$ are either adjacent in $G$ or in $\overline{G}$, they are assigned different colors in that subgraph of $K_n$. Thus, this is a coloring of $K_n$ using at most $k\ell$ colors. Therefore,

$$n = \chi(K_n) \leq k\ell = \chi(G) \cdot \chi(\overline{G}) .$$

This establishes the lower bound in (ii). Since the geometric mean of two positive real numbers never exceeds their arithmetic mean, it follows that

$$\sqrt{n} \leq \sqrt{\chi(G) \cdot \chi(\overline{G})} \leq \frac{\chi(G) + \chi(\overline{G})}{2}, \tag{14.3}$$

Consequently,

$$2\sqrt{n} \leq \chi(G) + \chi(\overline{G}) ,$$

which verifies the lower bound in (i).

To verify the upper bound in (i), let $p = \max\{\delta(H)\}$, where the maximum is taken over all subgraphs $H$ of $G$. Hence, the minimum degree of every subgraph of $G$ is at most $p$. By Theorem 14.19, $\chi(G) \leq 1+p$.

We claim that the minimum degree of every subgraph of $\overline{G}$ is at most $n-p-1$. Assume, to the contrary, that there is a subgraph $H$ of $\overline{G}$ such that $\delta(\overline{H}) \geq n-p$ for the subgraph $\overline{H}$ in $\overline{G}$. Thus, every vertex of $H$ has degree $p-1$ or less in $G$. Let $F$ be a subgraph of $G$ such that $\delta(F) = p$. So, every vertex of $F$ has degree $p$ or more in $G$. This implies that no vertex of $F$ belongs to $H$. Since the order of $F$ is at least $p+1$, the order of $H$ is at most $n-(p+1) = n-p-1$.