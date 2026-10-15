
`event`成员被设置为被映射的窗口或其父窗口，取决于选择了`StructureNotify`还是`SubstructureNotify`。`window`成员设置为被映射的窗口。`override_redirect`成员设置为窗口的`override-redirect`属性。如果`override-redirect`属性为 True，窗口管理器客户端通常会忽略此事件，因为这些事件通常是由弹出窗口生成的，而弹出窗口会覆盖结构控制。

# 映射通知事件 (MappingNotify Events)

X 服务器向所有客户端报告`MappingNotify`事件。没有机制可以表示对此类事件不感兴趣。当客户端应用程序成功执行以下操作时，X 服务器会生成此类型的事件：

- `XSetModifierMapping`：指示 KeyCodes 将作为修饰键使用
- `XChangeKeyboardMapping`：更改键盘映射
- `XSetPointerMapping`：设置指针映射

该事件类型的结构包含：

```c
typedef struct {
    int type;                /* MappingNotify */
    unsigned long serial;   /* 服务器处理的最后一个请求数 */
    Bool send_event;         /* 如果此事件来自 SendEvent 请求则为 true */
    Display *display;         /* 读取事件的显示器 */
    Window window;           /* 未用 */
    int request;             /* MappingModifier, MappingKeyboard, MappingPointer 之一 */
} XMappingEvent;
```

```c
typedef struct {
    int first_keycode; /* 第一个keycode */
    int count;       /* 定义从 first_keycode 开始的更改范围 */
} XMappingEvent;
```

`request`成员用于指示发生的映射类型，可以是`MappingModifier`、`MappingKeyboard`或`MappingPointer`。如果是`MappingKeyboard`或`MappingModifier`，则修饰键映射已更改。如果是`MappingPointer`，则指针按钮成员被设置为`MappingKeyboard`。如果是`MappingKeyboard`，则键盘映射已更改。`first_keycode`和`count`成员仅在`request`成员被设置为`MappingKeyboard`时被设置。`first_keycode`中的数字代表所更改映射范围中的第一个数字，`count`代表被更改的 keycode 数量。

为了更新客户端对键盘的认知，您应该调用`XRefreshKeyboardMapping`。

# 重父通知事件 (ReparentNotifyEvents)

X 服务器向想要获取窗口变化的客户端报告`ReparentNotify`事件。当客户端应用程序调用`XReparentWindow`且窗口实际上发生了重父时，X 服务器就会生成此事件。

要接收`ReparentNotify`事件，请在窗口的`eventmask`属性中设置`StructureNotifyMask`位，或者在旧窗口或新窗口的`SubstructureNotifyMask`属性（在这种情况下，重父任何子窗口都会生成一个事件）。

该事件类型的结构包含：

```c
typedef struct {
    int      type;           /* ReparentNotify */
    unsigned long serial; /* 服务器处理的最后一个请求数 */
    Bool     send_event;     /* 如果此事件来自 SendEvent 请求则为 true */
    Display  *display;       /* 读取事件的显示器 */
    Window   event;
    Window   window;
    Window   parent;
    int      x, y;
    int override_redirect;
} XReparentEvent;
```

`event`成员指示是旧窗口还是新窗口，取决于选择了`StructureNotify`还是`SubstructureNotify`。`window`成员设置为重父的窗口。`parent`成员设置为新窗口。`x`和`y`成员设置为相对于新父窗口原点的坐标，表示重父窗口左上角外边缘的位置。`override_redirect`成员设置为窗口的`override-redirect`属性。如果`override-redirect`属性为 True，窗口管理器客户端通常会忽略此。

# 取消映射事件 (Unmap Events)

X 服务器可以向想要窗口映射信息的客户端报告`UnmapNotify`事件。当客户端应用程序将状态从映射改为未映射时，X 服务器生成此类型的事件。

要接收`UnmapNotify`事件，请在窗口的`eventmask`属性中设置`StructureNotifyMask`，或在父窗口的`eventmask`中设置`SubstructureNotifyMask`（在这种情况下，取消映射任何子窗口都会生成事件）。

该事件类型的结构包含：

```c
typedef struct {
    int type;               /* UnmapNotify */
    unsigned long serial;   /* 服务器处理的最后一个请求数 */
    Bool send_event;         /* 如果此事件来自 SendEvent 请求则为 true */
    Display *display;         /* 读取事件的显示器 */
    Window event;
    Window window;
    Bool from_configure;
} XUnNotify;
```

`event`成员被设置为取消映射的窗口或其父窗口，取决于选择了`StructureNotify`还是`SubstructureNotify`。`window`成员设置为被取消映射的窗口。如果事件是因为父窗口大小调整且窗口自身重力为`UnmapGravity`时产生的，则`from_configure`成员被设置为 True。

# 可见性事件 (Visibility Events)

X 服务器向想要获取指定窗口任何变化的客户端报告`VisibilityNotify`事件。如果有人看屏幕可以看到窗口的区域，则该区域是可见的。当可见性改变时，X 服务器就会生成此事件。然而，此事件仅对类为`InputOnly`的窗口生成。

由层次结构变化引起的所有`VisibilityNotify`事件都在每次对应的层次结构事件（`UnmapNotify`、`MapNotify`、`ConfigureNotify`、`GravityNotify`、`ConfigureNotify`）之后生成。窗口上的任何`VisibilityNotify`事件都在窗口的`Exposure`事件之前生成，但并不要求所有窗口的`VisibilityNotify`事件都可以在所有窗口的`Exposure`事件之前生成。X 协议没有限制`VisibilityNotify`事件相对于`FocusOut`、`EnterNotify`和`LeaveNotify`事件的顺序。

要接收`VisibilityNotify`事件，请在窗口的 event-mask 属性中设置`VisibilityChangeMask`。

```c
typedef struct {
    int type;               /* VisibilityNotify */
    unsigned long serial;  /* # of last request processed by server */
    Bool send_event;       /* true if this came from a SendEvent request */
    Display *display;        /* Display the event was read from */
    Window window;
} XVisibilityEvent;
```
