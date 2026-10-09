
Method draws the polygon into the light map, using the same logic as the flat-shaded polygon rasterizer. There are only two changes to the rasterizer logic. First, instead of assigning a fixed color to each lumel we rasterize, we call `compute_light_level` to determine what the light level should be at the current pixel. Second, the horizontal and vertical size of the polygon is artificially increased, to allow for lumels on the edge of the polygon to be included in the light map computation.

Let's briefly discuss why we need to artificially increase the size of the polygon for light map rasterization purposes. The reason for this goes all the way back to a discussion in the introductory companion book *LinX 3D Graphics Programming*, when we first developed the rationale for our rasterization strategy. There, we said that it was of primary importance to plot every pixel once and only once, so that the polygons all lined up on the edges. We used the rule that only pixels whose upper-left corner was in the polygon were drawn. The problem is that using this same strategy here often leads to unsightly dark holes or dark strips in the light map, because certain lumels exactly on the edge of the polygon do not get rasterized and thus remain dark. When computing a light map, we should ideally compute a light intensity for every lumel of which any part—not just the upper-left corner—touches the polygon. Then, depending on how much of the lumel lies within the polygon, we would scale the computed intensity accordingly; a lumel only half within the polygon would only get half of its computed light intensity, for instance. This technique is called anti-aliasing. The shadow light map rasterizer here doesn't perform anti-aliasing, but it instead artificially expands the horizontal and vertical size of the polygon to cause it to cover more lumels. This means that the generated shadows are somewhat inaccurate, and sometimes contain a hole or two, but the code does serve its illustrative purpose in a working example.

Method `compute_light_level` computes the light level for a given 2D lumel coordinate $(u,v)$. It first goes from map space into world space—a very easy transformation using the axes of the light map space, as we saw in Chapter 2—then computes a light value using the diffuse reflection equation. The variables for storing the axes of the light map space are inherited from class `l3d_texture_computer`, and must have been set beforehand by the external caller.

**Listing 5-14: ras_sw1.h**

```cpp
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
l3d_rasterizer_2d_sw_imp(xs,ys,si) {};  void draw_polygon_flatshaded(const l3d_polygon_2d_flatshaded *p_poly);
};
#endif
```

**Listing 5-15: ras_swl.cc**

