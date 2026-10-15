
```c
GtkStyle *
gtk_ctree_node_get_row_style(GtkCTree *ctree, GtkCTreeNode *node);
```

参数标识树和行；返回值为 `Gtk+` 样式对象，如果未设置，则返回 `NULL`。

函数 `gtk_ctree_node_set_row_style()`：

```c
void
gtk_ctree_node_set_row_style(GtkCTree *ctree, GtkCTreeNode *node,
    GtkStyle *style);
```

可用于与行关联的样式对象（如果有）替换为您选择的样式对象。参数再次标识要附加样式的树和节点。参数 `style` 是将附加到指定节点上的样式对象。

以下代码片段从树中的节点读取样式对象，如果它存在则对其进行复制（如果不存在则创建一个新的），然后将字体更改为默认 `Gtk+` 类似的字体，但不加粗和斜体。它调用 `gtk_ctree_node_set_row_style()` 将新样式对象附加到获取原始样式对象的行上。

```c
GtkStyle *style, *new_style;
GdkFont *font;
```

```c
...
```

```c
// 向树中添加一个节点
text[0] = "Ralph", text[1] = "888"; text[2] = "666-444";
node = gtk_ctree_insert_node(GTK_CTREE(root), parent, NULL, text,
    5, NULL, NULL, NULL, FALSE, TRUE);
```

```c
// 读取样式对象 -- 这是 NULL，但接下来的
// 代码说明了如何处理 NULL 和非 NULL 返回值
```

```c
style = gtk_ctree_node_get_row_style(GTK_CTREE(root), node);
if ( style ) {
    new_style = gtk_style_copy( style ); // 复制读取到的
else
    new_style = gtk_style_new()); // 创建一个新的
```

```c
// 加载 Gtk+ 默认字体，但不加粗和斜体
font = gdk_font_load();
```

# "-adobe-helvetica-bold-o-normal--*-120--*-*-*-iso8859-1";

```c
// 如果上述加载成功，则更改字体
```

```c
if (font) {
    gdk_font_unref(new_style->font);
    new_style->font = font;
    gdk_font_ref(new_style->font);
}
```

```c
// 将样式对象附加到行
gtk_ctree_node_set_row_style(GTK_CTREE(root), node, new_style);
```

## 总结

一个部件与列表（`GtkList` 和 `GtkClip`）相似之处在于，它们都可以用于显示用户可以选择的一组项目。树比列表更强大，因为它们允许程序员对列表中无法组织的数据的数据，并且让您对任何时候显示的数据量有更多控制。在本章中，我们讨论了以下树相关的部件：`GtkTree`、`GtkTreeItem` 和 `GtkTree`。`GtkTree` 和 `GtkTreeItem` 一起用于显示包含理论上无限数量子树的树，树中的每个节点显示一个标签，或者如果应用程序偏好，管理任意类型的部件。（通常，这个部件是一个 box 部件，用于管理任意内容，如位映射图和标签部件；见图 12.10。）`GtkTree` 是一个更复杂的部件（其庞大的 API 表明），允许显示由多个列组成的树节点。`GtkTree` 显示树中每一列的可显示列标题，并支持键盘绑定，允许用户通过键盘输入折叠和展开行。然而，与在 `GtkTree` 部件中显示的树不同，树节点只能显示基于文本的数据。因此，如果应用程序必须在树中显示图像或其他任意数据，使用 `GtkTree` 和 `Gtk-TreeItem` 是唯一的选项。

## 第 13 章：范围部件和调整对象

在本章中，我将描述表 13.1 中列出的 `Gtk+` 范围部件。

**表 13.1** 本章中描述的部件

| 类名 | 描述 |
| --- | --- |
| `GtkRange` | 本章讨论的范围部件类的父类 |
| `GtkScale` | 刻度控件部件的父类 |
| `GtkHScale` | 水平刻度控件 |
| `GtkVScale` | 垂直刻度控件 |
| `GtkScrollbar` | 滚动条控件的父类 |
| `GtkHScrollbar` | 水平滚动条控件 |
| `GtkVScroll` | 垂直滚动条控件 |
| `GtkAdjustment` | 调整对象 |

作为一名应用程序开发者，你只会实例化属于以下部件类的类：`GtkScale`、`GtkVScale`、`GtkScrollbar` 或 `GtkVScroll`。其他类（`GtkRange`、`GtkScale` 和 `GtkScrollbar`）是基类，它们包含了你在处理 `GtkScale`、`GtkVScale`、`GtkHScrollbar` 或 `GtkVScroll` 时可能会觉得有用的功能，但你永远不会在应用程序中实际创建这些类的实例。

本章包含了对 `Gtk+` 调整对象（`GtkAdjustment`）的讨论。调整对象是我们在本章中查看的部件类实现其功能的基础。若干 `Gtk+` 部件类（包括 `GtkScrolledWindow`、`GtkListBox`、`GtkLayout` 和 `GtkProgress`）创建范围部件（刻度和滚动条）或调整对象的实例，其中某些类允许你在创建部件时指定一个调整对象，以覆盖该部件通常为自己创建的调整对象。

