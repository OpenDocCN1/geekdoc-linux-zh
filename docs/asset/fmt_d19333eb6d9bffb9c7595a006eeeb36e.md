
`inet 127.0.0.1/8 scope host`
`valid_lft forever preferred_lft forever`
`inet6 ::/128 scope host`
`valid_lft forever preferred_lft forever`
`25: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 disc noqueue group default qlen 1000`
`link/ether 00:0c:29:33:b5:2d brd ff:ff:ff:ff:ff:ff`
`inet 192.168.0.5/24 192.168.0.255 scope global`
`valid_lft forever preferred_lft forever`
`inet6 fe80::10c:29ff:fe3b25/64 scope link noprefixroute`
`valid_lft forever preferred_lft forever`

上述输出显示了 `lo` 接口和 `ens33` 接口，后者已通过上述命令分配了地址。

要验证设备的连通性，可以使用 `ping` 命令。当发送者向接收者请求响应时，会发送一种特殊的回显请求（echo request）。如果两个设备之间的连接能够成功建立，接收者将发回回显响应（echo reply），从而验证您的连接：

```
ping -c 3 192.168.0.1
PING 192.168.0.1 56(64) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=64 time=2.16 ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=64 time=1.85 ms
64 bytes from 192.168.0.1: icmp_seq=3 ttl=64 time=3.41 ms
192.168.0.1 statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 5ms
rtt min/avg/max/mdev = 1.849/2.473/3.410/0.674 ms
```

`-c 3` 参数使得 `ping` 在发送三个回显请求后停止。否则，`ping` 将继续运行，需要通过 `ctrl+C` 停止。

## IPv4 路由

路由是指数据包从源网络传输到目标网络的过程。每个设备都维护着路由表，其中包含以下信息：哪些 IP 网络可以通过设备连接的链路层网络直接到达，以及哪些 IP 网络可以通过将数据包传递给路由器来到达。最后，默认路由（default route）定义了接收所有未匹配其他路由的数据包的路径。

在建立连接时，设备会在其路由表中查找目标的 IP 地址。如果条目与该地址匹配，数据包将发送到相应的链路层网络，或转发给路由表中的路由器。

路由器本身也维护路由表。当接收到数据包时，路由器会在自己的路由表中查找目标地址，并将数据包发送给下一个路由器。这一过程不断重复，直到数据包到达目标网络上的路由器。在此过程中涉及的每个路由器被称为一个“跳”（hop）。最后一条路由会在路由表中为目标地址找到直接连接的链路，并将数据包发送到其目标接口。

大多数家庭网络只有一个出口，即来自互联网服务提供商（ISP）的单一路由器。在这种情况下，设备将所有非内部网络的数据包直接转发到路由器，然后路由器将其发送到提供商的路由器进行进一步转发。这就是默认路由的一个示例。

`ip route show` 列出当前的 IPv4 路由表：

```
$ ip route show
127.0.0.0/8 via 127.0.0.1 dev lo0
192.168.0.0/24 dev ens33 scope link
```

要添加默认路由，只需要作为默认网关的路由器内部地址。例如，如果路由器地址为 `192.168.0.1`，则通过以下命令设置默认路由：

```
$ sudo ip route add default via 192.168.0.1
```

再次运行 `ip route show` 进行验证：

```
$ ip route show
default via 192.168.0.1 dev ens33
127.0.0.0/8 via 127.0.0.1 dev lo0
```

## IPv6 网络

IPv6 的设计是为了解决随着更多设备上线导致 IPv4 地址不足的问题。然而，IPv6 还包含诸如自动配置的新协议等功能。IPv6 不再使用每个地址 32 位，而是使用 128 位……（注：后续原文内容严重混乱，此处未予翻译）

## Linux Essentials (版本 1.6) | 主题 4：Linux 操作系统

```
PING 2001:db8:abcd::1(2001:db8:abcd::1) 56 data bytes
64 bytes from 2001:db8:abcd::1: icmp_seq=1 ttl=64 time=0.030 ms
64 bytes from 2001:db8:abcd::1: icmp_seq=2 ttl=64 time=0.040 ms
64 bytes from 2001:db8:abcd::1: icmp_seq=3 ttl=64 time=0.072 ms
--- 2001:db8:abcd::1 ping 统计 ---
3 packets transmitted, 3 received, 0% packet loss, time 43ms
rtt min/avg/max/mdev = 0.030/0.047/0.072/0.018 ms
```

在某些 Linux 系统上，`ping` 不支持 IPv6。这些系统提供了一个已弃用的 `ping6` 命令作为替代。

再次使用 `ping` 验证链路本地地址。但由于所有接口都使用 `fe80::/64` 前缀，必须在地址后指定正确的接口：

```
$ ping6 -c 1 fe80::010c:29ff:fe33:3b25%ens3
PING fe80::010c:29ff:fe33:3b25(fe80::010c:29ff:fe33:3b25) 56 data bytes
64 bytes from fe80::010c:29ff:fe33:3b25%ens3: icmp_seq=1 ttl=64 time=0.049 ms
--- fe80::010c:29ff:fe33:3b25 ping 统计 ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.049/0.049/0.049/0.000 ms
```

### DNS

IP 地址很难记忆，而且如果你试图推销某种服务或产品，它们并没有很高的“酷炫系数”。这就是域名系统（DNS）大显身手的地方。在最简单的形式下，DNS 是一个分布式的电话簿，将如 `example.com` 这样易记的域名映射到 IP 地址。例如，当用户访问网站时，他们会将 DNS 主机名作为 URL 的一部分输入。网络浏览器将 DNS 名称发送到已配置的任何 DNS 解析器。该 DNS 解析器反过来返回与域名关联的地址。解析器回复该地址，网络浏览器随后尝试连接该地址的 Web 服务器。

Linux 用于查找 DNS 数据的解析器配置在 `/etc/resolv.conf` 文件中：

```
$ cat /etc/resolv.conf
search lpi
nameserver 192.168.0.1
```

# Linux Essentials (版本 1.6) | 4.4 网络上的你的计算机

当解析器执行名称查找时，它会首先检查 `/etc/hosts` 文件，查看其中是否包含请求名称的地址。如果包含，它将返回该地址而不联系 DNS。这允许网络管理员提供名称解析，而无需努力配置完整的 DNS 服务器。该文件中的每行包含一个 IP 地址，后面紧跟一个或多个：

```
127.0.0.1       localhost.localdomain localhost
::1              localhost.localdomain localhost
192.168.0.10    server
2001:db8:0abcd::f server
```

要在 DNS 中执行查找，请使用 `host` 命令：

```
$ host learning.lpi.org
learning.lpi.org has address 208.94.166.198
```

可以使用 `dig` 命令获取更详细的信息：

```
$ dig learning.lpi.org
<<< DIG: 14 learning.lpi.org
```
