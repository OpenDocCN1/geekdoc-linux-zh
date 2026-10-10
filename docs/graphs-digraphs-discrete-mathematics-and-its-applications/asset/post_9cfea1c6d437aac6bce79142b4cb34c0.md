
## 15.3. LIST COLORINGS

![](img/598a6ae3fd44120830ada34717906f29_421_0.png)

Figure 15.10: The graph $K_{3,3}$ is 3-choosable

**Proof.** Assume, to the contrary, that $\chi_l(K_{r,r}) \leq k$. Then $K_{r,r}$ is $k$-choosable. Let $U$ and $W$ be the partite sets of $K_{r,r}$, where
$U = \{u_1, u_2, \ldots, u_r\}$ and $W = \{w_1, w_2, \ldots, w_r\}$.
Let $S = \{1, 2, \ldots, 2k - 1\}$. There are $\binom{2k-1}{k}$ distinct $k$-element subsets of $S$. Assign these color lists to $\binom{2k-1}{k}$ vertices of $U$ and to $\binom{2k-1}{k}$ vertices of $W$. Any remaining vertices of $U$ and $W$ are assigned any of the $k$-element subsets of $S$. For $i = 1, 2, \ldots, r$, choose a color $a_i \in L(u_i)$ and let $T = \{a_i: \, 1 \leq i \leq r\}$. We consider two cases.

*Case 1.* $|T| \leq k-1$. Then there exists a $k$-element subset $S'$ of $S$ that is disjoint from $T$. However, $L(w_j) = S'$ for some $j$ with $1 \leq j \leq r$. This is a contradiction.

*Case 2.* $|T| \geq k$. Hence, there exists a $k$-element subset $T'$ of $T$. Thus, $L(w_j) = T'$ for some $j$ with $1 \leq j \leq r$. Whichever color from $L(w_j)$ is assigned for $w_j$, this color has been assigned to some vertex $u_i$. Thus, $u_i$ and $w_j$ have been assigned the same color and $u_iw_j$ is an edge of $K_{r,r}$. This is a contradiction. $\blacksquare$

For positive integers $r$ and $k$ such that $r \geq \binom{2k-1}{k}$, Theorem 15.18 provides a lower bound on $\chi_l(K_{r,r})$ for $r$ sufficiently large with respect to $k$. The following 1992 result of Noga Alon [3] gives an upper bound for $\chi_l(K_{r,r})$ for all $r \geq 3$.

**Theorem 15.19** For every integer $r \geq 3$,
$\chi_l(K_{r,r}) \leq \left\lceil 2 \log_2 r \right\rceil$.

Theorem 15.19 will be discussed again in Chapter 21 where a proof will be given.

## Exercises for Chapter 15

### Section 15.1. Perfect Graphs

- 1. Determine $G$ if, in the proof of Theorem 15.1,
    - (a) $H=K_{2}$;  (b) $H=C_{5}$.
- 2. Show, for every two integers $\ell$ and $k$ with $2 \leq \ell \leq k$, that there exists a graph $G$ with $\omega(G)=\ell$ and $\chi(G)=k$.
- 3. Prove or disprove: For every integer $k \geq 3$, there exists a triangle-free, $k$-critical graph.
- 4. Give an example of a regular triangle-free 4-chromatic graph.
- 5. Show that the graph of the octahedron (which is the graph $K_{2,2,2}$) is perfect.
- 6. Let $n \geq 2$ be an integer. Prove that every $(n-1)$-chromatic graph of order $n$ has clique number $n-1$.
- 7. Prove or disprove the following:
    - (a) If $G$ is a graph of order $n \geq 3$ with $\chi(G)=n-2$, then $\omega(G)=n-2$.
    - (b) If $G$ is a graph of sufficiently large order $n$ with $\chi(G)=n-2$, then $\omega(G)=n-2$.
- 8. Prove that a critically $k$-chromatic graph $G$ is perfect if and only if $G=K_{k}$.
- 9. Let $\mathcal{A}$ be a set and let $\mathcal{S}$ be a collection of nonempty subsets of $\mathcal{A}$. The **intersection graph** of $\mathcal{S}$ is that graph whose vertices are the elements of $\mathcal{S}$ and where two vertices are adjacent if the subsets have a nonempty intersection.
    - (a) Prove that every graph is an intersection graph.
    - (b) Let $G$ be a nonempty graph. Show that a set $\mathcal{F}$ can be associated with $G$ so that the intersection graph of $\mathcal{F}$ is the line graph of $G$.
- 10. For the graph $G=K_{4}-e$, determine the smallest positive integer $k$ for which there is a collection $\mathcal{S}$ of subsets of $\mathcal{A}=\{1, 2, \dots, k\}$ such that the intersection graph (see the definition in Exercise 9) of $\mathcal{S}$ is isomorphic to $G$.
- 11. Show that every induced subgraph of an interval graph is an interval graph.
- 12. Determine which connected graphs of order 4 are interval graphs.
- 13. (a) For the four open intervals $I_1 = (0, 1)$, $I_2 = (1, 2)$, $I_3 = (2, 3)$, $I_4 = (3, 4)$ of length 1 and the five open intervals
    $J_1 = (0, \frac{4}{3})$, $J_2 = (\frac{4}{3}, \frac{11}{3})$, $J_3 = (\frac{11}{3}, \frac{20}{3})$,
    $J_4 = (\frac{20}{3}, \frac{31}{3})$, $J_5 = (\frac{31}{3}, 4)$
    of length $\frac{4}{3}$, let $S = \{I_i:\ 1 \leq i \leq 4\} \cup \{J_j:\ 1 \leq j \leq 5\}$. Draw the
    interval graph $G$ with $V(G) = S$ and determine the size of $G$.
    - (b) Repeat the problem in part (a) for the open intervals $I_1 = (0, 1)$, $I_2 = (1, 2)$, $I_3 = (2, 3)$ and the open intervals $J_j = (\frac{4}{3}(j-1), \frac{4}{3}j)$ for $j = 1, 2, \ldots, 5$.
    - (c) Repeat the problem in part (a) for the open intervals $I_1 = (0, 1)$, $I_2 = (1, 2)$, $I_3 = (2, 3)$, $I_4 = (3, 4)$ and the open intervals $J_j = (\frac{4}{3}(j-1), \frac{4}{3}j)$ for $j = 1, 2, \ldots, 6$.
