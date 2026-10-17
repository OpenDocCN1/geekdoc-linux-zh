
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

SuSE 正在基于 XFree86 代码构建一系列 X 服务器。这些 X 服务器支持新的显卡，并且是 XFree86 X 服务器的错误修复版本。SuSE 正在与 The XFree86 Project, Inc. 一起构建这些 X 服务器。这些 X 服务器将包含在下一个 XFree86 版本中，可以在 `http://www.suse.de/index.html` 找到。目前，SuSE X 服务器可用于以下显卡：

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

Xi Graphics, Inc，前身为 X Inside, Inc（`http://www.xig.com`），销售三种 X 服务器产品。（支持的显卡按制造商排序。）

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
- **ATI**
  - 3D Xpression+ PC2TV 2MB/4MB
  - 3D Xpression+ 2MB/4MB
  - ALL-IN-WONDER 4MB/8MB
  - ALL-IN-WONDER PRO 4MB/8MB
  - Graphics Ultra (Mach8) 1MB
  - Graphics Pro Turbo (Mach64/VRAM) 2MB/4MB
  - Graphics Pro Turbo 1600 (Mach64/VRAM) 2MB/4MB
  - Graphics Ultra Plus (Mach32) 2MB
  - 8514/Ultra (Mach8) 1MB
  - Graphics Ultra Pro (Mach32) 1MB/2MB
  - Graphics Vantage (Mach8) 1MB
  - VGA Wonder Plus 512KB
  - VGA Wonder XL 1MB
  - Video Xpression 1MB
  - XPERT@Play 4MB/6MB/8MB
  - XPERT@Work 4MB/6MB/8MB
  - Video Xpression 2MB
  - WinBoost (Mach64/DRAM) 2MB
  - WinTurbo (Mach64/VRAM) 2MB
  - Graphics Wonder (Mach32) 1MB
  - Graphics Xpression 1MB/2MB
  - Rage II (SGRAM) 2MB/4MB/8MB
  - Rage II+ (SGRAM) 2MB/4MB/8MB
  - Rage Pro 2MB/4MB/8MB

- **Avance Logic**
  - ALG2101 1MB
  - ALG2228 1MB/2MB
  - ALG2301 1MB/2MB

- **Boca**
  - Voyager 1MB/2MB
  - Vortek-VL 1MB/2MB

- **Colorgraphic**
  - Dual Lightning 2MB
  - Pro Lightning Accelerator 2MB
  - Quad Pro Lightning Accelerator 2MB
  - Twin Turbo Accelerator 1MB/2MB

- **Chips & Technology**
  - 64300 1MB/2MB
  - 64310 1MB/2MB
  - 65510 512KB
  - 65520 1MB
  - 65530 1MB
  - 65535 1MB
  - 65540 1MB
  - 65545 1MB
  - 65550 2MB
  - 82C450 512KB
  - 82C451 256KB
  - 82C452 512KB
  - 82C453 1MB
  - 82C480 1MB/2MB
  - 82C481 1MB/2MB

- **Cirrus Logic**
  - GD5402 512KB
  - GD5420 1MB
  - GD5422 1MB
  - GD5424 1MB
  - GD5426 1MB/2MB
  - GD5428 1MB/2MB
  - GD5429 1MB/2MB
  - GD5430 1MB/2MB
  - GD5434 1MB/2MB
  - GD5436 1MB/2MB
  - GD5440 1MB/2MB
  - GD5446 1MB/2MB
  - GD5462 2MB/4MB PCI 和 AGP
  - GD5464 2MB/4MB PCI 和 AGP
  - GD5465 2MB/4MB PCI 和 AGP
  - GD54M30 1MB/2MB
  - GD54M40 1MB/2MB

- **Compaq**
  - ProLiant Series 512KB
  - ProSignia Series 512KB
  - QVision 1024 1MB
  - QVision 1280 1MB/2MB
  - QVision 2000+ 2MB
  - QVision 2000 2MB

- **DEC**
  - DECpc XL 590 (GD5428) 512KB

- **Dell**
  - 466/M & 466/ME (S3 805) 1MB
  - 板载 ET4000 1MB
  - DGX (JAWS) 2MB
  - OptiPlex XMT 590 (Vision864) 2MB

- **Diamond**
  - Fire GL 1000 Pro 4MB/8MB
  - Fire GL 1000 4MB/8MB
  - Stealth 3D 2000 2MB/4MB
  - Stealth 3D 3000XL 2MB/4MB
  - Stealth 64 Graphics 2001 1MB/2MB
  - Stealth 64 Graphics 2121XL 1MB/2MB
  - Stealth 64 Graphics 2201XL 2MB
  - SpeedStar 1MB
  - SpeedStar 64 Graphics 2000 1MB/2MB
  - SpeedStar 24 1MB
  - SpeedStar 24X 1MB
  - SpeedStar 64 1MB/2MB
  - SpeedStar Hicolor 1MB
  - SpeedStar PCI 1MB
  - SpeedStar Pro 1MB
  - SpeedStar Pro SE 1MB/2MB
  - Stealth 1MB
  - Stealth 24 1MB
  - Stealth 32 1MB/2MB
  - Stealth 64 VRAM 2MB/4MB
  - Stealth 64 DRAM 1MB/2MB
  - Stealth 64 Video VRAM (175MHz) 2MB/4MB
  - Stealth 64 Video DRAM 1MB/2MB
  - Stealth 64 Video VRAM (220MHz) 2MB/4MB
  - Stealth Hicolor 1MB
  - Stealth Pro 1MB/2MB
  - Stealth SE 1MB/2MB
  - Stealth 64 Video 2001TV 2MB
  - Stealth 64 Video 2121 1MB/2MB
  - Stealth 64 Video 2121TV 1MB/2MB
  - Stealth 64 Video 2201 2MB
  - Stealth 64 Video 2201TV 2MB
  - Stealth 64 Video 3200 2MB
  - Stealth 64 Video 3240 2MB/4MB
  - Stealth 64 Video 3400 4MB
  - Viper 1MB/2MB
  - Viper Pro 2MB
  - Viper Pro Video 2MB/4MB
  - Viper SE 2MB/4MB

- **ELSA**
  - VICTORY 3D 2MB/4MB
  - WINNER 1000 1MB/2MB
  - WINNER 1000AVI 1MB/2MB
  - WINNER 1000ISA 1MB/2MB
  - WINNER 1000PRO 1MB/2MB
  - WINNER 1000TRIO 1MB/2MB
  - WINNER 1000TRIO/V 1MB/2MB
  - WINNER 1000VL 1MB
  - WINNER 2000 2MB/4MB
  - WINNER 2000AVI 2MB/4MB
  - WINNER 2000AVI/3D 2MB/4MB
  - WINNER 2000PRO 2MB/4MB
  - WINNER 2000PRO/X 2MB/4MB/8MB
  - WINNER 3000-L 4MB
  - WINNER 3000-L 2MB
  - WINNER 3000-S 2MB
  - WINNER 1024 1MB
  - WINNER 1280, TLC34075 调色板 2MB
  - WINNER 1280, TLC34076 调色板 2MB
  - Gloria-XL
  - Gloria-MX
  - Gloria-L
  - Synergy

- **Everex**
  - ViewPoint 64P 1MB/2MB
  - VGA Trio 64P 1MB/2MB

- **Gateway**
  - Mach64 Accelerator (Mach64/VRAM) 2MB

- **Genoa**
  - 5400 512KB
  - 8500/8500VL 1MB
  - Phantom 32i 8900 2MB
  - Phantom 64 2MB

- **Hercules**
  - Dynamite 1MB
  - Dynamite Pro 1MB/2MB
  - Dynamite Power 2MB
  - Dynamite 3D / GL
  - Graphite 1MB
  - Stingray 64 1MB/2MB
  - Stingray Pro 1MB/2MB
  - Stingray 1MB
  - Terminator 3D 2MB/4MB
  - Terminator 64/Video 2MB
  - Graphite Terminator Pro 2MB/4MB

- **HP**
  - NetServer Lf/LC/LE (TVGA9000i) 512KB
  - Vectra VL2 (GD5428) 1MB
  - Vectra XM2i (Vision864) 1MB/2MB
  - Vectra XU (Vision864) 1MB/2MB

- **IBM**
  - 8514/A 1MB
  - PC 300 Series (GD5430) 1MB
  - PC 300 Series (Vision864) 1MB/2MB
  - PC 700 Series (Vision864) 1MB/2MB
  - PS/ValuePoint Performance Series (Vision864) 1MB/2MB
  - VC550 1MB
  - VGA 256KB
  - XGA-NI 1MB
  - XGA 1MB

- **IIT**
  - AGX014 1MB
  - AGX015 1MB/2MB

- **Integral**
  - FlashPoint 1MB/2MB

- **Leadtek**
  - WinFast L2300 4MB/8MB

- **Matrox**
  - Comet 2MB
  - Marvel II 2MB
  - Impression (MGA-IMP/3/A/H, MGA-IMP/3/V/H, MGA-IMP/3/M/H) 3MB
  - Impression Lite (MGA-IMP+/L/TE/P) 2MB
  - Impression Plus Lite (MGA-IMP+/L/TE/V) 2MB
  - Millennium (MGA-MIL) 2MB/4MB/8MB
  - Millennium 220 (MGA-MIL) 2MB/4MB/8MB
  - Millennium PowerDoc (WRAM) 2MB/4MB/8MB
  - Millennium II (WRAM) 2MB/4MB/8MB PCI 和 AGP
  - Mystique (MGA-MYS) 2MB/4MB
  - Mystique 220
  - Impression Plus (MGA-IMP+/P, MGA-IMP+/A) 2MB/4MB
  - Impression Plus 220 (MGA-IMP+/P/H, MGA-IMP+/A/H) 2MB/4MB
  - Impression Pro (MGA-PRO/4.5/V) 4.5MB
  - Ultima Plus (MGA-PCI/2+, MGA-VLB/2+) 2MB/4MB
  - Ultima (MGA-ULT/2/A, MGA-PCI/2, MGA-VLB/2) 2MB
  - Ultima (MGA-ULT/2/A/H, MGA-ULT/2/M/H) 2MB
  - Ultima Plus 200 (MGA-PCI/4/200, MGA-VLB/4/200) 4MB

