
如此原型所示，控件通过三个参数调用事件处理器：第一个参数是控件的 ID。第二个参数是在注册此事件处理器时作为 `XtAddEventHandler` 最后一个参数传递的指针。第三个参数是触发函数调用的 `XEvent` 结构体指针。

请参见“X 事件摘要”（X event summary）章节以获取 X 事件的摘要。

# Motif 控件

控件集就像任何一个工具箱；在使用工具之前，你必须了解每个工具的作用。本节提供了 Motif 控件的概述，以便你学习控件分类以及每个分类的功能。此外，你还应该学习如何使用每个分类中的重要控件。你将能够选择符合你需求的控件并在应用程序中使用它们。

Motif 控件存在三类不同的类别：

- 外壳控件（Shell widgets）为 Motif 提供顶层窗口。弹出对话框也使用外壳控件。
- 基础控件（Primitive widgets）代表独立控件，如标签（labels）、推按钮（push buttons）和滚动条（scrollbars）。
- 管理控件（Manager widgets）可以将其控件作为子控件，并管理子控件的布局。该类别包括表单（forms）、消息框和滚动窗口。

# 第 26 章：GUI 编程

所有 Motif 控件都继承自名为 Core 的控件的资源。了解 Core 控件的资源是非常重要的，因为它的资源适用于每一个控件。Core 资源如下：

- `XnMaccelerators` 是翻译表，将一系列键盘和鼠标事件绑定到特定操作上。
- `XMnancestorSensitive` 是一个布尔变量，指示控件的直接父级是否接收输入事件。要更改此资源设置，请调用 `XtSetSensitive` 函数。
- `Xmbackground` 是控件窗口的背景像素值。该像素值通过当前的调色板转换为实际的 RGB（红绿-蓝）颜色。
- `XmbackgroundPixmap` 是一个位图（pixmap，一个存储像素值数组的内存块），用于对控件窗口进行平铺。
- `XmnborderColorPixmap` 和 `XmnborderPixmap` 是控件窗口边框的调色板和位图。
- `XmnborderWidth` 是控件窗口边框的宽度。
- `Xncolormap` 是控件窗口中每个像素值所使用的位数。Xt Intrinsics 在窗口创建时会设置此值。
- `XndestroyCallback` 是通过调用 `XtDestroyWidget` 函数销控件时调用的函数列表。
- `Xmheight` 和 `Xwidth` 是控件窗口的高度和宽度，包括边框宽度。
- `XmmappedWhenManaged` 是一个标记，当设置为 True 时，一旦控件被实现（realized）并被管理（由 `XtCreateManaged` 函数管理控件），就会映射该控件窗口。你可以通过调用 `XtSetMappedWhenManaged` 函数来更改此标记。
- `Xmsensitive` 是一个布尔变量，当为 True 时，会将鼠标和键盘事件分发给控件。要更改此资源，请使用函数 `XtSetSensitive`。
- `XmnTranslations` 是翻译表——一个事件列表，当指定的事件发生时会调用相应的函数。
- `Xmnx` 和 `Xmy` 是控件窗口左上角的 x 和 y 坐标。坐标是在父控件的坐标坐标系中指定的。

# 外壳控件

外壳控件只管理子控件；外壳控件的主要用途是设置应用程序的顶层窗口。Xt Intrinsics 提供了几类外壳控件，其中最重要的包括：

- TopLevelShell
- OverrideShell
- TransientShell

当你调用 `XtAppInitialize` 时，Xt Intrinsics 会创建一个 `ApplicationShell` 控件实例，它是 `TopLevelShell` 的子类。`ApplicationShell` 和 `TopLevelShell` 控件用于应用程序的普通顶层窗口。窗口管理器与这些顶层窗口交互。

`TransientShell` 类用于弹出对话框，作为用户可以移动但不能缩为图标的顶层窗口。要创建对话框，请使用 `TransientShell` 的子类 `DialogShell`。Motif 包含了几个便利函数，允许你创建一个 `DialogShell` 控件并将其放在另一个控件中，例如选择框或消息框。这些便利函数的名称以 `XmCreate` 开头并以 `Dialog` 结尾（例如 `XmCreateDialog`）。

`OverrideShell` 控件是一种绕过窗口管理器的 Shell。窗口管理器不会在 `OverrideShell` 周加上边框。Motif 定义了 `OverrideShell` 的子类——`XMenuShell` 来显示弹出菜单。

