What is the maximum connectivity of a graph with n vertices and m edges?

In 1962 Harary [119] answered Berge’s question by showing that for every pair $n,m$ of integers with $2 \leq n - 1 \leq m \leq \frac{2}{3}n$, there exists a graph $G$ of order $n$ and size $m$ with $\kappa(G) = \lfloor \frac{2m}{n} \rfloor$. Of course, if $m = n - 1 \geq 2$, every tree $T$ of order $n$ has the desired property since

$\kappa(T) = \lfloor \frac{2m}{n} \rfloor = \lfloor \frac{2n - 2}{n} \rfloor = 1.$

We observed that $\kappa(G) = 2$ and $\lambda(G) = 3$ for the graph $G$ of Figure 4.2. Since $\delta(G) = 4$, this graph shows that the two inequalities stated in Theorem 4.4 can be strict. The first of these inequalities cannot be strict for cubic graphs, however.

# Theorem 4.6 For every cubic graph $G$,

$\kappa(G) = \lambda(G)$.

**Proof.** For a cubic graph $G$, it follows that $\kappa(G) = \lambda(G) = 0$ if and only if $G$ is disconnected. If $\kappa(G) = 3$, then $\lambda(G) = 3$ by Theorem 4.4. So two cases remain, namely $\kappa(G) = 1$ and $\kappa(G) = 2$. Let $U$ be a minimum vertex-cut of $G$. Then $|U| = 1$ or $|U| = 2$ and so $G - U$ is disconnected. Let $G_{1}$ and $G_{2}$ be two components of $G - U$. Since $G$ is cubic, for each $u \in U$, at least one of $G_{1}$ and $G_{2}$ contains exactly one neighbor of $u$.

*Case 1.* $\kappa(G) = |U| = 1$. Thus, $U$ consists of a cut-vertex $u$ of $G$. Since some component of $G - U$ contains exactly one neighbor $w$ of $u$, the edge $uw$ is a bridge of $G$ and so $\lambda(G) = \kappa(G) = 1$.

*Case 2.* $\kappa(G) = |U| = 2$. Let $U = \{u, v\}$. Assume that each of $u$ and $v$ has exactly one neighbor, say $u'$ and $v'$, respectively, in the same component of $G - U$. (This is the case that holds if $uv \in E(G)$.) Then $X = \{uu', vv'\}$ is an edge-cut of $G$ and $\lambda(G) = \kappa(G) = 2$. (See Figure 4.3(a) for the situation when $u$ and $v$ are not adjacent.)

![](bbox=[0.12, 0.81, 0.45, 0.95])

![](bbox=[0.5, 0.81, 0.85, 0.95])

Figure 4.3: A step in the proof of Case 2