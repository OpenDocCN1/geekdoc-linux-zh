A menu item can be disabled and enabled dynamically. When it is disabled, it appears grayed-out and does not respond to the mouse. This technique often is used to prevent user access to functions that have no meaning under the current circumstances. For example, the Save button can be disabled if there is no data available to be written to disk.

The following program has a simple three-button menu. The top and bottom buttons can be used to enable and disable the one in the middle.

```
```
1 /** mdisable.c **/
2 #include <gnome.h>
3
4 static void dummyCallback(GtkObject *gpointer);
5 static void enableProperties(GtkObject *gpointer);
6 static void disableProperties(GtkObject *gpointer);
7 gint eventDelete(GtkWidget *widget,
    GdkEvent *event,gpointer data);
9 gint eventDestroy(GtkWidget *widget,
    GdkEvent *event,gpointer data);
10
11
12 #define PROP_INDEX 1
13 GnomeUIInfo enableMenu[] = {
    GNOMEUIINFO_MENU_NEW_ITEM("Enable Properties",
    "Enable the Properties menu selection",
    enableProperties,NULL),
    GNOMEUIINFO_MENU_PROPERTIES_ITEM(dummyCallback,NULL),
    GNOMEUIINFO_MENU_NEW_ITEM("Disable Properties",
    "Disable the Properties menu selection",
    disableProperties,NULL),
    GNOMEUIINFO_END
};

GnomeUIInfo mainMenu[] = {
    GNOMEUIINFO_SUBTREE("Enable/Disable",enableMenu),
    GNOMEUIINFO_END
};

int main(int argc,char *argv[])
{
    GtkWidget *app;

    gnome_init("mdisable","1.0",argc,argv);
    app = gnome_app_new("mdisable","Menu Disable");
    gtk_window_set_default_size(GTK_WINDOW(app),200,100);
    gtk_signal_connect(GTK_OBJECT(app),"delete_event",
    GTK_SIGNAL_FUNC(eventDelete),NULL);
    gtk_signal_connect(GTK_OBJECT(app),"destroy",
```
```