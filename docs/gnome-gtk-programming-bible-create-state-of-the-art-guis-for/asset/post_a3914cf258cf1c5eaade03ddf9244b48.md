
the exact vertical center. For most applications, you simply divide the height in half and use the base line at that point. If, however, you want the exact center, you need to take into account the off-center nature of the base line, as is done on line 191.

The horizontal positioning is set in the switch statement beginning on line 197. If the string is to be on the left, you simply place the origin at the left margin by setting x to zero. Line 205 positions the string on the right side by setting the value of x to the width of the window—minus the length of the string. Line 202 positions the string in the horizontal center by halving the width of the window and subtracting half of the length of the string.

Each of the buttons has its own callback on lines 217 through 245. Each callback sets the position indicator in the context. Also, each callback calls gdk_window_clear_area(e) to erase the drawing area and issues an “expose” event that causes eventDraw() to draw the new string on the window.

## Summary

Of all the elements displayed as part of a graphical user interface, the eye is most critical of letters, numbers, and punctuation. We have been reading and writing all of our lives, so our brain instantly recognizes characters and patterns of characters. Some character fonts appear to be nice and friendly, even attractive, while some appear to be clunky or stiff. The actual difference, between one we like and one we don’t like, can be very small. Even though characters normally are displayed as very small items in a window, it is easy for us to instantly recognize the details of its shape. This preconceived notion of the appearance of characters is why a font can seem so dramatic to us. In this chapter, the fundamentals of font manipulation were described:

- Each font is stored in its own file, so it is easy to add new fonts or delete old ones.
- Your application can refer to a specific font by its exact name; or it can select a font by using descriptive terms, such as the font family and point size.
- There is a standard set of metrics that you can use to position text in the window, and to determine the size of the displayed text.
- The GnomeFontPicker widget can be included in your program to enable the user to pick a font.

The next chapter takes a peek inside the widgets. Every widget contains a displayable window and is capable of responding to the mouse and keyboard. But there is much more to a widget. If you know how the widgets work, you will be able to manipulate them into doing what you want them to do. Besides, you may find that some functions of your application can be best written as a widget.

# Widget Tricks

![](img/8bcc1ba72831c7d67cfc8b395deab95f_442_0.png)

This chapter deals with widgets. Every displayable object in GNOME has, as its parent or grandparent, a GtkWidget object. There are some settings and adjustments that can be made into a widget. A widget is a very sophisticated software object in the way it keeps track of information, passes events forward to the application program, and knows how and when to update itself on the display.

Because all GNOME displayable objects have the same heritage, they are all widgets. Every widget has certain things in common with every other widget. This has the great advantage that any widget-level function that works for one widget works for another. For example, it is possible to make color and font settings at the widget level. There also are standard ways to change the size and position of a widget; the function calls are exactly the same whether the widget is a menu, a label, a drawing area, or something that was made up especially for the application.

## Exploring a Widget

Through inheritance, every widget in your program is a combination of parts that include a GtkObject, a GtkWidget, and, possibly, other widgets. For example, a GtkButton widget is built on top of a GtkBin widget, which is built on top of a GtkContainer widget, which is built on top of a GtkWidget, which is built on top of a GtkObject. This form of inheritance gives GTK+ its object-oriented characteristics. The GNOME widgets are further extensions of GTK+ widgets, so they also have this same object-oriented form. Chapter 18 describes the internal structure in detail.

Every widget has some internal settings that an application program can read or write. And, because every widget is an aggregate — sort of a stack of different widgets — it was necessary to devise an interface that your application can use to address a specific value inside a specific widget found in the inheritance tree. To read or write one of these values, your program needs to know the name of the widget, the name of the value, and the data type.

## In This Chapter

- Exploring the internal construction of a widget
- Communicating with a widget
- Commanding a widget to appear, disappear, and reshape itself
- Customizing a widget by specifying a collection of style characteristics

![](img/8bcc1ba72831c7d67cfc8b395deab95f_443_0.png)

