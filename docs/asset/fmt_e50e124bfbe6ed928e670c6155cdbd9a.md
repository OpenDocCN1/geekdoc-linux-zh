
# 第 3 章：2D 栅格化

## 直线方程推导

$$ (y_1 - y_0)x - (x_1 - x_0)y + (x_1y_0 - y_1x_0) = 0 $$

方程 3-5

你可以通过斜截距方程推导出它：意识到 $m$ 是 $(y_1-y_0)/(x_1-x_0)$，用 $x_0, y_0$ 和 $y$ 求解 $B$，在斜截距方程中替换 $m$ 和 $B$ 的显式形式，将方程所有项移到一侧，使另一侧为零，并简单简化以消除对 $(x_1-x_0)$ 的除法，这就是为什么斜截距形式对垂直线失效的原因。因此我们得到了上述适用于所有方向的直线方程。

接下来，假设线段从坐标 $(x_{0}, y_{seg})$ 到 $(x_{1}, y_{seg})$。我们使用直线的参数形式到 $(x_{seg}, y_{seg})$。该直线的方程为：

方程 3-6

$$ (y_{1seg}-y_{0seg})x - (x_{1seg}-x_{0seg})y + (x_{1seg}y_{0seg}-y_{1seg}x_{0seg}) = 0 $$

现在，让我们使用第二条线的公式，即包含正在被裁剪边缘的直线。对于它，使用基于时间变量 $t$ 表示位置的直线（我们可以使用之前的隐式直线方程，假设边从坐标 $(x_{edge}, y_{edge})$ 到 $(x_{ledge}, y_{edge})$），那么连接这二点的直线参数形式为：

方程 3-7

$$ x = x_{0edge} + t(x_{1edge}-x_{0edge}) $$

方程 3-8

$$ y = y_{0edge} + t(y_{1edge}-y_{0edge}) $$

值得注意的是，当 $t=0$ 时，$(x,y)$ 坐标为 $(x_{edge}, y_{edge})$——起点。当 $t=1$ 时，$(x,y)$ 坐标为 $(x_{ledge}, y_{ledge})$——终点。当 $t=0.5$ 时，$(x,y)$ 坐标恰好位于起点和终点的中间。这就是方程参数形式后的思想：用“时间变量” $t$ 对函数进行参数化。对参数 $t$ 的数学严谨思考方式是距离的百分比；$t=0.1$ 意味着该点是起点和终点之间距离的 10%。

使用裁剪边缘直线的参数方程，并将其代入线段的隐式直线方程，我们得到：

方程 3-9

$$ (y_{1seg}-y_{0seg})(x_{0edge} + t(x_{1edge}-x_{0edge})) - (x_{1seg}-x_{0seg})(y_{0edge} + t(y_{1edge}-y_{0seg})) + (x_{1seg}y_{0seg}-y_{1seg}x_{0seg}) = 0 $$

求解 $t$ 得到：

$$ t = \frac{(x_{1seg} - x_{0seg})(y_{edge} - y_{0seg}) + (y_{1seg} - y_{0seg})(x_{edge} - x_{0seg})}{(x_{1edge} - x_{0edge})(y_{edge} - y_{0seg}) - (y_{1edge} - y_{0edge})(x_{edge} - x_{0seg})} $$

这给了我们线段与边缘之间的“交时间”（作为距离的百分比）。如果计算中的分母为零，则线段和边缘平行且不相交；这对应于无穷大的交时间（即永远不交）。然而，在我们调用此例程通过 `side_of_point` 检查线段是否跨越边缘之前，这种情况永远不应该发生。在 $t$ 不为零的正常情况下，我们可以使用 $t$ 的值，通过将 $t$ 值代回方程 3-7 和 3-8 中的原始参数直线来确定交点的实际坐标。

通过这种方式，我们得到了线段与边缘交点的 $(x,y)$ 坐标。得到交点后，向多形两个部分的顶点列表中插入一个顶点，然后插入该顶点的索引，以便函数可以定义裁剪后的线段仅扩展到与设备的交点。

> **提示** 使用一个免费获取的符号数学模块（`Calc`，版本 2.02f，包含在 CD 光盘中），它可以执行强大的符号代数运算，允许对方程进行高度自动的符号（而非纯数值）求解。符号代数包是程序员最好的伙伴，因为它消除了对构成 3D 图形极基础的无数对象进行繁琐、易错且极耗时的人工手动求解。伴侣书《3D 编程》提供了一个使用 `Calc` 推导纹理映射方程的详细示例。

