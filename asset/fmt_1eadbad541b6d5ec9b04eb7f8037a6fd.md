
`XmsFunctionSet` 结构中的屏幕初始化回调获取指定屏幕的颜色特征化数据（设备配置文件），通常在屏幕的根窗口上。然后初始化指定的 `XmsPerScrnInfo` 结构。如果成功，该程序将如下填充 `XmsPerScrnInfo` 结构：

- 它将 `screenData` 设置为创建的设备配置结构的地址（内容仅函数集已知）。
- 它设置了 `screenWhitePoint` 成员。
- 它接着设置 `functionSet` 成员为 `XcmsFunctionSet` 结构的地址。
- 然后它将 `state` 成员设置为 `XcmsInitSuccess`，并返回 `XcmsSuccess`。

如果执行失败，该程序会将 `state` 成员设置为 `XcmsInitFailure` 并返回 `XcmsFailure`。

`XcmsPerScnInfo` 结构包含：

```c
typedef struct _XcmsPerScnInfo {
XcmsColor screenWhitePoint;
Xpointer functionSet;
Xpointer screenData;
unsigned char state;
char pad[3];
} XcmsPerScnInfo;
```

`screenWhitePoint` 成员指定屏幕固有的白点。`functionSet` 成员指定相应的函数集。`screenData` 成员指定设备配置文件。`state` 成员设置为以下之一：

- `XcmsInitNone` 表示之前没有尝试过初始化。
- `XcmsInitFailure` 表示之前尝试过初始化但失败了。
- `XcmsInitSuccess` 表示之前尝试过初始化并成功了。

屏幕释放回调函数必须遵循以下软件接口规范：

```c
typedef void (*XcmsScreenFreeProc)(screenData);
```

`screenData` 指定要释放的数据。

此函数被用于释放存储在 `XcmsPerScnInfo` 结构中的 `screenData`。

# 第 7 章. 图形上下文函数

在 X 中执行图形操作时，会使用多种资源。关于执行图形操作的大部分信息（例如，前景颜色、背景线型等）都存储在名为图形上下文（GCs）的资源中。大多数图形操作（见第 8 章）都将 GC 作为参数传递。尽管在理论上 X 协议允许应用程序之间共享 GC，但预计应用程序在执行操作时将使用自己的 GC。强烈不建议共享 GC，因为库可能会缓存 GC 状态。

图形操作可以在窗口（windows）或位图（pixmaps）上执行，这些对象统称为“绘制绘制（drawables）”。每个可绘制对象存在于单个屏幕上。GC 是针对特定的屏幕和绘制深度创建的，并且只能与具有匹配屏幕和深度的可绘制对象一起。

本章讨论了如何：

- 操作图形上下文/状态
- 使用图形上下文约定函数

## 操作图形上下文/状态

图形操作的大多数属性存储在 GC 中。这些包括线宽、线型、平铺掩码、前景、背景、点彩、裁剪区域、端点、样式等。图形操作（例如，画线）使用这些值来确定实际的绘制操作。X 的扩展可能会为 GC 添加额外的组件。GC 的内容对 Xlib 是私有的。

Xlib 为 GC 中所有非 Xlib 资源 ID 的元素实现了写回缓存，以实现对 GC 调用的合并。例如，调用 `XSetForeground` 后再调用 `XSetLineAttributes` 会导致向服务器仅发送一次更改的 GC 协议请求。客户端应用程序之间不预期也不应共享 GC，因此写回缓存不会产生任何问题。应用程序在没有外部同步的情况下无法共享 GC。因此，强烈不建议应用程序之间共享 GC。

要设置 GC 的属性，请设置 `XValues` 结构中相应的成员，并在调用 `XCreateGC` 时对相应的值掩码位进行位或（OR）操作。值掩码位符号和 `XValues` 结构符号如下：

```c
/* GC 属性掩码位 */
#define GCFunction (1L<<0)
#define GCPlaneMask (1L<<1)
#define GCForeground (1L<<2)
#define GCBackground (1L<<3)
#define GCLineWidth (1L<<4)
#define GCLineStyle (1L<<5)
#define GCCapStyle (1L<<6)
#define GCJoinStyle (1L<<7)
```

