
```
$ lsblk
NAME  SIZE RO MOUNTPOINT
sda   500G 0
└─sda1 500G 1 /
sdb   500G 0
sdc   500G 0

$ dd if=/dev/sdb of=/dev/sdc bs=4M status=progress
106172462 bytes (1.1 GB) copied, 33.19629 s, 32.0 MB/s
dw: writing to '/dev/sdc' No space on device
1073741824 bytes (1.1 GB) copied, 34.6304 s, 31.8 MB/s
#
```

在列表 12.13 中，首先使用了`lsblk`。当通过`dd`复制磁盘时，最好确保磁盘已卸载。在列表 12.13 中，我们将`sdb`复制到`sdc`。`status=progress`操作数表示`sdb`上没有多少数据，因此`dd`操作很快完成了。

### 列表 12.14：使用 `dd` 零化整个磁盘

```
$ dd if=/dev/zero of=/dev/sdc bs=4M status=progress
106172462 bytes (1.1 GB) copied, 33.19629 s, 32.0 MB/s
dw: writing to '/dev/sdc' No space on device
1073741824 bytes (1.1 GB) copied, 34.6304 s, 31.8 MB/s
#
```

> `if=/dev/zero`使用设备文件向磁盘写入零。你需要至少执行此操作 10 次或更多才能彻底擦除磁盘。你也可以使用`/dev/random`和/或`/dev/urandom`文件向磁盘写入随机数据。这个特定任务对于大磁盘来说可能运行很长时间。

## 使用 `rsync` 复制

最初在第 3 章中介绍过，`rsync`工具以速度著称。通过这个程序，你可以在本地或远程复制文件，它对于创建备份非常有用。

在探索`rsync`程序之前，回顾一些常用的选项是一个好主意。第 3 章中的表 3.4 包含了更常用的`rsync`选项。除了表 3.4 中列出的选项外，还有几个额外的开关可以帮助通过`rsync`实用程序进行安全传输：

- `-e, --ssh`选项更改用于本地和远程连接之间通信的shell。默认值是`OpenSSH`。

- `-z`或`--compress`选项在传输过程中压缩文件数据。

在第 3 章中，我们简要地提到了归档选项`-a`（或`--archive`），它指示`rsync`执行备份拷贝。然而，这需要更多的解释。该选项等同于使用`-rlptgoD`选项，并执行以下操作：

- 留存以下项目：

  - 设备文件（仅在以超级用户权限运行时）

  - 文件组

  - 文件修改时间

  - 文件所有权（仅在以超级用户权限运行时）

  - 文件权限

  - 特殊文件

  - 符号链接

在本地进行`rsync`备份非常简单。最流行的选项`-ahv`允许你将文件备份到本地位置，如列表 12.15 所示。

# 列表 12.15：使用 `rsync` 本备份文件

```
$ ls -sh *.tar
40K Project4x.tar 40K ProjectVerify.tar
$
$ mkdir TarStorage
$
$ rsync -avh *.tar TarStorage/
sending incremental file list
Project4x.tar
ProjectVerify.tar

sent 82.1K bytes received 54 bytes 164.3K bytes/sec
total size is 81.92K speedup is 1.00
$
$ ls TarStorage
Project4x.tar ProjectVerify.tar
$
```

## 比较归档和恢复工具

`rsync`实用程序真正大放异是在网络备份时保护文件。

为了使远程拷贝生效，需要在远程系统上运行`OpenSSH`服务。此外，本地和远程机器都必须安装`rsync`实用程序。使用`rsync`命令在网络上安全拷贝文件的示例如列表 12.16 所示。

# 列表 12.16：使用 `rsync` 远程备份文件

