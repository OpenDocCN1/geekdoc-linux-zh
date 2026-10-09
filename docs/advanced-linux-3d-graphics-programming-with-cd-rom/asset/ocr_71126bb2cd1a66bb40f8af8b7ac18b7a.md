```
```text
ras_2d_imp_factory = new l3d_rasterizer_2d_mesa_imp_factory;
dispatcher_factory = new l3d_dispatcher_factory_mesa;
ras_3d_imp_factory = new l3d_rasterizer_3d_mesa_imp_factory;
plugin_loader_factory = new l3d_plugin_loader_linux_factory;
break;
case 4:
screen_factory = new l3d_screen_factory_x11;
ras_2d_imp_factory = new l3d_rasterizer_2d_sw_imp_factory;
dispatcher_factory = new l3d_dispatcher_factory_x11;
ras_3d_imp_factory = new l3d_rasterizer_3d_zbuf_sw_imp_factory;
plugin_loader_factory = new l3d_plugin_loader_x11_factory;
break;
case 5:
screen_factory = new l3d_screen_factory_x11_shm;
ras_2d_imp_factory = new l3d_rasterizer_2d_sw_imp_factory;
dispatcher_factory = new l3d_dispatcher_factory_x11;
ras_3d_imp_factory = new l3d_rasterizer_3d_zbuf_sw_imp_factory;
plugin_loader_factory = new l3d_plugin_loader_linux_factory;
break;
case 6:
screen_factory = new l3d_screen_factory_zbuf_mesa;
ras_2d_imp_factory = new l3d_rasterizer_2d_mesa_imp_factory;
dispatcher_factory = new l3d_dispatcher_factory_mesa;
ras_3d_imp_factory = new l3d_rasterizer_3d_zbuf_mesa_imp_factory;
plugin_loader_factory = new l3d_plugin_loader_linux_factory;
break;
factory_manager_v_0_2 = *this;
factory_manager_v_0_2.should_delete_factories = 0;
return 1;
```

```

# Sample Program: texzbuf

The sample program texzbuf is the same as the sample program textest, only the main program file has changed to use the new factory manager. It displays two intersecting pyramids, one static and one rotating. Run the program, and select one of the factories 4, 5, or 6 to see the z buffering in action. Notice closely the area where the two pyramid objects intersect. With the previous program textest (and with this program texzbuf, as well, if you select factories 1, 2, or 3), the piercing polygons appear to flip immediately from in front of to behind the pierced polygons, due to the use of the simple painter's algorithm. With the new program texzbuf, using one of the new z buffer factories 4, 5, or 6, the area of intersection between the pyramid objects is correctly drawn. Notice that the tip of the one pyramid really appears to pierce the face of the other pyramid, and there is a clear line of intersection between the pyramid objects, reflecting the real 3D positions of each pixel of each polygon. Again, this is one of the advantages of the z buffer algorithm: it is accurate to the pixel, even for intersecting polygons, and no polygons need be split to produce a correct display.