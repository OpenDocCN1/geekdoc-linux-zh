
```bash
[root@server1 ~]$ bunzip2 -v samplefile.bz2 samplefile2.bz2
samplefile.bz2: done
samplefile2.bz2: done
[root@server1 ~]$
```

如果即将有文件被覆盖，`bunzip2` 命令会提示用户确认。要跳过此确认，你可以包含 `-f` 选项。表 11-3 列出了 `bzip2` 实用程序的其他常用选项。

### bzip2 实用程序的常用选项

| 选项 | 描述 |
| :--- | :--- |
| `-#` | 指定压缩时使用的块大小；`-1` 表示块大小为 100KB，而 `-9` 表示块大小为 900KB。 |
| `-c` <br> `--stdout` | 与 `bunzip2` 命令配合使用时，将压缩文件的内容显示到标准输出。 |
| `-d` <br> `--decompress` | 与 `bzip2` 命令配合使用时，解压缩指定的文件（等同于 `bunzip2` 命令）。 |
| `-f` <br> `--force` | 与 `bzip2` 命令配合使用时，压缩符号链接。与 `bunzip2` 命令配合使用时，不询问用户直接覆盖任何已存在的文件。 |
| `-k` <br> `--keep` | 在压缩期间保留原始文件；创建一个扩展名为 `.bz2` 的新文件。 |
| `-q` <br> `--quiet` | 抑制所有警告消息。 |
| `-s` <br> `--small` | 在压缩期间最小化内存使用。 |
| `-t` <br> `--test` | 与 `bunzip2` 命令配合使用时，执行测试解压缩，以便用户在解压缩前查看任何错误消息；它不解压缩文件。 |
| `-v` <br> `--verbose` | 在压缩和解压缩期间显示详细输出（压缩率）。 |

# 系统备份

定期创建文件和目录的备份副本并将其存储在备用位置是个好主意。然后，你可以将这些备份副本分发到其他计算机，或使用它们来恢复因系统故障而丢失的文件。整个过程被称为系统备份，文件和目录的备份副本被称为归档。

你可以在许多不同类型的介质上创建归档，例如磁带、CD、DVD 或硬盘。传统上，磁带用于备份数据。如今，大型备份通常使用单独的硬盘执行。较小的备份使用 CD 或 DVD 执行，这需要稍后本章中描述的特殊烧录软件。

表 11-4 列出了用于不同磁带设备的一些常见设备文件。

典型的 Linux 系统可以包含数十万个文件，但你不必将所有文件都包含在归档中。例如，你不必包含 `/tmp` 和 `/var/tmp` 目录中的临时文件，也不需要包含每个用户主目录下 `.mozilla` 目录中（如果你使用 Mozilla Firefox Web 浏览器）发现的任何缓存 Internet 内容。

作为一条经验法则，你应该备份主目录中的用户文件以及重要的系统配置文件，如 `/etc/passwd`。除此之外，你可能还想备份系统服务使用的文件。例如，如果 Linux 计算机用作 Web 服务器，你需要备份网站文件。像 `grep` 和 `vi` 这样的程序不需要备份，因为在系统故障时，可以从原始安装介质中恢复它们。

![](img/c27875544958897d817484d558c208c8_510_0.png)

### 常见的磁带设备文件

| 设备文件 | 描述 |
| :--- | :--- |
| `/dev/st0` | 第一个 SCSI 磁带设备（回卷） |
| `/dev/st1` | 第二个 SCSI 磁带设备（回卷） |
| `/dev/st2` | 第三个 SCSI 磁带设备（回卷） |
| `/dev/nst0` | 第一个 SCSI 磁带设备（不回卷） |
| `/dev/ht0` | 第一个 ATAPI IDE 磁带设备（回卷） |
| `/dev/nht0` | 第一个 ATAPI IDE 磁带设备（不回卷） |
| `/dev/ftape` | 第一个软盘磁带设备 |

