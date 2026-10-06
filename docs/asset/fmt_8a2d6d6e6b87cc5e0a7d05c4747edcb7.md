
图 29.1 显示了一个包含 `label.c` 示例程序的窗口。

## 图 29.1
在 KDE 桌面中运行 `label.c` 示例程序。

![](img/69b363a7d7f58dc8d0b8c78c0052826f_506_0.png)

# 使用 Athena 和 Motif 控件

在第 28 章中，我们看到了使用低级 Xlib API 编写简单程序需要多少代码。
我们还回顾了 X 工具包，这是一个被 Athena 以及大多数其他顶层应用级控件库使用的工具库。在本章中，我们将学习如何实现以下操作：

- 使用 Athena 控件
- 使用 Motif 控件
- 在 C++ 程序中编写自己的 Athena
- 使用 C++ 类库封装 Athena 的分层面板 `Paned`、按钮 `Button`、标签 `Label` 和文本 `Text` 控件

## 使用 Athena 控件

Athena 控件集是为 MIT Athena 项目编写的，旨在 MIT 的学生和教师提供一个分布式计算环境。Athena 控件最初具有“扁平”的外观，大多数 Linux 分发版都有一个名为 `aw3d` 的可选包，它会覆盖 Athena 控件的库，将“扁平”外观替换为“3D”外观。本章实际上是使用 Athena 控件的教程。在每个节中，我们将开发一个短程序，展示如何使用标签、命令按钮、菜单和文本编辑器。

### Athena Label 控件

本节的示例程序 `label.c` 位于光盘镜像中的 `src/X/Athena` 目录下。该程序需要包含两个头文件：

```c
#include <X11/Intrinsic.h>
#include <X11/Xaw/Label.h>
```

`Intrinsic.h` 文件包含 X 工具包的定义，`Label.h` 定义了 Athena `Label` 类。通常，X 应用使用资源来更改程序的外观和行为。在这里，我们使用字符字符串数组来设置示例中使用的 `Label` 控件的资源。家目录下的 `.Xdefaults` 文件用于程序选项，允许你更改此处定义的具有 `Label` 属性属性的控件：

```c
String app_resources[] =
{ "*Label: Testing Athena Label Widget", NULL };
```

在 `main` 函数中，我们必须定义三个变量：一个顶层控件、一个 `Label` 以及一个应用上下文：

```c
XtAppContext application_context;
Widget top_level, label;
```

首先，我们为此应用创建并保存顶层控件的值，并定义变量 `application_context` 的值：

```c
top_level = XtAppInitialize(&application_context, "test", NULL, 0,
      &argc, argv,
      app_resources,
      NULL, 0);
```

现在我们为顶层控件创建一个子控件。这是我们的测试 `Label` 控件：

```c
label = XtCreateManagedWidget("label", labelWidgetClass, top_level,
      NULL, 0);
```

在调用 `XtRealizeWidget` 后，顶层控件和 `Label` 控件被实例化。

```c
XtRealizeWidget(top_level); // 创建窗口并可见
```

最后，我们将应用上下文传递给 `XtAppMainLoop` 来处理这个简单程序的所有事件：

```c
XtAppMainLoop(application_context); // 主事件循环
```

正如我们在第 28 章所看到的，`label.c` 示例程序还包含了获取 `Label` 控件和高度资源的示例代码：

```c
Dimension width, height;
Arg args[2];
XtSetArg(args[0], XtWidth, &width);
XtSetArg(args[1], XtHeight, &height);
GetValues(label, args, 2);
printf("Widget width=%d and height=%d\n", width, height);
```

图 29.1 显示了一个包含 `label.c` 示例程序的窗口。

## 图 29.1
在 KDE 桌面中运行 `label.c` 示例程序。

![](img/69b363a7d7f58dc8d0b8c78c0052826f_506_0.png)

### Athena List 控件

本节的示例程序 `list.c` 与前两个示例：`label.c` 和 `button.c` 相似。我们将关注处理 `List` 控件，并假设你已经阅读了最后两个节。

正如我们在第 28 章看到的，`label.c` 示例程序还包含了获取 `Label` 控件和高度资源的示例代码：

