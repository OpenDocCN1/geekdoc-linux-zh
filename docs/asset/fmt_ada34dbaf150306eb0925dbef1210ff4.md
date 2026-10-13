
系统重新启动并显示 `boot:` 提示符。你可以输入 `linux` 或按 Enter 首次启动 Red Hat Linux。当然，如果你忘记执行其中任何一项，LILO 将在短时间内超时并启动默认操作系统。

Linux 内核开始启动后，你会看到一个充满信息的对话框。如果看到的信息经过太快，不要绝望。你很快就能访问所有这些信息。请耐心等待系统在控制台上显示登录提示。

当显示登录提示时，以用户 `root` 登录，使用你在安装过程中输入的密码。你现在应该已以 `root` 身份登录到系统。你刚刚成为自己的 Red Hat Linux 服务器的超级用户。你的 Linux 系统等待你的命令。

如果你想查看启动过程中飞快闪过的內容，则运行 `dmesg` 命令以查看启动消息。如果屏幕滚动过快，使用 `dmesg | more` 每次查看一页。

![](img/c2419364ebb911c809b6a79991707c27_45_0.png)

### 提示

Linux 具有微软系统上找不到的功能：能够回滚到控制台的历史记录。按下 `Shift+PgUp` 会显示屏幕上刚刚闪过的內容。但是，当你切换到另一个虚拟控制台时，此历史记录会丢失。登录屏幕执行“清屏”操作会破坏引导显示的最后几行，这令人沮丧。出于这个原因，你可以修改 `/etc/inittab` 以避免在虚拟控制台 1 上运行 `getty`。

这是一个确保内核正确检测硬件的好时机。阅读 `dmesg` 程序的输出即可得知。

# 第 2 章

## 启动和关闭配置

### 配置第一个进程：init

Red Hat Linux 内核（即核心操作系统）通常存储在压缩文件中。当内核由引导加载程序（如 LILO）启动时，它会自行解压缩，初始化显示设备，并开始检查计算机上连接的其他硬件。随着它找到硬盘、软盘驱动器、网卡等，它会加载适当的设备驱动程序模块。在此过程中，它会在控制台屏幕上显示文本消息。

![](img/c2419364ebb911c809b6a79991707c27_46_0.png)

### 提示

如果你在启动系统时位于控制台，可以按 `Shift+PgUp` 向上滚动显示以查看启动消息。你也可以随时通过运行 `dmesg` 程序查看启动消息。`/var/log/messages` 文件中也会包含许多启动消息。

此时，内核以只读方式挂载根文件系统（`/`）并对文件系统进行检查。如果内核发现一切正常，它会以读写方式挂载根文件系统。如果出现问题且内核无法挂载根分区，内核会 `panic` 并系统停止。如果磁盘 somehow 损坏，内核可能会提供从受限 shell 运行文件系统检查程序（如 `fsck.ext2`）的选项。在这种情况下，在根分区或启动期间失败的任何其他分区上运行 `fsck.ext2`。例如，如果你的系统根分区位于 `/dev/sda1`（SCSI 磁盘分区）并且失败，则运行

```
fsck.ext2 /dev/sda1
```

修复过程完成后，通过键入 `exit` 退出 shell，系统将再次尝试启动。希望这次能成功。

根文件系统挂载后，内核启动一个名为 `init` 的程序。此程序启动所有其他程序。`init` 启动所有必要程序后，系统即可运行，启动过程完成。

`init` 在启动过程中运行的内容高度可定制。以下各节详细讨论 `init`。

`init` 程序有两种风格——UNIX System V `init` 和 BSD `init`。Red Hat 发行版附带 UNIX System V `init` 程序。两种风格的区别在于 System V `init` 使用运行级别（本节后面讨论），而 BSD `init` 不使用。由于 Red Hat 发行版使用 UNIX System V `init`，本管理员手册将 `init` 的讨论限制在此风格。

由于 `init` 是内核运行的第一个程序，其进程 ID（`PID`）为 1。`init` 启动时，它会读取一个名为 `/etc/inittab` 的配置文件。典型 Red Hat Linux 系统中的 `/etc/inittab` 文件如列表 2-1 所示。

### 列表 2-1 一个典型的 `/etc/inittab` 文件

```
# inittab - This file describes how the init
# process should set up the system in a
# certain run level.
#
# Author: Miquel van Smoorenburg,
# <miquels@drinkel.nl.mugnet.org>
#
# Modified for RHS Linux by Marc Ewing and Donnie Barnes
# Default runlevel. The runlevels used by RHS are:
# 0 - halt (Do NOT set initdefault to this)
# 1 - Single-user mode
# 2 - Multiuser, without NFS (The same as 3, if you
#     do not have networking)
# 3 - Full multiuser mode
# 4 - unused
# 5 - X11
# 6 - reboot (Do NOT set initdefault to this)
#
id:3:initdefault:

# System initialization.
si::sysinit:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6

# Things to run in every runlevel.
ud::once:/sbin/update

# Trap Ctrl+Alt+Delete
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

# When our UPS tells us power has failed, assume we have
# a few minutes of power left. Schedule a shutdown for
# 2 minutes from now.
#
# This does, of course, assume you have powerd installed
and your
# UPS connected and working correctly.
#
#
 pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure; \
System Shutting Down"

# If power was restored before the shutdown kicked in,
cancel it.
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; \
Shutdown Cancelled"

# Run gettys in standard runlevels
1:12345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6

# Run xdm in runlevel 5
x:5:respawn:/usr/bin/X11/xdm -nodaemon
```

此文件定义了 `init` 在服务器启动或关闭事件期间的行为。

以下讨论更详细地查看此文件。

`init` 程序会忽略 `/etc/inittab` 文件中的所有空白行和注释行（即以 `#` 符号开头的行）。带冒号分隔字段的行是 `init` 配置行。此类行的语法如下：

```
id:runlevels:action:process arguments
```

第一个字段是用于在文件中标识条目的唯一标签字段。`id` 可以长 2 到 4 个字符。第二个字段 `runlevels` 定义此行适用于哪些运行级别。第三个字段定义需要采取什么操作。最后一个字段（`process`）定义需要运行哪个进程。

可选地，你还可以在第四个字段中为进程指定命令行参数。

如前所述，运行级别指定系统的一种状态。九个运行级别在表 2-1 中描述。

### 表 2-1 init 的运行级别

| 运行级别 | 描述 |
|---|---|
| 0 | 停止 – 用于停止系统 |
| 1 | 单用户 – 用于将系统设置为适合单用户的最小配置 |
| 2 | 未使用 |
| 3 | 多用户 – 用于将系统设置为支持多用户的配置 |
| 4 | 未使用 |
