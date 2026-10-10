
| `fill_stipple` | `GdkBitmap*` | 均可 | 绘制填充时使用的点彩；仅限 GDK 模式 |
| `outline_stipple` | `GdkBitmap*` | 均可 | 绘制轮廓时使用的点彩；仅限 GDK 模式 |
| `width_pixels` | `guint` | 仅写 | 轮廓宽度，单位为像素（与缩放无关） |
| `width_units` | `double` | 仅写 | 轮廓宽度，单位为画布单位；像素宽度随缩放因子变化（每单位像素） |

## 线项目

`GnomeCanvas` 代表端端连接的多条线。你也可以用它表示未填充的多边形。`GnomeCanvasPolygon` 用于填充的多边形。

线使用 `GnomeCanvasPoints` 结构体指定，其如下所示：

```
typedef struct {
    int num_points;
    double *coords;
    int ref_count;
} GnomeCanvasPoints;
```

该字段包含一个交替 X 和 Y 坐标的点数组。在用 `gnome_canvas_points_new()` 创建 `GnomeCanvasPoints` 后，直接填充 `coords`；应使用 `gnome_canvas_points_unref()` 销毁结构。

线的两端都可以箭头；箭头形状通过三个参数指定，通常命名为 A、B 和 C。参数 A（通过 `arrowhead_a_argument` 指定）指定箭头底部到箭尖的距离。B 指定箭尖到末点的距离；C 指定末点到线边缘的距离。

### 表 12-2. GnomeCanvasLine 参数

| 名称 | 类型 | 读/写 | 说明 |
|---|---|---|---|
| `points` | `GnomeCanvas-Points*` | 均可 | 线中的点 |
| `fill_color` | `gchar*` | 仅写 | 填充颜色；用于 `gdk_color_parse` 的字符串 |
| `fill_color_gdk` | `GdkColor*` | 均可 | 填充颜色；指定为已分配的 `GdkColor` |
| `fill_color_rgba` | `guint32` | 均可 | 填充颜色；指定为将红、绿、蓝和 alpha 封装进字节 1、2、3、4 的 32 位值；alpha 为 255 不透明 |
| `fill_stipple` | `GdkBitmap*` | 均可 | 绘制线时使用的点彩；仅限 GDK 模式 |
| `width_pixels` | `guint` | 仅写 | 线宽，单位为像素（与缩放无关） |
| `width_units` | `double` | 仅写 | 线宽，单位为画布单位；像素宽度随缩放因子变化（每单位像素） |
| `cap_style` | `GdkCapStyle` | 均可 | 端样式（仅限 GDK 模式） |
| `join_style` | `GdkStyle` | 均可 | 连接样式（仅限 GDK 模式） |
| `line_style` | `GdkLineStyle` | 均可 | 线样式（仅限 GDK 模式） |
| `first_arrowhead` | `boolean` | 均可 | 是否在起点起点放置箭头 |
| `last_arrowhead` | `boolean` | 均可 | 是否在终点放置箭头 |
| `smooth` | `boolean` | 均可 | 是否使用样条平滑 |
| `spline_steps` | `guint` | 均可 | 曲线步数 |
| `arrow_shape_a` | `double` | 均可 | 箭头长度 |
| `arrow_shape_b` | `double` | 均可 | 箭头长度（到末点） |
| `arrow_shape_c` | `double` | 均可 | 箭头宽度 |

## 多边形项目

`GnomeCanvasPolygon` 代表填充的多边形；它可以是填充的或仅轮廓。与 `GnomeCanvasRE` 不同，未填充的多边形不是“空心”；中心的透明部分是画布的一部分。`GnomeCanvasLine` 用于“空心”。

### 表 12-3. GnomeCanvasPolygon 参数

