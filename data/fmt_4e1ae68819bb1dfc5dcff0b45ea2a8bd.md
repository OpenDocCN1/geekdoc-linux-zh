
```
root@localhost:~ COMMAND-list
File Edit Terminal Tabs help:
Sep 14 14:23:38 localhost sudo: bob TTY=pts/0 PWD=/home/bob USER=root COMMAND=/sbin/ifconfig
Sep 14 14:24:18 localhost sudo: bob TTY=pts/0 PWD=/home/bob USER=root COMMAND=/sbin/ifconfig eth0 down
Sep 14 14:25:11 localhost sudo: bob TTY=pts/0 PWD=/home/bob USER=root COMMAND=/sbin/ifconfig eth0 up
Sep 14 14:25:00 localhost sudo: bob TTY=pts/0 PWD=/home/bob USER=root COMMAND=/bin/is
Sep 14 14:26:24 localhost sudo: bob TTY=pts/0 PWD=/home/bob USER=root COMMAND=/usr/sbin/useradd susan
Sep 14 14:27:02 localhost sudo: bob TTY=pts/0 PWD=/home/bob USER=root COMMAND=/usr/sbin/vi /hosts
Sep 14 14:42:53 localhost sudo: bob TTY=pts/0 PWD=/home/bob USER=root COMMAND=/bin/vi /hosts
Sep 14 14:43:15 localhost sudo: bob TTY=pts/0 PWD=/home/bob USER=root COMMAND=/bin/cat /var/log/sudo
```

# 操作系统强化 • 第 2 章 55

## 第 2 章 操作系统加固

当系统停止并重启、当用户使用 `su` 命令升级到 root、当文件系统已满以及有人在嗅探系统时，都会发生这种情况。它可以从日志文件中监控任何所需的内容。

要了解 SWATCH 并下载该程序，你需要访问 SWATCH 主页 `http://swatch.sourceforge.net`。图 2.22 所示了 SWATCH 首页。

### 图 2.22 SWATCH 首页

![](img/33fc180c04c8f96c022bce6e62ae12fd_74_0.png)

在本文编写时，SWATCH 3.2.2 版本可下载。

SWATCH 使用两个必填字段：模式（patterns）和动作（actions）。

- **模式 (Patterns)**：SWATCH 配置文件会在日志条目中查找模式。例如，失败的登录尝试会显示“Failed Authentication”错误。

- **动作 (Actions)**：每当发现模式时，SWATCH 会执行相应的操作，例如向管理员发送登录失败尝试的电子邮件。

有两个可选字段用于进一步自定义配置文件：

- **节流 (Throttle)**：节流定义了 SWATCH 在再次列出该条目之前忽略重复日志条目的时间。这节省了管理员查看 300 个相同“Failed Authentication”错误的时间。然而，安全的系统应该限制登录尝试次数。节流项定义为 `HH:MM:SS`，其中 H 代表小时，M 代表分钟，S 代表秒。

- **时间戳 (Timestamp)**：时间戳定义了时间戳的长度和位置。时间戳项定义为 `start:length`。

以下是 SWATCH 配置文件的两个示例。当这些消息通过 `syslog` 工具写入各自的日志文件时，SWATCH 会主动监控这些消息。第一个示例监控日志中的失败登录尝试，并在发生登录失败时向 root 发送电子邮件。

```
### Failed login attempts
watchfor /failed/
echo bold
mail addresses=root,subject=Failed Authentication
```

第二个示例监控你的日志文件，并在用户尝试获取访问权限时向 root 发送电子邮件。

```
### Users used to gain root access
watchfor /su/:
echo bold
mail addresses=root,subject=User used to root
```

SWATCH 过滤日志文件，使管理员只接收他们需要的信息。配置完成后，它可以节省大量的时间和精力，建议那些被日志文件淹没的系统管理员使用。要下载 SWATCH 的 RPM 版本，请访问 `www.rpmfind.net`。

### Scanlogd

