# Chapter 2

# Rendering and Animation Techniques for 3D Polygons

This chapter examines rendering and animation techniques for 3D polygons. In Chapter 1, we saw that the I3d library classes provide facilities for storing, grouping, and manipulating 3D polygons, objects, and worlds. We also saw that I3d classes can rasterize flat-shaded polygons by stepping along the polygon’s edges from top to bottom, and drawing horizontal spans of pixels between the left and right edges. In this chapter, we extend these basic polygonal techniques to achieve more interesting and realistic visual effects.

We cover the following topics in this chapter:

+   * 3D morphing (allowing a 3D object to smoothly change shape into another)
+   * Adding surface detail through texture mapping
+   * Using the symbolic algebra package Cale to derive the texture mapping equations
+   * Mathematical models for computing light intensities
+   * Rendering computed light intensities with light mapping
+   * Shadows

This chapter presents the following sample programs: `morph3d` illustrating vertex animation and morphing in 3D, `textest` illustrating texture mapping, and `lightmap` illustrating light mapping.

# Vertex Animation and 3D Morphing

The program `morph2d` from the companion book *Linux 3D Graphics Programming* already explained and illustrated the concept of morphing in 2D. As we used the term earlier, morphing referred to the change in shape of a polygon by interpolating the vertices in its vertex list between certain key frames or morph targets.

Here, we wish to extend the concept of morphing to 3D, and also to groups of polygons instead of single polygons. As it turns out, this is extremely easy. First of all, the vertex