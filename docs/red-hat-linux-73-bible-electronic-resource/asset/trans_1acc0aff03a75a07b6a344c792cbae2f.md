

    ends 2 2002/05/04 15:48:12;
    hardware ethernet 00:50:ba:d8:03:9e;
    client-hostname "pine";
}

- 打开 Ethereal 窗口（从 GNOME 菜单中，选择“程序” → “互联网” → ethereal），并开始捕获数据（以混杂模式）。重启 DHCP 服务器并重启客户端上的网络接口。你应该会看到一系列 DHCP 数据包，显示如下顺序：DHCP Offer、DHCP Discover、DHCP Offer、DHCP Request 和 DHCP ACK。
- 从客户端计算机，你应该能够开始在网络上通信。如果客户端是 Linux 系统，输入 `ifconfig -a` 命令。你的以太网接口（可能是 eth0）应该会出现，并且 IP 地址设置为由 DHCP 服务器分配的地址。

当服务器正常运行时，你可以继续向网络中添加 DHCP 客户端，以利用你分配的地址池。

## 设置 DHCP 客户端

配置网络客户端从你的 DHCP 服务器获取地址相当简单。然而，不同类型的操作系统使用 DHCP 的方式不同。以下是设置 Windows 和 Red Hat Linux DHCP 客户端的示例。

**Windows：**

1. 在大多数 Windows 操作系统（Windows 95、98、ME 等）中，你从控制面板（开始 → 设置 → 控制面板）打开网络窗口。
2. 在“配置”选项卡中，单击与你的以太网卡关联的 TCP/IP 接口（例如 TCP/IP → 3Com EtherLink III）。
3. 单击“属性”。属性窗口会出现。
4. 单击“IP 地址”选项卡，然后选择“自动获取 IP 地址”。
5. 单击“确定”并重新启动计算机，以便客户端能够获取新的 IP 地址。

**Red Hat Linux：**

1. 在初始安装 Red Hat Linux 时，在“网络配置”屏幕上单击“使用 DHCP 配置”。你的网络客户端在启动时应该自动从你的 DHCP 服务器获取 IP 地址。
2. 要在安装后设置 DHCP，请打开网络配置窗口（neat 命令）。
3. 从网络配置窗口：
   - a. 单击“设备”选项卡。
   - b. 单击你的以太网设备（可能是 `eth0`）。
   - c. 单击“编辑”。
   - d. 单击“协议”选项卡。
   - e. 单击 TCP/IP。
   - f. 选择“编辑”。
4. 在 TCP/IP 设置窗口中，单击“自动获取 IP 地址设置方式为：”并选择 `dhcp`。
5. 然后，从终端窗口输入：

```
# /etc/init.d/network restart
```

默认情况下，Red Hat Linux 客户端不会接受从 DHCP 服务器传入的所有信息。Red Hat Linux 客户端处理 DHCP 服务器输入的方式基于 `/etc/sysconfig/network-scripts/ifup` 脚本中的设置。如果客户端开启了 DHCP，当系统启动网络服务时，`ifup` 脚本会以以下方式运行 `dhcpd` 命令：

- 如果 `dhcpd` 客户端进程当前正在运行，`dhcpd` 命令会向其发送信号，使其向 DHCP 服务器申请更新 IP 地址租约。
- 如果客户端当前未设置主机名（或主机名设置为 localhost），则向 `dhcpd` 传递 -H 选项，指示其应接受 DHCP 服务器提供的主机名。（如果主机名已设置，客户端不会从服务器重置主机名。）
- 客户端会接受任何新的 DNS 服务器分配。如果你的 DNS 服务器已在 `/etc/resolv.conf` 文件中配置，则可以向 `dhcpd` 传递 -R 选项，以防止其用新的 DNS 服务器信息更新该文件。（为此，请在客户端的 `/etc/sysconfig/network` 文件中添加 `PEERDNS=no`。）

若要更改 `dhcpd` 命令接受来自 DHCP 服务器信息的工作方式，你可以向 `dhcpd` 命令传递选项。通过向 `/etc/sysconfig/network` 配置文件中的 `DHCPDARGS` 变量添加参数来执行此操作。例如，`DHCPDARGS="-g"` 会使 `ifup` 脚本以调试模式运行 `dhcpd`，从而将消息发送到 `/var/log/messages` 文件。（输入 `man dhcpd` 以查看其他 `dhcpd` 选项。）

> **注意：** `dhcpd` 守护程序假定你的 DHCP 服务器可以在你的第一个以太网接口（`eth0`）上访问。如果你希望客户端从不同的接口获取 DHCP 信息，你可以将接口名称（`eth1`、`eth2` 等）添加到 `dhcpd` 命令行中。例如，要执行此操作，你可以向 `/etc/sysconfig/network` 文件添加 `DHCPDARGS=eth1`。

