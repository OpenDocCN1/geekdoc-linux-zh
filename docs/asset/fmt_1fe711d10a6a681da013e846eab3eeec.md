
显示了各种位信息，例如网卡的 48 位硬件地址（十六进制 `00:00:e8:3b:2d:a2`）。

## 25.6 配置路由

路由表现在路由 `192.168.3.0/255.255.255.0` 至 `eth0`：

| 目的 | 网关 | 子网掩码 | 标志 | 跃 | 接口 |
|---|---|---|---|---|---|
| `127.0.0.0` | `0` | `255.0.0.0` | `U` | `1` | `lo` |
| `192.168.3.0` | | `255.255.255.0` | `U` | `0` | `eth0` |

接口现在处于激活状态。路由表现在路由 `127.0.0.0/255.0.0` 至 `lo`，显示了各种位信息。路由表现在路由 `192.168.3.0/255.255.255.0` 至 `eth0`。此输出具有含义：`127.0.0.0/255.0.0.0` `lo`, `192.168.3.0/255.255.255.0` `eth0`。路由表现在路由 `127.0.0.0/255.0.0.0` `lo`, `192.168.3.0/255.255.255.0` `eth0`。路由表现在路由 `127.0.0.0/255.0.0.0` `lo`, `192.168.3.0/255.255.255.0` `eth0`。路由表现在路由 `127.0.0.0/255.0.0.0` `lo`, `192.168.3.0/255.255.255.0` `eth0`。路由表现在路由 `127.0.0.0/255.0.0.0` `lo`, `192.168.3.0/255.255.255.0` `eth0`。路由表现在路由 `127.0.0.0/255.0.0.0` `lo`, `192.168.3.0/255.255.255.0` `eth0`。路由表现在路由 `127.0.0.0/255.0.0.0` `lo`, `192.168.3.0/255.255.255.0` `eth0`。更具体的路由根据子网码排序，更具体的路由的优先级高于不具体的路由。路由表现在路由 `127.0.0.0/255.0.0.0` `lo`, `192.168.3.0/255.255.255.0` `eth0`。

## 25.7 配置启动脚本

大多数发行版都有模块化且可扩展的启动脚本系统用于初始化网络。

### 25.7.1 RedHat 网络脚本

RedHat 系统包含 `/etc/sysconfig/` 目录，其中包含了自动启动网络的配置文件。

文件 `/etc/sysconfig/network-scripts/ifcfg-eth0` 包含：

```
DEVICE=eth0
IPADDR=192.168.3.9
NETMASK=255.255.255.0
NETWORK=192.168.3.0
BROADCAST=192.168.3.255
ONBOOT=yes
```

文件 `/etc/sysconfig/network` 包含：

```
NETWORKING=yes
HOSTNAME=cericon.cranzgot.co.za
GATEWAY=192.168.3.254
```

你可以看到，这两个文件等同于上面完成示例配置。除了 IP 之外，这两个文件可以针对各种协议采取大量的选项，但这是最常见的配置。

用于回环设备的文件 `/etc/sysconfig/network-scripts/ifcfg-lo` 会在安装时自动配置；你永远不需要编辑它。

要停止和启动网络（即启用和禁用接口及路由），请输入（括号内为替代命令）：

```
/etc/init.d/network stop
( /etc/rc.init.d/network stop )
/etc/init.d/network start
( /etc/rc.init.d/network start )
```

这将间接读取你的 `/etc/sysconfig/` 文件。你可以添加更多文件，例如为次以太网设备在 `/etc/sysconfig/network-scripts/` 下添加 `ifcfg-eth1`。例如，`ifcfg-eth1` 可以包含：

```
DEVICE=eth1
IPADDR=192.168.4.1
NETMASK=255.255.255.0
NETWORK=192.168.4.0
BROADCAST=192.168.4.255
ONBOOT=yes
```

然后运行 `echo "1" > /proc/sys/net/ipv4/ip_forward` 来启用两个接口之间的数据包转发。

### 25.7.2 Debian 网络脚本

相反，Debian 有一个目录 `/etc/network/`，其中包含一个文件 `/etc/network/interfaces`。一如既，Debian 采用了一种整洁简洁的方法（参见 `interfaces(5)`）。与上述配置相同，该文件将包含：

```
iface lo inet loopback

iface eth0 inet static
    address 192.168.3.9
    netmask 255.255.255.0
    gateway 192.168.3.254
```

文件 `/etc/network/options` 包含相同的转发（以及其他）选项：

```
ip_forward=no
spoofprotect=yes
synccookies=no
```

要停止和启动网络（即启用和禁用接口及路由），输入：

```
/etc/init.d/networking stop
/etc/init.d/networking start
```

这将间接读取你的 `/etc/network/interfaces` 文件。
实际上，`/etc/init.d/networking` 脚本仅仅运行 `ifup` 和 `ifdown` 命令。请使用 `ifup(8)`。你也可以直接运行这些命令以获得更精细的控制。
我们通过向 `/etc/network/interfaces` 文件追加内容，类似于上述 RedHat 示例来添加更多接口。Debian 的等效方法是：

```
iface lo inet loopback

iface eth0 inet static
address 192.168.3.9
netmask 255.255.255.0
gateway 192.168.3.254

iface eth1 inet static
address 192.168.4.1
netmask 255.255.255.0
```

然后在你的 `/etc/network/options` 文件中设置 `ip_forward=yes`。

最后，RedHat 通过 `/etc/sysconfig/network` 中的 `HOSTNAME=...` 行设置其主机名，而 Debian 通过文件 `/etc/hostname` 的内容进行设置，在当前情况下，该文件仅包含：

```
cericon.cranzgot.co.za
```

## 25.8 复杂路由 — 多跳示例

考虑两个需要通信的远程局域网（LAN）。每个局域网各有一台专用机器，通过某种替代方法（在本例中为永久串口线）连接，如图 25.3 所示。

这种安排可以用五台机器 `X`、`A`、`B`、`C` 和 `D` 来总结。机器 `X`、`A` 和 `B` 在子网 `192.168.1.0/26` 上形成 `LAN 1`。机器 `C` 和 `D` 在子网 `192.168.1.128/26` 上形成 `LAN 2`。请注意我们如何使用“26”来表示前 26 位是网络地址位，而剩余 6 位是主机地址位。这意味着在 `LAN 1` 和 `2` 上，我们最多有 $2^6 = 64$ 个 IP 地址。我们的专用串口链路位于 `B` 和 `C` 之间。

机器 `X` 的 IP 为 `192.168.1.1`。这台机器是通往互联网的网关。机器 `B` 的以太网口配置 IP 地址 `192.168.1.2`，默认网关为 `192.168.1.1`。注意广播地址为 `192.168.1.63`（最后 6 位均为 1）。机器 `C` 的以太网口配置 IP 地址 `192.168.1.129`，未设置默认网关。在 `B` 和 `C` 之间配置了 `192.168.1.192/26` 网络，这在实际上是一个自己的局域网，尽管只有两台机器连接。机器 `B` 和 `C` 在接口上分别拥有 `192.168.1.252` 和 `192.168.1.253` 地址。这是一个不稳定的串口链路真实示例。为了保持链路可用，需要 `p` 和 shell 脚本在链路中断时重启。机器 `B` 的脚本为：

```
#!/bin/sh

while true ; do
pppd local mru 296 mtu 299 notetach nocrts
  192.168.1.253:192.168.1.252 /dev/tty8 115200 noauth
```
