
- `GTK_SELECTION_BROWSE` - 如果列表没有组件或只有禁用组件，则选择为 NULL；否则包含一个列表项。

- `GTK_SELECTION_MULTIPLE` - 如果没有列表项，选择为 NULL 或包含第一个选中项的 `GList` 指针；随后变为第二个选中项的 `GList` 结构，依此类推。

- `GTK_SELECTION_EXTENDED` - 选择始终为 NULL。

默认值为 `GTK_SELECTION_MULTIPLE`。

## D.1 信号

```c
void selection_changed( GtkList *list );
```

每当 `GtkList` 的选择变化时，此信号就会被调用。这在 `GtkList` 的子被选中或取消选中时发生。

```c
void select_child( GtkList *list,
                   GtkWidget *child);
```

当 `GtkList` 的子组件即将选中时，调用此信号。这主要发生在调用 `gtk_list_select_item(item)`、`gtk_list_select_child(child)`、按钮按下，以及有时在子组件添加到或移出 `GtkList` 时间接触发。

```c
void unselect_child( GtkList *list,
                     GtkWidget *child);
```

当 `GtkList` 的子组件即将取消选中时，调用此信号。这主要发生在调用 `gtk_list_unset_item(item)`、`gtk_list_unset_child(child)`、按钮按下，以及有时在子组件添加到或移出 `GtkList` 时间接触发。

## D.2 函数

```c
guint gtk_list_get_type( void );
```

返回 `GtkList` 类型标识符。

```c
GtkWidget *gtk_list_new( void );
```

创建一个新的 `GtkList` 对象。返回一个指向 `GtkWidget` 对象的指针作为新组件。失败时返回 NULL。

```c
void gtk_list_insert_items( GtkList *list,
               GList *items,
               gint position);
```

从位置开始向列表插入项。`items` 是一个双向链表，其中每个数据指针都预期指向一个新创建的 `GtkListItem`。`items` 的 `GList` 节点将被列表接管。

```c
void gtk_list_append_items( GtkList *list,
               GList *items);
```

在列表末尾以类似于 `gtk_list_insert_items()` 的方式插入项。`items` 的 `GList` 节点将被列表接管。

```c
void gtk_list_prepend_items( GtkList *list,
               GList *items);
```

在列表最开头以类似于 `gtk_list_insert_items()` 的方式插入项。`items` 的 `GList` 节点将被列表接管。

```c
void gtk_list_remove_items( GtkList *list,
               GList *items);
```

从列表中移除项。`items` 是一个双向链表，其中每个数据指针都预期指向列表的直接子项。迭代者负责在之后调用 `g_list_free(items)`。此外，调用者必须自己销毁列表项。

```c
void gtk_list_clear_items( GtkList *list,
               gint start,
               gint end );
```

从列表中移除并销毁列表项。如果组件在列表中的当前位置处于起始和结束指定的范围内，则该组件会受影响。

```
void gtk_list_select_item( GtkList *list,
               gint
               item );
```

通过其在列表中的当前位置指定的列表项触发 `select_child` 信号。

```
void gtk_list_unselect_item( GtkList *list,
               gint
               item);
```

通过其在列表中的当前位置指定的列表项触发 `unselect_child` 信号。

```
void gtk_list_select_child( GtkList *list,
               GtkWidget *child);
```

为指定的子组件触发 `select_child` 信号。

```
void gtk_list_unselect_child( GtkList *list,
               GtkWidget *child);
```

为指定的子组件触发 `unselect_child` 信号。

```
gint gtk_list_child_position( GtkList *list,
               GtkWidget *child);
```

返回组件在列表中的位置。如果失败则返回 "-1"。

```
void gtk_list_set_selection_mode( GtkList *list,
               GtkSelectionMode mode );
```

设置选择模式，其可以是 `GTK_SELECTION_SINGLE`、`GTK_SELECTION_BROWSE`、`GTK_SELECTION_MULTIPLE` 或 `GTK_SELECTION_EXTENDED`。

```
GtkList *GTK_LIST( gpointer obj );
```

将通用指针强制转换为 'GtkList'。*注意：更多信息请参阅标准宏。*

```
GtkListClass *GTK_LIST_CLASS( gpointer class);
```

将通用指针强制转换为 'GtkList*'。*注意：更多信息请参阅标准宏。*

```
gint GTK_IS_LIST( gpointer obj);
```

判断通用指针是否指向 'GtkList' 对象。*注意：更多信息请参阅标准宏。*

## D.3 示例

以下是一个示例程序，它将打印 `GtkList` 选择的变化，并允许你通过使用鼠标右键选择列表项来将它们“逮捕”到监狱中。

```c
/* 初始化 gtk+ (随后是 gdk) */
gtk_init(&argc, &argv);

/* 创建一个窗口来放置所有组件
* 将 gtk_main_quit() 连接到窗口的 "destroy" 事件
* 以处理窗口管理器的关闭窗口事件
 */
window=gtk_window_new(GTK_WINDOW_TOPLEVEL);
gtk_window_set_title(GTK(window), "GtkList Example");
gtk_signal_connect(GTK_OBJECT(window),
    "destroy",
    GTK_SIGNAL_FUNC(gtk_main_quit),
    NULL);
```

```c
/* 在窗口内部，我们需要一个框来垂直 
 * 排列组件 */
vbox=gtk_vbox_new(FALSE, 5);
gtk_container_set_border_width(GTK_CONTAINER(vbox), 5);
gtk_container_add(GTK_CONTAINER(window), vbox);
gtk_widget_show(vbox);
```

```c
/* 这是用于放置 Gtklist 内部的滚动窗口 */
scrolled_window=gtk_scrolled_window_new(NULL, NULL);
scrolled_widget_set_size(scrolled_window, 200, 150);
gtk_container_add(GTK_CONTAINER(vbox), scrolled_window);
gtk_widget_show(scrolled_window);
```
