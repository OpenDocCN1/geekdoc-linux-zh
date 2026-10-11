
```
DEVICE=eth1
HWADDR=00:1B:21:0A:E8:5E
TYPE=Ethernet
BOOTPROTO=none
ONBOOT=yes
NM_CONTROLLED=no
USERCTL=no
IPADDR=192.168.0.140
NETMASK=255.255.255.0
GATEWAY=192.168.0.1
```

# 第 14 章：网络管理

在 `ifcfg-eth1` 示例中，因为是静态设置地址或其他信息，因此 `BOOTPROTO` 被设置为 `none`。需要其他设置来配置通常从 DHCP 服务器获取的地址信息。在此种情况下，IP 地址被设置为 `192.168.0.140`，掩码为 `255.255.255.0`。`GATEWAY=192.168.0.1` 标识了连接互联网的路由器地址。

如果你对 `ifcfg-checks` 中使用的其他设置感兴趣，可以查看 `/usr/share/doc/initscripts-*` 目录下的 `sysconfig.txt` 文件。以下是可能让你感兴趣的几个设置：

- `PEERDNS`——设置 `PEERDNS=no` 可以防止 DHCP 覆盖 `/etc/resolv.conf` 文件。这允许你设置系统使用的 DNS 服务器，而不用担心由 DHCP 服务器提供的信息被擦除。
- `DNS`——如果 `ifcfg` 文件由 NetworkManager 管理，它将使用 DNS 条目设置 DNS 服务器的地址。例如，`DNS1=192.168.0.2` 会导致该 IP 地址被写入 `/etc/resolv.conf`。你可以有多个 DNS 条目（`DNS2=`、`DNS3=` 等）。

一旦创建了 `ifcfg-*` 文件，你就可以使用 `ifup` 和 `ifdown` 命令单独启动或停止接口，而不是同时启动或停止所有接口。例如，你可以使用以下命令启动和停止 `lo` (`ifcfg-lo`) 接口：

```
# ifdown lo
# ifconfig
# ifup lo
# ifconfig
```

刚刚显示的命令关闭了回环网络接口（`ifdown lo`），然后让你看到它处于未激活状态（`ifconfig`）。之后，你再次将其开启（`ifup lo`），并检查它是否已开启（`ifconfig`）。

除了配置主网络接口外，你可以在 `/etc/sysconfig/network-scripts` 目录中创建文件，用于别名（同一接口的多个 IP 地址）、绑定接口（在同一地址监听的多个网卡）和自定义路由。这些将在本节后面进行介绍。

## 其他网络文件

除了网络接口文件外，还有其他可以编辑以配置 Linux 网络配置文件。以下是其中：

```
/etc/sysconfig/network file
```

与本地网络相关的系统级设置可以包含在 `/etc/sysconfig/network` 文件中。系统的主机名通常在此文件中设置，但也可以在该文件中添加其他设置。以下是 `/etc/sysconfig/network` 文件内容的示例：

```
NETWORKWORKING=yes
HOSTNAME=abc.example.com
GATEWAY=192.168.0.1
```

# 第四部分：成为 Linux 服务器管理员

默认情况下，`host` 命令为 DNS 查询产生更简单的输出。它会显示 Redhat.com 的 IP 地址以及为 Redhat.com 邮件服务器（MX 记录）名称。`dig` 命令显示的信息与存储 DNS 记录的文件显示的内容类似。输出中的 `QUESTION` 部分显示了所请求 Redhat.com 地址的地址部分，而 `ANSWER` 部分显示了答案 (`209.132.183.181`)。你还可以看到被查询的 DNS 服务器的地址。

`host` 和 `dig` 命令仅用于查询 DNS 服务器。它们不会检查 `nswitch.conf` 文件，但也可以找到查询位置，例如本地 `hosts` 文件。对于该文件，你需要使用 `getent` 命令。例如：

```
# get hosts motel
192.168.0.201 motel
```

