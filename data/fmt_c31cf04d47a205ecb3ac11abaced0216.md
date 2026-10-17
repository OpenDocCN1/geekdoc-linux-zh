
### 表 3.1 事件

| 事件名称 | 描述 |
| :--- | :--- |
| `GDK_ENTER_NOTIFY` | 映射到 X11 EnterNotify 事件。指针进入了窗口。 |
| `GDK_LEAVE_NOTIFY` | 映射到 X11 LeaveNotify 事件。指针离开了窗口。 |
| `GDK_FOCUS_CHANGE` | 映射到 X11 FocusIn 或 FocusOut 事件。事件结构中的一个字段用于识别是哪种。窗口获取或丢失了焦点。 |
| `GDK_CONFIGURE` | 映射到 X11 ConfigureNotify 事件。正在通知窗口尺寸、位置、边框或堆叠顺序的某些。 |
| `GDK_MAP` | 映射到 X11 MapNotify 事件。窗口状态变为映射（显示）。 |
| `GDK_UNMAP` | 映射到 X11 UnmapNotify 事件。窗口状态变为未映射（隐藏）。 |
| `GDK_PROPERTY_NOTIFY` | 映射到 X11 PropertyNotify 事件。窗口属性已更改或删除。 |
| `GDK_NOTHING` | 映射到 X11 空。你不应该看到它。 |
| `GDK_DELETE` | 这是来自窗口管理器请求删除窗口的消息。 |
| `GDK_DESTROY` | 映射到 X11 Destroy 事件。窗口已被销毁。 |
| `GDK_EXPOSE` | 映射到 X11 Exposure 事件。窗口部分被暴露。 |
| `GDK_NO_EXPOSE` | 映射到 X11 NoExposure 事件。目标区域完全绘制。 |

### 表 3.1 事件（续）

| 事件名称 | 描述 |
| :--- | :--- |
| `GDK_MOTION_NOTIFY` | 映射到 X11 MotionNotify 事件。指针（通过鼠标、键盘、触摸板或通过 X 协议客户端）移动了。 |
| `GDK_BUTTON_PRESS` | 映射到 X11 ButtonPress 事件。鼠标按钮被按下。 |
| `GDK_2BUTTON_PRESS` | 在处理 X11 ButtonPress 事件时检测到鼠标双击。 |
| `GDK_3BUTTON_PRESS` | 在处理 X11 ButtonPress 事件时检测到鼠标三击。 |
| `GDK_BUTTON_RELEASE` | 映射到 X11 ButtonRelease 事件。 |
| `GDK_KEY_PRESS` | 映射到 X11 KeyPress 事件。报告所有按键，包括 Shift 和 Ctrl。 |
| `GDK_KEY_RELEASE` | 映射到 X11 KeyRelease 事件。报告所有按键，包括 Shift 和 Ctrl。 |
| `GDK_ENTER_NOTIFY` | 映射到 X11 EnterNotify 事件。指针进入了窗口。 |
| `GDK_LEAVE_NOTIFY` | 映射到 X11 LeaveNotify 事件。指针离开了窗口。 |

## 表 3.1 GDK 事件（续）

| 事件名称 |  |
| :--- | --- |
| `GDK_SELECTION_NOTIFY` | 映射到 X11 SelectionNotify 事件。请见下文讨论。 |
| `GDK_PROXIMITY_IN` | 用于感知 X Input 扩展并绘制自定义光标的程序。 |
| `GDK_PROXIMITY_OUT` | 用于感知 X Input 扩展并绘制自定义光标的程序。 |
| `GDK_DRAG_ENTER` | Motif 拖放的顶层进入。 |
| `GDK_DRAG_LEAVE` | Motif 拖放的顶层离开。 |
| `GDK_DRAG_MOTION` | Motif 拖放的移动。 |
| `GDK_DRAG_STATUS` | Motif 拖放的状态消息。 |
| `GDK_DROP_START` | Motif 拖放开始。 |
| `GDK_DROP_FINISHED` | Motif 拖放结束。 |
| `GDK_CLIENT_EVENT` | 映射到 X11 ClientMessage 事件，该事件是由客户端发送的消息。 |
| `GDK_VISIBILITY_NOTIFY` | 映射到 X11 VisibilityNotify 事件。窗口已完全或部分被遮挡。 |

请注意，某些 X11 事件并不会传递给 Gtk+。例如，MappingNotify 事件由 GDK 通过调用 `Mapping()` 来响应，这是 Xlib 客户端处理接收此类事件的标准方式。除非你计划在应用程序中处理特定事件，否则通常没有必要调用此例程。

### 事件掩码

在 Gtk+ 中，客户端还必须请求它们感兴趣的事件。这是基于每个部件（widget）的，使用了一种与调用 Xlib 中的 `XSelect` 非常相似的技术。在 Gtk+ 中，例程是调用 `gtk_widget_set_events()`。其原型如下：

