![](bbox=[0.14, 0.13, 0.86, 0.61])

For two graphs $F$ and $H$, the **Ramsey number** $R(F, H)$ is the minimum order $n$ of a complete graph such that for every red-blue coloring of $K_n$, there is either a subgraph isomorphic to $F$, all of whose edges are colored red (a red $F$), or a subgraph isomorphic to $H$, all of whose edges are colored blue (a blue $H$). The Ramsey number $R(F, H)$ exists for every two graphs $F$ and $H$. In fact, if $F$ has order $s$ and $H$ has order $t$, then

$$R(F, H) \leq R(s, t) .$$

To illustrate a Ramsey number of this type, we determine the Ramsey number $R(P_4, K_4)$.

+   Example 20.10    $R(P_4, K_4) = 10$.

Proof. To show that $R(P_4, K_4) \geq 10$, consider the red-blue coloring of $K_9$ in which the red subgraph is $3K_3$. Since the order of every component of $3K_3$ is 3, there is no red $P_4$ in this red-blue coloring of $K_9$. The blue subgraph in this case is $K_{3,3,3}$, which does not contain a 4-clique. Hence, there is also no blue $K_4$ in this red-blue coloring of $K_9$. Therefore, $R(P_4, K_4) \geq 10$.

We now show that $R(P_4, K_4) \leq 10$. Let there be given a red-blue coloring of $G = K_{10}$. We show that there is either a red $P_4$ or a blue $K_4$. Suppose first