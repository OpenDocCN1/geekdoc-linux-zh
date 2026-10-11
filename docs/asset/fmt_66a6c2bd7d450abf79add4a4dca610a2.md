
``` 
subnet 192.168.1.0 netmask 255.255.255.0 {

  # Options

  option routers 192.168.1.1;

  option subnet-mask 255.255.255.0;

  option domain-name "example.org";

  option domain-name-servers ns.example.org;

  # Parameters

  default-lease-time 21600;

  max-lease-time 43200;

  # Declarations

  range 192.168.1.25 192.168.1.49;

  # Nested declarations

  host client {

    hardware 00:80:c6:f7:62:00;

    fixed-address 192.168.1.50;

  }

}
```

## DHCP

在此示例中，请注意以下点：

- 定义了一个子网。DHCP 客户端指示使用 `192.168.1.1` 作为默认路由器（网关地址），并使用 `255.255.255.0` 作为子网掩码。
- DNS 信息被传递给客户端；它们将使用 `example.org` 作为域名，使用 `ns.example.org` 作为其 DNS 服务器。
- 设置了 `21600` 秒的租期；如果客户端请求更长的租期，可能会被授予长达 `43200` 秒。
- IP 地址范围从 `192.168.1.25` 开始，最高可以到 `192.168.1.49`。MAC 地址为 `00:80:c6:f7:62:00` 的机器将始终获得 IP 地址 `192.168.1.50`。

> 注意 至关重要的是，你必须确保你的 DHCP 服务器至少有一个网络接口配置了 IP 地址，该地址必须属于 `dhcp.conf` 子网声明中定义的同一网络。这意味着，例如，你不应该有一个读取为 `subnet 192.168.1.0 netmask 255.255.255.0` 的子网声明，而你的 DHCP 服务器却有一个 IP 地址为 `172.16.0.10` 的网络接口（如 `eth0`）。你还应该确保 DHCP 的 IP 地址排除在 `range` 声明中指定的发布/租用 IP 地址范围之外。你示例中的 DHCP 服务器应该有一个位于 `192.168.1.1` 到 `192.168.1.24` 范围内的静态 IP 地址。如果你忽略了这一点，DHCP 服务将无法启动并出现类似的错误：

```
No subnet declaration for eth0.
```

## 普通运行行为

一旦启动，守护进程会耐心等待客户端请求到达，然后再进行任何处理。当处理请求并分配地址时，它会将该地址记录在名为 `dhcpd.leases` 的文件中。在 Fedora、RHEL 和 CentOS 系统上，此文件存储在 `/var/lib/dhcpd/` 目录下。在基于 Debian 的发行版（如 Ubuntu）中，客户端租约存储在 `/var/lib/dhcpd/` 目录下。

## DHCP 客户端守护进程

ISC DHCP 客户端守护进程（名为 `dhclient`）包含许多流行的 Linux 发行版中，是用于与前节描述的 DHCP 服务器通信的软件组件。它将尝试从可用的 DHCP 服务器获取地址并相应地配置网络。

## 配置 DHCP 客户端

客户端通常从启动文件运行，也可以手动运行。它通常在其他网络服务启动之前启动，因为除非系统本身接入网络，否则其他网络服务是无法使用的。

另一方面，客户端可以在启动后的任何时候从命令行手动调用。启动客户端守护进程可以不带额外选项，但它将尝试在系统上配置的所有接口上获取租约。

以下是以最基本形式从命令行启动客户端的方法：

```bash
[root@clientB ~]# dhclient
....OUTPUT TRUNCATED...
Sending on LPF/eth0/00:0c:29:f8:b8:88
Sending on Socket/fallback
DHCPDISCOVER on lo to 255.255.255.255 port 67 interval 7
DHCPREQUEST on eth0 to 255.255.255.255 port 67
DHACK from 192.168.1.1
SIOCADRT: File exists
bound to 192.168.1.1
```
