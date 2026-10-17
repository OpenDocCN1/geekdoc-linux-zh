
`lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S40cups -> /etc/init.d/cups`

`lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S30cups -> /etc/init.d/cups`

`lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S20cups -> /etc/init.d/cups`

`lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S10cups -> /etc/init.d/cups`

`lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/K80cups -> /etc/init.d/cups`

等待，提供的文本在 OCR 输出中存在大量重复。我将根据提示中的逻辑内容提供清理后的正确版本。

## tty 服务

遵循在 `tty1` 上启动并监控 `getty` 进程（见第 448 页）的服务的定义文件：

```bash
$ cat /etc/init/tty.conf

# tty1 - getty

#

# 此服务从系统启动到再次关闭期间，
# 在 tty1 上维护一个 getty。

start on stopped rc RUNLEVEL=[2345]

stop on runlevel [12345]

respawn

exec /sbin/getty -8 38400 tty
```

`start on` 语句块中的事件名为 `stopped`（参见 `stopped` 页面）。当 `rc` 任务在 `RUNLEVEL` 等于 2、3、4 或 5 的情况下停止时，这会启动 `tty1` 服务。由于系统在完成每个运行级别时，`rc` 任务都会停止，因此当系统进入这些运行级别之一时，`tty1` 就会启动。

`stop on` 语句块中的事件名为 `runlevel`。当发射运行级别带有除 2、3、4 或 5 以外的参数时，该语句停止 `tty1` 服务——即当系统进入恢复模式、关机或重启时。

`restart` 关键字告诉 `init` 如果 `tty` 服务终止，则重启它。这会在 `tty1` 上以 38400 波特率运行一个无校验位（`-8`）的 `getty` 进程。在示例中，`initctl` 工具报告了 `tty1` 服务已启动并作为进程 1061 运行；`ps` 对该进程进行了报告：

```bash
$ status tty
tty start/running, process 1061

$ ps -ef | grep 1061
root 1061 1 0 12:26 tty 00:00:00 /sbin/getty -8 38400 tty1
```

`control-all` 查看第 451 页关于 `control-all-delete` 任务的讨论，你可以使用它来关闭系统。

在 SysVinit 下，`/etc/initab` 中的默认项告诉 `init` 在系统启动时将系统带到哪个运行级别（第 443 页）。Ubuntu 不包含 `inittab` 文件；相反，默认情况下，Upstart `init` 进程（使用 `rc-sysinit` 任务）将系统启动到多用户模式（运行级别 2）。如果你想让系统启动到不同的运行级别，请修改 `rc-sysinit.conf` 文件中的以下行：

```bash
$ cat /etc/init/rc-sysinit.conf

env DEFAULT_RUNLEVEL=2
```

### 不要将系统启动到运行级别 0 或 6

注意 永远不要将系统启动到运行级别 0 或 6，否则它无法正常启动。要启动到多用户模式（运行级别 2），将 `DEFAULT_RUNLEVEL` 设置为 2。要启动到恢复模式，将 `DEFAULT_RUNLEVEL` 设置为 S。

## 第 11 章 系统管理：核心概念

将 `DEFAULT_RUNLEVEL` 的值从 2 改为 S 会导致系统启动到恢复模式（运行级别 S；见第 444 页的注意）。当系统进入恢复模式时，如果系统上的根账户未锁定（第 431 页），`init` 会在显示根提示符之前请求根密码。否则，它将在不请求密码的情况下显示根提示符。

## SYSVinit(rc) 脚本：启动和停止系统服务

`rc` 脚本 `init`（初始化）脚本，也称为 `rc`（运行命令）脚本，是位于 `/etc/init.d` 目录下的 shell 脚本。它们通过 `/etc/rc.d` 目录中的符号链接进行访问，其中 `n` 是系统正在进入的运行级别。

### /etc/rc.d 和 /etc/init.d 目录中的大部分文件将会消失

正如第 434 页所示。Ubuntu 使用 `Startup` 模拟级别，以帮助迁移并提供与其他发行版的兼容性。本节解释了 `init` 脚本如何工作以（模拟的）级别来控制系统服务。在本节描述的 `/etc/rc.d` 和 `/etc/init.d` 目录中的许多脚本建议你使用脚本相应的 `initctl` 命令，因为这些链接已被 `/etc/init` 中的作业控制器所替换（见第 434 页）。

