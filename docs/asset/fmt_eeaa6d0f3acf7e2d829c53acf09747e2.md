
`matthew@seymour:-$ sudo echo 1 >/proc/sys/net/ipv4/tcp_sync_cookies`

使用 `/proc` 目录的其他方法包括：

- 从 `/proc/cpuinfo` 获取 CPU 信息，如系列、类型和速度。
- 在 `/proc/net/dev` 下查看重要的网络信息，如 `/proc/net/dev` 下的活动接口、`/proc/net/route` 中的路由信息以及 `/proc/net/netstat` 中的网络统计数据。
- 获取文件系统信息。
- 通过 USB 报告媒体挂载点信息；例如，如果系统中检测到 USB 摄像头或硬盘，Linux 内核会报告应使用哪个设备来访问文件（如 `/dev/sda`）。你可以使用 `dmesg` 命令查看此信息。
- 在 `/proc/version` 获取内核版本，在 `/proc/uptime` 获取性能信息（如运行时间），或在 `/proc/stat` 获取 CPU 负载、交换文件使用和进程等统计数据。

## 在 /usr 目录中处理共享数据

`/usr` 目录包含软件应用程序、库和其他供系统上任何人使用的其他类型的共享数据。许多 Linux 系统管理员为 `/usr` 单独分区。`/usr` 下的许多子目录包含手册页（`/usr/share/man`）、软件共享文件（`/usr/share/name_of_package`，例如 `/usr/share/emacs`）、额外的应用程序或软件包文档（`/usr/share/doc`）以及整个本地构建和安装的软件树 `/usr/local`。

## /tmp 目录中的临时文件存储

顾如其名，`/tmp` 目录用于临时文件存储；在使用 Linux 时，各种程序会在此目录中创建文件。

## 访问 /var 目录中的变量文件

`/var` 目录包含各种系统服务用于缓冲（spooling）和记录的子目录。这些变量数据文件（如打印缓冲队列）许多是临时的，而其他文件（如系统和内核日志）在使用过程中会重命名和轮换。入站电子邮件被投递到 `/var/spool/mail` 下的文件中。

Linux 还将 `/var` 用于其他重要的系统服务。这些包括 `/var/ftp` 下的最顶级文件传输协议（FTP）目录（参见第 25 章“使用 FTP 进行远程文件服务”）以及系统的 Apache 服务器初始主页目录 `/var/www/html`。有关使用 Apache 的更多信息，请参见第 23 章“Apache Web 服务器管理”。

## 注意

最近有一种趋势是将从 `/var/www` 和 `/var/ftp` 提供的数据移动到 `/srv`，但这并非普遍现象。

## 导航 Linux 文件系统

在 Linux 文件系统中，与其前身 UNIX 一样，一切都是文件：数据文件、二进制文件、可执行程序，甚至是输入和输出设备。这些文件被放置在系列类似于文件夹的目录中。目录无非一个包含其他文件/目录列表的特殊类型文件。这些文件和目录用于创建一个层次结构，实现特定类型文件的逻辑放置。在本章后面的部分，我们将讨论 Linux 文件系统的标准分层结构。首先，我们学习如何导航并与文件系统交互。

## 注意

包含内容的目录称为父目录，其内容称为子目录，例如“home/matthew/Documents 是 /home/matthew 的子目录，它是它的父目录”。

## 使用 ls 列出目录内容

`ls` 命令列出当前目录的内容。它通常单独使用，但 `ls` 提供了许多选项（也称为开关/switches），可以为你提供更多信息。如果你如之前描述的那样刚刚登录，此命令将列出你用户主目录下的文件和目录：

```
matthew@seymour:-$ ls -a

Documents        file.txt  Pictures  Music

.               bash_logout  Documents  Music

.               bashrc       local

.bash_history  config      profile
```

## 注意

本章中的所有目录列表为了节省空间都进行了缩写。

单独使用时，`ls` 命令只给出名称列表。有些是文件，有些是目录。如果我知道我在找什么但不记得确切的名称，这很有用。然而，在这种情况下使用 `ls` 有一些局限性。首先，它不显示隐藏文件。隐藏文件名以点（`.`）作为第一个字符。它们通常用于特定程序的配置，且不经常访问。由于由于原因，它们不包含在基础列表中。你可以通过在命令中添加此类开关来查看所有隐藏文件：

```
matthew@seymour:-$ ls -a
```

# 第 10 章 命令行启动

目录中的每个项目都有更多可用信息。要包含详细信息，如文件/目录权限、所有者和组（这些将在本章稍后讨论），以及大小、最后修改日期和时间，请输入以下：

```
matthew@seymour:~$ ls -al

total 608

drwxr-xr-x 3 root 4096 2011-06-04 08

drwxr-xr-x 3 root 4096 2011-05-15 16

--rw-r--r-- 1 matthew 421 2011-06-04 27 .bash_history

--rw-r--r-- 1 matthew 220 2011-06-04 27 .bash_logout
```
