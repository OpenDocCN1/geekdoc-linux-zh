
许多 `Gtk+` 部件类并不会为应用程序请求实例化的每个实例创建一个 X 窗口。这些部件类中，许多是容器类，它们创建的实例对用户是不可见的，因此不需要窗口。其他类则依赖于部件实例层级来提供一个窗口，其内容在该窗口中渲染。

以下是某些不会为每个实例化的部件创建 X 窗口的 `Gtk+` 部件类列表：`GtkFrame`, `GtkAspectFrame`, `GtkCTree`, `GtkHBBox`, `GtkVBox`, `GtkHBox`, `GtkVBox`, `GtkSeparator`, `GtkVSeparator`, `GtkImage`, `GtkLabel`, `GtkOptionMenu`, `GtkPacker`, `GtkPixmap` 和 `GtkTable`。

让我们剩下的讨论关注 `GtkTable`。`GtkTable` 不为其或其单元格创建窗口。单元格的内容要么在占据该单元格的部件创建的窗口中绘制，要么在部件实例层级更高的部件创建的窗口中绘制（即 `GtkTable` 部件实例的祖先）。

在本章之前介绍井棋示例中，游戏板是一个 `GtkTable` 实例。表格包含九个单元格，组织为三行三列。表格中的每个单元格管理一个 `GtkPixmap` 实例（pixmap 代表单元格的当前占用者，可以是 X 或 O 步，也可以是空单元格）。每个 pixmap 都根据 `GtkTable` 部件实例为其计算的布局，在顶层窗口（`GtkWindow` 实例）中绘制自己。图 11.36 展示了我刚刚描述的井棋盘的实例层级：

### GtkEventBox 561

![](img/b9af04aaed46302cb075052312fcd667_593_0.png)

图 11.36 井棋实例层级

假设由 `GtkWindow` 实例创建的窗口接收到一个 expose 事件（窗口被映射，或窗口的某部分变得未遮挡，可能是由于用户移动了在窗口堆叠顺序中较高的窗口，从而暴露了窗口的一部分）。为了处理此事件，`GtkWindow` 实例将（实际上）将事件传递给它的每个子部件（在这种情况下是单个 `GtkTable` 实例）。`GtkTable` 实例将接收该事件，并通过调用它的每个子部件（在这种情况下是 `GtkPixmap` 实例）来处理 expose 事件来处理它。每个 `GtkPixmap` 实例反过来将通过在提供的窗口中绘制自己来处理 expose 事件。显然，在这种情况下，表格没有为自己或其每个子部件创建窗口，也没有必要每个 `GtkPixmap` 实例创建一个窗口。另一方面，某些部件确实有必要创建自己的窗口。这样的类是 `GtkButton`。除了需要绘制自己（如果这是它的需求，它就不需要窗口）外，它还必须处理按钮按下和按键事件，并响应进入和离开事件，这些事件会在进入和离开预亮阶段（prelight stage）时触发重绘。

如果我们放置按钮而不是 pixmap，作为我们井棋部件的子部件，我们将获得点击它们的能力，并且按钮将像任何按钮一样响应进入和离开事件。

然而，假设我们希望 pixmap 响应按钮通常会响应的事件之一。鉴于 pixmap 没有窗口，因此不能作为 X 事件的目标，我们如何实现这一点呢？我们有几种方法可以做到这一点。一种方法是将我们的 pixmap 替换为 `GtkButton` 实例，让表格的 pixmap（如果有）接收按钮事件。这样做可行，但我们可能会继承使用按钮的所有开销。

更好的方法是，我们可以决定 event box 作为其包含的部件的封装；`GtkEvent` 设计用于为无法创建自己窗口的部件提供 X 窗口。应用这种策略的井棋游戏实例层级如图 11.37 所示：

![](img/b9af04aaed46302cb075052312fcd667_595_0.png)

图 11.37 带有 Event Box 的井棋实例层级

如果用户在井棋单元格上点击按钮，按钮按下事件将发送到指针所在单元格相关的 `GtkEvent`，而不是发送到表格实例所属的 `GtkWindow` 实例。应用程序可以轻松地为每个单元格关联唯一的按钮按下回调函数，而无需根据父窗口中鼠标点击的位置自行执行回调分发。由于每个单元格都有自己的窗口，应用程序可以需要按单元格修改事件处理（例如，它可能不想处理来自空单元格的事件）。

## 创建 Event Box 部件

函数 `gtk_event_box_new()` 用于创建一个 `GtkEventBox` 实例：

```c
GtkWidget *
gtk_event_box_new(void);
```

返回值 `GtkWidget` 实例是一个为其子部件创建唯一 X 窗口的容器。可以使用 `gtk_container_add(_)` 将子部件添加到容器中，如下所示。

以下代码创建一个 `GtkEventBox` 实例，将 `GtkPixmap` 作为其子部件添加到 event box，并对 event box 请求移动事件。当用户在 `GtkEvent` 实例创建的窗口中移动指针过 pixmap 时，回调函数 `MotionNotifyCallback()` 将被调用：

