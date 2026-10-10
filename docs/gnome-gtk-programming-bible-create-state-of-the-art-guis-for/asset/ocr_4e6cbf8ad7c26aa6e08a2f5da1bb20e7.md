Lines 26 through 31 create the drawing area, attach it to the application window, and assign to it the callback function *eventDraw*(). The pixels are painted to the window in the callback function.

The loop beginning on line 51 draws a zigzag line diagonally across the window as shown in Figure 10-2. The call to *gdk_draw_point*() on line 53 draws a black pixel. Because it is in a loop (beginning on line 52) and the *x* coordinate is incremented with each pixel drawing, the result is the horizontal line portion of the zigzag. The second loop, beginning on line 58, calls *gdk_draw_point*() to draw a white pixel while incrementing the *y* coordinate—which is the vertical portion of the zigzag.

![](bbox=[0.19, 0.38, 0.57, 0.54])

# Figure 10-2: Individual pixels drawn to a window

Lines 66 through 73 scatter white pixels randomly around the window. Using a constant value to seed the random number generator, as done in the call to *srand*() on line 66, the same sequence of pseudo-random numbers is generated. In this case, the ability to reproduce the same sequence is an advantage because the window can draw itself in exactly the same way every time it is exposed. Lines 68 and 69 call *rand*() to generate new values for both *x* and *y*. The function *rand*() returns a number from 0 to RAND_MAX, so it is necessary to scale the number to the range of possible pixel locations. The call to *gdk_draw_point*() draws the pixel using the white GdkGC. You can see the white spots scattered around the window in Figure 10-2.

Lines 76 through 79 use a different method of drawing pixels. Instead of calculating each pixel position and looking to draw each one, the pixel locations are stored in the array of *GdkPoint* structs defined on line 39. When drawn as black pixels, it appears as the smiley face on the left side of Figure 10-2. The GdkPoint struct contains nothing more than an *x* and a *y* value:

```
struct _GdkPoint {
  gint16 x;
  gint16 y;
};
```