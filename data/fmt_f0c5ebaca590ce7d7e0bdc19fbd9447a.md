
dnswalk 实用程序依赖于 `perl-Net-DNS` 工具，因此必须先安装后者。使用 Red Hat 发行版时，最简单的安装方式是通过 `rpm`。首先，从网络获取这两个文件：

- `ftp://rufus.w3.org/linux/contrib/libc5/1386/perl-Net-DNS-0.12-1.1386.rpm`

- `ftp://rufus.w3.org/linux/contrib/noarch/noarch/dnsvalk-2.0.2-1.noarch.rpm`

现在使用以下两个命令安装它们：

```
# rpm -ivh perl-Net-DNS-0.12-1.1386.rpm
# rpm -ivh dnsvalk-2.0.2-1.noarch.rpm
```

### 提示

如果您更喜欢从源代码编译、构建和安装，可以在 `http://www.visi.com/~barr/dnswalk/` 获取源代码。

必须按照上述顺序安装，因为 `dnswalk` 依赖于 `perl-Net-DNS`。`dnswalk` 可执行文件（实际上是一个 Perl 程序）安装在 `/usr/sbin` 目录中。`dnswalk` 通过指定域名作为唯一参数来使用。域名必须以点 `.` 结尾。以下是一个示例：

```
# dnswalk domain.cxm.
Checking domain.cxm.
BAD: domain.cxm. has only one authoritative nameserver
Getting zone transfer of domain.cxm. from mainserv.domain.cxm... done.
SOA=mainserv.domain.cxm contact:hostmaster.domain.cxm
0 failures, 0 warnings, 1 errors.
#
```

您会注意到它发现的唯一错误是缺乏二级 DNS 服务器。本章的大多数示例只定义了一个 DNS 服务器。在以下示例中，`named.domain.cxm` 已更改，使得 `mydesk.domain.cxm` 解析为 `192.168.100.22`，但 `named.192.168.100` 中的反向查找仍为 `192.168.100.2`。这是一种正向/反向不匹配——一个严重的问题，使用 `nslookup` 等工具将很难诊断：

```
# dnswalk domain.cxm.
Checking domain.cxm.
BAD: domain.cxm. has only one authoritative nameserver
Getting zone transfer of domain.cxm. from mainserv.domain.cxm... done.
SOA=mainserv.domain.cxm contact:hostmaster.domain.cxm
WARN: mydesk.domain.cxm A 192.168.100.22: no PTR record
0 failures, 1 warnings, 1 errors.
```

在上面的代码中，请注意“no PTR record”警告，表明 `192.168.100.22` 没有反向 DNS。

如果您在比最基础水平更高的层面上配置 DNS，`dnswalk` 是一项至关重要的投资。尽早并经常使用它。

## DNS 资源

虽然本章涵盖了最必需的 DNS 信息，但完整的 DNS 讨论可以轻松填满一本厚书。以下是其他 DNS 文档资源：

- `/usr/share/doc/bind-8.2_P5/` — 请注意，确切的目录名可能因您的 Red Hat 发行版而异。此目录包含 `CHANGES`、`INSTALL`、`TODO` 和 `Version`。它还包含 `bog/`、`html/`、`misc/`、`notes/`、`rfc/` 和 `tm.ac/` 目录。`html/` 和 `rfc/` 目录特别有趣。

- `http://www.isc.org/products/BIND/bind4.html` — 旧版 BIND 4 的文档。

- `http://www.dns.net/dnsrd/` — DNS 资源目录。

- `http://www.isc.org/bind.html` — Internet Software Consortium 的 BIND 页面，包含 BIND 下载链接以及其他宝贵信息的链接。此页面还包含指向 BIND 操作指南的链接，该指南提供 HTML、Postscript 和行式打印机版本（针对 BIND 4）。

## 使用 DHCP 自动配置客户端

`DHCP` 代表动态主机配置协议（Dynamic Host Configuration Protocol）。它是一种用于动态配置主机（计算机）的协议，这意味着未配置的客户端计算机可以接入提供 DHCP 服务的局域网，并自动获得 IP 地址、DNS 服务器地址、WINS 服务器地址以及许多其他配置项，否则这些配置需要由网络管理员手动设置。管理员唯一的网络配置任务是确保每个客户端拥有唯一的 `hostname`。

显然，在一个中等规模局域网的生命周期内，这可以节省数周的配置时间。当局域网的网络地址或网络掩码变更时，它也让重新编号变得轻而易举。`DHCP` 可用于自动重新配置局域网客户端，以适应 DNS 和 WINS 服务器地址的变化。

## 配置 DHCP 服务器

第一步是检查 DHCP 是否已在服务中。使用以下命令：

```
# ps ax | grep dhcpd
```

如果你看到一个正在运行的 `dhcpd` 实例，说明它已经配置好并在运行。否则，你需要配置 `dhcpd`。这是一个简单的任务。

第一步是尝试在前台运行 `dhcpd`，并观察错误消息（如果有的话）：

```
# dhcpd -f
Internet Software Consortium DHCP Server 2.0
Copyright 1995, 1996, 1997, 1998, 1999 The Internet Software Consortium.
All rights reserved.

Please contribute if you find this software useful.
For info, please visit http://www.isc.org/dhcp-contrib.html

Can't open /etc/dhcpd.conf: No such file or directory
exiting.
#
```

在上面的示例中，注意错误消息指出它找不到 `/etc/dhcpd.conf`。如果收到此错误，下一步是创建该文件。以下是一个位于 `192.168.100.1` 的服务器简单的 `dhcpd.conf` 示例：

```
subnet 192.168.100.0 netmask 255.255.255.0 {
  range 192.168.100.200 192.168.100.240;
  option subnet-mask 255.255.255.0;
  option broadcast-address 192.168.100.255;
  option routers 192.168.100.1;
  option domain-name-servers 192.168.100.1;
  option domain-name "domain.cxm";
  option ip-forwarding on;
  option netbios-node-type 8;
}
```

上述配置指定，`192.168.100.0/24` 子网中的任何客户端都将获得 `192.168.100.200-240` 范围内的 IP 地址，广播地址为 `192.168.100.255`，默认路由为 `192.168.100.1`，DNS（相当于 `resolv.conf`）位于 `192.168.100.1`，域名为 `domain.cxm`，IP 转发开启。`netbios-node-type 8` 指的是客户端的 netbios 节点类型 H，它指示客户端首先尝试通过单播进行 netbios 解析，失败后再通过广播进行解析。这是广泛推荐的方法。

注意，上述是一个极其简单的 `dhcpd.conf`。它可以变得更加复杂。可以提供多个子网的服务，它们可以在独立的物理网络上，也可以共享一个网络。子网组可以共享属性。单个主机可以集中配置，仅使用其 MAC 地址作为标识，并且如果需要，还可以集中分配主机名。甚至可以将 DHCP 配置为拒绝来自未在 `dhcpd.conf` 中列出的主机的请求，尽管这会消除一些“即插即用”功能。

DHCP 功能强大且灵活。要了解更多信息，请参考以下 man 页面：

- `dhcpd`

- `dhcpd.conf`

- `dhcp-options`

- `dhcpd.leases`

- `dhclient`

- `dhcrelay`

创建 `/etc/dhcpd.conf` 后，再次尝试在前台运行守护进程：
