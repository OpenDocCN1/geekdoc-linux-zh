# Functions

```
```c
void gtk_scale_draw_value(GtkScale *scale)
GtkType gtk_scale_get_type(void)
void gtk_scale_get_value_width(GtkScale *scale)
void gtk_scale_set_digits(GtkScale *scale, gint digits)
void gtk_scale_set_draw_value(GtkScale *scale, gboolean draw_value)
void gtk_scale_set_value_pos(GtkScale *scale, GtkPositionType pos)
```
```

# Enum

```
```c
typedef enum
{
    GTK_POS_LEFT,
    GTK_POS_RIGHT,
    GTK_POS_TOP,
    GTK_POS_BOTTOM
} GtkPositionType;
```
```

# GtkScrollbar

The GtkScrollbar class is **the base class** for GtkHScrollbar and GtkVScrollbar.

# Inheritance

GtkScrollbar->GtkRange->GtkWidget->GtkObject

# Function

```
```c
GtkType gtk_scrollbar_get_type(void)
```
```

# GtkScrolledWindow

A GtkScrolledWindow is a container that does not resize to fit in the space allotted to it. Instead, it adds scrollbars (as necessary) so you can view any part of the window.

# Inheritance

GtkScrolledWindow->GtkBin->GtkContainer->GtkWidget->GtkObject

# Functions

```
```c
void gtk_scrolled_window_add_with_viewport(
    GtkScrolledWindow *scrolled_window, GtkWidget *child)
GtkAdjustment *gtk_scrolled_window_get_hadjustment(
    GtkScrolledWindow *scrolled_window)
GtkType gtk_scrolled_window_get_type(void)
```
```