# Chapter 2: Rendering and Animation Techniques for 3D Polygons

v in screen coordinates. However, they will not be "too far" from the original values, since we know that the endpoints of the run are correct. The smaller the runs, the less noticeable the error, but the larger the runs, the fewer divisions we must perform and the better the overall performance of the texture mapping code.

![](bbox=[0.07, 0.22, 0.56, 0.46])

> Figure 2-38: *Dividing a horizontal row of pixels into runs. We only compute the true u and v values at the endpoints of the run. In between the endpoints, we linearly interpolate.*

We've now covered the theory we need to perform texture mapping. The approach implemented in 13d is the vertex-level approach, interpolating $u/z, v/z$, and $1/z$. Let's now look at the new polygon class needed to implement this texture mapping strategy.

# Associating Textures with 3D Polygons

The class 13d_polygon_3d_textured is a texture mapped polygon. It is a 3D polygon with a texture and with texture coordinates stored with each vertex index. The class 13d_polygon_ivertex_textured, inheriting from 13d_polygon_ivertex, allows us to store the texture coordinates. It is an index to a polygon vertex with an additional member tex_coord to store a texture coordinate. Note that we store the texture coordinates with the vertex indices and not with the vertices themselves. The vertices themselves are shared among all polygons in an object, but the vertex indices belong to each individual polygon. Since the texture coordinates must be associated with each vertex of a polygon, and since adjacent polygons sharing a vertex might nevertheless have different texture coordinates at the same vertex, we must store the texture coordinates with the polygon's own vertex index and not with the shared vertex. The class 13d_polygon_ivertex_textured_items_factory is a factory returning items of the new type 13d_polygon_ivertex_textured; recall, the 13d_list class internally stores a factory for production of new list items during automatic expansion of the list. The factory overrides the clone method to copy itself; when copying a polygon, we should also copy the vertex index factory so that the copied polygon can produce the same kind of vertex indices (textured or non-textured) as the original polygon.

Returning to the class 13d_polygon_3d_textured, the normal constructor replaces the iv_items_factory, responsible for producing vertex index items for the (inherited) lists ivertices, clip_ivertices, and temp_clip_ivertices, with the new factory so