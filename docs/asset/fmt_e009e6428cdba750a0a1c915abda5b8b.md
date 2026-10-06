
在 SysVinit 系统中，你有一组从 0 到 6 定义的运行级别。运行级别本质上是一个集合。

在 systemd 中，目标（targets）是新的运行级别。例如，`default.target` 文件通常是另一个目标文件（如 `graphical.target`）的符号链接。目标直接对应表 2-3 所示的 SysVinit 运行级别：

| 运行级别 | 文件 | 操作 |
| --- | --- | --- |
| 0 | poweroff.target | 关闭系统电源 |
| 1 | rescue.target | 配置救援 shell |
| 2 | multi-user.target | 设置系统为非图形多用户模式，通常没有网络服务 |
| 3 | multi-user.target | 设置系统为非图形多用户模式，带有网络服务 |
| 4 | multi-user.target | 与 3 相同 |
| 5 | graphical.target | 设置系统为图形多用户模式，带有网络服务 |
| 6 | reboot.target | 关闭并重启系统 |

### 表 2-3 运行级别和目标启动时发生的情况

表 2-3 显示了运行级别与目标之间的对应关系，并描述了启动运行级别或目标时发生的动作。

> 注意
> 还有另一种标记方式，即 `runlevel#.target`，其中 `#` 字符代表 0-6。这是为了兼容性。

### Wants 和 Requires

系统过程使用被称为“wants”和“requires”的选项或需求来指示单元之间的依赖关系。例如，如果你查看 `graphical.target` 文件的典型内容，可能会发现以下行：

```
Requires=multi-user.target
After=multi-user.target
Wants=display-manager.service
```

`Requires` 语句意味着在处理 `graphical.target` 之前，必须启动 `multi-user.target` 中的所有项。只有在满足该要求后，才会处理 `Wants` 语句（再次意味着启动相关的链接服务）。

目录，这次是（`/usr/lib/systemd/multi-user.target.wants` 目录），之后将使用 graphical.target。

### 使用 systemd 启动

在启动使用 systemd 的系统时，之前概述的相同步骤同样适用，仅当系统从 GRUB 启动 systemd/init 时，系统上层叠了一个类似于 SysVinit init 脚本结构的结构。

![](img/16cd7204aa58beaaf530d67f50f15fc5_93_0.png)

在内核和 initramdisk 之后读取的文件通常是 `default.target` 文件。该文件仅仅是指向 `multi-user.target` 文件的符号链接。这里情况变得奇怪起来，因为虽然启动过程看起来很简单（如示例 2-1 所示），但实际上并非如此。

### 示例 2-1 启动过程的理论层级

点击此处查看代码图像

```
Kernel
|
multi-user.target
|
graphical.target
```

实际情况是，`graphical.target` 需要 `multi-user.target`，而后者需要 `basic.target`，而 `basic.target` 又需要 `sysinit.target`。所有这些都必须成功加载其配置的服务才能继续后续操作，因此真实的启动顺序如示例 2-2 所示。

### 示例 2-2 启动过程的实际层级

点击此处查看代码图像

```
local-fs-pre.target
|
```

```
sysinit.target -- wants local-fs.target and swap.target
| 
basic.target -- wants
| 
multi-user.target -- wants
| 
graphical.target -- wants
```

需要一些时间来理解 systemd 的工作方式，但在实践中，它与 SysVinit 及其在多个目录中的几十个链接并没有太大区别。

### Upstart

特别值得注意的是 Upstart 系统初始化方案，其设计目标非常简单：

- 异步操作——Upstart 处理启动期间的运行启动、关机期间的运行停止，以及在正常系统运行期间的服务运行。
- 易于实现——由于与 sysinit 兼容，Upstart 极易过渡到它。
- 向后兼容性——Upstart 可以运行不经修改的 sysvinit 脚本，并在混合系统初始化环境中表现良好。
- 可扩展性——Upstart 具有卓越的可扩展性，允许更多的输入、事件、自定义任务和服务等。

