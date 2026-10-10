
```c
gtk_widget_show_all (dialog_window);
```

```c
main(int argc, char *argv[]) {
  gtk_init(&argc, &argv);
  GtkLayoutDialog();
  gtk_main();
}
```

## 设置和获取布局调整对象

之前的示例都使用了由 `GtkLayout` 创建的水平和垂直调整对象（adjustment objects）。这是因为我们在调用 `gtk_layout_new(window)` 时传递了 `NULL` 作为参数。我们可以通过分别调用 `gtk_layout_get_adjustment()` 和 `gtk_layout_get_vertical_adjustment()` 来获取由布局小部件创建的水平和垂直调整对象：

- `GtkAdjustment`

  `gtk_layout_get_horizontal_adjustment(GtkLayout *layout);`

- `GtkAdjustment`

  `gtk_layout_get_vertical_adjustment(GtkLayout *layout);`

这两个函数都接受一个 `GtkLayout` 实例作为唯一参数，并返回请求的调整对象。我们可以使用 `gtk_layout_set_adjustment()` 来设置或更改布局小部件的水平调整：

```c
void
gtk_layout_set_adjustment(GtkLayout *layout,
GtkAdjustment *adjustment);
```

```c
void
gtk_layout_set_vertical_adjustment(GtkLayout *layout,
GtkAdjustment *adjustment);
```

这两个函数都接受布局小部件和一个调整对象作为参数。

## 布局小部件：最后一个示例

我将通过展示一个示例的源码，该示例展示了如何使用小部件的调整来控制布局小部件的视口（viewport）。在之前的示例中，布局小部件管理区域的视口是通过滚动窗口（scrolled window）部件实现的，布局小部件作为子部件添加到其中。在这个示例中，我将使用一对旋钮按钮（spin button）小部件来控制布局小部件管理的可见区域。旋钮按钮小部件创建一个调整对象，该对象可以作为布局小部件的水平或垂直调整。

`GtkLayout` Demo

![](img/1441ee0eb9a357efc9aff107f92bf0c0_616_0.png)

图 11.39 使用旋钮按钮控制滚动位置

图 11.39 展示了客户端。旋钮按钮共同指定了进入布局小部件管理区域的视图点的 x 和 y 坐标。当任一旋钮按钮的值改变时，布局小部件将收到来自相应调整对象的 `value_changed` 信号。布局小部件将处理此信号。最终结果是，布局小部件根据用户选择的区域进行绘制，并使其对用户可见。

## 列表 11.13 使用旋钮按钮控制布局小部件滚动

```c
#include <gtk/gtk.h>
void
GtkLayoutDialog() {
  GtkWidget *layout, *spinner, *scrolled_window, *button, *vbox;
  GtkWidget *hbox, *dialog_window;
  GtkAdjustment *adj1, *adj2;
  char buf[32];
  int i, j;

dialog_window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
gtk_window_position(GTK_WINDOW(dialog_window), GTK_WIN_POS_CENTER);
gtk_widget_set_size(GTK_WIDGET(dialog_window), 200, 200);

g_signal_connect(GTK_OBJECT(dialog_window), "destroy",
  GTK_SIGNAL_FUNC(gtk_widget_destroyed), &dialog_window);
gtk_window_set_title(GTK_WINDOW(dialog_window), "GtkLayout Demo");
gtk_container_border_width(GTK_CONTAINER(dialog_window), 10);
  vbox = gtk_box_new(VERTICAL, 0);
gtk_container_add(GTK_CONTAINER(dialog_window), vbox);

layout = gtk_layout_new(NULL, NULL);

gtk_layout_set_size (GTK_LAYOUT (layout), 800, 12800);

for ( i = 0; i < 2; i++ {
  for ( j = 0; j < 2; j++ {
    sprintf(buf, "Button %d-%d", i, j);
    button = gtk_button_new_with_label(buf);
    gtk_container_add(GTK_CONTAINER(layout), button);
  }
}
hbox = gtk_box_new(HORIZONTAL, 0);
gtk_box_pack_start(GTK_BOX(vbox), layout, TRUE, TRUE, 0);
gtk_box_pack_start(GTK_BOX(vbox), hbox, FALSE, FALSE, 0);

scrolled_window = gtk_scrolled_window_new(NULL, NULL);
gtk_container_add(GTK_CONTAINER(scrolled_window), layout);
gtk_container_add(GTK_CONTAINER(vbox), scrolled_window);

adj1 = gtk_adjustment_new(0, 0, 800, 10, 10, 0);
adj2 = gtk_adjustment_new(0, 0, 12800, 10, 10, 0);
spinner = gtk_spin_button_new(adj1, NULL, 1);
gtk_box_pack_start(GTK_BOX(hbox), spinner, TRUE, TRUE, 0);
spinner = gtk_spin_button_new(adj2, NULL, 1);
gtk_box_pack_start(GTK_BOX(hbox), spinner, TRUE, TRUE, 0);

gtk_layout_set_adjustment(GTK_LAYOUT(layout), adj1);
gtk_layout_set_vertical_adjustment(GTK_LAYOUT(layout), adj2);

gtk_widget_show_all(dialog_window);
gtk_main();
}
```

# 第 12 章 树

在本章中，我将介绍三个部件类：`GtkTree`、`GtkTreeItem` 和 `GtkTreeView`。前两个类 `GtkTree` 和 `GtkTreeItem` 将在第一节中共同介绍。将 `GtkTree` 和 `GtkTreeItem` 放在一起讨论是因为在不了解另一类的情况下，你实际上无法使用其中任何一类。在对 `GtkTree` 和 `GtkTreeItem` 进行常规讨论后，我将分别介绍这些类的 API。最后，本章将在对 `GtkTree` 的回顾中结束。

## 为什么使用树？

树形部件与列表（`GtkList` 和 `GtkTreeList`）类似——两者都可以用于显示一组可以供用户选择的项目。树比列表更强大，因为它们允许程序员以列表无法实现的方式组织数据，并让用户对任何给定时刻显示的数据量有更多的控制权。这并不是说你应该在应用程序中使用树来代替列表。如果你显示的是一个简短的项目列表，那么树可能就大材小用了。但是，如果你显示的是可以表示层级结构的数据（例如公司通讯录或文件系统内容），或者你显示的是可以分类组织的数据，或者你显示的是聚合数据，那么树将是最佳选择。接下来的示例说明了一个明显优于列表使用树的情况。

我们可以显示生活在海洋中的动物名称，我们处理的数据涉及哺乳动物、无脊椎动物和鱼类。使用列表显示此类数据的示例见图 12.1。列出的某些动物是广为人知的，例如，大多数读者都能认出大白鲨是鱼类。但章鱼是什么呢？它是鱼类、哺乳动物还是无脊椎动物？对于显示此列表的应用程序来说，允许用户选择章鱼是不切实际的，因为用户界面没有提供足够的信息来做出选择。
