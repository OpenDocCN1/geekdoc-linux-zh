

下面是一个设备段的示例，该段必须以 Identifier 条目开头：

```
Section "Device"
    Identifier "MagicGraph NM2160"
    VendorName "Unknown"
    BoardName "Unknown"
    VideoRam 2048
    Chipset "NM2160"
    IOBase 0xfea00000
    MemBase 0xfd000000
    DacSpeed 90
    Option "intern_disp"
EndSection
```

## 设备段条目

| 使用此条目 | 用于执行此操作 |
| :--- | :--- |
| **BIOSBase** *地址* | 如果视频 BIOS 的基础地址不是默认的 0xC0000，请指定其基础地址。 |
| **BoardName** *名称* | 指定图形适配器的名称。要查看支持的图形设备列表，请参见 X11 目录中的 /usr/lib/X11/Cards。 |
| **Chipset** *芯片组* | 如果服务器探测未能确定，请指定图形适配器使用的芯片组。 |
| **COPBase** *地址* | 指定协处理器的基础地址，某些服务器需要此项。请查阅服务器的文档。 |
| **DACBase** *地址* | 指定 DAC 的基础地址，某些服务器需要此项。请查阅服务器的文档。 |
| **Instance** *n* | 指示视频电路是否位于主板上，某些服务器需要此项。请查阅服务器的文档。 |
| **IOBase** *地址* | 指定视频 I/O 的基础地址，某些服务器需要此项。请查阅服务器的文档。 |
| **Option** *字符串* | 此可选条目允许用户选择驱动程序提供的特定选项。可以给出多个选项条目。选项字符串的支持值在相应的 X 服务器手册页或特定芯片组的 README 文件中给出。 |
| **POSBase** *地址* | 指定 POS 的基础地址，某些服务器需要此项。请查阅服务器的文档。 |
| **VendorName** *供应商* | 此可选条目指定图形设备的制造商。 |
| **VGBase** *地址* | 指定 VGA 内存的基础地址，某些服务器需要此项。请查阅服务器的文档。 |
| **VideoRam** *n* | 指定安装在适配器上的视频 RAM 数量（以 K 为单位），某些服务器需要此项。请查阅服务器的文档。 |

## 屏幕段

屏幕段将之前输入到监视器段和设备段中的规格整合在一起。它定义一个或多个 Display 子段，指定使用系统时可用的视频模式。

以下是屏幕段的示例：

```
Section  "Screen"
Driver     "accel"
Device     "MagicGraph  NM2160"
Monitor    "LCD  Panel 1024x768"
Subsection  "Display"
Depth  16
Modes  "800 x 600"
Viewport 0 0
Virtual  1024  786
EndSubsection  
Subsection "Display"  
Depth 16  
Modes "1024x768"  
ViewPort0 0  
EndSubsection  
EndSection
```

> **提示**  
> 如果您定义了多个 Display 子段，可以通过按 Ctrl + Alt + 数字键盘加号或 Ctrl + Alt + 数字键盘减号在视频模式之间切换。

## 屏幕段条目

| 使用此条目 | 用于执行此操作 |
| :--- | :--- |
| **Driver** *名称* | 开始一个屏幕段并指定驱动程序，该驱动程序对每个段必须是唯一的。可用的选项包括 Accel、Mono、SVGA、VGA2 和 VGA16。 |
| **BlankTime** *时间* | 设置屏幕保护程序空白状态的不活动时间（以分钟为单位）。默认为 10 分钟。 |
| **DefaultColorDepth** *深度* | 指定颜色深度。可用的选项为 8、16、24 和 32。 |
| **Depth** *深度* | 当存在多个 Display 子段时，指定默认颜色深度（8、16、24 或 32）。 |
| **Device** *描述* | 指定图形设备描述。 |
| **Monitor** *名称* | 指定监视器名称，该名称必须与监视器段中的名称匹配。 |
| **OffTime** *超时* | 设置 DPMS 模式的不活动超时时间（以分钟为单位）。默认为 40。 |
| **Option** *字符串* | 指定一个字符串以启用特定服务器提供的选项。详情请查阅服务器文档。 |
| **StandByTime** *超时* | 设置 DPMS 模式待机阶段的不活动超时时间（以分钟为单位）。默认为 20。 |
| **SuspendTime** *超时* | 设置 DPMS 模式挂起阶段的不活动超时时间（以分钟为单位）。默认为 30 分钟。 |
| **ViewPort** *x y* | 设置初始显示左上角的 x 和 y 坐标（以像素为单位）。仅当虚拟屏幕分辨率与初始视频模式的分辨率不同时使用。 |
| **Virtual** *x y* | 指定大于物理显示分辨率的虚拟屏幕分辨率。对于大多数彩色 X 服务器，x 和 y 必须是 8 或 16 的倍数；对于单色服务器，必须是 32 的倍数。 |
| **Visual** *类型* | 指定根视觉类型。可用的选项包括 StaticGray、GrayScale、StaticColor、PseudoColor、TrueColor 和 DirectColor。 |

