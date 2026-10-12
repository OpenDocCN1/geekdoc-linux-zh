
`echo "1" /proc/sys/net/ipv4/ip_forward` 将启用该功能。

`echo "0" /proc/sys/net/ipv4/ip_forward` 将再次禁用它。

由于其巨大的实用性，我们将在讨论 `/proc` 中可以找到的信息，以及通过修改本书内容可以采取的操作。

1. 您可以将模块名称添加到 `/etc/modules` 中。由于那里列出的模块将按顺序加载，因此在填充此文件时，请注意哪个模块代表 `eth0`，哪个代表 `eth1`。

2. 您可以向 `modules.conf` 文件添加一条别名行（alias line）。该行将类似 `eth0` 这样的设备名称与模块名称关联起来。当内核需要该设备时，它将尝试加载指定的模块。您还可以在加载时指定该模块所需的选项。对于本章早期初始化的三块网卡，该文件中的条目如下：

```
alias eth0 epro100
alias eth1 natsemi
options natsemi=2 full_duplex=1
alias eth2 pcnet32
```

3. 您可以在自己的自定义网络启动脚本中显式加载模块。第 72 页提供了一个示例脚本。

- 我们为每个网络接口配置了适当的静态 IP 地址。配置网卡的操作会自动向内核路由表添加适当的网络路由。在您的系统上实现此操作取决于发行版，这就是为什么我们要坚持使用自己编写的网络启动脚本的原因。

- 我们通过将 `/proc/sys/net/ipv4/ip_forward` 的值设置为 `1`，指示内核在接口之间转发数据包。再次强调，如何使此更改永久取决于您的发行版。无论如何，知道如何手动操作总是比较好的。

## Debian 中的基础网络配置

上述配置可以在 Debian 2.2（或更高版本）系统上通过以下方式实现：

- 将所需的模块添加到 `/etc/modules` 或 `/etc/modules.conf`。

- 编辑 `/etc/network/interfaces` 以配置接口的 IP 设置。

```
auto eth0 eth1
iface eth0 static
      address 192.168.16.1
      netmask 255.255.255.0
      network 192.168.16.0
      broadcast 192.168.16.255
iface eth1 static
      address 192.168.18.1
      netmask 255.255.255.0
      network 192.168.18.0
      broadcast 192.168.18.255
```

然后，您可以使用 `ifup ethx` 和 `ifdown ethx` 来配置接口的开启和关闭，或者使用 `/etc/init.d/networking [start|stop]` 来启动/停止整个子系统。可以在文件中指定其他选项 - 请查看 `interfaces` 的 man 手册。

- `/proc/sys/net/ipv4/ip_forward` 的值由 `/etc/network/options` 中 `ip_forward` 参数设置控制。

由于我们是路由器管理员而不是工作站高手，我相信我们足够足够将所有的网络配置保留在自己的脚本中。这意味着禁用了发行版特定的网络启动，但给了我们对该过程的完全控制。到目前为止，硬件配置的版本看起来如下：

```
#!/bin/sh
#
# /etc/init.d/local_network
#
# 修改历史：
# 19990213/tm 为新硬件盒完成全新的重写
# 20000417/tm 为 2.2 内核修改：不再需要添加网络路由
# - 它们由 ifconfig 自动添加
############################################################################################
```

## 3.1 配置局域网路由器

### `Intf_up()`
