
时间单位可以是：天、小时、分钟或秒
在执行用户软限制之前宽限期：
/dev/sda5：块宽限期：0 天，文件宽限期：
0 天

您可以将宽限期指定为天、小时、分钟甚至秒。例如，在下面，磁盘空间限制（以块计）的宽限期为 7 天，而文件数量（inode）的宽限期仅为 5 小时：

```
Time units may be: days, hours, minutes, or seconds
Grace period before enforcing soft limits for users:
/dev/sda5: block grace period: 7 days, file grace period:
5 hours
```

## fdformat

语法：

```
fdformat floppy-device
```

fdformat 程序对软盘设备进行低级格式化。例如，

```
fdformat /dev/fd0H1440
```

使用高密度 1.44MB 格式格式化第一张软盘（/dev/fd0）。

## fdisk

fdisk 程序一次处理一个磁盘，尽管它提供了一个简单、不优雅的用户界面，但实际上比 Disk Druid 工具提供了更多的灵活性。

fdisk 具有简单的面向命令行提示符的界面。它也是在您已经安装 Red Hat Linux 后可用的默认分区工具。您可以使用以下语法从命令行运行 fdisk：

```
fdisk hard disk device
```

例如，

```
fdisk /dev/sda
```

告诉 fdisk 您想要操作第一块 SCSI 磁盘的分区。在输入此类命令后，fdisk 显示其命令提示符 Command (m for help):，您可以输入 m 来获取如下帮助屏幕：

### 命令操作

- a 切换可引导标志
- b 编辑 bsd 磁盘标签
- c 切换 dos 兼容性标志
- d 删除分区
- l 列出已知分区类型
- m 打印此菜单
- n 添加新分区
- o 创建新的空 DOS 分区表
- p 打印分区表
- q 不保存更改而退出
- t 更改分区的系统 id
- u 更改显示/输入单位
- v 验证分区表
- w 将表写入磁盘并退出
- x 额外功能（仅限专家）

要查看所选磁盘中的现有分区，请输入 p，这将以表格格式显示所有当前分区，如下所示：

磁盘 /dev/sda：33 个磁头，63 个扇区，1014 个柱面

单位 = 2079 * 512 字节的柱面

| 设备 | 启动 | 开始 | 结束 | 块 | Id | 系统 |
|---|---|---|---|---|---|---|
| /dev/sda1 |  | 1 | 505 | 524916 | 83 | Linux 原生 |
| /dev/sda2 |  | 506 | 1014 | 529105+ | 5 | 扩展 |

```
/dev/sda5  506   886  396018  83  Linux native
/dev/sda6  887  1011 129906  82  Linux swap
```

如图所示，/dev/sda 磁盘已被分为四个分区，其中第一个分区是 /dev/sda1，从块 1 开始到块 505 结束。每个块为 1,024 字节，或 1K，因此第一个分区由 524,916 个块组成，或 524,916K，或大约 512MB。

要逐一删除所有现有分区，请使用 d 命令并输入要删除的分区号。删除一个或多个分区后，您可以按如下方式创建新分区。

首先，输入 n 添加新分区：

```
Command (m for help): n
Command action
e   extended
p   primary partition (1-4)
```

如图所示，您有两个选择：创建扩展分区或主分区。您仅在想要创建超过四个分区时才需要扩展分区。因为在 Linux 下运行所需仅有 /、/usr、/home 和一个交换分区，所以您真的不需要创建扩展分区。因此，通过在提示符下输入 p 来创建主分区。下一个提示符要求您选择分区号：

```
Partition number (1-4): 1
```

输入 1 表示第一个分区，2 表示第二个，以此类推。下一个提示符要求您选择起始块号。括号中显示的范围是可用于分区的总块数。如果这是第一个分区，您可以选择 1 作为起始块：

```
First cylinder (1-1014): 1
```

要创建 512MB 分区，您可以以字节、千字节或兆字节输入大小。由于兆字节的值易于处理，此示例对最后一个柱面使用 +512MB：

```
Last cylinder or +size or +sizeM or +sizeK ([1]-1014):
+512M
```

