
最后，在退出之前，程序执行必要的清理工作。通常退出代码位于当用户单击应用程序提供的退出按钮（或窗口框架右上角的关闭按钮）时调用的程序中。

## 22.4.1.3 指定资源

所有 X Window 应用程序程序都有资源文件，可以在其中指定颜色、字体等选项。为了利用此功能，程序应编写为避免硬编码资源，以便使用配置文件中指定的资源。

X 应用程序的资源配置文件将与对 `XtAppInitialize()` 的调用中指定的应用程序名称相同。它可以位于应用程序启动的目录中，否则 X 将在变量 `XAPPLRESDIR` 指定的目录中搜索此文件。

## 22.4.1.4 编写 X Window 客户端应用程序的代码

为什么展示三种不同的库和编写客户端应用程序的方法？`Xlib` 和 `XCB` 基本上是过程式编程范式库，其中 `XCB` 的数据结构和 API 比 `Xlib` 更复杂。`Qt` 使用面向对象的客户端编程范式，具有相应的数据结构和类，并用 C++ 编写。

`Xlib` 或 `XCB` 的应用程序代码用 C 或 C++ 编写，并使用系统上可用的任何 C/C++ 编译器编译。

在用 C++ 编程 `Qt` 时，该库有自己的设施来编译、链接和组装客户端应用程序，并将其置于 `Qt` 项目的上下文中，如第 22.4.5 节“使用 Qt 工具包”所示。

## 22.4.2 Xlib versus XCB

我们包含 `Xlib` 和 `XCB` 客户端程序示例的原因是它们是 X Window 协议的两个官方 C 库。`Xlib` 是 `XCB` 的前身，是原始的 X 客户端库，并且在 `XCB` 引入之前是唯一的官方 X 客户端库。

这两个库基于非常不同的方法：`Xlib` 是更远离 X 协议的一层，使用传统且对程序员友好的 C API，而 `XCB` 是 X 协议之上的非常薄的一层，没有透明且友好的 API。

正如我们对 `Xlib` 和 `XCB` 的介绍所示，目前存在于 `XCB` 的文档远不如 `Xlib` 友好、完整和描述性。`XCB` 的这两个方面，即文档和用户友好性，是其与 X 协议本身复杂的

In practice, the difference in organizing schemes is most evident in how the two libraries handle the fundamental asynchronous event-request model between server and client of the X protocol itself. `Xlib` attempts to implement the asynchronous X protocol behind a mixed synchronous and asynchronous API, whereas the `XCB` API is asynchronous.

For example, to look up the attributes (e.g., size and position) of a window, you would write the following code using `Xlib`:

```
XWindowAttributes attrs;
XGetWindowAttributes(display, window, &attrs);
/* Execute some code */
```

The `Xlib` call to `XGetWindowAttributes()` in the client-side program sends a request to the X server and blocks until it receives a reply from the X server. This is a synchronous request-event sequence.

The following is the code for the same thing in `XCB`:

```
xcb_get_window_attributes_cookie_t cookie = xcb_get_window_attributes(connection, window);
/* Execute other code while waiting for the reply from the server */
xcb_get_window_attributes_reply_t *reply = xcb_get_window_attributes_reply(connection, cookie, NULL);
/* Execute some code based on the reply */
```

free(reply);

函数 `xcb_get_window_attributes` 向 X 服务器发送请求，并立即返回而不等待回复。这是一个异步请求-事件序列。客户端程序必须调用 `xcb_get_window_attributes_reply` 来阻塞等待回复。

异步方法的优势在于当我们需要同时检索多个窗口的属性时显现出来。使用 `XCB`，我们可以一次向 X 服务器发出多个请求，然后等待多个回复。而使用 `Xlib`，我们必须等待每个请求的响应后才能发送下一个请求。`XCB` 只需阻塞一个往返网络延迟周期，而 `Xlib` 则需要多次延迟周期等待。

为了完全异步，`XCB` 方法导致了更复杂的数据结构方法，以及一个对程序员不太友好的 API。前面 `Xlib` 的代码看起来像你平均的 C 库调用；`XCB` 代码具有更复杂的数据结构实现。

`XCB` 是完全异步的，而 `Xlib` 并非完全同步。`Xlib` 具有同步和异步 API 的混合。那些不返回值的函数（例如 `XResizeWindow`，它改变窗口大小）是异步的，而返回值的函数（例如 `XGetGeometry`，它返回窗口的大小和位置）是同步的。以下是摘自 *Xlib Programming Manual* 第 1 卷中关于 `Xlib` 同步性的引述：

> Buffering
>
> `Xlib` 保存请求而不是立即发送给服务器，以便客户端程序可以继续运行而不是在每次 `Xlib` 调用后等待获得网络访问权限。这是因为大多数 `Xlib` 调用不需要服务器立即执行。这种由客户端在发送到网络前对请求进行分组的做法也提高了大多数网络的性能，因为它使网络事务更长且更少，减少了涉及的总开销。

## 22.4.3 Xlib

在本节中，我们给出使用 `Xlib` 的编程示例。将这里给出的代码的复杂性与下一节中给出的 `XCB` 编程代码进行比较会很有用。此外，还请比较 `Xlib` 的文档程度与 `XCB` 可用的文档。

### 22.4.3.1 基本 Xlib 理论考虑

`Xlib` 采用客户端-服务器模型，这可以直接与这些组件的传统网络模型形成对比。本质上，用于 `Xlib` 的客户端-服务器模型颠倒了网络模型中假定的客户端和服务器的角色。下面，我们为您提供在 `Xlib` 模型中编程的实用介绍。

### 22.4.3.2 编译一个 Xlib 客户端应用程序

请注意，在 PC-BSD 系统上，您可能需要下载并安装 GNU C 编译器（版本 47 或最新可用版本），以便以下示例程序能够运行，如果尚未由您的系统管理员完成的话。如果您是系统管理员，您可以使用 PC-BSD 中的 AppCafe 中的程序或使用 Solaris 中的存储库为自己执行此操作。

在我们的 PC-BSD 系统上，我们使用了以下编译器命令以及所示的选项和参数。在 Solaris 上，您可以用 `gcc47` 替换 `gcc`。

```
gcc47 input_file.c -o output_file -lX11
```

这里，`input_file.c` 是您的 C 源代码文件名，`output_file` 是可执行程序的名称。

### 22.4.3.3 示例 Xlib 客户端应用程序

以下是三个基础的示例 `Xlib` 程序。每个程序前面都有一个说明程序功能的陈述，以及一个列出所调用的 X Window 函数及其描述的表格。要获取有关函数调用的更多信息——例如它们特定的参数列表数据结构和内容——请参阅本章末尾提供的 `Xlib` 在线文档。

#### 22.4.3.3.1 Xlib 示例程序 test2.c 目标：绘制一个黑色 500×500 像素的窗口，周围环绕着您系统上运行的窗口管理器的窗口装饰。然后，五秒后，窗口将消失。

Functions called (Table 22.7):

Code:

```
/*Standard includes*/
#include <stdio.h>
#include <stdlib.h>
#include <X11/Xlib.h>
#include <X11/Xutil.h>
#include <X11/Xos.h>
#include <X11/Xatom.h>
#include <X11/keysym.h>
/*Variable and pointer declarations*/
Display *dis;
```

### TABLE 22.7 Xlib Display Functions

| Xlib Function Name | Description |
|---|---|
| `XOpenDisplay` | 返回一个显示结构，作为与 X 服务器的连接 |
