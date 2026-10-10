
# The Applet Menu

Selecting an applet with the right mouse button brings up the menu shown in Figure 15-3.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_470_0.png)

The default menu has two selections—the applet can be removed from the panel or it can be moved to another location. You can add entries to the menu and assign callbacks to them. The following applet adds two entries to its menu, resulting in the menu shown in Figure 15-4.

```c
/** menu_applet.c **/
#include <gnome.h>
#include <applet-widget.h>

#define APPLETNAME "menu-applet"
#define VERSION "1.0"

void changeCallback(AppletWidget *applet,GtkLabel *label);
void aboutCallback(AppletWidget *applet,GtkLabel *label);

int main(int argc,char *argv[])
{
    GtkWidget *applet;
    GtkWidget *label;

    applet_widget_init(APPLETNAME,VERSION,
                     argc,argv,
                     NULL,0,NULL);

    applet = applet_widget_new(APPLETNAME);

    label = gtk_label_new("Menu\nApplet");
    gtk_widget_set_usize(label,48,48);
    applet_widget_add(APPLET_WIDGET(applet),label);

    gtk_widget_show_all(applet);

    applet_widget_register_callback(
               APPLET_WIDGET(applet),
               "Change","Change",
               (AppletCallbackFunc)changeCallback,label);
    applet_widget_register_stock_callback(
               APPLET_WIDGET(applet),
               "about",GNOME_STOCK_MENU_ABOUT,
               "About...",
               (AppletCallbackFunc)aboutCallback,label);

    applet_widget_gtk_main();
    exit(0);
}

void changeCallback(AppletWidget *applet,GtkLabel *label)
{
    int i;
    static GtkStyle *oldStyle = NULL;
    static GtkStyle *newStyle = NULL;
    static int change = TRUE;

    if(oldStyle == NULL) {
        oldStyle = gtk_widget_get_style(GTK_WIDGET(label));
        newStyle = gtk_style_copy(oldStyle);
        for(i=0; i<5; i++) {
            newStyle->fg[i] = oldStyle->light[i];
            newStyle->fg_gc[i] = oldStyle->light_gc[i];
        }
    }

    if(change)
        gtk_widget_set_style(GTK_WIDGET(label),newStyle);
    else
        gtk_widget_set_style(GTK_WIDGET(label),oldStyle);
    change = !change;
}

void aboutCallback(AppletWidget *applet,GtkLabel *label)
{
    GtkWidget *aboutBox;
    const gchar *writtenBy[] = {
        "Arthur Griffith",
        "George Spelvin",
        NULL
    };
    aboutBox = gnome_about_new("Menu Applet",
        "0.0",
        "(c) 1999 the Free Software Foundation",
        writtenBy,
        "This applet demonstrates the code "
        "necessary to add items to the menu. "
        "The added menu items can be simple text "
        "or it can be one of the stock items",
        NULL);
    gtk_widget_show(aboutBox);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_471_0.png)

Lines 16 through 26 perform the standard set of tasks necessary to create a widget that displays a `GtkLabel` with text.

A new menu item is added with the call to `applet_widget_register_callback()` on line 28. Of the two name strings on line 30, the first one is the internal widget name and the second is the text that appears on the menu. The last two arguments are the callback function and the data that is to be passed to it (in this case, the address of the label widget).

Another menu item is added—using one of the stock menu definitions—by the call to `applet_widget_register_stock_callback()` on line 32. The quoted string on line 34 is to be the internal name of the widget. Also on line 34 is the defined constant identifying a stock menu item. The quoted string on line 35 is the text that appears on the menu. The last two arguments, on line 36, specify the callback function and the data to be passed to it.

The callback function `changeCallback()` beginning on line 42 changes the color of the text on the applet window. It does this by keeping a copy of the applet’s `GtkStyle`, and also making and keeping a copy of the `GtkStyle` with the foreground color changed. The loop starting on line 52 changes the copy of the `GtkStyle` so the foreground settings are the same as the light settings. The Boolean toggle change is tested on line 58; the result of the test determines which `GtkStyle` is used. Line 62 reverses the toggle for the next time this function is called.

The callback function `aboutCallback()` beginning on line 64 displays a standard About box for the applet.

## Panel Orientation

Whenever an applet is displayed in a panel, the panel adjusts its size to make sure the entire applet window is displayed. This has the disadvantage that, for large applets, the panel can expand to take up quite a bit of real estate on the desktop. One solution to this is to reshape your applet window smaller, either in the vertical or horizontal position depending on the orientation of the panel. The following applet detects the orientation and position of the panel and adjusts itself accordingly.

```c
/** orient_applet.c **/
#include <gnome.h>
#include <applet-widget.h>
#include <stdio.h>

