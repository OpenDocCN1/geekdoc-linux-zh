
```c
struct GtkCellText
{
GtkCellType type;
int16 vertical;
int16 horizontal;
GtkStyle *style;
};

struct GtkCellPixmap
{
GtkCellType type;
int16 vertical;
int16 horizontal;
GtkStyle *style;
};

struct GtkCellPixText
{
GtkCellType type;
int16 vertical;
int16 horizontal;
GtkStyle *style;
};
```

## 使用列表

其参数如下：

| 参数 | 描述 |
| :--- | :--- |
| `clist` | 指向当前排序的 `GtkClipList` 的指针。 |
| `row1` | 指向比较中第一行的 `GtkListRow` 结构体的指针。 |
| `row2` | 指向比较中第二行的 `GtkListRow` 结构体的指针。 |

此回调函数在行相等时应返回 `0`，当 `row1` 小于 `row2` 时返回负整数，当 `row1` 大于 `row2` 时返回正整数。

比较的实际实现可以非常多样化，并根据任何可能的条件确定等等性和优先级。如果只将行作为 `GtkListCompareFunc` 回调函数的参数提供，则必须通过访问 `GtkClip` 结构中的 `sort_column` 索引成员来获取排序后的列。

`gtk_clist_sort()` 执行实际排序，其原型下所示：

```c
void gtk_clist_sort(GtkClipList *clist);
```

`gtk_clist_sort()` 的参数为：

| 参数 | 描述 |
| :--- | :--- |
| `clist` | 指向将排序的 `GtkClipList` 的指针。 |

如果 `GtkClipList` 在内容每次变化时都要自动排序，可以使用 `gtk_clist_set_auto_sort()` 函数来开启此功能。其完整原型如下：

```c
void gtk_clist_set_auto_sort(GtkClipList *clist, boolean auto_sort);
```

`gtk_clist_set_auto_sort()` 的参数为：

| 参数 | 描述 |
| :--- | :--- |
| `clist` | 指向函数将操作的 `GtkClipList` 的指针。 |
| `auto sort` | 布尔值，表示是否应自动对 `GtkClipList` 进行排序。 |

以下是一个 `GtkClipListCompareFunc` 回调函数的示例，它允许使用 `strcmp()` 对带有文本内容的行进行排序。

```c
gint row_stromp(GtkClipList *clist, GtkClipRow *row1, GtkClipRow *row2)
{
    gchar *string1 = ((GtkCellText*))(row1->cell[clist->sort_column]))->text;
    gchar *string2 = ((GtkCellText*))(&(row2->cell[clist->sort_column]))->text;

    return strcmp(string1, string2);
}
```

![](img/7fa9959a9d28ad339fa75e44952feeb9_422_0.png)

## 阐述涵盖 GtkList 功能的示例

本节讨论的所有功能都在一个演示程序中进行了说明，该程序可以从 `http://www.sampublishing.com` 网站下载。

此示例创建了一个 `GtkWindow`，其中包含两个主要区域：一个带有三列 `GtkList` 的 `GtkScrolledWindow` 以及一个包含六个 `GtkButton` 控件的 `GtkTable`。底部有一个 `GtkStatusBar`，用于提供最后执行操作的信息。

在启动时，`GtkList` 填充了 100 行。在这些这些行之前，`GtkList` 处于被冻结状态。当 `GtkList` 填充完成后，它会被解冻。此后每个新行都会被创建并填充内容。由于行的 id 将在之后用于在状态栏中提供反馈，因此它作为可选数据存储在每个新行中。新行的第一列包含一个 GTK+ 标志的小型位图（pixmap）和一些标识其创建 id 的文本。该位图及其掩码在程序启动时从 xpm 数据创建并存储在全局指针中。新行的第二列和第三列填充了随机数。任何 id 为 5 的倍数的行其背景都被设置为浅灰色。第一列的样式：第一列在未选中时背景为浅灰色，选中时背景为深绿色。对于本节中所涵盖的 GtkList 功能，所有功能都在一个演示程序中进行了说明，该程序可以从 `http://www.sampublishing.com` 网站下载。

