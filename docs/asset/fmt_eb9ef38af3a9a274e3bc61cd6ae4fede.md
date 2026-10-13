
如果你想绘制大量点并使用所有相同的 GC，可以使用 `XDrawPoints` 函数通过单个 X 协议请求同时绘制所有点。将点存储在 `XPoint` 结构体数组中。`XPoint` 结构体定义在 `<X11/Xlib.h>` 中如下：

```
typedef struct {
    short x, y; /* 点的 x 和 y 坐标 */
} XPoint;
```

按照通常方式调用 `XDrawPoints`，并将 `display`、`drawable` 和 `GC` 作为前三个参数：

```
XPoint pt[10];
int numpt = 10;
```

```
XDrawPoints(disp, win, thisGC, pt, numpt, CoordModeOrigin);
```

点数组和点数紧跟在三个标准参数之后。最后一个参数告诉服务器如何解释数组中点的坐标。你可以指定以下常量之一：

- `CoordModeOrigin` 表示坐标相对于窗口或位图的坐标点。
- `CoordModePrevious` 用于每个点的坐标是相对于前一个点的 x 和 y 偏移给出的情况。假设第一个点相对于窗口原点。

## 绘制直线

Xlib 包含了三个绘制线的函数：

- `XDrawLine`
- `XDrawSegments`
- `XDrawLines`

`XDrawLine` 函数具有以下调用语法：

```
XDrawLine(disp, win, thisGC, x1, y1, x2, y2);
```

该函数在命名为 `win` 的可绘制对象中在点 `(x1, y1)` 和 `(x2, y2)` 之间绘制一条线，使用 `GC` (`thisGC`) 中指定的线属性。

`XDrawSegments` 绘制几条不相交的线段，使用相同的图形属性。段通过 `XSegment` 结构体指定，该结构体在 `<X11/Xlib.h>` 中定义如下：

```
typedef struct {
  short x1, y1; /* 起点的坐标*/
  short x2, y2; /* 终点的坐标*/
} XSegment;
```

下面的示例显示了如何使用 `XDrawSegments` 绘制几条线：

```
Display *disp;
Window window;
GC thisGC;
XSegment lines[] = {
  (50, 80, 150, 20),
  (10, 20, 35, 60),
  (250, 10, 200, 100)
};
int numsegs = sizeof(lines) / sizeof(XSegment);
```

```
XDrawSegments(disp, window, thisGC, lines, numsegs);
```

`XDrawLines` 函数与 `XDrawPoints` 类似，区别在于：`XDrawPoints` 绘制点，而 `XDrawLines` 用线将它们连接。使用与 `XDrawPoints` 相同的参数调用 `XDrawLines`。

## 绘制和填充矩形

Xlib 包含了几个绘制矩形的函数。`XDrawRectangle` 函数用于根据左上角坐标及其宽度和高度绘制矩形。该函数调用形式如下：

```
XDrawRectangle(disp, window, thisGC, x, y, width, height);
```

为了绘制矩形周围的轮廓，`XDrawLines` 绘制以下线：

- `(x,y)` 到 `(x+width,y)`
- `(x+width, y)` 到 `(x+width,y+height)`
- `(x+width, y+height)` 到 `(x,y+height)`

你可以通过调用 `XDrawRectangles` 使用相同的 GC 绘制多个矩形，它接受矩形数组及其数量作为参数：

```
XRectangle rects[]; /* 矩形数组 */
int nrects; /* 矩形数量 */
```

```
XDrawRectangles(disp, window, thisGC, rects, nrects);
```

`XRectangle` 是用于存储矩形参数的结构体。它定义在 `<X11/Xlib.h>` 中如下：

```
typedef struct {
    short x, y; /* 左上角 */
    unsigned short width, height; /* 宽度和高度 */
} Rectangle;
```

你可以通过调用 `XFillRectangle` 绘制填充矩形。该函数的工作方式相同，使用相同的参数进行弧。

## 绘制多边形

多边形是由线条包围的图形。使用 `XDrawLines` 绘制多边形的轮廓。对于填充多边形，Xlib 提供了 `XPolygon` 函数，其用法如下：

```
int shape; /* Convex, Nonconvex 或 Complex */
int mode; /* CoordModeOrigin 或 CoordModePrevious */
```

```
XPoint points[]; /* 多边形的顶点 */
int multipoints; /* 顶点数量 */
```

```
XPolygon(disp, win, thisGC, points, multipoints, shape);
```

`mode` 参数的解释方式与绘制点时相同。请注意，如果你不确定多边形的形状，可以使用 `Complex` 作为 `shape`。绘制过程可能会慢一点，但结果是正确的。GC 中的填充规则决定哪些点被填充。你可以通过调用 `XSetFillRule` 设置填充规则。

### 第四部分：利用 Linux 娱乐与盈利

## 绘制文本

要显示文本，你首先需要选择一种字体。在 X 中，字体是存储在服务器上的资源。应用程序在使用字体之前必须加载它。当服务器成功加载字体时，它会返回一个资源 ID，应用程序随后使用该 ID 来引用该字体。在第 5 章中，你学习了如何命名字体。已知名称后，你可以通过如下调用 `XLoadFont` 函数来加载字体：

```c
Display *disp; /*标识与 X 服务器的连接 */
char fontname[] = "helvetica-bold-r140*/*/* 字体名称 */
Font helvb14; /* 字体 ID */
```

```c
if((helvb14 = XLoadFont(disp, fontname)) == None)
    printf(stderr, "Cannot load font: %s\n");
/* 处理错误。可能只需使用默认字体 */
/* ... */
```

当 `XLoadFont` 函数返回非零值（意味着函数成功）时，你可以通过设置 GC 的字体属性，开始使用示例所示的 14 点加粗 Helvetica 字体。要这样做，请如下调用 `XSetFont`：

```c
XSetFont(disp, gc, helvb14);
```

随后，每当使用 GC 绘制任何文本时，输出将是 14 点加粗 Helvetica。

由于字体是服务器驻留资源，当你的应用程序不再需要某个字体时，你应该使用 `XUnloadFont` 函数释放字体。该函数的格式如下：

```c
XUnloadFont(disp, helvb14);
```

（注：原文为 p_disp，但上下文显示为 disp；我尽可能保持文本一致）

请注意，如果你有一个使用 `helvb14` 为字体的 GC，并且你卸载了该字体，在 GC 被销毁之前，X 服务器并不会实际卸载该字体。

在你拥有了适当字体的 GC 后，应用程序可以调用以下函数之一来显示文本：

- `XDrawString(Display* display, Drawable d, GC gc, int x, int y, char* string, int length)`—仅用前景颜色绘制字符串。
- `XDrawImageString(Display* display, Drawable d, GC gc, int x, int y, const char* string, int length)`—同时使用前景和背景颜色绘制字符。
- `XDrawText(Display* display, Drawable d, GC gc, int x, int y, XTextItem* items, int nitems)`—在一行中绘制多个字符串。

## 第 23 章：Linux X 编程

每个函数在单行上绘制多个字符。前两个函数使用你作为参数提供的 GC 中指定的字体绘制所有字符。这些函数的调用方式相同，如下：

```c
char string[]; /* 要显示的字符串 */
int nchars; /* 字符串中的字符数 */

XDrawString(disp, window, thisGC, x, y, string, nchars);
XDrawImageString(disp, window, thisGC, x, y, string, nchars);
```
