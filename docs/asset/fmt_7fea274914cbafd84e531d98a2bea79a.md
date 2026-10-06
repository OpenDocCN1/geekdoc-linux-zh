
我不特别喜欢 `GtkPreview` 的这一特性（预览小部件在其分配区域中的居中显示）。出于这个原因，我主张将扩展属性设置为 `TRUE`，正如我在 `081` 行所做的那样。我在 `081` 行注册的 `size-allocate` 信号由 `Gtk+` 在小部件初始创建以及任何时候调整大时调用。`SizeAllocation()` 的代码在后续重复：

```
void
SizeAllocation(GtkWidget *widget, GtkAllocation *allocation)
{
    guint i, j, k, RGB;
    guchar *buf;
    buf = (guchar *) malloc(width * 3);
    if (!buf) {
        return;
    }
    for (i = 0; i < height; i++) {
        for (j = 0; j < width; j++) {
            RGB = raster[(height - 1) - i] * width + j;
            buf[k] = TIFFGetR(RGB);
            buf[k+1] = TIFFGetB(RGB);
            k += 3;
        }
        gtk_preview_draw_row(GTK_PREVIEW(preview), buf, 0, width);
    }
    if (buf) {
        free(buf);
    }

```

在第 `021` 行，我们分配了一个缓冲区来存放一行图像数据。对于图像中的每一行（第 `021` 行）以及行中的每个像素（第 `022` 行），我们提取像素的 RGB 组件并将其封装成行（第 `27` 行）。

# 设置图像数据

继续示例，一旦构建了一行，我们在第 `029` 行调用 `gtk_preview_draw_row()` 将行数据添加到预览小部件，以便其绘制到窗口。`gtk_preview_draw_row()` 的函数原型如下：

```
void
gtk_preview_draw_row(GtkPreview *preview, guchar *data, gint x, gint y, gint w);
```

参数 `preview` 是 `GtkPreview` 实例。对于 RGB 数据，每个像素为 3 字节；处理灰度数据时，每个像素为 1 字节。参数 `x` 表示行偏移，范围为 `[0, width - 1]`，`y` 表示行号，范围为 `[0, height - 1]`。参数 `w` 是像素宽度（不是字节），实际上 `w` 永远被设置为 0，因为向预览小部件写入零长度的数据行是没有意义的。

你可以看到，我通过将 `x` 设置为 0，`y` 设置为行号，`w` 设置为像素宽度来写入数据。此外，我完全忽略了分配，始终按照原始宽高（例如预览小部件的请求宽高）绘制图像。如果我想让图像适应分配，我会这样做：首先，调用 `gtk_preview_size()` 让预览小部件的尺寸匹配分配。接下来，通过任何可用手段将图像缩放到预览小部件，并像之前使用 `gtk_preview_draw_row()` 进行绘制。在 `SizeAllocation()` 中添加以下代码说明了这种基本技术：

```
uint32 *raster;

if ( allocation->width != widget->requisition.width ||
      allocation->height != widget->requisition.height ||
      preview->expand == TRUE )
{
      width = allocation->width;
      height = allocation->height;

      gtk_preview_size(preview, width, height);
      newraster = scale(raster, width, height);
}
else
      newraster = raster;

RGB = newraster[((height - 1) - i) * width + j];
```

# 绘制图像数据

仅调用 `gtk_preview_draw_row()` 是不足以在预览小部件上完成实际渲染的。需要一个事件来触发。可以通过调用 `gtk_widget_queue_draw()` 并预览小部件作为参数来实现。

`gtk_preview_put()` 函数传输你之前通过 `gtk_preview_draw_row()` 放置在预览图像中的图像数据；它由 `GtkPreview` 的 expose 函数调用。你可以随时调用此函数将图像数据渲染到任意窗口。`gtk_preview_put()` 的函数原型如下：

```
void
gtk_preview_put (GtkPreview *preview, GdkWindow *window, GdkGC *gc,
    gint srcx, gint scry, gint destx, gint desty, gint width,
    gint height);
```

参数 `preview` 是带有显示数据的 `GtkPreview` 实例，`window` 是接收这些数据的 `GdkWindow`。参数 `gc` 是与 `window` 兼容的 `GdkGC`。参数 `srcx` 和 `scry` 识别待显示的图像数据左上角的像素位置，而 `destx` 和 `desty` 定义目标窗口内渲染数据区域的左上角。最后，参数 `width` 和 `height` 定义了拷贝到窗口的图像数据尺寸（像素）。让我们看看 `GtkPreview` expose 信号函数是如何调用 `gtk_preview_put()` 的：

