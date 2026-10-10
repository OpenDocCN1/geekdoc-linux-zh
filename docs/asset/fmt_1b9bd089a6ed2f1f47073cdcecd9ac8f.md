
既然我们已经详细讨论了 `GtkList`，是时候看看类似的 Gtk+ 类——`GtkTreeView` 了。尽管它们相似，但 `GtkTreeView` 和 `GtkList` 在部件层次结构中之间互没有关系。正如你所看到的，`GtkTreeView` 比 `GtkList` 功能更强大。我的建议是对简单的单列列表使用 `GtkList`。如果你需要多列列表，或者需要 `GtkList` 提供的额外功能，请改用 `GtkTreeView`。

## GtkList

### 类名
`GtkList`

### 父类名
`GtkContainer`

### 宏
- 部件类型宏：`GTK_TYPE_CLIST`
- 对象到部件转换宏：`GTK_CLIST(obj)`
- 部件类型检查宏：`GTK_IS_CLIST(obj)`

### 表 6.4 信号
| 信号名称 | 触发信号的条件 |
| --- | --- |
| select_row | 列表中的某项状态变更为已选择。 |
| unselect_row | 列表中的某项状态变更为未选择。 |
| row_move | 列表中的某行通过 `gtk_clist_row_move()` 移动到了新位置。 |
| click_column | 列表中的列头被点击。 |
| resize_column | 用户调整了列的大小。 |
| toggle_focus_row | 焦点行状态已发生切换。 |
| select_all | 对列表执行了全选操作。 |
| unselect_all | 对列表执行了取消全选操作。 |
| undo_selection | 列表恢复到之前的选择状态。 |

### 表 6.4 信号（续）
| 信号名称 | 触发信号的条件 |
| --- | --- |
| start_selection | 在 Gtk+ 1.2.8 后未使用。 |
| end_selection | 当 clist 拥有键盘焦点时释放了左 Shift 键。 |
| toggle_add_mode | clist 的添加模式已发生切换。 |
| extend_selection | 当前选择已扩展。 |
| scroll_vertical | 垂直滚动条位置已改变。 |
| scroll_horizontal | 水平滚动条位置已改变。 |
| abort_column_resize | 列调整被取消。 |

### 信号函数原型

```
void
select_row(GtkClist *clist, gint row, gint column, GdkEventButton *event, gpointer user_data);
```

```
void
unselect_row(GtkClist *clist, gint row, gint column, GdkEventButton *event, gpointer user_data);
```

```
void
row_move(GtkClist *clist, gint arg1, gint arg2, gpointer user_data);
```

```
void
click_column(GtkClist *clist, gint column, gpointer user_data);
```

```
void
resize_column(GtkClist *clist, gint column, gint width, gpointer user_data);
```

```
void
toggle_focus_row(GtkClist *clist, gpointer user_data);
```

```
void
select_all(GtkClist *clist, gpointer user_data);
```

### 信号函数原型（续）

```
void
unselect_all(GtkClist *clist, gpointer user_data);

void
undo_selection(GtkClist *clist, gpointer user_data);

void
start_selection(GtkClist *clist, gpointer user_data);

void
end_selection(GtkClist *clist, gpointer user_data);

void
toggle_add_mode(GtkClist *clist, gpointer user_data);

void
extend_selection(GtkClist *clist, GtkScrollType scroll_type, gboolean position, gpointer user_data);

void
scroll_vertical(GtkClist *clist, GtkScrollType scroll_type, gboolean position, gpointer user_data);

void
scroll_horizontal(GtkClist *clist, GtkScrollType scroll_type, gboolean position, gpointer user_data);

void
abort_column_resize(GtkClist *clist, gpointer user_data);
```
