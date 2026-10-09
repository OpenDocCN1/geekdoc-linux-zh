The problem also exists with sphere-to-sphere collisions. Two fast-moving spheres might cross paths without ever colliding with one another, although they should actually have collided at an earlier point in time.

![](bbox=[0.21, 0.2, 0.77, 0.5])

*Figure 8-11: Two high-speed spheres sailing past one another without registering a collision.*

For the sphere-to-sphere case, and in general for other bounding-volumes-to-bounding-volume tests as well, we can detect this situation by using a *sweep test*. A *sweep* refers to the volume of space covered by a moving object between the object’s old position and its new position. Sweep tests therefore must detect if a collision occurred at any point along the object’s trajectories. Let’s derive a sweep test for sphere-to-sphere intersection, which illustrates the general methods used for developing such tests.

Assume we have two moving spheres $P$ and $Q$. Sphere $P$ was initially located at location $P_{0}$, and travels at a velocity $V_{P}$ towards its new position $P_{1}$. Similarly, sphere $Q$ begins at $Q_{0}$ and travels with velocity $V_{Q}$ towards its new position $Q_{1}$. Let us adopt the convention that at time $t=0$, both spheres were at their starting points, and at time $t=1$, both spheres were at their new positions. This is standard parameterization. Then, the question is, is there any $t$ such that the spheres collided? We define a sphere collision in terms of the distance between the spheres’ centers. We can compute the distance between two points as the square root of the dot product of an offset vector with itself, where the offset vector is the vector from one sphere’s center to the other. Thus, at a given time $t$, the distance between $P$ and $Q$ is given by:

```
```
Equation 8-1    d(t)   =  \sqrt{o(t) \cdot o(t)}
                 o(t)   =  (Q_{0} + tV_{Q}) - (P_{0} + tV_{P})
```
```