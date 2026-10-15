
您可以选择使用 Windows 启动加载程序加载 Linux 操作系统；只需在 Windows 启动加载程序配置中指定 `GRUB` 或 `LILO` 的位置即可。类似于 `LILO` 和 `GRUB`，适用于 Windows NT、Windows 2000、Windows XP 和 Windows Server 2003 自带的 `NTLOADER` 启动加载器可以在启动时显示屏幕，提示用户选择操作系统。因此，如果 Windows NT、Windows 2000、Windows XP 或 Windows Server 2003 与 Linux 双启动，您可以使用 Windows `NTLOADER` 启动加载器来加载 `LILO` 或 `GRUB`。

# 启动加载器

您必须确保系统首先安装了 Windows NT、Windows 2000、Windows XP 或 Windows Server 2003，并将其位于系统的第一个活动分区上；`NTLOADER` 启动加载器默认放置在硬盘的 MBR 上。接下来，您可以安装 Linux 并指定将 `GRUB` 安装在分区的扇扇而不是 MBR 上，如图 9-7 所示；否则，`GRUB` 将覆盖硬盘 MBR 上的 `NTLOADER`。

**图 9-7** 配置 `GRUB` 位于 Linux 分区

成功安装 Linux 后，再次使用第一张 Red Hat Fedora CD-ROM 启动计算机。在欢迎界面，在 `boot:` 提示符处输入 `linux` 并按 Enter。接着，在“语言和键盘类型选择”处点击 OK，在“设置网络”屏幕处选择 No，在“救援”屏幕处选择 Continue（继续）。当系统提示硬盘上 Linux 安装的根文件系统已挂载到 `/mnt/sysimage` 时，点击 OK，您将获得命令提示符。

接下来，您在软磁盘上创建一个目录（`mkdir /mnt/floppy`），将格式化为 FAT 文件系统的软磁盘放入软磁盘驱动器，并挂载您的软磁盘（`mount -t vfat /dev/fd0 /mnt/floppy`）。

然后您可以创建 `GRUB` 的可启动镜像。假设 `GRUB` 已安装在 `/` 分区 `/dev/hda2` 的第一个扇区；为了在 `/` 分区 `/dev/hda2` 上创建 `GRUB` 镜像，可以使用以下命令：

```bash
[root@server1 root]# mkdir /mnt/floppy
[root@server1 root]# mount -t vfat /dev/fd0 /mnt/floppy
[root@server1 root]# dd if=/dev/hda2 of=/mnt/floppy/grub.img bs=512 count=1
```

## LINUX 初始化

由于 `init` 守护进程负责启动和停止守护进程，从而更改运行级别（`runlevels`），运行级别通常被称为初始化状态（`initstates`）。在任何时候，系统可能处于七种运行级别之一；这些级别定义在表 9-3。

### 表 9-3 运行级别

| 运行级别 | 名称 | 描述 |

| :--- | :--- | :--- |

| 0 | 停机 | 无活动守护进程，准备关闭电源。 |

| 1 | 单用户模式 | 系统只有足够的守护进程允许一个用户登录并进行系统维护。进入单用户模式时会自动以 root 用户登录。 |

| 2 | 多用户模式 | 系统启动了大部分守护进程，允许多个用户登录并使用服务。除了特殊网络服务外，大多数网络服务在此级别均可用。 |

| 3 | 扩展多用户模式 | 系统与多用户模式相同，但启动了所有网络服务（例如 SNMP, NFS）。 |

| 4 | 未使用 | 通常不使用，但可以根据需要进行自定义。 |

| 5 | 图形模式 | 系统与扩展多用户模式相同，但在 tty7 上启动了名为 GNOME 显示管理器 (`gdm`) 的图形登录程序，允许图形登录。 |

| 6 | 重启 | 用于重启系统的特殊运行级别。 |

要查看系统当前的运行级别以及之前的运行级别（如果自系统启动以来运行级别发生了变化），可以使用 `runlevel` 命令，输出所示：

```
[root@server1 root]# runlevel
 5
[root@server1 root]#
```

之前的运行级别表示系统当前处于运行级别 5，且在此级别之前的最近一个运行级别不存在（N）。

要在运行的系统中更改运行级别，只需指定 `init` 命令后跟新的运行级别；若要从运行级别 5 更改到运行级别 1 执行系统维护任务，可以使用以下命令：

```bash
[root@server1 root]# init 1
```

# LINUX 初始化

