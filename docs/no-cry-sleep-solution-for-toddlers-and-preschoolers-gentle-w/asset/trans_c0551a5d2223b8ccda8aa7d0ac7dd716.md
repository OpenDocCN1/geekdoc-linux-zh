

![](img/6c226e8ba1efd427dec3bf582418d33f_378_0.png)

## FIGURE 19-2 Firewall rules applied to a local network example

最初，在脚本中你会使用 flush 选项 (-F) 清空当前的 iptables，然后为非用户定义的规则设置策略（默认目标）。在设置链规则时，IP 转发也应关闭：

```
echo 0 > /proc/sys/net/ipv4/ip_forward
```

## Drop Policy

首先，为 INPUT 和 FORWARD 内置 IP 链设置 DROP 策略。这意味着如果数据包不符合任何允许其通过的规则中的条件，它将被丢弃。然后拒绝所有 IP 欺骗攻击以及任何从外部发起连接的尝试（SYN 数据包）。外部连接尝试也会被记录下来。这是一个非常基础的配置，可以通过添加 iptables 规则轻松根据自己的需求进行完善。

```
iptables -P INPUT DROP
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT
```

## IP Spoofing

保护私有网络免受 IP 欺骗的一种方法是检查专门用于私有网络的以太网设备上的任何外部地址。在此示例中，任何在设备 eth1（专用于私有网络）上且源地址不是私有网络的包（即 -s 192.168.0.0）将被拒绝。还要检查是否有任何来自外部的数据包将私有网络指定为其源地址。在此示例中，任何源地址为私有网络但在私有网络以外的任何以太网设备（eth1）上的数据包将被拒绝。相同的策略也可以应用于本地主机。

```
# IP spoofing, deny any packets on the internal network
# that has an external source address.
iptables -A INPUT -j LOG -i eth1 \! -s 192.168.0.0/24
iptables -A INPUT -j DROP -i eth1 \! -s 192.168.0.0/24
iptables -A FORWARD -j DROP -i eth1 \! -s 192.168.0.0/24
# IP spoofing, deny any outside packets (any not on eth1)
# that have the source address of the internal network
iptables -A INPUT -j DROP \! -i eth1 -s 192.168.0.0/24
iptables -A FORWARD -j DROP \! -i eth1 -s 192.168.0.0/24
# IP spoofing, deny any outside packets with localhost address
# (packets not on the lo interface (any on eth0 or eth1))
# that have the source address of localhost
iptables -A INPUT -j DROP -i ! lo -s 127.0.0.0/255.0.0.0
iptables -A FORWARD -j DROP -i ! lo -s 127.0.0.0/255.0.0.0
```

然后，你将设置规则以允许系统内部（localhost）发送和接收的所有数据包通过：

```
iptables -A INPUT -j ACCEPT -i lo
```

## Server Access

对于 Web 服务器，你希望允许外部用户访问，但阻止任何试图从 Web 服务器向私有网络发起连接的访问。在下一个示例中，所有发送到 Web 服务器的消息都被接受，但 Web 服务器无法与私有网络发起联系。这可以防止任何人通过对外部开放的 Web 服务器侵入本地网络。已建立的连接是允许的，允许私有网络使用 Web 服务器。

```
# allow communication to the Web server (address 10.0.0.2), port www
iptables -A INPUT -j ACCEPT -p tcp -i eth0 --dport www -s 10.0.0.2
# Allow established connections from Web servers to internal network
iptables -A INPUT -m state --state ESTABLISHED,RELATED -i eth0 \
-p tcp --sport www -s 10.0.0.2 -d 192.168.0.0/24 -j ACCEPT
# Prevent new connections from Web servers to internal network
iptables -A OUTPUT -m state --state NEW -o eth0 -p tcp \
--sport www -d 192.168.0.1/24 -j DROP
```

## Firewall Outside Access

要允许防火墙访问外部网络，你允许所有数据包的输入，除了 ICMP 数据包。这些稍后处理。防火墙由防火墙设备 eth0 指定。首先，允许已建立和相关的连接继续：

```
# allow outside communication to the firewall,
# except for ICMP packets
iptables -A INPUT -m state --state ESTABLISHED,RELATED \
-i eth0 -p ! icmp -j ACCEPT
```

## Blocking Outside Initiated Access

为了防止外部人员发起对系统的任何访问，创建一个规则以使用 state 选项中的 NEW 阻止来自外部的 SYN 数据包访问。丢弃 eth0 连接上的任何新连接（假设只有 eth0 连接到互联网或外部网络）。

