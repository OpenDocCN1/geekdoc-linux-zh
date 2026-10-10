# # Drawing Polygons on a Canvas

A *polygon* (a figure of any shape with any number of sides) can be made into an item and displayed on a canvas. The following example program creates a simple arrow item and displays it on a canvas.

```
```
     1  /** canvaspolygon.c **/
     2  #include <gnome.h>
     3
     4  gint eventDelete(GtkWidget *widget,
     5     GdkEvent *event,gpointer data);
     6  gint eventDestroy(GtkWidget *widget,
     7     GdkEvent *event,gpointer data);
     8  GnomeCanvasPoints *makeArrow(gint h_gint v,
     9     gint h_off,gint v_off);
    10
    11 #define HORIZ 30
    12 #define VERT 30
    13 #define WIDTH (HORIZ * 6)
    14 #define HEIGHT (VERT * 6)
    15
    16 int main(int argc,char *argv[])
    17 {
    18     GtkWidget *app;
    19     GtkWidget *canvas;
    20     GnomeCanvasGroup *rootGroup;
    21     GnomeCanvasItem *item;
    22
    23     gnome_init("canvaspolygon", "1.0",argc,argv);
    24     app = gnome_app_new("canvaspolygon",
    25                    "Polygon Item");
    26     gtk_signal_connect(GTK_OBJECT(app),"delete_event",
    27             GTK_SIGNAL_FUNC(eventDelete),NULL);
    28     gtk_signal_connect(GTK_OBJECT(app),"destroy",
    29             GTK_SIGNAL_FUNC(eventDestroy),NULL);
    30
    31     canvas = gnome_canvas_new();
    32     gtk_widget_set_usize(canvas,WIDTH,HEIGHT);
    33     gnome_canvas_set_scroll_region(GNOME_CANVAS(canvas),
    34                 0.0,0.0,WIDTH,HEIGHT);
    35     rootGroup = gnome_canvas_root(GNOME_CANVAS(canvas));
    36     gnome_app_set_contents(GNOME_APP(app),canvas);
    37
    38     item = gnome_canvas_item_new(rootGroup,
    39                 gnome_canvas_polygon_get_type(),
    40                 "points",makeArrow(HORIZ,VERT,HORIZ,VERT),
    41                 "fill_color","white",
    42                 "outline_color","black",
    43                 NULL);
```
```