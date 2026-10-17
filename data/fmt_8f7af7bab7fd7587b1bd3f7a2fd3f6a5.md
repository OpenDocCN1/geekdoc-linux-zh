
因此，您可能会发现（特别是在全新硬件上安装时），您需要先使用 `fdisk` 以达到 `cfdisk` 可以处理的状态。尝试运行 `cfdisk`；如果它抱怨，则运行 `fdisk`。（如果您正在构建全 Linux 系统且 `cfdisk` 抱怨，一个好的处理方式是使用 `fdisk` 删除所有现有分区，然后启动 `cfdisk` 编辑空表。）

以下注释适用于 `fdisk` 和 `cfdisk` 两者。两者都接受一个参数，即您希望创建 Linux 分区的驱动器名称。硬盘设备名称如下：

- `/dev/hda`：第一 IDE 驱动器
- `/dev/hdb`：第二 IDE 驱动器
- `/dev/sda`：第一 SCSI 驱动器
- `/dev/sdb`：第二 SCSI 驱动器

例如，要在系统的第一 SCSI 驱动器上创建 Linux 分区，您将使用（或者安装程序可能从菜单选项生成）以下命令：

```bash
cfdisk /dev/sda
```

如果您不带参数使用 `fdisk` 或 `cfdisk`，它将假设 `/dev/hda`。

要在系统的第二驱动器上创建 Linux 分区，只需在运行 `fdisk` 时指定 `/dev/hdb`（对于 IDE 驱动器）或 `/dev/sdb`（对于 SCSI 驱动器）。

您的 Linux 分区不必都在同一个驱动器上。例如，您可能希望在 `/dev/hda` 上创建根文件系统分区，在 `/dev/hdb` 上创建交换分区。为了做到这一点，只需对每个驱动器运行一次 `fdisk` 或 `cfdisk`。

## 安装 Linux

在 Linux 中，分区根据其所属的驱动器命名。例如，驱动器 `/dev/hda` 上的第一个分区是 `/dev/hda1`，第二个是 `/dev/hda2`，依此类推。如果您有任何逻辑分区，它们的编号从 `/dev/hda5`、`/dev/hda6` 等开始。

![](img/a3584dae761d2e3abed8bf40d7637389_126_0.png)

> **警告**
>
> 使用 Linux `fdisk` 或 `cfdisk` 时，您不应该为除 Linux 以外的操作系统创建或删除分区。也就是说，不要使用此版本的 `fdisk` 创建或删除 MS-DOS 分区；请改用 MS-DOS 版本的 FDISK。如果您尝试使用 Linux `fdisk` 创建 MS-DOS 分区，MS-DOS 很可能无法识别该分区，无法正确启动。

下面是使用 `fdisk` 的一个例子。假设您有一个 MS-DOS 分区，在驱动器上使用了 61693 个块，其余部分留给 Linux。（在 Linux 中，一个块是 1024 字节。因此，61693 个块大约是 61 兆字节。）在这个教程示例中，您只需创建两个分区：交换和根分区。您可能应该根据上述建议将此扩展到四个 Linux 分区：一个用于交换，一个用于根文件系统，一个用于系统软件，以及一个主目录区域。

首先，使用 `p` 命令显示当前分区表。如您所见，`/dev/hda1`（`/dev/hda` 上的第一个分区）是一个 61693 个块的 DOS 分区。

```
Command (m for help): p
Disk /dev/hda: 16 heads, 38 sectors, 683 cylinders
Units = cylinders of 608 * 512 bytes

Device    Boot Begin Start End   Blocks Id System
/dev/hda1 *   1      203   61693 6 DOS 16-bit >32M

Command (m for help): 
```

接下来，使用 `n` 命令创建新分区。Linux 根分区大小为 80 兆字节。

```
Command (m for help): n
Command action
e extended
p primary partition (1-4)
p
```

这里系统询问您是否想要创建扩展分区还是主分区。在大多数情况下，您想要使用主分区，除非您需要在一个驱动器上拥有超过四个分区。有关更多信息，请参阅“重新分区您的 DOS/Windows 驱动器”部分。

