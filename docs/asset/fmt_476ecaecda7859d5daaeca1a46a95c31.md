
本教程描述了 GTK 的接口。GTK 有许多其他语言的绑定，如 C++、Go、Perl、Python、Ada、Objective C、Pascal 和 Eiffel。如果你想使用其他语言的 GTK 绑定，请查阅该绑定的文档。在某些情况下，文档可能会描述一些重要的约定（你应该先了解这些），然后引导你参考本教程。对于某些跨平台 API（如 Windows 和 X），你可以将 GTK 作为它们的平台之一使用；同样，请考虑它们的文档。

如果你在 C++ 中开发 GTK 应用程序，需要一些额外的支持。有一个名为 `gtkmm` 的 GTK C++ 绑定，它为 GTK 提供了类似 C++ 的接口；你可能应该考虑使用这个。如果你出于某种原因不喜欢那种方法，也有使用 GTK 的替代方案。首先，你可以在与 GTK 交互时使用 C++ 的子集并使用 C 接口。其次，通过将所有回调声明为 C++ 类中的函数来使用 GTK 和 C++，再次使用 C 调用 GTK。如果你选择最后这种方法，可以将回调的数据值包含在要操作的对象中（所谓的 "this" 值）。选择这些选项仅取决于偏好，因为在所有三种方法中你都可以使用 C++ 和 GTK。这些方法中都不需要使用特殊的预处理器，无论你选择哪种，都可以将标准 C 与 GTK 使用。

本教程旨在尽可能记录 GTK，但绝非完整。本教程假设读者对 C 语言以及如何创建 C++ 程序有良好的理解。读者如果有之前的 X 编程经验将大有益，但并非必须。如果你将 GTK 作为你的第一个组件来学习，请反馈你对本教程的感受以及你是否遇到了困难。请注意，GTK 的 C++ API (`gtk-`) 正在开发中，所以如果你倾向于使用 C++，你应该考虑使用它。还有 Objective C、ADA、Guile 等其他语言的绑定可用，但我不关注这些。

本文档处于“进行中”。请访问 `http://www.gtk.org/` `http://www.gtk.org/` 查找更新。

我非常希望听到任何通过本文档学习 GTK 的反馈，并欢迎关于如何改进的建议。请参见第 25 页更多信息。

# 2 入门

要第一第一是下载 GTK 源码并安装。你可以从 `ftp.gtk.org/pub/gtk` 获取最新版本。你也可以在 `http://www.gtk.org/` 查看关于 GTK 的其他信息。GTK 使用 GNU autoconf 进行配置。配置完成后，输入 `./configure` 查看选项列表。

GTK 源码发行版还包含本教程使用的所有示例源码，以及用于编译的 Makefile。

为了开始介绍 GTK，我们将从最简单的程序开始。该程序将创建一个 200x200 像素的窗口，并且没有 shell 退出方式。

```c
/* example-target base.c */

#include <gtk/gtk.h>
```

## 2.0 示例程序

```c
int main(int argc,
    char *argv[])
{
    Gtkwidget *window;

    gtk_init (&argc, &argv);

    window = gtk_window_new (GTK_WINDOW_TOPLEVEL);
    gtk_widget_show (window);

    gtk_main();

    return(0);
}
/* example-end above */
```

你可以使用 `gcc` 编译上述程序：

```
gcc base.c -o base 'gtk-config --cflags --libs'
```

常用编译选项的含义下文所示。

所有程序都会包含 `gtk/gtk.h`，它声明了在 GTK 应用程序中将使用的变量、函数、结构等。

下一行：

```c
gtk_init (&argc, &argv);
```

调用函数 `gtk_init(int *argc, char ***argv)`，该函数将在所有的 GTK 程序中被调用。它为我们设置了一些默认视觉效果和颜色映射，然后继续调用 `gdk_init(int *argc, char ***argv)`。该函数初始化库以便使用，设置默认信号处理器，并检查传递给应用程序的参数，寻找以下之一：

- `-gtk-module`
- `g-fatal-warnings`
- `gtk-debug`
- `gtk-no-debug`
- `gdk-debug`
- `gdk-no-debug`
- `-display`
- `-sync`
- `-no-xshm`
- `-name`
- `-class`

### 2.1 创建窗口

```c
window = gtk_window_new (GTK_WINDOW_TOPLEVEL);
gtk_widget_show (window);
```

`GTK_WINDOW_TOPLEVEL` 参数指定我们希望窗口由窗口管理器进行装饰和定位。与其创建一个 0x0 大小的窗口，一个没有子部件的窗口默认被设置为 200x200；你仍然可以对其进行操作。

`gtk_widget_show()` 函数让 GTK 知道我们已经完成了对该部件属性的设置，它可以显示了。

最后一行进入了 GTK 主处理循环。

```c
gtk_main ();
```

`gtk_main()` 是你在每个 GTK 中都会看到的另一个调用。当控制权到达此处时，GTK 将进入睡眠，等待 X 事件（如按钮或按键按下）、超时或文件 IO 通知的发生。然而，在我们的简单示例中，事件被忽略了。

## 2.1 GTK 中的 Hello World

现在来看一个带有小部件（按钮）的程序。这是 GTK 经典的 hello world。

```c
/* example-start helloworld.c */

#include <gtk/gtk.h>

/* 这是一个回调函数。data 参数在
*示例中被忽略了。关于回调的更多信息请见下文。 */
void hello(GtkWidget *widget,
gpointer      data )
{
  g_print ("Hello World\n");
}

gint delete_event(GtkWidget *widget,
GdkEvent *event,
gpointer      data )
{
  /* 如果你在 "delete-event" 信号处理程序中返回 FALSE，
  * GTK 将发射 "destroy" 信号。返回 TRUE 
  * 你不想窗口被销毁。
  * 
  * 这对于弹出“确定要退出吗？”之类的
  * 类型对话很有用。 */
  g_print ("delete event occurred\n");

  /* 将 delete 改为 FALSE，主窗口将随着
  * "delete_event" 被销毁。 */
  return(TRUE);
}

/* 另一个回调 */
void destroy(GtkWidget *widget,
gpointer      data )
{}
```
