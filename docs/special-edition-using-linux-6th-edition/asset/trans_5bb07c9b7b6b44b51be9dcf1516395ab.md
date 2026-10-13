

## 第13章
## 系统初始化

### 本章内容包括

- 关于初始化 270
- init：一切从此开始 270
- inittab 详解 273
- rc 脚本 278
- 紧急情况 282
- 故障排查 284

### 关于初始化

Linux 既可以使用 System V（SysV）风格的系统初始化，也可以使用 BSD 风格的系统初始化。这是 UNIX 和 Linux 世界中执行系统初始化的两种主要方法。BSD 使用少数几个大型脚本来处理所有系统初始化。BSD 初始化仅由 Slackware 发行版使用。SysV 使用运行级别和一组初始化脚本。这些初始化脚本根据*运行级别*（也称为*系统状态*）来启动和停止*守护进程*（后台进程）。每个守护进程或进程对应一个脚本，集中存放在一个目录中（稍后将详细讨论）。按照惯例，System V 的运行级别范围为 0–6，每个运行级别对应一种不同的操作模式，而且经常并非所有运行级别都会被使用。尽管 SysV 初始化看起来更复杂，尤其是对于来自 DOS 和 Windows 世界的人来说，但这种表象掩盖了 BSD 风格初始化所不具备的灵活性。

Windows 用户可能会想到将启动时按 F8 看到的初始屏幕与 Linux 的 SysV 运行级别进行比较。Windows 的“运行级别”包括 DOS、安全模式、带网络连接的安全模式等等。将它与 Linux 中的运行级别相比，就像把一架老式双翼飞机（你必须降落、拿出扳手、拆下爬升螺旋桨、换上巡航螺旋桨、爬回座舱、再次起飞）比作一架装有变距螺旋桨和自动废气门控制器的现代涡轮增压 Mooney 飞机。实在没法比。

### init：一切从此开始

图 13.1 展示了默认启动过程，假定未使用 initrd。这个启动过程可以通过不同方式被跳过或修改，但此图会让你对标准安装如何启动有一个清晰的认识。

**图 13.1**

默认启动顺序。

![](img/c741b1b6b6eccaba2ad43454c979a7f8_289_0.png)

内核载入内存之后（参见第12章“引导加载程序”），你就有了一个正在运行的 Linux 系统——但它还不太可用，因为内核不直接与用户或用户空间交互（更多细节参见第14章“自定义你的 Shell 环境”）。内核运行一个程序：init。这个程序负责其余一切，并被称为所有进程的父进程。然后内核退居其位，担任系统管理器，处理内核空间和所有资源访问请求。

当 init 启动时，它会从位于 /etc 目录中的一个名为 inittab 的文件（代表初始化表）读取其配置。如果在命令行上覆盖了 inittab 中的任何默认值，这些默认值将被丢弃。inittab 文件描述了 init 如何设置系统。默认的 OpenLinux inittab 参见清单 13.1。稍后，你将了解如何覆盖 inittab 默认值、为什么你可能想要或需要这样做，以及这样做的具体影响。

> **提示**
>
> 以 tab 结尾（如 inittab、fstab、mtab 等）表示该文件是一个表——通常是配置表。就 inittab 而言，它告诉 init 如何初始化系统，很像 DOS 中的 config.sys。

**清单 13.1 /etc/inittab 文件**

