$B_i = G[\backslash V(G_i) \cup \{v\}]$ are connected and referred to as the **branches** of $G$ at $v$. If a branch $B_i$ contains no cut-vertices of $G$, then $B_i$ is a **block** of $G$ – in fact, an **end-block** of $G$.

A connected graph $G$ containing three cut-vertices $u$, $v$ and $w$ and six blocks is shown in Figure 3.3. Four of these blocks are end-blocks. The graph $G$ has four branches at $v$, all of which are shown in Figure 3.3. Two of the four branches at $v$ are end-blocks of $G$.

![](bbox=[0.08, 0.31, 0.93, 0.65])

# ### 3.2 Introduction to Trees

We have seen that a connected graph may contain a vertex whose removal results in a disconnected graph and that such a vertex is a cut-vertex. There are also edges possessing this property.

# #### Bridges

An edge $e=uv$ in a connected graph $G$ whose removal results in a disconnected graph is a **bridge**. Necessarily, $G-e$ consists of two components, one containing $u$ and the other containing $v$. More generally, an edge $e$ is a bridge in a graph $G$ (connected or not) if $k(G-e)>k(G)$. Then $k(G-e)=k(G)+1$. In the graph $G$ of Figure 3.4, $v_3v_6$, $v_7$, $v_8$ and $v_9$ are cut-vertices, while $v_2v_5$, $v_5v_6$, $v_7v_{11}$ and $v_8v_9$ are bridges.

While there are connected graphs no vertex of which is a cut-vertex (the nonseparable graphs), there is no connected graph in which every vertex is a cut-vertex (see Theorem 3.1). There are, however, connected graphs in which every edge is a bridge. It is this class of graphs that we study in the current section. First, we discuss an important property of bridges.