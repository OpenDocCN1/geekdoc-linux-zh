
```
tcpmux      1/tcp       # TCP 端口服务复用器
echo        7/tcp
echo        7/udp
discard     9/tcp          sink null
```

# 408 Corel Linux 操作系统入门教程：官方指南

```
discard  9/udp      sink null
systat   11/tcp      users
daytime  13/tcp
daytime  13/udp
netstat 15/tcp
qotd     17/tcp      quote
sp      18/tcp      #消息发送协议
sp      18/udp      #消息发送协议
charger 19/tcp      ttytyst source
charger 19/udp      ttytyst source
ftp-data 20/tcp
ftp       21/tcp
fsp      21/udp      fspd
ssh       22/tcp      # SSH远程登录协议
ssh       22/udp      # SSH远程登录协议
telnet   23/tcp
```

左侧列包含服务的名称。中间列包含调用该服务所需的特定协议：`TCP`（传输控制协议）或 `UDP`（UNIX 数据报文协议）。注意，大多数服务都包含这两种协议的条目，以涵盖所有情况）。最后一列包含关于服务的其他信息，例如别名或注释。

此文件中的某些服务（如 `FTP` 和 `Telnet`）用于与互联网等网络进行交互。其他服务（如 `echo` 和 `discard`）主要供各种内部程序使用。

## /etc/inetd.conf 文件

`inet` 的主配置文件是 `/etc/inetd.conf`。该文件为 `inet` 程序提供信息，使其能够以正确的方式启动其各种子服务器。`/etc/inetd.conf` 文件的片段所示所示：

```
#
ftp      stream  tcp  nowait root      /usr/sbin/tcpd  in.ftpd
telnet   stream  tcp  nowait root      /usr/sbin/tcpd  in.telnetd
#n# Shell, login, exec, comsat and talk 是 BSD 协议。
#
```

## 第 25 章：INET 服务 409

| 服务 | 类型 | 协议 | 标志 | 用户 | 路径 | 服务器 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| shell | stream | tcp | nowait | root | /usr/sbin/tcpd | in.rshd |
| login | stream | tcp | nowait | root | /usr/sbin/tcpd | in.rlogind |
| #exec | stream | tcp | nowait | root | /usr/sbin/tcpd | in.rexecd |
| #comsat | dgram | udp | wait | root | /usr/sbin/tcpd | in.comsat |
| talk | dgram | udp | wait | nobody.tty | /usr/sbin/tcpd | in.tkalkd |
| ntalk | dgram | udp | wait | nobody.tty | /usr/sbin/tcpd | in.ntalkd |

为了更好地理解 `/etc/inetd.conf` 中条目的结构，请详细考虑以下单行：

- `ftp` `stream` `nowait` `root` `/usr/sbin/tcpd` `in.ftd`

- `ftp` 此条目中正在配置的服务。

- `stream` 此列定义了所使用的 socket 类型。Socket 类型通常对应 `TCP` 和 `UDP` 协议；`/etc/inetd.conf` 中的大多数条目使用 `stream` (`TCP`) 或 `dgram` (`UDP`) 类型（`dgram` 是 *datagram* 的缩写）。`Stream` 意味着该服务处理数据流， `TCP` 协议如此；`tcp` 此列定义了使用的协议；你通常可以从 socket 类型推断协议类型，但 `/etc/inetd.conf` 要求显式说明协议。

- `nowait` *flags* 列，通常仅适用于 `datagram` socket；它涉及 `datagram` socket 如何管理传递单个数据单元的连接。你通常会在该列中看到“wait”或“nowait”。

- `root` 用户列。此处的条目是运行程序的环境的用户名称。例如，如果用户是“root”，程序将以所有超级权限运行。出于安全考虑，某些服务器可能会以普通用户身份运行，权限较低。

- `/usr/sbin/tcp` 实际服务器位置的目录路径。你需要指定此路径，以便 `inetd` 知道在哪里找到被调用的服务。

