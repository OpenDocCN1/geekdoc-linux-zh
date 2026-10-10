
另一个良好的实践是在 tar 归档创建后立即自动验证备份。这很容易通过附加 `-W` 选项来实现，如清单 12.11 所示。

### 清单 12.11 使用 tar 自动验证备份的文件

```console
$ tar -Wcvf ProjectVerify.tar Project4?.txt
Project42.txt
Project43.txt
Project44.txt
Project45.txt
Project46.txt
Verify Project42.txt
Verify Project43.txt
Verify Project44.txt
Verify Project45.txt
Verify Project46.txt
$
```

如果您使用压缩来创建 tar 包，则不能使用 `-W` 选项。但是，您可以先创建并验证归档文件，然后在单独的步骤中对其进行压缩。您还可以在从 tar 归档文件中提取文件时使用 `-W` 选项。这对于立即验证从归档恢复的文件非常方便。

表 12.4 列出了一些您可以使用 tar 实用程序从 tar 归档文件或 tar 包中恢复数据的选项。请注意，用于创建备份的某些选项，例如 `-g` 和 `-W`，也可以在恢复数据时使用。

### 表 12.4 tar 命令常用的文件恢复选项

| 短选项 | 长选项 | 描述 |
|:---|:---|:---|
| `-x` | `--extract` | 从 tar 包或归档文件中提取文件，并将其放置在当前工作目录中 |
| | `--get` | |
| `-z` | `--gunzip` | 使用 gunzip 解压缩 tar 包中的文件 |
| `-j` | `--bunzip2` | 使用 bunzip2 解压缩 tar 包中的文件 |
| `-J` | `--unxz` | 使用 unxz 解压缩 tar 包中的文件 |

使用 tar 实用程序从归档文件或 tar 包中提取文件相当简单。清单 12.12 展示了一个从先前创建的 tar 包中提取文件的示例。

### 清单 12.12 使用 tar 从 tar 包中提取文件

```
$ mkdir Extract
$
$ mv Project4x.tar.gz Extract/
$
$ cd Extract
$
$ tar -zxvf Project4x.tar.gz
Project42.txt
Project43.txt
Project44.txt
Project45.txt
Project46.txt
$
$ ls
Project42.txt Project44.txt Project46.txt
Project43.txt Project45.txt Project4x.tar.gz
$
```

在清单 12.12 中，创建了一个新的子目录 Extract。将清单 12.6 中创建的 tar 包移动到新子目录中，然后从 tar 包中恢复文件。如果您将此清单中使用的 tar 命令与清单 12.6 中使用的命令进行比较，您会注意到这里用 `-o` 选项取代了清单 12.6 中使用的 `-c` 选项。另外，请注意在清单 12.12 中，文件提取后并未移除 tar 包，因此您可以根据需要反复使用它。

![](img/c0a399aca0d18f8822d714ad0a173123_442_0.png)

> tar 命令还有许多其他功能，例如使用 tar 备份参数和/或创建备份和恢复 shell 脚本的能力。请访问 GNU tar 网站 www.gnu.org/software/tar/manual，以了解更多关于这个流行的命令行备份工具的信息。

由于 tar 实用程序是磁带归档器，如果您愿意，还可以将 tar 包或归档文件放置在磁带上。在挂载并正确定位磁带后，只需在 tar 命令中用 SCSI 磁带设备文件名（如 /dev/st0 或 /dev/nst0）替换归档或 tar 包文件名即可。

## 使用 dd 进行复制

dd 实用程序允许您备份磁盘上的几乎所有内容，包括一些较旧的 Linux 发行版仍在使用旧的主引导记录（MBR）分区。它主要用于创建整个硬盘或分区的低级副本。它常用于数字取证中创建系统镜像、复制损坏的磁盘以及擦除分区。

该命令本身相当简单。dd 实用程序的基本语法结构如下：

```
dd  if=input-device of=output-device [OPERANDS]
```

output-device 是整个驱动器或分区。input-device 也是如此。请确保为 out 选择正确的设备，为 in 选择正确的设备；否则，您可能会无意中擦除数据。

除了 of 和 if 之外，还有几个其他参数（称为操作数）可以帮助进行 dd 操作。常用选项在表 12.5 中进行了描述。

### 表 12.5 dd 命令常用的操作数

| 操作数 | 描述 |
| :--- | :--- |
| bs=BYTES | 设置一次读取和写入的最大块大小（BYTES 的数量）。默认值为 512 字节。 |
| count=N | 设置要复制的输入块数量（N）。 |
| status=LEVEL | 设置显示到 STDERR 的信息量（LEVEL）。 |

status=LEVEL 操作数需要稍作解释。LEVEL 可以设置为以下值之一：

- none 仅显示错误消息。
- noxfer 不显示最终传输统计信息。
- progress 显示定期传输统计信息。

