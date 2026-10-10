
## Graceful Labeling

This is a graceful labeling of $C_{n}$. An illustration is given in Figure 13.17(b) for $n = 11.$

![](img/598a6ae3fd44120830ada34717906f29_368_0.png)

If $G$ is a graceful graph of order $n$ and size $m$, then, of course, the vertices of $G$ can be labeled with the elements of a set $\{a_{1}, a_{2}, \dots, a_{n}\} \subseteq \{0, 1, \dots, m\}$ so that the induced edge labels are precisely $1, 2, \dots, m.$ This means one vertex in some pairs of adjacent vertices is labeled 0 and the other vertex in the pair is labeled $m.$ Also, if we were to replace each vertex label $a_{i}$ by $m - a_{i}$, then we have a new graceful labeling, called the **complementary labeling** of $G.$

We saw in Figure 13.13 that the complete graphs $K_{3}$ and $K_{4}$ are graceful. It is very easy to show that $K_{2}$ is graceful. The following result of Golomb [106] shows that there are no other graceful complete graphs.

### Theorem 13.22
The complete graph $K_{n}$ $(n \geq 2)$ is graceful if and only if $n \leq 4.$

**Proof.** We have already observed that $K_{n}$ is graceful if $2 \leq n \leq 4.$ Assume then that $n \geq 5$ and suppose, to the contrary, that $K_{n}$ is graceful. Hence, there exists a graceful labeling of the vertices of $K_{n}$ from an $n$-element subset of $\{0, 1, \dots, m\}$, where $m = \binom{n}{2}.$

We have already seen that every graceful labeling of a graph of size $m$ requires 0 and $m$ to be vertex labels. Since some edge of $K_{n}$ must be labeled $m - 1,$ some vertex of $K_{n}$ must be labeled 1 or $m - 1.$ We may assume, without loss of generality, that a vertex of $K_{n}$ is labeled 1; otherwise, we may use the complementary labeling.

To produce an edge labeled $m - 2,$ we must have adjacent vertices labeled $0, m - 2$ or $1, m - 1$ or $2, m.$ If a vertex is labeled $2$ or $m - 1,$ then we have two edges labeled 1, which is impossible. Thus, some vertex of $K_n$ must be labeled $m-2$.

Since we now have vertices labeled 0, 1, $m-2$ and $m$, we have edges labeled 1, 2, $m-3$, $m-2$, $m-1$ and $m$. To have an edge labeled $m-4$, we must have a vertex labeled 4 because all other choices result in two edges with the same label.

Now we have vertices labeled 0, 1, 4, $m-2$ and $m$, which results in edges labeled 1, 2, 3, 4, $m-6$, $m-4$, $m-2$, $m-1$ and $m$. However, it is quickly seen that there is no vertex label that will produce the edge label $m-5$ without also producing a duplicate edge label. Hence, no graceful labeling of $K_n$ exists.

Unlike the classes of graphs we have considered, where some graphs are graceful and others are not, every complete bipartite graph is graceful.

### Theorem 13.23
Every complete bipartite graph is graceful.

**Proof.** Let $K_{s,t}$ have partite sets $U$ and $W$, where $|U| = s$ and $|W| = t$. Label the vertices of $U$ by 0, 1, ..., $s-1$ and label the vertices of $W$ by $s$, $2s$, ..., $(t-1)s$, $ts$ (see Figure 13.18). This is a graceful labeling.

![](img/598a6ae3fd44120830ada34717906f29_369_0.png)

## Exercises for Chapter 13

### Section 13.1. Factorization

- 1. Show that the Petersen graph is not 1-factorable.
- 2. Give an example of a connected graph $G$ of composite size having the property that whenever $F$ is a factor of $G$ and the size of $F$ divides the size of $G$, then $G$ is $F$-factorable.
- 3. (a) Prove that $Q_n$ is 1-factorable for all $n \geq 1$.
    (b) Prove that $Q_n$ is $k$-factorable if and only if $k \mid n$.
