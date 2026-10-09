we recursively call `render` on the portal’s connected sector, passing the portal polygon itself, whose geometry has now been projected into screen space, as the clipping window. This means that the screen space projection of the portal polygon limits the boundaries of what can be seen through the portal, which is the whole idea of portal rendering.

The only tricky part about the method `render` is the combination of the objects’ polygon lists and the sector’s polygon list. As we mentioned before, we should draw moveable objects in a cell after drawing that sector’s geometry, so that the objects appear on top of the sector’s geometry. We do this by joining all the polygon nodes of all objects together into one big list, then appending this object polygon node list to the polygon node list of the sector. In this way, we first process and draw the sector polygons, then draw and process the object polygons. Remember that for a correct display of object polygons we must use some other VSD mechanism to sort the polygons within and among the objects, but here we simply draw them in any order. When joining the object and sector polygon lists, we have to set the transformation stage variable (which tracks how many times an object, polygon, or vertex has been transformed) for the object polygons to be the same as that of the sector polygons. In general, an object polygon may have been transformed more times than the sector polygon, because the object may undergo its own local transformation (it may spin itself or move around, for instance). But when we join the object polygon list with the sector polygon list, all polygons should have the same transformation stage for consistency. The code in method `render` therefore takes care of joining the object and sector polygon lists, and ensuring that their transformation stage counters are the same.

Note that the method `render` is virtual; as mentioned earlier, this means that descendants of the sector class can implement new rendering methods for different types of sectors.

```
**Listing 5-10:** `sector.h`
```c
#ifndef  _SECTOR_H
#define  _SECTOR_H
#include \"../..//tool_os/nemann.h\"
#include \"bound.h\"
#include \"..//view/camera.h\"

class l3d_polygon_3d_portal_clippable;

class l3d_sector :
    public l3d_object_clippable_boundable
{
    public:
        l3d_sector(int num_fixed_vertices) :
            l3d_object(num_fixed_vertices),
            l3d_object_clippable(num_fixed_vertices),
            l3d_object_clippable_boundable(num_fixed_vertices)
        {
            objects = new l3d_list<l3d_object_clippable_boundable *>(l);
        };
        virtual ~l3d_sector(void);
        l3d_list*l3d_object_clippable_boundable *> *objects;
        int update(void);

        virtual void render(l3d_polygon_2d *clipping,
                          l3d_rasterizer_3d *rasterizer, l3d_camera *camera,
                          int xsize, int ysize);
```
```