```
$ ls -sh *.tar
40K Project4.tar 40K ProjectVerify.tar
$
$ rsync -avP -e ssh *.tar user1@192.168.0.104:
user1@192.168.0.104 password:
sending incremental file list
Project4.tar
  40,960 100% 0:00:00 (xfr#1, to-chk=1/2)
ProjectVerify.tar
  40,960 100% 39.06MB/s 0:00:00 (xfr#2, to-chk=0/2)
sent 82,121 bytes received 54 bytes, 18,261 bytes/sec
total size is 81,920 speedup is 1.00
$
```

注意列表 12.16 中使用了`-avP`选项，将在文件传输发生时提供详细信息。此列表中需要注意的重要开关是`-e`选项。该选项决定使用`OpenSSH`进行传输，并有效地创建了一个加密隧道，使得网络嗅探无法捕获流动的数据。命令中的`*.tar`选择了哪些本地文件要拷贝到远程机器。`rsync`命令中的最后一个参数指定了以下内容：

- 用于传输的位于远程系统的用户账户（`user1`）。

- 远程系统的IPv4 地址，也可以使用主机名。

- 文件存放的位置。在这种情况下，它是家目录，由`~`符号表示。

同样注意在最后一个参数中，IPv4 地址和目录符号之间有一个必要的冒号（`:`）。如果你不包含此冒号，你会将文件拷贝到本地目录中名为`user1@192.168.0.104~`的新文件中。

> `rsync`实用程序默认使用`OpenSSH`。然而，使用`-e`选项是一个好习惯。如果你在使用任何`ssh`命令选项（例如指定要使用的`OpenSSH`密钥或使用不同于默认端口 22 的端口），这一点是正确的。`OpenSSH`将在第 16 章中有更详细的介绍。

`rsync`实用程序对于将大文件拷贝到远程媒介非常有用。如果你有快速的CPU 但网络连接缓慢，可以通过采用`rsync -z`选项压缩传输数据来进一步提高速度。这并不是使用`gzip`压缩，而是通过`zlib`压缩库应用压缩。你可以在`https://zlib.net`找到更多关于`zlib`的信息。

## 保护异地/异系统备份

在业务中，数据就是钱。创建数据归档至关重要，保护它们也同样重要。当将备份传输到远程位置时，有一些额外的方法可以确保备份的安全。

除了`rsync`，你还可以使用`scp`实用程序，它基于安全拷贝协议（SCP）。此外，基于SSH 文件传输协议（SFTP）的`sftp`程序也是一种安全传输归档的手段。我们将在接下来的章节中介绍这两个实用程序。

## 通过 `scp` 安全拷贝

`scp`实用程序用于在两个系统之间以非交互方式快速传输文件。它使用`OpenSSH`。它最适合需要安全拷贝的小文件，因为如果在操作过程中发生中断，它无法断点继续。对于较大的文件或大量数量的文件，使用`rsync`或`sftp`更好。有一些实用的`scp`选项，如表 12.6 所示。

### 表 12.6：`scp` 命令常用选项

| 简写 | 说明 |
| :--- | :--- |
| `-C` | 在传输期间压缩文件 |
| `-p` | 保留文件访问时间和修改时间 |
| `-r` | 递归地拷贝目录及其任何子目录 |
| `-v` | 显示命令执行的详细信息 |

从本地系统到远程系统的安全拷贝非常简单。你需要在远程系统上运行`OpenSSH`。示例如列表 12.17 所示。

# 列表 12.17：使用 `scp` 安全拷贝到远程系统

```
$ scp Project4.txt user1@192.168.0.104:
user1@192.168.0.104 password:
Project4.txt    100%   29KB 0.5MB/s   00:00
$
```

注意完成此任务没有使用`scp`选项。`-v`选项提供了在这种情况下不需要的信息。`scp`实用程序将在不询问的情况下覆盖远程上具有相同名称的文件。使用`scp`拷贝文件时需要小心，以免覆盖现有文件。

使用`scp`从一个远程机器拷贝到另一个的方便方法。示例如列表 12.18 所示。

# 列表 12.18：使用 `scp` 从远程系统安全拷贝文件
