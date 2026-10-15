
`init` 启动（并成为父进程或祖进程）组成你的 Linux 系统的所有进程。首先，它运行 `/etc/rc.d/rc.sysinit`，该脚本设置你的路径，如有必要则设置网络，启动交换分区，检查文件系统，等等。基本上，`rc.sysinit` 负责处理系统初始化时需要完成的所有事情。例如，在网络化的系统中，`rc.sysinit` 使用 `/etc/sysconfig/network` 和 `/etc/sysconfig/clock` 文件中的信息来初始化网络进程和时钟。如果你有需要初始化的串行端口进程，它可能还会运行 `rc.serial`。

`init` 查看并执行 `/etc/inittab` 文件。`/etc/inittab` 文件描述了系统在每个运行级别（runlevel）中应如何设置，并设置默认的运行级别。该文件规定每当运行级别启动时，应运行 `/etc/rc.d/rc` 和 `/sbin/update`。

`/sbin/update` 文件将脏缓冲区刷新回磁盘。

每当运行级别发生变化时，`/etc/rc.d/rc` 都会启动和停止服务。首先，`rc` 为系统设置源函数库（通常是 `/etc/rc.d/init.d/functions`），该库规定了如何启动/终止程序以及如何查找程序的 PID。然后 `rc` 文件会确定当前和前一个运行级别，并告知 `linucconf` 适当的运行级别。

`rc` 文件启动系统运行所需的所有后台进程，并查找该运行级别的 `rc` 目录（`/etc/rc.d/rc<x>.d`，其中 `<x>` 编号为 0-6）。`rc` 终止 `/rc.d/` 中的所有终止脚本（其文件名以 `K` 开头）。然后在适当的运行级别目录中初始化所有启动脚本（其文件名以 `S` 开头）（以便所有服务和应用都能正确启动）。

例如，对于运行级别 5，`rc` 查看 `/etc/rc.d/rc5.d` 目录，发现需要终止 `ruserd`, `rwalld`, `rwhod`, `mcserv`, `mars-nwe`, `apmd` 和 `pcmcia`。在一片混乱之后，`rc` 查看同一目录，发现 `kmod`, `netwroek`, `nfsfs`, `rndr.com`, `syslog`, `afd`, `crond`, `portmap`, `snmpd`, `inet`, `xntpd`, `nfs`, `rpmsave`, `dhcdp`, `ypbind`, `autofs`, `keytab`, `sendmail`, `gpm`, `sound` 和 `smb/rpmsave` 的启动脚本。于是生命重新开始。

`/etc/inittab` 文件为每个虚拟控制台（登录提示符）分叉一个 `getty` 进程，针对每个运行级别（运行级别 2-5 获得全部六个；运行级别 1，即单用户模式，仅获得一个控制台；运行级别 0 和 6 不获得虚拟控制台）。`/etc/inittab` 还规定 `gdm`（X 登录管理器）应在运行级别 5 中启动。

此外，`/etc/inittab` 描述了系统应如何处理将 `[Ctrl]-[Alt]-[Delete]` 转换为类似 `/sbin/shutdown -t3 -r now` 的命令。最后，`/etc/inittab` 规定系统在断电情况下应做什么。

至此，你应该正看着一个登录提示符。这一切，仅仅花费了几秒钟。

接下来，我们将讨论 `/etc/sysconfig` 中文件的相关信息。

## 2.13.2 Sysconfig 信息

以下信息概述了 `/etc/sysconfig` 中的各个文件、其功能及其内容。

### /etc/sysconfig 中的文件

以下文件通常存在于 `/etc/sysconfig` 中：

- `/etc/sysconfig/clock`
- `/etc/sysconfig/hwconf`（编辑时应当忽略此文件）
- `/etc/sysconfig/mouse`
- `/etc/sysconfig/sendmail`
- `/etc/sysconfig/apmd`
- `/etc/sysconfig/init`
- `/etc/sysconfig/keyboard`
- `/etc/sysconfig/network`
- `/etc/sysconfig/pcmcia`
- `/etc/sysconfig/soundcard`（由 `sndconfig` 写入）

让我们逐一看看它们。

### /etc/sysconfig/clock

`/etc/sysconfig/clock` 文件控制从系统时钟读取的值的解释。早期版本的 Red Hat Linux 使用以下值（现已弃用）：

