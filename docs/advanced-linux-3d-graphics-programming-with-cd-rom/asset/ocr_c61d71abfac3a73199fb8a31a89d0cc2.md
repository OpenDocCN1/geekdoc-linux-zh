**NOTE** Small numerical inaccuracies during computation mean that we should, from time to time, ensure that all of the axis vectors in the matrix are orthogonal and of length one, a process called *orthonormalization*. We can do this by normalizing VRi and VUP, computing VFW as the cross product of VRi and VUP, then recomputing VUP as the cross product of VFW and VRi. At this point all three vectors should be at right angles to one another, and should be of length one.

Collision detection in `update` is almost identical to that for the class `l3d_camera_collidable`. We check the object’s bounding sphere against all polygons in the environment, and ensure that it collides with none. Additionally, we ensure that the object does not collide with any other plug-in objects in the environment. We use an `explosion_factor` variable to iteratively increase the size of the spring-like bounces which we perform after a collision is detected. In this way, multiple simultaneous collisions are eventually resolved by pushing the colliding objects apart again.

Collision detection is also used to detect when the object crosses through a portal from one sector into another. If this occurs, the object deletes itself from the previous sector’s object list, and enters itself into the new sector’s object list. This is so that when the new containing sector is drawn, it also correctly draws the object which just entered the sector.

The plug-in *destructor* and *copy data* functions are essentially identical to those of `vidmesh`.

# Listing 8-18: `seeker.h`

```
#include "../../dynamics/plugins/plugin.h"
#include "../../dynamics/colsp.h"

class l3d_texture_data;

typedef enum movement_states
{NONE, AROUND_VFW, AROUND_VRI, AROUND_VUP, ALONG_VFW, ALONG_VRI, ALONG_VUP} movement_states;

static const movement_states states_array[]=
{NONE, AROUND_VFW, AROUND_VRI, AROUND_VUP,
 ALONG_VFW, ALONG_VRI, ALONG_VUP};

class l3d_plugin_videoscape_mesh_seeker
{
public:
    l3d_plugin_environment *plugin_env;
    l3d_texture_data *tex_data;
    
    l3d_plugin_videoscape_mesh_seeker(l3d_plugin_environment *env);
    virtual ~l3d_plugin_videoscape_mesh_seeker(void);
    char mesh_fname[1024], texcoord_fname[1024], texture_fname[1024];
    
    int tick_count, max_ticks;
    movement_states movement_state;
    int turning_velocity;
    l3d_real moving_velocity;
};
```