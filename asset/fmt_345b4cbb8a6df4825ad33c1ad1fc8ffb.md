
```c
gdk_draw_string(widget->window,
                font,
                gc,
                x + 130, y + 5,
                "Not last");

/* Cap ROUND */

y += 20;

gdk_gc_set_line_attributes(gc,
                           10,
                           GDK_LINE_SOLID,
                           GDK_CAP_ROUND,
                           GDK_JOIN_MITER);

gdk_draw_line(widget->window,
              gc,
              x, y,
              x + 120, y);

gdk_draw_string(widget->window,
                font,
                gc,
                x + 130, y + 5,
                "Round");

/* Cap PROJECTING */

y += 20;

gdk_gc_set_line_attributes(gc,
                           10,
                           GDK_LINE_SOLID,
                           GDK_CAP_PROJECTING,
                           GDK_JOIN_MITER);

gdk_draw_line(widget->window,
              gc,
              x, y,
              x + 120, y);

gdk_draw_string(widget->window,
                font,
                gc,
                x + 130, y + 5,
                "Projecting");

/* Style SOLID */

y += 40;

gdk_gc_set_line_attributes(gc,
                           10,
                           GDK_LINE_SOLID,
                           GDK_CAP_BUTT,
                           GDK_JOIN_MITER);

gdk_draw_line(widget->window,
              gc,
              x, y,
              x + 120, y);

gdk_draw_string(widget->window,
                font,
                gc,
                x + 130, y + 5,
                "Solid");

/* Style ON_OFF_DASH */

y += 20;

gdk_gc_set_dashes(gc,
                  0,
                  dashList,
                  4);

gdk_gc_set_line_attributes(gc,
                           10,
                           GDK_LINE_ON_OFF_DASH,
                           GDK_CAP_BUTT,
                           GDK_JOIN_MITER);

gdk_draw_line(widget->window,
              gc,
              x, y,
              x + 120, y);

gdk_draw_string(widget->window,
                font,
                gc,
                x + 130, y + 5,
                "On off dash");

/* Style DOUBLE DASH */

y += 20;

gdk_gc_set_line_attributes(gc,
                           10,
                           GDK_LINE_DOUBLE_DASH,
                           GDK_CAP_BUTT,
                           GDK_JOIN_MITER);

gdk_draw_line(widget->window,
              gc,
              x, y,
              x + 120, y);

gdk_draw_string(widget->window,
                font,
                gc,
                x + 130, y + 5,
                "Double dash");

gdk_font_unref(font);
gdk_gc_unref(gc);
return (TRUE);
}

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data)
{
    return (FALSE);
}

gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data)
{
    gtk_main_quit();
    return (0);
}
```
