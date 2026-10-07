
然而，大多数 Linux 发行版根据配置文件在启动时分配网关。Red Linux 将网关配置信息存储在 `/etc/sysconfig/network` 文件中，包含两个变量：`GATEWAY` 和 `GATEWAYDEV`。这些应设置为网关节点的 IP 地址和内部节点的内部网络接口名称。内部节点的典型网络配置文件可能如下：

```
NETWORKING=yes

FORWARD_IPV4=false

HOSTNAME=b001

DOMAINNAME=beowulf.org

GATEWAY=192.168.1.1

GATEWAYDEV=eth0
```

配置网关节点以执行 IP 映射需要稍多工作，但并不特别困难。第一个要求是编译

> 8.IP 网络地址转换器 (NAT), Internet Engineering Task Force RFC 1631, info.internet.isi.edu/in-notes/rfc/files/rfc1631.txt.

你的内核需要支持网络防火墙、IP 转发/网关化以及 IP 伪装。此外还有你可能想要包含的额外选项，但这些是基本的。关于每个选项的详细信息，可以在 Linux 内核源码树中的 `masquerading.txt` 文档文件以及 IP Masquerade HOWTO 中找到。

安装完支持 IP 伪装的内核后，你需要启用 IP 转发。在 Red Hat Linux 系统上，你可以通过将 `/etc/sysconfig/network` 中的 `FORWARD_IPV4` 变量设置为 `true` 来实现。IP 转发是主机将其接收到的并非为其目的的数据包转发到其目的地的过程。这允许节点数据包被转发到外部主机。

最后一步是配置 IP 伪装规则。你不希望你的外部节点从任何地方转发数据包，因此你必须明确告诉它要转发哪些数据包。目前，可以在 2.4.x Linux 内核上使用 `iptables` 来此；这是 2.4.x 之前的 `ipfwadm` 和 `iptchains` 工具的演进版本。

`iptables` 程序用于配置防火墙过滤和路由规则。它可以根据数据包的源和目的、接收或路由数据包的网络接口、网络协议、目的端口和源端口以及许多其他信息来指定规则。为了设置外部节点，你可以使用 `iptables` 告诉内核对源自内部节点的数据包进行伪装。可以使用如下命令：

```
iptables -t nat -P PRERUTING DROP
iptables -t nat --source 192.168.1.0/24 -j ACCEPT
iptables -t nat -P PRERUTING -j LOG
```
