
## 描述
`XF86_S3` 是用于 S3 加速卡的 8 位伪色（PseudoColor）、16 位真色（TrueColor）服务器。请注意，并非所有 S3 加速卡都支持 16 位和 24 位操作。请参阅 `README.S3` 了解在哪些深度下支持哪些卡。

`XF86_Mach8` 是用于 ATI Mach8 加速卡的 8 位伪色服务器。

`XF86_Mach32` 是用于 ATI Mach32 显卡的 8 位伪色和 16 位真色服务器。注意，并非所有 Mach32 加速卡都支持 16 位操作。

`XF86_Mach64` 是用于 ATI Mach64 显卡的 8 位伪色、16 位真色和 24 位真色服务器。注意，RAMDAC 不支持 16 位和 24 位操作。请参阅 `README.Mach64` 了解在哪些深度下支持哪些 RAMDAC。

`XF86_P9000` 是用于 Weitek P9000 (P9000) 显卡的 8 位伪色、16 位真色和 24 位真色服务器。

`XF86_AGX` 是用于 AGX/XGA 显卡的 8 位伪色和 16 位真色服务器。

`XF86_W32` 是用于 ET4000/W32, ET4000/W32p 显卡的 8 位伪色服务器。

`XF86_8514` 是用于 8514/A 显卡的 8 位伪色服务器。

这些由带有 X11R5 的 X386 服务器衍生而来，由 Kevin Martin (+martin.nc.edu) 免费提供

## 配置
服务器支持以下芯片组：

| 芯片组 | 详情 |
| :--- | :--- |
| FX8_S3 | 86C911, 86C924, 86C801, 86C805, 86C85I, 86C928 - P, 86C732 (Trio32), 86C674 (Trio64), 86C864, 86C964, 86C968 |
| FX8_Mach8 | ATI Mach8, ATI Mach32 |
| FX8_Mach32 | ATI32 |
| FX8_Mach64 | Mach64 |
| FX8_P9000 | Diamond Viper V8, Diamond Viper PCI1, Orchid P9000, 以及某些克隆 (Weitek P9000) |
| FX8_AGX | GX-01, AGX-04, AGX-05, AGX-06, GX-A1, GX-2 |
| FX8_W32 | ET4000/I31, ET4000/W32p |
| FX8_8514 | 8514/A 及真正的克隆 |
| IBM | 真正的克隆 |

对于 S3，支持高达（大约）1,152×800 的虚拟分辨率，使用（最多）1MB 的显示内存（S3 芯片的新版本使用内部宽度 1280，因此 1MB 无法支持 1152×900）。使用 2MB 或更多显示内存可以实现 1280x1024 的虚拟分辨率（某些卡为 1600x1280）。虚拟分辨率取决于内存量，最大虚拟宽度为 2048，最大虚拟高度为 4096。

Mach64 支持类似的分辨率。请参阅 `README.Mach64` 详情。

Mach32 支持类似的分辨率。对于 Mach32，最大虚拟宽度为 1536，最大虚拟高度为 1280。

对于 Mach8，最大虚拟宽度为 1024。
对于 8514，最大分辨率为 1024×768。

对于 AGX 芯片，最大分辨率取决于芯片版本和可用显示内存。请参阅 `README.agx` 详情。

P9000，在足够的内存情况下，虚拟分辨率可以达到 1280x1024。所有服务器都支持 24 位色。

## 选项
除了在 `Xf86(1)` 中描述的选项外，这些服务器还接受某些开关。

Mach64, Mach32, S3, P9000 和 AGX 服务器支持 16 位色。Mach64, S3, P9000 和 AGX 服务器支持 24 位色。对于 32 位色，只有 S3 支持。

### 设置
在 `Xf86(1)` 中描述的选项外，这些服务器还接受某些开关。在足够的内存情况下，虚拟分辨率可以达到 1280x1024。请参阅 `xf86config(4)` 了解关于 S3, Mach32, Mach64, P9000, AGX, W32, 8514 的设置。

对于带有编程时钟的板，可以在这里指定时钟（见下 S3 芯片组的设置）。

