
## 使用 Athena 和 Motif 小件

第 29 章

接下来，我们为 Motif Strings 数组的每个元素定义值，并在创建 Motif List 小件时使用该数组。

```
motif_strings[0] = XmStringCreateSimple("list item at index 0");
motif_strings[1] = XmStringCreateSimple("list item at index 1");
motif_strings[2] = XmStringCreateSimple("list item at index 2");

XSetArg(arg[0], XmWidgetCount, 3);
XSetArg(arg[1], XmWidgetItems, motif_strings);
XSetArg(arg[2], XmVisibleItemCount, 3); // 所有列表元素均是可见的
XSetArg(arg[3], XmselectionPolicy, XmSINGLE_SELECT);
```

```
list = XmCreateList(top_level, "list", arg, 4);
```

我们为创建 `List` 小件指定了四个参数：

- 列表元素的数量
- 列表元素的数据
- 应该可见的列表元素数量
- 一次只能选择一个列表项

如果我们允许多项选择，那么我们必须重写回调函数 `do_list_click` 来处理获取多个选择。在创建 `List` 小件后，我们为该小件指定回调函数 `do_list_click`，使 `List` 小件变为 Top-Level 顶层小件可见，并处理 X 事件：

```
XtAddCallback(list, XmSingleSelectionCallback,
    (XtCallbackProc)do_list_click, NULL);
XtManageChild(list);
XtRealizeWidget(top_level);
XtMainLoop();
```

图 29.6 显示了在 KDE 桌面环境下运行的 `list.c` 程序。

图 29.6

Motif List 小件示例。

![](img/681a495129beb6adf91e7ff7f87e7dd4_510_0.png)

你可以通过切换目录到 `src/X/Motif` 并输入以下命令来编译并运行此程序：

```
make
list
```
