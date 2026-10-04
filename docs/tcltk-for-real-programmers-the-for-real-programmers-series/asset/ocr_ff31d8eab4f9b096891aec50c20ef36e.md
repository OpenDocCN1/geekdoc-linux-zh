# 9.3 Creating Displayable Canvas Items

+   - both Both ends.
- none No arrow (default)

-fill color The color to draw this line.

-smooth boolean
If set to true, this will cause the described line segments to be rendered with a set of Bezier splines.

-splinesteps number
The number of line segments to use for the Bezier splines
if-smooth is defined true.

ARC canvasName create arc x1 y1 x2 y2 options
Create an arc. The parameters x1 y1 x2 y2 describe a rectangle that would enclose the oval of which this arc is a part. Options to define the arc include:

+   -start angle The start location in degrees for this arc. The angle parameter is given in degrees. The 0-degree position is at 3:00 (the rightmost edge of the oval) and increases in the counterclockwise direction. The default is 0.

+   -extent angle The number of degrees counterclockwise to extend the arc from the start position. The default is 90 degrees.

+   -style style
The style of arc to draw. This defines the area that will be filled by the -fill option. May be one of:

+   - pieslice The ends of the arc are connected to the center of the oval by two line segments (default).
- chord The ends of the arc are connected to each other by a line segment.
- arc Draw only the arc itself. Ignore -fill options.

-fill color The color to fill the arc, if -style is not arc.