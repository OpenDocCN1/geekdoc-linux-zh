```
    {**poly->vlist}[("poly->clip_ivertices")[ivtx].ivertex].original_X_   
        && (*dest->vvertices)[new_ivtx].original_Y ==
        && ("*poly->vlist")[("poly->clip_ivertices")[ivtx].ivertex].original_Y_   
        && (*dest->vvertices)[new_ivtx].original_Z ==
        && ("*poly->vlist")[("poly->clip_ivertices")[ivtx].ivertex].original_Z_   
    }
    {
        found new_ivtx = 1;
        int next_idx = poly->ivertices->next_index();
        ("*poly->ivertices")[next_idx].ivertex = new_ivtx;
    }
    if(!found_new_ivtx) {
        dest->vvertices->next_varying_index();
        dest->vvertices->num_varying_items -=1;
        dest->vvertices->num_fixed_items ++;
        (*dest->vvertices)
            [dest->vvertices->num_fixed_items + 1].original
            =
            (*"*poly->vlist")[("*poly->clip_ivertices")[ivtx].ivertex].original ;
        int next_idx = poly->ivertices->next_index();
        ("*poly->ivertices")[next_idx].ivertex =
            dest->vvertices->num_fixed_items - 1;
    }
}

poly->vlist = &dest->vvertices;

int pnum = dest->polygons.next_index();
l3d_polygon_3d_clipable *poly3;
poly3 = dynamic_cast<l3d_polygon_3d_clipable*> (*poly);

*dest->polygons[pnum] = poly3;
poly3->compute_center();
poly3->compute_sf normal();
poly3->plane.align_with_point_normal
(poly3->center.original,
normalized(poly3->sfnormal.original - poly3->center.original));
}
n = n->next;
}

void l3d_bsptree::push_poly_to_children
(l3d_halfspace *tree,
 l3d_object_clipable_boundable *unsplit_obj_from_parent)
{
    static int lvl=0;
    lvl++;
    if(tree) {
        // define front and back clipping planes
        l3d_plane front_clip_plane, back_clip_plane;
        back_clip_plane.a = -tree->plane.a;
        back_clip_plane.b = -tree->plane.b;
```

> TEAM LinG - Live, Informative, Non-cost and Genuine!