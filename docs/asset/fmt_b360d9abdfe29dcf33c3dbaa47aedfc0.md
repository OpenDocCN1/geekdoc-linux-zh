
```
XGCValues gc_values;
unsigned long gc_mask = GCForeground | GCLineWidth;
gc_values.foreground = screenColor.pixel;
gc_values.line_width = 3;
GC gc = XCreateGC(display, win, gc_mask, &gc_values);
```

这些语句展示了使用 `XGCValues` 结构和相关位掩码（`gc_mask`）创建 `GC` 的“硬方法”，该掩码告诉 `XCreateGC` 要从其默认值覆盖哪些结构成员。在本例中，我们希望设置前景色和线宽，由位掩码 `GCForeground` 和 `GCLineWidth` 表示。由之前的 `XAllocNamedColor()` 调用初始化的 `screenColor.pixel` 成员为随后使用此 `GC` 的图形选择前景色。

或者，如果 `GC` 已创建，你可以通过调用 `XSetForeground()` 来更改前景色，如下所示：

```
XSetForeground(display, gc, screenColor.pixel);
```

```
typedef struct {
unsigned long pixel;
unsigned short red, green, blue;
char flags; // do_red, do_green, do_blue
char pad;
} XColor;
```

通常，`XColor` 结构中的 `pixel` 成员是你保存并用于在已分配颜色中绘制图形所需的一切。`red`、`green` 和 `blue` 值表示已分配颜色单元的 RGB 分量。然而，切勿假设符号颜色名（甚至“color”这个词）与用户实际看到的颜色有任何关系。`XColor` 结构中的 `flags` 字段仅对读写颜色单元有意义，用于指示要更改的 RGB 分量中的哪一个。在这里描述的颜色技术中，`flags` 字段毫无意义。最后的 `char` 成员 `pad` presumably 将 `XColor` 结构填充到偶数字节数。

> Note
>
> `XColor` 结构的 `red`、`green` 和 `blue` 成员使用 0 到 65535 的 `unsigned int` 值表示颜色级别。即使颜色单元中的实际值范围为 0 到 255 也是如此。`XColor` 成员值在 X 服务器中根据硬件和调色板的需要进行缩放。

## COLORING SCALED GRAPHICS

为了演示如何使用多种颜色绘制图形，Listing 28.2，`xrainbow.cpp`，在窗口中绘制了一道色彩缤纷的彩虹。该程序还演示了将图形缩放以适应窗口大小的重要技术，无论其大小如何。使用此方法，当用户调整窗口大小时，其内容会自动调整以适应新的窗口边界。Figure 28.2 显示了程序的窗口，在这里不幸没有你自己屏幕上那么色彩丰富（假设你有彩色显示器的话）。

Figure 28.2

一道色彩缤纷的彩虹演示了如何以多种颜色绘制图形，以及如何将图形缩放以适应窗口边界。

![](img/6eab91cc30158075ed10d0cabbac9029_724_0.png)

## LISTING 28.2 XRAINBOW.CPP (PARTIAL)

```
Display *display;    // X server display structure

#define MAXCOLORS 7  // Number of colors in following arrays

char *Roy_G_Biv[] = {
```

## 清单 28.2（续）

```
"Red",
"Orange",
"Yellow",
"Green",
"Blue",
"Violet",
"DarkViolet"  // Violet
};

unsigned long colors[ MAXCOLORS ];
void GetColors(unsigned long intDefaultColor);
void PaintRainbow(Window win, GC gc,
int winWidth, int winHeight);

int main()
{
    // Attempt to establish communications with the X Server
    //
    display = XOpenDisplay(NULL);
    if (display == NULL) {
        cerr << "Failure connecting to X Server";
        exit(1);
    }
    ...
    // Fill global colors array using intBlackColor for the
    // default color if any allocation fails.
    //
    GetColors(intBlackColor);
    // Specify the types of events we want to receive
    //
    XSelectInput(display, win,
        ExposureMask | KeyPressMask | StructureNotifyMask);
    // The event loop.
    //
    bool done = false;
    XEvent event;
    while (!done) {
        XNextEvent(display, &event);
        switch (event.type) {
            case Expose:
                if (event.xexpose.count == 0) {
                    XClearWindow(display, win);
                    PaintRainbow(win, gc, intWidth, intHeight);
                }
                break;
            case ConfigureNotify:
                intWidth = event.xconfigure.width;
                intHeight = event.xconfigure.height;
                break;
            case KeyPress:
                cout << "Keypress detected" << endl;
                done = true;  // Exit on any keypress
                break;
        }
    }
```

在 X 客户端中，分配多种颜色的方法有很多，但这里展示的是其中最通用的一种。首先，按照清单中的方式创建一个颜色名称字符串数组。在这里，我将数组命名为 `Roy_G_Biv`，以纪念那个容易记住的首字母缩略词，它代表了彩虹的基本颜色：红、橙、黄、绿、蓝、靛、紫。然而遗憾的是，X 并未定义 Indigo，而且自带的 Violet 颜色太浅——所以我用 Violet 和 DarkViolet 两种颜色替换了数组的最后两个颜色名称。

除了颜色名称字符串数组，还需要定义一个 `unsigned long` 值数组，每种颜色对应一个：

```
unsigned long colors[ MAXCOLORS ];
```

如果你需要访问该结构中的其他字段，也可以创建一个 `XColor` 对象数组，但这里我们只需要保存由 `XAllocNamedColor()` 返回的像素值。连接到 X 服务器后，示例程序调用一个本地函数 `GetColors()` 来填充 `colors` 数组。这个函数（位于清单末尾附近）会为每个颜色名称字符串调用 `XAllocNamedColor()`，并将返回的像素值赋给 `colors` 数组。如果有任何颜色无法分配，程序会分配一个默认颜色（这里为黑色）。在这个例子中，这样做可能并不合适，因为在单色系统上，如果所有颜色都默认为黑色，结果看起来就不太像彩虹了。不过，这恰恰指出了在 X 下使用颜色时的一个难点：永远无法预测颜色图形的确切效果，总是需要一点猜测加上一些信念。

然而，由于我们使用的是颜色名称，程序在大多数系统上应该都能正常运行。为了真正绘制彩虹，程序在收到 `Expose` 事件时会调用另一个本地函数 `PaintRainbow()`。该函数通过调用 Xlib 图形原语函数 `XFillArc()` 来绘制半月形，其参数设置为用连续的弧形填充窗口，从而模拟彩虹。最后一次对 `XFillArc()` 的调用会将最终的半月形擦除为窗口的背景色，完成这个幻觉。注意 `XSetForeground()` 是如何在绘制弧形之前从 `colors` 数组中逐个分配像素值的。
