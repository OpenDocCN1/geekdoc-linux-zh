
RAID 系统可以方便地通过其 ROM 设置程序进行配置（无需启动 MS-DOS 进行配置）。借助其监控实用程序 `gdtmon`，可以在运行期间管理整个 ICP RAID 系统（检查传输速率、设置控制器和硬盘的参数、更换有缺陷的硬盘等）。

该实用程序使 ICP Vortex 控制器在 Linux 硬件 RAID 控制器中脱颖而出。

## Mylex RAID 控制器

DAC960 驱动程序支持所有当前的 Mylex PCI RAID 控制器，包括 eXtremeRAID 1100 (DAC1164P)、AcceleRAID 150/200/250 以及较旧的 DAC960PJ/PG/PU/PD/PL 型号。Red Hat Linux 6.0+ 和 SuSE Linux 6.2 包含对这些控制器的支持。除了安装驱动程序外，还需要一组特殊的实用程序，这些程序提供 lilo 和 fdisk 的源代码路径和静态链接可执行文件，以便识别 DAC960 RAID 设备。驱动程序、实用程序和其他信息可通过 Dandelion Digital 的 Linux DAC960 页面获取：http://www.dandelion.com/Linux/DAC960.html。

## 应该使用什么硬件？

在选择 RAID 硬件时，需要考虑两个因素：

- 控制器类型的选择（例如 SCSI 到 SCSI 或基于主机的）
- 磁盘机箱类型的选择（这决定了热插拔、警告和其他功能）

### 控制器类型

鉴于这些选项，如果你正在寻找 RAID 解决方案，需要仔细考虑你的需求。根据你的具体用途以及要使用的 RAID 级别，某些卡可能比其他卡更好。例如，SCSI 到 SCSI 适配器可能不如基于主机的适配器。请参阅 EATA-DMA 驱动程序作者 Michael Neuffer 在其 Linux 高性能 SCSI 和 RAID 页面上的讨论：http://www.uni-mainz.de/~neuffer/scsi/。

### 机箱类型

