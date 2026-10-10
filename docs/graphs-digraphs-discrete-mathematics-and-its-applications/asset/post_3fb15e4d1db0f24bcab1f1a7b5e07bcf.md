
that $x$ and $y$ are not incident with any edges in $X$, implying that $d(x,y) \ge 3$, which is impossible. Assume, without loss of generality, that every vertex in $V_1$ is incident with some edge in $X$; that is, every vertex in $V_1$ is adjacent to some vertex of $V_2$ in $G$.

Let $v \in V_1$ such that $v$ is incident with a maximum number $k$ of edges in $X$, say $v$ is incident with the edges $e_1, e_2, \dots, e_k$ in $X$. Since there are $\delta - k$ edges in $X - \{e_1, e_2, \dots, e_k\}$ and every vertex in $V_1$ is incident with some edge in $X$, there are at most $\delta - k$ vertices in $V_1 - \{v\}$ and so $|V_1| \le \delta - k + 1$. On the other hand, $v$ must also be adjacent to $\deg v - k \ge \delta - k$ vertices in $V_1$ and so there are at least $\delta - k$ vertices in $V_1 - \{v\}$. Therefore, $|V_1| \ge \delta - k + 1$ and so $|V_1| = \delta - k + 1$. Let $u$ be any other vertex of $V_1$, where $u$ is incident, say, with $\ell$ edges, where then $\ell \le k$. Thus $u$ is incident with $\deg u - \ell$ vertices in $V_1 - \{u\}$ and so

$$ \delta - k + 1 = |V_1| \ge \deg u - \ell + 1 \ge \delta - k + 1, $$

which implies that $\deg u = \delta$ and $\ell = k$. Hence

(1) $G_1 = K_{\delta-k+1}$ and (2) $|X| = k(\delta-k+1) = \delta$.

Rewriting the equation in (2), we obtain $(k-\delta)(k-1) = 0$ and so $\delta = k$ or $\delta = 1$. Thus, $G_1 = K_1$ or $G_1 = K_{\delta}$. ■

If $G$ is a graph of order $n \ge 3$ such that $\deg u + \deg v \ge n-1$ for every two nonadjacent vertices $u$ and $v$, then $\text{diam}(G) = 2$. Therefore, the following result of Linda Lesniak [154] is a consequence of Theorem 4.7.

**Corollary 4.9** *If $G$ is a graph of order $n$ such that $\deg u + \deg v \ge n-1$ for each pair $u, v$ of nonadjacent vertices of $G$, then $\lambda(G) = \delta(G)$.*

### 4.2 Theorems of Menger and Whitney