遗憾的是对于 Upstart 来说，Linux 发行版世界通常倾向于转向 systemd，或者保留 SysVinit，最公开的背离是 Ubuntu，以保持与上游 Debian 代码库和方法的兼容性。

> 注意
> 谷歌的 Chrome OS 以及 Chromebook 上的操作系统使用了 Upstart，因此日益越来越多的系统正在利用 Upstart 的功能。

## 管理系统运行级别 (Runlevels)

能够正确管理系统的运行级别意味着你将能够以可预测的方式在适当模式下运行系统，启用正确的服务且准备就绪。

![](img/16cd7204aa58beaaf530d67f50f15fc5_95_0.png)

### 确定默认运行级别

在 SysVinit 系统上，确定运行级别很简单：你执行 `runlevel` 命令，它会返回以下输出：

```
N 2
```

第一列（包含字符 N）显示没有先的运行级别，因此系统已启动并到达运行级别 2（输出中的第 2 列），而没有经过任何运行级别 1 等中间步骤。

> 注意
> 如果你看到之前的运行级别（例如“1”）然后是当前运行级别（在此例中为“2”），你应该确定你或另一个有效的系统管理员由于某种理由负责将系统进入单用户模式，否则系统可能被篡改过。

此外，你可能可以运行 `who -r` 命令获取额外的、更像英语句的输出：

点击此处查看代码图像

```
run-level 2 2015-03-01 10:14
```

![](img/16cd7204aa58beaaf530d67f50f15fc5_95_1.png)

在运行的 systemd 中，你可以使用 `systemctl get-default` 来确定默认 target。输出是符号链接指向的 target 解析后的名称，例如

```
multi-user.target
```

> 运行级别是互斥的，而 target 不是。换句话说，只能有一个运行级别可以是当前运行级别，而你实际上可以有多个激活 target。

要确定所有激活的 target，请使用 `systemctl list-units --type=target` 命令。输出是激活的 target 文件名，例如

```
multi-user.target
graphical.target
```

![](img/16cd7204aa58beaaf530d67f50f15fc5_96_0.png)

### 设置默认运行级别

在 SysVinit 系统上，设置默认运行级别仅需选择你想要的运行级别，并编辑 `/etc/initab` 文件，将 `id:5default:` 修改为反映你想要的运行级别数字（将数字 5 替换为所需的数字）。

在 systemd 机器上，你可以通过指定 target 来设置默认 target：

```
systemctl set-default graphical.target
```

### 更改运行级别

在 SysVinit 系统上，更改运行级别涉及 `init` 命令。

> 注意
> `/sbin/init` 命令是为了历史目的而存在的，或者你仍然在使用它。

要将运行级别设置为 3，执行：

```
init 3
```

在 systemd 机器上，你可以通过执行以下命令将当前 target 设置单用户模式：

点击此处查看代码图像

```
systemctl isolate multi-user.target
```

或者

点击此处查看代码图像

```
systemctl isolate 3
```

等等，文中说：

点击此处查看代码图像

```
systemctl isolate graphical.target
```

在 systemd 机器上，你可以通过以下方式设置当前 target：

```
systemctl isolate graphical.target
```

### 从命令行关机和重启

正确关闭系统对于保存数据非常重要，但在运行的系统中直接掉电源几乎会导致问题。

在 SysVinit 系统上，你可以使用多个命令关闭系统，首先是

`halt -p`

这会停止系统然后关机。

![](img/16cd7204aa58beaaf530d67f50f15fc5_97_0.png)

更常用的命令是 `shutdown` 命令，它提供了多个选项：

- `H`, `--halt`——停止机器但不关机。
- `P`, `--poweroff`——停止并关机机器。
- `r`, `--reboot`——在关机后重启机器。
- `k`——不关机、停止或重启，只是写一条墙信息（也称为 -K）。此选项旨在希望吓跑用户离开系统，以便执行关键任务。

