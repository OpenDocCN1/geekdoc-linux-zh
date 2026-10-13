
```c
void gtk_scale_draw_value(GtkScale *scale, boolean draw_value)
```

`gtk_scale_draw_value()` 的参数如下：

| 参数 | 描述 |
| --- | --- |
| `scale` | 你正在更改 `draw_value` 的 `GtkScale` 或 `GtkScale` |
| `draw_value` | 如果显示 `scale` 的值则为 `TRUE`；否则为 `FALSE`。 |

最后，由于 `scale` 是范围组件，你可以使用 `GtkRange` 函数控制某些属性。主要感兴趣的是 `gtk_range_set_update_policy()`。该策略控制发射 `value_changed` 信号的频率。以下是函数原型：

```c
void gtk_range_set_update_policy(GtkRange *range, GtkUpdateType policy);
```

`gtk_range_set_update_policy()` 的参数如下：

| 参数 | 描述 |
| --- | --- |
| `range` | 你正在设置的范围组件或更新方式 |
| `policy` | 如何更新范围。有效选择是 `GTK_UPDATE_CONTINUOUS`、`GTK_UPDATE_DISCONTIN` 或 `GTK_UPDATE_DELAYED`。 |

默认情况下，范围组件（如 `scale`）在每次移动时都会更新。如果策略是 `GTK_UPDATE_CONTINUOUS`，则每次移动组件时都会发射 `value_changed` 信号。如果策略是 `GTK_UPDATE_DISCONTIN`，则只有在用户完成移动并释放组件时才会发射 `value_changed` 信号。最后，`GTK_UPDATE_DELAYED` 策略会在用户暂停移动组件或释放组件时发射 `value_changed` 信号。

> 通常，释放组件意味着释放用于移动 `scale` 或滚动条的鼠标左键。

# GtkScrollbar

你在第 7 天的“需要考虑的其他组件和问题”中看到了滚动条组件。然而，对于滚动窗口，滚动窗口创建了自己的滚动条，因为传递给 `gtk_scrolled_window_new()` 函数的调整值为 `NULL`。现在你将学习创建自己的滚动条，并将其提供给需要滚动能力的组件（如 `GtkText` 组件），或使用滚动条控制其他组件，例如图 17.17 测试页中的 `scale`。

`gtk_vscrollbar_new()` 和 `gtk_hscrollbar_new()` 的参数如下：

| 参数 | 说明 |
|---|---|
| `adjustment` | 一个控制滚动条范围的 `GTK+` 对象（例如 0 到 100%）。可以为 `NULL`。 |

为了将滑块和滚动条的操作结合在一起，你必须共享同一个调整对象。因此，当调整值发生变化时，滚动条会自动更新，反之亦然。列表 17.11 显示了添加滚动条的过程，它共享滑块的调整对象。

## 列表 17.11 滑块与滚动条，共享调整对象。

```c
1: GtkWidget *top_widget, *box, *scale, *scroll;
2: GtkObject *adj;
3: /* ... */
4: adj = gtk_adjustment_new(50.0, 0.0, 101.0, 0.1, 1.0, 1.0);
5: scale = gtk_hscale_new(GTK_ADJUSTMENT(adj));
6: gtk_widget_set_usable(scale, 150, 40);
7: gtk_box_pack_start_defaults(GTK_BOX( box ), scale);
8: scroll = gtk_hscrollbar_new(GTK_ADJUSTMENT(adj));
9: gtk_widget_set_usable(scroll, 150, 40);
10: gtk_box_pack_start_defaults(GTK_BOX( box ), scroll);
```

如果你想创建一个与之前讨论过的 `GtkText` 配合使用的滚动条，你应该共享滑块的调整对象，就像滚动条共享滑块的调整值一样。文本控件的调整值是 `GtkText` 结构中的字段。`GtkText` 结构的大部分是私有的，不打算直接访问。唯一的例外是水平和垂直调整字段。它们是 `hadj` 和 `vadj`，类型如下：

```c
GtkAdjustment *hadj;
GtkAdjustment *vadj;
```

