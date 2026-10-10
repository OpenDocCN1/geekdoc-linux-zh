
window, and it responds to the mouse buttons by displaying the name of the selected bar graph. Figure 18-1 shows an example of its output.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_509_0.png)

The AgBargraph widget has these characteristics:

- It is object-oriented. It has special functions that are called to create the widget and, at the end of its life, to destroy it. This way, allocated system resources are released automatically when the widget is deleted. Access to the widget control values is made through function calls.
- As with all widgets, AgBargraph is very easy to use as part of your application. It is only necessary to create the widget and attach it to a parent window that displays it.
- Your application can create any number of instances of this widget. Each instance operates independently, but uses the same set of functions for configuration and control.
- AgBargraph inherits all of the capabilities of GtkWidget. This enables it to select the events to be received simply by asking for them. Because GtkWidget takes care of the underlying structure of AgBargraph, most of the code deals with setting values and drawing the display.
- AgBargraph automatically resizes itself to fit the size allocated to it. It redraws itself when it becomes exposed. Additionally, AgBargraph changes its background color when the mouse enters its window. Clicking one of the bars in the graph causes its name to display.
- You can add new bar-graph information at any time — either before the widget is realized or while it is being displayed.

## Using the AgBargraph Widget

The following program creates and displays an AgBargraph widget.

```c
/** showbargraph.c **/
#include <gnome.h>

#include "agbargraph.h"

GtkWidget *makeBox();
gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data);

int main(int argc, char **argv)
{
    GtkWidget *window;
    GtkWidget *agbargraph;

    gnome_init("AgBargraph", "1.0", argc, argv);
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_container_set_border_width(GTK_CONTAINER(window), 25);
    gtk_signal_connect(GTK_OBJECT(window), "delete_event", GTK_SIGNAL_FUNC(eventDelete), NULL);
    gtk_signal_connect(GTK_OBJECT(window), "destroy", GTK_SIGNAL_FUNC(eventDestroy), NULL);

    agbargraph = ag_bargraph_new();
    ag_bargraph_add(AG_BARGRAPH(agbargraph), "Pickle", 82);
    ag_bargraph_add(AG_BARGRAPH(agbargraph), "Onion", 39);
    ag_bargraph_add(AG_BARGRAPH(agbargraph), "Herring", 54);
    ag_bargraph_add(AG_BARGRAPH(agbargraph), "Sardine", 12);
    ag_bargraph_add(AG_BARGRAPH(agbargraph), "Other", 90);

    gtk_container_add(GTK_CONTAINER(window), agbargraph);
    gtk_widget_show_all(window);
    gtk_main();
    exit(0);
}

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data) {
    return(FALSE);
}

gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data) {
    gtk_main_quit();
    return(0);
}
```

This is a very simple GNOME application program. On lines 17 through 24, the system is initialized, a window is created, and the callbacks are set up to close the application.

Lines 26 through 31 create the AgBargraph widget and immediately insert five bar graphs into it. The call to `ag_bargraph_new()` creates a new and empty widget. Each call to `ag_bargraph_add()` defines a new bar to be displayed by giving it a name and a value from 0 to 100.

Line 33 calls `gtk_container_add()`, which inserts the widget into the window’s container. The call to `gtk_widget_show_all()` realizes all the widgets in the tree, including the AgBargraph widget.

## The AgBargraph Header File

Each widget has its own header file to define the structures, constants, and functions that are included with the widget. The same header file is included by the application program using the widget, and by the C source code of the widget itself. The following is the header file for the AgBargraph widget.

