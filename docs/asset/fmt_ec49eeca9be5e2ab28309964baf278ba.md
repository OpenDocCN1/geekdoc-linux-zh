
`GtkWidget *dialog_window, *hbox, *list;`

```c
static char *titles[] =
{
    "Name",
    "Date of Birth",
    "Birth Location",
};
```

```c
gtk_init(&argc, &argv);
gtk_window_new();
hbox = gtk_box_new(GTK_ORIENTATION_HORIZONTAL, 0);
gtk_container_add(GTK_CONTAINER(dialog_window), hbox);
list = gtk_clist_new_with_titles(3, titles);
gtk_container_add(GTK_CONTAINER(hbox), list);
gtk_widget_show_all(list);
```

# 创建 Clist 小部件

要创建一个 `clist`，你的应用程序调用以下函数之一：`gtk_clist_new()` 或 `gtk_clist_new_with_titles()`。以下是这两个函数的函数原型：

```c
GtkWidget *
gtk_clist_new(gint columns);
```

```c
GtkWidget *
gtk_clist_new_with_titles(gint columns, gchar *titles[]);
```

第一个函数 `gtk_clist_new()` 创建一个不带列标题集的 `GtkClist` 实例。但请注意，如果没有列标题，`GtkClist` 将无法正确显示你添加到 `clist` 中的内容，除非你显式地设置列表列的宽度。这是因为默认情况下，`GtkClist` 会根据字符串的长度调整列的大小，而不是根据单元格中显示的内容。为了让单元格（以及列）根据内容调整大小，`gtk_clist_set_column_auto_resize()` 将确保列的大小与其内容相匹配。

第二个 `GtkClist` 实例函数是 `gtk_clist_new_with_titles()`。它接受一个额外的参数，即 `char *` 向量。参数中的每个 C 字符串都用作列标题。第 1 列的标题包含在 `titles[0]` 中，第 2 列的标题包含在 `titles[1]` 中，依此类推。如前所述，列的默认宽度基于列标题文本的宽度。

以下代码创建一个 `GtkClist` 实例并设置列标题，以反映将由 `clist` 管理的姓名、出生日期和出生地数据：

```c
GtkWidget *dialog_window, *hbox, *list;

static char *titles[] =
{
    "Name",
    "Date of Birth",
    "Birth Location",
};

gtk_init(&argc, &argv);
gtk_window_new();
hbox = gtk_box_new(GTK_ORIENTATION_HORIZONTAL, 0);
gtk_container_add(GTK_CONTAINER(dialog_window), hbox);
list = gtk_clist_new_with_titles(3, titles);
gtk_container_add(GTK_CONTAINER(hbox), list);
gtk_widget_show_all(list);
```

# 运行时操作

与 `GtkList` 一样，你的程序可以在运行时从 `clist` 添加或删除行。`clist` 唯一的静态属性是每行拥有的列数，这必须在创建 `clist` 时指定。

## 添加和移除列表中的内容

从列表中移除行，`GtkClist` 提供了以下函数：

```c
void
gtk_clist_remove_row(GtkClist *clist, gint row);
```

向列表中插入新项：

```c
void
gtk_clist_insert_row(GtkClist *clist, gint row, GList *values);
```

`gtk_clist_new_with_titles()` 函数接受一个额外的参数，即 `char *` 向量。参数中的每个 C 字符串都用作列标题。第 1 列的标题包含在 `titles[0]` 中，第 2 列的标题包含在 `titles[1]` 中，依此类推。如前所述，列的默认宽度基于列标题文本的宽度。

```c
gtk_clist_get_text(GtkClist *clist, gint row, gchar **text);
```

`clist` 是 `GtkClist` 的实例，一如既常，`row` 和 `column` 表示要检索的单元格，范围分别在 `[0, m-1]` 和 `[0, n-1]` 之间，正如 `gtk_clist_set_text(text)` 中所示。`text` 是一个指向 `char` 的指针。返回值，该指针将指向一个以 `NULL` 终止的字符串，该字符串包含 `clist` 中指定行、列处显示的文本。如果行或列超出范围或遇到其他问题，`text` 的值将不会改变。如果成功，`gtk_clist_get_text(text)` 返回 `1`；否则返回 `0` 表示失败。

请注意不要释放或修改通过 `gtk_clist_get_text()` 参数返回的值所指向的内存。该值指向的是由 `GtkClist` 部件维护的实际字符串，而不是它的副本。

# 显示位图

`Clist` 单元格除了文本外还可以显示位图（pixmap）。`GtkClist` 提供了几个例程，可以将位图与单元格关联。这些例程都接受一个 `GdkPixmap`，它包含要显示的位图，以及一个 `GdkBitmap`，后者定义了位图内要在单元格中显示的像素。

## GDK 位图

