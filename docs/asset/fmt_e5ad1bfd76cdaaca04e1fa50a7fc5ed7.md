
```
a ./Bshell/Domain, 14 bytes, 1 tape blocks
a ./Bshell/IP, 18 bytes, 1 tape blocks
a ./Bshell/dns_demo1, 227 bytes, 1 tape blocks
...
a ./Bshell/fs.csh, 1531 bytes, 3 tape blocks
a ./Bshell/dir1, 0 bytes, 0 tape blocks
a ./Bshell/copy, 2222 bytes, 5 tape blocks
x ./, 0 bytes, 0 tape blocks
x ./Bshell/Domain, 14 bytes, 1 tape blocks
x ./Bshell/IP, 18 bytes, 1 tape blocks
x ./Bshell/dns_demo1, 227 bytes, 1 tape blocks
...
x ./Bshell/fs.csh, 1531 bytes, 3 tape blocks
x ./Bshell/dir1, 0 bytes, 0 tape blocks
x ./Bshell/copy, 2222 bytes, 5 tape blocks
$
```

使用此命令行有以下优点：`cd` 和 `tar` 命令在所有 UNIX 系统上都可用，并且复制的文件具有源文件的访问权限和文件修改时间。

你也可以使用 `tar` 命令将目录复制到网络上的远程机器。在以下命令行中，`~/unixbook/examples` 目录被复制到名为 `ups un21` 的远程机器上的 `~/unixbook/examples.bak` 目录。`rsh` 命令（参见第 11 章）用于在 `ups un21` 上执行引用的命令组。由于 `tar` 命令未以详细模式运行，因此它静默运行，你不会在显示屏上看到任何输出。

```
$ (cd ~/unixbook/examples; tar cf - .) | rsh ups un21 "cd ~/unixbook/examples.bak; tar xf -"

$
```

## 23.6.2.5 `tar` 格式的软件分发和 `gtar`

公司经常使用 `tar` 命令来分发其软件，因为它会生成一个单一文件，客户只需复制该文件，并且与可能包含待分发软件的未归档目录层次结构相比，它可以节省磁盘空间。此外，大多数公司将其分发包（以 `tar` 格式）保存在其 Internet 站点上，客户可通过 `ftp` 命令下载它们。因此，`tar` 格式还减少了“复制”时间并减轻了客户的工作量，客户只需使用一个 `get`（或 `mget`）命令（`ftp` 命令），而如果需要下载目录层次结构，则需要使用多个命令序列。

由于软件包的大小很大，主要是由于其图形界面和多媒体格式，归档文件在放置到 `ftp` 站点之前会被压缩。软件用户需要在恢复之前先解压缩下载的文件。

现在考虑一个我们从 `ftp` 站点下载的文件 `tcsh-6.06.tar.Z`。为了恢复此文件，我们必须先解压缩再解包，如以下命令序列所示。

```
$ uncompress tcsh-6.06.tar.Z
$ tar xvf tcsh-6.06.tar
... [Output truncated]
$
```

如果一个软件包是通过二级存储介质（USB 闪存盘、DVD 或 CD-ROM）分发的，你需要将适当的文件复制到适当的目录并重复这些命令。

如果你想分发存储在目录层次结构中的某些软件，你首先需要使用 `tar` 命令为其制作一个归档，然后使用 `compress` 命令（或某些其他类似工具）对其进行压缩。这些步骤会创建一个压缩文件中的 `tar` 归档，可以将其放置在 `ftp` 仓库或网页上，或作为电子邮件附件发送。

磁盘文件备份是创建归档和备份最现代且最具成本效益的方式。

GNU 版本的 `tar`，`gtar` 的 `-z` 选项可用于生成 `tar` 归档的压缩版本。此选项也可用于恢复 `tar` 归档的压缩版本。使用此选项可消除使用 `gzip`（或 `gunzip`）实用程序压缩或解压缩归档然后再使用 `tar` 命令的过程；这一步骤过程可以仅由 `tar` 命令完成。在以下会话中，第一个 `tar` 命令在 `~/unixbook/backups/ub.tar.gz` 文件中生成当前目录的压缩 `tar` 归档，而第二个 `tar` 命令从同一文件恢复压缩 `tar` 归档到当前目录。

```
$ gtar -zcf ~/unixbook/backups/ub.tar.gz .
$ gtar -zxvf ~/unixbook/backups/ub.tar.gz
... [Output truncated]
$
```

## 23.6.3 其他 UNIX 归档和备份设施

除了传统的 `tar` 设施外，系统管理员还可以使用几种其他设施和方法来归档和备份单个用户账户、文件、文件系统以及整个系统本身。如前所述，要获得有关命令行设施的功能和选项的更完整列表，请查阅系统上这些命令的手册页。我们将简要描述并给出其中一些更现代和有用的设施和方法的简单示例。此外，我们还在第 24 章中提供了一种在 `ZFS` 中进行归档和备份的非传统方法。

### 23.6.3.1 `cpio`

`cpio` 在 UNIX 系统上与 `tar` 一样通用，它允许系统管理员备份整个系统并在文件系统之间传输文件。它可以与 `find` 命令结合使用，但如果备份整个文件系统则不一定需要。其通用格式为 `cpio -o [Abcv]` 用于创建归档，以及 `cpio -i [Btv] [pattern]` 用于恢复归档。

例如，以下命令将 `/home` 目录备份到通用名为 `device` 的 USB 闪存盘：

```
$ cd /home
$ touch level.1.cpio.timestamp
$ find . -newer level.0.cpio.timestamp -print \ | cpio -oacvB > device
...
$
```

### 23.6.3.2 `rsync`

如第 16 章中介绍的，`rsync` 命令是一种非常节省空间的备份文件和目录的方法，特别是使用 `ssh` 通过网络从一台机器备份到另一台机器。其操作也可以通过在 `crontab` 文件中设计和实现适当的条目来自动化。`rsync` 用于本地或远程复制的通用语法是

本地：

```
rsync [option(s)]... src... [dest]
```

远程：

Pull（复制到远程位置）：

```
rsync [option(s)]... [user@]host:src... [dest]
```

Push（从远程位置复制）：

```
rsync [option(s)]... src... [user@]host:dest
```

其中 `option(s)` 是 `rsync` 命令的有效选项，`src` 是源文件或目录，`dest` 是目标路径。

使用 `rsync` 将当前工作目录中的名为 `rsynctest` 的文件复制到本地目标 `/usr/home/bob/USBint` 的示例是

```
$ rsync -av rsynctest /usr/home/bob/USBint
sending incremental file list
rsynctest
sent 192 bytes received 35 bytes 454.00 bytes/sec
total size is 92 speedup is 0.41
$
```

使用 `rsync` 本地复制整个名为 `syncdir` 的目录的示例是

```
$ rsync -av syncdir /usr/home/bob/USBint
sending incremental file list
syncdir/
syncdir/Chap16.doc
syncdir/backup1.py
syncdir/ossystem.py
sent 280,176 bytes received 77 bytes 186,835.33 bytes/sec
total size is 279,855 speedup is 1.00
0
$
```

An example of copying an entire directory in push mode remotely is:

```
$ rsync -av -e ssh syncdir2 bob@192.168.0.7:/Users/b/unix3e
Password:
building file list ... done
syncdir2/
syncdir2/Chap16.doc
syncdir2/backup1.py
syncdir2/ossystem.py
sent 280,171 bytes received 96 bytes 16,985.88 bytes/sec
total size is 279,855 speedup is 1.00
0
$
```
