
# FreeBSD 精通之路：高级 ZFS (IT Mastery Book 9)

![](img/ec2cadedd00f39b2e62dde91407e8263_0_0.png)

* 关于作者

![](img/ec2cadedd00f39b2e62dde91407e8263_2_0.png)

我们非常感谢对本书稿提供反馈的人士：Will Andrews, Marie Helene Kvello-Aune, Josh Paetzel, Benedict Reuschling, Alan Somers, Matthew Seaman 和 Wim Wauters。

作者感谢 FreeBSD 项目和 FreeBSD 基金提供 NetPerf 集群中的 NVMe 设备，并感谢 Sentex Data Communications 托管了该集群。Lucas 感谢 Jude 以某种方式说服这些人授予 Jude 访问集群的权限，因为他们绝不会给 Lucas 的。此外，这意味着 Lucas 就不需要写书中的那部分了。

# 第 0 章：引言

Z 文件系统（或 ZFS）是一个复杂的怪兽，但它也是系统管理员蝙蝠侠工具用带中最强大的工具。本书试图揭秘让 ZFS 如此强大的某些魔力，并在你与存储巨龙作斗时，为你提供坚实且可操作的情报。

ZFS 包含了业内一些顶尖人才超过 100 个“工程年”的心血。尽管它有竞争对手，例如 B 树文件系统 (`BTRFS`)，但那些竞争对手还有很多路要走。而 ZFS 每天都在遥遥领先。

本书将带你进入管理 ZFS 的一些复杂且深奥的部分。如果你想知道为什么 1GB 的数据会填满你的 2GB 硬盘，如果你想自动更新你的灾难恢复设施，或者你只想笔记本电脑上运行启动环境，那么 *FreeBSD Mastery: Advanced ZFS* 正为你准备的。

书中几乎所有内容都适用于 OpenZFS。我们使用 FreeBSD 作为参考平台，但使用 OpenZFS 的机制在不同平台之间并没有太大。

## 前提条件

书名中包含了“进阶”一词。我们预计你在使用它之前已经掌握一些知识。简单的答案是你应该阅读并吸收早期的两本关于 FreeBSD 的著作：《存储精要》(Storage Essentials) 和《ZFS》。但你可能已经知道那些书中的内容了，所以这里是关于你需要准备知识的细节。

你需要熟悉 FreeBSD 的存储管理层 `GEOM`。在非 FreeBSD 平台上，你可以使用磁盘和分区设备运行 ZFS。请务必在磁盘或分区设备上使用 ZFS，而不是在 RAID 或软件设备上。

我们假设你熟悉 ZFS 存储池（`pools`）和数据集（`datasets`）。你知道如何向池中添加 `VDEV`，并理解为什么不能向 `RAID-Z` 中添加单块磁盘。你可以拍摄快照并创建克隆。

如果你想使用 FreeBSD 的加密 ZFS 支持，你必须理解 FreeBSD 的 `GELI` 加密。（如果你依靠加密来保护人类生命，可以使用 `GBDE`，但内置的 `GELI` 支持对我们大多数人来说足够了。）

## ZFS 最佳实践

虽然你可以从公开文档中获取所需的 ZFS 知识，但它并不会提供我们在之前的书中讨论过的 ZFS 最佳实践。正如许多其他事情一样，最佳实践的妙处在于有很多供选择。我们在这里讨论一些最佳实践。也许这些比你的更好，你会乐意采纳它们。它们至少让你知道我们是如何处理存储问题的。

## 空间管理

在写时复制（`copy-on-write`）文件系统中，删除文件会占用空间。习惯传统文件系统的系统管理员在开始使用 ZFS 时可能会发现这一点，直到第一次耗尽空间时感到震惊。当池接近容量时，ZFS 需要更多空间来存储额外数据。性能会下降。为了防止空间意外耗尽，理想情况下，你应该为池创建一个预留（`reservation`）。你可以在添加或删除数据时随时降低预留。你最希望的情况是耗尽空间。在可用磁盘剩余最后百分比时，创建一个预留 200GB 的数据集。

```
zfs create -o reservation=200G mypool
```

每当你探索 ZFS 空间问题时，记住 `zfs get space` 命令。你会看到所有与空间相关的属性。

```
zfs get space data/usr
NAME          SOURCE
data/usr      available     5.0T
data/usr      used          367M
```

虽然 `zfs get` 不会为你释放空间，但它是发现空间去向的最快路径。

### 选择 VDEV 类型

正如《FreeBSD Mastery: ZFS》中所讨论的，创建池时选择正确的 VDEV 类型是你所做出的最重要的决定。它影响池的性能以及扩展的可能性。Paris、Amer 和 Schwarz 的一项研究（http://arxiv.org/pdf/papers/1501/1501.pdf）发现，要构建一个无需人工干预即可生存四年的磁盘阵列，需要三冗余（triple parity）。双冗余即使有无限数量的备用盘也无法在四年内保持 99.999%（五九）的可靠性。将此考虑与你拥有的硬件以及你的存储需求相结合。

### 标签的重要性

通过对驱动器标记，你可以避免未来的很多麻烦。在将它们添加到 ZFS 池之前，标记你的磁盘和分区——我们将在本节中讨论这种方法。

以 Jude 的一个不幸的朋友为例，他使用原始设备名称创建池。当一个设备故障时，他在更换磁盘之前重启了。他的池看起来与预期的的不一样。

```
zpool status
pool: data
state: DEGRADED
status: 一个或多个设备正在恢复。池将继续运行，可能处于降级状态。
action: 等待恢复完成。
scan: resilver in progress since Sat 11 17:49:38 2015
62.0M scanned out 1.57T at 5.16M/s, 87h40m to go
9.81M resilvered, 0.00% denom
```

```
config:
  STATE    READ WRITE CKSUM
  data     DEGRADED     0      0      0
    mirror-0 DEGRADED     0      0      0
    spare-0  UNAVAIL     0      0      0
    5694975301095445325 FAULTED      0      0      0 was /dev/da1
```

| NAME | STATE | VALUE | SOURCE |

| :--- | :--- | :--- | :--- |

| data | DEGRADED | | |

| mirror-0 | DEGRADED | 856 (resivering) | da7 |

| da14 | ONLINE | | |

| mirror-1 | ONLINE | | |

| da1 | ONLINE | | |

| da13 | ONLINE | | |

最初，池有两个镜像：`da1` 和 `da15` 的 `mirror-0`，以及 `da2` 和 `da14` 的 `mirror-1`。磁盘 `da1` 故障了。

FreeBSD 在启动时动态分配设备节点。由于 `da1` 缺失，FreeBSD 重命名了剩余设备以向下移动一位。磁盘 `da15` 变成了 `da14`，`da14` 变成了 `da13`，最糟糕的是，`da2` 变成了 `da1`。

因此，`mirror-1` 包含了 `da1`——但这并不是故障磁盘所在的 `da1`。一旦 Jude 的 `Mirror-0` 使用了它的备用盘（`da7`）来代替原来的 `da1`。然而，一旦那个不幸的朋友为故障的 `da1` 放回了磁盘，`da7` 就变成了 `da8`。

ZFS 不使用 FreeBSD 磁盘名称来查找每个 VDEV 的成员，而是依赖于自带带有全局唯一标识符（`GUID`）的磁盘上标签。无论操作系统将设备节点放在哪里，ZFS 都能识别该磁盘。操作系统也不在乎——它为你找到了磁盘并挂载了文件系统；你还想要什么？

### 磁盘标记

FreeBSD 提供了几种标记磁盘或分区的方法。其中一些是自动的，另一些由用户管理。每种方法都有优缺点。一个设备可以拥有多个标记。

一旦访问了某个标记，指向同一设备的其他标记就会失效并变得无法访问。这防止了通过多个名称访问同一个设备。

所有自动生成的标记默认都是激活的。如果您想使用手动标记，最好禁用手动方法。

#### GPT 标记（手动）

如果磁盘使用 GUID 分区表 (`GPT`)进行分区，每个分区都可以包含一个您自定义的文本标记。这是作者首选的磁盘标记方法。

使用 `gpart(8)` 创建并标记新分区。

```
#### gpart add -t freebsd-zfs -zfs-mirror-1 da2
```

在这里，我们更改现有第 2 分区的标记。

```
#### gpart modify -i 2 -f01-serialnumber da2
```

手动标记有助于通过物理位置或序列号等特征来识别磁盘。

如果您使用 GPT 标记，我们建议禁用 GPTID 和磁盘 ID 标记。

#### GPTID 标记（自动）



## GPT 分区方案

在 GPT 分区方案中，每个分区都有一个唯一的 GUID。GPT 标记系统使用 GUID 来识别分区。问题是 GUID 对人类来说意义不大。通过观察其中几个，你会发现很难看出它们之间的差异。

```
ada0p1: /dev/gptid/b305e4ff-b889-11e5-002590db872e
ada1p1: /dev/gptid/b329ff70-b889-11e5-002590db872e
ada1p2: /dev/gptid/b33db4ac-b889-11e5-002590db872e
```

如果第一段的最后几个字符实际上不同，很容易产生混淆。

如果 ZFS 在其他标记下看到某个池之前，先在 GPT 标记下看到了该池，它将使用 GPTID 标记。这会隐藏您精心设计的标记。

通过在 `/boot/loader.conf` 中添加以下内容在启动时禁用 GPTID 标记。

```
kern.geom.label.gptid.enable=0
```

FreeBSD 默认启用 GPT ID。

## 磁盘标识标记（自动）

虽然 GPT 和 GPTID 标记识别分区，但磁盘标识（或 diskid）标记识别的是整个磁盘。设备名称基于磁盘的序列号，这非常方便。遗憾的是，序列号中的任何特殊字符（特别是空格）都会编码。这创建了非常难看的设备名称。此外，由于标记的是磁盘而非分区，设备名称的分区部分（p3）会被附加在后面，很难从设备中识别出来。

```
/dev/diskid/DISK-07013121E6B2BFA14
/dev/diskid/DISK-%20%20%20%20%20WD-WCC131365642
/dev/diskid/DISK-%20%20%20%20%20%20%20%20%20Z300HTCE
```

可以禁用这些自动生成的标记，以防止 ZFS 使用它们代替 GPT 标记。在 `/boot/loader.conf` 中添加以下内容：

```
kern.geom.label.disk_ident.enable=0
```

许多人支持 diskid 标记有强有力的理由。作者不会说这些观点是错误的。我们只会说 diskid 标记让我们双方都头疼。

FreeBSD 默认启用 diskid 标记。

## Glabel（手动）

除了其他类型的标记外，您还可以创建一个存储在磁盘或分区最后一个扇区的 GEOM 标记。这些标记采用 GEOM 特定的格式，称为 glabel。这些自定义标记的优点是它们不需要使用 GPT 格式，因此它们适用于 MBR 格式磁盘和没有分区的原始磁盘。`glabel` 使用提供者的最后一个扇区。

使用 `glabel(8)` 创建和查看 glabel。

```
#### glabel label -v mylabel /dev/ada02
Metadata value stored on /dev/ada02.
Done.
#### glabel status
Name Status Components
gpt/gptboot0 N/A ada0p1
label/mylabel N/A ada0p2
gpt/zfs0 N/A ada0p3
```

现在有了一个 `/dev/label/mylabel` 设备。

所有标记必须是唯一的。虽然您可以对多个磁盘应用相同的标记，但只会显示一个。

## DTrace

对某些 ZFS 特性的更高级调优需要使用 DTrace，这是一个用于跟踪软件行为和性能的程序。

使用 DTrace ZFS 的知识需要了解内核内部。这既不是一本关于 DTrace 的书，也不是内核内部。获取现有脚本并运行它不需要这些知识。

我们鼓励您使用这些 DTrace 脚本的输出来解决您的 ZFS 问题，并将其作为选择哪些内核内部的切入点。您可能不需要成为程序员，但专业的系统管理员应该对系统的工作原理建立理解。

盲目运行脚本正是 Lucas 极力抨击和反对的那种“神秘 IT”。尽管如此，他正是教你如何盲目运行一个 DTrace 脚本的。

DTrace 使用内核模块作为监控软件行为的软件探针：`dtrace.ko` 和 `dtraceall.ko`。您可以在 `loader.conf` 中在启动时自动加载这些模块。如果找不到内核模块，`dtrace(1)` 程序在您第一次运行时它会自动加载它们。

您必须以 root 身份运行 `dtrace`。

将您的脚本复制到文件中。然后运行 `dtrace -s`，将脚本作为参数。

按下 `CTRL-c` 中断脚本。

您可以从 zfsbook.com 链接到的 Lucas GitHub 仓库下载本书中提供的所有 DTrace 脚本。

理解内核工作原理的 FreeBSD 系统管理员可以更快、更准确地解决问题。关于 ZFS 内部的概览，请获取最新版本的《The Design and Implementation of the FreeBSD Operating System》（Addison-Wesley Professional, 2014）。同样，DTrace 是一个非常值得学习和理解的强大工具。我们推荐 Gregg 和 Mauro 的书籍《DTrace: Dynamic Tracing in Oracle Solaris, Mac OS X, and FreeBSD》（Prentice Hall, 2011）。

## 安装数据集

在 FreeBSD 10.1 及更高版本中，基于 ZFS 的安装会创建专门为启动环境（boot environments）设计的集。这在初看之下似乎违背直觉。让我们来看看默认安装中的几个数据集。

```
#### zfs list
NAME USED AVAIL REFER MOUNTPOINT
zroot/var 703K 1886 128K /var
zroot/var/crash 128K 1886 128K /var/crash
zroot/var/log 192K 1886 192K /var/log
zroot/var/mail 128K 1886 128K /var/mail
zroot/var/tmp 128K 1886 128K /var/tmp
```

我们为 `/var/` 的某些子目录创建了数据集：`/var/crash`、`/var/log`、`/var/mail` 和 `/var/tmp`。但 `/var` 下的所有其他目录呢？`/var/db` 目录包含了关键系统信息，比如软件包数据库。这难道至少和 `/var/tmp` 一样吗？

默认安装并没有根据目录内数据的重要性来创建数据集。它创建数据集是为了分离数据。

现在检查 `zfs mount` var，并看看这些数据集是如何挂载的。

```
#### zfs mount
zroot/ROOT/default /
n...
zroot/var/crash /var/crash
zroot/var/log /var/log
zroot/var/mail /var/mail
zroot/var/tmp /var/tmp
```

注意发现缺失的数据集：`/var`。该数据集存在，但没有挂载（`canmount` 属性设置为 no）。直接位于 `/var` 中的文件实际上进入了挂载为根目录的数据集，即 `zroot/ROOT/default`。而 `/var` 下具有自己独立数据集的文件（例如 `/var/log/messages`）则位于独立的数据集中。进入 `/var` 但没有自己独立数据集的文件（例如 `/var/db`）则进入根数据集。

数据的位置对于启动环境至关重要。可能受启动环境影响的数据存放在根数据集上。你不希望作为启动环境的一部分进行管理的数据将拥有自己的数据集。

考虑 `/var/db`。它包含关键信息，如软件包数据库、locate 数据库、`freebsd-update(8)` 记录等。所有这些与操作系统版本紧密绑定。将主机升级到新的操作系统版本需要使用 `freebsd-update`，并且可能意味着顺便也要更新你的附加软件。如果你必须回滚升级，你希望这些文件也一起回滚。

相比之下是 `/var/log`。如果我回滚升级，我不希望我的日志文件被回滚。日志涵盖的内容不仅仅是操作系统。同样，主目录和 `/var/mail` 中的邮件池最好不要随操作系统一起被回滚。¹

FreeBSD 升级会影响特定的目录。核心程序潜位于 `/bin`、`/sbin`、`/usr/bin` 和 `/usr/sbin` 中，库位于 `/lib` 和 `/usr/lib` 中。得益于不挂载的 `/usr` 目录，这些目录现在位于你的根数据集上。软件包安装在 `/usr/local` 下，但它也是根数据集的一部分。同样，得益于不挂载的 `/var`，包含所有关键系统信息的 `/var/db` 目录也是根数据集的一部分。

不属于核心系统的文件（如日志、用户主目录等）拥有它们自己的数据集。

这使得核心系统和官方软件包与主机的其他部分分离，让你能够将其作为一个整体进行管理。FreeBSD 开发者正在对基础系统以及附加软件包进行打包，这可能需要重新考虑这里讨论的系统。

## 使用启动环境

ZFS 的快照（snapshot）和克隆（clone）功能允许你保存、复制和复制文件系统。（详见 FreeBSD Mastery）。



使用 ZFS，在进行系统维护（如升级）之前创建快照是一个好主意。如果升级失败，你可以回滚到最后一个可用版本。为了调试失败的升级，将快照复制到测试系统进行调试，而你的生产系统保持运行在旧的操作系统版本上。

“启动环境”在系统维护之前打包成一个整洁的包。你不需要启动环境管理器来使用快照，但管理器让这些操作变得简单得多。FreeBSD 有一个启动环境管理器，`beadm`。

你现在准备好使用启动环境了。

### 查看启动环境

每个启动环境都是 `zroot/ROOT` 下的一个数据集。你刚刚安装了启动环境。使用 `beadm list` 查看所有启动环境。

```
#### beadm list
BE      Active  Mountpoint Space   Created
default NR        /        649.9M   2016-02-15 14:47
```

有一个名为 `default` 的环境，位于 `zroot/ROOT/default`。这是一个新安装的系统，这是符合预期的。

`Active` 列显示启动环境是否正在使用。`N` 表示该环境正在运行。`R` 表示该环境将被激活。

`Mountpoint` 列显示启动环境的位置。`Space` 列显示磁盘空间。`Created` 列显示创建环境的日期。

### 创建启动环境

在更改系统之前，创建一个启动环境。用补丁命名该环境。使用 `freebsd-update` 版本。

```
#### freebsd-version
```

等待，`Space` 列显示已用空间。`Created` 列显示创建环境的日期。

```
BE      Active  Mountpoint Space   Created
default NR        /        649.9M   2016-02-15 14:47
```

有一个名为 `default` 的环境，位于 `zroot/ROOT/default`。这是一个新安装的系统，这是符合预期的。

### 激活启动环境

假设你应用了最新的补丁，结果机器失控了。你的服务器崩溃了，内核恐了，或者小鬼精从 USB 端口跳出来偷走了你的勺子。通过激活启动环境并重启回退到旧版本。使用 `beadm` 激活启动环境。

```
#### beadm activate 10.3-release
Activated successfully
#### beadm list
```

`BE      Active  Mountpoint Space   Created`

`default N        /        308.1M   2016-05-19 10:04`

`10.3-release R -        457.1M   2016-05-19 14:13`

`default` 环境的 `Active` 标记为 `N`，意味着它正在运行。`10.3-release` 环境的 `Active` 标记为 `R`，所以重启后它将被激活。

重启系统，你突然回到了运行 `10.3-release` 环境，没有任何安全更新，并带有你最初安装的任何软件包。

空间。这些启动环境中的某些你可能再也不会使用了。

```
#### beadm list
| BE | Active | Mountpoint | Space | Created |
| :--- | :--- | :--- | :--- | :--- |
| default | NR | / | 3.6G | 2015-04-28 11:53 |
| install | | | 126.0M | 2015-04-28 12:19 |
| 10.3-p9 | | | 209.0M | 2015-05-14 08:01 |
| 10.3-p10 | | | 169.0M | 2015-05-24 11:02 |
| 10.3-p10-13Jun | | | 150.0M | 2015-06-10 14:24 |
| 10.3-p10-13Jun | | | 47.3M | 2015-06-13 06:19 |
| 10.3-p12 | | | 7.7M | 2015-06-19 07:06 |
```

使用 `freed-version` 告诉我这个特定的系统运行的是 FreeBSD 10.3-RELEASE-p13。我想我可能想回退到10.3-p12。但我不会回到 p10、或 p9，特别是尤其是 install 版本。删除这些启动环境将节省磁盘空间，并让我现有的启动环境更易阅读和理解。

使用 `beadm destroy` 和启动环境名称来移除不需要的启动环境。

```
#### beadm destroy 10.3-release
Are you sure you want to destroy '10.3-release'?
This action cannot be undone (y/[n]): y
Destroyed successfully
```

我 FreeBSD 10.3 的原始安装现在已经从这个系统中消失了。剩下的所有内容都以某种方式经过了修复。这可能会释放根池（root pool）上的一些空间——并不是所有启动环境使用的空间，快照和克隆在最后一个需要该块的快照被删除之前不会释放空间。但你会找回一些空间。

## 启动环境与 ZFS

启动环境利用了 ZFS 快照和克隆。但它们究竟是做什么的？看看我们最初安装在宿主机上的快照。

```
#### zfs list -t snapshot
| NAME | USED | AVAIL | REFER | MOUNTPOINT |
| zroot/ROOT/default@2016-02-16-08:35:22 | 25.9M | - | 479M | - |
```

这台主机有一个快照，以我创建的启动环境命名。默认启动环境是当前运行的那个，所以它不需要快照。现在看 `zroot/ROOT` 下的数据集。



每个启动环境都是 `zroot/ROOT` 下的一个数据集，从源快照克隆而来。默认启动环境是 `zroot/ROOT/default`，而 `10.3-release` 启动环境位于 `zroot/ROOT/10.3-release`。

虽然所有的启动数据集的挂载点都是 `/`，但除了活动环境外的，每个启动环境都不能设置为 `off`。如果你愿意，可以挂载这些数据集，但你会想要指定一个新的挂载点。

删除启动环境会销毁相关的快照和克隆。

### 访问未使用的启动环境

访问未使用启动环境内容的一种方法是检查创建这些启动环境时的快照。启动环境可以在隐藏的 `/.zfs` 目录中访问。这对于快速检查非常方便。

如果你想以读写方式挂载启动环境，请使用 `beadm mount` 命令和启动环境名称。启动环境将挂载在位置 `/tmp`。

```
#### beadm mount 10.3-p19
Mounted successfully on /tmp/10.3-p19
```

当你完成环境的操作后，使用 `beadm umount` 卸载它。

```
#### beadm unmount 10.3-p19
Unmounted successfully.
```

可以通过 `mount` 和 `mountpoint` 属性挂载和卸载启动环境快照。如果你操作不当，会将启动环境挂载到运行中的启动环境之上。虽然 FreeBSD 文件系统是可以堆叠的，但在运行系统上更改所有二进制文件会让你陷入困境。想象一下无法运行 `reboot(8)`，因为二进制文件无法与内核通信！使用内置于 `beadm(8)` 的挂载和卸载功能。

所以你真的搞坏了你的操作系统。忘记多用户模式吧——甚至是单用户模式也变成了一系列错误信息，以至于经验丰富的 FreeBSD 黑客都认为你的硬件故障了。你可以进入这个问题，但这需要控制台访问。FreeBSD 10.3 及以上版本允许你在引导程序提示符（loader prompt）更改启动环境。

```
+Welcome to FreeBSD==========
| 1. Boot Multi User [Enter] |
| 2. Boot [S]ingle User |
| 3. [E]scape to loader prompt |
| 4. Reboot |
| Options: |
| 5. [K]ernel: kernel (1 of 2) |
| 6. Configure Boot [O]ptions |
| 7. Select Boot [E]vironment... |
+===========================
```

选择项目 7，你会得到一个新的菜单。

```
+Welcome to FreeBSD==========
| 1. Active: |
| 2. bootfs: zroot/ROOT/default |
| 3. [P]age: 1 of 1 |
| Boot Environments: |
| 4. 10.3-release |
| 5. default |
+==========================
```

选择你偏好的启动环境。菜单将更新，显示你选择的环境（标记为 Active）。按 ENTER 返回主菜单，按 ENTER 启动。系统将恢复到已工作的环境，让你有机会发现出了什么问题。

## 启动环境与应用程序

FreeBSD 在过去的几十年里开发了许多做法，特别是软件包。其中一些基于 FreeBSD 的习惯：MySQL 存储在 `/var/db/mysql`。有些是基于软件本身的偏好：PostgreSQL 将记录保留在 `/usr/local/postgresql`。这些在使用启动环境时都会产生的问题。

以 MySQL 为例。目录 `/var/db/mysql` 是根数据集的一部分。如果你将数据库数据存储在启动环境中，回退到旧的启动环境会将你的数据库数据恢复到之前的版本。这可能不是你想要的。

其他软件具有相同的问题。处理这个问题并不，但你需要了解你的软件。你有两个选择：更改数据位置，或者在根目录下创建数据集。一旦你理解了需求，两种都可行。

### 移动应用程序数据

移动应用程序数据需要为数据创建一个数据集，并告诉应用程序使用该位置。在这里，我决定将 MySQL 数据放在 `/var/mysql`。

```
#### zfs create zroot/var/mysql
```

我现在必须告诉 MySQL 使用这个数据目录。检查 `/local/etc/rc.conf` 中的变量，发现我在 `/etc/rc.conf` 中需要 `mysql_dbdir` 选项：`mysql_dbdir=/var/mysql`。

我必须将 `/var/db/mysql` 中的任何现有数据和配置文件移动到 `/var/mysql`，然后重启服务器。

### 创建新数据集

启动环境只影响根文件系统数据集。如果你想将应用程序留在通常的位置，必须为该数据创建一个新数据集。以 PostgreSQL 为例。PostgreSQL 将数据存储在 `/usr/local/postgresql`，所以你可以直接创建该数据集。

```
#### zfs create zroot/usr/local/postgresql
```

没有 `/usr/local` 数据集，你无法创建 `zroot/usr/local/postgresql`。如果你创建一个标准的 `/usr/local` 数据集，你将从启动环境中提取 `/usr/local` 中的文件，或者在填充的 `/usr/local` 目录上覆盖一个空文件系统。与 `/usr` 一，解决方案是创建一个 `canmount` 属性设置为 `off` 文件系统，然后创建子数据集。

```
#### zfs create -o canmount=off zroot/usr/local
#### zfs create zroot/usr/local/postgresql
```

你现在拥有 `/usr/local/postgresql` 自己的数据集，并可以安全地通过启动环境运行 PostgreSQL。

两种解决方案都没有解决 Apache 这样混乱的软件软件包。例如，Apache 2.4 在 `/usr/local/www` 和 `/usr/local/etc/apache24` 中塞了一堆东西。管理员应该编辑这些文件的一部分，而不是全部。通过 ZFS 数据集进行完全分离。对于 Apache 此类程序，我通常会创建一个全新的数据集，例如 `/var/www/`，并将活动站点文件放在那里。

## 磁盘加密与启动环境

