
## 答案

- 1. 软限制是用户在没有任何警告的情况下可以消耗的最大磁盘空间量。当他们超出软限制时，系统会抱怨但仍允许他们继续。硬限制是不可违抗的约束，系统将拒绝用户添加新文件甚至扩大文件的尝试。
- 2. 第一步是编辑 /etc/fstab（或 Solaris 上的 vfstab）以在挂载时启用配额。
- 3. 一个主要限制是配额系统不跨多个文件系统，因此虽然可以限制用户每个设备的特定空间量，但没有内置机制来限制整体磁盘使用。
- 4. wall 命令允许你向当时登录的每个用户发送即时消息。
- 5. 如果你启用配额，在每个用户的 .login 或 .bash_profile 中添加对 quota（或根据需要 quota -v）的调用是非常明智的做法。

在下一小时，我们将转换思路并开始查看进程和系统控制。我们将重点关注 Unix 系统的启动和关闭，包括对运行级别和 init 状态的广泛讨论。这是任何系统管理员必读的内容！

![](img/5ced0c78d748bd190e9027e5549a3622_261_0.png)

## 第五部分

## 进程与系统控制

## 小时

- 13 更改系统状态 247
- 14 探索进程 265
- 15 将作业运行在未来 285
- 16 管理你的日志文件 301

![](img/5ced0c78d748bd190e9027e5549a3622_263_0.png)

## 第 13 小时

## 更改系统状态

与个人电脑操作系统相比，Unix 的多用户、多处理能力在某些方面似乎有点陌生。最值得注意的是，你是否曾停下来考虑过在启动或关闭 Unix 系统时会发生什么？

在本小时，我们将深入系统配置，了解在切换状态时——无论是启动、停止、重启，还是在单用户和多用户模式之间切换——究竟启动和停止了哪些进程（以及如何启动和停止）。

在本小时你将学习关于

- init 进程及其配置文件
- 在不同运行级别启用特定服务
- 以正确的方式关闭系统

## 配置和操作 init 进程

Unix 操作系统有多个运行级别，每个级别定义了操作系统的不同状态，以及可用的、正在运行的不同应用程序和守护进程。例如，按惯例，运行级别 0 是关机状态——处于运行级别 0 的系统已停止。

运行级别也称为 init 状态，以定义计算机这些不同运行级别的至关重要程序命名：init。

### 任务 13.1：init 进程和配置

为了开始本小时，让我们深入 init 程序及其配置文件 /etc/inittab 的内部。

1. 首先，快速调用 ps 将确认 init 守护进程正在运行。这很容易，因为在每个 Unix 系统上，init 程序都是操作系统运行的第一个程序。因此，它始终是进程 ID 1。

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

如果由于任何原因 init 程序未运行，你的系统将完全停止。

请注意，init 没有任何启动选项。相反，程序通过读取 /etc/inittab 文件来确定其配置。

2. 现在让我们暂时关注 Linux。在 Red Hat Linux 上，标准的 /etc/inittab 文件如下所示：

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

这可能看起来令人不知所措，但 /etc/inittab 文件中的所有行都有相同的通用格式：

unique ID : run levels : action : process

唯一 ID : 运行级别 : 动作 : 进程

例如，唯一标识为 inittab 行 x 的最后一行仅适用于运行状态（init 级别）5，并强制以指定的 -nodaemon 标志重新生成 /etc/X11/prefdm 程序。

![](img/5ced0c78d748bd190e9027e5549a3622_266_0.png)

> prefdm 脚本在 X Window System 环境中管理登录屏幕。

3. 让我们在表 13.1 中定义最常见的 init 级别，并在表 13.2 中定义已知的 init 动作。

## 表 13.1 常见的 init 级别

| 级别 | 含义 |
|---|---|
| 0 | Halt |
| 1 | Single-user mode (also called s mode on some systems) |
| 2 | Multiuser, but no remote file systems mounted; often also no networking daemons running |
| 3 | Full multiuser mode |
| 5 | Full multiuser + X11 graphics |
| 6 | Reboot |

## 表 13.2 已定义的 init 动作

| 动作 | 含义 |
|---|---|
| boot | Process will be executed during system bootup |
| bootwait | Like boot, but init waits for completion |
| ctrlaltdel | Process will be executed when the console keyboard device driver receives a Control-Alt-Del key sequence |
| initdefault | Specifies the default run level to boot into on system boot |
| once | Like wait, but init doesn't wait for completion |
| respawn | Process is guaranteed to be running—the system will restart it if it dies |
| sysinit | Process will be executed during boot, but before any boot or bootwait entries |
| wait | The process will be started once (as opposed to respawn), and init will wait for it to complete |

![](img/5ced0c78d748bd190e9027e5549a3622_267_0.png)

> Unix 的许多版本支持一些动作，让你能优雅地与不间断电源（UPS）交互，包括 powerwait、powerfail、powerokwait 和 powerfailnow。阅读 Linux 上的 apmd 手册页或 Solaris 上的 powerd 手册页以获取更多详细信息。

你的系统不在 init 级别 3（如果你有非图形 Unix 环境）或 init 级别 5（如果你有图形环境；例如启用 Aqua 以获得精美图形用户界面的 Mac OS X）的情况非常罕见。

4. 例如，在我的 Web 服务器上，我将默认 init 级别设置为 3——我不需要运行 X Window System 环境，所以我将周期节省给 Web 服务器、SSH 守护进程等。要查看 init 在此运行级别运行哪些进程，我只需逐步检查 inittab，查找运行级别字段中包含 3 的所有行。

这会列出以下内容：

```
l3:3:wait:/etc/rc.d/rc 3
pr:12345:powerwait:/sbin/shutdown -c 'Power Restored; Shutdown Cancelled'
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
```

其中，最后六个只是确保虚拟控制台有监听程序可用的进程。pr 行匹配电源恢复事件。（通过不在 powerfail 动作中指定 init 级别，你可以暗示它适用于所有状态——回头查看我们刚刚列出的 /etc/inittab 就明白我的意思了。）

最后，输出的第一行可能最重要：在进入 init 状态 3 时，运行 /etc/rc.d/rc.3 并等待其完成。rc 目录包含为每个特定 init 级别执行的所有脚本列表（这等同于“自动启动的所有守护进程和程序的列表”）。目录 /etc/rc.d/rc.3 包含控制在运行级别 3 运行（或不运行）内容的脚本。同样，init 状态 5 是多用户 + 图形用户界面，通常是 X Window System。/etc/inittab 中运行级别 5 的条目与运行级别 3 相同，唯一例外是运行级别 5 引用 /etc/rc.d/rc.5 而不是。

![](img/5ced0c78d748bd190e9027e5549a3622_267_1.png)

