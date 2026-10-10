
以及电话号码 608-555-1212 到数据库（$HOME/.phone.txt）中。下一个 ph 命令在数据库中搜索名字 Mary 并显示 Mary 的电话条目。如果脚本运行正常，请将其添加到您 PATH 中的某个目录（例如 $HOME/bin）中。

# 简单的备份脚本

由于没有什么能永远正常运行，且错误总会发生，因此在处理计算机数据时，备份是生活的常态。这个简单的脚本会备份 Fedora 系统上所有用户的家目录中的所有数据。

```bash
#!/bin/bash
# (@)my backup
# A very simple backup script
#

# Change the TAPE device to match your system.
# Check /var/log/messages to determine your tape device.
# You may also need to add scsi-tape support to your kernel.
TAPE=/dev/rft0

# Rewind the tape device $TAPE
mt -f $TAPE rew
# Get a list of home directories
HOMES="grep /home /etc/passwd | cut -f6 -d':'"
# Backup the data in those directories
tar cvf $TAPE $HOMES
# Rewind and eject the tape.
mt -f $TAPE rewoffl
```

> **交叉参考：** 有关备份和恢复文件以及获取 mt 命令（tape-tools 软件包的一部分，需单独安装）的详细信息，请参阅第 12 章。

## 系统初始化

当您打开计算机时，甚至在 Fedora 启动之前，已经发生了很多事。以下是每次启动计算机运行 Fedora 时发生的基本步骤：

1.  **引导硬件** — 基于计算机只读存储器（即 BIOS）中的信息，您的计算机将检查并启动硬件。其中部分信息告知计算机应检查哪些设备（软盘、CD、硬盘等）以找到可引导的操作系统。
2.  **启动引导加载程序** — 在确认软盘、CD 或 DVD 驱动器中没有可引导的操作系统后，通常 BIOS 会检查主硬盘上的主引导记录，以确定接下来要加载什么。在安装了 Fedora 后，GRUB 引导加载程序将被启动，允许您选择引导 Fedora 或另一个已安装的操作系统。
3.  **引导内核** — 假设您选择了引导 Fedora，Linux 内核将被加载。该内核将挂载基本文件系统并将控制权移交给 init 进程。

本节的其余部分描述了在内核将系统启动控制权移交给 init 进程后发生的情况。

## 启动 init

在引导过程中，从内核阶段（内核加载、设备探测和驱动程序加载）到 init 的移交由以下行指示：

```text
Welcome to Fedora
Press "I" to enter interactive startup.
```

init 程序是 upstart RPM 软件包的一部分，现在它掌握了控制权。ps 命令的输出总是列出 init（被称为“所有进程的父进程”）的 PID（进程标识符）为 1。

在 Fedora 9 之前，一个特殊的脚本 `/etc/inittab` 指导 init 程序的操作。从 Fedora 9 开始，一个名为 upstart 的新初始化系统取代了旧的 SysV UNIX 风格的 init 程序。

在 upstart 中，`/etc/inittab` 文件仅控制默认运行级别。其他所有内容都从每个运行级别的特殊脚本运行，例如，运行级别 5 的 `/etc/event.d/rc5`。Upstart 基于根据事件而非运行级别来启动程序的概念。Upstart 可以重启终止的服务，并且不像旧的 SysV init 系统那样脆弱。

然而，由于许多 Linux 程序对 init 系统做出了假设，upstart 在兼容模式下运行。此外，为了理解 upstart，您需要理解下文中描述的旧版 Linux 和 UNIX 运行级别。在多个 Fedora 版本中，upstart 将逐步淘汰旧版的 Linux 初始化方式。

但就目前而言，以下概念仍然适用。

## inittab 文件

以下示例显示了在 Fedora 9 之前版本中随 Fedora 提供的 `/etc/inittab` 文件的内容：

```text
# inittab This file describes how the INIT process should set up
# the system in a certain run level.
.
.
.
id:5:initdefault:

# System initialization.
si:sysinit:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6

# Trap CTRL-ALT-DELETE
ca:2:ctrlaltdel:/sbin/shutdown -t3 -r now

# When our UPS tells us power has failed, assume we have a few minutes
# of power left.  Schedule a shutdown for 2 minutes from now.
# This does, of course, assume you have powerd installed and your
# UPS connected and working correctly.
pf:powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"

# If power was restored before the shutdown kicked in, cancel it.
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

# Run getty in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6

# Run xdm in runlevel 5
x:5:once:/etc/X11/prefdm -nodemand
```

纯文本的 init tab 文件由几个以冒号分隔的字段组成，格式如下：

```text
id:runlevels:action:command
```

**id** 字段是一个唯一的标识符，长度为一到四个字母数字字符，代表系统启动期间要采取的一个特定操作。**runlevels** 字段包含将在其中运行命令的运行级别列表。常见的运行级别是 0、1、2、3、4、5 和 6（s 和 S 代表单用户模式，等同于 1）。运行级别 7、8 和 9 也可以用作与 on-demand 操作关联的特殊运行级别（a、b 和 c，分别等同于 A、B 和 C）。下一个字段代表 **init** 要采取的操作类型（有效的操作及其结果列于表 11-3 中），最后一个字段是要执行的实际命令。

### 表 11-3：有效的 init 操作

| 操作 | 命令运行方式 |
| :--- | :--- |
| once | 进入指定运行级别时执行一次命令。 |
| wait | 与 **once** 相同，但 **init** 会等待命令完成，然后再继续处理其他 inittab 条目。 |
| respawn | 监控该进程，如果原始进程终止，则启动一个新实例。 |
| powerfail | 在接收到来自通用电源（UPS）单元关联软件的 SIGPWR 信号时执行命令。这假设还有几分钟的电力，因此默认情况下，系统可以在两分钟内关闭系统。 |
| powerwait | 与 powerfail 相同，但 init 会等待命令完成。 |
| powerokwait | 如果 /etc/powerstatus 文件包含单词 OK，则在接收到 SIGKRW 信号时执行命令。这通常由 UPS 软件完成，表示正常电力水平已恢复。 |
| powerfailnow | 本地系统可能能够检测到外部 UPS 电量耗尽，并即将立即发生故障。 |
| ondemand | 当手动指示 init 进入特殊运行级别 a、b 或 c（分别等同于 A、B 和 C）时执行命令。实际上不会发生运行级别的变更。如果原始进程终止，程序将重新启动。 |
| sysinit | 在系统引导阶段执行命令；忽略 runlevels 字段。 |
| boot | 在系统引导阶段，处理完所有 sysinit 条目后执行命令；忽略 runlevels 字段。 |
| bootwait | 与 boot 相同，但 init 会等待命令完成，然后再继续处理其他 inittab 条目；同样忽略 runlevels 字段。 |
| initdefault | 完成 boot 和 sysinit 操作后要进入的运行级别。 |
| off | 不执行任何操作（可能对测试和调试有用）。 |
| ctrlaltdel | 拦截 Ctrl+Alt+Del 按键序列，通常用于优雅地关闭系统。 |
| kbsrequest | 用于拦截由键盘处理程序解释的特殊按键序列。 |

由于 inittab 文件是一个配置文件，而不是顺序执行的 shell 脚本，因此行的顺序并不重要。以井号（#）字符开头的行是注释，不会被处理。

前面示例 inittab 文件中的第一个非注释行将默认运行级别设置为 5。Fedora 的默认值 5（这是桌面系统常见的运行级别）意味着，在完成与 sysinit、boot 和

