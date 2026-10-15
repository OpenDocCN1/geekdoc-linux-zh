
## Extra

You can use the FontStyle enumeration to provide options for the style of font to draw. For example, you can print in bold italics font. To do this, you can combine the constants with the Or operator.

| MEMBER | DESCRIPTION |
|---|---|
| Bold | Bold text |
| Italic | Italic text |
| Regular | Normal text |
| Strikeout | Text with a line through the middle |
| Underline | Underlined text |

### Example:

```
Dim arial As New Font("Arial", 16, _
FontStyle.Bold Or FontStyle.Italic)
Dim red As Brush = Brushes.Red
e.Graphics.DrawString(
"Bold Italic Arial Font", arial, _
red, 10, 10)
```

![](img/d6f772854306e15fb6df39b861a7b541_168_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_168_1.png)

6 On a new line, type e.Graphics.DrawString("Big text", myFont, myBrush, 20, 50), replacing Big text with the string to print or a string variable, myFont with the name of the Font variable, myBrush with the name of the Brush variable, and 20, 50 with the coordinates to draw the text.

7 Press F5 to run your project.

The text renders onto the appropriate graphics container:

## CREATE A PATH

Because simple primitives may not provide the desired appearance for your application, you can combine multiple primitives into a single object with a single fill. You use the GraphicsPath object to create a complex object from a number of primitives. The GraphicsPath can also represent multiple figures, completely separate in space. A figure consists of an open or closed shape.

To create a GraphicsPath, declare a new instance of a GraphicsPath class with no entries passed to the constructor as parameters. The class is part of the System.Drawing.Drawing2D namespace. However, you may find creating the path through the constructor difficult. For more information on declaring new instances of classes and using constructors, see Chapter 7.

To begin building an individual figure, call the StartFigure method with no parameters. The AddLine method adds a line to the figure. AddCurve adds a curve to the figure. You can replicate all of the Draw methods throughout this chapter, such as DrawEllipse and DrawPie, with the prefix Add instead of Draw. The methods accept all the same parameters with the exception of the Pen parameter, which you leave out completely. To create a functioning path, the last point of a previous primitive and the first point of the following primitive must match. For more information on primitive drawing methods, see the section "Draw a Primitive."

If you want to close the figure before starting a new one, call the CloseFigure method. Call StartFigure again to start a new figure without closing the current one. Use the CloseAllFigures method with no parameters to close any open figures previously created.

To draw the path onscreen, call DrawPath with a Pen as the first argument and the GraphicsPath as the second argument. You can fill the interior areas of a path using FillPath. Pass a Brush as the first parameter and the GraphicsPath as the second.

![](img/d6f772854306e15fb6df39b861a7b541_169_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_169_1.png)

- 1. Create a new Windows Application project or open an existing project.
- 2. Open the Paint event where the primitive needs to draw.
- 3. Type Dim myPath As New Drawing.Drawing2D.GraphicsPath(), replacing myPath with the variable name for the path.
- 4. Type myPath.StartFigure(), replacing myPath with the path's variable name.
- 5. Type myPath.AddLine(10, 10, 300, 15), replacing myPath with the variable name and AddLine(10, 10, 300, 15) with a primitive adding method.
- 6. Repeat step 5 until the figure is complete.
- 7. Repeat steps 4 to 6 to create the necessary figures.
- You can type myPath.CloseFigure() replacing myPath with the path variable to create a closed figure.

## Extra

You can use the Warp method of the GraphicsPath object to warp objects. Pass a rectangle specifying the bounds of the path and an array of points making up a parallelogram into which you warp the rectangle. If you specify three points, the parallelogram adds the points and makes the lower-right point automatically. The command then warps all of the points in the path to fit the shape.

### Example:

```
Dim myPath As New Drawing2D.GraphicsPath()
Dim srcRect As New RectangleF(0, 0, 100, 200)
myPath.AddRectangle(srcRect)

e.Graphics.DrawPath(Pens.Black, myPath)

Dim point1 = New PointF(200, 200)
Dim point2 = New PointF(400, 250)
Dim point3 = New PointF(220, 400)
Dim destPoints() As PointF = {point1, point2, point3}

myPath.Warp(destPoints, srcRect)

e.Graphics.DrawPath(Drawing.Pens.Red, myPath)
```

![](img/d6f772854306e15fb6df39b861a7b541_170_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_170_1.png)

8 Declare a Pen to draw the path.

9 Type e.Graphics.DrawPath(redPen, myPath), replacing e.Graphics with the name of the Graphics object, redPen with the name of the Pen, and myPath with the name of the GraphicsPath.

The GraphicsPath draws onto the drawing region.

10 Press F5 to run the project.
