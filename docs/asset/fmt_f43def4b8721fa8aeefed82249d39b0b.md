
然而，某些设备驱动程序不支持您需要的配置选项。在这种情况下，您可以配置系统启动到 DOS 或 Linux。要配置卡，请进入 DOS 并运行配置卡的 DOS 程序。然后，通过例如启动到 Linux。

### 键盘

Red Hat Linux 支持 AT 风格和 PS/2 风格的键盘作为 Tier 1 设备。

### 鼠标

Red Hat Linux 包括对标准串口鼠标和 PS/2 鼠标的支持，这些鼠标通常在 Tier 1 支持。总线鼠标通常在 Tier 2 支持。最近的微软串口鼠标使用一种特殊的协议，尚未完全移植。微软的 IntelliMouse（滚轮鼠标）被列为 Tier 3 设备。

### 调制解器

Red Hat 在 Tier 1 支持大多数外部调制解器，以及基于 Lucent Venus 芯片组的内部 PCI 调制解器。遗憾的是，一类被称为 WinModems 的调制解器需要特殊的驱动程序才能运行。制造商随这些设备捆绑 Win32 软件，但并未为其他操作系统发布软件。因此，Red Hat Linux 不支持此类调制解器。它们也被列为与即插用内部调制解器不兼容，尽管可以通过 `isapnp` 或 `setser1a` 进行配置（尽管非常不便）。

### 网络适配器

- 3Com 3C501
- 3Com 3C905B, 3C905C（尽管 3Com 最近提供的驱动程序可能会缓解这个问题）
- 3Com ISA Etherlink XL (3Com 3C515)
- General Instruments SB1000
- Intel EtherExpress 100plus
- Intel EtherExpress Pro/10 PCI（兼容）
- Intel EtherExpress Pro/100B
- Linksys Fast 10/100 tulip 克隆版
- SeaLevel Systems 4012, 4021

### 声卡

- Silicon Integrated System Corporation Sis 900 PCI
- 使用 MX987x5 芯片的 Macbookix, Inc. 卡
- Xircom 以太网适配器（不兼容）

Red Linux发行版对声卡的支持在所有 Linux 发行版中是最好的。然而，声卡支持仍然是 Linux 的一个弱环节。声卡目前在 Tier 1 支持。以下声卡在 Tier 2 支持：

- Acer Notebook Sound
- AdLib
- Advance Logic ALS-007
- Compaq Deskpro XL sound
- Creative/Ensoniq Audio PCI 1371
- Crystal CS423x 声芯片
- Ensoniq Audio PCI 1370 (SoundBlaster 64/128 PCI)
- Ensoniq Soundscape
- ESS1688 AudioDrive
- ESS1868 AudioDrive
- ESS688 AudioDrive
- Gravis UltraSound
- Gravis UltraSound MAX
- Gravis UltraSound PnP
- Logitech SoundMan 16
- Logitech SoundMan Games（不是 SM16 或 SM Wave）
- MAD16 Pro (OPTI 82C929/82C930)
- MediarixAudio Pro (MT-0002-PC 控制芯片)
- MediaVision Jazz16 (ProSonic, SoundMan Wave)
- miroSOUND PCM12
- Mozart/MAD16 (OPTI 82C928)
- OPL3-SA1 声芯片

## 设备支持 33

- OPL3-SA2/3/x 声芯片
- Pro Audio Spectrum/Studio 16
- PSS (Orchid SW32, Cardinal DSP16)
- S3 SonicVibes
- Sound Blaster
- Sound Blaster 16/PNP
- Sound Blaster 32/64 AWE
- Sound Blaster DS
- Sound Blaster Pro
- Turtle Beach MultiSound Classic/Monterey/Tahiti
- Turtle Beach MultiSound Pinnacle/Fiji
- Windows Sound System (AD1848/CS4248/CS4231)

这些卡的克隆版本或列为兼容这些卡的卡并不一定被支持。

### 显卡

