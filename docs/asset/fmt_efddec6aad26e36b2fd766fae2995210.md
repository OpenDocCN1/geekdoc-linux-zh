
```
if (re->outline_svp != NULL) {
  gnome_canvas_render_svp(buf, re->outline_svp, re->outline_color);
}
```

如你所见，渲染的工作是在 `gnome_canvas_render_svp(svp)` 中进行的，这是 `libgnomeui/gnome-canvas-util.h` 中的另一个函数；这里是它的实现：

```
void
gnome_canvas_render_svp (GnomeCanvasBuf *buf, ArtSVP *svp, uint32 rgba)
{
  uint32 fg_color, bg_color;

  if (buf->is_bg) {
    bg_color = buf->bg_color;
    fg_color = rgba;
    art_rgb_svp(svp,
      buf->rect.x0, buf->rect.y0, buf->rect.x1, buf->rect.y1,
      fg_color, bg_color,
      buf->buf, buf->rowstride,
      NULL);
  } else {
    art_rgb_alpha(svp,
      buf->rect.x0, buf->rect.y0, buf->rect.x1, buf->rect.y1,
      rgba,
      buf->buf, buf->rowstride);
  }
}
```

要理解 `gnome_canvas_render_svp(svp)`，或者不使用 `libart` 进行自己的 RGB 缓冲区绘制，你需要了解 `GnomeCanvasBuf` 是：

```
typedef struct {
  guchar *buf;
  int rowstride;
  ArtRect rect;
  uint32 bg_color;
  unsigned int is_bg : 1;
  unsigned int is_buf : 1;
} GnomeCanvasBuf;
```

`buf` 成员是一个 RGB 缓冲区，如第 10 节“Buffers”部分所述。`rowstride` 是行距，如第 10 节“Buffers”部分所述。`ArtRect` 是一个表示该缓冲区代表画布坐标重绘区域的整数矩形。`rect.x0` 和 `rect.y0` 是缓冲区偏移，对应 RGB 缓冲区中的第 0 行第 0 列；你可以通过减去这些值将画布坐标转换为 RGB 缓冲区坐标。`rect.x1` 和 `rect.y1` 不是重绘区域的一部分，而是边界，大于等于 `rect.x0` 且小于 `rect.y1` 的坐标。画布不会用背景颜色初始化 RGB 缓冲区，因为第一个画布项可能会覆盖整个背景。因此，如果你的画布项是第一个渲染的，你必须在 `rect` 定义的重绘区域的每个像素中放入值。如果你的项没有覆盖某个像素，你应该用 `bg_color` 填充该像素；`bg_color` 是一个打包的 RGB 值。如果你手动这样做，可以这样解包 RGB 值：

```
guchar r, g, b;
r = (rgb >> 16) & 0xff;
g = (rgb >> 8) & 0xff;
b = rgb & 0xff;
```

然而，一个方便的函数是用其 `bg_color` 填充 `GnomeCanvasBuf`：

```
void
gnome_canvas_buf_ensure_buf (GnomeCanvasBuf *buf)
{
  guchar *bufptr;
  int y;

  if (buf->is_buf) {
    bufptr = buf->buf;
    for (y = buf->rect.y0; y < buf->rect.y1; y++) {
      art_bg_fill(bufptr,
                  buf->bg_color >> 16,
                  (buf->bg_color >> 8) & 0xff,
                  buf->bg_color & 0xff,
                  buf->rect.x1 - buf->rect.x0);
      bufptr += buf->rowstride;
    }
    buf->is_buf = 1;
  }
}
```

从 `gnome_canvas_buf_ensure_buf()` 的实现可以看出，`is_bg` 是一个标志，指示 RGB 缓冲区仍然包含内存垃圾；它尚未初始化，随后的项表示缓冲区将只自身，忽略背景像素。这两个标志是互斥的；如果你的项接收到一个设置了 `is_bg` 的缓冲区，则需要步骤填充缓冲区、取消 `is_bg` 并设置 `is_buf`：

```
if (buf->is_bg) {
  gnome_canvas_buf_ensure_buf(buf);
  buf->is_bg = FALSE;
}
```

## 速度与 RGB 渲染

如果你有大量对象，RGB 模式可能比 GDK 模式更快。到 RGB 缓冲区绘制只是简单的数组赋值，这比让 GDK 画布连接到 X 服务器并由其执行实际绘制快得多。昂贵的部分是在执行时将 RGB 缓冲区拷贝到 X 服务器。然而，无论你有多少画布项，拷贝的时间都是相同的，因为只在所有项渲染完成后执行一次。

这对于我正在编写的名为 "`Guppi`" 的应用程序是一个巨大的胜利。`Guppi` 是一个绘图程序。它必须要做之一是渲染带有数千个点的散点图。每个点都是一个小颜色的形状；如果我调用 `GoDK` 来渲染每个点，将会有跨网络的几十或数百次访问 X 服务器。相反，我使用 RGB 模式，通过自定义项渲染，画布一次性将 RGB 缓冲区拷贝到服务器。它既快又有响应。对于图中计算不那么密集的元素（例如图例），我可以节省时间并使用内置的画布项。

到 RGB 渲染的唯一困难之处在于，如果你想绘制默认画布项以外的任何内容，你需要一个与 GDK 原型相当的光栅化库。你可以在你的自定义项中使用它，如果你只绘制数百个形状，那是最好的；但如果你正在绘制数千个形状，你会很快需要更快速的东西。这是可以提供的；GDK Plotutils 包的维护者从 X 分发中提取了光栅化库，在 `Guppi` 开发期间我从 `Plotutils` 中提取了它并进行了修改以与画布的 RGB 缓冲区工作。我还添加了透明度支持。生成的库允许你在 RGB 缓冲区上绘制，就像使用 GDK 绘制一样。

Ralph Levien，关于 `libart_lg` 和 `GdkRGB` 模块，告诉我静态程序会更好；如果你需要更多速度，请考虑这个挑战。

## 绘制方法（GDK 模式）

使用 GDK 绘制比使用 `libart-lg` 绘制简单得多，尽管它的灵活性较低且质量较低。以下是 `GnomeCanvas` 方法方法的实现：

```
static void
gnome_canvas_rect_draw (GnomeCanvasItem *item, GdkDrawable *drawable,
	int x, int y, int width, int height)

GnomeCanvas *re;
	double i2w[6], w2c[6], i2c[6];
	int x1, y1, x2, y2;
	ArtPoint i1, i2;
	ArtPoint c1, c2;
```

## 第 13 章 编写 GnomeCanvasItem
