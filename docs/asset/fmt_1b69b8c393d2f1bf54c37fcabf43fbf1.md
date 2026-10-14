
# GNOME2 官方开发者指南

## 3.11.2 树视图 (Tree Views)

要移除渲染器数据函数，请调用上述函数并传入`NULL`。`GtkTreeView`对象具有以下属性：

- `visible (boolean)`: 如果为`FALSE`，则列不会显示在视图中。
- `resizable (boolean)`: 如果为`TRUE`，用户可能可以通过绘制列标题的边框来调整列宽。
- `widget (int, 只读)`: 列以像素为单位的当前宽度。
- `sizing (GtkTreeViewColumns)`: 列相对于模型的尺寸模式。可能的值如下：
  - `GTK_TREE_VIEW_COLUMN_GROW_ONLY`: 模型的更改会导致列扩展，但不会收缩。
  - `GTK_TREE_VIEW_COLUMN_FIXED`: 列将根据固定宽度属性（在本节稍后部分描述）保持相同宽度。
  - `GTK_TREE_VIEW_COLUMN_AUTOSIZE`: 随着数据进入或离开模型，列可能会扩展或收缩到最优宽度。这对于大型模型可能是无效的。
- `fixed-width (int)`: 如果您将`size`设置为固定，则此属性是列以像素为单位的宽度。
- `min-width (int)`: 列以像素为单位的最小宽度。
- `max-width (int)`: 列以像素为单位的最大宽度。
- `title (gchararray)`: 列的标题。
- `widget (GtkWidget)`: 放在列标题中而不是文本标题的 widget。

在标题中放置任意 widget 是没有意义的。小图标可以，但许多其他 widget 不行。

- `alignment (float)`: 列标题的水平对齐方式。与其他 widget 一，0.0 左对齐，0.5 居中，1.0 右对齐。
- `sort-indicator (boolean)`: 如果为`TRUE`，则列包含一个排序指示器（通常是标题中的箭头）。
- `sort-order (enumeration)`: 如果列对其数据进行排序，此属性指示排序顺序；可能的值为：
- `clickable (boolean)`: 如果为`TRUE`，则列包含一个排序指示器（通常是标题中的箭头）。

## 3.11 选择行

其中`mode`为以下模式之一：

- `GTK_SELECTION_NONE`: 用户无法在视图中选择任何内容。
- `GTK_SELECTION_SINGLE`: 用户在视图中最多只能选择一行。这是默认设置。
- `GTK_SELECTION_BROWSE`: 显示器中始终恰好有一行显示为选中状态。这对于字体、文件等列表非常有用，因为这些列表应该始终只有一个选中项。
- `GTK_SELECTION_MULTIPLE`: 用户可以选择多行。

在`GTK_SELECTION_SINGLE`和`GTK_SELECTION_BROWSE`模式下，你可以获取当前选中的节点

```c
boolean gtk_tree_selection_get_selected(GtkTreeSelection *selection, GtkTreeModel *model, GtkTreeIter *iter)
```

如果有当前选中项，此函数返回`TRUE`，`iter`指向当前选中项；如果`model`不为`NULL`，则返回指向选择列表或树模型的指针。然而，如果没有选中项，此函数返回`NULL`且不执行其他操作。

如果选择模式为`GTK_SELECTION_MULTIPLE`，则无法使用上述函数。有两种处理方法；较简单的方法是

```c
gtk_tree_selection_selected_foreach(selection, func, data)
```

即对`selection`中的每一行调用一次`func`，并带上数据指针。你必须编写对应类型的`func`：

```c
typedef void (*GtkTreeSelectionForEachFunc)(GtkTreeModel *model, GtkTreePath *path, GtkTreeIter *iter, gpointer data);
```

在这里，`iter`指向`model`中的选择节点：该节点即为地址。

如果你希望以`GList`的形式获取多行（例如，当你需要将选中项传递给其他函数时），请使用

```c
gtk_tree_selection_get_selected_rows(selection, model_ptr_addr)
```

返回值是一个包含`GtkPath`结构体的`GList`。如果你提供模型指针的地址作为`model_ptr_addr`，此函数会将该指针设置为当前模型。你负责负责释放返回值的内存；你可以通过以下方式实现：

```c
g_list_foreach(selected_rows, gtk_tree_path_free, NULL);
g_list_free(selected_rows);
```

这些额外的函数用于查询和操作：

- `gtk_tree_selection_path_is_selected(GtkTreeSelection *selection, GtkTreePath *path)`: 如果`path`是选择的一部分，则返回`TRUE`。
- `gtk_tree_selection_iter_is_selected(GtkTreeSelection *selection, GtkTreeIter *iter)`: 如果`iter`指向选择的一部分，则返回`TRUE`。
- `void gtk_tree_selection_select_path(GtkTreeSelection *selection, GtkTreePath *path)`: 将选择切换到`path`所指向的节点。
- `void gtk_tree_selection_select_iter(GtkTreeSelection *selection, GtkTreeIter *iter)`: 将选择切换到`iter`指向的节点。
- `void gtk_tree_selection_select_all(GtkTreeSelection *selection)`: 强制选择其对应视图中的所有节点。
- `void gtk_tree_selection_unselect_path(GtkTreeSelection *selection, GtkTreePath *path)`: 从选择中移除`path`所指向的节点。
- `void gtk_tree_selection_unselect_iter(GtkTreeSelection *selection, GtkTreeIter *iter)`: 从选择中移除`iter`指向的节点。
- `void gtk_tree_selection_unselect_all(GtkTreeSelection *selection)`

```c
typedef boolean (* GtkTreeSelectionFunc)(GtkTreeSelection *selection, GtkTreeModel *model, GtkTreePath *path, boolean path_currently_selected, gpointer data);
```
