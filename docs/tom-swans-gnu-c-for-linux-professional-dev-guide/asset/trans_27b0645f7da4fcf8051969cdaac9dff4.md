

screenColor 和 exactColor 都填充了程序可用于显示彩色图形的值。第一个值很可能是一个共享的像素值，表示 X 服务器能找到的最接近匹配的颜色。exactColor 表示所请求颜色的确切 RGB 值。你可以使用任一返回值，但第一个可能产生更一致的结果。

> Note
> 这里的颜色选择技术仅用于演示目的，生产软件不应如此严格地设置颜色。相反，你的程序应尽可能显示所有可用颜色，并让用户自行选择实际想要的颜色。

如果 XAllocNamedColor() 失败就结束程序，当然是一种极端的措施。在大多数情况下，如果函数返回 false，你的程序可能应采取其他措施——选择更有可能可用的替代颜色（例如用 green 代替 ForestGreen）。请记住，你始终可以退回到 BlackPixel() 和 WhitePixel() 宏。这些值即使在单平面单色系统上也能工作，因此在最坏的情况下，如果 XAllocNamedColor() 失败，一个编写良好的 X 客户端应简单地以黑白显示其图形。只有在这种做法不切实际时，程序才应在无法分配所请求颜色时结束。

成功调用 XAllocNamedColor() 后，你可以使用返回的像素值。基本上，使用已分配颜色有两种方法。你可以在使用 XCreateSimpleWindow() 或 XCreateWindow() 函数创建窗口时指定返回的像素值，或者你可以设置图形上下文中的前景色。示例程序使用后一种技术，通过以下语句创建 GC：

```
XGCValues gc_values;
unsigned long gc_mask = GCForeground | GCLineWidth;
gc_values.foreground = screenColor.pixel;
gc_values.line_width = 3;
GC gc = XCreateGC(display, win, gc_mask, &gc_values);
```

这些语句展示了使用 XGCValues 结构和相关位掩码（gc_mask）创建 GC 的“硬方法”，该掩码告诉 XCreateGC 要从其默认值覆盖哪些结构成员。在本例中，我们希望设置前景色和线宽，由位掩码 GCForeground 和 GCLineWidth 表示。由之前的 XAllocNamedColor() 调用初始化的 screenColor.pixel 成员为随后使用此 GC 的图形选择前景色。

或者，如果 GC 已创建，你可以通过调用 XSetForeground() 来更改前景色，如下所示：

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

通常，XColor 结构中的 pixel 成员是你保存并用于在已分配颜色中绘制图形所需的一切。red、green 和 blue 值表示已分配颜色单元的 RGB 分量。然而，切勿假设符号颜色名（甚至“color”这个词）与用户实际看到的颜色有任何关系。XColor 结构中的 flags 字段仅对读写颜色单元有意义，用于指示要更改的 RGB 分量中的哪一个。在这里描述的颜色技术中，flags 字段毫无意义。最后的 char 成员 pad  presumably 将 XColor 结构填充到偶数字节数。

> Note
> XColor 结构的 red、green 和 blue 成员使用 0 到 65535 的 unsigned int 值表示颜色级别。即使颜色单元中的实际值范围为 0 到 255 也是如此。XColor 成员值在 X 服务器中根据硬件和调色板的需要进行缩放。

## COLORING SCALED GRAPHICS

为了演示如何使用多种颜色绘制图形，Listing 28.2，xrainbow.cpp，在窗口中绘制了一道色彩缤纷的彩虹。该程序还演示了将图形缩放以适应窗口大小的重要技术，无论其大小如何。使用此方法，当用户调整窗口大小时，其内容会自动调整以适应新的窗口边界。Figure 28.2 显示了程序的窗口，在这里不幸没有你自己屏幕上那么色彩丰富（假设你有彩色显示器的话）。

Figure 28.2
一道色彩缤纷的彩虹演示了如何以多种颜色绘制图形，以及如何将图形缩放以适应窗口边界。

![](img/6eab91cc30158075ed10d0cabbac9029_724_0.png)

## LISTING 28.2 XRAINBOW.CPP (PARTIAL)

```
Display *display;    // X server display structure

#define MAXCOLORS 7  // Number of colors in following arrays

char *Roy_G_Biv[] = {
```
