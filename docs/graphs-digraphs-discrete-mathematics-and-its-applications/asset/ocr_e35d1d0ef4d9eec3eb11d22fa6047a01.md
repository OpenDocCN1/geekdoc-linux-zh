# **2.2. DISTANCE IN GRAPHS**

The distance $d$ defined above satisfies the following properties in a connected graph $G$:

+   (1) $d(u, v) \geq 0$ for every two vertices $u$ and $v$ of $G$;

+   (2) $d(u, v) = 0$ if and only if $u = v$;

+   (3) $d(u, v) = d(v, u)$ for all $u, v \in V(G)$ (the **symmetric property**);

+   (4) $d(u, w) \leq d(u, v) + d(v, w)$ for all $u, v, w \in V(G)$ (the **triangle inequality**).

Since $d$ satisfies the four properties (1)\u2013(4), $d$ is a **metric** on $V(G)$ and $(V(G), d)$ is a **metric space**. Because $d$ satisfies the symmetric property, we can speak of the distance *between* two vertices $u$ and $v$ rather than the distance *from* $u$ to $v$.

With the aid of this distance we can present a useful characterization of bipartite graphs.

**Theorem 2.6** *A nontrivial graph $G$ is a bipartite graph if and only if $G$ contains no odd cycles.*

**Proof.** Suppose first that $G$ is bipartite. Then $V(G)$ can be partitioned into partite sets $U$ and $W$ (and so every edge of $G$ joins a vertex of $U$ and a vertex of $W$). Let $C = (v_1, v_2, \dots, v_k, v_1)$ be a $k$-cycle of $G$. We may assume that $v_1 \in U$. Thus, $v_2 \in W$, $v_3 \in U$ and so forth. In particular, $v_i \in U$ for every odd integer $i$ with $1 \leq i \leq k$ and $v_j \in W$ for every even integer $j$ with $2 \leq j \leq k$. Since $v_1 \in U$, it follows that $v_k \in W$ and so $k$ is even.

For the converse, let $G$ be a nontrivial graph containing no odd cycles. If $G$ is empty, then $G$ is clearly bipartite. Hence it suffices to show that every nontrivial component of $G$ is bipartite and so we may assume that $G$ itself is connected. Let $u$ be a vertex of $G$ and let

```
$U = \{x \in V(G): \ d(u, x)\ \text{is even}\}$ and $W = \{x \in V(G): \ d(u, x)\ \text{is odd}\}.$
```

Thus, $u \in U$. We show that $G$ is a bipartite graph having partite sets $U$ and $W$. It suffices to show that no two vertices of $U$ are adjacent and no two vertices of $W$ are adjacent. Suppose that $W$ contains two adjacent vertices $w_1$ and $w_2$. Let $P_1$ be a $u-w_1$ geodesic and $P_2$ a $u-w_2$ geodesic. Let $z$ be the last vertex that $P_1$ and $P_2$ have in common (possibly $z = u$). Then the length of the $z-w_1$ subpath $P_1'$ of $P_1$ and the length of the $z-w_2$ subpath $P_2'$ of $P_2$ are of the same parity. Thus, the paths $P_1'$ and $P_2'$ together with the edge $w_1w_2$ produce an odd cycle. This is a contradiction. The argument that no two vertices of $U$ are adjacent is similar.