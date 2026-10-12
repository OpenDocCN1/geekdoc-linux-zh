

## 选项

| 选项 | 描述 |
| --- | --- |
| option pop-server ip-address [, ip-address…]; | 按优先级顺序列出客户端可用的 POP3 服务器地址。 |
| option nntp-server ip-address [, ip-address…]; | 按优先级顺序列出客户端可用的 NNTP 服务器地址。 |
| option www-server ip-address [, ip-address…]; | 按优先级顺序列出客户端可用的 WWW 服务器地址。 |
| option finger-server ip-address [, ip-address…]; | 按优先级顺序列出客户端可用的 Finger 服务器地址。 |
| option irc-server ip-address [, ip-address…]; | 按优先级顺序列出客户端可用的 IRC 服务器地址。 |

## 路由

| 选项 | 描述 |
| --- | --- |
| option ip-forwarding flag; | 指示客户端是否允许（1）或不允许（0）IP 转发。如果客户端充当路由器，则应允许此操作。 |
| option non-local-source-routing flag; | 指示客户端是否允许（1）或禁止（0）转发具有非本地源路由的数据报。 |
| option static-routes ip-address ip-address [, ip-address ip-address…]; | 指定客户端用于到达特定主机的静态路由。（按优先级降序列出到同一位置的多条路由。） |
| option router-discovery flag; | 指示客户端是否应使用路由器发现机制尝试发现路由器（1）或不尝试（0）。 |
| option router-solicitation-address ip-address; | 指示客户端应使用哪个地址来发送路由器请求数据包。 |

## 瘦客户机

| 选项 | 描述 |
| --- | --- |
| option boot-size uint16; | 指示客户端计算机启动时使用的默认引导映像的大小（以 512 字节块为单位）。 |
| option merit-dump string; | 指示如果客户端崩溃，内核映像应转储的位置。 |
| option swap-server ip-address; | 指示客户端计算机的交换服务器所在位置。 |
| option root-path string; | 指示客户端使用的根磁盘的位置（路径名）。 |
| option tftp-server-name string; | 指示客户端应使用哪个 TFTP 服务器来传输引导映像。在 DHCP 客户端中比在 BOOTP 客户端中更常用。 |
| option bootfile-name string; | 指示用于启动客户端的引导文件的位置。在 DHCP 客户端中比在 BOOTP 客户端中更常用。 |
| option x-display-manager ip-address [, ip-address… ]; | 按优先级顺序指示客户端可用的 X 窗口系统显示管理器服务器的位置。 |

## 启动 DHCP 服务器

配置完 `/etc/dhcpd.conf` 文件后，您可以立即启动 DHCP 服务器。在终端窗口中，以 root 用户身份输入以下内容：

```
# service dhcpd start
```

此时，您的 DHCP 服务器应已就绪，可以向局域网内的计算机分配信息。如果局域网中有等待您的 DHCP 服务器的客户端计算机，它们的网络接口现在应该处于活动状态。

如果一切正常运行，您可以通过开启 `dhcpd` 服务，让 DHCP 服务器在每次计算机启动时自动运行，方法如下：

```
# chkconfig dhcpd on
```

有几种方法可以验证您的 DHCP 服务器是否正在正常工作：

- 检查 `/var/lib/dhcp/dhcpd.leases` 文件。如果客户端成功从 DHCP 服务器获得了地址分配，该文件中应出现租约行。对于每个已租用 IP 地址的客户端，应有一组类似以下内容的信息：

```
lease 10.0.0.225 {
    start 2 2002/05/04 03:48:12;
    ends 2 2002/05/04 15:48:12;
    hardware ethernet 00:50:ba:08:03:9e;
    client-hostname "pine";
    }
```

- 打开 Ethereal 窗口（在终端窗口中输入 `ethereal&`）并开始捕获数据（以混杂模式）。重启 DHCP 服务器并重启客户端上的网络接口。您应该会看到一系列 DHCP 数据包，显示如下的序列：DHCP Offer（提议）、DHCP Discover（发现）、DHCP Offer（提议）、DHCP Request（请求）以及 DHCP ACK（确认）。

