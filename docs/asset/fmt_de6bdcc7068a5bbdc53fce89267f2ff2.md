
| 文件 | 描述 |
|---|---|
| aliases | 邮件别名，Sendmail 使用 |
| ethers | 以太网数字 |
| group | 用户组 |
| hosts | 主机名和数字 |
| netgroup | 网络范围的主机用户列表，用于访问规则；glibc 2.1 之前的 C 库通过 NIS 支持 netgroup |
| network | 网络名称和数字 |
| passwd | 用户密码 |
| protocols | 网络协议 |
| publickey | 使用 NFS 和 NIS+ 的 SecureRPC 公钥和密钥 |
| rpc | 远程过程调用名称和数字 |
| services | 网络服务 |
| shadow | 影子用户密码 |

**表 32-8：NSS 支持的文件**

动作项指定了特定服务的的操作。动作项放在服务后面的括号内。配置规范可以列出多个服务，每个服务都有其自己的动作项。在下例中，`network` 文件的条目的配置规范说明要检查 `nisplus` 服务，如果未找到，则检查 `/etc/protocols` 文件：

```
protocols: nisplus [NOTFOUND=return] files
```

## 第 32 章：管理 TCP/IP 网络

操作项（action item）由状态和一个动作组成。状态持有服务查找的可能结果，动作是在状态为真时执行的操作。目前，可能的状态值为 `SUCCESS`（成功）、`NOTFOUND`（未找到）、`UNAVA`（不可可用）和 `TRYAGAIN`（服务临时不可用）。可能的动作有 `return`（返回）和 `continue`（继续）：`return` 会停止配置文件的查找过程，继续到下一个列出的服务。在前面的示例中，如果在 NIS 中未找到记录，查找过程将结束。

| 服务 | 描述 |
| --- | --- |
| files | 检查相应的 `/etc` 文件以获取配置（例如，用于 hosts 的 `/etc/hosts`）；此服务适用于所有文件 |
| db | 检查相应的 `/var/db` 数据库以获取配置；除 netgroup 以外的所有文件均有效 |
| compat | 仅适用于 passwd、group 和 shadow 文件 |
| dns | 检查 DNS 服务；仅适用于 hosts 文件 |
| nis | 检查 NIS 服务；适用于所有文件 |
| nisplus | NIS 第 3 版本 |
| hesiod | 使用 Hesiod 进行查找 |

表 32-9：NSS 配置服务

此处显示 `/etc/nswitch.conf` 文件的副本，它列出了常用的条目。注释和被注释的条目以 `#` 号开头：

```
# /etc/nswitch.conf

#

# /etc/nswitch.conf

#

# 一个名称服务切换器配置文件示例。

passwd: db files nisplus nis

shadow: db files nisplus nis

group: db files nisplus nis

hosts: files nisplus dns

bootparams: nisplus [NOTFOUND=return] files

ethers: files

netmasks: files

networks: files

protocols: files

rpc: files

services: files

netgroup: files nis

publickey: nisplus

automount: files nis

alias: files nis
```

## 网络接口与路由：ifconfig 和 route

你的系统通过特定的硬件接口（如以太网卡或调制解调器）连接到网络。通过此接口传输的数据会被路由到你的网络。`ifconfig` 命令配置你的网络接口，而 `route` 命令据此设置连接。如果你使用配置工具（如 `system-config-network`）配置网络，则不需要使用 `ifconfig` 或 `route`。但是，你可以直接使用 `ifconfig` 和 `route` 配置接口。每每次启动系统时，都必须建立网络接口及其路由。这在启动机时由 `/etc/rc.d/init.d` 文件为每个接口执行 `ifconfig` 和 `route` 命令自动完成的，该文件在每次启动系统时都会执行。如果你手动添加接口，则必须设置网络脚本来为你的接口执行 `ifconfig` 和 `route` 操作。

## 网络启动脚本：/etc/rc.d/init.d/network

你的网络接口使用 `/etc/rc.d/init.d` 目录启动。该脚本将激活你的网络网卡（NIC），并实施网关、主机和 DNS 服务器标识等配置信息。你可以使用此脚本以及 `restart`、`start` 或 `stop` 选项，以及 `system-config-services` 手动关闭和启动网络接口。你可以使用 `service` 命令运行该脚本。以下命令将关闭并启动你的网络接口：

```
service network stop
service network start
```

如果你正在更改网络配置，将必须重启网络接口使更改生效：

```
service network restart
```

要测试接口是否正常，请使用 `ping` 命令配合网络上某个系统的 IP 地址（例如你的网关机器）。`ping` 命令会持续重复直到你用 CTRL-C 停止它。

```
ping 192.168.0.1
```

## 接口配置脚本：/etc/sysconfig/network-scripts

