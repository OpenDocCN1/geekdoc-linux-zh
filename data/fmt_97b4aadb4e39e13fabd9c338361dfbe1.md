
Usage: `initctl list [OPTION]...`

列出已知作业。

```
- --system 要连接到初始化守护进程的 D-Bus 系统总线
- --dest-NAME 系统总线上的目标已知名称
- -Q, --quiet 仅输出错误信息
- -V, --verbose 输出包含信息性消息
- --help 显示此帮助并退出
- --version 输出版本信息并退出
```

将输出已知的作业及其当前状态。

请向 `<upstart-dev@lists.ubuntu.com>` 报告漏洞。

将 `list` 替换为你想要获取更多信息的 `initctl` 命令。`start`、`reload` 和 `status` 实用程序是 `initctl` 的链接，它们运行与其同名的 `initctl` 命令。

## 作业 (JOBS)

`/etc/init` 目录下的每个文件定义了一个作业，通常通常包含一个事件和一个命令。当事件触发时，`init` 会执行该命令。这里描述了管理员定义的作业以及通过 `upstart` 包安装的作业的示例。

### 管理员定义的作业

以下管理员定义的作业使用 `exec` 命令来执行 shell 命令。你也可以使用此关键字执行存储在文件中的 shell 脚本或二进制可执行文件。

在第一个段落中（在运行级别 2 上启动），`start on` 是一个关键字（你可以用 `stop` 替换它），`runlevel` 是一个事件（第 433 页），`2` 是 `runlevel` 的参数。

```bash
$ /etc/init/mudat.conf

task

start on runlevel 2

exec echo "Entering multiuser mode on $(date)" > /tmp/mudat.out
```

此文件定义了一个任务：当系统进入多用户模式（运行级别 2）时执行 `echo` shell 命令。该命令将一条包含时间和日期的消息写入 `/tmp/mudat.out`。shell 使用命令替换（第 362 页）来执行 `date` 工具。在此作业运行完成后，`mudat` 任务停止并进入等待状态。

在下一个示例中，`cat` 工具显示 `/tmp/mudat.out` 文件的内容，`initctl` 命令显示了 `status` 实用程序对此任务的报告：

```bash
$ cat /tmp/mudat.out

Entering multiuser mode on Wed Mar 10 11:58:14 PST 2010
```

```bash
$ initctl list | grep mudat

mudat stop/waiting
$ status mudat

mudat stop/waiting
```

如果 `exec` 命令行包含 shell 特殊字符（第 160 页），它将执行 `/bin/sh`（指向 dash 的链接，第 292 页）并将命令行传递给 shell。否则，`exec` 将直接执行命令行。要运行多个 shell 命令，请使用 `exec` 运行存储在文件中的 shell 脚本，或者使用 `script...end script`（下文讨论）。

Upstart 初始化守护进程仅监控使用 `exec` 执行程序的作业（服务）；它无法监控使用 `script...end script` 的作业。另一种方法要求使用 `exec`，而任务可以使用任一一种方法运行程序。未来的 Upstart 初始化守护进程将能够监控这些作业。

你也可以定义一个事件并设置由该事件触发的作业。`myjob.conf` 定义文件定义了一个由 `hithere` 事件触发的作业：

```bash
$ cat /etc/init/myjob.conf

start on hithere

script

echo "Hi there, here I am!" > /tmp/myjob.out

date >> /tmp/myjob.out

end script
```

`myjob` 文件在 `script` 和 `end script` 关键字之间显示了两个命令。这些关键字始终会导致 `init` 执行 `/bin/sh`。命令将消息和数据写入 `/tmp/myjob.out`。你可以使用 `initctl emit` 来触发作业。

```bash
$ sudo initctl emit hithere
```

```bash
$ cat /tmp/myjob.out

Hi, here I am!

Wed Mar 10 11:59:23 PST 2010
```

```bash
$ status myjob

myjob stop/waiting
```

在前面的示例中，`cat` 显示了 `myjob` 生成的输出，`initctl` 显示作业的状态。你可以通过输入命令 `initctl start myjob`（或直接输入 `start myjob`）来运行相同的作业。`initctl start` 在你想在不触发事件的情况下运行作业时有用。例如，你可以使用命令 `initctl start mudat` 来运行之前示例中的 `mudat` 作业，而不会触发运行级别事件。

## 事件 (EVENTS)