```
[root@server root]# runlevel
5
[root@server root]# init 1
INIT: Switching to runlevel: 1
INIT: Sending processes the TERM signal
```

*当系统进入单用户模式时，`init` 守护进程正在停止的守护进程列表。*

告知 `INIT` 进入单用户模式。

INIT: Going single user

INIT: Sending processes the TERM signal

INIT: Sending processes the KILL signal

```
sh-2.05b# runlevel
1 S
sh-2.05b# 
```

# LINUX 初始化

## 注意事项

`telinit` 命令是 `init` 命令的快捷方式；因此，可以使用 `telinit 1` 命令来切换到单用户模式（Single User Mode）。

在单用户模式下，`runlevel` 命令会对当前运行级别显示 S（单用户模式），对最近一次的运行级别显示 1（单用户模式）；然而，当将运行级别更改为 `runlevel 5` 时（如下输出所示），`runlevel` 命令会正确显示当前和最近一次的运行级别。

```
sh-2.05b# init 5
INIT: Switching to runlevel: 5
INIT: Sending processes the TERM signal
INIT: Sending processes the KILL signal
```

*当系统进入运行级别 5 时，`init` 守护进程正在启动的守护进程列表。*

```
[root@server root]# runlevel
5 S
[root@server root]# 
```

# 第 9 章 系统初始化与 X Window

> 注意

> 当系统处于 `LILO` 启动提示符时，可以启动到特定的运行级别，只需输入 Linux 镜像名称后跟 I、S、s 或 `single` 即可。

### /etc/inittab 文件

`init` 守护进程需要通过启动或停止守护进程来更改系统的运行级别，它会查询 `/etc/inittab` 文件。在启动时将系统带到特定的运行级别时也会查询该文件。以下是 `/etc/inittab` 的一个示例：

```
[root@server1 root]# cat /etc/inittab
#
#### inittab
    此文件描述了 INIT 进程如何在
    在特定的运行级别下设置系统。
#
# Author: Miquel van Smorenburg, <miquel@drinkel.nl.mugnet.org>
    由 Marc Ewing 和 Donnie Barnes 为 RHS Linux 修改
#
# 默认运行级别。RHS 使用的运行级别为：
# 0 - 停止（不要将 initdefault 设置为此值）
#### 1 - 单用户模式
# 2 - 多用户模式，无 NFS（如果你没有网络，则与 3 相同）
#### 3 - 全多用户模式
#### 4 - 未使用
#### 5 - X11
# 6 - 重启（不要将 initdefault 设置为此值）

id:5:initdefault:

# 系统初始化。
si::wait:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6

# 捕捉 CTRL-ALT-DELETE
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

# 当我们的 UPS 我们断电时，假设我们还有几分钟
# 电。安排在 2 分钟后关机。
# 当然，这假设你安装了电源并且你的
# UPS 连接并正常工作。
pf::powerfail:/sbin/shutdown -f -h2 "Power Failure; System Shutting Down"

# 如果在启动之前电源恢复，则取消。
pr:12345:powerok:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

# 在标准运行级别下运行 getty
1:22345:respawn:/sbin/mingtty tty1
2:2345:respawn:/sbin/mingtty tty2
3:2345:respawn:/sbin/mingtty tty3
4:2345:respawn:/sbin/mingtty tty4
5:2345:respawn:/sbin/mingtty tty5
6:2345:respawn:/sbin/mingtty tty6

# 在运行级别 5 下运行 xdm
x5:respawn:/etc/X11/prefd -nodaemon
```

`/etc/inittab` 文件中条目的格式如下：

`label : runlevel(s) : action : command`

`label`（标签）是一个标识符，允许 `init` 守护进程按字母顺序检查此文件；`runlevel`（运行级别）指定 `/etc/inittab` 中该行对应的运行级别；`command`（命令）告诉 `init` 守护进程在进入运行级别时执行什么；`action`（动作）告诉 `init` 守护进程如何执行该命令。

