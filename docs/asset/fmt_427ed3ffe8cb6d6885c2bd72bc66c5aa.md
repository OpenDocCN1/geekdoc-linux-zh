
# 16 – 网络

除了在远程系统上开启 `shell` 会话外，`ssh` 还允许我们在远程系统上执行单个命令。例如，在名为 `remote-sys` 的远程主机上执行 `free` 命令，并将结果显示在本地系统上：

```
[me@linuxbox ~]$ ssh remote-sys free
me@twin4$ password:
total       used free shared buffers cached

Mem:       775516 507184 268352 0 110066 154596

-/ buffers/cache: 242520 533016
Swap:         1572856 0 1572856
[me@linuxbox ~]
```

可以使用更有趣的方法来使用这种技术，例如这个示例，我们在远程系统上执行 `ls` 并将输出重定向到本地系统的一个文件中：

```
[me@linuxbox ~]$ ssh remote-sys 'ls *' > dirlist.txt
me@twin4s password:
me@linuxbox ~]$
```

注意上面命令中使用了单引号。这样做是因为我们不希望在本地机器上执行路径扩展；相反，我们希望它在远程系统上执行。同样，如果我们将输出重定向到远程机器上的文件，我们可以在单引号内放置重定向操作符和文件名：

```
me@linuxbox ~]$ ssh remote-sys 'ls * > dirlist.txt'
```

## 使用 SSH 建立隧道

当通过 SSH 与远程主机建立连接时，发生的一部分情况是本地和远程系统之间创建了一个加密隧道。通常，此隧道用于允许在本地系统上输入的命令被安全地传输到远程系统，并将结果安全地传回。除了这项基本功能外，SSH 协议允许将大多数网络流量通过加密隧道发送，从而在本地和远程系统之间创建某种 VPN（虚拟私有网络）。

该功能最常见的用途可能是允许传输 X Window 系统流量。在运行 X Window 的系统上（即显示 GUI 的机器），可以在远程系统上启动并运行 X 客户端（图形化应用程序），并让其显示内容呈现在本地系统上。这很容易做到；这里有一个示例：假设我们坐在一个名为 `linuxbox` 的 Linux 系统前，连接到一个名为 `remote-sys` 的远程系统，并在本地系统上看到图形化输出。

```
me@linuxbox ~]$ ssh -X remote-sys
me@remote-sys's password:
Last login: Mon Sep 08 13:23:21 2008
me@remote-sys ~]$ xload
```

在远程系统上执行 `xload` 命令后，它的窗口会出现在本地系统上。在某些系统上，你可能需要使用 `-Y` 选项而不是 `-X` 选项来实现。

## 与远程主机进行安全通信

### `scp` 和 `sftp`

OpenSSH 软件包还包含两个可以使用 SSH 加密隧道跨网络复制文件的程序。第一个程序 `scp`（安全复制）非常像熟悉的 `cp` 程序来复制文件。最显著的区别是，源或目标路径之前可能有一个远程主机的名称，后跟一个冒号。例如，如果你想从远程系统 `remote-sys` 的家目录复制名为 `document.txt` 的文档到我们本地系统的当前工作目录，我们将这样做：

```
[me@linuxbox ~]$ scp remote-sys:document.txt
me@remote-sys's password:
document.txt         100% 5581    5.5KB/s 00:00
[me@linuxbox ~]
```

使用 `ssh` 时，如果远程主机账户与本地账户不匹配，你可以在远程主机名前使用用户名：

```
[me@linuxbox ~]$ scp bob@remote-sys:document.txt
```

第二个 SSH 文件复制程序 `sftp`，如其名所示，是 `ftp` 程序的安全替代品。`sftp` 的工作方式与原始 `ftp` 非常相似；然而，它不是使用明文传输，而是使用加密隧道。`sftp` 相比 `ftp` 有一个重要优势：它不需要运行一个服务器。这是一个示例：

```
me@linuxbox ~]$ sftp remote-sys
Connecting to remote-sys...
me@remote-sys's password:
sftp@remote-sys> ls
sftp@remote-sys> cd /
sftp@remote-sys> get document.txt
sftp@remote-sys> quit
```

