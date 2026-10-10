![](bbox=[0.17, 0.13, 0.55, 0.34])

The minimum size of a fixed widget is fairly easy to calculate. The width is the maximum distance from the left side of the container to the right side of each widget. Likewise, the height is the maximum distance from the top of the container to the bottom of each widget.

Widgets can be moved from one place to another. You can do this whether or not the window is actively displayed. The call to `gtk_fixed_move()` to reposition a widget has the same arguments as `gtk_fixed_put()` but does to add a widget. For example, if the widget button is already added to the fixed container, this call moves it to a new location:

```
```c
gtk_fixed_move(GTK_FIXED(fixed),button,25,25);
```
```

# The Alignment Container

This container can be used to hold a single widget and to impose some control over the widget's size and position. The contained widget changes and positions to fit inside the current size and shape of the alignment container. The widget is positioned in the container a certain percentage of the distance from the top, and a certain percentage of the distance from the left side. Also, the widget is sized as a certain percentage of the width and height of the container.

This example program centers a GtkButton widget in an alignment container:

```
```c
1 / ** alignment.c ** /
2 #include <gname.h>
3
4 GtkWidget *makeAlignment();
5 gint eventDelete(GtkWidget *widget,
6            GdkEvent *event, gpointer data);
```
```