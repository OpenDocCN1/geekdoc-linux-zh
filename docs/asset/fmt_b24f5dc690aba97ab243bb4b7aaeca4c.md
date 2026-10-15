
# 引言

FRiC, <frac@pobox.com> v6969, 1995年11月14日

本文列出了 Linux 支持的大多数硬件，并帮助你找到任何驱动程序。

欢迎阅读 Linux 硬件兼容性 HOWTO。本文列出了 Linux 支持的大多数硬件；如果人们在 USENET 上提问之前能先读读这个就好了！

标题为“其他（Others）”的小节列出了具有不同程度能力的 alpha 或 beta 驱动程序的硬件，或列出了未包含在标准内核中的驱动程序。另外请注意，某些驱动程序仅存在 alpha 内核中，如果你看到列出的支持项在你的 Linux 内核版本中没有，你应该升级。

本文档的最新版本可以在网络上存放 Linux HOWTO 的常规站点找到。（参见参本书的附录 B 以获取 HOWTO 站点列表。）

如果你知道任何未列出的 Linux 硬件兼容性情况，请告诉我——发送电子邮件或在互联网相对聊天（IRC）上给我发信。适用标准 Linux 文档项目（LDP）版权。如果你在商业发行中使用此或其他或其他任何 HOWTO，提供一份你产品的免费副本将很好。

# 体系

本文仅处理适用于 Intel 平台的 Linux；对于其他平台请检查以下内容：

| 平台 | 站点 |
| :--- | :--- |
| Linux/ARM | http://whirlig.ecs.ac.uk/~rmk92/armlinux.html |
| Linux/68k | http://users.informatik.rwth.de/~hn/linux68k.html |
| Linux/MIPS | http://waldorf-gnmbh/linux-mips.html |
| Linux/PowerPC | http://lib.stanford.edu/linux/ppc/ |
| Linux/8086 | http://www.linux.org/Linux86.html |
| Linux/Alpha | http://azstarnet.com/~axinusux/ |
| Linux for Acorn | http://phcl.ac.uk/~amb/linux.html |
| Linux/Mac | http://ibuu.se/maclinux/ |

# 计算机/主板/BIOS

工业标准架构 (ISA)、VESA 本线 (VLB)、扩展 ISA (EISA) 和外设连接 (PCI) 总线均支持。

标准内核不支持 PS/2 和通道 (MCA)。提供了 Alpha PS/2 内核，但不推荐初学者或专业用户使用。

# 特定系统

- Compaq Deskpro XL--http://www.uib.ac.at/xl/
- IBM PS/2 MCA--ftp://invaders.nd.edu/pub/misc/

# 笔记本电脑

某些笔记本电脑使用特殊的视频适配器或电源管理，在 Linux 下无法使用电源管理是不常的。查看 http://www.cs.utexas.edu/users/kharker/laptop 的 Linux 首页。

| 控制器 | 站点 |
| :--- | :--- |
| APM | ftp://tsx-11.mit.edu/pub/linux/laptops/apm/ |
| PCMCIA | ftp://cb-iris.stanford.edu/pub/pcmia/ |
| Non-blink | ftp://unsite.unc.edu/pub/linux/kernel/console/noblink-1.5.gz |
| Power savings (WD7600芯片组) | ftp://unsite.unc.edu/pub/linux/system/low-level/pwm-1.0.gz |
| 其他通用信息 | ftp://tsx-11.mit.edu/pub/linux/laptops/ |

# 特定笔记本电脑

| 笔记本品牌和型号 | 站点 |
| :--- | :--- |
| Compaq Contura Aero | http://domen.uninett.no/~hta/linux/aero-faq.html |
| IBM ThinkPad | http://peipa.essex.ac.uk/tp-linux/tp-linux.html |
| NEC Versa M and P | http://www.safe.edu:80/"nelson/versa-linux/ |
| Tadpole P1000 | http://peipa.essex.ac.uk/tadpole-linux/tadpole-linux.html |

