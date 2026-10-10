

![](img/8bcc1ba72831c7d67cfc8b395deab95f_701_0.png)

这里确实涉及两个小部件。第一个是弹出选择对话框的按钮。另一个是作为 *GnomeDialog* 小部件构建的选择对话框。每当按钮被选中时，对话框窗口就会出现，供用户选择一个图标。下面的**示例**将“changed”信号连接到 *GnomeIconEntry* 小部件内部的 *GnomeEntry* 小部件；这会在每次用户使用鼠标选择图标或输入图标名称时执行回调 *eventIconChanged*()。

你可以在回调 *eventIconChanged*() 中获取图标名称，但在选中 OK 按钮之前这并不重要。为了等待直到按钮被点击，有必要向 *GnomeDialog* 小部件添加“clicked”回调。此信号被设置为每当用户选择 OK 或取消按钮时执行 *eventIconSelected*() 回调。如果用户选择 OK 按钮，则可以获取所选图标的名称。在附加新信号之前，所有信号都会从按钮上移除，因为 *eventIconChanged*() 回调可能在“clicked”信号到达之前被调用多次。

> 注意
> 这种双重回调序列之所以是必要的，仅仅是因为回调函数 *eventIconChanged*() 在用户每次点击浏览窗口中的图标时都会被调用。虽然在该点可以获得新的图标文件名，但你仍需要另一个回调来确定用户是点击了 OK 还是取消按钮。

## GnomeIconSelection

此小部件加载并显示一组图标，并允许用户选择其中一个。应用程序必须指定包含要显示的图标的目录。此小部件用作 *GnomeIconEntry* 小部件中的选择窗口。

### 继承

```
GnomeIconSelection->GtkVBox->GtkBox->GtkContainer->GtkWidget->
    GtkObject
```

### 函数

```c
void gnome_icon_selection_add_defaults(
    GnomeIconSelection *gis)
void gnome_icon_selection_add_directory(
    GnomeIconSelection *gis, const gchar *dir)
void gnome_icon_selection_clear(GnomeIconSelection *gis, gboolean not_shown)
const gchar *gnome_icon_selection_get_icon(GnomeIconSelection *gis, gboolean full_path)
guint gnome_icon_selection_get_type()
GtkWidget *gnome_icon_selection_new(void)
void gnome_icon_selection_select_icon(GnomeIconSelection *gis, const gchar *filename)
void gnome_icon_selection_show_icons(GnomeIconSelection *gis)
void gnome_icon_selection_stop_loading(GnomeIconSelection *gis)
```

以下示例将默认图标集加载到 GnomeIconSelection 小部件中并显示，如图 22-16 所示。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_702_0.png)

此示例不包含确定用户何时选择小部件所需的按钮或其他机制。您可以通过添加一个带有回调函数的按钮来实现此功能，该函数调用 gnome_icon_selection_get_icon() 以获取图标的文件名。

## GnomeLess

GnomeLess 小部件显示文本文件的内容。

### 继承

```
GnomeLess->GtkVBox->GtkBox->GtkContainer->GtkWidget->GtkObject
```

### 函数

```c
void gnome_less_clear(GnomeLess *gl)
void gnome_less_fixed_font(GnomeLess *gl)
guint gnome_less_get_type()
GtkWidget *gnome_less_new(void)
void gnome_less_reshow(GnomeLess *gl)
void gnome_less_set_fixed_font(GnomeLess *gl, gboolean fixed)
void gnome_less_set_font(GnomeLess *gl, GdkFont *font)
gboolean gnome_less_show_command(GnomeLess *gl, const gchar *command_line)
gboolean gnome_less_show_fd(GnomeLess *gl, int file_descriptor)
gboolean gnome_less_show_file(GnomeLess *gl, const gchar *path)
gboolean gnome_less_show_filestream(GnomeLess *gl, FILE *f)
void gnome_less_show_string(GnomeLess *gl, const gchar *s)
gboolean gnome_less_write_fd(GnomeLess *gl, int fd)
gboolean gnome_less_write_file(GnomeLess *gl, const gchar *path)
```

以下示例程序使用 GnomeLess 小部件显示其自身的源代码，如图 22-17 所示。

