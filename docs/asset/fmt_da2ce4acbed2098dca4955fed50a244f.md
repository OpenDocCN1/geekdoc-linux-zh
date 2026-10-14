
# GNOME 官方开发者指南

## 4.3. 应用程序窗口

```
  "Delete selection and place into clipboard",

  NULL, G_CALLBACK(edit_handler), "Cut", -1);
```

```
gtk_toolbar_insert_stock(tools, GTK_STOCK_COPY,

  "Copy selection to clipboard",

  NULL, G_CALLBACK(edit_handler), "Copy", -1);
```

```
gtk_toolbar_insert_stock(tools, GTK_STOCK_PASTE,

  "Paste clipboard",

  NULL, G_CALLBACK(edit_handler), "Paste", -1);
```

```
* 将工具栏置于主应用程序窗口 /

gnome_app_set_toolbar(window, tools);
```

此应用程序有一个状态栏，但并未对其进行任何操作。

```
* 添加状态栏 //

gnome_app_set_statusbar(window, GTK_WIDGET(status));
```

主窗口包含一个简单的标签（`label`）：

```
* 使用一个简单的占位符标签作为内容 /

label = g_object_new(GTK_TYPE_LABEL, "label", "Your idea goes here.", NULL);
```

```
/* 将标签设置为应用程序内容 */

gnome_app_set_contents(window, GTK_WIDGET(label));
```

就像你使用 GTK+ 做的那样，显示窗口及其内部的所有内容（除菜单外）。下一页的图 4.1 显示此应用程序。

![](img/ae44ff3edd9313fce71c50baa18b0c66_241_0.png)

```
/* 显示所有内容并启动 GTK+ 主事件循环 */

gtk_widget_show_all(GTK_WIDGET(window));

gtk_main();
```

```
return 0;
```

从这个示例中你应该获得的整体结论是：创建一个 `GnomeApp` 后，你需要将内容放入它的菜单栏、工具栏、主内容窗口和状态栏中。否则，GNOME 应用程序的组件设置与 GTK+ 应用程序并没有显著区别。

## 菜单

有两个容器组件：`GtkMenu` (`GTK_TYPE_MENU`) 用于存放菜单项，`GtkMenuBar` 用于存放多个菜单。从技术上讲，这两个类是垂直菜单容器，而菜单栏是水平容器。它们都是 `GtkMenuShell` 的子类，因此在将组件放入菜单时，你经常会使用 `menu_shell` API。

注意：你可以在应用程序中拥有多个菜单，但这将违反几乎每一条用户友好型 GUI 开发的准则。`GnomeApp` 只定义了一个内置的菜单栏。

要开始使用菜单，你需要创建若干项。菜单容器中的每个项都是 `GtkMenuItem` (`GTK_TYPE_MENU_ITEM`) 或其子类的对象。

`GtkMenuItem` 仅显示文本。它的子类可以实现：

- `GtkImageMenuItem` (`GTK_TYPE_IMAGE_MENU_ITEM`): 图标
- `GtkCheckMenuItem` (`GTK_TYPE_MENU_ITEM`): 复选框项
- `GtkRadioMenuItem` (`GTK_TYPE_MENU_ITEM`): 单选项
- `GtkSeparatorMenuItem` (`GTK_TYPE_MENU_ITEM`): 分隔符

### 4.3.1 应用程序窗口

单选按钮菜单项有点复杂，因为它们通过一个 `GList` 参数进行分组：

```
gtk_radio_item_new_with_mnemonic(group, label)
```

通过这种方法，你很少需要处理实际元素。这里有一个示例：

```
GList *group = NULL;

GtkWidget *radio[4];

int i;

gchar *text[] = {

  "CD",

  "Phono",

  "Tape",

  "Tune"

};

for (i = 0; i < 4; i++) {

  radio[i] = gtk_radio_menu_item_new_mnemonic(group, text[i]);

  group = gtk_radio_menu_item_get_group(GTK_RADIO_MENU_ITEM(radio[i]));

}
```

```
g_object_set(radio[1], "active", TRUE, NULL);
```

确保在创建一组单选项后，你将默认项的属性设为 `TRUE`。`GtkRadioMenuItem` 是 `GtkCheckMenuItem` 的子类，因此除了 `active` 属性外，它还继承了 `toggled` 信号。

如果你不想允许键盘操作你的菜单项，请使用以下函数之一（它们的操作与对应的 `_mnemonic` 版本相似，但在标签中使用的是下划线）：

- `gtk_menu_item_new_with_label(label)`
- `gtk_image_menu_item_new_with_label(label)`
- `gtk_check_menu_item_new_with_label(label)`
- `gtk_radio_menu_item_new_with_label(group, label)`

要在菜单中创建一条线（例如，将一组单选项与其他项隔开），请使用

```
gtk_separator_menu_item_new();
```

现在你已经有了菜单项，必须将它们添加到菜单中。`GtkMenuShell` API 执行这些操作：

- `void gtk_menu_shell_append(GtkMenuShell *menu, GtkWidget *child)`：将 `child` 添加到菜单的（底部或右侧）。
- `void gtk_child_prepend(GtkMenuShell *menu, GtkWidget *child)`：将子项添加到菜单的顶部（或左侧）。
- `void gtk_menu_shell_insert(GtkMenuShell *menu, GtkWidget *child, gint position)`：在菜单的指定位置 `position` 处插入 `child`。菜单中的第一个位置是 0。

在将所有项目都放入菜单后，你需要某种方法来激活菜单。构建一个包含菜单标题（例如“文件”和“编辑”）的 `GtkMenuBar` 容器。用户就是通过点击这些标题来激活常规虚拟菜单的，因此，你真正想要做的是将一个子菜单附加到菜单栏上（如果这听起来很困惑，请参考示例程序查看其在实践中是如何运作的）。若要将子菜单附加到菜单项上：

```
gtk_menu_item_set_submenu(menu_item, submenu)
```

注意，`menu_item` 是一个 `GtkMenuItem` 对象，而 `submenu` 是一个 `GtkWidget`。如果你将项目声明为 `GtkWidget`，则需要对其进行一些类型转换。
若要移除某项，你需要：

```
gtk_menu_item_remove_submenu(menu_item)
```

总结来说，要使用菜单栏构建层次结构，请遵循以下步骤：

1. 根据这些指南创建菜单项：
   - 通常情况下，使用 `with_mnemonic` 生成器创建具有唯一快捷键的标签。
   - 如果普通的 `GtkMenuItem` 对象不包含子菜单，则设置其激活（`activate`）信号处理程序。
   - 对于 `GtkImageMenuItem`，设置 `image` 属性以指定自定义图像。使用标准项目（stock items），你需要一个 `AccelGroup` 对象来管理指向键盘操作的句柄。
   - 对于 `GtkCheckMenuItem`，你可能想为切换（`toggled`）状态附加处理程序。
   - 对于 `RadioMenuItem`，你需要一个列表来管理单选按钮组。你还应该将组中的其中一个单选项设置为激活状态（这意味着它是默认按钮）。
2. 创建一个菜单栏并为其填充项目以激活你的每个菜单。在此之前，分配唯一的键盘操作。
3. 为菜单栏创建子菜单，并填充步骤 1 中的项目。如果需要，你可以在步骤 2 之前（或同时）执行此操作。
4. 将每个子菜单附加到菜单栏中对应的项上。

获取菜单栏后，使用以下代码将其放入你的 GNOME 应用程序窗口：

```
gnome_app_set_menus(window, menu_bar)
```

最后，使用以下代码显示菜单栏：

```
gtk_widget_show_all(menu_bar)
```
