![](bbox=[0.05, 0.08, 0.95, 0.43])

# Wagner’s Theorem

The German mathematician Klaus Wagner (1910–2000) showed that the converse of Theorem 10.20 is true [251] in 1937, only a year after obtaining his Ph.D. from Universität zu Köln (University of Cologne), thereby giving another characterization of planar graphs.

**Theorem 10.21 (Wagner’s Theorem)** *A graph G is planar if and only if neither* $K_5$ *nor* $K_{3,3}$ *is a minor of G.*

**Proof.** We have already mentioned (in Theorem 10.20) that if a graph G is nonplanar, then either $K_5$ or $K_{3,3}$ is a minor of G. For the converse, suppose that G is a graph having $K_5$ or $K_{3,3}$ as a minor. If G were planar, then every minor of G is planar, contradicting the assumption that $K_5$ or $K_{3,3}$ is a minor of G. Thus, G is nonplanar. ▪

More specifically, Theorem 10.21 can be proved with the aid of the following result.

**Theorem 10.22** *Let G be a graph.*

+   (a) If G has $K_{3,3}$ as a minor, then G contains a subdivision of $K_{3,3}$.

+   (b) If G has $K_5$ as a minor, then G contains either a subdivision of $K_5$ or a subdivision of $K_{3,3}$.

**Proof.** Suppose first that $H = K_{3,3}$ is a minor of G. The graph H can be obtained by first deleting edges and vertices of G (if necessary), obtaining a connected graph G′, and then by a succession of edge contractions in G′. We show, in this case, that G′ contains a subgraph that is a subdivision of $K_{3,3}$ and so G′, and G as well, is nonplanar.