

- 如果事件队列为空，XNextEvent() 会刷新 Xlib 请求队列，将所有待处理的请求（如绘图命令）发送到 X 服务器。
- 如果事件队列为空，在刷新请求队列之后，XNextEvent() 会阻塞，意味着它不会在从 X 服务器接收到新事件之前返回。

获取每个事件后，大多数客户端应用程序使用 switch 语句分支到一个或多个用于处理特定事件的语句。（请参阅表 26.2 获取 X 事件类型名称列表。）在这种情况下，程序响应三种事件类型，并为每一种显示一条消息。要查看这些语句的效果，请在移动和调整程序窗口大小时查看用于启动 xwelcome 的终端窗口。

在此示例中，唯一执行有用操作的事件是 KeyPress。要结束事件循环，switch 语句中该事件的 case 会执行以下语句：

```
case KeyPress:
  cout << "Keypress detected" << endl;
  done = true;  // Exit on any keypress
  break;
```

这会将 done 设置为 true 并结束 while 循环。之后，程序通过调用另一个 Xlib 函数并从 main() 返回来关闭与 X 服务器的连接：

```
XCloseDisplay(display);
return 0;
```

调用 XCloseDisplay() 会断开客户端/服务器连接，取消映射所有客户端窗口（使其变得不可见），并销毁服务器为此客户端保存的所有相关数据结构。然而，尽管调用 XCloseDisplay() 是终止 X 客户端的正确方法，但并不能保证程序会执行到前面的语句。传递给窗口管理器的另一个事件可能会终止客户端/服务器连接，在 XNextEvent() 返回之前关闭程序的任务。例如，如果窗口在标题栏中有默认的关闭按钮，并且用户点击了该按钮，窗口管理器本身会接收到相关事件并终止客户端，导致屏幕上出现如下消息：

```
X connection to :0.0 broken (explicit kill or server shutdown).
```

> 提示
> 防止此常见消息的一种方法是使用带有析构函数调用 XCloseDisplay() 的 C++ 类将整个客户端封装起来。声明该类的全局对象可确保在程序终止序列期间调用析构函数。

## THE XWELCOME.CPP LISTING

作为参考，清单 26.3 显示了前面各节中描述的完整 xwelcome.cpp 清单。此文件位于 CD-ROM 上的 c26/xwelcome 目录中。

### LISTING 26-3 XWELCOME.CPP

```cpp
#include <iostream.h>      // Need exit()
#include <stdlib.h>

#include <X11/Xlib.h>       // Most X programs need these headers
#include <X11/Xutil.h>
#include <X11/Xos.h>

Display *display;            // X server display structure

int main()
{
    // Attempt to establish communications with the X Server
    //
    display = XOpenDisplay(NULL);
    if (display == NULL) {
        cerr << "Failure connecting to X Server";
        exit(1);
    }

    // Calculate window's dimensions and position
    //
    int intScreenNum = DefaultScreen(display);
    int intDisplayWidth = DisplayWidth(display, intScreenNum);
    int intDisplayHeight = DisplayHeight(display, intScreenNum);
    int intWidth = intDisplayWidth / 3;
    int intHeight = intDisplayHeight / 8;
    int intXPos = 0;
    int intYPos = 0;

    // Get the most basic of colors (black and white)
    //
    int intBlackColor, intWhiteColor;
    intBlackColor = BlackPixel(display, intScreenNum);
    intWhiteColor = WhitePixel(display, intScreenNum);

    // Create window (this does not make it visible)
    Window win =
    XCreateSimpleWindow(
        display,                   // X server display struct
        DefaultRootWindow(display), // Parent window
        intXPos, intYPos,          // Position
        intWidth, intHeight,       // Window width & height
        0,                          // Border width (default)
        intBlackColor, intWhiteColor); // Background, foreground

    // Assign a name for the window title bar (probably)
    //
    XStoreName(display, win, "Welcome to X Programming");

    // Map the window to the display
    // Window is visible when first Expose event is received
    //
    XMapWindow(display, win);

    // Specify the types of events we want to receive
```