`/etc/rc.d` 目录包含以 K 开头的脚本（`K19cups`、`K20dhcp`、`K74bleutoth` 等）和以 S 开头的脚本（`S15bind`、`S18nis`、`S20cima` 等）。当进入一个新的运行级别时，每个 K（kill）脚本都会带 `stop` 参数执行，然后每个 S（start）脚本都会带 `start` 参数执行。每个 K 文件都按数字顺序排列。S 文件也类似。这种安排允许设置这些文件的人在系统进入给定运行级别时控制哪些服务被停止和启动，以及按什么顺序执行。使用带有 `start` 和 `stop` 参数的脚本增加了灵活性，因为它允许根据调用的参数来同时启动和杀死进程。

如需自定义系统初始化，你可以向 `/etc/init.d` 目录添加脚本，并放置指向这些文件的链接（实践中，最好使用 `sysv-rc-conf` [已讨论] 来创建链接）。

此示例显示了 `cups` `init` 脚本的多个级别。这些链接由 `cups` 脚本调用，以便在不同的运行级别下启动或停止 `cups` 守护进程：

```bash
ls -l /etc/rc.d*/cups*
lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S50cups -> /etc/init.d/cups
lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S40cups -> /etc/init.d/cups
lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S30cups -> /etc/init.d/cups
lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S20cups -> /etc/init.d/cups
lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S10cups -> /etc/init.d/cups
lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/K80cups -> /etc/init.d/cups
```

## UPSTART 基于事件的守护进程

此示例显示了 `cups` `init` 脚本的多个级别。这些链接由 `cups` 脚本调用，以便在不同的运行级别下启动或停止 `cups` 守护进程：

### 442 第 11 章 系统管理：核心概念

仅——它不会改变任何服务的当前状态。执行以下命令查看服务列表：

```bash
$ sudo sysv-rc-conf --list
acpi-support 1:off 2:on 3:on 4:on 5:on
acpid
alsa-mixer-s
anacron
apparmor S:on
apport
atd
avahi-daemon
binfmt-support 2:on 3:on 4:on 5:on
bluetooth 0:off 1:off 2:on 3:on 4:on 5:on 6:off
```

所有运行守护进程（daemons）的服务都列在其中，每行一个，后面跟是每个运行级别（runlevel）的配置状态。如果缺少某个运行级别，意味着在 `/etc/rc.d` 目录对应的文件中没有该服务的条目。当所有运行级别都缺失时，意味着该服务由 Upstart 控制。你可以通过向之前的命令添加添加名称来检查特定守护进程的配置：

```bash
$ sudo sysv-rc-conf --list cups
cups 1:off 2:on 3:on 4:on 5:on
```

### 任务/初始化脚本的名称可能与其运行的守护进程名称不同

以下示例通过通过列出 `/etc/init` 和 `/etc/init.d` 目录的内容，并搜索与你想操作的守护进程名称或功能相似的文件，显示 `ssh` 任务控制 `ssh` 守护进程。例如，`/etc/init.d/cups` 脚本控制打印守护进程。

通常，脚本的前几行或任务中 `exec` 和 `description` 单元（stanza）的注释会标识其所控制的守护进程。任务描述文件显示了这些行：

```bash
$ cat /etc/init/ssh.conf
# ssh OpenBSD Secure Shell server
#
# The OpenSSH server为系统提供安全的 shell 访问
description "OpenSSH server"
exec /usr/sbin/sshd
```

在下一个示例中，`sysv-rc-conf`（`sysv-rc-conf` 包）配置了 `/etc/rc.d` 目录，使得 `cups` 守护进程在运行级别 2、3、4 和 5 中关闭，并确认更改。要进行这些更改，你必须使用 root 权限：

```bash
$ sudo sysv-rc-conf --level 2345 cups
$ sudo sysv-rc-conf --list cups
cups 1:off 2:off 3:off 4:off 5:off
```

## 系统操作 443

为了方便起见，你可以省略 `--level 2345` 参数。当你指定一个初始化脚本并开启或关闭状态时，`sysv-rc-conf` 默认对应运行级别 2、3、4 和 5。以下命令与上述的第一个命令等效：