时钟芯片类型
对于带有编程时钟的板，给出时钟名称。可能值包括：
S3 映射驱动的：
S228 驱动的：
828
8222
I/O 映射的：
732
674
864
968
Mach8 驱动的：
Mach32
Mach64
P9000 驱动的：
viperlb
viperci
AGX 驱动的：
016
015
014
010
xga

S3 服务器包括“28061a,2981f,23c584,sc14112,s3endam,s3sdac,38025,31026,2595,5300,5352,38931,stg1793,and_itb_rgb655

RAMDAC 类型
板上使用的这种类型的 RAMDAC。S3、AGX 和 W32 服务器使用此：
正常-(S3, AGX) 在此处不推荐。此选项仅供 S3 服务器在错误检测到这些其他 RAMDAC 时使用。AGX 服务器不自动检测 RAMDAC，这是未指定 RAMDAC 时的默认值。

通用-(W32) 强制 W32 服务器将 RAMDAC 视为通用 VGA RAMDAC。
At20c490-(S3, AGX) 用于 AT&T 20C490 或 AT&T20C491 RAMDAC。当指定 `de_8bit` 选项时，这些 RAMDAC 可以以 8 位 RGB 模式运行。它还允许使用 801/805/928 字节进行16bpp 操作。真正的 AT&T 20C490 RAMDAC 必须由 S3 服务器自动检测。这种 RAMDAC 必须在它的案例中显式指定。

### 第一部分：用户命令

- SC15025—(S3, AGX) 显卡带有 Sierra SC15025 或 SC15026 RAMDAC。S3 服务器代码可自动检测此 RAMDAC。

- SC11482—(S3) 显卡带有 Sierra SC11482、SC11483 或 SC11484 RAMDAC。S3 服务器代码可自动检测此 RAMDAC。

- SC11485—(S3) 显卡带有 Sierra SC11485 或 SC11489 RAMDAC。S3 服务器会将这些 RAMDAC 识别为 sc11482，因此必须指定此选项以利用额外功能（它们支持 16pp、15pp 和 8pp，而其他仅支持 15pp 和 8pp）。

- BT8485—(S3) 显卡带有 TreeBook BT8485 或 BT9485 RAMDAC。如果服务器未能检测到它，则必须指定此项。

- AT20C55—(S3) 显卡带有 AT&T 20C05 RAMDAC。如果服务器未能检测到 20C05，或者显卡带有 BT9485 RAMDAC 且在使用高于 67.5MHz 的频率时出现问题，则必须指定此项。

- AT20C48—(S3) 显卡带有 AT&T 20C48 或 21C48 RAMDAC。如果服务器未能检测到它，则必须指定此项。

- AT22C49—(S3) 显卡带有 AT&T 22C49 RAMDAC。如果服务器未能检测到它，则必须指定此项。

- IBM RGB5154—(S3) 显卡带有 IBM RGB5154 RAMDAC。如果服务器未能检测到它，则必须指定此项。

- IBM RGB5224—(S3) 显卡带有 IBM RGB5224 RAMDAC。如果服务器未能检测到它，则必须指定此项。

- IBM RGB625—(S3) 显卡带有 IBM RGB625 RAMDAC。如果服务器未能检测到它，则必须指定此项。

- IBM RGB5288—(S3) 显卡带有 IBM RGB5288 RAMDAC。如果服务器未能检测到它，则必须指定此项。

- ST1798—(S3) 显卡带有 ST1798 RAMDAC。如果服务器未能检测到它，则必须指定此项。

- ST17183—(S3) 显卡带有 ST17183 RAMDAC。此 RAMDAC 不支持 8 位 RGB 模式（当你指定 `dac_8_bit` 选项时）。它允许 801/805 板卡进行 16pp 操作。目前没有 RAMDAC 的自动检测。

- S3_dac—(S3) 显卡带有 S3 86C716 SDAC RAMDAC。如果服务器未能检测到它，则必须指定此项。

- ICS5300—(S3) 显卡带有 ICS5300 RAMDAC。如果服务器未能检测到它，则必须指定此项（服务器将将其识别为 S3 GENAC，这是可以）。

- ICS54342—(S3) 显卡带有 ICS54342 RAMDAC。如果服务器未能检测到它，则必须指定此项（服务器将将其识别为 S3 GENAC，这是可以）。

