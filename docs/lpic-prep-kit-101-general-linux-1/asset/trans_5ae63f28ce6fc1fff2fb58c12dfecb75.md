

- 任何已加载的设备驱动程序
- 交换空间的大小
- 网络适配器及其设置

有关此日志文件和 dmesg 命令用法的更多信息，请参阅第 10 章“管理任务”。

内核启动后，它会挂载根文件系统，该文件系统通常位于您的硬盘上。挂载根文件系统后，控制权便移交给了硬盘，而内核则保留在内存中。

## init 守护进程

内核执行的最后一步是调用 init 守护进程，该进程将保持活跃状态，直到您关闭系统。它负责创建系统其余部分所需的进程，例如登录 shell。init 守护进程还会在特定进程退出时重新启动它们。例如，当您注销时，init 会重新启动控制台，以便您可以再次登录。

init 守护进程的行为由其配置文件 /etc/inittab 控制。

## /etc/inittab 文件

/etc/inittab 文件的每一行都包含由冒号分隔的四个字段：

```
ID:runlevel:action:process
```

表 2.1 展示了每个字段的内容。

### 表 2.1 /etc/inittab 文件中各字段的作用

| 字段 | 内容及用途 |
| --- | --- |
| ID | 用于标识条目的一个或两个字符，通常是设备名称 |
| runlevel | 指示该行适用于哪些运行级别；可以列出多个运行级别；若留空，则适用于所有运行级别 |
| action | 如何处理该条目；有效值请参见表 2.2 |
| process | 要执行的命令 |

action 字段指示如何处理该命令，例如当命令停止时是否重新启动该命令。表 2.2 展示了该字段的有效条目。

### 表 2.2 /etc/inittab 文件中 action 字段的有效条目

| 条目 | 描述 |
| --- | --- |
| boot | 在首次读取 /etc/inittab 时运行 |
| bootwait | 在 boot 条目之后、首次读取 /etc/inittab 时运行 |
| initdefault | 设置初始运行级别；如果该进程正在运行则停止它；之后仅启动该进程一次 |
| ondemand | 保持进程运行；如果它停止则重新启动 |
| powerfail | 在接收到电源故障信号时执行 |
| sysinit | 在执行控制台之前执行 |
| respawn | 保持进程运行；如果该进程停止则重新启动 |
| wait | 仅启动该进程一次 |

**init** 进程用于启动内核及其运行系统所需的其他进程。如果您希望某应用程序在每次系统启动时都运行，请将相应命令写入其中一个 rc 脚本中，这些脚本将在下一节“运行级别”中讨论。

## 运行级别

*运行级别*（runlevel）定义了启动系统时需要启动的一组进程。这可以从用于系统管理的极少量进程，到支持所有已配置设备的配置不等。

不同运行级别对应的数字因您使用的发行版而异，并列在 /etc/inittab 文件中。例如，列表可能如下所示：

```
# Default runlevel. The runlevels used by RHS are:
# 0 - halt (Do NOT set initdefault to this)
# 1 - Single user mode
# 2 - Multiuser, without NFS (The same as 3, if you do not have networking)
# 3 - Full multiuser mode
# 4 - unused
# 5 - X11
# 6 - reboot (Do not set initdefault to this)
```

运行级别 **0** 和 **6** 分别仅保留用于**关机**（halt）和**重启**（reboot）。不同发行版的运行级别可能各不相同。无论您安装了什么发行版，init 守护进程只处理与当前运行级别关联的那些行。

单用户模式与其他可用的运行级别略有不同。此运行级别通常用于系统管理任务，例如修复损坏的文件系统。当系统处于此运行级别时，其他用户无法登录。但是，您仍然可以同时运行多个应用程序。这是 init 不读取 /etc/inittab 文件的唯一情况。相反，默认操作是运行 /bin/su 命令，您将以超级用户或 root 身份登录。

