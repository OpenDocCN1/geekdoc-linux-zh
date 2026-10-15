
图 11-6 阐明了块、`inode`（带有许多元数据属性）、目录及其关系。

### 图 11-6. 块、`inode`、目录、文件及其关系。

![](img/08b574e80eed8279bfda286dbd25d40d_310_1.png)

![](img/08b574e80eed8279bfda286dbd25d40d_311_0.png)

### 扩展文件系统 Ext2 中的块分配

在对文件进行顺序写入时，Ext2 文件系统会以 8 个连续块为单位预分配空间。当文件关闭时，未使用的预分配块会被释放，因此不会浪费空间。这种方法可以防止或减少碎片化。碎片化是指由于连续的块不可用，导致文件中的许多块分散在整个磁盘上的状态。连续块可以提高性能，因为在顺序读取文件时，磁盘磁头的移动最小化。

文件碎片化——即文件分散到非连续的块中——是所有文件系统都会遇到的问题。文件的创建和删除会导致碎片化。通过让文件系统使用高级算法来减少碎片化，可以解决这个问题。使用 `defrag` 文件系统实用程序，将碎片化的文件移动到具有连续块的位置，也可以解决此问题。Ext2 上可用的碎片整理工具称为 `defrag.ext2`。

### 创建 Ext2 文件系统

创建 Ext2 和 `Ext3` 文件系统的程序称为 `mkfs.ext2`。可以使用另外两个命令来创建 Ext2/Ext3 文件系统：`mkfs.ext2` 和 `mkfs.ext2`。本节其余部分将介绍 `mkfs` 命令的一些关键选项：

- `-b block-size` 选项指定块大小（以字节为单位）。有效的块大小值为每块 1024、2048 和 4096 字节。
- `-n number-of-inodes` 选项指定 `inode` 的数量。
- `-t fs-type` 选项指定文件系统的用途。有效选项如下：
  - `news` 每 4KB 块创建一个 `inode`。
  - `largefile` 每兆字节创建一个 `inode`。
  - `largefile4` 每 4 兆字节创建一个 `inode`。

有关 `mkfs.ext2` 选项的完整列表，请参阅 `mkfs.ext2` 手册页。

以下示例在设备 `/dev/hdb2` 上发出 `mkfs` 时使用默认设置。块大小默认为 4096，创建的 `inode` 数量为 502944。

```
### mkfs.ext2 /dev/hdb2

mke2fs 1.32 (09-Nov-2002)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
502944 inodes, 1004062 blocks
...
```

接下来，使用 `-b 1024` 选项将块大小设置为 1024，并使用 `-T news` 选项设置文件系统类型。创建的 `inode` 数量为 1005568。

```
### mkfs.ext2 -b 1024 -T news /dev/hdb2

mke2fs 1.32 (09-Nov-2002)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
1005568 inodes, 4016250 blocks
...
```

### Ext2 文件系统的 Ext3 扩展

Ext3 文件系统在不影响 Ext2 的健壮性（至少是其简单性和可靠性）的情况下提供了更高的可用性。Ext3 是 Ext2 的最小扩展，旨在添加日志记录支持。Ext3 使用与 Ext2 相同的磁盘布局和数据结构，并且与 Ext2 具有前向和后向兼容性。从 Ext2 迁移到 Ext3（反之亦然）非常简单，甚至可以在同一分区中原位完成。其他三种日志文件系统需要使用它们的 `mkfs` 实用程序格式化分区。

如果您想采用日志文件系统，但系统上没有空闲分区，那么 Ext3 可能是一个合适的日志文件系统选择。

#### 对 Ext3 的 Kernel 配置支持

您可以从配置菜单的文件系统部分中选择 `ext3` 选项，并启用以下选项：

> Ext3 日志文件系统支持 (`CONFIG_EXT3_FS=y,m,n`)

如果您希望将 Ext3 构建到内核中，请在 `ext3` 条目旁点击 `y`。如果您希望将 Ext3 构建为模块，请在 `ext3` 条目旁点击 `m`。如果需要 Ext3 支持，则使用 `n` 选项。

