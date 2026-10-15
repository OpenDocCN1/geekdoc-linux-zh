# CREATE A BRUSH

You use a Brush class to tell VB.NET how to fill an area. Each of the filled primitives, such as filled rectangles, requires you use a Brush to specify how to fill the area. To produce a Brush for use in VB.NET, create an instance of type Brush using the New operator. VB provides a number of Brush classes depending on the style you need. Each brush has a particular size. If the shape to fill is larger than the brush, the brush tiles to fill the entire space.

The System.Drawing namespace holds both the SolidBrush and TextureBrush classes. The SolidBrush paints an area in a single color. Pass the color for the brush as the only parameter. Because these brushes are a solid color, the brush is only 1 x 1 in size.

The System.Drawing.Drawing2D namespace contains a number of more complex brushes. The HatchBrush

creates a brush based on a pattern. Windows provides a collection of 2-bit hatch patterns. VB.NET provides constants for each of these patterns in the HatchStyle enumeration, ranging from BackwardDiagonal to ZigZag. To create the brush, declare an instance of the HatchBrush class and pass the constructor the pattern to use, followed by the foreground color as the second parameter, and the background color as the third parameter.

LinearGradientBrush fills in a steady range from one color to another, at any angle. For the constructor, pass an instance of a Rectangle class filled with the size of the gradient brush to create. The next parameter specifies the start color and the third parameter specifies the end color. See the section "Understanding the Graphics Object" to specify a color. The last parameter is the angle in degrees of the gradient. An angle of zero creates a horizontal gradient, and an angle of 90 creates a vertical gradient.

# CREATE A SOLID BRUSH

+   1. Create a new project or open an existing one.
+   2. Click the class list and select (Base Class Event) or the control on which to draw.

+   3. Click the method name list and select the Paint event.
+   4. Type Dim redBrush As New Drawing.SolidBrush(Color.Red), replacing redBrush with the name for the brush and Color.Red with the color.

# CREATE A HATCH BRUSH

+   5. Type Dim confettiBrush As New Drawing2D.HatchBrush(), replacing confettiBrush with the name for the brush.

+   6. Inside the parentheses, type the hatch pattern to use followed by the foreground and background colors, all separated by commas.

![](bbox=[0.04, 0.48, 0.48, 0.77])

![](bbox=[0.52, 0.48, 0.96, 0.77])