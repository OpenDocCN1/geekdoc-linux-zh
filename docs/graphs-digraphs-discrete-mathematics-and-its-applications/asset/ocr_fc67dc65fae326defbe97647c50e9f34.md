(b) Show that the result in (a) is best possible in general by showing that $\frac{2n+1}{3}$ cannot be replaced by $\frac{2n}{3}$.

# **Section 1.8. Multigraphs**

53. We saw that the irregular multigraph $G_2$ in Figure 1.30 has degree sequence $4,3,2,1$. Give an example of an irregular multigraph (if such a multigraph exists) having degree sequence

+   (a) 5,4,3,2,1
+   (b) 6,5,4,3,2,1
+   (c) 7,6,5,4,3,2,1.

54. Prove for every connected graph $G$ of order $n=3$ or $n=4$ and size $m$ that it is possible to label the edges of $G$ by $e_1,e_2,\ldots,e_m$ and replace $e_i$ by $i$ parallel edges for each $i$ $(1 \leq i \leq m)$ such that the degrees of the vertices of the resulting multigraph $H$ are distinct.

55. Determine which of the following sequences are the degree sequences of a multigraph.

+   (a) $s_1:3,2,1$            (b) $s_2:5,2,1$
+   (c) $s_3:6,4,2$            (d) $s_4:3,2,2$
+   (e) $s_5:4,4,2,2$          (f) $s_6:5,3,2,1$
+   (g) $s_7:4,4,4,4$          (h) $s_8:7,5,3,1$.

56. Prove that a sequence $s:d_1,d_2,\ldots,d_n$ $(n \geq 1)$ of nonnegative integers with $d_1 \geq d_2 \geq \cdots \geq d_n$ is the degree sequence of a multigraph if and only if $\sum_{i=1}^{n} d_i$ is even and $d_1 \leq \frac{1}{2}\sum_{i=1}^{n} d_i$.

57. Let $G$ be a connected graph of order $n$ where the vertices of $G$ are labeled as $v_1,v_2,\ldots,v_n$ in some way. A multigraph $H$ of size $n$ with $V(H) = V(G)$ is obtained by replacing each edge $v_iv_j$ of $G$ by $\min\{i,j\}$ parallel edges.

+   (a) Find $m$ if $G=K_5$.
+   (b) Find sharp upper and lower bounds for $m$ if $G=C_5$.
+   (c) Find the minimum value of $m$ if $G$ is bipartite.