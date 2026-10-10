+   b. Similarly, if G is semi-Eulerian, it has a trail that includes each edge exactly once.
+   It follows that G is connected, and every vertex, except possibly the first and last
+   vertices in the trail, has even degree.

We now come to the harder “if” part of the theorem. We prove by mathematical
induction on the number of edges that if G is a connected graph with more than one
vertex in which each vertex has even degree, then G is Eulerian. Such a graph must
have at least two edges if it is a multigraph and at least three edges if it is simple graph.
It is easy to see that a connected multigraph with two edges and a connected simple
graph with three edges must both be Eulerian. This provides the base for the proof by
induction.

Now suppose that the result is true for all graphs with fewer than k edges and
that G is a connected graph with k edges, with k ≥ 3, in which each vertex has even
degree. So each vertex has degree at least 2 and hence, by Theorem 9.5, G has a closed
path, say C.

If C includes all of the edges of G, our proof is complete. If not, then we continue the
proof by first removing from G the edges (but none of the vertices) included in C. This
produces a new graph, which may not be connected but in which each vertex still has
even degree, since by deleting the edges in C we remove two edges adjacent to each
vertex that occurs in C. The new graph has fewer than k edges, and so by our induction
hypothesis each connected part of this graph has a closed trail involving all its edges. Let
these closed trails be T₁, T₂, ..., Tₑ. Thus between them these closed trails together with the
closed path C include all the edges of G. Since G is connected, each of the closed trails
has at least one vertex that also occurs in C. It follows that we can obtain a closed trail
that includes all the edges of G by following the closed path C and, for 1 ≤ i ≤ n, the first
time we come to a vertex that also occurs in Tₐ, going round this trail before continuing
around G.

This completes the proof of the “if” part of (a). The “if” part of (b) can easily be
deduced from this. We ask you to do this in Exercise 9.6.2A. We have deliberately not
included a diagram to illustrate this proof, but you are strongly encouraged to draw
your own diagrams to help you to understand the proof.

Euler’s paper also contains some useful mathematical advice. He observes that one
could solve the Königsberg problem merely by trying all cases. He dismisses this as
“too difficult and laborious.” (And, he might have added, such a trial by cases would not
expose the real reason why the same result is true in general.) He also says (essentially),
“Before I attempt to solve the problem I shall try to determine if it can be solved, for if
it can’t, then attempts to find a solution would be a waste of time.”

Euler’s theorem could be of some interest to people who deliver the mail, or news-
papers, and to street cleaners, indeed everyone whose job requires them to visit a
number of streets in a certain area. It can tell them, in advance, if it is possible to
avoid traveling down any street more than once before returning to base: Namely, if
there is a point at which an odd number of streets meet, then Euler’s theorem tells
you that they will be wasting their time trying to discover such a route. If you are
delivering the mail or newspapers, you may need to deliver to both sides of a street,
and this involves walking along the street twice. This corresponds to connecting the