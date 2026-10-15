

available, maybe even Linux v2.0. I assume any newer versions will have the same, or at least a very comparable, version of the firewall code in the kernel.

我有几个选择该内核版本的原因。首先，内核的防火墙代码已经改进。版本 1.3.68 允许你为三种类型的流量指定规则：入站、出站和转发。这反过来使你能够精确指定哪些流量是受信任的，哪些流量被视为危险的。此外，IP 伪装也得到了改进。

要使用新的防火墙规则集，你需要一个特殊的防火墙管理程序版本 ipfwadm。该版本“知道”这些新规则。你不能使用旧版本（最高到内核 v1.3.65），因为它们不兼容并且肯定会造成麻烦。你可以从 ftp://ftp.xos.nl/pub/linux 下载这个新的 ipfwadm 程序。你至少需要 2.0 beta 版本。当你开始构建这个新内核时，你首先需要运行以下命令来启用和禁用内核功能。

```
make config
```

在该配置期间，你将启用硬件平台的不同硬件设备。在我的防火墙设置中，我有一块用于连接本地网络的 SMC8013 以太网卡，并使用 PPP 拨号链路连接到互联网。 （该测试网络的完整布局如图 12.2 所示。）我选择启用 PPP 支持

## Figure 12.2 A sample firewall implementation using IP masquerading, which allows you to “hide” local systems behind one IP address.

![](img/113bcc15fc2db8f0f40ac5d1e755f41c_139_0.png)

as dynamically loadable modules. Unlike statically linked drivers, modules can be loaded and unloaded at runtime. With PPP configured as a loadable module, I can take the firewall off-line by just unloading the PPP module.

我还启用 SLIP 作为可动态加载模块的支持。即使我使用 PPP 而不是 SLIP 作为拨号互联网协议，我也需要启用 SLIP 以使拨号按需守护进程 diald（v0.12）可用。该守护进程会在检测到发往互联网的流量时自动呼叫 ISP。

清单 12.1 显示了与防火墙和伪装代码相关的所有 make config 选项。构建防火墙内核时，你应使用这些相同的响应。

配置内核后你需要运行以下命令来构建内核。

```
make dep; make clean; make zImage
```

构建后，你可以启动该内核作为防火墙的软件基础。你可以开箱即用编译 ipfwadm 和 diald。构建并安装它们后，它们即可使用。

## Listing 12.1 The kernel make config options related to the firewall and masquerading code.

* Networking options
Network firewalls (CONFIG_FIREWALL) [Y/n/?] Y
Network aliasing (CONFIG_NET_ALIAS) [N/y/?] N
TCP/IP networking (CONFIG_INET) [Y/n/?] Y
IP: forwarding/gatewaying (CONFIG_IP_FORWARD) [Y/n/?] Y
IP: multicasting (CONFIG_IP_MULTICAST) [Y/n/?] N
IP: firewalling (CONFIG_IP_FIREWALL) [Y/n/?] Y
IP: accounting (CONFIG_IP_ACCT) [N/y/?] N
IP: optimize as router not host (CONFIG_IP_ROUTER) [Y/n/?] Y
IP: tunneling (CONFIG_NET_IPIP) [N/y/m/?] N
IP: firewall packet logging (CONFIG_IP_FIREWALL_VERBOSE) [N/y/?] N
IP: masquerading (ALPHA) (CONFIG_IP_MASQUERADE) [Y/n/?] Y
* (it is safe to leave these untouched)
IP: PC/TCP compatibility mode (CONFIG_INET_PCTCP) [N/y/?] N
IP: Reverse ARP (CONFIG_INET_RARP) [N/y/m/?] Y
IP: Disable Path MTU Discovery (normally enabled) (CONFIG_NO_PATH_MTU_DISCOVERY) [N/y/?] N
IP: Disable NAGLE algorithm (normally enabled) (CONFIG_TCP_NAGLE_OFF) [N/y/?] N
IP: Drop source routed frames (CONFIG_IP_NOSR) [Y/n/?] N
IP: Allow large windows (not recommended if <16Mb of memory) (CONFIG_SKB_LARGE) [N/y/?] N

## Configuring the Firewall Rules

Again, the kernel’s firewall supports three distinct groups of packet filtering rules: input, output, and forward. Each of these groups has its own set of firewall rules and, thus, needs to be configured appropriately.

输入组规则描述允许进入防火墙的流量。这些规则适用于防火墙上的所有网络接口，而不仅仅是互联网接口。每条规则给出源地址、目的地址和接口地址的组合。当 IP 数据包匹配一条规则时，它会根据规则中的操作进行处理。

输出组规则指定哪些数据包可以离开防火墙。这些规则类似于输入规则；只是流量的方向不同。

## Listing 12.2 The ipfwadm options.

```
ipfwadm 2.0beta1, 1996/02/10

Usage: /sbin/ipfwadm -A command [options] {accounting}
/sbin/ipfwadm -F command [options] {forwarding firewall}
/sbin/ipfwadm -I command [options] {input firewall}
/sbin/ipfwadm -O command [options] {output firewall}
/sbin/ipfwadm -M -i [options] {masquerading entries}
/sbin/ipfwadm -h {print this help information}

Commands:
-i [policy] insert rule (no policy for accounting rules)
-a [policy] append rule (no policy for accounting rules)
-d [policy] delete rule (no policy for accounting rules)
-l list all rules of this category
-r reset packet/byte counters of all rules of this category
-f remove all rules of this category
-p policy change default policy (accept/masquerade/deny/reject)
-c check acceptance of IP packet

Options:
-p protocol (either tcp, udp, icmp, or all)
-S address/mask [port ...] source specification
-D address/mask [port ...] destination specification
-V address interface address
-W name interface name
-b bidirectional match
-e extended output mode
-k match TCP packets with ACK set
-n numeric output of addresses and ports
-o turn on kernel logging for matching packets
-t and xor and/or masks for TOS field
-v verbose mode
-x expand numbers (display exact values)
-y match TCP packets with SYN set and ACK cleared
```

