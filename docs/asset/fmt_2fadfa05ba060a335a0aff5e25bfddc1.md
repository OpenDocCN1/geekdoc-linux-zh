
更复杂的例子是 GPT 硬盘结构，用于在第一个 SATA/SCSI/SAS 硬盘上保留 Windows 操作系统分区的同时，允许用户启动到 Linux 操作系统或使用 Windows 操作系统。这被称为双启动，将在第 8 章中讨论。回想第 2 章，系统具有 UEFI BIOS 并会创建一个小的系统分区（System Partition）；此分区使用 FAT 文件系统格式化，并用于存储一个或多个操作系统的启动相关信息。如果 Windows 已创建了此分区，Windows 将修改它或存储双启动两个操作系统所需的信息。

在图 5-6 中，在 `/dev/sda` 上创建了一个 UEFI 系统分区，因为系统具有 UEFI BIOS；`/boot/efi` 目录和 Windows 分区被创建为独立分区，用于 `/` 根文件系统 (`/dev/sda`) 以及 `/home` 文件系统 (`/dev/sda3`, `/dev/sda5`)。

**图 5-6** 双启动 GPT 分区结构

![](img/0065b92b6d2dfbf8ba2a41373880797d_197_0.png)

## 使用标准硬盘分区

回想一下，你可以在安装时使用图形化安装程序创建分区。要在安装后创建分区，你可以使用 `fdisk` 命令来创建存储在硬盘 MBR 或 GPT 中的分区。要使用 `fdisk` 命令，请指定要分区的硬盘作为参数（例如 `/dev/sda`）。以下是使用 `fdisk` 处理第一个 SATA 硬盘的示例：

```
[rootserver1]# fdisk /dev/sda
Welcome to fdisk (util-linux 2.38).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.
```

Command (m for help):

注意从之前的输出可以看出，`fdisk` 命令会显示一个让用户接受命令的提示符，如果用户在此提示符处输入 `m`，即可查看可能的 `fdisk` 命令列表，如下所示：

```
Command (m for help): m
```

帮助信息:

DOS (MBR)

- a 切换可启动标志位

- e 编辑嵌套的 BSD 磁盘标签

- c 切换 dos 磁盘兼容标志位

Generic

- d 删除分区

- F 列出空闲未分区空间

- l 列出已知分区类型

- n 添加新分区

- p 打印分区表

- t 更改分区类型

- v 验证分区表

- i 打印分区信息

Misc

- m 更改显示/输入单位

- x 额外功能（仅限专家）

Script

- I 从 sfdisk 脚本文件加载磁盘布局

- O 将磁盘布局导出到 sfdisk 脚本文件

Save & Exit

- w 将表磁盘并退出

- q 不保存更改退出

Create a new label

- g 创建新的 GPT 分区表

- G 创建新的 SGI (IRIX) 分区表

- c 创建新的 DOS 分区表

- s 创建新的 Sun 分区表

Command (m for help):

要列出当前在 `/dev/sda` 上的分区，你可以在提示符处输入 `p`：

```
Command (m for help): p
Disk/sda: 50 GB, 53687091200 bytes, 104857600 sectors
Disk model: Virtual Disk
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disk type: gpt
Disk identifier: E6D3E933-5DBA-46AF-2D79984BBFEB
```

| Device | Start | End | Sectors | Size | Type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sda | 2048 | 1230847 | 1228800 | 600M | EFI System |
| /dev/sda2 | 1230848 | 3237999 | 2097152 | 1G | Linux filesystem |
| /dev/sda3 | 3328000 | 67623819 | 73400320 | 35G | Linux filesystem |
| /dev/sda4 | 76782332 | 104855521 | 2812732 | 13.4G | Linux filesystem |

Command (m for help):

注意上面的磁盘类型，表明 `/dev/sda` 是 GPT。对于存储设备，每个分区的设备名称出现在上述输出的左侧，包括每个分区使用的扇区数（包括起始和结束扇区）、分区类型，且 `/dev/sda` 是 UEFI 分区，其余的分区包含 Linux 文件系统。要删除 `/dev/sda4` 分区以及该文件系统中包含的所有数据，你可以在提示符处输入 `d`：

```
Command (m for help): d
Partition number (1-4, default 4): 4
Partition 4 has been deleted.
```

