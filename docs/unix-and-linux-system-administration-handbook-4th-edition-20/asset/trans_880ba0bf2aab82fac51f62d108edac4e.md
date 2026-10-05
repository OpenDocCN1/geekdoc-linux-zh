
## 第3章 启动与关机

每个变量之前都有 YaST 可读的配置信息，以及对该变量用途的详细描述。例如，在 `windowmanager` 文件中，`DEFAULT_WM` 变量通过 X 设置桌面窗口管理器。

SUSE 还包含一个用于管理启动脚本的 `chconfig` 命令。它与 Red Hat提供的版本完全不同，但仍然是一个有效的工具，应该被优于手动脚本管理。

## Ubuntu 启动脚本和 Ubuntu 进程

从2007年初的 Feisty 开始，Ubuntu 用 Upstart 替了传统的 init。这是一种事件驱动的服务管理系统，某些 Linux 发行版也在使用。相比 init，Upstart 能更优雅地处理系统转换——例如硬件变化。它显著缩短了启动时间。

Upstart 通过响应添加设备或断开网络驱动器等系统事件来启动和停止服务。为了兼容，它还翻译了 init 传统的运行级别（run levels）。然而，启动和关机脚本的处理方式与你使用的有所不同。

Upstart 使用 `/etc/event.d` 中的作业定义文件而不是 `initab` 文件。作业在概念上类似于启动脚本：它执行一系列命令并将控制权交还 Upstart。Ubuntu 系统上的作业集合如下：

```
ubuntu3 ls /etc/event.d
control-all last-good-boot rc0 rc1 rc2 rc3 rc4 rc5 rc6
rc-default rc5 rc-sulogin sulogin tty1 tty2 tty3 tty4 tty5 tty6
```

随着时间的推移，会有更多的启动脚本转换为原生的 Ubuntu 作业。目前，Upstart 使用运行级别模拟脚本来启动系统。例如，`rc2` 脚本执行 `/etc/rc2.d/`，这将运行运行级别 2 的所有启动脚本。

由于需要维护这种兼容性，Ubuntu 管理员应该使用 Ubuntu 的 `update-rc.d` 命令来维护 `rc` 目录内启动脚本的链接。语法如下：

```
update-rc.d service { start | stop } sequence runlevels
```

`update-rc.d` 接受序列号（启动脚本应执行的顺序）和相应的运行级别作为参数。使用 `--` 结束解析。

在运行级别转换中启动的服务在系统退出该级别时应该更早停止。例如，CUPS 在启动期间的序列值为 80，它应该在关机过程早期序列值 20 左右停止。添加适当链接的 `update-rc.d` 命令应该是：

- - YaST 是一个 SUSE 特有的配置工具，维护着 SUSE 的许多方面

## AIX 启动

```
ubuntu$ sudo update-rc.cups start 80 2 3 4 5 . stop 20 S 1 6 .
Adding system startup for /etc/init.d/cups ...
/rc1.d/K20cups -> ../init.d/cups
/rc6.d/K20cups -> ../init.d/cups
/rc5.d/K20cups -> ../init.d/cups
/rc2.d/S80cups -> ../init.d/cups
/rc3.d/S80cups -> ../init.d/cups
/rc4.d/S80cups -> ../init.d/cups
/rc5.d/S80cups -> ../init.d/cups
```

该命令在运行级别 2, 3, 4 和 5 的序列 80 处添加“start”实例，并在运行级别 S、1 和 6 的序列 20 处添加“stop”实例。

默认运行级别由 `/etc/event.d/rc-default` 中的两条 telnet 行控制。
使用文本编辑器编辑 `rc-default` 来更改运行级别。

Upstart 还控制你持有的 tty" 终端上的登录。

## HP-UX 启动脚本

在 HP-UX 下，实际的启动脚本保存在 `/sbin/init.d` 中。运行级别目录也在 `/sbin` 中。与启动脚本相关的配置文件通常位于 `/etc/rc.config.d`。它们的名称与 `/sbin/init.d` 中的启动脚本名称对应。例如，脚本

- - /sbin/init.d/SnmpMaster

从 `/etc/rc.config.d/SnmpMaster` 获取其配置信息

并实际上由 `init` 通过以下链接的作业调用：

- - /rc2.d/S560SnmpMaster
- /rc1.d/K440SnmpMaster

HP-UX 将启动脚本的输出保存在 `/etc/rc.log` 中。如果你的某个启动脚本失败，请检查 `/etc/rc.log` 以查看问题。保存启动脚本输出是最有用且卓越的功能，而且实现也很简单。其他厂商没有发现这一点，令人惊讶。

`/etc/rc.config.d` 中的配置文件可能相当令人混乱，尽管它们有详细的注释。下一页的表 3.6 提供了对一些常用修改文件的解释。

这些文件中的默认值通常是好的。你可能需要的最常见的文件是 `netconf`、`netdaemons` 以及可能的 `nddcconf`。

## AIX 启动

与其他示例系统相比，AIX 启动过程的方法更为粗放。在启动期间，AIX 运行 `/sbin/rc.boot` 脚本，该脚本是用 ksh 写的。

## 表 3.6 常修改的 HP-UX-config 文件

| 文件(s) | 用途 |
| :--- | :--- |
| SNMPMaster | 关闭所有 SNMP 的主开关 |
| acct | 开启进程计数 |
| cde | 存储 CDE（桌面环境）设置 |
| clean | 初始化系统 |
| hnetconf | 配置以太网接口 |
| lp | 开启打印机 |
| mailserv | 启动 mailmail |
| nameserv | 配置名称 |
| nddconf | 设置可调内核参数 |
| netdaemons | 开启网络 |
| nfsconf | 配置 NFS |
| sshd | 开启 SSH |
| vt | 开启视频 |

## 服务管理设施 (SMF)

随着服务管理设施（SMF）的引入，Sun 改进了 Solaris 10 的启动过程。SMF 是一种全面且独特的服务方法。它在服务周围封装了一层新的逻辑，以处理依赖关系和软件故障。

SMF 很大程度上改变了启动过程。传统的 init 及其 rc 脚本理论上已经消失了。

Sun 将服务定义为“一个向应用程序以及本地远程服务提供能力列表的实体”。对于我们的目的，服务大致等同于守护进程：Web 服务器、syslog 日志记录器甚至是 init。同一个 SMF 服务存在多个实例。例如，你可能会运行多个具有不同 IP 地址的服务器。服务也可以被定义为其他服务的集合。这一功能让 SMF 取代了 init 传统规则的角色。

服务的每个实例通过“故障管理资源标识符”（FMRI）进行唯一标识。例如，以下 FMRI 指向 SSH 服务：

```
svc/network/ssh:default
network/ssh:default
```

ssh 服务属于网络类别，此 FMRI 描述了默认实例。SMF 包含多个类别，如应用程序、设备、网络和系统。一个名为里程碑（milestone）的特殊类别封装了运行级别的计数。

使用 `svcs` 命令检查服务的状态。使用 `svcs -a` 查看所有已定义的服务，或省略 `-a` 标志仅查看正在运行的服务。`svcs` 还可以检查单个服务。例如，以下命令显示了 SSH 服务的状态：

```
solaris$ svcs -l svc:/network/ssh:default
fmri
svc/network/ssh:default
SSH server
enabled
true
state
line
next_state
none
state_time
Mon Jul 13 15:56:19 2009
```

