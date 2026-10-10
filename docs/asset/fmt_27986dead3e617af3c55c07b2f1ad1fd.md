
从 `Blender` 导出带纹理的网格后，我们可以使用上一个程序中的 `Videoscape` 插件将它们导入程序中。下一个程序 `ika` 正是这样做的。网格是使用 `IK` 创建的事实对于 `Videoscape` 插件并不重要；我们只是将它们作为网格读取，然后可以在它们之间进行形变。

对于这个程序，我选择只是在两个关键帧之间来回形变，这两个关键帧分别保存在文件 `ikal.obj` 和 `ika7.obj` 中。它们对应原始 `Blender` 文件中的动画帧 11 和 71。由于我们在程序中只使用两个关键帧，这意味着我们跳过了导出的八个关键帧中的一些。由于此例中的运动非常简单，这并没有太大区别，但为了更精确的运动，我们可以通过加载相应的 `Videoscape` 文件将更多的关键帧导入程序中。

> **NOTE** 如果你仔细看，你会发现手臂末端，由三角形面组成，被错误地分配了纹理坐标。这是由于前面提到的明显的 `VRML` 导出 bug。为了避免这个问题，你不应该在使用 `VRML` 导出时使用三角形面。我注意到模型中的这个缺陷，但决定保留它，以便你能看到问题是什么样子以及如何识别它。

![](img/a19d4e8b1d7eb6387691dc6c865430e6_209_0.png)

> **Figure 3-27:** 程序 `ika` 的输出。

此程序的列表与前面的程序相似。我们加载不同的 `Videoscape` 文件，将纹理坐标文件传递给 `Videoscape` 插件，使形变速度稍快，并且只创建一个形变对象而不是多个，但其余代码相同。

**Listing 3-4: File shapes.h, program ika**

```cpp
#include "../lib/geom/object/objVect3d.h"
#include "geom/vertex/verInt.h"
#include "dynamics/plugins/plugenv.h"

class pyramid:public l3d_object {
    static const int num_keyframes = 2;
    int keyframe_no;
    l3d_two_part_list<l3d_coordinate> *keyframes[2];
    l3d_vertex_interpolator interp;
    bool currently_interpolating;

public:
    pyramid(l3d_two_part_list<l3d_coordinate> *keyframe0,
           l3d_two_part_list<l3d_coordinate> *keyframe1);
    virtual ~pyramid(void);
    int update(void);
};
```

**Listing 3-5: File shapes.cc, program ika**

```cpp
#include "shapes.h"

#include <stdlib.h>
#include <string.h>

pyramid::pyramid(l3d_two_part_list<l3d_coordinate> *keyframe0,
                l3d_two_part_list<l3d_coordinate> *keyframe1)
    :
    l3d_object(100)
{
    keyframes[0] = keyframe0;
    keyframes[1] = keyframe1;
}
```

## 列表 3-6：文件 main.cc，程序 ika

```cpp
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <math.h>
#include <stdarg.h>

#include "../lib/geon/object/object3d.h"
#include "../lib/geon/polygon/p3_flat.h"
#include "../lib/tool_2d/screen.h"
#include "../lib/tool_os/isparch.h"
#include "../lib/raster/rast3.h"
#include "../lib/tool_2d/screen.h"
#include "../lib/geon/world/world.h"
#include "../lib/system/fact2.h"
#include "../lib/pipeline/pl_war.h"
#include "../lib/dynamics/plugins/plugin.h"
#include "../lib/geon/texture/t_ppm.h"
#include "../lib/dynamics/plugins/vidmesh/vidmesh.h"

#include "shapes.h"
```

### 第 3 章：使用 Blender 进行 3D 建模