以下是一个为文本控件添加垂直滚动条的示例：

```c
* 创建文本框，带有滚动条 /
textbox = gtk_hbox_new(FALSE, 0);
gtk_box_pack_start_defaults(GTK_BOX( box ), textbox);
text = gtk_text_new(NULL, NULL);
gtk_widget_set_editable(text, GTK_TEXT(text), TRUE);
gtk_widget_set_usable(text, 100, 100);
gtk_box_pack_start_defaults(GTK_BOX( textbox ), text);
vscroll = gtk_vscrollbar_new(GTK_TEXT(text)->vadj);
gtk_box_pack_start_defaults(GTK_BOX( textbox ), vscroll);
```

### 总结

今天你学习了如何使用更多的 `GTK+` 控件集，包括 `GtkToggleButton`、`GtkCheckButton`、`GtkRadioButton`、`GtkOptionMenu`、`GtkCheckMenuItem`、`GtkRadioMenuItem`、`GtkTearOffMenuItem`、`GtkInput`、`GtkText`、`GtkScale` 和 `GtkScrollbar`。还有超出 21 天范围的可用控件。所有控件在附录 C 中简要描述。今天讨论的控件为你的用户界面设计提供了额外的功能。

### 问答

- 我为文本控件设置了水平滚动条，并将调整值设置为 `GTKTEXT(text_widget)->hadj`。滚动条出现了，但长度始终是文本控件的长度，且不起作用。

- 因为文本控件提供了换行和自动行的功能，所以水平滚动条没有效果。

- 我正在使用选项菜单（option menu），但选项菜单比当前选中的值大得多。出什么问题了？

- 选项菜单试图补偿最可能的选择，因此它比较小选择之一大得多。在某些 `GTK+` 版本中，选项菜单没有考虑长菜单并在选择时截断部分值，因此我们必须以某种方式打包以考虑选项菜单上的长条目。

- 调整（adjustments）只能用于滑块和滚动条控件吗？

- 调整通常与 `GtkRange` 控件（滑块和滚动条）、`GtkViewport` 控件、`GtkSpinButton` 控件关联。此外，`GtkColorSelection`、`GtkLayout`、`GtkProgress` 和 `GtkText` 也使用调整。

- 共享调整有什么特别的吗？例如，我只能在范围控件之间共享调整吗？或者可以在控件之间共享调整吗？

- 你可以在任何使用调整的控件之间共享调整。在今天的示例中，你可以轻松地将数字按钮（spin button）绑定到滑块和滚动条上。

- 有没有方法让一组 `GtkToggleButtons` 变得互斥，像 `GtkRadioButtons` 那样？

- 在组中仅有一个有效选择是 `GtkRadioButtons` 的严格功能。切换按钮没有关联的组。然而，你可以更改单选按钮的外观使其看起来像切换按钮。

![](img/7fa9959a9d28ad339fa75e44952feeb9_502_0.png)

使用 `gtk_toggle_button_set_mode()` 使按钮看起来像切换按钮，该函数接收一个切换按钮（或后代）和一个 `TRUE`/`FALSE` 作为参数。固定控件（fixed widget）允许你在窗口的特定位置放置图标并轻松地更改其位置。

### 工作坊

使用 `gtk_toggle_button_set_mode()` 使按钮看起来像切换按钮，该函数接收一个切换按钮（或后代）和一个 `TRUE`/`FALSE` 作为参数。固定控件允许你在窗口的特定位置放置图标并轻松地更改其位置。

### 测验

测验题和练习已为提供。

# 答案

1. `GtkFixed` 和 `GtkTable` 有什么区别？

2. 什么是调整（adjustment）？

3. 假设固定控件，什么是 `GtkFixed`？

```c
void start_smiley(GtkFixed* area, GtkWidget* widget) {
  static guint smile_tag = 0;
  smile_tag = gtk_timeout_add(500, area);
}
```

4. 如何防止用户更改文本？

### 练习

1. 使用 `fixed` 创建选项菜单。

2. 使用 `fixed` 创建可滚动区域。

## 更多容器组件
