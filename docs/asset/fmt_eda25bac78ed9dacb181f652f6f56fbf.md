
- `gnome-spell` 是一个简单的拼写检查控件。
- `gnome-preferences` 是用于设置 GNOME 偏好的控件。

第三个 GNOME 库是 `libgnornba`，它为 GNOME 应用程序提供 CORBA 接口。我们在本节中不会讨论 `libgnornba`，但如果你想了解更多关于 `libgnornba` 的信息，请查看：http://developer.gnome.org/arch/component/gnorba.html。

## GTK

在 GNOME 应用程序层面是 GTK，它代表 GIMP 工具包（GIMP Toolkit）。GTK 为图形应用程序提供控件和其他工具。GTK+ 最初为 GIMP 图形应用程序开发，已扩展到各种用途，包括 GNOME。

应用程序的窗口由数百甚至数千个称为控件（`widgets`）的小型图形项目组成。应用程序中的每个控件都形成了屏幕上窗口的一部分，或者作为另一个控件的容器。在某些容器控件内部有信号（`signals`），告诉程序执行某些操作。为了在信号发射时让按钮产生某种效果，另一个称为信号处理程序（`signal handler`）的函数会捕获信号，并调用执行操作所需的正确函数。当你与包含信号的控件交互时，信号被“激活”，发送发送给 X 服务器的消息，并执行该操作。

例如，一个滚动窗口将包含一个列表控件。在屏幕上，你看到带有列表的滚动窗口。滚动条是另一个控件。按钮控件将包含一个命名按钮的标签控件。其他控件将用于排列容器控件，例如对齐按钮控件的水平框和垂直框控件。

GTK+ 控件的一些示例是：

- 窗口（`Window`）
- 框架（`Frame`）
- 按钮（`Button`）
- 按钮内的标签（`Label`）
- 滚动窗口（`Scrollbar window`）
- 滚动条（`Scrollbar`）
- 菜单项（`Menu entry`）
- 水平容器
- 垂直容器

## GDK, Glib 和 Xlib

GNOME 应用程序的下一个组件是 GDK，它代表 GIMP 绘制包（GIMP Drawing Kit）。与 GTK 一样，GDK 最初也是为 GIMP 开发的。GDK 当 GTK 和 X 库（或 Xlib）之间的封装器。开发者使用 GDK 为窗口设置属性，或在窗口上绘制特殊对象。

GDK 增加了 GTK 的可移植性。因为 GTK 不直接与 X 库交互，将 GTK 适配到 X 以外的窗口系统非常简单。事实上，GTK 已经通过修改 GDK 被移植到 MS Windows。

`Glib` 是一个 C 库，提供了在 GNOME 应用程序中有用的程序。`Glib` 不由 GNOME 项目维护，但它被用作 GNOME 应用程序的基础。开发者使用 `Glib` 创建整个程序通用的结构，并且有一组用于常用函数的现成代码。`Glib` 还包含帮助将 GNOME 应用程序移植到其他系统的工具。为了使用 GTK，程序中必须包含 `Glib`。

`Xlib` 是 X 服务器用于创建 GNOME 运行的图形界面的库集合。

## Glade

准备好开始编程了吗？即使你永远不想编写 GNOME，你也应该熟悉一个名为 `Glade` 的工具。`Glade` 如图 24.2 所示。

## 学习更多

本节面向用户，以便你能更好地理解 GNOME 背后的技术。这里有一些优秀的资源：

- George Blank 在 IBM 网站写了一系列关于如何开发 GNOME 应用程序的文章。
- Tony Gale 写的 GTK+ 教程是另一个很好的资源，可以在。
- 在 GNOME 开发者网站也有丰富的信息。

## 总结

在本节中，你学习了 GNOME 应用程序的工作原理。你了解了构成 GNOME 程序的要素。你深入研究了 GNOME 的库，并介绍了 `Glade`。

## 问答

我寻找了 GNOME 库，但在目录树中没有找到。它们在哪里？

你必须从源码安装了 GNOME，或者安装了 GNOME 开发包，才能在系统中拥有这些库。大多数系统的头文件位于 `/usr/include` 或 `/usr/local/include`；这些文件对于了解库很有用。你可以使用 `whereis` 命令查找库——例如，要查看 `libgnomeui` 库安装在哪里，在 shell 提示符输入以下命令：

