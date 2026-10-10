
![](img/598a6ae3fd44120830ada34717906f29_545_0.png)

For two graphs $F$ and $H$, the **Ramsey number** $R(F, H)$ is the minimum order $n$ of a complete graph such that for every red-blue coloring of $K_n$, there is either a subgraph isomorphic to $F$, all of whose edges are colored red (a red $F$), or a subgraph isomorphic to $H$, all of whose edges are colored blue (a blue $H$). The Ramsey number $R(F, H)$ exists for every two graphs $F$ and $H$. In fact, if $F$ has order $s$ and $H$ has order $t$, then
$$R(F, H) \leq R(s, t) .$$
To illustrate a Ramsey number of this type, we determine the Ramsey number $R(P_4, K_4)$.

+ Example 20.10 $R(P_4, K_4) = 10$.

Proof. To show that $R(P_4, K_4) \geq 10$, consider the red-blue coloring of $K_9$ in which the red subgraph is $3K_3$. Since the order of every component of $3K_3$ is 3, there is no red $P_4$ in this red-blue coloring of $K_9$. The blue subgraph in this case is $K_{3,3,3}$, which does not contain a 4-clique. Hence, there is also no blue $K_4$ in this red-blue coloring of $K_9$. Therefore, $R(P_4, K_4) \geq 10$.

We now show that $R(P_4, K_4) \leq 10$. Let there be given a red-blue coloring of $G = K_{10}$. We show that there is either a red $P_4$ or a blue $K_4$. Suppose first that some vertex $v$ of $G$ is incident with four or more red edges, say $v u_{1}, v u_{2}, v u_{3}$ and $v u_{4}$ are red. If any edge joining two vertices of $S=\left\{u_{1}, u_{2}, u_{3}, u_{4}\right\}$ is red, then a red $K_{4}$ results; otherwise, $G[S]=K_{4}$ is blue.

Hence, we may assume that every vertex of $G$ is incident with six or more blue edges. Let $u \in V(G)$ and suppose that $u u_{1}, u u_{2}, \ldots, u u_{6}$ are blue edges of $G$. Let $A=\left\{u_{1}, u_{2}, \ldots, u_{6}\right\}$ and let $H=\left\{G[A]\right\}=K_{6}$. Since $R(3,3)=6$ by Theorem 20.3, it follows that $H$ contains either a red $K_{3}$ or a blue $K_{3}$. Since $u$ is joined to every vertex of $H$ by a blue edge, if $H$ contains a blue $K_{3}$, then $G$ contains a blue $K_{4}$. Hence, we may assume that $H$ contains a red $K_{3}$, which we denote by $F_{1}$. If some vertex of $F_{1}$ is joined to a vertex of $V(G)-V\left(F_{1}\right)$ by a red edge, then a red $F_{4}$ results. Thus, we may assume that $G$ contains a blue $K_{3,7}$ where $V\left(F_{1}\right)$ is the partite set of order 3. Since each vertex of $F_{1}$ is joined to six vertices of $V(G)-V\left(F_{1}\right)$ by blue edges, we may use the same reasoning as above to conclude that $G$ contains a red $K_{3}$, which we denote by $F_{2}$, where $V\left(F_{2}\right) \subseteq V(G)-V\left(F_{1}\right)$ and so $F_{1}$ and $F_{2}$ are disjoint. We may assume then that every vertex of $V(G)-V\left(F_{2}\right)$ is joined to the vertices of $F_{2}$ by blue edges. Hence, $G$ contains a blue $K_{3,3,4}$. Thus, every vertex of $V\left(F_{1}\right) \cup V\left(F_{2}\right)$ in the blue subgraph $G_{B}$ of $G$ has degree 7 and the remaining four vertices of $G_{B}$ have degree at least 6. Therefore, the size of $G_{B}$ is at least $6 \cdot(7+4 \cdot 6) / 2=33$. By Turán's theorem (Theorem 19.2), either $G_{B}$ contains a 4-clique (and so $G$ contains a blue $K_{4}$ ) or $G_{B}$ has size 33 and so is the Turán graph $T_{10,3}=K_{3,3,4}$. In the latter case, the red subgraph is $2 K_{3}+K_{4}$, which contains a red $K_{4}$ and a red $P_{4}$ as well, and so $G$ contains a red $P_{4}$.

## **Tree-Complete Graph Ramsey Numbers**

We saw in Example 20.10 that $R\left(P_{4}, K_{4}\right)=10$. Vasek Chvátal [57] extended this considerably by finding the exact value of $R(F, H)$ whenever $F$ is any tree and $H$ is any complete graph.

