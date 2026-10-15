
`handle_option(gpointer data, guint callback_action, GtkWidget *w)`

{
    `GtkMenuItem *newmenu = (GtkMenuItem *)w`;
}

`static GtkItemFactoryEntry menu_items[] = {`
    `"/Option1", NULL, handle_option, 1, NULL,`
    `"/Option2", NULL, handle_option, 2, NULL,`
    `"/Option3", NULL, handle_option, 3, NULL,`
    `"/Option4", NULL, handle_option, 4, NULL`
};

```
# GtkOptionMenu
```c
void get_option_menu (GtkWidget **menu)
{
    GtkAccelGroup *accel_group;
    int nmenu_items = sizeof(menu_items) / sizeof(menu_items[0]);
    item_factory = gtk_item_factory_new(GTK_TYPE_MENU, "<options>", NULL);
    gtk_item_factory_create_items(item_factory, nmenu_items, menu_items, NULL);
    if (menu)
        *menu = gtk_item_factory_get_widget(item_factory, "<options>");
}
int main (int argc, char *argv[])
{
    GtkWidget *menu;
    GtkWidget *optionMenu;
    gtk_init (&argc, &argv);
    get_option_menu(&menu);
    optionMenu = gtk_option_menu_new();
    gtk_option_menu_set_menu (GTK_OPTION_MENU (optionMenu), menu);
    gtk_main ();
    return(0);
}
```

在 `040` 行，调用了 `get_option_menu()`。此函数（`018` 到 `029` 行）创建了将绑定到选项菜单的菜单。在 `041` 行，创建了 `GtkOptionMenu` 实例。`040` 行创建的菜单通过 `gtk_option_menu_set_menu()` 绑定到选项菜单。

菜单在 `011` 到 `016` 行定义。定义每个菜单项的 `GtkItemFactoryEntry` 字段设置为 `NULL`。通常选项菜单中不使用加速键。每当用户在选项菜单中选择项时，都会调用 `handle_option()` 函数。每个菜单项都有一个 `callback_action` 字段（`1, 2, 3` 或 `4`），该字段将作为回调 `handler_function()` 的第二个参数传递。`handle_option()` 函数可以使用此参数告知用户选择了菜单中的哪一个项，从而跟踪用户对选项菜单进行的更改。在某处存储 `callback_action` 是很有用的；如果用户提交了对包含选项菜单对话框的更改，我将保存最后记录的值。例如，如果选项菜单包含红色、绿色和蓝色选项，并且选项菜单被用于编辑某些数据结构中名为 `"color"` 的字段：

```c
typedef struct _myData
{
  int color;
} MyData;
static MyData myData;
```

我可能会定义以下常量：

```c
#define COLOR_RED 0x00
#define COLOR_GREEN 0x01
#define COLOR_BLUE 0x02
```

以及持有当前选择的静态变量：

`static gint color;`

使用以下内容定义菜单：

```c
static GtkItemFactoryEntry menu_items[] = {
  "/Red", NULL, handle_option, COLOR_RED, NULL,
  "/Green", NULL, handle_option, COLOR_GREEN, NULL,
  "/Blue", NULL, handle_option, COLOR_BLUE, NULL
};
```

回调函数的代码为：

```c
static void
handle_option(gpointer data, guint callback_action, GtkWidget *w)
{
  color = callback_action;
}
```

当用户提交包含选项菜单的对话框时，存储在变量 `"color"` 中的值将复制到分配给对话框 `Commit`（提交）或 `OK` 按钮的 `"clicked"` 信号函数的 `MyData` 中：

`myData.color = color;`

# 初始化选项菜单选择

关于选项菜单，还有一个最后问题需要解决：如何初始化选项菜单菜单的当前选择。例如，如果在之前的 `"color"` 菜单中做的最后选择是绿色，我们希望初始化选项菜单的菜单，以便在下次显示该数据的选项菜单时，绿色是当前选择。要设置选项菜单菜单的选择，请调用 `gtk_option_menu_set_history()`：

参数 `option_menu` 是 `GtkOptionMenu` 的实例。参数索引范围在 `[0, n-1]` 之间，其中 `n` 是选项菜单中项目的数量。注意前文中，我如何将常量 `COLOR_RED`、`COLOR_GREEN` 和 `COLOR_BLUE` 分别定义为 `0`、`1` 和 `2`。这使得直接从数据初始化选项菜单变得简单，例如：

```c
GtkOptionMenu *myOptionMenu;
```

...

```c
gtk_option_menu_set_history(myOptionMenu, myData.color);
```

在选项菜单创建（通过调用 `gtk_option_menu_new()`）并且其菜单附加（通过调用 `gtk_option_menu_set_menu()`）之后，你可以任何时候调用 `gtk_option_menu_set_history()`。大多数应用程序会在将选项菜单提供给用户之前，只设置一次选项菜单的历史，因为通常来说，对选项菜单的更改应该只由用户完成，而不是由应用程序完成。

## 总结

`Gtk+1.2` 支持多种与菜单相关的控件。向应用程序中添加菜单的最简单方法是使用 `GtkItemFactory`：首先创建一个数据结构来定义菜单的组织和内容，并指定为菜单中的项调用的回调函数。然后，你将此数据结构传递给 `GtkItemFactory`，它将实现你描述的菜单系统。随后，你可以从 `GtkItemFactory` 获取实现该菜单的控件，并将该控件添加到应用程序的任意窗口中。

菜单的内容由多个菜单项目组成。例如，某些应用程序中的“编辑”菜单有“剪切”、“复制”和“粘贴”项目。`Gtk+` 支持多种类型的菜单项目。除了大多数菜单中常见的类型（`GtkMenuItem` 实例）外，还支持单选菜单项目（`GtkRadioMenuItem`，允许你在菜单的多个项目中的选择一个）和复选菜单项目（`GtkCheckMenuItem`，允许你在菜单中选择多个项目）。抽离式菜单（Tear menus）可以从其父级分离并在单独窗口中显示。抽离式菜单会保留在桌面上，直到用户或应用程序显式地关闭它们。`Gtk+` 允许菜单在任意窗口位置弹出；我在本章中说明了弹出和下拉菜单的技术。最后，`Gtk+` 支持的选项菜单解决了为用户提供一个可以从中选择多个项目的控件的问题，当当项目列表太大而无法以一组单选按钮的形式显示，又小到无法作为列表控件显示时。选项菜单有时用于用户界面空间受限的情况（即一组单选按钮或列表简单地占据了太多空间）。

# 第 10 章

## 容器与基类类

本章以及接下来的章节将介绍构成 `Gtk+ 1.2` 工具包的容器控件。

容器类在 `Gtk+` 中起着至关重要的作用，就像在 `X Window` 系统、`macOS` 和 `MS Windows`（以及无数其他平台）的其他工具包和控件集中一样。在 `X Window` 系统世界中，`Xaw`、`Motif` 等都提供了以某种方式类似于 `Gtk+` 容器控件的控件。

那么，究竟什么是容器控件呢？容器控件是管理其他控件的简单控件。窗口是容器的一个熟悉例子。窗口的目的是提供一个区域，将按钮、文本字段、单选按钮和标签等用户界面对象呈现给应用程序的用户。这种呈现是由容器控件执行的，有助于将一个控件类与其他控件类隔离开。容器控件有两个属性有助于定义它并与工具包中的其他容器控件隔离开。

第一个属性是可见性：容器对用户是否可见？窗口显然是对用户可见的。按钮也是如此，它们作为其标签的容器（按钮将在第 5 章“标签与按钮”中讨论）。但正如我们所看到的，许多容器对用户是不可见的，它们在后台工作，计算它们管理的子控件的布局，并响应应用程序窗口几何形状的变化，而窗口反过来又充当它们的容器。

第二个属性是容器的布局策略：容器如何在其内部放置其的子控件？某些容器（如 `GtkFixed` 或 `Motif` 的 `BulletinBoard`）让程序员预想控件的位置，并在编译时或在应用程序运行时通过表指定这些位置。一旦指定，这些控件的位置实际上是硬编码的，一旦应用程序对容器及其子控件进行了实例化并实现，这些位置就不会再发生变化。`Gtk+` 以及其他工具包中的大多数容器控件允许程序员指定容器与其包含的控件之间存在的抽象关系，或者让控件本身位于容器内，或者两者兼有。容器与控件之间可能存在的关系示例是：控件如何与容器的边缘相关。例如，作为控件，它们是从容器的左边缘还是右边缘（或者可能是从上到下或或下到上）添加的？是否有控件固定在容器的顶部边缘（左侧、右侧或底部，或者可能是四个角之一），并在容器调整大时保持该位置？

容器控件通常定义了容器子控件之间存在的相似关系。通常遇到的关系是容器内控件之间在垂直和水平方向上存在空间量。另一个属性“同质性”（homogeneity）决定了容器中的子控件是不同大小，还是具有相同的大小（通常是给一组设置的大小）。容器控件之所以有用，是因为它们允许程序员轻松构建用户界面，该界面不仅以一致的方式显示其组件，还能良好地响应用户引起的变化，特别是窗口大小。你越熟悉 `Gtk+` 提供的各种容器控件，就越可能明智地选择控件，并为你的用户提供一个设计良好且吸引人的界面，该界面在用户交互时将保持形状。

在本章以及接下来的章节中，我将介绍容器控件类并提供关于其用法的大量示例。你应该特别关注的两个控件类是立即介绍的 `GtkContainer`，以及在本章稍后描述的 `GtkBox` 及其子类 `GtkV` 和 `GtkH`。我相信，如果你计划编写最基本的 `Gtk+` 应用程序，对这些控件类的知识是必须。

# GtkContainer

- 类名：`GtkContainer`
- 父类名：`GtkWidget`

## 宏

- 控件类型宏：`GTK_TYPE_CONTAINER`
- 对象到控件转换宏：`GTK_CONTAINER (obj)`
- 控件类型检查宏：`GTK_IS_CONTAINER(obj)`

### 支持的信号

| 信号名称 | 触发信号的条件 |
|---|---|
| add | 子被添加到容器中。 |
| remove | 子从容器中移除。 |
| check_resize | 容器的 check resize 函数。 |
| focus | 容器（或子）获得了焦点。 |
| set_focus_child | 容器的焦点子被设置。 |

```c
void
add(GtkContainer *container, GtkWidget *widget, gpointer user_data);
void
remove(GtkContainer *container, GtkWidget *widget, gpointer user_data);
void
check_resize(GtkContainer *container, gpointer user_data);
GtkDirectionType
focus(GtkContainer *container, GtkDirectionType direction, gpointer user_data);
void
set_focus_child(GtkContainer *container, GtkWidget *widget, gpointer user_data);
```

### 支持的参数

前缀：`GtkContainer::`

表 10.2 GtkContainer 参数
| 名称 | 类型 | 权限 |
| --- | --- | --- |
| border_width | GTK_TYPE_ULONG | GTK_ARG_READWRITE |
| resize_mode | GTK_TYPE_RESIZE_MODE | GTK_ARG_READWRITE |
| child | GTK_TYPE_WIDGET | GTK_ARG_WRITABLE |

# 应用级 API 概览

在运行时返回常量 `GTK_TYPE_CONTAINER`：

```c
GtkType
gtk_container_get_type(void);
```

设置容器小部件的边框宽度（默认为 0）：

```c
向向容器添加子小部件：
```c
void
gtk_container_add(GtkContainer *container, GtkWidget *widget);
```

