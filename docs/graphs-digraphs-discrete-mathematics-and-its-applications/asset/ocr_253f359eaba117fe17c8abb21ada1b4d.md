interested in graph theory early in his mathematical career, at a time when the respectability of graph theory occurred primarily within Hungary. However, Dirac was attracted to graph theory and became one of those mathematicians whose contributions to graph theory brought it to a place of prominence. In fact, the mathematician Carsten Thomassen wrote:

> He (Dirac) was more interested in the intrinsic beauty of graph theory than its applications.

With the aid of Theorem 6.1, a sufficient condition for a graph to have a Hamiltonian path can also be given.

**Corollary 6.3** Let $G$ be a graph of order $n \geq 2$. If $\sigma_2(G) \geq n-1$, then $G$ contains a Hamiltonian path.

**Proof.** Let $H = G \vee K_1$ be the join of $G$ and $K_1$, where $w$ is the vertex of $H$ that does not belong to $G$. Then $\sigma_2(H) \geq n+1$. Since the order of $H$ is $n+1$, it follows by Theorem 6.1 that $H$ is Hamiltonian. Let $C$ be a Hamiltonian cycle of $H$. Deleting $w$ from $C$ produces a Hamiltonian path in $G.$

# The Closure of a Graph

J. Adrian Bondy and Vasek Chvalal [34] observed that the proof of Ore's theorem (Theorem 6.1) neither uses nor needs the full strength of the requirement that the degree sum of each pair of nonadjacent vertices is at least the order of the graph being considered. Initially, Bondy and Chvalal made the following observation.

**Theorem 6.4** Let $u$ and $v$ be nonadjacent vertices in a graph $G$ of order $n$ such that $\deg u + \deg v \geq n$. Then $G + uv$ is Hamiltonian if and only if $G$ is Hamiltonian.

**Proof.** Certainly, if $G$ is Hamiltonian, then $G + uv$ is Hamiltonian. For the converse, suppose that $G + uv$ is Hamiltonian but $G$ is not. Then every Hamiltonian cycle in $G + uv$ contains the edge $uv$, implying that $G$ contains a Hamiltonian $u-v$ path. We can now proceed exactly as in the proof of Theorem 6.1 to produce a contradiction.