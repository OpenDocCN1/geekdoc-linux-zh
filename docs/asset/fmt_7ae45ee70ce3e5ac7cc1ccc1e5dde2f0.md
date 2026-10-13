
| 参数 | 描述 |
| --- | --- |
| `ctree` | 函数将作用的 `GtkCree` 指针。 |
| `node` | 要从 `GtkCree` 中移除的 `GtkCreeNode` 指针。如果此参数为 `NULL`，将清空整个树。 |

![](img/7fa9959a9d28ad339fa75e44952feeb9_764_0.png)

```c
void gtk_ctree_select( GtkCree *ctree, GtkCreeNode *node )
```

```c
void gtk_ctree_select_recursive( GtkCree *ctree, GtkCreeNode *node )
```

| 参数 | 描述 |
|---|---|
| `ctree` | 指向 `GtkCree` 的指针，该函数将对其进行操作。 |
| `node` | 指向将被选中的 `GtkCreeNode` 的指针。递归版本也会选择该节点的子分支（如果存在的话）。 |

```c
void gtk_ctree_set_expander_style( GtkCree *ctree, GtkCreeExpanderStyle expander_style )
```

| 参数 | 描述 |
|---|---|
| `ctree` | 指向 `GtkCree` 控件的指针，将更改其展开器符号。 |
| `expander_style` | 使用哪种展开器符号。有效选项有：`GTK_CTREE_EXPANDER_NONE`, `GTK_CTREE_EXPANDER_SQUARE`, `GTK_CTREE_EXPANDER_TRIANGLE`, `GTK_CTREE_EXPANDER_CIRCULAR`。 |

```c
void gtk_ctree_set_line_style( GtkCree *ctree, GtkCreeLineStyle line_style )
```

| 参数 | 描述 |
|---|---|
| `ctree` | 指向 `GtkCree` 控件的指针，将更改其线条样式。 |
| `line_style` | 使用哪种线条样式。有效选项有：`GTK_CTREE_LINES_NONE`, `GTK_CTREE_LINES_SOLID`, `GTK_CTREE_LINES_DOTTED`, `GTK_CTREE_LINES_TABBED`。 |

```c
void gtk_ctree_set_node_info( GtkCree *ctree, GtkCreeNode *node, const gchar text, uint8_t spacing, GdkPixmap pixmap_closed, GdkBitmap mask_closed, GdkPixmap pixmap_opened, GdkBitmap mask_opened, boolean is_leaf, boolean expanded )
```

# 附录 D

| 参数 | 描述 |
| --- | --- |
| `ctree` | 指向 `GtkTree` 的指针，该函数将对其进行操作。 |
| `node` | 指向将被修改的 `GtkTreeNode` 结构的指针。 |
| `text` | 包含将显示在行树状列中文本的指针字符串。 |
| `spacing` | 整数，定义了行树状列位图与行树状列文本之间的像素距离。 |
| `pixmap_closed` | 指向 `GtkPixmap` 的指针，当分支折叠时将显示在行树状列中。 |
| `mask_closed` | 指向 `GdkBitmap` 的指针，将作为分支折叠时显示在行树状列中的位图的透明度掩码。 |
| `pixmap_opened` | 指向 `GtkPixmap` 的指针，当分支展开时将显示在行树状列中。 |
| `mask_opened` | 指向 `GdkBitmap` 的指针，将作为分支展开时显示在行树状列中的位图的透明度掩码。 |
| `is_leaf` | 布尔值，指示该节点是否为叶子节点（因此包含子分支）。 |
| `expanded` | 要添加到容器的控件。 |

```c
gtk_ctree_unselect()
```

```c
void gtk_ctree_unselect(GtkCree *ctree
```

```c
void gtk_ctree_unselect_recursive(GtkCree *ctree
```

| 参数 | 描述 |
| --- | --- |
| `ctree` | 指向 `GtkTree` 的指针，该函数将对其进行操作。 |
| `node` | 指向将被取消选择的 `GtkTreeNode` 的指针。递归版本也会取消选择该节点的子分支（如果存在的话）。 |

```c
gtk_dialog_new()
```

```c
GtkWidget* gtk_dialog_new( void )
```

```c
gtk_drag_begin()
```

# 函数原型

```c
GdkDragContext* gtk_drag_begin(GtkWidget *widget)
```

如果由于某些原因无法开始拖拽，则返回 `NULL`。否则，将返回与刚刚开始的拖拽事件对应的 `GdkDragContext` 指针。

| 参数 | 描述 |
| --- | --- |
| `widget` | 指向将成为源控件的指针。 |
| `targets` | 指向 `GtkTargetList` 的指针，包含要注册的变量。其内容会被复制到内部列表，因此后续对 `GtkTargetList` 的修改不会反映在活跃的拖拽操作中。 |
| `actions` | 源控件支持的操作。 |
| `button` | 点击开始拖拽的鼠标按钮。 |
| `event` | 指向触发拖拽的事件的指针。通常是 `motion_notify_event`。 |

```c
gtk_drag_finish()
void gtk_drag_finish(GdkDragContext *context, boolean success, boolean del, guint32 time )
```

| 参数 | 描述 |
| --- | --- |
| `context` | 指向对应此拖放操作的 `GdkDragContext` 结构。通常，这是你通过 `drag_data_received` 信号收到的那个。 |
| `success` | 布尔值。`TRUE` 表示拖拽执行成功；`FALSE` 表示失败。 |
| `del` | 布尔值，指示是否应该删除拖拽源的数据。这通常只在使用了 `GDK_ACTION_MOVE` 时使用。 |
| `time` | 拖拽结束的时间。通常，你将使用通过 `drag_data_received` 信号提供的值。 |

```c
gtk_drag_get_data()
void gtk_drag_get_data(GtkWidget *widget, GdkDragContext *context, GdkAtom target, guint32 time )
```

# 附录 D

| 参数 | 描述 |
| --- | --- |
| `widget` | 指向将接收 `drag_data_received` 信号的控件的指针。 |
| `context` | 指向对应当前拖放事件的 `GdkDragContext` 结构。 |
| `target` | 需要检索其数据的 atom。 |
| `time` | 请求的时间。通常，你将使用通过 `drag_drop` 信号提供的值。 |

```c
gtk_drag_highlight(), gtk_drag_unhighlight()
void gtk_drag_highlight(GtkWidget *widget )
void gtk_drag_unhighlight(GtkWidget *widget )
```

```c
gtk_drag_dest_set()
void gtk_drag_dest_set(GtkWidget *widget, GdkTargetFlags flags, const GtkTargetEntry *targets, gint ntargets) )
```

| 参数 | 描述 |
| --- | --- |
| `widget` | 指向将接收 `drag_data_received` 信号的控件的指针。 |
| `context` | 指向对应当前拖放事件的 `GdkDragContext` 结构。 |
| `target` | 必须获取数据的 atom。 |
| `time` | 请求的时间。通常，你将使用通过 `drag_drop` 信号提供的值。 |

```c
gtk_drag_highlight(),
_drag_unhighlight_
void_____(GtkWidget *widget G
void G,,,,,( GEntry *Entry *
, gint n )
```

| 参数 | 描述 |
| --- | --- |
| `widget` | 指向将接收 `drag_data_received` 信号的控件的指针。 |
| `context` | 指向对应当前拖放事件的 `GdkDragContext` 结构。 |
| `target` | 必须获取数据的 atom。 |
| `time` | 请求的时间。通常，你将使用通过 `drag_drop` 信号提供的值。 |
