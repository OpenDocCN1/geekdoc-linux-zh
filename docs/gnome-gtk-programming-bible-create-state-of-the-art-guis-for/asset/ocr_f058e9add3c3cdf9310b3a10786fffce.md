# Functions that Set Values in a GtkGC

There are two ways to insert values into a GtkGC. The previous examples all use a function call to set each individual value. Alternatively, you can use a GdkGCValues struct to set several values at the time the graphics context is created. The following example demonstrates the two different methods.

```
1 /** setgc.c **/
2 #include <gnome.h>
3
4 gint eventDelete(GtkWidget *widget,
5     GdkEvent *event,gpointer data);
6 gint eventDestroy(GtkWidget *widget,
7     GdkEvent *event,gpointer data);
8 gboolean eventDraw(GtkWidget *widget,
9     GdkEvent *event,gpointer data);
10 static GtkGC *functionCreateGC(GtkWindow *window);
11 static GtkGC *valueCreateGC(GtkWindow *window);
12
13 #define WIDTH 300
14 #define HEIGHT 100
15
16 int main(int argc,char *argv[])
17 {
18     GtkWidget *app;
19     GtkWidget *area;
20
21     gnome_init("setgc","1.0",argc,argv);
22     app = gnome_app_new("setgc","Setting GdkGC Values");
23     gtk_signal_connect(GTK_OBJECT(app),"delete_event",
24         GTK_SIGNAL_FUNC(eventDelete),NULL);
25     gtk_signal_connect(GTK_OBJECT(app),"destroy",
26         GTK_SIGNAL_FUNC(eventDestroy),NULL);
27
28     area = gtk_drawing_area_new();
29     gtk_widget_set_usize(area,WIDTH,HEIGHT);
30     gnome_app_set_contents(GNOME_APP(app),area);
31     gtk_signal_connect(GTK_OBJECT(area),"event",
32         GTK_SIGNAL_FUNC(eventDraw),area);
33
34     gtk_widget_show_all(app);
35     gtk_main();
36     exit(0);
37 }
38 gboolean eventDraw(GtkWidget *widget,
39     GdkEvent *event,gpointer data) {
40     GtkGC *gc;
41     GtkWidget *area;
42
43     area = GTK_WIDGET(data);
```