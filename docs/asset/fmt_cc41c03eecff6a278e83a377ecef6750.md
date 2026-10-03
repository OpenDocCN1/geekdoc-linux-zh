
# 第 4 章

## 表格

布局表格（`GtkTable`）在构建用户界面时提供了很大的灵活性，但同时也增加了复杂性。通过表格，你可以指定行数和列数。然后你可以将组件放入网格的单元格中，并指定组件的宽和高。例如，你可以将组件放在 (0, 0)（表格的左上角），让它向右延伸三列，向下延伸二行。创建一个表格并不比布局框复杂。它涉及到调用 `gtk_table_new`，格式如下：

```c
GtkWidget * gtk_table_new (int rows, int columns, gboolean homogenous) ;
```

如所示，它接受三个参数。第一个是表格中的行数，第二个是列数。最后一个参数是 `homogenous`，我们在本章前面详细介绍过它。将其设置为 `TRUE`，列将采用表格中最大组件的宽度，而行将采用表格中最大组件的高度。不用太担心它，在你自己的表格中稍微尝试一下参数，你就能理解它是如何工作的。

一旦你在这里创建了表格，就可以像通常一样将其添加到窗口或其他类型的布局框中。只需调用 `gtk_container_add`。

下一步是向表格添加一些组件。这里有两种方法可用。最简单的是 `gtk_table_attach_defaults`，如下代码所示：

```c
void gtk_table_attach_defaults (GtkTable * table, GtkWidget * widget,
gint left_attach, int right_attach, int top_attach, int bottom_attach) ;
```

比我们在其他 GTK+ 中看到的参数多得多。顾名思义，它将组件插入表格，并允许你精确指定组件在表格中出现的位置，以及组件的高度和宽度。标题中的“默认”部分指的是我们在处理布局框时遇到的 `expand`、`fill` 和 `padding` 参数。通过 `gtk_table_attach_defaults`，你添加的组件的 `padding` 被设置为 0，而 `expand` 和 `fill` 都被设置为 `TRUE`。结果是，你添加到表格的组件将占据网格中你分配的空间，不少，也不多。

调用时的前两个参数现在应该是显而易见的。它们指定了你想添加组件的表格以及你想添加的组件。这两个参数的工作方式与普通布局框相同。

其余的参数定义了组件的大小和位置。如果你有一个四列四行的表格，那么你实际上拥有编号为 0, 1, 2 和 3 的列。行也是如此。

你向 `left_attach` 和 `top_attach` 传递你想让组件开始的列号和行号。向 `right_attach` 和 `bottom_attach` 传递你想让组件结束的列号和行号。然而，并非完全如此。假设你想让一个组件出现在 (0,0)，即网格的左上位置。代码看起来如下。

```
gtk_table_attach_defaults ( atable, awidget, 0, 1, 0, 1 );
```

这里的关键在于，尽管你想让组件只占据网格中的单个单元格，但你不能像对 `left_attach` 和 `top_attach` 那样为 `bottom_attach` 和 `right_attach` 设置相同的坐标。你必须指定组件想要停止的坐标。因此，在上面的调用中，我们的组件位于 (0, 0) 且不再超过 (1, 1)。因此，它只占据了表格中的单个单元格。让我们来看看实际运行效果。

输入代码，编译并运行 `table.c`：

```c
/**
* table.c
*  一个短的应用程序，用于演示如何
* 使用带有默认打包值的
*表格
*/

#include <gtk/gtk.h>

/* 窗口关闭的信号处理器 */
void CloseApp ( GtkWidget * window, gpointer data )
{
    gtk_main_quit();
}

/* 在表格中创建按钮的实用函数 */
void CreateButtonInTable ( GtkWidget * table, const gchar * caption,
gint left, gint right, gint top, gint bottom)
{
    GtkWidget * button;

    button = gtk_table_new_with_label ( caption );
    gtk_table_attach_defaults ( GTK_TABLE ( table ), left, right, top, bottom);
}

/* 主 ( ) 函数 */
gint main ( gint argc, gchar * argv[])
{
    /* 为窗口设置组件指针 */
    GtkWidget * window;
    /* 为表格设置组件指针 */
    GtkWidget * table;

    gtk_init ( &argc, &argv );
```

```c
/* 以通常方式创建窗口 */
window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
gtk_window_set_title ( GTK_WINDOW ( window ), "Fun with Tables" );
gtk_window_set_default_size ( GTK_WINDOW ( window ), 320, 200 );
gtk_container_set_border_width ( GTK_CONTAINER ( window ), 10 );

/* 将 destroy 信号连接到它的处理器 */
gtk_signal_connect ( GTK_OBJECT ( window ),
    "destroy",
    GTK_SIGNAL_FUNC ( CloseTheApp ),
    NULL );

/* 现在是表格 - 我们来创建一个 10x10 的等高尺寸表格 */
table = gtk_table_new ( 10, 10, TRUE );

/* 将表格添加到窗口 */
gtk_container_add ( GTK_CONTAINER ( window ), table );

/* 现在向表格中添加一些按钮 */
CreateButtonInTable ( table, "Button 1", 0, 1, 0, 1 );
CreateButtonInTable ( table, "Button 2", 2, 8, 2, 5 );
CreateButtonInTable ( table, "Button 3", 9, 10, 9, 10 );
CreateButtonInTable ( table, "Button 4", 7, 8, 5, 9 );

/* 最后，显示所有内容并启动主循环 */
gtk_widget_show_all ( window );

gtk_main ( );

return 0;
```

