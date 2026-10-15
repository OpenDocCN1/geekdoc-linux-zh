
前述输出中的项通过主机服务器 `server1.class.com`、`localhost` 和 `localhost.localdomain` 指定本地计算机 `127.0.0.1`。同样，你可以使用主机 `ftp.sampledomain.com` 或 `fileserver` 来指向 IP 地址为 `3.0.0.2` 的计算机。此外，IP 地址为 `10.3.0.1` 的计算机可以使用名称 `alpha`。

由于在 `/etc/hosts` 文件中列出网上所有主机的名称非常繁琐，ISP 可以在互联网上的 DNS 服务器中使用 FDN（完全限定域名）。应用程序可以询问 DNS 获取特定 FDN 关联的 IP 地址。要配置你的系统通过联系 DNS 服务器来解析名称，请编辑 `/etc/resolv.conf` 文件。该文件可以包含三个 DNS 服务器；如果第一个 DNS 服务器不可用，系统将尝试连接到第二个 DNS 服务器，然后是文件列表中列出的第三个 DNS 服务器。以下是一个 `/etc/resolv.conf` 文件的示例：

```
[root@server1 ~]# cat /etc/resolv.conf
nameserver 209.121.197.2
nameserver 192.139.188.144
nameserver 6.0.4.211
[root@server1 ~]#
```

每个网络接口都有一套不同的 DNS 服务器用于名称解析。要实现这一点，你可以像本章前面所示，在网络接口的 IP 配置文件中指定 DNS 服务器。在这种情况下，当接口激活时，网络接口 IP 配置文件中列出的 DNS 服务器将被写入 `/etc/resolv.conf` 文件。

> 注意：在 Ubuntu Server 14.04 中，`/etc/resolv.conf` 文件是在启动时动态构建的。要手动添加 DNS 服务器，请向 `/etc/resolvconf/resolv.conf.d/base` 添加适当的行，它们将在随后的每次启动时合并到 `/etc/resolv.conf` 中。在运行 systemd 的 Linux 发行版中，由 systemd-resolved 服务处理名称请求。该服务查询大多数 Linux 发行版中 `/etc/resolv.conf` 文件列出的 DNS 服务器，但可能被配置为使用 `/run/systemd/resolve/stub-resolv.conf` 文件；在这种情况下，它只是指向 `/run/systemd/resolve/stub-conf` 的符号链接。可以在命令行提示符处将主机名或 FDN 作为参数传递 `nslookup`、`dig` 或 `host` 命令来测试 DNS 配置。

当在使用特定应用程序时指定主机名时，应用程序必须通过搜索本地 `/etc/hosts` 或 DNS 服务器将该主机名解析为适当的 IP 地址。应用程序用于解析主机名的方法由 `/etc/nsswitch.conf` 文件中的 "hosts" 行决定；以下输出为该示例：

```
[root@server1 ~# grep hosts /etc/nsswitch.conf
hosts:      files dns
[root@server1 ~]#
```

前述输出表明应用程序尝试使用 `/etc/hosts` (files) 解析主机名。如果失败，应用程序将联系 `/etc/resolv.conf` 文件中列出的 DNS 服务器 (dns)。

在较旧的 Linux 计算机上，使用 `/etc/host.conf` 文件代替 `/etc/nsswitch.conf`；该文件的存在是为了支持旧程序，如果安装了旧程序，则应包含与 `/etc/nsswitch.conf` 相同的名称解析顺序。以下输出显示了一个告诉应用程序搜索 `/etc/hosts` (hosts) 后搜索 DNS 服务器 (bind) 的 `/etc/host.conf` 文件示例：

```
[root@server1 ~#] cat /etc/host.conf
multi on
order hosts,bind
[root@server1 ~]#
```

### 路由

网络上的每台计算机都维护一个 IP 网络列表，数据包发送到适当的位置；此列表被称为路由表，存储在系统内存中。要使用路由表，可以使用 `route` 命令，如下输出所示：

