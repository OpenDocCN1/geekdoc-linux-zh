recognizable; indeed, the degree of regularity is a recognizable parameter. For regular graphs, much more can be said.

**Theorem 9.8** Every regular graph of order at least 3 is reconstructible.

**Proof.** As we have already mentioned, regularity and the degree of regularity are recognizable. Thus, without loss of generality, we may assume that $G$ is an $r$-regular graph with $V(G)=\{v_1, v_2, \dots, v_n\}$, $n\geq 3$. It remains to show that $G$ is uniquely determined by its subgraphs $G-v_i$, $i=1, 2, \dots, n$. Consider $G-v_1$, say. The graph $G-v_1$ then has order $n-1$, where $r$ vertices have degree $r-1$ and the remaining $n-r-1$ vertices have degree $r$. Adding the vertex $v_1$ to $G-v_1$ together with all those edges $v_1v$ where $\deg_{G-v_1}v=r-1$ produces the graph $G$.

If $G$ has order $n\geq 3$, then it can be determined whether $G$ is connected from the $n$ subgraphs $G-v$, $v\in V(G)$.

**Theorem 9.9** For graphs of order at least 3, connectedness is a recognizable property. In particular, if $G$ is a graph with $V(G)=\{v_1, v_2, \dots, v_n\}$, $n\geq 3$, then $G$ is connected if and only if at least two of the subgraphs $G-v_i$ are connected.

**Proof.** Let $G$ be a connected graph. By Theorem 3.1, $G$ contains at least two vertices that are not cut-vertices, implying the results.

Conversely, assume that there exist vertices $v_1, v_2\in V(G)$ such that both $G-v_1$ and $G-v_2$ are connected. Thus, $G-v_1$ and also in $G$, the vertex $v_2$ is connected to each vertex $v_i$ for $i\geq 3$. Moreover, in $G-v_2$ (and thus in $G$), $v_1$ is connected to each vertex $v_i$ for $i\geq 3$. Hence, every pair of vertices of $G$ are connected and so $G$ is connected.

Since connectedness is a recognizable property, it is possible to determine from the subgraphs $G-v$, $v\in V(G)$, whether a graph $G$ of order at least 3 is disconnected. We now show that disconnected graphs are reconstructible. There have been several proofs of this fact. The proof given here is due to Bennett Manvel [162].

**Theorem 9.10** Disconnected graphs of order at least 3 are reconstructible.

**Proof.** We have already noted that disconnectedness in graphs of order at least 3 is a recognizable property. Thus, we assume, without loss of generality, that $G$ is a disconnected graph with $V(G)=\{v_1, v_2, \dots, v_n\}$, $n\geq 3$. Further, let $G_i=G-v_i$ for $i=1, 2, \dots, n$. From Theorem 9.7, the degrees of the vertices $v_i$, $i=1, 2, \dots, n$, can be determined from the graphs $G_i$, $i=1, 2, \dots, n$. Hence, if $G$ contains an isolated vertex, then $G$ is reconstructible. Assume then that $G$ has no isolated vertices.

Since every component of $G$ is nontrivial, it follows that $k(G_j)\geq k(G)$ for $i=1, 2, \dots, n$ and that $k(G_j)=k(G)$ for some integer $j$ satisfying $1\leq j\leq$