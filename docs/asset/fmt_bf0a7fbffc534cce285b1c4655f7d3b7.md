
# `iptables -t nat -A PROSUTING -o SNAT --to-source 12.12.12.12`

```
```

## 第三部分：管理 Fedora 和 RHEL

- **限制** — 使用 `--limit` 选项来限制产生日志消息的匹配速率。此选项允许每秒仅产生有限次数的消息（默认值为每小时 2 次，允许突发 5 次）。
- **拒绝服务攻击（DOS 攻击）** — 你可以使用 `--limit` 选项来减少 DOS 攻击的影响，但它无法完全停止攻击。只要流量指向你的服务器，你的网络带宽就会被耗尽，机器也会消耗资源来忽略这些数据。
- **表类型** — 默认表类型是 `filter`。其他类型的表有 `nat`（用于 IP 伪装）和 `mangle`（用于修改数据包）。要使用其他表，必须添加 `-t table_type` 选项，其中 `table_type` 为 `nat` 或 `mangle`。

## 使用 TCP Wrappers 控制对服务的访问

完全禁用不使用的服务是免费的，但对于你真正需要的服务呢？你可以选择性地授予或拒绝对这些服务的访问。在 Red Hat Linux 之前的版本中，使用 `tcp` 守护进程 `tcpd` 来实现某些选择性访问。在当前的 Fedora 版本中，`tcp` wrapper 支持已集成到 `xinetd` 中。你可以查看 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件来决定何时为 `login`、`rsh`、`telnet`、`finger` 和 `talk` 等服务授予或拒绝特定连接。TCP wrappers 也默认适用于其他服务，例如 `ftp` 服务器（在 `vsftpd.conf` 文件中设置 `tcp_wrappers=YES`）。

当请求一个依赖 TCP wrappers 的服务时，系统会扫描 `hosts.allow` 和 `hosts.deny` 文件，并检查与连接机器 IP 地址匹配的条目。这些检查发生在连接尝试期间：

- 如果地址在 `hosts.allow` 文件中，则允许连接且不检查 `hosts.deny`。
- 如果地址在 `hosts.deny` 中（但不在 `hosts.allow` 文件中），则拒绝连接。
- 如果地址在两个文件中都不存在，则允许连接。

没有必要（甚至不可能）列出可能连接到你计算机的每一个地址。`hosts.allow` 和 `hosts.deny` 文件允许你指定整个子网和地址组。你可以使用关键字 `ALL` 来指定所有可能的地址。你还可以限制这些文件中的特定条目，使其仅适用于特定的网络服务。

查看一个典型的 `hosts.allow` 和 `hosts.deny` 文件对的示例。这里是 `/etc/hosts.allow` 文件：

```
# hosts.allow 此文件描述了由 '/usr/sbin/tcpd' 服务器决定的允许使用本地 INET 服务的主机名。

cups-lpd: 199.170.177.

in.telnetd: 199.170.177, ..ninuxtoys.net

vsftpd: ALL
```

这里是 `/etc/hosts.deny` 文件：

```
# hosts.deny
# 此文件描述了*不* 允许使用本地 INET 服务的主机名，
# 这些名是由 /usr/sbin/tcpd/ 服务器决定的。
```

前面的示例是一个相当严格的配置。它允许来自某些主机的 `cups-` 和 `inet` 服务的连接，但拒绝了所有其他连接。它还允许所有主机连接 FTP 服务 `vsftpd`。它在文件中留下了示例：

通常情况下，以 `#` 字符开头的行是注释，`xinetd` 在解析文件时会忽略它们。每行非注释行由由逗号分隔的守护进程列表组成，后面跟着冒号 `:`，然后是尝试访问你系统网络服务的任何计算机。

客户端可以是数字 IP 地址（例如 `199.170.177.25`）或主机名（例如 `jukebox.linuxxtoys.net`），但更多是指定地址范围的通配符变体。客户端有四种形式。`hosts.allow` 文件的在线手册页对其描述如下：

- 以点 `.` 字符开头的字符串。如果主机名的组成部分匹配指定的模式，则匹配主机名。例如，模式 `.tue.nl` 匹配主机名 `wzv.win.t.nl`。
- 以点 `.` 字符结尾的条目。如果主机地址的数字字段与给定字符串匹配，则匹配地址。例如，模式 `131.155` 匹配埃因霍芬大学网络上几乎每个主机的地址 `131.155.-x.x`。
- 以 `@` 符号开头的条目被视为 NIS 组名。如果该主机是指定网络的主机成员，则匹配主机。守护进程名称或客户端用户不支持网group 匹配。
- 形式为 `n.n.n.n/m.m.m` 的表达式被解释为网络/掩码。如果 `net` 等于 `mask` 的位与运算结果，则匹配主机地址。例如，网络/掩码 `131.155.72.0/255.255.254.0` 匹配 `131.155.72.0` 到 `131.155.73.255` 范围内的每一个地址。

示例 `host.allow` 包含了前两种类型的客户端规范。`199.170.177.` 将匹配任何以该开头的 IP 地址，例如 `199.170.177.25`。条目 `.linuxxtoys.net` 将匹配如 `jukebox.linuxxtoys.net` 或 `.frame.linuxxtoys.net` 等主机名。

让我们检查当名为 `jukebox.linuxxtoys.net`（IP 地址为 `199.170.177.8`）的主使用 Telnet 协议连接到你的 Fedora 系统时发生了什么：

1. `xinetd` 接收到连接请求。
2. `xinetd` 开始将 `jukebox.linuxxtoys.net` 的地址和名称匹配 `/etc/hosts.allow` 中列出的规则。它从文件顶部向下查找，直到找到匹配。守护进程（在 Fedora 上处理网络服务的程序）和连接客户端的 IP 地址或名称都匹配 `hosts.allow` 中的信息。在这种情况下，遇到请求的第二个规则是：`in.telnetd:199.170.177., .linuxxtoys.net`
3. `jukebox` 不在 `199.170.177.0` 子网中，但它在 `linuxxtoys.net` 域中。`xinetd` 一旦发现此匹配就会停止搜索。

如果 `jukebox` 使用 CUPS-lpd 协议连接到你的机器会怎样？在这种情况下，它没有匹配 `hosts.allow` 中的任何规则；引用 `lpd` 守护进程的唯一行并没有引用 `199.170.177.` 子网或 `linuxxtoys.net` 域。`xinetd` 继续检查 `hosts.deny` 文件。条目 `ALL` 匹配任何内容，因此 `tcpd` 拒绝了连接。通配符也会出现在 `hosts.allow` 中。对于运行一个互联网上任何人都可以访问的匿名 FTP 服务器是合适的。如果你没有运行匿名 FTP 站点，你可能不应该使用 `ALL`。
