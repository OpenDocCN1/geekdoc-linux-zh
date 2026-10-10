problem is to find a trail using each edge exactly once. Euler noted that in following such a trail, for each vertex other than the first and last vertices, we would have to reach the vertex along one edge and leave along another. Hence such a trail would use an even number of edges adjacent to each of these vertices. Therefore, as it would use each edge exactly once, the degrees of these vertices much be even numbers. However, we see in the graph of Figure 9.31 that there are more than two vertices with odd degrees. So the graph has no trail containing each edge exactly once. Hence the answer to Problem 9.11 is no.

Euler's argument, as applied to the particular graph of Figure 9.31, is not difficult, and it is hard to believe that it had not previously occurred to some smart citizen of Königsberg. Euler's real contribution was to realize that his argument applied in general, and also that his necessary condition for the existence of a trail using each edge once is also sufficient. This we now explain.

We first introduce some terminology, for graphs where there is a closed trail using each edge once, and for those where there is such a trail that need not be closed. These graphs are named in honor of Euler. We again remind you that here by “graph” we mean both simple graphs and multigraphs.

# DEFINITION 9.10

A graph that is connected and has a trail that includes each of its edges is said to be *semi-Eulerian*. It is said to be *Eulerian* if it is connected and has a closed trail including each edge. We specify that the graph consisting of just one vertex and no edges is not Eulerian.

# THEOREM 9.9
(EULER 1735*)

+   a.  If $G$ is a graph with more than one vertex, then $G$ is Eulerian if and only if $G$ is a connected graph in which the degree of each vertex is an even number.
+   b.  If $G$ is a graph with more than one vertex, then $G$ is semi-Eulerian if and only if $G$ is a connected graph in which there are at most two vertices whose degrees are odd numbers.

# Proof

As we have already seen, the “only if” parts of this theorem are straightforward.

+   a.  If $G$ is Eulerian there is a closed trail containing each edge exactly once, and hence in which each vertex occurs. So there is a trail and hence a path connecting each pair of vertices. So $G$ is connected. If a vertex, say $a$, occurs $k$ times in the closed trail, there must be $2k$ edges adjacent to $a$ (namely, $k$ “in” edges and $k$ “out” edges) and so $a$ has even degree.

* Euler stated only the “if” part of his theorem. The first published proof is attributed to C. Hierholzer, Über die Möglichkeit einen Linienzug ohne Wiederholung und ohne Unterbrechung zu umfahren, *Mathematische Annalen*, 6, 1873, pp. 30–32. Hierholzer, who lived a short life (1840–1871), died before his paper was published.