XFree86 项目提供了一个免费分发的 X Window 系统实现（也称为 X）。Red Hat Linux 发行版使用 XFree86 的 X 实现，并通常支持 XFree86 实现所支持的显卡。然而，存在若干异常情况，因此你应该咨询 Red 硬件兼容性列表 (www.redhat.com/support/hardware)，而不是由 XFree86 项目发布的显卡支持列表。支持和不支持的显卡列表太长，无法进行总结。在 Red Hat Linux 支持存在问题的知名显卡中，笔记本笔记本显卡，制造商通常会针对笔记本电脑的 LCD 进行定制。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_58_0.png)

笔记本带来了影响 Linux 兼容性的特殊复杂。例如，笔记本制造商经常在具有相同型号的笔记本中使用各种硬件组件。通常情况下，判断笔记本是否与 Red Hat Linux 兼容的唯一方法是在笔记本上安装、配置并运行 Linux。这种混乱的局面已变得常见，现在一些制造商正在销售预装 Linux 的笔记本电脑。然而，此类笔记本并不一定受到 Red Hat Linux 的官方支持。

©2000 SYBEX, Inc., Alameda, CA www.sysex.com

### 其他设备

在 Red Hat Linux 支持或兼容的其他字符设备中，包括以下设备：

- 红外设备
- 摇杆
- 多端口串口设备
- 打印机
- 扫描仪

IDE 驱动器的设备名称如 `/dev/hda`、`/dev/hdb` 和 `/dev/sdb` 等。SCSI 驱动器的设备名称如 `/dev/sda`、`/dev/sdb` 等。分区用数字指定，并将 `1` 附加在驱动器名称之后。因此，第一个 IDE 驱动器的第一个分区命名为 `/dev/hda1`，第二个 SCSI 驱动器的第三个分区命名为 `/dev/sdb3`。

### 主分区、扩展分区和逻辑分区

硬盘只能有四个普通分区，称为主分区。然而，主分区中的一个可以被指定为扩展分区。扩展分区不包含文件系统；相反，它包含最多 12 个其他分区，称为逻辑分区。第一个逻辑分区始终被指定为分区 5，即使定义的分区少于四个也是如此。图 2.2 显示了典型的硬盘分区结构。

图 2.2 典型的硬盘分区结构

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_62_0.png)

### 分区类型

Linux 使用的分区是以下两种主要类型之一：

- `Linux 原生 (Linux Native)`：用于存放包含程序和数据文件的标准 Linux 文件系统。
- `Linux 交换 (Linux Swap)`：用于临时存放从物理内存交换到硬盘的内存内容。

Red Hat Linux 还支持多种分区类型，包括 MS-DOS、VFAT、HPFS 和 NTFS。标准的 Red Hat Linux 内核无法访问 HPFS 和 NTFS 文件系统；如果你需要这些支持，则必须重新编译内核。

Linux 内核支持最大为 2GB 的交换分区。最多可以定义八个交换分区。

### 挂载点

与 UNIX 一样，Linux 将块设备的分区挂载为统一系统中的子目录。存放分区内容的目录称为其挂载点。以下两个通过挂载点命名的分区尤为重要：

- `根文件系统`
- `/boot` 启动分区，包含 Linux 内核

根分区在系统初始化过程开始时挂载，此时内核本身已加载到内存中。内核必须知道它的身份，这通常由 Red Hat Linux 系统上的 `LILO` 启动加载程序传递给内核。其他分区通过被挂载为根文件系统的子目录被集成到系统中。

启动分区是一个较小的分区，用于绕过许多系统 BIOS 的 1024 柱体限制。通过将启动分区定位在前 1024 个柱体内，可以确保 Linux 内核对 BIOS 可用。

### 总结

在本章中，你学习了 Linux 对各种硬件设备的支持。以下是本章涵盖的最重要主题：

- `硬件兼容性`：Red Hat, Inc. 发布了与 Red Hat Linux 兼容并支持的硬件列表。
- `硬件配置`：硬件设备通常必须分配一个唯一的 IRQ 和基 I/O 地址。某些设备还必须分配唯一的 DMA。
- `适配器卡`：配置 PCI 适配器卡是简单的。配置其他类型的卡（特别是 ISA 即插用卡）可能会困难。

总结 39
