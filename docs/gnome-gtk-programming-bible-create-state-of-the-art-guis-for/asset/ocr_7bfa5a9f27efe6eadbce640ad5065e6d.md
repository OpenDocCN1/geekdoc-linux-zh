A popup window is under the control of the window manager. However, no application is required to have a top-level window in order to be able to use one or more popup or dialog windows. This example has no top-level window, but is able to use a popup with a button to close the application:

```
```c
/** helloworld.c */
#include <gnome.h>

void buttonShutdown (GtkWidlet *widget, gpointer data);

int main (int argc, char *argv[])  {
    GtkWidget *popup;
    GtkWidget *button;

    gnome_init ("hellopopup", "1.0", argc, argv);

    popup = _gtk_window_new (GTK_WINDOW_POPUP);
    button = gtk_button_new_with_label ("Close");
    gtk_container_set_border_width (GTK_CONTAINER (popup), 20);
    gtk_container_add (GTK_CONTAINER (popup), button);
    gtk_signal_connect (GTK_OBJECT (button),
    "clicked", 
    GTK_SIGNAL_FUNC (buttonShutdown),
    NULL);

    gtk_widget_show (button);
    gtk_widget_show (popup);

    gtk_main ();
    exit (0);
}
void buttonShutdown (GtkWidlet *widget, gpointer data)  {
    exit (0);
}
```
```

Line 13 creates a popup widget and line 14 creates the push button that goes into it. The call to `gtk_container_add()` on line 17 adds the push button to the popup widget, and line 18 assigns a callback method to the push button. Lines 22 and 23 display the popup window and the button as shown in Figure 3-14. The callback function beginning on line 28 simply exits the program with the call to `exit()` on line 30.

![](bbox=[0.17, 0.83, 0.59, 0.88])