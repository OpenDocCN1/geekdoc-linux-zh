![](bbox=[0.25, 0.11, 0.82, 0.27])

+   (a) Prove that the balanced chromatic number is defined for every graph $G$.
+   (b) Determine $\chi_b(G)$ for the graph $G$ in Figure 14.9.

+   11. Let $G$ be an $r$-regular graph, $r \geq 3$, such that $3 \leq \chi(G) \leq r + 1$. Prove or disprove the following:
+       (a) For every edge $e$ of $G$, there exists an odd cycle containing $e$.
+       (b) For every edge $e$ of $G$, there exists an odd cycle not containing $e$.

+   12. (a) Show for every graph $G$ that
+   $$\chi(G)=\max \{\chi(H): H \text { is a subgraph of } G\}.
+   $$
+       (b) The problem in (a) should suggest a question to you. Ask and answer this question.

+   13. Prove Theorem 14.4: For graphs $G_1, G_2, \ldots, G_k$ and $G=G_1+G_2+\cdots+G_k$, $\chi(G)=\max\{\chi(G_i):1 \leq i \leq k\}$.

+   14. Prove Theorem 14.6: If $G$ is a graph with blocks $B_1$, $B_2$, ..., $B_k$, then $\chi(G)=\max\{\chi(B_i):1 \leq i \leq k\}$.

+   15. Prove Theorem 14.7: For graphs $G_1, G_2, \ldots, G_k$ and $G=G_1 \vee G_2 \vee \cdots \vee G_k$, $\chi(G)=\sum_{i=1}^{k} \chi(G_i)$.

+   16. Let $G$ be a graph of order $n$ with independence number $\alpha(G)=2$.
+       (a) Prove that if $G$ is disconnected, then $G$ contains $K_{\left\lceil \frac{n}{2} \right\rceil}$ as a subgraph.
+       (b) Prove that if $G$ is connected, then $G$ contains a path $(u, v, w)$ such that $uv \notin E(G)$ and every vertex in $G-\{u, v, w\}$ is adjacent to either $u$ or $w$ (or both).

+   17. By Theorem 14.9, it follows that for every graph $G$ of order $n$,
+   $$\frac{n}{\alpha(G)} \leq \chi(G) \leq n-\alpha(G)+1 .
+   $$
+       Prove or disprove: The chromatic number of a graph $G$ can never be closer to $n-\alpha(G)+1$ than to $\frac{n}{\alpha(G)}$.