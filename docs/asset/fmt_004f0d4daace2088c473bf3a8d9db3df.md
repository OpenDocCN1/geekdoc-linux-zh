
我们使用 `GtkTreeView` 作为 CD 应用程序的核心，当我们查询 CD 数据库时，将修改 `GtkTreeView` 的内容。

我们已经完成了对 `GTK+` 的之旅，现在我们将把注意力转向故事的另一部分：`GNOME`。我们将看到如何使用 `GNOME` 库为我们的应用程序添加菜单，以及 `GNOME` 控件如何让为 `GNOME` 桌面进行编程变得更加简单。

# GNOME 控件

`GTK+` 的设计是与桌面无关的；也就是说，`GTK+` 不会假设自己运行在 `GNOME` 中，甚至不假设运行在 `Linux` 上。这背后的原因是 `GTK+` 可以相对容易地移植到 `Windows` 或任何其他窗口系统。其结果是 `GTK+` 缺乏将程序与桌面绑定的手段，例如用于保存程序配置、帮助文件或编写小部件（`applets` 是运行在边缘面板上的微型工具）。

`GNOME` 库包含了 `GNOME` 控件，这些控件扩展了 `GTK+` 并用更易于使用的控件替换了 `GTK+` 的部分。在本节中，我们将查看如何使用 `GNOME` 控件进行编程。

在使用 `GNOME` 库之前，我们必须在程序开始时以与处理 `GTK+` 相同的方式初始化它们。我们像对纯 `GTK+` 程序调用 `gtk_init` 一样调用 `gnome_program_init`。

该函数接受 `app_id` 和 `app_version` 用于向 `GNOME` 描述我们的程序，一个 `module_info` 告诉 `GNOME` 初始化哪个库模块，命令行参数，以及设置以 `NULL` 结尾的名称/值对列表的应用程序属性。

```c
GnomeProgram* gnome_program_init (const char *app_id, const char *app_version,
                               const GnomeModuleInfo *module_info,
                               int argc, char **argv,
                               const char **first_property_name,
                               ......);
```

可选属性列表允许我们设置诸如查找位图图形的目录。

# 使用 GTK+ 为 GNOME 编程

# 尝试一下——一个 GNOME 窗口

现在让我们来看一个 `GNOME` 程序，通过查看 `GNOME` 对 `GtkWindow` 的替换品 `GnomeApp` 控件。

输入此程序并将其命名为 `gnome1.c`：

```c
#include <gnome.h>

int main (int argc, char *argv[])
{
  GtkWidget *app;
  gnome_program_init ("gnome", "1.0", MODULE, argc, NULL);
  app = gnome_app_new ("gnome", "The Window Title");
  gtk_widget_show(app);
  gtk_main (0);
  return 0;
}
```

要编译，我们需要 `GNOME` 头文件，因此我们将 `libgnui` 和 `libgnome` 传递给 `pkg-config`：

```bash
$ gcc gnome.c -o gnome `pkg-config --cflags --libs libgnome-2.0`
```

`GnomeApp` 扩展了 `GtkWindow`，并易于添加菜单、工具栏和底部的状态栏。由于它继承自 `GtkWindow`，我们可以使用 `GnomeApp` 控件使用任何 `GtkWindow` 函数。现在我们将查看菜单，并在我们的示例中添加状态栏。

你可以使用 `GTK+` 创建菜单，但 `GNOME` 提供了有用的结构和宏让工作变得更容易。在线 `GTK+` 文描述了如何在 `GTK+` 中创建菜单。

# GNOME 菜单

在 `GNOME` 中创建下拉菜单非常简单。菜单栏中的每个菜单由 `GnomeInfo` 结构体数组表示，数组中的每个元素对应一个菜单项。例如，如果我们有文件、编辑和视图菜单，会有三个数组。一旦创建了每个菜单，我们通过引用 `GnomeInfo` 结构体数组创建菜单栏。

`GnomeInfo` 结构体有点复杂，需要解释：