| 名称 | 类型 | 读/写 | 说明 |
|---|---|---|---|
| `points` | `GnomeCanvas-Points*` | 均可 | 多边形点 |
| `fill_color` | `gchar*` | 仅写 | 填充颜色，用于 `gdk_color_parse()` 的字符串，或透明为 NULL |
| `fill_color_gdk` | `GdkColor*` | 均可 | 填充颜色；指定为已分配的 `GdkColor` |
| `fill_color_rgba` | `guint32` | 均可 | 填充颜色；指定为将红、绿、蓝和 alpha 封装进字节 1、2、3、4 的 32 位值；alpha 为 255 不透明，0 为不可见 |
| `outline_color` | `gchar*` | 仅写 | 轮廓颜色；用于 `gdk_color_parse` 的字符串，或透明为 NULL |
| `outline_color_gdk` | `GdkColor*` | 均可 | 轮廓颜色；指定为已分配的 `GdkColor` |
| `outline_color_rgba` | `guint32` | 均可 | 轮廓颜色；指定为将红、绿、蓝和 alpha 封装进字节 1、2、3、4 的 32 位值；alpha 为 255 不透明，0 为不可见 |
| `fill_stipple` | `GdkBitmap*` | 均可 | 绘制填充时使用的点彩；仅限 GDK 模式 |
| `outline_stipple` | `GdkBitmap*` | 均可 | 绘制轮廓时使用的点彩；仅限 GDK 模式 |
| `width_pixels` | `guint` | 仅写 | 轮廓宽度，单位为像素（与缩放无关） |
| `width_units` | `double` | 仅写 | 轮廓宽度，单位为画布单位；像素宽度随缩放因子变化（每单位像素） |

## 图像项目

`GnomeCanvasImage` 在画布上放置图像；你传递一个使用 Imlib 例程加载的 `GdkImlibImage`。如果图像有透明区域，将得到正确处理（它们不会被视为图像的一部分，且不会接收事件）。要在 GDK 画布上使用 `GnomeCanvasImage`，必须在创建画布之前推送 Imlib 视觉和颜色表；参见 *Preparing the GnomeCanvas Widget* 章节。

### 表 12-4. GnomeCanvasImage 参数

| 名称 | 类型 | 读/写 | 说明 |
|---|---|---|---|
| `image` | `GdkImlibImage*` | 均可 | 要显示的 `GdkImlibImage` |
| `x` | `double` | 均可 | 锚点的 X 坐标 |
| `y` | `double` | 均可 | 锚点的 Y 坐标 |
| `anchor` | `GtkAnchorType` | 均可 | 锚点位置 |
| `width` | `double` | 均可 | 画布单位宽度（图像将缩放） |

## 文本项目

`GnomeCanvas` 显示文本字符串。你可以以有序对的形式指定字符串的坐标；这些坐标代表文本锚点的位置。例如，如果 "`anchor`" 参数设置为 `GTK_ANCHOR_NORTH`，则文本项目的坐标将代表项目顶部中心的位置。也就是说，文本将围绕 X 位置居中，并位于 Y 位置下方。可能的锚点值为：

- `GTK_ANCHOR_CENTER`
- `GTK_ANCHOR_NORTH`
- `GTK_ANCHOR_NORTH_WEST`
- `GTK_ANCHOR_NORTH_EAST`
- `GTK_ANCHOR_SOUTH`
- `GTK_ANCHOR_SOUTH_WEST`
- `GTK_ANCHOR_SOUTH_EAST`
- `GTK_ANCHOR_WEST`

| 名称 | 类型 | 读/写 | 说明 |
|---|---|---|---|
| `height` | `double` | 均可 | 画布单位高度（图像将缩放） |

### 表 12-5. GnomeCanvasText 参数

| 名称 | 类型 | 读/写 | 说明 |
|---|---|---|---|
| `text` | `gchar*` | 都 | 要显示的字符串 |
| `x` | `double` | 都 | 锚点的 X 坐标 |
| `y` | `double` | 都 | 锚点的 Y 坐标 |
| `anchor` | `GtkAnchorType` | 都 | 锚点的位置 |
| `font` | `gchar*` | 仅写 | `gdk_font_load()` 的字体名称 |
| `fontset` | `gchar*` | 仅写 | `gdk_fontset_load()` 的字体集名称 |
| `font_gdk` | `GdkFont*` | 都 | 用于渲染文本的字体 |
| `justification` | `GtkJustification` | 都 | 对齐方式（仅限多行） |