- 4. It was shown (following Theorem 13.3) that the bound on $r$ in the 1-Factorization Theorem cannot be improved when $n \equiv 2 \pmod{4}$ by observing that the graph $G = 2K_{n/2}$ contains no 1-factor and is therefore not 1-factorable. Show that if $n \geq 10$ and $n \equiv 2 \pmod{4}$, then a 2-connected $r$-regular graph $G$ of order $n$, where $r = \frac{n}{2} - 1$, need not be 1-factorable.
- 5. Show for even integers $n \geq 8$ with $n \equiv 0 \pmod{4}$ that the bound on $r$ in the 1-Factorization Theorem cannot be improved.
- 6. Use the proof of Theorem 13.4 to give a 2-factorization of the 4-regular graph $C_8^2$ (the square of the 8-cycle $C_8$).
- 7. Use the proof of Theorem 13.5 to produce a Hamiltonian factorization of $K_9$.
- 8. Use Theorems 13.2 and 13.5 to prove the following: Let $r$ and $n$ be integers with $0 \leq r \leq n-1$. Then there exists an $r$-regular graph of order $n$ if and only if $r$ and $n$ are not both odd.
- 9. Let $k$ be a nonnegative even integer and $n \geq 5$ an odd integer with $k \leq n-3$. Prove that there exists a graph $G$ of order $n$, all of whose vertices have degree $k$ or $k+2$.
- 10. Prove Corollary 13.6: *For each positive integer $k$, the complete graph $K_{2k}$ can be factored into $k$ Hamiltonian paths*.
- 11. Show that $K_{2k+1}$ cannot be factored into Hamiltonian paths.
- 12. Give a constructive proof of Theorem 13.7: *For each positive integer $k$, the graph $K_{2k}$ can be factored into a $k-1$ Hamiltonian cycles and a 1-factor*.
- 13. Show for every positive integer $a$ and odd positive integer $b$ that there exists a factorization of $K_{2a+b+1}$ into $a$ Hamiltonian cycles and $b$ 1-factors.
- 14. Show for every positive integer $k$ that the complete graph $K_{6k+4}$ is 3-factorable, where each 3-factor is Hamiltonian.
- 15. By Theorem 13.4 (and Exercise 6) the 4-regular graph $C_8^2$ is 2-factorable. Show that $C_8^2$ is, in fact, Hamiltonian factorable.
- 16. By Dirac’s theorem (Corollary 6.2), every 4-regular graph of order 8 is Hamiltonian. Suppose that a 4-regular graph $G$ of order 8 has a Hamiltonian cycle $C$ with the property that $H = G - E(C) = C_3 + C_5$. Show that $G$ is Hamiltonian factorable.
- 17. Theorem 13.10 is an improvement of Dirac’s theorem (Corollary 6.2) for sufficiently large integers $n$. Show that there is no equivalent improvement of Ore’s theorem (Theorem 6.1) by describing an infinite family of graphs $G$ of order $n$ with $\sigma_2(G) \geq n$ such that $G$ does not contain $(n-2)/8$ edge-disjoint Hamiltonian cycles.
- 18. Let $\{A, B\}$ be a partition of the vertex set of a graph $G$ of order $n = 8k+2 \geq 10$ where $|A| = 4k$ and $|B| = 4k + 2$. The edge set of $G$ is defined by $G[A] = \overline{K_{4k}}, G[B] = (2k + 1)K_2$ and all possible edges joining a vertex of $A$ and a vertex of $B$.
    - (a) Show that $G$ is Hamiltonian.
    - (b) Show that $G$ contains at most $\lfloor |B|/4 \rfloor = k = (n-2)/8$ edge-disjoint Hamiltonian cycles.

### Section 13.2: Decomposition

- 19. Show that there is a cyclic $P_3$-decomposition of the graph of the octahedron (see Figure 13.7).
- 20. Show that the graph of the octahedron (see Figure 13.7) is not $K_{1,4}$-decomposable.
- 21. Prove that there exists a Steiner triple system of order $n \geq 3$, then either $n \equiv 1 (\text{mod } 6)$ or $n \equiv 3 (\text{mod } 6)$.
- 22. Prove that nine schoolgirls can take four daily walks in three rows of three girls each so that no two girls walk in the same row twice.
- 23. For each odd integer $n \geq 5$, show that there is an ascending subgraph decomposition of $K_n$ for which
    - (a) each subgraph in the decomposition is a star;
    - (b) each subgraph in the decomposition is a path.
- 24. Show that there is an ascending subgraph decomposition of $4P_8$ such that each subgraph in the decomposition is 1-regular.
- 25. Give an example of an ascending subgraph decomposition of $K_{3,7}$ for which each subgraph in the decomposition is connected.
- 26. Give an example of an ascending subgraph decomposition of $K_6 + K_4$.

### Section 13.3. Cycle Decomposition

- 27. Figure 13.10 shows a $C_6$-decomposition of $K_9$. Display a $C_k$-decomposition of $K_9$ for all other possible values of $k$.
- 28. Give a cycle decomposition of $K_7$ such that the decomposition contains a maximum number of cycles of distinct lengths.
- 29. The graph $G$ of Figure 13.19 is an Eulerian graph of order 12 and size 30. Give an example of a cycle decomposition $\mathcal{D}_k$ of $G$ containing exactly $k$ odd cycles for every possible value of $k$.

![](img/598a6ae3fd44120830ada34717906f29_372_0.png)

Figure 13.19: The graph in Exercise 29

- 30. Give an example of a cycle decomposition of $K_7$ such that each cycle in the decomposition is one of two lengths and that the number of cycles of each length is the same.
- 31. Let $G$ be a connected graph with $2k \ge 2$ odd vertices for some positive integer $k$. According to Theorem 5.3, there is a decomposition of $G$ into $k$ open trails, at most one of which has odd length.
    - (a) Give an example of a connected graph $G$ of even size with $2k \ge 2$ odd vertices such that for every decomposition of $G$ into $k$ open trails, the trails have even length.
    - (b) Give an example of a connected graph $G$ of even size with $2k \ge 2$ odd vertices such that for every even integer $t$ with $0 \le t \le k$, there is a decomposition of $G$ into $k$ open trails, exactly $t$ of which are of odd length.
