
Metadata value on `/dev/da2`。

在这里看到 `gstripe(8)` 在 `/dev/da2` 上存储了信息。这台服务器在 `/dev/raid3/MyRaid3` 下提供 RAID-3 设备。我们可以看到设备的大小、块大小和其他有用信息。我们还有 `Consumers` 部分，它列出了 GEOM 设备中的所有底层磁盘。

使用 `gmirror` 的 `status` 命令查看你镜像中磁盘的状态：

```bash
# gmirror status
Name Status Components
mirror/MyMirror COMPLETE da7
```

你镜像中的所有磁盘都完全是最新的。由于只有一个磁盘，这在意料之中！使用 `insert` 命令向镜像集添加磁盘。你必须提供两个参数：镜像的名称和你想使用的驱动器：

```bash
# gmirror insert MyMirror /dev/da2
```

一旦你添加了磁盘，检查镜像状态：

```bash
# gmirror status
Name Status Components
mirror/MyMirror DEGRADED da7
da2 (11%)
```

镜像集尚未完全更新——需要几分钟时间从“完好的”磁盘将数据复制到新的镜像磁盘。取决于磁盘的大小和你的磁盘系统速度，这可能需要几分钟到几小时不等。你可以随时检查镜像状态以查看你的更新进展如何。

## 修复镜像

镜像的主要目的是冗余；当一个硬盘出现故障时，你希望能够恢复数据和/或维持运行。你的硬件决定了你继续操作和恢复的能力。如果你使用的系统带有热插拔 SCSI 或 SATA 驱动器，你可以动态修复镜像，但如果你在使用 ATA 系统，你可能需要关机来更换损坏的硬盘。

首先，使用 `gstripe(8)` 的 `forget` 命令从镜像集中移除损坏的驱动器。这指示 `gmirror(8)` 从镜像配置中移除所有当前不可用的驱动。`forget` 命令不会擦除整个镜像！只需使用你最初向配置添加驱动的同一个 `insert` 命令即可：

```bash
# gmirror forget MyMirror
# gmirror insert MyMirror /dev/da8
```

## 镜像启动磁盘

镜像启动磁盘并没有你想象的那么困难。虽然在安装过程中使用紧急 shell 甚至可以镜像你的驱动器，但我们将采取一种稍微简单的方法，在安装后完成。

首先，确保你的 `/boot/loader.conf` 加载了 `geom_mirror` 内核模块。如果没有它，FreeBSD 将无法找到启动磁盘；它将位于内核无法识别的磁盘设备上。重启一次是为了完全确保 `geom_mirror` 在启动时加载。

你的问题在于帮助 FreeBSD 找到启动驱动器。在默认的 FreeBSD 中，你的根分区位于磁盘设备如 `/dev/ada1` 上。当你将根驱动器放在镜像磁盘上时，你的路径变为 `/dev/mirror/MyBootDriveIa`。你的其他分区和切片位于类似的设备上。你必须在 `/etc/fstab` 中拥有正确的设备，以便 FreeBSD 正确启动。人们建议了各种技巧在单用户模式下更改 `/etc/fstab`，即使没有 `vi(1)` 可用。你可以使用 `sed(1)` 或编辑 `/usr` 到 `vi(1)`。为什么不在多用户模式下并在单独的文件进行更改呢？

将 `/etc/fstab` 复制到 `/etc/fstab-mirror`。编辑该文件为你的分区提供新的设备名称。假设你想为启动驱动器创建一个 `RootMirror0`。这里是一个小例子：`/etc/fstab`：

| /dev/ad0sia | | ufs | 1 | 1 |
| /dev/ad0sie | | /usr ufs | 2 | 2 |
| /dev/ad0sid | | /var ufs | 2 | 2 |

一旦你创建了镜像，FreeBSD 将期望一个这样的 `/etc/fstab`：

| /dev/mirror/RootMirror0sia | | ufs | 1 | 1 |
| /dev/mirror/RootMirror0sie | | /usr ufs | 2 | 2 |
| /dev/mirror/RootMirror0sid | | /var ufs | 2 | 2 |

