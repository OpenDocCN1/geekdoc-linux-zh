
`nmap` 命令包含一个 `-b` 标志以执行“FTP bounce”扫描：

```bash
nmap -b username:password@ftp.somecompanyasanexample.com:21 -p 4000-8000 target.somecompanyasanexample.com
```

> FTP 客户端在请求数据传输时可能使用被动模式，这将导致 FTP 客户端连接到 FTP 服务器上的端口以执行数据传输。然而，被动模式 FTP 有其自身的问题。被动模式 FTP 客户端可能容易受到“连接窃取”漏洞的影响。详情请参见第 4 章。

### TCP SYN/半开放

这种扫描类型导致扫描器向目标主机发送 SYN 数据包。如果目标主机正在监听特定端口，它将以 SYN+ACK 响应。如果目标主机存活但未监听特定端口，则将接收到 RST 数据包。由于这种扫描方法没有完成 TCP 三次握手，因此它是隐蔽的，因为目标主机通常不会记录此过程。

### SYN 扫描

在 `nmap` 中使用 `-sS` 标志将执行 SYN 扫描：

```bash
# nmap -sS 192.168.1.150

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )
Interesting ports on (192.168.1.150):
(The 1599 ports scanned but not shown below are in state: closed)

Port      State    Service
22/tcp    open     ssh
113/tcp   open     auth

Nmap run completed -- 1 IP address (1 host up) scanned in 2 seconds
```

### 源端口扫描

由于 FTP 协议的设计，当 FTP 客户端使用主动模式请求数据传输时，FTP 服务器必须发起连接回到 FTP 客户端上的端口。为了便于此操作，许多防火墙被配置为允许所有源端口设置为 20 的传入 IP 数据包。此外，来自 DNS 服务器的 IP 数据包的源端口设置为 53，因此许多防火墙允许所有源端口为 53 的传入数据包。使用 `-g` 开关可以指示 `nmap` 将其数据包的源端口设置为常量：

```bash
nmap -sS -g 20 192.168.1.1
```

## FIN

在此方法中，向目标主机发送一个 FIN 数据包。如果目标主机存活但未监听特定端口，它将以 RST 数据包响应。然而，如果目标主机正在监听特定端口，它不会响应。请注意，微软 Windows 主机在所有情况下都会发送 RST 数据包。这很有趣，因为它有助于识别目标主机为微软 Windows 主机。

> FIN IP 数据包用于终止已建立的 TCP 连接。

### FIN 扫描

在 `nmap` 中使用 `-sF` 标志将执行 FIN 扫描：

```bash
# nmap -sF 192.168.1.100

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )
Interesting ports on (192.168.1.100):
(The 1594 ports scanned but not shown below are in state: closed)

Port      State    Service
21/tcp    open     ftp
22/tcp    open     ssh
25/tcp    open     smtp
53/tcp    open     domain
80/tcp    open     http
110/tcp   open     pop-3
113/tcp   open     auth

Nmap run completed -- 1 IP address (1 host up) scanned in 43 seconds
```

## 反向 Ident

Ident（身份验证协议）服务器监听端口 113 上的连接。如果连接到运行 ident 服务器的主机上监听端口的 TCP 连接已建立，则可以查询 ident 服务器以获取与该连接相关进程的权限级别。

### 反向 Ident 扫描

在 `nmap` 中使用 `-I` 标志将执行 TCP 反向 ident 扫描：

```bash
# nmap -I -sT -p 80 192.168.1.100

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )
Interesting ports on (192.168.1.100):

| 端口 | 状态 | 服务 | 所有者 |
|:---|:---|:---|:---|
| 80/tcp | open | http | nobody |

Nmap run completed -- 1 IP address (1 host up) scanned in 1 second
```

## XMAS

这种扫描方法涉及发送一个设置了 FIN、URG 和 PUSH 标志的 TCP 数据包。如果目标主机正在监听特定端口，它会回传一个 RST 数据包。如果目标主机未监听该端口，它不会响应。

> FIN 数据包通常用于终止已建立的 TCP 连接。URG 数据包表示 IP 数据包内包含需要立即关注的信息，例如在 telnet 会话期间发送的 ^C。PUSH 数据包表示发送方请求接收方立即将所有缓冲数据传递给应用程序。

### XMAS 扫描

在 `nmap` 中使用 `-sX` 标志将执行 XMAS 扫描：

```bash
# nmap -sX 192.168.1.1

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )
Interesting ports on (192.168.1.1):
(The 1597 ports scanned but not shown below are in state: closed)

| 端口 | 状态 | 服务 |
|:---|:---|:---|
| 23/tcp | open | ssh |
| 80/tcp | open | http |
| 113/tcp | open | auth |
| 6000/tcp | open | X11 |

Nmap run completed -- 1 IP address (1 host up) scanned in 6 seconds
```

## 第 2 章：扫描与识别

### 空包扫描

这种类型的扫描涉及向目标主机发送一个 TCP 数据包，该数据包的 TCP 报头中所有标志位均被关闭（置为 0）。如果目标主机正在监听特定的端口，它将不会做出响应。否则，它将发送一个 RST 数据包。

在 `nmap` 中使用 `-sN` 标志可以执行 TCP 空包扫描：

```bash
[bash]$ nmap -sN 192.168.1.100
```

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )

Interesting ports on (192.168.1.100):

(The 1594 ports scanned but not shown below are in state: closed)

Port State Service

21/tcp open ftp

22/tcp open ssh

25/tcp open smtp

53/tcp open domain

80/tcp open http

110/tcp open pop-3

113/tcp open auth

Nmap run completed -- 1 IP address (1 host up) scanned in 41 seconds

### RPC 扫描

这种类型的扫描用于向开放端口发送 NULL 命令，以确定它们是否为 RPC（远程过程调用）端口。一旦确定某个开放端口是 RPC 端口，就会查询并获取绑定到该端口的应用程序信息。

在 `nmap` 中使用 `-sR` 选项可以执行 RPC 扫描：

```bash
[bash]$ nmap -sR 10.0.0.10
```

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )

Interesting ports on (10.0.0.10):

(The 1584 ports scanned but not shown below are in state: closed)

Port State Service (RPC)

7/tcp open echo

21/tcp open ftp

22/tcp open ssh

37/tcp open time

53/tcp open domain

111/tcp open sunrpc (rpcbind V2-4)

113/tcp open auth

512/tcp open exec

513/tcp open login

514/tcp open shell