`/etc/rc.d/init.d` 文件通过执行位于 `/etc/sysconfig/network-scripts` 目录下的专用脚本执行启动操作。网络脚本使用目录下名为 `ifup` 的脚本来激活网络连接，使用 `ifdown` 将其关闭；正在处理的 `ifup` 类型包括用于使用 PPP 协议的调制解调器的 `ifup-ppp`，或用于使用 IP 协议第 6 版本地址的网络设备的 `ifup-ipv6`。

注意：你可以通过 System | Administration | Network 访问 `system-config-network` 来激活和停用网络接口。

`ifup` 和 `ifdown` 脚本使用了与当前配置的网络接口同名的接口配置文件，例如用于第一个以太网设备的 `ifcfg-eth0`。这些文件定义了 shell 变量，用于持有接口信息，例如是否在启动时启动它们。例如，`ifcfg-eth0` 文件包含了 `NETWORK`、`BROADCAST` 和 `IPADDR` 的定义，这些被分配给设备使用的网络、广播和 IP 地址。

`ifdown` 和 `ifup` 脚本反过来持有 `ifconfig` 和 `route` 命令，使用在接口配置文件中定义的这些变量来激活脚本。如果你想用 `ifup` 手动启动接口，只需将接口配置文件作为其参数即可。以下命令启动第二块以太网卡：

```
cd /etc/sysconfig/network-scripts
ifup ifcfg-eth0
```

当你配置网络连接时，会自动生成接口配置文件，例如使用 Red Hat 和 Fedora 的 `system-config-network` 管理工具。你也可以手动编辑这些接口配置文件，进行诸如是否启动接口之类的更改。

```
# /sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
BOOTPROTO=static
BROADCAST=192.168.0.255
IPADDR=192.168.0.1
NETMASK=255.255.255.0
ONBOOT=yes
```

```
# /sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
BOOTPROTO=dhcp
BROADCAST=192.168.0.255
IPADDR=192.168.0.1
NETMASK=255.255.255.0
ONBOOT=yes
```

```
# /sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
BOOTPROTO=dhcp
BROADCAST=192.168.0.255
IPADDR=192.168.0.1
NETMASK=255.255.255.0
ONBOOT=yes
```

```
# /sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
BOOTPROTO=static
BROADCAST=192.168.0.255
IPADDR=192.168.0.1
NETMASK=255.255.255.0
ONBOOT=yes
```

`ifconfig` 命令以接口名称和各种选项为参数。`ifconfig` 命令的格式如下：

```
ifconfig eth0 192.168.0.1
```

`ifconfig` 命令的格式如下：

```
ifconfig eth0 down
```

### ifconfig

`up` 和 `down` 激活和停用接口。示例中，`ifconfig` 为：

```
ifconfig eth0 192.168.0.1
```

| 选项 | 描述 |
| --- | --- |
| Interface | 网络接口名称，例如用于以太设备的 `eth0` 或用于 PPP设备的 `ppp0` |
| up | 激活接口；如果指定了 IP 地址则隐含 |
| down | 停用接口 |
| all | 开启或关闭混杂模式；前面的 (-) 关闭，这允许网络监控 |
| mtu | 此接口上每次传输的最大字节数 |
| daddr | 点对点连接的目标 IP 地址 |
| netmask | 掩码；前面的 (-) 关闭 |
| broadcast | 广播地址；前面的 (-) 关闭 |
| point-to-point | 接口的点对点模式；如果包含地址 |
| hw | 设置接口的硬件地址 |
| Address | 分配给接口的 IP 地址 |

表 32-10：ifconfig 选项

对于这种简单的配置，`ifconfig` 会自动生成标准的广播地址和掩码。标准广播地址是主机地址加上 255。对于 C 类网络，掩码是 `255.255.255.0`，而对于 A 类网络，标准掩码是 `255.0.0.0`。如果你连接到具有特定掩码和广播地址的网络，在使用 `ifconfig` 时指定它们。指定广播地址的选项是 `broadcast`；网络掩码的选项是 `netmask`。表 32-10 列出了不同的 `ifconfig` 选项。示例中，`ifconfig` 包含了掩码和广播地址：

```
ifconfig eth0 192.168.0.1 broadcast 192.168.0.255 netmask 255.255.255.0
```

配置接口后，你可以使用 `ifconfig` 的 `up` 选项激活它，使用 `down` 选项停用它。如果你在 `ifconfig` 操作中指定了 IP 地址，在前面的示例中，该选项是隐含的：

```
ifconfig eth0
```

并行 IP (`PLIP`)、线路 IP (`SLIP`) 和点对点协议 (`PPP`) 等点对点接口需要你指示 `pointpoint` 选项。`PLIP` 接口名称使用带有地址的 `pip` 来标识。例如，`plip0` 是第一个接口。`SLIP` 接口使用 `slip0`。`PPP` 接口以 `ppp0` 开头。点对点接口是

## 第 32 章：TCP/IP 网络管理

这些通常运行在两个主机之间，例如通过调制解调器连接的两台计算机。当你指定点点（point-point）接口选项时，你需要包含主机的 IP 地址。在下一个示例中，配置了一个 `PLIP` 接口，将 IP 地址为 `192.168.1.72` 的计算机与 IP 为 `204.166.254.14` 的计算机连接起来。如果 `/etc/hosts` 文件中列出了这些系统的域名地址，则可以使用这些域名来代替 IP 地址。

