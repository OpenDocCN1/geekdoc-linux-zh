
### 13d_world_backface

If you have read the introductory companion book *Linux 3D Graphics Programming*, you can see that this program is nearly identical to the `fltsim` program.

Run the program and notice the display in the upper left of the screen, showing the number of polygons sent to the rasterizer. Only the front-facing polygons are drawn, as you can see by the drawn polygon count.

#### Listing 4-1: shapes.h, shape definition header file for program backface

```cpp
#include "../lib/geem/object/object3d.h"

class pyramid:public l3d_object {
    int xtheta;
    public:
        pyramid(void);
        virtual ~pyramid(void);
        int update(void);
};
```

![](img/a19d4e8b1d7eb6387691dc6c865430e6_226_0.png)

#### Figure 4-6: Output from sample program backface, illustrating the number of polygons drawn.

#### Listing 4-2: shapes.cc, shape definition code for program backface

```cpp
#include "shapes.h"
#include <stdlib.h>
#include <string.h>

pyramid::pyramid(void) :
    l3d_object(4)
{
    (*vertices)[0].original.set
    (float_to_l3d_real(0.),
     float_to_l3d_real(0.),
     float_to_l3d_real(0.),
     float_to_l3d_real(1.));
    (*vertices)[1].original.set
    (float_to_l3d_real(10.0),
     float_to_l3d_real(0.),
     float_to_l3d_real(0.),
     float_to_l3d_real(1.));
    (*vertices)[2].original.set
    (float_to_l3d_real(0.),
     float_to_l3d_real(0.),
     float_to_l3d_real(1.));
    (*vertices)[3].original.set
    (float_to_l3d_real(0.),
     float_to_l3d_real(0.),
     float_to_l3d_real(1.));
    int pi;
    pi = polygons.next_index();
    polygons[pi] = new l3d_polygon_3d_flathashed(3);
    printf("before: %p", polygons[pi]->vlist);
    polygons[pi]->vlist = &vertices;
    printf("after: %p", polygons[pi]->vlist);
    (*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=0;
    (*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=1;
    (*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=3;
    polygons[pi]->compute_center();
    polygons[pi]->compute_sfnormal();

    pi = polygons.next_index();
    polygons[pi] = new l3d_polygon_3d_flathashed(3);
    polygons[pi]->vlist = &vertices;
    (*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=2;
    (*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=3;
    (*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=1;
    polygons[pi]->compute_center();
    polygons[pi]->compute_sfnormal();

    pi = polygons.next_index();
    polygons[pi] = new l3d_polygon_3d_flathashed(3);
    polygons[pi]->vlist = &vertices;
    (*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=0;
    (*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=2;
    (*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=1;
    polygons[pi]->compute_center();
    polygons[pi]->compute_sfnormal();

    pi = polygons.next_index();
    polygons[pi] = new l3d_polygon_3d_flathashed(3);
    polygons[pi]->vlist = &vertices;
    (*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=3;
    (*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=2;
    (*polygons[pi]->vertices)[polygons[pi]->vertices->next_index()].ivertex=0;
    polygons[pi]->compute_center();
    polygons[pi]->compute_sfnormal();

    num_xforms = 2;
    xtheta=0;
    modeling_xforms[0] = l3d_mat_rot(xtheta);
    modeling_xforms[1].set
    ( float_to_l3d_real(1.), float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(0.),
      float_to_l3d_real(0.), float_to_l3d_real(1.), float_to_l3d_real(0.), float_to_l3d_real(0.),
      float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(1.), float_to_l3d_real(0.),
      float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(1.) );
    modeling_xform =
    modeling_xforms[1] | modeling_xforms[0];
}

pyramid::~pyramid(void) { 
    for(int i=0; i < polygons.num_items; i++) {
        delete polygons[i]; 
    }
}

int pyramid::update(void) {
  xtheta += 10; 
  if (xtheta>359) xtheta=0;
  modeling_xforms[0]=Id_mat*rotx(xtheta);
  modeling_xform =
    modeling_xforms[1] | modeling_xforms[0];
}
```

#### Listing 4-3: main.cc, main program file for program backface

