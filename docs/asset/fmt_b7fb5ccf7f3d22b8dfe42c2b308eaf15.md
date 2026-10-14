
```c
void handler (GtkTreeView *view,
               GtkTreePath *path,
               GtkTreeViewColumn *column,
               gpointer *data);
```

### 列

`GtkTreeViewColumn`对象在模型和单元渲染器之间传输数据。每列可以有多个渲染器；例如，你可以将人的姓名封装到单元中，名字旁边有一个 true/false 复选框，表示该人是否是左手子。

你可以通过以下代码创建大多数视图列：

```
col = gtk_tree_view_column_new_with_attributes(title, renderer, ...)
```

在这里，`title`是列的字符串，`renderer`绘制单元。后面是一个以 NULL 终止的渲染器属性列表（见 3.11 节的示例）。

单元渲染器通常由渲染类型作为列标识符（或数字）传递给渲染器。3.11 节的示例将 `"text"`映射到列标识符之一。单元渲染器属性不是属性，因此你不能用 `g_object_set()`设置它们。请使用这些函数：

- `void gtk_tree_view_column_set_attributes(GtkTreeViewColumn *column, GtkCellRenderer *renderer, ...)`
- `void gtk_tree_view_column_add_attribute(GtkTreeViewColumn *column, GtkCellRenderer *renderer, *attribute, gint col_id)`  
  用以 NULL 终止的属性对完全替换渲染器的属性。
- `void gtk_tree_view_column_add_attribute(GtkTreeViewColumn *column, GtkCellRenderer *renderer, *attribute, gint col_id)`  
  向渲染器添加新属性。`attribute`字符串是属性的名称，`col_id`是属性的标识符。
- `void gtk_tree_view_column_clear_attributes(GtkTreeViewColumn *column, GtkCellRenderer *renderer)`  
  移除渲染器的属性。
- `void gtk_tree_view_column_clear(GtkTreeViewColumn *column)`  
  移除列中所有渲染器的属性。

如果你想向列中添加渲染器，可以使用这些函数进行打包：

```
gtk_tree_view_column_pack_start(column, renderer, expand)

gtk_tree_view_column_pack_end(column, renderer, expand)
```

在这里，`expand`是一个布尔值；`TRUE`表示渲染器应尝试占据单元的任何空空间，类似于第 3.4 节中的对应属性。

示例显示了：

```
gtk_tree_view_append_column(view, column)
```

用于在视图列列表末尾追加列。此函数返回视图中列的数量，程序员经常忽略此返回值。

# GNOME 2 官方开发者指南

这里有更多操作视图中列的函数：

- `gtk_tree_view_insert_column(GtkTreeView *view, GtkTreeViewColumn *column, gint index)`  
  在指定的 `index`处向视图插入列。0 是列列表的起始位置；使用 -1 作为索引会将该元素添加到视图的末尾。此函数返回视图中新的列总数。
- `gtk_tree_view_insert_column_with_attributes(GtkTreeView *view, GtkTreeViewColumn *column, gint index, GtkCellRenderer *renderer, ...)`  
  与前面的函数相同，添加渲染器，随后跟一个以 NULL 结尾的单元渲染器属性列表。
- `gtk_tree_view_get_column(GtkTreeView *view, gint index)`  
  返回视图中对应于 `index`的列。视图中的第一列为 0。此函数在失败时返回 NULL。
- `gtk_tree_view_get_columns(GtkTreeView *view)`  
  返回视图中一个新分配的列列表。在完成后，您应该使用 `g_list_free()`释放此列表。
- `gtk_tree_view_move_after(GtkTreeView *view, GtkTreeViewColumn *col1, GtkTreeViewColumn *col2, gint col2)`  
  将 `col1`移动到 `col2`之后。如果 `col2`为 NULL，`col1`将位于视图的末尾。
- `gtk_tree_view_remove_column(GtkTreeView *view, GtkTreeViewColumn *column)`  
  从视图中移除列并返回视图中新的列数。

有一个方便的函数可以将视图中的所有列设置为其最优宽度：

```
gtk_tree_view_columns_autosize(view)
```

此函数仅在您通过列关联（将渲染器属性绑定到列标识符）将树模型打包到渲染器上后才有效，但您可以定义自己的列关联函数：

```
gtk_tree_view_insert_column_with_data_func(view,
                                            position,
                                            title,
                                            renderer,
                                            func,
                                            func_data,
                                            destroy_notify)
```

使用 `gtk_tree_view_insert_column_with_attributes()`时，`view`、`position`、`title`和 `renderer`分别是新列的视图、列位置、标题和单元渲染器，但 `func`是您将数据传递到单元渲染器的函数：`func_data`是 GTK 传递给 `func`的无类型指针，而 `destroy_notify`负责释放数据。

`func`的类型定义为

## 3.1.12 树视图 (Tree Views)

# GNOME 官方开发者指南

```c
typedef void (*GtkTreeViewCellDataFunc)(GtkTreeViewColumn *tree_column, GtkCellRenderer *cell, GtkTreeModel *tree_model, GtkTreeIter *iter, gpointer *data);
```

为了渲染单元格，GTK+ 会为视图的 `tree_column`、单元渲染器 `cell`和数据模型 `tree_model`调用此单元函数。最重要的参数是 `iter`，因为它指向要渲染的行。按照惯例，`data`是一个可选的数据指针。

此函数应该使用来自 `tree_model`的适当（可能可能经过微调的）数据来调用单元渲染器。第 3.11.4 节中的程序包含一个示例 `room_convert()`，用于将 -l 更改为横号。

如果您想在创建列后注册渲染器函数，请调用：

```
gtk_tree_view_column_set_cell_data_func(tree_column, cell_renderer, func, cell_data, destroy_notify)
```