`MotionNotifyCallback` 的细节并不重要；在这里我简单地向标准输出打印消息：

```c
gint
MotionNotifyCallback(GtkWidget *widget, GdkEvent *event,
gpointer data)
{
    printf("A motion notify event was received\n");
}
```

## GtkScrolledWindow

### 类名

`GtkScrolledWindow`

### 父类名

`GtkBin`

### 宏

- 控件类型宏：`GTK_TYPE_SCROLLED_WINDOW`
- 对象到控件转换宏：`GTK_SCROLLED_WINDOW (obj)`
- 控件类型检查宏：`GTK_IS_SCROLLED_WINDOW(obj)`

### 支持的参数

前缀：`GtkScrolledWindow::`

表 11.14 `GtkScrolledWindow` 参数

| 名称 | 类型 | 权限 |
| --- | --- | --- |
| adjustment | `GTK_TYPE_ADJUSTMENT` | `GTK_ARG_READWRITE` | `GTK_ARG_CONSTRUCT` |
| hscroll_policy | `GTK_TYPE_POLICY_TYPE` | `GTK_ARG_READWRITE` |
| vscroll_policy | `GTK_TYPE_POLICY_TYPE` | `GTK_ARG_READWRITE` |
| window_placement | `GTK_TYPE_CORNER_TYPE` | `GTK_ARG_READWRITE` |

### 层级 API 概览

在运行时获取常量 `GTK_TYPE_SCROLLED_WINDOW`：

```c
GtkType
gtk_scrolled_window_get_type(void);
```

创建一个 `GtkScrolledWindow` 实例，可选指定调整项：

```c
GtkWidget *
gtk_scrolled_window_new(GtkAdjustment *adjustment,
GtkAdjustment *adjustment);
```

设置或替换滚动窗口的水平调整项：

```c
void
gtk_scrolled_window_set_hadjust(GtkScrolledWindow
*scrolled_window, GtkAdjustment *hadjust);
```

设置或替换滚动窗口的垂直调整项：

```c
void
gtk_scrolled_window_set_adjustment(GtkScrolledWindow
*scrolled_window, GtkAdjustment *adjustment);
```

获取滚动窗口的水平调整项：

```c
GtkAdjustment *
gtk_scrolled_window_get_hadjust(GtkScrolledWindow
*scrolled_window);
```

获取滚动窗口的垂直调整项：

```c
GtkAdjustment *
gtk_scrolled_window_get_adjustment(GtkScrolledWindow
*scrolled_window);
```

设置水平和垂直滚动条的滚动策略：

```c
void
gtk_scrolled_window_set_policy(GtkScrolledWindow *scrolled_window,
GtkPolicyType hscroll_policy,
GtkPolicyType vscroll_policy);
```

设置滚动窗口的滚动位置偏好：

```c
void
gtk_scrolled_window_set_placement(GtkScrolledWindow
*scrolled_window, GtkType window_placement);
```

向滚动窗口添加一个子控件：

```c
void
gtk_scrolled_window_add_with_viewport(GtkScrolledWindow
*scrolled_window, GtkWidget *child);
```

### 类描述

滚动窗口包含一个区域，在该区域内向用户展示可以由滚动窗口管理的内容。如果内容的大小大于滚动窗口区域的大小，用户可以使用一对滚动条来导航内容。滚动窗口可以作为控件的父级，但它通常会呈现一个显示用户数据或应用程序数据的控件。以下是一些可能由滚动窗口作为父控件的 `Gtk+` 控件示例：

- 显示公司中每位员工记录的 `GtkList` 控件
- 显示文档或备忘录文本的 `GtkText` 控件
- 显示大图片的 `GtkDrawingArea` 控件
- 包含大量行和/或列的 `GtkTable` 控件

如前面的示例所示，滚动窗口解决了在有限大小的窗口或对话框中显示大量数据的问题（当滚动窗口与其他控件共享窗口或对话框时，它是窗口或对话框的一个有尺寸部分）。

使用滚动窗口非常简单。首先，你创建一个滚动窗口并将其作为对话框、窗口或其他某些容器控件的子控件。然后，你创建一个控件并将其作为滚动窗口的子控件。默认的滚动条策略是让 `GtkScrolledWindow` 根据需要显示滚动条。只有当被滚动窗口管理的子控件的大小大于分配给滚动窗口的区域时，滚动条才会显示。这是默认策略，适用于大多数应用程序。另一种滚动条策略是无论滚动窗口或被管理的子控件的大小如何，都显示水平和垂直滚动条。

你如何添加子控件取决于所添加的子控件类型或其是否支持。有两种基本情况：要么子控件支持滚动条调整，或者如果子控件不支持滚动条调整，你可以使用 `gtk_container_add()` 将子控件添加到滚动窗口。我将在“向滚动窗口添加子控件”章节中描述如何处理此情况。

## 创建 ScrolledWindow

要创建 `GtkScrolledWindow` 实例，请调用 `gtk_scrolled_window_new()`：

