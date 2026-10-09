
environment. If two vertices of a polygon lie on different faces of the environment map cube, we can split the polygon into two or more pieces, each lying on only one face of the cube.

With the spherical method, the environment map is a circular image representing the appearance of the environment as it would appear orthographically reflected in a sphere. The environment map in this case can be referred to as a *sphere map*. Physically, such sphere maps can be created by taking a photograph of a large chrome sphere with a camera located very far away from the sphere (to simulate orthographic viewing). Algorithmically, we can take a cubical environment map and warp it into a sphere by using image warping techniques, a technique documented in *Advanced OpenGL Game Development* [GOLD98]. Once you have such an environment map, you can then use the following equation to map from the 3D reflection vector *r* to the 2D (u,v) values in the environment map (the *m* value is a temporary magnitude value used in the computation and is not needed later):

```
m = \sqrt{r_2^2 + r_3^2 + (r_2+1)^2}

u = \frac{r_2}{m} + 0.5

v = \frac{r_3}{m} + 0.5
```

OpenGL directly supports sphere mapping, which means that it can compute these texture coordinates automatically for you by using the above equations. A sample code fragment that performs OpenGL sphere mapping follows.

```
glTexGeni (GL_S, GL_TEXTURE_GEN_MODE, GL_SPHERE_MAP);

glTexGeni (GL_T, GL_TEXTURE_GEN_MODE, GL_SPHERE_MAP);

glEnable (GL_TEXTURE_GEN_S);

glEnable (GL_TEXTURE_GEN_T);

glEnable (GL_TEXTURE_2D);

// polygon rendering comes here, e.g. glBegin (GL_POLYGON)

glNormal3f (nx,ny,nz);

glVertex3f (x,y,z);

// etc.. glEnd (GL_POLYGON);
```

The calls to glTexGeni turn on the OpenGL automatic texture generation, meaning that calls to glTexCoord4, which specify explicit texture coordinates, are not necessary; contrast this with the texture mapping Mesa rasterizer of Chapter 2.

For the generation of sphere maps, Mark Kilgard has written a library LibGLSnap, which creates a cubical environment map and then warps it into a spherical map for use by OpenGL sphere mapping. See *Advanced OpenGL Game Development* [GOLD98] for details. Such sphere maps can be generated dynamically, so that whenever the environment changes, the reflections also change. If the environment does not change, a static sphere map could be computed once and used.

> **NOTE** Blender supports rendering images with environment mapping, and was used to create the image of the environment mapped cylinder in Figure 7-1. You must use the TextureButtons in Blender to select an EnvMap texture to apply to a material, which is in turn applied to a mesh. When rendering a scene with environment mapping in Blender, notice that Blender briefly renders six small images, implying that it uses some variation of the cube map scheme. With the SaveEnvMap button in the TextureButtons, Blender allows you to save the computed environment map to a 2D Targa image file (you can convert it to another format with the GIMP program), which contains six small square images, one for each side of the cube. To use this environment map in your program, you would have to implement the cube mapping yourself, or warp the image into a sphere and use OpenGL's sphere mapping. See the Blender home page http://www.blender.nl for tutorials on environment mapping with Blender.

# Billboards

A billboard is a single texture mapped polygon which always rotates itself so that it directly faces the viewer. Billboards are also often called sprites. The texture image on the billboard is typically a 2D image of a more complicated 3D object. For instance, a 2D billboard could contain a pre-rendered image of a complex tree model containing hundreds of polygons. Then, we can approximate the visual appearance of the tree by rendering just one polygon. Thus, the purpose of using billboards is to create the illusion of complex geometry by using a single texture mapped polygon.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_500_0.png)

Figure 7-4: A billboard always changes its position so that it faces the viewer.

There are two main ways to define when the billboard “faces the viewer.” In one case, the billboard always rotates around all three axes so that it is perfectly parallel to the screen. We call such billboards screen-aligned billboards. Such billboards can be used for printing text (which is where the name billboard originally comes from), or for displaying explosions or smoke, as we see below. In the other case, the billboard only is allowed to rotate around one axis, typically its own up axis. We call such billboards axis-aligned billboards. This scheme can be used for modeling trees.

