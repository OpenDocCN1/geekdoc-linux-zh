
`iptables -I INPUT -i eth0 -p udp --sport 67:68 --dport 67:68 -j ACCEPT`

在本示例中，允许从到目标端口 67 和 68 的请求（`--sport 67:68` 和 `--dport 67:68`）通过 `eth0` 接口（这是你的第一个以太网卡）。DHCP 使用数据报传输协议（UDP）（`-p udp`）。

## 配置 `/etc/dhcp/dhcpd.conf`

假设你有一个 IP 地址池，想要分给同一子网上的计算机。以下是一个简单的 `dhcpd.conf` 示例：

```
dns-update-style none;

option domain-name "handsonhistory.com";

option domain-name-servers 10.0.0.1, 10.0.0.2;

default-lease-time 21600;

dns-update-style none;

subnet 10.0.0.0 netmask 255.255.255.0 {
  option routers 10.0.0.1;
  option subnet-mask 255.255.255.0;
  max-lease-time 43200;
  pool {
    range 10.0.0.150 10.0.0.225;
  }
}

# 设置名称服务器以固定地址出现
host ns {
  next-server ns1.handsonhistory.com;
  hardware ethernet 00:D0:B3:79:B5:35;
  fixed-address 10.0.0.1;
}
```

# 第 23 节：设置 DHCP 服务器

此 DHCP 服务器分派的地址池为 10.0.0.150 到 10.0.0.225，这是由 `range` 行设置的。除了为每个客户端分配 IP 地址外，客户端还会获得关联的子网掩码和域名。

DHCP 服务器分发的 IP 地址是租给每个客户端的特定时间。默认租约时间（`default-lease-time` 此处设置为 21,600 秒，即 6 小时）如果客户端未请求特定时长，则分配的时间。最大租约时间（`max-lease-time` 此处设置为 43,200 秒，即 12 小时）如果客户端请求，服务器将分配的最长时间。客户端可以更新租约，因此它们在在使用 IP 地址时就不必丢失它。

## 扩展 dhcpd.conf 文件

如前所述，这是一个非常简单的示例，适用于单个客户端计算机网络。以下是扩展你的 `dhcpd.conf` 文件的几种示例。

- 如果你在同一子网上有多个地址范围，可以在子网声明中添加多个 `range` 选项。这是一个示例：

```
subnet 10.0.0.0 netmask 255.255.255.0 {
  range 10.0.0.10 10.0.0.100;
  range 10.0.0.200 10.0.0.250;
}
```

此示例导致 DHCP 服务器在网络 10.0 上分配范围 10 之间以及 200 到 250 之间的 IP 地址。

- 你可以为特定的主机计算机设置固定地址，也称为地址预留（address reservations）。特别是，你可能希望对服务器计算机这样做，以确保它们的地址不会发生变化。虽然你可以简单地从 DHCP 分配的地址池中省略固定 IP 地址，但你将失去 IP 配置的集中化管理。DHCP 允许你完全配置所有的 IP 地址信息。实现此点的方法之一基于服务器网卡的以太网硬件地址。所有相关信息都可以包含在主机定义中，如下所示：

```
host pipe {
  hardware ethernet 00:04:5A:4F:8E:47;
  fixed-address 10.0.0.254;
}
```

在这里，当 DHCP 服务器遇到以太网地址时，将为其分配固定地址 10.0.0.254。静态分配 IP 地址是一个好主意。在服务器计算机上输入 `ifconfig` 来查看其以太网硬件地址（当接口处于开启时）。在此主机定义中，你也可以添加其他选项。例如，你可以设置不同路由的位置（`routers`）。

# 第四部分：Fedora RHEL 网络和服务器设置

- 你启用了许多选项来定义各种服务器类型的位置。这些选项可以在全局设置，也可以在特定的后或子集定义中设置。例如：
`option netbios-name-servers 10.0.0.252;`
`option time-servers 10.0.0.253;`

在这些示例中，`netbios-name-servers` 选项定义了 WINS 服务器的位置（如果你在使用基于 Samba 的 Windows 文件和打印服务器共享）。`time-servers` 选项设置了网络上时间服务器的位置。

- DHCP 服务器可用于提供 X 终端或无盘工作站启动网络所需的信息。以下是一个你可以用于在网络上启动此类计算机的定义示例：

```
host maple
filename = "/dwboot/maple.nb"
hardware ethernet 00:04:5A:4F:8E:47;
fixed-address 10.0.0.150;
```

在上例的示例中，无盘工作站从 DHCP 服务器使用的值位于 `/dwboot/maple.nb`。`hardware ethernet` 值识别客户端上的以太卡。客户端的 IP 地址被设置为 10.0.0.150。所有这些行都包含在 `host` 定义中，其中 `host` 被定义为 `maple`。（数据类型的描述请参见表 23-1，其他可能用于配置客户端的选项请参见表 23-2 中的 Thin Clients（瘦客户端）标题。）

## 添加选项

在 `/etc/dhcpd.conf` 文件中有几十种选项可以将信息从 DHCP 服务器传递给 DHCP 客户端。表 23-1 描述了你可以为不同选项使用的数据类型。表 23-2 描述了可用的选项。

## 表 23-1：数据类型

| 数据类型 | 描述 |
|---|---|
| ip-address | 输入 ip-address，可以是 IP 地址数字（10.111.111.111）或完全限定域名（compl.handsonhistory.com）。要使用域名，该名称必须解析为 IP 地址。 |
| int32, int16, int8, uint32, uint16, uint8 | 用于表示有符号和无符号的 32 位、16 位和 8 位整数。 |
| "string" | 输入由双引号包的字符字符串。 |
| Boolean | 在需要布尔值时输入 true 或 false。 |
| string | 输入不带引号的字符字符串。 |

# 第 23 节：设置 DHCP 服务器

在 `/etc/dhcpd.conf` 文件中有几十种选项可以将信息从 DHCP 服务器传递给 DHCP 客户端。表 23-1 描述了你可以为不同选项使用的数据类型。表 23-2 描述了可用的选项。

- 如果你在同一子网上有多个地址范围，你可以在子网声明中添加多个 `range` 选项。这是一个示例：

```
subnet 10.0.0.0 netmask 255.255.255.0 {
  range 10.0.0.10 10.0.0.100;
  range 10.0.0.200 10.0.0.250;
}
```

此示例导致 DHCP 服务器在网络 10.0 上分配范围 10 之间以及 200 到 250 之间的 IP 地址。

- 你可以为特定的主机计算机设置固定地址，也称为地址预留。特别是，你可能希望对服务器计算机这样做，以确保它们的地址不会发生变化。虽然你可以简单地从 DHCP 分配的地址池中省略固定 IP 地址，但你将失去 IP 配置的集中化管理。DHCP 允许你完全配置所有的 IP 地址信息。实现此点的方法之一基于服务器网卡的以太网硬件地址。所有相关信息都可以包含在主机定义中，如下所示：

```
host pipe {
  hardware ethernet 00:04:5A:4F:8E:47;
  fixed-address 10.0.0.254;
}
```
