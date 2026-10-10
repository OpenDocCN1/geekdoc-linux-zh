
## 3-6 简单问题对话框

```c
/** questiondialog.c **/
#include <gnome.h>

void cbfunction(gint reply,gpointer data);

int main(int argc,char *argv[])
{
    gnome_init("questiondialog","1.0",argc,argv);

    gnome_question_dialog("A simple question window",
                    (GnomeReplyCallback)cbfunction,
                    NULL);

    gtk_main();
    exit(0);
}
void cbfunction(gint reply,gpointer data) {
    if(reply == GNOME_YES)
       g_print("The answer is YES\n");
    else
       g_print("The answer is NO\n");
}
```

该程序显示的窗口如图 3-6 所示。第 10 行的函数调用创建并显示对话框。回调函数 `cbfunction()` 的名称被传递给对话框，因此，当用户选择 **YES** 或 **NO** 按钮时，该函数会被调用以通知程序用户的选择。第 17 行的 `cbfunction()` 函数由对话框调用，它携带一个保存回复值的整数和在第 12 行传入的数据指针的副本。关于这个数据指针存在是有原因的——有时回调函数执行的操作需要访问数据，而不是将数据设为全局变量，可以将其作为参数传入。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_72_0.png)

当问题得到回答时，*reply* 参数的值是 **GNOME_YES** 或 **GNOME_NO**。一个重要的点：你*必须*使用命名常量来测试 *reply* 值，因为实际值与标准 C 语言中的数字 true 和 false 测试是相反的。这将给你一个意外的答案：

```c
if(reply) . . .      /* wrong **/
```

有四个这样的常量值。常量值 GNOME_OK 与 GNOME_YES 相同，GNOME_CANCEL 与 GNOME_NO 相同。

这里有一个示例，它询问与图 3-6 中之前显示相同的问题，但这次对话框是模态的，并与父窗口相关联：

```c
/** qmpdialog.c **/
#include <gnome.h>

void yes_or_no(gint reply,gpointer data);

int main(int argc,char *argv[]) {
    GtkWidget *app;
    GtkWidget *dialog;
    GtkWidget *button;

    gnome_init("qmpdialog","1.0",argc,argv);
    app = gnome_app_new("qmpdialog","Question Dialog");
    button = gtk_button_new_with_label("Button");
    gtk_container_set_border_width(GTK_CONTAINER(app),30);
    gnome_app_set_contents (GNOME_APP(app),button);
    gtk_widget_show(button);
    gtk_widget_show(app);

    dialog = gnome_question_dialog_modal_parented(
        "A simple question window",
        (GnomeReplyCallback)yes_or_no,
        NULL,
        GTK_WINDOW(app));

    gtk_main();
    exit(0);
}
void yes_or_no(gint reply,gpointer data) {
    if(reply == GNOME_YES)
        g_print("The answer is YES\n");
    else
        g_print("The answer is NO\n");
}
```

这个示例显示了一个带有按钮的主窗口，并弹出问题对话框。第 20 行的函数调用创建了对话框，以应用程序的主窗口作为其父窗口，并将对话框显示为模态。由于对话框是父化的，主窗口（及其父窗口，如果有的话）永远无法遮挡该对话框。这也意味着当主窗口从一个位置移动到另一个位置时，对话框也随之移动。作为模态对话框，该对话框阻止应用程序主窗口上的按钮变得敏感。换句话说，在用户能够继续其他操作之前，必须先回答该问题。模态性仅适用于该单一应用程序，并发运行的应用程序显示的窗口不受影响。

## 3-7 确认对话框

还有另外两个函数调用可用于创建问题对话框窗口。在某些情况下，你可能希望有一个模态窗口，但不附带父窗口。为了做到这一点，将第 20 行至第 24 行更改为以下内容：

```c
dialog = gnome_question_dialog_modal(
      "A simple question window",
      (GnomeReplyCallback)yes_or_no,
      NULL);
```

结果是，其余的窗口变得不活动，并且不响应鼠标。请谨慎使用此方法，因为当应用程序窗口不活动时，该对话框可能会从视野中隐藏，导致用户困惑。要创建一个保持在父窗口之上但不禁用应用程序中任何窗口的问题对话框，将第 20 行至第 24 行更改为以下内容：

```c
dialog = gnome_question_dialog_parented(
      "A simple question window",
      (GnomeReplyCallback)yes_or_no,
      NULL,
      GTK_WINDOW(app));
```

### 你确定吗？

程序向用户询问的一个非常常见的问题是，是否应该执行请求的操作。这种类型的问题有其自己的对话框，带有 OK 和 CANCEL 按钮，如图 3-7 所示。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_74_0.png)

执行此功能的函数调用与上一个示例中的问题函数非常相似：

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

由于第 20 行创建对话框的函数调用指定了模态对话框，因此在显示该对话框期间主窗口上的按钮会被禁用。此外，由于创建的对话框是父化的，主窗口无法隐藏该对话框。但是，还有其他函数调用可用于创建非模态和/或非父化对话框。只需将第 20 行至第 24 行替换为以下其中一种形式即可。要创建一个父化但非模态的对话框，请使用以下形式：

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
