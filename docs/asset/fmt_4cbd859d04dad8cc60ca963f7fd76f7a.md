
```c
void
gtk_ctree_set_indent (GtkTree *ctree, gint indent);
```

参数 `indent` 是大于 0 的整数值。小于 0 将导致断言失败并使 `indent` 值恢复为默认的 20 像素。

## 设置间距

树中显示数据之间的间距可以通过 `gtk_ctree_set_spacing()` 控制：

```c
void
gtk_ctree_set_spacing (GtkTree *ctree, gint spacing);
```

`spacing` 是 0 或更大的整数值（负值会导致断言失败）。

## 设置线条样式

树的线条样式可以通过调用 `gtk_ctree_set_line_style()` 设置：

```c
void
gtk_ctree_set_line_style (GtkTree *ctree,
GtkCreeLineStyle line_style);
```

`line_style` 参数可以是表 12.7 中提供的值之一。

表 12.7 GtkreeLineStyle

|线条样式 | 结果 |

| :--- | :--- |

| GTK_CTREE_LINES_NONE | 不绘制线条。 |

| GTK_CTREE_LINES_SOLID | 实线（默认）。 |

| GTK_CTREE_LINES_DOTTED | 使用点线绘制线条。 |

| GTK_CTREE_LINES_TABBED | 参见图 12.3. |

GtkTree 示例

| 动物 | 栖地 |

| :--- | :--- |

| 鱼类 | |

| 危险动物 | |

| 大白鲨 | 远洋 |

| 石鱼 | 潮间带 |

| 非危险动物 | |

| 带纹鱼 | 海岸区域 |

| 鲞鱼 | 远洋 |

| 刺背鱼 | 海湾和河口 |

| 无脊椎动物 | |

| 危险动物 | |

| 海蜂 | 海岸海床 |

| 非危险动物 | |

| 金丝星 | 码头、潮池 |

| 海扇 | 海岸海床 |

| 太平洋章鱼 | 潮池、潮汐区 |

| 海胆 | | |

| 哺乳动物 | |

| 危险动物 | |

| 虎海豚 | 远洋、海湾 |

## 设置展开器样式

展开器（expander）是父节点左侧的图形，用户可以点击它可以展开或折叠该节点。展开器还提供视觉反馈，让用户知道节点的展开或折叠状态。你可以通过 `gtk_ctree_set_expander_style()` 展开器样式：

```c
void
gtk_ctree_set_expander_style(GtkTree *ctree,
nGTreeExpanderStyle expander_style);
```

参数 `expander_style` 可以表 12.8 中列出的图形之一。

表 12.8 GtkreeExpanderStyle

| 展开器样式 | 结果 |

| :--- | :--- |

| GTK_CTREE_EXPANDER_NONE | 不绘制展开器。 |

| GTK_CTREE_EXPANDER_SQUARE | 默认展开器（见前图）。 |

表 12.8 GtkTreeExpanderStyle（续）

| 展开器样式 | 结果 |

| :--- | :--- |

| GTK_CTREE_EXPANDER_TRIANGLE | 参见图 12.14. |

| GTK_CTREE_EXPANDER_CIRCULAR | 参见图 12.15. |

GtkTree 示例 | GtkTree 示例

| 动物 | 栖地 |

| :--- | :--- |

| 鱼类 | |

| 危险动物 | |

| 大白鲨 | 远洋 |

| L... | 潮间带 | |

| 非危险动物 | | |

| 带纹鱼 | 海岸区域 | |

| 鲞鱼 | 远洋 |

| 豹纹鱼 | 海湾和河口 |

| 刺背鱼 | 海岸区域、沙滩 |

| 无脊椎动物 | |

| 危险动物 | |

| 海蜂 | 海岸海床 |

| 非危险动物 | |

| 金丝星 | 码头、潮池 |

| 海扇 | 海岸海床 |

| 太平洋章鱼 | 潮池、潮汐区 |

| 海胆 | 海藻丛 |

| 哺乳动物 | |

| 危险动物 | |

| 虎海豚 | 远洋、海湾 |

| 非危险动物 | |

| 灰鲸 | 远洋 |

| 海海员 | 潮汐区、海藻丛 |

| 瓶颈海豚 | 远洋、浅滩 |

图 12.14 GTK_CTREE_EXPANDER_TRIANGLE

图 12.15 GTK_CTREE_EXPANDER_CIRCULAR

## 排序函数

以下函数执行树排序。这里讨论的第一个函数允许你指定比较函数，该函数将在拖放操作期间的默认比较函数中使用（应开启拖拽并启用；请参考之前对 `gtk_clist_insert_node()` 第六个参数的讨论）。`gtk_ctree_drag_compare_func()` 取两个参数：一个 `GtkTree` 实例和一个函数指针。

```c
void
gtk_ctree_drag_compare_func(GtkTree *tree,
    GtkTreeCompareDragFunc *cmp);
```

`comp_func` 的函数原型由 `GtkTreeCompareDragFunc` 定义：

