
# 18.2 List Edge Colorings

## Cycle Double Covers

There is another concept and conjecture related to bridgeless graphs which ultimately returns us to snarks.

If $G$ is a connected bridgeless plane graph, then the boundary of every region is a cycle and every edge of $G$ lies on the boundaries of two regions. Thus, if $S$ is the set of cycles of $G$ that are the boundaries of the regions of $G$, then every edge of $G$ belongs to exactly two elements of $S$. For which other graphs $G$ is there a collection $S$ of cycles of $G$ such that every edge of $G$ belongs to exactly two cycles of $S$?

A **cycle double cover** of a graph $G$ is a set (actually a multiset) $S$ of not necessarily distinct cycles of $G$ such that every edge of $G$ belongs to exactly two cycles of $S$. Certainly, no cycle of $G$ can appear more than twice in $S$. Also, if $G$ contains a bridge $e$, then $e$ belongs to no cycle and $G$ contains no cycle double cover. If $G$ is Eulerian, then $G$ has a cycle decomposition $S'$. If $S$ is the set of cycles of $G$ that contains each cycle of $S'$ twice, then $S$ is a cycle double cover of $G$.

That every bridgeless graph has a cycle double cover was conjectured by Paul Seymour [219] in 1979. George Szekeres [229] conjectured this for cubic graphs even earlier – in 1973.

> **The Cycle Double Cover Conjecture** *Every nontrivial connected bridgeless graph has a cycle double cover.*

The following result of Bryant, Horsley and Petterson [39], obtained in 2015, may be considered as an analogue of Theorem 13.16.

> **Theorem 18.15** *For every $t$ integers $k_1, k_2, \dots, k_t$ and an integer $n \geq 3$ such that $3 \leq k_i \leq n$ for each $i$ $(1 \leq i \leq t)$ and $\sum_{i=1}^{t} k_i = 2\binom{n}{2}$, the complete graph $K_n$ has $t$ cycles $C_{k_1}, C_{k_2}, \dots, C_{k_t}$ such that every edge of $K_n$ belongs to exactly two of these cycles.*

As we have seen, the Cycle Double Cover Conjecture is true for all nontrivial connected bridgeless planar graphs and for all Eulerian graphs. Initially, it may seem apparent that this conjecture is true in general, if we were to replace each edge of a bridgeless graph $G$ by two parallel edges then the resulting multigraph $H$ is Eulerian. This implies that there is a set $S$ of cycles of $H$ such that each edge of $H$ belongs to exactly one cycle in $S$. This, in turn, implies that each edge of $G$ belongs to exactly two cycles in $S$, completing the proof. This argument is faulty, however, for one or more cycles of $H$ in $S$ may be 2-cycles, which do not correspond to cycles of $G$. Nevertheless, no counterexample to the Cycle Double Cover Conjecture is known. If the Cycle Double Cover Conjecture is false, then there exists a minimum counterexample, namely, a connected bridgeless graph of minimum size having no cycle double cover. François Jaeger (1947–1997) proved that a minimum counterexample to the Cycle Double Cover Conjecture must be a snark [135]. However, all known snarks possess a cycle double cover.

In Section 15.2 we considered the topic of list colorings. In a list coloring of a graph $G$ there is a list (or set) of available colors for each vertex of $G$, with the goal being to select a color from each list so that a proper vertex coloring of $G$ results. One of the major problems concerns the determination of the smallest positive integer $k$ such that every bridgeless graph has a nowhere-zero $k$-flow. In this connection, William Tutte [241] conjectured the following.

> **Conjecture 18.11** *Every bridgeless graph has a nowhere-zero 5-flow.*

While this conjecture is still open, Paul Seymour [220] did establish the following.

> **Theorem 18.12** *Every bridgeless graph has a nowhere-zero 6-flow.*

Tait colorings (introduced in Chapter 17) deal exclusively with cubic graphs, of course, and it is this class of graphs that has received added attention when studying nowhere-zero flows. By Theorem 18.1, no cubic graph has a nowhere-zero 2-flow. In the case of nowhere-zero 3-flows, it is quite easy to determine which cubic graphs have these.

> **Theorem 18.13** *A cubic graph G has a nowhere-zero 3-flow if and only if G is bipartite.*

**Proof.** Let $G$ be a cubic bipartite graph with partite sets $U$ and $W$. Since $G$ is regular, $G$ contains a 1-factor $F$. Orient the edges of $F$ from $U$ to $W$ and assign each the value 2. Orient all other edges of $G$ from $W$ to $U$ and assign each of these arcs the value 1. This is a nowhere-zero 3-flow.