# 基础控件

所有 Motif 控件都派自 `XmPrimitive` 类，而该类又是 `Core` 类的子类。`XmPrimitive` 类定义了一组所有基础控件都继承的标准资源。以下 8 个控件直接派生自 `XmPrimitive` 类：

- `ArrowButton` 显示一个带有箭头的按钮。你可以指定箭头的方向。
- `Text` 显示并编辑多行复合字符串。文本可以包含多种字体、颜色、带下划线的文本和嵌入的制表符。
- `Label` 在窗口内显示字符串或位图。
- `List` 显示项目列表，用户可以从中选择一个或多个。
- `Sash` 充当两个窗格之间的分隔符。用户可以拖动 `sash` 来调整窗格的大小。
- `ScrollBar` 是一个在末端带有箭头和滑块的滚动条。滚动条可以是水平的或垂直的。
- `Separator` 用于分离菜单中的项目。
- `Text` 控件作为单行或多行编辑器。
- `TextField` 显示单行可编辑文本。

这些子类专门化了 `Label` 类的功能：

- `CascadeButton` 当用户点击 `CascadeButton` 时，显示关联的下拉菜单。
- `DrawnButton` 是一种允许你在上面绘图的按钮（这样你可以在按钮上显示任何内容）。
- `PushButton` 是一个标准的推按钮。
- `OffButton` 在小按钮旁边显示字符串或位图。该按钮表示两个状态：开启或关闭。当用户点击按钮时，状态会发生。

所有控件都继承 `XmPrimitive` 类的资源。`XmPrimitive` 类的一些重要资源包括：

- `XmShadowColor` 是用于绘制控件阴影底部和右侧的像素值。这两个侧统称为底部阴影。
- `XmShadowPixMap` 用于绘制底部阴影的位图。
- `XmForeground` 是基础控件使用的前景颜色。
- `XmHelpCallback` 是可以绑定到提供上下文帮助的函数的回调列表。
- `XmHighlightColor` 用于高亮控件窗口的颜色。例如，推按钮在用户点击时会被高亮。
- `XmHighlightOnEnter` 是一个布尔变量，当设置为 True 时，请求控件在光标进入窗口时高亮窗口（前提是输入焦点跟随指针；拥有输入焦点的窗口获得输入焦点）。如果用户必须点击来指示输入焦点，则忽略此资源。

# 第五部分：在红帽 Linux 上编程

## 管理部件 (Manager Widgets)

这些部件派自 `XmManager` 类——该类是 `Constraint` 类的子类，而后者又继承自 `Composite` 类。管理部件可以作为其他子部件的容器，并管理子部件的布局。某些管理部件（如 `Form`）允许你通过约束指定布局，例如“将此部件附加到容器的左边缘”。

所有管理部件都从 `XmManager` 类继承其资源。`XmManager` 资源与 `XmPrimitive` 类资源相似。

有几个重要的管理部件：

- `Command` 组件是 `SelectionBox` 的一种类型，提供了命令历史机制。它有一个命令输入区域，用户可以在其中输入命令。当你按回车键执行命令时，该命令字符串会被保存到历史缓冲区中，并显示在可滚动列表区域。你可以使用 `Command` 组件为你的命令驱动型应用程序接受用户输入。
- `DrawingArea` 组件提供了一个空窗口，你可以在其中绘制图形或文本（使用本章后面“选择概述”中描述的 Xlib 函数）。
- `FileSelectionBox` 组件是 `SelectionBox` 的特殊类型，它在列表框中显示文件名列表。该部件有一个区域，用户可以在其中输入文件过滤器，这是一个用于定位感兴趣文件的搜索字符串（例如，`.*` 会显示所有以 `..` 结尾的文件名）。用户的当前选择显示在另一个框中。部件底部有四个标记为 OK、Filter、Cancel 和 Help 的按钮。
- `Form` 组件支持通过某些资源指定复杂的布局，这些资源是部件附加到其每个子部件的。这些资源被称为“约束资源” (constraint resources)；实际上，它们提供了一种语言，让你指示子部件在 `Form` 中的放置方式。每个约束资源都指示子部件相对于 `Form` 或另一个部件的空间关系。
- `Frame` 组件在单个子部件周围显示一个框架（带有 3D 阴影）。
- `MainWindow` 组件为应用程序的主窗口提供标准布局。`MainWindow` 管理了菜单栏、`Command` 组件、`DrawingArea` 组件和滚动条的组合。
- `MessageBox` 组件显示一条消息和行三个标记为 OK、Cancel 和 Help 的按钮。
- `PanedWindow` 组件将其子部件垂直排列在窗格中。
- `RowColumn` 组件按行和列排列其子部件。你可以在菜单栏和拉取菜单中使用 `RowColumn` 组件。
- `Scale` 组件显示一个带有滑块的长矩形，允许用户输入数值。你可以为刻度条设置最小值和最大值，并对于浮点值，你可以指定小数点后的数字位数。
- `ScrolledWindow` 管理一个工作区域（可以包含其他部件）和两个滚动条（水平和垂直）。
- `SelectionBox` 组件在可滚动框中显示项目列表，并提供一个显示当前选择的区域。该部件有三个标记为 OK、Cancel 和 Help 的按钮。你可以选择性开启或关闭标记为 Apply 的第四个按钮。

