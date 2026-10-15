
矩形或椭圆的轮廓颜色以相同的方式传递，使用三种方法中的任何一种，而轮廓宽度通过`width_pixels`或`width_units`指定。

让我们看看半透明椭圆实际上看起来什么样。对`canvas.c`进行以下修改，并将其保存为`canvas2.c`：

```c
/*
 * canvas2.c
 *
 * 一个使用 GNOME
 * 画布绘制椭圆和矩形的简单程序
 */
```

```c
#include <gnome.h>

void CloseTheApp( GtkWidget * window, gpointer data )
{
  gtk_main_quit();
}

void CreateCanvasItem( GtkWidget * canvas )
{
  GnomeCanvasGroup * group;
  GnomeCanvasItem * rectangle;
  GnomeCanvasItem * ellipse;

  /* 获取画布根组 */
  group = gnome_canvas_root ( GNOME_CANVAS ( canvas ) );

  /* 绘制矩形 */
  rectangle = gnome_canvas_item_new ( group,
      "x1", 75.0, "x2", 250.0, "y1",
      50.0, "y2", 275.0, "fill_color",
      "red", "outline_color", "blue",
      "width_units", 2.5, NULL );

  /* 绘制半透明椭圆 */
  ellipse = gnome_canvas_item_new( group,
      gnome_canvas_ellipse_get_type(),
      "x1", 30.0, "y1", 30.0, "x2", 175.0,
      "y2", 200.0, "fill_color_rgba",
      0x5f9ea90, "outline_color", "black",
      "width_pixels", 5, NULL );

}
```

```c
gint main ( gint argc, gchar * argv[] )
{
    GtkWidget * window;
    GtkWidget * canvas;

    gnome_init("canvas-sample", "0.0", argc, argv);

    window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
    gtk_window_set_default_size ( GTK_WINDOW ( window ), 320, 320 );
    gtk_window_set_title ( GTK_WINDOW ( window ), "Canvas Sample" );

    gtk_signal_connect ( GTK_OBJECT ( window ), "destroy",
    GTK_SIGNAL_FUNC ( CloseTheApp ), NULL );

    /* 设置视觉效果和颜色色表 */
    gtk_widget_push_visual ( gdk_rgb_get_visual ( );
    gtk_widget_push_colormap ( gdk_rgb_get_cmap ( ) );

    /* 创建抗锯齿模式下的画布 */
    canvas = gnome_canvas_new_aa ( );

    /* 现在弹出视觉效果和颜色色表 */
    gtk_widget_pop_visual ( );
    gtk_widget_pop_colormap ( );

    /* 设置抗锯齿模式设置画布 */
    gnome_canvas_set_aa ( GNOME_CANVAS ( canvas ) );

    /* 添加画布到窗口 */
    gtk_container_add ( GTK_CONTAINER ( window ), canvas );

    /* 显示所有组件 */
    gtk_widget_show_all ( window );

    gtk_main();
    return 0;
}
```

# 第 15 章

最后，`line_style`影响线条的绘制方式。

| 线样式 | 描述 |
| --- | --- |
| `GDPR_LINE_SOLID` | 绘制实线。 |
| `GDPR_LINE_ON_OFF_DASH` | 绘制偶数段；不绘制奇数段。 |
| `GDPR_LINE_DOUBLE_DASH` | 正常绘制偶数段。如果填充样式为`GDPR_SOLID`，则奇数段使用背景色绘制（覆盖）；如果填充样式为`GDPR_STIPPLED`，则使用被点纹遮罩的背景色绘制。 |

让我们在`GnomeCanvasLine`的示例中将其付诸实践。通过修改`canvas2.c`中的`CreateCanvasItem`来创建`canvas3.c`，使其读取如下：

```c
void CreateCanvasItem ( GtkWidget * canvas ) {
  GnomeCanvasGroup * group;
  GnomeCanvasItem * line;
  GnomeCanvasPoints * points;

  /* 获取画布根组 */
  group = gnome_canvas_root ( GNOME_CANVAS(canvas));

  /* 初始化点 */
  points = gnome_canvas_points_new (6);

  points->coords[0] = 40.0;
  points->coords[1] = 250.0;

  points->coords[2] = 80.0;
  points->coords[3] = 50.0;

  points->coords[4] = 120.0;
  points->coords[5] = 250.0;

  points->coords[6] = 160.0;
  points->coords[7] = 50.0;

  points->coords[8] = 200.0;
  points->coords[9] = 250.0;

  points->coords[10] = 240.0;
  points->coords[11] = 50.0;

  /* 绘制线条项 * */
  line = gnome_canvas_item_new ( group, gnome_canvas_line_get_type(),
      "points", "points", "fill_color", "blue",
      "width_units", 6.0, "join_style",
      GDK_CAP_BUT, "last_arrowhead",
      "arrow_shape_a", 30.0, "arrow_shape_b",
      "arrow_shape_c", 20.0, NULL );

  /* 释放点结构 */
  gnome_canvas_points_unref ( points );
}
```

