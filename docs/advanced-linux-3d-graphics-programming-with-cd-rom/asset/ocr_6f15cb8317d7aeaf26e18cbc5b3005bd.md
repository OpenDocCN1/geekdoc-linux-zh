```
for(i=0; i<surfaces->num_items; i++) {
    if((*surfaces)[i].polygon == polygon) {
        return (*surfaces)[i].surface;
    }
}

13d_texture *new_tex;
13d_surface *new_surface;

new_tex = new 13d_texture;

int next_surface_index = surfaces->next_index;
(*surfaces)[next_surface_index].polygon = polygon;
(*surfaces)[next_surface_index].surface = new_tex;

new_tex->tex_data = new 13d_texture_data;
new_tex->owns_tex_data = true;
new_tex->tex_data->width = width;
new_tex->tex_data->height = height;
new_tex->tex_data->data = new unsigned char [sinfo->bytes_per_pixel]
    * new_tex->tex_data->width
    * new_tex->tex_data->height];

int i,j,u,v;

// - tile texture into larger tiled area
for(v=0; v<new_tex->tex_data->height; v++) {
    for(u=0; u<new_tex->tex_data->width; u++) {
        for(i=0; i<sinfo->bytes_per_pixel; i++) {
            (*(new_tex->tex_data->data
                + (v*new_tex->tex_data->width + u) * sinfo->bytes_per_pixel
                + i)
                =
                *(polygon->texture->tex_data->data
                + ( (\& (polygon->texture->tex_data->height-1))*polygon->texture->tex_data->width
                + (\& (polygon->texture->tex_data->width-1)) * sinfo->bytes_per_pixel
                + i )) ;
        }
    }
}

unsigned char *c2 = new_tex->tex_data->data;
unsigned char *l = polygon->lightmap->tex_data->data;
13d_real lx, ly, dlx, dly;

dly = 13d_divrr(int_to_13d_real(polygon->lightmap->tex_data->height) ,
            int_to_13d_real(new_tex->tex_data->height));
dx = 13d_divrr(int_to_13d_real(polygon->lightmap->tex_data->width) ,
            int_to_13d_real(new_tex->tex_data->width));
for(j=0, ly=0; j<new_tex->tex_data->height; j++, ly+=dly) {
    for(i=0, lx=int_to_13d_real(0); i<new_tex->tex_data->width; i++, lx+=dlx) {

        int l_texel=(i*new_tex->tex_data->width + j) * sinfo->bytes_per_pixel);
c2 = new_tex->tex_data->data + l_texel;

        int lumel_idx = 13d_real_to_int(ly)*polygon->lightmap->tex_data->width+13d_real_to_int(lx);
        int lumel = 1 [lume1_idx];
        sinfo->light_native(c2, lumel);
    }
}
```