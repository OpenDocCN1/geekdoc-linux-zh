
```c
      NULL);

/* ... 设置窗口标题和大小 ... */

gtk_widget_set_size(GTK_WIDGET(window), 200, 200);

/* ... 创建一个新的垂直框来存储控件 ... */

main_vbox = gtk_vbox_new(FALSE, 1);

/* ... 边框宽度为 1 ... */

gtk_container_border_width(GTK_CONTAINER(main_vbox), 1);

/* ... 将垂直框添加到主窗口 ... */

gtk_container_add(GTK_CONTAINER(window), main_vbox);

/* ... 使垂直框可见 ... */

gtk_widget_show(main_vbox);

/* ... 将窗口与 X Window 关联以创建位图 ... */

gtk_widget_realize(window);

/* ... 创建菜单/工具栏 ... */

CreateMenu(window, main_vbox);

CreateText(window, main_vbox);
```

```c
/* --- 显示顶层窗口 ... */

gtk_widget_show(window);
```

```c
/* 循环并处理消息 ... */

gtk_main();
```

```c
return(0);
```

## menu.c

定义工具栏图标并创建菜单和工具栏按钮的代码位于此文件中。此处的大部分代码与之前创建的简单前端相同。

`menu.c` 中的第一块代码定义了工具栏的位图，这些位图应该易于识别且清晰。通常，你应该将位图中使用的颜色数量限制在四种以内——通常更少。颜色过多会分散对位图目的的注意力，位图应该提供可识别的功能。由于许多应用程序使用熟悉的图标来执行功能，因此你应该遵循标准。使用一套新图标可能会让用户感到更加困惑。工具栏按钮的图标重用了之前几个章节中的内容。

从 `main` 调用的 `CreateMenu` 设置了加速表和菜单，并最终调用 `CreateToolbar` 函数来（显而易见地）创建工具栏。菜单项的回调带有 `menu` 前缀，以便将其与普通函数区分来。例如，当选择 File->New 菜单时，将调用 `menu_New` 函数。

```c
/*
CreateMenu
 * 创建主窗口以及与其关联的菜单/工具栏
 */

void CreateMenu(GtkWidget *window, GtkWidget *vbox)
{
  GtkWidget *menubar;
  GtkWidget *menu;
  GtkWidget *menuitem;
  win_main = window;
  /* --- 创建加速表 ... */
  accel_group = gtk_accel_group_new();
  accel_group = gtk_accel_group_attach(accel_group, GTK_OBJECT(window));
  /* 菜单栏 ... */
  menubar = gtk_menu_bar_new();
  gtk_box_pack_start(GTK_BOX(vbox), menubar, FALSE, 0);
  gtk_widget_show(menubar);
  /* 文件 菜单 */
  menu = gtk_menu_submenu(menubar, "File");
  menuitem = gtk_menu_item_new_with_label("New");
  gtk_menu_shell_append(GTK_SHELL(menu), menuitem);
  // ... 菜单项继续 ...
  menuitem = gtk_menu_item_new_with_label("Open");
  gtk_menu_shell_append(GTK_SHELL(menu), menuitem);
  menuitem = gtk_menu_item_new_with_label("Import");
  gtk_menu_shell_append(GTK_SHELL(menu), menuitem);
  menuitem = gtk_menu_item_new_with_label("Save");
  gtk_menu_shell_append(GTK_SHELL(menu), menuitem);
  menuitem = gtk_menu_item_new_with_label("Save As");
  gtk_menu_shell_append(GTK_SHELL(menu), menuitem);
  menuitem = gtk_menu_item_new_with_label("Quit");
  gtk_menu_shell_append(GTK_SHELL(menu), menuitem);
  /* 编辑 菜单 */
  menu = gtk_menu_submenu(menubar, "Edit");
  menuitem = gtk_menu_item_new_with_label("Cut");
  gtk_menu_shell_append(GTK_SHELL(menu), menuitem);
  menuitem = gtk_menu_item_new_with_label("Copy");
  gtk_menu_shell_append(GTK_SHELL(menu), menuitem);
  menuitem = gtk_menu_item_new_with_label("Paste");
  gtk_menu_shell_append(GTK_SHELL(menu), menuitem);
  /* 搜索 菜单 */
  menu = gtk_menu_submenu(menubar, "Search");
  menuitem = gtk_menu_item_new_with_label("Find");
  gtk_menu_shell_append(GTK_SHELL(menu), menuitem);
  /* 帮助 菜单 */
  menu = gtk_menu_submenu(menubar, "Help");
  menuitem = gtk_menu_item_new_with_label("About");
  gtk_menu_shell_append(GTK_SHELL(menu), menuitem);
  /* 创建工具栏 */
  CreateToolbar(vbox);
}
```

`CreateMenuItem` 函数的最后部分是 `CreateToolbar` 函数，它负责创建工具栏。大部分工具栏按钮重用了之前显示如何创建前端的示例。放入工具栏的按钮是简单的按钮。这些按钮设置了 GTK+ 在按下时调用 `menuNew` 函数，这正是 File->New 选择所调用的函数。

```c
/*
CreateToolbar
 * 创建常用选项的工具栏
 */

void CreateToolbar(GtkWidget *vbox_main)
{
  /* 创建工具栏并将其添加到窗口 */
  toolbar = gtk_toolbar_new(GTK_ORIENTATION_HORIZONTAL, GTK_TOOLBAR_ICONS);
  gtk_box_pack_start(GTK_BOX(vbox_main), toolbar, FALSE, TRUE, 0);
  gtk_widget_show(toolbar);
  /* ... 创建 新按钮 ... */
  gtk_toolbar_append_item(GTK_TOOLBAR(toolbar),
    NULL, "New window", NULL,
    CreateWidgetFromXpm(win_main, (gchar **) xpm_new),
    (GtkSignalFunc) menu_New,
    NULL);
  /* ... 创建 打开按钮 ... */
  gtk_toolbar_append_item(GTK_TOOLBAR(toolbar),
    "Open Dialog", "Open dialog",
    CreateWidgetFromXpm(win_main, (gchar **) xpm_open),
    (GtkSignalFunc) menu_Open,
    NULL);
  /* ... 一小间隙 ... */
  gtk_toolbar_append_space(GTK_TOOLBAR(toolbar));
  /* ... 创建 剪切按钮 ... */
```
