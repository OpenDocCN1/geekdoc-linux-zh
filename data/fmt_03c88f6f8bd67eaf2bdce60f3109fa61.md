
所有组件都会接收此事件（因为 `GTK_STRUCTURE_MASK` 自动在事件掩码中），但大多数组件会在响应大小分配时自行调整它们的 `GdkWindow`。配置事件只是报告了大小调整，这并不非常有用。有两个值得注意的例外。第一，顶层的 `GtkWindow` 组件负责启动大小分配过程，而不是从其他地方获取。它监控配置事件以确定其大小分配。当你使用窗口管理器调整 `GtkWindow` own运行时，它将接收配置事件并采取行动。第二个例外是 `Gtkdrawingarea`。当 `Gtkdrawingarea` 的大小分配改变时，它会发送配置事件。这就是为什么你通常希望在调整大小时重绘绘图的内容。对于所有由 GTK+ 创建的“伪造”事件，此配置事件的大小将为 `TRUE`。

`GdkWindow` 的其他变化由 `GdkEventAny` 信号；这些事件不包含特殊信息，它们只是告诉你发生了某些事情。它们通过 `type` 字段进行区分：

- `GTK_DELETE` 表示窗口管理器已请求应用程序销毁此窗口。如果组件接收到与此事件对应的信号，该信号的发射将由 GTK+ 主循环自动销毁。因为默认返回值为 `FALSE`，你必须连接一个返回 `TRUE` 的信号处理器，以防止用户销毁 `GdkWindow` 组件。
- `GDK_DESTROY` 表示窗口已销毁。组件通常在未实现（unrealized）时销毁自己的窗口。如果组件在窗口销毁事件后未被销毁，GTK+ 主循环将销毁它。
- `GDK_MAP` 表示窗口已显示在屏幕上。然而，你应该绘制窗口之前等待第一个事件。
- `GDK_UNMAP` 表示窗口已隐藏；可能它被最小化了，或者你调用了 `gtk_widget_hide()`

## 很少使用的事件 (Little-used Events)

还有其他几种不太实用的事件类型，因此本书没有详细介绍它们。本节对每种进行了简要描述以保持完整。你可以安全地跳过本节。

### 可见性事件 (Visibility Events)

可见性事件发生在窗口被遮挡或畅通时。它们并不有用，因为其他事件已经为你提供了你需要的信息。特别是当窗口被遮挡时，你会接收到指示你应该重绘的事件。这里是：

```
typedef _GdkEventVisibility GdkEventVisibility;
```

`state` 是一个指示窗口是被遮挡还是畅通的枚举值。

### 属性事件 (Property Events)

X 将属性与窗口关联。这些基本上是用于客户端通信的键值对；通常向窗口管理器传递信息。GTK+ 为所有重要的属性提供了高级接口，因此你不需要直接处理它们。当属性值改变时会发送属性事件。

```
typedef _GdkEventProperty GdkEventProperty;
```

```
struct _GdkEventProperty {
GdkEventType type;
GdkWindow *window;
gint send_event;
GdkAtom atom;
gint32 time;
int state;
};
```

### 选择事件 (Selection Events)

X 有简单的复制机制（通常你用鼠标键 1 选择，键 2 粘贴）。剪贴板的内容被称为选择。只有在你编写组件时才需要了解这些。事件指示当前选择发生了变化，其如下：

```
typedef struct _GdkEventSelection GdkEventSelection;

struct _GdkEventSelection {
  GdkEventType type;
  GdkWindow *window;
  gint send_event;
  GdkAtom selection;
  GdkAtom target;
  GdkAtom property;
  gint32 requestor;
  gint32 time;
};
```

大多数 GTK 组件使用 `gtk/gtkselection.h` 中的高级接口来处理选择。如果你对编写选择处理代码感兴趣，请查看该头文件。

### 客户端事件 (Client Events)

