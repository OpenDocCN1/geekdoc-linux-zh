

## GnomeClient

以下示例在用户注销时响应 GtkObject 中的 "save_yourself" 信号，并调用函数 `eventSaveYourself()`。此函数创建一个命令行参数数组，用于在程序停止的位置重启该程序。

```c
typedef enum {
    GNOME_DIALOG_ERROR,
    GNOME_DIALOG_NORMAL
} GnomeDialogType;

typedef enum {
    GNOME_SAVE_GLOBAL,
    GNOME_SAVE_LOCAL,
    GNOME_SAVE_BOTH
} GnomeSaveStyle;

typedef enum {
    GNOME_RESTART_IF_RUNNING,
    GNOME_RESTART_ANYWAY,
    GNOME_RESTART_IMMEDIATELY,
    GNOME_RESTART_NEVER
} GnomeRestartStyle;

typedef enum {
    GNOME_CLIENT_IDLE,
    GNOME_CLIENT_SAVING_PHASE_1,
    GNOME_CLIENT_WAITING_FOR_PHASE_2,
    GNOME_CLIENT_SAVING_PHASE_2,
    GNOME_CLIENT_FROZEN,
    GNOME_CLIENT_DISCONNECTED,
    GNOME_CLIENT_REGISTERING
} GnomeClientState;

typedef enum {
    GNOME_CLIENT_IS_CONNECTED,
    GNOME_CLIENT_RESTARTED,
    GNOME_CLIENT_RESTORED
} GnomeClientFlags;

/* gnomelclient.c */
#include <gnome.h>

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data);
gint eventSaveYourself(GnomeClient *client, gint phase, GnomeSaveStyle sStyle, gint isShutdown, GnomeInteractStyle iStyle, gint isFast, gpointer data);
```

```c
int main(int argc, char *argv[])
{
    int i;
    GtkWidget *app;
    GnomeClient *client;
    GtkWidget *label;
    GtkWidget *box;
    char string[80];

    gnome_init("gnomeclient", "1.0", argc, argv);
    app = gnome_app_new("gnomeclient", "GnomeClient");
    gtk_container_set_border_width(GTK_CONTAINER(app), 20);
    gtk_signal_connect(GTK_OBJECT(app), "delete_event", GTK_SIGNAL_FUNC(eventDelete), NULL);
    gtk_signal_connect(GTK_OBJECT(app), "destroy", GTK_SIGNAL_FUNC(eventDestroy), NULL);

    client = gnome_master_client();
    gtk_signal_connect(GTK_OBJECT(client), "save_yourself", GTK_SIGNAL_FUNC(eventSaveYourself), argv[0]);

    box = gtk_vbox_new(FALSE, 0);
    for (i = 0; i < argc; i++) {
        sprintf(string, "argv[%d]=%s", i, argv[i]);
        label = gtk_label_new(string);
        gtk_box_pack_start(GTK_BOX(box), label, FALSE, FALSE, 0);
    }

    gnome_app_set_contents(GNOME_APP(app), box);
    gtk_widget_show_all(app);
    gtk_main();
    exit(0);
}

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data) {
    return(FALSE);
}

gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data) {
    gtk_main_quit();
    return(0);
}

gint eventSaveYourself(GnomeClient *client, gint phase, GnomeSaveStyle sStyle, gint isShutdown, GnomeInteractStyle iStyle, gint isFast, gpointer data)
{
    guint argc;
    char *argv[2];

    argc = 2;
    argv[0] = (gchar *)data;
    argv[1] = "MyRestartValue";

    gnome_client_set_clone_command(client, argc, argv);
    gnome_client_set_restart_command(client, argc, argv);

    return(TRUE);
}
```

此示例使用垂直框来容纳一列标签，每个标签显示命令行中的一个参数。当程序首次运行时，其窗口外观如图 22-4 所示。如果用户关闭程序（通过菜单中的“关闭”选项或右上角的按钮），则不会保存任何配置信息。然而，如果用户注销并选择保存配置，则会向程序发送 `save_yourself` 信号。下一次用户登录时，程序会自动启动，并接收之前保存的信息。命令行的信息使窗口外观如图 22-5 所示。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_680_0.png)

图 22-4：没有客户端参数的命令行

![](img/8bcc1ba72831c7d67cfc8b395deab95f_680_1.png)

图 22-5：包含先前保存参数的命令行

## GnomeColorPicker

`GnomeColorPicker` 按钮会弹出一个 `GtkColorSelectionDialog`，允许选择颜色。该按钮的颜色会变为当前选定的颜色以进行匹配。

### 继承关系

```text
GnomeColorPicker->GtkButton->GtkBin->GtkContainer->GtkWidget->GtkObject
```

### 函数

