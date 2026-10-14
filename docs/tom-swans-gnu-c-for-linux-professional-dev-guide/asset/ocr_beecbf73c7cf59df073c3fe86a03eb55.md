■ **CoordModePrevious** Considers all XPoint coordinate values except the first to be relative to the preceding XPoint object.

The sample program uses the first setting so that all XPoint values are relative to the window’s origin. If you use the second mode setting, the drawing “walks” off the screen because each new point except for the first is considered to be relative to the previous one. In other words, with setting CoordModePrevious, if point A is (100, 100) and B is (50, 50), then B is actually at (150, 150) relative to the window. Normally, you should use CoordModeOrigin to connect polygon lines.

Another way to fill a polygon is to use a pixmap to fill the shape’s interior with a pattern. This requires some additional techniques that are useful in a variety of graphical programs. For example, you might use these methods to create a button with a shaded surface. Listing 28.7, xpat.cpp, demonstrates how to load and use a pixmap to paint a filled polygon with background colors selected at random. As with the previous example (Listing 28.6), run xpat.cpp and click the mouse pointer in the window to change the image. The pixmap is created from the same bitmap image from the xtile.cpp program in Chapter 27, “Controlling Xlib Input and Output.” Figure 28.5 shows a sample of the program’s output.

![](bbox=[0.059, 0.461, 0.515, 0.608])

```
**LISTING 28.7  XPAT.CPP (PARTIAL)**

```cpp
#define MAXPOINTS 12  // Num XPoint objects in points array
XPoint points[MAXPOINTS];
unsigned long polyColor;
unsigned int bmWidth, bmHeight; // Bitmap width and height
unsigned char * bitmap;          // Pointer to raw bitmap data
Pixmap pixmap;                   // Pixmap of same screen depth

void GetColors(unsigned long intDefaultColor);
void GetPoints(Window win, int winWidth, int winHeight);
void Paint(Window win, GC gc, int winWidth, int winHeight);

int main()
{
    srandom( time(NULL) );  // Seed random generator

    ...

    // Load bitmap from file for use as window background
```
```