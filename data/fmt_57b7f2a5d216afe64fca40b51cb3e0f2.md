
图 2-2：窗口系统控制对视频硬件的访问

![](img/49715b3934121066e59e93823d33ee3a_65_0.png)

窗口系统在应用程序和视频硬件之间形成了一个中间层。通常情况下，图形应用程序不再能够直接访问视频硬件，而是向窗口系统发送请求，在应用程序窗口内显示图像（图 2-3）。

图 2-3：通过窗口管理器访问屏幕

![](img/49715b3934121066e59e93823d33ee3a_65_1.png)

窗口开销（windowing penalty）的引入。通常情况下，我们必须接受这种性能损失，因为良好的图形程序必须能够在窗口内运行。不能期望每个图形应用程序都始终允许访问整个设计，并拒绝与其他运行的图形应用程序共存。然而，性能问题并没有表面看起来那么局限。上一章描述的将 `3D` 硬件加速集成到 `X Window` 系统中的努力已经产生了高性能的 `X` 架构。随着更快的 `3D` 硬件和高效的 `X` 接口，使用 `X` 带来的性能损失变得可以忽略不计。

然而，设计良好的程序会将应用程序代码与底层的屏幕访问代码隔离。应用程序应该只通过抽象的 `C++` 类接口将屏幕视为逻辑输出设备进行访问。这允许应用程序将其输出显示在各种物理类上——例如在 `X` 下的未加速窗口上、使用硬件加速的全屏，或者使用另一个操作系统（如 `Microsoft Windows`）的窗口上。

> 抽象类是指至少包含一个纯函数且不能实例化的类。具体类是非抽象的类，尽管它可能继承自抽象类。抽象类是面向对象设计的关键，因为它们代表了问题领域特征性的、基础的抽象，且与“无关”细节无关。“无关”的细节通过重写纯虚函数在派生的具体类中实现，但通过抽象接口类的用户可以对抽象类的所有变体（过去和未来）保持兼容。这项工作能够生效的前提是，抽象类必须是对该类所表示的数据类型所有过去和未来变体的通用、特征性分类，从而通过子类化实现未来的灵活性兼容性。找到合适的抽象类等同于识别或定义问题领域中基础的、通用抽象，这是面向对象设计中最困难的部分之一。

因此，从应用程序的角度来看，它的显示被定向到一个我们称为“屏幕的的逻辑输出设备。实际上，屏幕将由窗口系统查看，并且只使用物理显示器的一部分，这一事实对于程序是隐藏的，因此程序可以配置（在运行时）使用不同的输出设备。

在 `Linux` 操作系统，对视频内存的“直接访问”通常通过图形库 `SVGALIB` 完成，正如我们在第 1 章看到的，这在很大程度上已经过。`X Window System` 现在规范对视频硬件的访问。

因此，除了全屏硬件加速图形外，当我们使用“屏幕”一词时，实际上指的是在 `X Window System` 下创建的显示窗口。

让我们看看如何在 `X` 下创建窗口，然后看看如何在窗口中显示图像。

## X 程序的结构

`X Window System` 与窗口系统一样，是一个事件驱动的系统，它会通知各个窗口感兴趣的事件，从而允许窗口做出响应。例如，当窗口处于激活状态时按下按键将自动（通过窗口系统）向窗口发送按键事件。该窗口的应用程序代码随后将通知事件并调用函数来响应该事件；这种事件驱动的函数被称为回调函数。响应事件调用相应的函数被称为事件分发。

![](img/49715b3934121066e59e93823d33ee3a_67_0.png)

编写 `X Window System` 是一个非常广泛的专业领域；已有许多关于该主题的著作。为了本书的目的，我们不会深入探讨 `X` 的复杂细节，而是简单地将 `X` 视为一种显示窗口化 `2D` 图像的机制。（这本身就很复杂！）正如将在第 4 章中解释的，`3D` 图形最终也是转换为 `2D` 图像。

让我们从检查 `X` 程序的典型结构开始；在下一节中我们将处理图形显示。在伪代码中，一个典型的 `X` 应用程序如下：

