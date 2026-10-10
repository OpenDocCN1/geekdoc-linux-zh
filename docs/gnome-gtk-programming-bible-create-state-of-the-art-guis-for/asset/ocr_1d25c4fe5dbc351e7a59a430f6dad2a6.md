# Drawing Area Basics

A GtkDrawingArea widget is not much more than a basic X window—it is simply a window as a widget. There is a set of function calls that you can use to paint the pixels in a variety of ways. But the process is a little different from that of other widgets. Your program must take more responsibility for the details because this is all done at a level below some of the GTK+ (and the entire GNOME!) automation.

Most GNOME and GTK+ widgets assume the responsibility of keeping their display updated. This is not so with a GtkDrawingArea. You need to set up a callback function that draws the window whenever it becomes visible. Also, since you have pixel-by-pixel control of what gets drawn, you need to use GdkGC (graphics context) objects to do the drawing. There are a number of GdkGC objects that are supplied as a part of the GTK+ widget but, for special situations, you may need to create your own.

The following example demonstrates the basics of setting up a drawing area. This program fills the application window with a GdkDrawingArea and draws two lines on it.

```
1 /** simpleline.c **/
2 #include <gnome.h>
3
4 gint eventDelete(GtkWidget *widget,
5             GdkEvent *event,gpointer data);
6 gint eventDestroy(GtkWidget *widget,
7             GdkEvent *event,gpointer data);
8 gboolean eventDraw(GtkWidget *widget,
9             GdkEvent *event,gpointer data);
10
11 #define WIDTH 200
12 #define HEIGHT 100
13
14 int main(int argc, char *argv[])
15 {
16     GtkWidget *app;
17     GtkWidget *area;
18
19     gnome_init("simpleline","1.0",argc,argv);
20     app = gnome_app_new("simpleline","Drawing Area");
21     gtk_signal_connect(GTK_OBJECT(app),"delete_event",
22             GTK_SIGNAL_FUNC(eventDelete),NULL);
23     gtk_signal_connect(GTK_OBJECT(app),"destroy",
24             GTK_SIGNAL_FUNC(eventDestroy),NULL);
25
26     area = gtk_drawing_area_new();
27     gtk_widget_set_usize(area,WIDTH,HEIGHT);
28     gnome_app_set_contents(GNOME_APP(app),area);
29
30     gtk_signal_connect(GTK_OBJECT(area),"event",
31             GTK_SIGNAL_FUNC(eventDraw),NULL);
```