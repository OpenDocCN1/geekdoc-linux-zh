
```
subnet 192.168.100.0 netmask 255.255.255.0 {
    range 192.168.100.25 192.168.100.50;
    option domain-name-servers 1.1.1.1;
    option domain-name "mycompany.com";
    option subnet-mask 255.255.255.0;
    option routers 192.168.100.1;
    option broadcast-address 192.168.100.254;
    default-lease-time 600;
    max-lease-time 7200;
}
```

可以为某个客户端指定特定参数。为此，使用关键字 `host`，后跟标签和所需选项，如下面的摘录所示：

```
host rhelysystem {
    hardware ethernet 52:54:00:57:d0:9f;
    fixed-address 192.168.100.222;
}
```

配置文件设置完成后，在基于 Ubuntu/Debian 的系统上需要启动（或重启）的服务是 `isc-dhcp-server`，而在基于 RHEL 的系统上是 `dhcpd`。使用 `journalctl` 命令查看系统日志，可以获取有关请求和已分配 IP 地址的信息，如下面的摘录所示：

```
dhcpd[1151]: Server starting service.

dhcpd[1151]: DHCPDISCOVER from 52:54:00:57:d0:9f via enp8s0

dhcpd[1151]: DHCPOFFER on 192.168.100.222 to 52:54:00:57:d0:9f via enp8s0

dhcpd[1151]: DHCPREQUEST for 192.168.100.222 (192.168.100.1) from 52:54:00:57:d0:9f via enp8s0

dhcpd[1151]: DHCPACK on 192.168.100.222 to 52:54:00:57:d0:9f via enp8s0
```

作为测试 `DHCP 请求` 的客户端，`dhclient` 工具提供了一种可能性，即用动态 IP 配置一个接口，而不是使用系统配置（使用文件、`NetworkManager` 或 `netplan`）。此工具允许指定选项 `-v` 以启用详细日志记录。选项 `-r` 用于释放当前租约并停止该接口的客户端运行。图 9.6 展示了使用示例，并显示了输出：

```
[root@rhel ~]# dhclient -v enp7s0
Internet Systems Consortium DHCP Client 4.4.2bi
Copyright 2004-2019 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/

Listening on LPF/enp7s0/52:54:00:57:d0:9f
Sending on LPF/enp7s0/52:54:00:57:d0:9f
Sending on Socket/fallback
DHCPDISCOVER on enp7s0 to 255.255.255.255 port 67 interval 5 (xid=0x464c887f)
DHCPOFFER of 192.168.100.222 from 192.168.100.1
DHCPREQUEST for 192.168.100.222 on enp7s0 to 255.255.255.255 port 67 (xid=0x464c887f)
DHCPACK of 192.168.100.222 from 192.168.100.1 (xid=0x464c887f)
bound to 192.168.100.222 -- renewal in 284 seconds.
```

### 图 9.6：命令 dhclient 的输出示例

DHCP 服务器在文件中保存租约的路径，对于 IPv4 是 `/var/lib/dhcp/dhcpd.leases`，对于 IPv6 是 `/var/lib/dhcp/dhcpd6.leases`。对于软件 `dnsmasq`，需要安装同名的软件包。主要配置是 `/etc/dnsmasq.conf`，它不仅用于 DHCP 配置，还用于 DNS 和 TFTP。该文件也可以包含 IPv6 配置。提供 DHCP 服务的配置示例如下面的摘录所示：

```
listen-address=192.168.100.1
domain=mycompany.com
dhcp-range=192.168.100.25,192.168.100.50,2h
dhcp-host=52:54:00:57:d0:9f,192.168.100.222
dhcp-option=option:router,192.168.100.1
dhcp-option=option:dns-server,1.1.1.1
```

服务启动后，当接收到请求时，日志将出现在 `journalctl` 中。以下摘录显示了为配置了特定 IP 的主机分配 IP 的情况：

```
ubuntu dnsmasq-dhcp[1889]: DHCPDISCOVER(enp8s0) 192.168.100.222 52:54:00:57:d0:9f
ubuntu dnsmasq-dhcp[1889]: DHCPOFFER(enp8s0) 192.168.100.222 52:54:00:57:d0:9f
ubuntu dnsmasq-dhcp[1889]: DHCPREQUEST(enp8s0) 192.168.100.222 52:54:00:57:d0:9f
ubuntu dnsmasq-dhcp[1889]: DHCPACK(enp8s0) 192.168.100.222 52:54:00:57:d0:9f
```

`dnsmasq` 的租约文件是 `/var/lib/misc/dnsmasq.leases`。

### DNS 服务和客户端

域名系统（DNS）是一项将域名转换为 IP 地址并反向转换的服务。其结构基于层次结构，顶层包含根名称服务器。目前，这些根名称服务器是位于世界不同地区的 13 台服务器。这些服务器的语法为 `letter.root-servers.org`，其中的字母目前从 `a` 到 `m`。向根名称服务器的第一个查询是为了获取顶级域（TLD）的服务器，这些服务器负责层次结构中的第二级。这些服务器与顶级域相关联，例如 `.com`、`.net` 和 `.org`，国家代码 TLD（例如 `.in`、`.es` 和 `.jp`），以及新的 TLD（例如 `.tech` 和 `.space`）。这些顶级域服务器将提供指定域名的域服务器。这些域名负责提供所查询域名或子域名的答案。DNS 可以包含指示子域其他名称服务器的复杂配置。图 9.7 展示了包含两个域名示例的层次结构：

![](img/863afa537de4eed7deb11978bfbfa90e_283_0.png)

图 9.7：DNS 层次结构示例

查询使用 UDP 协议，目标端口为 `53`。DNS 服务可以运行在不同的模式下：

- `权威（Authoritative）`：负责一个或多个域名，并仅回答与此相关的查询。
- `转发（Forwarding）`：DNS 服务不负责任何域名，所有请求都转发给 `上游` DNS 服务器。
- `缓存（Cache）`：类似于 `转发`，但为客户端请求保留缓存。这是一种流行配置，旨在避免对上游服务器进行多次请求。

可以组合不同的模式，例如在同一个服务器上组合 `权威` 模式和 `缓存` 模式。该 DNS 服务将回答其负责域名的查询。对于其余域名，它将请求转发到配置的 `上游` DNS 服务器，并缓存客户端请求。

新技术和现代软件依赖于 DNS 才能正确运行。软件需要在服务之间通信以及从仓库拉取所需的软件制品（如容器镜像）时，具备正确的内部和外部解析能力。

在 DNS 服务器中配置的 DNS 记录有不同的类型，如表 9.1 所示：

### Linux DNS 服务器和客户端

| 记录类型 | 描述 |
|---|---|
| `A` | 将主机名解析为 IP |
| `AAAA` | 将主机名解析为 IP，适用于 IPv6。 |
| `CNAME` | 指定主机名的别名 |
| `PTR` | 将 IP 解析为主机名 |
| `NS` | 指定域名或子域名的名称服务器。 |
| `MX` | 指定域名或子域名的邮件服务器。 |
| `SRV` | 指定特定服务的主机和端口。 |
| `TXT` | 指定主机名的文本记录。用于检查域名所有者以及不同的域名配置。 |
| `SOA` | 代表“权威起点”（start of authority），并提供域名的管理员信息以及上次更新和刷新时间的信息。 |

*表 9.1：DNS 记录类型*
