
+ lpr.info /var/log/lpd-errs
+ cron.* /var/log/cron
+ *.err root
+ *.notice;news.err root
+ *.alert root
+ *.emerg *

你可以将此解读为：来自任何服务的 **err** 级别消息、来自内核的 **debug** 消息、授权 **notice** 消息以及来自邮件程序的 **crit** 消息都将打印到系统控制台，如果你将显示器连接到 FreeBSD 机器上，就能看到这些消息。同样，所有与安全相关的消息都会进入 `/var/log/security` 文件，而所有来自邮件程序的 **info** 级别消息则进入 `/var/log/maillog`。几乎所有其他消息都会进入 `/var/log/messages`，即通用系统日志文件。（如果你熟悉 Linux，这个文件相当于通常所说的 `syslog`。）

某些类型的消息不仅仅是写入日志文件，还会发送到各种其他类型的处理机制中。在默认的 `syslog.conf` 中，来自任何服务的 **err**、**notice** 或 **alert** 级别消息会打印到 root 用户登录的任何终端，而 **emerg** 消息会打印到所有用户的所有终端。表 10.4 展示了 `syslogd` 消息的可能操作及其语法。

### 表 10.4 syslogd 操作的语法

| 语法 | 执行的操作 |
| :--- | :--- |
| `/path/to/file` | 消息写入指定文件。 |
| `@some.hostname.com` | 使用 `syslog` 网络服务将消息转发到 `some.hostname.com` 上的 `syslogd`。 |
| `user1` | 消息打印到 `user1` 登录的任何终端。 |
| `root,user1,user2` | 所有指定用户在其所有终端上接收消息。 |
| `*` | 消息写入所有已登录用户。 |
| `\| "mail root"` | 消息通过邮件发送给 root。 |

有关如何配置 `syslogd` 的更多细节，可在 `syslogd` 和 `syslog.conf` 的 man 页面中找到。

> **注意**
> `/var/log` 中的每个日志文件都根据一组不同的规则进行滚动（归档）。例如，`/var/log/maillog` 文件每天由 `periodic` 程序归档并重启。其他日志文件，如 `/var/log/cron` 和 `/var/log/messages`，通过其他手段刷新（通常是由写入它们的程序内部完成）。归档的日志文件通常使用 `gzip` 压缩。要搜索旧的日志文件，请将 `gzcat` 与传统的 `grep` 结合使用：`# gzcat /var/log/messages.2.gz | grep "rejected"`

## 关于 /etc/rc.local 文件的说明

资源配置脚本 /etc/rc.local 在本章前面仅被描述为已过时。使用早期版本 FreeBSD 或某些 Linux 发行版的系统管理员会认出这个文件。它的目的与 /usr/local/etc/rc.d 目录类似——为你提供一种扩展系统启动行为的机制。

前面描述的 rc.d 方法是扩展系统启动行为的推荐方法，因为它是一种更结构化的方法。它将每个启动任务保存在其各自的脚本中，具有通用接口——被约束在 /usr/local 中，而不是 /etc 中。然而，如果你必须使用它，/etc/rc.local 仍然有效，尽管它不存在于默认安装中。你可以创建该文件（模仿其他 rc.* 文件编写正确的解释器行），并将任何一组 shell 命令放入其中，它将在 rc.d 脚本之前执行。

对 rc.local 的支持仅用于向后兼容性，最终可能会从 FreeBSD 中移除。要确保你的系统支持它，请检查 /etc/rc 中是否有对 rc.local 文件的提及，如清单 10.3 所示。

**清单 10.3 来自 /etc/rc 的摘录，显示对 /etc/rc.local 的支持**

```bash
# grep -A 5 rc.local /etc/rc
# Do traditional (but rather obsolete) rc.local file if it exists. If you
# use this file and want to make it programmatic, source /etc/defaults/rc.conf
# in /etc/rc.local and add your custom variables to /etc/rc.conf, as
# shown below. Please do not put local extensions into /etc/rc itself.
# Use /etc/rc.local
#
# --- rc.local ---
#	if [ -r /etc/defaults/rc.conf ]; then
#		./.etc/defaults/rc.conf
#	source_rc_confs
#	elif [ -r /etc/rc.conf ]; then
#		./.etc/rc.conf
--
# --- rc.local ---
#
if [ -r /etc/rc.local ]; then
	echo -n 'starting local daemons:'
	sh /etc/rc.local
	echo '.'
fi

# For each valid dir in $local_startup, search for init scripts matching *.sh
#
```

运行 `sh /etc/rc.local` 的循环就是你正在寻找的部分。如果它存在且未被注释掉，你就可以使用 `rc.local`。然而，使用 `rc.d` 脚本方法仍然是更好的主意。

# 第 11 章
## 定制 Shell

无论你选择通过 X-Window GUI 来操作你的 FreeBSD 系统——特别是作为管理员——你都需要处理 shell。Shell 提供了完成甚至最复杂任务所需的所有灵活性，但同时也规定了至少显得晦涩难懂的用户体验。在本章中，我们将让自己在 shell 中感到舒适——足以将其用作编程环境和用户界面。

### 什么是 Shell？

我们已经在第 7 章“使用 Shell”中讨论了 shell 的基础知识以及你可以用它做什么。那一章将 shell 介绍为一种命令行界面，并讨论了你可以在 FreeBSD 中使用的各种 shell 以及在 shell 中用于控制系统可用命令的类型。现在，我们将更详细地查看 shell 本身，并检查它如何应用于你可能需要在系统中支持的大量用户，以及如何按你的喜好进行定制。

你已经知道，shell（简要来说）是一种命令行界面，你可以在其中输入命令，使 Unix 计算体验与基于 GUI 的系统（如 Windows 或 Mac OS）有显著不同。Shell 在功能上类似于 MS-DOS 及其 Windows 后代中的 COMMAND.COM 命令解释器，但由于它在基于 GUI 的操作系统中扮演了比在那里更为重要的角色，因此它要复杂和有用得多。

但它为什么被称为 shell？答案与 Unix 架构中用于描述系统操作各个层级的术语有关，将其比喻为一个多层球体，最自动化的功能位于核心，用户触发的功能位于外层。内部是内核，这在前面章节中已有提及，并将在第 17 章“内核配置”中详细涵盖。系统的外部是用户。用户如何与内核及其周围的支持程序交互？自然是通过 shell。图 11.1 说明了这种关系。

![](img/48eec858cce7dfb89da36a4d40b7daf3_265_0.png)

**图 11.1** 被 shell 包围的内核。

Shell 的工作是给你——用户——一种安全、结构化的方式来访问内核。作为命令解释器，shell 接收你的命令，并将它们翻译成通过内核访问文件和设备的进程。它防止你执行可能导致内核崩溃的不安全代码，并帮助你查找和运行操作系统的程序。

从更实用的意义上说，shell 只是一个具备 fork 能力的实用工具，每当登录时由系统执行。Shell 向你显示命令提示符，解释你的命令，并在你注销时终止。事实上，这些是 shell 真正需要做的唯一事情；任何程序都可以充当 shell，这是一个事实，你可以非常有创造性地使用它，你将会看到。

你可能会在很多略有不同的上下文中遇到 shell 一词。例如，任何运行在另一个程序之上并提供其接口的程序都是某种 shell；Windows 95 在技术上是一个 shell，尽管它伪装得比它的

### 本章内容

- 什么是 Shell？
- 向系统添加 Shell 并使其可用
- 使用替代 Shell
- Shell 初始化文件
- 定制你的 Shell 环境
- Shell 和环境变量