- `in.ftpd` `inetd` 在收到适当请求时调用的服务器文件名和程序的实际文件名。如果没有它，`inetd` 将不知道该做什么。

## 410 Corel Linux 操作系统入门教程：官方指南

你想要从 `inetd` 的每个服务都必须在 `/etc/inetd.conf` 文件中有一个条目。如果没有条目，该服务将不会运行。假设你决定完全不想处理传入的 `FTP` 连接；你可以从 `/etc/inetd.conf` 中删除 `FTP` 条目（或多个条目），或者简单地通过在行开头放置 `#` 符号将其注释掉。如果你完成了此方法，你需要重启 `inetd` 程序。通过在文本提示符执行此命令来实现（你必须以 `root` 身份登录或已获得超级权限）：

```
/etc/init.d/netbase restart
```

`netbase` 脚本启动许多网络守护进程，包括 `inetd`。

## inet 的子服务

在本节中，我们将更仔细地查看由 `inetd` 控制的一些服务。注意，`inetd` 只处理我们可能称为“互联网服务”的某些选择。`Apache`（万网服务器）和 `INN`（新闻新闻服务器）传统上并不通过 `inetd` 处理。有些人确实通过 `inetd` 运行 `Apache`，但这种权衡在于

### Telnet

`Telnet` 是允许远程用户登录你的计算机的服务。它是 `TCP/stream`，因为它是交互式的。处理传入 `Telnet` 的程序默认运行在 `23` 端口。密码以明文形式通过网络传输。这意味着，如果某些心叵测的人使用被称为嗅探器的程序监控网络连接，那些密码很容易被捕获并用于

### FTP

`FTP` 是允许在机器之间移动文件的服务。与 `Telnet`一样，它是 `TCP` 服务。`FTP` 由文件 `in.ftpd` 控制，其默认端口为 `21`。

### login 和 rsh

`login` 和 `rsh` 是类似于 `Telnet` 的服务。`login` 与 `Telnet` 相同，它允许在远程机器上执行命令。`login` 由文件 `in.rlogind` 处理，其默认端口为 `513`。

### ssh

`ssh` 是 `login`、`rsh` 和 `Telnet` 的替代品。这三个服务的共同问题是密码安全性；在 `login`、`rsh` 或 `Telnet` 下，用户用于验证身份的密码是明文。`ssh` 通过将明文连接替换为加密连接解决了这个问题。由于美国法律禁止国际传播加密软件，未在所有 Linux 发行版中发行。在美国，可以从 `ftp://metalab.unc.edu/pub/packages/security/ssh` 下载包。`ssh` 主页位于 `http://www.ssh.org`；查看网站上的 FAQ 页面以确保下载和使用 `ssh` 是合法的。我们不想让你因非法出口加密软件而被捕。

`sshd`（`ssh` 守护进程）并不总是从 `inetd` 运行。通常，它会在你手动或通过初始化脚本调用时自行运行。但是可以从 `inetd` 运行 `ssh`。在 `/etc/inetd.conf` 中添加此行：

```
ssh stream nowait root /usr/sbin/ssh -i
```

然后向 `/etc/services` 中添加此行：

```
ssh     22/tcp    # SSH远程登录协议
```

为了强制你的远程用户使用这种安全方法，最好禁用 `rlogin`、`rsh` 甚至 `Telnet`。通过删除或注释掉 `/etc/inetd.conf` 中的这些行来实现。

> 注意 我们将在第 28 章“用户管理与安全”中更详细地讨论系统安全。如果你计划经常在互联网上使用计算机，或者你有如电缆调制解调器或 DSL 这样的持续连接，我们强烈建议你使用某种加密登录。

## 第 26 章

## Web 服务

![](img/b608ba7a04add87643140fbc345d68f8_448_0.png)

## 414 Corel Linux 系统入门指南：官方指南
