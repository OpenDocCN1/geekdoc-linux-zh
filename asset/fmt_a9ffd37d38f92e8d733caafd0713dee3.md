
| X_BITMAP | Pixmap (depth 1) |

| X_RECTANGLE | XRectangle |

| X_CARDINAL | int |

| X_STRING | char * |

| X_COLORMAP | Colormap |

| X_VISUALID | VisualID |

| X_CURSOR | Cursor |

| X_WINDOW | Window |

| X_DRAWABLE | Drawable |

| X_WM_HINTS | XWMHints |

| X_FONT | Font |

| X_INTEGER | int |

| X_WM_SIZE_HINTS | XSizeHints |

| X_PIXMAP | Pixmap (depth 1) |

在请求者成功调用 `gtk_selection_convert()` 后，所有者将接收到一个选择请求（`GDK_SELECTION_REQUEST`）事件。选择（Selection）标识了请求所属的选择。通常，选择将是 `GDK_SELECTION_PRIMARY`，除非所有者支持多个选择。目标（Target）是目标原子（例如表 3.7 中列出的原子之一）。属性（Property）标识了应该放置所选数据的原子或属性。请求者（Requestor）标识了发起请求的客户端窗口。

现在由于所有者已接收到 `GDK_SELECTION_REQUEST` 事件，它尝试将选择转换为其请求的类型。如果所有者无法执行转换（例如与选择关联的数据是文本，而请求者想要将其转换为调色板），则所有者将创建并向请求者发送 `GDK_SELECTION_NOTIFY` 事件，并将属性设置为 `GDK_NONE`。如果转换成功，所有者也会发送一个 `GDK_SELECTION_NOTIFY` 事件，但属性被设置为所有者在 `GDK_SELECTION_SELECTION_REQUEST` 事件中接收到的相同值。在任何 `GDK_SELECTION_NOTIFY` 事件中的 `selection` 和 `target` 字段应与在 `GDK_SELECTION_REQUEST` 事件中接收到的值相同。

选择协议的大部分发生于请求者端。请求者将接收到 `GDK_SELECTION_NOTIFY` 事件。如果 `property` 字段为 `GDK_NONE`，则请求者知道选择失败。否则，选择成功，请求者随后读取 `property` 字段中的属性以获取转换后的数据。

## GdkEventClient

```
struct _GdkEventClient
{
    GdkEventType type;
    GdkWindow *window;
    gint send_event;
    GdkAtom message_type;
    gushort data_format;
    union {
        char b[20];
        short s[10];
        long l[5];
    } data;
};/* GDK_CLIENT_EVENT */
```

### 事件名称字符串

client_event

### 回调函数原型

```
int
func(GtkWidget *widget, GdkEventClient *event, gpointer arg);
```

客户端事件提供了一种机制，允许一个客户端向另一个在 X 服务器上执行的另一个客户端发送事件。我们在讨论选择时讨论过这个示例。选择的所有者在响应 `GDK_SELECTION_REQUEST` 事件时，将向请求者发送 `GDK_SELECTION_NOTIFY` 事件以指示请求的结果。

客户端可以使用此机制从一个客户端向另一个客户端发送任何类型的事件。但在实践中，客户端事件的使用通常限制在需要满足选择协议的选择中，或者用于窗口管理器使用它们来通知客户端某些待处理事件（例如窗口销毁）。

客户端事件永远不会被接收客户端选择；无论与接收客户端窗口相关的事件掩码如何，它们都将发送给接收客户端。

`message_type` 是一个用于标识所发消息类型的原子。发送和接收此类类型消息的客户端需要对该字段的值达成一致。`data_format` 指定了在事件中发送的消息的格式，并且必须是以下值之一：8、16 或 32。这是为了让 X 服务器能够进行必要的字节交换。`data` 包含了消息中发送的实际数据，内容可以是 20 个 8 位的 char、16 位的 short，或 5 个 32 位的 long。

## GdkEventAny

```
struct _GdkEventAny {
    GdkEventType type;      /* 此处可以是任何事件类型 */
    GdkWindow *window;
    gint send_event;
};
```

### 事件名称字符串

