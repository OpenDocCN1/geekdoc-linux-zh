
# `/etc/inittab`

```cat /etc/inittab
# inittab 此文件描述了 INIT 进程应该如何设置

# 默认运行级别。R 使用的运行级别为：

# 0 halt (不要设置 initdefault)

# 1 Single user mode (单用户模式)

# 2 Multiser, no NFS (如果没有网络，则与 3 相同)

# 3 Full multiser mode (完全多用户模式)

# 4 unused (未使用)

# 5 X11

# 6 reboot (不要将 initdefault 设置为此项)

id:5:initdefault:
```

``` 
# 系统初始化。
s::sysinit:/etc/rc.d/rc.sysinit
```

```
10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
```

```
# 捕捉 CTRL-ALT-DELETE
ca:ctrlalt:/sbin/shutdown -t3 -r now
pf:powerfail:/sbin/shutdown -f -h +2
"Power Failure; System Shutting Down",
```

```
# 如果在关机启动前恢复电源，则取消。
pr:12345:powerorkit:/sbin/shutdown -c
"Power Restored; Shutdown Cancelled",
```

```
# 在标准运行级别运行 getty
1:2345:respawn:/sbin/mintty tty1
2:2345:respawn:/sbin/mintty tty2
3:2345:respawn:/sbin/mintty tty3
4:2345:respawn:/sbin/mintty tty4
5:2345:respawn:/sbin/mintty tty5
6:2345:respawn:/sbin/mintty tty6
```

```
# 在运行级别 5 运行 xdm
x:5:respawn:/etc/X11/prefdm -nodaemon
```

`/etc/inittab` 文件告诉 `init` 守护进程哪个运行级别是默认运行级别。运行级别（Runlevel）是一个决定启动哪些服务和停止哪些服务的分类数字。在前面的示例中，通过 `id:5:initdefault:` 这一行设置了默认运行级别 5。表 15.1 显示了标准的 Linux 运行级别。

## 表 15.1 标准的 Linux 运行级别

| 运行级别 | 名称 | 描述 |
|---|---|---|
| 0 | | 所有服务关闭，服务器停止。 |
| 1 or s | 单用户模式 | `root` 账户自动登录到服务器。其他用户无法登录。只有命令行界面可用。不启动网络服务。 |
| 2 | 多用户模式 | 用户可以登录服务器，但只有命令行界面可用。在某些系统上，网络接口和服务集会启动；其他系统则不会。最初，此运行级别用于启动虚拟设备以便使用户登录（但不会启动网络服务）。 |
| 3 | 扩展多用户模式 | 用户可以登录服务器，但只有命令行界面可用。网络接口和服务集会启动。这是服务器常用的运行级别。 |
| 4 | 用户自定义 | 用户可以自定义此运行级别。 |
| 5 | 图形化模式 | 用户可以登录服务器。命令行和图形界面均可用。启动网络服务。这是桌面系统常用的运行级别。 |
| 6 | 重启 | 服务器重启。 |

不同的 Linux 发行版在每个运行级别的定义以及提供的提供的运行级别上可能略有不同。例如，Ubuntu 发行版提供了运行级别 0–6 级别，但运行级别 2–5 启动的服务与表 15.1 中的运行级别 5 相同。

> 注意
> 在 `/etc/inittab` 文件中应该使用的运行级别仅为 2 到 5。其他运行级别可能会导致问题。例如，如果你将运行级别 6 设置为 `/etc/inittab` 文件中的默认值，当服务器重启时，它将进入循环并不断重启。

运行级别不仅用作 `/etc/inittab` 文件中的默认运行级别。它们也可以直接通过 `init` 守护进程本身调用。因此，如果你想立即停止服务器，可以在命令行中输入 `init 0`：

```
# init 0
System going down!
```

# 第 15 章：启动服务

`init` 命令接受表 15.1 中的任何运行级别数字，允许你将服务器从一个运行级别切换到另一个。例如，如果需要启动图形界面，可以执行 `init 5`：

```
# init 5
INIT: Starting...
```

运行级别不仅用作 `/etc/inittab` 文件中的默认运行级别。它们也可以直接通过 `init` 守护进程本身调用。因此，如果你想立即停止服务器，可以在命令行中输入 `init 0`：

```
# init 0
System going down!
```

# 第四部分：成为 Linux 服务器管理员

```. /etc/rc.d/init.d/functions

...

# 查看我们是如何被调用的。
case "$1" in
  start)
    start
  stop)
    stop
  status)
    status $httpd
    RETVAL=$?
esac
exit $RETVAL
```

执行完相应的 `/etc/rc.d/rc#` 目录下的运行级别脚本后，SysInit 守护进程的进程创建即告完成。此时的最后步骤是执行 `/etc/initab` 文件中指示的其他任何操作（例如，为虚拟控制台生成 `getty` 进程，如果你处于 5 级别，则启动桌面界面）。

# 理解 Upstart 守护进程基础

如前所述，许多 Linux 发行版在很一段时间内从经典的 `init` 守护进程迁移到了 Upstart 守护进程。这些发行版列表包括 RHEL 6 和 Ubuntu（15.04 之前的版本）。

经典 `init` 与 Upstart 之间的主要区别在于处理停止和启动服务的方式。SysInit 守护进程是为了在静态环境中运行而创建的，而 Upstart 守护进程是为了在灵活且不断变化的环境运行而创建的。

在 SysInit 中，服务根据运行级别（runlevels）进行停止和启动。Upstart `init` 守护进程并不关注运行级别，而是关注系统事件。事件决定了服务何时启动和/或停止。

事件是 Linux 服务器上触发必要的系统状态更改的发生情况，并会通信给 Upstart `init` 守护进程。以下是系统事件的示例：

- 服务器启动。
- 使用了 `init` 命令。
- USB 设备插入服务器。

# 第 15 章：启动和停止服务

经典的 `init` 守护进程可以处理前两个事件示例，但无法很好地处理第三种。

Upstart 通过定义的作业（jobs）处理服务。一个 Upstart 作业可以是一个任务（task），也可以是一个服务（service）。任务执行有限的职责，完成工作后返回等待状态。相比之下，服务是一个长时间运行的进程，它永远不会完成工作或自终止，而是保持在运行状态。守护进程（daemon）就是 Upstart 作业服务的示例。

接下来的示例显示了包含任务作业和服务作业的多个 Upstart 作业。任务作业处于启动/等待状态，例如任务 `rc`。服务作业处于启动/运行状态，例如 `cups` 守护进程。

```
$ initctl list
avahi-daemon start/running, process 456
mountall-net stop/waiting
rc stop/waiting
rsyslog start/running, process 411
...
sh start/running, process 405
uudev-fallback-graphics stop/waiting
control-alt-delete stop/waiting
hwclock stop/waiting
mounted-proc stop/waiting
network-manager start/running, process 458
...
rc-sysinit stop/waiting
cups start/running, process 1066
...
tty6 start/running, process 833
ureadahead stop/waiting
```

这些不同的作业通过作业定义文件定义。所有的作业定义文件都位于 `/etc/init` 目录，所示：

```
$ ls /etc/init
networking.conf
acpid.conf
network-interface.conf
alsa-restore.conf
```
