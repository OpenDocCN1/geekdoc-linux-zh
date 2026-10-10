
## **void gl_getcontext(GraphicsContext *gc)**

Here is the void gl_getcontext(GraphicsContext *gc) code:

```c
extern GraphicsContext currentcontext
```

Saves the current context in the structure variable gc. You can also get the current context from the global variable currentcontext. However, you access single elements in this structure with the macros given in vgagl. Don't copy currentcontext into another structure because the size of the structure might change, and your program doesn't know when it will be linked dynamically to future SVGAlib versions. Instead, use gl_allocatecontext() to allocate such a structure, fill it with gl_getcontext(), and release it with free() after usage.

## **void gl_setcontext(GraphicsContext *gc)**

Restores a previously saved context (makes it the current context).

## **int gl_setcontextvga(int mode)**

Sets the graphics context to the physical screen of a VGA mode, as defined in vga_setmode(). The mode must be set with vga_setmode() prior to using any of the drawing functions; vgagl doesn't take care of that. The function returns 0 for success and nonzero if the given mode is not supported by the hardware.

## **int gl_setcontextvgavirtual(int mode)**

Allocates a virtual screen in system memory identical to the graphics mode, as defined in vga_setmode(), and makes that the current graphics context. The function returns 0 for success and nonzero if the given mode is not supported by the hardware.

## **void gl_setcontextvirtual(int w, int h, int bpp, int bitpsp, void *vbuf)**

Defines the current graphics context to have a width of w pixels, a height of h pixels, bpp bytes per pixel, bitpsp significant color bits per pixel (8, 15, 16 or 24), with the frame buffer at vbuf. A 4-bytes-per-pixel context, with 24 significant color bits, is also valid.

## **GraphicsContext *gl_allocatecontext(void)**

Allocates a graphics context. This is preferable to hard-coding a context variable in a program because doing so may make your code incompatible with any possible future versions of vgagl that might have additional context fields.

## **void gl_freecontext(GraphicsContext *gc)**

Frees the space allocated for the virtual screen in the given context gc. This should be a virtual context.

## **void gl_setcontextwidth(int w)**

See gl_setcontextheight().

## **void gl_setcontextheight(int h)**

Sets the size of the current virtual context, effectively clipping everything to the top-left corner of size (w, h).

# Drawing Primitives

These functions are the drawing primitives—the building blocks of vglag.

## **void gl_clearscreen(int c)**

Fills the entire screen with color c.

## **int gl_rgbcolor(int r, int g, int b)**

Returns a pixel value used in the current context that corresponds with the given color components. Used by setpixrgb().

## **void gl_setpixel(int x, int y, int c)**

See gl_setpixrgb().

## **void gl_setpixrgb(int x, int y, int r, int g, int b)**

gl_setpixel draws a single pixel at position (x, y) in color c. The lower 8, 15, 16, or 24 bits of the color are significant, depending on the number of colors the current mode supports.

gl_setpixrgb draws a single pixel at position (x, y) with color components r, g, and b, ranging from 0 to 255. If it’s in 256-color mode, this function is only meaningful if the RGB palette is set (gl_setrgbpalette()).

## **int gl_getpixel(int x, int y)**

Returns the color of the pixel at position (x, y) in the format used in the screen memory. The color -1 is returned for points outside the clipping window.

## **void gl_getpixrgb(int x, int y, int *r, int *g, int *b)**

Stores color components from the pixel at (x, y), ranging from 0 to 255, into integers pointed to by r, g, and b.

## **void gl_hline(int x1, int y, int x2, int c)**

Draws a horizontal line from point (x1, y) to point (x2, y) in color c.

## **void gl_line(int x1, int y1, int x2, int y2, int c)**

Draws a line from point (x1, y1) to point (x2, y2), inclusively, in color c. You should not assume that the same drawing trajectory is used when you exchange start and end points.

## **void gl_circle(int x, int y, int r, int c)**

Draws a circle of radius r in color c, centered at (x, y).

