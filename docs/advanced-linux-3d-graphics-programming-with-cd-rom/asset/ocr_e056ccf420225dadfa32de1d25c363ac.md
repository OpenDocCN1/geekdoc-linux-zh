```
surface_orientation_0.original.set(0,X + U.X *minu + V.X *minv,
0,Y + U.Y *minu + V.Y *minv,
0,Z + U.Z *minu + V.Z *minv,
int_to_13d_real (1));
surface_orientation_0.original.set(0,X + U.X *maxu + V.X *minv,
0,Y + U.Y *maxu + V.Y *minv,
0,Z + U.Z *maxu + V.Z *minv,
int_to_13d_real (1));
surface_orientation_0.original.set(0,X + U.X *minu + V.X *maxv,
0,Y + U.Y *minu + V.Y *maxv,
0,Z + U.Z *minu + V.Z *maxv,
int_to_13d_real (1));

assign_tex_coords_from_tex_space (surface_orientation);

void 13d_polygon_3d_textured_lightmapped::init_transformed (void) {
13d_polygon_3d_textured ::init_transformed();

surface_orientation_0.transformed = surface_orientation_0.original;
surface_orientation_U.transformed = surface_orientation_U.original;
surface_orientation_V.transformed = surface_orientation_V.original;
}

void 13d_polygon_3d_textured_lightmapped::transform (const 13d_matrix &m, int count) {
13d_polygon_3d_textured::transform(m,count);

surface_orientation_0.transformed = m surface_orientation_0.transformed;
surface_orientation_U.transformed = m surface_orientation_U.transformed;
surface_orientation_V.transformed = m surface_orientation_V.transfomed;
}

13d_polygon_2d& 13d_polygon_3d_textured_lightmapped::clone (void) {
return new 13d_polygon_3d_textured_lightmapped (*this);
}

13d_polygon_3d_textured_lightmapped::13d_polygon_3d_textured_lightmapped
(const 13d_polygon_3d_textured_lightmapped &r)
: 13d_polygon_2d (r),
13d_polygon_3d(r),
13d_polygon_3d_textured (r),
13d_polygon_3d_clipable(r),
13d_texture_computer(r)
{
sCache = r.scache;
surface = r.surface;
surface_orientation = r.surface_orientation;
surface_xsize = r.surface_xsize;
surface_ysize = r.surface_ysize;
lightmap = r.lightmap;
}
```

The member variable `scache` is a pointer to the surface cache responsible for managing the surface of the polygon. The member variable `lightmap` points to the light map, which is a small texture containing light intensities. The member variable `surface` points to the surface itself, which contains the tiled and lighted version of the texture. The surface is created by the surface cache, which is also responsible for deleting the surface.