在选定用于系统备份的文件后，你可以使用备份实用程序将文件复制到适当的介质上。有几种备份实用程序可供 Linux 管理员使用。最常见的是以下这些：

- 磁带归档 (`tar`)
- 复制进/出 (`cpio`)
- `dump/restore`
- 光盘烧录软件

# 使用磁带归档 (tar)

磁带归档 (`tar`) 实用程序是最古老、使用最广泛的备份实用程序之一，并通过 `tar` 命令执行。它可以在文件系统上的文件中或直接在设备上创建归档。

与前面讨论的压缩实用程序类似，`tar` 命令接受选项来确定归档的位置以及对归档执行的操作。指定给 `tar` 命令的任何参数都列出了要放入归档的文件。表 11-5 描绘了与 `tar` 命令一起使用的一些常用选项列表。

![](img/c27875544958897d817484d558c208c8_511_0.png)

由于 `tar` 是一个广泛使用的实用程序，表 11-5 中显示的选项也常用于其他类似命令。一个例子是 `jar` 命令，它归档 Java 编程语言使用的可复用类文件。

要创建一个名为 `/backup.tar` 的归档，其中包含当前目录的内容并查看结果，你可以使用以下命令：

```bash
[root@server1 ~]# tar -cvf /backup.tar *
Desktop/
Desktop/Home.desktop
Desktop/trash.desktop
samplefile
samplefile2

[root@server1 ~]# ls -l /backup.tar
-rw-r-r-- 1 root root 40960 Jul 27 10:49 /backup.tar

[root@server1 ~]# _
```

## 表 11-5 tar 实用程序常用选项

| 选项 | 描述 |
|---|---|
| `-A` | 将完整的归档文件追加到另一个归档文件中 |
| `--concatenate` | |
| `-C` | 创建一个新归档 |
| `--create` | |
| `--exclude PATTERN` | 在创建归档时，排除文件名中包含匹配 `PATTERN` 的文件 |
| `-f FILENAME` | 指定归档的位置（`FILENAME`）；它可以是文件系统上的文件或设备文件 |
| `--file FILENAME` | |
| `-h` | 防止 `tar` 备份符号链接；相反，`tar` 会备份符号链接的目标文件 |
| `--dereference` | |
| `-j` | 使用 `bzip2` 实用程序压缩/解压缩归档 |
| `--bzip` | |
| `-P` | 使用绝对路径名在归档中存储文件名 |
| `--absolute-paths` | |
| `-r` | 将文件追加到现有归档中 |
| `--append` | |
| `--remove-files` | 在将文件添加到归档后移除这些文件 |
| `-t` | 列出现有归档的文件名内容（目录列表） |
| `--list` | |
| `-u` | 仅当文件比归档中同名的文件更新时，才将文件追加到现有归档中 |
| `--update` | |
| `-v` | 在操作归档时显示详细输出（文件和目录信息） |
| `--verbose` | |
| `-w` | 提示用户确认每个操作 |
| `--interactive` | |
| `--confirmation` | |
| `-W` | 创建归档后验证每个归档的内容 |
| `--verify` | |
| `-x` | 提取归档的内容 |
| `--extract` | |
| `--get` | |
| `-z` | 使用 `gzip` 实用程序压缩/解压缩归档 |
| `--gzip` | |
| `--ungzip` | |
| `-Z` | 使用 `compress` 实用程序压缩/解压缩归档 |
| `--compress` | |
| `--uncompress` | |

# 第 11 章 压缩、系统备份和软件安装

根据上述命令可知，`-f` 选项后跟随归档文件的路径名，并且 `*` 元字符表示当前目录中的所有文件都将被添加到该归档中。还请注意，默认情况下文件会被递归备份，并使用相对路径名存储；若要强制在创建归档时使用绝对路径名，只需在 `tar` 命令中使用 `-P` 选项即可。

![](img/c27875544958897d817484d558c208c8_513_0.png)

用于归档的文件名不需要有扩展名。但是，为了识别其内容，为归档文件添加扩展名是一个良好的实践，例如前面示例中的 `/backup.tar`。

