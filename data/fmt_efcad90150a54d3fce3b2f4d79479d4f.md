
## 套接字统计信息

- 0 bad segments received.
- 0 resets sent

### Udp

- 757 packets received
- 0 packets to unknown port.
- 0 packet receive errors
- 840 packets sent
- 0 receive buffer errors
- 0 send buffer errors

### Plite:TcpExt

- 219 TCP sockets finished time wait in fast timer
- 15 delayed acks sent
- 26 delayed acks further delayed of locked socket
- Quick ack mode was activated 1 times
- 229343 packet headers predicted
- 289 acknowledgments not containing data received
- 301 predicted acknowledgments
- TCPCoalesce: 7255

### Ext

- Routes: 2
- IncastPkts: 13
- OutcastPkts: 15
- InOctets: 41072578
- OutOctets: 836308
- IncastOctets: 2746
- OutcastOctets: 2826

输出可以大致评估你的 Linux 系统在网络上的繁忙程度。

## 检查套接字

`netstat` 工具提供了丰富的信息，但通常很难确定哪个程序正在监听哪个端口。`ss` 命令可以解决这个问题，显示哪些进程正在使用活跃的网络套接字：

```bash
$ ss -annt
State | Recv-Q | Send-Q | Local Address:Port | Peer Address:Port
| :--- | :--- | :--- | :--- | :--- |
| LISTEN | 0 | 0 | 127.0.0.1:25 | * |
| LISTEN | 0 | 0 | *:111 | * |
| LISTEN | 0 | 0 | 192.168.1.2:53 | * |
| LISTEN | 0 | 0 | *:22 | * |
| LISTEN | 0 | 0 | 127.0.0.1:631 | * |
| LISTEN | 0 | 0 | *:25 | * |
| LISTEN | 0 | 0 | *:111 | * |
| LISTEN | 0 | 0 | *:22 | * |
| LISTEN | 0 | 0 | 127.0.0.1:631 | * |
| ESTAB | 0 | 0 | *:22 | 127.0.0.1:4090 |
| ESTAB | 0 | 0 | *:4090 | 127.0.0.1:22 |
```

`-anpt` 选项显示监听和已建立的 TCP 连接以及它们关联的进程。此输出显示端口 22 有建立连接并由进程控制。

## 练习 7.1 确定网络环境

此练习将演示如何快速评估 Linux 系统的网络配置，无需挖掘大量的配置文件。记录系统网络信息，请遵循以下步骤：

- 以 root 身份登录，或通过 `su` 或 `sudo` 命令获取 root 权限。
- 输入 `ip address` 显示系统当前的网络接口。你可能会看到环回接口（命名为 `lo`）和多个网络接口。记录分配给每个网络接口的 IP（`inet`）和 IPv6（`inet6`）地址，以及硬件地址和网络掩码。
- 如果你的系统有无线网卡，输入 `iwlist wlan0 scan` 查看区域内的访问点。
- 如果你的系统有无线网卡，输入 `iwconfig` 显示网络接口的当前无线设置。
- 输入 `route` 显示系统上的路由。注意分配给系统的默认网关。它应该与分配给系统的 IP 地址在同一个网络上。
- 输入 `cat /etc/resolv.conf` 显示系统的 DNS 设置。
- 输入 `netstat -l` 显示监听传入连接的程序。标记为 `unix` 的项使用环回地址与系统内部其他程序通信。
- 输入 `ss -anpt` 显示系统上开启活跃端口的进程。

## 总结

如果你有正确的工具，将 Linux 系统连接到网络可以是无痛的。要连接 Linux 系统，你需要 IP 地址、掩码地址、路由器、主机名和 DNS 服务器。如果你不在意分配给 Linux 系统的 IP 地址，可以通过 DHCP 自动获取这些值。但是，如果你运行需要静态 IP 地址的 Linux 服务器，你可能需要手动配置这些值。你可以手动修改文件来存储适当的网络信息，也可以使用图形或命令行工具。`Network Manager` 工具是 Linux 发行版中最常用的图形工具。它允许你从图形窗口配置有线和无线网络设置。系统托盘中的 Network Manager 图标显示网络连接性以及无线网卡的基本无线信息。

