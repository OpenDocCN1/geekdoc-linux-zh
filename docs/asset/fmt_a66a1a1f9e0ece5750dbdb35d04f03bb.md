
GdkRGB 模块（见 RGB Buffers 部分）是处理颜色的另一种方法；除功能外，它可以从 RGB 值设置图形上下文的前景和背景颜色。相关函数是 `gdk_rgb_gc_set_foreground()` 和 `gdk_rgb_gc_set_background()`。`GdkRGB` 有一个预分配的调色板用于选择最佳匹配颜色，这意味着你的应用程序可以与其他使用 `GdkRGB` 的应用程序共享有限的调色板资源（但你也可以直接使用 `GdkRGB` 的调色板，见“RGB Buffers” 章节）。

## 可绘制对象与位图 (Pixmaps)

位图（pixmap）是你可以在其中绘制图形的离屏缓冲区。在位图中绘制后，你可以将其绘制到窗口中，使其出现在屏幕上（当窗口可见时）。当然，你也可以直接绘制到窗口。使用位图作为缓冲区允许你快速更新屏幕，而无需重复一系列绘制操作。位图还用于存储从磁盘加载的图像，如图标和图像。然后你可以将位图拷贝到窗口。在 GDK 中，该类型为 `GdkPixmap`。每个像素用一个位表示的位图是位图；GDK 类型为 `GdkBitmap`。“位图”并不是一个独立的类型；它只是深度为 1 的位map。像窗口一样，位图是服务器端的。

在 X 术语中，可绘制对象（drawable）是任何可以在上面绘制图形的物体。GDK 有对应的类型，称为 `GdkDrawable`。可绘制对象包括窗口、位图和位图。以下是类型在 GDK 中的定义：

```c
typedef struct _GdkWindow GdkWindow;
typedef struct _GdkWindow GdkBitmap;
typedef struct _GdkWindow GdkDrawable;
```

在客户端侧，位图和位图只是 `Gdk_WINDOW` 类型。`GdkDrawable` 用于函数声明，无论是窗口还是位图都是接受的参数。绘制图形的函数移动或设置窗口提示只接受窗口。`GDK_INPUT_ONLY` 窗口是一种特殊情况；它们不是可绘制的，你无法在上面绘制。

“窗口特征”和可绘制性的四种逻辑组合实际上：

| 可绘制 | 不可绘制 |
| --- | --- |
| 有特征窗口 | 仅输入窗口 |
| 无特征位图/位图 |  |

等等，在颜色有限的显示器上可能会失败。可写调色板条目也可能失败（因为在这种情况下最佳匹配没有意义……）。写调色板条目是可以随时更改的；某些显示器支持在屏幕上无需重绘图形即可实现。硬件将像素存储为指向调色板表格的索引，因此表格改变了像素的显示方式。可写调色板条目的缺点有很多。最显著的是：并非所有视觉效果都支持调色板条目的匹配，并且会被其他应用程序（只读条目可以共享，因为其他应用程序颜色将保持不变）。因此，避免分配可写颜色是一个好主意。在现代硬件上，它们带来的麻烦远大于收益；仅仅通过重绘图形所获得的速度将是察觉的。

当你完成对颜色的使用后，可以使用 `gdk_colormap_free_color` 将其从调色板中移除。这对于颜色和灰度视觉效果非常重要，因为这些颜色稀缺，且调色板可以在客户端之间共享。CDK 会为每种视觉类型执行正确的操作，因此请始终调用此函数。

获取 RGB 值的方便方法是使用 `gdk_color_parse()` 函数。它接收一个 X 规范并填充 `GdkColor` 的红、绿、蓝字段。X 规范有许多形式；一种可能性是 RGB 字符串：

```c
RGB:FF/FF/FF
```

这指定了颜色（红、绿、蓝均为全强度）。`RGB:` 指定了一个“颜色空间”，并决定了其后面数字的含义。它还能理解其他几种颜色空间。如果颜色规范不是以已识别的颜色空间开头，X 会假设它是一个颜色名称并在名称数据库中查找。你可以编写这样的代码：

