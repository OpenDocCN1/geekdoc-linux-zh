
# GNOME 开发者官方指南

尽管你拥有所有这些格式选项，但请尽量不要过度使用。使用`粗体斜体`字体表示强调，并使用相对字体大小表示上标或警告（请参见第 3.10 节中对话框的指南）。避免使用绝对字体大小，并且不要随意混合使用字体。`GtkLabel`的其他重要属性还包括：

- `use-underline` (布尔值): 如果为 TRUE，你可以在标签的第一个字母中使用下划线来表示热键。
- `mnemonic` (`GtkWidget`): 当按下上述属性中提到的按键时激活的控件。
- `justify` (`GtkJustification`): 决定文本的对齐方式。可能的值有：
    - `GTK_JUSTIFY_LEFT`
    - `GTK_JUSTIFY_RIGHT`
    - `GTK_JUSTIFY_FILL`（填充空格；仅多多行有效）
- `wrap` (布尔值): 如果为 TRUE，Pango 会对长文本进行换行。
- `selectable` (布尔值): 如果为 TRUE，用户可以使用鼠标选择标签中的文本。
- `cursor-position` (int, 只读): 上述属性所描述的选择位置；文本开头到选择开始位置之间的字符数。
- `selection-bound` (int, 只读): 选择区域的字符数。

当你为应用程序创建标签时，请尽量保持一致且无歧义。以下是一些建议：

- 除非有特殊原因，否则让你的标签左对齐。
- 为用户元素制作标签要具有足够的表现力，以便视力障碍用户知道该元素的作用。屏幕阅读器不应在用户能够采取行动之前读取窗口中的所有内容。特别是对话框，需要特别注意。
- 将大型图标和图像的标签放在图片下方，类似于书籍中的插图说明。
- 将带有小图标的标签直接放在图标右侧。图标作为入口点。
- 如果标签描述的是包含控件的大型区域（例如列表或按钮组），请将标签放在该区域上方。
- 与小图标的情况类似，复选框和单选按钮等小控件的标签位于它们的右侧。
- 当你将标签放在控件左侧是为了让用户像读句子一样阅读（例如小型文本输入框）时，在标签以冒号结尾，以便标签与控件之间有清晰的联系。
- 不要在一个窗口中使用相同的标签文本（或非常相似的文本）。

## 3.3.2 图像与 GdkPixbufs

要表示图像，请创建一个 `GdkImage` (`GTK_TYPE_IMAGE`) 控件并将其 `file` 属性设置为图像的文件名。

`Gdk` 在后台通过 `GdkPixbuf` 类（`GTK_TYPE_PIBUF`）工作，这是 `Gdk` 处理图像数据的底层类。`Gdk` 支持许多不同的图形文件格式，包括 JPEG、GIF、PNG、ICO、PNM、RAS、TGA、TIFF、Windows BMP、XMP 甚至 SVG。加载器是模块化的，`Gdk` 会定期添加新格式的支持。

除了加载自己的文件外，你还可以从内置图像库中选择图像。加载和存储图像的基础 `GtkImage` 属性如下：

- `pixbuf` (`GdkPixbuf`): 图像缓冲区。
- `pixbuf-animation` (`GdkPixbufanimation`): 如果图像是动画，则为图像数据。
- `file` (chararray, 只写): 用于 GDK 加载到图像缓冲区的图像文件。
- `stock` (chararray): 如果你想显示内置图像，这是 GTK+ 内置图像的标识符。
- `icon-size` (tint): 内置图像所需的所需的大小。
- `storage-type` (`GtkImageType`, 只读): 图像在内存中的表示类型。可能的值包括：
    - `GTK_IMAGE_EMPTY`: （还没有）图像数据。
    - `GTK_IMAGE_PIXBUF`: 图像来自文件或 `GdkPixbuf`。
    - `GTK_IMAGE_STOCK`: 图像是内置库的一部分。
    - `GTK_IMAGE_ANIMATION`: 图像包含 GDK Pixbuf 动画。

### GdkPixbuf

如果你需要更改图像以显示，或者想获得更多控制，可以创建自己的 `GdkPixbuf` 对象。

注意，`Gtk` 存储自己的数据。因此，如果你更改了已经在屏幕上的 `GdkPixbuf` 结构，你必须告诉 `GtkImage` 对象此更改，否则屏幕上不会发生任何变化。你将在随后的示例程序的 `render_image()` 函数中看到这一点。

