
我们的 `vpn-server` 和 `vpn-client` 程序编写时能够建立任意数量的任意 VPN 连接。这些命令通过检查程序名和参数来确定应该创建哪一个 VPN。如果指定了两个参数（如 `vpn-server start vpn1`），则第二个参数是 VPN 名称。如果通过符号链接（如 `/etc/init.d/vpn` 或 `/etc/rc.d/S99vpn1`）调用，它将使用程序名，并删除任何开头的 `#`（或 `K##`），从而产生 VPN 名称 `vpn1`。换句话说，脚本通过 `authorized_keys(2)` 文件中的命令行选项直观地推断出 VPN 名称。一旦确定了 VPN 名称，它将从文件 `/opt/ssh-vpn/etc/vpn_name` 获取其配置变量。因此，对于名为 `vpn1` 的 VPN，我们将创建一个 `/opt/ssh-vpn/etc/vpn1` 文件。配置文件中的每个变量都以 `server_` 或 `client_` 开头，这意味着如果你可以在系统之间共享它们而不必担心冲突。表 3.3 显示的变量是必要的。

# 表 3.3 配置文件变量

| 变量 | 使用者 | 示例 | 解释 |
| --- | --- | --- | --- |
| `client_network` | server | 192.168.1.0/24 | VPN 客户端上的网络。VPN 服务器通过 `route add` 命令建立到远程网络。 |
| `server_network` | client | 192.168.2.0/24 | VPN 服务器上的网络。VPN 客户端通过 `route add` 命令建立到远程网络。 |
| `server_ppp_ip` | server | 192.168.254.254 | VPN 服务器端的 PPP 链路地址。确保该地址在任何机器上可用。 |
| `client_ppp_ip` | server | 192.168.254.253 | VPN 客户端端的 PPP 链路地址。确保该地址在任何机器上可用。 |

# 表 3.4 配置文件可选选项

| 变量 | 使用者 | 示例 | 解释 |
| --- | --- | --- | --- |
| `client_debug` | client | yes | 在 `pppd` 参数中添加调试选项，并启用 `vpn-client` 脚本的 `set -x` 输出用于详细日志。 |
| `server_debug` | server | yes | 为 `pppd` 添加调试选项。 |
| `client_ssh_args` | client | -c | 此 VPN 特有的额外 ssh 参数。 |
| `client_pppd_args` | client | usepeer | 此 VPN 特有的 `pppd` 额外命令行参数。 |
| `server_pppd_args` | server | proxy | 此 VPN 特有的 `pppd` 额外命令行参数。 |

表 3.4 继续

| 变量 | 使用者 | 示例 | 解释 |
| --- | --- | --- | --- |
| `client_require_pap` | client | yes | VPN 客户端要求服务器的 PAP 认证。yes 以外的值等同于 no。 |
| `server_require_pap` | server | yes | VPN 服务器要求客户端的 PAP 认证。yes 以外的值等同于 no。 |
| `client_require_chap` | client | yes | 对于 CHAP 协议与 `client_require_pap` 相同。 |
| `server_require_chap` | server | yes | 对于 CHAP 协议与 `server_require_pap` 相同。 |

一个示例配置如下：

```
# VPN1 配置文件
# /opt/ssh-vpn/etc/vpn1

### 双方连接的网络，适用于
### 'route' 命令
client_network=192.168.2.0/24
server_network=192.168.1.0/24

### 我们需要调试信息吗？
client_debug="no"
server_debug="yes"

# 为每个需要的 VPN 选择不同的 IP。
server_ppp_ip=192.168.254.254
client_ppp_ip=192.168.254.253

# 我们应该要求 PPP 认证吗？
client_require_pap="yes"
server_require_pap="yes"
client_require_chap="no"
server_require_chap="no"

# 需要非标准的 ppp 参数吗？放在这里。
#client_pppd_args="usepeer"
#server_pppd_args="proxy"

# 需要额外的 ssh 参数吗？放在这里
#client_ssh_args="-C"
#server_ssh_args="*"
```

### VPN 脚本

你有两种主要方法来控制你的 ssh 命令。一种是在 `~/.ssh/config` 中创建条目，如本章之前所示。你也可以替换（或额外）将它们放在 `client_ssh_args` 变量中。此变量是一个紧接在 `pppd` 的 `pty` 参数中指定的 `$SSH` 命令之后的字符串。