`Scanlogd` 是一个开源程序，用于检测并记录系统上的 TCP 端口扫描。例如，它可以检测 `nmap` 扫描。`Nmap` 是黑客用来创建你的网络“地图”的程序。这通常是黑客一旦获得你的网络访问权限后采取的第一步，以确定要黑入哪个系统。`Nmap` 列出了网络上的系统和服务和服务

![](img/33fc180c04c8f96c022bce6e62ae12fd_75_0.png) 当网络正在被映射时，`Scanlogd` 可以向管理员报警，但它无法阻止入侵。

### 安全警报！

> `Scanlogd` 最初设计用于说明攻击，而不是修复攻击。因此，尽管在你的系统上运行它是安全的，但它并不能防止黑客攻击。你必须阅读系统日志以发现你的系统发生了什么，然后确定相应的解决方案。

`Scanlogd` 使用 `scanlog(3)` 机制每次扫描写入一行。它还会记录源地址在短时间内向几个不同端口发送许多数据包的情况。你可以在 `openwall.com/scanlogd` 了解 `scanlog` 并下载该程序。图 2.23 所示了 `scanlogd` 首页。

### 图 2.23 Scanlogd 首页

![](img/33fc180c04c8f96c022bce6e62ae12fd_76_0.png)

`scanlogd` 是 TCP 端口扫描检测工具，最初用于说明 IDS 开发者必须处理的各种攻击。与现有的某些端口扫描检测工具不同，`scanlogd` 的设计初衷是完全解决问题，发布的 `scanlogd` 构建时支持多个数据包捕获接口。在 Linux 的原始套接字接口的基础上，`scanlogd` 现在能够识别 `libp` 和 `libcap`。

不建议使用 `libp`。如果你位于 Linux 以外的系统并想要一次性监控整个网络的流量，你应该使用 `libp` 来处理分片的 IP 数据包。

请阅读 `scanlogd(8)` 手册页和原始 `Phrack` 杂志文章。

由于 `scanlogd` 仅用于检测扫描，因此在你的系统上运行是完全安全的。它必须具有原始 IP 数据包的权限才能运行，并可以捕获进出系统接口跨系统连接的网络的数据包。此外，`scanlogd` 支持 `libnads`、`libcap` 和 Linux 原始套接字接口。

### Syslog-ng

`Syslog-ng` 是一个日志守护进程，是传统 `syslogd` 的替代品。“ng” 是“next generation”的缩写。原始 `syslog` 守护进程处理请求，但很难配置。`Syslog-ng` 更容易配置并提供了额外功能，例如根据内容过滤消息。图 2.24 所示了 `syslog-ng` 首页。

### 图 2.24 Syslog-ng 首页

![](img/33fc180c04c8f96c022bce6e62ae12fd_77_0.png)

`syslog-ng` 可 AIX、 Debian、Red Hat 3、4、5、 Solaris 8、9 和 Linux 10。最新版本为 2.0。你可以从 `www.rpmfind.net` 了解更多信息。该产品提供开源和付费版本。额外的软件包如 `libcap`。

不建议使用 `libp`。如果你位于 Linux 以外的系统并想要一次性监控整个网络的流量，你应该使用 `libp` 来处理分片的 IP 数据包。

请阅读 `scanlogd(8)` 手册页和原始 `Phrack` 杂志文章。

由于 `scanlogd` 仅用于检测扫描，在你的系统上运行是完全安全的。它必须具有原始 IP 数据包的权限才能运行，并可以捕获进出系统接口跨系统连接的网络的数据包。此外，

### 图 2.25 Syslog-ng 平台

![](img/33fc180c04c8f96c022bce6e62ae12fd_78_0.png)

### Security Linux

`Security Linux` 或 `SELinux` 是 NSA 项研究计划。该项目的建议已整合到各种 Linux 发行版中。该项目关注内核子系统中的强制性访问控制 MAC 架构，而不是操作系统内部的安全漏洞。有关 `SELinux` 的更多信息、白皮书、演示和下载可用 `www.nasa.gov/selinux/`。