此示例创建了一个 `GtkWindow`，其中包含两个主要区域：一个带有三列 `GtkList` 的 `GtkScrolledWindow` 以及一个包含六个 `GtkButton` 控件的 `GtkTable`。底部有一个 `GtkStatusBar`，用于提供最后执行操作的信息。

在启动时，`GtkList` 填充了 100 行。在这些行之前，`GtkList` 处于被冻结状态。当 `GtkList` 填充完成后，它会被解冻。此后每个新行都会被创建并填充内容。由于行的 id 将在之后用于在状态栏中提供反馈，因此它作为可选数据存储在每个新行中。新行的第一列包含一个 GTK+ 标志的小型位图（pixmap）和一些标识其创建 id 的文本。该位图及其掩码在程序启动时从 xpm 数据创建并存储在全局指针中。新行的第二列和第三列填充了随机数。任何 id 为 5 的倍数的行其背景都被设置为浅灰色。第一列的样式：第一列在未选中时背景为浅灰色，选中时背景为深绿色。对于本节中所涵盖的 GtkList 功能，所有功能都在一个演示程序中进行了说明，该程序可以从 `http://www.sampublishing.com` 网站下载。

此示例创建了一个 `GtkWindow`，其中包含两个主要区域：一个带有三列 `GtkList` 的 `GtkScrolledWindow` 以及一个包含六个 `GtkButton` 控件的 `GtkTable`。底部有一个 `GtkStatusBar`，用于提供最后执行操作的信息。

在启动时，`GtkList` 填充了 100 行。在这些行之前，`GtkList` 处于被冻结状态。当 `GtkList` 填充完成后，它会被解冻。此后每个新行都会被创建并填充内容。由于行的 id 将在之后用于在状态栏中提供反馈，因此它作为可选数据存储在每个新行中。新行的第一列包含一个 GTK+ 标志的小型位图（pixmap）和一些标识其创建 id 的文本。该位图及其掩码在程序启动时从 xpm 数据创建并存储在全局指针中。新行的第二列和第三列填充了随机数。任何 id 为 5 的倍数的行其背景都被设置为浅灰色。第一列的样式：第一列在未选中时背景为浅灰色，选中时背景为深绿色。对于本节中所涵盖的 GtkList 功能，所有功能都在一个演示程序中进行了说明，该程序可以从 `http://www.sampublishing.com` 网站下载。

此示例创建了一个 `GtkWindow`，其中包含两个主要区域：一个带有三列 `GtkList` 的 `GtkScrolledWindow` 以及一个包含六个 `GtkButton` 控件的 `GtkTable`。底部有一个 `GtkStatusBar`，用于提供最后执行操作的信息。

在启动时，`GtkList` 填充了 100 行。在这些行之前，`GtkList` 处于被冻结状态。当 `GtkList` 填充完成后，它会被解冻。此后每个新行都会被创建并填充内容。由于行的 id 将在之后用于在状态栏中提供反馈，因此它作为可选数据存储在每个新行中。新行的第一列包含一个 GTK+ 标志的小型位图（pixmap）和一些标识其创建 id 的文本。该位图及其掩码在程序启动时从 xpm 数据创建并存储在全局指针中。新行的第二列和第三列填充了随机数。

（省略）

图 15.7 显示了 `GtkList`。

![](img/7fa9959a9d28ad339fa75e44952feeb9_424_0.png)

## 总结

今天介绍了两个组件：`GtkList` 和 `TreeView`。你学习了它们的优缺点。诸如行数据附加、列排序和拖放等功能只有在后者才可行。`GtkList`。

## 问答

- Q: 可以使用 `GtkList` 作为内容吗？
A: 不可以这样做。

- Q: 当我选择 `GtkList` 时，它运行正常吗？
A: 目前无法保证，但在未来的版本中可能会。

- Q: 我查看了 `gtkclist.h` 头文件并注意到 `GTK_CELL_WIDGET` 单元类型。这意味着可以使用 GTK+ 控件作为单元的内容吗？
A: 不，这仅仅意味着认为应该提供这种功能。目前尚未实现。

- Q: 我该如何自己计算 `GtkList` 的最佳宽度？
