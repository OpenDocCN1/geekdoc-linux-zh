
### 声卡

- 6850 UART（通用异步收发传输器）MIDI（乐器数字接口）
- Adlib (OPL2) 声卡
- ATI Stereo F/X（兼容 Sound Blaster）
- Audio Excell DSP16
- Aztec Sound Galaxy NX Pro
- 基于 Crystal CS4232（PnP — 即插即用）的显卡
- ECHO-PSS（Orchid SW32 和 Cardinal DSP16）
- Ensoniq SoundScape（但你必须启动 DOS 来初始化显卡）
- Gravis Ultrasound, Ultrasound MAX 以及 Ultrasound 16-bit 采样子板
- Logitech SoundMan 16 (PAS-16 兼容），SoundMan Games 和 SoundMan Wave (Jazz16/OPL4)
- MediaRIX AudioTriX Pro
- Media Vision 3D Jazz16（兼容 Sound Blaster），Pro Audio Spectrum 16 (PAS-16) 和 Pro Sonic 16 Jazz
- Microsoft Sound System (AD1848)
- MPU-401 MIDI
- OAK OTI-601D 卡（Mozart）
- Opti 82C928/82C929 卡（82C928/82C929 卡（MAD16/ISP/Mozart））
- Sound Blaster, Sound Blaster 16, 和 Sound Blaster Pro
- Sound Galaxy NX
- ThunderBoard（兼容 Sound Blaster）
- Turtle Beach Wavefront (Maui, Tropez)
- WaveBlaster 以及其他 Sound Blaster 16 子板
- ESS Audio 芯片，如 688, 1868

#### 网适配器

只有当你将 PC 连接到以太网时，才需要网络适配器。Linux 支持多种以太网适配器。也支持 Archnet 和 IBM 的令牌环。关于 Linux 对令牌环和其他适配器的支持更多信息，请参见第 16 章。

以下是 Linux 支持的以太卡列表：

- 3Com 3C503, 3C505, 3C507, 3C509B (ISA 总线) 和 3C579 (或 EISA 总线)
- 用于 PCI 总线的 3Com Etherlink II Vortex Ethercards (3C590, 3C592, 3C955, 3C597)
- 用于 PCI 总线的 3Com Etherlink Boomerang Ethercards (3C900, 3905) 以及用于 ISA 总线的 3Com Fast EtherLink (3C515)
- 用于 ISA 和 PCI 的基于 LANCE (7C960) 的以太卡
- Allied Telesis AT1500, AT1700 和 LA100-T
- Ansell Communications AC3200 EISA
- Apricot Xen
- AT&T GIS WaveLAN
- Cabletron E21xx（任意数字）
- Cogent EM110
- Danpex EN9400
- 数字设备公司 (DEC) DEPCA, EtherWORKS, EtherWORKS-3, DE425 (EISA), DE434 (PCI), DE435 (PCI), DE450, DE500, DE500-XA 和 DEC Silver
- 通通 FMV-181, FMV-182, FMV-183, FMV-184
- 惠尔--普罗 HP J2405A, PCLAN (27245 和 27xxx 系列), PCLAN PLUS (2724B 和 27252), 以及 10/100VG PCLAN (J2577, J2573, 2724B, 2585) (ISA, EISA 和 PCI)
- ICL EtherTeam 16i/32
- Intel EtherExpress 和 EtherExpress Pro
- KTI ET16/P-D2, ET16/P-DC ISA
- New Media Ethernet
- Novell Ethernet NE10000, NE1500, NE2000 和 NE2100（所有克隆版本都可能无法工作）
- PureData PDCUC8028 和 PCI30823
- Racal-Interlan NI5210（基于 82586 以太网芯片），NI6510（使用 AMD 7990 LANCE 芯片，且不支持超过 16MB 的内存）
- SEEQ 8005
- Schneider & Koch G16
- SMC (西部数据) WD8003, WD8013, SMC Elite, SMC Elite Plus, SMC Elite 16 Ultra, SMC EtherEZ (ISA), SMC 9000 系列, SMC PCIether10/100
- Zenith Z-Note 和 IBM ThinkPad 300 内置以太网适配器
- Znyx 312 Etherray

如果你计划在家里 PC 上使用 Linux，你可以通过 `SLIP` 或 `PPP` 连接互联网。详情请参见第 18 章。

#### 硬件清单

现在你已经看到了 Linux 支持的各种硬件外围总结，你应该大致了解你是否拥有运行 Linux 的正确 PC/硬件。如果你正在购买运行 Linux 的 PC，硬件列表应该帮助你决定新 PC 的硬件配置。

总结来说，通过以下清单以查看你是否准备好从本书的随附 CD-ROM 安装 Linux：

- 你的 PC 是否具有 80386 或更快的处理器，带有 ISA、EISA、VLB、MCA 或 PCI 总线；至少 8MB 内存；高密度软盘驱动器以及大硬盘（至少 500MB）？
- 你的 PC 是否具有 Linux 支持的 CD-ROM 驱动器？
- 如果你计划在 PC 上同时运行 Windows 和 Linux，你需要 1GB 的磁盘空间。

## 第一部分：配置你的 Linux 系统

### 在安装 Linux 之前在 MS-DOS 或 Windows 中操作

如果你是 MS-DOS 或 Windows 的新手，你可能会发现遵循某些必须在 MS-DOS 下执行的 Linux 安装步骤非常困难。以下是你执行必要的安装之前应该了解的一些术语和概念：

- 第一个软驱驱动器 (`A`) 是软盘驱动器。如果你将软盘插入 `A` 槽并打开电源，你的 PC 将自动尝试从软盘启动。（许多新 PC 允许你设置启动设备；默认情况下，几乎所有 PC 都将第一个软驱驱动器配置为启动设备。）此功能是内置在计算机中的，不取决于你系统硬盘上安装了什么操作系统。在大多数新系统中，`A` 盘是一个 3.5 英的软盘驱动器。许多旧系统使用 5.25 英的软盘作为 `A`。要安装 Linux，你需要一个高密度软盘驱动器。

- 物理硬盘可以被划分为若干部分，每部分都可以被视为独立的逻辑硬盘。虽然大多数新 PC 使用整个硬盘作为单个驱动器，但你可以将磁盘划分为多四个区域，称为主分区。要在你的硬盘上安装 Linux，你必须为 Linux 文件系统创建至少两个分区，另一个用于交换空间（一种虚拟内存，可以临时存储物理内存内容的虚拟内存）。如果你想在一个分区中保留 Windows 并同时安装 Linux，你需要三个分区。

- 重新划分硬盘。如果你的硬盘只有一个分区，那么创建更多分区的过程被称为重新划分。要对磁盘进行重新划分，你必须先备份其内容。然后使用 MS-DOS 的 `FDISK` 命令删除分区并创建新分区，最后将旧内容恢复到其中一个分区中。红帽 Linux 发行版（在本本书的 CD-ROM 上）包含一个名为 `FIPS` 的 MS-DOS 工具，你可以用它在不破坏旧分区内容的情况下对硬盘进行重新划分。该实用程序保证能够完美运行，因此在用 `FIPS` 重新划分硬盘之前，你仍然需要备份你的重要文件。

- MS-DOS `FDISK` 程序仅定义物理磁盘的一个区域以供 MS-DOS 等操作系统使用。你必须准备该磁盘区域，使其能够用于存储文件和目录。格式化是为文件系统创建分区的过程。

- 目录和文件。在 MS-DOS 中，一个驱动器被划分为多个目录。每个目录又可以包含其他目录和文件。文件是存储实际信息的地方。目录帮助你组织文档和程序。例如，Windows 操作系统的所有文件都在 `C:\directory` 中。`C:\WINDOWSSYSTEM` 目录包含 Windows 需要的一些特殊文件。如你所示，反斜杠字符作为目录之间的分隔符。目录 `C:\` 被称为根目录；`C:\WINDOWS` 是根目录的子目录；`C:\WINDOWS\SYSTEM` 是从根目录向下两层。

## 第一章：安装 Linux
