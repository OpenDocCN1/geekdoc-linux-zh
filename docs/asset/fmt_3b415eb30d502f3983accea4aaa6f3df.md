
你需要防范哪些类型的错误？最糟糕的错误是将危险服务提供给世界，无论是无意的还是有意的。一个常见的错误是运行本地网络服务，这些服务泄漏到互联网上，并对其他产生影响。另一个是允许可疑的出站流量，例如端口扫描，而这些流量可能是由你的机器上的某人意外或故意产生的。默认拒绝一切的防火墙策略可以保护你免受许多这类错误。

## 端口扫描的问题

端口扫描本身并无害处。它们由网络分析工具生成。如今端口扫描的问题在于，它们通常由意图不善的人生成。他们“分析”的是你的网络，而不是他们自己的。不幸的是，这使得仅仅好奇的人也显得有罪。

默认拒绝一切的防火墙策略使你能够在防火墙后运行许多私人服务而无需承担过度的风险。这些服务必须被显式允许通过防火墙才能被远程主机访问。这种泛化是对现实的近似。虽然特权端口上的 TCP 服务对于所有熟练且坚定的黑客来说相对安全，但 UDP 服务本质上安全性较低，并且一些服务被分配到非特权端口。通常通过 UDP 运行的 RPC 服务更有问题。基于 RPC 的服务绑定到某个端口，一个非特权端口。`portmap`守护进程映射 RPC 服务号和实际端口号。端口扫描可以显示这些基于 RPC 的服务绑定在哪里，而无需通过`portmap`守护进程。幸运的是，`portmap`的使用越来越少，因此这不像几年前那样令人担忧。

一些服务，通常是局域网服务，通过官方注册的、众所周知的非特权端口提供。此外，一些服务，如 FTP 和 IRC，使用不适合数据包过滤的更多通信协议。以下部分中描述的规则使本地或远程客户端不合格发起连接到这些端口之一的连接。

FTP 是一个很好的例子，说明默认拒绝策略并不总是足以涵盖所有可能的情况。FTP 协议在本章后面介绍。目前，重要的想法是 FTP 允许在两个非特权端口之间建立连接。因为一些服务监听注册的非特权端口，并且因为到这些服务的入站连接请求源自非特权客户端，所以 FTP 允许的规则无意中允许了到这些本地服务的入站连接。这种情况也是防火墙规则在逻辑上是分层的且依赖于顺序的一个例子。显式保护运行在非特权端口上的私人本地服务的规则必须先于允许访问入口非特权端口范围的 FTP 规则。

因此，其中一些规则看起来是冗余的，对某些人来说是冗余的。对于运行服务的其他人来说，以下规则对于保护运行在本地非特权端口上的私人服务是必要的。

# 禁止连接到常见的 TCP 非特权服务器端口

到远程 X Window 服务器的连接应通过 SSH 建立，SSH 自动支持 X Window 连接。通过指定 `--syn` 标志，指示 SYN 位，仅阻止到服务器端口的连接建立。使用端口作为客户端端口发起的其他连接不受影响。

X Window 端口分配从第一个运行服务器的端口 6000 开始。如果运行额外的服务器，每个服务器都会被分配到递增的端口。作为一个小型站点，您可能只运行一个 X 服务器，您的服务器将只监听端口 6000。端口 6063 通常是最高的分配端口，允许在一台机器上运行 64 个独立的 X 窗口管理器，尽管有时也会看到 6255 和 6999 的范围：

```
XWINDOW_PORTS="6000:6063" # (TCP) X Window
```

第一条规则确保您的机器不发起任何到远程 X 窗口管理器的出站连接尝试：

```
# X Window 连接建立
$IPT -A OUTPUT -o $INTERNET -p tcp --syn \
    --destination-port $XWINDOW_PORTS -j REJECT
```

下一条规则阻止入站连接尝试到您的 X 窗口管理器。本地连接不受影响，因为本地连接是通过回环接口建立的：

```
# X Window：入站连接尝试
$IPT -A INPUT -i $INTERNET -p tcp --syn \
    --destination-port $XWINDOW_PORTS -j DROP
```

剩余的基于 TCP 的服务可以通过多端口匹配扩展用单条规则进行阻止。如果机器没有运行该服务，阻止入站连接并不是必需的，但从长远来看，如果您稍后决定在本地运行该服务，这样做更安全。

