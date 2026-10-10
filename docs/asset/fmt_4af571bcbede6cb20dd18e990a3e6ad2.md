
```c
gtk_box_set_spacing(GTK_BOX(hbox), 10);

gtk_container_add(GTK_CONTAINER(node), hbox);

gtk_box_pack_start(GTK_BOX(hbox), image, FALSE, FALSE, 0);

gtk_box_pack_start(GTK_BOX(hbox), label, FALSE, FALSE, 0);

gtk_tree_append(GTK_TREE(subtree), node);

gtk_widget_show_all(node);
}
```

我将讨论新增的这些行。在第 001 行，创建了一个 `GtkLabel` 实例。标签通过 `colortable` 数据结构的字段进行设置。在第 002 行，将框间距设置为 10 像素，以便位图和标签之间有足够的水平间隔。在第 003 行，我仅将标签控件作为水平框的子节点，紧随位图之后。结果如图 12.10 所示。

![](img/1441ee0eb9a357efc9aff107f92bf0c0_648_0.png)

图 12.10 在树中显示颜色和颜色名称

## 子树

树项可以做两件事：第一，它们能够显示内容，通常是标签。这在本章中我们已经多次说明了这一点。第二，它们可以作为子树的锚点（anchor points）。一个仅显示标签或其他控件的树项可以被用户选择。锚定子树的树项也可以被选择，或者可以展开以显示其所锚定的子树的第一层内容。通常情况下，你赋予锚定子树的树项的名称应该为用户提供良好的指示，让他们知道打开子树后将找到的内容。

子树也是树。你通过调用 `gtk_tree_new()` 创建它们，并通过创建树项来填充它们，然后通过调用其中一个 `GtkTree` 函数（如 `gtk_tree_append()`、`gtk_tree_prepend()` 或 `gtk_tree_insert()`）将其附加到树。通过调用 `gtk_tree_item_set_subtree()` 将子树附加到父树。

```c
void gtk_tree_item_set_subtree(GtkTreeItem *tree_item, GtkWidget *subtree);
```

参数 `subtree` 是 `GtkTree` 的实例，其内容是任意的（例如它可以包含子树；树的结构并不相关）。参数 `tree` 是父树中的树项，它将作为所添加子树的锚点。

一个树项只能作为一个子树的锚点。调用 `gtk_tree_item_set_subtree` 会使该树项符合移除的条件。`gtk_tree_item_remove()` 的函数原型如下：

```c
void gtk_tree_item_remove(GtkTreeItem *tree_);
```

# 表 12.5 信号（续）

| 信号名称 | 触发信号的条件 |
| --- | --- |
| tree_move | 子树被移动到其他位置。 |
| change_focus_row_expansion | 选定的树发生了键盘展开/折叠（见正文）。 |

## 信号函数原型

```c
void
tree_select_row(GtkTree *ctree, GList *node, gint column,
gpointer user_data);
```

```c
void
tree_unselect_row(GtkTree *ctree, GList *node, gint column,
gpointer user_data);
```

```c
void
tree_expand(GtkTree *ctree, GList *node, gpointer user_data);
```

```c
void
tree_collapse(GtkTree *ctree, GList *node, gpointer user_data);
```

```c
void
tree_move(GtkTree *ctree, GList *node, GList *new_parent,
GList *new_sibling, gpointer user_data);
```

```c
void
change_focus_row_expansion(GtkTree *ctree,
GtkTreeExpansionType expansion, gpointer user_data);
```

## 支持的参数

前缀：`GtkTree::`

# 表 12.6 GtkTree

| 名称 | 类型 | 权限 |
| --- | --- | --- |
| n_columns | GTK_TYPE_UINT | GTK_ARG_READWRITE | GTK_ARG_CONSTRUCT_ONLY |
| tree_column | GTK_TYPE_UINT | GTK_ARG_READWRITE | GTK_ARG_CONSTRUCT_ONLY |

# 表 12.6 GtkCTree 参数（续）

| 名称 | 类型 | 权限 |
|---|---|---|
| indent | GTK_TYPE_UINT | GTK_ARG_READWRITE |
| spacing | GTK_TYPE_UINT | GTK_ARG_READWRITE |
| show_stub | GTK_TYPE_BOOL | GTK_ARG_READWRITE |
| line_style | GTK_TYPE_CTREE_LINE_STYLE | GTK_ARG_READWRITE |
| expander_style | GTK_TYPE_CTREE_EXPANDER_STYLE | GTK_ARG_READWRITE |

# 级 API 概览

在运行时返回常量 `GTK_TYPE_CTREE`：

```c
GtkType
gtk_ctree_get_type(void);
```

创建一个具有指定列数和标题的 `GtkCTree` 实例：
`GtkWidget *`

```c
gtk_ctree_new(gint columns, gint tree_column);
```

创建一个新节点并将其添加到树中：
`GtkCTreeNode *`

```c
gtk_ctree_insert_node(GtkCTree *ctree, GtkCTreeNode *parent,
GtkCTreeNode *sibling, gchar *text[1], guint spacing,
GdkPixmap *pixmap_closed, GdkBitmap *mask_closed,
GdkPixmap *pixmap_opened, GdkBitmap *mask_opened,
gboolean is_leaf, gboolean expanded);
```

从树中移除一个节点：
`void`

```c
gtk_ctree_remove_node(GtkCTree *ctree, GtkCTreeNode *node);
```

遍历树，为树中的每个节点调用 `func(ctree, node, data)`。遍历顺序为后序：
`void`

```c
gtk_ctree_post_recursive(GtkCTree *ctree, GtkCTreeNode *node,
GtkCTreeFunc func, gpointer data);
```

# 级 API 概览（续）

遍历树，为树中的每个节点调用 `func(ctree, node, data)`。遍历顺序为后序，且仅包含到指定深度的节点：
```c
void
gtk_ctree_recursive_to_depth(GtkCTree *ctree, GtkCTreeNode *node, int depth, GtkCTreeFunc func,
gpointer data);
```

遍历树，为树中的每个节点调用 `func(ctree, node, data)`。遍历顺序为前序：
```c
void
gtk_ctree_pre_recursive(GtkCTree *ctree, GtkCTreeNode *node,
GtkCTreeFunc func, gpointer data);
```

遍历树，为树中的每个节点调用 `func(ctree, node, data)`。遍历顺序为前序且仅包含到指定深度的节点：
```c
void
gtk_ctree_pre_recursive_to_depth(GtkCTree *ctree,
GtkCTreeNode *node, int depth, GtkCTreeFunc func,
gpointer data);
```

如果节点可见，则返回 TRUE：
```c
boolean
```
