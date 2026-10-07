
在你的网络上配置了 DHCP 后，客户端计算机只需表示它想使用 DHCP，DHCP 服务器就可以为其提供 IP 地址、子网掩码、DNS 服务器、NetBIOS、路由器（网关）以及在网络上运行所需的其他信息。

通过 DHCP，你可以极大地简化网络上每台客户端计算机所需的初始网络配置。稍后，随着网络的演进，你可以轻松地更新这些信息，并在客户端重启接口时自动捕获这些变化。

## 设置 DHCP 服务器

假设你已经设置了 DHCP 服务器与网络上客户端计算机之间的物理连接（假设是以太网局域网），让 DHCP 服务器工作所需的最少工具是：

- 一个允许 DHCP 访问的防火墙
- 一个配置好的 `/etc/dhcp.conf` 文件
- 一个正在运行的 `dhcpd` 守护进程（可以在启动时启动）

DHCP 服务器运行后，它会向局域网广播其作为 DHCP 服务器的可用性。客户端只需启动（打开以太网接口并将 DHCP 识别为其获取网络地址的方法），其在网络上运行所需的信息将从服务器传输给它。

> 注意：`dhcp.conf` 文件可以为 DHCP 客户端提供广泛的配置信息。要查看在该文件中可以设置的全set选项和参数，请参阅 `dhcp-options` 和 `dhcp.conf` 手页（输入 `man dhcp-options`）。

## 为 DHCP 开放防火墙

你 DHCP 服务器上的防火墙必须配置为允许访问 UDP 端口 67 和 68。如果你正在使用 `iptables`（且在安装期间没有开启端口），你可以为 `iptables` 添加新规则并永久保存更改。以 root 用户身份输入以下：

```bash
# iptables -I INPUT -i eth0 -p udp --sport 67:68 --dport 67:68 -j ACCEPT
```

在此示例中，允许来自 `eth0` 接口（即你的第一块以太网卡）端口 67 和 68 的请求。如果你的 DHCP 服务器同时还是你网络的路由防火墙，你希望确保只对你的局域网提供 DHCP 服务，而不面向互联网。（你需要确定 `eth0`、`eth1` 还是其他网卡连接到你的局域网。）

如果规则被接受（输入 `iptables -L` 确保），你可以保存整个防火墙配置，以便新规则被永久包含在内。这样做，你输入以下内容（作为 root 用户）：

```bash
# iptables-save > /etc/sysconfig/iptables
```

这将更新你的 `/etc/sysconfig/iptables` 文件，以便在下次重启 `iptables` 时包含所有当前规则（包括你刚刚添加的规则）。

## 配置 dhcpcd.conf 文件

假设你有一个 IP 地址池，想要将其分发给一组位于同一子网的计算机。换句话说，所有计算机都连接到一个集线器（或一组串联的集线器）。以下是一个简单的 `dhcpcd.conf` 文件的示例：

```conf
ddns-update-style interim;
ignore client-updates;

subnet 10.0.0.0 netmask 255.0.0.0 {
    option routers 10.0.0.1;
    range 10.0.0.10 10.0.0.100;
    range 10.0.0.200 10.0.0.250;
}

host ns {
    hardware ethernet 00:04:5A:4F:8E:47;
    fixed-address 10.0.0.254;
    option default-lease-time 16600;
    option max-lease-time 43200;
}
```

## 第 23 章：设置启动服务器：DHCP 和 NIS

在这些示例中，`netbios-name-servers` 选项定义了 WINS 服务器的位置（如果你正在使用 Samba 进行 Windows 文件和打印服务器共享）。`time-servers` 选项设置网络上时间服务器的位置。

- DHCP 服务器可用于为在网络启动的 X 终端或无盘工作站提供信息。以下是一个你可以用于启动网络上此类计算机的定义示例：

```
host maple {
  filename = "/dwboot/maple.nb"; hardware ethernet 00:04:5A:4F:8E:47;
  fixed-address 10.0.0.150;
}
```

在上例中，工作站从 DHCP 服务器使用的启动文件位于 `/dwboot/maple.nb`。`hardware ethernet` 值标识了客户端以太网卡的地址。客户端的 IP 地址被设置为 `10.0.0.150`。所有这些行都包含在一个主机定义中，其中主机名定义为 `maple`。（请参见表 23-2 中的“瘦客户端”标题，获取其他对配置客户端可能有选项。）

## 添加选项

你可以在 `/etc/dhcpd.conf` 文件中使用几十个选项，将信息从 DHCP 服务器传递给 DHCP 客户端。表 23-1 描述了你可以用于不同选项的数据类型。表 23-2 描述了可用的选项。

### 表 23-1：数据类型

| 数据类型 | 描述 |
|---|---|
| ip-address | 以 IP 地址数字 (11.111.111.11) 或完全限定域名 (comp1.history.com) 输入 ip-address。要使用域名，该名称必须能够解析为 IP 地址。 |
| int32, int16, int8, uint32, uint8 | 用于表示符号和无符号的 32 位、16 位和 8 位整数。 |
| "string" | 输入由双引号围绕的字符字符串。 |
| Boolean | 在需要布尔值时输入 `true` 或 `false`。 |
| data-string | 输入引号中的字符字符串 ("client1") 或十六进制字节串 (00:04:5A:4F:8E:47)。 |

