
对于罗技鼠标，你可能会使用 `BusMouse`（如果是总线鼠标）；对于串行鼠标，你可能会使用 `Microsoft` 或 `Mouseman` 协议，而不是显而见的 `Logitech` 协议。如果你的鼠标连接到 PS/2 端口，请使用 PS/2 协议。（如果你使用的是来自戴尔 `Dell` 等大众零售商的较新系统，请检查鼠标端口。许多新系统配备了 PS/2 鼠标端口，但它们并不总是 PS/2 端口；例如，戴尔称之为鼠标端口。

`Xqueue` 协议仅在你设置键盘、鼠标时使用。我们不建议使用它。`OSMouse` 仅用于 SCO UNIX，不适用于 Linux。

在我们的情况下，鼠标连接到一号串口，在 DOS 术语中通常称为 `com1`。在真正的 UNIX Tradition 中，Linux 从 0 开始计数串口。为了指定鼠标连接到 `com1`，我们使用设备名称 `/dev/tty0`，这是该端口的 Linux 设备文件。我们在表 3.10 中列出了常用的端口。

## 表 3.10 Linux 中常用的串行端口

| 端口 (Port) | Linux 中的设备文件名 (Device File Name in Linux) |
|---|---|
| `com1` | `/dev/tty0` |
| `com2` | `/dev/tty1` |
| `com3` | `/dev/tty2` |
| `com4` | `/dev/tty3` |

你的系统可能为鼠标端口设置了 `/dev/mouse` 设备文件。无论你选择哪个设备文件，鼠标必须预先存在。（在我们系统上，`/dev/mouse` 是指向 `/dev/tty0` 的链接。）

总线鼠标设备文件列在表 3.11 中。

## 表 3.11 总线鼠标设备名称

| 设备 (Device) | 用途 (Usage) |
|---|---|
| `/dev/atim` | ATI 总线鼠标 |
| `/dev/logbm` | 罗技总线鼠标 |
| `/dev/inportbm` | 微软总线鼠标 |
| `/dev/psaux` | PS/2 或 Quickport 鼠标 |

注意，除了 `/dev/psaux` PS/2 鼠标，所有总线鼠标都应该使用 `busmouse` 协议。`Pointer` 部分还有几个选项，但最好保持原样。（为了在 X 中获得最佳结果，你需要三键鼠标。我们通常不设置波特率。当我们尝试过，并没有作用。如果你这样做，`Ctrl-Alt-Backspace` 序列很有用。）

### 表 3.12 Pointer 部分选项

| 选项 (Option) | 用途 (Usage) |
| --- | --- |
| `BaudRate` | 指定串行鼠标的波特率 |
| `EmulateButtons` | 允许双键鼠标像三键鼠标一样工作；通过同时按下来模拟第三键 |
| `ChordMiddle` | 修复某些罗技鼠标的问题 |
| `SampleRate` | 修复某些 Mouseman 鼠标的问题 |
| `ClearDTR` | MouseSystems 模式双协议鼠标需要 |
| `ClearRTS` | MouseSystems 模式双协议鼠标可能 |

### 配置显示器部分 (Monitor Section)

`Monitor` 部分向 X 显示器。你可以在 `XF8Config` 文件中定义多个显示器，每个 `Monitor` 部分都有名称。`Screen` 部分（后文讨论）将显示器连接到显卡。例如，以下条目定义了 `MultiSync XE17`：

```
Section "Monitor"
Identifier "NEC MultiSync XE17"
VendorName "NEC"
Model "MultiSync 4FG"
HorizSync 31.5
VertRefresh 55-120
ModeLine "640x480" 31 640 680 704 832 480 489 492 520
ModeLine "800x600" 50 800 864 976 1040 600 637 647 666
ModeLine "1024x768" 81 1024 1068 1024 1326 776 778 782 807
EndSection
```

对于每个显示器，你需要定义表 3.13 中列出的项。

| 项目 (Item) | 用途 (Usage) |
| --- | --- |
| `Identifier string` | 用于后续标识显示器 |
| `VendorName string` | 用于参考 |
| `ModelName string` | 用于参考 |
| `Bandwidth` | 显示器的带宽，单位为 MHz |
| `HorizSync range` | 水平同步频率，单位为 kHz |
| `VertRefresh range` | 垂直刷新范围，单位为 Hz |
| `Gamma value` | 显示器的 Gamma 校正 |
| `Modeline values` | 单一分辨率模式 |

`identifier` 是用于后续引用显示器的字符串。你可以在 `XF8Config` 文件中定义多个显示器。`HorizSync` 范围描述显示器的水平同步频率。对于多同步显示器，它可以是一个逗号分隔的值列表或范围，例如 `42-65`。你应该从显示器文档中获取此值（你可以在那里找到所需的大部分信息）。`Modeline` 的格式为：

`Modeline "name"水平值垂直值`

例如，以下设置了一个标准的 VGA 模式：

```
640x400 @ 70 Hz, 31.5 kHz hsync
Modeline "640x400" 25.175 640 664 760 800 400 409 411 450
```

可以有一组 `modeline` 值。你可以从 X 的 `probeonly` 模式或 XFree86 自带的文档获取。部分相关文档列在表 3.14 中。

### 表 3.14 XFree86 视频模式文档

| 文件 (File) | 用途 (Usage) |
| --- | --- |
| `VideoModes.doc` | 说明如何计算模式 |
| `modeDB.txt` | 显示器的 modeline 数据库 |
| `Monitors` | 显示器的 modeline 数据库 |

所有这些文件位于 `/usr/X11R6/lib/X11/doc`。以下是 `Monitors` 文件的条目：

```
#Date: Sat, 17 Sep 1994 00:50:57 -0400
#From: Erik Nygren <nygren@mit.edu>
Section "Monitor"
Identifier NEC MultiSync 4FGe
VendorName "NEC"
ModelName "MultiSync 4FGe"
BandWidth 80MHz
HorizSync 27-62KHZ 来自显示器文档
VertRefresh 55-90Hz
ModeLine 640x480 31 640 680 704 832 480 489 492 520
ModeLine 800x600 50 800 864 976 1040 600 637 647 666
ModeLine 1024x768 81 1024 1068 1024 1326 776 778 782 807
EndSection
```

我们拥有的显示器之一 `NEC MultiSync XE17` 不在 `modeDB.txt` 或 `Monitors` 文件中。我们在列表中找到了最接近的 `NEC MultiSync 4FGe`，并实验了那些 `Modelines`。尽管如此，在其他显示器上使用 `Modelines` 时要小心。如果不小心，可能会损坏你的显示器。

## 第 3 章：安装与配置 XFree86

### 显卡配置章节

`Device` 部分向 X 描述你的显卡。例如，一个标准的 Super VGA 设备显示如下：

```
### Standard VGA Device:
Device
  Identifier "Generic VGA"    VendorName "Unknown"
  BoardName "Unknown"
  Chipset "generic"
### VideoRam 256
### Clocks 25.2 28.3
EndSection
```

针对 Actix S3 加速卡，有一个更详细的设备部分如下：

```
### Device configured by xf86config:
Section "Device"
  Identifier "Actix GE32+ 2MB"
  VendorName "Actix"
  BoardName "GraphicsEngine Ultra"
#VideoRam 1024
#Option "dac_8_bit"
  Ramdac "att20c490"
  Clocks 25 28 40 72 50 77 36 45 90 120 80 110 65 75 95
EndSection
```
