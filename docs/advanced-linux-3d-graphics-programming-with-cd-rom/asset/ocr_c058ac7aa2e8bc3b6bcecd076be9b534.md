# 44



```
```c
float_to_13d_real(0.0),
float_to_13d_real(1.1));
(*keyframes[0])[3].original.set
(float_to_13d_real(0.0),
float_to_13d_real(0.0),
float_to_13d_real(10.0),
float_to_13d_real(1.1));

keyframes[1] = new l3d_two_part_list<l3d_coordinate>(4);
(*keyframes[1])[0].original.set
(float_to_13d_real(5.0),
float_to_13d_real(5.0),
float_to_13d_real(5.0),
float_to_13d_real(1.1));
(*keyframes[1])[1].original.set
(float_to_13d_real(-10.0),
float_to_13d_real(10.0),
float_to_13d_real(0.0),
float_to_13d_real(1.1));
(*keyframes[1])[2].original.set
(float_to_13d_real(10.0),
float_to_13d_real(0.0),
float_to_13d_real(1.1));
(*keyframes[1])[3].original.set
(float_to_13d_real(10.0),
float_to_13d_real(0.0),
float_to_13d_real(1.1));

int pi;
pi = polygons.next_index();
polygons[pi] = new l3d_polygon_3d_flatshaded(3);
printf("before: %p", polygons[pi]->vlist);
polygons[pi]->vlist = &vertices;
printf("after: %p", polygons[pi]->vlist);
(*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex=0;
(*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex=1;
(*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex=3;
polygons[pi]->compute_center(*polygons[pi]->compute_sfcolorn();

pi = polygons.next_index();
polygons[pi] = new l3d_polygon_3d_flatshaded(3);
polygons[pi]->vlist = &vertices;
(*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex=2;
(*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex=3;
(*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex=1;
polygons[pi]->compute_center(*polygons[pi]->compute_sfcolorn();

pi = polygons.next_index();
polygons[pi] = new l3d_polygon_3d_flatshaded(3);
polygons[pi]->vlist = &vertices;
(*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex=0;
(*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex=1;
(*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex=2;
polygons[pi]->compute_center(*polygons[pi]->compute_sfcolorn();

pi = polygons.next_index();
polygons[pi] = new l3d_polygon_3d_flatshaded(3);
polygons[pi]->vlist = &vertices;
```
```