如果你必须从命令行配置网络设置，你需要几个不同的工具。对于无线连接，使用 `ifconfig` 命令设置无线访问点和 SSID 密钥。对于无线和有线连接，都使用 `ifconfig` 或 `ip` 命令设置接口的 IP 地址和掩码值。你可能还需要使用 `route` 命令定义网络的默认路由器。

要使用 IP 地址的主机名，你必须为你的网络定义 DNS 服务器。在 `/etc/resolv.conf` 配置文件中执行此操作。你还需要 `/etc/hostname` 或 `/etc/hosts` 文件定义 Linux 系统的主机名。

一旦网络配置完成，你可能需要对网络进行额外的故障排除。`ping` 和 `ping6` 命令允许你向远程主机发送 ICMP 数据包以测试连接性。如果你怀疑主机名存在问题，可以使用 `host` 和 `dig` 命令查询 DNS 服务器。

通过在命令中添加 `default` 关键字来指定网络使用的默认路由器（网关）。

总结分析网络设备状态所需的工具。`ifconfig` 和 `ip` 命令显示系统上所有网络接口的当前状态。你还可以使用 `netstat` 或 `ss` 命令显示所有监听网络端口的统计信息。

描述 Linux 如何初始化网络接口。基于 Debian 的 Linux 系统使用 `/etc/network/interfaces` 文件来配置 IP 地址、子网掩码和默认路由器。基于 Red Hat 的 Linux 系统使用 `/etc/sysconfig/network-scripts` 文件夹。`ifcfg-eth0s3` 文件包含 IP 地址和子网掩码设置，而 `network` 文件包含默认路由器设置。新版本的 Ubuntu 使用 Netplan 工具，它在启动时存储网络接口配置，并位于 `/etc/netplan` 文件夹中确定网络配置。

解释如何测试网络连接性。`ping` 和 `ping6` 命令允许你向远程主机发送 ICMP 消息并显示收到的响应。

描述一种在 Linux 中配置网络设置的图形化工具。Network Manager 工具为更改网络接口设置提供了图形化界面。Network Manager 以图标的形式出现在桌面系统的托盘区域。如果你的 Linux 系统使用无线网卡，图标显示为无线信号，而对于有线网络连接，它显示为微网络。当你点击图标时，它会显示当前网络状态，对于无线接口，它会显示检测到的访问点列表。当你打开 Network Manager 界面时，你可以设置静态 IP 地址信息，或配置网络使用 DHCP 服务器动态设置网络配置。

## 复习题

- 1. 哪两个命令可以使用命令行在接口上设置 IP 地址、子网掩码和默认路由器信息？
  - A. `netstat`
  - B. `ping`
  - C. `nmtui`
  - D. `ip`
  - E. `route`

- 2. 新版本的 Ubuntu 使用哪个工具来设置网络地址信息？
  - A. `netstat`
  - B. `Netplan`
  - C. `iwconfig`
  - D. `route`
  - E. `ifconfig`

- 3. 哪个命令显示以太网卡的双工模式设置？
  - A. `ethtool`
  - B. `netstat`
  - C. `iwconfig`
  - D. `iwlist`
  - E. `route`

- 4. 哪个命令显示 Linux 系统上的进程使用了哪些端口？
  - A. `iwconfig`
  - B. `ip`
  - C. `ping`
  - D. `nmtui`
  - E. `ss`

- 5. 如果你的 Linux 服务器没有安装图形化桌面，可以使用哪两个工具从命令行配置网络设置？
  - A. `nmcli`
  - B. `iwconfig`
  - C. `ip`
  - D. `netstat`
  - E. `ping`

- 6. 哪种网络设置定义了路由发往远程网络主机的数据包的网络设备？
  - A. Default router（默认路由器）
  - B. Netmask（子网掩码）
  - C. Hostname（主机）
  - D. IP address（IP 地址）
