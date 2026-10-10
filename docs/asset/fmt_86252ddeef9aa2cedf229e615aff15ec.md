
## 事件名称字符串

`no_expose_event`

## 回调函数原型

```c
gint
func (GtkWidget *widget, GdkEventAny *event, gpointer arg);
```

## 描述

如果成功执行 `CopyArea` 或 `CopyPlane` X 协议，则会接收到 `NoExpose` 事件。只有当源图像中的所有值都能被 X 服务器复制，且源窗口没有部分被遮挡，并且在 `CopyArea` 或 `CopyPlane` 请求中使用的 GC 的 `graphics_exposures` 标志被设置为 `True` 时，才会发生这种情况。`XCopyArea` 是由 `gdk_draw_pixmap()` 和 `gdk_window_copy_area()` 调用的。

## GdkEventVisibility

```c
struct _GdkEventVisibility {
    GdkEventType type;
    GdkWindow *window;
    gint send_event;
    GdkVisibilityState state;
}; /* GDK_VISIBILITY_NOTIFY */
```

## 事件名称字符串

`visibility_notify_event`

## 回调函数原型

```c
gint
func(GtkWidget *widget, GdkEventVisibility *event, gpointer arg);
```

## 描述

当窗口的可见性发生变化时会设置可见事件。事件的 `state` 字段描述了变化的性质，可以是表 3.4 中的值之一。

## 表 3.4 可见事件状态

| 值 | 含义 |
| --- | --- |
| `GDK_VISIBILITY_UNOBSCURED` | 窗口之前部分遮挡、完全遮挡或不可见，现在变为可见且完全遮挡。 |
| `GDK_VISIBILITY_PARTIAL` | 窗口之前可见且完全未遮挡，或不可见，现在变为可见且部分遮挡。 |
| `GDK_VISIBILITY_FULLY_OBSCURED` | 窗口之前可见且完全未遮挡，或可见且部分未遮挡，或不可见，现在变为可见且完全遮挡。 |

## GdkEventMotion

```c
struct _GdkEventMotion {
    GdkEventType type;
    GdkWindow *window;
    gint send_event;
}; /* GDK_MOTION_NOTIFY */
guint32 time;
gdouble x;
gdouble y;
gdouble pressure;
gdouble xtilt;
gdouble ytilt;
guint state;
gint16 is_hint;
GdkInputSource source;
guint32 deviceid;
gdouble x_root, y_root;
};
```

## 事件名称字符串

`motion_notify_event`

## 回调函数原型

```c
gint func (GtkWidget *widget, GdkMotion *event, gpointer arg);
```

## 描述

`Motion notify`（移动通知）事件表示指针已从屏幕的一个位置移动到另一个位置。`time` 字段表示事件在服务器速率时间中的时间（自上次服务器重置以来的毫秒）。如果窗口与根窗口在同一个屏幕上（通常情况下如此），那么 `x` 和 `y` 是相对于窗口原点的坐标；否则，它们都被设置为 0。`x_root` 和 `y_root` 是相对于根窗口的坐标。`pressure` 始终设置为值 0.5，`xtilt` 和 `ytilt` 始终设置为值 0。`source` 始终设置为 `GDK_SOURCE_MOUSE`，`deviceid` 始终设置为值 `GDK_CORE_POINTER`。如果用于选择事件的掩码 `GDK_POINTER_MOTION_HINT_MASK` 被使用，则 `is_hint` 设置为 1，否则为 0。调用 `pointer()` 时，`state` 指定事件发生前鼠标键和修饰键的状态。`state` 的可能值通过对以下任何项进行按位或构造

## 表 3.5 移动事件状态

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键按下。 |
| `GDK_LOCK_MASK` | lock 键按下。 |
| `GDK_CONTROL_MASK` | control 键按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

## 表 3.5 移动事件状态（续）

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

*(注：由于原文文本中存在大量重复的表格内容和逻辑混乱，此处遵循“不漏掉任何行”原则进行翻译，但实际文档工程中应检查源错误。)*

## Description

交叉事件（Crossing events）表示鼠标指针进入或离开了一个窗口。指针进入的窗口或离开的窗口由 `window` 指明。如果事件类型为 `GDPR_LEAVE_NOTIFY` 且指针起始于 `window` 的子窗口，则 `subwindow` 将设置为该子窗口的 GDPR ID，或者设置为 `NULL`。如果事件类型为 `GDPR_ENTER_NOTIFY` 且指针最终位于 `window` 的子窗口中，则 `subwindow` 将设置为该子窗口的 GDPR ID，或者设置为 `NULL`。`time` 表示事件相对于服务器时间的时间（自服务器重置以来的毫秒数）。如果 `window` 与根窗口（root）在同一块屏幕上（通常情况下如此），则 `x` 和 `y` 指定相对于窗口原点的指针坐标；否则，它们都被置为零。`X_root` 和 `y_root` 是指针相对于根窗口的坐标。如果进入或离开事件是由正常的鼠标移动引起的，或者由指针跳变（pointer warp，即客户端显式地移动了鼠标）引起的，则 `mode` 将设置为 `GDPR_CROSSING_NORMAL`。或者，如果交叉事件是由指针捕取（pointer grab）引起的，`mode` 将设置为 `GDPR_GRAB`。最后，如果交叉事件是由指针取消捕取（pointer ungrab）引起的，则 `mode` 将设置为 `GDPR_CROSSING_UNGRAB`。如果接收窗口是焦点窗口或焦点窗口的后代（`subwindow` 不为 `NULL`），则 `focus` 将设置为 `TRUE`；否则设置为 `FALSE`。`state` 指定了事件发生前鼠标按钮和修饰键的状态。`state` 的可能值与之前描述的 `GdkEvent` 相同。

最后一个字段的描述稍微有点复杂。这里将简单列出可以存储在此字段中的 GDPR 值以及它们映射到的 X11 值。在实践中，X11 客户端应用程序（以及扩展的 Gtk+ 应用程序）很少甚至从不会使用此字段中的数据（参见表 3.6）。

## 表 3.6 交叉事件事件详情字段

| X11 值 | GDPR Value |
| :--- | :--- |
| NotifyFocus | GDPR_NOTIFY_INFERIOR |
| NotifyAncestor | GDPR_NOTIFY_ANCESTOR |
| NotifyVirtual | GDPR_NOTIFY_VIRTUAL |
| NotifyNonlinear | GDPR_NOTIFY_NONLINEAR |
| NotifyNonlinearVirtual | GDPR_NOTIFY_NONLINEAR_VIRTUAL |

## GdkEventFocus

```c
struct _GdkEventFocus {
    GdkEventType type;
    GdkWindow *window;
    gint8 send_event;
    int16 in;
}; /* GDPR_FOCUS_CHANGE */
```

## 事件名称字符串

`focus_in_event`
`focus_out_event`

## 回调函数原型

```c
gint
func (GtkWidget *widget, GdkFocus *event, gpointer arg);
```
