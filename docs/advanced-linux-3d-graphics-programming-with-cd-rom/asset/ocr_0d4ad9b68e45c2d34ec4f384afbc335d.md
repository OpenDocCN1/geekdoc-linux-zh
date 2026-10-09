```
					} pt->texture->owns_tex_data = false;
			}
	}

	copy_target->plugin_data = (void *)new_mesh;
}
}

```

# # Sample Program: collide

As is usual with 13d programs, once the supporting lower-level classes are in place, the actual application program is simple. Program `collide` creates an instance of the new world class with collision detection, then asks it to load itself from disk. This causes creation of the appropriate collidable polygons and a collidable camera. Furthermore, the world file contains references to plug-in objects of type `seeker`, which also know how to collide themselves with the environment. The main program file also plays some background music stored in audio file `bgmusic.au`.

Listing 8-20: main.cc, main program file for program `collide`

```
```cpp
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <math.h>

#include "../lib/geom/object/object3d.h"
#include "../lib/geom/polygon/p_flat.h"
#include "../lib/geom/polygon/p_portal.h"
#include "../lib/tool_2d/screen.h"
#include "../lib/tool_os/dispatch.h"
#include "../lib/raster/rasteriz.h.h"
#include "../lib/tool_2d/script.h"
#include "../lib/geom/world0/world0.h"
#include "../lib/system/fact0_4.h"
#include "../lib/geom/texture/texload.h"
#include "../lib/geom/texture/tl_ppm.h"
#include "../lib/pipe/line/pi_lwr.h"
#include "../lib/geom/world0/w_pcoll.h"

#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <math.h>

main() {
    factory_manager_v_0_4.choose_factories();

    13d_dispatcher "d";
    13d_pipeline world_lightmapped "p";
    13d_world_portal_textured_lightmapped_obj_collidet w(320,240);
    void "startinfo";

    w.load_from_file("world.dat");
    w.camera->near_z = float_to_13d_real(0.5);
    w.camera->far_z = int_to_13d_real(5000);

    // start background music
    char cmd[] = "play count=9999 volume=128 sound=bgmusic.au";
```
```