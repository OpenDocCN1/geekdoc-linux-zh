# **Figure 4-13: Using boxes within boxes to position widgets**

![](bbox=[0.17, 0.13, 0.31, 0.26])

This layout is achieved by using a vertical box containing a single button at its top, a nested vertical box in the center, and a horizontal box at the bottom. This program creates the layout:

```
```cpp
1 /** boxnest.c **/
2 #include <gnome.h>
3
4 GtkWidget *makeBox();
5 GtkWidget *makeMiddleBox();
6 GtkWidget *makeBottomBox();
7 gint eventDelete(GtkWidget *widget,
                  GdkEvent *event,gpointer data);
8 gint eventDestroy(GtkWidget *widget,
                  GdkEvent *event,gpointer data);
9
10 int main(int argc,char * argv[])
11 {
12     GtkWidget *window;
13     GtkWidget *box;
14
15     gnome_init("boxnest","1.0",argc,argv);
16     window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
17     g_signal_connect(GTK_OBJECT(window),
18         "delete_event",
19         GTK_SIGNAL_FUNC(eventDelete),
20         NULL);
21     g_signal_connect(GTK_OBJECT(window),
22         "destroy"
23         GTK_SIGNAL_FUNC(eventDestroy),
24         NULL);
25
26     box = makeBox();
27     gtk_container_add(GTK_CONTAINER(window),box);
28     gtk_widget_show(box);
29
30     gtk_widget_show(window);
31     gtk_main();
32     exit(0);
33 }
34 GtkWidget *makeBox() {
35     GtkWidget *box;
36     GtkWidget *button;
```
```