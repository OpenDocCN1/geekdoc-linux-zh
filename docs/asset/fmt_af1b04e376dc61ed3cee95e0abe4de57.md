
- 隧道目的地

- 隧道源

你需要掌握的概念：

- 解释如何配置 IPv6-over-IPv4 隧道和 IPv6 多路复用。

- 解释如何排查 IPv6 配置和接口问题。

# 第8章

本章接续上一章的内容，涵盖了 IPv6 多路复用以及一种允许 IPv6 接口通过 IPv4 网络进行通信的机制。这被称为隧道技术（tunnelling）。本章还介绍了 IPv6 的故障排除。

## IPv6 多路复用

IP 多路复用在第5章“IP 多路复用”中介绍。使用 IPv6 多路复用，设置与 IPv4 非常相似，尽管存在一些重要的区别。最显著的区别是，测试地址是在同一个网络接口（如 `eth0`）上创建的，不需要额外的逻辑接口，而且测试地址也可以用于正常操作。在 IPv4 设置中，测试地址仅用于启用 `in.multipathd` 进程探测其状态。

与 IPv4 类似，IPv6 多路复用可以通过命令行或使用配置文件进行设置。

> 记住，如果你在命令行上设置多路复用，配置将在下次重启时丢失。为了让你的更改在重启后持续，你必须使用配置文件，以便系统每次重启时都实现多路复用。

### 使用配置文件

要对现有的 IPv6 接口使用 IP 多路复用，只需为你想要参与多路复用的网络接口编辑相关的 `/etc/hostname6.interface`，然后重启系统。

为有两个接口——`eth0` 和 `eth1` 的系统设置 IPv6 多路复用并使用名为 `ip6test` 的多路组，你需要编辑 `/etc/hostname6.eth0` 和 `/etc/hostname6.eth1` 文件，并在每个文件中添加以下条目：

- `failover group ip6test up`

> 使用配置文件配置 IPv6 多路复用假设 IPv6 接口已经存在——也就是说，它们已经配置好正常使用。此过程仅仅修改接口的功能以参与多路复用。

### 高级 IPv6 15

当系统重启时，使用 `ifconfig -a` 命令查看配置：

```bash
extra0# ifconfig -anlo: flags=1000849<UP,LOOPBACK,RUNNING,MULTICAST,IPv4> mtu 8232 index 1
inet 127.0.0.1 netmask ff000000
hme0: flags=1000843<UP,BROADCAST,RUNNING,MULTICAST,IPv4> mtu 1500 index 2
inet 192.168.28.28 netmask fffffffff0 broadcast 192.168.28.255
groupname ip6test
ether 08:20:b3:41:52
lo0: flags=2000843<UP,LOOPBACK,RUNNING,MULTICAST,IPv6> mtu 8252 index 1
inet6: ::1/128
hme0: flags=a000841<UP,RUNNING,MULTICAST,IPv6,NOFAILOVER> mtu 1500 index 2
ether 08:20:b3:41:52
inet6: fe80::a200:ff:feb3:4153/10
groupname ip6test
hme1: flags=a000841<UP,RUNNING,MULTICAST,IPv6> mtu 1500 index 3
inet 192.168.28.28 netmask fffffffff broadcast 192.168.28.255
groupname ip6test
ether 08:20:b3:41:52
inet6: fe80::a200:ff:feb3:4153/10
groupname ip6test
```

从这段代码中注意：

- 多路复组已应用于 IPv6 接口和 IPv4 接口。

- `hme0` 和 `hme1` 的 `inet6` 行现在被配置为 IPv6 多路复用守护进程 `in.pathd` 监控的测试地址。

### 使用命令行

IPv6 多路复用也可以手动在命令行上设置，但所做的任何更改将在系统下次重启时丢失。与 IPv4 类似，你可能需要使用 Solaris 8 10/000，并且你的系统需要支持本地以太网地址。这在第1章“局域网”的“分配基于端口以便太网地址”部分描述过。

为了在一个有两个网络接口——`hme0` 和 `hme1` 以及多路复组 `ip6test` 的系统上设置 IPv6 多路复用，需要执行以下操作：

