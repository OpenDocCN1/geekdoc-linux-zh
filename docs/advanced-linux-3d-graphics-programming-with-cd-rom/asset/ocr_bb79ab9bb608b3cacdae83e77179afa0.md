The ASCII contents of the `world.dat` text file define the sectors, portals, polygons, and objects within the world, according to the world format described earlier. Since it is an ASCII text file, you could create this file by hand, but this is unreasonably tedious for all but the simplest of worlds. A more realistic approach is to use a 3D modeling program to create the world file for us; see Chapter 8.

# Listing 5-18: **main.cc**, main program file for program **porl**tex

```
```
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <math.h>

#include "../lib/geon/object/object3d.h"
#include "../lib/geon/polygon/p_flat.h"
#include "../lib/geon/polygon/p_portal.h"
#include "../lib/tool_2d/screen.h"
#include "../lib/tool_os/dispatch.h"
#include "../lib/raster/rasteriz.h"
#include "../lib/tool_2d/screen.h"
#include "../lib/geon/world/world.h"
#include "../lib/system/fact0_3.h"
#include "../lib/geon/texture/texload.h"
#include "../lib/geon/texture/t_lpm.h"
#include "../lib/pipeline/pl_lwar.h"
#include "../lib/geon/world/w_portl.tex"

#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <math.h>

main() {
    factory_manager_v_0_2_choosen_factories();

    l3d_dispatcher *d;
    l3d_pipeline_world_lightmapped *p;
    l3d_world_portal_textured_lightmapped_obj w(320,240);
    void *startInfo;

    w.load_from_file("world.dat");
    w.camera->near_z = float_to_l3d_real(0.5);
    w.camera->far_z = int_to_l3d_real(5000);

    d = factory_manager_v_0_2_dispatcher_factory->create();

    p = new l3d_pipeline_world_lightmapped(&w);
    d->pipeline = p;
    d->event_source = w.screen;
    d->start();

    delete p;
    delete d;
}
```
```