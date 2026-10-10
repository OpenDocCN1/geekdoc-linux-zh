
vga_setcolor(1);
for (y = 75; y < 120; y++)
{
    vga_drawline(230, y, 280, y);
}

/* When any key is pressed, the red square disappears. */
vga_getch();
vga_setcolor(0);
for (y = 75; y < 120; y++)
{
    vga_drawline(30, y, 80, y);
}

/* On the next keypress, the green square disappears.
   The active color's already black, so we don't need to
   reset it with another vga_setcolor() statement. */
vga_getch();
for (y = 75; y < 120; y++)
{
    vga_drawline(130, y, 180, y);
}

/* And now the blue. Are we having fun yet? */
vga_getch();
for (y = 75; y < 120; y++)
{
    vga_drawline(230, y, 280, y);
}

/* Pause for a second, and then exit. Thank God. */
sleep(1);
vga_setmode(TEXT);
return 0;
}

If we wanted to wipe out everything in one fell swoop, **without** ending the program, we'd just use **vga_clear()**. This will reset the entire screen to color 0, which is usually black. Later on we'll discuss how to change the colors associated with numbers, but for now, you'll have to stick with the default. As Henry Ford said, you can have any color you want, so long as it's black.

![](img/2e475714ef8969ed272622c46473d334_76_0.png)

Final exam for this section: Draw a hollow triangle with **vga_drawline()**. I'll bet you can!

## Creating Your Own Functions

Wouldn't it be nice if you could set the background color to anything you want at the beginning of your program? Or perhaps draw a square with a single statement? Unfortunately, with straight SVGAlib, you can't. Now, vga* (the high-level library of drawing functions that complements SVGAlib) is filled with all sorts of fun stuff like that, but let's stick with pure SVGAlib for the moment. So, how can you color the screen without having to code a bunch of vga_drawline( ) functions? The answer is, of course, to create our own function. You save time by coding this procedure once and never having to do it again.

Listing 3.12 contains a sample function for setting the background color using only pure SVGAlib. We'll use two new functions to do it: vga_getxdim( ) and vga_getydim( ). These will tell us the x and y dimensions of the current screen mode—for example, the integer value returned by vga_getxdim( ) while in screen mode 5 (G320x200x256) is 320.

Now, what to call this new function? I don't want to preface it with vga because someone might be confused and think it's an actual, out-of-the-box function that comes with his or her distribution of SVGAlib. Instead, let's name it book_background( ). Listing 3.12 shows what I'm talking about.

**Listing 3.12 book_background().**

```c
void book_background(int color)
{
  int x,
        y,
        xmax = vga_getxdim(),
        ymax = vga_getydim();

  vga_setcolor(color);

  for (y = 0; y < ymax; y++)
  {
    for (x = 0; x < xmax; x++)
    {
      vga_drawline(0, y, xmax, y);
    }
  }
}
```

Now you can change your background in one clean sweep—just insert the function into your program, include the proper declaration, and away you go! For example, to make your background cyan, just use **book_background**(3). Listing 3.13 provides an example of using this function.

**Listing 3.13 Using book_background(0).**

```c
#include <stdlib.h>
#include <vga.h>

void book_background(int color);

int main(void)
{
int y;

vga_init();
vga_setmode(G320x200x256);

/* How about a lovely shade of cyan? */
book_background(3);

/* Draw another one of those wretched squares here,
or anything else that you'd like. */
vga_setcolor(2);
for (y = 75; y < 120; y++)
{
vga_drawline(130, y, 180, y);
}

vga_getch();
vga_setmode(TEXT);
return 0;
}

void book_background(int color)
{
int x,
y,
xmax = vga_getxdim(),
ymax = vga_getydim();

vga_setcolor(color);

for (y = 0; y < ymax; y++)
{
for (x = 0; x < xmax; x++)
{
vga_drawline(0, y, xmax, y);
}
}
}
```

Now, this is obviously slow, especially in the higher resolution modes, but it does demonstrate the principle of creating your own drawing functions. In Chapter 4, we'll make better work of this, but for now, be content to know that you have the ability to simplify your programs.

Ensure that any color assignments you make (that are not immediately followed by drawing functions) come *after* **book_background()**, because they'll be lost once this is done. For clarification purposes, the snippet in Listing 3.14 shows the wrong way to do it.

**Listing 3.14 A wasted color declaration.**

```c
vga_setcolor(8);
/* Color is now dark gray */

book_background(5);
/* Current color is now magenta, along with the
   background */

vga_drawline(10, 10, 100, 100);
/* Surprise! The line was drawn in magenta, not dark gray,
   making it invisible. */
```