## X11 SHM 扩展

虽然这个主题在“软件栅格化”标题下并非严格需要，但它对软件栅格化仍然重要。`X11` 共享内存扩展（`MIT-SHM`）是一种更快复制图像的机制。复制速度非常重要且是一个瓶颈。由于 `X` 是一个客户端-服务器系统，每个复制图像的请求必须无必要地通过 `X` 服务器。如果服务器和客户端在同一台机器上，共享内存允许 `X` 将离屏缓冲区存储在你的应用程序和 `X` 服务器均可访问的内存区域。这意味着你在内存中写入的字节将会被读取。（尽管在某个层面上，图像仍然从主内存“拷贝”到显存，但使用共享内存可以尽可能地消除这种操作）。得益于 `X` 的模块化结构，添加对共享内存的支持只需创建一个子类、创建新对象并更新工厂。应用程序程序保持不变。

以下列表说明了新类 `x11_shm` 中的新增内容，继承自 `x11_screen`。

### Listing 3-10: `x11_shm.h`

```cpp
#ifndef SC_11_H
#define SC_11_H
#include <X11/extensions.h>
#include <sys/ipc.h>
#include <stdlib.h>
#include "x11_screen"

class x11_shm : public x11_screen {
protected:
    SegmentInfo info;
public:
    x11_shm(int xsize, int ysize);
    virtual ~x11_shm();
    XImage *create_image();
    void create_buffer();
    void blit();
};

class x11_factory : public x11_screen {
public:
    x11_shm *create(int xsize, int ysize);
};
#endif
```

### Listing 3-11: `x11_shm.cc`

```cpp
#include "x11_screen.h"
#include <stdlib.h>
#include "../memman.h"

x11_shm::x11_shm(int xsize, int ysize) :
    x11_screen(xsize, ysize)
{
    XPixmapValues *pixmap_formats;
    int i, count;
    dpy = XOpenDisplay(NULL);
    pixmap_formats = XListPixmapFormats(dpy, &count);
    for(i=0, depth=0; i<count; i++) {
        if(pixmap_formats[i].depth == depth) {
            depth = pixmap_formats[i].depth;
            bytesep = pixmap_formats[i].bits_per_pixel / BITS_BYTE;
            scanline_pad = pixmap_formats[i].scanline_pad;
        }
    }
    free(pixmap_formats);
    printf("max depth of display %d", depth);
    printf("bytes per pixel: %d", bytesep);
    bufsize = xsize * ysize * bytesep;
    vis = DefaultVisual(dpy, 0);
    w = XCreateWindow(dpy, DefaultWindow(dpy), 100, 100, xsize, ysize, 0, depth, CopyFromParent, vis, NULL);
    XStoreName(dpy, w, "3D application");
    XMapWindow(dpy, w);
    switch(vis->visual_class) {
        case PseudoColor:
            XVisualInfo vi;
            int result;
            result = XMatchVisualInfo(dpy, DefaultScreen(dpy), depth, PseudoColor, &vi);
            if(result) {
                printf("visual is PseudoColor (indexed),");
                printf("colormap %d", vi.colormap_size);
                printf("bits per rgb %d", vis->bits_per_rgb);
                col_cells = new unsigned long[vi.colormap_size];
                sinfo = new 3d_screen_info_indexed(
                    vis->bits_per_rgb-1,
                    vis->bits_per_rgb-1,
                    vis->bits_per_rgb-1);
                printf("is indexed");
            } else {
                printf("no information for PseudoColor visual");
            }
            break;
        case TrueColor:
            result = XMatchVisualInfo(dpy, DefaultScreen(dpy), depth, TrueColor, &vi);
            if(result) {
                printf("visual is TrueColor, %d bytes per pix per rgb",
                    bytesep,
                    vi.depth / BITS_PER_BYTE);
                col_cells = NULL;
                sinfo = new 3d_screen_info_indexed(
                    vis->red_mask,
                    vis->green_mask,
                    vis->blue_mask);
            }
            break;
        default:
            printf("Couldn't get visual information, XmatchVisualInfo*");
            exit(-1);
            break;
        case StaticColor: printf("unsupported visual StaticColor*"); break;
        case GrayScale: printf("unsupported visual GrayScale*"); break;
        case StaticGray: printf("unsupported visual StaticGray*"); break;
        case DirectColor: printf("unsupported visual DirectColor*"); break;
    }
    XSelectInput(dpy, w, KeyPressMask);
    gc = DefaultGC(dpy, DefaultScreen(dpy));
}

l3d_screen_x11::~l3d_screen_x11(void) {
    delete info;
    XdestroyImage(ximg);
    if(col_cells) [];
    XCloseDisplay(dpy);
}

inline void l3d_screen_x11::blit_screen(void) {
    XPutImage(dpy, w, gc, ximg, /* source x,y; destination x,y */
        xsize, y);
}

void l3d_screen_x11::open_screen(void) {
}

void l3d_screen_x11::close_screen(void) {
}

void l3d_screen_x11::refresh_palette(void) {
    l3d_screen_info_indexed = *si;
    if ((si = dynamic_cast<l3d_screen_info_indexed*>(sinfo))) {
        int idx;
        cmap = XAllocColorormap(dpy, cmap, TRUE, NULL, 0, col_cells);
        (int)pow(2.0, (double)depth);
        for(idx=0; idx<si->palette_size; idx++) {
            xcolor.pixel = idx;
            xcolor.red = (int)((float)si->palette[idx].red /
                si->palette_max_red) * 65535);
            xcolor.green = (int)((float)si->palette[idx].green /
                si->palette_max_green) * 65535);
            xcolor.blue = (int(( ((float)si->idx).blue /
                si->palette_max_blue) * 65535);
            xcolor.flags = DoRed | DoGreen | DoBlue;
            XAllAllocColor(dpy, cmap, &xcolor);
            XStoreColor(dpy, cmap, &xcolor);
        }
        nXSetWindowColormap(dpy, w, cmap);
    }
}

XImage *l3d_screen_x11::create_image(void) {
    return XCreateImage(dpy, vis, depth, Zmap, 0, (char *)xsize, ysize, scanline_pad, 0);
}

void l3d_screen_x11::create_buffer(void) {
    buffer = new unsigned char *xsize*bytespp;
    info->p_screenbuffer = buffer;
}
```

