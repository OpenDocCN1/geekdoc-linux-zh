# 6.4. HIGHLY HAMILTONIAN GRAPHS

construct the closure $F=CL(H)$ of $H$. Since $\mathrm{deg}_{H} x+$ $\operatorname{deg}_{H} y \geq n+1$ for every two nonadjacent vertices $x$ and $y$ of $H$ that belong to $G$, it follows that $F[\lceil V(G)] = K_{n}$. Furthermore, if $x \in V(G)-\{u, v\}$, then $\mathrm{deg}_{F} x+\mathrm{deg}_{F} w \geq$ $(n-1)+2 = n+1$ so that $x w \in E(F)$. Therefore, $F=CL(H)=K_{n+1}$, which implies by Theorem 6.7 that $H$ is Hamiltonian. Since $\operatorname{deg}_{H} w=2$, every Hamiltonian cycle $C$ of $H$ must contain the edges $w u$ and $w v$. Removing $w$ from $C$ produces a Hamiltonian $u-v$ path in $G$.

There is now an immediate corollary, similar in statement to the sufficient condition given in Corollary 6.2 for a graph to be Hamiltonian.

> **Corollary 6.16** Let $G$ be a graph of order $n$ such that
> 
> $\operatorname{deg} v \geq(n+1) / 2$
> 
> for every vertex $v$ of $G$, then $G$ is Hamiltonian-connected.

# Hamiltonian Extension Numbers

As indicated by Hamilton’s remarks, the graph of the dodecahedron in Figure 6.2 is Hamiltonian. Indeed, Hamilton’s statement implies that this graph has a much stronger property. As was mentioned in the construction pamphlet to his Icosian Game, Hamilton also observed that every path of order 5 in the graph $G$ of the dodecahedron lies on a Hamiltonian cycle of $G$. (He didn’t use that terminology of course.) Although Hamilton didn’t mention that this is also true of paths of smaller order but not true of all paths of order 6 (see Exercise 1), this is nevertheless the case. This leads to another class of highly Hamiltonian graphs.

The **Hamiltonian extension number** of a Hamiltonian graph $G$, denoted by $\mathrm{he}(G)$, is the maximum positive integer $k$ for which every path in $G$ having order $k$ or less lies on a Hamiltonian cycle of $G$. Hence, $\operatorname{he}(G)=5$ for the graph $G$ of the dodecahedron.

By Dirac’s theorem (Corollary 6.2), if $G$ is a graph of even order $n \geq 4$ with $\delta(G) \geq n / 2$, then $G$ contains a Hamiltonian cycle. Obviously, every vertex of $G$ lies on a Hamiltonian cycle of $G$ and so $\operatorname{he}(G) \geq 1$. For each even integer $n \geq 4$, the graph $H=K_{2} \vee\left(2 K_{[n-2) / 2}\right)$ has order $n$ and $\delta(H)=n / 2$ such that not every edge of $H$ lies on a Hamiltonian cycle of $H$. For example, the Hamiltonian graph $H$ of order $n=6$ in Figure 6.10 has $\delta(H)=n / 2=3$ but no Hamiltonian cycle of $H$ contains the edge $u w$ (that is, no Hamiltonian cycle of $H$ contains the path $(u, v)$ of order 2). Thus, $\operatorname{he}(H)=1$. Because every edge of a Hamiltonian-connected graph $G$ lies on a Hamiltonian cycle of $G$, it follows by Corollary 6.16 that if $G$ is a graph of order $n \geq$ such that $\delta(G) \geq(n+1) / 2$, then $\operatorname{he}(G) \geq 2$. This is a special case of a more general result.

> **Corollary 6.17** Let $k$ and $n$ be integers such that $n \geq 3$ and $1 \leq k < n$. If $G$ is a graph of order $n \geq 3$ and $\delta(G) \geq(n+k-1) / 2$, then $\operatorname{he}(G) \geq k$.