关闭系统机器可以像之前概述 SysVinit 命令和选项那样进行，你也可以使用 `systemctl` 命令，如下：

- `systemctl halt`——如其名：停止系统；不关机。
- `systemctl poweroff`——关机（停止系统）并电源。
- `systemctl reboot`——关机（停止系统）然后重启系统。

> 注意
> 在不是 root 用户的系统中，或者 root 用户账户未用于常规管理，请在 `systemctl` 命令前加上 `sudo` 命令。你的账户必须设置 `sudo` 命令才能使用，但一旦完成，你就可以运行 `systemctl` 命令，如
> `sudo systemctl reboot`

### 通知用户

在任何关于关机、停止或重启系统的章节中，如果不讨论如何通知受系统状态变化的用户，都是完整的。

由于关机在定义上是有序的关机，系统进程已经收到了充分的警告称即将关闭，但用户通常希望有更多的时间和能力完成当前的工作。

> 注意
> `shutdown` 命令包含了你为了正确通知用户即将到来的关机而需要的所有内容，包括在关机开始不久后禁用新用户登录的功能。

例如，你可以使用绝对命令安排系统在今天下午 7:00 关机：

```
shutdown 19:00
```

你也可以使用相对表示法来指定关机时间，例如在 20 分钟后关机，命令为：

```
shutdown +20
```

![](img/16cd7204aa58beaaf530d67f50f15fc5_99_0.png)

你可以通过命令将时间指定与向所有登录用户（登录到控制台的用户，而非网络共享连接的用户）发送通知相结合：

点击此处查看图像

```
shutdown +30 "System going down in 30 minutes, save your work and log off!"
```

> 注意
> KDE 桌面具有一个守护进程，用于监控登录的图形用户界面 (GUI) 用户的系统重启。你只需要发出正确的关机命令，KDE 系统就会通知用户关机。

如果你安排了未来的关机，可以通过执行带有 -c 选项的 shutdown 命令来取消：

```
shutdown -c
```

### 正确终止进程

系统管理员经常必须终止那些无法或不会正常结束，或者无法根据父进程要求结束的进程。能够在进程表中找到这些进程并根据 PID（进程 ID）逐个杀死它们，或根据进程名批量杀死它们是非常关重要的。

![](img/16cd7204aa58beaaf530d67f50f15fc5_100_0.png)

### kill 和 killall

控制守护进程还包括使用 `kill` 和 `killall` 命令，它们分别作用于 PID 和命令名。

`kill` 和 `killall` 使用相同的信号；除了使用 PID 和名称外，它们在功能上是相似的。`kill` 命令非常简单，但你首先需要找到想要杀掉的进程的 PID 或进程 ID。要找到你系统中 smb 进程的 PID，请运行命令：

```
ps aux | grep
```

这将返回此处所示的输出：

点击此处查看图像

```
root 388 0.0 0.9 2460 ? S 00:38 /usr/sbin/smbd -D
```

然后你取第二列的数字即 PID，并将其作为参数提供给 `kill` 命令：

```
kill 388
```

如果程序没有，或者它是僵尸进程的父进程（一种已经完全消失以至于无法响应有效的 kill 或 SIGTERM 命令的进程），请使用绝对 kill 或带有 -9 选项的 kill 命令来发送 SIGKILL 信号，例如：

```
kill -9 388
```

`killall` 命令的工作原理类似。你可以通过运行的实际命令（即 ps 输出的最后一列）来命名失控的或不需要的进程。

要杀死你机器上所有正在运行的 Mozilla 浏览器实例，以 root 身份你只需输入：

```
killall mozilla-bin
```

如果由于某种原因浏览器没有响应，请使用带有 `-9` 选项的 `kill` 命令来发送 SIGKILL 或绝对 kill，如下所示：

```
kill -9 mozilla-bin
```

这将强制从内存中移除进程，而甚至不会允许它们清理内存和磁盘进程。因此，请注意，使用 `kill` 和 `killall` 命令强制终止进程可能会导致时间推移产生的内存使用问题，甚至可能导致你花一些高质量的时间处理 fsck。

