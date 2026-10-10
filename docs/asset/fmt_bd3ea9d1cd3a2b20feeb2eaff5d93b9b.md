
### `gzip` 工具优势与压缩级别

`gzip` 工具优于 `compress` 工具的优势之一是它可以通过数字选项来控制压缩级别。`-1` 产生快速压缩，但压缩率较低。相反，`-9` 产生最高的压缩率，但处理时间更长。如果未指定压缩级别，`gzip` 将使用级别 6。

以下命令使用快速压缩压缩 `samplefile` 并显示压缩率：

```
[root@localhost]# gzip -v -1 samplefile
samplefile: 51.3% -- replaced with samplefile.gz
[root@localhost]#
```

请注意，`samplefile` 的压缩比例为 51.3%，这低于之前使用默认级别 6 时获得的 56.8%。

注意：在解压文件时不需要指定压缩级别，因为该信息已内置在压缩文件本身。

`gzip` 工具还有许多其他选项用于压缩，且其中许多选项都有等效的 POSIX 选项。这些选项的列表所示。

## 13-7 压缩、备份和软件安装

| 选项 | 说明 |
|--- | --- |
| `#` | 指定压缩的彻底程度，其中 `#` 可以是数字 1-9（选项 `-1` 代表快速压缩，压缩耗时较短但压缩率较低；选项 `-9` 代表彻底压缩，耗时较长但压缩率较高） |
| `--best` | 与 `-9` 选项相同；产生更高的压缩率 |
| `-c`, `--stdout`, `--to-stdout` | 与 `gzip` 命令配合使用，将压缩文件的内容显示到标准输出（功能与 `zcat` 命令相同） |
| `-d`, `--decompress`, `--uncompress` | 与 `gzip` 命令配合使用，解压指定的文件（功能与 `zcat` 命令相同） |
| `-f`, `--force` | 与 `gzip` 命令配合使用，用于压缩符号链接；与 `gzip` 命令配合使用，在不提示用户的情况下覆盖任何现有文件 |
| `--fast` | 与 `-1` 选项相同；产生较低的压缩率 |
| `-h`, `--help` | 显示 `gzip` 命令的语法和可用选项 |
| `-l`, `--list` | 列出使用 `gzip` 压缩的文件的压缩率 |
| `-n`, `--no-name` | 不保留文件的原始修改时间和访问时间 |
| `-q`, `--quiet` | 抑制所有警告消息 |
| `-r`, `--recursive` | 递归地指定目录内所有文件的压缩或解压 |
| `-S suffix`, `--suffix` | 在压缩或解压文件时指定 `.gz` 以外的文件后缀 |
| `-t`, `--test` | 与 `gzip` 命令配合使用，进行解压测试，使用使用户可以查看任何错误消息；不进行压缩 |
| `-v`, `--verbose` | 在压缩和解压期间显示详细输出（压缩率和文件名） |

# 压缩、备份与软件安装 13-11

- 11 输入以下命令：
`ps -ef | compress -v >psfile.Z`

将 `ps -ef` 命令的输出压缩到名为 `psfile.Z` 的文件中。

- 12 输入 `zmore psfile.Z`

查看 `psfile.Z` 文件的压缩内容。

按 `q` 退出 `more` 实用程序。

- 13 输入 `gzip -v termcap`

压缩 `termcap` 文件。

- 输入 `ls -l termcap.gz`

显示关于 `termcap` 的信息。

- 14 输入 `gunzip -v termcap.gz`

解压 `termcap` 文件。

- 15 输入 `gzip -v -9 termcap`

压缩 `termcap` 文件。注意压缩比率。

- 16 输入 `gunzip -v termcap.gz`

解压 `termcap` 文件。

- 17 输入 `gunzip -v -1 termcap`

解压 `termcap` 文件。注意压缩比率。

- 18 输入 `gunzip -v termcap.gz`

解压 `termcap` 文件。

- 19 输入 `bzip2 -v termcap`

压缩 `termcap` 文件。注意压缩比率。

- 20 输入 `ls -l termcap.bz2`

查看 `termcap` 文件的文件信息。

- 21 输入以下命令：
`bunzip2 -v termcap.bz2`

解压 `termcap` 文件。

- 22 输入 `exit`

注销。

# 主题 B：系统备份

本主题涵盖以下 CompTIA Linux+ 考试目标。

| # | 目标 | |
|---|---|---|
| 1.9 | 安装操作系统后管理包。 | `tar` |
| 2.8 | 执行并验证备份与恢复。 | `tar`, `cpio` |
| 2.9 | 访问并向可记录介质写入数据。 | CDRW, 硬盘, `flash` |
| 6.5 | 识别并配置大规模存储设备和 RAID。 | `ATAPI`, 磁带, 光学记录 |

## 备份的重要性

保护数据和系统的关键之一是对组成用户和系统的文件和目录创建副本。无论你是将文件副本保存到软盘，还是将整个卷或系统复制到 DLT 磁带，你都在创建文件的备份副本，当原始文件丢失或损坏时可以使用这些副本。备份副本通常称为归档。