标准的 `beadm` 启动环境管理器只与单个根文件系统数据集工作。安装到 GELI 加密磁盘的 FreeBSD 与 `beadm` 不兼容。

在加密设备上安装带有 ZFS 的默认 FreeBSD 需要一个小的、未加密的分区来存储引导内核。默认安装程序为此创建 `bootpool` 池，并将 `/boot` 放在 `bootpool/boot`。在运行的系统中，`/boot` 是指向其他 pool 的符号链接。其余部分进入 `zroot` 池。

PC-BSD 10 确实支持 GELI 加密磁盘上的启动环境，但它们使用 GRUB 引导加载程序和一些特殊技巧。

FreeBSD 11.0 预计支持从 GELI 加密的 ZFS 启动，而无需独立的启动池，使得启动环境的工作方式与在未加密磁盘上完全一致。在本书出版时，该功能尚未发布。

对于大多数 FreeBSD ZFS 用户来说，启动环境节省了大量麻烦。让我们继续讨论其他可以帮你节省麻烦的方法。

> 我们听说，世界贸易组织认为篡改系统管理员的电子邮件是处刑的理由。我们还没有通过实验来验证这一点，因为这符合我们的偏见。

# 第 2 章：委托与监狱 (Jails)

ZFS 设计者尽力减轻系统管理员的存储管理工作。

减少工作量最好的方法之一就是让别人为你工作。ZFS 拥有一个功能全委托系统，允许你规定用户或用户组在每个数据集上可以使用命令和功能。你可以允许用户创建和销毁自己的快照、创建子数据集、生成空间消耗报告，或控制数据集的属性。ZFS 基于委托功能为 jails 提供了特殊支持。

## ZFS 委托

ZFS 允许你针对每个数据库，按属性和按命令将管理任务委托给用户。你可以让数据库管理员完全控制数据库池，或让 Web 服务器管理员控制网站数据上的快照。使用 `zfs allow` 命令来委托权限。

将池或数据集作为参数传递给 `zfs allow` 会显示该设备的权限。在这里，我获取 `remotepool` 池的权限。

```bash
#### zfs allow remotepool
---- Permissions on remotepool -----
Local+Descendent permissions:
  user replicator compression, create, destroy, mount, mountpoint, receive
```

该池有一个权限条目，针对 `replicator`。该用户拥有 `compression` 和 `mountpoint` 属性的权限，以及 zfs 的 `create`、`destroy`、`mount` 和 `receive` 子命令。（第 4 章讨论了这些特定权限的重要性。）



应用程序和用户可以定义自己的属性。像 `zftools` 这样的程序创建属性来管理快照。有一个特殊的权限 `userprop`，允许用户创建用户定义的属性。用户定义的属性被作为一个单一权限分配：你不能单独分配不同的用户定义属性。

虽然 `root` 在这里没有被列出任何权限，但 `root` 可以随心所欲地做任何事。因为 `Unix` 就是这么运行的。

### 添加权限

将池或数据集的权限委托给用户或组。`-u` 标志允许你为 `zfs allow` 指定用户名，`-g` 指定组。

```bash
zfs allow -u username permissions pool/dataset
```

假设我们有一个麻烦的用户——就叫他 Lucas 吧。他总是尝试一些愚蠢的 `Unix` 技巧，搞坏了他的家目录。让我们允许 Lucas 创建自己的快照，这样他每次弄坏环境时就不需要打扰系统管理员了。

```bash
zfs allow -u lucas snapshot,rollback mypool/usr/home/lucas
```

当你查看数据集权限时，你分配给他的两个权限就会显示出来。

```bash
zfs allow mypool/usr/home/lucas
```

```
---- Permissions on mypool/usr/home/lucas -----
Local+Descendent permissions:
  user lucas rollback, snapshot
```

委托是自动继承的。当 Lucas 获得对其家目录数据集创建快照的能力时，他也获得了家目录下所有子数据集的权限。出于某种原因，他有一个名为 `blackmail`（勒索）的数据集。那可能是他存放所有照片和记录的地方，他用这些来获取 BSD 开发者帮助他进行研究和技术评审。

```bash
zfs allow mypool/usr/home/lucas/blackmail
```

```
--- Permissions on mypool/usr/home/lucas
Local+Descendent permissions:
 lucas rollback, snapshot
```

Lucas 应该拥有创建快照的权限。但在告诉他可以用之前，先模拟身份并创建一个快照。

```bash
$ su lucas
$ zfs snapshot mypool/usr/home/lucas/blackmail@bsdcan-drunken-escapes
$ zfs list -t all -r -o name mypool/usr/home/lucas
```

```
NAME
mypool/usr/home/lucas
mypool/usr/home/lucas/blackmail
mypool/usr/home/lucas/blackmail@bsdcan-drunken-escapes
```

我们知道这样做。在 Lucas 产生新想法之前，让我们删掉这个快照。

```bash
$ zfs destroy mypool/usr/home/lucas/blackmail@bsdcan-drunken-escapes
cannot destroy snapshots: permission denied
```

创建新数据集涉及挂载，而销毁数据集显然应该包括卸载。为了能够有用，`clone`、`create` 和 `destroy` 命令都需要 `mount` 权限。要授予 lucas 权限，运行 `zfs allow -u lucas` 并列出所需的权限和数据集。

```bash
zfs allow -u lucas destroy,mount mypool/usr/home/lucas
```

检查你的工作会显示两次运行 `zfs allow` 时分配的所有权限。

```bash
zfs allow mypool/usr/home/lucas
```

```
--- Permissions on mypool/usr/home/lucas
Local+Descendent permissions:
 lucas destroy, mount, rollback
```

Lucas 现在可以自作自受地毁掉他家目录所在的数据集。而且他一定会来抱怨的。

在 Lucas 的家目录下运行 `zfs destroy` 现在是系统管理员的特权。

### 创建时间权限

ZFS 允许你今天就创建权限，用于下周二或未来某个某个时间才会存在的数据集。创建时间权限适用于创建数据集的用户。它们就像权限委托的“粘滞位（sticky bit）”。使用 `-c` 定义时间权限。

这类权限的一个常见需求是将权限赋予所有人，而不是指定系统上的每个用户，或者定义一个包含所有用户的组。与其使用 `-u` 或 `-g` 加上用户名或组名，不如使用 `-e` 标记表示所有人（所有用户）。

使用创建时间权限需要对继承关系进行精细控制。你希望创建时间权限应用于子数据集，而不是父数据集。父数据集应该有它自己的权限，通过 `-l` 设置。

假设我们有一个所有人都可以使用的临时数据集（scratch dataset）。它类似于 `/tmp`，但具有 ZFS 特性。我们希望每个人都能在这个空间内创建和挂载数据集，但没有权限删除整个数据集集。这些权限必须被限制（通过 `-l` 标记），以允许执行 `-e create,mount mypool/scratch` 而不被新的子数据集自动继承。

```bash
zfs allow -l -e create,mount mypool/scratch
```

现在使用 `-c` 指定分配给新创建数据集的创建时间权限。

```bash
zfs allow -c snapshot,rollback,destroy mypool/scratch
```

检查你的工作将看到创建时间权限以权限集的形式显示。

```bash
zfs allow mypool/scratch
```

```
---- Permissions on mypool/scratch
Permission sets:
  destroy, rollback, snapshot
Local permissions:
  everyone create, mount
```

当然，真正的测试是以普通用户身份运行这些命令。让 Lucas 在 `mypool/scratch` 下创建一些数据集。

```bash
su lucas
```

```bash
$ zfs create mypool/scratch/lucas
```

执行成功了。但他拥有哪些权限？

```bash
$ zfs allow mypool/scratch/lucas
```

```
---- Permissions on mypool/scratch/lucas
Local permissions:
```

```
user lucas destroy,rollback,snapshot
---- Permissions on mypool/scratch --------------------
Permission sets:
  destroy,rollback, snapshot
Local permissions:
  everyone create,mount
```

现在 Lucas（且只有 Lucas）可以创建快照并删除数据集。其他用户可以创建只有他们自己访问的数据集。

### 修改权限的权限

拥有 `allow` 命令权限的用户可以委托他已拥有的任何权限。这让你作为团队负责人或项目经理能够撤销其成员的权限。

考虑之前那个临时数据集的例子。假设 Lucas 想允许 `l1z` 用户在他新的临时数据集上创建快照。

首先，通过允许 Lucas 使用 `zfs allow` 命令，赋予他委托权限的能力。

```bash
zfs allow -u lucas mypool/scratch/lucas
```

```bash
zfs allow mypool/scratch/lucas
```

```
---- Permissions on mypool/scratch/lucas
Local permissions:
  user lucas destroy, snapshot
Local+Descendent permissions:
  user lucas allow
---- Permissions on mypool/scratch
Permission sets:
  destroy, snapshot
Local permissions:
  everyone create, mount
```

现在 Lucas 可以将他所拥有的任何权限委托给 `l1z` 账户。通过以他的身份登录来测试这一点。



```
#### su lucas
$ zfs allow -u l1z snapshot myypool/scratch/lucas
$ zfs allow myypool/scratch/lucas
---- Permissions on myypool/scratch/lucas
Local permissions:
  user lucas destroy, snapshot
Local+Descendent permissions:
  user lucas allow
  user l1z snapshot
---- Permissions on myypool/scratch
Permission sets:
  destroy, snapshot
Local permissions:
  everyone create, mount
```

但 Lucas 无法给出他并不拥有的权限：

```
$ zfs allow -u l1z clone myypool/scratch/lucas
cannot: permission denied
```

系统管理员可以将权限委托给用户，并让用户负责其数据集的进一步委托。

### 权限集 (Permission Sets)

运行 `zfs allow` 会显示一个你可以授予用户的 60 多种权限列表。我们不会在这里列出所有，但你可以对每个 `zfs(8)` 子命令以及每个池和数据集属性授予权限。与其给每个用户授予长列表并不可避免地遗漏某一项，不如使用 `-s` 标记并给出一个以 `@` 开头的权限集名称。然后列出该集中的权限，以及该权限集有效的数据集名称。

运行 `zfs allow` 会显示一个你可以授予用户的 60 多种权限列表。我们不会在这里列出所有，但你可以对每个 `zfs(8)` 子命令以及每个池和数据集属性授予权限。

## 委托与监狱 (Delegation and Jails)

FreeBSD 支持一种名为 `jails` 的轻量级虚拟方法。

### 监狱 (Jailing a Dataset)

要构建监狱，将 `jailed` 属性设置为 `on`。主机将不再能够挂载该数据集。要构建监狱，使用 `zroot/lucas/jail` 数据集作为根。在这里我们使用

```
#### zfs create -o jailed=on mountpoint=/jail zroot/lucas/jail
```

一旦有了数据集，启动一个以它为根的临时监狱。

```
# jail -c path=/zroot/lucas/jail mount.devfs allow.allow.mount.zfs \
hostname=lucas ip4.addr="lo0|127.0.0.2" exec.poststart=\n/sbin/zfs jail lucas zroot/lucas/jail command=/bin/sh
```

现在进入监狱。

#### jexec lucas sh

由于我们在监狱（jail）中，我们可以创建一个新的数据集。

```
jail# zfs create zroot/jails/lucas/jail/foo
```

新的数据集以及该监狱的父数据集是可见的。

```
jail# zfs list -o name,mountpoint
NAME MOUNTPOINT
zroot /zroot
zroot/jails /zroot/jails
zroot/jails/lucas /zroot/jails/lucas
zroot/jails/lucas/jail /jail
zroot/jails/lucas/jail/foo /jail/foo
```

在 `zroot/jails` 中，或者实际上在该监狱的底层宿主机中是否存在其他数据集？监狱内的用户永远不知道。

用户 `lucas` 现在可以挂载点、创建和销毁数据集、将数据集委托给监狱内的普通用户等。如果这样做是为了防止 Lucas 这类用户闯入现实世界……

## 构建带有 ZFS 委托的监狱

你的监狱可能并不想要一个空壳监狱。你可能想要一个真实的用户空间，包含程序以及运行服务的。。这意味着要在你的监狱数据集上安装 FreeBSD。监狱可能极其复杂，因此我们不会完全涵盖它们。我们将在监狱数据集上进行基础的 FreeBSD 安装，以便你可以将 ZFS 添加到现有的监狱进程中。

首先，创建监狱数据集。

```
#### zfs create -p mypool/jails/lucas/zroot
```

现在在该数据集上安装操作系统。你可以直接从 FTP 安装，我们那里有 FreeBSD 10.3 的 amd64 版本。

```
#### fetch -o ftp://ftp.freebsd.org/pub/FreeBSD/releases/amd64/10.3-RELEASE/base.txz | tar -Xf -C /
/mypool/jails/lucas/
```

如果你打算安装多个监狱，请下载适用于你版本的 `base.txz` 并解压：

```bash
#### tar -xf base.txz -C /mypool/jails/lucas/
```

一旦你将操作系统拷贝到监狱数据集中，请将该数据集标记为不可信。这使得宿主机无法访问该数据集。

```
#### zfs set mountpoint=/zroot mypool/jails/lucas/zroot
#### zfs set jailed=on mypool/jails/lucas/zroot
```

准备好数据集后，在监狱配置文件 `/etc/jail.conf` 中为该监狱创建一个条目。

在这里我们定义监狱名称 `no.gelato.for.michaelwlucas.com`。

有了 `jail.conf` 条目后，我们可以使用标准的 FreeBSD 工具启动监狱。

```
#### service jail start nogelatoforyou
```

最后一部分设置需要在监狱内部完成。或者，你也可以在安装操作系统时预先进行一些疯狂疯狂的计划，但那会让过程失去乐趣。让我们进入监狱并查看我们的数据集。

```
#### jexec nogelatoforyou /bin/sh
jail# zfs list
```

| NAME | USED | AVAIL | REFER | MOUNTPOINT |
| :--- | :--- | :--- | :--- | :--- |
| mypool | 5.21G | 13.16T | 96K | none |
| mypool/jails | 180M | 13.16T | 96K | /mypool/jails |
| mypool/jails/lucas | 180M | 13.16T | 180M | /mypool/jails/lucas |
| mypool/jails/zroot | 96K | 13.16T | 96K | /zroot |

这个新监狱在 `rc.conf` 中没有启用 ZFS，因此新数据集未被宿主机挂载。

```
jail# sysrc zfs_enable=YES
```

修改配置后，重启并重新进入监狱。

```
#### service jail restart
```

你将看到新创建的数据集。

```
jail# zfs create mypool/jails/lucas/zroot/test
```

（此处由于原文中存在大量重复和错误：在处理这些困难用户时，ZFS 提供了 `snapshot_limit` 和 `filesystem_limit` 属性，允许你限制快照或子数据集的数量。）

```
path /dev/zvol/vm/db1
size 1T
}
}
```

iSCSI target 的名称基于提供 target 的组织的域名名。理论上，你可以以任何你喜欢的方式为 iSCSI target 命名，但某些启动器软件会尝试使用该名称设置优化。最好的做法是从你的商业 SAN 商处复制 target 名称。

iSCSI 设备的命名方案始终以字符串 `iqn` 开头。接着是域名注册的年份和月份，然后是反转的域名名。在这里，`mwluccas.org` 于 2013 年 11 月注册，因此 target 名称以 `iqn.2013-11.org.mwluccas` 开头。然后是一个冒号以及该特定 target 的名称。

与我们的门户组（portal group）一样，这个 target 不需要身份验证。`portal-group` 关键字将我们与之前创建的 `group0` 门户组关联起来。

此 target 只有一个 LUN，编号为 0。我们提供了文件或设备节点的路径以及 target 的大小。注意我们在这里使用的设备节点，`/dev/zvol/vm/db1`。虽然一个 `zvol` 可能有多个设备节点，但请始终访问 `/dev/zvol` 下 iSCSI 导出的 `zvols` 的设备节点。最好的办法是使用 `volmode` 为 `dev` 创建此类 `zvols`，这样服务器的 GEOM 层就不会探测并预配置该 `zvol`。



一旦 `/etc/ctld1.conf` 存在，启动 `ctld(8)`。

```
service ctld start
```

状态和错误信息显示在 `/var/log/messages` 中。

如果 `ctld(8)` 不符合你的需求，请使用你喜欢的任何 target 软件。使用 zvol 的设备节点将其提供给启动器。

## 网络文件系统

关于网络文件系统（或 NFS）已经写了整整的书。许多不同的操作系统都支持 NFS，可以作为服务器、客户端或两者兼具。在书中，我们将关注如何通过 ZFS 集成工具提供 NFS 共享。

### NFS 配置类型

你可以使用传统的 FreeBSD `/etc/exports` 文件来管理基于 ZFS 的 NFS 导出，这不会发生发生任何可怕的事情。如果你是一个老 FreeBSD 高手，`/etc/exports` 甚至可能让你感到更舒服。`zfs(8)` 为你处理了 NFS 管理的许多方面，并在所有 ZFS 平台上工作方式完全相同。

无论你在主机上如何管理 NFS，我们强烈建议你选择一种方法并坚持下去。不要同时使用 `/etc/exports` 和 ZFS 来管理你的共享。FreeBSD 会从这两个位置读取共享信息，这使得故障排除变得更加麻烦。

FreeBSD 主机必须有一个 `/etc/exports` 文件来提供 NFS 共享，即使你完全在 ZFS 内部管理 NFS。获取此文件的简单方法是执行 `touch /etc/exports`，尽管你可能想要一个只包含注释的 exports 文件，引导其他系统管理员使用 `zfs(8)`。

就像处理 iSCSI 一样，我们不会完全涵盖 NFS。我们将从 ZFS 的角度涵盖管理 NFS，并在有用的地方与传统的 NFS 配置进行比较。

### 启用 NFSv2/v3

如果主机没有运行 NFS 所需的服务，那么在 ZFS 级别启用 NFS 将没有任何作用。在 `/etc/rc.conf` 中设置以下内容以便在启动时启动提供 NFS 所需的进程。

```
nfs_server_enable=YES
rpcbind_enable=YES
mountd_enable=YES
rpc_lockd_enable=YES
rpc_statd_enable=YES
```

并不是所有的环境都需要所有这些服务，但开启它们不会消耗许多系统资源，并提供最广泛的兼容性和不错的的性能。

你还必须通过 `/etc/hosts.allow` 条目允许网络上的主机访问 `rpcbind(8)`。在这里，我允许网络 `203.0.113.0/24` 访问我的 NFS 服务。

```
rpcbind: 203.0.113.0/255.255.255:0: allow
```

如果没有这个 `hosts.allow` 条目，你的客户端将用无意义的 NFS 错误让你抓疯。

### 通过 ZFS 配置 NFSv2/v3

ZFS 是以数据集为单位配置 NFS 的。ZFS 属性 `share` 决定了数据集如何共享。此属性可以设置为 `on`、`off` 或数据集的 NFS 共享选项。

如果设置为 `off`，ZFS 不为该数据集配置共享。但是，该数据集仍然可以通过 `/etc/exports` 共享。

将此属性设置为 `on` 会通过 NFS 共享数据集。这等同于通过 `/etc/exports` 列出文件系统。为 `zroot/home` 将 `share` 设置为 `on` 就像下面的 `/etc/exports` 条目。

世界上任何一个主机都可以访问并挂载此主机。为我们允许的所有主机设置要明智得多。

```
zfs share="203.0.113.0/24" zroot/home
```

这将生成类似这样的 `/etc/zfs/exports`。

```
/home 203.0.113.0/24
```

如果你在属性中输入了更复杂的值，请用引号括起来或进行转义。

```
zfs share="-network 203.0.113.0 -mask 255.255.255.0" zroot/home
```

任何有效的 `/etc/exports` 条目都可以作为 `share` 的值。

### 启用 NFSv2/v3

如果主机没有运行 NFS 所需的服务，那么在 ZFS 级别启用 NFS 将没有任何作用。在 `/etc/rc.conf` 中设置以下内容以便在启动时提供 NFS 所需的进程。

```
nfs_server_enable=YES
rpcbind_enable=YES
mountd_enable=YES
rpc_lockd_enable=YES
rpc_statd_enable=YES
```

并不是所有的环境都需要所有这些服务，但开启它们不会消耗许多系统资源并提供最广泛的兼容性和不错的性能。

你还必须通过 `/etc/hosts.allow` 条目允许网络上的主机访问 `rpcbind(8)`。在这里，我允许网络 `203.0.113.0/24` 访问我的 NFS 服务。

```
rpcbind: 203.0.113.0/255.255.255:0: allow
```

如果没有这个 `hosts.allow` 条目，你的客户端将用无意义的 NFS 错误让你抓疯。

### 通过 ZFS 配置 NFSv2/v3

ZFS 是以数据集为单位配置 NFS 的。ZFS 属性 `share` 决定了数据集如何共享。此属性可以设置为 `on`、`off` 或数据集的 NFS 共享选项。

如果设置为 `off`，ZFS 不为该数据集配置共享。但是，该数据集仍然可以通过 `/etc/exports` 共享。

将此属性设置为 `on` 会通过 NFS 共享数据集。这等同于通过 `/etc/exports` 列出文件系统。为 `zroot/home` 将 `share` 设置为 `on` 就像下面的 `/etc/exports` 条目。

世界上任何一个主机都可以访问并挂载此主机。为我们允许的所有主机设置要明智得多。

```
zfs share="203.0.113.0/24" zroot/home
```

这将生成类似这样的 `/etc/zfs/exports`。

```
/home 203.0.113.0/24
```

如果你在属性中输入了更复杂的值，请用引号括起来或进行转义。

```
zfs share="-network 203.0.113.0 -mask 255.255.255.0" zroot/home
```

任何有效的 `/etc/exports` 条目都可以作为 `share` 的值。

### 启用 NFSv2/v3

如果主机没有运行 NFS 所需的服务，那么在 ZFS 级别启用 NFS 将没有任何作用。在 `/etc/rc.conf` 中设置以下内容以便在启动时提供 NFS 所需的进程。

```
nfs_server_enable=YES
rpcbind_enable=YES
mountd_enable=YES
rpc_lockd_enable=YES
rpc_statd_enable=YES
```

并不是所有的环境都需要所有这些服务，但开启它们不会消耗许多系统资源并提供最广泛的兼容性和不错的性能。

你还必须通过 `/etc/hosts.allow` 条目允许网络上的主机访问 `rpcbind(8)`。在这里，我允许网络 `203.0.113.0/24` 访问我的 NFS 服务。

```
rpcbind: 203.0.113.0/255.255.255:0: allow
```

如果没有这个 `hosts.allow` 条目，你的客户端将用无意义的 NFS 错误让你抓疯。

### 通过 ZFS 配置 NFSv2/v3

ZFS 是以数据集为单位配置 NFS 的。ZFS 属性 `share` 决定了数据集如何共享。此属性可以设置为 `on`、`off` 或数据集的 NFS 共享选项。

如果设置为 `off`，ZFS 不为该数据集配置共享。但是，该数据集仍然可以通过 `/etc/exports` 共享。

将此属性设置为 `on` 会通过 NFS 共享数据集。这等同于通过 `/etc/exports` 列出文件系统。为 `zroot/home` 将 `share` 设置为 `on` 就像下面的 `/etc/exports` 条目。

世界上任何一个主机都可以访问并挂载此主机。为我们允许的所有主机设置要明智得多。

```
zfs share="203.0.113.0/24" zroot/home
```

这将生成类似这样的 `/etc/zfs/exports`。

```
/home 203.0.113.0/24
```

如果你在属性中输入了更复杂的值，请用引号括起来或进行转义。

```
zfs share="-network 203.0.113.0 -mask 255.255.255.0" zroot/home
```

任何有效的 `/etc/exports` 条目都可以作为 `share` 的值。

## 但我有 rsync！



几十年来，`rsync(1)` 一直是机器间同步文件的标准工具。为了同步文件，`rsync` 会遍历目录树，评估每个文件的时间戳和加密校验和，并将其与远程侧的文件进行比较。许多组织已经部署了基于 `rsync` 的大量基础设施。

`ZFS` 从磁盘底层开始设计，以实现最大性能。它对 `rsync` 的完胜如此惨烈，以至于 `rsync` 的妈妈都急需医疗救治。`ZFS` 在磁盘上维护了一个列表，记录每个快照之间不同的块。复制过程不需要确定哪些文件发生了变化——文件系统本身已经持有了这些信息。复制过程会立即尽可能快地开始发送这些块。由于更改的块包含了重组文件所需的所有元数据，复制过程甚至不需要知道这些块属于哪个文件。

当 `rsync` 正在遍历你的文件系统、查看每个文件、检查时间戳、计算校验和并将其与另一侧的版本进行比较时，`ZFS` 已经完成了。如果你有 10 TB 的数据，而只有 1 GB 发生了变化，`rsync` 仍然需要检查每一个文件。而 `ZFS` 只需要抓取那 1 GB 更改的块并发送它们。

需要更快的 `rsync` 同步的系统管理员可以告诉 `rsync` “作弊”，假设如果本地和远程文件的最后修改时间相同，则文件没有发生变化。（这实际上并不总是如此，但不要因此埋怪 `rsync`——系统管理员应该对此了然）。当文件时间戳发生变化时，`rsync` 会计算双方文件分块的校验和，并比较这些校验和。如果它发现差异，就会计算出一个增量并将其发送过去。这意味着如果你对一个大文件进行了微小的修改，`rsync` 必须在本地和远程侧都读取并检查整个文件。使用 `rsync` 在备份机器上维护 500 GB 的虚拟机磁盘镜像副本会消耗大量的带宽和 CPU 时间。

`ZFS` 中的每个块都有一个出生时间（`birthtime`），即创建该块的事务组 ID。复制过程会发送任何晚于上次运行复制任务时的块。这些块是来自一个新文件，还是来自一个巨大文件的中间，并不重要。

基于快照的复制的优势在定期同步文件系统时真正大显威力。假设你在备份服务器上复制了一个快照。一小时后，你创建了一个新快照并将该快照增量发送到备份服务器。`ZFS` 在几秒钟内完成，而 `rsync` 仍在遍历第一层目录。

`rsync(1)` 支持快照备份模式。然而，`rsync` 快照与 `ZFS` 快照完全不同。在 `rsync` 快照中，如果你修改了一个 1 GB 文件的 1 字节，`rsync` 会保留该文件的两个副本。而相反，`ZFS` 保留的是单个块的两个不同版本。文件的两个版本共享剩余的块。

为 `rsync` 辩护，它是一个跨平台、跨文件系统的工具。你可以使用 `rsync` 同步不同操作系统以及不同文件系统之间的目录树。Lucas 曾使用 `rsync` 在截然不同的 Unix 类平台（如 FreeBSD、AIX 和 Linux）之间同步目录树。

