
```
001 #include <gtk/gtk.h>
002 
003 int main( int argc, char argv[] )
004 {
005     GtkWidget *window, *packer, *one, *two, *three;
006     GdkColor color;
007     GtkStyle *style;
008     GtkPackerOptions options;
009 
010 gtk_init(&argc, &argv);
011 
012 window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
013 gtk_signal_connect(GTK_OBJECT(window), "destroy",
014                                     GTK_SIGNAL_FUNC(gtk_main_quit), "WM destroy");
015 gtk_window_set_title(GTK_WINDOW(window), "Packer");
016 
     style = gtk_style_new();
019     color.red = 0x0;
020     color.green = 0x0;
021     color.blue = 0x0;
022     style->bg[GTK_STATE_NORMAL] = color;
023     gtk_widget_set_style(window, style);
024 
     packer = gtk_packer_new();
025     options = 0;
026 
     one = gtk_drawing_area_new();
029     gtk_widget_set_size(one, 100, 50);
030     gtk_packer_add_defaults(GTK_PACKER (packer), one,
                               GTK_SIDE_BOTTOM, GTK_ANCHOR_CENTER, options);
032     style = gtk_style_new();
033     color.red = 0x8000;
034     color.green = 0x8000;
035     color.blue = 0x8000;
036     style->bg[GTK_STATE_NORMAL] = color;
037     gtk_widget_set_style(one, style);
038     gtk_widget_show(one);
039     two = gtk_drawing_area_new();
```

# GtkPacker 507

```
gtk_widget_set_size(two, 40, 40 );
gtk_packer_add_defaults(GTK_PACKER packer ), two,
GTK_SIDE_BOTTOM, GTK_ANCHOR_CENTER, options );
style = gtk_style_new();
color.red = 0xffff;
color.green = 0xffff;
color.blue = 0xffff;
style-bg[GTK_STATE_NORMAL] = color;
gtk_widget_set_style(two, style );
gtk_widget_show(two );
tree = gtk_drawing_area_new();
gtk_widget_set_size(three, 20, 20 );
gtk_packer_add_defaults(GTK_PACKER ( packer ), three,
GTK_SIDE_RIGHT, GTK_ANCHOR_CENTER, options );
style = gtk_style_new();
color.red = 0xffff;
color.green = 0xffff;
color.blue = 0xffff;
style-bg[GTK_STATE_NORMAL] = color;
gtk_widget_set_style(three, style );
gtk_widget_show(packer );
gtk_container_add(GTK_CONTAINER ( window ), packer );
gtk_widget_show(window );
gtk_main( );
return(0);
}
```

在前面的示例中，我创建一个窗口并将其背景设置为黑色（第 012 到 022 行）。第 024 行创建一个 `packer` 部件。该 `packer` 通过剩余代码持有三个绘制区域部件。第 027 到 037 行，创建了一个 100x50 的灰色绘制区域并将其打包到 `packer` 的底部。第 039 到 049 行，创建了一个 40x40 的白色绘制区域部件并同样打包到 `packer` 的底部，这导致它位于之前打包的（灰色）绘制区域之上。最后，第 051 到 061 行，将一个 20x20 的浅色绘制区域打包到 `packer` 的右侧。它比第二个（白色）绘制区域更高，因为第二个部件拥有它左侧（水平方向）的空间。图 11.7 显示了结果。

表 11.4 GTK_FILL_X 和 GTK_FILL_Y 选项

| 标志 | Tcl/Tk pack 参数 |
| :--- | :--- |
| `GTK_FILL_X` | -fill x |
| `GTK_FILL_Y` | -fill y |

我们可以将这些选项应用于前面的代码查看填充是如何工作的。唯一需要的更改是第 025 行：

`025 options = GTK_FILL_X;`

结果如图 11.8 所示：

![](img/b9af04aaed46302cb075052312fcd667_540_0.png)

这里发生的情况相对简单。如果不指定 `GTK_FILL_X`，绘制区域部件将只占据它们所需的空间。绘制区域一是所有绘制区域中最宽的，因此定义了后续添加其他绘制区域的区域。让我们看看指定 `GTK_FILL_X` 作为选项时会发生什么。首先，绘制区域一是 `packer` 部件中打包的最宽部件，它占据了 `packer` 的整个宽度。因此，它没有可以填充的空间。但绘制区域二并非如此。绘制区域二小于一，会被 `packer` 调整大小，使其宽度与其打包的“空隙”相同。无论是否指定 FILL_X，这个空隙在某种意义上都是为绘制区域二预留的，这就是即使绘制区域三打包在父区域的右侧，它仍然位于绘制区域二上方。

