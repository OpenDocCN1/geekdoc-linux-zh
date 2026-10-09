
# 第 3 章：使用 Blender 进行 3D 建模

```cpp
#include <string.h>
#include <stdio.h>
#include <math.h>
#include <stdarg.h>

class my_world : public l3d_world {
    public:
    my_world(void);
};

my_world::my_world(void)
  : l3d_world(400, 300)
{
    l3d_screen_info *si = screen->sinfo;

    camera->VRP.set(0, 0, -50, 0);
    camera->near_z = float_to_l3d_real(5.5);
    camera->far_z = int_to_l3d_real(500);

    rasterizer_3d_imp->fovx = &(camera->fovx);
    rasterizer_3d_imp->fovy = &(camera->fovy);
    rasterizer_3d_imp->surface_xsize = &(screen->ysize);
    rasterizer_3d_imp->surface_ysize = &(screen->ysize);

    int i, j, k, num = 0;
    i = 10; j = 0; k = 20;
    k = 0;

    /*- create two videoscape plug-in objects, one for the first morph */
    /*- target and one for the second */

    l3d_object *morph_target0, *morph_target1;

    l3d_texture_loader *texloader;
    l3d_surface_cache *scache;
    texloader = new l3d_texture_loader_pgm(si);
    scache = new l3d_surface_cache(si);
    l3d_plugin_environment *plugin_env0, *plugin_env1;

    plugin_env0 = new l3d_plugin_environment(texloader, screen, scache,
            (void *)"0 0 0 1 0 0 0 1 0 0 0 1 cube.obj tree.pgm tree.vrv");
    morph_target0 = new l3d_object(10);
    /*- max 10 fixed vertices, can be overridden by plug-in if desired */
    /*- by redefining the vertex list */

    morph_target0->plugin_loader =
        factory_manager_v_0_2_plugin_loader_factory->create();
    morph_target0->plugin_loader->load("../lib/dynamics/plugins/vdmesh/vdmesh.so");
    morph_target0->plugin_constructor =
        (void (*)(l3d_object *, void *))
        morph_target0->plugin_loader->find_symbol("constructor");
    morph_target0->plugin_update =
        (void (*)(l3d_object *))
        morph_target0->plugin_loader->find_symbol("update");
    morph_target0->plugin_destructor =
        (void (*)(l3d_object *))
        morph_target0->plugin_loader->find_symbol("destructor");
    morph_target0->plugin_copy_data =
        (void (*)(const l3d_object *, l3d_object *))
        morph_target0->plugin_loader->find_symbol("copy_data");

    if (morph_target0->plugin_constructor) {
       (*morph_target0->plugin_constructor) (morph_target0, plugin_env0);
    }

    plugin_env1 = new l3d_plugin_environment(texloader, screen->sinfo, scache,
       (void *)"0 0 0 0 1 0 0 1 0 1 0 0 1 tree.obj tree.ppm tree.vrv");
    morph_target1 = new l3d_object(10);
    // - max 10 fixed vertices, can be overridden by plug-in if desired
    // - by redefining the vertex list

    morph_target1->plugin_loader =
       factory_manager->v_0_2_plugin_loader_factory->create();
    morph_target1->plugin_loader->load("../lib/dynamics/plugins/vdmesh/vdmesh.so");
    morph_target1->plugin_constructor =
       (void (*)(l3d_object *, void *))
       morph_target1->plugin_loader->find_symbol("constructor");
    morph_target1->plugin_update =
       (void (*)(l3d_object *))
       morph_target1->plugin_loader->find_symbol("update");
    morph_target1->plugin_destructor =
       (void (*)(l3d_object *))
       morph_target1->plugin_loader->find_symbol("destructor");
    morph_target1->plugin_copy_data =
       (void (*)(const l3d_object *, l3d_object *))
       morph_target1->plugin_loader->find_symbol("copy_data");

    if (morph_target1->plugin_constructor) {
       (*morph_target1->plugin_constructor) (morph_target1, plugin_env1);
    }

    // - create some pyramid objects
    for (i = 1; i < 100; i += 20) {
       objects[onum = objects.next_index()] =
          new pyramid(morph_target0->vertices, morph_target1->vertices);
    }

    *objects[onum] = *morph_target0;
    objects[onum]->num_xforms = 2;
    objects[onum]->modeling_xforms[0] = l3d_mat_rotx(0);
    objects[onum]->modeling_xforms[1].set(
       float_to_l3d_real(1.0), float_to_l3d_real(0.0), float_to_l3d_real(0.0), float_to_l3d_real(0.0),
       float_to_l3d_real(0.0), float_to_l3d_real(1.0), float_to_l3d_real(0.0), float_to_l3d_real(0.0),
       float_to_l3d_real(0.0), float_to_l3d_real(0.0), float_to_l3d_real(0.0), float_to_l3d_real(1.0)
    );

    objects[onum]->modeling_xform =
       objects[onum]->modeling_xforms[1] * objects[onum]->modeling_xforms[0];
    objects[onum]->vertices = morph_target0->vertices;

    l3d_screen_info_indexed *si_idx;
    l3d_screen_info_rgb *si_rgb;

    l3d_polygon_3d_flatshaded *p;
    for (int pnum = 0; pnum < objects[onum]->polygons.num_items; pnum++) {
       p = dynamic_cast<l3d_polygon_3d_flatshaded *>(objects[onum]->polygons[pnum]);
       if (p) {
          p->final_color = si->ext_to_native(
             rand() % si->ext_max_red,
             rand() % si->ext_max_green,
             rand() % si->ext_max_blue
          );
       }
    }

    if (objects[num] == NULL) exit(1);
    objects[num]->modeling_xforms[0].set(
        int_to_l3d_real(1), int_to_l3d_real(0), int_to_l3d_real(ii),
        int_to_l3d_real(0), int_to_l3d_real(1), int_to_l3d_real(0), int_to_l3d_real(ii),
        int_to_l3d_real(0), int_to_l3d_real(0), int_to_l3d_real(ii), int_to_l3d_real(ii),
        int_to_l3d_real(1), int_to_l3d_real(0), int_to_l3d_real(0), int_to_l3d_real(ii)
    );
    objects[num]->modeling_xform =
        objects[num]->modeling_xforms[0];
}

screen->refresh_palette();

}

main() {
    l3d_dispatcher *d;
    l3d_pipeline_world *p;
    my_world *w;

    factory_manager_v0_2_choose_factories();
    d = factory_manager_v0_2_dispatcher_factory->create();

    w = new my_world();
    p = new l3d_pipeline_world(w);
    d->pipeline = p;
    d->event_source = w->screen;

    d->start();

    delete d;
    delete p;
    delete w;
}
```