```
create_window();
ask_to_be_notified_of_interesting_events();
while({
  if event_pending_for_window({
    dispatch_event(); // 调用回调函数
  }
});
```

该程序无非一个经典的事件轮询循环。我们有一个无限循环等待事件发生，然后对该事件做出反应。在大多数情况下，特定的事件（例如输入 `q` 或点击退出按钮）最终将导致程序退出事件轮询循环并终止执行。

有了这些理解，我们现在可以对上一章中创建的示例程序进行详细分析。

### 列表 2-1：hello.cc

```c
#include <stdio.h>
#include <X11/Intrinsic.h>
#include <X11/Xlib.h>

#define SCREEN_X 320
#define SCREEN_Y 200

int main() {
    Display *dpy;
    Visual *vis;
    Window w;
    
    // 建立服务器连接
    dpy = XOpenDisplay(NULL);
    
    // 创建映射（显示）窗口
    vis = DefaultVisual(dpy,0);
    
    w = XCreateWindow(dpy, RootWindow(dpy,0),
                        100, 100,
                        SCREEN_X, SCREEN_Y,
                        0, 0, vis, None);
    
    XStoreName(dpy, w, "hello");
    XMapWindow(dpy, w);
    XSelectInput(dpy, w, KeyPressMask);
    
    XEvent event;
    char *ch;
    KeySym keysym;
    int xcompstat;
    
    while(1) {
        if(XNextEvent(dpy,&event)) {
            XLookupString(&event.x.key, ch, 1, &keysym, &xcompstat);
            switch(keysym) {
                case 'q':
                    exit(0);
            }
        }
    }
}
```

## Xlib、 Toolkit 与抽象类

`hello.cc` 程序包含以下头文件：

```c
#include <stdio.h>
#include <X11/Intrinsic.h>
#include <X11/Xlib.h>
```

每个 `C` 程序员都熟悉 `stdio.h`（标准输入输出库头文件），但 `X` 头文件对你来说可能是新的。`/usr/include/X11/Intrinsic.h` 和 `/usr/include/X11/Xlib.h`。你可能想浏览一下这些文件以获得了解。

出现在尖括号 `<>` 中的 `#include` 文件路径位于 `/usr/include` 或 `/usr/local/include`。这些目录是 `Linux` 系统的标准目录。

本例中的 `X` 并不包含机信息，而是 `Xlib` 库和 `Toolkit` 的函数定义。`Xlib` 是一个用于控制 `X` 服务器窗口输出输入的低级 `C` 库。`Toolkit` 是一个用于编程 `X` 的高级函数库，分为两个部分：`Xt` 抽象和一组小部件。图 2-5 形象地展示了 `Xlib`、`Xt` 抽象和小部件集之间的关系。

与其他操作系统相反，理论上可以在不使用任何库的情况下编写应用程序。这是因为 `X` 服务器协议是在网络包的字节级别定义的。`X` 客户端可以直接与 `X` 服务器建立 `TCP/IP` 网络连接，并手动发送、接收和解码字节包，以控制 `X` 服务器上的显示。然而，这将绝对复杂，但了解从技术上讲 `X` 库是一种便利而非必需品是很有用的。

## 第 2 章：访问屏幕

接下来，我们为屏幕定义了一些常量：

```
#define SCREEN_SIZE 320
#define SCREEN_YSIZE 200
```

## 连接到 X 服务器

由于 `X` 是一个客户端-服务器系统，而且由于我们的程序都是 `X` 客户端，我们必须连接到 `X` 服务器以便创建窗口并在屏幕上显示图形。`hello.cc` 声明了变量 `dpy`，它代表指向 `Display` 结构的指针。`Display` 表示我们的应用程序（`X` 客户端）与 `X` 服务器（连接到显示器的服务器）之间的连接。

```
Display *dpy;
```

在真正的客户端-服务器设置中，如果 `X` 服务器和 `X` 客户端位于两个物理独立的机器上，客户端与服务器之间的连接可能是 `TCP/IP` 网络连接。在本地设置中（即 `X` 服务器和 `X` 客户端位于同一台机器上），连接将通过某些本地进程间通信协议完成。

让我们来看一下 `Display` 结构的定义。它位于 `/usr/include/X11/Xlib.h`：

