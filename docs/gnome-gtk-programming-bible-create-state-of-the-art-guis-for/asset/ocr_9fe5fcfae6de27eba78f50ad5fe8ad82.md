# Create, Realize, Map, and Show

The following description is intended to be a conceptual overview of the birth, life, and death of widgets. Widgets can get a bit complicated, and there is a lot going on behind the curtain, so the exact process varies from one widget to another. There is more information on this in Chapter 18

When a widget is born and works its way up from a pattern of bits in memory to a graphic object appearing on the display, it goes through the process of being created, mapped, realized, and shown. Then, at the end of the widget’s life, it is hidden, unmapped, unrealized, and destroyed. But this is not a linear sequence. During the life of a widget, your application can move the widget back and forth between show and hide—causing it to appear and disappear. Also, to move a widget from one parent window to another, it can be unrealized and then realized again.

# Create and Destroy

Each widget has at least one `*new` function that you can use to create new instances of it. For example, `gtk_label_new()` can be used to create `GtkLabel` widgets and `gnome_about_new()` can be used to create new `GnomeAbout` widgets. When a widget is first created, it is an empty shell—its window hasn’t been created and it has no parent. Some other things must happen before it can be used.

When a widget is destroyed, all of its allocated memory is returned to the system—it cannot be used again. You can destroy a widget by calling `gtk_widget_destroy()`. If the widget is a type that possibly can have more than one reference, it also can be destroyed by a call to `gtk_widget_unref()`, which reduces a reference counter by one and, if the count reaches zero, destroys the widget. This function makes sure that a window is hidden, unmapped, and unrealized before it is destroyed. Destroying a widget returns all of the allocated memory back to the system.

# Show and Hide

When a widget is shown, the window (or windows) of the widget appears on the display. In this state, the window is active and available for mouse and keyboard activity. The window first appears in the area mapped for it by the window manager. A window is shown with a call to `gtk_widget_show()`, which calls `gtk_widget_map()` and `gtk_widget_realize()` if necessary.

When a widget is hidden, its window is no longer visible on the display. A hidden window also is unmapped, allowing the container widget to remap its other child members automatically to update the display. For example, if you hide a button on a menu, the remaining buttons move up so there is no gap left. To hide a window, call `gtk_widget_hide()`, which automatically calls `gtk_widget_unmap()`.