
物理链路层（通常是以太网）协议用于将 IP 数据包交付到最终目的地。当两台计算机跨子网络或互联网通信时，使用 IP 数据包来封装 TCP 和 UDP 数据包。IP 数据包从一个网络路由到另一个网络，直到到达目标网络设备物理连接的子网络；路由基于 IP 头部中包含的源 IP 和目的 IP。在 IP 数据包路由到最终目的地子网络后，它会被交付给物理设备。该过程通过将 IP 数据包封装在以太网帧（或包）中完成。

与 IP 数据包不同，以太网帧的头部不包含 IP 地址、端口或其他信息。相反，它使用目标网络设备 NIC（网络接口卡）的硬件地址。世界上每台以太网设备都有（或至少应该有）由设置唯一地址。硬件地址（也称为机器地址或 MAC）由六个十六进制组成，例如 `00:05:5D:F1:03:C4`。

控制 IP 数据包所在子网络的本地路由器将其封装在以太网帧中。目标网络设备读取它看到的每个以太网帧的前几个字节。如果以太网帧地址与网络设备的以太网 MAC 地址匹配，则 NIC 读取帧的其余部分。NIC 将以太网帧发送给 Linux 内核。内核从以太网帧中提取 IP 数据包。

### 查看红帽 Linux 系统的网络布局

红 Hat Linux (RHL) 使用程序、脚本和文件来存储信息并配置其网络系统。RHL 将这些执行各种许多实体存储在多个目录中。本节将描述这些文件、它们的位置及其功能。

### 重要网络配置文件

了解配置文件和脚本的位置非常重要，因为这些文件包含了系统在启动期间初始化网络接口和路由的信息。你也可以使用这些文件和脚本手动执行这些任务。

#### `/ETC` 目录

这个无处不在的目录存储了大多数 Linux 操作系统（以及许多应用程序）的 `/etc` 配置信息 `/etc` 目录及其子目录存储了关于网络的信息。以下列表描述了：

- `hosts`：包含环回以及你想包含的额外主机的 IP 地址和名称。
- `resolv.conf`：此文件包含主机的域名、域名服务器地址（或地址）和搜索域。
- `modules.conf`：配置文件定义了启动时加载的模块。

## 第二章：配置红帽 Linux 网络

![](img/75465a3c65cedf6b73d2aa7a566f6512_46_0.png)

上述 `/etc/hosts` 显示了最小配置。然而，我们建议保持最小配置，并让域名服务 (DNS) 来处理地址。保持稀疏的 `/etc/hosts` 文件可以确保在你修改 DNS 时，它不会过时。

`nsswitch.conf`: 此配置文件告诉 Linux 从何处查找网络和其他系统信息（如主机名）。例如，如果你想让计算机在查询 DNS 之前查找 `/etc/hosts` 文件，则可以使用此文件来实现。

默认的红帽 Linux（Red Hat Linux）`nsswitch.conf` 配置如下：

`hosts: files nisplus dns`

此顺序告诉 Linux 在查找名称时首先查找 `/etc/hosts` 表。如果 Linux 没找到该名称，它将依次使用 `nisplus`，最后使用 `dns` 来查找信息。

`sysctl.conf`: 此文件包含内核级的网络配置信息。你可以在此文件中找到开启或关闭 IP 转发、IP 分片以及源路由验证的标志。`sysctl` 程序使用这些信息修改内核。以下是默认的 `/etc/sysctl.conf` 文件：

```bash
### 禁用数据转发
net.ipv4.ip_forward = 0
### 启用源路由验证
net.ipv4.conf.all.rp_filter = 1
# 禁用 magic-sysrq 
kernel.sysrq = 0
```

例如，如果你想创建一个 Linux 互联网网关，如下所示修改第一个参数：

`net.ipv4.ip_forward = 1`

以 root 身份运行 `sysctl -p` 命令，IP 转发将会被开启。

#### `/ETC/RC.D/INIT/NETWORK` 目录

该脚本用于启动和停止 Linux 的网络功能；它提供了有关机器网络的状态和其他信息。软链接（一种本质上充当指针的 Linux 文件）`/etc/rc.d/rc3.d/S0network`（在非图形模式下运行）和 `/etc/rc.d/rc5.d/S0network`（图形模式）指向 `/etc/rc.d/init/network` 脚本。系统使用这些指针在启动计算机时开启网络。