- 显示特定数据的类型类型。
- 该结构的内容取决于实现。
- 应用程序代码应将 `Display` 视为不透明的结构。

```c
#ifndef XLIB_ILLEGAL_ACCESS
typedef struct _XDisplay Display;
#endif
```

如结构所示，我们不需要——也不应该知道 `Display` 结构的内部细节，因为它的内容取决于具体的实现，并且不能保证在 `FreeX11` 的不同实现或版本中保持不变。这是信息隐藏这一面向对象技术的典型示例，特定类或结构的用户可以免于不可避免的、已发生或将发生的变更。通过将 `Display` 结构视为不透明的，我们确保了当 `Display` 结构的内部表示发生变化时，我们的程序仍能继续运行。

> 注意：这个信息隐藏的例子有些极端，`Display` 结构是完全不透明的；作为它的用户，我们无法访问它的任何部分。更一般地说，面向对象设计中的类将向外部世界暴露一个公共接口，该接口必须是一个相对稳定的基础，类的用户（称为客户端类）可以对其产生依赖。提供者类（客户端使用的类）的内部工作要波动得多，并且“隐藏”在提供者类的私有部分中。这些部分可以在不影响客户端类的情况下进行更改，因为编译器禁止客户端类访问提供者类的私有成员，并带有错误消息终止编译。这保证了最低级别的公共/私有分离。面向对象设计中最困难的声明之一是决定类的哪些部分应该是公共的，哪些应该是私有的。这个问题有一个完整的答案，但它本质上是理论性的，基于抽象数据类型的类理论 [MEVEY7]。简而言之，这个想法是：必须无法编写出一个其正确性以任何方式依赖提供者类私有声明的客户端类。换句话说，特定提供者类的客户端正确性必须仅使用提供者类的公共声明进行形式化证明。

在声明变量 `dpy` 之后，我们可以使用 `XOpenDisplay` 函数建立与 `X` 服务器的连接：

```c
dpy = XOpenDisplay(NULL);
```

该函数的完整描述出现在在线手册中。希望你已经花时间阅读了主页中的一些条目。如果没有，这里是 `XOpenDisplay` 的完整手册条目：

```text
XOpenDisplay(X11) XLIB FUNCTIONS XOpenDisplay(X11)
- 名称
XOpenDisplay, XCloseDisplay - 连接或断开与 X 服务器的连接
- 语法
Display *OpenDisplay(display_name)
char *display_name;
XCloseDisplay(display)
Display * "display";
- 参数
display: 指定到 X 服务器的连接。
display_name: 指定硬件显示名称，它决定了要使用的显示和通信域。在符合 POSIX 的系统上，如果 display_name 为 NULL，它默认为 DISPLAY 环境变量的值。
- 描述
XOpenDisplay 函数返回一个 Display 结构，作为到 X 服务器的连接并包含有关该 X 服务器的所有信息。XOpenDisplay 通过 TCP 或 Deco 通信协议，或通过本地进程间通信协议将您的应用程序连接到 X 服务器。如果主机是主机且冒号（:）分隔了主机和显示编号，如果未指定主机，OpenDisplay 将使用 TCP 连接，Xlib 使用任何最快的传输方式。如果主机是主机且是双冒号（::），OpenDisplay 将使用 Deco 连接。单个服务器可以同时支持这些或全部这些传输机制。特定的 Xlib 实现可以支持更多此类传输机制。
如果成功，XOpenDisplay 返回指向 Display 结构的指针，该结构定义在 <X11/Xlib.h> 中。如果失败，它返回 NULL。在成功调用 XOpenDisplay 后，显示器中的所有屏幕都可以供客户端使用。display_name 参数指定的屏幕由 DefaultScreen 宏（或 DefaultScreen 函数）返回。你只有通过信息宏或函数才能访问 Display 和 Screen 结构的元素。有关使用宏和函数从 Display 结构中获取信息，请参见第 2.2.1 节。
XDisplay 函数连接到 Display 结构中指定的 X 服务器，并销毁客户端在该显示器上创建的所有窗口、资源 ID（Window、Font、Pixmap、Colormap、Cursor 和 GContext）或其他资源，除非已请求关闭资源（参见 XCloseDown）。因此，当 Display 结构内部表示发生变化时，该窗口将继续工作。
此后，XOpenDisplay 返回一个指向 Display 结构指针。
XI1, X-Display(XI1), XSetParent(XI1), XCloseDown(XI1), X-Sync(XI1)
- 参见
-Planes(XI1), XFlush(XI1), X-Sync(XI1)
- 语言
- C Language(XI1), X-Display(XI1)
- 注意：此信息隐藏的例子有些极端，Display 结构是完全不透明的；作为它的用户，我们无法访问它的任何部分。更一般地说，面向对象设计中的类将向外部世界暴露一个公共接口，该接口必须是一个相对稳定的基础，类的用户（称为客户端类）可以对其产生依赖。提供者类（客户端使用的类）的内部工作要波动得多，并且“隐藏”在提供者类的私有部分中。这些部分可以在不影响客户端类的情况下进行更改，因为编译器禁止客户端类访问提供者类的私有成员，并带有错误消息终止编译。这保证了最低级别的公共/私有分离。面向对象设计中最困难的声明之一是决定类的哪些部分应该是公共的，哪些应该是私有的。这个问题有一个完整的答案，但它本质上是理论性的，基于抽象数据类型的类理论 [MEVEY7]。简而言之，这个想法是：必须无法编写出一个其正确性以任何方式依赖提供者类私有声明的客户端类。换句话说，特定提供者类的客户端正确性必须仅使用提供者类的公共声明进行形式化证明。
```