但如果你正在使用 `ZFS`，复制功能特别适合处理 `ZFS`。复制功能能够理解并复制 `ZFS` 属性。它可以维护克隆（`clone`）与其父级快照之间的关系，而 `rsync` 则会丢失这种链接并导致你所有的空间节省。`rsync(1)` 在原始块设备上工作得并不好，但 `ZFS` 复制可以与 `zvols` 工作。复制还使用了文件系统集成的校验和，因此不存在收到的文件与原始文件存在差异的风险。

`ZFS` 复制也是版本无关的。只有当你刻意添加命令行标志请求它们时，新的池功能才会被启用。这使得 `ZFS` 复制能够轻松地在不同版本的池之间移动数据。

# 为什么要复制？

复制在许多方面发挥作用：最明显是在备份中，但也适用于测试、虚拟化和数据迁移。

你记得 RAID 不是备份吧？即使是 RAID-Z3 也不是真正的备份。当你的机器起火时，当执法部门在你的托管提供商处没收硬件，或者你不小心删除了那个重要数据集时，RAID-Z3 无法拯救你。将重要的池复制到外部驱动器、备份机器或磁带库。`ZFS` 的妙之处在于，在初始复制之后，每次备份都可以是增量的。

让我们更进一步。也许仅仅能够恢复数据是不够的。你必须保证数据始终可用，24x7x365 全天在线。你需要高可用性。将你的数据复制到第二和第三台服务器，每隔几分钟进行一次增量快照。现在，你的数据已准备好在 n+2 台热服务器上运行。现在使用其中一台位于远程位置的服务器，你就防止了整个设施被毁的风险。

所以，你那里的那份很不错的客户数据集。你想用它来测试计费系统的新版本。与其在同一台机器上克隆数据，你需要在开发环境中有一个完全独立的副本。无论目标是远程机器还是同一池上的新数据集，`ZFS` 复制都是拷贝数据最快、最可靠的方法。

你是否有几十个或数百个完全相同的机器、虚拟机或容器？使用 `ZFS` 复制将你完美制作的镜像部署到每处。如果你设计系统得当，甚至可以使用增量复制来部署更新。

复制还极大地简化了数据迁移，即使是跨越遥距离迁移海量数据。也许你必须将一个巨大的数据集迁移到另一端。

## 基础复制

`ZFS` 不复制数据集（`datasets`）。它复制的是快照。快照在复制过程中不会更改，因此可以保证内部一致性。首先为你的数据创建一个快照。

```bash
# zfs snapshot mypool/someata@snappycheckpoint
```

现在让我们在本地和远程主机上复制这个快照。

### 本地复制

`ZFS` 复制是单向的，这意味着它不需要接收方的反馈。在这里，你可以使用标准重定向和管道将快照导入任何其他程序。在这里我们将 `zfs send` 的输出馈到一个文件。（如果你添加了 `-v` 标志，`zfs send` 会打印进度摘要。）

```bash
# zfs send mypool/someata@snappycheckpoint > backup_file
```

这是我们第一次使用 `ZFS` 复制，所以它不是增量的。它包含了快照中的所有内容。它与数据集的大小相当。然而，它本身并没有什么用处——很少有人能在不将其转换为文件系统的情况下读取流文件系统。让我们用 `zfs receive` 将数据集接收回 `ZFS`。

```bash
# zfs receive mypool/copy < backup_file
```

`ZFS(8)` 从 `backup_file` 读取复制流并创建一个新的数据集，它是原始数据集的精确副本。

在本地复制中，你不需要中间文件。这是一个类 Unix 系统。我们拥有管道的奇迹。这台主机在根池上有主目录，但我正将它们移动到新池。

```bash
# zfs zroot/home@weds zfs receive mypool/home
```

我现在调整了几个数据集挂载点，并将主目录移动到新池。

`ZFS` 的单向性允许你复制任何可以被命令指向的对象，例如磁带。通过管道，你可以将 `zfs send` 倒入 SSH 并馈入 `zfs receive`，从而在远程机器上复制数据集。

# 查看副本

想查看流文件的内部内容吗？`zstreamdump(8)` 实用程序可以检查流并显示其细节。你可以检查文件，也可以直接从 `zfs send` 读取。

```bash
# zstreamdump < backup_file
```

`zstreamdump` 程序会为 `zfs send` 流中的每一个快照返回一个如下所示的部分：

```
BEGIN record
hdrtype = 1
toname = 4
features = 2f5bac
magic = 56a53713
type = 2
flags = 0x0
toguid = 4264598740125b
fromuid = 0
toname = mypool@somedata@snappycomeback
END checksum = 14035a47cfdef2/65a46eb5247f0/e70deff7d7456/9
```

该输出包含了大量来自 `zfs send` 流的信息。其中部分以易读的方式呈现。尽管如此，我们仍然从中提取一些信息。

`creation_time` 字段给出了 `zfs send` 执行的时间，以 Unix 纪元的秒为单位——当然是十六进制的。为什么不使用十进制呢？将此值 (`56a53713`) 转换为人类可读的值（使用 `date` 命令)。在值前面加上 `0x` 以将其识别为十六进制值。

```
$ date -0x56a53713
Sun Jan 24 15:41:55 EST 2016
```

在 FreeBSD 上，`date` 可能不接受十六进制值。虽然有很多转换方法，但你可以尝试这样做：

```
$ printf "%d\n" 0x56a53713 | xargs -r
```

每个快照都有一个易读的名字，位于 `toname` 中。此快照名为 `mypool@somedata@snappycomeback`，这说明了为数据集和快照使用意义名称的重要性。

流中的每个快照还有一个全局唯一标识符，即 GUID。此快照的 GUID 出现在 `toguid` 字段中。

`fromguid` 字段用于增量 `ZFS`（参见本文后面的“增量复制”），包含两个快照之间的更改。在本示例中为零，意味着该 `zfs send` 流包含一个完整的快照。它不是增量的。将 `zfs send` 流恢复到活动数据集是合理的（这取决于快照所的基础）。

如果流中包含多个快照——例如，通过递归 `zfs send`——你可以使用 `toguid` 和 `frag` 值来将快照组合在一起。然而，将 `zfs send` 流恢复到数据集并查看它。



每个部分以 `checksum` 结束。你无法使用校验和来手动验证此部分的快照，但知道 ZFS 使用校验和是件好事。

在打印每个快照的详情后，`zstreamdump` 会打印一个摘要。

`SUMMARY:`:

```
Total DRR_BEGIN records = 5
Total DRR_END records = 6
```

```
Total records = 170
Total write size = 69216 (0xa9200)
Total stream length = 65960 (0xa1b68)
```

摘要包含了大量的 ZFS 内部元数据。这里最有趣的部分是 `DRR_BEGIN` 记录数，它对应于流中的快照数量。结尾的大小单位是字节。`write size` 是流中包含的数据大小，而 `stream length` 是流本身的大小。`ZFS send` 流包含用于将数据恢复到磁盘的所需的元数据。

### 远程复制

为了将 ZFS 复制到远程主机，远程主机需要一个可以接受复制的用户以及通往远程主机的安全管道。最常见的安全管道类型是 SSH，因此我们将假设你的工具如此。从长远来看，使用 SSH 最简单的方法是基于密钥的认证。如果你不熟悉 SSH，请咨询许多在线教程或 Lucas 的《Mastery》(2)。你可以使用 root 账户来接收流，这意味着允许以 root 身份登录 SSH。以 root 身份 SSH 是一个坏主意。不要这样做。而且你真的希望互联网上某处的随机人员都能访问你所有的机器吗？同样，虽然你可以以 root 身份发送 ZFS 数据集，但你可能希望操作员或普通用户拥有发送能力。

# 复制用户和数据集

在发送和接收主机上，我们都创建一个专门复制的用户。我们的示例用户名为 `replicator`。它需要一个 shell，不需要特殊的组组成。

```
local pw user add replicator -m /bin/sh
remote pw user add replicator -m /bin/sh
```

在发送主机上，复制需要被发送数据集的 `send` 和 `snapshot` 权限。这里我们将这些权限赋予了 `home` 用户。

```
# zfs allow -u replicator send,snapshot zroot/user/home
```

发送用户需要一个 SSH 密钥对。发送和接收两端的用户都可以使用他们自己的密钥。对于专用账户，使用 `ssh-keygen(1)` 生成密钥对。

```
$ replicator@$ ssh-keygen
```

`ssh-keygen` 程序会提示你输入密码短。如果是为了自动化过程，请使用空密码。密钥文件位于用户主目录下的 `.ssh/id_rsa.pub`。我们还建议限制可以使用此密钥登录远程机器，以帮助防止密钥被盗。为了在远程机器上恢复该快照，你可以这样做：

```
$ cat ~/.ssh/id_rsa.pub | ssh user@remote "cat >> ~/.ssh/authorized_keys"
```

在接收主机上，由于接收主机需要一个可以接受复制的用户以及一个通往接收主机的安全管道。为了在接收主机上创建数据集，先创建一个快照。

```
$ zfs snapshot zroot/user/home/monday
```

现在使用 `zfs send` 传输此快照，通过 SSH 管道到 `zfs receive`。记住，由于是第一次复制此数据集，`zfs send` 流包含了快照的所有块。

```
$ zfs send zroot/user/home/monday | ssh user@host zfs receive remotool/backup
```

除了复制到另一个机器上的池，你还可以复制到同一个池或同一机器上的第二个池、到文件或到管道。复制到文件或管道对于备份（如磁带）或不同的文件系统很有用。

你可以让主机登录另一个主机来触发 `zfs send`，从而将 ZFS 复制从“推”改为“拉”。

```
$ ssh user@host zfs send zroot/user/home/monday | zfs receive remotool/backup
```

本书假设从本地数据集发送以保持一致性，但反向同样适用。

### 增量复制

真正的威力来自于增量复制。现在我们已经将数据集的所有数据复制到了 Monday，周二的复制只需要发送发生更改的块。命令的接收端完全不需要更改，但在发送端使用 `-i` 标志来指示最近的快照。

```
$ zfs snapshot zroot/user/home/monday
$ zfs send -i zroot/user/home/monday | ssh user@host zfs receive remotool/backup/home
```

现在查看接收系统上的数据集。

```
# zfs list -t snap -r zroot/backup
NAME USED AVAIL REFER MOUNTPOINT
zroot/backup/usr/home/monday 8K - 49.0M -
zroot/backup/usr/home/tuesday 0 - 49.0M -
```

显示两个快照。

增量备份的一个常见错误是没有指定远程系统存在的最后一个快照。如果你不指定最近传输的快照，将收到错误。

```
# zfs send zroot/usr/home/tuesday | ssh hotspot zfs recv remotool/backup/usrhome
cannot receive new filesystem stream: destination remotool/backup/usrhome' exists
specify -F to overwrite it
```

# 增量复制假设

磁带增量备份几乎是固定的：你可能会覆盖它们，但在21世纪，你不会直接在磁带上编辑文件。然而，磁盘增量备份则非常容易实现。

增量复制要求接收端的数据集副本在两次复制运行之间不发生变化。副本的更改会破坏整个过程。如果你编辑了数据集的备份副本，下一次增量更新将无法再次连接到该备份副本。如果你想在备份机器上编辑副本，请为接收到的数据集创建一个克隆并编辑该克隆。

如果有人无意或不知情编辑了副本，请将更改回滚到上一个快照。通过在 `zfs receive` 命令中添加 `-F` 参数，让接收端强制回滚到匹配远程快照。

```
# zfs send -I zroot/usr/home@today | ssh user@hotspot zfs receive -F remotool/backup/home
```

通过将被复制数据集的 ZFS 属性 `readonly` 设置为 `on` 来防止副本被修改。凭借之前赋予的权限，你可以向只写数据集添加快照。

```
#### zfs set readonly=on@remotpool/backup
```

你仍然可以在 `remotool/backup` 上添加快照。你可以检查数据集中的文件。但在不更改 ZFS `readonly` 属性的情况下，没有人可以编辑文件。任何拥有该访问权限的人要么应该明理，要么是迫切需要现在让该数据集上线，对吧。

### 差异复制

ZFS 复制可以在同一数据集的任何两个快照之间进行，因此你也可以进行差异备份。使用 `-I`（大写 i）而不是 `-i` 会发送两个快照之间存在的所有快照（注：原文此处为 -l，根据上下文及命令逻辑应为 -I）。

假设周二的快照复制因为随机网络问题失败了。在周三，你想通过周二和周三的快照同时发送。

```
# zfs send -I @monday zroot/usr/home@wednesday | ssh hotspot zfs recv remotool/backup/usrhome
```

现在现在有了周二的快照，尽管你从未显式发送过它。

具有备份经验的人会意识到，我们对“增量”和“差异”这两个词的使用方式与大多数备份软件略有不同。备份软件的设计是为了将块发送到磁带，并尽可能减少恢复文件时所需的磁带数量。我们可以发明一种新语言，可以去挖掘精确但不熟悉的词汇，或者我们可以对现有的语言进行稍微扩展。

# SSH 带宽限制

你可能会发现 SSH 连接对于你的需求来说不够快。那些需要每秒数百兆字节以上复制速度的人可能应该考虑外部安全解决方案，例如专用 VPN。在没有非常特定的修改的情况下，SSH 无法快速传输数据，因此请考虑 `mbuffer(1)`。

# 增量复制的复杂性

ZFS 复制是单向的，从发送端到接收端。发送端得不到接收端的反馈，允许转储流向几乎任何地方。这在选择增量复制和差异复制时变得非常重要。

增量备份（使用 `-i`）发送第一个快照和最后一个快照创建时间之间所有更改的块，而不会发送中间存在的快照。如果一个数据集在每周的每一天都有快照，`zfs send -i monday zroot/usr/home@thursday` 生成的流依赖于接收端存在 `@thursday` 快照，并且导致中间的快照不会被复制。



差异备份（使用 `-I`）的工作方式与增量备份完全相同，但它们会创建任何中间快照。类似 `zfs send -I monday zroot/usr/home@monday` 的命令要求远程端存在 `@monday` 快照，它会在执行过程中创建缺失的 `@tuesday` 和 `@wednesday` 快照。

假设你自动对数据集拍摄了每日快照，并想将它们发送到远程服务器。将 `@monday` 快照复制到远程池：

```
# zfs send zroot/usr/home@monday | zfs receive remotipool/usrhome
```

在你的远程主机上检查 `@monday` 快照是否存在。

```
# zfs list -t all -r remotipool/backup
NAME USED AVAIL REFER
remotepool/backup/usrhome 19.5K 472M 19.5K /remotepool/weekday
remotepool/backup/usrhome@monday 0 19.5K
```

现在我们增量复制 `@tuesday` 快照。

```
# zfs send -i remotepool/backup/usrhome@tuesday | zfs receive remotipool/backup
```

检查远程主机，你会发现快照。

```
# zfs list -t all -r remotipool/backup
NAME USED AVAIL REFER
remotepool/backup/usrhome 29K 472M 19.5K /remotepool/weekday
remotepool/backup/usrhome@monday 9.5K 19.5K
```

在周三，如果你是在闲逛——我的意思是，"出故障了"——所以你没有进行复制。周四，你想赶上进度，所以你对 `@thursday` 快照进行差异复制。

```
# zfs send -I tuesday zroot/usr/home@thursday | zfs receive remotipool/backup/usrhome
```

我们的备用主机现在有了快照。

```
# zfs list -t all -r remotipool/backup/usrhome
NAME USED AVAIL REFER
remotepool/backup/usrhome 19.5K 472M 19.5K /remotepool/weekday
remotepool/backup/usrhome@monday 9.5K 19.5K
remotepool/backup/usrhome@tuesday 9.5K 19.5K
remotepool/backup/usrhome@wednesday 9.5K 19.5K
remotepool/backup/usrhome@thursday 0 19.5K
```

等待，提示词中提供的 72-75 页的 OCR 文本在后期变得非常混乱。让我根据文本中提供的 ZFS 文档逻辑进行重新处理。

（注：提供的第 72-75 页 OCR 文本严重损坏且重复。我已根据可用文本提供了去重并清理后的版本。）

### 高级发送选项

发送者可以通过多种方式更改其发送数据集的方法。

#### 发送属性

若要发送数据集属性以及实际数据，请添加 `-p` 标志。当接收到的数据集属性与数据集上已有的属性不同时，`zfs receive` 会尝试更改属性以匹配它们。也就是说，如果你正在从一个使用 `l4` 压缩的数据集复制属性到一个已经使用 `l4` 的数据集，`zfs receive` 将不会对该属性执行任何操作。但是，如果发送者使用了 `gzip-9` 压缩，接收端将更改以匹配原始设置。

接收数据集的用户必须拥有设置你想要复制的属性的权限。如果用户具有复制权限，但没有所有属性的权限，则允许的属性会被设置，而不允许的属性将会被拒绝。

假设源数据集的 `dedup` 设置为 `on`，`compression` 设置为 `gzip-9`。接收的数据集的 `dedup` 设置为 `off`，`compression` 设置为 `l4`。我们希望被复制的数据集使用相同的压缩方式，但保留原来的 `dedup` 设置。我们允许我们的复制用户更改压缩设置。

```
#### zfs allow -u replicator zroot/backup
```

当我们发送数据集时，将会得到错误。

`cannot receive compression dedup on remotool/backup: permission denied`

这没关系——我们不想在副本上设置 `dedup` 属性。不过，`compression` 属性按预期进行了复制。

我们为什么要复制属性，而不是直接在目标上设置它们？对于压缩和去重等简单属性，手动配置可能还可以，但对于共享或任何配额等复杂属性来说并不适用。

#### 去重数据流

你的数据去重了吗？它适合去重吗？ZFS 允许你对数据流进行去重。通过 `-d`，每个唯一的块只会被发送一次。它不会改变接收者写入磁盘的内容，只会影响数据流。

去重的数据流使用与磁盘去重不同的去重内存集。如果你的数据可以被有效去重，但该去重使用了许多 GB 的内存，那么发送和接收主机都需要相似的内存来对数据流进行去重。不要在 `zfs send` 中轻率去重！

#### 调试与测试

`zfs send` 支持一些可以帮助调试、测试和监控的选项。

`-v` 选项让 `zfs send` 进入详细模式。它会打印关于要发送的数据的信息，并定期添加状态更新。

`-p` 标志在流开始流动时立即打印有关发送流的信息。手册将此类信息描述为“机器可读”。这些信息人类可以读懂，但不是整齐的表格形式。然而，它非常适合交给你的脚本。

`-n` 标志防止 `zfs send` 实际发送任何数据。相反，当与 `-v` 或 `-p` 结合使用时，它会提供 `zfs send` 如果实际运行将执行的操作统计。

#### 大块与小块

较新版本的 ZFS 通过 `large_blocks zpool(8)` 特性支持大于 128 KB 的磁盘块。`-L` 标志允许 `zfs send` 包含大块，而不是将其拆分为小块。接收端池也必须支持大块。

对于具有非常小块的主机，`-e` 通过使用 `embedded_data` 特性缩小数据流的大小。目标池也必须支持 `embedded_data` 特性标志。

#### 高级接收选项

接收端可以通过 `zfs receive` 的参数来调整其存储传入 ZFS 流的方式。

#### 路径与挂载管理

接收到的 ZFS 流包含了源的池和数据集路径。你可以保留此路径，也可以将其剥离。

通过添加 `-d` 标志，你 `zfs receive` 将使用源的完整路径（池名除外）作为目标数据集的路径，而不是要求管理员指定目标数据集。早些，我们将 `zroot:/usr/` 复制到 `remotepool/backup/usrhome`。在这里使用 `-d`，我们让 `zfs receive` 使用源路径。

```
# zfs send zroot:/usr/ | zfs receive -d remotepool/backup
```

这会创建 `remotepool/backup/usr`。如果不使用 `-d`，我们需要使用 `zfs receive remotepool/backup/usrhome`。

如果你想重命名接收到的数据集，可以使用 `-d` 剥离路径。

```
# zfs send zroot:/usr/home/ | zfs receive -d remotepool/backup
```

这会创建 `remotepool/backup/usr/home`。

## 回滚更改

如果有人更改了数据集，`-F` 标志会让 `zfs receive` 回滚到之前的状态。

```
# zfs send zroot:/usr/home | zfs receive -F remotepool/backup
```

mypool/weekday 96K 13.5G 96K /mypool/weekday

mypool/weekday@saturday 0 96K -

mypool/weekday#bm-friday - -

遗憾的是，书签（bookmarks）列在快照之后，即使它们比快照更旧。不过，ZFS 命令行非常强大。为了方便起见，让我们使用 `-t` 来告诉它只列出快照和书签。`-s` 参数告诉 `zfs(8)` 如何排序输出，因此我们将按照创建（创建日期）属性进行排序。在最大递归深度为 `1` 的情况下会忽略数据集的快照。

```
# zfs list -t snapshot,bookmark -s creation -d 1 zroot/usr/home
NAME USED AVAIL REFER MOUNTPOINT
zroot/usr/home#bm-friday - - -
zroot/usr/home@saturday 64K - 96K -
```



现在，使用 `bm-friday` 书签作为源快照，将 `@daily` 快照复制到远程主机。

```
# zfs send -i #bm-friday zroot/usr/home@saturday | ssh hotshare zfs receive remot/backup/usrhome
```

远程主机将 `@daily` 快照作为增量快照接收，即使源端不再有周五的快照。

```
# zfs list -t all -r remotool/usrhome
NAME USED AVAIL REFER MOUNTPOINT
remotool/backup/usrhome 58.5K 472M 19.5K /remotool/weekday
remotool/backup/usrhome@monday 9.50K - 19.5K -
remotool/backup/usrhome@wednesday 9.50K - 19.5K -
remotool/backup/usrhome@thursday 9.50K - 19.5K -
remotool/backup/usrhome@friday 1K - 19.5K -
remotool/backup/usrhome@saturday 0 - 19.5K -
```

书签允许我们从源池中删除快照以节省空间，但在目标池中保留它们，以便我们仍然可以引用文件的旧版本。

## 可恢复的发送 (Resumable Send)

仅仅 ZFS 让数据集复制变得简单，并不意味着现实世界会配合。随着数据集规模增大，某些瞬时网络问题破坏连接并中断流的可能性会增加。如果你在互联网上传输 40 GB 的数据流快要完成了，ISP 的两分钟断网就足以让你发火霆。不要去去找运营商报销；请改用可恢复的 `zfs send`，它可以让你恢复已中断的复制。可恢复的 `zfs send` 最于 2016 年初出现在 FreeBSD 10.3 中。

要让 ZFS 流变为可恢复，为 `zfs receive` 添加 `-s` 参数。

`mypool/from` 数据集需要几 GB 的大小。通过在 `zfs receive` 语句中添加 `-s`，我们使流变得可恢复。这是件好事，因为我们将用 `CTRL` 中断传输。

```
local# zfs snapshot mypool/from/resumeme
local# zfs send -v mypool/from@resumeme | ssh hotspot zfs receive -s remote
full send of mypool/from@resumeme estimated size is 2.00G
total estimated size is 2.00G
TIME SENT SNAPSHOT
17:12:43 279M mypool/from@resumeme
17:12:44 529M mypool/from@resumeme
17:12:45 786M mypool/from@resumeme
^
```

当然，由于 ZFS 复制是单向的，发送者并不知道哪些块最近被捕获并写入磁盘。如果没有可恢复功能，你必须重新开始传输。

在接收端，部分接收的数据集有一个新属性 `receive_resume_token`。发送者需要该属性的值来接上工作。

```
remote# zfs get -o value receive_resume_token remotop/to
```

`db9a171a3-c8789c6306400310a50ec5c306710e725`

现在使用 `-t` 标志提供该 token。你不需要包含源数据集，因为 token 包含了 `zfs` 发送的所有内容。添加 `-v` 可以输出更多传输详情。

```
local# zfs send -v -t 1db9a171a3-c8789c6306400310a50ec5c306710e7265
resume token contents:
version: 0
object = 0x35000
offset = 0x35000
bytes = 0x35630
guid = 0xc2374c4522d45
name = mypool/from@resumeme
full sent of mypool/from@resumeme estimated size is 2.16G
TIME SENT SNAPSHOT
17:38:20 263M mypool/from@resumeme
17:38:21 472M mypool/from@resumeme
...
17:42:04 2.16G mypool/from@resumeme
```

一旦 `zfs receive` 完成，该属性将为空。

```
# zfs get receive_resume_token remotool/to
NAME PROPERTY VALUE
remotepool/to -
```

如果你不恢复该发送，目标池将有一个不可用的不完整的数据集占用空间。使用 `-A` 删除它。

```
remote# zfs receive -A remotool/to
```

这将移除部分接收的流并释放空间。

## 自动化复制

每个人想要备份，但必须手动运行的备份不算备份，因为它们不会自动发生。当然，你会运行一两次，但某天会出问题，你几乎无法记得上次停在哪里。可靠的备份需要测试，但对于自动化我们有 `zxfer`。

`Zxfer(8)` 检查本地和远程数据集，确定哪些快照必须复制以同步数据集，并发送数据集。一旦从本地池中删除，它也可以从远程删除快照。FreeBSD 默认不包含 `zxfer`，但你可以通过 `pkg` 轻松安装。由于 `zxfer` 可以以推或拉模式工作，你只需要在一个系统上安装它。为了演示，我们将在所有节点上安装。

```
#### pkg install zxfer
```

`zxfer` 命令不支持书签或可恢复复制。它也不设置复制账户。你必须配置这些账户、创建 SSH 密钥，并像普通复制一样设置权限。

### 使用 zxfer

我们所有的复制示例都使用了推（push）模式；具有当前数据集的主机将其推送到复制目标。我们将类似地使用 `zxfer` 登录拉（pull）模式。`Zxfer` 要求你声明是要复制单个数据集还是数据集及其所有子集。`-R` 标志启用递归，而 `-N` 表示单个数据集及其快照。对于备份，递归模式几乎总是正确的。你也可以添加 `-v` 进入详细模式。

```
$ zxfer -v -T user@host -R localhost remotep
```

如果两边的账户相同，你可以跳过用户标识；它们不能与不需要标识的参数组合。你可以使用 `-v -T user@host`，但 `-VT user@host` 会让 `zxfer` 抱怨。要记住的一点是，接收 `zxfer` 参数的是 shell 脚本，它使用 `getopt(1)` 处理命令行参数，而不是更复杂的程序中提供的特殊选项处理。

