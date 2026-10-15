
# Extra

You can create different fill patterns for objects with complex shapes, such as curves, using the FillMode enumeration. You have two options for FillMode: Winding, and the default, Alternate. Alternate moves across the curve and alternates between filling and not filling as it hits lines of the curve. Winding uses the direction of the curve to determine whether to fill it. Generally, the default Alternate does an effective job, but you may try Winding when Alternate does not give the appropriate results.

You can use Bezier curves, a more advanced cubic curve, to specify more exact coordinates of curvature. Most professional drawing applications work with Bezier curves instead of the simpler cardinal spline curves used by DrawCurve. To draw a Bezier curve, you use the DrawBezier method, which only draws one curve defined by the four points. The method requires a Pen object, which you follow with four Point objects for its parameters. The first and last Point objects make up the curve's endpoints. The two middle Point objects make up the two control points that create the desired curvature. When the curve draws, it pulls the curve out to the control points.

```
Example:
e.Graphics.DrawBezier(Drawing.Pens.Red, _
    New Point(100, 100), New Point(150, 150), _
    New Point(150, 200), New Point(100, 250))
```

![](img/d6f772854306e15fb6df39b861a7b541_166_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_166_1.png)

7 To draw a curve, declare an array of Point objects that the curve passes through.

8 Type e.Graphics.DrawCurve(myPen, pts), replacing DrawCurve with either DrawCurve or DrawClosedCurve and myPen with the name of the Pen object and pts with the name of the Point array.

9 Press F5 to run your project.

The curve draws onto the graphics container.

# DRAW TEXT

Most applications use text to title, label, and explain functions on a form. In some cases, a Label control can provide the appearance necessary. For advanced text rendering, you can use the text drawing routines that VB .NET includes in the Graphics object. For more information on the Label control, see Chapter 3. Using the Graphics system, you can apply a Brush to your text to create text filled with a gradient, a bitmap texture, or a hatch pattern.

The standard method of rendering text with the Graphics object is the DrawString method. In each available overloaded method call, the first parameter contains the String to print. DrawString expects a Font object as the second parameter and a Brush object as the third parameter. For the fourth parameter, you pass a Point object specifying the top, left point to draw the text. The simplest constructor requires these four parameters. Optionally for the fifth parameter, you can pass a StringFormat object to designate how the text styles.

Chapter 4 contains more detailed information on the String variable type.

To provide the font to pass to DrawString, create a new instance of the System.Drawing.Font class. Depending on the data you want to provide to the Font constructor, you can pass either a FontFamily object, or a String to select a font family, such as Arial or Times New Roman. The second parameter is the size of the font in points. Optionally for the third parameter, specify the font style using the FontStyle enumeration.

The Graphics object exposes a method called MeasureString. Use this method to determine the width and height of a string you want to draw. Pass the String and Font as the two parameters to the method. MeasureString returns a SizeF structure, contained in the System.Drawing namespace. The Width and Height properties of the SizeF contain the appropriate values.

# DRAW TEXT

![](img/d6f772854306e15fb6df39b861a7b541_167_0.png)

- 1 Create a new Windows Application project or open an existing project and the form with which to work.
- 2 Open the Paint event where the primitive needs to draw.
- 3 Declare a Brush object to draw the text.
- 4 Type Dim myFont As New Drawing.Font(), replacing myFont with the name for the Font variable.
- 5 Inside the parentheses, type "Arial Black", 72, replacing Arial Black with the font face to use and 72 with the size of the font.

Note: To create a Brush, see the section "Create a Brush."
