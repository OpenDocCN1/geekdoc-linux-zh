# USING REGIONS

Windows GDI+ enables you to create complex areas of space defined as a region. A region consists of any number of rectangles and paths that build a contained area of space. The Region class that VB .NET provides represents a region. Windows uses a region to determine the shape of a window. For more information on creating a shaped window, see the section “Create a Shaped Window.”

To create a region, declare a new instance of the Region class using Dim combined with the New operator. The class is part of the System.Drawing namespace. To create a simple rectangular region, pass the constructor a Rectangle object. To create a more complex region, you create a GraphicsPath object and pass it to the Region constructor. For more information on creating a GraphicsPath, see the section “Create a Path.”

The real power of regions comes from their ability to combine. Each of the two methods below expects a

GraphicsPath, Rectangle, or another Region. Union takes the object from the argument and adds the object’s space to the current region. Intersect takes the object from the argument and leaves only the part of the current region where both objects exist. Complement updates the current region to the portion of the specified object that does not intersect with the object. Exclude updates the current region to the portion of its interior that does not intersect with the specified object. Xor updates the current region with the union minus the intersection of itself with the object.

To draw a region, the Graphics object provides a FillRegion method. This method accepts a Brush as the first parameter and a Region as the second parameter. To use a Region you create as a Clip region in a Graphics object, and set the Graphics.Clip property equal to the Region.

# USING REGIONS

![](bbox=[0.06, 0.62, 0.42, 0.87])

![](bbox=[0.55, 0.62, 0.92, 0.87])

+   1 Open the Paint event where the primitive needs to draw.

+   2 Create a GraphicsPath object specifying a closed path.

Note: To create a GraphicsPath, see the section “Create a Path.”

+   3 Type Dim myRegion As New Region(path), replacing myRegion with the name for the Region and path with the name of the GraphicsPath.

+   4 To combine regions, declare and initialize a new GraphicsPath or Rectangle object.

+   5 Type myRegion.Xor(myRect), replacing myRegion with the name of the Region, Xor with one of the combination methods, and myRect with the name of the new object.