- **MaxVision**
  - VideoMax 2000 2MB/4MB

- **Metheus**
  - Premier 801 1MB
  - Premier 928-1M 1MB
  - Premier 928-2M 2MB
  - Premier 928-4M 4MB

- **Micronics**
  - Mpower 4 Plus (Mach64) 1MB

- **MIRO**
  - miroCRYSTAL 10AD 1MB
  - miroCRYSTAL 12SD 1MB
  - miroCRYSTAL 12SD 2MB
  - miroCRYSTAL 20PV 2MB
  - miroCRYSTAL 20SD 2MB
  - miroCRYSTAL 20SV 2MB
  - miroCRYSTAL 22SD 2MB
  - miroCRYSTAL 40SV 4MB
  - miroCRYSTAL VR2000 2MB/4MB
  - miroMAGIC 40PV 4MB
  - miroMAGIC plus 2MB
  - miroVIDEO 12PD 1MB/2MB
  - miroVIDEO 20SD 2MB
  - miroVIDEO 20SV 2MB
  - miroVIDEO 20TD 2MB
  - miroVIDEO 22SD 2MB
  - miroVIDEO 40SV 4MB

- **NEC**
  - Versa P Series 1MB

- **Nth Graphics**
  - Engine/150 2MB
  - Engine/250 2MB

- **Number Nine**
  - GXE Level 10, AT&T 20C491 调色板 1MB
  - GXE Level 10, Bt485 或 AT&T20C505 调色板 1MB
  - GXE Level 11 2MB
  - GXE Level 12 3MB
  - GXE Level 14 4MB
  - GXE Level 16 4MB
  - GXE64 1MB/2MB
  - GXE64pro 2MB/4MB
  - GXE64pro (-1600) 2MB/4MB
  - Imagine 128 2MB
  - Imagine 128 (-1280) 4MB
  - Imagine 128 Series 2 (DRAM) 2MB/4MB
  - Imagine 128 Pro (-1600) 4MB/8MB
  - Imagine 128 Series 2 (VRAM) 2MB/4MB/8MB
  - Imagine 128 Series III (Revolution 3D) (WRAM) 8MB/16MB PCI 和 AGP
  - Revolution 3D “Ticket to Ride” (WRAM) 8MB/16MB PCI 和 AGP
  - 9FX Motion331 1MB/2MB
  - 9FX Motion531 1MB/2MB
  - 9FX Motion771 2MB/4MB
  - 9FX Reality332 2MB
  - 9FX Reality772 2MB/4MB
  - 9FX Reality 334 PCI 和 AGP
  - 9FX Vision330 1MB/2MB

- **Oak Technology**
  - OTI-067 512KB
  - OTI-077 1MB
  - OTI-087 1MB
  - OTI-107 1MB/2MB
  - OTI-111 1MB/2MB

- **Orchid**
  - Fahrenheit 1280 Plus, AT&T 20C491 调色板 1MB
  - Fahrenheit 1280 1MB
  - Fahrenheit 1280 Plus, SC15025 调色板 1MB
  - Fahrenheit ProVideo 64 2MB/4MB
  - Fahrenheit Video 3D 2MB
  - Kelvin 64 1MB/2MB
  - Kelvin Video64 1MB/2MB
  - P9000 2MB

- **Packard Bell**
  - Series 5000 主板 1MB

- **Paradise**
  - 8514/A 1MB
  - Accelerator 24 1MB
  - Accelerator Value card 1MB
  - Bahamas 64 1MB/2MB
  - Bali 32 1MB/2MB
  - VGA 1024 512KB
  - VGA Professional 512KB

- **Pixelworks**
  - WhirlWIN WL1280 (110MHz) 2MB
  - WhirlWIN WL1280 (135MHz) 2MB
  - WhirlWIN WW1280 (110MHz) 2MB
  - WhirlWIN WW1280 (135MHz) 2MB
  - WhirlWIN WW1600 1MB

- **Radius**
  - XGA-2 1MB

- **Reveal**
  - VC200 1MB
  - VC300 1MB
  - VC700 1MB

- **S3**
  - ViRGE 2MB/4MB
  - ViRGE/DX 2MB/4MB
  - ViRGE/GX 2MB/4MB
  - ViRGE/GX /2 2MB/4MB
  - ViRGE/VX 2MB/4MB
  - Trio32 1MB/2MB
  - Trio64 1MB/2MB
  - Trio64V+ 1MB/2MB
  - Trio64V2/DX 1MB/2MB
  - Trio64V2/GX 1MB/2MB
  - 801 1MB/2MB
  - 805 1MB/2MB
  - Vision864 1MB/2MB
  - Vision866 1MB/2MB
  - Vision868 1MB/2MB
  - 911 1MB
  - 924 1MB
  - 928 1MB
  - 928 2MB/4MB

- Sierra（西拉）
  - Falcon/64 1MB/2MB

- Sigma（西格玛）
  - Legend 1MB
  - SPEA/V7
  - Mercury P64 2MB
  - Storm Pro +4MB
  - ShowTime Plus 2MB

- STB
  - Evolution VGA 1MB
  - Horizon Plus 1MB
  - Horizon VGA 1MB
  - Horizon 64 1MB/2MB
  - Horizon 64 Video 1MB/2MB
  - Horizon Video 1MB
  - LightSpeed 2MB
  - LightSpeed 128 2MB
  - Nitro 3D 2MB/4MB
  - Nitro 64 1MB/2MB
  - Nitro 64 Video 1MB/2MB
  - PowerGraph VL-24 1MB
  - PowerGraph X-24 1MB
  - PowerGraph 64 3D 2MB
  - PowerGraph 64 1MB/2MB
  - PowerGraph 64 Video 1MB/2MB
  - PowerGraph Pro 2MB
  - Velocity 3D 4MB
  - Velocity 64V 2MB/4MB

- 东芝（Toshiba）
  - T4900CT 1MB

- Trident（泰鼎）
  - TGUI9400CXi 1MB/2MB
  - TGUI9420DGi 1MB/2MB
  - TGUI9440 1MB/2MB
  - TGUI9660 1MB/2MB
  - TGUI9680 1MB/2MB
  - TVGA8900B 1MB
  - TVGA8900C 1MB
  - TVGA8900CL 1MB
  - TVGA8900D 1MB
  - TVGA9000 512KB
  - TVGA9000i 512KB
  - TVGA9200CXr 1MB/2MB

- Tseng Labs
  - ET3000 512KB
  - ET4000 1MB
  - ET6000 2MB/4MB
  - VGA/16 (ISA) 1MB
  - VGA/16 (VLB) 1MB/2MB
  - VGA/32 1MB/2MB
  - ET4000/W32 1MB
  - ET4000/W32i 1MB/2MB
  - ET4000/W32p 1MB/2MB

- VLSI
  - VL82C975 (AT&T RAMDAC) 2MB
  - VL82C975 (BrookTree RAMDAC) 2MB
  - VL82C976 (Internal RAMDAC) 2MB

- 西数（Western Digital）
  - WD90C00 512KB
  - WD90C11 512KB
  - WD90C24 1MB
  - WD90C26 512KB
  - WD90C30 1MB
  - WD90C31 1MB
  - WD90C33 1MB
  - WD9510-AT 1MB

- Weitek
  - P9100 2MB
  - P9000 2MB
  - W5186 1MB
  - W5286 1MB

## 笔记本电脑 ACCELERATED-X 显示服务器

- Broadax
  - NP8700 (Cyber 9385)

- Chips & Technologies
  - 65510 512KB
  - 65520 1MB
  - 65530 1MB
  - 65535 1MB
  - 65540 1MB
  - 65545 1MB
  - 65554 2MB/4MB
  - 65555 2MB

- Cirrus Logic
  - GD7541 1MB/2MB
  - GD7543 1MB/2MB
  - GD7548 2MB

- 康柏（Compaq）
  - LTE 5400 (Cirrus Logic CL5478)
  - Presario 1090ES (NM 2093)

- 戴尔（Dell）
  - Latitude XPi 896 (NeoMagic 2070)
  - Latitude XPi (NM 2070)
  - Latitude XPi CD 1MB (NM 2090)
  - Latitude LM (NM 2160)
  - Latitude CP (NM 2160)
  - Inspiron 3000 (NM 2160)

- 迪吉多（Digital，DEC）
  - HiNote VP (NeoMagic 2090)

- 富士通（Fujitsu）
  - Lifebook 435DX (NeoMagic 2093)

- Gateway 2000
  - Solo 2300 (NeoMagic 2160)
  - Solo 2300 SE (NM 2160)
  - Solo 9100 (C&T 65554)
  - Solo 9100XL (C&T 65555)

- 惠普（Hewlett Packard）
  - OmniBook 800 (NM 2093)

- 日立（Hitachi）
  - Notebook E133T (NeoMagic 2070)

- IBM
  - VGA 256KB
  - Thinkpad 380D (NeoMagic 2090)
  - Thinkpad 385ED (NeoMagic 2090)*
  - Thinkpad 560E (Cyber 9382)
  - Thinkpad 760XD (Cyber 9385)
  - Thinkpad 770 (Cyber 9397)

- Micron
  - TranSport XKE (NeoMagic 2160)
  - Millennia Transport (Cirrus Logic GD7548)

