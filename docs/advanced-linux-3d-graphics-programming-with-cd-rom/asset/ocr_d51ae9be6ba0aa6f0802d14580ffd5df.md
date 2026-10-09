+   Define polygons as portals
+   Link portals with sectors
+   Place plug-in objects with sectors
+   Define the geometry, texturing, position, orientation, and behavior of plug-in objects

These requirements are fairly modest, but given the fact that plug-in objects can have any appearance and behavior, defined via a plug-in file which is external to the world editing system, the system does allow for creation of interesting, dynamic worlds.

The next three sections look at one system for using Blender to reach these goals. We look at this world editing system from three different perspectives. First, we look at the Blender features we use, the limitations of those features, and ways of working around these limitations. Second, we look at the system from a step-by-step perspective, as you would view the procedure when creating a world. Finally, we look at the system in terms of data flow. After understanding the system from these three perspectives, we then proceed to create a simple world to see exactly how to use Blender and the external tools.

# Main Ideas of a Blender Portal World Editor

Let’s now look at the main ideas of how we are going to use Blender in combination with some custom tools to fulfill the above requirements. The main ideas of our Blender portal world editing system are as follows.

+   Meshes as sectors. We represent a sector as a single polygonal mesh object in Blender. The geometry of the mesh defines the geometry of the sector. A sector cannot be split across two meshes. Similarly, a single mesh should not contain the geometry for more than one sector. For a convex cell portal engine the geometry in each cell should be convex; for an arbitrary cell portal engine, using an additional means of VSD, the geometry in each cell need not be convex. Checking for sector convexity is the responsibility of the person doing the world editing.

> NOTE A custom world editor could prevent the creation of any non-convex mesh. This again illustrates the fundamental difference between the choices of writing your own editor or adapting an existing editor. Adapting an existing editor allows you to leverage the existing editing framework, but also means that the creation of certain illegal features, such as non-convex sectors, is allowed within the editor and can only be detected later on.

![](bbox=[0.15, 0.78, 0.82, 0.94])

Figure 6-4. Each sector in a world is modeled as a separate mesh in Blender.