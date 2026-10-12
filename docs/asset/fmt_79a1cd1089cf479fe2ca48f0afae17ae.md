
| `XLookupString` | 将按键事件转换为 ASCII 字符串、keysym 和 ComposeStatus。 |
| `XSetForeground` | 设置给定 GC（图形上下文）的前景属性。 |
| `XDrawString` | 在可绘制实体中绘制文本字符。 |
| `XSetStandardProperties` | 提供一种方法，使简单应用程序可以通过单个调用设置最核心的属性。 |
| `ButtonPressMask` | 指定将按钮按下选择为当前窗口的事件。 |
| `XSelectInput` | 请求 X 服务器报告与指定事件相关的事件。 |
| `XCreateGC` | 创建并返回一个 GC；可以与任何根窗口和深度作为指定的可绘制实体一起使用。 |
| `XSetBackground` | 设置给定 GC 的背景属性。 |
| `XSetForeground` | 设置 GC 中的前景像素值。参数为 Display、GC 和无符号整数前景。 |
| `XClearWindow` | 清除指定窗口中的区域。 |
| `XMapRaised` | 映射窗口及其所有具有映射请求的子窗口，并将窗口置于栈顶。 |
| `FreeGC` | 销毁 GC 以及所有关联存储。 |
| `DestroyWindow` | 销毁指定的窗口及其所有子窗口，并导致 X 服务器为每个窗口生成 DestroyNotify 事件。 |

`XClearWindow` - 清除窗口，但不发送显示（exposure）事件。参数为 Display 和指定的窗口。

## 2.4 使用 XCB

在本节中，我们将详细介绍另一个用于创建交互式 X Window 系统应用程序官方客户端库。我们将展示在实际编写 XCB 客户端应用程序代码之前，需要考虑的一些基本的自顶而下考虑因素。然后，我们将展示如何编译和链接 XCB 程序。最后，我们提供了使用 XCB 编程的示例。

正如第 2.3.9.3 节关于 Xlib 的内容提到的，从在线资源为 XCB 汇编自己的文档集，并根据各自的文档对这两个库进行比较将对你有帮助。我们还鼓励你将本节中示例的基本结构和复杂性与 Xlib 提供的示例程序进行比较。

# 章末练习

2.16 使用在线资源、打印文档和书籍，为 XCB 以及上一节的 Xlib 创建你自己的文档集。文档比较中最重要的部分是对比目录并进行分类和组织，以便有效地为你个人提供服务，展示文档如何从自顶而下的概述落实到使用库的最底层细节。这种方法（我们在这里只能进行部分说明和规定）将允许你获取我们的示例并对其进行扩展，以便在你可能遇到用例的情况下，能够编写更复杂的 Windows 应用程序。

### 2.4.1 XCB 自顶而下的考虑因素

XCB 在在线文档中强调的几个维度上比其前身 Xlib 更高效。对于初学者来说，XCB 客户端应用程序程序符合第 2.3.7.2 节中的基本结构。这种通过调用 XCB 函数和与 XCB 数据结构相互作用来实现的结构结构，与第 2.3.9.1 节所示的 Xlib 程序的基本结构非常相似。当然，你必须用 XCB 函数调用替换 Xlib 函数调用。在此重复该基本结构，并在必要处进行相应的函数调用替换：

为 XCB 编写的客户端应用程序通常按如下方式运行：

- 1. 使用 `xcb_connect()` 建立与 X 服务器的，如果无法连接，则优雅地终止程序。
- 2. 轮询服务器获取物理屏幕信息，并使用获取的信息计算窗口参数（如尺寸、位置等）。
- 3. 使用 `xcb_create_window()` 在物理屏幕上创建窗口。
- 4. 为窗口管理器设置标准属性。
- 5. 选择并指定为了工作而需要接收并响应的事件类型。
- 6. 如果将在窗口中输出文本，则加载用于该文本的字体。
- 7. 创建一个 GC 来控制绘制请求的操作。
- 8. 使用 `xcb_map_window()` 显示窗口。
- 9. 开始并持续（或逻辑上）迭代（循环），以处理来自服务器的可能事件，并向客户端发送回调。
  - a. 可能在窗口中执行实际的绘制操作。通过响应由映射窗口产生的显示（expose）事件以及随后的其他显示事件，调用绘制文本和位图图形的例程来实现。
  - b. 处理事件直到到达 `KeyPress` 或 `ButtonEvent`（这结束了不确定迭代），然后关闭显示连接，清理环境并退出。

