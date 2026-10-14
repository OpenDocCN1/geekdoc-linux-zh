
这两个函数都返回布尔值，当它们成功将 `iter` 指向与路径对应的节点时返回 `TRUE`。唯一的区别在于路径的指定方式：`path` 是一个 `GtkTreePath` 结构体，而 `path_string` 是一个用冒号分隔的路径字符串。

自然地，`gtk_tree_model_get_iter_from_string()` 是一个便利函数，但它仍然可以节省你三行代码：树的声明、它的初始化以及返回内存池。这里是更多 `GtkTreeIter` 函数：

- `gboolean gtk_tree_model_get_iter_first(GtkTreeModel *model, GtkTreeIter *iter)`
  将 `iter` 设置为模型中的第一个节点（即具有路径的节点）。如果模型为空，此函数返回 `FALSE`。
- `gboolean gtk_tree_model_get_iter_next(GtkTreeModel *model, GtkTreeIter *iter)`
  将 `iter` 指向模型中的下一个兄弟节点。如果它是最后一个兄弟节点，此函数返回 `FALSE`。
- `gboolean gtk_tree_model_iter_children(GtkTreeModel *model, GtkTreeIter *iter, GtkTreeIter *parent)`
  将 `iter` 指向 `parent` 的第一个孩子。如果没有孩子，此函数返回 `FALSE`。
- `gboolean gtk_tree_model_iter_nth_child(GtkTreeModel *model, GtkTreeIter *iter, GtkTreeIter *parent, guint n)`
  将 `iter` 指向 `parent` 的第 `n` 个子节点。如果 `parent` 为 `NULL`，此函数指向顶层级第 `n` 个节点。
- `gboolean gtk_tree_model_iter_has_child(GtkTreeModel *model, GtkTreeIter *iter)`
  如果 `iter` 处的节点有孩子，则返回 `TRUE`。
- `gint gtk_tree_model_iter_n_children(GtkTreeModel *model, GtkTreeIter *iter)`
  返回 `iter` 的子数量。如果你对 `iter` 指定 `NULL`，此函数返回顶层节点的数量。
- `gboolean gtk_tree_model_iter_parent(GtkTreeModel *model, GtkTreeIter *iter)`
  将 `iter` 指向其父节点。如果无法实现，此函数返回 `FALSE`。

移除或修改模型中的节点会使模型的所有迭代器失效（例如，在信号触发时）。如果你需要稍微的稳定性，可以使用引用计数的对象。它们的类是 `GtkRowReference`，这是一种无论信号如何都可以使用的弱引用。你可能使用这些引用的一种情况是在节点上做标记，只要节点存在，标记就有效。

- `GtkRowReference *gtk_tree_row_reference_new(GtkTreeModel *model, GtkTreePath *path)`
  返回给定 `path` 给出的模型中行（节点）的新引用。如果没有该节点，此函数返回 `NULL`。

### 3.1.1 列表与树 API

- `GtkPath *gtk_tree_row_reference_get_path(GtkRowReference *ref)`
  返回对应于树中 `ref` 节点的新路径，如果引用无效，则返回 `NULL`。
- `boolean gtk_tree_row_reference_valid(GtkRowReference *ref)`
- `void gtk_tree_row_reference_free(GtkRowReference *ref)`
  移除行引用。

### 3.11.2 树视图

`GtkTreeView` 实现了 MVC 中的 V（视图）。你可以为单个模型拥有尽可能多的视图；实际的视图显示通过查询模型（视为数据库）与模型分离的。

列和单元渲染器负责查询和格式化数据的实际工作。因此，`GtkTreeView` 的函数和属性主要涉及视图的外观和用户界面（某些可渲染属性除外）。

