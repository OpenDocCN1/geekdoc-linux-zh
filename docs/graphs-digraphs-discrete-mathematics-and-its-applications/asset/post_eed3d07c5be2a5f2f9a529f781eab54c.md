
interested in graph theory early in his mathematical career, at a time when the respectability of graph theory occurred primarily within Hungary. However, Dirac was attracted to graph theory and became one of those mathematicians whose contributions to graph theory brought it to a place of prominence. In fact, the mathematician Carsten Thomassen wrote:

> He (Dirac) was more interested in the intrinsic beauty of graph theory than its applications.

With the aid of Theorem 6.1, a sufficient condition for a graph to have a Hamiltonian path can also be given.

**Corollary 6.3** Let $G$ be a graph of order $n \geq 2$. If $\sigma_2(G) \geq n-1$, then $G$ contains a Hamiltonian path.

**Proof.** Let $H = G \vee K_1$ be the join of $G$ and $K_1$, where $w$ is the vertex of $H$ that does not belong to $G$. Then $\sigma_2(H) \geq n+1$. Since the order of $H$ is $n+1$, it follows by Theorem 6.1 that $H$ is Hamiltonian. Let $C$ be a Hamiltonian cycle of $H$. Deleting $w$ from $C$ produces a Hamiltonian path in $G.$

## The Closure of a Graph

J. Adrian Bondy and Vasek Chvalal [34] observed that the proof of Ore's theorem (Theorem 6.1) neither uses nor needs the full strength of the requirement that the degree sum of each pair of nonadjacent vertices is at least the order of the graph being considered. Initially, Bondy and Chvalal made the following observation.

**Theorem 6.4** Let $u$ and $v$ be nonadjacent vertices in a graph $G$ of order $n$ such that $\deg u + \deg v \geq n$. Then $G + uv$ is Hamiltonian if and only if $G$ is Hamiltonian.

**Proof.** Certainly, if $G$ is Hamiltonian, then $G + uv$ is Hamiltonian. For the converse, suppose that $G + uv$ is Hamiltonian but $G$ is not. Then every Hamiltonian cycle in $G + uv$ contains the edge $uv$, implying that $G$ contains a Hamiltonian $u-v$ path. We can now proceed exactly as in the proof of Theorem 6.1 to produce a contradiction.

![](img/598a6ae3fd44120830ada34717906f29_143_0.png)

![](img/598a6ae3fd44120830ada34717906f29_143_1.png)

**Figure 6.4: Constructing the closure of a graph**

**Theorem 6.5** Let $G$ be a graph of order $n$. If $G_1$ and $G_2$ are graphs obtained by repeatedly joining pairs of nonadjacent vertices whose degree sum is at least $n$ until no such pair remains, then $G_1=G_2$.

**Proof.**  Suppose that $G_1$ is obtained by adding the edges $e_1, e_2, \ldots, e_r$ to $G$ in the given order and $G_2$ is obtained from $G$ by adding the edges $f_1, f_2, \ldots, f_s$ in the given order. Assume, to the contrary, that $G_1 \neq G_2$. Then $E(G_1) \neq E(G_2)$. Thus, we may assume that there is a first edge $e_i = xy$ in the sequence $e_1, e_2, \ldots, e_r$ that does not belong to $G_2$. If $i=1$, then let $G=H$; otherwise, let $H=G + \{e_1, e_2, \ldots, e_{i-1}\}$. Then $H \neq x$ is a subgraph of $G_2$ and $x$ and $y$ are nonadjacent vertices of $H$. Since $\operatorname{deg}_H x + \operatorname{deg}_H y \geq n$, it follows that $\operatorname{deg}_{G_2} x + \operatorname{deg}_{G_2} y \geq n$, which produces a contradiction.

Repeated application of Theorem 6.4 gives us the following result.

**Theorem 6.6** A graph is Hamiltonian if and only if its closure is Hamiltonian.

Since each complete graph with at least three vertices is Hamiltonian, we obtain the following sufficient condition for a graph to be Hamiltonian due to Bondy and Chvátal [34].

**Theorem 6.7** Let $G$ be a graph with at least three vertices. If $CL(G)$ is complete, then $G$ is Hamiltonian.