**Theorem 20.11** Let $T$ be a tree of order $p \geq 2$. For every integer $n \geq 2$,
$$R\left(T, K_{n}\right)=(p-1)(n-1)+1 .$$

**Proof.** First, we show that $R\left(T, K_{n}\right) \geq(p-1)(n-1)+1$. Consider a red-blue coloring of the complete graph $K_{(p-1)(n-1)}$ such that the resulting red subgraph is $(n-1) K_{p-1}$; that is, the red subgraph consists of $n-1$ copies of $K_{p-1}$. Since each component of the red subgraph has order $p-1$, it contains no connected subgraph of order greater than $p-1$. In particular, there is no red tree of order $p$. The blue subgraph is then the complete $(p-1)$-partite graph $K_{p-1, p-1, \ldots, p-1}$, where every partite set contains exactly $p-1$ vertices. Hence, there is no blue $K_{n}$ either. Since this red-blue coloring of $K_{(p-1)(n-1)}$ produces neither a red tree $T$ nor a blue $K_{n}$, it follows that $R\left(T, K_{n}\right) \geq(p-1)(n-1)+1$.

We now show that $R\left(T, K_{n}\right) \leq(p-1)(n-1)+1$ for an arbitrary but fixed tree $T$ of order $p \geq 2$ and an integer $n \geq 2$. We verify this inequality by induction on $n$. For $n=2$, we show that $R(T, K_2) \le (p-1)(2-1)+1=p$. Since $R(K_p, K_2)=R(p, 2)=p$, as noted in (20.1), every red-blue coloring of $K_p$ produces a red $K_2$ or a blue $T_2$. Thus, $R(T, K_2) \le p$. Therefore, the inequality $R(T, K_n) \le (p-1)(n-1)+1$ holds when $n=2$. Assume for an integer $k \ge 2$ that
$R(T, K_k) \le (p-1)(k-1)+1$.
Consequently, every red-blue coloring of $K_{(p-1)(k-1)+1}$ contains either a red $T$ or a blue $K_k$. We now show that
$R(T, K_{k+1}) \le (p-1)k+1$.
Let there be given a red-blue coloring of $K_{(p-1)k+1}$. We show that there is either a red tree $T$ or a blue $K_{k+1}$. We consider two cases.

Case 1. There exists a vertex $v$ in $K_{(p-1)k+1}$ that is *incident with at least* $(p-1)(k-1)+1$ blue edges. Suppose that $v v_i$ is a blue edge for $1 \le i \le (p-1)(k-1)+1$. Consider the subgraph $H$ induced by the set $\{v_i: 1 \le i \le (p-1)(k-1)+1\}$. Thus, $H=K_{(p-1)(k-1)+1}$. By the induction hypothesis, $H$ contains either a red $T$ or a blue $K_k$. If $H$ contains a red $T$, so does $K_{(p-1)k+1}$. On the other hand, if $H$ contains a blue $K_k$, then, since $v$ is joined to every vertex of $H$ by a blue edge, there is a blue $K_{k+1}$ in $K_{(p-1)k+1}$.

Case 2. Every vertex of $K_{(p-1)k+1}$ is *incident with at most* $(p-1)(k-1)$ blue edges. So every vertex of $K_{(p-1)k+1}$ is incident with at least $p-1$ red edges. Thus, the red subgraph of $K_{(p-1)k+1}$ has minimum degree at least $p-1$. By Theorem 3.20, this red subgraph contains a red $T$. Therefore, $K_{(p-1)k+1}$ contains a red $T$ as well. ▪

General Ramsey numbers involving three or more graphs exist as well. For $k \ge 3$ graphs $G_1, G_2, \ldots, G_k$, the **Ramsey number** $R(G_1, G_2, \ldots, G_k)$ is the smallest positive integer $n$ such that if every edge of $K_n$ is colored with one of $k$ given colors $i=1, 2, \ldots, k$, then for some $i$ $(1 \le i \le k)$, the graph $K_n$ contains a subgraph (isomorphic to) $G_i$, all of whose edges are colored $i$. The next result gives the Ramsey number of the two stars $K_{1,3}$ and $K_{1,5}$ and the 5-cycle.

## Theorem 20.12 $R(K_{1,3}, K_{1,5}, C_5)=15$.

Proof. First, consider the edge coloring of $K_{14}$ in which every edge of $K_{7,7}$ is colored green. At this point every edge of $2K_7$ is uncolored. Since $K_7$ can be factored into three Hamiltonian cycles by Theorem 13.5, we can color the edges red in one Hamiltonian cycle in each copy of $K_7$ and the remaining edges blue. Then the red subgraph is 2-regular and the blue graph is 4-regular. With this edge coloring, there is no red $K_{1,3}$, no blue $K_{1,5}$ and no green $C_5$. Thus, $R(K_{1,3}, K_{1,5}, C_5) > 14$.

