To ensure that polygon corners are handled right, both start and end points must be drawn (in `ROP_XOR` mode). Accordingly, it's best to use `ACCEL_DRAWLINE` instead of `ACCEL_POLYLINE`. Finally, skip drawing all horizontal lines (which would confuse `ACCEL_SCREENCOPYMONO`).

+   Set foreground and background colors, raster operation, and bitmap transparency to the values you want for your polygon.

+   Use `ACCEL_SCREENCOPYMONO` to copy the offscreen pattern to the screen.

The raster operations and the transparency that are signaled to be supported for `ACCEL_POLYFILLMODE` by `vga_ext_set()` are actually meant to apply to the last `ACCEL_SCREENCOPYMONO` call.

Because this polygon drawing uses more screen read/write operations, it's probably slower than using `ACCEL_DRAWHLINELIST` or `ACCEL_POLYHLINE` for drawing a polygon scanline by scanline. However, it's easier to use and it will work mostly without intervention of the CPU, which can then do other calculations.

> **Note**
> 
> *It's unspecified if the left or right endpoints of the scanlines are drawn, and most cards (such as Mach32) will omit them on one end, at least. Because of that, you should always draw the boundary line in the fill color (or another color) after filling the polygon.*

`vga_accel(ACCEL_SETMODE, mode)`
Sets the blit strategy. There are two choices for `mode`, namely `BLITS_SYNC` AND `BLITS_IN_BACKGROUND`. The first ensures that a `vga_accel()` call only returns when the accelerator has finished its operation. The second allows for an immediate return, thus allowing parallel operation of the CPU and the accelerator. Consecutive accelerator operations will wait for each other to complete (and block if necessary). However, direct screen memory access (done implicitly by calls to some SVGA/ib functions) may find any intermediate state in VGA memory or even corrupt the running accelerator operation.

`vga_accel(ACCEL_SYNC)`
Waits for the accelerator to finish when in `vga_accel(BLITS_IN_BACKGROUND)` mode.

`vga_accel(ACCEL_SETOFFSET, int address)`
Sets a screen offset as `vga_setdisplaystart()` does. The same restrictions for this function, as reported by `vga_getmodeinfo()`, apply to `address`. Whenever the video screen offset is modified, the accelerator's offset will follow. However, you can modify it later with this function.

The following mode values are defined for `vga_accel(ACCEL_SETTRANSPARENCY, int mode, ...):`