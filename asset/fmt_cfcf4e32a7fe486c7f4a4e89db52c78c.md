
在这个示例中，`eth0` 是连接到互联网的接口。`eth0` 接口没有直接出现在上面的命令行中，但它的 IP 地址就是出现在 `--to` 参数位置的那个地址。`eth1` 接口是连接到内部网络的接口。

对于互联网主机来说，所有来自内部网络主机的数据包似乎都带有 `eth0` 的 IP 地址。执行 NAT 的主机接收入站数据包，查找它们的真实目的地，使用适当的内部网络 IP 地址重写它们，然后将它们发送出去。

## 14.13 SOLARIS 网络

Solaris 提供了丰富的启动脚本。在一次贸易博览会上，我们曾获得过一份每天页面都印有杂项问问题的撕拉式配置单。1 月 1 日的问题是列出在运行 Solaris 的机器上更改主机名和 IP 地址时必须修改的所有文件。快速查看答案发现有六个文件。这是推向极端的模块化。现在，让我们来看 Solaris 网络配置。

### Solaris 基础网络配置

Solaris 在 `/etc` 和 `/etc/inet` 中冲突了一些网络配置文件。许多文件通过 `/etc/inet` 的符号链接在 `/etc/inet` 中重复，实际文件位于 `/etc/inet` 中，而链接位于 `/etc` 中。

要设置主机名，将其输入文件 `/etc/hostname` 中。更改将在机器重启时生效。某些系统仅使用短主机名；另一些则使用完全限定域名名。

`/etc/defaultdomain` 文件的命名暗示它可能被用于指定 DNS 域，但它实际上指定的是 NIS 或 NIS+ 域。DNS 域像通常一样在 `/etc/resolv.conf` 中指定。

Solaris 使用 `/etc/nsswitch.conf` 来设置对 `/etc/hosts`、NIS、NIS+ 和 DNS 进行主机名解析的顺序。我们建议查看 hosts 文件，以便于启动。`nsswitch.conf` 中的该行应该是：

```
hosts: files dns
```

如果主机通过 DHCP 获取其 DNS 服务器的地址，这就是默认配置。

Solaris 网络可以运行在传统模式或“网络自动魔法（NWAM）模式”，其中网络由 `nwam` 守护进程自主管理。NWAM 模式用于工作站，但它的可配置性有限，并且仅允许一个网络接口处于激活状态。下面的讨论假设使用传统模式。

要查看哪个活跃的网络模式，运行 `svcs:/network/physical`。应该有两个配置行，一个用于 NWAM，一个用于传统的：

```bash
solaris$ svcs svc/network/physical
STATE STIME FMRI
disabled Mar 31 svc/network/physical:default
online Mar 31 svc/network/physical:nwam
solaris$ sudo svcad disable:nwam
solaris$ sudo svcad enable:network/physical:default
```

Solaris 通过名为 `/etc/hostname.interface` 的文件配置每个网络接口的 IP 地址，其中 `interface` 是接口的名称。文件可以包含 `hosts` 文件中的主机名，也可以包含 IP 地址。`hostname.interface` 中的值被用作 `ifconfig` 的地址。`hostname.interface` 中的值被用于 `ifconfig` 的地址，因此这样更安全。启动脚本通过查看 `/etc/interfaces` 发现 IP 地址。任何子网（A, B, C）都以不同的方式配置。这是一个网掩码文件的示例：

```
# Network      netmask
128.38.0 255.255.255
128.38.192 255.255.255
128.38.192.64 255.255.255
128.38.193.0 255.255.255
128.38.193.32 255.255.255
```

Solaris 通过 `/etc/hostname.interface` 文件配置每个网络接口的 IP 地址。

### Solaris TCP/IP 网络

在 Solaris 的早期版本中，启动脚本位于 `/etc/init.d`。Solaris 10 彻底重构了服务管理的方式，现在位于 `/lib/svc`。如果指定了默认网关，Solaris 实际上会运行路由服务。但在 Solaris 10 及更高版本中，必须显式启用路由。使用 `svcs` 命令来确定路由的状态。

注意：如果机器有多个网络接口，路由会自动进入服务器模式。这通常不是你想要的。可以通过开启“静默”标志来防止路由启动：

```bash
solaris$ svccfg -s routing:default setprop routing/quiet = true
```

### Solaris 配置示例

以下是启用 Solaris 接口并添加网关路由的命令示例：

```bash
solaris$ sudo ifconfig e100g plumb
solaris$ sudo ifconfig e1000g 192.108.21.48 netmask 255.255.0 up
solaris$ sudo route add 192.108.21.254
```

以下示例显示了如何查看网络接口和路由表。前带 `sudo` 的命令必须以 root 身份运行。最后一个示例显示了 `route` 命令在其他架构上不存在的功能：`get` 参数显示了通往特定目的地的下一跳。为了适应页面，我们做了一些调整。