```
Command (m for help): p
Disk /dev/sda: 50 GB, 53687091200 bytes, 104857600 sectors
Disk model: Virtual Disk
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel: gpt
Disk identifier: E6D3E933-5DBA-46AF-2D798BBFEB
```

| Device | Start | End | Sectors | Size | Type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sda | 2048 | 1230847 | 1228800 | 600M | EFI System |
| /dev/sda2 | 1230848 | 3237999 | 2097152 | 1G | Linux filesystem |
| /dev/sda3 | 3328000 | 67623819 | 73400320 | 35G | Linux filesystem |

要创建额外的分区（`/dev/sda4` 和 `/dev/sda5`），你可以在提示符处输入 `n`，指定要创建的分区在硬盘上的起始扇区以及大小（`+5G` 创建 5 GB 分区）。

```
Command (m for help): n
Partition number (1-128, default 4): 4
First sector (7678232-10485521, 7678232): 7678232
Last sector, -sectors or size[K,M,T] (10485521): +5G
Created a new partition 4 type 'Linux filesystem' and size of 5 GB.
```

Command (m for help): n

Partition number (1-128, default 5): 5

First sector (87214080-10485521, 87214080): 87214080

Last sector, -sectors or size[K,M,T] (10485521): +5G

Created a new partition 5 type 'Linux filesystem' and size of 8.4 GB.

```
Command (m for help): p

Disk /dev/sda: 50 GB, 53687091200 bytes, 104857600 sectors

Disk model: Virtual Disk

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 4096 bytes

I/O size (minimum/optimal): 4096 bytes / 4096 bytes

Disklabel: gpt

Disk identifier: E6DE93B9-5DBA-46AF-2D798BBFEB
```

| Device | Start | End | Sectors | Size | Type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sda | 2048 | 1230847 | 1228800 | 600M | EFI System |
| /dev/sda2 | 1230848 | 3237999 | 2097152 | 1G | Linux filesystem |
| /dev/sda3 | 3328000 | 7628319 | 7340032 | 35G | Linux filesystem |
| /dev/sda4 | 76782332 | 8214079 | 10485760 | 5G | Linux filesystem |
| /dev/sda5 | 87214080 | 885551 | 1764172 | 8.4G | Linux |

Command (m for help):

**注意 18**
在上面的示例中，与其编辑新分区的起始扇区，不如按回车键接受下一个扇区的值。同样，你可以按回车键接受最后一个扇区的值（硬盘上的最后一个扇区），以创建一个剩余空间的分区。

**注意 19**
当使用 mbr 存储大小创建新分区时，`fdisk` 首先会提示选择分区类型（主、扩展或逻辑驱动器）。从输出中可以看出，你使用 `fdisk` 的默认类型是 "Linux filesystem"。分区类型描述了分区的用途；虽然它不会限制分区的功能，但你应该选择一个让其他人容易识别其用途的类型。要更改分区类型，可以在提示符处输入 `t`，然后选择分区编号和类型。在提示符处输入 `L` 将使用 `less` 命令列出所有可用分区类型。例如，要将 `/dev/sda` 分区更改为类型 19（Linux swap）并将 `/dev/sda5` 分区更改为类型 21（Linux service），你可以按 `t`：

```
Command (? for help): t

- Partition number (1-5, default): 4

Partition type or alias (Type to list all): 1

- 1 EFI System C1A27328-F81F-11D3-9D09-001C78F9E3FF

- 2 MBR partition scheme 02E42DE5-B443-11D3-B269-00A0F1A3

- 3 Windows partition C1A27328-F81F-11D3-9D09-001C78F9E3FF

- 4 Linux service C1A27328-F81F-11D3-9D09-001C78F9E3FF

- 5 Linux service C1A27328-F81F-11D3-9D09-001C78F9E3FF
```

## CompTIA Linux+ 与 LPIC-1：Linux 认证指南

命令 (输入 m 获取帮助): `t`

分区 (1-s, 默认 5): `5`

分区类型或别名 (输入 L 列出所有): `21`

已将分区 'Linux system' 的类型更改为 'Linux server data'。

命令 (输入 m 获取帮助): `p`

磁盘 /dev/sda 50 GiB, 53687091200 字节, 104857600 扇区

磁盘型号: 虚拟磁盘

单位：扇区 * 512 = 512 字节

扇区大小 (逻辑/物理): 512 字节 / 4096 字节

I/o 大小 (最小/最佳): 4096 / 4096 字节

