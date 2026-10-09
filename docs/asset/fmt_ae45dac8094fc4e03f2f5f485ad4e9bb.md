
## 配置 DHCP IPv4 服务器

你可以使用 `/etc/rc.d/init.d` 目录下的 `dhcpd` 脚本启动和停止 DHCP 服务器。使用 `services-admin` 工具或带有 `start`、`restart` 和 `stop` 选项的 `dhcpd` 脚本。以下示例启动 DHCP 服务器。使用 `stop` 选项将其关闭，使用 `restart` 重新启动。

`service dhcpd start.`

动态分配的 IP 地址（称为租约，leases）会被分配一段时间。当租约过期时，可以扩展它或生成一个新的。当前租约列在 `/var/lib/dhcp` 目录下的 `dhcpd.leases` 文件中。租约条将指定 IP 地址、租约的开始和结束时间以及客户端主机名。

## GNOME DHCPD 配置，GDHCPD

你也可以使用 GNOME DHCPD 配置工具 (GDHCPD) 软件包来图形化配置 DHCP 服务器。尽管仍处于早期开发阶段，但 GDHCPD 提供了一种易于设置服务器的方法。该包将安装在“Administration | System Tools”菜单下。

在“Scopes”选项卡上，你输入网络连接、该连接的 IP 地址和子网掩码。然后点击 Add。在“Range”框中，输入要分配的地址范围，然后点击 Add。

“single hosts”选项卡允许你为特定主机指定静态 IP 地址。这些通常用于 IP 地址通常不会改变的系统。

点击“Settings”按钮查看你的服务器配置设置，例如使用的配置和租约文件，以及是否允许 DNS 更新。

## `/etc/dhcpd.conf`

DHCP 服务器的配置文件为 `/etc/dhcpd.conf`，在其中你指定了定义 DHCP 服务器如何访问网络上 DHCP 客户端的参数和声明，以及定义 DHCP 服务器传递给客户端的信息的选项（options）。这些参数、声明和选项可以针对某些子网或特定主机进行全局定义。全局参数、声明和选项适用于所有客户端，除非被子网或主机声明中相应的声明和选项覆盖。从技术上讲，`dhcpd.conf` 文件中的所有项都是可以是声明或参数的语句。语句以分号结束。选项在选项参数语句中指定。参数与声明的区别在于，它们定义了是否以及如何执行任务，例如如何分配租约。声明描述网络特性，例如要分配的地址范围或可访问的网络。参见表 31-1 的常用声明和选项列表。

声明为 DHCP 服务器提供信息或指定其要执行的操作。例如，`range` 声明用于指定动态分配给主机的 IP 地址范围：

```
192.168.0.5 192.168.0.128;
```

通过参数，你可以指定服务器如何处理客户端。例如，`default-lease-time` 声明指定了分配租约的秒数。

## 第 31 章：自动配置与 DHCP

选项为客户端提供信息，例如网关、子网掩码和代理地址。参见表 31-1 的常用声明和选项列表。

## DHCP 动态 IPv4 地址

你的 DHCP 服务器可以配置为从给定范围选择 IP 地址并将其分配给不同的客户端。对于许多可能始终连接到网络的客户端情况，你可以用较小的 IP 地址池为它们提供服务。IP 地址仅在需要时才分配。通过 `range` 声明，你指定了一个可以动态分配的地址范围。该声明接受两个参数，范围内的第一个和最后一个地址

```
range 192.168.1.5 192.168.1.128;
```

例如，如果你正在建立自己的小型家庭网络，将使用以 192.168 开头的网络地址。范围将指定你网络可能的 IP 地址。因此，对于 192.168.0.0 网络，你只需放置一个范围声明以及任何其他你想提供给客户端主机的信息。在以下示例中，从 192.168.0.1 到 192.168.0.128 的地址范围可以分配给该网络上的主机：

```
range 192.168.0.5 192.168.0.128;
```

## 第6 部分：网络支持

