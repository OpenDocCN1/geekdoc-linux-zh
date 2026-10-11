
由于 *init* 是第一个进程，它的 PID 编号始终为 1。

文件 */etc/inittab* 包含了 *init* 在每个运行级别（run-level）下如何设置系统的相关信息。如果 */etc/inittab* 文件丢失或严重损坏，你将无法引导任何标准运行级别（0-6），而必须使用单用户模式或紧急模式。

/sbin/init 程序执行一些系统检查，例如验证文件系统的完整性，并启动操作系统正常运行所需的关键程序。随后，它会检查 */etc/inittab* 文件以确定 Linux 的整体操作模式或运行级别。表 1 列出了有效的运行级别：

表 1：展示 Linux 运行级别

| 模式/运行级别 | 目录 | 运行级别描述 |
| --- | --- | --- |
| 0 | /etc/rc.d/rc0.d | 关机 |
| 1 | /etc/rc.d/rc1.d | 单用户模式 |
| 2 | /etc/rc.d/rc2.d | 未使用（可由用户定义） |
| 3 | /etc/rc.d/rc3.d | 完全多用户模式（无图形界面） |
| 4 | /etc/rc.d/rc4.d | 未使用（可由用户定义） |
| 5 | /etc/rc.d/rc5.d | 完全多用户模式（带图形界面） |
| 6 | /etc/rc.d/rc6.d | 重启 |

根据选定的运行级别，init 进程执行位于 */etc/rc.d* 目录子目录中的启动脚本。用于运行级别 0 到 6 的脚本分别位于子目录 */etc/rc.d/rc0.d* 到 */etc/rc.d/rc6.d* 中。

以下是 */etc/rc.d/rc3.d* 目录中脚本的目录列表：

```bash
[root@netmon tmp]# ls /etc/rc.d/rc3.d
K01nnd k20rwhod k50xinetd k74ypserv
K921pysadm S60lpd
K08wmare K25squid K54pxe K74yxprfd K92upsd S83iscsi
K09junkbuster K28am K55routed K75gated K961rda S90crond
K10fontcastie k30mserv K61ldap K75nets K95kudzu S90xfs
K121msqld
K30sendmi K65ident K846ppd S06reconfig S91atalik
K15gpm K34yppasswd K65kadmin k84ospsf6d S081ptabless95anacon
K15httpl k35sm K65procpspr K84ospsd S10network S97rhnsd
K15postgresql S35vncserver K65krp524 k84ripd s12syslog S991local
K16varpd K40lms-4nvk K65krp5kdc K84riprnd S17keytabIe S93local
K20bootparam K45arpwatch K73xpybind k85zebra
S20random S99wine
K20nfs k45nand K74app k86fnflock S28autofs
K20restart k46radvd K74nsd K87portmp S40atd
K20rusersd k50smnd K74ntpd K911sdsn S55sshd
K20rwatld k50tux K74nps K921pchans S56rawdevices
[root@netmon opt]#ls /etc/rc.d/rc3.d/
```

S 脚本将按照此顺序启动，直到它们全部启动完毕。当系统关闭时，对应的 K（或 kill）脚本将运行，以关闭从 rc 目录启动的服务。通常，每个 S 脚本都应该有一个对应的 K 脚本来在关机时终止服务。如果你在启动目录中找不到对应的 K 脚本，它可能位于关机目录中。当系统关闭时，它进入运行级别 6。

# 确定默认引导运行级别

默认引导运行级别在 /etc/inittab 文件中通过 initdefault 变量设置。当设置为 3 时，系统将在 VGA 控制台上以文本界面引导；当设置为 5 时，你将获得图形控制台。

以下是文件的一个片段（删除你不需要的 initdefault 行）：

```bash
# default runlevel. The runlevels used by RHS are:
# 0 - halt (Do NOT set initdefault to this)
# 1 - Single user mode
# 2 - Multiuser, without NFS (The same as 3, if you do not have networking)
# 3 - Full multiuser mode
# 4 - unused
# 5 - X11
# 6 - reboot (Do NOT set initdefault to this)
#
id:3:3:initdefault: # Console Text Mode
id:5:5:initdefault: # Console GUI Mode
```

将 initdefault 从 3 更改为 5，或反之，会影响你下一次重启。请参阅以下章节，了解如何在下次重启前始终获取图形登录界面。

不要将 initdefault 值设置为 6，否则你的系统将不断重启。将其设置为 0 将永远不会允许系统启动！

# 获取图形控制台

如果你的系统在 VGA 控制台上以文本终端模式启动，而你希望获取图形控制台，你有两个主要选项。选项如下：

手动方法：每次需要时，你可以通过在 VGA 控制台上运行以下 startx 命令来启动 X 终端图形应用程序：

```bash
[root@netmon tmp]# startx
```

请记住，当你注销时，你会再次回到普通的基于文本的控制台。

自动方法：你可以使用 init 命令让 Linux 在每次登录尝试时自动启动到 X 终端图形控制台，直到下一次重启。你需要如前几节所述，编辑 /etc/inittab 文件中的 initdefault 变量，以便在重启后保留此功能。