```bash
solaris$ ifconfig -a
lo0: flags=20010849-UP,LOOPBACK,RUNNING,MULTICAST,IPV4,VIRTUAL>
mtu 832 index 1 127.0.0.1 netmask ff000000
e1000g: flags=1000843-UP,BROADCAST,RUNNING,MULTICAST,IPV4>
mtu 1500 index 2 192.108.21.48 netmask fffffffff broadcast 192.108.21.255
solaris$ ifconfig e1000g
e1000g: flags=1000843-UP,BROADCAST,RUNNING,MULTICAST,IPV4>
mtu 1500 index 2 192.108.21.48 netmask fffffffff broadcast 192.108.21.255
```

### Solaris DHCP 配置

```bash
solaris$ netstat -nr
Routing Table: IPv4

| 目的 | 网关 | UG | Ref | Use | 接口 |
| --- | --- | --- | --- | --- | --- |
| default | 192.108.21.254 | UG | 1 | 9959 | |
| 192.108.21.0 | 192.108.21.48 | U | 1 | 4985 | e1000g0 |
| 127.0.0.1 | 127.0.0.1 | UH | 1 | 107 | |
```

```bash
solaris$ sudo route get google.com
route to: gw-in-f100-google.com
destination: default
mask: default
gateway: 192.108.21.254
interface: e1000g0
flags: <UP,GATEWAY,DONE,STATIC>
recvpipe sendpipe ssthresh rtt rttvar hopcount mtu expire
0 0 0 0 1500 0
```

Solaris 包含一个 DHCP 客户端，并因最简单、最合理的 DHCP 客户端配置而获奖：

```bash
solaris$ sudo ifconfig dhcp
```

它生效了！`ifconfig` 调用 `dhcp` 程序从 DHCP 获取接口参数，并用这些参数配置接口。你可以在 `ifconfig` 命令行中包含多个选项，以指定某个接口为主接口、设置超时、增加租用时间或显示接口状态。要手动取消 DHCP 配置，只需运行：

```bash
solaris$ sudo ifconfig dhcp drop
```

这些都非常棒，但你可能希望在启动时自动咨询 DHCP。你可以通过完全不提供任何配置文件来实现此设置（然后依赖于自动配置，类似于 Linux 的 Network-Manager），或者通过创建一个 `/etc/dhcp.interface` 文件与相应的 `/etc/hostname.interface` 文件配对。如果你愿意，`dhcp.interface` 文件可以包含传递给 `ifconfig` 命令的额外命令行参数。

`hostname.interface` 文件必须存在以便进行接线（plumbed）；但它可以保持为空白。如果 `hostname.interface` 文件不为空，启动脚本最初将使用其内容配置接口，稍后使用 DHCP 重新配置接口。

`dhcp` 从 DHCP 的视角管理接口。在其他任务中，它会协商租约扩展并在租约不再需要时取消租约。如果一个已配置了 DHCP 的接口随后被手动重新配置，`dhcp` 将停止对该接口的管理。

`dhcp` 从 DHCP 服务器收集租用值（默认路由、域名、名称服务器等），但它并不直接对大部分这些值执行操作。相反，它通过 `dhcpinfo` 命令提供这些参数。服务管理脚本通过统计 `dhcpinfo` 来获取各种信息，这些信息随后被用作 `route` 的参数、放入 `resolv.conf` 文件等。

`dhcpagent` 通过 `daemon` 设施（facility）和 `critical` 优先级将错误传输到 `syslog`。使用 `-d` 标志可以获得调试级别的 syslog 输出。

你可以检查 `/etc/dhcp` 中的文件来查看特定接口的配置。然而，接口文件 `interface.dhc` 的存在并不意味着 `dhcpagent` 当前正在控制该接口——租约可能已经过期。

### ndd: Solaris 的 TCP/IP 和接口调优

Solaris 的 `ndd` 命令在运行的系统上重新配置 TCP/IP 协议栈。也许“重新配置”这个词太重了；每个模块都暴露了参数，这些参数可以被检查并在某些情况下动态调整。

基本语法为：

```bash
ndd [-set] device ? | variable
```

如果你提供参数（必须通过 `\?` 保护不受 shell 转义），`ndd` 会返回驱动程序理解的指定设备的变量列表。如果你使用变量的供应名称，`ndd` 返回该变量的值。如果你使用 `-set` 标志并提供一个值，则指定的变量将被设置为你所指定的值。

遗憾的是，`ndd` 帮助页没有告诉你可能的设备名称，也没有没有你你在某些设备上运行 `ndd`（例如 `ip` 和 `hme`）需要 root 权限，而在另一些设备上（`tcp` 和 `udp`）则不需要。表 14.10 为你提供了一个快速参考：

#### 表 14.10 使用 Solaris 的 ndd 命令可以探测的设备

