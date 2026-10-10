![](bbox=[0.35, 0.05, 0.65, 0.3])

and triangle-free. The fact that a graph can be triangle-free and yet have a large chromatic number has been established by a number of mathematicians, including Blanche Descartes [66], John B. Kelly and Leroy M. Kelly [141] and Alexander Zykov [263]. The proof of this fact that we present here, however, is due to Jan Mycielski [174].

![](bbox=[0.2, 0.45, 0.8, 0.67])

# **Theorem 15.1** For every positive integer $k$, there exists a triangle-free $k$-chromatic graph.

**Proof.** Since no graph with chromatic number 1 or 2 contains a triangle, the theorem is obviously true for $k = 1$ and $k = 2$. To verify the theorem for $k \geq 3$, we proceed by induction on $k$. As we have already observed, $\chi(C_5) = 3$ and $C_5$ is triangle-free; so the statement is true for $k = 3$.

Assume there exists a triangle-free graph with chromatic number $k$, where $k \geq 3$. We show that there exists a triangle-free $(k+1)$-chromatic graph. Let $H$ be a triangle-free graph with $\chi(H) = k$, where $V(H) = \{v_1, v_2, \ldots, v_n\}$. We construct a graph $G$ from $H$ by adding $n + 1$ new vertices $u, u_1, u_2, \ldots, u_n$, joining $u$ to each vertex $u_i$ ($1 \leq i \leq n$) and joining $u_i$ to each neighbor of $v_i$...