![](img/c27875544958897d817484d558c208c8_513_1.png)

`tar` 实用程序无法备份设备文件或文件名长度超过 255 个字符的文件。

创建归档后，可以通过指定 `tar` 命令的 `-t`（目录列表）选项和要查看的归档来查看其详细内容。例如，要查看前面创建的 `/backup.tar` 归档的详细内容，可以发出以下命令：

```
[root@server1 ~]# tar -tvf /backup.tar
drwx------ root/root        0 2015-07-21 08:15 Desktop/
-rw-r--r-- root/root     3595 2015-06-21 20:32 Desktop/Home.desktop
-rw-r--r-- root/root     3595 2015-06-21 20:32 Desktop/trash.desktop
-rw-r--r-- root/root    20239 2015-07-21 08:15 samplefile
-rw-rw-r-- root/root      574 2015-07-21 08:18 samplefile2
[root@server1 ~]# _
```

您可以使用 `tar` 命令的 `-x` 选项来提取指定的归档。要将 `/backup.tar` 文件的内容提取到一个名为 `/tartest` 的新目录中并查看结果，您可以发出以下命令：

```
[root@server1 ~]# mkdir /tartest
[root@server1 ~]# cd /tartest
[root@server1 tartest]# tar -xvf /backup.tar
Desktop/
Desktop/Home.desktop
Desktop/trash.desktop
samplefile
samplefile2
[root@server1 tartest]# ls -F
Desktop/ samplefile samplefile2
[root@server1 tartest]# _
```

在文件系统上的文件中创建归档后，可以通过网络或 Internet 将该文件发送到其他计算机。这是当今最常见的备份形式，也是通过 Internet 分发软件的常用方法。不幸的是，`tar` 实用程序不会压缩归档内的文件。因此，通过网络传输归档所需的时间较长。为了减少传输时间，您可以在传输之前使用压缩实用程序压缩归档。由于这是一项常见任务，`tar` 命令接受允许您在创建后立即使用 `compress`、`gzip` 或 `bzip2` 命令压缩归档的选项。

要创建一个名为 `/backup.tar.gz` 的 `gzip` 压缩归档，该归档包含当前目录的内容并查看结果，您可以使用以下命令：

```
[root@server1 ~]# tar -zcvf /backup.tar.gz *
Desktop/
Desktop/Home.desktop
Desktop/trash.desktop
samplefile
samplefile2
[root@server1 ~]#
```

```
[root@server1 ~]# ls -l /backup.tar*
-rw-r--r--  1 root  root  40960 Jul 27 10:49 /backup.tar
-rw-r--r--  1 root  root  12207 Jul 27 11:18 /backup.tar.gz
```

在前面的输出中请注意，`-z` 选项表示使用 `gzip` 实用程序进行压缩，并且我们选择以 `.tar.gz` 扩展名结尾。此外，`/backup.tar.gz` 文件的大小远小于之前创建的 `/backup.tar` 文件。

![](img/c27875544958897d817484d558c208c8_514_0.png)

> 以 `.tar.gz` 或 `.tgz` 扩展名结尾的文件名通常被称为 tarballs（压缩包），因为它们代表压缩的 `tar` 归档。

要查看 `gzip` 压缩归档的内容，除了 `-t` 选项外，您还必须使用 `-z` 选项，后接要查看的归档。可以使用以下命令查看 `/backup.tar.gz` 文件的详细内容：

```
[root@server1 ~]# tar -ztvf /backup.tar.gz
drw-x------  root/root        0 2015-07-21 08:15 Desktop/
-rw-r--r--  root/root     3595 2015-06-21 20:32 Desktop/Home.desktop
-rw-r--r--  root/root     3595 2015-06-21 20:32 Desktop/trash.desktop
-rw-r--r--  root/root    20239 2015-07-21 08:15 samplefile
-rw-rw-f--  root/root      574 2015-07-21 08:18 samplefile2
```

