
The variable `helloauto_SOURCES` specifies the source files that are used to build the binary output file named `helloauto`. Using this information, the make file is generated to check all of these files for dependencies.

The variable `helloauto_LDADD` specifies a list of libraries that are searched to resolve external references in the files that make up `helloauto`.

You can add other programs to the same file by adding its name to the list in `bin_PROGRAMS`, and adding a new `SOURCES` and `LDADD` entry for it. Also, if you wish to have subdirectories of source files, you can use a `SUBDIRS` definition to point to the right directory. This means that to add a new directory to your source tree, you simply create a `Makefile.am` file in the new source directory and add a `SUBDIRS` entry in the `Makefile.am` of the parent directory.

## Running the `autogen.sh` Script

There are two steps required to compile everything. First, the script is run from your root development directory like this:

```
autogen.sh
```

This adds a number of files to your root development directory. Exactly what files are added depends largely on the settings and choices you made earlier. For example, if you use `ALL_LINGUAS` to set up some translation, the subdirectories `po` and `intl` are created to hold translation strings.

After the script runs, simply enter:

```
make
```

This command compiles and links everything in the entire directory tree. If you are in any of the source subdirectories, entering `make` only compiles that current directory and those below it.

The make files compare the dates on the source to the dates on the object files, so if you compile again, only the changed files are included. However, you can force a complete recompilation by removing the object files. To delete all the object files, along with any other files that are created during the compile, enter:

```
make clean
```

As you develop your application and add new source files, you will need to update the appropriate `Makefile.am` file and then execute `autogen.sh` to include the new source file.

After you have a successful compile, you can install the executable files with:

```
make install
```

## Summary

The setup to get automatic compilation to work is a bit involved, but the rewards come later as you develop your software. All of the dependencies among your source files are tracked automatically, and a correct and complete set of commands is used to compile and link your programs. As explained in detail in this chapter, the following is a list of the steps to take:

- Create a development directory containing the appropriate collection of files and directories. It also should include a copy of the macros distributed with the GNOME development software.
- Create the `configure.in` file that contains, by using macros, a basic description of your project. Also, create the `acconfig.h` file to be used as a template in creating `config.h`.
- Create a simple `autogen.sh` script you can use to find the dependencies and generate the make files.
- Create a `Makefile.am` file listing the names of the source files to be used as input, and the names of the object files to be generated. One of these appears in every directory in the development tree.

The next two chapters are for reference. Chapter 21 contains a list of the widgets of GTK+, and Chapter 22 contains a list of the widgets of GNOME. Many of these have been used in programs earlier in the book but, for those that haven't, there are small examples.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_560_0.png)

# The Widgets of GTK+

## In This Chapter

This chapter provides an alphabetical listing of the GTK+ objects. Most of the objects are widgets, but there are a few objects that inherit directly from the base class `GtkObject`. Each entry includes the inheritance and all of the functions that are available to your application.

- Listing and explaining the widgets, and other objects, of GTK+
- Determining all of the signals and functions that are defined for an object
- Determining all of the inherited functions available in an object by examining its inheritance
- Determining the enum constants defined for passing configuration settings to the functions
- Starting you off by including a simple example of each object

You can use any widget as the base to create another widget, but not all widgets can be displayed—some are intended for use only as base classes. If a class does not have a function name that ends in `_new` (or has `_new_` somewhere in its name) and returns a pointer to a newly created widget, you can use it only as a base class.

The example code included with each widget is a function that creates the displayable widget and returns a pointer to it. The mainline of all the programs that display the widgets are very much alike. The following example is the one used for the `GtkEntry` widget:

```c
/** xgtkentry.c **/
#include <gnome.h>

gint eventDelete (GtkWidget *widget,
                  GdkEvent *event, gpointer data);
gint eventDestroy (GtkWidget *widget,
                   GdkEvent *event, gpointer data);
static GtkWidget *makeWidget();

int main(int argc, char *argv[])
{
    GtkWidget *app;
    GtkWidget *widget;

    gnome_init ("xgtkentry", "1.0", argc, argv);
    app = gnome_app_new("xgtkentry", "GtkEntry");
    gtk_container_set_border_width(GTK_CONTAINER(app), 20);
    gtk_signal_connect(GTK_OBJECT(app), "delete_event",
                       GTK_SIGNAL_FUNC(eventDelete), NULL);
    gtk_signal_connect(GTK_OBJECT(app), "destroy",
                       GTK_SIGNAL_FUNC(eventDestroy), NULL);

    widget = makeWidget();
    gnome_app_set_contents(GNOME_APP(app), widget);
    gtk_widget_show_all(app);
    gtk_main();
    exit(0);
}

gint eventDelete(GtkWidget *widget,
                 GdkEvent *event, gpointer data) {
    return(FALSE);
}

gint eventDestroy(GtkWidget *widget,
                  GdkEvent *event, gpointer data) {
    gtk_main_quit();
    return(0);
}

static GtkWidget *makeWidget()
{
    GtkWidget *widget;

    widget = gtk_entry_new_with_max_length(40);
    gtk_entry_set_text(GTK_ENTRY(widget), "Edit me!");
    return(widget);
}
```

There may be a minor difference here and there. For example, widgets that wrap themselves in their own top-level window, and thus control their own actions, do not return a pointer. If you examine the source code on the CD, or downloaded from the web site, you see the complete program for each example—not just the snippets shown in this chapter.

## GtkAccelLabel

This label widget reads and displays the accelerator key from another widget. It displays the text, if any, used to create it until it is assigned a widget with an accelerator key.

### Inheritance

`GtkAccelLabel` -> `GtkLabel` -> `GtkWMisc` -> `GtkWidget` -> `GtkObject`

### Functions

```c
guint gtk_accel_label_get_accel_width(
              GtkAccelLabel *accel_label);
GtkType gtk_accel_label_get_type(void);
GtkWidget *gtk_accel_label_new(const gchar *string);
boolean gtk_accel_label_refetch(GtkAccelLabel *accel_label);
void gtk_accel_label_set_accel_widget
     (GtkAccelLabel *accel_label, GtkWidget *accel_widget);
```

### Signals

- `"changed"` `void cb(GtkWidget *, gpointer)`
- `"value_changed"` `void cb(GtkWidget *, gpointer)`

The following example displays the window shown in Figure 21-1.

```c
static GtkWidget *makeWidget()
{
    GtkWidget *widget;

    widget = gtk_accel_label_new("Label String");
    return(widget);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_562_0.png)

## GtkAdjustment

This object stores geometry information, such as upper and lower bounds, step and page increments, and the size of a page. Other objects use a GtkAdjustment object to store their internal dimension settings. It also is passed as an argument to specify geometry.

A call to `gtk_adjustment_changed()` issues a `"changed"` signal; a call to `gtk_adjustment_value_changed()` issues a `"value changed"` signal, if there is a change in a value since the last signal was emitted.

### Inheritance

`GtkAdjustment` -> `GtkData` -> `GtkObject`

### Functions

- `void gtk_adjustment_changed(GtkAdjustment *adjustment)`
- `void gtk_adjustment_clamp_page(GtkAdjustment *adjustment, gfloat lower, gfloat upper)`
- `GtkType gtk_adjustment_get_type(void)`
- `GtkObject *gtk_adjustment_new(gfloat value, gfloat lower, gfloat upper, gfloat step_increment, gfloat page_increment, gfloat page_size)`
- `void gtk_adjustment_set_value(GtkAdjustment *adjustment, gfloat value)`
- `void gtk_adjustment_value_changed(GtkAdjustment *adjustment)`
