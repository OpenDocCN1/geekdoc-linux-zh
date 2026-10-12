
| `-f FILENAME` | 指定存档的路径；`FILENAME` 可以是文件系统上的文件或设备设备文件。 |
| `-u` | 指定在备份成功后更新 `/etc/dumpfiles` 文件。 |
| `-n` | 当发生任何错误或备份完成时通知用户。 |
| `-r` | 与 `restore` 命令配合使用时，提取整个存档。 |
| `-x FILENAME` | 与 `restore` 命令配合使用时，提取由 `FILENAME` 代表的特定文件或文件。 |
| `-i` | 与 `restore` 命令配合使用时，交互方式恢复文件，对所有操作向用户提示确认。 |

## 系统备份

| 选项 | 描述 |
| :--- | :--- |
| `-t` | 与 `restore` 命令配合使用时，列出现有存档的文件内容（目录）。 |
| `-v` | 在操作存档时显示详细输出（文件和目录信息）。 |

例如，以下 `dump` 命令的输出：

```
root@server1 root]# df
Filesystem     1K-blocks Used Available% Mounted on
/dev/hda3      4032124 2840560 986736 75% /
/dev/hda2      101107 10550 85336 12% /boot
none           192232 0 192232 0% /dev/shm
root@server1 root]# dump -ouf /dev/st0 /dev/hda2
DUMP: Date of this level 0 dump: Sat Jul 23 16:43:09 2005
DUMP: Dumping /dev/hda2 (/boot) to /dev/st0
DUMP: Exclude ext3 journal inode 8
nDUMP: Label: /boot
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 6485 tape blocks.
DUMP: Volume 1 started with block 1 at: Sat Jul 23 16:43:10 2005
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: Closing /dev/st0
DUMP: Volume 1 completed at: Sat Jul 23 16:43:11 2005
DUMP: Volume 1 6470 tape blocks (6.32MB)
DUMP: Volume 1 took 00:00:01
DUMP: Volume 1 transfer rate: 6470 kBytes/s
DUMP: 6470 tape blocks (6.32MB) on 1 volume(s)
DUMP: finished in 1 seconds, throughput 6470 KBytes/sec
DUMP: Date of this level 0 dump: Sat Jul 23 16:43:09 2005
DUMP: Date of this dump completed: Sat Jul 23 16:43:11 2005
DUMP: Average transfer rate: 6470 kB/s
DUMP: IS DONE
root@server1 root]#
```

要将 `/boot` 分区 (`/dev/hda2`) 全备份到第一个可回绕的 SCSI 设备，并更新创建的 `/etc/dumpdates` 文件，可以使用以下命令：

> 另外，在使用 `dump` 命令时，您也可以指定文件系统挂载点，命令 `dump -ouf /dev/st0 /boot` 与前例中使用的命令等效。

![](img/8fe037bf1ed016dccb79dbd1a27184f2_556_0.png)

现在 `/etc/dumpdates` 文件的内容显示已进行了全备份：

```
[root@server1 ~]# cat /etc/dumpdates
/dev/hda2 0 Sat Jul 23 16:43:09 2005
[root@server1 ~]#
```

要执行增量备份并查看 `/etc/dumpdates` 文件的内容，可以将新磁带放入 SCSI 驱动器并执行以下命令：

```
[root@server1 ~]# dump -luf /dev/st0 /dev/hda2
DUMP: Date of this level 0 dump: Sat Jul 23 16:43:09 2005
DUMP: Date of this dump completed: Sat Jul 23 16:43:11 2005
DUMP: Dumping /dev/hda2 (/boot) to /dev/st0
DUMP: Exclude ext3 journal inode 8
nDUMP: Label: /boot
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 6485 tape blocks.
DUMP: Volume 1 started with block 1 at: Sat Jul 23 16:43:10 2005
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: Closing /dev/st0
DUMP: Volume 1 completed at: Sat Jul 23 16:43:11 2005
DUMP: Volume 1 6470 tape blocks (6.32MB)
DUMP: Volume 1 took 00:00:01
DUMP: Volume 1 transfer rate: 6470 kBytes/s
DUMP: 6470 tape blocks (6.32MB) on 1 volume(s)
DUMP: finished in 1 seconds, throughput 6470 KBytes/sec
DUMP: Date of this level 0 dump: Sat Jul 23 16:43:09 2005
DUMP: Date of this dump completed: Sat Jul 23 16:43:11 2005
DUMP: Average transfer rate: 6470 kB/s
DUMP: IS DONE
```

# 软件安装

# 543

![](img/8fe037bf1ed016dccb79dbd1a27184f2_560_0.png)

**图 12-2** X-CD-Roast 程序

获取和编译源代码的优势在于源代码并不是为特定的硬件架构创建的。编译后，程序将在其被编译的架构上执行。

> 获取 Linux 软件最常用的方法是通过互联网。附录 C，““在互联网上寻找 Linux 资源”列出了一些托管 Linux 开源软件下载的常用网站。

> 当从互联网下载文件时，许多网站会列出文件的校验和值，该值是根据文件内容计算的。几乎所有的校验和值都是使用消息摘要 5 (`MD5`) 算法计算的。为了确保下载后接收了完整的文件，你应该使用 `sum` 命令验证 `MD5` 校验和值是否相同。只需运行 `filename` 命令，其中 `filename` 是下载的文件名。

程序源代码通常以 tarball 格式分发，然后可以对 tarball 进行解压并提取源代码以便进行编译。预编译的二进制程序也可以以 tarball 格式分发，但通常以供包管理器使用的格式分发。

回想第 1 章“Linux 简介”，包管理器提供了一种分发程序的标准格式，以及一个用于存储系统上安装的软件包信息的中央数据库；这允许对软件包进行查询并方便地卸载。如今 Linux 系统中最常用的包管理器是红帽软件包管理器 (`RPM`)。

## 将源代码编译为程序

将源代码编译为二进制程序的步骤在今天大多数开源软件开发者中已经标准化的。由于大多数源代码以 tarball 格式出现，因此你必须解压并提取文件。这会在当前目录下创建一个包含源代码的子目录。此外，该目录通常还包含一个包含程序信息的 `README` 文件和一个包含安装说明的 `INSTALL` 文件。

在源目录内时，安装的第一步是运行 `configure` 程序。它会对系统要求进行初步检查，并在当前目录中创建一个名为 `Makefile` 的文件，列出需要编译的内容。