```
whereis libgnomeui
```

可以使用 `locate` 命令代替 `whereis`。`locate` 不需要文件在你的 PATH 中。

## 工作坊

测试题和练习旨在增加你的理解并鼓励你继续实验。答案见附录 B，“答案”。

## 测验

1. 什么是函数？
2. 什么是库？
3. 包含另一个控件的控件是什么？
4. 哪些库处理图形界面？
5. GNOME 库是用什么编程语言编写的？
6. 关于函数位于哪个库？
7. GTK 和 GDK 代表什么？
8. 对/错：当开发者在应用程序中选择界面包含后，`Glade` 会为其构建源代码。

## 练习

1. 打开你喜欢的文本编辑器并输入这个小程序：

```c
/* example-start gnome_love gnome_love.c */

#include <gtk/gtk.h>

void hello( GtkWidget *widget, gpointer data)
{
```

```c
g_print ("I love GNOME\n");
gint delete_event(GtkWidget *widget
```

# GNOME 应用程序剖析

```c
/*
 * 当按钮接收到“clicked”信号时，它将调用
 * 函数 hello() 并传递 NULL 作为其参数。hello()
 * 函数在上方已定义。 */
gtk_signal_connect(GTK_OBJECT (button), "clicked",
    GTK_SIGNAL_FUNC (hello), NULL);
```

```c
/*
 * 当被“clicked”时，这将通过调用
 * gtk_widget_destroy(window) 导致窗口销毁。同样，销
 * 信号可能来自这里，也可能来自窗口管理器。 */
gtk_signal_connect_object(GTK_OBJECT (button), "clicked",
    GTK_SIGNAL_FUNC (gtk_widget_destroy),
    GTK_OBJECT (window));
```

```c
/*
 * 这将按钮封装到窗口（一个 gtk 容器）中。 */
gtk_container_add (GTK_CONTAINER (window), button);
```

```c
/*
 * 最后一步是显示这个新创建的小部件。 */
gtk_widget_show (button);
```

```c
/*
 * 还有窗口 */
gtk_widget_show (window);
```

```c
/*
 * 所有 GTK 应用程序必须有一个 gtk_main()。控制在此结束
 * 并等待事件发生（例如按键按下或
 * 鼠标事件）。 */
gtk_main ();
```

```c
}
return(0);
/* example-end */
```

当你完成后，将其保存为 `gnome_love.c` 并在 shell 提示符输入以下命令进行编译：

```bash
gcc -Wall -g gnome_love.c -o gnome_love `gtk-config --cflags` \
`gtk-config --libs`
```

![](img/56ffc05f2012b0375f08095ea492838b_354_0.png)

# 附录 A 故障排除

GNOME 是一个稳定、可靠的桌面环境，但它也非常新。仍然有许多可以发现的 bug，特别是在早期发布的软件中。一个名为 `Bug Buddy` 的奇妙小实用程序允许你对崩溃的程序进行故障排除并报告 bug。

`Bug Buddy` 的目的是让用户能够轻松发送 bug 报告，同时自动收集对开发者有用的信息。它还可以帮助你判断程序崩溃是因为你的系统出了问题，还是因为程序本身存在真正的 bug。

在有 `Bug Buddy` 之前，如果你有一个核心转储（`core dump`），你必须启动 `gdb`，然后尝试重新创建导致崩溃的条件。你必须了解堆栈跟踪（`stack traces`）以及如何运行 `gdb`（这并不是一项易事），并且具备足够的编程知识来读取 trace 结果的含义。有了 `Bug Buddy`，任何人都可以向 GNOME bug 跟踪系统提交有用的 bug 报告。

发现 GNOME 应用程序和桌面环境本身崩溃的用户越多，提交的 bug 报告就越多，GNOME 在未来就会变得越稳定。不要因为你认为这可能是一个已经报告过的常见问题就害羞于提交 bug 报告。GNOME 核心黑客决定修复哪些 bug 的方法之一，就是特定 bug 收到的 bug 报告数量。

正如首席大师 Eric Raymond 所说：“只要有足够的眼睛，所有的 bug 都是浅的。”

## Bug Buddy 的要求

使用 `Bug Buddy` 必须安装以下软件：

- `gnome-libs` (建议使用 1.0.53 或更高版本)
