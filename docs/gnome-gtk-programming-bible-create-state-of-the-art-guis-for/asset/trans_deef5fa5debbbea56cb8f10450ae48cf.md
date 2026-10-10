

# GnomeCanvasEllipse

GnomeCanvasEllipse 是一种 GnomeCanvasItem，它会在 GnomeCanvas 上将自己绘制为一个椭圆。

- **继承关系**
  GnomeCanvasEllipse -> GnomeCanvasRE -> GnomeCanvasItem -> GtkObject
- **函数**
  GtkType gnome_canvas_ellipse_get_type(void)

第 9 章提供了 GnomeCanvasEllipse 小部件的示例。

# GnomeCanvasGroup

此类的对象在 GnomeCanvas 小部件内部创建和管理。其目的是包含并控制由 GnomeCanvas 显示的一组 CanvasItem 对象。将 GnomeCanvasItem 添加到 GnomeCanvas 的唯一方法是将其添加到 GnomeCanvasGroup 对象中。而且，由于 GnomeCanvasGroup 本身也是一个 GnomeCanvasItem，它可以包含其他 GnomeCanvasGroup。每个 GnomeCanvas 中始终都有一个 GnomeCanvasGroup（根组）。

- **继承关系**
  GnomeCanvasGroup -> GnomeCanvasItem -> GtkObject
- **函数**
  - void gnome_canvas_group_child_bounds(GnomeCanvasGroup *group, GnomeCanvasItem *item)
  - GtkType gnome_canvas_group_get_type(void)

第 9 章包含 GnomeCanvasGroup 的示例。

# GnomeCanvasImage

GnomeCanvasImage 在 GnomeCanvas 上显示图像。

- **继承关系**
  GnomeCanvasImage -> GnomeCanvasItem -> GtkObject
- **函数**
  GtkType gnome_canvas_image_get_type(void)

你可以在第 9 章中看到使用 GnomeCanvasImage 的示例。

# GnomeCanvasItem

GnomeCanvasItem 是 GnomeCanvas 显示的所有项目的基础类。

### 继承关系

GnomeCanvasItem -> GtkObject

### 函数

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

有关创建不同类型的 GnomeCanvasItem 的示例，请参见第 9 章。

# GnomeCanvasLine

GnomeCanvasLine 是一种 GnomeCanvasItem，它会在 GnomeCanvas 上绘制一条线。
这条线可以包含多个线段。

- **继承关系**
  GnomeCanvasLine -> GnomeCanvasItem -> GtkObject
- **函数**
  GtkType gnome_canvas_line_get_type(void)

你可以在第 9 章中找到 GnomeCanvasLine 的示例。

# GnomeCanvasPolygon

GnomeCanvasPolygon 是一种 GnomeCanvasItem，它会在 GnomeCanvas 上绘制一个填充多边形。

- **继承关系**
  GnomeCanvasPolygon -> GnomeCanvasItem -> GtkObject
- **函数**
  - GtkType gnome_canvas_polygon_get_type(void)
  - double gnome_canvas_polygon_to_point(double *poly, int num_points, double x, double y)

有关 GnomeCanvasPolygon 的示例，请参见第 9 章。

# GnomeCanvasRE

这是一个基础类，作为 GnomeCanvasRectangle 和 GnomeCanvasEllipse 的父类。该基础类包含与颜色和大小相关的信息，但两个子类则包含绘图细节。

- **继承关系**
  GnomeCanvasRE -> GnomeCanvasItem -> GtkObject
- **函数**
  GtkType gnome_canvas_re_get_type(void)

第 9 章提供了 GnomeCanvasEllipse 和 GnomeCanvasRect 的示例。

# GnomeCanvasRect

GnomeCanvasRect 是一种 GnomeCanvasItem，它会在 GnomeCanvas 上将自己绘制为一个矩形。

- **继承关系**
  GnomeCanvasRect -> GnomeCanvasRE -> GnomeCanvasItem -> GtkObject
- **函数**
  GtkType gnome_canvas_rect_get_type(void)

你可以在第 9 章中看到 GnomeCanvasRect 的示例。

# GnomeCanvasText

GnomeCanvasText 是一种 GnomeCanvasItem，它会在 GnomeCanvas 上显示一行文本。

- **继承关系**
  GnomeCanvasText -> GnomeCanvasItem -> GtkObject
- **函数**
  GtkType gnome_canvas_text_get_type(void)

第 9 章有 GnomeCanvasText 的示例。

# GnomeCanvasWidget

GnomeCanvasWidget 不是一个小部件——它是一种能够容纳小部件的 GnomeCanvasItem。你可以使用 GnomeCanvasWidget 在 GnomeCanvas 中显示任何小部件，就像该小部件是一个 GnomeCanvasItem 一样。

### 继承关系

GnomeCanvasWidget -> GnomeCanvasItem -> GtkObject

### 函数

```c
GtkType gnome_canvas_widget_get_type(void)
```

你可以在第 9 章中找到使用 GnomeCanvasWidget 的示例。

# GnomeClient

GnomeClient 对象使你的应用程序能够在用户注销时保存会话信息。如果在注销时，用户选择保存当前设置，则会向每个应用程序发送一个“save_yourself”信号。然后，应用程序可以以这样一种方式保存信息，即当程序通过用户登录自动重启时，该信息会在命令行中提供。

### 继承关系

GnomeClient -> GtkObject

### 函数

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

### 枚举

```c
typedef enum {
GNOME_INTERACT_NONE,
GNOME_INTERACT_ERRORS,
GNOME_INTERACT_ANY
} GnomeInteractStyle;
```

