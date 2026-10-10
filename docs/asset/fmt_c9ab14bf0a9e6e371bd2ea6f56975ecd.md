
`adj1 = gtk_adjustment_new(0.0, 0.0, 100.0, 1.0, 5.0, 0.0);`

`gtk_signal_connect(GTK_OBJECT(adj1), "value_changed", GTK_SIGNAL_FUNC(AdjustmentChanged), NULL);`

// 创建水平刻度。将值显示在刻度的
// 左侧，并将刻度值显示为整数

`hscale = gtk_hscale_new(GTK_ADJUSTMENT(adj1));`

`gtk_scale_set_value_pos(GTK_SCALE(hscale), GTK_POS_LEFT);`

`gtk_scale_set_digits(GTK_SCALE(hscale), 0);`

`gtk_box_pack_start(GTK_BOX(hbox), hscale, TRUE, TRUE, 0);`

// 为第二个控件创建一个调整对象

`adj2 = gtk_adjustment_new(0.0, 0.0, 100.0, 1.0, 5.0, 0.0);`

`gtk_signal_connect(GTK_OBJECT(adj2), "value_changed", GTK_SIGNAL_FUNC(Adjustment2Changed), NULL);`

// 使用控件提供的默认值创建一个垂直刻度

`vscale = gtk_vscale_new(GTK_ADJUSTMENT(adj2));`

`gtk_box_pack_start(GTK_BOX(hbox), vscale, TRUE, TRUE, 0);`

`return 0;`

}

# GtkScale

```c
adjustments.adj1 = GTK_ADJUSTMENT(adj1);
adjustments.adj2 = GTK_ADJUSTMENT(adj2);
button = gtk_button_new_with_label( "Ok" );
gtk_signal_connect(GTK_OBJECT(button), "clicked", (GtkSignalFunc) HandleOkButton, &adjustments);
gtk_pack_end(GTK_BOX ( vbox ), button, FALSE, FALSE, 0 );
gtk_widget_show_all(GTK_WIDGET ( window )
ggtk_main();
}
```

上述代码中最需要注意的一点可能是对调整对象（adjustment objects）的使用。显然，是调整对象用于指定滑块控件（scale widget）所代表的范围；这可以从第 065 行和 080 行看出（它们创建了调整对象并设置了它们的范围），也可以从第 072 行和 086 行看出（它们将调整对象与使用它们的滑块控件关联）。同样显然，调整对象维护了由用户更改的滑块值。这通过 `value_changed` 信号函数得以证明，该函数读取调整对象的当前值来确定滑块控件当前显示的值；同时也通过 OK 按钮的点击信号函数证明，因为它实际上也执行了相同的操作。例如，将第 086 行修改如下：

```c
vscale = gtk_vscale_new ( GTK_ADJUSTMENT(adj1) );
```

即将 "`adj2`" 改为 "`adj1`" 并重新执行程序。这种更改的结果是什么？请务必阅读本章稍后介绍的调整对象章节，以了解调整对象如何以这种方式在多个控件之间共享的细节。滑块控件与调整对象的关系对于所有派自 `GtkRange` 的控件都是相同的。（目前，其他唯一派自 `GtkRange` 的控件类是））

# 滚动条 (Scrollbars)

我在本节中将讨论的 Gtk+ 类（`GtkScrollbar`、`GtkVScrollBar` 和 `GtkScrollBar`）构成了派自 `GtkRange` 的 Gtk 类集合。滚动条大部分由控件开发者使用，而不是应用程序开发者使用。应用程序通常应该 get 使用诸如 `GtkScrolledWindow` 的控件来包含需要滚动的父级内容。如果你正在设计一个支持滚动的控件，这同样适用。`GtkText` 使用 `GtkScrolledWindow` 而不是它自己的类来实现滚动功能。事实证明，只有 `GtkMain` 和 `GtkScrolledWindow` 是会实例化其自身滚动条的 Gtk+ 类（截至 Gtk 1.2.7）。

在许多方面，滚动条与滑块控件（在前节中已描述）相似。两者都可以用于控制 `GtkAdjustment` 对象的值，并且都可以由用户操作以在范围内选择一个值。然而，你始终应该使用 `GtkScale` 或 `GtkVScale` 来创建这种类型的控制控件；如果你的用户界面中存在滚动条，它们应该由 `GtkScrollWindow` 或或其他控件类创建，而不是直接由你的应用程序创建。此举的原因是，用户期望使用滑块控件来选择范围内的值，而滚动条则预期用于控制对应用程序管理的大型虚拟数据集（文档或图像）的视图，而这类工作最适合由滚动窗口控件等容器控件来处理。接下来的几页将详细介绍 `GtkScroll` 相关类。

# GtkHScrollBar

## 类名

`GtkHScrollBar`

## 父类名

`GtkScrollBar`

## 宏

控件类型宏：`GTK_TYPE_HSCROLLBAR`

对象到控件转换宏：`GTK_HSCROLLBAR(obj)`

控件类型检查宏：`GTK_IS_HSCROLLBAR(obj)`

## 应用程序级 API 摘要

在运行时返回常量 `GTK_TYPE_HSCROLLBAR`：

```c
GtkType
gtk_hscrollbar_get_type(void)
```

创建一个带有可选调整对象的 `GtkHScrollBar` 新实例：

```c
GtkWidget *
gtk_hscrollbar_new(GtkAdjustment *adjustment)
```

# GtkVScroll

## 类描述

`GtkHScroll` 是一个简单的类，提供了一个函数 `gtk_hscrollbar_new()`，该函数可用于创建一个水平滚动条：

```c
GtkWidget *
gtk_hscrollbar_new(GtkAdjustment *adjustment)
```

`gtk_hscrollbar_new()` 的参数是一个 `GtkAdjustment` 对象。它可以是任何调整对象，可以是专门为此 `GtkHScroll` 实例创建的调整对象，也可以其他控件实例正在使用的其他调整对象。虽然你可以传递 `NULL` 作为参数，这将使滚动条失效；系统会为你创建一个调整对象，但该调整对象的属性将不是你的应用程序所需的。你可以通过调用 `gtk_range_get_adjustment()`（在本章稍后描述）来获取代表你创建的调整对象，并使用 `GtkAdjustment` API（同样在本章稍后描述）来设置调整值。你也可以调用 `gtk_range_set_adjustment()` 来设置滚动条调整对象，但归底，直接将一个非 `NULL` 的调整对象传递给 `gtk_hscrollbar_new()` 比使用任何其他方法都要简单。

# GtkVScrollbar

## 类名

`GtkVScrollbar`

## 父类名

`GtkScrollbar`

## 宏

控件类型宏：`GTK_TYPE_VSCROLLBAR`

对象到控件转换宏：`GTK_VSCROLLBAR(obj)`

控件类型检查宏：`GTK_IS_VSCROLLBAR(obj)`

## 应用程序级 API 摘要

在运行时返回常量 `GTK_TYPE_VSCROLLBAR`：

```c
GtkType
gtk_vscrollbar_get_type(void)
```

创建一个带有可选调整对象的 `GtkVScrollbar` 新实例：

```c
GtkWidget *
gtk_vscrollbar_new(GtkAdjustment *adjustment)
```

## 类描述

`GtkVscrollbar` 与 `GtkHScroll` 类似，但它用于创建垂直滚动条，而不是水平滚动条。与 `GtkHbar` 一样，只有一个感兴趣的函数用于创建 `GtkVscrollbar`：

```c
GtkWidget *
gtk_vscrollbar_new(GtkAdjustment *adjustment)
```