因此，`id:5:initdefault:` `/etc/inittab` 文件告诉 `init` 守护进程，在系统启动时初始化 Linux 系统时，5 是默认的运行级别。此外，`si:sysinit:/etc/rc/rc.sysinit` 行告诉 `init` 守护进程在进入系统初始化运行级别之前运行 `/etc/rc/rc.sysinit` 程序。该程序初始化系统的硬件组件，设置如 `PATH` 和 `HOSTNAME` 等环境变量，检查文件系统，并执行系统任务。`/etc/rc/rc.sysinit` 的输出在系统启动期间显示在终端屏幕上；只需点击 Details 查看详情。由于默认运行级别是 5，只有 `15:5:wait:/etc/rc/rc.d 5` 会在 `/etc/inittab` 文件的后续部分执行。`/etc/rc.rc5` 执行所有以 S 或 K 开头的文件，该目录中的每个文件都是指向启动特定守护进程的脚本的符号链接，且这些文件按字母顺序执行；S 或 K 表示在进入此运行级别时对应的启动或杀死该守护进程。以下是 `/etc/rc5.d` 目录的一些示例内容：

```
[root@server1]# ls /etc/rc5.d
K0yum K35cyrus-im K84bspf S26amprof
K05indi K35dchcp K84osspf S28autofs
K05saslas K35mbd K48ripid S40smartmd
K10dc_client K35vncserver K48riping S44acpid
K10spaccs K36li14 K852 S54hpoj
K10radius K45parwych K89netpug S55cups
K12dc_client K45named K901cis S55sshd
K12mailman K46radvd K92ysidam S56redraw
K12mysqld K50netdump S01sysystat
K15grelmd K50snmpradt S04readahead S80sendmail
K15htpped K500tux S80spassin
K15postgresql K50vsftd S05kuz S84privry
K16rard K51dceed S06pus S85gpom
K20bootparam K54dovect S07iptables S87liim
K20iscci K55routed S08iptables S90canna
K21dildap S09isdn S90crond
K20netdum-server K61lldap S10network
K20nfs K65ident S12syslog S90xfs
K20rstad K65kadmin S13irq S95acron
K20rusers K65krop S13portman S95atd
K20wald K65krbs24 S14nflock S96readahead
K20whrod K655cd S18rpcpgssd S97messagebau
K20tomcat K70ae1003 S19rpccssd S97rnhsd
K24irda K70pcm8520 S19rpcgssd S99local
K25quid K74ntpd S20random S99monitor
K28amd K74ups S24pcmcmia S99dmp
K34dchrelay K74ypvers S25blueeto S99d
K34ypsapp K74xypprd S25netflix
K35atalk K84bgpd
```

从前面的输出可以看出，`init` 守护进程在进入此运行级别时将启动 `cron` 守护进程（`S90crond`），如果 `ldap` 守护进程（`K61ldap`）存在则杀死它。此外，前面目录中的文件按字母顺序执行；`K65identd` 在 `K65kadmin` 文件之前执行。回运行级别 1（单用户模式）仅供单个用户执行系统任务的守护进程；如果用户使用 `init` 命令通过 `init` 守护进程切换到此运行级别，`init` 守护进程会在 `/etc/init` 中找到相应的条目（`11:1:wait:/etc/rc.d/rc`），并继续执行 `/etc/rc.d/rc.d1` 中以 S 或 K 开头的文件。由于单用户模式启动的守护进程很少，该目录中的大多数文件以 K 开头：

```
[root@server1]# ls /etc/rc.d/rc1.d

K0yum K20rast K50vsftpd K84osfpfd

K03messagebus K20rusers K50xinetd K84ripd

K03rhnsd K20rwall K54dovec K84ripngd

K05ancron K20rwhod K55routed K84zebra

K05atd K20rwhod K56acpid K86nfslock

K05indi K20tomcat K60crond K87irqbalance

K05saslauth K24irda K61hopoj K87portmap

K09privoxy K25squid K61dailap K88syslog

K10dc_server K30sendmail K65identd K89netplug

K10psacct K30passassin K65kprop K90is

K10radius K34crelay K65krb24 K90xfs

K10xfs K34myapp K65krb5 K91is

K12canna K35atalk K68rpcssd K92iptables

K12_client K35dhcpd K69pmadcd K92iptables

K12FreeWeinn K35smbd K70ae1000 K92ipsvad

K12mailman K36lisa K70bcm5820 K95kudu

K12mysqld K35svcnerver K72autofs K96pcmcia

K15grekillmd K40smartd K79ymmonitor 99monitor

K15gpm K44rawdevices K74ntpd 99microcode_ctl

K15httpd K45as K74ntpd 99readahead

K15postgresql K45parch K74ups

K16rarpd K46radvad K74xpyverser 99readahead_early

K17ilim K47as K75xpyfyd S00single

K20bootparam K50netumpd S75netfs S01sysstat

K20iscsi K50snmpd S80random S06cpuspeed

K20netumpd-server K50snptrad K84bbgpd
```
