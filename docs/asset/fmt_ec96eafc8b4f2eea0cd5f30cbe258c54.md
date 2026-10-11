
```
DHCP_SERVER="my.dhcp.server" # 如果您使用一个的话

# 初始化或重新绑定：没有租约或租约时间已过期。
$IPT -A OUTPUT -o $INTERNET -p udp \
  -s BROADCAST_SRC --port 68 \
  -d BROADCAST_DEST --dport 67 -j ACCEPT

# 来自可用 DHCP 服务器的传入 DHCP OFFER
$IPT -A INPUT -i $INTERNET -p udp \
  -s BROADCAST_SRC --port 67 \
  -d BROADCAST_DEST --dport 68 -j ACCEPT

# 回退到初始化
# 客户端知道其服务器，但已失去其租约，
# 或者在重启后需要重新确认 IP 地址。
$IPT -A OUTPUT -o $INTERNET -p udp \
  -s BROADCAST_SRC --port 68 \
  -d DHCP_SERVER --dport 67 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p udp \
  -s $DHCP_SERVER --port 67 \
  -d BROADCAST_DEST --dport 68 -j ACCEPT

# 结果，我们假设使用此消息更改您的 IP
# 地址，该消息旨在发给我们的新
# 地址，而 DHCP 客户端尚未收到更新。
# 根据服务器实现，目标地址
# 可以是新的 IP 地址、子网地址或有限
# 广播地址。

# 如果使用网络子网地址作为目标，
# 下一条规则必须允许发送目标的传入数据包
# 子网地址，并且该规则必须位于阻止包括广播数据包的任何一般规则之前。

# 租约更新
$IPT -A OUTPUT -o $INTERNET -p udp \
  -s $IPADDR --port 68 \
  -d $DHCP_SERVER --dport 67 -j ACCEPT
$IPT -A INPUT -i $INTERNET -p udp \
  -s $DHCP_SERVER --port 67 \
  -d $IPADDR --dport 68 -j ACCEPT
```

请注意，DHCP 流量无法完全限制到您的 DHCP 服务器。在初始化序列期间，当您的客户端尚未获得分配的 IP 地址甚至

## 启用通用 UDP 服务

... 服务器的 IP 地址，数据包是广播的，而不是点对点发送的。在第二层，数据包可能被寻址到你网卡的硬件地址。

### 7.6.3 访问远程网络时间服务器（UDP 端口 123）

网络时间服务如 NTP 允许访问一个或多个公共互联网时间提供者。这对维护准确的系统时钟很有用，特别是当你的内部时钟倾向于漂移时，以及用于在启动或断电后建立正确的时间和日期。小型系统用户应将该服务用作互联网客户端。很少有小型站点拥有到英国格林威治的卫星链路、到原子钟的无线电链路或自己的铯原子钟。

`ntpd` 是服务器守护进程。除了向客户端提供时间外，`ntpd` 还使用服务器之间的点对点关系。很少有小型站点需要 `ntpd` 提供的额外精度。`ntdate` 是客户端程序，并使用客户端到服务器的关系。客户端程序是小型站点所需的全部内容。表 7.16 列出了 NTP 服务的客户端/服务器交换协议。很少（如果有的话）有理由运行 `ntpd` 本身，因为那是服务器组件。如果你必须运行 NTP 服务器（而不是客户端），请在 root 环境中这样做。

#### 表 7.16 NTP 协议

| 描述 | 协议 | 远程地址 | 远程端口 | 入/出 | 本地地址 | 本地端口 |
|---|---|---|---|---|---|---|
| 本地客户端查询 | UDP | TIMESERVER | 123 | 出 | IPADDR | 1024:65535 |
| 远程服务器响应 | UDP | TIMESERVER | 123 | 入 | IPADDR | 1024:65535 |

在启动时运行的 `ntpd` 启动脚本使用 `ntdate` 查询一系列公共时间服务提供商。`ntpd` 守护进程在服务器回复后启动。这些主机将在一系列防火墙规则中单独指定：

