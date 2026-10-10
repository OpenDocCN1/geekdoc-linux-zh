
```c
/** canmpdialog.c **/
#include <gnome.h>

void cancel_or_ok(gint reply,gpointer data);

int main(int argc,char *argv[])
{
    GtkWidget *app;
    GtkWidget *dialog;
    GtkWidget *button;

    gnome_init("canmpdialog", "1.0", argc, argv);
    app = gnome_app_new("canmpdialog", "Question Dialog");
    button = gtk_button_new_with_label("Button");
    gtk_container_set_border_width(GTK_CONTAINER(app), 30);
    gnome_app_set_contents(GNOME_APP(app), button);
    gtk_widget_show(button);
    gtk_widget_show(app);

    dialog = gnome_ok_cancel_dialog_modal_parented(
        "Do you really want to do this?",
        (GnomeReplyCallback)cancel_or_ok,
        NULL,
        GTK_WINDOW(app));

    gtk_main();
    exit(0);
}
void cancel_or_ok(gint reply, gpointer data) {
    if(reply == GNOME_CANCEL)
        g_print("Action cancelled\n");
    else
        g_print("Action okayed\n");
}
```

由于第 20 行创建对话框的函数调用指定了模态对话框，因此在显示该对话框期间主窗口上的按钮会被禁用。此外，由于创建的对话框是父化的，主窗口无法隐藏该对话框。但是，还有其他函数调用可用于创建非模态和/或非父化对话框。只需将第 20 行至第 24 行替换为以下其中一种形式即可。

要创建一个父化但非模态的对话框，请使用以下形式：

```c
dialog = gnome_ok_cancel_dialog_parented(
        "Do you really want to do this?",
        (GnomeReplyCallback)cancel_or_ok,
        NULL,
        GTK_WINDOW(app));
```

要创建一个模态但非父化的对话框，请使用以下形式：

```c
dialog = gnome_ok_cancel_dialog_modal(
        "Do you really want to do this?",
        (GnomeReplyCallback)cancel_or_ok,
        NULL,
        GTK_WINDOW(app));
```

要创建一个既非父化也非模态的对话框，请使用以下形式：

```c
dialog = gnome_ok_cancel_dialog(
    "Do you really want to do this?",
    (GnomeReplyCallback)cancel_or_ok,
    NULL,
    GTK_WINDOW(app));
```

## 键盘输入

你可以使用一个对话框直接从键盘获取输入。它提示输入单个字符串，例如文件名或网站 URL。该程序演示了字符串对话框：

```c
/** stringdialog.c **/
#include <gnome.h>

void stringCallback(gchar *string,gpointer data);

int main(int argc,char *argv[])
{
    GtkWidget *app;
    GtkWidget *dialog;
    GtkWidget *button;

    gnome_init("stringdialog","1.0",argc,argv);
    app = gnome_app_new("stringdialog","String Dialog");
    button = gtk_button_new_with_label("Button");
    gtk_container_set_border_width(GTK_CONTAINER(app),30);
    gnome_app_set_contents(GNOME_APP(app),button);
    gtk_widget_show(button);
    gtk_widget_show(app);

    dialog = gnome_request_string_dialog(
                "File name",
                (GnomeStringCallback)stringCallback,
                NULL);
    gtk_window_set_modal(GTK_WINDOW(dialog),TRUE);

    gtk_main();
    exit(0);
}
void stringCallback(gchar *string,gpointer data)
{
    if(string != NULL)
       g_print("Called back with a NULL string\n");
    else if(strlen(string) == 0)
       g_print("Called back with a zero-length string\n");
    else
       g_print("GOT: %s\n",string);
}
```

第 20 行对 `gnome_request_string_dialog()` 的调用创建并显示了对话框，如图 3-8 所示。创建时，该对话框被分配了回调函数 `stringCallback()`，该函数定义在第 29 行。表 3-1 描述了用户可以采取的四种操作及其每种操作的结果。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_77_0.png)

### 图 3-8：用户输入提示

#### 表 3-1

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