你可以包含 `-l username` 或 `-p 222` 等选项。你也可以放置 `~/.ssh/config` 中提供的任何任意选项，但你必须对其进行微调。例如，`~/.ssh/config` 选项 `Hostname client.example.org` 的命令行变体是 `-hostname=client.example.org`。

我们通常倾向于将所有的 ssh 配置放在一个位置，要么在 `~/.ssh/config` 中，要么在 `/opt/ssh-vpn/etc/vpn_name` 中。这有助于一次性看到所有选项。

### 启动和停止 VPN

要手动启动 VPN，你只需在客户端运行以下命令：

```
falcons-client# /etc/init.d/vpn start
```

你只能在客户端启动 VPN，因为是 VPN 发起了 SSH 连接。要停止 VPN，你可以运行以下命令：

```
root# /etc/init.d/vpn stop
```

你可以从客户端或服务器停止 VPN，因为它做的只是杀掉相关的 `pppd` 命令。你也可以通过手动指定 VPN 名称给 `vpn-server` 或 `vpn-client` 命令来启动或停止 VPN，例如：

```
bears-server# /opt/ssh-vpn/bin/vpn-server stop vpn1
falcons-client# /opt/ssh-vpn/bin/vpn-client start vpn1
```

### 支持多个 VPN

我们的脚本设计支持任意数量的 VPN 连接，你发起或维持的数量取决于可用资源（内存、处理能力、进程数等）。每个 VPN 必须使用自己的 SSH 身份。这是必要的，因为服务器使用客户端的 SSH 身份通过命令行选项在 `authorized_keys(2)` 文件中设置 VPN 名称。

假设我们要创建一个名为 `vpn2` 的第二个 VPN 连接。在身份创建阶段，我们将使用 `ssh-keygen` 创建一个新的 SSH 身份，但包含一个文件名参数，如下：

```
sshvpn@falcons-client$ ssh-keygen -f /opt/ssh-vpn/.ssh/identity.vpn2 -t rsa -N ''
```

# 第3 章 使用 SSH 和 PPP 构建 VPN

（将 `-t rsa` 替换为 `-t dsa` 或 `-t rsa` 以创建 SSH2 密钥。）

要强制让你的 `vpn-client` 脚本使用此配置而非默认配置，请向 `/opt/ssh-vpn/.ssh/config` 中添加以下内容：

```bash
Host vpn2
Identity /opt/ssh-vpn/.ssh/identity.vpn2
```

你也可以将以下内容添加到 `vpn2` 配置文件 `/opt/ssh-vpn/etc/vpn2` 中：

```bash
client_ssh_args='-i /opt/ssh-vpn/.ssh/identity.vpn2'
```

## 故障排除

SSH 之上的 PPP 是一个棘手的家伙。接下来的章节将讨论在尝试让其工作时，你可能需要的若干实用的故障排除措施。

## PPP 失败

如果 `pppd` 无法正确建立 PPP 连接，请在两端都使用调试选项来查看 `pppd` 失败的原因，并检查你的系统日志。

如果你无法看到看到调试信息，请确保已配置了 syslog 来报告所有调试消息。`pppd` 通常被编译为使用 daemon-facility，因此确保你的 `/etc/syslog.conf` 中有一行类似于 `daemon.debug /var/log/messages` 的内容。你可能更倾向于使用 `logfile` 选项来查看 `pppd`。

如果你遇到 PAP 或 CHAP 认证问题，请考虑为 `pppd` 使用 `show-password` 参数进行额外调试。在验证它们是问题根源之前，你可能想关闭 PAP 或 CHAP 要求。

如果你的 PPP 连接已正确建立但你没有获得路由，请确保你的脚本是以适用于你的 Linux 发行版的方式从 `ip-up` 用的。同时，确保在 VPN 配置文件中设置了 `client_network` 和 `server_network` 的值。为了验证语法，你可能想尝试使用这些变量中指定的值手动添加路由。

## SSH 失败

尝试从客户端手动 `ssh` 连接到服务器（使用你打算用于 VPN 的相同参数），并查看是否可以无密码登录。如果配置正确，远程端应该自动启动 `pppd`，你应该能在屏幕上看到 PPP 握手的杂乱信息。

