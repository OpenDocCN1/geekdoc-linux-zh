
# 24.5. DHCP

## 瘦客户端

### 选项

| 选项 | 描述 |
| :------- | :---------- |
| option router-solicitation-address ip-address; | 指示客户端应使用的地址，以转发路由器发现请求。 |
| option boot-size uint16; | 指示客户端计算机用于引导的默认引导映像的大小（以 512 字节块为单位）。 |
| option merit-dump string; | 指示如果客户端崩溃，核心映像应该转储到哪里。 |
| option swap-server ip-address; | 指示客户端计算机的交换服务器位置。 |
| option root-path string; | 指示客户端使用的根磁盘的位置（路径名）。 |
| option tftp-server-name string; | 指示客户端应使用的 TFTP 服务器名称，用于传输引导映像。在 DHCP 客户端中比在 BOOTP 客户端中更常用。 |
| option bootfile-name string; | 指示用于引导客户端的引导文件的位置。在 DHCP 客户端中比在 BOOTP 客户端中更常用。 |
| option x-display-manager ip-address [, ip-address… ]; | 指示客户端可使用的 X 窗口系统显示管理器服务器位置，按优先级排序。 |

## 启动 DHCP 服务器

在配置完 `/etc/dhcp/dhcpd.conf` 文件后，您可以立即启动 DHCP 服务器。以 root 用户身份在终端窗口中，输入以下内容：

```bash
# service dhcpd start
```

此时，您的 DHCP 服务器应已可用，可以向局域网中的计算机分发信息。如果局域网中有客户端计算机正在等待您的 DHCP 服务器，它们的网络接口现在应该处于活动状态。

> **注意：** 如果您没有为服务器上配置的所有网络接口卡指定子网，则需要编辑 `/etc/sysconfig/dhcpd` 并指定它应监听哪些接口。

如果一切正常运行，您可以通过以下方式开启 dhcpd 服务，使 DHCP 服务器在计算机每次启动时自动启动：

```bash
# chkconfig dhcpd on
```

您可以通过以下几种方式验证您的 DHCP 服务器是否正在工作：

- 检查 `/var/log/messages` 文件。如果 DHCP 服务启动遇到问题，您会在此文件中看到指示问题的信息。
- 检查 `/var/lib/dhcpd/dhcpd.leases` 文件。如果客户端已成功从 DHCP 服务器获得地址分配，该文件中应出现一行租约记录。对于每个已租用 IP 地址的客户端，应有一组类似以下内容的信息：

```text
lease 10.0.0.225 {
    starts 2 2009/05/04 03:48:12;
    ends 2 2009/05/04 15:48:12;
    hardware ethernet 00:50:ba:d8:03:9e;
    client-hostname "pine";
}
```

- 启动 Wireshark（输入 `yum install wireshark` 进行安装，输入 `wireshark &` 运行）并开始捕获数据（处于混杂模式）。重启 DHCP 服务器并重启客户端上的网络接口。您应该会看到一系列显示如下序列的 DHCP 数据包：DHCP Discover、DHCP Offer、DHCP Request 和 DHCP ACK。
- 从客户端计算机，您应该能够开始在网络上进行通信。如果客户端是 Linux 系统，输入 `ifconfig -a` 命令。您的以太网接口（可能是 eth0）应显示出来，且 IP 地址已设置为由 DHCP 服务器分配的地址。如果您的客户端是 Windows 系统，打开命令提示符并输入 `ipconfig /all`。您会看到所有网络接口的配置信息。

当服务器正常运行时，您可以继续向网络中添加 DHCP 客户端，以利用您分配的地址池，直到达到分配的数量上限。

# 24.6. 配置 DHCP 客户端

大多数客户端计算机（Windows、Linux 或 Mac）默认配置为使用 DHCP 启动并连接到网络。然而，如果不是这种情况，您可能需要手动指示使用 DHCP。

配置网络客户端从您的 DHCP 服务器获取地址相当简单。但是，不同类型的操作系统使用 DHCP 的方式不同。以下是设置 Windows、Linux 和 Mac DHCP 客户端的示例。

## Windows (Vista 或 7)

