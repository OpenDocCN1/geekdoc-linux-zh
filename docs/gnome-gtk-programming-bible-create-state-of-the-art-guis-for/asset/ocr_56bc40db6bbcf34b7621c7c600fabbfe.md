Lines 79 through 89 copy the right-foot section of the source bitmap to the drawing area, and then, using another string, adds a tag noting that it is the right foot. Lines 91 through 100 add an annotation to the left foot. The call to gkd_draw_string() draws the text. The call to gdk_draw_polygon() uses the set of points defined on line 45 to draw a filled arrow pointing from the text to the foot.

Lines 102 and 103 return the pixmap and the font to the system. The callback routine builds them from scratch each time it is called, so there is no need to keep it—besides, failure to return it can cause memory leaks. In a real application, it makes more sense to store both of these in static variables so they can be used again without requiring a complete rebuild.

# # Resizing the Drawing Area

The drawing area may be resized, depending on the rules applied to it by its containing widget. If you ignore the size change, your drawing can leave spaces or be clipped on the right and bottom. However, you can have your drawing resize itself to fit the new window configuration.

> > It may not be worth the effort to write the code that resizes the drawing. To make a drawing resizable, you need to calculate all the coordinates as a ratio of width and height of the window. Some things, such as XPM image data and text fonts, don’t rescale easily. Also, a change in the aspect ratio changes circles to ellipses and squares to rectangles.

The following example draws rectangles based on the height and width of the window, and allows for these values to change.

```
```
1 /** configure.c **/
2 #include <gnome.h>
3
4 gint eventDelete(GtkWidget *widget,
5    GdkEvent *event,gpointer data);
6 gint eventDestroy(GtkWidget *widget,
7    GdkEvent *event,gpointer data);
8 gboolean eventDraw(GtkWidget *widget,
9    GdkEvent *event,gpointer data);
10 gboolean eventConfigure(GtkWidget *widget,
11    GdkEventConfigure *event,gpointer data);
12
13 static int width = 20;
14 static int height = 20;
15
16 int main(int argc,char *argv[])
17 {
18    GtkWidget *app;
```
```