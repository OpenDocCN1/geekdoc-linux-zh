![](bbox=[0.2, 0.11, 0.85, 0.24])

**Figure 5-15. Octree division of space.** We begin with an undivided cube (shown at the left of the diagram), then divide it into eight equally sized regions numbered 0-7 (shown in the middle part of the diagram; note that octant 0 is hidden), then again divide octant 7 into eight further octants (shown at the right of the diagram). The numbering scheme chosen for the octants is not standardized, and is taken from [FOLE92].

![](bbox=[0.2, 0.37, 0.85, 0.74])

**Figure 5-16. Storing an octree.** We can store all eight children directly as child nodes of the parent node, or we can store the eight children within a BSP tree by splitting space three ways.

We can use the octree in a manner similar to the way we use an axis-aligned BSP tree. As with the axis-aligned BSP tree, there is no guarantee of convexity of the polygon groups within an octree node. So, to display the contents of an octree, we can traverse the nodes back to front or front to back, relying on a z sort, z buffer, or mini BSP tree to resolve the visibility question within