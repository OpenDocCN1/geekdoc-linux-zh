
Corollary 10.2 If $G$ is a plane graph with $n$ vertices, $m$ edges and $r$ regions, then
$$n - m + r = 1 + k(G).$$

## An Upper Bound for the Size of Planar Graphs

If $G$ is a connected plane graph of order 4 or more, then the boundary of every region of $G$ must contain at least three edges. This observation is helpful in showing that with respect to the least order of a planar graph, its size cannot be too great.

Theorem 10.3 If $G$ is a planar graph of order $n \geq 3$ and size $m$, then
$$m \leq 3n - 6.$$

Proof. Since the size of every graph of order 3 cannot exceed 3, the inequality holds for $n = 3$. So we may assume that $n > 4$. Furthermore, we may assume that the planar graphs under consideration are connected, for otherwise edges can be added to produce a connected graph. Suppose that $G$ is a connected planar graph of order $n > 4$ and size $m$. Let there be given a planar embedding of $G$, resulting in $r$ regions. By the Euler Identity, $n - m + r = 2$. Let $R_1, R_2, \ldots, R_r$ be the regions of $G$ and suppose that we denote the number of edges on the boundary of $R_i$ ($1 \leq i \leq r$) by $m_i$. Then $m_i \geq 3$ for $1 \leq i \leq r$. Since each edge of $G$ is on the boundary of at most two regions of $G$, it follows that
$$3r \leq \sum_{i=1}^{r} m_i \leq 2m.$$

Hence,
$$6 = 3n - 3m + 3r \leq 3n - 3m + 2m = 3n - m$$
and so $m \leq 3n - 6$. $\blacksquare$

By expressing Theorem 10.3 in its contrapositive form, we obtain the following reformulation of the theorem.

Theorem 10.4 If $G$ is a graph of order $n \geq 5$ and size $m$ such that $m > 3n - 6$, then $G$ is nonplanar.

There is an immediate consequence of this theorem.

Corollary 10.5 Every planar graph contains a vertex of degree 5 or less.

Proof. The result is obvious for planar graphs of order 6 or less. Let $G$ be a graph of order $n$ and size $m$ all of whose vertices have degree 6 or more. Then $n \geq 7$ and

$$2m = \sum_{v \in V(G)} \deg v \geq 6n$$
and so $m \geq 3n$. By Theorem 10.4, $G$ is nonplanar. $\blacksquare$

## The Five Regular Polyhedra

We saw, by the Euler Polyhedron Formula, that if $V$, $E$ and $F$ are the number of vertices, edges and faces of a polyhedron, then

$$V - E + F = 2.$$

When dealing with a polyhedron $P$ (as well as the graph of the polyhedron $P$), it is customary to represent the number of vertices of degree $k$ by $V_k$ and number of faces bounded by a $k$-cycle ($k$-sided faces) by $F_k$. It follows then that

$$2E = \sum_{k \geq 3} kV_k = \sum_{k \geq 3} kF_k.$$ (10.1)

By Corollary 10.5, every polyhedron has at least one vertex of degree 3, 4 or 5. As an analogue to this result, we have the following.

Theorem 10.6 At least one face of every polyhedron is bounded by a $k$-cycle for some $k$ where $k \in \{3,4,5\}$.

Proof. Assume, to the contrary, that the statement is false. Then $F_3 = F_4 = F_5 = 0$. By equation (10.1),

$$2E = \sum_{k \geq 6} kF_k \geq \sum_{k \geq 6} 6F_k = 6 \sum_{k \geq 6} F_k = 6F.$$
Hence, $E \geq 3F$. Also,

$$2E = \sum_{k \geq 3} kV_k \geq \sum_{k \geq 3} 3V_k = 3 \sum_{k \geq 3} V_k = 3V.$$

By Theorem 10.1, $V - E + F = 2$ and so $3V - 3E + 3F = 6$. Hence, $6 = 3V - 3E + 3F \leq 2E - 3E + E = 0$, which is a contradiction. $\blacksquare$

