

对于主要以大文件为主的服务器，建议将大小设置为 1024 到 1024 的倍数（通常小于 4096）。让我们看看如何更改块大小。

## 更改 ext2 文件系统的块大小

要了解特定 ext2 分区上有哪些类型的文件（就大小而言），请执行以下操作：

- 1. 切换至 root 用户并进入 ext2 分区根目录。
- 2. 运行以下命令，该命令实际上是一个使用 find 和 awk 实用工具的小型脚本。此命令行脚本将显示所有文件及其大小，最后提供整个分区的总大小和平均大小。

```bash
find . -type f -exec ls -l {} \; | \
awk 'BEGIN {tsize=0;fcnt=1;} \
| printf("%03d File: % 60.5s size: %d bytes\n",fcnt++, $9, $5); \
tsize += $5; } \
END { printf("Total size = %d\nAverage file size = %.02f\n", tsize, tsize/fcnt); }'
```

- 3. 知道文件系统的平均文件大小后，您可以确定是否应更改块大小。假设您发现平均文件大小为 8192，即 2 × 4096。您可以将块大小更改为 4096。
- 4. 不幸的是，如果不重建现有 ext2 文件系统，无法更改其块大小。因此，您必须备份文件系统上的所有文件，然后使用 /sbin/mke2fs /dev/partition -b 4096 命令重建它。例如，如果您已备份 /dev/hda7 分区并希望将块大小更改为 4096，请使用 /sbin/mke2fs /dev/hda7 -b 4096 命令。

> **注意**
> 将块大小更改为高于默认值（1024）的数字可能会因寻道次数减少而显著提高原始读取速度，同时还可能加快启动期间的 fsck 会话，减少文件碎片等。然而，盲目增加块大小（即不知道平均文件大小）会导致空间浪费。如果平均文件大小为 2010 字节，而系统使用 4096 字节的块，那么每个文件平均将浪费 2086 字节（4096 − 2010）！因此在调整块大小之前，请务必了解您的文件大小。

## 安装 e2fsprogs 以调优 ext2 文件系统

为了调优 ext2 文件系统，您需要按照以下步骤安装 e2fsprogs 实用工具包：

- 1. 从 www.rpmfind.net 下载 e2fsprogs-version_src.rpm（将 version 替换为最新版本号）源发行版。我下载了 e2fsprogs-1.19-0.src.rpm 包。您也可以从 e2fsprogs 项目网站 http://e2fsprogs.sourceforge.net 获取源码。切换至 root 用户。
- 2. 运行 `rpm -ivh e2fsprogs-version.src.rpm` 命令，将源提取到 `/usr/src/redhat/SOURCES/` 目录。源 RPM 会放下一个 `e2fsprogs-version.tar.gz` 文件，需要使用 `tar xzvf e2fsprogs-version.tar.gz` 命令进行解压。这将创建一个名为 `e2fsprogs-version` 的子目录。
- 3. 进入新的子目录 `e2fsprogs-version`。
- 4. 运行 `mkdir build` 创建一个新子目录，然后切换到该子目录。
- 5. 运行 `.../configure` 脚本以配置源树。然后运行 `make` 实用程序生成二进制文件。接着运行 `make check` 以确保所有构建都正确。最后，运行 `make install` 命令安装二进制文件。

安装 e2fsprogs 实用工具后，您可以开始使用它们，具体方法见下一节。

## 使用 tune2fs 实用程序进行文件系统调优

您可以使用 `tune2fs` 实用程序来调优 ext2 文件系统的各个方面。但是，切勿在已挂载的 ext2 文件系统上应用 tune2fs 实用程序，并且在修改任何属于文件系统的内容时，务必备份您的数据。在本节中，我将讨论如何使用 `tune2fs` 实用程序（它是 e2fsprogs 包的一部分）来调优未挂载的名为 `/dev/hda7` 的 ext2 文件系统。如果您使用下面讨论的一个或多个设置，请记得将分区名称（`/dev/hda7`）更改为合适的名称。首先，运行以下命令以确定 `tune2fs` 显示未挂载的 `/dev/hda7` 的当前设置：

```
/sbin/tune2fs -l /dev/hda7
```

输出应类似于以下内容：

```
tune2fs 1.19, 13-Jul-2000 for EXT2 FS 0.5b, 95/08/09
Filesystem volume name:   <none>
Last mounted on:              <not available>
Filesystem UUID:     5d06c65b-dd11-4df4-9230-a10f2da783f8
Filesystem magic number:      0xEF53
Filesystem revision #:    1 (dynamic)
Filesystem features:    filetype sparse_super
Filesystem state:    clean
Errors behavior:    Continue
Filesystem OS type:    Linux
Inode count:    1684480
Block count:    13470471
Reserved block count:  673523
Free blocks:    13225778
Free inodes:    1674469
First block:    1
Block size:    1024
Fragment size:    1024
```