如果你收到 `Aborted by user` 错误，请确保在接受并验证服务器主机密钥之前，没有为 SSH 登录设置 `BatchMode`。确保你已将公钥存放在正确的客户端文件中：SSH1 对应 `~/.ssh/authorized_keys`，SSH2 对应 `~/.ssh/authorized_keys2`。

## 局限性

在客户端，使用 `-v` 选项运行 `ssh` 以获取详细调试信息。在服务器上，检查你的系统日志。确保你正在通过 syslog 记录所有调试消息。SSH 通常使用 auth 设施，因此确保你的 `/etc/syslog.conf` 中有一行类似于 `auth.debug /var/log/messages` 的内容。或者，你也可以尝试使用 `-d` 选项手动运行 `ssh`，以便在前台运行并将调试信息输出到终端。

如果 SSH 连接未建立，请尝试在 `~/.ssh/config` 或 `Client_ssh_args` 变量中显式指定你想要的 SSH 版本。此外，确保你使用的是兼容的身份标识。在两台机器上运行相同版本的 SSH 是一个好主意，因为你将面临更少的操作性问题。

## 网络问题

如果 PPP 连接已建立但你发现某些或所有数据包未通过，请检查 `/proc/sys/net/ipv4/ip_forward` 中相应的 IP 转发值。同时检查是否有任何 `iptables` 规则可能会拦截数据包。使用 `iptables` 的 `-v` 选项记录数据包并检查你的系统日志。

如果你在远程网络上查找主机名遇到困难，请考虑在 PPP 中使用 `peers` 选项（通常在客户端）。

## 局限性

VPN 运行在 SSH 上，SSH 是一个 TCP 协议。传输控制协议是一种可靠协议，会自动处理重传远程端未收到的数据包。因此，数据包要么到达另一端并被及时确认，要么连接在超时后被终止。将 TCP 用于 VPN 有一个缺点：我们在这条连接上封装了 IP 协议（TCP、UDP、ICMP）。特别是，UDP（用户数据报协议）用于不需要保证可靠递送的情况，例如数据包丢失不会产生灾难性影响的流媒体传输。当这些数据包通过 TCP 连接发送时，它们的传输将得到保证，而通常可能会丢失的数据包反而会被重传。这可能导致你的 VPN 比认为的要慢。

PPP 最初仅构建用于处理 TCP、UDP 和 ICMP 等 IP 协议。因此，任何非 IP 流量都无法通过 VPN。尽管 `pppd` 确实支持 IPX（Novell NetWare 使用的协议），但 `pppd` 中某些 IPX 相关的选项可能需要你调整才能使其工作。请参考 `ppp(8)` 帮助页。

## 总结

在本章中，我们讨论了成功使用 PPP 和 SSH 创建安全 VPN 所需的所有组件。我们为你提供了即插即用的脚本，既可扩展又易使用。然而，即使有了这些工具，第一次设置 PPP 也是件令人头疼的事。你可能会发现自己仍在调试连接，尽管它已经正常运行了几个月。SSH 之上的 PPP 是一种经过验证的方法。这些协议非常稳健、定义良好，而且最重要的一点是——不像许多其他 VPN 技术那样正处于变动状态。

# 使用 SSL/TLS 和 PPP 构建 VPN

大多数想要使用 PPP 建立 VPN 的人已经使用过 SSH。这部分归因于 VPN 开始创建时，SSH 易于获取。PPP 可以封装在任何安全协议中，SSL 显然符合这一要求。然而，很少有人尝试过这种方法。

当你完成本章后，你将能够手动或使用提供的脚本来使用 SSL/TLS 和 PPP 创建 VPN。我们认为你会发现它与 SSH 之上的 PPP 足够相似，从而感到熟悉，甚至可能比使用 SSH 更轻量、更简洁。

## PPP-over-SSL 概述

为了理解 PPP-over-SSL/TLS 的实现，我们必须首先描述涉及的协议。

### PPP

PPP 代表点点协议（Point-to-Point Protocol）。PPP 是流行的分级数据链路控制（HDLC）（另一种二层点对点协议，通常用于 T1 线路）的派生版本，用于完成线路控制活动并封装用户数据。PPP 最常用于在电话线上的调制调器之间建立连接，例如拨号接入 ISP 时。大多数 Linux 发行版都带有如下工具：

# 第 4 章 使用 SSL/TLS/PPP 构建 VPN

