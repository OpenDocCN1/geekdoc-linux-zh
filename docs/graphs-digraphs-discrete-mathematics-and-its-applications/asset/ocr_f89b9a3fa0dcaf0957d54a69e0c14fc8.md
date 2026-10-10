# 12.4. DOMINATION

Theorem 12.13 (The König–Egerváry Theorem) If G is a bipartite graph, then

> $$\beta(G)=\alpha^{\prime}(G) .$$

Proof. Since $\beta(G) \geq \alpha^{\prime}(G)$, it suffices to show that $\beta(G) \leq \alpha^{\prime}(G)$. Let $U$ and $W$ be the bipartite sets of $G$ and let $M$ be a maximum matching in $G$. Then $\alpha^{\prime}(G)=|M|$. Denote by $A$ the set of all $M$-unmatched vertices in $U$. (If $A=\emptyset$, then the proof is complete.) Observe that $|M|=|U|-|A|$. Let $S$ be the set of all vertices of $G$ that are connected to some vertex in $A$ by an $M$-alternating path. Define $U^{\prime}=S \cap U$ and $W^{\prime}=S \cap W$.

As in the proof of Hall's theorem (Theorem 12.3), we have that $U^{\prime}-A$ is matched to $W^{\prime}$ and that $N(U^{\prime})=W^{\prime}$. Since $U^{\prime}-A$ is matched to $W^{\prime}$, it follows that $|U^{\prime}|-|W^{\prime}|=|A|$.

Observe that $C=(U-(U^{\prime})) \cup W^{\prime}$ is a vertex cover in $G$; for otherwise, there is an edge $vw$ in $G$ such that $v \in U^{\prime}$ and $w \notin W^{\prime}$. Furthermore,

> $$|C|=|U|-|U^{\prime}|+|W^{\prime}|=|U|-|A|=|M| .$$

Therefore, $\beta(G) \leq|C|=|M|=\alpha^{\prime}(G)$ and the proof is complete.

As a consequence of the König–Egerváry theorem (Theorem 12.13) and Hall's theorem (Theorem 12.11), we have the following result of König and Richard Rado [192].

Theorem 12.14 (The König–Rado Theorem) If G is a bipartite graph without isolated vertices, then

> $$\alpha(G)=\beta^{\prime}(G) .$$

Proof. By Theorems 12.11 and 12.13,

> $$\alpha(G)+\beta(G)=\alpha^{\prime}(G)+\beta^{\prime}(G) \text { and } \beta(G)=\alpha^{\prime}(G) .$$

Thus $\alpha(G)=\beta^{\prime}(G)$.

# 12.4 Domination

An area of graph theory that has received increased attention during recent decades is that of domination in graphs. A vertex $v$ in a graph $G$ is said to **dominate** itself and each of its neighbors, that is, $v$ dominates the vertices in its closed neighborhood $N[v]$. A set $S$ of vertices of $G$ is a **dominating set** of $G$ if every vertex of $G$ is dominated by at least one vertex of $S$. Equivalently, a set $S$ of vertices of $G$ is a dominating set if every vertex in $V(G)-S$ is adjacent to at least one vertex in $S$. The minimum cardinality among the dominating sets of $G$ is called the **domination number** of $G$ and is denoted by $\gamma(G)$. A dominating set of cardinality $\gamma(G)$ is then referred to as a **minimum dominating set**. Although $\gamma(G)$ is the same notation that is used for the genus of a graph $G$,