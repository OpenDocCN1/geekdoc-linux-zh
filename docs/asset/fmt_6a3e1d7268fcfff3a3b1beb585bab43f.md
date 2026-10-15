
![](img/786ba9bd5cd671beb490264fd2e6aae1_177_0.png)

## 第二部分 X 的组成部分

你还没有看到列表 6.5 中使用 `Xtnbackground` 资源指定颜色的方法。X 提供了几个宏来指定黑色和白色或像素值，其中两个是 `WhitePixelOfScreen` 和 `BlackPixelOfScreen`。这些宏需要一个 `Screen` 结构体参数，可以通过 `XtScreen` 宏从任何组件中获得。

X 中除黑之外的颜色规范可能是一项麻烦的任务。因此，第 7 章的整个章节专门用于创建和使用颜色。

你已经在列表 6.5 中看到了 `GxDrawArea` 组件的创建以及该组件相对于父级的放置。注意变量 `GxDrawArea` 没有在代码列表中声明。很快将证明，该变量是全局声明的，供整个应用程序使用。

继续列表 6.5，关注新函数 `XtAddEventHandler` 的引入。

```c
14: XtAddEventHandler(                /*发送事件的组件 *
14a:     GxDrawArea,
15:     PointerMask|ButtonPressMask, /* 要发送事件 *
16:     False,                         /* 不可屏蔽事件 *
17:     (XtEventHandler)drawEventProc, /* 要调用的函数 *
18:     (XtPointer)NULL);               /* 传递给函数的数据 *
```

列表 6.5 使用调用 `AddEventHandler` 为 `GxDrawArea` 组件注册了两个事件：`PointerMotion` 和 `ButtonPress`。

组件只需要 X Toolkit 通知它们满足其固有行为动作的事件。`PointerMotion` 和 `ButtonPress` 事件对于 Form 组件来说是不典型的，因为它们通常不响应用户输入。

然而，将 `GxDrawArea` Form 组件作为绘制我们图形编辑器对象的画布，则要求我们知道用户何时穿过画布移动鼠标光标，或者何时点击鼠标按钮开始或结束绘制动作。

`XtAddEventHandler` 函数允许将额外的事件添加到组件的通知列表中。

该函数期望第一个参数是要添加事件的组件。其次，`XtAddEventHandler` 函数期望一个事件掩码，其中每个位代表一个或多个事件。当指定多个事件时（如本例所示），将对要添加到组件的事件掩码进行按位或（OR）操作。

## 拓展

### 逐位操作变量值

位域操作在 X 中是常见的，作为将唯一值组合到单个变量中的有效方法。位域元素被称为掩码或标志。

实际上，变量中的每个位都代表一个唯一值。如下的声明：

```c
char fields:4;
```

将字段定义为 4 位。设置一个位将代表变量中的一个不同值，如...

### 创建按钮

为用户提供一个绘图区域是应用程序界面的一个重要元素。然而，用于请求绘图功能的按钮同样重要。

在创建用于调用绘图动作的按钮时，首要考虑的是将它们放在哪里。

> 注意：当你从零开始编写应用程序布局时，你应该对应用程序的外观有一个良好的脑海中，或者实际上随手画一张草图。我对于图形编辑器（Graphics Editor）应用程序的脑海如图 6.1 所示。

图 6.1 我对图形编辑器布局的脑海。

![](img/786ba9bd5cd671beb490264fd2e6aae1_181_0.png)

根据我对应用程序布局的想象，需要一个包含绘图按钮的框。列表 6.6 显示了一个满足此要求的函数。

#### 列表 6.6 按钮创建函数

```c
1: #include <X11/Xaw/Command.h> /* 用于使用 Command 组件 */
2: #include <X11/Xaw/Box.h> /* 用于使用 Box 组件 */
3: 
4: void create_buttons(Widget parent )
5: {
6: Widget btnnPanel, exitB;
7: 
8: /*
9: * 为绘图图标创建一个面板
10: */
```

##### 列表 6.6 继续

```c
11:   btnPanel = XtVaCreateWidget( "drawButton", 
12:                             widgetClass, parent,
13:                             XtNtop, XawChainTop,
14:                             XtRight, XawChainRight,
15:                             XtBottom, XawChainTop,
16:                             XtLeft, XawChainRight,
17:                             XtNhorizDistance, 10,
18:                             XtNfromHoriz, GxDrawArea,
19:                             XtNSpace, 1,
20:                             XtNSpace, 1,
21:                             NULL );
22:
23:   create_icons(btnPanel, drawIcons, draw_manager);
24:   XtManageChild(btnPanel);
25:
26:   exitB = XtVaCreateManagedwidget( " Exit ",
27:                              commandWidgetClass, parent,
28:                              XtNtop, XawChainBottom,
29:                              XtBottom, XawChainBottom,
30:                              XtLeft, XawChainRight,
31:                              XtRight, XawChainRight,
32:                              XtNfromVert, btnPanel,
33:                              XtNfromHoriz, GxStatusBar,
34:                              NULL );
36:   XtAddCallback(exitB, XtNcallback, gx_exit, NULL );
37: )
```

再次，你看到了 `XtVaCreateWidget` 的使用。这次实例化了一个 Box 组件来包含应用程序的绘图按钮。

通过其附加属性指定的 Box 组件的位置是相对于父组件的顶部和底部，以及右边缘和左边缘，以保持与父组件右边缘的相对距离。

这种布局确保了通过移动窗口管理器应用于的底部或右侧缩放装饰来调整应用程序大小时，会移动该框而不改变其大小；移动时的顶部和底部同步移动，右边缘和左边缘也是如此。

两个边缘（上/下和左/右）将保留它们相对于父边缘的相对位置，防止 Box 缩放，从而破坏界面的美观。画布（`GxDrawArea`）唯一需要的缩放是随 `ApplicationShell` 一起增大或缩小。比其包含的图标更大的按钮没有意义，而更大的画布意味着有更多的绘图空间。

在考虑实际将 Command 组件（按钮）放入 Box 组件的函数之前，先考虑退出（Exit）按钮的创建。

## X 应用程序的组件

再次参考列表 6.6 中创建组件的熟悉程序（第 26–34 行）。你会发现一些需要注意的区别；具体来说，退出按钮是相对于另外两个组件放置的。

`XtnfVert` 的使用告诉 Xt，顶部和底部边缘附加是根据 `XtnfVert` 资源或 `btnPanel` Box 组件的值相对于组件进行解释的。同样，`XtnfHoriz` 的使用指示 Xt 左侧和右侧组件边缘相对于名为 `GxStatusBar` 的组件，你必须已经创建了它以便作为 `XtnfHoriz` 资源的值使用。

![](img/786ba9bd5cd671beb490264fd2e6aae1_183_0.png)

> `GxStatusBar` 变量引用一个 Label 组件，应用程序使用它向用户显示指令或状态。该组件的创建在章节末尾的代码列表中进行了回顾。`GxStatusBar` 变量是全局的，因为它在整个应用程序中都被使用。
