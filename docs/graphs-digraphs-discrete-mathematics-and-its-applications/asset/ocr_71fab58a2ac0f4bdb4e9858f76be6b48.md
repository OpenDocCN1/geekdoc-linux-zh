$n = n_1 + n_2 + \dots + n_k$, $1 \leq n_1 \leq n_2 \leq \dots \leq n_k$, and $n_k - n_1 \leq 1$.

For every two integers $k$ and $n$ with $1 \leq k \leq n$, the integers $n_1, n_2, \dots, n_k$ are unique. For example, for $n = 11$ and $k = 3$, the integers $n_1, n_2, n_3$ are $3, 4, 4$; while for $n = 14$ and $k = 6$, the integers $n_1, n_2, \dots, n_6$ are $2, 2, 2, 2, 3, 3$. The complete $k$-partite graph $K_{n_1, n_2, \dots, n_k}$ is called the **Túrán graph** $T_{n,k}$. Thus, the Túrán graph $T_{n,k}$ is the complete $k$-partite graph of order $n$, the cardinalities of whose partite sets differ by at most 1. The number of elements in each partite set of $T_{n,k}$ is either $\left\lfloor\frac{n}{k}\right\rfloor$ or $\left\lceil\frac{n}{k}\right\rceil$. If $n/k$ is an integer, then $\left\lfloor\frac{n}{k}\right\rfloor = \left\lceil\frac{n}{k}\right\rceil = \frac{n}{k}$; while if $n/k$ is not an integer and $r$ is the remainder when $n$ is divided by $k$, then exactly $r$ of the partite sets of $T_{n,k}$ have cardinality $\left\lceil\frac{n}{k}\right\rceil$.

# Túrán’s Theorem

Since the Túrán graph $T_{n,k}$ is a complete $k$-partite graph, $T_{n,k}$ contains no $(k+1)$-clique (a clique of order $k+1$). The size of $T_{n,k}$ is denoted by $t_{n,k}$. Thus, there exists a graph of order $n$ and size $t_{n,k}$ containing no $(k+1)$-clique. Túrán [237] showed that for positive integers $n$ and $k$ with $n \geq k$, the graph $T_{n,k}$ is the unique graph of order $n$ and maximum size having no $(k+1)$-clique.

**Theorem 19.2 (Túrán’s Theorem)** Let $n$ and $k$ be positive integers with $n \geq 3$ and $n \geq k$. The Túrán graph $T_{n,k}$ is the unique graph of order $n$ and maximum size having no $(k+1)$-clique.

**Proof.** We proceed by induction on $k$. Since the only graph of order $n$ containing no 2-clique is $\overline{K}_n = T_{n,1}$, the result holds for $k = 1$. Assume, for an integer $k \geq 2$ and an integer $n'$ with $n' \geq k - 1$, that $T_{n', k-1}$ is the unique graph of order $n'$ and maximum size containing no $k$-clique. Next, let $n \geq k$ and let $G$ be a graph of order $n$ and maximum size containing no $(k+1)$-clique. We show that $G = T_{n,k}$.

Let $v$ be a vertex of $G$ with $\deg v = \Delta(G) = \Delta$ and let $H = G[N_G(v)]$. Thus, $H$ is a graph of order $\Delta$ containing no $k$-clique. We show that $\Delta \leq k - 1$. Assume, to the contrary, that $\Delta \leq k - 2$. Since $n \geq k$, there exists $u \in V(G) - \{v\}$ that is not adjacent to $v$. Then the graph $G + uv$ contains a $(k+1)$-clique. On the other hand, each vertex $x \in V(G) - \{u, v\}$ has degree at most $\Delta \leq k - 2$ in $G + uv$ and $k + 1 \geq 3$, which is impossible. Hence, $\Delta \geq k - 1$. By the induction hypothesis, $H' = T_{\Delta, k-1}$ is the unique graph of order $\Delta$ and maximum size containing no $k$-clique. Thus, $|E(H')| \leq |E(H')|$ and

$|E(H)| = |E(H')|$ only if $H = H' = T_{\Delta, k-1}$.

Define $G' = \overline{K}_{n - \Delta} \vee H'$. Hence, $G'$ has order $n$. Also, since $H'$ is a $(k - 1)$-partite graph, $G'$ is a $k$-partite graph and so contains no $(k + 1)$-clique. Furthermore,