此 `getent` 命令可以找到在我的 `/etc/hosts` 文件中输入的具名节点。（`getent` 命令可用于查询 `nswitch.conf` 文件中设置的任何信息。例如，输入 `get passwd root` 显示本地文件中 root 账户的条目，但如果你配置了该功能，也可以查询远程 LDAP 数据库中的用户信息，如第 11 章“管理用户账户”所述。）

# 设置别名网络接口

有时，你可能希望你的网络接口在多个 IP 地址上监听。如果你正在设置一个为多个域名（example.com、example.org 等）提供内容（https）的服务器，每个域名都需要独立的 IP 地址（与独立的证书关联）。在这种情况下，你不需要为电脑添加多个网卡，只需在单块网卡上创建多个别名即可。

要创建一个别名接口，你需要创建一个 `ifcfg-` 文件。参考与同一网卡关联的 `eth0` 接口的示例。要做到这一点，你需要在 `/etc/sysconfig/network-scripts` 目录下创建一个名为 `ifcfg-eth0:0` 的文件，其中包含如下信息：

```
DEVICE=eth0:0
ONPARENT=yes
IPADDR=192.168.0.141
NETMASK=255.255.255.0
```

示例代码为网络接口 `eth0` 创建了一个名为 `eth0:0` 的别名。这里不是 `ONBOOT`，而是 `ONPARENT` 表示当父接口（`eth0`）启动时启动此接口并监听地址 `192.168.0.141`。你可以通过输入 `ifup eth0:0` 来启动该接口。然后可以使用 `ip` 命令检查该接口是否已启动：

```
$ ip addr show eth0
2: eth0:<BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc
pfifo_fact state UP qlen 1000
```

## 第 14 章：网络管理

```
link/ether 0de:f1:28:46:d9 brd ff:ff:ff:ff:ff
inet 192.168.0.140/24 brd 192.168.0.255 scope global eth0
inet 192.168.0.141/24 brd 192.168.0.255 scope secondary eth0:0
inet6 fe80::fde:ff28:48:d69/64 scope link
valid_lft forever preferred_lft forever
```

你可以看到网络接口在两个地址上监听：`192.168.0.140` (`eth0`) 和 `192.168.0.141` (`eth0:0`)。因此，该系统将响应指向这两个地址之一的数据包。你可以通过创建 `ifcfg-eth0:` 文件（如 `ifcfg-eth0:1`、`ifcfg-eth0:2` 等）为你的接口添加更多 IP 地址。

## 设置以太网绑定（Bonding）

以太网绑定（Ethernet bonding）允许你在具有单个 IP 地址的电脑上使用多个网卡。有几个原因你可能想这样做：

- **高可用性**——IP 地址上的多个网卡可以确保如果某个子网宕机或某个网卡损坏，仍然可以通过连接到另一个子网的网卡访问该地址。
- **性能**——如果一个网卡处理的流量过多，你可以将流量分摊到多个网卡上。

在 Red Hat Linux 和 Fedora 中，你可以通过创建几个 `ifcfg` 文件并加载必要的模块来设置以太网绑定。你可以从一个绑定文件开始（例如 `ifcfg-bond0`），然后将多个 `ifcfg-eth?` 文件指向该绑定接口。你可以加载绑定模块。

根据你想要做的绑定类型，你可以在不同的模式下设置绑定接口。使用 `BONDING_OPTS` 变量，你可以定义模式和绑定选项（这些都是绑定模块的一部分）。你可以通过输入 `modinfo bonding` 或通过安装 `kernel-docs` 包并读取 `/usr/share/doc/kernel-doc*/Documentation/networking/bonding.txt` 目录下的 `bonding.txt` 文件来了解该模块。

这里是一个定义绑定接口的文件示例。示例中的文件为 `/etc/sysconfig/network-scripts/ifcfg-bond0`：

```
DEVICE=bond0
ONBOOT=yes
IPADDR=192.168.0.50
NETMASK=255.255.255.0
BOOTPROTO=none
BONDING_OPTS="mode=active-backup"
```
