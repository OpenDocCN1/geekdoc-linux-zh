
一旦我们通过 `podman ps` 确认该容器正在运行，使用 `podman healthcheck` 命令来获取容器的健康状况：

```bash
[jsg@rhel9-bpp~$] podman healthcheck mycontainer
```

Healthy

# 配方 #56：管理容器网络

在 Podman 中，你可以为内部和外部网络创建新规则并管理流量。

- 无 root（Rootless）：网络自动设置。
- 有 root（Rootful）：网络分配 IP。

默认情况下，`podman` 创建桥接。从终端列出所有活跃网络：

```bash
[jsg@rhel9-bpp~$] podman network ls
```

要检查网络的详情，使用 `podman inspect`：

```bash
[jsg@rhel9-bpp~$] podman network inspect mycontainer
```

要创建一个新网络，使用 `podman network create` 命令：

```bash
[jsg@rhel9-bpp~$] podman network create mynetwork
```

要将容器连接到网络，使用 `podman network connect` 命令：

```bash
[jsg@rhel9-bpp~$] podman network connect mynetwork mycontainer
```

要从网络断开容器，使用 `podman network disconnect` 命令：

```bash
[jsg@rhel9-bpp~$] podman network disconnect mynetwork mycontainer
```

要删除未使用的网络，使用 `podman network rm` 命令：

```bash
[jsg@rhel9-bpp~$] podman network rm mynetwork
```

## 结构

在本章中，我们将涵盖以下主题：

- 配置以太网和 Wi-Fi 连接
- 配置 VLAN 以保护网络流量
- 在网络接口上配置网络绑定（Bonding）以获得更高的吞吐量
- 配置 VPN 连接
- 建立 IP 隧道
- 使用 `parted` 和 `fdisk` 进行基础磁盘管理
- 使用 LVM 创建逻辑存储设备
- 管理远程 iSCSI 存储
- 设置 Samba 服务用于文件和打印服务
- 建立 NFS 服务

## 目标

在本章中，我们将讨论为什么 RHEL 9 是管理网络基础设施的卓越平台，并强调其在安全配置和管理网络服务方面的能力。我们将涵盖这些网络服务的创建，重点关注如何保护它们免受威胁，以及如何在 RHEL 9 生态系统中有效管理文件存储和相关存储设备。此外，我们将强调为网络用户量身构建和管理文件服务，并实施强有力的措施来保护这些存储设备并维护数据的完整性和可用性。

# 菜谱 #57：配置以太网和 Wi-Fi 连接

在深入配置 RHEL 9 中的以太网和 Wi-Fi 连接之前，你可能用过或听过如 `ifconfig` 或 `ip` 等网络配置工具。这些是存在很久的低级工具，今天仍在使用，尽管它们的流行已被 NetworkManager 等更易于使用的工具所掩盖。旧的网络配置方法通常涉及编辑 `/etc/sysconfig/network-scripts/` 下的配置文件，这可能容易出错且不那么直观。

从 RHEL 9 开始，红帽将 NetworkManager 作为网络配置的主要工具，在不同环境中提供了更一致、更易于用户的方法。我们不会在本章中讨论旧方法（尽管如此），我们可能会引用一些对于高级故障排除可选的低级工具。

## 绕过网络、文件和存储服务

如果你使用控制台，可以使用 NetworkManager 的一部分—— `nmcli` 命令行工具，来同时配置以太网和 Wi-Fi 连接：

```bash
[1b@rhel19_bp ~]$ sudo nmcli connection add type ethernet con-name "Office-LAN" ifname eth0 ip4 192.168.1.100/24 gw4 192.168.1.1
[1b@rhel19_bp ~]$ sudo nmcli device wifi connect "MyHomeWiFi" password "mysecurepassword"
```

NetworkManager 及其工具 `nmcli` 和 `nmui` 开发是为了提供更顺畅的网络配置体验，并具有以下优势：

