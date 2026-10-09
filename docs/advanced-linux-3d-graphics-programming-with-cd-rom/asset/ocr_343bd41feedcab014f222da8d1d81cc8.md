than the frustum itself; all eight corners lie outside the frustum, but part of the box does lie within the frustum.

![](bbox=[0.15, 0.17, 0.89, 0.35])

*Figure 4-12: An arbitrarily oriented bounding box is transformed along with its geometry, making for a tight fit but possibly more complicated computations.*

An *axially aligned bounding box* is the same as a bounding box, with the exception that all of its sides are always parallel to one of the $x$-$y$, $y$-$z$, or $x$-$z$ planes. In other words, the normal vectors of the sides of the AABB must lie along one of the principal coordinate axes, hence the term “axially aligned.” In contrast to an arbitrarily oriented bounding box, an axially aligned bounding box is not transformed along with its underlying geometry due to the alignment restriction on the sides. This means that as an object rotates, its AABB might need to be recomputed. Since the sides of an AABB are all conveniently aligned, we only need to store two opposite corner points of the AABB, not all eight corner points. AABBs generally provide a fairly poor fit to the underlying geometry, but certain operations on AABBs are very easy. For instance, intersection of two AABBs can be determined by three consecutive one-dimensional overlap tests; if the $x$, $y$, and $z$ intervals defining the sides of the two AABBs overlap, then the AABBs themselves overlap; otherwise they are disjoint. For the purposes of view volume culling, AABBs can be handled like OBBs; we test the corner points of the AABB against the view frustum to see if the entire AABB is inside or outside of the view frustum.

![](bbox=[0.15, 0.7, 0.89, 0.86])

*Figure 4-13: An axis-aligned bounding box has sides whose normal vectors lie along the principal coordinate axes. It provides a poor fit to geometry, but simplifies some computations.*