## 备份介质

归档可以在许多不同的介质上创建，例如磁带、Zip 磁盘、闪 设备、软盘、CD-RW/DVD-RW 设备或硬盘。每种介质在便利性、容量、制作方式以及介质可靠性方面都有其优缺点。用于备份大量数据最常用的介质是几种磁带格式之一，例如 DLT 盒。

以下是一些用于各种磁带设备的设备文件列表。

| 设备文件 | 说明 |
|---|---|
| `/dev/st0` | 第一个 SCSI 磁带设备（卷绕） |
| `/dev/st1` | 第二个 SCSI 磁带设备（卷绕） |
| `/dev/st2` | 第三个 SCSI 磁带设备（卷绕） |
| `/dev/nst0` | 第一个 SCSI 磁带设备（非卷绕） |
| `/dev/ht0` | 第一个 ATAPI 磁带设备（卷绕） |
| `/dev/nht0` | 第一个 ATAPI 磁带设备（非卷绕） |
| `/dev/ftape` | 第一个软盘磁带设备 |

注意：磁带 (`mt`) 命令可用于操作磁带设备或为系统备份准备磁带。例如，要卷绕系统上的第一个磁带设备，可以使用命令 `mt -f /dev/st0`。

## 备份计划

典型的 Linux 系统可能有几十万个文件，但并不是所有文件都需要包含在归档中。不应进行归档的文件示例包括：

- `/tmp` 和 `/var/tmp` 目录下的临时文件
- 浏览器保存在用户主目录中的缓存 Internet 内容

应该备份的文件示例包括：

- 主目录下的用户文件
- 重要的系统配置文件，如 `/etc/passwd`
- 系统服务使用的文件，例如数据库或网站文件（如果该系统是 Web 服务器）

如 `grep` 和 `vi` 等程序不需要备份，因为它们可以从原始安装介质恢复。

在选择好用于系统备份的文件后，你可以使用备份工具将文件复制到归档介质。

# 13-14 CompTIA Linux+ 认证， 2004 目标

动手吧！

## B-1：讨论备份介质

### 练习

1. `mt` 命令可操作磁带设备或为系统备份准备磁带。真或否？

2. 下列哪项代表系统上的第一个非卷绕 SCSI 磁带设备？
A `/dev/st0`
B `/dev/nst0`
C `/dev/ht0`
D `/dev/nst0`

3. ______ 是备份大量数据最常用的介质。
A Zip 磁盘
B 硬盘
C CD-RW 光盘
磁带

4. ______ 是通常不应归档的目录示例。
A `/etc/passwd`
B `/tmp`
C `/var/http`
D `/var/database`

# 备份工具

说明
Linux 管理员可以使用多种备份工具。最常见的有：

- `tar`
- `cpio`
- `dump`/`restore`
- 刻录软件

## `tar` 工具

磁带归档 (`tar`) 工具是最古老且常用的备份工具之一。它可以在文件系统或设备上创建归档。

与压缩工具一样，`tar` 接受参数来决定归档的位置以及对其进行的操作。参数指定要放入归档的文件。使用 `tar` 可以以多种方式创建归档，如下所示。

| 选项 | 说明 |
|---|---|
| `-A`, `--concatenate` | 将归档合并到归档 |
| `-c`, `--create` | 创建新归档 |
| `--exclude filename` | 创建归档时排除文件名 |
| `-f filename` | 指定归档的位置（可以是文件或设备） |
| `-h`, `--dereference` | 防止 `tar` 备份符号链接，而是备份链接的目标文件 |
| `-j`, `--bzip` | 使用 `bzip` 压缩归档 |
| `-P`, `--absolute-paths` | 使用绝对路径存储文件名 |
| `-r`, `--append` | 将文件追加到现有归档 |
| `--remove-files` | 添加后删除文件 |
| `-t`, `--list` | 列出归档内容 |
| `-u`, `--update` | 如果文件比归档中的文件新，则追加到归档 |
| `-v`, `--verbose` | 操作归档时显示详细输出 |

| 选项 | 说明 |
|---|---|
| `-w`, `--interactive` | 询问用户确认每个归档 |
| `-W`, `--verify` | 创建后验证归档内容 |
| `-x`, `--extract`, `--get` | 提取归档内容 |
| `-z`, `--gzip`, `--ungzip` | 使用 `gzip` 压缩/解压 |
| `-Z`, `--compress`, `--uncompress` | 使用 `compress` 压缩/解压 |

创建一个包含当前目录内容的 `backup.tar` 并查看结果，使用以下命令：

```
[root@localhost root]# tar -cvf /backup.tar
Desktop/
Desktop/starthere.desktop
samplefile
sample2
[root@localhost root]# ls -l /backup.tar
```

注意上述命令中 `f` 后面是归档路径，`*` 表示当前目录中的所有文件都添加到此归档中。

