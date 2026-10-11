
| 1 | 1049kB | 99.6MB | 98.6MB | ext4 | primary | |

| 2 | 99.6MB | 200MB | 100MB | ext4 | primary | |

| 3 | 200MB | 300MB | 99.6MB | ext4 | primary | |

你不小心使用 `rm 2` 删除了分区 2。要恢复它，你可以使用 `rescue` 命令，其语法为 `rescue START END`，其中 `START` 是分区起始的大致位置，而 `END` 是分区结束的大致位置。

`parted` 将扫描磁盘以查找分区，并询问是否恢复找到的任何分区。在上面的例子中，分区 2 从 99.6 MB 开始，到 200 MB 结束。因此，你可以使用以下命令来恢复该分区：

```
(parted) rescue 90m 210m
Information: A ext4 primary partition was found at 99.6MB -> 200MB.
Do you want to add it to the partition table?

Yes/No/Cancel? y
```

这将恢复分区及其内容。请注意，`rescue` 只能恢复安装了文件系统的分区。空分区无法被检测到。

## 调整 ext2/3/4 分区大小

可以使用 `parted` 调整分区大小，使其变大或变小。然而，有一些注意事项：

- 在调整分区大小时，分区必须未被使用且未挂载。
- 你需要在分区 *之后* 有足够的空闲空间才能将其扩展到你想要的大小。

命令为 `resizepart`，后跟分区编号及其应结束的位置。例如，如果你有如下分区表：

| 编号 | 起始 | 结束 | 大小 | 文件系统 | 名称 | 标志 |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| 1 | 1049kB | 99.6MB | 98.6MB | ext4 | primary | |

| 2 | 99.6MB | 200MB | 100MB | ext4 | | |

尝试使用 `resizepart` 扩展分区 1 会触发错误消息，因为在新的大小下，分区 1 将与分区 2 重叠。然而，分区 3 可以调整大小，因为其后方有空闲空间，这可以通过 `print free` 命令进行验证：

```
(parted) print free
Model: Kingston DataTraveler 2.0 (scsi)
Disk /dev/sdb: 1999MB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags:

Number  Start   End     Size    File system  Name     Flags
        17.4kB  1049kB  1031kB  Free Space
  1     1049kB  99.6MB  98.6MB  ext4         primary
  2     99.6MB  200MB   100MB   ext4
  3     200MB   300MB   99.6MB  ext4         primary
        300MB   1999MB  1699MB  Free Space
```

因此，你可以使用以下命令将分区 3 调整为 350 MB：

```
(parted) resizepart 3 350m

(parted) print
Model: Kingston DataTraveler 2.0 (scsi)
Disk /dev/sdb: 1999MB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags:

Number  Start   End     Size    File system  Name     Flags
  1     1049kB  99.6MB  98.6MB  ext4         primary
  2     99.6MB  200MB   100MB   ext4
  3     200MB   350MB   150MB   ext4         primary
```

请记住，新的结束点是从磁盘起始处开始计算的。因此，由于分区 3 原本在 300 MB 处结束，现在它需要在 350 MB 处结束。

但调整分区大小只是任务的一部分。你还需要调整其中驻留的文件系统的大小。对于 ext2/3/4 文件系统，这使用 `resize2fs` 命令完成。在上面的例子中，当挂载时，分区 3 仍显示“旧”的大小：

```
$ df -h /dev/sdb3
Filesystem  Size  Used Avail Use% Mounted on
/dev/sdb3     88M  1.6M   80M   2% /media/carol/part3
```

要调整大小，可以使用 `resize2fs DEVICE SIZE` 命令，其中 `DEVICE` 对应你想要调整大小的分区，而 `SIZE` 是新的尺寸。如果你省略 size 参数，它将使用分区的所有可用空间。在调整大小之前，建议先卸载该分区。

在上面的例子中：

```
$ sudo resize2fs /dev/sdb3
resize2fs 1.44.6 (5-Mar-2019)
Resizing the filesystem on /dev/sdb3 to 146212 (1k) blocks.
The filesystem on /dev/sdb3 is now 146212 (1k) blocks long.

$ df -h /dev/sdb3
Filesystem  Size  Used  Avail Use% Mounted on
/dev/sdb3     135M  1.6M  123M   2% /media/carol/part3
```

要缩小分区，过程需要按相反顺序进行。首先，你将文件系统调整到新的、更小的尺寸，然后使用 `parted` 调整分区本身的大小。

> **警告** 缩小分区时要特别注意。如果你搞错了顺序顺序，你会丢失数据！

在我们的例子中：

```
# resize2fs /dev/sdb3 88m
resize2fs 1.44.6 (5-Mar-2019)
Resizing the filesystem on /dev/sdb3 to 90112 (1k) blocks.
The filesystem on /dev/sdb3 is now 90112 (1k) blocks long.

# parted /dev/sdb3
(parted) resizepart 3 300m
Warning: Shrinking a partition can cause data loss, are you sure
you want to continue?

Yes/No? y
```

```
(parted) print
Model: Kingston DataTraveler 2.0 (scsi)
Disk /dev/sdb: 1999MB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags:

Number  Start   End     Size    File system  Name     Flags
 1      1049kB  99.6MB  98.6MB  ext4                 primary
 2      99.6MB  200MB   100MB   ext4
 3      200MB   300MB   99.7MB  ext4                 primary
```

提示：除了指定新的大小，你还可以使用 `resize2fs` 的 `-M` 参数来调整文件系统的大小，使其刚好足够容纳其上的文件。

### 创建交换分区

在 Linux 中，系统可以根据需要将内存页面从 RAM 交换到磁盘，将其存储在通常作为磁盘上单独分区实现的独立空间中，称为 *交换分区* 或简称 *swap*。此分区需要是特定类型，并在使用前通过适当的实用工具（`mkswap`）进行设置。

使用 `fdisk` 或 `gdisk` 创建交换分区时，只需按照之前描述的创建常规分区的方法进行即可。唯一的区别是你需要将分区类型更改为 *Linux swap*。

- 在 `fdisk` 中，使用 `t` 命令。选择你要使用的分区，并将其类型更改为 `82`。使用 `w` 将更改写入磁盘并退出。
- 在 `gdisk` 中，更改分区类型的命令也是 `t`，但代码是 `8200`。使用 `w` 将更改写入磁盘并退出。