现在知道必要的 `/etc/fstab` 看起来什么样了，在你手头方便编辑器时提前创建它。反复检查你的工作；确保你的文件系统正确比在引导加载程序或修复 CD 中折腾要容易得多！

现在重启进入单用户模式。在单用户模式下，FreeBSD 只以只读模式启动根分区。虽然对于挂载磁盘上的任何 GEOM 模块，设置 `sysctl kernel.geom.debugflags=16` 可以让你执行操作，但如果你想将根分区放在任何其他类型的 RAID 上，这将不起作用，但在镜像磁盘的情况下它效果良好。在单用户模式下，将你新的 `/etc/fstab` 就位，启用 GEOM 并创建你的根镜像：

```bash
# /etc/fstab /etc/fstab-nomror
# /etc/fstab-mirror /etc/fstab
# sysctl kernel.geom.debugflags=16
# geomir label -v RootMirror /dev/ado
```

重启后，FreeBSD 应该会在新的镜像 GEOM 磁盘上找到你的根分区。注意，你的镜像中只有一个磁盘，这使得它一个相当脆弱的镜像。然而，一旦你进入多用户模式，只需运行适当的 `insert` 命令添加备份磁盘：

```bash
# gmir insert RootMirror0 /dev/ad6
```

恭喜你！你有一个启动磁盘了。

## 多路镜像

虽然在安装过程中使用紧急 shell 甚至可以镜像你的驱动器，但我们将采取一种稍微简单的方法，在安装后完成。

首先，确保你的 `/boot/loader.conf` 加载了 `geom_mirror` 内核模块。如果没有它，FreeBSD 将无法找到启动磁盘；它将位于内核无法识别的磁盘设备上。重启一次是为了完全确保 `geom_mirror` 在启动时加载。

你的问题在于帮助 FreeBSD 找到启动驱动器。在默认的 FreeBSD 中，你的根分区位于磁盘设备如 `/dev/ada1` 上。当你将根驱动器放在镜像磁盘上时，你的路径变为 `/dev/mirror/MyBootDriveIa`。你的其他分区和切片位于类似的设备上。你必须在 `/etc/fstab` 中拥有正确的设备，以便 FreeBSD 正确启动。人们建议了各种技巧在单用户模式下更改 `/etc/fstab`，即使没有 `vi(1)` 可用。你可以使用 `sed(1)` 或编辑 `/usr` 到 `vi(1)`。为什么不在多用户模式下并在单独的文件进行更改呢？

将 `/etc/fstab` 复制到 `/etc/fstab-mirror`。编辑该文件为你的分区提供新的设备名称。假设你想为启动驱动器创建一个 `RootMirror0`。这里是一个小例子：`/etc/fstab`：

| /dev/ad0sia | | ufs | 1 | 1 |
| /dev/ad0sie | | /usr ufs | 2 | 2 |
| /dev/ad0sid | | /var ufs | 2 | 2 |

一旦你创建了镜像，FreeBSD 将期望一个这样的 `/etc/fstab`：

| /dev/mirror/RootMirror0sia | | ufs | 1 | 1 |
| /dev/mirror/RootMirror0sie | | /usr ufs | 2 | 2 |
| /dev/mirror/RootMirror0sid | | /var ufs | 2 | 2 |

现在知道必要的 `/etc/fstab` 看起来什么样了，在你手头方便编辑器时提前创建它。反复检查你的工作；确保你的文件系统正确比在引导加载程序或修复 CD 中折腾要容易得多！

现在重启进入单用户模式。在单用户模式下，FreeBSD 只以只读模式启动根分区。虽然对于挂载磁盘上的任何 GEOM 模块，设置 `sysctl kernel.geom.debugflags=16` 可以让你执行操作，但如果你想将根分区放在任何其他类型的 RAID 上，这将不起作用，但在镜像磁盘的情况下它效果良好。在单用户模式下，将你新的 `/etc/fstab` 就位，启用 GEOM 并创建你的根镜像：

```bash
# /etc/fstab /etc/fstab-nomror
# /etc/fstab-mirror /etc/fstab
# sysctl kernel.geom.debugflags=16
# geomir label -v RootMirror /dev/ado
```

