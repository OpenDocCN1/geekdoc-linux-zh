
...ment implies that any techniques requiring a texture-world space or world-texture space conversion cannot be applied. In particular, the single-pass light mapping strategy of Chapter 2, using a single pre-tiled surface combining texture and light map information, cannot be applied with objects that have been textured through direct $(u,v)$ assignment, because this technique requires us to convert from texture (or lumpel) space back into world space, which is not (easily) possible if the $(u,v)$ coordinates have been arbitrarily assigned. Note that a two-pass light mapping strategy is still entirely possible even with arbitrarily assigned $(u,v)$ coordinates, because in this case the second lighting pass has nothing to do with the arbitrary $(u,v)$ coordinates, instead using a well-defined light map space. It’s only with the single-pass light mapping that we have problems.

For this reason, the Videoscope plug-in creates textured polygons, but not textured light mapped polygons.

## Testing the Morph in Blender

At this point, you should have a textured tree object, which was formed by deforming a cube in the second morph target.

You can preview the morph in Blender simply by using the arrow keys to change the active frame number; as mentioned earlier, Blender automatically interpolates the vertices between the positions saved within the vertex keys. If you want to see the animation without keyboard intervention, press **Alt+r**a within the 3DWindow. This animates the mesh automatically for a certain number of frames. Two buttons on the DisplayButtons control the starting and ending frames of the animation: the Sta button specifies the starting frame, and the End button specifies the ending frame. Press **Esc** to terminate the animation.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_189_0.png)

## Exporting the Two Morph Targets

Once we are satisfied with the morphing animation, we can export the two (compatible) models as follows:

- 1. Change to frame 1. Notice that the mesh appears cubical in the 3DWindow, as defined by the first vertex key.
- 2. Press **Alt+w** and write the current mesh to the file `cube.obj`.
- 3. Change to frame 21. The mesh appears as defined by the second vertex key.
- 4. Press **Alt+w** and write the current mesh to file `tree.obj`.
    - That was the easy part. Now comes the more tricky part—exporting the texture coordinates.

## Exporting the Texture Information

The Videoscape file format does not store texture coordinates, so by exporting the morph target meshes to Videoscape, we lose the texture information. One simple solution is to export the file in VRML format, which is also an ASCII file format but is slightly more complicated to parse than Videoscape. With VRML export, Blender does save the texture coordinates in the VRML file. Fortunately, the ordering of the vertices and faces is the same in the Videoscape and the VRML files. This means that to associate texture coordinates with our Videoscape format objects, we can simply cut out the texture coordinate mapping within the VRML file, save it to a separate texture coordinates file, and read in this file later while reading in the Videoscape file.

> **NOTE** The newest free version of Blender supports Python scripting (previously this was only available in the commercial C-key version). Therefore, it should also be possible to write a Python script to export the texture coordinates.

The texture coordinates file is the mesh.uv file we spoke of earlier when discussing the parameter string passed to the Videoscape plug-in object. It is simply an ASCII file, where each line contains a single $(u,v)$ coordinate. The ordering of the lines in the texture coordinates file should be the same as the order of the vertex indices defining the faces in the Videoscape file. Note that the texture coordinates are associated with each vertex index defining a face, and not with the common vertices shared by all faces. This is because even though two adjacent faces may share a vertex, the texture coordinate at the shared vertex might be different for the two faces. Thus, texture coordinates are defined per face, and the texture coordinates file specifies one $(u,v)$ coordinate for each vertex index of each face.

Again, you can create this texture coordinates file simply by cutting out the appropriate portion of a VRML exported file, as follows:

- 1. Save the file as VRML by pressing Space to bring up the Toolbox, choosing File, then Save VRML.
- 2. Edit the VRML file in your favorite text editor. Search for the beginning of the definition of your mesh object; the line begins with the keyword DEF (for definition) and contains the name of the mesh.
- 3. Search for the texture coordinate definition for this mesh. It follows the DEF line and begins with the keyword TextureCoordinate2. Following this line is a list of several texture coordinates.
- 4. Save the list of texture coordinates into a separate file. I suggest giving this file an extension of .uv, for instance, meshname.uv.
- 5. Specify this meshname.uv file in the parameter string passed to the Videoscape plug-in object, as discussed earlier. In this way, the $(u,v)$ coordinates are read out of the file while loading the geometry from the Videoscape mesh file, and the texture mapping is applied.

