# Gouraud Shading

A technique developed by Henri Gouraud for shading triangles in which each corner of the triangle is given its own color, and the triangle is then drawn with an even blend of all three colors, one smoothly transitioning to the next. Such shading is intended to be used in 3D images.

chosen as an imaginary source of light, and virtual “rays” are beamed from that spot to every visible point in your 3D image. As the “rays” strike, color values are generated, and a 2D screen image is created. This procedure results in a very realistic-looking picture, although what’s gained in realism is offset by the enormous toll on the processor.

Figure 13.1 shows how the screen sits in relation to the light source and the rendered spatial objects.

# Code For Raytracing

The two examples I’ve included here were created by an extraordinary programmer, Mr. Marcus Geelnard. Geelnard, a university student in Sweden, has managed to come up with some very inventive code in his spare time. Fortunately for me, he’s not yet out in the working world, or I might not have a job! All jokes aside, I think you’ll appreciate the brevity and simplicity of his code.

MinRay, shown in Listing 13.1, is a “minimal” raytracer—although it holds its own against the competition quite nicely. This small program was written as a demonstration of how a raytracer works. The output is phenomenal for such a compact piece of code—see for yourself in Figure 13.2.

Regarding programming, one important mathematical simplification has been made: the camera (viewing point) is fixed in (x,y,z)={0,0,0}, thus making for easier equations.

MinRay writes a 24-bit, 640-by-480 pixel PPM image directly to the standard output, so you’ll have to redirect it to a file (for example, minray > output.ppm). Enjoy!

![](bbox=[0.15, 0.71, 0.44, 0.84])

Figure 13.1
Layout of a raytraced scene.