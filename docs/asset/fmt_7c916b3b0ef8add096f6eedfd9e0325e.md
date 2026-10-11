
链是空的。你从零开始。系统处于默认状态。

## 定义瓶颈的默认策略

瓶颈的默认策略是拒绝所有方向的流量。瓶颈防火墙的默认策略是拒绝所有流量。瓶颈的默认策略是除非显式允许，否则拒绝所有流量。

```
# 设置默认策略
ipchains -P input
ipchains -P output
ipchains -P forward
```

## 启用瓶颈的回环接口

瓶颈的默认策略是拒绝所有流量。你需要允许回环流量，否则系统将无法正常工作。

```
# 允许回环流量
ipchains -A input -i $LOOPBACK -j ACCEPT
ipchains -A output -i $LOOPBACK -j ACCEPT
```

## 源欺和其他

防火墙的默认策略是拒绝所有流量。以下规则拒绝声称来自内部网络或DMZ的数据包。

```
# 拒绝伪造的IP地址
ipchains -A input -i $CHOKE_DMZ_INTERFACE -s $BASTION_DMZ_IPADDR -j REJECT
ipchains -A output -i $CHOKE_LAN_INTERFACE -s $BASTION_DMZ_IPADDR -j REJECT

ipchains -A input -i $CHOKE_LAN_INTERFACE -s $CHOKE_DMZ_IPADDR -j REJECT
ipchains -A output -i $CHOKE_DMZ_INTERFACE -s $CHOKE_DMZ_IPADDR -j REJECT
```

以下规则还防止数据包被声称来自其进入的接口。

```
# 拒绝伪造的网络地址
ipchains -A input -i $CHOKE_DMZ_INTERFACE -s $DMZ_ADDRESSES -j REJECT
ipchains -A output -i $CHOKE_LAN_INTERFACE -s $DMZ_ADDRESSES -j REJECT

ipchains -A input -i $CHOKE_LAN_INTERFACE -s $DMZ_ADDRESSES -j REJECT
ipchains -A output -i $CHOKE_DMZ_INTERFACE -s $DMZ_ADDRESSES -j REJECT
```

本节的后续规则将拒绝并记录自称来自 E 类预留网络的数据包：

```bash
# 拒绝预留的 IP 地址
ipchains -A input -i CHOKE_DMZ_INTERFACE -s RESERSEVED_NET -j REJECT -1
ipchains -A input -i CHOKE_LAN_INTERFACE -s RESERSEVED_NET -j REJECT -1
```

## 过滤 ICMP 控制和状态消息

启用 IP 伪装（`masquerading`）时，ICMP 消息的处理方式有所不同。除非在内核编译时启用了通用 IP 伪装，否则只有 ICMP 错误消息会为现有连接转发并伪装，例如 `ping` 和 `traceroute` 使用的消息。如果也启用了 ICMP 伪装，其他控制消息可以从内部的伪装机器发送到互联网。否则，这些 ICMP 消息可以在同一网络上的本地主机之间发送。Red Hat release 6.0 默认启用 ICMP 伪装。在较早的版本中，必须显式地编译进内核。

在通用伪装的情况下，如果启用了 ICMP 伪装，你的本地机器可以与外部机器发起 ICMP 交互，但外部机器不能向你的任何本地机器发起 ICMP 消息。只有堡垒机（bastion machine）的外部接口是直接可见的。

## 源抑制（类型 4）消息

当连接源（通常是路由器）发送数据的速度快于下一个路由的处理能力时，会发送 ICMP 消息类型 4，源抑制（Source Quench）。源抑制被用作 IP 网络层的一种原始流量控制形式，通常用于两个相邻的点对点机器之间。

## 源抑制控制 DMZ 配置

接受所有源抑制消息的堡垒规则为：

```bash
ipchains -A output -i BASTION_DMZ_INTERFACE -p icmp \
-s BASTION_DMZ_IPADDR 4 -d DMZ_ADDRESSES -j ACCEPT
```

