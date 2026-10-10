
在大多数应用程序中，“文件”菜单项包含其他菜单项，这些菜单项仅在菜单下拉时才可见。当被选中时，“文件”菜单项不会导致应用程序执行操作。相反，“文件”会打开一个子菜单，其中包含可选择的选项，如“新建”、“打开”和“保存”。因为“文件”实际上关联着一个包含这些其他项的新菜单。在创建一个包含“新建”、“打开”和“保存”选项的新 `GtkMenu` 后，你可以使用另一个 `gtk_menu_item_set_submenu` 函数。

```c
/* ---为“新建”、“打开”等创建新菜单 --- */
menu = gtk_menu_new ();
```

```c
/* 在“文件”菜单项下标记子菜单 -- */
gtk_menu_item_set_submenu(GTK_MENU_ITEM (menuFile), menu);
```

现在你可以向子菜单添加 `GtkMenuItems`。为了简化操作，通过一个函数来向子菜单添加 `GtkMenuItems`：

```c
/*
* CreateSubMenu
* 创建子菜单
* menu - 父菜单
* szName - 子菜单名称
*/
GtkWidget *CreateSubMenu(GtkWidget *menu, char *szName)
{
  GtkWidget *menuitem;
  GtkWidget *submenu;

  /* 创建菜单项 -- */
  menuitem = gtk_menu_item_new_with_label(szName);

  /* 将其添加到菜单 -- */
  gtk_menu_append(GTK_MENU (menu), menuitem);
  gtk_widget_show(menuitem);

  /* 创建子菜单 -- */
  submenu = gtk_menu_new ();
  gtk_menu_item_set_submenu(GTK_MENU_ITEM (menuitem), submenu);

  /* 搞定！ -- */
  return (submenu);
}
```

添加子菜单后，你可以向它添加 `GtkMenuItem`。首先创建一个 `GtkMenuItem`：

```c
menuitem = gtk_menu_item_new_with_label ("New");
```

然后将 `GtkMenuItem` 添加到子菜单并使其可见。

```c
gtk_menu_append (GTK_MENU (submenu), menuitem);
gtk_widget_show(menuitem);
```

当然，菜单还没有执行任何操作。首先，你需要捕获用户选择 `GtkMenuItem` 的事件。`GtkMenuItem` 有一个“activate”信号表示 `GtkMenuItem` 被选中。通过在“activate”信号上放置回调函数，应用程序可以响应用户选择菜单项的操作。

在两个 `GtkMenuItem` 实例之间可以通过调用不带标签的 `gtk_menu_item_new` 函数并将新的 `GtkMenuItem` 添加到子菜单来插入分隔符。这会在菜单中添加一条水平线以分隔命令组。分隔符在长菜单中特别有用。“退出”菜单项应与其他选项分开，以免用户在选择附近的菜单项时误点“退出”。

## 复选菜单

除了处理菜单项外，`GtkCheckMenuItem` 像菜单中的复选框一样，允许你查看和修改布尔值。创建 `GtkCheckMenuItem` 的步骤与创建普通 `GtkMenuItem` 的步骤相似，但你使用的是 `gtk_check_menu_item_new_with_label` 函数，并且你想捕获“toggle”信号。你可以创建一个完成创建 `GtkCheckedMenuItem` 所有工作的函数：

```c
/*
* CreateMenuItem
* 创建带有复选框的菜单项
* menu - 添加检查菜单的父菜单
* szName - 分配给菜单项的名称
* func - 菜单项切换时调用的事件处理器
* data - 传递给事件处理程序的额外信息
*/
GtkWidget *CreateMenuItem(GtkWidget *menu, char *szName, GtkSignalFunc func, gpointer data)
{
GtkWidget *menuitem;

    /* 创建菜单项 -- */
    menuitem = gtk_check_menu_item_new_with_label(szName);

    /* 将其添加到菜单 -- */
    gtk_menu_append(GTK_MENU (menu), menuitem);
    gtk_widget_show(menuitem);

    /* 监听“toggled”消息 -- */
    g_signal_connect(GTK_OBJECT (menuitem), "toggled", func, data);

    return (menuitem);
}
```

复选菜单项可以使用 `gtk_check_menu_item_set_state` 函数进行设置。

```c
/* ... 将其设置为 false ... */
gtk_check_menu_item_set_state (menuitem, FALSE);
```

## 单选菜单项

正如菜单项可以作为复选框一样，菜单项也可以在一个组内充当单选按钮（`GtkRadioMenuItem`）。想要像单选按钮一样运行的菜单项需要使用 `gtk_radio_menu_item_new_with_label` 函数创建，该函数接收单选菜单项要添加的组以及菜单项名称。在添加第一个单选菜单项之前，组的新值需要设为 `NULL`，在添加每个项目后，需要获取该组的值。下面的代码说明了这一过程：

```c
GList *group = NULL;
```

```c
/* 向组中添加 "Tall" ... */
menuitem = gtk_radio_menu_item_new_with_label (group, "Tall");
/* 更新我们添加项的组 ... */
group = gtk_radio_menu_item_group (GTK_RADIO_MENU_ITEM (menuitem));
/* 将菜单项添加到菜单中 ... */
gtk_menu_append (GTK_MENU (menu), menuitem);
/* 显示菜单项 ... */
gtk_widget_show (menuitem);
/* 连接信号处理器 ... */
gtk_signal_connect (GTK_OBJECT (menuitem), "toggled",
                   GTK_SIGNAL_FUNC (TallFunc), NULL);
```

`GtkRadioMenuItem` 继承自 `GtkCheckMenuItem`；因此，信号是相同的，且获取和设置 `GtkRadioMenuItem` 状态的函数与获取和设置 `GtkCheckMenuItem` 状态的函数相同。事实上，可以使用以下代码设置 `GtkRadioMenuItem`：

```c
/* ... 将其设置为 false ... */
gtk_check_menu_item_set_state (GTK_CHECK_MENU_ITEM (menuitem), FALSE);
```

## 工具提示

你可以为用户提供的一个很好的功能是工具提示。工具提示是当鼠标悬过组件时出现、当鼠标移出组件时消失的小型弹出文本窗口。它们为用户提供了关于组件的额外信息；也就是说，工具提示解释了组件的作用。（如果是一个画技糟糕的艺术家在绘制你的工具栏图标，那么工具提示将格别有用。）工具提示主要用于工具栏，也可以用于其他组件。你可以使用 `gtk_tooltips_new` 函数创建一个工具提示。

```c
/* 创建工具提示 ... */
tooltips = gtk_tooltips_new ();
```

在创建工具提示后，你可以使用 `gtk_tooltips_set_tip` 函数将它们添加到菜单项中。

```c
/* 将提示添加到菜单项中 ... */
gtk_tooltips_set_tip (tooltips, menuitem,
"一日一苹果，医生远离我", NULL);
```

你可以通过 `gtk_tooltips_set_colors` 函数让工具提示变得非常色彩丰富。通过传入背景和前景的 `GdkColor`，可以修改工具提示上的颜色。

```c
/* 修改颜色 ... */
gtk_tooltips_set_colors (tooltips, background, foreground);
```

# 第 5 章 菜单、工具栏和工具提示

```c
GTK_SIGNAL_FUNC(func), data;
```

```c
return (menuitem);
}
```
