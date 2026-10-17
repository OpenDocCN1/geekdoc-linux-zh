
`clist` 是 `GtkClist` 实例，`row` 和 `column` 分别位于 `[0, m-1]` 和 `[0, n-1]` 范围内。`text` 是要在指定单元格显示的 NULL 终止字符串。`gtk_clist_get_text()` 在成功时返回 1，如果 `row` 或 `column` 超出范围，则返回 0。`text` 指向返回文本的指针。通过 `gtk_clist_set_text()` 修改 `text` 时要小心，`gtk_clist_get_text()` 返回的 `text` 是指向返回文本的指针。

## 显示位图

在描述位图之前，我们需要详细介绍对位图（bitmaps）的使用。位图可以显示在 Gtk 窗口。位图可以与 Gtk 控件关联。

第一个参数 `window` 是一个 `GdkWindow` 句柄；通常，这将是位图数据将要显示的窗口。你可以通过类似于下面的代码从 `GtkWidget` 实例获取窗口句柄：

```
GtkWidget *myWindow;
GdkWindow *myWindow;
```

```
myWindow = myWindow->window;
```

该参数是位图数据；宽度（`width`）和高度（`height`）是不言自明的的。对于 `xlogo16`，你必须将 `xlogo16_bits` 作为数据参数，将 `xlogo16_width` 作为宽度参数，并将 `xlogo16_height` 作为高度参数。

返回时，你将获得一个指向 `GdkPixmap` 的指针，用于任何需要 1 位 `GdkPixmap` 数据的地方。

要从 X 位图数据（例如 `xlogo16`）创建一个 `n` 位 `GdkPixmap`，请调用 `gdk_pixmap_create_from_data()`：

```
GdkPixmap *
gdk_pixmap_create_from_data(GdkWindow *window, const gchar *data,
	gint width, gint height, gint depth, GdkColor *fg, GdkColor *bg);
```

参数 `window` 是 `GdkWindow` 的句柄，其视觉颜色映射（visual color-map）和深度（depth）与位图将要显示的窗口相同。理想情况下，你应该传递最终显示你创建的 `GdkPixmap` 的组件所在的窗口。如果你传递 `-1`，将使用 X 服务器的根窗口（root window）。参数 `data` 与之前的（例如 `xlogo16_bits`）相同，`width` 和 `height` 也是如此（分别对应 `xlogo16_width` 和 `xlogo16_height`）。参数 `depth` 是 pixmap 的深度，或者如果你传递 `-1`，则是与你作为第一个参数传递的窗口所关联的视觉（visual）的深度。你应该确保稍后显示该窗口的 pixmap 深度与 X 服务器匹配，否则将产生 X 错误（例如 `BadMatch`）。参数 `fg` 和 `bg` 是在结果生成的 pixmap 中使用的前景像素和背景像素；输入位图数据中的任何 "1" 都将转换为前景像素，而 "0" 将被转换为背景像素数据。

现在你已经知道如何处理 X 位图数据了，让我们来看看如何处理 X pixmap 数据（例如作为 "openfile" 的 XPM 数据）。

我将讨论的第一个程序是 `gdk_pixmap_colormap_from_xpm`：

```
GdkPixmap *
gdk_pixmap_colormap_from_xpm(GdkWindow *window,
GdkColor *colormap, GdkBitmap **mask,
GdkColor *transparent_color, gchar *filename);
```

参数 `window` 是窗口句柄，在大多数情况下，它应该是 pixmap 最终显示的窗口，或者至少是与显示 pixmap 的窗口共享相同视觉类（visual class）和颜色映射（colormap）的窗口。传递 `NULL` 将导致 `gdk_pixmap_colormap_create_from_xpm()` 使用 X 服务器的根窗口。参数 `colormap` 是 `GdkColormap` 实例。你可以通过调用 `gdk_window_get_colormap()` 并传递一个窗口（类型为 `GdkWindow*`）作为参数来获取此颜色映射。在大多数情况下，你只需要将 `colormap` 设置为 `NULL`；通过这样做，`gdk_pixmap_colormap_create_from_xpm()` 将为你传递的窗口获取使用的颜色映射（或使用被设置为 `NULL` 的 X 根窗口）。参数 `mask` 是一个指向 `GdkBitmap` 类型变量的指针。从此函数返回时，`mask` 将指向一个位图。在这个位图中，每个前景像素由 '1' 表示，图像中的每个背景像素由一个 '0' 位表示。此掩码（mask）可以直接传递给下节节描述的 `GtkClList` 函数。参数 `transparent_color` 可以很容易地设置为 `NULL`。传递一个指向 `GdkColor` 的指针将导致 `gdk_pixmap_colormap_create_from_xpm()` 使用指定的颜色作为 pixmap 的透明颜色。

最后一个参数 `filename` 是包含 XPM 数据的文件的路径（绝对路径或相对路径）。函数 `gdk_pixmap_colormap_create_from_xpm()` 将代表调用者打开并读取该文件以获取 pixmap 数据。

下一个程序 `gdk_pixmap_colormap_create_from_xpm()` 与 `gdk_pixmap_colormap_create_from_xpm()` 相同，但它不接受颜色映射作为参数：

```
GdkPixmap *
gdk_pixmap_colormap_create_from_xpm(GdkWindow *window, GdkBitmap *mask,
GdkColor *transparent_color, const gchar *filename);
```
