
如果 `visible` 设置为 `TRUE`，则列将显示；如果设置为 `FALSE`，则被隐藏。列的可见性应该由用户控制（例如，通过偏好设置）。

## 表 6.8 用于设置列属性的函数

| 属性 | 函数(s) |
| --- | --- |
| 列对齐 | `gtk_clist_set_column_justification()` |
| 列可见性 | `gtk_clist_set_column_visibility()` |
| 列缩放 | `gtk_clist_set_column_resizable()` |
| | `gtk_clist_set_column_autosize()` |

## 表 6.9 列对齐选项

| 选项 | 含义 |
| --- | --- |
| `GTK_JUSTIFY_LEFT` | 初始字符位于单元格第一个位置 |
| `GTK_JUSTIFY_RIGHT` | 最后一个字符位于单元格最后一个位置 |
| `GTK_JUSTIFY_CENTER` | 文本在单元格内居中 |
| `GTK_JUSTIFY_FILL` | 与 `GTK_JUSTIFY_CENTER` 相同（源代码处理两个常量，这可能是一个错误）。 |

# GtkClist 235

正如我之前提到的，用户可以通过将指针悬停在列标题的任一末端，点击鼠标左键并拖动来调整其新大小。您的应用程序可以通过调用 `gtk_clist_set_column_resizable()` 来按列禁用（或重新启用）此功能：

```
void
gtk_clist_set_column_resizable(GtkClist *clist, gint column,
               boolean resizable);
```

如果参数 `resizable` 设置为 `TRUE`，则用户可以调整列的大小（这是默认值）。如果设置为 `FALSE`，则用户无法更改列的大小。

`clist` 中列的大小可以通过 `GtkClist` 提供的若干例程来控制。列可以被“自动调整大小（autosized）”，在这种情况下，列宽的设置将使得列表中显示的最大项目清晰可见。否则，列的大小将由显示列标题所需的空间决定。

自动调整大小可以按列指定，也可以针对 `GtkClist` 中的所有列进行指定。要指定列是否应根据其内容自动调整到最佳宽度，请调用 `gtk_clist_set_column_auto_resize()`：

```
void
gtk_clist_set_column_auto_resize(GtkClist *clist, gint column,
               boolean auto_resize);
```

参数列表和列现在应该已经熟悉了。如果 `auto_resize` 设置为 `TRUE`，当数据被添加到或从 `clist` 中移除时，列将自动调整自身大小，以确保所有数据都是可见的。如果为 `FALSE`，列的大小将基于列标题的宽度。您可以通过调用 `gtk_clist_columns_autosize()` 来自动调整 `clist` 中所有列的大小：

```
gint
gtk_clist_columns_autosize(GtkClist *clist);
```

例程 `gtk_clist_optimal_column_width()` 返回显示该列中所有内容所需的列大小：

```
gint
gtk_clist_optimal_column_width(GtkClist *clist, gint column);
```

此大小与当列被自动调整大时分配给该列的大小相同。

您的应用程序可以通过调用 `gtk_clist_set_column_width()` 显式将列的宽度设置为指定值：

```
void
gtk_clist_set_column_width(GtkClist *clist, gint column, gint width);
```

参数是期望的宽度。如果列没有自动调整大小，您可以调用之前描述的 `gtk_clist_optimal_column_width()` 来确定一个能够显示列中所有内容而不裁剪的列宽。

列的大小（包括 `GtkList` 为自动调整大小的列创建）可以通过您的应用程序通过指定最大和最小宽度来控制。如果您指定了最小列宽，则在对列宽进行任何更改之前应用此最小宽度；如果计算或指定的宽度小于最小列大小，则使用最小列大小代替。对于最大列大小也是如此；具有最大限制的列将不允许超过该大小，无论列的内容或 `auto` 属性如何。

要设置列的最小宽度，调用 `gtk_clist_set_column_min_width()`：

```
void
gtk_clist_set_column_min_width(GtkList *clist, gint column,
    int min_width);
```

要设置列的最大宽度，调用 `gtk_clist_set_column_max_width()`：

```
void
gtk_clist_set_column_max_width(GtkList *clist, gint column,
    int max_width);
```

上述函数的参数应该是自言自明的。一如既往，请记住 `clist` 中的列从左到右编号，从 `0` 开始到 `m-1` 结束，其中 `m` 是 `clist` 中列的数。

# 行和单元格 API

现在让我们来看看适用于 `clist` 中数据行以及单个单元格的一些函数。

行高默认设置为当前字体的高度。行高不包括 `clist` 行与行之间的间距。您可以通过调用 `gtk_clist_set_row_height()` 来覆盖计算出的行高：

```
void
gtk_clist_set_row_height(GtkList *clist, gint height);
```

传递高度 `0` 会导致高度与当前字体相同。`clist` 中的每个单元格都有一个特定类型。单元格类型定义在表 6.10 中。

### 表 6.10 单元格类型