> **CAUTION** VRML export of texture coordinates on triangular faces does not appear to work in Blender. So, only use quadrilaterals if you wish to export texture information.

Unfortunately, it appears that there is a small bug in the Blender VRML export of texture coordinates with triangular faces. In the experiments I performed, the VRML exported texture coordinates are simply not correct if the faces are triangular. Making the faces into quads (four-sided) seems to fix the problem. Thus, to export manually assigned texture coordinates in this manner, make sure all your faces have four sides.

Also, notice that the orientation of the $v$ axis in texture space is different in Blender/VRML than it is in l3d. We have been using the convention that the upper-left pixel in the texture image is $(0,0)$ in texture space. Blender's exported VRML texture coordinates, however, take the lower-left pixel as point $(0,0)$ in texture space. This means that, for texture coordinates in the range 0.0 to 1.0 (which is the case if all of the texture coordinates lie within the image in Blender's ImageWindow), the $v$ coordinate we use in l3d is $1.0-v$ from the `mesh.uv` file, which essentially flips the orientation of the $v$ axis.

# Importing the Morph Targets into a Program

The program `vids3d` imports our morph-compatible meshes and performs a morph between the cube and tree shapes.

> Listing 3-1: File shapes.h, program vids3d

```cpp
#include "../../lib/geom/object/object3d.h"
#include "geom/vertex/vertidx.h"
#include "dynamic/cg/plugns/plugenv.h"

class pyramid:public l3d_object {
    static const int num_keyframes = 2;
    int keyframe_no;
    l3d_two_part_list<l3d_coordinate> *keyframes[2];
    l3d_vertex_interpolator interpol;
    bool currently_interpolating;
    public:
    pyramid(l3d_two_part_list<l3d_coordinate> *keyframe0,
            l3d_two_part_list<l3d_coordinate> *keyframe1);
    virtual ~pyramid(void);
    int update(void);
};
```

> Listing 3-2: File shapes.cc, program vids3d

```cpp
#include "shapes.h"
#include <stdlib.h>
#include <string.h>
#include "../../lib/tool_os/memman.h"

pyramid::pyramid(l3d_two_part_list<l3d_coordinate> *keyframe0,
                 l3d_two_part_list<l3d_coordinate> *keyframe1)
:
    l3d_object(100)
{
    keyframes[0] = keyframe0;
    keyframes[1] = keyframe1;

    currently_interpolating = false;
    keyframe_no=0;

    pyramid::~pyramid(void) {
        //- set vertices pointer to NULL to prevent parent l3d_object from trying
        // to delete these vertices, because they do not belong to us
        vertices = NULL;
    }

    int pyramid::update(void) {
        if(currently_interpolating) {
            vertices = interp_list;
            if(i_interp_step()) {
                currently_interpolating = false;
            }
        }else {
            keyframe_no++;
            if(keyframe_no >= num_keyframes) {keyframe_no = 0;}
            int next_keyframe = keyframe_no + 1;
            if(next_keyframe >= num_keyframes) {next_keyframe = 0;}

            vertices = keyframes[keyframe_no];
            interp_start( *keyframes[keyframe_no], *keyframes[next_keyframe],
                rand()%100 + 50, 3);
        }
        currently_interpolating = true;

        //-- it is important to recalculate the normals because the mesa
        // texture mapping reverse projection relies on correct normals!
        int i;
        for(i=0; i<polygons.num_items; i++) {
            polygons[i]->compute_center();
            polygons[i]->compute_sfnormal();
        }
    }
}
```

> Listing 3-3. File main.cc program vids3d

```cpp
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <math.h>

#include "../lib/geom/object/object3d.h"
#include "../lib/geom/polygon/p3d_flat.h"
#include "../lib/tool_2d/screen.h"
#include "../lib/tool_os/dispatch.h"
#include "../lib/raster/rast3.h"
#include "../lib/tool_2d/scriinfo.h"
#include "../lib/geom/world/world.h"
#include "../lib/system/act0.2.h"
#include "../lib/pipeline/pi_word.h"
#include "../lib/dynamics/plugins/pplugin.h"
#include "../lib/geom/texture/tl_ppm.h"
#include "../lib/dynamics/plugins/vidmesh/vidmesh.h"
#include "../lib/tool_os/memman.h"

#include "shapes.h"

#include <stdlib.h>
```