- 在 Windows Vista 或 Windows 7 中，选择 开始 > 控制面板 > 网络和 Internet > 网络和共享中心 > 管理网络连接。
- 选择 本地连接。
- 选择 属性。属性窗口将显示。
- 选择 Internet 协议版本 4 并单击 属性。
- 在 常规 选项卡上，确保选中了“自动获取 IP 地址”按钮。

## Windows (95, 98, 2000 或 XP)

- 在大多数较旧的 Windows 操作系统（Windows 95、98 和 2000）中，您从控制面板（开始 > 设置 > 控制面板）打开 网络 窗口。对于 Windows XP 系统，选择 开始 > 控制面板 > 网络连接 > 网络连接，然后选择您的 本地连接 并选择 属性。
- 从 配置 选项卡（或在 Windows XP 中的 常规 选项卡），单击与您的以太网卡关联的 TCP/IP 接口（例如 TCP/IP > 3Com EtherLink III）。
- 单击 属性。属性窗口将显示。
- 单击 IP 地址 选项卡（或在 Windows XP 中的 常规 选项卡），然后选中“自动获取 IP 地址”复选框。
- 单击 确定 并重启计算机，以便客户端可以使用新的 IP 地址。

## Fedora

在最初安装 Linux 时，在 网络配置 屏幕上单击 使用 DHCP 配置。您的网络客户端在启动时应自动从您的 DHCP 服务器获取 IP 地址。

要在安装后使用网络管理器设置 DHCP，请按照以下步骤操作：

- 右键单击 GNOME 面板中的 网络管理器 图标。
- 选择 编辑连接。
- 高亮显示“系统 eth0”并按 编辑... 按钮。
- 选择 IPv4 设置 选项卡。
- 从 方法 下拉框中选择“自动 (DHCP)”。
- 单击 应用，然后单击 关闭。
- 单击 网络管理器 图标并选择 系统 eth0 重新连接。

此外，Fedora 服务器上还有一个常用的传统工具，您可以使用它代替网络管理器。要在安装后使用传统网络配置工具设置 DHCP，请按照以下步骤操作：

- 打开 网络配置 窗口（选择 系统 > 管理 > 网络 或运行 `system-config-network` 命令）。
- 从 网络配置 窗口：
  - 单击 设备 选项卡（默认处于打开状态）。
  - 单击您的以太网设备（可能是 eth0）。
  - 单击 编辑。
  - 单击 常规 选项卡。
  - 单击“自动获取 IP 地址设置使用”并选择 dhcp。
  - 单击 确定。
  - 选择 文件 → 保存。
- 然后，在终端窗口中输入以下内容：

```bash
# service network restart
```

## Apple Mac OS X

- 在 Mac OS X 系统中，选择 Apple 菜单 > 系统偏好设置 > 网络。从 互联网和局域网 部分打开 网络 窗口。
- 选择要配置 DHCP 的适当网络接口。
- 在 配置 字段中，选择 使用 DHCP。
- 单击 高级 按钮以添加您的 DHCP 客户端 ID。您还可以选择 续租 DHCP 租约 以手动向 DHCP 服务器请求带有新租约的 IP 地址。完成后单击 确定。
- 添加任何其他相关信息并单击 应用。

默认情况下，Fedora 客户端不会接受从 DHCP 服务器传递给它的所有信息。Fedora 客户端处理 DHCP 服务器输入的方式基于 `/etc/sysconfig/network-scripts/ifup` 脚本中的设置。如果客户端启用了 DHCP，当系统启动网络时，`ifup` 脚本会运行 `dhclient` 命令。您可以通过创建 `/etc/dhclient.conf` 文件来调整 `dhclient` 的行为。（输入 `man dhclient.conf` 以了解如何设置您的 `dhclient.conf` 文件。）

# 总结

DHCP 提供了一种集中管理网络中计算机的机制，并且可以提供有助于客户端计算机快速在网络中运行的信息。

DHCP 用于向网络中的 Windows、Linux、Mac 或其他客户端计算机提供关于您网络的信息。IP 地址可以动态分配，这意味着它们从 IP 地址池中分发。或者，可以根据特定的以太网硬件地址将特定地址分配给客户端。

