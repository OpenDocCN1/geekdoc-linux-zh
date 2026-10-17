
| `-d`<br/>`--decompress`<br/>`--uncompress` | 当与 `gzip` 命令一起使用时，解压缩指定的文件（等同于 `gunzip` 命令）。 |

| `-f`<br/>`--force` | 当与 `gzip` 命令一起使用时，压缩符号链接。当与 `gunzip` 命令一起使用时，在不提示用户的情况下覆盖任何现有文件。 |

| `-fast` | 获得较低的压缩率；等同于 `-1` 选项。 |

| `-h` | 显示 `gzip` 和 `gunzip` 命令的语法和可用选项。 |

| `-help` | |

| `-l` | 列出使用 `gzip` 压缩的文件的压缩率。 |

| `-list` | |

| `-n` | 不允许 `gzip` 和 `gunzip` 保留文件的原始修改时间和访问时间。 |

| `-no-name` | |

| `-q` | 抑制所有警告消息。 |

| `-quiet` | |

| `-r` | 指定递归压缩或解压缩指定目录内的所有文件。 |

| `-recursive` | |

| `-S *.suffix*` | 在压缩或解压缩文件时，指定除 `*.gz` 以外的文件后缀。 |

| `-suffix *.suffix*` | |

| `-t` | 当与 `gunzip` 命令一起使用时，执行测试解压缩，使用户可以在解压缩前查看任何错误消息；它不会实际解压缩文件。 |

| `-test` | |

| `-v` | 在压缩和解压缩过程中显示详细输出（压缩率和文件名）。 |

| `-verbose` | |

## `bzip2` 工具

`bzip2` 工具与之前讨论的 `compress` 和 `gzip` 工具的不同之处在于，它在压缩文件时使用了 **Burrows-Wheeler 块排序 Huffman 编码** 算法。此外，`bzip2` 工具不能用于压缩整个目录中的文件，`zcat` 和 `zmore` 命令不能用于查看使用 `bzip2` 压缩的文件，并且平均压缩率为 **50-75%**。

与 `compress` 和 `gzip` 工具类似，仅当使用 `-f` 选项时，符号链接才会被压缩，并且可以使用 `-v` 选项显示压缩率。同样，压缩期间会保留文件的所有权、修改时间和访问时间。

使用 `bzip2` 压缩的文件给定的文件扩展名是 `.bz2`。要压缩 `samplefile` 和 `samplefile2` 文件并查看它们的压缩率和文件名，您可以使用以下命令：

```
[root@server1 root]# bzip2 -v samplefile samplefile2
samplefile1: 2.63f:1, 3,034 bits/byte, 62.08% saved, 20239 in,7675 out.
samplefile2: 1.463:1, 5,394 bits/byte, 32.58% saved, 574 in,387 out.
[root@server1 root]# ls -1
total 16
drwx------ 3 root root 4096 Jul 21 08:15 Desktop
-rw-rw-r-- 1 root root 387 Jul 21 08:18 samplefile2.bz2
-rw-r-r-- 1 root root 7675 Jul 21 08:15 samplefile.bz2
[root@server1 root]# _
```

由于压缩算法不同于 `compress` 和 `gzip` 工具使用的算法，您必须使用 `bcat` 命令 将压缩文件的内容显示到标准输出，如下例所示：

```
[root@server1 root]# bcat samplefile2.bz2
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining room this year while vacationing in Algonquin Park - I especially wished to see the model of the Highland Inn and the train station in the dining room.

I have been reading on the history of Algonquin Park but no where could I find a description of where the Highland Inn was originally located on Cache lake.

If it is no trouble, could you kindly let me know such that I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth

[root@server1 root]# _
```

> **注意**
>
> 还存在 `bzmore` 命令 和 `bless` 命令，可用于逐页查看 `bzip2` 压缩文件的内容。

# 压缩、备份和软件安装

要解压缩文件，您可以使用 `bunzip2` 命令后跟要解压缩的文件名；与 `compress` 和 `gzip` 不同，解压缩文件时必须包含文件扩展名。要解压缩本文件中之前创建的 `samplefile` 和 `samplefile2` 文件，您可以使用以下命令：

```
[root@server1 root]# bunzip2 -v samplefile.bz2 samplefile2.bz2
samplefile.bz2: done
samplefile2.bz2: done
[root@server1 root]#
```

如果任何文件将被覆盖，`bunzip2` 命令会提示用户确认，除非指定了 `-f` 选项。表 12-3 列出了 `bzip2` 工具的其他常用选项。

##### 表 12-3 bzip2 工具常用选项

| 选项 | 描述 |
|---|---|
| `-#` | 指定压缩期间使用的块大小；`-1` 表示 100K 的块大小，而 `-9` 表示 900K 的块大小。 |
| `-c`<br/>`--stdout` | 当与 `bunzip2` 命令一起使用时，将压缩文件的内容显示到标准输出。 |
| `-d`<br/>`--decompress` | 当与 `bzip2` 命令一起使用时，解压缩指定的文件（等同于 `bunzip2` 命令）。 |
| `-f`<br/>`--force` | 当与 `bzip2` 命令一起使用时，压缩符号链接。当与 `bunzip2` 命令一起使用时，在不提示用户的情况下覆盖任何现有文件。 |
| `-k`<br/>`--keep` | 在压缩期间保留原始文件；创建一个带有 `.bz2` 扩展名的新文件。 |
| `-q`<br/>`--quiet` | 抑制所有警告消息。 |
| `-s`<br/>`--small` | 最小化压缩期间的内存使用量。 |
| `-t`<br/>`--test` | 当与 `bunzip2` 命令一起使用时，执行测试解压缩，使用户可以在解压缩前查看任何错误消息；它不会实际解压缩文件。 |
| `-v`<br/>`--verbose` | 在压缩和解压缩过程中显示详细输出（压缩率）。 |

### 系统备份

### 系统备份

可以将文件和目录定期复制到备用位置。这些备份副本随后可以分发到其他计算机，或在发生导致信息丢失的系统故障时用于恢复文件。这一整个过程被称为**系统备份**，文件和目录的备份副本称为**存档**。

可以在许多不同类型的介质上创建存档，例如磁带、Zip 磁盘、软盘、CD-RW/DVD-RW 光盘或硬盘。在 Linux 系统上备份数据最常用的介质是**磁带**；然而，CD-RW/DVD-RW 备份正迅速变得比磁带备份更受欢迎。将数据备份到 CD-RW/DVD-RW 需要特殊的刻录软件；因此，将在本节的稍后部分对其进行讲解。

表 12-4 列出了一些用于不同磁带设备的常见设备文件。

#### 表 12-4 常见的磁带设备文件

| 设备文件 | 描述 |
| :--- | :--- |
| `/dev/st0` | 第一个 SCSI 磁带设备（卷回） |
| `/dev/st1` | 第二个 SCSI 磁带设备（卷回） |
| `/dev/st2` | 第三个 SCSI 磁带设备（卷回） |
| `/dev/ntst0` | 第一个 SCSI 磁带设备（非卷回） |
| `/dev/ht0` | 第一个 ATAPI IDE 磁带设备（卷回） |
| `/dev/nht0` | 第一个 ATAPI IDE 磁带设备（非卷回） |
| `/dev/ftape` | 第一个软盘磁带设备 |

> **注意**
>
