
$IPT -A EXT-input -p icmp -icmp-in

$IPT -A EXT-output -p icmp -icmp-out

################################################################

# ICMP 流量
## 记录并丢弃 ICMP 分片

$IPT -A EXT-in -fragment -j LOG --log-prefix "incoming ICMP:"

$IPT -A EXT-out -fragment -j LOG --log-prefix "outgoing ICMP:"

## 出站 ping

if [ "$CONNECTION_TRACKING" = "1" ]; then

  $IPT -A EXT-out -p icmp \
  --icmp-type echo-request \
  -m state --state NEW \
  -j ACCEPT

fi

$IPT -A EXT-out -p icmp \
  --icmp-type echo-request \
  -j ACCEPT

$IPT -A EXT-in -p icmp \
  --icmp-type echo-reply \
  -j ACCEPT

## 入站 ping

if [ "$CONNECTION_TRACKING" = "1" ]; then

  $IPT -A EXT-in -p icmp \
  -s $MY_ISP \
  --icmp-type echo-request \
  -m state --state NEW \
  -j ACCEPT

fi

$IPT -A EXT-in -p icmp \
  -s $MY_ISP \
  --icmp-type echo-request \
  -j ACCEPT

$IPT -A EXT-out -p icmp \
  -d $MY_ISP \
  --icmp-type echo-reply \
  -j ACCEPT

## 目标不可达类型 3

$IPT -A EXT-out -p icmp \
  --icmp-type fragmentation-needed \
  -j ACCEPT

$IPT -A EXT-in -p icmp \
  --icmp-type destination-unreachable \
  -j ACCEPT

## 参数问题

$IPT -A EXT-out -p icmp \
  --icmp-type parameter-problem \
  -j ACCEPT

$IPT -A EXT-in -p icmp \
  --icmp-type parameter-problem \
  -j ACCEPT

################################################################

# TCP 状态标志
## 所有位都已清除

```
$IPT -A tcp-state-flags -p tcp --tcp-flags ALL NONE -j log-tcp-state
```

# 第 6 章 341 优化 iptables 防火墙

## 同时设置了 SYN 和 FIN

```
# 同时设置了 SYN 和 FIN
$IPT -A tcp-state-flags -p tcp --tcp-flags SYN,FIN,FIN -j log-tcp-state
```

## 同时设置了 SYN 和 RST

```
# 同时设置了 SYN 和 RST
$IPT -A tcp-state-flags -p tcp --tcp-flags SYN,RST,RST -j log-tcp-state
```

## 同时设置了 FIN 和 RST

```
# 同时设置了 FIN 和 RST
$IPT -A tcp-state-flags -p tcp --tcp-flags FIN,RST,RST -j log-tcp-state
```

## 仅设置了 FIN 位，且伴随预期的 ACK

```
# 仅设置了 FIN 位，且伴随预期的 ACK
$IPT -A tcp-state-flags -p tcp --tcp-flags ACK,FIN -j log-tcp-state
```

## 仅设置了 PSH 位，且伴随预期的 ACK

```
# 仅设置了 PSH 位，且伴随预期的 ACK
$IPT -A tcp-state-flags -p tcp --tcp-flags ACK,PSH,PSH -j log-tcp-state
```

## 仅设置了 URG 位，且伴随预期的 ACK

```
# 仅设置了 URG 位，且伴随预期的 ACK
$IPT -A tcp-state-flags -p tcp --tcp-flags ACK,URG,URG -j log-tcp-state
```

################################
## 记录并丢弃状态组合错误的 TCP 数据包

```
$IPT -A log-state -p tcp -j LOG \
  --log-prefix "Illegal TCP state: " \
  --log-options --log-tcp-state
```

```
$IPT -A log-tcp-state -j DROP
```

################################################
## 对 ESTABLISHED 状态的交换跳过规则检查

```
if [ "CONNECTION_TRACKING" = "1" ]; then
  # 对已建立的交换跳过防火墙过滤器 -m state \
  $IPT -A connection-tracking -m state \
  --state ESTABLISHED,RELATED \
  -j ACCEPT
```

```
$IPT -A connection-tracking -m state --state INVALID \
  -j LOG --log-prefix "INVALID packet: "
$IPT -A connection-tracking -m state --state INVALID -j LOG
```

```
fi
```

################################################
## DHCP 流量
有些广播包被防火墙显式忽略。
# 其他的被默认策略丢弃。
# DHCP 测试必须在广播相关的规则之前，因为 DHCP
# 初期依赖于广播流量。

```
if [ "DHCP_CLIENT" = "1" ]; then
```

## 初始化或重新绑定：无租约或租约过期。

```
$IPT -A local-dhcp-client-query \
  -s $BROADCAST_SRC \
  -d $BROADCAST_DEST -j ACCEPT
```

## 来自可用 DHCP 服务器的入站 DHCPPOFFER

# 342 附录 B 防火墙示例和支持脚本

```
$IPT -A remote-dhcp-server-response \
  -s BROADCAST_SRC \
  -d BROADCAST_DEST -j ACCEPT
```

## 回退初始化
# 客户端知道其服务器，但丢失了租约，
# 或者在重启后需要重新确认 IP 地址。

```
$IPT -A local-dhcp-client-query \
  -s $BROADCAST_SRC \
  -d DHCP_SERVER -j ACCEPT
```

```
$IPT -A remote-dhcp-server-response \
  -s DHCP_SERVER \
  -d BROADCAST_DEST -j ACCEPT
```

## 由于上述结果，我们应该通过此消息更改 IP
# 地址，该消息在 dhcp 客户端接收到更新之前
# 发往我们的新地址。
# 取决服务器的实现，目标地址
# 可以是新的 IP 地址、子网地址或受限地址。

## 如果使用子网地址作为目标，
# 则下一条规则必须允许指向
# 子网地址的数据包，且该规则必须在
# 包含广播包的规则之前。

```
$IPT -A remote-dhcp-server-response \
  -s DHCP_SERVER -j ACCEPT
```

## 租约更新

```
$IPT -A local-dhcp-client-query \
  -s IPADDR \
  -d DHCP_SERVER -j ACCEPT
```

```
fi
```

################################################

# 源地址伪装检查

## 丢弃来自接收接口的数据包

$IPT -A source-address-check -s IPADDR -j DROP

## 拒绝声称来自私有网络的数据包
