
void gnome_dialog_close_real(GnomeDialog *dialog)
void gnome_dialog_construct(GnomeDialog *dialog,
const gchar *title, va_list ap)
void gnome_dialog_construct(GnomeDialog *dialog,
const gchar *title, const gchar **buttons)
void gnome_dialog_editable_enters(GnomeDialog *dialog,
GtkEditable *editable)
guint gnome_dialog_get_type()
GtkWidget *gnome_dialog_new(const gchar *title, ...)
GtkWidget *gnome_dialog_new(const gchar *title,
const gchar **buttons)
gint gnome_dialog_run(GnomeDialog *dialog)
gint gnome_dialog_run_and_close(GnomeDialog *dialog)
void gnome_dialog_set_accelerator(GnomeDialog *dialog,
gint button, const guchar accelerator_key,
guint8 accelerator_mods)
void gnome_dialog_set_close(GnomeDialog *dialog,
gboolean click_closes)
void gnome_dialog_set_default(GnomeDialog *dialog, gint button)
void gnome_dialog_set_parent(GnomeDialog *dialog,
GtkWindow *parent)
void gnome_dialog_set_sensitive(GnomeDialog *dialog,
gint button, gboolean setting)

该示例在顶部显示一个 `GtkLabel` 控件，并在底部使用两个标准按钮，如图 22-8 所示。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_684_0.png)

按钮按照在 `gnome_dialog_new()` 函数中命名的顺序，从左到右添加到对话框中。为了获取按钮的响应，需要将 “clicked” 回调函数连接到整个对话框。在回调函数内部，所选按钮由其编号指定——第一个按钮为零，第二个为一，依此类推。此外，在回调函数中调用了 `gtk_widget_destroy()` 来销毁对话框。

```c
/** gnomedialog.c **/
#include <gnome.h>

static void dialogCallback(GtkWidget *widget,
gint button, gpointer data);

int main(int argc, char *argv[])
{
GtkWidget *dialog;
GtkWidget *box;
GtkWidget *label;

gnome_init("gnomedialog", "1.0", argc, argv);

dialog = gnome_dialog_new("GnomeDialog",
    GNOME_STOCK_BUTTON_OK,
    GNOME_STOCK_BUTTON_CANCEL,
    NULL);

label = gtk_label_new("Text of the dialog box");
box = GNOME_DIALOG(dialog)->vbox;
gnome_dialog_set_default(GNOME_DIALOG(dialog), 0);
gtk_box_pack_start(GTK_BOX(box), label, TRUE, TRUE, 0);

gtk_signal_connect(GTK_OBJECT(dialog), "clicked",
    dialogCallback, NULL);

gtk_widget_show_all(dialog);
gtk_main();
exit(0);
}

static void dialogCallback(GtkWidget *widget,
gint button, gpointer data)
{
switch(button) {
case 0:
g_print("The OK Button\n");
break;
case 1:
g_print("The CANCEL Button\n");
break;
}
gtk_widget_destroy(widget);
}
```

以下是您可以包含在对话框中的标准按钮列表。

- GNOME_STOCK_BUTTON_OK
- GNOME_STOCK_BUTTON_CANCEL
- GNOME_STOCK_BUTTON_YES
- GNOME_STOCK_BUTTON_NO
- GNOME_STOCK_BUTTON_CLOSE
- GNOME_STOCK_BUTTON_APPLY
- GNOME_STOCK_BUTTON_HELP
- GNOME_STOCK_BUTTON_NEXT
- GNOME_STOCK_BUTTON_PREV
- GNOME_STOCK_BUTTON_UP
- GNOME_STOCK_BUTTON_DOWN
- GNOME_STOCK_BUTTON_FONT

## GnomeDock

您可以将 GnomeDock 控件添加到窗口中，以管理控件的停靠和取消停靠。它实际上管理着一组 GnomeDockBands，每个 GnomeDockBand 可以包含一个或多个 GnomeDockItems。

## 继承

```
GnomeDock->GtkContainer->GtkWidget->GtkObject
```

## 函数

```c
void gnome_dock_add_floating_item (GnomeDock *dock,
GnomeDockItem *item, gint x, gint y,
GtkOrientation orientation)
gboolean gnome_dock_add_from_layout (GnomeDock *dock,
GnomeDockLayout *layout)
void gnome_dock_add_item (GnomeDock *dock, GnomeDockItem *item,
GnomeDockPlacement placement, guint band_num,
gint position, guint offset, gboolean in_new_band)
void gnome_dock_allow_floating_items (GnomeDock *dock,
gboolean enable)
GtkWidget *gnome_dock_get_client_area (GnomeDock *dock)
GnomeDockItem *gnome_dock_get_item_by_name (GnomeDock *dock,
const gchar *name, GnomeDockPlacement *placement_return,
guint *num_band_return, guint *band_position_return,
guint *offset_return)
GnomeDockLayout *gnome_dock_get_layout (GnomeDock *dock)
GtkType gnome_dock_get_type (void)
GtkWidget *gnome_dock_new (void)
void gnome_dock_set_client_area (GnomeDock *dock,
GtkWidget *widget)
```

## 枚举

```c
typedef enum {
GNOME_DOCK_TOP,
GNOME_DOCK_RIGHT,
GNOME_DOCK_BOTTOM,
GNOME_DOCK_LEFT,
GNOME_DOCK_FLOATING
} GnomeDockPlacement;
```

## 信号

```c
"layout_changed"    void cb(GtkWidget *, gpointer)
```

