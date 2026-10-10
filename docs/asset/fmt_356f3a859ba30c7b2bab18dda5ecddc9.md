
Ubuntu 一直从 SysVinit 配置向更干净、更灵活的 Upstart 配置转变。随着更多的系统服务纳入 Upstart 的控制，`/etc/init` 目录中的条目（参见第 440 页的提示）将替代 `/etc/init.d` 和 `/etc/rc?.d` 目录的内容。运行级别将不再是 Ubuntu 的正式特性，尽管为了与第三方软件兼容而会被保留。最终，Upstart 也将替代 `crond`。

## 软件包

Upstart 系统包含在一个软件包中，该软件包默认安装：

- **`upstart`**——提供 Upstart init 守护进程和 `initctl` 实用程序。

### 定义

事件是可以传达给 `init` 的状态变化。几乎任何状态变化——无论是对系统内部还是外部——都可以触发一个事件。例如，引导加载程序触发 `startup` 事件（参见 `startup` man 手册页），而 `telinit` 命令（第 444 页）触发 `runlevel` 事件（第 444 页）。移除和安装热插拔（第 502 页）或 USB 设备（如打印机）也可以触发事件。你还可以通过输入 `initctl emit` 命令（第 436 页）手动触发事件。更多信息请参考第 437 页的“事件”。

作业是 `init` 读取的一系列指令。这些指令通常包括一个程序（二进制文件或 shell 脚本）和一个事件名称。当事件被触发时，Upstart init 守护进程运行该程序。你可以通过分别输入 `initctl start` 和 `stop` 命令（第 436 页）手动运行和停止作业。

作业分为任务和进程。默认情况下，作业是一个服务；你必须明确指定某个作业为任务，它才能作为任务运行。

- **任务：** 任务是执行其工作后返回等待状态的作业。任务会阻塞发出触发该任务的信号的程序/进程，直到其指定的程序运行完毕。第 438 页描述的 `rc` 任务是任务的一个例子。

- **服务：** 服务是通常不会自行终止的作业。例如，`logd` 守护进程和 `getty` 进程（第 439 页）作为服务实现。init 守护进程监控每个服务，如果服务失败则重新启动服务，如果服务被手动或事件停止则终止服务。服务会阻塞发出触发该服务的信号的程序/进程，直到其指定的程序开始运行。

- **作业定义文件：** `/etc/init` 目录包含作业定义文件（定义 Upstart init 守护进程运行的作业的文件）。最初，该目录由 Upstart 软件包填充。安装某些服务时，会向此目录添加文件以控制该服务，替代在以前安装服务时放置在 `/etc/rc?.d` 和 `/etc/init.d` 目录中的文件。

- **init 是一台状态机：** 在其核心部分，Upstart init 守护进程是一台状态机。它跟踪作业的状态，并随着事件被触发，跟踪作业状态的变化。当 `init` 跟踪作业从一种状态变到另一种状态时，它可能会执行该作业的命令或终止该作业。

- **运行级别仿真：** System V init 守护进程使用运行级别的变化（第 443 页）来确定何时启动和停止进程。依赖 Upstart init 守护进程的 Ubuntu 系统没有运行级别的概念。为了便于从基于运行级别的系统迁移到基于事件的系统，并为了提供与其他发行版软件兼容性，Ubuntu 使用 Upstart 仿真运行级别。

由 `/etc/init/rc.conf` 文件定义的 `rc` 任务运行 `/etc/init.d/rc` 脚本。该脚本进而从 `/etc/rc?.d` 目录中的链接运行 `/etc/init.d` 中的 init 脚本，在 SysVinit 下仿真这些链接的功能。`rc` 任务在系统进入运行级别时运行这些脚本；通常当系统离开运行级别时不采取任何行动。参见第 438 页关于 `rc` 任务的讨论和第 440 页关于 init 脚本的信息。Upstart 实现 `runlevel`（第 444 页）和 `telinit`（第 444 页）实用程序以提供与 SysVinit 系统的兼容性。

**`initctl`：** `initctl`（init 控制）实用程序与 Upstart init 守护进程通信。普通用户可以使用 `initctl list` 和 `status` 命令查询 Upstart init 守护进程。具有 **root** 权限的系统管理员既可以查询该守护进程，也可以启动和停止作业。例如，`initctl list` 命令列出作业及其状态：

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

有关更多信息，请参阅 `initctl` 手册页和本节中的示例。你可以输入命令 `initctl help`（help 前无需连字符）来显示 `initctl` 命令列表。或者，你可以输入以下命令来显示关于 `list` 命令的更多信息：