重启后，FreeBSD 应该会在新的镜像 GEOM 磁盘上找到你的根分区。注意，你的镜像中只有一个磁盘，这使得它一个相当脆弱的镜像。然而，一旦你进入多用户模式，只需运行适当的 `insert` 命令添加备份磁盘：

```bash
# gmir insert RootMirror0 /dev/ad6
```

恭喜你！你有一个启动磁盘了。

## RAID-3

RAID-3 提供了某种程度的冗余和容错能力。

## 修复 RAID-3

RAID-3 提供了某种程度的冗余和容错能力。如果我们的一个硬盘出现故障，你将在状态报告中看到它：

| raid3 status Components |
| raid3/Myraid DEGRADED da2 |
| da0 |

这看起来不太妙。`/dev/da1` 发生了什么？我们会去解决它5，但现在重要的是恢复服务。我在 SCSI 阵列中有几个热备，所以让我们放入一个来恢复我们的冗余。

> 5 调查将显示有人从阵列中拔掉了驱动器以产生故障，这样就有东西可以写了。坦白说，我的老板不读我的书。

## RAID-3

RAID-3 提供了某种程度的冗余和容错能力。

## 每日检查

RAID-3 提供了某种程度的冗余和容错能力。

## RAID-3

RAID-3 提供了某种程度的冗余和容错能力。

## 销毁镜像磁盘

RAID-3 提供了某种程度的冗余和容错能力。

首先，让我们从 RAID-3 中移除所有对旧驱动器的引用。列出设备并获取每个驱动器的编号：

## raid3 list

```
1. Name: da2
Mediasize: 9186603008 (8.6G)
Number: 2
Type: PARITY

2. Name: dao
Mediasize: 9105018880 (8.5G)
```

我们正在寻找 RAID-3 中剩余每个磁盘的类型和编号。磁盘 `/dev/da2` 是阵列中的第 2 号磁盘；它是校验盘。磁盘 `/dev/dao0` 是第 0 号磁盘并包含数据。因此，我们丢失了一块数据盘，幸好有校验盘提供备份。如果我们丢失了校验盘，在更换磁盘之前，我们的 RAID-3 将大致按照条带磁盘的方式工作。

我们有三块磁盘中的 0 号和 2 号，所以故障的磁盘是 1 号。1. 先从 RAID-3 设备中移除 1 号驱动器，为替换设备留出空间。（记住，RAID-3 设备只能有奇数个成员，所以你不能直接添加驱动器。）然后添加一个新的 1 号驱动器 `/dev/da3`。

```
# raid3 remove -n 1 Myraid3
# raid3 insert -n 1 Myraid3 da3
raid3: warning: da3: only 9105018368 bytes from 9186602496 used.
```

嗯，这看起来很顺畅，尽管由于新磁盘比旧磁盘大，我们等待了一会儿磁盘空间。但它有效吗？检查状态。

## raid3 status

| Name Status |
| :--- |
| raid3/MyRaid3 DEGRADED da2 dao |
| da3 (1%) |

它看起来确实有效。等一会儿，看看阵列是否成功重建。

## 销毁 RAID-3

如果你不再想使用 RAID-3 设备，请卸载分区并在镜像上使用 `raid3 stop` 命令。然后你可以从涉及的磁盘中删除 raid3 的元数据：

```
# raid3 stop MyRaid3
# raid3 clear /dev/da3 /dev/da2 /dev/dao
```

然后你可以在其他地方使用这些磁盘——例如在 RAID-10 中。

## RAID-10

镜像磁盘的条带（或 RAID-10）可能是获取大量高性能存储的最快方法。磁盘被分组为镜像，然后数据在这些对之间进行条带化。没有校验盘；相反，镜像提供了冗余，而条带提供了性能。虽然 RAID-10 使用了大量磁盘，但它是高吞吐量性能的唯一选择。

从技术上讲，RAID-10 是一种嵌套 RAID。它是运行在 RAID 1 之上的 RAID 0。通过先启动镜像（RAID 1），然后在这些镜像上对数据进行条带化（RAID 0）。GEOM 允许你构建这样的层。RAID-10 通常用于高性能、高可用性环境。对于普通镜像就足够的客户 Web 来说，它太贵了，但奇怪的是，当涉及到自己的数据时，财务部门似乎愿意花这么多钱。对于镜像磁盘来说，如果可能，它们位于不同的控制器和不同机架的不同 SCSI 机柜中是非常重要的。

