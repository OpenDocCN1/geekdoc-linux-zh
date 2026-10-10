# **Chapter 8   Section 8.1**

+   1. No.

+   3. (a) $a = 1$, $b = 2$ and $c = 1$. (b) $\mathrm{val}(f) = 4$.

+   5. Show that for the flow $f'$, the net flow out of each vertex in $N'$ equals the net flow out of this vertex for the flow $f$.

+   7. (a) Let $\mathcal{U}$ be the set of all maximal paths $P$ in $D$ whose initial vertex is $u$ and such that no arc of $P$ belongs to $A$. Consider the set $X = \bigcup_{P \in \mathcal{U}} V(P)$.
+   
+   (b) Let $D$ be a $u-v$ path of length 2.

+   9. (a) Show that $\mathrm{val}(f) = \mathrm{cap}(K)$ and apply Corollary 8.3.
+   
+   (b) Use the proof of Theorem 8.6 to show that $f(\overline{X}, \overline{X}) = 0$ and $c(X, \overline{X}) = f(X, \overline{X})$.

# **Section 8.2**

+   11. Apply Algorithm 8.7 three times to obtain a maximum flow $f''$ with $\mathrm{val}(f'') = 6$ and a minimum cut $[X, \overline{X}]$ with $X = \{u, s\}$.

+   13. (a) The statement is false. (b) The statement is true.

# **Section 8.3**

+   15. The maximum number of pairwise arc-disjoint $u-v$ paths in $D$ is 1.

+   17. Suppose that $S = \{s_1, s_2, \dots, s_r\}$ and $T = \{t_1, t_2, \dots, t_q\}$. Add a new vertex $s$ and the arcs $(s, s_i), 1 \leq i \leq r$, and add a new vertex $t$ and the arcs $(t_i, t), 1 \leq i \leq q$. Let $C = \sum_{e \in E(D)} c(e)$.

# **Chapter 9   Section 9.1**

+   1. $\mathrm{Aut}(G_1) = \{e, (t\; u), (y\; z), (t\; u)(y\; z)\}.$
+   
+   $\mathrm{Aut}(G_2) = \{e, (1\;2), (6\;7), (1\;2)(6\;7), (3\;5)(1\;6)(2\;7), (3\;5)(2)(6\;1)(7), (3\;5)(1\;7\;2\;6), (3\;5)(1\;6\;2\;7)\}$.

+   3. Yes. $K_4 - e$.

+   5. See the figure below.

![](bbox=[0.35, 0.82, 0.65, 0.92])

+   7. Such a pair $(k, n)$ is realizable except when $k = n$ and $2 \leq n \leq 5$.

+   9. Let $n = 2k$ for some positive integer $k$ and let $G$ be the bipartite graph with partite sets $U = \{u_1, u_2, \dots, u_k\}$ and $W = \{w_1, w_2, \dots, w_k\}$ where $u_i$ $(1 \leq i \leq k)$ is adjacent to $w_j$ if $i + j > k$.

+   11. The graph $G_3$ has two cut-vertices. In $G_4$, consider the subgraphs induced by the neighborhoods of its vertices.