You can avoid this by setting your colors immediately before the functions in which they're needed. Another solution is to pass a second argument to **book_background()**, this one stating the current color number, and then revising **book_background()** to reset the current color back to its previous assignment. Make sense?

At this point, you should be an expert on home-brewed functions. Can you figure out how to write and implement **book_square()**? How about **book_filledsquare()**?

### Vgagl

Before you start thinking that SVGAlib is for total lamen with a lot of time on their hands, let's jump into the high-speed, low-drag functions of vgagl. As you may remember, these functions aren't exactly a part of SVGAlib itself; instead, they're part of a second shared library that complements SVGAlib. As such, they need another flag on the command line during compilation: -lvagagl.

Don't be afraid to mix and match functions from SVGAlib and vgagl. A program doesn't have to be exclusively one or the other. In fact, vgagl requires the same **vga_init()** and **vga_setmode()** statements that we used before. Note, however, that you must initialize the vgagl library before you use it. This is done with the **gl_setcontextvga(int mode)** command, which should come immediately after **vga_setmode()**. Both should use the same mode number. Also, you'll need to #include <vgagl.h> in addition to <vga.h>. Finally, if you haven't noticed, all vgagl functions are prefixed with gl_.

To use vgagl functions, you *must* use the `gl_setcontextvga(int mode)` statement, and you *must* include the `-Ivgagl` flag **before** `-Ivga` during compilation. Otherwise, you’ll be looking at some segmentation faults. Lastly, `#include <vgagl.h>`.

Now we’re ready to rock and roll.

## Shapes, The Fast And Easy Way

Let’s revisit that program with the three squares. Now we’ll do it the vgagl way, as shown in Listing 3.15, which means using `gl_fillbox(int x, int y, int w, int h, int c)`.

**Listing 3.15 Three squares with vgagl.**

```c
#include <stdlib.h>
#include <vga.h>
#include <vgagl.h>

int main(void)
{
    vga_init();
    vga_setmode(G320x200x256);
    gl_setcontextvga(G320x200x256);

    gl_fillbox(30, 85, 50, 45, 4);
    gl_fillbox(130, 85, 50, 45, 2);
    gl_fillbox(230, 85, 50, 45, 1);

    vga_getch();
    vga_setmode(TEXT);
    return 0;
}
```

Now, that’s a bit cleaner, isn’t it? It’s a lot faster, too. The vgagl-specific parts are highlighted in gray. We need to supply five arguments to `gl_fillbox()`: the upper-left x coordinate, the upper-left y coordinate, the width, the height, and the color. You compile it like this:

```bash
gcc -Wall -O3 -o gl_squares gl_squares.c -Ivgagl -Ivga
```

You can color the background by drawing one large box. To give a mode 5 screen a red background, all you have to do is use `gl_fillbox(0, 0, 320, 200, 4)`. That sure beats the heck out of `book_background()`.

Let’s make a more interesting program with vgagl. Let’s show all the standard 256 colors of SVGALib, displayed in a neatly arranged 16×16 grid of boxes (made with `gl_fillbox()`, of course). Have a look at Listing 3.16 for my rendition of this.

> **Warning**  
> *For now, don’t try using vgagl in 16 color modes.*

**Listing 3.16 Neatly arranged boxes displaying the first 256 standard SVGA colors.**

```c
#include <stdlib.h>
#include <vga.h>
#include <vgagl.h>

int main(void)
{
    int x,
        y,
        c = 0;

    vga_init();
    vga_setmode(G320x200x256);
    gl_setcontextvga(G320x200x256);

    for (y = 2; y < 183; y += 12)
    {
        for (x = 2; x < 183; x += 12)
        {
            gl_fillbox(x, y, 10, 10, c++);
        }
    }

    vga_getch();
    vga_setmode(TEXT);
    return 0;
}
```

Figure 3.4 shows how this should turn out, minus the color.

Pretty cool, huh? If you only compile one program from this chapter, I’d suggest you do this one. Not only will you be able to impress your friends, you’ll have the option of using this as a programming reference for the future. Need a hue? Just fire up your 256-color table and choose one.

Notice that the second half of the colors is rather dark. Some people complain that the programs they’ve ported to SVGA**lib** are too dark; their colors aren’t exactly the same as

**Port**

To alter software so that it can be run under a different operating system. If you’re rewriting the graphics in a Windows C program for SVGA**lib**, you’re porting the program to Linux. This is often easier said than done, regardless of the source or destination.
