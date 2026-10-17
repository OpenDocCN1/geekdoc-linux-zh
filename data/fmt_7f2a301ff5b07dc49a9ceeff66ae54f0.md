
## 第6 部分：网络支持

| 条目 | 描述 |
| --- | --- |
| 声明 (Declarations) | |
| `shared-network name` | 表示某些子网是否共享相同的物理网络。 |
| `subnet subnet-number netmask` | 引用整个地址子网。 |
| `range [ dynamic-bootp ] low-address { high-address };` | 提供最高和最低动态分配的 IP 地址。 |
| `host hostname` | 引用特定的主机。 |
| `group` | 允许你对一组参数和声明进行标记，然后使用该标签将它们应用于子网和主机。 |
| `allow unknown-clients; deny unknown-clients;` | 不向未知客户端动态分配地址。 |
| `allow bootp; deny bootp;` | 决定是否响应 bootp 查询。 |
| `allow booting; deny booting;` | 决定是否响应客户端查询。 |
| 参数 (Parameters) | |
| `default-lease-time time;` | 为租约分配长度（单位：秒）。 |
| `max-lease-time time;` | 分配最大租约长度。 |
| `hardware hardware-type hardware-address;` | 指定网络硬件类型（以太网或令牌环）和地址。 |
| `filename "filename";` | 指定初始启动文件的名称。 |
| `server-name "name";` | 指定客户端从中从中启动的服务器名称。 |
| `next-server server-name;` | 指定加载 `filename` 中指定启动文件的服务器。 |
| `fixed-address address [, address ... ];` | 为客户端分配固定地址。 |
| `get-lease-hostnames flag;` | 决定是否查找并使用客户端的 IP 地址。 |
| `authoritative; not authoritative;` | 拒绝无效的地址请求。 |
| `server-identifier hostname;` | 指定服务器。 |
| 选项 (Options) | |
| `option subnet-mask ip-address;` | 指定客户端的子网掩码。 |
| `option routers ip-address [, ip-address ... ];` | 指定路由器 IP 地址列表。 |

## 第31 章：自动配置与 DHCP

| | |
|--- |--- |
| `option domain-name-servers ip-address [ , ip-address... ];` | 在客户端子网上。 |
| `option log-servers ip-address [ , ip-address... ];` | 指定客户端使用的域名服务器列表。 |
| `option host-name string;` | 指定客户端的主机名。 |
| `option domain-name string;` | 指定客户端的域名。 |
| `option broadcast-address ip-address;` | 指定客户端的广播地址。 |
| `option nis-domain string;` | 指定客户端的网络信息服务（NIS）域。 |
| `option nis-servers ip-address [ , ip-address... ];` | 指定客户端可以使用的 NIS 服务器。 |
| `option smtp-server ip-address [ , ip-address... ];` | 客户端使用的 SMTP 服务器列表。 |
| `option pop-server ip-address [ , ip-address... ];` | 客户端使用的 POP 服务器列表。 |
| `option nntp-server ip-address [ , ip-address... ];` | 客户端使用的 NNTP 服务器列表。 |
| `option www-server ip-address [ , ip-address... ];` | 客户端使用的 Web 服务器列表。 |

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

### DHCP 子子网

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
```
