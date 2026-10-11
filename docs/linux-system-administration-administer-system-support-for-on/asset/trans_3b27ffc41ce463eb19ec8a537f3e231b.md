
`-a` 选项会为所有文件系统启用配额。你可以指定特定的文件系统（例如，`quota /home`），这将为存储大多数用户文件的 /home 目录启用配额。你还可以为特定的用户或组在所有文件系统（或某个特定文件系统）上定义配额。对用户请使用 `-u` 选项，对组请使用 `-g` 选项。

要关闭配额，请使用命令 `quotaoff`。它接受与 `quotaon` 相同的选项。

如果你是系统用户，并输入 `quota`，你应该会看到以下消息：

```
$ quota
Disk quotas for user stripes (uid 1000): none
```

在将文件系统以读写方式挂载后再开启配额。为此，需要做几件事。第一件事是在 /etc/fstab 中将你的文件系统定义为支持配额。

为此，编辑 /etc/fstab 并在 defaults 选项后添加配额类型。可用的配额类型有 `usrquota` 和 `grpquota`。如果你希望同时启用两者，请确保在每个类型后面加上逗号。

```
/dev/sda2        /home     ext2    defaults,usrquota,grpquota        1 1
```

配额仅在 ext2fs 上可用，因此请确保不要尝试在其他类型的文件系统上启用它。

接下来，你需要在启动脚本（例如，/etc/rc.d/rc.M）中开启配额。务必在文件系统以读写方式挂载之后再开启配额，否则系统会报错。

![](img/8ad518fddafc7f5e73715a2604b61d50_106_0.png)

在分别用于关闭和重启系统的脚本 /etc/rc.d/rc.0 和 /etc/rc.d/rc.6 中，配额应该已经处于关闭状态。如果没有，请确保修正该情况。

始终在你想要实施磁盘配额的分区中创建 quota.user 和 quota.group 文件。只需触摸这些文件并将其权限更改为仅 root 可读写即可。对于用户文件，你可以这样做：

```
# touch /dev/sda2/quota.user
# chmod 600 /dev/sda2/quota.user
```

由于你对文件系统做了更改，需要重启系统。重启后，运行 `quotacheck -avug` 来检查文件系统，并确保配额正常工作。

要编辑特定用户的配额，首先确保你是 root，然后输入命令

```
# edquota username
```

这应该会自动打开你的默认编辑器以及你想要编辑的用户配额。你可以更改软限制（warn users that they are above quota），这会警告用户他们已超出配额，以及硬限制（hard limits），用户不能超过此限制。这些值可以修改以增加用户的磁盘空间。你还可以更改用户可以拥有的 inode 数量。

![](img/8ad518fddafc7f5e73715a2604b61d50_107_0.png)

> 不要仅用编辑器编辑用户的配额文件；请使用 **edquota** 命令。

你可以为软配额执行前的时间限制启用宽限期。换句话说，如果用户超过了他们的软配额，你可以允许他们有一段特定的时间，在此之前该软配额不会被强制执行。时间可以定义为任何基本增量（从秒到月）。

要定义宽限期，请使用 `-t` 选项。将 0 天替换为你认为合理的任何时间。

```
# edquota -t
```

现在你已经启用了配额，让我们看看 bob 的磁盘使用和配额情况。

```
# quota bob
Quotas for user bob:
  /dev/sda2: blocks in use: 879, limits (soft = 4000, hard = 5000)
  inodes in use: 894, limits (soft = 1000, hard = 2000)
```

如果 bob 想查看他的磁盘配额和使用情况，他只需要输入 *quota* 即可。

```
$ quota
Quotas for user bob:
  /dev/sda2: blocks in use: 879, limits (soft = 4000, hard = 5000)
  inodes in use: 894, limits (soft = 1000, hard = 2000)
```

对于配额报告，命令 `repquota -avug` 应该显示为每个磁盘、组和用户启用的所有配额。

# 交换空间

如果你有孩子，你知道他们打扫房间时会做什么吗？他们只是把混乱从地板转移到别处——衣柜、书桌抽屉、床底下。在某种意义上，交换空间（swap space）的工作原理也是如此。

如果你使用 `gcc`、X-Window 或其他任何资源密集型应用程序，除非使用 **swap**，否则你的系统会显著变慢。就像孩子玩完玩具后把它扔进衣柜并拿出另一个玩具来玩一样，Slackware Linux 将当前未使用的内容移动到硬盘存储中，从而为当前正在使用的其他程序释放内存。也就是说，Linux 正在收起一个玩具并拿出另一个。不过，如果你有大量的 RAM，你可能不需要交换空间，因为内存可以在自身内部移动，而无需使用磁盘空间。