If a graph $G$ satisfies the conditions of Theorem 6.1, then $CL(G)$ is complete and so, by Theorem 6.7, $G$ is Hamiltonian. Thus, Ore’s theorem is an immediate corollary of Theorem 6.7 (although chronologically it preceded the theorem of Bondy and Chvátal by several years). In fact, many sufficient conditions for a graph to be Hamiltonian based on the degrees of the vertices of a graph can be deduced from Theorem 6.7. The following result of Chvátal [54] is an example of one of the strongest of these.

**Theorem 6.8** Let $G$ be a graph of order $n \geq 3$, the degrees $d_i$ of whose vertices satisfy $d_1 \leq d_2 \leq \cdots \leq d_n$. If there is no integer $k < n/2$ for which $d_k \leq k$ and $d_{n-k} \leq n - k - 1$, then $G$ is Hamiltonian.

**Proof.** Let $H = CL(G)$. We show that $H$ is complete which, by Theorem 6.7, implies that $G$ is Hamiltonian. Assume, to the contrary, that $H$ is not complete. Let $u$ and $w$ be nonadjacent vertices of $H$ for which $\deg_H u + \deg_H w$ is as large as possible. Since $u$ and $w$ are nonadjacent vertices of $H$, it follows that $\deg_G u + \deg_G w \leq n - 1$. Assume, without loss of generality, that $\deg_H u \leq \deg_H w$. Thus, if $k = \deg_H u$, we have that $k \leq (n-1)/2 < n/2$ and $\deg_H w \leq n - 1 - k$. Let $W$ denote the vertices other than $w$ that are not adjacent to $w$ in $H$. Then $|W| = n - 1 - \deg_H w \geq k$. Also, by the choice of $u$ and $w$, every vertex $v \in W$ satisfies

$\deg_G v \leq \deg_H v \leq \deg_H u = k.$

Thus, $G$ has at least $k$ vertices of degree at most $k$ and so $d_k \leq k$. Similarly, let $U$ denote the vertices other than $u$ that are not adjacent to $u$ in $H$. Then $|U| = n - 1 - \deg_G u = n - k - 1$. Every vertex $v \in U$ satisfies

$\deg_G v \leq \deg_H v \leq \deg_H w \leq n - 1 - k,$

implying that $d_{n-k-1} \leq n - k - 1$. However,

$\deg_G u \leq \deg_H u \leq \deg_H w \leq n - 1 - k,$

so $d_{n-k} \leq n - k - 1$. This, however, contradicts the hypothesis of the theorem. Thus, $H = CL(G)$ is complete. $\blacksquare$.

All of the sufficient conditions presented thus far for a graph $G$ to be Hamiltonian involve the degrees of the vertices of $G$. In fact, if $G$ has order $n$, then each of these conditions requires some one of the vertices of $G$ to have degree at least $n/2$. In the case of regular graphs, however, this situation can be improved. Bill Jackson [134] showed that every 2-connected $r$-regular graph of order at most $3r$ is Hamiltonian. As we are about to see, the Petersen graph shows that $3r$ cannot be replaced by $3r+1$. We mentioned earlier that the girth (the length of a smallest cycle) of the Petersen graph $P$ is 5 and its circumference (the length of a longest cycle) is 9. In fact, $P - v$ contains a 9-cycle for every vertex $v$ of $P$. We now verify that the Petersen graph has circumference 9 by showing that it is not Hamiltonian.

# **Theorem 6.9** The Petersen graph is not Hamiltonian.

**Proof.** Assume, to the contrary, that the Petersen graph $P$ is Hamiltonian. Then $P$ has a Hamiltonian cycle

$C = (v_1, v_2, \dots, v_{10}, v_1).$

Since $P$ is cubic, $v_1$ is adjacent to exactly one of the vertices $v_3, v_4, \dots, v_9$. However, since $P$ contains neither a 3-cycle nor a 4-cycle, $v_1$ is adjacent to exactly one of $v_5, v_6$ and $v_7$. Because of the symmetry of $v_5$ and $v_7$, we may assume that $v_1$ is adjacent either to $v_5$ or to $v_6$.

