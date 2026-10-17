
在切换到另一个操作系统时，请务必执行冷启动。这会清空内存。当从一个操作系统切换到另一个时，我遇到了热启动的问题。任何操作系统都可能出现各种奇怪的错误，有时驱动程序无法正确加载。

![](img/8ad518fddafc7f5e73715a2604b61d50_228_0.png)

确保备份所有内容，并在更改引导扇区时小心谨慎。

![](img/8ad518fddafc7f5e73715a2604b61d50_228_1.png)

你可以使用第三方程序（如 `Partition Magic`）或 `FIPS`（随 `Slackware` 附带）来分割和操作分区。尽管这两种方法都相当可靠，但是，它们并不能替代备份的需求；你永远不知道会发生什么。

![](img/8ad518fddafc7f5e73715a2604b61d50_228_2.png)

有关 `FIPS` 的详细信息，请参阅第 1 章。

双启动分区的另一个主要问题是当 `LILO` 卡在引导扇区中，并且需要将其移除。这种情况包括升级 `Slackware` 版本或重新分配硬盘空间。要从 `DOS`/`Windows95` 端移除它，只需在 `DOS` 提示符下键入以下内容：

```
C:\> fdisk /mbr
```

这将清理引导扇区。如果你需要重新安装 `LILO`，它会将其放回引导扇区。

![](img/8ad518fddafc7f5e73715a2604b61d50_228_3.png)

你可能希望在重新分区 `Windows95` 或 `DOS` 分区之前移除 `LILO`。然后使用 `Linux` 启动盘重启并重新安装 `LILO`。

## 运行级别

你的 `Slackware` 系统始终以某个运行时级别，即`运行级别`运行。电视有开和关两种状态，而 `Slackware` 系统则有多个“开”的级别。这些对应于五种用户类型的运行级别：单用户模式（级别一）以及第二、第三、第四和第五级别。这些级别决定了计算机在当时的功能。每个运行级别的功能由`/etc/inittab`文件确定，如清单 7-3 所示。

# 清单 7-3：使用 `/etc/inittab`

```
"# inittab  This file describes how the INIT process should set up\n#     the system in a certain run level.\n#\n# Version:   @(#)/inittab       2.04   17/05/93   MVS\n#                  2.10   02/10/95         PV\n#\n# Author:   Miguel van Snoorenburg, <MiguelS@drinkel.nl.mugnet.org>\n# Modified by:  Patrick J. Volkerding, <volkerdi@ftp.cdrom.com>\n#\n# Default runlevel.\nid:3:initdefault:\n"
```

这是默认的运行级别。当您启动 `Linux` 系统时，它会自动启动到运行级别 3。您可以根据需要更改此设置。

```
"# System initialization (runs when system boots).\nsi::sysinit:/etc/rc.d/rc.S\n"
```

无论您的系统使用哪个运行级别，它总是先运行 `S` 级别（系统初始化级别）。然后，在系统初始化运行级别下，它会读取`/etc/rc.d/rc.S`文件。

```
"# Script to run when going single-user (run level 1).\nsu:1S:wait:/etc/rc.d/rc.K\n"
```

如果您需要对磁盘分区或文件系统执行系统维护，请启动到单用户模式。安装 `Slackware` 时，您就处于单用户模式。这是一种管理模式，因此系统不会提示您输入 `root` 密码。请记住，您不希望任何人都能启动到单用户模式；这就是为什么物理安全很重要——尤其是对于笔记本电脑。

```
"# Script to run when going multi user.\nrc:2345:wait:/etc/rc.d/rc.M\n"
```

运行级别 2、3、4 和 5 是多用户级别。它们允许 `root` 以外的用户登录到 `Linux` 系统。运行级别 3 和 4 已经定义；要定义其他运行级别，您需要为`/etc/rc.d/rc.2`和`/etc/rc.d/rc.5`编写脚本。示例如下。

```
# What to do at the "Three-Finger Salute"
ca::ctrlaltdel:/sbin/shutdown -t5 -rf now

# Runlevel 0 halts the system.
10:0:wait:/etc/rc.d/rc.0

# Runlevel 6 reboots the system.
16:6:wait:/etc/rc.d/rc.6
```

`运行级别 0` 和 `6` 用于关闭系统。`运行级别 6` 在关闭后重启系统，使主机进入系统初始化模式。

![](img/8ad518fddafc7f5e73715a2604b61d50_230_0.png)

> 虽然您可以像在 `DOS` 中那样通过按下 `Ctrl-Alt-Del`（“三指致敬”）来强制重启系统，但这样做可能会破坏已挂载的文件系统。请将此方法仅保留在紧急情况使用。

如果系统处于多用户运行级别时您需要重启，请使用 `运行级别 6` 或 `reboot` 命令，如下例所示：

```
# What to do when power fails (shut down to single-user).
pf:powerfail:/sbin/shutdown -f +5 "THE POWER IS FAILING"

# If power is back before shutdown, cancel the running shutdown.
pg:0123456:powerokwait:/sbin/shutdown -c "THE POWER IS BACK"

# If power comes back in single-user mode, return to multiuser mode.
ps:S:powerokwait:/sbin/init 5
```

上面给出的脚本是处理电源故障期间运行级别的典型脚本。如果电源故障，`Linux` 将关闭到单用户模式。如果电源在关机完成前恢复，则取消关机。但是，如果电源恢复且 `Linux` 主机处于单用户模式，`级别 5` 启动（`/sbin/init 5` 将当前运行级别更改为 5）。示例如下：

```
# The getties in multiuser mode on consoles an serial lines.
#
# NOTE NOTE NOTE adjust this to your getty or you will not be
#       able to login !!
#
# Note: for 'agetty' you use linespeed, line.
# for 'getty_ps' you use line, linespeed and also use 'gettydefs'
c1:12345:respawn:/sbin/agetty 38400 tty1 linux
```

```
c2:1235:respawn:/sbin/getty 38400 tty2 linux
c3:1235:respawn:/sbin/getty 38400 tty3 linux
c4:1235:respawn:/sbin/getty 38400 tty4 linux
c5:1235:respawn:/sbin/getty 38400 tty5 linux
c6:1235:respawn:/sbin/getty 38400 tty6 linux
```

`getty` 命令生成新的终端。您可能需要更改设置以匹配适当的线路速度。这在所有活动的运行级别上设置了六个控制台（`c1` 到 `c6`）。

```
# Serial lines
#$1:12345:respawn:/sbin/getty 19200 ttyS0 vt100
#$2:12345:respawn:/sbin/getty 19200 ttyS1 vt100
# Dialup lines
#d1:12345:respawn:/sbin/getty -mt60 38400,19200,9600,2400,1200 ttyS0 vt100
#d2:12345:respawn:/sbin/getty -mt60 38400,19200,9600,2400,1200 ttyS1 vt100
```

此代码设置您的串行连接。目前，它仅设置 `ttyS0` 和 `ttyS1`，但您可以对其进行调整以适用于额外的串行连接，如下一个示例所示：
