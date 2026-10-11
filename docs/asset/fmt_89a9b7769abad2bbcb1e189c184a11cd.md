
`e2fsck` 实用程序检查文件系统的多个方面以检查一致性。如果没有发现问题，`e2fsck` 会发出类似清单 9-4 中所示的消息。请注意，`e2fsck` 应仅在未挂载的文件系统上运行。虽然可以在已挂载的文件系统上运行，但这可能会对磁盘或 Flash 设备上的内部文件系统结构造成严重损坏。

为了创建一个更有趣的示例，清单 9-5 是在 CompactFlash 设备仍然挂载的情况下将其从插槽中拔出而创建的。我们在从系统中移除该设备之前，故意在该设备上创建了一个文件并进行了编辑会话。这可能会导致描述该文件的数据结构以及包含文件数据的实际数据块损坏。

#### 清单 9-5

损坏的文件系统检查

```bash
#### e2fsck -y /dev/sdb1

   e2fsck 1.37  (21-Mar-2005)

/dev/sdb1 was not cleanly unmounted, check forced.

Pass 1: Checking inodes, blocks, and sizes

Inode 13, i_blocks is 16, should be 8.  Fix? yes

Pass 2: Checking directory structure

Pass 3: Checking directory connectivity

Pass 4: Checking reference counts

Pass 5: Checking group summary information

/dev/sdb1: ***** FILE SYSTEM WAS MODIFIED *****

/dev/sdb1: 25/2880 files (4.0% non-contiguous), 488/11504 blocks

#
```

从清单 9-5 中，你可以看到 `e2fsck` 检测到 CompactFlash 未被干净地卸载。此外，你可以看到 `e2fsck` 检查期间对文件系统的处理。`e2fsck` 实用程序对文件系统执行五次遍历，检查内部文件系统数据结构的各个元素。与文件相关的错误由 inode 13 标识，由于 `e2fsck` 命令行中包含了 `-y` 标志，该错误已自动修复。

当然，在真实系统中，你可能不会这么幸运。某些类型的文件系统错误无法使用 `e2fsck` 修复。此外，嵌入式系统设计师应理解，如果电源移除时未正确关机，启动周期可能会被扫描启动设备并修复任何错误所需的时间延迟。事实上，如果这些错误无法修复，系统启动将被中断，并指示需要手动干预。此外，值得注意的是，如果文件系统很大，文件系统检查 `fsck` 可能需要数分钟甚至数小时，特别是对于大型的多千兆字节文件系统。

防止文件系统损坏的另一种防御措施是确保写入操作在发生后立即提交到磁盘。`sync` 实用程序可用于强制将所有排队的 I/O 请求提交到各自设备。最小化因意外电源丢失或驱动器故障导致数据损坏的脆弱窗口的策略之一是在每次文件写入后或根据应用程序需求在战略上发出 `sync` 命令。这里的权衡当然是性能惩罚。延迟磁盘写入是所有现代操作系统中使用的性能优化。有效使用 `sync` 会抵消这种优化。

`ext2` 文件系统已成熟为 Linux 系统快速、高效且健壮的文件系统。然而，如果你需要日志文件系统额外的可靠性，或者在不干净关机后的启动时间是设计中的问题，你应该考虑 `ext3` 文件系统。

## 9.3 ext3

`ext3` 文件系统已成为一个强大、高性能且健壮的日志文件系统。它目前是许多流行的桌面 Linux 发行版的默认文件系统，例如 Red Hat 和 Fedora Core 系列。

`ext3` 文件系统基本上是 `ext2` 文件系统的扩展，增加了日志功能。日志是一种技术，其中对文件系统的每个更改都记录在特殊文件中，以便从已知的日志点进行恢复。`ext3` 文件系统的主要优点之一是其能够在不干净关机后直接挂载的能力。如上一节所述，

³ 文件系统中的文件由称为 `inode` 的内部 `ext2` 数据结构表示。

当系统意外关闭，例如在电源故障期间，系统将强制进行文件系统一致性检查，这可能是一个耗时的操作。对于 `ext3` 文件系统，由于日志可以直接重放以确保文件系统的一致性，因此无需进行一致性检查。

尽管不深入探讨超出本书范围的设计细节，但值得简要说明日志文件系统的工作原理。日志文件系统包含一个特殊文件（通常对用户隐藏），用于存储文件系统元数据^4 以及文件数据本身。这个特殊文件被称为日志。每当文件系统发生变更（如写操作）时，变更首先被写入日志。文件系统驱动程序确保在将实际变更提交到存储介质（例如磁盘或闪存）之前，日志写入已经提交。一旦变更被记录在日志中，驱动程序会将变更发布到介质上的实际文件和元数据。如果在介质写入期间发生电源故障并触发重启，恢复文件系统一致性所需做的仅仅是重放日志中的变更。

`ext3` 文件系统最重要的设计目标之一是与 `ext2` 文件系统保持向后和向前兼容。可以在不重新格式化或重写磁盘上所有数据的情况下，将 `ext2` 文件系统转换为 `ext3` 文件系统，再转回 `ext2`。让我们来看看这是如何实现的。^5 清单 9-6 详细说明了该过程。

#### 清单 9-6：将 ext2 文件系统转换为 ext3 文件系统

```bash
#### mount /dev/sd1 /mnt/flash    # Mount the ext2 file system
#### tune2fs -j /dev/sd1          # Create the journal

tune2fs 1.37 (21-Mar-2005)

Creating journal inode: done

This file system will be automatically checked every 23 mounts or

180 days, whichever comes first. Use tune2fs -c or -i to override.

#
```

请注意，我们首先将文件系统挂载到 `/mnt/flash` 仅用于说明目的。通常，我们会在未挂载的 `ext2` 分区上执行此命令。当文件系统已挂载时，`tune2fs` 的设计行为是创建一个名为 `.journal` 的日志文件，这是一个隐藏文件。在 Linux 中，以点号（`.`）开头的文件被视为隐藏文件；大多数 Linux 命令行文件工具会静默忽略此类文件。从清单 9-7 中，我们可以看到 `ls` 命令使用了 `-a` 标志，该标志指示 `ls` 工具列出所有文件。

#### 清单 9-7：ext3 日志文件

```bash
$ ls -al /mnt/flash

total 1063

drwxrwxrwx  15 root root    1024 Aug 25 19:25

drwxr-xr-x   5 root root    4096 Jul 18 19:49 ..

drwxr-xr-x   2 root root    1024 Aug 14 11:27 bin

drwxr-xr-x   2 root root    1024 Aug 14 11:27 boot

drwxr-xr-x   2 root root    1024 Aug 14 11:27 dev

drwxr-xr-x   2 root root    1024 Aug 14 11:27 etc

drwxr-xr-x   2 root root    1024 Aug 14 11:27 home

drwxr-xr-x   1 root root 1048576 Aug 25 19:25 .journal

drwxr-xr-x   2 root root    1024 Aug 14 11:27 lib

drwxr-xr-x   2 root root   12288 Aug 14 11:27 lost+found

drwxr-xr-x   2 root root    1024 Aug 14 11:27 proc

drwxr-xr-x   2 root root    1024 Aug 14 11:27 root

drwxr-xr-x   2 root root    1024 Aug 14 11:27 sbin

drwxr-xr-x   2 root root    1024 Aug 14 11:27 tmp

drwxr-xr-x   2 root root    1024 Aug 14 11:27 usr

drwxr-xr-x   2 root root    1024 Aug 14 11:27 var
```
