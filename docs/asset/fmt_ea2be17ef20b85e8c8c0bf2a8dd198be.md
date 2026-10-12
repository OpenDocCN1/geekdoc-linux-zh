
`mesg` 命令禁止其他用户通过 `write` 命令等方式向你正在使用的终端（ty）写入内容。`stty` 命令关闭字符回显。这是必要的，因为否则对方发送的所有内容都会被回显给它。上面提供的最重要的 `pppd` 选项是 `-detach`，因为它防止 `pppd` 从控制终端中脱离。如果我们不指定这个选项，它将运行在后台，导致 shell 脚本退出。`silent` 选项让 `pppd` 在发送数据之前等待，直到接收到来自调用系统的数据包后才开始发送。这可以防止当调用系统启动 PPP 客户端较慢时发生传输超时。`modem` 选项让 `pppd` 监控 DTR 线以查看对方是否断开了连接，而 `crtscts` 则开启硬件握手。

除了这些选项外，你可能想强制进行某种认证，例如通过在 `pppd` 的命令行中指定 `auth` 或在全局选项文件中指定。手册页还讨论了用于开启或关闭单个认证协议的更具体的选项。

# 第8 章

## 各种网络应用

在成功设置 IP 和解析器后，你必须转向你想要通过网络提供的服务。本章涵盖了几个简单网络应用的配置，包括 `inetd` 服务器以及来自 `login` 家族的程序。还将简要介绍作为网络文件系统 (NFS) 和网络信息系统 (NIS) 等服务基础的远程过程调用接口。然而，NFS 和 NIS 的配置占据了更多空间，将在单独的章节中描述。这同样适用于电子邮件和网络。

当然，我们无法在书中涵盖所有的网络应用。如果你想安装一个这里没有讨论的程序，请参阅其手册页以获取详情。

### inetd 超服务器

通常，服务是由所谓的“守护进程”（daemons）执行的。守护进程是一个打开特定端口并等待传入连接的程序。如果发生连接，它会创建一个子进程来接受连接，而父进程则继续监听后续请求。这种概念的缺点是，对于提供的每个服务，必须有一个守护进程运行并监听端口等待连接发生，这通常意味着浪费了交换空间等系统资源。

因此，几乎所有的安装都会运行一个“超服务器”，它为许多服务创建套接字，并使用 `select(2)` 系统调用同时监听所有套接字。当远程主机请求其中一个服务时，超服务器会并并为该端口指定的服务器。

常用的超服务器是 `inetd`，即互联网守护进程（Internet Daemon）。它在系统启动时启动，从启动文件 `/etc/inetd.conf` 中获取它要管理的的服务列表。除了这些被调用的服务器外，还有许多个由 `inetd` 自身执行的微小服务，称为内部服务。它们包括简单生成字符字符串的 `chargen`，以及返回系统认为的当前时间的 `daytime`。

该文件中的条目由由以下字段组成的单行组成：

`service type protocol user server cmdline`

每个字段的含义在表 8.1 中列出。

| 表 8.1 字段定义。 |
| --- | --- |
| `service` | 提供服务名称。必须通过查找 `/etc/services` 文件将服务名称转换为端口号。该文件将在第 10 章中描述。 |
| `type` | 指定套接字类型，`stream`（用于面向连接的协议）或 `dgram`（用于数据报协议）。因此，基于 TCP 的服务器应始终使用 `stream`，而基于 UDP 的服务器应使用 `dgram`。 |
| `protocol` | 指定服务使用的传输协议名称。这可能是协议文件中找到的有效协议名称，下文也将进行解释。 |
| `wait` | 此选项仅适用于 `dgram` 套接字。它可以是 `wait` 或 `nowait`。如果指定了 `wait`，`inetd` 在任何时候只为指定的端口执行一个服务器。否则，它在执行服务器后会立即继续监听该端口。这对于读取所有传入数据包直到没有更多数据包然后退出的“单线程”服务器非常有用。大多数 RPC 服务器都是这种类型，并且应该指定 `wait`。相反的类型，“多线程”服务器允许无限数量的实例并发运行；这很少使用。这些服务器应该指定 `nowait`。`stream` 套接字始终使用 `nowait`。 |
| `user` | 这是正在执行的进程的登录 ID。这通常是 `root` 用户，但某些服务可能使用不同的账户。应用最小权限原则是一个非常好的主意，该原则规定如果程序不需要正常运行，就不应该在特权账户下运行命令。例如，NNTP 服务器将以 `news` 身份运行，而可能带来安全风险的服务（如 `tftp` 或 `finger`）将以 `nobody` 身份运行。 |
| `server` | 提供要执行程序的完整名称。内部服务标记为 `internal`。 |
| `cmdline` | 传递服务器的命令行。这包含了参数 0，即程序名。对于内部服务，此字段为空。 |