# PCMCIA

见 http://hyper.stanford.edu/~dhinds/pcmmia/。

PCMIA 驱动目前支持所有常见的 PCMIA 控制器，包括 DataBook TCIC/2、Intel 82365SL、Cirrus PD67xx 和 Vadem VG-468 芯片组。某些笔记本电脑使用的 Motorola 6AHC05GA 控制器不支持。附录结尾的支持 PCMIA 卡列表。

# CPU/FPU

Intel/AMD Cyrix 386SX/DX/DXL/SLC，486SX/DX/SLX2/DX/DX4, Pentium：基本上 386 或更好的处理器都能工作。如果你没有数学协处理器，Linux 有内置的 FPU 仿真。

内核 1.3.31 及更高版本包含了实验性的 SMP（多 CPU）支持。查看 Linux/SMP 项目页面获取详情和更新。

| 控制器 | 站点 |
| :--- | :--- |
| Linux/SMP Project | http://www.linux.org.uk/SMP/title.html |

少数早期 486DX 可能会在特殊情况下挂起。所有当前芯片应该是没问题的，更换旧 CPU 可能不是什么问题。

ULSI MathCo 在 FSAVE 和 FRSTOR 指令中有一个漏洞，会导致所有保护模式操作系统的问题。一些较老的 IIT 和 Cyrix 芯片也有这个问题。

在非常旧的内核 (1.1.x) 中， U5C 芯片的 TLB 刷新存在问题。

| 处理器 | 站点 |
| :--- | :--- |
| 在 Cyrix 处理器上启用缓存 | ftp://sunsite.unc.edu/pub/Linux/kernel/CxPatch030.tar.gz |
| Cyrix 软件缓存控制 | ftp://sunsite.unc.edu/pub/linux/kernel/patches/linux.cxpatch |

# 显卡

Linux 在文本模式下支持所有显卡。下方未列出的 VGA 卡可能仍可以使用单色 VGA 和/或标准 VGA 驱动工作。

如果你正在考虑购买一张廉价显卡来运行 X，请记住加速显卡（如 ATI Mach、ET400/W32p 和 S3）比未加速或部分加速的显卡快得多（例如，带有 2 MB DRAM 的 Cirrus 和 S3 Trio6 核心价格约为 160 美元，带有 2 MB DRAM 的 S3 868 卡价格约为 200 美元）。

# 显卡

"32 bpp" 实际上是在 32 位边界上对齐的 24 位颜色。这**并不意味着**显卡支持 32 位颜色；它仍然是 24 位颜色（16,777,216 色彩）。XFree86 不支持 24 位紧凑像素模式，因此在其他操作系统中支持 24 位颜色模式的显卡，在 XFree86 中可能无法实现 24 位颜色。这些显卡包括 Mach32、Cirrus 542x、S3 801/805/868/968、ET4000 等。

# Diamond 显卡

目前大多数 Diamond 显卡都受当前的 XFree86 支持。早期的 Diamond 显卡可能没有 XFree86 的官方支持，但有方法让它们运行。Diamond 现在正积极支持 XFree86 项目。支持的显卡如表所示：

| 显卡 | 站点 |
| --- | --- |
| Diamond 对 XFree86 的支持 | http://www.diamondmm.com/linux.html |
| Diamond 常见（针对旧显卡） | ftp://sunsite.unc.edu/pub/Linux/X11/Diamond.FAQ |
| Diamond 不满用户页面 | ~gladstone.uoregon.edu/~trenton/diamond/ (针对旧显卡) |

# SVGALIB (控制台图形)

- - VGA
- EGA
- ARK Logic ARK1000PV/2000PV
- ATI VGA Wonder
- Mach32
- Cirrus 542x, 543x
- OAK OTI037/67/77/87
- S3 (有限支持)
- Trident TVGA8900/9000
- Tseng ET3000/ET4000/W32