该线条在最后一个点处带有一个箭头。尝试上述的一些不同参数，请记住对于某些参数，你需要在 GDK 模式下使用画布。

# GnomeCanvasPolygon

`GnomeCanvasPolygon`用于绘制一个填充的多边形，使用`GnomeCanvasPoints`来定义角点，其方式与`GnomeCanvasLines`非常相似，但`GnomeCanvasPolygon`会将第一个点和最后一个点连接起来，以完成一个闭合的多边形。

| 名称 | 类型 | 描述 |
|---|---|---|
| `points` | `GnomeCanvasPoints` | 连接以形成线条的点 |
| `fill_color` | `gchar` | 以字符串形式指定的填充颜色，或`NULL`为透明 |
| `fill_color_gdk` | `GdkColor` | 以`GdkColor`指定的填充颜色 |
| `fill_color_rgba` | `guint32` | 以4字节红、绿、alpha值指定的填充颜色 |
| `outline_color` | `gchar` | 以字符串形式指定的轮廓颜色，或`NULL`为透明 |
| `outline_color_gdk` | `GdkColor` | 以`GdkColor`指定的轮廓颜色 |
| `outline_color_rgba` | `Guint32` | 以4字节红、绿、蓝、alpha值指定的轮廓颜色 |
| `fill_stipple` | `GdkBitmap` | 用于绘制多边形的填充点纹。仅 GDK 模式 |
| `outline_stipple` | `GdkBitmap` | 用于绘制多边形的轮廓点纹。仅 GDK 模式 |
| `width_pixels` | `guint` | 以像素指定的轮廓宽度，与缩放无关 |
| `width_units` | `double` | 以画布单位指定的轮廓宽度 |

# GnomeCanvasText

你通常想在画布上放置文本，这是通过使用`GnomeCanvasText`画布项实现的。参数列表与其他画布项非常相似，但增加了对齐方式和字体等内容。

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `text` | `gchar` | 要显示的文本 |
| `x` | `double` | 锚点的 X 坐标 |
| `y` | `double` | 锚点的 Y 坐标 |
| `anchor` | `gtkAnchorType` | 文本相对于锚点的位置 |
| `font` | `gchar` | 用于`gdk_fontset_load`的字体名称 |
| `fontset` | `gchar` | 用于`gdk_fontset_load`的字体集名称 |
| `font_gdk` | `gdkFont` | 渲染字体 |
| `justification` | `gtkJustification` | 多行文本的对齐方式 |
| `fill_color` | `gchar` | 字符串形式的填充颜色或`NULL`为透明 |
| `fill_color_gdk` | `gdkColor` | 由`GdkColor`指定的填充颜色 |
| `fill_color_rgba` | `guint32` | 4字节红、绿、alpha值指定的填充颜色 |
| `fill_stipple` | `gdkBitmap` | 用于绘制的填充点纹。仅 GDK 模式 |
| `clip_width` | `double` | 以画布单位指定的文本矩形宽度 |
| `clip_height` | `double` | 以画布单位指定的文本矩形高度 |
| `clip` | `gboolean` | 是否裁剪文本 |
| `x_offset` | `double` | 添加到位置的 X 偏移 |
| `y_offset` | `double` | 添加到位置的 Y 偏移 |

文本的位置由锚点和锚点类型给出。我们可以选择`GTK_ANCHOR_CENTER`、`GTK_ANCHOR_NORTH`、`GTK_ANCHOR_WEST`、`GTK_ANCHOR_EAST`、`GTK_ANCHOR_SOUTH`、`GTK_ANCHOR_WEST`（此处原文有重复）等。我们还有选项使用`clip_width`和`clip_height`裁剪文本，确保它不会超出特定区域。

