# Chapter 3: 3D Modeling with Blender

```
#include <string.h>
#include <stdio.h>
#include <math.h>
#include <stdarg.h>

class my_world:public l3d_world {
    public:
    my_world(void);
};

my_world::my_world(void)
  : l3d_world(400,300)
{
    l3d_screen_info *si = screen->sinfo;

    camera->VRP.set(0,0,-50,0);
    camera->near_z = float_to_l3d_real(5.5);
    camera->far_z = int_to_l3d_real(500);

    rasterizer_3d_imp->fovx = &(camera->fovx);
    rasterizer_3d_imp->fovy = &(camera->fovy);
    rasterizer_3d_imp->surface_xsize = &(screen->ysize);
    rasterizer_3d_imp->surface_ysize = &(screen->ysize);

    int i,j,k,num=0;
    i=10; j=0; k=20;
    k=0;

    /*- create two videoscape plug-in objects, one for the first morph */
    /*- target and one for the second

    l3d_object *morph_target0, *morph_target1;

    l3d_texture_loader *texloader;
    l3d_surface_cache *scache;
    texloader = new l3d_texture_loader_pgm(si);
    scache = new l3d_surface_cache(si);
    l3d_plugin_environment *plugin_env0, *plugin_env1;

    plugin_env0 = new l3d_plugin_environment(texloader, screen, scache,
            (void ")"0 0 0 1 0 0 0 1 0 0 0 1 cube.obj ttee.pgm tree.u");
    morph_target0 = new l3d_object(10);
    /*- max 10 fixed vertices, can be overridden by plug-in if desired */
    /*- by redefining the vertex list

    morph_target0->plugin_loader =
        factory_manager_v_0_2_plugin_loader_factory->create();
    morph_target0->plugin_loader->load("../lib/dynamics/plugins/vdmesh/vdimesh.so");
    morph_target0->plugin_constructor =
        (void (*) (l3d_object *, void *))
        morph_target0->plugin_loader->find_symbol("constructor");
    morph_target0->plugin_update =
        (void (*) (l3d_object *))
        morph_target0->plugin_loader->find_symbol("update");
    morph_target0->plugin_destructor =
        (void (*) (l3d_object *))
        morph_target0->plugin_loader->find_symbol("destructor");
    morph_target0->plugin_copy_data =
        (void (*) (const l3d_object *, l3d_object *))
```

TEAM LinG – Live, Informative, Non-cost and Genuine!