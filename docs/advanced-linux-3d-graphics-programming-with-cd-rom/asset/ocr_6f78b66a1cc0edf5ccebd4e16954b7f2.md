ment implies that any techniques requiring a texture-world space or world-texture space conversion cannot be applied. In particular, the single-pass light mapping strategy of Chapter 2, using a single pre-tiled surface combining texture and light map information, cannot be applied with objects that have been textured through direct $(u,v)$ assignment, because this technique requires us to convert from texture (or lumpel) space back into world space, which is not (easily) possible if the $(u,v)$ coordinates have been arbitrarily assigned. Note that a two-pass light mapping strategy is still entirely possible even with arbitrarily assigned $(u,v)$ coordinates, because in this case the second lighting pass has nothing to do with the arbitrary $(u,v)$ coordinates, instead using a well-defined light map space. It’s only with the single-pass light mapping that we have problems.

For this reason, the Videoscope plug-in creates textured polygons, but not textured light mapped polygons.

# ## Testing the Morph in Blender

At this point, you should have a textured tree object, which was formed by deforming a cube in the second morph target.

You can preview the morph in Blender simply by using the arrow keys to change the active frame number; as mentioned earlier, Blender automatically interpolates the vertices between the positions saved within the vertex keys. If you want to see the animation without keyboard intervention, press **Alt+r**a within the 3DWindow. This animates the mesh automatically for a certain number of frames. Two buttons on the DisplayButtons control the starting and ending frames of the animation: the Sta button specifies the starting frame, and the End button specifies the ending frame. Press **Esc** to terminate the animation.

![](bbox=[0.15, 0.56, 0.85, 0.71])

# ## Exporting the Two Morph Targets

Once we are satisfied with the morphing animation, we can export the two (compatible) models as follows:

+   1.  Change to frame 1. Notice that the mesh appears cubical in the 3DWindow, as defined by the first vertex key.
+   2.  Press **Alt+w** and write the current mesh to the file `cube.obj`.
+   3.  Change to frame 21. The mesh appears as defined by the second vertex key.
+   4.  Press **Alt+w** and write the current mesh to file `tree.obj`.
+       That was the easy part. Now comes the more tricky part—exporting the texture coordinates.