以下列表中讨论的设置在上述输出中以粗体显示。

- **错误处理**（**Errors behavior**）设置决定了内核在文件系统检测到错误时的行为。此设置有三个可能的值：continue（继续）、remount-ro（只读重新挂载）和 panic（内核恐慌）。默认设置是在即使有错误的情况下继续。
- **挂载计数**（**Mount count**）设置是您挂载此文件系统的次数。
- **最大挂载计数**（**Maximum mount count**）设置意味着，在达到最大读写模式挂载次数（在本例中为 20 次）之后，文件系统将在下一个启动周期中接受 fsck 检查会话。
- **上次检查**（**Last checked**）设置显示了上次执行 fsck 检查的日期。
- **检查间隔**（**Check interval**）设置显示了两个连续 fsck 会话之间的时间差。仅当间隔期间未达到最大读写挂载次数时，才使用检查间隔。换句话说，如果您在 6 个月内没有卸载文件系统，即使挂载计数仅为 2，由于文件系统超过了检查间隔，fsck 检查也将被强制触发。
- 下次 fsck 检查日期显示在 **下次检查**（**Next check after**）设置中。
- **保留块 uid**（**Reserved blocks uid**）和 **保留块 gid**（**Reserved blocks gid**）设置显示了哪个用户和组拥有此文件系统的保留部分。默认情况下，保留部分由超级用户（UID = 0, GID = 0）使用。

对于未挂载的文件系统（如 /dev/hda7），您可以使用 tune2fs 的 -c 选项将最大读写挂载计数设置更改为更适合您需求的值。例如，/sbin/tune2fs -c 1 /dev/hda7 将强制每次启动系统时都对文件系统执行 fsck 检查。您还可以使用 -i 选项更改基于时间的 fsck 检查强制策略。

例如，`/sbin/tune2fs -i 7d /dev/hda7` 命令确保如果文件系统在一周后以读写模式重新挂载，则强制执行 `fsck` 检查。类似地，`/sbin/tune2fs -i 10 /dev/hda7` 命令禁用基于时间的 `fsck` 检查。

## 使用 e2fsck 实用程序检查和修复文件系统

如果您有损坏的 `ext2` 文件系统，可以使用 `e2fsck` 实用程序尝试修复它。要使用 `e2fsck` 检查分区，必须首先卸载它，然后运行 `/sbin/e2fsck /dev/device` 命令，其中 `/dev/device` 是您的磁盘驱动器。例如，要在名为 `/dev/hda7` 的设备上强制 `fsck` 检查，请使用 `/sbin/e2fsck -f /dev/hda7` 命令。这样的检查可能会显示如下所示的输出：

```
e2fsck 1.19, 13-Jul-2000 for EXT2 FS 0.5b, 95/08/09
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/hda7: 12/1684256 files (0.0% non-contiguous), 52897/3367617 blocks
```

`e2fsck` 实用程序会询问您修复问题，您可以通过使用 `-p` 选项来避免这些问题。

## 通过日志文件系统提高 Linux 的可靠性

Linux 文件系统领域新的热门话题是日志文件系统（journaling file system）。*日志文件系统*  simply 是一个基于事务的文件系统。每个更改文件系统的文件系统活动都会记录在事务日志中。在发生崩溃的情况下，文件系统可以重放必要的事务，在非常短的时间内恢复到稳定状态。这是一种许多广泛使用的数据库引擎（如 IBM DB2 和 Oracle）使用的技术，以确保文件系统始终处于已知且可恢复的状态。

`ext2` 文件系统的问题在于，不幸发生崩溃时，文件系统可能处于如此不干净的状态，以至于可能损坏到无法有意义地恢复。用于检查和潜在修复文件系统的 `fsck` 程序往往无法解决此类问题。对于日志文件系统而言，这样的噩梦已成为过去！因为事务日志记录了文件系统中的所有活动，崩溃恢复迅速且数据损失最小。

> 日志文件系统不会在日志中记录数据；它仅记录与磁盘操作相关的元数据，因此重放日志仅使文件系统在结构关系和资源分配方面保持一致。因此，可能会有少量数据丢失。此外，记录也和其他活动一样受媒体错误的影响。因此，如果媒体损坏，日志记录也无济于事。