第一个柱面应该是最后一个分区结束后的*下一个*柱面。在以下情况下，`/dev/hda1` 结束于柱面 203，因此我们在柱面 204 开始新分区。

```
Partition number (1-4): 2
First cylinder (204-683): 204
Last cylinder or +size or +sizeM or +sizeK (204-683): +80M
```

如您所见，如果使用符号 `+80M`，它指定一个 `80` 兆字节的分区。同样，符号 `+80K` 将指定一个 `80` 千字节分区，而 `+80` 将指定一个 `80` 字节分区。

如果您看到此警告，可以忽略它：

```
Warning: Linux cannot currently use 33090 sectors of this partition
```

这是旧限制遗留下来的，当时 Linux 文件系统只能有 `64` 兆字节的大小。然而，随着较新的文件系统类型，情况不再如此——分区现在可以高达 `4` 兆字节。

接下来，创建您的 `10` 兆字节交换分区，`/dev/hda3`。

```
Command (m for help): n
Command action
e extended
p primary partition (1-4)
p
```

```
Partition number (1-4): 3
First cylinder (474-683): 474
Last cylinder or +size or +sizeM or +sizeK (474-683): +10M
```

再次，显示分区表的内容。请务必记下这里的信息，特别是每个分区的块大小。您稍后需要这些信息。

```
Command (m for help): p
Disk /dev/hda: 16 heads, 38 sectors, 683 cylinders
Units = cylinders of 608 * 512 bytes
```

```
Device Boot Begin Start End Blocks Id System
/dev/hda1 * 1 1 203 61693 6 DOS 16-bit >=32M
/dev/hda2 204 473 82080 83 Linux native
/dev/hda3 474 474 507 10336 83 Linux native
```

注意 Linux 交换分区（这里，`/dev/hda3`）的类型是*Linux native*。我们需要将交换分区的类型更改为

设置为 Linux 交换分区，以便安装程序将其识别为交换分区。为此，请使用 `fdisk` 的 `t` 命令：

```
Command (m for help): t
Partition number (1-4): 3
Hex code (type L to list codes): 82
```

如果您使用 `L` 列出类型代码，会发现 `82` 是 Linux 交换分区的对应类型。

要退出 `fdisk` 并将更改保存到分区表中，请使用 `w` 命令。要退出 `fdisk` 而不保存更改，请使用 `q` 命令。

退出 `fdisk` 后，系统可能会提示您重启以确保更改生效。通常，在使用 `fdisk` 后没有必要重启——现代版本的 `fdisk` 和 `cfdisk` 足够智能，无需重启即可更新分区。

## 分区后的步骤

编辑分区表后，安装程序会询问是否查看这些表并为您启用交换分区。（安装程序不会自动执行此操作，以防您正在运行双启动系统，而您的某个非 Linux 分区可能恰好看起来像交换卷。）请让安装程序继续执行此操作。

接下来，程序将要求您将 Linux 文件系统名称（例如 `/`、`/usr`、`/var`、`/tmp`、`/home`、`/home2` 等）与您将要使用的每个非交换分区关联起来。

这只有一个硬性规定：必须有一个名为 `/` 的根文件系统，并且它必须是可引导的。您可以随意命名其他 Linux 分区。但关于如何命名它们有一些约定，这可能会简化您后来的生活。

前面我建议了一个基本的三分区配置，包括一个较小的根分区、一个中等大小的系统软件分区和一个较大的主目录分区。传统上，这些被称为 `/`、`/usr` 和 `/home`。反直觉的 `/usr` 名称是从早期 Unix 系统演变而来的遗留问题，当时（规模小得多的）Unix 系统将系统软件和用户主目录放在同一个非根分区上。有些软件依赖于它。

如果您有多个主目录区域，通常惯例是将它们命名为 `/home`、`/home2`、`/home3` 等。如果您有两个物理磁盘，可能会出现这种情况。例如，在我的个人系统中，当前的布局如下所示：

| 文件系统 | 1024-块 | 已用 | 可用 | 容量 | 挂载点 |
|---|---|---|---|---|---|
| /dev/sda1 | 30719 | 22337 | 6796 | 77% | / |