在我们绘制的线条下方添加一些文本。现在到了`canvas4.c`，请将以下内容添加到`CreateCanvasItem`：

```c
void CreateCanvasItem ( GtkWidget * canvas )
  GnomeCanvasGroup * group;
  GnomeCanvasItem * line;
  GnomeCanvasItem * text;

  /* 创建文本项 */
  text = gnome_canvas_item_new ( group, gnome_canvas_text_get_type(),
    "text", "This sentence is self-referential, which is nice.",
    "x", 20.0, "y", 270.0, "anchor", GTK_ANCHOR_WEST,
    "font", "fixed", "fill_color", "black", NULL);
```

文本出现在 (20, 270) 左侧，这就是全部。到目前为止我们所有的示例都很静态，所以让我们使用下一个`GnomeCanvasItem`来活跃一下。

# GnomeCanvasWidget

使用`GnomeCanvasWidget`在画布中嵌入组件。就像文本一样，它通过锚点在画布上定位。

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `widget` | `GtkWidget *` | 在画布上显示的组件 |
| `x` | `double` | 锚点的 X 坐标 |
| `y` | `double` | 锚点的 Y 坐标 |
| `anchor` | `GtkAnchorType` | 组件相对于锚点的位置 |
| `width` | `double` | 组件的宽度 |
| `height` | `double` | 组件的高度 |
| `size_pixels` | `boolean` | 如果为`TRUE`，宽度和高度为像素；`FALSE`则为画布单位 |

如果我们选择在画布上放置按钮组件，可以将按钮的值连接到画布的缩放因子，从而实现即时缩放！关键函数是：

```c
void gnome_canvas_set_pixels_per_unit ( GnomeCanvas * canvas, double ppu );
```

使用这种方法缩放会同时扩展 X 和 Y 方向。我们将扩展`ellipse`示例`canvas.c`，进行这些更改并保存为`canvas5.c`：

```c
/**
 * canvas5.c
 *
 * 使用 gnome canvas 绘制椭圆、矩形和按钮组件的简单程序
 */
```

```c
#include <gnome.h>

void CloseTheApp ( GtkWidget * window, gpointer data )
{
  gtk_main_quit();
}
```

```c
/** 响应按钮改变画布缩放因子的回调 */
void ChangeZoomFactor ( GtkEditable * spin, gpointer data )
{
  GtkWidget * canvas = GTK_WIDGET(data);
  gnome_canvas_set_pixels_per_unit ( GNOME_CANVAS ( canvas ), (double )
    gtk_spin_button_get_value_as_float ( GTK_SPIN_BUTTON ( spin ) );
}

void CreateCanvasItem ( GtkWidget * canvas ) {
  GnomeCanvasGroup * group;
  GnomeCanvasItem * rectangle;
  GnomeCanvasItem * ellipse;
  GnomeCanvasItem * widget;
  GtkObject * adjustment;
  GtkWidget * spinbutton;

  /* 获取画布根组 */
  group = gnome_canvas_root ( GNOME_CANVAS ( canvas ) );
  rectangle = gnome_canvas_item_new ( group, gnome_canvas_rect_get_type(),
    "x1", 75.0, "x2", 250.0, "y1", 50.0, "y2", 275.0, "fill_color",
    "red", "outline_color", "blue", "width_units", 2.5, NULL );

  ellipse = gnome_canvas_item_new ( group, gnome_canvas_ellipse_get_type(),
    "x1", 30.0, "y1", 30.0, "x2", 175.0, "y2", 200.0, "fill_color",
    0x5F9E9A0, "outline_color", "black", "width_pixels", 5, NULL );

  /* 创建调整对象并连接到按钮组件 */
  adjustment = gtk_adjustment_new ( 1.0, 0.5, 1.5, 0.1, 0.1 );
  spinbutton = gtk_spin_button_new ( GTK_ADJUSTMENT ( adjustment ), 0.02, NULL );

  /* 将回调连接到按钮 */
  gtk_signal_connect ( GTK_OBJECT ( spinbutton ), "changed",
    ( GtkSignalFunc ) ChangeZoomFactor, canvas );

  /* 为按钮创建组件项 */
  widget = gnome_canvas_item_new ( group, gnome_canvas_widget_get_type(),
    "widget", spinbutton, "x", 100.0, "y", 100.0, "anchor", GTK_ANCHOR_WEST,
    "width", 50.0, "height", 20.0, "size_pixels", TRUE, NULL );
}
```