```
typedef gboolean (*GtkTreeCompareDragFunc)(GtkTree *ctree,
                                            GtkTreeNode *source_node, GtkTreeNode *new_parent,
                                            GtkTreeNode *new_sibling);
```

您的拖放比较函数应该使用传入的参数来确定是否允许或拒绝拖放操作。参数 `source_node` 指定了正在移动的节点；如果允许调整顺序，则 `new_parent` 指定了 `source_node` 的新父节点；如果允许拖放操作，则 `new_sibling` 指定了 `source_node` 的兄弟节点。如果您想拒绝该操作，您的拖放比较函数应返回 `FALSE`。返回 `TRUE` 将导致执行拖放操作。

您可以使用 `GtkTree` 实例来自动对 `ctree` 进行排序（即 `GList auto_sort`）。这是通过调用 `gtk_list_set_auto_sort()` 实现的。关于 `GtkTree` 实例的额外 `GtkList` 排序函数，请见第 6 章。

如果您选择禁用 `GtkList-set-autosorting`，您仍然可以通过调用 `GtkTree` 定义的两个函数为用户提供排序功能。第一个函数 `gtk_tree_sort_node()` 排序树中特定节点的直接子节点。其函数原型如下：

```
void
gtk_tree_sort_node(GtkTree *ctree, GtkTreeNode *node);
```

顺序由最后一次调用 `gtk_list_set_sort_type()` 定义，或者如果没有进行此类调用，则使用 `GTK_SORT_ASCENDING`。比较规则由最后一次调用 `gtk_list_set_compare_func()` 设置，该函数将取代 `gtklist.c` 中定义的默认函数（`default_compare`）。

若要将排序递归扩展到给定节点以下的所有子节点，可以调用 `gtk_tree_sort_recursive()`：

```
void
gtk_tree_sort_recursive(GtkTree *ctree, GtkTreeNode *node);
```

上述针对 `gtk_tree_sort_node()` 的说明同样适用于 `gtk_tree_sort_recursive()`。

## 递归函数

在本节中，我将描述本质上是递归的 `GtkTree` 函数。这些函数允许您为树中的每个节点调用应用程序中的回调函数，查找应用程序附加到某个节点或一组节点上的数据，并查询树控件关于其所管理的节点的某些属性。

所描述的前四个函数允许您从指定的节点开始遍历树。对于树中的每个节点，`GtkTree` 都会调用由您提供的回调函数。您提供的回调函数必须符合以下函数原型：

```
typedef void (*GtkCTreeFunc) (GtkCTree *ctree, GtkCTreeNode *node,
gpointer data);
```

在上述函数原型中，`node` 指定了正在访问的节点，而 `data` 是您的应用程序需要传递给回调函数的客户端数据。

第一个函数 `gtk_ctree_post_recursive()` 从特定节点开始对树进行后序遍历：

```
void
gtk_ctree_post_recursive(GtkCTree *ctree, GtkCTreeNode *node,
gtkCTreeFunc func, gpointer data);
```

参数是待遍历的 `GtkCTree` 实例，`data` 是遍历的起始节点，`func` 是每个每个遍历的节点时被调用的函数，`data` 是将通过其参数 `data` 传递给 `func` 的客户端数据。

函数 `gtk_ctree_post_recursive_to_depth()` 与 `gtk_ctree_post_recursive()` 相同，不同在于 `depth` 参数将遍历限制在特定的深度：

```
void
gtk_ctree_post_recursive_to_depth(GtkCTree *ctree, GtkCTreeNode *node,
int depth, GtkCTreeFunc func, gpointer data);
```

如果 `depth` 为 -1，则遍历整个树。如果 `depth` 为 0，则只访问第一个（根）节点。指定深度为 1 将访问根节点及其直接子节点，依此类推。

最后两个递归函数 `gtk_ctree_pre_recursive()`：

```
void
gtk_ctree_pre_recursive(GtkCTree *ctree, GtkCTreeNode *node,
gtkCTreeFunc func, gpointer data);
```

以及 `gtk_ctree_pre_recursive_to_depth()`：

```
void
gtk_ctree_pre_recursive_to_depth(GtkCTree *ctree, GtkCTreeNode *node,
int depth, GtkCTreeFunc func, gpointer data);
```

在功能上与 `gtk_ctree_post_recursive()` 和 `gtk_ctree_pre_recursive_to_depth()` 镜像。区别在于后两个函数按前序遍历树，而不是后序（关于后序和遍历顺序的更多信息，请参阅数据结构的书籍）。

将客户端数据传递给遍历函数。我应该给您一个提示，说明为什么向递归遍历函数传递客户端数据可能是很有用的。没有固定的规则规定何时传递或不向遍历函数传递数据。这完全取决于您作为开发者，如何以任何符合您应用程序逻辑的方式来利用遍历。为了让您思考可能如何在您的应用程序中使用此功能，我编写了一段示例代码，该代码遍历了一个地址通讯录数据树，并将每个区号为 123 的电话号码更改为 456。我使用遍历函数检查树中的每个节点，并仅转换匹配的项。为了使示例简单，区号存储在单独的列中，与电话号码的其他部分隔开。

