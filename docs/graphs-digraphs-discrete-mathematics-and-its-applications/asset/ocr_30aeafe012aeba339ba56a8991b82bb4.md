# The Square and Cube of a Graph

Associated with each connected graph of order $n$ and diameter $d$ is a class of graphs defined in terms of distance. For each positive integer $k$, the **kth power** $G^k$ of a graph $G$ is that graph with $V(G^k) = V(G)$ and $uv \in E(G^k)$ if and only if $1 \leq d_G(u, v) \leq k$. Thus, $G^1 = G$ and $G^k = K_n$ if $k \geq d$. The graph $G^2$ is also called the **square** of $G$, while $G^3$ is called the **cube** of $G$. A graph $G$ with its square and cube are shown in Figure 6.14. While the graph $G^3$ of Figure 6.14 is Hamiltonian, $G^2$ is not.

![](bbox=[0.03, 0.46, 0.97, 0.65])

Figure 6.14: A graph and its square and cube

Since the $k$th power $G^k$ $(k \geq 2)$ of a connected graph $G$ contains $G$ as a subgraph (as a proper subgraph if $G$ is not complete), it follows that $G^k$ is Hamiltonian if $G$ is Hamiltonian. Even if $G$ is not Hamiltonian, $G^k$ is Hamiltonian for a sufficiently large integer $k$. It is therefore natural to ask for the minimum positive integer $k$ for which $G^k$ is Hamiltonian. Certainly, for connected graphs in general, $k = 2$ will not suffice since the graph $G^2$ of Figure 6.14 is not Hamiltonian. We noted that $G^3$ is Hamiltonian, however. In fact, the cube of every connected graph of order at least 3 is Hamiltonian. Indeed, a stronger result exists, discovered by Milan Šakanin [218] and later, but independently, by Jerome Karaganas [138].

**Theorem 6.22** If $G$ is a connected graph, then $G^3$ is Hamiltonian-connected.

**Proof.** If $H$ is a spanning tree of $G$ and $H^3$ is Hamiltonian-connected, then $G^3$ is Hamiltonian-connected. Hence, it suffices to prove that the cube of every