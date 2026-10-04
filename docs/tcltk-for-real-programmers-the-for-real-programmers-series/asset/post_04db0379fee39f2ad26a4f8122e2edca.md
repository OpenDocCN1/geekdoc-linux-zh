
## Chapter 9. The canvas Widget, Images, and Events

### 9.4.5 Fonts and Text items

Fonts can be just as complex a problem as some 6000 years of endeavor with written language can make them. They can also be quite simple. I'm just going to discuss the platform-independent, simple method of dealing with fonts. Other methods are described in the online documentation under font.

The pre-8.0 releases of Tk name fonts use the X Window System naming convention of:

```
-foundry-family-weight-slant-setwidth-addstyle-pixel-point-resx-resy-spacing-width-charset-encoding.
```

If you need to work with a version of Tk earlier than 8.0, you are probably on a Unix system and can determine a proper name of an available font with the XII command xfont -x xfonts.

With the 8.0 release of Tcl and Tk, life became much simpler: a font is named with a list of attributes: family ?size? ?style? 

If the Tcl interpreter can't find a font that will match the font requested, it will find the closest match. It is guaranteed that a font will be found for any syntactically correct set of attributes.

- family: The family name for a font. On all systems, helvetica, and courier are defined. A list of the defined fonts can be obtained with the font families command.
- size: The size for this font. If this is a positive value, it is the size in points (1/72 of an inch). The scaling for the monitor is defined when Tk is initialized. If this is a negative number, it will be converted to positive and will define the size of the font in pixels. Defining a font by point size is preferred and should cause applications to look the same on different systems.
- style: The style for this font. May be one or more of normal (or roman), bold, italic, underline or overstrike.

Information about fonts can be obtained with the font command. As usual, I'll discuss only some of the more commonly used subcommands.

### 9.4 Canvas Widget Subcommands

Syntax: `font families ?-displayof windowName?`
`font families`

Returns a list of valid font families for this system.

- -displayof: If this option is present, it defines the window (frame, canvas, topwindow) to return this data. By default, this is the primary graphics window ".".

The font measure command is useful when you are trying to arrange text on a display in an aesthetic manner.

Syntax: `font measure font ?-display windowName? text`
`font measure`

The font measure command returns the number of horizontal pixels that the string text will require if rendered in the defined font.

- font: The name of the font, as described above.
- -displayof: If this option is present, it defines the window (frame, canvas, topwindow) to return this data. By default, this is the primary graphics window ".".
- text: The text to measure.

If Tk can't get an exact match to the requested font on your system, it will find the best match. You can determine what font is actually being used with the font actual command.

Syntax: `font actual font ?-display windowName?`
`font actual`

Return the actual font that will be used when font is requested.

- font: The name of the requested font.
- -displayof: If this option is present, it defines the window (frame, canvas, topwindow, etc.) to return this data. By default, this is the primary graphics window ".".

### Chapter 9. The canvas Widget, Images, and Events

With Tk 8.1, Tcl and Tk begin to support the Unicode character fonts. These are encoded by preceding the four-digit Unicode value with "\u". You can get information on the Unicode character sets at http://Unicode.org.

Unicode provides a standard method for handling letters other than US ASCII alphabet. The Unicode alphabet uses 16 bits to describe 65,536 letters. Each alphabet is assigned a range of numbers to represent its characters. With Unicode, you can represent Japanese katakana, Korean hangul, or any other major alphabet.

The following example steps through the fonts available on a generic Unix system and displays some sample text in ASCII and Unicode. Note that if the Unicode fonts are not supported in a given font, the Unicode numbers are displayed instead. This example was run using Tcl/Tk version 8.1a2. Unicode support is just being added in this revision. By the time you read this book, more Unicode support will be available.

#### Example 9.4.5-1

Example Script

```tcl
canvas .c -height 950 -width 800
p .c ypos 15
pset families [font families]
foreach family $families {
  c create 4 $ypos -font [list times 18 bold] \
  -text "$family" -anchor nw
  c create 240 $ypos -font [list $family 18] \
  -text "text line -- UNICODE: \u30Ab \u042f \u3072" \
  -anchor nw
  c create 4 [expr $ypos+25] -font [list roman 14] \
  -text "[font actual [list family 18]]" -anchor nw
  c create line 4 [expr $ypos+45] 800 [expr $ypos+45]
 incr ypos 50
}
```

### 9.4 More Canvas Widget Subcommands

#### Script Results

| fixed | test |
| :--- | :--- |
| -size 15 | helvetica |
| -size 16 | mincho |
| -size 15 | courier |
| -size 16 | lyricypewriter |
| -size 15 | lyricright |
| -size 16 | lucida |
| -size 15 | utopia |
| -size 16 | fixed |
| -size 15 | nil |
| -size 16 | clean |
| -size 15 | terminal |
| -size 16 | symbol |
| -size 15 | gothic |
| -size 16 | new century school |

### 9.4.6 Using a Canvas Larger than the View

When you create a canvas with the canvas command, you can provide -width xsize and -height ysize arguments define the size of the canvas to display.

If you don't also use a -scrollregion argument, then the canvas will be xsize by ysize.

The -scrollregion command will let you declare that the actual canvas is larger than its visible portion.

For example,

```tcl
canvas .c -width 200 -height 150 -scrollregion {0 0 4500 2000}
```

creates a window 150 pixels high and 200 pixels wide into a canvas that is actually 4500×2000 pixels.

If you attach scrollbars to this canvas, you can scroll this 200x150 pixel window around the larger space.

The -xscrollincrement and -yscrollincrement arguments will let you set how much of the canvas should scroll at a time. For instance, if you are displaying a lot of text in a canvas, you would want to set the -scrollincrement to the height of a line. This will cause the canvas to display full lines of text, instead of displaying partial lines at the top and bottom of the canvas as you scroll through the text.

The next example shows a checkerboard pattern with each square labeled to show its position in the grid. Because the -xscrollincrement is set to the size of a square, the full width of each square is displayed. Because the -yscrollincrement is half the size of a square, half the height of a square can be displayed.

Notice that the -scrollregion can include negative coordinates as well as positive, but you won't be able to scroll to it unless you've set the -scrollregion to include the area you've drawn to.

For example, if you've got a complex image to create and you don't know what the size will be until it's drawn, you can draw the image to a canvas and then determine the bounding box for the image with the command

```tcl
set coords[canvasName bbox all]
```
.