For the converse, let $G$ be a cubic graph having a nowhere-zero 3-flow. By Theorem 18.3, there is an orientation $D$ on which is defined a nowhere-zero 3-flow having only the values 1 and 2. In particular, the values must be 1, 1, 2 for the three arcs incident with each vertex of $D$. The arcs having the value 2 form a subdigraph $H$ of $D$ and the underlying graph of $H$ is a 1-factor of $G$. Let $U$ be the set of vertices of $G$ where each vertex of $H$ has outdegree 1 in $H$ and let $W$ be the remaining vertices of $G$. Every arc of $D$ not in $H$ must then have a value of 1 and be directed from a vertex of $W$ to a vertex of $U$. Thus, $G$ is a bipartite graph with partite sets $U$ and $W$. ■

Those cubic graphs having a nowhere-zero 4-flow depend only on their chromatic index.

> **Theorem 18.14** *A cubic graph G has a nowhere-zero 4-flow if and only if G is of Class one.*

**Proof.** Let $G$ be a cubic graph that has a nowhere-zero 4-flow. By Theorem 18.3, there exists an orientation $D$ of $G$ and a nowhere-zero 4-flow $\phi$ on $D$ such that $\phi(e) \in \{1,2,3\}$ for each arc $e$ of $D$. Then each vertex is incident with arcs having either the values $1,\ 1,\ 2$ or $1,\ 2,\ 3$. In particular, each vertex of $D$ is incident with exactly one arc having the value 2. The arcs having the value 2 produce a 1-factor of $G$ and so the remaining arcs of $D$ produce a 2-factor of $G$. If the 2-factor is a Hamiltonian cycle of $G$, then $G$ is of Class one. Hence, we may assume that this 2-factor consists of two or more mutually disjoint cycles. Let $C$ be one of these cycles and let $H$ be the orientation of $C$ in $D$.

Suppose that $C$ is an $r$-cycle and let $S = V(C)$. Since each arc of $D$ joining a vertex of $S$ and a vertex of $V(D)-S$ has flow value 2 and since $\sigma^+(S,\phi) = \sigma^-(S,\phi)$ by Theorem 18.5, it follows that there is an even number $t$ of arcs joining the vertices of $S$ and the vertices of $V(D)-S$. Since this set of arcs is independent, it follows that $G[S]$ contains $t$ vertices of degree 2 and $r-t$ vertices of degree 3. Because $\phi[S]$ has an even number of odd vertices, $r-t$ is even. However, since $t$ is also even, $r$ is even as well and $C$ is an even cycle. Thus, the 2-factor of $G$ is the union of even cycles and so $G$ is of Class one.

We now verify the converse. Let $G$ be a cubic graph of Class one. Therefore, $G$ is 3-edge colorable and 1-factorable into factors $F_1,\ F_2,\ F_3$, where $F_i$ is the 1-factor $(1 \le i \le 3)$ whose edges are colored $i$. Every two of these three 1-factors produce a 2-factor consisting of a union of disjoint cycles. Since the edges of each cycle alternate in colors, the cycles are even and each 2-factor is bipartite. Let $G_1$ be the 2-factor obtained from $F_1$ and $F_2$, and $G_2$ the 2-factor obtained from $F_2$ and $F_3$. Now, let $D$ be an orientation of $G$ and let $D_i$ be the resulting orientation of $G_i$, $(i = 1,2)$. Since each component of each graph $G_i$ is Eulerian, it follows by Theorem 18.1 that there is a nowhere-zero 2-flow $\phi_i$ on $D_i$. For $e \in E(D) - E(D_3)$, define $\phi_i(e) = 0$ for $i = 1,2$. Then $\phi_1$ is a 2-flow on $D$. By Theorem 18.4, the function $\phi$ defined by $\phi = \phi_1 + 2\phi_2$ is also a flow on $D$. Because $\phi(e) \in \{\pm1,\pm2,\pm3\}$, it follows that $\phi$ is a nowhere-zero 4-flow on $D$.

Since the Petersen graph is a cubic graph that is of Class two, it follows by Theorem 18.14 that it does not have a nowhere-zero 4-flow (which we also saw in Theorem 18.9). We noted that the Petersen graph does have a nowhere-zero 5-flow. Of course, if Conjecture 18.11 is true, then every bridgeless graph has a nowhere-zero 5-flow.

important role among cubic graphs as Neil Robertson, Daniel Sanders, Paul Seymour and Robin Thomas verified in a series of papers [208, 210, 209, 214, 215].

> **Theorem 18.10** *Every bridgeless cubic graph not having the Petersen graph as a minor has a nowhere-zero 4-flow.*