当以高于单用户模式的运行级别启动时，系统将以多用户模式启动。在此模式下，init 会执行 action 为 sysinit、boot 或 bootwait 的那些行。通常，这些行会挂载文件系统。

接下来，init 守护进程将执行运行级别字段中列出的当前运行级别对应的其他所有行。

您的初始运行级别由以下行定义：

```
id:3:initdefault:
```

请注意，此行没有定义要启动的进程，而是定义了启动所用的运行级别。您可以使用 init 命令更改运行级别。其语法如下：

```
init [runlevel]
```

init 命令接受一个运行级别作为参数。您可以使用带有 -t seconds 选项的 telinit 命令来指定在更改运行级别前的等待时间。默认延迟为 5 秒。telinit 命令是 init 命令的一个链接。请务必在更改运行级别前通知所有已登录的用户。

例如，命令

```
init 5
```

将把运行级别更改为级别 5。init 首先发送信号以停止那些未在新运行级别中定义的正在运行的进程。在指定的延迟时间后，telinit 会向这些进程发送 kill 信号。然后，它启动新运行级别中定义的、尚未运行的任何进程。

您也可以通过向 init 或 telinit 命令传递 s 或 S 来切换到单用户模式。

/etc/inittab 文件的下一节定义了要运行的启动脚本，例如：

```
si::sysinit:/etc/rc.d/rc.sysinit
```

行首的 ID si 由 init 守护进程内部使用。此行启动 rc.sysinit 脚本，该脚本处理诸如激活交换分区、运行 fsck 以及挂载文件系统等任务。fsck 命令用于检查文件系统是否存在损坏条目，详细内容将在第 6 章“维护文件系统”中讨论。该脚本可能因发行版而异。请阅读您系统上对应的脚本以了解其具体功能。

/etc/inittab 文件的下一节运行适用于您运行级别的脚本，这些脚本位于 /etc/rc.d 目录中：

```
1:1:wait:/etc/rc.d/rc 1  
12:2:wait:/etc/rc.d/rc 2  
13:3:wait:/etc/rc.d/rc 3  
14:4:wait:/etc/rc.d/rc 4  
15:5:wait:/etc/rc.d/rc 5  
16:6:wait:/etc/rc.d/rc 6
```

这是通过调用带有标识运行级别参数的 `rc` 脚本来实现的。然后，`rc` 脚本会运行位于 `rcn.d` 目录中的脚本，其中 `n` 代表运行级别。根据您的发行版，您的系统还可以执行其他启动脚本，例如 `/etc/rc.local`。

您的 `rc` 脚本还可以调用*模块*。模块是可以在系统运行期间加载和卸载的内核代码片段。这些模块通常是不需要始终使用的设备的设备驱动程序。

您可以使用 `/etc/conf.modules` 文件在模块加载时向每个模块传递参数。这些参数通常是 `I/O` 地址和中断。一个示例 `conf.modules` 文件如下：

```
alias eth0 3c59x  
alias sound 0s1370
```

这会加载以太网卡和声卡所需的模块。

接下来是应在每个运行级别运行的进程。这些通常包括启动一个 `getty` 进程，该进程会为每个虚拟终端创建会话。

您的 `inittab` 文件还可以包含关于电源故障时如何处理以及电源恢复后如何处理的指令。一个示例如下：

```
# When our UPS tells us power has failed, assume we have a few minutes  
of power left. Schedule a shutdown for 2 minutes from now.  
# This does, of course, assume you have powered installed and your  
# UPS connected and working correctly.  
  
pf::powerfail:/sbin/shutdown -f -h +2 'Power Failure; System Shutting Down'  
  
# If power was restored before the shutdown kicked in, cancel it.  
pr:12345:powerokwait:/sbin/shutdown -c 'Power Restored; Shutdown Cancelled'  
# Run gettys in standard runlevels  
1:2345:respawn:/sbin/mingetty tty1  
2:2345:respawn:/sbin/mingetty tty2  
3:2345:respawn:/sbin/mingetty tty3
```

