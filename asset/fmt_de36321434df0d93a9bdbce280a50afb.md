
`gint gtk_window_activate_default(GtkWindow *window)`

`gint gtk_window_activate_focus(GtkWindow *window)`

`void gtk_window_add_accel_group(GtkWindow *window, GAccelGroup *accel_group)`

`void gtk_window_add_embedded_xid(GtkWindow *window, guint xid)`

`void gtk_window_get_type(void)`

`GtkWidget *gtk_window_new(GtkWindowType type)`

`void gtk_window_remove_accel_group(GtkWindow *window, GAccelGroup *accel_group)`

`void gtk_window_remove_embedded_xid(GtkWindow *window, guint xid)`

`void gtk_window_set_default(GtkWindow *window, GtkWidget *default_widget)`

`void gtk_window_set_default_size(GtkWindow *window, gint width, gint height)`

`void gtk_window_set_focus(GtkWindow *window, GtkWidget *focus)`

`void gtk_window_set_geometry_hints(GtkWindow *window, GtkWidget *geometry_widget, GdkGeometry *geometry, GdkWindowHints geom_mask)`

`void gtk_window_set_modal(GtkWindow *window, gboolean modal)`

`void gtk_window_set_policy(GtkWindow *window, gint allow_shrink, gint allow_grow, gint auto_shrink)`

`void gtk_window_set_position(GtkWindow *window, GtkWindowPosition position)`

`void gtk_window_set_title(GtkWindow *window, const gchar *title)`

`void gtk_window_set_transient_for(GtkWindow *window, GtkWindow *parent)`

`void gtk_window_set_wmclass(GtkWindow *window, const gchar *wmclass_name, const gchar *wmclass_class)`

### 枚举

```c

typedef enum {

    GTK_WINDOW_TOPLEVEL,

    GTK_WINDOW_DIALOG,

    GTK_WINDOW_POPUP

} GtkWindowType;

```

### 信号

```c

"set_focus" void cb(GtkWidget *, GtkWidget *, gpointer)

```

由于每个图形用户界面应用程序都必须拥有一个，因此创建顶层窗口的示例贯穿全书。特别是，您可以在第 3 章中看到弹出一个对话框窗口的过程。

## 摘要

本章提供了 GTK+ 部件的字母顺序列表，以及用于构建应用程序的许多其他 GTK+ 对象。每个类都随以下项目列出：

- 为对象定义信号、枚举类型和函数的列表
- 每个对象的继承关系，以便您可以跟踪特定部件定义的所有信号和函数
- 可显示部件和容器部件的示例，以及指向书中位于示例所在其他章节的引用

下一章是 GNOME 对象和部件的字母顺序列表。每个 GNOME 部件都基于 GTK+。这意味着在下一章中，将有必要追溯 GNOME 部件的继承关系回到本章中的 GTK+ 祖先。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_664_0.png)

# GNOME 部件

## 本章内容

本章提供了 GNOME 部件（以及其他一些对象）的字母顺序列表。每个部件都随其继承关系、应用程序可用的所有函数以及一个简单的示例列出。

- 列出并解释 GNOME 的部件以及其它一些对象
- 确定每个对象定义的所有信号和函数
- 通过检查继承关系来确定对象中可用的所有继承函数
- 确定用于向函数传递配置设置的枚举常量
- 通过包含每个部件的简单示例来起步

每个部件随附的示例代码，在大多数情况下，是一个创建可显示部件并返回其地址的函数。第 21 章的开头描述了显示这些部件的主程序。

## GnomeAbout

`GnomeAbout` 部件对话框窗口旨在从应用程序菜单中的“关于”按钮弹出。其目的是统一表单和内容。

### 继承

```
GnomeAbout -> GnomeDialog -> GtkWidget -> GtkContainer ->
GtkWindow -> GtkBin -> GtkWidget -> GObject
```

### 函数

```c

void gnome_about_construct(GnomeAbout *about,
    const gchar *title, const gchar *version,
    const gchar *copyright, const gchar **authors,
    const gchar *comments, const gchar *logo)

guint gnome_about_get_type()

GtkWidget *gnome_about_new(const gchar *title,
    const gchar *version, const gchar *copyright,
    const gchar **authors, const gchar *comments,
    const gchar *logo)

```

第 2 章展示了一个菜单按钮启动“关于”框的示例。

## GnomeAnimator

`GnomeAnimator` 部件一次显示一个图像列表，使得如果图像绘制正确，则显示动画序列。序列可以是连续的，从最后一个图像循环回到第一个图像，在最后一个图像显示后停止，或一次显示一个图像。

注意：目前，`GnomeAnimator` 部件尚不完整，因此您可能会发现这里的信息与较新版本存在一些差异。

### 继承

```
GnomeAnimator -> GtkWidget -> GtkObject
```

### 函数

```c

gboolean gnome_animator_advance(GnomeAnimator *animator, gint num);

gboolean gnome_animator_append_frame_from_file(GnomeAnimator *animator, const gchar *name, gint x_offset, gint y_offset, guint32 interval);

gboolean gnome_animator_append_frame_from_file_at_size(GnomeAnimator *animator, const gchar *name, gint x_offset, gint y_offset, guint32 interval, guint width, gint height);

gboolean gnome_animator_append_frame_from_gnome_pixmap(GnomeAnimator *animator, GnomePixmap *pixmap, gint x_offset, gint y_offset, guint32 interval);

gboolean gnome_animator_append_frame_from_umlb(GnomeAnimator *animator, GdkPmlbImage *image, gint x_offset, gint y_offset, guint32 interval);

gboolean gnome_animator_append_frame_from_umlb_at_size(GnomeAnimator *animator, GdkPmlbImage *image, gint x_offset, gint y_offset, guint32 interval, guint width, gint height);
```
