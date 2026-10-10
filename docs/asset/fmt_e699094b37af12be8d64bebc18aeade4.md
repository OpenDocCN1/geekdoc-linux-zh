
| `option time-servers ip-address [, ip-address...];` | 按优先级顺序列出 DHCP 客户端可以使用的一个或多个时间服务器。 |
| `option ien116-name-servers ip-address [, ip-address...];` | 按优先级顺序列出客户端可以使用的一个或多个 IEN 116 名称服务器。（IEN 116 名称服务器早于调制解调器 DNS，被认为是过时的）。 |
| `option log-servers ip-address [, ip-address...];` | 列出一个或多个 MIT-LCS UDP 服务器。按应被查询的顺序列出服务器。 |
| `option cookie-servers ip-address [, ip-address...];` | 列出一个或多个每日一言（cookie）服务器（RFC 865）。按应被查询的顺序列出服务器。 |
| `option lpr-servers ip-address [, ip-address...];` | 列出一个或多个可用的行打印机服务器。按应被查询的顺序列出服务器。 |
| `option impress-servers ip-address [, ip-address...];` | 列出一个或多个 Imagen Image 服务器。按应被查询的顺序列出服务器。 |
| `option resource-location-servers ip-address [, ip-address...];` | 列出一个或多个资源位置服务器（RFC 887）。按应被查询的顺序列出服务器。 |
| `option nis-domain string;` | 如果客户端有 NIS 服务器可用，则指明 NIS 域的名称。 |
| `option nis-servers ip-address [, ip-address...];` | 按优先级顺序列出客户端可用的 NIS 服务器地址。 |
| `option ntp-servers ip-address [, ip-address...];` | 按优先级顺序列出网络时间协议服务器的地址。 |
| `option netbios-name-servers ip-address [, ip-address...];` | 列出 WINS 服务器的地址，用于 NetBIOS 名称解析（用于 Windows 文件和打印共享）。 |
| `option netbios-dd-server ip-address [, ip-address...];` | 按优先级顺序列出 NetBIOS 数据报文分布（NBDD）服务器的地址。 |

# 第 23 章：设置启动服务器：DHCP 和 NIS 905

| 选项 | 描述 |
| --- | --- |
| `option netbios-node-type uint8;` | 包含一个数字（单字节），指明 NetBIOS 名称是如何定义的（用于 TCP/IP 上的 NetBIOS）。可接受的值包括：1（广播：WINS），2（对等：仅限 WINS），4（混合：广播、WINS），8（混合：先 WINS，后广播）。 |
| `option font-servers ip-address [, ip-address...];` | 指明客户端可使用的 X Window 显示管理器服务器的位置。 |
| `option nisplus-domain string;` | 指明 NIS+ 域。 |
| `option nis-servers ip-address [, ip-address...];` | 按优先级顺序列出客户端可用的 NIS+ 服务器。 |
| `option smtp-servers ip-address [, ip-address...];` | 列出客户端可用的 SMTP 服务器。 |
| `option pop-servers ip-address [, ip-address...];` | 列出客户端可用的 POP3 服务器。 |
| `option ntp-servers ip-address [, ip-address...];` | 列出客户端可用的 NNTP 服务器。 |
| `option www-servers ip-address [, ip-address...];` | 列出客户端可用的 WWW 服务器。 |
| `option finger-servers ip-address [, ip-address...];` | 列出客户端可用的 Finger 服务器。 |
| `option isc-servers ip-address [, ip-address...];` | 列出客户端可用的 IRC 服务器。 |
| `option ip-forwarding flag;` | 指明客户端是否允许（1）或禁用（0）IP 转发。 |
| `option nonlocal-source-routing flag;` | 指明客户端是否允许（1）或禁用（0）带有本地路由的数据文。 |
| `option static-routes ip-address [, ip-address...];` | 指定客户端使用的静态路由。 |
| `option router-discovery flag;` | 指明客户端是否通过发现机制尝试发现（1）路由器。 |

# 第四部分：Fedora 和 RHEL 网络与服务器设置

| 选项 | 描述 |
| --- | --- |
| `option router-solicitation-address ip-address;` | 指明客户端用于传输请求的地址。 |
| `option boot-size uint16;` | 指明客户端启动时镜像的大小（以 512 字节块计算）。 |
| `option merit-dump string;` | 指明客户端崩溃时转储镜像的位置。 |
| `option swap-server ip-address;` | 指明客户端交换服务器的位置。 |
| `option root-path string;` | 指明客户端使用的根磁盘路径名称。 |
| `option tftp-server-name string;` | 指明客户端用于传输镜像的 TFTP 服务器名称。 |
| `option bootfile-name string;` | 指明用于启动的引导引导的位置。 |
| `option x-display-manager ip-address [, ip-address...];` | 按优先级顺序列出客户端可使用的 X Window 显示管理器服务器的位置。 |

## 启动 DHCP 服务器

在配置 `/etc/dhcp.conf` 文件后，你可以立即启动 DHCP 服务器。

作为 root 用户从终端窗口输入以下内容：

```
# service dhcpd start
```

你的 DHCP 服务器现在应该向局域网内的计算机分发信息。如果局域网内有等待 DHCP 服务器的客户端，它们的网络接口现在应该是激活状态的。

如果一切正常，你可以通过以下方式开启 `dhcpd` 服务，使其在每次计算机启动时自动运行：

```
# chkconfig dhcpd
```

你可以通过几种方法验证你的 DHCP 服务器是否正常工作：

- 检查 `/var/log/messages` 文件。如果 DHCP 服务启动遇到问题，你将在该文件中看到指示问题所在的消息。

## 第23章：设置启动服务器：DHCP 和 NIS 907

- 检查 `/var/lib/dhcp/dhcpd.leases` 文件。如果客户端已从 DHCP 服务器分配了地址，则该文件中应该出现此行。对于每个租用了 IP 地址的客户端，都应该有一组看起来如下的信息：

```
lease 10.0.0.225 {
  starts 2 2006/05/04 03:48:12;
  ends 2 2006/05/04 15:48:12;
  hardware ethernet 00:50:ba:d8:03:9e;
  client-hostname "pine";
}
```

- 从终端窗口中启动 Wireshark（使用 `wireshark&`）并开始捕获数据（使用混杂模式）。重启 DHCP 服务器并重启客户端上的网络接口。你应该能看到一系列 DHCP 数据包，它们显示出如下的序列：DHCP Discover、DHCP Offer、DHCP Request 和 DHCP ACK。

- 从客户端计算机，你应该能够开始在网络上通信。如果客户端是 Linux 系统，使用 `ifconfig -a` 命令。你的以太网接口（可能是 `eth0`）应该会出现，并带有由 DHCP 服务器 分配的 IP 地址。如果你的客户端是 Windows 系统，打开命令提示符并输入 `ipconfig /all`。你将看到所有网络接口的配置信息。

当服务器运行正常时，你可以继续向网络添加 DHCP 客户端，以利用你分配的地址池。

## 设置 DHCP 客户端
