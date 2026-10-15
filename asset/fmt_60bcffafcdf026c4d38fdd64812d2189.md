
该参数标识 `GTree` 实例，并指定节点或行。参数 `column` 范围在 `[1, n]` 之间，其中 `n` 是树的列数，指定要滚动到的列。参数 `row_align` 和 `col_align` 均为 `float` 类型，它们描述了如何放置被放入视图的数据（参见第 6 章中 `gtk_clist_moveto()` 的描述）。

## 总结

小部件（`widget`）与列表（`GtkList` 和 `GtkClientSize`）类似，因为它们都可以用于显示一组可以由用户选择的项目。这些小部件比列表更强大，因为它们赋予程序员在列表不允许的列表结构中组织数据的能力，并让用户对在任何时间显示的数据量有更强的控制力。在本章中，我们讨论了以下与树相关的小部件：`GtkTree`、`GtkTreeItem` 和 `GtkTreeView`。`GtkTree` 和 `GtkTreeItem` 结合使用，显示包含（理论上）无限数量子集的树，每个节点显示一个标签，或者如果应用程序有需要，则管理任意类型。（通常，此小部件将是一个增长的框，用于管理任意内容，如 `pixmap` 和标签小部件；参见图 12.10。）`GtkTree` 是一个复杂的节点（如其相当大的 API 所示），它允许显示由多个列组成的树节点。`ctree` 显示树中每一列的列标题，并支持键盘绑定，允许用户通过键盘输入折叠和展开行。然而，与在 `GtkTree` 小部件中显示的树不同，树节点只能显示基于文本的数据。因此，如果你的应用程序必须在树中显示图像或其他任意数据，使用 `GtkTree` 和 `GtkTreeView` 是唯一的选择。

# 第 13 章

# 范围小部件与调整对象

在本章中，我将描述表 13.1 中列出的 `Gtk+` 范围小部件。

表 13.1 本章描述的小部件
| 类名 | 描述 |
| --- | --- |
| `GtkRange` | 本章讨论的范围小部件类的父类 |
| `GtkScale` | 缩放小部件父类 |
| `GtkAutoScale` | 水平缩放小部件 |
| `GtkVScale` | 垂直缩放小部件 |
| `GtkScrollbar` | 滚动条小部件父类 |
| `GtkHscrollbar` | 水平滚动条小部件 |
| `GtkVScroll` | 垂直滚动条小部件 |
| `GtkAdjustment` | 调整对象 |

作为应用程序开发者，你只会实例化属于以下小部件类的小部件：`GtkAutoScale`、`GtkVScale`、`GtkHscrollbar`、`GtkVScroll`。其他类（`GtkRange`、`GtkScale` 和 `GtkScrollbar`）是基类，包含了你在处理 `GtkAutoScale`、`GtkVScale`、`GtkHscrollbar` 或 `GtkVScroll` 时可能会发现有用的功能，但你永远不会在应用程序中实际创建这些类的实例。

本章包含了对 `Gtk+` 调整对象（`GtkAdjustment`）的讨论。调整对象是我们章节中所查看的小部件类实现其功能的基础。若干 `Gtk+` 小部件类包括 `GtkScrolledWindow`、`GtkList`、`GtkLayerout` 和 `GtkProgress` 会创建范围小部件（缩放和滚动条）或调整对象，其中某些类允许你在创建小部件时指定一个调整对象，以覆盖小部件通常为其创建的调整对象。

# 缩放小部件 (Scale Widgets)

缩放小部件为用户提供了一种方便的方法来选择预定义范围内的值。图 13.1 展示了 `Gtk+` 支持的两种缩放小部件：水平和垂直。缩放小部件的水平或垂直区域代表了用户可以选择的全值范围。在该区域内，一个可移动的“滑块”（thumb）指示缩放小部件的当前值，可以使用键盘或鼠标进行定位以更改缩放小部件的值。应用程序可以配置为每当缩放小部件的值变化时发出通知。如果应用程序需要对用户选择的值做出实时响应，这种策略效果良好。应用程序也可以在对它最方便的时间查询缩放小部件的值，例如，当用户点击显示缩放小部件的对话框中的 OK 按钮时，表示应该读取并保存其所选择的值。

