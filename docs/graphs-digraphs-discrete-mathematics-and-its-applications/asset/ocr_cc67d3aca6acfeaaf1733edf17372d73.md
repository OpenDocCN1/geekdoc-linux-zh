# Blocks

Let $G$ be a nontrivial connected graph. A **block** of $G$ is a maximal nonseparable subgraph of $G$; that is, a block of $G$ is a nonseparable subgraph of $G$ that is not a proper subgraph of any nonseparable subgraph of $G$. Every two distinct blocks of $G$ have at most one vertex in common; and if they have a vertex in common, then this vertex is a cut-vertex of $G$. A block of $G$ containing exactly one cut-vertex of $G$ is called an **end-block** of $G$. If $B$ and $B'$ are two blocks containing the cut-vertex $v$, while $u \in V(B)$ and $w \in V(B')$ for $u, w \neq v$, then every $u-w$ path in $G$ must contain the vertex $v$. This is essentially Theorem 3.2. A graph $G$ and its five blocks $B_i$, $1 \le i \le 5$, are shown in Figure 3.2. The end-blocks of $G$ are $B_1$, $B_2$ and $B_5$. A connected graph with cut-vertices must contain two or more end-blocks.

![](bbox=[0.2, 0.4, 0.85, 0.75])

# **Theorem 3.7** *Every connected graph containing cut-vertices has at least two end-blocks.*

**Proof.** If $G$ contains only one cut-vertex, then every block of $G$ is an end-block. Hence, we may assume that $G$ contains two or more cut-vertices. Among all pairs of cut-vertices of $G$, let $u, v$ be a pair for which $d(u, v)$ is a maximum and let $P$ be a $u-v$ geodesic, say
$$P=(u=u_0, u_1, \ldots, u_k = v), \text{ where } k \geq 1. \tag{*}$$
Then $u_1$ belongs to a block $B$ and $u_{k-1}$ belongs to a block $B'$, where possibly $B = B'$. In fact, possibly $u_1 = v$. Since $u$ is a cut-vertex of $G$, it follows