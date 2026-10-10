# Functions

```
GtkButtonBoxStyle gtk_vbutton_box_get_layout_default(void)
 gint gtk_vbutton_box_get_spacing_default(void)
 guint gtk_vbutton_box_get_type(void)
 GtkWidget *gtk_vbutton_box_new(void)
 void gtk_vbutton_box_set_layout_default(
   GtkButtonBoxStyle layout)
 void gtk_vbutton_box_set_spacing_default(gint spacing)
```

# Enum

```
typedef enum {
  GTK_BUTTONBOX_DEFAULT_STYLE,
  GTK_BUTTONBOX_SPREAD,
  GTK_BUTTONBOX_EDGE,
  GTK_BUTTONBOX_START,
  GTK_BUTTONBOX_END
} GtkButtonBoxStyle;
```

You can find a number of examples of GtkVButtonBox in Chapter 5.

# GtkViewport

A GtkViewport is a container that does not resize to fit in the space allotted to it. Instead, it adds scrollbars as necessary so you can view any part of the window.

# Inheritance

GtkViewport->GtkBin->GtkContainer->GtkWidget->GObject

# Functions

```
GtkAdjustment *gtk_viewport_get_hadjustment(
  GtkViewport *viewport)
 GtkType gtk_viewport_get_type(void)
 GtkAdjustment *gtk_viewport_get_vadjustment(
  GtkViewport *viewport)
 GtkWidget *gtk_viewport_new(GtkAdjustment *hadjustment,
  GtkAdjustment *vadjustment)
 void gtk_viewport_set_hadjustment(GtkViewport *viewport,
  GtkAdjustment *adjustment)
 void gtk_viewport_set_shadow_type(GtkViewport *viewport,
  GtkShadowType type)
 void gtk_viewport_set_vadjustment(GtkViewport *viewport,
  GtkAdjustment *adjustment)
```

# Enum

```
typedef enum {
  GTK_SHADOW_NONE,
  GTK_SHADOW_IN,
```