- NEC
  - Versa P Series 1MB
  - Versa 6230 2MB (NeoMagic 2160)

- NeoMagic
  - MagicGraph128 / NM2070 896
  - MagicGraph128 / NM2070
  - MagicGraph128V / NM2090
  - MagicGraph128V+ / NM2097
  - MagicGraph128ZV / NM2093
  - MagicGraph128XD / NM2160

- 索尼（Sony）
  - VAIO PCG-505 (NeoMagic 2097)

- 东芝（Toshiba）
  - T4900CT 1MB
  - Tecra 740CDT (C&T 65554)

- Trident（泰鼎）
  - Cyber 9397
  - Cyber 9385
  - Cyber 9382

- Twinhead
  - Slimnote 9166TH (Cyber 9385)

\* 众多 XiG 客户已确认支持。

## 多显示器 ACCELERATED-X 显示服务器

**METRO-X 4.3.0** Metro Link sales@metrolink.com

### 表 B.1 支持的显卡

| 显卡 | 显卡芯片组 |
|---|---|
| ATI 3D RAGE | 3D RAGE |
| ATI 3D RAGE II | 3D RAGE II |
| ATI ALL-IN-WONDER PRO AGP | 3D RAGE PRO |
| ATI ALL-IN-WONDER PRO PCI | 3D RAGE PRO |
| ATI Graphics Pro Turbo | Mach64 |
| ATI Graphics Ultra | Mach8 |
| ATI Graphics Xpression | Mach64 |
| ATI Mach32 | Mach32 |
| ATI Mach64 | Mach64 |
| ATI VGA STEREO-F/X | ATI 28800 |
| ATI Winturbo PCI | Mach64 |
| ATI XPERT@Play | 3D RAGE PRO |
| ATI XPERT@Play AGP | 3D RAGE PRO |
| ATI XPERT@Work | 3D RAGE PRO |
| ATI XPERT@Work AGP | 3D RAGE PRO |
| Diamond Fire GL 1000Pro | PERMEDIA 2 |
| Diamond SpeedStar 24X | Western Digital 90C31 |
| Diamond SpeedStar Pro SE | Cirrus 5430 |
| Diamond Stealth 24 | S3 801 |
| Diamond Stealth 32 | ET4000/W32p |
| Diamond Stealth 3D 2000 | S3 ViRGE |
| Diamond Stealth 64 | S3 964, Bt485KPJ135 |
| Diamond Stealth 64 DRAM | S3 Trio64 |
| Diamond Stealth 64 DRAM (SDAC) | S3 864, S3 SDAC |
| Diamond Stealth 64 Graphics 2000 Series | S3 864, S3 SDAC |
| Diamond Stealth 64 Graphics 2200 | S3 Trio64 |
| Diamond Stealth 64 VRAM | S3 968, IBM RGB526CF22 |
| Diamond Stealth 64 Video 3000 Series | S3 968, TI 3026-175 |
| Diamond Stealth 64 Video VRAM | S3 968, TI 3026-175 |
| Diamond Stealth Video (SDAC) | S3 868, S3 SDAC |
| Diamond Stealth Video 2000 Series | S3 868, S3 SDAC |
| Diamond Viper (110 MHz RAMDAC) | P9000 |
| Diamond Viper (135 MHz RAMDAC) | P9000 |
| ELSA Gloria Synergy | PERMEDIA 2 |
| ELSA Victory 3D | S3 ViRGE |
| ELSA WINNER 2000 Office AGP | PERMEDIA 2 |
| ELSA Winner 2000 TRIO/V | S3 Trio64V+ |
| ELSA Winner 2000 AVI | S3 968, TI 3026-175 |
| ELSA Winner 2000 PRO/X-2, -4 | S3 968, TI 3026-220 |
| ELSA Winner 2000 PRO/X-8 | S3 968, IBM RGB5280CF25 |
| EPS Apex L-200 | C&T 65550 |
| 通用 | ATI 28800 |
| 通用 | Alliance ProMotion |
| 通用 | Ark 2000 |
| 通用 | Avance Logic 22xx/23xx/24xx |
| 通用 | Chips & Technologies |
| 通用 | Cirrus 5420 |
| 通用 | Cirrus 5422/5424 |
| 通用 | Cirrus 5426/5428 |
| 通用 | Cirrus 5429 |
| 通用 | Cirrus 5430 |
| 通用 | Cirrus 5434 |
| 通用 | Cirrus 5436 |
| 通用 | Cirrus 5446 |
| 通用 | Cirrus 5462 |
| 通用 | Cirrus 5462/5465 |
| 通用 | Cirrus 5480 |
| 通用 | Cirrus 62x5 |
| 通用 | Cirrus 6410/6412/6420/6440 |
| 通用 | Cirrus 754x |
| 通用 | ET3000 |
| 通用 | ET4000/W32P |
| 通用 | ET4000AX |
| 通用 | ET6000 |
| 通用 | Mach32 |
| 通用 | Mach64 |
| 通用 | Mach8 |
| 通用 | P9000 |
| 通用 | PERMEDIA 2 |
| 通用 | S3 864/868/924/928/964 |
| 通用 | S3 968 |
| 通用 | S3 Trio64 |
| 通用 | S3 Trio64V+ |
| 通用 | S3 ViRGE |
| 通用 | S3 ViRGE/GX/DX |
| 通用 | SiS 86c201/86c202/86c205 |
| 通用 Trident | TGUI9440 |
| 通用 Trident | TGUI96xx |
| 通用 | Trident8900 |
| 通用 | VGA |
| 通用 | Western Digital SVGA |
| Genoa Phantom 64 | S3 Trio64V+ |
| Genoa WindowsVGA 8500VL | Cirrus 5426 |
| Hercules Dynamite 128/Video | ET6000 |
| Hercules Dynamite 3D/GL | PERMEDIA 2 |
| Hercules Dynamite 3D/GL AGP | PERMEDIA 2 |
| Hercules Stingray | Advance Logic 2301 |
| Hercules Stingray 128/3D | Alliance ProMotion AT3D |
| Hercules Stingray 64 | Ark 2000 |
| Hercules Terminator 3D | S3 ViRGE/DX |
| IBM VGA |  |
| Matrox Marvel | ET4000 |
| Matrox Marvel II | ET4000 |
| Matrox Millennium | MGA Storm |
| Matrox Millennium II AGP | MGA 2164, TI 3026-250 |
| Matrox Millennium II PCI (220 MHz) | MGA 2164, TI 3026-220 |
| Matrox Millennium II PCI (250 MHz) | MGA 2164, TI 3026-250 |
| Matrox Mystique | MGA 1064 |
| Matrox Mystique 220 | MGA 1164 |
| Number Nine GXE64 | S3 864 |
| Number Nine Imagine 128 | Imagine 128 |
| Number Nine Imagine 128 Series 2 | Imagine 128 Series 2 |
| Number Nine Motion 531 | S3 868 |

**表 B.1 续**

| 显卡 | 显卡芯片组 |
| --- | --- |
| Number Nine Motion 771 | S3 968 |
| Number Nine Revolution 3D | Ticket to Ride |
| Number Nine Vision 330 | S3 Trio64 |
| Orchid Kelvin 64 | Cirrus 5434 |
| SPEA Mirage Video | S3 Trio64V+ |
| STB NITRO 3D | S3 ViRGE/GX |
| STB/Symmetric GLyder MAX-2 | PERMEDIA 2 |
| Sigma Designs VGA Legend | ET4000 |
| Tech Source Raptor | Imagine 128 Series 2 |
| Trident 64-Bit ProVidia 9685 |  |
| Trident 8900 | Trident 8900 |
| Trident 9440 | TGUI9440-2 |
| V PCI-53 | Cirrus 5434 |

## 控制器（硬盘）

Linux 可以配合标准的 IDE、MFM 和 RLL 控制器工作。使用 MFM/RLL 控制器时，格式化磁盘务必使用 ext2fs 并启用坏块检查选项。

支持增强型 IDE（EIDE）接口，最多可连接两个 IDE 接口和四个硬盘或 CD-ROM 驱动器。Linux 可识别以下 EIDE 接口：

- CMD-640（在 2.2 内核中支持有缺陷的接口）
- DTC 2278D
- FGI/Holtek HT-6560B VLB（在 2.2 内核中支持辅助接口）
- RZ1000（在 2.2 内核中支持有缺陷的接口）
- Triton I（82371FB）（支持总线主控 DMA）
- Triton II（82371SB）（支持总线主控 DMA）

模拟 ST-506（MFM/RLL/IDE）接口的 ESDI 控制器也可以使用。关于坏块检查的说明同样适用于这些控制器。

通用的 8 位 XT 控制器也可以使用。

从 pre-patch-2.0.31-3 开始提供 IDE/ATAPI 支持。

### Alpha、Beta 驱动程序

- UMC 8672 接口（2.2 内核中的实验性支持）
- Promise DC4030VL 缓存接口卡（2.2 内核中的实验性支持）

## 控制器（硬盘 RAID）

- Tekram D690CD IDE PCI 缓存控制器（支持 RAID 1 镜像和缓存）
- ARCO Inc. DupliDisk IDE 磁盘镜像控制器
    - 支持 ATA、IDE、E-IDE 和 UDMA 驱动器。可用的控制器可插入 ISA 和 PCI 插槽，也可直接插入 IDE 控制器。此外，还提供适用于相应驱动器托架的 3.5 英寸和 5.25 英寸托架安装单元。更多信息请访问 `http://www.arcoide.com`。确保固件版本至少为 3.00。
- Mylex RAID 控制器
    - 更多信息可在 `http://www.dandelion.com/Linux/DAC960.html` 找到。

## 控制器（SCSI）

