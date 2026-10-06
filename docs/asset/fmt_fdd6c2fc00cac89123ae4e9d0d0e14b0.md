
`XEvent` 结构体有一个 `type` 字段，指示发生了什么事件。在这里，你需要将 `event_return_type` 的值与以下常用常量进行对比：

- `ButtonPressMask`—任何按键按下
- `Button1PressMask`—按下 1 键
- `Button2PressMask`—按下 2 键
- `Button3PressMask`—按下 3 键
- `ButtonMotionMask`—按下任何按键时移动
- `Button1MotionMask`—按下 1 键时移动
- `Button2MotionMask`—按下 2 键时移动
- `Button3MotionMask`—按下 3 键时移动
- `KeyPress`—键盘上任何按键被按下
- `KeyRelease`—任何按键被松开
- `Exposure`—窗口被暴露（大多数应用程序会重绘）

还有许多其他可能的事件类型，但这些是最常用的类型。

# 初始化图形上下文和字体

一个 X 窗口有一个图形上下文（GC），用于指定绘制参数，如前景颜色、背景颜色和当前字体。`XFontInfo` 数据结构使用 `XLoadFont` 定义，其函数签名如下：

```
XFontStruct *XLoadFont(Display * display, char * name)
```

## 用户界面编程
第四部分

示例字体名称为 `8x10`、`9x15` 和 `fixed`。GC 通过 `XCreateGC` 创建，其函数签名如下：

```
GC XCreateGC(Display * display, Drawable d,
                unsigned long valuemask,
                XGCValues * values)
```

`Drawable` 通常是一个窗口对象，但也可以是 `PixMap`。在定义 GC 后，程序可能想要使用以下函数设置字体、前景颜色和背景颜色：

```
XSetFont(Display *display, gc, Font font)
XSetForeground(Display *display, gc, unsigned long a_color)
XSetBackground(Display *display, gc, unsigned long a_color)
```

颜色值可以通过使用 `XParseColor` 或以下宏之一获取：

```
BlackPixel(Display * display, Screen screen)
WhitePixel(Display * display, Screen screen)
```

# 在 X 窗口中绘制

在 X 窗口中的绘制是在程序接收到暴露事件（expose event）后进行的。在任何绘制命令之前，都可以更改 GC 以改变前景颜色和其他选项。以下绘制函数列表显示了 X 窗口程序员可用的图形操作示例：

```
XDrawString(Display *display, Drawable d, gc gc,
         char * string, int x, int string_length)
```

`XDrawString` 使用 GC 当前的字体和前景颜色绘制字符串：

```
XDrawLine(Display *display, Drawable d, gc gc,
           int x1, int y1, int x2, int y2)
```

`XDrawLine` 在两点 `(x1,y1)` 和 `(x2,y2)` 之间画一条线：

```
XDrawRectangle(Display *display, Drawable d, gc gc,
           int x, int y, int width, int height)
```

`XDrawRectangle` 使用 GC 当前的颜色绘制矩形：

```
XDrawArc(Display *display, Drawable d, gc,
                int x, int y, int width, int height,
                int angle1, int angle2)
```

`XFillRectangle` 使用 GC 当前的颜色填充矩形：

```
XFillRectangle(Display *display, Drawable d, gc,
                int x, int y, int width, int height)
```

`XFillArc` 使用 GC 当前的颜色填充弧形：

```
XFillArc(Display *display, Drawable d, gc,
                int x, int y, int width, int height,
                int angle1, int angle2)
```

`XFillPolygon` 使用 GC 当前的颜色填充多边形：

```
XFillPolygon(Display *display, Drawable d, gc,
                int npoints, Point *points, int close)
```

`XDrawArc` 使用 GC 当前的颜色绘制弧形：

```
XDrawArc(Display *display, Drawable d, gc,
                int x, int y, int width, int height,
                int angle1, int angle2)
```

`XDrawPolygon` 使用 GC 当前的颜色绘制多边形：

```
XDrawPolygon(Display *display, Drawable d, gc,
                int npoints, Point *points, int close)
```

`XDrawLines` 使用 GC 当前的颜色绘制多条线：

```
XDrawLines(Display *display, Drawable d, gc,
                int npoints, Point *points)
```

`XDrawStrings` 使用 GC 当前的颜色绘制多个字符串：

```
XDrawStrings(Display *display, Drawable d, gc,
                int nstrings, char **strings, int *x, int *y)
```

以下绘制函数列表显示了 X 窗口程序员可用的图形操作示例：

# X Window 编程
第 28 章

在这里，如果你找不到 `9x15`，那说明你真的修复了它。你现在准备好为窗口中的绘图操作创建一个 GC（图形上下文）：

```
gc = XCreateGC(display,win, (unsigned long)&0,&values);
XSetFont(display, gc, font_info->fid);
XSetForeground(display, gc, BlackPixel(display,screen));
```

在这里，你还为 GC 设置了字体和前景颜色。

