
安装软件的另一种方法是使用 `rpm` 命令。Red Hat 事实已将 Motif 软件封装在后续章节中讨论的 RPM（Red Hat 包管理器）中。

# `motif-devel-2.0.1-1.i386.rpm`

此包包含构建 Motif 客户端所需的静态库和 `#include` 文件（或头文件）。你还会找到 Motif 用户界面语言编译器 `uil` 以及 Motif 函数调用手册页。

# `motif-2.0.1-1.i386.rpm`

如果你只想运行 `mwm` 或 Motif 工作空间管理器 `Wsm`，你就需要此包中的共享库。超过 800 个图标将从此文件安装到 `/usr/X11/include/X11/icons` 目录下。

# `motif-mwm-2.0.1-1.i386.rpm`

在这里你不仅能找到窗口管理器 `mwm`，还能找到 `Wsm`，它演示了 Motif 2.0 的一些新功能。

# `motif-demosrc-2.0.1-1.i386.rpm`

如果你对探索 Motif 2.0 的新功能感兴趣，需要源码示例来帮助学习，请安装此包。你还需要安装开发库。这里的示例包括：

- `airport` —— 展示拖放
- `animate` —— 在窗口中动画化位图
- `drag_and_drop` —— 彻底的拖放演示
- `draw` —— 一个简单的应用程序
- `earth` —— 旋转的地球
- `filemanager` —— 简单的文件管理器
- `fileview` —— 简单的查看器
- `getres` —— 获取 Motif 资源
- `hellmotif` —— 一个 hello world 程序
- `i18input` —— 显示处理输入
- `panner` —— 一个简单的滚动器
- `periodic` —— 显示一些功能
- `popups` —— 显示弹出菜单
- `setdate` —— 设置日期
- `texteditor` —— 一个简单的编辑器

# 修改源码

- `transfer` —— 展示数据传输
- `workspace` —— 源码工作空间

# Motif 概念的简单示例

本节介绍了一个 Motif 程序的极简示例。你将学到足够的入门。在进入细节之前，让我们在 Motif 编程概述中涵盖基本概念。

虽然在 Linux 命令行中使用 C 编写程序相当简单，但如果你熟悉 X 编程，你就知道编写一个窗口程序涉及很多工作。你必须考虑标签、对话框、窗口、滚动条、颜色、按钮以及以及程序内部算法之外的程序运行的许多功能。在这些功能的同时，当你进行 X 编程时，应该考虑一致性和用户易用性。

这正是 Motif 发挥用处的地方。通过提供丰富的函数，Motif 可以帮助程序员构建美观且易于使用的程序。在 Motif 编程中，大量的程序代码（特别是较小的程序）是用于图形界面的。

当你为 Linux 命令行编写 C 程序时，通常会使用 `libc6` 库。如果你为 X 编写程序，你通常会使用 `X11` 库。当你为 Motif 编程时，你使用 X 作为系统窗口，并使用 X Toolkit 或 `xt` 库（其他）来实现界面。

安装 Motif 后，你将在 `/usr/X11R6/lib` 目录下找到以下库：

# Motif 编程

# 第 26 章

Motif 的 `#include` 文件位于 `/usr/X11R6/include/Mrm`、`/usr/X11R6/include/Xm` 和 `/usr/X11R6/include/uil` 目录下。这些库和头文件的位置在所有计算机系统中都是相当标准的，但如果它们位于不同的地方，这种差异将记录在 `imake` 和 `xmkmf` 的配置文件和规则文件中。（请参阅本章稍后的“使用 imake 和 xmkmf”以获取有关这些工具的更多信息。）

## MOTIF 编程

### 小部件与事件驱动编程

为 X 和 Motif 编程时，需要考虑的一个重要概念是，这些程序通常不是运行即退出；这些程序是由鼠标点击、按钮按下、鼠标拖动和击键等事件驱动的。Apple 程序员在为 Motif 编程时会感到非常熟悉。拦截这些事件的一些界面元素是用称为小部件（`widgets`）的 Motif 例程构建的，随着你变得越来越精通，你甚至会编写自己的小部件。

如果你刚开始 Motif 编程，不要被这个主题的一些新术语和概念吓跑。你将学习回调函数（`callbacks`）、类（`classes`）、复合体（`composites`）、耦合资源（`coupled resources`）、小工具（`gadgets`）、层次结构（`hierarchies`）、实例化（`instantiation`）、模态（`modality`）、属性（`properties`）、接收器（`receivers`）和子类（`subclasses`）。虽然书中没有足够的空间涵盖所有主题，但列表 26.1 包含了一个入门示例。

### 简单的 Motif 程序

列表 26.1 创建了一个带有文件（File）、编辑（Edit）和帮助（Help）菜单的小窗口。应用程序可以调整大小，可以最小化或最大化，并且与其他 Motif 应用一样。此程序演示了如何创建窗口、菜单栏、下拉菜单、按钮和弹出对话框。

这不是一个完美的示例，因为界面位于程序的 `main()` 部分，它没有使用资源，而且实际上并没有做任何事情；程序运行的内部原理将由你自己学习。

# 列表 26.1 Motif 程序骨架。

```c
/* 一个简单的骨架程序 /

#include <Xm/RowColumn.h>

#include <Xm/MainW.h>

#include <Xm/CascadeB.h>

#include <Xm/MessageB.h>

#include <Xm/PushBG.h>
```

```c
Widget skeleton; /* 我们的应用程序 *

/* 当用户选择退出时发生什么 * /
void skel_exit_action() {
  exit(0);
}
```

# 列表 26.1，续

```c
/* 销毁对话框 */
void skel_dialog_handler(skel_dialog)
Widget skel_dialog;
{
    XtUnmanageChild(skel_dialog);
};
```

```c
/* 创建一个帮助动作对话框 */
void skel_help_action()
{
    Arg args[10];
    Widget skel_dialog;
    Xstring skel_string;
    /* 存储帮助字符串 */
    skel_string =
    XstringCreateLocalized("This is Skeleton v0.1, a simple Motif client.");
```

```c
/* 释放存储 */
XmStringFree(skel_string);
    /* 显示对话框 */
    XtManageChild(skel_dialog);
};
```

```c
/* 主程序在此开始 */
main (int argc, argv)
int argc;
char *argv[];
{
    /* 声明我们的小部件，包括菜单动作 */
    Widget skel_window, /* 主窗口 */
           skel_menubar, /* 主窗口菜单栏 */
           skel_filepulldown, /* 文件菜单 */
           skel_new,
           skel_open,
           skel_close,
           skel_save,
           skel_exit,
           skel_editpupldown, /* 编辑菜单 */
           skel_cut,
           skel_paste,
           skel_helppdown, /* 帮助菜单 */
           skel_version, /* 临时存储 */
    Xstring skel_string;
    XtAppContext skel_app;
```

```c
XtSetLanguageProc(NULL, NULL, NULL);
```

```c
/* 命名并设置初始大小 */
// skeleton = XtvaAppInitialize(&skel_app, Skeleton, NULL, 0, &argc, argv)
NULL, Xnwidth, 320, Xnheight, 240, NULL);
```

```c
/* 创建主窗口 */
skel_window = XtvaCreateManagedWidget("skel", xmainWindowClassClass, skeleton,
XnscrollingPolicy, AUTOMATIC, NULL);
```

```c
/* 在主窗口构建菜单栏 */
```