在这里我们将 `zroot/somedata` 数据集复制到远程的 `remotool/backups` 池中。

```
local$ zxfer -T replicator@remote -R mypool/somedata remotool/backups
```

如果你添加 `-v` 进入详细模式，你会看到 `zxfer` 正在传输每个快照。

+   - Sending zroot/somedata@snappycomeback to remotool/backups/somedata.

- Sending zroot/somedata@reply to remotool/backups/somedata.

- (incremental to zroot/somedata@snappycomeback).

- Sending zroot/somedata@more to remotool/backups/somedata.

- (incremental to zroot/somedata@reply).

一旦 `zfs` 退出，远程主机拥有了所有快照。

```
remote$ zfs list -t all -r remotool/backups
NAME USED AVAIL REFER MOUNTPOINT
remotepool/backups/somedata 10.1M 15.0G 10.1M /remotepool/ba
remotepool/backups/somedata@snappycomeback 8K 10.1M
remotepool/backups/somedata@reply 8K 10.1M
remotepool/backups/somedata@more 8K 10.1M
```

这些快照的进一步复制可以以推模式或拉模式运行。让我们接下来尝试拉模式。

### Zxfer 拉模式

在拉模式下，`zxfer` 通过 SSH 登录远程机器并运行 `zfs send` 将快照传回给运行 `zxfer` 的主机。使用 `-o` 标志配合登录和主机来指定所有池。一切都是一样的。

```
$ zxfer -O @user@host -R localpath remotep
```



现在在源池上创建一个额外的快照。

```
local$zfs snapshot pool/somedata@new
```

在目标机器上，运行 `zxfer` 来拉取快照。在这里我们添加了 `-v` 来显示更多真实发生的情况。

```
remote#zxfer -v -O replicator@local -R zroot/somedata remotepool/back
```

### 轮快快 (Rotating Snapshots)

如果你一直发送快照，远程池最终会填满。你可能想要删除源机器上不再存在的远程快照。使用 `-d` 来实现此操作。从删除旧快照开始。

```
local# zfs destroy zroot/somedata@reply
```

使用 `-d` 标志从目标端清理任何已删除的快照：

```
local$ zferfer -vd -T remote -R zroot/somedatemepool/backup
```

在详细模式下，`zxfer` 会显示每个数据集以及它创建的数据集。

正在删除快照 `remotepool/somedata@reply`。

你可以眼睁睁看着匆忙输入的错误命令销毁了你心爱的数据。

### 保留旧快照

常见的快照方案要求每 15 分钟创建一次快照，然后每小时、每天、每周和每月创建一次。（我们在 *FreeBSD Mastery: ZFS* 中讨论了这种旋转方案）。主机在几小时后丢弃 15 分钟的快照，在几天后丢弃小时快照，以此此类推。你希望在远程主机上丢弃这些 15 分钟的快照，但你可能希望在源删除它们后，让远程主机保留某些快照。我们中的许多人想保留每周或每月的快照作为长期备份。

`-g` 标志允许你通过一个天数的参数来保护最旧的备份。例如，`-g 375` 告诉 `zxfer` 不要删除 375 天或或更早的快照。

假设你想保留所有的月度快照，但自动删除任何从源端删除的其他快照。源端在三个月后删除月度快照，在六周后删除每周快照。六周是 42 天。再为系统异常多留出一周，设置 `-g 50` 将告诉 `zxfer` 不要删除任何 50 天或或更早的快照。

```
local$ zxfer -vd -g 50 -T remote -R zroot/somedatemepool/backup
```

最终，你的备份池将会填满。你必须进去清理掉那些老到已经不再有用的快照。这与清理公司的磁带柜没有区别。

### 属性与灾难恢复

你通常会想要复制复杂的属性，例如 `sharenfs` 和任何配额（`quotas`）。`-p` 参数告诉 `zxfer` 将目标端的属性设置为与源端匹配。

在某些情况下，你想知道属性是什么，但你不想在复制时立即恢复它们。`zxfer` 命令可以将数据集属性复制到文本文件中，让你稍后从该文件恢复。

`-k` 标志告诉 `zxfer` 在副本的根目录下创建属性文本文件。该文件名为 `.zxfer_backup_info`，后面跟着一个句点和池名称。如果你正在将一个整个主机 `web5` 的 `zroot` 池复制到备份主机上的 `remotepool/web5`，那么属性备份文件将位于 `remotepool/web5/.zxfer_backup_info.zroot`。

使用 `-e` 标志从此文件中恢复数据集和池属性。

一种常见的配置是让主机留出一个池来接收备份，然后留出另一个池用于灾难恢复。如果源机器坏了，你可以在本地使用 `zxfer` 将最新的备份复制到灾难恢复池。你可以在 `zxfer(8)` 手册页中找到完全一致的例子，但这里有一个常见的例子，包括恢复属性。我正在将主机 `web5` 的备份恢复到一个同样名为 `web5` 的池中。

```
# zxfer -defP -R remotepool/web5/ web5
```

从新的 `web5` 池启动，你就恢复了服务！

### Zxfer 选项

`zxfer` 程序有一系列选项来处理各种棘手的情况。

如果你有复杂的 SSH 设置，你可能需要在 `zxfer` 用户的 `$HOME/.ssh/config` 中设置一些客户端选项。或者，你也可以在单个 `-o -t` 中添加这些选项。

`-o` 和 `-T` 标志也可以用于注入 SSH 选项以及命令行参数。在用户和主机之前的额外参数将为 `zfs(8)` 命令添加前缀。（不过，使用 `sudo` 配置 ZFS 数据集权限对你更有帮助。）

```
-O 'port=1022 -i /path/to/key/file replication@hotspot'
```

`-f` 标志告诉 `zfs receive` 回滚所有被复制的数据集。如果你更改了被复制的数据集，`-f` 将彻底抹掉那些更改。

你可以让 `zxfer` 在运行前自动拍摄快照。它不会删除快照，因此它不是一个真正的快照旋转方案。然而，它适用于即时备份，只是将清理问题留到了另一天。添加 `-s` 让 `zxfer` 对每个复制的数据集拍摄快照。

最后，`-n` 标志触发空操作（no-op）模式。`zxfer` 程序不会传输或删除任何快照。相反，它会执行分析并打印出如果你没有设置 `-n` 它将做什么。

既然你已经过过了复制，相比之下，ZFS 卷的问题应该看起来简单了。或者，也许并没有……

- 1 在你的 IT 员工中安排地理上的高可用性是一个独立的问题。我们建议让大家居家办公。为了获得最佳效果，在斐济岛和塞舌尔群岛等地方为他们买房。把那个不受欢迎的人困在阿拉斯加州的穆斯伯普（Moose Base）。
- 2 那些能够在不将文件系统转回文件系统的情况下读取流文件系统的人，对时间有更好的利用。
- 3 系统管理员可能会将发生的任何一次问题归咎于“随机网络问题”。这在行为准则中是有规定的。
- 4 Lucas 会发现让你编造一个符合 ZFS 的晦涩单词是巨大的乐趣。

## 卷模式 (Volume Mode)

在为应用程序创建卷之前，请考虑它的预期用途以及哪些主机将访问它。FreeBSD 默认的 ZFS 设置假设托管 zvol 的系统完全控制着它。然而，如果你将 zvol 用作虚拟机的存储器，那么客体操作系统对其拥有完全控制权。这很重要，因为 FreeBSD GEOM 层会自动配置存储。已经由主机配置好的存储会给虚拟化客端系统带来问题。

使用 `volmode` 属性来控制由哪个系统配置卷。

默认的 `volmode` 为 `geom`，意味着卷所在的系统对其进行控制。如果我们在主机 A 上创建一个 zvol，则主机 A 将通过 GEOM 配置并管理该卷。除了 ZFS 卷的设备节点外，它还会在 `/dev/label1/` 等类似位置（注：原文为 /dev/label1）获取设备节点。在本地使用 zvol 时，请使用 `geom volmode`。

> `volmode` 表示该 zvol 仅通过 `/dev/zvol` 中的单个设备节点可用。GEOM 不会尝试自动配置此卷。你可以为该节点分配标签，但 FreeBSD 甚至不会尝试查看它。对于虚拟机存储（如 `bhyve(8)` 主机），请使用 `dev volmode`。

`volmode` 表示该 zvol 甚至不会获得设备节点。你可以对此卷进行克隆、快照或复制。这种模式仅对备份有用。

你无法更改正在运行的 zvol 的模式——虽然你可以更改 `volmode` 属性的值，但该卷的实际模式不会发生改变。要让 `volmode` 的更改生效，请导出（export）并重新导入（import）该卷。（你也可以重命名卷，这实际上相当于导出该卷并在不同的名称下导入它）

通过在命令行指定模式或设置全局默认值来创建具有所需模式的卷。

### 命令行中的 volmode

与任何其他属性一样，在创建 zvol 时使用 `-o` 标志来设置 `volmode`。

```
#### zfs create -V 10G -o volmode=dev vm/swap0
```

这个新的 zvol 仅可以通过设备节点 `/dev/zvol/vm/swap0` 访问。

### 默认 volmode

如果一个主机经常需要使用 `geom` 以外的 `volmode`，那么更改默认 `volmode` 是合理的。`sysctl vfs.zfs.vol.mode` 控制新 zvol 的默认 `volmode`。

默认值 `1` 告诉 ZFS 使用 `geom` 模式。设置为 `2` 表示 `dev` 模式，而 `3` 则表示 `none` 模式。使用 `sysctl(8)` 修改默认值，或通过 `/etc/sysctl.conf` 中的条目使更改在下次重启时永久生效。这里有一个 `/etc/sysctl.conf` 条目，用于让虚拟化服务器创建模式为 `dev` 的新 zvol：`vfs.zfs.vol.mode=2`

不需要显式定义 `geom` volmode。

### 访问 zvol

你不能像挂文件系统数据集那样 `zfs mount` 一个 zvol。zvol 的意义在于它是一个块设备。要访问它，必须访问设备节点或其 GEOM 提供者。最可能是设备节点。



zvol 会在 `/dev/zvol/` 下以池命名的子目录下获得一个设备节点。我们示例 zvol `vm/db1` 的设备节点将是 `/dev/zvol/vm/db1`。

我们可能会将此 zvol 存储分配给 bhyve 虚拟机，在这种情况下，我们可能会让虚拟机对磁盘进行分区。

对于其他用途，我们可能想在本地对其分区。在这里，我们在 zvol 上创建一个 GPT 分区方案，并使其作为一个大分区，带有 `db1` 的 GEOM 标签。我们还为它分配了一个 GEOM 标签。

```
#### gpart create -s g /dev/zvol/vm/db1
zvol/vm/db1 created
#### gpart add -t freebs-ufs -1 db1 /dev/zvol/vm/db1
zvol/vm/db1p added
#### glabel db1 /dev/zvol/vm/db1
```

由于此 zvol 是用默认的 `volmode` (`geom`) 创建的，它现在也可以通过设备节点 `/dev/label/db1` 访问。

一旦分区存在，你就可以在其上创建文件系统。

```
#### newfs -j /dev/zvol/vm/db1
/dev/zvol/vm/db1: 2097152.0MB (4294967296 sectors) block size 32768, fragment using 3350 cylinder groups of 626.9MB, 20035 blks, 80256 inodes.
with soft updates
```

等一下——我们为什么可能要在 zvol 上使用 UFS 呢？

也许我们的 iSCSI 客端或虚拟机虚拟机没有资源来有效运行 ZFS。通过为客端提供带有其可以支持的文件系统的 ZFS 支撑卷，客端可以获得 ZFS 的额外保护，即使客端无法直接使用 ZFS。然而，我通过 `-j` 启用了 UFS 软更新日志，因为 ZFS 的数据完整性与 UFS 文件系统日志保护的是完全不同的内容。ZFS 完整性检查确保了写入是安全的，而文件系统日志则验证所有写入都已完成。

现在 zvol 有了文件系统，你就可以挂载它。

```
#### mount /dev/gpt/db1 /media/
```

大功告成！我有一个由 ZFS 支持的 UFS 文件系统，准备可以使用。

zvol 最常见的用途是作为虚拟机的后端存储。...（注：此处提供的原始文本后半部分似乎出现了大量乱码或重复的无意义字符，已根据指令翻译了前半部分并在此处逻辑结束）

SAS 扩展器变得稍微复杂了一些。你会看到 SAS 扩展器的条目，然后是扩展器内部的所有组件。SAS 扩展器几乎不会出错，但某些组件确实提供了状态显示。

- Element 41, Type: SAS Expander
- Status: Unsupported (0x00 0x00 0x00)
- Description: SAS Expanders
- Element 42, Type: SAS Expander
- Status: OK (0x01 0x00 0x00)
- Description: Primary Expander
- Element 44, Type: SAS Connector
- Status: OK (0x01 0x11 0xff)
- Description: Upstream Connector (Primary)
- Element 45, Type: SAS Connector
- Status: OK (0x01 0x11 0xff)
- Description: Downstream Connector 1 (Primary)
- Element 46, Type: SAS Connector
- Status: OK (0x01 0x11 0xff)
- Description: Downstream Connector 2 (Primary)

即使是单个连接器也会显示出来

- Element 47, Type: SAS Connector
- Status: OK (0x01 0x20 0x00)
- Description: Drive Connector 00

这些细节比我们需要的要多得多。但在开始批量更换硬盘之前，检查你的 SAS 扩展器和控制器的状态可以节省你很多痛苦。

## 封闭路径 (Closure Path)

你可以通过连接方式来描述磁盘在机箱中的位置。要访问特定的磁盘，操作系统必须进入某个机箱，进入该机箱的某个槽位。FreeBSD 根据此路径自动生成设备节点目录。这允许系统管理员识别特定硬件块的设备。此设备路径是一系列键值对，由 `@` 符号分隔。例如，机箱 `500304801786b87d` 显示为 `enc@n500304801786b87d`。每个路径都包含组件：机箱、设备类型、槽位，然后是创建如下所示路径的元素描述。

```
/dev/enc/n500304801786b87d/type@0/slot@a/elmdesc/Slot_10/
```

此设备代表机箱 `500304801786b87d`。机箱前面的 `N` 标识表示这是一个网络寻址权威 (NAA) 标识符，这在很大程度上是冗余，因为这里的所有内容都是 NAA 标识符。十六进制数是被寻址逻辑单元（Address Logical Unit）的 SAS 地址。这个数字的确定方法取决于供应商。

`type` 是数字设备类型。磁盘是该驱动程序目前支持的设备，但后续 FreeBSD 版本可能会增加对其他设备的支持。

`slot` 是硬盘槽。槽位使用十六进制进行编号：`slot a` 是 10，`b` 是 11，以此此类推。Slot 10 实际上是 16。

最后一个组件是元素描述，当运行运行 `sesutil map` 时出现。

此目录包含指向与此槽位相关的所有设备节点的符号链接。它包含标签子目录（你正在使用标签管理磁盘，对吧？）

```
# ls -l /dev/enc@n50030480178BB8D7/type//@slot/elmdesc@Slot_10/
total 1
lwxr-xr-x 1 root wheel 15 Oct 5 23:27 da9@ -> ../../../da9
dr-xr-x 2 root wheel 512 Oct 5 23:27 gpt/ ->
lwxr-xr-x 1 root wheel 18 Oct 5 23:27 pass13@ -> ../../../pass13
```

如果你的机箱上的第 15 槽发出异常的嗡嗡声，你可以进入基于机箱的设备节点并识别哪个指示灯亮着。

## 保持指示灯开启 (Keeping the lights on)

你的硬件维护人员需要尽可能的帮助。那些槽号可能是用 6 号字体打印的，只有当你把硬盘从槽位取出时才可见。紧急硬盘更换总是发生在现场团队几乎意识不清的时候。

机箱槽位有特定的定位灯（locate lights），为你的远程人员提供额外线索。使用 `sesutil locate` 激活槽位灯。在这里，我们激活了驱动 `da2` 的槽位的灯。

```
#### sesutil locate da2
```

指示灯会亮起或闪烁，取决于制造商。

`sesutil map` 命令显示某个槽位的定位灯已开启。

```
#### sesutil map
...
Element 3, Type: Array Device Slot
Status: OK (0x01 0x00 0x02 0x00)
Description: Slot 03
Device Names: da2,pass6
Extra status:
- LED=locate
```

你可能需要在一个没有硬盘的槽位中激活定位灯——例如，告诉技术人员在哪里安装新硬盘。使用 SES 设备节点和元素编号，而不是设备节点。槽号通常（但并非总是）与元素编号相同。请小心。

在这里我们激活了机箱 `/dev/ses0` 上元素 3 的定位灯。

```
#### sesutil locate -u /dev/ses0 3 on
```

要关闭定位灯，运行相同的命令，但将 `on` 替换为……等一下……`off`。

## 控制主机适配器 (Controlling Host Adapters)

FreeBSD 包含了几个用于管理非 RAID 硬盘控制器（通常称为主机适配器或 HBA）的工具。对于旧的控制器，你可能更倾向于使用 `mpsutil` 和 `mpr`。FreeBSD 10.3 拥有 `mpr` 和 `mpsutil`。`mpr` 用于 LSI Fusion-3 HBAs，而 `mpsutil` 用于 LSI Fusion-2 HBAs。（由于 Avago 收购了 LSI，你可能看到带有 Avago 品牌的卡。）这两个程序的行为相同。`mpsutil` 展示。

### 适配器详情 (Adapter Details)

首先，找到连接到系统的适配器。

```
#### mpsutil show adapters
Device Name Chip Name
/dev/mps0 SAS2308 130000
/dev/mps1 SAS2308 130000
```



现在查看所有连接的设备。两个工具默认访问第一个设备节点 `/dev/mps0` 或 `/dev/mpr`。使用 `-u` 标志和设备编号访问其他 HBA 设备。

| SAS Address | Handle | Parent | Speed | Slot | Wdt |
|---|---|---|---|---|---|
| 00 | 08 | 5000ca2235ddd0a | 00a | SAS Target | 6.0 | 0002 | 0 |
| 00 | | 5000ca2235ddd0a | 00a | SAS Target | 6.0 | 0002 | 1 |
| 00 | 09 | 5000ca2235d2719d | 00b | SAS Target | 6.0 | 0002 | 1 |
| 00 | 10 | 5000ca2235dbbd0 | 00c | SAS Target | 6.0 | 0002 | 2 |
| 00 | 11 | 5000ca2235e028d | 00d | SAS Target | 6.0 | 0002 | 3 |

每一行都是响应 SCSI 命令的设备。大部分是硬盘。任何位于 SCSI 总线上的都是目标（target）。深入研究这些需要对 SAS 和 SCSI 有了解，但即使没有深厚的知识也可以获取有用信息。前两列显示设备的 SCSI 风格地址。第三列给出设备的物理地址。类似于以太网卡，每个 SAS 设备都有唯一的 `Handle` 列指示设备名称，而 `Parent` 列显示该设备连接到哪里。看我们的第一行。它的 handle 是 0009。第二列 parent 是 0009。第二行的设备连接到第一行的设备。

`Device` 列显示这是什么设备。“SAS Target”是“硬盘”的一种高级说法。SMP（串行连接管理协议）目标是 SAS 交换机或扩展器。`Speed` 列显示每秒 GB 的连接速度。`Enc` 列显示机箱，而 `Slot` 列显示槽位。最后 `Wdt` 列显示该设备上的端口连接数。

### 显示机箱

使用 `show enclosures` 命令查看连接到 HBA 的机箱。在这里我们列出了连接到 `/dev/mps1` 的机箱。

```
mpsutil -u 1 show enclosures
Slots Logical ID SEPHandle EnchHandle Type
08 500605b009d018c 0001 Direct Attached SGPIO
25 500304801786b87f 0022 External SES-2
13 5003048001f7ab3f 0003 External SES-2
```

你会看到机箱中的槽位数量、设备的句（如果有）以及机箱的类型。逻辑 ID 是 SAS 地址。你可以将这些映射到 `sesutil(8)` 或其他命令显示的 SAS 地址。

## sas2ircu

如果你使用的是没有 `mpsutil` 的旧版本 FreeBSD，或者需要它没有提供的功能，LSI/Avago 提供了他们自己的专有工具 `sas2ircu(8)`。`mpsutil(8)` 缺少控制器内置软件 RAID 功能。`sas2ircu(8)` 还可以让你获取有关 HBA 固件版本的信息。它作为 FreeBSD 端口 `sysutils/sas2ircu` 提供。

`sas2ircu` 程序期望至少两个参数：控制器（设备节点）编号和命令。即使你只有一个控制器，也必须指定控制器编号。

### 查看硬件

要查看连接到 HBA 的硬件，使用 `display` 命令。在这里我们查看连接到控制器 0 `/dev/mps0` 或 `/dev/mps0` 的设备。

```
sas2ircu 0 display
```

你会得到大量的版权信息，以及像这样的有用的注释：

已启动控制器 0 的配置读取

或者，“现在按照你的要求执行该操作。”

```
Controller information

Controller type         : SAS2308_2
BIOS version            : 7.37.00.00
Firmware version        : 19.00.00.00
Channel description    : 1 Serial Attached SCSI
....
```

BIOS 和固件版本在需要故障排除或使用制造商技术支持时非常有用。过了所有这些，我们获取了实际硬件的信息。每个硬盘都有这样的一个条目。

### 物理设备信息

```
Initiator at ID #0

Device is a Hard disk
Enclosure #           : 1
Slot #                : 0
SAS Address            : 4433221-1-0300-0000
State                 : Ready (RDY)
Size (in MB)/(sectors)  : 4769307/976541167
Manufacturer         : ATA
Model Number          : TOSHIBA MD0ACA5
```

固件版本：FP2A

序列号：55FGK5SUFS9A

GUID：无

协议：SATA

驱动器类型：SATA_HDD

你可以看到序列号、驱动器类型、硬盘是否准备就绪、大小等信息。

一旦遍历完所有硬盘，它将列出关于机柜本身的详细信息。

#### 机柜信息

机柜编号#：1

逻辑 ID：500605b0:09cfc82

槽位数量：8

起始槽位：0

这并不完全是你机柜的所有信息——它无法告诉你是哪块硬盘产生了焦糊味——但它提供了指导建议。

#### 定位指示灯

要开启或关闭特定硬盘槽上的 LED 灯，你需要控制器编号、机柜编号和槽位号。通过 `display` 命令获取所有这些信息。

```
sas2ircu <controller#> Locate <enclosure#:slot#> on
```

假设我们想要激活上一节所示机柜上 8 号硬盘的 LED 灯。我们使用的是控制器 0，即 `/dev/mps0`。`display` 命令显示每个设备的机柜编号和槽位号。8 号硬盘位于槽位 7——记住，槽位通常从 0 开始计数。因此，要在 `/dev/mps0` 上闪烁 8 号硬盘（上述）的 LED 灯，你需要运行：

```
sas2ircu 0 locate 1:7 on
```

完成后再次将其关闭。

## SAS 多路并发

具有高可用性需求且配备大量磁盘的系统可能需要 SAS 多路。多路的目标是提供 CPU 到每块磁盘的单条路径。其他路径可以用于负载均衡或故障转移。通常，多路意味着将两个或多个控制器连接到包含磁盘的背板或存储架。

### 为什么需要多路？

当每块硬盘都可以通过任何控制器访问时，单个控制器或电缆的故障不会中断服务。此外，它允许你使用所有控制器的总带宽。

这个概念甚至可以扩展到完全的高可用性。如果你有一个装满硬盘的 JBOD 机柜，将一个 SAS 端口连接到第一台服务器，另一个连接到第二台服务器。现在两台机器都可以访问这些磁盘。使用类似 CARP（许多心跳域之一）或某些基于仲裁的高可用性服务，让这两台服务器共享一个 IP 地址。

由于两台机器都拥有所有数据的权限，你可以在机器之间优雅地切换服务。这让你能够完成一直推迟的操作系统升级，而无需关闭文件服务器。

需要格外确保两个系统不会尝试同时挂载磁盘。这就是为什么 `zpool import` 命令会检查主机 ID，并拒绝导入看起来被另一个系统使用的池。

### 多路模式

多路带来了一个有趣的问题。如果你的每块硬盘都有两条或更多通往 CPU 的路径，操作系统会多次看到每个独立的磁盘，通过每个控制器看到一次。现在，我那 36 块硬盘的系统突然变成了 72 块磁盘。

GEOM 多路模块 `gmultipath(8)` 获取这些多路径并为操作系统提供单一的逻辑存储设备。`gmultipath(8)` 会自动选择到达磁盘的最佳路径，因此上层无需担心这个问题。

GEOM 多路目前支持三种运行模式：活动/被动、`active/passive`、活动/活动 `active/active` 和活动/只读 `active/read`。

活动/被动模式一次只使用一条路径。当路径失败时，系统会在下一条路径上重新发出命令。使用 `-P` 指定活动/被动。

活动/活动模式同时使用所有路径以增加可用带宽。使用所有路径有时实际上会损害性能。活动/活动模式不知道文件系统或应用程序级别正在发生什么；它将指令分散到不同的控制器上。相互依赖的命令可能需要等待另一个控制器的响应才能继续。使用 `-A` 指定活动/活动模式。



活动/只读模式使用所有路径进行读取，但通过主路径进行所有写入。这种混合方法解决了使用活动/活动模式可能引入的写入顺序问题。这种模式可以通过提供更多的控制器带宽来饱和 SSD。对于普通的旋转硬盘，随机 I/O 性能可能不如活动/被动。使用 `-R` 指定活动/只读。

第四种模式逻辑块（logical block）正在研究中，但尚未可用。逻辑块模式将磁盘划分为指定大小的块，并始终使用相同的路径访问该区域。这可以避免缓存重复，因为磁盘区域不会被两个控制器访问。这还可以解决写入排序问题，并预计性能优于活动/活动模式。

### 识别磁盘

配置多路中最麻烦的部分是识别哪些设备节点（`/dev/dax`）代表相同硬件的不同视图。在给磁盘添加任何标签之前，必须解决这个问题。解决此问题的方法是在 SAS 设备上使用 `camcontrol(8)` 获取序列号。

```
#### camcontrol inquiry da7 -S
EHNLRC
#### camcontrol inquiry da43 -S
EHNLRC
```

编译设备及其序列号列表，并找到匹配项。

或者，你可以使用 `sesutil(8)` 来匹配槽位号。我们以 Jude 的多路系统作为示例。它有两个机柜：前面的机柜将一个 SAS 端口连接到第一台服务器，另一个连接到第二台服务器。现在两台机器都可以访问这些磁盘。

