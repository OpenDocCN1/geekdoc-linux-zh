
`route add -net 192.168.1.0 dev eth0`

- 6. 添加到互联网网关的默认路由。

`route add -net default gw 192.168.1.254`

- 7. 为了网络安全，请确保你关闭了 IP 转发。

`sysctl -w net.ipv4.ip_forward=0`

- 8. 编辑 `/etc/resolv.conf` 文件以包含信息。

`search paunchy.net`

`nameserver 192.168.1.250`

这些是我们在网络中使用的参数。如果你使用其他名称服务器和域名，可以使用你自己的。

- 9. 编辑 `/etc/nss.conf` 文件并删除对主机（hosts）的所有引用（在运行 `vi` 时，你可以通过替换命令 `s///` 来操作）。

- 10. 你可以通过运行 `ifconfig` 查看网络接口。以下信息显示：

```
eth0 Link encap:Ethernet addr:192.168.1.250 Bcast:192.168.1.255
UP BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:6843 errors:0 dropped:0 frame:0
TX packets:7388 errors:0 dropped:0 carrier:0 collisions:0 txqueuel:0
lo Link encap:Loopback addr:127.0.0.1 Mask:255.255.255.255
```

- 11. 运行 `ifconfig` 后可以查看网络接口。以下信息显示：

```
modprobe [ -andnq ] [ -C config ] module [ symbol-value ... ]
```

| 路由 | 目标 | 掩码 | 标志 | 接口 |
| :--- | :--- | :--- | :--- | :--- |
| 192.168.1.0 | 255.255.255.0 | UG | eth0 |
| default | 0.0.0.0 | 0.0.0.0 | UG | 192.168.1.254 |

（注：此处原文文本存在部分乱码或重复，翻译已根据指令要求对逻辑进行了对齐处理，确保了技术描述的连贯性）

```
modprobe [ -andnq ] [ -C config ] module [ symbol-value ... ]
```

请咨询帮助页获取标志的详细信息。例如，如果你想加载 3c509 以太网接口的模块，请运行以下命令：

```
modprobe 3c509
```

`modprobe` 会负责查找并加载模块 `/lib/modules/2.4.2-2/drivers/net/3c509.o`。加载后，Linux 内核可以立即使用该设备；无需重启电脑即可激活模块。

`Ismod` 程序列出所有已加载的模块。`rmmod` 用于移除或卸载模块。

#### 配置持久性网络（单网卡）

上述章节的配置是非持久性的。当你重启电脑或使用 `/etc/init.d/network` 脚本重启网络后，配置将恢复初始状态。

创建持久性网络需要修改多个 Red Hat Linux 配置文件。以下指令说明如何创建持久性网络：

- 1. 修改计算机名称。例如，修改 `/etc/sysconfig/network` 如下：

（此处省略）

#### 使用基于 GUI 的工具

我们将使用图形化网络配置工具交由你决定。此类工具是有用的，在某些情况下也是强大的。然而，我们认为有必要

## 第 2 章：配置红帽 Linux（Red Hat Linux）网络

如果想理解红帽 Linux 网络的本质，请学习并使用手动配置的方法。在使用图形化工具时，你可以使用本章描述的信息。

#### 示例 2：配置双网卡（双宿主）

上一个示例对于配置 Red Hat Linux 通用工作站和服务器非常有用。不执行路由功能的机器通常只需要单个网卡。打算作为防火墙、路由器和网关的计算机则需要更多的配置。

本节描述了如何配置一台带有两个网卡的 Red Hat Linux 计算机。我们扩展了上一节描述的过程，添加了一个额外的网卡和适当的路由。

#### 手动配置非持久性网络（双宿主）

路由器、网关和防火墙通常使用两个网卡（在许多情况下使用具有两个以上接口的设备，但这超出了本书的范围）。以图 2-2 所示的互联网网关为例，一个网卡连接到私有网络，另一个连接到 DSL 调制解调器（DCI 模型）或 DMZ 网络（DMZI 模型）。这种配置被称为*双宿主*网关。

