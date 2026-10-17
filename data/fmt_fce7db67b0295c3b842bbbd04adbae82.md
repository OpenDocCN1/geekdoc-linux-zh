
- 3. 在红帽企业 Linux 6 中，旧的 SysInit 脚本被什么新的启动工具取代？

- 4. 运行级别 0 重启系统。对还是错？

- 5. 如果你的系统崩溃并无法启动，你必须重新安装整个操作系统。对还是错？

- 6. 你可以使用什么命令来管理系统服务？

[PAGE 99]

# 第 2 章：系统初始化

- 7. 哪个命令可以禁用系统启动时运行 SSH 服务？

- 8. 如何列出系统上的所有服务以判断它们是否在启动时启动？

- 9. `/etc/rc.d/rc2.d` 目录下的 `S12rsyslog` 代表什么？

- 10. 系统启动后，如何验证 SSH 服务的状态？

- 11. 使用什么命令和选项可以启用服务在启动时运行？

## 复习题答案

- 1. 阶段 1：在此阶段，主引导加载程序由 BIOS 从 MBR 读入内存。阶段 1.5：在此阶段，引导加载程序由阶段 1 引导加载程序读入内存（仅在需要时）。阶段 2：在此阶段，引导加载程序读取操作系统或内核。

- 2. 通过进入 GRUB 启动菜单，你可以选择向内核命令行选项添加内容的的选项​​。

- 3. `Upstart`。`Upstart` 工具现在被用于红帽企业 Linux 6 的启动过程​​。

- 4. 错。运行级别 0 停止系统。运行级别 6 重启系统。

- 5. 错。大多数启动问题都可以通过进入救援模式（`rescue mode`）并修复问题来解决。

- 6. `service` 命令用于用于启动、停止和管理系统服务。

- 7. `chkconfig sshd off`

- 8. `chkconfig --list`

- 9. 当系统进入运行级别 2 时，`rsyslog` 服务启动时的优先级为 12。数字较小（或数字相同但首字母靠前）的项目会在 `rsyslog` 服务之前启动。

- 10. `service sshd status`

- 11. 使用 `chkconfig` 命令在启动过程中启用或禁用服务。`on` 选项启用服务，`off` 禁用服务。

[PAGE 100]

## 实验 2

### 任务 1 – GRUB 设置

- **步骤 1.** 在 RHEL01 上，用任何文本编辑器打开 GRUB 配置文件。

- **步骤 2.** 在配置文件中添加一个新条目：

    - **a.** 新条目的标题（`title`）应该是 Red Hat Recovery。

    - **b.** 新条目不应为默认项。

    - **c.** 恢复条目应允许你进入恢复模式。

- **步骤 3.** 将启动选择的超时时间改为 10 秒。

当系统启动时 GRUB 菜单中显示两个条目且两者均正常工作时，任务完成。

### 任务 2 – 启动问题

- **步骤 1.** 确保你有红帽安装光盘。在 RHEL02 上，删除 `/etc/inittab` 文件并重启系统。

你会收到一个错误消息，显示系统找不到该文件。

- **步骤 2.** 从红帽安装光盘启动进入恢复模式。

- **步骤 3.** 将光盘中的文件替换到系统的正确位置。

> 提示：你可能需要使用命令 `mount /dev/cd-rom /mnt` 来访问光驱驱动器。

当系统再次启动时，任务完成。

### 任务 3 – 系统服务

执行以下系统服务相关的操作：

- **步骤 1.** 在所有系统中，执行以下系统服务相关的操作。

- **步骤 2.** 在所有系统中，执行以下系统服务相关的操作。

[PAGE 101]

- **步骤 3.** 在所有系统中，执行以下系统服务相关的操作。

- **步骤 4.** 在所有系统中，执行以下系统服务相关的操作。

[PAGE 102]

### 任务 4 – 丢失密码

- **步骤 1.** 在 RHEL02 上，更改密码为某个值。

- **步骤 2.** 假设你忘记了新生成的密码，恢复该密码。

当你可以以 root 身份登录时，任务完成。

[PAGE 103]

![](img/6f327e3a1ee7d861fc243df75aa6102_png)

## 磁盘与分区

### 基本分区

磁盘分区是在准备系统时必须采取的许多步骤之一。在每个系统中，物理磁盘驱动器被逻辑地划分为分区，允许你在上面存储数据（当然是在创建文件系统之后，将在下一章介绍）。还有特殊类型的分区，例如 RAID，可以提高性能、冗余或两者兼顾。LVM 像 RAID 一种高级分区形式，便于管理并使扩展存储容量变得简单。要记住的一个关键点是永远提前规划。

```
fdisk 磁盘分区工具
```

```
part 另一个磁盘分区工具
```

虽然 `fdisk` 更常用，但它正逐渐被更灵活的 `parted` 所取代。你也可以使用 `cat` 来检查 `/proc` 文件系统上各种文件的输出以获取信息。`/proc` 文件系统是由内核在系统启动时创建的，包含了有关系统的当前信息（你将在第 10 章“内核”中学习更多关于 `/proc` 文件系统的知识）。

要查看当前分区布局信息，请使用以下命令：

```bash
# cat /proc/partitions | grep hd
8 0 2097152 hda
8 1 512000 hda1
8 2 20458496 hda2
8 16 8388608 hdb
8 32 8388608 hdc
8 48 8388608 hdd
```

如果你使用的是 SCSI 磁盘而不是 IDE 磁盘，只需将命令改为：

```bash
# cat /proc/partitions | grep sd
```

从输出结果中可以看到，你得到了四个不同磁盘的列表：`hda`、`hdb`、`hdc` 和 `hdd`。

> 注意：前两个字母代表磁盘是 SCSI (`sd`) 还是 IDE (`hd`)；第三个字母代表它实际上是哪块磁盘。如果三个字母后面有一个数字，则是该分区的编号。对于实验，你可以看到它们都是 `hdd` 磁盘，意味着它们是 IDE 磁盘。还有四个物理设备：`a`、`b`、`c` 和 `d`。由于最后三块磁盘（`hdb`、`hdc` 和 `hdd`）尚未创建分区，因此没有数字。同时，你可以看到 `sda` 有三个分区。

在这种情况下，你想对最后三个磁盘进行分区，因此需要查看它们当前的分区以确认是否存在。你可以使用 `fdisk` 命令来完成操作。

语法：`fdisk [options] [device]`

选项：

- `-b` 指定磁盘的扇区大小

- `-h` 指定磁盘上的磁头数

- `-l` 列出当前分区表

# 第 3 章：磁盘与分区

要列出所有磁盘上的当前分区，请使用此命令：

```bash
# fdisk -l
```

Disk /dev/hda: 21.5 GB, 2147483648 bytes

255 heads, 63 sectors/track, 2610 cylinders

Units = cylinders of 16065 * 512 = 8225280 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disk identifier: 0x0021654

| Device | Boot | Start | End | Blocks | Id | System |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda1 | * | 64 | 512000 | 83 | Linux |
| /dev/hda2 | | 64 | 2048596 | 8e | Linux LVM |

Disk /dev/hdb: 8589 MB, 8589934592 bytes

255 heads, 63 sectors/track, 1044 cylinders

Units = cylinders of 16065 * 512 = 8225280 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disk identifier: 0x0004b72d

Disk /dev/hdb doesn't contain a valid partition

Disk /dev/hdc: 8589 MB, 8589934592 bytes

255 heads, 63 sectors/track, 1044 cylinders

Units = cylinders of 16065 * 512 = 8225280 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disk identifier: 0x00000000

Disk /dev/hdc doesn't contain a valid partition