```c
GtkWidget *
gtk_scrolled_window_new(GtkAdjustment *adjustment,
	GtkAdjustment *adjustment);
```

与其他 `*_functions` 一样，它返回一个 `GtkWidget` 实例。你可以使用 `GTK_SCROLLED_WINDOW` 宏将其转换为 `GtkScrolledWindow` 实例。`adjustment` 和 `adjustment` 参数指定了你创建或从使用调整项的其他控件获取的调整对象。在大多数情况下，你会希望将这些设置为 `NULL` 并使用自动创建的调整项。

## 向滚动窗口添加子控件

要向滚动窗口添加子控件，你可以执行以下操作：

- 如果子控件支持滚动条调整，使用 `gtk_container_add()` 添加子控件。
- 通过 `gtk_scrolled_window_add_with_viewport()` 添加子控件。

## 设置和获取水平与垂直调整

设置或替换滚动窗口的水平调整项：

```c
void
gtk_scrolled_window_set_hadjust(GtkScrolledWindow
*scrolled_window, GtkAdjustment *hadjust);
```

设置或替换滚动窗口的垂直调整项：

```c
void
gtk_scrolled_window_set_adjustment(GtkScrolledWindow
*scrolled_window, GtkAdjustment *adjustment);
```

获取滚动窗口的水平调整项：

```c
GtkAdjustment *
gtk_scrolled_window_get_hadjust(GtkScrolledWindow
*scrolled_window);
```

获取滚动窗口的垂直调整项：

```c
GtkAdjustment *
gtk_scrolled_window_get_adjustment(GtkScrolledWindow
*scrolled_window);
```

## 覆盖默认调整

在下面的示例中，我创建一个包含 40 行和 40 列的 `GtkTable` 实例：

```c
#include <gtk/gtk.h>

#define ROWS 40
#define COLS 40

void
GtkScrolledWindow()
{
    GtkWidget *spinner, *button, vbox, *dlog, *table;
    GtkAdjustment *adj1, *adj2;
    int i, j;
    char buf[32];

    dlog = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_window_position(GTK_WINDOW(dlog), GTK_WIN_MOUSE);
    gtk_widget_set_size(GTK_WIDGET(dlog), 200, 200);

    gtk_signal_connect(GTK_OBJECT(dlog), "destroy",
    GTK_SIGNAL_FUNC(gtk_window_destroyed), &dlog);
    gtk_window_set_title(GTK_WINDOW(dlog),
    "GtkScrolledWindow Demo");
    gtk_container_border_width(GTK_CONTAINER(dlog), 0);

    vbox = gtk_vbox_new(FALSE, 0);
    gtk_container_add(GTK_CONTAINER(dlog), vbox);

    sw = gtk_scrolled_window_new(NULL, NULL);
    gtk_box_pack_start(GTK_BOX(vbox), sw, TRUE, 0);

    table = gtk_table_new(ROWS, COLS, TRUE);
    gtk_scrolled_window_add_view(GTK_SCROLLED_WINDOW(sw), table);

    for (i = 0; i < ROWS; i++) {
        for (j = 0; j < COLS; j++) {
            sprintf(buf, "%d, %d", i, j);
            button = gtk_button_new_with_label(buf);
            gtk_table_attach_defaults(GTK_TABLE(table),
            button, j, j + 1, i + 1);
        }
    }

    hbox = gtk_vbox_new(FALSE, 0);
    gtk_box_pack_end(GTK_BOX(vbox), hbox, FALSE, FALSE, 0);

    adj1 = (GtkAdjustment *)gtk_adjustment_new(0.0, 0.0,
    (float)COLS - 1, 1.0, 1.0, 0.0);
    spinner = gtk_spin_button_new(adj1, 0, 0);
    gtk_box_pack_start(GTK_BOX(hbox), spinner, FALSE, FALSE, 0);

    gtk_widget_show_all(GTK_WIDGET(dlog));
    gtk_main();
}
```

### 570 第11章 • 更多容器类

```c
gtk_spin_button_wrap (GTK_SPIN_BUTTON (spinner), TRUE);
gtk_box_pack_start (GTK_BOX (hbox), spinner, TRUE, 0);
adj2 = (GtkAdjustment *) gtk_adjustment_new(0, 0.0, 0.0,
      (gFLOAT) -1.0, 1.0, 0, 0);
spinner = gtk_spin_button_new(adj2, 0, 0);
gtk_spin_button_wrap (GTK_SPIN_BUTTON (spinner), TRUE);
gtk_box_pack_start (GTK_BOX (hbox), spinner, TRUE, 0);
gtk_scrolled_window_set_adjustment (GTK_SCROLLED_WINDOW ( sw ), adj1);
gtk_scrolled_window_set_adjustment (GTK_SCROLLED_WINDOW ( sw ), adj2);
gtk_widget_show_all (dock);
main(int argc, char *argv[]) {
  gtk_init(&argc, &argv);
  CreateScrolledWindow();
  gtk_main();
}
```
