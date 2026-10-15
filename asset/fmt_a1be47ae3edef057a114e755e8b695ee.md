
```c
39:    file_item = create_file_and_menu( GTK_MENU_BAR(menu_bar) );

40:

41:    /* 创建绘制项 */

42:    plot_item = gtk_menu_new_with_label("Plot");

43:    gtk_menu_bar_append( GTK_MENU_BAR(menu_bar), plot_item);

44:    gtk_signal_connect( GTK_OBJECT(plot_item), "activate",

45:                        GTK_SIGNAL_FUNC(line_plot), plot_area );

46:

47:    /* 显示小部件 */

48:    gtk_widget_show_all(top_widget);

49:

50:    /* 循环处理 */

51:    gtk_main();

52:    g_print("Bye!\n");

53:    return 0;

54: }
```

第 5 行定义了带有标签子元素的弹出窗口小部件变量，用于显示坐标。第 11 行创建了一个类型为 `GTK_WINDOW_POPUP` 的 `GtkWindow` 作为父窗口。这是第一个使用弹出窗口的示例。因为包含坐标的标签不会显示很长时间（是瞬态的），因此 `GTK_WINDOW_POPUP` 是最逻辑的选择（不需要与窗口管理器交互）。第 12-14 行创建并显示了作为 `coord_popup` 子元素的标签小部件。第 17-30 行是之前 `line_plot()` 用户界面中使用的标准小部件：一个顶层窗口，带有一个管理菜单栏和绘制区域的垂直框（box）。第 31-32 行将 `show_coord()` 回调连接到按钮按下事件信号，传递标签小部件用于显示坐标。第 33-34 行挂载了 `gtk_widget_hide(coord_popup)` 按钮释放事件信号。第 35-36 行请求绘制区域添加按钮按下和释放事件的处理（并在接收相应的 G 事件时发射 `button-press-event` 和 `release-event` 信号），因为 `GtkDrawingArea` 没有处理这些事件。

# 添加 GDK 事件处理

一个常见的错误是编写并连接了适当的信号处理程序，却忘记将事件添加到小部件中。因为有内置信号，很容易忽视它们不会自动发射 GDK 包装（wrapped）信号的这一事实。这尤其令人人感到困惑，因为某些 GDK 包装信号是由某些小部件发射的，例如 `GtkButton` 关于 `button-press-event` 和 `button-release`。要点在于，如果 GDK 包装信号与该小部件执行的固有动作相关（例如在 `GtkButton` 上可以按钮按下和释放，从而发射 `clicked` 信号），那么它可能已经选择了相应的 GDK 包装事件。否则，你需要手动添加。

作为次要点，为小部件设置它已经在收集的事件并无害，这样即使小部件正在通过 `gtk_widget_set_events()` 处理这些事件，你也可以调用任何 GDK 包装信号。

列表 12.4 展示了显示坐标的回调。

## 12.4 show_coord()

```c
1: gboolean show_coord( GtkWidget *area, GdkEventButton *event,
2:     GtkWidget *label ) {
3: GtkWidget *popup = gtk_widget_get_ancestor(label, gtk_window_get_type());
4: int x = event->X-X_PAD;
5: int y = event->Y_AXIS+Y_PAD-event->y;
6: char *coords = g_strdup_printf("%d, %d\n", x, y);
7:
8: gtk_label_set_text( GTK_LABEL(label), coords);
9: gtk_widget_popup(popup, event->x_root, event->y_root );
10:    return TRUE;
11: }
```

![](img/7fa9959a9d28ad339fa75e44952feeb9_304_0.png)

第 1-2 行根据按钮按下事件处理程序的原型定义了 `show_coord()`，其中标签通过用户数据字段接收。第 3 行获取标签小部件的弹出窗口父级。第 4 行通过从绘制区域边缘减去内边距（padding）并从 `GtkEventButton` 结构体中报告的 x 轴起始位置来计算 X 坐标。如果你还记得 `line_plot()` 函数，内边距是在回调文件中定义的，因此此函数需要与 `line_plot()` 位于同一个文件中。第 5 行通过从报告的 y 位置中减去内边距并加上 y 轴偏移量来计算 Y 坐标。第 6 行使用 `g_strdup_printf` 创建坐标字符串。第 7 行是空行。第 8 行使用 `gtk_label_set_text` 设置标签文本。第 9 行使用 `gtk_widget_popup` 显示弹出窗口。第 10 行返回 `TRUE`。

# 添加 CDK 事件处理

## 处理暴露事件（重温位图）

昨天，在讨论位图（pixmaps）时，我提到位图通常用于处理图像中出现空洞并必须更新的情况。每当出现空洞时，系统就会就会向你的窗口发送一个暴露事件（expose event），例如当一个原本在顶部的窗口被遮挡时。或者：当用户移动或折叠颜色选择对话框时，该对话框部分遮挡并擦除了饼图的区域，如图 12.4 所示。

图 12.4

饼图中由于重叠的颜色选择对话框而产生的空洞，现已隐藏。

![](img/7fa9959a9d28ad339fa75e44952feeb9_308_0.png)

> 注意，今天早些时候显示的标签小部件和下拉菜单通常不会在你的图像中留下空洞。弹出窗口使用一种被称为“备份存储”（backing store）的功能，它在弹出小部件之前会记住较小的区域，并在小部件弹出时恢复该区域。备份存储需要少量的内存，因此在许多服务器上都是可用的。但如果没有，在标签弹出或菜单结束时，你将收到一个暴露事件来进行处理。

![](img/7fa9959a9d28ad339fa75e44952feeb9_308_1.png)

处理饼图程序暴露事件的第一步是添加位图。绘制图像时涉及的大部分时间都用于确定响应绘图请求应该设置哪些像素。如果这种渲染是在位图上进行的，那么通过将适当的像素从位图传输到屏幕就可以更新空洞，而不需要重复渲染过程。准备饼图程序处理暴露事件的第一步是修改 `draw_pie_chart()` 以使用位图。

不应该让位图的大小直接与饼图的大小一致，而应该让位图的大小与绘图区域的大小一致。这样，当暴露事件指示一个空洞时，你可以轻松地从位图拷贝到绘图窗口，因为暴露事件给出的矩形区域与绘图区域的位置完全相同。要确定小部件的大小，你需要了解 `Gtkwidget` 结构中的 `allocation`（分配）字段。列表 12.5 显示了在第 8 天“为你的应用程序添加图形”中引入的 `Gtkwidget` 结构。

### 列表 12.5 GtkWidget 结构

```
1: struct _GtkWidget
2: {
3:   GtkObject object;
4:   guint6 private_flags;
5:   uint8 state;
6:   uint8 saved_state;
7:   gchar *name;
8:   GtkStyle *style;
9:
10:  /* The widgets desired size.
11:  */
12:  GtkRequisition requisition;
13:
14:  /* The widgets allocated size.
15:  */
16:  GtkAllocation allocation;
17:
18:  GdkWindow *window;
19:  GtkWidget *parent;
20: };
```

第 16 行显示了 `allocation` 字段，它表示小部件分配的大小。（第 12 行显示了相关的 `requisition` 字段，它表示小部件所需的大小。取决于父小部件，有时这两个字段是等价的。）列表 12.6 显示了 `GtkAllocation` 结构。

### 列表 12.6 GtkAllocation 结构

```
1: typedef struct _GtkAllocation GtkAllocation;
2: /* 分配包含一个大小和一个位置。在一个小部件
3:  * 可以请求一个所需的大小时，它实际上在指定位置
4:  * 被给予了该数量的空间。
5:  */
6: struct _GtkAllocation
7: {
8:   int16 x;
```