```c
void gtk_widget_set_events(GtkWidget *widget, GdkEvent events);
```

参数 `events` 是一个位掩码，用于指示客户端希望从 Gtk+ 接收的事件类型，它是事件所属的小部件句柄。这并不意味着没有对小部件请求事件；GDK 实现很可能会请求一个或多个事件。事件掩码可以通过按位或（OR）一个或多个由 GDK 定义的常量来构建（见表 3.2）。

## 表 3.2 GDK 事件掩码

| 掩码 | 请求的事件 |
| :--- | --- |
| `GDK_EXPOSURE_MASK` | 暴露事件（但不包括 NoExpose） |
| `GDK_POINTER_MOTION_MASK` | 光标移动事件 |
| `GDK_POINTER_MOTION_HINT_MASK` | 所有指针事件 |
| `GDK_BUTTON_MOTION_MASK` | 按钮按下时光标移动 |
| `GDK_BUTTON1_MOTION_MASK` | 鼠标 1 键按下时光标移动 |
| `GDK_BUTTON2_MOTION_MASK` | 鼠标 2 键按下时光标移动 |
| `GDK_BUTTON3_MOTION_MASK` | 鼠标 3 键按下时光标移动 |
| `GDK_BUTTON_PRESS_MASK` | 指针按钮按下事件 |
| `GDK_BUTTON_RELEASE_MASK` | 指针按钮释放事件 |
| `GDK_KEY_PRESS_MASK` | 键按下事件 |
| `GDK_KEY_RELEASE_MASK` | 键释放事件 |
| `GDK_ENTER_NOTIFY_MASK` | 指针窗口进入事件 |
| `GDK_LEAVE_NOTIFY_MASK` | 指针窗口离开事件 |
| `GDK_FOCUS_CHANGE_MASK` | 键盘焦点的任何变化 |
| `GDK_STRUCTURE_MASK` | 窗口配置的任何变化 |
| `GDK_PROPERTY_CHANGE_MASK` | 属性的任何变化 |
| `GDK_VISIBILITY_NOTIFY_MASK` | 可见性的任何变化 |
| `GDK_PROXIMITY_IN_MASK` | 用于 X Input 扩展程序 |
| `GDK_PROXIMITY_OUT_MASK` | 用于 X Input 扩展程序 |
| `GDK_SUBSTRUCTURE_MASK` | 子窗口重配置通知 |
| `GDK_ALL_EVENTS_MASK` | 以上所有 |

上表中的掩码与表 3.1 中列出的事件并非一一对应。某些掩码会导致接收到多个事件，根据应用程序的不同，你的回调函数可能需要检查接收了哪种事件。表 3.3 将阐明掩码与事件之间的映射关系。

## 表 3.3 掩码到事件的映射

| 掩码 | 请求的事件 |
| :--- | --- |
| `GDK_EXPOSURE_MASK` | `GDK_EXPOSE` |
| `GDK_POINTER_MOTION_MASK` | `GDK_MOTION_NOTIFY` |
| `GDK_POINTER_MOTION_HINT_MASK` | `GDK_MOTION_NOTIFY` |
| `GDK_BUTTON1_MOTION_MASK` | `GDK_MOTION_NOTIFY` |
| `GDK_BUTTON2_MOTION_MASK` | `GDK_MOTION_NOTIFY` |
| `GDK_BUTTON3_MOTION_MASK` | `GDK_MOTION_NOTIFY` |
| `GDK_BUTTON_PRESS_MASK` | `GDK_BUTTON_PRESS` |
| `GDK_BUTTON_RELEASE_MASK` | `GDK_BUTTON_RELEASE` |
| `GDK_KEY_PRESS_MASK` | `GDK_KEY_PRESS` |
| `GDK_KEY_RELEASE_MASK` | `GDK_KEY_RELEASE` |
| `GDK_ENTER_NOTIFY_MASK` | `GDK_ENTER_NOTIFY` |
| `GDK_LEAVE_NOTIFY_MASK` | `GDK_LEAVE_NOTIFY` |
| `GDK_FOCUS_CHANGE_MASK` | `GDK_FOCUS_CHANGE` |
| `GDK_STRUCTURE_MASK` | `GDK_DESTROY`, `GDK_CONFIGURE` |
| `GDK_PROPERTY_CHANGE_MASK` | `GDK_PROPERTY_CHANGE` |
| `GDK_VISIBILITY_NOTIFY_MASK` | `GDK_VISIBILITY_NOTIFY` |
| `GDK_PROXIMITY_IN_MASK` | `GDK_PROXIMITY_IN` |
| `GDK_PROXIMITY_OUT_MASK` | `GDK_PROXIMITY_OUT` |

