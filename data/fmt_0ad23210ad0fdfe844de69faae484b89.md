
你稍后会看到这些函数的含义，但现在请观察宏的使用。每一个可以想象到的类型转换都存在宏。

> 如果觉得这一切毫无意义，不要担心；你不需要了解面向对象编程的细节就能掌握 `GNOME/GTK+`。事实上，这是一种无痛的方法，让你在舒适的 C 语言环境中学习面向对象背后的思想和益处。

`GNOME` 是 `GNU` 图像处理程序 (`GIMP`) 于 1997 年启动的一个项目的名称，旨在为 `Linux` 创建一个统一的桌面。当时达成了一个共识，即采用 `Linux` 作为桌面平台的阻碍在于缺乏连贯的策略。当时，`Linux` 桌面就像荒野西部，没有整体标准或约定的规范。

`GTK+` 许可证提供的自由与其竞争对手 `Qt`（下一章的主题）形成了对比，后者的 `GPL` 许可证禁止使用 `Qt` 开发商业软件。

## 使用 GTK+ 编程 GNOME

在本章中，我们将使用 `GNOME/GTK+ 2`，因此请确保你的安装包含了 `2.x` 库。对于使用 `RPM` 的发行版，你至少应该拥有以下 `RPM`：

- `gtk2-2.2.1-4.rpm`
- `gtk2-engines-1.1.8-5.rpm`
- `gtk2-devel-2.2.1-4.rpm`
- `libnome-2.2.0.1-8.rpm`
- `libnomeui-2.2.0.1-5.rpm`
- `libgnome-devel-2.2.0.1-8.rpm`
- `libgnome-devel-2.2.0.1-5.rpm`

在 `Debian` 中，你可以使用 `apt-get` 从各种镜像安装 `GNOME/GTK+` 软件包——详情请参考 `http://www.gnome.org` 的链接。

要检查一切是否安装正确，可以在命令行上运行 `pkg-config`：

```bash
$ pkg-config
```

`pkg-config` 是一个查找系统中 `GTK` 和 `GNOME` 配置的方便工具。注意，`pkg-config` 取代了 `GTK+ 1.x` 自带的 `gtk-` 工具。

还可以尝试 `GTK+` 演示应用程序，它展示了所有的部件（见图 16-3）：

```bash
$ gtkk-demo Code Demos
```

## 尝试一下——一个简单的 GtkWindow

让我们从简单的 `GUI` 程序开始学习 `GTK+` 编程：显示一个窗口。我们将看到 `GTK+` 库的运行情况，并看到通过极少的代码就能获得如此强大的功能。

1. 输入此程序并将其命名为 `gtk1.c`：

```c
#include <gtk/gtk.h>

int main (int argc, char *argv[])
{
    GtkWidget *window;

    gtk_init(&argc, &argv);

    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);

    gtk_widget_show(window);

    gtk_main();

    return 0;
}
```

2. 要编译 `gtk1.c`，输入：
`$ gcc gtk1.c -o gtk1 `pkg-config --cflags -libs gtk+-2.0``

注意输入的是反引号（backticks），而不是单引号（apostrophes）——记住反引号是告诉 shell 执行并追加所包含命令输出输出的指令。

当我们使用以下命令运行该程序时，你的窗口应该弹出（见图 16-4）：

`$ ./gtk1.c`

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_672_0.png)

注意我们可以调整大小、最小化和最大化窗口。

## 工作原理

我们通过一条 `<gtk/gtk.h>` 语句包含了必要的 `GTK+` 和相关库头文件（包括 `GLib`）。接下来，我们声明窗口为指向 `GtkWidget` 的指针。

接着，为了初始化 `GTK+` 库，我们必须调用 `gtk_init` 并传递命令行参数和 `argv`。这让 `GTK+` 有机会解析它需要获知的的任何命令行参数。注意，在调用任何 `GTK+` 函数之前，我们必须始终以这种方式初始化 `GTK+`。

示例的核心是我们对 `gtk_window_new` 的调用。其原型为：