# XFree86 3.1.2, 加速

- - ATI Mach8
- ATI Mach32 (16 bpp——不支持所有 Mach32 显卡)
- ATI Mach64 (16/32 bpp)
- Cirrus Logic 5420, 542x/5430 (16 bpp), 5434 (16/32 bpp), 62x5
- IBM 8514/A
- IBM XGA, XGA-II
- IIT AGX-010/014/015/016
- Oak OTI-087
- S3 911, 924, 801, 805, 928, 864, 964, Trio32, Trio64, 868, 968
- 本 HOWTO 的附录 A 提供了支持的 S3 显卡列表
- Tseng ET4000/W32/W32/W32p
- Weitek P9000 (16/32 bpp)
- Diamond Viper VLB/PCI
- Orchid P9000
- Western Digital WD90C03/31/33

# Free86 3.1.1, 未加速

- ARK Logic ARK1000PV/VL, ARK2000PV
- ATI VGA Wonder 系列
- Avance Logic AL2101/2228/2301/2302/2308/2401
- Chips & Technologies 65520/65530/65540/6545
- Cirrus Logic 6420/6440
- Compaq AVGA
- Genoa GVGA
- MCGA (32 × 200)
- MX68000/MX6810
- NCR 77C22, 77C22E, 77C22+
- Oak OTI-067, OTI-077
- RealTek RTG3106
- Trident VGVA8800, VGVA8900, VGVAxxx (不支持 TGUI 芯片组)
- Tseng ET3000, ET400AX
- VGA (标准 VGA，4 位，速度慢)
- Video 7/Headland Technologies HT216-32
- Western Digital/Paradise PVGA1, WD90C0/10/11/24/30/31/33

# 单色

- Hercules mono
- Hyundai HGC-1280
- Sigma LaserView PLUS
- VGA mono

# 其他

- - EGA (古老的，1992年)—ftp://ftp.funet.fi/pub/Linux/BETA/Xega/
- ET4000/W32 和 ICS5341 GenDAC—ftp://sunsite.unc.edu/pub/Linux/X11/X-servers/
- Trident TGU1940—ftp://sunsite.unc.edu/pub/Linux/X11/X-servers/

# 开发中

- - Compaq QVision

我不知道这些显卡的支持何时完成，请不要问我。如果你现在就需要这些显卡的支持，请使用 Accelerated-X。

# 商用 X 服务器提供 XFree86 不支持的显卡，并可能为 XFree86 支持的显卡提供更好的性能。通常情况下，它们支持的显卡比 XFree86 多，因此我只列出 XFree86 不支持的显卡。直接联系供应商或查看 Commercial HOWTO 获取更多信息。商用服务器列在附录 B 中。

# Accelerated-X 1.2

- Chips & Technologies 8C45x, 8C48x, 655xx
- Compaq QVision 2000
- Matrox MGA-I, MGA-II
- Number Nine I-128
- Weitek P9100
- X Inside Inc.-info@inside.com

Accel-X 支持 16 和 32bpp 模式的显卡，并支持具有这些模式的 24 位像素模式，包括 ATI Mach32、Mach64 (128 bpp)、ET4000/W32、S3-866/968 等。Accel-X 还支持其他硬件，如图形触摸屏。Accel-X 还显示 XV (X) 扩展（在 Matrox Comet, Marvel ShowTime Plus 上）、PEX 和 IDE。

# Metro-X 2.3.2

Metro-sales@metrolink.com 支持的板卡比Free86 多，但比 Accel-X 少；然而，他们没有更多他们的信息。请直接邮件给他们获取更多信息。

# 附录 C

**注意**：Red Hat Linux 的商业版本包含 Metro-Link Metro-X 服务器的单用户许可。书中附带的不包含此产品。

# 控制器 (硬盘)

