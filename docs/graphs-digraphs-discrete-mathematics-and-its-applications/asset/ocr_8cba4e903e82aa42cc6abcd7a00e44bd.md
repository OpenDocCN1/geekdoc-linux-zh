As an illustration of the greedy coloring algorithm, suppose that we consider the graph $C_6$ of Figure 14.8. If we list the vertices of $C_6$ in the order $u, w, v, y, z, x$, then the greedy coloring algorithm yields the coloring $c$ of $G$ defined by

$c(u) = 1$, $c(w) = 1$, $c(v) = 2$, $c(y) = 1$, $c(z) = 2$, $c(x) = 2$. This gives $\chi(C_6) \leq 2$. Of course, $\chi(C_6) = 2$ and so with this ordering of the vertices of $C_6$, a $\chi(C_6)$-coloring is produced. On the other hand, if the vertices of $G$ are listed in the order $u, x, v, w, z, y$, then the greedy coloring algorithm yields the coloring $c'$ of $G$ defined by

$c'(u) = 1$, $c'(x) = 1$, $c'(v) = 2$, $c'(w) = 3$, $c'(z) = 2$, $c'(y) = 3$. This gives a 3-coloring of $C_6$, which, of course, is not the chromatic number of $C_6$.

![](bbox=[0.35, 0.36, 0.65, 0.56])

From the second listing of the vertices of $C_6$, we see that $\chi(C_6) \leq 3$. As the proof of the following theorem shows, no greater upper bound for $\chi(C_6)$ is possible using the greedy coloring algorithm.

# Theorem 14.18 For every graph $G$,

$\chi(G) \leq 1 + \Delta(G)$. **Proof.** Suppose that the vertices of $G$ are listed in the order $v_1, v_2, \dots, v_n$ and the greedy coloring algorithm is applied. Then $v_1$ is assigned the color 1 and for $2 \leq i \leq n$, the vertex $v_i$ is either assigned the color 1 or is assigned the color $k + 1$, where $k$ is the largest integer such that all of the colors $1, 2, \dots, k$ are used to color the neighbors of $v_i$ in the set $S = \{v_1, v_2, \dots, v_{i-1}\}$. Since at most deg $v_i$ neighbors of $v_i$ belong to $S$, the largest value of $k$ is deg $v_i$. Hence, the color assigned to $v_i$ is at most $1 +$ deg $v_i$. Thus,

$\chi(G) \leq \max_{1 \leq i \leq n}\{1 + \text{deg } v_i\} = 1 + \Delta(G)$, as desired.