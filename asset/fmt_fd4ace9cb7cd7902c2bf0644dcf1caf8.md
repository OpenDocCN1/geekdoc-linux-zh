
![](img/9139201cfcaf4292284a0eed074928e5_673_0.png)

## 12

## RHCE Administrative Tasks

### CERTIFICATION OBJECTIVES

- 12.01 Automate System Maintenance
- 12.02 Kernel Run-Time Parameters
- 12.03 Create an RPM Package
- 12.04 Special Network Options
- ✓ Two-Minute Drill
- Q&A Self Test

系统维护的自动化是 RHCSA 和 RHCE 考试的目标。对于 RHCE，你需要知道如何为此目的创建 shell 脚本。你将学习 RHEL 6 上使用的一些示例脚本。标准脚本可能按小时、天甚至每周使用。Linux 内核灵活且高度可定制。通过在 `/proc` 目录中配置不同的运行时参数，内核可以修改以满足用户的需求。

RHCE 考试的特殊挑战之一是自定义 RPM 包的配置。比你想象的要容易。RHEL 6 已包含优秀的工具来帮助你创建该自定义 RPM。

RHCE 目标还包括一些特殊网络选项。你需要知道如何将系统设置为 Kerberos 客户端。在复杂的网络中，你可能需要在网络之间配置特殊路由。最后，鉴于可以配置的系统种类繁多，你应该知道如何通过网络连接到远程存储；RHCE 为此指定了 Internet Small Computer Systems Interface（iSCSI）。

## INSIDE THE EXAM

本章直接涉及六个 RHCE 目标。第一个是系统管理的基本技能，具体为

- Use scripting to automate system maintenance tasks

虽然较早版本的目标指定使用 bash shell，但一些 Linux 用户使用不同的 shell。没关系。管理脚本将一系列命令组合在单个可执行文件中。自动化脚本通常按固定时间表运行，这使得 cron 守护进程非常适合此目的。

一些 Linux 管理任务可以通过内核运行时参数来完成，即内核如何管理操作系统。这是通过 `/proc/sys` 目录中的文件和 `sysctl` 命令实现的，并由以下目标概括：

- Use /proc/sys and sysctl to modify and set kernel run-time parameters

由于 RHEL 和其他 Linux 发行版使用 RPM 包配置，了解如何创建自己的 RPM 会很有帮助。以下 RHCE 目标是该过程的第一步，即

- Build a simple rpm that packages a single file

本章还涉及 RHCE 目标中的几个网络任务。iSCSI 发起程序的配置，如以下目标所述，是客户端的配置：

- Configure system as an iSCSI Initiator persistently mounting existing Target

以下目标与将系统配置为 Kerberos 客户端相关：

- Configure system to authenticate using Kerberos

最后，以下目标与企业网络的细节相关；

- Route IP traffic and create static routes

## CERTIFICATION OBJECTIVE 12.01

### Automate System Maintenance

如第 9 章所述，RHEL 6 包含许多用于系统维护的标准脚本，由 `/etc/crontab` 和 `/etc/anacrontab` 配置文件驱动。在该章中，你可以回顾在各种 `/etc/cron.*` 目录中脚本运行时间的基本信息。在本章中，你将深入了解 `/etc/cron.*` 目录中的一些标准脚本的细节，然后详细分析各种脚本命令。掌握这些信息后，你也能够创建管理脚本。

### Standard Administrative Scripts

从 `/etc/cron.hourly` 目录中的脚本开始。虽然 anacron 脚本的意图已在第 9 章中总结，但你将在此处详细分析它。但首先，从一个更简单的脚本 `mcelog.cron` 开始，它每小时记录机器检查异常数据。该脚本有两行。第一行在大多数脚本中都是标准的，因为它指定后续命令受 bash shell 语法的管辖：

```
#!/bin/bash
```

通常，以井号符号（`#`）开头的行是注释。这行是个例外。第二行是对 `mcelog` 命令的直接执行，如果未找到设备则会静默退出（`--ignorenodev`），并过滤掉（`--filter`）已知问题，然后将消息（`>>`）追加到 `/var/log/mcelog` 文件的末尾。

```
/usr/sbin/mcelog --ignorenodev --filter >> /var/log/mcelog
```

接下来，检查 `/etc/cron.daily` 目录的内容。稍复杂一些的脚本是 `logrotate`。它以看起来像是不同 shell 操作符的内容开头：

> 实际上与 `0anacron` 脚本相关存在一个错误；有关更多信息，请在 https://bugzilla.redhat.com 上搜索 bug 675077。

```
#!/bin/sh
```

但该命令是软链接到 `/bin/bash` 命令，即 bash shell。文件中的下一行会自动执行。`logrotate` 命令根据 `/etc/logrotate.conf` 文件中定义的规则轮转日志，如第 9 章所述。标准日志消息被发送到 `/dev/null`，这本质上是 Linux 的垃圾箱。错误消息，如 `2>` 所表示，被发送到标准输出，如 `&1` 所指示。

> 某些 Linux 发行版（非 Red Hat）将 `/bin/sh` 命令链接到 bash 以外的 shell。除非在脚本中指定了 `#!/bin/bash`，否则它可能无法移植到其他发行版。

```
/usr/sbin/logrotate /etc/logrotate.conf >/dev/null 2>&1
```

以下行将标准退出值赋给名为 `EXITVALUE` 的变量：

```
EXITVALUE=$?
```

成功时的退出值为 0。如果出现问题，退出值是其他某个数字。`if` 命令开始一个条件语句。感叹号字符（`!`），看起来像感叹号，本质上意味着“不是”或“除此之外”。因此，下面的 if 条件在 `EXITVALUE` 的值不是 0 时为真：

```
if [ $EXITVALUE != 0 ];
```

因此，如果 `EXITVALUE` 不是 0，则 if 条件内的命令会被执行，这可以帮助管理员识别 `logrotate` 脚本或相关日志文件的问题。

```
/usr/bin/logger -t logrotate "ALERT exited abnormally with [$EXITVALUE]"
```

![](img/9139201cfcaf4292284a0eed074928e5_676_0.png)

![](img/9139201cfcaf4292284a0eed074928e5_676_1.png)

随后出现的 `fi` 命令结束以 `if` 开始的条件语句。最后一个指令返回 0，表示成功：

```
exit 0
```

由于这对于刚接触脚本的用户来说可能令人困惑，现在是时候查看脚本中可用的一些基本命令了。

## 脚本命令

脚本包含各种命令结构。一些命令组被组织在循环中，只要条件满足就会继续运行。这些命令结构也称为操作符。常见的操作符包括 `for`、`if` 和 `test`。循环的结尾可以用 `done` 或 `fi` 等操作符标记。某些操作符仅在其他操作符的上下文中存在，这将在以下小节中描述。

## 使用 if 的测试操作符

`if` 操作符主要用于检查文件是否属于某种类型。例如，以下命令检查 `/var/cache/man/whatis` 文件（一个本地的手册页数据库）是否不是一个普通文件：

```
if [ ! -f /var/cache/man/whatis ]
```

如前所述，感叹号（`!`）表示“除此之外”。`-f` 检查其后的文件名是否为当前存在的普通文件。关键在于 bash shell 脚本中常见的测试操作符。其中一些操作符列在表 12-1 中。

`if` 操作符通常与 `then` 相关联，可能还有 `else` 操作符。例如，考虑以下假设示例：

```
if [ -e /etc/inittab ];
then
/bin/ls /home > /root/homedirs
else
/bin/echo "Don't reboot, /etc/inittab is missing!"
fi
```
