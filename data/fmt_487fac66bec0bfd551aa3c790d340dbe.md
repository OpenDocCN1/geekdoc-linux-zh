
```
void gdk_drag_status( GdkDragContext *context, GdkDragAction action,
gint32 time )
```

| 参数 | 描述 |
| --- | --- |
| `context` | 通过 `drag_motion` 信号接收到的 `GdkDragContext` 结构指针。 |
| `action` | 目标控件将接受的动作。如果目标不是有效的投放目标，则将其设置为 `NULL`。 |
| `time` | `drag_motion` 信号提供的时间。 |

## `gdk_draw_arc()`

```
void gdk_draw_arc( GdkDrawable *drawable, GdkGC *gc, gint filled,
gint x, gint y, gint width, gint height,
gint angle1, gint angle2 )
```

| 参数 | 描述 |
| --- | --- |
| `drawable` | 在何处绘制 |
| `gc` | 绘制线条时使用的图形上下文 |
| `filled` | 是否填充圆形（`TRUE` 或 `FALSE`） |
| `x`, `y`, `width`, `height` | 弧形边界矩形的大小和位置 |
| `angle1`, `angle2` | 以 1/64 度为单位的起始角度和大小。 |

## `gdk_draw_line()`

```
void gdk_draw_line( GdkDrawable *drawable, GdkGC *gc, gint x1, gint y1,
gint x2, gint y2 )
```

![](img/7fa9959a9d28ad339fa75e44952feeb9_738_0.png)

## 附录 D

| 参数 | 描述 |
| --- | --- |
| `drawable` | 在何处绘制 |
| `gc` | 绘制线条时使用的图形上下文 |
| `x1`, `y1` | 线条起点 |
| `x2`, `y2` | 线条终点 |

## `gdk_draw_lines()`

```
void gdk_draw_lines(GdkDrawable *drawable, GdkGC *gc, GdkPoint *points,
int npoints )
```

| 参数 | 描述 |
| --- | --- |
| `drawable` | 在何处绘制点 |
| `gc` | 绘制点时使用的图形上下文 |
| `points` | 要绘制的 `GdkPoints` 数组 |
| `npoints` | 要绘制的点数 |

## `gdk_draw_pixmap()`

```
void gdk_draw_pixmap(GdkDrawable *drawable, GdkGC *gc, GdkDrawable *src,
int xsrc, int ysrc, int xdest, int ydest,
int width, int height )
```

| 参数 | 描述 |
| --- | --- |
| `drawable` | 你正在拷贝到的目标 `drawable` |
| `gc` | 复制时使用的图形上下文 |
| `src` | 你正在拷贝的源 `drawable` |
| `xsrc`, `ysrc` | `src` 中待拷贝部分的左上角 （如果拷贝整个图片，则为 0, 0) |
| `xdest`, `ydest` | `drawable` 中放置拷贝位置的左上角 |
| `width`, `height` | 要拷贝的 `src` `pixmap` 部分的像素大小 |

## `gdk_draw_point()`

```
void gdk_draw_point(GdkDrawable *drawable, GdkGC *gc, int x, int y )
```

| 参数 | 描述 |
| --- | --- |
| `drawable` | 在何处绘制点 |
| `gc` | 绘制点时使用的图形上下文 |
| `x`, `y` | 要绘制的点。（大小为单个像素。） |

## 函数原型

### `gdk_draw_points()`

```
void gdk_draw_points( GdkDrawable *drawable, GdkGC *gc,
GdkPoint *points, gint npoints )
```

| 参数 | 描述 |
| --- | --- |
| `drawable` | 在何处绘制点 |
| `gc` | 绘制点时使用的图形上下文 |
| `points` | 要绘制的点数组 |
| `npoints` | 要绘制的点数 |

### `gdk_draw_rectangle()`

```
void gdk_draw_rectangle( GdkDrawable *drawable, GdkGC *gc, gint filled,
gint x, gint y, gint width, gint height )
```

| 参数 | 描述 |
| --- | --- |
| `drawable` | 在何处绘制矩形 |
| `gc` | 绘制时使用的图形上下文 |
| `filled` | 矩形是填充还是描边（`TRUE` 或 `FALSE`） |
| `x`, `y` | 矩形的左上角位置 |
| `width`, `height` | 矩形的大小 |

### `gdk_draw_segments()`

```
void gdk_draw_segments( GdkDrawable *drawable, GdkGC *gc,
GdkSegment *segs, gint nsegs )
```

| 参数 | 描述 |
| --- | --- |
| `drawable` | 在何处绘制段 |
| `gc` | 绘制时使用的图形上下文 |
| `segs` | 要绘制的 `GdkSegments` 数组 |
| `nsegs` | 要绘制的段数 |

### `gdk_draw_string()`

```
void gdk_draw_string( GdkDrawable *drawable, GdkFont *font, GdkGC *gc,
gint x, gint y, gchar *string )
```

| 参数 | 描述 |
| --- | --- |
| `drawable` | 要绘制的窗口或 `pixmap` |
| `font` | 使用的字体 |

![](img/7fa9959a9d28ad339fa75e44952feeb9_740_0.png)

## 附录 D

### `gdk_draw_text()`

```
void gdk_draw_text( GdkDrawable *drawable, GdkFont *font, GdkGC *gc,
int x, int y, gchar *text, int text_length )
```

| 参数 | 描述 |
| --- | --- |
| `drawable` | 绘制字符窗口或 `pixmap` |
| `font` | 使用的字体 |
| `gc` | 使用的图形上下文 |
| `x`, `y` | 字符基线的起始位置，单位为像素 |
| `text` | 要绘制的字符 |
| `text_length` | 绘制的字符数 |

### `gdk_font_load()`

```
GdkFont* gdk_font_load( const gchar *font_name )
```

| 参数 | 描述 |
| --- | --- |
| `font_name` | 要加载的字体名称 |

### `gdk_free_compound_text()`

```
void gdk_free_compound_text( guchar *ctext )
```

| 参数 | 描述 |
| --- | --- |
| `ctext` | 需要释放的复合文本 |

### `gdk_free_text_list()`

```
void gdk_free_text_list( gchar **list )
```

| 参数 | 描述 |
| --- | --- |
| `list` | 需要释放的字符串数组 |

### `gdk_pixmap_colormap_create_xpm()`

```
GdkPixmap * gdk_pixmap_colormap_create_xpm( GdkWindow *window,
GdkColormap *colormap,
GdkBitmap **mask,
GdkColor *transparent_color,
const gchar *filename )
```

返回新 `GdkPixmap` 的指针。

| 参数 | 描述 |
| --- | --- |
| `window` | 用于获取信息的窗口。如果指定了 `colormap`，可以为 `NULL`。 |
| `colormap` | 新 `pixmap` 使用的调色板。如果为 `NULL`，则从窗口获取信息。 |
| `mask` | 存储由此函数创建的透明掩罩（用于形状窗口或光标）。如果忽略透明度，则为 `NULL`。 |
