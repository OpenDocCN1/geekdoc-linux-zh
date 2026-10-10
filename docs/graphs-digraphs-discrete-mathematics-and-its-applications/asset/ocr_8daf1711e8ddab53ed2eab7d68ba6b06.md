Since $\alpha(G') \le \alpha(G)$ by the construction of $G'$, it follows that

$\chi(G') \ge \frac{|V(G')|}{\alpha(G')} \ge \frac{|V(G')|}{\alpha(G)} = |S|.$  (15.6)

Consequently, by (15.5) and (15.6), we have

$\chi(G') \ge |S| > |S| - 1 = \omega(G')$, which contradicts (15.4).

Lovász [158] obtained another characterization of perfect graphs (see Exercise 26).

**Theorem 15.11** *A graph $G$ is perfect if and only if $|V(H)| \le \alpha(H) \cdot \omega(H)$ for every induced subgraph $H$ of $G$.*

# The Strong Perfect Graph Theorem

As we have mentioned, if $G$ is an odd cycle of length 5 or more or is the complement of such an odd cycle, then $\chi(G) \neq \omega(G)$. In 1961 Claude Berge conjectured that this fact is critical in determining whether a graph is perfect.

**The Strong Perfect Graph Conjecture** *A graph $G$ is perfect if and only if neither $G$ nor $\bar{G}$ contains an induced odd cycle of length 5 or more.*

After an intensive 28-month assault on this conjecture, its truth was established in 2002 by Maria Chudnovsky, Neil Robertson, Paul Seymour and Robin Thomas [53].

**Theorem 15.12** (The Strong Perfect Graph Theorem) *A graph $G$ is perfect if and only if neither $G$ nor $\bar{G}$ contains an induced odd cycle of length 5 or more.*

# 15.3 List Colorings

In recent decades there has been increased interest in colorings of graphs in which the color of each vertex is to be chosen from a specified list of allowable colors. Let $G$ be a graph for which there is an associated set $L(v)$ of permissible colors for each vertex $v$ of $G$. The set $L(v)$ is commonly called a **color list** for $v$. A **list coloring** of $G$ is then a proper coloring $c$ of $G$ such that $c(v) \in L(v)$ for each vertex $v$ of $G$. A list coloring is also referred to as a **choice function**. If

$\mathfrak{L} = \{L(v) : v \in V(G)\}$