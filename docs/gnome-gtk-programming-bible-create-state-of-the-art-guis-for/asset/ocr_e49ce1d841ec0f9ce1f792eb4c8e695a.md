```
22
gtk_widget_show_all(applet);
24
25
applet_widget_gtk_main();
26
27
exit(0);
28
)
```

Because the characteristics of an applet normally are not part of a GNOME or GTK+ application, the applet header file is not included by gnome.h. Line 3 includes the header file applet-widget.h, which contains the definition AppletWidget and its associated functions. The inheritance of the applet widget looks very much like the inheritance of any other displayable widget:

```
AppletWidget->GtkPlug->GtkWindow->GtkBin->GtkContainer->
GtkWidget->GtkObject
```

The call to applet_widget_init() on line 13 initializes the session. This function does for the applet the same thing that gnome_init() does for a GNOME application. The AppletWidget itself is created on line 17 by the call to applet_widget_new(). The AppletWidget inherits from GtkContainer, so it can contain any displayable widget you want to insert into it.

Lines 19 through 22 create a button and add it to the applet widget as the item to be displayed. The button is sized 48x48 to match some of the other applets commonly included on the panel. However, the panel automatically resizes itself to accommodate the largest contained applet, so no matter what size you choose, your applet is visible.

Line 23 calls gtk_show_all() to display the applet and all of its children. Just like any other container widget, the AppletWidget shows itself and all the widgets it contains. The main loop applet_widget_gtk_main() is called on line 25. This is the applets version of gtk_main(). It does not return until the program ceases execution.

Whenever this program is run, it appears as an applet on the panel as shown in Figure 15-1. The button responds to the mouse, but because no callback activity is defined for the button, no action is taken.

![](bbox=[0.15, 0.86, 0.35, 0.91])

The applet modules are not a part of the standard set of GNOME and GTK+ libraries, and need to be included separately. The following is a make file that compiles and links this program.

```
CC=gcc
LDFLAGS=`gnome-config --libs gnomenu` -lpanel_applet -lgnomba
CFLAGS=`gnome-config --cflags gnomenu`
```