
## 分区类型参考

| 编号 | 文件系统类型 | 编号 | 文件系统类型 | 编号 | 文件系统类型 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 05 | 扩展 | 50 | OnTrack DM | A5 | BSD/386 |
| 06 | FAT16 | 51 | OnTrack DM6 Aux1 | A6 | OpenBSD |
| 07 | HPFS/NTFS | 52 | CP/M | A7 | NeXTSTEP |
| 08 | AIX | 53 | OnTrack DM6 Aux3 | B7 | BSDI fs |
| 09 | AIX 可引导 | 54 | OnTrack DM6 | B8 | BSDI 交换 |
| 0A | OS/2 引导管理器 | 55 | EZ-Drive | C1 | DRDOS/sec (FAT-12) |
| 0B | Win95 FAT32 | 56 | Golden Bow | C4 | DRDOS/sec (FAT-16) |
| 0C | Win95 FAT32 (LBA) | 5C | Priam Edisk | C6 | DRDOS/sec (FAT-16) |
| 0E | Win95 FAT16 (LBA) | 61 | SpeedStor | C7 | Syrix |
| 0F | Win95 扩展 (LBA) | 63 | GNU HURD 或 SysV | DB | CP/M/CTOS / ... |
| 10 | OPUS | 64 | Novell Netware 286 | E1 | DOS 访问 |
| 11 | 隐藏 FAT12 | 65 | Novell Netware 386 | E3 | DOS 只读 |
| 12 | Compaq 诊断 | 70 | DiskSecure 多重引导 | E4 | SpeedStor |
| 14 | 隐藏 FAT16 <32M | 75 | PC/IX | EB | BeOS fs |
| 16 | 隐藏 FAT16 | 80 | 旧版 Minix | F1 | SpeedStor |
| 17 | 隐藏 HPFS/NTFS | 81 | Minix/旧版 Linux | F4 | SpeedStor |
| 18 | AST Windows 交换文件 | 82 | Linux 交换 | F2 | DOS 辅助 |
| 24 | NEC DOS | 83 | Linux (ext3) | FE | LANstep |
| 3C | PartitionMagic 恢复 | 84 | OS/2 隐藏 C: 驱动器 | FF | BBT |
| 40 | Venix 80286 | 85 | Linux 扩展 | | |
| 41 | PPC PreP 引导 | 86 | NTFS 卷集 | | |

在“磁盘设置”部分，您可以看到连接到计算机的每个硬盘。首先显示的是驱动器名称。“几何结构”部分（Geom）分别显示了磁盘上的柱面数、磁头数和扇区数。磁盘总空间、已用空间和空闲空间以兆字节为单位显示。

## 分区的原因

关于如何划分硬盘，存在不同的观点。以下是一些问题：

- **是否希望安装另一个操作系统？** 如果您希望在计算机上同时安装 Windows 和 Linux，您至少需要一个 Windows 分区（Win95 FAT16 或 VFAT 类型）、一个 Linux 分区（Linux ext3）和一个 Linux 交换分区。
- **它是多用户系统吗？** 如果您独自使用该系统，您可能不需要很多分区。对操作系统进行分区的一个原因是防止整个系统一次性耗尽磁盘空间。这也起到限制个人在其主目录中可使用的空间的作用。
- **您有多个硬盘吗？** 每个硬盘至少需要一个分区。如果系统有两个硬盘，您可以将其中一个分配给 `/`，另一个分配给 `/home`（如果有很多用户）或 `/var`（如果计算机是共享大量数据的服务器）。

## 删除、添加和编辑分区

在添加分区之前，硬盘上需要有可用的空闲空间。如果硬盘上的所有空间当前都分配给了一个分区（这在 DOS 或 Windows 中很常见），在您想要占用另一个分区的空间之前，必须先删除或调整该分区的大小。关于回收磁盘空间的章节讨论了如何在现有单分区系统中添加分区而不丢失信息。

> **注意：** 在删除分区之前，请确保备份您想要保留的任何数据。删除分区时，其所有数据都会丢失。

Disk Druid 比 `fdisk` 实用程序灵活性稍差，但更直观。Disk Druid 允许您删除、划分和编辑分区。

> **提示：** 如果您创建多个分区，请确保在适当的位置有足够的空间以完成安装。例如，大多数 Linux 软件安装在 `/usr` 目录（及其子目录）中，而大多数用户数据最终会添加到 `/home` 或 `/var` 目录中。

要在 Disk Druid 中删除分区，请执行以下操作：

