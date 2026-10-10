vertex has degree 2 must be Hamiltonian as it must consist of $n$ vertices in a single path. For each $n \geq 3$ there is a Hamiltonian graph with $n$ vertices and only $n$ edges. At the other extreme, for $n \geq 3$ the complete graph, $K_n$, is Hamiltonian as we can follow a path through each vertex in any order we like. These examples indicate that there cannot be a straightforward condition in terms of the number of edges or the degrees of the vertices for a graph to be Hamiltonian.

Also, there is no relationship between a graph being Eulertian and its being Hamiltonian, as the following problem shows.

# **PROBLEM 9.12**

Give examples of simple graphs that are

+   a. Eulertian and Hamiltonian
+       b. Eulertian but not Hamiltonian
+   c. Hamiltonian but not Eulerian    d. Neither Eulertian nor Hamiltonian
+       but with more than one vetex

# Solution

See Figure 9.36. There are, of course, lots of possible solutions. We have given examples with the smallest possible number of vertices and, for this number of vertices, the smallest number of edges.

We content ourselves with just one theorem, which gives a straightforward sufficient condition for a graph to be Hamiltonian.

# **THEOREM 9.10**

**(ORE 1960***)

If $G$ is a simple graph with $n$ vertices with $n \geq 3$, such that for each pair of vertices $u$, $v$ not joined by an edge, $\delta(u) + \delta(v) \geq n$, then $G$ is Hamiltonian.

# **Proof**

Suppose that $G$ satisfies the condition of the theorem but is not Hamiltonian. Since the complete graph $K_n$ is Hamiltonian, we may assume that $G$ is not complete. However, adding to $G$ one “missing” edge at a time, we shall eventually reach a graph, $G_1$, say, such that $G_1$ is not Hamiltonian and yet adding one more edge, say $\{x, y\}$, to $G_1$ makes

![](bbox=[0.2, 0.67, 0.8, 0.86])

O. Ore, Note on Hamiltonian Circuits, *American Mathematical Monthly*, 67, 1960, p. 55.