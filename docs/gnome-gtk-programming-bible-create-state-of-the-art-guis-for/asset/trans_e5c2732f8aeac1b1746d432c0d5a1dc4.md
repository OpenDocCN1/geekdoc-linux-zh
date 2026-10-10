

# 对话框是独立的

弹出窗口或对话框由一个或多个控件组成。*控件* 是一种单用途软件对象，通常用于显示一个窗口。该窗口用于输入、输出或两者兼有。控件可以非常简单（例如一个按钮），也可以相当复杂（例如一个动态大小的下拉选择列表）。虽然也存在一些例外，但大多数控件旨在与其他控件一起包含在窗口中，以定义弹出窗口或对话框界面的布局。

弹出窗口种类繁多。简单的弹出窗口只有一条语句和一个“确定”按钮，而其他的则包含多个标签和其他用于数据输入的控件。通常，一个程序会有一个主窗口，其他所有操作都通过对话框完成，这些对话框在用户鼠标的控制下出现和消失。

当你的程序创建并显示一个对话框时，该对话框会立即独立运行。这种架构是 X 窗口系统基础的一部分。一旦对话框开始运行，创建它的函数就会返回，以便你的程序可以继续运行。你的程序从对话框获取信息的唯一方式，是调用你指定的**可选回调函数**。当然，它可以捕获鼠标以防止访问应用程序中的任何其他窗口，但你的程序不会知道这一点。它只是耐心地等待来自鼠标或键盘的输入。

每个程序都使用相同的函数作为其主循环：

```
gtk_main()
```

此函数调用会等待来自鼠标或键盘的事件。每当有事件到达时，信息会被分派到正确的窗口，该窗口进而可能会调用一个回调函数。如果你编写了一个耗时的回调函数（例如排序一个巨大的文件），那么在你的函数运行期间，鼠标完全不起作用，因为没有事件被读取。虽然有一些方法可以在保持鼠标活跃的同时运行耗时任务（如第 5 章中所述），但我在此想要强调的点是，对话框窗口与你的程序分离，以便 `gtk_main()` 中的事件捕获循环可以继续工作。

# GNOME 定义的对话框

有一组预定义且随时可以显示的对话框。它们是传统的用于告知用户类似“文件未找到！”等信息或询问类似“你确定吗？”等问题时使用的信息框和询问框。

# 制作简单语句

下面的程序表明，只需很少的代码就可以显示一个对话框：

```c
/** okdialog.c **/
#include <gnome.h>

int main(int argc, char *argv[])
{
    gnome_init("okdialog", "1.0", argc, argv);
    gnome_ok_dialog("A simple information window");
    gtk_main();
    exit(0);
}
```

在对话框显示之前，只需调用 gnome_init() 即可。对 gnome_ok_dialog() 的函数调用创建并显示对话框，如 图 3-1 所示。对 gtk_main() 的调用会等待你点击“确定”按钮；当这样做时，对话框就会关闭。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_68_0.png)

此对话框不会向程序反馈任何信息。事实上，程序会一如既往地继续运行，就好像对话框从未显示过一样——它一直保留在屏幕上，直到“确定”按钮被点击，然后悄无声息地消失。

对话框会自动调整大小以适应文本的大小。如果文本太长无法在一行内显示，可以通过插入换行符（如本例中的换行符）使其在下一行继续显示：

```c
/** okmultiple.c **/
#include <gnome.h>

gchar message[] =
    "To display a message on\nmore than one line\n"
    "it is only necessary to insert\na newline character\n"
    "\nWherever you would like the line to break.";

int main(int argc, char *argv[])
{
    gnome_init("okmultiple", "1.0", argc, argv);
    gnome_ok_dialog(message);
    gtk_main();
    exit(0);
}
```

本例生成的多行对话框如 图 3-2 所示。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_69_0.png)

**图 3-2：** 一个包含多行的简单消息弹出窗口

对话框也可以设置为*模态*（modal），这意味着应用程序中的其他窗口不会接受鼠标或键盘输入。以下程序演示了其工作原理：