| 单元格类型 | 意义 |
| :--- | :--- |
| `GTK_CELL_EMPTY` | 单元格不包含数据。 |
| `GTK_CELL_TEXT` | 单元格包含文本。 |
| `GTK_CELL_PIXMAP` | 单元格包含位图（pixmap）数据。 |
| `GTK_CELL_PIXTEXT` | 单元格同时包含文本和位图数据。 |
| `GTK_CELL_WIDGET` | 该类型在 `Gtk+ 1.2` 中尚未实现。 |

# GtkClist

要获取行 = `m`，列 = `n` 单元格的类型，调用 `gtk_clist_get_cell_type()`：

```
GtkCellType
gtk_clist_get_cell_type(GtkClist *clist, int row, int column);
```

如果单元格不存在，`gtk_clist_get_cell_type()` 返回 `-1`。可以通过调用 `gtk_clist_set_foreground()` 和 `gtk_clist_set_background()` 设置行的前景颜色和背景颜色：

```
void
gtk_clist_set_foreground(GtkClist *clist, int row, GdkColor *color);
void
gtk_clist_set_background(GtkClist *clist, int row, GdkColor *color);
```

在接下来的代码中，字体也被更改为 16 点的 Helvetica，并将新的样式信息与 `gtk_clist_set_style()` 的调用关联起来。

```
// 现在更改字体
gtk_clist_unref(style->font);
style->font =
gtk_font_load("*-helvetica-*-*-*-16--*-*---*-*-*");
// 最后，更改新样式
gtk_clist_set_style(GTK_CLIST(list), 0, 3, style);
```

函数 `gdk_font_unref()` 接收一个类型为 `GdkFont *` 的参数。它将字体的引用计数减 1。如果引用计数变为 0，则该字体（或字体类型）将被释放。`gdk_font_load()` 函数创建一个新的 `GdkFont`，将其引用计数设为 1，并返回它的引用（也是一个 `GdkFont *`）。我们只需要将样式的 `font` 字段设置为 `gtk_font_load()` 返回的值，即可更改样的字体。当样式属性发生变化后，通过调用 `gtk_clist_set_style()` 将修改后的样式与列表中位置为 `0, 3` 的单元格关联。

关于上述代码的一个细微之处是，我们获取了单元格全局样式的副本，将其作为我们自己的模板。这个全局样式在类被 `GtkList` 实现时被用于关联该类。假设我们已经对单元格 `0, 3` 做了修改，稍后在应用程序中我们想要再次修改它（将字体更改为其他）。这里有两种方案。一种是制作单元格全局样式的副本，执行之前相同的更改（设置 `GTK_STATE_ACTIVE` 和 `GTK_STATE_SELECTED` 状态的前景颜色），然后设置新字体。另一种方案是获取单元格样式的副本，该副本已经设置了所需的颜色，只需修改字体即可。要获取单元格样式的副本，可以如下所示使用 `gtk_clist_get_cell_style()`：

```
GtkStyle *style;
style = gtk_clist_get_cell_style(GTK_CLIST(list), 0, 3);
style = gtk_style_copy(style);
```

此时，你可以像之前所示的那样修改样式以设置新字体，然后调用 `gtk_clist_set_cell_style()` 使更改生效。`gtk_clist_get_cell_style()` 的函数原型为：

```
GtkStyle *
gtk_clist_get_cell_style(GtkClist *list, gint row, gint column);
```

`gtk_clist_get_cell_style()` 的参数应该是自而易懂的。如果任何参数无效（`GtkStyle`），则返回 `NULL`。同样，如果单元格没有关联样式，则返回 `NULL`。

对于列表中的行，也存在与 `gtk_clist_set_cell_style()` 和 `gtk_clist_get_cell_style()` 类似的函数。`gtk_clist_set_row_style()` 函数设置的样式将应用到该行中所有未设置单元格样式的单元格：

```
void
gtk_clist_set_row_style(GtkList *clist, int row, GtkStyle *style);
```

`gtk_clist_get_row_style()` 函数类似于 `gtk_clist_get_cell_style()`。然而，检索到的样式是应用到行中没有应用单元格样式的样式。与单元格一样，如果没有对指定的行应用行样式，则将返回 `NULL`。以下是 `gtk_clist_get_row_style()` 的函数原型：

```
GtkStyle *
gtk_clist_get_row_style(GtkList *clist, int row);
```

你的应用程序可能会发现需要对单元格中显示的位图或文本的左上角应用垂直/或水平偏移。如果是这样，你可以调用 `gtk_clist_set_shift()` 来指定这些偏移：

```
void
gtk_clist_set_shift(GtkList *clist, int row, int column, int vertical, int horizontal);
```

