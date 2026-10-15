
OpenBoot 3.10.25, 512 MB memory installed, Serial #14242136.

Ethernet address 8:0.20:d9:51:58, Host ID: 80d95158.

Executing last command: `boot -s`

Boot device: `/pcci01f/0/pcci01l/02/disk0:a` File and args: `-s`

SunOS Release 5.8 Version Generic_08528-03 64-bit

Copyright 1983-2000 Microsystems, Inc. All rights reserved.

configuring IPv4 interfaces: `hme0`.

hostname: `dino`

```
> 重启后，系统执行用于单用户模式的 -s 选项
```

`INIT: SINGLE USER MODE` ←

输入 `control-d` 以继续正常启动，
(或为系统维护提供密码): ←

```
> 系统处于单用户模式的通知
> 系统的 root 密码提示
```

当系统被置于单用户模式时，系统会提示 `root` 密码。在 Linux 或 HP-UX 系统上运行时，上述输出是类似的。然而，Linux 的 `reboot` 命令不支持 `-s` 选项，无法将额外的命令行选项传递给引导加载程序。可以使用以下命令重启系统：

```bash
init 6
```

再次，当系统有活动用户时，这并不是重启系统的首选方法。

# 正常系统关机

当系统处于多用户模式时，用户已登录系统并正在进行工作；关闭系统的最佳方法是使用 `shutdown` 命令。该命令允许用户在未来的某个时间点调度关机，并知道系统何时变得不可用。此外，`shutdown` 命令可以包含有关系统即将关闭的警告消息或信息。例如，假设系统必须在一小时后进行某些磁盘维护。在 Solaris 和 HP-UX 上，使用此命令：

```bash
shutdown -g 3600 "###### Down for Disk Maintenance: System back in two hours ####"
```

`-g` 选项用于指示命令在执行关机操作前等待指定的秒数。在本例中，`3600` 代表一小时。

### 提示

在实践中，管理员关机系统时应给予比一小时更多的时间。。但是，如果维护任务非常重要必须立即执行——例如修复磁盘故障——则无法进行待关机。每个登录系统的用户都会收到待关机通知。当首次执行 `shutdown` 命令时，会向系统中的所有用户发送如下消息：

```
Broadcast from root (console) Feb 3 15:23:55
The system will be down in 1 hour
###### Down for Disk Maintenance: System back in two hours ####
```

`-g` 选项用于指示命令在执行关机操作前等待指定的秒数。在本例中，`3600` 代表一小时。

# 258 UNIX 系统管理：入门指南

系统启动和关机期间的进程。此外，当系统管理员修改此文件时，`init` 进程可以在需要时重新读取该文件。Solaris、HP-UX 和 Linux 的 `/etc/inittab` 在语法和内容上存在巨大差异。换句话说，为它们各个运行级别（run levels）启动的服务程序是不同的，但该文件的基本结构是相同的。

在 Solaris 上，`/etc/inittab` 文件包含以下：

```
1 ap::sysinit:/sbin/autopush -f /etc/iu.ap
2 ap::sysinit:/sbin/sconfig -f /etc/sock2path
3 fs::sysinit:/sbin/rc5 >/dev/msglog 2</console>
4 15:3initdefault
5 p3:s1234:powerfail:/usr/sbin/shutdown -y -i5 -g0 >/dev/msglog 2</dev/msglog
6 s6:s:wait:/sbin/rc >/dev/msglog 2</console>
7 s0:wait:/sbin/rc0 >/dev/msglog 2</console>
8 s1:respawn:/sbin/rc1 >/dev/msglog 2</console>
9 s23:wait:/sbin/rc2 >/dev/msglog 2</console>
10 s3:wait:/sbin/rc3 >/dev/msglog 2</console>
11 s5:wait:/sbin/rc5 >/dev/msglog 2</console>
12 s6:wait:/sbin/rc6 >/dev/msglog 2</console>
13 fw:0:wait:/sbin/uadmin 20 >/dev/msglog 2</console>
14 of:5:wait:/sbin/uadmin 6 >/dev/msglog 2</console>
15 rb:6:wait:/sbin/uadmin 2 1 >/dev/msglog 2</console>
16 sc:24:respawn:/usr/lib/sac -t 300
co:24:respawn:/usr/lib/ttymon -g -h -p "name -n' console login: "-T suncolor -d /dev/console -1 -m ldterm,ttcompat
```

在 Linux 上，`/etc/inittab` 文件包含以下：

```
1 id:5:initdefault
2
3 # 系统初始化。
4 si::sysinit:/etc/rc.d/rc.sysinit
5
10:0:wait:/etc/rc.d/rc 0
```

![](img/2928fe42a92e6fb43bbbe3768008092f_278_0.png)

# 第 9 节：系统操作 259

```
7 11:wait:/etc/rc.d/rc 1
8 12:wait:/etc/rc.d/rc 2
9 13:wait:/etc/rc.d/rc 3
10 14:wait:/etc/rc.d/rc 4
11 15:wait:/etc/rc.d/rc 5
12 16:wait:/etc/rc.d/rc 6
13
14 # 在每个运行级别下运行的项目。
15 ud:once:/sbin/update
16
17 # 捕获 CTRL-ALT-DELETE
18 shutdown -cctrldel:/sbin/shutdown -t3 -r now
19
20 pf:powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"
21
22 # 如果关机启动之前恢复了电源，则取消。
23 pr:12345:powerokwat:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"
24
25 在标准运行级别运行 getty
26 1:2345:respawn:/sbin/mingetty tty1
27 2:2345:respawn:/sbin/mingetty tty2
28 3:2345:respawn:/sbin/mingetty tty3
29 4:2345:respawn:/sbin/mingetty tty4
30 5:2345:respawn:/sbin/mingetty tty5
31 6:2345:respawn:/sbin/mingetty tty6
32
33 # 在运行级别 5 中运行 xdm
34 # xdm 现在是一个独立的服务
5:respawn:/etc/inittab
```