```
ifconfig pip0 192.168.1.72 point-point 204.166.254.14
```

如果需要，你也可以使用 `ifconfig` 来配置环回设备（loopback device）。环回设备的名称为 `lo`，其 IP 地址是特殊地址 `127.0.0.1`。以下示例显示了配置方法：

```
ifconfig lo 127.0.0.1
```

`ifconfig` 命令用于检查接口状态。如果你输入带有接口名称的 `ifconfig` 命令，将显示有关该接口的信息：

```
ifconfig eth0
```

要查看你的环回接口是否已配置，可以使用带有环回接口名称 `lo` 的 `ifconfig`：

## 路由

传输中的数据包会通过特定的路由到达目的地。在大型网络中，数据包从一台计算机传输到另一台计算机，直到到达目标计算机。路由决定了进程从哪里开始，以及你的系统需要将数据包发送到哪台计算机以到达目的地。在小型网络中，路由可能是静态的——也就是说，从一个系统到另一个系统的路由是固定的。人们知道如何通过固定的路径到达另一个系统。然而，在较大的网络和互联网上，路由是动态的。你的系统知道首先将数据包发送给哪台计算机，然后该计算机接收数据包并将其传递给另一台计算机，再由该计算机决定传递到哪里。对于动态路由，你的系统需要的很少。然而，静态路由可能会变得复杂，因为你必须跟踪所有的网络连接。

你的路由列在 `/proc/net/route` 文件的路由表中。要显示路由表，输入不带参数的 `route`；`netstat -r` 命令也会显示路由表：

```
$ route
Kernel routing table      Destination Gateway Flags Metric Ref Use Iface
192.168.0.0         255.255.255.0 U      0      0      eth0
127.0.0.0         *   255.255.255.0 U      0      0      lo
default               192.168.0.1     0.0.0.0  UG     0      0      eth0
```

路由表中的每个条目都有多个字段，提供如路由目的和使用的接口类型的信息。不同的字段列在表 32-11 中。

| 字段 | 说明 |
| --- | --- |
| Destination | 路由目的 IP 地址 |
| Gateway | 使用的网关 IP 地址或主机名；* 表示不使用网关 |
| Genmask | 路由的子网掩码 |
| Flags | 路由类型：U = 启用(up), H = 主机(host), G = 动态(dynamic), M = 已修改(modified) |
| Metric | 路由的指标成本 |
| Ref | 依赖于此路由的路由数量 |
| Window | AX.25 网络的 TCP 窗口 |
| Use | 使用次数 |
| Iface | 此路由使用的接口类型 |

表 32-11：路由表条目

使用 `add` 参数，你可以通过 `-net` 选项为网络添加路由，或通过 `-host` 选项为 IP 接口（主机）添加路由。`-host` 选项是默认选项。此外，你可以指定多个参数，例如子网掩码（`netmask`）、网关（`gw`）、接口（`dev`）以及默认路由（`default`）。如果你的系统上有多个 IP 接口（多个以太网卡），必须使用 `dev` 参数指定接口名称。如果你的网络有网关，使用 `gw` 参数指定默认路由。如果你的系统连接到网络，路由表中至少有一个指定默认路由的条目。这是当没有其他路由条目时数据包所走的路由。以下示例是一个以太网接口的路由：

```
route add 192.168.1.2 dev eth0
```

如果你的系统只有一个以太网设备作为 IP 接口，你可以：

```
route add 192.168.1.2
```

你可以通过调用带有 `del` 参数和该路由 IP 地址的 `ifconfig` 来删除任何路由，例如：

```
route del 192.168.1.2
```

对于网关，首先为网关接口添加路由，然后指定其为网关。此示例中的网关接口地址为 `192.168.1.1`：

```
route add 192.168.1.1
route default gw 192.168.1.1
```

如果你使用网关访问子网，添加该网络的地址（在本示例中为 `192.168.23.0`）：

```
route add -net 192.168.23.0 gw eth0
```

要为系统的不同接口添加另一个 IP 地址，使用新 IP 地址的 `ifconfig` 和 `route` 命令。以下命令为第二个以太网卡（`eth1`）配置 IP 地址 `192.168.1.3`：

```
ifconfig eth1 192.168.1.3
route add 192.168.1.3 dev eth1
```

## IP 别名 (Aliasing)

在某些情况下，你可能希望为一个接口的 Linux 系统分配两个或多个 IP 地址。例如，你可能希望在同一个网络上通过不同的 IP 地址运行不同的网站。实际上，你正在为系统设置一个可以访问的别名；这被称为 IP 别名，允许你设置多个基于 IP 的主机（或每个接口上设置多个）。请参考第 21 和 22 章的 FTP 和 Web 服务器信息，以及第 30 章的域名服务。