参数 `row`、`list` 和 `column` 指定了应用偏移的列表和单元格。参数 `vertical` 和 `horizontal` 是大于 0 的像素数，它们将加到单元格中渲染的文本或位图的左上角起点处。默认情况下，正如之前讨论的，单元格的高度是用于渲染内容的字体高度，而单元格的宽度由单元格所在的列宽定义。在单元格中显示数据的起点添加偏移可能会导致数据被裁剪；单元格不会调整大小以确保显示的数据可见。`Autos` 也无法提供帮助；尺寸是在应用偏移之前就确定的。确保列宽足够显示带有水平偏移的内容的唯一方法是使用一个 `GtkList` 函数来显式设置列宽。然而，没有明显的方法可以确保垂直偏移不会被裁剪。

你的应用程序可以通过调用 `gtk_clist_set_selectable()` 来控制列表中行的可选性：

```
void
gtk_clist_set_selectable(GtkList *clist, int row, gboolean selectable);
```

# GtkClist

它有一个 `select_row` 信号用于跟踪当前选中项，还有一个我们可以调用来获取选中项的函数。例如：

```c
static gint gCurrentSelection = -1;
```

```c
gint
GetCurrentSelection( void )
{
    return( gCurrentSelection );
}
```

```c
void
SetCurrentSelection(GtkWidget *widget, gint row, gint column, GtkEventButton *event, gpointer data)
{
    gCurrentSelection = row;
}
```

`Gtk+` 传递给 `SetCurrentSelection()` 的参数并不是应用程序与该行关联的客户端数据（使用我即将介绍的函数）。然而，它是作为第四个参数传递给 `gtk_signal_connect()` 的客户端数据，该函数是由应用程序通过调用 `gtk_signal_connect()` 将 `SetCurrentSelection()` 注册为列表的 `select_row` 信号的句柄。（有关信号和信号函数的更多信息，请参阅第 3 章。）

以下函数 `DeleteItemItem` 是在点击列表下方删除按钮时调用的信号函数。

```c
void
DeleteItemItem( GtkWidget *widget, gpointer client_data )
{
    Grab *myNode;
    // 获取客户端数据
    if ( gCurrentSelection == -1 ) // 无选中
        return;
    myNode = (Record *) gtk_list_get_row_data( (GTK_CLIST(list), gCurrentSelection ) );
    if ( myNode->delete == 1 )
        myNode->delete = 0;
    else
        myNode->delete = 1;
    UpdatedDeletedRowGUI( list, gCurrentSelection, myNode->delete );
}
```

`DeleteItem()` 执行的第一件事是检查用户是否已进行了选择。如果 `gCurrentSelection` 为 `-1`，则没有选中项且函数返回（一种用户友好的响应是显示消息对话框，指示用户先选择一个项目并重试）。在获取选中项后，调用了 `gtk_clist_list_get_row_data()`。`gtk_clist_list_get_row_data()` 的函数原型如下：

```c
gpointer
gtk_clist_get_row_data(GtkClist *clist, int row);
```

参数 `clist` 是要从中检索客户端数据的 `clist`，`row` 是从中检索的行。参数 `row` 一如既往，范围在 `[0, m-1]` 之间，其中 `m` 等于当前 `clist` 中的行数。该函数的返回值是一个类型为 `pointer` 的通用指针。如你所见，我将返回值强制转换为 `Record *` 类型并将其赋值给同类型的局部变量。现在应用程序已经从该行检索了指针，它就可以对删除该项目的请求做出响应，即切换该项的已删除状态。最后，一个名为 `UpdateDeletedGUI()` 的函数将更改活动（或已删除）行的样式。在这个示例中，我可能会调用 `gtk_clist_set_row_style()` 来更改标记为已删除的行的前景颜色，或者将已删除行的前景颜色恢复为默认的黑色。早些在描述 `GtkClist` 中样式如何工作时，已经介绍了一个如何设置行前景颜色的示例。

这些按钮的基本逻辑如下：你需要实现一个对话框，由与“添加（Add）”和“修改（Modify）”按钮相关的点击信号函数显示。同一个对话框可以用于两者。在“修改”情况下，它会显示与所选行关联的所有数据，允许用户进行编辑。可以调用 `gtk_clist_get_row_data()` 函数从链表中检索与选中行对应的数据。在“添加”操作情况下，对话框的控件是未初始化的，对话框用于获取有关新上下文的信息。对话框中的“取消”按钮可以关闭对话框并取消通知。对话框中的“确定”按钮可以接受对数据进行的更改。在“确定”按钮的点击信号函数中，数据被检索并写入链表中的节点。在“修改”操作情况下，该节点已存在于链表中并已与某行关联。在“添加”操作情况下，应用程序必须创建一个类型为 `Record` 的节点，将其添加到链表中，并将其字段设置为用户输入的数据。此外，应用程序必须向 `clist` 附加一个新行，并将新添加的节点与此 `clist` 关联。为了建立链表中的节点与 `clist` 中的行之间的关联，应用程序必须调用 `gtk_clist_set_row_data()` 函数：

```c
void
gtk_clist_set_row_data(GtkClist *clist, int row, gpointer data);
```