仔细选择 SCSI 控制器非常重要。许多廉价的 ISA SCSI 控制器是为驱动 CD-ROM 而设计的，而非用于其他设备。这种低端 SCSI 控制器并不比 IDE 好。购买 SCSI 卡之前，请参阅 SCSI HOWTO 并查看性能数据。

### 已支持

- AMI Fast Disk（**VLB/EISA**）（兼容 BusLogic）
- Adaptec AVA-1502E（**ISA/VLB**）（AIC-6360）（AHA1520）
- Adaptec AVA-1505/1515（**ISA**）（兼容 Adaptec AHA-152x）
- Adaptec AVA-1825（**VLB**）（兼容 Adaptec AHA-152x）
    - 此卡具有 SCSI、EIDE 和软盘端口，均能正常工作。
- Adaptec AHA-1510/152x（**ISA/VLB**）（AIC-6260/6360）
- Adaptec AHA-154x（**ISA**）（所有型号）
- Adaptec AHA-174x（**EISA**）（增强模式）
- Adaptec AHA-274x/274x-T（**EISA**）（AIC-7771）。自 2.1.x 内核系列起支持 274x-T（AHA2740）
- Adaptec AHA-284x（**VLB**）（AIC-7770）（AHA2740）
- Adaptec AHA-2910B（**PCI**）（自 2.1.x 内核系列起支持）
- Adaptec AHA-2920（PCI）。使用 Future Domain 驱动程序。用于硬盘时需要 LILO 参数。
- Adaptec AHA-2920C（PCI）
- Adaptec AHA-2930/U/U2（PCI）
- Adaptec AHA-2940/U/UW/AUW/U2W/U2/U2B/U2B OEM（PCI）（AIC-7861、AIC-7871、AIC-7844、AIC-7881、AIC-7884）。其中一些仅自 2.1.x 内核系列起支持（AHA2740）。
- Adaptec AHA-2944D/WD/UW/UWD（PCI）。其中一些仅自 2.1.x 内核系列起支持（AHA2740）。
- Adaptec AHA-2950U2/U2B/U2W
- Adaptec AHA-3940/U/W/UW/AUW/U2W（PCI）（AIC-7872、AIC-7882）（自 1.3.6 起）。其中一些仅自 2.1.x 内核系列起支持。
- Adaptec AHA-3950U2B/U2D
- Adaptec AHA-3985U/W/UW（PCI）（AIC-7873、AIC-7883）。其中一些仅自 2.1.x 内核系列起支持。
- 使用 AIC-7850、AIC-7855、AIC-7860 的 Adaptec PCI 控制器
- 使用 AIC-777x（EISA）、AIC-785x、AIC-786x、AIC-787x（PCI）、AIC-788x（PCI）、AIC-789x、AIC-3860、AIC-7869x 的 Adaptec 板载控制器自 2.1.x 内核系列起支持。
- Advansys ABP510/5150 总线主控（ISA）：`http://advansys.com/support/software/os/linux.htm`
- Advansys ABP5140 总线主控（ISA）即插即用：`http://advansys.com/support/software/os/linux.htm`
- Advansys ABP5142 总线主控（ISA）即插即用（带软盘）：`http://advansys.com/support/software/os/linux.htm`
- Advansys ABP920 总线主控（PCI）：`http://advansys.com/support/software/os/linux.htm`
- Advansys ABP930/U 总线主控（PCI/Ultra）：`http://advansys.com/support/software/os/linux.htm`
- Advansys ABP960/U 总线主控（PCI/Ultra）MAC/PC：`http://advansys.com/support/software/os/linux.htm`
- Advansys ABP542 总线主控（ISA）带软盘（单通道）：`http://advansys.com/support/software/os/linux.htm`
- Advansys ABP742 总线主控（EISA）（单通道）：`http://advansys.com/support/software/os/linux.htm`
- Advansys ABP842 总线主控（VL）（单通道）：`http://advansys.com/support/software/os/linux.htm`
- Advansys ABP940/U 总线主控（PCI/Ultra）（单通道）：`http://advansys.com/support/software/os/linux.htm`
- Advansys ABP970/U 总线主控（PCI/Ultra）MAC/PC（单通道）：`http://advansys.com/support/software/os/linux.htm`
- Advansys ABP752 双通道总线主控（EISA）（双通道）：`http://advansys.com/support/software/os/linux.htm`
- Advansys ABP852 双通道总线主控（VL）（双通道）：`http://advansys.com/support/software/os/linux.htm`
- Advansys ABP950 双通道总线主控（PCI）（双通道）：`http://advansys.com/support/software/os/linux.htm`
- Always IN2000
- AMD AM53C974
- BusLogic FlashPoint LT/DL/LW/DW（BT-930(R)、BT-920、BT-932(R)、BT-950(R)、BT-952(R)）：`http://www.dandelion.com/Linux/`
- Compaq Smart Array 2
- DPT PM2001、PM2012A（EATA-PIO）
- DPT Smartcache/SmartRAID Plus、III、IV 系列（ISA/EISA/PCI）
    - 请查看 `http://www.uni-mainz.de/~neuffer/scsi/dpt/`（EATA-DMA）
    - 这些系列中的卡包括 PM2011、PM2021、PM2041、PM3021、PM2012B、PM2022、PM2122、PM2322、PM2042、PM3122、PM3222、PM3332、PM2024、PM2124、PM2044、PM3124、PM3224 和 PM3334。
- DTC 3180/3280
- DTC 329x（EISA）（兼容 Adaptec 154x）
- Future Domain TMC-16x0、TMC-3260（PCI）
- Future Domain TMC-8xx、TMC-950
- Future Domain 芯片 TMC-18C00、TMC-18C50、TMC-18C30、TMC-36C70
- ICP-Vortex PCI-SCSI 磁盘阵列控制器（支持多种 RAID 级别）
    - 适用于 Linux 2.1.13 和 2.0.29 的补丁可在 `ftp://icp-vortex.com/download/linux/` 获取。支持以下控制器：GDT6111RP、GDT6121RP、GDT6117RP、GDT6127RP、GDT6511RP、GDT6521RP、GDT6517RP、GDT6527RP、GDT6537RP 和 GDT6557RP。也可以使用 pre-patch-2.0.31-4 至 pre-patch-2.0.31-9。
- ICP-Vortex EISA-SCSI 控制器（支持多种 RAID 级别）
    - 适用于 Linux 1.2.13 和 2.0.29 的补丁可在 `ftp://ftp.icp-vortex.com/download/linux/` 获取。支持以下控制器：GDT3000B、GDT3000A、GDT3010A、GDT3020A 和 GDT3050A。也可以使用 pre-patch-2.0.31-4 至 pre-patch-2.0.31-9。
- Iomega PPA3 并行端口 SCSI 主机总线适配器（内置于 ZIP 驱动器中）
- Initio Corp. INI-9090U/INI-9100-NU/INI-9100W/UW、INI-9200U/UW、INI-9400U/UW、INI-9520U/UW、INI-A100U2W
- Initio Corp. INIC-950
- Media Vision Pro Audio Spectrum 16 SCSI（ISA）
- Mylex（原 BusLogic）W 系列（PCI）（BT-948、BT-958、BT-958D）
- Mylex（原 BusLogic）C 系列（ISA/EISA/VLB/PCI）（BT-946C、BT-956C、BT-956D、BT-445、BT-747C、BT-757C、BT-757CD、BT-545C、BT-540CF）
- Mylex（原 BusLogic）S 系列（ISA/EISA/VLB）（BT-445S、BT-747S、BT-747D、BT-757S、BT-757SD、BT-545S、BT-542D、BT-742A、BT-542B）
- Mylex（原 BusLogic）A 系列（ISA/EISA）（BT-742A、BT-542B）
- NCR 5380 通用卡
- NCR 53C400（Trantor T130B）（使用通用的 NCR 5380 SCSI 支持）
- NCR 53C406a（Acculogic ISA 支持/Media Vision Premium 3D SCSI）
- NCR 芯片 53C7x0（53C710 仅支持 PCI 版本）
- NCR 芯片 53C810、53C815、53C820、53C825、53C860、53C875、53C895（53C895 “理论上”支持）
- QLogic/Control Concepts SCSI/IDE（FAS408）（ISA/VLB）
- QLogic FASXXX/FASXX 芯片系列（ISA/VLB）
- QLogic IQ-PCI、IQ-PCI-10、IQ-PCI-D（PCI）（ISP1020 芯片）
- Quantum ISA-200S、ISA-250MG
- Seagate ST-01/ST-02（ISA）
- SIIG Ultrawide SCSI Pro（Initio 芯片组）。驱动程序和内核补丁可在 `http://www.initio.com/suse.htm` 找到。
- SoundBlaster 16 SCSI-2（兼容 Adaptec 152x）（ISA）
- Tekram DC-390、DC-390W/U/F
- Trantor T128/T128F/T228（ISA）
- UltraStor 14F（ISA）、24F（EISA）、34F（VLB）
- Western Digital WD7000 SCSI

### Alpha、Beta 驱动程序

- AMD AM79C974（PCI）（Compaq、HP、Zeos 板载 SCSI）
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/scsi/AM79C974-0.3.tgz`
- Adaptec ACB-40xx SCSI-MFM/RLL 桥接板
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/scsi/adaptec-40xx.tar.gz`
- Always Technologies AL-500
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/scsi/al500-0.2.tar.gz`
- Iomega PC2/2B
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/scsi/iomega_pc2-1.1.x.tar.gz`
- Ricoh GSI-8
  `ftp://tsx-11.mit.edu/pub/Linux/ALPHA/scsi/gsi8.tar.gz`

### 不支持

