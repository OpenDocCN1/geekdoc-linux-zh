
# GNOME 2 开发者指南

注意：为了让你的对话框尽可能一致且清晰，请遵循以下指南：

- 使用简短的窗口标题，不要与内容标题完全相同。
- 尽可能使用标准图标，并配合 `GTK_ICON_SIZE_DIALOG`。
- 使用以 `<big><b>...</b></big>` 开头的简短标题。
- 不要让标题过于冗长。
- 避免使用可能歧义的按钮标签，如“是”（Yes）和“否”（No）。使用动词短语（参考示例）。
- 当你设置默认按钮时（即你向用户建议该按钮可能是点击的正确选项），请将该按钮放在对话框的右下角。

最后，你应该记住，你可以将任何小部件封装在对话框的 `vbox` 中。这样你就可以对话框中请求额外数据。这通常比手动完成一切要好，因为 `GtkDialog` 会与窗口管理器和其他系统部分完成许多后台工作，使对话框的行为看起来像真正的对话框。否则，你必须手动完成这些工作——这几乎会浪费时间和精力。

## 3.11 树与列表小部件

GTK+ 对其最大且最强大的小部件使用了 MVC 概念。MVC 代表模型（model）、视图（view）和控制器（controller）；它意味着数据的内部表示（模型）、显示数据的方式（视图）以及操作视图和模型的方法（控制器）是相互相互通信的独立对象。

GTK+ 并没有严格强制这些划分。模型和视图是明确分离的，但没有特殊的控制器。你可以准确地将用于树和列表的系统称为“瑞士军刀”型小部件；它可以显示从单列列表到树结构表格的任何内容。真正的缺点是，你必须放弃一些 MVC 原教主义的想法。

