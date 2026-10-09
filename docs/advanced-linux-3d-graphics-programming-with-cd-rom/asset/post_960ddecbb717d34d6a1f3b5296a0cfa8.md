
# Chapter 8: Non-Graphical Techniques for Games and Interactive Environments

```cpp
objects[new_onum]->polygons[p_idx]->compute_sfcnormal();

pt->compute_surface_orientation_and_size();

pt->plane_align_with_point_normal(pt->center_original, normalized(pt->sfcnormal_original -
    pt->center_original));
}
else if(strcmp(s, "GEOMPOLY_TEX") == 0) {
int num_vtx;

l3d_polygon_3d_textured_lightmapped_collidable *pt;
s = strtok(NULL, " ");
    sscanf(s, "%d", &num_vtx);
objects[new_onum]->polygons[p_idx] =
pt =
    new l3d_polygon_3d_textured_lightmapped_collidable
    (num_vtx, scache);
objects[new_onum]->polygons[p_idx]->vlist = &objects[new_onum]->vertices;

for(int vtx = 0; vtx < num_vtx; vtx++) {
s = strtok(NULL, " ");
    int iv;

    sscanf(s, "%d", &iv);

(*objects[new_onum]->polygons[p_idx]->vertices)[iv - 1]
objects[new_onum]->polygons[p_idx]->vertices->next_index()->ivertex = iv;
}
s = strtok(NULL, " ");

pt->fov_x = &(camera->fov_x);
pt->fov_y = &(camera->fov_y);
pt->screen_xsize = &(screen->xsize);
pt->screen_ysize = &(screen->ysize);

int tex_id;
sscanf(s, "%d", &tex_id);
pt->texture = new l3d_texture;
pt->texture->tex_data = &tex_data[tex_id];
pt->texture->owns_tex_data = false;
float x, y, z;
s = strtok(NULL, " ");
sscanf(s, "%f", &x);
s = strtok(NULL, " ");
sscanf(s, "%f", &y);
s = strtok(NULL, " ");
sscanf(s, "%f", &z);

pt->texture->o_original.set(float_to_l3d_real(x),
    float_to_l3d_real(y),
    float_to_l3d_real(z),
    int_to_l3d_real(1));

s = strtok(NULL, " ");
sscanf(s, "%f", &x);
s = strtok(NULL, " ");
sscanf(s, "%f", &y);
s = strtok(NULL, " ");
sscanf(s, "%f", &z);
pt->texture->v_original.set(float_to_l3d_real(x),
    float_to_l3d_real(y),
    float_to_l3d_real(z),
    int_to_l3d_real(1));

objects[new_onum]->polygons[p_idx]->compute_center();
objects[new_onum]->polygons[p_idx]->compute_sfcnormal();

pt->compute_surface_orientation_and_size();

pt->plane_align_with_point_normal(pt->center_original, normalized(pt->sfcnormal_original -
    pt->center_original));

} else {
int num_vtx;

s = strtok(NULL, " ");
sscanf(s, "%d", &num_vtx);
objects[new_onum]->polygons[p_idx] = new l3d_polygon_3d_portal_collidable(num_vtx);
objects[new_onum]->polygons[p_idx]->vlist = &objects[new_onum]->vertices;
for(int vtx=0; vtx<num_vtx; vtx++) {
s = strtok(NULL, " ");
int iv;
sscanf(s, "%d", &iv);
(*objects[new_onum]->polygons[p_idx]->vertices)[iv - 1]
objects[new_onum]->polygons[p_idx]->vertices->next_index()->ivertex = iv;
}
objects[new_onum]->polygons[p_idx]->compute_center();
objects[new_onum]->polygons[p_idx]->compute_sfcnormal();

s = strtok(NULL, " ");
char *s2 = s + strlen(s)-1;
while(*s2=='}' || *s2==' ') {*s2=0; s2--; }
l3d_polygon_3d_portal *pp;
pp = dynamic_cast<l3d_polygon_3d_portal *>(objects[new_onum]->polygons[p_idx]);
if(pp) strcpy(pp->connected_sector_name, s);
}
}

}else if(strcmp(keyword,"ACTOR")==0) {
int new_onum;

objects[new_onum = objects.next_index()]
= (*current_sector->objects)[current_sector->objects->next_index()]
= new l3d_object_clipable_boundable_collidable(100);
strcpy(objects[new_onum]->name, sname);
strcpy(objects[new_onum]->plugin_name, plugin_name);
objects[new_onum]->parent = current_sector;

if(strlen(plugin_name)) {

    objects[new_onum]->plugin_loader = 

        factory_manager_v_0_4_4.plugin_loader_factory->create();

    objects[new_onum]->plugin_loader->load(plugin_name);

    objects[new_onum]->plugin_constructor = 

        (void (*)(l3d_object *, void *))

        objects[new_onum]->plugin_loader->find_symbol("constructor");

    objects[new_onum]->plugin_update = 

        (void (*)(l3d_object *))

        objects[new_onum]->plugin_loader->find_symbol("update");

    objects[new_onum]->plugin_destructor = 

        (void (*)(l3d_object *))

        objects[new_onum]->plugin_loader->find_symbol("destructor");

    objects[new_onum]->plugin_copy_data = 

        (void (*)(const l3d_object *, l3d_object *))

        objects[new_onum]->plugin_loader->find_symbol("copy_data");

    l3d_plugin_environment *e = new l3d_plugin_environment

        (texture_loader, screen->sinfo, scache, rest_params);

    if(objects[new_onum]->plugin_constructor) {

        (*objects[new_onum]->plugin_constructor) (objects[new_onum], e);

    }
} else if(strcmp(keyword,"CAMERA")==0) {

    float posx,posy,posz;

    float xaxis_x, xaxis_y, xaxis_z,

        yaxis_x, yaxis_y, yaxis_z,

        zaxis_x, zaxis_y, zaxis_z;

    char *tok;

    tok = strtok(rest_params, " "); 

    if(tok) {sscanf(tok, "%f", &posx);}

    tok = strtok(NULL, " "); 

    if(tok) {sscanf(tok, "%f", &posy);}

    tok = strtok(NULL, " "); 

    if(tok) {sscanf(tok, "%f", &posz);}

    tok = strtok(NULL, " "); 

    if(tok) {sscanf(tok, "%f", &xaxis_x);}

    tok = strtok(NULL, " "); 

    if(tok) {sscanf(tok, "%f", &xaxis_y);}

    tok = strtok(NULL, " "); 

    if(tok) {sscanf(tok, "%f", &xaxis_z);}

    tok = strtok(NULL, " "); 

    if(tok) {sscanf(tok, "%f", &yaxis_x);}

    tok = strtok(NULL, " "); 

    if(tok) {sscanf(tok, "%f", &yaxis_y);}

    tok = strtok(NULL, " "); 

    if(tok) {sscanf(tok, "%f", &yaxis_z);}

    tok = strtok(NULL, " "); 

    if(tok) {sscanf(tok, "%f", &zaxis_x);}

    tok = strtok(NULL, " "); 

    if(tok) {sscanf(tok, "%f", &zaxis_y);}

    tok = strtok(NULL, " "); 

    if(tok) {sscanf(tok, "%f", &zaxis_z);}

    this->current_sector = current_sector;

    camera->WVP.set(float_to_l3d_real(posx),

        float_to_l3d_real(posy),

        float_to_l3d_real(posz),

        int_to_l3d_real(1));

    camera->pCalculate_viewing_xform();
}

for(int i=0; i<objects.num_items; i++) {

    for(int pi=0; pi<objects[i]->polygons.num_items; pi++) {

        l3d_polygon_3d_portal *p;

        if ((p = dynamic_cast<l3d_polygon_3d_portal *>(objects[i]->polygons[pi])) )
            p->connected_sector = sector_by_name(p->connected_sector_name);
    }
}
```

