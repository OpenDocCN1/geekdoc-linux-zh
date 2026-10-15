
| `GCLineStyle` | `line_style` | 线条样式 (`LineSolid`, `LineOffDash`, `LineDoubleDash`) |
| `GCCap` | `cap_size` | 端点样式 (`CapLast`, `CapBut`, `CapRound`, `CapProjecting`) |
| `GCJoinStyle` | `join_style` | 接接类型 (`JoinMiter`, `JoinBevel`, `JoinRound`) |
| `GCFillStyle` | `fill_style` | 填充样式 (`FillSolid`, `FillTiled`, `FillStippled`) |
| `GCFillRule` | `fill_rule` | 填充规则 (`EvenOddRule`, `WindingRule`) |
| `GCTile` | `tile` | 用于平铺文件的 pixmap |
| `GCStipple` | `stipple` | 用于平铺点点的 Ibppixmap |
| `GCTileStipOrigin` | `ts_x_origin` | 平铺点彩操作的偏移量 |
| `GCTileStipOrigin` | `ts_y_origin` | 平铺点彩操作的偏移量 |
| `GCFont` | `font` | 文本操作的默认字体 |
| `GCsubwindowMode` | `subwindow_mode` | 子窗口裁剪 (`ClipByChildren`) 或 包含从属 (`IncludeInferiors`) |
| `GCraphics` | `exposures` | 布尔信息 |
| `GCClipOrigin` | `x_origin` | 裁剪区域的偏移量 |
| `GCClipOrigin` | `y_origin` | 裁剪区域的偏移量 |
| `GCClipMask` | `mask` | 位图 (`pixmap`) |
| `GCDash` | `dashes` | 虚线数据 |

## 绘制图像

既然我们已经可以绘制像素，现在该做些更有趣的。Xlib 使用名为 `.XPM` 的格式。XPM 文件非常简单，类似于 C 文件。`XReadBitmap` 加载 `.XPM` 文件，原型为：

```c
extern int XReadBitmap(Display* display, Drawable d,
    const char* filename, unsigned int* width,
unsigned int* height, Pixmap* bitmap,
int* x, int* y);
```

前两个参数是显示器对象。下一个参数是你想要绘制的 pixmap 路径和文件名。其他参数是存储信息的指针。

## 编程

在加载 pixmap 后，你可以使用 `XCopyPlane()` 函数绘制它，其原型显示在此：

```c
extern int XCopyPlane(Display* display, Drawable src, Drawable dest, GC gc,
 int src_x, int src_y, unsigned int width, unsigned int height, int dest_x,
 dest_y, int depth);
```

使用 `XCopyPlane()` 非常简单。与其他函数一样，你必须传递显示指针。你必须传递可绘制对象（源和目标）。下一个参数是标准 GC，你可以通过调用 `XCreateGC(display, window, 0, NIL)` 创建。接下来的四个参数描述源尺寸，随后是目标坐标。最后一个参数是源图像的颜色深度。

以下示例演示了 `XCopyPlane()` 的用法。将以下代码添加到本章前面的原始 Xsample.c 示例的开头定义部分。

- `Pixmap pic;`
- `GC gc;`
- `XGCValues gcv;`
- `int x, y;`
- `int width, height, hoxy, hoty;`
- `int err;`
- `char FILE = "/usr/share/pixmap/clock.xpm";`

// 准备上下文

`gcv.foreground = BlackPixel(display, myscreen);`

`gcv.graphics_exposures = 0;`

`gc = XCreateGC(display, window, GCForeground, &gcv);`

// 加载位图

`if (err = XReadBitmapFile(display, window,`

`FILE,`

`&width, &height, &pic,`

`&hotx, &hoty)) {`

`XCloseDisplay(display);`

`fprintf(stderr,"无法加载图像: %d", err);`

`}`

// 绘制像素

`XCopyPlane(display, pic, window, gc,`

`hotx, hoty, width, height, 0, 0, 1);`

// 释放内存

`XFreeGC(display, gc);`

### Linux 下的 ZD 图形

```c
while (1) {
x = rand() % 320;
y = rand() % 200;
}
```

```c
XCopyPlane(
    display, pic,    // 源图像
    window, gc,      // 目标细节
    0,               // 源起点
    width, height,   // 图像尺寸  
    x, y, 1);       // 目标坐标
)
```

```
// 释放内存
XFreeGC(display, gc);
XFreePixmap(display, pixmap);
```

## 双缓冲

直接绘制到窗口上有几个缺点，包括在需要时必须手动重绘屏幕，以及忍受闪烁的细节。避免屏幕闪烁的一种常用策略是使用双缓冲。这个过程涉及将所有内容都绘制到一个离屏对象上，并在所有内容完成后将其复制到窗口中。

