
(ii) $\lim_{n \to \infty} \frac{p(n)}{r(n)} = \infty$ implies that $\lim_{n \to \infty} P[G \in G(n, p(n))] \text{ has } Q] = 1$.

In other words, a function $r(n)$ is called a threshold function for $Q$ if

- (i) $\lim_{n \to \infty} \frac{p(n)}{r(n)} = 0$ implies that almost no graphs have property $Q$ and
- (ii) $\lim_{n \to \infty} \frac{p(n)}{r(n)} = \infty$ implies that almost all graphs have property $Q$.

Figure 21.2 indicates many well-known graph properties and corresponding threshold functions ([224, p. 17] and [149, 189]).

| Property | Threshold Functions |
| --- | --- |
| Contains a path of length $k$ | $r(n) = n^{-(k+1)/k}$ |
| Is not planar | $r(n) = 1/n$ |
| Is Hamiltonian | $r(n) = (\ln n)/n$ |
| Is connected | $r(n) = (\ln n)/n$ |
| Contains a copy of $K_k$ | $r(n) = n^{-2/(k-1)}$ |

Figure 21.2: Threshold functions

## Exercises for Chapter 21

### Section 21.1. The Probabilistic Method

- 1. Show that if $\binom{n}{2}2^{1-\binom{k}{2}} < 1$, then $R(t, t) > n$.
- 2. Prove Theorem 21.2 without using the probabilistic method.
- 3. We have seen that $\chi_{\ell}(K_{10,10}) \ge 4$. How does this compare to the upper bound given for $\chi_{\ell}(K_{10,10})$ by Theorem 21.2?
- 4. Show that if $\binom{n}{k}2^{\binom{k}{2}} + \binom{n}{n-k}2^{-\binom{k}{2}} < 1$, then $R(s, t) > n$.
- 5. A nontrivial tournament $T$ of order $n$ has *property* $U_k$ ($1 \le k \le n - 1$) if for every set $U$ of $k$ vertices of $T$, there is a vertex $w \notin U$ that is adjacent to every vertex of $U$. Show that if $\binom{n}{k}(1 - 2^{-k})^{n-k} < 1$, then there is a tournament $T$ of order $n$ with property $U_k$.

### Section 21.2. Random Graphs

- 6. (a) Show that $P[A \cap B] \ge 1 - (P[\overline{A}] + P[\overline{B}])$.
  - (b) Prove Theorem 21.8:
    Let $Q_1$ and $Q_2$ be *graphical properties*. If *almost all graphs have property* $Q_1$ *and almost all graphs have property* $Q_2$, *then almost all graphs have both properties* $Q_1$ *and* $Q_2$.
  - (c) Let $Q_1, Q_2, \dots, Q_k$, $k \ge 2$, be graphical properties. Prove that if *almost all graphs have property* $Q_i$ *for all* $i = 1, 2, \dots, k$, *then almost all graphs have all of these* $k$ *properties*.
- 7. Show that Theorem 21.6 is a corollary of Theorem 21.7.
- 8. Prove Corollary 21.11: *For each positive integer* $k$ *and each positive constant* $p < 1$, *almost no graphs are* $k$-*colorable*.
- 9. Prove Corollary 21.12: *For each positive integer* $k$ *and each positive constant* $p < 1$, *almost no graphs have genus at most* $k$.
- 10. Without using the fact that a threshold function for the property of containing a copy of $K_k$ is $n^{-2/(k-1)}$, show for every integer $k \ge 5$ that if
  $$\lim_{n \to \infty} \frac{p(n)}{n^{-2/(k-1)}} = 0, \text{ then almost no graph in } G(n, p(n)) \text{ contains a copy of } K_k.$$
- 11. Prove or disprove: If $r(n)$ is a threshold function for some property $Q$, then $r(n)$ is unique.
- 12. Let $T(n, \frac{1}{2})$ denote the probability space of the $\binom{n}{2}$ labeled tournaments $T$ of order $n$ with vertex set $V(T) = \{v_1, v_2, \dots, v_n\}$, where the probabilities are defined by setting $P[(v_i, v_j) \in E(T)] = P[(v_j, v_i) \in E(T)] = \frac{1}{2}$. In Exercise 5, a nontrivial tournament $T$ of order $n$ was said to have property $U_k$ ($1 \leq k \leq n-1$) if for every set $U$ of $k$ vertices of $T$, there is a vertex $w \notin U$ that is adjacent to every vertex of $U$. Show for a fixed positive integer $k$, that almost all tournaments have property $U_k$, that is, $\lim_{n \to \infty} P[T \in T(n, \frac{1}{2}) \text{ has } U_k] = 1$.
- 13. Show for a fixed positive real number $p < 1$ that almost all graphs have eccentricity sequence $2, 2, \dots, 2, 1, 1, \dots, 1$, where $i$ terms equal 2 and $n-i$ terms equal 1, for some integer $i$ with $2 \leq i \leq n$.

