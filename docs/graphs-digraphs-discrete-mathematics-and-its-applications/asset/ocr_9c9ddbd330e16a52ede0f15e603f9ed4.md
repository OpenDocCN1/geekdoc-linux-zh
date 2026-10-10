Since $(n-2x)^2 \geq 0$, it follows that

```
$n^2 \geq 4nx - 4x^2 = 4x(n-x)$
```

and so $x(n-x) \leq n^2/4$. Since $x(n-x)$ is an integer, $x(n-x) \leq \lfloor n^2/4 \rfloor$. ■

No bipartite graph $G$ can contain a triangle $H$, for otherwise, at least two vertices $u$ and $v$ of $H$ must belong to the same partite set and so $u$ and $v$ are not adjacent. Hence if $G$ is a graph of order $n \geq 3$ and size $m \leq \lfloor n^2/4 \rfloor$, then $G$ need not contain a triangle. However, in 1907 the Dutch mathematician Willem Mantel [161] showed that any graph of order $n$ with a larger size must contain a triangle.

# **Theorem 1.9** Every graph of order $n \geq 3$ and size $m > \lfloor n^2/4 \rfloor$ contains a triangle.

**Proof.** First, observe that the result is true for $n=3$ and $n=4$. Suppose, however, that the statement is false. Then there is a smallest integer $n \geq 5$ and a graph $G$ of order $n$ and size $m > \lfloor n^2/4 \rfloor$ not containing a triangle. Let $uv$ be an edge of $G$. Since $G$ contains no triangle, there is no vertex in $G$ adjacent to both $u$ and $v$. Hence, $(\deg u - 1) + (\deg v - 1) \leq n - 2$ and so $\deg u + \deg v \leq n$. Let $G' = G - u - v$. Since $G'$ is a subgraph of $G$, it follows that $G'$ also does not contain a triangle. Furthermore, $G'$ has order $n-2$ and size

```
$m' = m - (\deg u + \deg v) + 1 > \lfloor n^2/4 \rfloor - n + 1$.
```

Thus,

```
$m' > \frac{n^2}{4} - n + 1 = \frac{n^2 - 4n + 4}{4} = \frac{(n-2)^2}{4}$.
```

From the defining property of the graph $G$, it follows that $G'$ contains a triangle, producing a contradiction. ■

Therefore, from Theorems 1.8 and 1.9, it follows that every graph of order $n \geq 3$ and size $m > \lfloor n^2/4 \rfloor$ not only fails to be bipartite, it must, in fact, contain a triangle.

# **Complete Multipartite Graphs**

Bipartite graphs belong to a more general class of graphs. For an integer $k \geq 1$, a graph $G$ is a **k-partite graph** if $V(G)$ can be partitioned into $k$ subsets $V_1, V_2, \dots, V_k$ (again called **partite sets**) such that every edge of $G$ joins vertices in two different partite sets. A 1-partite graph is then an empty graph and a 2-partite graph is bipartite. A **complete k-partite graph** $G$ is a k-partite graph with the property that two vertices are adjacent in $G$ if and only if the vertices belong to different partite sets. If $|V_i| = n_i$ for $1 \leq i \leq k$, then $G$ is denoted by $K_{n_1, n_2, \dots, n_k}$ (the order in which the numbers $n_1, n_2, \dots, n_k$