# 10.1. THE EULER IDENTITY

![](bbox=[0.08, 0.11, 0.9, 0.37])

**Theorem 10.1 (The Euler Identity)** For every connected plane graph of order $n$, size $m$ and having $r$ regions,

> $n - m + r = 2$.

**Proof.** We proceed by induction on the size $m$ of a connected plane graph. There is only one connected graph of size 0, namely $K_1$. In this case, $n = 1$, $m = 0$ and $r = 1$. Since $n - m + r = 2$, the base case of the induction holds.

Assume for a positive integer $m$ that if $H$ is a connected plane graph of order $n'$ and size $m'$, where $m' < m$ such that there are $r'$ regions, then $n' - m' + r' = 2$. Let $G$ be a connected plane graph of order $n$ and size $m$ with $r$ regions. We consider two cases.

+   * Case 1. $G$ is a tree. In this case, $m = n - 1$ and $r = 1$. Thus $n - m + r = n - (n - 1) + 1 = 2$, producing the desired result.

+   * Case 2. $G$ is not a tree. Since $G$ is connected and is not a tree, it follows by Theorem 3.10 that $G$ contains an edge $e$ that is not a bridge. In $G$, the edge $e$ is on the boundaries of two regions. So in $G - e$ these two regions merge into a single region. Since $G - e$ has order $n$, size $m - 1$ and $r - 1$ regions and $m - 1 < m$, it follows by the induction hypothesis that $n - (m - 1) + (r - 1) = 2$ and so $n - m + r = 2$.

The Euler Polyhedron Formula is therefore a special case of Theorem 10.1. While Euler struggled with the verification of $V - E + F = 2$, he did not have the luxury of a developed graph theory at his disposal.

From Theorem 10.1, it follows that every two planar embeddings of a connected planar graph result in planar graphs having the same number of regions; thus one can speak of the number of regions of a connected planar graph. For planar graphs in general, we have the following result. (See Exercise 2.) Recall that $k(G)$ denotes the number of components of a graph $G$.