该脚本使用存储在 `/etc/sysconfig/network-scripts` 中的信息来启动、停止和显示红帽 Linux 网络的状态。为了简洁起见，我们省略了脚本的细节。

#### `/ETC/SYSCONFIG/NETWORK` 目录

此文件包含主机名、默认 IP 地址、网关设备（NIC）和 IP 转发标志（尽管该标志实际上已不再改变该功能）。`/etc/sysconfig/network-scripts` 中的脚本在配置计算机网络时使用这些信息。

### 配置红帽 Linux 网络

#### `/ETC/SYSCONFIG/NETWORK-SCRIPTS` 目录

此目录包含用于控制红帽 Linux 网络的脚本。如 `ifcfg-eth0` 等脚本包含特定特定接口的信息。`network-function` 脚本包含控制脚本使用的子程序。如 `ifup`、`ifdown` 和 `ifup-routes` 等脚本控制网络接口的状态。

- `ifup` 和 `ifdown`: 这些脚本使用包含如 `ifcfg-lo`、`ifcfg-eth0` 等文件中的信息来开启或关闭相应的接口。
- `ifcfg-lo`: 包含关于你的环回接口（loopback interface）的信息。`ifup` 和 `ifdown` 使用此脚本来开启或关闭环回接口。
- `ifcfg-eth0`: 包含关于你的第一个以太网适配器的配置信息，包括 IP 地址。`ifup` 和 `ifdown` 使用此脚本开启或关闭设备。
- `ifcfg-eth1`, `ifcfg-eth2`, ... : 包含关于你的第二个及任何额外以太网适配器的配置信息，包括 IP。`ifup` 和 `ifdown` 使用此脚本开启或关闭设备。
- `ifup-ppp` and `ifdown-ppp`: 包含关于点点协议（PPP）设备的信息，并用于 `ifup` 和 `ifdown` 脚本开启或关闭 PPP。PPP 通常用于通过模拟电话连接将计算机和网络连接到 ISP（某些 DSL 设备使用 PPP 连接到 ISP）。
- `ifup-routes`: 包含关于路由的信息。
- `network-routes`: 包含关于 `/etc/sysconfig/network` 的路由配置信息。`ifup` 和 `ifdown` 使用此脚本开启或关闭路由。
- `network-functions`: 包含通用网络信息。`ifup` 和 `ifdown` 使用此脚本开启或关闭网卡。

> **提示**：`/etc/sysconfig/network` 脚本用于配置地址族（协议）。

- 静态路由：`/etc/sysconfig/network` 脚本用于配置网卡并开启或关闭网卡。
- `192.168.1.0` 接口 `eth0` 激活时。

### 重要的应用程序

Linux 使用许多工具来配置和操作。这些工具并不难学习或使用，是管理员必须掌握的必备工具：

- `arp`
- `ifconfig`
- `netstat`
- `ping`
- `route`
- `sysctl`
- `tcpdump`
- `usermctl`
- `modprobe`

这些工具可以获取网络详细信息。以下章节将简要介绍每个工具。

#### `arp`

Linux 维护一个与其通信过的本地机器 MAC 地址和 IP 地址列表。地址解析协议（ARP）表。

| 地址 | 类型 | 硬件地址 | 标志 | 接口 |
| :--- | :--- | :--- | :--- | :--- |
| 192.168.1.254 | ether | 00:50:BA:DE:25:35 | C | eth0 |
| 192.168.1.12 | ether | 00:05:5D:F1:03:C4 | C | eth0 |

`ifconfig` 工具设置 IP 地址、子网掩码和其他参数。它还可以显示网卡的信息。非 root 用户可以使用此工具显示信息，但在设置任何参数时必须是 root。你应该使用 `ifup` 和 `ifdown` 脚本来配置你的网络接口。

`ifconfig` 使用以下语法：

```bash
ifconfig interface [aftype] options address
```

- 显示所有网络接口。在没有提供选项的情况下，`ifconfig` 显示所有配置接口的信息，包括逻辑环回设备。如果包含接口参数，则显示该设备的信息。
- `eth0`。Linux 接口几乎是以太网设备如 `eth0`，也可以是其他类设备（如环形接口 `tr0`）。第一个设备在设备类型后面附加一个零 (`eth0`)；第二个设备将零增加为一 (`eth1`)，依此类推。