要查看分区是否已按要求创建，请使用 p 命令查看分区信息：

```
Disk /dev/sda: 33 heads, 63 sectors, 1014 cylinders
Units = cylinders of 2079 * 512 bytes
```

| 设备 | 启动 | 开始 | 结束 | 块 | Id | 系统 |
|---|---|---|---|---|---|---|
| /dev/sda1 |  | 1 | 505 | 524916 | 83 | Linux 原生 |

如最后两行所示，第一个分区已按要求创建，默认分区类型为 Linux 原生；如果您想更改此设置，请使用 t 命令切换分区的系统 ID 标志。例如，要将分区的系统 ID 标志切换为 Linux swap，请使用以下命令：

```
Command (m for help): t
Partition number (1-4): 1
Hex code (type L to list codes): 82
Changed system type of partition 1 to 82 (Linux swap)
```

```
Command (m for help): p
```

```
Disk /dev/sda: 33 heads, 63 sectors, 1014 cylinders
Units = cylinders of 2079 * 512 bytes
```

| 设备 | 启动 | 开始 | 结束 | 块 | Id | 系统 |
|---|---|---|---|---|---|---|
| /dev/sda1 |  | 1 | 505 | 524916 | 82 | Linux swap |

首先，输入 t 命令以切换分区的系统 ID。然后选择分区并输入 82 作为交换分区类型。L 命令可用于列出所有可用的分区类型。

请注意，如果您使用 fdisk 创建分区，必须使 Linux 原生分区可引导。例如，要将 /dev/sda1 设为可引导分区，需要切换引导标志，输入以下内容：

命令 (m for help): a
分区号 (1-6): 1

使用 p 命令显示现有分区表：

```
Disk /dev/sda: 33 heads, 63 sectors, 1014 cylinders
Units = cylinders of 2079 * 512 bytes
```

| 设备 | 启动 | 开始 | 结束 | 块 | Id | 系统 |
|---|---|---|---|---|---|---|
| /dev/sda1 | * | 1 | 505 | 524916 | 83 | Linux 原生 |
| /dev/sda2 |  | 506 | 1014 | 529105+ | 5 | 扩展 |
| /dev/sda5 |  | 506 | 886 | 396018 | 83 | Linux 原生 |
| /dev/sda6 |  | 887 | 1011 | 129906 | 82 | Linux swap |

/dev/sda1 在 Boot 列中有 “*”，表示该分区可引导。

## mkfs

语法：

```
mkfs [-t fstype] [-cv] device-or-mount-point [blocks]
```

mkfs 命令允许您创建新的文件系统。例如，mkfs -t ext2 /dev/hda3 在第一块 IDE 硬盘的 /dev/hda3 分区上创建 ext2 类型文件系统。-c 选项可指示 mkfs 在构建文件系统前检查坏块。-v 选项产生详细输出。

## mount

语法：

```
mount -a [-t fstype] [-o options] device directory
```

mount 命令挂载文件系统。通常，常用文件系统的挂载选项存储在 /etc/fstab 中。例如，如果

```
/dev/hda6  /intranet  ext2  defaults  1  2
```

在 /etc/fstab 中找到，则可以按如下方式挂载存储在分区 /dev/hda6 中的文件系统：

```
mount /intranet
```

也可以按如下方式挂载同一文件系统：

```
mount -t ext2 /dev/hda6 /intranet
```

-t 选项用于指定文件系统类型。要挂载 /etc/fstab 中指定的所有文件系统，请使用 -a 选项。例如，以下命令挂载所有 ext2 文件系统：

```
mount -a -t ext2
```

-o 选项的常用参数是 ro（只读）和 rw（读写）。例如，以下命令将 /dev/hda6 以只读文件系统的方式挂载到 /secured：

```
mount -t ext2 -o ro /dev/hda6 /secured
```

## quota

要了解特定用户使用了多少磁盘空间，请按如下方式运行 quota 命令：

```
quota -u username
```

例如：

```
quota -u kabir
Disk quotas for user kabir (uid 500):
Filesystem blocks quota limit grace files quota limit grace
/dev/sda5  0  1024  4096  1  128  512
```
