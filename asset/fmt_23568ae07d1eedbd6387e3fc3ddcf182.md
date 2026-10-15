
目前，一个受良好支持的基于主机的硬件 RAID 控制器（即在 Linux 下存在一个或多个受良好支持的驱动程序的控制器）是由 DPT (`http://www.dpt.com`) 制造的。然而，也存在其他可以在 Linux 下工作的基于主机的控制器和 SCSI 到 SCSI 控制器。其中包括 Syred (`http://www.syred.com`)、`ICP-Vortex` (`http://www.icp-vortex.com`) 和 Mylex (`http://www.mylex.com`) 制造的控制器。有关更多信息，请参阅 Linux RAID 解决方案页面 `http://linas.org/linux/raid.html`。

### DPT 控制器

基本上所有 SmartRAID IV 和 V 控制器都受支持。安装和配置部分将重点介绍基于 SCSI 的硬件 RAID 的设置，主要针对 DPT 基于主机的适配器，尽管此处应用的原理相当通用。具体来说，Smartcache IV PM2144UW 和 PM3334UW 控制器已在 Linux 2.0.3x 和 2.2.x 内核上使用 DPT 提供的机箱进行了测试。SmartRAID V Decade 卡需要额外的软件。有关更多详细信息和最新信息，请查阅位于 `http://www.ram.org/computing/linux/dpt_raid.html` 的《DPT 硬件 RAID HOWTO》。

### ICP Vortex 控制器

ICP Vortex 拥有一整套支持 Linux 的磁盘阵列控制器。ICP 驱动程序自 Linux 内核 2.0.3 版本起就包含在内。所有主要的 Linux 发行商——SuSE、LST Power Linux、Caldera 和 Red Hat——都支持将 ICP 控制器用作引导/安装控制器。

RAID 系统可以方便地通过其 ROM 设置程序进行配置（无需启动 MS-DOS 进行配置）。借助其监控实用程序 `gdtmon`，可以在运行期间管理整个 ICP RAID 系统（检查传输速率、设置控制器和硬盘的参数、更换有缺陷的硬盘等）。

该实用程序使 ICP Vortex 控制器在 Linux 硬件 RAID 控制器中脱颖而出。

### Mylex RAID 控制器

`DAC960` 驱动程序支持所有当前的 Mylex PCI RAID 控制器，包括 eXtremeRAID 1100 (`DAC1164P`)、`AcceleRAID 150/200/250` 以及较旧的 `DAC960PJ/PG/PU/PD/PL` 型号。Red Hat Linux 6.0+ 和 SuSE Linux 6.2 包含对这些控制器的支持。除了安装驱动程序外，还需要一组特殊的实用程序，这些程序提供 `lilo` 和 `fdisk` 的源代码路径和静态链接可执行文件，以便识别 `DAC960` RAID 设备。驱动程序、实用程序和其他信息可通过 Dandelion Digital 的 Linux DAC960 页面获取：`http://www.dandelion.com/Linux/DAC960.html`。

## 应该使用什么硬件？

在选择 RAID 硬件时，需要考虑两个因素：

- 控制器类型的选择（例如 SCSI 到 SCSI 或基于主机的）
- 磁盘机箱类型的选择（这决定了热插拔、警告和其他功能）

### 控制器类型

鉴于这些选项，如果你正在寻找 RAID 解决方案，需要仔细考虑你的需求。根据你的具体用途以及要使用的 RAID 级别，某些卡可能比其他卡更好。例如，SCSI 到 SCSI 适配器可能不如基于主机的适配器。请参阅 EATA-DMA 驱动程序作者 Michael Neuffer 在其 Linux 高性能 SCSI 和 RAID 页面上的讨论：`http://www.uni-mainz.de/~neuffer/scsi/`。

### 机箱类型

机箱类型会影响驱动器的热插拔功能、警告系统（即是否会有故障指示，以及你是否会知道哪个驱动器发生了故障），以及驱动器的工作条件（例如冗余冷却和电源）。DPT 提供的机箱工作效果非常好，但价格昂贵。Wetex (`http://www.wetex.com`) 的机箱缺乏 DPT 机箱的热插拔能力，但在其他方面表现良好。

![](img/6c13bcf02a08ad7923caab46f051d96a_167_0.png)

## 安装

安装分为两部分：配置硬件和配置内核。

### 安装和配置硬件

请参阅说明手册以安装控制器和驱动器。对于 DPT，由于尚不存在适用于 Linux 的存储管理器，你必须创建一张包含系统文件的 MS-DOS 格式化磁盘（通常在 MS-DOS 提示符下使用 `format /s` 命令创建）。你还需要使用适用于 MS-DOS 的 DPT 存储管理器，为了安全起见，最好为其制作一份副本。

硬件就位后，使用 DOS 系统盘启动。将 DOS 磁盘替换为存储管理器，然后使用以下命令调用存储管理器：

```
a:\dptmgr
```

大约等待一分钟左右，你会看到一个选项菜单。将一组磁盘配置为硬件 RAID（单个逻辑阵列）。选择“other”作为操作系统。

MS-DOS 存储管理器使用鼠标操作要容易得多，因此你可能希望在创建的系统启动盘上包含鼠标驱动程序。

从技术上讲，应该可以在 Linux 下运行 SCO 存储管理器，但这可能得不偿失。在 Linux 下运行 MS-DOS 存储管理器可能更容易。

### 配置内核

你需要配置内核以支持 SCSI 和相应的底层驱动程序。有关编译内核的指导，请参阅第 11 章“构建 Linux 内核”。或者，查阅 Kernel HOWTO `http://sunsite.unc.edu/mdw/HOWTO/Kernel-HOWTO.html` 获取有关如何编译内核的信息。在 SCSI 支持选项中选择“yes”后，在底层驱动程序部分，选择你需要的驱动程序（对于大多数符合 EATA DMA 的 (DPT) 卡，选择 EATA DMA 或 EATA ISA/EISA/PCI；对于 DPT 非常古老的 PM2001 和 PM2012A，选择 EATA PIO）。大多数驱动程序，包括 EATA DMA 和 EATA ISA/EISA/PCI 驱动程序，在最近的内核版本中应该可用。

内核编译完成后，重新启动；如果一切设置正确，你应该会看到驱动程序将 RAID 识别为单个 SCSI 磁盘。如果使用 RAID-5，你会看到此磁盘的大小是实际可用磁盘空间的三分之二。

#### 启动消息

如果你使用 EATA DMA 驱动程序，启动时看到的消息应该类似这样：
