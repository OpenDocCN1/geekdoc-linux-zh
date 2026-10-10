

第 20 行对 `gnome_request_string_dialog()` 的调用创建并显示了对话框，如图 3-8 所示。创建时，该对话框被分配了回调函数 `stringCallback()`，该函数定义在第 29 行。表 3-1 描述了用户可以采取的四种操作及其每种操作的结果。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_77_0.png)

## 图 3-8：用户输入提示

### 表 3-1
**用户响应结果**

| 操作 | 回调中的结果 |
| :--- | :--- |
| 输入字符串并选择确定 | 输入的字符串传递给回调 |
| 字符串留空并选择确定 | 一个零长度字符串传递给回调 |
| 字符串留空并选择取消 | 一个 NULL 字符串指针传递给回调 |
| 输入字符串并选择取消 | 一个 NULL 字符串指针传递给回调 |

没有函数可以创建模态字符串对话框，但你可能会觉得拥有一个模态字符串请求更方便。示例程序中的对话框之所以是模态的，是因为在第 24 行调用了 `gtk_window_set_modal()`。有一个函数调用可用于创建父级对话框——只需将第 20 行至第 23 行更改为以下内容：

```
dialog = gnome_request_string_dialog_parented(
    "File name",
    (GnomeStringCallback)stringCallback,
    NULL,
    GTK_WINDOW(app));
```

还有另外两个创建接受字符串输入的对话框的函数，但有一个不同之处。输入的文本不会回显到屏幕上。窗口将为输入的每个字符显示一个星号，如图 3-9 所示。你可以通过将第 20 行至第 23 行更改为以下内容，来修改提示可见字符串输入的程序，使其提示为遮蔽字符串输入：

```
dialog = gnome_request_password_dialog(
    "Password",
    (GnomeStringCallback)stringCallback,
    NULL);
```

你可以这样创建一个父级版本：

```
dialog = gnome_request_password_dialog_parented(
    "Password",
    (GnomeStringCallback)stringCallback,
    NULL,
    GTK_WINDOW(app));
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_78_0.png)

有时，你需要对输入字符串对话框有更多的控制。你可能希望指定输入字符串的最大长度，或者用默认值初始化对话框输入。使用此示例中的函数调用来实现：

```c
/** requestdialog.c **/
#include <gnome.h>

void requestCallback(gchar *string,gpointer data);

int main(int argc,char *argv[])
{
    GtkWidget *app;
    GtkWidget *dialog;
    GtkWidget *button;

    gnome_init("requestdialog","1.0",argc,argv);
    app = gnome_app_new("requestdialog","Request Dialog");
    button = gtk_button_new_with_label("Button");
    gtk_container_set_border_width(GTK_CONTAINER(app),30);
    gnome_app_set_contents(GNOME_APP(app),button);
    gtk_widget_show(button);
    gtk_widget_show(app);

    dialog  = gnome_request_dialog(FALSE,
            "File name",
            "/var/tmp/workfile.dat",
            36,
            (GnomeStringCallback)requestCallback,
            NULL,
            GTK_WINDOW(app));
    gtk_window_set_modal(GTK_WINDOW(dialog),TRUE);

    gtk_main();
    exit(0);
}