你会发现绘制区域三没有占据 `packer` 的整个宽度；尽管我们为它指定了 `GTK_FILL_X`，它仍然保持 20×20 的尺寸。这是因为我们在底部、顶部、左侧或右侧打包部件时，部件的侧是因为它们是用 `GTK_SIDE_BOTTOM` 打包的。因此，它们可以在 x 方向上填充。相反，绘制区域三是使用 `GTK_SIDE_RIGHT` 打包的。因此，它可以在 y 方向上填充，该部件忽略了 `GTK_FILL_X` 选项。因此，绘制区域三在打包后保留了原始尺寸。这引导我们离开了表 11.5。

表 11.5 适用于 GTK_FILL_X 和 GTK_FILL_Y 的打包选项

| 选项 | 适用打包 |
| :--- | :--- |
| `GTK_FILL_X` | `GTK_SIDE_TOP`, `GTK_SIDE_BOTTOM` |
| `GTK_FILL_Y` | `GTK_SIDE_LEFT`, `GTK_SIDE_RIGHT` |

# GtkPacker

如果指定 `GTK_PACK_EXPAND` 作为选项，则此表无效（参见下文讨论）。下图说明了当我们缩放之前的两个客户端时发生的情况。图 11.9 显示了选项设置为 0 的情况，图 11.10 显示了设置为 `GTK_FILL_X` 的情况。图 11.9 中的两个绘制区域都没有缩放填充窗口，但在图 11.10 中它们缩放了。

![](img/b9af04aaed46302cb075052312fcd667_541_0.png)

**图 11.9** 缩放窗口的图 11.7

![](img/b9af04aaed46302cb075052312fcd667_541_1.png)

**图 11.10** 缩放窗口的图 11.8

顺便说一下，将 `GTK_FILL_X` 和 `GTK_FILL_Y` 进行或运算（如下所示）与在 Tcl/Tk 中指定“-fill both”相同：

`options = GTK_FILL_X | GTK_FILL_Y;`

# **扩展选项**

最后一个标志是 `GTK_PACK_EXPAND`。此标志对应于 Tcl/Tk 打包参数 `-expand true`。人们很容易混淆 `GTK_PACK_EXPAND` 和 `GTK_FILL_X` 以及 `GTK_FILL_Y`。毕竟，之前的示例展示了扩展到其分配的空隙中的绘制区域。理解区别的关键在于意识到

`GTK_FILL_X` 和 `GTK_FILL_Y` 选项告诉部件填充它们已分配的空腔，而 `GTK_PACK_EXPAND` 则导致空腔本身被扩展。

让我们回到原始示例，看看它是如何工作的（现在请参阅图 11.7）。通过将 `options` 参数更改为 `GTK_PACK_EXPAND`：

```
options = GTK_PACK_EXPAND;
```

我们得到了图 11.11 所示的结果：

![](img/b9af04aaed46302cb075052312fcd667_542_0.png)

图 11.11 图 11.7 选项设置为 GTK_PACK_EXPAND

绘图区域拥有的空腔水平方向上扩展以填充窗口的剩余区域。20x20 的绘图区域放置在该空腔的中心，因为我们指定了 `GTK_ANCHOR_CENTER` 锚点。现在，我们为 `options` 参数添加一个 `GTK_FILL_X` 标记：

```
options = GTK_PACK_EXPAND | GTK_FILL_X;
```

添加 `GTK_FILL_X` 会导致 20x20 的绘图区域扩展到创建的空腔中，因为我们也指定了 `GTK_PACK_EXPAND` 为选项，如图 11.12 所示。

![](img/b9af04aaed46302cb075052312fcd667_542_1.png)

图 11.12 图 11.7 选项设置为 GTK_PACK_EXPAND | GTK_FILL_X

# 锚定

在之前所有的示例中，`gtk_packer_add()` 的 `anchor` 参数都设置为 `GTK_ANCHOR_CENTER`，这是一个很好的默认值。对于那些熟悉 Tcl/Tk packers 的人员来说，`gtk_packer_add()` 的 `anchor` 参数等于 `pack` 命令的 `-anchor` 参数。

让我们回到图 11.7 中的示例。如果我们在打包绘图区域三时将 `anchor` 参数更改为任何其他值（例如 `GTK_ANCHOR_NORTH`），我们仍然会得到相同的结果，因为绘图区域三和它被打包的空腔的大小相同。因此，`anchor` 参数仅在空腔大于被打包的部件时才有效。这就是为什么在图 11.11 中，绘图区域三位于空腔的中心；我们导致空腔比绘图区域大，从而增加了锚点的意义。如果我们在这种情况下强制让绘图区域位于空腔的右边缘，我们将指定 `GTK_ANCHOR_EAST` 锚点参数：

```
024 packer = gtk_packer_new();
025 options = GTK_PACK_EXPAND;
    ...
```

```
051 three = gtk_drawing_area_new();
052 gtk_widget_set_size( three, 20, 20 );
053 gtk_packer_add_defaults( GTK_PACKER ( packer ), three,
054 GTK_SIDE_RIGHT, GTK_ANCHOR_EAST, options :);
```

