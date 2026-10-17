
## 6. 在 `GtkTree` 上点击鼠标中间按钮或右键触发什么事件？

## 7. `GtkTree` 中有一个特殊列。它的功能是什么？如何调用？

## 8. 使用哪些元素来构建 `GtkList` 行？如何访问它们？

## 练习

### 1. 编写代码创建一个支持多选择模式的新 `GtkTree`。确保显示树结构。

### 2. 填充前一个练习中的 `GtkTree`，带有十个显示 `Root` 标签的项。叶子和其他是节点。为这些显示 `Child` 标签的节点创建一个分支。

### 3. 为前一个练习 `GtkTree` 的 `selection_changed` 信号编写处理器。

### 4. 使用编写的函数模拟 `GtkTree` 控件的焦点。假设 `GtkTree` 存在且支持焦点。打印“当前没有焦点”。

### 5. 创建一个具有两列的新 `GtkTree` 控件，第一列为树列。选择模式已扩展。树的样式是固定的，展开符号是三角形的。`GTK+` 会自动调整树列的大小。

### 6. 使用 `GtkList` 函数显示前一个练习 `GtkTree` 的树列和 `Column2` 标题。同时也禁用列按钮。

# 第三周

# 第 17 天

# 更多控件

在过去的 16 天里，你学习了大量 `GTK+` 的知识，包括关于 `GDK` 和 `GLib` 库的信息。作为 `GTK+` 程序员，你可能发现了大量的工具，包括大量的可用控件。今天你将学习：

- `GtkToggleButton`、`GtkCheckButton` 和 `GtkRadioButton` 的用法
- 菜单以及如何使用选项菜单
- 输入和显示文本
- `Scale` 和滚动条的用法

# 按钮回顾

到为止看到的所有按钮都是 `GtkButton` 类，有时被称为推按钮。文件选择、字体选择、颜色选择以及对话框按钮都是推按钮。`GtkButton` 通常用于在用户点击按钮时调用操作。还有其他按钮可以给用户提供额外的状态信息。这些包括 `GtkToggleButton`、`GtkCheckButton` 和 `GtkRadioButton`，它们都是 `GtkButton` 类的后代，如图 17.1 所示。

# 图 17.1

`GtkButton` 分类的类树。

| `GtkBin` |
| `GtkButton` |
| `GtkToggleButton` |
| `GtkCheckButton` |
| `GtkRadioButton` |

切换按钮和复选框提供状态信息，通常表示开启或关闭。当多个按钮之间的状态信息互斥时（只有一个有效），使用单选按钮。图 17.2 显示了来自 `testgttk` 的切换、复选框和单选按钮示例。

# 图 17.2

![](img/7fa9959a9d28ad339fa75e44952feeb9_471_0.png)

切换按钮、复选框和单选按钮。（一次只能选择单选按钮。）

切换按钮和复选框提供相同的信息，但视觉方式不同。使用其中一个还是另一个完全取决于程序员的偏好，取决于你喜欢的样式。

# GtkToggleButton

切换按钮通常带有标签子节点创建，使用 `gtk_toggle_button_new_with_label()`。以下是该函数原型：

`GtkWidget *gtk_toggle_button_new_with_label(const gchar *label)`

返回切换按钮。`gtk_toggle_button_new_with_label()` 的参数如下：

| 参数 | 描述 |
|---|---|
| `label` | 放置在新切换按钮标签子节点上的文本 |

如果你更喜欢创建一个空的切换按钮，也许可以创建一个位图子节点，或者创建一个带有包含位图子框的标签，正如菜单项上做的那样。

第 11 天。“包含位图。” 创建一个空的切换按钮可以通过 `gtk_toggle_button_new()` 完成。这里是该函数的原型定义：

```
GtkWidget *gtk_toggle_button_new( void )
```

返回一个新的新的切换按钮。

切换按钮在被点击时会发射一个 `toggled` 信号。这里是 `toggled` 信号处理函数：

```
void user_function( GtkToggleButton *togglebutton, gpointer user_data )
```

与其在第 11 天的笑脸动画示例中使用动画菜单，或许许将切换按钮直接放在图片下方（如图 17.3 所示）会更有意义。

# 图 17.3

带有切换按钮的笑脸动画。

![](img/7fa9959a9d28ad339fa75e44952feeb9_472_0.png)

切换按钮允许用户在动画的开启和关闭，而无需在菜单选项中进行查找。列表 17.1 显示了第 11 天笑脸动画修改后的用户界面。

# 列表 17.1 toggle_smiley 用户界面

```
1: int main( int argc, char *argv[])
2: {
3:   GtkWidget *top_widget, *box, *drawing, *smiley_button;
4:   GtkWidget *menu_bar, *file_item, *file_menu;
5: 
6:   /* 初始化环境 */
7:   gtk_init(&argc, &argv);
8: 
9:   /* 创建切换小部件 */
10:  top_widget = gtk_window_new(GTK_WINDOW_TOPLEVEL, "delete-event");
11:  gtk_signal_connect(GTK_OBJECT(top_widget), "delete_event_handler", NULL);
12:  GTK_SIGNAL_FUNC(delete_event_handler),
13:   gtk_signal_connect(GTK_OBJECT(top_widget), "destroy",
14:   GTK_SIGNAL_FUNC(print_and_quit), NULL);
15:
16:
17:   /* 创建垂直框小部件 */
18:   box = gtk_vbox_new(FALSE, 0); /* 非均匀，无间距 */
19:
20:   gtk_container_add(GTK_CONTAINER (top_widget), box );
21:
22:   /* 创建菜单栏小部件 */
23:   menu_bar = gtk_menu_bar_new();
24:   gtk_box_pack_starts(GTK_BOX(box ), menu_bar, FALSE );
25:
26:   /* 创建文件菜单项及其菜单小部件 */
27:   file_item = gtk_menu_item_new_label("File");
28:   gtk_menu_bar_append(GTK_MENU_BAR(menu_bar), file_item);
29:
30:   file_menu = gtk_menu_new();
31:
32:   gtk_menu_item_set_submenu(GTK_MENU_ITEM(file_item), file_menu);
33:
34:   /* 创建文件项目 * */
35:   append_menu_item(GTK_MENU(file_menu), "Exit", print_and_quit, NULL );
36:
37:   /* 创建绘制区域小部件 */
38:   drawing = gtk_drawing_area_new();
39:   gtk_drawing_area_size(GTK_DRAWING_AREA(drawing), 200, 200);
40:   gtk_box_pack_starts(GTK_BOX(box ), drawing, FALSE );
41:
42:   /* 创建切换按钮 */
43:   smile_button = gtk_toggle_button_new_with_label("Animate smiley");
44:   gtk_box_pack_starts(GTK_BOX(box ), smile_button, FALSE );
45:
46:   /* 绑定笑脸 */
47:   gtk_signal_connect(GTK_OBJECT(smile_button), "toggled",
48:   GTK_SIGNAL_FUNC(toggle_smiley), drawing);
49:
50:   /* 显示小部件 */
51:   gtk_widget_show_all(top_widget);
52:
53:   /* 运行循环 * */
54:   gtk_main();
55:   g_print("Bye!\n");
56:   return 0;
```