## RAID-10 设置

在开始之前写下你的磁盘安排，以免产生混乱。我们将使用四块驱动器：`/dev/da0`、`/dev/da2`、`/dev/da3` 和 `/dev/da4`。磁盘 `da0` 和 `da2` 配对 `mirror1`，`da3` 和 `da4` 组成我们的 `mirror2`。如果可能，`da0` 和 `da3` 不应该与 `da2` 和 `da4` 在同一个 SCSI 控制器上。

使用 `mirrorcommand (8)` 配置你的镜像：

```
# mirror label -v mirror0 /dev/dao /dev/da2
# mirror label -v mirror1 /dev/da3 /dev/da4
```

检查镜像状态以验证所有镜像都已按指定创建，并且每个镜像都是完整的。

> 我不仅粗鲁地把 `/dev/da1` 从 SCSI 机柜中拔了出来，而且我实在太懒了，不想离开椅子把它放回去。

现在创建一个包含两个镜像设备的 `gstripe(8)` 卷。我们将使用标准条带大小并将设备称为 `raid10`：

```
# gstripe label -s 131072 raid10 /dev/mirror/mirror0 /dev/mirror/mirror1
Metadata value stored on /dev/mirror/mirror0
warning: /dev/mirror/mirror1: only 910501785 bytes from 9186601984 bytes used.
Metadata value stored on /dev/mirror/mirror1.
```

你完成了。
不，真的。就是这些了。在 `/dev/stripe` 中有一个 `raid10` 设备。运行 `newfs -U /dev/stripe/raid10` 在设备上创建一个文件系统，挂载它，你就可以运行了！

## RAID-10 状态

要验证 RAID-10 阵列的状态，你必须检查镜像和条带设备的状态：

## gmirror status Components

| Name Status Components |
| :--- | :--- | :--- |
| mirror/mirror0 COMPLETE | dao |
| | | da2 |
| mirror/mirror1 COMPLETE | da3 |
| | | da4 |

## gstripe status

| Name Status Components |
| :--- | :--- | :--- |
| stripe/raid10 DEGRADED | mirror/mirror0 |
| | | mirror/mirror1 |

它看起来确实有效。等一会儿，看看阵列是否成功重建。

## 销毁 RAID-3

如果你不再想使用 RAID-3 设备，请卸载分区并在镜像上使用 `raid3 stop` 命令。然后你可以从涉及的磁盘中删除 raid3 的元数据：

```
# raid3 stop MyRaid3
# raid3 clear /dev/da3 /dev/da2 /dev/dao
```

将 FreeBSD 开箱即用的 `/usr` 分区移动到磁盘上的另一个分区，在单用户模式下为 `/usr` 配置日志功能，并恢复 `/usr`。其他分区的初始数据要少得多，因此更容易转换。一旦 `gjournal(8)` 退出实验性阶段，我预计其支持将集成到安装程序中。

## 配置 gjournal(8)

`gjournal(8)` 需要一个日志文件。这可以是一个独立的磁盘设备，也可以包含在带有日志文件系统的分区中。如果日志文件和文件系统位于同一个磁盘设备上，则没有性能理由将它们分离。然而，如果你能将日志放在单独的磁盘设备上，可能会获得更好的性能。（再次强调，两个使用同一个控制器的旧式 ATA 驱动器是不够行的！）对于我们的初始示例，我们假设日志文件与要进行日志处理的文件系统位于同一个磁盘分区上。

使用 `gjournal Load` 加载内核模块，或手动加载 `geom_journal.ko` 内核模块。你也可以在 `/boot/loader.conf` 中在启动时加载该模块。

现在将该分区标记为 `gjournal(8)` 用户。在这里我们将此磁盘上的单个分区 `/dev/da0sid` 转换为使用日志功能：

```
# gjournal label /dev/da0sid
gjournal: File system exists on /dev/da0sid and this operation would destroy it. Use -f if you really want to do it.
```
