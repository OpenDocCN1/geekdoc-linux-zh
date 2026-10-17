
## 10.13. `sysctl`

欲更多信息，请查看`sysctl`的`man`页面。

```
root@debian6-# man sysctl
root@debian6-# sysctl -a 2>/dev/null | grep ip_forward
net.ipv4.ip_forward = 0
```

## 10.14. 实践：数据包转发

0. 在`VirtualBox`或`VMware`中添加网卡时，你可以选择（或创建）一个内部网络。使用此选项创建两个内部网络。我将它们命名为`leftnet`和`rightnet`，但你可以选择任何其他名称。

### Network

```
Adapter 1: Intel PRO/1000 MT Desktop (bridged Adapter, en1: AirPort)
Adapter 2: Intel PRO/1000 MT Desktop (Internal Network, 'leftnet')
Adapter 3: Intel PRO/1000 MT Desktop (Internal Network, 'rightnet')
```

1. 设置两台`Linux`机器，一台在`leftnet`上，另一台在`rightnet`上。确保它们都在正确的子网中获取了`IP`地址。这两台机器对于“路由器”来说是“左侧”和“右侧”。

![](img/93b29716e9fc0b0730b4dac1126847e3_85_0.png)

2. 设置第三台`Linux`计算机，带有三块网卡，一块在`leftnet`上，另一块在`rightnet`上。这台计算机将作为“路由器”。在下表中填写相关的名称、`IP`地址和`MAC`地址。

表 10.1. 数据包转发练习

| `leftnet` 计算机 | 路由器 | `rightnet` 计算机 |
|---|---|---|
| `n` | `MAC` | | | |
| `IP` | | | |

3. 你如何验证路由器默认是否允许数据包转发？测试从路由器`ping`到另外两台机器，以及从那两台机器`ping`到路由器。使用`arp -a`确保你连接的是正确的`MAC`地址。

4. 从`leftnet`计算机`ping`到`rightnet`计算机。在路由器上启用和/禁用数据包转发，并验证两个网络之间的`ping`发生了什么变化。如果你无法在两个网络（不同子网）之间进行`ping`，请使用`wireshark`或`tcpdump`等嗅探工具来发现问题。

5. 使用`wireshark`或`tcpdump -xx`回答以下问题：当数据包通过过滤器时，源`MAC`地址会变化吗？目的`MAC`地址呢？

6. 经过路由器时，两个`MAC`地址都会发生变化。使用如下所示的`tcpdump`：

```
root@router-# tcpdump -xx -i eth1
root@router-# tcpdump -xx -i eth2
```

![](img/93b29716e9fc0b0730b4dac1126847e3_86_0)

## 10.15. 解决方案：数据包转发

![](93b29716e9fc0b0730b4dac1126847e3_87_0

1. 设置两台`Linux`机器，一台在`leftnet`上，另一台在`rightnet`上。确保它们都在正确的子网中获取了`IP`地址。这两台机器对于“路由器”来说是“左侧”和“右侧”。

这可以通过`grep ip_forward /etc/sysctl.conf`完成（1 表示启用，0 表示禁用）或`sysctl -a | grep ip_forward`。

2. 设置第三台`Linux`计算机，带有三块网卡，一块在`leftnet`上，另一块在`rightnet`上。这台计算机将作为“路由器”。在下表中填写相关的名称、`IP`地址和`MAC`地址。

表 10.2. 数据包转发

| `leftnet` 计算机 | 路由器 | `rightnet` 计算机 |
|---|---|---|
| `08:00:27:f6:ab:b9` | `08:00:23:1f:5a` | `08:00:27:be:4a` |
| `192.168.60.8` | `192.168.60.1` | `192.168.70.9` |

3. 你如何验证路由器默认是否允许数据包转发？测试从路由器`ping`到另外两台机器，以及从那两台机器`ping`到路由器。使用`arp -a`确保你连接的是正确的`MAC`地址。

你的`IP`地址可能与表中不同。

4. 从左侧计算机`ping`到右侧计算机。在路由器上启用和/禁用数据包转发，并验证两个网络之间的`ping`发生了什么变化。如果你无法在两个网络（不同子网）之间进行`ping`，请使用`wireshark`或`tcpdump`等嗅探工具来发现问题。

你是否忘记为内网机器添加默认网关？使用`route default gw 'ip-address'`

```
root@left-# route add default gw 192.168.60.1
root@right-# route add default gw 192.168.70.1
```

当数据包转发启用且两个默认网关配置正确时，你应该能够进行`ping`。当数据包转发禁用或网关配置不正确时，`ping`将无法工作。

### 路由器介绍

6. 还记得路由器上的第三块网卡吗？将此网卡连接到有互联网的局域网（`LAN`）。在许多局域网上，执行`dhclient eth0`命令即可生效（将`eth0`替换为正确的接口名称）。

```
root@router~# dhclient eth0
```

你现在的设置与此图类似。需要做哪些操作才能让`leftnet`和`rightnet`访问互联网？

![](img/93b29716e9fc0b0730b4dac1126847e3_89_0.png)

`leftnet`和`rightnet`上的客户端需要一个工作的`dns`服务器。我们在这里使用`Google`的其中一个`dns`服务器。

```
echo nameserver 8.8.8.8 > /etc/resolv.conf
```

# 第 11 章 `iptables` 防火墙

本章介绍了一些简单的防火墙规则以及如何使用`iptables`配置它们。

`iptables`是一个允许用户配置`Linux`内核内置防火墙功能的应用程序。

## 11.1. `iptables` 表（tables）

默认情况下，内核中有三个表，其中包含一组规则。

`filter`表（过滤表）用于数据包过滤。

```
root@debian6~# iptables -t filter -L
Chain INPUT (policy ACCEPT)
  target               prot opt source       destination
Chain FORWARD (policy ACCEPT)
  target               prot opt source       destination
Chain OUTPUT (policy ACCEPT)
  target               prot opt source       destination
```

`nat`表（转换表）用于地址翻译。

```
root@debian6~# iptables -t nat -L
Chain PREROUTING (policy ACCEPT)
  target               prot opt source       destination
Chain POSTROUTING (policy ACCEPT)
  target               prot opt source       destination
Chain OUTPUT (policy ACCEPT)
  target               prot opt source       destination
```

`mangle`表（修改表）用于数据包的特殊处理。

每个表中的系列规则被称为链（`chain`）。我们将在本章稍后讨论链和`nat`表。

## 11.2. 启动和停止 `iptables`

下面的截图显示了如何在`Red Hat`/`Fedora`/`CentOS`及兼容发行版上停止和启动`iptables`。

```
root@centos6 ~# service iptables stop
root@centos6 ~# service iptables start
iptables: Applying firewall rules      [ ok ]
root@centos6 ~#
```

`Debian`和`ubuntu`发行版没有这个脚本，但允许卸载。

```
root@debian6~# aptitude purge iptables
```

## 11.3. `filter` 表

### 11.3.1 关于数据包过滤

数据包过滤不仅仅是数据包转发。数据包转发只使用路由表来做决策，而数据包过滤还使用规则列表。内核将检查数据包，并根据这些规则决定对每个数据包进行什么操作。
