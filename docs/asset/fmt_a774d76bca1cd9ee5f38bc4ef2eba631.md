
```
iptables -N incoming
iptables -A incoming -j DROP eth0 -s 192.168.0.45
iptables -A incoming -j ACCEPT -i lo
iptables -A FORWARD -j incoming
iptables -A INPUT -j incoming
```

## 第 2 部分：安全

| 选项 | 功能 |
| --- | --- |
| `-p [!] proto` | 指定协议，例如 TCP、UDP、ICMP 或 ALL |
| `-s [!] address[mask] [!] [port[:port]]` | 匹配的源地址。带有端口参数，你可以指定端口。 |
| `--sport [!] [port[:port]]` | 源端口指定。你可以使用冒号 `port:port` 指定一个端口范围。 |
| `-d [!] address[mask] [!] [port[:port]]` | 匹配的目的地址。带有端口参数，你可以指定端口。 |
| `--dport [!] [port[:port]]` | 目的端口指定。 |
| `--icmp-type [!] typename` | 使用名称指定输入网络接口（例如 `eth0`）。`+` 号充通配符。附加在名称末尾的 `+` 匹配所有具有该前缀的接口（`eth+` 匹配所有以太网接口）。只能用于 `INPUT` 链。 |
| `-i [!] name+` | 使用名称指定输入网络接口（例如 `eth0`）。只能用于 |
| `-j target [port]` | 指定规则的目标（对于 `REDIRECT` 目标指定 `[port]`）。 |
| `--to-source <ipaddr> [-< ipaddr>]: port-port` | 与 `SNAT` 目标配合，使用新的源 IP 地址重写数据包。 |
| `--to-destination <ipaddr> [-< ipaddr>]: port-port` | 与 `DNAT` 目标配合，使用新的目的 IP 地址重写数据包。 |
| `-n` | 地址和端口的数字输出，配合 `-L` 使用。 |
| `-c [!] name+` | 使用名称指定输出网络接口（例如 `eth0`）。只能用于 `FORWARD` 和 `OUTPUT` 链。 |
| `-t table` | 指定使用的表，在 `-t nat` 中用于 NAT 表。 |
| `-v` | 详细模式，显示规则详情，配合 `-L` 使用。 |
| `-x` | 扩展数字（显示精确值），配合 `-L` 使用。 |
| `[!] -f` | 匹配分片的数据包。 |
| `[!] -V` | 打印包版本。 |
| `!` | 否定选项或地址 |
| `-m` | 指定使用的模块，例如 `state`。 |
| `--state` | 指定状态，如 `NEW`、`RELATED` 和 `ESTABLISHED`。用于检测包的状态。 |
| `-p ACCEPT` | 指定协议...作为状态。引用 SYN 包（新连接）。 |
| `--syn` | SYN 包，新连接。 |
| `--tcp-flags` | TCP 标志：SYN, ACK, FIN, URG, PS 以及所有标志。 |
| `--limit` | `limit` 模块的选项（`-m limit`）。用于控制每秒匹配的次数。 |
| `--limit-burst` | 指定限制生效前的最大突发次数。用于控制拒绝服务攻击。 |

## 表 5：IPTables 选项

| 序号 | 名称 | 所需 |
| --- | --- | --- |
| 0 | echo-reply | ping |
| 3 | destination-unreachable | 任意 TCP/UDP 流量 |
| 5 | redirect | 如果未运行进程 |
| 8 | echo-request | ping |
| 11 | time-exceeded | traceroute |

## ICMP

防火墙经常阻塞 Internet 控制协议 `ICMP` 消息，这些消息可以控制你的路由路径。在大多数情况下，你需要允许这些数据包；一些常见的 ICMP 包类型列在表 14-6 中。你可以使用 `--icmp-type` 选项启用 ICMP 类型，该选项接受数字或名称。以下示例启用了 `echo-reply`、`echo-request` 和 `destination-unreachable` 消息，它们的数字分别为 0、8和3。

```
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type echo-reply -d 10.0.1
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type echo-request
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type destination-unreachable -d 10.0.1
```

你的规则列表如下：

```
ACCEPT icmp -- 0.0.0.0/0 10.0.1 type 0
ACCEPT icmp -- 0.0.0.0/0 10.0.1 type 8
ACCEPT icmp -- 0.0.0.0/0 10.0.1 type 3
```

Ping 操作需要进一步控制以避免“死亡 ping”（ping-of-death）威胁。你可以通过几种方法实现。一种是拒绝任何分片的 Ping 包。Ping 包通常很小。使用 `-f` 选项指示分片。

```
iptables -A INPUT -p icmp -j DROP -f
```

另一种方法是限制接收到的 Ping 包数量。使用 `limit` 模块控制 ICMP ping 操作的匹配次数。使用 `-m limit` 和 `--limit` 指定允许的匹配次数。1/s 表示每秒允许一次。

```
iptables -A FORWARD -p icmp --icmp-type echo-request -m limit --limit 1/s -j ACCEPT
```

## 表 14-6：常见 ICMP 包

## 控制端口访问

如果你的系统托管 Internet 服务（如 FTP 服务器），你可以使用 IPTables 控制它的访问。你可以通过使用服务使用的源端口（`--sport`）或目的端口（`--dport`）来指定特定服务。IPTables 允许端口使用名称，例如 Web 服务器端口使用 `www`。服务的名称及其使用的端口列在 `/etc/services` 文件中，将端口映射到特定服务。对于域名服务器，端口为 `domain`。如果你愿意，也可以使用端口号，在数字前加冒号。以下示例接受除位于 192.168.0.43 的 Web 服务器以外的所有流量：

```
iptables -A INPUT -d 192.168.0.43 --dport www -j ACCEPT
```

你可以使用端口引用保护某些服务并拒绝其他服务。这种方法通常用于对 Internet 更开放的防火墙，允许用户使用 Internet 连接。已知有害的服务（如 Telnet 和 NTP）可以被拒绝。例如，要拒绝防火墙上的任何 Telnet 操作，你可以丢弃进入 Telnet 端口 23 的包。为了保护 NFS 操作，你可以拒绝访问 portmapper 端口 111。你可以使用端口号或端口名称。

```
# 拒绝防火墙上对 portmapper 的外部访问。
iptables -A INPUT -j DROP -p tcp -i eth0 --dport 111
# 拒绝防火墙上对 telnet 端口的外部访问。
iptables -A INPUT -j DROP -p tcp -i eth0 --dport telnet
```

规则列表如下：

```
DROP tcp 0.0.0.0/0 0.0.0.0/0 tcp dport:111
DROP tcp 0.0.0.0/0 0.0.0.0/0 tcp dport:23
```

一个端口相关的安全问题是你的 X 服务器端口，范围从 6000 到 6009。在相对开放的防火墙上，这些端口可能被用于通过 X 服务器 非法访问你的系统。端口范围可以使用冒号指定，例如 6000:6009。你可以

## 第 14 章：防火墙

第一部分也使用 x11，即 x11:609。X 服务器上的会话可以使用 SSH 进行加密，通常通过端口 6010 访问 X 服务器。

```
iptables -A INPUT -j DROP -p tcp -i eth0 --dport 6000:6009
```

这里显示了常见的检查端口及其标签：

| 服务 | 端口号 | 端口标签 |
|---|---|---|
| Auth | 113 | auth |
| Finger | 79 | finger |
| FTP | 21 | ftp |
| NTP | 123 | ntp |
| Portmapper | 111 | sunrpc |