- 从客户端计算机，您应该能够在网络上开始通信。如果客户端是 Linux 系统，请输入 **ifconfig -a** 命令。您的以太网接口（通常是 eth0）应该会出现，并且 IP 地址设置为 DHCP 服务器分配的地址。如果您的客户端是 Windows 2000 或 XP 系统，请打开命令提示符并输入 **ipconfig /all**。您将看到所有网络接口的配置信息。

当服务器正常运行时，您可以继续向网络中添加 DHCP 客户端，以利用您分配的地址池。

## 配置 DHCP 客户端

配置网络客户端以从您的 DHCP 服务器获取地址非常简单。然而，不同类型的操作系统使用 DHCP 的方式有所不同。以下是设置 Windows 和 Linux DHCP 客户端的示例。

### Windows：

1. 在大多数 Windows 操作系统（Windows 95、98、2000、XP 等）中，从控制面板打开“网络”窗口（开始 → 设置 → 控制面板）。
2. 在“配置”选项卡中，点击与您的以太网卡相关的 TCP/IP 接口（例如 TCP/IP → 3Com EtherLink III）。
3. 点击“属性”。将显示属性窗口。
4. 点击“IP 地址”选项卡，然后选中“自动获得 IP 地址”复选框。
5. 点击“确定”并重启计算机，以便客户端可以使用新的 IP 地址。

### Linux：

1. 在最初安装 Linux 时，在“网络配置”屏幕上点击“使用 DHCP 配置”。您的网络客户端在启动时应自动从您的 DHCP 服务器获取 IP 地址。
2. 要在安装后设置 DHCP，请打开“网络配置”窗口（`neat` 命令）。
3. 在“网络配置”窗口中：
   - 点击“设备”选项卡（默认开启）。
   - 点击您的以太网设备（通常是 eth0）。
   - 点击“编辑”。
   - 点击“常规”选项卡。
   - 点击“使用以下方式自动获取 IP 地址设置”，并选择 `dhcp`。
   - 点击“确定”。
   - 点击“应用”。
4. 然后，在终端窗口中输入：

```
# service network restart
```

默认情况下，Fedora 客户端不会接受 DHCP 服务器传递给它的所有信息。Fedora 客户端处理 DHCP 服务器输入的方式基于 `/etc/sysconfig/network-scripts/ifup` 脚本中的设置。如果客户端开启了 DHCPd，当系统启动网络时，`ifup` 脚本会运行 `dhclient` 命令。您可以通过创建 `/etc/dhclient.conf` 文件来调整 `dhclient` 的行为。（输入 `man dhclient.conf` 以了解如何设置您的 `dhclient.conf` 文件。）

## 理解网络信息服务

网络信息服务（NIS）由 Sun Microsystems 创建，作为一种在网络中管理一组主机计算机共享信息的方法。使用 NIS，计算机可以共享一组通用的用户账户、用户组和 TCP/IP 主机名，以及其他信息。

> 注意：NIS 最初被称为“黄页”，但由于这是商标，Sun 不得不更改此名称。有些人仍将 NIS 称为 YP，许多 NIS 命令（甚至 NIS 软件包名称）都以“yp”开头。要使用 NIS 作为客户端，您需要安装 `ypbind` 和 `yp-tools` 软件包。要配置 NIS 服务器，还需要安装 `ypserv` 软件包。

您通过 NIS 共享的信息来源于用于 UNIX 系统的文件，因此与其他类 UNIX 系统（如 Fedora 或 Red Hat Linux）兼容。主 NIS 服务器支持的一组计算机称为 NIS 域。该域是一组定义的主机计算机，可能与 TCP/IP 域中包含的计算机组相同，也可能不同。

在 NIS 中，管理员从常见的 UNIX（或 Linux）系统文件创建称为映射（maps）的信息数据库。NIS 映射在主 NIS 服务器上创建，并且可以从该服务器访问其他主机计算机。以防主服务器宕机或无法访问的情况，可以定义一个或多个从服务器。NIS 从服务器包含 NIS 映射的副本，并可以在主服务器不可用时向客户端计算机提供该信息。然而，NIS 从服务器不用于创建映射。

当映射在 NIS 域中的计算机之间共享后，主要结果是所有计算机共享一组通用的用户和网络配置。以下是 NIS 可用于共享的文件列表（并非所有这些都默认设置为共享）。

- `/etc/group` — 定义计算机上用户所属的组。

