
## CREATE A PEN

You use a Pen to tell VB .NET the style, color, and thickness of a line to draw for the various primitives. For example, a variety of outlined primitives use a Pen, like rectangles, ellipses, and curves. A Pen specifies details for VB .NET to know how to draw these shapes. Use a Brush to fill a primitive object or the inside of a Pen. For more information on the Brush object, see the section "Create a Brush."

To produce a single color pen, create a new instance of the Pen class using the Dim command and the New operator. VB .NET stores the Pen class in the System.Drawing namespace. For more information on instantiating classes, see Chapter 7. For the most basic constructor of the Pen, pass a color as the single parameter. The second constructor expects a color for the first parameter and the line width as the second parameter. See the section "Using the Graphics Object" for more information on specifying a color.

To create a Pen object based on a Brush, create a new instance of the Pen class and provide the Brush as the first argument. To specify the width of the pen, use the alternate constructor that expects a Brush and a line width passed in as a Single.

After you create a Pen instance, a number of properties allow editing the appearance. The StartCap and EndCap properties expect a constant from the LineCap enumeration. The properties specify the type of end caps to put on a pen. A primitive without ends, for example, a rectangle or ellipse, ignores the values. Instead, the LineJoin property specifies how to connect corners of lines and expects a value from the LineJoin enumeration. To create different styles of dashed lines, set the DashStyle. The DashCap property specifies a DashCap enumerated value that represents the style to use for dashes.

## CREATE A PEN

![](img/d6f772854306e15fb6df39b861a7b541_159_0.png)

- 1. Create a new project or open an existing one.
- 2. Click the class list and select (Base Class Event) or the control on which to draw.
- 3. Click the method name list and select the Paint Event.
- 4. Type Dim redPen As New Drawing.Pen(Color.Red), replacing redPen with the variable name and Color.Red with the type of the color to use.
- 5. The example uses the Color class to provide a supplied color Red.

## Extra

You can use the LineCap, DashCap, and LineJoin constants to specify how a pen draws.

## DRAWING.DRAWING2D.LINECAP ENUMERATION

| MEMBER | DESCRIPTION |
|---|---|
| AncorMask | A mask used to check a line cap |
| ArrowAnchor | Arrow-shaped anchor cap |
| Custom | A custom line cap |
| DiamondAnchor | Diamond anchor cap |
| Flat | Flat line cap |
| NoAnchor | No anchor |
| Round | Round line cap |
| RoundAnchor | Round anchor cap |
| Square | Square line cap |
| SquareAnchor | Square anchor line cap |
| Triangle | Triangular line cap |

## DRAWING.DRAWING2D.DASHCAP ENUMERATION

| MEMBER | DESCRIPTION |
|---|---|
| Flat | Squares off ends of each dash |
| Round | Rounds off ends of each dash |
| Triangle | Points ends of each dash |

## DRAWING.DRAWING2D.LINEJOIN ENUMERATION

| MEMBER | DESCRIPTION |
|---|---|
| Bevel | Beveled join |
| Miter | Angled miter join |
| MiterClipped | Clipped miter join |
| Round | Smooth, rounded join |

![](img/d6f772854306e15fb6df39b861a7b541_160_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_160_1.png)

5 Type e.Graphics.DrawLine (redPen, 5, 5, 200, 200) replacing DrawLine with the Graphics method to use the pen, redPen with the variable name of the Pen object, and 5, 5, 200, 200 with the appropriate parameters.

Note: See the section "Draw Simple Primitives" to draw a primitive.

6 Press F5 to run your project.

The graphics method runs and draws using the selected color.

## VISUAL BASIC .NET

## DRAW BITMAPS AND IMAGES

You can add images to a form in conjunction with drawing commands. The PictureBox control provides a simple way to load an image onto the form, but you cannot draw around the PictureBox, unless you contain all of the drawing inside. You can use commands from the System.Drawing namespace to draw images onto the form without using a control.

Two classes provide the ability to work with bitmaped images. You more commonly use the Bitmap class to load a raster image from a file, create an instance of a Bitmap class and pass the filename as the parameter to the Bitmap constructor. The class stores the pixel data and properties of the image.

Only a few of the many method calls available for DrawImage appear in the introduction. See Visual Basic .NET help for a complete list. The simplest constructor expects an Image and a Point, which specifies the

position for the top, left corner of the image. By providing an array of three Point classes that form a parallelogram, DrawImage skews the image to fit the shape. By passing a Rectangle as the second parameter, DrawImage scales the image to fit the dimensions of the rectangle starting from the top, left corner of the rectangle.

You can use TextureBrush to paint an image onto a shape. This allows you to create an image that has shaped edges, and lets you place the image inside an ellipse or more advanced shapes. The first parameter of the available constructors accepts an Image or Bitmap class. For the simplest constructor, you only need this parameter. Another constructor of the TextureBrush class expects a Rectangle as the second parameter that specifies the section of the image to use as the brush. The width and height of the rectangle determine the size of the brush.

## DRAW BITMAPS AND IMAGES

![](img/d6f772854306e15fb6df39b861a7b541_161_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_161_1.png)

- 1 Create a new Windows Application or open an existing one.
- 2 Open the method or event where the image needs to draw.
- 3 Type Dim myPic As New Drawing.Bitmap("C:\WINNT\Coffee Bean.bmp"), replacing myPic with the name for the image variable and "C:\WINNT\Coffee Bean.bmp" with the path to a supported raster image file.
- 4 On a new line, type e.Graphics.DrawImage(myPic), replacing e.Graphics with the name of the Graphics object and myPic with the variable name of the Bitmap object.