Of the five Platonic solids shown in Figure 10.1, three are cubic polyhedra (the tetrahedron, cube and dodecahedron) as each vertex in these polyhedra has degree 3. The dodecahedron has twelve faces, all 5-sided. If the icosahedron (which has twelve vertices of degree 5 and twenty 3-sided faces) is “truncated”, replacing each vertex by a pentagon, another polyhedron results – namely a cubic polyhedron containing twelve 5-sided faces and twenty 6-sided faces. This is precisely what occurs with a soccer ball, which has 32 faces, 12 of which are pentagonal faces and 20 are hexagonal faces. Indeed, every cubic polyhedron containing only 5-sided and 6-sided faces must contain exactly twelve 5-sided faces. To see this, suppose that $P$ is a cubic polyhedron with $V$ vertices, $E$ edges and $F$ faces. Then $V = V_3$, $F = F_5 + F_6$ and, by the Euler Polyhedron Formula, $V - E + F = 2$. By (10.1), $2E = 3V_3 = 5F_5 + 6F_6$. Therefore,

$$
\begin{align*}
12 &= 6V - 6E + 6F = 6V_3 - 6E + 6(F_5 + F_6) \\
&= (10F_5 + 12F_6) - (15F_5 + 18F_6) + (6F_5 + 6F_6) = F_5.
\end{align*}
$$

A **regular polyhedron** is a polyhedron whose faces are bounded by congruent regular polygons and whose polyhedral angles are congruent. In particular, for a regular polyhedron, $F = F_s$ for some $s$ and $V = V_t$ for some $t$, where $s, t \in \{3, 4, 5\}$. For example, a cube is a regular polyhedron with $V = V_3$ and $F = F_4$. There are only four other regular polyhedra. These five regular polyhedra are the Platonic solids we saw in Figure 10.1. Over two thousand years ago, the Greeks were aware that there are only five such polyhedra.

Theorem 10.7 There are exactly five regular polyhedra.

Proof. Let $P$ be a regular polyhedron and let $G$ be an associated plane graph. Then $V - E + F = 2$, where $V$, $E$ and $F$ denote the number of vertices, edges and faces of $P$ and the number of vertices, edges and regions of $G$. Therefore,

$$
\begin{align*}
-8 &= 4E - 4V - 4F \\
&= 2E + 2E - 4V - 4F \\
&= \sum_{k \geq 4} kF_k + \sum_{k \geq 3} kV_k - 4 \sum_{k \geq 3} V_k - 4 \sum_{k \geq 3} F_k \\
&= \sum_{k \geq 4} (k - 4)F_k + \sum_{k \geq 3} (k - 4)V_k. \tag{10.2}
\end{align*}
$$

Since $G$ is regular, there exist integers $s$ and $t$ with $s, t \in \{3, 4, 5\}$ such that $F = F_s$ and $V = V_t$. Hence

$$
\begin{align*}
-8 &= (s - 4)F_s + (t - 4)V_t. \tag{10.2}
\end{align*}
$$

Moreover, $sF_s = 2E = tV_t$. If $s, t \geq 4$, then (10.2) yields $-8 = (s - 4)F_s + (t - 4)F_t \geq 0$, which is impossible. Hence either $s = 3$ or $t = 3$. This results in five possibilities for the pairs $s, t$.

Case 1. $s = 3$ and $t = 3$. Here we have

$$
\begin{align*}
-8 &= -F_3 - V_3 \quad \text{and} \quad 3F_3 = 3V_3; \\
\text{so } F_3 = V_3 = 4. \text{ Thus } P \text{ is the } \textit{tetrahedron}. \text{ (That the tetrahedron is the only regular polyhedron with } V_3 = F_3 = 4 \text{ follows from geometric considerations.)}
\end{align*}
$$

Case 2. $s = 3$ and $t = 4$. Therefore,
$$-8 = -F_3 \text{ and } 3F_3 = 4V_4,$$
Hence $F_3 = 8$ and $V_4 = 6$, implying that $P$ is the octahedron.

Case 3. $s = 3$ and $t = 5$. In this case,
$$-8 = -F_3 + V_5 \text{ and } 5F_3 = 5V_5,$$
so $F_3 = 20$, $V_5 = 12$ and $P$ is the icosahedron.

Case 4. $s = 4$ and $t = 3$. We find here that
$$-8 = -V_3 \text{ and } 4F_4 = 3V_3,$$
Thus $V_3 = 8$, $F_4 = 6$ and $P$ is the cube.

