
## 2. Select both meshes and join
Select both meshes and press Ctrl+j, Enter to join the selected meshes.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_392_0.png)

## 3. Enter EditMode and hide vertices
Enter EditMode by pressing Tab. Select all vertices except for those around the portals. Hide all of these vertices by pressing h.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_392_1.png)

![](img/a19d4e8b1d7eb6387691dc6c865430e6_392_2.png)

## 4. Align portal vertices
Move each vertex of each portal as close as possible to its corresponding vertex in the other portal with which it should overlap. Move vertices as usual by right-clicking and pressing g to grab them, then using either the arrow keys or the mouse to move the vertex to the desired position and pressing Enter. Switch frequently among top, front, and side views, zoom in closely, and also use the perspective view mode with interactive view rotation to check if the vertices really overlap. The danger is that they might appear to overlap from one viewing angle, but not from another; thus the importance of frequently switching among viewpoints while editing and of interactively rotating the view in perspective.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_393_0.png)

## 5. Select overlapping portal vertices
Select all portal vertices for the two portals which should overlap. Ensure that all vertices from both portals are selected; temporarily start then cancel a grab operation to verify this. If any vertices are not selected, they will appear to stick to their old positions during the temporary grab operation; in this case, use border select mode to select the still unselected portal vertices.

## 6. Remove double vertices
In the EditButtons, find the button **Rem Doubles**. This button removes overlapping or nearly overlapping vertices. Directly beneath this button is a NUMBUT labeled “Limit.” This button controls the minimum distance below which two vertices will be merged into one. Depending on how close you were able to move the vertices to one another, you will need to change this limit. For this example, the limit was set to 0.35.

## 7. Execute Rem Doubles
After setting the limit for double vertex removal, click **Rem Doubles**. Blender then displays a message showing how many doubles were removed. The count should be the same as the number of vertices in one of the portal polygons; if not, then the limit was set too low. In this case, set the limit slightly higher, and repeat step 6.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_394_0.png)

## 8. Verify double removal
After you believe that all doubles have been removed, verify this as follows. Select each individual vertex of the portal. Press g to temporarily enter grab. Move the mouse slightly to see if another vertex is lying “underneath” the selected vertex. After looking underneath the vertex, press Esc to cancel the grab. If any such vertex appears underneath the currently selected one, then it is a double vertex which has not yet been removed; thus, increase the limit and repeat step 6. If no such vertices appear underneath any of the portal’s vertices, then all doubles have been removed, and the same portal vertices are now shared among the two meshes.

## 9. Align portal vertices in a plane
After removing the doubles, it is likely that the vertices of the portal no longer lie within a plane. Ensuring that the vertices do lie within a plane is important since otherwise the portal will be non-planar, and portal crossing computations based on collision detection (see Chapter 8) will not function reliably. It is not absolutely essential to align the vertices in a plane (in other words, 3d programs will not crash if the vertices are not completely aligned), but it is best to try. Align the vertices in a plane as follows.

### 9a. Select portal vertices
Select all vertices belonging to the portal.

### 9b. Switch to top view
Switch to orthogonal top view. Remember the approximate orientation of the portal.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_394_1.png)

### 9c. Rotate to grid line
Rotate the portal so that it is parallel to a grid line. Press r, move the mouse to rotate, and press Enter.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_395_0.png)

Figure 6-28

### 9d. Side view rotation
If necessary, repeat the rotation process in orthogonal side view, again remembering the approximate original orientation in side view. Such a rotation would be necessary if the portal were tilted around the *x* axis so that it was not perfectly straight up and down. For this example, the portal is not tilted around the *x* axis, so no side view rotation is necessary. After such a side view rotation, switch back to top view. At this point, the portal should be aligned more or less perfectly vertically, and you should be looking straight down along the top edge of the portal.

### 9e. Adjust grid size
Adjust the grid size to be small enough so that the grid points (the intersections between the lines) are located fairly close to the portal vertices. In the 3DWindow, press **Shift+F7**, enter the desired grid spacing in the NUMBUT labeled “Grid,” then press **Shift+F5** to change back to the 3DWindow. Here, we have reduced the grid spacing from 1.0 to 0.1.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_395_1.png)

Figure 6-29

### 9f. Snap to grid
Press **Shift+s**, then select **Sel->Grid** from the menu. This snaps all selected vertices, which are all portal vertices, to the nearest grid point. Now it is clear why we reduced the grid spacing in the previous step: we don’t want the portal vertices to be snapped to vertices very far away, which would distort the shape of the portal.

### 9g. Align to single grid line
Now, all portal vertices lie on grid lines but not necessarily on the same grid line. Manually select and grab portal vertices so that from top view, they all appear to lie on the same grid line. Press and hold **Ctrl** while grabbing the vertices to ensure that they remain exactly on the grid lines. At this point, the portal should be completely planar, lying within the plane of the single grid line containing the vertices. Rotate the view interactively in perspective mode to verify that it looks approximately planar.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_396_0.png)

![](img/a19d4e8b1d7eb6387691dc6c865430e6_396_1.png)

### 9h. Restore original orientation
Select all portal vertices, switch to orthogonal top view, and rotate the portal so that it has its original orientation as seen from top view. In other words, you now undo the rotation you did earlier. Do the same in orthogonal side view, if you rotated the portal in side view. The portal is now planar, but with its original orientation.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_397_0.png)

### 9i. Display hidden vertices
Press **Alt+h**. This again displays all hidden vertices.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_397_1.png)

### 9j. Check other polygons
Conceivably, through the process of snapping portal vertices to make the portal polygon planar, other four-sided polygons which shared the same vertices are no longer planar. (This is not an issue with triangles, since a triangle is always planar.) Visually check for any such anomalies, and make any such polygons planar by a similar process: select polygon, hide everything else, rotate, snap to grid, align to one single grid line, rotate back.

## 10. Separate meshes
Finally, select the vertices of each convex part of the mesh, and press **p**, **Enter** to separate these into separate meshes. At this point, you have separate convex meshes, which line up exactly on the portals.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_398_0.png)

Figure 6-34

To summarize the idea of aligning portals, we join meshes together and eliminate duplicate vertices around the portal so that both meshes share identical vertices along the portal boundary. Then, we make the portal planar by rotating it into a convenient grid-aligned orientation, snapping it to a plane on the grid, then rotating it back. Finally, we separate the mesh back into individual pieces, which automatically causes duplication of the shared vertices along portal boundaries. This means that the portals align exactly.

# Tips for Working with Portals

Now that we understand how to create sectors with portals that line up exactly, let’s review some tips for effectively working with this system. We saw most of these tips in the tutorials above, but the last few tips in the list are new.

- Temporarily grab vertices to see if there are any hidden vertices underneath a given vertex; cancel the grab with Esc.

- Switch often between multiple viewpoints, and rotate the view interactively in perspective mode, to get a spatial feeling for which vertices are selected. Also, temporarily grab the selection and move the mouse to move the selection around; this way, you can verify which vertices are selected.

- Snap vertices to the grid to create precise alignments. For exact planar alignment on arbitrarily oriented portals or polygons, first rotate the polygon to align with the grid, snap the vertices to one grid line, then rotate the now-planar polygon back to its original position. Exact alignment of two vertices, as required for portal joining, can be achieved by manually moving vertices close then increasing the Rem Doubles limit, or by snapping vertices exactly to one another as follows: select the first vertex, press **Shift+c**, select **Curs->Sel**, select the second
