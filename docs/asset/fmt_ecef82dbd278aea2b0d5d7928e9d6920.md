
# 第 2 章：3D 多边形的渲染与动画技术

```cpp
static const GLubyte letters[][13] = {
 {0x0, 0x0, 0x0, 0x60, 0x60, 0x0, 0x30, 0x18, 0xc3, 0x1, 0xc3, 0x3, 0xff},
 {0x0, 0x0, 0x7E, 0xff, 0xc3, 0xc3, 0xc3, 0x7E, 0xc7, 0xc3, 0xc3, 0xc3, 0x27},
 {0x0, 0x0, 0x7E, 0xff, 0xc3, 0x3, 0x3, 0x7F, 0xc3, 0xc3, 0xc3, 0xc3, 0x7E}
 };

static const GLubyte letters[][13] = {
 {0x0, 0x0, 0xc3, 0xc3, 0xc3, 0xc3, 0xff, 0xc3, 0xc3, 0xc3, 0xc3, 0x66, 0xc3c, 0x18},
 {0x0, 0x0, 0xc3, 0xc7, 0xc3, 0xc3, 0xc7, 0xfe, 0xc7, 0xc3, 0xc3, 0xc7, 0xfe},
 {0x0, 0x0, 0xc7, 0xc7, 0xc0, 0xc0, 0xc0, 0xc1, 0xc0, 0xc0, 0xc0, 0x7c, 0x7e},
 {0x0, 0x0, 0xfe, 0xc0, 0xc7, 0xc3, 0xc3, 0xc3, 0xc3, 0xc0, 0xc7, 0xc0, 0xfc},
 {0x0, 0x0, 0xfc, 0xfc, 0xc0, 0xc0, 0xc0, 0xfc, 0xc0, 0xc0, 0xc0, 0xc0, 0xff},
 {0x0, 0x0, 0xc0, 0xc0, 0xc0, 0xc0, 0xc0, 0xc0, 0xfe, 0xc0, 0xc0, 0xc0, 0xff},
 {0x0, 0x0, 0xc7, 0xc7, 0xc3, 0xc3, 0xc3, 0xc1, 0xc3, 0xc3, 0xc3, 0xc0, 0xc0},
 {0x0, 0x0, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc0, 0xc0},
 {0x0, 0x0, 0xc7, 0xc1b, 0xc3, 0x18, 0x18, 0x18, 0x18, 0x18, 0x18, 0x18, 0x7e},
 {0x0, 0x0, 0xc7, 0xc0e, 0xc0e, 0xc6, 0xc0, 0xd6, 0xd0, 0xd6, 0xd8, 0xd6, 0x3e},
 {0x0, 0x0, 0xc3, 0xc6, 0xcc, 0xcc, 0xd8, 0xf0, 0xc3, 0xb8, 0x6c, 0xc3, 0xc3},
 {0x0, 0x0, 0xfc, 0xc0, 0xc0, 0xc0, 0xc0, 0xc0, 0xc0, 0xc0, 0xc0, 0xc0, 0xc0},
 {0x0, 0x0, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xddb, 0xfc, 0x7f, 0x7e, 0xc7},
 {0x0, 0x0, 0xc7, 0xc7, 0xc7, 0xc0, 0xfc, 0xb, 0xc0, 0x1, 0xc3, 0xc3, 0xc3},
 {0x0, 0x0, 0xc7, 0xc7, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc0},
 {0x0, 0x0, 0xc0, 0xc0, 0xc0, 0xc0, 0xc0, 0xc0, 0xc0, 0xc7, 0xc3, 0xc3, 0xc0},
 {0x0, 0x0, 0xf3, 0xd6, 0xc3, 0xfd, 0xd0, 0xc0, 0xc3, 0xc3, 0xc3, 0x66, 0xc3},
 {0x0, 0x0, 0xc3, 0xc0, 0xcc, 0xd8, 0xb, 0xc0, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3},
 {0x0, 0x0, 0xc3, 0xc3, 0xc0, 0xc3, 0xc3, 0xc0, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3},
 {0x0, 0x0, 0xc1, 0xc18, 0x18, 0xc18, 0xc18, 0x18, 0xc18, 0xc18, 0x18, 0x8, 0xff},
 {0x0, 0x0, 0xc7, 0xc7, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3, 0xc0},
 {0x0, 0x0, 0x18, 0xc1b, 0xc3c, 0x7c, 0x6, 0xc6, 0xc0, 0xc3, 0xc3, 0xc3, 0x18},
 {0x0, 0x0, 0xc3, 0xc7, 0xfc, 0xff, 0xd6, 0xd8, 0xc3, 0xc3, 0xc3, 0xc3, 0xc3},
 {0x0, 0x0, 0xc7, 0xc7, 0x6, 0x66, 0xc3, 0x3c, 0x18, 0xc3c, 0xc3, 0xc3, 0xc3},
 {0x0, 0x0, 0x18, 0x8, 0xc18, 0xc18, 0xc18, 0xc18, 0xc3, 0xc3, 0x66, 0xc3},
 {0x0, 0x0, 0xc1, 0xc18, 0x18, 0x18, 0x18, 0x18, 0xc3, 0xc3, 0xc3, 0xc3, 0xc0}
};
```

