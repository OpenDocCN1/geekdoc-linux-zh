
获取基准的间隔会因组织而异。例如，频繁地获取基准是一个好主意，例如每周。相反，工作站可以处理更长的间隔。

一旦收集了数据，使用文字处理器或电子表格应用程序（如 `OpenOffice.org`）将前面的步骤中收集的信息汇成系统基准文档。

# 配置日志文件

如上一章所学，你的系统日志存储在 `/var/log` 目录中，如图 16-5 所示。

注意图 16-5，`/var/log` 中有许多子目录，例如 `apache2`、`apparmor`、`audit` 和 `cups`，用于存储守护进程（daemons）的日志文件。正如我们在上一章中学到的，其中某些日志是简单的文本文件，可以使用文本处理工具进行读取。另一些则是二进制文件，需要使用特殊的实用程序（如 `lastlog`）。如你在图 16-5 中所示，`/var/log` 及其子目录中有大量文件。尽管如此，某些日志远比其他日志要有用得多。图 16-8 包含了一些重要日志文件的列表。

这些是 `SUSE Linux` 系统使用的日志文件。其他发行版（如 `Fedora`）可能默认使用不同的文件。你可以使用接下来讨论的 `syslog.conf` 文件自定义你的日志记录。

![](img/8156850acb7240fabbc4667ef20f2fa8_1018_0.png)

**图 16-5**

**表 16-5 /var/log 目录的内容**

```
linux1:/var/log $ ls -l
-rw-r---- 1 root 38963 Apr 24 07:33 Sax.log
-rw-rw- 1 root 10 Oct 10 12:34 Free86.log -> Xorg.log
-rw-rw- 1 root 26865 Feb 23 12:08:16 Free86.0.log -> Xorg.0.log
-rw-rw- 1 root 26865 Feb 23 12:11:37 Xorg.0.log
drwxr-xr-x 2 root 800 Feb 21 12:13:52 atime
-rw-r---- 1 root 21288 Feb 22 12:12:01 cron
drwxr-xr-x 5 root 144 Feb 9 12:13:45 apache2
-rw-r---- 1 root 80 Feb 22 12:14:06 auditd
drwxr-xr-x 3 root 0 Oct 10 12:30:10 boot
-rw-r---- 1 root 34868 Feb 23 12:21:07 boot.msg
-rw-r---- 1 root 400525 Feb 23 12:02:16 boot.old
drwxr-xr-x 2 root 136 Feb 16 12:17:52 core
-rw-r---- 1 root 24168 Feb 9 12:34:24 faillog
drwxr-xr-x 1 root 167161 Feb 23 12:14:41 firewall
-rw-r---- 1 root 152177 Feb 23 12:16:08 km.log
drwxr-xr-x 2 root 48 May 2 2006 knrb
-rw-xr-x 1 root 294044 Feb 23 12:14:01 lastlog
-rw-r---- 1 root 126 Feb 2 12:13:51 localmessages
-rw-r---- 1 root 28948 Oct 16 10:14:18 mail
-rw-r---- 1 root 26172 Oct 16 10:14:18 mail.info
-rw-r---- 1 root 1454724 Feb 23 14:41:45 messages
lrwxrwxrxr 1 root root 23 23 Feb 9 12:35:99 syslog.log -> ../lib/mysql/mysql
```

**表 16-8 日志文件描述**

| 有用日志文件 | 描述 |
| --- | --- |
| `boot.log` | 包含守护进程启动时的日志条目。 |
| `boot.msg` | 包含系统启动期间屏幕上显示的所有消息。在尝试修复启动问题时，这是一个非常有用的故障排除工具。屏幕上显示的消息通常运行得太快无法阅读。 |
| `faillog` | 包含失败的身份验证尝试。 |
| `firewall` | 包含防火墙日志记录。 |
| `lastlog` | 包含用户的最后登录信息。 |
| `mail` | 包含 `postfix` 或 `sendmail` 守护进程生成的消息。 |
| `messages` | 包含大多数运行进程的消息。这可能是最有用的日志文件之一。你可以使用它来排查无法启动的服务、看似运行正常的服务等问题。 |
| `warn` | 包含警告消息。 |
| `wtmp` | 包含已登录系统的用户列表。 |
| `xinetd.log` | 包含 `xinetd` 守护进程的日志记录。 |

