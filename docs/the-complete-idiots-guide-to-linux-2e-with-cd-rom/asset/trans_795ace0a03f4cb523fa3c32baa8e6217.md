

颜色深度选择由面板底部的四个按钮激活：8 bpp（每像素位数）将产生 256 种颜色，16bpp 将产生 32768 种颜色，而 24 和 32bpp 分别将产生 65535 和数百万种颜色。请注意，并非所有显卡都支持所有显示深度。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_313_0.png)

Modeselection 面板允许您设置要在监视器上使用的分辨率以及默认颜色深度。

## 其他配置

其他配置涉及切换分辨率和退出 X 服务器的选项（参见下图）。Ctrl+Alt+数字键盘上的加号 (+) 和减号 (-) 键允许您即时在不同显示分辨率之间切换。Ctrl+Alt+Backspace 序列用于立即退出 X 服务器。如果您启动到 X Windows 而无法读取屏幕，Ctrl+Alt+Backspace 将带您返回到命令行提示符。您可能需要在配置正确之前这样做一次或两次。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_313_1.png)

其他配置面板允许您设置有关切换分辨率和退出 X-Windows 的选项。

## 完成配置

当您单击“完成”退出 XF86Setup 程序时，XF86Setup 会提示您确认是否已完成系统设置。如果您选择“确定”，XF86Setup 将尝试使用您为监视器和显卡指定的设置启动您卡专用的 X 服务器。如果您的设置看起来正常，您就完成了。如果您的屏幕被挤压并且监视器几何按钮无法纠正问题，您可能需要使用 xvidtune，这是一个可以微调视频速率的程序。Xvidtune 是一个潜在危险的程序，只有在您无法使用监视器的控件调整画面时才应使用。

如果您的设置正确，您应该会看到黑白网格作为屏幕的背景，以及一个没有标题栏的窗口，其与屏幕左上角对齐。如果正确，请单击“保存配置并退出”按钮。您的系统现在将启动到多用户模式并准备使用。

恭喜！现在您已经安装并配置了 Caldera OpenLinux，请转到第 1 章“在 KDE 桌面上的首次登录”，开始使用您的新操作系统。

目录

Products | Contact Us | About Us | Privacy | Ad Info | Home

使用本网站须遵守某些条款和条件。Copyright © 1996-2000 EarthWeb Inc.
保留所有权利。未经 EarthWeb 明确书面许可，不得以任何形式或媒体复制全部或部分内容。

## SPIDER KILLER

## spider catcher

- HOME
- ACCOUNT INFO
- SUBSCRIBE
- LOGIN
- SEARCH
- MY ITKNOWLEDGE
- FAQ
- SITEMAP
- CONTACT US

要访问内容，请单击章节和节标题。

## Complete Idiot's Guide to Linux

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

Bookmark It

Search this book:

目录

## 附录 B
OpenLinux 兼容性指南

本附录经 Caldera 网站许可转载。如需最新信息，请访问 http://www.calderasystems.com/products/openlinux/hardware.html。如果您的硬件未列出，很可能不受支持。请联系制造商获取更多信息或购买兼容的替代品。确保您的型号与受支持的指定完全匹配非常重要。

## CD-ROM 驱动器

以下是 Caldera OpenLinux 1.3 版支持的 CD-ROM 驱动器和接口卡列表。

## CD-ROM 驱动器

## 支持的 CD-ROM 驱动器

| Company | Model |
|---|---|
| Aztech | CDA268-01A |
| Conrad | TXC |
| Creative Labs | CD-200F (CD-200 not fully supported) |
| CyCDROM | CR520 |
|  | CR520ie |
|  | CR540 |
|  | CR940ie |
| ECS-AT | Vertos 100 |
| Funai | E2550UA |
|  | MK4015 |
|  | 2800F |
| Goldstar/Reveal | R420 |
| IBM | External ISA drive |
| Kotobuki | See Panasonic |
| Laseramate | CR328A |
| Longshine | LCS-7260 |
| Matsushita | See Panasonic |
| Mitsumi | CRMC LU005S |
|  | FX001S (single speed) |
|  | FX001S (multisession) |
|  | FX001D (double speed) |
|  | FX001D (multisession) |
| Okano/Wearnes | CDD110 |
| Optics Storage | DOLPHIN 8000 AT |
| Orchid | CDS-3110 |
| Panasonic | CR-521 |
|  | CR-522 |
|  | CR-523 |
|  | CR-562 |
|  | CR-563 |
| Philips/LMS | cm206 (w/ cm206 card) |
| Sanyo | CDR-H94A |
| Sony | CDU-31A (not auto-probed) |
|  | CDU-33A (not auto-probed) |
|  | CDU-510 |
|  | CDU-515 |
|  | CDU-531 |
|  | CDU-535 |
| Teac | CD-55A |

## 支持的 CD-ROM 接口卡

## 支持的 CD-ROM 接口卡

## Company

- ISP16
- MAD16
- Mozart

大多数具有 512 或 2048 字节块大小的 SCSI 驱动器应该可以工作。您需要有受支持的 SCSI 控制器卡才能使用其中一个驱动器。注意：一些 CD-ROM 驱动器随附非标准的 SCSI 适配器，可能不受支持。

大多数通过 IDE/ATAPI 接口连接的驱动器应该可以工作。目前销售兼容驱动器的一些厂商包括 Aztech、Mitsumi、NEC、Sony、Creative Labs 和 Vertos。一些多 CD 换带机，如 NEC CDR-251 和 Sanyo 的“非标准”3-CD 换带机作为 ATAPI 驱动器受支持，因此在前面的列表中没有特殊的驱动程序。以下文档末尾包含了一个示例 CD 更换程序：