以下列表是 `/inetd.conf` 文件的示例。

# 列表 8.1 示例 /inetd.conf 文件。

```
#
### inetd services
ftp         stream nowait root      /usr/sbin/ftpd -l
telnet      stream nowait root      /usr/sbin/inetd -b/etc/issue
#finger     stream nowait bin      /usr/sbin/fingerd in.fingerd
#ftfp      dgram udp wait nobody    /usr/sbin/tftpd   in.tftpd
#ftfp      dgram udp wait nobody    /usr/sbin/tftpd /boot/diskless
login       stream nowait root      /usr/sbin/rlogind in.logind
shell       stream nowait root      /usr/sbin/rshd   in.rshd
exec        stream nowait root      /usr/sbin/rexecd   in.rexecd
#
          inetd internal services
#
daytime     stream nowait root internal
daytime     dgram udp nowait internal
time        stream nowait root internal
time        dgram udp nowait internal
echo        stream nowait root internal
echo        dgram udp nowait internal
discard     stream nowait root internal
discard     dgram udp nowait internal
chargen     stream nowait root internal
chargen     dgram udp nowait internal
```

`finger` 服务被注释掉了，因此不可。这通常出于安全考虑，攻击者可能利用它获取系统上的用户名。

`tftp` 也显示被注释了。`tftp` 实现的是原始文件传输协议，允许在没有密码检查的情况下传输系统上的任何可读文件。这在没有使用阴影密码时尤为有害。

`tftp` 通常用于无盘客户端和 X 终端从启动服务器下载代码。如果你由于这个原因需要运行 `ttftp`，请通过将这些目录名称添加到 `ttftp` 的命令行来限制其范围。这在列表 8.1 的第二个 `ttftp` 行所示。

# tpcpd 访问控制设施

将计算机开放到网络访问涉及许多安全风险，应用程序的设计用于防御多种类型的攻击。然而，其中一些可能存在缺陷。

# 116 Linux 网络管理员指南：第 8 章

（最显著的例子是 RTM 互联网蠕虫），或者如果不区分安全主机和对特定服务的请求，那么安全主机的请求将被接受，而不安全主机的请求将被拒绝。我们在上面已经简要讨论了 `finger` 和 `tftp` 服务。因此，人们希望将对这些服务的访问限制为“受信任主机”，但在通常的设置中是不可能的，因为 `inetd` 为所有客户端（或并非所有）提供服务。

实现此点的有用工具是 `tcpd`（由 Wietse Venema 编写，wietse@zw.win.tue.nl），它被称为守护进程封装（daemon wrapper）。对于你想要监控或保护的 TCP 服务，它将代替服务器程序被调用。`tcpd` 将请求记录到 syslog 守护进程，检查远程主机是否允许使用该服务，如果成功，它将执行真正的服务器程序。注意，这不适用于基于 UDP 的服务。

例如，为了封装 `finger` 守护进程，你需要更改 `inetd.conf` 中的相应行：

```
# wrap finger daemon
finger stream tcp nowait root /usr/sbin/tcpd.fingerd
```
