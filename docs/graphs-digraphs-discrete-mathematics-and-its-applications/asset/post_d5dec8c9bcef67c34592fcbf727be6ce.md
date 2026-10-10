
## 17.2. CLASS ONE AND CLASS TWO GRAPHS

![](img/598a6ae3fd44120830ada34717906f29_477_0.png)

Day 1: AB-CE, AC-BD, AE-BC, AD-BE
Day 2: AB-CD, AC-BE, AE-BD, BC-DE
Day 3: AB-DE, AD-BC, AE-CD, BD-CE
Day 4: AC-DE, AD-CE, BC-CD

Figure 17.9: The Petersen graph $G$ in Example 17.11 and a 4-edge coloring of $G$

A subgraph $H$ of odd order $n'$ and size $m'$ of a graph $G$ is an **overfull subgraph** of $G$ if

$m' > \lfloor \frac{n'}{2} \rfloor \Delta(G)$.

Actually, if $H$ is an overfull subgraph of $G$, then $\Delta(H) = \Delta(G)$ (see Exercise 16). This says that $H$ is itself of Class two. Not only is an overfull subgraph of a graph $G$ of Class two, $G$ itself is of Class two.

**Theorem 17.12** Every graph having an overfull subgraph is of Class two.

**Proof.** Let $H$ be an overfull subgraph of a graph $G$. As we noted, $\Delta(H) = \Delta(G)$ and $H$ is Class two; so $\chi'(H) = 1 + \Delta(H)$. Thus,

$\chi'(G) \geq \chi'(H) = 1 + \Delta(H) = 1 + \Delta(G)$

and so $\chi'(G) = 1 + \Delta(G)$.

In the definition of an overfull subgraph $H$ of order $n'$ and size $m'$ in a graph $G$, we have $m' > \lfloor \frac{n'-1}{2} \rfloor \Delta(G)$. As we saw in Theorem 17.12, this implies that $G$ is of Class two. On the other hand, if $G$ should contain a subgraph $H$ of order $n'$ and size $m'$ such that $m' > \lfloor \frac{n'-1}{2} \rfloor \Delta(H)$, where $\Delta(H) < \Delta(G)$, then $H$ is an overfull graph and so $H$ is of Class two. This need not imply that $G$ is of Class two, however. For example, $C_5 \subset K_6$ is of Class one but $C_5$ is of Class two.

While every graph containing an overfull subgraph must be of Class two, a graph can be of Class two without containing any overfull subgraph. The Petersen graph $P$ (which is 3-regular of order 10) contains no overfull subgraph; yet we saw that $P$ is of Class two.

The following result provides a useful property of overfull subgraphs of a graph.

**Theorem 17.13** *Let $G$ be an $r$-regular graph of even order $n = 2k$, where $\{V_1, V_2\}$ is a partition of $V(G)$ such that $|V_1| = n_1$ and $|V_2| = n_2$ are odd. If $G_1 = G[V_1]$ is an overfull subgraph of $G$, then $G_2 = G[V_2]$ is also an overfull subgraph of $G$. Furthermore, if $k$ is odd, then $r < k$; while if $k$ is even, then $r < k - 1$.*

**Proof.** Let the size of $G_i$ be $m_i$ for $i = 1, 2$ and let $m'$ denote the number of edges in the set $[V_1, V_2]$. Thus,

$rn_1 = 2m_1 + m'$ and $rn_2 = 2m_2 + m'$.

Since $G_1$ is overfull, $m_1 > \frac{n_1-1}{2}r$. We show that $m_2 > \frac{n_2-1}{2}r$. Now,