机箱类型会影响驱动器的热插拔功能、警告系统（即是否会有故障指示，以及你是否会知道哪个驱动器发生了故障），以及驱动器的工作条件（例如冗余冷却和电源）。DPT 提供的机箱工作效果非常好，但价格昂贵。Wetex (http://www.wetex.com) 的机箱缺乏 DPT 机箱的热插拔能力，但在其他方面表现良好。

![](img/6c13bcf02a08ad7923caab46f051d96a_167_0.png)

## 安装

安装分为两部分：配置硬件和配置内核。

### 安装和配置硬件

请参阅说明手册以安装控制器和驱动器。对于 DPT，由于尚不存在适用于 Linux 的存储管理器，你必须创建一张包含系统文件的 MS-DOS 格式化磁盘（通常在 MS-DOS 提示符下使用 format /s 命令创建）。你还需要使用适用于 MS-DOS 的 DPT 存储管理器，为了安全起见，最好为其制作一份副本。

硬件就位后，使用 DOS 系统盘启动。将 DOS 磁盘替换为存储管理器，然后使用以下命令调用存储管理器：

```
a:\dptmgr
```

大约等待一分钟左右，你会看到一个选项菜单。将一组磁盘配置为硬件 RAID（单个逻辑阵列）。选择“other”作为操作系统。

MS-DOS 存储管理器使用鼠标操作要容易得多，因此你可能希望在创建的系统启动盘上包含鼠标驱动程序。

从技术上讲，应该可以在 Linux 下运行 SCO 存储管理器，但这可能得不偿失。在 Linux 下运行 MS-DOS 存储管理器可能更容易。

### 配置内核

你需要配置内核以支持 SCSI 和相应的底层驱动程序。有关编译内核的指导，请参阅第 11 章“构建 Linux 内核”。或者，查阅 Kernel HOWTO http://sunsite.unc.edu/mdw/HOWTO/Kernel-HOWTO.html 获取有关如何编译内核的信息。在 SCSI 支持选项中选择“yes”后，在底层驱动程序部分，选择你需要的驱动程序（对于大多数符合 EATA DMA 的 (DPT) 卡，选择 EATA DMA 或 EATA ISA/EISA/PCI；对于 DPT 非常古老的 PM2001 和 PM2012A，选择 EATA PIO）。大多数驱动程序，包括 EATA DMA 和 EATA ISA/EISA/PCI 驱动程序，在最近的内核版本中应该可用。

内核编译完成后，重新启动；如果一切设置正确，你应该会看到驱动程序将 RAID 识别为单个 SCSI 磁盘。如果使用 RAID-5，你会看到此磁盘的大小是实际可用磁盘空间的三分之二。

### 启动消息

如果你使用 EATA DMA 驱动程序，启动时看到的消息应该类似这样：

```
EATA (Extended Attachment) driver version: 2.59b
developed in co-operation with DPT
(c) 1993-96 Michael Neuffer, mike@i-Connect.Net
Registered HBAs:
HBA no. Boardtype   Revis  EATA Bus  BaseIO IRQ DMA Ch Id Pr QS S/G IS
scsi0 : PM334UW      v07L.0 2.0c PCI  0xef90 10  DM3  7  N  64 252 Y
scsi1 : PM2144UW     v07L.2 0.0c PCI  0xef50  9  BMST 1  7  N  64 252 Y
scsi2 : PM2044UW     v07K.2 0.0c PCI  0xef10 11  BMST 1  7  N  64 252 Y
scsi0 : EATA (Extended Attachment) HBA driver
scsi1 : EATA (Extended Attachment) HBA driver
scsi2 : EATA (Extended Attachment) HBA driver
scsi : 3 hosts.
  Vendor: DPT       Model: RAID-5              Rev: 07L0
  Type: Direct-Access                      ANSI SCSI revision: 02
Detected scsi disk sda at scsi0, channel 0, id 0, lun 0
scsi0: queue depth for target 0 on channel 0 set to 64
  Vendor: DPT       Model: ATOS                Rev: 07LY
  Type: Direct-Access                      ANSI SCSI revision: 02
Detected scsi disk sdb at scsi1, channel 0, id 8, lun 0
scsi1: queue depth for target 8 on channel 0 set to 64
  Vendor: SONY      Model: SDT-9000            Rev: 0200
  Type: Sequential-Access                  ANSI SCSI revision: 02
scsi2: queue depth for target 0 on channel 0 set to 64
SCSI device sda: hdwr sector=512 bytes. Sectors=105676800 [51600 MB] [51.6 GB]
sda: sda1
SCSI device sdb: hdwr sector=512 bytes. Sectors=35561984 [17364 MB] [17.4 GB]
sdb: sdb1
```

以上显示内容对应的是一个使用三个 DPT SCSI 控制器的设置，其中包含两个 RAID-5 阵列，大小分别为 51.6GB（七个 9GB 磁盘）和 17.4GB（三个 9GB 磁盘）。

如果你使用 EATA ISA/EISA/PCI 驱动程序，启动时看到的消息应该类似这样：

```
EATA0: IRQ 11 mapped to IO-APIC IRQ 16.
EATA/DMA 2.0x: Copyright 1994-1999 Dario Ballabio.
EATA config options -> tc:y, lc:n, mq:16, eh:y, rs:y, et:n.
EATA0: 2.0C, PCI 0xef10, IRQ 16, BMST, SG 122, MB 64.
EATA1: SCSI channel 0 enabled, host target ID 7.
EATA1: IRQ 9 mapped to IO-APIC IRQ 18.
EATA1: 2.0C, PCI 0xef50, IRQ 18, BMST, SG 122, MB 64.
EATA1: wide SCSI support enabled, max_id 16, max_lun 8.
EATA1: SCSI channel 0 enabled, host target ID 7.
scsi0 : EATA/DMA 2.0x rev. 5.10.00
scsi1 : EATA/DMA 2.0x rev. 5.10.00
scsi : 2 hosts.
  Vendor: SONY      Model: SDT-9000            Rev: 0200
  Type: Sequential-Access                  ANSI SCSI revision: 02
EATA0: scsi0, channel 0, id 0, lun 0, cmds/lun 2.
  Vendor: DPT       Model: ATOS                Rev: 07LY
  Type: Direct-Access                      ANSI SCSI revision: 02
Detected scsi disk sda at scsi1, channel 0, id 8, lun 0
EATA1: scsi1, channel 0, id 8, lun 0, cmds/lun 16, unsorted, tagged.
SCSI device sda: hdwr sector=512 bytes. Sectors=35561984 [17364 MB] [17.4 GB]
sda: sda1
```

以上显示内容对应的是一个使用两个 DPT SCSI 控制器的设置，其中包含一个大小为 17.4GB（三个 9GB 磁盘）的 RAID-5 阵列。

## 配置和测试阵列

现在，你可以开始将 RAID 5 阵列视为普通磁盘来使用。你需要做的第一件事是对磁盘进行分区（使用 fdisk）。然后，你需要建立一个 ext2 文件系统。这可以通过以下命令完成：

```
# mke2fs /dev/sdXN
```

/dev/sdXN 是 SCSI 分区的名称。完成此操作后，你就可以挂载这些分区，并像使用任何其他磁盘一样使用它们（包括在 /etc/fstab 中添加条目）。

## 热插拔

要测试阵列的热插拔功能，只需在系统运行期间从阵列中移除一个驱动器。如果 RAID 5 阵列配置正确且工作正常，系统应该在移除一个磁盘的情况下继续运行。性能会有所下降，因为缺失的数据必须在访问磁盘时即时重建。

如果你重新插入移除的磁盘或新磁盘，系统将继续运行，同时重建该磁盘的数据。重建期间性能会受到影响，如果阵列使用频繁，用户会明显感觉到。

> **提示：**请记住，RAID 5 仅提供有限的冗余。你不能同时从阵列中移除两个驱动器。如果这样做，阵列将停止工作，数据将丢失，你需要从备份中恢复。

## 性能

你可以使用 bonnie 程序测试 RAID 阵列的性能。bonnie 是一个文件系统基准测试工具，可从 http://www.textuality.com/bonnie/ 获取。

bonnie 是可用的最佳“开放系统”基准测试工具之一，用于衡量系统 I/O 性能。它和其他基准测试工具都可以在 AC&NC RAID 和磁盘存储基准测试页面 http://www.acnc.com/benchmarks.html 获取。

> **提示：**无论你使用哪种类型的 RAID 或哪种基准测试工具，请务必也在真实的应用环境中测试性能。不要只依赖基准测试结果！

以下是使用 3344 UW 控制器的阵列的 bonnie 计时输出示例：

