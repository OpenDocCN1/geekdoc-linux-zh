![](bbox=[0.17, 0.13, 0.38, 0.23])

**Figure 10-1:** A pair of lines drawn on a drawing area

# One Pixel at a Time

If you want to have ultimate control over your graphics, you can write to the window one pixel at a time. There are two basic ways of doing this— a *single-point function* draws a single pixel, and a *multiple-point function* enables you to store the pixel locations in an array. The following example demonstrates both of these methods.

```
1  /* pixels.c **/
2  #include <gnome.h>
3
4  gint eventDelete(GtkWidget *widget,
5            GdkEvent *event,gpointer data);
6  gint eventDestroy(GtkWidget *widget,
7            GdkEvent *event,gpointer data);
8  gboolean eventDraw(GtkWidget *widget,
9            GdkEvent *event,gpointer data);
10
11 #define WIDTH 400
12 #define HEIGHT 200
13
14 int main(int argc,char *argv[])
15 {
16     GtkWidget *app;
17     GtkWidget *area;
18
19     gnome_init("pixels","1.0",argc,argv);
20     app = gnome_app_new("pixels","Drawing Pixels");
21     gtk_signal_connect(GTK_OBJECT(app),"delete_event",
22                GTK_SIGNAL_FUNC(eventDelete),NULL);
23     gtk_signal_connect(GTK_OBJECT(app),"destroy",
24                GTK_SIGNAL_FUNC(eventDestroy),NULL);
25
26     area = gtk_drawing_area_new();
27     gtk_widget_set_usize(area,WIDTH,HEIGHT);
28     gnome_app_set_contents(GNOME_APP(app),area);
29
30     gtk_signal_connect(GTK_OBJECT(area),"event",
31                GTK_SIGNAL_FUNC(eventDraw),NULL);
32
33     gtk_widget_show_all(app);
34     gtk_main();
35     exit(0);
36 }
37 gboolean eventDraw(GtkWidget *widget,
```