![](img/16cd7204aa58beaaf530d67f50f15fc5_101_0.png)

### 重新加载或“挂起”进程

当你运行具有许多活动系统服务并为多个客户端提供资源访问的服务器时，并不总是能够通过重启系统来使配置文件的所有更改生效。

重启系统进程（如 Apache、Samba 或 Syslog）并使其重新加载配置的方便方法是使用 SIGHUP 信号。本质上，此信号会导致进程简单地重新加载其配置文件，从而在不中断连接或客户端访问的情况下应用任何新的配置选项。

发送 SIGHUP 信号的形式如下：

```
kill -HUP 2112
```

此外，你也可以使用数字信号 -1 来完成相同的进程配置文件的重新加载。

### 记录启动事件

当你运行 SysVinit 系统时，启动日志相对简单：你可以使用 `dmesg` 命令查看上一次系统启动的输出。此输出也将与主系统日志（通常为 `/var/log/messages` 或 `/var/log/syslog`）中的其他项目混合。

当你使用 `dmesg` 命令时，你看到的并不是日志文件，而是由内核环形缓冲区（运行内核的一个部分）生成的消息。

> 注意
> 在某些发行版中，初始化脚本可能会将这些内核环形缓冲区消息发送到配置的日志系统和日志文件（如 `/var/log/messages`）。

相比之下，系统将所有日志信息保存在 systemd/journald 中。要查看特定的启动，使用 systemctl 命令：

```
journalctl --list-boot
```

这将返回此处所示的输出：

点击此处查看图像

![](img/16cd7204aa58beaaf530d67f50f15fc5_102_png)

例如，要列出启动，执行以下命令：

```
journalctl --boot
```

- a. `/etc/group`
- b. 组标签
- c. `groupmod`
- d. `gkill`

4. 下列哪个命令模拟系统关机事件，但不会实际关闭系统？

- a. `shutdown -h`
- b. `shutdown -k`
- c. `shutdown -r`
- d. `shutdown -c`

5. 你编辑了名为 `daemon1` 的服务的配置文件，需要该服务重新读取配置并继续为其连接的客户端进程提供服务。以下哪些可以实现这一目标？选择所有适用项。

- a. `kill -s SIGHUP daemon1`
- b. `kill -15 daemon1`
- c. `kill -9 daemon1`
- d. `kill -HUP daemon1`
- e. `kill -1 daemon1`

6. 在上一次系统启动期间，你注意到几条错误信息快速掠过屏幕且无法查看。你不确定使用的是哪种系统初始化方案。下列哪个命令可能仅显示最近一次系统启动的消息？（选择三项）

- a. `systemctl --viewboot`
- b. `journalctl -b`
- c. `syslog --boot`
- d. `dmesg`
- e. `cat /var/log/boot.msg`

## 第3章 软件包安装与管理

本章涵盖了以下主题：

- Linux 系统中的软件
- Debian 管理
- RPM 和 YUM 软件包管理

本章涵盖的考试目标是：

- 管理共享库：102.3
- 使用 Debian 软件包管理：102.4
- 使用 RPM 软件包管理：102.5

Linux 系统的目的应该是执行一些有用操作，例如读取电子邮件、浏览网页或作为某种应用程序服务器。Linux 内核非常强大，但它本身并做不了什么——为此，你需要软件。

Linux 有许多可用的软件；你只需要安装它们即可。你可以根据你的发行版以及软件的打包方式，通过几种方法安装软件。

曾经，软件是以源码形式分发的，这需要被编译成可以在计算机上运行程序。这种方式仍然存在，但作为一个社区，我们已经转向分发更容易安装的二进制包。二进制包不仅避免了编译步骤，而且依赖关系、库、配置和文档都会自动管理。这些软件包有几种不同的格式，但在大多数情况下，两种最流行：Debian 风格和 Red Hat 风格。
