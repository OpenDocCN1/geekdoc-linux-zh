
# GTK Tree Model API

## 获取值

### `gtk_tree_model_get_value`
```c
void gtk_tree_model_get_value(GtkTreeModel *model, GtkTreeIter *iterator, int column, GValue *value)
```

获取列 `column` 中迭代器对应的值，并将结果放入 `value` 指向的 `GValue` 中。处理完 `value` 后，使用 `g_value_unset()` 释放它。

### `gtk_tree_model_get`
```c
void gtk_tree_model_get(GtkTreeModel *model, GtkTreeIter *iterator, ...)
```

与前面的函数相似，但从当前节点检索所有值。在迭代器之后，放置一个 `GValue` 指针列表；用 `-1` 结束列表。

## 设置值

### `gtk_tree_store_set`
```c
void gtk_tree_store_set(GtkTree *tree, GtkTreeIter *iterator, ...)
```

与前面的函数相似，但在当前节点中设置值而不是读取它们。注意参数不是 `NULL`；它们是列标识符和数据的对。

### `gtk_list_store_set`
```c
void gtk_list_store_set(GtkListStore *list, GtkTreeIter *iterator, ...)
```

与前面的函数相似，但用于列表。

## 插入节点

### `gtk_tree_store_insert`
```c
void gtk_tree_store_insert(GtkTreeStore *tree, GtkTreeIter *iterator, GtkTreeIter *parent, int index)
```

在树的给定索引处插入新节点。如果 `parent` 不为 `NULL`，则新节点成为该节点的子节点。此函数将 `iterator` 指向新节点。

### `gtk_list_store_insert`
```c
void gtk_list_store_insert(GtkListStore *list, GtkTreeIter *iterator, int index)
```

与前面的函数相似，但用于列表。

### `gtk_tree_store_insert_before`
```c
void gtk_tree_store_insert_before(GtkTreeStore *tree, GtkTreeIter *iterator, GtkTreeIter *parent, GtkTreeIter *sibling)
```

在树中作为 `parent` 的子，在 `sibling` 之前插入新节点（`parent` 可能为 `NULL`）。如果 `sibling` 为 `NULL`，节点位于 `parent` 之后。如果 `parent` 和 `sibling` 均为 `NULL`，节点将进入顶层子节点。调用后 `iterator` 指向新节点。

### `gtk_list_store_insert_before`
```c
void gtk_list_store_insert_before(GtkListStore *list, GtkTreeIter *iterator, GtkTreeIter *sibling)
```

与前面的函数相似，但用于列表。

### `gtk_tree_store_insert_after`
```c
void gtk_tree_store_insert_after(GtkTreeStore *tree, GtkTreeIter *iterator, GtkTreeIter *parent, GtkTreeIter *sibling)
```

与 `gtk_tree_store_insert_before()` 相似，但在 `sibling` 之后插入（如果 `sibling` 为 `NULL` 则在所有子节点之前）。

### `gtk_list_store_insert_after`
```c
void gtk_list_store_insert_after(GtkListStore *list, GtkTreeIter *iterator, GtkTreeIter *sibling)
```

与前面的函数相似，但用于列表。

### `gtk_tree_store_prepend`
```c
void gtk_tree_store_prepend(GtkTreeStore *tree, GtkTreeIter *iterator, GtkTreeIter *parent)
```

将新节点作为 `parent` 的第一个子节点插入树。此函数的工作原理类似于 `gtk_tree_store_insert_before()`，但没有 `sibling` 参数。

### `gtk_list_store_prepend`
```c
void gtk_list_store_prepend(GtkListStore *list, GtkTreeIter *iterator, GtkTreeIter *parent)
```

与前面的函数相似，但用于列表。

### `gtk_tree_store_append`
```c
void gtk_tree_store_append(GtkTreeStore *tree, GtkTreeIter *iterator, GtkTreeIter *parent)
```

