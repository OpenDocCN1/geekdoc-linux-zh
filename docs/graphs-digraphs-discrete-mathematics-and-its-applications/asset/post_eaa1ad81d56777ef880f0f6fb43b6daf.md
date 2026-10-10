
## 2.2. DISTANCE IN GRAPHS

The distance $d$ defined above satisfies the following properties in a connected graph $G$:

-   (1) $d(u, v) \geq 0$ for every two vertices $u$ and $v$ of $G$;
-   (2) $d(u, v) = 0$ if and only if $u = v$;
-   (3) $d(u, v) = d(v, u)$ for all $u, v \in V(G)$ (the **symmetric property**);
-   (4) $d(u, w) \leq d(u, v) + d(v, w)$ for all $u, v, w \in V(G)$ (the **triangle inequality**).

Since $d$ satisfies the four properties (1)–(4), $d$ is a **metric** on $V(G)$ and $(V(G), d)$ is a **metric space**. Because $d$ satisfies the symmetric property, we can speak of the distance *between* two vertices $u$ and $v$ rather than the distance *from* $u$ to $v$.

With the aid of this distance we can present a useful characterization of bipartite graphs.

**Theorem 2.6** *A nontrivial graph $G$ is a bipartite graph if and only if $G$ contains no odd cycles.*

**Proof.** Suppose first that $G$ is bipartite. Then $V(G)$ can be partitioned into partite sets $U$ and $W$ (and so every edge of $G$ joins a vertex of $U$ and a vertex of $W$). Let $C = (v_1, v_2, \dots, v_k, v_1)$ be a $k$-cycle of $G$. We may assume that $v_1 \in U$. Thus, $v_2 \in W$, $v_3 \in U$ and so forth. In particular, $v_i \in U$ for every odd integer $i$ with $1 \leq i \leq k$ and $v_j \in W$ for every even integer $j$ with $2 \leq j \leq k$. Since $v_1 \in U$, it follows that $v_k \in W$ and so $k$ is even.

For the converse, let $G$ be a nontrivial graph containing no odd cycles. If $G$ is empty, then $G$ is clearly bipartite. Hence it suffices to show that every nontrivial component of $G$ is bipartite and so we may assume that $G$ itself is connected. Let $u$ be a vertex of $G$ and let

$U = \{x \in V(G): \ d(u, x)\ \text{is even}\}$ and $W = \{x \in V(G): \ d(u, x)\ \text{is odd}\}.$

Thus, $u \in U$. We show that $G$ is a bipartite graph having partite sets $U$ and $W$. It suffices to show that no two vertices of $U$ are adjacent and no two vertices of $W$ are adjacent. Suppose that $W$ contains two adjacent vertices $w_1$ and $w_2$. Let $P_1$ be a $u-w_1$ geodesic and $P_2$ a $u-w_2$ geodesic. Let $z$ be the last vertex that $P_1$ and $P_2$ have in common (possibly $z = u$). Then the length of the $z-w_1$ subpath $P_1'$ of $P_1$ and the length of the $z-w_2$ subpath $P_2'$ of $P_2$ are of the same parity. Thus, the paths $P_1'$ and $P_2'$ together with the edge $w_1w_2$ produce an odd cycle. This is a contradiction. The argument that no two vertices of $U$ are adjacent is similar.

### The Eccentricity of a Vertex

It is often of value to know how far any vertex of a connected graph $G$ is from a given vertex of $G$. The **eccentricity** $e(v)$ of a vertex $v$ in a connected graph $G$ is the distance between $v$ and a vertex farthest from $v$ in $G$. The eccentricities of the vertices of the graph $G$ in Figure 2.7 are shown in Figure 2.8.

![](img/598a6ae3fd44120830ada34717906f29_58_0.png)

![](img/598a6ae3fd44120830ada34717906f29_58_1.png)

The eccentricities of the vertices in the graph $G$ of Figure 2.8 illustrate the following theorem.

> **Theorem 2.7** If $u$ and $v$ are adjacent vertices in a connected graph $G$, then
>
> $$|e(u) - e(v)| \leq 1.$$

**Proof.** Assume, without loss of generality, that $e(u) \geq e(v)$. Moreover, let $w$ be a vertex of $G$ such that $e(u) = d(u, w)$. By the triangle inequality, $d(u, w) \leq d(u, v) + d(v, w)$. Since $d(u, v) = 1$ and $d(v, w) \leq e(v)$, it follows that

$$|e(u) - e(v)| = e(u) - e(v) \leq d(u, w) - d(v, w) \leq d(u, w) - 1. \quad \blacksquare$$