`upstart` 包定义许多事件。以下命令列出了事件及其简要描述。有关每个事件的更多信息，请查看相应的 man 页。

- `$ apropos event 2 grep signalling`
- `all-swaps (7)` - 信号所有交换分区已激活的事件
- `control-alt-delete (7)` - 信号控制台按下 Control-Alt-Delete 的事件
- `filesystem (7)` - 信号文件系统已挂载的事件
- `keyboard-request (7)` - 信号控制台按下 Alt-上箭头的事件
- `local-filesystems (7)` - 信号本地文件系统已挂载的事件
- `mounted (7)` - 信号某个文件系统已挂载的事件
- `mousing (7)` - 信号文件系统正在挂载的事件
- `power-status-changed (7)` - 信号电源状态改变的事件
- `remote-filesystems (7)` - 信号远程文件系统已挂载的事件
- `runlevel (7)` - 信号运行级别的事件
- `started (7)` - 信号作业已启动的事件
- `starting (7)` - 信号作业正在启动的事件
- `startup (7)` - 信号启动的事件
- `stopped (7)` - 信号作业已停止的事件
- `stopping (7)` - 信号作业正在停止的事件
- `virtual-filesystems (7)` - 信号虚拟文件系统已

## 带参数的事件 (SPECIFYING EVENTS WITH ARGUMENTS)

`telinit`（444 页）和 `shutdown`（450 页）发射 `runlevel`。该事件将环境变量 `RUNLEVEL` 设置为新的运行级别，并将 `PREVLEVEL` 设置为之前的运行级别。

要在更改运行级别时指定参数，事件定义包含了参数。你可以使用以下语法匹配这些事件：

```bash
start on event [arg]
```

## /etc/init 中的作业定义文件 (JOB DEFINITION FILES IN /etc/init)

随着 Ubuntu 继续从 SysV 转换为 Upstart，更多的作业将在 `/etc/init` 中定义。本节描述了 upstart 放在此目录的一些作业。

`runlevel` 事件（440 页）信号运行级别的更改。`/etc/init/rc.conf` 作业定义了 `rc` 任务。该任务监控 `runlevel` 事件。文件末尾的 `task` 关键字将此作业指定任务而非服务。由于它是任务，它会阻塞发射 `runlevel` 事件的任务，直到 `rc` 任务完成。

`rc.conf` 中的 `exec` 调用 `/etc/init.d/rc` 脚本（而不是 `rc` 任务）并传递参数 `RUNLEVEL`。

```bash
$ cat /etc/init/rc
# rc - System V运行级别兼容
# 此任务在更改运行级别时运行旧的 System V 风格 rc 脚本。
```

description "System V 运行级别兼容"
author "Scott James Remnant <scott@netsplit.com>"

```bash
start on runlevel [0123456]
stop on runlevel [!RUNLEVEL]
```

```bash
export RUNLEVEL
export PREVLEVEL
```

```
console output
env INIT_VERBOSE
```

```bash
task
exec /etc/init.d/rc $RUNLEVEL
```

### tty 服务

遵循在 tty1 上启动并监控 getty 进程的服务1（见第 448 页）的作业定义文件：

```bash
$ cat /etc/init/tty.conf
# tty1 - getty
#
# 此服务从系统启动到再次关闭期间，
# 在 tty1 上维护一个 getty。
start on stopped rc RUNLEVEL=[2345]
stop on runlevel [12345]
respawn
exec /sbin/getty -8 38400 tty
```

`start on` 语句块中的事件名为 `stopped`（参见 `stopped` 页面）。当 `rc` 任务在 `RUNLEVEL` 等于 2、3、4 或 5 的情况下停止时，这会启动 tty1 服务。由于系统在完成每个运行级别时，`rc` 任务都会停止，因此当系统进入这些运行级别之一时，tty1 就会启动。

`stop on` 语句块中的事件名为 `runlevel`。当发射运行级别带有除 2、3、4 或 5 以外的参数时，该语句会停止 tty1 服务——即当系统进入恢复模式、关机或重启时。

`restart` 关键字告诉 `init` 如果 tty 服务终止，则重启它。这会在 tty1 上以 38400 波特率运行一个无校验位（-8）的 `getty` 进程。在示例中，`initctl` 工具报告了 tty1 服务已启动并作为进程 1061 运行；`ps` 对该进程进行了报告：

