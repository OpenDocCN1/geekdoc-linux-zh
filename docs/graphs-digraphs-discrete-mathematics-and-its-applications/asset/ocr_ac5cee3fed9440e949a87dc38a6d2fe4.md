![](bbox=[0.15, 0.1, 0.85, 0.35])

Figure 1.8: Isomorphic and non-isomorphic graphs

$\alpha : V(G_3) \rightarrow V(G_1)$, the vertices $\alpha(u_1), \alpha(u_2), \alpha(u_6)$ must also be mutually adjacent in $G_1$. Since $G_1$ does not contain three mutually adjacent vertices, there is no isomorphism from $G_3$ to $G_1$ and so $G_1 \not\cong G_3$. Furthermore, $G_2 \not\cong G_3$ as well.

![](bbox=[0.15, 0.54, 0.85, 0.73])

Figure 1.9: Isomorphic and non-isomorphic graphs

Suppose that two graphs $G$ and $H$ are isomorphic. Then there exists an isomorphism $\phi : V(G) \rightarrow V(H)$. Since $\phi$ is a bijective function, $|V(G)| = |V(H)|$. Furthermore, since two vertices $u$ and $v$ are adjacent in $G$ if and only if $\phi(u)$ and $\phi(v)$ are adjacent in $H$, it follows that $|E(G)| = |E(H)|$. These facts are summarized below, together with another necessary condition for two graphs to be isomorphic.

> **Theorem 1.6** *If two graphs $G$ and $H$ are isomorphic, then they have the same order and the same size, and the degrees of the vertices of $G$ are the same as the degrees of the vertices of $H$.*