- Adaptec AHA 2940UW Pro
- Adaptec AAA-13x RAID 适配器
- Adaptec AAA-113x RAID 端口卡
- Adaptec AIC-7810
- NCR 53C710 芯片（ISA）（过时的老芯片，但仍在某些 Compaq 型号中使用）
- 非 Adaptec 兼容的 DTC 板卡（327x、328x）

## 控制器（I/O）

任何标准的串行/并行/游戏杆/组合卡均可。Linux 支持 8250、16450、16550 和 16550A UART。支持非标准 IRQ（IRQ 9）的卡也可以使用。

参见 Neal Samuelson 的《Application Note AN-493》，作者 Martin S. Michael。第 5.0 节详细描述了 NS16550 与 NS16550A 之间的差异。简而言之，NS16550 的 FIFO 电路存在缺陷，而 NS16550A（及后续）芯片修复了这些问题。然而，National 很久以前生产的 NS16550 数量极少，因此现在应该非常罕见。而且，现代板卡上实际使用的许多“16550”器件来自众多生产多器件的制造商，可能并不使用 National 的“A”后缀。此外，一些多端口板卡会使用 16552 或 16554，或 National 及其他供应商的各种多端口或多功能芯片（通常为焊接在板上的密集封装，而非 40 引脚 DIP）。除非你遇到一颗非常古老的、散装或装在旧板上的 National“NS16550”（无 A）40 引脚 DIP 芯片，否则不必担心；若真遇到，应将其视为 16450（无 FIFO），而非 16550A——Zdhahai Stewart（zstewart@hisys.com）。

## 控制器（多端口）

### 非智能卡

**支持的型号**

- AST FourPort 及仿制卡（4 端口）
- Accent Async-4（4 端口）
- Arnet Multiport-8（8 端口）
- Bell Technologies HUB6（6 端口）
- Boca BB-1001、1008（4、8 端口）- 无 DTR、DSR 和 CD
- Boca BB-2016（16 端口）
- Boca IO/AT66（6 端口）
- Boca IO 2by4（4 串口/2 并口，使用 5 个 IRQ）
- Computone ValuePort（4、6、8 端口）（与 AST FourPort 兼容）
- DigiBoard PC/X、PC/Xem、PCI/Xem、EISA/Xem、PCI/Xr（4、8、16 端口）
- Control Hostess 550（4、8 端口）
- PC-COMM 4 端口（4 端口）
- SIIG I/O Expander 4S（4 端口，使用 4 个 IRQ）
- STB 4-COM（4 端口）
- Twincom ACI/550
- Usenet Serial Board II（4 端口）

非智能卡通常有两种类型：一种使用标准 COM 端口地址和 4 个 IRQ；另一种与 AST FourPort 兼容，使用可选的地址块和单个 IRQ。（地址和 IRQ 通过 setserial 设置。）如果你要购买这类卡，务必确认它符合哪种标准；价格并不能说明问题。

### 智能卡

**支持的型号**

- Computone IntelliPort II（4/8/16 端口）
  `ftp://ftp.computone.com/pub/bbs/beta/ip2linux-1.0.2.tar.gz`
- Cyclades Cyclom-Y（基于 RISC，8-32 端口）（ISA/PCI）
  `http://www.cyclades.com/`
- Cyclades-Z（高端，16-64 端口）（PCI）
  `http://www.cyclades.com/`
- DigiBoard PC/Xe（ISA）、PC/Xi（EISA）和 PC/Xeve
  `ftp://ftp.digibd.com/drivers/linux/`
- Equinox SST 智能串行 I/O 卡
  `http://www.equinox.com`
- Hayes ESP 1、2 和 8 端口版本
  自 2.1.15 起包含在内核中。适用于 2.0.x 内核版本的驱动程序可在以下位置找到：
  `http://www.nyx.net/~arobins...`
- Stallion EasyIO（ISA）/EasyConnection 8/32（ISA/MCA）/EasyConnection 8/64（PCI）
  有关 DIP 开关设置和配置文件，请查看 `http://www.stallion.com`。
- Stallion EasyConnection 8/64（ISA/EISA）/OnBoard（ISA/EISA）/Brumby（ISA）
  最新驱动程序可在 `ftp://ftp.stallion.com/drivers/ata5/Linux/v544.tar.gz` 找到。

### Alpha、Beta 驱动程序

- Control RocketPort（8/16/32 端口）
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/serial/control-1.04.tar.gz`（适用于 1.2.x 内核）。适用于 2.x 内核的驱动程序可在以下位置找到：
  `http://ftp.leidenuniv.nl/linux/tsx-11/packages/control/.`
- DigiBoard COM/Xi
- Moxa C102、C104、C168、C218（8 端口）、C320（8/16/24/32 可扩展）和 C320T
  `ftp://ftp.moxa.com.tw/drivers/linux/`
- RISCcom/8
- Specialix SIO/XIO（模块化，4 到 32 端口）
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/serial/sidrv.taz`
- Specialix IO8+
  - 联系 `devices@BitWizard.nl`。

## 网络适配器

以太网适配器的性能差异很大。一般来说，设计越新越好。有些非常老的卡，如 3Com 3c501，之所以还有用，只因为能在废品堆里以每个 5 美元的价格找到。对兼容卡要小心——并非所有兼容卡都是好的，劣质兼容卡在 Linux 下常常导致莫名其妙的死机。请阅读 Ethernet HOWTO（`http://metalab.unc.edu/LDP/HOWTO`），了解各种网卡的详细说明。

### 支持的以太网

对于采用 DECchip DC21x4x 系列的以太网卡，可使用“Tulip”驱动程序。有关此驱动程序的更多信息，请访问 `http://cesdis.gsfc.nasa.gov/linux/drivers/tulip.html`。

- 3Com 3c501——尽量避而远之（3c501 驱动）
- 3Com 3c503（3c503 驱动）、3c505（3c505 驱动）、3c507（3c507 驱动）、3c509/3c509B（ISA）/3c579（EISA）
- 3Com Etherlink III Vortex 以太网卡（3c590、3c592、3c595、3c597）（PCI）、3Com Etherlink XL Boomerang（3c900、3c905）（PCI）和 Cyclone（3c905B、3c980）以太网卡（3c59x 驱动）以及 3Com Fast EtherLink 以太网卡（3c515）（ISA）（3c515 驱动）
  - 这些驱动程序的更新版本可在 `http://cesdis.gsfc.nasa.gov/linux/drivers/vortex.html` 获取。
  - 尽量避开 3c900 卡，因为驱动程序对该卡支持不佳。
- 3Com 3cFE575 Cyclone Cardbus（3c59x 驱动）
- 3Com 3c575 系列 Cardbus（3c59x 驱动）（全部 PCMCIA ??）
- AMD LANCE（79C960）/ PCnet-ISA/PCI（AT1500、HP J2405A、NE1500/NE2100）
- AT&T GIS WaveLAN
- Allied Telesis AT1700
- Allied Telesis LA100PCI-T
- Allied Telesyn AT2400T/BT（“ne”模块）
- Ansel Communications AC3200（EISA）
- Apricot Xen-II / 82596
- Cabletron E21xx
- Cogent EM110
- Crystal Lan CS8920、Cs8900
  - `http://www.cirrus.com/private/drivers/ethernet/edrivers.html`
- Danpex EN-9400
- DEC DE425（EISA）/DE434/DE435（PCI）/DE450/DE500（DE4x5 驱动）
- DEC DE450/DE500-XA（dc21x4x）（Tulip 驱动）
- DEC DEPCA 和 EtherWORKS
- DEC EtherWORKS 3（DE203、DE204、DE205）
- DEC QSilver（Tulip 驱动）
- Digi International RightSwitch
- DLink DE-220P、DE-528CT、DE-530+、DFE-500TX、DFE-530TX
  - 更多信息请参见 `http://www.dlink.ca/linux.html`。
- Fujitsu FMV-181/182/183/184
- HP PCLAN（27245 和 27xxx 系列）
- HP PCLAN PLUS（27247B 和 27252A）
- HP 10/100VG PCLAN（J2757、J2573、27248B、J2585）（**ISA/EISA/PCI**）
  - 更多信息请参见 `http://cesdis1.gsfc.nasa.gov:80/linux/drivers/100vg.html`。
- ICL EtherTeam 16i/32（**EISA**）
- Intel EtherExpress
- Intel EtherExpress Pro
- KTI ET16/P-D2、ET16/P-DC ISA（无需跳线，且支持硬件配置选项）
- Macromate MN-220P（PnP 或 NE2000 模式）
- NCR WaveLAN
- NE2000/NE1000（注意仿冒品）
- Netgear FA-310TX（Tulip 芯片）
- New Media Ethernet
- PureData PDUC8028、PDI8023
- SEEQ 8005
- SMC Ultra/EtherEZ（ISA）
- SMC 9000 系列
- SMC PCI EtherPower 10/100（Tulip 驱动）
- SMC EtherPower II（epic100.c 驱动）
- Sun LANCE 适配器（内核 2.2 及更高版本）
- Sun Intel 适配器（内核 2.2 及更高版本）
- Schneider & Koch G16
- Western Digital WD80x3
- Zenith Z-Note/IBM ThinkPad 300 内置适配器
- Znyx 312 etherarray（Tulip 驱动）

### ISDN

- Linux ISDN WWW 页面
    - 这个页面似乎已经不存在了。
- ISDN4Linux 工具可从 `ftp://ftp.franken.de/pub/isdn4linux/v2.0` 获取。

### ISDN

- 3Com Sonix Arpeggio
  - `ftp://metalab.unc.edu/pub/Linux/kernel/patches/network/sonix.tgz`
