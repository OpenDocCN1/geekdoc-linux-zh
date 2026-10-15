
```bash
# chconfig dhcpd --list
dhcpd 0:off 1:off 2:on 3:on 4:on 5:on
6:off
```

## 配置 DHCP 服务器

为了开始配置，让我们来看处理 DHCP 服务选项的重要文件：

- `/etc/dhcp/dhcp.conf` 使用 IPv4 地址的 DHCP 服务主配置文件
- `/etc/dhcp/dhcpd6.conf` 使用 IPv6 地址的 DHCP 服务主配置文件
- `/var/lib/dhcp/dhcpd.leases` IPv4 客户端租文件
- `/var/lib/dhcp/dhcpd6.leases` IPv6 客户端租文件

> 迁移提示
>
> 在 RHEL5 中，主配置文件的位置是 `/etc/dhcpd.conf`。现在在 RHEL6 中，由于增加了 IPv6 地址的额外配置文件，配置文件已移动到目录 `(/etc/dhcp)`。

主配置文件通常除了一两个注释外是空的。好消息是，该软件包提供了一个示例配置文件供你使用。该示例文件提供了示例和注释，说明了如何为你的 DHCP 服务器配置选项。

要拷贝示例文件，请使用以下命令：

```bash
# /usr/share/doc/dhcp-4.1.1/dhcpd.conf.sample /etc/dhcp/dhcpd.conf
```

如果你是刚接触 DHCP 服务器，这个示例文件中包含的注释将对你有帮助，这些注释解释了不同的选项。下面的示例配置文件提供了入门所需的基础知识。它比示例文件更整洁，更容易解释。

这里是示例 DHCP 服务器文件：

```conf
# 全局选项
ddns-update-style none;
authoritative;
```

```conf
# 子网定义
```

`subnet 172.168.1.0 netmask 255.255.255.0 {`

```conf
# 本地子网的参数
option routers 172.168.1.1;
option subnet-name 255.255.255.0;

option domain-name "example.com";
option domain-name-servers 172.168.1.1;

default-lease-time 21600;
max-lease-time 43200;
```

```conf
# 客户端 IP 范围
range dynamic-boot 172.168.1.100 172.168.1.200;
```

`}`

让我们将此文件分成几个部分。第一部分包含 DHCP 服务器本身的两个选项，也称为全局选项：

- `ddns-update-style`: 这意味着 DHCP 服务器不会更新客户端记录。
- `authoritative`: 这通知客户端 DHCP 服务器包含合法的信息。

### 实战技巧

> 如果服务器不包含 `authoritative` 选项且客户端切换了子网，那么在旧的租约完全过期之前，它无法获得新的 IP 地址。向配置不正确的客户端发送 `DHCPNAK` 也有安全方面的益处。

下一部分定义了一个子网。你在子网中列出的任何选项都仅适用于你定义的该子网。如果你想设置全局选项（如 `authoritative`），需要在子网部分之外定义它们。在此部分中，使用了以下选项：

- `option routers`: 定义指向子网的默认网关
- `option subnet-mask`: 定义子网的掩码
- `option domain-name`: 定义域名
- `option domain-name-servers`: 定义子网的 DNS 服务器
- `default-lease-time`: 指定客户端在请求续约之前保留租约的时间（秒）
- `max-lease-time`: 指定客户端保留租约的最长时间（秒）
- `range dynamic-boot`: 指定可以分配给客户端的 IP 地址范围

有了配置文件，你就拥有了 DHCP 服务器正常运行所需的所有内容。虽然本部分没有描述 DHCP 服务可用的所有选项，但这是启动 DHCP 服务器的良好开始。对于考试，如果你忘记了选项的名称，可以随时查阅文档。虽然我不喜欢让你参考很多页面，但要记住每个服务的一切是不可能的。在需要时找到信息对于考试和现实世界至关重要。以下是你应该了解的三个页面：

```
# dhcpd.conf
# dhcpd.leases
# dhcp-options
```

如果你想拥有多个子网，只需定义一个带有自身选项集的新子网部分。部分的数量没有限制。

# 432 Red Hat® 考试实战指南：RHCSA® 和 RHCE® 指南与实验手册

第 1 步查询你需要更改的布尔值：

```bash
setboolean -a grep dhcpd_dis
dhcpd_disable_trans --> off
```

第 2 步禁用 SELinux ：

```bash
setboolean -P dhcpd_disable_trans=1
```

第 3 步验证布尔值已更改：

```bash
setboolean -a grep dhcpd
dhcpd_disable_trans --> on
```

现在你应该拥有了一个功能完整的 DHCP 服务器！你可以启动客户端并查看它们是否获取了 IP 地址，或者如果客户端已经开启，可以使用 `dhcpclient` 命令从服务器请求 IP 地址。

第 4 步从服务器请求动态 IP：

```bash
dhcpclient
```

Internet Systems Consortium DHCP Client V3.0.5-RedHat

Copyright 2004-2006 Internet Systems Consortium.

保留所有权利。

欲了解信息，请访问 http://www.isc.org/sw/dhcp/

Listening on LPF/eth0#08:00:27:74:5b11

Sending on LPF/eth0#08:00:27:74:5b11

Sending on Socket/fallback

DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 7

DHPOFFER from eth0 192.168.1.1

DHCPREQUEST on eth0 to 255.255.255.255 port 67

DHCPACK from eth0 192.168.1.1 bound to 192.168.1:7 renewal in 40126 seconds.

## DHCP 故障排除

并非所有的配置都能如你所想的那样顺利。当你排查 DHCP 服务器时，有几点需要注意。例如，在主配置文件 `/etc/dhcpd.conf` 中，确保所有选项（`options`）都以分号（`;`）结尾。如果你没有这样做，服务在检查配置文件时会抛出错误。此外，确保在防火墙规则生效后测试 DHCP 服务器。对于客户端故障排除，DHCP 服务器提供了一个客户端租约文件。该文件包含了每个从服务器获取 IP 地址的客户端的所有租约信息。当你有一个拥有 DHCP 地址的客户端时，可以使用以下命令查看租约文件：

```bash
# cat /var/lib/dhcpd/dhcpd.leases
```

`lease 172.168.1.200 {`
`starts 2 2010/05/11 12:24:10;`
`ends 2 2010/05/11 18:24:10;`
`tstp 2 2010/05/11 18:24:10;`
`binding state free;`
`hardware ethernet 08:00:27:74:5b:11;`
`}`

`lease 172.168.1.199 {`
`starts 4 2010/05/20 11:24:03;`
`ends 4 2010/05/20 17:24:03;`
`tstp 4 2010/05/20 17:24:03;`
`binding state free;`
`hardware ethernet 08:00:27:2f:00:8c;`
`}`

从文件输出可以看出，有两个客户端的活动租约。在查看租约时，你应该注意 `dhcpd.leases` 文件中的所有时间都是 UTC (GMT)。之所以这样做是因为该时区没有夏令，因此可以在国际范围内使用。如果你正在尝试排查此文件，请务必注意这个问题。最后一个提示是，在重启服务之前，确保使用配置选项来测试配置文件的语法。这可以防止在尝试启动服务时出现任何错误。

### 实战技巧

你可能考虑设置一个备用 DHCP 服务器作为故障转移。如果主服务器故障，它可以为你提供备份（不要只依赖这个备用服务器；确保你测试过它）。如果你创建了备备服务器，应该遵循 80/20 原则：80% 的 IP 地址应该在主服务器上使用，20% 应该在备用服务器上使用。

# 网络时间协议
