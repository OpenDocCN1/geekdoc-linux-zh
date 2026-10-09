# Chapter 2: Rendering and Animation Techniques for 3D Polygons

```
if (!p_poly->get_scache()->find_texdata(p_poly->texture->tex_data)) {

if (glIsTexture(p_poly->texture->tex_data->id)) {

glDeleteTextures(1, &glid);
}

glGenTextures(1, & glid );
p_poly->texture->tex_data->id = glid;

glBindTexture(GL_TEXTURE_2D, p_poly->texture->tex_data->id);

glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_NEAREST);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_NEAREST);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);

glHint(GL_PERSPECTIVE_CORRECTION_HINT, GL_NICEST);
glEnable(GL_TEXTURE_2D);

glTexImage2D(GL_TEXTURE_2D,
0,
GL_RGBA,
p_poly->texture->tex_data->width,
p_poly->texture->tex_data->height,
0,
GL_RGBA,
GL_UNSIGNED_BYTE,
p_poly->texture->tex_data->data);
} else {

glBindTexture(GL_TEXTURE_2D, p_poly->texture->tex_data->id);
}

// - based on texture orientation: compute uvz's for each vertex
for(int i=0; i<p_poly->clip_ivertices->num_items; ++i) {

float px =
( (*p_poly->vlist) [(*p_poly->clip_ivertices)[i].ivertex].transformed_X_
- *screen_xsize/2 )
/ ( *screen_xsize * *f0vx);

float py =
(*screen_ysize/2
- (*p_poly->vlist) [(*p_poly->clip_ivertices)[i].ivertex].transformed_Y_ )
/
(*screen_ysize * *f0vy);

float ox = p_poly->texture->o.transfomed_X_;
float oy = p_poly->texture->o.transfomed_Y_;
float oz = p_poly->texture->o.transfomed_Z_;
float ux = p_poly->texture->v.transfomed_X_ - oX;
float uy = p_poly->texture->v.transfomed_Y_ - oY;
float uz = p_poly->texture->v.transfomed_Z_ - oZ;
float vx = p_poly->texture->t.transfomed_X_ - oX;
float vy = p_poly->texture->t.transfomed_Y_ - oY;
float vz = p_poly->texture->t.transfomed_Z_ - oZ;

float u = (px*(oy*vz - oz*vy) + py*(oz*vx - ox*vz) - oy*vx + ox*vy) / 
( px*(uz*vy - uy*vz) + py*(ux*vz - uz*vx) + uy*vx - ux*vy);

```

TEAM LinG - Live, Informative, Non-cost and Genuine!