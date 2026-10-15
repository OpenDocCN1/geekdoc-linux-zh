
```
00:00.0 Host bridge: Intel Corp. 82845 845 (Brookdale) Chipset Bridge (rev 05)
00:01.0 PCI bridge: Intel Corp. 82845 845 (Brookdale) Chipset AGP Bridge (rev 05)
00:1d.0 USB controller: Intel Corp. 82801CA/CAM USB (Hub #1) (rev 02)
00:1d.1 USB controller: Intel Corp. 82801CA/CAM USB (Hub #2) (rev 02)
00:1e.0 PCI bridge: Intel Corp. 82801AM/CAM PCI Bridge (rev 42)
00:1f.0 ISA bridge: Intel Corp. 82801CAM ISA Bridge (LPC) (rev 02)
00:1f.1 IDE interface: Intel Corp. 82801CAM IDE U100 (rev 02)
00:1f.3 SMBus: Intel Corp. 82801CA/CAM SMB (rev 02)
00:1f.5 Multimedia audio controller: Intel Corp. 82801CA/CAM AC'97 Audio (rev 02)
00:1f.6 Modem: Intel Corp. 82801CA/CAM AC'97 Modem (rev 02)
01:00.0 VGA compatible controller: NVIDIA NV11 [GeForce 2] (rev 01)
02:01.0 Ethernet controller: 3Com Corporation 3c905C-TX/TM [Tornado] (rev 78)
02:04.0 CardBus bridge: 02 Micro, Inc. OZ26912 Cardbus Controller
```

输出的第一部分显示了 PCI 设备的总 ID。在这种情况下，ID `01:00.0` 指显卡。因此，`BusID` 行应该是：

```
BusID      "PCI:01:00:00"
```

## 理解 Monitor 节

`Monitor` 节列出了显示器的技术规格：水平同步（水平同步）频率和垂直刷新率。你可以从显示器手册中获得这两个值。

![](img/b418dfc0d37b54b9876d5e801170c507_127_0.png)

# 第 3 章：X Window 系统设置

水平同步信号发生在每一行扫描线的结束处；此信号将电子束从一行的末尾移动到下一行扫描线的开始。水平同步频率本质上是显示器每秒在显示屏幕上跟踪扫描线的次数。如果显示器能够显示 480 行（640x480 分辨率），并且每秒重绘屏幕 72 次（垂直刷新率为 72 Hz），则水平同步频率至少为每 480 x 72 = 34560 次/秒 = 34560 Hz = 34.56 kHz。实际值会更高，因为显示器始终必须追踪比显示更多的行数。

在指定水平同步和垂直刷新率的值时必须非常小心，因为 X 服务器使用这些值来选择从显卡发送的信号。如果显卡发送的信号超出显示器的规格，显示器可能会物理损坏。

大多数显示器都是多同步的，支持一个范围内的水平同步频率（而不是固定的频率）。如果你有显示器的说明书，可以指定显示器支持的水平同步频率范围。

显示器（`Monitor`）部分可能还包含 `ModeLines`，它定义了适用于显示器的视频模式。通常，X 服务器内部定义了一组 VESA 标准视频模式，因此对于大多数显示器，不需要在 `Monitor` 部分中显式定义任何视频模式。

以下是一个典型的 `Monitor` 部分（显示了视频模式规格的格式）：

```
Section "Monitor"
  Identifier "Monitor0"
  Vendor "Monitor Vendor"
  Model "Monitor Model"
  HorSync 30.0-69.0
  VertRefresh 55.0-120.0
EndSection
```

## 模式可以用两种格式指定。一种是紧凑单行格式，另一种是多行格式。

### 以下两种是等效的

```
#ModeLine "1024x768*" 45 1024 1048 1028 1264 768 776 784 817 Interlace

# Mode "1024x768"
# DotClock 45
# HTimings 1024 1048 1028 1264
# VTimings 768 776 784 817
# Flags "Interlace"
# EndMode
```

`Monitor` 部分的 `Identifier` 字段用于引用此显示器。你应该根据显示器说明书中的信息填充 `Screen` 部分的 `HorizSync` 和 `VertRefresh` 行。

## 计算 ModeLine

虽然你可以直接使用于在 XFree86 4.2.0 服务器中定义的 VESA 标准视频模式，但有时你可能需要手动添加 `ModeLine` 才能使视频模式在特定的视频/显示器组合上工作。

