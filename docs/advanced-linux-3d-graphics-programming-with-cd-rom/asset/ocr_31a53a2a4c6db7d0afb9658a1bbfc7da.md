and expressive walking motion. As mentioned earlier, this tutorial is only meant to introduce you to some of the important aspects of character animation. For now, just make the arms and legs swing back and forth over time.

Remember, you don’t have to specify too many key frames; Blender interpolates the positions between the key frames to create a smooth animation. In this example, I created five key frames, at frames 1, 21, 41, 61, and 81. For each key frame, I positioned the effectors of the arm and leg Ikas, and inserted a key for each effector. Key frame 81 is identical to key frame 1, so that the animation—in this case, a walking motion—appears to loop.

Although it’s not important for exporting the results (which we do later in this tutorial), it is a nice feature to make the animation loop in Blender. This way, can let your animation run several times to see how it looks in a loop. You can do this by selecting an Ika, changing to the IpoWindow, and clicking on the W-shaped button, which represents a repeating angular curve. This button sets the extend mode for an interpolation curve to be cyclic; the curve then repeats its shape infinitely. Do this for all Ika curves by selecting each Ika in turn and setting its curves to be cyclically extended. In this way, the entire animation is then cyclic or looped. View the animation, as mentioned in the previous morphing tutorial, with **Alt+a**.

Now, we have a walking motion through our Ikas, but still have no polygonal model. The goal is to animate a polygonal model in a walking motion. Thus, the next step is to associate a series of meshes with the Ikas.

# ## Connecting Ika Chains and Meshes

Ideally, we would like to create one single polygonal model with arms and legs, and associate each part of the model with its appropriate Ika—arm polygons with the arm Ikas and leg polygons with the leg Ikas. Unfortunately, this is not currently possible in Blender. In Blender, an Ika always affects an entire mesh, not just part of a mesh. So, we must split up our human-like model; in particular, the rule is. Each limb in each Ika must be associated with a separate mesh.

This rule ensures that the shape of each limb never changes. If we just had one mesh for several limbs (doing this would incidentally require us to create a skeleton with **Ctrl+K** as mentioned earlier), then this one mesh would be stretched and distorted based on the influence of several Ika limbs simultaneously. While this is fine for animating amorphous shapes (such as a sack of flour) without well-defined appendages, it looks rather ugly for shapes such as humans with arms and legs which shouldn’t drastically change shape when they bend.

This rule, that we need a separate Ika for each mesh, means that we need two meshes for each arm, two meshes for each leg, and one mesh for the main body. We also add in an additional mesh for the head, even though it is not connected to any Ika in this example. Our humanoid figure thus consists of ten separate meshes.

For each Ika limb in the arm and leg Ikas, proceed as follows:

+   1. Create a new tube mesh, and position and scale it in 3D space so that it exactly surrounds the appropriate limb.

+   2. Select the tube and the Ika, with the Ika active.