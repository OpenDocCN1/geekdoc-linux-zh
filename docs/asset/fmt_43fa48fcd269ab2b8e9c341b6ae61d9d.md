
## 事件名称字符串
`motion_notify_event`

## 回调函数原型

### 描述
运动通知事件指示指针已从屏幕的一个位置移动到另一个位置。`time`字段指示事件的服务器时间（自上次服务器重置以来的毫秒数）。如果窗口与`root`在同一个屏幕上（这通常是如此），那么`x`和`y`是相对于窗口原点的坐标；否则，它们都将被设置为`0`。`x_root`和`y_root`是相对于`root`窗口的坐标。`pressure`始终设置为`0.5`，而`xtilt`和`ytilt`始终设置为`0`。`source`始终设置为`GDK_SOURCE_MOUSE`，并且始终设置为`GDK_CORE_POINTER`。如果用于选择事件的掩码是`GDK_POINTER_MOTION_HINT_MASK`，则`is_hint`设置为`1`；否则将为`0`。如果`is_hint`为`1`，则需要通过调用`gdk_window_get_pointer()`获取当前位置信息。`state`用于指定事件发生前鼠标键和修饰键的状态。`state`可能的值通过按位（OR）表 3.5 中的任何位来构造而成。

### 表 3.5 运动事件状态

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

### 表 3.5 运动事件状态（续）

| 值 | 含义 |
|---|---|
| `GDK_MOD3_MASK` | mod3 被按下。 |
| `GDK_MOD4_MASK` | mod4 被按下。 |
| `GDK_MOD5_MASK` | mod5 被按下。 |
| `GDK_BUTTON1_MASK` | Button1 被按下（通常为左键）。 |
| `GDK_BUTTON2_MASK` | Button2 被按下（通常为右键）。 |
| `GDK_BUTTON3_MASK` | Button3 被按下（通常为中键）。 |
| `GDK_BUTTON4_MASK` | Button4 被按下。 |
| `GDK_BUTTON5_MASK` | Button5 被按下。 |

这些事件指示指针已从屏幕的一个位置移动到另一个位置。`time`字段指示服务器时间（自上次服务器重置以来的毫秒数）。如果窗口与`root`在同一个屏幕上，那么`x`和`y`是相对于窗口原点的坐标；否则，它们都将被设置为`0`。`x_root`和`y_root`是相对于`root`窗口的坐标。`pressure`始终设置为`0.5`，而`xtilt`和`ytilt`始终设置为`0`。`Source`始终设置为`GDK_SOURCE_MOUSE`，并且始终设置为`GDK_CORE_POINTER`。如果用于选择事件的掩码是`GDK_POINTER_MOTION_HINT_MASK`，则`is_hint`设置为`1`；否则将为`0`。如果`is_hint`为`1`，则需要通过调用`gdk_window_get_pointer()`获取当前位置信息。`State`用于指定事件发生前鼠标键和修饰键的状态。`state`可能的值通过按位（OR）表 3.5 中的任何位来构造而成。

*注：由于原文文本在 Table 3.5 之后出现了格式混乱和重复，上述翻译基于标准 GDK 文档逻辑进行了对齐和补全。*

```c
struct _GdkEventButton {
    GdkEventType type;
    GdkWindow *window;
    gint send_event;
    guint32 time;
    double x;
    double y;
    double pressure;
    double xtilt;
    double ytilt;
    guint state;
    GdkInputSource source;
    guint32 deviceid;
    double x_root, y_root;
};
```

## 事件名称字符串
`press_event`
`release_event`

## 回调函数原型

```c
gint
func (GtkWidget *widget, GdkEventButton *event, gpointer arg);
```

### 描述
按钮事件指示按钮按下或释放。`time`字段指示服务器时间（自上次服务器重置以来的毫秒数）。如果窗口与`root`在同一个屏幕上（这通常是如此），那么`x`和`y`是相对于窗口原点的坐标；否则，它们都将被设置为`0`。`x_root`和`y_root`是相对于`root`窗口的坐标。`pressure`始终设置为`0.5`，而`xtilt`和`ytilt`始终设置为`0`。`Source`始终设置为`GDK_SOURCE_MOUSE`，并且始终设置为`GDK_CORE_POINTER`。`State`用于指定事件发生前鼠标键和修饰键的状态。`state`可能的值通过按位（OR）表 3.5 中的任何位来构造而成。

```c
struct _GdkEventKey {
    GdkEventType type;       /* GDK_PRESS */
    GdkWindow *window;
    gint send_event;
    guint32 time;
    guint state;
    guint keyval;
    gint length;
    gchar *string;
};
```

## 事件名称字符串
`key_press_event`
`key_release_event`

## 回调函数原型

```c
gint
func (GtkWidget *widget, GdkKey *event, gpointer arg);
```

