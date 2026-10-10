**Proof.** The result is obvious for planar graphs of order 6 or less. Let $G$ be a graph of order $n$ and size $m$ all of whose vertices have degree 6 or more. Then $n \ge 7$ and

$2m = \sum_{v \in V(G)} \deg v \ge 6n$
and so $m \ge 3n$. By Theorem 10.4, $G$ is nonplanar. ■

# The Five Regular Polyhedra

We saw, by the Euler Polyhedron Formula, that if $V$, $E$ and $F$ are the number of vertices, edges and faces of a polyhedron, then

$V - E + F = 2.$

When dealing with a polyhedron $P$ (as well as the graph of the polyhedron $P$), it is customary to represent the number of vertices of degree $k$ by $V_k$ and number of faces bounded by a $k$-cycle ($k$-sided faces) by $F_k$. It follows then that

$2E = \sum_{k \ge 3} kV_k = \sum_{k \ge 3} kF_k.$ (10.1)

By Corollary 10.5, every polyhedron has at least one vertex of degree 3, 4 or 5. As an analogue to this result, we have the following.

> **Theorem 10.6** *At least one face of every polyhedron is bounded by a $k$-cycle for some $k$ where $k \in \{3,4,5\}.$*

**Proof.** Assume, to the contrary, that the statement is false. Then $F_3 = F_4 = F_5 = 0$. By equation (10.1),

$2E = \sum_{k \ge 6} kF_k \ge \sum_{k \ge 6} 6F_k = 6 \sum_{k \ge 6} F_k = 6F.$
Hence, $E \ge 3F$. Also,

$2E = \sum_{k \ge 3} kV_k \ge \sum_{k \ge 3} 3V_k = 3 \sum_{k \ge 3} V_k = 3V.$

By Theorem 10.1, $V - E + F = 2$ and so $3V - 3E + 3F = 6$. Hence, $6 = 3V - 3E + 3F \le 2E - 3E + E = 0$, which is a contradiction. ■

Of the five Platonic solids shown in Figure 10.1, three are cubic polyhedra (the tetrahedron, cube and dodecahedron) as each vertex in these polyhedra has degree 3. The dodecahedron has twelve faces, all 5-sided. If the icosahedron (which has twelve vertices of degree 5 and twenty 3-sided faces) is “truncated”, replacing each vertex by a pentagon, another polyhedron results – namely a cubic polyhedron containing twelve 5-sided faces and twenty 6-sided faces. This