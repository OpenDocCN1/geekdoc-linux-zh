![](bbox=[0.28, 0.13, 0.72, 0.34])

Figure 11.17: An embedding of $K_7$ on the torus

Figure 11.17 shows an embedding of $K_7$ on the torus where the vertex set of $K_7$ is $\{v_1, v_2, \dots, v_7\}$. Because $K_6$ is nonplanar and $K_6$ is a subgraph of a graph that can be embedded on a torus, $\gamma(K_6) = 1$.

Applying Theorem 11.13 to the complete graph $K_n$, $n \geq 3$, we have

$\gamma(K_n) \geq \binom{n}{6} - \frac{n}{2} + 1 = \frac{(n - 3)(n - 4)}{12}$.

Since $\gamma(K_n)$ is an integer,

$\gamma(K_n) \geq \left\lceil \frac{(n - 3)(n - 4)}{12} \right\rceil.$

Born in India, Ted Youngs (1910–1970) received his Ph.D. in 1934. In 1964 he was appointed one of the first faculty members of the University of California Santa Cruz. Born in Austria, Gerhard Ringel (1919–2008) was one of the pioneers of graph theory. He received his Ph.D. from the University of Bonn in Germany in 1951. In addition to his mathematical skills, Ringel was well known for his interest in collecting and breeding butterflies. Ringel left Germany in 1970 to join Youngs at the University of California Santa Cruz in order to complete a proof of a famous theorem in graph theory, which will be discussed in Chapter 16. However, the truth of this theorem required showing that the lower bound for $\gamma(K_n)$ in (11.7) is, in fact, the value of $\gamma(K_n)$, which Ringel and Youngs were successful in accomplishing [204].

**Theorem 11.18** For every integer $n \geq 3$,

$\gamma(K_n) = \left\lceil \frac{(n - 3)(n - 4)}{12} \right\rceil.$

Ringel [203] was also successful in obtaining a formula for the genus of every complete bipartite graph.

**Theorem 11.19** For every two integers $s, t \geq 2$,

$\gamma(K_{s,t}) = \left\lceil \frac{(s - 2)(t - 2)}{4} \right\rceil.$