## Hints and Solutions to Odd-Numbered Exercises

### Chapter 1 Section 1.1

- 1. Let the vertices of the graph represent the boxes where two vertices are adjacent if the corresponding boxes contain a wire segment of the same color.

### Section 1.2

- 3. The degree of each remaining vertex is 3.

### Section 1.3

- 5. **Proof.** Let $G$ be a graph with $r$ vertices of degree $r$, $r+1$ vertices of degree $r+1$ and $r+2$ vertices of degree $r+2$. Thus, the order of $G$ is $3r+3$.
  First, we show that $r$ is odd. Assume, to the contrary, that $r$ is even. Then $G$ contains an odd number $2r+1$ of odd vertices, which is impossible. Thus, $r$ is odd and $G$ contains $2r+2$ vertices of odd degree.
  (a) $G_1\cong G_2$. (b) $H_1\not\cong H_2$.
- 9. (a) Apply the definition of isomorphism to $G[S]$ and $H[T]$.
  (b) Consider $r=3$.

### Section 1.4

- 11. Consider the average degree $2m/n$ of $G$.
- 13. Let $V(G)=\{u, v, w, x\}$ and $E(G)=\{uv, vw, wx, xu, vx\}$. Let $e=vx$.
  Then $G-e=C_4$ and $G-u=C_3$.
- 15. If $G$ is not $r$-regular, then let $G'$ be another copy of $G$ and join corresponding vertices whose degrees are less than $r$.
- 17. The Petersen graph.

### Section 1.5

- 19. $n=22$.
- 21. Let the partite sets of a 3-partite graph $G$ of order $n=3k$ and size $m$ be $A, B$ and $C$, where $|A|=a$, $|B|=b$ and $|C|=c$ and $a+b+c=3k$. We may assume that $a\geq b\geq c$ and let $a=k+x, c=k-y$ and $b=3k-a-c=k-x+y$.
  Then show that $m\leq ab+ac+bc\leq 3k^2-x^2+xy-y^2\leq 3k^2$.

### Section 1.6

- 23. Observe that if $G$ has a partite set with three or more vertices, then $\overline{G}$ is not bipartite.
- 25. Observe that $\overline{G}$ in (a) is $C_7$ or $C_3 + C_4$, while $\overline{G}$ in (b) is one of $C_9, C_6 + C_3, C_5 + C_4$ or $3C_3$.
- 27. Let $C = \langle v_1, v_2, v_3, v_4, v_5, v_6\rangle$, replace $v_1$ by a copy $H$ of $C_5$ and join every vertex of $H$ to every vertex of $\overline{H}$ if $v_i v_j$ is an edge of $C$.
- 29. Use induction and the hint given in Exercise 15.
- 31. Since there is a self-complementary graph of order $n$ for every integer $n$ with $n \equiv 0 \pmod{4}$ or $n \equiv 1 \pmod{4}$ by Exercise 29, we may assume that $n \equiv 2 \pmod{4}$ or $n \equiv 3 \pmod{4}$. Use induction on $n$.
- 33. (a) The degree of $u_1$ in $G_1 + G_2$ is $\deg_{G_1} u_1$.
  (b) The degree of $u_1$ in $G_1 \vee G_2$ is $\deg_{G_1} u_1 + n_2$.
  (c) The degree of $(u_1, u_2)$ in $G_1 \square G_2$ is $\deg_{G_1} u_1 + \deg_{G_2} u_2$.

### Section 1.7

- 35. $G - uv - xy + ux + wy$.

![](img/598a6ae3fd44120830ada34717906f29_576_0.png)

- 37. $G = P_4$.
- 39. Assume that for each graph $H$ with $V(H) = \{v_1, v_2, \dots, v_n\}$ where $\deg v_i = d_i$ for $1 \le i \le n$, there is a vertex $v_k$ ($1 \le k \le n$) such that both (1) and (2) fail.
- 41. (b), (c) and (e) are graphical.
- 43. If a graph $G$ of order 6 contains two vertices of degree 5, it has no vertex of degree 1.
- 45. Observe that $\sum_{i=1}^{3} d_i = 17$ and $3(3-1) + \sum_{i=4}^{7} \min\{3, d_i\} = 16$.
- 47. Let $S = \{a_1, a_2, \dots, a_n\}$ and $k = \text{lcm}(a_1+1, a_2+1, \dots, a_n+1)$. For $S = \{2, 6, 7\}, k = 4$.
- 49. In one direction, assume that $s_1$ and $s_2$ are bipgraphical sequences. Let $V_1 = \{u_1, u_2, \dots, u_r\}$ and $V_2 = \{w_1, w_2, \dots, w_t\}$. Suppose that there is no bipartite graph $H$ with partite sets $V_1$ and $V_2$ and a vertex $u$ of $H$ of degree $a_1$ in $V_1$ adjacent to vertices of degrees $b_1, b_2, \dots, b_{a_1}$.
- 51. (a) $rK_1 + (s/2)K_2$, (b) The minimum size is $s/2$.
  (c) The maximum size is $\binom{n}{2} - s/2$.

