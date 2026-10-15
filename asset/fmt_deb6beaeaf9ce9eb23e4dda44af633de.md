
```
#include <gdk/gdk.h>
void gdk_draw_pixmap(GdkDrawable* drawable, GdkGC* gc, GdkDrawable* src, int xsrc, int ysrc, int xdest, int ydest, int width, int height);
```

## RGB 缓冲区

`GdkRGB` 模块允许你将客户端的图像数据缓冲区拷贝到绘制区域。如果你想大量操作图像数据，或者将图像数据拷贝到服务器，这是正确的方法。你不能直接拷贝 `GdkPixmap`，因为它是一个服务器对象。使用 `gdk_draw_point` 将图像数据拷贝到服务器将慢得令人置信，因为每个点都需要一次服务器请求（可能多于一次，因为你为每个点更改 GC）。

在内部，`GdkRGB` 使用一个对象来拷贝需要传输的数据——`GdkRGB` 经过了高度优化，如果客户端和服务器位于同一台机器上，它会使用共享内存。考虑到 X 架构，这是执行此任务最快的方法。它还会为你处理棘手的问题（例如适配 X 服务器上的颜色表和视觉效果）。

你打算拷贝 RGB 缓冲区的绘制区域必须使用 `GdkRGB` 的视觉和颜色表。如果该绘制区域是一个部件的一部分，确保此点的简单方法是在创建部件时推入 `GdkRGB` 视觉和颜色表：

```
GtkWidget* widget;
gtk_widget_push_visual(gdk_get_visual(widget));
```

```
gtk_widget_push_colormap(gdk_rgb_get_cmap());
widget = gdk_whatever_new();
gdk_widget_pop_visual();
gdk_widget_pop_colormap();
```

在当前的 GTK+ 版本中，如果你在绘制期间创建顶层窗口时执行此操作，表现会更好；而不是创建绘制区域本身。然而，在原则上，你可以对任何绘制区域执行此。

`GdkRGB` 理解多种图像数据，包括 24 位和 32 位 RGB 数据、8 位灰度以及指向 RGB 值数组的 8 位索引（一个客户端 `GdkRGBbmap`）。这种缓冲区是最简单的，即 24 位 RGB 数据；它通过 `gdk_draw_rgb_image()` 进行渲染。有单独的函数渲染其他类型，但所有工作方式都相同。

24 位缓冲区是一个字节的一维数组；每三个字节元组组成一个像素（字节 0 是红色，字节 1 是绿色，字节 2 是蓝色）。三个数字描述了数组的大小以及字节在内部的位置：

- 宽度是图像每行的像素数。
- 高度是图像的行数。
- 行间距（`rowstride`）是行与行之间的字节数。也就是说，对于步为 `r` 的缓冲区，第 `n` 行从数组第 `n` 行的索引 `n*r` 处开始。行间距不一定是缓冲区宽度的三倍；如果源指针和行间距对齐到 4 字节边界，`GdkRGB` 速度更快。指定行间距允许你使用填充来实现这一点。

`gdk_draw_rgb_image()` 的 `x`, `y`, `width` 和 `height` 参数定义了要拷贝 RGB 缓冲区的绘制区域。RGB 缓冲区必须有 `width` 列和 `height` 行。RGB 缓冲区的第 0 行第 0 列将被拷贝到绘制区域上的 `(x, y)` 点。

在调色板有限的显示器上对大量颜色进行抖动。抖动仅在 8 位和 16 位显示器上重要；24 位显示器没有调色限制。抖动是一个枚举类型；它有三个可能的值：

- `GDK_RGB_DITHER_NONE` 指定不进行抖动。它适用于颜色较少的线条画，但不适用于照片图像。
- `GDK_RGB_DITHER_NORMAL` 指定在 8 位显示器上进行抖动，但在 16 位显示器上不。这通常是质量与性能的最佳平衡。
- `GDK_RGB_DITHER_MAX` 指定在 8 位和 16 位显示器上始终进行抖动。16 位显示器上的质量提升可能不值得速度损失。

`gdk_draw_rgb_image()` 的 `gc` 参数被简单地传递给 `gdk_draw_rgb_image()`（记得 `GdkRGB` 内部使用 `Gdk`）。有意义的 `gc` 组件（如裁剪掩码、绘制函数和子窗口模式）。

```
#include <gdk/gdkrgb.h>
```

```
void gdk_rgb_init(void);
GdkColormap* gdk_rgb_get_cmap(void);
GdkVisual* gdk_rgb_get_visual(void);
void gdk_draw_rgb_image(GdkDrawable* drawable, GdkGC* gc, int x, int y, int width, int height, GdkRgbmap dither, guchar* buffer, int stride);
```

## 资源管理

你打算拷贝 RGB 缓冲区的绘制区域必须使用 `GdkRGB` 的视觉和颜色表。如果该绘制区域是一个部件的一部分，确保此点的简单方法是在创建部件时推入 `GdkRGB` 视觉和颜色表。

`GdkRGB` 理解多种图像数据，包括 24 位和 32 位 RGB 数据、8 位灰度以及指向 RGB 值数组的 8 位索引（一个客户端 `GdkRGBbmap`）。这种缓冲区是最简单的，即 24 位 RGB 数据；它通过 `gdk_draw_rgb_image()` 进行渲染。有单独的函数渲染其他类型，但所有工作方式都相同。

24 位缓冲区是一个字节的一维数组；每三个字节元组组成一个像素（字节 0 是红色，字节 1 是绿色，字节 2 是蓝色）。三个数字描述了数组的大小以及字节在内部的位置：

- 宽度是图像每行的像素数。
- 高度是图像的行数。
- 行间距（`rowstride`）是行与行之间的字节数。也就是说，对于步为 `r` 的缓冲区，第 `n` 行从数组第 `n` 行的索引 `n*r` 处开始。行间距不一定是缓冲区宽度的三倍；如果源指针和行间距对齐到 4 字节边界，`GdkRGB` 速度更快。指定行间距允许你使用填充来实现这一点。

`gdk_draw_rgb_image()` 的 `x`, `y`, `width` 和 `height` 参数定义了要拷贝 RGB 缓冲区的绘制区域。RGB 缓冲区必须有 `width` 列和 `height` 行。RGB 缓冲区的第 0 行第 0 列将被拷贝到绘制区域上的 `(x, y)` 点。

在调色板有限的显示器上对大量颜色进行抖动。抖动仅在 8 位和 16 位显示器上重要；24 位显示器没有调色限制。抖动是一个枚举类型；它有三个可能的值：

- `GDK_RGB_DITHER_NONE` 指定不进行抖动。它适用于颜色较少的线条画，但不适用于照片图像。
- `GDK_RGB_DITHER_NORMAL` 指定在 8 位显示器上进行抖动，但在 16 位显示器上不。这通常是质量与性能的最佳平衡。
- `GDK_RGB_DITHER_MAX` 指定在 8 位和 16 位显示器上始终进行抖动。16 位显示器上的质量提升可能不值得速度损失。

`gdk_draw_rgb_image()` 的 `gc` 参数被简单地传递给 `gdk_draw_rgb_image()`（记得 `GdkRGB` 内部使用 `Gdk`）。有意义的 `gc` 组件（如裁剪掩码、绘制函数和子窗口模式）。

## GtkStyle 和主题

`GtkStyle` 是 GTK+ 和 GDK 之间的一个抽象层，允许用户自定义部件的渲染方式。样式共享资源以减少开销；它们允许用户自定义 GTK+ 的外观。这里是 `TtkStyle` 结构体：
