
```bash
# Flush all the rules out of all three default chains
iptables -F INPUT
iptables -F OUTPUT
iptables -F FORWARD

# Set the default policy for the FORWARD chain to deny all
iptables -P FORWARD deny

# Block all incoming traffic coming from public interface (eth0)
iptables -A INPUT -i eth0 -j DROP

# Block all outgoing traffic going out the public interface (eth0)
iptables -A OUTPUT -o eth0 -j DROP

# Instruct Netfilter to accept fragmented packets (-f)
iptables -A FORWARD -f -j ACCEPT

# Accept incoming TCP packets from established connections
# (-state ESTABLISHED,RELATED)
iptables -A FORWARD -m state -p tcp --state ESTABLISHED,RELATED -j ACCEPT

# Accept incoming TCP connections to SSH arriving at eth0
iptables -A FORWARD -p tcp -i eth0 -d 208.209.210.0/24 --dport ssh -j ACCEPT

# Accept incoming TCP connections to SSH arriving at eth0
iptables -A FORWARD -p tcp -i eth0 -d 208.209.210.0/24 --dport ssh -j ACCEPT

# Accept incoming TCP connections to DMZ SMTP server (64.65.66.3)
iptables -A FORWARD -p tcp -i eth0 -d 64.65.66.3 --dport smtp -j ACCEPT

# Accept incoming TCP connections to Web server from remote branch only
iptables -A FORWARD -p tcp -i eth0 -s 128.129.130.0/24 -d 64.65.66.2 -dport:www -j ACCEPT

# Accept all outgoing TCP connections received via both eth1 and eth2
# (the private and the DMZ interfaces respectively)
iptables -A FORWARD -p tcp -i eth1,eth2 -j ACCEPT

# Accept all outgoing UDP connections received via both eth1 and eth2
# (the private and the DMZ interfaces respectively)
iptables -A FORWARD -p udp -i eth1,eth2 -j ACCEPT

# Accept incoming ICMP packet of `echo reply` (`0`) type (ping replies)
iptables -A FORWARD -p icmp -i eth0 -d 208.209.210.0/24 --icmp-type 0 -j ACCEPT
iptables -A FORWARD -p icmp -i eth0 -d 64.65.66.0/24 --icmp-type 0 -j ACCEPT

# Accept all outgoing ICMP connections received from either the
# private interface (eth1) or the DMZ interface (eth2)
iptables -A FORWARD -p icmp -i eth1, eth2 -j ACCEPT

# Drop all other traffic in the FORWARD chain
iptables -A FORWARD -j DROP
```

在列表 9.4 中，你只是向前向链添加了两条规则，一条允许所有到邮件服务器（`64.65.66.3`）的 SMTP 流量，另一条允许来自 `128.129.130.0/24` 的源流量连接到 DMZ Web 服务器（`64.65.66.2`）的 80 端口。注意，你还必须允许 ICMP 响应进入 `eth0` 并定向到 DMZ，并通过 DMZ 接口 `eth2` 退出。

### 防范已知攻击

除了对内部主机实施访问控制的能力外，`Netfilter` 和 `iptables` 还可以用于通过过滤与攻击指纹匹配的数据包来防范特定类型的 Internet 攻击。本节描述了用于解决这些已知漏洞的若干示例 `iptables` 语句。

#### 地址欺骗

许多防火墙配置允许在验证数据包头部的源字段中包含来自专用网络的地址后转发该数据包。问题在于，攻击者很容易合成一个“欺骗”数据包，该数据包生成自他们的网络但携带你的源地址。通过使用 `iptables` 命令（如下所示）要求来自本地网络的源地址的数据包必须从连接到本地网络的接口接收，从而保护你的站点免受地址欺骗：

```bash
iptables -A FORWARD -s internal_network -i public_interface -j DROP
```

此命令向前向链添加了一条规则，该规则匹配源自内部网络但通过公共接口进入系统的流量。通过添加此命令，你强制 `Netfilter` 丢弃到达你防火墙公共接口的欺骗数据包。

例如，考虑之前在图 9.4 中描绘的双宿主防火墙架构，其中本地网络是 `208.209.210.0/24`，路由器的公共接口是 `157.35.66.65`。该防火墙的地址欺骗规则如下所示：

```bash
iptables -A FORWARD -s 208.209.210.0/24 -i eth0 -j DROP
```

此规则检查到达公共接口（`eth0`）的数据包，如果它们携带（专用）`208.209.210.0/24` 网络中的源地址，则静默丢弃它们。

#### 碎片攻击（Smurf Attack）

`smurf` 攻击是通过向内部网络的广播地址发送 ICMP 回显请求（`ping`）数据包来实施的。数据包的源被伪造为 `smurf` 攻击目标地址，该目标会被所有内部主机的 ICMP 回显响应淹没。

以下 `iptables` 命令应通过阻止伪造的 ICMP 回显请求进入你的网络来防范 `smurf` 攻击：

```bash
iptables -A FORWARD -p icmp -d internal_network_broadcast_address -j DROP
```

此命令向前向链添加了一条规则，该规则匹配进入防火墙任何接口的、目的地为你的内部 LAN 广播地址的任何 ICMP 数据包。当匹配到此规则时，数据包执行 `DROP` 动作。例如，在之前图 9.4 中描绘的网络中，你将使用以下命令：

```bash
iptables -A FORWARD -p icmp -i eth0 -d 208.209.210.255 -j DROP
```

在这种情况下，你正在寻找目的地为 `208.209.210.255`（即 `208.209.210.0/24` 网络的广播地址）的 ICMP 流量。

#### Syn-Flood 攻击

`syn-flood` 攻击是通过向主机发送大量 TCP 连接请求（设置 `SYN` 标志）并抑制正常的 `SYN-ACK` 响应来实施的，从而试图消耗其所有可用的数据结构，而这些结构正忙于跟踪这些半打开的连接。

使用 `limit` 外部匹配模块，你可以使用以下 `iptables` 命令将 TCP `SYN` 请求的接受速率限制为每秒一次：

```bash
iptables -A FORWARD -p tcp --syn -m limit --limit 1/s -j ACCEPT
```

每秒一个 TCP `SYN` 请求的速率对于大多数 Internet 服务器来说是可接受的，但它限制入站 `SYN` 请求的发生次数足够多，以确保你的系统始终有足够的可用资源来处理合法连接。

#### 端口扫描攻击

许多端口扫描应用程序试图通过向给定的端口范围发送 `SYN` 或 `FIN` 信号并期望对未激活的端口收到 `RST` 信号来识别你系统中所有开放的 TCP 和 UDP 端口。你可以使用以下 `iptables` 命令将此活动限制为每秒一次：
