

# Red Hat 网络配置

表 14.7 /etc/sysconfig/network 下的 SUSE 网络配置文件

| 文件 | 在此设置的内容 |
| --- | --- |
| ifcfg-interface | 主机名、IP 地址、子网掩码等 |
| ifroute-interface | 特定接口的路由定义 |
| routes | 所有接口的默认路由和静态路由 |
| config | 许多较少使用的网络变量 |

除了 DNS 参数和系统主机名外，SUSE 将大多数网络选项设置在 `/etc/sysconfig/network` 目录下的 `ifcfg-interface` 文件中。系统中的每个接口都应该有一个此类文件。

除了为接口指定 IP 地址、网关和广播信息外，`ifcfg-*` 文件还可以调整许多网络细节。请查看 `ifcfg.template` 以获取可能参数的详细注释说明。以下是一个简单的示例：

```
PROTO='static' # 隐含为静态，但冗余一些并无害。
IPADDR='192.168.1.24' # /24 定义了 NETWORK 和 NETMASK 变量
NAME='AMD PCnet - Fast 79C91' # 用于启动和停止接口。
STARTMODE='auto' # 启动时启动
USERCONTROL='no' # 禁止通过互联网/netminer GUI 进行控制
```

SUSE 系统的全局静态路由信息（包括默认路由）存储在 `routes` 文件中。该文件中的每一行都像路由命令，但省略了选项名称，并包含存储在路由表中以供路由守护进程使用的。对于上述配置的主机（它只有默认路由）在路由表中存储以供其使用的额外参数，`routes` 文件包含以下行：

```
default 192.168.1.254 -
```

指向特定接口的路由保留在 `ifroute-interface` 文件中，其中接口组件的命名法与 `ifcfg-*` 文件相同。其内容与 `routes` 文件格式相同。

# Red Hat 网络配置

Red Hat 的网络配置 GUI 也是 `system-config-network`；它也可以通过“系统->管理”菜单下的网络名称进行访问。该工具提供了一个用于配置单个网络接口和静态路由的 UI。它还具有用于设置 IPsec 隧道、配置 DNS 和添加 `/etc/hosts` 条目的面板。

表 14.8 显示了此 GUI 编辑的底层配置文件。

你在 `/etc/sysconfig/network` 中设置机器主机名，该文件还包含指定机器 DNS 域和默认网关的行。

![](img/579efec8c67772f31ecf34844bbb71a2_535_0.png)

# 第 14 章 TCP/IP 网络连接

**表 14.8 /etc/sysconfig 下的 Red Hat 网络配置文件**

| 文件 | 在此设置的内容 |
|---|---|
| network static-routes | 主机名、默认路由、静态路由 |
| network-scripts/ifcfg-ifname | 接口特定参数：IP 地址、子网掩码等 |

例如，这里是一个具有单个以太网接口的主机的**网络文件**：

```
NETWORKING=yes
NETWORKING_IPV6=no
HOSTNAME=redhat.toadranch
DOMAINNAME=toadranch ### 可选
WAY=192.168.1.254
```

接口特定数据存储在 `/etc/sysconfig/network-scripts/ifcfg-ifname` 中，其中 *ifname* 是网络接口的名称。这些配置文件设置了每个接口的 IP 地址、子网掩码和广播地址。它们还包含一行，指定接口在启动时是否应配置为“启用（up）”。

通用名称具有对应以太网接口（eth0）和环回接口（lo）的文件。例如，

```
DEVICE=eth0
ADDR=192.168.1.13
NETMASK=255.255.255.0
NETWORK=192.168.1.0
BROADCAST=192.168.1.255
ONBOOT=yes
```

以及

```
DEVICE=lo
ADDR=127.0.0.1
NETMASK=255.0.0.0
NETWORK=127.0.0.0
BROADCAST=127.255.255
ONBOOT=yes
NAME=loopback
```

是上述 redhat.toadranch 机器的 **ifcfg-eth0** 和 **ifcfg-lo**。eth0 的基于 DHCP 的设置更为简单：

```
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
```

在更改 `/etc/sysconfig` 中的配置信息后，对相应接口运行 *ifdown ifname* 然后再运行 *ifup ifname*。如果你一次重新配置多个接口，可以使用命令 *service network restart* 来重置所有（这实际上是运行 /etc/rc.d/network 的简写，该脚本在启动时被调用）。启动脚本还可以配置静态路由。任何添加到文件 `/etc/sysconfig/static-routes` 的路由都会在启动时输入到路由表中。这些条目指定了路由添加，尽管顺序不同：

```
eth0 130.225.0.0 netmask 255.255.255.0 gw 130.225.0.1
eth1 192.168.8.0
```

指向特定接口的路由保留在 `ifroute-interface` 文件中，其中接口组件的命名法与 `ifcfg-*` 文件相同。其内容与 `routes` 文件格式相同。

对于上述 redhat.toadranch 机器，**ifcfg-eth0** 和 **ifcfg-lo** 如下。eth0 的基于 DHCP 的设置更为简单：

```
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
```

