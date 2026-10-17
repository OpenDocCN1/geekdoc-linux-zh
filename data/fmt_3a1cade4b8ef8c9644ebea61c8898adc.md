
接下来 `gnome_canvas_rect_update(item)` 继续处理 `GnomeCanvasRect` 的细节。完成了以下任务：

- 更新画布项的边界（bounding box）。每个画布项都有关联的边界框；`GnomeCanvasGroup` 和 `render` 方法使用它来确定哪些项在重绘区域。在 `GDK` 和抗齿模式下，必须更新边界框。
- 在抗齿模式下，会创建一个排序矢量路径。排序矢量路径仅仅是一系列类似于 PostScript 操作的绘制指令，`libart_lgl` 可以将其渲染到 RGB 缓冲区。
- 在抗齿模式下，`update` 方法的 `affine` 和 `clip_path` 参数用于变换排序矢量路径；然后隐式存储 `affine` 和 `clip` 供 `render` 方法使用。如果你在自己的画布项没有没有 `libart_lgl` 的排序矢量路径，你必须安排它们以确保在渲染时考虑到仿射和裁剪。
- 在两种模式下，都会对使用的区域请求重绘，该区域现在将更新。

这大部分工作在 `libgnome` 的实用函数中完成。`gnome_canvas_update_bbox()` 设置项的新边界框；它使用的是 `GDK` 模式。`gnome_canvas_update_bbox()` 期望像素坐标；`get_bounds()` 是一个计算像素坐标矩边界的简单函数。

为了让你知道后台发生了什么，这里是 `gnome_canvas_update_bbox()` 的实现：

```c
void
gnome_canvas_update_bbox (GnomeCanvasItem *item,
                               int x1, int y1,
                               int x2, int y2)
{
    gnome_canvas_request_redraw (item->canvas,
                               item->x1, item->y1,
                               item->x2, item->y2);

    item->x1 = x1;
    item->y1 = y1;
    item->x2 = x2;
    item->y2 = y2;
    gnome_canvas_request_redraw (item->canvas,
                               item->x1, item->y1,
                               item->x2, item->y2);
}
```

当然，你可以自由执行等效操作，这仅仅是一个便利函数。

在 `GDK` 模式下，发生的就是这些：我们更新边界并返回。抗齿模式稍微复杂一些，但执行的任务本质相同。首先，`gnome_canvas_item_reset_bbox()` 将项的边界设置为空矩形。然后准备两个矢量路径；一个用于矩形的实心部分（如果有），另一个用于矩形（如果有）。每次都遵循相同的步骤。首先，为 `libart_lgl` 准备一个矢量；对路径进行变换；然后使用 `gnome_canvas_item_update_svp_clip()` 请求旧路径重绘、释放旧路径、裁剪新路径、请求新路径重绘并保存新路径用于渲染。如果矩形的填充或轮廓已关闭，则请求旧路径重绘，但不创建新路径。

## 第 13 章 编写一个 GnomeCanvasItem

### `gnome_canvas_item_update_svp_clip`

```c
gnome_canvas_item_update_svp_clip (GnomeCanvasItem *item,
ArtSVP **p_svp, ArtSVP *new_svp,
ArtSVP *clip_svp)
{
 ArtSVP *clipped_svp;
 if (clip_svp != NULL) {
  clipped_svp = art_svp_intersect (new_svp, clip, clip_svp);
  art_svp_free (new_svp);
} else {
  clipped_svp = new_svp;
} 
  gnome_canvas_item_update_svp (item, p_svp, clipped_svp);
}
```

### `gnome_canvas_item_update_svp`

```c
void
gnome_canvas_item_update_svp (GnomeCanvasItem *item,
ArtSVP **p_svp, ArtSVP *new_svp)
{
Rect bbox;
 gnome_canvas_update_svp (item->canvas, p_svp, new_svp);
{
 bbox.x0 = item->x1;
box.y0 = item->y1;
box.x1 = item->x2;
box.y2 = item->y2;
art_direct_svp_union (&bbox, new_svp);
item->x1 = bbox.x0;
item->y1 = bbox.y0;
item->x2 = bbox.x1;
item->y2 = bbox.y1;
}
}
```

### `gnome_canvas_update_svp`

```c
void
gnome_canvas_update_svp (GnomeCanvas *canvas,
ArtSVP **p_svp, ArtSVP *new_svp)
{
 ArtSVP *old_svp;
ArtSVP *diff;
ArtU *repaint_uta;

old_svp = *p_svp;
 if (old_svp != NULL && new_svp != NULL) {
 repaint_uta = art_uta_from_svp (old_svp);
 gnome_canvas_request_redraw_uta (canvas, repaint_uta);
 repaint_uta = art_uta_from_svp (new_svp);
 gnome_canvas_request_redraw_uta (canvas, repaint_uta);
}
else if (old_svp != NULL)
{
  repaint_uta = art_uta_from_svp (old_svp);
  art_svp_free (old_svp);
  gnome_canvas_request_redraw_uta (canvas, repaint_uta);
  *p_svp = new_svp;
}
}
```

再次，所有这些内容在 `libgnomeui/gnome-canvas-util.h` 中对于任何画布项来说都更容易管理。忽略实现细节；核心思想只是查看正在执行哪些工作。如果你知道 `libart` 中的 `ArtDirect` 是一个“带有双精度数的矩形”，而 `Uta` 是一个“细微箭头”（基本上是小区域的列表），那么代码可能会更容易理解。（抗锯齿画布以非常复杂的方式跟踪重绘区域。注意，`Uta` 中的“U”应该是表示“微”的希腊字母，它并不代表以 U 开头的单词。）

## 请求更新

当项目的属性发生且需要刷新屏幕时，由画布负责请求更新或重绘。这是直接的。例如，这里是 `gnome_canvas_re_set_arg()` 的一段代码，它设置了 `"y2"` 参数：

```c
case ARG_Y2:
re->y2 = GTK_VALUE_DOUBLE (*arg);
gnome_canvas_item_request_update (item);
break;
```

由于 `"y2"` 修改了矩形，必须重新创建路径并进行更新。注意 `gnome_canvas_item_request_update(item)` 只是设置了一个标志，并在如果没有挂起的任务的情况下安装一个空闲处理程序，因此可以调用多次而不会产生性能损失。

并不是所有更改都需要更新；重绘可能足够了，或者该参数与显示无关。这取决于画布项以及具体更改了什么。

## Render 方法（抗锯齿模式）

该方法由 `GnomeCanvasRect` 和 `GnomeCanvasEllipse` 共享；它将项中创建的路径绘制到 RGB 缓冲区：

```c
static void
gnome_canvas_re_render (GnomeCanvasItem *item,
  GnomeCanvasBuf *buf)
{
  GnomeCanvasRE *re;
  uint32 fg_color, bg_color;

  re = GNOME_CANVAS_RE (item);
if (re->fill_svp != NULL) {
  gnome_canvas_render_svp(buf, re->fill_svp, re->fill_color);
}
}
```