以下是操作 `GdkPixbuf` 类型的最重要函数：

- `GdkPixbuf *gdk_pixbuf_new_from(const gchar *filename, GError **error)`
将 `filename` 中的图像加载到图像缓冲区并返回缓冲区的指针。如果加载图像过程中发生某些问题，此函数返回 NULL 并设置 *error*（可能的错误类为 `GDK_PIXBUF_ERROR` 和 `G_FILE_ERROR`）。

使用 `g_object_unref()` 释放 pixbuf 的内存。

- `int gdk_pixbuf_get_width(GdkPixbuf *pixbuf)`
返回 pixbuf 的宽度。
- `int gdk_pixbuf_get_height(GdkPixbuf *pixbuf)`
返回 pixbuf 的高度。
- `GdkPixbuf *gdk_pixbuf_copy(const GdkPixbuf *pixbuf)`
返回 pixbuf 的拷贝。
- `void gdk_pixbuf_copy_area(const GdkPixbuf *source, int src_x, int src_y, int width, int height, GdkPixbuf *dest, int dest_x, int dest_y)`
将 source 从 (src_x, src_y) 开始的区域复制到 dest 的 (dest_x, dest_y)。
- `GdkPixbuf *gdk_pixbuf_scale_simple(const GdkPixbuf *pixbuf, int width, int height, GdkInterType interpolation)`
返回按宽度和高度缩放的 pixbuf 拷贝。插值选择：
    - `GTK_INTERP_NEAREST`: 近邻法最快，但不适用于缩小图像。
    - `GTK_INTERP_TILE`: 瓦片插值比近邻法好。
    - `GTK_INTERP_BILINEAR`: 如果在 CPU 消耗适的情况下获得良好效果，双线性插值通常是很好的选择。
    - `GTK_INTERP_HYPER`: 超插值提供卓越的结果，但消耗大量的处理器时间。
- `void gdk_pixbuf_scale(const GdkPixbuf *source, GdkPixbuf *dest, int dest_x, int dest_y, int width, int height, double scale_x, double scale_y, GdkInterType interpolation)`
此函数让你控制如何缩放图像。水平方向按 scale_x 垂直方向按 scale_y 缩放，并将其置于 dest (dest_x, dest_y)。
- `void gdk_pixbuf_composite(const GdkPixbuf *source, GdkPixbuf *dest, GdkInterType interpolation, int alpha)`
工作方式类似于前面的，但不是替换目标，而是将新缩放的图像作为透明层添加。当源具有透明像素或你指定的 alpha 值小于 255 时才有意义。
- `boolean gdk_pixbuf_get_alpha(const GdkPixbuf *pixbuf)`
如果 Pixbuf 包含 alpha通道（透明信息），则返回 TRUE。
- `GdkPixbuf *gdk_pixbuf_add_alpha(const GdkPixbuf *pixbuf, guchar r, guchar g, guchar b)`
返回带有通道通道的 pixbuf 拷贝。如果 substitute 为 TRUE，此函数将所有像素匹配 RGB 颜色。此函数将 alpha 通道设置为 255（不透明）。
- `void gdk_pixbuf_saturate_and_pixelate(const GdkPixbuf *source, GdkPixbuf *dest, gfloat saturation, gboolean pixelate)`
更改 source 中的饱和度（色彩对比度），对结果进行像素化（如果 pixelate 为 TRUE），并拷贝到 dest。dest 必须预存在且与 source 维度相同。饱和度值是一个大于等于 0 的浮点数。在 0 时，图像变为灰色；1 对图像没有影响，任何更大的数字都会放大色彩（例如用于 GTK+ 敏感图标效果）。

# GNOME 开发者官方指南

用颜色像素填充 pixbuf。该颜色值是红、绿、蓝和 alpha 通道（透明度）的四字节表示法，例如：`0xceceeff` 表示不透明灰色，`0x00000000` 表示透明黑色，而 `0xffff80` 表示半透明白色。

下面是 `GdkPixbuf` 的简单演示，它使用滑块小部件来执行缩放和饱和度操作。图 3.6 显示了结果。

![](img/ae44ff3edd9313fce71c50baa18b0c66_128_0.png)

该程序的第一部分由你之前已经见过的信号处理函数组成。

```c
```