### Section 1.8

- 53. Only the sequence in (c) is a degree sequence of an irregular multigraph.
- 55. Each of the sequences in (a), (c), (e), (g) and (h) is the degree sequence of a multigraph.
- 57. (a) $m = 20$. (b) $9 \le m \le 11$.
  (c) Let $U = \{u_1, u_2, \dots, u_s\}$ and $W = \{w_1, w_2, \dots, w_t\}$ where $\deg u_1 \geq \deg u_2 \geq \cdots \geq \deg u_s$ and $\deg w_1 \geq \deg w_2 \geq \cdots \geq \deg w_t$. Then $m = \min\{\sum_{i=1}^{s} i \deg u_i, \sum_{i=1}^{t} i \deg w_i\}.$

### Chapter 2 Section 2.1

- 1. Let $G = K_{2,2}$ and let $u$ and $v$ be the two vertices of $G$ with $\deg u = \deg v = 3$.
- 3. (a) The statement is true. (b) The statement is false.
- 5. For $i \neq j$, the $(i,j)$-entry of $A^2$ is the number of different $v_i-v_j$ paths of length 2 and the $(i,j)$-entry of $A^3$ is the number of different $v_i-v_j$ walks of length 3. The vertices $v_1$ and $v_4$ belong to one triangle while the vertices $v_2$ and $v_3$ belong to two triangles.
- 7. $V(G) = \{v_1,v_2,v_3,v_4,v_5\}$ and $E(G) = \{v_1v_2,v_1v_3,v_2v_3,v_3v_4,v_4v_5\}.$
- 9. Let $P_{k+1}=(u_1,u_2, \dots, u_{k+1})$ be a path of order $k+1$ and let $G$ be the graph obtained from $P_{k+1}$ by adding $k$ new vertices $v_1,v_2, \dots, v_k$ and joining $v_i$ to $u_i$ and $u_{i+1}$ for $1 \leq i \leq k$.
- 11. Consider a longest path in $G$.
- 13. If $G$ contains a $u-v$ path and a $v-w$ path, then $G$ contains a $u-w$ path.
- 15. Suppose that the statement is false and consider $k$-longest path in $G$.
- 17. Let $V(G)=\{u=v_1,v_2, \dots,v_n=v\}$ and let $P_i$ be a $v_i-v_{i+1}$ path for $i=1,2, \dots,n-1$.
- 19. (a) Consider a path connecting two vertices of distinct degrees. (b) No.
- 21. Suppose that $G$ has $k$ or more components and consider a component of minimum order.
- 23. For every nonempty proper subset $S$ of $V(G)$, there is a vertex in $S$ adjacent to a vertex in $G-S$.

### Section 2.2

- 25. Observe that $d(u,v)+d(u,w)+d(v,w)=[d(u,v)+d(v,w)]+d(u,w)\geq 2d(u,w).$
- 27. $G = K_{n-1,1}.$
- 29. (a) $d(u,v) = \deg v$. (b) For $1 \leq k \leq n-1$, let $m_k$ denote the number of pairs $u,v$ of vertices of $G$ such that $d(u,v) = k$. Then $\sum_{v\in V(G)}d_k(v)=2m_k$. (c) $n^{\circ} - n$.
- 31. Let $G$ be obtained by identifying an end-vertex of $P_{n-1}$ with a vertex of $C_{2n}$.
- 33. For $n \geq 4$, let $e_1,e_2$ and $e_3$ be the edges of a triangle in $K_n$. Let $F = K_n-e_1-e_2$ and $G = K_n-e_1-e_2-e_3$.
- 35. Let $H = K_{2,k}$ where the partite sets of $H$ are $U = \{u_1,u_2\}$ and $W = \{w_1,w_2, \dots, w_k\}$ and let $G$ be the graph obtained from $H$ by adding two vertices $v_1$ and $v_2$ and the two edges $u_1v_1$ and $u_2v_2$. Then $\deg w_i = e(w_i) = 2$ for $i=1,2, \dots,k$.
- 37. $n = 2+ (r-1)\sum_{i=1}^{s-1}(r-2)^i$.