void requestCallback(gchar *string,gpointer data)
{
    if(string == NULL)
        g_print("Called back with a NULL string\n");
    else if(strlen(string) == 0)
        g_print("Called back with a zero-length string\n");
    else
        g_print("GOT: %s\n",string);
}
```

第 20 行对 `gnome_request_dialog()` 的调用创建了图 3-10 中显示的对话框。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_79_0.png)

第一个参数是 TRUE 或 FALSE，用于指示输入字符串是否需要遮蔽（如密码那样）。如果值为 TRUE，则初始值和用户键入的任何字符都会显示为星号字符串。第二个参数是显示提示，第三个是插入到文本字段中的默认字符串值，作为对话框首次出现时的内容。如果不需要初始值，你可以传入 NULL 或零长度字符串。

本示例中的下一个参数位于第 23 行，它是输入字段中允许的最大字符数。如果你不希望限制字符数量，最大请使用 0。字符数量可以超过数据输入窗口能容纳的数量，因为窗口可以前后滚动以允许数据输入。

最后两个参数与前面的示例相同。第 25 行是传递给回调例程的数据指针，最后一个参数是将成为此窗口父级的窗口。如果你不想让对话框拥有父级，请传入 NULL 指针作为父窗口。

## 向回调传递数据

如前几个示例所示，有一个机制可以将数据指针传递给 GNOME 函数，该函数随后传递给回调函数。GNOME 和 GTK* 完全忽略此数据指针，这意味着你可以传入任何你喜欢的地址。在一个程序中进行多个相关决策时，传递此指针的能力可能非常有用。

例如，如果程序通过弹出对话框询问文件名来响应 **另存为** 菜单选择，回调函数可能需要访问当前文件名以及用户选择的文件名。当然，这可以通过将所有信息存储在全局变量中来完成，但从控制和设计的角度来看，通常认为将数据作为参数传递更好。但是，由于你不直接从程序中调用回调函数，因此需要间接传递参数，如下例所示：

```c
/* datacallback.c **/
#include <gnome.h>

typedef struct {
    GtkWidget *app;
    gchar defaultFilename[40];
    gchar currentFilename[40];
} pgmContext;

gint eventDelete(GtkWidget *widget,
    GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget,
    GdkEvent *event, gpointer data);
void saveAsButton(GtkWidget *widget, pgmContext *pc);
void fileSaveCallback(gchar *filename, pgmContext *pc);

int main(int argc, char *argv[]) {
    GtkWidget *button;
    pgmContext pc;

    strcpy(pc.defaultFilename, "/var/dcall/sqLIM.dat");

    gnome_init("datacallback", "1.0", argc, argv);
    pc.app = gnome_app_new("datacallback", "Data Passing");
    setTermination(pc.app);

    button = gtk_button_new_with_label(
        "Save As");
    gtk_signal_connect(GTK_OBJECT(button),
        "clicked",
        GTK_SIGNAL_FUNC(saveAsButton),
        &pc);
    gnome_app_set_contents (GNOME_APP(pc.app),button);

    gtk_container_set_border_width
            (GTK_CONTAINER(pc.app),30);
    gtk_widget_show(button);
    gtk_widget_show(pc.app);
    gtk_main();
    exit(0);
}

void saveAsButton(GtkWidget *widget,pgmContext *pc) {
    GtkWidget *dialog;

    dialog = gnome_request_dialog(FALSE,
                                "File name",
                                pc->defaultFilename,
                                40,
                                (GnomeStringCallback)fileSaveCallback,
                                pc,
                                GTK_WINDOW(pc->app)));
    gtk_window_set_modal(GTK_WINDOW(dialog),TRUE);
}

void fileSaveCallback(gchar * filename,pgmContext *pc) {
    if((filename == NULL) || (strlen(filename) == 0))
        return;
    strcpy(pc->currentFilename, filename);
    g_print("Save file as %s\n",pc->currentFilename);
}

void setTermination(GtkWidget *app) {
    gtk_signal_connect(GTK_OBJECT(app),
                        "delete_event",
                        GTK_SIGNAL_FUNC(eventDelete),
                        NULL);
    gtk_signal_connect(GTK_OBJECT(app),
                        "destroy",
                        GTK_SIGNAL_FUNC(eventDestroy),
                        NULL);
}

gint eventDelete(GtkWidget *widget,
                GdkEvent *event,gpointer data) {
    return(FALSE);
}

gint eventDestroy(GtkWidget *widget,
                  GdkEvent *event,gpointer data) {
    gtk_main_quit();
    return(0);
}
```

此程序显示一个带有单个按钮的窗口，如图 3-11 所示。