```c
void gnome_color_picker_get_d(GnomeColorPicker *cp, gdouble *r, gdouble *g, gdouble *b, gdouble *a);
void gnome_color_picker_get_116(GnomeColorPicker *cp, gushort *r, gushort *g, gushort *b, gushort *a);
void gnome_color_picker_get_18(GnomeColorPicker *cp, guint8 *r, guint8 *g, guint8 *b, guint8 *a);
GtkWidget gnome_color_picker_get_type(void);
GtkWidget *gnome_color_picker_new(void);
void gnome_color_picker_set_d(GnomeColorPicker *cp, gdouble r, gdouble g, gdouble b, gdouble a);
void gnome_color_picker_set_dither(GnomeColorPicker *cp, gboolean dither);
void gnome_color_picker_set_116(GnomeColorPicker *cp, gushort r, gushort g, gushort b, gushort a);
void gnome_color_picker_set_18(GnomeColorPicker *cp, guint8 r, guint8 g, guint8 b, guint8 a);
void gnome_color_picker_set_title(GnomeColorPicker *cp, const gchar *title);
void gnome_color_picker_set_use_alpha(GnomeColorPicker *cp, gboolean use_alpha);
```

GnomeColorPicker 的默认初始颜色为黑色。有一些函数可用于设置和获取当前颜色。以下示例创建一个 GnomeColorPicker，它显示为一个按钮。当被选中时，它会弹出颜色选择对话框，如图 22-6 所示。

```c
static GtkWidget *makeWidget()
{
    GtkWidget *colorpicker;

    colorpicker = gnome_color_picker_new();
    return(colorpicker);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_681_0.png)

**图 22-6：** 由 GnomeColorPicker 控制的颜色选择对话框

## GnomeEntryEdit

GnomeEntryEdit 对象可以插入到 GtkNotebook 中的两个页面中。这两个页面允许用户编辑显示在系统菜单中的应用程序和目录信息。这包括程序名称、启动程序的命令以及帮助文档的位置。

### 继承关系

```text
GnomeEntryEdit->GtkObject
```

### 函数

```c
void gnome_dentry_edit_clear(GnomeEntryEdit *dee);
void *gnome_dentry_edit_get_icon(GnomeEntryEdit *dee);
gchar *gnome_dentry_edit_get_name(GnomeEntryEdit *dee);
guint gnome_dentry_edit_get_type(void);
void gnome_dentry_edit_load_file(GnomeEntryEdit *dee, const gchar *path);
GtkObject *gnome_dentry_edit_new(void);
GtkObject *gnome_dentry_edit_new_notebook(GtkNotebook *notebook);
void gnome_dentry_edit_set_dentry(GnomeEntryEdit *dee, GnomeDesktopEntry *dentry);
GtkWidget *gnome_dentry_get_comment_entry(GnomeEntryEdit *dee);
GnomeDesktopEntry *gnome_dentry_get_icon_entry(GnomeEntryEdit *dee);
GnomeDesktopEntry *gnome_dentry_get_doc_entry(GnomeEntryEdit *dee);
GtkWidget *gnome_dentry_get_exec_entry(GnomeEntryEdit *dee);
GtkWidget *gnome_dentry_get_icon_entry(GnomeEntryEdit *dee);
GtkWidget *gnome_dentry_get_name_entry(GnomeEntryEdit *dee);
GtkWidget *gnome_dentry_get_tryexec_entry(GnomeEntryEdit *dee);
```

虽然 GnomeEntryEdit 对象不是一个小部件，但它包含一些小部件。这些小部件被组织在一起，形成插入到 GtkNotebook 中的两个页面。GtkNotebook 小部件用于显示由 GnomeEntryEdit 对象添加的两个页面。以下示例创建一个空的 GnomeEntryEdit 对象并将其插入到笔记本中，如图 22-7 所示。

```c
static GtkWidget *makeWidget()
{
    GtkObject *dentryedit;
    GtkWidget *notebook;

    notebook = gtk_notebook_new();
    dentryedit = gnome_dentry_edit_new_notebook(GTK_NOTEBOOK(notebook));

    return(notebook);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_683_0.png)

图 22-7：位于 GtkNotebook 内部的双页 GnomeEntryEdit 对象

## GnomeDialog

你可以使用 GnomeDialog 小部件来构建自定义的对话框。对话框在其自己的顶层窗口中创建。它使用垂直框作为容器，并能够在框的底部插入一行标准按钮。你的应用程序可以将其他小部件打包到框的顶部。

GnomeMessageBox 是 GnomeDialog 的封装，简化了接口。此外，第 3 章提供了一组预定义对话框的示例和信息。

### 继承关系

```text
GnomeDialog->GtkWindow->GtkBin->GtkContainer->GtkWidget->GtkObject
```

### 函数

```c
void gnome_dialog_append_button(GnomeDialog *dialog, const gchar *button_name);
void gnome_dialog_append_button_with_pixmap(GnomeDialog *dialog, const gchar *button_name, const gchar *pixmap_name);
void gnome_dialog_append_buttons(GnomeDialog *dialog, const gchar *first, ...);
void gnome_dialog_append_buttons_with_pixmaps(GnomeDialog *dialog, const gchar **names, const gchar **pxmaps);
void gnome_dialog_append_buttonsv(GnomeDialog *dialog, const gchar **buttons);
void gnome_dialog_button_connect(GnomeDialog *dialog, gint button, GtkSignalFunc callback, gpointer data);
void gnome_dialog_button_connect_object(GnomeDialog *dialog, gint button, GtkSignalFunc callback, GtkObject *obj);
void gnome_dialog_close(GnomeDialog *dialog);
void gnome_dialog_close_hides(GnomeDialog *dialog, gboolean just_hide);
```

