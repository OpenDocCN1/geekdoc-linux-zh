
**图 1.** GRUB，作为红帽 Linux 的默认引导加载程序，允许你在 Linux 和 Microsoft Windows 之间进行双启动。

以下步骤假设你尚未用完所有的四个主分区，并且硬盘上没有扩展分区。它还假设你将分割第一个主分区，该分区在 Microsoft Windows 中被分配给 `C` 盘。

1. 从 DOS 提示符运行 `FIPS.EXE` 命令。如果你需要终止实用程序，可以随时按 `Ctrl-C`。
2. 在 Microsoft Windows 中准备你的硬盘。使用 Windows 操作系统上的微软磁盘碎片整理程序。这可以最大化分区末尾的可用空间。
3. 准备一个 DOS 启动盘。为此，它通常与 Windows 98 关联。你可以从 `www.bootdisk.com` 获取此启动盘的副本。将 `FIPS.EXE` 和 `RESTORRB.EXE` 复制到该盘。在 Red Hat Linux 中，这些文件位于第一张安装光碟的 `/dos` 目录中。

你可能还想打印 `FIPS.DOC` 文件，它与 `FIPS.EXE` 位于同一目录下。其中包含了使用 `RESTORRB.EXE` 的说明。

## 第 1 章：基础 Linux 安装

4. 在软驱中插入 DOS 启动盘并重启电脑。

5. 当你的电脑启动到 `A:` 盘时，运行 `FIPS.EXE` 命令。在提示时按任意键。如果 `FIPS.EXE` 检测到你的电脑上有两个硬盘，你将被要求在驱动器之间进行选择。（你无法从第三块物理硬盘启动 Linux）

6. 你应该看到一个列出硬盘上分区的表格，类似于图 2。如你所见，在这个特定的驱动上只配置了一个主分区。如果有多个主分区，将提示你进行选择。如果四个槽位都已配置，`FIPS.EXE` 将终止，因为它会分割分区。

| 分区 (Part.) | 可启动 | 道:扇:头 | 道:扇 | 扇区 (Sectors) | 数量 | MB |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 是 | 1 | 0 | 01: Bch1 | 259 | 63: 4176837 ( 2839) |
| 2 | | 1 | 0 | 01: 08h | 0 | 01: 0 |
| 3 | 否 | 1 | 0 | 01: 08h | 0 | 01: 0 |
| 4 | 否 | 1 | 0 | 01: 08h | 0 | 01: 0 |

检查根扇区 ... OK
按任意键

> 图 2 `FIPS.EXE` 检查硬盘的主分区。

7. `FIPS.EXE` 扫描所选分区。在列出基本信息后，它提议对你的硬盘的根扇区和启动扇区制作备份。接受建议吧！让 `FIPS.EXE` 将备份存储在你的启动软盘上。记住文件名 `a:\boot.000`。这是错误的最佳保障。

8. 根据你可用的空间，现在可以分割所选分区。使用方向键在旧分区之间分配空间。你将看到类似的屏幕：

| 旧分区 | 道 (Cylinder) | 新分区 |
| :--- | :--- | :--- |
| 4150.6 MB | 290 | 6120.3 MB |

9. 如果你的分区包含 Windows 媒体，记住为交换文件和碎片留出足够的空间。如果你对结果满意，按 `Enter`。

10. `FIPS.EXE` 测试新分区。如果一切正常，你将看到一个类似于图 2 的修订分区表。你可以使用 `c` 或 `r` 命令继续或重新编辑分区。

11. 写入你的新分区磁盘方案。如果一切顺利，将在 Linux 安装过程中识别此分区。或者，你可以使用 Linux 版本的 `fdisk` 删除并重新配置与新分区的空间。

### 基础文件系统术语

查看以下术语。它们可以帮助你理解分区、RAID 和 LVM。

`卷 (Volume)`：磁盘空间区域，例如 Microsoft 驱动器 `C:` 或 Linux 目录 `/boot`。卷通常等于分区，除非你配置了两个或多个分区在 RAID 0 阵列中工作。

`挂载点 (Mount point)`：用于挂载分区、RAID 设备或逻辑卷的目录，例如 `/boot`。

`RAID`：磁盘冗余阵列。对于硬件 RAID，有两个或多个物理硬盘共同工作。硬件 RAID 需要第三方软件。

