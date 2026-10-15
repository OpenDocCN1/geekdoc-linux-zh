
`window` 成员设置为可见性状态发生变化的窗口。`state` 成员设置为窗口的可见性状态，可以是 `VisibilityUnobscured`（未遮挡）、`VisibilityPartiallyObscured`（部分遮挡）、`VisibilityFullyObscured`（完全遮挡）。X 服务器在确定窗口的可见性状态时会忽略窗口的所有子窗口，并按照以下方式处理 `VisibilityNotify` 事件：

- 当窗口状态从部分遮挡、完全遮挡或不可变为变为可见且完全未遮挡时，X 服务器生成事件，并将 `XVisibilityEvent` 结构体中的 `state` 成员设置为 `VisibilityUnobscured`。
- 当窗口状态从可见且完全未遮挡或不可变为变为可见且部分遮挡时，X 服务器生成事件，并将 `XVisibilityEvent` 结构体中的 `state` 成员设置为 `VisibilityPartiallyObscured`。
- 当窗口状态从可见且完全未遮挡、可见且部分遮挡或不可变为可见且完全遮挡时，X 服务器生成事件，并将 `state` 成员设置为 `VisibilityFullyObscured`。

## 结构控制事件 (Structure Control Events)

本节讨论了：

- `CirculateRequest` 事件
- `ConfigureRequest` 事件
- `MapRequest` 事件
- `ResizeRequest` 事件

### CirculateRequest 事件

X 服务器可以向想要获取另一个客户端何时对指定窗口发起循环窗口（circulate window）请求的客户端报告 `CirculateRequest` 事件。每当客户端对窗口发起循环窗口请求且实际上有子窗口需要重叠时，X 服务器就会生成此类型的事件。客户端通过调用 `XCirculateSubwindows`、`XCirculateSubwindowsUp` 或 `XCirculateSubwindowsDown` 对窗口发起循环窗口请求。

要处理 `ConfigureRequest` 事件，请在窗口的 `event-mask` 属性中设置 `SubstructureRedirectMask`。此时，针对指定窗口的窗口请求将不会执行，因此任何子窗口在堆栈中的位置都不会发生改变。例如，假设客户端调用 `XCirculateSubwindowsUp` 将一个子窗口提升到堆栈顶端。如果你在窗口上选择了 `SubstructureRedirectMask`，X 服务器将向你报告一个 `CirculateRequest` 事件，而不会将该子窗口提升到堆栈顶端。

此类型的事件结构包含：

```c
typedef struct {
    int type; /* XCirculateRequest */
    unsigned long serial; /* # of last request processed by server */
    Bool send_event; /* true if this came from a SendEvent request */
    Window *display; /* Display the event was read from */
    Window *parent;
    Window *window;
    int place; /* PlaceOnTop, PlaceOnBottom */
} XCirculateRequest;
```

`parent` 成员设置为父窗口。`window` 成员设置为要重新映射的子窗口。`place` 成员设置为新堆叠顺序应处的位置，可以是 `PlaceOnTop`（置于顶层）或 `PlaceOnBottom`（置于底部）。如果是 `PlaceOnTop`，则子窗口应位于所有兄弟窗口之上；如果是 `PlaceOnBottom`，则子窗口将位于所有兄弟窗口之下。

### ConfigureRequest 事件

服务器可以向想要获取另一个客户端何时发起窗口请求的客户端报告 `ConfigureRequest` 事件。窗口请求尝试重新配置窗口的大小、位置、边框和堆叠顺序。每当另一个客户端通过调用 `XConfigureWindow`、`XLowerWindow`、`XRaiseWindow`、`XMapRaised`、`XMoveResizeWindow`、`XMoveWindow`、`XResizeWindow` 或 `XWindowBorderWidth` 发起窗口请求时，X 服务器就会生成事件。

要处理 `ConfigureRequest` 事件，请在窗口的 `event-mask` 属性中设置 `SubstructureRedirectMask`。当另一个客户端向子窗口发出 `ConfigureWindow` 协议请求时，会生成 `ConfigureRequest` 事件。例如，假设应用程序调用 `XLowerWindow` 来降低一个窗口。如果你在父窗口上选择了 `SubstructureRedirectMask`，且窗口的 `override-redirect` 属性设置为 `False`，则 X 服务器将向你报告 `ConfigureRequest` 事件，而不会降低指定的窗口。

此类型的事件结构包含：

```c
typedef struct {
    int             type;           /* ConfigureRequest */
    unsigned long serial;      /* # of last request processed by server */
    Bool            send_event;     /* true if this came from a SendEvent request */
    Display         *display;       /* Display the event was read from */
    Window          parent;
    Window          window;
    int             x, y;
    int             width, height;
    int             border_width;
    Window          above;
    detail;         /* Above, Below, TopIf, BottomIf, Opposite */
    unsigned long value_mask;
} XConfigureEvent;
```

`parent` 成员设置为父窗口。`window` 成员设置为要重新配置大小、位置、边框和/或堆叠顺序的窗口。`value_mask` 表示在 `ConfigureWindow` 协议请求中指定了哪些组件。相应的值将在请求中报告。其余值将用窗口当前的几何形状填充，但 `above`（兄弟窗口）和 `detail`（堆叠模式）除外，如果请求中未给出，它们分别被报告为 `Note` 和 `Above`。

### MapRequest 事件

X 服务器可以向想要获取另一个客户端映射（map）意图的客户端报告 `MapRequest` 事件。当窗口的映射完成时，该窗口被映射。每当另一个客户端对一个 `override-redirect` 为 `False` 的未映射窗口发起映射请求时，X 服务器就会生成此事件。

要接收映射事件，请在窗口的 `event-mask` 属性中设置 `SubstructureRedirectMask`。例如，假设应用程序调用 `XLowerWindow` 来映射窗口。如果你在父窗口上选择了 `SubstructureRedirectMask`，且窗口的 `override-redirect` 属性设置为 `False`，则 X 服务器将向你报告 `MapRequest` 事件，而不会映射指定的窗口。因此，此事件赋予了窗口管理器客户端控制子窗口位置的能力。

此事件的结构包含：

```c
typedef struct {
    int type;        /* MapRequest */
    unsigned long serial; /* # of last request processed by server */
    Bool send_event;    /* true if this came from a SendEvent request */
    Display display;      /* Display the event was read from */
    Window parent;
    Window window;
} XMapRequestEvent;
```