通常通过示例来理解 dd 实用程序更容易。清单 12.13 展示了一个将一个完整磁盘逐位复制到另一个磁盘的简化示例。

### 清单 12.13 使用 dd 复制整个磁盘

```
# lsblk
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT

[..]
  sdb      8:16   0  4M 0 disk
   |sdb1   8:17   0  4M 0 part
  sdc      8:32   0  1G 0 disk
   |sdc1   8:33   0 1023M 0 part
[..]

# dd if=/dev/sdb of=/dev/sdc status=progress
8192+0 records in
8192+0 records out
4194304 bytes (4.2 MB) copied, 0.232975 s, 18.0 MB/s
#
```

在清单 12.13 中，首先使用 `lsblk` 命令。当通过 `dd` 实用程序复制磁盘时，请确保驱动器未在虚拟目录结构中的任何位置挂载。此操作中涉及的两个驱动器 `/dev/sdb` 和 `/dev/sdc` 均未挂载。在 `dd` 命令中，使用 `if` 操作数指示要复制的磁盘，即 `/dev/sdb` 驱动器。`of` 操作数表示 `/dev/sdc` 磁盘将存储复制的数据。此外，`status=progress` 将显示定期传输统计信息。您可以从清单 12.13 中的传输统计信息看出 `/dev/sdb` 上没有太多数据，因此 `dd` 操作很快完成。

您还可以使用类似于清单 12.13 中显示的 `dd` 命令来创建系统镜像备份，只需进行一些必要的修改即可。基本步骤如下：

1. 关闭您的 Linux 系统。
2. 连接必要的备用驱动器。您需要为每个系统驱动器准备一个相同大小或更大的驱动器。
3. 使用 live CD、DVD 或 USB 启动系统，以便在备份操作之前保持系统驱动器未挂载或取消挂载它们。
4. 对于每个系统驱动器，发出一个 `dd` 命令，使用 `if` 操作数指定要备份的驱动器，使用 `of` 操作数指定备用驱动器。
5. 关闭系统，并移除包含系统镜像的备用驱动器。
6. 重新启动您的 Linux 系统。

如果您有一个不再使用的磁盘，您还可以使用 `dd` 命令将磁盘清零。示例显示在清单 12.14 中。

### 清单 12.14 使用 dd 将整个磁盘清零

```
# dd if=/dev/zero of=/dev/sdc status=progress
1061274672 bytes (1.1 GB) copied, 33.196299 s, 32.0 MB/s
dd: writing to '/dev/sdc': No space left on device
2097153+0 records in
2097152+0 records out
1073741824 bytes (1.1 GB) copied, 34.6304 s, 31.0 MB/s
#
```

`if=/dev/zero` 使用零设备文件向磁盘写入零。您需要至少执行此操作 10 次或更多次才能彻底擦除磁盘。您也可以使用 `/dev/random` 和/或 `/dev/urandom` 设备文件向磁盘写入随机数据。对于大型磁盘，此特定任务可能需要很长时间才能运行。最好仍然粉碎不再由您的公司使用的任何磁盘。

## 使用 rsync 进行复制

`rsync` 实用程序在第三章“管理文件、目录和文本”中首次介绍，以其速度著称。使用此程序，您可以在本地或远程复制文件，它非常适合创建备份。

在探索 `rsync` 程序之前，最好回顾一下几个常用选项。第三章中的表 3.4 包含了更常用的 `rsync` 选项。除了表 3.4 中列出的选项外，还有几个额外的开关有助于通过 `rsync` 实用程序进行安全数据传输：

- `-e` 或 `-rs` 选项更改用于本地和远程连接之间通信的程序。默认是 OpenSSH。
- `-z` 或 `--compress` 选项在传输过程中压缩文件数据。

在第三章中，我们简要提到了归档选项 `-a`（或 `--archive`），它指示 `rsync` 执行备份复制。但是，它需要更多的解释。此选项相当于使用 `-rlptgoD` 选项，并执行以下操作：

- 指示 `rsync` 复制目录内容，对于原始目录树内的任何子目录，依次复制其内容（递归地）。
- 保留以下项目：
  - 设备文件（仅在以超级用户权限运行时）
  - 文件组
  - 文件修改时间
  - 文件所有权（仅在以超级用户权限运行时）
  - 文件权限
  - 特殊文件
  - 符号链接

在本地进行 `rsync` 备份相当简单。最流行的选项 `-ahv` 允许您快速将文件备份到本地位置，如清单 12.15 所示。

### 清单 12.15 使用 `rsync` 在本地备份文件

```bash
$ ls -sh *.tar
40K Project4x.tar   40K ProjectVerify.tar
$
$ mkdir TarStorage
$
$ rsync -ahv *.tar TarStorage/
sending incremental file list
Project4x.tar
ProjectVerify.tar
```

