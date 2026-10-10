
```cpp
#include "shapes.h"
#include "../lib/tool_os/memman.h"
#include <stdlib.h>
#include <string.h>

pyramid::pyramid(l3d_texture_loader *l):
    l3d_object(4)
{
    (*vertices)[0].original.set(float_to_l3d_real(0.0),float_to_l3d_real(0.0),float_to_l3d_real(0.0),
    float_to_l3d_real(1.0));
    (*vertices)[1].original.set(float_to_l3d_real(10.0),float_to_l3d_real(0.0),float_to_l3d_real(0.0),
    float_to_l3d_real(1.0));
    (*vertices)[2].original.set(float_to_l3d_real(0.0),float_to_l3d_real(10.0),float_to_l3d_real(0.0),
    float_to_l3d_real(1.0));
    (*vertices)[3].original.set(float_to_l3d_real(0.0),float_to_l3d_real(0.0),float_to_l3d_real(10.0),
    float_to_l3d_real(1.0));
    l3d_polygon_3d_textured *p;
    int pi;

pi = polygons.next_index();
polygons[pi] = p = new l3d_polygon_3d_textured(3);

polygons[pi]->vlist = &vertices;
(*polygons[pi]->vertices)[0][polygons[pi]->vertices->next_index()]].ivertex=0;
(*polygons[pi]->vertices)[0][polygons[pi]->vertices->next_index()]].ivertex=1;
(*polygons[pi]->vertices)[0][polygons[pi]->vertices->next_index()]].ivertex=3;

l->load("test.ppm");
p->texture = new l3d_texture;
p->texture->tex_data = new l3d_texture_data;
p->texture->tex_data->width = l->width;
p->texture->tex_data->height = l->height;
p->texture->tex_data->data = l->data;
p->texture->owns_tex_data = true;
p->texture->o0 = ((*polygons[pi]->vlist)[(*polygons[pi]->vertices)[0]].ivertex];
p->texture->v0 = ((*polygons[pi]->vlist)[(*polygons[pi]->vertices)[1]].ivertex];
p->texture->v1 = ((*polygons[pi]->vlist)[(*polygons[pi]->vertices)[2]].ivertex];
polygons[pi]->compute_center(); polygons[pi]->compute_sfcmormal();
p->assign_tex_coords_from_tex_space(*p->texture);

pi = polygons.next_index();
polygons[pi] = p = new l3d_polygon_3d_textured(3);
polygons[pi]->vlist = &vertices;

(*polygons[pi]->vertices)[0][polygons[pi]->vertices->next_index()]].ivertex=2;
(*polygons[pi]->vertices)[0][polygons[pi]->vertices->next_index()]].ivertex=3;
(*polygons[pi]->vertices)[0][polygons[pi]->vertices->next_index()]].ivertex=1;

p->texture = new l3d_texture;
p->texture->tex_data = new l3d_texture_data;
p->texture->tex_data->width = l->width;
p->texture->tex_data->height = l->height;
p->texture->tex_data->data = l->data;
p->texture->owns_tex_data = false;

p->texture->O = (**(polygons[pi]->vlist))[(*(polygons[pi]->ivertices))[0].ivertex];
p->texture->U = (**(polygons[pi]->vlist))[(*(polygons[pi]->ivertices))[1].ivertex];
p->texture->V = (**(polygons[pi]->vlist))[(*(polygons[pi]->ivertices))[2].ivertex];

polygons[pi]->compute_center(); polygons[pi]->compute_sfnormal();
p->assign_tex_coords_from_tex_space(p->texture);

pi = polygons.next_index();
polygons[pi] = p = new l3d_polygon_3d_textured(3);
polygons[pi]->vlist = &vertices;
(*(polygons[pi]->ivertices))[0]polygons[pi]->ivertices->next_index()[].ivertex=0;
(*(polygons[pi]->ivertices))[1]polygons[pi]->ivertices->next_index()[].ivertex=2;
(*(polygons[pi]->ivertices))[2]polygons[pi]->ivertices->next_index()[].ivertex=1;

p->texture = new l3d_texture;
p->texture->tex_data = new l3d_texture_data;
p->texture->tex_data->width = T->width;
p->texture->tex_data->height = l->height;
p->texture->tex_data->data = l->data;
p->texture->owns_tex_data = false;

p->texture->O = (**(polygons[pi]->vlist))[(*(polygons[pi]->ivertices))[0].ivertex];
p->texture->U = (**(polygons[pi]->vlist))[(*(polygons[pi]->ivertices))[1].ivertex];
p->texture->V = (**(polygons[pi]->vlist))[(*(polygons[pi]->ivertices))[2].ivertex];

polygons[pi]->compute_center(); polygons[pi]->compute_sfnormal();
p->assign_tex_coords_from_tex_space(p->texture);

pi = polygons.next_index();
polygons[pi] = p = new l3d_polygon_3d_textured(3);
polygons[pi]->vlist = &vertices;
(*(polygons[pi]->ivertices))[0]polygons[pi]->ivertices->next_index()[].ivertex=0;
(*(polygons[pi]->ivertices))[1]polygons[pi]->ivertices->next_index()[].ivertex=2;
(*(polygons[pi]->ivertices))[2]polygons[pi]->ivertices->next_index()[].ivertex=0;

p->texture = new l3d_texture;
p->texture->tex_data = new l3d_texture_data;
p->texture->tex_data->width = T->width;
p->texture->tex_data->height = l->height;
p->texture->tex_data->data = l->data;
p->texture->owns_tex_data = false;

p->texture->O = (**(polygons[pi]->vlist))[(*(polygons[pi]->ivertices))[0].ivertex];
p->texture->U = (**(polygons[pi]->vlist))[(*(polygons[pi]->ivertices))[1].ivertex];
p->texture->V = (**(polygons[pi]->vlist))[(*(polygons[pi]->ivertices))[2].ivertex];

polygons[pi]->compute_center(); polygons[pi]->compute_sfnormal();
p->assign_tex_coords_from_tex_space(p->texture);

num_xforms = 2;
xtheta=0;
modeling_xforms[0] = l3d_mat_rot(xtheta);
modeling_xforms[1].set
( float_to_l3d_real(1.), float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(0.),
  float_to_l3d_real(0.), float_to_l3d_real(1.), float_to_l3d_real(0.), float_to_l3d_real(0.),
  float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(1.), float_to_l3d_real(0.),
  float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(1.), float_to_l3d_real(0.));
```

