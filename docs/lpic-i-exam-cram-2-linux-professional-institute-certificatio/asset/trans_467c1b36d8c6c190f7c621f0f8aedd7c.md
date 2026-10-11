

## inetd 配置文件

inetd 比 xinetd 历史悠久得多，两者之间的主要区别在于配置文件的结构。

inetd 使用单个配置文件，通常是 `/etc/inetd.conf` 文件。该文件包含以 `#` 开头的注释项以及定义单个服务的条目。以下是 `/etc/inetd.conf` 中几行典型内容（实际内容远不止这些）的示例：

```text
ftp    stream  tcp  nowait  root  /usr/sbin/in.ftpd  in.ftpd
telnet stream  tcp  nowait  root  /usr/sbin/in.telnetd  in.telnetd
```

上面所示的行分解为以下字段和定义：

- **服务名称** — 此名称必须与 `/etc/services` 文件中的有效服务名称条目匹配。
- **套接字类型** — 可以是 `stream`、`dgram`、`raw`、`rdm` 或 `seqpacket` 中的任意一种。
- **协议** — 这是 `/etc/protocols` 文件中定义的协议之一；通常是 `tcp` 或 `udp`。
- **wait** 或 **nowait** 参数 — 对于获取套接字并操作直至超时的单线程服务器，使用 `wait` 参数；对于在不活动时会释放套接字的多线程服务器，使用 `nowait`。
- **用户/组** — 该服务应以哪个用户或组身份运行，这使您能够将有风险的服务限制在非 root 账户中运行。
- **服务器程序** — 提供服务的程序的完整路径和名称。
- **服务器参数** — 服务正常运行可能需要的任何参数。

如果服务需要由 `hosts.deny` 和 `hosts.allow` 或 TCP wrappers 控制，则服务器程序应为 `/usr/sbin/tcpd`，且服务器参数应为 tcpd 将监视的服务的完整路径和名称。这只适用于 inetd，不适用于 xinetd。您可以在第 19 章“安全”中了解有关此内容的更多信息。

> **警示**
> 如果你之前运行的是 **inetd** 并且正在转换为运行 **xinetd**，那么最重要的文件是 `/etc/inetd.conf`，其中包含定义哪些服务应按需提供需求的条目。这些行应作为新的 **xinetd** 配置的基础。Red Hat 提供了一个名为 **inetdconvert** 的工具，可以帮助完成此过程。

### xinetd 配置文件

**xinetd** 守护进程最初使用 `/etc/xinetd.conf` 文件来设置一些守护进程配置参数，这些默认值将被所有由 **xinetd** 管理的服务读取，并指定 include 目录。（这些默认值会被单个服务配置文件中的设置覆盖。）

include 目录通常是 `/etc/xinetd.d`，其中包含每个受管理服务的单个文本文件。服务配置文件包含服务的定义以及为确保正确运行需要设置的特殊设置。

图 18.1 展示了 **xinetd** 服务和文件的组件之间的关系。

![](img/49f4f38f3aec011238fa50f89e643db3_486_0.png)

**图 18.1** **xinetd** 的工作原理。

如你所见，**xinetd** 读取 `/etc/xinetd.conf` 并获取其配置，包括 include 目录的位置；然后它等待客户端请求其服务之一。当客户端请求到达时，xinetd 查看数据包，找到目标端口/服务，并在 `/etc/xinetd.d` 目录中通过名称查找该服务。该目录中包含每个服务一个文件，文件名与服务在 `/etc/services` 中出现的服务名称完全一致。

`/etc/xinetd.conf` 文件本质上很简单：

```bash
# Simple configuration file for xinetd
# Some defaults, and include /etc/xinetd.d/
defaults
{
    instances                  = 60
    log_type                   = SYSLOG authpriv
    log_on_success             = HOST PID
    log_on_failure             = HOST
    cps                        = 25 30
}
include /etc/xinetd.d
```

该文件包含几行用于设置由 xinetd 管理的服务的默认限制。如果单个服务的配置文件中存在冲突的设置，则该单个文件设置优先。

> **警示**
> 你很可能会看到关于如何让服务以不同用户身份运行的问题，这可以通过编辑服务的配置文件并更改 user 行来实现。

其中几行需要进一步定义：

- **instances** — 这设置了允许的守护进程实例总数；此守护进程限制为 60 个实例。
- **cps** — 这限制通过 xinetd 允许每秒的连接数。超过最大值（25）会导致服务被禁用 30 秒，然后检查是否可以接受更多连接。
- 其他设置与日志记录有关，成功连接时记录主机和 PID，未成功连接时仅记录主机。

