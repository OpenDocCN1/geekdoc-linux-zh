

## 单用户模式与运行级别

处于单用户模式时，`runlevel` 命令会显示当前运行级别为 S（单用户模式），最近一次运行级别为 1（单用户模式）；然而，当运行级别切换回运行级别 5 时，如下面的输出所示，`runlevel` 命令会正确显示当前和最近的运行级别。

```
sh-2.05b# init 5
INIT: Switching to runlevel: 5
INIT: Sending processes the TERM signal
INIT: Sending processes the KILL signal

*系统在进入运行级别 5 期间，由 init 守护进程启动的一组守护进程列表。*

[root@server1 root]# runlevel
S 5
[root@server1 root]#
```

**注意**

**telinit** 命令是 **init** 命令的快捷方式；因此，可以使用命令 `telinit 1` 来切换到单用户模式。

### /etc/inittab 文件

当 init 守护进程需要通过启动或停止守护进程来更改系统运行级别时，它会查询 /etc/inittab 文件。在启动时将系统引导至特定运行级别时，也会查询此文件。下面是一个 /etc/inittab 的示例：

```bash
[root@server1 root]# cat /etc/inittab

#
# inittab          This file describes how the INIT process should set up
#                  the system in a certain run-level.
#
# Author:          Miquel van Smoorenburg, <MiquelS@drinkel.nl.mugnet.org>
#                  Modified for RHS Linux by Marc Ewing and Donnie Barnes
#
# Default runlevel. The runlevels used by RHS are:
#   0 - halt (Do NOT set initdefault to this)
#   1 - Single user mode
#   2 - Multiuser, without NFS (The same as 3, if you do not have networking)
#   3 - Full multiuser mode
#   4 - unused
#   5 - X11
#   6 - reboot (Do NOT set initdefault to this)

id:5:initdefault:

# System initialization.
si::sysinit:/etc/rc.d/rc.sysinit

# Boot-time settings.
l0:0:wait:/etc/rc.d/rc 0
l1:1:wait:/etc/rc.d/rc 1
l2:2:wait:/etc/rc.d/rc 2
l3:3:wait:/etc/rc.d/rc 3
l4:4:wait:/etc/rc.d/rc 4
l5:5:wait:/etc/rc.d/rc 5
l6:6:wait:/etc/rc.d/rc 6

# Trap CTRL-ALT-DELETE
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

# When our UPS tells us power has failed, assume we have a few minutes
# of power left. Schedule a shutdown for 2 minutes from now.
# This does, of course, assume you have power installed and your
# UPS connected and working correctly.
pf::powerfail:/sbin/shutdown -f h +2 "Power Failure; System Shutting Down"

# If power was restored before the shutdown kicked in, cancel it.
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

# Run gettys in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6

# Run xdm in runlevel 5
x:5:respawn:/etc/X11/prefdm -nodaemon

[root@server1 root]#
```

**注意**

在系统位于 LILO 启动提示符时，您也可以启动到特定的运行级别；只需输入 Linux 映像名称后跟随 1、S、s 或 single 即可。

/etc/inittab 文件中条目的格式如下：

`标签 : 运行级别 : 操作 : 命令`

标签只是一个标识符，允许 init 守护进程按字母顺序检查此文件；运行级别指定 /etc/inittab 中该行对应的运行级别；命令告诉 init 守护进程在进入运行级别时要执行什么；操作告诉 init 守护进程如何执行该命令。

因此，/etc/inittab 文件中的行 `id:5:initdefault:` 告诉 init 守护进程，在系统启动初始化 Linux 系统时，运行级别 5 是默认的引导运行级别。此外，`si::sysinit:/etc/rc.d/rc.sysinit` 行告诉 init 守护进程在系统初始化时进入运行级别之前运行程序 /etc/rc.d/rc.sysinit。该程序初始化系统的硬件组件，设置环境变量（如 PATH 和 HOSTNAME），检查文件系统，并执行守护进程加载所需的系统任务。/etc/rc.d/rc.sysinit 程序的输出会在图形化启动开始后立即显示在终端屏幕上；只需在图形化启动屏幕上点击“显示详细信息”即可查看各项操作。

由于默认运行级别是 5，因此在之前看到的 /etc/inittab 文件的下一部分中，只有行 `l5:5:wait:/etc/rc.d/rc 5` 会被执行。该行执行 /etc/rc.d/rc 5 命令，并在继续执行 /etc/inittab 文件的其余部分之前等待其完成。/etc/rc.d/rc 5 命令执行 /etc/rc.d/rc5.d/ 目录中所有以 S 或 K 开头的文件。该目录中的每个文件都是指向启动特定守护进程的脚本的符号链接，并且这些文件按字母顺序执行；S 或 K 分别表示在进入此运行级别时是启动（Start）还是终止（Kill）守护进程。/etc/rc.d/rc5.d 目录中的一些示例内容如下面的输出所示：

