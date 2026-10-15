
```c
  gtk_init (&argc, argv);

  window = gtk_window_new(GTK_WINDOW_TOPLEVEL);

  gtk_window_set_size(GTK_WINDOW(window), 200, 600);

  g_signal_connect (GTK_OBJECT(window), "destroy", GTK_SIGNAL_FUNC(onClose), NULL);

  button = gtk_button_new_with_label("Ok");

  togglebutton = gtk_toggle_button_new_with_label("Toggle");

  checkbutton = gtk_check_button_new();

  radiobutton1 = gtk_radio_button_new(NULL);

  radiobutton2 = gtk_radio_button_new_from_widget(GTK_RADIO_BUTTON, radiobutton1);

  vbox = gtk_vbox_new(TRUE, 4);

  add_widget_with_label(GTK_CONTAINER(vbox), "Toggle:", togglebutton);

  add_widget_with_label(GTK_CONTAINER(vbox), "Check:", checkbutton);

  add_widget_with_label(GTK_CONTAINER(vbox), "Radio 1:", radiobutton1);

  add_widget_with_label(GTK_CONTAINER(vbox), "Radio 2:", radiobutton2);

  add_widget_with_label(GTK_CONTAINER(vbox), "Button:", button);

  g_signal_connect (GTK_OBJECT(button), "clicked", GTK_SIGNAL_FUNC(on_button_clicked), NULL);

  gtk_container_add(GTK_CONTAINER(window), vbox);

  gtk_window_show_all(window);

  return 0;

}
```

图 16-10 显示了运行中的按钮，包含了四种常见的 `GtkButton` 类型。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_688_0.png)

图 16-10

这个程序是四种 `GtkButton` 类型的简单示例，展示了我们如何使用单一的 `gtk_toggle_button_get_active` 来读取 `GtkToggleButton`、`GtkCheckButton` 和 `GtkRadioButton` 的状态。这是面向对象方法的最大好处之一——因为我们不需要为每种按钮编写单独的函数，可以减少代码量。

## `GtkTreeView`

到为止，我们查看了一些简单的 GTK+ 部件，但并不是所有部件都是简单的输入或显示设备。当然，`GtkWidget` 的复杂性是没有限制的，`GtkTreeView` 是封装了大量功能的部件的绝佳示例。

```text
GtkWidget

+-GtkContainer

  +-GtkTreeView
```

`GtkTreeView` 是 GTK+ 2 新引入的一系列部件的一部分，用于创建你在电子表格或文件管理器中常见的数据列表和树形视图。使用 `GtkTreeView`，我们可以创建复杂的数据视图、混合文本和位图图形，甚至使用 `GtkEntry` 部件输入数据等等。

快速上手 `GtkTreeView` 的方法是运行与 GTK+ 自带的 `gtk-demo` 应用程序。该程序展示了每个 GTK+ 部件的功能，包括 `GtkTreeView`（如图 16-11 所示）。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_689_0.png)

图 16-11

`GtkTreeView` 家族由四个组件组成。

- `GtkTreeView`：树和列表视图
- `GtkTreeViewColumn`：表示列表或树列
- `GtkCellRenderer`：控制单元格绘制
- `GtkTreeModel`：表示树和列表数据

```c
);

void closeApp (GTtkWidget *window, gpointer data)

{

  gtk_main_quit();

}

int main (int argc, char *argv[])

{

  GtkWidget *window;

  GtkTreeStore *store;

  GtkWidget *view;

  GtkTreeIter parent_iter, child_iter;

  GtkCellRenderer *renderer;

  gtk_init(&argc, &argv);

  window = gtk_window_new (GTK_WINDOW_TOPLEVEL);

  gtk_window_set_default_size (GTK_WINDOW(window), 300, 200);

  g_signal_connect (window, "destroy", GTK_SIGNAL_FUNC (closeApp), NULL);
```

树存储（tree store），传入每列的数量和类型：

1. 在这里我们创建树存储，传入每列的数量和类型：
   ```c
   store = gtk_tree_store_new (N_COLUMNS, G_TYPE_STRING, G_TYPE_STRING, G_TYPE_STRING);
   ```

2. 下一步向树中添加父行和子行。
   ```c
   gtk_tree_store_append (store, &parent_iter, NULL);
   gtk_tree_store_set (store, &parent_iter, COLUMN_TITLE, "Dark Side of the Moon", COLUMN_ARTIST, "Pink Floyd", COLUMN_CATALOGUE, "B000024D4P", -1);
   gtk_tree_store_append (store, &child_iter, &parent_iter);
   gtk_tree_store_set (store, &child_iter, COLUMN_TITLE, "Speak to Me", -1);
   ```
   ```c
   view = gtk_tree_view_new_with_model (GTK_TREE_MODEL (store));
   ```

3. 最后我们向视图中添加列，设置它们的数据源和标题。
   ```c
   renderer = gtk_cell_renderer_text_new ();
   gtk_tree_view_insert_column_with_attributes (GTK_TREE_VIEW(view), COLUMN_TITLE, renderer, "text", NULL);
   gtk_tree_view_insert_column_with_attributes (GTK_TREE_VIEW(view), COLUMN_ARTIST, renderer, "text", COLUMN_ARTIST, -1);
   ```

# 第16 章

```c
NULL;

gtk_tree_view_insert_column_with_attributes (GTK_TREE_VIEW(view),

COLUMN_CATALOGUE,

"Catalogue", renderer,

"text", COLUMN_CATALOGUE,

NULL);

gtk_container_add (GTK_CONTAINER (window), view);

gtk_widget_show_all (window);

gtk_main ();

return 0;

}
```