```bash
$ initctl list --help
   Usage: initctl list [OPTION]...
   List known jobs.

   Options:
      --system use D-Bus system bus to connect to init daemon
      --dest=NAME destination well-known name on system bus
      -q, --quiet reduce output to errors only
      -v, --verbose increase output to include informational messages
      --help display this help and exit
      --version output version information and exit
```

已知的任务及其当前状态将被输出。

向 `<upstart-devel@lists.ubuntu.com>` 报告 bug

将 `list` 替换为你希望获取更多信息的 `initctl` 命令。`start`、`stop`、`reload` 和 `status` 实用工具是指向 `initctl` 的链接，它们分别执行以其命名的 `initctl` 命令。

## 任务（JOBS）

`/etc/init` 目录中的每个文件都定义一个任务，通常至少包含一个事件和一个命令。当事件被触发时，`init` 会执行该命令。本节介绍了管理员定义的任务和随 `upstart` 包安装的任务的示例。

### 管理员定义的任务（ADMINISTRATOR-DEFINED JOBS）

以下由管理员定义的任务使用 `exec` 关键字来执行 shell 命令。你也可以使用此关键字来执行存储于文件中的 shell 脚本或二进制可执行文件。

> 在第一个语句中（`start on runlevel 2`），`start on` 是一个关键字（你可以用 `stop on` 替代它），`runlevel` 是一个事件（第 433 页），而 `2` 是 `runlevel` 的参数。

```bash
$ cat /etc/init/mudat.conf
start on runlevel 2
task
exec echo "Entering multiuser mode on " $(date) > /tmp/mudat.out
```

此文件定义了一个任务：当系统进入多用户模式（runlevel 2）时，它运行 `echo` shell 命令。该命令将包含时间和日期的写入 `/tmp/mudat.out`。shell 使用命令替换（第 362 页）来执行 `date` 实用工具。在此任务运行完成后，`mudat` 任务停止并进入等待状态。

在下一个示例中，`cat` 实用工具显示 `/tmp/mudat.out` 文件的内容，而 `initctl` `list` 命令和 `status` 实用工具报告此任务的状态：

```bash
$ cat /tmp/mudat.out
Entering multiuser mode on Wed Mar 10 11:58:14 PST 2010

$ initctl list | grep mudat
mudat stop/waiting

$ status mudat
mudat stop/waiting
```

如果 `exec` 命令行包含 shell 特殊字符（第 160 页），`init` 将执行 `/bin/sh`（指向 `dash` [第 292 页] 的链接）并将命令行传递给 shell。否则，`exec` 将直接执行命令行。要运行多个 shell 命令，可以使用 `exec` 来运行存储于文件中的 shell 脚本，或者使用 `script...end script`（将在下文讨论）。

Upstart `init` 守护进程只能监控使用 `exec` 执行程序的 任务（服务）；它无法监控使用 `script...end script` 运行的任务。换句话说，`services`（服务）需要使用 `exec`，而 `tasks`（任务）可以使用这两种方法中的任意一种来运行程序。未来版本的 Upstart `init` 守护进程将能够监控这些任务。

### `myjob` 示例

你还可以定义一个事件，并设置一个由该事件触发 的任务。`myjob.conf` 任务定义文件定义了一个由 `hi` `there` 事件触发 的任务：

```bash
$ cat /etc/init/myjob.conf
start on hi there
script
    echo "Hi there, here I am!" > /tmp/myjob.out
    date >> /tmp/myjob.out
end script
```

`myjob` 文件展示了另一种执行命令的方式：它在 `script` 和 `end script` 关键字之间包含两行命令。这些关键字始终会导致 `init` 执行 `/bin/sh`。这些命令将消息和日期写入 `/tmp/myjob.out` 文件。你可以使用 `initctl` `emit` 命令来触发此任务。

### `initctl emit`

```bash
$ sudo initctl emit hi there

$ cat /tmp/myjob.out
Hi there, here I am!
Wed Mar 10 11:59:23 PST 2010

$ status myjob
myjob stop/waiting
```

### `initctl start` 和 `stop`

在上面的示例中，`cat` 显示了 `myjob` 生成的输出，而 `initctl` 显示了任务的状态。你可以通过输入命令 `initctl` `start` `myjob`（或仅 `start` `myjob`）来运行相同的任务。`initctl` `start` 命令在你希望不触发事件就运行任务时很有用。例如，你可以使用命令 `initctl` `start` `mudat` 来运行前一个示例中的 `mudat` 任务，而无需触发 `runlevel` 事件。

