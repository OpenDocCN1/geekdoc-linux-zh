
## 这是一个注释

Section "SectionName"

EntryName Value

...

Subsection "SubsectionName"

EntryName Value

...

EndSubsection

EndSection

## 第 3 章：X Window 系统设置

`xorg.conf` 中的三个部分涉及显卡和显示器：

- `Screen`（屏幕）部分将显卡、显示器与 X 服务器用于屏幕的视频模式结合在一起。每个 `Screen` 部分包含多个 `Display`（显示）子部分——每个子部分对应一种深度（depth）和显示模式。如果系统有多个显示器，该配置可以包含多个 `Screen` 部分，每个部分对应一个显示屏幕。
- `Device`（设备）部分列出了显卡（也称为图形设备）的特性，以及 X.Org X11 使用该显卡所需的驱动程序。如果系统有多个显卡，配置文件可以包含多个 `Device` 部分，每个部分对应一个显卡。
- `Monitor`（显示器）部分列出了显示器的技术规格，特别是水平和垂直同步率。

正如你在本章前面的部分学到的，你可以通过运行 `system-config-display` 实用程序来创建 `xorg.conf` 文件。如果 `system-config` 正确检测到了你的显卡和显示器，生成的 `xorg.conf` 文件可能可以直接工作。通常，当你尝试使用高级显卡的全部功能时，会遇到一些问题。

### 理解 Screen 部分

X 服务器根据 `Screen` 部分来确定显卡和显示器的设置。`Screen` 部分指定了构成此屏幕的 `Device`（显卡）和 `Monitor`（显示器）的名称。以下是典型的 `xorg.conf` 文件中的一个 `Screen` 部分：

```
Section "Screen"

Identifier "Screen0"

Device "Videocard0"

Monitor "Monitor0"

DefaultDepth 24

Subsection "Display"

ViewPort 0 0

Virtual 1024 768

Depth 16

Modes "800x600" "640x480"

EndSubsection

Subsection "Display"

ViewPort 0 0

Depth 24

Modes "1024x768" "800x600" "640x480"

EndSubsection

... other Display subsections ...

EndSection
```

注释行以井号 (`#`) 开头。该部分的定义包含在 `Section ... End` 块中。

### 第一部分：安装 Linux

`Identifier`（标识符）为此屏幕命名。该名称用于在 `ServerLayout` 部分中引用该屏幕。在 `Device` 和 `Monitor` 名称之后是若干个 `Display` 部分。每个 `Display` 子部分适用于一个特定的 `Depth`（每个像素的比特数，它决定了同时可以显示的颜色数量）。

X 服务器会自动使用 `Screen` 定义中的第一个 `Display` 子部分，但你可以使用指定不同 `Depth` 的命令行选项来启动服务器。通过在 `/etc/X11/gdm/gdm.conf` 文件的 `[Servers]` 部分包含以下行，你可以以 24 深度启动 X 服务器：

```
0=/usr/bin/X11/X -bpp 24
```

X 服务器的 `-bpp` 选项代表每像素比特数（bits per pixel），与 `Depth` 相同。只要显卡和显示器能够支持相应的深度，选择一个 `Depth` 值就是可行的。你可以通过 `Screen` 部分中的 `DefaultDepth` 条目指定默认深度。

`Display` 子部分中的 `Modes` 列出了你的显示器和显卡可以支持的视频模式名称。在 `xorg.conf` 文件的 `Monitor` 部分中存储了这些模式的信息。

对于显卡，如果显卡的内存空间比存储特定模式下所有可见像素信息所需的内存要多，X 服务器可以使用剩余内存创建一个比视频模式指定的 640 × 480 或 1024 × 768 大得像素区域。换句话说，`Virtual` 行表示此虚拟屏幕的大小，而 `ViewPort` 则指定虚拟屏幕的哪个部分映射到物理显示器。

### 理解 Device 部分

`xorg.conf` 文件的 `Device` 部分提供了有关显卡的信息。对于基于 nvidia GeForce 2 Go 芯片的显卡，`xorg.conf` 中的 `Device` 部分如下所示：

