
`GtkFontSelectionDialog` 是一个弹出组件，因此是 `GtkWindow` 的子组件。列表 10.4 是 Gtk+ 源码中 `GtkFontSelectionDialog` 的定义。

### 列表 10.4 GtkFontSelectionDialog

```
1: typedef struct _GtkFontSelectionDialog GtkFontSelectionDialog;
2: struct _GtkFontSelectionDialog
3: {
4:   GtkWindow window;
5:
6:   GtkWidget *fontsel;
7:
8:   GtkWidget *main_vbox;
9:   GtkWidget *action_area;
10:  GtkWidget *ok_button;
11:  /* 'Apply' 按钮默认不显示，但你可以显示/隐藏它。 */
12:  GtkWidget *apply_button;
13:  GtkWidget *cancel_button;
14:
15:  /* 如果用户更改了对话框的宽度，我们将关闭自动缩放 */
16:    guint dialog_width;
17:    gboolean auto_resize;
18: };
```

第 6-13 行显示了字体选择对话框包含的子组件（`child_widgets`）（第 5 行是父级 `GtkWindow`）。`fontsel` 字段包含一个作为子成员的字体选择组件。字体选择对话框是一个弹出组件，包含一个字体选择组件以及结构体中所示各种按钮。为了给用户提供选择字体的能力而不使用弹出窗口，你可以使用图 10.10 所示的 `GtkFontSelection` 组件。

## 分析

### 图 10.10

`GtkFontSelection` 组件的示例。

![](img/7fa9959a9d28ad339fa75e44952feeb9_257_0.png)（等待，检查路径 - 保持链接）

`GtkFontSelection` 是 `GtkNotebook` 的后代，在第 16 天详细讨论“树”。图 10.11 显示了 `GtkFontSelection` 的类树。

### 图 10.11

`GtkFontSelection` 在 GTK+ 类树中的位置。

![](img/7fa9959a9d28ad339fa75e44952feeb9_257_1)

在饼图的情况下，当用户想要更改饼图标签使用的字体时，字体选择组件应该弹出。例如，响应“更改字体”菜单项可以弹出 `GtkFontSelectionDialog`。GTK+ 函数 `gtk_font_selection_dialog_new()` 创建字体选择对话框。函数原型如下：

```
GtkWidget* gtk_selection_dialog_new (const gchar *title)
```

`gtk_selection_dialog_new()` 的参数如下：

| 参数 | 说明 |
|---|---|
| `title` | 你希望显示的标题，提醒用户此字体对话框的目的 |

列表 10.5 显示了饼图程序的“更改字体”菜单项和相应的信号处理器，如图 10.12 所示。

### 更改你的字体

### 图 10.12

饼图的新菜单。

![](img/7fa9959a9d28ad339fa75e44952feeb9_258_0.png)

### 列表 10.5 GtkFontSelectionDialog

```
1: int main(int argc, char *argv[])
2: {
3: GtkWidget *top_widget, *box, *pie_area;
4: GtkWidget *menu_bar, *pie_item, *pie_menu;
5: GtkWidget *font_item, *fontsel_dlg;
6:
7:     /* 初始化环境 */
8:     gtk_init(&argc, &argv);
9:
10:    /* 创建 widget */
11:    top_widget = gtk_window_new("Pie Chart");
12:
13:    /* 创建垂直框 */
14:    box = gtk_box_new(GTK_VERTICAL, G_PADDING);
15:    gtk_container_add(GTK_CONTAINER(top_widget), box);
16:
17:    /* 创建菜单条 widget */
18:    menu_bar = gtk_menu_bar_new(GTK_BOX(box));
19:    gtk_box_pack_start(GTK_BOX(box), menu_bar, FALSE, FALSE);
20:
21:    /* 创建绘制区域 widget */
22:    pie_area = gtk_drawing_area_new();
23:    gtk_widget_area_size_request(GTK_DRAWING_AREA(pie_area), 200, 250);
24:    gtk_box_pack_start(GTK_BOX(box), pie_area, TRUE, TRUE);
25:
26:    /* 创建文件项及其菜单 widget */
27:    create_file_and_menu(GTK_MENU_BAR(menu_bar), menu_bar);
28:
29:    /* 创建饼图项及其菜单 widget */
30:    pie_item = gtk_menu_item_new_with_label("Pie");
31:    gtk_menu_bar_append(GTK_MENU_BAR(menu_bar), pie_item);
32:    pie_menu = gtk_menu_item_new();
33:    gtk_menu_item_set_submenu(GTK_MENU_ITEM(pie_item), pie_menu);
34:
35:    /* 创建饼图菜单项 */
36:    font_item = append_menu_item(GTK_MENU(pie_menu), "Change Font",
37:    NULL, NULL);
38:    append_menu_item(GTK_MENU(pie_menu), NULL, NULL);
39:    append_menu_item(GTK_MENU(pie_menu), "Draw pie chart", plot_values,
40:    pie_area);
41: 
42:    /* 创建选择对话框，并连接信号处理器
43:    以将其弹出 */
44:    fontsel_dlg = gtk_font_selection_dialog_new("Select Pie label's new font");
45:    gtk_signal_connect_object(GTK_OBJECT(font_item), "activate",
46:    GTK_SIGNAL_FUNC(gtk_widget_show), GTK_OBJECT(fontsel_dlg));
47:    gtk_signal_connect(fontsel_dlg, "delete_handler",
48:    GTK_SIGNAL_FUNC(dialog_delete_handler), NULL);
49:    gtk_signal_connect_object(GTK_OBJECT(font_item),
50:    GTK_FONT_SELECTION_DIALOG(fontsel_dlg)->cancel_button,
51:    "clicked");
52: 
53:    /* 显示所有 widget */
54:    gtk_widget_show_all(top_widget);
55: 
56:    /* 循环 */
57:    gtk_main();
58:    g_print("Bye!\n");
59:    return 0;
60:}
```

第 29-33 行在菜单条上创建了一个饼图项，并附带了子菜单。第 36-37 行创建了“更改字体”菜单项，它将用于激活选择对话框。第 38-40 行创建了子菜单中的其他项目：分隔符和“绘制饼图”菜单项。第 44 行创建了选择对话框 `fontsel_dlg`。第 45-46 行为“更改字体”菜单项连接了信号处理器，在激活时调用 `gtk_widget_show(fontsel_dlg)`。第 47-48 行连接了第 7 天编写、昨天在讨论 `GtkColorSelectionDialog` 时复过的 `dialog_delete_handler()`，以处理用户从窗口管理器框架关闭字体选择对话框的情况。第 49-52 行在用户改变主意时隐藏字体选择对话框。

## 分析