## Xlib 与 Motif

你可以使用 Motif 部件来构建 Motif 应用程序的用户界面，但仅凭 Motif 部件无法构建大多数真实世界的应用程序。假设你的应用程序用于查看天气预报的卫星图像。你可以使用 Motif 部件让用户选择卫星图像，甚至可以准备一个可滚视图区域来显示图像。然而，为了显示图像，你必须依赖 Xlib 函数。在 Motif 应用程序中，使用 Xlib 函数来显示图像、图形和文本。此外，你可能需要编写代码来响应 X 事件。

底线是，即使你在大多数应用程序中使用了 Motif 工具包，也必须学习带有 Xlib 函数的 X 编程基础。接下来的几节将提供 Xlib 和 X 事件的概述。此外，你将在 Motif 应用程序中看到 Xlib 绘制函数的示例。

## Xlib 概述

X 系统使用客户端/服务器模型提供服务。X 服务器负责显示器的输入输出。X 应用程序是客户端，通过发送 X 协议请求来使用服务器的能力。X 协议请求通过客户端和 X 服务器之间的通信链路传输。如果客户端和服务器运行在不同的机器上，该链路就是网络连接。如果客户端和服务器在同一台机器上，通信可以通过共享内存块或操作系统支持的其他进程间通信 (IPC) 机制进行。

尽管你可以编写通过向服务器发送 X 协议请求来执行所有输入输出的 X 应用程序，但这样做就像直接用机器语言为微处理器编程一样。为了减轻程序员的工作，X 窗口系统包含了 Xlib，这是一组 C 语言函数和宏，X 应用程序可以使用它们来访问 X 服务器的功能。

由于 Motif 基于 X，因此 Motif 应用程序也是一个 X 客户端；在底层，Motif 应用程序通过调用 Xlib 函数工作。

Xlib 的主要目的是为 C 语言程序员提供一种向服务器发送 X 协议请求的简单方法。然而，Xlib 不仅仅是一组与所有可能的 X 协议请求一一一对应的函数；它还包含了便利函数，以减轻处理常见任务的负担，同时向程序员完全隐藏 X 协议。例如，只存在一种 X 协议用于创建窗口，但 Xlib 有创建窗口的例程：`CreateSimpleWindow` 和 `CreateWindow`（前者比后者更简单）。同样，窗口的前景和背景颜色是在图形上下文 (GC) 中指定的。要设置这些颜色，只需调用 `XForeground` 和 `XBackground`。Xlib 负责在指定的 GC 中设置这些颜色。

## 第 26 章：GUI 编程

## 关于 Xlib 和 Motif 编程的更多信息

本章提供了 Motif 编程的概述以及 Xlib 函数如何在 Motif 应用程序中使用。然而，单章节不足以提供你充分利用 Xlib 力量所需的所有信息。由于 Xlib 和 Motif 编程的流行，已经有很多关于这些主题的书籍。要更全面地讨论 Xlib 和 Motif 工具包，请参阅以下书籍：

