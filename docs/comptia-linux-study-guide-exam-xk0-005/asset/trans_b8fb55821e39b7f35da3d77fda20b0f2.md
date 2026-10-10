
- 有几个文件维护设置可以控制日志允许使用的空间量，以及基于时间或文件大小拆分为存档日志文件的频率。

- ForwardToSyslog 设置决定 systemd-journald 是否应将接收到的消息转发给系统中运行的独立 syslog 程序（例如 rsyslogd）。这提供了两层日志记录功能。

有一些设置允许你自定义 systemd-journald 在你的系统中的工作方式。要查看所有设置的完整列表和解释，请在命令提示符下输入 `man journal.conf`。

## 查看日志

systemd-journald 程序并不将日志条目存储在文本文件中。相反，它使用自己的二进制文件格式，其工作原理类似于数据库。虽然这使得查看日志条目稍微困难一些，但确实为快速搜索特定事件条目提供了便利。

journalctl 程序是我们访问日志文件的界面。journalctl 命令的基本格式如下：

```
journalctl [options] [matches]
```

选项控制返回的数据，而匹配条件则决定显示的内容。表 17.3 列出了可用的选项。

### 表 17.3 journalctl 命令选项

| 选项 | 描述 |
| :--- | :--- |
| -a | 显示所有数据字段 |
| -e | 跳转到底部的日志并使用分页工具显示条目 |
| -l | 显示所有可打印的数据字段 |
| -n 数字 | 显示最近指定数量的日志条目 |
| -r | 反转输出中日志条目的顺序 |

匹配参数定义要显示哪种类型的日志条目。表 17.4 列出了可用的匹配项。

### 表 17.4 journalctl 匹配参数

| 匹配项 | 描述 |
| :--- | :--- |
| *字段* | 匹配日志中的特定字段 |
| *内核* | 仅显示内核日志条目 |
| *优先级=值* | 仅匹配具有指定优先级的条目 |
| *_UID=用户ID* | 仅匹配由指定用户 ID 创建的条目 |
| *_主机名=主机* | 仅匹配来自指定主机的条目 |
| *_传输=传输方式* | 仅匹配通过指定传输方式接收的条目 |
| *_UDEV_SYSNAME=设备* | 仅匹配来自指定设备的条目 |
| *对象_PID=进程ID* | 仅匹配由指定应用程序进程 ID 创建的条目 |

当您在日志中寻找特定事件条目时，`journalctl` 命令非常实用；它允许您使用匹配条件过滤事件，并使用选项决定如何显示它们，如清单 17.3 所示。

### 清单 17.3：journalctl 命令的输出

```
[rich@localhost ~]$ journalctl -r _TRANSPORT=kernel
-- 日志始于 Fri 2019-02-08 12:47:04 EST, 终于...
Feb 08 12:48:36 localhost.localdomain kernel: TCP: lp registered
Feb 08 12:48:17 localhost.localdomain kernel: fuse init (API version 7.22)
Feb 08 12:47:43 localhost.localdomain kernel: virbr0: port 1(virbr0-nic)
Feb 08 12:47:43 localhost.localdomain kernel: IPv6: ADDRCONF(NETDEV_UP):
Feb 08 12:47:43 localhost.localdomain kernel: virbr0: port 1(virbr0-nic)
Feb 08 12:47:35 localhost.localdomain kernel: e1000: enp0s8 NIC Link is Up
Feb 08 12:47:32 localhost.localdomain kernel: IPv6: ADDRCONF(NETDEV_CHANGE)
Feb 08 12:47:32 localhost.localdomain kernel: ip_set: protocol 6
Feb 08 12:47:32 localhost.localdomain kernel: IPv6: ADDRCONF(NETDEV_UP)
...
```

这使得浏览日志文件变得容易多了！练习 17.1 将引导你实时监控系统日志，并观察当你向 Linux 系统的日志设施发送消息时的情况。

## 练习 17.1 创建日志或日志条目

本练习演示如何创建日志或日志条目，并在 rsyslog 日志和 systemd-journald 日志中查看该条目。

