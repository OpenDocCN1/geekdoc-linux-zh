
## `gdk_string_to_compound_text()` 的参数

| 参数 | 说明 |
| --- | --- |
| `string` | 指向必须转换为复合文本的字符串的指针。 |
| `encoding` | 现有 `GdkAtom` 的引用，复合文本的编码将存储其中。 |
| `format` | 现有 `gint` 的引用，复合文本的格式将存储其中。 |
| `ctext` | 现有无符号字符指针的引用，指向复合文本的指针将存储其中。 |
| `length` | 现有 `gint` 的引用，复合文本的长度将存储其中。 |

不应使用该函数的返回值，因为它可能包含来自低层 Xlib 函数的值。

之后，必须使用 `gdk_free_compound_text()` 释放复合文本的内存。其完整原型如下：

```
void gdk_free_compound_text(gchar *ctext);
```

### `gdk_free_compound_text()` 的参数

| 参数 | 说明 |
|---|---|
| `ctext` | 必须释放的复合文本 |

## 处理所有权的丢失

有时，当小部件丢失对选择的所有权时接收通知是非常重要的。此通知作为指示，用于释放当小部件成为选择所有者时所分配的内存。要接收此通知，应将 `selection_clear_event` 信号连接到所有者小部件。

```
gtk_signal_connect(widget, "selection_clear_event",
(GtkSignalFunc)selection_clear_handler,NULL);
```

`selection_clear_event` 信号处理函数的原型为：

```
boolean selection_clear_handler(GtkWidget *widget, GdkEventSelection *event, [sr])
gpointer user_data
```

### `selection_clear_event` 的参数

| 参数 | 说明 |
|---|---|
| `widget` | 指向丢失所有权的小部件的指针 |
| `event` | 指向 `GdkEvent` 结构的指针 |
| `user_data` | 当该信号的信号处理器连接到小部件时提供的可选用户数据。 |

![](img/7fa9959a9d28ad339fa75e44952feeb9_580_0.png)

当你想要明确从小部件中移除特定选择的所有权时，必须使用 `gtk_selection_owner_set()` 函数，并将 `widget` 参数的值设置为 `NULL`。例如：

`gtk_selection_owner_set(NULL, GDK_SELECTION_PRIMARY, GDK_CURRENT_TIME);`

## 一个简单的所有权示例

列表 20.3 创建了一个带按钮的窗口。在启动时，支持的目标 `STRING` 和 `LENGTH` 被注册到按钮小部件上，用于 `PRIMARY` 选择。

列表 20.3 演示所有者的作用
