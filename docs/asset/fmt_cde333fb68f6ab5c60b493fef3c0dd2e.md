
C 类地址 — 使用前三个字节识别 TCP/IP 网络的 IP 地址。

D 类地址 — 一种通过组播数据包同时与多个主机进行通信的 IP 地址。

E 类地址 — 不应在 TCP/IP 网络上使用的 IP 地址，仅供研究目的。

默认网关（default gateway）—— 将网络与其他网络连接的路由器。主机将来自远程网络的数据包发送到此默认网关路由器。

默认路由（default route） — 标识你的主机所属的 DNS 协议的名称。

域名命名系统（DNS） — 互联网上使用的命名系统。每个主机通过主机名和域名进行标识。

动态主机配置协议（DHCP） — 一种用于为网络主机分配 TCP/IP 配置信息的协议。

Ethereal — 一个用于捕获和检查网络 IP 数据包的图形化程序。

以太网（Ethernet） — 目前访问网络介质的标准方法。网络上的大多数适配器都使用以太网。

防火墙（firewall） — 一种允许主机丢弃符合特定标准或有害 IP 数据包的软件功能。

网路由（gateway route） — 见网络路由。

主机（host） — 可以在网络上通信的计算机。

主机 ID（host ID） — IP 地址中唯一标识网络上主机的部分。

主机路由（host route） — 指定发往特定主机数据包时必须经过路由器。

`ifconfig` 命令 — 用于查看、配置和管理网络接口上的 IP 地址。

`ifdown` 命令 — 用于停用网络接口。

`ifstatus` 命令 — 用于显示网络接口的状态。

`ifup` 命令 — 用于激活网络接口。

网络控制消息协议（ICMP） — 一种用于通知主机网络错误条件的 TCP/IP 核心协议。它也被程序（如 `ping`）用于网络诊断。

# 436 第 7 节 将 SUSE Linux Enterprise 服务器连接到网络

`互联网协议（IP）地址` — 用于标识 TCP/IP 网络上计算机的唯一地址。

`互联网协议（IP）数据包` — 在 TCP/IP 网络上发送的信息单元。

`ip 别名（ip aliases）` — 分配给网络接口的额外 IP 地址。

`ip` 命令 — 用于查看、配置和管理网络接口以及路由表。

`回环（loopback）` — 用于测试本地主机的 IP 地址。

`域名服务器（name server）` — 一个包含网络主机记录的服务器。可以查询它以解析为 IP 地址。

`netcat` 命令 — 用于使用 UDP 测试主机之间的通信。

`网络 ID（network ID）` — IP 地址中标识所在网络的部分。

`网络掩码（network mask）` — 见`子网掩码（subnet mask）`。

`网络路由（network route）` — 指定发往特定网络数据包时必须经过路由器。

`节点（node）` — 见主机。

`ping` 命令 — 使用 ICMP 测试网络连通性。

`route` 命令 — 用于查看和修改路由表。

`路由器（router）` — 将 IP 数据包从一个 TCP/IP 网络中继到另一个网络的设备。

`路由（routing）` — 将 IP 数据包从一个 IP 网络发送到另一个网络的过程。

`路由表（routing table）` — 存储在每个主机上的表，包含本地和远程路由器的列表。

`套接字（socket）` — 主机之间建立的网络连接。TCP 使用 STREAM DGRAM 套接字。

`静态路由（static route）` — 标识远程网络和用于转发数据包到该网络的路由器。

`站（station）` — 见主机。

`子网掩码（subnet mask）` — 用于确定 IP 地址中哪些部分是网络 ID 和主机 ID 的数字。

`tcpdump` 命令 — 用于捕获和检查网络上的 IP 数据包。

`traceroute` 命令 — 用于标识 IP 数据包通往远程主机的路径。

`传输控制协议（TCP）` — TCP/IP 协议套件的一部分，为网络上主机之间提供可靠通信。

`传输控制协议/网协议（TCP/IP）` — 一套用于与网络上其他计算机通信的协议。