To perform the actual rotation for either kind of billboard, we must construct a rotation matrix rotating from the billboard’s current orientation to the desired orientation. Think of the billboard as being a camera with its own local coordinate system. The VUP axis points up the billboard, the VRI axis points horizontally along the billboard, and the VFW axis points along the billboard’s surface normal. These axes are the billboard’s current orientation. Then, express desired orientation in terms of vectors. For the screen-aligned billboard, the desired orientation is the camera orientation, with the same VUP vector but with reversed VRI and VFW vectors. For the axis-aligned billboard, the desired alignment can be expressed as a rotation of the current alignment around the billboard’s own VUP vector. Given the desired alignment, we can then construct a matrix converting from the original alignment to the desired alignment.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_501_0.png)

> Figure 7-5: Screen-aligned billboard. Regardless of the camera orientation, the billboard always faces the camera.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_501_1.png)

> Figure 7-6: Axis-aligned billboard. The billboard is only allowed to rotate about its vertical axis, meaning that a view from above does not cause the billboard to tilt backward.

Typically a billboard will have a so-called alpha channel. This is because the billboard polygon is usually rectangular, for simplicity, but the image on the billboard is not generally rectangular. This means that parts of the billboard rectangle are unused. We don’t want to draw the parts of the billboard that are unused, because then this would look as if we were sticking rectangular pictures all over the top of our scene—which is in fact what we are doing, but we can make it look better with an alpha channel. An alpha channel is a special type of color that specifies the transparency of an image. We can thus use the alpha channel to set the unused part of the billboard polygon to be transparent and the rest to be opaque.

An alpha channel is typically physically represented in memory by a certain number of bits. For instance, if we have a 24-bit red-green-blue (RGB) color model, with 8 bits each for red, green, and blue, then we can introduce an additional 8 bits for the alpha channel, giving a 32-bit red-green-blue-alpha (RGBA) color model. Graphics acceleration hardware often supports an alpha channel directly, whereas implementing alpha in software manually requires the rasterizer to check for alpha values and combine the new color with the previous color accordingly. (The situation is somewhat easier with just a 1-bit alpha channel, since no color mixing needs to be done; either you see the old color with an alpha of zero, or you see the new color with an alpha of one.)

![](img/a19d4e8b1d7eb6387691dc6c865430e6_501_2.png)

> Figure 7-7: An alpha channel allows us to see through the unused parts of a billboard, creating a natural appearance. The billboards on the left use no alpha channel, and it is obvious that they are rectangular textured polygons; the billboards on the right use an alpha channel.

Billboards can be used in combination with other techniques to create visual special effects, with fewer polygons than would otherwise be required. We'll now look at some of these techniques.

# Lens Flare

Lens flare is a phenomenon caused by the imperfection of real-world lenses when confronted with very bright light, causing a sparkle or flare to appear in the final image. We can use billboards to simulate lens flare, thereby giving or underscoring the appearance of bright light in an image. We simply render or draw a 2D image texture that looks like a small sparkle, then draw this texture onto a screen-aligned billboard. We can render the lens flare after all other geometry is rendered, so that the lens flares never appear to be obstructed by other geometry. Such an obstruction would make it clear that the lens flare is merely a textured polygon.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_502_0.png)

We can control the drawing of the lens flare with line-of-sight and distance parameters. For instance, we can model a bright light source as being behind a wall. If a straight line of sight from the camera to the light source exists, we can draw the lens flare billboard; otherwise, we do not draw it. This creates the desired effect of having the lens flare suddenly pop into existence as soon as the light is visible. We can also draw the lens flare billboard larger as we move closer to the light source, and smaller as we move away, by using a distance formula. Although the lens flare would already automatically increase in apparent size as we approach it due to normal perspective, we can exaggerate this effect by making the lens flare grow or shrink in size exponentially as we approach or recede from it. We would want to exaggerate the growth or shrinkage of the lens flare with distance because the lens flare should not appear to be a physical point in space that we can normally approach; it is instead a lens artifact that depends on our viewing position.
