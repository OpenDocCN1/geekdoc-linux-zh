```
class l3d_surface_cache {
    protected:
        l3d_screen_info *sinfo;
        l3d_list<l3d_surface> *surfaces;

    public:
        l3d_surface_cache(l3d_screen_info *sinfo) {
            surfaces = new l3d_list<l3d_surface> (10);
            this->sinfo = sinfo;
        }
        virtual ~l3d_surface_cache(void) {
            int i;
            delete surfaces;
        }

        l3d_texture *combine_lightmap_and_textmap(int width,
                                                   int height,
            const l3d_polygon_3d_textured_lightmapped *polygon);
        void reset(void) {
            delete surfaces;
            surfaces = new l3d_list<l3d_surface> (10);
        }
        l3d_texture_data *find_textdata(l3d_texture_data *textdata);
    };
    #include "../polygon/p3_tex.h"
    #include "../polygon/p3_ltex.h"
    #endif
```

# **Listing 2-20: s cache.cc**

```
#include "scache.h"
#include "../tool_2d/si_rgb.h"
#include "../../tool_os/memman.h"

l3d_surface::l3d_surface(void) {
    surface = NULL;
    polygon = NULL;
}

l3d_surface::~l3d_surface(void) {
    if(surface) delete surface;
    if(polygon) (polygon->surface = NULL; }

l3d_texture *l3d_surface_cache::
combine_lightmap_and_textmap(int width,
                             int height,
                             const l3d_polygon_3d_textured_lightmapped *polygon)
{
    int i;
```