## 第四部分：Fedora 网络和服务器设置

选项包含了从 DHCP 服务器传递到客户端的值。尽管表 23-2 列出了这些值，但客户端计算机将无法使用你可能传递给它的每一个每一个值。换句话说，并不是所有选项在所有情况下都是适当的。

表 23-2 分为以下几类：

- *名称、地址和时间* — 这些选项设置客户端使用的值，用于定义其主机名、域名、网络号和时间（相对于 GMT 的偏移量）。
- *服务器和路由器* — 这些选项用于告诉 DHCP 客户端在网络上的何处找到路由器和服务器。虽然列出了十多种服务器类型，但通常你只需要指示路由器的地址，而 DNS 服务器将使用它。
- *路由* — 这些选项指示客户端是否路由数据包。
- *瘦客户端* — 如果 DHCP 被用作客户端的启动服务器，这些选项非常有用。客户端可能是一个具有处理能力 X 终端或无盘工作站，但没有磁盘（或磁盘非常小），因此无法自行存储启动镜像和文件系统。

### 表 23-2：DHCP 选项

| 选项 | 描述 |
| --- | --- |
| option *host-name string;* | *指示客户端计算机可以用于标识自身的名称。它可以是一个简单的主机名（例如 pine），也可以是一个完全限定域名（例如 pine.handhistory.com）。你可以在主机声明中使用此项，其中主机计算机通过以太网地址进行识别。* |
| option *domain-name string;* | 标识客户端在解析 DNS 主机名时应使用的默认域名。 |
| option *subnet-mask ip-address;* | 将子网掩码与 IP 地址相关联。例如，*option 255.0.0.0 10.0.0.1*。 |
| option *time-offset int32;* | 指示与协调世界时 (UTC) 的偏移量（秒为单位）。例如，六小时的 UTC 偏移设置如下：*option time-offset 21600;*。 |
| 服务器和路由器 | 描述 |
|---|---|
| option routers ip-address [, ip-address...]; | 按优先级顺序列出连接到本地子网的一个或多个路由器。客户端可能将此值视为网关。 |
| option domain-name-servers ip-address [, ip-address...]; | 列出客户端可用于将名称解析为 IP 地址的一个或多个域名系统 (DNS) 服务器。按尝试的顺序列出服务器。 |
| option time-servers ip-address [, ip-address...]; | 按优先级顺序列出 DHCP 客户端可以使用的一个或多个时间服务器。 |
| option ien116-name-servers ip-address [, ip-address...]; | 按优先级顺序列出客户端可以使用的一个或多个 IEN 116 名称服务器。（IEN 116 名称服务器是现代 DNS 服务器的前身，被认为已过时。） |
| option log-servers ip-address [, ip-address...]; | 按优先级顺序列出一个或多个日志服务器。 |
| option cookie-servers ip-address [, ip-address...]; | 按尝试顺序列出一个或多个 cookie 服务器（RFC 865）。 |
| option ip-servers ip-address [, ip-address...]; | 按尝试顺序列出一个打印服务器。 |
| option impress-servers ip-address [, ip-address...]; | 按尝试顺序列出一个或多个印象服务器。 |
| option resource-location-servers ip-address [, ip-address...]; | 按尝试顺序列出一个或多个资源位置服务器（RFC 887）。 |
| option nis-domain string; | 指示 NIS 域，如果可用。 |
| option nis-servers ip-address [, ip-address...]; | 按优先级顺序列出 NIS 服务器。 |
| option ntp-servers ip-address [, ip-address...]; | 按优先级顺序列出网络时间协议服务器。 |
| 选项 | 描述 |
|---|---|
| option netbios-name-servers ip-address [, ip-address...]; | 列出 WINS 服务器（用于 Windows 文件和打印服务器共享）。 |
| option netbios-dd-server ip-address [, | | 按优先级顺序列出 NetBIOS 数据报分布 (NBDD) 服务器。 |
| option netbios-node-type uint8 | 包含一个数字（单字节），指示 NetBIOS 名称是如何确定的（通过 TCP/IP）。有效值包括：1（广播：无 WINS），2（点对点：仅限 WINS），4（混合：广播，WINS），8（混合：WINS，后广播）。 |
| option font-servers ip-address [, ip-address...]; | 按优先级顺序列出一个或多个 X 字体服务器。 |
| option nisplus-domain string; | 指示 NIS+ 域名。 |
| option nisplus-servers ip-address [, ip-address...]; | 按优先级顺序列出 NIS+ 服务器。 |

## 第 23 章：设置启动服务器：DHCP 和 NIS

| 选项 | 描述 |
|---||---|
| **路由** | |
| option ip-forwarding flag; | 指客户端是否应允许 (1) 或不允许 (0) IP 转发。如果客户端作为路由器运行，则允许此操作。 |
| option non-local-source-routing flag; | 指客户端是否应允许 (1) 或禁止 (0) 转发带有非本地源路由的数据报文。 |
| option static-routes ip-address address [, ip-address ip-address...]; | 指定客户端访问特定主机时应使用的静态路由。（按优先级降序排列列出指向同一位置的多个路由。） |
| option router-discovery flag; | 指客户端是否应尝试使用路由器发现机制发现路由器 (1) 或不发现 (0)。 |
| option router-solicitation-address address; | 指客户端应使用用于发送路由器请求请求的地址。 |
| **瘦客户端** | |
| option boot-size uint16; | 指客户端计算机用于启动时使用的默认启动镜像的大小（以 512 字节块为单位）。 |
| option merit-dump string; | 指客户端崩溃时核心镜像应转储的位置。 |
| option swap-server ip-address; | 指客户端计算机交换服务器所在的位置。 |
| option root-path string; | 指客户端使用的根磁盘所在位置（路径名）。 |
| option tftp-server-name string; | 指客户端应用于传输启动镜像的 TFTP 服务器名称。与 BOOTP 客户端相比，更多地用于 DHCP 客户端。 |
| option bootfile-name string; | 指用于启动客户端的引导文件的位置。与 BOOTP 客户端相比，更多地用于 DHCP 客户端。 |
| option x-display-manager ip-address [ , ip-address...]; | 指客户端可以使用 X 窗口显示管理器服务器的位置，按优先级顺序排序。 |

## 启动 DHCP 服务器

配置 `/etc/dhcpd.conf` 文件后，可以立即启动 DHCP 服务器。在终端窗口中以 root 用户身份输入以下命令：

```bash
# service dhcpd start
```

现在，您的 DHCP 服务器应该可以开始向局域网（LAN）上的计算机分发信息了。如果局域网上有等待 DHCP 服务器的客户端，它们的网络接口现在应该是处于激活状态。

如果一切运行正常，您可以通过以下方式开启 `dhcpd` 服务，以便在每次计算机启动时自动启动您的 DHCP 服务器：

```bash
# chconfig dhcpd on
```

有几种方法可以验证您的 DHCP 服务器是否正常工作：

- 检查 `/var/lib/dhcp/dhcpd.leases` 文件。如果客户端成功从 DHCP 服务器分配了地址，文件中应该出现一条租约行。对于每个租用 IP 地址的客户端，都应该有一组如下所示的信息：

```
lease 10.0.0.225 {
  starts 2002/05/04 03:48:12;
  ends 2002/05/04 15:48:12;
  hardware ethernet 00:50:ba:d8:03:9e;
  client-hostname "pine";
}
```

- 开启 Ethereal 窗口（在终端窗口输入 `ethereal&`）并开始捕获数据（混杂模式）。重启 DHCP 服务器并重启客户端上的网络接口。您应该看到一系列 DHCP 数据包，显示序列如下：DHCP Offer、DHCP Discover、DHCP Offer、DHCP ACK。

- 从客户端计算机，您应该能够开始进行网络通信。如果客户端是 Linux 系统，输入 `ifconfig -a` 命令。您的以太网接口（可能是 `eth0`）应该出现，且 IP 地址已设置为由 DHCP 服务器分配的地址。

当服务器运行正常时，您可以继续向网络中添加 DHCP 客户端，从您分配的地址池中获取地址。

## 设置 DHCP 客户端

配置网络客户端从您的 DHCP 服务器获取地址非常简单。然而，不同类型的操作系统使用 DHCP 的方式不同。以下是设置 Windows 和 Linux DHCP 客户端的示例。

Windows：

1. 从大多数 Windows 操作系统（Windows 95, 98, 2000, ME 等）中，从控制面板打开“网络”窗口（开始 -> 设置 -> 控制面板）。
2. 在“配置”选项卡中，点击与以太网卡相关的 TCP/IP 接口（类似于 TCP/IP -> 3Com EtherLink III）。
3. 点击“属性”。出现属性窗口。
4. 点击“IP 地址”选项卡，然后勾选“自动获得 IP 地址”复选框。
5. 点击“确定”并重启计算机，以便客户端可以使用新的 IP 地址。

Linux：

1. 在初始安装 Linux 时，在“网络配置”屏幕上点击“使用 DHCP 配置”。您的网络客户端在启动时应自动从您的 DHCP 服务器获取 IP 地址。
2. 若要在安装后设置 DHCP，请打开网络配置窗口（使用 `neat` 命令）。
3. 从网络配置窗口：
   a. 点击“设备”选项卡（默认值）。
   b. 点击您的以太网设备（可能是 `eth0`）。
   c. 点击“编辑”。
   d. 点击“常规”选项卡。
   e. 点击“自动获取地址”并选择 `dhcp`。
   f. 点击“确定”。
   g. 点击“应用”。
4. 然后，从终端窗口执行：

```bash
# service network
```