- 14. Let $a$ and $b$ be integers with $2 \leq a < b$. For $i = 1, 2, \ldots, a$, let $I_i = (i-1, i)$ and for $j = 1, 2, \ldots, b$, let $J_j = (\frac{a}{b}(j-1), \frac{a}{b}j)$. Let $G$ be the interval graph with $V(G) = S$.
    - (a) Show that $G$ is acyclic.
    - (b) Determine the size of $G$.
- 15. (a) Determine the interval graph $G$ with vertex set $S = \{I_1, I_2, \ldots, I_5\}$ consisting of the five closed intervals $I_1 = [1, 7]$, $I_2 = [6, 8]$, $I_3 = [6, 9]$, $I_4 = [7, 20]$ and $I_5 = [20, 22]$.
    - (b) Show that the same graph $G$ can be obtained from a set $T = \{J_1, J_2, \ldots, J_5\}$ of five open intervals where $I_i \subseteq J_i$ for $i = 1, 2, \ldots, 5$.
- 16. Show, for every integer $k \geq 3$, that there exists a $k$-chromatic graph that is not chordal.
- 17. Prove that every interval graph is a chordal graph.
- 18. Give an example of a chordal graph that is not an interval graph.

### Section 15.2. **The Perfect and Strong Perfect Graph Theorems**

- 19. For each integer $n \geq 7$, give an example of a graph $G_n$ of order $n$ such that no induced subgraph of $G_n$ is an odd cycle of length at least 5 but $G_n$ is not perfect.
- 20. Let $G = C_{2k+1}$ for some integer $k \geq 2$. Show that $\overline{G}$ is not perfect by determining $\chi(\overline{G})$ and $\omega(\overline{G})$.
- 21. Determine whether $\overline{G_S}$ is perfect.
- 22. Let $\mathcal{G}$ be the set of all connected graphs of order 25, say $\mathcal{G} = \{G_1, G_2, \ldots, G_k\}$, and let $G = G_1 + G_2 + \cdots + G_k$ be the union of these graphs. Prove or disprove the following:
    - (a) For the graph $G$, $\chi(G)=\omega(G)$.
    - (b) The graph $G$ is perfect.
- 23. Let $G$ be a graph where $v \in V(G)$.  According to Theorem 15.9, if $G$ is perfect, then the replication graph $R_v(G)$ is perfect.  Is the converse true?
- 24.  A **transitive orientation** of a graph $G$ is an orientation $D$ of $G$ such that whenever $(u, v)$ and $(v, w)$ are arcs of $D$, then so too is $(u, w)$.  If $G$ has a transitive orientation, then $G$ is called a **comparability graph**.
    - (a) Show that every bipartite graph is a comparability graph.
    - (b) Show that every complete graph is a comparability graph.
    - (c) Show that every comparability graph is perfect.
    - (d) Use (a)-(c) to show that every bipartite graph and every complete graph is perfect.
    - (e) Give an example of a comparability graph that is neither complete nor bipartite.
- 25. Let $G$ be a graph with $V(G)=\left\{v_1, v_2, \ldots, v_n\right\}$.  The **shadow graph** $\operatorname{Shad}(G)$ of $G$ is that graph with vertex set $V(G) \cup\left\{u_1, u_2, \ldots, u_n\right\}$, where $u_i$ is called the **shadow vertex** of $v_i$ and where $u_i$ is adjacent to both $u_j$ and $v_j$ if $v_i$ is adjacent to $v_j$ for $1 \leq i, j \leq n$.  How are $\omega(G)$ and $\omega(\operatorname{Shad}(G))$ related and how are $\chi(G)$ and $\chi(\operatorname{Shad}(G))$ related?
- 26.
    - (a) Show that if $G$ is perfect, then $|V(H)| \leq \alpha(H) \cdot \omega(H)$ for every induced subgraph $H$ of $G$ (see Theorem 15.11).
    - (b) Use Theorem 15.11 to prove the Perfect Graph Theorem (Theorem 15.10).

### Section 15.3.  List Colorings

- 27. Use the greedy coloring algorithm to show that $\chi_{\ell}(G) \leq 1+\Delta(G)$ for every graph $G$.
- 28. Prove, without using Exercise 27, that every odd cycle is 3-choosable.
- 29. Prove that $\chi_{\ell}\left(K_{2,3}\right)=2$.
- 30. Prove that $\chi_{\ell}\left(K_{2,4}\right)=3$.
- 31. Prove that $\chi_{\ell}\left(K_{3,27}\right)>3$.
- 32. We have seen that $\chi_{\ell}\left(K_{3,3}\right)=3$.  By Theorem 15.18, $\chi_{\ell}\left(K_{10,10}\right)>3$.  Give a precise and detailed proof of this special case of Theorem 15.18.
- 33. Prove that the list-chromatic number of $P_n \square K_2$ is 3 for every integer $n \geq 4$.