- TI30020—(S3) 显卡带有 TI ViewPoint Ti30020 RAMDAC。如果服务器未能检测到 Ti30020，则必须指定此项。注意，如果任何模式需要高于 70MHz 的点时钟，则此 RAMDAC 将使用像素复用。

# x86_Accel

- TI3025—(S3) 显卡带有 TI ViewPoint TI3025 RAMDAC。如果服务器未能检测到 TI3025，则必须指定此项。

- TI3026—(S3) 显卡带有 TI ViewPoint TI3026 RAMDAC。如果服务器未能检测到 TI3026，则必须指定此项。

- Bt4481—(AGX) 显卡带有 BrookTree Bt481 RAMDAC。

- Bt4482—(AGX) 显卡带有 BrookTree Bt482 RAMDAC。

- Here_dual_dac—(AGX) 显卡（Hercules Graphite Pro）同时带有 44针（Bt485 和 AT&T2C055）和 44针（Bt481 或 Bt482）RAMDAC。

- Here_smal_dac—(AGX) 显卡（Hercules Graphite Pro）仅带有 44针（Bt481 或 Bt482）。

- 指定扩展 ID 的基地址。此项由 AGX 服务器和 P9000 使用。关于如何使用它的详情，请参考 RECHE 和 P9000。

- 指定线性缓冲区的硬线部分。此选项仅用于 P9000、S3、Mach64 和 Mach32（当使用线性缓冲区时）。对于 S3 服务器，硬线部分是地址的高 10 位（掩码为 0xFFFFFC00）。注意：对于整个缓冲区软件可选的 RAMDAC，不需要此项。此外，在 3.1 之前的版本中，S3 服务器使用地址的前 6 位，并与 0xC00000 取或。对于 Mach32 服务器，掩码为 0xC00000（PCI 显卡忽略此地址设置）。

- 此项在 P9000 服务器上必须指定。对于本地 Diamond Vipers，基地址可以是 0x800000、0xC000000 或 0xE00000。默认值为 0x800000。只要不与另一个设备冲突，任何值均可；至少对于 Viper PCI 请参考 RECHE 和 P9000。对于 Orchid，基地址可能是 0xC000000、0xC000000 或 0xE00000。注意：S3 服务器通常会自动探测此项。设置此选项将覆盖服务器使用线性缓冲区的问题。Mach64 服务器需要内存窗口。对于 ISA 显卡，这意味着必须启用窗口且窗口必须设置为小于 16MB（这意味着在 ISA 系统上，使用 Mach64 服务器必须拥有 12MB 或更少的内存）。通常，Mach64 服务器对该地址使用预定义值，但设置此选项将覆盖预定义地址。Mach32 服务器在正常情况下不需要使用此选项。

- COPBase—设置 AGX 服务器的协处理器基地址。详情参考 README。

- Instance—设置 AGX 服务器的 XGA 数量。详情参考 README。这允许指定显卡的内存值。这仅用于 805、864 和 Trio32/64 显卡，对于 S3 或 Trio64 显卡不应在此给出值。此条目不会更改显卡的内存频率，但用于计算 DRAM 参数。

- S3MClk—允许调整 DRAM 显卡的某些定时参数。详情参考 README.s3。单位为 MHz。

- S3NAdjustM—设置 S3 内存频率。

- S3RefClk—允许指定 PLL 参考。对于某些使用 IBM RGB55 RAMDAC 的显卡是必需。

选项标志可以在 "optionstring" 的 Device 部分或 Display 子部分中指定——允许用户选择驱动程序提供的选项。识别以下字符串：

- Nomemaccess—(S3) 禁用直接访问显存。此选项用于 864 和 964 芯片。

- Noacel—(AGX, 9000) 禁用 P9000 的硬件加速，并禁用 AGX 的缓存。

- Vram_128—(AGX, 9000) 当内存探测失败时，如果有 128k VRAM 则使用此项。

- Vram_256—(AGX, 9000) 当内存探测失败时，如果有 128k VRAM 则使用此项。

- Linear—(S3, and Math32) 禁用使用线性映射缓冲区。

- Ti3020_curs—(S3) 启用 Ti3020 的内部硬件光标。（默认）

- No_ti3020_curs—(S3) 禁用 Ti3020 的内部硬件光标。

- Sw_cursor—(S3, Math32, Mach64, P9000, AGX) 禁用硬件光标。