在更改 `/etc/sysconfig` 中的配置信息后，对相应接口运行 *ifdown ifname* 然后再运行 *ifup ifname*。如果你一次重新配置多个接口，可以使用命令 *service network restart* 来重置所有（这实际上是运行 /etc/rc.d/network 的简写，该脚本在启动时被调用）。启动脚本还可以配置静态路由。任何添加到文件 `/etc/sysconfig/static-routes` 的路由都会在启动时输入到路由表中。这些条目指定了路由添加，尽管顺序不同：

```
eth0 130.225.0.0 netmask 255.255.255.0 gw 130.225.0.1
eth1 192.168.8.0
```

SUSE 系统的全局静态路由信息（包括默认路由）存储在 `routes` 文件中。该文件中的每一行都像路由命令，但省略了选项名称，并包含存储在路由表中以供路由守护进程使用的。对于上述配置的主机（它只有默认路由）在路由表中存储以供其使用的额外参数，`routes` 文件包含以下行：

```
default 192.168.1.254 -
```

指向特定接口的路由保留在 `ifroute-interface` 文件中，其中接口组件的命名法与 `ifcfg-*` 文件相同。其内容与 `routes` 文件格式相同。

除了 DNS 参数和系统主机名外，SUSE 将大多数网络选项设置在 `/etc/sysconfig/network` 目录下的 `ifcfg-interface` 文件中。系统中的每个接口都应该有一个此类文件。

除了为接口指定 IP 地址、网关和广播信息外，`ifcfg-*` 文件还可以调整许多网络细节。请查看 `ifcfg.template` 以获取可能参数的详细注释说明。以下是一个简单的示例：

```
PROTO='static' # 隐含为静态，但冗余一些并无害。
IPADDR='192.168.1.24' # /24 定义了 NETWORK 和 NETMASK 变量
NAME='AMD PCnet - Fast 79C91' # 用于启动和停止接口。
STARTMODE='auto' # 启动时启动
USERCONTROL='no' # 禁止通过互联网/netminer GUI 进行控制
```

SUSE 系统的全局静态路由信息（包括默认路由）存储在 `routes` 文件中。该文件中的每一行都像路由命令，但省略了选项名称，并包含存储在路由表中以供路由守护进程使用的。对于上述配置的主机（它只有默认路由）在路由表中存储以供其使用的额外参数，`routes` 文件包含以下行：

```
default 192.168.1.254 -
```

指向特定接口的路由保留在 `ifroute-interface` 文件中，其中接口组件的命名法与 `ifcfg-*` 文件相同。其内容与 `routes` 文件格式相同。

# Red Hat 网络配置

Red Hat 的网络配置 GUI 也是 `system-config-network`；它也可以通过“系统->管理”菜单下的网络名称进行访问。该工具提供了一个用于配置单个网络接口和静态路由的 UI。它还具有用于设置 IPsec 隧道、配置 DNS 和添加 `/etc/hosts` 条目的面板。

表 14.8 显示了此 GUI 编辑的底层配置文件。

你在 `/etc/sysconfig/network` 中设置机器主机名，该文件还包含指定机器 DNS 域和默认网关的行。

![](img/579efec8c67772f31ecf34844bbb71a2_535_0.png)

# 第 14 章 TCP/IP 网络连接

**表 14.8 /etc/sysconfig 下的 Red Hat 网络配置文件**

| 文件 | 在此设置的内容 |
|---|---|
| network static-routes | 主机名、默认路由、静态路由 |
| network-scripts/ifcfg-ifname | 接口特定参数：IP 地址、子网掩码等 |

例如，这里是一个具有单个以太网接口的主机的**网络文件**：

```
NETWORKING=yes
NETWORKING_IPV6=no
HOSTNAME=redhat.toadranch
DOMAINNAME=toadranch ### 可选
WAY=192.168.1.254
```

接口特定数据存储在 `/etc/sysconfig/network-scripts/ifcfg-ifname` 中，其中 *ifname* 是网络接口的名称。这些配置文件设置了每个接口的 IP 地址、子网掩码和广播地址。它们还包含一行，指定接口在启动时是否应配置为“启用（up）”。

通用名称具有对应以太网接口（eth0）和环回接口（lo）的文件。例如，

```
DEVICE=eth0
ADDR=192.168.1.13
NETMASK=255.255.255.0
NETWORK=192.168.1.0
BROADCAST=192.168.1.255
ONBOOT=yes
```

以及

```
DEVICE=lo
ADDR=127.0.0.1
NETMASK=255.0.0.0
NETWORK=127.0.0.0
BROADCAST=127.255.255
ONBOOT=yes
NAME=loopback
```

是上述 redhat.toadranch 机器的 **ifcfg-eth0** 和 **ifcfg-lo**。eth0 的基于 DHCP 的设置更为简单：

```
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
```

在更改 `/etc/sysconfig` 中的配置信息后，对相应接口运行 *ifdown ifname* 然后再运行 *ifup ifname*。如果你一次重新配置多个接口，可以使用命令 *service network restart* 来重置所有（这实际上是运行 /etc/rc.d/network 的简写，该脚本在启动时被调用）。启动脚本还可以配置静态路由。任何添加到文件 `/etc/sysconfig/static-routes` 的路由都会在启动时输入到路由表中。这些条目指定了路由添加，尽管顺序不同：

```
eth0 130.225.0.0 netmask 255.255.255.0 gw 130.225.0.1
eth1 192.168.8.0
```