| 设备 | 描述 | 变量名 |
|---|---|---|
| `/dev/tcp` | TCP 协议变量 | `tcp_` |
| `/dev/udp` | UDP 协议变量 | `udp_` |
| `/dev/ip` | IP 协议变量 | `ip_` 和 `ip6_` |
| `/dev/icmp` | ICMP 协议变量 | `icmp_` |
| `/dev/rawip` | 等同于 `/dev/icmp` | `icmp_` |
| `/dev/arp` | ARP 协议变量 | `arp_` |

`/dev/ip` 类别下的接口特定变量名控制特定网络接口上的 IP 转发。例如，`e1000g0.ip_forwarding` 控制 `/dev/e1000g0` 上的 IP 转发。有一个全局 `ip_forwarding` 变量。

如果你有 HP-UX 机器，运行带有 `-h` 标志（帮助）的 `ndd`，它将为你提供设备名称、变量名以及每个项目的含义。

接口特定的选项（如链路速度、自动协商和巨型包支持）也可以通过 `ndd` 获取：直接运行。遗憾的是，`ndd` 页面没有告诉你可能的设备名称，也没有没有你你在某些设备上运行 `ndd`（例如 `ip` 和 `hme`）需要 root 权限，而在另一些设备上（`tcp` 和 `udp`）则不需要。表 14.10 为你提供了一个快速参考：

`/dev/ip` 类别下的接口特定变量名控制特定网络接口上的 IP 转发。例如，`e1000g0.ip_forwarding` 控制 `/dev/e1000g0` 上的 IP 转发。有一个全局 `ip_forwarding` 变量。

如果你有 HP-UX 机器，运行带有 `-h` 标志（帮助）的 `ndd`，它将为你提供设备名称、变量名以及每个项目的含义。

接口特定的选项（如链路速度，自动协商和巨型包支持）也可以通过 `ndd` 获取：直接运行。遗憾的是，`ndd` 页面没有告诉你可能的设备名称，也没有没有你你在某些设备上运行 `ndd`（例如 `ip` 和 `hme`）需要 root 权限，而在另一些设备上（`tcp` 和 `udp`）则不需要。表 14.10 为你提供了一个快速参考：

#### 表 14.11 Solaris 中相关的安全行为

| 特性 | 默认 | ndd 变量 |
| --- | --- | --- |
| IP 转发 | off | `ip_forwarding` |
| ICMP 重定向 | ignores | `ip_src` |
| 广播 ping (respond) | on | `ip_respond` |
| 广播 ping (cast) | off | `ip_broadcasts` |

Solaris 包含一个 DHCP 客户端，并因最简单、最合理的 DHCP 客户端配置而获奖：

| ARP 协议变量 | `arp_` |
| ICMP 协议变量 | `icmp_` |
| IP 协议变量 | `ip_` 和 `ip6_` |
| TCP 协议变量 | `tcp_` |
| UDP 协议变量 | `udp_` |

### Solaris 的运行特性

`ifconfig -a` 的输出在以 root 身份运行时与以普通用户运行时不同。当以 root 身份运行时，它除了显示 IP 地址和参数外，还会显示链路层以太网地址。

Solaris 允许你通过 `ifconfig` 命令和 `ether` 地址族更改网络接口的链路层（MAC）地址。如果你需要潜入一个受 MAC 限制的无线网络，此功能将非常有用。

## 14.14 HP-UX 网络

HP-UX 网络配置非常简单：所有的配置参数都设置在 `/etc/rc.config.d/netconf` 中。该文件中的值（以及 `rc.config.d` 目录下的所有其他文件）在启动时被读入环境并在机器启动时由 `/sbin/rc` 脚本使用。`netconf` 带有大量的注释，告诉你是哪些变量必须设置以及它们的含义。

### HP-UX 基础网络配置

要为机器分配主机名并配置第一个网络接口，请编辑 `netconf` 文件并为以下变量分配值：

```
HOSTNAME
INTERFACE_NAME[0]
IP_ADDRESS[0]
SUBNET_MASK[0]
```

例如：

```
HOSTNAME=disaster
INTERFACE_NAME[0]=lan0
IP_ADDRESS[0]=192.108.21.99
SUBNET_MASK[0]=255.255.255.0
```

第二个网络接口将具有子网 1，其存在将通过将变量 `NET_CARDS` 设置为 `2` 来指示。
`netconf` 文件还包含用于配置静态路由和启动路由守护进程的变量。要建立默认路由，请设置以下变量：

```
ROUTE_DESTINATION[0]=default
ROUTE_MASK[0]=0
ROUTE_GATEWAY[0]=192.108.21.254
ROUTE_COUNT[0]=1
```

要测试配置，请运行：

```
solaris$ sudo ipnat -CF /etc/ipf/ipnat.conf
```

这些选项会先删除所有现有规则，然后从 `/etc/ipf/ipnat.conf` 文件加载全套规则。