$m_2 = \frac{rn_2 - m'}{2} = \frac{r(n - n_1) - (rn_1 - 2m_1)}{2} = \frac{rn}{2} - rn_1 + m_1$.

Since $2m_1 > rn_1 - r$, it follows that

$2m_2 = rn - 2rn_1 + 2m_1 > rn - 2rn_1 + rn_1 - r = r(n - n_1 - 1) = r(n_2 - 1)$.

Hence, $m_2 > \frac{n_2-1}{2}r$ and $G_2$ is overfull. Therefore, both $G_1$ and $G_2$ are overfull.

Now, either $n_1 \leq k$ or $n_2 \leq k$, say the former. If $k$ is even, then $n_1 \leq k - 1$. Since $G_1$ is overfull,

$m_1 > \frac{n_1-1}{2}r$ and so $2m_1 > (n_1 - 1)r$.

Since the size $m_1$ of $G_1$ is at most $\binom{n_1}{2}$, it follows that

$2\binom{n_1}{2} \geq 2m_1 > (n_1 - 1)r$ and so $n_1(n_1 - 1) > (n_1 - 1)r$.

Consequently, $r < n_1 \leq k - 1$ and so $r < k - 1$. If $k$ is odd, then $r < k$.

### The Overfull Conjecture

Amanda G. Chetwynd and Anthony J. W. Hilton [52] conjectured that the only way that a graph $G$ with sufficiently large minimum degree can be of Class two is for $G$ to contain an overfull subgraph.

**The Overfull Conjecture** *Let $G$ be a graph of order $n$ such that $\Delta(G) > n/3$. Then $G$ is of Class two if and only if $G$ contains an overfull subgraph.*

Let $v$ be a vertex of the Petersen graph $P$. Then $P-v$ has order $n=9$ and $\Delta(P-v)=\frac{n}{3}=3$. Even though $P-v$ is Class two, it has no overfull subgraph. Hence, if the Overfull Conjecture is true, the resulting theorem cannot be improved in general.

We encountered the following conjecture in Chapter 13.

**The 1-Factorization Conjecture** If $G$ is an $r$-regular graph of even order $n$ such that $(1) \ r \geq n/2$ if $n \equiv 2 \pmod{4}$ or $(2) \ r \geq (n-2)/2$ if $n \equiv 0 \pmod{4}$, then $G$ is 1-factorable.

In Theorem 13.3, we saw that this conjecture is true for sufficiently large even integers $n$. This theorem is restated below, this time in terms of edge colorings.

**Theorem 17.14** If $G$ is an $r$-regular graph of sufficiently large even order $n$ such that $(1) \ r \geq n/2$ if $n \equiv 2 \pmod{4}$ or $(2) \ r \geq (n-2)/2$ if $n \equiv 0 \pmod{4}$, then $G$ is of Class one.

If the Overfull Conjecture is true, then the 1-Factorization Conjecture is true for *all* positive even integers $n$.

**Theorem 17.15** If the Overfull Conjecture is true, then so too is the 1-Factorization Conjecture.

**Proof.** Assume, to the contrary, that the Overfull Conjecture is true but the 1-Factorization Conjecture is false. Then either (1) there exists an $r$-regular graph $G$ of order $n$ where $n \equiv 2 \pmod{4}$ and $r \geq n/2$ such that $G$ is not 1-factorable or (2) there exists an $r$-regular graph $G$ of order $n$ where $n \equiv 0 \pmod{4}$ and $r \geq (n-2)/2$ such that $G$ is not 1-factorable. Thus, $G$ is of Class two. Since $\Delta(G)>n/3$, it follows by the Overfull Conjecture that $G$ contains an overfull subgraph $G_1$.

Let $G_2$ be the subgraph of $G$ induced by $V(G)-V(G_1)$. By Theorem 17.13, $G_2$ is also overfull. At least one of $G_1$ and $G_2$ has order at most $n/2$. Suppose $G_1$ has order at most $n/2$. Again, by Theorem 17.13, if $n/2$ is odd, then $r < n/2$; while if $n/2$ is even, then $r < (n/2)-1$. Since $(1) \ r \geq n/2$ if $n/2$ is odd and $(2) \ r \geq (n-2)/2$ if $n/2$ is even, a contradiction is produced. $\blacksquare$

## 17.3 Tait Colorings

His attempted proofs contained an interesting and useful idea. Tait's idea was to consider coloring the boundary lines of cubic maps. In fact, he stated as a lemma that:

> *The boundary lines of every cubic map can always be colored with three colors so that the three lines at each meeting point are colored differently.*

Tait also mentioned that this lemma could be easily proved and showed how the lemma could be used to prove the Four Color Theorem. Although Tait was correct that this lemma could be used to prove the Four Color Theorem, he was incorrect when he said that the lemma could be easily proved. Indeed, as it turned out, this lemma is equivalent to the Four Color Theorem [232] and, of course, was equally difficult to prove.

### Tait's Theorem

In the proof of the following theorem, we use the so-called Klein four-group which is the direct product $\mathbb{Z}_2 \times \mathbb{Z}_2$ of two copies of the cyclic group of order 2.

**Theorem 17.16 (Tait's Theorem)** *A bridgeless cubic plane graph $G$ is 4-region colorable if and only if $G$ is 3-edge colorable.*

**Proof.** Suppose first that $G$ is 4-region colorable. Let a 4-region coloring of $G$ be given, where the colors are the four elements of $\mathbb{Z}_2 \times \mathbb{Z}_2$. Thus, each color can be expressed as $(a, b)$ or $ab$, where $a, b \in \{0, 1\}$. The four colors used are then $c_0 = 00$, $c_1 = 01$, $c_2 = 10$ and $c_3 = 11$. Addition of colors is defined as coordinate-wise addition in $\mathbb{Z}_2$. For example, $c_1 + c_3 = 01 + 11 = 10 = c_2$. Since every element of $\mathbb{Z}_2 \times \mathbb{Z}_2$ is self-inverse, the sum of two distinct elements of $\mathbb{Z}_2 \times \mathbb{Z}_2$ is never $c_0 = 00$.

We now define an edge coloring of $G$. Since $G$ is bridgeless, each edge $e$ lies on the boundary of two distinct regions. Define the color of $e$ as the sum of the colors of the two regions having $e$ on their boundary. Thus, no edge of $G$ is assigned the color $c_0$ and a 3-edge coloring of $G$ is produced. It remains to show that this 3-edge coloring is proper. Let $e_1$ and $e_2$ be two adjacent edges of $G$ and let $v$ be the vertex incident with $e_1$ and $e_2$. Then $v$ is incident with a third edge $e_3$ as well. For $1 \leq i < j \leq 3$, suppose that $e_i$ and $e_j$ are on the boundary of the region $R_{ij}$. Since the colors of $R_{13}$ and $R_{23}$ are different, the sum of the colors of $R_{13}$ and $R_{23}$ and the sum of the colors of $R_{12}$ and $R_{23}$ are different and so this 3-edge coloring is proper.

We now turn to the converse. Suppose that $G$ is 3-edge colorable. Let a 3-edge coloring of $G$ be given using the colors $c_1 = 01$, $c_2 = 10$ and $c_3 = 11$, as described above. This produces a partition of $E(G)$ into three perfect matchings $E_1$, $E_2$ and $E_3$, where $E_i$ ($1 \leq i \leq 3$) is the set of edges colored $c_i$.