| multipath/f00-1EHM9MC OPTIMAL da0 (ACTIVE) da36 (PASSIVE) |

| multipath/f01-1EHJZMBC OPTIMAL da1 (ACTIVE) da37 (PASSIVE) |

| multipath/f07-1EHNLWRC OPTIMAL da7 (ACTIVE) da43 (PASSIVE) |

在每个路径之后，你将看到一条注释，指示每个设备节点是激活（active）还是被动的（passive）。

### 更改多路径模式

我们之前讨论了不同的多路径模式及其对性能的影响。当你标记磁盘时，`gmultipath` 默认使用激活/被动模式 `-P`。你可以添加 `-A` 来触发激活/激活（active/active），或者添加 `-R` 切换到激活/读取（active/read）。

你也可以使用这些标志来更改现有多路径设备的模式。使用 `multipath configure`、所需模式的标志以及磁盘的 `gmultipath` 标签。在这里，我们将标记为 `f07-1EHNLWRC` 的磁盘切换到激活/读取模式。

```
#### gmultipath configure -R f07-1EHNLWRC
是否执行成功？
#### gmultipath status
```

| multipath/f07-1EHNLWRC OPTIMAL da7 (ACTIVE) da43 (READ) |

在激活/被动和激活/读取配置中，你还可以使用 `rotate` 命令来切换哪个设备为激活状态。

```
#### gmultipath rotate f07-1EHNLWRC
#### gmultipath status
```

| multipath/f07-1EHNLWRC OPTIMAL da7 (READ) da43 (ACTIVE) |

现在，即使是 SSD 也可以旋转。尽情享受吧！

提到 SSD……

## SSD

固态硬盘（或 SSD）与普通的旋转驱动器显著不同，其要求也与传统磁盘完全不同。其一，它们甚至不是磁盘。

对于旋转驱动器要读取磁盘上不同位置的两个扇区，读头必须定位到正确的位置，等待旋转盘片转到正确位置，读取扇区，然后重新定位到第二个扇区，再次等待盘片转到正确的偏移量，然后读取第二个扇区。这种等待被称为*寻道时间*（seek time）。

SSD 没有移动部件。当你从驱动器的两个不同部分读取数据时，驱动器的寻道时间为零。大多数 SSD 获得较高的读写速度是因为它们并发地读写多个存储单元。为了保持多个内存单元处于忙碌状态，操作系统必须向驱动器提供一个待完成的任务队列。

对于一个普通的旋转驱动器来说，拥有“深度”队列是有害的。这意味着请求数据到写入或返回数据之间的时间较长，因为必须等待队列中前面的工作完成。通过较低的队列深度，更重要的任务项可以到达队列前端，插在正在排队等待的次要任务之前。然而，要充分利用 SSD 的性能，队列深度必须足够高，以确保每个单元都能分配到工作。如果没有满队列，你就无法获得包装盒上吹嘘的性能。

与位于盘片上固定位置扇区的旋转磁盘不同，SSD 是一个不可移动闪存单元阵列。SSD 使用 FTL（闪存转换层）将磁盘上的逻辑位置映射到包含存储数据的特定闪存单元。虽然 SSD 声称拥有与旋转磁盘器相同的逻辑块地址（LBA），但 FTL 为它们提供了这些 LBA。SSD 上的 LBA 与旋转磁盘相比与现实的关系更小。

由于闪存单元会磨损，几乎所有 SSD 包含的存储空间都比盒上声称的多。驱动器将数据分散在单元中，以便磨损更均匀。一旦所有空间被占用，垃圾回收程序就会运行。垃圾回收程序找到不再被引用或操作系统通过 TRIM (SATA) 或 UNMAP (SCSI) 命令标记为未使用的单元，并清除它们供后续使用。

当你将 SSD 或支持 TRIM 的其他设备添加到 ZFS 池时，FreeBSD 默认会对整个分区或设备进行 TRIM 操作，使其从已知状态开始。这可能会导致驱动器在使用之前出现几分钟甚至几小时的延迟。如果你的设备是新的，或者你不想在将它们添加到池时对其进行 TRIM，请在将设备添加到池之前，将 `sysctl vfs.zfs.vdev.trim_on_init` 设置为 0。

## NVMe

非易失性内存表达式（或 NVMe）是一种较新技术，旨在进一步提高固态存储速度。它用于闪存驱动以及其他非易失性内存如 Intel 的 3D Xpoint。NVMe 本身是一种物理接口规范，是 SATA 或 SCSI/SAS 的替代方案。你会发现连接 PCI-e 总线的 NVMe 线缆和适配器。

SSD 最慢、最复杂且容易出错的部分是 FTL。假装得像 1980 年代的旋转磁盘一样真是一项苦力活。NVMe 通过放弃这种笨拙的伪装，转而采用闪存内存协议提高了性能。

NVMe 设备与 SSD 之间最大的区别之一是 NVMe 设备具有多个队列，通常每个 CPU 有一个读队列和一个写队列。与其试图保持一个包含足够占据多个单元任务的单队列，NVMe 拥有多个队列。NVMe 队列可以保持较浅，以允许高优先级任务取代旧工作。将负载分散到各个 CPU 上有助于获得更强大的性能。

虽然 HDD 和 SSD 使用 AHCI 接口（AHCI 每个设备具有 64 个命令的单队列），但 NVMe 接口允许多达 65536 个队列。NVMe 接口需要更少的锁同时提供了更大的并行性。FreeBSD 的 `nvme` 驱动出现在 9.2 版本。像硬盘一样，你可以预计第一个 `nvme` 设备是 `/dev/nvme0`，第二个是 `/dev/nvme1`，依此类推。NVMe 原生支持命名空间，允许将其划分为逻辑命名空间，类似于分区。与计算一切不同，NVM Express 规范从 1 开始命名空间。只有较新的 NVMe 设备支持管理空间。当前设备只有一个命名空间。

### 查看 NVMe 设备

使用 `nvmectl` 管理 NVMe 设备。首先列出连接到系统的 NVMe 设备。

```
#### nvmectl list
nvme0: INTEL SSD800G
nvme0ns1 (763097MB)
```

此主机有一个单命名空间的 NVMe。使用 `nvmectl identify` 命令学习设备的特定信息。

```
#### nvmectl identify nvme0
Controller Capabilities/Features
Vendor ID: 8086
Subsystem ID: 8086
Serial Number: CFT403004A80CG
Model Number: INTEL SSD800G
Firmware Version: 2DV1051
```

这些是支持的 NVMe 功能。`identify` 命令也适用于命名空间。



```
#### nvmectl identify nvme0ns1
Size (in LBAs): 156284368 (1490M)
Capacity (in LBAs): 156284368 (1490M)
Utilization (in LBAs): 156284368
Thin Provisioning: Not Supported
Number of LBA Formats: 7
Current LBA Format: LBA Format #00
LBA #00: Data Size: 512 Metadata Size: 0
LBA #01: Data Size: 512 Metadata Size: 8
LBA #02: Data Size: 512 Metadata Size: 16
LBA #03: Data Size: 4096 Metadata Size: 0
LBA #04: Data Size: 4096 Metadata Size: 8
LBA #05: Data Size: 4096 Metadata Size: 64
LBA #06: Data Size: 4096 Metadata Size: 128
```

LBA 格式允许指定扇区大小，包括用于加密或元数据的额外空间。FreeBSD 尚未让你用不同的扇区格式化驱动器。

### NVMe 性能

`nvmectl` 工具还包含性能测试工具 `nvmeftest`。虽然你可能想测试驱动器的性能，它可以演示多队列的优势。在这里，我们使用增加线程数来测量读取速度，每个测试持续 30 秒。最后一列显示每个线程数量的实际吞吐量，单位为每秒兆字节。

从 512 字节块开始。

```
#### for threads in 1 2 4 8 16 32 64; do nvmeftest -n $threads -o read
Threads: 1 Size: 512 READ Time: 30 IO/s: 215377 MB/s: 105
Threads: 2 Size: 512 READ Time: 30 IO/s: 309203 MB/s: 150
Threads: 4 Size: 512 READ Time: 30 IO/s: 509555 MB/s: 248
Threads: 8 Size: 512 READ Time: 30 IO/s: 534976 MB/s: 261
Threads: 16 Size: 512 READ Time: 30 IO/s: 535131 MB/s: 261
Threads: 32 Size: 512 READ Time: 30 IO/s: 534682 MB/s: 261
Threads: 64 Size: 512 READ Time: 30 IO/s: 533701 MB/s: 260
```

使用一个线程时，我们可以读取 105 MB/s。使用八个或更多线程，我们达到了 260 MB/s。这可能是该设备在该块大小下的最大吞吐量。

这是使用 4096 字节 (4 KB) 块的相同测试。

```
#### for threads in 1 2 4 8 16 32 64; do nvmeftest -n $threads -o read
Threads: 1 Size: 4096 READ Time: 30 IO/s: 171216 MB/s: 668
Threads: 2 Size: 4096 READ Time: 30 IO/s: 308111 MB/s: 1203
Threads: 4 Size: 4096 READ Time: 30 IO/s: 521704 MB/s: 2037
Threads: 8 Size: 4096 READ Time: 30 IO/s: 549384 MB/s: 2144
Threads: 16 Size: 4096 READ Time: 30 IO/s: 543376 MB/s: 2122
Threads: 32 Size: 4096 READ Time: 30 IO/s: 542464 MB/s: 2119
Threads: 64 Size: 4096 READ Time: 30 IO/s: 533710 MB/s: 3213
```

即使使用一个线程，我们也超过了 512 字节块的性能。八个线程可以达到约 2000 MB/s，而 16 个线程可以获得约 2120 MB/s。通过更多的测试，你可以发现九或十个线程使该块大小的性能达到最大。

现在忘记这些微小的块大小，跳转到 128 KB 块。

```
#### for threads in 1 2 4 8 16 32 64; do nvmeftest -n $threads -o read
Threads: 1 Size: 131072 READ Time: 30 IO/s: 217706 MB/s: 2721
Threads: 2 Size: 131072 READ Time: 30 IO/s: 257804 MB/s: 3222
Threads: 4 Size: 131072 READ Time: 30 IO/s: 257804 MB/s: 3222
Threads: 8 Size: 131072 READ Time: 30 IO/s: 257580 MB/s: 3219
Threads: 16 Size: 131072 READ Time: 30 IO/s: 257064 MB/s: 3213
Threads: 32 Size: 131072 READ Time: 30 IO/s: 257184 MB/s: 3214
Threads: 64 Size: 131072 READ Time: 30 IO/s: 257104 MB/s: 3213
```

两个线程使这些大块的吞吐量最大。

一旦 NVMe 设备拥有命名空间（namespace），`nvd(4)` 驱动程序就会开始运行。该设备实际上是一个 GEOM 提供程序，可以用于 ZFS 存储数据。你会看到类似 `/dev/nvd0`、`/dev/nvd1` 等设备节点。

如果你计划将 NVMe 设备作为启动驱动器，你必须对启动设备 `/dev/nvd` 进行分区（可能需要使用 GPT）。如果你不从该设备启动，可以跳过分区表，直接在设备节点上上写文件系统。

传统的 BIOS 和 CSM 模块只理解传统的磁盘以及伪装成磁盘的东西。NVMe 设备的意义在于它们拒绝撒谎，并且不模拟传统的硬盘。

从 NVMe 设备启动需要使用 UEFI 启动。FreeBSD 在 10.3 版本中获得了通过 EFI 启动根位于 ZFS（root-on-ZFS）的能力。

# zfsd

预计于 2016 年 7 月发布的 FreeBSD 11.0 将包含第一个版本的 `zfsd(8)`。这个针对 FreeBSD 特有的守护进程提供了 Solaris 服务管理设施（SMF）的一些功能。`zfsd(8)` 接收内核无法自行处理的故障通知并解决它们。

该守护进程监听 `devctl(4)` 事件，例如 I/O 错误或磁盘附加和移除事件，然后通过激活和禁用热备盘，或将池中的单个设备上线（online）和离线（offline）来做出响应。

`zfsd(8)` 不需要任何配置。它根据你的池配置做出所有决策。在 `zfsd` 的第一个版本中，只有 `autoreplace` 池属性有效。

如果接收到属于 VDEV 成员磁盘的设备通知，`zfsd` 会立即激活池中的热备盘并开始重构（resilvering）。

当一个新的 GEOM 设备出现时时，`zfsd` 首先检查是否有 ZFS 标签。如果磁盘带有标签显示它曾是某个池的成员，则该池会被重新附加。一旦重构完成，任何临时替换该设备的热备盘将被禁用并返回可用备用盘列表。

如果新到达的设备没有 ZFS 标签，但其物理路径与某个 VDEV 缺失成员的路径匹配，且设置了池属性，则使用新设备替换缺失设备。在较新版本的 FreeBSD 中，物理路径可能是明亮的，也可能是 SES 路径，`/dev/enc50030480176b87d/type@0/slot/1/elmdesc@slot_01/gpt/f0-1EHJZMC`。

重构完成后，`zfsd` 会禁用任何替换该设备的热备盘。被禁用的设备返回可用备用盘列表。

如果 VDEV 变为降级或故障，`zfsd` 尝试通过激活热备盘来解决问题。

如果单个设备在 60 秒内产生超过 50 次 I/O 或校验和错误，`zfsd` 会将该设备标记为降级并激活热备盘。ZFS 继续使用该降级设备直到池完成重构，`zfsd` 会将故障设备从池中移除。

如果池中添加或返回了新的热备盘，`zfsd` 会在需要替换另一个设备时激活该备用盘。

当重构操作完成时，`zfsd` 尝试禁用不再需要的任何热备盘，以便它们能够替换后续发生的故障。

`zfsd(8)` 还监听“物理路径更改”事件，以便在新到达磁盘的路径设置时收到通知。这可能比磁盘插入到达稍后发生。当物理路径更新且池的 `autoreplay` 属性被设置时，`zfsd` 尝试用相同的物理路径替换缺失的磁盘。

当你更换故障磁盘且 CAM 子系统注意到新磁盘位于相同的插槽、相同的路径时，`zfsd` 会自动启动替换操作并将池恢复到健康状态。



将磁盘从一个插槽移动到另一个插槽与移除磁盘后重新插回完全相同。内核会将磁盘标记为已移除。当你插回磁盘时，内核会看到磁盘上的 ZFS 标签，识别它属于哪个池，并自动将其上线（online）。池的元数据随物理路径更新。

现在我们已经讨论了如何使用高级硬件，让我们来看看各种 ZFS 缓存的高级用法。

- 1 所有管理员都非常清楚在任何情况下发生多少恐慌是。
- 2 你不是在尝试在 ZFS 下使用软件 RAID 吧？别让 Jude 过来那里！
- 3 如果你的笔记糟糕或不存在，未来的你会诅咒你出生的那天以及你的宠物。已经足够的人有你了吗？
- 4 我们告诉这些是为了你好，而不是为了我们以后能说“我们早就说过了”。
- 5 就像 Lucas 在冰淇淋摊前插队一样熟练。
- 6 遗憾的是，不是光速引擎。

# 第 7 章：缓存

与任何其他文件系统一样，ZFS 使用内存缓存来提高性能。但与大多数其他文件系统不同，管理员可以调整这些缓存来优化系统行为。ZFS 在 `zpool.cache` 中缓存系统池列表。

系统已声占用总计 23 GB。

ZFS 访问的文件经常出现在 MFU 空间中。这显示 ARC 中有 15 GB 的 MFU 数据。

MRU 条目显示有 7,398 MB 用于存储最最近访问的文件。

从一个队列移动到另一个队列的数据，或者要刷到磁盘的异步写入，会出现在 Anon 空间中。标记为 Header 的内存供 ARC 自身的元数据使用。这 23 GB 的 ARC 需要 412 MB 的元数据。其他内容包括如仅在运行时使用的元数据等，用于帮助 ARC 在其缓存中查找内容。严格来说，它不是缓存本身的一部分，而是支持性基础设施。

虽然 ARC 对内存非常“贪婪”，但请注意，这个长时间运行的系统仍有几 GB 的空闲内存。磁盘几乎全满，但真实用户需求的数据量相对较小。任何管理过文件服务器的人都能看出这种模式——每家公司的会计部门都有一份主电子表格，再加上无数个日期略有不同的电子表格副本，而所有这些都至关重要，且必须为了后世永远保留下去。如果 ARC 正在使用大部分系统内存，那是因为某个进程访问了文件。ARC 并不会为了榨取内存而去寻找理由。

## Zfs-stats

FreeBSD 通过 `vfs.zfs` 和 `kstat.zfs` 中的各种 `sysctl` 暴露了 ZFS 性能、设置和指标。这些值本身通常意义不大，但相互比较时就具有明示性。与其解析这些值，我们强烈建议使用 `zfs-stats` 软件包来检查 ARC。

使用 `zfs-stats -A` 获取有关 ARC 的基本信息，例如其当前大小以及 ARC 内部每个队列的大小。以下是来自 Lucas 系统的一份 `zfs-stats` 报告中的一些趣味性片段。

```
# zfs-stats -A
```

```
ARC Summary: (HEALTHY)
  Memory Throttle Count: 0
```

`Memory Throttle Count`（内存节流计数）告诉我们 ARC 有多少次缩小以归还给内核供其他进程使用。如果内存节流计数很高，你可能考虑降低 ARC 大小限制，以确保为其他进程留足够的空闲内存。不过，ARC 内存节流并不意味着系统必须拥有更多内存，仅仅意味着它会利用额外的内存。

| 指标 | 值 |
| :--- | :--- |
| ARC Size: | 36.22% 10.89 GB |
| 大小 (自适应): | 100.00% 30.07 GB |
| 最小大小 (硬限制): | 12.50% 3.76 GB |
| 最大大小 (高水位): | 8:1 30.07 GB |

这个特定的 ARC 处于其最大大小的 36.22%，即 10.89 GB。它配置的最大大小为 30.07 GB。最小为 3.76 GB。

| ARC 大小细分: | |
| :--- | :--- |
| 最近使用缓存大小 (MRU): | 50.00% 15.03 GB |
| 频繁使用缓存大小 (MFU): | 50.00% 15.03 GB |

ARC 甚至对分配给 MRU 和 MFU 缓存的内存进行了划分。

由 `zfs-stats -E` 提供的 ARC 效率报告比通用报告更有趣。以下是另一台服务器上该输出中最有趣的片段。

### zfs-stats -E

| 指标 | 值 |
| :--- | :--- |
| ARC 效率: | 78.40m |
| 缓存命中率: | 97.76% 76.65m |
| 缓存缺失率: | 2.24% 1.75m |
| 实际命中率: | 97.76% 76.65m |

ZFS 将内存块解码为文件缓存。此报告的顶部向我们展示了从中获得了了多少收益。`Cache Hit Ratio` 说明了百分之的磁盘读取请求是从 ARC 提供的而不是去访问磁盘。在这种情况下，该机器上 97.76% 的读取请求都是从内存提供的。百分比后面的数字是请求的原始数量。这从 ARC 托管了 7665 万次磁盘请求。

接下来，`zfs-stats` 显示了缓存文件来自哪个缓存。

| 按缓存列表分类的缓存命中: | |
| :--- | :--- |
| 最近使用 (MRU): | 3.35% 2.57m |
| 频繁使用 (MFU): | 96.65% 74.08m |
| 最近使用幽影 (MRU Ghost): | 0.04% 28.81k |
| 频繁使用幽影 (MFU Ghost): | 0.08% 63.26k |

MRU 缓存类似于传统的缓冲区缓存，提供了从 ARC 服务的 3.35% 的文件。96.65% 的所有文件来自 MFU 缓存。这些队列之间确实存在重叠——在没有 MFU 缓存的情况下，某些频繁访问的文件会出现在 MRU 缓存中。但这很好地说明了为什么 ARC 使用 MFU 缓存。

Ghosts（幽影）保存了最近缓存过但由于内存压力或限制而被丢弃的数据列表。增加内存并增大 ARC 大小会提高我们的缓存命中率吗？由于幽影列表的命中仅为 0.04% 和 0.08%，增加内存并不会真正改善缓存。此主机的 ARC 仅填充了 36%，因此项目没有被驱逐。这些微小的百分比代表数万次请求，但与它提供的数百万请求相比，几乎可以忽略不计。额外的内存可能会改善其他进程，但不会改善 ARC。

接下来我们看到从 ARC 获取的数据类型。

| 按数据类型分类的缓存命中 | | |
| :--- | :--- | |
| 需求数据 (Demand Data): | 97.15% 74.46m |
| 预取数据 (Prefetch Data): | 0.00% 0 |
| 需求元数据 (Demand Metadata): | 2.85% 2.19m |
| 预取元数据 (Prefetch Metadata): | 0.00% 0 |

数据是文件的内容，而元数据是关于文件的一切信息。我们在第 8 章讨论预取，但无论预取是什么，它显然没有来到这里。在硬币的另一面，我们看到了哪些数据没有被缓存。

| 按数据类型分类的缓存缺失 | | |
| :--- | :--- | |
| 需求数据 (Demand Data): | 31.72% 556.25k |
| 预取数据 (Prefetch Data): | 0.00% |
| 需求元数据 (Demand Metadata): | 2.85% (此处对应原文) |
| 预取元数据 (Prefetch Metadata): | 0 |

如果 `zfs-stats -E` 显示从 ARC 中提取的数据远多于元数据，你可能考虑增加元数据限制，看看性能是否有所提高。请记住，默认情况下，ARC 的最小大小是可用于元数据容量的一半。此外，缓存的元数据使用的空间不能超过整个 ARC。

## 数据集与 ARC

某些数据具有规律的访问模式，这使得 ARC 变得无关紧要——当任何文件被第二次访问时，它早已从 MRU（最近最使用）列表和 MFU（最频繁使用）列表中过期了。这通常发生在数据集包含数百万个文件，且你可以轻松预测其使用情况的情况下。告诉 ARC 不要缓存这些文件可以释放内存，用于缓存可能从中获益的文件。

ZFS 属性 `primarycache` 定义了数据集信息中哪些部分进入 ARC。默认值 `all`（全部）意味着同时缓存文件数据和元数据。

将 `primarycache` 设置为 `metadata`（元数据）告诉 ARC 只缓存每个文件的元数据，而不是内容。对于包含大量文件的目录，你可能会发现这很有用。如果没有元数据缓存，在大型目录上运行 `ls(1)` 可能需要花费几分钟，因为 ZFS 需要读取磁盘并组装信息。仅缓存元数据会导致 ZFS 预取失效，这对性能的损害可能比仅元数据缓存带来的帮助更大。

将 `primarycache` 设置为 `none`（无）告诉 ARC 不要缓存此数据集的任何内容。没有缓存就无法进行预取，但如果一个数据集没有被缓存，性能显然不再需要考虑的问题。



例如，Lucas 的服务器之一拥有一个数 TB 大的数据集，其中在过去的 15 年中创建了无数文件。在这些文件被访问的少数情况下，它们是按顺序搜索的。服务器没有足够的内存来有效地缓存所有这些文件的内容。告诉 ARC 在此数据集上缓存元数据意味着 `ls(1)` 仍然运行飞快，但我们不会让这台机器的 ARC 被无用的垃圾占用。

在更改 `primarycache` 属性之前，你必须卸载并重新挂载数据集：

```bash
# zfs set primarycache=metadata cdr/cdr
# zfs unmount cdr/cdr
# zfs mount cdr/cdr
```

现在 ARC 可以空出有用的工作，例如缓存分析这些记录时创建的临时文件。

卸载数据集会从 ARC 和 L2ARC 中移除关于该数据集的所有缓存信息。

## 二级 ARC

ARC 会不断进行自我修剪以保持在允许的大小内。长时间未被引用的文件会从 MRU 列表中移除。通常情况下，从 ARC 中删除的项会消失——虽然它们会在幽灵列表（ghost lists）中，因此 MFU 队列可以在它们再次出现时识别出它们，但系统依赖于文件的磁盘副本。

二级 ARC（或 L2ARC）是一个二级读取缓存。L2ARC 捕从 ARC 中掉出的项。通过使用小型、快速、高耐用的磁盘来缓存 ARC 数据，你可以同时减少系统主存储的读取负载并提高读取性能。`zpool(8)` 命令将 L2ARC 称为缓存设备。

虽然 L2ARC 被写入磁盘，但其中的数据在重启后不会仍然存在。即使这些索引可用，在重启系统之前，池可能已经在另一台机器上被修改过。ZFS 无法信任缓存设备上的信息。

截至 2016 年初，已经有了几乎完整的持久化 L2ARC 实现。有了持久化 L2ARC，系统将重新加载主 L2ARC 并将所有内容加载回内存。虽然此功能可能永远不会广泛普及，但重度 L2ARC 用户未来可能会关注该功能。

当你有多个用户、虚拟机或应用程序访问单个数据集时，使用 L2ARC 是有意义的。如果工作集大于你能够负担得起的 RAM 数量，你的第二个选择是基于 SSD 或 NVMe 设备的 L2ARC。对于大多数应用程序（如典型的家庭级 NAS），L2ARC 不会提高性能。L2ARC 可能会通过内存消耗损害性能。

## L2ARC 使用

当 L2ARC 包含了大量缓存数据和元数据时，索引位于 ARC 中。根据经验，每个 GB 的 L2ARC 大约需要 25 MB 的 ARC（这取决于扇区大小、`recordsize` 属性和其他数据集特性，使得实际计算非常困难）。可以假设 1 TB 的 L2ARC 满后会消耗 25 GB 的 ARC。

大多数 L2ARC 并没有 1 TB——至少目前不是。具有足够耐用性的用于缓存的 SSD 仍然昂贵，以至于我们没有它们。对于规划超过 40 块硬盘的大型阵列，请记住这一点。

## L2ARC 缓存

L2ARC 只能缓存从 ARC 中掉出的数据。不在 ARC 中的数据不会出现在 L2ARC 中。

假设你通过将 `primarycache` 属性设置为 `none`，完全禁用了特定池上所有数据集的缓存。向该池添加 L2ARC 不会提高 ZFS 性能。没有缓存数据可以进入 L2ARC。

你可能认为一个 ARC 包含元数据而 L2ARC 缓存实际文件的数据集是有意义的。Lucas 的那个数 TB 大的 `cdr/cdr` 数据集似乎是很好的候选对象。

```bash
# zfs get primarycache secondarycache cdr/cdr
primarycache    metadata  local
secondarycache  all       local
```

软件设置显然不会让你超过硬件的限制。