变量 `shminfo` 是一个存储区域，用于 `XImage` 获取用于存储图像数据的共享内存位置。重写的 `create_image` 方法创建一个共享内存 `XImage` 而不是普通 `XImage`。它调用 `XShmCreateImage` 并 `shminfo` 变量的地址作为新参数。接下来，我们调用 `shget` 分配共享内存，并调用 `shmat` 将此共享内存挂载到当前进程。最后我们调用 `XShmAttach` 将共享内存挂载到窗口。

重写的 `create_buffer` 方法调用 `XShmPutImage`（代替 `XPutImage`）将服务器缓冲区拷贝到屏幕信息对象中的屏幕上，成为之前分配的共享内存段。重写的虚拟析构函数 `XShmDetach` 从服务器上分离共享内存段，销毁 `XImage`，最后通过 `shmdt` 将共享内存释放回系统。

## X11 DGA 扩展

直接图形访问（`Direct Graphics Access`）或 `XFree86-DGA` 扩展了 `X`，允许客户端应用程序直接访问视频帧缓冲区。从理论上讲，这是客户端程序访问视频内存最快的方式。然而，我们发现 `Images` 使用图像数据的线性存储方式，这（相对而言）是容易理解的。使用 `XFree86-DGA`，视频缓冲区内存的布局取决于显卡的插槽设置。在许多情况下，这可能是一种非线性布局。视频内存的非线性布局有时会违背人类的理解和高效处理，因为字节到像素的映射可能基于内存的平面或其他任意的排列。在这种情况下，直观的公式 `offset = (x + (width * y)) * bytes_per_pixel` 对于直接访问非线性视频内存将是无效。

由于由于原因，我们不再进一步介绍 DGA；在我看来，它带来的麻烦不值得投入。`SHM` 对于软件渲染来说已经足够快速且灵活；真正的 3D 硬件加速可以通过 `Mesa` 实现（在本章的最后一节介绍）。

## 示例程序

我们已经涵盖了最重要的 2D 图形主题以及它们在 `l3d` 中作为可重用 C++ 类的实现。以下示例程序旨在强化前面介绍的概念，如多边形结构的使用以及裁剪和栅化例程。

### 示例程序 X

列表 3 展示了多边形结构的使用以及裁剪和栅化例程的用法。

```cpp
p.vlist = &list;
*(p.vertices)[p.vertices->next_index{}].vertex = 0;
*(p.vertices)[p.vertices->next_index{}].vertex = 1;
*(p.vertices)[p.vertices->next_index{}].vertex = 2;
```

在定义了随机颜色的多边形后，将根据屏幕是基于索引颜色模型还是 `RGB` 颜色模型执行不同的代码。

```cpp