```
TIME_SERVER="my.time.server" # 外部时间服务器，如果有
if [ "$CONNECTION_TRACKING" = "*" ]; then
$IPT -A OUTPUT -o $INTERNET -p udp \
    -s $IPADDR --sport $UNPRIVPORTS \
    -d $TIME_SERVER --dport 123 \
    -m state --state NEW -j ACCEPT
fi
$IPT -A OUTPUT -o $INTERNET -p udp \
    -s $IPADDR --sport $UNPRIVPORTS \
    -d $TIME_SERVER --dport 123 -j ACCEPT
$IPT -A INPUT -i $INTERNET -p udp \
    -s $TIME_SERVER --sport 123 \
    -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

请注意，上述规则是为标准的客户端/服务器 UDP 通信编写的。根据你的特定客户端和服务器软件，其中一个或两者都使用 NTP 服务器到服务器的通信模型，即客户端和服务器都使用 UDP 端口 123，这是可能的。

## 7.7 过滤 ICMP 控制状态消息

ICMP 消息是对许多错误条件的响应生成的，并由 `ping` 和 `traceroute` 等网络分析程序产生。

### ICMP 消息类型和 IPTABLES

`iptables` 支持使用 ICMP 数字消息类型或字母符号名称。`Iptables` 还支持使用消息子类型或代码。这对于对类型 3 目标不可达消息进行更细粒度的过滤控制特别有用。例如，你可以通过禁用传入的 `traceroute` 来明确禁止发出端口不可达消息，或者你可以明确只允许发出分片所需消息。

要查看 `iptables` 中所有支持的 ICMP 符号名称列表，请运行 `iptables -p icmp -h`。要查看官方 RFC 分配，请前往 http://www.iana.org/assignments/icmp-parameters。

### 7.7.1 错误状态和控制消息

四种 ICMP 控制状态消息需要通过防火墙：源抑制（Source Quench）、参数问题（Parameter Problem）、传入的目标不可达（Destination Unreachable）以及发出的分片所需（Fragmentation Needed）子类型的不可达消息。其他 ICMP 消息类型是可选的：回声请求（Echo Request）、回声回复（Echo Reply）、其他发出的目标不可达子类型，以及超时（Time Exceeded）。其他消息类型可以被忽略，或由默认策略过滤掉。

在可以或应该被忽略的消息类型中，重定向（redirect）是危险的，因为它在拒绝服务攻击中扮演重定向炸弹的角色。（有关重定向炸弹的更多信息，请参阅第 5 章。）除了重定向，剩余的 ICMP 消息类型是专门用于路由器之间控制和状态消息。

以下各节详细描述了与中间路由器相比，对端点主机重要的消息类型。

#### 分片的 ICMP 消息

在正常情况下，ICMP 消息永远不会被分片。ICMP 消息应该完全适应第二层帧。丢弃分片的 ICMP 消息是安全的。这样的数据包通常用于拒绝服务攻击：

```
$IPT -A INPUT -i $INTERNET --fragment -p icmp -j LOG \
--log-prefix "Fragmented ICMP: "
$IPT -A INPUT -i $INTERNET --fragment -p icmp -j DROP
```

#### 源抑制控制（类型 4）消息

当连接源（通常是路由器）发送数据的速度快于下一个目标路由器所能处理的速度时，可以发送 ICMP 消息类型 4，即源抑制（Source Quench）。源抑制在 IP 网络层用作一种原始形式的流量控制，通常位于两台相邻的点对点机器之间：

```
$IPT -A INPUT -i $INTERNET -p icmp \
--icmp-type source-quench -d $IPADDR -j ACCEPT
$IPT -A OUTPUT -o $INTERNET -p icmp \
-s $IPADDR --icmp-type source-quench -j ACCEPT
```

路由器的主机或目标机器发送源抑制命令。源路由器通过以较慢的速率发送数据包来响应，随着接收另一个源抑制消息，逐渐增加速率。

实际上，源抑制在互联网中已不再常用。流量控制留给高层协议。然而，在局域网中可以看到这种消息类型。

#### 参数问题状态（类型 12）消息

ICMP 消息类型 12，即参数问题（Parameter Problem），在接收到包含头部中非法或意外数据的数据包时，或当头部校验和不匹配接收机生成的校验和时发送：