同样，在提取 `gzip` 压缩归档时，您必须向 `tar` 命令提供 `-z` 选项。要将 `/backup.tar.gz` 文件的内容提取到一个名为 `tartest2` 的新目录中并查看结果，您可以发出以下命令：

```
[root@server1 ~]# mkdir tartest2
[root@server1 ~]# cd tartest2
[root@server1 tartest2]# tar -zxvf /backup.tar.gz
Desktop/
Desktop/Home.desktop
Desktop/trash.desktop
samplefile
samplefile2
[root@server1 tartest2]#
```

```
[root@server1 tartest2]# ls -F
Desktop/  samplefile*  samplefile2
```

将文件备份到文件系统上的压缩归档中，当您计划通过网络传输归档数据时很有用。然而，您可以使用 `tar` 将数据直接备份到设备（如磁带）上。要将文件备份到设备，您可以使用 `tar` 命令的 `-f` 选项来指定相应设备文件的路径名。然后，文件将被直接传输到设备，覆盖可能存在任何其他数据或文件系统。

例如，要在第一个可回绕 SCSI 磁带设备上创建一个包含当前目录内容的归档，您可以使用以下命令：

```
[root@server1 ~]# tar -cvf /dev/st0 *
Desktop/
Desktop/Home.desktop
Desktop/trash.desktop
samplefile
samplefile2
[root@server1 ~]#
```

然后，您可以使用命令 `tar -tvf /dev/st0` 查看前面示例中使用的磁带设备上归档的内容，或者使用命令 `tar -xvf /dev/st0` 提取磁带设备上归档的内容，方式类似于前面显示的示例。

由于磁带设备可以存储大量信息，您可能希望向已存在于磁带设备上的 `tar` 归档中添加内容。为此，只需在使用 `tar` 实用程序时，将 `-c` 选项替换为 `-r` 选项即可。例如，要将名为 `samplefile3` 的文件追加到前一次输出中创建的归档并查看结果，您可以使用以下命令：

```
[root@server1 ~]# tar -rvf /dev/st0 samplefile3
samplefile3
[root@server1 ~]# tar -tvf /dev/st0
drwx------ root/root 0 2010-07-21 08:15 Desktop/
-rw-r--r-- root/root 3595 2010-06-21 20:32 Desktop/Home.desktop
-rw-r--r-- root/root 3595 2010-06-21 20:32 Desktop/trash.desktop
-rw-r--r-- root/root 20239 2010-07-21 08:15 samplefile
-rw-rw-f-r root/root 574 2010-07-21 08:18 samplefile2
-rw-r--r-- root/root 147 2010-07-27 16:15 samplefile3
[root@server1 ~]# _
```

## 使用 复制进/出 (cpio)

另一个常用的备份实用程序是 `copy in/out` (`cpio`)，可以通过 `cpio` 命令执行。虽然 `cpio` 使用与 `tar` 类似的选项，但它具有一些附加功能，包括支持长文件名和备份设备文件的能力。

由于其主要用途是在系统故障时备份文件，`cpio` 在归档时默认使用绝对路径名。此外，`cpio` 通常从标准输入获取要归档的文件列表，并将文件“输出”到由 `-O` 选项指定的归档中。相反，在提取归档时，您必须包含 `-I` 选项以指示从中“输入”文件的归档。

表 11-6 提供了 `cpio` 命令常用选项及其描述的列表。

## 表 11-6 与 cpio 实用程序常用的选项

| 选项 | 描述 |
|---|---|
| `-A` | 向现有归档追加文件 |
| `-append` | |
| `-B` | 将默认块大小从 512 字节更改为 5KB，从而加快信息传输速度 |
| `-c` | 使用一种存储格式（SVR4），该格式被 UNIX 和 Linux 的不同版本 `cpio` 广泛识别 |
| `-d` | 在提取过程中按需创建目录 |
| `-make-directories` | |
| `-i` | 从归档中读取文件 |
| `-extract` | |
