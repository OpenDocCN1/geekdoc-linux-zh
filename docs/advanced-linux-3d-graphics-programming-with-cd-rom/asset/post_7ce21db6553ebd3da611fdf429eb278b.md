
![](img/a19d4e8b1d7eb6387691dc6c865430e6_386_0.png)

> Figure 6-11: Free edges have a polygon on just one side. A consecutive series of free edges forms a hole in the sector, and thus is a portal.

Note that such an implicit definition of a portal rules out the possibility of two exactly adjacent portals sharing one edge (such a portal would appear to the viewer to be one portal), since the shared edge in this case has no geometric polygons on either side, just portal polygons, meaning that the edge is not saved by Blender as part of the geometry. Even if such an invisible edge between adjacent portals were saved with the geometry, we still would not know whether one large portal or two smaller ones were wanted, since both would form valid loops of free edges. With the system described here, specifying adjacent portals is not possible; because of the lack of a separating edge, the two adjacent portals are automatically combined into one larger portal. This would be incorrect if we wanted two adjacent portals which lead to different sectors. Supporting such cases would require explicit rather than implicit specification of portals, and would probably require writing a custom world editor from scratch. The reason for this is that polygons in Blender can only have three or four sides, but portal polygons can have a greater number of sides. Since Blender doesn’t allow us to specify arbitrary convex polygons with more than four sides, this means that explicit portal specification, and the ability to have two exactly adjacent portals leading to different sectors, requires another tool. Note that the 13d classes for handling portals have absolutely no problem with adjacent portals; the only problem here is the specification of such adjacent portals within a modeling tool.

Portal connectivity (which sector is connected to a portal) is also implicit. Once we have a list of portals (holes) in each sector, we then search for portals whose vertices exactly overlap. Each such portal is then connected with the sector of the other portal.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_387_0.png)

![](img/a19d4e8b1d7eb6387691dc6c865430e6_387_1.png)

> Figure 6-12: Portal connectivity is implicitly determined by overlapping of portals. Here, portal A.0 of sector A exactly overlaps with portal B.0 of sector B. Therefore, portal A.0 is connected with sector B. Also, portal B.0 of sector B exactly overlaps with portal A.0 of sector A; therefore, portal B.0 is connected with sector A. Portal B.1 in this figure is not connected to any sector.

> Figure 6-13: Slightly misaligned portals means that no corresponding overlapping portals will be found, and that portals are left unlinked. Here, no portals overlap with one another, meaning that no portal connectivity could be automatically determined.

This implies that precise alignment of the vertices of the portals in adjoining sectors is essential to correct operation of this system. If portals from adjacent sectors do not align exactly, then the world editing system will not be able to find overlapping portals, and will thus be unable to connect portals to their target sectors.

Let’s now see how we can best create such sectors and portals within Blender, so that the portals line up.

## Tutorial: Creating Aligned Portals via Extrusion and Separation

The best way of aligning the vertices of portals is to initially create separate sectors as one mesh, then later separate parts of the mesh into individual sectors. The idea is to cut a portal into a sector by deleting some faces. Then, we select the vertices along the edges of the deleted faces and extrude these vertices, producing a tunnel which exactly lines up with the portal we created. Finally, we separate the original sector and the extruded tunnel into two separate meshes, automatically preserving the overlapping of the portals. The following tutorial illustrates how to do this.

- 1. Begin with an empty Blender window. Ensure that Draw Faces is activated in the EditButtons (F9).

- 2. Create a simple cubical sector. Press Shift+a, select Mesh, then Cube.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_388_0.png)

- 3. Select the vertices of a face in which you wish to have a passageway to another sector. You can either use border select mode (press b) or you can individually Shift+right-click each of the desired vertices.

- 4. Subdivide the face until enough smaller faces appear so that you can remove a few to create a small hole in the face. With a face selected, subdivide it as follows: press w, then select Subdivide from the menu. Here, we have subdivided the far face twice, yielding 16 smaller faces.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_388_1.png)

- 5. Select the vertices of the faces which you wish to remove, and delete the faces only by pressing x, then select Faces. The faces should all lie within one plane. Here, we have deleted the four faces in the bottom center of the subdivided face, creating a small doorway.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_389_0.png)

- 6. Select the vertices lying on the edges of the faces you just deleted. Extrude the vertices by pressing e, Enter, drag the mouse, and left-click to finish. It is easiest to perform the extrusion in the top, front, or side orthogonal views (press 7, 1, or 3 on the numeric keypad to choose these viewpoints, and press 5 to toggle between orthogonal and perspective viewing). This extrusion creates a tunnel or corridor.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_389_1.png)

- 7. Select just the vertices of the original mesh, and separate them from the newly extruded tunnel by pressing p, Enter. The selected vertices are then removed from the current mesh and moved into a new, separate mesh. The vertices of the open part of the tunnel exactly match up with the vertices in the open part of the original sector mesh, meaning that the two portals between the two sectors exactly overlap.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_390_0.png)

By repeatedly extruding sectors in this way, we cause the creation of corridors or rooms that are built upon the existing vertices of the polygonal portal. Then, by separating the geometry into separate meshes, we cause exact duplication of the portal vertices. Thus, the general procedure is: create a mesh, cut a hole to form a portal, extrude the portal, separate the mesh into two sectors.

## Tutorial: Aligning Portals from Separate Meshes

The previous example showed you how to create a mesh via extrusion of a portal, and separation of the mesh into pieces. But sometimes you already have two separate sectors, which were created independently and not via extrusion of a portal. You can also connect these sectors via portals. To do this, each sector must have a portal with the same number of vertices and edges. The idea is to join the meshes together into one mesh, manually eliminate duplicate vertices around the portals so that both meshes share exactly the same vertices along the portal, and then separate the meshes again so that the resulting portals align exactly.

The following tutorial shows you how to align portals from two separate meshes. The files from this example may be found in directory $L3D/data/levels/tworooms.

- 1. Create a cube with an extruded tunnel as in the last example.

- 2. Exit EditMode. Duplicate the mesh so that there are two copies of the mesh: select the mesh, press Shift+d, move the copied mesh to its new location, and left-click.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_390_1.png)

![](img/a19d4e8b1d7eb6387691dc6c865430e6_391_0.png)

- 3. To make this example more difficult—and more realistic—switch to top view and rotate the meshes so they are positioned diagonally facing one another. This makes the example more difficult because the portals now lie on an arbitrary plane in space instead of being neatly axis-aligned. When working with real models, you will encounter arbitrarily aligned portals.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_391_1.png)

Now, we have a typical situation where we have two separate, arbitrarily aligned meshes, each having a portal with identical vertex and edge counts. What we now want to do is join the two tunnels with one another via a portal.

- 4. Move the meshes together so that the portals align as closely as possible.
