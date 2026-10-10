
`selection_changed` (`GtkTree` *tree, `gpointer` `user_data`);

`void`

`select_child` (`GtkTree` *tree, `GtkWidget` *widget, `gpointer` `user_data`);

`void`

`unselect_child` (`GtkTree` *tree, `GtkWidget` *widget, `gpointer` `user_data`);

### 应用层级 API 摘要

在运行时返回常量 `GTK_TYPE_TREE`：
```c
GtkType
gtk_tree_get_type(void);
```

创建一个 `GtkTree` 的新实例：
```c
GtkWidget *
gtk_tree_new(void);
```

向子树追加一个 `GtkTreeItem` 实例：
```c
void
gtk_tree_append(GtkTree *tree, GtkWidget *tree_item);
```

向子树头部添加一个 `GtkTreeItem` 实例：
```c
void
gtk_tree_prepend(GtkTree *tree, GtkWidget *tree_item);
```

向子树中插入一个 `GtkTreeItem` 实例：
```c
void
gtk_tree_insert(GtkTree *tree, GtkWidget *tree_item, gint position);
```

从树中移除项：
```c
void
gtk_tree_remove_items(GtkTree *tree, GList *items);
```

从子树中移除范围内的项：
```c
void
gtk_tree_clear_items(GtkTree *tree, gint start, gint end);
```

在子树中选择一个项：
```c
void
gtk_tree_select_item(GtkTree *tree, gint item);
```

在子树中取消选择一个项：
```c
void
gtk_tree_unselect_item(GtkTree *tree, gint item);
```

### 应用层 API 摘要（续）

选择对应于指定树组件的项：
```c
void
gtk_tree_select_child(GtkTree *tree, GtkWidget *tree_item);
```

取消选择对应于指定树组件的项：
```c
void
gtk_tree_unselect_child(GtkTree *tree, GtkWidget *tree_item);
```

确定子树中节点的位置：
```c
gint
gtk_tree_child_position(GtkTree *tree, GtkWidget *child);
```

指定树的选择模式：
```c
void
gtk_tree_set_selection_mode(GtkTree *tree, GtkSelectionMode mode);
```

指定树视图模式：
```c
void
gtk_tree_set_view_mode(GtkTree *tree, GtkTreeView mode);
```

指定树线是否可见：
```c
void
gtk_tree_set_lines(GtkTree *tree, gboolean flag);
```

## 类描述

后续章节中，我们将描述如何创建 `GtkTree` 实例，以及如何从树中添加和移除项。我们将探讨与树选择相关的问题。我描述 `GtkTree` 支持的各种模式以及支持这些模式的 `GtkTree` API 函数。

#### 创建 GtkTree 实例

通过调用 `gtk_tree_new()` 创建 `GtkTree` 实例：
```c
GtkWidget *
gtk_tree_new(void);
```
返回的树可以被应用程序用树的根节点，或者通过附加将其添加到现有树作为子树。树的概述及其构造在本章开头提供；树项将在 `GtkTreeItem` 章节中描述。

#### 添加项

一旦你创建了 `GtkTree`，`GtkTreeItem` 章节将讨论如何创建树项。一旦创建，可以通过调用以下函数之一 `gtk_tree_append()`、`gtk_tree_prepend()` 或 `gtk_tree_insert()` 将树项添加到树中。

树由树项组成。每个树项由一个索引管理，该索引决定其相对于树中其他树项的位置。树项索引必须在 `[0, n-1]` 范围内，其中 `n` 是容器树中树项的数量。索引为 `n-1` 的树项比索引为 `n` 的树项更高（更靠近顶部）；索引为 0 的树项将显示在树的顶部，而索引为 `n-1` 的树项将显示在树的底部。

向树添加树项，调用 `gtk_tree_append()`：
```c
void
gtk_tree_append(GtkTree *tree, GtkWidget *tree_item);
```
参数是正在添加树项的 `GtkTree` 实例。索引是 `n`，即追加操作之前树中树项的数量。

要向树头部添加（添加到树的顶部）`GtkTreeItem` 实例，你可以调用 `gtk_tree_prepend()`：
```c
void
gtk_tree_prepend(GtkTree *tree, GtkWidget *tree_item);
```
传递给 `gtk_tree_prepend()` 的参数与传递给 `gtk_tree_append()` 的相同。通过 `gtk_tree_prepend()` 添加的树项将成为其所在树的最顶部子节点（即其索引为 0）。由于此调用，树中剩余每个树项的索引都会增加 1。

最后，你可以通过调用 `gtk_tree_insert()` 在特定位置向子树插入 `GtkTreeItem` 实例：
```c
void
gtk_tree_insert(GtkTree *tree, GtkWidget *tree_item, gint position);
```
两个参数与传递给 `gtk_tree_append()` 和 `gtk_tree_prepend()` 的相同。最后一个参数无歧地指定了在 `gtk_tree_insert()` 返回后，树项相对于树所包含的其他树项的位置。将 `position` 设置为 0 将允许调用 `gtk_tree_prepend()`，而在 `gtk_tree_insert()` 中将 `position` 设置为 -1 的行为等同于调用了 `gtk_tree_append()`。传递一个在 `[0, n-1]` 范围内的位置参数 `m` 会导致树项位于位置 `m`。

# 604 第 12 章 • 树

你可能也想自己维护一个树项列表，跳过调用 `GTK_TREE_SELECTION`。如果用户提供的不是前一个示例中的“删除”按钮，而是一个代表抽象操作（例如“删除所有被认为对人类危险的项”）的控件，那么这可能非常有用。为了实现此类功能，你的应用程序需要将 `GtkTreeItemId` 实例与这些树项代表的应用程序数据进行映射。举个简单的例子：

```c
// 存储动物名称、其对人类
// 危险程度的指示以及代表树中动物的
// GtkTreeItemId 实例的结构体
```

```c
typedef struct animal {
    gchar name [MAXNAME]; // 例如：大白鲨
    gboolean isDangerous; // 在这种情况下，为 TRUE
    GtkWidget *treeItem; // 持有相关的树项
} Animal;
```

```c
// 声明一个动物数组
```

```c
Animal myAnimals[] = {
    {"Great White Shark", TRUE, 0 },
    {"Grunion", FALSE, 0 }
};
```

```c
// 为每个动物创建树项，并将生成的
// 控件存储在 treeItem 字段中
```

```c
for ( i = 0; i < sizeof(myAnimals ) / sizeof( Animal ); i++ )
    myAnimals[i].treeItem =
        gtk_tree_item_new_with_label(
            ( myAnimals[i].name );
```

以下例程可以遍历 `Animals` 数据结构，根据它们对人类的危险程度创建一个动物的 `GList`，该列表可以传递给 `gtk_tree_remove_items()` 以从树中移除：

```c
GList *
GetAnimalsOfType( gboolean isDangerous )
{
    GList *list = NULL;
    int i;
```
