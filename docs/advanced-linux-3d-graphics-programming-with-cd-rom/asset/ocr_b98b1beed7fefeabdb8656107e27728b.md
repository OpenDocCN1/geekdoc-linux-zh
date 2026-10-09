```
int intersects_sphere(const l3d_bounding_sphere & sphere);
};

#endif
```

# Listing 4-7: vfrust.cc

```
#include "vfrust.h"
#include "../../tool_os/memman.h"

void l3d_viewing_frustum::create_from_points
(const l3d_point & top_left,
const l3d_point & top_right,
const l3d_point & bot_left,
const l3d_real & near_z,
const l3d_real & far_z,
const l3d_matrix& xform)
{
l3d_point eye(0,0,0,1);

top.align_with_points(xform[eye, xform[top_right], xform[top_left]];
bottom.align_with_points(xform[eye, xform[bot_left, xform[bot_right]];
left.align_with_points(xform[eye, xform[top_left, xform[bot_left]];
right.align_with_points(xform[eye, xform[bot_right, xform[top_right]];

l3d_point p1, p2, p3;

p1.set(int_to_l3d_real(0), int_to_l3d_real(0), near_z, int_to_l3d_real(1));
p2.set(int_to_l3d_real(1), int_to_l3d_real(0), near_z, int_to_l3d_real(1));
p3.set(int_to_l3d_real(0), int_to_l3d_real(1), near_z, int_to_l3d_real(1));
point.align_with_points(xform[p1,xform[p2,xform[p3]]);

p1.set(int_to_l3d_real(0), int_to_l3d_real(1), far_z, int_to_l3d_real(1));
p2.set(int_to_l3d_real(1), int_to_l3d_real(0), far_z, int_to_l3d_real(1));
p3.set(int_to_l3d_real(0), int_to_l3d_real(1), far_z, int_to_l3d_real(1));
far.align_with_points(xform[p1,xform[p2,xform[p3]];
}

int l3d_viewing_frustum::intersects_sphere(const l3d_bounding_sphere & sphere)
{
return
sphere.distance_to_plane(top) > -sphere.radius &&
sphere.distance_to_plane(bottom) > -sphere.radius &&
sphere.distance_to_plane(left) > -sphere.radius &&
sphere.distance_to_plane(right) > -sphere.radius &&
sphere.distance_to_plane(near) > -sphere.radius &&
sphere.distance_to_plane(far) > -sphere.radius
};
```