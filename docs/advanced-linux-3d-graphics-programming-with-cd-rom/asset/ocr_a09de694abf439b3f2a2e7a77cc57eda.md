```
float_to_13d_real(1.);
(*vertices)[2].original.set
(float_to_13d_real(0.),
float_to_13d_real(0.),
float_to_13d_real(1.));
(*vertices)[3].original.set
(float_to_13d_real(0.),
float_to_13d_real(0.),
float_to_13d_real(1.));
int pi;
pi = polygons.next_index();
polygons[pi] = new 13d_polygon_3d_flats haded(3);
printf("before: %p", polygons[pi]->vlist);
polygons[pi]->vlist = &vertices;
printf("after: %p", polygons[pi]->vlist);
(*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=0;
(*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=1;
(*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=3;
polygons[pi]->compute_center();polygons[pi]->compute_sfnormal();
pi = polygons.next_index();
polygons[pi] = new 13d_polygon_3d_flats haded(3);
polygons[pi]->vlist = &vertices;
(*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=2;
(*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=3;
(*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=1;
polygons[pi]->compute_center();polygons[pi]->compute_sfnormal();
pi = polygons.next_index();
polygons[pi] = new 13d_polygon_3d_flats haded(3);
polygons[pi]->vlist = &vertices;
(*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=0;
(*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=2;
(*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=1;
polygons[pi]->compute_center();polygons[pi]->compute_sfnormal();
pi = polygons.next_index();
polygons[pi] = new 13d_polygon_3d_flats haded(3);
polygons[pi]->vlist = &vertices;
(*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=3;
(*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=2;
(*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=0;
polygons[pi]->compute_center();polygons[pi]->compute_sfnormal();
num_xforms = 2;
xtheta=0;
modeling_xforms[0] = 13d_mat_rot(xtheta);
modeling_xforms[1].set
( float_to_13d_real(1.), float_to_13d_real(0.), float_to_13d_real(0.), float_to_13d_real(0.),
float_to_13d_real(0.), float_to_13d_real(1.), float_to_13d_real(0.), float_to_13d_real(0.),
float_to_13d_real(0.), float_to_13d_real(0.), float_to_13d_real(1.), float_to_13d_real(0.),
float_to_13d_real(0.), float_to_13d_real(0.), float_to_13d_real(0.), float_to_13d_real(1.) );
modeling_xform=
modeling_xforms[1] | modeling_xforms[0];
}
```