Next, let there be given an edge coloring of $G = K_{15}$ with the colors red, blue and green and suppose that there is no red $K_{1,3}$ and no blue $K_{1,5}$. Then every vertex of G is incident with at least 8 green edges. Thus, in the green subgraph H of G, deg_H v ≥ 8 for every vertex v of H which results in deg_H u + deg_H v ≥ 16 for every pair u, v of nonadjacent vertices of H. Since H has no K₅, it follows by Theorem 6.21 that H is pancyclic and so G contains a green C₅. Therefore, R(K₁,₃, K₁,₅, C₅) = 15. ▪

We now determine the Ramsey number of $k \ge 2$ graphs, all of which are stars.

## Theorem 20.13
Let $s_1, s_2, \ldots, s_k$ be $k \ge 2$ positive integers, $t$ of which are even, and let $s = \sum_{i=1}^k (s_i - 1)$. Then
$$
R(K_{1,s_1}, K_{1,s_2}, \ldots, K_{1,s_k}) = \begin{cases} s + 1 & \text{if } t \text{ is positive and even} \\ s + 2 & \text{otherwise} \end{cases}
$$

Proof. Let $n = R(K_{1,s_1}, K_{1,s_2}, \ldots, K_{1,s_k})$. We consider two cases.

Case 1. $t = 0$ or $t$ is odd. We show here that $n = s + 2$. Let there be given a $k$-edge coloring of $K_{s+2}$ with the colors $1, 2, \ldots, k$ and let $v$ be a vertex of $K_{s+2}$. Since $\deg v = s + 1 = \sum_{i=1}^k (s_i - 1) + 1$, it follows that $v$ is incident with at least $s_i$ edges colored $i$ for some $i$ ($1 \le i \le k$). Thus, $K_{s+2}$ contains $K_{1,s_i}$ as a subgraph all of whose edges are colored $i$ for some $i$ ($1 \le i \le k$). Therefore, $n \le s + 2$.

Next, we show that $n \ge s + 2$. First, suppose that $t = 0$. Then $s + 1$ is odd and, by Theorem 13.5, the complete graph $K_{s+1}$ can be factored into $s/2$ Hamiltonian cycles. For $i = 1, 2, \ldots, k$, let $F_i$ be the $(s_i - 1)$-factor obtained from $(s_i - 1)/2$ Hamiltonian cycles. Assigning the color $i$ to each edge in $F_i$ produces a $k$-edge coloring of $K_{s+1}$ having no subgraph $K_{1,s_i}$, all of whose edges are colored $i$. Thus, $n \ge s + 2$ and so $n = s + 2$.

Next, suppose that $t$ is odd. Hence, $s + 1$ is even and, by Theorem 13.2, the complete graph $K_{s+1}$ can be factored into $s = \sum_{i=1}^k (s_i - 1)$ 1-factors. For $i = 1, 2, \ldots, k$, let $F_i$ be the $(s_i - 1)$-factor obtained from $s_i - 1$ 1-factors. Assigning the color $i$ to the edges in $F_i$ produces a $k$-edge coloring of $K_{s+1}$ having no subgraph $K_{1,s_i}$, all of whose edges are colored $i$. Thus, $n \ge s + 2$ and so $n = s + 2$.

Case 2. $t$ is positive and even. We show here that $n = s + 1$. In this case, $s$ is even. First, we show that $n \le s + 1$. Assume, to the contrary, that there is a $k$-edge coloring of $K_{s+1}$ containing no subgraph $K_{1,s_i}$, all of whose edges are colored $i$, for every $i$ with $1 \le i \le k$. Since every vertex of $K_{s+1}$ has degree $s = \sum_{i=1}^k (s_i - 1)$, it follows that $K_{s+1}$ contains a spanning $(s_i - 1)$-regular subgraph for every $i$ ($1 \le i \le k$). Because some integer $s_i - 1$ is odd, at least one of these subgraphs has an odd number of odd vertices, which is impossible. Thus, $n \le s + 1$.

Next, we show that $n \ge s + 1$. Since $t$ is positive and even, $s$ is even and $K_s$ has a 1-factorization into $s - 1$ 1-factors. We may assume that $s_k \ge 2$ is even. Let $G_i$ be the $(s_i - 1)$-regular spanning subgraph obtained from $s_i - 1$ of these 1-factors.