```c
Dimension width, height;
Arg args[2];
XtSetArg(args[0], XtWidth, &width);
XtSetArg(args[1], XtHeight, &height);
GetValues(label, args, 2);
printf("Widget width=%d and height=%d\n", width, height);
```

回调函数 `do_list_item_selected` 使用第三个参数来打印点击的列表的索引和标签：

```c
void do_list_item_selected(XWidget w, XtPointer unused, XtPointer data) {
    XawListReturnStruct *list_item = (XawListReturnStruct*)data;
    printf("Selected %d text is %s\n",
           list_item->list_index, list_item->string);
}
```

`main` 函数为两个小件和一个应用上下文定义了变量：

```c
Widget top_level, list;
XtAppContext application_context;
```

我们创建了一个顶层 `Top-Level` 小件并为应用上下文初始化它：

```c
top_level = XtAppInitialize(&application_context,
                              NULL, ZERO,
                              &argc, argv, NULL,
                              NULL, 0);
```

当我们创建一个列表 `List` 小件时，我们使用 `"char *"` 字符串值数组作为列表项的标签：

```c
String items[] = {
    "1", "2", "3", "4", "5", "six", "seven", "8",
    "9th list entry", "this is the tenth list entry",
    "11", "12",
    NULL
};
```

为了创建一个列表小件，我们使用 `XtVaCreateManagedWidget`——这是 `XtCreateManagedWidget` 的另一种形式——它接受任意数量的选项：

```c
list = XtVaCreateManagedWidget("list", listWidgetClass,
                               Xt, items,
                               NULL, 0);
```

我们像在 `button.c` 示例中看到的方式，将回调函数与列表小件关联：

```c
XtAddCallback(list, Xtkcallback,
              do_list_item_selected, (XtPointer)NULL);
```

和之前一样，我们让小件在 X 服务器上可见并能够处理事件：

```c
XtRealizeWidget(top_level);
XtAppMainLoop(application_context);
```

图 29.3 显示了一个包含 `list.c` 示例程序的 X 窗口。

![](img/69b363a7d7f58dc8d0b8c78c0052826f_510_0.png)

## 图 29.3
在 KDE 桌面环境上运行 `list.c` 示例程序。

| 1 | 2 |
| 3 | 4 |
| 5 | els |
| seven | this is the tenth list entry |
| 7 | 12 |

你可以通过切换目录到 `src/X/Athena` 并输入：`make list` 来构建并运行此测试程序。

### Athena 文本小件 Text Widget

Athena `Text` widget 有许多可以使用资源值在 `.defs` 文件中或在程序中定义设置的选项。以下三个文件分别用 `Paned`、`AsciiText` 和 `Command` 按钮小件定义。`Paned` 是一种容器 `Container` 小件，用于容纳其他小件。默认情况下，`Paned` 提供了微小的“句柄 handles”，它们可以用于手动调整任何被包含小件的尺寸。

```c
#include <X11/Xaw/Paned.h>
#include <X11/Xaw/AsciiText.h>
#include <X11/Xaw/Command.h>
```

当我们定义一个小件时，我们希望提供回调函数来显示小件中的文本并清除小件中的所有文本。为了显示小件的文本，我们将使用操作小件指定为第一个参数的 `XtVaValues` 函数。第二个参数是用于指定我们想要获取字符串资源值的字符串。第三个参数是字符串变量的地址，它指向字符块。该字符块的存储由 `Text` widget 内部管理。第四个参数为 `NULL`，表示不再从 `Text` widget 获取进一步的资源值。

下面的代码列表显示了 `do_display_widget` 回调函数的实现。当文本小件发生事件时，会调用此函数。为了演示目的，我们使用 `XtVaValues` 获取小件中的当前文本并将其打印：

```c
void do_display_widget(Widget W,
XtPointer text_ptr,
XtPointer unset) {
    Widget text = (Widget) text_ptr;
    String str;
    XtVaValues(text,
               value, &str,
               NULL);
    printf("Widget Text is:%s\n", str);
}
```

我们还希望能够擦除小件中的文本。为了实现这一点，我们使用工具函数 `XtVaValues` 将字符串资源的值设为 `NULL`：

```c
void do_erase_text_widget(Widget w,
XtPointer text_ptr,
XtPointer unused) {
    Widget text = (Widget) text_ptr;
    XtVaValues(text,
               value, "",
               NULL);
}
```

