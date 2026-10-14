

## 客户端间通信

原子（Atom）是客户端之间进行通信的唯一可靠方法。尽管你可能会尝试使用其他技术，但请记住，在网络环境中，两个客户端必须运行在物理上分离的机器上，而且可能类型不同。即使是在客户端间通信，使用临时文件也是不安全的。相反，可以考虑使用原子属性来传输信息。如果原子与根窗口关联，那么你可以确信它对于运行在用户 X 服务器上的所有客户端都是可用的。

在客户端之间传递信息的最佳且最简单的方法之一，就是使用 X 服务器提供的八个剪切缓冲区之一。剪切缓冲区（cut buffer，又称剪贴板）是一个原子属性，其名称从 XA_CUT_BUFFER0 到 XA_CUT_BUFFER7。大多数客户端使用第一个剪切缓冲区在彼此之间传输文本信息。清单 28.4（xcut.cpp）演示了当该剪切缓冲区发生变化时，客户端如何收到通知，以及如何检索缓冲区的内容。

```
Listing 28.4  X CUT.CPP (PARTIAL)

// Specify the types of events we want to receive
//
XSelectInput(display, win,
ExposureMask | KeyPressMask | PropertyChangeMask );
XSelectInput(display, DefaultRootWindow(display),
PropertyChangeMask);

// The event loop
//
bool done = false;
XEvent event;
int nbytes = 0;
char *s = NULL;
while (!done) {
```

### 清单 28.4（续）

```
XNextEvent(display, &event);
switch (event.type) {
case Expose:
    cout << "Expose event received" << endl;
    break;
case PropertyNotify:
    cout << "PropertyNotify event" << endl;
    s = XFetchBytes(display, &bytes);
    if (s != NULL && nbytes > 0) {
        cout << "Property changed: " << s << endl;
        XFree(s);
    }
    break;
case KeyPress:
    cout << "Keypress detected" << endl;
    done = true;  // Exit on any keypress
    break;
}
```

要使客户端在剪切缓冲区被更改时收到通知，有必要为根窗口指定 PropertyChangeMask。根窗口拥有剪切缓冲区原子，因此仅将 PropertyChangeMask 添加到我们窗口的事件中是不够的。显然，为根窗口和客户端窗口都选择此事件掩码并无坏处，而且这似乎可以确保窗口创建时最初生成该事件。但如果你不想这样做，可以从第一次调用 XSelectInput() 时删除 PropertyChangeMask。

### 注意

> 你不必选择接收剪切缓冲区更改的通知。或者，你可以使用此处展示的相同技术，在响应其他类型的事件（例如鼠标按钮单击或按键）时访问剪切缓冲区。不过，你可能会希望使用 PropertyChangeMask 设置一个标志，以指示剪切缓冲区中有新信息可用。通常，客户端这样做是为了启用“粘贴”（Paste）菜单命令或按钮，在 UNIX 中它通常被称为 Yank 命令。

当用户向剪切缓冲区插入数据时，PropertyNotify 事件的 switch case 将被选中。程序调用 XFetchBytes() 来检索信息——该函数始终使用被标识为 XA_CUT_BUFFER0 的第一个缓冲区。要使用其他剪切缓冲区，可以调用类似的 XFetchBuffer() 函数。要向缓冲区插入数据，请调用 XStoreBytes() 或 XStoreBuffer()。

始终像示例程序所示那样调用 XFree() 来释放 XFetchBytes() 或 XFetchBuffer() 返回的字符串数据。这些数据是服务器中保存信息的副本，因此释放它不会妨碍这些信息被再次使用。

## 线条与填充样式

在 X 客户端应用程序中，所有图形输出都是参照图形上下文（Graphics Context，简称 GC）进行的。本章与前两章展示了许多创建和使用简单 GC 的示例，但本节将解释一些你无疑会想使用的更高级功能。借助 GC，你可以选择线条样式，也可以设置用于填充对象（如弧线和矩形）的像素图图案。

### 线条宽度与样式

X 服务器能够以任何实际宽度和多种样式绘制线条。线条样式不仅影响直线，也影响其他形状的轮廓，因此这些概念几乎在每一个图形程序中都会发挥作用。清单 28.5（xdash.cpp）展示了创建实线和虚线的最简单方法。该程序还展示了一种更改虚线宽度的方法——这是一个晦涩的特性，在许多教程中既不明显，也没有得到很好的解释。图 28.3 显示了该程序的窗口。（第三行的背景颜色在本页上可能可见，也可能不可见，但在屏幕上应该是淡黄色。）

### 图 28.3

示例 xdash.cpp 窗口，显示三种线条样式：LineSolid、LineOnOffDash 和 LineDoubleDash。

![](img/6eab91cc30158075ed10d0cabbac9029_732_0.png)

### 清单 28.5 XDASH.CPP（部分）

```
// Create a graphics context for our window
//
XGCValues gc_values;
unsigned long gc_mask = GCDashList;
gc_values.dashes = 24; // Width of dashes and spaces
GC gc = XCreateGC(display, win, gc_mask, &gc_values);

// Paint lines in different styles
void PaintLines(Window win, GC gc,
    int winWidth, int winHeight)
{
    int x1, y1, x2, y2;
    unsigned int lineWidth = 8;

    x1 = 0;
    y1 = lineWidth * 6;
    x2 = winWidth;
    y2 = y1;

    XSetForeground(display, gc, colors[0]);
```