- Dat_6_bit—强制 6 位 RGB。这在 8 位模式被自动启用的情况下是必需的。对于带有 44针（Bt481 或 Bt482）RAMDAC 的显卡，在 S3 服务器上是默认设置的 6 位 RGB。适用于带有 44针（Bt485 和 AT&T2C055）的显卡。

- Sync_on_green—(S3, P9000) 在带有 Bt485 的显卡上产生绿色同步信号。

- Power_saver—(S3, and Mach64) 此选项开启了 VESA 的省电功能。

- intel_ga—(Mach32) 设置 Intel 显卡的硬线偏移。

### 第一部分：用户命令

- slow_vram-(S3) 为使用慢速 VRAM 的显卡调整 VRAM 序。某些 Diamond Stealth 64 VRAM 和 Hercules Terminator 64 显卡需要。
- Fast_vram-(S3) 调整 VRAM 序以实现更快的 VRAM 访问。如果你的显卡不支持，将会出现错误和像素花点。
- Slow_dram_refresh-(S3) 为具有慢速 DRAM 的显卡调整 DRAM 刷新，避免在切换模式时出现像素损坏行。
- No_block_write-(Mach64) 禁用特定类型 VRAM Mach64 显卡的块写入模式。如果屏幕上出现噪声或阴影，此选项可以将其消除。
- Block_write-(Mach64) 启用特定类型 VRAM Mach64 显卡的块写入模式。通常情况下，Mach64 服务器会自动判断显卡是否能处理块模式，但此选项将覆盖探测结果。
- No_clocks-(Mach64) Mach64 服务器通常从 bios 读取时钟。此选项将覆盖时钟并强制服务器使用 XF86Config 文件中的时钟。

AGX 服务器还有许多调优选项。详情请参阅 README。

注意，Free86 具有内部能力来确定运行的是什么硬件。因此，没有指定 chipset、clocks 和 videom 关键字。但在某些情况下，自动检测可能会失败（例如，在启动服务器时机器上负载过高）。对于此类情况，应先在未加载负载的机器上运行服务器，查看自动检测的结果（在服务器启动期间打印出来），然后在配置文件中显式指定这些参数。建议对所有参数，特别是 C6clock 值，进行

## 文件

- `<Xroot>/bin/XF86 S3`
- `<Xroot>/bin/XF86 Mach`
- `<Xroot>/bin/XF86 Mach32`
- `<Xroot>/bin/XF86 Mach64`
- `<Xroot>/bin/XF86 P9000`
- `<Xroot>/bin/XF86 AGX`
- `<Xroot>/bin/XF86 W32`
- `<Xroot>/bin/XF86 8514`
- `/etc/XF86Config`
- `<Xroot>/lib/X11/XF86Config`
- `<Xroot>/lib/X11/doc/README.agx`
- `<Xroot>/lib/X11/doc/README.P9000`
- `<Xroot>/lib/X11/doc/README.S3`
- `<Xroot>/lib/X11/doc/README.W32`

- 用于 S3 的 8 位、16 位和 24 位颜色服务器
- 用于 Mach 的 8 位颜色服务器
- 用于 Mach32 的 8 位和 16 位颜色服务器
- 用于 Mach64 的 8 位、16 位和 24 位颜色服务器
- 用于 P9000 的 8 位、16 位和 24 位颜色服务器
- 用于 AGX 和 XGA 的 8 位和 16 位颜色服务器
- 用于 ET4000/W32 的 8 位颜色服务器
- 用于 IBM 8514 及兼容显卡的 8 位颜色服务器
- 服务器配置文件
- 服务器配置文件（次要位置）
- AGX 服务器的额外文档
- P9000 服务器的额外文档
- S3 服务器的额外文档
- W32 服务器的额外文档

注意：`<Xroot>` 指 X11 安装根目录。

## 另见

`X(1)`, `Xserver(1)`, `XFree86(1)`, `XFree86Config(4/5)`, `xvdtune(1)`, `xdm(1)`, `xf86config(1)`, `xinit(1)`

## 作者

除了 XFree86 的作者外，以下人员对本文工作做出了主要贡献：Kevin Martin (martin@cs.nc.edu), John Toms (tombs@XFree86.org), Rik Faith (faith@cs.nc.edu)。（在整体工作期间，我们加速了服务器。）

