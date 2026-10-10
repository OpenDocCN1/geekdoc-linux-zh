```
```
75
76    GtkWidget *dialog;
       GtkWidget *button;
78
79    dialog = gtk_window_new(GTK_WINDOW_DIALOG);
       button = gtk_button_new_with_label("Close Dialog");
80    gtk_container_set_border_width(
            GTK_CONTAINER(dialog),20);
81    gtk_container_add(GTK_CONTAINER(dialog),button);
82    gtk_signal_connect(GTK_OBJECT(button),
83    gtk_container_add(GTK_CONTAINER(dialog),button);
            "clicked",
84            GTK_SIGNAL_FUNC(destroyDialog),
85            dialog);
86
87    gtk_widget_show(button);
88    gtk_widget_show(dialog);
89 }
90
91 void destroyPopup(GtkWidget *widget,gpointer data)
92 {
93    gtk_widget_destroy(GTK_WIDGET(data));
94 }
95 void destroyDialog(GtkWidget *widget,gpointer data)
96 {
97    gtk_widget_destroy(GTK_WIDGET(data));
98 }
```
```

![](bbox=[0.14, 0.53, 0.6, 0.62])

**Figure 3-16: A main window with two buttons**

![](bbox=[0.14, 0.65, 0.38, 0.68])

**Figure 3-17: A popup window with a Close button**

![](bbox=[0.14, 0.71, 0.38, 0.76])

**Figure 3-18: A dialog window with a Close button**

Lines 18 through 25 initialize GNOME, set the destroy callback, create a top-level window, and specify the margin around the window to be 20 pixels wide.

Line 26 creates a box widget, which is a special kind of widget called a container. A container widget is capable of organizing and displaying several widgets at once. This is necessary because the main window needs to display more than one widget.