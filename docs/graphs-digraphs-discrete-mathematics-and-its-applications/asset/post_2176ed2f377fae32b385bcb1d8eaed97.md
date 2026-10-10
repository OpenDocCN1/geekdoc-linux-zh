
In this case, $D_\Delta(\Gamma)$ is the complete symmetric digraph $K_n^*$ and so Aut($D_\Delta(\Gamma)$) is the symmetric group $S_n$. Since every permutation of the elements of $\Gamma$ is an automorphism of $D_\Delta(\Gamma)$, the permutation $\alpha = \langle g_1 \ g_2 \ g_4 \rangle$ is an automorphism. Hence, $\alpha$ maps the arc $\langle g_1, g_2 \rangle$ into the arc $\langle g_2, g_4 \rangle$. Since the color of $\langle g_1, g_2 \rangle$ is $a$ and the color of $\langle g_2, g_4 \rangle$ is $a^2$, it follows that $\alpha$ is not color-preserving. In this case, the subgroup of color-preserving automorphisms of $D_\Delta(\Gamma)$ consists of $\epsilon, \langle g_1 \ g_2 \ g_3 \ g_4 \rangle, \ \langle g_1 \ g_3 \rangle \langle g_2 \ g_4 \rangle, \ \langle g_1 \ g_4 \ g_3 \ g_2 \rangle,$ which is a cyclic group of order 4 and is, therefore, isomorphic to the group $\Gamma$. We are about to see that this is no coincidence.

![](img/598a6ae3fd44120830ada34717906f29_237_0.png)

A useful characterization of color-preserving automorphisms is given in the next result (see Exercise 14).

> **Theorem 9.4** *Let* $\Gamma$ *be a nontrivial finite group with generating set* $\Delta$ *and let* $\alpha$ *be a permutation of* $V(D_\Delta(\Gamma))$. *Then* $\alpha$ *is a color-preserving automorphism of* $D_\Delta(\Gamma)$ *if and only if* $\alpha(gh) = (\alpha(g))h$ *for every* $g \in \Gamma$ *and* $h \in \Delta$.

With the aid of Theorem 9.4, we can now prove the following result.

> **Theorem 9.5** *Let* $\Gamma$ *be a nontrivial finite group with generating set* $\Delta$. *Then the group of color-preserving automorphisms of* $D_\Delta(\Gamma)$ *is isomorphic to* $\Gamma$.

**Proof.** Let $\Gamma = \langle g_1, g_2, \dots, g_n \rangle$. For $i = 1, 2, \dots, n$, define $\alpha_i : V(D_\Delta(\Gamma)) \to V(D_\Delta(\Gamma))$ by $\alpha_i(g_s) = g_i g_s$ for $1 \leq s \leq n$. Since $\Gamma$ is a group, the mapping $\alpha_i$ is one-to-one and onto. Let $h \in \Delta$. Then for each $i$ ($1 \leq i \leq n$) and for each $s$ ($1 \leq s \leq n$), $\alpha_i(g_i h) = g_i (g_i h) = (g_i g_i)h = (\alpha_i(g_i))h.$ Hence, by Theorem 9.4, $\alpha_i$ is a color-preserving automorphism of $D_\Delta(\Gamma)$.

Let $\alpha$ be an arbitrary color-preserving automorphism of $D_\Delta(\Gamma)$ and let $g_1$ be the identity of $\Gamma$. Suppose that $\alpha(g_1) = g_s$, let $g_s \in \Gamma$. The element $g_s$ of $\Gamma$ can be expressed as a product of generators, say $g_s = h_1h_2 \cdots h_t$, where $h_j \in \Delta$ and $1 \leq j \leq t$. Therefore,

$\begin{array}{rl} \alpha(g_s) & = \alpha(g_1h_1h_2 \cdots h_t) = \alpha(g_1h_1h_2 \cdots h_{t-1})h_t \\ & = \alpha(g_1h_1 \cdots h_{t-2})h_{t-1}h_t = \cdots = \alpha(g_1)h_1h_2 \cdots h_t = g_sg_s. \end{array}$

Thus, $\alpha = \alpha_r$.

We now show that the mapping $\phi$ defined by $\phi(g_i) = \alpha_i$ is an isomorphism from $\Gamma$ to the group of color-preserving automorphisms of $D_\Delta(\Gamma)$. The mapping $\phi$ is already one-to-one and onto. It remains to show that $\phi$ is operation-preserving, namely that $\phi(g_ig_j) = \phi(g_i)\phi(g_j)$ for $g_i, g_j \in \Gamma$. Let $g_ig_j = g_k$. Then $\phi(g_ig_j) = \phi(g_k) = \alpha_k$ and $\phi(g_i)\phi(g_j) = \alpha_i\alpha_j$. Now,

$\alpha_k(g_s) = g_kg_s = (g_ig_j)g_s = g_i(g_jg_s) = \alpha_i(g_jg_s) = \alpha_i(\alpha_j(g_s)) = (\alpha_i\alpha_j)g_s$

and so $\alpha_k = \alpha_i\alpha_j$. $\square$

## Frucht’s Theorem

In the early years of the 20th century, Germany had been known for its mathematicians who excelled in group theory. One of these was Issai Schur. While at the University of Berlin, Schur supervised several doctoral students. One of Schur’s students was Roberto Frucht (1906–1997), who received his Ph.D. in 1930 in the area of group theory.