```c
static GtkWidget *makeWidget()
{
  GtkWidget *less;
  less = gnome_less_new();
  gnome_less_show_file(GNOME_LESS(less),"gnomeless.c");
  return(less);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_703_0.png)

图 22-17：GnomeLess 小部件显示文本文件的内容

## GnomeMDI

GnomeMDI 对象用于跟踪组成多文档界面（MDI）各个窗口的多个小部件。

### 继承

```
GnomeMDI->GtkObject
```

### 函数

```c
gint gnome_mdi_add_child(GnomeMDI *mdi, GnomeMDIChild *child)
gint gnome_mdi_add_toplevel_view(GnomeMDI *mdi, GnomeMDIChild *child)
gint gnome_mdi_add_view(GnomeMDI *mdi, GnomeMDIChild *child)
GnomeMDIChild *gnome_mdi_find_child(GnomeMDI *mdi, gchar *name)
GnomeMDIChild *gnome_mdi_get_active_child(GnomeMDI *mdi)
GtkWidget *gnome_mdi_get_active_view(GnomeMDI *mdi)
GnomeApp *gnome_mdi_get_app_from_view(GtkWidget *view)
GnomeApp *gnome_mdi_get_toplevel(GnomeMDI *mdi)
GnomeUIInfo *gnome_mdi_get_child_menu_info(GnomeApp *app)
GnomeUIInfo *gnome_mdi_get_menubar_info(GnomeApp *app)
GnomeUIInfo *gnome_mdi_get_view_from_window(GnomeMDI *mdi, GnomeApp *app)
guint gnome_mdi_get_type()
GtkWidget *gnome_mdi_get_view_from_window(GnomeMDI *mdi, GnomeApp *app)
GtkObject *gnome_mdi_new(gchar *appname, gchar *title)
void gnome_mdi_open_toplevel(GnomeMDI *mdi)
void gnome_mdi_register(GnomeMDI *mdi, GtkObject *object)
gint gnome_mdi_remove_all(GnomeMDI *mdi, gint force)
gint gnome_mdi_remove_child(GnomeMDI *mdi, GnomeMDIChild *child, gint force)
gint gnome_mdi_remove_view(GnomeMDI *mdi, GtkWidget *view, gint force)
void gnome_mdi_set_active_view(GnomeMDI *mdi, GtkWidget *view)
void gnome_mdi_set_child_list_path(GnomeMDI *mdi, const gchar *path)
void gnome_mdi_set_child_menu_path(GnomeMDI *mdi, const gchar *path)
void gnome_mdi_set_menubar_template(GnomeMDI *mdi, GnomeUIInfo *menu_tmpl)
void gnome_mdi_set_mode(GnomeMDI *mdi, GnomeMDIMode mode)
void gnome_mdi_set_toolbar_template(GnomeMDI *mdi, GnomeUIInfo *tbar_tmpl)
void gnome_mdi_unregister(GnomeMDI *mdi, GtkObject *object)
void gnome_mdi_update_child(GnomeMDI *mdi, GnomeMDIChild *child)
```

第 17 章提供了 GnomeMDI 的示例。

## GnomeMDIChild

GnomeMDIChild 对象是一个基类，用于创建 GnomeMDI 可以作为 MDI 窗口管理的小部件。除非您有特殊需求，否则您可以使用基于 GnomeMDIChild 的 GnomeMDIGenericChild。

### 继承

```
GnomeMDIChild->GtkObject
```

### 函数

```c
GtkWidget *gnome_mdi_child_add_view(GnomeMDIChild *mdi_child)
guint gnome_mdi_child_get_type()
void gnome_mdi_child_remove_view(GnomeMDIChild *mdi_child, GtkWidget *view)
void gnome_mdi_child_set_menu_template(
  GnomeMDIChild *mdi_child, GnomeUIInfo *menu_tmpl)
void gnome_mdi_child_set_name(GnomeMDIChild *mdi_child,
  gchar *name)
```

## GnomeMDIGenericChild

GnomeMDIGenericChild 小部件是子窗口的一种通用形式，可用于 MDI。

### 继承

```
GnomeMDIGenericChild->GnomeMDIChild->GtkObject
```

### 函数

```c
guint gnome_mdi_generic_child_get_type()
GnomeMDIGenericChild *gnome_mdi_generic_child_new(
  gchar *name)
void gnome_mdi_generic_child_set_config_func(
  GnomeMDIGenericChild *child, GnomeMDIChildConfigFunc func,
  gpointer data)
void gnome_mdi_generic_child_set_config_func_full(
  GnomeMDIGenericChild *child, GnomeMDIChildConfigFunc func,
  GtkCallbackMarshal marshal, gpointer data,
  GtkDestroyNotify notify)
void gnome_mdi_generic_child_set_label_func(
  GnomeMDIGenericChild *child, GnomeMDIChildLabelFunc func,
  gpointer data)
void gnome_mdi_generic_child_set_label_func_full(
  GnomeMDIGenericChild *child, GnomeMDIChildLabelFunc func,
  GtkCallbackMarshal marshal, gpointer data,
  GtkDestroyNotify notify)
void gnome_mdi_generic_child_set_menu_creator(
  GnomeMDIGenericChild *child, GnomeMDIChildMenuCreator func,
  gpointer data)
void gnome_mdi_generic_child_set_menu_creator_full(
  GnomeMDIGenericChild *child, GnomeMDIChildMenuCreator func,
  GtkCallbackMarshal marshal, gpointer data,
  GtkDestroyNotify notify)
void gnome_mdi_generic_child_set_view_creator(
  GnomeMDIGenericChild *child, GnomeMDIChildViewCreator func,
  gpointer data)
void gnome_mdi_generic_child_set_view_creator_full(
```

