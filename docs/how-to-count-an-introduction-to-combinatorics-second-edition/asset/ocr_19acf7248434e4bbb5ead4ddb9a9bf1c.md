of degrees 1 and 2. A key idea behind the proof is that, however, such a graph must contain some vertices whose degrees are quite low, in the sense given by our next result.

# **THEOREM 9.11**

A connected triangulated plane graph has at least four vertices whose degrees are at most 5.

# **Proof**

Let $G=(V,E)$ be a connected triangulated plane graph with $v$ vertices and $e$ edges. By Theorem 9.7 we have that $e \leq 3v - 6$. This is good enough for our purposes, but it is worth noting that, as $G$ is triangulated, each face is bounded by exactly three edges, and so the inequality $3f \leq 2e$ in the proof of Theorem 9.7 may be replaced by the equation $3f = 2e$, and hence in this case we can deduce that

$e = 3v - 6$. \qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad (9.6)

Now suppose that the highest degree of any vertex of $G$ is $r$ and that for $k = 3,4,5,\dots,r$, the graph $G$ has $a_k$ vertices of degree $k$. Then

$v = a_3 + a_4 + \dots + a_r$ \qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad (9.7)

and

$\sum_{x \in V} \delta(x) = 3a_3 + 4a_4 + 5a_5 + ... + ra_r$. \qquad\qquad\qquad\qquad\qquad\qquad (9.8)

Hence, by the handshaking lemma,

$2e = 3a_3 + 4a_4 + 5a_5 + ... + ra_r$ \qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad (9.9)

From Equations 9.6, 9.7, and 9.9 it follows that

$3a_3 + 4a_4 + 5a_5 + 6a_6 + ... + ra_r = 6(a_3 + a_4 + a_5 + a_6 + ... + a_r)-12$

and hence that

$3a_3 + 2a_4 + a_5 = a_3 + 2a_5 + ... + (r - 6)a_r + 12$. \qquad\qquad\qquad\qquad (9.10)

It follows that

$3(a_3 + a_4 + a_5) \geq 3a_3 + 2a_4 + a_5 \geq 12$

and hence that

$a_3 + a_4 + a_5 \geq 4$. \qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad (9.11)

The inequality 9.11 is what we were aiming to prove.