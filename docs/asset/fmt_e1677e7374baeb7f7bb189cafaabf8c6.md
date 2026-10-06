
### 类描述

GtkClist 的主要用途与 `GtkList` 类似，用于显示一组组织成列表的文本字符串，用户可以从中进行选择。之前描述过的 `GtkList` 允许用户使用四种不同的选择模式选择项目：单选、浏览、多选和扩展。`GtkClist` 支持完全相同的选择模式。

除了项目选择外，`GtkClist` 还提供了额外功能；我们提供给用户的两个功能是：

- 根据任意排序标准对行进行排序
- 将行中的数据组织为一系列可调整的列

尽管我会涵盖 `GtkClist` 暴露 API，但我将倾向于关注 API 中涉及列管理和数据排序的函数。

### 示例

![](img/b9af04aaed46302cb075052312fcd667_250_0.png)

| 姓名 | 出生日期 | 出生地 |
|---|---|---|
| Fred Jaspers | 05/12/1970 | Miami, FL |
| Sam Jones | 04/12/1972 | Bakersfield, CA |
| Jim Edwards | 02/17/1984 | Phoenix, AZ |
| Quit | | |

图 6.5 GtkClist 示例

让我们从使用基本函数创建并显示类似图 6.5 所示的列表开始。关于图 6.5 有几点需要注意。首先，这是一个三列 clist，第一列显示人的姓名，第二列显示该人的出生日期，第三列显示出生地。在 clist 中，列从左到右编号，从 0 开始到 `$n-1$` 结束，其中 $n$ 是 clist 中的列数。行的编号类似于 `GtkList`，最顶部的行分配为 0，最后一行分配为 `$m-1$`，其中 $m$ 是表格中的行数。在数据上方，即 clist 的最顶部，有一个标题区域，显示分配给 clist 中每列的标题。这实际上是一个标题，如果你的程序需要，它可以被激活并附加到点击的信号函数上，当用户点击标题时将触发该函数。默认情况下，用户可以通过将指针悬停在分离一对标题按钮的边界上，点击左鼠标键并拖动列边界到新位置，来更改表格中列的宽度。你的程序可以控制列的各种属性，包括它们的最小和最大宽度，以及单个列是否可以由用户调整大小。

与 `GtkList` 一样，你的程序可以在运行时从 clist 中添加或删除行。clist 静态属性是每行拥有的列数，这必须在创建 clist 时指定。

## 创建 Clist 小部件

要创建一个 clist，你的应用程序调用以下函数之一：`gtk_clist_new()` 或 `gtk_clist_new_with_titles()`。以下是这两个函数的原型：

```
GtkWidget *
gtk_clist_new(gint columns);
```

```
GtkWidget *
gtk_clist_new_with_titles(gint columns, gchar *titles[]);
```

第一个函数 `gtk_clist_new()` 创建一个不具有列标题集的 `GtkClist` 实例。然而，请注意，如果没有列标题，`GtkClist` 将无法正确显示你添加到 clist 中的内容，除非你显式地设置列表列的宽度。这是因为默认情况下，`GtkClist` 会根据字符串的长度调整列的大小，而不是根据单元格中显示的内容。为了让单元格（以及列）根据内容调整大小，`gtk_clist_set_column_auto_resize()` 将确保列的大小与其内容恰当。我将在本节稍后的部分更详细地讨论列的大小调整。

第二个 `GtkClist` 实例例程是 `gtk_clist_new_with_titles()`。它接受一个额外的参数，即 `char *` 向量。参数中的每个 C 字符串都用作列标题。第 1 列的标题包含在 `titles[0]` 中，第 2 列的标题包含在 `titles[1]` 中，依此类推。如前所述，列的默认宽度基于列标题文本的宽度。

以下代码创建一个 `GtkClist` 实例并设置列标题，以反映将由 clist 管理的姓名、出生日期和出生地数据：

```c
GtkWidget *dialog_window, *hbox, *list;
static char *titles[] =
{
    "Name",
    "Date of Birth",
    "Birth Location",
};
gtk_init(&argc, &argv);
gtk_window_new();
hbox = gtk_box_new(GTK_ORIENTATION_HORIZONTAL, 0);
gtk_container_add(GTK_CONTAINER(dialog_window), hbox);
list = gtk_clist_new_with_titles(3, titles);
gtk_container_add(GTK_CONTAINER(hbox), list);
gtk_widget_show_all(list);
```

第一个函数 `gtk_clist_new()` 创建一个不带列标题集的 `GtkClist` 实例。但请注意，如果没有列标题，除非你显式设置列表列的宽度，否则 `GtkClist` 将无法正确显示你添加到 clist 中的内容。这是因为默认情况下，`GtkClist` 根据字符串的长度调整列的大小，而不是根据单元格中显示的内容。为了让单元格（以及列）根据内容调整大小，`gtk_clist_set_column_auto_resize()` 将确保列的大小与其内容相匹配。我将在本节稍后的部分更详细地讨论列的大小调整。

第二个 `GtkClist` 实例函数是 `gtk_clist_new_with_titles()`。它接受一个额外的参数，即 `char *` 向量。参数中的每个 C 字符串都用作列标题。第 1 列的标题包含在 `titles[0]` 中，第 2 列的标题包含在 `titles[1]` 中，依此类推。如前所述，列的默认宽度基于列标题文本的宽度。

以下代码创建一个 `GtkClist` 实例并设置列标题，以反映将由 clist 管理的姓名、出生日期和出生地数据：

```c
GtkWidget *dialog_window, *hbox, *list;
static char *titles[] =
{
    "Name",
    "Date of Birth",
    "Birth Location",
};
gtk_init(&argc, &argv);
gtk_window_new();
hbox = gtk_box_new(GTK_ORIENTATION_HORIZONTAL, 0);
gtk_container_add(GTK_CONTAINER(dialog_window), hbox);
list = gtk_clist_new_with_titles(3, titles);
gtk_container_add(GTK_CONTAINER(hbox), list);
gtk_widget_show_all(list);
```