TEAM LinG – 生活、资讯、零成本、真实！

该程序与第 2 章中的变形金字塔程序几乎完全相同。首先，我们创建两个 Videscape 插件对象，并分别将立方体和树对象加载到这些对象中。然后，就像我们在第 2 章所做的那样，我们创建了一系列可变形金字塔对象。（在此，"pyramid" [金字塔] 这个词其实有点名不副实，因为在这种情况下，可变形的对象并不是金字塔，但为了强调代码与第 2 章的相似性，我们保留了相同的命名。）

在这种情况下，我们没有显式地指定源和目标变形顶点列表中的顶点，而是简单地使用了已加载插件对象中的顶点列表。然后，每个金字塔对象使用顶点插值类，从源顶点列表变形到目标顶点列表，然后再变回去。

因此，逻辑上基本上与第 2 章中较简单的变形程序相同，只是现在我们是在两个在 Blender 中创建和纹理化的真实 3D 模型之间进行变形。逻辑很简单，但 3D 效果看起来相当不错。

请注意，与第 2 章中的变形程序不同，在这个变形程序中，我们在变形过程中重新计算了表面法线。这是因为，如第 2 章所述，Mesa 纹理映射例程需要反向投影。在 Mesa 纹理映射期间执行此反向投影需要我们有准确的表面法线向量，这就是为什么我们每次插值顶点位置时都会重新计算它的原因。

![](img/a19d4e8b1d7eb6387691dc6c865430e6_196_0.png)

*图 3-14：示例程序 vids3d 的输出。*

## 教程：使用逆运动学和动作捕捉建模行走的人形

本教程展示了 Blender 的两个非常强大的功能：逆运动学和动作捕捉（rotoscoping）。这些技术允许我们动画化一个类似人类关节的人形，然后将其导入程序中。

本教程是对*角色动画*领域的一个简短介绍。角色动画是动画的一个特殊分支，涉及对*角色*——如人类、狗或外星人等想象中的生物等有生命实体——进行动画化。即使是通常无生命的物体，如一袋面粉，也可以作为角色进行动画化，使其看起来像在行走、移动并“复活”。事实上，“动画”（animate）一词的字面意思就是赋予生命。角色动画是一个非常广阔的领域，需要多年的研究才能掌握。这是因为角色动作的微妙细微之处传达了关于该角色个性的许多信息。创建可信的角色需要对您想要表现的角色有清晰的概念，并且对解剖学、比例、舞台调度、姿势、时间节奏、重量、运动等有所理解。

虽然这个小教程无法展示角色动画的所有方面，但它展示了使用 Blender 进行基本角色动画的技术层面。我们将创建一个简单的人形角色，并移动其四肢以模拟行走动作。角色动画最重要的工具之一是逆运动学，我们现在将更详细地研究它。
