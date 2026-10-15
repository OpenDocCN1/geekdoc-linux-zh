
```c
void
gtk_menu_bar_insert(GtkMenuBar *menu_bar, GtkWidget *child,
gint position);
```

`gtk_menu_bar_insert()` 函数接收一个额外的参数。假设通过调用 `gtk_menu_bar_insert()`，菜单栏现在有 `n` 个项。将 `position` 设置为 `-1`、`n` 或任何大于 `n` 的值，其效果与调用 `gtk_menu_bar_append()` 相同。将 `position` 设置为 `0` 等于调用 `gtk_menu_bar_prepend()`。将 `position` 设置为 `[1, n-1]` 范围内的值将导致菜单项被插入到菜单栏中对应的位置。

## 设置阴影类型

这里讨论的最后一个函数 `gtk_menu_bar_set_shadow_type()` 允许你设置应用于整个菜单栏的阴影类型：

```c
void
gtk_menu_bar_set_shadow_type(GtkMenuBar *menu_bar,
GtkShadowType type);
```

关于 `type` 可能值的描述和插图，请参阅第 6 章中 `gtk_list_set_shadow_type()` 的讨论。

我将在下一节中展示代码，说明如何使用 `gtk_menu_bar_new()` 和 `gtk_menu_bar_append()` 函数。为了给出一个有意义的示例，我首先需要描述 `GtkMenuItem` 是如何工作的，我将在后续节介绍。

# GtkMenuItem

## 类名

`GtkMenuItem`

## 父类名

`GtkItem`

## 宏

小控件类型宏：`GTK_TYPE_MENU_ITEM`

对象到小控件转换宏：`GTK_MENU_ITEM(obj)`

小控件类型检查宏：`GTK_IS_MENU_ITEM(obj)`

## 支持的信号

表 9.5 信号

| 信号名称 | 触发信号的条件 |
|--- |--- |
| activate | 用户激活了该菜单项。 |

## 信号函数原型

```c
void
activate(GtkMenuItem *menuitem, gpointer user_data);
```

## 应用级 API 摘要

在运行时获取常量 `GTK_TYPE_MENU_ITEM`。

`GtkType`

`gtk_menu_item_get_type(void);`

创建一个新的 `GtkMenuItem` 实例：

```c
GtkWidget *
gtk_menu_item_new(void);
```

## 应用级 API 摘要（继续）

将菜单与菜单项关联：

```c
void
gtk_menu_item_set_submenu(GtkMenuItem *menu_item, GtkWidget *submenu);
```

从菜单项中移除菜单：

```c
void
gtk_menu_item_remove(GtkMenuItem *menu_item);
```

设置菜单项的放置属性（`Gtk_TOP` 或 `Gtk_BOTTOM`）：

```c
void
gtk_menu_item_set_placement(GtkMenuItem *menu_item, GtkPlacement placement);
```

通过用户选择菜单项来显示该菜单项：

```c
void
gtk_menu_item_select(GtkMenuItem *menu_item);
```

撤销调用 `menu_item_select()` 的效果：

```c
void
gtk_menu_item_deselect(GtkMenuItem *menu_item);
```

通过用户点击菜单项来激活指定的菜单项：

```c
void
gtk_menu_item_activate(GtkMenuItem *menu_item);
```

将最后一个菜单项右对齐：

```c
void
gtk_menu_item_right_justify(GtkMenuItem *menu_item);
```

## 类描述

`GtkMenuItem` 实现了菜单项的视觉外观和行为。菜单项以文本形式在菜单栏（例如，“文件”）或菜单（例如，“打开”）中显示。一个菜单项可以关联一个子菜单。没有子菜单的菜单项在被激活时，将调用分配给它的激活信号函数。带有子菜单的菜单项被激活时，将显示该子菜单。

## 创建菜单项

创建一个 `GtkMenuItem` 实例类似于创建一个新的 `GtkLabel`。要创建一个没有标签的菜单项，只需调用 `gtk_menu_item_new()`：