`Linux` 系统的日志记录由 `syslog` 守护进程处理。并不是每个守护进程都维护自己的独立日志文件，大多数 `Linux` 服务默认配置为将日志条目写入 `/dev/log`。该设备由 `syslog` 守护进程维护。当服务写入此套接字时，它会被 `syslog` 捕获。`syslog` 守护进程使用图 16-6 所示的 `/etc/syslog.conf` 文件中的条目来决定信息的去向。

> `Linux` 版本 10 及以后使用 `syslog-ng` 代替 `syslogd` 来管理日志记录。

`syslog.conf` 文件的语法为：

```
service.priority      file
```

`syslog` 守护进程使用以下优先级级别：

- `debug` 所有信息
- `info` 信息性消息

![](img/8156850acb7240fabbc4667ef20f2fa8_1019_0.png)

# 982 第 16 章：系统的文档记录与故障排除

**图 16-9：配置远程日志**

```
root@fedora:/etc
$ cat 192.168.1.15
# 将所有内核消息记录到控制台。
# 记录每条其他信息会刷屏。
/dev/console
# 记录 info 或更高级别的所有内容（邮件除外）。
# 不要记录身份验证消息！
.info:mail.none;authpriv.none;cron.none
/var/log/messages
# authpriv 有限制访问权限。
authpriv.*
/var/log/secure
# 将所有邮件消息记录在一个地方。
mail.*
-/var/log/maillog
# 记录 cron 相关内容
cron.*
/var/log/cron
# 每一项都会接收紧急消息
.emerg
*
# 将 crit 及更高级别的新错误保存到特殊文件中。
INSERT --
```

6. 要配置 `loghost` 系统以接收来自其他系统的日志消息，请执行以下操作：
    a. 在文本编辑器中，打开 `/etc/sysconfig/syslog`。
    b. 找到 `SYSLOGD_PARAMS` 指令。
    c. 将 `SYSLOGD_PARAMS` 指令的值设置为 `-r`。
    d. 保存更改并退出文件。
    e. 重启 `syslogd`。

在这些背景的基础上，让我们讨论如何实际查看和你的日志文件。

# 使用日志文件排除问题

正如我在本章开头提到的，在排除 `Linux` 问题时，你的日志文件是无价的资源。如果内核或服务遇到问题，它将被记录在日志文件中。查看这些日志文件可以为你提供丰富的信息，这些信息并不一定显示在屏幕上。正如我们在上一章讨论过的，某些日志文件是二进制文件，必须使用特殊程序进行读取。然而，你的大多数日志文件都是简单的文本文件，可以使用标准的文本处理工具进行查看。在本书前面的章节，

# 排除系统问题 983

**图 16-10：使用 `less` 查看日志文件**

```
user@linux -- 控制台... 
编辑  查看  设置  帮助
10月10日 19:49:32 linux syslog-ng[2979]: syslog-ng version 1.6.8 starting
inserting as_acci(/lib/modules/2.
10月10日 19:49:34 linux modprobe: FATAL: Error inserting as_acci(as_acci.ko): No such device
16.13-04-default-kernel/drivers/acpi/as_acci.ko): No such device(/lib/modules/2.6
16.13-04-default-kernel/drivers/acpi/as_acci.ko): No such device
10月10日 19:49:35 linux loading tushiba_acpi/2.
16.13-04-default-kernel/drivers/acpi/tushiba_acpi.ko): No such device
10月10日 19:49:36 linux ifconfig: lo is 127.0.0.1/8 host lo
10月10日 19:49:36 linux ifconfig: eth0 is UP (LOOPBACK, UP) mtu 1500 qadisc no
10月10日 19:49:36 linux ifconfig: link 00:00:00:00:00:00 br 00:00:00
10月10日 19:49:37 linux ifconfig: lo: inet 127.0.0.1/8 host lo
10月10日 19:49:37 linux ifroute: IP address: 127.0.0.1/8
10月10日 19:49:38 linux ifroute: Configured routes for interface lo:
128/ - -
10月10日 19:49:39 linux ifroute: Active routes for interface lo:
10月10日 19:49:39 linux ifroute: 127.0.0.1/8 scope link
10月10日 19:49:39 linux ifconfig: eth0: inet 192.168.1.10/24
10月10日 19:49:40 linux ifconfig: eth0: address: 192.168.1.10
10月10日 19:49:40 linux ifconfig: eth0: device: Advanced Micro Devices [PCI]
10月10日 19:49:40 linux ifconfig: eth0: configuration: eth-id
10月10日 19:49:41 linux ifconfig: eth0: IP address: 192.168.1.10
/var/log/messages [000005.log
```