1. 运行 `ifconfig -a` 查看当前的接口设置：

```bash
extra0# ifconfig -a
lo: flags=1000849<UP,LOOPBACK,RUNNING,MULTICAST,IPv4> mtu 8232 index 1
inet 127.0.0.1 netmask ff000000
hme0: flags=1000843<UP,BROADCAST,RUNNING,MULTICAST,IPv4> mtu 1500 index 2
inet 192.168.28.28 netmask fffffffff0 broadcast 192.168.28.255
groupname ip6test
ether 08:20:b3:41:52
lo: flags=2000843<UP,LOOPBACK,RUNNING,MULTICAST,IPv6> mtu 8252 index 1
inet6: ::1/128
hme0: flags=a000841<UP,RUNNING,MULTICAST,IPv6,NOFAILOVER> mtu 1500 index 2
ether 08:20:b3:41:52
inet6: fe80::a200:ff:feb3:4153/10
groupname ip6test
hme1: flags=a000841<UP,RUNNING,MULTICAST,IPv6> mtu 1500 index 3
inet 192.168.28.28 netmask fffffffff broadcast 192.168.28.255
groupname ip6test
ether 08:20:b3:41:52
inet6: fe80::a200:ff:feb3:4153/10
groupname ip6test
```

当前配置显示 `hme0` 和 `hme1` 都有 IPv6 地址——这些是步骤1代码中 `hme0` 和 `hme1` 的十六进制值。

2. 将 `hme0` 接口分配给多路组 `ip6test`：

```bash
ultra1# ifconfig group ip6test
```

3. 对 `hme1` 接口重复步骤2，使两个接口都关联多路组 `ip6test`。

4. 为 `hme0` 和 `hme1` IPv6 接口配置测试地址，以便 `in.pathd` 监控：

```bash
ultra1# ifconfig hme0 inet6 -failover
ultra1# ifconfig hme1 inet6 -failover
```

5. 启动 `in.pathd` 进程（如果尚未运行）以监控网络接口。通过输入以下命令检查守护进程是否运行：

```bash
ultra1# ps -ef grep multipath
root 366 354 0 10:41:07 pts/2 0:00 grep multipath
root 365 1 10:41:03 ? 0:00 /sbin/in.pathd
```

结果显示守护进程正在运行。如果进程未运行，你可以重启系统或手动启动：

```
ultra1# /sbin/in.pathd
```

6. 多路复用现在正在运行。

> IPv6 接口的多路复用测试地址不需要标记为弃用（防止普通应用程序使用该地址），就像你在 IPv4 中实现多路复用时那样。

![](img/b8864f36e279929da7f839558b4dd_189_0.png)

## IPv6 隧道

在从 IPv4 到 IPv6 的过渡期间，会出现这种情况：网络上的两个主机配置了 IPv6 地址，但中间的主机和路由器属于 IPv4 网络。本节介绍了如何使用隧道来解决这个问题。

### 什么是 IPv6-over-IPv4 隧道？

IPv6-over-IPv4 隧道是一种允许 IPv6 数据报在 IPv4 网络上传输的机制。发送者和接收者都支持 IPv6（以及 IPv4），但路径上的主机和路由器仅支持 IPv4。例如，可以将加密比作类比。只有发送者和目标接收者知道如何获取数据（例如信用卡详情）。当这些敏感信息在互联网上传输时，实际数据是无法访问的，并传递到目的地，在那里被正确提取。通过 IPv6-over-IPv4 隧道，数据在发送端被封封装成 IPv4 数据报，然后作为普通的 IPv4 数据报跨网络传输。当数据报到达目的地时，IPv6 数据被提取（解封装）。

### 配置隧道

本节介绍了如何在两个主机（`ultra0` 和 `systema`）之间配置 IPv6-over-IPv4 隧道，每个主机都有一个 `hme0` 网络接口。

以下步骤描述了如何创建隧道。

1. 需要在两个系统上配置一个新的 IPv4 逻辑接口。

在 `ultra0` 主机上输入：