来自 `/etc/xinetd.d` 目录的单个服务配置文件，例如 `telnet`，将包含以下内容：

```text
 service telnet
 {
     disable     = yes
     flags       = REUSE
     socket_type = stream
     wait        = no
     user        = root
     server      = /usr/sbin/in.telnetd
     log_on_failure += USERID
     access_times   = 08:00-17:00
     only_from      = snowlower
 }
```

这些文件包含许多设置：

- **service** — 此关键字后必须跟随服务名称，例如 `telnet`。
- **disable** — 值包括 *yes*（禁用服务且不接受任何连接）和 *no*（不禁用或启用服务以接受连接）。
- **flags** — 存在许多且多样的标志；最常见的是 *REUSE*，它允许端口和服务接受多个连接。
- **socket_type** — 可以是 `stream`、`dgram`、`raw`、`rdm` 或 `seqpacket`。
- **wait** — 对于获取套接字并操作直至超时的单线程服务器，使用 `wait` 参数；对于在不活动时会释放套接字的多线程服务器，使用 `nowait`。
- **user** — 该服务应以哪个用户或组身份运行，这使您能够将有风险的服务限制在非 `root` 账户中运行。
- **server** — 这是客户端请求连接时运行的服务器或守护进程程序的完整路径和文件名。
- **log_on_failure** — 也可以是 `log_on_success`，值包括 `HOST`、`USERID` 和 `PORT`，仅列举几个选项。
- **access_times** — 此设置允许你为服务设置访问时间范围，例如前一个文件中从上午 8 点到下午 5 点。
- **only_from** — 这可以是主机名、IP 地址、地址通配符以及 `/etc/networks` 文件中定义网络名称的列表。

要启用由 `xinetd` 管理的服务，例如之前的 `telnet` 服务，你将使用以下命令：

```bash
chkconfig telnet on
```

这将使前面的文件包含以下内容：

```text
disable = no
```

服务现在已启用，可以接受请求的连接。对服务文件的更改不需要重启服务或 `xinetd`；这些更改会在你更改文件的服务的下一个及后续实例中生效。

![](img/49f4f38f3aec011238fa50f89e643db3_488_0.png)

> 如果你手动编辑 `/etc/xinetd.d/telnet` 文件，可能需要重启 `xinetd` 服务才能使更改生效。这是由 `chkconfig` 命令自动完成的。

要完全禁用服务由 `xinetd` 初始化管理，你将使用以下命令：

```bash
chkconfig telnet off
```

这会禁用该服务，并且 `xinetd` 从此忽略对该服务的请求。

在将新配置写入 `/etc/inetd.conf` 文件后，必须重启 inetd，但 xinetd 动态读取 `/etc/xinetd.d` 中的服务配置文件，只有在你更改 `/etc/xinetd.conf` 文件时才需要重启。

## 使用 TCP Wrappers 保护服务安全

如果你想保护按需服务，请使用 TCP wrappers 作为不常用服务的一层保护。

使用 TCP wrappers 的常见概念是，只有 `/etc/inetd.conf` 文件中的服务才能被包装或保护；这种说法是不正确的。TCP wrappers 软件包包含一个名为 `libwrap.a` 的库，越来越多的 Linux 服务参考该库以确保安全性。虽然过去确实服务必须包含在 `/etc/inetd.conf` 中以便由 `tcpd` 管理，但许多服务可以直接使用 `libwrap.a` 库和 allow/deny 文件来进行保护。

### inetd 和 TCP Wrappers

当与 inetd 一起使用时，使用 TCP wrappers 的概念是在每台机器上运行的每个服务前面放置一个控制守护进程，并指示谁被允许或被拒绝。在 inetd 广泛使用的时代，大多数服务没有内置保护，因此它们被配置为作为 `tcpd` 守护进程的参数运行。

`tcpd` 设置为参考 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件，以决定哪些主机被允许或拒绝访问由 `tcpd` 保护的服务。

### xinetd 和 TCP Wrappers

如果你正在使用 xinetd 或运行当前的 Linux 发行版，许多服务已开发为使用 `libwrap.a` 库，最终将 TCP wrappers 与 `inetd.conf` 文件分离。

对于当前发行版和 xinetd，任何能够引用 `libwrap.a` 的服务都有可能受益于 `hosts.allow` 和 `hosts.deny` 文件提供的保护。

此外，如果你希望运行一组既安全又快速的服务，你将使用 TCP wrappers 和独立守护进程，而不是使用

