to check that no such path of length 4 exists. Similarly, we can rule out the use of the edges $\{c, h\}$, $\{d, i\}$, and $\{e, j\}$. Therefore there is no closed path of length 7.

**9.4.4A** Let $G = (V, E)$ be a simple graph with $n$ vertices that is not connected. Select a vertex $v_0$ of $G$. Let $V_1$ be the set of vertices consisting of $v_0$ together with all the vertices connected to $v_0$ by an edge, and let $V_r = V \setminus V_1$. Let $\#(V_r) = r$. Then $\#(V_r) = n - r$. Since $G$ is not connected, $1 \leq r < n$. There are no edges joining a vertex in $V_1$ to a vertex in $V_r$. So the maximum number edges $G$ can have is the number of edges joining each pair of vertices in $V_1$ plus the number of edges joining each pair of vertices in $V_r$. So $G$ has at most $e_r$ edges, where $e_r = \frac{1}{2} r(r - 1) + \frac{1}{2} (n - r)(n - r - 1)$ edges. Now $e_r = \frac{1}{2} n^2 - \frac{1}{2} n + r + (r - \frac{1}{2}n)^2$. It follows that for $1 \leq r < n$, $e_r$ achieves a maximum value when $|r - \frac{1}{2}n|$ is as large as possible, that is, for $r = 1$ and $r = n - 1$. It follows that $e_r \leq \frac{1}{2} (n - 1)(n - 2)$. Therefore, if $G$ has $\frac{1}{2} (n - 1)(n - 2) + 1$ edges, then $G$ must be connected.

+   **9.4.5** a. The following algorithm applied to a graph $G = (V, E)$ determines whether the graph is connected.

> **ALGORITHM FOR DECIDING WHETHER A GRAPH G = (V,E) IS CONNECTED**
> 
> 1. Choose a vertex $v \in V$ and put $i = 0$ and $V_0 = \{v\}$
> 2. Let $V_{i+1}$ be the set of those vertices in $V \setminus \bigcup_{j=0}^{i} V_j$ that are joined to a vertex in $V_i$.
> 3. If $V_{i+1} = \emptyset$, stop. Otherwise replace $i$ by $i + 1$, and return to step 1.
> If, when the algorithm terminates, $i = k$ and $V = \bigcup_{j=0}^{k} V_j$, the graph is connected; otherwise, the graph is not connected.

It is easy to see that when the algorithm terminates, $\bigcup_{j=0}^{k} V_j$ is the set of vertices connected to $v$ by a path, and hence the graph is connected if and only if $\bigcup_{j=0}^{k} V_j$ is the set of all the vertices of $G$.

b. We apply the algorithm of (a) to each graph in turn.

i.  | $i$ | $V_i$ |
|---|---|
| 0 | $\{a\}$ | $V_1 \cup V_2 \cup V_3 \neq V$, and so the graph is not connected. |
| 1 | $\{d, e, f\}$ |
| 2 | $\emptyset$ |
| | |
| | |
| 0 | $\{a\}$ |
| 1 | $\{b, c, d, e, f\}$ | $V_0 \cup V_1 \cup V_2 = V_3 = V$, and so the graph is connected. |
| 2 | $\{g, h\}$ |
| 3 | $\emptyset$ |