你使用以下语法在单行中指定 `ModeLine`：

```
ModeLine "name" CLK HRES HSS HTOT VRES VSS VTOT flags
```

你必须填写所有参数，最后一个参数除外，它是一个可选的关键字，表示模式的类型。例如，`flags` 字段可以是 `Interlace`（隔行扫描模式，在图像时间内交替绘制行）或 `DoubleScan`（每条扫描线加倍）。其他标志表示同步信号的极性。根据你指定的极性，值可以是 `+HSync`、`-HSync`、`+VSync` 或 `-VSync`。

`ModeLine` 上的参数具有以下含义：

- `"name"`: 模式名称，用双引号括起来。模式的分辨率用作名称。因此，你会看到如 `"640x480"` 和 `"1024x768"` 这样的模式名称。这些模式名用于 `Screen` 部分的 `Display` subsection。

- `CLK`: 用于此模式的时钟频率。对于具有固定点点数的显卡，时钟应该是 `XF86Config` 文件 `Device` 部分中的 `Clocks` 之一。

- `HRES` `HTOT`: 计时参数。`HRES` 是扫描线上可见像素数量的水平分辨率。如图 3-1 所示，扫描线的实际像素数超过了可见像素数。`HTOT` 是扫描线的总像素数。`HSS` 是水平同步信号开始的地方，`HSE` 是水平同步结束的地方。水平同步信号将电子束从一行移动到下一行。对于 640x480 模式，这四个参数为 640 720 864。这组数字表示扫描线上有640 个可见像素，水平同步从像素 680 开始，在像素 864 结束。

- `VRES` `VSS` `VTOT`: 垂直参数。`VRES` 是显示屏扫描线数量的垂直分辨率。如图 3-1 所示，扫描线的实际数量超过了可见扫描线数量。`VTOT` 是总扫描线。`VSS` 是垂直同步信号开始的行数，`VSE` 是垂直同步结束的行数。垂直同步信号将电子束从屏幕底部移动到第一行。对于 640x480 模式，这四个参数为 640 488 521。

从显示器的说明书中获取两个关键参数：垂直刷新率（Hz）和同步频率（kHz）。显示器说明书提供了这两个值的范围。垂直刷新率通常为 50 Hz 到 90 Hz；同步频率可以在 30 kHz 到 135 kHz 之间。以下是定义 `ModeLine` 上点时钟与水平垂直参数关系的两个方程：

```
CLK = RR * HTOT
CLK = HSF * VTOT
```

在这些方程中，`RR` 是显示器刷新率范围内的，`HSF` 是显示器支持的扫描频率。应用这些公式时，记得将所有值转换为通用单位（例如，确保均为 Hz）。

要定义一个模式，可以从理想的刷新率（`RR`）如 72 Hz 开始。对于给定的点钟，你可以从第一个方程计算出 `HTOT * VTOT`。接下来，在显示器支持的扫描频率范围内输入 `HSF` 值。因为点钟已经已知，你可以从第二个方程计算出 `HTOT`。知道 `HTOT` 后，你可以确定 `VTOT`，因为你已经计算出了 `HTOT * VTOT`。

此时，你知道了 `HTOT` 和 `VTOT`。你需要为 `ModeLine` 选择参数 `HSS`、`HSE`、`VSS` 和 `VSE`。的是，确定这四个参数需要尝试。你可以先选择 `HRES` 和 `VRES` 值（模式的分辨率）。然后在 `HRES` 和 `HTOT` 之间选择 `HSS` 和 `HSE`，确保 `HSS > HSE`。同样，`VSS` 和 `VSE` 应在 `VRES` 和 `VTOT` 之间；确保 `VSE > VSS`。

如果显示区域太小或未居中，必须更改 `HSS`、`HSE`、`VSS` 和 `VSE` 的值来调整显示。修复任何细微显示问题的方法之一是运行 XFree86 带的 `xsync`。如果你的显示正常但不符合预期（例如没有填充屏幕或偏向一侧），在终端窗口输入 `xsync`。程序会在终端打印几行关于显示器的信息。`xsync` 窗口和对话框出现。对话框（见图 3-8）显示使用 `xsync` 可能会损坏显示器和显卡的警告。
