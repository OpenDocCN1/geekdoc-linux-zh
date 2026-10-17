
请记住，并非所有驱动程序都有关联的描述，但大多数都有。

## 一致的网络设备命名

最新的 Fedora Linux 发行版版本

新的设备命名约定工作如下：

- 带有板载或嵌入式 NIC 的系统的以太网接口以前缀 `em<PORT_NUMBER>` 命名，其中 `<PORT_NUMBER>` 是物理机箱标签。例如，第一个板载以太网将被分配名称 `em1`，第二个命名为 `em2`，依此类推。
- 插入系统 PCI、PCI-e、PCI-X 等插槽的网络接口卡命名为 `p<SLOT_NUMBER>p<PORT_NUMBER>`，其中 `<SLOT_NUMBER>` 识别物理插槽 `<PORT_NUMBER>` 识别对应 NIC 上的特定端口。使用此规则的设备示例为 `p1p1`、`p8p1`、`p7p1` 等。

虚拟机将继续使用传统的 `ethX` 命名约定。在支持的平台上，通过将 `biosdevname=0` 参数作为启动时选项传递给 Linux 内核，你可以完全跳过新的命名方案。

## 网络设备配置工具 (`ip` 和 `ifconfig`)

`ifconfig` 程序负责设置你的网卡（NIC）。它的所有操作都可以通过命令行选项完成，因为它的原生格式没有菜单或图形界面。使用过 Windows `ifconfig` 程序的管理员可能会发现一些相似之处，因为微软实现了一些命令行界面（CLI）网络工具，模仿了其 UNIX 对应程序的功能子集。

> 注意 `ifconfig` 程序通常位于 `sbin` 目录，该目录包含在 root 用户的 `PATH` 中。某些登录脚本（如 openSUSE 中的脚本）默认不会为特权用户包含 `/sbin` 在 `PATH` 中。当你作为普通用户调用它时，可能需要调用 `/sbin/ifconfig`。如果你预计经常使用 `/sbin` 下的命令，可能会发现将 `/sbin` 添加到 `PATH` 是明智的。

已经编写了许多工具来封装 `ifconfig` 命令行以提供菜单驱动或图形界面，其中许多工具随各种 Linux 发行版一起发布。例如，Fedora 有一个名为 `system-config-network` 的 GUI 工具。作为管理员，你至少应该知道如何手动配置网络接口；了解这一点是无价的，因为 GUI 中未显示的许多额外选项在 CLI 中都是的。因此，本节将介绍 `ifconfig` 命令行工具的使用。

另一个可用于管理 Linux 中网络设备的强大工具是 `ip` 工具。它随 `iproute` 软件包一起，该包包含了网络实用（如 `ip`），这些工具旨在利用并操作 Linux 内核的高级网络功能。`ip` 工具的语法略显简短，且没有 `ifconfig` 工具那么宽容，但 `ip` 命令要强大得多。

> 提示 仍然在使用 Windows 的管理员可能会发现 `%SYSTEMROOT%\system32\netsh.exe` 是一个实手的工具，可以通过 CLI 暴露并操作 Windows 网络的细节。

接下来的章节将同时使用 `ifconfig` 命令和 `ip` 命令来配置我们示例服务器上的网络设备。

## 简单用法

在最简单的用法中，你只需要提供已配置的接口名称和 IP 地址。`ifconfig` 程序将从 IP 地址推断出其余信息。因此，你可以输入以下内容：

```
[root@server ~]# ifconfig eth0 192.168.1.42
```

这将将 `eth0` 设备设置为 IP 地址 `192.168.1.42`。因为 `192.168.1.42` 是一个 C 类地址，计算出的默认掩码为 `255.255.255.0`，广播地址为

如果你设置的 IP 地址是子网划分不同的 A 类、B 类或 C 类，你需要在命令行显式设置子网掩码和网络地址，如下所示：

```
[root@server ~]# ifconfig dev ip netmask nmask broadcast
```

在这里，`dev` 是你正在配置的网络设备，`ip` 是你要设置的 IP 地址，`nmask` 是子网掩码，`bcast` 是广播地址。
以下示例将将 `eth0` 设备设置为 IP 地址 `1.1.1.1`，子网掩码为 `255.255.255.0`，广播地址为 `1.1.1.255`。

```
[root@server ~]# ifconfig eth0 1.1.1.1 netmask 255.255.255.0 broadcast 1.1.1.255
```

使用 `ip` 命令执行相同操作，你需要输入：

```
[root@server ~]# ip address add 1.1.1.1/24 broadcast 1.1.1.255 dev eth0
```

> 提示 `ip` 命令允许在语法中使用唯一的缩写。前述命令也可以缩短为：
```
# ip a ad 1.1.1.1/24 br 1.1.1.255 dev eth0
```

使用 `ip` 命令删除之前创建的 IP 地址，类型为：

```
[root@server ~]# ip address del 1.1.1.1/24 broadcast 1.1.1.255 dev eth0
```

使用 `ip` 命令为接口 `eth0` 分配 IPv6 地址（例如，`2001:DB8::`），你会使用以下内容：

```
[root@server ~]# ip -6 addr add 2001:DB8::1/64 dev eth0
```

```
[root@server ~]# ip -6 addr del 2001:DB8::1/64 dev eth0
```

`ifconfig` 命令也可以用于为接口分配 IPv6 地址。例如，通过运行以下命令为 `eth2` 分配 IPv6 地址 `2001:DB8:3`：

```
[root@server ~]# ifconfig eth2 inet6 add 2001:DB8::3/64
```

要显示所有接口上的 IPv6 地址，你可以这样使用 `ip` 命令：

```
[root@server ~]# ip -6 show
```

## IP 别名 (IP Aliasing)

在某些情况下，单个主机需要多个 IP 地址。Linux 可以通过使用 IP 别名支持这一点。Linux 系统中的每个接口都可以有多个 IP 地址。这是通过用冒号跟数字枚举接口的每个实例来实现的——例如，`eth0` 是主接口，`eth0:1` 是别名接口，`eth0:2` 是另一个别名接口，依此类推。

配置别名接口与其他接口一样：只需使用 `ifconfig` 为 `eth0:0` 设置地址 `10.0.0.2` 和掩码 `255.255.255.0`，我们将执行：

```
[root@server ~]# ifconfig eth0:0 10.0.0.2 netmask 255.255.255.0
```

使用 `ip` 命令执行相同操作，输入：

```
[root@server ~]# ip addr add 10.0.0.2/24 dev eth0
```

你可以通过输入以下内容查看你的更改：

```
[root@server ~]# ifconfig eth0:0
```

Link:Ethernet Haddr 00:0C:29:AC:5B:CD

inet:10.0.0.2 Bcast:10.0.0.255 Mask:255.255.255.0

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

Interrupt:17 Base address:0x1400
