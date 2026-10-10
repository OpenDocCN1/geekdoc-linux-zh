
**eth1** 上的内部接口地址将为 **192.168.1.65**，通向边界 DMZ 网络。Choke 防火墙机器的外部接口地址在其 **eth0** 上将为 **192.168.1.126**，通向边界 DMZ 网络。Choke 防火墙机器的内部接口地址在 **eth1** 上将为 **192.168.1.129**，通向专用局域网（LAN）。

分配给 DMZ 主机的地址空间为 **192.168.1.66** 到 **192.168.1.125**，因为 DMZ 位于 **192.168.1.64/26** 网络中。广播地址为 **192.168.1.127**。在 **192.168.1.128** 网络范围内，分配给局域网主机的地址空间为 **192.168.1.130** 到 **192.168.1.190**。广播地址为 **192.168.1.191**。

## 表 6.4
C 类网络 **192.168.1.0** 划分为四个子网

| 属性 | 子网 0 | 子网 1 | 子网 2 | 子网 3 |
| :--- | :--- | :--- | :--- | :--- |
| **接口** | 网关外部 | 网关 DMZ | Choke DMZ | Choke LAN |
| **网络地址** | 192.168.1.0 | 192.168.1.64 | 192.168.1.128 | 192.168.1.192 |
| **子网掩码** | 255.255.255.192 | 255.255.255.192 | 255.255.255.192 | 255.255.255.192 |
| **IP 地址** | 192.168.1.1 | 192.168.1.65 | 192.168.1.126 | 192.168.1.129 |
| **首个可用主机地址** | N/A | 192.168.1.66 | 192.168.1.130 | 192.168.1.193 |
| **末个可用主机地址** | N/A | 192.168.1.125 | 192.168.1.190 | 192.168.1.254 |
| **广播地址** | 192.168.1.63 | 192.168.1.127 | 192.168.1.191 | 192.168.1.255 |
| **总主机数** | 62 | 62 | 62 | 62 |

### 公共网关防火墙的附加常量

以下常量被添加到网关防火墙脚本中，用于引用网关的内部接口、Choke 的 IP 地址以及 DMZ 的网络地址块：

```bash
DMZ_INTERFACE="eth1"       # 通向 DMZ 的网络接口
DMZ_IPADDRESS="192.168.1.65"    # DMZ IP 地址
CHOKE_IPADDRESS="192.168.1.126" # Choke 防火墙 DMZ 地址
DMZ_ADDRESSES="192.168.1.64/26" # DMZ IP 地址范围
DMZ_BROADCAST="192.168.1.127"   # DMZ 广播地址
LAN_ADDRESSES="192.168.1.128/26"  # 局域网 IP 地址范围
LOCAL_ADDRESSES="192.168.1.0/24"  # 任何本地 IP 地址
```

### 私有 Choke 防火墙的常量

如果在防火墙 shell 脚本中针对重复出现的名称和地址使用符号常量，脚本将更易于阅读和维护。以下常量要么在本章的示例中全程使用，要么是网络标准中定义的通用常量：

```bash
DMZ_INTERFACE="eth0"          # 通向 DMZ 的网络接口
LAN_INTERFACE="eth1"          # 通向局域网的网络接口
LOOPBACK_INTERFACE="lo"        # 依据系统命名而定

DMZ_IPADDR="192.168.1.126"       # DMZ IP 地址
GATEWAY_IPADDR="192.168.1.65"     # 网关防火墙 – 路由器
DMZ_ADDRESSES="192.168.1.64/26"   # DMZ IP 地址范围
DMZ_NETWORK="192.168.1.64"        # DMZ 子网基地址
DMZ_BROADCAST="192.168.1.127"     # DMZ 广播地址
LAN_IPADDR="192.168.1.129"        # 局域网 IP 地址
LAN_ADDRESSES="192.168.1.128/26"  # 局域网 IP 地址范围
LAN_NETWORK="192.168.1.128"        # 局域网子网基地址
LAN_BROADCAST="192.168.1.191"      # 局域网广播地址

LOOPBACK="127.0.0.0/8"         # 保留的环回地址范围
CLASS_A="10.0.0.0/8"          # A 类私有网络
CLASS_B="172.16.0.0/12"       # B 类私有网络
CLASS_C="192.168.0.0/16"      # C 类私有网络
CLASS_D_MULTICAST="224.0.0.0/4" # D 类组播地址
CLASS_E_RESERVED_NET="240.0.0.0/5" # E 类保留地址
BROADCAST_SRC="0.0.0.0"        # 广播源地址
BROADCAST_DEST="255.255.255.255" # 广播目标地址
PRIVPORTS="0:1023"            # 知名、特权
                               # 端口范围
UNPRIVPORTS="1024:65535"      # 非特权端口范围
```

此处未列出的常量在它们所使用的特定规则上下文中定义。

### 对 Choke 防火墙进行宽松设置

以下步骤与第 4 章中的步骤完全相同。Choke 防火墙的引语部分与网关的相同：

```bash
# 启用广播回声保护
echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts

# 禁用源路由数据包
for f in /proc/sys/net/ipv4/conf/*/accept_source_route; do
    echo 0 > $f
done

# 启用 TCP SYN Cookie 保护
echo 1 > /proc/sys/net/ipv4/tcp_syncookies

# 禁用 ICMP 重定向接受
for f in /proc/sys/net/ipv4/conf/*/accept_redirects; do
    echo 0 > $f
done

# 不发送重定向消息
for f in /proc/sys/net/ipv4/conf/*/send_redirects; do
    echo 0 > $f
done

# 丢弃从接口进入的欺骗数据包，如果对这些数据包进行回复，
# 回复将从不同的接口发出。
for f in /proc/sys/net/ipv4/conf/*/rp_filter; do
    echo 1 > $f
done

# 记录具有不可能地址的数据包。
for f in /proc/sys/net/ipv4/conf/*/log_martians; do
    echo 1 > $f
done
```

