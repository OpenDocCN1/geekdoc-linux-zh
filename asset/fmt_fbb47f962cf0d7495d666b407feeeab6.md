
在第 001 到 005 行，我定义了一个类型 `MenuItem`，它包含三个字段。第一个字段是一个整数，通过“activate”信号函数 `event_menu_cb()` 的 `callback_data` 传递，该函数定义在第 007 到 010 行。将此值（每个都是常量值，例如 `RUNNING` 设置为 1，`CYCLING` 设置为 2）作为信号函数的参数的好处是，它可以告诉信号函数哪个单选菜单项被激活了。`MenuItem` 的第二个字段定义单选项的标签。第三个也是最后一个字段是指信号函数的指针，当用户激活单选菜单项时将调用该函数。菜单中包含的所有单选菜单项的定义显示在第 012 到 018 行。

`build_menu()` 函数负责根据传递给它的参数类型 `MenuItem` 类型创建菜单（参见第 049 行的调用示例）。在第 028 行，当 `GtkMenu` 创建时；第 031 到 041 行循环中的每个单选菜单项都将被添加到此菜单中（这在第 039 行通过 `gtk_menu_append()` 完成）。

让我们了解单选菜单项是如何创建并添加到单选组的。在第 029 行，`"group"` 变量被设置为 `NULL`。这将是第 032 行在循环中调用 `gtk_radio_menu_item_with_label()` 时的值。由于第一个单选菜单项是用 `NULL` 组创建的，`GtkRadioMenuItem` 将创建一个新的单选组，并将 `Running` 作为其唯一成员。在第 037 行，代码查询 `Running` 单选菜单项的组并将其存储在 `"group"` 变量中。因此，下一次调用 `gtk_radio_menu_item_with_label()` 时，`"group"` 参数将被设置为它所属的 `Running` 单选菜单项。结果是，下一个单选菜单项 `Cycling` 将添加到 `Running` 菜单项所属的组。从现在起，返回的组将始终是之前创建的单选菜单项所在的同一个组。因此，所有的单选菜单项将被放在同一个组中，这是想要的结果。

## 设置单选菜单项的单选组

`GtkRadioMenuItem` 支持的最后一个函数是 `gtk_radio_menu_item_set_group()`：

```c
void
gtk_radio_menu_item_set_group(GtkRadioMenuItem *radio_menu_item,
GtkList *group);
```

此函数接收一个单选菜单项和一个组（通过调用 `gtk_radio_menu_item_group()` 从其他单选菜单项获取）。该单选菜单项将从它所属的组中移除并被于指定的组。

## GtkTearoffMenuItem

### 类名

`GtkTearoffMenuItem`

### 父类名

`GtkMenuItem`

### 宏

- 小部件类型宏：`GTK_TYPE_TEAROFF_MENU_ITEM`
- 对象到小部件的转换宏：`GTK_TEAROFF_MENU_ITEM(obj)`
- 小部件类型检查宏：`GTK_IS_TEAROFF_MENU_ITEM(obj)`

### 应用级 API 摘要

在运行时获取常量 `GTK_TYPE_TEAROFF_MENU_ITEM`：

```c
GtkType
gtk_tearoff_menu_item_type(void);
```

创建一个新的 `GtkTearoffMenuItem` 实例：

```c
GtkWidget *
gtk_tearoff_menu_item_new(void);
```

### 类描述

`GtkTearoffMenuItem` 是 `GtkMenuItem` 的子类。大多数情况下，这意味着 `GtkTearoffMenuItems` 可以用于任何使用 `GtkMenuItem` 实例的地方。然而，分离菜单项（tearoff menu items）是一种特殊的菜单项，因为该菜单项没有回调函数，也没有管理或包含标签的能力。图 9.3 显示的“选项”菜单就是一个分离菜单。从视觉上看，分离菜单看起来和其他任何菜单都一样，区别在于分离菜单有一个分离菜单项，这在图 9.3 中 `Option1` 菜单项附近的系列虚线表示。