David Dawes (dawes@XFree86.org), David Wexblatt (dexw@XFree86.org),（开发并将其工作合并到 XFree86。）

John Toms (tombs@XFree86.org), David Wexblatt (dexw@XFree86.org), David Dawes (dawes@XFree86.org), Amancio Hasty (hasty@cm.com), Robin Cowan (rotcin@xFree86.org), Northern Distler (norter.Distler@physik.tu-chen.de), Leonard N. Ziffner (zn@netflix.com), Harald Koenig (koenigpt@phys.uni-tuebingen.de), Bernhard Bender (brela@ms.compquare.com), Hans Nasten (nasten@neeverstay.com).（S3 特定代码的开发和改进。）

Kevin Martin (martin@cs.nc.edu), Rik Faith (faith@cs.nc.edu), Tiago Gons (tiago@comajsn.hobby.nl), Hans Nasten (nasten@neeverstay.com), Scott Laird (slaird@uchicago.edu).（Mach-8 和 4514/A 特定代码的开发。）

Kevin Martin (martin@cs.nc.edu), Rik Faith (faith@cs.nc.edu), Tiago Gons (tiago@comajsn.hobby.nl), Hans Nasten (nasten@neeverstay.com), Scott Laird (slaird@uchicago.edu).（Mach32 特定代码的开发。）

Kevin Martin (martin@cs.nc.edu), Rik Faith (faith@cs.nc.edu), Mike Benson (mike@ebsun.mlb), Mark Weaver (MarkWeaver@brome.edu).（此处原文重复）

Kevin Martin (martin@cs.nc.edu).（Mach6 特定代码的开发。）

Erik Nyberg (nygren@gmail.com), Harry Langbacher (harry@rayn.gov), Chris Mason (utchnosm@mail.isc), Harmsen (harmsen@reitel.se).（P900 特定代码的开发。）

Henry Worth (henryworth@amdahl.com).（AGX 特定代码的开发。）

Genn Lai (glenncs@utex.edu).（E7400/J32 特定代码的开发。）

## BUG

某些带有 et485 的显卡连接到 85MHz 以外的时钟。P900 服务器在 VGA 模式下可能与 Diamond 显卡出现问题，这种情况不应发生。不建议使用大于 110MHz 的频率。Diamond 声称 135MHz 是最大速度，但如果你在 Viper 上没有 135MHz，他们会给你 RMA 号以更换板卡。分配功能正在添加。目前，CopyArea、MoveWindow 和 DrawLine 在使用 xdm 时似乎存在问题。返回 VT 时光标会混乱。

## 联系信息

可以从 FTP ftp.Free86.org 和镜像获取 Free86。详情请向 Free86.org 发送邮件。

XFree86 版本 3.1.2

# XF86_Mono

用于 x86 平台的 XFree86 1 位非加速 Window 服务器

## 概要

`XF86 Mono [:displaynumber] [option]`

## 描述

`XF86_Mono` 是用于 VGA 和 Super VGA 以及其他单色显卡的 1 位静态服务器。

## 配置

`XF86_Mono` 服务器支持以下单色模式下的 Super VGA 芯片：

（此处省略部分重复/通用列表翻译，根据上下文逻辑保留 XF86_Mono 特定说明）

## XF86_Mono

`XF86Config` 中 Device 部分的条目包括：

| name | 指定驱动程序可芯片组。 |
|---|---|
| ATI | Vagon |
| Tseng | Et3000, et4000, et4800/W3 |
| Western Digital | Pvga1, wd90c, wd90c1, wd90c31, wd90c33 |
| NCR | 77C22, 77EE |
| Compaq | AVGA: OI067, OI077, OI087 |
| Oak Cirrus | CLG0524, CLG0522, CLG0524, CLG0526, CLG0528, CLG0529, CLG0538, CLG0534, CLG0536, CLG6205, CLG6215, CLG6225, CLG6235, CLG6418, CLG6412, CLG6428, CLG440 |

`XF86_Mono` 服务器支持以下单色显卡和分辨率：

- L-View, LaserView PLUS（1bpp 模式）：1664×1280
- 来自 Apollo 工作站的单色显卡（ID 为 9）：NGC-1280:1280[1472]:1024
- Apollo 1280,1024
- Hercules 及兼容显卡：720xx348