### 描述
键事件指示键盘按下或释放。`time`字段指示服务器时间（自上次服务器重置以来的毫秒数）。`state`用于指定事件发生前鼠标键和修饰键的状态。`state`可能的值通过按位（OR）表 3.5 中的任何位来构造而成。Keysyms 是代表键的符号值。键盘产生硬件相关的值，Xlib 使用服务器提供的表映射为 keysyms。例如，用户按下标记为 `"A"` 的键产生的硬件代码被转换为 keysym 值 `XK_A`。这个值存储在 `keyval` 中。`String` 包含了 GDK 通过调用 `Xlib LookupString()` 获取的 ASCII 字符。通常，长度为 1 的字符串直接对应于按下或释放的键字形或符号（例如，对于 `XK_A`，字符串将是 `"A"`）。然而，客户端可以使用 `XRebindKeysym()` 任意长度的字符串。该字符串的长度（GDK 限制为 16 个字符）存储在 `length` 中，`string` 包含了 `XLookupString()` 返回的字符串（必要时截断为 16 个字符）。

```c
struct _GdkEventCrossing
{
    GdkEventType type;                /* GDK_ENTER_NOTIFY GDK_LEAVE_NOTIFY */
    GdkWindow *window;
    gint send_event;
    GdkWindow *subwindow;
    guint32 time;
    double x;
    double y;
    double x_root;
    double y_root;
    GdkCrossingMode mode;
    Gdknotify detail;
    gboolean focus;
    guint state;
};
```

## 事件名称字符串
`enter_notify_event`
`leave_notify_event`

## 回调函数原型

```c
gint
func(GtkWidget *widget, GdkEventCrossing *event, gpointer arg);
```

## Description

跨越事件（Crossing events）表示鼠标指针进入或离开了一个窗口。指针进入或离开的窗口由 `window` 指明。如果事件类型为 `CDK_LEAVE_NOTIFY` 且指针起始于 `window` 的子窗口中，则 `subwindow` 将设置为该子窗口的 CDK ID，或者被设置为值 `NULL`。如果事件类型为 `CDK_ENTER_NOTIFY` 且指针最终位于 `window` 的子窗口中，则 `subwindow` 将设置为该子窗口的 CDK ID，或者被设置为值 `NULL`。`time` 表示相对于服务器的事件时间（自服务器事件以来的毫秒）。如果 `window` 与根窗口（root）在同一屏幕上（这通常是如此），则 `x` 和 `y` 指定相对于 `window` 原点的指针坐标；否则，它们都被设置为零。`X_root` 和 `y_root` 是指针相对于根窗口的坐标。如果进入或离开事件是由普通的鼠标移动引起的，或者是由指针跳跃（pointer warp）引起的（即客户端显式地移动了鼠标），则 `mode` 将设置为 `CDK_CROSSING_NORMAL`。或者，如果跨越事件是由指针抓取（pointer grab）引起的，`mode` 将设置为 `CDK_CROSSING_GRAB`。最后，如果跨越事件是由指针选取（pointer undergrad）引起的，则 `mode` 将设置为该值。如果接收窗口是焦点窗口或焦点窗口的后代（`subwindow` 不为 `NULL`），则 `focus` 将设置为 `TRUE`；否则，将设置为 `FALSE`。`state` 指定事件发生前鼠标按钮和修饰键的状态。`state` 的可能值与之前描述的 `GdkEvent` 相同。

最后一个字段描述起来有点复杂。这里将列出可以存储在此字段中的 G 值以及它们映射的 X11 值。在实践中，X11 客户端应用程序（以及 Gtk+ 应用程序）很少甚至从不使用此字段中的数据（参见表 3.6）。

### 表 3.6 跨越事件详细字段

| X11 Value | GDK Value |
|---|---|
| ChangeNotifier | `GDK_NOTIFY_INFERIOR` |
| NotifyAncestor | `GDK_NOTIFY_ANCESTOR` |
| NotifyVirtual | `GDK_NOTIFY_VIRTUAL` |
| NotifyNonlinear | `GDK_NOTIFY_NONLINEAR` |
| NotifyNonlinearVirtual | `GDK_NOTIFY_NONLINEAR_VIRTUAL` |

# GdkEventFocus

```c
struct _GdkEventFocus {
  GdkEventType type;
  GdkWindow *window;
  gint8 send_event;
  gint16 in;
} /* GDK_FOCUS_CHANGE */
```

## 事件名称字符串
`focus_in_event`
`focus_out_event`

## 回调函数原型

```c
gint
func (GtkWidget *widget, GdkFocus *event, gpointer arg);
```

## Description

焦点事件表示键盘焦点从一个窗口切换到另一个窗口。当键盘焦点发生变化时，会发送两个事件。其中一个事件发送给在焦点变化之前拥有键盘焦点的窗口。另一个事件发送给刚刚获得键盘焦点的窗口。如果 X11 事件类型为 `FocusIn`，则由 `window` 标识的窗口接收了焦点，并将设置为 `TRUE`。否则，如果 X11 事件类型为 `FocusOut`，则由 `window` 标识的窗口失去了焦点，并将设置为 `FALSE`。