从容器中移除子小部件：

```c
void
gtk_container_remove(GtkContainer *container, GtkWidget *widget);
```

对容器中的每个子部件调用回调函数：

```c
void
gtk_container_foreach(GtkContainer *container, GtkCallback callback, gpointer callback_data);
```

获取每个子容器的列表（下一层）：

```c
GList *
gtk_container_children(GtkContainer *container);
```

根据指定的焦点方向将焦点设置到容器或其一个子部件：

```c
gint
gtk_container_focus(GtkContainer *container, GtkDirectionType direction);
```

### 类描述

`GtkContainer` 是 `Gtk+` 支持的一大类小部件类的父类，这些类设计用于管理窗口区域内其他小部件的布局。在 `Gtk+` 小部件层级结构中，许多小部件类继承自 `GtkContainer`，其中大多数将在本章中描述。

在你的应用程序中，你永远无法实际创建 `GtkContainer` 的实例；`GtkContainer` 实例的存在是因为你继承了自它的其他类。因此，没有 `gtk_container_new()` 供你调用。但是，`GtkContainer` API 中有几个函数你可能会发现很有用。特别是正如我们所看到的，`gtk_container_add()` 在你的应用程序中将被频繁使用。

为了获取 `GtkContainer` 类提供的通用概念，最好跳过本节。当你开发应用程序代码时，本章中描述的其他类对你来说更有用。