### 使用分离菜单

将鼠标悬停在分离菜单项上并按下鼠标 1 键将导致分离菜单分离并在它自己的顶层窗口中显示，如图 9.4 所示。如你所见，分离菜单项仍然可见；再次选择它将导致分离菜单关闭。通过重复最初显示分离菜单项并将其从菜单栏中分离的步骤也可以关闭分离菜单。当分离菜单处于分离状态时，在菜单中选择菜单项的行为与该菜单项在仍附着在原始、未检测的位置时从菜单中选择的行为相同。用户可以在分离状态下重放菜单并从中选择项目。通常情况下，这并不是问题。例如，使菜单项不可用：

![创建分离菜单](https://example.com/image_44_057.png)

### 创建分离菜单

分离菜单项应通过调用 `gtk_menu_item_new()` 添加到菜单：

```c
GtkWidget *menu_item = gtk_menu_new();
```

一旦创建了菜单，你就可以调用 `gtk_menu_append()` 将菜单项添加到菜单中：

```c
GtkWidget *menu, *menu_item;
menu_item = gtk_menu_new();
gtk_menu_append(menu, menu_item);
gtk_widget_show(menu);
```

这结束了我对 `GtkMenuItem` 的讨论。我下一个将讨论的类 `GtkMenu` 与 `GMenuBar` 类似，因为菜单的基本目的是作为菜单项的容器。菜单栏和菜单之间的主要区别在于，菜单是垂直排列项目的，而菜单栏是水平排列项目的。

## GtkMenu

| 类名 | `GtkMenu` |

| :--- | :--- |

### 父类名

`GtkShell`

### 宏

- 小部件类型宏：`GTK_TYPE_MENU`

### 应用级 API 摘要

在运行时获取常量 `GTK_TYPE_MENU`：

```c
GtkType
gtk_menu_type(void);
```

创建一个新的的 `GtkMenu` 实例：

```c
GtkWidget *
gtk_menu_new(void);
```

将菜单项（子项）添加到菜单的末尾：

```c
void
gtk_menu_append(GtkMenu *menu, GtkWidget *child);
```

将菜单项（子项）添加到菜单的开头：

```c
void
gtk_menu_prepend(GtkMenu *menu, GtkWidget *child);
```

### 应用级 API 摘要（继续）

在菜单的任意位置插入菜单项（子项）：

```c
void
gtk_menu_insert(GtkMenu *menu, GtkWidget *child, gint position);
```

弹出菜单，使用一个可选函数计算其在屏幕上的位置：

```c
void
gtk_menu_popup(GtkMenu *menu, GtkWidget *parent_shell,
GtkWidget *parent_item, GtkMenuPosition func,
gpointer data, guint button, guint2 activate_time);
```

弹出菜单并移除其 X Server 捕取：

```c
void
gtk_menu_popdown(GtkMenu *menu);
```

查询菜单中当前激活的菜单项：

```c
GtkWidget *
gtk_menu_get_active(GtkMenu *menu);
```

设置菜单的激活菜单项：

```c
void
gtk_menu_set_active(GtkMenu *menu, guint index);
```

设置菜单的加速组：

```c
void
gtk_menu_set_accel_group(GtkMenu *menu, GtkAccelGroup *accel_group);
```

将菜单项（子项）添加到菜单的末尾：

### GtkMenu 403

在特定位置设置菜单项（通过范围 [0, n] 中的位置参数指定，其中 n-1 是调用前菜单中已有的菜单项数量）。将位置设置为 -1 等同于调用 `gtk_menu_append()`。`gtk_menu_append()`、`gtk_menu_prepend()` 和 `gtk_menu_insert()` 的函数原型如下所示：

```
void
gtk_menu_append(GtkMenu *menu, GtkWidget *child);
```

```
void
gtk_menu_prepend(GtkMenu *menu, GtkWidget *child);
```

```
void
gtk_menu_insert(GtkMenu *menu, GtkWidget *child, gint position);
```

## 弹出菜单
