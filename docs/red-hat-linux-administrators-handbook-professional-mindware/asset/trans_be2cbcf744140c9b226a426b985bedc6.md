

## 540 附录

在这里，用户 *kabir* 迄今为止在磁盘分区 */dev/sda5*（受 usrquota 控制）上已使用了 0 个块（单位为 K），且限制（*软* 或 *硬*）尚未设置。同样，该用户尚未拥有任何文件（索引节点），且未设置任何限制（*软* 或 *硬*）。

正如你所见，你可以同时设置用户可消耗的空间量（以块为单位）的限制，并控制用户可拥有的文件数量。软限制指定用户在文件系统上可拥有的最大磁盘空间（块）或文件数（索引节点）。硬限制是用户可拥有的绝对磁�盘空间量（以块为单位）或文件数（索引节点）。

例如，假设你想允许用户 *kabir* 拥有 1MB（1,024K）的磁盘空间软限制和 4MB（4,096K）的硬限制。此外，假设你想允许该用户拥有 128 个文件/目录（索引节点）的软限制和 512 个文件/目录的硬限制。你可以使用 *edquota -u kabir* 设置配额限制，如下所示：

用户 kabir 的配额：

/dev/sda5: 已用块数: 0, 限制 (软 = 1024, 硬 = 4096)

已用索引节点数: 0, 限制 (软 = 128, 硬 = 512)

保存配置后，用户将无法超过硬限制。如果用户试图超过这两个（磁盘空间和索引节点计数）限制中的任何一个，将显示错误消息。例如，在下面的示例中，用户 *kabir* 尝试在 */home* 中创建一个新目录，但该配额的限制已被超过，因此显示错误消息：

[kabir@picaso /home]$ *mkdir eat_space*

mkdir: cannot make directory 'eat_space': Disc quota exceeded

如果你有许多用户需要分配配额，前面的方法可能会相当耗时。为了帮助你应对这种情况，*edquota* 程序包含一个 *-p 原型用户* 选项，允许你为其他用户复制原型用户的磁盘配额配置。例如，假设你想将刚为用户 *kabir* 创建的配额配置用于其他三个用户（*sheila*、*jennifer* 和 *mrfrog*）。你可以运行以下命令：

```
edquota -p kabir -u sheila jennifer mrfrog
```

现在，这三个用户都拥有与 kabir 相同的配额配置。将组置于磁盘配额控制之下非常相似。用于配置组配额要求的 edquota 语法如下：

```
edquota -g group name
```

要对用户或组配额强制执行软限制，请使用 edquota -t 命令配置宽限期。运行此命令时，你的编辑器将显示类似以下的内容：

```
Time units may be: days, hours, minutes, or seconds
Grace period before enforcing soft limits for users:
/dev/sda5: block grace period: 0 days, file grace period:
0 days
```

你可以以天、小时、分钟甚至秒为单位指定宽限期。例如，在下面的示例中，磁盘空间限制（以块为单位）的宽限期为 7 天，文件数量（索引节点）的宽限期仅为 5 小时：

```
Time units may be: days, hours, minutes, or seconds
Grace period before enforcing soft limits for users:
/dev/sda5: block grace period: 7 days, file grace period:
5 hours
```

## fdformat

**语法：** fdformat floppy-device

fdformat 程序对软盘设备进行低级格式化。例如，

```
fdformat /dev/fd0H1440
```

使用高密度 1.44MB 格式对第一个软盘（/dev/fd0）进行格式化。

## fdisk

fdisk 程序一次处理一个磁盘，尽管它提供了一个简单、不美观的用户界面，但它实际上比 Disk Druid 工具提供了更多的灵活性。

fdisk 具有简单的面向命令提示符的界面。它也是在安装完 Red Hat Linux 后可用的默认分区工具。使用以下语法从命令行运行 fdisk：

```
fdisk hard_disk_device
```

例如，

```
fdisk /dev/sda
```

告诉 fdisk 你想处理第一个 SCSI 磁盘的分区。输入此类命令后，fdisk 会显示其命令提示符 `Command (m for help):`，你可以输入 m 以获得如下帮助屏幕：

- a 切换可引导标志
- b 编辑 bsd 磁盘标签
- c 切换 dos 兼容性标志
- d 删除一个分区
- l 列出已知分区类型
- m 打印此菜单
- n 添加一个新分区
- o 创建一个新的空 DOS 分区表
- p 打印分区表
- q 不保存更改退出
- t 更改分区的系统 ID
- u 更改显示/输入单位
- v 验证分区表
- w 将表写入磁盘并退出
- x 额外功能（仅限专家）

