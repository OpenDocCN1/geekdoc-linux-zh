**Proof.** Suppose that the theorem is false. Among all multigraphs $H$ with $\chi'(H) > 3\Delta(H)/2$, let $G$ be one of minimum size. Let $\Delta(G) = \Delta$ and $\mu(G) = \mu$. Suppose that $\chi'(G) = k$. Hence, $k(G - f) = k - 1$ for every edge $f$ of $G$. By Theorem 17.3, $k \leq \Delta + \mu$ and, by assumption, $k > 3\Delta/2$.

Suppose that $\mu$ edges join the vertices $u$ and $v$. Let $e$ be one of these edges. Since $\chi'(G - e) = k - 1$, there exists a $(k - 1)$-edge coloring of $G - e$. The number of colors not used in coloring the edges incident with $u$ is at least $(k - 1) - (\Delta - 1) = k - \Delta$. Similarly, the number of colors not used in coloring the edges incident with $v$ is at least $k - \Delta$ as well.

Each of these $k - \Delta$ or more colors not used to color an edge incident with $u$ must be used to color an edge incident with $v$, for otherwise there is a color available for $e$, contradicting our assumption that $\chi'(G) = k$. Similarly, each of the $k - \Delta$ or more colors not used to color an edge incident with $v$ must be used to color an edge incident with $u$. Hence, the total number of colors used to color the edges incident with $u$ or $v$ is at least $2(k - \Delta) + \mu - 1$ and so

$2(k - \Delta) + \mu - 1 \leq k - 1.$

Since $3\Delta/2 < k \leq \Delta + \mu$, it follows that $\mu > \Delta/2$ and so

$2(k - \Delta) + (\Delta/2) - 1 < 2(k - \Delta) + \mu - 1 \leq k - 1.$

Therefore,

$2k - (3\Delta/2) - 1 < k - 1,$

implying that $k < 3\Delta/2$, which is a contradiction.

There are occasions when the upper bound for the chromatic index of a multigraph given by Shannon’s theorem (Theorem 17.4) is an improvement over that provided by Theorem 17.3. For the multigraph $G$ of Figure 17.6(a), $\Delta(G) = 7$ and $\mu(G) = 4$. Thus, $\chi'(G) \leq 11$ by Theorem 17.3. By Shannon’s theorem, $\chi'(G) \leq (3 \cdot 7)/2$ and so $\chi'(G) \leq 10$. Since the size of $G$ is 16 and at most two edges of $G$ can be assigned the same color, it follows by Theorem 17.1 for multigraphs (17.2) that $\chi'(G) \geq 16/2 = 8$. In fact, $\chi'(G) = 8$ as the 8-edge coloring of $G$ in Figure 17.6(b) shows.

# 17.2 Class One and Class Two Graphs

By Vizing’s theorem (Theorem 17.2), it follows that for every nonempty graph $G$, either $\chi'(G) = \Delta(G)$ or $\chi'(G) = 1 + \Delta(G)$. A graph $G$ is said to belong to or is of **Class one** if $\chi'(G) = \Delta(G)$ and is of **Class two** if $\chi'(G) = 1 + \Delta(G)$. Consequently, a major question in the area of edge colorings is that of determining to which of these two classes a given graph belongs. This is far from being an easy question to answer in general, however, as Ian Holyer [130] showed that the problem of determining the chromatic index of an arbitrary graph is **NP**-complete. In fact, the problem is **NP**-complete even for cubic graphs.