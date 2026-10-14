
- 你的 Linux 系统正在为多个网站提供 Web 托管服务。理想情况下，每个网站的主机名都应关联一个唯一的 IP 地址。为此，你的系统必须响应所有这些 IP 地址的请求。这通常通过虚拟地址来实现。

- 你的 Linux 系统正在为多个域提供邮件服务。你可能希望服务器为每个邮件域使用不同的主机名和 IP 地址来标识。同样，这通常通过虚拟地址来实现。

假设你已经正确配置了系统以与本地局域网通信，那么添加对虚拟地址的支持只需为每个虚拟地址额外执行一条 `ifconfig` 命令即可。

在本章前面的手动配置示例中，你看到了一个配置了 IP 地址 `192.168.147.5` 的单个以太网设备 `eth0` 的系统：

```text
# /sbin/ifconfig eth0 192.168.147.5 netmask 255.255.255.0 up
```

唯一的问题是要使用哪个以太网设备。如果你尝试为设备 `eth0` 分配第二个 IP 地址，`ifconfig` 只会更改与该设备关联的 IP 地址。因此，需要使用虚拟设备。`eth0` 与特定的物理网络接口关联，而 `eth0:1`、`eth0:2`、`eth0:3` 等是与同一物理网络接口关联的虚拟设备。

因此，如果你想为 `eth0` 分配一个虚拟 IP 地址 `192.168.147.10`，请使用以下命令：

```text
# /sbin/ifconfig eth0:1 192.168.147.10 netmask 255.255.255.0 up
```

同样，要为同一个网络接口分配第三个 IP 地址 `192.168.147.15`，请使用以下命令：

```text
# /sbin/ifconfig eth0:2 192.168.147.15 netmask 255.255.255.0 up
```

完成上述操作后，使用 `ifconfig` 命令显示网络设备的当前状态时，会分别显示每个虚拟设备：

```text
# ifconfig
eth0      Link encap:Ethernet  HWaddr 00:20:AF:EB:41:69
          inet addr:192.168.147.5  Bcast:192.168.147.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:14583 errors:9 dropped:0 overruns:0 frame:9
          TX packets:521 errors:0 dropped:0 overruns:0 carrier:9
          collisions:6 txqueuelen:100
          Interrupt:10 Base address:0x300

eth0:1    Link encap:Ethernet  HWaddr 00:20:AF:EB:41:69
          inet addr:192.168.147.10  Bcast:192.168.147.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:14583 errors:9 dropped:0 overruns:0 frame:9
          TX packets:521 errors:0 dropped:0 overruns:0 carrier:9
          collisions:6 txqueuelen:100
          Interrupt:10 Base address:0x300

eth0:2    Link encap:Ethernet  HWaddr 00:20:AF:EB:41:69
          inet addr:192.168.147.105  Bcast:192.168.147.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:14583 errors:9 dropped:0 overruns:0 frame:9
          TX packets:521 errors:0 dropped:0 overruns:0 carrier:9
          collisions:6 txqueuelen:100
          Interrupt:10 Base address:0x300

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:3924  Metric:1
          RX packets:8 errors:0 dropped:0 overruns:0 frame:0
          TX packets:8 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
```

### 故障排除

由于成功配置涉及众多变量 `网络接口`、`内核模块`、`DNS 服务器`、`路由`、`网络拓扑` 等，故障排除是一个广泛的主题。很难给出针对所有可能问题的具体建议。

对 TCP/IP 网络进行故障排除需要深入理解基本的网络原理、熟悉网络环境，并熟练使用一组诊断网络工具。此外，还需要有条理地分析当前问题，并能够将问题分解为更小的部分，从而定位问题的根本原因。

在分析问题时，第一步是收集有关当前情况的详细信息。其中一些细节包括出现故障的应用程序名称、所涉及机器的主机名和 IP 地址，以及报告的错误消息。登录到有问题的机器并尝试重现问题。在不同的系统上运行相同的应用程序。

当用户报告运行特定网络应用程序时出现问题，需要检查以下可能的情况：

- 如果所有其他网络应用都运行正常，那么这个特定应用可能存在配置错误，需要找出并修复。
- 检查该应用的问题是否出现在所有主机上。这可能指向提供该特定应用的某个远程主机，而问题可能就出在那里。
- 查看远程主机是否与应用试图联系的网络不在同一网络中。如果是，到达该主机可能存在路由问题。

另外，在调试网络问题时，需要牢记一些一般性提示：

- 不要忽视显而易见的东西。检查以太网线缆、故障集线器、配置错误的交换机端口、坏的连接器和松动的线缆。
- 有条不紊地解决问题。从正常工作的部分开始测试，然后向不正常的部分推进。
- 记录你已完成的测试及其结果。
- 密切注意错误消息。错误消息记录在系统日志文件中。有时它们并不能准确告诉你问题所在，但通常能提供有助于解决问题的线索。
- 不要把帮助台人员或用户提供的问题描述当作最终定论。尝试自己复现。你常常会发现问题描述中存在不一致之处。在验证并纠正问题描述后，通常就能找到解决方案。
- 不要排除人为错误的可能。有时问题是由缺乏经验的信息系统工作人员造成的。修复问题后与他们沟通，以避免将来重复类似的错误。
- 学会熟练使用一些简单的故障排查工具。在 TCP/IP 中，你可以用少数几种工具诊断网络问题。我们将在下一节中介绍其中一些。
- 在尝试联系远程系统的网络管理员之前，确保你已彻底测试了自己这边的所有环节。如果所有测试都表明问题出在你无法控制的远程系统上，那么你应该已收集了足够的测试结果，可以与远程管理员共享，以帮助其诊断工作。

### Linux 网络故障排查工具

所有 Linux 发行版都捆绑了多个有用的网络故障排查工具。利用这些工具，可以诊断和修复绝大多数网络问题。虽然有第三方商业网络故障排查工具可用，但它们通常不是必需的，本书对此不做讨论。

表 13.4 概述了可用于问题诊断和故障排查的标准 Linux TCP/IP 工具。

**表 13.4  Linux TCP/IP 工具**

| 工具 | 描述 |
|---|---|
| `ping` | 测试基本网络连通性 |
| `traceroute` | 跟踪数据包从源系统到目标系统所经过的路由 |
| `netstat` | 显示网络连接信息；常用于检查系统路由表 |
| `ifconfig` | 显示网络接口信息，并设置接口的 IP 地址、网络掩码和广播地址 |
| `arp` | 显示本地网络上主机的 IP 地址及对应的以太网 MAC 地址 |
| `nslookup` | 查询主机名、IP 地址以及存储在 DNS 数据库中的各种其他与主机和域相关的信息 |
| `tcpdump` | 显示网络上的数据包以供分析 |

#### 使用 `ping`