## 清单 2-15：`pyramid.cc`，程序 `textest` 中自定义金字塔类的实现

```cpp
float_to_13d_real(0.), float_to_13d_real(0.), float_to_13d_real(0.), float_to_13d_real(1.))} ;

modeling_xform=
    modeling_xforms[1] | modeling_xforms[0];
}

pyramid::pyramid(void)
{
}

int pyramid::update(void) {
    xtheta += dx_theta; if (xtheta>359) xtheta-=360;
    modeling_xforms[0]=13d_mat_rotx(xtheta);
    modeling_xform=
        modeling_xforms[1] | modeling_xforms[0];
}
```

## 清单 2-16：`textest.h`，程序 `textest` 中自定义世界类的声明

```cpp
#ifndef __TEXTTEST_H
#define __TEXTTEST_H

#include "../lib/geom/world/world.h"
#include "../lib/pipeline/pi_war.h"
#include "../lib/geom/texture/texture.h"
#include "../lib/geom/texture/texture_cl_ppm.h"

class my_world:public 13d_world {
public:
    my_world(void);
    void update_all(void);
    virtual ~my_world() {delete texture_loader;}
    13d_texture_loader *texture_loader;
};

#endif
```

## 清单 2-17：`textest.cc`，程序 `textest` 中自定义世界类的实现

```cpp
#include "textest.h"

#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <math.h>
#include <stdarg.h>

#include "../lib/geom/object/object3d.h"
#include "../lib/tool_2d/screen.h"
#include "../lib/tool_os/dispatch.h"
#include "../lib/raster/rasterize.h"
#include "../lib/tool_2d/scriinfo.h"
#include "../lib/geom/world/world.h"
#include "../lib/geom/texture/texture.h"
#include "../lib/geom/texture/texture_cl_ppm.h"

#include "shapes.h"

void my_world::update_all(void) {
    13d_world::update_all();
}

my_world::my_world(void)
: 13d_world(400,300)
{
    rasterizer_3d_imp->fovx = &(*camera->fovx);
    rasterizer_3d_imp->fovy = &(*camera->fovy);
    rasterizer_3d_imp->screen_ysize = &(*screen->ysize);
    rasterizer_3d_imp->screen_xsize = &(*screen->xsize);

    13d_screen_info *si = screen->sinfo;
    texture_loader = new 13d_texture_loader_ppm(*screen->sinfo);
    camera->VRP_set(0,0,-50,0);
    camera->near_z = float_to_13d_real(5.5);
    camera->far_z = int_to_13d_real(500);

    int i,j,k,onum;

    i=10; j=0; k=20;
    k=0;

    for(i=1; i<10; i+=5) {
        pyramid *p;
        objects[onum = objects.next_index()] = p = new pyramid(texture_loader);
        p->dx_theta = i-1;

        if (*objects[onum] ==NULL) exit(1);
        objects[onum]->modeling_xforms[1].set
        (
            int_to_13d_real(0), int_to_13d_real(0), int_to_13d_real(0), int_to_13d_real(-i),
            int_to_13d_real(0), int_to_13d_real(0), int_to_13d_real(0), int_to_13d_real(i/2),
            int_to_13d_real(0), int_to_13d_real(0), int_to_13d_real(1), int_to_13d_real(1)
        );
        objects[onum]->modeling_xforms[0] =
        objects[onum]->modeling_xform =
        objects[onum]->modeling_xforms[1] |
        objects[onum]->modeling_xforms[0] ;
        onum++;
    }

    screen->refresh_palette();
    screen->sinfo->compute_light_table();
    screen->sinfo->compute_fog_table();
}
```

## 清单 2-18：`main.cc`，程序 `textest` 的主程序文件