以下示例创建了一个 GnomeDock 控件并将其添加到应用程序的主窗口中。函数 `makeWidget()` 创建该控件并安装了三个工具栏。当窗口首次显示时，顶部有一个工具栏，右侧有一个，还有一个自由悬浮的，如图 22-9 所示。

```c
/** gamedock.c ***/
#include <gnome.h>

gint eventDelete(GtkWidget *widget,
GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget,
GdkEvent *event, gpointer data);
static GtkWidget *makeWidget();
static GtkWidget *makeToolbar();
static void uib_signal(GnomeUIInfo *uifinfo, gchar *signal_name,
GnomeUIBuilderData *uidata);

static GnomeUIInfo toolbarDef[] = {
{ GNOME_APP_UI_ITEM, "New",
"Create a new file", NULL, NULL, NULL,
GNOME_APP_PIXMAP_STOCK, GNOME_STOCK_PIXMAP_NEW,
0, 0, NULL },
{ GNOME_APP_UI_ITEM, "Open",
"Open an existing file", NULL, NULL, NULL,
GNOME_APP_PIXMAP_STOCK, GNOME_STOCK_PIXMAP_OPEN,
0, 0, NULL },
{ GNOME_APP_UI_ITEM, "Save",
"Save the current file", NULL, NULL, NULL,
GNOME_APP_PIXMAP_STOCK, GNOME_STOCK_PIXMAP_SAVE,
0, 0, NULL },
{ GNOME_APP_UI_ITEM, "Save as",
"Save to a new file", NULL, NULL, NULL,
GNOME_APP_PIXMAP_STOCK, GNOME_STOCK_PIXMAP_SAVE_AS,
0, 0, NULL },
GNOME_UIINFO_END
};

int main(int argc, char *argv[])
{
GtkWidget *app;
GtkWidget *widget;

gnome_init("gnomedock", "1.0", argc, argv);
app = gnome_app_new("gnomedock", "GnomeDock");
gtk_widget_set_usize(GTK_WIDGET(app), 350, 350);
gtk_signal_connect(GTK_OBJECT(app), "delete_event",
GTK_SIGNAL_FUNC(eventDelete), NULL);
gtk_signal_connect(GTK_OBJECT(app), "destroy",
GTK_SIGNAL_FUNC(eventDestroy), NULL);

widget = makeWidget();

gnome_app_set_contents(GNOME_APP(app), widget);
gtk_widget_show_all(app);
gtk_main();
exit(0);
}

gint eventDelete(GtkWidget *widget,
GdkEvent *event, gpointer data) {
return(FALSE);
}

gint eventDestroy(GtkWidget *widget,
GdkEvent *event, gpointer data) {
gtk_main_quit();
return(0);
}

static GtkWidget *makeWidget()
{
GtkWidget *dock;
GnomeDockLayout *layout;
GtkWidget *item;
GtkWidget *toolbar;

dock = gnome_dock_new();
layout = gnome_dock_layout_new();

toolbar = makeToolbar();
item = gnome_dock_item_new("Item1",
GNOME_DOCK_ITEM_BEH_EXCLUSIVE);
gtk_container_add(GTK_CONTAINER(item), toolbar);
gnome_dock_layout_add_item(layout, GNOME_DOCK_ITEM(item),
GNOME_DOCK_TOP, 0, 0, 0);

toolbar = makeToolbar();
item = gnome_dock_item_new("Item2",
GNOME_DOCK_ITEM_BEH_NORMAL);
gtk_container_add(GTK_CONTAINER(item), toolbar);
gnome_dock_layout_add_item(layout, GNOME_DOCK_ITEM(item),
GNOME_DOCK_RIGHT, 0, 0, 0);

toolbar = makeToolbar();
item = gnome_dock_item_new("Item3",
GNOME_DOCK_ITEM_BEH_NORMAL);
gtk_container_add(GTK_CONTAINER(item), toolbar);
gnome_dock_layout_add_item(layout, GNOME_DOCK_ITEM(item),
GNOME_DOCK_FLOATING, 0, 0, 0);

gtk_widget_show(toolbar);
gtk_widget_show(item);

gnome_dock_layout_add_to_dock(GNOME_DOCK_LAYOUT(layout),
GNOME_DOCK(dock));

return(dock);
}

static GtkWidget *makeToolbar()
{
GtkWidget *toolbar;
GnomeUIBuilderData uibdata;

toolbar = gtk_toolbar_new(GTK_ORIENTATION_HORIZONTAL, GTK_TOOLBAR_ICONS);
gtk_container_set_border_width(GTK_CONTAINER(toolbar), 1);

uibdata.connect_func = uib_signal;
uibdata.data = NULL;
uibdata.is_interp = FALSE;
uibdata.relay_func = NULL;
uibdata.destroy_func = NULL;
gnome_app_fill_toolbar_custom(GTK_TOOLBAR(toolbar), toolbarDef, &uibdata, NULL);

return(toolbar);
}

static void uib_signal(GnomeUIInfo *uinfo, gchar *signal_name,
GnomeUIBuilderData *uibdata)
{
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_689_0.png)

**图 22-9：** 显示三个工具栏的停靠窗口

随着每个工具栏的创建，通过调用 `gtk_container_add()` 将其插入到 `GnomeDockItem` 中。然后，`GnomeDockItem` 依次被添加到 `GnomeDockLayout` 中。最后，通过调用 `gnome_dock_layout_add_to_dock()` 将 `GnomeDockLayout` 添加到 `GnomeDock` 中。

`GnomeApp` 窗口提供了一种更简单的方式来创建工具栏。您可以在第 8 章中看到一些示例。

