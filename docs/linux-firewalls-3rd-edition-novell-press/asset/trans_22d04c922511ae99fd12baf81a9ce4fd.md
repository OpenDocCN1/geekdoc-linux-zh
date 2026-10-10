
## ICMP 流量

最后，最后一对规则匹配入站和出站的 ICMP 流量：

```
# ICMP traffic
$IPT -A EXT--input -p icmp -j EXT-icmp-in
$IPT -A EXT--output -p icmp -j EXT-icmp-out
EXT-icmp-in AND EXT-icmp-out,
```

这两条用户自定义链 **EXT-icmp-in** 和 **EXT-icmp-out** 对本地主机与远程机器之间交换的 ICMP 数据包进行最终判定。

**EXT-icmp-in** 链基于消息类型选择入站的 ICMP 数据包。**EXT-icmp-out** 链基于消息类型选择出站的 ICMP 数据包：

```
# Log and drop initial ICMP fragments
$IPT -A EXT-icmp-in --fragment -j LOG \
--log-prefix "Fragmented incoming ICMP: "
$IPT -A EXT-icmp-in --fragment -j DROP
$IPT -A EXT-icmp-out --fragment -j LOG \
--log-prefix "Fragmented outgoing ICMP: "
$IPT -A EXT-icmp-out --fragment -j DROP
```

```
# Outgoing ping
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A EXT-icmp-out -p icmp \
--icmp-type echo-request \
-m state --state NEW \
-j ACCEPT
fi

$IPT -A EXT-icmp-out -p icmp \
--icmp-type echo-request -j ACCEPT

$IPT -A EXT-icmp-in -p icmp \
--icmp-type echo-reply -j ACCEPT
```

```
# Incoming ping
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A EXT-icmp-in -p icmp \
-s $MY_ISP \
--icmp-type echo-request \
-m state --state NEW \
-j ACCEPT
fi
```

```
$IPT -A EXT-icmp-in -p icmp \
--icmp-type echo-request \
-s $MY_ISP -j ACCEPT
```

```
$IPT -A EXT-icmp-out -p icmp \
--icmp-type echo-reply \
-d $MY_ISP -j ACCEPT
```

```
# Destination Unreachable Type 3
$IPT -A EXT-icmp-out -p icmp \
--icmp-type fragmentation-needed -j ACCEPT
```

```
$IPT -A EXT-icmp-in -p icmp \
--icmp-type destination-unreachable -j ACCEPT
```

```
# Parameter Problem
$IPT -A EXT-icmp-out -p icmp \
--icmp-type parameter-problem -j ACCEPT
```

```
$IPT -A EXT-icmp-in -p icmp \
--icmp-type parameter-problem -j ACCEPT
```

```
# Time Exceeded
$IPT -A EXT-icmp-in -p icmp \
--icmp-type time-exceeded -j ACCEPT
```

```
# Source Quench
$IPT -A EXT-icmp-out -p icmp \
--icmp-type source-quench -j ACCEPT
```

```
$IPT -A EXT-icmp-in -p icmp \
--icmp-type source-quench -j ACCEPT
```

## tcp-state-flags

**tcp-state-flags** 链是您将附加到内置 INPUT 和 OUTPUT 链上的第一个用户自定义链。测试匹配那些人为构造的 TCP 状态标志组合，这些组合常用于隐蔽扫描：

```
# All of the bits are cleared
$IPT -A tcp-state-flags -p tcp --tcp-flags ALL NONE -j log-tcp-state

# SYN and FIN are both set
$IPT -A tcp-state-flags -p tcp --tcp-flags SYN,FIN SYN,FIN -j log-tcp-state

# SYN and RST are both set
$IPT -A tcp-state-flags -p tcp --tcp-flags SYN,RST SYN,RST -j log-tcp-state

# FIN and RST are both set
$IPT -A tcp-state-flags -p tcp --tcp-flags FIN,RST FIN,RST -j log-tcp-state

# FIN is the only bit set, without the expected accompanying ACK
$IPT -A tcp-state-flags -p tcp --tcp-flags ACK,FIN FIN -j log-tcp-state

# PSH is the only bit set, without the expected accompanying ACK
$IPT -A tcp-state-flags -p tcp --tcp-flags ACK,PSH PSH -j log-tcp-state

# URG is the only bit set, without the expected accompanying ACK
$IPT -A tcp-state-flags -p tcp --tcp-flags ACK,URG URG -j log-tcp-state
```

## log-tcp-state

log-tcp-state 链有两个用途。首先，日志消息带有特定的解释性前缀，并且由于这是一个构造的数据包，任何 IP 或 TCP 选项都会被报告。其次，匹配的数据包会被立即丢弃。后面提到的两条通用日志记录链是在如下假设下编写的：被记录的数据包在从这些链返回时会立即被默认策略丢弃：

```
$IPT -A log-tcp-state -p tcp -j LOG \
    --log-prefix 'Illegal TCP state: ' \
    --log-ip-options --log-tcp-options

$IPT -A log-tcp-state -j DROP
```

## connection-tracking

connection-tracking 链是您将附加到内置 INPUT 和 OUTPUT 链上的第二个用户自定义链。匹配的数据包将绕过防火墙规则并被立即接受：

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
    # Bypass the firewall filters for established exchanges
    $IPT -A connection-tracking -m state \
        --state ESTABLISHED,RELATED \
        -j ACCEPT

    $IPT -A connection-tracking -m state --state INVALID \
        -j LOG --log-prefix "INVALID packet: "
    $IPT -A connection-tracking -m state --state INVALID -j DROP