## 创建交换空间

在添加交换空间之前，先决定你需要多少。如果你有 64 兆字节或更少的内存，将那个数量加倍并分配给交换空间。例如，我的 PC 有 32 兆字节的 RAM，所以我分配了 64 兆字节的交换空间。

要创建交换空间，进入 `fdisk` 并添加它。我将以我的电脑为例。

> **提示** 在初始配置交换空间时，请先配置其他分区，最后再配置交换空间。这样你的分区就按数字顺序排列（1、2、3 等），而不会跳过任何分区。

因此，我们运行 `fdisk`，在我的电脑上它将默认使用 `/dev/hda`。

```
# fdisk
Using /dev/hda as default device!
```

现在，让我们看看分区表。这显示了 `df` 命令所显示的所有内容（除了每个磁盘上已使用的空间量），并且它还显示交换空间。

```
Command (m for help): p

Disk /dev/hda: 128 heads, 63 sectors, 525 cylinders
Units = cylinders of 8064 * 512 bytes

Device   Boot    Begin     Start       End     Blocks    Id    System
/dev/hda1             1         1       127      512032+  83    Linux native
/dev/hda2           128       128       254      512064   83    Linux native
/dev/hda3           288       288       525      959616   83    Linux native
```

很好。我们仍然留有第 288 到 525 个柱面用于交换空间。这大约是 120 兆字节。要创建一个交换分区，我们需要以与创建文件系统时非常相似的方式创建一个新的分区。

```
Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
p
Partition number (1-4): 4
First cylinder (255-525): 255
Last cylinder or +size or +sizeM or +sizeK ([255]-287): 287
```

我们可以将剩余的磁盘空间用于交换空间，即使它超过了我为 32 兆字节 RAM 所需的 64 兆字节。所需数量因系统而异。某些应用不需要那么多交换空间，但如果你使用许多应用程序且内存较少，交换空间可以使性能略有提升。

我们将再次打印分区表，以确认新分区 /dev/hda4 已经创建。它是这样的：

```
Command (m for help): p

Disk /dev/hda: 128 heads, 63 sectors, 525 cylinders
Units = cylinders of 8064 * 512 bytes

Device   Boot    Begin     Start       End     Blocks    Id    System
/dev/hda1             1         1       127      512032+  83    Linux native
/dev/hda2           128       128       254      512064   83    Linux native
/dev/hda3           288       288       525      959616   83    Linux native
/dev/hda4           255       255       287      133056   83    Linux native
```

新分区已存在，但如果没有为除 Linux 以外的其他操作系统格式化，它默认是 Linux native。因此，我们必须进入分区表并更改它的文件类型。

```
Command (m for help): t
Partition number (1-4): 4
Hex code (type L to list codes): 82
Changed system type of partition 4 to 82 (Linux swap)
```

`fdisk` 中的 `t` 命令告诉 Linux 你想要重新定义新分区。代码（十六进制表示法）是 `82`。这将分区更改为 `swap`。

```
Command (m for help): p

Disk /dev/hda: 128 heads, 63 sectors, 525 cylinders
Units = cylinders of 8064 * 512 bytes

Device    Boot    Begin     Start     End     Blocks  Id  System
/dev/hda1        1         127      512032+   83  Linux native
/dev/hda2       128       128      254      512064   83  Linux native
/dev/hda3       288       288      525      959616   83  Linux native
/dev/hda4       288       288      525      959616   82  Linux swap
```

从这里你可以看到交换空间已被定义。保存分区表。

```
Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.

WARNING: If you have created or modified any DOS 6.x partitions, please see the fdisk manual page for additional information.
```

你可以忽略该警告，因为这里只是修改计算机的 Linux 部分。

接下来，你需要将你的分区添加到 `/etc/fstab` 文件中。在我的案例中，我添加了这一行：

```
/dev/hda4        swap      swap       defaults 1 1
```

然后你需要制作交换空间并使其生效。通过发出命令 `mkswap` 和 `swapon` 来完成。

```
# mkswap /dev/hda4
# swapon -a
```

这些命令激活了交换分区。如果你以后想要停用它，发出以下命令：

```
# swapoff -a
```

`-a` 选项影响 `/etc/fstab` 文件中的所有交换分区。