由 `MakeAddressTree()` 创建的树被主程序添加到垂直框控件（vertical box widget）中，“将 123 替换为 456”按钮也是如此。点击信号函数 `ChangeAreaCode()` 已被注册到按钮控件上。

在第 026 行，初始化了一个 `Area` 类型的变量，用于在遍历过程中（i）存储要搜索的区域以及替换后的区域（code）。在第 029 行，调用了 `gtk_tree_post_recursive()` 来遍历树。`gtk_tree_post_recursive()` 的调用封装在 `gtk_list_freeze()` 和 `gtk_list_thaw()` 调用之间，以强制 `GtkTreeList` 推迟重绘，直到遍历完成。

遍历回调函数 `CallbackFunc()` 接收了正在遍历的树的引用（`tree`）、正在访问的节点（`node`）以及持有搜索参数的 `Area` 数据结构（`data`）。调用了 `GtkTree` 函数 `gtk_tree_node_get_text()` 来提取存储在第 2 列（区号）中的数据。在第 015 行，我将从节点中读取的搜索区号值与回调函数进行比较。如果找到匹配，我通过调用 `gtk_tree_node_set_text()`（第 016 行）将值替换为新的区号。

```
015    if ( strcmp(text, area->in) )
016        gtk_tree_node_set_text(ctree, node, 1, area->out);
```

我将在本节稍后的部分详细描述 `gtk_tree_node_get_text()` 和 `gtk_tree_node_set_text()`。

## 查询树和节点属性

接下来的几个函数可以用于查询 `GtkTree` 实例及其包含的节点的属性。首个函数 `gtk_tree_is_viewable()` 可用于判断树中的某个节点是否可见：

```
boolean
gtk_tree_is_viewable(GtkTree *ctree, GtkTreeNode *node);
```

参数 `tree` 是一个 `GtkTree` 实例。参数 `node` 是一个 `GtkTreeNode` 实例，指定了感兴趣的节点。如果该节点的每个祖先都已展开，则返回 TRUE；否则返回 FALSE。

如果指定的节点是树中指定节点的兄弟或子节点，以下函数将返回 TRUE：

```
boolean
gtk_tree_find(GtkTree *ctree, GtkTreeNode *node,
    GtkTreeNode **child);
```

同样地，如果指定的节点是指定子节点的祖先，`gtk_tree_is_ancestor()` 将返回 TRUE：

```
boolean
gtk_tree_is_ancestor(GtkTree *ctree, GtkTreeNode *node,
    GtkTreeNode *child);
```

## 附加和检索客户端数据

在查看下一组搜索函数之前，我需要描述你如何将客户端数据附加到节点上。要实现这一点，你可以调用两个函数之一：`gtk_ctree_node_set_row_data()`：

```
void
gtk_ctree_node_set_row_data(GtkCtree *ctree, GtkCTreeNode *node,
 gpointer data);
```

或者 `gtk_ctree_node_set_row_data_full()`：

```
void
gtk_ctree_node_set_row_data_full(GtkCtree *ctree, GtkCTreeNode *node,
 gpointer data, GtkDestroyNotify destroy);
```

这两个函数共享前三个参数。参数 `tree` 是一个 `GtkCtree` 实例，`node` 是代表树中节点的 `GtkCTreeNode` 实例，而 `data` 是你的客户端想要附加的任意数据。`gtk_ctree_node_set_row_data_full()` 接受一个额外的参数。调用 `gtk_ctree_node_set_row_data()` 等同于调用 `gtk_ctree_node_set_row_data_full()` 并将 `node` 设置为 `NULL`。如果非 `NULL`，则必须是一个指向符合以下函数原型的指针：

```
typedef void (*GtkDestroyNotify) (gpointer data);
```

当数据所在的行或节点被销毁时，`GtkCtree` 将通过注册表调用你。你可以通过上述两个函数中的任一个注册它，它将作为唯一参数传递给销毁函数。

客户端数据的典型用法是直接向节点附加一个指向数据结构或内存位置的指针，该位置持有由节点显示的数据。这使得你可以在任何需要的时候访问这些数据，例如从之前提到的某一个递归函数的文中。要从特定节点检索客户端数据，你可以调用 `gtk_ctree_node_get_row_data()`：

```
gpointer
gtk_ctree_node_get_row_data(GtkCtree *ctree, GtkCTreeNode *node);
```

返回值是由 `gtk_ctree_node_set_row_data_full()` 或 `gtk_ctree_node_set_row_data()` 添加的 `gpointer`。

## 基于客户端数据搜索节点

`GtkCtree` 将向你返回树中所有（从你指定的节点开始）具有匹配特定值数据的节点列表。要获取此列表，请调用 `gtk_ctree_find_all_by_row_data()`：

- LIST

`gtk_ctree_find_all_by_row_data(GtkCtree *ctree, GtkCTreeNode *node, gpointer data);`

参数 `tree` 是要搜索的树，`node` 是起始节点（`NULL` 会导致搜索整个树），参数 `data` 是要搜索的数据。以下代码是示例程序的修改：

### 列表 12.6 基于客户端数据搜索