- ASUSCOM Network Inc. ISDNlink 128K PC 适配器 (HiSax)
- AVM A1 (HiSax)
- AVM B1 (avmb1)
- Combinet EVERYWARE 1000 ISDN
  - `ftp://metalab.unc.edu/pub/Linux/kernel/patches/network/combinet1000isdn-1.02.tar.gz`
- Compaq ISDN S0 (ISA) (HiSax)
- Creatix PnP S0 (HiSax)
- Dr. Neuhaus Niccy PnP/PCI (HiSax)
- Dynalink IS64PH (HiSax)
- Eicon Diehl Diva 2.0 (ISA/PCI) (S0 和 U 接口，无 PRO 版本) (HiSax)
- Eicon Diehl Diva Piccolo (HiSax)
- Elsa Microlink PCC-16、PCF、PCF-Pro、PCC-8 (HiSax)
- ELSA QuickStep 1000/1000PCI/3000 (HiSax)
- 基于 HFC-2BS0 的卡 (HiSax)
- IBM Active 2000 (ISA) (act2000)
- ICN ISDN 卡 (icn)
- Ith Kommunikationstechnik GmbH MC 16 (ISA) (HiSax)
- ITK ix1-micro Rev.2 (HiSax)
- Octal PCBIT (pcbit)
- Sedlbauer Speed Card (HiSax)
- Teles S0-8/S0-16.0/S0-16.3/S0-16.3c/S0-16.4 及兼容型号 (HiSax)
- Traverse Technologie NETjet PCI S0 (HiSax)
- USR Sportster 内置 TA (HiSax)

模拟标准调制解调器或常见以太网适配器的 ISDN 卡无需任何特殊驱动程序即可工作。

### 帧中继

- Emerging Technologies Inc 同步适配器 (`http://www.etinc.com`)
- ET/5025 (1 端口，8 位 ISA)
- ET/5025-16 (2 端口，16 位 ISA)
- ET/5025-25 (2 端口，16 位 ISA)
- ET/5025pq (4 端口，PCI)

## 无线网络

- ZCOM WL2420 ISA
  - 产品信息可在 `http://www.zcom.com.tw` 找到。内核目标文件驱动程序可在 `www.boerde.de/~matthias/airnet/zcom_v12` 获取。

## X.25

- Emerging Technologies Inc 同步适配器 (`http://www.etinc.com`)
- ET/5025 (1 端口，8 位 ISA)
- ET/5025-16 (2 端口，16 位 ISA)
- ET/5025-25 (2 端口，16 位 ISA)
- ET/5025pq (4 端口，PCI)

## 袖珍型和便携式适配器

有关 Linux 以及并行端口使用的更多信息，请访问 Linux 并行端口主页 `http://www.torque.net/linux-pp.html` 或 `http://www.torque.net/parport/`。请查阅“受支持的并行端口设备”，以获取受支持的并行端口设备（不包括打印机）的完整列表。

## 无插槽

- SLIP/CSLIP/PPP（串行端口）
- EQL（串行 IP 负载均衡）
- PLIP（并行端口）—使用 LapLink 电缆或双向电缆

## ARCNET

适用于所有 ARCnet 卡。

## 令牌环

- `http://www.linuxtr.net`
- 3Com 3C619/B/C Tokenlink 16/4 (ibmtr)
- 3Com 3C319 Velocity ISA (ibmtr)
- IBM PCI 令牌环适配器
- IBM Wake on LAN TR 适配器
- IBM 16/4 TR PCI Adapter 2、Adapter 2 Wake on LAN、Adapter 2 Wake on LAN Special
- IBM High Speed 100/16/4 令牌环
- IBM ISA 16/4、MCA 16/4 (ibmtr)
- IBM Tropic 芯片组卡
- Olicom RapidFire 3139、3140、3141、3540
  - `http://www.olicom.com`
- Olicom OC-3136、OC-3137、OC-3138、OC-3129
  - `http://www.olicom.com`
- Madge Smart 100/16/4 PCI、16/4 PCI Mk3、16/4 PCI Mk2
  - `http://www.madge.com`
- Madge Presto PCI、16/4 CardBus
  - `http://www.madge.com`
- SysKonnect TR4/16(+) SK-4190 ISA、SK-4590 PCI、SK-4591 PCI (sktr)

## FDDI

- DEC DEFEA (EISA)/DEFPA (PCI) (内核 2.0.24 及更高版本)

## 业余无线电 (AX.25)

- Gracilis PacketTwin
- Ottawa PI/PI2
- 大多数基于 8530 的通用 HDLC 板卡

## PCMCIA 卡

- 请参阅“受支持的 PCMCIA 卡”获取完整列表，或访问 David Hinds 的网页 `http://hyper.stanford.edu/HyperNews/get/pcmcia/home.html`。

### Alpha、Beta 驱动程序

### 以太网

- Racal-Interlan NI5210（i82586 以太网芯片）。在内核 2.2 及更高版本中获得改进支持。
- Racal-Interlan NI6510（am7990 Lance 芯片）。从内核 1.3.66 开始支持超过 16MB 的 RAM。
- Racal-Interlan PCI 卡（AMD PCnet 芯片 Am79C970）

### ISDN

- SpellCaster 的 Datacomute/BRI、Telecomute/BRI (ISA) (sc)

### ATM

- Efficient Networks ENI155P-MF 155Mbps ATM 适配器 (PCI)
  - `http://lrcwww.epfl.ch/linux-atm/`

### 帧中继

- Sangoma S502 56K 帧中继卡
  - `ftp://ftp.sovereign.org/pub/wan/fr/`

### 无线

- Proxim RangeLAN2 7100 (ISA)/630x (OEM mini-ISA)
  - `http://www.komacke.com/distribution.htm`

## 不支持的设备

- 3Com 3C359 Velocity XL PCI
- 3Com 3C339 Velocity PCI
- IBM PCI LANStreamer、MCA LANStreamer 令牌环
- Intel TokenExpress PRO、TokenExpress 16/4
- SysKonnect/Schneider & Koch 令牌环卡（全部）

## 声卡

有关声音驱动程序和声卡的更多信息，请访问 `http://www.opensound.com/ossfree` 或 `http://www.opensound.com/oss.html`。

### 支持的设备

- 4Front Technology Virtual Mixer（包含 SoftOSS）
- 4Front Technology Virtual Synth (SoftOSS)
- 6850 UART MIDI
- A-Plus Sound of Music (OPL3-SA)
- A-Trend Harmony 3D S751 (PCI)
- AcerMagic S23
- AdLib FM 合成器卡
- AdLib MSC 16 PnP (CS4235)
- AMD Interwave 参考卡
- ARC Probook
- Audio Excel DSP16
- 基于 Avance Logic ALS-007 芯片的卡。
  - 此芯片的代码已集成在 Sound Blaster 16 驱动程序中。应使用 Isapnptools 进行配置。
- AW32 Pro (R2.2-W2)
- AW35 (CS4237)
- AW37 Pro (CS4235)
- Aztech Sound Galaxy NX Pro、NX Pro 16、WaveRider 32+
- Aztech Washington
- BTC Mozart Sound System
- BTC-1831 声卡 (Opti 1688)
- Bravo 声卡 (Opti 82C930)
- Bull PowerPC 内置音频
- CRD4235-6/-8
- CS32-3DI
- Compaq Deskpro XL 集成 Business Audio
- Creative EMU8000 附加卡 (PnP)
- Creative Phone Blaster 28.8/33.6
- Creative Sound Blaster 1.0 至 2.0
- Creative Sound Blaster Pro
- Creative Sound Blaster 16
- Creative Sound Blaster 16 ASP
- Creative Sound Blaster 16 PnP (type-1 至 type-10)
- Creative Sound Blaster 16 Vibra
- Creative Sound Blaster 2.x
- Creative Sound Blaster 32/AWE
- Creative Sound Blaster 32/AWE PnP (type-1 至 type-10)
- Creative Sound Blaster AWE64 (type-1 至 type-7)
- Creative Sound Blaster AWE64 Gold (type-1 和 type-2)
- Creative Sound Blaster PCI64/128
- Creative Sound Blaster AWE64/Gold 和 16/32/AWE PnP 卡需要使用 autoprobe 激活。
- Creative ViBRA16C/CL/S (type-1 和 type-2) PnP
- Creative ViBRA16X PnP（仅半双工）
- Crystal Lake Crystal Clear Series 100
- Crystal Audio (CS4235)
- Crystal CRD4236B-1E
- Crystal CRD4237B-5/-8
- Crystal CSC0B35 (CS4236B)
- Crystal CX4237B-SIDE
- Crystal 板载 PnP 音频 (CS4235)
- Dell Latitude 内置音频
- Diamond Crystal MM PC/104
- Digital AXP 内置音频
- ECHO-PSS 卡 (Orchid SoundWave32、Cardinal DSP16)
- ESS 1868、1869 (type-1 和 type-2)、1878、1879、1968 PnP AudioDrive
- Ensoniq AudioPCI (ES1371)
- Ensoniq AudioPCI/SoundBlaster PCI (ES1370)
- Ensoniq Soundscape Elite
- Ensoniq Soundscape PnP (型号 1 和 2)
- Ensoniq Soundscape S-2000
- Ensoniq Soundscape VIVO、VIVO90
- Ensoniq ActionNote 880 C/CX
- Gallant 声卡（基于 SC-6000 和 SC-66000）
- 基于 AD1815 的通用声卡 (PnP)
- 基于 CMI8330 的通用声卡 (PnP)
- 基于 Crystal CS4232 的通用声卡或主板（非 PnP）
- Acer 的通用 Crystal CS4232（PnP 模式）
- 通用 Crystal CS4232 type-1 至 type-3（PnP 模式）
- 通用 Crystal CS4235 type-1
- 通用 Crystal CS4236（type-1 至 type-3）
- 基于 Crystal CS4236 的通用声卡或主板（非 PnP）
- 通用 Crystal CS4236A（type-1 和 type-2）、CS4236B
- 基于 Crystal CS4237 的通用声卡或主板（非 PnP）
- 通用 Crystal CS4237B（type-1 和 type-2）
- 基于 Crystal CS4238 的通用声卡或主板（非 PnP）
- 基于 ESS ES688、ES1688、ES1788、ES1868、ES1869、ES1887、ES1888 的通用声卡或主板
- 基于 Jazz16 的通用声卡
- 通用 MAD16 (OPTi 82C928)、MAD16 Pro、MAD16 Pro（双工）(OPTi 82C929)
- 通用 Mozart 声卡（OAK OTI-601 芯片）
- 基于 OPTi 82C924、82C925 的通用声卡 (PnP)
- 通用 OPTi 82C924 声卡（非 PnP 模式）。使用 MSS 驱动程序和 isapnp 工具。
- 通用 OPTi 82C930
- 通用 OPTi 82C931
  - 参见 `http://spoke.nols.com/~drees/opti931.html`。