Finding a job as a mathematician in Germany was very difficult during those days. Frucht wasn’t even able to be hired as a high school teacher since Frucht was a Czechoslovakian citizen and German citizenship was required. So, Frucht moved to Italy to work for an insurance company. Frucht stayed there until 1938. During the time he was in Italy, he had essentially become mathematically inactive. However, one day in 1936, he received a catalogue advertising a book on graph theory, the first book written exclusively on graph theory. Frucht ordered this book and became an enthusiastic graph theorist the very day that the book arrived.

On page 5 of the first section (Basic Concepts) of the first chapter (Foundations) of this book, the author Dénes König [148, p. 5] wrote (translated into English):

> When can a given abstract group be interpreted as the group of a graph and if this is the case, how can the corresponding graph be constructed?

König’s question on automorphism groups immediately caught Frucht’s attention. After several months of unsuccessfully trying to solve the problem, he found a solution that seemed rather easy (after he had found it). Frucht [97] proved that every finite group has this property. We are now in a position to describe Frucht’s proof of this result.

If $\Gamma$ is the trivial group, then for $G = K_1$, we have Aut($G$) $\cong \Gamma$. Therefore, we may assume that $\Gamma$ is nontrivial and so $\Gamma = \{g_1, g_2, \dots, g_n\}$ where $n \ge 2$. Let $\Delta = \{h_1, h_2, \dots, h_l\}$, $1 \le t \le n$, be a generating set for $\Gamma$. We first construct the Cayley color graph $D_\Delta(\Gamma)$ of $\Gamma$ with respect to $\Delta$, which, recall, is actually a digraph. By Theorem 9.5, the group of color-preserving automorphisms of $D_\Delta(\Gamma)$ is isomorphic to $\Gamma$. We now transform the digraph $D_\Delta(\Gamma)$ into a graph $G$ by the following technique. Let $(g_i, g_j)$ be an arc of $D_\Delta(\Gamma)$ colored $h_k$. Delete this arc and replace it by the graphical path $g_i, u^t_{ij}, u^b_{ij}, g_j$. At the vertex $u^b_{ij}$ we construct a new path $P^t_{ij}$ of length $2k - 1$ and at the vertex $u^b_{ij}$ we construct a path $P^b_{ij}$ of length $2k$. This construction is now performed for every arc of $D_\Delta(\Gamma)$. This is illustrated in Figure 9.12 for $k = 1,2,3$.

![](img/598a6ae3fd44120830ada34717906f29_239_0.png)

Figure 9.12: Constructing a graph G from a given group $\Gamma$

The addition of the paths $P_{ij}$ and $P^t_{ij}$ in the formation of $G$ is equivalent, in a sense, to assigning a direction and a color to each arc in the construction of $D_\Delta(\Gamma)$. Observing that every color-preserving automorphism of $D_\Delta(\Gamma)$ induces an automorphism of $G$, and conversely, results in a proof of Frucht’s theorem.

## Theorem 9.6 (Frucht’s Theorem)

For every finite group $\Gamma$, there exists a graph $G$ such that Aut($G$) $\cong \Gamma$.

The condition of having a given group prescribed is not a particularly stringent one for graphs. For example, Herbert Lubicki [133] showed that for every finite group $\Gamma$ and integer $r \ge 3$, there exists an $r$-regular graph $G$ with Aut($G$) $\cong \Gamma$.

## Caley Graphs

We have now seen that for every finite group $\Gamma$ and generating set $\Delta$, there is an associated digraph, namely the Cayley color graph $D_\Delta(\Gamma)$. The underlying graph of a Cayley color graph $D_\Delta(\Gamma)$ is called a **Cayley graph** and is denoted by $G_\Delta(\Gamma)$. Thus, a graph $G$ is a Cayley graph if and only if there exists a finite group $\Gamma$ and a generating set $\Delta$ for $\Gamma$ such that $G \cong G_\Delta(\Gamma)$; that is, the vertices of $G$ are the elements of $\Gamma$ and two vertices $g_1$ and $g_2$ of $G$ are adjacent if and only if either $g_1 = g_2h$ or $g_2 = g_1h$ for some $h \in \Delta$.

As observed earlier, the complete symmetric digraph $K_n^*$ is a Cayley color graph; consequently, every complete graph is a Cayley graph. Since $K_2 \square K_3$ is the underlying graph of the Cayley color graph of Figure 9.10, $K_2 \square K_3$ is also a Cayley graph. Every Cayley graph is necessarily regular. Indeed, every Cayley graph is vertex-transitive. The converse is not true, however. The Petersen graph (Figure 9.8), for example, is vertex-transitive but it is not a Cayley graph.

## 9.3 The Reconstruction Problem

If $\phi$ is an automorphism of a nontrivial graph $G$ and $u$ is a vertex of $G$, then $G - u \cong G - \phi(u)$, that is, if $u$ and $v$ are similar vertices of a graph $G$, then $G - u \cong G - v$. The converse of this statement is not true, however. Indeed, the vertices $u$ and $v$ of the graph $G$ of Figure 9.13 are not similar; yet $G - u \cong G - v$.

![](img/598a6ae3fd44120830ada34717906f29_240_0.png)

This comment brings up a question. Suppose that $G$ and $H$ are two graphs of the same order with $V(G) = \{v_1, v_2,\dots, v_n\}$ and $V(H) = \{u_1, u_2,\dots, u_n\}$, say. If it should occur that $G - v_1 \cong H - u_1$, then this does not imply that $G \cong H$. But what if, in addition to having $G - v_1 \cong H - u_1$, we also know that $G - v_2 \cong H - u_2$, $G - v_3 \cong H - u_3$ and so on, up to $G - v_n \cong H - u_n$? Can we then conclude that $G \cong H$?