```c
typedef struct {
  GnomeUIType type;
  gchar *label;
  gchar *hint;
  gpointer moreinfo;
  gpointer user_data;
  gpointer unused_data;
  GnomePixmapType pixmap_type;
  gpointer pixmap_info;
  guint accelerator_key;
  GdkModifierType ac_mods;
  GtkWidget *widget;
} GnomeInfo;
```

结构中的第一个项定义了后续菜单元素的类型。可以是 `GNOME` 定义的 `GnomeUIType` 之一：

| GnomeUIType | 描述 |
| :--- | :--- |
| `GNOME_APP_UI_ENDOFINFO` | 表示这是数组中的最后一项。 |
| `GNOME_APP_UI_ITEM` | `GNOME_APP_UI_RADIOITEMS` 之前的普通项。 |
| `GNOME_APP_UI_TOGGLEITEM` | 切换按钮或复选框项。 |
| `GNOME_APP_UI_RADIOITEMS` | 单选按钮组。 |
| `GNOME_APP_UI_SUBTREE` | 表示子菜单。指向子菜单数组的 info。 |
| `GNOME_APP_UI_SEPARATOR` | 在菜单中插入分隔线。 |
| `GNOME_APP_UI_HELP` | 在菜单中创建帮助主题。 |
| `GNOME_APP_UI_BUILDER_DATA` | 指定后续条目的数据。 |
| `GNOME_APP_UI_CONFIGABLE` | 可配置的菜单项。 |
| `GNOME_APP_UI_SUBTREE_STOCK` | 与 `GNOME_APP_UI_SUBTREE` 相同，但标签应该在 `gnome-libs` 中查找。 |
| `GNOME_APP_UI_INCLUDE` | 与 `GNOME_APP_UI_SUBTREE` 相同，但项包含在当前菜单作为子菜单。 |

结构的第二个和第三个成员定义了菜单项的文本和弹出提示（提示显示在窗口底部的状态栏中）。

`moreinfo` 的用途取决于类型。对于 `ITEM` 和 `TOGGLEITEM`，它指向菜单项激活时调用的回调函数。对于 `RADIOITEMS`，它指向一组单选按钮的 `GnomeInfo` 数组。`user_data` 是传递给回调函数的任意指针。`pixmap_type` 和 `pixmap_info` 允许我们为菜单项添加位图图标，`accelerator_key` 和 `ac_mods` 帮助我们定义快捷键。最后，`widget` 用于菜单函数内部持有菜单项指针。

# 尝试一下——GNOME 菜单

用这个短程序尝试菜单。将其命名为 `menu.c`。

```c
#include <gnome.h>

void closeApp (GtkWidget *window, gpointer data)
{
    gtk_main_quit();
}
```

1. 我们为菜单项 `item_clicked` 定义一个回调函数：

```c
void item_clicked(GtkWidget *widget, gpointer user_data)
{
    printf("Item Clicked!\n");
}
```

2. 接下来是我们的菜单定义。我们有一个子菜单、顶层菜单和一个菜单数组。

```c
static GnomeUIInfo submenu[] = {
    (GNOME_APP_UI_ITEM, "SubMenu", "Menu Hint",
    GTK_SIGNAL_FUNC(item_clicked), NULL, NULL, 0, NULL, 0, NULL),
    (GNOME_APP_UI_ENDOFINFO, NULL, NULL, NULL, NULL, NULL, 0, 0, 0, NULL)
};

static GnomeUIInfo menu[] = {
    (GNOME_APP_UI_ITEM, "Menu 1", "Menu Hint",
    NULL, NULL, 0, 0, NULL,
    (GNOME_APP_UI_SUBTREE, "Menu Item 2", "Menu Hint", submenu,
    NULL, NULL, 0, 0, NULL,
    (GNOME_APP_UI_ENDOFINFO, NULL, NULL, NULL, NULL, NULL, 0, 0, 0, NULL)
};
```
