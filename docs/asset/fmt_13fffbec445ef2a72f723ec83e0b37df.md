
1. **引导硬件** — 基于计算机只读存储器中的信息（称为`BIOS`），计算机检查并启动硬件。这些信息中的一部分告诉计算机检查哪些设备（软盘、CD、硬盘等）以寻找可引导的操作系统。

2. **启动引导加载程序** — 通常，在检查软盘、CD 或 DVD 驱动器中没有准备就绪的可引导操作系统后，`BIOS` 会检查主硬盘上的主引导记录，以决定接下来加载什么。安装 `CentOS` 后，`GRUB` 引导加载程序将启动，允许你选择启动 `CentOS` 或其他已安装的操作系统。

3. **引导内核** — 假设你选择启动 `CentOS`，则加载 Linux 内核。该内核挂载基本文件系统并将控制权转移给 `init` 进程。本节其余部分描述了在内核将系统启动控制权移交给 `init` 进程之后发生的情况。

### 启动 init

在引导过程中，从内核阶段（加载内核、探测设备和加载驱动程序）到 `init` 的转移由以下行表示：

```text
Welcome to CentOS release 5.3 (Final)
Press "I" to enter interactive startup.
```

`init` 程序，`SysVinit` `RPM` 包的一部分，现在处于控制状态。

`ps` 的输出始终将 `init`（被称为 `所有进程的父进程`）列为 `PID`（进程标识符）1。

在 `CentOS` 中，一个特殊的脚本 `/etc/inittab` 指导 `init` 程序的动作。

### inittab 文件

以下示例显示了随 `CentOS` 提供的 `/etc/inittab` 文件的内容：

```text
#
# Inittab  This file describes how the INIT process should set up
# the system in a certain run-level.
#
# Author:  Miguel van Smoorenburg, <miquels@drinkel.nl.mugnet.org>
# Modified for RHLinux by Marc Ewing and Donnie Barnes
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

# System initialization.
```

### 第三部分 管理

### 初始化配置

```text
si::sysinit:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6

# 捕获 CTRL-ALT-DELETE
ca:ctrlaltdel:/sbin/shutdown -t3 -r now

# 当我们的 UPS 通知我们电源故障时，假设我们还有几分
钟的电力。调度在 2 分钟后执行关机。
# 当然，这假设您已安装 powered 软件并且您的
# UPS 已连接并正确工作。
pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shut-
ting Down"

# 如果电源恢复时关机尚未开始，则取消它。
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Can-
celled"

# 在标准运行级别中运行 getty
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6

# 在运行级别 5 中运行 xdm
x:5:respawn:/etc/X11/prefdm -nodaemon
```

纯文本 `inittab` 文件由几个冒号分隔的字段组成，其格式如下：

```text
id:runlevels:action:command
```

`id` 字段是一个唯一标识符，长度为 1 到 4 个字母数字字符，代表系统启动期间要执行的特定操作。`runlevels` 字段包含命令将运行的运行级别列表。常见的运行级别是 0、1、2、3、4、5 和 6（`s` 和 `S` 代表单用户模式，等价于 1）。运行级别 7、8 和 9 也可以用作与 on-demand（按需）操作相关的特殊运行级别（a、b 和 c，分别等价于 A、B 和 C）。下一个字段表示 `init` 要执行的操作类型（有效的操作及其结果列于表 11-3 中），最后一个字段是要执行的实际命令。

### 表 11-3 有效的 init 操作