- `void gtk_tree_view_scroll_to_cell(GtkTreeView *view, GtkTreePath *path, GtkTreeViewColumn *column, boolean align, gfloat row_align, gfloat col_align)`
  滚动到 `path` 和 `column` 给出的单元。如果你只需要水平或垂直滚动，这两个参数中的一个可以为 `NULL`。如果你想控制视图的显示方式，将 tree 设置为 0.0 到 1.0 之间的数字（0.0 为左或顶部，0.5 为中间，1.0 为右或底部）。
- `void gtk_tree_view_set_cursor(GtkTreeView *view, GtkTreePath *path, GtkTreeViewColumn *column, boolean start_editing)`
  将焦点移动到 `path` 给出的单元（且 `column` 非 `NULL`）并选择该单元。如果你将 `start_editing` 设置为 `TRUE`，GTK+ 将打开单元供编辑。
- `void gtk_tree_view_get_cursor(GtkTreeView *view, GtkTreePath **path, GtkTreeViewColumn **column)`
  获取光标位置并将 `path` 和 `column` 指针设置为相应的行和列。如果没有选中，此函数将 `column` 设置为 `NULL`。如果没有选择，两个都为 `NULL`。
- `void gtk_tree_view_row_activated(GtkTreeView *view, GtkTreePath *path, GtkTreeViewColumn *column)`
  激活 `path` 和 `column` 给出的行或视图（例如，双击行或单元即构成一种操作）。
- `void gtk_tree_view_expand_all(GtkTreeView *view)`
  完全展开视图；否则，此函数展开显示的所有行。
- `void gtk_tree_view_collapse_all(GtkTreeView *view)`
- `gboolean gtk_tree_view_expand_row(GtkTreeView *view, GtkTreePath *path, gboolean recursive)`
  展开对应于 `path` 的行。如果 `recursive` 为 `TRUE`，则展开 `path` 处的整个子树。此函数如果展开了行返回 `TRUE`。
- `gboolean gtk_tree_view_collapse_row(GtkTreeView *view, GtkTreePath *path)`
  折叠 `path` 处的行，如果成功返回 `TRUE`。
- `gboolean gtk_tree_view_row_expanded(GtkTreeView *view, GtkTreePath *path)`
  如果视图中的 `path` 目前处于展开状态，返回 `TRUE`。

`GtkTreeView` 有以下属性：

- `model` (`GtkTreeModel`): 视图内部当前的模型。
- `adjustment` (`GtkAdjustment`): 水平滚动方向的调整对象。
- `vadjust` (`GtkAdjustment`): 垂直滚动方向的调整对象。
- `headers-visible` (`gboolean`): 如果为 `TRUE`，标题出现在列顶部。
- `headers-clickable` (`gboolean`): 如果为 `TRUE`，用户可以点击标题（更改排序）。
- `expander-column` (`GtkTreeViewColumn`): 显示箭头的列。默认是第一列。
- `reorderable` (`gboolean`): 如果为 `TRUE`，用户可以通过将行拖到视图中的不同位置来重新排序。注意这仅适用于实现了 `GtkDragSource` 和 `GtkDragDest` 接口的模型（如 `GtkListStore` 和 `GtkTreeStore`）。如果你激活了 `reorderable`，你可以任意操作行。否则，你必须提供自己的拖放机制（一项复杂的任务）。
- `rules–init` (`gboolean`): 如果为 `TRUE`，视图将采用格式并从视觉增强中受益。此属性直接影响视图的外观；由主题决定做什么。因此，如果你想要特定的特征（如条纹列表），不要将其设置为 `TRUE`；主题不需要执行任何细节。
- `enable–search` (`gboolean`): 如果为 `TRUE`，用户可以在其中列上执行交互式搜索（按下 `CTRL–F`）（见下文）。
- `search–column` (`int`): 用户可以执行交互式搜索的列。

`GtkTreeView` 有一个重要的信号 `row–activated`，当用户通过双击或键盘操作激活单元时，该信号会触发。它的原型如下，`path` 和 `column` 设置为相应的行和单元：
