
| 参数 | 描述 |
| --- | --- |
| `ctree` | 函数将作用的 `GtkCtree` 指针。 |
| `node` | 指向将展开或折叠的 `GtkCreeNode` 指针。如果存在子分支，函数的递归版本也会展开或折叠该节点的子分支。 |
| `depth` | 表示子分支展开或折叠到何种深度的值。 |

```c
gtk_ctree_find_node_ptr()
GtkCreeNode * gtk_ctree_find_node_ptr(GtkCtree *ctree, GtkCreeRow *ctree_row
```

# 函数原型

如果找到了 `GtkTreeRow`，则返回指向相应 `GtkTreeNode` 结构的指针，否则返回 `NULL`。

| 参数 | 描述 |
| --- | --- |
| `ctree` | 函数将作用的 `GtkTree` 指针。 |
| `ctree_row` | 需要查找其对应 `GtkTreeNode` 结构体的针。 |

## `gtk_ctree_insert_node()`

```c
GtkTreeNode* gtk_ctree_insert_node(GtkTree *ctree, GtkTreeNode *parent, GtkTreeNode *sibling, gchar *text[], guint8 spacing, GdkPixmap *pixmap_closed, GdkBitmap *mask_closed, GdkPixmap *pixmap_opened, GdkBitmap *mask_opened, gboolean is_leaf, gboolean expanded)
```

返回新创建的 `GtkTreeNode` 结构的指针。

| 参数 | 描述 |
| --- | --- |
| `ctree` | 函数将作用的 `GtkTree` 指针。 |
| `parent` | 指向父 `GtkTreeNode` 的指针，值为 `NULL` 则将节点插入到树的顶层。 |
| `sibling` | 指向兄弟 `GtkTreeNode` 的指针，值为 `NULL` 则将节点附加到分支末尾。 |
| `text` | 指向字符串数组的指针，包含要在新行每个单元格中显示的文本。该数组的大小必须与树的列数相同。 |
| `spacing` | 整数，定义行树状列像素图与该行树状列文本之间的像素距离。 |
| `pixmap_closed` | 指向在分支折叠时在行树状列中显示的 `GtkPixmap` 指针。 |
| `mask_closed` | 指向 `GdkBitmap` 指针，将用作分支折叠时在行树状列中显示的像素图的透明掩码。 |
| `pixmap_opened` | 指向在分支展开时在行树状列中显示的 `GtkPixmap` 指针。 |
| `mask_opened` | 指向 `GdkBitmap` 指针，将用作分支展开时在行树状列中显示的像素图的透明掩码。 |

![](img/7fa9959a9d28ad339fa75e44952feeb9_762_0.png)

# 附录 D

`is_leaf`
布尔值，指示此节点是否为叶子节点（不包含子分支）。

`expanded`
要添加到容器的组件

```c
gtk_ctree_new()
GtkWidget* gtk_ctree_new(gint columns, gint tree_column)
```

| 参数 | 描述 |
| --- | --- |
| `columns` | `GtkTree` 使用的列数。这在创建组件后无法更改。 |
| `tree_column` | 用于提供 `GtkTree` 特定功能的列索引。第一列为 0，第二列为 1，依此类推。 |

```c
gtk_ctree_with_titles()
GtkWidget* gtk_ctree_with_titles(gint columns, gint tree_column)
```

| 参数 | 描述 |
| --- | --- |
| `columns` | `GtkTree` 使用的列数。这在创建组件后无法更改。 |
| `tree_column` | 用于提供 `GtkTree` 特定功能的列索引。第一列为 0，第二列为 1，依此类推。 |

```c
gtk_ctree_nth()
GtkTreeNode* gtk_ctree_nth(GtkTree *ctree, gint row)
```

| 参数 | 描述 |
| --- | --- |
| `ctree` | 函数将作用的 `GtkTree` 指针。 |
| `row` | `GtkTree` 中的位置。 |

```c
gtk_ctree_node_set_pixmap()
void gtk_ctree_node_set_pixmap(GtkTree *ctree, GtkTreeNode *node, gint column, GdkPixmap *pixmap, GdkBitmap *mask)
```

| 参数 | 描述 |
| --- | --- |
| `ctree` | 函数将作用的 `GtkTree`。 |
| `node` | `GtkTreeNode` 结构。 |
| `column` | 单元格列索引。 |
| `pixmap` | 将在单元格中显示的 `GtkPixmap`。 |
| `mask` | 作为像素图透明掩码的 `GdkBitmap`。 |

```c
gtk_ctree_node_set_text()
void gtk_ctree_node_set_text(GtkTree *ctree, GtkTreeNode *node, gint column, const gchar *text)
```

| 参数 | 描述 |
| --- | --- |
| `ctree` | 函数将作用的 `GtkTree`。 |
| `node` | 修改的 `GtkTreeNode`。 |
| `column` | 单元格列索引。 |
| `text` | 显示在单元格中的字符串指针。 |

```c
gtk_ctree_node_set_data()
void gtk_ctree_node_set_data(GtkTree *ctree, GtkTreeNode *node, gpointer data)
```

| 参数 | 描述 |
| --- | --- |
| `ctree` | 函数将作用的 `GtkTree`。 |
| `node` | 修改的 `GtkTreeNode`。 |
| `data` | 存储在节点中的指针。 |

```c
gtk_ctree_node_set_data_full()
void gtk_ctree_node_set_data_full(GtkTree *ctree, GtkTreeNode *node, gpointer data, GtkNotify destroy)
```

| 参数 | 描述 |
| --- | --- |
| `ctree` | 函数将作用的 `GtkTree`。 |
| `node` | 存储数据的 `GtkTreeNode`。 |
| `data` | 作为额外数据存储的指针。 |
| `destroy` | 当行从 `GtkList` 移除时调用的 `GtkNotify` 回调函数。 |

```c
gtk_ctree_remove_node()
void gtk_ctree_remove_node(GtkCree *ctree, GtkCreeNode *node)
```
