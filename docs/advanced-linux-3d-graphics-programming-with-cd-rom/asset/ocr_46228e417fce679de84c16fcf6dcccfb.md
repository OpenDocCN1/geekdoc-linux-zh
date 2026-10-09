# Chapter 2: Rendering and Animation Techniques for 3D Polygons

```
left_x_start=I3d_real_to_fixed(VTX(top_y_idx).X);
left_celix_start=icel_fix(left_x_start);
left_y_start=I3d_real_to_fixed(VTX(top_y_idx).Y);
left_celuy_start=icel_fix(left_y_start);
left_cely_end=left_celuy_start;
left_zi_start = fixixsiv(int2fix(IZ.MULT FACTOR),
13d_real_to_fixed(((I3d polygon ivertext textured *)
& ((p.poly->cIip_ivertices))[left_idx])>>tex_coord.Z_
+ float2fix(Z.ADD_FACTOR));
left_zi_end = left_zi_start;
left_ui_start = fixixmul(
13d_real_to_fixed(((I3d_polygon ivertext textured *)
& ((p.poly->cIip_ivertices))[left_idx])>>tex_coord.X_x),
left_zi_start);
left_ui_end = left_ui_start;
left_vi_start = fixixsml(
13d_real_to_fixed(((I3d_polygon ivertext textured *)
& ((p.poly->cIip_ivertices))[left_idx])>>tex_coord.Y),
left_vi_end = left_vi_start;
left_vi_end = left_vi_start;
right_x_start=left_x_start;
right_y_start=left_y_start;
right_celilx_start=left_celilx_start;
right_celilx_end=right_celilx_start;
right_ui_start = left_ui_start;
right_vi_start = left_vi_start;

scanline = left_celilx_start;
cnt omeshot=1;

while(scanline < ysize) {
/* if needed, find next left-edge whose scanline_end < current scanline
while( left_celilx_end - scanline <= 0 )
{
if (left_idx == bottom_y_idx) {
return;
}
left_idx = p.poly->next clipidx_left(left_idx,p.poly->clip_iyvertices->num_items);
left_y_end=I3d_real_to_fixed(VTX(left_idx).Y);
left_celilx_end = icel_fix(left_y_end);
if(left_celilx_end - scanline)
}
#endif MIN_EDGE_HIGHER float2fix(0.005)
#define MIN_EDGE_WIDTH float2fix(0.005)
left_x_end=I3d_real_to_fixed(VTX(left_idx).X);
left_celilx_end=icel_fix(left_x_end);
left_zi_end = fixixsiv(int2fix(IZ.MULT FACTOR),
13d_real_to_fixed(((I3d polygon ivertext textured *)
& ((p.poly->cIip_ivertices))[left_idx])>>tex_coord.Z_
+ float2fix(Z.ADD_FACTOR));
left_ui_end = fixixsml(
13d_real_to_fixed(((I3d polygon ivertext textured *)
& ((p.poly->cIip_ivertices))[left_idx])>>tex_coord.X_x),
left_zi_end);
left_vi_end = fixixsml(
13d_real_to_fixed(((I3d polygon ivertext textured *)
& ((p.poly->cIip_ivertices))[left_idx])>>tex_coord.Y_),
```