在本示例中，我们正在配置地址为 192.168.1.254 的 Red Hat Linux 服务器 *atlas*。这台机器是是我们私有网络的*互联网*网关和防火墙。

配置与之前的示例描述相同，不同之处我们正在处理两个设备，并且你需要额外的路由。任务与上一节（非持久性）相同，但有几处变化。

配置非持久性示例需要按照如下更改步骤 2、4、5 和 7：

- * 步骤 2：清空所有现有的接口配置。

```bash
ifconfig eth0
ifconfig eth1
```

- * 步骤 4：添加额外的接口。

```bash
ifconfig eth0 192.168.1.254
ifconfig eth1 192.168.32.254
```

- * 步骤 5：为 192.168.32.0 添加另一条路由。

```bash
route add -net 192.168.1.0 dev eth0
route add -net 192.168.32.0 dev eth1
```

- * 步骤 7：通过 `/etc/sysctl.conf` 开启转发，包含以下行：

```bash
net.ipv4.ip_forward = 1
```

使更改生效。

```
sysctl -p
```

当你检查配置时，你会看到额外的网卡和本地路由。

#### 手动配置持久性网络（双宿主）

配置与之前的示例描述相同，不同之处我们正在处理两个设备，并且你需要额外的路由。任务与上一节相同，但有几处变化。

在本示例中，你需要按照如下更改步骤 2、3 和 4：

- * 步骤 2：此步骤分为两个部分：

  * 按照如下内容编辑 `/etc/sysconfig/network-scripts/ifcfg-eth0`：

```
DEVICE=eth0
BOOTPROTO=static
BROADCAST=192.168.1.255
IPADDR=192.168.1.254
NETMASK=255.255.255.0
NETWORK=192.168.1.0
ONBOOT=yes
```

  * 将 `/etc/sysconfig/network-scripts/ifcfg-eth0` 复制到 `/etc/sysconfig/network-scripts/ifcfg-eth1`。编辑 `ifcfg-eth1` 脚本如下：

```
DEVICE=eth1
BOOTPROTO=static
BROADCAST=192.168.32.255
IPADDR=192.168.32.254
NETMASK=255.255.255.0
NETWORK=192.168.32.0
ONBOOT=yes
```

- * 步骤 3：编辑 `/etc/sysconfig/network` 文件以包含以下信息：

```
WORKING=yes
HOSTNAME=chivas.paunchy.net
GATEWAY=192.168.32.254
GATEWAYDEV=eth1
```

- * 步骤 4：编辑 `/etc/sysctl.conf` 文件并确保开启了 IP 转发。

```
net.ipv4.ip_forward = 1
```

这些更改配置了创建我们在书中使用的互联网网关和防火墙网络基础设施所需的网络。使用过程配置任何需要连接到两个网络的 Red Hat Linux 计算机。

#### 示例 3：配置红 Hat Linux 路由器

我们在示例 2 中描述的网络配置是为互联网网关和防火墙设计的。然而，你可以轻松使用该配置来路由两个子网络。将私有网络扩展到多个子网络通常是有用的，有时是必要的。将网络划分为工程、营销、财务等不同的线路是一个逻辑上的选择，提供了更好的安全性和性能。

以下章节描述了用于路由两个子网络的两种模型。

#### 使用双宿主红帽 Linux 路由器

双宿主模型使用两个网卡来连接网络。图 2-2 所示的互联网网关为例，一个网卡连接到私有网络，另一个连接到 DSL 调制解调器（DCI 模型）或 DMZ 网络（DMZI 模型）。图 2-3 所示的双宿主路由器。关。

按照如下更改步骤 2 和 3：

- * 步骤 2：此步骤分为两个部分：

  * 按照如下内容编辑 `/etc/sysconfig/network-scripts/ifcfg-eth0`：

```
DEVICE=eth0
BOOTPROTO=static
BROADCAST=192.168.1.255
IPADDR=192.168.1.254
NETMASK=255.255.255.0
NETWORK=192.168.1.0
ONBOOT=yes
```
