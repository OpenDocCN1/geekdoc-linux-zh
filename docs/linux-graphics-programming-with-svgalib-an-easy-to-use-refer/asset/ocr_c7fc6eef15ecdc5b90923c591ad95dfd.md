# **void gl_getcontext(GraphicsContext *gc)**

Here is the void gl_getcontext(GraphicsContext *gc) code:

```
extern GraphicsContext currentcontext
```

Saves the current context in the structure variable gc. You can also get the current context from the global variable currentcontext. However, you access single elements in this structure with the macros given in vgagl. Don't copy currentcontext into another structure because the size of the structure might change, and your program doesn't know when it will be linked dynamically to future SVGAlib versions. Instead, use gl_allocatecontext() to allocate such a structure, fill it with gl_getcontext(), and release it with free() after usage.

# **void gl_setcontext(GraphicsContext *gc)**

Restores a previously saved context (makes it the current context).

# **int gl_setcontextvga(int mode)**

Sets the graphics context to the physical screen of a VGA mode, as defined in vga_setmode(). The mode must be set with vga_setmode() prior to using any of the drawing functions; vgagl doesn't take care of that. The function returns 0 for success and nonzero if the given mode is not supported by the hardware.

# **int gl_setcontextvgavirtual(int mode)**

Allocates a virtual screen in system memory identical to the graphics mode, as defined in vga_setmode(), and makes that the current graphics context. The function returns 0 for success and nonzero if the given mode is not supported by the hardware.

# **void gl_setcontextvirtual(int w, int h, int bpp, int bitpsp, void *vbuf)**

Defines the current graphics context to have a width of w pixels, a height of h pixels, bpp bytes per pixel, bitpsp significant color bits per pixel (8, 15, 16 or 24), with the frame buffer at vbuf. A 4-bytes-per-pixel context, with 24 significant color bits, is also valid.

# **GraphicsContext \*gl_allocatecontext(void)**

Allocates a graphics context. This is preferable to hard-coding a context variable in a program because doing so may make your code incompatible with any possible future versions of vgagl that might have additional context fields.

# **void gl_freecontext(GraphicsContext *gc)**

Frees the space allocated for the virtual screen in the given context gc. This should be a virtual context.

# **void gl_setcontextwidth(int w)**

See gl_setcontextheight().