1. 登录到 Linux 图形桌面，并打开两个新的命令提示符窗口。如果你使用的是虚拟终端，请打开两个独立的虚拟终端会话。
2. 在一个命令提示符窗口或虚拟终端会话中开始监控标准日志文件。在 Ubuntu 系统上，使用 `sudo tail -f /var/log/syslog`。对于基于 Red Hat 的系统（如 Fedora、Rocky 和 CentOS），使用 `sudo tail -f /var/log/messages`。
3. 在第二个命令提示符窗口或虚拟终端会话中，使用命令 `logger "This is a test log entry."` 创建日志事件。
4. 观察第一个窗口或虚拟终端会话中的输出。你应该能看到新的日志条目出现在适合你系统的日志文件末尾。
5. 使用命令 `journalctl -r` 显示日志的末尾。你应该能看到你的日志事件消息也出现在日志中。Debian 和基于 Red Hat 的系统都使用 systemd-journald，但也会将事件消息转发给 rsyslogd 应用程序，因此你通常可以在两个系统中看到事件。

## 摘要

记录发生在你的 Linux 系统或应用程序上的事件对于能够排除故障至关重要。Linux 系统已采用 syslog 协议方法来处理事件消息。syslog 协议定义了一种事件类型，称为设施（facility），以及事件严重级别。这有助于你确定哪些事件需要采取行动，哪些只是信息性的。

rsyslogd 日志应用程序利用 syslog 协议来记录系统和应用程序事件。`/etc/rsyslog.conf` 配置文件控制记录哪些事件以及如何记录。rsyslogd 应用程序可以将事件记录到文件、应用程序、远程主机、终端，甚至直接记录给用户。

Linux systemd 服务包还包括一种称为日志记录（journaling）的自身事件记录方法。systemd-journald 应用程序监控系统中的所有事件和应用程序，并将它们发送到特殊的日志文件。systemd-journald 的操作由 `/etc/systemd/journald.conf` 配置文件控制。你必须使用 journalctl 应用程序来读取存储在日志文件中的事件。

## 考试要点

- **描述大多数 Linux 日志应用程序使用的日志协议。** syslog 协议已成为大多数 Linux 日志应用程序的事实标准。它使用设施代码（定义事件类型）和严重级别（定义事件消息的重要性）来识别事件。sysklogd、syslog-ng 和 rsyslogd 应用程序都使用 syslog 协议来管理 Linux 中的系统和应用程序事件。

- **描述 rsyslogd 应用程序如何将事件引导至特定位置。** rsyslogd 应用程序使用 `/etc/rsyslog.conf` 配置文件来定义处理事件的规则。每条规则都指定了一个 syslog 设施和严重级别，以及要采取的操作。符合设施条件且优先级等于或高于所定义严重级别的事件将被发送到指定的操作。操作可以是将事件消息发送到日志文件、将消息管道传输到应用程序，或将事件消息发送到远程主机或系统中的用户。

- **解释 Systemd 服务如何使用不同的方法记录事件。** Systemd 服务包使用 systemd-journald 应用程序，它不使用 syslog 协议记录事件。相反，systemd-journald 创建自己的二进制日志文件来存储事件消息。二进制日志文件经过索引，以提供更快的搜索速度。journalctl 应用程序提供了向日志文件发送搜索查询并显示搜索结果的接口。

## 复习题

1. 哪种协议在 Linux 中追踪系统事件消息时成为事实标准？
   A. SMTP
   B. FTP
   C. NTP
   D. syslog
   E. journalctl

2. Nancy 想要编写一条 rsyslogd 规则，将来自系统作业调度器的事件消息分离到一个单独的日志文件中。她应该使用哪个 syslog 设施关键字？
   A. cron
   B. user
   C. kern
   D. console
   E. local0

3. 在 rsyslogd 中，哪个 syslog 严重级别具有最高的优先级排名？
   A. crit
   B. alert
   C. emerg
   D. notice
   E. err

4. 哪个 syslog 严重级别代表正常但重要的状况消息？
   A. crit
   B. notice
   C. info
   D. alert
   E. local0

5. 哪个 syslog 应用程序以火箭般的速度著称？
   A. syslogd
   B. syslog-ng
   C. systemd-journald
   D. klogd
   E. rsyslogd

