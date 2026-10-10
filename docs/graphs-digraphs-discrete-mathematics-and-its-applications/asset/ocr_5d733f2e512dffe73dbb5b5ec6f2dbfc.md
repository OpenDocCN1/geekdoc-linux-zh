*Case 2. One vertex of $S$ lies on $C$*. Then $P - S$ contains a component of order at least 5 and so $|S|/k(P-S) \geq 1$.

*Case 3. Two vertices of $S$ lie on $C$*. Then $|S|=4$ and $P-S$ contains at most four components. Thus, $|S|/k(P-S) \geq 1$. $\blacksquare$

The maximum real number $t$ for which a noncomplete graph $G$ is $t$-*tough* is called the **toughness** of $G$ and is denoted by $t(G)$. Certainly, the toughness of a noncomplete graph is a rational number. Also, $t(G)=0$ if and only if $G$ is disconnected. Indeed, it follows that if $G$ is a noncomplete graph, then

> $\quad\quad\quad t(G)= \min \bigg\{\frac{|S|}{k(G-S)}\bigg\}, \qquad (6.1)$

where the minimum is taken over all vertex-cuts $S$ of $G$.

For the graph $G$ of Figure 6.7, $S_{1} = \{u, v, w\}$, $S_{2} = \{w\}$ and $S_{3} = \{u, v\}$ are three (of many) vertex-cuts. Observe that

$\quad\quad\quad \frac{|S_{1}|}{k(G-S_{1})} = \frac{3}{8}, \quad \frac{|S_{2}|}{k(G-S_{2})} = \frac{1}{3} \quad \text{and} \quad \frac{|S_{3}|}{k(G-S_{3})} = \frac{2}{7}.$

Since there is no vertex-cut $S$ of $G$ with $|S|/k(G-S) < \frac{2}{7}$, it follows that $t(G) = \frac{2}{7}$.

![](bbox=[0.09, 0.55, 0.91, 0.75])

The toughness of a graph $G$ can be considered as a measure of how tightly the subgraphs of $G$ are held together. Thus, the smaller the toughness, the more vulnerable the graph is. A 1-*tough* graph, for example, has the property that breaking the graph into $k$ components (if this is possible) requires the removal of at least $k$ vertices; while breaking a 2-*tough* graph into $k$ components requires the removal of at least $2k$ vertices.

A parameter that plays an important role in the study of toughness is the independence number. The independence number is related to toughness in the sense that among all the vertex-cuts $S$ of a noncomplete graph $G$, the maximum value of $k(G-S)$ is the independence number $\alpha(G)$ of $G$; so for every vertex-cut $S$ of $G$, we have that $\kappa(G) \leq |S|$ and $k(G-S) \leq \alpha(G)$. This leads to bounds for the toughness of a graph obtained by Chvátal [55].