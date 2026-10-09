
当你输入 `su` 命令时，你会获得一个常规 shell。当你输入命令 `su -`（你可以使用 `-l` 或 `--login` 代替连字符）时，你会获得一个 **root** 登录 shell：这就像你以 **root** 身份登录了一样。不仅 shell 的用户和组 ID 与 **root** 的匹配，而且环境也与 **root** 的完全相同。登录 shell 在显示提示符之前会执行相应的启动文件（第 293 页）。

`id` 实用程序会显示你的用户和组 ID 以及你所关联的组的变化：

```bash
$ id
uid=1002(sam) gid=1002(sam) groups=117(admin),1002(sam)
$ su
Password:
# id
uid=0(root) gid=0(root) groups=0(root)
```

你可以使用带有 `-c` 选项的 `su` 以 **root** 权限运行一条命令行，当命令执行完毕时返回到原始 shell。下面的例子首先表明用户不被允许终止（第 455 页）进程。然而，通过使用 `su -c` 和 **root** 密码，用户被允许终止该进程。引号是必需的，因为 `su -c` 将其命令作为单个参数接受。

```bash
$ kill -15 4982
-bash: kill: (4982) - Operation not permitted
$ su -c "kill -15 4982"
Password:
$
```

### 超级用户、PATH 与安全

> 当你以 **root** 身份工作时，你在 **PATH** 中保留的目录越少，你就越不可能以 **root** 身份执行不可信的程序。永远不要将工作目录包含在 **PATH** 中（例如 `.`, `*`, 或 **PATH** 中的 `anywhere`，或者作为 **PATH** 的最后一个元素）。更多信息请参考第 319 页的“PATH：Shell 在哪里查找程序”。

## UPSTART 基于事件的 INIT 守护进程

由于传统的 System V **init** 守护进程（SysVinit）无法很好地处理现代硬件，包括热插拔（第 502 页）设备、USB 硬盘和闪存盘以及网络挂载的文件系统，Ubuntu 用 Upstart **init** 守护进程（upstart.ubuntu.com 和 upstart.ubuntu.com/wiki）替换了它。

还有其他几种 SysVinit 的替代方案可用。其中最著名的是 **init**（initng.sourceforge.net/trac）。此外，Solaris 使用 **SMF**（服务管理设施），而 macOS 使用 **launchd**。随着时间的推移，Ubuntu 会将这些每个系统的特性融入到 Upstart 中。

基于运行级别的 SysVinit 守护进程使用运行级别（恢复/单用户、多用户等）和从 `/etc/rc.d/` 目录链接到 `/etc/init.d` 中的 init 脚本来启动和停止系统服务（第 440 页）。基于事件的 Upstart init 守护进程使用事件来启动和停止系统服务。在 Feisty 版本（7.04）中，Ubuntu 切换到 Upstart init 守护进程，并开始从 SysVinit 配置向 Upstart 配置过渡。本节讨论 Upstart 和仍然保留的 SysVinit 部分：`/etc/rc?.d` 和 `/etc/init.d` 目录以及运行级别的概念。参见第 445 页关于术语的提示。

Upstart init 守护进程是基于事件的，当系统中某些东西发生变化时，它会运行指定的程序。这些程序（通常是脚本）启动和停止服务。这种设置在概念上类似于 SysVinit 在进入运行级别时调用的 init 脚本链接，只是 Upstart 更加灵活。Upstart 不仅限于在运行级别变化时启动和停止服务，还可以在其接收到系统中某些东西已改变的信息时启动和停止服务。这种改变被称为事件。例如，当 Upstart 从 `udev`（第 502 页）得知文件系统、打印机或其他设备已被添加或从运行系统中移除时，它可以采取措施。它还可以在系统启动、系统关闭或作业状态改变时启动和停止服务。

从 SysVinit 转换到 Upstart 涉及 Linux 系统的许多部分。为了平滑地进行转换并尽可能减少错误，Upstart 团队选择在这个跨多个版本中进行过渡。

Ubuntu 一直从 SysVinit 配置向更干净、更灵活的 Upstart 配置转变。随着更多的系统服务纳入 Upstart 的控制，`/etc/init` 目录中的条目（参见第 440 页的提示）将替代 `/etc/init.d` 和 `/etc/rc?.d` 目录的内容。运行级别将不再是 Ubuntu 的正式特性，尽管为了与第三方软件兼容而会被保留。最终，Upstart 也将替代 `crond`。

