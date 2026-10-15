
由`/etc/init.conf`文件定义的`rc`任务运行`/etc/init.d rc`脚本。该脚本反过来通过`/etc/rc.d`目录中的符号链接运行`/etc/init.d`中的脚本，模拟了这些链接在`SysInit`环境下的功能。`rc`任务在系统进入运行级别时运行服务；当系统离开运行级别时不采取任何操作。关于`rc`任务的讨论请参阅第 438 页，关于`init`脚本的信息请参阅第 440 页。`Upstart`实现了运行级别（第 444 页）和`telnet`工具以提供与`SysInit`系统的兼容性。

`init`（init 控制）工具与`Upstart init`守护进程通信。普通用户可以使用`init list`和`start`命令查询`Upstart init`守护进程。具有`root`权限的系统管理员可以查询此守护进程并启动和停止作业。例如，`init list`列出了作业以及：

```bash
$ initlist
alsa-mixer-save stop/waiting
avahi-daemon start/running, process 509
mountall-net stop/waiting
rc stop/waiting
rsyslog start/running, process 653
tty4 start/running, process 695
udev start/running, process 252
```

查阅`initctl`手页和本节中的示例以获取更多信息。你可以输入`initctl help`命令（在连字符之前）来显示`initctl`命令列表。或者，你可以输入以下命令显示关于`list`命令的更多信息：

```bash
$ initctl list --help
用法: initctl list [OPTION]...
列出已知作业。

选项：

--system            使用 D-Bus 系统连接
--destName          目标已知名称连接
-q, --quiet        仅输出错误
-V, --verbose      增加输出以包含信息消息
--help             显示此帮助并退出
--version           输出版本信息并退出
```

作业及其当前状态将被输出。

将`list`替换为你想要获取更多信息的`initctl`命令。`start`、`stop`、`reload`和`status`工具是运行对应命令的`initctl`链接。

## 作业

`/etc/init`目录中的每个文件都定义了一个作业，并且通常包含一个事件和一个命令。当事件触发时，`init`执行该命令。本节描述了由管理员定义的作业以及通过`upstart`软件包安装的作业。

### 管理员定义的作业

示例：以下管理员定义的作业，它使用`exec`关键字执行`shell`命令。你也可以使用该关键字执行存储在文件中的`shell`脚本或可执行文件。在第一个语句（`start on runlevel 2`）中，`start on`是关键字（你可以用`stop on`替换它），`runlevel`是事件（第 433 页），而`2`是运行级别的参数。

```bash
$ cat /etc/init.conf

start on runlevel 2

    exec echo "Entering multiuser mode on $(date)" > /tmp/init.out
```

此文件定义了一个任务：当系统进入多用户模式（运行级别 2）时，运行`echo`命令。该命令将包含时间和期的消息写入`/tmp/init.out`。`shell`使用命令替换（第 362 页）来执行`date`工具。作业运行完成后，该任务停止并进入等待状态。

### 436 第 11 章系统管理：核心概念

在下一个示例中，`cat`工具显示了`/tmp/init.out`文件的内容，`init list`命令列出了该任务的状态报告：

```bash
$ cat /tmp/init.out

Enter multiuser mode on Wed Mar 10 11:58:14 PST 2010
```

```bash
$ initctl status | grep rc

rc stop/waiting

$ status rc

rc stop/waiting
```

如果`exec`命令行包含`shell`特殊字符（第 160 页），它会执行`/bin/sh`（`dash`的链接，第 292 页）并将命令行传递给`shell`。否则，`exec`直接执行命令行。要运行多个`shell`命令，请使用`exec`运行文件中的脚本，或使用`script`（后文讨论）。

`Upstart init`守护进程只能监控使用`exec`执行的作业（服务）；它无法监控使用`script`执行的作业。另一种方法是服务需要使用`exec`，而任务可以使用任种方法运行程序。`Upstart init`守护进程将能够监控这些作业。

你也可以定义一个事件，并设置一个由该事件触发的作业。

### 事件

`upstart`软件包了许多事件。以下命令列出了事件及其简要描述。有关每个事件的信息请参见相应的`man`页。

- `all-swaps (7)` - 信号交换分区已激活的事件
- `control-alt-delete (7)` - 信号控制台按下 Alt-Delete 的事件
- `filesystem (7)` - 信号文件系统已挂载的事件
- `keyboard-request (7)` - 信号控制台按下 Alt-Arrow 的事件
- `local-filesystems (7)` - 信号本地文件系统已挂载的事件
- `mounted (7)` - 信号文件系统已挂载的事件
- `mounting (7)` - 信号文件系统正在挂载的事件
- `power-status-changed (7)` - 信号电源状态变化的事件
- `remote-filesystems (7)` - 信号远程文件系统已挂载的事件
- `runlevel (7)` - 信号作业正在运行的事件
- `started (7)` - 信号作业正在启动的事件
- `startup (7)` - 信号系统启动的事件
- `stopped (7)` - 信号作业已停止的事件
- `stopping (7)` - 信号作业正在停止的事件
- `virtual-filesystems (7)` - 信号虚拟文件系统已挂载的事件

