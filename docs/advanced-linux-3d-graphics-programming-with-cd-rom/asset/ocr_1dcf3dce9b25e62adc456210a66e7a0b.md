![](bbox=[0.15, 0.11, 0.61, 0.32])

Figure 2-13: Correct radial fog versus simpler z depth fog.

Having decided on a distance to use (radial distance or z depth distance), we then need to map this distance into a fog value from 0 to 1. We can choose to map the fog linearly or exponentially. A linear mapping causes colors to fade out at a constant rate as they move into the fog. An exponential mapping causes colors to fade out more quickly as they recede into the fog. We can even use a discontinuous fog function to cause fog only to appear at certain distances from the viewer.

> **NOTE** An option somewhere between z depth fog and radial fog is to approximate radial fog by taking the z depth value, then subtracting a percentage of x and y deviation from the center of the screen. This is more accurate than z depth fog, but still faster than true radial fog.

Notice that regardless of the means of computing fog, the computation is done in camera coordinates because fog is an effect which depends on distance from the camera. This is another example of why we need the camera_transform method in classes l3d_object and l3d_polygon_3d, which allows us to save the camera space coordinates for later use. The fog computation is typically done just before polygons are about to be drawn to the screen in the rasterizer; at this point, however, the polygons have already undergone the perspective transformation, meaning that we must have previously saved the camera space coordinates in order to perform this late fog computation.

# # Rendering Techniques for Drawing Light

The previous sections dealt with the mathematical computation of light intensities based on the properties and orientations of the light sources and the surfaces. We haven’t yet addressed the issue of how often and exactly at which points in 3D space we need to evaluate the lighting equations. It turns out that this issue depends on the rendering technique we use for drawing light on our polygons. Such rendering techniques are also called shading techniques.

Let’s now look at a number of rendering techniques for light, and also at the implications that each technique has on the frequency and location of lighting computations.

> **TIP** The rendering or shading technique influences how many lighting calculations we perform and at which points in 3D space.