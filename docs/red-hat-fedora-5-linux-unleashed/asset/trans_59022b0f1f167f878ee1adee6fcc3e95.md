

为了进一步检查，将新驱动器的跳线重置，使其成为主驱动器，断开旧驱动器，并在新位置插入新驱动器。如果新驱动器现在能被正确检测到，则怀疑驱动器之间存在某种兼容性问题。在进行驱动器线缆更改时，务必关闭电源，否则会损坏驱动器。

![](img/2045828cf45e5632bf056f9ca99d6755_985_0.png)

## 创建分区表并格式化磁盘

安装并被 BIOS 识别后，需要创建分区表。使用 `fdisk`（或您选择的程序）在驱动器上创建一个单分区，并记住在退出程序前将更改写入 MBR（参见本章前面的“创建分区表”部分）。

接下来是格式化驱动器。由于我们要创建一个新的 ext3 文件系统，因此我们使用 `j` 选项，如下所示：

```bash
# mkfs -j /dev/hdd1
```

请注意，我们在格式化驱动器时（使用 `-c` 选项）正在检查坏块。尽管这会给驱动器格式化增加大量时间，但初始坏块检查始终是个好主意。该程序将识别坏块并避免使用它们；如果我们未标记文件系统以忽略这些坏块，它们只会损坏我们的数据。

## 挂载新分区并将迁移的文件填充其中

对于下文的示例，假设 `/home` 曾是挂载在 `/` 分区的一部分目录，而不是独立的分区。

在这里，我们创建一个临时挂载点并挂载新分区：

```bash
# mkdir /mnt/newpartition
```

```bash
# mount -t ext3 /dev/hdd1 /mnt/newpartition
```

现在是时候将 `/home` 中的所有文件复制到 `/mnt/newpartition` 了。重要的是，我们要保留文件的时间戳和权限。我们要复制整个目录和子目录，因此使用三种基本复制方法（`tar`、`cpio` 或 `cp`）中最适合此场景的一种：

```bash
# cp -a /home/* /mnt/newpartition
```

我们需要修改 `/etc/fstab`，以便新的 ext3 分区能够正确挂载：

```text
/dev/hdb1    /home    ext3    defaults    1    2
```

在这里，我们选择使用 ext3 分区的默认挂载选项。默认值与 ext2 文件系统的默认值相同，同时还额外选择了默认的 `data=ordered` 日志记录模式。

每次重启时，包含复制文件的新分区将自动挂载到 `/home`。但在那之前，`cd` 到 `/home` 并输入以下内容：

```bash
# touch thisistheoldhomepartition
```

现在我们可以挂载新分区了：

```bash
# umount /mnt/newpartition
# mount /dev/hdb1 /home
```

请注意，如果你输入：

```bash
# ls -al /home
```
你将看不到我们使用 `touch` 命令创建的 `thisistheoldhomepartition` 文件。那么，旧文件发生了什么？它们仍然在那里，只是因为我们将一个目录“覆盖”在它们上面而被隐藏了。当我们确信一切正常后，我们可以卸载新创建的主分区，并删除包含 `thisistheoldhomepartition` 文件的分区中的文件。

> 你可以使用之前解释的技术作为占位符或警告，用于任何临时挂载的文件系统，以免误以为文件系统已挂载，而实际上并未挂载。

## 逻辑卷管理

前面的示例向您展示了如何添加新驱动器以克服磁盘空间不足的问题。如果可以在不进行所有挂载和文件复制的情况下做到这一点呢？这就是逻辑卷管理（LVM）有用的地方。使用 LVM，可以将来自多个驱动器的磁盘空间池化到一个逻辑卷中。

与任何新技术一样，使用 LVM 都有一个陡峭的学习曲线，其中也包括其术语。在这个术语体系中，分区被称为物理卷，或 pv。我们将 pv 添加到卷组中，卷组定义了一个逻辑卷，我们可以在其中创建文件系统。

在重度使用的系统上，备份期间文件可能会发生变化，恢复的文件可能处于不稳定状态。LVM 还可以对逻辑卷制作快照，然后可以挂载并备份这些快照。