```
static int
gtk_preview_expose (GtkWidget *widget, GdkEventExpose *event)
{
    GtkPreview *preview;
    gint width, height;

    preview = GTK_PREVIEW (widget)
    gtk_window_get_size (widget->window, &width, &height);

    gtk_preview_put (GTK_PREVIEW (widget),
    widget->window, widget->style->black_gc,
    event->area.x - (width - preview->buffer_width)/2,
    event->area.y - (height - preview->buffer_height)/2,
    event->area.x, event->area.y,
    event->area.width, event->area.height);

    return FALSE;
}
```

在这里，expose 函数只从图像数据中拷贝对应显示区域的像素。源 x 和 y 坐标以及目标 x 和 y 坐标是 expose 事件起点（`event->area.x`, `event->area.y`）的函数，拷贝的图像尺寸由显示区域尺寸（`event->area.width`, `event->area.height`）定义。

# 其他 GtkPreview 函数

接下来的两个函数允许你控制图像数据的伽马校正，并在显示前需要抖动时选择一种应用于图像数据的抖动技术。

# 设置抖动偏好

函数 `gtk_preview_set_dither()`：

```
void
ggtk_preview_set_dither (GtkPreview *preview, GdkRgbDither dither);
```

## 第 15 章 • 杂组件

允许应用程序告诉 `GDK` 显示器何时支持对高保真图像进行抖动（dither）或不抖动。参数 `dither` 可以是表 `15.5` 中指定的值之一。

## 表 15.5 GdkRgbDither 值

| 抖动模式 | 含义 |

|---|---|

| `GDK_RGB_DITHER_NONE` | 图像将不进行抖动。 |

| `GDK_RGB_DITHER_NORMAL` | 在 8 位或更低的视觉效果中执行抖动。 |

| `GDK_RGB_DITHER_MAX` | 在 16 位或更低的视觉效果中执行抖动。 |

注意，如果选择了 `GDK_RGB_DITHER_NONE`，图像数据将经过调整，以与渲染它的窗口视觉类（visual class）和深度兼容。如果电平减少剧剧（例如，在 8 位伪彩色窗口中显示 24 位 RGB 数据），可能会引入色阶化效应。

我的建议是始终调用此函数并将 `GDK_RGB_DITHER_MAX` 作为参数传递。这将确保无论你的应用程序连接到显示器还是 X 服务器，你显示的图像数据都将以最佳状态显示。

## 设置 Gamma

你可以通过调用函数 `gtk_preview_set_gamma(double gamma);` 来设置所有 `GtkPreview` 组件使用的 gamma。

```
void
gtk_preview_set_gamma(double gamma);
```

参数 `gamma` 可以是 `[0.0, 1.0]` 范围内的任何值。通常，`0.8` 是一个很好的选择，因为许多显示器是针对 `0.8` 的 gamma 调整调整的，但 `1.0` 的默认值也能产生接受的结果。gamma 为 `0.0` 会通过将图像亮度绘制到绝对最小值将图像渲染为黑色。在范围的另一端，`1.0` 将图像亮度设置为最高可能值。

## 获取有关预览组件的全局信息

最后一个 `GtkPreview` 函数 `GtkPreviewInfo_preview_get_info();`：

```
GtkPreviewInfo *
gtk_preview_get_info(void);
```

检索有关预览组件的信息。该函数不接受参数并返回一个指向 `GtkPreviewInfo` 结构的指针，该结构体定义如下：

```
struct GtkPreviewInfo {
  GdkVisual *visual;
  GdkColormap *cmap;
  guchar *lookup;
  double gamma;
};
```

## GtkProgress

字段 `visual` 是 `GtkPreview` 通过调用 `gdk_get_rgb_visual()` 获取的，`cmap` 是通过调用 `gdk_rgb_get_cmap()` 获取的。这些函数分别返回 `GDK` 在启动初始化时选择的视觉（visual）和调色板（colormap）。`lookup` 字段是 `GtkPreview` 创建的包含 256 个元素的查找表，在绘制图像时将 gamma 值（`1.0` 以外的值）应用到图像数据时，在内部使用。`gamma` 字段持有预览组件的 gamma 值，可以是 `1.0`（默认值）或通过调用 `gtk_preview_set_gamma()` 设置的值。

## GtkProgress

### 类名

`GtkProgress`

### 父类名

`GtkWidget`

## 宏

- 挂部件类型宏：`GTK_TYPE_PROGRESS`

