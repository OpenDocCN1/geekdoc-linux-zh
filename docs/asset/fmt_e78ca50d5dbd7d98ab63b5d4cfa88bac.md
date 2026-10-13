
```
 /* 首先，为标签创建复合字符串 */
xlabel = XmCreateStringLt("WarnGen", XString_DEFAULT_CHARSET);
h_button = XtCreateManagedWidget("WarnGen",
xmPushButtonWidgetClass, tolevel,
nMWidth, 200,
nMHeight, 100,
nMabelString, xlabel,
NULL, NULL);
```

```
 /* 释放复合字符串（Motif 工具包会创建一个副本） */
XStringfree(xlabel);
```

如代码段所示，`XtVaCreateManagedWidget` 接受变数量的参数，如下所示：

- 前三个参数是必须的，且与 `XtCreateManagedWidget` 所要求的相同。第一个参数是部件名称，第二个是部件类，第三个用于指定父级部件。

- 紧随两个强制性参数之后是资源规范列表。每个规范的格式为资源名称后跟该资源的值。

- 一个 `NULL` 资源名称标记此列表的结束。

# 回调函数注册

大多数 Motif 部件包含一类称为回调（callbacks）的资源，它们指向函数的指针。你可以将此类资源设置为你的某个函数之一，并让部件在响应一个或多个事件时调用该函数。这些函数被称为回调函数，因为 Motif 工具包会在适当的时候对它们进行回调（call back）。

一个部件通常有多种类型的回调资源，每种类型都用于在特定情况下调用的函数。部件的回调资源实际上是一个函数列表，而不是单个函数。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_730_0.png)

当该回调资源的条件满足时，部件会调用所有回调。调用顺序与注册回调的顺序相同。

在“一个简单的 Motif 程序”标题下列出的程序，函数 `cb_quit` 是推按钮 `XmactivateCallback` 资源的回调函数。根据 PushButton 的文档，当用户点击按钮时，部件会调用 `XmactivateCallback` 资源中的函数。除了 `XmactivateCallback` 之外，PushButton 还有两个回调资源：

- `XmnarmCallback` 函数，在用户点击按钮时被调用

- `XmdisarmCallback` 列表，在用户释放按钮时被调用

示例所示，你使用 `XtAddCallback` 函数将函数添加到回调列表中，通过使用 `cb_quit` 函数到 `quit_button` 部件的 `XmactivateCallback` 资源，我们执行如下操作：

```
XtAddCallback(quit_button, XmactivateCallback, cb_quit, NULL);
```

`XtAddCallback` 的最后一个参数——声明为 `XtPointer` 类型——是一个指向数据的指针，当函数调用回调时，你想传递该数据。回调 `cb_quit` 具有以下原型：

```
static void cb_quit(Widget w, XtPointer client_data, XtPointer call_data):
```

回调函数是指向 `XAnyCallbackStruct` 结构的指针，该结构定义在 `<xm/xm.h>`（引用文件 `/usr/include/xm/xm.h`）中，如下：

```
typedef struct {
    int reason;    /* 指明为何调用回调 */
    XEvent event;   /* 关于关触发回调的事件信息 */
} XAnyCallbackStruct;
```

![](img/a5afb9ccf4a412511e9fcfa4280141e3_731_0.png)

`reason` 字段表示部件调用回调函数的原因。你必须咨询部件的文档来解释此字段的值。`event` 字段是一个指向 `XEvent` 结构的指针，其中包含触发回调的事件信息。

# 事件处理器注册

假设你想允许用户用鼠标在你的窗口中绘制一个部件。（Motif 为此目的提供了 `XmDrawingArea` 部件。）为了编写此功能，你想捕获窗口中的鼠标点击。Motif 工具包允许你通过类似于部件用于回调资源的方法来实现。本质上，你可以为部件窗口中的选定事件注册自己的事件处理器。此后，当这些事件发生时，将触发你的处理器。通过使用类似于部件用于回调资源的方法来实现此。本质上，你可以为部件窗口中的选定事件注册自己的事件处理器。使用 `XtEventHandler` 为 `ButtonPress` 事件添加 `handler`：

