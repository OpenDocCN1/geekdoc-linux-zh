
多组播（Multicast）是一种较新的网络流量实现方式，一组主机在特定配置端口上监听流量。让我们了解网络上的三种主要流量类型：

- 单播（Unicast，直接发送）。一个主机直接将流量发送给另一个主机，类似于人与人之间的通话。
- 广播（Broadcast）。主机发送一组指向该网络上所有主机的包。广播就像在工作场所使用对讲机呼叫一个你不确定位置的人。
- 多组播（Multicast）。多组播类似于与特定小组进行电话会议，所有人都在监听特定端口的信息，或将对这些信息进行操作。使用多组播可以减少特殊用途所需的流量，例如使用 NetShow 和 NetMeeting 进行协作，或 RealNetworks Media 服务器。

## 范围类 (Scope Classes)

范围类是一个在理论上合理的特性，可能在某些确切知道所有办公桌位在何处的组织中获得一定人气，但普通人还无法从此特性中受益。

## 厂商特定选项

在 NT 4.0 的 DHCP 服务器实现中，没有客户端分类，它们都是平等的；它们要么获取地址，要么拥有预留。在 Windows 2000 的 DHCP 服务器中，有一个强大的新功能称为“范围类”，它允许根据厂商特定信息来分配选项。由于新 DHCP 选项的标准流程可能让 FDA 的药品审批过程看起来像飞快一样，厂商可以选择各种选项，并通过嵌入系统或 BIOS 中的数据位触发这些选项。这些选项在 RFC 2132 中有极其详尽的描述。

## 用户类支持

历史上，所有的 DHCP 客户端系统都是平等的，用户对于 DHCP 过程甚至并不重要。用户类（User classes）的出现允许 DHCP 客户端指定自己属于什么类型的客户端。例如，桌面和笔记本电脑的最佳配置之间存在差异。笔记本客户端将获得较短的租约，因为它们长时间离开网络每次都会导致一个地址闲置。同样，普通的桌面级客户端可以获得更长的租约，因为它的移动频率低，甚至不移动。可以通过这种方式设置多种选项，包括 WINS、DNS 和租约长度。

## 使用 DHCP 继代理

如果你的路由器不符合用于 DHCP 广播包转发的 RFC 1452 标准且无法升级，你可以通过安装和配置 DHCP 继代理服务，设置一个 Windows 2000 或 Windows NT 服务器 4.0 服务器作为子网之间的继代理代理。继代理是一种设备或应用程序，可以将 DHCP 或 BOOTP 消息从一个子网传递到另一个子网。

## 在 Linux 上安装 DHCP 服务器

DHCP 守护程序的软件包或安装文件包含在我见过的每一个发行版中，因此这是一个选择软件包还是编译的问题。向导将引导你完成此过程，尽管许多人可能不需要或不想配置超范围。

## 软件包还是编译？

如果你没有软件包或它无法升级，你可以通过安装和配置 DHCP 继代理服务，设置一个 Windows 2000 或 Windows NT 服务器 4.0 服务器作为子网之间的继代理代理。继代理是一种设备或应用程序，可以将 DHCP 或 BOOTP 消息从一个子网传递到另一个子网。

## 分配和管理 IP 地址信息

以下是解决此问题的方法：

1. 你必须以 root 身份登录。
2. 输入：`route add dhcpserver`
3. 查看输出结果；如果提示“未知主机”，请到第 4 步。
4. 在你的 `/etc/hosts` 文件中放置以下条目：
5. 再次尝试该名称

## 让所有参与者就绪

在开始为客户端提供 IP 地址之前，你必须设置控制你的范围、起始和结束地址以及许多其他可以完全配置客户端的选项。

你将编辑或创建一个新文件：`/etc/dhcpd.conf`。在 Red Hat 7.x 系统上（以及其他系统），你还需要通过执行命令创建租约数据：`touch /var/lib/dhcp/dhcpd.leases`。

## 理解 DHCP配置文件

