# **Vertex**

A point in a polygon that comprises the intersection of two or more lines. Vertices also appear in angles, polyhedrons, and graphs.

to get you started. Moving along, I’ve made Listing 11.2 a bit more modularized, so you can see how a polygon function might fit into a “real” program. Keep in mind that the output is the same.

Here’s how they work: Points (or vertices/intersections) are passed to a function, which then proceeds to “connect the dots” with **vga\_drawline()**. That’s about as basic as one can hope for. Have a look at Listings 11.1 and 11.2 to see the intimate details. Although this code may appear to be unnecessarily simplistic to some, it does lay the foundation for the more advanced example in Listing 11.3. Note that it makes no difference how you plot your points—clockwise or counterclockwise—so long as the points are in order.

# **Listing 11.1** Outline of a convex polygon.

```
```c
#include <vga.h>
#include <stdlib.h>

int main(void)
{
    /* The next two lines define the three vertices of the
    triangle. The actual points are (10,10), (10,100), and
    (100,10). The x-coordinates are defined in xarray[] and
    the y-coordinates in yarray[]. */

    int xarray[3] = {10,10,100},
        yarray[3] = {10,100,10},
        x1,
        y1,
        x2,
        y2,
        n = 3,  /* number of vertices */
        i;

    vga_init();
    vga_setmode(G320x200x256);
    vga_setcolor(vga_white());

    for (i = 0; i < n; i++)
    {
        x1 = xarray[i];
        y1 = yarray[i];
        if (i != (n - 1))
        {
```
```