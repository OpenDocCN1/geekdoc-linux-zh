interpolator class we used in 2D, `13d_vertex_interpolator`, can be reused for the 3D morphing case. Second, all polygons in a 3D object share a common vertex list; therefore, changing the vertex list in the object automatically redefines the geometry of all polygons in the object.

![](bbox=[0.15, 0.21, 0.38, 0.38])

> *Figure 2-1: Morphing in 3D is a simple extension of the same concept in 2D. We need only interpolate the vertex list, shared by all polygons, from one key frame to another. Here, we have a cube defined by vertices c1-c8, and a pyramid defined by vertices p1-p8. Each vertex c1-c8 is morphed to the corresponding vertex p1-p8, which morphs the cube into the pyramid.*

Note that in order to be completely correct, we would have to recompute the surface normal vector for all affected polygons any time we made any change to the vertex list. If we change one vertex in the vertex list, we would need to recompute the surface normals for all polygons using that vertex. If we change all vertices in the vertex list, as is usually the case with morphing, then we would need to recompute the surface normals for all polygons in the object. Also, any other geometry-specific information stored with the polygons or the object would need to be recomputed whenever we change the vertex list, because changing the vertex list is equivalent to changing the underlying geometry of the object.

In the following sample program `morph3d`, however, we won't be recomputing the normals, but rather just changing the vertex list. This leads to simpler and faster code, but is actually incorrect since the surface normals are no longer normal to the morphed geometry. Since we don't use the surface normal in this sample program, the fact that the post-morphing normals are incorrect is actually not noticeable.

![](bbox=[0.15, 0.69, 0.42, 0.82])

> *Figure 2-2: Surface normals or other additional 3D geometrical attributes are no longer accurate after morphing.*

# Sample Program: `morph3d`

Sample program `morph3d` displays a number of morphing pyramid objects in an interactive scene. Each pyramid slowly changes shape from a compact pyramid to a more elongated shape, then back again. You can interactively fly though the scene with the standard keyboard controls used in `13d` library: