
```c
/* 设置异或模式的 GC（用于橡皮筋框绘制） */
xcgov.foreground = bg;
xcgov.background = bg;
xcgov.function = GXor;
xorGC = XtGetGC(drawing_area, GCForeground |
    GCBackground | GCFunction, &xcgov);
```

```c
/* 为绘制区域添加回调以处理暴露（expose）事件 */
XtAddCallback(drawing_area, XmposeCallback, handle_expose,
    drawing_area);
```

```c
/* 为绘制区域创建一个交叉光标 */
xair_cursor = XCreateFontCursor(XtDisplay(drawing_area),
    xc_cursor);
```

```c
/* 为按钮事件添加事件处理器以处理绘制区域 */
XtAddEventHandler(drawing_area, ButtonPressMask, False,
    start_rubber_band, NULL);
AddEventHandler(drawing_area, ButtonMotionMask, False,
    continue_rubber_band, NULL);
AddEventHandler(drawing_area, ButtonReleaseMask, False,
    end_rubber_band, NULL);
```

```c
/* 实例化所有组件 */
XtRealizeWidget(top_level);
```

```c
/* 设置绘制区域的光标 */
XtDefineCursor(XtDisplay(drawing_area), XtWindow(drawing_area),
    xair_cursor);
```

```c
/* 设置一个在鼠标按钮按下期间将光标更改为交叉
    并限制在绘制区域内的捕捉。这是通过所谓的“捕获”实现的
*/
XGrabButton(XtDisplay(drawing_area), AnyButton, AnyModifier);
```

```c
XtWindow(drawing_area), True, ButtonPressMask|
ButtonMotionMask | ButtonReleaseMask,
GrabModeAsync, GrabModeAsync,
XtWindow(drawing_area), xhair_cursor);
```

```c
/* 释放光标 */
FreeCursor(XtDisplay(drawing_area), xhair_cursor);
```

```c
/* 启动主事件循环 */
XtMainLoop(app);
```

```c
/* start_rubberband
```

```c
/* start_rubberband */
void start_rubberband(Widget w, XtPointer data, XEvent *p_event,
Boolean *cdisp)
{
    int x = p_event->x;
    int y = p_event->y;
    /* 粗略检查确保未超出容量 */
    if (numlines < MAXLINES) {
        lines[curline].x1 = x;
        lines[curline].y1 = y;
        lines[curline].x2 = x;
        lines[curline].y2 = y;
        numlines++;
    }
}
```

```c
/* continue_rubberband */
/* 绘制时处理移动 */
void continue_rubberband(Widget w, XtPointer data, XEvent *p_event,
Boolean *cdisp)
{
    /* 在旧位置绘制一次 */
}
```

```c
/* end_rubberband */
/* 绘制结束 */
void end_rubberband(Widget w, XtPointer data, XEvent *p_event,
Boolean *cdisp)
{
    /* 更新并重绘 */
}
```

# 第23 章：Linux 上的 X 编程

- `PseudoColor`（伪色）视觉类模拟了一种常见的显示硬件——每个像素值都查找一个 RGB 值，且颜色表（colormap）可以随时被修改。
- `StaticColor`（静态色）显示与 `PseudoColor` 类似，不同之处在于颜色表不能被修改。
- `GrayScale`（灰度）视觉表示允许修改强度映射的灰度显示器。`GrayScale` 视觉是 `PseudoColor` 视觉在灰度上的等效。
- `StaticGray`（静态灰度）与 `GrayScale` 类似，但具有固定的灰级映射。黑白（单色）显示通过深度为 1 的 `StaticGray` 视觉进行建模。

X 显示器中的每个屏幕至少有一个视觉效果（visual）结构。许多服务器为屏幕提供多个一个视觉效果。例如，一个 8-位显示器的服务器可能会提供一个深度为 8 的 `PseudoColor` 视觉和一个深度为 1 的 `StaticGray` 视觉。因此，屏幕上的窗口可以作为颜色窗口，或者在 `StaticGray` 的情况下作为单色窗口。

即使服务器支持多个视觉效果，其中一个也是默认视觉效果。你可以使用宏 `DefaultVisual(display,screen)` 来引用此默认视觉效果，它返回指向由 `display` 标识的 X 显示器中指定视觉效果的 `Visual` 结构的指针。

## 可用的视觉效果

要查看系统上 X 服务器支持的视觉效果列表，请启动 X（使用 `startx` 命令），然后在 shell 提示符下输入以下命令：

```
xdpyinfo display :0.0
```

`xdpyinfo` 程序显示了关于 X 服务器的大量信息，包括视觉效果的数量。通常，X 服务器支持六种视觉效果，默认是 8-位 `PseudoColor` 视觉。

通常，你不需要选择任何视觉效果，因为默认视觉效果对于大多数应用程序都是足够的。但如果你的系统有 24 位显卡且默认视觉是 8 位的，你可能希望显式地选择并使用 24 位视觉效果。

在 Motif 应用程序中使用非默认视觉效果，你必须在部件实现（realized）之前指定顶层 shell 的三个资源——视觉类型、颜色表和深度。

## X 颜色表

在 X 中，每个窗口都有一个关联的颜色表，它决定了像素值如何翻译为颜色（在灰度显示器上为灰级）。虽然硬件可能只允许一种颜色表，但 X 允许每个窗口拥有自己的颜色表，只要屏幕的视觉类不是 `TrueColor`、`StaticColor` 或 `StaticGray`。在窗口中的像素值根据这种虚拟颜色表解释之前，该颜色表必须安装到硬件颜色表中。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_768_0.png)

![](img/a5afb9ccf4a412511e9fcfa4280141e3_768_1.png)

你需要一个窗口管理器来处理这项工作。按照惯例，窗口管理器实现策略：一旦窗口获得输入焦点，立即将窗口的颜色表安装到硬件中。

颜色表是 X 服务器的资源。通常，你不需要为你的应用程序创建新的颜色表。当服务器启动时，它会创建并安装默认颜色表。服务器通常仅在该默认颜色表中定义两个颜色单元。其余的单元可以由任何 X 应用程序分配和使用。

要使用颜色表中的颜色，你首先必须找到颜色表的标识符，它是一个类型为 `Colormap` 的变量。当你创建一个新颜色表时，得到一个 ID。对于默认颜色表，颜色表的 ID 由宏 `DefaultColormap(display,screen)` 返回，这需要你标识显示器和屏幕。你可以使用 `DefaultScreen(display)` 作为 `DefaultColormap` 的屏幕参数。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_769_0.png)

## 来自颜色表的颜色

当你在 Motif 应用程序中使用颜色时，由于许多应用程序可能使用相似的颜色，X 提供了两种分配颜色表单元的方法：

- 共享只读单元
- 私有读写单元

![](img/a5afb9ccf4a412511e9fcfa4280141e3_769_1.png)

## 共享只读单元

你可以在任何视觉类中分配共享只读单元，但要分配读写单元，视觉类必须允许修改颜色表。这意味着视觉类必须是 `DirectColor`、`PseudoColor` 或 `GrayScale`。