TEAM LinG – Live, Informative, Non-cost and Genuine!

### Plug-in Object Seeker, Class l3d_plugin_videoscape_mesh_seeker

Class `l3d_plugin_videoscape_mesh_seeker` is a plug-in data class used by the plug-in `seeker.so`. The seeker plug-in is an object which randomly moves about the environment, giving the appearance of seeking something. Real seeking behavior for a specific target could also be programmed into the update routine.

Member variables `plugin_env`, `tex_data`, `mesh_fname`, `texcoord_fname`, and `texture_fname` are the same as with the Videoscape plug-in `vidmesh`.

Enumeration `movement_states` defines the allowable movement states for the seeker. `NONE` means no movement; the `AROUND_` states indicate rotation around one of the seeker’s local coordinate axes; and the `ALONG_` states indicate movement in the direction of one of the seeker’s local coordinate axes.

Member variable `tick_count` is a count of frames indicating how long the current movement state has been executed.

Member variable `max_ticks` is a count of frames indicating the duration of the current movement state.

Member variable `turning_velocity` represents how rapidly the object rotates about its current rotation axis, in degrees per frame.

Member variable `moving_velocity` represents how rapidly the object moves along its current movement axis, in world units per frame. Note that the use of frame-based velocities is not physically realistic; see the particle system program in Chapter 7 and the section titled “Physics” for information on more physically realistic simulation.

The plug-in constructor is identical to the `vidmesh` constructor, except it also specifies a bounding sphere for collision detection purposes.

The plug-in `update` function handles object movement and collision detection. Object movement is handled by extracting the axes of the local object coordinate system from the object’s composite transformation matrix. To do this, we interpret the matrix as a coordinate system and use the first three columns of the matrix as the vectors VRI, VUP, and VFV, and the last column as VRP. Then, based on the current movement state, we multiply the current rotation matrix with a new matrix for the new rotation or translation, and save the new matrix as the composite transformation matrix. Contrast this orientation and movement method with the approach of the camera, which explicitly stored orientation as VRI, VUP, and VFV vectors. As we now see, these vectors can also be extracted from a transformation matrix, and do not need to be stored explicitly (though we might still want to for clarity).