# 设置容器的边框宽度

让我们通过考虑容器的边框宽度来观察 `GtkContainer`。容器的边框宽度在 `Gtk+` 中默认为 0，它定义了除了容器布局子部件所需的空间外，容器上方下方提供的空间（像素为单位）。要设置容器小部件的边框宽度，你调用 `gtk_container_set_border_width()`。

```c
void
gtk_container_set_border_width(GtkContainer *container, guint border_width);
```

由于你无法直接从应用程序中创建 `GtkContainer` 实例，你要么在处理 `GtkWidget` 实例，要么在处理某些继承自 `GtkContainer` 的小部件（如 `GtkVBox`）。因此，你必须使用宏 `GTK_CONTAINER` 将 `gtk_container_set_border_width()` 的第一个参数转换为 `GtkContainer`，如例例所示：

```c
GtkWidget *widget;
...
gtk_container_set_border_width( GTK_CONTAINER( widget ), 0 );
```

`GtkContainer` API 定义的所有其他函数也需要相同的策略，因为它们都接受 `GtkContainer` 实例作为作为第一个参数。

# 添加和移除子部件

可以通过调用 `gtk_container_add()` 向大多数 `GtkContainer` 派生类添加子小部件：

```c
void
gtk_container_add(GtkContainer *container, GtkWidget *widget);
```

同样，可以通过调用 `gtk_container_remove()` 从 `GtkContainer` 派生类中移除之前添加的子小部件：

```c
void
gtk_container_remove(GtkContainer *container, GtkWidget *widget);
```

向容器添加和移除子部件通常会导致容器及其内容的重绘，以适应小部件子部件列表的变化。`GtkContainer` 实际上并没有提供 `gtk_container_add()` 或 `gtk_container_remove()` 的实现。这些函数是由继承自 `GtkContainer` 的类提供的。这些函数中的大多数都列在表 10.3 中。

# 表 10.3 添加和移除函数

| 类 | 添加函数 | 移除函数 |
| --- | --- | --- |