Linux 支持标准的 IDE、MFM 和 RLL 控制器。当使用 MFM/RLL 控制器时，格式化磁盘时使用 ext2fs 和块检查选项是重要的。支持增强 IDE (EIDE) 接口，最多两个 IDE 接口和最多四个硬盘/CD-ROM 驱动器。Linux 检测这些 EIDE 接口：

- CMD-640
- DTC228D
- FGI/Holtek HT6560B
- RZ1000
- Triton (82371FB) IDE (带有总线主 DMA)

模拟 ST-506 (MFM/RLL/IDE) 接口的 ESDI 控制器也可以工作。块检查也适用于这些控制器。通用的 8 位 XT 控制器也可以工作。

# 控制器 (SCSI)

仔细选择 SCSI 控制器非常重要。许多廉价的 ISA 控制器是为驱动 CD-ROM 而非硬盘设计的。低端 SCSI 控制器并不比 IDE 好。在购买显卡之前，查看 SCSI HOWTO 和性能数据。

- `/usr/src/HOWTO/SCSI-HOWTO.gz`

# 支持

- AMI Fast Disk VLB/EISA (兼容 BusLogic)
- Adaptec AVA-1505/1515 (ISA) (兼容 Adaptec 152x)
- Adaptec AHA-1510/152x (ISA) (兼容 6260/6360)
- Adaptec AHA-154x (ISA) (所有型号)
- Adaptec AHA-174x (EISA) (增强模式下)
- Adaptec AHA-274x (EISA)/284x (VLB) (兼容 7770)
- Adaptec AHA-2940/3940 (PCI) (兼容 7870) (自 1.3.6 起)
- Always IN2000
- BusLogic (ISA/EISA/VLB/PCI) (所有型号)
- DPT PM2001, PM2012A (EATA-PIO)
- DPT Smartcache (EATA-DMA) (ISA/EISA/PCI) (所有型号)
- DTC 329x (EISA) (兼容 Adaptec 154x)
- Future Domain TMC-16x0, TMC-3260 (PCI)
- Future Domain TMC-8xx, TMC-950
- Media Vision Pro Audio Spectrum 16 (ISA)
- NCR 5380 通用显卡
- NCR 53c400 (Trantor T130B) (使用通用 NCR 5380 SCSI 支持)
- NCR 53c406a (AcouLogic IsPort / Media Vision Premium 3D SCSI)
- NCR 53c7x0, 53c8x0 (PCI)
- Qlogic/Control Control Concepts SCSI/IDE (FAS408) (ISA/VLB/PCIA) (与 PCI 不兼容，不同芯片)
- Seagate ST-01/ST-02 (ISA)
- SoundBlaster 16 SCSI-2 (兼容 Adapter 152x) (ISA)

# 不支持

- - VGA (标准 VGA，4 位，速度慢)
- Video 7/Headland Technologies HT216-32
- Western Digital/Paradise PVGA1, WD90C0/10/11/24/30/31/33

# 网络适配器 707

- SIIG I/O 扩展器 4S (4端口，使用 4 个 IRQ)
- PC-COMM 4端口
- STB 4-COM
- Twincom ACI/550
- Usenet 串口板 II

非智能网卡通常有两种种类：一种使用标准串口地址并占用 4 个 IRQ；另一种是是兼容 AST FourPort 的，使用可选择的地址块和单个 IRQ。（地址和 IRQ 通过使用 `retailsial` 设置）。如果你正在弃用这些卡，请务必检查它们符合哪种标准；价格没有参考价值。

# 支持的智能控制器（多部分支持）

- Cycles Cyclcom-8/16 (ISA/PCI)
- Stallion EasyIO (ISA) / EasyConnection 8/32 (ISA/MCA)
- Stallion EasyConnection 8 / 64 / OnBOARD (ISA/EISA/MCA) / Brumbly / Stallion (ISA)

其他

