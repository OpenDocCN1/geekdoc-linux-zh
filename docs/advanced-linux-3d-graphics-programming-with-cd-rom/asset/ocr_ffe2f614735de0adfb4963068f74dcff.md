```
morph_target0->plugin_loader->find_symbol("copy_data");

if(morph_target0->plugin_constructor) {
   (*morph_target0->plugin_constructor) (morph_target0,plugin_env0);
}

plugin_env1 = new l3d_plugin_environment(texloader, screen->sinfo, scache,
   (void *)"0 0 0 0 1 0 0 1 0 1 0 0 1 tree.obj tree.ppm tree.vrv");
morph_target1 = new l3d_object(10);
// - max 10 fixed vertices, can be overridden by plug-in if dired
// - by redefining the vertex list

morph_target1->plugin_loader =
   factory_manager->v_0_2_plugin_loader_factory->create();
morph_target1->plugin_loader->load("../lib/dynamics/plugins/vidmesh/vidmesh.so");
morph_target1->plugin_constructor =
   (void (*)(l3d_object *, void *));
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
   (*morph_target1->plugin_constructor) (morph_target1,plugin_env1);
}

// - create some pyramid objects
for(i=1; i<100; i+=20) {
   objects[onum=objects.next_index()] =
      new pyramid(morph_target0->vertices, morph_target1->vertices);
}

*objects[onum] = *morph_target0;
objects[onum]->num_xforms = 2;
objects[onum]->modeling_xforms[0] = l3d_mat_rotx(0);
objects[onum]->modeling_xforms[1].set =
   { float_to_l3d_real(1.), float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(0.),
   float_to_l3d_real(0.), float_to_l3d_real(1.), float_to_l3d_real(0.), float_to_l3d_real(0.),
   float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(0.), float_to_l3d_real(1.);

objects[onum]->modeling_xform=
   objects[onum]->modeling_xforms[1] | objects[onum]->modeling_xforms[0];
objects[onum]->vertices = morph_target0->vertices;

l3d_screen_info_indexed *si_idx;
l3d_screen_info_rgb *si_rgb;

l3d_polygon_3d_flatshaded *p;
for(int pnum=0; pnum<objects[onum]->polygons.num_items; pnum++) {
   p = dynamic_cast<l3d_polygon_3d_flatshaded *>(objects[onum]->p0lygons[pnum]);
   if(p) {
      p->final_color = si->ext_to_native
         rand() %5i->ext_max_red,
         rand() %5i->ext_max_green,
```