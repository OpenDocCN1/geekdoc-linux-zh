
![](img/a19d4e8b1d7eb6387691dc6c865430e6_185_0.png)

1. Open an *ImageWindow* next to the *3DWindow*.
2. In the *3DWindow*, press **f** to enter *FaceSelect* mode.
3. If all faces are not selected, then press **u** until all faces are selected.
4. Press **Alt+z**. This turns on the textured display mode in the *3DWindow*. Since we are going to be editing texture coordinates on the mesh, it is important that we see the results of our work immediately in the *3DWindow*. (Type **t** to return to non-textured display and to toggle between normal wire-frame display and solid non-textured display.)
5. In the *ImageWindow*, click the **Load** button, and select an image file with square dimensions (width and height identical). Middle-click the selected filename to load it.

At this point, the texture image is loaded, and is mapped to every face on the polygon. The texture is mapped so that each face has a complete copy of the image. This is very similar to the default texture mapping used in the last sample program, along with the undesirable property that this is not in general the mapping that we want.

The way we change the mapping is as follows. In the *3DWindow*, first select the faces for which you wish to apply the texture in a different way. Then, type **u**. This brings up a pop-up menu that allows you to specify the mapping of the current texture image onto the selected faces. The various entries in the menu have the following meanings.

- **Cube**: Applies a cubical mapping to the faces. From the object center, an imaginary cube (consisting of six faces) is drawn around the object. The texture mapped onto the faces takes on the orientation of one of the six faces of the cube which is oriented most closely with the face. Mostly vertical faces get a texture mapping defined by the vertical sides of the cube; mostly horizontal faces get a texture mapping defined by the horizontal (top or bottom) sides of the cube. Mathematically, either the (x, *y*), (x, z), or (y, z) coordinates are used as the (*u*, *v*) coordinates depending on the normal vector to the face. A cubical mapping is good for mapping textures onto mostly horizontal or vertical surfaces, such as walls, floors, and ceilings.

- **Cylinder**: Applies a cylindrical mapping. The texture space is an imaginary cylinder drawn around the object, and the texture coordinates are determined by projecting vertices of each polygon onto this cylinder. A cylindrical mapping is good for wrapping a label texture around a bottle.

- **Sphere**: Applies a spherical mapping. The texture space is an imaginary sphere around the object, and the texture coordinates are determined by projecting vertices of each polygon onto the sphere. A spherical mapping is good for wrapping a texture around a sphere or sphere-like object—a creature’s head, for instance.

- **Bounds to 64, bounds to 128**: Uses the current projection of the polygons in the 3DWindow for computing the texture coordinates, rounding these to fit within a bounding box of 64 64 or 128 128 pixels, respectively.

- **Standard 64, standard 128, standard 256**: Uses the default square mapping, where every face is mapped to an identical square subset of the texture with a size of 64 64, 128 128, or 256 256 pixels, respectively. This is the initial face mapping.

- **From window**: Uses the current projection of the polygons in the 3DWindow for computing texture coordinates.

After selecting one of these mappings, Blender computes the mapping and stores a $(u, v)$ texture coordinate with every vertex of every selected face. The results of the mapping are immediately visible in the 3DWindow (assuming that textured display mode has been activated with Alt+z).

Furthermore, the $(u, v)$ mapping for the selected faces is displayed as a set of connected vertices in the ImageWindow. Remember that the ImageWindow displays the texture, which represents the texture space; the $(u, v)$ texture coordinates for each vertex are locations in texture space, which can thus be displayed as points on the image. Within the ImageWindow, you can then use the normal mesh editing keys to select, grab, scale, or rotate the $(u, v)$ coordinates within the ImageWindow, which has the effect of repositioning the point within texture space and thus assigning new texture coordinates to the original polygon’s vertex. This allows you, for instance,

![](img/a19d4e8b1d7eb6387691dc6c865430e6_186_0.png)

![](img/a19d4e8b1d7eb6387691dc6c865430e6_186_1.png)

Figure 3-10: Texture coordinates in the ImageWindow (right), which correspond to the vertices of the selected faces (left) and can be moved arbitrarily.

to exactly map a certain part of the texture to fill an entire face, by moving the points corresponding to the face’s vertices onto the appropriate locations on the image in the ImageWindow.

The texture file `treetex.jpg` (in the same directory as the `treemorph.blend` file) has been applied to the tree by using a cylindrical mapping for the trunk and a window-based mapping for the leaves. The texture file contains two parts. The top part of the texture is green, for the leaves; the bottom part of the texture is brown, for the trunk.

You can now see why we earlier stated that it is not necessarily very limiting that our VideoScope plug-in only allows one texture per object. By defining a suitably large texture containing many smaller images, and by assigning specific parts of the texture to specific faces, we can effectively apply several textures to different faces, even though physically we are only using one texture.

For this example of the palm tree, you can perform the mapping as follows:

1. Select all faces in the trunk of the tree model. You will need to rotate the model and extend the selection with **Shift+right-click** a few times to do this, because it is not possible to select a face when you are viewing it from its back side.
2. Press **u** and apply a cylindrical mapping to all the faces in the trunk of the tree.
3. In the ImageWindow, press **a** to select all texture vertices.
4. Press **s** to scale down the texture vertices vertically. Move the mouse cursor vertically towards the center of the selected vertices and middle-click. This limits the scaling in the vertical direction. Scale down the vertices until they are as high as the brown portion of the texture.
5. Press **s** to scale down the texture vertices horizontally. Move the mouse cursor horizontally towards the center of the selected vertices and middle-click. Scale down the vertices until they are as wide as the brown portion of the texture.
6. Press **g** to translate the texture vertices. Move them so that all vertices are located within the brown portion of the texture.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_187_0.png)

*Figure 3-11: The faces for the trunk are cylindrically mapped to just the brown part of the texture image.*

At this point, you have cylindrically wrapped the brown portion of the texture around the selected faces, which is a fairly good way of doing the mapping, since the trunk of a tree is essentially a cylinder.

Proceed in a similar fashion to wrap the green portion of the texture around the leaves, but use the From Window mapping. First, look at the tree from the side view in the 3DWindow so that the flat sides of the leaves are visible. Then, select all leaf faces, apply a texture mapping from the window view, and scale and translate the vertices in the ImageWindow to be positioned over the correct portion of the texture (the green part in this case).

![](img/a19d4e8b1d7eb6387691dc6c865430e6_188_0.png)

If you want to tweak the texture coordinates, you simply need to drag the appropriate vertices in the ImageWindow. Again, you would do this to exactly control which parts of the image get mapped to which parts of which faces. After repositioning a vertex in the ImageWindow, the 3DWindow automatically displays the results of the new mapping. To see the results of the mapping while you are still moving the vertex and before you have confirmed its new position, activate the Lock button in the header of the ImageWindow.

**CAUTION**: Single-pass light mapping does not work if $(u,v)$ coordinates have been directly assigned as described above.

It is important to note that manually assigning $(u,v)$ vertices in this manner creates a non-linear mapping between texture space and world space. Each vertex in the ImageWindow represents a vertex of a polygon in 3D space. By manually positioning these vertices in the ImageWindow, we create a connection between the vertex location in 3D space and a $(u,v)$ location in texture space. In other words, we create an *arbitrarily defined mapping* between world space and texture space. This means that with this method, we have no simple matrix that converts between texture and world space, as we did in Chapter 2, where we always used the texture space to calculate the texture coordinates as opposed to letting the user arbitrarily position them. The lack of a simple conversion between texture and world space when using direct $(u,v)$ texture coordinate assign-