![](img/1441ee0eb9a357efc9aff107f92bf0c0_698_0.png)

图 13.1 水平与垂直缩放小部件

缩放小部件在控件旁边显示一个标签，指示缩放小部件的当前值。缩放小部件的默认行为是显示此标签，但 `GtkScale` 允许隐藏它。你还可以指定标签相对于控件的位置。

`GtkScale` 的呈现方式如下。首先我将描述派自 `GtkScale` 的两个类：`GtkScale` 和 `GtkAutoScale`。这些是你直接实例化的类。然后我将详细描述它们的父类 `GtkScale`。我将通过示例应用程序说明如何响应用户对值的变化，以及如何在特定时间（例如，当用户关闭包含缩放小部件的对话框时）提取缩放小部件的值。

# GtkScale

## 类名

`GtkScale`

## 父类名

`GtkScale`

## 宏

类型宏：`GTK_TYPE_HSCALE`

对象到小部件的转换宏：`HSCALE(obj)`

类型检查宏：`GTK_IS_HSCALE(obj)`

## 支持的参数

前缀：`GtkScale::`

表 13.2 `GtkScale` 参数

| 名称 | 类型 | 权限 |
|---|---|---|
| `adjustment` | `GTK_TYPE_ADJUSTMENT` | `GTK_ARG_READWRITE` | `GTK_ARG_CONSTRUCT` |

# 应用程序 API 摘要

运行时返回常量 `GTK_TYPE_HSCALE`：
`GtkType`
`gtk_scale_get_type(void)`

+   创建一个 `GtkScale` 实例：
- `GtkWidget *gtk_hscale_new (GtkAdjustment *adjustment)`

## 类描述

`GtkScale` 是一个非常简单的类。对于大多数应用程序来说，感兴趣的函数是创建 `GtkScale` 实例的 `gtk_hscale()`：

```c
GtkWidget *
gtk_hscale_new(GtkAdjustment *adjustment)
```

参数 `adjustment` 指定了一个应用程序定义的调整对象。你必须创建一个调整对象，或者提供一个由其他小部件创建的对象，以便水平缩放小部件正常工作。我将在本章后续介绍调整对象（参见 `GtkAdjustment`）。

以下代码段创建一个允许用户在 0.0 到 99.0 范围内选择值的水平滚动条：

```c
GtkAdjustment *adjustment;
GtkWidget *scale;
adjustment = gtk_adjustment_new(0.0, 0.0, 100.0, 0.1, 1.0, 1.0);
scale = gtk_hscale_new(GTK_ADJUSTMENT (adjustment));
```

# GtkVScale

## 类名

`GtkScale`

## 父类名

`GtkScale`

## 宏

类型宏：`GTK_TYPE_VSC`

对象到小部件的转换宏：`VSALE(obj)`

类型检查宏：`GTK_IS_VSCALE (obj)`

## 支持的参数

前缀：`GtkVScale ::`

表 13.3 `GtkVScale` 参数
| 名称 | 类型 | 权限 |
|---|---|---|
| `adjustment` | `GTK_TYPE_ADJUSTMENT` | `GTK_ARG_READWRITE` | `GTK_ARG_CONSTRUCT` |

## 应用程序级 API 摘要

在运行时返回常量 `GTK_TYPE_VScale`：
```c
GtkType
gtk_vcale_get_type(void)
```

创建一个新的 `GtkVScale` 实例：
```c
GtkWidget *
gtk_vcale_new (GtkAdjustment *adjustment)
```

## 类描述

`GtkVScale` 与之前描述的 `GtkHScale` 几乎相同，不同在于由 `GtkVScale` 创建的控件是垂直绘制的，而 `GtkHScale` 是水平绘制的。要创建一个新的 `GtkVScale` 实例，可以调用 `gtk_hscale_new()`：

```c
GtkWidget *
gtk_hscale_new (GtkAdjustment *adjustment)
```