SSD 不再像以前那样臭名地脆弱了。现代数据中心级 SSD，例如 200 GB 的 Intel DC S3700，其耐用性评分为“5 年每天写入 10 次硬盘”。这意味着每天约 2,000 GB，或每秒 23 MB。你可以持续向此驱动器写入 22 MB/s 的数据，根据英特的说法，它可以持续五年。在高性能服务器上，将 `sysctl` 节流参数调到这些值，并备注在 58 个月后订购新的缓存设备是合理的。由于你的主机可能不会一直以全速写入 L2ARC，因此将这些参数调得更高也可能意义。

# ZFS 意图日志 (ZFS Intent Log)

缓存不仅仅是为了读取数据。ZFS 也通过 ZFS 意图日志 (ZIL) 对写入进行缓存。ZFS 将写入操作写入 ZIL，并处理这些写入以将其正确地添加到 ZFS 中。每个池都有自己的 ZIL。在正常使用情况下，ZFS 在每个提供设备上使用一部分空间作为 ZIL。如果你需要，可以添加一个额外设备作为 ZIL。严格来说，ZIL 并不完全是写入缓存。但它具有某种缓存特性，因此我们将在本章中介绍它。

然而，ZIL 的工作方式并非人们认为的那样。要理解池何时需要独立的日志设备，何时不需要，你必须理解 ZFS 是如何写入数据的。

# 同步与异步事务 (Sync and Async Transactions)

ZFS 核心在于到达持久性存储的数据完整性。磁盘上的数据应该始终保持一致。系统可能会在程序和磁盘之间丢失数据，但没有任何文件系统可以保护仅驻留在 RAM 中的传输中数据。

为了确保磁盘数据的完整性，ZFS 将请求分组在事务组（transaction groups，txgs）中。事务组是一组数据以及相关的文件系统元数据。当你请求系统写入磁盘时，ZFS 会在一个事务组中收集这些写入操作。一个事务组可以包含来自许多无关进程的写入。当该组拥有足够的数据或计时器超时时，该事务组就会写入磁盘。该计时器可能长达 30 秒，也可能短至 5 秒，取决于你运行的 FreeBSD 版本。

事务组是文件系统的待办列表。正就像你的待办列表一样，如果发生了糟糕的事情，列表就会被抛给狼群。在完全写入磁盘之前，数据很容易受到系统故障的影响。如果系统在事务组写入磁盘之前崩溃或死亡，这些数据就会丢失。缩短事务组超时可能会减少数据丢失量，但也会影响性能。

作为系统管理员，你的工作是管理数据丢失风险。让我们来看看写入磁盘的过程。

程序将一段数据交给内核并说：“请写入磁盘”。在内核确认接收数据之前，程序不会继续执行。一旦内核说“我收到数据了”，程序就会继续。等待此响应的程序被称为在 I/O 上发生阻塞（blocking on I/O）。

重要的问题是：内核何时确认接收数据？是在数据被添加到事务组时，还是在写入磁盘时？

在正常操作中，当数据作为待处理事务组的一部分添加到内存时，内核就会确认数据。数据不在磁盘上——内核仅仅是承担了数据的责任。如果系统是一家餐厅，那么现在的晚餐就在服务员通往客户手中的手中的，但服务员仍可能绊倒。异步操作的变体在现代文件系统中很常见，例如 Linux 的各种版本 extfs 和 BSD UFS。

文件系统也可以以同步模式工作，在这种模式下，只有当位写入物理存储介质时内核才会确认数据。同步计数（Sync counts）极其安全，但也极其缓慢。写入数据的程序将阻塞等待内核的写入请求。某些程序（例如数据库服务器）使用 `fsync(2)` 系统调用对特定文件请求同步确认。`zsadmin` 同步命中元数据，以便系统仅在写入完成后才确认数据，或者可以使用 `fsync(8)` 程序告诉系统立即将所有内容刷新（flush）到磁盘。

# ZFS 意图日志 (ZFS Intent Log)

当 ZFS 在同步模式下写入文件时，它不会立即将事务推送到磁盘。相反，这些写入会被倾倒入 ZIL。它们并没有像 ZFS 数据集块那样整齐地排列；相反，它们只是磁盘上的一堆块。当事务组写入磁盘时，ZIL 上的块会被写入到它们正确的位置。

池导入（pool import）过程会检查 ZIL，查找尚未到达最终位置的数据。如果系统在正在导入的池中发现传输中的块，它将完成这些事务。

池通常使用每个存储提供设备上的一个小块空间作为 ZIL。是的，这意味着同步写入会被写入物理存储两次。但池仅对同步写入的数据使用 ZIL。正常的异步写入被存储在 RAM 中，并作为常规事务组的一部分提交。

你有时可以通过将 ZIL 放在一个专用的快速设备上（称为“独立意图日志”，Separate Intent LOG）来提高性能。

# 独立意图日志 (Separate Intent Log)

你可以通过使用独立意图日志（SLOG）将 ZIL 从池中分离。通过将 ZIL 移动到独立的专用硬件上，你避免了向存储提供设备写入两次相同的数据。如果 SLOG 硬件比池快，内核可以更快地确认数据，从而提高请求应用程序的性能。

尽管用法常见，SLOG 并不等同于 ZIL。SLOG 运行在 ZIL 或存储提供设备上。你可以通过一个窗口启动 SLOG。

最快、最可靠且昂贵的 SLOG 是 NVRAM 芯片。高耐用性 SSD 是 SLOG 的常见选择。你甚至可以使用 SAS 驱动器，但它们是最不可靠的。每一个都需要一个电源（例如电池或超级电容器），以便在系统故障时完成写入。



SLOG 不需要很大。`vfs.zfs.dirty_data_max` 给出了可能的传输数据量。FreeBSD 10 默认使用的 ZIL 大小等于系统内存的十分之一。你可以使用一个设备为多个池提供 SLOG，但会分摊该设备的 I/O。

并不是所有 SSD 都是一样的。对于数据完整性至关重要的应用程序，作者强烈建议你咨询硬件供应商如 `www.ixsystems.com`。糟糕的选择会毁灭你的性能。

# 数据集 ZIL 调优 (Per-Dataset ZIL Tuning)

你可以通过 `sync` 属性控制数据集是否使用 ZIL。默认设置 `标准` 会告诉数据集使用 ZIL。将 `sync` 设置为 `always` 是管理数据最安全的方法，但会有严重的性能代价。

将 `sync` 设置为 `disabled` 会完全禁用该数据集的 ZIL。所有写入都是异步的。永远在任何由数据库或 NFS 使用的数据集上禁用 ZIL。唯一的理由是，如果禁用 ZIL 解决了你的应用程序问题，请一定要提交错误报告或安装快速的 SLOG。

在所有情况下，请将 `sync` 留为 `标准`。你可能有一个。

ZFS 成为许多不同应用程序（如网络文件系统 NFS 和 iSCSI）的数据存储后端。你可能使用一个卷作为虚拟化系统的驱动器。所有这些不同层都独立运行。虽然它们可以通过常用的系统调用和 API 进行通信，但它们并不互相控制。应用程序栈中的每一层（并且经常）欺骗其他层。这一点最明显且危险的地方过于 `fsync(2)` 系统调用。

假设你有一个运行在 iSCSI 驱动器上的虚拟机，该驱动器由服务器上的一个卷支持。虚拟机的操作系统请求同步磁盘写入。iSCSI 栈请求该操作并传递给 ZFS。如果你在那个卷上设置 `sync` 为 `disabled`，ZFS 会冷笑说：“同步？没问题！包你的，伙计，”并等待到下一个 `txg` 才执行任何操作。

# zpool.cache

现在让我们讨论一个你可能听过，但对日常系统管理没有影响的文件：`/boot/zfs/zpool.cache`。

`zpool.cache` 文件包含了系统中当前活跃的存储池（pools）及其提供者的描述。当你启动 ZFS 系统时，内核会检查根池上的 `zpool.cache` 文件，以发现它应该导入哪些系统存储池。

ZFS 的 `db(8)` 使用缓存文件中的信息进行调试。对于没有缓存的存储池，你无法对其使用调试器。

你可以通过 `cachefile` 属性控制缓存文件的位置。在这里，我们更改 `work` 存储的缓存文件。

```bash
# zpool set cachefile=/work/zfs/work.zpool.cache work
```

尽管许多遗留的过时文档给出了相反的，但在现代版本的 ZFS 或 FreeBSD 中，几乎没有理由更改 `cachefile` 的位置。

既然你已经理解了缓存，我们就可以谈谈性能了。

> ¹1 如果你必须再次进行这个对话，请尽量不要加上“噢，你到底凭什么领到今天的饭吃？”——这种话通常不受欢迎。

> ²2 显然，狼群不在乎纸质列表。为了让这个比喻生效，我们建议将你的待办事项写在斜坡烤炉上。

# 第 8 章：性能

我们都希望存储系统是快速、功能丰富且无限的。虽然我们还没有达到极限，但在良好的硬件上，ZFS 的功能可以非常快。然而，即使是最好的硬件也可能无缘无故变慢。了解如何使用诊断工具可以帮助你理解系统的性能。也许你无法用手头的设备修复它，但至少你心里清楚哪里出了问题，并可能将部分负载转移到其他地方。

FreeBSD 包含了检查通用磁盘和文件系统性能的工具，以及 ZFS 特有的工具。你可以通过 `sysctl(8)`、`vmstat(8)` 和相关命令获取详细信息，但我们强烈建议安装 `zfs-stats` 附加包，以便于解析和处理这些信息。

一旦你理解了如何评估系统性能，我们将讨论几个 ZFS 性能特性以及它们在何时可能有用。

在深入评估 ZFS 性能之前，让我们先泛谈谈性能。

## 什么是性能？

性能可以被描述为“系统管理工作负载的优劣”。每个系统的负载略有不同，因此即使是相同的硬件执行看似相同的任务，性能也会存在差异。即使你尽力在另一个系统上复制硬件、软件安装和工作负载，别人也能发现它们之间的差异。这正是让基准测试（benchmarking）令人恼的原因之一。

系统管理员主要关心提高性能。这意味着识别并消除瓶颈。普通计算机有四种基本资源：存储输入/输出（I/O）、网络带宽、内存和 CPU。如果你向系统堆积工作，直到它无法处理更多任务，你实际上是在发现这些资源中哪一个先达到饱和。那个资源就是你的瓶颈。

提高性能需要识别并转移瓶颈。你总是会遇到下一个瓶颈。如果 CPU 是当前的瓶颈，而你增加了更多的处理能力，计算机就会加速，直到磁盘 I/O 或网络内存达到饱和。你确实提高了性能，是的……但仅限于新硬件允许的范围。

不同的工作负载可能有完全不同的瓶颈。

许多系统管理工作需要增强这些资源中的某一个以适应另一个。Lucas 总是将“系统调优”称为“重新排列瓶颈”。¹

考虑一下 ZFS 压缩。ZFS 压缩减少了系统写入磁盘的数据量。压缩和解压数据会消耗处理器时间。压缩是用存储 I/O 交换 CPU 时间。然而，大多数计算机的处理器能力远超过其可能使用的量。我正在写的笔记本电脑有一个四核处理器，但只有一个中等速度且 I/O 有限的磁盘。在这个系统上开启压缩是一个显而易见的获。。在一个磁盘 I/O 多于处理器能力的系统上，你可能会做出不同的决定。

你的存储越复杂，就越能调整和转移瓶颈。你的服务器有六个磁盘控制器，但所有的 I/O 都流向其中一个？重新排列你的数据集，将负载分散到多个控制器上。也许某个特定磁盘饱和了？拆分该负载。也许你的存储池读或写满了，或者读写都满了。添加一个配置适当的 SLOG 和 L2ARC 来帮助。

不过，在进行任何更改之前，请调查瓶颈在哪里。如果系统的特定工作负载受限于 CPU 或内存，购买更快的磁盘系统将毫无帮助。如果磁盘读取限制了服务器的性能，为 ZIL 添加快速 SSD 也不会提高性能。

系统管理中许多长久问题之一是：是什么在消耗我的磁盘带宽？ZFS 存储池扫描（scrub）可能会影响其他操作，但在日常使用中，ZFS 并对这个问题产生任何新答案。使用 `top -m io` 来识别密集使用磁盘的进程。最活跃的进程应该是繁忙吗？

如果你的性能不符合预期，请记住，你的存储系统性能取决于其最慢的组件。你可以拥有非常快的 SAS 控制器和顶级高速硬盘，但可能因为劣质的驱动线而获得糟糕的性能。SATA 端口倍增器会根据连接磁盘的数量按比例降低性能。仅仅是因为你可以把某些硬件组件连接在一起而已。

## ZFS 与性能

许多常见建议适用于 ZFS。`atime` 属性可能是性能的杀手，因为每次读取都会变成一次写入。如果磁盘是瓶颈，将 `atime` 设置为 `off` 可以很有帮助。

该池以 275 次操作/秒的速度读取 7.34 MB/秒，且没有写入操作。这意味着每次读取操作平均为 27 KB（7.34 MB / 275 = 27 KB）。

该池更有趣。我们有每秒两次读取请求，以及每秒 402 次写入，总计 24 MB/s。读取忽略不计，但每次写入平均为 60 KB。这里有实际的操作在进行。将 `atime` 设置为 `off` 可以很有帮助。

## iostat

`zpool iostat` 提供了存储池在特定时刻性能的快照。要查看系统启动以来的平均活动，使用 `zpool iostat`。

| pool alloc free operations write read read write |
|---|---|---|---|---|---|
| work | 2.21G | 1.81T | 2 | 402 | 36.2K | 24.0M |
| zroot | 15.5G | 905GB | 275 | 0 | 7.34M | 0 |

我们有每个池的名称，以及分配和可用空间量。最后四列显示每个池的读写活动，以每秒操作数和字节为单位。

要查看单个池的活动，给出池的名称。

### zpool iostat work

这消除了指定池以外的所有输出。

## 当前和持续的池活动

要查看池在此时刻的行为，以及活动如何随时间变化，让 `zpool iostat` 每隔几秒打印新的统计信息。在命令行末尾指定秒数。这里我们每两秒更新一次。按 CTRL-c 退出。

### zpool iostat 2

| 池 分配 容量 空闲 | 操作 读 写 | 带宽 读 写 |
| --- | --- | --- | --- | --- | --- | --- |
| work | 3.37G | 1.81T | 14 | 107 | 146K | 900K |
| zroot | 15.5G | 905G | 3 | 2 | 32.9K | 12.7K |
| work | | 3.37G | 1.81T | 0 | 0 | 0 | 0 |
| zroot | 15.5G | 905G | 0 | 0 | 0 | 0 |

第一条目是自系统启动以来的平均活动，就像运行没有间隔的 `zpool iostat` 一样。第二及后续条目给出当前值。



在表头之后，前两个条目给在你运行命令时的池活动以及一组虚线。两秒后，它会在分隔符下方打印一组新数据。

如果你指定检查单个池，`zpool iostat` 会丢失分隔符。在这里我们查看 `work`。

| # 池 分配 容量 空闲 | 操作 读  写 | 带宽 读  写 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| work | 3.35G | 1.81T | 15 | 104 | 148K | 897K |
| work | 3.35G | 1.81T | 0 | 616 | 2.25K | 3.74M |
| work | 3.35G | 1.81T | 1 | 553 | 5.74K | 2.78M |
| work | 3.36G | 1.81T | | 607 | 21.0K | 2.57M |

该池平均每秒执行104次操作，但此时它每秒正在执行600次操作。它正在处理真正的工作！

## 虚拟设备活动

虽然每个池包含一个或多个相同的虚拟设备，但池对虚拟设备的使用可能并不相同。

一种常见的情况是你有一个几乎满载的池，并添加了一个新的虚拟设备以获得更多空间。此时池的表面写入性能可能会下降到新虚拟设备的水平，而不是带有所有虚拟设备的整个池的理论吞吐量。新虚拟设备拥有所有的空闲空间，因此新的写入进入那里。随着时间的推移，随着你删除旧文件并移除旧快照，每个 VDEV 的利用率可能会达到平均。然而，取决于你的负载，VDEV 利用率可能永远无法平衡。

要查看每个池的每个 VDEV 活动，请在 `iostat` 之后添加 `-v` 标志。与普通的非详细模式 `zpool iostat` 类似，你获得的第一个输出代表自系统启动以来的平均值。在详细模式下，这些数字看起来有点奇怪。

### `zpool iostat -v work`

| 容量 | 操作 | 带宽 |
| 分配 空闲 | 读 写 | 读 写 |
| work | 2.13G 1.81T | 10 87 | 100K 715K |
| mirror | 1.06G 927G | 5 43 | 50.9K 359K |
| gpt/zfs0 | | 2 8 | 26.4K 360K |
| gpt/zfs1 | | 2 8 | 26.4K 360K |
| mirror | 1.07G 927G | 4 43 | 49.6K 356K |
| gpt/zfs2 | | 2 8 | 25.0K 357K |
| gpt/zfs3 | | 2 8 | 26.4K 357K |

你会得到池的总量、池中 VDEV 的总量以及池中每个提供者的数量。查看池每秒写入操作。自系统启动，池平均每秒执行十次操作。第一个镜像设备负责其中五个，第二个负责四个。每个虚拟设备中的每个磁盘每秒处理两次读取。

写入活动看起来非常奇怪。ZFS 的初始数据显示该池每秒平均87次写入请求，其中43来自每个池。这并不糟糕——每个设备的值显示每个磁盘每秒写入请求。无论你如何取整这些值，它们并不接近。简单的答案是，ZFS 的平均值不可靠。它们在比例上是正确的。`zpool iostat` 在测量性能时不会锁定内核结构，命令运行时你会得到细微的变化。与非详细模式 `zpool iostat` 一样，为了查看当前值，必须在命令末尾提供间隔。在这里我们显示每秒更新一次的池每设备活动。

### `zpool iostat -v work 2...`

| 容量 | 操作 | 带宽 |
| 分配 空闲 | 读 写 | 读 写 |
| work | 2.36G 1.81T | 0 69 | 0 147K |
| mirror | 1.15G 927G | 0 40 | 0 93.6K |
| gpt/zfs0 | | 0 10 | 0 94.9K |
| gpt/zfs1 | | 0 10 | 0 94.9K |
| mirror | | 0 28 | 0 53.3K |
| gpt/zfs2 | | 0 6 | 0 54.6K |
| gpt/zfs3 | | 0 6 | 0 54.6K |

第一个镜像 VDEV 执行的每秒 I/O 操作多第二个镜像。再次，单个磁盘数字并不等于设备的总操作数，但它们在比例上是准确。现在你可以看到你的池运行得如何，让我们讨论一些可以改变你池性能的特性。

## ZFS 预取

文件系统的工作是根据请求提供数据。ZFS 进一步实现了这一想法，准备提供你即将请求的数据。这发生在两个级别：每个 VDEV 和每个文件。FreeBSD 默认未启用每个 VDEV 取取，但启用每个文件预取。

### 每个 VDEV 预取

从旋转磁盘检索数据最耗时的部分是将磁头定位到磁道上。这就像做三明治——在两片面包之间涂抹花生酱需要两分钟，但去商店买面包和花生酱可能需要一个小时。现在硬件已经物理排列好了，从以 5000 或 10000 转旋转的磁盘读取整条磁道的数据只需要微秒。

每个 VDEV 预取尝试让移动头部变得值得。FreeBSD 默认不使用每个 VDEV 预取，但如果你的负载涉及复杂的元数据、大型目录树或许多小文件，每个 VDEV 预取可能会有所帮助。每当 ZFS 从 VDEV 读取几个块时，它也会读取目标之后的几个块以寻找元数据。发现的任何元数据都会进入特殊的每个 VDEV 预取缓存。请求程序很有返回并请求该元数据。每当程序请求预取的元数据时，ZFS 从缓存中提供它，返回物理 VDEV 并预取更多块。

每个 VDEV 预取的块进入简单的“最近使用”缓存，而不是 ARC。VDEV 缓存的大小等于 VDEV 中存储提供者的数量乘以可调参数 `vfs.zdev.cache.size`。FreeBSD 默认将其设置为 0，因此不使用该缓存。通过在 `/boot/loader.conf` 中将此可调参数设置为所需值来启用缓存。一个常见的值 `vfs.zdev.cache.size="10M"`。

重启后，你将有一个每个 VDEV 预取缓存生效。`sysctl kstat.zfs.misc.vdev_cache_stats.miss` 显示 ZFS 检查每个 VDEV 缓存中的元数据但未找到的次数。同样，`sysctl kstat.zfs.misc.vdev_cache_stats.hits` 显示 ZFS 在缓存中找到东西的频率。

在没有每个 VDEV 预取的情况下测试你的负载并观察其行为。

每个 VDEV 预取预先缓存了多少？`sysctl vfs.zdev.max` 给出了从 VDEV 读取的最小大小。这默认值为 16384，即 16 KB。如果程序请求小于此大小的内容，就会触发每个 VDEV 预取。

然而，`vfs.zdev.cacheshift` 给出了要预取并搜索的数据量。这是一个位移值，所以默认的 16 意味着 64 KB。

因此，如果程序请求小于 16 KB 的读取，ZFS 而是读取 64 KB。如果程序请求例如 20 KB 的读取，则发生没有 VDEV 预取。

虽然更改预取值在某些旧版本的 ZFS 中有助于性能，但在现代 ZFS 中，你应该几乎总是保持原样。作者知道很多时候更改这些值会导致痛苦。

### 每个文件预取

文件系统的任务是根据请求提供数据。ZFS 通过准备提供你即将提问的数据，进一步地利用了这一想法。这发生在两个级别：每个 VDEV 和每个文件。FreeBSD 默认不启用每个 VDEV 预取，但启用了每个文件预取。

## 事务组调优

你可以通过调整事务组和 I/O 调度器来优化性能。我们专门针对 FreeBSD 10 及更高版本的调优。在早期版本中，调优 OpenZFS 写入的机制要复杂得多。

事务组（或 txg）是按顺序写入磁盘的单块大容量数据。一个事务组可以包含来自许多不同程序的许多数据块。如果整个事务组没有成功写入磁盘，则整个组都会被取消。

你可以控制系统写入事务组的频率及其最大尺寸。

### txg 计时

如果没有其他触发因素将 txg 写入磁盘，ZFS 会每隔几秒写入一次，这具体由 `sysctl vfs.zfs.txg.timeout` 决定。虽然该设置的值在 OpenZFS 的早期版本中有所波动，但目前的默认值是五秒。最坏的情况下，任何待处理的数据都会每五秒写入一次磁盘。

对于大多数系统来说，每五秒写入一次是可以的。像 `top(1)` 这样的程序可能会每五秒显示一次 CPU 活动突峰，因为待处理的事务组正在被压缩。你很少会将超时时间减少到五秒以下。

然而，对于某些系统，增加该值是有意义的。如果你在低负载虚拟机上运行 ZFS，你可能会将 txg 超时时间增加到 15 秒左右。Lucas经常在虚拟机上运行主机 LDAP 镜像和权威 DNS 服务器，而这类主机对磁盘 I/O 的需求通常不高。减少事务写入的频率不会提高这台特定虚拟机的性能，但它会提高运行在超层视程序上的其他虚拟机的硬件访问效率。为大多数运行低负载设置的虚拟机提供低设置可以提高所有虚拟机的整体性能，但单个自私或高负载的虚拟机可能会消耗掉许多此类增益。（不过，这可能恰恰是你想要达到的目标。）

在共享读写带宽的典型硬件上，增加超时时间在大多数情况下可能会提高读取性能，但在写入期间会降低读取性能。



如果计时器到期且系统没有等待写入磁盘的事务，ZFS 将不会写入任何数据。ZFS 不会为了有一个事务组而写入一个空事务。然而，它仍然会增加事务组的计数。

将事务组超时时间设置为五秒以下会遇到 I/O 调度器和写入节流的限制。对大多数人来说，五秒是最小合理值。

## txg 大小

增长得足够大的 `txg` 会在超时之前提交到磁盘。FreeBSD 在启动时会根据主机的内存量和可调优的 `vfs.zfs.dirty_data_max_percent` 自动调整事务组的最大尺寸。默认值为 10%，最高可达 4 GB，并由 `vfs.zfs.dirty_data_max_max` 控制。一旦事务组使用了系统 10% 的内存内存，它就会被写入磁盘。

你可以在系统启动后使用 `sysctl vfs.zfs.dirty_data_max` 更改事务组的最大尺寸。该值的单位是字节，将你所需的 GB 数值乘以 `$1024^3` 即可获得适当的 `sysctl` 值。

棘手的问题是：你是否应该更改事务组的大小？你的系统将 RAM 的 10% 写入磁盘需要多久？发生的频率是多少？大多数主机的 RAM 内存远大于其 I/O 吞吐量。尝试在五秒内写入十分分之一的内存将是一场灾难。Lucas 的测试主机在单个池中有几块硬盘并拥有 32 GB 内存。向磁盘写入 3.2 GB 数据需要 20 秒。如果该主机在标准的五秒超时时间内生成了 3.2 GB 的磁盘活动，机器将迅速陷入不可用的状态。

如果你的系统是一个高性能磁盘阵列，具有极大的吞吐量目标和经济规模的内存，你可能会发现增加最大值是有用的。

在“写入周期”期间，大多数从磁盘的读取会被挂起。这允许写入尽快完成。写入完成后，读取恢复。这种交替工作负载通常可以提高性能。通过对工作负载的了解，你可以决定是频繁地刷新大组还是频繁地刷新小组。在同一个池内大量拷贝数据时，Jude 将 `txg` 大小增加到 24 GB 并将超时延长到 30 秒，性能提高了 25%。

## txg 持续时间和内容

如果你正在调整事务组的大小和周期，使用以下脚本测量它们的大小和耗时是合理的：

```dtrace
#!/usr/bin/dtrace -s
txg-syncing
((dsl_pool_t*)arg0)->dp_spa->spa_name == $1/
{
  start = timestamp;
}
txtg-synced
/start && ((dsl_pool_t*)arg0)->dp_spa->spa_name == $1/
{
  this->d = timestamp - start;
  printf("%4dMB of %dMB synced in %d.%0d seconds",
  d_total / 1024 / 1024,
  d_max / 1024 / 1024, this->d / 1000000000,
  this->d / 1000000000 % 100);
}
```

运行脚本并传入池名称。Lucas 创建了一些可以同时测量这两者的 `dtrace` 脚本。