- 基于通用 Soundscape 的声卡
- 兼容通用 Windows 声音系统
- 基于通用 Yamaha OPL3-SA1 (YMF701) 的声卡
- 基于通用 Yamaha OPL3-SA2 (YMF711) 的声卡（类型 1、类型 3、类型 4）
- 基于通用 Yamaha OPL3-SA3 (YMF715) 的声卡
- 通用 Yamaha OPL3-SAx (YMF715/YMF719) 非 PnP 声卡
- Gravis Ultrasound
- Gravis Ultrasound Extreme
- Gravis Ultrasound 16 位采样子卡
- Gravis Ultrasound MAX
- Gravis Ultrasound ACE
- Gravis Ultrasound PnP（带 RAM）、PnP Pro
- HP OmniBook 2100 (CS4236)
- Home Studio 64（仅模拟音频）
- IBM Audio Feature (CS423x)
- Logitech SoundMan Games（SBPro，支持 44kHz 立体声）
- Logitech SoundMan Wave (Jazz16/OPL4)
- Logitech SoundMan 16（兼容 PAS-16）
- MED3201 声卡
- Maxi Sound 32 PnP（仅模拟音频）
- Maxi Sound 64 Dynamic 3D（仅模拟音频）
- Media Sound SW/32（非 PnP 模式）
- Media TriX AudioTriX Pro、3D XG
- Media Vision Premium 3D (Jazz16)
- Media Vision Pro Sonic 16 (Jazz)
- Media Vision Pro Audio Spectrum 16 (PAS-16)
- Media Vision Pro Audio Studio 16
- Media Vision Thunderboard
- Microsoft Windows Sound System 板 (AD1848)
- MiroSound PCM1-pro
- MultiWave AudioWave Green 16
- Music Quest MIDI 连接卡 (MCC)
- Music Quest MQX-16、MQX-16S MIDI 适配器
- Music Quest MQX-32、MQX-32M MIDI 适配器
- Music Quest PC MIDI 卡
- NEC Harmony
- Orchid SoundDrive 16EZ
- Pine PT201
- Primax SoundStorm FM 16、SoundStorm Wave
- Pro Audio Spectrum 16、Studio 16
- RME Digi32、Digi32 Pro、Digi32/8
- Reveal SC300
- Reveal WaveXtreme Pro（带 RAM）
- Roland MPU IPC-T MIDI 适配器
- S3 SonicVibes
- Shark Mako
- Sharp PC8800
- Shuttle Sound System 48
- Spacewalker HOT-255 PCI 3D (PCI)
- TerraTec Maestro 32/96
- Terratec EWS64XL（仅音频）
- Terratec Sound System Base 1 (AD1816)
- Terratec Sound System Base 64 (AD1816)
- Tomato Sound System (OPTi 82C930)
- Trust Sound Expert De Luxe Wave 32
- Turtle Beach Classic/Tahiti/Monterey
- Turtle Beach Maui
- Turtle Beach Monte Carlo 928、Monte Carlo 929
- Turtle Beach Pinnacle/Fiji
- Turtle Beach Tropez、Tropez Plus（仅音频）
- Turtle Beach Daytona（仅音频）
- Wearnes Classic 16
- Yamaha Sound Edge SW20-PC
- Zefiro Acoustics ZA2（不推荐）
- Zenith Z-Player
- AWE32/64 支持从 2.1.x 内核系列开始提供（安装详情请参阅 Marcus Brinkmann 编写的 SoundBlaster AWE mini-HOWTO）。
- MPU-401 MIDI 智能模式（不要盲目启用）
- MPU IPC-T
- MQX-32M
- MPU-401 MIDI UART 仅限哑端口（不要盲目启用）
- Yamaha FM 合成器（OPL2、OPL3、OPL3-SA(x)（自 2.1.x 内核系列起）和 OPL4）
- OSS 支持所有 MIDI 子卡，包括 Wave Blaster、TB Rio 和 Yamaha DB50XG。唯一的要求是“宿主”卡受 OSS 支持。请注意，只有“宿主”卡需要使用 soundconf 配置。子卡将通过“宿主”卡的 MIDI 自动访问。

### 1.3.2 Alpha、Beta 驱动程序

- 4Front Tech. Waveloop 音频设备
- Acer FX-3D（基于 AD1816）
- AVM Apex Pro 卡（基于 AD1816）
- Aztech AZT1008、AZT12320、AZT3000
- Aztech SC-16 3D（基于 AD1816）
- Creative Sound Blaster Vibra16x
- Creative Sound Blaster Live! 和 Live! Value Edition
- Creative Labs 为这款卡提供了测试版驱动程序。它们适用于内核 2.0.36 和 2.2.5（很可能也适用于这些系列中更新的内核）。驱动程序可以在 `http://www.creativelabs.com` 的软件下载区域获取。
- Highscreen Sound-Booster 32 Wave 3D（基于 AD1816）
- Highscreen Sound-Booster 16（基于 AD1816）
- HP Kayak（基于 AD1816）
- IBM MWave
- Newcom SC-16 3D（基于 AD1816）
- PC 扬声器/并行端口 DAC
  `ftp://ftp.informatik.hu-berlin.de/pub/os/linux/hu-sound/`
- Rockwell WaveArtist 芯片组
- Sonorus STUDI/O
- SY-1816（基于 AD1816）
- Terratec Base 1、Base 64（基于 AD1816）
- Terratec EWSS64S（基于 AD1816）
- Turtle Beach Malibu `ftp://ftp.cs.colorado.edu/users/mccreary/archive/tbeach/multisound/`

基于 AD1816 音效芯片的声卡需要 isapnptools 进行配置。

### 不支持

- A-Trend Harmony 3DS724 (PCI)
- Atech PCI 388-A3D
- Adaptec AME-1570
- Aureal Vortex (PCI)
- Cardinal DSP 16
- 贡献的低级驱动程序
- Crystal CS4614 (PCI)
- Cyrix MediaGX 内置音频
- Diamond Monster Sound MX300
- Diamond Sonic Impact
- Dream 94PnP Home Studio
- EON Bach SP901 (A3D)
- ESS (PCI)
- ESS Maestro-1 (PCI)、Maestro-2 (PCI)
- ESS Solo-1 (PCI)
- Echo Personal Sound System
- 基于通用 ALS007、ALS100 的声卡
- Orchid NuSound 3D
- Orchid SoundWave 32
- Paradise DSP-16
- Quicknet Internet LineJACK
- Terratec XLerate (A3D)
- Turtle Beach Montego
- Turtle Beach TBS-2000
- Videologic SonicStorm
- Wearnes Beethoven ADSP-16
- Western Digital Paradise DSP-16
- Yamaha YMF724 (PCI)

Sound Blaster 16 系列上的 ASP 芯片不受支持。AWE32 板载的 E-mu MIDI 合成器也不受支持。

Nathan Laredo（laredo@gnu.ai.mit.edu）愿意编写 AWE32 驱动程序，但前提是你送他一块免费的卡。如果你寄送免费的硬件样品，他也几乎愿意为任何硬件编写驱动程序。

带有 DSP 4.11 和 4.12 的 Sound Blaster 16 存在一个硬件缺陷，当同时播放 MIDI 和数字音频时，会导致音符悬挂/卡住。这个问题可能发生在 Wave Blaster 子卡或连接到 MIDI 端口的 MIDI 设备上。目前尚无已知的修复方法。

## 硬盘驱动器

如果控制器受支持，所有硬盘驱动器都应该能工作。

（摘自 SCSI HOWTO）所有块大小为 256、512 或 1024 字节的直接访问 SCSI 设备都应该能工作。其他块大小将无法工作（请注意，通常可以使用 MODE SELECT SCSI 命令更改块或扇区大小来解决此问题）。

大容量 IDE（EIDE）驱动器与较新的内核配合良好。由于 PC BIOS 的限制，启动分区必须位于前 1024 个柱面内。

某些 Conner CFP1060S 驱动器可能与 Linux 和 ext2fs 存在兼容性问题。症状包括 e2fsck 期间出现 inode 错误以及文件系统损坏。Conner 已发布固件升级来解决此问题。请致电 Conner，电话号码：1-800-4CONNER（美国）或 +44-1294-315333（欧洲）。致电时请准备好微代码版本（位于驱动器标签上，9WA1.6x）。

据报道，许多 Maxtor 和 Western Digital IDE 驱动器无法与另一制造商的驱动器在同一条 IDE 电缆上愉快地共存。通常其中一个驱动器会在运行期间发生故障。解决方案是将它们放在不同的 IDE 电缆上。

某些 Micropolis 驱动器与 Adaptec 和 BusLogic 卡存在兼容性问题。如果怀疑有问题，请联系驱动器制造商获取固件升级。

