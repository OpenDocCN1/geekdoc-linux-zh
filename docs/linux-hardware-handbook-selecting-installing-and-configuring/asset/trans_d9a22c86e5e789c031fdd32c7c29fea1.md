

## 2 主板

### 表 2.2 Intel 芯片组及其特性

| 名称 | 最大总线速度 | 支持的 CPU | SMP 支持 | 内存类型 | 内存错误处理 | 最大内存 | 最大可缓存内存 | AGP 支持 | IDE 支持 | USB 支持 |
|---|---|---|---|---|---|---|---|---|---|---|
| 430 LX (Mercury) | 66MHz | P60/66 | 否 | FPM | 奇偶校验 | 192MB | 192MB | 否 | 无 | 无 |
| 430 NX (Neptune) | 66MHz | P75+ | 是 | FPM | 奇偶校验 | 512MB | 512MB | 否 | 无 | 无 |
| 430 FX (Triton) | 66MHz | P75+ | 否 | FPM, EDO | 无 | 128MB | 64MB | 否 | 总线主控 | 无 |
| 430 MX (Mobile Triton) | 66MHz | P75+ | 否 | FPM, EDO | 无 | 128MB | 64MB | 否 | 总线主控 | 无 |
| 430 HX (Triton II) | 66MHz | P75+ | 是 | FPM, EDO | 奇偶校验, ECC | 512MB | 512MB | 否 | 总线主控 | 是 |
| 430 VX (Triton II) | 66MHz | P75+ | 否 | FPM, EDO | 无 | 128MB | 64MB | 否 | 总线主控 | 是 |
| 430 TX | 66MHz | P75+ | 否 | FPM, EDO, SDRAM | 无 | 256MB | 64MB | 否 | Ultra-33 | 是 |
| 440 FX (Natoma) | 66MHz | Pentium-II | 是 | FPM, EDO, BEDO | 奇偶校验, ECC | 1GB | N/A | 否 | 总线主控 | 是 |

### 表 2.3 SIS 芯片及其特性

| 名称 | 最大总线速度 | 支持的 CPU | SMP 支持 | 内存类型 | 内存错误处理 | 最大可缓存内存 | AGP 支持 | IDE 支持 | USB 支持 |
|---|---|---|---|---|---|---|---|---|---|
| 5511 | 66MHz | Pentium 级 | 否 | FPM, EDO | 奇偶校验 | 256MB | 否 | Bus Master | 否 |
| 5581 | 75MHz | Pentium 级 | 否 | FPM, EDO, SDRAM | 无 | 128MB | 否 | Ultra-33 | 是 |
| 5591 | 75MHz | Pentium 级 | 否 | FPM, EDO, SDRAM | 奇偶校验或 ECC | 256MB | 1x 和 2x | Ultra-33 | 是 |
| 530 | 100MHz | Pentium 级 | 否 | SDRAM, SGRAM (用于视频) | 无 | 1.5GB | 集成 2x | Ultra-66 | 是 |
| 540 | 100MHz | Pentium 级 | 否 | SDRAM | 无 | 512MB | 集成 2x | Ultra-66 | 是 |
| 600 | 100MHz | Pentium 级 | 否 | FPM, EDO, SDRAM | ECC | 1.5GB | 1x 和 2x | Ultra-53 | 是 |
| 620 | 100MHz | Celeron II/III, Celeron | 否 | SDRAM, SGRAM (用于视频) | 无 | 1.5GB | 1x 和 2x | Ultra-66 | 是 |
| 630 | 100MHz | Pentium 级 | 否 | SDRAM, SGC VQ | 无 | 1.5GB | 1x 和 4x | Ultra-66 | 是 |

若干 SiS 芯片组具备集成视频功能。具体来说，5581/5582、530、540、620 和 630 芯片组集成了视频功能。540 和 630 还集成了音频和以太网功能。大多数 SiS 芯片组的 SiS 视频功能都有 XFree86 驱动程序，但 Linux 尚不支持 SiS 音频和以太网功能。对于某些 SiS 芯片组，您可能需要使用来自 SuSE 的最新 XFree86 服务器。Linux 目前未包含对最新 SiS 芯片组中 *EIDE* 控制器的显式支持。您在 Linux 下仍可使用 EIDE 设备，但无法获得最快可能的速度。

### VIA 芯片组

VIA 科技（http://www.via.com.tw）目前是 x86 计算机非常流行的芯片组供应商（见表 2.4）。VIA 的产品线也是最多样化的之一，不仅包括用于 Pentium 和 Pentium-II 系统的芯片组，还包括用于 AMD 的 *Athlon* 的芯片组。VIA 芯片组偶尔会以其他名称出现。例如，AMD 曾短暂以 *AMD 640* 的名称销售 VIA VP-2，而 Soyo 主板则包含以 *ETEQ* 名称销售的 VIA 芯片组。

在 Pentium 级 CPU 中，VIA Apollo MVP3 芯片组是最受欢迎的之一。MVP4 基于 MVP3，但增加了基于 Trident Cyber3D 芯片组的视频功能，XFree86 3.3.4 及更高版本中存在该功能的驱动程序。MVP4 还包括音频功能，在 2.2.x 内核后期版本中已有 Linux 驱动程序。VIA 的 Apollo Pro 和 Apollo Pro 133 芯片组用于一系列尊重的 Slot 1 和 Socket 370 主板。Linux 包含对 VIA 芯片组 IDE 控制器的支持，因此您可以使用其完整 DMA 模式。

### 表 2.4 VIA 芯片组及其特性

