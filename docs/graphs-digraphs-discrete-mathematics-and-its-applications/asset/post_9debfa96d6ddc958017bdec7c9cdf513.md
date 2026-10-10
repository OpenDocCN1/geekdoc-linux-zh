
occasions, I too; but *nolens volens* the idea occurred to me that this loss of time could have been minimized if the number of crossings of the rails had been minimized. But what is the minimum number of crossings? I realized after several days that the actual situation could have been improved, but the exact solution of the general problem with $s$ kernels and $t$ storage yards seemed to be very difficult . . . the problem occurred to me again . . . at my first visit to Poland where I met Zarankiewicz. I mentioned to him my ‘brick-factory’-problem . . . and Zarankiewicz thought to have solved (it). But Ringel found a gap in his published proof, which nobody has been able to fill so far – in spite of much effort. This problem has also become a notoriously difficult unsolved problem . . .

## Crossing Numbers of Complete Bipartite Graphs

Kazimierz Zarankiewicz [262] thought he had proved that

$$ \operatorname{cr}(K_{s,t}) = \left\lfloor \frac{s}{2} \right\rfloor \left\lfloor \frac{s-1}{2} \right\rfloor \left\lfloor \frac{t}{2} \right\rfloor \left\lfloor \frac{t-1}{2} \right\rfloor \tag{11.4} $$

but, in actuality, he had only verified that the right-hand expression of (11.4) is an upper bound for $\operatorname{cr}(K_{s,t})$. As it turned out, both Paul C. Kainen and Gerhard Ringel found flaws in Zarankiewicz’s argument. Hence, (11.4) remains only a conjecture. The best general result on crossing numbers of complete bipartite graphs is the following, due to the combined work of Daniel Kleitman [144] and Douglas Woodall [260].

**Theorem 11.4** *If* $s$ *and* $t$ *are positive integers with* $s \leq t$ *and either* (1) $s \leq 6$ *or* (2) $s = 7$ *and* $t \leq 10$, *then*

$$ \operatorname{cr}(K_{s,t}) = \left\lfloor \frac{s}{2} \right\rfloor \left\lfloor \frac{s-1}{2} \right\rfloor \left\lfloor \frac{t}{2} \right\rfloor \left\lfloor \frac{t-1}{2} \right\rfloor \text{.} $$

It follows, therefore, from Theorem 11.4 that

$$ \operatorname{cr}(K_{3,t}) = \left\lfloor \frac{t}{2} \right\rfloor \left\lfloor \frac{t-1}{2} \right\rfloor \text{,} \quad \quad \operatorname{cr}(K_{4,t}) = 2 \left\lfloor \frac{t}{2} \right\rfloor \left\lfloor \frac{t-1}{2} \right\rfloor \text{,} $$

$$ \operatorname{cr}(K_{5,t}) = 4 \left\lfloor \frac{t}{2} \right\rfloor \left\lfloor \frac{t-1}{2} \right\rfloor \text{ and } \operatorname{cr}(K_{6,t}) = 6 \left\lfloor \frac{t}{2} \right\rfloor \left\lfloor \frac{t-1}{2} \right\rfloor $$

for all $t$. For example, $\operatorname{cr}(K_{3,3}) = 1$, $\operatorname{cr}(K_{4,4}) = 4$, $\operatorname{cr}(K_{5,5}) = 16$, $\operatorname{cr}(K_{6,6}) = 36$ and $\operatorname{cr}(K_{7,7}) = 81$. A drawing of $K_{4,4}$ with four crossings is shown in Figure 11.3.

![](img/598a6ae3fd44120830ada34717906f29_292_0.png)

Figure 11.3: A drawing of $K_{4,4}$ with four crossings

As would be expected, the situation regarding crossing numbers of complete $k$-partite graphs, $k \geq 3$, is even more complicated. For the most part, only bounds and highly specific results have been obtained in these cases. On the other hand, some of the proof techniques employed have been enlightening. As an example, the following result of Arthur T. White [254, p. 67] establishes the crossing number of $K_{2,2,3}$.

**Theorem 11.5** The crossing number of $K_{2,2,3}$ is 2.

**Proof.** The graph $K_{2,2,3}$ has order 7 and size 16. Suppose that $\mathrm{cr}(K_{2,2,3}) = c$. Since $K_{3,3}$ is nonplanar and $K_{3,3} \subseteq K_{2,2,3}$, it follows that $K_{2,2,3}$ is nonplanar and so $c \geq 1$. Let there be given a drawing of $K_{2,2,3}$ in the plane with $c$ crossings. At each crossing we introduce a new vertex, producing a connected plane graph $G$ of order $n = 7 + c$ and size $m = 16 + 2c$. By Theorem 10.3, $m \leq 3n - 6$.

Let $u_1u_2$ and $v_1v_2$ be two (nonadjacent) edges of $K_{2,2,3}$ that cross in the given drawing, giving rise to a new vertex. If $G$ is a maximal planar graph, then $C = \langle u_1, v_1, u_2, v_2, u_1 \rangle$ is a cycle of $G$, implying that the subgraph induced by $\{u_1, u_2, v_1, v_2\}$ in $K_{2,2,3}$ is $K_4$. However, $K_{2,2,3}$ contains no such subgraph; thus, $G$ is not a maximal planar graph and so $m < 3n - 6$. Therefore,

$$ 16 + 2c < 3(7 + c) - 6, $$

