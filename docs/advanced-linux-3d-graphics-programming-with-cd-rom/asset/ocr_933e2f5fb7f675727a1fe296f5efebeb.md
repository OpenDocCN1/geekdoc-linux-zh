```
(*polygons[pi]->ivertices[polygons[pi]->ivertices->next_index()]].ivertex=3;
(*polygons[pi]->ivertices[polygons[pi]->ivertices->next_index()]].ivertex=2;
(*polygons[pi]->ivertices[polygons[pi]->ivertices->next_index()]].ivertex=0;
polygons[pi]->compute_o_center();polygons[pi]->compute_sfconvex();
```

```
num_xforms = 2;
modeling_xforms[0] = l3d_mat_rotx(0);
modeling_xforms[1].set(
{
float_to_l3d_real(1.0), float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(0.),
float_to_l3d_real(0.), float_to_l3d_real(1.), float_to_l3d_real(0.), float_to_l3d_real(0.),
float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(1.), float_to_l3d_real(1.);
float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(1.); });
```

```
modeling_xform=
modeling_xforms[1] | modeling_xforms[0];
currently_interpolating = false;
keyframe_no=0;
vertics = keyframes[keyframe_no];
```

```
pyramid::~pyramid(void) {
for (register int i=0; i<polygons.num_items; i++) { delete polygons[i]; }
for(int i=0; i<num_keyframes; i++) {
delete keyframes[i];
}
}
```

```
int pyramid::update(void) {
if(currently_interpolating) {
vertics = interep.list;
if(l_interpolate()) {
currently_interpolating = false;
}
} else {
keyframe_no++;
if(keyframe_no >= num_keyframes) {keyframe_no = 0; }
int next_keyframe = keyframe_no + 1;
if(next_keyframe >= num_keyframes) (next_keyframe = 0; }

vertics = keyframes[keyframe_no];
interep.start(*keyframes[keyframe_no], *keyframes[next_keyframe],
rand(\%100 + 50, 3));

currently_interpolating = true;
}
return 0;
}
```

The program morph3d uses the l3d_world and l3d_object classes to store the virtual world. The file main.cc is very simple: it declares a world subclass which creates some pyramid objects.

The pyramid class is a morphing 3D pyramid. It changes its shape between a compact and an elongated pyramid. To accomplish this, we added the following lines to the pyramid class:

```
class pyramid:public l3d_object {
static const int num_keyframes = 2;
int keyframe_no;

two_pair_l3d_coordinate* *keyframes[2];
l3d_vextex_interpolator_interp;
bool currently_interpolating;
};
```