要查看所选磁盘中的现有分区，请输入 **p**，这将以表格形式显示所有当前分区，如下所示：

```
Disk /dev/sda: 33 heads, 63 sectors, 1014 cylinders
Units = cylinders of 2079 * 512 bytes

Device Boot Start End Blocks Id System
/dev/sda1 1 505 524916 83 Linux native
/dev/sda2 506 1014 529105+ 5 Extended
/dev/sda5 506 886 396018 83 Linux native
/dev/sda6 887 1011 129906 82 Linux swap
```

如上所示，*/dev/sda* 磁盘已被划分为四个分区，其中第一个分区是 */dev/sda1*，起始于块 1，结束于块 505。每个块为 1,024 字节，即 1K，因此第一个分区由 524,916 个块组成，即 524,916K，约 512MB。

要逐个删除所有现有分区，请使用 **d** 命令并输入要删除的分区编号。删除一个或多个分区后，你可以按如下方式创建新分区。

首先，输入 **n** 以添加新分区：

```
Command (m for help): n
Command action
 e extended
 p primary partition (1-4)
```

如所示，你有两个选择：创建扩展分区或主分区。只有当你想创建四个以上分区时才需要扩展分区。因为在 Linux 下启动系统只需要 /、/usr、/home 和一个 swap 分区，所以你实际上不需要创建扩展分区。因此，在提示符下输入 **p** 创建主分区。下一个提示要求你选择分区编号：

```
Partition number (1-4): 1
```

为第一个分区输入 **1**，为第二个输入 **2**，依此类推。下一个提示要求你选择起始块编号。括号中显示的范围是可用于分区的总块数。如果这是第一个分区，请选择 1 作为起始块：

`First cylinder (1-1014): 1`

要创建一个 512MB 的分区，请以字节、千字节或兆字节为单位输入大小。因为以兆字节为单位的值易于处理，此示例对最后一个柱面使用 `+512MB`：

`Last cylinder or +size or +sizeM or +sizeK (1-1014): +512M`

要查看分区是否已按要求创建，请使用 `p` 命令查看分区信息：

```
Disk /dev/sda: 33 heads, 63 sectors, 1014 cylinders
Units = cylinders of 2079 * 512 bytes

Device Boot     Start      End Blocks Id System
/dev/sda1           1       505  524916 83 Linux native
```

如最后两行所示，第一个分区已按要求创建，默认分区类型为 Linux native；如果要更改此类型，请使用 `t` 命令切换分区的系统 ID 标志。例如，要将分区的系统 ID 标志切换为 Linux swap，请使用以下命令：

```
Command (m for help): t
Partition number (1-4): 1
Hex code (type L to list codes): 82
Changed system type of partition 1 to 82 (Linux swap)

Command (m for help): p
```

```
Disk /dev/sda: 33 heads, 63 sectors, 1014 cylinders
Units = cylinders of 2079 * 512 bytes

Device Boot     Start      End Blocks Id System
/dev/sda1           1       505  524916 82 Linux swap
```

首先，输入 `t` 命令以切换分区的系统 ID。然后，选择分区并输入 82 作为 swap 分区类型。`L` 命令可用于列出所有可用的分区类型。

请注意，如果你使用 fdisk 创建分区，必须使 Linux native 分区可引导。例如，要将 `/dev/sda1` 设为可引导分区，需要切换引导标志。输入以下内容：

Command (m for help): **a**

Partition number (1-6): **1**

使用 `p` 命令显示现有分区表：

| 设备 | 引导 | 起始 | 结束 | 块数 | ID | 系统 |
|:----- |:-----|:-----|:-----|:-----|:-----|:-----|
| `/dev/sda1` | * | 1 | 505 | 524916 | 83 | Linux native |
| `/dev/sda2` | | 506 | 1014 | 529105+ | 5 | Extended |
| `/dev/sda5` | | 506 | 886 | 396101 | 83 | Linux native |
| `/dev/sda6` | | 887 | 1011 | 129906 | 82 | Linux swap |

`/dev/sda1` 的引导列中有 *，表明该分区是可引导的。

## mkfs

**语法：** `mkfs [-t fstype] [-cv] device-or-mount-point [blocks]`

mkfs 命令允许你创建一个新的文件系统。例如，`mkfs -t ext2 /dev/hda3` 在第一块 IDE 硬盘的 `/dev/hda3` 分区上创建一个 ext2 类型的文件系统。`-c` 选项允许你指示 `mkfs` 在构建文件系统前检查坏块。`-v` 选项产生详细输出。

## mount

**语法：** `mount -a [-t fstype] [-o options] device directory`

