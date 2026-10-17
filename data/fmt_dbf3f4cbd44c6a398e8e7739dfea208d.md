
| left 计算机 | 路由器 | rightnet 计算机 |
|---|---|---|
| `08:00:27:f6:ab:b9` | `08:00:27:13:f5:a` | `08:00:27:bc:4a:6b` |
| `192.168.60.8` | `192.168.60.1` | `192.168.70.1` |

### 3. 如何验证路由器默认是否允许数据包转发？

测试从路由器 ping 到另外两台机器，以及从那两台机器到路由器。使用`arp -a`确保你连接的是正确的 MAC 地址。

这可以通过`grep ip_forward /etc/sysctl.conf`（`1`为启用，`0`为禁用）或使用`sysctl -a | grep ip_forward`来完成。

```
root@router-# grep ip_forward /etc/sysctl.conf
net.ipv4.ip_forward = 0
```

### 4. 从左电脑 ping 到右电脑

在路由器上启用/禁用数据包转发，并验证两个网络之间的 ping 发生了什么变化。如果你无法在两个网络（不同子网）之间进行 ping，请使用`wireshark`或`tcpdump`等嗅探器来发现问题。

你是否忘记为局域网机器添加默认网关？使用`route add default gw 'ip-address'`。

```
root@left-# route add default gw 192.168.60.1
root@right-# route add default gw 192.168.70.1
```

当数据包转发启用（且默认网关配置正确）时，你应该能够成功 ping。当数据包转发禁用或网关配置不正确时，ping 将无法工作。

### 5. 使用 wireshark 或 tcpdump 分析数据包

使用`wireshark`或`tcpdump -xx`来回答以下问题。数据包通过过滤器时，源 MAC 会发生变化吗？目的 MAC 呢？源和目的 IP 地址呢？

通过路由器时，两个 MAC 地址都会发生变化。像这样使用`tcpdump -xx`：

```
root@router-# tcpdump -xx -i eth1
root@router-# tcpdump -xx -i eth2
```

## 路由器简介

### 6. 连接互联网

还记得路由器上的第三张网卡吗？将此网卡连接到带有互联网的局域网。在许多局域网中，`dhclient eth0`命令可以直接运行（将`eth0`替换为正确的接口）。

```
root@router~# dhclient eth0
```

你现在有了与图片类似的设置。需要执行什么操作才能为`leftnet`和`rightnet`提供互联网访问。

![](img/1d499a6177836f6f088a9e2a53e11a14_128_0.png)

`leftnet`和`rightnet`上的客户端需要一个工作的`dns server`。我们在这里使用 Google 的 dns 服务器之一。

```
echo nameserver 8.8.8.8 > /etc/resolv.conf
```

# 第 8 章 iptables 防火墙

本章介绍了一些简单的防火墙规则以及如何使用`iptables`配置它们。

`iptables`是一个允许用户配置 Linux 内核内置防火墙功能的应用程序。

## 8.1. iptables

默认情况下，内核中有三张包含一组组规则的表。

`filter`表用于数据包过滤。

```
root@debian6~# iptables -t filter -L
Chain INPUT (policy ACCEPT)
  target     prot source destination
Chain FORWARD (policy ACCEPT)
  target     prot source destination
Chain OUTPUT (policy ACCEPT)
  target     prot source destination
```

`nat`表用于地址转换。

```
root@debian6~# iptables -t nat -L
Chain PRERUTING (policy ACCEPT)
  target     prot source destination
Chain POSTROUTING (policy ACCEPT)
  target     prot source destination
Chain OUTPUT (policy ACCEPT)
  target     prot source destination
```

`mangle`表可用于数据包的特殊处理。

每个表中的规则系列称为`chain`。我们稍后会讨论链。

## 8.2. 启动和停止 iptables

下面的截图显示了如何在 Red Hat/Fedora/CentOS 兼容发行版上启动和停止`iptables`。

```
root@centos6 ~# service iptables stop
root@centos6 ~# service iptables start
iptables: Applying firewall rules  [ ok ]
root@centos6 ~#
```

Debian 和 Ubuntu 没有这个脚本，但可以卸载。

```
root@debian6~# aptitude purge iptables
```

## 8.3. filter 表

### 8.3.1 关于数据包过滤

`数据包过滤`比数据包转发复杂一点。数据包转发仅使用路由表做决策，而数据包过滤使用规则列表。内核将根据这些规则决定对每个数据包进行什么操作。

#### 8.3.2. filter 表

`iptables`中的`filter`表有三个链（规则组）。`INPUT`链用于进入系统的数据包。`OUTPUT`链用于离开系统的数据包。`FORWARD`链用于通过系统转发（路由）的数据包。

![](img/1d499a6177836f6f088a9e2a53e11a14_131_0.png)

截图显示了如何列出`filter`表及其所有规则。

```
[root@RHEL5]# iptables -t filter -nL
Chain INPUT (policy ACCEPT)
  target     prot source destination
Chain FORWARD (policy ACCEPT)
  target     prot source destination
Chain OUTPUT (policy ACCEPT)
  target     prot source destination
[root@RHEL5]#
```

你可以看到，`filter`表中的三个链都设置为`ACCEPT`。`ACCEPT`是默认行为。

#### 8.3.3. 设置默认规则

规则的默认确实是`ACCEPT`所有。这不是最安全的防火墙。更安全的设置是`DROP`所有。被丢弃的数据不会在任何链中继续，也不会向任何地方发送警告或错误。

下面的命令将锁定计算机。不要在`ssh` shell 内部执行这些命令。

```
root@debianpaul:~# iptables -P INPUT DROP
root@debianpaul:~# iptables -P OUTPUT DROP
root@debianpaul:~# iptables -P FORWARD DROP
root@debianpaul:~# iptables -L
```

```
Chain INPUT (policy DROP)
  target     prot source destination

Chain FORWARD (policy DROP)
  target     prot source destination

Chain OUTPUT (policy DROP)
  target     prot source destination
```

#### 8.3.4. 修改策略规则

首先，让我们所有链的默认策略设置为`drop`。注意，输入此命令时可能会丢失连接；

```
[root@RHEL5 ~]# iptables -P INPUT DROP
[root@RHEL5 ~]# iptables -P FORWARD DROP
[root@RHEL5 ~]# iptables -P OUTPUT DROP
```

接下来，我们允许服务器使用自己的回环设备（这允许链访问在`localhost`上运行的服务）。我们首先向`INPUT`链添加规则允许来自`lo`（回环）接口的流量，然后对通过回环接口离开系统的数据包执行相同的操作。

查看`filter`表（省略`-filter`因为它是默认表）：

```
[root@RHEL5 ~]# iptables -nL
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT
```