## 软件包

Upstart 系统包含在一个软件包中，该软件包默认安装：

- **upstart**——提供 Upstart init 守护进程和 `initctl` 实用程序。

## 定义

事件是可以传达给 `init` 的状态变化。几乎任何状态变化——无论是对系统内部还是外部——都可以触发一个事件。例如，引导加载程序触发 `startup` 事件（参见 `startup` man 手册页），而 `telinit` 命令（第 444 页）触发 `runlevel` 事件（第 444 页）。移除和安装热插拔（第 502 页）或 USB 设备（如打印机）也可以触发事件。你还可以通过输入 `initctl emit` 命令（第 436 页）手动触发事件。更多信息请参考第 437 页的“事件”。

作业是 `init` 读取的一系列指令。这些指令通常包括一个程序（二进制文件或 shell 脚本）和一个事件名称。当事件被触发时，Upstart init 守护进程运行该程序。你可以通过分别输入 `initctl start` 和 `stop` 命令（第 436 页）手动运行和停止作业。

作业分为任务和进程。默认情况下，作业是一个服务；你必须明确指定某个作业为任务，它才能作为任务运行。

- **任务：** 任务是执行其工作后返回等待状态的作业。任务会阻塞发出触发该任务的信号的程序/进程，直到其指定的程序运行完毕。第 438 页描述的 `rc` 任务是任务的一个例子。

- **服务：** 服务是通常不会自行终止的作业。例如，`logd` 守护进程和 `getty` 进程（第 439 页）作为服务实现。init 守护进程监控每个服务，如果服务失败则重新启动服务，如果服务被手动或事件停止则终止服务。服务会阻塞发出触发该服务的信号的程序/进程，直到其指定的程序开始运行。

- **作业定义文件：** `/etc/init` 目录包含作业定义文件（定义 Upstart init 守护进程运行的作业的文件）。最初，该目录由 Upstart 软件包填充。安装某些服务时，会向此目录添加文件以控制该服务，替代在以前安装服务时放置在 `/etc/rc?.d` 和 `/etc/init.d` 目录中的文件。

- **init 是一台状态机：** 在其核心部分，Upstart init 守护进程是一台状态机。它跟踪作业的状态，并随着事件被触发，跟踪作业状态的变化。当 `init` 跟踪作业从一种状态变到另一种状态时，它可能会执行该作业的命令或终止该作业。

- **运行级别仿真：** System V init 守护进程使用运行级别的变化（第 443 页）来确定何时启动和停止进程。依赖 Upstart init 守护进程的 Ubuntu 系统没有运行级别的概念。为了便于从基于运行级别的系统迁移到基于事件的系统，并为了提供与其他发行版软件兼容性，Ubuntu 使用 Upstart 仿真运行级别。

由 `/etc/init/rc.conf` 文件定义的 `rc` 任务运行 `/etc/init.d/rc` 脚本。该脚本进而从 `/etc/rc?.d` 目录中的链接运行 `/etc/init.d` 中的 init 脚本，在 SysVinit 下仿真这些链接的功能。`rc` 任务在系统进入运行级别时运行这些脚本；通常当系统离开运行级别时不采取任何行动。参见第 438 页关于 `rc` 任务的讨论和第 440 页关于 init 脚本的信息。Upstart 实现 `runlevel`（第 444 页）和 `telinit`（第 444 页）实用程序以提供与 SysVinit 系统的兼容性。

**initctl：** `initctl`（init 控制）实用程序与 Upstart init 守护进程通信。普通用户可以使用 `initctl list` 和 `status` 命令查询 Upstart init 守护进程。具有 **root** 权限的系统管理员既可以查询该守护进程，也可以启动和停止作业。例如，`initctl list` 命令列出作业及其状态：

```bash
$ initctl list
alsa-mixer-save savp/waiting
avahi-daemon start/running, process 509
mountall-net stop/waiting
rc stop/waiting
rsyslog start/running, process 463
tty4 start/running, process 695
udev start/running, process 252
...
```

