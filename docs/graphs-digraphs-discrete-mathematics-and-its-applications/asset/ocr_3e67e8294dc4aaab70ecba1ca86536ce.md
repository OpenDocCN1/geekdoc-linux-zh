$uv \in M$. The vertices $u$ and $v$ cannot be adjacent to distinct unmatched vertices $x$ and $y$, respectively, for otherwise, $(x, u, v, y)$ is an $M$-augmenting path in $G$, contradicting Theorem 12.2. If $u$ is adjacent to $v$ an unmatched vertex, place $u$ in $S$; otherwise, place $v$ in $S$. This is done for each edge of $M$. Thus, $S$ is a dominating set of $G$ and $\gamma(G) \le |S| = |M| = \alpha'(G)$. ▪

Vadim Vizing conjectured that the domination number of the Cartesian product of two graphs is always at least as large as the product of the domination numbers of these two graphs.

# **Vizing's Conjecture** For every two graphs $G$ and $H$,

$\gamma(G \Box H) \ge \gamma(G) \cdot \gamma(H)$.

# **Independent Dominating Sets**

Recall that an independent set $S$ of vertices of a graph $G$ is a maximal independent set if $S$ is not a proper subset of any independent set in $G$. Thus, every maximum independent set is maximal. The minimum cardinality of a maximal independent set of vertices of $G$ is denoted by $i(G)$. Thus, for $K_{s,t}$, where $s < t$, there are only two maximal independent sets of vertices, namely, the partite sets of $K_{s,t}$. Hence, $\alpha(K_{s,t}) = t$ while $i(K_{s,t}) = s$.

Since every maximal independent set of vertices in a graph $G$ is a dominating set of $G$, it follows that $\gamma(G) \le i(G)$. Not every dominating set is independent, however. Indeed, not every minimum dominating set is independent. For example, in the graph $G$ of Figure 12.11, the set $S_1 = \{u_1, u_2, v_1, v_2, w_1, w_2\}$ is a maximal independent set (and consequently a dominating set) of $G$; while $S_2 = \{x, y, z\}$ is a minimum dominating set of $G$ and certainly $S_2$ is not independent. (These sets are indicated in Figure 12.11 by solid circles.) However, $G$ does contain a minimum dominating set of $G$ that is independent, namely, $S_3 = \{u, v, w\}$.

A set $S$ of vertices in a graph $G$ is an **independent dominating** set of $G$ if $S$ is both an independent and a dominating set of $G$. Thus, the sets $S_1$ and $S_3$ in Figure 12.11 are independent dominating sets while $S_2$ is not. The **independent domination number** $i(G)$ of $G$ is the minimum cardinality among all independent dominating sets of $G$. That this is precisely the notation used for the minimum cardinality of a maximal independent set of vertices in a graph is justified by the following observation of Berge [25].

**Theorem 12.21** A set $S$ of vertices in a graph is an independent dominating set if and only if $S$ is a maximal independent set of vertices.

**Proof.** We have already noted that every maximal independent set of vertices is a dominating set. Conversely, suppose that $S$ is an independent dominating