`用户数据报协议（UDP）` — TCP/IP 协议套件的一部分，为网络上主机之间提供快速但不可靠的通信。

## 复习题

- 1. 每台计算机必须具备什么才能参与 TCP/IP 网络并通过名称联系远程网络上的主机？（选择所有适用项）

  a. IP 地址

  b. 网络掩码

  c. DNS 服务器

  d. 默认网关

- 2. 在 A 类网络中，主机 ID 默认有多长？

  a. 1 字节

  b. 2 字节

  c. 3 字节

  d. 4 字节

- 3. 以下哪些是 B 类 IP 地址？（选择所有适用项）

  a. 192.168.1

  b. 172.16.10

  c. 127.0.0.1

  d. 133.1.2

- 4. 哪个地址保留给回环（loopback）？

- 5. 使用什么名称来标识网络接口？

- 6. 哪个文件将主机名解析为 IP 地址？

  a. `/etc/resolv.conf`

  b. `/etc/sysconfig/scripts`

  c. `/etc/dns`

  d. `/etc/sysconfig`

- 7. 你可以使用什么命令配置 192.168.1.1？

- 8. 你可以使用什么命令来配置子网掩码？

- 9. 以下哪些命令可以查看 IP 配置？

- 10. 哪个文件包含启动时的静态路由？

- 11. 你可以使用哪个文件从 DHCP 获取 IP？

- 12. `/etc/resolv.conf` 中可以列出多少 DNS 服务器？

  a. 一个

  b. 三个

  c. 无限制

- 13. 你输入哪两个命令可以向 192.168.1.254 添加路由？

  a. `ip route add 188.1.254`

  b. `route add 172.16.10`

  c. `ip route add 133.1.2`

  d. `route add 192.168.1`

- 14. 主机路由指定发往特定主机数据包时必须经过路由器。

## 第 8 节

## 启用基础设施服务

在本节中，你将学习启用 SUSE Linux Enterprise Server 9 中提供的某些最常用网络基础设施服务的基础知识。

- 配置和管理网络打印服务

- 配置网络文件系统

- 管理网络上的资源

### 目标 1 配置和管理网络打印服务

为了在 SUSE Linux Enterprise Server 中配置网络打印服务，你需要了解以下内容：

- 打印机与 Linux 的支持

- CUPS 与 SUSE Linux Enterprise Server

- 如何配置 SUSE Linux Enterprise Server 网络打印机

- 如何修改 SUSE Linux Enterprise Server 网络打印机

- 如何从命令行管理打印

- 如何访问 CUPS Web 管理工具

- 如何排查 CUPS 打印系统

#### 打印机与 Linux 的支持

如果你想确认你的打印机是否受 Linux 支持（或在购买新打印机之前），请检查以下来源以查看 Linux 如何支持该打印机：

- `http://cdb.suse.de/` 或 `http://harddb.suse.de/`。这是 SUSE Linux Enterprise 打印机数据库。

- `www.linuxprinting.org/`。这包含了 linuxprinting.org 上的打印机数据库。

- `www.cs.wisc.edu/~ghost/`。这是 Ghostscript 的 页面。

- `file:/user/share/doc/packages/ghostscript/catalog.devices`。这列出了包含的驱动程序。

在线数据库始终显示最新的 Linux 支持状态。然而，Linux 发行版只能集成发布时可用的驱动程序。

因此，目前被评为“完美支持（Perfectly Supported）”的打印机，在最新 SUSE Linux Enterprise server 版本发布时可能尚未具有此状态。

#### CUPS 与 SUSE Linux Enterprise Server

CUPS（通用 Unix 打印系统）是 SUSE Linux Enterprise Server 的默认打印系统。

要理解 CUPS 如何与 SUSE Linux Enterprise Server 工作，你需要知道以下内容：

- CUPS 如何处理打印作业

- `cupsd` 打印守护进程的工作原理

### 配置和管理网络打印服务

#### CUPS 如何处理打印作业

以下是提交打印作业到在打印机上获得实际打印之间发生的事件序列：

- 打印作业由用户或程序创建。

- 待打印的文件保存在队列中。