## 图形上下文函数

```c
#define GCFillStyle (1L<<8)
#define GCFillRule (1L<<9)
#define GCStyle (1L<<10)
#define GCStyle (1L<<11)
#define GCStilepXOrigin (1L<<12)
#define GCStilepYOrigin (1L<<13)
#define GCFont (1L<<14)
#define GCSubwindowMode (1L<<15)
#define GGraphicsExposures (1L<<16)
#define GCClipXOrigin (1L<<17)
#define GCClipOrigin (1L<<18)
#define GCClipMask (1L<<19)
#define GCDashOffset (1L<<20)
#define GCDashlist (1L<<21)
#define GArcMode (1L<<22)
```

```c
/* Values */
typedef struct {
    int function;
    unsigned long plane_mask;
    unsigned long foreground;
    unsigned long background;
    int line_width;
    int line_style;
    int cap_style;
    int join_style;
    int fill_style;
    int fill_rule;
    int arc_mode;
    Pixmap tile;
    Pixmap style;
    int ts_x_origin;
    int ts_y_origin;
    int font;
    int subwindow_mode;
    Bool graphics_exposures;
    int clip_x_origin;
    int clip_y_origin;
    Pixmap clip_mask;
    int dash_offset;
    char dashes;
} XGCValues;
```

```c
/* 逻辑运算 */
/* 平面掩码 */
/* 前景像素 */
/* 背景像素 */
/* 线宽（像素单位） */
/* 实线, 虚线, 双虚线 */
/* 圆端, 平端, 折线端 */
/* 直角连接, 圆角连接 */
```

## 图形上下文函数

或者边界立即位于下方（y 轴增加方向），边界的内部立即位于右侧（x 轴增加方向）。

细线（零宽度）是使用未指定的、依赖于设备的算法绘制的单像素宽的线。该算法只有两个限制：

- 如果一条线从 `[x1,y1]` 到 `[x2,y2]` 在未裁剪的情况下被绘制，且另一条线从 `[x1+dx,y1+dy]` 到 `[x2+dx,y2+dy]` 在未裁剪的情况下被绘制，那么只有当点 `[x+dx,y+dy]` 被绘制的第二条线触及时，点 `[x,y]` 才会被绘制的第一条线触及。
- 组成直线的有效点集不能受裁剪影响。也就是说，裁剪后的线中的某个点被触及，当且仅当该点位于裁剪区域内部，且在未裁剪的情况下绘制时会被该线触及。

从 `[x1,y1]` 到 `[x2,y2]` 的宽线绘制绘制的像素与从 `[x2,y2]` 到 `[x1,y1]` 的宽线绘制始终相同（不考虑端点样式和连接样式）。建议此属性也适用于细线，但并非强制要求。宽度为零的线所绘制的像素可能与宽度为一的线不同。这允许使用许多制造商的线条绘制硬件，这些硬件的运行速度可能比更精确的宽线快得多。

通常情况下，绘制细线会比绘制宽度为 1 的宽线快。然而，由于绘制算法不同，细线在审美上可能与线条混合不协调。如果希望在所有显示器上获得精确且均匀的结果，客户端应始终使用宽度为一的线而不是宽度为零。

线样式（line-style）定义了线的哪些部分被绘制：

- `LineSolid`（实线）：绘制线的完整路径。
- `LineDoubleDash`（双点虚线）：绘制线的完整路径，但偶数虚线的填充方式与奇数虚线不同（见填充样式 fill-style），并在偶、奇数虚线交汇处使用 `CapBut`。
- `LineOnOffDash`（点空虚线）：仅绘制偶数虚线，且端点样式适用于所有单个虚线的内部末端，但 `CapNotLast` 被视为 `CapBut`。

端点样式（cap-style）定义了线的端点如何被绘制：

- `CapNotLast`（非末端端）：这等同于 `CapBut`，但在宽度为零时，最后一个端点不绘制。
