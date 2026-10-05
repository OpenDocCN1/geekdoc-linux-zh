

# TCP/IP 与网络管理
## 第 7 章

通过此配置，除网络名称外的所有名称都将首先在 `/var/db` 中查找（为了提高效率）。如果在该处未找到，则将在相应的 `/etc` 文件中查找。如果相应的数据库中存在适当的条目，NIS 还可以查找相当多的数据库。

## 配置 DNS 客户端：/etc/resolv.conf

`/etc/resolv.conf` 文件用于配置 DNS 客户端。它包含了主机的域名搜索顺序和 DNS 服务器的地址。每行都应该包含一个关键字和一个或多个由空格分隔的参数。以下是有效的关键字：

| 关键字 | 含义 |
| --- | --- |
| nameserver | 它的单个参数表示 DNS 服务器的 IP 地址。最多可以三行 `nameserver`，每行对应一个 IP 地址。`nameservers` 将按照它们在文件中出现的顺序进行查询。如果第一个 `nameserver` 没有响应，才会查询第一个之后的 `nameserver`。 |
| domain | 它的单个参数表示主机的域名。这被多个程序（如邮件系统）使用，并且在对没有域名的主机（例如没有点的点）进行 DNS 查询时也会使用。如果没有域名，将使用主机名，并删除第一个点之前的所有内容。 |
| search | 它的多个参数表示域名的搜索顺序。如果对没有域名的主机进行查询，则将在关键字所指定的每个域名中连续查找该主机。注意，`domain` 和 `search` 是互斥的；如果两者都出现，则使用最后出现的一个。 |
| sortlist | 允许按特定顺序对返回的域名进行排序。通过网络/掩码对指定参数，允许任意的排序顺序。 |

![](img/cbac72550c7126a22162e94d91a0c360_218_0.png)

Linux 不提供通用的默认 `/etc/resolv.conf` 文件。其内容根据安装时提供的选项动态构建的。这是一个 `/etc/resolv.conf` 示例：

```
search my.domain.com other.domain.com
nameserver 10.1.1.1
nameserver 10.10.10.1
sortlist 10.1.1.0/255.255.255 10.0.0.0/255.255.255
```

该文件表示，未限定的主机将首先作为 `my.domain.com` 搜索，然后作为 `other.domain.com` 搜索。首先会联系 IP 地址为 `10.1.1.1` 的服务器。如果该服务器在超时后没有响应，将联系 `10.10.10.1` 的服务器。如果返回了多个主机，将首先返回 C 类网络 `10.1.1.0` 中的主机，然后是 A 类网络 `10.0.0.0` 中的任何其他主机，最后是任何其他主机。

通常情况下，你不需要手动编辑此文件，因为 YaST 提供了一种易于使用的修改此文件的方法，可以满足几乎所有用户的需求。

## 配置程序

上一节详细介绍的文件用于配置许多通用网络参数。大多数这些网络选项都可以使用 YaST 或编辑适当的文件进行动态修改。然而，动态配置主机的 IP 地址和路由表需要特殊的命令。

## 配置主机网络接口：ifconfig

`ifconfig` 程序用于配置主机的网络接口。这包括基础配置，如 IP 地址、子网掩码和广播地址，以及高级选项，例如为对点链路（如 PPP 链路）设置远程地址。

在 Linux 下，所有网络接口都有由驱动程序名称组成的名称。这些是支持 Linux 的一些接口及其类型：

| 驱动名称 | 设备类型 |
|---|---|
| eth | 以太网 |
| tr | 令牌环 |
| ppp | 对点协议 |
| slip | 串行链路 |
| plip | 并行链路 |

在 Linux 下，所有网络接口都有驱动程序名称后跟一个数字。如果使用 SuSE 编译的内核，接口将从 0 开始计数。这些是内核的：

如果返回多个网卡，将返回 C 类网络 `10.1.1.0` 中的主机。如果你使用编译到内核的网卡，`ifconfig` 只能显示一个。相反，如果你有多个网卡且是编译到内核的，需要将以下内容添加到 `/etc/resolv.conf`：

```
BROUP, RUNNING,MULTICAST,  mt=0
```

`nameserver` 它的单个参数表示 DNS 服务器的 IP 地址。最多可以三行 `nameserver`，每行对应一个 IP 地址。`nameservers` 将按照它们在文件中出现的顺序进行查询。如果第一个 `nameserver` 没有响应，才会查询第一个之后的 `nameserver`。

`domain` 它的单个参数表示主机的域名。这被多个程序使用。

## 基础配置

这是 `ifconfig` 的基本格式：

```
ifconfig interface address[netmask][broadcast]
```

这种 `ifconfig` 格式只能由 root 使用。如果省略了这些，`ifconfig` 将从内核获取值。

> 注意：内核将按照其指示进行操作。

> 提示：域名掩码和广播是可选的。参见“掩码”。

## 启用和禁用接口

接口也可以临时关闭（取消激活）而无需重新配置。这是通过以下命令实现的：

```
ifconfig interface down
ifconfig interface up
```

这些 `ifconfig` 形式可以使用 root 使用。

## 检查接口状态

如果你想知道某个接口的状态，只需执行 `ifconfig` 命令。如果你想知道所有活动接口的状态，使用 `ifconfig -a`。这些 `ifconfig` 版本可以任何用户可以使用。它们显示接口的配置信息，包括 IP 地址、子网掩码、广播地址。它们还显示接口状态（例如开启或关闭，以及是否为环回接口），以及其他信息：通过接口发送的最大数据包单元（MTU）、网卡的 I/O 地址和中断号，以及接收、发送包和冲突的数量。

以下是 `ifconfig -a` 的输出示例：

```
$ /sbin/ifconfig -a
lo Link:Local Loopback
addr:127.0.0.1 Bcast:127.255.255.255 Mask:255.255.0
up BROADCAST RUNNING MTU:3584 Metric:1
RX packets:16000 errors:0 dropped:0 overruns:0 frame:0
tX packets:92691 errors:0 dropped:0 overruns:0 carrier:0
Collisions:0
eth0 Link:Ethernet HWaddr 00:20:87:3E:F0:61

addr:10.0.1.1 Bcast:10.0.255.255 Mask:255.255.255.0
up BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:90560 errors:0 dropped:0 overruns:0 frame:0
tX packets:92691 errors:0 dropped:0 overruns:0 carrier:1
Collisions:667
Interrupt:3 Base address:0x310
```

## 网络别名——一个接口，多个地址

有时，单个网络接口具有多个 IP 地址是非常有用的。例如，一台服务器可能运行多个服务，但你可能希望客户端为每个服务访问不同的 IP 地址，以便将来更容易重新配置（例如，如果你需要将某些服务拆分另一台服务器上）。Linux 和大多数其他 UNIX 变体一样提供名为网络别名的功能，它可以实现这一点。为了能够使用网络别名，你必须重新配置并编译内核，并在网络选项配置部分中启用网络别名（Network Aliasing）和别名支持（Aliasing Support）选项。这些选项既可以编译到内核中，也可以作为模块。

