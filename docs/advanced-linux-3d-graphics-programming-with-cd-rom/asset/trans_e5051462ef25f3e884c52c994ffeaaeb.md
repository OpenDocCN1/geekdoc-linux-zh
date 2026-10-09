

```cpp
for(i=0; i<surfaces->num_items; i++) {
    if((*surfaces)[i].polygon == polygon) {
        return (*surfaces)[i].surface;
    }
}

l3d_texture *new_tex;
l3d_surface *new_surface;

new_tex = new l3d_texture;

int next_surface_index = surfaces->next_index;
(*surfaces)[next_surface_index].polygon = polygon;
(*surfaces)[next_surface_index].surface = new_tex;

new_tex->tex_data = new l3d_texture_data;
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
                + ( (u & (polygon->texture->tex_data->width-1))) *polygon->texture->tex_data->width
                + (v & (polygon->texture->tex_data->height-1)) * sinfo->bytes_per_pixel
                + i )) ;
        }
    }
}

unsigned char *c2 = new_tex->tex_data->data;
unsigned char *l = polygon->lightmap->tex_data->data;
l3d_real lx, ly, dlx, dly;

dly = l3d_divrr(int_to_l3d_real(polygon->lightmap->tex_data->height) ,
            int_to_l3d_real(new_tex->tex_data->height));
dlx = l3d_divrr(int_to_l3d_real(polygon->lightmap->tex_data->width) ,
            int_to_l3d_real(new_tex->tex_data->width));
for(j=0, ly=0; j<new_tex->tex_data->height; j++, ly+=dly) {
    for(i=0, lx=int_to_l3d_real(0); i<new_tex->tex_data->width; i++, lx+=dlx) {

        int l_texel = (i*new_tex->tex_data->width + j) * sinfo->bytes_per_pixel;
        c2 = new_tex->tex_data->data + l_texel;

        int lumel_idx = int_to_l3d_real(ly)*polygon->lightmap->tex_data->width + int_to_l3d_real(lx);
        int lumel = l[lumel_idx];
        sinfo->light_notice(c2, lumel);
    }
}

return new_tex;
}

l3d_texture_data *l3d_surface_cache::
find_texdata(l3d_texture_data *texdata)
{
int i;

for(i=0; i<surfaces->num_items; i++) {
  if((*surfaces)[i].surface->tex_data == texdata)
    return (*surfaces)[i].surface->tex_data;
}

l3d_texture *new_tex;
l3d_surface *new_surface;

new_tex = new l3d_texture;

int next_surface_index = surfaces->next_index();
(*surfaces)[next_surface_index].polygon = NULL;
(*surfaces)[next_surface_index].surface = new_tex;

new_tex->tex_data = texdata;
new_tex->owns_tex_data = false;
return new_tex;
}
```

## 表面缓存

表面缓存负责管理已创建的 surface（表面）。每当关联的多边形第一次被绘制时，我们就会创建一个 surface。由于创建 surface 是一个耗时的过程（必须复制纹理数据并与光照贴图结合），我们在表面缓存中保存已创建的 surface，以便后续重复使用。

类 `l3d_surface_cache` 是实现表面缓存的类。成员变量 `sinfo` 指向屏幕信息对象，以便我们知道纹理数据的像素格式。成员变量 `surfaces` 是指向 surface 对象指针的列表。方法 `reset` 从缓存中删除所有 surface，从而重置缓存，并使所有 surface 在需要时重新生成。方法 `find_texdata` 在缓存中搜索特定的纹理数据对象，如果找到则返回指向该数据的指针；如果未找到，则将其插入缓存并返回 `NULL`。

