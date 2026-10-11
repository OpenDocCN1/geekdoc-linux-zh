
```

返回值是打印的字符数。

为了兼容性原因，此函数未包含在`a.out`库中。

> **注**
>
> - 此函数（及其原始描述）由 Trek 编写，可通过`trek00@freenet.hut.fi`和/或`trek@mediaservice.net`联系到。

### 字体

`extern unsigned char *gl_font8x8`

`gl_font8x8`包含一个打包像素字体，每个字符 8x8 像素。在使用之前，你可能想用`gl_expandfont()`对其进行扩展。虽然速度较慢，但当`gl_setwritemode()`标志`FONT_COMPRESSED`被设置时，可以使用未扩展的字体。

## 像素图和位图绘制

以下函数用于复制和粘贴屏幕区域。

`void gl_getbox(int x, int y, int w, int h, void *dp)`

将位置`(x, y)`处大小为`(w, h)`的矩形位图从屏幕复制到缓冲区`dp`。像素图采用行优先顺序。目标像素图的大小为`w * h * BYTESPERPIXEL`。

`void gl_copybox(int x1, int y1, int w, int h, int x2, int y2)`

将位于`(x1, y1)`处大小为`(w, h)`的矩形区域复制到`(x2, y2)`。

`void gl_copyboxfromcontext(GraphicsContext *gc, int x1, int y1, int w, int h, int x2, int y2)`

将上下文`gc`中位于`(x1, y1)`处大小为`(w, h)`的矩形区域复制到当前上下文中的位置`(x2, y2)`。这比`copyboxtocontext()`更高效。

`void gl_copyboxtocontext(int x1, int y1, int w, int h, GraphicsContext *gc, int x2, int y2)`

将位于`(x1, y1)`处大小为`(w, h)`的矩形区域复制到上下文`gc`中的位置`(x2, y2)`。如果可能，请改用`copyboxfromcontext()`。

`void gl_putbox(int x, int y, int w, int h, void *dp)`

将内存缓冲区`dp`的内容复制到位置`(x, y)`处大小为`(w, h)`的矩形位图。像素图采用行优先顺序。源像素图内存大小为`w * h * BYTESPERPIXEL`。

`void gl_putboxpart(int x, int y, int w, int h, int bw, int bh, void *dp, int xo, int yo)`

将内存缓冲区`dp`的内容复制到位置`(x, y)`处大小为`(w, h)`的矩形位图。但是，只复制位图的一部分。复制的大小为`(bw, bh)`，从偏移量`(xo, yo)`开始。像素图采用行优先顺序。源像素图内存大小为`w * h * BYTESPERPIXEL`。

`void gl_putboxmask(int x, int y, int w, int h, void *dp)`

将内存缓冲区`dp`的内容复制到位置`(x, y)`处大小为`(w, h)`的矩形位图。此函数的工作原理类似于`gl_putbox`，但不写入颜色为零的像素图像素。如果同一像素图经常使用，应考虑使用更快的`gl_putboxmaskcompiled()`。

像素图采用行优先顺序。源像素图内存大小为`w * h * BYTESPERPIXEL`。

`void gl_putboxmaskcompiled(int x, int y, int w, int h, void *dp)`

将内存缓冲区`dp`的内容复制到位置`(x, y)`处大小为`(w, h)`的矩形位图。此函数的工作原理类似于`gl_putbox()`，但不写入颜色为零的像素图像素。此外，为了更快操作，像素图应先使用`gl_compileboxmask()`进行编译。

`void gl_compileboxmask(int w, int h, void *mdp, void *dmp)`

将位于`mdp`处大小为`(w, h)`的矩形带掩码位图转换为允许更快绘制的压缩格式，并存储在`dmp`中。通常，为编译版本分配`w * h`字节就足够了；上限应为`(w + 2) * h`。仅在 256 色线性模式下支持编译位图。

`int gl_compiledboxmasksize(int w, int h, void *mdp)`

返回`compileboxmask()`将生成的位于`mdp`处大小为`(w, h)`的带掩码位图的编译版本的大小。仅在 256 色线性模式下支持编译位图。

`void gl_scalebox(int w1, int h1, void *mdp, int w2, int h2, void *dmp)`

将位于`mdp`处大小为`(w1, h1)`的位图缩放到大小`(w2, h2)`并存储在`dmp`中，`dmp`必须是足够大的缓冲区。使用当前图形上下文的像素大小。

## 调色板处理

这些函数与调色板管理有关。

`void gl_getpalettedir(int c, int *r, int *g, int *b)`

参见`gl_getpalette()`。

`void gl_getpalettedirs(int s, int n, void *dp)`

参见`gl_getpalette()`。

`void gl_getpalette(void *dp)`

`gl_getpalettedir`从颜色查找表中获取颜色`c`的红、绿、蓝值（范围在 0 到 63 之间），并将它们作为整数存储在由`r`、`g`和`b`指向的内存位置。

`gl_getpalettedirs`获取从`s`开始的`n`个颜色的 RGB 值，它们作为每三个字节一组表存储在`dp`处。

`gl_getpalette`等效于`gl_getpalettedirs(0, 256, dp)`。

`vga_ext_set()`可能会将返回颜色的范围更改为 0 到 255。

`void gl_setpalettecolor(int c, int r, int g, int b)`

参见`gl_setpalette()`。

`void gl_setpalettecolors(int s, int n, void *sp)`

参见`gl_setpalette()`。

`void gl_setpalette(void *sp)`

`gl_setpalettecolor`将颜色查找表中颜色`c`的红、绿、蓝值（范围在 0 到 63 之间）设置为`r`、`g`和`b`。

`gl_setpalettecolors`设置从`s`开始的`n`个颜色的 RGB 值，它们作为每三个字节一组表存储在`sp`处。

`gl_setpalette`等效于`gl_setpalettecolors(0, 256, sp)`。

`vga_ext_set()`可能会将要设置的颜色的范围更改为 0 到 255。

`void gl_setrgbpalette(void)`

设置 256 色 RGB 调色板（位 0 到 2 为蓝色，3 到 5 为绿色，6 到 7 为红色）。在 256 色模式下使用`gl_getpixelrgb()`、`gl_rgbcolor()`或`gl_setpixelrgb()`之前调用此函数。

## 来自 threeDKit 的三角形图元

threeDKit，包括演示，由 Paul Sheer (`psheer@icon.co.za`) 开发。

以下是他的邮寄地址：

Paul Sheer
P.O. Box 890507
Lynhurst, Johannesburg 2106
South Africa

> **警告**
>
> 注意！这些函数不是 `libvga` 或 `libvga` 的直接一部分。但是，其源代码随 `SVGA lib` 版本 `1.4.0` 分发，可以在 `SVGA lib` 发行版中的 `threeDKit` 子目录中找到。

用法类似于 `vga`。你需要在头部包含`<triangle.h>`。实际例程定义在`trio.o`和`triangl.o`文件（或其相应的源代码）中，也在`threeDKit`子目录中，这些必须在编译时链接到你的程序中。

`void gl_triangle(int x0, int y0, int x1, int y1, int x2, int y2, int color, int bf)`

使用`color`中给出的颜色，在三个点 0、1 和 2 之间绘制一个非插值（实心）三角形。`bf`值用于告诉例程如果三角形面向另一侧则不绘制。此外，`bf`告诉三角形需要面向哪个方向才能被绘制，因为你很可能需要两种组合。

重要的是要知道`bf = 0`在点按顺时针排列时禁用绘制，`bf = 1`在点按逆时针排列时禁用绘制，而`bf = -1`可能会总是绘制三角形。

`void gl_swtriage(int x0, int y0, int xd0, int yd0, int x1, int y1, int xd1, int yd1, int x2, int y2, int xd2, int yd2, int c, TD_tridata *tri)`

以下代码

```c
// 注意：原文此处未提供具体代码内容，仅提示“以下代码”，故保留代码块起始符并补充结束符以保持Markdown结构完整
// 如果原文确实没有后续代码，则此处仅为结构占位
```