```
[root@server1 root]# ls /etc/rc.d/rc5.d
K01yum            K35cyrus-imapd  K84ospfd        S26apmd
K05innd           K35dhcpd         K84ospfd        S28autofs
K05sathd          K35mb            K84ripd         S40smartd
K10dc_server      K35vncserver     K84ripngd       S44ccpidd
K10ospect         K361isa          K85zebra        S54pnpd
K10rdadusd        K45arwatchd      K89netplugd     S55cups
K12dc_client      K45named         K901sccmd       S55sshd
K12mailman        K46rgadvd        K921sysadm      S56rdevdevices
K15mysql          K50netdump       S00mircocode_ctl S56knetd
K159krel1md       K50smpd          S01sysstat      S80sendmail
K15httd           K50snnmctrpd     S04readhead_early S80spamassassin
K15postqrsq       K505ux           S01sysstat      S84privoxy
K16qrapd          K50vsftp         S06cpuspeed     S85pmm
K20bootparamd     K540devco        S081bootpabled  S8711im
K205ccls          K55outed         S081ptables     S90canna
K20netdump-server K611dgp          S091snd         S90cron
K20nfs            K651dend         S10network      S90FreeWnn
K20rsatd          K65kadmind       S12syslog       S90xf
K20usersd         K65krop          S131portbalance S95asamcron
K20rwalld         K65krb524        S13portmap      S95atd
K20whod           K65krb5dc        S14nflock       S96readahead
K20tomcat         K70aep1000       S19pcpgssd      S97mesagebus
K24irda           K70bcm5B20       S19rpcbind      S97rnsd
K25squad          K74nupd          S19rpcsvcgvssd  S99local
K28amd            K74ups           S20rgmand       S99dmonitor1d
K34hcrelay        K74ypeserv       S24csmcia       S999dmtd
K34ypasssswd      K74xypfrd        S25bluetooth
K35atalik         K84bgpd          S25ntfs
K35atalik         K84bgpd          S25ntfs
[root@server1 root]#
```

根据前面的输出，您可以看到 init 守护进程在进入此运行级别时将启动 cron 守护进程（S90cron），如果内存中存在 1dapd 守护进程（K611dap），则将其终止。此外，前面目录中的文件按字母顺序执行；文件 K651dend 在文件 K65kadmind 之前执行。

请记住，运行级别 1（单用户模式）仅包含足够让单个用户登录并执行系统任务的守护进程；如果用户使用 `init 1` 命令发现 init 守护进程更改为此运行级别，init 守护进程会在 /etc/inittab 中找到相应的条目（`l1:1:wait:/etc/rc.d/rc 1`），并执行 /etc/rc.d/rc1.d 目录中所有以 S 或 K 开头的文件。由于单用户模式下启动的守护进程较少，该目录中的大多数文件都以 K 开头：

```
[root@server1 root]# ls /etc/rc.d/rc1.d
K01yum K20statd K50vsftpd K84ospfd
K03messagesbug K20usersd K50xinetd K84rjpd
K03rhnsd K20wiald K54devcot K84rijngd
K05anacron K20rwhod K56reoute K85zebra
K05atd K20tomcat K56acpid K86ifsqos
K05innnd K24irda K60crond K87rnplance
K05saslauthd K25squid K61hpj3 K87portmap
K09privoxy K25sshd K61ldap K88syslog
K10cups K28amd K65ident K89netplugd
K10dc_server K30sendmail K65admin K90bluetooth
K10psacct K30pamassassin K65kprop K901scom
K10radiusd K34ncrelay K65krb524 K90network
K10xfs K34ypasssswd K65krb5kdc K91lsdn
K12canma K35atalk K68rpcgssd K921ptable
K12dc_client K35cyrus-imapd K692imapd K921ptables
K12FreeWin K35dhcpd K69rpcsvcgssd K921pvsnm
K12mailman K35smb K7000100 K95kduz
K12mysq1d K35vncserver K70bcms820 K96pcmcia
K15kernelmod K361isa K72autofs K99dmodmon
K15pgp K40smartd K74apmd K99dmcpd
K15httpd K44rawdevices K74ntpd K99miscodoc_dctrl
K15postgresql K45erwatch K74ups K99readahead
K16arpd K45named K745pserv K99readahead_early
K1711m K46radvd K74yp K501single
K20bootparam K50netdump K75netfs S011sysd
K201scsi K50smpd K80random S06cpuspeed
K20netdump-server K50smptrapd K840bgpd
K20nfs K501ux K84ospfd
[root@server1 root]#
```

大多数在系统启动时加载的守护进程是从 `/etc/inittab` 中的条目执行的，这些条目在系统启动时运行 `/etc/rc.d/rc` 命令，从适当的 `/etc/rc.d/rc*.d` 目录中以 S 开头的文件加载守护进程（其中 `*` 指代默认运行级别）。与 `/etc/rc.d/rc.sysinit` 程序一样，启动时的消息会指示 `/etc/rc/rc*.d` 目录中的每个文件是否成功加载。此列表中的一部分如下所示：

```
Starting up APM daemon: [ OK ]
Starting automount: No Mountpoints Defined [ OK ]
Starting xinetd: [ OK ]
Starting sendmail: [ OK ]
Starting console mouse services: [ OK ]
```