```cpp
class my_world:public l3d_world {
public:
   my_world(void);
};

my_world::my_world(void)
   : l3d_world(400,300)
{

   l3d_screen_info *si = screen->info;
   camera->RP.set(0,0,-50,0);
   camera->near_z = float_to_l3d_real(5.5);
   camera->far_z = int_to_l3d_real(500);

   rasterizer_3d_imp->fov_x = &(camera->fov);
   rasterizer_3d_imp->fov_y = &(camera->fov);
   rasterizer_3d_imp->screen_xsize = &(screen->xsize);
   rasterizer_3d_imp->screen_ysize = &(screen->ysize);

   int i,j,k,num=0;

   i=10; j=0; k=20;
   k=0;
   // - create two videoscape plug-in objects, one for the first morph
   // - target and one for the second

   l3d_object *morph_target0, *morph_target1;

   l3d_texture_loader *texloader;
   l3d_surface_cache *scache;
   texloader = new l3d_texture_loader_ppm(si);
   scache = new l3d_surface_cache(si);
   l3d_plugin_environment *plugin_envl;

   plugin_env0 = new l3d_plugin_environment(texloader, screen->info, scache,
                      (void *)"0 0 0 0 0 0 0 0 0 0 0 ikaI.obj ika.ppm ika.uv\0" );
   morph_target0 = new l3d_object(10);
   // - max 10 fixed vertices, can be overridden by plug-in if desired
   // - by redefining the vertex list

   morph_target0->plugin_loader =
      factory_manager_v_0_2.plugin_loader_factory->create();
   morph_target0->plugin_loader->load("../lib/dynamics/plugins/vidmesh/vidmesh.so");
   morph_target0->plugin_constructor =
      (void (*)(l3d_object *, void *))
   morph_target0->plugin_loader->find_symbol("constructor");
   morph_target0->plugin_update =
      (void (*)(l3d_object *));
   morph_target0->plugin_loader->find_symbol("update");
   morph_target0->plugin_destructor =
      (void (*)(l3d_object *));
   morph_target0->plugin_loader->find_symbol("destructor");
   morph_target0->plugin_copy_data =
      (void (*)(const l3d_object *, l3d_object *));
   morph_target0->plugin_loader->find_symbol("copy_data");

   if(morph_target0->plugin_constructor) {
      (*morph_target0->plugin_constructor) (morph_target0, plugin_env0);
   }

   plugin_env1 = new l3d_plugin_environment(texloader, screen->info, scache,
      (void *)"0 0 0 0 1 0 0 0 1 0 0 1 ika7ib/dynamics/plugins/vidmesh/vidmesh.so");
   morph_target1 = new l3d_object(10);
   // - max 10 fixed vertices, can be overridden by plug-in if desired
   // - by redefining the vertex list

   morph_target1->plugin_loader =
      factory_manager_v_0_2.plugin_loader_factory->create();
   morph_target1->plugin_loader->load("../lib/dynamics/plugins/vidmesh/vidmesh.so");
   morph_target1->plugin_constructor =
      (void (*)(l3d_object *, void *))
   morph_target1->plugin_loader->find_symbol("constructor");
   morph_target1->plugin_update =
      (void (*)(l3d_object *));
   morph_target1->plugin_loader->find_symbol("update");
   morph_target1->plugin_destructor =
      (void (*)(l3d_object *));
   morph_target1->plugin_loader->find_symbol("destructor");
   morph_target1->plugin_copy_data =
      (void (*)(const l3d_object *, l3d_object *));
   morph_target1->plugin_loader->find_symbol("copy_data");

   if(morph_target1->plugin_constructor) {
      (*morph_target1->plugin_constructor) (morph_target1, plugin_env1);
   }

   // - create some pyramid objects
   num = objects.next_index();
   objects[num] =
      new pyramid(morph_target0->vertices, morph_target1->vertices);

   *objects[num] = *morph_target0;
   objects[num]->num_xforms = 2;
   objects[num]->modeling_xforms[0] = l3d_mat_rotx(0);
   objects[num]->modeling_xforms[1].set
      (float_to_l3d_real(1.), float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(0.),
       float_to_l3d_real(0.), float_to_l3d_real(1.), float_to_l3d_real(0.), float_to_l3d_real(0.),
       float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(1.), float_to_l3d_real(0.),
       float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(1.));
   objects[num]->modeling_xforms[2] =
      objects[num]->modeling_xforms[1] | objects[num]->modeling_xforms[0];
   objects[num]->vertices = morph_target0->vertices;

   l3d_screen_info *si_idx;
   l3d_screen_info_rgb *si_rgb;

   l3d_polygon_3d *p;
   for(int pnum=0; pnum<objects[num]->polygons.num_items; pnum++) {
      p = dynamic_cast<l3d_polygon_3d_flatshaded *>(&objects[num]->polygons[pnum]);
      if(p) {
         p->final_color = si->next_to_native(
            rand() % si->ext_max_red,
            rand() % si->ext_max_green,
            rand() % si->ext_max_blue);
      }
   }

   if (objects[num] == NULL) exit(0);
   objects[num]->modeling_xforms[1].set
      (int_to_l3d_real(1), int_to_l3d_real(0), int_to_l3d_real(0), int_to_l3d_real(1),
       int_to_l3d_real(0), int_to_l3d_real(1), int_to_l3d_real(0), int_to_l3d_real(1),
       int_to_l3d_real(0), int_to_l3d_real(0), int_to_l3d_real(1), int_to_l3d_real(1),
       int_to_l3d_real(0), int_to_l3d_real(0), int_to_l3d_real(0), int_to_l3d_real(1) );
   objects[num]->modeling_xform =
      objects[num]->modeling_xforms[0] | objects[num]->modeling_xforms[1];
   }
   screen->refresh_palette();
}

int main() {
   l3d_dispatcher *d;
   l3d_pipeline_world *p;
   my_world *w;

   factory_manager_v_0_2::choose_factories();
   d = factory_manager_v_0_2::dispatcher_factory->create();

   w = new my_world();
   p = new l3d_pipeline_world(w);
   d->pipeline = p;
   d->event_source = w->screen;

   d->start();

   delete d;
   delete p;
   delete w;
   return 0;
}
```

*LING 团队 - 实用、资讯丰富、无成本且真实！*

### 动态描图（Rotoscoping）与逆向运动学

`Blender` 提供了一种有趣的特性，可以简化逆向运动学（`IK`）动画的制作。该特性称为动态描图（Rotoscoping）。动态描图是指使用实时视频素材来辅助创建计算机动画。`Blender` 对动态描图的支持允许将视频文件的单独帧与 `Blender` 动画帧同步。视频图像叠加在 3D 窗口之上。使用方向键改变 `Blender` 动画帧时，也会改变显示的视频帧。例如，在 `Blender` 中向前移动五个动画帧，视频也会向前移动五帧。
