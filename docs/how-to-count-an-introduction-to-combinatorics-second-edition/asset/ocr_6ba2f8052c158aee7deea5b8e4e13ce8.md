# **DEFINITION 10.4**

Let $G$ be a graph. We say that the subgraph $G'$ *spans* $G$ if it has the same vertices as $G$. A *spanning tree* of $G$ is a subgraph that spans $G$ and that is a tree.

Which graphs have spanning trees? If $G$ is not connected, then no subgraph with the same set of vertices can be connected, and so $G$ does not have a spanning tree. On the other hand it is not difficult to show that every connected graph has a spanning tree. In particular, for large $n$, the complete graph $K_n$ has lots of spanning trees. If we label the vertices of the complete graph, $K_n$, with $n$ vertices with the numbers $1,2,\dots,n$, then the spanning trees for $K_n$ correspond to the labeled trees with $n$ vertices, and so by Cayley’s theorem, $K_n$ has $n^{n-2}$ different spanning trees.

In many practical applications we seek more than just a spanning tree. We illustrate this with the following problem, before discussing the general case.

# **PROBEM 10.4**

It is desired to connect five islands by tunnels. The graph in Figure 10.14 shows the cost (in suitable units, for example, 1 unit = £10,000,000) of building a tunnel between pairs

![](bbox=[0.27, 0.43, 0.73, 0.64])

![](bbox=[0.27, 0.67, 0.73, 0.91])