```
back_clip_plane.c = -tree->plane.c;
back_clip_plane.d = -tree->plane.d;
front_clip_plane.a = tree->plane.a;
front_clip_plane.b = tree->plane.b;
front_clip_plane.c = tree->plane.c;
front_clip_plane.d = tree->plane.d;

L3d_object_clippable_boundable *back_obj;
back_obj = new L3d_object_clippable_boundable
    (tree->object->vertices->num_fixed_items);
int should_delete_back_obj = 1;

*back_obj = *tree->object;

// uncomment the following to cause all polys to end up in the
// right children in the tree (be sure to comment out the similar
// assignment below to front_obj->polygons.num_items = 0)
//
back_obj->polygons.num_items = 0;
if(unsplit_obj_from_parent) {
    unsplit_obj_from_parent->reset();
    unsplit_obj_from_parent->clip_to_plane(back_clip_plane);
    _permanently_merge_objects(back_obj, unsplit_obj_from_parent);
}

if(back_obj->polygons.num_items > 0) {
    back_obj->reset();

    if(tree->children[0]) {
        push_polys_to_children(tree->children[0], back_obj);
    } else {
        // there previously were no polys in the back half space, but
        // now due to a poly pushed down from the parent, there are.
        // so create a new left child.
        tree->children[0] = new L3d_halfspace;
        tree->children[0]->object = back_obj;
        tree->children[0]->children.num_items = 0;
        tree->children[0]->children[tree->children[0]->children.next_index()] = NULL;
        tree->children[0]->children[tree->children[0]->children.next_index()] = NULL;
        tree->children[0]->bounding_sphere.compute_around_object(back_obj);

        should_delete_back_obj = 0;
    }
} else {
    if(tree->children[0]) {
        push_polys_to_children(tree->children[0], NULL);
    }
}

if(should_delete_back_obj) {delete back_obj;}
L3d_object_boundable *front_obj;
front_obj = new L3d_object_clippable_boundable
    (tree->object->vertices->num_fixed_items);
int should_delete_front_obj = 1;
```