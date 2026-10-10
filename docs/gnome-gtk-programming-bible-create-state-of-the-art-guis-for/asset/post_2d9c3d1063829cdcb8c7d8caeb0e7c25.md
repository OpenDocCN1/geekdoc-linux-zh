
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

This example displays a GtkLabel widget at the top and uses two of the standard buttons at the bottom, as shown in Figure 22-8.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_684_0.png)

The buttons are added to the dialog box from left to right in the order you name them on the `gnome_dialog_new()` function. To get a response from the buttons, a "clicked" callback is connected to the entire dialog box. Inside the callback function, the selected button is specified by its number — the first button is zero, the second is one, and so on. Also, a call to `gtk_widget_destroy()` is made in the callback function to delete the dialog box.

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

The following is the list of stock buttons that you can include in a dialog box.

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

You can add the GnomeDock widget to a window to manage the docking and undocking of widgets. It actually manages a set of GnomeDockBands, and each GnomeDockBand can contain one or more GnomeDockItems.

## Inheritance

```
GnomeDock->GtkContainer->GtkWidget->GtkObject
```

## Functions

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

## Enum

```c
typedef enum {
GNOME_DOCK_TOP,
GNOME_DOCK_RIGHT,
GNOME_DOCK_BOTTOM,
GNOME_DOCK_LEFT,
GNOME_DOCK_FLOATING
} GnomeDockPlacement;
```

## Signal

```c
"layout_changed"    void cb(GtkWidget *, gpointer)
```

The following example creates a GnomeDock widget and adds it to the main window of the application. The function `makeWidget()` creates the widget and installs three toolbars into it. When the window first appears, it has one toolbar at the top, one on the right, and one free-floating, as shown in Figure 22-9.

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

**Figure 22-9:** A docking window showing three toolbars

As each toolbar is created, it is inserted into `GnomeDockItem` with a call to `gtk_container_add()`. Then, in turn, the `GnomeDockItem` is added to the `GnomeDockLayout`. Finally, the `GnomeDockLayout` is added to the `GnomeDock` with the call to `gnome_dock_layout_add_to_dock()`.

The `GnomeApp` window provides a simpler way to create toolbars. You can see some examples of this in Chapter 8.