```cpp
l3d_rasterizer_3d_imp * l3d_rasterizer_3d_mesa_imp_factory::create
(int xs, int ys, l3d_screen_info *si)
{ return new l3d_rasterizer_3d_mesa_imp(xs,ys,si); }

l3d_rasterizer_3d_mesa_imp::
l3d_rasterizer_3d_mesa_imp(int xs, int ys, l3d_screen_info *si):
l3d_rasterizer_3d_imp(xs,ys,si),
l3d_rasterizer_2d_mesa_imp(xs,ys,si)
{
  make_raster_font();
  set_text_color(si->next_max_red,
                 si->next_max_green,
                 si->next_max_blue);

  glMatrixMode(GL_PROJECTION);
  glLoadIdentity();
  gluOrtho2D(-ysize/2., xsize/2., -ysize/2., ysize/2.);

  glMatrixMode(GL_MODELVIEW);
  glLoadIdentity();
  gluViewport(0,0,xsize,ysize);

  // 防止绘制背向多边形——即顶点朝向为逆时针的那些多边形——以模拟软件光栅化器的行为。
  glFrontFace(GL_CCW);
  glCullFace(GL_BACK);
  glEnable(GL_CULL_FACE);
}

void l3d_rasterizer_3d_mesa_imp::clear_buffer(void)
{
   l3d_rasterizer_2d_mesa_imp::clear_buffer();
}

void l3d_rasterizer_3d_mesa_imp::draw_point(int x, int y, unsigned long col) {
   glBegin(GL_POINTS);
   sinfo->set_color(col);
   glVertex2i(x-(xsize>>1), (ysize>>1)-y);
   glEnd();
}

void l3d_rasterizer_3d_mesa_imp::draw_line(int x0, int y0, int x1, int y1,
    unsigned long col)
{
   glBegin(GL_LINES);
   sinfo->set_color(col);
   glVertex2i(x0-(xsize>>1), (ysize>>1)-y0);
   glVertex2i(x1-(xsize>>1), (ysize>>1)-y1);
   glEnd();
}

void l3d_rasterizer_3d_mesa_imp::draw_polygon_flatshaded
(const l3d_polygon_2d_flatshaded *p_poly)
{
   int i;

   glBegin(GL_POLYGON);
   sinfo->set_color(p_poly->final_color);
   for(i=0; i<p_poly->clip_ivertices->num_items; i++) {
      glVertex2i(iceil( (**p_poly->vlist)
         [*(p_poly->clip_ivertices)[i].ivertex].transformed.X )
         - (xsize>>1),
         (ysize>>1) - iceil( (***p_poly->vlist)
         [*(p_poly->clip_ivertices)[i].ivertex].transformed.Y ));
   }
   glEnd();
}

void l3d_rasterizer_3d_mesa_imp::texture_setup
(const l3d_polygon_3d_textured *p_poly)
{
   if (!glIsTexture(p_poly->texture->tex_data->id)) {
      printf("生成纹理");
      GLuint glid = (GLuint) (p_poly->texture->tex_data->id);
      glGenTextures(1, &glid );
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
   }
   else {
      glEnable(GL_TEXTURE_2D); // 纹理化可能已被其他操作关闭
      glBindTexture(GL_TEXTURE_2D, p_poly->texture->tex_data->id);
      float texx[4] = {0.0, 0.0, 1.0, 1.0 };
      float tely[4] = {0.0, 1.0, 1.0, 0.0 };
   }
}

void l3d_rasterizer_3d_mesa_imp::draw_polygon_textured
(const l3d_polygon_3d_textured *p_poly)
{
   texture_setup(p_poly);
   glBegin(GL_POLYGON);
   ogl_texturing_between_glbegin_end(p_poly);
   glEnd();
}

void l3d_rasterizer_3d_mesa_imp::ogl_texturing_between_glbegin_end
(const l3d_polygon_3d_textured *p_poly)
{
   int i;

   GLfloat plane[4];
   l3d_vector plane_normal;

   plane_normal = normalized(p_poly->sfctransformed,
                 - p_poly->center.transformed);

   plane[0] = plane_normal->A[0];
   plane[1] = plane_normal->A[1];
   plane[2] = plane_normal->A[2];
   plane[3] = -plane[0] * p_poly->center.transformed.X
             - plane[1] * p_poly->center.transformed.Y
             - plane[2] * p_poly->center.transformed.Z;

   for(i=0; i<p_poly->clip_ivertices->num_items; i++) {
      #define SCREEN_X (((p_poly->vlist) [(*(p_poly->clip_ivertices)[i].ivertex)].transformed.X))
      #define SCREEN_Y (((p_poly->vlist) [(*(p_poly->clip_ivertices)[i].ivertex)].transformed.Y))

      l3d_real hf=l3d_multi(*fvox, *screen_xsize),
               vf=l3d_multi(*fovy, *screen_ysize);
      float orig_z_denom =
          (plane[0])*(SCREEN_X - xsize/2)/ hf -
          plane[1]* (SCREEN_Y - ysize/2)/ vf +
          plane[2];
      if(orig_z_denom < -0.0001) {
          // 这意味着 orig_z 值小于 0.0001，即为非正值
          // 因此我们取消整个多边形绘制操作
          return;
      }

      l3d_real hf=l3d_multi(*fvox, *screen_xsize),
               vf=l3d_multi(*fovy, *screen_ysize);
      float orig_z = -plane[3] /
          (plane[0])* (SCREEN_X - xsize/2)/ hf -
          plane[1]* (SCREEN_Y - ysize/2)/ vf +
          plane[2]);

      GLfloat tmp[4];

      tmp[0] =
          ((*p_poly->vlist)
          [(*p_poly->clip_ivertices))[i].ivertex].transformed.X - xsize/2)
          * orig_z );

      tmp[1] =
          (-(*p_poly->vlist)
          [(*p_poly->clip_ivertices))[i].ivertex].transformed.Y + ysize/2)
          * orig_z );
      tmp[2] = 1;
      tmp[3] = orig_z;

      glTexCoord2f
      {
        ((l3d_polygon_ivertex_textured *)&(*p_poly->clip_ivertices)[i])
        ->tex_coord.X,
        ((l3d_polygon_ivertex_textured *)&(*p_poly->clip_ivertices)[i])
        ->tex_coord.Y
      };

      glVertex4fv(tmp);
   }
}

void l3d_rasterizer_3d_mesa_imp::make_raster_font(void)
{
    GLuint i, j;
```
