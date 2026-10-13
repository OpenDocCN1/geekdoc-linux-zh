
每列的标题具有以下功能：当 `GtkClist` 标题栏被显示/隐藏时，`clist` 指向。当列被点击时，会触发 `clist_column_signal`。该信号处理函数的原型如下：

```
void column_handler(GtkClist *clist, gint column, gpointer user_data);
```

| 参数 | 说明 |
| --- | --- |
| clist | 指向被点击的 `GtkClist`。 |
| column | 被点击的列号。 |
| user_data | 传递的自定义数据。 |

在创建时未设置标题文本的新 `GtkClist` 并不知道需要显示它们。因此，应该通过 `gtk_clist_column_titles_show()` 显式显示它们。相反的函数 `gtk_clist_column_titles_hide()` 也存在，它可以隐藏列。这提供了在执行期间动态显示它们的能力。完整原型如下：

```
void gtk_clist_column_titles_show(GtkClist *clist);
void gtk_clist_column_titles_hide(GtkClist *clist);
```

| 参数 | 说明 |
| --- | --- |
| clist | 指向将显示/隐藏标题栏的 `GtkClist` 指针。 |

# 使用 GtkClist

在创建时未设置标题文本的新 `GtkClist` 并不知道需要显示它们。因此，应该通过 `gtk_clist_column_titles_show()` 显式显示它们。相反的函数 `gtk_clist_column_titles_hide()` 也存在，它可以隐藏列。这提供了在执行期间动态显示它们的能力。完整原型如下：

```
void gtk_clist_column_titles_show(GtkClist *clist);
void gtk_clist_column_titles_hide(GtkClist *clist);
```

| 参数 | 说明 |
| --- | --- |
| clist | 指向将显示/隐藏标题栏的 `GtkClist` 指针。 |

# 使用 GtkClist 宽度

每个列都有其特定的宽度，如果太小则对 GTK+ 无法感知。通过 `gtk_clist_set_column_width` 函数设置这些宽度。其原型如下：

```
void gtk_clist_set_column_width(GtkClist *clist, gint column, gint width);
```

`gtk_clist_set_column_width()` 的参数为：

| 参数 | 说明 |
| --- | --- |
| clist | 指向将作用的 `GtkClist`。 |
| column | 将设置宽度的列号。 |
| width | 指定列的像素宽度。 |

为了方便工作，`gtk_clist_optimal_column_width()` 函数计算显示列中所有信息所需的宽度。注意，这在内容的特定状态下有效，并且每次需要时都应该重新计算。该函数的原型如下：

```
gint gtk_clist_optimal_column_width(GtkClist *clist, gint column);
```

`gtk_clist_optimal_column_width()` 的参数为：

| 参数 | 说明 |
| --- | --- |
| clist | 指向将作用的 `GtkClist`。 |
| column | 将计算最优宽度的列号。 |

该函数返回提供列的最优宽度。

如果 `gtk_clist_optimal_column_width()` 函数提供的宽度是你始终对特定列使用的值，你可以要求 GTK+ 自动跟踪更改。它将动态更新列宽。使用 `gtk_clist_set_auto_resize()` 函数来切换这种行为。其完整原型如下：

```
void gtk_clist_set_auto_resize(GtkClist *clist, gint column, gboolean auto_resize);
```

`gtk_clist_set_auto_resize()` 的参数为：

| 参数 | 说明 |
| --- | --- |
| clist | 指向 `GtkClist`。 |
| column | 将自动计算并设置最优宽度的列号。 |

`gtk_clist_columns_autosize()` 将所有列调整为它们的最优宽度。如果 `GtkClist` 的宽度大于所有最优列宽之和，剩余部分

# 使用列表

宽度将添加到最后一列的宽度中。`gtk_clist_columns_autosize()` 的原型如下：

```
int gtk_clist_columns_autosize(GtkClist *clist);
```

`gtk_clist_columns_autosize()` 参数为：

| 参数 | 描述 |
| --- | --- |
| clist | 指向 `GtkClist` 的指针，其列将被设置为最优宽度。 |

该函数返回所有列的最优宽度之和。

用户可以通过拖动列标题之间的细垂直条到另一个位置来更改此宽度。此功能对所有列默认都是开启的。`gtk_clist_set_column_resizable()` 允许对特定列切换此项功能。其完整原型如下：

```
void gtk_clist_set_column_resizable(GtkClist *clist, int column, gboolean resizeable);
```

`gtk_clist_set_column_resizable()` 参数为：

| 参数 | 描述 |
| --- | --- |
| clist | 指向函数将作用的 `GtkClist` 的指针。 |
| column | 要切换可调整大小属性的列索引。 |
| resizeable | 布尔值，决定该列是否应该是可调整的。 |

当列被调整大小后，会发出 `resize_column` 信号。这很重要，因为用户可能希望保持设置该列时的宽度。默认宽度计算应该被覆盖，并固定为用户选择的宽度。`resize_column_handler` 的原型如下：

```
void resize_column_handler(GtkClist *clist, int column, int width, gpointer user_data);
```

`resize_column_signal` 句器的参数为：

| 参数 | 描述 |
| --- | --- |
| clist | 指向发射信号的 `GtkClist` 的指针。 |
| column | 已调整大小的列索引。 |
| width | 用户设置的新宽度，单位为像素。 |
| user_data | 在将信号处理程序连接到控件时提供的可选用户数据。 |

![](img/7fa9959a9d28ad339fa75e44952feeb9_412_0.png)

# 在 GtkClist 行和单元格中使用样式

可以使用 GTK 样式更改 `GtkClist` 中每行的视觉属性。若要获取特定行的样式，应该使用 `gtk_clist_get_row_style()` 函数。请记住，如果你想更改此样式，必须先用 `gtk_style_copy()` 函数进行复制。`gtk_clist_get_row_style()` 函数的原型如下：

```
GtkStyle* gtk_clist_get_row_style(GtkClist *clist, gint row);
```

`gtk_clist_get_row_style()` 参数为：

| 参数 | 描述 |
| --- | --- |