在映射窗口（使其变为可见）之前，你需要设置供窗口管理器使用的属性，并选择你想要处理的事件：

```
XSetStandardProperties(display, win,
  "Robert May's population model",
  "Bifurcation", None,
  0, NULL);
XSelectInput(display, win, ExposureMask | ButtonPressMask);
```

在这里，你使用了默认值来编辑窗口标题以及当调用此应用程序时使用的标签。`XSelectInput` 的调用通知 X 服务器你想接收暴露（exposure）事件和任何按键事件。最后，我们准备好让窗口可见并绘制窗口内容：

```
XMapWindow(display, win);
draw_bifurcation(win,gc,display,screen,blue);
```

在 `main` 函数中唯一需要做的就是处理事件：

```
while (1) {
  XNextEvent(display, &x_event);
  switch (x_event.type) {
    case Exposure:
      draw_bifurcation(win,gc,display,screen);
      break;
    case ButtonPressMask:
      XCloseDisplay(display);
      exit(0);
    default:
      break;
  }
}
```

这个事件循环非常简单：你调用 `XNextEvent`（它会阻塞直到事件可用）来填充 `XEvent` 变量。`X_event.type` 字段是整数事件类型，你将其与 `Exposure` 和 `ButtonPressMask` 常量进行比较。如果你收到暴露事件，则窗口必须重绘，你可以再次调用 `draw_bifurcation`。如果用户在窗口中按下任何鼠标按钮，你通过 `XCloseDisplay` 关闭与 X 服务器的连接并终止程序。

## 用户界面编程

第四部分

`draw_bifurcation` 函数相当简单：

```
void draw_bifurcation(Window win, GC gc, Display *display,
    int screen, XColor font_color) {
    float lambda = 0.1;
    float x = 0.0;
    float population = 0.0;
    int x_axis, y_axis, iter;
    XSetForeground(display, win, gc, font_color.pixel);
    XDrawing(display, win, gc, 236, 22,
        "Extinction", strlen("Extinction"));
    XDrawing(display, win, gc, 16, 41,
        "Steady state", strlen("Steady state"));
    XDrawing(display, win, gc, 334, 123,
        "Period doubled", strlen("Period doubled"));
    XSetForeground(display, gc, BlackPixel(display,screen));
    for (y_axis=0; y_axis<198; y_axis++) {
        lambda = 4.0f * (0.28f + (y_axis / 250.0f));
        for (iter=0; iter<198; iter++) {
            population = lambda * x * (1.0f - x);
            x_axis = (int)(population * 500.02f);
            if (x_axis > 0.0f && x_axis < 501.0f) {
                XDrawing(display,win,gc, x_axis, y_axis, x_axis, y_axis);
            }
        }
        x = population;
    }
}
```

对于本书而言，决定在 X Window 中何处绘制点的算法并不有趣。以下函数用于在窗口 GC 中进行绘制：

- `XSetForeground`——用于在黑色和蓝色之间切换前景颜色
- `XDrawing`——用于使用 GC 设置的字体在窗口中绘制三个文本字符串
- `XDrawLine`——用于在窗口中绘制点

你调用 `XSetForeground` 来更改绘制文本和绘制线条的颜色。你通过绘制长度为 1 像素的线段来绘制点。你可以通过切换到 `src/X/xlib` 并输入以下内容来运行示例 `program.c`：

```
make
./bifurcation
```

# X Toolkit API

你已经看到 Xlib API 是一个编写 X 应用程序的基础但非常高效的库。X Toolkit（或内建库 intrinsics）库为编写部件（widgets）提供了更高级的编程方法。部件是面向对象的显示对象，例如数据输入字段、绘图工具等。它们通常用 C 语言编写，但从面向对象的角度来说，它们支持继承并通过公共 API 访问内部部件数据来维护私有数据。在下一章中，你将使用两个流行的部件集：Athena 部和 Motif 部。

# 开始使用 X Toolkit

在应用程序可以使用 X Toolkit 之前，必须在调用任何其他工具包函数之前调用以下函数（`String` 类型定义为 `char *`，`Cardinal` 定义为 `int`）：

```
Widget XtInitialize(String shell_name,
String application_class,
XrmmOptionDescRec *options,
Cardinal num_options,
int * argc, Char **argv)
```

`name` 和 `class` 参数指定应用程序顶层部件的名称和类。通常，你可以为应用程序创建一个有意义的名称，并通过将应用程序名称的首字母大写创建一个类名。`options` 参数通常可以指定为 `NULL`，表示没有特殊选项。如果你使用 `NULL` 指定选项，请将 `NULL` 作为 `num_options` 的值。最后两个参数传递给应用程序的 `main` 函数（通过移除任何 X 特有的参数进行修改）。

X Toolkit 使用指定为字符串的资源。为了提高程序的可读性，X Toolkit 和 Xlib 头文件为资源字符串定义了常量名：

```
#define XtNWidth "width"
#define XtNHeight "height"
#define XtNLabel "label"
```
