![](bbox=[0.35, 0.09, 0.72, 0.42])

Figure 13.16: A cyclic decomposition of $K_{11}$ into copies of the nongraceful graph $C_5$

# Ringel's Conjecture  For every tree $T$ of size $m$, the complete graph $K_{2m+1}$ is $T$-decomposable.

Not only does the truth of Kotzig's conjecture imply the truth of Ringel's conjecture, the truth of Kotzig's conjecture also implies the truth of the following conjecture, due jointly to Ringel and Kotzig.

# The Ringel-Kotzig Conjecture  For every tree $T$ of size $m$, $K_{2m+1}$ can be cyclically decomposed into copies of $T$.

Although there are no general sufficient conditions for a graph to be graceful, there are necessary conditions.

# Theorem 13.19  If $G$ is a graceful graph of size $m$, then there exists a partition of $V(G)$ into two subsets $V_{e}$ and $V_{o}$ such that the number of edges joining $V_{e}$ and $V_{o}$ is $\lceil m/2 \rceil$.

**Proof.**  Let a graceful labeling of $G$ be given. Denote the set of vertices labeled with an even integer by $V_{e}$ and the set of vertices labeled with an odd integer by $V_{o}$. All edges labeled with an odd integer must then join a vertex of $V_{e}$ and a vertex of $V_{o}$. Since there are $\lceil m/2 \rceil$ such edges, the result follows.

Theorem 13.19 will be revisited again in Chapter 19. The following necessary condition for an Eulerian graph to be graceful is due to Rosa [211].

# Theorem 13.20  If $G$ is a graceful Eulerian graph of size $m$, then

$m \equiv 0 \pmod 4$ or $m \equiv 3 \pmod 4$.