```c
GtkWidget *
gtk_menu_item_new(void);
```

`GtkMenuItem` 是 `GtkContainer` 的实例，因此可以通过调用 `container_add()` 为菜单项关联标签。例如：

```c
GtkWidget *label, *menu_item;
label = gtk_label_new("File");
gtk_container_add(GTK_CONTAINER(menu_item), label);
```

我将在本节介绍不使用 GtkFactory 时，说明单独创建菜单项及其标签的重要性。

如果你愿意，也可以在创建菜单项时通过调用 `gtk_menu_item_new_with_label()` 指定菜单项显示的标签：

```c
GtkWidget *
gtk_menu_item_new_with_label(const gchar *label);
```

参数是一个 NULL 终止的 C 字符串。注意，`gtk_menu_item_new_with_label()` 不像 Gtk2 那样解析你在标签中指定的任何下划线 `_` 字符来识别快捷键。由于此原因，`gtk_menu_item_new()` 是更好的选择，这样菜单项可以关联一个快捷键序列。我将在本节末尾提供一个示例说明为什么这样做。

## 子菜单

子菜单可以与任何菜单项关联。没有子菜单的菜单项在被激活时，将调用分配给它的激活信号函数。带有子菜单的菜单项被激活时，将显示该子菜单。（如果选中的菜单项位于菜单栏中，子菜单通常垂直显示。如果菜单项位于菜单中，子菜单通常显示为弹出菜单。）

将子菜单与菜单项关联或从菜单项中移除子菜单是简单的。只需调用 `gtk_menu_item_set_submenu()`：

```c
void
gtk_menu_item_set_submenu(GtkMenuItem *menu_item, GtkWidget *submenu);
```

参数 `menu_item` 是 `GtkMenuItem` 或其任一子类的实例。参数 `submenu` 是 `GtkMenu` 的实例。将在后续代码中给出该函数的调用示例。

# 第 9 章 • 菜单

要移除菜单项的子菜单，请调用 `gtk_menu_item_remove_submenu()`：

```c
void
gtk_menu_item_remove_submenu(GtkMenuItem *menu_item);
```

菜单项的布局定义了子菜单相对于菜单项的位置，该菜单项激活后将显示子菜单。`gtk_menu_item_set_placement()` 程允许你指定此项偏好：

```c
void
gtk_menu_item_set_placement(GtkMenuItem *menu_item,
GtkSubmenuPlacement placement);
```

参数可以是 `GTK_TOP_BOTTOM` 或 `GTK_LEFT_RIGHT`。默认情况下，菜单栏中对应菜单项的子菜单布局为 `GTK_TOP_BOTTOM`，而传统菜单中对应菜单项的子菜单布局为 `GTK_LEFT_RIGHT`。

## 右对齐的菜单项

大多数读者都见过标记为“帮助”的菜单项，它位于菜单栏的最右侧，如图 9.1 所示。在 Gtk+ 中，你调用 `gtk_menu_item_right_justify()` 函数来设置菜单的位置：

```c
void
gtk_menu_item_right_justify(GtkMenuItem *menu_item);
```

`gtk_menu_item_right_justify()` 函数接受一个参数，即要放置在菜单栏最右侧的菜单项。该菜单项必须在菜单栏中，这一点很重要；指定的菜单项右侧不能有其他菜单项（参见前文的 `gtk_menu_item_insert`）。如果不符合此情况，则对 `gtk_menu_item_right_justify()` 的调用将不起作用（no-op）。

# 选择和取消选择菜单项

剩余的 `GtkMenu` API 调用很少会出现在典型的 Gtk+ 程序中。

第一个函数 `gtk_menu_item_select()` 可用于选择指定的菜单项以便在选中模式下显示。也就是说，`gtk_menu_item_select()` 的作用就像用户弹出了包含该菜单项的菜单，并移动到该菜单但没有激活它（参见本节稍后介绍 `gtk_menu_item_activate()`）：