```
Section "Device"

Identifier "Videocard"

Driver "nv"

Vendor "Videocard vendor"

Name "nvidia GeForce 2 Go"

EndSection
```

该部分中的每行都提供了关于显卡的某些信息。在这种情况下，`Identifier` 是分配给此显卡的名称；该标识符在 `Screen` 部分中用于引用此特定的显卡。如果信息可用，`VendorName` 和 `BoardName` 会标识显卡。

对于没有可编程点时钟（dot clock）的旧显卡，`Device` 部分中非常重要的一行是 `Clocks` 行。该行中的值表示显卡支持的点时钟频率。一个典型的 `Clocks` 行如下：

```
Clocks 25,2 28,3
```

如今，大多数显卡不再需要 `Clocks` 行，因为它们具有可编程点时钟。除了 `Clocks` 行外，你还可以针对 `Device` 部分中指定的显卡类型为 X 服务器指定一个或多个标志位（flags）。

如果你的 PC 有多块显卡，你还需要在 `xorg.conf` 文件的 `Device` 部分中包含一个 `BusID`，标识该特定显卡在总线上的位置。对于 PCI 显卡，请使用 `lspci` 命令来查找此信息。例如，以下是输出：

## 第3章：X Window 系统设置

显示器部分的 `Identifier` 为显示器提供了一个名称；该名称在 `Screen` 部分中用于引用该显示器。你应该根据显示器手册的信息填充 `HorizSync` 行。

### 计算 ModelLine

虽然你可以使用服务器中定义的 VESA 标准视频模式，但有时可能需要手动添加 `ModelLine` 以使特定的视频模式工作。

你通过以下语法在单行上指定 `ModelLine`：

```
ModelLine "name" CLK HRES HSE HTOT VRES VSE TOT
```

你必须填写所有参数，除了最后一个参数，它是一个指示模式类型的可选关键字。`flags` 字段可以是 `Interlace`（隔行扫描，通过交替绘制）或 `Double`（双行扫描，每行绘制两次）。其他标志指示同步信号的极性。值为 `+HSync`、`+VSync` 或 `-VSync`，取决于你指定的极性。

`ModelLine` 上的参数含义如下：

- `name`: 该模式的名称，用双引号括起来。模式的分辨率用作其名称。你将使用 "640 x 480" 和 "1024 x 768" 等模式名称。这些名称用于 `Screen` 的 `Display` 子部分。
- `CLK`: 用于此模式的点钟频率。对于一组点钟频率的视频，点钟频率应该是 `xorg.conf` 文件中 `Device` 部分的数值。
- `HRES HSE HTOT`: 水平计时参数。`HRES` 是相对于扫描行像素数的水平分辨率。如图 3-1 所示，扫描行的实际像素数超过可见像素数，`HTOT` 是总像素数。`HSE` 是水平同步信号开始的像素位置，HSync 信号将电子束移动到下一行。对于 640x480 视频模式，这四个参数可能是 640 720 864，但 840 是可见的。水平同步信号在像素 680 和 864 处开始。
- `VRES VSE TOT`: 垂直计时参数。`VRES` 是相对于扫描行数的垂直分辨率。如图 3-1 所示，`TOT` 是扫描行的总数。`VSE` 是垂直同步信号开始的行数，`VSE` 是垂直同步信号结束的行数。垂直同步信号将电子束从屏幕底部移动到第一行。对于 640x480 视频模式，这四个参数可能是 480 498 521。

### 第一部分：设置 Linux

从显示器手册中，你可以获得两个参数：垂直刷新率（单位为 Hz）和水平同步频率（单位为 kHz）。显示器提供这两个值的有效范围。垂直刷新率通常在 50 Hz 到 90 Hz 之间，水平同步频率可以从 30 kHz 到 135 kHz 不等。以下是两个定义点钟与 `ModelLine` 上水平和垂直计时参数之间关系的方程：

```
CLK = RR * HTOT = TOT

CLK = HSF * VTOT
```
