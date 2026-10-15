
![](img/bafa5678973f896b93838a140b8f7840_574_3.png)

你也可以通过网络配置工具中的 DNS 标签编辑 `/etc/resolv.conf` 文件。

![](img/bafa5678973f896b93838a140b8f7840_575_0.png)

要通过将名称解析为 IP 地址来测试 DNS 配置，可以在命令行提示符输入 `nslookup name`、`dig name` 或 `host name`，其中 `name` 是远程主机的主机名或 FQDN。

![](img/bafa5678973f896b93838a140b8f7840_575_1.png)

在使用特定应用程序指定主机名时，该应用程序必须通过搜索本地 `/etc/hosts` 文件、DNS 服务器或 NIS 服务器将该名称解析为相应的 IP 地址。应用程序用于解析主机名的方法由 `/etc/nsswitch.conf` 中的 `hosts` 行决定。示例所示：

```
[root@server1]# grep hosts /etc/nsswitch.conf

hosts: files nis dns

hosts: files dns

[root@server1]#
```

上述输出表明应用程序首先尝试使用 `/etc/hosts` 文件解析主机名。如果失败，应用程序将联系 `/etc/resolv.conf` 中列出的 DNS 服务器 (`dns`)，如果配置了，则随后联系 NIS 服务器 (`nis`)。

在 Linux 计算机上，使用 `/etc/hosts` 文件代替了 `/etc/nsswitch.conf`。`/etc/hosts` 文件仍然存在以支持应用程序，并应包含与 `/etc/nsswitch.conf` 相同的解析。应用程序搜索 `/etc/hosts` 文件 (`hosts`)，然后是 DNS 服务器 (`bind`) 和 NIS 服务器 (`nis`) 的 `/etc/host.conf` 示例所示：

```
[root@server1]# cat /etc/host.conf

multi on

order hosts,bind,nis

[root@server1]#
```

### 路由

每台计算机都维护一个将数据包发送到相应位置的 TCP/IP 网络列表。此列表被称为路由表，存储在内存系统中。要查看路由表，你可以简单地使用 `route` 命令，输出所示：

```
[root@server1]# route
Kernel IP routing table
```

| Destination | Gateway | Genmask | Flags | Metric | Ref | Use | Iface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 10.0.0.0 | | 255.255.255.0 | U | 2 | 0 | 0 | wlan0 |
| 192.168.0.0 | | 255.255.255.0 | U | 0 | 0 | 0 | eth0 |
| 127.0.0.0 | | 255.0.0.0 | U | 0 | 0 | 0 | lo |
| default | 192.168.0.1 | 0.0.0.0 | UG | 0 | 0 | 0 | eth0 |

```
[root@server1]#
```

`netstat -r` 命令等同于 `route` 命令。

前面的输出显示的路由表表明，从一个接口发送到另一个接口的所有数据包将发送到设备 `wlan0`。同样，所有发往 `192.168.0.0` 网络的数据包将发送到设备 `eth0`，而发往 `127.0.0.0` 网络的数据包将发送到回环适配器 (`lo`)。必须发送到任何其他网络的数据包将发送到默认网关。最终输出显示默认网关是 IP 地址为 `192.168.0.1` 的计算机，通过 `eth0` 设备连接。

如果你的计算机配置了多个网络接口，路由表中的条目将比可用的 TCP/IP 路由多。拥有多个网络接口的计算机被称为多宿主（multihomed）。多宿主主机可以配置为从一个接口转发数据包以帮助其到达目的地；此过程通常被称为 IP 路由。要在你的 Linux 系统上启用路由，只需在 `/proc/sys/netipv4/ip_forward`（针对 IPv4）或 `/proc/sys/netipv6/conf/all/forwarding`（针对 IPv6）文件中放置数字 1，如下所示所示：

```bash
[root@server1]# cat /proc/sys/netipv4/ip_forward
0
[root@server1]# cat /proc/sys/netipv6/conf/all/forwarding
0
[root@server1]# echo 1 > /proc/sys/netipv4/ip_forward
[root@server1]# echo 1 > /proc/sys/netipv6/conf/all/forwarding
1
[root@server1]# cat /proc/sys/netipv6/conf/all/forwarding
1
```

要在每次启动时启用 IPv4 路由，请确保 `/etc/sysctl.conf` 中存在 `ipv4.ip_forward = 1` 这一行。要在每次启动时启用 IPv6 路由，请确保 `/etc/sysctl.conf` 文件存在 `ipv6.conf.default.forwarding = 1` 行。

如果你的计算机有多个网络接口并启用了路由，你的计算机只会将数据包路由到它拥有网络接口的网络。在较大的网络中，你可能有几条路由，在这种情况下，数据包可能需要经过多个路由器才能到达目的地。由于路由器只知道它们直接连接的网络，你可能需要向路由器的路由表添加默认路由，以便它知道向何处发送未知网络。例如，你的组织有三个 TCP/IP 网络（`1.0.0.0/8`, `2.0.0.0/8` 和 `3.0.0.0/8`），由两个路由器划分，如图 12 所示。

`RouterA` 有一个接口，显示它连接到 (1) 通过 IP 地址为 `1.0.0.1` 的网络接口的 `1.0.0.0/8` 网络，以及 (2) 通过 IP 地址为 `2.0.0.1` 的网络接口的 `2.0.0.0/8` 网络。当 `RouterA` 接收发往 `3.0.0.0/8` 网络的数据包时，这两条路由会自动建立，但它不知道应该将其转发到何处，因为它的路由表中没有 `3.0.0.0/8` 的路由。

## 第 12 章网络配置

![](img/bafa5678973f896b93838a140b8f7840_577_0.png)

图 12-7 示例路由网络

来源：Course Technology/Cengage Learning

为了在 `RouterA` 上为 `3.0.0.0/8` 网络添加适当路由，你可以在 `RouterA` 上运行以下命令：`gw`

```bash
@server1~# route add -net 3.0.0.0/8 netmask 255.255.0.0 gw 2.0.0.2
@server1~#
```

现在，`RouterA` 将由 `3.0.0.0/8` 网络交付的数据包发送到计算机 `2.0.0.2` (`RouterB`)。`RouterB` 然后将数据包转发到 `3.0.0.0/8` 网络，因为它的表中有一条路由，显示它通过 IP 地址为 `3.0.0.1` 的网络接口连接到 `3.0.0.0/8`。

同样，对于 `RouterB` 转发发往 `1.0.0.0/8` 网络的数据包，它必须有一条路由通过接口 `2.0.0.1` 将这些数据包发送到 `RouterA`：

```bash
@server1~# route add -net 1.0.0.0/8 netmask 255.255.0.0 gw 2.0.0.1
@server1~#
```

![](img/bafa5678973f896b93838a140b8f7840_577_1.png)

> 使用 `route <route>` 命令从路由表中删除条目。

![](img/bafa5678973f896b93838a140b8f7840_577_2.png)
