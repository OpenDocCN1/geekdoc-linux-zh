
# Chapter 3: 3D Modeling with Blender

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

TEAM LinG – Live, Informative, Non-cost and Genuine!

The program is almost identical to the morphing pyramid program from Chapter 2. First, we create two Videscape plug-in objects and load the cube and the tree object into each of these objects. Then, we create a series of morphable pyramid objects, just as we did in Chapter 2. (The name pyramid is here somewhat of a misnomer, since the morphable objects are not pyramids in this case, but the naming remains the same to emphasize the similarity of the code with that of Chapter 2.)

In this case, instead of explicitly assigning the vertices in the source and destination morph vertex lists, we simply use the vertex lists from the already loaded plug-in objects. Then, each pyramid object morphs itself from its source to its target vertex list, and back again, using the vertex interpolator class.

The logic, therefore, is essentially the same as the simpler morphing program of Chapter 2, only now we are morphing between two real 3D models, created and textured within Blender. The logic is simple, yet the results look quite good in 3D.

Note that in this morphing program, in contrast to the morphing program of Chapter 2, we do recalculate the surface normals during morphing. This is because the Mesa texture mapping routines require a reverse projection, as we saw in Chapter 2. Performing this reverse projection during Mesa texture mapping requires us to have an accurate surface normal vector, which is why we recalculate it whenever we interpolate the vertex positions.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_196_0.png)

*Figure 3-14: Output from sample program vids3d.*

## Tutorial: Using Inverse Kinematics and Rotoscoping to Model a Walking Human Figure

This tutorial illustrates two very powerful features of Blender: inverse kinematics and rotoscoping. These techniques allow us to animate a human-like jointed figure, which we then import into a program.

This tutorial is a small introduction to the field of *character animation*. Character animation is a special branch of animation dealing with animating *characters*—living entities such as humans, dogs, or imaginary creatures such as aliens. Even ordinarily inanimate objects, such as a sack of flour, can be animated as characters so that they appear to walk, move around, and come to life. Indeed, to animate literally means to bring to life. Character animation is a very broad field and requires years of study to master. This is because the subtle nuances of a character’s movement convey much about that character’s personality. Creating believable characters requires a firm concept of the character you wish to portray as well as an understanding of anatomy, proportion, staging, posing, timing, weight, movement, and so forth.

While this small tutorial cannot show you all of the aspects of character animation, what it does illustrate is the technical side of basic character animation using Blender. We’ll create a simple human-like character and move its limbs around to simulate a walking motion. One of the most important tools for doing character animation is inverse kinematics, which we now look at in more detail.