## Xinput 段

* Xinput 段是可选的。它允许您定义某些输入设备，如摇杆和绘图板。下面的 Xinput 示例展示了摇杆的定义：

```
Section "XInput"
  SubSection "Joystick"
    Port "/dev/joY0"
    DeviceName "Joystick"
    TimeOut 10
    MinimumXPosition 100
    MaximumXPosition 1300
    MinimumYPosition 100
    MaximumYPosition 1100
    CenterX 700
    CenterY 600
    Delta 20
  EndSubSection
EndSection
```

要使用在此段中定义的设备，必须告知 X 服务器加载相应的模块。您可以通过 Modules 段中的条目来实现这一点，该段在前面已经讨论过。

下表讨论了用于定义摇杆子段的可使用条目。

## 摇杆子段选项

| 使用此条目 | 用于执行此操作 |
| :--- | :--- |
| **AlwaysCore** | 启用核心指针共享 |
| **CenterX** *值* | 设置摇杆空闲时的 X 轴中心 |
| **CenterY** *值* | 设置摇杆空闲时的 Y 轴中心 |
| **Delta** *值* | 设置最大值 |
| **DeviceName** *名称* | 指定设备名称 |
| **MaximumXPosition** *值* | 设置 X 轴最大值 |
| **MaximumYPosition** *值* | 设置 Y 轴最大值 |
| **MinimumXPosition** *值* | 设置 X 轴最小值 |
| **MinimumYPosition** *值* | 设置 Y 轴最小值 |
| **Port** *路径* | 指定设备驱动程序的路径 |
| **TimeOut** *超时* | 设置两次轮询设备驱动程序之间的时间间隔（以毫秒为单位） |

## XFree86 第 4 版

XFree 86 的最新版本即第 4 版，目前正在 Linux 发行版中提供，并在本书付印之际发布；未来版本将完整记录第 4 版的配置文件。本节重点介绍了从第 3.3 版到第 4 版的最重要变更：

- **单一二进制文件**：XFree86 的早期版本使用了多个独立的二进制文件，旨在适用于各种类的视频驱动程序和显示器。在第 4 版中，只有一个 XFree86 二进制文件；它被设计为与可加载模块协同工作，因此在更改视频驱动程序时无需卸载该二进制文件（随后安装不同的二进制文件）。
- **选项标志**：第 4 版更广泛地使用选项标志，通过在子段中键入 Option 一词后跟用引号括起来的名称来指定特定选项。某些选项还允许指定数值；同样，这些值必须用引号括起来。
- **模块段**：在此段中，不要使用 .so 扩展名来指定模块名称。务必加载 extmod 模块（`Load "extmod"`），该模块默认未加载但包含基本代码。TrueType 支持通过 `Load "freetype"` 启用。
- **键盘、指针和 Xinput 段**：这些段已组合到 InputDevice 段中。配置文件可以包含一个或多个 InputDevice 段，每个段通过选项标志定义给定的输入设备，如键盘或鼠标。
- **在启动时指定颜色深度**：旧的 `-bpp` 选项已被 `-depth n` 取代，其中 n 是所需的颜色深度（8、15、16 或 24）。

监视器段、设备段和屏幕段保持不变，仅有少数细微例外。关于 XF86 第 4 版的更多信息，请参见该程序的首页 http://www.xf86.org。

## 配置打印机

![](img/e85417bb52fc523c6fc7b3b77b124ecb_570_0.png)

您可能在安装 Linux 发行版时已经配置了打印机。大多数发行版现在都包含交互式引导您完成此过程的实用工具。如果您升级到新的打印机，则需要更改打印机设置。为此，最好使用发行版提供的打印机配置实用工具。例如，Red Hat 控制面板实用工具提供的 printtool。只有当您的发行版缺少打印机配置实用工具时，才应尝试手动配置打印机。