- destroy_event
- delete_event
- map_event
- unmap_event
- no_expose_event

### 回调函数原型

```
gint
func (GtkWidget *widget, GdkEventAny *event, gpointer arg);
```

`GdkEventAny` 是一种方便且独立于事件的方法，通过它可以访问任何事件的 `type`、`window` 和 `s_event` 事件。通常，你的信号函数将映射到特定类型的事件，而你永远不会使用这种类型。然而，某些事件只通信类型和窗口信息，因此使用 `GdkEventAny` 将事件传递给回调函数，代价是降低代码的清晰度。具有 `GDK_DESTROY`、 `GDK_DELETE`、`GDK_UNMAP`、`GDK_EXPOSE` 的事件类型。

## 信号和事件 API

每个小部件（widget）都有一个信号，当触发时表示状态。在此我们将讨论信号的一些要点。让我们看看可用的函数。

### 信号查找

第一个函数是 `gtk_signal_lookup()`。该函数的原型如下：

```
gint
gtk_signal_lookup(gchar *name, gint object_type)
```

`gtk_signal_lookup()` 的作用是从 `object_type` 开始递归向上搜索由 `name` 标识的信号。如果搜索成功，则将返回标识信号的唯一数字。如果搜索失败，则 `gtk_signal_lookup()` 返回 -1。

要使用它，你需要了解对象类型和信号名称。让我们从对象类型开始。每个 Gtk 小部件都有一个由程序员定义的对象类型。类型的命名约定似乎是 `GTK_OBJECT*`，其中 `*` 替换为类的名称。例如，对应 GtkButton 类的类型是 `GTK_OBJECT_BUTTON`。对象类型定义在小部件类的头文件中，通常是 `gtk.h`，其中类型是类的名称。再次以 GtkButton 为例，定义 `GTK_OBJECT_BUTTON` 宏的头文件是 `gtkbutton.h`。该函数的命名有一个约定，对于这种情况下的调用，它是 `gtk_*get_type()`，对于 GtkButton 类来说就是 `gtk_button_get_type()`。

现在让我们谈谈信号名称。在本章早些时候的示例中，我们将回调连接到代表应用程序主窗口的窗口对象的“destroy”，代码如下：

```
gtk_signal_connect(GTK_OBJECT(window), "destroy",
    GTK_SIGNAL_FUNC(PrintAndExit), times);
```

这是一个信号名称的示例。另一个是我们连接到 GtkButton 小部件类定义的“clicked”信号。每个小部件类都定义了许多特定于该类的信号。多个类共的信号将定义在父类中，共享的小部件类可以从从中继承。

### 信号查找

识别我们传递给 `gtk_signal_connect()` 的信号名称。请注意，这是一个构造的示例，但它将说明如何调用 `gtk_signal_lookup()`。

```c
if ( gtk_signal_lookup( "destroy", GTK_OBJECT_WINDOW ) )
```

/* "destroy" 信号已实现，现在继续向小部件注册信号函数 */

```c
gtk_signal_connect(GTK_OBJECT(window), "destroy",
GTK_SIGNAL_FUNC(PrintAndWait), times);
```

```c
else
printf(stderr, "destroy' is not implemented\n");
```

以下是调用 `gtk_signal_lookup()` 的回调函数的另一种方法：

`GtkObject *object;`

```c
object = GTK_OBJECT(window);
if ( gtk_signal_lookup( "destroy", GTK_OBJECT_TYPE(object) ) )
```

`GTK_OBJECT_TYPE` 接收一个 `GtkObject` 参数。我将在本章中详细讨论。注意，前面的代码提高了重用性。我们可以使用这种策略定义一个函数，该函数可以被调用并在任意小部件中搜索指定的信号名称：

/* 如果信号名称未定义则返回 0，否则返回 1 */

```c
gint
HasSignal( GtkWidget *widget, char *name)
{
GtkObject *object;
int retval = 0;

object = GTK_OBJECT(widget);
if ( object != (GtkObject *) NULL )
retval = gtk_signal_lookup( name,
GTK_OBJECT_TYPE( object ) );
return ( retval );
}
```

Gtk+ 还定义了一个接收信号数字并返回该信号字符名称的函数。以下是它的原型：

