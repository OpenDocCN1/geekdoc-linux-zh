

![](img/863afa537de4eed7deb11978bfbfa90e_219_0.png)

![](img/863afa537de4eed7deb11978bfbfa90e_219_1.png)

作为Linux系统管理员，理解网络的基本概念至关重要，这涵盖了从流量如何由物理设备管理到数据如何呈现给最终用户的全过程。**开放系统互连模型**（*Open Systems Interconnection Model*，即OSI模型）描述了通用的标准通信协议。该模型定义了以下七个抽象层：

- **物理层（第1层）**：负责设备中数据的传输和接收，例如系统中的以太网设备、电缆或路由器中的端口。
- **数据链路层（第2层）**：提供不同节点之间的数据传输。例如，同一局域网内两台服务器之间的通信。
- **网络层（第3层）**：将数据从一个网络的一个节点传输到另一个网络的不同节点。这需要节点在不同第2层（数据链路）之间路由流量。
- **传输层（第4层）**：使用协议（如UDP或TCP）进行数据传输。
- **会话层（第5层）**：维护并同步两个节点之间的连接。
- **表示层（第6层）**：格式化和转换待使用的数据，例如数据加密/解密或压缩/解压。
- **应用层（第7层）**：用户与之交互的应用程序层。

[图 7.2](#) 展示了OSI模型中不同层之间的流量流动：

![](img/863afa537de4eed7deb11978bfbfa90e_220_0.png)

图 7.2：OSI模型层流量流动。来源：Wikipedia

在过去几十年里，网络经历了演变，从最初的通信发展到新技术的采用。早期的通信主要是在物理服务器之间通过交换机和路由器进行的。当时的主导流量是*南北向*数据流，即系统与局域网外部的设备进行通信。

随着虚拟化技术的普及，服务迁移到虚拟机中带来了通信方面的新挑战，从而增加了*东西向*流量，这指的是同一网络内部不同服务之间的通信。

容器的采用增加了系统之间的流量，并且先进的网络配置和先进的网络实现（如软件定义网络和*隧道协议*）已成为当今服务器配置时所需的知识。

另一个重要的转变是大型企业的网络架构转向称为Spine Leaf的新架构，该架构提高了流量效率并减少了由传统架构可能引起的瓶颈。图 7.3 展示了传统架构与新架构之间的区别：传统架构具有三层（接入层、汇聚层和核心层），存在并行流量方面的限制；而新架构具有网状连接，具备高带宽和低延迟特性：

![](img/863afa537de4eed7deb11978bfbfa90e_221_0.png)

*图 7.3：传统架构与Spine Leaf架构。来源：Aruba Networks*

过去几年里另一个重要变化是IPv6的引入，这是最新的互联网协议版本。这个新版本使用128位地址代替了IPv4中的32位地址。IPv6在局域网中的使用仍然有限，但互联网服务提供商（ISP）和大型企业的采用已成为现实。

## 物理层（第1层）

第6章“监控系统资源”介绍了如何使用 `lshw` 命令列出系统上可用的以太网设备。同一章还介绍了 `ethtool` 命令，用于获取状态信息，例如是否检测到链路以及可用的速度。

`ip` 命令取代了传统且已弃用的 `ifconfig` 命令在Linux中用于列出接口信息的操作。指定 `link` 作为参数时，将列出网络接口的物理信息，如图 7.4 所示：

```text
root@ubuntu:~# ip --color=auto link
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state  UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp1s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 52:54:00:ce:80:b8 brd ff:ff:ff:ff:ff:ff
3: enp7s0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT group default qlen 1000
    link/ether 52:54:00:07:3a:f8 brd ff:ff:ff:ff:ff
```

![](img/863afa537de4eed7deb11978bfbfa90e_222_0.png)

`ip link` 命令的输出包含重要信息。Linux发行版包含一个名为 $lo$ 的本地接口，用于系统内部的通信，例如TCP/UDP连接。在现代系统中，物理接口的格式为 $en$（*以太网设备*）+ $p[PCI$ *总线号*] + $s[插槽$ *号*]，而过去则使用 $ethX$（其中 $X$ 是从0开始的数字）。

输出结果将指示接口是 UP（检测到链路且接口在系统中处于活动状态）还是 DOWN（未检测到链路或接口在系统中未激活）、MTU（*最大传输单元*，通常默认为1,500）以及MAC地址（用于识别单个网络设备）。

MAC地址是配置网络接口时的重要值，例如在使用动态主机配置协议（DHCP）时分配静态IP，或在使用预启动执行环境（PXE）进行网络安装时。

局域网内节点之间的通信需要知道目的节点的MAC地址。为了知道某个节点的MAC地址，Linux会向网络发送一个数据包，询问谁拥有该目的IP地址。当获取到该信息后，它会在一个包含IP地址与MAC地址映射关系的表中存储此关系。参数 $neigh$（取代了历史命令 $arp$）显示该表信息，如图 7.5 所示：

```text
root@ubuntu:~# ip --color neigh
192.168.122.1 dev enp1s0 lldaddr 52:54:00:81:84:22 REACHABLE
192.168.122.145 dev enp1s0 lldaddr 52:54:00:a2:cb:2a REACHABLE
```

![](img/863afa537de4eed7deb11978bfbfa90e_222_1.png)

## 数据链路层（第2层）

命令 **ip** 可用于显示第2层信息、IP地址和网络掩码。添加参数 *address*（或 *a*）可显示分配给接口的地址，如 *图 7.6* 所示：

```text
root@ubuntu:~# ip --color=auto address
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
        valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
        valid_lft forever preferred_lft forever
2: enp1s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 52:54:00:ce:80:b8 brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.101/24 metric 100 brd 192.168.122.255 scope global dynamic enp1s0
        valid_lft 3414sec preferred_lft 3414sec
    inet6 fe80::5054:ff:ce:8bb8/64 scope link
        valid_lft forever preferred_lft forever
3: enp50: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ether 52:54:00:07:3a:f8 brd ff:ff:ff:ff:ff:ff
```

![](img/863afa537de4eed7deb11978bfbfa90e_223_0.png)

接口 *lo* 始终分配并配置为IP 127.0.0.1，网络掩码为255.0.0.0（/8）。前文 *图 7.6* 显示了一个名为 *enp1s0* 的接口，配置为IP 192.168.122.101，网络掩码为255.255.255.0（/24），*广播IP* 为192.168.122.255。

名为 *enp1s0* 的接口被分配了一个IPv6本地地址（以 *fe80* 开头），子网掩码为 /64。*图 7.7* 展示了一个配置了IPv6地址的接口示例：

```text
root@lab:~# ip --color -6 address show dev eth0
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 st1de UP qlen 1000
    inet6 2001:41d0:1:ee26::1/128 scope global
        valid_lft forever preferred_lft forever
    inet6 fe80::225:90ff:fe22:424a/64 scope link
        valid_lft forever preferred_lft forever
```

![](img/863afa537de4eed7deb11978bfbfa90e_223_1.png)

## 网络层（第3层）

第3层需要有关如何访问非本地网络的信息。这包括访问网络外部的默认网关，以及在需要时访问其他网络的特定网关。带有 *route* 参数的 **ip** 命令会列出当前的目标地址和网关表。*图 7.8* 展示了一个示例：

```text
root@ubuntu:~# ip --color route
default via 192.168.122.1 dev enp1s0 proto dhcp src 192.168.122.101 metric 100
192.168.122.0/24 dev enp1s0 proto kernel scope link src 192.168.122.101 metric 100
```