| 控制器 | 站点 |
|---|---|
| Comtrol RocketPort (8/16/32端口) | [ftp://tsx-11.mit.edu/pub/linux/packages/comatrol/] |
| DigiBoard COM/Xi—联系 Simon Park | si@wimpol.demon.co.uk (电子邮箱地址) |
| DigiBoard PC/Xe (ISA) 和 PC/Xi (EISA) | [ftp://ftp.digib.com/drivers/] |
| Hayes ESP8 | 联系 Dennis Boylan：den@lan.com |
| Moxa C218 (8端口) / C320(8/16/24 可扩展) | <ftp://ftp.moxa.com.tw/drivers/c-218-320/32 index/> |
| Specializ SIO/XIO (模块化，4到32个端口) | [ftp://sunsite.unc.edu/pub/Linux/kernel/patches/serial/sriv0_5.jaz] |
| Stallion Technologies EasyIO/ | [ftp://sunsite.unc.edu/pub/Linux/kernel/patches/EasyConnection 8/32serial/stallion-0.1.9.tar.gz] |

# 网络适配器

以太网适配器的性能差异很大。通常情况下，适配器越新，性能越好。某些非常旧的卡（如 3C501）之所以有用，是因为可以在垃圾堆里以 5 美元的价格买到一个。要小心克隆卡——并非所有克隆都是良品，糟糕的克隆卡经常会导致 Linux 下出现异常死机。请阅读 Ethernet HOWTO 以获取各种卡的详细说明。（参见附录 B，“Linux HOWTO Index”获取 Ethernet HOWTO 的地址。）

# 支持的以太网

- 3C501—如瘟疫一样避开
- 3C503, 3C505, 3C507, 3C509/3C509B (ISA)/3C579 (EISA)
- AMD LANCE (TC9960/PCNet-ISA/PCI) (AT1500, HP J2405A, NE1500/NE2100)
- AT&T GIS Wave
- Allied Telesis AT1700
- Ansel Communications AC3200 EISA
- Apricot Xen-II
- Cabletron E21xx
- DEC DE425 (EISA)/DE434/DE435 (PCI)
- DEC DEPCA 和 EtherWorks
- HP PCLAN (27245 和 27xxx 系列)
- HP PCLAN PLUS (27247B 和 27252A)
- HP 10/109VG PCLAN (ISA/EISA/PCI)
- Intel EtherExpress
- Intel EtherExpress Pro
- NE2000/NE1000 (小心克隆卡)
- New Media Ethernet
- Racal-Interlan NI51210 (i82586 以太网芯片)
- Racal-Interlan NI66510 (am7990 通道芯片)。当内存超过 16MB 时无法工作。
- PureData PDC8028, PDI8023
- SEEK 8005
- SMC Ultra
- Schneider & Koch G16
- Western Digital WD80x3
- Zenith Z-Note/IBM ThinkPad 300 内置适配器

# 口袋及便携式适配器

- AT-Lan/Tec/RealTek 并口适配器
- D-Link DE600/DE620 并口适配器

# 无槽式

- SLIP/CSLP/PPP (串口)
- EQL (串口 IP 负载均衡)
- PLIP (并口)—使用 LapLink 或双向清空

# ARCnet

- 兼容所有 ARCnet 卡

# 令牌环 (Token Ring)

- IBM Tropic 芯片卡

# 业余无线 (AX.25)

- Ottawa PI/PI2
- 大多数基于 8530 的 HDLC 板

# 其他

| 适配器 | 站点 |
| --- | --- |
| 以太网 3Com Vortex 系列网卡 (3C590, 3C595 (100 Mbps)) (PCI) | [http://cesdisis.gsfc.nasa.gov/pub/linux/drivers/vortex.html] |
| DEC 21040/21140 "Tulip"/SMC PCI EtherPower 10/100 | [http://cesdisis.gsfc.nasa.gov/linux/tulip.html] |

# ISDN

查看 ISDN 页面：

```
