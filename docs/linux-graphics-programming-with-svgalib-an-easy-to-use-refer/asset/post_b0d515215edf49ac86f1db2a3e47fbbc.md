
# Drawing Primitives

These functions are the drawing primitives—the building blocks of SVGAlib:

```c
int vga_clear(void)
```

Clears the screen and sets all visible pixels to 0 (which is usually black). This is automatically done by a `vga_setmode()` call. This function returns 0 (but that shouldn't be relied upon).

```c
void vga_setcolor(int color)
```

Sets the current color to the supplied color value. You may only use `vga_setcolor()` in 256 or fewer color modes. For the other modes, use `vga_setrgbcolor()` instead. The specified color is used by `vga_drawpixel()` and `vga_drawline()`. The `fun` and `vgatest` demos show the basic use of this function.

```c
void vga_setrgbcolor(int r, int g, int b)
```

Sets the current color to the RGB values `r`, `g`, and `b`, each in the range of 0 to 255. This operation does not make sense in 256 (or fewer) color modes. Instead, use `vga_setcolor()`. The color is used by `vga_drawpixel()` and `vga_drawline()`. The `fun` and `vgatest` demos show the basic use of this function.

```c
void vga_setegacolor(int color)
```

Sets the current color to be a color resembling the 16 EGA colors. This works regardless of the depth of the current video mode.

```c
int vga_drawpixel(int x, int y)
```

Draws a single pixel at screen coordinates `(x, y)`. The color drawn is set with `vga_setcolor()` or `vga_setrgbcolor()`. The function should always return 0, but it might be a good idea not to rely on this.

```c
int vga_drawline(int x1, int y1, int x2, int y2)
```

This draws a line from `(x1, y1)` to `(x2, y2)` on the screen. If you exchange the start and end of the line, you shouldn't expect to have exactly the same set of pixels covered by the line. This function is very inefficient because it's mainly comprised of a bunch of `vga_drawpixel()` calls. Instead, you should consider using direct screen access. Alternatively, you can use `vga_drawcassegment()` to handle more than one pixel. The color drawn is set with `vga_setcolor()` or `vga_setrgbcolor()`. The function should always return 0, but it might be a good idea not to rely on this.

```c
int vga_drawcassegment(int line, unsigned char *color)
```

This draws a horizontal line spanning the entire screen using “y” coordinate `line`. The colors drawn are taken from `color[0]` to `color[length -1]`. The color is a simpler front end to `vga_drawcassegment()`.

```c
int vga_getpixel(int x, int y)
```

Reads a pixel’s value from the screen. This function is very inefficient, so you should consider either using direct screen access or using `vga_getcassegment()` to handle more than one pixel.

```c
int vga_getcassegment(unsigned char *colors, int x, int y, int length)
```

The direct opposite of `vga_drawcassegment()`. The line of `length` pixels starting at `(x, y)` is not drawn; instead, the color values are taken from the screen and copied into `color[0]..color[length -1]`. The SVGAlib version was introduced in version 1.2.10. In high/true color modes, the `length` must be given in bytes, not pixels.

```c
void vga_waitretrace(void)
```

Waits for vertical retrace, which is when the video beam goes dark and returns from the bottom line to the top line. This can be used to synchronize animation with monitor refresh. However, because Linux is a multiplexer OS, some time may elapse before the function returns. Also, not all cards support this function in every mode.

# Basic (Nonraw) Keyboard I/O

These functions deal with basic keyboard I/O:

```c
int vga_getch(void)
```

Waits for a keypress just like `getch()` would. For a nonblocking check for a keypress, use `vga_getkey()`. Alternatively, if you want to wait for several events to occur at once, use `vga_waitevent()`.

```c
int vga_getkey(void)
```

Reads a character from the keyboard without waiting. Returns 0 if no key has been pressed, and returns the key’s ASCII value otherwise. This function must not be used in raw keyboard mode. In this situation, use `keyboard_getstate()` or `keyboard_keypressed()` instead.

```c
int vga_waitevent(int which, fd_set *input, fd_set *output, fd_set *except, struct timeval *timeout)
```

This is the only SVGAlib function that allows you to wait for keyboard and mouse events. It’s based on the `select()` library function, so for a deeper understanding of `vga_waitevent()`, have a look at `select()` as well.

able, or being ready for new write data, or being in an exceptional condition (urgent data arriving on a TCP stream), set the corresponding bits in the `fd_set` structures passed (see `select()`). On a W32 `vga_waitevent()` to return after a timeout value, it has a `struct timeval` with the desired value. If you're not interested in the corresponding events, you may pass `NULL` for any of the pointers.

If `NULL` is passed for timeout, `vga_waitevent()` will not time out but block until any of the other events occur. If the integer returned is a < 0, an error has occurred. Check the global variable `errno` for details. If a value >= 0 is returned, it is a bitmask constructed using `VGA_MOUSEEVENT` and `VGA_KEYEVENT` to show which of these events has occurred.

If any of these two occurred, the appropriate update functions are already called by `vga_waitevent()`. `vga_waitevent()` operates in raw as well as non-raw keyboard mode. In the latter case, use `vga_getch()` and not `vga_getkey()` to read the newly arrived keys.

Any of the file related conditions being met will be signalled by setting exactly the bits for files that met the conditions in the corresponding `fd_set` structures. If a non-`NULL` timeout is passed the remaining time is written into it on return. If it is 0 a timeout occurred (again: cf. `select()`). Therefore, depending on context, `vga_waitkey()` may return 0 if only special, non-SVGA/lib, events occurred.

# Direct VGA Memory Access

These functions are in regard to direct VGA memory access:

### `void vga_setpage(int page)`

Usually, SVGA cards have more than 64K of memory, which suffices for an ordinary VGA card. However, the memory window mapped at `vga_getgraphmem()` is only 64K large. `vga_setpage()` selects the page—that is, the 64K memory chunk—to be visible at position `vga_getgraphmem()`. The `fun()` and `vgatest()` demos show the basic use of this function.

### `void vga_setreadpage(int page)`

Usually, SVGA cards have more than 64K of memory, which suffices for an ordinary VGA card. However, the memory window mapped at `vga_getgraphmem()` is only 64K. Therefore, `vga_setreadpage()` selects the page—that is, the 64K memory chunk—to be visible for reads at position `vga_getgraphmem()`.

### `void vga_setwritepage(int page)`

Usually, SVGA cards have more than 64K of memory, which suffices for an ordinary VGA card. However, the memory window mapped at `vga_getgraphmem()` is only 64K large. `vga_setwritepage()` selects the page—that is, the 64K memory chunk—to be visible for writes at position `vga_getgraphmem()`.

```c
unsigned char *graph_mem; /* This declaration is already in vga.h */
```

```c
unsigned char *vga_getgraphmem(void)
```

Returns a pointer to the 64K VGA frame buffer window. `vga_setpage()`, `vga_setreadpage()`, and `vga_setwritepage()` allow you to select which page of the VGA memory shows up at this position. `vga_setlinearraddressing()` maps all VGA memory at a consecutive memory area (if your hardware supports it). In this mode, `vga_getgraphmem()` will return the location of this area, too. You can also access the global variable `graph_mem`, which will also contain this address. Most demos, especially `vgatest`, show the direct use of this function to access screen memory.

```c
void vga_copytoplanar256(unsigned char *virtual, int pitch, int voffset, int vpitch, int w, int h)
```

Copies part of a linear virtual screen in system memory at `*virtual` to Mode X-style video memory. Argument `pitch` is the logical width of the virtual screen (in pixels, which are one byte large), `voffset` is the address offset into video memory, `vpitch` is the logical scanline width of the screen, and `(w, h)` is the width and height of the area to copy in pixels (the width must be a multiple of four).

```c
void vga_copytoplanar16(unsigned char *virtual, int pitch, int voffset, int vpitch, int w, int h)
```

Similar to `vga_copytoplanar256()` but for 16 color modes (however, it's not well tested). Assumes pixels are stored in consecutive bytes, ranging from 0 to 15 in the virtual screen. Copies part of a linear virtual screen in system memory at `*virtual` to Mode X-style video memory. Argument `pitch` is the logical width of the virtual screen (in pixels, which are one byte large), `voffset` is the address offset into video memory, `vpitch` is the logical scanline width of the screen, and `(w, h)` is the width and height of the area to copy in pixels (the width must be a multiple of four).

```c
void vga_copytoplane(unsigned char *virtual, int pitch, int voffset, int vpitch, int w, int h, int plane)
```

Similar to `vga_copytoplane16()` but copies only a subset of the four 16-color mode planes (`plane` should be in the range 0 to 15). The bits set in `plane` select which of the four 16-color mode planes to modify. Assumes pixels are stored in consecutive bytes, ranging from 0 to 15 in the virtual screen. Copies part of a linear virtual screen in system memory at `*virtual` to VGA 16-mode video memory. Argument `pitch` is the logical width of the virtual