```bash
ipchains -A input -i BASTION_DMZ_INTERFACE -p icmp \
-s DMZ_ADDRESSES 4 -d BASTION_DMZ_IPADDR -j ACCEPT
```

## 阻塞抑制（Choke Quench）控制 DMZ 配置

接受所有源抑制消息的阻塞规则为：

```bash
ipchains -A output -i CHOKE_DMZ_INTERFACE -p icmp \
-s DMZ_ADDRESSES 4 -d CHOKE_DMZ_IPADDR -j ACCEPT
```

```bash
ipchains -A input -i CHOKE_DMZ_INTERFACE -p icmp \
-s CHOKE_DMZ_IPADDR 4 -d DMZ_ADDRESSES -j ACCEPT
```

## 形式化子网防火墙 153

## 参数问题（类型 12）消息

ICMP 消息类型 12，参数问题（Parameter Problem），当接收到的数据包头部包含非法或意外数据时，或者当头部校验和与接收机器生成的校验和不匹配时，会被发送。

## 堡垒参数状态 DMZ 配置

接受所有参数问题消息的堡垒规则为：

```bash
ipchains -A output -i BASTION_DMZ_INTERFACE -p icmp \
-s ANYWHERE 12 -d DMZ_ADDRESSES -j ACCEPT
```

```bash
ipchains -A input -i BASTION_DMZ_INTERFACE -p icmp \
-s DMZ_ADDRESSES 12 -d ANYWHERE -j ACCEPT
```

## 阻塞参数问题状态 DMZ 配置

接受所有参数问题消息的阻塞规则为：

```bash
ipchains -A input -i CHOKE_DMZ_INTERFACE -p icmp \
-s ANYWHERE 12 -d CHOKE_DMZ_IPADDR -j ACCEPT
```

```bash
ipchains -A output -i CHOKE_DMZ_INTERFACE -p icmp \
-s CHOKE_DMZ_IPADDR 12 -d ANYWHERE -j ACCEPT
```

## 目的不可达错误（类型 3）

ICMP消息类型 3，目的不可达（Destination Unreachable），是一种通用错误消息。

## 堡垒目的不可达错误 DMZ 配置

接受所有目的不可达消息的堡垒规则为：

```bash
ipchains -A output -i BASTION_DMZ_INTERFACE -p icmp \
-s ANYWHERE 3 -d DMZ_ADDRESSES -j ACCEPT
```

```bash
ipchains -A input -i CHOKE_DMZ_INTERFACE -p icmp \
-s DMZ_ADDRESSES 3 -d ANYWHERE -j ACCEPT
```

## 阻塞目的不可达错误 DMZ 配置

接受所有目的不可达消息的阻塞规则为：

```bash
ipchains -A input -i CHOKE_DMZ_INTERFACE -p icmp \
-s ANYWHERE 3 -d CHOKE_DMZ_IPADDR -j ACCEPT
```

```bash
ipchains -A output -i CHOKE_DMZ_INTERFACE -p icmp \
-s CHOKE_DMZ_IPADDR 3 -d ANYWHERE -j ACCEPT
```

## 超时状态（类型 11）消息

ICMP消息类型 11，超时（Time Exceeded），表示超时情况，或者更准确地说，超过了数据包的最大跳数。在第4章 LAN 问题、多防火墙和边界网络中，入站超时消息通常被视为对输出 `traceroute` 请求的 ICMP 响应。

## 堡垒超时状态 DMZ 配置

仅通过阻塞防火墙接受超时消息的堡垒规则为：

```bash
ipchains -A output -i BASTION_DMZ_INTERFACE -p icmp \
-s BASTION_DMZ_IPADDR 11 -d DMZ_ADDRESSES -j ACCEPT
```

```bash
ipchains -A input -i BASTION_DMZ_INTERFACE -p icmp \
-s DMZ_ADDRESSES 11 -d BASTION_DMZ_IPADDR -j ACCEPT
```

## 阻塞超时状态 DMZ 配置

仅通过堡垒防火墙接受超时消息的阻塞规则为：