在 X 中复制对象非常简单。首先，你使用 `XCreatePixmap()` 创建窗口的精确副本，然后每当需要将新创建的图像复制到窗口时。为了实现此过程的第二部分，你使用 `XCopyArea()`。这些函数的原型所示所示：

```
extern Pixmap XCreatePixmap(Display display, Drawable d, unsigned int width, unsigned int height, unsigned int depth);
extern int XCopyArea(Display display, Drawable src, Drawable dest, GC gc, int src_x, int src_y, unsigned int width, unsigned int depth, int dest_x, int dest_y);
```

`XCopyArea()` 的功能与 `XCopyPlane()`（在前节中描述）几乎相同，只是它没有深度参数。由于你没有指定区域的颜色深度，你必须确保两个可绘制对象具有相同的颜色深度，否则会发生 BadMatch 错误并且你的程序将终止。

`XCreatePixmap()` 是一个相对简单的函数。下面的示例演示了如何用它创建一个离屏窗口。

## Linux 游戏编程

```
// 创建双缓冲
Pixmap dbl_buf = XCreatePixmap(display, window, window_width, window_height, // 窗口尺寸
DefaultDepth(display, myscreen)); // 深度
```

创建双缓冲后，使用该对象作为可绘制表面而不是窗口。当需要显示你绘制的内容时，将缓冲区复制到窗口。代码如下所示：

```
GC gc = XCreateGC(display, window, 0, NIL);
XCopyArea(display, dbl_buf, window, gc, 0, 0, window_width, window_height, 0, 0);
```

## 安装调色板

如果你在 8 位颜色深度下工作，可能想要设置自己的调色板。只有在使用 8 位颜色时才需要调色板，因为任何其他颜色深度都使用 RGB 索引。要检测使用的颜色深度，请使用 `DisplayDepth()` 函数，它接受显示器和屏幕（示例中的 `myscreen`）作为参数。

如果使用的颜色深度是 8 位颜色，你可能需要安装调色板。你可以使用 `XCreateColormap()` 创建自己的调色板。该函数的示例所示：

```
Colormap c_map = XCreateColormap(display, window, DefaultVisual(display, myscreen), AllocNone);
```

创建调色板后，你需要分配颜色。第一步是创建一个类型为 `XColor` 的调色板。这种数据类型与之前描述的 `SDL_Color` 数据类型类似；它包含了描述颜色每个部分（红、绿、蓝）的成员，还有一个名为 `pixel` 的成员，它是颜色索引。

当你定义了颜色后，调用 `XAllocColor()`将其包含调色板。该函数的第一个参数是现在创建的显示器指针。接下来是使用 `XCreateColormap()` 创建的调色板 ID。最后一个参数是指向颜色定义的指针。

现在你已经创建了调色板（在内存中），你需要用 `XWindowColormap()` 函数来安装它。该函数接受三个参数，第一个是显示器指针。第二个参数是你想要安装颜色的窗口 ID，最后一个参数是调色板本身的 ID。

接下来的示例代码演示了调色板的安装：

```
// 创建调色板
Colormap c_map = XCreateColormap(display, window, DefaultVisual(display, myscreen), AllocNone);

// 安装一个条目
XColor red;
red.pixel = 1;
red.red = 0xFF;
red.green = 0;
red.blue = 0;
XAllocColor(display, c_map, &red);

// 设置调色板
XWindowColormap(display, window, c_map);
```

现在我们已经安装了调色板，不妨就使用它。要使用调色板，调用 `XSetForeground()`（指定像素的颜色）和 `XSetBackground()`。这些每个函数都接受三个参数：指向显示器的指针、GC 和索引。

## 清理

当退出程序时，你必须清理一些东西。你创建的每个对象都必须使用 Xlib API 进行销毁。你应该使用 `XFreeWindow()` 销毁创建的窗口，使用 `XFreeGC()` 销毁 GC，以此此类推。如果为创建的对象有特定的函数，请使用它。当你释放了各种对象使用的内存后，必须关闭与服务器的连接。要做到这一点，请使用 `CloseDisplay()`。

# LINUX 游戏编程

```
graph_mem = vga_getgraphmem();
// 绘制一些图案
for (x = 0; x < 320; x++)
    for (y = 0; y < 200; y++)
        PLOT(x,y,x ^ y);

return 0;
```

要编译此示例程序，请使用以下命令：

```
gcc -lvga -o VGAsample VGAsample.c
```

程序编译完成后，在以 root 用户登录的情况下，可以运行 `chown root VGAsample` 接着运行 `chmod 4755 VGAsample`，这将通过设置应用程序的 suid 位允许任何用户运行该程序；或者直接从 root shell 中运行该程序。