- 多设备驱动程序（RAID-0、RAID-1）
  `ftp://sweet-smoke.ufr-info-p7.ibp.fr/public/Linux/`

### 不支持

以下硬盘被提及不受 Linux 支持。请阅读可用的错误报告。

- NEC D3817、D3825、D3827、D3847
  - 这些驱动器在 Mode Sense Page 3 报告的值中略微不符合 SCSI-2 规范。在 Mode Sense Page 3 中，所有 NEC D38x7 驱动器报告的扇区大小均为零。NEC 驱动器是我们遇到的第一种将扇区大小报告为零的驱动器品牌。不幸的是，Mode Sense Page 3 中的该字段不可修改，并且无法更新 D38x7 驱动器的固件来解决此问题。问题在 D3825 和 D3827（均为修订版 0407）上被提及。这两个硬盘的修订版 0410 似乎解决了此问题。

## 磁带驱动器

### 支持

- SCSI 磁带驱动器
  - （摘自 SCSI HOWTO）支持使用小于驱动程序缓冲区长度（在发行版源码中设置为 32k）的固定和可变长度块的驱动器。几乎所有驱动器都应该能工作。（如果您知道任何不兼容的驱动器，请发送邮件告知。）
- Seagate Sidewinder 50 AIT（在 ICP 6527 RAID 控制器上）
- QIC-02 驱动器
- Iomega Ditto 内置（ftape 3.04c 及更新版本）

### Alpha、Beta 驱动程序

- QIC-117、QIC-40/80、QIC-3010/3020 (QIC-WIDE) 驱动器
  - 大多数使用软盘控制器的磁带驱动器应该能工作。各种专用控制器（Colorado FC-10/FC-20、Mountain Mach-2、Iomega Tape Controller II）也受支持。
  - `ftp://metalab.unc.edu/pub/Linux/kernel/tapes`
- ATAPI 磁带驱动器
  - 对于这些驱动器，内核中提供了 alpha 驱动程序（ide-tapec）。支持的 ATAPI 磁带驱动器有：
  - Seagate TapeStor 8000
  - Conner CTMA 4000 IDE ATAPI Streaming 磁带驱动器

### 不支持

- Emerald 和 Tecmar QIC-02 磁带控制器卡——Chris Urlich
  - `insom@math.ucr.edu`
- 连接到并行端口的驱动器（例如：Colorado Tracker）
- 某些高速磁带控制器（Colorado TC-15）
- Irwin AX250L/Accutrak 250（不是 QIC-80）
- IBM 内置磁带备份单元（不是 QIC-80）
- COREtape Light

### CD-ROM 驱动器

有关 CD-ROM 驱动器的更多信息，请查看 `http://metalab.unc.edu/LDP/HOWTO/` 上的 CDROM-HOWTO。

## 受支持的硬件

### 常见 CD-ROM 驱动器

- SCSI CD-ROM 驱动器
  - (摘自 CD-ROM HOWTO) 任何块大小为 512 或 2048 字节的 SCSI CD-ROM 驱动器都应在 Linux 下正常工作；这涵盖了市面上绝大多数 CD-ROM 驱动器。
- EIDE (ATAPI) CD-ROM 驱动器 (IDECD)
  - 几乎所有双倍速、四倍速和六倍速驱动器均受支持，包括：
    - Mitsumi FX400
    - NEC-260
    - Sony 55E

### 专有 CD-ROM 驱动器

- Aztech DAZ68-01A, Orchid CDS-3110, Okano/Wearnes CDD-110, Conrad TXC, CyCDROM CR520ie/CR540ie/CR940ie (AZTCD)
- Creative Labs CD-200 (SBPCD)
- Funai E2550UA/MK4015 (SBPCD)
- GoldStar R420 (GSCD)
- IBM 外部 ISA (SBPCD)
- Kotobuki (SBPCD)
- Lasermate CR328A (OPTCD)
- LMS Philips CM 206 (CM206)
- Longshine LCS-7260 (SBPCD)
- Matsushita/Panasonic CR-521/522/523/562/563 (SBPCD)
- MicroSolutions Backpack 并口驱动器 (BPCD)
- Mitsumi CR DC LU005S (MCD/MCDX)
- Mitsumi FX001D/F (MCD/MCDX)
- Optics Storage Dolphin 8000AT (OPTCD)
- Sanyo CDR-H94A (SJCD)
- Sony CDU31A/CDU33A (CDU31A)
- Sony CDU-510/CDU-515 (SONYCD535)
- Sony CDU-535/CDU-531 (SONYCD535)
- Teac CD-55A SuperQuad (SBPCD)

### Alpha、Beta 驱动

- LMS/Philips CM 205/225/202
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/cdrom/lmscd0.4.tar.gz`
- NEC CDR-35D (旧版)
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/cdrom/linux-neccdr35d.patch`
- Sony SCSI 多会话 CD-XA
  `ftp://tsx-11.mit.edu/pub/linux/patches/sony-multi-0.00.tar.gz`
- 并口驱动
  `http://www.torque.net/linux-pp.html`

### 注意事项

所有 CD-ROM 驱动器在读取数据方面的表现应基本相同。音频 CD 播放工具存在各种兼容性问题 (尤其是较新的低端 NEC 驱动器)。一些 Alpha 驱动可能尚不支持音频。

早期 (单倍速) NEC CD-ROM 驱动器可能无法与当前可用的 SCSI 控制器正常配合。

支持 PhotoCD (XA)。Hadmut Danisch 编写的 `hpcdtoppm` 程序可将 PhotoCD 文件转换为可移植位图格式。该程序可从 `ftp://ftp.gwdg.de/pub/linux/hpcdtoppm` 获取，或作为 PBM 工具集的一部分获得。

此外，从 2.1.3x 及更高版本的内核系列开始支持读取视频 CD。内核 2.0.30 有一个补丁可用。

最后，大多数 IDE CD-ROM 换盘器均受支持。

### CD 刻录机

Linux 现在支持许多 CD 刻录机。要获取受支持的 CD 刻录机的最新列表，请查看位于 `http://metalab.unc.edu/LDP/HOWTO/CD-Writing-HOWTO.html` 的 CD-Writing mini-HOWTO，或查看 `http://www.shop.de/cgi-bin/winni/lsc.pl`，或查看 `http://www.gwdg.de:8080/cgi-bin/winni/lsc.pl`。`ftp://metalab.unc.edu/pub/Linux/utils/disk-management/` 中的程序以及 `cdrecord` (`http://www.fokus.gmd.de/research/cc/glone/employees/joerg.schilling/private/cdrecord.html`) 可用于刻录 CD。Linux 的 X-CD-Roast 软件包是使用 CD 刻录机的图形前端。该软件包可在 `ftp://metalab.unc.edu/pub/Linux/utils/disk-management/xcdroast-0.96d.tar.gz` 找到。

- Grundig CDR 100 IPW
- HP CD-Writer+ 7100
- HP SureStore 4020i
- HP SureStore 6020es/i
- JVC XR-W2010
- Kodak PCD 225
- Mitsubishi CDRW-226
- Mitsumi CR-2600TE
- Olympus CDS 620E
- Philips CDD-5210/522, 2000, 2600, 3610
- Pinnacle Micro RCD-5020/5040
- Plextor CDR PX-24CS
- Ricoh MP 1420C
- Ricoh MP 6200S/6201S
- Sanyo CRD-R24S
- Smart and Friendly Internal 2006 Plus 2.05
- Sony CDU 920S/924/926S
- Taiyo Yuden EW-50
- TEAC CD-R50S
- WPI (Wearnes) CDR-632P
- WPI (Wearnes) CDRW-622
- Yamaha CDR-100
- Yamaha CDR-200/200t/200tx
- Yamaha CDR-400t/400tx

### 可移动驱动器

只要控制器受支持，所有 SCSI 驱动器都应能正常工作，包括磁光 (MO)、WORM、软光盘 (floptical)、Bernoulli、Zip、Jaz、SyQuest、PD 等。

Panasonic MO 将 CD-ROM 驱动器与可移动光盘结合在一起。在配置内核时，你必须设置一个开关，才能使这两部分同时工作。

- 并口 Zip 驱动器
  `ftp://gear.torque.net/pub/`
- 并口 Avatar Shark-250
  `http://www.torque.net/parport/`

可移动驱动器的工作方式与硬盘和软盘类似，只需使用 fdisk/mkfs 分区并挂载磁盘即可。如果你的驱动器支持，Linux 还提供驱动器锁定功能。如果磁盘为 MS-DOS 格式，也可以使用 mtools。

CD-R 驱动器需要特殊软件才能工作。请阅读 CD-R Mini-HOWTO。

Linux 支持 512 字节/扇区和 1024 字节/扇区的磁盘。从内核 2.1.32 开始，Linux 还支持 2048 字节/扇区。内核 2.0.30 的补丁可从 `http://liniere.gen.u-tokyo.ac.jp/2048.html` 获取。

以下设备需要 2048 字节/扇区的支持：

- Fujitsu 磁光磁盘驱动器 M2513

从 pre-patch-2.0.31-3 开始，IDE/ATAPI 内置 Zip 驱动器、软光盘 (floptical) 和 PD 均受支持。

- LS-120 软光盘 (floptical)
- PD-CD

## 鼠标设备

### 受支持

- Microsoft 串口鼠标
- Mouse Systems 串口鼠标
- Logitech Mouseman 串口鼠标
- Logitech 串口鼠标
- ATI XL Inport 总线鼠标
- C&T 82C710 (QuickPort) (Toshiba、TI Travelmate)
- Microsoft 总线鼠标
- Logitech 总线鼠标
- PS/2 (辅助设备) 鼠标

### Alpha、Beta 驱动

- Sejin J-mouse
```
