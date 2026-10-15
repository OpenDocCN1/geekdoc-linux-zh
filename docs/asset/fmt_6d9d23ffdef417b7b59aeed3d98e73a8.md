
`event` 成员被设置为重新配置的窗口或其父窗口，取决于选择了 `StructureNotify` 还是 `SubstructureNotify`。`window` 成员被设置为尺寸、位置、边框和堆叠顺序发生更改的窗口。

`x` 和 `y` 成员设置为相对于父窗口起点的坐标，指示窗口外部左上角的位置。`width` 和 `height` 成员设置为窗口内部尺寸，不包括边框。`border_width` 成员设置为窗口边框的宽度（像素为单位）。

`above` 成员设置为兄弟窗口，用于堆叠操作。如果 X 服务器将其设置为 `None`，则状态更改的窗口位于堆栈底部。然而，如果将其设置为某个兄弟窗口，则状态更改的窗口将置于该兄弟窗口之上。

`override_redirect` 成员设置为窗口的覆盖重定向（override redirect）属性。如果该成员为 `True`，窗口管理器将忽略此。

## CreateNotify 事件

X 服务器可以向想要窗口创建信息的客户端报告 CreateNotify 事件。每当客户端应用程序通过 `CreateWindow` 或 `XCreateSimpleWindow` 创建窗口时，X 服务器生成此事件。

要接收 CreateNotify 事件，需要在窗口的 `eventmask` 属性中设置 `SubstructureNotifyMask` 位。此时，创建任何子窗口都会生成事件。

此类型的事件结构包含：

```c
typedef struct {
    int             type;
    unsigned long serial;
    Bool            send_event;
    Display         *display;
    Window          parent;
    Window          window;
    int             x, y;
    int             width, height;
    int             border_width;
    Bool            override_redirect;
} XCreateWindowEvent; /* CreateNotify */
/* 服务器处理的最后一个请求数 */
/* 如果来自 SendEvent 请求则为 true */
/* 读取事件的显示器 */
/* 窗口的父窗口 */
/* 创建的窗口 ID */
/* 窗口位置 */
/* 窗口尺寸 */
/* 边框宽度 */
/* 创建将被重定向 */
```

`parent` 成员设置为父窗口。`window` 成员指定创建的窗口。`x` 和 `y` 成员设置为创建窗口相对于父窗口起点的坐标以及窗口外部左上角的位置。`width` 和 `height` 成员设置为窗口的内部尺寸（不包括边框）。`border_width` 成员设置为创建窗口边框的宽度（像素为单位）。`override_redirect` 成员设置为窗口的覆盖重定向属性。如果该成员为 `True`，窗口管理器将忽略此。

## DestroyNotify 事件

X 服务器可以向想要获取窗口销毁信息的客户端报告 DestroyNotify 事件。每当客户端应用程序通过 `XDestroyWindow` 或 `XDestroySubwindows` 销毁窗口时，X 服务器生成此事件。

DestroyNotify 事件的顺序是：对于任何窗口，在窗口本身生成事件之前，会先在其内部生成事件。X 协议并不限制兄弟窗口之间以及跨子层次的顺序。

要接收 DestroyNotify 事件，需要在窗口的 `eventmask` 属性中设置 `StructureNotifyMask` 位，或者在父窗口的 `eventmask` 属性中设置 `StructureNotifyMask`（在这种情况下，销毁子窗口会生成事件）。

此类型的事件结构包含：

```c
typedef struct {
    int             type;
    unsigned long serial;
    Bool            send_event;
    /* DestroyNotify */
    /* 服务器处理的最后一个请求数 */
    /* 如果来自 SendEvent 请求则为 true */
```

# 事件 (Events)

```c
typedef struct {
    Display *display;      /* 读取事件的显示器 */
    Window event;
    Window window;
} XdestroyWindowEvent;
```

`event` 成员被设置为被销毁的窗口或其父窗口，取决于选择了 `StructureNotify` 还是 `SubstructureNotify`。`window` 成员设置为被销毁的窗口。

# 重力通知事件 (GravityNotifyEvents)

当窗口因父窗口大小改变而移动时，X 服务器可以向需要的客户端报告 GravityNotify 事件。当客户端应用程序通过 `XConfigureWindow`、`XMoveResizeWindow` 或 `XResizeWindow` 调整父窗口大小导致子窗口移动时，X 服务器就会生成此事件。

接收 GravityNotify 事件

该事件类型的结构：

```c
typedef struct {
    int type;                  /* GravityNotify */
    unsigned long serial;      /* 服务器处理的最后一个请求数 */
    Bool send_event;           /* 如果此事件来自 SendEvent 请求则为 true */
    Display *display;          /* 读取事件的显示器 */
    Window event;
    Window window;
    int x, y;
} XGravityNotifyEvent;
```

`event` 成员被设置为移动的窗口或其父窗口，取决于选择了 `StructureNotify` 还是 `SubstructureNotify`。`window` 成员设置为被移动的子窗口。`x` 和 `y` 成员设置为相对于新父窗口原点的坐标，表示窗口左上角外边缘的位置。

# 映射通知事件 (MapNotifyEvents)

X 服务器可以向想要获取窗口映射（mapped）信息的客户端报告 MapNotify 事件。当客户端应用程序通过调用 `XMapWindow`、`XMapRaised`、`XMapSubwindows`、`XReparentWindow` 或由于 setprocessing 的结果将窗口状态从未映射改为映射时，X 服务器就会生成此事件。

要接收 MapNotify 事件，请在窗口的 `eventmask` 属性中设置 `StructureNotifyMask` 位，或者在父窗口的 `eventmask` 属性中设置 `SubstructureNotifyMask` 位（在这种情况下，映射任何子窗口都会生成一个事件）。

该事件类型的结构包含：

```c
typedef struct {
    int type;                /* MapNotify */
    unsigned long serial;   /* 服务器处理的最后一个请求数 */
    Bool send_event;         /* 如果此事件来自 SendEvent 请求则为 true */
    Display *display;         /* 读取事件的显示器 */
    Window window;           /* boolean, is override set... */
    Window override_redirect;
} XMapEvent;
```
