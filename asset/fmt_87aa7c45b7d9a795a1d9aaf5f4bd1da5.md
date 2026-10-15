
这种配置将允许 DHCP 服务器根据客户端所处的子网向其提供不同的信息。

## 添加选项

在 `/etc/dhcp.conf` 文件中，有几十种选项可以将信息从 DHCP 服务器传递给 DHCP 客户端。表 23-1 描述了你可以用于不同选项的数据类型。表 23-2 描述了可用的选项。

## 第 23 章：设置启动服务器：DHCP 和 NIS 885

| 表 23-1: 数据类型 |
| 数据类型 | 说明 |
|---|---|
| ip-address | 输入 ip-address，可以是 IP 地址数字 (11.111.111.11) 或完全限定域名 (compl.handsonhistory.com)。要使用域名，该名称必须能够解析为 IP 地址数字。 |
| int32, int16, int8, uint32, uint16, uint8 | 分别用于表示符号和无符号 32 位、16 位和 8 位整数。 |
| "string" | 输入由双引号围绕的字符串。 |
| Boolean | 在需要布尔值时输入 true 或 false。 |
| data-string | 输入带引号的字符串 ("client1") 或十六进制字节字节串 (00:04:5A:4F:8E:47)。 |

选项（Options）包含了从 DHCP 服务器传递给客户端的值。虽然表 23-2 列出了有效选项，但客户端计算机将无法使用你可能传递给它的每一个值。换句话说，并非所有选项在所有情况下都适用。

表 23-2 分为以下几类：

- *名称、地址和时间* — 这些选项设置客户端用于定义主机名、域名、网络号和时间（相对于 GMT 的偏移量）的值。
- *服务器和路由器* — 这些选项用于告诉网络上的 DHCP 客户端寻找路由器和服务器。虽然列出了十多个服务器，但通常你只需要指定客户端将使用的路由器地址和 DNS 服务器地址。
- *路由* — 这些选项指示客户端是否路由数据包。
- *瘦客户端* — 如果 DHCP 被用作瘦客户端的启动服务器，这些选项非常有用。客户端可能是 X 终端或无盘工作站，它们具有处理能力，但没有磁盘（或磁盘非常小），因此无法无法存储启动镜像和文件系统。

## 表 23-2：DHCP 选项

| 选项 | 说明 |
|---|---|
| 名称、地址和时间 | |
| `option host-name string;` | 指明客户端计算机可用于识别身份的名称。它可以是简单的主机名（例如，`pine`）或完全限定域名（例如，`pine.handsonhistory.com`）。你可以在主机声明中使用它，其中主机通过以太网地址进行标识。 |
| `option domain-name string;` | 标识客户端在解析 DNS 主机时应使用的默认域名。 |
| `option subnet-mask ip-address;` | 将子网掩码与 IP 地址关联。例如，`option 255.0.0.0.1`。 |
| `option time-offset int32;` | 指明相对于协调世界时 (UTC) 的偏移量（秒）。例如，六小时的 UTC 偏移设置如下：`option time-offset 21600;` |
| 服务器和路由器 | |
| `option routers ip-address [, ip-address...];` | 按偏好顺序列出连接到本地子网的一个或多个路由器。客户端可能将此值视为网关。 |
| `option domain-name-servers ip-address [, ip-address...];` | 列出客户端可用于将名称解析为 IP 地址的一个或多个域名系统 (DNS) 服务器。按尝试尝试顺序列出。 |
| `option time-servers ip-address [, ip-address...];` | 按偏好顺序列出 DHCP 客户端可以使用的一个或多个时间服务器。 |
| `option len116-name-servers ip-address [, ip-address...];` | 按偏好顺序列出客户端可以使用的一个或多个 IEN 116 名称服务器。IEN 116 名称服务器早于现代 DNS 服务器，被认为已过。 |

## 第 23 章：设置启动服务器：DHCP 和 NIS 887

