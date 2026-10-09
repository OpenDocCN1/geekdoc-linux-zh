```
```
13d_rasterizer_2d rast(rast_imp);

rast_imp->O = pt->surface_orientation.O.transformed;
rast_imp->U = pt->surface_orientation.U.transformed - rast_imp->O;
rast_imp->V = pt->surface_orientation.V.transformed - rast_imp->O;

13d_polygon_2d flatshaded *(lightmap_poly);
13d_two_part_list<13d_coordinate> *vlist;
vlist = new 13d_two_part_list<13d_coordinate>
    (pt->clip_ivertices, num_items);

int i;
lightmap_poly = new 13d_polygon_2d_flatshaded
    (pt->clip_ivertices, num_items);
lightmap_poly->vlist = &vlist;
for(i=0; i< pt->clip_ivertices->num_items; i++) {
  13d_point tex_coord;
  tex_coord =
    world_to_tex_matrix(pt->surface_orientation)
    | camera_inverse_viewing_xform
    [ (*pt->vlist) [ *(*pt->clip_ivertices)[i].iverterx ].transformed;

if(tex_coord.W_ != int_to_13d_real(1)) {
  13d_real inw = 13d_divint(int_to_13d_real(1), tex_coord.W_);
  tex_coord.X = 13d_mulrint(tex_coord.X_, inw);
  tex_coord.Y = 13d_mulrint(tex_coord.Y_, inw);
  tex_coord.Z = 13d_mulrint(tex_coord.Z_, inw);
  tex_coord.W = int_to_13d_real(1);
}

13d_real ul, vl;
ul = 13d_mulri(tex_coord.X_, pt->lightmap->tex_data->width);
vl = 13d_mulri(tex_coord.Y_, pt->lightmap->tex_data->height);

13d_coordinate vtx;
vtx.transformed.set
  (ul, vl,
   int_to_13d_real(0),
   int_to_13d_real(1));

(*vlist)[i] = vtx;
(*lightmap_poly->clip_ivertices)
[lightmap_poly->clip_ivertices->next_index()] .iverterx = i;

}

lightmap_poly->final_color = 255;
lightmap_poly->draw(&rast);

delete vlist;
delete lightmap_poly;
delete si;
delete rast_imp;
}
   n = n->next;
}

recursolevel--;
```
```