客户端事件是从一个应用程序到另一个应用程序的任意数据块。然而，有一些可以发送的常规“消息”，大多定义在客户端通信规范（ICCM）中。ICCM 主要用于应用程序与窗口管理器之间的通信（携带的 XLib 事件是 ClientMessage，因此请在 ICCM 中查找 ClientMessage）。一种从窗口管理器发送到应用程序的重要客户端消息是用于在删除前请求确认，GDK 将这些转换为类型为 `GDK_DELETE` 的事件，因此不会接收 `GdkEventClient`。拖放中的某些事件也是客户端消息，因此 GDK 将这些转换为 `GdkEventNDND`，因此不会为它们接收 `GdkEventClient`。只有当某些客户端向 GTK+ 发送非常规的消息且未准备好处理时，才会接收到 `GdkEventClient`。

仅供参考，这里是该事件：

```
typedef struct _GdkEventClient GdkEventClient;

struct _GdkEventClient {
GdkEventType type;
GdkWindow *window;
gint send_event;
GdkAtom message_type;
gushort data_format;
un
char b[20];
short s[10];
long l[5];
};
```

```
 } data;
};
```

末尾的联合（union）用于存储消息的内容。`send_event` 始终为 TRUE，因为此事件始终从一个客户端发送到另一个客户端，而不是来自 X 服务器。

### 拖放事件

如果你在应用程序中实现拖放功能，那么拖放事件实际上非常有用。然而，由于很少有应用程序需要这种功能，而且该主题相当复杂，本书略提了这一主题。GTK+ 自带了一些关于拖放示例的文档。

```c
typedef _GdkEventDND GdkEventDND;

struct _GdkEventDND {
GdkEventType type;
GdkWindow *window;
gint8 send_event;
GdkDragContext *context;

guint32 time;
gshort x_root, y_root;
};
```

### 接近事件

当使用 GDK 对 XInput 扩展的封装时，会生成接近事件。XInput 扩展是标准 X 的一个插件，允许你使用图形写板等非标准设备。接近事件表示手写笔进入或离开了触摸板的接触范围，或者用户的手指进入或离开了触摸屏的接触范围。X 分发版带有关于 XInput 扩展的文档，以及 Owen Taylor 的 gusumi 应用代码。

```c
typedef _GdkEventProximity GdkEventProximity;
struct _GdkEventProximity {
GdkEventType type;
GdkWindow *window;
gint8 send_event;
guint32 time;
GdkInputSource source;
guint32 deviceid;
};
```

# 鼠标指针

鼠标指针在屏幕上由一个小位图光标表示。鼠标指针通常是箭头形状，但可以按窗口进行更改。当指针移动时，它会产生运动事件并移动屏幕上的光标给用户提供反馈。

## 指针位置

你可以通过 `gdk_window_get_pointer()`（图 10-7）查询指针的位置。此函数请求相对于作为第一个参数传递的窗口的指针 X 和 Y 坐标。它还请求当前的修饰状态（包括键和按钮；此字段与多个事件（如按钮事件）中的状态相同）。如果对 x、y 或 state 参数传递 NULL，则这些参数将被忽略。

```c
#include <gdk/gdk.h>
GdkWindow* gdk_window_get_pointer(GdkWindow* window, wint* x, wint* y, GdkModifierMask* state);
```

图 10-7. 查询指针位置

## 捕获指针

可以捕获（grab）指针，这意味着在捕获期间，所有的指针事件将发送到捕获窗口。通常情况下，指针事件发送到指针所在的窗口。如果用户正在点击并拖动以选择矩形区域，你就应该捕获指针。如果你将指针拖到窗口外，你将继续跟踪指针的位置并相应地更改选择。捕获还确保指针事件不会发送到其他应用程序。

要捕获指针，请调用图 10-8 所示的 `gdk_pointer_grab()`。该函数的第一个参数是捕获窗口；此窗口在捕获期间接收事件。下一个参数应该是 TRUE 或 FALSE；它指定了哪些事件将仅发送到捕获窗口或其子窗口。`config` 参数指定了要限制的指针。用户将无法将指针移动到此窗口之外，除非他们在捕获期间使用不同的光标；创建光标请参见下一节。如果你不想更改光标，请将 NULL 作为光标参数传递。（注意：在调用 `gdk_pointer_grab()` 后立即销毁光标是安全的，因为它是服务器资源，在捕获结束之前不会释放）