## 创建并映射窗口

接下来，我们要屏幕创建一个窗口。为了这个目的，声明了两个变量：

```c
Visual *vis;
Window w;
```

`Visual` 结构的定义位于 `X11/Xlib.h`：

```c
/* Visual 结构；包含颜色信息。 */
typedef struct {
    XEvent *ext_data;      /* 扩展数据 */
    VisualID visualid;     /* 此视觉 ID */
#if defined (_cplus) || defined (cplusplus)
    int class;             /* 屏幕类（单色等） */
#else
    int class;             /* 屏幕类（单色等） */
#endif
    unsigned long red_mask, green_mask, blue_mask; /* 掩码 */
    int bits_per_rgb;      /* rgb 比特 */
    int map_entries;       /* 映射条目 */
} Visual;
```

`Visual` 结构定义非常简单且注释详细。它涉及屏幕的颜色。我们稍后会在“深度与视觉”章节返回这里。我们声明的变量类型为 `Window`。它在 `/include/Xlib.h` 中的声明如下：

```c
typedef unsigned long XID;
typedef XID Window;
```

`Window` 只是一个整数。第一步是使用 `DefaultVisual` 宏向 `X` 服务器请求默认视觉：

```c
vis = DefaultVisual(dpy,0);
```

有了之前的显示和现在已视觉，我们就有足够的信息来创建窗口。`CreateWindow` 函数在特定的显示上创建一个窗口。`hello` 调用该函数的方式如下：

```c
w = CreateWindow(dpy, // 显示
    DefaultRootWindow(dpy), // 父窗口
    100, 100, // x, y 位置
    SCREEN_SIZE, SCREEN_SIZE, // 宽，高
    0, // 边宽
    CopyFromParent, // 深度（我们使用掩码）
    CopyFromParent, // 视觉类（真色等）
    vis, // 视觉
    0, NULL); // 掩码
XName(dpy, w, "hello");
```

`CreateWindow` 函数有多个参数，其中某些可能需要进一步解释。特别是标记为深度、视觉类、值掩码和窗口属性的参数描述提到。

父窗口指定了要创建的窗口的父窗口。正如第 1 章所述，窗口是分级排列的。父窗口是子窗口在层级结构中的直接祖先。在这种情况下，我们指定父窗口为根窗口，它是涵盖物理屏幕的层级结构顶端的窗口。

深度和视觉类参数紧密配合以指定窗口可用的颜色数量和类型。我们将在“深度与视觉”章节中更详细地讨论。在我们的情况下，我们将这些参数指定为 `CopyFromParent`，这只是从父窗口复制值。

## 第 2 章：访问屏幕