```c
GtkWidget* gtk_window_new (GtkWindowType type);
```

`type` 根据窗口的目的可以取两个值之一：

- `GTK_WINDOW_TOPLEVEL`：带边框的标准窗口
- `GTK_WINDOW_POPUP`：适用于对话框的无框窗口

我们将始终使用 `GTK_WINDOW_TOPLEVEL` 在内存中设置窗口，这样在实际上在屏幕上显示它之前，我们有机会向其中填充对话框、调整大小、更改窗口等。为了让窗口真正显示在屏幕上，我们调用 `gtk_widget_show`：

```c
gtk_widget_show(window);
```

方便的是，它接受一个 `gtk*` 指针，所以我们只需要传递窗口的引用即可。

最后的调用是执行 `gtk_main`。这个关键函数通过将控制权交给 `GTK+` 来启动交互过程，并在调用 `gtk_main_quit` 之前不会返回。正如你所见，在 `gtk1.c` 中这从未发生过，因此即使窗口关闭后应用程序也不会结束。我们通过点击关闭图标来尝试，发现命令行提示符没有返回。我们将在下一节学习信号（signals）和回调（callbacks）后纠正这个问题。

## 事件、信号和回调

所有的 `GUI` 库都有一个共同点：必须有一种机制来响应用户操作执行代码。命令行程序可以停止执行等待输入，然后使用类似 `switch` 语句的方法根据输入进行分支执行。这种方法在 `GUI` 中是不实用的，因为应用程序必须不断响应用户输入；例如，

现代窗口系统拥有事件和事件监听器系统来解决这个问题。其核心思想是每次输入（通常来自鼠标或键盘）都会触发一个事件。例如，按下键盘会触发一个“键盘事件”。然后编写代码来监听这些事件并在事件被触发时执行操作。

正如我们将看到的，`X` 窗口系统发出这些事件，但对我们这些 `GTK+` 程序员来说，这些事件并没太大帮助，因为它们太底层了。当点击鼠标按钮时，`X` 会发出一个包含指针坐标的事件——而我们真正需要知道的是用户激活某个部件（widget）的时机。

## 使用 GTK+ 编写 GNOME

因此，`GTK+` 有它自己的事件和监听器系统，被称为信号和回调。它们非常易用，因为你可以使用 C 语言中一个非常有用的特性——函数指针来设置信号处理器。

首先是一些定义：当发生用户输入等情况时，`GObject` 会发出一个 `GTK+` 信号。连接到信号并在每次信号发出时被调用的函数被称为回调函数（callback function）。

注意，`GTK+` 信号与第 11 章讨论的 `UNIX` 信号是完全不同的。

作为一名 `GTK+` 程序员，你只需要担心编写和连接回调函数，因为发射信号的代码是该特定部件内部的。

回调函数的原型通常如下：

```c
void a_callback_function ( GtkWidget *widget, gpointer user_data );
```

我们接收到两个参数：第一个指针用于连接到发射信号的部件，第二个指针是我们在连接回调时自行选择的任意指针。我们可以将此指针用于任何目的。

连接回调非常简单：我们只需调用 `g_signal_connect` 并传递部件、字符串形式的信号名称、回调函数和任意指针即可。

```c
g_signal_connect(gpointer object, const gchar *name, GCallback func, gpointer user_data);
```

## 事件、信号和回调（继续）

```c
#include <gtk/gtk.h>

#include <stdio.h>

static int count = 0;

void button_clicked(GtkWidget *widget, gpointer data) {
    printf("%s pressed %d time\n", (char*)data, ++count);
}

int main (int argc, char *argv[]) {
    GtkWidget *window;
    GtkWidget *button;

    gtk_init(&argc, &argv);

    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);

    button = gtk_button_new_with_label("Hello World!");

    gtk_container_add(GTK_CONTAINER(window), button);

    g_signal_connect(G_OBJECT(button), "clicked", G_CALLBACK(button_clicked), "Button");

    gtk_widget_show(button);

    gtk_widget_show(window);
}
```
