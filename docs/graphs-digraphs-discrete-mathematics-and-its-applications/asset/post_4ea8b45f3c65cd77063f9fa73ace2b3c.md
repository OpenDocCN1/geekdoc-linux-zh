
## Section 16.5

- 11. Recall that the chromatic polynomial of a graph *G* of order *n* can be expressed as
  $$P(G, \lambda) = \lambda^n - a_1 \lambda^{n-1} + a_2 \lambda^{n-2} + \dots + (-1)^{n+1} a_{n-1} \lambda .$$

- 13. (a) See the figure below.

![](img/598a6ae3fd44120830ada34717906f29_596_0.png)

(b) $P(K_{2,2,2}, 3) = 6 = \chi(K_{2,2,2})!$

- 15. (a) Every two unicyclic graphs of the same order and containing a cycle of the same length are chromatically equivalent.

(b) *n* - 2.

- 17. (a) Assume that the statement is false. Then among all counterexamples, let *S* be the set of those of minimum order *n* and let *G* be a graph in *S* of minimum size *m*. Then $P(G, \lambda) = \lambda g(\lambda)$ where $g(0) = 0$. Then *G* is not a tree. Let $e = uv$ be an edge of *G* that is not a bridge and let *H* be the graph obtained by identifying *u* and *v* in $G - e$. Consider the coefficients of $\lambda$ in $P(G, \lambda)$, $P(G - e, \lambda)$ and $P(H, \lambda)$.

(b) Apply Exercise 16 and (a).

- 19. Proceed by induction on the number of blocks in *G* and apply Exercise 16.

- 21. Since $K_{r,r}$ is the only bipartite graph of order 2*r* and size $r^2$, it is chromatically unique.

- 23. The vertices of *G* can be listed as $v_1, v_2, \dots, v_n$ such that $v_i$ ($2 \leq i \leq n$) is adjacent to at least one vertex of $\{v_1, v_2, \dots, v_{i-1}\}$. Consider the number of ways that the vertices of *G* can be colored using this ordering.

- 25. The statement is true.

## Section 16.6

- 27. (a) See the figure below. (b) By the Generalized Euler Identity (Theorem 11.10), $r = 5$. (c) Five colors are needed.

![](img/598a6ae3fd44120830ada34717906f29_597_0.png)

- 29. Consider the graph $K_8$.

## Chapter 17

### Section 17.1

- 1. The chromatic index of this graph is 4.
- 3. Since $\Delta(G \square K_2) = 1 + \Delta(G)$, it suffices to show that there exists a $(1 + \Delta(G))$-edge coloring of $G \square K_2$. Because $\chi'(G) \leq 1 + \Delta(G)$, there exists a $(1 + \Delta(G))$-edge coloring of $G$.
- 5. (a) Observe that $G$ contains $G_1$, $G_2$ and the complete bipartite graph $K_{n_1,n_2}$ as subgraphs.
(b) Consider $G_1 = K_2$ and $G_2 = C_5$.

### Section 17.2

- 7. Show that $G$ is overfull and apply Corollary 17.9.
- 9. Since $G$ is 3-regular, it follows that $G$ has even order. Consider a Hamiltonian cycle $C$ of $G$.
- 11. The graph of each regular polyhedra is of Class one.
- 13. Show that there exists a $\Delta(G)$-regular bipartite graph containing $G$ as an induced subgraph.
- 15. Apply Theorem 17.8.
- 17. Let $G = C_n \square K_2$ where $n \geq 3$ is odd.
- 19. Apply Theorem 17.8.
- 21. Apply Corollary 17.9.
- 23. (a) France has two consecutive days off.
(b) Player B only plays in one match on Day 4 and all other players play at least two matches every day.
- 25. The graph $G$ is overfull.

### Section 17.3

- 27. (a) No. (b) Yes.
- 29. (a) No. (b) No. (c) Yes.
- 31. (a) $\chi'(G) = 4$. (b) No.

## Chapter 18

### Section 18.1

- 1. See the figure below.

![](img/598a6ae3fd44120830ada34717906f29_598_0.png)

- 3. Show that $\sigma^+(v; a\omega_1 + b\omega_2) = \sigma^-(v; a\omega_1 + b\omega_2)$ for integers $a$ and $b$ and for every vertex $v$ of $D$.