| 操作 | 命令执行方式 |
| :--- | :--- |
| `once` | 进入指定运行级别时，命令执行一次。 |
| `wait` | 与 `once` 相同，但 `init` 会等待命令完成后再继续处理其他 `inittab` 条目。 |
| `respawn` | 监控该进程，如果原始进程终止，则启动一个新实例。 |
| `powerfail` | 在接收到来自与 `UPS` 单元关联软件的 `SIGPWR` 信号时执行命令。这假设还有几分钟的电力，因此默认情况下，系统可以在 2 分钟内关机。 |
| `powerwait` | 与 `powerfail` 相同，但 `init` 会等待命令完成。 |
| `powerokwait` | 如果 `/etc/powerstatus` 文件包含单词 `OK`，则在接收到 `SIGPWR` 信号时执行命令。这通常由 `UPS` 软件完成，表明正常的电力水平已恢复。 |
| `powerfailnow` | 本地系统可能能够检测到外部 `UPS` 电力耗尽并即将几乎立即失效。 |
| `ondemand` | 当 `init` 被手动指示进入特殊运行级别 a、b 或 c（分别等价于 A、B 和 C）之一时，执行命令。实际上不会发生运行级别的变化。如果原始进程终止，程序将重新启动。 |
| `sysinit` | 命令在系统引导阶段执行；忽略 `runlevels` 字段。 |
| `boot` | 命令在系统引导阶段执行，在所有 `sysinit` 条目处理之后；忽略 `runlevels` 字段。 |
| `bootwait` | 与 `boot` 相同，但 `init` 会等待命令完成后再继续处理其他 `inittab` 条目；`runlevels` 字段也被忽略。 |
| `initdefault` | 完成 `boot` 和 `sysinit` 操作后要进入的运行级别 |
| `off` | 不发生任何事（可能对测试和调试有用）。 |
| `ctrlaltdel` | 捕获 `(Ctrl)+(Alt)+(Del)` 键序列，通常用于优雅地关闭系统。 |
| `krequest` | 用于捕获特殊键序列，由键盘处理器进行解释 |

由于 `inittab` 文件是配置文件，而不是顺序 shell 脚本，因此行的顺序并不重要。以井号（`#`）字符开头的行是注释，不会被处理。

在前面的示例 `inittab` 文件中，第一行非注释行将默认运行级别设置为 5。默认值为 5（这是桌面系统的常见运行级别）意味着，在完成与 `sysinit`、`boot` 和 `bootwait` 操作相关的所有命令后，系统将进入运行级别 5（引导到基于 GUI 的登录界面）。

另一个常见的 `initdefault` 级别是运行级别 3（通常用于以文本模式启动的服务器，且通常没有 GUI）。表 11-4 描述了每个运行级别，并帮助您选择最适合您环境的默认运行级别。

> 如果在 `inittab` 文件中没有指定 `initdefault`，引导序列将被中断，并且系统会提示您指定机器将引导进入的默认运行级别。

`inittab` 文件中的下一行指示 `init` 在进入默认运行级别之前执行 `/etc/rc.d/rc.sysinit` 脚本。该脚本执行许多初始化例程，例如选择键映射文件、检查和挂载 `root` 和 `proc` 文件系统、设置时钟和主机名、配置交换空间、清理临时文件以及加载模块。

接下来的七行控制在每个主要运行级别内执行的命令。在其中，调用 `/etc/rc.d/rc` 脚本，并使用所需的运行级别作为参数。反过来，它会进入相应的目录树（例如，对于运行级别 3，进入 `/etc/rc3.d` 目录）。

`inittab` 文件中的 `ctrlaltdel` 操作告诉 `init` 执行 PC 用户在同时按下 `[Ctrl]+[Alt]+[Delete]` 键时所预期的确切操作。系统在 3 秒延迟后以有序的方式重新启动自身（切换到运行级别 6）。

接下来的两行（及其注释）涉及在您拥有不间断电源（`UPS`）和已安装软件的情况下进行的优雅关机。第一行在接收到 `UPS` 发出的表示电源故障的信号后 2 分钟发起停机（切换到运行级别 0）。如果电源恢复，第二行将取消关机。

六行 `getty` 行启动虚拟控制台以允许登录。这些进程始终在任意倍数运行级别中运行。当连接到虚拟控制台的某位用户注销时，该 `getty` 进程终止，然后 `respawn` 操作告诉 `init` 启动一个新的 `getty` 进程。您可以通过按 `[Ctrl]+[Alt]+[F1]`、`[Ctrl]+[Alt]+[F2]` 等按键在虚拟控制台之间切换。

