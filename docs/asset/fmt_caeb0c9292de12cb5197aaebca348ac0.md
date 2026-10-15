
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

然后，你将设置规则以允许系统内部（`localhost`）发送和接收的所有数据包通过：

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

要允许防火墙访问外部网络，你允许所有数据包的输入，除了 ICMP 数据包。这些稍后处理。防火墙由防火墙设备 `eth0` 指定。首先，允许已建立和相关的连接继续：

```
# allow outside communication to the firewall,
# except for ICMP packets
iptables -A INPUT -m state --state ESTABLISHED,RELATED \
-i eth0 -p ! icmp -j ACCEPT
```

## 阻止外部发起的连接（Blocking Outside Initiated Access）

为了防止外部人员发起对系统的任何访问，创建一个规则以使用 `state` 选项中的 `NEW` 阻止来自外部的 SYN 数据包访问。丢弃 `eth0` 连接上的任何新连接（假设只有 `eth0` 连接到互联网或外部网络）。

```
iptables -A INPUT -m state --state NEW -i eth0 -j DROP
iptables -A FORWARD -m state --state NEW -i eth0 -j DROP
```

## 本地网络访问

要允许内部网络与防火墙进行交互，你允许在内部以太网连接 `eth1` 上的所有数据包输入。有效的内部网络地址被指定为输入源：

```
iptables -A INPUT -j ACCEPT -p all -i eth1 -s 192.168.0.0/24
```

## 伪装本地网络

为了实现伪装，使私有网络上的系统可以使用网关的 Internet 地址连接到 Internet 主机，你创建一个 `NAT` 表 (`-t nat`) `POSTROUTING` 规则，使用 `MASQUERADE` 目标：

```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

## 控制 ICMP 数据包

此外，为了允许 `ping` 和目标可达 ICMP 数据包，你输入以防火墙为目的地的 `INPUT` 规则。为了启用 `ping` 操作，你同时使用 `echo-reply` 和 `echo-request` ICMP 类型，对于目标不可达，你使用 `destination-unreachable` 类型：

```
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type \
echo-reply -d 10.0.0.1
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type \
echo-request -d 10.0.0.1
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type \
destination-unreachable -d 10.0.0.1
```

最后，IP 转发再次打开：

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

## 列出规则

列出这些 `iptables` 选项会显示每个选项的不同规则，如下所示：