你可能在用户界面中见过表示项目层级结构的列表和树。请查看第 219 页的 [图 38](#) 看看是否眼熟。本书使用了以下术语：

- 节点（node）是显示中的一行。每个节点都有一个值。
- 列表（list）是节点节点的集合。
- 树（tree）是考虑了每个节点自身的子节点的列表。
- 下拉箭头（drop arrow）展开（显示）或收叠显示中的节点节点。

树有几列；每列包含节点中的一个值。一列中的所有值类型相同，且每个节点包含的数量等于列数。

要使用列表和树，你必须从一个反映这种结构的模型开始。任何实现了 `GtkTreeModel` (`GTK_TYPE_TREE_MODEL`) 接口的类，可能都不想走到自己编写模型和接口的这一步。在大多数情况下，你会发现 GTK+ 的内置模型之一就足够了。这些是用于列表的 `GtkListStore` (`GTK_TYPE_LIST_STORE`) 和用于完整树的 `GtkTreeStore` (`GTK_TYPE_TREE_STORE`)。

你可以使用 `GtkTreeIter` 迭代器来处理列表和树。迭代器本质上是树中某一个节点的引用。你使用实用函数操作迭代器。

`GtkTreeView` (`GTK_TYPE_TREE_VIEW`) 位于组件的顶层。每一列都需要它自己的 `GtkTreeViewColumn` 对象，并且为了绘制模型中的每个值，你需要一个 `GtkCellRenderer` (`GTK_TYPE_CELL_RENDERER`) 渲染器。

为了说明这些组件是如何组合在一起的，这里有一个创建一个两列列表小部件的示例。第一列包含数字，第二列包含这些数字对应的拼写单词。

初始声明将数字拼写放在数组中，并为列定义了常量标识符：

```c
/* coding: utf-8; */

/* list.c -- demonstrate GtkTreeView */

#include <gtk/gtk.h>

const char *numbers[] = { "Zero", "One", "Two", "Three", "Four", "Five" };

enum {
    INT_COLUMN,
    STRING_COLUMN,
    N_COLUMNS
};

// 标准事件处理器 >>
```

你可以在以下代码中看到列表、视图、列和单元渲染器的声明：

```c
int main(int argc, char **argv) {
    GtkWindow *window;
    GtkListStore *list;
    GtkTreeIter iter;
    GtkTreeView *view;
    GtkTreeViewColumn *num_column, *word_column;
    GtkCellRenderer *text_renderer;
    int i;

    /* 初始化 GTK+, 创建主窗口 */
    gtk_init(&argc, argv);
    window = g_object_new(GTK_TYPE_WINDOW, "title", "Two Column List", "default-width", 300, NULL);

    // 将标准处理器连接到主窗口 >>
```

以下代码创建了列表（模型）结构；在这里你指定了列数以及每列的类型。

```c
/* 创建一个两列列表 */
list = gtk_list_store_new(N_COLUMNS, G_TYPE_INT, G_TYPE_STRING);
```

将数据加载到列表中相对容易。注意函数中的迭代器；首先使用它来获取列表新节点的句柄，然后设置节点的值。

```c
/* 向列表中存入一些数据 */
for (i = 0; i < 5; i++) {
    gtk_list_store_append(list, &iter);
    gtk_list_store_set(list, &iter, INT_COLUMN, STRING_COLUMN, numbers[i], -1);
}
```

`GtkTreeView` (`GTK_TYPE_TREE_VIEW`) 位于组件的顶层。每一列都需要它自己的 `GtkTreeViewColumn` 对象，并且为了绘制模型中的每个值，你需要一个 `GtkCellRenderer` (`GTK_TYPE_CELL_RENDERER`) 渲染器。

为了说明这些组件是如何组合在一起的，这里有一个创建一个两列列表小部件的示例。第一列包含数字，第二列包含这些数字对应的拼写单词。

（注：原文后续大量重复段落已根据要求过滤，仅保留核心逻辑翻译）

## 官方 GNOME 2 开发者指南

- 3. 设置新节点的内容，使用 `gtk_list_store_set()`（或其他函数）。注意示例，内容与列标识符成对出现，并以 -1 (NULL) 结束；这将被求值为列标识符。
- 4. 创建整体视图，这是一个 `GtkTreeView` 类的对象。
- 5. 创建你的单元渲染对象（对象）。如果你只是绘制文本，使用 `gtk_cell_renderer_text_new()` 即可。
- 6. 为每列创建一个视图对象。确保你使用了适当的单元渲染对象和列标识符。你通常使用 `gtk_tree_view_column_new_with_attributes()` 创建列视图。
- 7. 使用 `gtk_tree_view_append_column()` 将列添加到整体视图中。

### 3.11.1 列表与树 API 引用

`GtkTreeModel` 接口定义了一组方法，适用于任何实现了该接口的模型；它们大部分用于从模型中读取数据。`GtkListStore` 和 `GtkTreeStore` 有许多函数，一个用于写入和删除节点。由于这些类非常相似，一个类中的每个函数在另一个类中都有对应项。尽管参数略有不同，但你需要处理节点之间的关系；在列表中，所有节点都是单个根节点的子节点。

你可以通过观察前缀判断以下函数是否实现了 `GtkTreeModel` 接口；接口方法以 `gtk_tree_model` 开头，普通类方法以 `gtk_tree_store` 和 `gtk_list_store` 开头。

```
*GtkTree*gtk_tree_store_new(int num_columns, ...)
```

创建一个具有 `num_columns` 列的新 `GtkTree` 对象。剩余的参数是你预期的 `GValue` 类型（见第 2.4.2 节）。

```
*GtkListStore*gtk_list_store_new(int num_columns, ...)
```

与前面的函数相似，但创建一个 `GtkListStore` 对象。

```c
void gtk_tree_store_set_value(GtkTree *tree, GtkTreeIter *iterator, int column, GValue value)
```

在迭代器指定的树节点中存储一个 `GValue`。列值是一个整数列标识符。

```c
void gtk_list_store_set_value(GtkListStore *list, GtkTreeIter *iterator, int column, GValue value)
```

与前面的函数相似，但用于列表。
