

/dev/zero 来自此文件的内容包含无限长度的零字符串（数值零零，而非 ASCII 零）。你可以使用类似这样的命令来填充文件（例如交换文件，第 498 页）或用零覆盖文件：

```
$ dd if=/dev/zero of=zeros bs=1024 count=10
10+0 records in
10+0 records out
10240 bytes (10 KB) copied, 0.000160263 seconds, 63.9 MB/s
```

```
$ od -c zeros
0000000 \0 \0 \0 \0 \0 \0 \0 \0 \0 \0\n* 0024000
```

od 工具显示了新文件的内容。

当你尝试对 /dev/zero 执行你对 /dev/null 执行所能做的事情时，你会填满你当前正在工作的分区：

```
$ cp /dev/zero bigzero
cp: 'bigzero': No space left on device
$ rm bigzero
```

/etc/aliases 邮件传递系统使用，用于存储用户的别名。编辑此文件以设置本地需求。更多信息，请参阅第 722 页的 /etc/aliases。

/alternatives 存储符号链接，你可以通过不同于工具所在文件的名称来调用工具。例如，当你输入 bdownloadcurses 命令时，shell 会通过以下链接运行 bdownloadcurses.bittorrent：

```
$ ls -1 /usr/bin/bdownloadcurses -> /etc/alternatives/bdownloadcurses
$ ls -1 /etc/alternatives/bdownloadcurses -> /etc/alternatives/bdownloadcurses.bittorrent
```

alternatives 目录还允许工具出现在多个目录中：

```
$ ls -1 /usr/X11/bin/bdownloadcurses /usr/bin/X11/bdownloadcurses
/usr/X11/bin/bdownloadcurses -> /etc/alternatives/bdownloadcurses.bittorrent
/usr/bin/X11/bdownloadcurses -> /etc/alternatives/bdownloadcurses
```

此外，alternatives 目录允许你通过多个名称调用同一个工具。虽然 alternatives 并没有让开发者能够任何在没有它时无法实现的操作，但它提供了一种保留和更新这些链接的方法。第 179 页可以找到指向某个工具的所有链接。

/etc/at.allow 默认情况下，用户可以使用 at 和 crontab 工具。at.allow 和 cron.allow /etc/at.deny 分别列出了允许使用 at 和 crontab 的用户。at.deny /etc/cron.allow 和 cron.deny 文件则列出了不允许使用 cron 的用户。按照 Ubuntu Linux 的配置方式，at.deny 文件包含某些系统账户列表，且没有 at.allow，这允许非管理员用户使用 at。cron.allow 和 cron.deny 文件的缺失允许任何人使用 crontab。要防止除以 root 权限运行的用户外的任何人都使用 at，请删除 at.allow 和 at.deny 文件。要防止除以 root 权限运行的用户外的任何人都使用 crontab，请创建一个仅包含单条目 root 的 cron.allow 文件。关于 crontab 的更多信息，请参阅第 605 页的“任务调度”。

## 第 12 章 文件、目录和文件系统

/etc/bashrc 包含全局交互式、登录非 shell 初始化脚本。默认的 Ubuntu /etc/profile（第 495 页）文件执行此文件中的命令。用户可以在 ~/.bashrc（第 488 页）覆盖此文件中的设置。

/etc/default 存储系统服务和工具（如 NFS 和 useradd）的默认值。查看此目录下的文件以获取更多信息。

/etc/dumpdates 包含有关上次备份的信息。对于每个文件系统，它存储执行的时间。备份软件使用这些信息来确定备份哪些文件。请参阅第 599 页的“备份”。以下是带有四个文件系统的 dumpdates 示例：

| hda1 | Apr 22 03:55 2010 |
| hda8 | Sun 18 25:24 2010 |
| hda9 | Sun 18 57:32 2010 |
| hda10 | Sun 18 58:06 2010 |
| hda11 | Sun 18 02:27 2010 |
| hdb8 | Mar 21 03:35 2010 |
| hdb9 | Mar 21 33:40 2010 |
| hdb10 | Mar 21 43:45 2010 |

第一列包含文件系统的名称。第二列包含备份日期和时间。

/etc/event.d 存放定义 Upstart 任务的文件。参阅第 434 页获取更多信息。

/etc/fstab 文件系统表——包含系统管理员指定的所有可挂载设备列表。程序不写入此文件；仅从文件中读取。参阅第 510 页获取更多信息。

/etc/group 允许用户共享组。etc/group 中的每个条目有四个字段：组名:密码:组ID:登录列表。组名是组的。密码是可选的。组ID 是数字。登录列表是逗号分隔的用户列表。如果一个条目过长无法在一行显示，在行末尾加上反斜杠 (\)，并在下一行继续该条目。当……。参阅第 221 页的“ACL：访问控制列表”以进行更细粒度的控制。

当你创建一个新文件时，Linux 会将其分配给目录所在的组，前提是你属于该组。如果你不属于访问该文件的组，将受到该文件的公共权限限制。

当你尝试访问一个你不拥有的文件时，Linux 会检查你是否是访问该文件的组的成员。如果你不是访问该文件的组成员，将受到该文件的公共权限限制。

/etc/hostname 存储系统的主机名。更改此文件的内容将在下次启动时更改系统主机名。使用 hostname 命令立即更改。如果不更改 /etc/hostname，主机名将在下次启动时恢复。

/etc/initab 初始化表——某些发行版使用此文件来控制进程的行为。它在 Ubuntu 系统上不存在。更多信息请参阅第 439 页的“rc-sysinit 任务和 initab”。

