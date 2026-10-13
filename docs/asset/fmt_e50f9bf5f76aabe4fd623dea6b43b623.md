
要么将列表项引用为 `GtkListItem` 控件的指针，或者使用其在 `GtkList` 中的位置。

### 4. `Glib` 与 `GtkList` 控件之间是什么什么关系？

许多 `GtkList` 函数接受一个包含指向 `GtkListItem` 指针的 `GList` 作为其参数。

### 5. 从 `GtkList` 中删除项的两种不同方法是什么？

当 `GtkCList` 项从其列表中删除时，它可以被保留或销毁。

### 6. 焦点项（focused item）和选中项（selected items）有什么区别？

焦点项是用户最后交互的项；选中项是用户想要处理的项。

### 7. 哪种控件提供了为 `GtkList` 控件附加滚动条的方法？

`GtkScrolledWindow` 控件。

### 8. `GtkCList` 的单元包含什么内容？

文本、位图或文本和位图。

### 9. 为 `GtkList` 提供滚动条有什么区别？

`GtkScrolledWindow` 控件。

### 10. `GtkCList` 的单元包含什么内容？

文本、位图或文本和位图。

### 11. 为 `GtkList` 提供滚动条有什么区别？

`GtkScrolledWindow` 控件。

### 12. `GtkCList` 的单元包含什么内容？

文本、位图或文本和位图。

```c
gtk_clist_column_titles_show(GTK_CLIST(clist));
```

```c
gtk_clist_set_selection_mode(GTK_CLIST(clist), GTK_SELECTION_MULTIPLE);
```

### 6. 编写代码为上一个练习中的 `GtkClist` 填充 30 行数据。第一个单元格包含创建时行的行的 ID，第二个单元格包含仍需创建的行数。

代码如下：

```
gint counter = 0;
gchar *content[2];
gchar buffer1[3];
gchar buffer2[3];
```

```
content[0] = buffer1;
content[1] = buffer2;
```

```
gtk_clist_freeze(GTK_CLIST(clist));
```

```
for(counter = 0; counter < 30; counter++)
{
    sprintf(buffer1, "%d", counter);
    sprintf(buffer2, "%d", 29-counter);
```

```
gtk_clist_append(GTK_CLIST(clist), content);
```

```
gtk_clist_thaw(GTK_CLIST(clist));
```

### 7. 为上一个示例中连接到 `GtkClist` 的 `select_row_signal` 信号编写处理函数，函数名为 `select_row_handler`。将选中行两个单元格的文本打印到标准输出。

代码如下：

```
void select_row_handler(GtkClist *clist, int row, gint column, GdkEventButton *event, gpointer user_data)
{
    gchar *cell1 = NULL;
    gchar *cell2 = NULL;
```

```
    gtk_clist_get_text(clist, row, 0, &cell1);
    gtk_clist_get_text(clist, row, 1, &cell2);
```

```
    printf("cell1 = %s cell2 = %s\n", cell1, cell2);
}
```

### 8. 编写代码检查上一个练习中的 `GtkClist` 是否有焦点行。如果是，将其移动到 `GtkClist` 的底部，并移动可见区域以显示该行所在的新位置。

代码如下：

```
gint focus = -1;

focus = clist->focus_row;
if (focus != -1) {
    gtk_clist_row_move(GTK_CLIST(clist), focus,
    GTK_CLIST(clist)->rows-1;
    gtk_clist_moveto(GTK_CLIST(clist),
    GTK_CLIST(clist)->rows-1, 0, 1, 0);
}
```

## 第 16 天答案

- 1. 用正确的名称列出树结构的不同部分。

树包含项，这些项可以是叶节点也可以是节点。节点是可以可以包含子项的项。这些子项的集合被称为分支。

- 2. 可以提供什么视觉辅助手段来使 `GtkTree` 的结构更全面？

可以在节点和它的子节点之间、以及属于同一个分支的项之间画线。

- 3. `GtkTree` 的选择存储在在哪里？如何访问它？

`GtkTree` 选择存储在结构中的第一个 `GtkTree` 中。这被称为根树。可以使用 `GTK_TREE_SELECTION()` 宏进行访问。

- 4. 在什么情况下，当项被移除时，`GtkTree` 子树会被移除？

当子树不为空且其所有子项在一次调用中被移除时。

- 5. 如何通知 `GtkTreeItem` 被取消选择？

通过连接处理函数到 `select_child` 处理器。该处理器必须测试提供的 `GtkTreeItem` 是否存在于 `GtkTree` 的选择中。如果不在，则该项已被取消选择。

- 6. 在 `GtkTreeItem` 上点击鼠标中键或右键会触发什么事件？

点击中键展开节点并总是发出 `expand` 信号，而点击右键则折叠节点并总是发出 `collapsed` 信号。

- 7. `GtkTree` 中有一个特殊的列。它的功能是什么？如何称呼它？

该列用于渲染特定的树属性，例如展开/折叠符号、连接项的线条以及用于视觉化结构的的项内容缩进。它被称为树列（tree column）。

- 8. 哪些元素用于构建 `GtkTree`？如何访问它们的信息？这些元素如何与 `GtkList` 行相关？

`GtkTree` 是由 `GtkCTreeNode` 结构构建的，可以通过相应的 `GtkTreeRow` 结构访问。可以通过 `GTK_CTREE_ROW()` 宏获取。`GtkTreeRow` 只是一个扩展的 `GtkListRow` 结构，两者可以自由交换。

## 练习题

- 编写代码创建一个支持多选模式的新 `GtkTree`。确保显示勾勒结构轮廓的线条。

代码如下：

```
GtkWidget *tree = NULL;

tree = gtk_tree_new();
gtk_tree_set_selection_mode(GTK_TREE(tree), GTK_SELECTION_MULTIPLE);
gtk_tree_set_view_lines(GTK_TREE(tree), 1);
```

- 为上一个示例中的 `Gtktree` 填充十个项，这些项显示 `Root [root_id]` 作为标签，其中 `[root_id]` 是创建时项的 ID。ID 为奇数的项是叶节点，其他是节点。为节点创建一个子分支，并填充三个子项，这些子项显示 `Child [child_id]` 作为标签，其中 `[child_id]` 是创建时叶节点的 ID。

代码如下：