from which it follows that $c \geq 2$. The inequality $c \leq 2$ follows from the fact that there exists a drawing of $K_{2,2,3}$ with two crossings (see Figure 11.4).

![](img/598a6ae3fd44120830ada34717906f29_292_1.png)

Figure 11.4: A drawing of $K_{2,2,3}$ with two crossings

## Crossing Numbers of Cartesian Products of Graphs

Other graphs whose crossing numbers have been investigated with little success are the $n$-cubes $Q_n$. Since $Q_n$ is planar for $n = 1, 2, 3$, $\operatorname{cr}(Q_n) = 0$ for each such $n$. Roger Eggleton and Richard Guy [76] have shown that $\operatorname{cr}(Q_4) = 8$ but $\operatorname{cr}(Q_n)$ is unknown for $n \geq 5$. One might observe that

$$ Q_4 = K_2 \square K_2 \square K_2 \square K_2 = C_4 \square C_4 $$

so that $\operatorname{cr}(C_4 \square C_4) = 8$. This raises the question of determining $\operatorname{cr}(C_s \square C_t)$ for $s, t \geq 3$. For the case $s = t = 3$, Frank Harary, Paul Kainen and Allen Schwenk [120] showed that $\operatorname{cr}(C_3 \square C_3) = 3$. Their proof consisted of the following three steps:

- **Step 1.** Exhibiting a drawing of $C_3 \square C_3$ with three crossings so that $\operatorname{cr}(C_3 \square C_3) \leq 3$.
- **Step 2.** Showing that $C_3 \square C_3 - e$ is nonplanar for every edge $e$ of $C_3 \square C_3$ so that $\operatorname{cr}(C_3 \square C_3) \geq 2$.
- **Step 3.** Showing, by case exhaustion, that it is impossible to have a drawing of $C_3 \square C_3$ with exactly two crossings so that $\operatorname{cr}(C_3 \square C_3) \geq 3$ (see Exercise 6).

Richard D. Ringeisen and Lowell W. Beineke [200] then significantly extended this result by determining $\operatorname{cr}(C_3 \square C_t)$ for all integers $t \geq 3$.

**Theorem 11.6** For each integer $t \geq 3$, $\operatorname{cr}(C_3 \square C_t) = t$.

**Proof.** We label the vertices of $C_3 \square C_t$ by the $3t$ ordered pairs $(0,j)$, $(1,j)$ and $(2,j)$, where $j = 0,1,\dots,t - 1$, and, for convenience, we let

$$ u_j = (0,j), \quad v_j = (1,j) \text{ and } w_j = (2,j). $$

First, we note that $\operatorname{cr}(C_3 \square C_t) \leq t$. This observation follows from the fact that there exists a drawing of $C_3 \square C_t$ with $t$ crossings. A drawing of $C_3 \square C_4$ with four crossings is shown in Figure 11.5. Drawings of $C_3 \square C_t$ with $t$ crossings for other values of $t$ can be given similarly.

![](img/598a6ae3fd44120830ada34717906f29_294_0.png)

Figure 11.5: A drawing of $C_3 \square C_4$ with four crossings

*Case 1. No edge of any triangle $T_j = G[\{u_j, v_j, w_j\}]$, $j = 0, 1, \dots, k$, is crossed.* For $j = 0, 1, \dots, k$, define

$$ H_j = G[\{u_j, w_j, w_{j+1}, u_{j+1}, v_{j+1}, w_{j+1}\}], $$

where the subscripts are expressed modulo $k + 1$. We show that for each $j = 0, 1, \dots, k$, the number of times edges of $H_j$ are crossed totals at least 2. Since, by assumption, no triangle $T_j$ has an edge crossed and since every edge not in any triangle $T_j$ belongs to exactly one subgraph $H_j$, it will follow that there are at least $k + 1$ crossings in the drawing because each crossing of an edge in $H_j$ involves either two edges of $H_j$ or an edge of $H_j$ and an edge of $H_i$ for some $i \neq j$.

If two of the edges $u_jw_{j+1}$, $v_jv_{j+1}$ and $w_jw_{j+1}$ cross each other, then two edges of $H_j$ are crossed. Assume then that no two edges of $H_j$ cross each other. Thus, $H_j$ is a plane subgraph in the drawing of $C_3 \square C_{k+1}$ (see Figure 11.6). The triangle $T_{j+2}$ must lie within some region of $H_j$. If $T_{j+2}$ lies in a region of $H_j$ bounded by a triangle, say $T_i$, then at least one edge of the cycle $(u_0, w_1, \dots, u_k, w_0)$, for example, must cross an edge of $T_j$, contradicting our assumption. Thus, $T_{j+2}$ must lie in a region of $H_j$ bounded by a 4-cycle, say $(u_j, w_{j+1}, w_j, u_j)$. However then, edges of the cycle $(v_0, v_1, \dots, v_k, v_0)$ must cross edges of the cycle $(u_j, w_{j+1}, w_j, u_j)$ at least twice and, hence, edges of $H_j$ at least twice, as asserted.

*Case 2. Some triangle, say $T_0$, has at least one of its edges crossed.* Suppose that $\mathrm{cr}(C_3 \square C_{k+1}) < k + 1$. Then the graph $C_3 \square C_{k+1} - E(T_0)$, which is a subdivision of $C_3 \square C_k$, is drawn with fewer than $k$ crossings, contradicting the inductive hypothesis.

The only other result giving the crossing number of graphs $C_s \square C_t$ is the following theorem of Beineke and Ringeisen [19].
