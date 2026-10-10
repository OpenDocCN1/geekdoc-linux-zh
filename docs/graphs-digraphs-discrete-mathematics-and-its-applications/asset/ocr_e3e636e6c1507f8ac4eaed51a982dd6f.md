# **15.1. PERFECT GRAPHS**

**Proof.** Let $G$ be a graph of order $n$ such that $\overline{G}$ is bipartite. Since the complement of every (nontrivial) induced subgraph of $G$ is also bipartite, to verify that $G$ is perfect, it suffices to show that $\chi(G) = \omega(G)$. Suppose that $\chi(G) = k$ and $\omega(G) = \ell$. Then $k \geq \ell$. Let there be given a $k$-coloring of $G$. Then each color class of $G$ consists either of one or two vertices; for if $G$ contains a color class with three or more vertices, then this would imply that $\overline{G}$ has a triangle, which is impossible.

Of the $k$ color classes, suppose that $p$ of these classes consist of a single vertex and that each of the remaining $q$ classes consists of two vertices. Hence, $p + q = k$ and $p + 2q = n$. Let $W$ be the set of vertices of $G$ belonging to a singleton color class. Since every two vertices of $W$ are necessarily adjacent, $G[W] = K_p$ and so $\overline{G}[W] = \overline{K}_p$.

Since no $k$-coloring of $G$ results in more than $q$ color classes having two vertices, it follows that $\overline{G}$ has a set $M$ of $q$ pairwise nonadjacent edges but no more than $q$ such edges. We claim that for each edge $uv \in M$, either $u$ is adjacent to no vertex of $W$ or $v$ is adjacent to no vertex of $W$ in $\overline{G}$. Suppose that this is not the case. Then we may assume that $u$ is adjacent to some vertex $w_1 \in W$ and $v$ is adjacent to some vertex $w_2 \in W$ in $G$. Since $\overline{G}$ is triangle-free, $w_1 \neq w_2$. However then, $(M \setminus \{uv\}) \cup \{uw_1, vw_2\}$ is a set of $q + 1$ pairwise nonadjacent edges in $\overline{G}$. This, however, is impossible and so, as claimed, for each edge $uv$ in $M$ either $u$ is adjacent to no vertex of $W$ or $v$ is adjacent to no vertex of $W$.

Therefore, $G$ contains an independent set of at least $p + q = k$ vertices and so $\omega(G) = \ell \geq k$. Hence, $\chi(G) = \omega(G)$. ■

# Interval Graphs

For a collection $S = \{I_1, I_2, \dots, I_n\}$ of finite closed intervals of real numbers, the **interval graph** $G$ representing $S$ has vertex set $V(G) = \{v_1, v_2, \dots, v_n\}$ where $v_iv_j \in E(G)$ if $I_i \cap I_j \neq \emptyset$. If $G$ is an interval graph, then every induced subgraph of $G$ is also an interval graph (see Exercise 11). In the definition of “interval graph”, we arrive at the same concept if open intervals are used rather than closed intervals. Indeed, we can use half-open (half-closed) intervals or a mixture of any of these (see Exercises 13 and 15).

For example, the graph $G$ in Figure 15.4 a is an interval graph as can be seen by considering the five intervals $I_1 = [0,2]$, $I_2 = [1,5]$, $I_3 = [3,6]$, $I_4 = [4,8]$, $I_5 = [7,9]$, where $v_i$ and $v_j$ are adjacent in $G$, $1 \leq i,j \leq 5$, if $I_i \cap I_j \neq \emptyset$. Observe that $\chi(G) = \omega(G) = 3$ for this graph $G$. This graph is also a perfect graph. Indeed, every interval graph is a perfect graph.

**Theorem 15.5** Every interval graph is a perfect graph.

**Proof.** Let $G$ be an interval graph with $V(G) = \{v_1, v_2, \dots, v_n\}$. Since every induced subgraph of an interval graph is also an interval graph, it suffices to show that $\chi(G) = \omega(G)$. Because $\overline{G}$ is an interval graph, there exist $n$ closed