在 Ext3 配置中，Ext3 选择中还有其他选项可用。如果您需要这些选项中的任何一个，请在此处选择。

#### 使用 Ext3

调整 Ext3 文件系统有三种方法：

1. 在文件系统创建时进行，这是最有效的方式
2. 通过 `tune2fs` 调整实用程序，可用于在文件系统创建后对其进行调整
3. 通过文件系统挂载时可用的选项

上述三种调整选项将在以下章节中讨论。

#### 创建 Ext3 分区

创建 Ext3 文件系统的程序称为 `mke2fs`。您也可以使用 `mkfs.ext3` 和 `mkfs.ext2` 命令来创建 Ext3 文件系统。本节其余部分将介绍 `mkfs` 命令的一些关键选项：

- `-b block-size` 选项指定块大小（以字节为单位）。有效的块大小值为每块 1024、2048 和 4096 字节。
- `-n number-of-inodes` 选项指定 `inode` 的数量。
- `-t fs-type` 选项指定文件系统的用途。有效选项如下：
  - `news` 每 4KB 块创建一个 `inode`。
  - `largefile` 每兆字节创建一个 `inode`。
  - `largefile4` 每 4 兆字节创建一个 `inode`。

有关 `mkfs.ext3` 选项的完整列表，请参阅 `mkfs.ext3` 手册页。

以下示例在设备 `/dev/sdb1` 上发出 `mkfs` 时使用默认设置。块大小为 1024，创建的 `inode` 数量为 128016。

```
##### mkfs.ext3 /dev/sdb1

mke2fs 1.28 (31-Aug-2002)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
128016 inodes, 511984 blocks
...
```

Ext3 文件系统格式化完成后，建议取消文件系统的自动检查（文件系统每 3 次挂载或 180 天自动检查一次，以先到者为准）。要取消自动检查，请使用带有 `-c` 选项的 `tune2fs` 命令将检查次数设置为 0。

```
##### tune2fs -c 0 /dev/sdb1

tune2fs 1.28 (31-Aug-2002)
Setting maximal mount count to -1
```

#### 将 Ext2 文件系统转换为 Ext3

本节介绍如何将 Ext2 文件系统转换为 Ext3：

1. 备份文件系统。
2. 通过运行带有 `-j` 选项的 `tune2fs` 程序，为想要转换的现有 Ext2 文件系统添加日志文件。您可以在挂载或未挂载的 Ext2 文件系统中运行 `tune2fs`。例如，如果 `/dev/hdb3` 是一个 Ext2 文件系统，以下命令将创建日志：

```
# tune2fs -j /dev/hdb3
```

如果文件系统已挂载，则名为 `.journal` 的日志文件将放置在文件系统的根目录中。如果文件系统未挂载，则日志文件将被隐藏。（当挂载 Ext3 文件系统时，`.journal` 文件会出现。`.journal` 文件可以表明该文件系统确实是 Ext3 类型。）
3. 将 `/etc/fstab` 文件中 `/dev/hdb3` 的条目从 `ext2` 更改为 `ext3`。
4. 重新启动，并通过输入 `mount` 并查看输出来验证 `/dev/hdb3` 分区的类型是否为 Ext3。输出应包含类似以下内容的条目：

```
# mount

/dev/hdb3 on /test type ext3 (rw)
```

#### 在 Ext3 文件系统上使用独立的日志设备

要在 Ext3 文件系统上使用外部日志，您需要做的第一件事是在日志设备上发出 `mkfs` 命令。外部日志的块大小必须与 Ext3 文件系统的块大小相同。在以下示例中，`/dev/hda1` 设备用作 Ext3 文件系统的外部日志：

```
##### mkfs.ext3 -b 4096 -O journal_dev /dev/hda1
##### mkfs.ext3 -b 4096 -J device=/dev/hda1 /dev/hdb1
```

#### Ext2/Ext3 实用程序

`e2fsprogs` 包包含用于 Ext2 和 Ext3 文件系统的各种实用程序。以下是每个实用程序的简要说明：

- `badblocks`: 搜索设备上的坏块。
- `chattr`: 更改 Ext2 或 Ext3 文件系统上的文件属性。
