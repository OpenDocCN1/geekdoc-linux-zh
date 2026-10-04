
## Chapter 9. The canvas Widget, Images, and Events

For instance, you could bind a double mouse click event to bringing up a message box that would describe an item. A plumber could then double click on a joint and see a description of the style of fitting to use, where to buy it, and an expected cost.

## 9.2 Creating a canvas

Creating a canvas is just as easy as creating other Tk widgets. You simply invoke the canvas command to create a canvas and then tell one of the layout managers where to display it.

As with the other Tk commands, a command will be created with the same name as the canvas widget. You will use this command to interact with the canvas, creating items, modifying the configuration, etc.

Syntax: canvasName ?options?

- canvas Create a canvas widget.
- canvasName The name for this canvas.

- ?options? Some of the options supported by the canvas widget are:
- -background color The color to use for the background of this image. The default color is light gray.
- -closeenough distance Defines how close a mouse cursor must be to a displayable item to be considered on that item. The default is 1.0 pixel. This value may be a fraction and must be positive.
- -scrollregion boundingBox Defines the size of a canvas widget. The bounding box is a list, left top right bottom, that defines the total area of this canvas, which may be larger than the displayed area.

These coordinates define the area of a canvas widget that can be scrolled into view when the canvas is attached to a scrollbar widget.

This defaults to 0 to 0 width height, the size of the displayed canvas widget.

- -height size The height of the displayed portion of the canvas. If -scrollregion is declared larger than this and scrollbars are attached to this canvas, this defines the height of the window into a larger canvas.

The size parameter may be in pixels, inches, millimeters, etc.

- -width size The width of this canvas widget. Again, this may define the size of a window into a larger canvas.

- -xscrollincrement size The amount to scroll when scrolling is requested. This can be used when the image you are displaying has a grid nature, and you always want to display an integral number of grid sections and not display half-grid sections.

- -yscrollincrement size The amount to scroll when scrolling is requested. This can be used when the image you are displaying has a grid nature, and you always want to display an integral number of grid sections and not display half-grid sections.

## 9.3 Creating Displayable Canvas Items

There are several widget subcommands associated with the procedure created when you create a canvas widget. The subcommand for drawing items on a canvas is the `create` subcommand. This subcommand creates a graphic item in a described location. Various options allow you to specify the color, tags, etc. for this item. The `create` subcommand returns the unique number that can be used to identify this drawable item.

The `create` subcommand includes a number of options that are specific to the class of item. Most drawable items support the following options (except when the option is not applicable to that class of drawable; for instance, line width is not applicable to a text item).

- -width width
The width of line to use to draw the outline of this item.

- -outline color
The color to draw the outline of this item. If this is an empty string, the outline will not be drawn. The default color is black.

- -fill color
The color with which to fill the item if the item encloses an area. If this is an empty string (the default), the item will not be filled.

- -stipple bitmap
The stipple pattern to use if the `-fill` option is being used.

- -tagList
A list of tags to associate with this item.

The items that can be created with the `create` subcommand are:

```
LINE canvasName create line x1 y1 x2 y2 ?xn options
```

Create a polyline item. The $x$ and $y$ parameters define the ends of the line segments. Options for the line item include:

- -arrow end
Specifies which end of a line should have an arrow drawn on it. The end argument may be one:
* first The first line coordinate.
* last The end coordinate.
* both Both ends.
* none No arrow (default)

- -fill color The color to draw this line.

- -smooth boolean
If set to true, this will cause the described line segments to be rendered with a set of Bezier splines.

- -splinesteps number
The number of line segments to use for the Bezier splines if -smooth is defined true.

```
ARC canvasName create arc x1 y1 x2 y2 options
```

Create an arc. The parameters x1 y1 x2 y2 describe a rectangle that would enclose the oval of which this arc is a part. Options to define the arc include:

- -start angle The start location in degrees for this arc. The angle parameter is given in degrees. The 0-degree position is at 3:00 (the rightmost edge of the oval) and increases in the counterclockwise direction. The default is 0.

- -extent angle The number of degrees counterclockwise to extend the arc from the start position. The default is 90 degrees.

- -style style
The style of arc to draw. This defines the area that will be filled by the -fill option. May be one of:
- - pieslice The ends of the arc are connected to the center of the oval by two line segments (default).
- - chord The ends of the arc are connected to each other by a line segment.
- arc Draw only the arc itself. Ignore -fill options.

- -fill color The color to fill the arc, if -style is not arc.

```
canvasName create rectangle x1 y1 x2 y2 options
```

Create a rectangle. The parameters x1 y1 define opposite corners of the rectangle.

```
canvasName create oval x1 y1 x2 y2 options
```

Create an oval. The parameters x1 y1 x2 y2 define opposite corners of the rectangle that would enclose this oval.

```
canvasName create polygon x1 y1 x2 y2 ... xn yn options
```

Create a polygon. The x and y parameters define the vertices of the polygon. A final line segment connecting xn, yn to x1, y1 will be added automatically.

The polygon item uses the same -smooth and -splinessteps options as the line item.

```
canvasName create text x y options
```

Create a text item.

The text item has these unique options:

- -anchor position
Describes where the text will be positioned relative to the x and y.

The position argument may be one:
* center—Center the text on the position (default).
* nse ne sw—one or more sides of the text to place on the position. If a single side is specified, that side will be centered on the y location. If two adjacent sides are specified, then that corner will be placed on the x/y location. For example, if position is defined as w, the text will be drawn with the center of the left edge on the specified x/y location. If position is defined as se, the bottom rightmost corner of the text will be on the x/y location.

- -justify style
If the text item is multiline (has embedded newline characters), this option describes whether the lines should be right justified, left justified, or center justified. The default is left.

- -text text
The text to display.

- -font fontDescriptor
The font to use for this text.

- -fill color
The color to use for this text item.

```
BITMAP canvasName create bitmap y options
```

Create a two-color bitmap image. Options for this item include:

-anchor position
This option behaves as described for the text item.

- -bitmap name
Defines the bitmap to display. May be one of:
@file.xbm The name of a file with bitmap data.
bitmapName The name of one of the predefined bitmaps.

The Tcl 8.0 distribution includes these bitmaps for the PC, Mac, and Unix platforms:

| info | question | hourglass | warning |
| --- | --- | --- | --- |
| i | ? | ![ | ! |
| error | gray12 | gray25 | gray50 | gray75 |

The Mac platform supports these additional bitmaps:

accessory A desk accessory
application A generic application
