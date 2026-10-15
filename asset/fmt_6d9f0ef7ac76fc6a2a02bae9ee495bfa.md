
- `piano`—一个简单的 Motif MIDI 应用程序（你需要 MIDI 支持）
- `popups`—展示 Motif 2.0 中弹出菜单的改进
- `sampler2_0`—Motif 2.0 功能的相当完整的演示
- `setdate`—设置系统日期并演示 Motif SpinBox 小部件

除了这些程序，你将在另一个目录中找到另外 10 个示例。

# Motif Demos rpms

如果你不想花时间从源码构建示例客户端，并且倾向于直接尝试 Motif 的某些功能，请安装此包。在运行这些客户端之前，你必须安装共享库。

# Motif 编程概念的简单示例

这里介绍了一个极其简单的 Motif 程序——仅足够入门。但在进入细节之前，我将从 Motif 编程的视角概述其基本概念。

用 C 语言为 Linux 命令行编写程序相当简单，但如果你熟悉 X 编程，你就知道编写窗口化程序涉及的内容要多得多。你必须考虑标签、对话框、窗口、滚动、颜色、按钮以及程序运行方式的许多其他特性——除了让程序与众不同的内部算法之外。在具有这些独特功能的同时，当你为 X 编程时，应该考虑用户的一致性和易用性。

![](img/fbfff30e42d507bc7531108a281d6cf4_1016_0.png)

（注：此处980 可能是页码标记，保留原样或根据语境处理，此处保留原样）

980

Linux 编程

第四部分

这就是 Motif 可以帮到你的地方。通过提供丰富的函数，Motif 可以帮助程序员构建具有吸引力且易于使用的程序。在 Motif 编程中，大量的程序代码（尤其是较小的程序）都用于图形界面。

当你为 Linux 命令行编写 C 程序时，你通常会使用 `libc` 库。如果你为 X 编写程序，通常会使用 `X1ib` 库。当你为 Motif 编程时，你将使用 X 作为窗口系统以及 X Toolkit `xt` 库（以及其他库）。

安装 Motif 2.1 后，你将在 `/usr/X11R6/lib` 目录下找到许多库：

```
/usr/X11R6/lib/libMrm.a
/usr/X11R6/lib/libUil.a
/usr/X11R6/lib/libXm.a
/usr/X11R6/lib/libXcm.a
/usr/X11R6/lib/libMrm.so
/usr/X11R6/lib/libXm.so.2
/usr/X11R6/lib/libMrm.so.2.0
/usr/X11R6/lib/libXm.so
/usr/X11R6/lib/libXm.so.2.0
```

Motif 的 `#include` 头文件位于 `/usr/X11R6/include/Mrm`、`/usr/X11R6/include/Xml` 和 `/usr/X11R6/include/util` 目录下。这些库和头文件的位置在所有计算机系统中都是相当标准的，但如果它们位于不同的地方，这种差异将记录在配置文件以及 `imake` 和 `xmkmmf` 的规则中（有关这些工具的更多信息，请参阅本章后续的“使用 imake 和 xmkmmf”章节）。

# 小部件与事件驱动编程

为 X 和 Motif 编程时需要考虑的一个重要概念是：这些程序通常不是运行即退出。这些程序是由鼠标点击、按钮按下、鼠标拖拽、其他程序和按键等事件驱动的。Apple Macintosh 程序员会觉得 Motif 编程上手。拦截这些事件的一些界面元素是用 Motif 小部件构建的，随着你变得越来越精通，你甚至会编写一些自己的。

如果你刚开始 Motif 编程，不要被这些新术语和概念吓跑。你将学习回调（`callbacks`）、子元素（`children`）、类（`classes`）、耦合资源（`coupled resources`）、小部件（`gadgets`）、层次结构（`hierarchies`）、初始化器（`initiators`）、实例化（`instantiation`）、模态（`modality`）、属性（`properties`）、接收者（`receivers`）、子类（`subclasses`）。虽然我们书中没有足够的空间涵盖所有主题，但列表 32.1 包含了一个让你入门的简单示例。

# 简单的 Motif 程序

列表 32.1 创建了一个带有“文件”、“编辑”和“帮助”菜单的小窗口。应用程序窗口是可以调整大小的，可以最小化或最大化，并且像任何 Motif 应用程序一样响应。这个程序演示了如何创建窗口、菜单栏、下拉菜单、按钮和弹出对话框。

它并不是一个完美的示例，因为界面位于程序的 `main()` 部分，它没有使用资源，而且并没有执行任何操作。我将程序可能运行的内部细节留给你。

## 列表 32.1 `motif_skeleton.c`

```c
/* 一个简单的骨架程序 */
#include <Xm/Cm.h>
#include <Xm/MainWindow.h>
#include <Xm/Cascade.h>
#include <Xm/Message.h>
#include <Xm/Separator.h>
#include <Xm/Push.h>

Widget skeleton;    /* 我们的应用程序 */

/* 当用户选择退出时 */
void skel_exit_action() {
    exit(0);
}

/* 销毁对话框 */
void skel_dialog_handler(Widget skel_dialog)
{
    Widget skel_dialog;
    XtaddChild(skel_dialog);
}

/* 创建帮助对话框 */
void skel_help_action() {
    Arg args[1];
    Widget skel_dialog;
    CString skel_string;

    /* 存储字符串 */
    skel_string = XtStringCreate("This is Skeleton v.1, a simple client.");
}
```
![](img/fbfff30e42d507bc7531108a281d6cf4_1016_0.png)

（Linux 编程）

```c
/* 构建对话框 */
skel_dialog = XmCreateDialog(skeleton, "dialog", args, 0);
XtSetValues(skel_dialog, messageString, NULL);

/* 在按下 OK 按钮后调用 skel_dialog_handler */
XtAddCallback(skel_dialog, okCallback, skel_dialog_handler, NULL);

/* 释放存储 */
XtStringFree(skel_string);

/* 显示对话框 */
XtManageChild(skel_dialog);
}
```

```c
/* 主程序开始 */
main (int argc, char *argv[])
{
    int argc; /* 声明我们的小部件、动作 */
    Widget skel_window, /* 主窗口 */
        skel_menubar, /* 主菜单栏 */
        skel_filepulndown, /* 文件菜单 */
        skel_new,
        skel_open,
        skel_close,
        skel_save,
        skel_exit,
        skel_editpuldown, /* 编辑菜单 */
        skel_cut,
        skel_paste,
        skel_helpldown, /* 帮助菜单 */
        skel_version;
    XtString skel_string; /* 临时存储 */
    XtAppContext skel_app;

    XtSetAppContext(NULL, NULL);

    /* 给应用一个名称和初始大小 */
    skeleton = XtVaInitialize(&skel_app, "Skeleton", NULL, 0, argc, argv,NULL, XmWidth, 320, XmHeight, 240, NULL);

    /* 创建主窗口 */
    skel_window = XtVaCreateManagedWidget("skel", MainWindowClass, skeleton,
    ScrollingPolicy, XmAUTOMATIC, NULL);
}
```

```c
/* 跨主窗口构建菜单栏 */
skel_menubar = XmCreateMenuBar(skel_window, skel_menubar, NULL, 0);
```

```c
/* 构建文件下拉菜单 */
skel_filepulndown = XmCreatePulldownMenu(skel_menubar, "File", NULL, 0);
skel_string = XtStringCreate("File");
```