```dtrace
dtrace -s 'duration' matched 2 probes

CPU ID:NAME
1::txg-synced synced 0.11 seconds
2::txg-synced synced 0.24 seconds
4::txg-synced synced 0.22 seconds
2::txg-synced synced 0.31 seconds
```

## 写入节流

你可能会听到的一个术语是写入节流（`write throttle`）。当程序向内存提供数据而 ZFS 可以将其写入磁盘时，写入节流就会发挥作用。随着系统 RAM 越来越满，ZFS 开始在每个写入请求中插入微小的延迟。程序会等待写入请求的响应，这种延迟迫使它们慢下来。目标是确定磁盘可以承受的负载，并让程序以恰好该速度运行。

FreeBSD 10 及更高版本中的写入节流算法运行得流畅得多。你可以通过 I/O 调度器对其进行调优，将在下文中讨论。

## I/O 调度

并非所有硬件都是平等的。Jude 的顶配笔记本电脑的 I/O 容量远低于他的内容分发网络服务器。FreeBSD 的默认设置相当通用。虽然在笔记本电脑上你并不需要对它们进行调优，但如果你有几十个或上百个具有特定工作负载的磁盘，你可以通过调优调度来调整性能。I/O 调度允许你调整延迟和吞吐量。

吞吐量是指可以从存储设备读取和写入的数据量。当你说 SATA-3 可以以 6.0 GB/s 的速度传输数据时，你说的的就是吞吐量。

延迟是系统处理这些请求所需的时间。复杂的存储系统（带有光纤通道总线和建筑多个部分的多个机架）在数据穿过系统时可能会产生延迟。当你通过同时复制太多文件导致硬盘过载时，你的笔记本电脑更容易出现存储延迟。

虽然硬盘通常的营销描述是它们每秒可以执行多少次 I/O 操作（IOPS），但这个术语的意义并不如你想象的那样。能够执行 250 IOPS 经过仔细挑选的数据，并不能说明硬盘处理你数据的能力。

将硬盘想象成汽车。有些针对容量进行了优化，另一些针对里程进行了优化。一辆巨大的双挂牵引车可以运输的货物远比特斯拉 Roadster 多，而后者在红灯起步时并不敏捷。我们大多数人会在周末使用大卡车将一个百人的呼叫中心搬到城市另一端，但在阑尾破裂前把孩子送到医院时会倾向于不同的优化方案。

与汽车不同，你可以在某种程度上控制大多数硬盘的优化。（某些特殊存储设备是专门为某些优化而设计的。）这就是为什么你可以向笔记本电脑的硬盘中倾倒大量数据并导致系统无响应——你只是用吞吐量换了延迟。

ZFS I/O 调度旨在平滑延迟。这可能会降低吞吐量，但会让整体体验更具一致性。通常，通过更改调度，你是在尝试在不引入过多延迟的情况下提高性能。

ZFS 调度是围绕 I/O 队列构建的。

## 测量延迟和吞吐量

你如何知道某个更改是否正向影响了系统性能？通过测量来。Adam Leventhal 为 illumos 编写了一个延迟和吞吐量的 DTrace 脚本，但这里有一个针对 FreeBSD 修改后的的版本。

```c
#pragma D option quiet
inline uint32_t BIO_READ = 1;
inline uint32_t BIO_WRITE = 2;
this uint64_t delta;
BEGIN
{
 start = timestamp;
io::=start / args[0] /
{
 ts[args[0]] = timestamp;
}
 io::=done /args[0] & ts(args[0])/
this->delta = (timestamp - ts(args[0])) / 1000;
this->name = (args[0]-bio_cmd & BIO_READ | BIO_WRITE) == BIO_READ ?
"read" : "write"
@q[this->name] = quantize(this->delta);
@a[this->name] = avg(this->delta);
@v[this->name] = stddev(this->delta);
@if[this->name] = count();
@b[this->name] = sum(args[0]->bio_bcount);
ts(args[0]) = 0;
}
END
{
normalize(@q);i, (timestamp - start) / 1000000000);
normalize(@b, (timestamp - start) / 1000000000 * 1024);
printf("%-30s %11s %11s %11s\n", "", "avg latency", "stddev", "iops")
printf("%-30s %9us %9us %bu/s %8uk/s\n", @a, @v, @i, @b);
```

在系统承受正常负载时多次运行脚本，以获得延迟和吞吐量的准确基准。

`dtrace -s rw.d -c 'sleep 30'`

`sleep` 命令告诉脚本花费多长时间收集数据。`rw.d` 脚本监控这几秒钟内的吞吐量和延迟，然后打印读取和写入两张图表。最后你将得到如下所示报告：

| avg latency | stddev | iops | throughput |

| :--- | :--- | :--- | :--- |

| write | 1362us | 8378us | 68/s | 4620k/s |

| read | 6943us | 5839us | 2/s | 46k/s |

通而言之，性能调优的目标是在提高你关心的数字的同时，不让其他数字变得太大。尝试调整每类型允许的最大读取和写入次数，在每次运行之间增加 20–100%。确保不要将这些值调得太高以至于你的 VDEVs 超过了每个 VDEV 的限制——或者，尝试调整最小值。

`stddev`（标准差）列特别值得注意。你可能获得了卓越的吞吐量，但发现延迟波动很大。如果你的某些读取和写入需要五秒才能完成，巨大的吞吐量还可以吗？只有你知道。



在调整读取性能时，注意 ARC。如果你一直访问同一个文件，内核将使用内存中的副本而不是从磁盘重新读取。为了正确测试读取性能，请清除缓存。

# I/O 队列

ZFS 将 I/O 分为几个队列：同步写入、异步写入和校验（scrub）。每个队列中未处理的请求数受 `sysctls` 限制。

同步写入程序使用 `fsync(2)` 系统调用的地方。这些请求直接进入 `ZIL`，是在独立的 `SLOG` 上还是磁盘上。这些写入是最重要的，因为应用程序正在等待操作完成。调整此值会降低吞吐量并增加延迟。

异步写入是不经过 `ZIL` 的正常流量。异步写入保留在 `txg` 中，然后批量提交。

校验进程有自己的队列，控制池中同时可以有多少个活跃的 I/O 请求。

同步读取最大：10

异步读取最大：3

同步写入最大：10

异步写入最大：10

清洗最大：2

一个具有最大可能并发请求数的磁盘将会有 35 个待处理请求。一个 10 块磁盘的 VDEV 可以有 350 个并发待处理请求，而 29 块磁盘的 VDEV 可以有 1015 个并发待处理请求。

观察每类型的请求，你会发现这是一个相当平衡的计划。同步和异步写入都有自己的队列，因此你的写入不会过载 `ZIL`（同步日志）。只要降低异步预取读取，你就可以获得大量的读取，这样 ZFS 对你的程序将要访问数据的猜测就不会阻塞活跃的流量。

更改这些值会调整 ZFS 分配请求的方式。你希望系统偏向于写入数据吗？增加异步写入的数量。你想要快速清洗吗？提高清洗请求的上限。

然而，你无法通过提高这些设置来提升硬件速度。现有的限制已经足以完全饱和一个 5400 转的 SATA 硬盘。对于具有读写分离硬件的高端存储设备，可能可以处理略高的值。即使如此，你很快就会达到最大容量。

对于固态存储（如 SSD），其 IOPS 远大于旋转硬盘，通过增加其所有调优参数可以提高性能。为了从设备获得最大的性能，你必须给它足够的工作来保持忙碌，但同时工作不能太多，以免导致重要的请求排在队列末尾时等待太久。使用本章节前面提供的 DTrace 脚本测量负载下的延迟并根据需要进行调整。

但如果你拥有顶级的硬件并将限制提高过高，就会触及每个 VDEV 的限制，改变一切。

## 调度大型 VDEV

ZFS 有两个调度系统：一个用于系统允许许多待处理 I/O 请求的情况，另一个用于系统不允许的情况。多少算“许多”？这取决于你的 VDEV 和宿主机。

`sysctl vfs.zfs.vdev.max_active` 给出了 ZFS 更改调度算法的标记位。FreeBSD 的默认值是 1000。对于大多数主机，在默认配置下，这意味着在切换算法之前，一个 VDEV 可以包含 28 块磁盘。如果你更改了 I/O 队列，你就改变了计算方式。

达到限制意味着 ZFS 改变了调度方式。它不再将最大值作为上限，而是允许每块磁盘拥有等于最小值的待处理请求数。

- 同步读取最小：10
- 异步读取最小：3
- 同步写入最小：10
- 异步写入最小：1
- 清洗最小：1

这意味着每块磁盘至少获得 25 个待处理请求。系统默认可以支持多达 1000 个待处理请求，因此任何额外的请求将按优先级顺序分配。

如果你在单个 VDEV 中有超过 40 个存储提供者，即使是最小值也超过了系统允许的总数。要么更改 `vfs.zfs.vdev.max_active` 以允许更多请求，或者（最好）重新排列你的 VDEV，使其包含合理数量的存储提供者。

## 异步写入与事务组大小

异步写入的工作方式略有不同。当系统大部分时间空闲且没有太多要写入时，系统会创建一个异步写入请求。（从技术上说，最小数量是 `vfs.zdev.async_write_min_active`，但没有理由将其高于 1。） 内存中等待写入磁盘的数据被称为“脏数据”。随着事务组（`txg`）大小和频率的增加，ZFS 会调度更多的并发写入。当系统达到 `vfs.zdev.async_write_max_active` `sysctl` 定义的最大写入请求数时，它开始人为地放慢写入。

`vfs.zdev.async_write_min_percent` 和 `vfs.zdev.async_write_max_dirty_percent` 控制 ZFS 如何添加写入请求。这些是系统允许脏数据的百分比——事务组的最大大小。在最小百分比以下，系统使用最小写入请求数，留出更多带宽。在最大百分比及以上，系统使用最大写入请求数以匹配需要写入的数据。请求数在它们之间线性缩放。

默认情况下，最小百分比是 30，最大是 60。异步写入的数量是 1，最大是 10。这是如何运作的？

假设 `vfs.zdev.dirty_data_max` 设置为 1 GB，这使得计算变得简单。一个事务组只能是 1 GB。如果宿主机有 300 MB 数据准备好写入（即 1 GB 的 30%），它使用单个写入请求。每超过 300 MB 的脏数据就会增加另一个写入请求。如果宿主机有 600 MB 数据准备好写入（即 1 GB 的 60%），它会队列 10 个写入请求。

在理想情况下，系统在正常负载下运行时，事务组的大小应该处于最小和最大值之间。

## 清洗（Scrub）与重构（Resolver）性能

任何在大型企业工作过的人都经历过过完全适用于现代硬件的维护窗口策略的苦扰。Lucas 曾多次在工作期间延迟更换故障的热插拔硬盘，因为公司的维护政策规定周日是进行维护的唯一时间。如果你受限于这类政策，那么让重构（resolvers）和清洗（scrubs）快速完成就至关重要，这样你才能继续你当天的工作。

清洗和重构具有内置的速率限制，以确保这些操作不会干扰正常运行。如果任何其他进程需要 I/O，这些维护操作就会延迟。加速清洗和重构意味着要限制速率。

速率限制是一个 `sysctl` 参数，它为该进程的每次 I/O 操作之间留出时间。这种速率限制仅在磁盘非空闲时生效。

延迟以系统时答（ticks）为单位。每秒的时答数由 `kern.hz` `sysctl` 控制。该默认值为 1000，尽管许多虚拟机和笔记本电脑用户可能为了提高性能而将其设置为 100。

“非空闲”到底意味着什么？磁盘必须持续等于 `vfs.zfs.scan_idle` `sysctl` 数值的时答时间内没有任何活动。

`vfs.zfs.resolver_delay` `sysctl` 控制重构的这种人工延迟，而 `vfs.zfs.scrub_delay` 则处理清洗。默认情况下，清洗在操作之间等待四个时答，而重构延迟两个时答。如果 ZFS 每次 I/O 睡眠四个时答，那么在非空闲池上清洗产生的最大 IOPS 将是 250 IOPS（每秒 1000 时答除以每次操作四个时答）。其他进程可以在这些阶段执行 I/O。运行这些操作会进一步延迟清洗或重构。

其他 OpenZFS 消费者（如 illum）通常使用每秒 100 个时答。FreeBSD 的延迟只有大多数其他操作系统的十分之一。这可能是一个疏忽，而不是刻意的设计决策。

要消除清洗或重构延迟，请将这些值设置为 0，使你的维护任务与其他任何进程具有相同的优先级。请记住，这些延迟仅在池中存在其他活动时才会触发。

你可以控制清洗发送到 I/O 调度器的数据量。增加队列深度为 ZFS I/O 调度器提供了更有效运行的机会。`vfs.zfs.top_maxinflight` 控制清洗的 I/O 队列深度。它的默认值为 32，有些人将其调高到 2048。增加过高会耗尽系统内存，因此在调整清洗时要密切监控系统。

每个 `txg`（事务组）在重验证（resverifying）上花费的时间有限。默认情况下，一个 `txg` 在重验证上花费至少 3000 毫秒。`vfs.zfs.resilver_min_time_ms` 控制事务组在重验证 I/O 上花费多少时间。当没有进行重验证时，此值会被忽略。

无论你做什么，最终你都会达到硬件对于工作负载的极限。重新排列瓶颈就像在邮轮船上重新布置甲板椅。在某些船上，你可以为一场精彩的滑板游戏腾出空间。然而，如果这艘船是泰坦尼克号，无论如何移动资源都无法让你浮起来。

> Lucas 将很多事情称为“重新排列瓶颈”。他通过花费时间和洗涤剂资源来解决“脏衣服”瓶颈。在你读这段字的精确时刻，他几乎肯定正遭受冰淇淋瓶颈的困扰。

> 这些是平均值，所以不要让 ZFS 认为 2+2=5 的事实让你担心。ZFS 的校验功能计算数学更加准确。

> 你可以在启动后后更改 `vfs.zfs.dirty_data_max_percent`。它不会以任何方式影响系统性能，但你可以更改它。

> 并不是 Lucas 记得由于这种愚蠢浪费的每一分钟。也没有列出那些政策浪费了他周末的人员。或者在等待 Kneecappers Inc 对其报价请求的正式回复。

# 第 9 章：优化

学习 ZFS 的系统管理员通常会花时间对 ZFS 的空间使用感到头疼。池化存储、数据集、快照和克隆使得 ZFS 空间利用变得非常复杂，以至于在《FreeBSD Mastery: ZFS》中专门用了一整章。当你开始折腾数据集和 `zvols` 的 `recordsize` 和 `volblocksize` 属性时，利用率可能会直接进入“神秘领域”。



`volblocksize` 属性给出了 zvol 上一个块的大小。该块的大小应该代表在 zvol 上使用的文件系统块。默认的 `volblocksize` 为 8 KB，它可以容纳两个 4 KB 或十六个 512 字节的扇区。

`recordsize` 属性给出了 ZFS 数据集中逻辑块的最大大小。默认的 `recordsize` 为 128 KB，在 4 KB 扇区的磁盘上相当于 32 个扇区，在 512 字节扇区的磁盘上相当于 256 个扇区。随着 `large_blocks` 特性的引入，最大大小被增加到了 1 MB。许多数据库引擎更倾向于较小的块，例如 4 KB 或 8 KB。对于此类此类文件的数据集，更改 `recordsize` 是有意义。即使你不这样做，ZFS 也会根据需要自动调整大小。写入 16 KB 的文件应该只占用 16 KB（加上冗余空间），而不是浪费整个 128 KB。
块大小与冗余之间的交互意味着磁盘可能会突然填满，尽管它们只占了你预期的数据的 25%。理解为什么需要深入研究。

## 镜像（Mirrors）与条带（Stripes）
镜像和条带需要元数据来附加 ZFS 树，但它们不需要额外的冗余块。我们的 8 KB 使用两个 4 KB 或十六个 512 字节的扇区。

## RAID-Z1
在 4 KB 扇区的 RAID-Z1 池上，8 KB 的数据本身需要两个块。我们需要一个块作为校验数据，总共三个块。RAID-Z1 允许以二的倍数分配块（校验位+1），因此会向上取到四个块。假设你有三盘 RAID-Z1，如果磁盘是 4 KB 扇区，这种配置意味着你只能填满磁盘。填充会消耗剩余空间。
在 512 字节扇区的三盘 RAID-Z1 上，同样的 8 KB 占用 16 个块。我们需要一个校验块，总共 17 个块。分配必须能被二整除，所以池分配一个填充块，使总数达到 18 个块。

## RAID-Z2
在 4 KB 扇区的 RAID-Z2 池上，8 KB 的数据再次占用两个块。我们需要两个块作为校验数据，总共四个块。RAID-Z2 池允许以三的倍数分配块（校验位+1），因此这会向上取到六个块。在四盘 RAID-Z2 上，你预计能够填满磁盘的一半。但如果你用 8 KB 块填充池，你只能填满 33%。

## RAID-Z3
在具有 4 KB 文件系统扇区的 ZFS 上，数据本身需要两个扇区。该池使用三重校验，因此你需要三个磁盘扇区作为校验数据。对于 4 KB 扇区，RAID-Z3 允许你以四的倍数分配扇区，因此 ZFS 为这 8 KB 数据分配八个扇区。八个扇区是 32 KB。你无法将这个 zvol 填充超过 25%。只要池有 800 GB 的物理空间，你可以完全填充一个 200 GB 的 zvol。
在具有 512 字节文件系统扇区的 ZFS 上，数据本身需要 16 个扇区。它还需要另外三个扇区作为校验数据，总共 19 个扇区。由于分配必须是四的倍数，这次写入将被分配 20 个文件系统扇区。二十个扇区是 10 KB，给你 80% 的效率。

# 条带化镜像 (Striped Mirrors)
条带镜像不需要任何校验数据。ZFS 将数据整体地复制到多个存储提供者。条带镜像不会为了适应分配大小而填充数据。条带镜像是存储数据最高的地方，但它的数据保护模型与 RAID-Z 不同。
三路镜像提供与 RAID-Z2 类似的数据保护——你可以从每个 VDEV 中丢失两个驱动器而不会丢失数据——但你只能获得总空间的的 33%。

# 更改分配大小
将 `recordsize` 或 `volblocksize` 更改为 4 KB 会改变计算结果。较小的条带大小意味着更多的校验数据，这可能意味着更多的空填充。
看看我们对 RAID-Z3 上的 8 KB 写入示例。它被分成两个条带。在具有 4 KB 块的 zvol 上，每个条带需要四个扇区，这同样导致了 25% 的空间效率。使用 512 字节块时，每个条带需要 11 个块，并向上取整到 12 个。你将获得大约 66% 的空间效率。
条带大小（`volblocksize`）、校验数据和填充之间的相互作用，就是为什么你不需要对文件系统数据集执行这些计算的原因。128 KB 的条带大小可以将分配填充减少到更少。

# 建议
在为数据库或 zvols 设置系统之前，请仔细考虑数据池底层的存储。对于我们强烈推荐的 8 KB 常用 `recordsize` 设置，建议顺序为：镜像条带池（mirrored stripe pool）、四驱动 RAID-Z2 池，或三驱动 RAID-Z 池。
如果你正在使用 `volblocksize` 为 4 KB 的 zvol 来支持虚拟机，你的选择会更加有限。镜像条带池允许你获得最大的空间效率，而所有其他大小都会由于填充导致至少的空间损失。镜像在 IOPS 方面相比 RAID-Z 具有巨大的优势。

# 数据库与 ZFS
许多 ZFS 特性对数据库非常有利。每个 DBA 都希望有快速、简单且高效的复制、快照、克隆、可调缓存和池化存储。虽然 ZFS 被设计为通用文件系统，但你可以对其进行调优，让你的数据库飞起来。
数据库通常由多种类型的文件组成，每种文件都有不同的特征和使用模式，且都需要不同的调优。我们将专门讨论 MySQL 和 PostgreSQL，但这些原理适用于任何数据库软件。
你可以为可以执行的最重要的调优是数据集块大小，通过 `recordsize` 属性实现。对于任何可能被覆盖的文件，都必须与应用程序使用的块大小匹配。
调优块大小还可以避免写放大（write amplification）。写放大发生在当更改少量数据却需要写入大量数据时。假设你必须更改 128 KB 块中间的 8 KB。ZFS 必须读取这 128 KB，修改其中某处的 8 KB，计算新的校验和，并写入新的 128 KB 块。ZFS 是一个写时复制（copy-on-write）文件系统，因此它将为了更改那 8 KB 而最终写入整个 128 KB 块。这并不是你希望看到的。现在将此乘以你数据库的写入次数。写放大会损害性能。
虽然这种优化对我们许多人来说并不是必要的，但对于高性能系统来说，它可能是无价的。它还会影响 SSD 以及其他闪存存储的寿命，这些设备在整个寿命内只能处理有限的写入量。当然，不同的数据库引擎并没有让这变得容易，每个引擎都有不同的需求。日志、二进制复制日志、错误和查询日志以及其他文件都需要不同的调优。
在创建具有小 `recordsize` 的数据集之前，请确保你理解 VDEV 类型与空间利用之间的相互作用。在某些情况下，具有较小的 512 字节扇区数的磁盘可以提供更好的存储效率。你完全可能为你的数据库专门设置一个独立的池更好，而将主池用于你的其他文件。
对于高性能系统，请使用镜像而非任何类型的 RAID-Z。是的，为了韧性，你可能想要 RAID-Z。选择你的痛苦点。¹

# 所有数据库
在数据库上启用 `lz4` 压缩，不直觉地实际上可以降低延迟。
压缩数据可以更快地从物理介质读取，因为需要读取的内容更少，从而导致更短的传输时间。`lz4` 的早期终止（early abort）功能在最坏的情况下只比禁用压缩慢几毫秒，但收益通常是非常显著的。这就是为什么 ZFS 对它所有的元数据和 `L2ARC` 使用 `lz4` 压缩。在不远的将来，当压缩 ARC 特性进入 OpenZFS 时，在数据集上启用压缩将允许更多数据保留在 `ARC` 中，这是 ZFS 最快的缓存。
在 Delphix 的一个生产案例中，一个拥有 768 GB 内存的数据库服务器使用超过 90% 的内存来缓存数据库，仅使用 46 GB 内存即可缓存 1.2 TB 的压缩数据。压缩内存缓存导致了显著的性能提升。由于机器无法支持更多内存，压缩是改进的唯一方法。
ZFS 元数据也会影响数据库。当数据库发生快速变化时，为每次更改写入两或三份元数据可能会消耗底层存储大量的可用 IOPS。通常，与 128 KB 的记录大小相比，元数据的数量相对较小。尽管如此，数据库的小记录大小运行更好。保留三份元数据可能会导致与向池写入实际数据的磁盘活动相当甚至更多。
较新的 OpenZFS 版本包含 `redundant_metadata` 属性，默认认为 all。将 `redund metadata` 设置为 off 可以节省 IOPS，但会增加损坏的风险。对于大多数数据库，默认值是可以的。然而，如果元数据开销是瓶颈，你可以对此进行调优。
一旦压缩 ARC 特性可用，明智的做法可能是减小数据库内部缓存的大小，而是让 ZFS 处理缓存。在相同的内存中可以容纳更多数据。

# MySQL – InnoDB/XtraDB
InnoDB 在 MySQL 5.5 中成为默认存储引擎，其特性与 MyISAM 有显著不同。Percona 的 XtraDB（也被 MariaDB 使用）与 InnoDB 类似。InnoDB 和 XtraDB 都使用 16 KB 的块大小，因此 ZFS 数据集的记录大小被设置为匹配。我们还建议使用 MySQL 的 `innodb_file_per_table` 设置，将每个表的 InnoDB 数据保留在单独的文件中，而不是将其分组到单个 ibdata 文件中。这使得快照更有用，并允许选择性的恢复或回滚。



在不同的数据集上存储不同类型的文件。数据文件需要 `16 KB` 块大小、压缩和减少元数据。你可能会看到仅缓存元数据带来的性能提升，但这同时也允许了预取（prefetch）。实验并观察你的环境表现如何。

```
# zfs create - recordsize=16k -o compress=lz4 -o redundant_metadata=most -o primarycache=metadata mypool/var/db/mysql
```

主 MySQL 日志用 `gzip` 压缩效果最好，且不需要内存缓存。

```
# zfs create -compress=gzip -o primarycache=none var/log/mysql
```

复制日志使用 `lz4` 压缩效果最好。

```
# zfs create -compress=lz4 mypool/var/log/replication
```

通过 `/usr/local/etc/my.cnf` 设置让 MySQL 使用这些数据集。

```
data_path=/var/db/mysql
log_path=/var/log/mysql
binlog_path=/var/log/mysql/replication
```

现在你可以初始化数据库并开始加载数据了。

# MySQL – MyISAM

许多 MySQL 应用程序在使用旧的 MyISAM 存储引擎，是因为它的简单，或者因为它们还没有转换为使用 InnoDB。

MyISAM 使用 `8 KB` 的块大小。数据集记录大小应设置为匹配。除此之外，数据集布局应与 InnoDB 相同。

# PostgreSQL

如果调优得当，ZFS 可以支持非常大且快速的 PostgreSQL 系统。

在创建所需的数据集之前初始化你的数据库

PostgreSQL 默认对所有内容都使用 `8 KB` 的存储块。如果你更改了 PostgreSQL 的块大小，你必须更改数据集的大小以匹配它。

在默认的 FreeBSD 安装中，PostgreSQL 位于 `/usr/local/postgresql/data`。对于大型安装，你可能为这些数据准备了单独池（pool）。在这里，我为 PostgreSQL 使用名为 `pgsql` 的池。

```
# zfs create mountpoint=/usr/local/postgresql pgsql
# zfs create pgsql/data
```

现在我们遇到了一个先有鸡还是有蛋的问题。PostgreSQL 的数据库初始化例程期望创建它自己的目录树，但我们希望特定的子目录拥有自己的数据集。实现此的最简单方法是让 PostgreSQL 初始化，然后创建数据集并移动文件。

```
# /usr/local/etc/rc.d/initdb
```

初始化例程创建数据库、视图、架构、配置文件以及高级数据库的所有其他组件。现在你可以为特殊部分创建数据集了。

PostgreSQL 将数据库存储在 `/usr/local/postgresql/data/base`。写预读日志（WAL）位于 `/usr/local/postgresql/data/pg_xlog`。将这两者都移开。

```
# cd /usr/local/postgresql/
# mv base base-old
# mv pg_xlog pg_xlog-old
```

这两者都使用 `8 KB` 的块大小，你可能希望分别对它们进行快照，以便为每个创建一个数据集。对于 MySQL，告诉 ARC 只缓存元数据。还要通过 `logbias` 属性告诉这些操作绕过延迟。

