method draws the polygon into the light map, using the same logic as the flat-shaded polygon rasterizer. There are only two changes to the rasterizer logic. First, instead of assigning a fixed color to each lumel we rasterize, we call `compute_light_level` to determine what the light level should be at the current pixel. Second, the horizontal and vertical size of the polygon is artificially increased, to allow for lumels on the edge of the polygon to be included in the light map computation.

Let's briefly discuss why we need to artificially increase the size of the polygon for light map rasterization purposes. The reason for this goes all the way back to a discussion in the introductory companion book LinX 3D Graphics Programming, when we first developed the rationale for our rasterization strategy. There, we said that it was of primary importance to plot every pixel once and only once, so that the polygons all lined up on the edges. We used the rule that only pixels whose upper-left corner was in the polygon were drawn. The problem is that using this same strategy here often leads to unsightly dark holes or dark strips in the light map, because certain lumels exactly on the edge of the polygon do not get rasterized and thus remain dark. When computing a light map, we should ideally compute a light intensity for every lumel of which any part—not just the upper-left corner—touches the polygon. Then, depending on how much of the lumel lies within the polygon, we would scale the computed intensity accordingly; a lumel only half within the polygon would only get half of its computed light intensity, for instance. This technique is called anti-aliasing. The shadow light map rasterizer here doesn't perform anti-aliasing, but it instead artificially expands the horizontal and vertical size of the polygon to cause it to cover more lumels. This means that the generated shadows are somewhat inaccurate, and sometimes contain a hole or two, but the code does serve its illustrative purpose in a working example.

Method `compute_light_level` computes the light level for a given 2D lumel coordinate (u,v). It first goes from map space into world space—a very easy transformation using the axes of the light map space, as we saw in Chapter 2—then computes a light value using the diffuse reflection equation. The variables for storing the axes of the light map space are inherited from class `l3d_texture_computer`, and must have been set beforehand by the external caller.

```
**Listing 5-14: ras_sw1.h**

```
finder_RAS_SW_H
#define RAS_SW_H
include "../cool_os/memman.h"
include "ras_sw.h"
include "math.h"
include "../system/sys_dep.h"
include "../geom/texture/texture.h"

class l3d_rasterizer_2d_sw_lighter_imp:
virtual public l3d_rasterizer_2d_sw_imp,
virtual public l3d_texture_computer
{
protected:
virtual int compute_light_level(int lumel_x, int lumel_y);
public:
l3d_rasterizer_2d_sw_lighter_imp(int xs, int ys, l3d_screen_info *si) :
l3d_rasterizer_2d_sw_imp(xs,ys,si),
```

```