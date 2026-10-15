
# 服务器配置文件

注意：`<XRoot>` 指向 X11 安装树的根目录。

# XF86_SVGA

另请参阅 `X(1)`, `Xserver(1)`, `XFree86(1)`, `XFree86Config(4/5)`, `xf86config(1)`, `xvdtime(1)`, `xdm(1)`, `xinit(1)`

## 缺陷

目前尚无已知 Bug，尽管我们欢迎发送电子邮件至下方列出的地址。

## 联系信息

`XFree86` 源码可通过 FTP 服务器 `ftp.XFree86.org` 获取。
详情请发送电子邮件至 `XFree86@XFree86.org`。

## 作者

参考 `XFree86(1)` 手页。

`XFree86` 版本 3.1.2

# XF86_SVGA

`XF86_SVGA`—适用于 x86 平台上 UNIX 上的非加速 SVGA X 窗口系统

## 摘要

`XF86 SVGA [:displaynumber] [ option ] ...`

## 描述

`XF86_SVGA` 是为 Super VGA 卡设计的 8 位伪彩色（PseudoColor）、16 位真色和 24 位真色。它源自带有 x185 的 x386 服务器。注意：16 位真色目前仅支持某些 Cirrus 和 ARK 芯片，而 24 位真色仅支持某些 Cirrus 芯片。

## 配置方案

`XF86_SVGA` 服务器在 256 色模式下支持以下 Super VGA 芯片。支持高达（约）1152x900 的虚拟分辨率以及（最多）1MB 的内存深度。Western Digital `WD9633` 和某些 Cirrus 芯片支持 2MB 的内存深度以及 1,280x1,024 及更高的虚拟分辨率。某些 Cirrus 芯片在某些配置下支持 16bpp 和 32bpp（真色）模式。某些 ARK 芯片在某些配置下支持 16bpp。还支持 800x600 分的通用 VGA 卡。

- ATI: 18800, 18800-1, 18800-2, 18800-4, 18800-5, 18800-6, 18800-3, 6880-6, 6880X, WD90CX, WD8800
- Western Digital: ET3000, ET4800/932, WD96C10, WD96C11, WD90C24, WD90C30, WD98C31, WD8C33
- Trident: TVGA8900, TVGA89B, TVGA89C, TVGA89BL
- Cirrus Logic: CLD0528, CLD0522, CLD0524, CLD0526, CLD0529, CLD0530, CLD0534, CLD0536, CLD0620, CLD0615, CLD0635, CLD0618, CLD0620, CLD1440, CLD6440
- ARK: ARK1000PV, ARK100VL, ARK2000PV
- RealTek: realtek
- Compaq: cpg_avga
- Oak: oti067, oti077, oti087
- Avance Logic: al2101, al2301, al2302, al2308, al2401
- Chips & Technology: ct65520, ct65530, ct65540, ct65545
- MX: rx
- Video7: video7
- Generic: generic

# 第一部分：用户命令

## Chips & Technology

`AL2101`, `AL2301`, `AL2302`, `AL2308`, `AL2401`, `65520`, `65530`, `65540`, `65545`, `MX6800`, `MX6810` 大多数 Cirrus 芯片以及 Western Digital `WD90C31` 和 `WD9033` 支持加速。`ET4000/WD32` 的加速在独立的服务器中实现（参见 `XF86_W32`）。基于 ATI Mach38、Mach32 和 Mach64 的板应分别参考 `XF86_Mach(1)`、`XF86_Mach32(1)` 和 `XF86_Mach64(1)` 手页。

除了 `Xserver(1)` 手页描述的普通服务器选项，`XF86_SVGA` 还接受 `XF88(1)` 手页描述的更多开关。

# 设置

`XF86config` 使用名为 `XF86Config` 的配置文件进行初始设置。详情见 `XF86config(4/5)` 手页。此处仅解释 `XF86_SVGA` 部分。

此服务器需要在 `XF86Config` 中包含带有 `svga` 的 Screen 部分。

`XF86Config` 中的 Device 部分包括：

| 芯片组名称 | 指定芯片组以便使用正确的驱动程序 |
| :--- | :--- |
| ATI | et3800,et4000,et4000w32,et4000w321,et4000w32p |
| Tseng | |
| Western Digital | pvga1,wd90c00,wd90c10,wd90c24,wd90c30,wd90c31,wd90c33 |
| Genoa | gva |
| Trident | tva8800s,tva8900b,tva8900c,tva8900c1,tva9000e |
| NCR | ncr77c22,ncr77c2e |
| Cirrus Logic | cld5420,clg5422,clg5424,clg5426,clg5428,clg5429,clg5430,clg5434,clg5436,clg6200,clg6215,clg6235,clg6418,clg6420,clg1440 |
| RealTek | realtek |
| ARK | ark1000vp,ark1000vi,ark2000vp |
| Compaq | cpg_avga |
| Oak | oti067,oti077,oti087 |
| Avance Logic | al2101,al2301,al2302,al2308,al2401 |
| Chips & Technology | ct65520,ct65530,ct65540,ct65545 |
| MX | rx |
| Video7 | video7 |
| Generic | generic |

