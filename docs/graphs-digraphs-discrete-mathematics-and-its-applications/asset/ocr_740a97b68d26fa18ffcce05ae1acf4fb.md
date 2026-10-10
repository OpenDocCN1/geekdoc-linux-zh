there exists a connected and bridgeless graph $G$ that has no strong orientation. Among the subgraphs of $G$, let $H$ be one of maximum order that has a strong orientation. Such a subgraph exists since for each $v \in V(G)$, the subgraph $G[\{v\}]$ trivially has a strong orientation. Thus, $|V(H)| < |V(G)|$, since, by assumption, $G$ has no strong orientation.

Assign directions to the edges of $H$ so that the resulting digraph $D$ is strong, but assign no directions to the edges of $G - E(H)$. Let $u \in V(H)$ and let $v \in V(G) = V(H)$. Since $G$ is connected and bridgeless, it follows by Theorem 4.18 that $G$ contains two edge-disjoint $u-v$ paths. Let $P$ be one of these $u-v$ paths and let $Q$ be the $v-u$ path that results from the other $u-v$ path. Further, let $u_1$ be the last vertex of $P$ that belongs to $H$, let $v_1$ be the first vertex of $Q$ belonging to $H$. Next, let $P_1$ be the $u_1-v$ subpath of $P$ and let $Q_1$ be the $v-v_1$ subpath of $Q$. Direct the edges of $P_1$ from $u_1$ toward $v$, producing the directed path $P_1^*$ and direct the edges of $Q_1$ from $v$ toward $v_1$, producing the directed path $Q_1^*.$

Define the digraph $D'$ by

$V(D') = V(D) \cup V(P_1^*) \cup V(Q_1^*)$ and $E(D') = E(D) \cup E(P_1^*) \cup E(Q_1^*)$. Since $D$ is strong, so too is $D'$, contradicting the choice of $H$.

As we mentioned, Theorem 7.5 is due to Robbins. The paper in which this theorem appears is titled “A theorem on graphs, with an application to a problem of traffic control” and was published in 1939 in the *American Mathematical Monthly*, only a year after Robbins received his Ph.D. from Harvard University in topology, under the direction of Hassler Whitney. This was only Robbins’ second publication of what would become a long and impressive list. Also in 1939, at age 24, Robbins began work on the classic book *What is Mathematics?* with Richard Courant. Robbins classified this book as a literary work rather than a scientific work. This book discussed mathematics as it existed at that time. A few years later, Robbins became interested in and devoted his research to mathematical statistics, to which he made major contributions.

# ### 7.3 Eulerian and Hamiltonian Digraphs

Eulerian and Hamiltonian graphs have natural analogues for digraphs. In both instances, these are strong digraphs.

# **Eulerian Digraphs**

An **Eulerian circuit** in a connected digraph $D$ is a circuit that contains every arc of $D$ (necessarily exactly once); while an **Eulerian trail** in $D$ is an open trail that contains every arc of $D$. A connected digraph that contains an Eulerian circuit is an **Eulerian digraph**. The next theorem gives a character-