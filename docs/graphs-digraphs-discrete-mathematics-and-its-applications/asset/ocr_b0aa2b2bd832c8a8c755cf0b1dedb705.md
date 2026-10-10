are written is not important). If $n_i = 1$ for all $i$ $(1 \leq i \leq k)$, then $\mathbf{G}$ is the complete graph $K_k$. A **complete multipartite graph** is a complete $k$-partite graph for some integer $k \geq 2$. Some complete multipartite graphs are shown in Figure 1.18

![](bbox=[0.15, 0.16, 0.85, 0.32])

Figure 1.18: Some complete multipartite graphs

# # 1.6 Operations on Graphs

There are many ways of producing a new graph from one or more given graphs. The most common of these is the complement of a graph.

# ## The Complement of a Graph

The **complement** $\overline{G}$ of a graph $G$ is that graph with vertex set $V(G)$ such that two vertices are adjacent in $\overline{G}$ if and only if these vertices are not adjacent in $G$. Any isomorphism from a graph $G$ to a graph $H$ is also an isomorphism from $\overline{G}$ to $\overline{H}$. Consequently, $\overline{G} \cong \overline{H}$ if and only if $G \cong H$. If $G$ is a graph of order $n$ and size $m$, then $\overline{G}$ is a graph of order $n$ and size $\binom{n}{2} - m$. A graph $G$ and its complement are shown in Figure 1.19. The complement $\overline{K_n}$ of the complete graph $K_n$ is the empty graph of order $n$.

![](bbox=[0.2, 0.72, 0.8, 0.85])

Figure 1.19: A graph and its complement

A graph $G$ is **self-complementary** if $G$ is isomorphic to $\overline{G}$. Certainly, if $G$ is a self-complementary graph of order $n$, then its size is $m = \binom{n}{2}/2 = n(n - 1)/4$. Since only one of $n$ and $n - 1$ is even, either $4 \mid n(n - 1)$; that is, if $G$ is a self-complementary graph of order $n$, then either $n \equiv 0 \pmod{4}$ or