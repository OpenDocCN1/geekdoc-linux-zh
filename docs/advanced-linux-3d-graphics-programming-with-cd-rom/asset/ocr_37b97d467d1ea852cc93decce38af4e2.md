![](bbox=[0.15, 0.11, 0.27, 0.22])

*Figure 2-16: Gouraud shading makes a surface appear smooth and round.*

Note that Gouraud shading is not always desirable, because it “washes out” all the sharp changes in light intensity which occur over the entire 3D object. If the object being modeled is supposed to appear round, then this is fine. But, if the object is supposed to have some sharp corners or edges, then the light intensity should indeed change suddenly from one face to the next because of the physical properties of the surface. But simple Gouraud shading would smooth over all sharp changes in light intensity, including the desired ones.

![](bbox=[0.15, 0.39, 0.46, 0.58])

*Figure 2-17: Gouraud shading eliminates all sharp edges, even if these edges should actually appear.*

Solving this problem would require storing vertex normals per polygon instead of per object; this would effectively allow each shared vertex to have several vertex normals, one for each face touching the vertex. All vertex normals for one vertex would be the same if the surface is supposed to appear rounded at that point; the vertex normals would be different if an edge should appear between the adjacent faces.

A popular technique for allowing smooth edged polygons and sharp edged polygons in the same model is to use *smoothing groups*. With this technique, we assign a 32-bit long integer to each polygon, which is then treated as 32 Boolean flags. During the creation of a 3D model, the 3D artist can turn each of these on or off. When determining each vertex normal for a polygon, the long value is subjected to a logical AND operation with the long value of each neighbor. If the result is not zero, the neighbor’s normal is included in the calculation; if it is zero, that neighbor is excluded. This means that each vertex can have more than one vertex normal depending on which polygon it is being considered for. By carefully setting the bits, the artist can specify which polygons affect which adjacent polygons, and thereby control smoothing (or lack thereof) on each edge.