1. 从主 Disk Druid 窗口上的“当前磁盘分区”列表中选择一个分区（点击它或使用箭头键）。
2. 若要立即删除分区（无确认提示！），请点击 Delete。
3. 如果操作失误，请点击 Reset 返回到开始使用 Disk Druid 时的分区状态。

要在 Disk Druid 中添加分区，请从主 Disk Druid 窗口执行以下步骤：

1. 选择 New。会出现一个窗口，允许您创建新分区。
2. 输入挂载点名称（该分区将挂载到 Linux 文件系统的目录）。您至少需要一个根（/）分区和一个交换分区。
3. 选择该分区将使用的文件系统类型。您可以从 Linux 原生文件系统（ext2 或 preferably ext3）、软件 RAID、Linux 交换（swap）或 Windows FAT（vfat）中进行选择。

> **提示：** 若要创建与其他不同的文件系统类型，请暂时保留所需的空间为空闲。您可以点击 Back 按钮并选择 fdisk 而不是 Disk Druid。或者，您可以等待安装完成后，使用 `fdisk` 或 `sfdisk` 创建您想要类型的分区。

4. 输入用于该分区的兆字节数（在 Size 字段中）。如果希望该分区扩展以填充硬盘的剩余部分，您可以在该字段中输入任何数字（1 即可）。
5. 如果有多个硬盘，请从 Allowable Drives 框中选择要放置该分区的磁盘。
6. 将分区大小（以兆字节为单位）输入到 Size (MB) 框中。
7. 选择以下附加大小选项之一：

    - **固定大小** — 点击此处以在创建分区时使用仅输入到 Size 框中的兆字节数。
    - **填充至指定大小 (MB)** — 如果您希望使用所有剩余空间直至特定兆字节数，请点击此处并填入该数字。（如果您正在创建高达 2048MB 限制的 VFAT 分区，可能需要这样做，因为这是 Disk Druid 可以创建的上限。）
    - **填充至最大允许大小** — 如果您希望该分区扩展以填充磁盘的剩余部分，请点击此处。

8. 如果希望确保能够启动该分区，可选择 **强制作为主分区**；如果希望检查分区中的错误，可选择 **检查坏块**。
9. 如果一切正确，请选择 **确定**。（更改在后续几个步骤中询问开始安装软件包之前不会生效。）

要在 Disk Druid 中编辑分区，请从主 Disk Druid 窗口执行以下步骤：

1. 点击您想要编辑的分区。
2. 点击 **编辑** 按钮。会出现一个窗口，准备让您编辑分区定义。
3. 更改任何属性（如添加分区步骤中所述）。对于新安装，您可能需要为主要的 Linux 分区添加挂载点（/）。
4. 选择 **确定**。（更改在后续几个步骤中询问开始安装软件包时不会生效。）

> **说明：** 如果要创建 RAID 设备，首先需要创建至少两个 RAID 分区。然后点击 **创建 RAID** 按钮，将这两个分区变为 RAID 设备。有关 RAID 的更多信息，请参阅 *Red Hat Linux 定制指南*。该指南可在任何 Red Hat 镜像站点（如 ftp.redhat.com）获取，路径为：pub/redhat/redhat-7.3-en/doc/RH-DOCS/rhl-cg-en-7.3/index.html。

## 使用 fdisk 进行分区

在安装过程中，Red Hat 建议使用 Disk Druid 来更改分区，但也提供了使用 fdisk 的选项。fdisk 及相关工具执行与 Disk Druid 相同的工作，但可以在安装后运行。工具包括 `fdisk` 和 `sfdisk` 命令。

> **注意：** 请记住，任何分区命令都很容易擦除磁盘或使其无法访问。在使用任何工具更改分区之前，请备份关键数据！然后非常小心地进行所做的更改。随时备有一张紧急启动盘也是一个好主意。

`fdisk` 命令是许多不同操作系统上可用的命令（尽管在每个系统上其外观和行为不同）。在 Linux 中，`fdisk` 是一个基于菜单的命令。若要使用 `fdisk` 列出所有分区，请以 root 用户身份输入以下内容：

```bash
# fdisk -l

Disk /dev/sda: 255 heads, 63 sectors, 554 cylinders
Units = cylinders of 16065 * 512 bytes

Device Boot Start End Blocks Id System
/dev/sda1 * 1 83 666666+ b Win95 FAT32
/dev/sda2 84 89 48195+ 83 Linux
/dev/sda3 90 522 3478072+ 83 Linux
/dev/sda4 523 554 257040 5 Extended
```

