
| Red Hat 的 `route-eth0` 示例 | `192.168.10.0/24 via 192.168.122.1 dev eth0` <br> `192.168.11.0/24 via 192.168.122.1 dev eth0` |

| 使用 `nmcli` 进行 `NetworkManager` 操作 | `nmcli con mod test +ipv4.routes "192.168.10.0/24 192.168.122.10,192.168.11.0/24 192.168.122.11"` |

表 7.4：路由配置

配置静态路由后，命令 `ip route` 的输出示例如图 7.22 所示：

![](img/863afa537de4eed7deb11978bfbfa90e_235_0.png)

图 7.22：命令 `ip` 的输出示例。

配置 `Linux` 系统作为路由器时，如果使用的是同一个接口来将从源客户端到目的地的流量重定向，则通常不需要高级配置。使用不同接口则需要了解与安全防火墙相关的知识，这在下一章中有所描述。

系统中用于确定是否允许转发流量的参数由 `sysctl` 配置中的键 `net.ipv4.ip_forward` 定义。出于安全考虑，默认情况下它是禁用的（值为 `0`），可以使用命令 `sysctl` 临时启用它，或使用文件 `/etc/sysctl.conf` 永久启用。

图 7.23 到 7.26 展示了如何检查和配置 `IP` 转发，并确保该 `Linux` 系统作为路由器正常工作：

- 检查名为 `ubuntu` 的服务器上系统参数 `ip_forward` 的值：

```
root@ubuntu:~# sysctl net.ipv4.ip_forward
net.ipv4.ip_forward = 0
```

图 7.23：命令 `sysctl` 的输出示例。

- 配置名为 `rhel` 的系统使用 `ubuntu` 系统的 `IP`（`192.168.122.101`）作为网关，并尝试访问一个外部 `IP`（`Google` 的 `DNS` `IP` `8.8.8.8`）：

```
[root@rhel ~]# ip route del default
[root@rhel ~]# ip route add default via 192.168.122.101
[root@rhel ~]# ping -c1 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.

--- 8.8.8.8 ping statistics ---
1 packets transmitted, 0 received, 100% packet loss, time 0ms
```

图 7.24：使用命令 `ip` 操作及命令 `ping` 的输出示例。

- 在名为 `ubuntu` 的系统中启用 `ip forwarding`（`IP` 转发）：

```
root@ubuntu:~# sysctl net.ipv4.ip_forward=1
net.ipv4.ip_forward = 1
```

图 7.25：命令 `sysctl` 的输出示例

- 从节点 `rhel` 尝试使用 `ping` 命令以确保通信可行：

### 高级网络配置

```
[root@rhel ~]# ping -c1 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=34.9 ms

--- 8.8.8.8 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 34.929/34.929/34.929/0.000 ms
```

图 7.26：`ping` 命令的输出示例

与路由相关的另一个重要主题，尤其对于企业而言，是动态路由。这种类型的路由会实时调整；用于传输 `IP` 数据包的通路取决于不同的条件，如最短路径或最佳可用性。`边界网关协议 (BGP)` 和 `开放式最短路径优先 (OSPF)` 等协议是动态路由的一些流行示例。

#### 链路聚合 (绑定)

现在管理 `Linux` 系统需要三种重要的高级网络配置：

- 向最终用户提供服务点系统需要特殊的网络配置，以避免瓶颈并减少网络停机发生的可能性。这涉及配置链路聚合（绑定）的知识。

- 使用虚拟化技术运行虚拟机的系统需要配置网络桥接，以提供连通性和流量隔离。`Linux` 提供工具来创建所谓的 `Linux` 桥接，或使用一些工具（如 `Open vSwitch`）使用虚拟交换机。

- 在一个网络内部管理多个网络需要与 `虚拟局域网 (VLAN)` 和配置 `Linux` 系统访问这些网络相关的知识。

#### 链路聚合 (绑定)

绑定指的是将多个网络连接聚合为一个。其目的是拥有高可用性连接，允许其中一个连接故障而不造成任何停机。使用名为 `LACP (802.3ad)` 的协议，不仅可实现高可用性聚合，还可以聚合可用的流量带宽。该协议要求拥有支持此协议的交换机，并配置连接到系统的端口。

图 7.27 展示了一个使用 `nmtui` 定义新绑定（组合两个接口 `enp7s0` 和 `enp8s0`）的示例，从而创建一个新的虚拟绑定接口 `bond0`：

![](img/863afa537de4eed7deb11978bfbfa90e_238_0.png)

运行 `ip` 命令列出接口将显示物理接口和新的绑定接口。物理接口将显示其所属绑定的名称。请参见图 7.28：

```
[root@rhel ~]# ip -c -a | tail -10
3: enp7s0: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc fq_codel master bond0 state UP group default qlen 1000
    link/ether 52:54:00:10:65:8d brd ff:ff:ff:ff:ff:ff
4: enp8s0: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc fq_codel master bond0 state UP group default qlen 1000
    link/ether 52:54:00:10:65:8d brd ff:ff:ff:ff:ff:ff permaddr 52:54:00:c8:55:25
5: bond0: <BROADCAST,MULTICAST,MASTER,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 52:54:00:10:65:8d brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.218/24 brd 10.0.0.255 scope global dynamic noprefixroute bond0
       valid_lft 3474sec preferred_lft 3474sec
    inet6 fe80::6777:ae7a:a30a:bf68/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

图 7.28：`ip` 命令的输出示例

在特殊目录 `/proc/net/bonding/` 内创建一个文件，其名称与绑定接口相同，其中包含与配置相关的信息。

```
Ethernet Channel Bonding Driver: v5.14.0-70.17.1.el9_0.x86_64
Bonding Mode: load balancing (round-robin)
MII Status: up
MII Polling Interval (ms): 100
Up Delay (ms): 0
Down Delay (ms): 0
Peer Notification Delay (ms): 0

Slave Interface: enp7s0
MII Status: up
Speed: Unknown
Duplex: Unknown
Link Failure Count: 0
Permanent HW addr: 52:54:00:10:65:8d
Slave queue ID: 0

Slave Interface: enp8s0
MII Status: up
Speed: Unknown
Duplex: Unknown
Link Failure Count: 0
Permanent HW addr: 52:54:00:c8:55:25
Slave queue ID: 0
```

上述代码块展示了图 7.28 中显示的先前绑定的示例，这是一种采用负载均衡模式的配置。

#### 网络桥接
