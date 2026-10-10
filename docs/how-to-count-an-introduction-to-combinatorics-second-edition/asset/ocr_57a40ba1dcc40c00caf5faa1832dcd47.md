# **THEOREM 9.1**

If the graph $G_1=(V_1,E_1)$ is isomorphic to the graph $G_2=(V_2,E_2)$, then $#(V_1)=#(V_2)$ and $#(E_1)=#(E_2).$

We have already used Theorem 9.1 in Problem 9.3 to show that graphs with different numbers of edges are not isomorphic. Of course, the converse of Theorem 9.1 is not true. For example, the graphs (i) and (ii) of Figure 9.5 are not isomorphic even though they are both graphs with four vertices and three edges.

Up to now we have relied on geometric pictures to justify this last statement, but we now introduce an important idea that enables us to make the argument more precise.

# **DEFINITION 9.4**

We say that the edge $\{a,b\}$ of a graph is *adjacent* to the vertex $v$ if either $v=a$ or $v=b$. The *degree* of a vertex $v$ is the number of edges that are adjacent to $v$. We use $\delta(v)$ for the degree of the vertex $v$. We also say that the vertices $a$ and $b$ are *adjacent* if $\{a,b\}$ is an edge.

In terms of pictures, the degree of a vertex is just the number of edges that meet at the vertex. If a graph has $n$ vertices, each vertex can be joined to all, some, or none of the other $n-1$ vertices, so the degree of a vertex $v$ in a graph with $n$ vertices is an integer, $\delta(v)$, in the range $0\leq\delta(v)\leq n-1$. (In a multigraph where multiple edges and loops are allowed there are no restrictions on the degrees of individual vertices.) Note that a minority of authors uses *valence* instead of *degree*.

# **PROBLEM 9.4**

Calculate the degrees of the vertices of the graphs pictured in Figure 9.5.

# **Solution**

(i)
| v | δ(v) |
|---|---|
| e | 1 |
| f | 3 |
| g | 1 |
| h | 1 |

(ii)
| v | δ(v) |
|---|---|
| i | 1 |
| j | 2 |
| k | 2 |
| l | 1 |

(iii)
| v | δ(v) |
|---|---|
| m | 2 |
| n | 1 |
| p | 2 |
| q | 1 |

(iv)
| v | δ(v) |
|---|---|
| r | 2 |
| s | 3 |
| t | 1 |
| u | 2 |

(v)
| v | δ(v) |
|---|---|
| v | 3 |
| w | 3 |
| x | 3 |
| y | 3 |

Because of the way an isomorphism between graphs matches the vertices and the edges of two graphs, in the following theorem the first statement is evident, and the second is an immediate consequence.

# **THEOREM 9.2**

+   a. If $\phi: V_1 \to V_2$ is an isomorphism between the graphs $G_1=(V_1,E_1)$ and $G_2=(V_2,E_2)$, then for each $v\in V_1$, $\delta(v)=\delta(\phi(v))$.
+   b. If two graphs are isomorphic, they have the same number of vertices of each degree.