我们在这个示例中添加了新内容：一个退出按钮 `quit button`。我们可以简单地调用它，但最好先调用 `DestroyApplicationContext` 来清理对共享资源的任何引用。在这个示例中，我们将应用上下文声明为全局变量，这样 `do_quit` 函数就可以访问应用上下文：

```c
XtAppContext application_context;
void do_quit(Widget w, XtPointer unused1, XtPointer unused2) {
    DestroyApplicationContext(application_context);
    exit(0);
}
```

与之前的示例一样，我们直接在程序中定义默认资源。在这里，我们正在为 `Text`、`erase` 和 `display` 类定义资源。注意，我们没有为 `Quit` 命令定义任何默认资源，就像我们为 `Erase` 和 `Display` 命令按钮做的那样。`Quit` 按钮将以其名称作为默认标签——在这种情况下是 `Quit`。

下面的代码列表说明了如何设置应用资源：

```c
String app_resources[] = {
    "**editType: edit",
    "**autoFill: on",
    "**scrollVertical: whenNeeded",
    "**scrollHorizontal: whenNeeded",
    "**erase:label: Erase the Text widget",
    "**display:label: Display the text from the Text widget",
    "**preferredPaneSize: 300",
    NULL
};
```

小件属性 `autoFill` 用于控制自动换行。小件属性 `editType` 用于设置文本为可编辑。`preferredPaneSize` 属性设置了位于 `Pane` 小件中的小件的默认像素高度。`main` 函数定义了一个顶层 `Top-Level` 小件。

以下包含定义了这些部件类型：

添加到简单菜单的每个菜单项都可以有其独特的回调 `Callback` 函数，用以执行相应的菜单操作。在 `menu.c` 示例中，我们使用了一个的回调函数 `do_menu_selection`，该函数通过菜单元素名称来确定用户选择了哪个菜单项。示例程序 `menu.c` 有一个标记为“Exit program”的元素。因为我们要在退出程序之前复制任何使用的 X 资源和数据，我们将应用程序上下文设置为全局变量，以便在回调函数中使用它：

```c
XtAppContext application_context;
void do_menu_selection(Widget item_selected, XPointer unused) {
	char * name = Xtname(item_selected);
	printf("Menu %s has been selected.\n", name);
	if (strcmp(name, "Exit program") == 0) {
		XtDestroyApplicationContext(application_context);
	}
}
```

`Xtname` 资源返回部件的字段名。该名称可以用于在运行示例程序时确定用户选择了哪个菜单项。虽然我们通常使用 `.Xdefaults` 来自定义 X 资源，但 `menu.c` 示例中的以下数据用于定义默认或“回退”资源：

```c
String fallback_resources[] = {
	*menuButton.label: This is a menubutton label,
	*menu.label: Sample menu label,
	NULL
};
```

这些数据在示例程序中作为全局变量分配；它们也可以在 `main` 函数中定义：

```c
char * menu_item_names[] = {
	"Menu item1", "Menu item2", "Menu item3",
	"Menu item4", "Exit program",
};
```

在 `main` 函数中分配部件数据是可以的。但你必须小心：如果你使用了从 `main` 函数调用的独立“设置”函数，请确保将任何部件设置数据声明为 `static`，这样当程序退出函数时，其内存分配就不会丢失。记住，函数中的非静态数据分配在调用栈上；这些存储在退出函数后就会“消失”。我们定义了四个变量来存储 `menu.c` 示例程序中创建的部件的值：

```c
Widget top_level, menu_button, menu, menu_element;
```

变量 `menu_element` 被复用用于创建并添加到简单菜单的每个菜单元素例如 `Sme` 部件。正如我们在之前的示例中看到的，我们需要创建应用程序的部件：

```c
top_level = XtVaAppInitialize(&application_context,
    "textmenu", NULL, 0,
    &argc, argv, fallback_resources,
    NULL);
```

```c
menu_button = XtCreateManagedWidget("menuButton",
    menuButtonClass,
    top_level, NULL, 0);
```

```c
menu = XtCreatePopupShell("menu", simpleMenuWidgetClass, menu_button,
    NULL, 0);
```