There are a number of terms used to refer to these program-accessible values stored in a widget. They are known as object arguments, widget parameters, settings, values, options, and so on. However, the term argument probably fits best because the three letters “arg” appear internally in GTK+ and GNOME widgets.

The following program displays the list of argument names and types for a widget.

```c
/** argnames.c **/
#include <gnome.h>

void showArgs(GtkWidget *);

int main(int argc, char *argv[])
{
    GtkWidget *clist;
    GtkWidget *window;

    gnome_init("argnames", "1.0", argc, argv);
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);

    clist = gtk_clist_new(4);
    showArgs(clist);

    exit(0);
}

void showArgs(GtkWidget *widget)
{
    GkType objectType;
    GtkArg *arg;
    gint argCount;
    guint32 *argFlags;
    GtkArgInfo *argInfo;
    gint i;

    objectType = GTK_OBJECT_TYPE(widget);

    while(objectType != GTK_TYPE_INVALID) {
        arg = gtk_object_query_args(objectType,
                 &argCount);
        g_print("%s:\n", gtk_type_name(objectType));
        for(i=0; i<argCount; i++) {
            gtk_object_arg_get_info(objectType,
                  arg[i].name, &argInfo);
            g_print("  \"%s\" %s",
                  argInfo->name,
                  gtk_type_name(argInfo->type));
            if((argInfo->arg_flags & GTK_ARG_READWRITE)
              == GTK_ARG_READWRITE)
              g_print("  Read/Write");
            else if(argInfo->arg_flags & GTK_ARG_READABLE)
              g_print("  Readonly");
            else if(argInfo->arg_flags & GTK_ARG_WRITABLE)
              g_print("  Writenly");
            if(argInfo->arg_flags & GTK_ARG_CONSTRUCT_ONLY)
                g_print(" Not wrtable after realized");
            g_print("\n");
        }
        g_free(arg);
        g_free(argflags);
        objectType = gtk_type_parent(objectType);
    }
}
```

This program has a minimal mainline—all we require is that a widget be created and passed to the showArgs() function to list the available settings. On line 11, a GtkCList widget is created; on line 12, it is used in a call to showArgs(). The showArgs() function, beginning on line 19, contains a nested loop. The outer loop executes once for each widget in the hierarchy. The inner loop executes once for each argument found in that widget.

To start things off, you need to get the object type. You do this with the macro GTK_OBJECT_TYPE() on line 28. At the top of the widget loop, on line 31, a call is made to gtk_object_query_args()—using the object type—to retrieve an array of GtkArg structs, a count of the number of members in the array, and a set of flags. The g_print() function call on line 33 calls gtk_type_name() to extract the type name from the object and print it. At the bottom of the outer loop, on lines 51 and 52, the GtkArg array and the flags deallocated because they were dynamically allocated.

The inner loop, beginning on line 34, executes once for each argument found in the widget. On line 35, a call is made to gtk_object_arg_get_info() using the type of the object and the name of the argument. As a return value, the function stores an address in the GtkArgInfo struct pointer defined on line 25. This structure contains all we need to know about the argument.

The test on line 40 determines whether both the GTK_ARG_READABLE and GTK_ARG_WRITABLE flags are set. If both are not set, the code checks to see which one is set. The test on line 47 catches the condition of an argument being wrtable, but only before a widget has been realized. The output from this program looks like this:

GtkCList::
  "n_columns" guint Read/Write (Not writable after realized)
  "shadow_type" GtkShadowType Read/Write
  "selection_mode" GtkSelectionMode Read/Write
  "row_height" guint Read/Write
  "reorderable" gbool Read/Write
  "titles_active" gbool Read/Write
  "use_drag_icons" gbool Read/Write
GtkContainer::
  "border_width" guint Read/Write
  "resize_mode" GtkResizeMode Read/Write
  "child" GtkWidget Write/only
GtkWidget::
  "name" GtkString Read/Write