# 17 – 查找文件

当我们漫游 Linux 系统时，有一点变得清晰：典型的 Linux 系统有很多文件！这引出了一个问题：“我们如何找到它们？”我们已经知道 Linux 文件系统根据从上一代 Unix 类系统继承来的规范进行了良好的组织，但文件的巨大数量可能会带来令人敬畏的问题。

在本章中，我们将查看两个在系统中查找文件的工具。这些工具是：

- `locate` – 按名称查找文件
- `find` – 在目录中搜索文件

此外，我们还将查看一个与文件搜索命令配合使用以处理生成的文件列表的命令：

- `xargs` – 从标准输入构建并执行命令行
- `touch` – 修改文件时间
- `stat` – 显示文件或文件系统状态

## `locate` – 简单的查找方法

`locate` 程序对路径执行快速数据库搜索，然后输出匹配给定子字符串的名称。例如，假设我们要找到所有以 `zip` 开头的程序。由于我们正在寻找程序，我们可以假设包含程序的目录名称将以 `bin` 结尾。因此，我们可以尝试这样使用 `locate` 来查找我们的文件：

```
[me@linuxbox ~]$ locate bin/zip
```

`locate` 将搜索其数据库并输出包含该字符串的所有 `bin/zip`：

```
/usr/bin/zip
/usr/bin/zipcloak
/usr/bin/zipgrep
/usr/bin/zipinfo
/usr/bin/zipnote
/usr/bin/zipsplit
```

如果搜索需求并不简单，可以将 `locate` 与 `grep` 等其他工具结合，设计更有趣的搜索：

```
me@linuxbox ~$ locate zip | grep bin
/bin/bunzip2
/bzip2
/bin/bzip2recover
/bin/gunzip
/bin/gzip
/usr/bin/funzip
/usr/bin/gpg-zip
/usr/bin/preunzip
/usr/bin/prezip
/usr/bin/prezip-bin
/usr/bin/unzip
/usr/bin/unzipsfx
/usr/bin/zip
/usr/bin/zipcloak
/usr/bin/zipgrep
/usr/bin/zipinfo
/usr/bin/zipnote
/usr/bin/zipsplit
```

`locate` 程序已经存在多年了，常用的有几种不同的变体。在现代 Linux 发行版中，常见的两种版本包括 `slocate` 和 `mlocate`，它们通常通过名为 `locate` 的符号链接进行访问。不同版本的 `locate` 具有重叠的选项。某些版本包含了正则表达式匹配（我们将在后面的章节中介绍）和对通配符的支持。检查 `locate` 的 `man` 手册页以确定安装了哪个版本的 `locate`。

### `locate` 数据库从哪里来？

你可能会注意到，在某些发行版中，`locate` 在系统安装后立即无法工作，但如果你第二天重试，它就能用了。这是怎么回事？`locate` 数据库是由另一个名为 `updatedb` 的程序创建的。通常，它作为 `cron` 任务定期运行；即由 `cron` 守护进程按间隔执行的任务。大多数配备了 `locate` 的系统每天运行一次 `updatedb`。由于数据库不是持续更新的，你会发现使用 `locate` 时，最近的文件不会显示。为了解决这个问题，可以通过成为超级用户并在提示符处手动运行 `updatedb` 程序。

## `find` – 费力查找文件

虽然 `locate` 程序可以仅根据文件名找到文件，但 `find` 程序会根据各种属性在目录（及其子目录）中搜索文件。我们将花费大量时间在 `find` 身上，因为它有很多有趣的功能，当我们开始在后面的章节介绍编程概念时，会反复看到这些功能。

在最简单的用法中，给 `find` 传入一个或多个要搜索的目录名称。例如，列出我们主目录的列表：

```
me@linuxbox ~$ find ~
```

在大多数活跃的用户账户上，这将产生一个巨大的列表。由于列表被发送到标准输出，我们可以将列表管道到其他程序。让我们使用 `wc` 来统计文件数量：

```
me@linuxbox ~$ find ~ | wc -l
47068
```
