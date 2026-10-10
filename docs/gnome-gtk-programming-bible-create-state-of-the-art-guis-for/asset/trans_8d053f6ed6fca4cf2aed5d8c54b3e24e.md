
# GnomeAnimator

## 函数

- `GnomeAnimator *animator)`
- `GnomeAnimatorLoopType gnome_animator_get_loop_type(GnomeAnimator *animator)`
- `gint gnome_animator_get_playback_direction(GnomeAnimator *animator)`
- `double gnome_animator_get_playback_speed(GnomeAnimator *animator)`
- `GnomeAnimatorStatus gnome_animator_get_status(GnomeAnimator *animator)`
- `guint gnome_animator_get_type(void)`
- `void gnome_animator_goto_frame(GnomeAnimator *animator, guint frame_number)`
- `GtkWidget *gnome_animator_new_with_size(guint width, guint height)`
- `void gnome_animator_set_loop_type(GnomeAnimator *animator, GnomeAnimatorLoopType loop_type)`
- `void gnome_animator_set_playback_direction(GnomeAnimator *animator, gint playback_direction)`
- `void gnome_animator_set_playback_speed(GnomeAnimator *animator, double speed)`
- `void gnome_animator_start(GnomeAnimator *animator)`
- `void gnome_animator_stop(GnomeAnimator *animator)`

## 枚举

- `GNOME_ANIMATOR_LOOP_NONE`
- `GNOME_ANIMATOR_LOOP_RESTART`
- `GNOME_ANIMATOR_LOOP_PING_PONG`
- `GNOME_ANIMATOR_STATUS_STOPPED`
- `GNOME_ANIMATOR_STATUS_RUNNING`

以下示例实现了图 22-1 中所示的调制类似图的动画。序列的每一帧都作为 XPM 数据存储在名为 "animator.xpm" 的文件中，而每帧的地址则存储在名为 anim 的数组中。这部分内容位于程序的开头，形式如下：

- `#include "animator.xpm"`
- `static char **anim[] = { anim1,anim2,anim3,anim4,anim5 };`

其中包含一个循环，为每一帧创建一个 GnomePixmap，并将每个 pixmap 作为帧追加到序列中。animator 被设置为按顺序显示帧，然后回到开头重新开始。你也可以将 animator 设置为只按顺序遍历帧一次，或者将其设置为仅显示第一帧并等待应用程序切换帧。

- `static GtkWidget *makeWidget() { ... }`

![](img/8bcc1ba72831c7d67cfc8b395deab95f_667_0.png)

# GnomeApp

GnomeApp 小部件是 GNOME 应用程序的主窗口。它是一个容器小部件，可以容纳单个子小部件。它还提供了用于附加菜单、工具栏、状态栏以及可停靠小部件的设施。

## 继承

`GnomeApp->GtkWindow->GtkBin->GtkContainer->GtkWidget->GtkObject`

## 函数

- `void gnome_app_add_dock_item(GnomeApp *app, GnomeDockItem *item, GnomeDockPlacement placement, gint band_num, gint band_position, gint offset)`
- `void gnome_app_add_docked(GnomeApp *app, GtkWidget *widget, const gchar *name, GnomeDockItemBehavior behavior, GnomeDockPlacement placement, gint band_num, gint band_position, gint offset)`
- `void gnome_app_add_toolbar(GnomeApp *app, GtkToolbar *toolbar, const gchar *name, GnomeDockItemBehavior behavior, GnomeDockPlacement placement, gint band_num, gint band_position, gint offset)`
- `void gnome_app_construct(GnomeApp *app, gchar *appname, char *title)`
- `void gnome_app_enable_layout_config(GnomeApp *app, gboolean enable)`
- `GnomeDock *gnome_app_get_dock(GnomeApp *app)`
- `GnomeDockItem *gnome_app_get_dock_item_by_name(GnomeApp *app, const gchar *name)`
- `GtkType gnome_app_get_type(void)`
- `GtkWidget *gnome_app_new(gchar *appname, char *title)`
- `void gnome_app_set_contents(GnomeApp *app, GtkWidget *contents)`
- `void gnome_app_set_menus(GnomeApp *app, GtkMenuBar *menubar)`
- `void gnome_app_set_statusbar(GnomeApp *app, GtkWidget *statusbar)`
- `void gnome_app_set_statusbar_custom(GnomeApp *app, GtkWidget *container, GtkWidget *statusbar)`
- `void gnome_app_set_toolbar(GnomeApp *app, GtkToolbar *toolbar)`

## 枚举

- `GNOME_DOCK_ITEM_BEH_NORMAL = 0`
- `GNOME_DOCK_ITEM_BEH_EXCLUSIVE = 1 << 0`
- `GNOME_DOCK_ITEM_BEH_NEVER_FLOATING = 1 << 1`
- `GNOME_DOCK_ITEM_BEH_NEVER_VERTICAL = 1 << 2`
- `GNOME_DOCK_ITEM_BEH_NEVER_HORIZONTAL = 1 << 3`
- `GNOME_DOCK_ITEM_BEH_LOCKED = 1 << 4`
- `GNOME_DOCK_TOP`
- `GNOME_DOCK_RIGHT`
- `GNOME_DOCK_BOTTOM`
- `GNOME_DOCK_LEFT`
- `GNOME_DOCK_FLOATING`

第 2 章提供了一些关于 GnomeApp 小部件的入门示例。

# GnomeAppBar

GnomeAppBar 小部件是一个带有文本注释的进度条。

