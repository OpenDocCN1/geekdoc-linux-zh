**Note**

*Although threeDkit functions begin with the gl\_* prefix, they are not a part of vgaal.*

Ignoring these shortcomings, let's jump right in. The first function to explore is gl\_strangle(int x0, int y0, int x1, int y1, int x2, int y2, int color, int bf). The s in strangle stands for solid (as this will be a filled triangle). It should be fairly self-explanatory; you pass the x and y values of three screen points to the function, followed by the fill color. Then you get to that weird bf value. This is used in three-dimensional drawing, so you won't need to be concerned with it here. Its purpose is to state when, if ever, the triangle shouldn't be drawn (say, if it were on the back side of a hill, and drawing it would only slow things down because it would be overwritten by the front side of the hill anyway). For now, use a value of -1 for bf, which should ensure that the triangle will always be drawn.

If you're using a screen mode of 640x480, and you use points (100,300), (150,290), and (230,260), your output will resemble what's shown in Figure 11.6.

Note that you can create an octagon with eight calls to gl\_strangle(); the triangles point inward like eight pieces of a pie. See Listing 11.4 and Figure 11.7 for an example of how one might do this.

# Listing 11.4  Code for the octagon.

```
```c
#include <std\lib.h>
#include <vga.h>
#include <vgaal.h>
#include "triangle.h"

int main(void)
{
   int c = 3,
       bf = -1;

   vga\_init();
   vga\_setmode((640x480x16));
   gl\_setcontextvga((640x480x16));

   gl\_strangle(270, 223, 303, 190, 320, 240, c, bf);
   gl\_strangle(303, 190, 336, 190, 320, 240, c, bf);
   gl\_strangle(336, 190, 370, 223, 320, 240, c, bf);
   gl\_strangle(370, 223, 370, 256, 320, 240, c, bf);
   gl\_strangle(370, 256, 336, 290, 320, 240, c, bf);
   gl\_strangle(336, 290, 303, 290, 320, 240, c, bf);
   gl\_strangle(303, 290, 270, 256, 320, 240, c, bf);
   gl\_strangle(270, 256, 270, 223, 320, 240, c, bf);
```
```