```cpp
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <math.h>

#include "../lib/geomet/object/object3d.h"
#include "../lib/geomet/polygon/p3_flat.h"
#include "../lib/tool_2d/screen.h"
#include "../lib/tool_os/disppatch.h"
#include "../lib/raster/rast3.h"
#include "../lib/tool_2d/scrimlin.h"
#include "../lib/geomet/world/world.h"
#include "../lib/geomet/world/k_back.h"
#include "../lib/system/fact0_2.h"
#include "../lib/pipeline/pi_wor.h"
#include "../lib/dynamics/plugins/plugenv.h"

#include "shapes.h"

#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <math.h>
#include <stdarg.h>

class my_world:public l3d_world_backface {
public:
  my_world(void);
};

my_world::my_world(void)
  : l3d_world_backface(640,400)
{
  l3d_screen_info *si = screen->sinfo;

  camera->VRP.set(0.0,50.0);
  camera->near_Z = float_to_l3d_real(5.5);
  camera->far_Z = int_to_l3d_real(500);

  int i,j,k,onum=0;

  i=10; j=0; k=20;

  k=0;

  // - create some pyramid objects
  for(i=1; i<=20; i+=20) {
    objects[onum=objects.next_index()] = new pyramid();
    
    l3d_screen_info_indexed *si_idx;
    l3d_screen_info_rgb *si_rgb;

    l3d_polygon_3d_flathashed *p;
    for(int pnum=0; pnum<objects[onum]->num_polygons.num_items; pnum++) {
        p = dynamic_cast<l3d_polygon_3d_flathashed *>(objects[onum]->polygons[pnum]);
        if(p) {
            p->final_color = si->ext_to_native
            (rand()%si->ext_max_red,
             rand()%si->ext_max_green,
             rand()%si->ext_max_blue);
        }
    }

    if (objects[onum]==NULL) exit(1);
    objects[onum]->modeling_xforms[1].set
    (int_to_l3d_real(1), int_to_l3d_real(0), int_to_l3d_real(0), int_to_l3d_real(1),
     int_to_l3d_real(0), int_to_l3d_real(1), int_to_l3d_real(0), int_to_l3d_real(1),
     int_to_l3d_real(0), int_to_l3d_real(0), int_to_l3d_real(1), int_to_l3d_real(1));
    objects[onum]->modeling_xform =
    (int_to_l3d_real(0), int_to_l3d_real(0), int_to_l3d_real(0), int_to_l3d_real(1),
     int_to_l3d_real(0), int_to_l3d_real(1), int_to_l3d_real(0), int_to_l3d_real(1),
     int_to_l3d_real(0), int_to_l3d_real(0), int_to_l3d_real(1), int_to_l3d_real(1));
    objects[onum]->modeling_xform =
    objects[onum]->modeling_xforms[1] |
    objects[onum]->modeling_xforms[0];
    
    // create a plugin object

    objects[onum]=objects.next_index();
    objects[onum] = new l3d_object(10);
    //-> max 10 fixed vertices, can be overriden by plug-in if desired
    //-> by redefining the vertex list

    objects[onum]->plugin_loader =
    factory_manager_v_0_2.plugin_loader_factory().create();
    objects[onum]->plugin_loader->load("../lib/dynamics/plugins/pyramid/pyramid.so");
    objects[onum]->plugin_constructor =
    (void (*)(l3d_object *, void *))
    objects[onum]->plugin_loader->find_symbol("constructor");
    objects[onum]->plugin_update =
    (void (*)(l3d_object *))
    objects[onum]->plugin_loader->find_symbol("update");
    objects[onum]->plugin_destructor =
    (void (*)(l3d_object *))
    objects[onum]->plugin_loader->find_symbol("destructor");
    objects[onum]->plugin_copy_data =
    (void (*)(const l3d_object *, l3d_object *))
    objects[onum]->plugin_loader->find_symbol("copy_data");

    l3d_plugin_environment *e = new l3d_plugin_environment
    (NULL, screen->info, NULL, (void **));

    if(objects[onum]->plugin_constructor) {
        (*objects[onum]->plugin_constructor) (objects[onum],e);
    }
  }
}

int main(int argc, char *argv[]) {
  my_world *w;

  factory_manager_v_0_2::choose_factories();
  l3d_dispatcher *d = factory_manager_v_0_2::dispatcher_factory->create();

  w = new my_world();
  l3d_pipeline *p = new l3d_pipeline_world(w);
  d->pipeline = p;
  d->event_source = w->screen;

  d->start();

  delete d;
  delete p;
  delete w;
  return 0;
}
```

## Class l3d_world_backface

The new class `l3d_world_backface` has modified the main polygon processing loop, by overriding method `draw_all`, to perform back-face culling. Recall that we group polygons into objects, but can also access the polygons as individual polygons, through the `nonculled_polygon_nodes` linked list member of `l3d_object`. Until now, the only time we removed polygons from this list was if they were completely clipped away against the near z plane. Now, with back-face culling, we also remove any polygons from the list if they are back-facing. Only the polygons surviving all culling operations are inserted into the final polygon list to be drawn for each frame.

The following code snippet from class `l3d_world_backface` performs the back-face culling.

```cpp
      // vector from facet center to camera (at 0,0,0), for backface culling
      l3d_vector facet_to_cam_vec;
      // facet's sfc normal relative to origin (afacet.sfc_normal is relative
      // to facet center)
      l3d_vector N;
      n = objects[id0bj]->nonculled_polygon_nodes;
      while(n) {
          N = n->polygon->sfcnormal.transformed(~ n->polygon->center.transformed);

          facet_to_cam_vec.set( 0 - n->polygon->center.transformed_X_,
                               0 - n->polygon->center.transformed_Y_,
                               (0 - n->polygon->center.transformed_Z_ -
                                int_to_l3d_real(0)));

      // dot product explicitly formulated so no fixed point overflow
      // ((facet_to_cam_vec is very large)
      // (use of the inline function "dot" uses default fixed precision)
      #include "../..../math/fix_lowp.h"
      #define BACKFACE_EPS  float_to_l3d_real(0.1)
      if(( l3d_mulrr(FX_CVT(N.X_), FX_CVT(facet_to_cam_vec.X_)) +
           l3d_mulrr(FX_CVT(N.Y_), FX_CVT(facet_to_cam_vec.Y_)) +
           l3d_mulrr(FX_CVT(N.Z_), FX_CVT(facet_to_cam_vec.Z_)) > BACKFACE_EPS)
      // equivalent to: if(N.dot(facet_to_cam_vec) > BACKFACE_EPS )
      #include "..../math/fix_prec.h"
      &&
```
