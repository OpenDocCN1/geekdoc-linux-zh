
`type` 成员被设置为唯一标识它的事件类型常量。例如，当 X 服务器向客户端应用程序发送 `GraphicsExpose` 事件时，它会带上 `XGraphicsExpose` 结构。

# 事件

| 事件掩码 (EventMask) | 情况 (Circumstances) |
| --- | --- |
| ExposureMask | 需要任何暴露事件 |
| VisibilityChangeMask | 需要任何可见性变化 |
| StructureNotifyMask | 需要任何窗口结构变化 |
| ResizeRedirectMask | 重定向此窗口的尺寸调整重定向 |
| SubstructureNotifyMask | 需要子结构通知 |
| SubstructureRedirectMask | 重定向子窗口的结构请求 |
| FocusChangeMask | 需要任何焦点变化 |
| PropertyChangeMask | 需要任何属性变化 |
| ColormapChangeMask | 需要任何调色板变化 |
| OwnerGrabMask | 当 owner_events 设置为 True 时，激活自动抓取（grabs） |

# 事件处理概述

在事件处理期间向客户端报告的事件取决于你为窗口的 `event-mask` 属性提供了哪些事件掩码。对于某些事件掩码，事件掩码与事件类型常数之间存在一对一的对应关系。例如，如果你传递了事件掩码 `ButtonMask`，X 服务器将只返回按钮事件（Button events）。大多数事件都包含一个 `time` 成员，即事件发生的时间。

在其他情况下，一个事件掩码可以映射到多个事件类型常数。例如，如果你传递了事件掩码 `SubstructureNotifyMask`，X 服务器将返回 `CircleNotify`、`ConfigureNotify`、`CreateNotify`、`DestroyNotify`、`GravityNotify`、`MapNotify`、`ReparentNotify` 或 `UnmapNotify` 事件。

另一种情况下，两个事件掩码可以映射到一个事件类型。例如，如果你传递了 `EitherPointerMask` 或 `ButtonMotionMask`，X 服务器将返回 `MotionNotify`。

下表列出了事件掩码、事件类型以及与事件类型相关的结构名称。其中某些结构实际上是 `typedef` 到两个事件类型共享的通用结构。在信息不适用的列中显示 `N.A.`。

| 事件掩码 (Event Mask) | 事件类型 (Event Type) | 结构 (Structure) | 通用结构 (Generic Structure) |
| --- | --- | --- | --- |
| ButtonMotionMask | MotionNotify | XPointerMoved | XMotionEvent |
| Button1MotionMask | | | |
| Button2MotionMask | | | |
| Button3MotionMask | | | |
| Button4MotionMask | | | |
| Button5MotionMask | | | |
| ButtonPressMask | ButtonPress | XButtonPressed | XButtonEvent |

# 事件

| 事件掩码 (Event Mask) | 事件类型 (Event Type) | 通用结构 (Generic Structure) |
| --- | --- | --- |
| ButtonReleaseMask | ButtonRelease | XButtonEvent |
| ColormapChangeMask | ColormapNotify | XColormapEvent |
| EnterWindowMask | EnterWindow | XCrossingEvent |
| LeaveWindowMask | LeaveWindow | XCrossingEvent |
| ExposureMask | Exposure | XExposeEvent |
| GGraphicsExposures in GC | GraphicsExpose | XGraphicsExposeEvent |
| | NoExposure | XNoExposureEvent |
| FocusChangeMask | FocusIn | XFocusInEvent XFocusChangeEvent |
| | FocusOut | XFocusChangeEvent |
| KeymapStateMask | KeymapNotify | XKeymapEvent |
| KeyPressMask | KeyPress | XKeyEvent |
| KeyReleaseMask | KeyRelease | XKeyReleasedEvent XKeyEvent |
| OwnerGrabButtonMask | N.A. | N.A. |
| PointerMotionMask | MotionNotify | XMotionEvent |
| PointerMotionHintMask | H.A. | N.A. |
| PropertyMask | PropertyNotify | XPropertyEvent |
| ResizeRedirectMask | ResizeRequest | XResizeEvent |
| StructureNotifyMask | CirculateNotify | XCirculateEvent |
| | ConfigureNotify | XConfigureEvent |
| | DestroyNotify | XDestroyWindow |
| | GravityNotify | XGravityEvent |
| | MapNotify | XMapEvent |
| | ReparentNotify | XReparentEvent |
| | UnmapNotify | XUnmapEvent |
| SubstructureNotifyMask | CirculateNotify | XCirculateEvent |
| | ConfigureNotify | XConfigureEvent |
| | CreateNotify | XCreateWindow |
| | DestroyNotify | XDestroyWindow |
| | GravityNotify | XGravityEvent |
| | MapNotify | XMapEvent |
| | ReparentNotify | XReparentEvent |
| | UnmapNotify | XUnmapEvent |
| SubstructureRedirectMask | CalculateRequest | XCirculateEvent |
| | ConfigureRequest | XConfigureRequest |
| | MapRequest | XMapRequest |
| N.A. | ClientMessage | XClientMessageEvent |
| N.A. | MappingNotify | XMappingEvent |
| N.A. | SelectionClear | XSelectionClear |

| 事件掩码 (Event Mask) | 事件类型 (Event Type) | 结构 (Structure) | 通用结构 (Generic Structure) |
| --- | --- | --- | --- |
| N.A. | SelectionNotify | XSelectionEvent | |
| N.A. | SelectionRequest | XSelectionRequest | |
| VisibilityChangeMask | VisibilityNotify | XVisibilityEvent | |

后续章节描述了选择不同事件掩码时发生的处理过程。这些章节根据以下处理类别进行组织：

- 键盘和指针事件
- 窗口跨越事件
- 输入焦点事件
- 键映射状态通知事件
- 暴露事件
- 窗口状态通知事件
- 结构控制事件
- 调色板状态通知事件
- 客户端通信事件

## 键盘和指针事件

本节讨论了：

- 指针按钮事件
- 键盘和指针事件

### 指针按钮事件

以下描述了当指针在某些窗口 `w` 中处理指针按钮按下，且没有正在进行的活动指针抓取（grab）时发生的事件处理。

X 服务器从根节点向下搜索 `w` 的祖先，寻找要激活的被动抓取（passive grab）。如果在 `w` 上没有找到匹配的被动抓取，事件将发送到窗口。如果找到了匹配的被动抓取，则将其激活并将事件发送给抓取所有者。

## 键盘和指针事件

本节讨论了当产生键盘或指针事件时发生的事件处理。事件将发送到具有的窗口，除非存在活动抓取。

# 事件

```c
```
