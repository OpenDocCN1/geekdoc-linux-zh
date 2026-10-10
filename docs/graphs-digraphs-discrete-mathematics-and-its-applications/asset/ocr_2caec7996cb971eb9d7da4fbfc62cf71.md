# 7.1. INTRODUCTION TO DIGRAPHS

![](bbox=[0.18, 0.13, 0.85, 0.3])

A digraph $D_1$ is a **subdigraph** of a digraph $D$ if $V(D_1) \subseteq V(D)$ and $E(D_1) \subseteq E(D)$. We use $D_1 \subseteq D$ to indicate that $D_1$ is a subdigraph of $D$. A subdigraph $D_1$ of $D$ is a **spanning subdigraph** of $D$ if $V(D_1) = V(D)$. Vertex-deleted, arc-deleted, induced and arc-induced subdigraphs are defined in the expected manner. These last two concepts are illustrated for the digraph $D$ of Figure 7.4, where

$V(D)=\{v_1, v_2, v_3, v_4\}$, $U=\{v_1, v_2, v_3\}$ and $X=\{(v_1, v_2), (v_2, v_4)\}.$

![](bbox=[0.15, 0.5, 0.85, 0.68])

We now consider certain types of digraphs that occur periodically. A digraph is **symmetric** if whenever $(u,v)$ is an arc of $D$, then $(v,u)$ is an arc of $D$ as well. There is a natural one-to-one correspondence between symmetric digraphs and graphs. The **complete symmetric digraph** $K_n^s$ of order $n$ has both arcs $(u, v)$ and $(v, u)$ for every two distinct vertices $u$ and $v$. A digraph is called an **oriented graph** if whenever $(u, v)$ is an arc of $D$, then $(v, u)$ is *not* an arc of $D$. Thus, an oriented graph $D$ can be obtained from a *graph* $G$ by assigning a direction to (or by “orienting”) each edge of $G$, thereby transforming each edge of a graph $G$ into an arc and transforming $G$ itself into an oriented graph. The digraph $D$ is also called an **orientation** of $G$. Figure 7.5 shows three digraphs $D_1, D_2$ and $D_3$. While $D_1$ is a symmetric digraph and $D_2$ is an oriented graph, the digraph $D_3$ is neither. The **underlying graph** of a digraph $D$ is that graph obtained by replacing each arc $(u, v)$ or symmetric pair $(u, v)$, $(v, u)$ of arcs by the edge $uv$. The underlying graph of each digraph in Figure 7.5 is the graph $G$.