最后一行表明，只要系统处于运行级别 5，"首选显示管理器"（`xdm`、`gdm`（`Gnome`）、`kdm`（`KDE`）等）就会运行。这会呈现图形登录提示，而不是通常的基于文本的登录，并消除了运行 `startx` 来启动 GUI 的需要。

### 表 11-4 可能的运行级别

| 运行级别 | 在此运行级别中发生的事情 |
| :--- | :--- |
| `0` | 所有进程终止，机器有序停机。正如 `inittab` 注释所指出的，这不是 `inittabdefault` 的好选择，因为一旦内核、模块和驱动程序加载完毕，机器就会停机。 |
| `1`, `s`, `S` | 这是单用户模式，常用于系统维护以及最好保持很少进程运行且未激活服务的情况。在单用户模式下，网络不存在，`X` 服务器未运行，并且可能有些文件系统未挂载。 |
| `2` | 多用户模式。允许多个用户登录，挂载所有配置的文件系统，并启动除 `X`、`at` 守护进程、`xinetd` 守护进程和 `NIS/NFS` 之外的所有进程。如果您的机器没有（或可能不需要）永久网络连接，这是 `inittabdefault` 的好选择。 |
| `3` | 带有网络服务的多用户模式。运行级别 3 是 `CentOS` 服务器上 `inittabdefault` 的典型值。 |
| `4` | 运行级别 4 可作为用户定义的运行级别使用。在默认 `CentOS` 配置中，它与运行级别 3 几乎相同。 |
| `5` | 带有网络服务和 `X` 的多用户模式。此运行级别启动 `X` 服务器并呈现图形登录窗口，视觉上类似于任何较昂贵的基于 `UNIX` 的工作站。这是 `CentOS` 工作站或桌面系统常见的 `inittabdefault` 值。 |
| `6` | 所有进程终止，机器优雅地重新启动。同样，`inittab` 文件中的注释提到这不是 `inittabdefault` 的好选择，甚至可能比运行级别 0 更糟。效果可能是无限循环的引导，然后是重新启动。 |
| `7`, `8`, `9` | 通常未使用且未定义，这些运行级别具有满足默认选项未涵盖的任何需求的潜力。 |
| `a`, `b`, `c`, `A`, `B`, `C` | 与 `ondemand` 操作一起使用。这些实际上不指定运行级别，但可以根据指示“按需”启动程序或守护进程。 |

### 系统启动和关机

在系统启动期间，会运行一系列脚本以启动您所需的服务。这些包括启动网络接口、挂载目录以及监控系统的脚本。这些脚本大多从 `/etc/rc.d` 的子目录中运行。启动这些脚本的大多数程序

### 自动化系统任务

在系统启动时启动服务、在关机时停止服务的是 `/etc/rc.d/rc` 脚本。以下各节将介绍运行级别脚本以及如何使用它们。

### 启动运行级别脚本

如前所述，`/etc/rc.d/rc` 脚本对于运行级别的概念至关重要。任何运行级别的变更都会导致该脚本执行，并将新的运行级别作为参数传入。以下是 `/etc/rc.d/rc` 脚本功能简述：

- **检查运行级别脚本是否正确** — `rc` 脚本会查找每个存在的运行级别脚本，并排除那些由 `rpm` 更新留下的备份脚本。

- **确定当前和之前的运行级别** — 确定当前和之前的运行级别，以了解需要停止（上一级别）和启动（当前级别）哪些运行级别脚本。

- **决定是否进入交互式启动** — 如果在启动时将 `confirm` 选项传递给启动加载程序，则所有服务器进程在启动前必须在系统控制台上得到确认。

- **终止并启动运行级别脚本** — 停止上一级别的运行级别脚本，然后启动当前级别的运行级别脚本。

在 `CentOS` 中，提供给网络和计算机的大多数服务都是通过运行级别脚本启动的。

### 理解运行级别脚本

如果一个软件包需要在启动时（或系统更改运行级别时）启动某个服务，它可以向 `/etc/init.d` 目录添加一个脚本。然后，该脚本可以链接到适当的运行级别目录，并使用 `start` 或 `stop` 选项运行（以启动或停止服务）。

