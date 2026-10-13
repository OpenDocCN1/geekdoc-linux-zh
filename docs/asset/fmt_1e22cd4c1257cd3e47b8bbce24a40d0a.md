
`skel_menubar = XmCreateMenuBar(skel_window, "skel_menubar", NULL, 0);`

```c
/* 构建文件下拉菜单 */

skel_filepulldown = XmCreatePopupMenu(skel_menubar, "File", NULL, 0);

->skel_string = XmStringLocalized("File");
```

```c
/* 创建名称，分配 ALT+F 为助记键 */

XtvaCreateManagedWidget("file", xcascadeButtonWidgetClass, skel_menubar,

Xmnlabelstring, skel_string, XmMnnemonic, 'F', XnsubMenuId,

->skel_filepulldown, NULL);
```

```c
/* 释放存储 */

XmStringFree(skel_string);
```

```c
/* 添加下拉菜单元素 */

skel_new = XtvaCreateManagedWidget("New", xPushButtonGadet,

skel_pulldown, NULL);

skel_open = XtvaCreateManagedWidget("Close", xPushButtonGadet,

skel_pul, NULL);

XtXtvavaManagedseparator("separatorseparator x,,,

pulpul,,,,

__copycopy =vavaManagedWidget("("",",PushButtonGadGad,

pulldown, NULL);

skel_save = XtvaCreateManagedWidget("Save", xPushButtonGadet,

skld_,,,

);

Xtvava("separator("separator", x,,,

pulpul,,,sk);

skel_exit = XtvaCreateManagedWidget("Exit", xGadGadet,

pulldown, NULL);
```

```c
/* 当用户选择退出时添加回调 */

XtAddCallback(skel_exit, XnactivateCallback, skel_exit_action, NULL);
```

```c
/* 构建编辑菜单 */

skel_editpulldown = XmCreatePopupMenu(skel_menubar, "Edit", NULL, 0);

skel_string = XmStringLocalized("Edit");

XtvaCreateManagedWidget("Edit", xcascadeButtonWidgetClass, skel_menubar,

Xmnlabelstring, skel_string, XmMnnemonic, 'E', XnsubMenuId,

skel_editpulldown, NULL);
```

```c
/* 释放存储 */

XmStringFree(skel_string);
```

```c
/* 添加编辑下拉菜单元素 */

skel_cut = XtvaCreateManagedWidget("Cut", xPushButtonGadet,

edit_pulldown, NULL);

skel_copy = XtvaCreateManagedWidget("Copy", xPushButtonGadet,

edit_pulldown, NULL);
```

# 自动化、 编程与修改源代码

## 列表 26.1 续

要编译此程序，可以使用以下命令：
```bash
gcc -o skel skeleton.c -L/usr/X11/lib -lXpm -lXt -lX11
```
此行引导 GNU 链接器在 `/usr/X11/lib` 中查找所需的库。程序随后使用共享的 Xm、Xpm、Xt 和 X11 库进行链接。程序的最终大小小于13000字符。

### 程序工作原理

当你用C语言编写命令行或X程序时，你知道如果你使用了某些例程或函数，必须告诉编译器所需的 `#include` 文件。此程序通过列出 `skeleton.c` 中使用的不同函数的 `#include` 文件开始。

接下来，将 `skeleton` 声明为顶层小部件使得程序信息外部可用。这是因为创建 Motif 对话框的 `skel_help_action()` 需要知道对话框属于谁。接下来两个例程 `skel_exit_action()` 和 `skel_dialog_handler()` 被称为回调函数。

回调函数让程序工作。当你按下按钮或选择菜单项从其他程序或操作系统接收信息时。如果你查看 `skel_dialog_handler()`，你会看到此行：
```c
XtAddCallback(skel_dialog, XmNoCallback, skel_dialog_handler, NULL);
```
此函数告诉程序在对话框出现后做什么，以及当你点击 OK 按钮或按下 Enter 键时做什么——这一切不需要大量的额外代码。

`skel_help_action()` 也是一个回调函数，响应 `main()` 程序的调用：
```c
XtAddCallback(skel_version, XactivateCallback, skel_help_action, NULL);
```
在此实例中，当你从程序的帮助菜单拉“版本”菜单项时，`skel_help_action()` 将运行。从程序的文件菜单退出时，会调用 `skel_exit_action()` 例程。在创建了要显示的版本信息的字符串空间后，`skel_help_action()` 然后创建对话框：
```c
skel_dialog = XCreateMessageDialog(skeleton, "dialog", args, 0);
```
然后用例程填充所需信息：
```c
XtSetValues(skel_dialog, XmessageString, skel_string, NULL, NULL);
```
随后是回调指定，最后通过以下显示对话框：
```c
XtManageChild(skel_dialog);
```
`main()` 例程从不同小部件和小部件元素的声明开始。对 `XtVaInitialize()` 的调用声明了应用程序名称，指示了程序是否应该读取任何命令行参数，并分配了像素宽度和高度的初始大小。

### 示例程序资源

初始窗口大小（以及所有其他 Motif 和 X11 程序的许多其他默认操作）也可以通过使用资源设置。这样做的方法之一是打开主目录下的 `.defaults` 文件，然后输入：
```
Skeleton.height: 480

Skeleton.width: 640
```
并保存文件。将行：
```c
skeleton = XtVaInitialize(&skel_app, "Skeleton", NULL, 0, &argc,
argv, NULL, XmWidth, 320, XmHeight, 240, NULL);
```
替换为
```c
skeleton = XtAppInitialize(&skel_app, "Skeleton", NULL, 0, &argv,
NULL, NULL, NULL);
```
