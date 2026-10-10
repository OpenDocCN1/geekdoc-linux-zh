Now, this is obviously slow, especially in the higher resolution modes, but it does demonstrate the principle of creating your own drawing functions. In Chapter 4, we'll make better work of this, but for now, be content to know that you have the ability to simplify your programs.

Ensure that any color assignments you make (that are not immediately followed by drawing functions) come *after* **book\_background()**, because they'll be lost once this is done. For clarification purposes, the snippet in Listing 3.14 shows the wrong way to do it.

# **Listing 3.14 A wasted color declaration.**

```
```
vga_setcolor(8);
/* Color is now dark gray */

book_background(5);
/* Current color is now magenta, along with the
   background */

vga_drawline(10, 10, 100, 100);
/* Surprise! The line was drawn in magenta, not dark gray,
   making it invisible. */
```
```

You can avoid this by setting your colors immediately before the functions in which they're needed. Another solution is to pass a second argument to **book\_background()**, this one stating the current color number, and then revising **book\_background()** to reset the current color back to its previous assignment. Make sense?

At this point, you should be an expert on home-brewed functions. Can you figure out how to write and implement **book\_square()**? How about **book\_filledsquare()**?

# ### Vgagl

Before you start thinking that SVGAlib is for total lamen with a lot of time on their hands, let's jump into the high-speed, low-drag functions of vgagl. As you may remember, these functions aren't exactly a part of SVGAlib itself; instead, they're part of a second shared library that complements SVGAlib. As such, they need another flag on the command line during compilation: -lvagagl.

Don't be afraid to mix and match functions from SVGAlib and vgagl. A program doesn't have to be exclusively one or the other. In fact, vgagl requires the same **vga\_init()** and **vga\_setmode()** statements that we used before. Note, however, that you must initialize the vgagl library before you use it. This is done with the **gl\_setcontextvga(int mode)** command, which should come immediately after **vga\_setmode()**. Both should use the same mode number. Also, you'll need to #include <vgagl.h> in addition to <vga.h>. Finally, if you haven't noticed, all vgagl functions are prefixed with gl\_.