
```
# su root

Password: xxx

Su: Password for user 'root' has expired

New Password: YYY

Re-enter new Password: YYY

su: password successfully changed for root

#
```

## 23.2.5 系统服务管理、启动和关机程序

本节详细介绍了启动和优雅关闭 PC-BSD 和 Solaris 的一般程序。它简要概述了这些系统在成功关机时所经历的步骤。然后概述了系统管理员可用的一些重要系统服务管理实用程序，其中最突出的是 Solaris 的 SMF。此外，我们还给出了用于操作和更改这些系统服务的命令示例，通过启用和运行新服务。

### 23.2.5.1 启动过程

基本上，UNIX 系统按以下顺序启动：

- 主系统板上的固件找到可启动介质。
- 启动加载程序从启动介质将单体内核加载到 RAM 中并启动它。
- 内核使用启动加载程序传递的命令找到主文件系统，此时它可以找到并运行初始化程序，该程序在 PC-BSD 和 Solaris 中有所不同。
- 初始化程序运行其他程序以找到文件系统并启动网络和本地服务进程。

启动是指将操作系统从完全关电状态带到稳定、完全正常的运行状态。这里值得注意的是 UNIX 系统与 Linux 中的 `systemd` 以及 OS X 中的 `launchd` 的不同之处。

对于 PC-BSD 和 Solaris 系列 UNIX 系统，启动过程和优雅关机序列本质上是相同的，只是处理系统服务初始化程序的程序存在细微差异。

### 23.2.5.2 优雅关机

对于 PC-BSD 和 Solaris 系统，优雅关机程序通常如下进行。

1. 关闭系统和用户进程
2. 将系统内存刷新到磁盘
3. 卸载文件系统
4. 关闭电源

这些程序可能在 PC-BSD 中被归纳为三个不同的系统调用、系统服务阶段。优雅关机或重启程序可以从活动窗口系统图形化操作，或从命令行或控制台窗口使用 `halt` 或 `shutdown` 命令及其选项进行。PC-BSD 上的示例如下。

```
$ shutdown -h now
```

其中 `-h` 表示停止处理器，`now` 表示立即执行。

在 Solaris 上，使用 `shutdown` 的示例如下：

```
# shutdown -i0 -g180 "System down in 2 minutes"
```

## 表 23.1 运行级别信号模拟

| 运行级别 | 信号 | 操作 |
|---|---|---|
| 0 | `SIGUSR2` | 停止并关闭电源 |
| 1 | `SIGTERM` | 进入单用户模式 |
| 6 | `SIGINT` | 重启机器 |
| c | `SIGSTP` | 阻止进一步登录 |
| q | `SIGHUP` | 重新扫描 `ttyS(5)` 文件 |

服务通过在 `/etc/rc.conf` 中为服务添加条目来启用。系统默认值位于 `/etc/defaults/rc.conf` 中，这些默认设置会被 `/etc/rc.conf` 中的设置覆盖。有关可用条目的更多信息，请参阅 `rc.conf`。在安装额外应用程序时，请查看应用程序的安装信息，以确定如何启用相关服务。

以下是在示例 `/etc/rc.conf` 中的条目，启用了 `sshd`、启用了 Apache 2.4，并指定 Apache 应使用 SSL 启动。

```
# enable SSHD

sshd_enable="YES"

# enable Apache with SSL

apache24_enable="YES"

apache24_flags="-DSSL"
```

一旦在 `/etc/rc.conf` 中启用了服务，就可以在不重启系统的情况下启动它：

```
# service sshd start
# service apache24 start
```

如果服务未被启用，可以使用 `onestart` 从命令行启动它：

```
# service sshd onestart
```

### 23.2.5.3.2 Solaris 系统启动、SMF 和运行级别

当 Solaris 启动并到达 `init` 阶段时，Solaris 上的 `init` 启动 `svc.startd` 守护进程，即 SMF（系统管理框架）。SMF 是主进程启动器和重启器。SMF 不仅在启动时启动服务，还提供管理服务的机制。

Solaris `init` 是默认的第一个用户进程，即 PID 1。在启动期间传递给内核的选项可能会导致使用替代的第一个用户进程。`init` 进程启动 SMF 的核心组件和 `svc.configd`。如果它们失败，`init` 会重启这些组件。为保持向后兼容性，`init` 还会启动并重启类似于 PC-BSD `init` 的通用进程。

