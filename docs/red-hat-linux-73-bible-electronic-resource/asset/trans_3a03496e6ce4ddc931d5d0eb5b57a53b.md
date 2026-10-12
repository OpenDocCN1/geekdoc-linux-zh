

## 表 23-2：DHCP 选项

| 选项 | 描述 |
| :--- | :--- |
| **名称、地址和时间** | |
| `option host-name string;` | 指示客户端计算机可用于标识自身的名称。它既可以是简单的主机名（例如，`pine`），也可以是完全限定的域名（例如，`pine.handsonhistory.com`）。您可以将其用于主机声明中，在那里通过以太网地址来标识一台主机计算机。 |
| `option domain-name string;` | 标识客户端应用于解析 DNS 主机名的默认域名。 |
| `option subnet-mask ip-address;` | 将子网掩码与 IP 地址关联。例如，`option 255.0.0.0 10.0.0.1;`。 |
| `option time-offset int32;` | 指示与世界协调时（UTC）的偏移量（以秒为单位）。例如，六小时的 UTC 偏移量设置如下：`option time-offset 21600;`。 |
| **服务器和路由器** | |
| `option routers ip-address [, ip-address... ];` | 按优先级顺序列出连接到本地子网的一个或多个路由器。客户端可以将此值称为网关。 |
| `option domain-name-servers ip-address [, ip-address... ];` | 列出客户端可用于将名称解析为 IP 地址的一个或多个域名系统（DNS）服务器。按应尝试的顺序列出服务器。 |
| `option time-servers ip-address [, ip-address... ];` | 按优先级顺序列出可供 DHCP 客户端使用的一个或多个时间服务器。 |
| `option ien116-name-servers ip-address [, ip-address... ];` | 按优先级顺序列出客户端可使用的一个或多个 IEN 116 名称服务器。（IEN 116 名称服务器早于现代 DNS 服务器，被视为过时。） |
| `option log-servers ip-address [, ip-address... ];` | 列出一个或多个 MIT-LCS UDP 日志服务器。按应尝试的顺序列出服务器。 |
| `option cookie-servers ip-address [, ip-address... ];` | 列出一个或多个每日名言（cookie）服务器（参见 RFC 865）。按应尝试的顺序列出服务器。 |
| `option lpr-servers ip-address [, ip-address... ];` | 列出可用的一个或多个行式打印机服务器。按应尝试的顺序列出服务器。 |
| `option impress-servers ip-address [, ip-address... ];` | 列出一个或多个 Imagen Impress 图像服务器。按应尝试的顺序列出服务器。 |
| `option resource-location-servers ip-address [, ip-address... ];` | 列出一个或多个资源位置服务器（RFC 887）。按应尝试的顺序列出服务器。 |
| `option nis-domain string;` | 指示 NIS 域的名称（如果客户端有可用的 NIS 服务器）。 |
| `option nis-servers ip-address [, ip-address... ];` | 按优先级顺序列出客户端可用的 NIS 服务器地址。 |
| `option ntp-servers ip-address [, ip-address... ];` | 按优先级顺序列出网络时间协议服务器地址。 |
| `option netbios-name-servers ip-address [, ip-address... ];` | 列出用于 NetBIOS 名称解析（用于 Windows 文件和打印共享）的 WINS 服务器地址。 |
| `option netbios-dd-server ip-address [, ip-address... ];` | 按优先级顺序列出 NetBIOS 数据报分发（NBDD）服务器地址。 |
| `option netbios-node-type uint8;` | 包含一个数字（单八位字节），指示如何确定 NetBIOS 名称（用于基于 TCP/IP 的 NetBIOS）。可接受的值包括：1（广播：无 WINS）、2（对等：仅 WINS）、4（混合：先广播，后 WINS）、8（杂凑：先 WINS，后广播）。 |
| `option font-servers ip-address [, ip-address... ];` | 指示客户端可使用的一个或多个 X Window 字体服务器的位置，按优先级顺序列出。 |
| `option nisplus-domain string;` | 指示 NIS+ 域的 NIS 域名。 |
| `option nisplus-servers ip-address [, ip-address... ];` | 按优先级顺序列出客户端可用的 NIS+ 服务器地址。 |
| `option smtp-server ip-address [, ip-address... ];` | 按优先级顺序列出客户端可用的 SMTP 服务器地址。 |
| `option pop-server ip-address [, ip-address... ];` | 按优先级顺序列出客户端可用的 POP3 服务器地址。 |
| `option nntp-server ip-address [, ip-address... ];` | 按优先级顺序列出客户端可用的 NNTP 服务器地址。 |
| `option www-server ip-address [, ip-address... ];` | 按优先级顺序列出客户端可用的 WWW 服务器地址。 |
| `option finger-server ip-address [, ip-address... ];` | 按优先级顺序列出客户端可用的 Finger 服务器地址。 |
| `option irc-server ip-address [, ip-address... ];` | 按优先级顺序列出客户端可用的 IRC 服务器地址。 |
| **路由** | |
| `option ip-forwarding flag;` | 指示客户端是否应允许（1）或不允许（0）IP 转发。如果客户端充当路由器，则允许此操作。 |
| `option non-local-source-routing flag;` | 指示是否应允许（1）或禁止（0）转发具有非本地源路由的数据报。 |
| `option static-routes ip-address ip-address [, ip-address ip-address... ];` | 指定客户端应到达特定主机时应使用的静态路由。（按优先级降序列出到同一位置的多条路由。） |
| `option router-discovery flag;` | 指示客户端是否应尝试使用路由器发现机制来发现路由器（1）或不发现（0）。 |
| `option router-solicitation-address ip-address;` | 指示客户端应使用何种地址来发送路由器请求报文。 |
| **瘦客户端** | |
| `option boot-size uint16;` | 指示客户端计算机用于启动的默认启动映像的大小（以 512 字节块为单位）。 |
| `option merit-dump string;` | 指示如果客户端崩溃，核心映像应转储到哪里。 |
| `option swap-server ip-address;` | 指示客户端计算机的交换服务器位于何处。 |
| `option root-path string;` | 指示客户端使用的根磁盘的位置（路径名）。 |
| `option tftp-server-name string;` | 指示客户端应使用何种 TFTP 服务器来传输启动映像。在 DHCP 客户端中比在 BOOTP 客户端中更常用。 |
| `option bootfile-name string;` | 指示用于启动客户端的引导文件的位置。在 DHCP 客户端中比在 BOOTP 客户端中更常用。 |
| `option x-display-manager [ip-address, ip-address... ];` | 按优先级顺序指示客户端可使用的 X Window System 显示管理器服务器的位置。 |

## 启动 DHCP 服务器

配置 /etc/dhcpd.conf 文件后，您可以立即启动 DHCP 服务器。作为 root 用户，在终端窗口中输入以下内容：

```
# /etc/init.d/dhcpd start
```

您的 DHCP 服务器现在应该可以向您 LAN 中的计算机分发信息。如果 LAN 中有客户端计算机在等待您的 DHCP 服务器，它们的网络接口现在应该处于活动状态。

如果一切运行正常，您可以通过如下方式启用 dhcpd 服务，让 DHCP 服务器在每次计算机启动时自动启动：

```
# chkconfig dhcpd on
```

有几种方法可以检查您的 DHCP 服务器是否正在工作：

- 检查 /var/lib/dhcp/dhcpd.leases 文件。如果客户端已成功从 DHCP 服务器获取地址，该文件中应出现一条租约行。对于每个已租用 IP 地址的客户端，应有一组看起来像以下这样的信息：

```
lease 10.0.0.100 {
starts 2 2002/05/04 03:48:12;
```

