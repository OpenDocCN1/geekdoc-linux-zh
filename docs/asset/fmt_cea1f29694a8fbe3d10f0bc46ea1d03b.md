
您现在有了足够的信息来创建一个简单的 `iptables` 脚本，为连接到互联网的单个系统提供基本保护。以下脚本提供了 IP tables 过滤过程，以保护本地网络和网站免受外部攻击。它为私有网络配置了一个简单的防火墙（查看 `iptables` HOWTO 可获取更复杂的示例）。如果您有本地网络，可以对此脚本进行适配。在此项配置中，所有来自外部的远程访问都被阻止，但用户在网络中与外部系统使用的连接允许双向通信。在本例中，防火墙系统的私有网络地址为 `192.168.0.0`（见图 35-1）。为了本例，互联网地址为 `10.0.0.1`。该系统有两个以太网设备：一个用于私有网络 `eth1`，另一个用于互联网 `eth0`。网关防火墙系统还支持地址为 `10.0.0.2` 的 Web 服务器。示例中由于过长无法放在单行的条目将延续在第二行，并换行符用反斜杠引用。

应用于网络不同部分的基本规则如图所示：

首先，为 `INPUT` 和 `FORWARD` 内置 IP 链设置了 `DROP` 策略。这意味着如果数据包不符合任何规则中允许通过的准则，它将被丢弃。

![](img/0160c5015efa6b5e7fe8c8f2b89e33c1_888_0.png)

图 35-1 带有防火墙的网络

## 864 红帽 Linux：完整参考

![](img/0160c5015efa6b5e7fe8c8f2b89e33c1_889_0.png)

图 35-2. 应用于本地网络示例的防火墙规则

```
mylfilter
# 防火墙网关系统 IP 地址 10.0.0.1，使用以太网设备 eth0
# 私有网络地址为 192.168.0.0，使用以太网设备 eth1
# 网站地址为 10.0.0.2
# 关闭 IP 转发
echo 0 > /proc/sys/net/ipv4/ip_forward
# 清空链规则
iptables -F INPUT
iptables -F OUTPUT
iptables -F FORWARD
# 设置默认（策略）规则
iptables -P INPUT DROP
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT

# IP 欺骗，拒绝内部网络中任何带有外部
# 源地址的数据包。
iptables -A INPUT -j LOG -i eth1 \ -s 192.168.0.0/24
iptables -A INPUT -j DROP -i eth1 \ -s 192.168.0.0/24
iptables -A FORWARD -j DROP -i eth1 \ -s 192.168.0.0/24
```

## 第 35 章：网络防火墙：Netfilter 865

```
# 欺骗，拒绝任何带有内部网络 
# 地址（任何不在 eth0 上的）的外部数据包
iptables -A INPUT -j DROP \ -i eth1 -s 192.168.0.0/24
iptables -A OUTPUT -j DROP \ -i eth1 -s 192.168.0/24
# 欺骗，拒绝任何带有本地地址
#（数据包）不在 lo 接口上（任何在 eth0 或 eth1 上的）且带有
# localhost 源地址的数据包
iptables -A INPUT -j DROP \ -i lo -s 127.0.0.0/255.0.0.0
iptables -A OUTPUT -j DROP \ -i lo -s 127.0.0.0/255.0.0.0

# 允许防火墙系统用户的入站消息
iptables -A INPUT -ACCEPT -i lo

# 允许与 Web 服务器（地址 10.0.0.2）通信
niptables -A INPUT -ACCEPT -p tcp -i eth0 --dport -s 10.0.0.2
# 允许从 Web 服务器到内部网络的已连接
iptables -A OUTPUT -m state --ESTABLISHED,RELATED -i eth0 -p tcp
--sport -s 10.0.0.2 -d 192.168.0/24 -j ACCEPT
# 防止 Web 服务器到内部网络的新连接
iptables -A OUTPUT -m state --NEW -i eth0 -p tcp --sport
-d 192.168.0/24 -j DROP
```

## 第 35 章：网络防火墙：Netfilter

```
# 指向系统的已建立和相关的外部通信
# 允许外部与防火墙通信，除了 ICMP 数据包
iptables -A INPUT -m state --ESTABLISHED,RELATED -i eth0 \ icmp -nACCEPT
# 防止外部发起连接
iptables -A INPUT -m state --NEW -i eth0 -j DROP
# 允许本地和之间的所有本地通信
iptables -A INPUT -m state --NEW -i eth0 -j DROP
# 允许防火墙用户的入站消息
iptables -A INPUT -ACCEPT -i lo
# 允许与 Web 服务器（地址 10.0.0.2）通信
niptables -A INPUT -ACCEPT -p tcp -i eth0 --dport -s 10.0.0.2
# 允许从 Web 服务器到内部网络的已连接
iptables -A OUTPUT -m state --ESTABLISHED,RELATED -i eth0 -p tcp
--sport -s 10.0.0.2 -d 192.168.0/24 -j ACCEPT
```

## 红帽 Linux 8：完整参考手册

```
# 允许外部访问防火墙，
# ICMP 包除外
iptables -A INPUT -m state --state ESTABLISHED, RELATED \
  -i eth0 -p ! icmp -j ACCEPT
```

为了防止外部人员访问你的任何系统，请创建一个规则，使用状态 选项配合 `NEW` 允许从外部通过 SYN 数据包进行访问。丢弃 `eth0` 连接上的任何新连接（假设只有 `eth0` 连接到互联网或外部网络）。

```
# 防止由外部发起的连接
iptables -A INPUT -m state --state NEW -i eth0 -j DROP
iptables -A FORWARD -m state --state NEW -i eth0 -j DROP
```

为了允许内部网络与防火墙进行交互，你允许来自内部以太网连接 `eth1` 的所有数据包的输入。有效的内部网络地址被指定为输入源：

```
iptables -j ACCEPT -p all -i eth1 -s 192.168.0.0/24
```

要实现地址伪装（masquerading），即私有网络上的系统可以使用网关的互联网地址连接互联网主机，你需要创建一个带有 `MASQUERADE` 目标的 NAT 表（`-t nat`）`POSTROUTING` 规则：

```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

除了允许 ping 和目标不可达 ICMP 包外，你还输入了以防火墙为目的的 `INPUT` 规则。为了启用 ping 操作，你同时使用了 `echo-reply` 和 `echo-request` ICMP 类型，以及 `destination-unreachable` 类型：

```
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type \
  echo-reply -d 10.0.0.1
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type \
  echo-request -d 10.0.0.1
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type \
  destination-unreachable -d 10.0.0.1
```

最后，再次开启 IP 转发：

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

`iptables` 选项列表显示了每个选项对应的不同规则，如下：