## **void gl_fillbox(int x, int y, int w, int h, int c)**

Fills a rectangular area with single color c. Its upper-left corner is at position (x, y), and its dimensions are (w, h).

# Copying of Screen Buffers and Page Flipping

The following functions are in regard to frame buffers and page flipping.

## **void gl_copyscreen(GraphicsContext *gc)**

Copies the current graphics context's contents (screen data) to the specified graphics context (the physical screen, for example). Contexts are assumed to be identical in size.

## **void gl_setscreenoffset(int o)**

Sets the offset (in pixels) into video memory for gl_copyscreen(), gl_copyboxtocontext(), and gl_copyboxfromcontext(), thereby allowing page flipping. Must be a multiple of the scanline width in bytes. It's reset to zero after the completion of gl_copyscreen().

## **void gl_setdisplaystart(int x, int y)**

Sets the physical display start address to the pixel at (x, y). This function can be used for hardware scrolling or for page flipping (for example, setdisplaystart(0, HEIGHT) displays from the second page). Make sure the scanline width (BYTEWIDTH) of the current context corresponds with the physical screen. Note also that the display start cannot be set to completely arbitrary points. See vga_setdisplaystart.

## **int gl_enablepageflipping(GraphicsContext *gc)**

Enables page flipping or triple buffering in gl_copyscreen() if the physical context gc can do it. Returns 3 if triple buffering will be used, 2 for page flipping, and 0 if page flipping is not possible (due to video memory/mode limitations).

When page flipping is enabled, gl_screenoffset() is ignored in gl_copyscreen(). The idea is that you draw your picture in gc and copy it to the screen via consecutive gl_copyscreen() calls. Each of these will choose a free buffer in the screen and adjust the display start accordingly. The current context must by the physical screen when gl_copyscreen() is called in this situation.

# Clipping

The next three functions pertain to clipping.

## **void gl_disableclipping(void)**

Disables clipping. This is the default.

## **void gl_enableclipping(void)**

Enables automatic clipping in most functions. One exception is gl_copybox().

## **void gl_setclippingwindow(int x1, int y1, int x2, int y2)**

Sets the clipping window to a rectangle with its top-left corner at (x1, y1) and its bottom-right corner at (x2, y2).

# Text-Drawing Primitives

These functions involve the use of bitmapped fonts.

## **void gl_setfont(int fw, int fh, void *fp)**

Uses the font stored as character bitmaps at fp, with characters of size (fw, fh), as the basic font for write operations. Note that the font included in the library must be expanded first, because it’s stored bit per pixel; this is not required if the gl_setwritemode() flag FONT_COMPRESSED is set.

## **void gl_setfontcolors(int bg, int fg)**

Sets the background and foreground colors for the compressed font write mode. This, in turn, is set with gl_setwritemode().

## **void gl_expandfont(int fw, int fh, int c, void *sfp, void *dfp)**

Converts a bit-per-pixel font at sfp with 256 characters of size (fw, fh) to an expanded font of character bitmaps stored at dfp (the size will be 256 * fw * fh * BYTESPERPIXEL). All nonzero pixels are set to color c. It’s possible to use nonexpanded fonts (but it’s slower) when the FONT_COMPRESSED gl_setwritemode() flag is set.

## **void gl_colorfont(int fw, int fh, int c, void *fp)**

Sets all nonzero pixels in the expanded font fp with 256 characters of size fw and fh, each to color c.

## **void gl_setwritemode(int m)**

Sets the writemode flags for the font routines. Argument m must be exactly one choice out of the following two groups of constants (giving you four choices, actually):

- WRITEMODE_MASKED
- WRITEMODE_OVERWRITE (default)
- FONT_COMPRESSED
- FONT_EXPANDED (default)

If WRITEMODE_MASKED is set, only foreground pixels of the font are used for write operations; the screen background is not erased.

> **Note**
> If FONT_COMPRESSED is set, text writes will use the compressed bit-per-pixel font rather than the expanded font (which would be slightly faster).