```bash
$ status tty
tty start/running, process 1061
$ ps -ef | grep 1061
root 1061 1 0 12:26 tty 00:00:00 /sbin/getty -8 38400 tty1
```

`control-all` own第 451 页关于 `control-all-delete` 任务的讨论，你可以使用它来关闭系统。

在 SysVinit 下，`/etc/initab` 中的默认项告诉 `init` 在系统启动时将系统带到哪个运行级别（见第 443 页）。Ubuntu 不包含 `inittab` 文件；相反，默认情况下，Upstart init 进程（使用 `rc-sysinit` 任务）将系统启动到多用户模式（运行级别 2）。如果你想让系统启动到不同的运行级别，请修改 `rc-sysinit.conf` 文件中的以下行：

```bash
$ cat /etc/init/rc-sysinit.conf
env DEFAULT_RUNLEVEL=2
```

# 不要将系统启动到运行级别 0 或 6

注意 永远不要将系统启动到运行级别 0 或 6，否则它无法正常启动。要启动到多用户模式（运行级别 2），将 `DEFAULT_RUNLEVEL` 设置为 2。要启动到恢复模式，将 `DEFAULT_RUNLEVEL` 设置为 S。

# 第 11 章 系统管理：核心概念

将 `DEFAULT_RUNLEVEL` 的值从 2 改为 S 会导致系统启动到恢复模式（运行级别 S；见第 444 页的注意）。当系统进入恢复模式时，如果系统上的根账户未锁定（见第 431 页），`init` 会在显示根提示符之前请求根密码。否则，它将在不请求密码的情况下显示根提示符。

## SYSVinit(rc) 脚本：启动和停止系统服务

`rc` 脚本 `init`（初始化）脚本，也称为 `rc`（运行命令）脚本，是位于 `/etc/init.d` 目录下的 shell 脚本。它们通过 `/etc/rc.d` 目录中的符号链接进行访问，其中 `n` 是系统正在进入的运行级别。

# /etc/rc.d 和 /etc/init.d 目录中的大部分文件将会消失

正如第 434 页所示。Ubuntu 使用 `Startup` 模拟级别，以帮助迁移并提供与其他发行版的兼容性。本节解释了 `init` 脚本如何工作以通过（模拟的）级别来控制系统服务。在本节描述的 `/etc/rc.d` 和 `/etc/init.d` 目录中的许多脚本建议你使用脚本相应的 `initctl` 命令，因为这些链接已被 `/etc/init` 中的作业控制器所替换（见第 434 页）。

`/etc/rc.d` 目录包含以 K 开头的脚本（`K19cups`、`K20dhcp`、`K74bleutoth` 等）和以 S 开头的脚本（`S15bind`、`S18nis`、`S20cima` 等）。当进入一个新的运行级别时，每个 K（kill）脚本都会带 `stop` 参数执行，然后每个 S（start）脚本都会带 `start` 参数执行。每个 K 文件都按数字顺序排列。S 文件也类似。这种安排允许设置这些文件的人在系统进入给定运行级别时控制哪些服务被停止和启动，以及按什么顺序执行。使用带有 `start` 和 `stop` 参数的脚本增加了灵活性，因为它允许根据调用的参数来同时启动和杀死进程。

如需自定义系统初始化，你可以向 `/etc/init.d` 目录添加脚本，并放置指向这些文件的链接（实践中，最好使用 `sysv-rc-conf` [已讨论] 来创建链接）。

此示例显示了 `cups` init 脚本的多个级别。这些链接由 `cups` 脚本调用，以便在不同的运行级别下启动或停止 `cups` 守护进程：

```bash
ls -l /etc/rc.d*/cups*
lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S50cups -> /etc/init.d/cups
lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S40cups -> /etc/init.d/cups
lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S30cups -> /etc/init.d/cups
lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S20cups -> /etc/init.d/cups
lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S10cups -> /etc/init.d/cups
lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/K80cups -> /etc/init.d/cups
```

## UPSTART 基于事件的守护进程

此示例显示了 `cups` init 脚本的多个级别。这些链接由 `cups` 脚本调用，以便在不同的运行级别下启动或停止 `cups` 守护进程：

```bash
ls -l /etc/rc.d*/cups*
lr-xr-x 1 root 14 2010-02-26 10:11 /etc/rc.d/S50cups -> /etc/init.d/cups
```
