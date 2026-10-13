
`FontPath`    "`usr/XF86Config/lib/X11/fonts/Type1`"

`FontPath`    "`usr/XF86Config/lib/X11/fonts/Speed2`"

`FontPath`    "`usr/XF86Config/lib/X11/fonts/75dpi/*`"

`FontPath`    "`usr/XF86Config/lib/X11/fonts/100dpi/*`"

```
要查看这些行是否正确，请查看列表 10.1 中提到的每个目录，查看它们是否有文件。如果这些目录是空的，说明你没有安装字体，或者它们可能在另一个位置。
```

# 键盘章节

你应该指定 `ServerLock`。这是为 XFree86 指定键盘的简单方法。否则，只需要手动设置那些为了国际支持所需的键盘修改。在典型的 `x86config` 文件中，此章节看起来像列表 10.2 所示。

## 列表 10.2. 键盘选择

```
Section "Keyboard"

AutoRepeat 0 5

ServerLock 1 2 3

# 要将 LeftAlt 设置为 Meta，RightAlt 设置为 ModeShift，
# 将 RightCtl 键设置为 Compose，将 ScrollLock 键设置为 ModeLock:

LeftAlt Meta

RightCtl Compose

ScrollLock ModeLock

EndSection
```

# 指针章节

指针章节是鼠标类型的名称。鼠标类型是鼠标使用的协议。例如，连接到 PS/2 端口的微软鼠标使用的是这些 PS/2 协议，而不是微软协议。

- 鼠标连接的设备类型：串口或总线。（通常你可以使用 `/dev/mouse`。）
- 你是否想使用国家键盘布局，或者你是否想运行通用的美国键位表。

> 注：原文文本后续存在大量重复乱码，译文已根据要求进行精简处理。

# 设置视频模式

这是最困难的部分。在开始之前，请阅读 `VideoModes.doc`。如果你正在使用 `x86config`（我强烈建议使用）且你的显示器不在数据库中，请选择通用模式并从那里开始创建你自己的模式。如果你没有 `x86config`，请阅读 `README.config` 文件中关于构建模式的教程。

> 注意
> 我知道整个章节都充满了警告。请不要惊慌。只需留心，并在执行每一步之前仔细阅读说明即可。

Free86 发行版包含一个实用的实用工具 `xvitune`，用于调优视频模式。由于系统没有对模式的可用性进行检查，因此在测试模式之前，你必须根据你显示器的规格对该模式进行检查。调优模式的第一行提供了有关该模式规格的信息。在测试该模式之前，你必须持续检查这些值是否在你的显示器的能力范围内。

请查看列表 10.5 获取 Free86 的常用视频模式。

## 列表 10.5. 视频模式

```
Section "Device"

Identifier "Generic VGA"

VendorName "Unknown"

BoardName "Unknown"

ChipSet "generic"

VideoRam 256

Clocks 25.2 28.3

EndSection
```

```
****************************************************************

# Screen sections

****************************************************************
```

```
# 颜色 SVGA 服务器
```

```
Section "Screen"

Driver "svga"

Device "Generic SVGA"

Monitor "Generic Monitor"

Subsection "Display"

Depth 8

Modes "640x480"

Viewport 0 0

Virtual 800 600

EndSubsection
```

```
# 16色 VGA 服务器
```

# X 窗口
第 10 章

```
Section "Screen"
Driver "vga16"
Device "Generic VGA"
Monitor "Generic Monitor"
Subsection "Display"
Modes "640x480"
ViewPort 0 0
Virtual 800 600
SubsectionEndSection
```

# 单色服务器

```
Section "Screen"
Driver "vga2"
Device "Generic VGA"
Monitor "Generic Monitor"
Subsection "Display"
Modes "640x480"
ViewPort 0 0
Virtual 800 600
SubsectionEndSection
```

视频部分中的模式最多可以包含 10 个值。修改这些值时务必非常小心，因为错误的设置可能会毁坏你的显示器！如果这些值不存在也没关系，因为可以使用默认值。覆盖显示器默认值的典型行如下：

`"640x480" 28 64 480 728 776 480 482 494`

按从左到右顺序的 10 个值显示在以下章节中。这些值对于视频工程师或那些必须处理未在默认模式定义的显示器的人来说才有意义。请检查你显示器的硬件规格，并从那里获取这些值来填充这十个参数。以下是需要设置的字段：

- 标签：屏幕分辨率的标签；例如 `640x480` 或 `1024x768`。
- 以 MHz 为单位的时钟频率。
- 水平显示结束（Horizontal Display End）：屏幕上每行可见像素数。
- 水平消隐起始值（Start Horizontal Retrace）：这指定了视频同步开始的脉冲数。
- 水平消隐值（Horizontal Retrace）：定义了同步脉冲的结束。
- 水平总值（Horizontal Total）：每行不可见和可见像素的总数。
- 垂直显示结束值（Vertical Display End）：屏幕上可见的行数。
- 垂直消隐起始值（Start Vertical Retrace）：同步脉冲开始前的行数。
- 垂直消隐值（Vertical Retrace）：同步脉冲结束时的行数。
- 垂直总值（Vertical Total）：屏幕上不可见和可见的行总数。

![](img/421e47878893966b6e8fcf1c1c761441_209_0.png)

## 配置其他服务器

多扫描（Multiscan）显示器处理 15 到 40 Hz 的频率。某些显示器以 72 Hz 的垂直扫描频率工作以防止闪烁。你必须能够根据显示器的规格计算频率并得出这些数字。一个很好的起点是关于如何获取这些值的 XFree86-HOWTO 文档。记住，你的视频显示器只是一个华丽的设备。你给它正确的值，就可以尝试。

# XFree86 的国际化键盘布局

XFree86 服务器能够从 Linux 内核读取键表

用于 `ModeShift` 修饰符的可配置按键为 `LeftAlt`、`RightAlt` (=Gr)、`Ctrl1` 和 `ScrollLock`。

通常使用 `AltGr` 键进行键盘的国际化修饰。若要让 XFree86 服务器从内核读取 `AltGr` 键表，你需要在 `.olwmrc` 文件中放入以下行：

```
"ModeShift"
```
