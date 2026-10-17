
在请求者成功调用 `gtk_selection_convert()` 后，所有者会接收到一个选择请求（`GDK_SELECTION_REQUEST`）事件。选择（Selection）标识了请求所属的选择。通常情况下，除非所有者支持多个选择，否则选择将 `GDK_SELECTION_PRIMARY`。目标（Target）是目标原子（例如表 3.7 中列出的原子）。属性（Property）标识了应放置选取数据的原子或属性。请求者（Requestor）标识了发起请求的客户端窗口。

现在所有者已经接收了 `GDK_SELECTION_REQUEST` 事件，它将尝试将选择转换为请求的类型。如果所有者无法执行转换（例如，与选择相关的数据是文本，而请求者想将其转换为调色板），则所有者将创建向请求者发送一个 `GDK_SELECTION_NOTIFY` 事件，其 `property` 字段被设置为 `GDK_NONE`。如果转换成功，所有者也会发送一个 `GDK_SELECTION_NOTIFY` 事件，但其 `property` 字段被设置为所有者在 `GDK_SELECTION_SELECT_REQUEST` 事件中接收到的相同值。任何 `GDK_SELECTION_NOTIFY` 事件中的 `selection` 和 `target` 字段的值应与在 `GDK_SELECTION_REQUEST` 事件中接收到的值相同。

选择协议的大部分发生在请求者端。请求者将接收到一个 `GDK_SELECTION_NOTIFY` 事件。如果 `property` 字段为 `GDK_NONE`，则请求者知道选择失败。否则，选择成功，请求者随后读取 `property` 字段中指定的属性以转换后的数据。

## GdkEventClient

```
struct _GdkEventClient {
  GdkEventType;
  GdkWindow *window;
  gint8 send_event;
  GdkAtom message_type;
  gushort data_format;
  union {
    char b[20];
    short s[10];
    long l[5];
  } data;
}; /* GDK_CLIENT_EVENT */
```

## 事件名称字符串

`client_event`

## 回调函数原型

```
gint func(GtkWidget *widget, GdkEventClient *event, gpointer arg);
```

客户端事件提供了一种机制，使一个客户端可以向运行在 X server 上的另一个客户端发送事件。我们在讨论选择时说明了这种机制的一个示例。选择的所有者在响应 `GDK_SELECTION_REQUEST` 事件时，将向请求者客户端发送一个 `GDK_SELECTION_NOTIFY` 事件，以指示请求的结果。

任何类型的事件都可以通过此机制从一个客户端发送到另一个客户端。但在实践中，客户端事件的使用通常仅限于选择（在需要满足选择协议时），或窗口管理器（它们使用这些来通知客户端某些待处理事件，例如窗口销毁）。

客户端事件永远不会被接收客户端选择；无论与接收客户端窗口关联的事件掩码（event mask）如何，它们都将发送给接收客户端。

`Message_type` 是一个用于标识发送的消息类型的原子。发送和接收此类类型消息的客户端需要就该字段的值达成一致。`Data_format` 指定了事件中发送的消息格式，并且必须是以下值之一：8、16 或 32。这是为了确保 X server 能够进行必要的字节交换。`Data` 包含在消息中发送的实际数据，可以是 20 个 8 位字符、16 个 16 位短型或 5 个 32 位长型。

## GdkEventAny

```
struct _GdkEventAny {
    GdkEventType type;
    GdkWindow *window;
    gint send_event;
};
/* 此处可以是任何事件类型 */
```

## 事件名称字符串

- `destroy_event`
- `delete_event`
- `map_event`
- `unmap_event`
- `no_expose_event`

## 回调函数原型

```
gint func (GtkWidget *widget, GdkEventAny *event, gpointer arg);
```

`GdkEventAny` 是一种方便的、独立于事件的方法，可以访问任何事件的类型、窗口和 `send_event` 事件。通常，你的信号函数将映射到特定类型的事件，而你永远不会使用这种类型。然而，有几个事件只通信类型和窗口信息，因此它们利用 `GdkEventAny` 将事件传递给回调函数，代价是降低了代码的清晰度。回调函数中包含 `GdkEventAny *` 的事件类型包括 `GDK_DESTROY`、`GDK_DELETE`、`GDK_UNMAP`、`GDK_MAP`。

