
## 7.5 Kings in Tournaments

While tournaments can be used to represent the results of round robin tournaments (especially among teams participating in a sports event), they can be used to model any collection of objects where in each pair of objects, one is preferred over the other in some manner. An example of this occurs in a flock of chickens. In a pair of chickens, one chicken will dominate the other. The dominant chicken in the pair asserts this dominance by pecking the other on its head and neck. (This is what led to the term _pecking order_.) It is rare when this dominance is transitive; that is, if the first chicken pecks a second chicken and the second pecks a third, it does not mean that the first necessarily pecks the third. The question then arises: Which chicken (or chickens) should be considered most dominant in the flock? Any such chicken is referred to as a _king chicken_. Landau [152] defined a chicken $K$ in a flock $\mathcal{F}$ of chickens to be a _king_ if for every chicken $C$ in $\mathcal{F}$, either $K$ pecks $C$ or $K$ pecks a chicken that pecks $C$.

This situation can be modeled by a tournament and leads to a concept involving tournaments. A vertex $u$ in a tournament $T$ is a **king** in $T$ if for every vertex $w$ different from $u$, either $u \to w$ or there is a vertex $v$ such that $u \to v \to w$. Landau then proved the following.

> **Theorem 7.20** _Every tournament contains a king._

**Proof.** Let $T$ be a tournament and let $u$ be a vertex having maximum out-degree in $T$. We show that $u$ is a king. If this is not the case, then there is a vertex $w$ in $T$ for which $u$ is neither adjacent to $w$ nor adjacent to any vertex that is adjacent to $w$. Then $u$ is adjacent to every vertex to which $u$ is adjacent and adjacent to $u$ as well. Thus, $\operatorname{od}w > \operatorname{od}u$, a contradiction. $\blacksquare$

A vertex $u$ in a tournament of order $n$ is called an **emperor** if $\operatorname{od}u = n-1$. Since no vertex is adjacent to $u$, we have the following observation.

> **Theorem 7.21** _If a tournament $T$ has an emperor $u$, then $u$ is the unique king in $T$._

While it’s possible for a tournament to have exactly one king, it is not possible for a tournament to contain exactly two kings.

> **Theorem 7.22** _Every tournament containing no emperor contains at least three kings._

### Proof of Theorem 7.22

Let $u$ be a king in $T$. By Theorem 7.21, $u$ is not an emperor. Let $v$ be a vertex of maximum out-degree among the vertices adjacent to $u$. We claim that $v$ is also a king of $T$. Assume, to the contrary, that $v$ is not a king. Then there is a vertex $x$ of $T$ such that $v$ is neither adjacent to $x$ nor adjacent to a vertex that is adjacent to $x$. Thus, $x$ is adjacent to both $u$ and $v$. Furthermore, $x$ is adjacent to every vertex to which $v$ is adjacent. However then, $\operatorname{od} x > \operatorname{od} v$, a contradiction. Thus, $v$ is a king of $T$.

Next, among the vertices adjacent to $v$, let $w$ be one of maximum out-degree. We claim that $w$ is also a king of $T$. Assume, to the contrary, that $w$ is not a king. Then there is a vertex $y$ of $T$ such that $w$ is neither adjacent to $y$ nor adjacent to a vertex that is adjacent to $y$. Thus, $y$ is adjacent to $v$ and $w$. In addition, $y$ is adjacent to every vertex to which $w$ is adjacent. However then, $\operatorname{od} y > \operatorname{od} w$, a contradiction. Hence $w$ is a king of $T$.

## 7.6 Hamiltonian Tournaments

The large number of arcs in a tournament often produce paths and cycles of varying lengths. Perhaps the most basic result of this type was a property of tournaments first observed by László Rédei [197] in 1934, resulting in the first theoretical result on tournaments. A path in a digraph $D$ containing every vertex of $D$ is a **Hamiltonian path**.

> **Theorem 7.23** *Every tournament contains a Hamiltonian path.*

**Proof.** Let $T$ be a tournament of order $n$ and let $P = (v_1, v_2, \dots, v_k)$ be a longest path in $T$. If $P$ is not a Hamiltonian path of $T$, then $1 \leq k < n$ and there is a vertex $v$ of $T$ not on $P$. Since $P$ is a longest path, $(v, v_1), (v_k, v) \notin E(T)$, and so $(v_1, v), (v, v_k) \in E(T)$. This implies that there is a largest integer $i$ ($1 \leq i < k$) such that $(v_i, v) \in E(T)$. So $(v, v_{i+1}) \in E(T)$ (see Figure 7.18). But then

$$(v_1, v_2, \dots, v_i, v, v_{i+1}, \dots, v_k)$$

is a path whose length exceeds that of $P$, producing a contradiction.

![](img/598a6ae3fd44120830ada34717906f29_192_0.png)

