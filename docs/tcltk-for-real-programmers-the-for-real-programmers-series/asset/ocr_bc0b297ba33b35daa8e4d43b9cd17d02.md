# 9.4 Canvas Widget Subcommands

Syntax: font families ?-displayof windowName?
font families

Returns a list of valid font families for this system.

-displayof If this option is present, it defines the window (frame, canvas, topwindow) to return this data. By default, this is the primary graphics window ".

The font measure command is useful when you are trying to arrange text on a display in an aesthetic manner.

Syntax: font measure font ?-display windowName? text
font measure

The font measure command returns the number of horizontal pixels that the string text will require if rendered in the defined font.

font The name of the font, as described above.

-displayof If this option is present, it defines the window (frame, canvas, topwindow) to return this data. By default, this is the primary graphics window ".

text The text to measure.

If Tk can't get an exact match to the requested font on your system, it will find the best match. You can determine what font is actually being used with the font actual command.

Syntax: font actual font ?-display windowName?
font actual

Return the actual font that will be used when font is requested.

font The name of the requested font.

-displayof If this option is present, it defines the window (frame, canvas, topwindow, etc.) to return this data. By default, this is the primary graphics window ".