| 条目 | 描述 |
| --- | --- |
| 声明 (Declarations) | |
| shared-network name | 表示某些子网是否共享相同的物理网络。 |
| subnet subnet-number netmask | 引用整个地址子网。 |
| range [ dynamic-bootp ] low-address { high-address }; | 提供最高和最低动态分配的 IP 地址。 |
| host hostname | 引用特定的主机。 |
| group | 允许你对一组参数和声明进行标记，然后使用该标签将它们应用于子网和主机。 |
| allow unknown-clients; deny unknown-clients; | 不向未知客户端动态分配地址。 |
| allow bootp; deny bootp; | 决定是否响应 bootp 查询。 |
| allow booting; deny booting; | 决定是否响应客户端查询。 |
| 参数 (Parameters) | |
| default-lease-time time; | 为租约分配长度（单位：秒）。 |
| max-lease-time time; | 分配最大租约长度。 |
| hardware hardware-type hardware-address; | 指定网络硬件类型（以太网或令牌环）和地址。 |
| filename "filename"; | 指定初始启动文件的名称。 |
| server-name "name"; | 指定客户端从中从中启动的服务器名称。 |
| next-server server-name; | 指定加载 `filename` 中指定启动文件的服务器。 |
| fixed-address address [, address ... ]; | 为客户端分配固定地址。 |
| get-lease-hostnames flag; | 决定是否查找并使用客户端的 IP 地址。 |
| authoritative; not authoritative; | 拒绝无效的地址请求。 |
| server-identifier hostname; | 指定服务器。 |
| 选项 (Options) | |
| option subnet-mask ip-address; | 指定客户端的子网掩码。 |
| option routers ip-address [, ip-address ... ]; | 指定路由器 IP 地址列表。 |

## 第31 章：自动配置与 DHCP

| | |
|--- |--- |
| option domain-name-servers ip-address [ , ip-address... ]; | 在客户端子网上。 |
| option log-servers ip-address [ , ip-address... ]; | 指定客户端使用的域名服务器列表。 |
| option host-name string; | 指定客户端的主机名。 |
| option domain-name string; | 指定客户端的域名。 |
| option broadcast-address ip-address; | 指定客户端的广播地址。 |
| option nis-domain string; | 指定客户端的网络信息服务（NIS）域。 |
| option nis-servers ip-address [ , ip-address... ]; | 指定客户端可以使用的 NIS 服务器。 |
| option smtp-server ip-address [ , ip-address... ]; | 客户端使用的 SMTP 服务器列表。 |
| option pop-server ip-address [ , ip-address... ]; | 客户端使用的 POP 服务器列表。 |
| option nntp-server ip-address [ , ip-address... ]; | 客户端使用的 NNTP 服务器列表。 |
| option www-server ip-address [ , ip-address... ]; | 客户端使用的 Web 服务器列表。 |

表 31-1：DHCP 声明、参数和选项

你应该定义租约时间，包括默认时间和最大值：
`default-lease-time 21600;`
`max-lease-time 43200;`

对于小型家庭网络，你只需要列出 `range` 声明以及此处显示的任何全局选项。如果你的 DHCP 服务器管理着多个子网络，则你将必须使用 `subnet` 声明。

为了给网络分配动态地址，DHCP 服务器要求你的网络拓扑知道哪些网络地址属于给定的网络。即使只使用一个网络，也需要为其指定地址空间。你通过 `subnet` 声明来定义网络。在 `subnet` 声明内部，你可以指定用于该子网的任何参数、声明或选项。`subnet` 声明告知 DHCP 服务器子网包含的可能 IP 地址。这是由网络 IP 地址和该网络的掩码决定的。下一个示例定义了一个地址空间为 192.168.0.0 到 192.168.0.255 的本地网络。`range` 声明允许从 192.168.0.5 到 192.168.0.128 分配地址。

```
subnet 192.168.0.0 mask 255.255.255.0 {
  range 192.168.0.5 192.168.0.128;
}
```

3.0 之前的 DHCP 版本要求你甚至要映射未由 DHCP 服务的连接网络接口。因此，每个网络接口都必须有一个相应的 `subnet` 声明。未由 DHCP 服务的接口没有如下所示的 `not authoritative` 参数（此处 '192.168.2.0' 是一个不由 DHCP 服务的网络）。在 3.0 及更高版本中，DHCP 简单地忽略未映射的网络接口：

```
subnet 192.168.2.0 netmask 255.255.255.0 (
  not authoritative;
)
```

以下显示了一个用于动态地址的简单 DHCP 服务器的实现：

```
subnet 192.168.0.0 netmask 255.255.255.0 (
  option subnet-mask 255.255.255.0;
  option routers 192.168.0.1;
  range 192.168.0.5 192.168.0.128;
  not authoritative;
)
```

## 第 6 部分：网络支持

对于需要更新的 DNS 服务器，建议在区域条目中使用主语句显式地标识它们。

为了生成用于 DNS 更新的完全限定主机名（FQDN），DHCP 服务器通常会使用它自己的域名和 DHCP 客户端提供的主机名（示例参见 `dhcp.conf` 页面）。你应该为主机分配一个特定的主机名；可以在主机的硬件部分使用 `ddns-hostname` 语句来指定它。域名在 `domain-name` 选项中指定：

```
option domain-name "mytrek.com";
```

