```
```
30       gtk_signal_connect(GTK_OBJECT(button), "clicked",
                           GTK_SIGNAL_FUNC(grabMouse), window);

32
33       button = gtk_button_new_with_label("Ungrab Mouse");
34       gtk_box_pack_end(GTK_BOX(box), button, FALSE, FALSE, 0);
35       gtk_signal_connect(GTK_OBJECT(button), "clicked",
                           GTK_SIGNAL_FUNC(ungrabMouse), NULL);
36
37
38       gtk_container_add(GTK_CONTAINER(window), box);
39       gtk_widget_show_all(window);
40       gtk_main();
41       exit(0);
42 }
43 void  grabMouse(GtkWidget *widget, GtkWidget *containWidget)
44 {
45       GdkWindow *window = containWidget->window;
46       GdkCursor *cursor = gdk_cursor_new(GDK_CROSSHAIR);
47       gdk_pointer_grab(window,
48                       TRUE,
49                       (GdkEventMask)0,
50                       window,
51                       cursor,
52                       GDK_CURRENT_TIME);
53 }
54 void ungrabMouse(GtkWidget *widget, gpointer data) {
55       if(gdk_pointer_is_grabbed())
56              gdk_pointer_ungrab(GDK_CURRENT_TIME);
57 }
58
59 gint eventDelete(GtkWidget *widget,
60                 GdkEvent *event, gpointer data) {
61       return(FALSE);
62 }
63 gint eventDestroy(GtkWidget *widget,
64                 GdkEvent *event, gpointer data) {
65       if(gdk_pointer_is_grabbed())
66              gdk_pointer_ungrab(GDK_CURRENT_TIME);
67       gtk_main_quit();
68       return(0);
69 }
```
```

A vertical box container is constructed on line 26. Lines 28 through 36 create a pair of buttons, add them to the vertical box, and assign a callback to each one of them. The callback that grabs the mouse is named `grabMouse()` and the one that releases it is named `ungrabMouse()`. The connection to `grabMouse()` on line 31 uses the main window as the data to be passed to the function.

The callback function `grabMouse()` beginning on line 43 makes a call to the function `gdk_pointer_grab()` to limit the movement of the mouse to the rectangular area of a specified window.