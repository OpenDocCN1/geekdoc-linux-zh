
```
typedef struct _GtkWindow GtkWindow;
struct _GtkWindow
{
  GtkBin bin;
  gchar *title;
  gchar *wmclass_name;
  gchar *wmclass_class;
  GtkWindowType type;
  GtkWidget *focus_widget;
  GtkWidget *default_widget;
  GtkWindow *transient_parent;
  gushort resize_count;
  guint allow_shrink : 1;
  guint allow_grow : 1;
  guint auto_shrink : 1;
  guint handling_resize : 1;
  guint position : 2;
};
```

> / 当窗口被映射时，以下标志位初始为 TRUE。
> * 并且在首次进行定位后将设置为 FALSE。
> * 当窗口大小发生变化时，该位也会被临时重置。
> * 当为 TRUE 时，我们将窗口移动到应用程序设置的位置：

```
guint use_position : 1;
guint modal : 1;
```

![](img/7fa9959a9d28ad339fa75e44952feeb9_854_0.png)

# GTK+ 版权

```
/* GTK - The GIMP Toolkit
* Copyright (C) 1995-1997 Peter Mattis, Spencer Kimball, Josh MacDonald
* 此库是免费软件；你可以重新分发它，或者
* 根据自由软件基金发布的 GNU 库通用公共
* 许可证条款对其进行修改；或者遵循
* 该许可证的第 2 版本或（根据你的选择）任何更高版本。
*/
* 分发此库的希望是它有用，
* 但不提供任何保证；甚至没有关于
* 商业性或适用于特定用途的隐式保证。详情请参阅 GNU
* 库通用公共许可证。
*/
* 你应该在收到此库的同时收到一份 GNU 库通用
* 许可证的副本；如果没有，请信寄至
* Free Software Foundation, Inc., 59 Temple Place - Suite 330,
* Boston, MA 02111-1307, USA.
*/
* 由 GTK+ 团队及其他于 1997-1999 年修改。请查看 AUTHORS
* 文件获取 GTK+ 团队人员列表。查看 ChangeLog
* 文件获取更改列表。这些文件随 GTK+ 发布
* 地址为 http://ftp.gtk.org/pub/gtk/。
*/
```

# 附录 F

## 给 Motif 和 Xt 程序员的说明

本附录旨在为具有 Motif 和/或 Xt 编程经验的程序员，通过解释差异来帮助其从 Motif（或其他某些基于 Xt 的工具包）过渡到 GTK+。这并不是在讨论两者之间的优劣。程序员有自己的个人偏好，并且经常直言不讳地表达这些偏好。本附录仅旨在解释 GTK+ 编程模型与 Motif 和 Xt 中模型之间的基本区别。

## 通用信息

你在 GTK+ 和 Motif/Xt 之间注意到的第一个区别是函数命名的变化。首先，GTK+ 不使用大写字母；全部使用小写并用下划线字符 (`_`) 分隔。其次，GTK+ 遵循对象/方法风格的函数命名，而不是使用 `XCreateMenuBar`（或 `XtManagedWidget()`），你应该使用 `gtk_menu_bar_new()`。

> 注意

菜单栏是一个独立的控件类，即 `GtkMenuBar`，而不是一个设置了某些资源的行列控件。此外，GTK+ 有垂直框控件（`GtkVBox`）或水平框控件（`GtkHBox`），而不是一个可以兼顾两者的 `XmRowColumn`。`GtkBox` 和 `GtkVBox` 是更通用 `GtkBox` 的子类，后者并未实例化。GTK+ 控件具有与行列控件某种相似的功能。此外，菜单控件是 `GtkMenu`，这又是一个不同的控件类。

GTK+ 的初始化过程与 Motif/Xt 略有不同。例如，你不需要在 GTK+ 中指定应用程序上下文。此外，不支持多显示器。而且，资源的概念在 GTK+ 中是不同的，特别是在用户可配置选项方面。在 GTK+ 中，用户可以修改颜色、字体，并且背景位图可以绑定在主题中，这会对基本外观和感觉产生复杂的变化。功能不受影响。键盘绑定也可以放置在资源文件中。但，仅此而已。你无法获得在 Motif/Xt 资源文件中可以为单个控件指定的、那样的所有可自定义资源。在 GTK+ 中，此类单个控件资源（如 `xmLabelString`）是从资源文件进行用户控制的。此外，GTK+ 资源文件不支持颜色名称（如 `red`、`blue`、`PapayaWhip`），尽管在 GTK+ 应用程序内部可以访问颜色名称。

# GTK+ 控件

GTK+ 控件集的视觉外观与 Motif 相似。图 F.1 显示了一个带有“文件”和“帮助”以及绘图区域的标准用户界面。

图 F.1:![](img/7fa9959a9d28ad339fa75e44952feeb9_854_0.png)

Listing F.1 显示了创建此界面的程序。由于控件名称在资源文件中是小写的，所以你不需要做任何。给 Motif 和 Xt 程序员的说明

LISTING F.1 用户界面![](img/7fa9959a9d28ad339fa75e44952feeb9_858_0.png)
