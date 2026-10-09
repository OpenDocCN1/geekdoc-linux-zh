```
```cpp
13d_polygon_3d_collidable(void) : 13d_polygon_3d_clippable() {};
13d_polygon_3d_collidable(int num_pts) :
   13d_polygon_3d(num_pts),
   13d_polygon_2d(num_pts)
{};
int contains_point(const 13d_point &point);
13d_polygon_3d_collidable(const 13d_polygon_3d_collidable &r);
13d_polygon_2d *clone(void);
};

#if __LH__ACTIVE__P3_COLL_H
#else
#endif
```
```

# **Listing 8-12: p3_coll.cc**

```
```cpp
#include "p3_coll.h"
#include "../..\tool_os\nemman.h"

int 13d_polygon_3d_collidable::contains_point(const 13d_point& point) {
   int collindex[2];
   int inside_side;

   if (13d_abs(plane.a) > 13d_abs(plane.b) &&
       13d_abs(plane.a) > 13d_abs(plane.c))
   {
      //- smallest variation in the a (x) direction (largest normal component);
      //- drop it
      collindex[0] = 2; //- z axis becomes new 2D x axis
      collindex[1] = 1; //- y axis becomes new 2D y axis
      //- NOTE: look at LHS system. drop x. we must use "y" as the vertical
      //- axis and "z" as horiz. in order for left-right orientation to stay
      //- the same.

      //- if the dir. of the normal vector component you dropped is positive,
      //- the orientation of the orthogonally-projected poly is clockwise
      //- (the normal case for a LHS coordinate system) else counterclockwise.
      //- BUT it side of point assumes SCREEN-SPACE coords, i.e., +ve y axis is
      //- DOWN, but here we are working in 3D space with one axis dropped,
      //- giving an orthogonically projected point with +ve y axis going UP.
      //- so we flip our interpretation of "inside" and "outside" from the
      //- result returned by side_of_point: we treat -1 as inside for normal
      //- clockwise polys, and treat +1 as inside for reversed counterclockwise
      //- polys.

      if(plane.a > 0) inside_side = -1; else inside_side = 1;
   }else if(13d_abs(plane.b) > 13d_abs(plane.a) &&
       13d_abs(plane.b) > 13d_abs(plane.c))
   {
      //- smallest variation in the b (y) direction (largest normal component);
      //- drop it
      collindex[0] = 0; //- x axis becomes new 2D x axis
      collindex[1] = 2; //- z axis becomes new 2D y axis

      //- if the dir. of the normal vector component you dropped is positive,
      //- the orientation of the orthogonally-projected poly is clockwise
      //- (the normal case for a LHS coordinate system) else counterclockwise.
```
```