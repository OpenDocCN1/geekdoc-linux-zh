It’s also possible to customize a dashed line’s appearance, similar to the way a word processor lets you select tart spacing. Basically, to do this, you need to provide a list of dash and space widths and call the Xlib `XSetDashes()` function to insert this information into a GC before drawing your lines. Enter *info XSetDashes* for more information about this topic.

# FILL RULES AND STYLES

Unlike with many graphics libraries, even complex shapes such as filled polygons are drawn by the X server, not by code linked to the client application. Although accessed through Xlib function calls, graphics primitives are intrinsic properties of X. The importance of this feature might not be realized until you consider that your client application can run on a wide range of hardware without requiring linking to system-dependent object code.

Even the most complex of graphical operations such as filling a polygon with a color pixmap are handled in the X server. The next two programs (see Listings 28.6 and 28.7) demonstrate these features and explain some other options you can select to fine-tune your program’s graphical output.

Listing 28.6, xfill.cpp, displays polygons filled with solid colors. The polygon coordinates and colors are selected at random using the standard C library’s `random()` function. Run the program and click the mouse inside the window to display a new polygon in one of several possible colors. Figure 28.4 shows a sample of the program’s output.

![](bbox=[0.069, 0.524, 0.531, 0.658])

```
```cpp
#define MAXPOINTS 12 // Num XPoint objects in points array
XPoint points[ MAXPOINTS ];
unsigned long polyColor;

void GetColors(unsigned long int defaultColor);
void GetPoints(int winWidth, int winHeight);
void Paint(Window win, GC gc, int winWidth, int winHeight);

int main()
{
  srandom( time(NULL) );  // Seed random generator
  ...
}
```
```