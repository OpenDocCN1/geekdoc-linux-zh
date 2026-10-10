
![](img/8bcc1ba72831c7d67cfc8b395deab95f_342_0.png)

**Figure 10-5:** Polygons being filled and outlined

Lines 76 through 87 move the array coordinates to the right and draw two polygons. The first drawing is a black outline and the second is a white-filled shape. The same situation that applies to rectangles applies to polygons — the outline is slightly larger than the filled form. As with a rectangle, vertical right sides are one pixel further to the right and horizontal bottom sides are one pixel further down. As you can see from the patterns along the edges of the third polygon in the figure, the filled polygon covers some of the pixels and leaves others.

The polygon on the right, drawn by lines 89 to 100, has the filler drawn first and then the outline drawn on top of it. This way, the outline around the polygon is complete.

## Drawing Circles, Ellipses, and Arcs

The following program demonstrates the drawing and filling of curved shapes. The same function is used to draw both circles and ellipses (a circle is simply an ellipse with the same height and width). This function also has the ability to limit the drawing to only a portion of the circle or ellipse. Additionally, there is an option to draw the figure as an outline, or to fill the region created by the shape.

```c
/** arcs.c **/
#include <gnome.h>

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data);
gboolean eventDraw(GtkWidget *widget, GdkEvent *event, gpointer data);
static void drawArcs(GtkWidget *widget, gint y, gint fill);

#define WIDTH 455
#define HEIGHT 140

int main(int argc, char *argv[])
{
    GtkWidget *app;
    GtkWidget *area;

    gnome_init("arcs", "1.0", argc, argv);
    app = gnome_app_new("arcs", "Drawing Circles and Ellipses");
    gtk_container_set_border_width(GTK_CONTAINER(app), 20);
    gtk_signal_connect(GTK_OBJECT(app), "delete_event",
                       GTK_SIGNAL_FUNC(eventDelete), NULL);
    gtk_signal_connect(GTK_OBJECT(app), "destroy",
                       GTK_SIGNAL_FUNC(eventDestroy), NULL);

    area = gtk_drawing_area_new();
    gtk_widget_set_size(area, WIDTH, HEIGHT);
    gnome_app_set_contents(GNOME_APP(app), area);

    gtk_signal_connect(GTK_OBJECT(area), "event",
                       GTK_SIGNAL_FUNC(eventDraw), NULL);

    gtk_widget_show_all(app);
    gtk_main();
    exit(0);
}

gboolean eventDraw(GtkWidget *widget, GdkEvent *event, gpointer data) {
    drawArcs(widget, 0, FALSE);
    drawArcs(widget, 80, TRUE);
    return(TRUE);
}

static void drawArcs(GtkWidget *widget, gint y, gint fill) {
    gdk_draw_arc(widget->window,
                 widget->style->black_gc,
                 fill,
                 0, y,
                 60, 60,
                 0, 360 * 64);
    gdk_draw_arc(widget->window,
                 widget->style->black_gc,
                 fill,
                 80, y,
                 60, 60,
                 135 * 64, 90 * 64);
    gdk_draw_arc(widget->window,
                 widget->style->black_gc,
                 fill,
                 110, y,
                 60, 60,
                 135 * 64, -270 * 64);

    gdk_draw_arc(widget->window,
                 widget->style->black_gc,
                 fill,
                 190, y,
                 100, 60,
                 0, 360 * 64);
    gdk_draw_arc(widget->window,
                 widget->style->black_gc,
                 fill,
                 310, y,
                 100, 60,
                 135 * 64, 90 * 64);
    gdk_draw_arc(widget->window,
                 widget->style->black_gc,
                 fill,
                 350, y,
                 100, 60,
                 135 * 64, -270 * 64);
}

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data) {
    return(FALSE);
}

gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data) {
    gtk_main_quit();
    return(0);
}
```

The function `eventDraw()` on line 40 is called whenever the drawing area is exposed. It calls `drawArcs()` to do the actual drawing. The top row shown in Figure 10-6 is drawn by the call to `drawArcs()` on line 43, and the second row is drawn by the call on line 44. The first argument is the drawing area widget. The second argument is the offset along the x-axis. The third argument determines whether or not the drawn figures are filled.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_344_0.png)

**Figure 10-6:** Draw and fill both complete and incomplete arcs

The call to `gdk_draw_arc()` on line 49 draws a complete circle in the upper-left corner of the drawing area. The first and second arguments are the window and the graphics context. The next argument is TRUE if the figure is to be filled, and FALSE if otherwise. The next two arguments are the x and y coordinates of the circle. These coordinates determine the location of the upper-left corner of the box bounding the circle or ellipse. The next two arguments are the width and height of the bounding box.

The next-to-last argument to `gdk_draw_arc()` is the angle at which the drawing of the arc should begin. The last argument determines how far around the circle the drawing should proceed. The angles are integer values; the units are 1/64th of a degree. The angles are set up in the Cartesian coordinate system with zero degrees to the right and positive angles counter-clockwise.

The mechanics involved with drawing an arc are shown in Figure 10-7. In the figure, the drawing begins at the 45-degree point and proceeds counter-clockwise for a total of 270 degrees—which, after adding the original 45 degrees to it, brings the end of the circle to an angle of 315 degrees. You can specify a negative value for either or both of the angles. A negative starting angle positions itself clockwise from the 0-degree location on the left. Also, a negative angle value for the second angle causes drawing to take place from the starting angle in a clockwise manner. For example, another way to draw the same arc as in Figure 10-7 is to use `-(45 * 64)` as the starting angle and `-(270 * 64)` as the number of degrees to draw. The resulting curve looks like the one in the figure, but the curve is drawn in the opposite direction.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_345_0.png)

Figure 10-6 showed the same set of figures being drawn and filled. With a closed circle or ellipse, the outline inscribes the same shape as the fill. When the circle or ellipse is not closed, the outline simply leaves a portion blank, while the fill function assumes boundary lines from each end of the curve to the center of the figure.

## Drawing Text

There are two functions that draw strings of characters to a drawing area. They both require an array of character values as input, but one draws the entire string while the other draws a selected subset.

```c
/** text.c **/
#include <gnome.h>

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data);
gboolean eventDraw(GtkWidget *widget, GdkEvent *event, gpointer data);
static void mark(GtkWidget *widget, gint x, gint y);

#define WIDTH 420
#define HEIGHT 140

int main(int argc, char *argv[])
{
    GtkWidget *app;
    GtkWidget *area;

    gnome_init("text", "0.0", argc, argv);
    app = gnome_app_new("text", "Drawing Text");
    gtk_signal_connect(GTK_OBJECT(app), "delete_event",
                       GTK_SIGNAL_FUNC(eventDelete), NULL);
    gtk_signal_connect(GTK_OBJECT(app), "destroy",
                       GTK_SIGNAL_FUNC(eventDestroy), NULL);

    area = gtk_drawing_area_new();
    gtk_widget_set_size(area, WIDTH, HEIGHT);
    gnome_app_set_contents(GNOME_APP(app), area);
    gtk_signal_connect(GTK_OBJECT(area), "event",
                       GTK_SIGNAL_FUNC(eventDraw), NULL);

    gtk_widget_show_all(app);
    gtk_main();
    exit(0);
}
```