| 名称 | 最大总线速度 | 支持的 CPU | SMP 支持 | 内存类型 | 内存错误处理 | 最大内存 | 最大可缓存 | AGP 支持 | IDE 支持 | USB 支持 |
|---|---|---|---|---|---|---|---|---|---|---|
| Apollo VP1 | 66MHz | Pentium 级 | 否 | FPM, EDO, SDRAM | 无 | 512MB | 512MB | 否 | 总线主控 | 是 |
| Apollo VP2 | 66MHz (非官方 75MHz) | Pentium 级 | 否 | FPM, EDO, SDRAM | 奇偶校验或 ECC | 512MB | 512MB | 否 | Ultra-33 | 是 |
| Apollo VPX | 75MHz | Pentium 级 | 否 | FPM, EDO, BE DO, SDRAM | 奇偶校验 | 512MB | 512MB | 否 | Ultra-33 | 是 |
| Apollo VP3 | 66MHz | Pentium 级 | 否 | FPM, EDO, SDRAM | 奇偶校验或 ECC | 1GB | 1GB | 1x 和 2x | 1x 和 Ultra-33 | 是 |
| Apollo MVP3 | 100MHz | Pentium 级 | 否 | FPM, EDO, SDRAM | 奇偶校验或 ECC | 1GB | 512MB | 1x 和 2x | 1x 和 Ultra-33 | 是 |
| Apollo MVP4 | 100MHz | P5 级 | 否 | FPM, EDO, SDRAM, DDR | 奇偶校验或 ECC | 756MB | 512MB | 集成 | Ultra-66 | 是 |
| Apollo Pro | 100MHz | Pentium Pro, Pentium II/III, Celeron | 否 | FPM, EDO, SDRAM | 奇偶校验或 ECC | 1GB | N/A | 1x 或 2x | Ultra-33 | 是 |
| Apollo Pro 133 | 133MHz | Pentium-III/III, Celeron | 否 | FPM, EDO, SDRAM | N/A | 1.5GB | N/A | 1x 或 2x | Ultra-66 (Ultra-66 版本) | 是 |
| Apollo KX133 | 200MHz | Athlon | 否 | FPM, EDO, SDRAM, VC-SDRAM | ECC | 2GB | N/A | 1x-4x | Ultra-66 | 是 |

### 板载端口

所有主板都至少包含一些板载端口。最基本而言，主板必须有一个键盘端口——事实上，许多 80486 及更早的主板*只有*键盘端口。然而，从 80486 时期后期开始，所有主板都包含多于键盘端口的端口。总体而言，主板上的端口与 Linux 附带的标准驱动程序配合良好，尽管有一些例外。例如，并非所有集成在主板上的 SCSI 或以太网端口都受 Linux 支持。

### 键盘和鼠标

AT 和 Baby AT 主板通常配有较大的 5 针 DIN 连接器用于键盘。较新的主板使用较小的 mini-DIN 连接器用于此目的。这两种类型的连接器在电气上兼容，因此如果您拥有一种类型的键盘，而主板上的连接器不对应，您可以购买一个便宜的适配器。图 2.12 展示了旧的键盘连接器和带有较新 mini-DIN 端的适配器。键盘处理相当标准化，因此您在 Linux 中无需为键盘安装特殊驱动程序。

![](img/860d0c38bd76c9ded976e9d1e179ef25_87_0.png)

**图 2.12**
左侧较大的 DIN 连接器可以通过使用类似右侧的适配器连接到较新的主板上。

**注意**

键盘处理的统一性存在两个例外。首先，*AT* 之前的计算机使用不同类型的键盘电子电路。因此，如果您有一个来自 PC XT 或类似计算机的非常旧的键盘，您将无法在现代计算机上使用它。那个时代的某些键盘有一个开关，允许您将键盘用于两种类型的计算机之一。将开关设置为 *AT*，您应该就能在现代计算机上使用它。其次，USB 键盘最近开始出现，一些系统现在附带 USB 键盘。Linux 可以使用 USB 键盘，但您可能需要编译一个支持 USB 的内核。在 2000 年初，大多数 Linux 发行版未启用此支持。在此支持成为 Linux 发行版标准部分之前，我建议避免使用 USB 键盘。

x86 硬件存在多种类型的鼠标。（我使用*mouse*一词来指代传统鼠标和替代指点设备，如轨迹球和触摸板。）两种最流行的鼠标接口是串口和 PS/2，其中 PS/2 鼠标在较新的硬件上更为流行。Linux 支持这两种鼠标类型，大多数 Linux 安装程序会自动检测和自动配置您的鼠标。大多数现代主板在后部面板上包含一个 PS/2 鼠标端口（参见图 2.7）。如果您不使用 PS/2 鼠标，某些主板的 BIOS 实用程序允许您禁用鼠标端口，从而为其他设备释放一个 IRQ。

与键盘一样，USB 鼠标最近也日益普及，但您需要内核中的 Linux 支持才能使用 USB 鼠标，而此支持尚未成为大多数发行版的标准部分。

第 15 章“键盘和鼠标”包含了更多关于键盘和鼠标的信息。

### 串行和并行端口

大多数主板包含一个并行端口和两个串行端口。通常，您使用并行端口连接打印机，有时也连接网络摄像头、外部 Zip 驱动器或扫描仪。串行端口可用于鼠标、外部调制解调器、数码相机、个人数字助理（PDA）或其他设备。少数主板，特别是来自 Compaq 等大型制造商的主板，只包含一个串行端口。

现代主板无不支持标准化的现代并行和串行端口协议。Linux 对这些设备的支持相当成熟，因此，假设硬件没有缺陷，您在使用任何主板的并行或串行端口时不应有任何问题。

80486 时代及更早的主板通常不包含串行或并行端口。在这些计算机上，您必须在 ISA 卡上添加这些端口。如果您正在翻新旧系统，并且看不到主板上的这些端口，原因就在于此。

第 16 章“并行和串行端口”更详细地介绍了这些端口。

