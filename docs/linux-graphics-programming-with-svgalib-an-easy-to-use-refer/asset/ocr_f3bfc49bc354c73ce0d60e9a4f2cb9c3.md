# Complete Code

At this point, you have a working interface and some working tools. The next step will be to create the pull-down menus. Because menus are an integral element of any GUI, I've decided to give the subject complete coverage in Chapter 19.

The rectangle and circle routines can be copied more or less from the line functions. That leaves the flood fill, which I'll leave to you to figure out. You may find it easier to go with a different, yet similar, incarnation, in which every pixel of a certain color is changed, regardless of what it touches.

I'll leave you now with the complete code for this chapter. Listing 18.9 has everything I've discussed thus far, plus a little more. Again, the menus will be coded in the next chapter. In case you decide to create your own drawing tools, I've left you plenty of room.

# Listing 18.9  The (more or less) complete drawing program.

```
#include <stdlib.h>
#include <math.h>
#include <unistd.h>
#include <lug.h>
#include <lugfnts.h>
#include <vga.h>
#include <vgagl.h>
#include <vgamouse.h>

/* parameters of drawing window */
#define LEFT      62
#define RIGHT     617
#define TOP        27
#define BOTTOM    457
#define BOX_WIDTH  555
#define BOX_HEIGHT 430

void move_cursor(int x, int y, int ox, int oy);
void draw_cursor(int x, int y);

void tool10_up();
void tool10_down();
void tool11_up();
void tool11_down();
void tool12_up();
void tool12_down();
void tool13_up();
void tool13_down();
void tool14_up();
void tool14_down();
void tool15_up();
```