#define APPLETNAME "orient-applet"
#define VERSION "1.0"

void orientEvent(GtkWidget *widget, PanelOrientType orient,
                 GtkWidget *abel);

int main(int argc,char *argv[])
{
    GtkWidget *applet;
    GtkWidget *label;

    applet_widget_init(APPLETNAME,VERSION,
    argc,argv,
    NULL,0,NULL);

    applet = applet_widget_new(APPLETNAME);

    label = gtk_label_new("");
    gtk_widget_set_usize(label,48,48);

    gtk_signal_connect(GTK_OBJECT(applet),"change_orient",
    GTK_SIGNAL_FUNC(orientEvent),label);

    applet_widget_add(APPLET_WIDGET(applet),label);
    gtk_widget_show_all(applet);
    applet_widget_gtk_main();
    exit(0);
}

void orientEvent(GtkWidget *widget,PanelOrientType orient,
    GtkWidget *label)
{
    gchar *text;

    switch(orient) {
    case ORIENT_UP:
        gtk_widget_set_usize(label,100,48);
        text = "Horizontal Bottom";
        break;
    case ORIENT_DOWN:
        gtk_widget_set_usize(label,90,48);
        text = "Horizontal Top";
        break;
    case ORIENT_LEFT:
        gtk_widget_set_usize(label,48,48);
        text = "Vertical\nRight";
        break;
    case ORIENT_RIGHT:
        gtk_widget_set_usize(label,48,48);
        text = "Vertical\nLeft";
        break;
    }
    gtk_label_set_text(GTK_LABEL(label),text);
}
```

The applet is created on lines 17 through 21 and, for its display window, a label is created and sized on lines 23 and 24.

On line 26, a call is made to `gtk_signal_connect()` that connects the signal named "`change_orient`" to the applet widget. This is a special signal defined inside `AppletWidget`. It is set to call the function `orientEvent()` whenever the panel changes its orientation. Lines 29 and 30 insert the label into the applet, and put the applet on display in the panel. The "`change_orient`" callback is made when the applet first appears on the panel.

The callback function `orientEvent()` beginning on line 34 changes the text and resizes the label to reflect the current orientation. The second argument, the `PanelOrientType`, is used in the switch statement on line 40 to select the orientation. The orientation names refer to the direction from the applet to the root window. That is, `ORIENT_UP` means the applet is on the bottom of the window with the root window above it. `ORIENT_LEFT` means the applet is on the right with the root window to its left.

The size of the label is modified to fit the orientation. If the applet is in a panel at the top or bottom of the screen, the label is widened to accommodate a single line of text. If the applet is on one of the sides, the label is narrowed and the line of text is split.

## Summary

An applet is a GNOME program with a small main window, and that window appears inside the GNOME panel. An applet derives its special abilities from the `AppletWidget`, which acts as a presentation layer for the applet's main window. This chapter discussed the parts and options, in building an applet:

- The functions that define and control an applet closely resemble the ones that define and control an application. The function `applet_widget_init()` is used in place of `g_app_init()`. The function `applet_widget_new()` is used in place of `g_app_new()`. The function `applet_widget_gtk_main()` is used in place of `gtk_main()`.
- An applet can be a mouse-sensitive button that serves as the entrance to a much larger program, but it also can be used to display short messages and simple information.
- An applet can add any number of members to its menu.
- An applet can resize and reorient itself to fit with its current environment.

The following chapter explains how you can make inter-process communications available at the GUI interface. The mouse can be used to drag objects from one location to another. The tricks required to package an object and transfer its ownership from one application to another are all built into the GNOME API.