- 5. Let $G$ be a bridgeless graph containing an Eulerian trail and let $u$ and $v$ be the two odd vertices of $G$. Then $G$ is 2-edge-connected and by Theorem 4.18, $G$ contains two edge-disjoint $u-v$ paths $P$ and $P'$. Begin by assigning flow values to the appropriately directed edges of these paths.

- 7. Let $V(K_6) = \{1, 2, 3, 4, 5, 6\}$. A cycle double cover of $K_6$ consisting of five Hamiltonian cycles is $(1,2,3,4,5,6,1)$, $(1,3,6,2,5,4,1)$, $(1,4,2,6,5,3,1)$, $(1,5,2,3,4,6,1)$, $(1,2,4,6,5,3,1)$.

### Section 18.2

- 9. Let $\Delta(G) = \Delta$ and for each edge $e$ of $G$, let $L(e)$ be a list of $2\Delta - 1$ colors (positive integers). Let $e_1, e_2, \dots, e_m$ be an ordering of the edges of $G$ and give a greedy coloring of the edges.

### Section 18.3

- 11. $\chi(G) = 3$, $\chi'(G) = 4$ and $\chi''(G) = 5$.
- 13. $\chi'(G) = 4$.
- 15. Since $\Delta(K_{s,t}) = t$, it follows that $\chi''(K_{s,t}) \geq t + 1$. Describe a $(t + 1)$-total coloring of $K_{s,t}$.

## Chapter 19

### Section 19.1

- 1. $T_{7,2} = K_{3,4}$, $t_{7,2} = 12$, $T_{7,3} = K_{2,2,3}$, $t_{7,3} = 16$, $T_{7,4} = K_{1,2,2,2}$, $t_{7,4} = 18$, $T_{8,2} = K_{4,4}$, $t_{8,2} = 16$, $T_{8,3} = K_{2,2,3}$, $t_{8,3} = 21$, $T_{8,4} = K_{2,2,2,2}$, $t_{8,4} = 24$.
- 3. $m = 13$.
- 5. Show that $G$ contains a vertex of degree 2 or more.
- 7. For $n \geq 4$, the smallest integer $m$ such that every graph of order $n$ and size $m$ contains $\overline{K}_{1,3}$ as a subgraph is $n + 1$.
- 9. (a) Let $e = uv$ be an edge of $G$, let $A = N(u) - \{v\}$ and let $B = N(v) - \{u\}$. First show that $|A \cap B| \geq \lceil n + 2 \rceil/3$.
(b) For an integer $r \geq 3$, let $G = K_{r,r,r}$.
- 11. $m = \lceil n^2/4 \rceil + 2$.

### Section 19.2

- 13. Let $g=g(G)$. Consider the cases where $g$ is even or $g$ is odd.
- 15. Suppose that $H$ is an $(s,g)$-graph and assume, to the contrary, that $H$ is an $(s,g)$-cage. Since $H$ contains 4-cycles, either $g=3$ or $g=4$.
- 17. (a) $n(4,3,4)=5$. (b) $n(4,3,6)=8$.

## Chapter 20

### Section 20.1

