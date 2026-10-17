
8. 切换连接开关。

## ethtool 命令

`ethtool` 用于管理网卡驱动程序和网络配置。是否默认安装取决于所使用的发行版。`httool` 工具具有许多收集信息的选项。

```
[root@server01 ~]# ethtool -S enp3s0
NIC statistics:
  tx packets: 34038
  rx packets: 41021
  tx errors: 0
  rx errors: 0
  rx missed: 0
  align errors: 0
  tx single collisions: 0
  tx multi collisions: 0
  unicast: 39280
  broadcast: 1741
  multicast: 0
  tx aborted: 0
```

![](img/b739f72e1850e8363a4e440b6c753d29_236_0.png)

显示网络接口的统计信息。

### 语法

`ethtool` 命令的语法为 `ethtool [options] {device name}`

`-f {interface}`

[image]

### 用途

显示 NIC（网卡）的统计信息。

显示 NIC 的驱动程序信息。

对 NIC 执行自检。

更改 NIC 的设置，例如速度和双工模式。

写入（闪存）到 NIC。

## brctl 命令

网络桥接涉及将通常互不传递流量的两个网络关联。桥接工作在 OSI 第 2 层，使用 MAC 地址。Linux 系统可以被配置为桥接两个网络。`brctl`（桥接控制）命令用于在 Linux 内部配置桥接。

桥接的一个常见示例如下：

1. `brctl show` — 查看桥接配置。
2. `brctl addif [bridge name]` — 创建一个空桥。
3. `brctl addif [bridge name] eth0` — 将 `eth0` 添加到桥中。
4. `brctl addif [bridge name] eth1` — 将 `eth1` 添加到桥中，连接连接到 `eth0` 和 `eth1` 的网络。

### 语法

`brctl` 命令的语法为 `brctl [command]`

## NIC 绑定 (BONDING)

在同一系统上将两个或多个 NIC 关联起来，可以实现带宽聚合、容错/冗余以及负载均衡。接口通常被独立管理，并具有不同的 IP 地址配置。使用绑定时，接口被视为单个设备进行管理，并具有相同的 IP 地址配置。绑定两个或多个 NIC 的能力是服务器的一项重要功能。如果绑定中有两个 NIC 其中一个故障，另一个将继续提供连接。

Linux 支持 NIC 绑定，但网络交换机也必须支持。这种支持被称为 EtherChannel。它是大多数企业级交换机的功能之一。

注意：某些 Linux 发行版还支持 NIC 组 (`teaming`)，这是一种类似但更灵活的链路聚合方法。例如，RHEL 6 支持 NIC 绑定，而 RHEL 7 同时支持 NIC 绑定和 NIC 组。

![](img/b739f72e1850e8363a4e440b6c753d29_240_0.png)

### NIC 1

### NIC 2

交换机

绑定在同一交换上的上的 NIC。

## NIC 绑定流程

创建 NIC 绑定配置的过程从创建绑定开始，然后将 NIC 添加到绑定中。

1. 确保加载支持 NIC 绑定的内核模块。
2. 运行 `modprobe --first-time binding command` 来加载模块。
3. 运行 `modinfo binding command` 查看关于内核模块的额外信息。
4. 在 `/etc/modprobe.d/` 目录下创建一个名为 `bond.conf` 的文件，内容为：`alias bond00`
5. 创建绑定接口：
   a. `nmcli add type bond con-name bond00 interface bond00 mod active-passive`
6. 将 NIC 接口添加到绑定接口：
   a.a. `<device ID> <device ID> masterbond00`
   b.b. `<device ID> <device ID> masterbond00`
7. 设置绑定接口及其 IP 配置，就像普通 NIC 一样。对于服务器，通常意味着将设置静态 IP 地址。
8. 测试连接，包括任何故障转移设置。不要忘记你可能还需要配置交换机以支持 NIC 绑定。