```c
GdkColor color;

if (gdk_color_parse("orange", &color))
{
    if (gdk_colormap_alloc_color(colormap, &color, FALSE, TRUE))
        /* 我们得到橙色了！ */
}
```

# 第 10 章 GDK 基础

如你所见，如果 `gdk_color_parse()` 解析出你传递的字符串，它将返回 TRUE。无法确切知道颜色数据库中会有什么，请始终检查此返回值。

```c
#include <gdk/gdk.h>

gboolean gdk_colormap_alloc_color(GdkColormap* colormap, GdkColor* color, gboolean writeable, gboolean best_match);
void gdk_colormap_free_colors(GdkColormap* colormap, GdkColor* colors, int ncolors);
int gdk_color_parse(gchar* spec, GdkColor* color);
```

图 10-3 调色板

## 获取调色板

如果你正在编写 GtkWidget 子类，获取调色板的正确方法是使用 `gtk_widget_get_colormap()`（见第 11 章）。否则，系统（默认）调色板通常是你需要的；调用 `gdk_colormap_get_system()`，它不接受参数并返回默认颜色。

`GdkRGB` 模块（见 RGB Buffers 部分）是处理颜色的另一种方法；除功能外，它可以从 RGB 值设置图形上下文的前景和背景颜色。相关函数是 `gdk_rgb_gc_set_foreground()` 和 `gdk_rgb_gc_set_background()`。`GdkRGB` 有一个预分配的调色板用于选择最佳匹配颜色，这意味着你的应用程序可以与其他使用 `GdkRGB` 的应用程序共享有限的调色板资源（但你也可以直接使用 `GdkRGB` 的调色板，见“RGB Buffers” 章节）。

## 可绘制对象与位图 (Pixmaps)

位图（pixmap）是你可以在其中绘制图形的离屏缓冲区。在位图中绘制后，你可以将其绘制到窗口中，使其出现在屏幕上（当窗口可见时）。当然，你也可以直接绘制到窗口。使用位图作为缓冲区允许你快速更新屏幕，而无需重复一系列绘制操作。位图还用于存储从磁盘加载的图像，如图标和图像。然后你可以将位图拷贝到窗口。在 GDK 中，该类型为 `GdkPixmap`。每个像素用一个位表示的位图是位图；GDK 类型为 `GdkBitmap`。“位图”并不是一个独立的类型；它只是深度为 1 的位map。像窗口一样，位图是服务器端的。

在 X 术语中，可绘制对象（drawable）是任何可以在上面绘制图形的物体。GDK 有对应的类型，称为 `GdkDrawable`。可绘制对象包括窗口、位图和位图。以下是类型在 GDK 中的定义：

```c
typedef struct _GdkWindow GdkWindow;
typedef struct _GdkWindow GdkBitmap;
typedef struct _GdkWindow GdkDrawable;
```

在客户端侧，位图和位图只是 `Gdk_WINDOW` 类型。`GdkDrawable` 用于函数声明，无论是窗口还是位图都是接受的参数。绘制图形的函数移动或设置窗口提示只接受窗口。`GDK_INPUT_ONLY` 窗口是一种特殊情况；它们不是可绘制的，你无法在上面绘制。

“窗口特征”和可绘制性的四种逻辑组合实际上：

| 可绘制 | 不可绘制 |
| --- | --- |
| 有特征窗口 | 仅输入窗口 |
| 无特征位图/位图 |  |

## 事件

事件发送到你的应用程序，以指示 `GdkWindow` 的变化或你可能感兴趣的操作。所有事件都与 `GdkWindow` 相关。它们也与 `GtkWidget` 相关；GTK+ 主循环将事件从 GDK 传递给 GTK+ 树。

## 事件类型

有很多种事件；`GdkEvent` 联合可以表示任意一种。特殊的事件类型 `GdkEventAny` 包含了所有事件共有的字段；任何事件都可以转换为 `GdkEventAny`。`GdkEventAny` 的第一个字段是类型标记 `GdkEventType`；`GdkEventType` 也包含在 `GdkEvent` 联合中。困惑了吗？看下面的代码。这里是 `GdkEventAny`：

```c
structGdkEventAny {
  GdkEventType type;
  GdkWindow *window;
  gint send_event;
}
```

and `GdkEvent`:
