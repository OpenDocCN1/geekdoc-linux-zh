

- 事件循环：启动一个事件驱动的循环，使应用程序能够与显示器通信
- 清理：清理并优雅退出

该描述可以进一步扩展如下：

- 初始化
  - 执行初始化例程
  - 连接到 X 服务器
  - 执行 X 相关初始化
- 事件循环（while 未完成）
  - 从 X 服务器接收下一个事件
  - 处理事件，可能向 X 服务器发送各种绘图请求
  - 如果事件为退出消息，则退出循环
- 清理
  - 关闭与 X 服务器的连接
  - 执行清理操作

初始化部分为用户交互设置窗口系统。初始化后，程序进入一个循环，在该循环中它反复尝试从窗口系统获取事件并处理它们。

最后，在退出之前，程序执行必要的清理工作。通常退出代码位于当用户单击应用程序提供的退出按钮（或窗口框架右上角的关闭按钮）时调用的程序中。

## 22.4.1.3 指定资源

所有 X Window 应用程序程序都有资源文件，可以在其中指定颜色、字体等选项。为了利用此功能，程序应编写为避免硬编码资源，以便使用配置文件中指定的资源。

X 应用程序的资源配置文件将与对 XtAppInitialize() 的调用中指定的应用程序名称相同。它可以位于应用程序启动的目录中，否则 X 将在变量 XAPPLRESDIR 指定的目录中搜索此文件。

## 22.4.1.4 编写 X Window 客户端应用程序的代码

为什么展示三种不同的库和编写客户端应用程序的方法？Xlib 和 XCB 基本上是过程式编程范式库，其中 XCB 的数据结构和 API 比 Xlib 更复杂。Qt 使用面向对象的客户端编程范式，具有相应的数据结构和类，并用 C++ 编写。

Xlib 或 XCB 的应用程序代码用 C 或 C++ 编写，并使用系统上可用的任何 C/C++ 编译器编译。

在用 C++ 编程 Qt 时，该库有自己的设施来编译、链接和组装客户端应用程序，并将其置于 Qt 项目的上下文中，如第 22.4.5 节“使用 Qt 工具包”所示。

## 22.4.2 Xlib 与 XCB

我们包含 Xlib 和 XCB 客户端程序示例的原因是它们是 X Window 协议的两个官方 C 库。Xlib 是 XCB 的前身，是原始的 X 客户端库，并且在 XCB 引入之前是唯一的官方 X 客户端库。

这两个库基于非常不同的方法：Xlib 是更远离 X 协议的一层，使用传统且对程序员友好的 C API，而 XCB 是 X 协议之上的非常薄的一层，没有透明且友好的 API。

正如我们对 Xlib 和 XCB 的介绍所示，目前存在于 XCB 的文档远不如 Xlib 友好、完整和描述性。XCB 的这两个方面，即文档和用户友好性，是其与 X 协议本身复杂的[content]

- 事件循环：启动一个事件驱动的循环，使应用程序能够与显示器通信
- 清理：清理并优雅退出

该描述可以进一步扩展如下：

- 初始化
  - 执行初始化例程
  - 连接到 X 服务器
  - 执行 X 相关初始化
- 事件循环（while 未完成）
  - 从 X 服务器接收下一个事件
  - 处理事件，可能向 X 服务器发送各种绘图请求
  - 如果事件为退出消息，则退出循环
- 清理
  - 关闭与 X 服务器的连接
  - 执行清理操作

初始化部分为用户交互设置窗口系统。初始化后，程序进入一个循环，在该循环中它反复尝试从窗口系统获取事件并处理它们。

最后，在退出之前，程序执行必要的清理工作。通常退出代码位于当用户单击应用程序提供的退出按钮（或窗口框架右上角的关闭按钮）时调用的程序中。

## 22.4.1.3 指定资源

所有 X Window 应用程序程序都有资源文件，可以在其中指定颜色、字体等选项。为了利用此功能，程序应编写为避免硬编码资源，以便使用配置文件中指定的资源。

X 应用程序的资源配置文件将与对 XtAppInitialize() 的调用中指定的应用程序名称相同。它可以位于应用程序启动的目录中，否则 X 将在变量 XAPPLRESDIR 指定的目录中搜索此文件。

## 22.4.1.4 编写 X Window 客户端应用程序的代码

为什么展示三种不同的库和编写客户端应用程序的方法？Xlib 和 XCB 基本上是过程式编程范式库，其中 XCB 的数据结构和 API 比 Xlib 更复杂。Qt 使用面向对象的客户端编程范式，具有相应的数据结构和类，并用 C++ 编写。

Xlib 或 XCB 的应用程序代码用 C 或 C++ 编写，并使用系统上可用的任何 C/C++ 编译器编译。

在用 C++ 编程 Qt 时，该库有自己的设施来编译、链接和组装客户端应用程序，并将其置于 Qt 项目的上下文中，如第 22.4.5 节“使用 Qt 工具包”所示。

## 22.4.2 Xlib versus XCB

我们包含 Xlib 和 XCB 客户端程序示例的原因是它们是 X Window 协议的两个官方 C 库。Xlib 是 XCB 的前身，是原始的 X 客户端库，并且在 XCB 引入之前是唯一的官方 X 客户端库。

这两个库基于非常不同的方法：Xlib 是更远离 X 协议的一层，使用传统且对程序员友好的 C API，而 XCB 是 X 协议之上的非常薄的一层，没有透明且友好的 API。

正如我们对 Xlib 和 XCB 的介绍所示，目前存在于 XCB 的文档远不如 Xlib 友好、完整和描述性。XCB 的这两个方面，即文档和用户友好性，是其与 X 协议本身复杂的

In practice, the difference in organizing schemes is most evident in how the two libraries handle the fundamental asynchronous event-request model between server and client of the X protocol itself. Xlib attempts to implement the asynchronous X protocol behind a mixed synchronous and asynchronous API, whereas the XCB API is asynchronous.

For example, to look up the attributes (e.g., size and position) of a window, you would write the following code using Xlib:

```
XWindowAttributes attrs;
XGetWindowAttributes(display, window, &attrs);
/* Execute some code */
```

The Xlib call to XGetWindowAttributes() in the client-side program sends a request to the X server and blocks until it receives a reply from the X server. This is a synchronous request-event sequence.

The following is the code for the same thing in XCB:

```
xcb_get_window_attributes_cookie_t cookie = xcb_get_window_attributes(connection, window);
/* Execute other code while waiting for the reply from the server */
xcb_get_window_attributes_reply_t *reply = xcb_get_window_attributes_reply(connection, cookie, NULL);
/* Execute some code based on the reply */
```