A nontrivial graph $G$ is connected (or, equivalently, 1-connected) if every two distinct vertices of $G$ are connected by at least one path. This fact has been generalized in several ways, many of which involve, either directly or indirectly, a theorem [169] due to Karl Menger (1902–1985), who was born in Vienna, Austria. Menger developed a talent for mathematics and physics at an early age and entered the University of Vienna in 1920 to study physics. The following year he attended a lecture by Hans Hahn on *Neueres über Kurvenbegriff* (What's new concerning the concept of a curve) and Menger's interests turned toward mathematics. In the lecture it was mentioned that (at that time) there was no satisfactory definition of a curve, despite attempts to do so by a number of distinguished mathematicians, including Georg Cantor, Camille Jordan and Giuseppe Peano. Some mathematicians, including Felix Hausdorff and Ludwig Bieberbach, felt that it was unlikely that this problem would ever be solved. Despite being an undergraduate with limited mathematical background, Menger solved the problem and presented his solution to Hahn. This led Menger to work on curve and dimension theory. After completing his studies at Vienna, Menger left to broaden his mathematics in Amsterdam.

In 1927 Menger returned to the University of Vienna to accept the position of Chair of Geometry. It was during that year that he published the paper “Zur allgemeinen Kurventheorie” (which contained Menger’s Theorem). Menger himself referred to this result as the “n-arc theorem” and proved it as a lemma for a theorem in curve theory.

In the spring of 1930, Karl Menger traveled to Budapest and met many Hungarian mathematicians, including Dénes König. Menger had read some of König’s papers. During his visit, Menger learned that König was working on a book that would contain what was known about graph theory at that time. Menger was pleased to hear this and mentioned his theorem to König. However, König was not aware of Menger’s work and, in fact, didn’t believe that the theorem was true. Indeed, the very evening of their meeting, König set out to construct a counterexample. When the two met again the next day, König greeted Menger with “A sleepless night!”. König then asked Menger to describe his proof, which he did. After that, König said that he would add a final section to his book on the theorem. As a result, König added a chapter to his 1936 book *Theorie der endlichen und unendlichen Graphen*, which would become the first book written on graph theory [148]. This was a major reason why Menger’s theorem became so widely known among those interested in graph theory.

While Menger had visiting positions in the United States during 1930–31 (at Harvard University and the Rice Institute), he held professorships at the University of Notre Dame during 1937–46 and the newly founded Illinois Institute of Technology during 1946–71.

## Menger’s Theorem

Before stating and presenting a proof of Menger’s theorem, some additional terminology is needed. For two nonadjacent vertices $u$ and $v$ in a graph $G$, a $u-v$ separating set is a set $S \subseteq V(G)-\{u, v\}$ such that $u$ and $v$ lie in different components of $G-S$. A $u-v$ separating set of minimum cardinality is called a minimum $u-v$ separating set.

For two distinct vertices $u$ and $v$ in a graph $G$, a collection of $u-v$ paths is internally disjoint if every two paths in the collection have only $u$ and $v$ in common. Menger’s theorem states that the concepts of internally disjoint $u-v$ paths and $u-v$ separating sets are linked. In the graph $G$ of Figure 4.4, there is a set $S=\{w_1, w_2, w_3\}$ of vertices of $G$ that separate the vertices $u$ and $v$. No set with fewer than three vertices separates $u$ and $v$. According to Menger’s theorem, there are three internally disjoint $u-v$ paths in $G$.

![](img/598a6ae3fd44120830ada34717906f29_116_0.png)

Figure 4.4: A graph illustrating Menger's theorem

## Theorem 4.10 (Menger's Theorem)

Let $u$ and $v$ be nonadjacent vertices in a graph $G$. The minimum number of vertices in a $u - v$ separating set equals the maximum number of internally disjoint $u - v$ paths in $G$.

**Proof.** We proceed by induction on the size of graphs. The theorem is certainly true for every empty graph. Assume that the theorem holds for all graphs of size less than $m$, where $m \geq 1$, and let $G$ be a graph of size $m$. Moreover, let $u$ and $v$ be two nonadjacent vertices of $G$. If $u$ and $v$ belong to different components of $G$, then the result follows. So we may assume that $u$ and $v$ belong to the same component of $G$. Suppose that a minimum $u - v$ separating set consists of $k \geq 1$ vertices. Then $G$ contains at most $k$ internally disjoint $u - v$ paths. We show, in fact, that $G$ contains $k$ internally disjoint $u - v$ paths. Since this is obviously true if $k = 1$, we may assume that $k \geq 2$. We now consider three cases.

*Case 1. Some minimum $u - v$ separating set $X$ in $G$ contains a vertex $x$ that is adjacent to both $u$ and $v$. Then $X - \{x\}$ is a minimum $u - v$ separating set in $G - x$ consisting of $k - 1$ vertices. Since the size of $G - x$ is less than $m$, it follows by the induction hypothesis that $G - x$ contains $k - 1$ internally disjoint $u - v$ paths. These paths together with the path $P = (u, x, v)$ produce $k$ internally disjoint $u - v$ paths in $G$.*

*Case 2. For every minimum $u - v$ separating set $S$ in $G$, either every vertex in $S$ is adjacent to $u$ and not to $v$ or every vertex in $S$ is adjacent to $v$ and not to $u$. Necessarily then, $d(u, v) \geq 3$. Let $P = (u, x, y, \ldots, v)$ be a $u - v$ geodesic in $G$, where $e = xy$. Every minimum $u - v$ separating set in $G - e$ contains at least $k - 1$ vertices. We show, in fact, that every minimum $u - v$ separating set in $G - e$ contains $k$ vertices.*

Since $Z \cup \{y\}$ is also a minimum $u-v$ separating set in $G$ and each vertex $z_i$ $(1 \leq i \leq k-1)$ is adjacent to $u$ but not to $v$, it follows that $y$ is adjacent to $u$. This, however, contradicts the assumption that $P$ is a $u-v$ geodesic. Thus, $k$ is the minimum number of vertices in a $u-v$ separating set in $G-e$. Since the size of $G-e$ is less than $m$, it follows by the induction hypothesis that there are $k$ internally disjoint $u-v$ paths in $G-e$ and in $G$ as well.

*Case 3. There exists a minimum $u-v$ separating set $W$ in $G$ such that*

(1) *no vertex of $W$ is adjacent to both $u$ and $v$ and*

(2) *$W$ contains at least one vertex not adjacent to $u$ and at least one vertex not adjacent to $v$.*

Let $W = \{w_1, w_2, \dots, w_k\}$. Let $G_u$ be the subgraph of $G$ consisting of, for each $i$ with $1 \leq i \leq k$, all $u-w_i$ paths in $G$ in which $w_i \in W$ is the only vertex of the path belonging to $W$. Let $G^\prime_u$ be the graph constructed from $G_u$ by adding a new vertex $v^\prime$ and joining $v^\prime$ to each vertex $w_i$ for $1 \leq i \leq k$. The graphs $G_v$ and $G^\prime_v$ are defined similarly.

Since $W$ contains a vertex that is not adjacent to $u$ and a vertex that is not adjacent to $v$, the sizes of both $G^\prime_u$ and $G^\prime_v$ are less than $m$. So $G^\prime_u$ contains $k$ internally disjoint $u-v^\prime$ paths $A_i$ $(1 \leq i \leq k)$, where $A_1$ contains $w_1$. Also, $G^\prime_v$ contains $k$ internally disjoint $u^\prime-v$ paths $B_i$ $(1 \leq i \leq k)$, where $B_1$ contains $w_1$. Let $A^\prime_i$ be the $u-w_i$ subpath of $A_i$ and let $B^\prime_i$ be the $w_i-v$ subpath of $B_i$ for $1 \leq i \leq k$. The $k$ paths constructed from $A^\prime_i$ and $B^\prime_i$ for each $i$ $(1 \leq i \leq k)$ are internally disjoint $u-v$ paths in $G.$

## Whitney’s Theorem

We mentioned that Karl Menger visited Dénès König in Budapest, Hungary early in 1930, which led to his theorem being included in König’s book. Later in 1930, Menger went to the United States and spent the period from September of 1930 to February of 1931 as a visiting lecturer at Harvard University. It was at one of his seminar talks that he presented his theorem. During that period, Hassler Whitney (1907–1989) was doing research for his doctoral thesis in graph theory at Harvard. For a short period after receiving his Ph.D. in 1932 from Harvard, Whitney worked on graph theory, making important contributions, but thereafter turned to topology when the area was just being called topology. Whitney was a faculty member at Harvard until 1952, when he went to the Institute for Advanced Study in Princeton. Whitney was at Harvard during the period that the United States was involved in World War II. He had great interest and ability in applied mathematics. Because of this, he was brought in as a consultant to the Applied Mathematics Group at Columbia University. That part of the Applied Mathematics Panel was primarily the responsibility of Whitney. He developed mathematical principles to discover best techniques for aerial gunnery and was involved in making improvements to weapons systems.

Although research was a large part of Whitney’s professional life, he contributed to mathematics in two ways. During 1944–1949 he was editor of