*Case 1.* $v_{1}$ is adjacent to $v_{5}$ in $P$. Then $v_{10}$ is adjacent to exactly one of $v_{4}$, $v_{5}$ and $v_{6}$, which results in a 4-cycle, a 3-cycle or a 4-cycle, respectively, each of which is impossible.

*Case 2.* $v_{1}$ is adjacent to $v_{6}$ in $P$. Again, $v_{10}$ is adjacent to exactly one of $v_{4}$, $v_{5}$ and $v_{6}$. Since $P$ does not contain a 3-cycle or a 4-cycle, $v_{10}$ must be adjacent to $v_{4}$. However, then this returns us to Case 1, where $v_{1}$ and $v_{5}$ are replaced by $v_{10}$ and $v_{4}$, respectively. $\blacksquare$

The next sufficient condition for a graph $G$ to be Hamiltonian does not involve the degrees of the vertices of $G$ but, rather, involves the cardinality of sets of pairwise nonadjacent vertices of a graph and its connectivity. A set $U$ of vertices in a graph $G$ is **independent** if no two vertices in $U$ are adjacent. (Some refer to an independent set of vertices as a **stable set**.) The maximum number of vertices in an independent set of vertices of $G$ is called the **vertex independence number** or, more simply, the **independence number** of $G$ and is denoted by $\alpha(G)$. For example, $\alpha(K_{n,s}) = \max\{r, s\}$, $\alpha(C_{n}) = \lfloor \frac{n}{2} \rfloor$ and $\alpha(K_{n}) = 1$. Vašek Chvátal and Paul Erdős [58] showed that if $G$ is a graph of order at least 3 whose connectivity is at least as large as its independence number, then $G$ must be Hamiltonian.

# **Theorem 6.10** Let $G$ be a graph of order at least 3. If $\kappa(G) \geq \alpha(G)$, then $G$ is Hamiltonian.

**Proof.** If $\alpha(G) = 1$, then $G$ is complete and therefore Hamiltonian. Hence, we may assume that $\alpha(G) = k \geq 2$. Since $\kappa(G) \geq 2$, it follows that $G$ is 2-connected and so $G$ contains a cycle by Theorem 4.15. Let $C$ be a longest cycle in $G$. By Theorem 4.15, $C$ contains at least $k$ vertices. We show that $C$ is a Hamiltonian cycle. Assume, to the contrary, that $C$ is not a Hamiltonian cycle. Then there is some vertex $w$ of $G$ that does not lie on $C$. Since $G$ is $k$-connected, it follows with the aid of Corollary 4.13 that $G$ contains $k$ paths $P_{1}$, $P_{2}, \dots , P_{k}$ such that $P_{i}$ is a $w-v_{i}$ path where $v_{i}$ is the only vertex of $P_{i}$ on $C$ and such that the paths are pairwise-disjoint except for $w$.

In some cyclic ordering of the vertices of $C$, let $u_{i}$ be the vertex that follows $v_{i}$ on $C$ for each $i$ $(1 \leq i \leq k)$. No vertex $u_{i}$ is adjacent to $v_{j}$ for otherwise, replacing the edge $u_{i}v_{i}$ by $P_{i}$ and $uw_{i}$ produces a cycle whose length exceeds that of $C$. Let $S = \{w, u_{1}, u_{2}, \dots , u_{k}\}$. Since $|S| = k + 1 > \alpha(G)$ and $uw_{i} \notin E(G)$ for each $i$ $(1 \leq i \leq k)$, there are distinct integers $r$ and $s$ such that $1 \leq r, s \leq k$ and $u_{r}u_{s} \in E(G)$. Replacing the edges $u_{r}v_{r}$ and $u_{s}v_{s}$ by the edge $u_{r}u_{s}$ and the paths $P_{r}$ and $P_{s}$ produces a cycle that is longer than $C$. This is a contradiction. $\blacksquare$

For the non-Hamiltonian Petersen graph $P$, $\kappa(P) = 3$ and $\alpha(P) = 4$; so, as anticipated by Theorem 6.10, $\kappa(P) < \alpha(P)$. On the other hand, $\kappa(P) \geq \alpha(P) - 1$ and, consequently, $P$ has a Hamiltonian path (see Exercise 13).
