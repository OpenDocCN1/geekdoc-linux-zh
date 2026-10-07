

**提示** 如果你拥有一块在 Linux 中使用前需要在 DOS 环境下初始化的硬件，LOADLIN 特别有用。例如，某些声卡在 Linux 中使用前必须被初始化为特殊的 SoundBlaster 兼容模式，而执行此操作的程序只能在 DOS 下运行。你可以创建一个 DOS 分区，从 CONFIG.SYS 或 AUTOEXEC.BAT 中运行声卡初始化程序，然后启动 LOADLIN。其结果是 Linux 启动时，硬件已处于 Linux 可接受的状态。

**警告** 尽管 LOADLIN 可以在 Windows 的 DOS 提示符下运行，也可以在 Windows 95 和 98 的 DOS 兼容模式下运行，但该模式实际上已从 Windows Me/NT/2000/XP 中移除。因此，如果不进行特殊处理，LOADLIN 无法从完整的 Windows Me/NT/2000/XP 启动中运行，但它可以从 Windows Me 紧急软盘或 Windows 95/98 启动软盘中运行。有关进一步说明，请参阅 [http://www.tldp.org/HOWTO/mini/Loadlin+Win95−98−ME.html](http://www.tldp.org/HOWTO/mini/Loadlin+Win95−98−ME.html) 上的 HOWTO 文档。

## 单用户模式

单用户模式是一种维护模式，在这种模式下会启动 root shell，且不允许其他用户登录。提示符会变为井号（#），以表明这是一个 root shell。可以使用命令 `init 1` 启动此模式，或者在 LILO 提示符后的镜像标签后添加单词 `single` 或数字 `1`。如果你正在系统上工作并决定需要进入单用户模式，请输入 `init 1`。如果你使用 LILO，并且由于内核恐慌（kernel panic）等原因重启了系统，当 LILO 提示符出现时，只需在镜像标签后添加 1，例如：

```
LILO: linux single
```

或者

```
LILO: linux 1
```

如果你使用 GRUB 并需要进入单用户模式，你必须进入图形化的 GRUB 屏幕，选择 Red Hat 启动标签。然后按 E 键进行编辑。向下移动到 kernel 行，按 E 键编辑。在提示符处输入单词：**single**。当返回到包含内核信息的 GRUB 屏幕时，按 B 键将系统启动到单用户模式。

当系统启动到单用户模式时，与多用户环境相关的初始化任务将被跳过，如果通过 init 程序切换到单用户模式，所有守护进程（daemon processes）都会停止。init 进程接下来会在 /dev/console 上以 root 用户身份启动一个 Bourne shell。根文件系统会被挂载，其他文件系统可供检查或挂载。不会自动运行守护进程，并且由于某些资源的主文件系统未挂载，这些资源可能不可用。

例如，如果 /usr 位于单独的分区（即它是独立的文件系统），除非手动挂载 /usr 分区，否则 /usr/bin、/usr/sbin 或 /usr/X11R6/bin 中的任何命令都不可用。在提示符处输入 `exit` 将退出单用户 shell，而 Ctrl+D 会将系统启动到其正常的多用户模式。

如果启动过程出现问题，你也可能进入系统发起的单用户模式。在这种情况下，你会被放入一个 root shell，拥有 root 访问权限，可以进行必要的更改以使系统可启动。这种情况最常见于启动期间运行的 fsck 过程失败，且系统需要手动检查和修复文件系统时。

单用户模式的一个用途是在密码未知时更改 root 密码，例如当员工离开公司但未提供密码时。没有方法可以检索旧密码，但单用户模式提供了 root 访问权限，因此你可以使用 `passwd` 命令输入新的 root 密码。当你重启到多用户模式时，新密码将像以前一样允许你拥有 root 访问权限。

这说明了允许对系统控制台进行无限制访问所带来的安全威胁以及单用户模式的风险。显然，你不希望任何人都能启动你的系统并更改 root 密码。为了保护单用户模式，你可以让引导加载程序（boot loader）要求密码，如前面在具体的 GRUB 和 LILO 章节中所述。

为了获得最佳安全性，你应该对 BIOS 进行密码保护，并将其设置为*不*从软盘启动。这两个操作将计算机配置为：除非用户拥有 BIOS 密码，否则无法从软盘启动计算机。如果你不采取这些步骤，拥有物理访问权限的入侵者只需插入一张 Linux 启动软盘即可修改磁盘上的系统。尽管有了更多时间，拥有物理访问权限的入侵者可以移除硬盘或使用主板上的恢复跳线来绕过这些预防措施。除非对磁盘上的所有数据进行加密，否则如果入侵者可以打开计算机机箱，你将无法阻止篡改。

## 初始化和启动脚本

在本章前面，我们将初始化确定为启动过程的最后阶段。不同发行版之间的初始化过程略有不同。这些差异包括脚本的位置和名称，以及默认实际运行的内容。我们将首先查看该过程，并在遇到差异时进行讨论。初始化过程从内核启动 init 程序时开始。该程序解析 /etc/inittab 文件以确定要运行哪些程序的具体内容，以及完成后系统将处于哪个运行级别（run level）。我们将查看一个来自 Red Hat（使用 System V 风格的脚本）的示例，以及另一个来自 Debian（使用 BSD 模型）的示例。Slackware 和 SuSE 的方法与 Debian 模型中看到的非常相似。Slackware 默认自带一个空的 rc.local。

### Red Hat 模型

所有发行版都在某种程度上定制其初始化脚本，但大多数 inittab 文件都非常相似。列表 3.3 展示了 Red Hat 7.3 系统中 inittab 文件的一个示例。

**列表 3.3：一个 inittab 文件示例**

```
#
# inittab    This file describes how the INIT process should set up
#             the system in a certain run-level.
#
# Author:          Miguel van Smoorenburg, <miquels@drinkel.nl.mugnet.org>
# Modified for RHEL Linux by Marc Ewing and Donnie Barnes
#
#
# Default runlevel. The runlevels used by RH are:
#
#   0 - halt (Do NOT set initdefault to this)
#   1 - Single user mode
#   2 - Multiuser, without NFS (The same as 3, if you do not have networking)
#   3 - Full multiuser mode
#   4 - unused
#   5 - X11
#   6 - reboot (Do NOT set initdefault to this)
#
id:3:initdefault:

# System initialization.
si::sysinit:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6

# Things to run in every runlevel.
ud:once:/sbin/update

# Trap CTRL-ALT-DELETE
ca:ctrlaltdel:/sbin/shutdown -t3 -r now

# When our UPS tells us power has failed, assume we have a few minutes
# of power left.  Schedule a shutdown for 2 minutes from now.
# The following lines were added on 9/17/01 for a CyberPower 700 AVR UPS

#UPS signals a power outage.
pf:12345:powerfail:/sbin/powstatd.fail

# UPS signals power restored before the shutdown kicks in.
pr:12345:powerokwait:/sbin/powstatd.ok

# UPS signals low battery power: emergency shutdown.
pn:12345:powerfailnow:/sbin/powstatd.low

# Run gettys in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6

# Run xdm in runlevel 5
# xdm is now a separate service
x:5:respawn:/etc/X11/prefdm -nodaemon
p:1:respawn:/usr/sbin/moused -Q
```

该文件以一组注释开头，包括 Red Hat 中使用的运行级别摘要；让我们花点时间看看这六个运行级别及其用途：

| 运行级别 | 描述 |
| :--- | :--- |
| 0 | 用于停止系统。为此，系统执行 INIT 0 命令并停止。如注释所述，你不应将 initdefault 设置为此级别。 |
| 1 | 将系统置于单用户模式。 |
| 2 | 将系统置于多用户模式，但不支持网络。 |
| 3 | 将系统置于标准的完全多用户模式，但不会自动启动 X。 |
| 4 | 未使用 |
| 5 | X11：将系统置于带有图形（基于 X 的）登录的标准多用户模式。 |