## 事件（EVENTS）

`upstart` 包定义了许多事件。以下命令列出事件及其简要描述。有关每个事件的更多信息，请参阅相应的手册页。

```bash
$ apropos event 2>&1 | grep signalling
all-swaps (7)          - event signalling that all swap partitions have been activated
control-alt-delete (7) - event signalling console press of Control-Alt-Delete
filesystem (7)         - event signalling that filesystems have been mounted
keyboard-request (7)   - event signalling console press of Alt-UpArrow
local-filesystems (7)  - event signalling that local filesystems have been mounted
mounted (7)            - event signalling that a filesystem has been mounted
mounting (7)           - event signalling that a filesystem is mounting
power-status-changed (7) - event signalling change of power status
remote-filesystems (7) - event signalling that remote filesystems have been mounted
runlevel1 (7)          - event signalling change of system runlevel
started (7)            - event signalling that a job is running
starting (7)           - event signalling that a job is starting
startup (7)            - event signalling system startup
stopped (7)            - event signalling that a job has stopped
stopping (7)           - event signalling that a job is stopping
virtual-filesystems (7) - event signalling that virtual filesystems have been mounted
```

`apropos` 实用工具（第 139 页）是 `whatis` 的链接，它将输出发送到标准错误。`2>&1` 运算符是一种重定向，它将 `apropos` 的标准错误（第 297 页）发送到 `grep` 的标准输入。

### 指定带参数的事件（Specifying Events with Arguments）

`telinit`（第 444 页）和 `shutdown`（第 450 页）实用工具发出包含参数 的 runlevel 事件。例如，`shutdown` 发出 `runlevel 0`，而 `telinit 2` 发出 `runlevel 2`。你可以在任务定义中使用以下语法匹配这些事件：

`start|stop on event [arg [arg...]]`

其中 `event` 是诸如 `runlevel` 之类的事件，而 `arg` 是一个或多个参数。要在系统从 runlevel 1 进入 runlevel 2 时停止任务，请指定 `stop on runlevel 2 1`。你还可以指定 `[235]` 来匹配 2、3 和 5，或使用 `[!2]` 来匹配除 2 以外的任何值。

#### 事件参数（Event arguments）

虽然 Upstart 会忽略事件中的额外参数，但任务定义文件中事件名称内的额外参数必须在事件中存在。例如，任务定义文件中的 `runlevel`（无参数）匹配所有 `runlevel` 事件（无论参数如何），而 `runlevel 5 arg1 arg2` 不匹配任何 `runlevel` 事件，因为 `runlevel` 事件接受两个参数（系统正在进入的 runlevel 和之前的 runlevel）。

### `/etc/init` 中的任务定义文件（JOB DEFINITION FILES IN /etc/init）

随着 Ubuntu 继续从 SysVinit 向 Upstart init 过渡，将在 `/etc/init` 目录中定义更多任务。本节介绍了 `upstart` 包放入此目录中的一些任务。

`runlevel` 事件（[`runlevel(7)` 手册页]）表示 runlevel 的变化，并由 `telinit`（第 444 页）和 `shutdown`（第 450 页）发出。此事件将环境变量 `RUNLEVEL` 设置为新 runlevel 的值，并将 `PREVELEVEL` 设置为之前 runlevel 的值。

`/etc/init/rc.conf` 任务定义文件定义了 `rc` 任务。此任务监控 `runlevel` 事件。文件末尾附近的 `task` 关键字将此任务指定为任务而非服务。因为它是一个任务，所以在 `rc` 任务完成运行之前，它会阻塞发出 `runlevel` 事件的调用。

`rc.conf` 中的 `exec` 语句以 `$RUNLEVEL` 作为参数调用 `/etc/init.d/rc` 脚本（不是 `rc` 任务）。`rc` 脚本调用 `/etc/rcn.d` 目录中的链接，其中 `n` 等于 `RUNLEVEL`（第 440 页）。因此，当 `RUNLEVEL` 设置为 2 时调用 `rc` 任务，它会运行 `/etc/rc2.d` 目录中的链接所指向的初始化脚本。

当系统从 0 到 6 的任意 runlevel 进入时，`rc` 任务会运行 `rc` 脚本（`start on runlevel [0123456]`）。通常，当 `rc` 任务完成执行 `rc` 脚本后就会终止。