## 了解网络信息服务

网络信息服务（NIS）由 Sun Microsystems 创建，作为一种在网络上的一组主机计算机之间管理共享信息的方式。使用 NIS，计算机可以共享一组通用的用户账户、用户组和 TCP/IP 主机名，以及其他信息。

> **注意：** NIS 最初称为“黄页”（Yellow Pages），但由于该名称已被注册为商标，Sun 不得不更改此名称。有些人仍将 NIS 称为 *YP*，许多 NIS 命令（甚至 NIS 包名称）以 *'yp.'* 开头。

你通过 NIS 共享的信息来自 UNIX 系统使用的文件，因此与其他类 UNIX 系统（如 Red Hat Linux）兼容。主 NIS 服务器支持的计算机组称为 NIS 域。该域是一组定义好的主机计算机，它们可能也可能不是 TCP/IP 域中包含的同一组计算机。

使用 NIS，管理员从常见的 UNIX（或 Linux）系统文件创建称为*映射*的信息数据库。NIS 映射在*主 NIS 服务器*上创建，并且可以从该服务器访问其他主机计算机。为防止主服务器宕机或不可访问，可以定义一个或多个从服务器。NIS 从服务器包含 NIS 映射的副本，并可以在主服务器不可用时向客户端计算机提供这些信息。然而，NIS 从服务器不用于创建映射。

当映射在 NIS 域中的计算机之间共享后，主要结果是所有计算机共享一组通用的用户和网络配置。以下是可供 NIS 共享的文件列表（并非所有文件默认都设置为共享）。

- `/etc/group` — 定义计算机上用户所属的组。
- `/etc/passwd` — 定义在计算机上设有账户的用户。
- `/etc/shadow` — 包含在 `/etc/passwd` 文件中设置的用户加密密码。
- `/etc/gshadow` — 包含与 `/etc/groups` 文件中包含的组相关联的加密密码。（此文件是可选的，通常不使用。）
- `/etc/passwd.adjunct` — 如果你的系统不使用影子密码，则用于保护密码条目。（此文件用于 SunOS 系统。）
- `/etc/aliases` — 包含用于邮件的用户别名。它允许发送到特定用户名的邮件被重定向到不同的用户（或一组用户）。在某些系统上，此文件可能是 `/etc/mailaliases`。
- `/etc/ethers` — 由 RARP 用于将以太网地址映射为 IP 号码。此文件是可选的。（默认情况下，Red Hat Linux 中未配置 RARP 支持。）
- `/etc/bootparams` — 包含启动无盘工作站所需的条目（通常用于启动 Sun Microsystems 无盘工作站）。
- `/etc/hosts` — 包含可在 TCP/IP 网络上访问的计算机名称和 IP 地址。（通常用于包含私有 LAN 的所有地址，而互联网地址则从 DNS 服务器确定。）
- `/etc/networks` — 用于为网络附加名称。这样，你可以按名称而不是按号码引用网络。
- `/etc/printcap` — 包含打印机定义。
- `/etc/protocols` — 识别分配给不同互联网网络协议（如 IP、TCP、UDP 等）的号码。
- `/etc/publickey` — 在某些 UNIX 系统中用于包含用户名以及用于 NFS 和相关功能安全网络的相关公钥和私钥。
- `/etc/rpc` — 包含受支持的远程过程调用（rpc）协议列表。这些协议用于 Sun Microsystems UNIX 系统，以允许请求网络服务（如 NIS 等）。
- `/etc/services` — 包含识别与互联网协议一起使用的受支持网络服务的端口号和协议的列表。
- `/etc/netgroup` — 用于定义用户（来自特定主机和域），用于与远程挂载、远程 shell 和远程登录相关的权限检查。
- `/etc/netid` — 包含将 RPC 网络名称映射到 UNIX 凭据的信息。

> **注意：** 上述某些文件可能不适用于你的 Red Hat Linux 系统。如果这些文件中有一些不存在，请不要担心。在设置系统的过程中（添加用户、配置网络等），你会设置所需的文件。

尽管这些文件是在 /etc 目录中创建的，但 NIS 管理员可以将这些文件复制到不同位置并进行修改，以免共享主 NIS 服务器的原始配置文件。NIS 管理员还可以根据需要向此列表添加文件或从列表中删除文件。当配置 NIS 客户端计算机时，此配置信息可以从 NIS 主服务器获取。

## 将 Red Hat Linux 设置为 NIS 客户端

如果你的网络使用 NIS 集中管理用户、组、网络地址和其他信息，你可以将 Red Hat Linux 系统设置为使用这些信息作为 NIS 客户端。要将 Red Hat Linux 配置为 NIS 客户端，你需要从 NIS 管理员那里获取以下信息：