## 信号与事件

所有者在选择协议中，响应 `GDK_SELECTION_REQUEST` 事件将向请求者客户端发送一个 `GDK_SELECTION_NOTIFY` 事件，以指示请求的结果。

任何类型的事件都可以通过此机制从一个客户端发送到另一个客户端。但在实践中，客户端事件的使用通常仅限于选择（在需要满足选择协议时），或窗口管理器（它们使用这些来通知客户端某些待处理事件，例如窗口销毁）。

`Message_type` 是一个用于标识发送的消息类型的原子。发送和接收此类类型消息的客户端需要就该字段的值达成一致。`Data_format` 指定了事件中发送的消息格式，并且必须是以下值之一：8、16 或 32。这是为了确保 X server 能够进行必要的字节交换。`Data` 包含在消息中发送的实际数据，可以是 20 个 8 位字符、16 个 16 位短型或 5 个 32 位长型。

## 发送信号

所有者在选择协议中，响应 `GDK_SELECTION_REQUEST` 事件将向请求者客户端发送一个 `GDK_SELECTION_NOTIFY` 事件，以指示请求的结果。

任何类型的事件都可以通过此机制从一个客户端发送到另一个客户端。但在实践中，客户端事件的使用通常仅限于选择（在需要满足选择协议时），或窗口管理器（它们使用这些来通知客户端某些待处理事件，例如窗口销毁）。

客户端事件永远不会被接收客户端选择；无论与接收客户端窗口关联的事件掩码如何，它们都将发送给接收客户端。

`Message_type` 是一个用于标识发送的消息类型的原子。发送和接收此类类型消息的客户端需要就该字段的值达成一致。`Data_format` 指定了事件中发送的消息格式，并且必须是以下值之一：8、16 或 32。这是为了确保 X server 能够进行必要的字节交换。`Data` 包含在消息中发送的实际数据，可以是 20 个 8 位字符、16 个 16 位短型或 5 个 32 位长型。

## 信号查找

所有者在选择协议中，响应 `GDK_SELECTION_REQUEST` 事件将向请求者客户端发送一个 `GDK_SELECTION_NOTIFY` 事件，以指示请求的结果。

任何类型的事件都可以通过此机制从一个客户端发送到另一个客户端。但在实践中，客户端事件的使用通常仅限于选择（在需要满足选择协议时），或窗口管理器（它们使用这些来通知客户端某些待处理事件，例如窗口销毁）。

客户端事件永远不会被接收客户端选择；无论与接收客户端窗口关联的事件掩码如何，它们都将发送给接收客户端。

`Message_type` 是一个用于标识发送的消息类型的原子。发送和接收此类类型消息的客户端需要就该字段的值达成一致。`Data_format` 指定了事件中发送的消息格式，并且必须是以下值之一：8、16 或 32。这是为了确保 X server 能够进行必要的字节交换。`Data` 包含在消息中发送的实际数据，可以是 20 个 8 位字符、16 个 16 位短型或 5 个 32 位长型。

## 查找信号

所有者在选择协议中，响应 `GDK_SELECTION_REQUEST` 事件将向请求者客户端发送一个 `GDK_SELECTION_NOTIFY` 事件，以指示请求的结果。

任何类型的事件都可以通过此机制从一个客户端发送到另一个客户端。但在实践中，客户端事件的使用通常仅限于选择（在需要满足选择协议时），或窗口管理器（它们使用这些来通知客户端某些待处理事件，例如窗口销毁）。

客户端事件永远不会被接收客户端选择；无论与接收客户端窗口关联的事件掩码如何，它们都将发送给接收客户端。

`Message_type` 是一个用于标识发送的消息类型的原子。发送和接收此类类型消息的客户端需要就该字段的值达成一致。`Data_format` 指定了事件中发送的消息格式，并且必须是以下值之一：8、16 或 32。这是为了确保 X server 能够进行必要的字节交换。`Data` 包含在消息中发送的实际数据，可以是 20 个 8 位字符、16 个 16 位短型或 5 个 32 位长型。

## 触发信号