```
# zfs create recordsize=8k -o redundant_metadata=most -o primarycache=metadata logbias=throughput pgsql/data/pg_xlog
# zfs create recordsize=8k -o redundant_metadata=most -o primarycache=metadata logbias=throughput pgsql/base
```

将原始目录的内容复制到新数据集中。

```
# cp -Rp base-old/*
# cp -Rp pg_xlog-old/* pg_xlog
```

你现在可以启动 PostgreSQL 了。

## 针对文件大小调优

ZFS 设计为一种优秀的通用文件系统。如果你有一个 ZFS 系统作为典型办公室的文件服务器，你并不需要针对文件大小进行调优。然而，如果你知道你将拥有多大的文件，可以进行更改以提高性能。

### 小文件

在没有 SLOG（专用日志设备）的系统中高速创建许多小文件时，ZFS 会花费大量时间等待文件和元数据刷新到稳定存储中。

如果你愿意承担最后五秒内创建的任何新文件的丢失风险（如果你的 `vfs.zfs.txg.timeout` 较高），将 `sync` 属性设置为 `disabled`，这将告诉 ZFS 将所有写入视为异步。即使应用程序请求不要在文件安全之前通知它写入已完成，ZFS 也会立即返回，并随下一个定期计划的 txg 一起写入文件。

高速 SLOG 让你能够既同步又快速地存储那些微小文件。

### 大文件

ZFS 最近通过 `large_block` 特性增加了对大于 `128 KB` 块的支持。如果你正在存储许多大文件，务必考虑这一点。默认的最大块大小为 `1 MB`。

理论上，你可以使用大于 `1 MB` 的块大小。然而，很少有系统对此进行过广泛测试，而且与内核内存分配子系统的交互在长时间使用中尚未经过测试。你可以尝试使用大的 `recordsize`，以便在一切出现问题时寻求一个文件报告。`sysctl vfs.zfs.max_recordsize` 控制最大块大小。

一旦你激活了 `large_blocks`（或任何其他特性），该池将无法被不支持该特性的主机使用。通过删除任何曾经设置过 `recordsize` 的数据集来禁用该特性。

一旦池完成了驱动器的重构（resilvering），你就可以拆分该池。

## 拆分池

使用 `zpool split` 命令从每个 VDEV 中提取设备来创建一个新池。该命令有强制性参数：你想要拆分的池名称以及新创建池的名称。在这里，我们拆分 `db` 池，在 `db2` 池中创建一个完全相同的副本。

ZFS 会移除每个镜像（mirror）中最近添加的设备，以此创建一个新池。

拆分池不会自动导入新池。一旦你导入了它，拆分后的池看起来如下：

```
# zpool status db2
...
NAME      STATE READ WRITE CKSUM
db2      ONLINE 0     0      0
gpt/zfs4 ONLINE 0     0      0
gpt/zfs5 ONLINE 0     0      0
```

此池包含两个条带化（striped）磁盘。

在原始池中，三路镜像的条带对已变为双路镜像的条带对。

如果你打算长时间保留这个拆分出来的池，你应该添加更多磁盘以创建适当的镜像。不过，如果你只是从这些驱动器提取备份，则可能不需要再添加一组磁盘。

## 快照规范

快照非常棒——但它们会带来很多麻烦（tribbles™）。一旦你习惯了使用快照来处理系统管理问题，你会发现自己因为拥有这么多快照而面临磁盘存储空间不足。删除单个快照很容易。

```
# zfs destroy mypool/dataset@snapshotname
```

但如果你想一次删除 10 个快照呢？识别每个快照并在命令行中指定每一个是非常繁琐的。

ZFS 允许你通过快照规范（snapspec）识别多个相邻的快照。你不能使用 `snapspec` 指定多个互不连续的快照，但如果你想删掉从 `@monday` 到 `@saturday` 的每日快照，`snapspec` 就是你的助手。

每当你使用 `snapspec` 时，我们建议带有 `-n` 和 `-v` 参数运行命令。`-v` 告诉 `zfs(1)` 详细打印命令的操作。`-n` 告诉它不要实际执行任何操作。两者结合起来的作用是“详细告诉我此命令将具体执行什么”。由于你可以分配任意的快照名称，最好验证一下某个需要但遗忘的快照不会被“快照大杀”误伤。一旦你确定了命令将删除哪些快照，就不带 `-n` 重新运行命令。

## 快照范围

基本的 `snapspec` 格式是 `fromsnap%tosnap`。它会删除两个标记之间的每一个快照，包括它们本身：

```
# zfs destroy -vn mypool/dataset@one@three
would destroy mypool/dataset@one
would destroy mypool/dataset@two
would destroy mypool/dataset@three
```

如果你在带编号的快照之间滑入了一个 `@beforeUpgrade` 快照怎么办？这就是为什么要先使用 `-n` 的原因。

## 按年龄指定



你可以使用 `@foo` 删除 `snapshot@foo` 以及任何比它旧的快照。

```
# zfs destroy -vn mypool/dataset@four
would destroy mypool/dataset@one
would destroy mypool/dataset@two
would destroy mypool/dataset@three
would destroy mypool/dataset@four
```

同样，使用 `@foo%` 删除 `@foo` 以及任何比它更更新的快照：

```
# zfs destroy -vn mypool/dataset@six%
would destroy mypool/dataset@six
would destroy mypool/dataset@seven
would destroy mypool/dataset@eight
would destroy mypool/dataset@nine
would destroy mypool/dataset@ten
```

这比重新输入每个快照要简单得多。

## 快照大屠杀 (Snapshot Slaughter)

有时，你想删除所有快照。使用 `@%` 将它们全部付之一于炬。

```
# zfs destroy -vn mypool/dataset@%
would destroy mypool/dataset@one
would destroy mypool/dataset@two
...
would destroy mypool/dataset@ten
```

现在你可以再次开始积累快照了。

如果你拍摄了递归快照，你可能想删掉整个树。添加 `-r` 可以清除某个数据集及其所有子数据集的快照。在这里，我们已经完成了升级，并且对结果表示满意：

```
# zfs destroy -nvR pgsql/data%
would destroy pgsql/data@beforeupgrade
would destroy pgsql/data/base@beforeupgrade
would destroy pgsql/data/pg_xlog@beforeupgrade
```

但是，你知道的……我们想再多留那些备份。

## 恢复已删除的池 (Recovering Destroyed Pools)

当你意识到“等一下，那个命令是个可怕的错误！”时，没有什么比这更糟糕了！你试图停止，但你知道神经冲动在手指按下回车键之前就已经大脑。

在删除 ZFS 池时可能会发生这种情况。ZFS 的设计者非常清楚这种症状。

`zpool destroy` 命令实际上并没有损坏底层磁盘上的任何数据。相反，它将池标记为已删除。`zpool list` 会跳过标记为已删除的池。如果你没有向已删除池下的磁盘写入数据或物理移除磁盘，你就可以恢复该池。使用 `zpool import` 的 `-d` 参数可以查看已删除的池。

```
# zpool import -D
```

你会得到两种响应，针对可恢复的池和不可恢复的池。

### 可恢复的池 (Recoverable Pools)

这是一个你可以轻松恢复的池。

```
# zpool import -D
pool: db2
id: 555215874600692385
state: ONLINE
action: The pool is
config:
  db2
  gpt/zfs4
  gpt/zfs5
```

此池包含两个条带化磁盘。

在原始池中，三路镜像的条带对已变为双路镜像的条带对。

如果你打算长时间保留这个拆分出来的池，你应该添加更多磁盘以创建适当的镜像。不过，如果你只是从这些驱动器提取备份，则可能不需要再添加一组磁盘。

### 不可恢复的池 (Non-Recoverable Pools)

其他池就不容易了。

```
# zpool import -D
pool: db
id: 131227496263209
state: DESTROYED
action: The pool is missing
config:
  db2                DEGRADED
```

### 恢复时重命名 (Rename at Recovery)

有时你想在恢复时重命名池。也许它与某个运行中的池同名，或者池的功能发生了变化。在导入时重命名池，在旧池名称之后添加新名称。在这里我们导入已删除的 `db2` 池并将其重命名为 `olddb2`。

```
# zpool import -D olddb2
```

其余与重命名导入池相同。

## 克隆机器 (Cloning Machines)

ZFS 是虚拟机非常明智的选择。虽然失去对磁盘的直接访问意味着 ZFS 可以为你处理错误，但快照和复制等功能使得 ZFS 变得有利。

大多数虚拟化系统都会为你克隆系统，有时伪装成你可以部署的模板。但是，如果你将包含 ZFS 池的磁盘镜像复制到新的虚拟机，那么你的虚拟机就是原始机的副本。这意味着某些应该是全局唯一的项不再是唯一的了。这在独立的虚拟机上会产生问题吗？但如果你要在虚拟机之间移动磁盘镜像，你将需要更改每个虚拟机池的 GUID。

`guid` 属性包含池的 GUID。在这里我们获取 `db2` 池的 GUID。

```
# zpool get guid db2
NAME PROPERTY VALUE SOURCE
db2 guid 5552158746006792385 default
```

要生成新的池 GUID，使用 `zpool reguid`。将池名作为参数。

```
# zpool reguid db2
# zpool get guid db2
NAME PROPERTY VALUE SOURCE
db2 guid 76624604609377566669 default
```

现在你可以将一个虚拟机的磁盘镜像连接到另一台虚拟机，而不会让 ZFS 发脾气。

如果由于某种原因 `zdb(8)` 找不到你的 `pool.1234`，给池分配一个新的 GUID 也有帮助。

## 不区分大小写的文件系统

某些客户端（特别是 OS X）期望文件系统是不区分大小写的。你可以通过 `casesensitivity` 属性让 ZFS 数据集不区分大小写。

`casesensitivity` 属性默认是 `sensitive`，即传统的 Unix 风格区分大小写。如果你将其设置为 `mixed`，ZFS 可以支持区分大小写和不区分大小写的请求。将 `casesensitivity` 设置为 `insensitive` 意味着 ZFS 将完全不区分大小写。

你只能在创建数据集时设置此属性。

```
# zfs create -o casesensitivity=mixed samba/share
```

要更改现有数据集的大小写敏感性，创建一个正确设置属性的新数据集，然后将文件复制过去。

## ZFS 深度解析：zdb(8)

为了更好地了解 ZFS 内部正在发生什么，能够窥探幕后情况会有帮助。检查 ZFS 的内部状态可以帮助你理解系统为何以这种方式运行运行。即使你对“香肠是如何制作的”不感兴趣，本节也可能包含一些感兴趣的点。

许多人阅读《FreeBSD 系统的设计与实现》第 2 版，Addison-Wesley Professional, 2014 中的 ZFS 章节来学习 ZFS 的内部数据结构。虽然该书提供了大量信息，但对系统中的实际文件研究这些数据结构的能力会让一切更有意义。

FreeBSD 提供的 ZFS 工具套包含 `zdb(8)`，它是 ZFS 调试器。`zdb(8)` 手页明确指出：“命令的输出通常指的是 ZFS 池的磁盘上结构，并且在本质上是不稳定的。大多数调用的精确输出均未记录，假设用户了解 ZFS 内部原理。”输出基于磁盘上的内容以及 `zdb(8)` 对任何时刻内存中内容的模拟。解释工作很大程度上留给了操作员。如果你真的深入研究 `zdb(8)`，你可能需要手头准备一份《设计与实现》以供参考。

`zdb(8)` 命令有许多标记。其中大多数标记可以指定多次，以增加信息的详细程度。

### 块统计

`zdb(8)` 实用可以检查池中块分配的分类情况。我们将从检查一个虚拟机的极小池开始，然后增加较大的池。使用 `-b` 标记和池名称来获取该池的块统计。

分析块统计需要大量内存，因为 `zdb(8)` 在计算各种统计数据时必须跟踪每一个块。非常大的池可能需要的内存超过宿主机内存，最终内核的 OOM 杀手会为了保护系统而终止 `zdb`。在生产系统上运行此命令时要小心，因为 `zdb(8)` 可能会导致系统停顿。

让我们从虚拟机的小型单磁盘池开始。

```
# zdb -b mypool
traversing all blocks to verify nothing leaked...
925M completed ( 473MB/s) estimated time remaining: Uhr 00min 00sec
No leaks (block matches space maps exactly)
```



```
bp count: 85010
ganged count: 0
bp logical: 2159973376 avg: 25408
bp physical: 89729176 avg: 10555 compression: 2.41
bp allocated: 1159446528 avg: 13638 compression: 1.86
bp deduped: 0 ref>1: 0 deduplication: 1.00
SPA allocated: 1159446528 used: 5.72%
```

额外的、非指针类型的块数量：5873

同一 `vdev` 上的 Dittoed 块：9645

统计数据的第一部分涵盖了指针，即包含数据块元数据和索引细节的块。`bp count` 字段显示池中有多少个块指针——这里是 85,010 个。

`bp logical` 字段显示逻辑空间的总量，或这些块的实际大小。这些块指针指向 2,159,973,376 字节，约 2 GB。平均块指针处理约 25,408 字节。

`bp physical` 数量显示这些块在磁盘上消耗了多少空间。这就是压缩优势显示的地方。虽然我们有大约 2 GB 的文件，但显示我们使用了大约 800 MB 的磁盘空间来存储文件。但这并不是全部。

`bp allocated` 数字给出了真实世界的磁盘空间消耗情况。扇区大小、填充和校验意味着我们没有获得压缩提供的全部节省。这台服务器的真实压缩系数为 1.86，将那 2 GB 进了 1.1 GB——这是重大的。

这里有一个来自活动服务器的较大池，只有一个单磁盘 `VDEV`：

例如池的 `GUID` 以及如果主机正在使用该池，则 `hostid`。该池已有 15,612,202 个事务组被提交。`vdev_children` 字段显示此池中包含多少个 `VDEV`。

池的 `VDEV` 信息以树状形式显示，列出每个 `VDEV` 及其该 `VDEV` 中的磁盘。这里是媒体池中的一个 `VDEV`。

```
children[0]:ntype: 'raidz'
id: 0
guid: 85916174893029042218
parity: 2
metaslab_array: 30
metaslab_shift: 37
ashift: 12
asize: 179906354872232
is_log: 0
create_txg: 4
```

你还记得在创建 `VDEV` 时指定过偏移量（shift）吗？在这里你可以找到它的值。你还会看到 `VDEV` 的 `GUID` 和类型，以及其他 `ZFS` 内部机制的细节。

`VDEV` 中的每个磁盘也会获得条目。

```
children[0]:ntype: 'disk'
id: 0
guid: 14921375587032757624
path: '/dev/ada1p3'
phys_path: '/dev/ada1p3'
whole_disk: 1
DTL: 8495
create_txg: 4
```

这会告诉你最底层的信息：`ZFS` `GUID`、FreeBSD 设备节点以及一些内部细节。

在最底部，你会看到此池的只读特性列表。

`features_for_read`:

`.delphix:hole_birth`

`.delphix:embedded_data`

如果你在使用池名称的同时使用第二个 `-c`，`zdb` 会同时检索磁盘数据和缓存数据，以便你进行比较。它们之间会有差异吗？并不会。

## 数据集信息

详细检查数据集也可以提供很多信息，并帮助文件系统内部机制的可可视化。

## 数据集基础

要查看数据集的基本内部信息，请使用 `-d` 和数据集名称。在这里，我们检查上一节中使用的媒体池上的数据集。

### `zdb - media/svn/base`

`Dataset media/svn/base[ZPL], ID 4778, cr_txg 4820082, 3.82G, 259339 objects`

这并没有提供多少信息。`cr_txg` 字段显示创建此数据集的事务组，是该池中 15,612,202 个中的第 4,820,082 个。它持有 3.82 GB 的数据，其中包含 259,339 个对象。对象包括文件和目录，还包括元数据、`ACL` 以及 `ZFS` 可以包含任何其他类型。

## 数据集详情

想要更多细节吗？添加第二个 `-d` 并坐好。你可能需要运行此脚本(1) 或另一个终端录制程序。

### `zdb - media/svn/base`

`Dataset media/svn/base[ZPL], ID 4778, cr_txg 4820082, 3.82G, 259339 objects`

| Object | lvl | iblk | dsize | lsize | %full | type |
|---|---|---|---|---|---|---|
| 0 | 7 | 16K | 1K | 417M | 622M | 20.04 | DMU dnode |
| -1 | 7 | 16K | 1K | 0 | 1K | 100.00 | ZFS user/group used |
| -2 | 1 | 16K | 0 | 1K | 100.00 | ZFS user/group used |
| 2 | 1 | 16K | 16K | 16K | 512 | 100.00 | ZFS master node |
| 9 | 1 | 16K | 16.5K | 16K | 16.5K | 100.00 | ZFS directory |
| 11 | 3 | 120K | 43.3M | 155M | 82.49 | ZFS plain file |
| 13 | 1 | 16K | 512 | 8K | 512 | 100.00 | ZFS plain file |

这种情况还要持续到多久？

|  | lvl | iblk | dsize | lsize | %full | type |
|---|---|---|---|---|---|---|
| 1294291 | 1 | 16K | 3.50K | 8K | 3.50K | 100.00 | ZFS plain file |
| 1294324 | 1 | 16K | 4K | 8K | 4K | 100.00 | ZFS plain file |
| 1294328 | 1 | 16K | 4.50K | 8K | 4.50K | 100.00 | ZFS plain file |

这个数据集有一堆文件、目录和相关内容。几列可能让你感兴趣。`dblk` 列是每个对象的记录大小。`Isize` 是对象的逻辑大小，我们大多数人在说“文件大小”时想的是这个。第一行给了我们基本信息。但之后，我们看到了每个对象的细节。虽然前几个对象始终是 `ZFS` 元数据，但后面的对象大部分是文件和目录。你会看到分配给对象的值。

## 检查特定对象

这个数据集对象列表可能让你感兴趣，但这些每一个是什么呢？通过指定编号来检查对象。在这里我们加大力度，调查 `media/svn/base` 上的 1294328。

```
# zdb -ddd media/svn/base 1294328
Dataset media/svn/base[ZPL], ID 4778, cr_txg 4820082, 3.82G, 259339 objects
```

我们从关于数据集的细节开始，因为对象的创建数量是确切的。我们看到了许多更多细节，例如校验和等等。

```
Object iblk dsize lsize %full type
1294328 1 16K 4.50K 8K 4.50K 100.00 ZFS plain file
```

此文件为 4.50 KB，其磁盘大小（`dsize`）是 8 KB。我们得到了文件的内部结构。

```
dnode flags: USED_BYTES
dnode maxblkid: 0
path /head/sys/
uid 1001
gid 1001
atime 9 12:40:2015
mtime 9 12:40:2015
ctime 9 12:40:2015
gen 10832
mode 1064
size 4139
parent 12475
links 1
plflags 40800
Indirect blocks:
  L 0:1c092000:3000 1200/a00P F=1-b083255
200 size 4.50K
```

你会看到许多传统的 Unix 信息：权限、文件名、路径、父对象等。如果你用 `ls` 查看此文件，它的大小似乎是 4139 字节，但它并没有包含支持它的 `ZFS` 元数据。现在让我们考虑一个更大的、lz4 压缩的文件。

## `zdb -ddddd zstore/tmp 3628`

| Object | lvl | iblk | dblk | dsize | %full | type |
| --- | --- | --- | --- | --- | --- |
| 3628 | 2 | 16K | 128K | 244K | 100.00 168 | ZFS plain file |



这从基本证明开始，深入到文件本身。虽然这个文件占据 244 KB 的磁盘空间，但它的真实大小是 896 KB。压缩减少了所需的磁盘空间。但在 Unix 信息之后，我们可以获得间接块的列表。

间接块：

- 0 L0: 0:20ed2c20:00 4000L/1000P F=7 B=19665896/19665896
- 0 L0: 0:188fc2c00:c000 2000L/8000P F=1 B=19665895/1966585
- 20000 L0: 0:188fc2f800:c000 2000L/8000P F=1 B=19665895/1966585
- 40000 L0: 0:188fc2c00:c000 2000L/8000P F=1 B=19665895/1966585
- 60000 L0: 0:188fc2c00:c000 2000L/8000P F=1 B=19665895/1966585

第一列中的数字是块大小，如 2 的幂次方千 KB 所示。`$2^{13} = 8,192$`，所以是 8 KB。这个 metaslab 有 281 KB 的分配。

第 14 行是 16 KB。这个 metaslab 有 197 KB 的分配。

第 15 行是 32 KB，有 189 次分配，以此类推，直到单次 `$2^{32}`（或 4 GB）分配。

在查看内存中 metaslab 的直方图后，我们可以看到磁盘上版本的 metaslab 样子。在繁忙的磁盘上，ZFS 一直在分配和释放数据块。

```
On-disk histogram: fragmentation 0
13: 295 *********************
14: 198 ********************
15: 189 *******************
16: 107 *****************
17: 29 ****
18: 3 *
```

32: 1 *

向下滚动，不。最终，你会来到一个看起来截然不同的后期 metaslab。在本例中是 metaslab 43。

```
metaslab 43 offset 56000000000 spacemap 8280 free 59.16
segments 17893 maxsize 815M freepct 46%
```

这个 metaslab 有 17,893 次分配，但空闲比例为 46%。而且块大小分布明显不同。

```
In-memory histogram:
13: 891 *********
14: 565 *******************
15: 806 ****************
16: 994 *********************
17: 3341 *****************
18: 1452 *****************
19: 1932 **********************************
20: 4406 ************************************
21: 1557 *****************
22: 934 *************
23: 488 ***
24: 272 **
25: 103 *
26: 80 *
27: 47 *
28: 19 *
29: 6 *
```

我们最常见的分配是 17 (128 KB) 和 20 (1 MB)。

不过磁盘给出了为什么 metaslab 只有一半满的提示。

```
On-disk histogram:      fragmentation 11
13: 7520 *********************
14: 5782 *******************
15: 4096 *****************
```

注意碎片化程度——11。在磁盘上，metaslab 43 存在碎片化的。这意味着空闲空间块相对较小。对于机械硬盘，连续存储文件分块可以提高性能。当 ZFS 需要写入一个大块时，它可能会转向后期的 metaslab。

甚至可以进一步深入到你的 metaslabs 内部。

```
metaslab 121 offset f2000000000 spacemap 0 free 128G
segments 1 maxsize 128G freepct 100%
In-memory histogram:
37: 1 *
```

末尾附近的 slabs 由连续的 128 GB 块组成。如果这个存储池之前几乎是满的，编号较高的 metaslab 可能会包含数据碎片，而在此存储池中，它们尚未被触碰。

ZFS 通常将一个 VDEV 分为 200 个等大小的 metaslab。你可以通过 `vfs.zfs.vdev.metaslabs_per_vdev` `sysctl` 来调整这个数字，但你必须在创建 VDEV 之前设置该 `sysctl`。选择数字 200 是因为它看起来工作得很好，但在 metaslab 分配上有很大的实验空间。

当你通过更换为更大的磁盘来扩展 VDEV 时，ZFS 会创建 metaslab 来支持增加的空间。通过这种方式，你可以获得拥有远超 200 个 metaslab 的存储池。

ZFS 同时在内存中保留 metaslab 的数量有限。将 VDEV 扩展到原始大小会对性能产生负面影响，因为 ZFS 会在磁盘和内存之间移动 metaslab。

# Uberblock

如果不查看存储池的 uberblock，这还能是一个什么样的 ZFS 调试部分呢？

```
# zdb -u media
Uberblock:
magic = 00000000000bab10c
```

```
version = 5000
txg = 15741196
guid_sum = 7884957152936881795
timestamp = 1456030423 UTC = Sat Feb 20 23:53:43 2016
```

你能用这些做什么呢？没什么。但在这一刻，ZFS 几乎是赤裸裸地暴露在你面前。

你还能学到什么取决于你自己。

- 1 这件事发生过 Jude 身上，但 Lucas 确定这实际上是操作失误。
- 2 实际上，Jude 认为这可能与从旧版本升级存储池有关，因为这种情况最近在他所在的另外两台机器上也发生过。
- 3 在磁盘上，metaslab 43 存在碎片化的。这意味着空闲空间块相对较小。对于机械硬盘，连续存储文件分块可以提高性能。当 ZFS 需要写入一个大块时，它可能会转向后期的 metaslab。
- 4 在磁盘上，metaslab 43 存在碎片化的。这意味着空闲空间块相对较小。对于机械硬盘，连续存储文件分块可以提高性能。当 ZFS 需要写入一个大块时，它可能会转向后期的 metaslab。
- 5 在磁盘上，metaslab 43 存在碎片化的。这意味着空闲空间块相对较小。对于机械硬盘，连续存储文件分块可以提高性能。当 ZFS 需要写入一个大块时，它可能会转向后期的 metaslab。

# 不要错过 Michael W Lucas 的新发布！

订阅 Michael W Lucas 的邮件列表。
`https://www.michaelwlucas.com/mailing-lists`

# Michael W Lucas 的更多技术书籍

- 绝对 BSD（Absolute BSD）
- 绝对 OpenBSD（第1版和第2版）
- 绝望者的 Cisco 路由器指南（Cisco Routers for the Desperate，第1版和第2版）
- PGP 和 GPG
- 绝对 FreeBSD（Absolute FreeBSD）
- 网络流分析（Network Flow Analysis）

# IT 精通系列 (the IT Mastery Series)

- SSH 精通
- DNSSEC 精通
- Sudo 精通
- FreeBSD 精通：存储核心
- 系统管理员网络技术
- Tarsnap 精通
- FreeBSD 精通：ZFS
- FreeBSD 精通：特种文件系统
- FreeBSD 精通：高级 ZFS
- PAM 精通（即将推出）

FreeBSD 精通：高级 ZFS
版权 2016 所有 Allan Jude 和 Michael W Lucas。
保留所有权利。

作者：Allan Jude, Michael W Lucas
校对：Lindy Lou Lush
封面设计：Eddie Sharam，取材自 Schwind 的《圣沃尔夫冈与魔鬼》。

BSD Daemon 版权 1988 归 Marshall Kirk McKusick。保留所有权利。

本书中的信息按“原样”提供，不提供任何保证。在准备本书的过程中已尽了一切预防措施，但作者或 Tilted Windmill Press 对因书中包含的信息直接或间接造成或声称造成的任何损失或损害均不对任何个人或实体承担任何责任。

Tilted Windmill Press

`https://www.tiltedwindmillpress.com`
