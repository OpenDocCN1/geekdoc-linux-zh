# 4.1. CONNECTIVITY AND EDGE-CONNECTIVITY

$G$ is not a complete graph. Hence, there exists a vertex-cut $U$ of $G$ such that $|U|=\ell \le k-1$. The graph $G-U$ is therefore disconnected and has order $n-\ell$. Let $G_{1}$ be a component of $G-U$ of smallest order, say $n_{1}$. Thus $n_{1} \le \lfloor(n-\ell)/2\rfloor$. Let $v$ be a vertex of $G_{1}$. Necessarily, $v$ is adjacent in $G$ only to vertices of $U$ and to other vertices of $G_{1}$. Hence,

```
deg v $\begin{array}{lll} & \leq & \ell+\left(n_{1}-1\right) \leq \ell+\lfloor(n-\ell) / 2\rfloor-1 \\ & = & \lfloor(n+k-2) / 2\rfloor \leq\lceil(n+k-3) / 2\rceil,\end{array}$
```

contrary to the hypothesis.

# The Edge-Connectivity of a Graph

How connected a graph $G$ can be measured not only in terms of the number of vertices that need to be deleted from $G$ to arrive at a disconnected or trivial graph but in terms of the number of edges that must be deleted from $G$ to arrive at such a graph.

An **edge-cut** of a graph $G$ is a subset $X$ of $E(G)$ such that $G-X$ is disconnected. An edge-cut of minimum cardinality in $G$ is a **minimum edge-cut** and this cardinality is the **edge-connectivity** of $G$, which is denoted by $\lambda(G)$. (The symbol $\lambda$ is the Greek letter *lambda*.) The trivial graph $K_{1}$ does not contain an edge-cut but we define $\lambda(K_{1})=0$. Therefore, $\lambda(G)$ is the minimum number of edges whose removal from $G$ results in a disconnected or trivial graph. Since the set of edges incident with any vertex of a graph $G$ of order $n$ is an edge-cut of $G$, it follows that

```
$0 \leq \lambda(G) \leq \delta(G) \leq n-1$. (4.1)
```

A graph $G$ is $k$-**edge-connected**, $k \geq 1$, if $\lambda(G) \geq k$. That is, $G$ is $k$-edge-connected if the removal of fewer than $k$ edges from $G$ results in neither a disconnected graph nor a trivial graph. Thus, a 1-edge-connected graph is a nontrivial connected graph and a 2-edge-connected graph is a nontrivial connected bridgeless graph.

For the graph $G$ of Figure 4.2, $n(G)=2$ and $\lambda(G)=3$. Both $\{u, v_{1}\}$ and $\{u, v_{2}\}$ are minimum vertex-cuts, while $\{e_{1}, e_{2}, e_{3}\}$ is a minimum edge-cut. The class of $k$-edge-connected graphs is characterized in the following simple but useful theorem.

**Theorem 4.2** A nontrivial graph $G$ is $k$-edge-connected if and only if there exists no nonempty proper subset $W$ of $V(G)$ such that the number of edges joining $W$ and $V(G)-W$ is less than $k$.

**Proof.** First assume that there exists no nonempty proper subset $W$ of $V(G)$ such that the number of edges joining $W$ and $V(G)-W$ is less than $k$ but that $G$ is not $k$-edge-connected. Since $G$ is nontrivial, there exist $\ell$ edges, where