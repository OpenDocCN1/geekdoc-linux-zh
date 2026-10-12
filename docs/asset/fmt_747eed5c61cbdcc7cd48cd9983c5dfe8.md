
系统引导到 `/etc/inittab` 中设置的默认运行级别。在 Red Hat Linux 中，默认引导级别是 3。当引导到 X-windows 登录时，默认引导级别是 5。

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

让我们来讨论如何通过手动方式和使用 `chkconfig` 来管理 `rc` 脚本。

# 手动管理 `rc` 脚本

如果你想配置哪些服务需要在启动时启动，你需要编辑相应运行级别的 `rc` 脚本。如果你需要重启某个从 `rc` 目录启动的服务，你可以使用 `restart` 选项运行其启动脚本。此过程确保在服务再次启动时遵循所有正确的步骤（读取配置文件、释放锁文件等）。因此，例如，要重启 `syslog`，请从 `rc` 目录运行以下命令：

```bash
[root@netmon rc3.d]# ./Sl2syslog restart
Shutting down kernel logger: [  OK  ]
Shutting
Down system logger: [  OK  ]
Starting system logger: [  OK  ]
Starting kernel logger: [  OK  ]
```

# 使用 `chkconfig` 管理 `rc` 脚本

Red Hat Linux 有一个有用的工具叫 `chkconfig`，它帮助系统管理员管理 `rc` 脚本和 `xinetd` 配置文件，而无需直接操作它们。它是受 IRIX 操作系统中包含的 `chkconfig` 命令启发的。

输入 `chkconfig --list` 可以查看 `chkconfig` 知道的所有服务，以及它们在每个运行级别中是停止还是启动状态。以下是一个简化的输出示例

### 控制 `rcX.d` 初始化脚本

- `chkconfig`：命令行运行级别配置工具
- `ntsysv`：用于配置守护进程的全屏文本模式实用工具
- `serviceconf`：用于编辑运行级别的图形化 X 窗口实用工具

![](img/f3b9cff79e19317416c12eaf5ded7245_82_0.png)

![](img/f3b9cff79e19317416c12eaf5ded7245_83_0.png)

### `chkconfig` 示例

你可以使用 `chkconfig` 来更改特定软件包的运行级别。这里我们看到 `sendmail` 在运行级别 3 或 5 的常规启动时会启动。让我们进行更改，使 `sendmail` 在启动时不运行。

### 使用 `chkconfig` 获取 `sendmail` 当前启动选项的列表

可以将 `chkconfig` 命令与 `grep` 一起使用，以确定 `sendmail` 将在哪些运行级别中运行。这里我们看到它将在级别 3 和 5 中运行：

```
[root@netmon tmp]# chkconfig --list | grep mail
sendmail  0:off  1:off  2:off  3:on  4:off  5:on  6:off
[root@netmon tmp]#
```

### 关闭 `sendmail` 在级别 3 和 5 中的启动

带有 `--level` 开关的 `chkconfig` 命令表示需要在作为其值的运行级别中执行某些操作。命令中的第一个参数是要影响的软件包，第二个参数定义你是要开启还是关闭它。在这种情况下，我们希望 `sendmail` 在进入运行级别 3 和 5 时不启动：

```
[root@netmon tmp]# chkconfig --level 35 sendmail off
[root@netmon tmp]#
```

如果不通过 `--level` 开关指定运行级别，`chkconfig` 会自动为运行级别 3 和 5 做出更改：

```
[root@netmon tmp]# chkconfig sendmail off
```

由于意图是永久关闭 `sendmail`，我们也可能需要立即停止其运行：

```
[root@netmon tmp]# service sendmail stop
Shutting down sendmail: [  OK  ]
Shutting down sm-client: [  OK  ]
[root@netmon tmp]#
```

### 双重检查 `sendmail` 不会启动

然后我们可以使用 `chkconfig` 来双重检查我们的工作：

```
[root@netmon tmp]# chkconfig --list | grep mail
sendmail 0:off 1:off 2:off 3:off 4:off 5:off 6:off
[root@netmon tmp]#
```

### 重新开启 `sendmail`

若要重新激活 `sendmail`，我们可以再次使用 `chkconfig`，但使用 `on` 参数。再次启动 `sendmail` 以使其立即运行，而不仅仅是在下次重启后。
