

- IBM ThinkPad
  `http://peipa.essex.ac.uk/tp-linux/tp-linux.html`
- IBM ThinkPad 770 系列
  `http://resources.ibm.com/linux/thinkpad770`
- NEC Versa M 和 P
  `http://www.swan.ac.uk:80/~nelson/versa-linux/`
- Tadpole P1000
  `http://www.tadpole.com/support-trdi/plans/linux.html`
- Tadpole P1000（另一个）
- TI TravelMate 4000M
  `ftp://ftp.batman.jussieu.fr/pub/linux/TM4000M-mini-HOWTO.txt.Z`
- TI TravelMate 5100
- Toshiba Satellite Pro 400CDT
  `http://terra.mpimg-teltow.mpg.de/~burger/T400CDT-Linux.html`

## PCMCIA

- PCMCIA
  `http://hyper.stanford.edu/HyperNews/get/pcmcia/home.html`

PCMCIA 驱动程序目前支持所有常见的 PCMCIA 控制器，包括 Databook TCIC/2、Intel i82365SL、Cirrus PD67xx 和 Vadem VG-468 芯片组。某些 Hyundai 笔记本电脑中使用的 Motorola 6AHC05GA 控制器不受支持。有关受支持的 PCMCIA 卡列表，请参阅“受支持的 PCMCIA 卡”。

## CPU/FPU

支持 Intel/AMD/Cyrix 386SX/DX/SL/DXL/SLC、486SX/DX/SL/SX2/DX2/DX4。Intel Pentium、Pentium Pro、Pentium II、Pentium III（普通版和 Xeon 版）以及 Celeron 也能正常工作。AMD K5 和 K6 运行良好，但应避免使用较旧版本的 K6，因为它们存在缺陷。在 BIOS 设置中禁用“内部缓存”可以作为一种解决办法。AMD K6-2 和 K6-3 同样可以工作。一些早期的 K6-2 300MHz 芯片在与系统芯片搭配时存在问题。Cyrix 6x86 开箱即用。

IDT Winchip C6-PSME2006A 处理器在 Linux 下也受支持（`http://www.winchip.com`）。

如果你没有数学协处理器，Linux 内置了 FPU 仿真。

实验性 SMP（多 CPU）支持包含在 1.3.31 及更新版本的内核中。详情和更新请查看 Linux/SMP 项目页面。

- Linux/SMP 项目
  `http://www.linux.org.uk/SMP/title.html`

Cyrix MediaGX 内置的高级多媒体效果不受支持。

极少数早期的 AMD 486DX 在特殊情况下可能会死机。所有当前芯片应该都没问题，而且旧 CPU 更换芯片应该不是问题。

ULSI Math*Co 系列在 FSAVE 和 FRSTOR 指令中存在缺陷，这会导致所有保护模式操作系统出现问题。一些较老的 IIT 和 Cyrix 芯片也可能存在此问题。

在非常老的内核（1.1.x）中，UMC U5S 芯片存在 TLB 刷新问题。

- 在 Cyrix 处理器上启用缓存
  `ftp://metlab.unc.edu/pub/Linux/kernel/patches/CxPatch030.tar.z`

- Cyrix 软件缓存控制
  `ftp://metlab.unc.edu/pub/Linux/kernel/patches/linux.cxpatch`

- Cyrix 5x86 CPU 寄存器设置
  `ftp://metlab.unc.edu/pub/Linux/kernel/patches/cx5x86mod_1.0c.tgz`

## 内存

所有类型的内存，如 DRAM、EDO 和 SDRAM，都可以与 Linux 一起使用。有一点你必须考虑：通常内核不支持超过 64MB 的内存。当你添加超过 64MB 的内存时，必须在 LILO 配置文件中添加以下行：

```
append="mem=[number of Mb]M"
```

所以，当你有 96MB 内存时，应该变成这样：

```
append="mem=96M"
```

不要输入比你实际拥有的 MB 数更高的数字。这可能会导致不可预料的崩溃。

## 显卡

Linux 在文本模式下可以与所有显卡一起工作。下文中未列出的 VGA 卡可能仍可使用单色 VGA 或标准 VGA 驱动程序。

如果你打算购买一块便宜的显卡来运行 X，请记住，加速卡（ATI Mach、ET4000/W32p、S3）比非加速或部分加速（Cirrus、WD）卡快得多。

32 bpp 实际上是按 32 位边界对齐的 24 位颜色。这并不意味着这些卡能够显示 32 位颜色；它们仍然显示 24 位颜色（16,777,216 种颜色）。XFree86 不支持 24 位打包像素模式，因此在其他操作系统中可以通过 24 位模式获得更高分辨率的显卡，在使用 XFree86 的 X 中却无法做到这一点。这些卡包括 Mach32、Cirrus 542x、S3 801/805/868/968、ET4000 等。

AGP（加速图形端口）支持正在迅速发展。大多数 X 服务器（无论是免费版本还是商业版本）都或多或少地支持 AGP。

## DIAMOND 显卡

当前版本的 XFree86 支持目前大多数可用的 Diamond 卡。早期的 Diamond 卡可能不受 XFree86 官方支持，但有一些方法可以让它们工作。Diamond 现在积极支持 XFree86 项目。

## SVGALIB（控制台图形）

- VGA
- EGA
- ARK Logic ARK1000PV/2000PV
- ATI VGA Wonder
- ATI Mach32
- Cirrus 542x, 543x
- OAK OTI-037/67/77/87
- S3（有限支持）
- Trident TVGA8900/9000
- Tseng ET3000/ET4000/W32

## XFREE86 3.3.2

### 加速

