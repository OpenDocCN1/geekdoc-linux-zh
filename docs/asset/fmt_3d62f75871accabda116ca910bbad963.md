
这是通过调用 `rc` 脚本并传入标识运行级别的参数来实现的。随后，`rc` 脚本会执行位于 `rcn.d` 目录中的脚本，其中 `n` 代表运行级别。根据你的发行版不同，系统还可以执行其他启动脚本，例如 `/etc/rc.local`。

你的 `rc` 脚本还可以调用模块。这些模块是可以在系统运行时加载和卸载的内核代码片段。这些模块通常是你无法一直使用的设备的驱动程序。

你可以使用 `/etc/conf.modules` 文件在模块加载时向其传递参数。这些参数通常是 I/O 地址和中断号。一个 `conf.modules` 文件示例如下：

```
alias eth0 3c59x
alias sound es1370
```

这会加载以太网卡和声卡所需的模块。

接下来是应在每个运行级别中运行的进程。这些通常包括启动 `getty` 进程，用于创建各个虚拟终端。

你的 `inittab` 文件还可以包含在发生断电时以及电源恢复时应执行的操作说明。示例如下：

```
# When our UPS tells us power has failed, assume we have a few minutes
# of power left.  Schedule a shutdown for 2 minutes from now.
# This does, of course, assume you have powered installed and your
# UPS connected and working correctly.
pf:powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"

# If power was restored before the shutdown kicked in, cancel it.
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Canceled"
# Run gettys in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
```

`shutdown` 命令将在本章稍后部分讨论。

`init` 守护进程在读取 `/etc/inittab` 文件后保持活跃状态。它监控系统，以检测更改运行级别的指令，或者监控其启动的进程是否停止。如果 `init` 的子进程之一停止运行，它会执行以下两项操作：

- 首先，它重新读取 `/etc/inittab` 文件。如果操作是重启该进程，它就会执行重启。
- 其次，它会在 `/etc/wtmp` 和 `/etc/utmp` 文件中记录该进程终止的事实及原因。这些文件将在第 10 章“管理任务”中讨论。

如果 `init` 被指示更改运行级别，或者收到断电通知，它也会重新读取 `/etc/inittab` 文件。

如果你想要修改 `/etc/inittab` 文件，可以在系统运行期间使用任何文本编辑器来更改该文件。然而，这些更改只有在 `init` 守护进程重新读取文件时才会生效。这种情况发生在以下时机：

- 运行级别发生变化时
- 发生断电时
- 你执行命令 `init q` 时

`init q` 命令会使 `init` 重新读取 `/etc/inittab` 文件。

编辑 `/etc/inittab` 文件时要格外小心，因为错误可能导致你无法登录系统。请备份原始的正确文件，并制作一张启动软盘以防出错。你或许可以尝试通过单用户模式启动来恢复，但这并不总是可行。偶尔，你在编辑 `/etc/inittab` 时可能会犯拼写错误，导致系统陷入循环，反复启动和停止某个进程。为防止这种情况发生，`init` 守护进程会跟踪重启进程的频率。如果一个进程在 2 分钟内被重启超过 10 次，`init` 守护进程将发送一条错误消息，并等待 5 分钟后再重启该进程。

![](img/8c0f494a2e9a2273fb49af52267f311e_49_0.png)

## LILO

`LILO`（LI**n**ux LOader）是一个引导加载程序，可以放置在你的硬盘或启动软盘上。它在系统启动时执行。`LILO` 的功能包括以下内容：

- 适用于 DOS、UNIX、OS/2、Windows 95/98 和 Windows NT
- 替换你硬盘上的主引导记录（Master Boot Record）
- 可以在不同的分区上使用多达 16 个不同的引导映像，每个映像都可以设置密码保护
- 允许引导扇区文件、映射文件和引导映像位于不同的分区上

`LILO` 具备作为其他操作系统引导加载程序的能力。它允许你选择要启动的操作系统。

> **关键概念**
>
> `LILO` 提供了一种高效的方法来启动 Linux 以及其他操作系统。`LILO` 可以在单个硬盘上处理多达 16 个不同的引导映像。
>
> 安装 `LILO` 时，你可以选择是否覆盖主引导记录。

如果没有做出选择，通常会启动默认的操作系统。你可以通过按下某个键（`Alt`、`Shift` 或 `Ctrl` 键）或在 `/etc/lilo.conf` 文件中请求提示符来绕过此默认行为。这些操作中的任何一个都会使 `LILO` 显示引导提示符：

`BOOT:`

此时，你可以输入要启动的操作系统名称。如果在 `LILO` 引导提示符下按下 `Tab` 键或输入 `?`，将显示已配置的操作系统列表。如果你没有做出选择，`LILO` 将启动它找到的第一个操作系统。

在引导提示符下输入选择项时，你可以向内核传递选项。这通常用于通过输入以下内容以单用户模式启动系统：

```
kernelName single
```

在引导提示符下输入。其他可以传递的选项包括 `root=device`、只读模式（`ro`）和读写模式（`rw`）。

`LILO` 的行为由其默认配置文件 `/etc/lilo.conf` 控制。`LILO` 命令有多种用途，其语法为：

```
lilo [options]
```

要安装 `LILO`，只需调用它而不带任何选项。`LILO` 可使用的选项列在表 2.3 中。

## 表 2.3 可用于 LILO 的选项

| **选项** | **操作** |
| :--- | :--- |
| `-b bootdev` | 指定引导设备 |
| `-C filename` | 使用指定的配置文件 |
| `-c` | 通过合并相邻扇区的读取来加快启动速度 |
| `-D label` | 使用带有给定标签的内核作为默认值 |
| `-D deciseconds` | 指示等待选择的时间长度 |
| `-f filename` | 指定磁盘参数文件；默认为 `/etc/disktab` |
| `-I` | 询问内核路径 |
| `-i filename` | 识别用作引导扇区的文件；默认为 `/boot/boot.b` |
| `-L` | 生成线性扇区地址 |
| `-m filename` | 使用指定的映射文件代替默认文件 |
| `-P [fix|ignore]` | 修复或忽略损坏的分区表 |
| `-q` | 列出从 `/boot/map` 文件引导的内核名称和位置 |
| `-R command` | 设置下次重启的默认值 |
| `-r directory` | 在更改其他内容之前更改根目录；用于故障排除 |
| `-S filename` | 覆盖现有文件 |
| `-s filename` | 指定旧引导扇区的存储位置；与 `-u` 一起使用时，指定要恢复的引导扇区 |
| `-t` | 测试你的配置而不进行安装 |
| `-u` 或 `-U` | 卸载 `LILO` |
| `-v` | 使 `LILO` 显示信息；多个 `-v` 可以增加显示的信息量 |

大多数情况下，调用 `LILO` 时使用配置文件而不是命令行。在创建配置文件时，你使用关键字代替表 2.3 中显示的选项。可用的关键字列在表 2.4 中。

## 表 2.4 LILO 配置文件中可用的关键字及其对应选项

| 关键字 | 选项 |
| :--- | :--- |
| `-b bootdev` | `boot=bootdev` |
| `-c` | `compact` |
| `-d ceciseconds` | `delay=dsec` |
| `-D label` | `default=label` |
| `-i filename` | `install=bootsector` |
| `-f filename` | `disktab=file` |
| `-l` | `linear` |
| `-m filename` | `map=mapi file` |
| `-P fix` | `fix-table` |
| `-P ignore` | `ignore-table` |
