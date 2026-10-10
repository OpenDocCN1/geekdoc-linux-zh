# **DEFINITION 9.7**

+   i. Two vertices in a graph are said to be *connected* if there is a walk in the graph with the given vertices as its ends.
+   ii. A graph is said to be *connected* if each pair of vertices is connected.
+   iii. If a graph is not connected it can be split up into separate connected parts, which are called the *connected components* of the graph.

For example, in the graph of Figure 9.15, the pairs of vertices *a* and *b*, *a* and *c*, *b* and *c*; and *d* and *e* are connected, but none of *a*, *b*, and *c* is connected to either *d* or *e*. Since not all the pairs of vertices are connected, the graph is *not* connected. It has two connected components, one with vertex set {a,b,c} and edges *ab* and *bc*; and the other with vertex set {d,e} and edge *de*.

# **PROBLEM 9.9**

How many of the graphs with four vertices, as shown in Figure 9.9, are connected?

**Solution**

Six of these graphs are connected, namely, (v), (vi), (viii), (ix), (x), and (xi).

# *Exercises*

+   **9.4.1A** Prove that if *G* is a connected graph with *n* vertices and no closed paths, then *G* has *n*−1 edges.
+   
+   **9.4.1B** Prove that if *G* is a simple graph with *n* vertices such that, for all pairs of vertices *u*, *v* that are not joined by an edge, δ(*u*) + δ(*v*) ≥ *n*−1, then *G* is connected.
+   
+   **9.4.2A** Prove that, given a connected graph *G*, the removal of a particular edge results in a graph that is still connected if and only if the edge that is removed occurs in a closed path in *G*.
+   
+   **9.4.2B** Suppose that *G* is a connected graph with 16 edges in which each vertex has degree at least three. Find the maximum number of vertices it can have. Draw a picture of such a graph.
+   
+   **9.4.3A** Show that the Petersen graph has a closed path of length 6 but no closed path of length 7.
+   
+   **9.4.3B** Does the Petersen graph have a closed path of length 9? Does it have a closed path of length 8?

![](bbox=[0.35, 0.84, 0.6, 0.96])

FIGURE 9.15