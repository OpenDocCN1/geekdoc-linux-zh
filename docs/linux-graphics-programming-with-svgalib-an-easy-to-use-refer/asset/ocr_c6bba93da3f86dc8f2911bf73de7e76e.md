+   ◆ joystick_getb4() for joystick_getbutton(0, 3)
+   ◆ joystick_getx() for joystick_getaxis(0, 0)
+   ◆ joystick_gety() for joystick_getaxis(0, 1)
+   ◆ joystick_getz() for joystick_getaxis(0, 2)

# int vga_accel(unsigned operation, ...)

This section deals with vga_accel()’s many features.

> Note
> This is the major function of the new accelerator interface that was sketched in version 1.2.3 but was then implemented in later versions. The main goal is to define functions that can be used as part of certain kinds of interesting graphical operations (not necessarily interesting primitives on their own). Obviously useful primitives in their own right are FillBox, ScreenCopy, DrawHlineList (solid polygon), and DrawLine.

Another interesting purpose is the fast drawing of color bitmaps, both straight and transparent (masked; certain colors are not written). For masked bitmaps (sprites), there are a number of possible methods, the availability of which depends on the chips. Caching in nonvideo video memory is often useful. One way is to use a transparency color compare feature of a BITBLT chip, either transferring the image from system memory or cached in video memory. If transparency compare is not available, it may be possible to first clear (zero) the mask in the destination area and then use a BITBLT raster operation to OR the image into the destination (this requires the mask color to be 0). A higher-level (library) interface should control this kind of operation.

Vga.h contains several macros that may be used for this operation. Most of the macros accept several optional arguments that may be specified. The SVGAlib demo, accel(), shows the basic usage of this function. The function returns -1 if the operation is not available and 0 if it is.

Currently the following parameters for vga_accel() are defined:

```
vga_accel(ACCEL_FILLBOX, int x, int y, int w, int h)
```

Simple solid fill of a box at pixels (x, y) with width w and height h in the current foreground color.

```
vga_accel(ACCEL_SCREENCOPY, int x1, int y1, int x2, int y2, int w, int h)
```

Simple screen-to-screen blit. It copies a box of width w and height h pixels from position x1, y1 to position x2, y2. You may assume that the copy is noncorrupting in case of overlapping source and destination areas.