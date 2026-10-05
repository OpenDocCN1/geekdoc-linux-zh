# Tutorial MonoGame

# # Apply textures in MonoGame for realistic models

Bitmaps provide a significant boost to image quality while not increasing resource consumption

The past few tutorials in this series have promoted a solid understanding of models, the rendering pipeline and the role of shaders. Essentially, a shader is a program that handles part of the projection which transforms three-dimensional objects into two-dimensional scenes for display on a PC screen. Sadly, the creation of realistic geometric detail is difficult. If achieved, the amount of vertices needed sky-high - at some point, even the mesh becomes seamless.

Textures provide a nice workaround. Think of them as skins that wrap around the vertices: instead of rendering every part of a model in one colour, the colour values are obtained from a texture. With a lightning-fast, hardware-accelerated lookup process, and consider yourself in heaven.

As this tutorial teaches texture handling, we will abandon the pre-manufactured models used in the installments of the tutorial. Instead, we will return to the manually-created cube that we used previously. Our example was based on the VertexPositionColor class, which consists of a Vertex coordinate along with a colour:

| public class CubeClass |
| public VertexPositionColor[] my; |

Texturing is understood if we start with a little illustration. The left-hand image on the next page shows a plane described by three-dimensional vertex coordinates (with the triangle with the gradient). In addition to that, each of the 'edges' is also a set of two-dimensional coordinates.

These coordinates - referred to as extras or texture coordinates - map each of the vertices to the bitmap. When the GPU interpolates the position, thereby the correct colour automatically.

### Atlas's texture

One theory is out of the way, it is to update our cube coordinates. XNA and MonoGame, vertex information is stored in classes which implement the IVertex interface - for our purposes, VertexPositionTexture class shall suffice. Refactor it to receive the code shown:

![](bbox=[0.058, 0.263, 0.193, 0.363])

![](bbox=[0.206, 0.603, 0.903, 0.733])

![](bbox=[0.058, 0.743, 0.193, 0.903])

+   - **Tom Hanna**
- had no idea what he was doing until his lap and after found himself new prototyping to reach familiarity with much more knowledge that transfers across seamlessly

+   - **Resources**
- MonoGame
monogame.net

+   - Here's the simple texture we wrapped around our cube; mirrored to form a square for each face