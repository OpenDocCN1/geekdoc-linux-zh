```
center_original_Y_ =
13d_divri(min_Y_ + max_Y_, 2);
center_original_Z_ =
13d_divri(min_Z_ + max_Z_, 2);

radius = int_to_13d_real(0);
for(i=0; i<0bject->vertices->num_fixed_items; i++) {
int vtx_is_referenced=0;
for(int pi=0; pi<0bject->polygons.num_items && !vtx_is_referenced;pi++) {
for(int vi=0; vi<object->polygons[pi]->vertices->num_items; vi++) {
if((\*object->polygons[pi]->vertices)[vtx].ivertex_ == i) {
vtx_is_referenced = 1;
break;
}
}
}

if(vtx_is_referenced) {
13d_real dist_squared;
dist_squared = dot((\*object->vertices)[i].original - center_original,
(\*object->vertices)[i].original - center_original));

if(dist_squared > radius) {
radius = dist_squared;
}
}
}
// the value computed in the above loop was the max squared distance,
// now take the square root to retrieve the actual distance
radius = 13d_sqrt(radius);
reset(); // copy original into transformed
```

# Other Bounding Volumes

Other bounding volumes are also used in 3D graphics for the purposes of faster testing and early rejection. Two common ones are the arbitrarily oriented bounding box (OBB) and the axially aligned bounding box (AABB).

An *arbitrarily oriented bounding box* is a cube-like box, with pairwise parallel sides which fully encompass the geometry it bounds. Like a cube, it can be defined with eight points. In general, a bounding box is stored along with the geometry it bounds, and is transformed the same way. For instance, if we rotate an object, we rotate its bounding box as well. This means that a bounding box can be arbitrarily oriented in space. On the one hand, this makes bounding boxes good bounding volumes, because they can tightly “fit” the underlying geometry (i.e., the bounding volume contains relatively little empty space around the bounded geometry), but on the other hand, the arbitrary orientation of the bounding box means that we have six arbitrarily oriented faces and eight arbitrarily located points. For instance, computing if two arbitrarily aligned bounding boxes intersect is not trivial; any one point of one box might pierce any face of the other box. For the purposes of view volume culling, we can check all corner points of the bounding box against all planes of the view frustum, then use the same logic we used for spheres for determining containment in the view frustum. One special case which must be handled is a huge bounding box larger