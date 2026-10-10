There are some special exceptions (such as foreground and background colors) but for the most part, the contents of a graphics context cannot be addressed directly. However, they can be copied in and out using a GdkGCValues struct:

```
struct _GdkGCValues {    GdkColor foreground;    GdkColor *background;    GdkFont *font;    GdkFunction function;    GdkFill fill;    GdkPixmap *tile;    GdkPixmap *stipple;    GdkPixmap *clip_mask;    GdkSubwindowMode subwindow_mode;    gint ts_x_origin;    gint ts_y_origin;    gint clip_x_origin;    gint clip_y_origin;    gint graphics_exposures;    gint line_width;    GdkLineStyle line_style;    GdkCapStyle cap_style;    GdkJoinStyle join_style;};
```

The following example retrieves the graphics context from a window and displays information about its contents. It not only displays the values stored in a GdkGC, it also demonstrates which values are available for each field.

```
1 /* showgc.c **/
2 #include <gnome.h>
3
gint eventDelete(GtkWidget *widget,
GdkEvent *event,gpointer data);
gint eventDestroy(GtkWidget *widget,
GdkEvent *event,gpointer data);
int listValues(gpointer data);
static char *functionString(GdkFunction function);
static char *fillString(GdkFill fill);
static char *subwindowString(GdkSubwindowMode mode);
static char *lineStyleString(gint style);
static char *capStyleString(gint style);
static char *joinStyleString(gint style);

#define WIDTH 40
#define HEIGHT 30

int main(int argc,char *argv[])
{

GtkWidget *app;
GtkWidget *area;
```