## 继承

`GnomeAppBar->GtkHBox->GtkBox->GtkContainer->GtkWidget->GtkObject`

## 函数

- `void gnome_appbar_clear_prompt(GnomeAppBar *appbar)`
- `void gnome_appbar_clear_stack(GnomeAppBar *appbar)`
- `void gnome_appbar_construct(GnomeAppBar *ab, gboolean has_progress, gboolean has_status, GnomePreferencesType interactivity)`
- `GtkProgress *gnome_appbar_get_progress(GnomeAppBar *ab)`
- `Gchar *gnome_appbar_get_response(GnomeAppBar *appbar)`
- `guint gnome_appbar_get_type();`
- `GtkWidget *gnome_appbar_new(gboolean has_progress, gboolean has_status, GnomePreferencesType interactivity)`
- `void gnome_appbar_pop(GnomeAppBar *appbar)`
- `void gnome_appbar_push(GnomeAppBar *appbar, const Gchar *status)`
- `void gnome_appbar_refresh(GnomeAppBar *appbar)`
- `void gnome_appbar_set_default(GnomeAppBar *appbar, const Gchar *default_status)`
- `void gnome_appbar_set_progress(GnomeAppBar *ab, gfloat percentage)`
- `void gnome_appbar_set_prompt(GnomeAppBar *appbar, const Gchar *prompt, gboolean modal)`
- `void gnome_appbar_set_status(GnomeAppBar *appbar, const Gchar *status)`

## 枚举

- `GNOME_PREFERENCES_NEVER`
- `GNOME_PREFERENCES_USER`
- `GNOME_PREFERENCES_ALWAYS`

GnomeAppBar 显示两部分数据。如图 22-2 所示，左侧是一个描述性字符串，右侧是一个进度条。调用函数 gnome_set_progress() 可设置进度值，调用 gnome_appbar_set_prompt() 可设置字符串。

- `static GtkWidget *makeWidget() { ... }`

![](img/8bcc1ba72831c7d67cfc8b395deab95f_669_0.png)

**图 22-2：GnomeAppBar 显示文本和进度条**

# GnomeCalculator

GnomeCalculator 小部件是一个弹出窗口，其中包含一个完全功能化的科学计算器。

## 继承

`GnomeCalculator->GtkVBox->GtkBox->GtkContainer->GtkWidget->GtkObject`

## 函数

- `void gnome_calculator_clear(GnomeCalculator *gc, const gboolean reset)`
- `quint gnome_calculator_get_type(void)`
- `GtkWidget *gnome_calculator_new(void)`
- `void gnome_calculator_set(GnomeCalculator *gc, gdouble result)`

由于 GnomeCalculator 处理所有用户输入和输出，因此其编程接口非常简单。图 22-3 展示了计算器面板。

- `static GtkWidget *makeWidget() { ... }`

![](img/8bcc1ba72831c7d67cfc8b395deab95f_670_0.png)

图 22-3：GnomeCalculator 小部件的布局

# GtkCanvas

你可以使用 **GtkCanvas** 小部件来绘制图形、显示图像、定位小部件等。

## 继承

`GtkCanvas->GtkLayout->GtkContainer->GtkWidget->GtkObject`

## 函数

- `void gtk_canvas_c2w(GtkCanvas *canvas, int cx, int cy, double *wx, double *wy)`
- `int gtk_canvas_get_color(GtkCanvas *canvas, char *spec, GdkColor *color)`
- `GtkCanvasItem *gtk_canvas_get_item_at(GtkCanvas *canvas, double x, double y)`
- `void gtk_canvas_get_scroll_offsets(GtkCanvas *canvas, int *cx, int *cy)`
- `void gtk_canvas_get_scroll_region(GtkCanvas *canvas, double *x1, double *y1, double *x2, double *y2)`
- `GtkType gtk_canvas_get_type(void)`
- `GtkWidget *gtk_canvas_new(void)`
- `GtkWidget *gtk_canvas_new_aa(void)`
- `void gtk_canvas_request_redraw(GtkCanvas *canvas, int x1, int y1, int x2, int y2)`
- `void gtk_canvas_request_redraw_uta(GtkCanvas *canvas, ArtUta *uta)`
- `GtkCanvasGroup *gtk_canvas_root(GtkCanvas *canvas)`
- `void gtk_canvas_scroll_to(GtkCanvas *canvas, int cx, int cy)`
- `void gtk_canvas_set_pixels_per_unit(GtkCanvas *canvas, double n)`
- `void gtk_canvas_set_scroll_region(GtkCanvas *canvas, double x1, double y1, double x2, double y2)`
- `void gtk_canvas_set_stipple_origin(GtkCanvas *canvas, GdkGC *gc)`
- `void gtk_canvas_update_now(GtkCanvas *canvas)`
- `void gtk_canvas_w2c(GtkCanvas *canvas, double wx, double wy, int *cx, int *cy)`
- `void gtk_canvas_w2c_affine(GtkCanvas *canvas, double *affine [6])`
- `void gtk_canvas_w2c_d(GtkCanvas *canvas, double wx, double wy, double *cx, double *cy)`
- `void gtk_canvas_window_to_world(GtkCanvas *canvas, double winx, double winy, double *worldx, double *worldy)`
- `void gtk_canvas_world_to_window(GtkCanvas *canvas, double worldx, double worldy, double *winx, double *winy)`

第 9 章重点介绍了如何使用 GtkCanvas 小部件。