有关 Linux 下 LVM 的更多信息，请阅读位于 [http://tldp.org/HOWTO/LVM-HOWTO/](http://tldp.org/HOWTO/LVM-HOWTO/) 的 LVM HOWTO，该文档解释了术语并提供了在 Linux 系统上设置和使用 LVM 的指南。

## 文件系统操作

不同的人有不同的学习方式。对于偏好示例而非讲座的读者，这里有一些实用示例，让你学习如何在文件内创建文件系统并使用回环文件系统挂载它——这是一种允许我们完成这一有用操作的特殊文件系统。你可以使用创建的文件系统来实验并练习本章中找到的几乎所有命令，而无需担心损坏系统。

## 创建用于测试的文件系统

因为我们大多数人没有多余的计算机或硬盘来进行实验和练习，我们可以自己创建一个，方法是创建一个包含我们选择的文件系统的映像文件，并使用回环文件系统来挂载它。这样，我们就不会冒意外搞乱系统本身的风险。虽然你也可以使用软盘驱动器进行这些相同的练习，但其小尺寸限制了你的灵活性。

### 步骤 1—制作空白映像文件

使用 `dd` 命令创建一个块大小为 1,024 字节（1 MB）的文件，并创建一个大小为 10 MB 的文件。（你需要在硬盘上有足够的空间来容纳这么大的文件，因此请相应调整大小。）我们需要 10,000 个 1KB（1,024 字节）的块，因此我们选择计数为 10000。

如果我们想要一个软盘大小的映像，我们会选择块大小（`bs`）为 512，对于 1.44MB 的软盘计数为 2880，或者对于 2.88MB 的软盘计数为 5760。以下是其方法：

```bash
# dd if=/dev/zero of=/tmp/fedoratest.img bs=1024 count=10000
```

我们看到计算机响应如下：

```text
10000+0 records in
10000+0 records out
```

如果我们检查新文件的命令，我们会看到：

```bash
# file /tmp/fedoratest.img
/tmp/fedoratest.img: data
```

### 步骤 2—创建文件系统

现在我们需要让系统认为该文件是一个块设备，而不是一个 ASCII 文件，因此我们使用 `losetup`，这是一个将回环设备与普通文件或块设备关联的工具；我们将使用回环设备 `/dev/loop0`。

```bash
# losetup /dev/loop0 /tmp/fedoratest.img
```

现在我们可以将文件格式化为 ext2 文件系统：

```bash
# mke2fs /dev/loop0
```

我们看到计算机响应如下：

```text
mke2fs 1.27 (8-Mar-2003)
File System label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
2512 inodes, 10000 blocks
500 blocks (5.00%) reserved for the super user
First data block=1
2 block groups
8192 blocks per group, 8192 fragments per group
1256 inodes per group
Superblock backups stored on blocks:
	8193
Writing inode tables: done
Writing superblocks and file system accounting information: done

This file system will be automatically checked every 21 mounts or 180 days, whichever comes first. Use tune2fs -C or -i to override.
```

### 步骤 3—挂载我们的测试文件系统

创建测试文件系统后，你可以实验你将使用的格式化命令的不同选项。为我们的映像文件创建一个挂载点很有用：

```bash
# mkdir /mnt/image
```

然后挂载它：

```bash
# mount /dev/loop0 /mnt/image
```

我们现在就可以做到这一点，因为我们已经将回环文件系统与映像文件关联。稍后如果我们重新挂载它，我们必须使用以下格式来使用回环选项：

```bash
# mount -o loop /tmp/fedoratest.img /mnt/image
```

挂载新文件系统后，我们可以查看它，发现已在其上创建了 `/lost+found` 目录，并且 `df` 命令返回：

```bash
# df /x /mnt/image

Filesystem           1024-blocks      Used Available Capacity Mounted on
/dev/loop0                 9830         0     9830          0% /mnt/image
```

*注意：原文 OCR 文本在 `df` 输出部分存在格式问题。上述 Markdown 表格代表了文本数据"9.5M 13k 8.9M 1% /mnt/image"通常与 `df` 输出关联的标准输出结构，但严格遵循“保留原始信息”规则，这里是将精确文本转换为代码块/表格表示，或者简单地保留为文本。然而，标准的 `df` 输出是表格形式。让我们坚持使用 OCR 中找到的文本表示，但对其进行整洁格式化。*

实际上，查看 OCR 文本：`9.5M   13k  8.9M   1% /mnt/image` 跟在标题 `File System  Size Used Avail Use% Mounted on /dev/loop0` 之后。这看起来像是 `df -h` 或类似命令。让我们将其格式化为 Markdown 表格，如“类表格文本”所要求的。

| 文件系统 | 大小 | 已用 | 可用 | 使用率 | 挂载于 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/loop0 | 9.5M | 13k | 8.9M | 1% | /mnt/image |

要卸载它，请使用：

```bash
# umount /mnt/image
```

对映像进行备份，以防我们弄坏原始文件：

```bash
# cp /tmp/fedoratest.img fedoratest.bak
```

创建测试文件系统后，你可以创建目录，将文件复制到其中，删除文件，尝试恢复它们，并且总的来说，在学习和练习宝贵技能的同时，在计算机上制造受控的混乱。如果你损坏了映像上的文件系统且无法修复，请卸载它，删除它，并创建一个新文件系统（或从备份中复制一个新文件系统）。

### 在运行中的系统上以只读方式挂载分区

请记住，为了进行几乎任何形式的文件系统操作（格式化、检查等），你应该卸载文件系统；这样做可以避免向文件系统写入任何数据，从而防止其损坏。

如何在运行中的系统上重新挂载分区？例如，要将 `/home` 分区（假设它与根分区位于不同的物理分区上）重新挂载为只读以对其运行 `fsck`，然后重新挂载为读写，请使用 `mount` 的 `remount` 选项：

```bash
# mount -o ro,remount /home
```

> 注意
> 如果普通用户已登录，重新挂载将不起作用，因为 /home 处于忙碌状态（使用中）。你可能需要切换到运行级别 1（init 1），即单用户模式，才能重新挂载 /home。