/usr/src/linux/Documentation/cdrom/ide-cd

CyCDROM 940i 和 520ie 驱动器，虽然连接到 IDE 接口，但不是 IDE 设备；它们使用 Aztech 驱动程序。

## 并行端口 CD-ROM 驱动器

## 兼容的并行端口 CD-ROM 驱动器

| Company | Model | Module |
|---|---|---|
| Arista | ParaCD 525 (4/8 bit only) | arcd |
| DataStor | EP2000 | dscd |
| Freecom | Power CD* | pwcd |
| KingByte Information Sys. | KBIC-951A | kicd |
| Microsolutions | Backpack (modern) | bpcd |
|  | Backpack (old) | bpmcd |
| OnSpec Electronics | 90c26 | oicd |
| Shuttle Technologies | EPIA | eicd |
|  | EPAT | epcd |
|  | EPEZ | epcd |

*必须先在 DOS 中使用 POWER-CD.SYS 初始化；然后使用 LOADLIN 启动到 Linux。

## 网络卡

以下是 Caldera OpenLinux 1.3 版（包括 Standard、Base 和 Lite）支持的以太网、帧中继、令牌环和无线调制解调器卡列表。

## 以太网卡

## 以太网卡

| Company | Model | Module |
|---|---|---|
| 3Com | Etherlink | 3c501 |
| 3Com | Etherlink II | 3c503 |
| 3Com | Etherlink II/16 | 3c503 |
| 3Com | Etherlink Plus | 3c505 |
| 3Com | Etherlink16 | 3c507 |
| 3Com | Etherlink III (3c509) | 3c509 |
| 3Com | Etherlink III (3c579) | 3c509 |
| 3Com | Fast Etherlink (3c590, 3c592, 3c595, 3c597) | 3c59x |
| 3Com | Fast Etherlink XL (3c900, 3c905, 3c905B) | 3c59x |
| 3Com | Corkscrew Etherlink XL (ISA) | 3c515 |
| Accton | EtherDuo PCI | tulip |
| Accton | EN1207 (all three types) | tulip |
| Adaptec | ANA6901/C | tulip |
| Adaptec | ANA6911/TX | tulip |
| Allied Telesis | AT1500 | lance |
| Allied Telesis | AT1700 (ALPHA) | at1700 |
| Allied Telesis | LA100PCI-T | tulip |
| AMD Lance | PCnet-ISA | lance |
| AMD Lance | PCnet-ISA+ | lance |
| AMD Lance | PCnet-PCI | lance32 |
| AMD Lance | PCnet-PCI II | lance |
| AMD Lance | PCnet-32 | lance32 |
| Ansel Com. | AC3200 EISA | ac3200 |
| Apricot | Xen-II | apricot |
| ARCnet | All (ALPHA) | arcnet |
| AT-Lan-Tec/Realtek | RTL8002 (chipset) | atp |
| AT-Lan-Tec/Realtek | RTL8012(chip) | atp |
| Bay Networks | Netgear FX310 TX 10/100 | tulip |
| BOCA | AMD 79C960 based cards | lance |
| Cabletron | E2100 | e2100 |
| C-NET | CNE-935 | tulip |
| Cogent | EM100 | tulip |
|  | EM110 | tulip |
|  | EM400 | tulip |
|  | EM960 | tulip |
|  | EM964 Quartet | tulip |
| Compaq | Netelligent 10(PCI) | tlan |
|  | Netelligent 10/100(PCI) | tlan |
|  | Integrated NetFlex-3/P(PCI) | tlan |
|  | NetFlex-3/P(PCI) | tlan |
|  | ProLiant Netelligent 10/100(PCI) | tlan |
|  | Dual Port Netelligent 10/100(PCI) | tlan |
|  | Deskpro 4000 5233MMX (PCI) | tlanCompex |
|  | Readylink ENET100-VG4(EISA/PCI) | hp100 |
| Danpex | EN-9400P3 | tulip |
| D-Link | DE-530CT | tulip |
|  | DE-600 | de600 |
|  | DE-620 | de620 |
|  | DFE500-Tx | tulip |
| DEC | DEPCA | depca |
|  | DE-100 | depca |
|  | DE-101 | depca |
|  | DE-200 Turbo | depca |
|  | DE-201 Turbo | depca |
|  | DE-202 Turbo (TP BNC) | depca |
|  | DE-203 Turbo (BNC) | ewrk3 |
|  | DE-204 Turbo (TP) | ewrk3 |
|  | DE-205 Turbo (TP BNC) | ewrk3 |
|  | DE-210 | depca |
|  | DE-422 (EISA) | depca |
|  | DE-425 (TP BNC EISA) | de4x5 |
|  | DE-434 (TP PCI) | de4x5 |
|  | DE-435 (TP BNC AUI PCI) | de4x5 |
|  | DE-450 (TP BNC AUI PCI) | de4x5 |
|  | DE-500 10/100 | de4x5 |
|  | EtherWORKS | depca |
|  | EtherWORKS III | ewrk3 |
|  | EtherWORKS 10 (PCI) | tulip |
|  | EtherWORKS 10/100 (PCI) | tulip |
|  | QSILVER | tulip |
|  | DEC chips 21040/21041/21140 | tulip |
|  | DEC chips 21142/21443 | tulip |
|  | DEC chips 21040(no SROM)/21041A | de4x5 |
|  | DEC chips 21140A | de4x5 |