与 `gtk_tree_store_prepend()` 相似，但新节点成为 `parent` 的最后一个子节点而不是第一个。

### `gtk_list_store_append`
```c
void gtk_list_store_append(GtkListStore *list, GtkTreeIter *iterator)
```

与前面的函数相似，但用于列表。

## 删除节点

### `gtk_tree_store_remove`
```c
void gtk_tree_store_remove(GtkTreeStore *tree, GtkTreeIter *iterator)
```

移除 `iterator` 处的节点。

### `gtk_list_store_remove`
```c
void gtk_list_store_remove(GtkListStore *list, GtkTreeIter *iterator)
```

移除列表中的 `iterator` 节点。

### `gtk_tree_store_clear`
```c
void gtk_tree_store_clear(GtkTreeStore *tree)
```

移除列表中的所有节点。

### `gtk_list_store_clear`
```c
void gtk_list_store_clear(GtkListStore *list)
```

## 查询

### `gtk_tree_store_is_ancestor`
```c
boolean gtk_tree_store_is_ancestor(GtkTreeStore *tree, GtkTreeIter *iterator, GtkTreeIter *child)
```

如果 `child` 在以 `iterator` 为根的树中，则返回 `TRUE`。

### `gtk_tree_store_depth`
```c
int gtk_tree_store_depth(GtkTreeStore *tree, GtkTreeIter *iterator)
```

`iterator` 在树中的深度（`0` 是顶层，`1` 是下一层，依此类推）。

## 遍历

### `gtk_tree_model_foreach`
```c
void gtk_tree_model_foreach(GtkTreeModel *model, GtkTreeModelFunc *function, gpointer data)
```

树的所有节点上运行函数。查看 `GtkTreeModelFunc` 原型：

```c
typedef gboolean (*GtkTreeModelFunc)(GtkTreeModel *model, GtkTreePath *path, GtkTreeIter *iter, gpointer data);
```

`model` 参数是调用时的树或列表，`data` 参数也是如此。当前节点是 `iter`。`path` 是树内的地址。`path` 本质上是数字列表；如果你跟随列表中的数字，可以从 `parent` 到达节点。在列表中只有一个数字；`0` 是第一个元素，`5` 代表列表中的第 6 个元素（记住它最终显示为视图中的行）。对于树，你可以通过冒号读取数字。`4:3` 是树中第四个节点的第三个子节点；另一个例子是 `0:6:2`。大多数路径以 `0` 开头。你可以使用 `path` 创建包含数据的树结构。当程序读取文件时，它可以读取树结构并将其发送树对象。

## 路径操作

### `gtk_tree_model_get_path`
```c
GtkTreePath *gtk_tree_model_get_path(GtkTreeModel *model, GtkTreeIter *iter)
```

返回 `path` 的新副本。

### `gtk_tree_path_free`
```c
void gtk_tree_path_free(GtkTreePath *path)
```

释放 `path` 的内存。

### `gtk_tree_path_to_string`
```c
gchar *gtk_tree_path_to_string(GtkTreePath *path)
```

返回对应 `path` 的冒号分隔字符串。当你不再需要它时，应使用 `g_free()` 释放此字符串。

### `gtk_tree_path_append_index`
```c
void gtk_tree_path_append_index(GtkTreePath *path, gint index)
```

在 `path` 末尾追加索引。

### `gtk_tree_path_prepend_index`
```c
void gtk_tree_path_prepend_index(GtkTreePath *path, gint index)
```

在 `path` 头部插入索引。

### `gtk_tree_path_get_depth`
```c
gint gtk_tree_path_get_depth(GtkTreePath *path)
```

返回 `path` 的深度。

### `gtk_tree_path_get_indices`
```c
gint *gtk_tree_path_get_indices(GtkTreePath *path)
```

返回索引数组。每个数字对应 `path` 中的一个索引。这是 `path` 内部数据的指针，因此在完成后你不应释放它。