```
#
# inittab       This file describes how the INIT process should set up
#               the system in a certain run-level.
#
# Author:       Miguel van Smoorenburg, <miquels@drinkel.nl.nugnet.org>
#               Modified for RHS Linux by Marc Ewing and Donnie Barnes
#               Modified for COL by Raymund Will
#
#
# The runlevels used by COL are:
#   0 - halt (Do NOT set initdefault to this)
#   1 - Single user mode (including initialisation of network interfaces,
#       if you do have networking)
#   2 - Multiuser, (without NFS-Server und some such)
#       (basically the same as 3, if you do not have networking)
#   3 - Full multiuser mode
#   4 - unused
#       (should be equal to 3, for now)
#   5 - X11
#   6 - reboot (Do NOT set initdefault to this)
#
#
# Default runlevel.
id:5:initdefault:
#
# System initialization.
s0::sysinit:/bin/bash -c 'C=/sbin/booterd; [ -x $C ] && $C'
si::sysinit:/bin/rc.d/rc.boot
s1::sysinit:/bin/bash -c 'C=/etc/rc.d/rc.S; [ -x $C ] && $C default'
s2::sysinit:/bin/bash -c 'C=/etc/rc.d/rc.serial; [ -x $C ] && $C'
bw:bootwait:/etc/rc.d/rc.boot

# What to do in single-user mode.
~:S:wait:/etc/rc.d/rc 1
~~:S:wait:/sbin/sulogin

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
# Normally not reached, but fallthrough in case of emergency.
z6:6:respawn:/sbin/sulogin

# Trap CTRL-ALT-DELETE
ca:12345:ctrlaltdel:/sbin/shutdown -t3 -r now

# Action on special keypress (ALT-UpArrow).
kb::kbrequest:/bin/echo "Keyboard Request --edit /etc/inittab to let this work."

# When our UPS tells us power has failed, assume we have a few minutes
# of power left. Schedule a shutdown for 2 minutes from now.
# This does, of course, assume you have power installed and your
# UPS connected and working correctly.
pf::powerfail:/sbin/shutdown -h +5 "Power Failure; System Shutting Down"

# If battery is fading fast -- we hurry...
p1::powerfailnow:/sbin/shutdown -c 2> /dev/null
p2::powerfailnow:/sbin/shutdown -h now "Battery Low..."

# If power was restored before the shutdown kicked in, cancel it.
po:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

# Run gettys in standard runlevels
1:12345:respawn:/sbin/getty tty1 VC linux
2:2345:respawn:/sbin/getty tty2 VC linux
3:2345:respawn:/sbin/getty tty3 VC linux
4:2345:respawn:/sbin/getty tty4 VC linux
5:2345:respawn:/sbin/getty tty5 VC linux
6:2345:respawn:/sbin/getty tty6 VC linux

# Run kdm in runlevel 5
gu:5:respawn:/bin/sh -c "C=/etc/rc.d/rc.gui;[ -x $C ]&&exec $C;init 3"
```

> 运行级别只是使用软件将进程包分组的一种便捷方式。它们对内核没有特殊意义。所有 Linux 内核都以相同的方式启动引导过程。只有在 init 启动之后，你才开始使用运行级别。

### inittab 详解

> **注意**
>
> 本文以 Caldera OpenLinux 的 `inittab` 为例进行说明。你的 `inittab` 可能不同，但工作方式相同。阅读完本节后，你应该能够理解大多数 Linux 的 `inittab`。

阅读 `inittab` 时，你会跳过任何以 `#` 开头的行，因为这些行会被 `init` 当作注释忽略。其余的行可以像许多其他典型的 UNIX 类配置表一样轻松阅读；也就是说，每一列用冒号（`:`）分隔，可以按如下方式解读：

- **id**——第一列是该行的唯一标识符。它最长可以是四个字母数字字符，但通常限制为两个。较旧的系统限制为两个字母数字字符，大多数发行版没有改变这一惯例。
- **runlevel**——第二列指示该行对哪些运行级别有效。此列可以为空，也可以包含任意数量的有效运行级别。如果为空，则对所有运行级别都有效。
- **action**——可以是多种情况；最常见的是 `respawn`，但也可以是以下任何一种：`once`、`sysinit`、`boot`、`bootwait`、`wait`、`off`、`ondemand`、`initdefault`、`powerwait`、`powerfail`、`powerokwait`、`ctrlaltdel`、`kbrequest`。
- **process**——要运行的具体进程或程序。

`inittab` 中的每一行都有一个唯一标识符。通常，这个标识符很容易与所执行的特定操作关联起来。例如，在第一个串行端口上生成一个 getty 的行可能会对 `/dev/ttyS0` 使用标识符 `S0`。

默认情况下，运行级别标识为 0–6 和 A–C。运行级别 0、1 和 6 是特殊的——不要随意更改它们。它们分别对应系统停机、维护模式和系统重启。例如，更改运行级别 1 可能会产生深远影响。请注意，要进入维护模式（运行级别 1），你可以向 init 传递参数 1（使用 telinit）。或者，你也可以使用 S 或 s。如果你更改了运行级别 1 所对应的操作，那么使用 S 或 s 时也会应用相同的更改。不过，运行级别 2–5 可以根据需要自定义。（参见“故障排查”一节，了解如何引导到默认运行级别之外的运行级别。）

> **注意**
>
> 使用 `telinit` 是向 init 传递命令的首选方法，但直接调用 init 也并不少见。

大多数 Linux 发行版都包含 `runlevel` 命令（位于 `/sbin` 中），该命令可用于提供有关当前和先前运行级别的信息。执行此命令会输出先前的运行级别和当前的运行级别，例如 `N 3`。`N` 表示没有先前的运行级别，这种情况可能出现在重启之后；`3` 表示当前的运行级别。如果你将运行级别更改为 2，然后重新发出 `runlevel` 命令，你将看到 `3 2`。