```c
/** okmddialog.c **/
#include <gnome.h>

int main(int argc, char *argv[])
{
    GtkWidget *app;
    GtkWidget *dialog;
    GtkWidget *button;

    gnome_init("okmdialog", "1.0", argc, argv);
    app = gnome_app_new("okmdialog", "Okay Dialog");
    button = gtk_button_new_with_label("Button");
    gtk_container_set_border_width(GTK_CONTAINER(app), 30);
    gnome_app_set_contents(GNOME_APP(app), button);
    gtk_widget_show(button);
    gtk_widget_show(app);

    dialog = gnome_ok_dialog(
            "A simple information window");
    gtk_window_set_modal(GTK_WINDOW(dialog), TRUE);

    gtk_main();
    exit(0);
}
```

该程序显示之前 图 3-1 中展示的对话框，同时也显示 图 3-3 中的窗口。第 10 到 20 行创建并显示主窗口及其按钮。当主窗口和对话框都显示时，由于第 20 行对 gtk_window_set_modal() 的调用，只有对话框中的按钮对鼠标做出反应。主窗口中的按钮会忽略鼠标操作，直到对话框的“确定”按钮被点击且对话框关闭。在此之后，主窗口中的按钮恢复正常工作。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_70_0.png)

**图 3-3：** 主窗口的按钮

第 15 和 16 行显示按钮和应用程序控件。在此示例中，按钮控件在其父控件（即应用程序控件）之前显示。如果 gtk_widget_show() 调用的顺序颠倒，最终结果是一样的——但在屏幕上绘制控件的过程会有所不同。我将在本章后面详细讨论这一点。

第 18 到 20 行创建并显示对话框的代码不需要应用程序窗口作为参数。这意味着你可以轻松地在程序的任意位置创建对话框，并且该对话框可以中止应用程序内所有窗口的活动，直到对话框被确认。

第 15 和 16 行对 gtk_widget_show() 的调用可以是任意顺序。事实是，如果应用程序控件没有显示，按钮控件根本不会显示，因为第 14 行对 gnome_app_set_contents() 的调用将按钮放置在应用程序控件内部。一般来说，以这种方式从内向外显示控件更好，因为整个窗口及其所有控件会同时出现。对于一个大型窗口（包含大量控件的窗口），如果先显示外层窗口，控件可能会在包含窗口首次出现后依次逐个显示。

到目前为止，对话框窗口是一个自由体，鼠标可以将其放置在显示器上其他任何窗口的前面或后面。此示例表明，如果对话框有一个父窗口，它始终保持在父窗口的前面。当使用模态对话框时，这一点尤其有意义，因为父窗口本来就是非活动状态，隐藏对话框可能会导致混乱。你可以通过将第 18 和 19 行更改为以下内容来修改程序：

```
dialog = gnome_ok_dialog_parented( 
  "A simple information window", 
  GTK_WINDOW(app));
```

这会使应用程序窗口成为对话框的父窗口。任何窗口都可以是一个或多个子窗口的父窗口，因此你可以使用这种相同的技术为应用程序中的任何窗口弹出对话框。

还有另外两个与“确定”对话框窗口工作方式相同的对话框窗口。警告和错误对话框窗口都具有父窗口和非父窗口模式，并且都可以是模态或非模态的。要显示 图 3-4 中所示的错误窗口，请将第 18 和 19 行更改为以下内容：

```
dialog = gnome_error_dialog_parented(
    "A simple error window",
    GTK_WINDOW(app));
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_71_0.png)

简单“确定”弹出窗口的第三种形式是警告，如 图 3-5 所示。显示代码与其他形式相同：

```
dialog = gnome_warning_dialog_parented(
    "A simple warning window",
    GTK_WINDOW(app));
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_71_1.png)

### 提出一个简单问题

要从对话框中获取“是”或“否”的回答，有必要弄清楚用户做了哪两种选择。响应通过一个回调函数来捕获。下面是一个显示问题对话框并捕获响应的程序示例：

