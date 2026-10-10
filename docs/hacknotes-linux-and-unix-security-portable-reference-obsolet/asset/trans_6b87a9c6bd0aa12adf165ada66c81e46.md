

# 反向标识

标识（Identification Protocol）服务器在端口 113 上监听连接。如果与运行标识服务器的某主机上正在监听的端口建立了 TCP 连接，标识服务器可能会收到针对与该连接关联的进程的特权级别的查询请求。

# 反向标识扫描

在 `nmap` 中使用 `-I` 标志将执行 TCP 反向标识扫描：

```bash
$ nmap -I -sT -p 80 192.168.1.100
```

启动 `nmap` V. 3.00 ( www.insecure.org/nmap/ )
(192.168.1.100) 上的相关端口：

| 端口 | 状态 | 服务 | 拥有者 |
| :--- | :--- | :--- | :--- |
| 80/tcp | 开放 | http | 无用户 |

Nmap 运行完成 -- 扫描 1 个 IP 地址（1 台主机在线），耗时 1 秒

# XMAS

这种扫描方法涉及发送一个设置了 FIN、URG 和 PUSH 标志的 TCP 数据包。如果目标主机正在监听特定端口，它会返回一个 RST 数据包。如果目标主机没有监听该端口，则不响应。

> FIN 数据包通常用于断开已建立的 TCP 连接。URG 数据包表示 IP 数据包中存在需要立即处理的信息，例如在 telnet 会话期间发送的 ^C。PUSH 数据包表示发送方请求接收方立即将所有缓冲数据传递给应用程序。

# XMAS 扫描

在 `nmap` 中使用 `-sX` 标志将执行 XMAS 扫描：

```bash
$ nmap -sX 192.168.1.1
```

启动 `nmap` V. 3.00 ( www.insecure.org/nmap/ )
(192.168.1.1) 上的相关端口：
（以下未显示的 1597 个已扫描端口处于关闭状态）

| 端口 | 状态 | 服务 |
| :--- | :--- | :--- |
| 22/tcp | 开放 | ssh |
| 80/tcp | 开放 | http |
| 113/tcp | 开放 | auth |
| 6000/tcp | 开放 | X11 |

Nmap 运行完成 -- 扫描 1 个 IP 地址（1 台主机在线），耗时 6 秒

## NULL

这种扫描类型涉及向目标主机发送一个 TCP 数据包，其中 TCP 头部中的所有标志均被关闭。如果目标主机正在监听特定端口，它将不响应。否则，它将发送一个 RST 数据包。

## NULL 扫描

在 `nmap` 中使用 `-sN` 标志将执行 TCP NULL 扫描：

```bash
$ nmap -sN 192.168.1.100
```

启动 `nmap` V. 3.00 ( www.insecure.org/nmap/ )
(192.168.1.100) 上的相关端口：
（以下未显示的 1594 个已扫描端口处于关闭状态）

| 端口 | 状态 | 服务 |
| :--- | :--- | :--- |
| 21/tcp | 开放 | ftp |
| 22/tcp | 开放 | ssh |
| 25/tcp | 开放 | smtp |
| 53/tcp | 开放 | domain |
| 80/tcp | 开放 | http |
| 110/tcp | 开放 | pop-3 |
| 113/tcp | 开放 | auth |

Nmap 运行完成 -- 扫描 1 个 IP 地址（1 台主机在线），耗时 41 秒

## RPC

这种扫描类型用于向开放端口发送 NULL 命令，以确定它们是否为 RPC（远程过程调用）端口。一旦确定开放端口为 RPC 端口，就会查询并获取绑定到该端口的应用程序信息。

## RPC 扫描

在 `nmap` 中使用 `-sR` 选项将执行 RPC 扫描：

```bash
$ nmap -sR 10.0.0.10
```

启动 `nmap` V. 3.00 ( www.insecure.org/nmap/ )
(10.0.0.10) 上的相关端口：
（以下未显示的 1584 个已扫描端口处于关闭状态）

| 端口 | 状态 | 服务 (RPC) |
| :--- | :--- | :--- |
| 7/tcp | 开放 | echo |
| 21/tcp | 开放 | ftp |
| 22/tcp | 开放 | ssh |
| 37/tcp | 开放 | time |
| 53/tcp | 开放 | domain |
| 111/tcp | 开放 | sunrpc (rpcbind V2-4) |
| 113/tcp | 开放 | auth |
| 512/tcp | 开放 | exec |
| 513/tcp | 开放 | login |
| 514/tcp | 开放 | shell |
| 515/tcp | 开放 | printer |
| 587/tcp | 开放 | submission |
| 2049/tcp | 开放 | nfs (nfs V2-3) |
| 4045/tcp | 开放 | lockd (nfs V2-3) |
| 7100/tcp | 开放 | font-service |
| 32771/tcp | 开放 | sometimes-rpc5 (ypserv V1-2) |
| 32772/tcp | 开放 | sometimes-rpc7 |

