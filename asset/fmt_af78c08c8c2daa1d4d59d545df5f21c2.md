
`gtk_range_set_adjustment()` 如果你传递了该范围正在使用的调整项，它将什么都不做，无论你是否更改了它的字段。如果你传递了一个新的 `GtkAdjustment`，它将取消对旧调整项的引用（可能会销毁它），在新调整项上连接相应的信号，并调用函数 `gtk_range_adjustment_changed()`，该函数将（至少，理上应该……）重新计算滑块的大小和位置，并在必要时重绘。正如在调整节中提到的，如果你想重用同一个 `GtkAdjustment`，如果你直接修改了值，你应该在它上发射 "changed" 信号，如下：

```c
gtk_signal_emit_by_name(GTK_OBJECT (adjustment), "changed");
```

## 8.4 按键和鼠标绑定

所有的 GTK+ 范围小部件的移动方式大体相同。在槽位中点击左键将导致其调整项的 `page_increment` 从其值中加上或减去，并使滑块移动。在槽位中点击右键将把滑块跳转到点击按钮的位置。点击滚动条上的任何按钮都会导致调整项的值每次按 `step_increment` 步长变化。

这可能需要一点时间来适应，但在 GTK+ 中，滚动条以及缩放小部件都可以获取键盘焦点。如果你发现用户觉得这很困惑，你始终可以通过取消设置滚动条上的 `GTK_CAN_FOCUS` 来禁用它，如下：

```c
GTK_WIDGET_FLAGS (scrollbar, GTK_CAN_FOCUS);
```

按键绑定（它们在滚动条和缩放小部件之间略有不同）

### 8.4.1 垂直范围小部件

垂直范围小部件可以通过上下方向键操作，以及 `Page Up` 和 `Page Down` 键。用户还可以通过 `Home` 和 `End` 键将滑块移动到起始或末端。

### 8.4.2 水平范围小部件

左右方向键将如你预期的那样工作，让滑块左右移动。`Page Up` 和 `Page Down` 键会按页移动滑块。

## 8.5 示例

此示例是“范围小部件”示例的修改版本。它基本上放置了连接到同一个调整项的范围小部件。

# 8. 范围小部件

```
GtkWidget *button;
GtkWidget *scrollbar;
GtkWidget *separator;
GtkWidget *opt, *item;
GtkWidget *label;
GtkWidget *scale;
GtkObject *adj1, *adj2;
```

```c
/* 标准窗口创建相关代码 */
window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
gtk_signal_connect(GTK_OBJECT (window), "destroy",
GTK_SIGNAL_FUNC(gtk_main_quit),
NULL);
gtk_window_set_title(GTK_WINDOW (window), "range controls");
```

```c
box1 = gtk_box_new(GTK_FALSE, 0);
gtk_container_add(GTK_CONTAINER (window), box1);
gtk_widget_show(box1);
```

```c
box2 = gtk_box_new(GTK_FALSE, 0);
gtk_container_set_border_width(GTK_CONTAINER (box2), 10);
gtk_box_pack(GTK_BOX (box1), box2, TRUE, 0);
gtk_widget_show(box2);
```

```c
/* value, lower, upper, step_increment, page_increment, page_size */
/* 注意 page_size 值仅对滚动条小部件产生影响，
 * 你能获得的最大值实际上是
 * (upper - page_size)。 */
adj1 = gtk_adjustment_new(0.0, 0.0, 101.0, 0.1, 1.0, 0.0);
```

```c
vscale = gtk_scale_new(GTK_ADJUSTMENT (adj1));
scale_set_default_values(GTK_SCALE (vscale));
gtk_box_pack_start(GTK_BOX (box2), vscale, TRUE, 0);
gtk_widget_show(vscale);
```

```c
box3 = gtk_box_new(GTK_FALSE, 0);
gtk_box_pack_start(GTK_BOX (box2), box3, TRUE, 0);
gtk_widget_show(box3);
```

```c
/* 复用同一个调整 */
hscale = gtk_scale_new(GTK_ADJUSTMENT (adj1));
gtk_widget_set_scale(GTK_WIDGET (hscale), 200, 30);
scale_set_default_values(GTK_SCALE (hscale));
gtk_box_pack_start(GTK_BOX (box3), hscale, TRUE, 0);
gtk_widget_show(hscale);
```

```c
/* 再次复用同一个调整 */
scrollbar = gtk_scrollbar_new(GTK_ADJUSTMENT (adj1));
/* 注意当滚动条移动时，这会导致滚动条
 * 持续更新 */
gtk_range_set_update_policy(GTK_RANGE (scrollbar),
GTK_UPDATE_CONTINUOUS);
```

```c
gtk_box_pack_start(GTK_BOX (box3), scrollbar, TRUE, 0);
gtk_widget_show(scrollbar);
```

```c
box2 = gtk_box_new(GTK_FALSE, 0);
gtk_container_set_border_width(GTK_CONTAINER (box2), 10);
gtk_box_start(GTK_BOX (box1), box2, TRUE, 0);
gtk_widget_show(box2);
```

```c
/* 一个用于控制是否显示数值的按钮
 * */
button = gtk_check_button_new_label("Display value on scale widgets");
gtk_toggle_button_set_active(GTK_TOGGLE_BUTTON (button), TRUE);
gtk_signal_connect(GTK_OBJECT (button), "toggled",
GTK_SIGNAL_FUNC(cb_draw_value), NULL);
gtk_box_start(GTK_BOX (box2), button, TRUE, 0);
gtk_widget_show(button);
```

```c
box2 = gtk_hbox_new(FALSE, 10);
gtk_container_set_border_width(GTK_CONTAINER (box2), 10);
```

```c
/* 用于数值数值/标签位置的选项 */
label = gtk_label_new("Scale Value Position:");
gtk_box_start(GTK_BOX (box2), label, FALSE, 0);
gtk_widget_show(label);
```

```c
opt = gtk_option_menu_new();
menu = gtk_menu_new();
```

```c
item = make_menu_item("Top",
GTK_SIGNAL_FUNC(cb_pos_menu_select),
GTK_TO_POINTER (GTK_POS_TOP));
gtk_menu_append(GTK_MENU (menu), item);
```

```c
item = make_menu_item("Bottom",
GTK_SIGNAL_FUNC(cb_pos_menu_select),
GTK_TO_POINTER (GTK_POS_BOTTOM));
gtk_menu_append(GTK_MENU (menu), item);
```

```c
item = make_menu_item("Left",
GTK_SIGNAL_FUNC(cb_pos_menu_select),
GTK_TO_POINTER (GTK_POS_LEFT));
gtk_menu_append(GTK_MENU (menu), item);
```
