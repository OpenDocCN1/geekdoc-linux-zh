```
glPixelStorei(GL_UNPACK_ALIGNMENT, 1);

fontOffset = glGenLists(128);
for (i = 0, j = 'A'; i < 26; i++, j++) {
    glNewList(fontOffset + j, GL_COMPILE);
    glBitmap(8, 13, 0.0, 2.0, 10.0, 0.0,
             letters[i]);
    glEndList();
}
for (i = 0, j = 'a'; i < 26; i++, j++) {
    glNewList(fontOffset + j, GL_COMPILE);
    glBitmap(8, 13, 0.0, 2.0, 10.0, 0.0,
             letters[i]);
    glEndList();
}
for (i = 0, j = '0'; i < 10; i++, j++) {
    glNewList(fontOffset + j, GL_COMPILE);
    glBitmap(8, 13, 0.0, 2.0, 10.0, 0.0,
             digits[i]);
    glEndList();
}



    glNewList(fontOffset + ' ', GL_COMPILE);
    glBitmap(8, 13, 0.0, 2.0, 10.0, 0.0,
             space);
    glEndList();

    glNewList(fontOffset + '.', GL_COMPILE);
    glBitmap(8, 13, 0.0, 2.0, 10.0, 0.0,
             period);
    glEndList();

```

```
void l3d_rasterizer_3d_mesa_imp::raw_text(int x, int y, const char *string) {
  sinfo->set_color(text_color);
  glDisable(GL_TEXTURE_2D); //: text should not be displayed using a texture
  glRasterPos2f(x-(xsize>>1),(ysize>>1)- 13); //: 13 is height of 1 char
  glPushAttrib (GL_LIST_BIT);
  glListBase(fontOffset);
  glCallLists((GLsizei) strlen(string), GL_UNSIGNED_BYTE, (GLubyte *) string);
  glPopAttrib ();
}


void l3d_rasterizer_3d_mesa_imp::set_text_color(int red, int green, int blue) {
  text_color = sinfo->next_to_natives(red, green, blue);
}


void l3d_rasterizer_3d_mesa_imp::draw_polygon_textured_lightmapped
(const l3d_polygon_3d_textured_lightmapped *p_poly)
{
  GLuint glid = ((GLuint) (p_poly->texture->tex_data->id));

  l3d_list<l3d_point> old_texcoords(10);

  //: try to find texture data in surface cache
```