在描述这些例程之前，我们需要详细介绍一下 GDK 中位图的使用。GDK 提供了用于创建位图的例程。GDK 的例程是位于 Xlib 例程之上的薄层代码，而它们提供了相同的功能。位图（Pixmaps）和位点图（Bitmaps）包含图像数据，其深度与渲染这些数据的窗口深度一致，而位点图始终是 1 位的。在 X 和 GDK 中，位图和位点图是相同的；唯一的区别在于它们的深度（n 位与 1 位）。

可以使用程序本地数据或通过存储在磁盘上的 X Pixmap (XPM) 文件来创建位图。XPM 文件是 ASCII 文件，最好使用 `xpm(1)` 等工具进行创建和操作。XPM 文件存储在扩展名为 `.xpm` 的文件中，但这不是强制要求的。位点图文件最好使用 `xmap(1)` 或 `bitmap(1)` 等工具进行操作。在 `/usr/include/X11/bitmaps` 中有很多位点图文件示例。位点图和位图在 Linux 和 UNIX 系统上均可用，如果没有，可以通过 ftp 轻松获得。关于这些程序的更多信息，请参阅各自的在线页面。

你可以选择在本节中将讨论的 GDK 函数在运行时将 xpm 和 xbm 数据读入你的程序中，或者你可以在编译时将数据包含在源代码中的 XBM 或 XPM 文件的内容。如果你选择在编译时提供数据，我建议 `#include` xpm 或 xbm 文件。例如：

```c
#include "MyIcon.xpm"
```

这将使你能够使用像 `xpaint` 或 `bitmap` 的程序（作为 C 源代码）更方便地维护数据。最后，涉及的数据量非常小，因此在运行时从文件读取或在编译时包含它很大程度上取决于风格。请参考任何关于 X 窗口系统的优秀书籍。

以下是一个位点图文件 `xlog16`，取自 `/usr/X11/include/bitmaps`。该图像存储了 16×16、1 位的 X 窗口系统标志 (`xlog16`)：

```c
#define xlog16_width 16
#define xlog16_height 16
static unsigned char xlog16_bits[] = {
    0x0f, 0x80, 0x1e, 0xe0, 0x3c, 0x40, 0x78, 0x20, 0x78,
    0x10, 0xf0, 0x08, 0xe0, 0x09, 0x0c, 0x05, 0x00, 0x02, 0x40, 0x07,
    0x20, 0x0f, 0x20, 0x10, 0x1e, 0x08, 0x3c, 0x04, 0x78, 0x02,
    0x0f};
```

以下是一个示例 xpm 文件的内容。在示例中，宽度、高度、颜色数量以及使用多少 ASCII 字符表示位图中的每个像素都编码在 `open` 的第一个用引号分隔的字符串中。你应该能够通过查看 ASCII 数据轻松确定位图的结构（在本示例中，位图表示一个对钩）：

```c
/* XPM */
static char *openfile[] = {
    /* width height num_colors chars_per_pixel */
    " 10 9 5 1",
    /* colors * */
    " c None",
    "# c #000000",
    "# y #666666",
    "# i #ff1f00",
    "# c #9f9f9f",
    /* pixels * */
    "      ",
    "    ......",
    "    ......",
    "  ......",
    "  YYYYYY",
    "    ....",
    "      ",
};
```

让我们看看 GDK 提供的创建位图数据的几个函数，参考提供的示例数据。第一个函数 `gdk_bitmap_create_from_data()` 是 GDK 提供的从位点图数据创建 1 位深度 `GdkPixmap` 的唯一函数：

```c
GdkPixmap *gdk_bitmap_create_from_data(GdkWindow *window, const gchar *data, gint width, gint height);
```

第一个参数 `window` 是 `GdkWindow` 的句柄，这通常是位图要显示的窗口。你可以通过以下代码从 `GtkWidget` 实例获取窗口句柄：

```c
GtkWidget *widget;
GdkWindow *myWindow;
myWindow = widget->window;
```

参数 `data` 是位点图数据；`width` 和 `height` 是自自明的。在 `xlog16` 的情况下，必须将 `xlog16_bits` 作为数据，`xlog16_width` 作为宽度，`xlog16_height` 作为高度。返回时，将返回一个 `GdkPixmap` 指针。要从位图数据创建 n 位深度 `GdkPixmap`，调用 `gdk_pixmap_create_from_data()`：

```c
GdkPixmap *gdk_pixmap_create_from_data(GdkWindow *window, const gchar *data, gint width, gint height, GdkColor *fg, GdkColor *bg);
```

参数 `window` 是 `GdkWindow` 的句柄，具有相同的视觉类（visual class），以及位图将显示。理想情况下，你将传递最终显示 `GdkPixmap` 的窗口。如果你传递 `-1`，将使用服务器根窗口。参数 `data` 与前述相同（例如：`xlog16_bits`），`width` 和 `height` 分别为 `xlog16_width` 和 `xlog16_height`。返回时的深度是位图的，如果你传递 `-1`，则是作为第一个参数传递的窗口的深度。你应该确保位图将稍后显示，否则服务器将产生错误（例如 `BadMatch`）。参数 `fg` 和 `bg` 是结果位图中使用的前景和背景像素；输入位图数据中的任何“1”将转换为前景像素，而任何“0”将转换为背景位图数据。