Nmap 运行完成 -- 扫描 1 个 IP 地址（1 台主机在线），耗时 40 秒

## IP 协议

这种扫描类型的目的是确定目标主机支持哪些 IP 协议。它发送指向特定协议的原始 IP 数据包，如果收到 ICMP 协议不可达消息，则该特定协议很可能在目标主机上不受支持。

### IP 协议扫描

在 `nmap` 中使用 `-sO` 标志将执行 IP 协议扫描：

```bash
$ nmap -sO 192.168.1.1
```

启动 `nmap` V. 3.00 ( www.insecure.org/nmap/ )
(192.168.1.1) 上的相关协议：
（以下未显示的 251 个已扫描协议处于关闭状态）

| 协议 | 状态 | 名称 |
| :--- | :--- | :--- |
| 1 | 开放 | icmp |
| 2 | 开放 | igmp |
| 6 | 开放 | tcp |
| 17 | 开放 | udp |

## ACK

这种扫描类型主要用于确定防火墙规则集。向目标主机发送 ACK 数据包。如果目标主机不响应或返回 ICMP 不可达数据包，则端口很可能被防火墙过滤。如果目标主机返回 RST 数据包，则端口未被防火墙过滤。

### ACK 扫描

可以通过使用带有 `-sA` 标志的 `nmap` 来执行 ACK 扫描：

```bash
nmap -sA target_address
```

## 窗口

这种扫描类型虽然类似于 ACK 扫描，但由于某些系统在报告 TCP 窗口大小时存在异常，有时有助于检测某些系统上的开放、已过滤和未过滤端口。

### 窗口扫描

潜在入侵者可以使用带有 `-sW` 标志的 `nmap` 来执行窗口扫描：

```bash
nmap -sW target_address
```

## UDP

为了确定某主机是否正在监听特定的 UDP 端口，会向该端口发送一个 UDP 数据包。如果目标主机没有监听该特定端口，则会收到 ICMP 端口不可达数据包。然而，如果目标主机正在监听该特定端口，则不会收到此类数据包。由于 UDP 不是面向连接的协议，因此 UDP 扫描不可靠。

### UDP 端口扫描

在 `nmap` 中使用 `-sU` 选项将执行 UDP 扫描：

```bash
$ nmap -sU 192.168.1.100

Starting Nmap 7.54BETA31 ( https://nmap.org/ )
Interesting ports on (192.168.1.100):
(The 1454 ports scanned but not shown below are in state: closed)
PORT      STATE         SERVICE
53/udp    open          domain
```

### 防御端口扫描

你可以使用以下方法来反击针对你网络的扫描：

- 配置防火墙以丢弃发往已关闭端口的数据包。这将减慢针对你网络的扫描速度，因为这会导致端口扫描应用程序在超时值超过后重新发送 SYN 数据包。只有在多次超时后，端口扫描应用程序才会假定端口已过滤，并继续扫描下一组端口。
- 大多数防火墙和入侵检测系统（IDSS）具有检测端口扫描的能力。利用此功能，并定期检查你的日志。
- 配置防火墙不要信任源端口值。状态防火墙具有功能，仅允许来自已知建立连接的 FTP 服务器的源端口 20 的数据包。无论如何，不建议使用 FTP 等明文协议。存在更好的替代方案（如 SSH），应使用这些替代方案。此外，除非数据包发往需要执行区域传输的你的 DNS 服务器，否则不要允许源端口设置为 53 的传入 TCP 数据包。通过授权为你主机提供服务的 DNS 服务器的 IP 地址来限制 DNS 流量。
- 大多数 FTP 服务器不允许客户端发出带有除客户端外其他主机 IP 地址的 PORT 命令。这将防止 FTP 弹射扫描。有关详细信息，请查阅你的 FTP 服务器文档和配置。
- 配置防火墙以丢弃或重置针对标识端口（113）的连接尝试。
- 使用状态防火墙。这将阻止上述文本中提到的大多数扫描。

## 指纹识别

尽管许多操作系统设计者尽最大努力遵循相关 RFC，但操作系统内核作者有时会以不同的方式解释细节。Xprobe2 和 Nmap 等工具会探测这些差异，以识别目标操作系统的指纹。

### 使用 Xprobe2 对操作系统进行指纹识别

Xprobe2 使用 ICMP 数据包执行指纹识别。结果根据对目标操作系统最佳猜想的评分进行排序。该工具能够区分通往目的地的路径上的过滤设备，可在此处获取：http://www.sys-security.com/html/tools/tools.html。

以下是使用 Xprobe2 的示例：

```bash
# xprobe2 -v target.somecompanyasanexample.com

Xprobe2 v.0.1 Copyright (c) 2002 Fygrave@tigerteam.net,
ofir@sys-security.com

[+] Target is target.somecompanyasanexample.com
[+] Loading modules.
[+] Following modules are loaded:
    [x]ICMP echo (ping)
    [x]TTL distance
    [x]ICMP echo
```