Case 5. $s = 5$ and $t = 3$. For these values,
$$-8 = F_5 - V_3 \text{ and } 5F_5 = 3V_3,$$
Solving for $F_5$ and $V_3$, we find that $F_5 = 12$ and $V_3 = 20$, so $P$ is the dodecahedron.

The graphs of the five regular polyhedra are shown in Figure 10.3.

## The Graphs $K_5$ and $K_{3,3}$

Theorem 10.4 provides us with a large class of nonplanar graphs.

Corollary 10.8 The graph $K_5$ is nonplanar.

Proof. The graph $K_5$ has order $n = 5$ and size $m = 10$. Since $m = 10 > 9 = 3n - 6$, it follows by Theorem 10.4 that $K_5$ is nonplanar.

Since it is evident that any graph containing a nonplanar subgraph is itself nonplanar, it follows that once we know that $K_5$ is nonplanar, we can conclude that $K_n$ is nonplanar for every integer $n \geq 5$. Of course, $K_n$ is planar for $1 \leq n \leq 4$.

We will soon see that $K_5$ is an especially important nonplanar graph. Another important nonplanar graph is $K_{3,3}$. Since $K_{3,3}$ has order $n = 6$ and size $m = 9$ but $m < 3n - 6$, Theorem 10.4 cannot be used to establish the nonplanarity of $K_{3,3}$, however. On the other hand, we can use the fact that $K_{3,3}$ is bipartite to establish this property.

Corollary 10.9 The graph $K_{3,3}$ is nonplanar.

Proof. Suppose that $K_{3,3}$ is planar. Let there be given a planar embedding of $K_{3,3}$, resulting in $r$ regions. Thus, by the Euler Identity, $n - m + r = 6 - 9 + r = 2$ and so $r = 5$. Let $R_1, R_2, \dots, R_5$ be the five regions and let $m_i$ be the number of edges on the boundary of $R_i$ ($1 \leq i \leq 5$). Since $K_{3,3}$ is bipartite, $K_{3,3}$ contains no triangles and so $m_i \geq 4$ for $1 \leq i \leq 5$. Since every edge of $K_{3,3}$ lies on the boundary of a cycle, every edge of $K_{3,3}$ belongs to the boundary of two regions. Thus,

$$20 = 4r \leq \sum_{i=1}^{5} m_i = 2m = 18,$$
which is impossible.

## 10.2 Maximal Planar Graphs

A planar graph $G$ is **maximal planar** if the addition to $G$ of any edge joining two nonadjacent vertices of $G$ results in a nonplanar graph. Necessarily then, if a maximal planar graph $G$ of order $n \geq 3$ and size $m$ is embedded in the plane resulting in $r$ regions, then the boundary of every region of $G$ is a triangle and so $3r=2m$. It then follows by the proof of Theorem 10.3 that $m=3n-6$. All of the graphs shown in Figure 10.6 are maximal planar.

![](img/598a6ae3fd44120830ada34717906f29_260_0.png)

A graph $G$ is **nearly maximal planar** if there exists a planar embedding of $G$ such that the boundary of every region of $G$ is a cycle, at most one of which is not a triangle. Thus, every maximal planar graph is nearly maximal planar (see Figure 10.7(a)). Also, the wheels $W_{n}= C_{n}\vee K_{1}$ $(n\geq 3)$ are nearly maximal planar (see Figure 10.7(b)). In addition, the graphs in Figures 10.7(c) and 10.7(d) (where the graph in Figure 10.7(d) is redrawn in Figure 10.7(e)) are nearly maximal planar.

We now derive some results concerning the degrees of the vertices of a maximal planar graph.

Theorem 10.10 If $G$ is a maximal planar graph of order 4 or more, then the degree of every vertex of $G$ is at least 3.

Proof. Let $G$ be a maximal planar graph of order $n\geq 4$ and size $m$ and let $v$ be a vertex of $G$. Since $m=3n-6$, it follows that $G-v$ has order $n-1$ and size $m-\deg v$. Since $G-v$ is planar and $n-1\geq 3$, it follows that

$$m-\deg v \le 3(n-1)-6$$
and so $m-\deg v = 3n-6-\deg v \le 3n-9.$ Thus, $\deg v \geq 3.$