## 刻度部件

刻度部件为用户提供了一种方便的方法来选择落在预定义范围内的值。图 13.1 展示了 `Gtk+` 支持的两种类型的刻度部件：水平和垂直。刻度部件的水平或垂直区域代表了用户可以选择的完整值范围。在该区域内，一个移动的“滑块”（thumb）指示刻度部件的当前值，并可以使用键盘或鼠标进行定位，以更改刻度部件的值。应用程序可以安排在刻度部件的值发生变化时发出通知。如果应用程序需要对用户选择的值做出实时响应，这种策略效果非常好。应用程序也可以在对它最方便的时候查询刻度部件的值，例如，当用户点击显示刻度部件的对话框中的“确定”按钮时，表示他们选择的值应该被读取和保存。

图 13.1 水平和垂直刻度部件

刻度部件在刻度控件相邻处显示一个标签，用以描述或指示刻度部件的当前值。刻度部件的默认行为是显示此标签，但 `GtkScale` 允许你在需要时隐藏标签。你还可以指定标签相对于刻度控件的位置。

我对比 `GtkScale` 的介绍组织如下：首先，我将描述派生自 `GtkScale` 的两个类：`GtkAutoScale` 和 `GtkVerticalScale`。这两个类是你将直接实例化的类，而一旦我描述了这这两个类，我将详细描述它们的父类 `GtkScale`。然后，我将结合一个示例应用程序统一介绍这些内容，说明如何响应用户对刻度值产生的变化，以及如何在离散的时间点提取刻度部件的值（例如，当用户关闭了包含刻度控件的对话框时）。

## GtkHScale

### 类名

`GtkHScale`

### 父类名

`GtkScale`

## 宏

- 部件类型宏：`GTK_TYPE_HSCALE`
- 对象到部件的转换宏：`GTK_HSCALE(obj)`
- 部件类型检查宏：`GTK_IS_HSCALE(obj)`

### 支持的参数

前缀：`GtkHScale::`

表 13.2 `GtkHScale` 参数

| 名称 | 类型 | 权限 |
|--- |--- |--- |
| adjustment | `GTK_TYPE_ADJUSTMENT` | `GTK_ARG_READWRITE` | `GTK_ARG_CONSTRUCT` |

## 应用程序级 API 摘要

在运行时返回常量 `GTK_TYPE_HSCALE`：

```c
GtkType
gtk_hscale_get_type(void)
```

创建一个 `GtkHScale` 的新实例：

```c
GtkWidget *
gtk_hscale_new(GtkAdjustment *adjustment)
```

### 类描述

`GtkHScale` 是一个非常简单的类。对于大多数应用程序，唯一感兴趣的是用于创建 `GtkHScale` 实例的 `gtk_hscale_new()`：

```c
+ GtkWidget *
  gtk_hscale_new(GtkAdjustment *adjustment)
```

参数 `adjustment` 指定了一个应用程序定义的调整对象。为了让水平刻度部件正常工作，你必须创建自己的调整对象，或者通过其他部件提供一个。我将在本章稍后部分描述调整对象（参见 `GtkAdjustment`）。

以下代码创建了一个水平滚动条，允许用户在 0.0 到 99.0 的范围内选择值：

```c
GtkAdjustment *adjustment;
GtkWidget *scale;

adjustment = gtk_adjustment_new(0.0, 0.0, 99.0, 1.0, 0.0);
scale = gtk_hscale_new(adjustment);
```

## GtkVScale

### 类名

`GtkVScale`

### 父类名

`GtkScale`

## 宏

- 部件类型宏：`GTK_TYPE_VSCALE`
- 对象到部件的转换宏：`GTK_VSCALE(obj)`
- 部件类型检查宏：`GTK_IS_VSCALE(obj)`

### 支持的参数

前缀：`GtkVScale::`

表 13.3 `GtkVScale` 参数

| 名称 | 类型 | 权限 |
|--- |--- |--- |
| adjustment | `GTK_TYPE_ADJUSTMENT` | `GTK_ARG_READWRITE` | `GTK_ARG_CONSTRUCT` |

## 应用程序级 API 摘要

在运行时返回常量 `GTK_TYPE_VSCALE`：

```c
GtkType
gtk_vscale_get_type(void)
```

创建一个 `GtkVScale` 的新实例：

```c
GtkWidget *
gtk_vscale_new(GtkAdjustment *adjustment)
```

### 类描述

`GtkVScale` 是一个非常简单的类。对于大多数应用程序，唯一感兴趣的是用于创建 `GtkVScale` 实例的 `gtk_vscale_new()`：

```c
+ GtkWidget *
  gtk_vscale_new(GtkAdjustment *adjustment)
```

参数 `adjustment` 指定了一个应用程序定义的调整对象。为了让垂直刻度部件正常工作，你必须创建自己的调整对象，或者通过其他部件提供一个。我将在本章稍后部分描述调整对象。

## GScale

### 类名

`GScale`

### 父类

`Range`

## 宏

- 部件类型宏：`GTK_TYPE_SCALE`
- 对象到部件的转换宏：`GTK_SCALE(obj)`
- 部件类型检查宏：`GTK_IS_SCALE(obj)`

