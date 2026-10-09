```
13d_polygon_ivertex *
swap_iv =
&(((*target->polygons[polygon_idx]->ivertices))
[target->polygons[polygon_idx]->next_index()]);
for(i=0; i<numv/2; i++) {
*swap_iv = *((*target->polygons[polygon_idx]->ivertices))[i];
(*(*target->polygons[polygon_idx]->ivertices))[i] =
(*(*target->polygons[polygon_idx]->ivertices))[numv-1 - i];
(*(*target->polygons[polygon_idx]->ivertices))[numv-1 - i] =
*swap_iv;

// don't swap the tex coords (i.e. swap them back)
if(fp_texcoord) {
((13d_polygon_ivertex_textured *)
( & (*(*target->polygons[polygon_idx]->ivertices))[numv-1 - i]))
->tex_coord =
((13d_polygon_ivertex_textured *)
( & (*(*target->polygons[polygon_idx]->ivertices))[i]))
->tex_coord;

((13d_polygon_ivertex_textured *)
( & (*(*target->polygons[polygon_idx]->ivertices))[i]))
->tex_coord =
((13d_polygon_ivertex_textured *)swap_iv)->tex_coord;
}

if(fp_texcoord) {
((13d_polygon_ivertex_textured *)swap_iv)->tex_coord =
((13d_polygon_ivertex_textured *)
( & (*(*target->polygons[polygon_idx]->ivertices))[0 ]))
->tex_coord;
for(i=0; i<numv-1; i++) {

((13d_polygon_ivertex_textured *)
( & (*(*target->polygons[polygon_idx]->ivertices))[i ]))
->tex_coord =
((13d_polygon_ivertex_textured *)
( & (*(*target->polygons[polygon_idx]->ivertices))[i+1 ]))
->tex_coord;

((13d_polygon_ivertex_textured *)
( & (*(*target->polygons[polygon_idx]->ivertices))[i ]))->tex_coord =
((13d_polygon_ivertex_textured *)swap_iv)->tex_coord;
}

target->polygons[polygon_idx]->ivertices->num_items =
target->polygons[polygon_idx]->ivertices->num_items - 1;

p->texture = new 13d_texture;
p->texture->tex_data = mesh->tex_data;
p->texture->owns_tex_data = false;

// no texture coord file found, so assign default tex coordinates
if(!fp_texcoord)
```