```
XtEventHandler(drawing, ButtonMask, FALSE, handler);
```

`XtEventHandler` 的第一个参数是你正在设置的部件。第二个参数是事件掩码（mask）。第三个参数是指定事件的布尔值。第四个参数是事件处理器的指针。按照如下原型设置：

```
void handler(Widget w, XtPointer client_data)
```

如该函数所示，部件通过三个参数调用事件：

- 第一个参数是部件。

- 第二个参数是事件掩码。

- 第三个参数是触发事件的 `XEvent`。

# Motif 部件

部件集就像一个工具箱；在使用工具之前，你必须了解每个工具的作用。本节提供了 Motif 部件的概述。接下来的几节将提供你所需的部件的概述。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_732.png)

有三种 Motif 部件：

- 外壳部件（Shell widgets）提供顶层窗口。弹出对话框也使用外壳部件。

- 基本部件（Primitive widgets）代表独立部件，如标签、按钮和滚动条。

- 管理部件（Manager widgets）可以包含其他部件并管理它们的布局。该类别包括表单、消息框和滚动窗口。

所有 Motif 部件继承 Core 的资源。了解 Core 的资源很重要，因为它的资源适用于所有部件。以下是 Core 资源列表：

- Accelerators 是将键盘和鼠标事件绑定到特定动作的翻译表。

- Sensitive 是一个布尔变量，指示部件的直接父是否接收输入。要更改此资源设置，请调用 `XtSetSensitive` 函数。

- Background 是部件窗口的背景像素值。该像素值通过当前的颜色映射转换为实际 RGB（红-绿-蓝）颜色。

- BackgroundPixmap 是一个像素图（存储像素数组的内存块），用于平铺部件窗口。

- BorderColor 和 BorderPixmap 是部件边界的颜色映射和像素图。

- BorderWidth 是部件边界的宽度。

- Colormap 是部件窗口使用的颜色映射。

- Depth 是部件窗口每个像素值使用的位数。此值由 XtIntrinsics 在窗口创建时设置。

- DestroyCallback 是当你调用 `XtDestroyWidget` 销部件时调用的函数列表。

- Height 和 Width 是部件窗口的高度和宽度。

- MappedWhenManaged 是一个标志，当设置为 True 时，一旦部件被实现并管理，就会映射部件（`XtCreateManagedWidget` 函数管理部件）。你可以通过调用 `XtSetMappedWhenManaged` 函数来更改此标志。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_733_0.png)

## 第 23 章：Linux X 编程

- XmScreen 是一个指向 Screen 数据结构的指针，其中包含显示部件窗口的物理显示屏的信息。

- XmSensitive 是一个布尔变量，如果为 True，则会导致 Xt 内置函数（Intrinsics）将鼠标和键盘事件分发给部件。要更改此设置，请使用函数 `XtSetSensitive`。

- XmTranslations 是翻译表——一个事件列表，当指定的事件发生时，会调用相应的函数。

- XmNx 和 XmNy 是部件窗口左上角的 x 和 y 坐标，不包括边框。这些坐标是在父级部件的坐标系中指定的。

## 壳小部件 (Shell widgets)

Shell 小部件只管理一个子部件；其主要目的是设置应用程序的顶层窗口。Xt 内置函数提供了几类 Shell 小部件，其中最重要的类如下：

- TopLevelShell（顶层壳）

- OverrideShell（覆盖壳）

- TransientShell（瞬态壳）

当你调用 `XtInitialize` 时，Xt 内置函数会创建一个 ApplicationShell 实例，它是 TopLevelShell 的子类。Applications 和 TopLevelShell 部件用于应用程序的标准顶层窗口。窗口管理器与这些顶层窗口进行交互。

# 第四部分：利用 Linux 获取乐趣与盈利