- **跨平台一致性**：无论你是在服务器、桌面甚至不同的 Linux 发行版上，NetworkManager 都提供了一个一致的接口。
- **动态配置**：在不同的网络或连接类型之间轻松切换，无需重新配置。
- **与桌面环境集成**：对于 GNOME 或 KDE 用户，NetworkManager 与 GUI 无缝集成。
- **扩展性**：通过插件支持各种 VPN 隧道、移动宽带等。

`nmcli` 是 NetworkManager 的命令行界面，旨在提供对 NetworkManager 功能的全访问。它在服务器环境或脚本编写中特别有用。在本章的大多数练习将使用 `nmcli`。

`nmui` 是一个文本界面，提供了一种更视觉化、菜单驱动的网络配置方法。它对于那些倾向于引导式体验或在没有完整 GUI 的环境中工作的人来说非常棒。

`nm-connection-editor` 是 NetworkManager 的图形化工具，通常用于桌面环境。虽然我们在本章中关注命令行工具，但桌面用户可能会发现此工具非常直观。

> 提示：本章将重点关注使用 `nmcli` 进行网络配置。红帽客户门户提供了关于 RHEL 9 中 NetworkManager 的全面文档。你可以通过 https://access.redhat.com/documentation/en/red_hat_enterprise_linux/9/html-single/configuring_and_managing_networking/index 进行阅读。

如果你希望使用旧的网络配置方法，可以通过安装 `network-scripts` 包来实现。然而，不建议这样做，因为在 RHEL 9 中它被视为遗留方案。保留旧脚本主要是为了兼容旧的配置或尚未迁移到 NetworkManager 的非常特定的设置：

```bash
[1b@rhel19_bp ~]$ sudo dnf install network-scripts
```

本着向现代、健壮工具迈进的精神，我们强烈建议在 RHEL 9 的所有网络配置需求中使用 NetworkManager。

# 菜谱 #58：配置 VLAN 以保护网络流量

在 RHEL 9 中使用 VLAN 保护网络流量，你可能用过或听过物理网络隔离或为不同部门使用独立网络交换机的技术。这些传统方法已存在很久，今天仍在使用，尽管它们的灵活性成本效益被 VLAN 技术所掩盖。旧方法通常涉及购买额外的硬件、重新布线办公室空间以及手动配置每个交换机，这可能是昂贵的、耗时的，并且对变化的业务需求适应性较差。与 RHEL 9 一，红帽将 VLAN 配置与 NetworkManager 无缝集成，提供了一种更动态、软件定义的隔离方法。我们不会在本章中讨论物理网络隔离实践（尽管我们可能会参考全面的网络安全实践）。大多数企业交换机支持 VLAN 标记（IEEE 802.1Q），它与 RHEL 9 的 VLAN 功能无缝工作。可以使用 NetworkManager 提供的 `nmcli` 工具在 RHEL 9 中设置 VLAN 以保护网络流量。在示例中，我们将为财务部门创建一个 VLAN，将其敏感流量与其他网络隔离开。

```bash
[1b@rhel19_bp ~]$ sudo nmcli connection add type vlan con-name "Finance-VLAN" device eth0 id 10
```

一旦创建了 VLAN，我们就可以激活它开始使用接口：

```bash
[1b@rhel19_bp ~]$ sudo nmcli connection up "Finance-VLAN"
```

现在，让我们验证 VLAN 是否已启动并拥有 IP 地址：

```bash
[1b@rhel19_bp ~]$ ip addr show vlan10
```

输出应该类似于：

```text
2: vlan10: <BROADCAST,MULTICAST,UP,LOWER> state UP qlen 1000
    link/ether 52:54:00:12:34:56 brd ff:ff:ff:ff:ff:ff
    valid_lft forever no_dft 100000
    inet 192.168.10.50/24 scope global 192.168.10.50
       valid_lft forever__lft forever
```

为了测试连通性，我们可以 ping 网关或 VLAN 上的其他设备：