（此处对应原文位置）这些工具允许你无需调整底层的 PPP 命令和配置即可建立现代调制调器连接。然而，PPP 并不限于物理连接；PPP 连接可以在任何具有网络连接的主机之间建立。我们的目标是在互联网上的不同机器之间建立 PPP 连接，并用它建立 VPN。

要运行 `pppd`（PPP 协议守护进程），内核必须支持它。PPP 通常被编译为模块，你可以通过 `insmod` 命令进行查询。如果是这样，它会在需要时自动加载。大多数 Linux 发行版的内核都构建了 PPP 支持，因此这不是一个问题。

大多数 Linux 发行版还提供了预编译的 PPP 版本供你安装。你可能不需要自己编译安装 `pppd`。然而，由于后续提到的原因，我们建议 `pppd` 2.3.7 或更高版本。

PPP 的重点一直是传输数据的隐私，作为直接结果，它依赖外部加密方法来解决这个问题。电话线上 PPP 数据拦截的风险限于线路分接或链路末端的物理存在。然而，由于我们想通过互联网发送流量使用 PPP 建立连接，我们必须将此 PPP 连接隧道到加密层内部。

## SSL/TLS

安全套层（SSL）协议的创建是为了允许安全的网络通信。SSL 使用强加密通过封装来保护明文协议——字面上将其封装在加密层内部。被封装的协议（如 HTTP、POP 或 NNTP）不需要了解任何密码学知识。事实上，它甚至不知道自己正在通过 SSL 安全地传输。所有的加密和解密不仅仅是加密层到明文的翻译。它还，

### SSL/TLS 历史

SSL 由 Netscape Communications 创建。最初的协议设计 SSL 1.0 版本于 1994 年 7 月完成，但并未发布。SSL 2.0 版本于 1994 年 12 月发布，并包含在 Netscape 浏览器中。SSLv2 被发现存在一些缺陷，其中最显著的一个问题是：攻击者可以在支持更高级加密算法的情况下，欺骗端点使用弱加密方法。

Netscape 于 1995 年 11 月发布了 SSL 3.0 版本，该版本修复了这些缺陷。它还包含许多增强功能，例如支持额外的加密算法、将身份验证和加密密钥解耦、允许加密算法协商以及提高协议的安全性。

1999 年 1 月，SSLv3 被用作传输层安全（TLS）协议的基础，该协议是在 RFC-2246 中定义的规范。TLS 包含了 SSLv3 的所有功能，但经过了精炼，足以与旧的 SSLv3 协议兼容。然而，TLS 规范定义了当远端不支持 TLS 时，软件如何透明地回退到 SSLv3。因此，当我们谈论 SSL/TLS 时，指的是 TLS 协议及其在需要时自动回退到 SSLv3 的能力。

### SSL/TLS 身份验证

SSL/TLS 内置了对主机验证的支持。这种身份验证的实现确保了攻击者无法读取或操纵传输的数据，并确保端点是你预期的对象。这种身份验证不是强制性的，但显然是一个好主意。

为了让服务器或客户端通过身份验证，它必须具备两个要素：第一个是公钥/私钥对，即 RSA 或 DSA 密钥；第二个是证书，它是签名后的公 RSA 或 DSA 密钥。该证书本质上是一段数据，内容为：“我，签名者，承诺此密钥对属于所有者。”SSL/TLS 中使用的证书是 X.509 结构，对于我们的目的来说，你不需要了解它的具体含义。

在标准的 SSL/TLS 事务中，客户端会验证服务器的证书；然而，反过来可能并非。例如，HTTPS 事务很少要求客户端（网页浏览器）拥有证书进行身份验证。为了确保我们要求的是最高级别的安全性，我们将要求对服务器和客户端进行证书验证。然而，证书有多种签名方式，选择使用何种证书取决于我们。证书签名方法有两种：第三方证书和自签名证书。

### 第三方证书

最广泛使用的证书类型是：由管理员将其公钥由受信任的第三方签名的证书。这些第三方被称为证书颁发机构（CA）。

你的网页浏览器包含一个公共 CA 列表。当连接到网站时，会检查服务器提供的证书；如果服务器的公钥是由这些受信 CA 之一签名的，则允许连接。如果证书未由认可的 CA 正确签名，通常会弹出一个警告框，询问你是否仍然继续。