- 1. (a) Consider $H=G \vee K_1$. (b) Consider $F = G + K_1$.
- 3. To show that $R(s,t') \le R(s,t)$, let $G$ be a graph of order $R(s,t)$. Then apply the definition of Ramsey number.
- 5. To show that $R(4,4) \le 18$, consider a red-blue coloring of $K_{18}$. Each vertex of $K_{18}$ is incident with nine edges of the same color.
- 7. $\min \{t_i \} = 2$.
- 9. No.

### Section 20.2

- 11. $R(F,H)=7$.
- 13. $R(K_3,C_5)=9$.
- 15. Consider the cases when $n$ is even and $n$ is odd. Apply Theorems 13.5 and 13.2.
- 17. (a) Yes. (b) Let $n=R_\chi(s-1,t)+R_\chi(s,t-1)$. Let there be given a red-blue coloring of the complete graph $K_n$. Show that $K_n$ contains a red subgraph with chromatic number at least $s$ or a blue subgraph with chromatic number at least $t$.
(c) $R_\chi(3,3)=5$. (d) For $3 \le s \le t$, $R_\chi(s,t) = 1 + (s-1)(t-1)$.
- 19. Let $n=R(K_{n_1},K_{n_2}, \dots, K_{n_r}, T_n)$. To show that $n \le 1 + (r-1)(s-1)$, apply Theorem 12.21. To show that $n \ge 1+(r-1)(s-1)$, exhibit an edge coloring of $K_{(r-1)(s-1)}$ with the colors $1,2, \dots,k+1$ such that for each $i$ with $1 \le i \le k$ there is no copy of $K_{n_i}$ all of whose edges are colored $i$ and there is no copy of $T_n$ all of whose edges are colored $k+1$.
- 21. (a) $R(K_1,3,K_3)=7$. (b) $MR(K_{1,3},K_3)=6$.
- 23. $MR(F,H)=6$.
- 25. $RR(K_{1,3},P_4)=5$.
- 27. $BR(P_4,P_4)=3$.

## Chapter 21

### Section 21.1

- 1. Follow the proof of Theorem 21.1.
- 3. Determine a bound on $\log_2 10$.
- 5. Consider the probability space $S$ whose elements are the $\binom{n}{2}$ different labeled tournaments $T$ with vertex set $V(T)=\{v_1,v_2,\dots,v_n\}$. The probabilities are defined by $P((v_i,v_j) \in E(T)) = P((v_j,v_i) \in E(T)) = \frac{1}{2}$ for each pair $v_i,v_j$ of distinct vertices of $T$ and these events are then mutually independent. Consider, for each $k$-element subset $U \subseteq \{v_1, v_2, \dots, v_n\}$, the probability of the event that no vertex in $V(G)-U$ is adjacent to every vertex of $U$.

### Section 21.2

- 7. Apply Theorem 21.7 to property $Q_{2.0}$.
- 9. Let $n$ be a positive integer such that $(n-3)(n-4)/12 > k$. By Theorem 21.9, almost all graphs contain $K_n$ as a subgraph. By Theorem 11.18, $\gamma(K_n) > k$. Therefore, almost all graphs have genus exceeding $k$ and consequently, almost no graphs have genus at most $k$.
- 11. Show that if $r(n)$ is a threshold function for some property, then so too is $2r(n)$. What about $cr(n)$ for any constant $c > 0$?
- 13. Consider the eccentricity sequence of a connected graph with diameter 2.

# Bibliography

- [1] B. M. Ábreço, S. Fernández-Merchant and G. Salazar, The rectilinear crossing number of $K_n$: Closing in (or are we?) *Thirty essays on geometric graph theory* 5-18, Springer, New York, 2013. [286]
- [2] Y. Alavi, A. J. Boals, G. Chartrand, P. Erdős and O. R. Oellermann, The ascending subgraph decomposition problem. *Congr. Numer.* **58** (1987) 7-14. [345]
- [3] N. Alon, Choice numbers of graphs; a probabilistic approach, *Comb. Prop. Comput.* **1** (1992) 107-114. [409]
- [4] B. Alspach, Research problems, Problem 3. *Discrete Math.* **36** (1981) 333. [349]
- [5] B. Alspach, The wonderful Walecki construction. *Bull. Inst. Combin. Appl.* **52** (2008) 7-20. [341]
- [6] B. Alspach and H. Gavlas, Cycle decompositions of $K_n$ and $K_n-I$. *J. Combin. Theory Ser B* **81** (2001) 77-99. [348, 350]
- [7] V. I. Arnautov, Estimation of the exterior stability number of a graph by means of the minimal degree of the vertices. (Russian) *Prik. Mat. i Programmivanie Vyp.* **11** (1974) 3-8. [325, 550]
- [8] I. Anderson, Perfect matchings of a graph. *J. Combin. Theory Ser. B* **10** (1971) 183-186. [311]
- [9] K. Appel and W. Haken, Every planar map is four colorable. *Bull. Amer. Math. Soc.* **82** (1976) 711-712. [427]
- [10] D. Archdeacon and P. Huneke, A Kuratowski theorem for nonorientable surfaces. *J. Combin. Theory Ser. B* **46** (1989) 173-231. [300]
- [11] A. T. Balaban, Trivalent graphs of girth nine and eleven, and relationships among cages. *Rev. Roumaine Math. Pures Appl.* **18** (1973) 1033-1043. [516]