```bash
[root@netmon tmp]# init 5
```

如果你的服务器 CPU 容量或可用内存较低，或者你想要最大化所有系统资源，你可能希望大部分时间都在运行级别 3 的文本模式下操作，仅在有必要时使用 startx 命令使用图形界面。

既作为个人工作站又作为服务器，或者可能需要由相对非技术人员长时间操作的服务器，可能需要始终通过 init 5 命令在运行级别 5 下运行。请记住，你可以通过编辑 /etc/inittab 文件使运行级别 5 在重启后永久生效。

# 使用虚拟控制台

默认情况下，Linux 在 VGA 控制台上运行六个虚拟控制台或 TTY 会话。这些控制台由 /etc/inittab 文件中的 mingetty 语句定义。X 终端图形控制台通过使用第一个可用的、不由 mingetty 控制的 TTY 创建自己的虚拟控制台。这使得图形界面运行编号为 7：

- 你可以通过使用 Ctrl-Alt-F1 到 F6 键组合依次切换到每个虚拟控制台会话。每次尝试都会得到一个新的登录提示。
- 你可以在运行级别 5 下，或在启动 startx 后图形界面正在运行时，通过组合键 Ctrl-Alt-F7 获取图形登录界面。

# 管理 init 脚本（SysV 启动脚本）

Init 脚本决定了哪些程序在启动时启动。Red Hat 和其他 Unix 发行版具有不同的运行级别，因此每个运行级别启动的程序集也不同。通常，Red Hat Linux 在启用网络的多用户模式下启动。以下是一些可用的运行级别：

- # 0 --- 关机
- # 1 --- 单用户模式
- # 2 --- 多用户模式，无网络
- # 3 --- 完全多用户模式
- # 4 --- 未使用
- # 5 --- 完全多用户模式（带基于 X 的登录屏幕）
- # 6 --- 重启

系统引导到 /etc/inittab 中设置的默认运行级别。在 Red Hat Linux 中，默认引导级别是 3。当引导到 X-windows 登录时，默认引导级别是 5。

```text
#
#
inittab  This file describes how the INIT process should set up
#
the system in a certain run-level.
#
# Author: Miquel van
smorenburg, <miquels@sdrinkel.nl.mugnet.org>
# Modified for RHS Linux by Marc Ewing and Donnie Barnes
#
# Default runlevel. The runlevels used by RHS are:
#  0 - halt (Do NOT set initdefault to this)
#  1 - Single user mode
#  2 - Multiuser, without NFS (The same as 3, if you do not have networking)
#  3 - Full multiuser mode
#  4 - unused
#  5 - X11
#  6 - reboot (Do NOT set initdefault to this)
#
id:5:initdefault:
#System initialization.
s1::sysinit:/etc/rc.d/rc.sysinit
10:0:wait:/etc/rc.d/rc 0
1l:1:wait:/etc/rc.d/rc 1
l2:2:wait:/etc/rc.d/rc 2
l3:3:wait:/etc/rc.d/rc 3
l4:4:wait:/etc/rc.d/rc 4
l5:5:wait:/etc/rc.d/rc 5
l6:6:wait:/etc/rc.d/rc 6
# Things to run in every runlevel.
rd:once:/sbin/update

# Trap CTRL-ALT-DELETE
cal:ctrlaltdel:/sbin/shutdown -t3 -r now
# When our UPS tells us power has failed, assume we have a few minutes
# of power left. Schedule a shutdown for 2 minutes from now.
# This does, of course, assume you have powerd installed and your
# UPS connected and working correctly.
pf::powerfail:/sbin/shutdown -h +2 "Power Failure;System Shutting Down"
pr:12345:powerwait:/sbin/shutdown -c "Power Restored; Shutdown
Cancelled"
# Run gettys in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/minge2p tty6
# Runxdm in runlevel 5
#xdm is now a separate service
x:5:respawn:/etc/Xl1/prefd#-no daemon
```

让我们来讨论如何通过手动方式和使用 chkconfig 来管理 rc 脚本。

# 手动管理 rc 脚本

如果你想配置哪些服务需要在启动时启动，你需要编辑相应运行级别的 rc 脚本。如果你需要重启某个从 rc 目录启动的服务，你可以使用 restart 选项运行其启动脚本。此过程确保在服务再次启动时遵循所有正确的步骤（读取配置文件、释放锁文件等）。因此，例如，要重启 syslog，请从 rc 目录运行以下命令：

```bash
[root@netmon rc3.d]# ./Sl2syslog restart
Shutting down kernel logger: [  OK  ]
Shutting
Down system logger: [  OK  ]
Starting system logger: [  OK  ]
Starting kernel logger: [  OK  ]
```

# 使用 chkconfig 管理 rc 脚本

Red Hat Linux 有一个有用的工具叫 chkconfig，它帮助系统管理员管理 rc 脚本和 xinetd 配置文件，而无需直接操作它们。它是受 IRIX 操作系统中包含的 chkconfig 命令启发的。

输入 `chkconfig --list` 可以查看 chkconfig 知道的所有服务，以及它们在每个运行级别中是停止还是启动状态。以下是一个简化的输出示例

