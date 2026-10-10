
# GnomeCanvasEllipse

The GnomeCanvasEllipse is a GnomeCanvasItem that draws itself as an ellipse on a GnomeCanvas.

- **Inheritance**
  GnomeCanvasEllipse -> GnomeCanvasRE -> GnomeCanvasItem -> GtkObject
- **Function**
  GtkType gnome_canvas_ellipse_get_type(void)

Chapter 9 provides examples of the GnomeCanvasEllipse widget.

# GnomeCanvasGroup

Objects of this class are created and managed inside a GnomeCanvas widget. Its purpose is to contain and control a collection of CanvasItem objects displayed by the GnomeCanvas. The only way to add a GnomeCanvasItem to a GnomeCanvas is to add it to a GnomeCanvasGroup object. And, because the GnomeCanvasGroup also is a GnomeCanvasItem, it can contain other GnomeCanvasGroups. There is always one GnomeCanvasGroup (the root group) in a GnomeCanvas.

- **Inheritance**
  GnomeCanvasGroup -> GnomeCanvasItem -> GtkObject
- **Functions**
  - void gnome_canvas_group_child_bounds(GnomeCanvasGroup *group, GnomeCanvasItem *item)
  - GtkType gnome_canvas_group_get_type(void)

Chapter 9 includes examples of the GnomeCanvasGroup.

# GnomeCanvasImage

A GnomeCanvasImage displays an image on a GnomeCanvas.

- **Inheritance**
  GnomeCanvasImage -> GnomeCanvasItem -> GtkObject
- **Function**
  GtkType gnome_canvas_image_get_type(void)

You can see examples of using GnomeCanvasImage in Chapter 9.

# GnomeCanvasItem

The GnomeCanvasItem is the base class of all items that a GnomeCanvas displays.

### Inheritance

GnomeCanvasItem -> GtkObject

### Functions

```c
void gnome_canvas_item_affine_absolute(GnomeCanvasItem *item, const double affine[6])
void gnome_canvas_item_affine_relative(GnomeCanvasItem *item, const double affine[6])
void gnome_canvas_item_construct(GnomeCanvasItem *item, GnomeCanvasGroup *parent, const gchar *first_arg_name, va_list args)
void gnome_canvas_item_constructv(GnomeCanvasItem *item, GnomeCanvasGroup *parent, guint nargs, GtkArg *args)
void gnome_canvas_item_get_bounds(GnomeCanvasItem *item, double *x1, double *y1, double *x2, double *y2)
GtkType gnome_canvas_item_get_type(void)
int gnome_canvas_item_grab(GnomeCanvasItem *item, guint event_mask, GdkCursor *cursor, guint32 etime)
void gnome_canvas_item_grab_focus(GnomeCanvasItem *item)
void gnome_canvas_item_hide(GnomeCanvasItem *item)
void gnome_canvas_item_ic_affine(GnomeCanvasItem *item, double affine[6])
void gnome_canvas_item_i2w(GnomeCanvasItem *item, double *x, double *y)
void gnome_canvas_item_i2w_affine(GnomeCanvasItem *item, double affine[6])
void gnome_canvas_item_lower(GnomeCanvasItem *item, int positions)
void gnome_canvas_item_lower_to_bottom(GnomeCanvasItem *item)
void gnome_canvas_item_move(GnomeCanvasItem *item, double dx, double dy)
GnomeCanvasItem *gnome_canvas_item_new( GnomeCanvasGroup *parent, GtkType type, const gchar *first_arg_name, ... )
GnomeCanvasItem *gnome_canvas_item_newv( GnomeCanvasGroup *parent, GtkType type, guint nargs, GtkArg *args )
void gnome_canvas_item_raise(GnomeCanvasItem *item, int positions)
void gnome_canvas_item_raise_to_top(GnomeCanvasItem *item)
void gnome_canvas_item_reparent(GnomeCanvasItem *item, GnomeCanvasGroup *new_group)
void gnome_canvas_item_request_redraw_svp( GnomeCanvasItem *item, const ArtSVP *svp )
void gnome_canvas_item_request_update(GnomeCanvasItem *item)
void gnome_canvas_item_reset_bounds(GnomeCanvasItem *item)
void gnome_canvas_item_set(GnomeCanvasItem *item,
				const gchar *first_arg_name, ...)
void gnome_canvas_item_set_valist(GnomeCanvasItem *item,
				const gchar *first_arg_name, va_list args)
void gnome_canvas_item_setv(GnomeCanvasItem *item, guint nargs,
				GtkArg *args)
void gnome_canvas_item_show(GnomeCanvasItem *item)
void gnome_canvas_item_ungrob(GnomeCanvasItem *item,
				 guint32 etime)
void gnome_canvas_item_update_svp(GnomeCanvasItem *item,
				ArtSVP **p_svp, ArtSVP *new_svp)
void gnome_canvas_item_update_svp_clip(GnomeCanvasItem *item,
				ArtSVP **p_svp, ArtSVP *new_svp, ArtSVP *clip_svp)
void gnome_canvas_item_w2i(GnomeCanvasItem *item, double *x,
				double *y)
```

See Chapter 9 for examples of creating different kinds of GnomeCanvasItems.

# GnomeCanvasLine

The GnomeCanvasLine is a GnomeCanvasItem that draws a line on a GnomeCanvas.
The line can contain multiple segments.

- **Inheritance**
  GnomeCanvasLine -> GnomeCanvasItem -> GtkObject
- **Function**
  GtkType gnome_canvas_line_get_type(void)

You can find examples of GnomeCanvasLine in Chapter 9.

