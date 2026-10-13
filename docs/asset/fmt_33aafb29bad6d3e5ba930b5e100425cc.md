
假设你选择了启动 Fedora，Linux 内核将被加载。该内核挂载基本文件系统，并将控制权传递给 `init` 进程。本节的其余部分描述了内核将系统启动控制权移交给 `init` 进程后发生的事情。

## 启动 init

在启动过程中，从内核阶段（内核加载、设备探测和驱动程序加载）到 `init` 的转换由以下行指示：

```
INIT: version 2.05 booting
```

Welcome to Fedora Core

Press "I" to enter interactive startup.

`init` 程序，作为 `SysVinit` RPM 包的一部分，现在处于控制地位。被称为“所有进程的之父”，`ps` 的输出始终将 `init` 列为 `PID`（进程标识符）1。其操作由 `/etc/inittab` 文件指导，该文件如下所示。

### inittab 文件

以下示例显示了随 Fedora 提供的 `/etc/inittab` 文件的内容：

```
# inittab	This file describes how the INIT process should set up
#		the system in a certain run level.
.
.
.

id:3:5:initdefault:

# System initialization.

si::sysinit:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6

# Trap CTRL-ALT-DELETE.
ca:ctrlaltdel:/sbin/shutdown -t3 -r now

# When our UPS tells us power has failed, assume we have a few minutes
# of power left. Schedule a shutdown for 2 minutes from now.

# This does, of course, assume you have powerd installed and your
# UPS connected and working correctly.
pf:powerfail:/sbin/shutdown -h +2 "Power Failure; System Shutting Down"

# If power was restored before the shutdown kicked in, cancel it.
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

# Run getty in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
```

```
6:23:45:respawn:/sbin/mingetty tty6
```

# 在运行级别 5 中运行 xdm

# xdm 现在是一个独立的服务

x:5:respawn:/etc/X11/prefdm -nodademon

#### inittab 文件格式

纯文本 `inittab` 文件由若干以冒号分隔的字段组成，格式如下：

```
id:runlevels:action:command
```

`id` 字段是一个唯一的标识符，长度为 1 到 4 个字母数字字符，代表系统在启动期间要执行的特定操作。`runlevels` 字段包含将在其中执行命令的运行级别列表。常见的运行级别为 0、1、2、3、4、5 和 6（s 和 S 代表单用户模式，等效于 1）。运行级别 7、8 和 9 也可用作与按需（on demand）操作相关联的特殊运行级别（a、b 和 c，分别等效于 A、B 和 C）。下一个字段表示 `init` 要执行的操作类型（有效的操作及其结果列于表 12-3 中），最后一个字段是要执行的实际命令。

##### 表 12-3：有效的 init 操作

| 操作 | 命令执行方式 |
| :--- | :--- |
| once | 在进入指定的运行级别时，命令只执行一次。 |
| wait | 与 `once` 相同，但 `init` 在继续处理其他 `inittab` 条目之前，会等待命令执行完毕。 |
| respawn | 进程会被监控，如果原始进程终止，则启动一个新实例。 |
| powerfail | 当接收到来自 UPS 单元相关软件的 SIGPWR 信号时，执行该命令。 |
| powerwait | 与 `powerfail` 相同，但 `init` 会等待命令执行完毕。 |
| powerwaitok | 如果 `/etc/powerstatus` 文件包含单词 OK，则在接收到 SIGPWR 信号时执行该命令。这通常由 UPS 软件完成，表示正常电力水平已恢复。 |
| ondemand | 当手动指示 `init` 进入特殊运行级别 a、b 或 c（分别等效于 A、B 和 C）时执行该命令。实际上不会发生运行级别的变化。如果原始进程终止，程序会重新启动。 |
| sysinit | 在系统启动阶段执行该命令；忽略 `runlevels` 字段。 |
| boot | 在系统启动阶段，处理完所有 `sysinit` 条目后执行该命令；忽略 `runlevels` 字段。 |
| bootwait | 与 `boot` 相同，但在继续处理其他 `inittab` 条目之前，等待命令执行完毕；同样忽略 `runlevels` 字段。 |
| initdefault | 在完成 `boot` 和 `sysinit` 操作后进入的运行级别。 |
| off | 不执行任何操作（可能用于测试和调试）。 |
| ctrlaltdel | 捕获 Ctrl+Alt+Del 键序列，通常用于优雅地关闭系统。 |
| kbdrequest | 用于捕获由键盘处理程序解释的特殊键序列。 |

##### inittab 文件解析

由于 `inittab` 文件是配置文件，而非顺序执行的 shell 脚本，因此行的顺序并不重要。以井号（`#`）开头的行是注释，不会被处理。

前述示例 `inittab` 文件中的第一个非注释行将默认运行级别设置为 3。默认为 3 意味着，在完成所有与 `sysinit`、`boot` 和 `bootwait` 操作相关的命令后，系统将进入运行级别 3（启动到基于文本的登录界面）。另一个常见的 `initdefault` 级别是运行级别 5（启动到图形用户界面登录屏幕）。表 12-4 描述了每个运行级别，并帮助您选择最适合您环境的默认运行级别。

##### 表 12-4：可能的运行级别

| 运行级别 | 此运行级别中发生的情况 |
| :--- | :--- |
| 0 | 所有进程终止，机器有序停机。正如 `inittab` 注释指出的，这不是 `initdefault` 的好选择，因为一旦内核、模块和驱动程序加载完毕，机器就会停机。 |
| 1, s, S | 这是单用户模式，常用于系统维护，且可能更倾向于只运行少量进程并停用服务。在单用户模式下，网络不存在，X 服务器未运行，且部分文件系统可能未挂载。 |
| 2 | 多用户模式。允许多个用户登录，所有配置的文件系统均已挂载，并启动了除 X、at 守护进程、`xinetd` 守护进程和 NIS/NFS 之外的所有进程。如果您的机器没有（或可能不需要）永久网络连接，这是 `initdefault` 的一个不错的选择。 |
| 3, 4 | 带有网络服务的多用户模式。运行级别 3 是 Fedora 服务器上 `initdefault` 的典型值，但在默认的 Fedora 配置中，运行级别 4（通常留给用户自定义）几乎与之相同。 |
| 5 | 带有网络服务和 X 的多用户模式。此运行级别启动 X 服务器并显示图形登录窗口，视觉上类似于更昂贵的基于 UNIX 的工作站。这是 Fedora 工作站或桌面系统常见的 `initdefault` 值。 |
| 6 | 所有进程终止，机器优雅地重启。同样，`inittab` 文件中的注释提到这不是 `initdefault` 的好选择，甚至可能比运行级别 0 更糟。其效果可能是启动后重启的无限循环。 |
| 7, 8, 9 | 通常未使用且未定义，这些运行级别有可能满足默认选项未覆盖的任何需求。 |
| a, b, c, A, B, C | 与 `ondemand` 操作配合使用。这些并不真正指定运行级别，但如果收到指示，可以“按需”启动程序或守护进程。 |
