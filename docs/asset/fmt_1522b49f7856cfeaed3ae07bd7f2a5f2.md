
以下示例创建了一个 `GnomeDock` 控件并将其添加到应用程序的主窗口中。函数 `makeWidget()` 创建该控件并安装了三个工具栏。当窗口首次显示时，顶部有一个工具栏，右侧有一个，还有一个自由悬浮的，如图 22-9 所示。

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

## `GnomeDockBand`

`GnomeDockBand` 是一个专门用于包含 `GnomeDock` 小组件中一组小部件的容器小部件。

### 继承

`GnomeDockBand` -> `GtkContainer` -> `GtkWidget` -> `Gtk Object`

### 函数

```c
gboolean gnome_dock_band_append(GnomeDockBand *band, GtkWidget *child, guint offset)
```
