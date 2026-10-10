**Theorem 18.21** *For every positive integer* $r$*,*

$\chi''(K_{r,r}) = \chi(K_{r,r}) + \chi'(K_{r,r}).$

**Proof.** Let $G = K_{r,r}$. Then $|V(G) \cup E(G)| = r^2 + 2r$. Suppose that $\chi''(G) = k$. Then $V(G) \cup E(G)$ can be partitioned into sets $X_1, X_2, \ldots, X_k$ where each set $X_i$ ($1 \le i \le k$) consists of an independent set of vertices and an independent set of edges, where no vertex of $X_i$ is incident with an edge of $X_i$. Necessarily, $|X_i| \le r$ for each $i$ ($1 \le i \le k$). Hence, $k \ge r + 2$. Since $\chi'(K_{r,r}) = r$ by König’s theorem (Theorem 17.7) and $\chi(K_{r,r}) = 2$, it follows by Theorem 18.19 that $\chi''(G) \le r + 2$ and so

$\chi''(G) = 2 + r = \chi(K_{r,r}) + \chi'(K_{r,r}),$

as desired. \blacksquare

Even though it is not known if $2 + \Delta(G)$ is an upper bound for the total chromatic number of every graph, the number $2 + \chi_t'(G)$ is an upper bound.

**Theorem 18.22** *For every graph* $G$*,*

$\chi''(G) \le 2 + \chi_t'(G).$

**Proof.** Suppose that $\chi_t'(G) = k$. Then

$\begin{array}{l} \chi(G) \le 1 + \Delta(G) \le 1 + \chi'(G) \le 1 + \chi_t'(G) \\ \quad < 2 + \chi_t'(G) = 2 + k. \end{array}$

Thus, $G$ is $(k+2)$-colorable. Let a $(k+2)$-coloring $c$ of $G$ be given, using the colors $1, 2, \ldots, k+2$, say. For each edge $e = uv$ of $G$, let $L(e) = \{1, 2, \ldots, k+2\}$ and let

$L'(e) = L(e) - \{c(u), c(v)\},$

Since $|L'(e)| \ge k$ for each edge $e$ of $G$ and $\chi_t'(G) = k$, it follows that there is a proper edge coloring $c'$ of $G$ such that $c'(e) \in L'(e)$ and so $c'(e) \notin \{c(u), c(v)\}$. Hence, the total coloring $c''$ of $G$ defined by