two vertices of $T(G)$ are adjacent if the corresponding elements in $G$ are two adjacent vertices, two adjacent edges or an incident vertex and edge. A graph $H$ and its total graph $T(H)$ are shown in Figure 6.19.

![](bbox=[0.25, 0.17, 0.75, 0.4])

One might observe that $T(H) \cong G^{2}$ for the graph $H$ of Figure 6.19 and the graph $G$ of Figure 6.14. We saw that $G^{2}$ is not Hamiltonian. Thus, for the graph $H$ of Figure 6.19, $T(H)$ is not Hamiltonian. This, in fact, is not surprising for if $F$ is any graph, then $T(F) \cong [S(F)]^{2}$, that is, the total graph of $F$ is the square of the subdivision graph of $F$. Since the graph $G$ of Figure 6.14 is isomorphic to $S(K_{1,3})$ and the graph $H$ of Figure 6.19 is isomorphic to $K_{1,3}$, it follows that $T(H) \cong G^{2}$, where $G$ is the graph of Figure 6.14.

While the total graph of a nontrivial connected graph $G$ need not be Hamiltonian, the same cannot be said for $T(T(G)).$

**Theorem 6.30** If $G$ is a nontrivial connected graph, then $T(T(G))$ is Hamiltonian.

**Proof.** First, we consider $T(G)$. Since $S(G)$ is a nontrivial connected graph, $[S(G)]^{2}$ is 2-connected and $T(G) \cong [S(G)]^{2}$, it follows that $H = T(G)$ is 2-connected. Hence, $S(H)$ is 2-connected. By Theorem 6.23, $[S(H)]^{2}$ is Hamiltonian. Thus, $T(H) \cong [S(H)]^{2}$ and so $T(T(G))$ is Hamiltonian.