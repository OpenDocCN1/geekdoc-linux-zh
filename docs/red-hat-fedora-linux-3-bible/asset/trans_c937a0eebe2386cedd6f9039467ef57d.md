
## DHCP 预留

- 您可以为特定的主机计算机设置固定地址，也称为**地址预留**。特别是，您希望针对服务器计算机执行此操作，以确保其地址不会更改。虽然您可以简单地从 DHCP 分配地址池中省略固定 IP 地址，但您将失去对 IP 配置的集中管理。DHCP 预留允许您集中配置所有 IP 地址信息。实现此目的的一种方法基于服务器以太网卡的以太网硬件地址。该计算机的所有信息都可以包含在主机定义中，例如以下示例：

```
host pine {
   hardware ethernet 00:04:5A:4F:8E:47;
   fixed-address 10.0.0.254;
}
```

在此处，当 DHCP 服务器遇到该以太网地址时，**fixed-address**（10.0.0.254）将被分配给该地址。在服务器计算机上输入 **ifconfig -a** 以查看其以太网硬件地址（前提是接口处于活动状态）。在此主机定义内，您还可以添加其他选项。例如，您可以设置不同路由的位置（*routers* 选项）。

- 许多选项允许您定义各种服务器类型的位置。这些选项可以全局设置，也可以在特定的主机或子网定义中设置。例如：

```
option netbios-name-servers 10.0.0.252;
option time-servers 10.0.0.253;
```

在这些示例中，**netbios-name-servers** 选项定义了 WINS 服务器的位置（如果您正在使用 Samba 进行 Windows 文件和打印服务器共享）。**time-servers** 选项设置网络上时间服务器的位置。

- 可以使用 DHCP 服务器提供 X 终端或无盘工作站在网络上启动时所需的信息。以下是一个可用于在网络上启动此类计算机的定义示例：

```
host maple {
   filename "/dwboot/maple.nb";
   hardware ethernet 00:04:5A:4F:8E:47;
   fixed-address 10.0.0.150;
}
```

在上面的示例中，无盘工作站从 DHCP 服务器使用的启动文件位于 */dwboot/maple.nb*。**hardware ethernet** 值标识客户端上以太网卡片的地址。客户端的 IP 地址设置为 10.0.0.150。所有这些行都包含在一个主机定义中，其中主机名定义为 **maple**。（有关可能有助于配置瘦客户端的其他选项，请参阅表 23-2 中的瘦客户端标题。）

`/etc/dhcpd.conf` 文件中有数十个选项可用于将信息从 DHCP 服务器传递给 DHCP 客户端。表 23-1 描述了可用于不同选项的数据类型。表 23-2 描述了可用的选项。

### 表 23-1：数据类型

| 数据类型 | 描述 |
| --- | --- |
| ip-address | 将 ip-address 输入为 IP 地址数字（11.111.111.11）或完全限定域名（comp1.handsontest.com）。若要使用域名，该名称必须能解析为 IP 地址数字。 |
| int32, int16, int8, uint32, uint16, uint8 | 用于表示带符号和无符号的 32 位、16 位和 8 位整数。 |
| "string" | 输入由双引号包围的字符串。 |
| Boolean | 当需要布尔值时，输入 true 或 false。 |
| data-string | 输入引号中的字符串（"client1"）或十六进制八位字节序列（00:04:5A:4F:8E:47）。 |

选项包含从 DHCP 服务器传递到客户端的值。虽然表 23-2 列出了有效选项，但客户端计算机无法使用您可能传递给它的每个值。换句话说，并非所有选项在所有情况下都适用。

表 23-2 分为以下几个类别：

- **名称、地址和时间** — 这些选项设置用于定义客户端的主机名、域名、网络编号和时间（与 GMT 的偏移量）的值。
- **服务器和路由器** — 这些选项用于告知 DHCP 客户端在网络上哪里可以找到路由器和服务器。虽然列出了十多种服务器类型，但通常您只需指示客户端将使用的路由器和 DNS 服务器的地址。
- **路由** — 这些选项指示客户端是否路由数据包。
- **瘦客户端** — 如果将 DHCP 用作瘦客户端的启动服务器，这些选项非常有用。瘦客户端可能是 X 终端或无盘工作站，它具有处理能力，但没有磁盘（或非常小的磁盘），因此无法自行存储启动映像和文件系统。

