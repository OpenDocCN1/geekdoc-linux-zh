# Drawing Primitives

These functions are the drawing primitives—the building blocks of SVGAlib:

```
int vga_clear(void)
```

Clears the screen and sets all visible pixels to 0 (which is usually black). This is automatically done by a vga_setmode() call. This function returns 0 (but that shouldn't be relied upon).

```
void vga_setcolor(int color)
```

Sets the current color to the supplied color value. You may only use vga_setcolor() in 256 or fewer) color modes. For the other modes, use vga_setrgbcolor() instead. The specified color is used by vga_drawpixel() and vga_drawline(). The fun and vgatest demos show the basic use of this function.

```
void vga_setrgbcolor(int r, int g, int b)
```

Sets the current color to the RGB values r, g, and b, each in the range of 0 to 255. This operation does not make sense in 256 (or fewer) color modes. Instead, use vga_setcolor(). The color is used by vga_drawpixel() and vga_drawline(). The fun and vgatest demos show the basic use of this function.

```
void vga_setegacolor(int color)
```

Sets the current color to be a color resembling the 16 EGA colors. This works regardless of the depth of the current video mode.

```
int vga_drawpixel(int x, int y)
```

Draws a single pixel at screen coordinates (x, y). The color drawn is set with vga_setcolor() or vga_setrgbcolor(). The function should always return 0, but it might be a good idea not to rely on this.

```
int vga_drawline(int x1, int y1, int x2, int y2)
```

This draws a line from (x1, y1) to (x2, y2) on the screen. If you exchange the start and end of the line, you shouldn't expect to have exactly the same set of pixels covered by the line. This function is very inefficient because it's mainly comprised of a bunch of vga_drawpixel() calls. Instead, you should consider using direct screen access. Alternatively, you can use vga_drawscansegment() to handle more than one pixel. The color drawn is set with vga_setcolor() or vga_setrgbcolor(). The function should always return 0, but it might be a good idea not to rely on this.