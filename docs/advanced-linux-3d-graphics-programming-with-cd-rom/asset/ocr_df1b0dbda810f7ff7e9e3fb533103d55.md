sort of collision response if we detect a collision, such as moving the objects apart again. Collision detection algorithms are important for 3D graphics applications for two reasons:

They allow us to impart a sense of physical reality to our virtual 3D worlds, greatly enhancing the user’s sense of place in the virtual world.

They illustrate useful geometric intersection techniques which are often also needed for visual 3D graphics algorithms, such as ray tracing or shadow computation.

In this section, we’ll look at collision detection in general, and then develop a very simple collision detection and response system to prevent us from walking through walls in our virtual world. We’ll also populate our virtual world with other moving objects that wander throughout the world, using collision detection to keep them from walking through walls and each other.

# Intersection Testing and Bounding Volumes

Collision detection essentially requires us to determine if two objects spatially overlap. Spatial overlap is the same as intersection between any parts of the two objects. Since our objects are arbitrary, non-convex polygonal solids, one way of checking would be to test every polygon of one object against every polygon of the other object, checking for intersection. With a large number of objects, this sort of exhaustive testing quickly becomes impractical because of the explosive number of tests that need to be done. Furthermore, such precise collision detection is often not even needed. It depends on the purpose of the collision detection. Often, in interactive 3D applications, a primary goal of collision detection is simply to prevent objects as a whole from moving through one another. This means that we can enclose the objects within simple, convex bounding volumes, such as spheres or boxes, and check these bounding volumes for intersection. If the bounding volumes do not intersect, then the objects do not intersect. If the bounding volumes intersect, the objects might intersect. Depending on the application, we can then perform finer polygon-to-polygon intersection tests to determine the exact collision points, or we can treat a bounding volume collision as an actual collision.

![](bbox=[0.21, 0.62, 0.56, 0.95])

> Figure 8-1: Checking for collisions can be done by checking every polygon of one object against every polygon of the other object, but this is slow.