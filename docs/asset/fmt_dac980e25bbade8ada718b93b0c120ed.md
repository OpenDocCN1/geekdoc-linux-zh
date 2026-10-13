
第 1 行和第 2 行从树 `GtkTree` 获取选择并移除所有被选中项。第 4 行和第 5 行获取选中的树项。第 7 行和第 8 行说明在移除项时选择 `GList` 会发生变化，因此将复制的 `GList` 保存到另一个。第 9 行到第 14 行循环处理 `selected_items`。第 16 行到第 22 行说明如果选择中有项，则移除它们。

# 使用树

```c
7:   /* 删除子树中的所有项，如果该子树不为空
8:   则也将删除子树。 */
9:   gtk_tree_clear_items(GTK_TREE(tree), 0, -1);
10:  /* 如果子树是空的，之前的函数将不会
11:  删除它。此时需要显式地删除它。 */
12: if(GTK_TREE_ITEM_SUBTREE(tree_item))
13:  {
14:    gtk_tree_item_remove_subtree(GTK_TREE_ITEM(tree_item));
15:  }
16: 
17:  /* 创建一个新的 GtkTree 小部件并将其设置为折叠项的
18:  的子树。 */
19:  tree = gtk_tree_new();
20:  gtk_tree_item_set_subtree(tree_item, tree);
21: }

23: void expand_handler(GtkTreeWidgetItem *tree_item, GtkTree *parent_tree)
24: {
25:   GtkWidget *tree = NULL;
26:   int counter = 0;
27:   GtkWidget *new_tree_item = NULL;
28:   GtkWidget *sub_tree = NULL;
29: 
30:   tree = GTK_TREE_ITEM_SUBTREE(tree_item);
31: 
32:   /* 在添加新项之前，验证子树中是否已经存在项。 */
33:   if(!g_list_length(GTK_TREE(tree)->children))
34:   {
35:     /* 创建 10 个新的 GtkTreeWidgetItem 小部件。 */
36:     for(int counter = 0; counter < 10; counter++)
37:     {
38:       new_tree_item = gtk_tree_item_new();
39: 
40:       /* 为该项填充内容。 */
41:       gtk_widget_show_all(new_tree_item);
42:       gtk_object_set_data(GTK_OBJECT(new_tree_item), "parent",
43:       tree);
44:       /* 将信号处理程序连接到新的 GtkTree
45:       树。 */
46:       gtk_signal_connect(GTK_OBJECT(new_tree_item), "collapse",
47:       (GtkSignalFunc)collapse_handler, tree);
48: 
49:       gtk_signal_connect(GTK_OBJECT(new_tree_item), "expand",
50:       (GtkSignalFunc)expand_handler, tree);
51: 
52: 
53:       /*将新项追加到树中。 */
54:       gtk_tree_append(GTK_TREE(tree), new_tree_item);
55:    /* 为每个新项创建一个空的子树。 */
56:    sub_tree = gtk_tree_new();
57:    gtk_tree_item_set_subtree(GTK_TREE_ITEM(new_tree_item,
58:                               sub_tree);
59: 
60: 
61: }
```

`collapse_handler()` 函数从折叠树项的子树中删除所有项（第 5–9 行）。这通常会删除子树本身，除非它已经是空的。如果在一个已经折叠的项上点击鼠标右键，可能会出现此情况。在这种情况下，必须显式地删除子树（第 10–15 行）。会创建一个新的空树（第 19 行），并将其设置为折叠项的子树行（第 20 行）。如果不这样做，该树项将变成叶子节点且无法再次展开。

`expand_handler()` 函数首先检查已展开的项是否已经拥有子项（第 34 行）。如果在一个已经展开的项上点击鼠标中间，子树可能会被填充。只有空子树才应该被填充。子树将填充 10 个新的树项（第 37–40 行，以及第 52 行和第 53 行）。折叠和展开信号被连接到新项上（第 46–51 行），并且每个新项都会获得一个新的子树（第 55–58 行）。这允许新树项的子项也可以动态生成。

# 为 GtkTree 模拟聚焦项

`GtkTree` 小部件会在获得聚焦的项周围显示熟悉的黑色矩形。然而，目前没有提供程序化的支持来提供获取所聚焦项的功能。因此，我们将自己编写一些代码来模拟此功能。该模拟可以分为三个部分：

- 1. 记住上一次访问的项。
- 2. 获取聚焦项。
- 3. 在使用聚焦项之前验证其是否仍然有效。

## 记住上一次访问的项

为了记住上一次访问的 `GtkTreeItem`（即聚焦项），将它的指针作为对象数据存储在根 `GtkTree` 中。这必须在 `select_child` 信号的句程序中完成。

列表 16.7 是为了模拟 `GtkTree` 焦点元素而需要添加到 `select_child` 信号句程序中的额外代码。

### 16.7 GtkTree 焦点元素模拟

```c
1: void select_child_handler(GtkTree *tree,
2:   GtkWidget *tree_item,
3:   gpointer user_data)
4: {
5:   /* 其他代码 */
6: 
7:   gtk_object_set_data(GTK_OBJECT(GTK_TREE(tree)),
8:     "focus", tree_item);
9: 
10:  /* 其他代码 */
11: }
```

## 获取聚焦项

以下函数通过从根树获取数据来返回聚焦项。它的参数是任意子树的指针。

### 16.8 GtkTree 焦点元素模拟——get_focused_item()

```c
1: GtkWidget *focused_item(GtkTree *tree)
2: {
3:   GtkWidget *focused_item = NULL;
4: 
5:   focused_item = gtk_object_get_data(GTK_OBJECT(GTK_TREE(tree)),
6:     "focus");
7: 
8:   return focused_item;
9: }
```

## 验证聚焦项

以下函数在使用聚焦项之前检查其仍然有效。如果此检查失败，则返回 -1。

```c
1: int is_focused_item(GtkTree *tree)
2: {
3:   GtkWidget *focused_item = get_focused_item(tree);
4: 
5:   if(focused_item)
6:     return 1;
7:   else
8:     return -1;
9: }
```

# GtkTree 的滚动条

## GtkTree 的滚动条

为 `GtkTree` 添加滚动条简单方法是将 `GtkTree` 嵌入到滚动窗口中。`GtkTree` 小部件本身不提供视口，因此必须使用 `gtk_scrolled_window_add_viewport()` 函数。

# 列表 16.10 为 GtkTree 添加滚动条的示例

| | |

|---|---|

|1: GtkWidget *scrolled_window = NULL; | |

| 2: GtkWidget *tree = NULL; | |

| 3: | |

| 4: scrolled_window = gtk_scrolled_window_new(NULL, NULL); | |

| 5: tree = gtk_tree_new(); | |

| 6: gtk_scrolled_window_add_viewport( | |

| 7: GTK_SCROLLED_WINDOW(scrolled_window), tree); | |

它们的参数含义如下：

| 参数 | 说明 |

| --- | --- |

| tree | 指向包含将要选中或取消选择项的 `GtkTree` 的指针。 |

| item | 将要选中或取消选择的 `GtkTreeItem` 在父级树中的位置。 |