现在你已经知道如何处理位图数据（例如 XPM 数据），让我们看看如何处理 XPM 位图数据。我将讨论的第一个例程是 `gdk_pixmap_colormap_create_from_xpm()`：

```c
GdkPixmap *gdk_pixmap_colormap_create_from_xpm(GdkWindow *window, GdkColor *colormap, GdkBitmap **mask, GdkColor *transparent_color, const gchar *filename);
```

参数 `window` 是窗口句柄，大多数情况下应该是位图最终显示的窗口，或者至少是与位图共享视觉类和调色板的窗口。传递 `NULL` 将导致 `gdk_pixmap_colormap_create_from_xpm()` 使用服务器根窗口。参数 `colormap` 是 `Gdkormap` 的实例。你可以通过调用 `gdk_window_get_colormap()` 并传递窗口（类型为 `GdkWindow*`）来获取此调色板。大多数情况下，你只需要将 `colormap` 设置为 `NULL`；这样做，`gdk_pixmap_colormap_create_from_xpm()` 将获取传入的窗口（如果设置为 `NULL` 则使用服务器根窗口）。参数 `mask` 是指向 `GdkBitmap*` 变量的指针。从此函数返回时，如果 `mask` 不是 `NULL`，它将指向一个位点图。在这个位点图中，前景像素由 '1' 表示，图像中的每个背景像素由 '0' 表示。此掩码可以直接传递给下一节描述的 `GtkList` 函数。参数 `transparent_color` 可以很容易地设置为 `NULL`。传递一个 `GdkColor` 指针将导致 `gdk_pixmap_colormap_create_from_xpm()` 使用指定的颜色作为位图的透明色。

最后一个参数 `filename` 是包含 XPM 文件的路径（绝对或相对路径）。`gdk_pixmap_colormap_create_from_xpm()` 函数将代表调用者打开并读取文件以位图数据。

下一个例程 `gdk_pixmap_colormap_create_from_xpm()` 与 `gdk_pixmap_colormap_create_from_xpm()` 相同，但它不接受调色板作为参数：

```c
GdkPixmap *gdk_pixmap_colormap_create_from_xpm(GdkWindow *window, GdkBitmap *mask, GdkColor *transparent_color, const gchar *filename);
```

我将介绍的最后两个函数功能上镜像了 `gdk_pixmap_colormap_create_from_xpm()` 和 `gdk_pixmap_create_from_xpm()`，区别在于它们不接受 XPM 文件的路径。这两个函数都要求你传递 XPM 文件的内容。当你编译时提供 XPM 数据时使用这些例程，这再次通过 `#include` XPM 文件来实现。如果你发现自己需要使用 `gdk_pixmap_create_from_xpm()` 或 `gdk_pixmap_colormap_create_from_xpm()`，打开 XPM 文件并将其读取为数据传递给其中任一个函数可以让它们为你打开并读取文件。例如：

```c
#include "foo.xpm" // 声明了 char 数组 "openfile"
```

```c
GtkPixmap *myPixmap;
GdkWindow *myWindow;
GdkBitmap *mask;
...
myPixmap = gdk_pixmap_colormap_create_from_pixmap_d(myWindow, NULL, openfile);
&mask, NULL, openfile);
```

`gdk_pixmap_colormap_create_from_pm_d()` 函数的参数与 `gdk_pixmap_colormap_create_from_xpm()` 相同，除了第一个参数外，正如我所提到的。

```c
GdkPixmap *
gdk_pixmap_colormap_create_from_xpm_d(GdkWindow *window, GdkColormap
*colormap, GdkBitmap **mask, GdkColor *transparent_color,
gchar **data);
```

`gdk_pixmap_create_from_xpm_d()` 和 `gdk_pixmap_colormap_create_from_xpm_d()` 函数等效，区别在于 `gdk_pixmap_create_from_xpm_d()` 不需要颜色映射（colormap）参数。

```c
GdkPixmap *
gdk_pixmap_create_from_xpm_d(GdkWindow *window, GdkBitmap **mask,
GdkColor *transparent_color, gchar **data);
```

# GtkList Pixmap 函数

现在我们已经描述了用于获取 pixmap 数据和相应掩码的例程，让我们继续讨论 `GtkList` 以及所有使用 pixmap 数据的例程。

第一个函数 `gtk_list_set_pixmap()` 允许你指定一个与 `GtkClist` 实例的单元格一起的 pixmap：

```c
void
gtk_list_set_pixmap(GtkClist *clist, gint row, gint column,
```