fi
```

## local_dhcp_client_query 和 remote_dhcp_server_response

`local_dhcp_client_query` 和 `remote_dhcp_server_response` 链包含了 DHCP 客户端所需的规则。这些规则在链层级中的位置对于任何欺骗或通用广播规则而言至关重要。此外，主机在从服务器接收 DHCPOACK 确认消息之前不会配置其 IP 地址。服务器在 DHCPOACK 消息中使用的目标地址取决于特定的服务器实现。如果您想使用此规则，您需要将 `DHCP_CLIENT` 设置为 `1` 并定义 `DHCP_SERVER` 变量：

```
# Some broadcast packets are explicitly ignored by the firewall.
# Others are dropped by the default policy.
# DHCP tests must precede broadcast-related rules, as DHCP relies
# on broadcast traffic initially.
if [ "${DHCP_CLIENT}" = "1" ]; then
    DHCP_SERVER="my.dhcp.server"

    # Initialization or re-binding: No lease or Lease time expired.
    $IPT -A local-dhcp-client-query \
    -s $BROADCAST_SRC \
    -d $BROADCAST_DEST -j ACCEPT

    # Incoming DHCPPOFFER from available DHCP servers
    $IPT -A remote-dhcp-server-response \
    -s $BROADCAST_SRC \
    -d $BROADCAST_DEST -j ACCEPT

    # Fall back to initialization
    # The client knows its server, but has either lost its lease,
    # or else needs to reconfirm the IP address after rebooting.
    $IPT -A local-dhcp-client-query \
    -s $BROADCAST_SRC \
    -d ${DHCP_SERVER} -j ACCEPT

    $IPT -A remote-dhcp-server-response \
    -s $DHCP_SERVER \
    -d $BROADCAST_DEST -j ACCEPT

    # As a result of the above, we're supposed to change our IP
    # address with this message, which is addressed to our new
    # address before the dhcp client has received the update.
    # Depending on the server implementation, the destination address
    # can be the new IP address, the subnet address, or the limited
    # broadcast address.

    # If the network subnet address is used as the destination,
    # the next rule must allow incoming packets destined to the
    # subnet address, and the rule must precede any general rules
    # that block such incoming broadcast packets.
    $IPT -A remote-dhcp-server-response \
    -s $DHCP_SERVER -j ACCEPT

    # Lease renewal
    $IPT -A local-dhcp-client-query \
    -s $IPADDR \
    -d $DHCP_SERVER -j ACCEPT

fi
```

## source-address-check

source-address-check 链测试明显非法的源地址。该链仅附加到 INPUT 链。防火墙规则保证由该主机生成的数据包包含您的 IP 地址作为其源地址。请注意，如果主机拥有多个网络接口，或者私有局域网正在使用私有类别 IP 地址，这些规则需要进行一些调整。

DHCP 客户端在执行这些测试之前需要处理与 DHCP 相关的广播流量：

```
# Drop packets pretending to be originating from the receiving interface
$IPT -A source-address-check -s $IPADDR -j DROP

# Refuse packets claiming to be from private networks
$IPT -A source-address-check -s $CLASS_A -j DROP
$IPT -A source-address-check -s $CLASS_B -j DROP
$IPT -A source-address-check -s $CLASS_C -j DROP
$IPT -A source-address-check -s $CLASS_D_MULTICAST -j DROP
$IPT -A source-address-check -s $CLASS_E_RESERVED_NET -j DROP
$IPT -A source-address-check -s $LOOPBACK -j DROP
$IPT -A source-address-check -s 0.0.0.0/8 -j DROP
$IPT -A source-address-check -s 169.254.0.0/16 -j DROP
$IPT -A source-address-check -s 192.0.2.0/24 -j DROP
```

## destination-address-check

destination-address-check 链测试广播数据包、误用的多播地址以及知名的非特权服务端口。该链附加到 INPUT 和 OUTPUT 链两者。DHCP 客户端在执行这些测试之前需要处理与 DHCP 相关的广播流量：

```
# Block directed broadcasts from the Internet
$IPT -A destination-address-check $BROADCAST_DEST -j DROP
$IPT -A destination-address-check -d $SUBNET_BASE -j DROP
$IPT -A destination-address-check -d $SUBNET_BROADCAST -j DROP
$IPT -A destination-address-check -p udp \
   -d $CLASS_D_MULTICAST -j DROP

# Avoid ports subject to protocol and system administration problems

# TCP unprivileged ports
# Deny connection requests to NFS, SOCKS and X Window ports
$IPT -A destination-address-check -p tcp -m multiport \
   --destination-port $NFS_PORT,$OPENWINDOWS_PORT,$SOCKS_PORT,$QUID_PORT \
   --syn -j DROP

$IPT -A destination-address-check -p tcp --syn \
   --destination-port $XWINDOW_PORTS -j DROP

# UDP unprivileged ports
# Deny connection requests to NFS and lockd ports
$IPT -A destination-address-check -p udp -m multiport \
   --destination-port $NFS_PORT,$LOCKD_PORT -j DROP
```

## 记录被丢弃的数据包

EXT-log-in 和 EXT-log-out 链包含了记录数据包立即在数据包落入各自链的末尾并被默认策略丢弃之前的规则。几乎所有被丢弃的出站数据包都会被记录，因为它们要么表明防火墙规则存在问题，要么表明有未知（或未授权的服务）试图联系外部世界：