### 支持的参数

前缀：`GScale::`

表 13.4 `GScale` 参数

| 名称 | 类型 | 权限 |
|--- |--- |--- |
| digits | `GTK_INT` | `GTK_ARG_READWRITE` |
| draw_value | `GTK_BOOL` | `GTK_ARG_READWRITE` |
| value_pos | `GTK_POSITION` | `GTK_ARG_READWRITE` |

## 应用程序级 API 摘要

在运行时返回常量 `GTK_TYPE_SCALE`：

```c
GtkType
gtk_scale_get_type(void)
```

设置刻度显示的有效位数：

```c
void
gtk_scale_set_digits(GScale *scale, int digits)
```

显示或隐藏刻度值：

```c
void
gtk_scale_draw_value(GScale *scale, gboolean draw_value)
```

设置值标签的位置的位置：

```c
void
gtk_scale_set_value_pos(GScale *scale, GtkType pos)
```

### 应用程序级 API 摘要（继续）

获取刻度值的宽度（像素为单位）：

```c
gint
gtk_scale_get_value_width (GScale *scale)
```

重新绘制刻度值：

```c
void
gtk_scale_draw_value (GScale *scale)
```

### 类描述

`GScale` 是 `GtkHScale` 和 `GAutoScale` 的父类。因此，它提供了对实例化 `GtkHScale` 或 `GtkVScale` 的程序员感兴趣的接口。

设置有效位数

在这里描述的第一个函数是 `gtk_scale_set_digits()`：

```c
void
gtk_scale_set_digits (GScale *scale, int digits);
```

此函数允许应用程序控制刻度标签（显示时）的有效位数。通常情况下，显示的有效位数为 1（所有基于调整对象的部件如此）。将 `digits` 设置为 0 将导致值以整数形式显示。

显示和隐藏刻度值

默认情况下，刻度部件将以标签形式显示值。你可以通过调用 `gtk_scale_draw_value()` 来显示或隐藏此标签：

```c
void
gtk_scale_draw_value (GScale *scale, gboolean draw_value)
```

参数是 `GScale` 的实例（`GtkHScale` 或 `GtkVScale`），参数 `draw_value` 是一个控制刻度标签显示的布尔值。如果 `draw_value` 设置为 `TRUE`，则会被绘制；如果设置为 `FALSE`，标签将被隐藏。

设置值标签的位置

默认情况下，水平和垂直刻度部件都将其标签显示在刻度控件的上方。你可以通过调用 `gtk_scale_set_value_pos()` 来更改默认位置。

```c
void
gtk_scale_set_value_pos(GtkScale *scale, GtkPositionType pos)
```

参数 `pos` 可以是表 13.5 所示的列值之一。

## 表 13.5 GtkPositionType 值

| Value | 含义 |
| --- | --- |
| `GTK_POS_LEFT` | 值显示在控件的左侧。 |
| `GTK_POS_RIGHT` | 值显示在控件的右侧。 |
| `GTK_POS_TOP` | 值显示在控件上方（默认值）。 |
| `GTK_POS_BOTTOM` | 值显示在控件下方。 |

## 其它滑块小部件函数

有两个可能很少使用的函数，允许您获取滑块文本的宽度（`gtk_scale_get_value_width()`）并让滑块控件重绘其值（`gtk_scale_draw_value()`）。这些函数的原型如下：

```c
gint
gtk_scale_get_value_width(GtkScale *scale)
```

```c
void
gtk_scale_draw_value(GtkScale *scale)
```

这两个函数都接受一个 `GtkScale` 实例作为其唯一参数。`gtk_scale_get_value_width()` 函数返回滑块小部件正在（或将要）显示的文本宽度，单位为像素。

### 示例

现在来看示例程序。该示例程序创建了一个 `GtkScale` 实例，将滑块值放置在滑动条的左侧。还创建并显示了一个 `GtkScale` 实例在水平滑块旁边。它的标签绘制在默认位置。这两个滑块均可由用户独立且相互影响地设置为 `[0, 100]` 范围内的值。水平滑块小部件标签显示的有效数字设置为 0。垂直滑块小部件显示其当前值，位数为 1 个有效数字。

当用户更改滑块的位置时，每个滑块小部件都会显示其当前值。这是通过在应用程序为每个创建的调整对象注册的 _changed 信号函数_ 内部将滑块的值打印到 `stderr` 实现的。这说明了应用程序如何监控滑块值的实时变化。滑块小部件下方还显示了一个确定按钮（`GButton`）。按下此按钮会调用点击信号函数；该点击信号函数查询每个调整对象的当前值，并同样显示从 `stderr` 获取的值。这说明了应用程序如何在特定时间点获取滑块的值。我将在本章稍后部分更详细地描述调整对象的用法（你可以在查看我即将展示的源代码之前，直接跳过去阅读关于调整对象的介绍）。这里展示的示例虽然简单，但它确实说明了在应用程序中使用滑块小部件时需要知道的大部分内容。

## 列表 13.1 小部件示例
