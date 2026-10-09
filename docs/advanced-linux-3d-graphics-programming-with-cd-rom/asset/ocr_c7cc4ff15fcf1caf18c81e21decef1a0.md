```
oc = dynamic_cast <l3d_object_c1ippable *>(objects[i0bj]);
if(oc) {
    oc->clip_to_plane(frustum.near);
    oc->clip_to_plane(frustum.far);
    oc->clip_to_plane(frustum.top);
    oc->clip_to_plane(frustum.bottom);
    oc->clip_to_plane(frustum.left);
    oc->clip_to_plane(frustum.right);
}

objects[i0bj]->camera_transform(camera->viewing_xform);

l3d_polygon_3d_node *n;

// - vector from facet center to camera (at 0,0,0), for backface culling
l3d_vector facet_to_cam_vec;
//- facet's sfc normal relative to origin (aFacet.sfc_normal is relative
//- to facet center)
l3d_vector N;
n = objects[i0bj]->nonculled_polygon_nodes;
while(n) {
    N = n->polygon->sfcnormal.transformed - n->polygon->center.transformed;

    facet_to_cam_vec.set (0 - n->polygon->center.transformed.X_,
                          0 - n->polygon->center.transformed.Y_,
                          0 - n->polygon->center.transformed.Z_);
                          int_to_l3d_real(0));

    //- dot product explicitly formulated so no fixed point overflow
    //- (facet_to_cam_vec is very large)
    //-(use of the inline function "dot" uses default fixed precision)

    #include "../../math/fix_lowp.h"
    #define BACKFACE_EPS (float_to_l3d_real(0.1)
    if((l3d_mulr(FX_CVT(N.X_), FX_CVT(facet_to_cam_vec.X_)) +
        l3d_mulr(FX_CVT(N.Y_), FX_CVT(facet_to_cam_vec.Y_)) +
        l3d_mulr(FX_CVT(N.Z_), FX_CVT(facet_to_cam_vec.Z_)) > BACKFACE_EPS)
    //- equivalent to: if(N.dot(facet_to_cam_vec) > BACKFACE_EPS ) -
    #include "../../math/fix_prec.h"
}
{
    //- polygon is not culled
} else {
    //- take this polygon out of the list of nonculled_polygon_nodes
    if(n->prev) {
        n->prev->next = n->next;
    } else {
        objects[i0bj]->nonculled_polygon_nodes = n->next;
    }

    if(n->next) {
        n->next->prev = n->prev;
    }
}

n = n->next;
```