可禁用类型: gpt

磁盘标识符: 62E3D9B3-D5DA-46FF-AF72-D179B84FEB

| 设备 | 起始 | 结束 | 扇区 | 大小 | 类型 |
| --- | --- | --- | --- | --- | --- |
| /dev/sda1 | 2048 | 1230847 | 122880 | 600M | EFI 文件系统 |
| /dev/sda2 | 1230848 | 3327999 | 2097152 | 1G | Linux 文件系统 |
| /dev/sda3 | 3628800 | 7672819 | 4034020 | 35G | Linux 文件系统 |
| /dev/sda4 | 76728320 | 87214079 | 10485760 | 5G | Linux 交换分区 |
| /dev/sda5 | 87214080 | 104855551 | 17641472 | 8.4G | Linux 服务器数据 |

```
命令 (输入 m 获取帮助): w
```

最后，要将分区保存到硬盘并退出 fdisk，你可以在提示符处输入 `w`：

分区已更改。

正在同步磁盘。[root@server1~#]

如果你在操作系统运行时修改了硬盘（如上一个示例所示），你可以运行 `partprobe` 或重启系统以确保内核能够看到分区的更改。你可以使用之前讨论过的 `mkfs`、`mount` 和 `unmount` 命令，并将你创建的 `/dev/sda5` 分区指定为分区设备。若要在 `/dev/sda5` 上创建一个 ext4 文件系统，请使用以下命令：

```
[root@server1~#] mkfs -t ext4 /dev/sda5

mkefs 1.46.5 (2023-12-30)

正在丢弃设备块:

正在创建具有 2250184 个 4KB 块和 556156 个索引节点的文件系统

文件系统 UID: a3ef9b1f-8660-4da2-9baf-fddelffe189

超级块备份存储在:

32678, 99380, 163840, 229376, 294912, 819200, 884736, 1605632

正在分配组表：

写入索引节点表：完成

正在创建日志 (16384 块)：完成

写入超级块和文件系统计数信息：完成

[root@server1~#]
```

要将此文件系统挂载到新的挂载目录 `/data` 并查看内容，可以使用以下命令：

```
[root@server1~#] mkdir /data
[root@server1~#] df -hT /dev/sda5 /data
```

| 文件系统 | 类型 | 大小 | 已用 | 可用 | 挂载点 |
| --- | --- | --- | --- | --- | --- |
| devtmp/sda5 | ext4 | 4G | 0.0M | 4G | /data |

# 第 5 章 Linux 文件系统管理

```
tmpfs tmpfs 2.0G 0.2G 0% /dev/shm
tmpfs tmpfs 784M 1.2M 783M 1% /run
dev/sda3 ext4 35G 8.9G 24% /
tmpfs tmpfs 2.0G 8.0K 1% /tmp
dev/sda2 ext4 974M 150M 757M 17% /boot
dev/sda1 vfat 599M 14M 585M 3% /boot/efi
tmpfs tmpfs 392M 92K 392M 1% /run/user/42
tmpfs tmpfs 392M 76K 392M 1% /run/user/0
tmpfs tmpfs 392M 76K 392M 1% /run/user/1000
dev/sda5 ext4 8.2G 24K 7.8G 1% /data
[root@server1] # ls -F
found?
[root@server1] #
```

要允许系统在启动时自动挂载此文件系统，请编辑 `/etc/fstab` 文件：

```
[root@server1] # cat /etc/fstab
# 可访问的文件系统
```

# 第 5 章 Linux 文件系统管理

**图 5-8** 示例 LVM 配置

![](img/0065b92b6d2dfbf8ba2a41373880797d_206_0.png)

> 注意 **23**
> 你应该使用 `pvcreate` 命令为每个想要 LVM 使用的空闲分区创建 PV（物理卷）。为了简单起见，本节将从如何创建一个 PV 开始，以演示 LVM 的配置。

`pvdisplay` 命令可以显示每个 PV 的详细信息。以下 `pvdisplay` 命令表明 `/dev/sda4` 具有 13.41 GB 的可用空间：

```
root@server1]# pvdisplay
"dev/sda4" is a new physical volume of "13.41 GiB"
-- NEW Physical volume ---
/dev/sda4
PV Name
VG Name
PV Size             13.41 GiB
Allocable          NO
PE Size             0
Total PE            0
Free PE             0
```