The **diameter** $\operatorname{diam}(G)$ of a connected graph $G$ is the largest eccentricity among the vertices of $G$, while the **radius** $\operatorname{rad}(G)$ is the smallest eccentricity among the vertices of $G$. The diameter of $G$ is, therefore, the greatest distance between any two vertices of $G$. A vertex $v$ with $e(v) = \operatorname{rad}(G)$ is called a **central vertex** of $G$ and a vertex $v$ with $e(v) = \operatorname{diam}(G)$ is called a **peripheral vertex** of $G$. Two vertices $u$ and $v$ of $G$ with $d(u, v) = \operatorname{diam}(G)$ are **antipodal vertices** of $G$. Necessarily, if $u$ and $v$ are antipodal vertices in $G$, then both $u$ and $v$ are peripheral vertices. For the graph $G$ of Figure 2.8, $\operatorname{diam}(G) = 4$ and $\operatorname{rad}(G) = 2$. In particular, $v_6$ is the only central vertex of $G$ and $v_1$ and $v_8$ are the only peripheral vertices of $G$. Since $d(v_1, v_8) = 4 = \operatorname{diam}(G)$, it follows that $v_1$ and $v_8$ are antipodal vertices of $G$. It is certainly not always the case that $\operatorname{diam}(G) = 2 \operatorname{rad}(G)$ as, for example, $\operatorname{diam}(P_4) = 3$ and $\operatorname{rad}(P_4) = 2$. Indeed, the following can be said about the radius and diameter of a connected graph.

> **Theorem 2.8** For every nontrivial connected graph $G$,
>
> $$\operatorname{rad}(G) \leq \operatorname{diam}(G) \leq 2 \operatorname{rad}(G).$$

**Proof.** The inequality rad$(G) \leq$ diam$(G)$ is immediate from the definitions. Let $u$ and $w$ be two antipodal vertices of $G$ and let $v$ be a central vertex of $G$. Therefore, $d(u, w) = \text{diam}(G)$ and $e(v) = \text{rad}(G)$. By the triangle inequality,
$\text{diam}(G) = d(u, w) \leq d(u, v) + d(v, w) \leq 2e(v) = 2\text{rad}(G)$,
as desired.

For a connected graph $G$ of order $n \geq 2$, the **eccentricity sequence** of $G$ is the nondecreasing sequence $e_1, e_2, \ldots, e_n$ of positive integers for which the vertices of $G$ can be labeled as $v_1, v_2, \ldots, v_n$ such that $e(v_i) = e_i$ for $1 \leq i \leq n$. Thus, $e_1 = \text{rad}(G)$ and $e_n = \text{diam}(G)$. In fact, since $G$ has at least two peripheral vertices, $e_{n-1} = \text{diam}(G)$ as well. The eccentricity sequence of the graph $G$ of Figure 2.8 is

2, 3, 3, 3, 3, 3, 3, 3, 4, 4.

In fact, for every connected graph $G$ of order $n \geq 2$, its eccentricity sequence $e_1, e_2, \ldots, e_n$ satisfies (1) $e_n \leq 2e_1$ by Theorem 2.8 and (2) $e_{i+1} - e_i \leq 1$ for $1 \leq i \leq n-1$. To see why (2) is true, suppose that $e(v_i) = e_i$ for $1 \leq i \leq n$. Let $\boldsymbol{P} = (v_1 = u_1, u_2, \ldots, u_k = v_{i+1})$ be a $v_1-v_{i+1}$ path in $G$. By Theorem 2.7, $|e(u_{i+1}) - e(u_i)| \leq 1$ for $1 \leq i \leq k-1$ and so the eccentricities of consecutive vertices on $\boldsymbol{P}$ differ by at most 1. Therefore, every integer between $e_1$ and $e_n$ is the eccentricity of some vertex of $G$.

Theorem 2.8 gives the lower bound rad$(G)$ for the diameter of a connected graph $G$ as well as the upper bound 2 rad$(G)$. This is one of many results for which a question of “sharpness” is involved. These invite the question: Just how good is this result? Ordinarily, there are many interpretations of such a question. We shall consider some possible interpretations in the case of the upper bound.

Certainly, the upper bound in Theorem 2.8 would not be considered sharp if diam$(G) < 2$ rad$(G)$ for every graph $G$; however, it would be considered sharp indeed if diam$(G) = 2$ rad$(G)$ for every graph $G$. In the latter case, we would actually have a formula or an identity, not just a bound. Of course, we have seen that there are graphs $G$ for which diam$(G) < 2$ rad$(G)$ and there are graphs $H$ for which diam$(H) = 2$ rad$(H)$. This alone may be satisfactory to say that this bound is sharp. However, a preferred reason for calling this bound sharp is if there is an infinite class $\mathcal{H}$ of graphs such that diam$(H) = 2$ rad$(H)$ for each graph $H$ belonging to $\mathcal{H}$. Such a class exists; for example, let $\mathcal{H}$ consist of the graphs of the type $K_l \vee \overline{K_s}$. One disadvantage of this class is that for each $H \in \mathcal{H}$, diam$(H) = 2$ and rad$(H) = 1$. Perhaps a more satisfactory infinite class would be the class of paths $P_{2k+1}$, $k \geq 1$. In this case, diam$(P_{2k+1}) = 2k$ and rad$(P_{2k+1}) = k$; that is, for each positive integer $k$, there exists a connected graph $G$ such that diam$(G) = 2$ rad$(G) = 2k$.
