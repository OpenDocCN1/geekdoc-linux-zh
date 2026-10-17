
# Motif 编程

## 第 26 章

Motif 的 `#include` 文件位于 `/usr/X11R6/include/Mrm`、`/usr/X11R6/include/Xm` 和 `/usr/X11R6/include/uil` 目录下。这些库的位置在所有计算机系统中都是非常标准的，但如果它们位于不同的地方，这种差异将记录在 `imake` 和 `xmkmf` 的配置文件和规则文件中。（请参阅本章稍后的“使用 imake 和 xmkmf”以获取更多关于这些工具的信息。）

## 小部件与事件驱动编程

为 X 和 Motif 编程时，需要考虑的重要概念是：程序通常不是运行的；它们是由事件驱动的，例如鼠标点击、按钮按下、鼠标拖动和击键。在 Motif 编程中感觉很自如。某些界面元素是用 Motif 小部件构建的，随着你变得熟练，你也将编写一些。如果你刚刚开始 Motif 编程，不要被这些新术语和概念吓到。你将学习回调、类、组合、资源、层次结构、实例化、属性和子类。虽然书中没有足够的空间涵盖所有主题，但示例 26.1 包含了一个入门的示例。

### 简单程序

示例 26.1 创建了一个带有文件、编辑和帮助菜单的小窗口。应用程序窗口是可以调整的，可以最小化或最大化，并且通常像任何应用程序一样响应。该程序演示了如何创建窗口、菜单栏、下拉菜单、按钮和弹出对话框。在程序的 `main()` 部分，它没有使用资源，而你将学习程序的工作原理。

### 示例 26.1 skeleton

```c
/* 一个简单的 skeleton 程序 */

#include <Xm/Widget.h>

#include <Xm/Main.h>

#include <Xm/Cascade.h>

#include <Xm/Message.h>

#include <Xm/Push.h>

Widget skeleton; /* 应用程序 */

/* 选择 Exit 时发生 */

void skel_exit() {
  exit(0);
}
```

### 示例 26.1，续

```c
/* 销毁对话框 */
void skel_dialog_handler(skel_dialog)
Widget skel_dialog;
{
    XtDestroyChild(skel_dialog);
}

/* 创建对话框 */
void skel_help_action()
{
    Arg args[10];
    Widget skel_dialog;
    XtString skel_string;
    /* 存储字符串 */
    skel_string = XtStringLocalized("This is Skeleton v0.1, a simple client.");
    /* 构建对话框 */
    skel_dialog = XCreateMessageDialog(skeleton, "dialog", args, 0);
    XtSetValues(skel_dialog, XmessageString, skel_string);
    /* 点击 OK 按钮后调用 skel_dialog_handler() */
    XtAddCallback(skel_dialog, XmNoCallback, skel_dialog_handler, NULL);
    /* 释放存储 */
    XtStringFree(skel_string);
    /* 显示对话框 */
    XtManageChild(skel_dialog);
}

/* 程序开始 */
main (int argc, argv)
    int argc;
    char *argv[];
{
    /* 声明我们的小部件，包括菜单动作 */
    Widget skel_window,           /* 主窗口 */
        skel_menubar,             /* 主菜单栏 */
        skel_filepullown,          /* 文件菜单 */
        skel_new,
        skel_open,
        skel_close,
        skel_save,
        skel_exit,
        skel_editpulldown,       /* 编辑菜单 */
        skel_cut,
        skel_copy,
        skel_paste,
        skel_helpldown,          /* 帮助菜单 */
        skel_version;            /* 临时存储 */
    XtString skel_string;
    XtAppContext skel_app;
    XtSetLanguageProc(NULL, NULL, NULL);
}
```

```c
/* 命名并设置初始大小 */
skeleton = XtAppInitialize(&skel_app, "Skeleton", NULL, 0, &argc, argv,
NULL, Xnwidth, 320, Xnheight, 240, NULL);
```

```c
/* 创建主窗口 */
skel_window = XtCreateManagedWidget("skel", xMainWindowWidgetClass, skeleton,
XnscrollingPolicy, xAUTOMATIC, NULL);
```

```c
/* 跨主窗口构建菜单栏 */
skel_menubar = XmCreateMenuBar(skel_window, "skel_menubar", NULL, 0);
```

```c
/* 构建文件下拉菜单 */
skel_filepulown = XmCreatePullDownMenu(skel_menubar, "File", NULL, 0);
skel_string = XmStringLocalized("File");
```

```c
/* 创建菜单，ALT+F 为记忆键 */
XtCreateManagedWidget("file", xcascadeButtonWidgetClass, skel_menubar,
Xmnlabelstring, skel_string, Xmmnnemonic, 'F', XnsubmenuId,
skel_filepulown, NULL);
```

```c
/* 释放存储 */
XmStringFree(skel_string);
```

```c
/* 添加所有下拉菜单元素 */
skel_new = XtCreateManagedWidget("New", xPushButtonGadgetClass,
skel_filepulown, NULL);
skel_open = XtCreateManagedWidget("Open", xPushButtonGadgetClass,
skel_filepulown, NULL);
XtCreateManagedWidget("separator", xseparatorGadgetClass, skel_filepulown,
NULL);
```

```c
skel_copy = XtCreateManagedWidget("Copy", xPushButtonGadgetClass,
skel_filepulown, NULL);
skel_save = XtCreateManagedWidget("Save", xPushButtonGadgetClass,
skel_filepulown, NULL);
XtCreateManagedWidget("separator", xseparatorGadgetClass, skel_filepulown,
NULL);
```

```c
skel_exit = XtCreateManagedWidget("Exit", xPushButtonGadgetClass,
skel_filepulown, NULL);
```

```c
/* 当用户选择 Edit 时添加 */
XtAddCallback(skel_exit, XmActivateCallback, skel_exit_action, NULL);
```

```c
/* 构建编辑菜单 */
skel_editpulldown = XmCreatePullDownMenu(skel_menubar, "Edit", NULL, 0);
skel_string = XmStringLocalized("Edit");
XtCreateManagedWidget("Edit", xcascadeButtonWidgetClass, skel_menubar,
```
