
### 18.3 SSH Tunnel

如果有 root 权限，可以使用 `iptables` 创建端口转发。特定主机的 `iptables` 端口转发设置可能取决于已有的配置。要在 Linux 中转发数据包，需要向 `/proc/sys/net/ipv4/interface/forwarding` 写入“1”来启用我们要转发的接口（如果尚未配置允许转发）。

本学习单元涵盖了 SSH 隧道的基础知识：
1. 学习 SSH 隧道的基础知识
2. 使用 SSH 本地、动态、远程和远程动态端口转发方法
3. 理解 SSH 隧道的优缺点

从高层次来说，隧道（tunneling）描述的是数据流在跨网络传输时封装的行为。某些隧道协议专门为此设计。Secure Shell（安全壳）就是其中一个例子。

SSH 最初开发是为了让管理员能够通过加密连接远程登录到他们的服务器。在 SSH 之前，`rlogin` 和 `Telnet` 等工具提供了类似的远程管理功能，但是在未加密的连接上运行的。

在每个 SSH 连接的后台，命令、密码和数据都会通过使用 SSH 协议构建的加密隧道进行传输。SSH 协议主要是一种隧道协议，因此可以通过 SSH 连接传递任何类型的数据。由于这个原因，绝大多数 SSH 工具都内置了隧道功能。

SSH 隧道的另一个巨大优势是它可以轻松地融入到网络环境的背景流量中。网络管理员经常使用 SSH 进行合法的远程管理，以及在限制性网络情况下的灵活的端口转发设置。在 Linux 主机上安装 SSH 客户端软件或在那里运行 SSH 服务器是常见现象。如果网络环境没有被严密监控，SSH 流量看起来与普通的管理流量相似。其内容也无法被监控。

在大多数官方文档中，通过 SSH 连接传输数据被称为端口转发（port forwarding）。不同的 SSH 软件提供的提供的功能略有不同。我们将使用 OpenSSH 提供的常用端口转发类型。

(Wikipedia, 2019), https://en.wikipedia.org/wiki/Tunneling
(Wikipedia, 2022), https://en.wikipedia.org/wiki/Secure_Shell
(SSH, 2018), https://www.ssh.com/protocol/
(Wikipedia, 2022), https://en.wikipedia.org/wiki/Berkeley_r-commands
(OpenSSH, 2022), https://www.openssh.com/
(SSH, 2022), https://www.ssh.com/academy/ssh-tunneling

SSH 端口转发在网络情况下是非常强大的工具，对于在限制性环境下工作的攻击者来说，它也可以是一个非常有用的选项。

### 18.3.1 SSH 本地端口转发

让我们回顾 `Socat` 场景中的第一个端口转发示例。我们设置 `Socat` 在 `CONFLUENCE01` 的外网接口上监听 TCP 端口 `2345`。接收到该端口的数据包被转发到 `PGDATABASE01` 上的 TCP 端口 `5432`。我们通过这种方式，连接到 `PGDATABASE01` 上的 PostgreSQL 服务。这种情况的关键在于监听和转发都来自同一台主机（`CONFLUENCE01`）。

SSH 本地端口转发在此加入了一个微妙的变化。在 SSH 本地端口转发中，数据包不是由 SSH 服务器转发的。相反，两个主机（SSH 客户端和 SSH 服务器）之间建立了 SSH 连接，由 SSH 客户端打开一个监听端口，在该端口接收的所有数据包都通过 SSH 连接隧道到 SSH 服务器。然后由 SSH 服务器将其转发到我们指定的套接字。

这个概念目前可能有点抽象。通过练习设置本地端口转发，我们可以更好地理解它。

让我们重新考虑之前的场景并稍作修改：`CONFLUENCE01` 上不再可用 `Socat`。我们仍然拥有之前从 Confluence 数据库破解的所有凭据，并且没有防火墙阻止我们连接到在 `CONFLUENCE01` 上绑定的端口。

使用 `database_admin` 凭据，我们将连接 `PGDATABASE01`。在这种情况下，我们使用 SSH 本地端口转发来桥接。我们在本地 Kali 上打开一个端口，发送到该端口的所有流量都会通过 SSH 连接隧道到 `CONFLUENCE01`，然后由其转发到 `PGDATABASE01`。

(OpenBSD manual, 2022), https://www.openbsd.org/ssh

# OffSec

使用 Kali Linux 进行渗透测试

欢迎使用 Ubuntu (GNU/Linux 5.4.0-122-generic x86_64)

+ * 文档：https://help.ubuntu.com
* 管理：https://landscape.canonical.com
* 支持：https://ubuntu.com/advantage

系统信息，截至 2022年8月18日周四 03:01:09 PMC

| 进程: | 241 |
| --- | --- |
| 系统负载: 0.0 | 2 |
| 使用率: 7.7768 的 59.4% | 登录用户: ens192:10.4.50.215 |
| 内存使用: 16% | IPv4 地址: |
| 交换空间使用率: 0% | ens224 的 IPv4 地址:172.16.50.215 |

有 0 个更新可以立即应用。

上次登录：2022年8月18日周四 14:33:08 来自 10.4.50.63

`database_admin@pgdatabase01:-`

列表 539 - 使用 Python 的 pty 提供 shell TTY 功能，并以 `database_admin` 身份登录 `PGDATABASE01`。

现在我们已经建立了到 `CONFLUENCE01` 上 `PGDATABASE01` 的 SSH 连接，我们将运行 `ip addr` 来查询所有可网络接口。

```
database_admin@pgdatabase01:-$ ip addr
1: lo <LOOKBACK,UP,LOWER_UP> mtu 65536 qdisc noiscop state UNKNOWN group default qlen 1000
    link/ether 00:00:00:00:00:00 br 00:00:00:00:00:00
    inet 127.0.0.1/8 host
        valid_ preferred preferred_lft
    inet6 ::/128 host
        valid_ preferred preferred_lft
2: ens192 <BROADCAST,MULTICAST,LOWER_UP> mtu 1500 qdisc fq_codate UP group default qlen 1000
    link/ether 80:50:6a:b9:bd ff:ff:ff:ff:ff:ff
    inet 10.4.50.215/24 br 10.4.50.255 scope global ens192
        valid_ preferred preferred_lft
    inet6 fe80::25ff:fe60:db6:6 link
        valid_ preferred preferred_lft
3: ens224 <BROADCAST,MULTICAST,LOWER_UP> mtu 1500 qdisc fq_codate UP group default qlen 1000
    link/ether 80:50:6a:b9:bd ff:ff:ff:ff:ff:ff
    inet 172.16.50.215/24 br 172.16.50.255 scope global ens224
        valid_ preferred preferred_lft
    inet6 fe80::25ff:fe60:db6:4 link
        valid_ preferred preferred_lft
4: ens256 <BROADCAST,MULTICAST> mtu 1500 qdisc noisc state DOWN group default qlen 1000
    link/ether 80:50:6a:b9:bd ff:ff:ff:ff:ff:ff
```

列表 534 - 在 `PGDATABASE01` 上列举网络接口。

我们将运行 `ip route` 来发现路由表中已经存在了哪些子网。

```
database_admin@pgdatabase01:-$ ip route
10.4.50.0/24 dev ens192 kernel link scope global 10.4.50.215
10.4.50.0/24 via 10.4.50.254 dev ens192 proto static
```

PWK - 2023 OffSec Services Limited. 版留所有。

制作于摩洛哥