X Windows System Wayland, Xwayland, Wayfire, GTK, Qt, Gnuplot 139

#### 2.4.1.1 XCB API

XCB 的应用程序编程接口（API）结构有两个基础层：底层是支持建立 X 服务器连接的 XCB Connection 层，以及中间的 XCB 协议层。XCB 协议层为 X 协议提供了直接的 C API。还有许多可用的 API 提供客户端和服务器之间其他类型的交互。XCB API 使用 Xlib 风格的“事件循环”方法进行交互。与阻塞并缓存请求的 Xlib 不同，XCB 请求被转换为“回复 Cookie”（reply cookies），这使得事件被缓存。XCB 具有高效的数据结构。正如我们在 2.3.9.1 节中看到的，与 Xlib 主机/显示器/屏幕的划分不同，XCB 将连接限制在单个显示器上。事件和请求队列的建立和刷新方式最重要的是：客户端和服务器之间的一种纯异步的交互形式。XCB 数据结构/函数调用 API 可以被分为各种类别，例如创建连接和 XID 的函数、非阻塞请求（如绘制原语）、阻塞请求、数据检索以及事件处理器。

#### 2.4.1.2 XCB 文档

为了补充你自己的 XCB 文档集，我们在本书 Github 站的以下存储库中提供了大量的核心 API 和主要 XCB 函数的在线字母排序列表：`github.com/bob48/unittextbook`

该列表标题为 `xcb_functions.doc`。列表中的每个条目均采用以下形式：

### 函数原型

| 数据结构函数名称 | ( 类型定义 参数 1 |
| | 类型定义 参数 2 |
| | ... ... |
| | ) |

函数的简要描述。

参数

| 参数 1 描述。 |
| 参数 2 描述。 |
| ... |

返回

对函数返回内容的描述。

函数的详细描述。

引用。该函数引用的其他函数。

从该函数列表中提取的一个示例函数如下：

```
xcb_void_cookie_t xcb_create_window ( xcb_connection_t * c,
uint8_t depth,
cb_window_t wid,
cb_window_t parent,
int16_t x,
int16_t y,
uint16_t width,
uint16_t height,
uint16_t border_width,
uint16_t class,
cb_visualid_t visual,
uint32_t value_mask,
const void * value_list )
```

创建一个窗口。

# X Windows System, Wayland, Xwayland, Wayfire GTK, Qt, Gnuplot 141

## Parameters

- **c depth**:
指定新窗口的深度。特殊值 `XCB_COPY_FROM_PARENT` 表示深度从父窗口继承。
- **wid**:
你将用于引用新窗口的 ID，由 `xcb_generate_id` 创建。
- **parent**:
新窗口的父窗口。
- **x**:
新窗口的 X 坐标。
- **y**:
新窗口的 Y 坐标。
- **width**:
新窗口的宽度。
- **height**:
新窗口的高度。
- **border_width**: 如果类为 InputOnly 或发生了 `xcb_match_error_t` 错误，则必须为 0。
- **class**:
`xcb_window_class_t` 值的位掩码。
- **visual**:
指定新窗口视觉效果（visual）的 ID。特殊值 `XCB_COPY_FROM_PARENT` 表示视觉效果从父窗口继承。
- **value_mask**:
`xcb_cw_t` 值的位掩码。

## Returns

一个 cookie

作为指定父窗口的子创建一个未映射（unmapped）窗口。将生成一个 CreateNotify 事件。新窗口在兄弟窗口的堆叠顺序中位于顶部。

坐标系中 X 轴为水平，Y 轴为垂直，原点 `[0, 0]` 位于左上角。坐标是以像素为单位的整数，并与像素中心对齐。每个窗口和位图（pixmap）都有自己的坐标系。对于窗口，原点是内部左上角的边框。

创建的窗口尚未显示（映射），调用 `xcb_map_window` 来显示它。

创建的窗口最初将使用与其父窗口相同的光标。

引用 `XCB_CREATE_WINDOW`。
