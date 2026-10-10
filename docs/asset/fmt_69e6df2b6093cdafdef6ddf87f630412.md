
`gint argc, gchar *argv[]`)

`void gnome_client_set_restart_command(GnomeClient *client,`

`gint argc, gchar *argv[])`

`void gnome_client_set_restart_style(GnomeClient *client,`

`GnomeRestartStyle style)`

`void gnome_client_set_shutdown_command(GnomeClient *client,`

`gint argc, gchar *argv[])`

`void gnome_client_set_user_id(GnomeClient *client,`

`const gchar *id)`

`GnomeClient *gnome_cloned_client(void)`

`void gnome_interaction_key_return(gint tag,`

`gboolean cancel_shutdown)`

`GnomeClient *gnome_master_client(void)`

### 枚举

```c
typedef enum {
GNOME_INTERACT_NONE,
GNOME_INTERACT_ERRORS,
GNOME_INTERACT_ANY
} GnomeInteractStyle;
```

## GnomeClient

以下示例在用户注销时响应 `GtkObject` 中的 `"save_yourself"` 信号，并调用函数 `eventSaveYourself()`。此函数创建一个命令行参数数组，用于在程序停止的位置重启该程序。

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