> 注意：可以使用 `nmcli ui` 或 NetworkManager GUI 工具配置 NIC 绑定。

## `/etc/sysconfig/network-scripts/` 目录

`/etc/sysconfig/network-scripts/` 目录包含网络设备配置文件。这些文件包含了 Linux 系统上可能任何 NIC 和网接器的配置。这些文件通常采用 `ifcfg-<NIC>` 的形式。设置可以包括 NIC 配置为静态还是动态 IP 地址、NIC 是否启用等。具体设置取决于所需的配置和设备类型。

虽然可以使用 Vim 或 nano 等文本编辑器手动编辑这些文件，但 NetworkManager 实用程序通常是管理接口的更好的方法。NetworkManager 提供了命令行、文本界面和图形界面。

```
[root@server01~# ls -l /etc/sysconfig/network-scripts/
total 248
--rw-r--r-- 1 root root 351 Jan 24 14:21 ifcfg-ifpc30-
--rw-r--r-- 1 root root 254 Jan 25 2018 ifcfg-lo
--rw-r--r-- 1 root root 22 Nov 14 18:12 ifup -> ../../usr/sbin/ifup
-rwxr-xr-x 1 root root 240 Jan 22 2018 ifdown-bnep
-rwxr-xr-x 1 root root 654 Jan 25 2018 ifdown-eth
-rwxr-xr-x 1 root root 6199 Apr 2018 ifdown-ib
-rwxr-xr-x 1 root root 781 Jan 22 2018 ifdown-ippp
--rw-r--r-- 1 root root 4549 Jan 25 2018 ifcfg-ipv6
--rw-r--r-- 1 root root 11 Dec 11 18:17 ifcfg-isdn -> ifdown-isdn
```

续约租约。续约过程为在网络配置发生变化时更新客户端提供了机会。

租约通常包含客户端的 IP 地址、相关的子网掩码、默认网关（路由器）的 IP 地址、一个或多个 DNS 服务器的 IP 地址以及租约的有效期。还有其他可以配置的额外选项。

DHCP 客户端定期续约其租租的 IP 地址。如果 DHCP 服务器检测到客户端的信息已过时，它将强制客户端租用新的配置。如果没有变化，续约将成功。租约续约过程是初始租约生成过程中的第三步和第四步。

### DHCP 客户端

### DHCP 服务器

![](img/b739f72e1850e8363a4e440b6c753d29_243_0.png)

DHCP 客户端从 DHCP 服务器租用 IP 地址的过程。

## `/etc/dhcp/dhclient.conf` 文件

主要的 DHCP 客户端引用文件是 `/etc/dhcp/dhclient.conf` 文件。该文件允许配置 DHCP 客户端设置，包括超时值、动态 DNS 配置等。该文件由 NetworkManager 调用并管理，NetworkManager 是多个网络设置的网络配置服务。通常建议使用 NetworkManager 来管理 DHCP 客户端配置，而不是直接编辑 `/etc/dhcp/dhclient.conf`。

## 如何配置 DHCP 客户端

使用以下步骤配置 DHCP 客户端。

### 配置 DHCP 客户端

要配置 DHCP 客户端：

1. 假设拥有超级用户权限。
2. 打开或创建文件 `/etc/dhcp/dhclient.conf`。
3. 在此情况下，添加行以以配置 DHCP 租约过程，包括：
   - `<time>`：指定客户端在无法连接到 DHCP 服务器时等待的时间，之后它将尝试通过其他手段配置地址。
   - `retry <time>`：指定客户端在再次尝试连接 DHCP 服务器之前必须等待的时间。
   - `reject <IP>`：拒绝来自 DHCP 服务器或服务器范围的租约提议。
   - `request <options>`：仅向 DHCP 服务器请求特定类型的数据。
   - `require <options>`：忽略任何不包含所有指定选项的 DHCP 租约建议。
4. 保存并关闭文件。
5. 重启 `dhclient` 服务。

## IP 解析