- ARK Logic ARK1000PV/VL, ARK2000PV/MT
- ATI Mach8
- ATI Mach32（支持带有 RAMDAC ATI 68875、AT&T 20C49x、BT481 和 2MB 显存的卡以 16 bpp 运行）
- ATI Mach64（支持带有 RAMDAC ATI 68860、ATI 68875、CH8398、STG1702、STG1703、AT&T 20C408、3D Rage II、内部、IBM RGB514 的卡以 16/32 bpp 运行）
- Chips & Technologies 64200, 64300, 65520, 65525, 65530, 65535, 65540, 65545, 65546, 65548, 65550, 65554
- Cirrus Logic 5420, 542x/5430（16 bpp）, 5434（16/32 bpp）, 5436, 544x, 546x, 5480, 62x5, 754x
- Diamond Viper 330
- Gemini P1（ET6000 芯片）
- IBM 8514/A
- IBM XGA-1, XGA-II
- IIT AGX-010/014/015/016（16 bpp）
- Matrox MGA2044W（Millennium）
- Matrox MGA1064SG（Mystique）
- Number Nine Imagine I128
- Oak OTI-087
- S3 732（Trio32）, 764（Trio64）, Trio64V+, 801, 805, 864, 866, 868, 86C325（ViRGE）, 86C375（ViRGE/DX）, 86C385（ViRGE/GX）, 86C988（ViRGE/VX）, 911, 924, 928, 964, 968
- 有关受支持的 S3 卡列表，请参阅“XFree86 3.3.x 支持的 S3 卡”
- SiS 86c201, 86c202, 86c205
- Trident 9440, 96xx, Cyber938x
- Tseng ET4000/W32/W32i/W32p, ET6000
- Weitek P9000（16/32 bpp）
- Diamond Viper VLB/PCI
- Orchid P9000
- Western Digital WD90C24/24A/24A2/31/33

### 非加速

- Alliance AP6422, AT24
- ATI VGA Wonder 系列
- Avance Logic AL2101/2228/2301/2302/2308/2401
- Cirrus Logic 6420/6440, 7555
- Compaq AVGA
- DEC 21030
- Genoa GVGA
- MCGA（320x200）
- MX MX68000/MX68010
- NCR 77C22, 77C22E, 77C22E+
- NVidia NV1
- Oak OTI-037C, OTI-067, OTI-077
- RealTek RTG3106
- SGS-Thomson STG2000
- Trident 8800CS, 8200LX, 8900x, 9000, 9000i, 9100B, 9200CXr, 9320LCD, 9400CXi, 9420, 9420DGi, 9430DGi
- Tseng ET3000, ET4000AX
- VGA（标准 VGA，4 位，速度慢）
- Video 7/Headland Technologies HT216-32
- Western Digital/Paradise PVGA1, WD90C00/10/11/30

### 单色

- Hercules 单色
- Hyundai HGC-1280
- Sigma LaserView PLUS
- VGA 单色

### ALPHA、BETA 驱动程序

- EGA（古老的，约 1992 年）
  - `ftp://ftp.funet.fi/pub/Linux/BETA/Xega/`

## SuSE X 服务器

SuSE 正在基于 XFree86 代码构建一系列 X 服务器。这些 X 服务器支持新的显卡，并且是 XFree86 X 服务器的错误修复版本。SuSE 正在与 The XFree86 Project, Inc. 一起构建这些 X 服务器。这些 X 服务器将包含在下一个 XFree86 版本中，可以在 http://www.suse.de/index.html 找到。目前，SuSE X 服务器可用于以下显卡：

- XSuSE Elsa GLoria X 服务器
  - ELSA GLoria L、GLoria L/MX、Gloria S
- 采用 Alliance Semiconductor AT3D（以及 AT25）芯片的显卡
  - Hercules Stingray 128 3D
- XSuSE NVidia X 服务器（支持 PCI 和 AGP、NV1 芯片组和 Riva128）
  - ASUS 3DExplorer
  - Diamond Viper 330
  - ELSA VICTORY Erazor
  - STB Velocity 128
- XSuSE Matrox。支持 Mystique、Millennium、Millennium II 和 Millennium II AGP
- XSuSE Trident。支持 9685（包括 ClearTV）和最新的 Cyber 芯片组
- XSuSE Tseng。支持 W32、W32i ET6100 和 ET6300。

## 商业 X 服务器

商业 X 服务器为 XFree86 不支持的显卡提供支持，并且可能为 XFree86 支持的显卡提供更好的性能。总的来说，它们支持的显卡比 XFree86 多得多，因此这里我只列出 XFree86 不支持的显卡。请直接联系供应商或查看 Commercial HOWTO 以获取更多信息。

### XI GRAPHICS, INC

Xi Graphics, Inc，前身为 X Inside, Inc（http://www.xig.com），销售三种 X 服务器产品。（支持的显卡按制造商排序。）：

### ACCELERATED-X DISPLAY SERVER

- 3Dlabs
  - 300SX
  - 500TX Glint
  - 500MX Glint
  - Permedia 4MB/8MB
  - Permedia II 4MB/8MB
- Actix
  - GE32plus 1MB/2MB
  - GE32ultra 2MB
  - GraphicsENGINE 64 1MB/2MB
  - ProSTAR 64 1MB/2MB
- Alliance
  - ProMotion-3210 1MB/2MB
  - ProMotion-6410 1MB/2MB
  - ProMotion-6422 1MB/2MB
- ARK Logic
  - ARK1000PV 1MB/2MB
  - ARK1000VL 1MB/2MB
  - ARK2000PV 1MB/2MB
- AST
  - Manhattan 5090P (GD5424) 512KB
- ATI
  - 3D Xpression 1MB/2MB
  - 3D Pro Turbo PC2TV 4MB/8MB
  - 3D Pro Turbo PC2TV 6144