### 可选：带参数指定事件

`telinit`（第 444 页）和`shutdown`（第 450 页）工具发出包含参数的运行级别事件。例如，`shutdown`发出运行级别 0，`telinit 2`发出运行级别 2。你可以在作业定义中使用以下语法匹配这些事件：

```
start|stop event [arg [arg...]]
```

其中`event`是如`runlevel`的事件，`arg`是一个或多个参数。要在系统从运行级别 1 进入运行级别 2 时停止作业，请指定`stop on runlevel 2 1`。你也可以指定`2`、`3`、`5`或`[!2]`来匹配除 2 以外的所有值。

## /etc/init 目录中的作业定义行

随着`Ubuntu`继续从`SysVinit`向`Upstart init`过渡，将会有更多的作业定义在`/etc/init`目录中。本节描述了`upstart`软件包放在此目录中的某些作业。

运行事件（`runevent`，`runlevel(7) man page`）标志着运行级别（`runlevel`）的变化，并由`telinit`（第 444 页）和`shutdown`（第 450 页）发出。此事件将环境变量`RUNLEVEL`设置为新运行级别的值，并将`PREVLEVEL`设置为上一个运行级别的值。

`/etc/init/rc.conf`作业定义文件定义了`rc`任务。该任务监控运行级别事件。文件末尾的`task`关键字将此作业指定为任务（`task`）而不是服务（`service`）。由于它是任务，它会阻塞发出运行级别事件的调用，直到`rc`任务完成。

`rc.conf`中的`exec`句段调用了带有`RUNLEVEL`参数的`/etc/init.d` `rc`脚本（而不是`rc`任务）。`rc`脚本调用`/etc/rc.d`目录中的链接，其中`n`等于`RUNLEVEL`（第 440 页）。因此，带有`RUNLEVEL`为 2 调用的`rc`任务会运行`/etc/rc.d`目录中链接指向的`init`脚本。

当系统进入从 0 到 6 的运行级别时（在运行级别`[0123456]`上启动），`rc`任务会运行`rc`脚本。通常情况下，该任务在完成`rc`脚本后终止。

`stop`句段（在运行级别`[!RUNLEVEL]`上）处理了当`rc`任务正在运行`rc`脚本时尝试启动第二个运行级别事件。在这种情况下，`RUNLEVEL`的值不等于调用`rc`任务时的`RUNLEVEL`值，`rc`任务将停止。

```bash
$ cat /etc/init/rc.conf

# rc - System V运行级别兼容性

#
# 此任务在切换运行级别时运行旧的 System V 风格 rc 脚本。

description     "System V runlevel compatibility"
author          "Scott James Remnant <scott@netsplit.com>"

start on runlevel [0123456]
stop on runlevel [!RUNLEVEL]

export RUNLEVEL
export PREVLEVEL

console output
env INIT_VERBOSE

exec /etc/init.d/rc $RUNLEVEL
```

`services`下面是在`tty1`上启动并监控`getty`进程（第 448 页）的服务的作业定义文件：

```bash
$ cat /etc/init/tty1.conf

# tty1 - getty

#
# 此服务从系统启动到再次关机，在 tty1 上
# 维护一个 getty 进程。

start on stopped rc RUNLEVEL=[2345]
stop on runlevel!=[2345]

respawn
exec /sbin/getty -8 38400 tty1
```

`start on`句段中的事件名为`stopped`（参见`stopped` man 页面）。当`rc`任务以`RUNLEVEL`等于 2、3、4 或 5 启动时，会启动`tty1`服务。由于系统在完成每个运行级别时`rc`任务都会停止，因此当系统进入这些任何一个运行级别时，`tty1`服务就会启动。

`stop on`句段中的事件名为`runlevel`。当发出带有 2、3、4 或 5 以外参数的运行级别时，会停止`tty1`服务——即当系统进入恢复模式、关机或重启时。

`respawn`关键字告诉`init`如果`tty1`服务发生退出，则重启它。`exec`句段在`tty1`上以无校验位（`-8`）和 38,400 波特率运行`getty`进程。在下一个示例中，`init`工具报告了`ps`服务已启动并作为进程 1061 运行；`ps`报告该进程的情况：

```bash
$ status tty1

tty1 start/running, process 1061

$ ps -ef | grep 1061

root 1061 1 0 12:26 00:00:00 /sbin/getty -8 38400 tty1
```

有关`control-delete`任务的讨论，请参阅第 451 页，你可以使用它来关闭系统。在`rc-sysinit`任务下，`/etc/initab`文件中的默认条目告诉启动时将系统带到何种运行级别（第 443 页）。`Ubuntu`不包含`initab`文件；相反，默认情况下，`Upstart init`守护进程（`rc-sysinit`任务）启动系统到多用户模式（运行级别 2）。如果你想让系统启动到不同的运行级别，请修改`rc-sysinit.conf`中的以下行：