A simple but useful consequence of Theorem 7.23 concerns transitive tournaments.

> **Corollary 7.24** *Every transitive Tournament contains exactly one Hamiltonian path.*

The preceding corollary is a special case of a result found independently by Rédei [197] and Tibor Szekeres [231], who showed that every tournament contains an odd number of Hamiltonian paths.

Figure 7.19 shows a tournament of order 5 consisting of three strong components $S_1$, $S_2$ and $S_3$, where $S_1$ and $S_3$ consists of a single vertex and $S_2$ is a 3-cycle. This tournament has three Hamiltonian paths, namely $P_1 = (u, v, w, x, y)$, $P_2 = (u, w, x, v, y)$ and $P_3 = (u, x, v, w, y)$.

![](img/598a6ae3fd44120830ada34717906f29_193_0.png)

While each transitive tournament contains exactly one Hamiltonian path, there are, not surprisingly, tournaments with many Hamiltonian paths. The next result, also due to Szekeres [231], establishes the existence of such tournaments and provides a lower bound on the number of Hamiltonian paths in them. The proof of this result, considered the first application of the probabilistic method in combinatorics, will be presented in Chapter 21 (see Theorem 21.3).

**Theorem 7.25** *For each integer $n \geq 2$, there exists a tournament of order $n$ containing at least $n!/2^{n-1}$ Hamiltonian paths.*

While every tournament contains a Hamiltonian path, certainly not every tournament contains a Hamiltonian cycle. Indeed, by Theorem 7.12, every transitive tournament is acyclic. If a tournament $T$ contains a Hamiltonian cycle, then $T$ is strong by Theorem 7.4. Paul Camion [41] showed that the converse is true as well.

**Theorem 7.26** *A nontrivial tournament $T$ is Hamiltonian if and only if $T$ is strong.*

**Proof.** We have already seen that every Hamiltonian tournament is strong. For the converse, assume that $T$ is a nontrivial strong tournament. Thus, $T$ contains cycles. Let $C$ be a cycle of maximum length in $T$. If $C$ contains all of the vertices of $T$, then $C$ is a Hamiltonian cycle. So, assume that $C$ is not Hamiltonian, say

$$C = (v_1, v_2, \dots, v_k, v_1),$$

where $3 \leq k < n$. If $T$ contains a vertex $v$ that is adjacent to some vertex of $C$ and adjacent from some vertex of $C$, then there must be a vertex $v_i$ of $C$ that is adjacent to $v$ such that $v_{i+1}$ is adjacent from $v$. In this case,

$$C' = (v_1, v_2, \dots, v_i, v, v_{i+1}, \dots, v_k, v_1)$$

is a cycle whose length is greater than that of $C$, producing a contradiction.

Hence, every vertex of $T$ that is not on $C$ is either adjacent to every vertex of $C$ or adjacent from every vertex of $C$. Since $T$ is strong, there must be vertices of each type.

Let $U$ be the set of all vertices of $T$ that are not on $C$ and such that each vertex of $U$ is adjacent from every vertex of $C$, and let $W$ be the set of those vertices of $T$ that are not on $C$ such that every vertex of $W$ is adjacent to each vertex of $C$ (see Figure 7.20). Then $U \neq \emptyset$ and $W \neq \emptyset$.

![](img/598a6ae3fd44120830ada34717906f29_194_0.png)

Since $T$ is strong, there is a path from every vertex of $C$ to every vertex of $W$. Since no vertex of $C$ is adjacent to any vertex of $W$, there must be a vertex $u \in U$ that is adjacent to a vertex $w \in W$. However then,

$$C'' = (v_1, v_2, \dots, v_k, u, w, v_1)$$

is a cycle whose length is greater than the length of $C$, a contradiction.

If $T$ is a Hamiltonian tournament, then, of course, every vertex of $T$ lies on every Hamiltonian cycle of $T$. Actually, every vertex of $T$ lies on a triangle of $T$ as well.

**Theorem 7.27** *Every vertex in a nontrivial strong tournament belongs to a triangle.*

**Proof.** Let $v$ be a vertex in a nontrivial strong tournament $T$. By Theorem 7.26, $T$ is Hamiltonian. Thus, $T$ contains a Hamiltonian cycle $\langle v = v_1, v_2, \dots, v_n, v_1 \rangle$. Since $v$ is adjacent to $v_2$ and adjacent from $v_n$, there is a vertex $v_i$ with $2 \leq i < n$ such that $\langle v, v_i \rangle$ and $\langle v_{i+1}, v \rangle$ are arcs of $T$. Thus, $\langle v, v_i, v_{i+1}, v \rangle$ is a triangle of $T$ containing $v$.

This proves that if a tournament is Hamiltonian, then it must possess significantly stronger properties. A digraph $D$ of order $n \geq 3$ is **pancyclic** if it contains a cycle of every possible length, that is, $D$ contains a cycle
