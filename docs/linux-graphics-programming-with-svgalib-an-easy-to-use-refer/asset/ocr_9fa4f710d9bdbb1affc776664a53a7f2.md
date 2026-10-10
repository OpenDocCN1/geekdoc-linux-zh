(But how does an application know?) The Mach32 support for this is smarter. It enables this feature only when it's safe to be used.

To avoid all these problems, you can use the following:

+   - *nonlinear*—Inhibits use of a linear mmap’d frame buffer.
+   - *linear*—Allows (not enforces) use of a linear mmap’d frame buffer.

**Note**

Add a line in the /etc/vga/libvga.config file to disable the linear frame buffer if it cannot be used.

This function returns the size of the mapped framebuffer if successful (it can be less than total video memory) and -1 if not. The *testlinear* demo shows the use of this feature (should it work for you).

```
void vga_setmodeX(void)
```

Tries to enable Mode X-like memory organization for the 256-color modes that use up to 256K of memory, such as G320x200x256 and G640x400x256. Modes such as G320x240x256 are Mode X-like by default. *vga_modeinfo*() lists which modes have Mode X memory layouts. A Mode X-like memory layout means that memory is organized in four pages—one vga_setpage()—and that the top-most pixel (0,1,2,3) is the first pixel in pages 0, 1, 2, and 3. Pixels 4, 5, 6, 7 are then the second pixels in pages 0, 1, 2, and 3.

On the other hand, packed pixel screen modes will have pixel 0,1,2,3 as pixel 0,1,2,3 in page 0, and so on. It will only use the next pages if the size of the first 64K page is exceeded. This is the way that most SVGA 256-color modes work. This function isn’t guaranteed to work. A better method would be to define a new mode for planar 320x200x256.

# ## Extended Features

This enormous section deals with SVGAlib’s extended features:

```
int vga_ext_set(unsigned what, ...)
```

This function comprises several extended features of SVGAlib. Before trying to call vga_ext_set(), you should check whether it’s available in *vga_getmodeinfo()* for compatibility with older versions of SVGAlib. In addition, the availability of certain features will depend on the current graphics mode. However, VGA_EXT_PAGE_OFFSET and VGA_EXT_FONT_SIZE are features of the base module of SVGAlib and are always available if your version of SVGAlib supports them.

Actually, the result of *vga_getmodeinfo()* shows the availability of enhancements of vga_ext_set() in the given SVGA graphics mode. Hence, these base features may be supported even if SVGAlib doesn’t admit it. Since version 1.2.13, you’ve been able to check *vga_getmodeinfo*(TEXT) to see if basic *vga_ext_set()* functionality is available. The VGA_EXT_PAGE_OFFSET and VGA_EXT_FONT_SIZE calls are then available in any mode even if *vga_getmodeinfo()* states that you shouldn’t call *vga_ext_set()* at all.