```c
/* agbargraph.h */

#ifndef __AG_BARGRAPH_H
#define __AG_BARGRAPH_H

#include <gtk/gtk.h>
#include <gtk/gtkwidget.h>

#ifdef __cplusplus
extern "C" {
#endif

#define AG_BARGRAPH(obj) \
GTK_CHECK_CAST(obj,ag_bargraph_get_type(),AgBargraph)
#define AG_BARGRAPH_CLASS(klass) GTK_CHECK_CLASS_CAST( \
klass,ag_bargraph_get_type(),AgBargraphClass)
#define AG_IS_BARGRAPH(obj) \
GTK_CHECK_TYPE(obj,ag_bargraph_get_type())

typedef struct _AgBargraph AgBargraph;
typedef struct _AgBargraphClass AgBargraphClass;
typedef struct _AgBargraphBar AgBargraphBar;

struct _AgBargraph {
GtkWidget widget;
GdkColor *outside_color;
GdkColor *inside_color;
gint maximum_value;
gint bar_count;
gboolean contains_pointer;
AgBargraphBar *bars;
gchar *show_text;
GdkFont *text_font;
};

struct _AgBargraphClass {
GtkWidgetClass parent_class;
};

struct _AgBargraphBar {
gchar *name;
gint value;
GdkGC *gc;
gint x_right;
gint x_left;
};

#define AG_BARGRAPH_MAXIMUM 100

GtkWidget *ag_bargraph_new(void);
guint ag_bargraph_get_type(void);
void ag_bargraph_add(AgBargraph *agbargraph, gchar *name, gint value);

#ifdef __cplusplus
};
#endif

#endif /* __AG_BARGRAPH_H */
```

The preprocessor conditionals on lines 3, 4, and 59 prevent the header file from inadvertently being included more than once. This widget uses *GtkWidget* as its parent type, so it is necessary to include *gtk.h* and *gtkwidget.h*—as is done on lines 6 and 7. It is possible to use this widget in a C++ program because the compiler is notified that everything between the braces on lines 10 and 57 is to be compiled as C, not C++. A C++ compiler always defines *__cplusplus*.

The macro *AG_BARGRAPH*, defined on line 13, attempts to cast a pointer to an AgBargraph widget pointer—if the pointer is the wrong type, the cast fails and an error message is emitted. In the same manner, the macro *AG_BARGRAPH_CLASS* defined on line 15 casts a pointer to an AgBargraphClass pointer. The macro *AG_IS_BARGRAPH* defined on line 17 returns either *TRUE* or *FALSE* depending on whether the object passed to it is an AgBargraph widget.

You can see more of the naming convention in the typedef statements on lines 20 through 22. The structs are defined with a leading underscore, and then the typedef is used to assign the name. Using *typedef* to define the names of the structs has the advantage of allowing declarations of this form:

```c
AgBargraph *bargraph;
```

The struct for the AgBargraph is defined on lines 24 through 34. On line 25, the first thing at the top of the AgBargraph struct is a GtkWidget struct. This means that a pointer to an AgBargraph struct also can be created as a pointer to a GtkWidget struct—both structs begin at the same address. This is why a pointer to an AgBargraph can be cast to a pointer to a GtkWidget. The top of the GtkWidget struct is declared this way:

```c
struct GtkWidget {
  GObject;
  guint16 private_flags;
  ...
};
```

Because the first thing in a GtkWidget struct is a GObject, all three of these types share the same starting address. This means that an AgBargraph pointer can be cast to a GtkWidget pointer or a GObject pointer, and any GtkWidget pointer can be cast to a GtkWidget pointer or a GObject. This technique is used in all of the objects of GTK+ and GNOME; the parent object of them all is GObject. GObject is the parent, or grandparent, of all other objects—it inherits from no other object.

The fields defined on lines 26 through 33 are specific to a single instance of the AgBargraph widget. For example, the bar_count value is incremented each time a new bar is added to the widget, so it can be a different value for each instance of AgBargraph. It is this trick of storing all of the variable information in a single struct that makes it so easy to create and manage multiple instances. The class struct _AgBargraphClass on line 36 holds any fields that are defined for the entire class of objects, instead of just for a single instance. For example, the text_font defined on line 33 can be used to set the font independently for each instance of AgBargraph. If the text_font field were included in the class struct instead, changing it once would apply the change to all instances of the widget. In this example, the AgBargraphClass struct contains only the class struct of its parent class.

The struct _AgBargraphBar on line 40 contains the data required to define a single bar. Each time a new bar is added to the widget, a structure of this type is added to the array named bars on line 31.

The function prototypes are defined on lines 50 through 53. These are the nonstatic functions—the ones an application program calls. There is always at least one “new” function so the object can be created, and one “type” function so the object can be identified by a unique type ID number. Normally, there are several other functions that can be used to control the widget. In this example, the only customizing function is ag_bargraph_add(), which adds a new bar to the widget. Some functions can be designed to operate on the entire class, while others operate on one specific instance. A function that operates on a specific instance has a widget pointer as its first argument (so the function knows which instance to operate on), while a class-level function needs no such pointer because its operations apply to the entire class.