让我们分段查看 `/etc/dhcpd.conf` 文件，解释其工作原理以及你可能看到或用于为客户端提供 IP 地址和其他信息的各种选项。该文件如 `dhcpd.conf` 手册页所示，包含了参数和声明。例如，“`subnet 192.168.33.0` 等将是一个声明，因为它设定了文件的拓扑结构和范围，而 `option routers` 行将是参数的示例。

### 表 7.1 dhcpd.conf 参数

| 条目文件 | 说明 |
| --- | --- |
| subnet | 设置服务器服务的子网及其子网掩码 |
| option routers | 设置默认网关，用于将流量从子网发送到其他网络，通常设置为 1 或 2；多个条目之间用逗号分隔。 |
| option subnet-mask | 设置客户端的子网掩码，单条目。 |
| option nis-domain | 传递用于认证的正确 NIS/NIS+ 域，除非运行 NIS，否则请保持注释（在行开头添加 #）。 |
| option domain-name | DNS 域名，例如客户端将把该域名附加到其主机名之后。这可能需要在客户端端使用 -D 或 -H 选项来强制客户端接受 domain.com。 |
| option domain-name-servers | 为客户端名称到 IP 地址解析请求提供 DNS 解析的服务器。也可以以完全域名 (FDN) 形式输入，例如 dns1.bigsite.com, dns2.bigsite.com。 |
| option time-offset | 客户端与格尼治标准时间 (GMT) 之间的小时差。（GMT 是所有美国军方和退役军人使用的 Zulu 时间。） |
| option ntp-servers | 设置网络时间协议服务器的 IP 地址的位置（该服务器可让你同步机器时钟）。 |
| option netbios-name-servers | WINS 或其他 NetBIOS 服务器的 IP 地址，这些地址允许客户端将 NetBIOS 名称（16 字符，微软网络）解析为正确的 IP 地址。对于 Windows 2000 之前的环境中的 Microsoft Windows 性至关重要。 |
| option netbios-node-type | 此选项对于处理过 WINS 服务器的 NT 或 Windows 2000 管理员来说很熟悉；它是客户端的节点类型，决定了搜索资源解析 NetBIOS 名称的顺序。 |
| range dynamic-boot | “range”本身允许 DHCP 守护进程动态分配该范围内的地址。如果你添加了“dynamic-boot”参数，服务器/守护进程还将动态且自动地服务 DHCP 和 BOOT 客户端。 |
| default-lease-time | 以秒为单位，这是分配给未指定特定租约长度的所有客户端的租约时间。（所有 Microsoft 客户端将获得默认租约时间，因为它们没有请求租约长度的能力。） |
| max-lease-time | 同样以秒为单位，当客户端请求特定租约长度时可以分配的最长租约。 |

### 分配和管理 IP 地址信息 169

示例 `/etc/dhcpd.conf`:

```
subnet 192.168.33.0 netmask 255.255.255.0 {
## --- 默认网关
    option routers 192.168.0.1;
    option subnet-mask 255.255.255.0;

# option nis-domain "bruson.org"
    option domain-name "bruson.org"
    option domain-name-servers 192.168.33.1;

    option time-offset -6; # 中心标准时间
    option ntp-servers 192.168.1.1;
    option netbios-name-servers 192.168.1.1;
# -- 选择点对点节点（默认是混合)。除非你非常理解 Netbios，否则不要更改此项
    option netbios-node-type 2;

    range dynamic-boot 192.168.33.128 192.168.33.254;
    default-lease-time 21600;
    max-lease-time 43200;
}
```

### 为客户端设置固定地址

```
host productionserver {

hardware ethernet 01:CU:81:2B:R5:49;

fixed-address 192.168.33.144;

}
```

示例文件的最后部分提供了一些特殊处理；这是你可以设置微软术语中所谓的“客户端预留”的地方，就像在 Windows 2000 和 Windows NT 的 DHCP 服务器中可以一样。

`host productionserver {` 此条目指的是你想要使用的名称，这可能用于引导其他主机访问其提供的服务。
