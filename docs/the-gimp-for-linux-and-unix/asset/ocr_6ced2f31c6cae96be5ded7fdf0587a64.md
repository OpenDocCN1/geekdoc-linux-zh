# The Bezier Selection Tool

The Bezier Selection Tool creates selections using control points, levers, and handles (Figure 20). The handles determine the curvature of segments of the selection boundary. The levers are just a visual representation of which handle goes with which control point.

With the Bezier Selection Tool, you can create straight selection segments and curvy segments. After you have created a bezier selection, you can edit it, using the control points and handles to change the shape of the selection segments.

When creating a selection with the Bezier Selection Tool, it's easiest to use the following steps:

+   - Create a basic, straight segment selection;
- Move any control points that are out of place; and then
- Edit the control points to add curves and sharp bends.

To create the basic, straight segment selection:

+   1. Use the Layers & Channels dialog box to set which layer is active. (This is the layer whose pixels will be selected.)
2. Click the Bezier Selection Tool in the Toolbox or press B on the keyboard.
3. Position the mouse crosshair over image where you would like the first segment to start.
4. Click. A circular control point will appear where you clicked (Figure 21).

![](bbox=[0.068, 0.035, 0.467, 0.31])

Figure 20. The control points and handles control the shape of a bezier selection boundary. In this figure, a bezier selection boundary has been shaped around the outer edge of the jabbitrack.

![](bbox=[0.068, 0.435, 0.467, 0.655])

Figure 21. A circular control point appears where you click the mouse.

# Closing an Image while a Selection is Active

If you are working on an image saved in the native GIMP file format, xcf, and close it while a selection is active, that selection will still be active and available the next time you open the file.

(continued)