| 选项 | 说明 |
| --- | --- |
| `option log-servers ip-address [, ip-address...];` | 列出一个或多个 MIT-LCS UDP 服务器。按尝试顺序列出。 |
| `option cookie-servers ip-address [, ip-address...];` | 列出一个或多个每日一语 (cookie) 服务器（通过 RFC 865）。按尝试顺序列出。 |
| `option lpr-servers ip-address [, ip-address...];` | 列出可用的一个或多个行打印机服务器。按尝试顺序列出。 |
| `option impress-servers ip-address [, ip-address...];` | 列出一个或多个 Imagen Image 服务器。按尝试顺序列出。 |
| `option resource-location-servers [, ip-address...];` | 列出一个或多个资源位置服务器 (RFC 887)。按尝试顺序列出。 |
| `option nis-domain string,` | 如果客户端可用 NIS 服务器，则指明 NIS 域的名称。 |
| `option nis-servers ip-address [, ip-address...];` | 按偏好顺序列出客户端可用的 NIS 服务器地址。 |
| `option ntp-servers ip-address [, ip-address...];` | 按偏好顺序列出网络时间协议服务器地址。 |
| `option netbios-servers ip-address [, ip-address...];` | 按偏好顺序列出客户端可用的 NetBIOS 服务器地址。 |

## 表 23-2：DHCP 选项（续）

| 选项 | 说明 |
| --- | --- |
| `option nis-servers ip-address [, ip-address...];` | 按偏好顺序列出客户端可用的 NIS 服务器地址。 |
| `option ntp-servers ip-address [, ip-address...];` | 按偏好顺序列出网络时间协议服务器地址。 |
| `option netbios-servers ip-address [, ip-address...];` | 按偏好顺序列出客户端可用的 NetBIOS 服务器地址。 |
| `option netbios-type uint16;` | 包含 NetBIOS 类型的数量：1 (广播)，2 (对等)，4 (混合)，8 (混合类型)。 |

# 890 第四部分：红帽 Linux 网络与服务器设置

```
ends 2 2002/05/04 15:48:12;

hardware ethernet 00:50:ba:d8:03:9e;

client-hostname "pine";
```

- 开启以太网轮（从 GNOME 菜单，选择所有应用程序 -> 互联网 -> ethereal）并开始捕获数据（混杂模式）。重启 DHCP 服务器并在客户端上重启网络接口。你将看到一系列 DHCP 数据包，它们显示出如下的序列：DHCP Offer、DHCP Discover、DHCP Request 和 DHCP ACK。
- 从客户端计算机，你应该能够开始与网络通信。如果客户端是 Linux 系统，请使用 `ifconfig -a` 命令。你的以太网接口（可能是 `eth0`）应该出现，其 IP 地址为由 DHCP 服务器分配的地址。

如果服务器运行正常，你可以继续向网络添加 DHCP 客户端或从你分配的地址池中提取。

## 设置 DHCP 客户端

配置网络客户端从你的 DHCP 服务器获取地址非常简单。然而，不同类型的操作系统使用 DHCP 的方法不同。以下是设置 Windows 和红帽 Linux 客户端的示例。

### Windows：

1. 从大多数 Windows 操作系统（Windows 95、98、ME 等）中，从控制面板打开网络窗口（开始 -> 设置 -> 控制面板）。
2. 在“配置”选项卡中，点击与以太网卡相关的 TCP/IP 接口（类似于 TCP/IP -> 3Com EtherLink III）。
3. 点击“属性”。出现属性窗口。
4. 点击“IP 地址”选项卡并选择“自动获得 IP 地址”。
5. 点击“确定”并重启计算机，以便客户端获取新的 IP 地址。

### Red Hat Linux：

1. 在初始安装红帽 Linux 时，在网络配置屏幕上点击“使用 DHCP 配置”。你的网络客户端在启动时会自动从你的 DHCP 服务器获取 IP 地址。
2. 若要在安装后设置 DHCP，请打开网络配置窗口（`neat` 命令）。
3. 从网络配置窗口中：

   a. 点击“设备”选项卡。
   b. 点击你的以太网设备（可能是 `eth0`）。
   c. 点击“编辑”。
   d. 点击“常规”选项卡。
   e. 点击“自动获取 IP 地址设置，使用”并选择 `dhcp`。
   f. 选择“确定”。
   g. 选择“应用”。
4. 然后，从终端窗口输入：

```bash
# /etc/init.d/network restart
```
