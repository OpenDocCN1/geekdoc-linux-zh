```
```text
objects[ibj]-->apply_perspective_projection(*camera,
    screen->xsize, screen->ysize);

n = objects[ibj]-->nonculled_polygon_nodes;

while(n) {

    plist[pnum+] = n->polygon;

    /* Use the average of all z-values for depth sorting */
    l3d real zsum=int_to_l3d_real(0);
    register int ivtx;

    for(ivtx=0; ivtx<n->polygon->vertices->num_items; ivtx++) {
        zsum += ((*n->polygon->plist)) { (*n->polygon->vertices)[ivtx].ivertex
            ].transformed_intermediates[1]_Z : }
    }
    n->polygon->zvisible = l3d_divisi(zsum, ivtx);
    n = n->next;
}

/* Sort the visible facets in decreasing order of z-depth */
qsort(plist, pnum, sizeof(l3d_polygon_3d *), compare_facet_zdepth);

/* Display the facets in the sorted z-depth order (painter's algorithm) */
for(int i=0; i<pnum; i++) {
    plist[i]->draw(rasterizer);
}

char msg[256];
sprintf(msg,"%d POLYS DRAWN", pnum);
rasterizer->draw_text(0,16,msg);

sprintf(msg,"%d objects culled",
    culled_obj_count);
rasterizer->draw_text(0,32,msg);
```
```

The first thing we do in the new `draw_all` routine is compute the view frustum in world coordinates. We perform a reverse projection to get the four corner points on the near plane (using the formulas from Chapter 2), then call `l3d_viewing_frustum::create_from_points` to create the view frustum, passing the inverse camera transformation matrix as a parameter so that the frustum is computed in world space, not camera space. The XOFF and YOFF constants in the code are pixel offsets from the corner of the screen. Instead of using the extreme upper/lower left/right corners of the screen for the reverse projection, we use points slightly offset towards the center of the screen. For instance, instead of (0,0) at the upper left, we use (2,2). This makes the frustum slightly smaller than the actual screen, to allow for minor numerical inaccuracy in the clipping code. The reason we make the frustum smaller than that clipping polygons against the frustum is mathematically equivalent to 2D clipping to the view window, as we noted earlier. But smaller numerical errors in clipping computations can lead to clipped vertices which lie slightly outside the frustum. By artificially making the frustum smaller with the XOFF and YOFF