
```c
/* 根据需要设置 xgcv 成员的值。
* 然后设置掩码，此示例将前景和
* 背景像素设置为屏幕默认的白色和黑色
* 颜色
*/
xgcv.foreground = WhitePixel(disp, DefaultScreen(disp));
xgcv.background = BlackPixel(disp, DefaultScreen(disp));
mask = GCForeground|GCBackground;
```

```c
gc = XCreateGC(disp, win, mask, &xgcv);
```

由于 `GC` 是一种资源，它会消耗 X 服务器的内存。因此，在不再需要时，你应该释放 `GC`。你可以通过 `XFreeGC` 函数来实现，如下：

```c
Display *disp;
GC gc;
```

```c
XFreeGC(gc, disp);
```

当应用程序退出时，X 服务器会自动释放你所有的资源（包括 `GC`），因此只有当你为了临时目的创建 `GC` 时才需要显式销毁它。

## GC 属性

X 服务器维护 `GC`，因此你不需要了解 `GC` 的内部细节。你通过 `XGCValues` 结构体指定 `GC` 属性的值。基本思想是设置你需要的属性值，然后创建一个 `GC` 位掩码来指示结构中的哪些成员具有有效值。X 服务器结合 `XGCValues` 结构体和位掩码来决定更改 `GC` 的部分。

`XGCValues` 结构的定义让你了解可以控制的属性。以下是该结构的定义：

```c
typedef struct {
    int function;               /* 像素操作 */
    unsigned long plane_mask;    /* 受影响的平面 */
    unsigned long foreground;      /* 前景像素值 */
    unsigned long background;      /* 背景像素值 */
    int             line_width;     /* 线宽（0 或更多） */
    int             line_style;     /* 样式之一：实线、
                                     虚线、
                                     双虚线 */
    int             cap_style;      /* 端点样式：末尾端、
                                     起始端、
                                     圆端、
                                     投影端 */
    int join_style;               /* 连接样式：直角连接、
                               圆角连接、
                               倒角连接 */
    int fill_style;                /* 填充样式之一：实色、
                               平铺、点彩、
                               透明点彩 */
    int fill_rule;                 /* 填充规则：奇偶规则、
                               环绕规则 */
    int arc_mode;                  /* 弧形模式：圆弦弧、
                               扇形弧 */
    Pixmap tile;                   /* 平铺的位图 */
    Pixmap stipple;                /* 点彩位图 */
    int ts_x_origin;               /* 平铺的 x 和 y 偏移 */
    int ts_y_origin;               /* 或点彩操作 */
    int font;                       /* 默认字体 */
    int window_mode;               /* 窗口模式之一：裁剪子窗口、
包含子窗口 */
    Bool graphics_exposures;       /* True 生成暴露事件 */
    int clip_x_origin;             /* 裁剪掩码的起点 */
    int clip_y_origin;
    Pixmap clip_mask;              /* 裁剪位图 */
    int offset;                    /* 控制虚线 */
    char dashes;                    /* 虚线模式 */
} XGCValues;
```

# 第 23 章：Linux X 编程

## 表 23-3 GC 属性的位掩码常量

| 属性名称 | 位掩码常量 | 说明 |
|---|---|---|
| function | GCFunction | 对像素进行操作（默认值：覆盖现有像素） |
| plane_mask | GCPlaneMask | 受影响的位平面（默认值：影响所有位平面） |
| foreground | GCForeground | 前景像素（默认值：0） |
| background | GCBackground | 后景像素（默认值：1） |
| line_width | GCLineWidth | 线宽（默认值：0） |
| line_style | GCLineStyle | 线样式（默认值：实线） |
| cap_style | GCCapStyle | 线端样式（默认值：在端点结束，无任何投影） |
| join_style | GCJoinStyle | 线段连接方式（默认值：斜接连接） |
| fill_style | GCFillStyle | 填充样式（默认值：实填充） |
| fill_rule | GCFillRule | 图形填充方式（默认值：使用偶数规则，即从图形外部向内画出的线跨越边界奇数次，则该点位于内部） |
| arc_mode | GCAMode | 填充弧的外观或使用弦闭合（默认值：弧形作为扇形填充） |
| tile | GCTile | 平铺的位图（默认值：用前景像素填充的位图） |
| stipple | GCStipple | 点彩的位图（默认值：全 1 位图）。点彩类似于一个模板，通过它将前景颜色应用到可绘制对象上。 |
| ts_x_origin | GCTileClipOrigin | 平铺或点彩的 x 偏移（默认值：0） |
| ts_y_origin | GCTileClipOrigin | 平铺或点彩的 y 偏移（默认值：0） |
| font | GCFont | 文本输出的默认字体（默认值：取决于 X Server） |
| subwindow_mode | GCSubwindowMode | 是否绘制到子窗口（默认值：不绘制到窗口内） |
| graphics_exposures | GCGraphics Exposures | 如果为 True 则生成的图形曝光事件（默认值：True） |
| clip_x_origin | GCClipOrigin | 裁剪掩码的 x 起点（默认值：0） |

### 表 23-3（续）

| 属性名称 | 位掩码常量 | 说明 |
| --- | --- | --- |
| clip_y_origin | GCClipOrigin | 裁剪掩码的 y 起点（默认值：0） |
| clip_mask | GCClipMask | 裁剪位图（默认值：不使用裁剪掩码） |
| dash_offset | GCDashOffset | 虚线模式中的起点（默认值：0） |
| dashes | GCDashList | 虚线模式（默认值：4 像素开启、4 像素关闭的模式） |

### 绘制点

X 中最简单的图形操作是在窗口或位图中绘制一个点。你可以通过以下调用在坐标 `x`, `y` 处绘制一个单点：

```
Display *disp;      /* 与 X server 的连接 */
Window win;         /* 可绘制对象--窗口 */
GC thisGC;           /* 用于绘图的图形上下文 */
int x, y;            /* 待绘制的点 */
```

`XPoint(disp, win, thisGC, x, y);`

该位置的像素被设置为 `GC` 中指定的前景颜色。`GC` 中的其他属性控制该点的最终外观。例如，如果该点位于裁剪掩码之外，则将不绘制该点。