此外注意默认使用相对路径进行备份。要在创建归档时强制使用绝对路径，只需使用 `-P` 选项。

归档文件名不需要扩展名，但包含一个会更好。扩展名标识该文件是由工具创建的归档。

注意：`tar` 工具无法备份设备文件或文件名超过 255 个字符的文件。

可以使用 `-t`（内容列表）选项查看归档的详细内容。查看 `/backup.tar` 的详细内容，使用以下命令：

```
[root@localhost root]# tar -tvf /backup.tar
drwxr-xr-x root 0 2005-07-21 08:15:09 Desktop/
-rw-r--r-- root 3595 2005-07-21 20:32:48 Desktop/starthere.desktop
-rw-r--r-- root 20239 2005-07-21 08:15:35 samplefile
-rw-r--r-- root 574 2005-07-21 18:18:08 sample2
[root@localhost root]#
```

# 压缩、备份与软件安装 13-17

`-x` 选项用于提取指定的归包。要将 `/backup.tar` 的内容提取到名为 `/tartest` 的新目录并查看结果，你可以使用以下命令：

```
[root@localhost root]# mkdir /tartest
[root@localhost root]# cd /tartest
[root@localhost tartest]# tar -xvf /backup.tar
Desktop/
Desktop/starthere.desktop
samplefile
sample2
[root@localhost tartest]# ls -F
Desktop/ samplefile sample2
[root@localhost tartest]#
```

## 压缩归包

归包可以保存到备份介质或通过网络发送到另一台计算机进行存储或使用。遗憾的是，`tar` 不压缩归包内部的文件，因此存储它所需的空间或通过网络传输归包所需可能会很高。

压缩归包通常用于软件分发，其中很小的文件可以被压缩并解包，以创建存储在复杂结构中的许多文件。这些归包通常被称为 `tar` 包（`tarballs`）。文件名通常以 `.tar` 或 `.gz` 扩展名结尾，并保持为 `gzip` 压缩归包。

`tar` 命令接受各种选项，允许你使用 `compress`、`gzip` 或 `bzip2` 之一之一。要创建一个包含当前目录内容的 `gzip` 压缩归包并查看结果，你可以使用以下命令：

```
[root@localhost root]# tar -zcvf /backup.tar.gz *
Desktop/
Desktop/starthere.desktop
samplefile
[root@localhost root]# ls -l /backup.tar
-rw-r--r-- 1 root root 40960 Jul 27 10:49 /backup.tar
-rw-r--r-- 1 root root 12207 Jul 27 21:18 /backup.tar.gz
[root@localhost root]#
```

`-z` 选项表示使用 `gzip` 工具进行压缩。我们在文件名结尾使用 `.tar.gz` 扩展名，以表示归包格式和压缩方法。

注意 `/backup.tar.gz` 文件的大小远小于之前创建的 `/backup.tar` 文件。

> 注意：要查看 `gzip` 压缩归包的内容，请包含 `-z` 和 `-t` 选项，并指定要查看的归包。

```
[root@localhost root]# tar -ztvf /backup.tar.gz
drwx-xr-x root root 0 2025-07-21 08:15:09 Desktop/
-rw-r--r-- 1 root root 3595 2025-06-21 20:32:48 Desktop/starthere.desktop
-rw-r--r-- 1 root root 20239 2025-07-21 08:15:35 samplefile
-rw-rw-w-- 1 root root 574 2025-07-21 08:18:08 samplefile2
[root@localhost root]#
```

# 13-18 CompTIA Linux+ 认证，2004 目标

在提取 `gzip` 压缩归包时，对 `tar` 命令使用 `-z` 选项。要将 `/backup.tar.gz` 的内容提取到名为 `target2` 的新目录并查看结果，你可以使用以下命令：

```
[root@localhost root]# mkdir /target2
[root@localhost root]# cd /target2
[root@localhost target2]# tar -zxvf /backup.tar.gz
Desktop/
Desktop/starthere.desktop
samplefile
samplefile
[root@localhost target2]# ls -F
Desktop/ samplefile samplefile2
[root@localhost target2]#
```

## 与 `tar` 磁带设备配合

如果你打算通过网络发送归包，将文件备份到活动文件系统上的压缩归包中是可以的。但并不是为了安全或系统恢复备份大量数据的好方法。
可拆卸的高容量设备（如磁带）对于保护系统归包更好。这些设备不应每天使用，因此受损的可能性较小。而且介质可以存储在外部的安全位置。

要将文件备份到设备，你再次使用 `-f` 文件位置选项，但要指定相应设备文件的路径。归包文件将直接传输到设备，覆盖可能存在的任何其他数据或文件系统。
例如，要在第一个卷 SCSI 磁带设备上创建一个包含当前设备内容的归包，可以使用以下命令：

```
[root@localhost root]# tar -cvf /dev/st0 *
Desktop/
Desktop/starthere.desktop
samplefile
samplefile
[root@localhost root]#
```