`GtkPacker` 将根据部件被打包的空腔使用合理的 `anchor` 参数值。如果空腔的高度与部件的高度相同，则忽略锚点的北和南部分。同样，如果空腔的宽度等于被打包子部件的宽度，则忽略西部分。例如，锚点 `GTK_ANCHOR_NORTH_EAST` 在空腔的高度与被打包的子部件的高度相同时等同于指定 `GTK_ANCHOR_NORTH`；在空腔的高度与被打包的子部件的高度相同时等同于 `GTK_ANCHOR_EAST`。如果子部件的大小和空腔的大小相同，实际上 `anchor` 参数可以设置为任何值，尽管我建议你使用 `GTK_ANCHOR_CENTER` 并检查你的应用程序，以确保容器窗口的几何变化（例如窗口缩放）行为符合你的预期。

关于锚定的更详细讨论和额外的 Tcl/Tk 代码示例，请参阅 Brent Welch 的书。

# 边框宽度和内边距

你可以通过 `gtk_packer_set_default_border_width()` 设置应用于所有打包到 `packer` 中的子部件的边框宽度：

```
void
gtk_packer_set_default_border_width(GtkPacker *packer, guint border);
```

参数 `packer` 是 `GtkPacker` 的实例，`border` 是所需的无符号整数边框宽度。图 11.13 展示了通过在每个子部件周围设置 5 像素的边框对图 11.7 布局的影响：

![](img/b9af04aaed46302cb075052312fcd667_543_0.png)

图 11.13 图 11.7 默认边框宽度为 5 像素

# 512

第 11 章 更多容器类

`GtkPacker` 识别两种内边距（padding）。这两种内边距都控制除了被打包部件外，为打包到 `packer` 中的部件分配多少空间。使用内部内边距，部件的大小按指定值增加，部件将调整自身以适应该大小。使用外部内边距，部件的大小不会 way，但如果 `packer` 的边框宽度不为零，`GtkPacker` 将像在部件周围添加边框一样在部件周围添加额外空间。指定边框宽度 5 和外部内边距 5 等同于将边框宽度或外部内边距设置为0。可以分别为 x 和 y 维度指定外部和内部内边距；而间距（spacing）则应用于 x 和 y 维度（例如）。图 11.14 展示了将 x 维度外部内边距设置为 5，y 维度设置为 20 的效果。在此示例中边框宽度设置为 0。图 11.15 展示了设置内部内边距。注意，部件的大小发生了变化。

![](img/b9af04aaed46302cb075052312fcd667_544_0.png)

图 11.14 图 11.7 外部内边距 X=5, Y=20

![](img/b9af04aaed46302cb075052312fcd667_544_1.png)

图 11.15 图 11.7 内部内边距 X=5, Y=20

# GtkPacker 513

要设置 `packer` 在 x 和 y 维度上的默认外部内边距，调用 `gtk_packer_set_default_pad()`：

```
void
gtk_packer_set_default_pad(GtkPacker *packer, guint pad_x, guint pad_y);
```

参数 `pad_x` 和 `pad_y` 指定将添加到 `packer` 所有子部件的外部内边距。要设置内部内边距，调用 `gtk_packer_set_default_ipad()`：

```
void
gtk_packer_set_default_ipad(GtkPacker *packer, guint i_pad_x, guint i_pad_y);
```

参数与 `gtk_packer_set_default_pad()` 相同，影响的是内部而不是外部。你可以使用 `gtk_packer_set_child_padding()` 一次性设置给定部件的所有打包选项，覆盖最初最初添加到 `packer` 时设置的任何值。`gtk_packer_set_child_padding()` 的函数原型如下：

```
void
gtk_packer_set_child_padding(GtkPacker *packer, GtkWidget *child,
GtkSideType type, GtkAnchorType anchor,
GtkPackerOptions options, guint border_width, guint pad_x,
guint pad_y, guint i_pad_x, guint i_pad_y);
```

参数等于传递给 `gtk_packer_add()` 的参数。

# 重新排序部件

这里使用的最后一个函数是将 `packer` 的子部件移动到打包顺序中的指定位置：

```
void
gtk_packer_reorder_child(GtkPacker *packer, GtkWidget *child,
guint position);
```

`packer` 是 `GtkPacker` 的相关实例，`child` 是正在移动的部件，`position` 是在 `gtk_packer_reorder_child()` 返回后该部件在打包顺序中的新位置。位置的范围为 [0, n-1]，其中 n 是 `packer` 管理的子部件数量。假设我们有位于位置 0、1 和2 的三个部件——a、b 和 c。如果我们将部件 a 的位置更改为1，部件 b 将位于位置 0，而 c 将保持在位置 2。从 m 移动到另一个位置 n < m 会导致 m 到 m-1 位置的部件位置增加 1。将部件 m 移动到某个位置 p > m 会导致 m+1 到 p 位置的部件位置值减少 1。

# 514

# 第 11 章 更多容器类

![](img/b9af04aaed46302cb075052312fcd667_546_0.png)

图 11.16 五个按钮，从左到右打包
