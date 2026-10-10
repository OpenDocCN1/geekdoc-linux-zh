$C_r$. Thus for some $i$, with $1 \leq i \leq k+1$, $K_{n_i}$ has a $K_6$ of color $C_r$. Thus the result holds also for $m = k+1$. This completes the proof.

*The least such number* M that satisfies the conditions of Theorem 16.10 is usually denoted by $R(n_1, n_2, \ldots, n_r)$ and is called the $(n_1, n_2, \ldots, n_r)$ *Ramsey number*. The only Ramsey number with $m \geq 3$ whose actual value is known is $R(3, 3, 3)$, which is 17 (see Exercise 16.3.1B).

As we have already noted, we could also generalize the above result by replacing the two-element subsets, that is, graph edges, by three-, four-, and one-element subsets of a given set. If we go in the other direction and consider one-element subsets of a set, that is, we color the elements of a set (rather than pairs, triples, quadruples, etc., of elements), we obtain Theorem 15.3, one of the generalizations of the pigeonhole principle. We therefore see that Ramsey theory is a vast generalization of Dirichlet’s pigeonhole principle.

# **Exercises**

+   16.3.1A a. Use the proof of Theorem 16.10 to show that for each positive integer $k$ and all positive integers $n_1, \ldots, n_k, n_{k+1}$, $R(n_1, \ldots, n_k, n_{k+1}) \leq R(R(n_1, \ldots, n_k), n_{k+1})$, and deduce that for all positive integers $p, q$, and $r$
+   
+   $$R(p, q, r) \leq \min\{R(R(p, q), r), R(R(p, r), q), R(R(q, r), p)\}.$$
+   
+   b. Prove that, for all positive integers $p, q, r \geq 2$,
+   
+   $$R(p, q, r) \leq R(p-1, q, r) + R(p, q-1, r) + R(p, q, r-1) - 1.$$

+   16.3.1B Suppose the edges of $K_{17}$ are colored using red, blue, or green. Let $v$ be a vertex of $K_{17}$. Show that
+   i. At least six of the edges with $v$ as endpoint must be of the same color (say red).
+   ii. Consider the subgraph whose vertices are six vertices joined to $v$ by red edges. Note that either this subgraph has at least one red edge, or all its edges are blue or green. Show that in the first case $K_{17}$ has a red triangle, and in the second either a green or a blue triangle.
+   iii. Deduce that $R(3, 3, 3) \leq 17$.

# 16.4 EUCLIDEAN RAMSEY THEORY

There are some fascinating Ramsey-type problems of a geometric nature. Here are some involving either coloring all points on the real line (or, if you prefer, the $x$-axis, or any other infinite straight line) or coloring all the points in the plane.

**PROBLEM 16.1** Suppose that, with each point on the real line, we associate either the color red or the color blue (loosely, “we color each point of the line red or blue”). Show that we can always find points $A$, $B$, $C$, on the line, all of the same color and with $B$ the midpoint of $AC$.