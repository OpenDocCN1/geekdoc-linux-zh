![](bbox=[0.14, 0.12, 0.57, 0.39])

*Figure 3-6*

+   5. Press **Right Arrow** to return the frame number back to frame 21. Notice that the sharp point reappears as you approach frame 21, the time at which the second vertex key was inserted. Importantly, and quite fortunately, if we save a Videoscape mesh from Blender, the exported geometry reflects the current state of the mesh for the currently active frame. This means that to export two compatible morph targets, we simply change to frame 1, write the first mesh, then change to frame 21, at which point Blender automatically interpolates the vertices to the second vertex key, and write a second mesh.

Now, you should again be at frame 21. Your job now is to enter EditMode and deform the mesh into something interesting. Any shape will do, but for this tutorial I chose to deform the mesh into the shape of a palm tree. Here are some hints for making the palm tree:

+   1. Start by making the bottom half of the cube longer and thinner to represent the trunk. Next, make the top flat and somewhat x-shaped. Finally, pull down the outer edges of the top x to make the leaves droop down.
+   2. Select groups of vertices using border select mode, and translate, rotate, or scale these groups of vertices. Creating the tree by moving each vertex individually would be very time consuming.
+   3. Be careful not to pull vertices around in physically impossible ways. For instance, if a vertex is originally on one side of an edge in the original model, you should not pull the vertex such that it is on the other side of the edge. If you do so, this would reverse the front/back orientation of the faces connected with the vertex, which leads to incorrect display later. Think of yourself as a sculptor working with a malleable medium; you can stretch or compress the balloon to change its shape, but if you try to poke the balloon through itself, the whole thing blows up in your face.