# GnomeCanvasPolygon

A GnomeCanvasPolygon is a GnomeCanvasItem that draws a filled polygon on a GnomeCanvas.

- **Inheritance**
  GnomeCanvasPolygon -> GnomeCanvasItem -> GtkObject
- **Functions**
  - GtkType gnome_canvas_polygon_get_type(void)
  - double gnome_canvas_polygon_to_point(double *poly, int num_points, double x, double y)

Refer to Chapter 9 for examples of GnomeCanvasPolygon.

# GnomeCanvasRE

This is a base class that acts as a parent for both GnomeCanvasRectangle and GnomeCanvasEllipse. This base class includes information pertaining to colors and sizes, but the two descendants contain the drawing details.

- **Inheritance**
  GnomeCanvasRE -> GnomeCanvasItem -> GtkObject
- **Functions**
  GtkType gnome_canvas_re_get_type(void)

Chapter 9 provides examples of GnomeCanvasEllipse and GnomeCanvasRect.

# GnomeCanvasRect

The GnomeCanvasRect is a GnomeCanvasItem that draws itself as a rectangle on a GnomeCanvas.

- **Inheritance**
  GnomeCanvasRect -> GnomeCanvasRE -> GnomeCanvasItem -> GtkObject
- **Function**
  GtkType gnome_canvas_rect_get_type(void)

You can see examples of GnomeCanvasRect in Chapter 9.

# GnomeCanvasText

A GnomeCanvasText is a GnomeCanvasItem that displays a line of text on a GnomeCanvas.

- **Inheritance**
  GnomeCanvasText -> GnomeCanvasItem -> GtkObject
- **Function**
  GtkType gnome_canvas_text_get_type(void)

Chapter 9 has examples of GnomeCanvasText.

# GnomeCanvasWidget

The GnomeCanvasWidget is not a widget — it is a GnomeCanvasItem that is capable of containing a widget. You can use a GnomeCanvasWidget to display any widget in a GnomeCanvas as if the widget were a GnomeCanvasItem.

### Inheritance

GnomeCanvasWidget -> GnomeCanvasItem -> GtkObject

### Function

```c
GtkType gnome_canvas_widget_get_type(void)
```

You can find an example of using the GnomeCanvasWidget in Chapter 9.

# GnomeClient

The GnomeClient object makes it possible for your application to save session information when the user logs out. If, when logging out, the user chooses to save the current settings, a “save_yourself” signal is sent to each application. Then an application can save information in such a way that it is supplied on the command line whenever the program automatically restarts by a user login.

### Inheritance

GnomeClient -> GtkObject

### Functions

```c
void gnome_client_add_static_arg(GnomeClient *client, ...)
void gnome_client_connect(GnomeClient *client)
void gnome_client_disable_master_connection(void)
void gnome_client_disconnect(GnomeClient *client)
void gnome_client_flush(GnomeClient *client)
gchar *gnome_client_get_config_prefix(GnomeClient *client)
GnomeClientFlags gnome_client_get_flags(GnomeClient *client)
gchar *gnome_client_get_global_config_prefix(GnomeClient *client)
void gnome_client_init(void)
GnomeClient *gnome_client_new(void)
void gnome_client_new_without_connection(void)
void gnome_client_request_interaction(GnomeClient *client,
                                      GnomeDialogType dialog_type,
                                      GnomeInteractFunction function, gpointer data)
void gnome_client_request_interaction_interp(
GnomeClient *client, GnomeDialogType dialog_type,
GtkCallbackMarshal function, gpointer data,
GtkDestroyNotify destroy)
void gnome_client_request_phase_2(GnomeClient *client)
void gnome_client_request_save(GnomeClient *client,
GnomeSaveStyle save_style, gboolean shutdown,
GnomeInteractStyle interact_style, gboolean fast,
gboolean global)
void gnome_client_save_any_dialog(GnomeClient *client,
GnomeDialog *dialog)
void gnome_client_save_error_dialog(GnomeClient *client,
GnomeDialog *dialog)
void gnome_client_set_clone_command(GnomeClient *client,
gint argc, gchar *argv[])
void gnome_client_set_current_directory(GnomeClient *client,
const gchar *dir)
void gnome_client_set_discard_command(GnomeClient *client,
gint argc, gchar *argv[])
void gnome_client_set_environment(GnomeClient *client,
const gchar *name, const gchar *value)
void gnome_client_set_global_config_prefix(
GnomeClient *client, gchar *prefix)
void gnome_client_set_id(GnomeClient *client, const gchar *id)
void gnome_client_set_priority(GnomeClient *client,
guint priority)
void gnome_client_set_process_id(GnomeClient *client,
pid_t pid)
void gnome_client_set_program(GnomeClient *client,
const gchar *program)
void gnome_client_set_resign_command(GnomeClient *client,
gint argc, gchar *argv[])
void gnome_client_set_restart_command(GnomeClient *client,
gint argc, gchar *argv[])
void gnome_client_set_restart_style(GnomeClient *client,
GnomeRestartStyle style)
void gnome_client_set_shutdown_command(GnomeClient *client,
gint argc, gchar *argv[])
void gnome_client_set_user_id(GnomeClient *client,
const gchar *id)
GnomeClient *gnome_cloned_client(void)
void gnome_interaction_key_return(gint tag,
gboolean cancel_shutdown)
GnomeClient *gnome_master_client(void)
```

### Enums

```c
typedef enum {
GNOME_INTERACT_NONE,
GNOME_INTERACT_ERRORS,
GNOME_INTERACT_ANY
} GnomeInteractStyle;
```