方法 `combine_lightmap_and_texmap` 将光照贴图与纹理贴图结合，返回指向新纹理的指针。该方法以宽度和高度为参数，这两个参数必须是平铺后纹理（pre-tiled texture）的新尺寸，可能会比原尺寸大。（我们将在下一节中看到如何计算这些尺寸参数。）首先，我们搜索是否已经创建并缓存了该 surface；如果是，则返回指向现有 surface 的指针。如果没有，则必须创建该 surface。我们通过创建一个指定宽度和高度的新纹理来实现这一点，请记住，该纹理可能比原始纹理尺寸大，以允许对纹理进行预平铺。然后，我们将原始多边形纹理复制到新分配的纹理中，必要时重复纹理。接着，我们遍历这个预平铺纹理的所有 texel（纹理素），同时步进光照贴图中的 lumel（光照素）。这是一个简单的缩放操作；我们只需将光照贴图拉伸到预平铺纹理的尺寸。注意，由于光照贴图的分辨率低于纹理贴图，多个 texel 将映射到一个 lumel。对于每个 texel，我们调用 `l3d_screen_info::light_notice`，传入对应 lumel 的强度；这将改变 texel 的颜色以匹配给定的光照级别。

关于如何计算预平铺纹理的尺寸的问题仍未解决。正如我们所说，这取决于原始纹理尺寸与纹理所映射的多边形尺寸之间的相对大小。类 `l3d_polygon_3d_textured_lightmapped` 中的例程 `compute_surface_orientation_and_size` 专门处理这项任务。因此，让我们现在来看看类 `l3d_polygon_3d_textured_lightmapped`。

## 光照映射多边形

类 `l3d_polygon_3d_textured_lightmapped` 扩展了带纹理的多边形类，以支持光照映射。

**列表 2-21: p3_ltex.h**

```cpp
#ifndef _P3_LTEX_H
#define _P3_LTEX_H
#include "../..//tool_os/memman.h"
#include "p3_tex.h"
#include "../surface/scache.h"

class l3d_polygon_3d_textured_lightmapped :
  virtual public l3d_polygon_3d_textured,
  virtual public l3d_texture_computer
{
  protected:
    l3d_surface_cache *scache;
  public:
    mutable l3d_texture *surface;
    // mutable since the draw routine for s/w rendering needs to assign
    // this member (the tiled, lit surface) if the surface is not currently
    // in the cache, though the poly is otherwise passed as const. Logically
    // the draw routine handles the polygon as a const, physically though
    // it can change the mutable surface member

    l3d_surface_cache *get_scache(void) const {return scache; }

    l3d_texture_space surface_orientation;
    int surface_xsize, surface_ysize;

    l3d_polygon_3d_textured_lightmapped(int num_pts, l3d_surface_cache *scache);

    ~l3d_polygon_3d_textured_lightmapped(void) {
      // DO NOT delete the surface! It belongs to the surface cache,
      // or might not even have been created if h/w accel with Z-pass
      // rendering was used
      delete lightmap;
    }

    l3d_texture *lightmap;

    void compute_surface_orientation_and_size(void);

    void init_transformed(void);
    void transform(const l3d_matrix &m, int count);

    void draw(l3d_rasterizer_3d *r) {
        r->draw_polygon_textured_lightmapped(this);
    }

    l3d_polygon_3d &operator=(const l3d_polygon_3d &r);
    l3d_polygon_2d *clone(void);

};

#endif
```

**列表 2-22: p3_ltex.cc**

```cpp
#include "p3_ltex.h"

#include "../../raster/ras3_sw.h"
#include "../../tool_os/memman.h"

#define EPSILON_VECTOR 0.001

l3d_polygon_3d_textured_lightmapped::l3d_polygon_3d_textured_lightmapped
(int num_pts, l3d_surface_cache *scache):
    l3d_polygon_2d(),
    l3d_polygon_3d(),
    l3d_polygon_3d_clipable(),
    l3d_polygon_3d_textured(num_pts)
{
    this->scache = scache;
    lightmap = new l3d_texture;
    lightmap->tex_data = new l3d_texture_data;
    lightmap->owns_tex_data = true;
    lightmap->tex_data->width = 64;
    lightmap->tex_data->height = 64;
    lightmap->tex_data->data = new unsigned char[lightmap->tex_data->width *
    lightmap->tex_data->height];

    int i, j;
    for(j=0;j<lightmap->tex_data->height;j++) {
        for(i=0;i<lightmap->tex_data->width;i++) {
            lightmap->tex_data->data[i + j*lightmap->tex_data->width] = MAX_LIGHT_LEVELS/4;
        }
    }

    surface = NULL;
}

void l3d_polygon_3d_textured_lightmapped::compute_surface_orientation_and_size
(void)
{
```

