

## 红帽（Red Hat）接口配置

在 Red Hat 机器上，`/etc/sysconfig/network-scripts` 目录包含用于配置并启动和停止机器上网络接口的脚本。

例如，如果你有一个需要配置静态 IP 地址和其他设置的 `eth0` 接口，你可以选择运行 `netconfig`（`redhat-config-network-*` 实用工具之一），或者直接编辑这些文件本身。图 17.4 展示了 `netconfig` 命令的界面。这些实用工具本身就足够完善（且不出现在考试中），因此我们来讨论如何通过编辑文件来配置接口。

![](img/49f4f38f3aec011238fa50f89e643db3_460_0.png)

> Red Hat 在 Red Hat Linux 各个版本中包含的图形化实用工具均不在考试测试范围内，考试对于配置接口的实用工具提及的范围仅限于文件编辑以及可能的 **netconfig**。

要查看 *ifcfg-eth0* 文件，你可以使用以下命令：

```bash
cat /etc/sysconfig/network-scripts/ifcfg-eth0
```

如果是静态配置，你看到的输出类似于：

```text
DEVICE=eth0
ONBOOT=yes
BOOTPROTO=static
IPADDR=192.168.1.73
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
```

如果接口配置为 DHCP，你看到的输出类似于：

```text
DEVICE=eth0
ONBOOT=yes
BOOTPROTO=dhcp
```

无论你决定使用哪种方法，都可以通过编辑此文件并设置所需的参数来实现。这些参数是自解释的，除了 **BOOTPROTO** 参数可能例外。**BOOTPROTO** 参数设置为 static 或 dhcp 时，会告诉网络守护程序如何配置此接口：是通过读取 *ifcfg-eth0* 文件中的其他参数，还是使用 DHCP 获取地址。

## Debian 接口配置

Debian 使用不同的接口配置风格：Debian 没有使用多个较小的脚本或配置文件，而是使用 `/etc/network/interfaces` 文件来管理所有接口。尽管 Debian 默认不包含 `netconf` 实用工具，但某些 Debian 发行版包含了 `netcardconfig` 程序，它大致执行相同的功能。

要查看此文件的内容，请使用以下命令：

```bash
cat /etc/network/interfaces
```

这将产生类似于以下内容的输出：

```text
# /etc/network/interfaces - configuration file for ifup(8), ifdown(8)
# The loopback interface
# automatically added when upgrading
auto lo eth0
iface lo inet loopback
iface eth0 inet static
    address 192.168.15.5
    netmask 255.255.255.0
    network 192.168.15.0
    broadcast 192.168.15.255
    gateway 192.168.15.2
```

接口文件中定义的每个接口都以关键字 `iface` 开头，随后是接口名称、地址类型（inet 代表 IP，ipx 代表 IPX，inet6 代表 IPv6），最后是接口的方法（static 或 dhcp）。

在配置好接口的正确参数后，建议使用此处所示的命令重启网络守护程序：

```bash
/etc/init.d/networking restart
```

这会重启网络服务，并使接口停止后再重新启动。

> **警告** 请注意，Debian 的接口文件包含网关地址，但并不像 Red Hat 那样使用大写字母。此外，Debian 的接口文件在参数和值之间不使用等号（=）。Debian 还将脚本用作输入或源文件，而 Red Hat 则是实际执行其配置脚本。

> **注意** 需要注意的是，尽管 Debian 主要使用上述方法，但在 Debian 机器上经常可以发现 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件的实例。你需要阅读你的发行版或方法的文档，以确定两者之间的关系。你可以放心地假设这不会成为考试中的问题。

## 查看和配置网关地址

默认网关用于将流量发送到作为你其他网络入口或网关的接口，因此得名。默认网关是必要的，因为你不想在所有机器上都为每个目标网络配置静态路由——那将很繁琐且很快就会过时。

### 查看默认网关

要查看机器上配置的默认网关，你可以使用 **route** 命令或以下命令：

```bash
netstat -r
```

这将显示类似于以下的输出：

```text
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
192.168.1.0     *               255.255.255.0   U         40  0       0      eth0
127.0.0.0       *               255.0.0.0       U         40  0       0      lo
default         192.168.1.2     0.0.0.0         UG        40  0       0      eth0
```

这是一组重要的输出。如果没有正确配置的默认网关，你的机器只能访问本地网络上的主机。

以 **192.168.1.0** 开头的那一行是你子网或网络的实际网络地址。输出中会出现一个位于同一网络上的地址，它代表提供网关功能的路由器的实际 IP；在这种情况下，它位于最后一行，即 **192.168.1.2**。

![](img/49f4f38f3aec011238fa50f89e643db3_462_0.png)

警惕任何试图让你误以为网关的实际 IP 是 0.0.0.0 的问题或答案。事实并非如此；那只是 IP 寻址方案在你查找未配置路由的目标网络时用来表示默认网关的方法。

### 配置默认网关

正如你在 Red Hat 和 Debian 的配置文件中看到的，有效的 **GATEWAY** 或 **gateway** 参数以及一个 IP 值可以为接口配置有效的网关。

在 Red Hat 机器上，你可以编辑 `/etc/sysconfig/network` 文件或 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件，并添加 **GATEWAY** 条目：

```text
GATEWAY=10.0.0.1
```

Debian 使用实际的 `/etc/network/interfaces` 文件来设置每个接口的网关值。

在两种类型的系统上，你都可以使用以下命令手动添加默认网关：

```bash
route add default gw 10.0.0.1
```

逐行注意上一个命令的语法是非常重要的：

- `route`—`route` 命令，用于许多与建立、查看和删除到其他网络的路由相关的事情。
- `add`—用于添加默认网关。其他选项包括 `del`，用于删除特定路由。
- `default`—默认网关是在没有其他路由存在或不匹配目标地址时使用的路由。
- `gw`—表示该条目是通往其他网络的网关，流量应通过此接口路由。
- `10.0.0.1`—替换为你的网关地址，或提供此功能的主机的可解析域名。

> 预计会出现关于默认网关的故障排除、配置或填空题。这类问题在考试中会出现好几次，形式可能为填空或多选题（有时两者都有），表述略有不同。

## 本地名称配置

本地名称配置是不同文件的大杂烩，其中最重要的是：

- `/etc/hosts`
- `/etc/resolv.conf`
- `/etc/nsswitch.conf`

这三个文件用于配置本地名称解析是如何发生的。图 17.5 展示了这些文件之间的关系，以及它们如何相互使用来解析客户端软件应用需要连接的主机的名称。