# 第 3 章 信号、对象与类型

```c
int callback_func( GtkWidget *widget, GdkEvent *event, gpointer callback_data );
```

## 类型

之前我们介绍了 Gtk+ 在接收到客户端请求的信号时调用的回调函数原型。`GdkEvent` 是一个结构联合体（union），对于表 3.1 中列出的每类型类型一个结构：

```c
union _GdkEvent
{
  GdkEventType type;
  GdkEventAny any;
  GdkEventExpose expose;
  GdkEventNoExpose no_expose;
  GdkEventVisibility visibility;
  GdkEventMotion motion;
  GdkEventButton button;
  GdkEventKey key;
  GdkEventCrossing crossing;
  GdkEventFocus focus_change;
  GdkEventConfigure configure;
  GdkEventProperty property;
  GdkEventSelection selection;
  GdkEventProximity proximity;
  GdkEventClient client;
  GdkEventDND dnd;
};
```

以下描述了 `GdkEvent` 联合体中封装的每个结构（未涵盖的是 `GdkEventProximity`，以及 `GdkEventDND`，后者是用于拖放实现的内部事件类型，书中也未进行讨论）。上述每个名称都是对应结构体的类型定义（typedef），名称相同并带有下划线缀。例如：

```c
typedef struct _GdkEventExpose GdkEventExpose;
```

在之前的例程中，如果事件指针为 NULL 或事件类型不是 `GDK_LEAVE_NOTIFY`，我们就会跳过信号函数。

## GdkEventExpose

```c
struct _GdkEventExpose {
    GdkEventType type;       /* GDK_EXPOSE */
    GdkWindow *window;
    gint send_event;
    GdkRectangle area;
    gint count;               /* 如果不为 0，则后续有多少个事件 */
};
```

事件名称字符串
`expose_event`

## 回调函数原型

```c
gint
func (GtkWidget *widget, GdkEventExpose *event, gpointer arg);
```

### 描述
暴露事件（Expose events）通过设置为 `GDK_EXPOSE` 的 type 字段来识别。`window` 标识需要重绘的窗口，`area` 定义了该事件描述的区域。如果一个窗口中有多个区域被暴露，X 服务器将发送多个暴露事件。该窗口等待的事件数量由 `count` 标识。如果你的代码忽略了 `area` 字段并在 expose 信号函数中重绘整个窗口，那么你的代码应该等待直到接收到一个 `count` 字段等于零的 expose 事件。

## GdkEventNoExpose

```c
struct _GdkEventNoExpose {
    GdkEventType type;       /* GDK_NO_EXPOSE */
    GdkWindow *window;
    gint send_event;
};
```

事件名称字符串
`no_expose_event`

## 回调函数原型

```c
gint
func (GtkWidget *widget, GdkEventAny *event, gpointer arg);
```

### 描述
当成功执行 CopyArea 或 CopyPlane X 协议时，会接收到 NoExpose 事件。只有当源图像中的所有值都能被窗口 X 服务器复制，且源窗口没有部分被遮挡，并且 CopyArea 或 CopyPlane 请求中使用的 GC 的 graphics_exposures 标志设置为 True 时，这种情况才会发生。CopyArea 被 `gdk_draw_pixmap()` 和 `gdk_window_copy_area()` 调用的。

## GdkEventVisibility

```c
struct _GdkEventVisibility {
    GdkEventType type;
    GdkWindow *window;
    gint send_event;
    GdkVisibilityState state;
}; /* GDK_VISIBILITY_NOTIFY */
```

事件名称字符串
`visibility_notify_event`

## 回调函数原型

```c
gint
func(GtkWidget *widget, GdkEventVisibility *event, gpointer arg);
```

### 描述
当窗口可见性发生变化时，会发送可见性事件。事件的 `state` 字段描述变化的性质，可以是表 3.4 中的以下内容。

表 3.4 可见性事件状态

| 值 | 含义 |
|---|---|
| `GDK_VISIBILITY_UNOBSCURED` | 窗口部分遮挡、完全遮挡或不可见，变为可见且完全未遮挡。 |
| `GDK_VISIBILITY_PARTIAL` | 窗口可见且完全未遮挡，或不可见，变为可见且部分遮挡。 |
| `GDK_VISIBILITY_FULLY_OBSCURED` | 窗口可见且完全未遮挡，或可见且部分遮挡，或不可见，变为可见且完全未遮挡。 |

## GdkEventMotion

```c
struct _GdkEventMotion {
    GdkEventType type;
    GdkWindow *window;
    gint send_event; /* GDK_MOTION_NOTIFY */
    guint32 time;
    double x;
    double y;
    double pressure;
    double xtilt;
    double ytilt;
    guint state;
    gint16 is_hint;
    GdkInputSource source;
    guint32 deviceid;
    double x_root, y_root;
};
```
