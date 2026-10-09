
![](img/a19d4e8b1d7eb6387691dc6c865430e6_235_0.png)

Figure 4-7: The view frustum can be defined by six planes: near, far, left, right, top, and bottom. The corner points are computed via reverse projection of the screen space corner points, and are used to compute the equations for the left, right, top, and bottom planes.

The near and far planes of the frustum are the near and far z clipping planes, each defined by a plane equation of the form z=k, where k is the distance of the plane (near or far) from the eye. Until now, we have not actually clipped against a far z plane, but the idea is the same as with the near z plane, with the exception that the far z plane’s normal points in the opposite direction as the near z plane’s, because we clip against the near side of the near plane, but against the far side of the far plane.

The remaining four planes of the frustum are a bit trickier to define. They represent the left, right, bottom, and top limits to the field of vision, due to the finite size of the projection window. Recall that knowing three points lying on a plane can define the plane; we only need to use the three points to form two unique vectors, take the cross product to find the plane normal (the $A$, $B$, and $C$ terms of the plane equation), and then use one of the three points to solve for the $D$ term of the plane equation. Method `l3d_plane::align_with_points` computes the plane coefficients based on three given points; remember that the order of the points passed to the method is important, because it determines the front/back orientation of the plane.

To define the remaining four planes of the frustum, we first calculate the camera space coordinates of the four corners on the near plane which, when projected from 3D to 2D, yield the four corners of the screen in screen space. In other words, we take a reverse projection of the four corners of the screen in 2D screen space, giving us four camera space points in 3D camera space lying on the near z plane. Each view frustum plane passes through two of these points.

For instance, (0,0), (319,0), (319,239), (0,239) would be the screen space corner coordinates for a 320x240 window; we would reverse project these onto the near z plane using the reverse projection formulas from Chapter 2. Recall that reverse projection first finds the z value of the projected point by using the plane equation of the plane on which the 3D point must lie, then multiplies the projected $x$ and $y$ by the computed 3D $z$ value to obtain the 3D $x$ and $y$ values, thus reversing the perspective division by $z$. See Chapter 2 for the full equations, which involve the field of view terms and the screen size. Note that in this case we actually don’t need to use the plane equation to compute the $z$ value; since we are reverse projecting onto the near $z$ plane, where $z$ is a constant, we already know the $z$ value to use in the reverse projection formulas of Chapter 2.

We then use consecutive pairs of these reverse projected corner points, along with the camera space coordinates of the camera itself (which is conveniently (0,0,0) in camera space), and calculate a plane given these three points, because these three points lie exactly on each side of the view frustum. Assuming we call the reverse projected corner points of the screen “upper-left,” “upper-right,” “lower-right,” and “lower-left,” the following list shows us which points to use to calculate a particular frustum plane.

- Top frustum plane: Camera location (0,0,0), upper-right, and upper-left.
- Right frustum plane: Camera location (0,0,0), lower-right, and upper-right.
- Bottom frustum plane: Camera location (0,0,0), lower-left, and lower-right.
- Left frustum plane: Camera location (0,0,0), upper-left, and lower-left.

> NOTE In the above list, the order of the points has been *carefully* chosen so as to define the inside side of the plane to be inside of the frustum; in other words, when viewed from the inside of the frustum, the specified points *appear* clockwise. This is important for the method `l3d_plane::align_with_points`, as mentioned earlier.

## Computing the Frustum in World Coordinates

The above procedure gives us frustum planes, defined in terms of plane equation coefficients, in camera space. We can also perform the same procedure by using the world space locations by multiplying each point by the inverse camera transformation matrix just before using the point to compute the frustum plane. This gives us the frustum planes in world coordinates instead of camera coordinates. This can be useful to allow us to perform frustum culling in world space rather than camera space, which allows us to cull objects before transforming them to camera space. Note that such world space culling only saves computational effort if we use a simplified bounding volume to represent the geometry for the culling purposes; see the section titled “Bounding Spheres and the View Frustum.”

For instance, to compute the top frustum plane in world coordinates, we multiply camera location (0,0,0) by the inverse camera transformation matrix to get the camera’s position in world space. Similarly, we multiply the upper-right and upper-left corner points by the inverse camera matrix to obtain these points in world space instead of camera space. Then using these world space coordinates, we compute the plane equation.

Computing the near and far frustum planes in world space also requires us to create planes using three points in world space, not camera space. This is also straightforward: the near and far planes are defined, in camera space, by an equation of the form $z = k$, where $k$ is a constant defining the distance from the eye to the plane. Therefore, in camera space, any point of the form $(x,y,k)$, for arbitrary $x$ and $y$, lies on the plane in question. We can choose any three points $(x_i,y_i,k)$ that do not lie in a straight line to define the plane in camera space; then, we multiply these camera space points by the inverse camera matrix to obtain world space points from which we can compute the world space plane. A convenient choice of non-collinear (not lying in a straight line) points for the near plane is (0,0,k), (1,0,k), and (0,1,k); for the far plane, use the same points in reverse order: (0,1,k), (1,0,k), (0,0,k). The far plane’s normal must point in the opposite direction of the near plane’s normal so that the inside side of each plane lies on the inside of the frustum—hence, the reversal of point ordering for near and far planes. For instance, if the near plane is defined in camera space as z=1.5, we would take points (0,0,1.5), (1,0,1.5), and (0,1,1.5) as points known to be on the near plane in camera space. Then we multiply these points by the inverse camera matrix to obtain world space points. Finally, we compute the plane using these three points.

## Class l3d_viewing_frustum

Class `l3d_viewing_frustum` represents a view frustum. It stores six planes for the six sides of the frustum, in member variables top, bottom, left, right, near, and far.

The method `create_from_points` creates a view frustum given four reverse projected corner points (as covered earlier), a near plane, a far plane, and a transformation matrix. The routine aligns the six planes of the frustum using the scheme described in the previous section: the top, bottom, left, and right planes are created using the eye point and two of the four corner points. The front and back planes are created using a simple non-collinear set of three points located on the near and far planes. Creation (or alignment, depending on how you view it) of all planes takes place through method `l3d_plane::align_with_points`. Before all points are passed to this method, they are multiplied with the transformation matrix `xform`, which is passed as a parameter. By default, the frustum creation takes place in camera coordinates and yields a set of planes representing the location of the frustum in camera coordinates. By passing a transformation matrix that changes from camera coordinates to world coordinates, we can compute the frustum in world coordinates, which is generally more desirable. This means that we pass the inverse viewing matrix from the camera as the `xform` parameter to obtain the frustum planes in world space. To obtain the frustum in camera space, pass an identity matrix as the `xform` parameter.

The method `intersect_with_sphere` tests to see if a sphere is inside of the view frustum. The next sections cover this method and the idea in more detail.

> Listing 4-6: vfrust.h

```cpp
#ifndef _VFRUST_H
#define _VFRUST_H
#include "../tool_gs/memman.h"
#include "../point/point.h"
#include "../plane/plane.h"
#include "../boundvol/boundsph.h"

class l3d_viewing_frustum {
public:
    l3d_plane top, bottom, left, right, near, far;
void create_from_points(const l3d_point & top_left,
 const l3d_point & top_right,
 const l3d_point & bot_right,
 const l3d_point & bot_left,
 const l3d_real & near_z,
 const l3d_real & far_z,
 const l3d_matrix& xform);
```