```bash
$ sudo sysv-rc-conf cups off
```

`ps` 实用程序确认即使 `sysv-rc-conf` 将 `cups` 设置为在所有运行级别下都关闭，它仍在运行。`sysv-rc-conf` 并没有关闭 `cups`。

```bash
$ ps -ef | grep cups
root 998 1 12:47 ? 00:00:00 /usr/bin/cupsd -C /etc/cups/cupsd.conf
zach 5618 1334 0 18:28 pts/0 00:00:00 grep --color=auto cups
```

通过上述更改，当你重启系统时，`cups` 将不会启动。你可以使用 `cups` 初始化脚本轻松地停止它：

```bash
$ sudo service cups stop
* Stopping Unix Printing System: cupsd
$ ps -ef | grep cups
zach 5637 1334 0 18:29 pts/0 00:00:00 grep --color=auto cups
```

## 系统操作

本节涵盖了系统运行的基本知识，可以帮助你作为系统管理员做出明智决策。它没有深入检查系统管理的每一个可能的方面，以至于让你能够设置或修改所有系统功能。相反，它提供了一份启动系统并保持日常运行的指南。

## 运行级别 (RUNLEVELS)

随着 Upstart 的引入，真正的运行级别从系统中消失了。作为一种过渡工具，它们被一种在 Upstart 下运行并模拟运行级别的结构所取代（见第 434 页）。表 11-1 列出了在 Upstart 下存在的这些伪运行级别（pseudounlevels）。

表 11-1 伪运行级别

| 编号 | 名称/功能 |
| :--- | :--- |
| 0 | 关闭系统 |
| 1 | 将系统带恢复（S，单用户）模式 |
| S | 恢复（单用户）模式，文本登录，极少数系统服务运行 |
| 2 | 多用户模式，图形化登录，所有计划的系统服务均运行 |
| 3, 4, 5 | 多用户模式，图形化登录，所有计划的系统服务均运行（对于系统定制，运行级别 2–5 是完全相同的） |
| 6 | 重启系统 |

## 444 第 11 章 系统管理：核心概念

**默认运行级别** 默认情况下，Ubuntu 系统启动到多用户模式（运行级别 2）。请参第 439 页的“rc-sysinit 任务和 inittab”获取如何更改此设置的说明。

**runlevel** `runlevel` 实用程序 [`runlevel(8)` 手册页；不要将其与第 438 页描述的运行级别事件混淆] 显示之前的和当前的运行级别。该实用程序是一个过渡工具，提供了对 SysVinit 的兼容性。在示例中，N 表示系统不知道之前的运行级别是什么，2 表示系统处于多用户模式。

```bash
$ runlevel
2
```

**telinit** `telinit` 实用程序（`man`）允许具有 root 权限的用户关闭系统、重启系统以及切换恢复（单用户）和多用户模式。`telinit` 实用程序是一个过渡工具，提供了对 SysVinit 的兼容性。该实用程序根据其参数发布运行级别事件（第 438 页）。`telinit` 命令的格式为

*runlevel* 是表 11-1（上一页）描述的伪运行级别之一。

**恢复模式和 root 密码** 当系统进入恢复（单用户）模式时，如果 `root` 账户锁定（第 431 页），它会在显示 `root` 提示符之前请求 `root` 密码。否则，它直接显示 `root` 提示符。

**不要直接运行级别** 使用 `telinit` 运行级别 S 是一个糟糕的主意。

**Upstart 会** 在系统启动时调用 `rc-sysinit` 文件（第 439 页）。

**启动系统**

**列出内核启动消息** 要保存内核消息列表，请启动后立即运行 `dmesg`：

```bash
$ dmesg > dmesg.boot
```

## 446 第 11 章 系统管理：核心概念

```
GNU GRUB version 1.98-ubuntu
Ubuntu, with Linux 2.6.32-22-generic
Ubuntu, with Linux 2.6.32-22-generic (recovery mode)
Ubuntu, with Linux 2.6.32-21-generic
Ubuntu, with Linux 2.6.32-21-generic (recovery mode)
Memory test (memtest86+)
Memory test (memtest86+, serial console i15200)
```