# XF86_SVGA

## 选项 "optionstring"

允许用户选择驱动程序提供的某些选项。目前识别以下字符串：

`legend`—适用于基于 Sigma Legend ET4000 的板。此选项启用了 Legend 板上特殊的时钟选择算法。

`swp_habit`—适用于 Western Digital/PVGA 芯片。基于 Western Digital 的板需要反转高位时钟选择位。

`hibit_low`,`hibit_high`—适用于 Tseng ET4000 芯片。对于某些 ET4000 卡，服务器在从高分辨率文本模式启动时，难以正确获取高位时钟选择位的状态。这些选项允许指定该状态的正确初始值。要确定正确的初始状态，请从 80x25 文本模式启动服务器。仅当服务器从高分辨率文本模式启动时报告的时钟与从 80x25 文本模式启动时报告的时钟不同时，才此。

`8clocks`—适用于 PVGA 芯片组，默认为 4 个时钟。某些带有此芯片组的卡支持 8 个时钟。指定此选项将允许驱动检测并使用额外的时钟。

`16clocks`—适用于 Trident VG8000 和 VG8900 芯片。某些使用 VG8000 和 VG8900 芯片的卡实际上支持 16 个时钟，而不是标准的 8 个。某些单元带有 TCK082 或 TCK038 芯片。指定此选项将允许驱动检测并使用额外的 8 个时钟。

`probe_clocks`—适用于 Cirrus 芯片。有一组通常使用的固定时钟。指定此选项将强制驱动程序探测时钟而不是重复内置默认值。此选项仅用于调试目的。

`power_save`—此选项允许服务器使用 VESA DPMS 兼容显示器的电源功能。目前不支持挂起（suspend）。参考 `XF86Config(4/5)` 手页了解如何设置不同操作级别的超时时间。此选项为实验性功能。

`noaccel`—适用于 Cirrus 和 WD 芯片。此选项禁用了 `cld5426`、`cld5428`、`wd8924` 和 `wd8923` 芯片的加速功能。

`fifo_conservative`—适用于 Cirrus 芯片。此选项将超过 65MHz 时钟的 CRT FIFO 阈值设置为保守值。这会降低性能

`fifo_aggressive`—适用于 Cirrus 芯片。此选项将超过 65MHz 时钟的 CRT FIFO 阈值设置为激值。这可能会提高性能。

# 第一部分：用户命令

`slow_dram`—适用于 Cirrus 芯片。此选项为慢 DRAM 芯片设置 DRAM定时。
`fast_dram`—适用于 ET4000 和 Cirrus 芯片组。此选项为快速 DRAM 芯片设置 DRAM定时。
`no_2mb_banks`—适用于 Cirrus 芯片。具有 2MB 视频的 Cirrus 卡需要此选项，其形式为 512kx8 DRAM（4 块芯片）而非 256kx4 DRAM（16 块芯片）。
`no_bitbl`—适用于 Cirrus 芯片。此选项禁用硬件 BitBL 使用。
`linear`—尝试将帧缓冲区线性映射到高内存。目前仅支持某些 Cirrus 芯片。
`med_dram`,`favour_bitbl`,`sw_cursor`,`cld6225_lcd`,`mio`—更多针对 Cirrus 的特定选项。请参阅 `/usr/x11/lib/x11/doc/README` 了解 Cirrus 选项使用的详细说明。

## 加速选项集

可选的选择字符串可以取以下值：

`speedup "selection"`

`all`
如果省略选择，或者省略 speed 选项，则选择默认为 all。某些加速只能与 ET4000、W908C31 和 WD908C3 芯片组配合，另一些需要宽度为 1024 的虚拟分辨率。适用于给定配置的加速将被自动禁用。

`nospeedup`

`Randac randac-type`

禁用加速代码。这等同于 `speedup none`。
指定板上 RAMDAC 的类型。目前只有 t48 使用此 RAMDAC。识别的 RAMDAC 类型包括
- `Att28c490`—AT&T 20C490 或兼容的 8 位 RAMDAC。
- `Att28c498`—AT&T 20C498 或兼容的 16 位 RAMDAC。
- `Zoomdac`—Hercules Stingray ProV 和 64V 使用的 RAMDAC。
- `Stig1700`—Stig1700 或兼容的 RAMDAC。

注意，Free86 具有内部检测运行硬件的能力。因此通常不需要指定芯片组、时钟和视频。但在某些情况下，自动检测机制可能会失败（例如，启动服务器时机器负载过高）。对于此类情况，应先在未匹配的负载下运行 `X86_SVGA`，查找自动检测结果（服务器启动期间打印），并在配置文件中显式指定这些参数。建议在 `Free86Config` 文件中指定所有参数，尤其是 Clock 值。

# 文件
