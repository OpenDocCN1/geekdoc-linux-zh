
这假设你在 IP 地址 `192.168.1.4` 上有一个主 DNS 服务器。一旦你在本地计算机上激活了 `named` 守护进程，就可以测试结果了。像上一节描述的那样运行 `host` 和 `dig` 命令。例如，如果 `host -l example.com` 命令不起作用，说明你添加的 DNS 转发服务器不包含关于你的 `example.com` 域的信息。

## 使用 DNS 客户端

如果你已经配置了计算机与互联网通信，你已经将其设置为了 DNS 客户端。当你想要访问另一台计算机时，你会查找一个主机名和 IP 地址的数据库。

正如第 16 章所讨论的，有两个主机名和 IP 地址的数据库：`/etc/hosts` 和 `/etc/resolv.conf` 中列出的 DNS 服务器。如果你在自己的网络上配置了 DNS 服务器，请确保其 IP 地址包含在 `/etc/resolv.conf` 中。否则，将你的 ISP 分配的 DNS 服务器添加到此处。

你的计算机所使用的数据库由 `/etc/host.conf` 文件决定。该文件通常包含一行：`order hosts,bind`。这意味着你的计算机在搜索 `/etc/resolv.conf` 中列出的任何 DNS 服务器之前，会先在 `/etc/hosts` 中查找 IP 地址，你可以根据第 16 章中的说明对其进行配置。不需要额外的配置。

## 设置 DHCP 服务器

动态主机配置协议 (DHCP) 可以自动为你网络上的所有 TCP/IP 计算机提供其通信所需的信息。这包括路由器、DNS 服务器、其他类型的服务器以及基本的 IP 划分信息。

要将计算机配置为 DHCP 服务器，你需要确保网卡能够处理多播请求。如果你有较旧的 Microsoft Windows 计算机，还应该将广播地址设置为专用路由。然后你可以配置 DHCP 配置文件 `/etc/dhcp.conf`。如果你想为远程网络使用 DHCP 服务器，你还需要在局域网之间的路由器/网关上配置 `dhcprelay`。`dhcprelay` 守护进程支持 BOOTP 协议。

DHCP 服务器作为 Network Server 组的默认部分安装。或者，你可以使用适当的 `rpm` 命令安装它。在编写本文时，没有用于配置 DHCP 服务器的 Red Hat GUI 工具。

## 基本配置

在开始配置 `/etc/dhcp.conf` 之前，你需要检查关于你网络的几点。你的网卡需要支持多播。你可能还需要启用广播地址。

多播支持可能已经内置在你的网卡和内核中。要检查这一点，运行 `ifconfig` 命令。你应该能看到网卡的输出如下：

```
UP BROADCAST RUNNING MULTICAST MTU:1500 METRIC:1
```

如果在该行中没有看到 `MULTICAST`，你需要为内核配置多播支持。详情请参阅第 12 章。

如果你的网络上有较旧的客户端（例如 Windows 95），你需要配置指向 `255.255.255.255` 的路由。要在你的以太网上设置此项，运行以下命令：

```
# route 255.255.255.255 eth0
```

## 配置文件：/etc/dhcp.conf

现在你可以配置主 DHCP 配置文件 `/etc/dhcp.conf`。从 `/usr/share/doc/dhcp-*` 目录下的示例文件开始。它列出了 IP 地址，你需要将其更改以匹配你的网络设置。

要了解更多关于 DHCP 服务器的信息，分析该文件可能会很有帮助。以下是示例文件的部分摘录。第一行允许动态 DNS 更新，显示如下。如果你的网络适用 IP 地址不同，请相应替换。

```
ddns-update;
```

你可能不想让个人用户更新 DNS 服务器中的主机名或 IP 地址，因此可以使用此命令：

```
ignore-client-updates;
```

或者，你可以使用 `allow-updates` 命令，允许用户更新主机名或 IP 地址。

以下行设置了允许的 IP 地址范围。这些地址可能为特定计算机预留：

```
subnet 192.168.0.0 mask 255.255.255.0
```

如果你的局域网连接到另一个局域网，应该有一个连接你的局域网和对方的网关 IP 地址。以下命令指定了该网关 IP 地址：

```
option routers 192.168.0.1;
```

接下来的命令非常简单；它指定了子网掩码（也称为网络掩码）：

```
option subnet-mask 255.255.255.0
```

如果你为网络配置了 NIS 授权数据库，可以指定它的域（替换此命令中的 domain）。有关 NIS 的更多信息，请参见第 23 章。

```
option nis-domain 'domain.org';
```

当然，你的网络可能有一个域名。根据本章前面的示例，此命令中的内容可能是 `example.com`，请将你的局域网域名替换为 `domain.org`。

```
option domain-name 'domain.org';
```

如果你在局域网上设置了 DNS 服务器，请在这里列出其地址。它可以帮助此 DHCP 服务器找到你所需的 DNS 服务器。你可以使用类似的标识符来识别入站邮件服务器（`option pop-server` 或 `smtp-server`）、Web 服务器（`option www-server`），甚至用于日志文件的服务器（`option log-server`）。

```
option domain-name-servers 192.168.1.1;
```

下一步帮助你同步时钟。时间相对于格林尼治时间 (GMT) 的秒。

```
option time-offset -1800;
```

某些时钟比其他的快。如果你有多个计算机运行相同的进程（例如 Web 服务器），同步它们的时钟可能是重要的。这可以通过网络时间协议 (NTP) 服务器实现：

```
option ntp-servers 192.168.1.1;
```

Linux 时钟是基于 Microsoft Windows 网络配置的一部分。微软名称服务之一基于 NetBIOS。

```
option netbios-servers 192.168.1.1;
```

可以将 DHCP 服务器配置为“p-节点”计算机；换句话说，它会查找 WINS 服务器和可能的 LMHOSTS 文件进行名解析。

```
option netbios-node-type 2;
```

你可以配置一个 IP 地址范围分配给远程网络上的计算机（如果你只为局域网服务，请从此行删除 `dynamic-boot` 变量）。这些地址必须位于定义的网络地址范围内。

```
range dynamic-boot 192.168.0.128 192.168.0.254
```

DHCP 服务器临时分配 IP 地址。IP 地址第一次续约的由 `default-lease-time`（秒）决定。

```
default-lease-time 21600
```

IP 地址应通过 `max-lease-time`（秒）进行续约。

```
max-lease-time 43200
```

你可以根据特定计算机网卡的硬件地址分配固定的 IP 地址：

```
host ns {
  hardware ethernet 12:23:34:45:AB:CD
  fixed-address 207.175.42.254
}
```

一旦你为局域网自定义了此文件，将其保存为 `/etc/dhcpd.conf`。我在图 19.7 中说明了我对我的网络的操作。

## 启动 DHCP 服务器

要运行 Linux DHCP 服务器，你需要一个已经拥有 IP 地址的网卡。如有必要，如第 16 章所述，使用 `ifconfig` 命令分配 IP 地址。

## 图 19.7 私有网络 /etc/dhcpd.conf

```
ddmsns-update-style interim;
ignore client-updates;
allow bootstrap;
allow bootstrap;
subnet 192.168.1.0 mask 255.255.255.0 {
  # default gateway
  option routers 192.168.1.113;
  option subnet-mask 255.255.255.0;
  option domain-name "example.com";
  option domain-name-servers 192.168.1.4;
  option time-offset -3800; # Eastern Standard
  range 192.168.1.128 192.168.1.254;
  default-lease-time 2160;
  max-lease-time 43200;
  # we want the name to appear at a fixed address
  host {
```