### 从 Choke 防火墙中删除任何现有的规则

在定义一组过滤规则时，首先要做的是从规则链中删除任何现有规则。否则，您定义的任何新规则都将被添加到现有规则之后。数据包很容易在到达您从此处开始定义链中的那个点之前匹配到一个预先存在的规则。以下命令一次性冲洗所有三个内置过滤表链——INPUT、OUTPUT 和 FORWARD——的规则。（用户定义的链也会被冲洗，但本章中没有使用。）这与前面章节中构建的网关防火墙中的相同：

```bash
# 冲洗所有链中的任何现有规则
$IPT --flush
$IPT -t nat --flush
$IPT -t mangle --flush
$IPT -X
$IPT -t nat -X
$IPT -t mangle -X
```

链现在是空的。您是从零开始的。如果系统刚刚启动，则系统处于默认的接受一切策略状态。如果正在重新初始化防火墙，则默认策略是先前设置的那些。冲洗规则不会影响默认策略。

### 定义 Choke 防火墙的默认策略

Choke 策略是拒绝双向的所有流量。为了返回 ICMP 3 错误消息，必须使用 **REJECT** 目标。最简单的方法是以通用的 **REJECT** 规则结束链，以捕获任何未匹配 **ACCEPT** 规则的内容。这导致立即提供有意义的错误消息，而不是迫使本地主机等待超时。请注意，这与网关防火墙不同，网关防火墙的默认策略是使用 **DROP** 静默丢弃流量。

为了创建一个已知良好的环境，以便可以使用防火墙脚本来停止防火墙，第一个默认策略是 **ACCEPT**。这与前面章节中看到的策略设置相同：

```bash
$IPT --policy INPUT ACCEPT
$IPT --policy OUTPUT ACCEPT
$IPT --policy FORWARD ACCEPT
$IPT -t nat --policy PREROUTING ACCEPT
$IPT -t nat --policy OUTPUT ACCEPT
$IPT -t nat --policy POSTROUTING ACCEPT
$IPT -t mangle --policy PREROUTING ACCEPT
$IPT -t mangle --policy OUTPUT ACCEPT
```

接下来，添加创建停止动作的位。同样，这些与前面章节中相同：

```bash
if [ "$1" = "stop" ]
then
	echo "防火墙已完全停止！警告：此主机没有正在运行的防火墙。"
	exit 0
fi
```

两个防火墙默认都丢弃或拒绝一切，而不是默认接受一切：

```bash
# 将 Choke 防火墙的默认策略设置为拒绝
$IPT --policy INPUT REJECT
$IPT --policy OUTPUT REJECT
$IPT --policy FORWARD REJECT
```

此时，所有网络流量都被阻塞。

### 启用 Choke 机器的环回接口

您需要启用不受限制的环回流量。这使您能够运行任何您选择的本地网络服务，或系统依赖的服务，而无需担心指定所有防火墙规则：

```bash
# 在环回接口上无限制流量
$IPT -A INPUT  -i $LOOPBACK_INTERFACE -j ACCEPT
$IPT -A OUTPUT -o $LOOPBACK_INTERFACE -j ACCEPT
```

### 隐蔽扫描和 TCP 状态标志

由于 iptables 提供对所有 TCP 状态标志的访问，因此可以测试常见的 TCP 隐蔽扫描形式。以下规则阻止常见的隐蔽扫描探测。测试的任何 TCP 状态组合都不是合法组合。

由于以下输入和转发规则中未匹配特定接口，因此这些规则适用于所有接口。同样，代码与网关防火墙相同：

```bash
# 所有位都被清除
$IPT -A INPUT    -p tcp --tcp-flags ALL NONE -j DROP
$IPT -A FORWARD -p tcp --tcp-flags ALL NONE -j DROP

# SYN 和 FIN 都被设置
$IPT -A INPUT    -p tcp --tcp-flags SYN,FIN SYN,FIN -j DROP
$IPT -A FORWARD -p tcp --tcp-flags SYN,FIN SYN,FIN -j DROP

# SYN 和 RST 都被设置
$IPT -A INPUT    -p tcp --tcp-flags SYN,RST SYN,RST -j DROP
$IPT -A FORWARD -p tcp --tcp-flags SYN,RST SYN,RST -j DROP

# FIN 和 RST 都被设置
$IPT -A INPUT    -p tcp --tcp-flags FIN,RST FIN,RST -j DROP
$IPT -A FORWARD -p tcp --tcp-flags FIN,RST FIN,RST -j DROP

# FIN 是唯一的位，没有预期的伴随 ACK
$IPT -A INPUT    -p tcp --tcp-flags ACK,FIN FIN -j DROP
$IPT -A FORWARD -p tcp --tcp-flags ACK,FIN FIN -j DROP

# PSH 是唯一的位，没有预期的伴随 ACK
$IPT -A INPUT    -p tcp --tcp-flags ACK,PSH PSH -j DROP
$IPT -A FORWARD -p tcp --tcp-flags ACK,PSH PSH -j DROP

# URG 是唯一的位，没有预期的伴随 ACK
$IPT -A INPUT    -p tcp --tcp-flags ACK,URG URG -j DROP
$IPT -A FORWARD -p tcp --tcp-flags ACK,URG URG -j DROP
```