- 第 2 ：Xlib Reference Manual, O'Reilly & Associates, 1993
- 第 6A ：Motif Programming Manual, Second Edition, Dan Heller, Paula Ferguson and David Brennan, O'Reilly & Associates, 1994
- 第 6B ：Motif Reference Manual, Paula Ferguson and David Brennan, O'Reilly & Associates, 1993
- 第 1 ：Xlib Programming Manual, O'Reilly & Associates, 1993

Xlib 还包含许多与与 X 服务器交互无关的实用函数。Xlib 工具函数帮助你从资源文件中获取用户选择、处理屏幕图像和位图、将颜色名称翻译为像素值，以及使用资源管理器。

## Xlib 函数概述

广义地说，Xlib 函数允许应用程序打开 X 显示器（连接到 X 服务器）、创建窗口并在其中绘图、检索事件，最后关闭显示器。如果你正在开发 Motif 应用程序，只需要少量的 Xlib 函数即可完成。例如，如果你使用 Motif 工具包，就不必担心打开显示器的问题。在 Motif 应用程序中，你主要使用 Xlib 的图形、图像和文本输出函数。

表 26-1 总结了常用的 Xlib 函数，并按任务进行了分类。此列表并非完整，但相当长。作为一名 Motif 程序员，你不需要学习所有的函数；此列表让你对 Xlib 的功能有一个整体了解。要获取 Xlib 函数的完整覆盖，请参阅侧边栏中列出的“关于 Xlib 和 Motif 编程的更多信息”。

# 第五部分：红帽 Linux 编程

| 表格 26-1：按任务分组的常用 Xlib 函数 |
| 任务 | 用的 Xlib 函数 |
|---|---|
| 打开/关闭 X 显示器 | XOpenDisplay XCloseDisplay |
| 获取用户选择 | XGetDefault XrmInitialize XrmGetResource XrmParseCommand |
| 创建/管理窗口 | XCreateSimpleWindow XCreateWindow XDestroyWindow XMapRaiseWindow XUnmapWindow XGetWindowAttributes XChangeWindowAttributes |
| 控制窗口的大小和位置 | XGetGeometry XMoveWindow XResizeWindow XMoveResizeWindow XRaiseWindow XCirculateSubWindow |
| 与窗口管理器交互 | XSetProperties XGetWMHints XSetWMHints |
| 获取并处理事件 | XSelectInput XEventsQueued XNextEvent XPeekEvent |
| 与服务器同步 | XFlush XSync Synchronize |
| 处理错误 | XSetText XErrorHandler XSetIOErrorHandler |
| 操作图形上下文 | XCreateGC XChangeGC XCopyGC XFreeGC XSetForeground XSetBackground XSetFunction |
| 绘制图形 | XDraw XArcs DrawLine DrawLines XSDashes XSetArcMode XDrawPoints DrawPoint DrawRectangle DrawRectangles XFillArc XFillSet XFillRectangle XFillRectangles XFillPolygon XSetLineAttributes |
| 清除和复制区域 | XClearWindow XClearArea XCopyArea XPlane |
| 绘制文本 | XLoadFont XQueryFont XSetFont XUnloadFont DrawString XDrawImage XTypeText ListFonts |
| 使用颜色 | XDefaultColorMap XDefaultVisual XGetVisualInfo XParseColor XAllocColor XStandardColorMap XSetWindowColorMap XFreeColors |

# 第 26 章：GUI 编程

| 任务 | 常用的 Xlib 函数 |
|---|---|
| 显示图像 | XCreatePixmap XFreePixmap XCreatePixmapFromBitmapData XReadBitmapFile XWriteBitmapFile XCreateImage DestroyImage XGetImage XPutPixel XGetPixel |
| 处理鼠标和键盘输入 | XQueryPointer TranslateCoordinates XCreateCursor XDefineCursor XFreeCursor XUndoCursor XMotionEvents XLookupString XRefreshKeyboardMapping XRebindKeysym |
| 进程间通信 | XInternAtom XChangeProperty GetWindowProperty XDeleteProperty XSendEvent XGetSelectionOwner XSetSelectionOwner XConvertSelection |

# Common Xlib 特性

尽管 Xlib 有许多函数，但这些函数共享一些共同特性。了解这些共同特性可以帮助你有效地使用 Xlib。这些共同特性分为以下几类：

- 共同头文件
- 函数和数据结构的命名规范
- 函数调用中的参数顺序

# 头文件

如果你在程序中使用 Xlib 函数，你必须包含这些头文件：

```c
```