```c
gchar*
tk_signal_name (int signal_num)
```

Gtk+ 维护了一个全局信号名称表。Gtk+ 中的信号数字仅仅是该表中的索引，因此此函数实际的作用是返回存储在由 `signal_num` 索引表中的字符串（如果 `signal_num` 不是表中有效索引，则返回 0）。

### 发射信号

虽然在实践中这可能不是常见操作，但 Gtk+ 确实赋予了客户端触发事件和信号的能力。这可以通过调用 `gtk_signal_emit*` 函数之一来实现：

```c
void
gtk_signal_emit (GtkObject *object, gint signal_type, ...)

void
gtk_signal_emit_by_name (GtkObject *object, gchar *name, ...)
```

这两个函数的第一个参数都是来自产生信号或事件的对象。`gtk_signal_emit()` 的第二个参数是信号类型。这可以通过如前所述的调用 `gtk_signal_lookup()`（或之前开发的 `HasSignal()` 函数）来找到。`gtk_signal_emit_by_name()` 的第二个参数是事件名称，`gtk_signal_emit_by_name()` 将由其自己执行查找操作。如果你已经有了信号值，调用 `gtk_signal_emit()` 会更高效，因为可以避免 `gtk_signal_emit_by_name()` 在查找事件名称字符串并将其转换为 `gtk_signal_emit()` 接受的信号类型值时产生的开销。

`gtk_signal_emit*` 函数的剩余参数其类型和数量根据发射的信号而异。例如，`map_event (GDK_MAP)` 回调函数的原型如下：

```c
gint
func(GtkWidget *widget, GdkAny *event, gpointer arg);
```

随后调用 `gtk_signal_emit_by_name()` 的方式如下：

```c
GdkEventAny event;
gint retrieval;

...
gtk_signal_emit_by_name (GK_OBJECT(window), "map_event", &event,
&retrieval);
```

`gtk_signal_emit_by_name()` 的第三个参数指向 `GdkEventAny` 结构的指针，它作为第二个参数传递给信号回调函数。第四个参数是指回调函数返回值的指针，类型为 `int`。如果调用的回调函数是 `void`，我们只需省略 `gtk_signal_emit*` 的最后一个参数（如下例所示）。

注意，执行上述调用的应用程序需要填充 `event` 的字段，包括窗口 ID 和 `second_event` 字段。回调的第三也是最后一个参数是传递给 `gtk_signal_connect()` 的应用程序特定指针或数据。

作为第二个示例，`GtkButton` 小部件 "pressed" 信号的回调函数具有以下函数原型：

```c
void
func (GtkWidget *button, gpointer data);
```

为了调用此处理程序，我们将如下调用 `gtk_signal_emit_by_name()`：

`gtk_signal_emit_by_name (GTK_OBJECT (button), "pressed");`

回调没有返回值（该函数是 `void`），我们不需要传递一个用于持有返回值的指针，而是传递 `NULL`。回调函数没有参数（除了所有回调函数都会接收的强制性小部件指针和应用程序私有数据外），因此我们不向 `gtk_signal_emit*` 函数传递额外的参数。

某些小部件函数是有参数的。例如，`GtkListBox` 小部件（我们将在本书的后半部分讨论）当用户选择某行时调用的回调函数具有以下函数原型：

```c
void
select_row_callback(GtkWidget *widget, int row, int column, GdkEvent *event, gpointer data);
```

`select_row_callback` 函数传递给每个信号的 `widget` 和 `data` 参数外，还接收三个参数——`row`、`column` 和 `event`。在这种情况下，对 `gtk_signal_emit_by_name()` 的调用如下：

```c
GtkWidget *clist;
int row, column;

gtk_signal_emit_by_name (GTK_OBJECT (clist), "select_row", row,
column, NULL);
```

`NULL` 作为 "event" 参数传递给 `select_row_callback()`。

### 发射信号——示例

现在该提供一些示例代码。此示例创建一个带有 `GtkDrawingArea` 子部件的顶层窗口。每秒，应用程序生成并处理一个合成事件。它还处理当鼠标移动过窗口时发生的运动事件。