NFS 绑定到 UDP 端口 2049，但可以使用 TCP。你不应该在防火墙机器上运行 NFS，但如果正在运行，则拒绝外部访问。

不应允许连接到 OpenWindow 管理器。Linux 发行版不包含 OpenWindow 管理器。到端口 2000 的入站连接不需要阻止（当防火墙的 FORWARD 规则保护其他本地主机时，情况将有所不同，这将在后文提到）。

尝试连接到远程 SOCKS 服务器相当常见，且常涉及入侵利用。SOCKS 使用端口 1080。

`squid` 是一个 Web 缓存和代理服务器。`squid` 默认使用端口 3128，但可以配置为使用其他端口。

以下规则阻止本地客户端发起连接到远程 NFS 服务器、OpenWindow 管理器、SOCKS 代理服务器或 `squid` Web 缓存：

```
NFS_PORT="2049" # (TCP) NFS
SOCKS_PORT="1080" # (TCP) socks
OPENWINDS_PORT="2000" # (TCP) OpenWindows
SQUID_PORT="3128" # (TCP) squid

# 通过 TCP 建立到 NFS、OpenWindows、SOCKS 或
# squid 的连接
$IPT -A OUTPUT -o $INTERNET -p tcp \
  -m multiport --destination-port \
  $NFS_PORT,$OPENWINDS_PORT,$SOCKS_PORT,$SQUID_PORT \
  --syn -j REJECT
$IPT -A INPUT -i $INTERNET -p tcp \
  -m multiport --destination-port \
  $NFS_PORT,$OPENWINDS_PORT,$SOCKS_PORT,$SQUID_PORT \
  --syn -j DROP
```

## 分配到非特权端口的常见本地 UDP 服务

由于 TCP 的链接建立协议，TCP 协议规则可以比 UDP 协议规则处理得更精确。作为数据报服务，UDP 没有与之相关的连接状态。除非使用状态，否则对 UDP 服务的访问只能简单地被阻止。会为 DNS 和您可能使用的其他少数基于 UDP 的互联网服务做出明确的例外。幸运的是，常见的 UDP 互联网服务通常是客户端和特定服务器之间使用的类型。过滤规则通常允许与一个特定远程主机进行交换。

NFS 是需要关注的 UNIX UDP 服务，也是最常用的服务之一。NFS 运行在非特权端口 2049 上。与之前的基于 TCP 的服务不同，NFS 主要是基于 UDP 的服务。它可以配置为运行作为基于 TCP 的服务，但通常不这样做。

与 NFS 相关的是 NFS 的 RPC 锁守护进程 `lockd`。`lockd` 运行在 UDP 端口 4045 上：

```
NFS_PORT="2049" # NFS
LOCKD_PORT="4045" # RPC lockd for NFS

# NFS 和 lockd
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p udp \
    -m multiport --destination-port $NFS_PORT,$LOCKD_PORT \
    -m state --state NEW -j REJECT

  $IPT -A INPUT -i $INTERNET -p udp \
    -m multiport --destination-port $NFS_PORT,$LOCKD_PORT \
    -m state --state NEW -j DROP
else
  $IPT -A OUTPUT -o $INTERNET -p udp \
    -m multiport --destination-port $NFS_PORT,$LOCKD_PORT \
    -j REJECT
  $IPT -A INPUT -i $INTERNET -p udp \
    -m multiport --destination-port $NFS_PORT,$LOCKD_PORT \
    -j DROP
fi
```

# TCP 和 UDP 服务协议表

本章的其余部分致力于定义允许访问特定服务的规则。对于基于 TCP 和 UDP 的服务，客户端/服务器通信都涉及使用特定于该服务的协议进行某种双向通信。因此，访问规则始终表示为 I/O 对。客户端程序发出查询，服务器发送响应。给定服务的规则被归类为客户端规则或服务器规则。客户端类别表示本地客户端访问远程服务器所需的通信。服务器类别表示远程客户端访问由您的机器托管的服务所需的通信。

应用消息封装在 TCP 或 UDP 传输协议消息中。由于每种服务使用其特有的应用协议，TCP 或 UDP 交换的特定特征在某种程度上对于给定服务是独特的。