表 11-5 列出了在 `/etc/init.d` 中发现的许多典型运行级别脚本，并解释了它们的功能。根据你在系统上安装的 `CentOS` 软件包，你可能会看到比这里列出的多几十种运行级别脚本。（稍后，我将描述这些文件如何链接到特定的运行级别目录中。）

每个代表你希望启动或停止的服务的脚本都链接到每个运行级别目录中的一个文件。对于每个运行级别，以 `K` 开头的脚本会停止服务，而以 `S` 开头的脚本会启动服务。

文件名中 `K` 或 `S` 后面的两位数字提供了一种选择程序运行优先级的机制。例如，`S12syslog` 在 `S90crond` 之前运行。然而，文件 `S110my_daemon` 却在 `S85gnup` 之前运行，尽管可以很容易看出 85 小于 110。这是因为 `ASCII` 排序顺序对文件进行了排序，这意味着仅仅是对位置字符进行比较。因此，在运行级别 3 中，以 `S110` 字符开头的脚本会在 `S10network` 和 `S15netfs` 之间执行。

### /etc/init.d 中包含的运行级别脚本

| 运行级别脚本 | 它的作用是什么？ |
|---|---|
| `acpid` | 控制高级配置和电源接口（`ACPI`）守护进程，该进程监控内核中的事件并向用户级别报告。 |
| `anacron` | 运行那些因为系统关机而未在预定时间执行的 `cron` 任务。 |
| `atd` | 启动或停止 `at` 守护进程，用于接收、排队和运行通过 `at` 或 `batch` 命令提交的任务。（`anacron` 运行级别脚本会运行那些因为计算机关机而未执行的 `at` 和 `batch` 任务。） |
| `autofs` | 启动和停止自动挂载守护进程，用于自动挂载文件系统（例如，插入光盘时自动挂载光盘）。 |
| `bluetooth` | 启动用于与蓝牙设备通信的服务，如认证、发现和人体接口设备。 |
| `crond` | 启动或停止 `cron` 守护进程，用于定期执行常规命令。 |
| `cups` | 控制处理打印请求排队的打印机守护进程（`cupsd`）。 |
| `dhcpc` | 启动或停止 `dhcpcd` 守护进程，该进程自动为局域网中的计算机分配 `IP` 地址。 |
| `firstboot` | 检查是否需要运行 `firstboot`，如果需要则运行它。这通常在首次安装 `CentOS` 后完成。 |
| `gpm` | 控制 `gpm` 守护进程，允许鼠标与控制台和基于文本的应用程序交互。 |
| `haldaemon` | 启动 `hald` 守护进程以发现和设置硬件。用于挂载可移动介质、管理电源或自动播放多媒体。 |
| `halt` | 终止所有进程，写出会计记录，移除交换空间，卸载所有文件系统，并根据命令调用方式关闭或重启机器。 |
| `hplip` | 启动 `HP` Linux 图像和打印（`HPLIP`）服务，用于运行 `HP` 多功能外围设备。 |
| `httpd` | 启动 `httpd` 守护进程，允许你的计算机充当 `HTTP` 服务器（即提供网页）。 |
| `iptables` | 从 `/etc/sysconfig/iptables` 加载定义好的防火墙规则。 |
| `killall` | 在关机或重启之前，终止任何可能仍在运行的子系统。 |
| `ldap` | 启动轻量级目录访问协议守护进程（`slapd`），监听来自网络中的 `LDAP` 请求。 |
| `mysqld` | 运行 `MySQL` 数据库守护进程（`mysqld`），监听对 `MySQL` 数据库的请求。 |
| `named` | 启动和停止 `BIND` `DNS` 服务器守护进程（`named`），用于监听和解析域名系统请求。 |
| `netfs` | 挂载或卸载网络（`NFS`、`SMB` 和 `NCP`）文件系统。 |
| `network` | 启动或停止所有配置好的网络接口，并初始化 `TCP/IP` 和 `IPX` 协议。 |
| `NetworkManager` | 自动切换到最佳可用的网络连接。 |
