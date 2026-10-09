two steps: a test to see if the ray crosses the plane of the polygon, and if so, a second test to see if the point of intersection actually lies within the polygon. For simplicity, we assume that the polygons being tested are convex.

The first test is easy. We simply evaluate the plane equation twice, once with the first point and once with the second point. If the signs of the results differ, the point moved from one side of the plane to the other. This is because evaluating a plane equation with a point's coordinates tells us the position of the point relative to the plane.

![](bbox=[0.15, 0.28, 0.57, 0.57])

Figure 8-4: The point has crossed from one side of the polygon's plane to the other.

If the sign changes, the segment of the ray between the starting and ending points crosses the plane of the polygon, but not necessarily the polygon itself. The next test, therefore, is to compute the actual intersection point between the ray and the polygon, and see if it lies within the polygon.

![](bbox=[0.15, 0.66, 0.57, 0.96])

Figure 8-5: Even if the point crosses the plane, it may or may not cross the polygon. Here, the point's path does not cross the polygon.