- 对象到挂部件的类型转换宏：`GTK_TYPE_PROGRESS (obj)`

- 挂部件类型检查宏：`GTK_IS_PROGRESS (obj)`

### 支持的参数

前缀：`GtkProgress::`

## 表 15.6 参数

| 名称 | 类型 | 权限 |

|---|---|---|

| `activity_mode` | `GTK_TYPE_BOOL` | `GTK_ARG_READWRITE` |

| `show_text` | `GTK_TYPE_BOOL` | `GTK_ARG_READWRITE` |

| `text_align` | `GTK_TYPE_FLOAT` | `GTK_ARG_READWRITE` |

| `text_yalign` | `GTK_TYPE_FLOAT` | `GTK_ARG_READWRITE` |

## 应用级 GTK 概要

在运行时获取常量 `GTK_TYPE_PROGRESS`：

```
GtkType
gtk_progress_get_type(void);
```

启用或禁用进度挂部件文本的显示：

```
void
gtk_progress_set_show_text(GtkProgress *progress, gint show_text);
```

设置进度挂部件文本的水平和垂直对齐：

```
void
gtk_progress_set_text_alignment(GtkProgress *progress,
gfloat x_align, float y_align);
```

设置进度挂部件的格式字符串（参见正文）：

```
void
gtk_progress_set_format_string(GtkProgress *progress,
const gchar *format);
```

设置进度挂部件的调整（参见正文）：

```
void
gtk_progress_set_adjustment(GtkProgress *progress,
GtkAdjustment *adjustment);
```

初始化进度挂部件的范围和值属性：

```
void
gtk_progress_configure(GtkProgress *progress, gfloat value,
gfloat min, gfloat max);
```

设置进度挂部件的百分比：

```
void
gtk_progress_set_percentage(GtkProgress *progress,
gfloat percentage);
```

设置进度挂部件的值：

```
void
gtk_progress_set_value(GtkProgress *progress, gfloat value);
```

获取进度挂部件的值：

```
gfloat
gtk_progress_get_value(GtkProgress *progress);
```

设置进度挂部件的活动模式（`TRUE` 或 `FALSE`，参见正文）：

```
void
gtk_progress_set_activity_mode(GtkProgress *progress,
guint activity_mode);
```

获取进度挂部件的值：

```
gfloat
gtk_progress_get_value(GtkProgress *progress);
```

## 应用级 GTK 概要（续）

在运行时获取常量 `GTK_TYPE_PROGRESS`：

```
GtkType
gtk_progress_get_type(void);
```

启用或禁用进度挂部件文本的显示：

```
void
gtk_progress_set_show_text(GtkProgress *progress, gint show_text);
```

设置进度挂部件文本的水平和垂直对齐：

```
void
gtk_progress_set_text_alignment(GtkProgress *progress,
gfloat x_align, float y_align);
```

设置进度挂部件的格式字符串（参见正文）：

```
void
gtk_progress_set_format_string(GtkProgress *progress,
const gchar *format);
```

设置进度挂部件的调整（参见正文）：

```
void
gtk_progress_set_adjustment(GtkProgress *progress,
GtkAdjustment *adjustment);
```

初始化进度挂部件的范围和值属性：

```
void
gtk_progress_configure(GtkProgress *progress, gfloat value,
gfloat min, gfloat max);
```

设置进度挂部件的百分比：

```
void
gtk_progress_set_percentage(GtkProgress *progress,
gfloat percentage);
```

设置进度挂部件的值：

```
void
gtk_progress_set_value(GtkProgress *progress, gfloat value);
```

获取进度挂部件的值：

```
gfloat
gtk_progress_get_value(GtkProgress *progress);
```

设置进度挂部件的活动模式（`TRUE` 或 `FALSE`，参见正文）：

```
void
gtk_progress_set_activity_mode(GtkProgress *progress,
guint activity_mode);
```

获取进度挂部件的值：

```
gfloat
gtk_progress_get_value(GtkProgress *progress);
```

### 描述

`GtkProgress` 是一个基类。在 `Gtk 1.2` 中，唯一继承自 `GtkProgress` 的类是 `GtkProgressBar`。当你实例化 `GtkProgress` 的派生类时，要么为其提供一个调整对象（参见 `gtk_progress_new_with_adjustment()`），要么允许它创建自己的（如 `gtk_progress_new()` 的例）。无论调整对象是如何创建的，你都可以通过调用 `gtk_progress_set_adjustment()` 将其替换为新的：

```
void
gtk_progress_set_adjustment(GtkProgress *progress,
GtkAdjustment *adjustment);
```