`软件 RAID (Software RAID)`：使用分区而非硬盘的 RAID。为了生效，软件 RAID 阵列中的每个分区应位于不同的硬盘上。

`RAID 设备 (RAID device)`：可以挂载分区的阵列。RAID 阵列有几种配置方式：RAID 0、RAID 1 和 RAID 5。在 Red Hat Linux 中，RAID 设备命名为 `/dev/md0`、`/dev/md1` 等。

`RAID 0`：快，但不安全数据。RAID 0 允许你结合两个或更多分区和硬盘的空间。被称为“条带”（stripping）。

`RAID 1`：慢，但为了数据安全。RAID 1 复制两个独立分区或硬盘上的数据。被称为“镜像”（mirroring）。

`RAID 5`：数据安全性极高；速度中等。RAID 5 包含额外的校验位，可以帮助从任何损坏的分区或硬盘恢复数据。

`物理卷 (Physical Volume, PV)`：为卷管理 (LVM) 分配的主分区或逻辑分区。

`物理区 (Physical Extent, PE)`：每个 LE 对应一个 PE。物理区然后组织成卷。

`逻辑卷 (Logical Volume, LV)`：一组的 LV，可以挂载目录——就像分区一样。

`卷组 (Volume Group, VG)`：系统的所有 LV ![](img/6ee4859e736a0839007ea9afb576c195_38_0.png) 用于卷组。

> RAID 0、RAID 1 和 RAID 5 是红帽支持的版本。

### 使用 fdisk 添加和删除分区

Linux 中添加和删除分区的标准工具是 `fdisk`。该程序的微软版本 `FDISK.EXE` 可创建多个分区。由于 Linux 包含了此工具，因此不再需要使用 `fdisk` 准备分区。该磁盘实用程序可以管理 100 多种不同类型的分区，包括各种 Microsoft、Novell 以及 Linux 类型。在向你展示如何创建新区的示例之前，请查看表 9 列出的五种基础分区类型。与每个类型关联的数字是 `fdisk` 中的标记。

#### 表 9. Linux 分区类型。

| 类型 | 十进制代码 | 用途 |
| :--- | :--- | :--- |
| Linux | 83 | 适用于标准的 Linux 数据格式，包括 `ext2`, `ext3`, `ReiserFS` 和 `xfs`。 |
| Linux Extended (扩展) | 85 | 与包含逻辑分区的扩展分区相关。 |
| Linux LVM | 8e | 用于将空间分配给 LVM 卷的分区。 |
| Linux RAID | fd | 分配给软件 RAID 阵列中的分区。 |
| Linux swap (交换) | 82 | 用于 Linux 交换的分区。 |

现在让我们在新硬盘上配置分区。例如，如果你安装了一个新的 SCSI 驱动器并运行 `fdisk -l` 命令，你应该看到驱动器上配置的分区表，类似于图 3。

```
[root@NoPaws root]# fdisk -l

Disk /dev/sda: 4293 MB, 4294967296 bytes

255 heads, 63 sectors/track, 522 cylinders

Units = cylinders of 16065 * 512 = 8225280

    Device Start Blocks Id System

/dev/sda * 13 104091 83 Linux

/dev/sdb 14 474 3075282 81 Linux

/dev/sdc 475 522 385560 82 Linux swap

Disk /dev/sdd: 2146 MB, 2147483648 bytes

128 heads, 32 sectors/track, 1023 cylinders

Units = cylinders of 4096 * 512 = 2097152

Disk /dev/sdd doesn't contain a valid partition table

[root@NoPaws root]#
```

#### 图 3. 检查分区。

> 根据你用户的默认设置，可能会遇到“找不到命令”错误。在这种情况下，使用命令的完整路径，例如 `/sbin/fdisk /dev/sdb`。例如，如果我想找到 `fdisk` 的完整路径，运行命令 `locate fdisk | more`。

![](img/6ee4859e736a0839007ea9afb576c195_39_0.png)

你也可以从图 3 看到在安装新硬盘后发生了什么。注意这个名称；它是 `/dev/sdb`。根据本章早些的讨论，你应该意识到它是电脑上的第二块 SCSI 硬盘器。现在使用以下命令开始配置该硬盘：

```
fdisk /dev/sdb
```