- `CLOCKMODE=mode`，其中 `mode` 为以下之一：
  - `GMT` -- 表示时钟设置为 UTC。
  - `ARC` -- 仅在 Alpha 上表示 ARC 控制台的 42 年时间偏移量生效。

目前，正确的值是：

- `UTC=boolean`，其中 `boolean` 为以下之一：
  - `true` -- 表示时钟设置为 UTC。其他任何值表示设置为本地时间。
- `ARC=boolean`，其中 `boolean` 为以下之一：
  - `true` --（仅适用于基于 Alpha 的系统）表示 ARC 控制台的 42 年时间偏移量生效。其他任何值表示假定使用正常的 UNIX 纪元。
- `ZONE="filename"` -- 表示 `/usr/share/zone-info` 下 `/etc/localtime` 是某个 zonefile 的副本，例如：
  - `ZONE="US/Eastern"`

### /etc/sysconfig/hwconf

`/etc/sysconfig/hwconf` 文件列出了 `kudzu` 在你的系统上检测到的所有硬件，以及使用的驱动程序、供应商 ID 和设备 ID 信息。该文件不是用来编辑的。如果你编辑它，设备可能会突然出现为已添加或已移除。

### /etc/sysconfig/mouse

`/etc/sysconfig/mouse` 文件用于指定关于可用鼠标的信息。可以使用以下值：

- `MOUSETYPE=type`，其中 `type` 为以下之一：
  - `microsoft` -- 微软鼠标。
  - `mouseman` -- MouseMan 鼠标。
  - `mousesystems` -- Mouse Systems 鼠标。
  - `ps/2` -- PS/2 鼠标。
  - `msbm` -- 微软总线鼠标。
  - `logibm` -- 罗技总线鼠标。
  - `atibm` -- ATI 总线鼠标。
  - `logitech` -- 罗技鼠标。
  - `mmseris` -- 较旧的 MouseMan 鼠标。
  - `mmhittab` -- mmhittab 鼠标。
- `XEMU3=*emulation*`，其中 `*emulation*` 为以下之一：
  - `yes` -- 应模拟三个鼠标按钮。
  - `no` -- 鼠标已经有三个按钮。

此外，`/dev/mouse` 是一个指向实际鼠标设备的符号链接。

### /etc/sysconfig/sendmail

`/etc/sysconfig/sendmail` 允许将消息发送给一个或多个收件人，通过必要的网络路由消息。该文件设置 `sendmail` 程序运行的默认值。其默认值作为后台守护程序运行，并且每小时检查一次其队列，以防有积压。

可以使用以下值：

- `DAEMON=*answer*`，其中 `*answer*` 为以下之一：
  - `yes` -- 应配置 Sendmail。`yes` 意味着 `-bd`。
  - `no` -- 不应配置 Sendmail。
- `QUEUE=1h`，该值作为 `-q$QUEUE` 提供给 `sendmail`。如果 `/etc/sysconfig/sendmail` 存在且 `QUEUE` 为空或未定义，则不会向 `sendmail` 提供 `-q` 选项。

### /etc/sysconfig/apmd

`/etc/sysconfig/apmd` 由 `apmd` 使用，作为配置在挂起或恢复时启动/停止/更改哪些服务的文件。根据硬件是否支持高级电源管理（`apm`），或者是否选择不使用它，该文件用于设置开机时是否启用或禁用 `apmd`。

### /etc/sysconfig/init

`/etc/sysconfig/init` 文件控制系统在启动时的外观。

可以使用以下值：

- `BOOTUP=<某种启动模式>`，其中 `<某种启动模式>` 为以下之一：
  - `BOOTUP=color` 表示新的（自 Red Hat Linux 6.0 起）启动显示。
  - `BOOTUP=verbose` 表示旧式显示。
  - 其他任何值均表示新显示，但不带 ANSI 格式化。
- `LOGLEVEL=<数字>`，其中 `<数字>` 设置内核的初始控制台日志级别。默认为 7：8 表示所有级别（包括调试）；1 表示除了内核恐慌外不记录任何日志。`syslogd` 启动后将覆盖此设置。
- `RES_COL=<数字>`，其中 `<数字>` 是屏幕列号，用于开始状态标签。默认为 60。
- `MOVE_TO_COL=<命令>`，其中 `<命令>` 将光标移动到 `$RES_COL`。默认为 `echo -e` 输出的 ANSI 序列。
