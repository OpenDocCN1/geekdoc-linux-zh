
[root@serverA ~#] `cd /etc/sysconfig/network-scripts`

[root@serverA network-scripts]# `./ifup eth1`

> 注意：也可以使用这种方法配置别名 IP 地址。

## 附加参数

`ifconfig` 命令的格式如下：

```
[root@serverA]# ifconfig device address options
```

其中 `device` 是以太网设备的名称（例如 `eth0`），`address` 是你想要应用到设备上的 IP 地址，`options` 是以下选项之一：

| 选项 | 描述 |
| :--- | :--- |
| up | 启用设备。此选项是隐式的。 |
| down | 禁用设备。 |
| arp | 启用此设备响应请求（默认值）。 |
| -arp | 禁止此设备响应请求。 |
| mtu value | 设置设备的最大传输单元 (MTU)。在以太网下，默认值为 1500。（参见关于千兆以太卡的表格）。 |
| netmask address | 设置接口的子网掩码。如果没有提供值，`ifconfig` 将根据 IP 地址的类计算子网掩码。A 类获取掩码 255.0.0，B 类获取 255.255.0，C 类获取 255.255.255.0。 |
| broadcast address | 设置广播地址。 |
| pointpoint | 设置点对点。 |

> 注意：这种方法也可以配置别名 IP 地址。

## 路由管理

如果你的主机连接到多个子网，你需要设置网关。

> 注意：在 Fedora 系统中，网关通常在 `/etc/sysconfig/network` 中设置。

# Linux 管理：入门指南

### Debian 类系统中的网络配置（Ubuntu, Kubuntu 等）

基于 Debian 的系统如 Ubuntu 使用不同的网络配置机制。具体来说，网络配置是通过 `/etc/network/interfaces` 文件完成的。文件的格式简单且有完善的文档。
接下来将示例 `/etc/network/interfaces` 文件中的内容。为了方便阅读，添加了行号。

1) # 回环接口
2) auto lo
3) iface inet loopback
4)
5) # 第一个网络接口 eth0
6) auto eth0
7) iface eth0 inet static
8) address 192.168.1.45
9) netmask 255.255.255.0
10) gateway 192.168.1.1
11) iface eth0:0 inet dhcp
12)
13) # 第二个网络接口 eth1
14) auto eth1
15) iface eth1 inet dhcp
16) iface eth1 inet static
17) address 2001:DB8::3
18) netmask

第一行：任何以井号 (`#`) 开头的行都是注释，会被忽略。空行也是如此。
第二行：以单词 `auto` 开头的行用于识别执行 `ifup` 命令时要启动的接口，例如此处的 `auto lo` 指向回环设备。可以在同一段落的后续行提供额外的选项。可用选项取决于族和方法。
第七行：`iface` 指令定义了正在处理的接口的物理名称。在本例中，它是 `eth0` 接口。示例中的 `iface` 指令支持 `inet` 选项，其中 `inet` 指的是地址。`inet` 支持多种方法。`loopback`（第 3 行）、`static`（第 7 行）和 `dhcp`（第 14 行）方法都是支持的。

第 8-10 行第 7 行指定的静态方法允许各种选项，如 `address`、`netmask`、`gateway` 等。这里的 `address` 选项定义接口 IP 地址 (`192.168.1.45`)，`netmask` 选项定义子网掩码 (`255.255.255.0`)，`gateway` 选项定义默认网关 (`192.168.1.1`)。

第 11 行使用的 `iface` 指令用于定义名为 `eth0:0` 的虚拟接口，该接口将使用 DHCP 配置。

第 15 行 `iface` 指令定义了正在处理的接口物理名称。在本例中，它是 `eth1` 接口。示例中的 `iface` 指令支持 `inet` 选项，即使用 `dhcp` 选项。这意味着该接口将使用 DHCP 进行动态配置。

第 16-18 行这些行为 `eth1` 接口分配了一个 IPv6 地址。本示例中分配的地址为 `2001:DB8::3`，网络掩码为 64。

在对 `interfaces` 文件进行任何更改并保存后，可以使用 `ifup` 命令启动或关闭网络接口。例如，为设备创建新条目后，你可以输入：

```
yyang@ubuntu-server:~$ sudo ifup eth1
```

要关闭 `eth1` 接口，你需要运行：

```
yyang@ubuntu-server:~$ sudo ifdown eth1
```

这里讨论的 `interfaces` 示例是一个简单的配置。`/etc/interfaces` 文件支持大量的配置选项，我们仅触及了皮毛。幸运的是，该文件的 man page（`man 5 interfaces`）有完善的文档。

# 简单用法

典型的 `route` 命令结构如下：

```
[root@serverA /root]# route cmd type addy netmask gw gway dev
```

参数如下：

| 参数 | 描述 |
| --- | --- |
| cmd | 或是 `add` 或 `del`，取决于你是要添加还是删除路由。如果你正在删除路由，唯一需要的参数是 `addy`。 |
| type | 或是 `-net` 或 `-host`，取决于 `addy` 代表的是网络地址还是路由器地址。 |
| add | 你想要为其提供路由的目标网络。 |
| netmask mask | 将 `add` 地址的网掩码设置为 `mask`。 |
| gw gateway | 设置 `add` 的路由器地址为 `gateway`。通常用于默认路由。 |
| dev dn | 将所有数据包通过 `ifconfig` 设置的网络设备 `dn` 发送。 |

在具有单个以太网设备和网关 `192.168.1.1` 网关的示例主机上设置默认路由：

```
root@serverA /root]# route add -net default gw 192.168.1.1 dev eth0
```

使用 `route` 工具程序为没有现有默认路由的系统添加默认路由，你需要：

```
root@serverA ~# ip route add default via 192.168.1.1
```

使用 `ip` 命令将默认 IPv6 路由指向地址为 `2001:db8::` 的 IPv6 网关，请输入：

```
root@serverA ~# ip -6 route add default via 2001:db8::
```

使用 `ip` 命令替换或更改主机上现有的默认路由，你会使用：

```
root@serverA ~# ip route replace default via 192.168.1.1
```

下一行命令行设置了一个主机路由，使得所有请求远程主机 `192.168.2.50` 的数据包通过第一个 PPP 设备发送：