在任何给定时间，系统处于八个可能的运行级别之一，与之前为 PC-BSD 定义的类似。`init` 为这些运行级别中的每一个启动的进程可以在 `/etc/inittab` 中定义。`init` 进程可以处于 0–6 以及 `S` 或 `s` 中的一个运行级别。运行级别在特权用户运行 `/usr/sbin/init` 时发生变化。

由 `init` 调用的运行级别 `S` 或 `s` 将系统切换到单用户状态。在此状态下，系统控制台设备（`/dev/console`）被打开以进行读写。运行级别 0、5 和 6 是用于关闭系统的保留状态。运行级别 2、3 和 4 可用作多用户操作状态。

Solaris SMF 管理应用程序和系统服务。它除了传统的 UNIX 启动脚本、`init` 运行级别和配置文件之外工作。SMF 的工作方式使得依赖服务在必要时可以自动重启。管理每个服务所需的信息存储在服务配置存储库中，该存储库提供了一种简化管理每个服务的方法。SMF 还允许您启动或停止在启动时未默认启动的服务。第 23.2.5.5 节中为 Solaris 显示的示例说明了这一点。

SMF 拥有一组可以由管理员，通常是 `root` 用户，在服务上调用的操作。这些操作可以通过命令行手动操作，例如使用 `svcadm` 命令，包括 `enable`、`disable`、`refresh` 和 `restart`。每个服务都由一个服务重启器管理，该重启器执行管理操作。一般来说，重启器通过执行服务的 `<|message|>` 方法来执行操作。每个服务的方法在服务配置存储库中定义。这些方法允许重启器将服务从一个状态移动到另一个状态。

以下是 SMF 用于管理服务的命令列表。

- `inetadm`: 控制 `inetd` 守护进程服务
- `svcadm`: 执行常见的服务管理任务，如启用、禁用或重启服务实例
- `svccfg`: 显示并更改服务配置存储库
- `svcprop`: 通过从服务配置存储库检索属性值提供 shell 脚本代码
- `svcs`: 提供服务配置存储库中所有实例的服务状态的详细详细信息
- `svcbundle`: 生成 SMF 清单

请参阅以下示例以更完整地描述使用其中一些命令。您也可以在系统上查看这些命令的 `man` 手册页。

### 23.2.5.4 系统服务管理示例

在本节中，我们通过举例说明如何为 `telnet`、`ftp`、`rlogin` 和 `rsh` 守护进程启用服务器端主机服务，来说明 PC-BSD 和 Solaris 服务管理的使用。

在第 25 章中，我们将展示如何在 PC-BSD Jail、Solaris Zone 或 VirtualBox VM 中安全地实现这些服务。

为准备本节的 PC-BSD 组件，你应参考第 20 章第 10 节“UNIX 超级服务器 `inetd`”，以获取有关 `inetd` 服务操作及其配置的更多信息。

正如将要指出的那样，在执行这些示例时应谨慎，特别是如果你没有使用第 25 章中所示的虚拟化方法之一，并且处于连接到互联网的不安全网络上。你还必须在计算机上拥有 `root` 权限才能执行以下示例。

## EXERCISE 23.3

从互联网上的远程站点使用 `ftp`、`telnet`、`rlogin` 或 `rsh` 登录到你的家庭服务器有什么危险？

#### 23.2.5.4.1 在 PC-BSD 和 Solaris 上启用 `telnet` 和 `ftp` 服务器的示例

对于 PC-BSD 主机或服务器：

- CAUTION: 此步骤会关闭主机计算机对 23 和 21 端口入站流量的防火墙。
- 在桌面上使用 PC-BSD 控制面板并进入防火墙管理器。
- 在防火墙管理器中，为 `telnet` 添加新的 TCP 端口 23，为 `ftp` 添加端口 21，以便入站流量可以进入。
- 此时，重新启动防火墙管理器并退出它。
- 检查 `telnet` 是否处于活动状态：
- 如果你没有得到此输出，请继续执行以下操作：

```
$ netstat -anf inet|grep LIST|grep 23

tcp4      0      0 *.23

*.*       LISTEN
```

作为超级用户：

```
$ vi /etc/inetd.conf
```

- 取消注释，或删除以下行的第一个字符 `#`：

```
ftp     stream  tcp nowait root    /usr/libexec/ftpd    ftpd-1
```
