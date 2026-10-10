TABLE 10.3

| Stage | (i) | (ii) | (iii) | (iv) | (v) | (vi) | (vii) | (viii) | (ix) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Vertex, x |  |  |  |  |  |  |  |  |  |
| u | (*,0) | [*,0] |  |  |  |  |  |  |  |
| n | (*,∞) | (u,5) |  | [u,5] |  |  |  |  |  |
| p | (*,∞) |  |  | (n,14) |  |  | (q,13) | [q,13] |  |
| q | (*,∞) |  |  |  | (s,11) | [s,11] |  |  |  |
| r | (*,∞) | (u,3) | [u,3] |  |  |  |  |  |  |
| s | (*,∞) |  |  | (r,12) | (n,8) | [n,8] |  |  |  |
| t | (*,∞) |  |  |  |  | (s,13) |  | [s,13] |  |
| v | (*,∞) |  |  |  |  |  | (q,17) |  | [t,14] | [t,14] |

We have used roman numerals for the stages to avoid confusion with the numbers used for the steps in the algorithm. At stage (i) we have assigned labels to the vertices in accordance with step 1 of the algorithm. Now at stage (ii), we have y = u because in the label attached to u the distance is 0, whereas it is ∞ for all the other vertices with a temporary label. So the label attached to u is made permanent. Now u is joined by edges to the vertices n and r. We see that l(u) + μ(un) = 0 + 5 = 5, and so n is assigned the temporary label (u,5). And as l(u) + μ(ur) = 0 + 3 = 3, r is assigned the temporary label (u,3).

Of the current temporary labels, (u,3) assigned to the vertex has the least second component. So at stage (iii) we assign the permanent label [u,3] to the vertex r. The vertex r is joined to the vertices n and s, which do not have permanent labels. The vertex r has the permanent label [u,3]. The vertex n has the temporary label (u,5). Since l(r) + μ(rn) = 3 + 4 = 7 > 5, the temporary label attached to n is left unchanged. The vertex s has the temporary label (*,∞). Since l(r) + μ(rs) = 3 + 9 = 12 < ∞, the temporary label attached to s is replaced by (r,12).

Now consider stage (vi). At this stage the vertices with temporary labels are (n,14) for p, (s,11) for q, (s,∞) for t and (*,∞) for v. So the minimal value of l is associated with the vertex p. Therefore at step 2 in the algorithm we put x = n and make the label attached to q permanent. The vertices with temporary labels that are joined to q by an edge are p, t, and v. The vertex p has a temporary label (n,14). Since l(q) + μ(qp) = 11 + 2 = 13 < 14, we replace the temporary label attached to p by (q,13). The vertex t has a temporary label (s,13). Since l(q) + μ(qt) = 11 + 4 = 15 > 13, the temporary label attached to t is unchanged. The vertex v has a temporary label (*,∞). Since l(q) + μ(qv) = 11 + 6 = 17 < ∞, the temporary label attached to v is replaced by (q,17).

The algorithm terminates after stage (ix). From Table 10.3 we see that the shortest path from u to v has length 14. Also, we can trace the path back from v by following the vertex that forms the first part of the permanent label attached to v. In this way we obtain the path

v ← t ← s ← n ← u.