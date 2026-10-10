# 3.4. THE MINIMUM SPANNING TREE PROBLEM

the edges $e_1$, $e_2$, …, $e_{k+1}$, where $0 \leq k < n-1$. If $k=0$, let $U=\{u\}$; while if $k \geq 1$, let $U$ be the set of $k+1$ vertices that are incident with one or more of the edges $e_1$, $e_2$, …, $e_k$. By Prim’s Algorithm, $e_{k+1}$ joins a vertex of $U$ and a vertex of $V(T)-U$.

The subgraph $H+e_{k+1}$ therefore contains a cycle $C$ and $e_{k+1}$ is on $C$. Necessarily, $C$ contains an edge $e_0$ distinct from $e_{k+1}$ such that $e_0$ also joins a vertex of $U$ and a vertex of $V(T)-U$. By the construction of $T$ from Prim’s Algorithm, $w(e_{k+1}) \leq w(e_0)$. Now $T'=H+e_{k+1}-e_0$ is a spanning tree of $G$ whose weight is

$$w(T') = w(H) + w(e_{k+1}) - w(e_0).$$

Since $H$ is a minimum spanning tree, $w(H) \leq w(T')$ and so $w(H) \leq w(H) + w(e_{k+1}) - w(e_0)$, which implies that $w(e_0) \leq w(e_{k+1})$. Consequently, $w(e_0)=w(e_{k+1})$ and $w(H) = w(T')$. Therefore, $T'$ is also a minimum spanning tree of $G$. If $e_0$ does not belong to $T$, then $T'$ is a minimum spanning tree having more edges in common with $T$ than $H$ does, which is impossible since $H \in \mathcal{H}$. Hence $e_0$ belongs to $T$, which implies that $T'$ has the same number of edges in common with $T$ as $H$ does and so $T' \in \mathcal{H}$. Necessarily, $e_0 = e_j$ for some $j > k+1$. Since $T'$ contains all of the edges $e_1$, $e_2$, …, $e_{k+1}$, this contradicts the defining property of $H$.

# Complexity of an Algorithm

While it is essential that an algorithm solve the problem under consideration, another important characteristic of an algorithm concerns its efficiency. **The complexity** of an algorithm refers to the number of basic computational steps (ordinarily arithmetic operations and comparisons) required to execute the algorithm. This number depends on the nature of its input as well as the size of the input. For a graph of order $n$ and size $m$, the complexity typically depends on $n$ and/or $m$. If the complexity is bounded above by a polynomial in its input size, then it is called a **polynomial-time algorithm**. For example, if the input is a graph of order $n$ and the complexity of an algorithm is at most some constant times $n^p$ for some positive integer $p$, then the algorithm is a polynomial-time algorithm and we denote the complexity by $O(n^p)$. An algorithm of complexity $O(n^2)$ is a **linear-time algorithm**, while an algorithm of complexity $O(n^2)$ is a **quadratic-time algorithm**.

Polynomial-time algorithms are considered efficient as these algorithms are typically computationally feasible even when applied to graphs of large order. The complexity of Kruskal’s algorithm is $O(m^2)$ and that of Prim’s algorithm is $O(n^3)$.