你学习了如何使用 `cat`，让我们在 `Linux` 系统上查看文本文件。这些工具当然也可以用于查看文件。然而，这些工具存在一个问题：日志文件通常太长了，无法用它们来查看。例如，在图 16-10 中，在 shell 提示符下执行了 `/var/log/messages` 命令。注意屏幕底部显示的行。`/var/log/messages` 文件有 188,555 行！该工具一次显示 24 行。你将多次按下空格键才能到达文件末尾！有两种策略可以到达那里。我们在上一章中向你介绍了第一种：你可以重定向 `cat` 的输出来定位日志文件中的特定文本。此外，你可以使用 `head` 和 `tail` 工具按时间顺序查看日志记录（从旧到新）。如果你想查看日志文件的开头，可以在提示符输入文件名。

# 984 第 16 章：系统的文档记录与故障排除

**图 16-11：使用 `grep` 在日志文件中查找信息**

```
2月22日 12:00:31 linux.log[8324]: connect from 192.168.1.10 (192.168.1.10)
2月22日 12:00:31 linux.log[8324]: Connection from 192.168.1.10 on port
2月22日 12:00:31 linux.log[8325]: connect from 192.168.1.10 (192.168.1.10)
2月22日 12:00:31 linux.log[8326]: connect from 192.168.1.10
2月22日 12:00:31 linux.log[8327]: connect from 192.168.1.10 (192.168.1.10)
2月22日 12:00:31 linux.log[8328]: connect from 192.168.1.10
2月22日 12:00:31 linux.log[8329]: connect from 192.168.1.10 (192.168.1.10)
2月22日 12:00:31 linux.log[8330]: connect from 192.168.1.10 (192.168.1.10)
2月22日 12:00:31 linux.log[8331]: connect from 192.168.1.10
2月22日 12:00:31 linux.log[8332]: connect from 192.168.1.10 (192.168.1.10)
2月22日 12:00:31 linux.log[8333]: connect from 192.168.1.10 (192.168.1.10)
2月22日 11:37:48 linux.vxinetd[2979]: Reading included configuration file: /etc/inetd.log /file=/etc/xinetd.log[20]
10月10日 19:49:36 linux [3339]: Reading included configuration file: /etc/inetd.log /file=/etc/xinetd.log[20]
linux1:~ #
```

提示符显示文件的前几行。例如，在图 16-12 中，使用 `head` 显示了 `/var/log/messages` 文件的开头。`tail` 的工作与 `head` 相反。当你需要查看日志最后几行进行故障排除时，这非常有用。在提示符处使用 `tail` 即可。在图 16-13 中，正在使用 `tail` 查看 `/var/log/messages` 文件。

**图 16-12：使用 `head` 查看日志文件**

```
~$ /var/log/messages
10月10日 19:49:36 linux syslog-ng: version 1.6.8 starting
10月10日 19:49:34 linux modprobe: FATAL: Error inserting as_acci(as_acci.ko): No such device
16.13-04-default-kernel/drivers/acpi/as_acci.ko): No such device(/lib/modules/2.6
16.13-04-default-kernel/drivers/acpi/as_acci.ko): No such device
10月10日 19:49:35 linux loading tushiba_acpi/2.
16.13-04-default-kernel/drivers/acpi/tushiba_acpi.ko): No such device
10月10日 19:49:36 linux ifconfig: lo is 127.0.0.1/8 host lo
10月10日 19:49:36 linux ifconfig: eth0 is UP (LOOPBACK, UP) mtu 1500 qadisc no
10月10日 19:49:36 linux ifconfig: link 00:00:00:00:00:00 br 00:00:00
10月10日 19:49:37 linux ifconfig: lo: inet 127.0.0.1/8 host lo
10月10日 19:49:37 linux ifroute: IP address: 127.0.0.1/8
10月10日 19:49:38 linux ifroute: Configured routes for interface lo:
128/ - -
10月10日 19:49:39 linux ifroute: Active routes for interface lo:
10月10日 19:49:39 linux ifroute: 127.0.0.1/8 scope link
10月10日 19:49:39 linux ifconfig: eth0: inet 192.168.1.10/24
10月10日 19:49:40 linux ifconfig: eth0: address: 192.168.1.10
10月10日 19:49:40 linux ifconfig: eth0: device: Advanced Micro Devices [PCI]
10月10日 19:49:40 linux ifconfig: eth0: configuration: eth-id
10月10日 19:49:41 linux ifconfig: eth0: IP address: 192.168.1.10
~$ #
```

# 排除系统问题

**图 16-13：使用 `tail` 查看日志文件**