当你运行应用程序时，你应该会看到一个类似于下面截图的窗口视图：

![](img/aa3546013f120531cd191b770d85869c_131_0.png)

让我们快速看一下代码，看看它们是如何结合在一起的。

主函数的启动方式与其他任何函数一样，重点是创建窗口并分配属性，使其具有实用的尺寸和恰当的标题。

```c
gtk_init (&argc, &argv );
```

```c
/* 以通常方式创建窗口 */
window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
gtk_window_set_title ( GTK_WINDOW ( window ), "Fun with Tables" );
gtk_window_set_default_size ( GTK_WINDOW ( window ), 320, 200 );
gtk_container_set_border_width ( GTK_CONTAINER ( window ), 10 );

/* 将 destroy 信号连接到它的处理器 */
gtk_signal_connect ( GTK_OBJECT ( window ),
    "destroy",
    GTK_SIGNAL_FUNC ( CloseTheApp),
    NULL );
```

在这个窗口示例中，标题被设置为 "Fun with tables"，并分配了宽 300 像素、高 200 像素的尺寸。包含边框也被设置，以便在窗口边缘与表格边缘之间提供间隙。

下一行代码创建了该打包表格。

```c
table = gtk_table_new ( 10, 10, TRUE );
```

创建表格时具有 10 列（第一个参数）和 10 行。它还设置为等高尺寸的，正如我之前解释的，在添加组件后，网格中的每行和每列都将调整为匹配最大的行和列。

组件通过 `CreateButtonInTable` 函数添加，这是一个通用的例程，用于简化在表格中逐个创建按钮的重复任务。

```c
/* 在表格中创建按钮的实用函数 */
void CreateButtonInTable ( GtkWidget * table, const gchar * caption,
gint left, gint right, gint top, gint bottom)
{
    GtkWidget * button;

    button = gtk_table_new_with_label ( caption );
    gtk_table_attach_defaults ( GTK_TABLE ( table ), left, right, top, bottom);
}
```

这里的关键在于，尽管你想让组件只占据网格中的单个单元格，但你不能像对 `left_attach` 和 `top_attach` 那样为 `bottom_attach` 和 `right_attach` 设置相同的坐标。你必须指定组件想要停止的坐标。因此，在上面的调用中，我们的组件位于 (0, 0) 且不再超过 (1, 1)。因此，它只占据了表格中的单个单元格。让我们来看看实际运行效果。

```c
CreateButtonInTable ( table, "Button 1", 0, 1, 0, 1 );
CreateButtonInTable ( table, "Button 2", 2, 8, 2, 5 );
CreateButtonInTable ( table, "Button 3", 9, 10, 9, 10 );
CreateButtonInTable ( table, "Button 4", 7, 8, 5, 9 );
```

当你运行应用程序时，你应该会得到一个类似于下面截图的窗口视图：

![](img/aa3546013f120531cd191b770d85869c_131_0.png)

让我们快速看一下代码，看看它们是如何结合在一起的。

主函数的启动方式与其他任何函数一样，重点是创建窗口并分配属性，使其具有实用的尺寸和恰当的标题。

```c
gtk_init (&argc, &argv );
```

```c
/* 以通常方式创建窗口 */
window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
gtk_window_set_title ( GTK_WINDOW ( window ), "Fun with Tables" );
gtk_window_set_default_size ( GTK_WINDOW ( window ), 320, 200 );
gtk_container_set_border_width ( GTK_CONTAINER ( window ), 10 );

/* 将 destroy 信号连接到它的处理器 */
gtk_signal_connect ( GTK_OBJECT ( window ),
    "destroy",
    GTK_SIGNAL_FUNC ( CloseTheApp),
    NULL );
```

在这个窗口示例中，标题被设置为 "Fun with tables"，并分配了宽 300 像素、高 200 像素的尺寸。包含边框也被设置，以便在窗口边缘与表格边缘之间提供间隙。

下一行代码创建了该打包表格。

```c
table = gtk_table_new ( 10, 10, TRUE );
```

创建表格时具有 10 列（第一个参数）和 10 行。它还设置为等高尺寸的，正如我之前解释的，在添加组件后，网格中的每行和每列都将调整为匹配最大的行和列。

组件通过 `CreateButtonInTable` 函数添加，这是一个通用的例程，用于简化在表格中逐个创建按钮的重复任务。