可以通过 `ddns-update-style` 语句开启或关闭所有域的 DNS 更新功能。默认是开启的。若要关闭特定域的更新，可以使用 `ddns-updates` 语句。这同样是默认设置。

## DHCP 子子网

如果你将网络空间划分为几个子网，可以使用单个 DHCP 服务器来管理它们。在这种情况下，你需要为每个子网准备一个子网声明（subnet declaration）。如果你正在建立自己的小型网络，你使用以 192.168 开头的网络地址。范围指定了该子网内可能的 IP 地址；对于地址为 192.168.0 的网络，你创建一个掩码为 255.255.255.0 的子网声明。在此声明内部，你放置一个范围声明（range declaration）以及任何你想提供给客户端主机的其他信息。在接下来的示例中，从 192.168.0.1 到 192.168.0.75 的 IP 地址范围可以分配给该网络上的主机：

```
subnet 192.168.0.0 mask 255.255.255.0 {
  range 192.168.0.5 192.168.0.75;
}
```

你可能想为每个子网指定不同的策略，例如不同的租约时间。子网声明中的任何条目都会覆盖全局设置。如果你已经设置了全局租约时间，子网声明中的租约将覆盖该子网的全局设置。接下来的示例为不同的子网设置了不同的租约时间以及不同的地址。第一个子网的租约时间取自全局租约时间设置，而子网则定义了自己的租约时间：

```
default-lease-time 21600;
max-lease-time 43200;
subnet 192.168.1.0 mask 255.255.255.0 {
  range 192.168.0.5 192.168.0.75;
}
subnet 192.168.1.128 mask 255.255.255.252 {
  range 192.168.0.129 192.168.0.215;
  default-lease-time 56000;
  max-lease-time 62000;
}
```

## 第 31 章：自动配置与 DHCP

如果你的子网属于同一个物理网络，你需要通过将它们声明为共享网络（shared networks）来告知服务器此事实。做法是将子网声明放在 `shared-network` 声明内部，并指定共享网络的名称。该名称可以是任何描述性名称，尽管也可以使用域名。在 `shared-network` 声明内部且子网声明之外指定的任何选项对于这些子网来说都是全局的。在接下来的示例中，子网属于同一个物理网络，因此被放置在 `shared-network` 声明中：

```
shared-network mytrek.com
{
  default-lease-time 21600;
  max-lease-time 43200;
  subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.0.5 192.168.0.75;
  }
  subnet 192.168.1.128 netmask 255.255.255.252 {
    range 192.168.0.129 192.168.0.215;
    default-lease-time 56000;
    max-lease-time 62000;
  }
}
```

## DHCP 固定地址

与其为主机使用一个可能的 IP 地址池，你可能可能想为每个主机提供一个特定的地址。使用 DHCP 服务器仍然可以让你控制哪个地址将分配给特定的主机。然而，要为特定主机分配地址，你需要知道该主机网络网卡（NIC）的硬件地址。特别是具有指定 IP 地址的特定网络连接设备。为了做到这一点，DHCP 服务器需要知道你指的是哪个设备。你可以通过其硬件地址（即 MAC 地址）来识别网络设备。要查找客户端的硬件地址，请登录客户端并使用 `ifconfig` 命令查找有关网络设备的信息。要列出所有网络设备，请使用 `-a` 选项。如果你知道网络设备的名称，可以使用它。接下来的示例将列出关于第一个以太网设备 eth0 的所有信息：

```
ifconfig eth0
```

这将列出所有客户端的信息。要列出所有网络设备，请使用 `-a` 选项。如果你知道你的网络设备名称，可以使用它。接下来的示例将列出关于第一个以太网设备 eth0 的所有信息：

`ifconfig eth0`

使用 DHCP 服务器仍然可以让你控制哪个地址将分配给特定主机。然而，要为特定主机分配地址，你需要知道该主机网络网卡（NIC）的硬件地址。特别是具有指定 IP 地址的特定网络连接设备。为了做到这一点，DHCP 服务器需要知道你指的是哪个设备。你可以通过其硬件地址（即 MAC 地址）来识别网络设备。要查找客户端的硬件地址，请登录客户端并使用 `ifconfig` 命令查找有关网络设备的信息。在 `dhcp.conf` 文件中，为每个子网准备一个子网声明。在此声明内部，你放置一个范围声明以及任何你想提供给客户端主机的其他信息。在接下来的示例中，从 192.168.0.1 到 192.168.0.75 的 IP 地址范围可以分配给该网络上的主机：

```
subnet 192.168.0.0 mask 255.255.255.0 {
  range 192.168.0.5 192.168.0.75;
}
```