## GdkEventConfigure

```c
struct _GdkEventConfigure
{
    GdkEventType type;                /* GDK_CONFIGURE */
    GdkWindow window;
    gint8 send_event;
    gint6 x, y;
    gint6 width;
    gint6 height;
};
```

## 事件名称
`configure_event`

## 回调函数原型

```c
gint
func (GtkWidget *widget, GdkEventConfigure *event, gpointer arg);
```

## Description

配置事件（Configure events）表示窗口大小和/或位置的变化。`window` 字段标识被移动或调整大小的窗口。`x` 和 `y` 字段标识窗口在根窗口坐标空间中的新 x 和 y 位置。`width` 和 `height` 标识窗口宽的高度。

## GdkEventProperty

```c
struct _GdkEventProperty
{
    GdkEventType type;                /* GDK_PROPERTY_NOTIFY */
    GdkWindow *window;
    int8 send_event;
    GdkAtom atom;
    guint32 time;
    guint32 state;
};
```

## 事件名称字符串
`property_notify_event`

## 回调函数原型

```c
gint
func (GtkWidget *widget, GdkEvent *event, gpointer arg);
```

## Description

属性（Properties）表示属性的变化。属性是与窗口关联的命名数据。这些数据存储在你的 Gtk+ 客户端连接的 X 服务器上。属性具有唯一的 ID，该 ID 是预定义的或动态生成的。属性表示属性的变化。属性是与窗口关联的命名数据。这些数据存储在你的 Gtk+ 客户端连接的 X 服务器上。属性具有唯一的 ID，该 ID 是预定义的或动态生成的。属性（属性属性。属性是。属性是与窗口关联的命名数据。这些数据存储在你的 Gtk+ 客户端连接的 X

上。

```c
struct _GdkEventSelection {
  GdkEventType type;
  GdkWindow *window;
  int8 send_event;
  GdkAtom atom;
  guint32 time;
  guint32 state;
};/* GDK_SELECTION_CLEAR GDK_SELECTION_REQUEST GDK_SELECTION_NOTIFY */
```

# 第3章 信号、事件、对象和类型

## 事件名称
`selection_clear_event`
`selection_request_event`
`selection_notify_event`

## 回调函数原型

```c
gint
func (GtkWidget *widget, GdkEvent *event, gpointer arg);
```

选择（Selections）是所有 X 客户端（包括使用 Gtk+ 的客户端）的一种重要的进程间通信方式。选择提供了客户端之间执行复制和粘贴的操作。这种操作的经典示例是在 xterm 中高亮文本并进行粘贴。高亮文本的 xterm 是所有者（owner client），而进行粘贴的 xterm 是请求者（requester client）。所有者拥有当前选中的数据，而请求者想要这些数据。允许请求者意识到数据可用，并提供所有者将数据转换为请求者所需格式的机制。

选择协议。基本上来说，所有者和请求者之间的协议如下。在示例中，我们假设正在两个不同的文本编辑（entry）控件之间执行复制和粘贴。我们将客户端 1 中的文本编辑控件称为 `entry-1`，将客户端 2 中的文本编辑控件称为 `entry-2`。

当用户在 `entry-1` 中选择文本时（此处我们忽略具体实现），客户端 1 将调用 `gtk_selection_owner_set()` 来获取命名为 `GDK_SELECTION_PRIMARY` (`XA_PRIMARY`) 选择的所有权。如果成功且客户端 1 尚未拥有该选择，则会发送 `SelectionClear` (`GDK_SELECTION_CLEAR`) 事件。接收到 SelectionClear 事件的客户端将响应并取消高亮。注意，到为止我们所做的只是在客户端之间切换所有权。

现在假设客户端 2 中的文本编辑控件（`entry-2`）获得了焦点，用户以特定的应用程序方式发起了操作。客户端 2 承担请求者的角色，并调用 `gtk_selection_convert()` 获取数据。`gtk_selection_convert()` 将调用 `gdk_selection_convert()`，后者将调用 `XSelection()`。`XSelection()` 被传递了一个窗口 ID、`GDK_SELECTION_PRIMARY` 原子和一个目标原子（target）。目标原子用于指示请求者希望将选定数据转换成的类型，或者如果可能，所有者在将选定数据传输到 X 服务器之前进行转换。一组基础目标原子是由 X11 的《客户端间通信规范》（ICCM）预定义的。表 3.7 阐明了 X11 中一些预定义的目标原子。

## 表 3.7 X11 中的预定义目标原子

| 原子 (Atom) | X11 数据类型 (Data Type) |
| --- | --- |
| `X_ARC` | `XArc` |
| `X_POINT` | `XPoint` |
| `X_ATOM` | `Atom` |
| `X_RGB_COLOR_MAP` | `Atom` (标准调色板) |