## 显示图像

SVGlib 并没有图像文件提供内置支持，因此你将需要实现自己的函数库来加载和显示图像。在这些示例中，我将演示如何加载（并显示）PCX 文件，但如果你想使用其他图像格式，可以轻松地修改函数来加载不同的文件格式。

## 理解 PCX 格式

PCX 文件使用一种称为 RLE（游程编码）的简单压缩算法。该系统用 3 字节块表示相同颜色的长段像素序列（而不是通常表示该串独立像素时所需的若干字节数）。这使得 PCX 格式适用于具有大块相同颜色的图像（如标志和简单的精灵图），但不适用于像照片那样复杂的图像。

与大多数图形格式（原始数据除外）一样，PCX 文件以一个简单的头部开始。该头部可以使用包含不同头部字段的简单结构来表示，如下所示：

```
typedef struct PCXHeader {
    char manufacturer;   // 始终为 10 (ZSoft .pcx)
    char version;         // 版本号
    char encoding;        // 编码方法 (1-RLE)
    char bitpixel;       // 每个像素的位数
    short xmin;           // 图像 X 起点
    short ymin;           // 图像 Y 起点
    short xmax;           // 图像宽度
}
```

## Linux 53 下的 Z 图形

```
short ymax; // 图像高度
short hdpi; // 水平分辨率
short vdpi; // 垂直分辨率
char colormap[48]; // 调色板信息
char reserved1; // 预留
char nplanes; // 每行的字节数
short bytesperline; // 调色板解释信息
short paletteinfo; // 水平屏幕尺寸 (v 4+)
short vscreensize; // 垂直屏幕尺寸 (v4)
char filler[54]; // 未使用数据
```

头部之后存储的是实际图像数据。图像解压后的尺寸为 `(xmax - xmin + 1)` 和 `(ymax - ymin + 1)`。总存储量为图像面积 `(xsize * ysize)` 乘以每个像素的字节数（256 色时为 1）。

解码数据非常简单。图像数据的每个字节都代表一个像素。如果像素的高两个位为 1（即像素像素值大于或等于 192），则它是一个编码像素。像素剩余的六位指示游程的长度，随后的位即为像素值。接下来的示例代码演示了如何解码像素。

```
int i = 0;
int tot_bytes = ((xmax - xmin + 1) * (ymax - ymin + 1)), curr_byte = 0;

while (curr_byte < tot_bytes) {
  ch = (*image_data + i);
  if (ch & 0xC0) { // 编码位
    num_bytes = ch - 192; // 游程长度
    i++;
    ch = *(image_data + i); // 像素颜色
    for (int n = 0; n < num_bytes; n++) {
      curr_byte += *(image + curr_byte) = ch;
    }
  } else { // 标准像素
    curr_byte += *(image + curr_byte) = ch;
  }
  i++;
}
```

## 54 Linux 游戏编程

在你成功解码数据后，你几乎获得了一个完整的图像。然而，文件末尾前的 739 字节处可能是调色板数据开始的地方。如果假设调色板数据的第一个字节是 12，则剩余数据就是图像调色板的信息。调色板的每个条目

3 字节，每个分量一个（顺序为红、绿、蓝）。

加载图像的完整代码如下：

```
// 调色板信息
typedef struct {
    char r, g, b;
} RGBval;

// PCX 图像
typedef struct {
    PCXHeader header; // 头部信息
    char *image; // 解压缩图像
    RGBval palette[256]; // 调色板数据
} PCImage;

PCXImage pcx_load(char *filename) {
    FILE *fp;
    PCXHeader head;
    PCXImage image;
    int xsize;
    int ysize;
    int curr_byte, num_bytes;

// 打开文件
    if (!fp = fopen(filename, "r")) {
        fprintf(stderr, "pcx_load(): 打开读取文件错误");
        return NULL;
    }

    fread(image.header, sizeof(image.header), 1, fp); // 修正：此处原文逻辑略有偏差，保留翻译

    if (image.header.manufacturer != 10) {
        fprintf(stderr, "pcx_load(): Invalid PCX format");
        return NULL;
    }

// 计算尺寸
    xsize = (image.header.xmax - image.header.xmin + 1);
    ysize = (image.header.ymax - image.header.ymin + 1);

// 为图像分配内存
    image.image = (char*)malloc(xsize * ysize);

```

while (curr_byte < tot_bytes) {

  ch = *(image_data + i);

  if (ch & 0xC0) { // 编码位

    num_bytes = ch - 192; // 游程长度

    i++;

    ch = *(image_data + i); // 像素颜色

    for (int n = 0; n < num_bytes; n++) {