### 表 23-2：DHCP 选项

| 选项 | 描述 |
| --- | --- |
| **名称、地址和时间** | |
| `option host-name string;` | 指示客户端计算机可用于标识自身的名称。它可以是简单的主机名（例如，`pine`）或完全限定域名（例如，`pine.handsonhistory.com`）。您可以在主机声明中使用此选项，其中主机计算机通过以太网地址进行标识。 |
| `option domain-name string;` | 标识客户端用于解析 DNS 主机名的默认域名。 |
| `option subnet-mask ip-address;` | 将子网掩码与 IP 地址关联。例如，`option 255.0.0.0 10.0.0.1;`。 |
| `option time-offset int32;` | 指示与协调世界时（UTC）的偏移量（以秒为单位）。例如，6 小时的 UTC 偏移量设置如下：`option time-offset 21600;`。 |
| **服务器和路由器** | |
| `option routers ip-address [, ip-address...];` | 按优先级顺序列出连接在本地子网上的一个或多个路由器。客户端可能将此值称为网关。 |
| `option domain-name-servers ip-address [, ip-address...];` | 列出客户端可用于将名称解析为 IP 地址的一个或多个域名系统（DNS）服务器。按应尝试的顺序列出服务器。 |
| `option time-servers ip-address [, ip-address...];` | 按优先级顺序列出一个或多个可被 DHCP 客户端使用的时间服务器。 |
| `option ien116-name-servers ip-address [, ip-address...];` | 按优先级顺序列出一个或多个可被客户端使用的 IEN 116 名称服务器。（IEN 116 名称服务器早于现代 DNS 服务器，现已被视为过时。） |
| `option log-servers ip-address [, ip-address... ];` | 列出 MIT-LCS UDP 日志服务器中的一个或多个。按应尝试的顺序列出服务器。 |
| `option cookie-servers ip-address [, ip-address... ];` | 列出每日一句（cookie）服务器中的一个或多个（参见 RFC 865）。按应尝试的顺序列出服务器。 |
| `option lp-servers ip-address [, ip-address... ];` | 列出可用的行式打印机服务器中的一个或多个。按应尝试的顺序列出服务器。 |
| `option impress-servers ip-address [, ip-address... ];` | 列出 Impress 图像服务器中的一个或多个。按应尝试的顺序列出服务器。 |
| `option resource-location-servers ip-address [, ip-address... ];` | 列出资源位置服务器（RFC 887）中的一个或多个。按应尝试的顺序列出服务器。 |
| `option nis-domain string;` | 如果客户端有可用的 NIS 服务器，则指示 NIS 域的名称。 |
| `option nis-servers ip-address [, ip-address... ];` | 按优先级顺序列出客户端可用的 NIS 服务器的地址。 |
| `option ntp-servers ip-address [, ip-address... ];` | 按优先级顺序列出网络时间协议服务器的地址。 |
| `option netbios-name-servers ip-address [, ip-address... ];` | 列出 WINS 服务器的地址，用于 NetBIOS 名称解析（用于 Windows 文件和打印共享）。 |
| `option netbios-dd-server ip-address [, ip-address... ];` | 按优先级顺序列出 NetBIOS 数据报分发（NBDD）服务器的地址。 |
| `option netbios-node-type uint8;` | 包含一个数字（单个八位字节），指示如何确定 NetBIOS 名称（与 TCP/IP 上的 NetBIOS 配合使用）。可接受的值包括：1（广播；无 WINS），2（对等：仅 WINS），4（混合：先广播，后 WINS），8（混合：先 WINS，后广播）。 |
| `option font-servers ip-address [, ip-address... ];` | 指示客户端可使用的一个或多个 X 窗口字体服务器的位置，按优先级顺序列出。 |
| `option nisplus-domain string;` | 指示 NIS+ 域的 NIS 域名。 |
| `option nisplus-servers ip-address [, ip-address... ];` | 按优先级顺序列出客户端可用的 NIS+ 服务器的地址。 |
| `option smtp-server ip-address [, ip-address... ];` | 按优先级顺序列出客户端可用的 SMTP 服务器的地址。 |