此外，它支持最大分辨率约为 800×650 的通用 VGA 显卡。在支持的 SVGA 芯片中，`XF86_Mono` 将使用 1/2 显示模式，在 1MB 显存下产生约为 1664×1260 的最大分辨率。`XF86_Mono` 不支持支持芯片的加速功能。

## 选项

除了 `Xserver(1)` 手册描述的服务器服务器外，`XF86_Mono` 还接受更多命令行开关，如 `XFree86(1)` 手册所述。

## 设置

`XFree86` 在初始设置期间使用 `XFree8Config` 配置文件。通用详情请参阅 `XFree8Config(4/5)` 帮助页。这里仅解释 `XF86_Mono` 特定的部分。

## Generic VGA

可能的芯片组：

| | |
|---|---|
| Hyundai | hgc1200 |
| Apollo | sigmal |
| Hercules | apollo9 |

`MemBase menaddress` 指定显存基地址。此选项仅用于 Sigma LaserView。这些显卡的有效地址为 0xA0000, 0xB0000, 0xC0000, 0xD0000, 0xE0000。

`Black red green blue` 设置 RGB 值。这些值必须是 0–63 之间的整数。默认值为 0。此选项仅适用于 vga2 类型。

`White red green blue` 设置 RGB 值。这些值必须是 0-63 之间的整数。默认值为 63。此选项仅适用于 vga2 类型。

允许用户选择驱动提供的选项。目前识别以下字符串：

- swap_habit：用于 Western Digital/PVGA1 芯片组。某些基于 Western Digital 的板卡需要反转高时钟选择。服务器无法在运行时确定此信息。如果服务器检测的时钟列表中第 9 个时钟小于 30MHz，则可能需要设置此选项。
- legend：用于 Sigma Legend 2400 基板卡。此选项启用 Legend 板卡使用的特殊时钟选择算法，这些板卡正常工作必须指定此选项。

### 第一部分：用户命令

hibit_low,hibit_high—适用于 Tseng ET4000 芯片。对于某些 ET4000 卡，服务器在从高分辨率文本模式启动时，难以正确获取高位时钟选择位的状态。这些选项允许指定该状态的正确初始值。要确定正确的初始状态，请从 80x25 文本模式启动服务器。仅当服务器从高分辨率文本模式启动时报告的时钟与从 80x25 文本模式启动时报告的时钟不同时，才此。

8clocks—适用于 PVGA 芯片组，默认为 4 个时钟。某些带有此芯片组的卡支持 8 个时钟。指定此选项将允许驱动检测并使用额外的时钟。

16clocks—适用于 Trident VG8000 和 VG8900 芯片。某些使用 VG8000 和 VG8900 芯片的卡实际上支持 16 个时钟，而不是标准的 8 个。某些单元带有 TCK082 或 TCK038 芯片。指定此选项将允许驱动检测并使用额外的 8 个时钟。

Power_save—此选项允许服务器使用 VESA DPMS 兼容显示器的电源功能。目前不支持挂起（suspend）。参考 `XF86Config(4/5)` 手页了解如何设置不同操作级别的超时时间。此选项为实验性功能。

secondary—适用于 hgc128 和 apoll09 芯片。此选项允许使用这些跳线到次级 I/O 内存地址。

- hgc128: I/O 0x30-0x3F, mem 0x0000-xFFFF (主)。
- apoll09: I/O 0x30-0x3F, mem 0x0000-0xCFFF (主)。
- I/O 0x30-0x3F, mem 0x0000-0xDFFF (次)。

`XF86Config` 会检测位于主地址和次级地址上的 HGC-128；对于 apoll09，默认使用主地址。

注意，`XF86` 具有内部能力确定硬件的运行方式。通常情况下，不需要指定芯片组、时钟和视频。但在某些情况下，自动检测机制的负载过高会导致失败，除非你启动服务器时指定。对于此类情况，可以在一台未加载的机器上运行 `XF86_mono`，查看自动检测的结果（在服务器启动期间打印出来），然后在配置文件中显式指定这些参数。建议在 `XF86Config` 文件中指定所有参数，特别是 Clock（时钟）值。

# 文件
```
