9. Deselect all vertices, then select all faces which should use this texture space. For instance, if you just defined the FRONT texture space, then select all faces on the top of the cube.

![](bbox=[0.22, 0.18, 0.55, 0.48])

10. Click **New Face Property** in `blend_at` and wait for the command to complete. Notice that `blend_at` creates several new FACE `<>` lines, one for each selected face. Edit each of these lines to read:

```
FACE <> USES_TEX_SPACE <NAME>
```

where `<NAME>` is the name of the previously defined texture space, such as FRONT. Since there will be several faces using the same texture space, you can copy and paste text between lines to save work. Press **Ctrl+c** and **Ctrl+v** to copy and paste text, respectively.

11. Repeat this process of face classification by repeating from step 6 until all faces have been classified.

12. Click **Save** to save your changes to the attributes file.

Let’s step back for a moment and summarize what we have just done. We have created six extra right triangles, all located parallel to but slightly outside of the cube. We then marked each of these triangles as being a texture space, and then assigned the faces from each side of the cube to use the appropriate one of the six texture spaces.

One item deserves special comment, the reason that we create the triangles slightly outside of the cube. We do this for two reasons. First of all, we can easily see that these triangles are separate from the mesh geometry, giving us a visual cue that they are texture definition triangles. Second, the fact that the texture definition triangles are topologically separate from the rest of the mesh allows us to use a convenient feature of Blender, *linked selection*. Linked selection works in EditMode, and selects vertices starting at the mouse cursor location, extending the selection to all vertices that are connected by an edge to the original vertex. To try this, select the cube and enter EditMode. Move the mouse cursor near the middle of the cube, next to some vertex in the middle, but away from the magic vertices. Then press I for linked select. Notice that just the cube has been