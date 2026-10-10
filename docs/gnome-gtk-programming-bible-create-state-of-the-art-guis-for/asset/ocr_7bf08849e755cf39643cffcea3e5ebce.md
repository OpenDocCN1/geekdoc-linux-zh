![](bbox=[0.14, 0.13, 0.23, 0.22])

As a bit of legacy built into X at its very beginning, outlined rectangles are larger than filled rectangles. The drawing concept used is that a coordinate specifies a point *between* the pixels, and all drawing at that point occurs to the pixel below and to the right of the coordinate. For the most part this works the way we expect, but this one-pixel difference in size results from using these rules to determine which pixels are bound by the coordinates when filling, and which pixels are drawn when outlining.

# # Drawing and Filling Polygons

A polygon can be drawn from a set of points. The points are stored as an array of GdkPoint struct —the same as for pixel-by-pixel drawing described earlier in this chapter. The function `gdk_draw_polygon()` draws a line segment from the first point to the second one, then to the third, and so on until a line is drawn to the last point. Then, to close the polygon, a line is drawn from the last point back to the first one. The following example draws the same polygon in *different* ways to show the results of filling and outlining.

```
1 /** polygons.c **/
2 #include <gnome.h>
3
4 gint eventDelete(GtkWidget *widget,
5           GdkEvent *event,gpointer data);
6 gint eventDestroy(GtkWidget *widget,
7           GdkEvent *event,gpointer data);
8 gboolean eventDraw(GtkWidget *widget,
9           GdkEvent *event,gpointer data);
10
11 #define HORIZ 20
12 #define VERT 20
13 #define WIDTH (HORIZ * 29)
14 #define HEIGHT (VERT * 9)
15
16 static GdkPoint points[] = {
17     { 80, 20 },
18     { 20, 80 },
19     { 40, 80 },
20     { 60, 120 },
21     { 20, 160 },
22     { 80, 140 },
23     { 140, 160 },
24     { 100, 120 },
25     { 120, 80 },
26     { 140, 80 },
27 };
28
29 int main(int argc,char *argv[])
```