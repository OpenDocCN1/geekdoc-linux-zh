
![](img/5ced0c78d748bd190e9027e5549a3622_263_0.png)

### 第 13 小时

### 更改系统状态

与个人电脑操作系统相比，Unix 的多用户、多处理能力在某些方面似乎有点陌生。最值得注意的是，你是否曾停下来考虑过在启动或关闭 Unix 系统时会发生什么？

在本小时，我们将深入系统配置，了解在切换状态时——无论是启动、停止、重启，还是在单用户和多用户模式之间切换——究竟启动和停止了哪些进程（以及如何启动和停止）。

在本小时你将学习关于

- `init` 进程及其配置文件
- 在不同运行级别启用特定服务
- 以正确的方式关闭系统

#### 配置和操作 init 进程

Unix 操作系统有多个运行级别，每个级别定义了操作系统的不同状态，以及可用的、正在运行的不同应用程序和守护进程。例如，按惯例，运行级别 0 是关机状态——处于运行级别 0 的系统已停止。

运行级别也称为 init 状态，以定义计算机这些不同运行级别的至关重要程序命名：`init`。

##### 任务 13.1：init 进程和配置

为了开始本小时，让我们深入 `init` 程序及其配置文件 `/etc/inittab` 的内部。

1. 首先，快速调用 `ps` 将确认 `init` 守护进程正在运行。这很容易，因为在每个 Unix 系统上，`init` 程序都是操作系统运行的第一个程序。因此，它始终是进程 ID 1。

在 Linux 机器上：

```
# ps -up 1
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
root 1 0.0 0.0 1412 52 ? S 00:58 0:06 init
```

在 Solaris 机器上：

```
# ps -fp 1
UID PID PPID C STIME TTY TIME CMD
root 1 0 0 Jan 26 ? 0:00 /etc/init -
```

而在 Mac OS X Darwin 机器上：

```
# ps -up 1
USER PID %CPU %MEM VSZ RSS TT STAT TIME COMMAND
root 1 0.0 0.1 1292 268 ?? SLs 0:00.00 /sbin/init
```

如果由于任何原因 `init` 程序未运行，你的系统将完全停止。

请注意，`init` 没有任何启动选项。相反，程序通过读取 `/etc/inittab` 文件来确定其配置。

2. 现在让我们暂时关注 Linux。在 Red Hat Linux 上，标准的 `/etc/inittab` 文件如下所示：

```
# cat /etc/inittab
#
#
```

```
# inittab    This file describes how the INIT process should set up
#            the system in a certain run-level.
#
# Author:    Miquel van Smoorenburg, <miquels@drinkel.nl.mugnet.org>
#            Modified for RHS Linux by Marc Ewing and Donnie Barnes
#
id:5:initdefault:

# System initialization.
si::sysinit:/etc/rc.d/rc.sysinit

l0:0:wait:/etc/rc.d/rc 0
l1:1:wait:/etc/rc.d/rc 1
l2:2:wait:/etc/rc.d/rc 2
l3:3:wait:/etc/rc.d/rc 3
l4:4:wait:/etc/rc.d/rc 4
l5:5:wait:/etc/rc.d/rc 5
l6:6:wait:/etc/rc.d/rc 6

# Things to run in every runlevel.
ud::once:/sbin/update
# Trap CTRL-ALT-DELETE
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

# When our UPS tells us power has failed, assume we have a few minutes
# of power left. Schedule a shutdown for 2 minutes from now.
# This does, of course, assume you have powerd installed and your
# UPS connected and working correctly.
pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"

# If power was restored before the shutdown kicked in, cancel it.
pr:12345:powerwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

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
```

这可能看起来令人不知所措，但 `/etc/inittab` 文件中的所有行都有相同的通用格式：

`unique ID` : `run levels` : `action` : `process`

唯一 ID : 运行级别 : 动作 : 进程

例如，唯一标识为 `inittab` 行 `x` 的最后一行仅适用于运行状态（init 级别）5，并强制以指定的 `-nodaemon` 标志重新生成 `/etc/X11/prefdm` 程序。

![](img/5ced0c78d748bd190e9027e5549a3622_266_0.png)

> `prefdm` 脚本在 X Window System 环境中管理登录屏幕。

3. 让我们在表 13.1 中定义最常见的 init 级别，并在表 13.2 中定义已知的 init 动作。

##### 表 13.1 常见的 init 级别

| 级别 | 含义 |
|---|---|
| 0 | Halt |
| 1 | Single-user mode (also called s mode on some systems) |
| 2 | Multiuser, but no remote file systems mounted; often also no networking daemons running |
| 3 | Full multiuser mode |
| 5 | Full multiuser + X11 graphics |
| 6 | Reboot |

##### 表 13.2 已定义的 init 动作

| 动作 | 含义 |
|---|---|
| boot | Process will be executed during system bootup |
| bootwait | Like boot, but init waits for completion |
| ctrlaltdel | Process will be executed when the console keyboard device driver receives a Control-Alt-Del key sequence |
| initdefault | Specifies the default run level to boot into on system boot |
| once | Like wait, but init doesn't wait for completion |
| respawn | Process is guaranteed to be running—the system will restart it if it dies |
| sysinit | Process will be executed during boot, but before any boot or bootwait entries |