```
[root@server1 ~]# route
Kernel IP routing table
```

| 目的 | 网关 | 掩码 | 标志 | 标量 | Ref | 使用 | 接口 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 10.0.0.0 | * | 255.255.0.0 | U | 2 | 0 | 0 | wlan0 |
| 192.168.0.0 | * | 255.255.0.0 | U | 0 | 0 | 0 | eth0 |
| 127.0.0.0 | * | 255.255.0.0 | U | 0 | 0 | 0 | lo |
| default | 192.168.0.1 | 0.0.0.0 | UG | 0 | 0 | 0 | eth0 |

```
[root@server1 ~]#
```

注意：`netstat -r` 命令等于 `route` 命令。`/etc/networks` 文件包含 IP 网络的别名。前述输出中的 "default" 行指的是 0.0.0.0 网络，因为 `/etc/networks` 为 0.0.0.0 网络提供了名为 "default" 的别名。要查看不带别名的路由，请向 `route` 或 `netstat -r` 命令提供 `-n` 选项。前述输出中的路由表表明，发往 10.0.0.0 网络的的所有数据包都将发送到 wlan0 设备。同样，发往 192.168.0.0 网络的数据包将发送到 eth0 设备，发往 127.0.0.0 网络的数据包将发送到环回接口 (lo)。

现在，RouterA 将所有发往 3.0.0/8 网络的数据包发送到计算机 2.0.0.2 (RouterB)。随后，RouterB 将这些数据包转发到 3.0.0/8 网络，因为它的路由表中有一条路由记录，显示它通过 IP 地址为 3.0.0.1 的网络接口连接到 3.0.0/8 网络。

同样，对于 RouterB 接收的来自 1.0.0/8 网络的转发数据包，它必须有一条路由通过 2.0.0.1 接口将这些数据包发送到 RouterA：

```
[root@server1 ~]# route add -net 1.0.0.0 netmask 255.0.0.0 gw 2.0.0.1
[root@server1 ~]# _
```

你可以使用 `route del <route>` 命令删除路由表条目。

`ip` 命令也可用于查看和操作路由表。例如，可以使用命令 `ip route add 1.0.0.0/8 via 2.0.0.1` 将之前输出所示的路由添加到路由表，而命令 `ip route show` 可以显示路由表。

计算机关机时路由内容将会丢失；为了在每次启动时都将之前输出中的额外路由加载到路由表，在 Fedora 28 系统上，将行 `1.0.0.0/ via 2.0.0.1 dev interface` 添加到 `/etc/sysconfig/network-scripts/route-interface` 文件中；在 Ubuntu Server 14 系统上，将行 `route -net 1.0.0.0 netmask 255.0.0.0 gw 2.0.0.1` 添加到 `/etc/network/interfaces` 文件的网络接口部分。对于 Ubuntu，你可以在 `/etc/netplan` 下的 YAML 文件的网络接口部分内添加以下行：

+   routes:
  - to: 1.0.0.0/8
    via: 2.0.0.1

你还可以在网络内的路由器上使用路由协议来自动向路由表添加路由。两种常见的路由协议是路由信息协议 (RIP) 和开放最短路径优先协议 (OSPF)。如果你安装了 `zebra` 软件包，可以使用 `zebra` 命令配置 RIP 和 OSPF 路由。

像互联网等大型网络上的所有路由列表太大了，无法存储在路由器的路由表中，大多数路由器都配置了默认网关。任何目标不在路由表中列出的数据包都会发送到默认网关，默认网关可以将数据包转发到适当的网络或路由器自身的网关，以此此类推，直到数据包到达目的地。

# 第 12 章 网络配置

如果你网络上的计算机无法连接到远程网络上的计算机，问题可能与路由有关。用于诊断路由的常用工具是 `traceroute` 命令；它显示当前计算机和远程计算机之间的所有路由器。要追踪从本地计算机到 IP 地址 3.4.5.6 的路径，你可以使用以下：