```bash
$ cat /etc/init/rc-sysinit.conf

...
env DEFAULT_RUNLEVEL=2

# 不要将系统启动到运行级别 0 或 6。永远不要将系统设置到运行级别 0 或 6，否则它无法正常启动。要启动到多用户模式（运行级别 2），将 DEFAULT_RUNLEVEL 设置为 2。要启动到恢复模式，将 DEFAULT_RUNLEVEL 设置为 S。
```

### 第 11 章 系统管理：概念

将`DEFAULT_RUNLEVEL`的值从 2 改为`S`会导致系统启动到恢复模式（运行级别`S`；见第 444 页的警告）。当系统进入恢复模式时，

（注：原文此处似乎存在部分文本的重复或乱码，翻译已根据语意进行逻辑对齐）

`rc.conf`中的`exec`句段调用了带有`RUNLEVEL`参数的`/etc/init.d` `rc`脚本（而不是`rc`任务）。`rc`脚本调用`/etc/rc.d`目录中的链接，其中`n`等于`RUNLEVEL`（第 440 页）。因此，带有`RUNLEVEL`为 2 调用的`rc`任务会运行`/etc/rc.d`目录中链接指向的`init`脚本。

当系统进入从 0 到 6 的运行级别时（在运行级别`[0123456]`上启动），`rc`任务会运行`rc`脚本。通常情况下，该任务在完成`rc`脚本后终止。

`stop`句段（在运行级别`[!RUNLEVEL]`上）处理了当`rc`任务正在运行`rc`脚本时尝试启动第二个运行级别事件。在这种情况下，`RUNLEVEL`的值不等于调用`rc`任务时的`RUNLEVEL`值，`rc`任务将停止。

（注：由于原文后部分存在大量重复的段落和无意义字符，译文已根据核心技术含义进行了清理处理，确保不重复输出原文。）

## 442 第 11 章 系统管理：核心概念

仅如此——它不会改变任何服务的当前状态。执行以下命令查看服务列表：

```bash
$ sudo sysv-rc-conf --list

acpi-support 1:off 2:on 3:on 4:on 5:on

acpid

alisa-mixer-s

anacron

apparmor S:on

apport

atd

avahi-daemon

binfmt-support 2:on 3:on 4:on 5:on

bluetooth 0:off 1:off 2:on 3:on 4:on 5:on 6:off

...
```

所有运行守护进程的服务都列在其中，一一一对应，随后跟的是它们在每个运行级别（`runlevel`）下的配置状态。如果缺少某个运行级别，意味着在`/etc/rc.d`目录下没有该服务的条目。当所有运行级别都缺失时，意味着该服务由`Upstart`控制。你可以通过向之前的命令添加其名称来检查特定守护进程的配置：

```bash
$ sudo sysv-rc-conf --list cups

cups 1:off 2:on 3:on 4:on 5:on
```

### 任务/初始化脚本名称可能与其控制的守护进程名称不同

> 下面的示例显示了`ssh`进程。你可以通过列出`/etc/init`和`/etc/init.d`目录的内容，并搜索与你想要操作的进程名称或功能相似的文件，找到控制该守护进程的任务名称。例如，`/etc/init.d/cups`脚本控制打印守护进程。

通常，脚本的前几行或任务中`exec`和`desc`段落的注释会标识出它所控制的守护进程。下面的任务描述文件显示了这些行：

```bash
$ cat /etc/init/ssh.conf

# ssh OpenSSH Shell server
# The OpenSSH server为系统提供安全的 shell 访问。

...
description "OpenSSH server"
exec /usr/sbin/sshd
```

在下一个示例中，`sysv-rc-conf`（`sysv-rc-conf`软件包）配置了`/etc/rc.d`目录，使得`cupsd`守护进程在运行级别 2、3、4 和 5 中处于状态，并确认了此更改。要进行此类更改，你必须拥有`root`权限：

```bash
$ sudo sysv-rc-conf --level 2345 cups off

$ sudo sysv-rc-conf --list cups

cups 1:off 2:off 3:off 4:off 5:off
```

## 系统操作 443

为了方便起见，你可以省略`--level 2345`参数。当你指定初始化脚本以及`on`或`off`时，`sysv-rc-conf`默认运行级别 2、3、4 和 5。以下命令与之前的第一个命令等效：

```bash
$ sudo sysv-rc-conf cups off
```

`ps`工具确认了尽管`sysv-rc-conf`将`cups`设置为在所有运行级别下都关闭，但它仍在运行。`sysv-rc-conf`工具并没有关闭`cups`。

```bash
$ ps -ef | grep cups

998      1 0 12:47 ?       00:00:00 /usr/bin/cupsd -C /etc/cups/cups.conf
zach    5618 1334    0 18:20 pts/0      00:00:00 
```
