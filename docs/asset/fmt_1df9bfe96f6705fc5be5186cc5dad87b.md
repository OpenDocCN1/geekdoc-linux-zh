
参数 `events` 是一个位码，用于指示客户端希望从 Gtk+ 接收的事件类型，而 `widget` 是与事件通知相关的 Gtk 小组件句柄。X 服务器将只发送 `events` 掩码中指定的、属于 `widget` 所定义窗口的事件。这意味着没有创建窗口的小组件无法接收事件（我们将在本书的后部分回到此问题）。未请求窗口请求的事件不会由 X 服务器传输给客户端。

除非你计划在应用程序中处理特定事件，否则真的没有需要调用此例行函数。这并不意味着不会为小组件请求事件；小组件实现很可能会请求一个或多个事件。

事件位码可以通过按位或（OR'ing）组合由 GDK 定义的一个或多个常量（参见表 3.2）来构建。

### 表 3.2 GDK 事件掩码

| 掩码 | 请求的事件 |
| --- | --- |
| `GDK_EXPOSURE_MASK` | expose 事件（但不包括 GraphicsEx 或 NoExpose） |
| `GDK_POINTER_MOTION_MASK` | 较少的光标移动事件 |
| `GDK_POINTER_MOTION_HINT_MASK` | 所有的光标移动事件 |
| `GDK_BUTTON_MOTION_MASK` | 鼠标按钮按下时的光标移动 |
| `GDK_BUTTON1_MOTION_MASK` | 鼠标按钮按下时的光标移动 |
| `GDK_BUTTON2_MOTION_MASK` | 按下鼠标按钮 2 时的光标移动 |
| `GDK_BUTTON3_MOTION_MASK` | 按下鼠标按钮 3 时的光标移动 |
| `GDK_BUTTON_PRESS_MASK` | 光标按钮按下事件 |
| `GDK_BUTTON_RELEASE_MASK` | 光标按钮释放事件 |
| `GDK_KEY_PRESS_MASK` | 键按下事件 |
| `GDK_KEY_RELEASE_MASK` | 键释放事件 |
| `GDK_ENTER_NOTIFY_MASK` | 光标进入窗口的事件 |
| `GDK_LEAVE_NOTIFY_MASK` | 光标离开窗口的事件 |
| `GDK_FOCUS_CHANGE_MASK` | 焦点的任何变化 |
| `GDK_STRUCTURE_MASK` | 窗口的任何变化 |
| `GDK_PROPERTY_CHANGE_MASK` | 属性的任何变化 |
| `GDK_VISIBILITY_NOTIFY_MASK` | 可见性的任何变化 |
| `GDK_PROXIMITY_IN_MASK` | 用于 X Input 程序 |
| `GDK_PROXIMITY_OUT_MASK` | 用于 X Input 程序 |
| `GDK_SUBSTRUCTURE_MASK` | 关于子元素的通知 |
| `GDK_ALL_EVENTS_MASK` | 以上所有内容 |

## 第 3 章 信号、事件与类型

前表中的掩码与表 3.1 中列出的事件并非一一对应关系。某些掩码会导致接收到多个事件，取决于应用程序，你的回调函数可能需要检查接收到了哪种事件。表 3.3 应该阐明掩码与事件之间的映射关系。

### 表 3.3 事件掩码到事件的映射

| 掩码 | 请求的事件 |
| --- | --- |
| `GDK_EXPOSURE_MASK` | expose |
| `GDK_POINTER_MOTION_MASK` | motion_notify |
| `GDK_POINTER_MOTION_HINT_MASK` | motion_notify |
| `GDK_BUTTON_MOTION_MASK` | motion_notify |
| `GDK_BUTTON1_MOTION_MASK` | motion_notify |
| `GDK_BUTTON2_MOTION_MASK` | motion_notify |
| `GDK_BUTTON3_MOTION_MASK` | motion_notify |
| `GDK_BUTTON_PRESS_MASK` | button_press |
| `GDK_BUTTON_RELEASE_MASK` | button_release |
| `GDK_KEY_PRESS_MASK` | key_press |
| `GDK_KEY_RELEASE_MASK` | key_release |
| `GDK_ENTER_NOTIFY_MASK` | enter_notify |
| `GDK_LEAVE_NOTIFY_MASK` | leave_notify |
| `GDK_FOCUS_CHANGE_MASK` | focus_change |
| `GDK_STRUCTURE_MASK` | structure_notify |
| `GDK_PROPERTY_CHANGE_MASK` | property_notify |
| `GDK_VISIBILITY_NOTIFY_MASK` | visibility_notify |
| `GDK_PROXIMITY_IN_MASK` | proximity_in |
| `GDK_PROXIMITY_OUT_MASK` | proximity_out |
| `GDK_SUBSTRUCTURE_MASK` | substructure_notify |
| `GDK_ALL_EVENTS_MASK` | 以上所有 |

除非你计划在应用程序中处理特定事件，否则真的没有需要调用此例行函数。这并不意味着不会为小组件请求事件；小组件实现很可能会请求一个或多个事件。

事件位码可以通过按位或（OR'ing）组合由 GDK 定义的一个或多个常量（参见表 3.2）来构建。

在前面的例程中，如果事件指针为 NULL 或者事件类型不是 `GDK_LEAVE_NOTIFY`，我们将跳过信号函数。

### GdkEventExpose

```
struct _GdkEventExpose {

    GdkEventType type;      /* GDK_EXPOSE */

    GdkWindow *window;

    gint send_event;

    GdkRectangle area;

    int count;              /* 如果非零，则后续有多少个事件 */

};
```

#### 事件名称字符串

`expose_event`

#### 回调函数原型

```
gint

func (GtkWidget *widget, GdkEventExpose *event, gpointer arg);
```

#### 描述

Expose（暴露）事件通过被设置为 `GDK_EXPOSE` 的类型来标识。`window` 标识了需要重绘的窗口，`area` 定义了该事件描述的区域。如果窗口中有一个超过一个区域被暴露，X 服务器将发送多个 expose 事件。等待该窗口的事件数量由 `count` 标识。如果你的代码忽略了 `area` 字段并在 expose 信号函数中重绘整个窗口，那么你的代码应该等待直到接收到一个 `count` 字段等于零的 expose 事件。

### GdkEventNoExpose

```
struct _GdkEventNoExpose {

    GdkEventType type;      /* GDK_NO_EXPOSE */

    GdkWindow *window;

    gint send_event;

};
```

#### 事件名称字符串

`no_expose_event`

#### 回调函数原型

```
gint

func (GtkWidget *widget, GdkEventAny *event, gpointer arg);
```

#### 描述

如果成功执行 CopyArea 或 CopyPlane X 协议，则会接收到 NoExpose 事件。只有当源图像中的所有值都能被 X 服务器复制，且源窗口没有部分被遮挡，并且在 CopyArea 或 CopyPlane 请求中使用的 GC 的 graphics_exposures 标志被设置为 True 时，才会发生这种情况。`XCopyArea` 是由 `gdk_draw_pixmap()` 和 `gdk_window_copy_area()` 调用的。

### GdkEventVisibility

```
struct _GdkEventVisibility {

    GdkEventType type;

    GdkWindow *window;

    gint send_event;

    GdkVisibilityState state;

}; /* GDK_VISIBILITY_NOTIFY */
```

#### 事件名称字符串

`visibility_notify_event`

#### 回调函数原型

```
gint

func(GtkWidget *widget, GdkEventVisibility *event, gpointer arg);
```