```cpp
#include "ras_swl.h"
#include "../system/sys_dep.h"
#include <string.h>
#include <stdlib.h>
#include "../tool_os/meman.h"

int l3d_rasterizer_2d_sw_lighter_imp::compute_light_level(int lumel_x, int lumel_y)
{
l3d_real x,y,z;
l3d_real u,v;

u = l3d_divr ( int_to_l3d_real(lumel_x), xsize );
v = l3d_divr( int_to_l3d_real(lumel_y), ysize );

x = 0.X_ + l3d_mulri(U.X_, u) + l3d_mulri(V.X_, v);
y = 0.Y_ + l3d_mulri(U.Y_, u) + l3d_mulri(V.Y_, v);
z = 0.Z_ + l3d_mulri(U.Z_, u) + l3d_mulri(V.Z_, v);
l3d_real a_light(0.0,0.0,1);

l3d_vector L(alight.X_ - x ,
            alight.Y_ - y ,
            alight.Z_ - z ,
            int_to_l3d_real(0)),
N(cross(U,V));
l3d_real intensity;

l3d_real f_att=l3d_divrr(int_to_l3d_real(1),
    (float_to_l3d_real(0.1)*float_to_l3d_real(0.01)*sqrt(l3d_real_to_float(dot(L,L)))));
if ( f_att>int_to_l3d_real (1)) f_att=int_to_l3d_real(1);
l3d_real n_dot_l;
n_dot_l = dot(normalized(N), normalized(L));
intensity = l3d_mulrr ( l3d_mulrr(int_to_l3d_real(128), f_att) ,
                        n_dot_l);
if (intensity>int_to_l3d_real(128)) intensity = int_to_l3d_real(128);
if (intensity<int_to_l3d_real(2)) {intensity = int_to_l3d_real(2);} 
return l3d_real_to_int(intensity);
}

void l3d_rasterizer_2d_sw_lighter_imp::draw_polygon_flatshaded
(const l3d_polygon_2d_flatshaded *p_poly)
{
l3d_real x0,y0,x1,y1,x2,y2,x3,
left_x_start,left_y_start,left_x_end,left_y_end,left_dx,left_x,leftedge,
right_x_start,right_y_start,right_x_end,right_y_end,right_dx,right_x,rightedge;
int left_celly_start, left_celly_end,
right_celly_start, right_celly_end, scanline;
l3d_real top_y,bottom_y;
int point_on_right=0;
int left_idx,right_idx, top_y_idx, bottom_y_idx;

int clipeleftedge, cliprightedge;
int maxy_upper, iceil_y0, iceil_y1, iceil_y2;

int i;


/*- convenience macro for accessing the vertex coordinates. Notice
/*- that we access the clipped vertex index list (not the original),
/*- and the transformed coordinate (not the original). This means
/*- we draw the clipped version of the transformed polygon.
#define VTX(i) ((*((p_poly->clist)[ ((*p_poly->clip_vertices)[i]).ivertex ])).transformed)

#define XPAD 4
#define YPAD 1
/*-
/*- STEP 1: Find top and bottom vertices
/*-

 top_y = VTX(0).Y;
 top_y_idx = 0;
 bottom_y = top_y;
 bottom_y_idx = top_y_idx;
 for(i=0; i<p_poly->clip_ivertices->num_items; i++) {

   if(VTX(i).Y < top_y) {
     top_y = VTX(i).Y;
     top_y_idx = i;
   }

   if(VTX(i).Y > bottom_y) {
     bottom_y = VTX(i).Y;
     bottom_y_idx = i;
   }
 }

 left_idx = top_y_idx;
 right_idx = top_y_idx;

/*-
/*- STEP 2: Create empty left edge
/*-
 left_x_start = VTX(top_y_idx).X;
 left_y_start = VTX(top_y_idx).Y;
 left_celly_start=iceil(left_y_start);
 left_celly_end=left_celly_start;

/*-
/*- STEP 3: Create empty right edge
/*-
 right_x_start=left_x_start;
 right_y_start=left_y_start;
 right_celly_start=left_celly_start;
 right_celly_end=right_celly_start;

/*-
/*- STEP 4: Loop from top y to bottom y
/*-

scanline = left_celley_start;

int first_scanline_done = 0;
while (scanline <= ysize) {

//--------------------------------------------------------------
// STEP 5: Find next left-edge of non-zero height (if needed)
//
while (left_celley_end - scanline <= 0) {
  if (left_idx == bottom_y_idx) return;  // done
  left_idx = p_poly->next_clip.left
    (left_idx

if (right_cell_end > ysize) right_cell_end = ysize;

// - STEP 7: Loop until left and/or right edge is finished
//
while ( ( scanline < left_cell_end) && (scanline < right_cell_end) ) {
   if(! first_scanline_done) {
      first_scanline_done = 1;
   }

   int top_pad;
   top_pad = scanline - yPAD;
   if(top_pad < 0) top_pad = 0;
   int target = scanline;

   for(scanline=top_pad ; scanline < target; scanline++) {

      clipleftedge = ifloor(left_x)-xPAD;

      clipleftedge = (clipleftedge < 0) ? 0 : clipleftedge;
      cliprightedge = iceil(right_x)*xPAD;

      cliprightedge = (cliprightedge > xsize-1) ? xsize-1 : cliprightedge;

      int lumeI_x = clipleftedge;
      for(register char unsigned *pix =
            &address_of_point(clipleftedge,
            SW_RAST_Y_REVERSAL(ysize,scanline));

            pix <= &address_of_point(cliprightedge, scanline);
            lumeI_x++) {
         {
            int light_value = compute_light_level(lumeI_x, scanline);

            light_value += *pix;
            if(light_value > 255) light_value = 255;
            draw_point_at_padress(&pix, light_value);
         }
      }

      left_x+= left_dx;
      right_x+= right_dx;
   }
}

clipleftedge = ifloor(left_x)-xPAD;

clipleftedge = (clipleftedge < 0) ? 0 : clipleftedge;
cliprightedge = iceil(right_x)*xPAD;

cliprightedge = (cliprightedge > xsize-1) ? xsize-1 : cliprightedge;
{
// - - STEP 8: Draw horizontal span
//
int lumeI_x = clipleftedge;
for(register char unsigned *pix =

TEAM LIN G - Live, Informative, Non-cost and Genuine!
