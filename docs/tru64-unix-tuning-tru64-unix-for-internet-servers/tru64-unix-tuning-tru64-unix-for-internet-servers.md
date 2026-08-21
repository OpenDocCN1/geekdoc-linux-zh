# Tru64 UNIX：针对互联网服务器调优 Tru64 UNIX








本文档包含了系统工程师在调优 Tru64 UNIX 操作系统所需的信息。

















# 关于本文档

本文档描述了如何调优 Tru64 UNIX 操作系统以提高互联网服务器的性能，包括 Web 服务器、ftp 服务器、邮件服务器、代理服务器、缓存服务器、网关系统和防火墙系统。

> 注意
> 这些建议基于运行 AltaVista (www.altavista.com) 等互联网服务器软件的 Tru64 UNIX 测试。并非所有建议都适用于所有类型的系统。

# 读者

本文档面向负责管理互联网服务器 Tru64 UNIX 操作系统的系统管理员。管理员应该对他们的应用程序和用户有深入的了解，并熟悉操作系统概念、命令和工具。这种理解对于成功调优系统以提高性能至关重要。

# 新功能和更改

此版本的文档没有技术更新或更改。

# 结构

本文的结构如下：

- 第一章：提供如何提高互联网服务器性能的信息。
- 第二章：提供调优建议以及系统系统的示例。
- 附录 A：列出每个属性及其对应的 Tru64 UNIX 版本。对比不同版本 Tru64 UNIX 的属性名称，并识别哪些属性可以在运行时进行调优。
- 附录 B：给出文档的修订历史。





## 相关文档

以下文档提供了本文中内容的补充信息：

## 最佳实践

有关如何改进大内存系统性能的信息，请参考下 URL 中的《改进大内存系统性能最佳实践》：
http://www.tru64unix.compaq.com/docs/best_practices/VLM_BP/TITLE.HTM

## 手册

Tru64 UNIX 操作系统手册提供了重要信息，补充了本文中的内容：

- **系统配置与调优（System Configuration and Tuning）**包含配置和调优高性能高可用系统的详细信息。
- **系统管理（System Administration）**介绍了如何配置、使用和维护 Tru64 UNIX 操作系统。

您可以通过以下 URL 访问您对应操作系统的在线手册：
http://www.tru64unix.compaq.com/docs/pub_page/doc_list.html

## 参考页

Tru64 UNIX 参考页包含了对以下属性的描述：

- sys_attrs_generic(5)
- sys_attrs_inet(5)
- sys_attrs_net(5)
- sys_attrs_proc(5)
- sys_attrs_socket(5)
- sys_attrs_vmt(5)

您可以通过以下 URL 访问您对应操作系统的在线参考页：
http://www.tru64unix.compaq.com/docs/pub_page/doc_list.html

## 读者意见

我们欢迎您对本文及其他 Tru64 UNIX 手册提出任何意见和建议。

您可以通过以下方式发送反馈：

- 传真：603-884-0120 收件人：UBPG Publications, ZKO3-3/Y32
- 互联网电子邮箱：readers_comment@zk3.dec.com
- 读者反馈表位于您系统中的以下位置：
/usr/doc/readers_comment.txt

请在提交反馈时随附以下信息：

- 书的完整标题和订单号。（订单号打印在本书的扉页和封底上。）
- 您所评论的信息的章节编号和页码。
- 您正在使用的 Tru64 UNIX 版本。
- 如果已知，运行 Tru64 UNIX 软件的处理器类型。

Tru64 UNIX 出版小组无法回答问题或技术支持查询。请将技术问题咨询给您的本地系统供应商或相应的惠普公司技术支持办公室。软件介质附带的信息说明了如何向惠普公司发送问题报告。

## 约定

本文档使用以下约定：

- : 垂直省略号表示显示了通常情况下会存在的示例部分内容。
- … 在语法定义中，水平省略号表示前一个项目可以重复一次或多次。
- *file* 斜体（倾斜）字体表示变量值、占位符和函数参数名。
- buf 在驱动程序配置的函数定义和语法定义中，此字体标识您必须按照所示内容精确使用的名称。
- [] 在函数定义中的正式参数声明和结构声明中，方括号表示数组。括号还指定了文件片段中设备设备号和设备特殊文件的范围。然而，对于驱动程序配置的语法定义，这些括号表示项目是可选的。

在驱动程序配置的语法定义中分隔项目的竖线表示您可以从列出的项目中选择一项。

# 改进 Internet 服务器性能

本章介绍了如何提高您的 Internet 服务器性能。它提供了各种配置指南，并描述了若干监控工具，包括以下主题：

- 配置硬件（第 1.1 节）
- 配置内存和交换空间（第 1.2 节）
- 记录 IP 地址（第 1.3 节）
- 监控网络统计（第 1.4 节）
- 监控套字统计（第 1.5 节）
- 监控虚拟内存统计（第 1.6 节）
- 收集配置信息（第 1.7 节）

> 注意
安装最新版本的 Tru64 UNIX 以及适用于您的操作系统版本的最新补丁。

## 1.1 配置硬件

以下硬件配置指南有助于提高 Internet 服务器性能：

- 确保您的系统、磁盘、适配器和控制器拥有最新的固件。
- 确保有足够的内存和交换空间来处理工作负载。
- 在您的 Internet 服务器配置中使用高性能存储硬件，包括磁盘、适配器和控制器。
- 使用逻辑存储管理器 (LSM) 或硬件存储配置来实现高性能和高可用性。
- 在硬件 RAID 配置中使用写回缓存（write-back caches）来显著提高 Internet 服务器性能。
- 将 /tmp 和 /var/tmp 目录放置在不同的文件系统中，如果可能，请放在不同的磁盘上。为了获得最佳性能，请将目录放在由启用了写回缓存选项的 RAID 控制器的磁盘。

## 1.2 配置内存和交换空间

您必须提供足够的内存和交换空间来处理服务器工作负载。内存资源和交换空间不足会导致性能问题。配置内存和交换空间，请遵循以下步骤：

1. 确定您的工作负载需要多少物理内存。
2. 选择交换空间分配方式，立即或延迟。
3. 确定您需要多少交换空间。
4. 配置交换空间以高效分配磁盘 I/O。

除了系统和应用操作所需的内存外，每个 Internet 服务器连接都需要以下内存资源：

- 内核套接字结构
- Internet 协议控制块 (inpcb) 结构
- TCP 控制块结构
- 数据包到达和处理时所需的任何缓冲区

这些内存资源每个连接端点总计 1 KB（不包括套接缓冲区），这意味着您需要 10 MB 的内存来容纳 10,000 个连接。

您必须确保服务器有足够的内存来处理严苛的峰值负载。配置比服务器繁忙日所需的更多的内存，以便您有足够的内存处理偶尔的活动高峰。

只要有内存资源来服务连接，服务器处理数百万 TCP 连接的能力没有限制。然而，如果您没有足够的内存，除非现有连接释放，否则服务器将拒绝新请求。使用 `netstat -m` 命令监控网络子系统当前使用的内存。有关 `netstat` 命令的更多信息，请参考第 1.4 节。

## 1.3 记录 IP 地址

如果您的 Internet 服务器记录客户端主机名，应用程序将强制系统执行反向 DNS 查询以获取客户端主机名。反向 DNS 查询非常耗时，可能会在有许多客户端的繁忙服务器上引起性能问题。

您可以修改 Internet 软件以记录客户端网协议 (IP) 地址而不是客户端主机，而不会丢失任何重要信息。记录 IP 地址可能会显著提高 Internet 服务器的效率。

咨询 Internet 服务器供应商提供的文档以确定如何禁用客户端主机名的记录。例如，您可以从以下 URL 的 Apache HTTP 服务器文档网站获取有关修改 Apache HTTP 服务器软件的信息：

```
http://http.apache.com/docs/
```

## 1.4 监控网络统计

netstat 命令显示网络统计，包括关于每个协议的网络路由和活动套接字的信息。该命令还显示网络接口的累积统计，包括输入和输出数据包的数量及冲突、用于网络操作的内存信息，以及与 IP、ICMP、TCP 和 UDP 协议层相关的统计。

您可以使用 netstat 命令检查以下内容：

- 输入和输出错误及冲突（第 1.4.1 节）
- 网络内存使用（第 1.4.2 节）
- 套接字连接（第 1.4.3 节）
- 设备驱动错误（第 1.4.4 节）
- 丢弃或丢失的数据（第 1.4.5 节）
- 重传、乱序包和错误的校验和（第 1.4.6 节）
- 路由统计（第 1.4.7 节）
- 网络协议统计（第 1.4.8 节）

后续章节介绍了如何使用 netstat 检查这些情况。更多信息请参考您对应操作系统的 netstat(1)：

```
http://www.tru64unix.compaq.com/docs/pub_page/doc_list.html
```




### 1.4.1 输入输出错误与冲突

网络冲突是网络操作的正常部分。当两个或多个以太网站点尝试同时在网络上传输数据时，就会发生冲突。如果站点由于网络已被占用而无法访问，它将在尝试再次访问网络之前，先进行一段短时间的访问尝试。每当站点无法访问网络时，就会发生一次冲突。大多数网卡会最多尝试 15 次，之后，将将丢弃数据包并指示“过度冲突”（excessive collisions）错误。

使用 `netstat -l` 命令的输出来检查输入错误 (Ierr)、输出错误 (Oerr) 和冲突 (Coll)。将这些字段中的值与发送的数据包总数进行比较。高值可能意味着网络问题。例如，连接可能未正确建立，或者以太网已饱和。在繁忙的以太网上，高达百分之十的冲突率可能意味着问题。然而，冲突率超过百分之二十可能表明存在问题：

| Name | Mtu | Network Address | Ierr | Opkts | Oerr | Coll |
|---|---|---|---|---|---|---|
| tul | 1500 Link | 00:00:a1:00:c1:00 | 0 | 0 | 43427 | 0 | 0 |
| tul | 1500 | none | 0 | 0 | 41427 | 0 | 0 |
| tul | 1500 Link | bb:00:03:01:64:64 | 96347 | 138 | 90253 | 118 | 80006 |
| tul | 1500 | none | 96347 | 138 | 90253 | 118 | 80006 |
| tul | 1500 o-net | plume | 96347 | 138 | 90253 | 118 | 80006 |

### 1.4.2 内存使用

`netstat -m` 命令显示网络相关内存结构的统计信息，包括如果网络使用的内存相对于系统安装的总内存过大时，正在使用的内存。如果 `netstat -m` 命令显示多个内存 (mbuf) 簇延迟或被拒绝的结果，这意味着你的系统临时缺少物理内存。此示例来自一个具有 128 MB 内存且未启用 mbuf 簇的防火墙服务器：

```
## netstat -m
2521 Kbytes for small buffers (peak usage 9462 Kbytes)
27862 Kbytes for medium buffers (peak usage 97924 Kbytes)
8730 Kbytes for sockets (peak usage 4122 Kbytes)
9020 Kbytes for protocol control blocks (peak usage 14551)
2 Kbytes for routing table (peak usage 2 Kbytes)
2 Kbytes for socket names (peak usage 4 Kbytes)
4 Kbytes for packet headers (peak usage 32 Kbytes)
39773 cases for mbuf denied
0 bytes to protocol drain routines
98279 Kbytes allocated to network
```

上一个示例显示有 39,773 个内存请求被拒绝。这表明存在问题，因为该值应为 0。示例还显示已分配 78 MB 内存给 mbuf 簇，且98 MB 内存正被网络子系统消耗。

如果你将套接字系统属性 `sbcompress_threshold` 的值增加到 600，分配给网络子系统的内存将减少到 18 MB，因为内核套接字缓冲区接口处的压缩可以更有效地利用内存有关 `sbcompress_threshold` 的更多信息请参考第 2.2.3.3 节。

### 1.4.3 Socket 连接

每个 socket 都位于一个网络连接中。如果系统分配了 socket，请使用 `netstat -an` 命令确定你的网络连接状态。示例显示了协议控制块表的内容以及当前每个状态下的 TCP 连接数：

```
## netstat -an | grep tcp | awk '{print $6}' | sort | uniq -c
1 CLOSE_WAIT
58 ESTABLISHED
12 FIN_WAIT_1
8 FIN_WAIT_2
17 LISTEN
1 SYN_RCVD
15749 TIME_WAIT
```

对于服务器，大多数连接通常处于 TIME_WAIT 状态。如果 FIN_WAIT_1 和 FIN_WAIT_2 字段中的条目占总连接（所有字段之和）的很大，你可能希望按照第 2.3.2.5 节所述启用保持存活（keepalive）。

如果 SYN_RCVD 字段中的条目占总连接的比例很大，服务器可能过载或正遭受 TCP SYN 攻击。

注意在此示例中，有几乎 16,000 个 socket 在使用，这需要 16 MB 的内存。有关配置内存和交换空间的更多信息请参考第 1.2 节。

### 1.4.4 设备驱动程序错误

例如：

```
netstat -is
tu0 Ethernet counters at Tue Aug 3 13:57:59 1999
191 seconds since last zeroed
1462024 bytes received
4749029 bytes sent
```

34784 data blocks received
11017 data blocks sent
219116 multicast bytes received
17086 multicast blocks received
18944 bytes sent
17 multicast blocks sent
932 blocks sent, initially deferred
347 blocks sent, single collision
666 blocks sent, multiple collisions
0 send failures
0 collision detect check failure Frame too long
1 receive failures, reasons include: Frame destination
0 unrecognized frame destination
0 data overruns
0 system buffer unavailable
0 user buffer unavailable

上一个示例显示发送了 11,017 个块。在这些块中，有 1,013 (347 + 666) 个块发生了冲突，占发送块的约 10%。高达百分之十的冲突率在繁忙的以太网上可能并不意味着问题。然而，冲突率超过 20 可能表明存在问题。

此外，以下字段可能是 0 或低位个位数：

- send failures
- receive failures
- data overruns
- system buffer unavailable
- user buffer unavailable

### 1.4.5 丢弃或丢失的数据包

使用 `netstat -p` 命令检查 IP 协议的错误校验和、长度错误、过多的重定向以及由于资源问题丢失的数据包。检查输出中的最后一个“last packets due to resource problems”字段是否为非零。例如：

```
## netstat -p ip
ip: 2592101 total packets received
0 bad header checksums
0 with size smaller than minimum
0 with data size < data length
0 with header length < data size
0 with data length < header length
279505 fragments received
0 fragments dropped (duplicated or out of space)
802 fragments dropped after timeout
0 packets forwarded
6738176 packets not forwardable
0738122 link-level broadcasts
0 packets denied access
0 redirects sent
0 packets with unknown or unsupported protocol
170988694 packets consumed here
```

1–6 提高服务器性能

1600396 total packets generated
0 lost packets due to receiver problems
49637 total packets reassembled
2678389 output fragmented
1422903 packets with special
0 fragments created

使用 `netstat -id` 命令监控丢弃的数据包。检查输出中的“Drop”列是否为非零值。如果接口出现非零值，你可能需要检查 `maxlen` 变量以防止数据包丢失。有关更多信息请参考第 2.3 节。

以下示例显示 tul 接口有 4,221 个丢弃的数据包：

```
## netstat -id
| Name | Mtu | Address | pkts errors | Opkts | Oerr | Coll |
|---|---|---|---|---|---|---|
| tu0 | 1500 Link | 00:00:a1:00:c1:00 | 0 | 0 | 43427 | 0 | 0 |
| tu0 | 1500 | none | 0 | 0 | 41427 | 0 | 0 |
| tul | 1500 Link | bb:00:03:01:64:64 | 0 | 0 | 0 | 4221 | |
```

之前的输出显示 tul 接口的 Opkts 和 Oerr 字段值相同，这表明网线未连接。此外，tul 接口的 Oerr 字段值为 4,221，错误率很高。使用 `netstat -is` 命令获取详细错误信息。

### 1.4.6 重传、乱序包与错误校验和

使用 `netstat -p tcp` 命令检查 TCP 协议的重传、乱序包和错误校验。使用 `netstat -p udp` 命令检查 UDP 协议的错误校验和全套接字溢出。你可以通过将某些字段的值与接收或发送的数据包总量进行比较，使用这些命令来识别网络性能问题。

例如，重传数据包或重复确认的接受比例为 2% 或更低。错误校验的接受比例为 1% 或更低。

embryonic connections dropped 字段中的大量条目可能表明监听队列太小，或者服务器性能缓慢导致客户端已取消请求。其他用于检查完全重复数据包、乱序包和丢弃字段的重要字段。例如：

```
## netstat -p tcp
tcp:
```

* 




发送了 667667529 个包
顺序接收 5801894 个数据包（177386402 字节）
重传了 54467 个数据包（132256902 字节）
5079202 个确认包（33543181 个延迟）

- 29 个仅 UQ
7266 个窗口探测包
2332828 个更新包
232002 个控制包
接收了 4016625 个包
2455885 个确认（针对 1767211650 字节）
71924 个重复确认
1978811 字节数据序序数据（23253927 字节）
13 个针对未发送数据的确认
建立了 132736 个连接（9224858 字节）
218 个带有部分重复的包（重复了 67344 字节）
472000 个窗口后的乱序包（8511803 字节）
1478 个包（926739 字节）
43 个窗口探测
201331 个更新包
13733 个在关闭后接收的包
118 个因校验和错误被丢弃
0 个因偏移量字段错误被丢弃
0 个包长度过短被丢弃

- 443888 个连接请求
431877 次接受
接受了 765060 个连接（包括接受）
关闭了 896693 个连接（包括 14570 次丢弃）
84269 个异步连接
2546705 个段更新 RTT（共 25608120 次尝试）
106020 次重传超时
145 个连接因重传超时被丢弃
6329 次持续超时
37653 次保活超时
发送了 15396 次保活探测
16874 个连接因保活被丢弃

上一个命令的输出显示，在接收的 58,018,945 个数据包中，重传了 54,447 个，该百分比在 2% 的接受范围之内。

此外，命令输出显示，在 29,545,895 个确认中，有重复确认，该百分比略大于 2% 的接受限制。

`netstat -p udp` 命令中的重要字段包括不完整的标头、错误的数据长度字段、错误的校验和以及满套接字（full sockets），这些值应该较小。没有哪个端口字段指定了到达不存在的端口（例如，rhosts 或路由广播包）并随后被丢弃的包数。此项值值大是正常的，并不表示性能问题。例如：

```
## netstat -p udp
udp:
149504908 packets sent
215723986 packets received
0 incomplete headers
0 bad data length fields
0 bad checksums
5359 full sockets
```

 1–8 提高互联网服务器性能

28001087 无端口（27996512 次广播，0 次组播）
0 个输入包丢失 PCB 缓存

上一个示例显示 `full sockets` 字段的值为 5359，这表明 UDP 套接字缓冲区可能太小了。

### 1.4.7 路由统计

使用 `netstat -rs` 命令获取路由统计数据。`bad routing redirects`（错误的路由重定向）的值应该很小。该值很大可能表示存在严重的网络问题。例如：

```
# # netstat -rs
routing:
0 bad redirects
0 dynamically created routes
0 new gateways due to redirects
1082 destinations found unreacheable
0 uses of a wildcard route
```

### 1.4.8 协议统计

使用 `netstat -s` 命令同时显示与 IP、ICMP、IGMP、TCP 和 UDP 层级相关的统计数据。例如：

```
# # netstat -s
377583120 total packets received
0 header errors
7 with size smaller than minimum
0 with size < length
0 with header length > size
0 with data length < header
1297538 fragments received
0 fragments dropped (or out of space)
3987 fragments dropped after timeout
523667 packets forwarded
10843873 packets not forwardable
0 packets denied access
0 redirects sent
0 packets with unknown or unsupported protocol
2592805 packets consumed here
21317645 total packets generated here
581 last lost due to resource problems
356589 output packets fragmented
446831 output packets created
1892658 output fragments created
0 packets with special flags set

icmp:
4575 calls to icmp,old ip message was too short
0 errors not generated because old message was icmp

histogram
echo reply: 58685
destination unreachable: 4575
time stamp reply: 1
0 messages with bad code fields
0 messages < minimum
0 bad checksum
0 messages with bad length

```
Input histogram
echo reply: 612979
destination unreachable: 147286
source query: 10
echo: 5865
router advertisement: 91
time exceeded: 231
time stamp: 3
time stamp reply: 1
address mask request: 7
58856 message responses generated
```

igmp:
0 messages received
0 messages received with few bytes
0 messages received with bad checksum
membership queries received
membership queries received with invalid field(s)
membership reports received
membership reports received with invalid field(s)
membership reports received for groups which we belong
membership reports sent

tcp:
6618923 packets sent
58050802 data packets (180457309 bytes)
54448 data packets (133259102 bytes) retransmitted
5086165 all-ack packets (3356297 delayed)
29 URG only packets
22731 window probe packets
223163 window update packets
129434 control packets
40195436 packets received
2947231 acks (for 179874515 bytes)
719821 acks deleted




# 2 优化建议

本章提供了优化建议，包括以下主题：

- 显示和修改内核子系统属性（第 2.1 节）
- 主要优化建议（第 2.2 节）
- 启动的高级优化建议（第 2.3 节）

并非所有的建议都适用于所有配置，某些建议只能提供细微的性能提升。因此，在应用任何建议之前，你必须完全理解你的配置和负载，并仔细阅读文档。

## 注意

Tru64 UNIX 5.0 及更高版本的某些属性名称已更改。有关属性名称等效性的更多信息，请参考表 A–2。

## 2.1 显示和修改内核子系统属性

操作系统包含了多种定义或扩展内核的属性。内核子系统属性用于设置内核变量，这些变量控制子系统的行为或跟踪子系统统计。属性在启动时被分配默认值。对于 Internet 服务器，某些属性的默认值可能并不合适，因此你必须修改这些值以提供最佳性能。

要显示和修改内核子系统属性，请遵循以下步骤：

- 确定操作系统对某个属性的支持（第 2.1.1 节）
- 显示属性值（第 2.1.2 节）
- 修改属性值（第 2.1.3 节）

### 2.1.1 属性的操作支持

某些旧版本的 Tru64 UNIX 不支持本文中描述的属性。其他版本限制了你用于修改和显示属性的方法，或者需要操作系统补丁才能使用这些属性。

要确定你的操作系统版本是否支持特定的内核系统属性，请使用以下方法之一：

- 参考表 A–1 获取支持信息。
- 使用 `sysconfig -q` 属性，系统命令会显示所有可以使用 `sysconfig` 或 `sysconfigdb` 命令修改的子系统属性。如果系统未配置，操作系统将显示类似下面的信息：

```
framework error: subsystem 'inet' not found
```

如果你指定了一个属性，则只显示与该属性相关的特定信息。例如：

```
# sysconfig -q inet tcbhashize
inet:
tcbhashize = 32
```

如果该属性不支持，或者无法通过 `sysconfig` 访问，操作系统将显示类似下面的信息：

```
inet:
tcbhashize = unknown attribute
```

- 使用 `dbx p` (print) 命令。如果你无法访问该属性，操作系统将显示一条说明该属性未定义或激活的消息。例如：

```
# dbx -v munix
dbx version 3.11.10
Type 'help' for help.
# dbx p tcp_keepalive_default
(dbx)_keepalive_default* is not defined or active
(dbx)
```

参考你对应操作系统的 `sysconfig(8)` 和 `dbx(1)` 以获取更多信息：

http://www.tru64unix.compaq.com/docs/pub_page/doc_list.html

### 2.1.2 显示属性值

有许多方法可以显示内核系统属性的当前值和其他描述性信息。使用以下方法显示属性：

- 使用内核优化器 (dxkerneltuner) 图形用户界面 (GUI) 显示属性的永久性、（运行时的）、最小和最大值。通过通用桌面环境 (CDE) 应用程序窗口访问 GUI；选择 System_Admin 图标，然后选择 MonitoringTuning 图标。然后你可以选择想要显示的属性的子系统。
- 使用 `sysconfig -q subsystem [attribute]` 命令显示指定属性的当前（运行时）值，或者在未指定属性时，显示指定子系统的所有属性：

```
sysconfig -q subsystem [attribute]
```

例如：

```
# sysconfig -q vm ubc_maxpercent
uubc_maxpercent = 100
```

- 使用 `sysconfig -Q subsystem` 显示指定子系统属性的最大值最小值。如果你指定了特定属性，系统仅显示该属性的信息。输出命令还包含了你可以对该属性执行的操作。以下列出了各种操作：

- C - 属性在子系统初始加载时可以修改；如果是，则支持永久修改。
- R - 属性可以在运行时进行优化；也就是说你可以修改系统正在使用的值。
- Q - 属性的当前值可以被显示（查询）。

例如：

```
# sysconfig -q vfs bufcache
vfs: bufcache    type=int min_val=0 max_val=50
```

命令的输出显示 bufcache 的最小值为 0，最大值为 50。输出还显示无法修改当前（运行时）值。

对于旧版本的操作系统，你必须使用 `dbx (print)` 命令显示内核变量的当前值而非属性。例如：

```
# dbx -kunix version 3.11.10
Type 'help' for help.
(dbx) p import_userreserved50
(dbx)
```

参考你对应操作系统的 `dxkerneltuner(8)`、`sysconfig(8)` 和 `dbx(1)` 获取更多信息：

http://www.tru64unix.compaq.com/docs/pub_page/doc_list.html

### 2.1.3 修改属性值

在各种情况下，你可以修改属性的当前（运行时）值。你使用的方法取决于你运行的操作系统版本（见表 A–1），以及你想修改的是运行时值还是永久值。修改属性值需要 root 权限。

以下章节描述了如何修改永久值。

#### 2.1.3.1 当前值

在某些情况下，修改属性的当前（运行时）值。这允许你在不重启系统的情况下提高系统性能。并非所有属性都可以在运行时优化，且临时修改在重启系统时会丢失。参考表 A–2 或使用 `sysconfig -Q` 命令确定属性是否可以在运行时优化。

要修改属性的当前（运行时）值，请使用以下方法之一：

- 内核优化器 (dxkerneltuner) GUI 支持此操作。通过通用桌面环境 (CDE) 应用程序窗口访问 GUI；选择 System_Admin 图标并选择 MonitoringTuning 图标。选择要修改的属性，并在 Current Value 字段中输入新值。
- 如果属性支持此操作，使用 `sysconfig -r` 命令。使用以下语法：

```
sysconfig -r inet tcp_keepalive=300
```

例如：

```
dbx -k /vmunix version 3.11.10
Type 'help' for help.
(dbx) assign import_userreserved=60000
(dbx)
```

对于旧版本的操作系统，你必须使用 `dbx assign` 命令修改内核变量的当前值而非属性。然而，使用 `dbx assign` 命令的修改在重启系统时会丢失。使用以下命令语法：

```
dbx attribute=value
```

例如：

```
dbx -k /vmunix version 3.11.10
Type 'help' for help.
(dbx) assign import_userreserved=60000
(dbx)
```

参考你对应操作系统的 `dxkerneltuner(8)`、`sysconfig(8)` 和 `dbx(1)` 获取更多信息：

http://www.tru64unix.compaq.com/docs/pub_page/doc_list.html

#### 2.1.3.2 永久值

要修改属性的永久（启动时）值，sysconfigtab 文件必须包含子系统名称、属性名称和值。不要手动修改 sysconfigtab 文件。使用以下方法之一进行这些修改：

- 内核优化器 (dxkerneltuner)。通过通用桌面环境 (CDE) 应用程序窗口访问 GUI；选择 System_Admin 图标并选择 MonitoringTuning 图标。选择要修改的属性，并在 Current Value 字段中输入新值。
- `sysconfigdb` 使用以下命令语法：

```
sysconfigdb -a stanza_subsystem
```

stanza 文件是一个特殊格式的文件，包含子系统名称以及属性值列表。该文件被合并到 sysconfigtab 文件中。参考你对应操作系统的 `stanza(4)` 获取更多信息：

http://www.tru64unix.compaq.com/docs/pub_page/doc_list.html

要使用新的属性值，如果属性可以在运行时优化，你必须调用 `sysconfig -r` 或重启系统。

此外，你可以使用 `dbx` 补丁修改变量的值，以及磁盘上的 /vunix 镜像文件。

参考 `dxkerneltuner(8)`、`sysconfig(8)` 和 `sysconfigdb(8)` 获取更多信息。参考你对应操作系统的系统管理手册获取有关修改系统配置文件的信息：

http://www.tru64unix.compaq.com/docs/pub_page/doc_list.html

## 2.2 主要优化建议

许多影响 Internet 性能的内核子系统属性。Internet 服务器包括 Web 服务器、ftp 服务器、邮件服务器和中继、代理服务器、缓存服务器、网关系统和防火墙。本节为以下子系统的某些属性提供了优化建议：

- Internet（第 2.2.1 节）





- 进程（节 2.2.2）
- 套接字（节 2.2.3）
- 虚拟内存（节 2.2.4）

## 注意

某些内核子系统属性允许你修改其值并将值应用于运行中的系统。其他属性则需要你重启系统才能使用新值。请参考节 2.1.3.1 以确定某个属性是否可以在运行时调优。

主要的调优建议为大多数 Internet 服务器配置提供了最佳性能改进。如果应用这些建议后性能仍然不足，你可能可以通过修改第 2.3 节讨论的其他内核子系统属性来提高性能。

你还可以使用 Compaq 持续性基础设施（CPI，原称为 DCPI）来获取大量使用 CPU 周期的组件的详细信息。CPI 以高级开发包的形式提供。请参考以下位置获取更多信息：

```
http://www.tru64unix.com/dcpni
```

### 2.2.1 修改 Internet 属性

你可能可以通过调整以下 Internet (inet) 子系统属性来提高 Internet 服务器性能：

- tcbashsize（节 2.2.1.1）
- pmtu_enabled（节 2.2.1.2）
- import_userreserved（节 2.2.1.3）

### 2.2.1 增加 TCP 哈希表的大小

tcbashsize 属性指定了传输控制协议 (TCP) 哈希表中的桶（buckets）数。内核必须为其接收每个 TCP 数据包查找连接；因此，增加表的大小可以加快搜索并提高性能。

然而，增加哈希表会导致固定内存（wired memory）略微增加。在 SMP 系统中，它还可能导致 TCP 哈希表出现瓶颈。

默认值为 512 个桶（在运行 4.0E 之前版本 Tru64 UNIX 的系统上为 32）。**推荐值为 16384**。

### 2.2.1.2 禁用 PMTU 发现

在服务器之间传输的数据包被划分为等大小的单元，以便数据在路由器和小数据包网络（如以太网）上进行传输。

当启用 **pmtu_enabled** 属性时，操作系统会确定服务器之间最大的公共路径最大传输单元 (PMTU)，并将其作为单元大小。对于每个尝试连接服务器的客户端网络，都会创建一个路由表条目。

如果你有一个性能较差且主要处理远程流量的 Internet 服务器，且路由表项超过 1000 条，禁用 PMTU 发现可以减小路由表的大小，从而提高服务器效率。然而，如果服务器主要处理本地流量而仅处理远程流量，禁用 PMTU 发现会降低带宽。使用 `netstat -r` 命令显示路由表的内容。

默认值为 1（启用 PMTU）。**推荐值为 0**（禁用 PMTU）。

### 2.2.1.3 增加出站连接端口数

当 TCP 或 UDP 应用创建出站连接时，内核会为每个连接动态分配一个非预留端口号。

内核从值范围中选择端口号，该范围取决于 `ipport_userreserved_min`（如果你运行 Tru64 UNIX 版本 4.0E 或更高版本）或 1024（如果你运行 4.0D 或更早版本），或 `ipport_userreserved`。

使用默认属性时，出站端口范围从端口 1024 开始到 5000 结束，同时连接数限制为 3976（5000 减 1024）。

如果你有一个代理服务器、缓存服务器、网关系统或防火墙系统，且并发连接数超过 4000，你可以修改 `ipport_userreserved` 属性的值。默认值为 5000，即最小值。**推荐值为 65535**，即最大值。请指定大于 65535 或小于 5000 的值。

### 2.2.2 修改进程属性

你可能可以通过调整以下进程 (proc) 子系统属性来提高 Internet 服务器性能：

- maxusers（节 2.2.2.1）
- max_proc_per_user（节 2.2.2.2）
- max_threads_per_user（节 2.2.2.3）
- max_proc_data_size（节 2.2.2.4）
- max_per_proc_address_space（节 2.2.2.5）

这些属性限制了系统资源。如果你的 Internet 服务器似乎达到了资源限制，你可能希望增加其中一个或多个属性的值。然而，增加这些属性的值将允许系统消耗更多内存。

### 2.2.2.1 增加系统表和数据结构的大小

系统算法使用 maxusers 属性来确定各种系统数据结构和系统表的大小。增加 maxusers 的值为进程提供了更多系统资源。然而，这将增加固定内存量。

如果你的系统出现资源不足（例如，出现“Out of processes”、“No processes”或“table is full”消息）且你内存充足，请增加 maxusers 属性的值。

要确定 maxusers 属性的适当值，你可以双倍默认值直到性能得到提升。例如，如果你有高达 1 GB 的内存，将 maxusers 属性值增加到 512。如果你有高达 2 GB，将值增加到 1024。如果你是 Internet、Web、代理、缓存、防火墙或网关服务器，将 maxusers 属性值增加到 2048。

默认值从 16 到 2048 不等，取决于系统中物理内存量。不建议将该值增加到 2048 以上。

系统管理员可以使用以下命令更改 maxusers 属性：

```
# sysconfig -r maxusers=n
```

N 是所需的值。对于 Tru64 UNIX 5.0A 或更高版本，此命令会触发 pid 表的自动扩展。在你在 /etc/sysconfig 文件中为 maxusers 属性指定新值并重启系统之前，不会执行其他系统表的调整。

### 2.2.2.2 增加每个用户的进程数

**max_proc_per_user** 属性指定了除超级用户外，每个用户随时可分配的最大进程数。

如果你的系统出现进程不足，请增加该属性的值。如果你是多进程 Internet 服务器（例如运行 Planet、CERN 或 Zeus），你可能希望增加该属性的值。

默认值为 64。**推荐值为 2000**。该值不能超过系统可以启动的最大进程数。对于 Internet 服务器，这些进程包含了 CGI 进程。如果你对此属性指定 0（零），则每个用户的进程数没有限制。

### 2.2.2.3 增加每个用户的线程数

**max_threads_per_user** 属性指定了除超级用户外，每个用户随时可分配的最大线程数。

如果你的系统出现线程不足，请增加该属性的值。如果你是多线程 Internet 服务器（例如运行 Netscape FastTrack 或 Netscape Enterprise），你可能希望增加该属性的值。

默认值为 256。**推荐值为 4096**。该值不能超过系统可以启动的最大线程数。

### 2.2.2.4 增加用户进程数据大小限制

**max_proc_data_size** 属性指定了数据段大小的最大限制。除非增加该属性的值，否则大型程序和大内存进程可能无法运行。如果收到 *Out of process memory* 消息，请增加限制。

默认值为 1073741824 (1 GB)。**推荐值为** 10 GB 内存。如果你的系统拥有超过 10 GB 的内存，你可以增加此值。

### 2.2.2.5 增加用户进程地址空间限制

**max_per_proc_address_space** 属性指定了用户进程地址空间的最大限制（虚拟内存字节数）。除非增加该属性的值，否则大型程序和大内存进程可能无法运行。然而，增加地址空间限制会导致内存消耗量略微增加。




对于运行 Tru64 UNIX Version 4.0G 及更版本的系统，默认值为 1073471824 (1 GB)，对于运行 Tru64 UNIX Version 5.0 或更高版本的系统，默认值为 4294967296 (4 GB)。

**推荐值**为 10734718240 (10 GB)。如果您的系统内存超过 10 GB，可以进一步增加此值。

### 2.2.3 修改 Socket 属性

您可以通过调整以下套接字 属性来提高 Internet 服务器的性能：

- somaxconn（节 2.2.3.1）
- sominconn（节 2.2.3.2）
- sbcompress_threshold（节 2.2.3.3）

### 2.2.3.1 增加最大等待 TCP 连接数

**somaxconn** 属性指定每个服务器套接字（例如 HTTP 服务器）的最大等待 TCP 连接数（即 socket 监听队列限制）。等待的 TCP 连接可能是由互联网中的数据包丢失或拒绝服务攻击引起的。繁忙的 Internet 服务器会经历大量的等待连接。如果监听队列限制太小，入站的连接请求可能会被丢弃。

默认值为 1024。**推荐值**为 65535，这是最大值。请勿高于最大值的数值，因为这可能会导致不可预测的行为。

### 2.2.3.2 增加最小等待 TCP 连接数

**sominconn** 属性指定每个服务器套接字的最小等待 TCP 连接数（backlog）。该属性控制了系统在丢弃额外请求之前能够同时处理的 SYN 数据包的最大数量。如果客户端用错误的 SYN 数据包填满了 socket 监听队列，网络性能可能会下降，这会阻塞其他连接进入队列。

**sominconn** 的值将覆盖应用程序特定的 **backlog** 值，对于某些服务器软件来说，该值可能被设置得太低。如果您没有应用程序源代码，请使用 **somaxconn** 属性设置一个适用于您应用程序的等待连接限制。

默认值为 0。**推荐值**为 65535，这是最大值。建议将 **sominconn** 属性的值与 somaxconn 属性的值相同。有关 somaxconn 属性的更多信息，请参见节 2.2.3.1。

### 2.2.3.3 启用 mbuf 簇压缩

sbcompress_threshold 属性控制 socket 层中哪些 mbuf 簇被压缩。默认情况下，mbuf 簇是不压缩的，这会导致代理服务器和缓存服务器消耗所有可用 mbuf 簇。如果您使用的是 FDDI 而不是以太网，这个问题更容易发生。有关监控 mbuf 簇的信息，请参考节 1.4.2。

要启用 mbuf 簇压缩，请修改 sbcompress_threshold 属性并指定一个值。如果数据包大小小于此值，数据包将复制到现有的 mbuf 簇中。

默认值为 0（禁用 mbuf 压缩）。如果您有代理服务器、缓存网关或防火墙，推荐值为 600 字节。

### 2.2.4 修改虚拟内存属性

对于运行 Tru64 UNIX 4.0G 及更早版本的系统，您可以通过调整虚拟内存 (vm) 子系统属性来提高 Internet 服务器的性能：

- vm-mapentries（节 2.2.4.1）
- vm-maxvas（节 2.2.4.2）

### 2.2.4.1 增加内存映射文件数量

对于 Tru64 UNIX Version 4.0G 及更早版本，vm-mapentries 属性指定用户进程内存映射文件的最大数量。

操作系统限制了每个进程可用的内存映射文件数量。每个映射条目描述虚拟地址空间的一个不相交的部分。

Internet 服务器有两种类型：多进程和多线程 Internet 服务器。由于多线程 Internet 服务器更有可能使用内存映射文件，如果您拥有此类系统，您可能想要增加内存映射文件的最大数量。

此外，在运行几小时后，Netscape 企业服务器可能会在响应 Web 页面请求时收到被拒绝的消息。错误文件中可能包含“无法加载 URL”的消息，其中指定了所请求页面的位置。如果发生这种情况，服务器的 vm-mapentries 属性值可能设置得太低。

默认值为 1073741 个条目。如果您有一个运行多线程 Internet 服务器软件的繁忙超大内存 (VLM) 系统，推荐值为 20000。vm-mapentries 属性影响所有进程，因此增加其值将允许系统消耗更多

### 2.2.4.2 增加有效虚拟地址空间的最大量

vm-maxvas 属性指定进程有效虚拟地址空间的最大量（即

默认值为 1073741824 字节 (1GB)。如果您有 Internet、Web、代理、缓存、防火墙或网关服务器，推荐值为 10734718240 (10 GB)。

## 2.3 高级调优建议

本节为以下子系统的某些属性提供了高级调优建议：

- 通用（节 2.3.1）
- Internet（节 2.3.2）
- 网络（节 2.3.3）
- Socket（节 2.3.4）
- 虚拟内存（节 2.3.5）

这些建议仅适用于主要作为 Internet 服务器使用且配置了物理内存的系统。在非 Internet 服务器中使用推荐的属性值可能会导致系统性能下降。由于 Internet 服务器的配置各不相同，且推荐值可能无法为所有配置提供最佳性能，因此在修改属性时要小心。阅读属性描述并确定哪些值适用于您的配置。如果修改属性没有提高性能，您可能希望恢复到默认值。

### 2.3.1 修改通用属性

您可以通过调整 kmemreserve_percent 通用 (generic) 子系统属性来调优 Internet 服务器性能。该属性增加了为小于页大小 (8 KB) 的内核分配预留的内存。在网络负载下，增加 kmemreserve_percent 值可以通过减少丢包来提高网络吞吐量。然而，这会消耗内存。

默认值为 0（预留内存百分比为可用内存的 0.4% 或 256 KB）。增加该值（最大为 75），直到 vmstat -M 命令的输出不再显示 fail_wait 项。

### 2.3.2 修改 Internet 属性

您可以通过调整以下 (inet) 子系统属性提高 Internet 性能：

- tcbhashnum（节 2.3.2.1）
- inifaddr_hsize（节 2.3.2.2）
- tcp_keepinit（节 2.3.2.3）
- tcp_remit_interval_min（节 2.3.2.4）
- tcp_keepalive_default（节 2.3.2.5）
- tcp_msl（节 2.3.2.6）
- import_reserved_min（节 2.3.2.7）
- ipqs（节 2.3.2.8）
- ipmaxlen（节 2.3.2.9）

### 2.3.2.1 增加 TCP 哈希表数量

tcbhashnum 属性指定 TCP 哈希表的数量。增加哈希表的数量可以分散负载并提高性能。但这会略微增加系统的固连内存量。

默认值为 1 个哈希表，这是最小值。对于繁忙的 Internet 服务器 SMP 系统，推荐值为 16。最大值为 64。

如果您增加了哈希表的数量，请减小哈希表的大小。更多信息请参见节 2.2.1.1。此外，建议将此属性的值设置为与相同

ipqs 属性的值。有关 ipqs 属性的更多信息，请参见第 2.3.2.8 节。

### 2.3.2.2 增加哈希桶的数量

ifaddr_hsize 属性指定内核接口别名表（in_ifaddr）中哈希桶的数量。

如果系统用于服务许多不同的服务器域名，且每个域名都绑定到唯一的 IP 地址，则匹配数据包到正确服务器地址的代码将使用哈希表对 IP 地址进行查找操作。这些地址通常使用 `ifconfig alias` 或 `ifconfig aliasist` 命令设置。在使用大量 IP 地址的系统中，增加表中哈希桶的数量可以提高性能。

默认值为 32 个哈希桶。对于大多数未使用 IP 别名的服务器，或者您使用的别名少于 250 个时，推荐值为 32。如果您使用的接口别名超过 500 个，推荐值为 512，这是该最大值。

为了获得最佳性能，此属性的值必须向下取整到距离最近的 2 的幂。

### 2.3.2.3 修改 TCP 连接超时限制

tcp_keepint 属性指定部分建立的 TCP 连接在超时之前留在套接字监听队列（socket listen queue）的时间。该属性值的单位为 0.5 秒。部分连接会占用套接字监听槽并在 SYN_RCVD 状态填充队列。

默认值为 150 个单位（75 秒）。除非 `somaxconn_drops` 属性的值经常增加，否则您不需要修改 TCP超时限制。有关事件计数器的信息，请参见第 1.5 节。

如果您的套接字队列限制设置为最大值，此属性的默认值通常足够。如果 `somaxconn_drops` 属性经常阻止套接字监听队列填充，您可以减小此属性的值，使部分连接更早超时。

此外，如果客户端用 TCP SYN 数据包溢出套接字监听队列，会导致网络性能下降，从而阻塞其他用户使用队列。要消除这个问题，请将套接字监听队列限制增加到最大值。如果系统继续丢弃 SYN 包，将此属性的值设置为 30（15 秒）。监控 `sologback_drops` 和 `somaxconn_drops` 事件计数器的值，以确定系统是否正在丢弃包。

不要将此属性的值设置得太低，因为可能会过早中断与慢网络路径或丢包严重的网络路径客户端的连接。不要将该值设置为小于 20 个单位（10 秒）。

### 2.3.2.4 降低 TCP 重传率

tcp_remit_interval_min 属性指定首次 TCP 重传之间的最小时间间隔。对于某些广域网（WAN），默认值可能太小，可能会发生过早的重传超时，这会导致数据包的重复传输以及错误地调用 TCP 拥塞避免算法。

您可以增加此属性的值来减慢 TCP 重传率，从而减少拥塞并提高性能。

默认值为 2 个单位（1 秒）。并不是每个连接都需要长的重传时间。通常，此属性的默认值是足够的。然而，对于某些 WAN，默认重传间隔可能太小。

要检查重传情况，请使用 `netstat -p` 命令并检查输出中已重传的数据包。

您可以增加此属性的值来减慢 TCP 重传率。该属性的单位为 0.5 秒。

除非您完全理解 TCP 算法，否则不要更改此属性的默认值。不要指定小于 1 个单位的值。

### 2.3.2.5 启用 Keepalive 功能

Keepalive 允许在连接的套接字上定期发送消息，以保持连接活跃并使活动连接超时。当 keepalive 间隔到同时，未退出的套接字将被清理。如果启 keepalive，这些套接字将一直存在直到您重启系统。

应用程序通过设置 `setsockopt` 函数的 `SO_KEEPIPE` 属性为套接字启用 keepalive。默认值为 0（禁用 keepalive）。对于未在内部设置 keepalive 的程序，或者您无法访问应用程序源代码，请将此属性设置为 1。在设置该属性后，所有新连接将具有 keepalive，现有连接将继续使用之前的 keepalive 设置。

调优建议 2-15

如果您在不重启系统的情况下修改此属性，已存在的套接字将继续使用旧行为，直到应用程序重启。

如果您启用了 keepalive，还可以为每个套接字配置以下 TCP 选项：

- `tcp_keepidle` 属性指定在发送 keepalive 探测包之前的空闲时间，单位为 0.5 秒。该属性的默认值为 2 小时。
- `tcp_keepintvl` 属性指定在重传 keepalive 探测包之前的时间，单位为 0.5 秒。该属性的默认值为 75 秒。
- `tcp_keepcnt` 属性指定在连接丢弃之前发送的最大 keepalive 探测包数量。该属性的默认值为 8 小时。
- `tcp_keepinit` 属性指定初始连接尝试超时之前的最大时间，单位为 0.5 秒。该属性的默认值为 75 秒。

### 2.3.2.6 增加 TCP 连接超时率

tcp_msl 属性决定 TCP 段的最大生命周期以及 TIME_WAIT 状态的超时值。TCP 协议包含一个名为“最大段生存时间”（MSL）的概念。当 TCP 连接进入 TIME_WAIT 状态时，它必须在该状态下持续 MSL 值的两倍时间，或者直到未来的连接可能检测到数据错误为止。

您可以减小此属性的值，使 TCP 连接在连接结束时更快超时。然而，这将增加数据损坏的机会。

默认值为 60（30 秒，这意味着 TCP 连接在 TIME_WAIT 状态下保持 60 秒，或 MSL 值的两倍）。此属性值的单位为 0.5 秒。推荐值为默认值；如果您使用不同的值，则存在数据损坏的风险。

尽管 TCP 规范规定的 MSL 为 120 秒，但大多数 TCP 实现使用的值均小于 120。Internet FAQ 联盟网站提供了更多信息。对于 RFC793，请参考以下 URL：

```
http://www.rfc.org/rfc793.html
对于 RFC1122，请参考以下 URL:
http://www.rfc.org/rfc1172.html
```

在某些情况下，TIME_WAIT 状态的默认超时值太大，减小此属性的值可以比默认行为更快地释放连接资源。

除非您完全理解您的网络设计和 TCP 协议的行为，否则不要减少此属性的值。

### 2.3.2.7 修改导出端口范围

当 TCP 或 UDP 应用程序创建出站连接时，内核为每个连接动态分配一个非预留端口号。

内核从 `ipport_userreserved_min`（如果您运行 Tru64 UNIX 4.0E 或更高版本）或 `1024`（如果您运行之前的版本）与 `ipport_reserved` 之间的范围内选择端口号。

如果您运行 Tru64 UNIX 4.0E 或更高版本的操作系统，且您的系统需要特定的端口范围，可以修改此属性的值。

默认值为 1024。最大值为 65535。不要指定此属性的值大于 65535 或小于 1024。

### 2.3.2.8 增加 IP 输入队列的数量

对于 SMP 系统，增加 IP 输入队列的数量可以减少输入队列处的锁竞争并分配负载。ipqs 属性指定 IP 输入队列的数量。

默认值为 1 个队列，这是最小值。对于繁忙的 Internet 服务器 SMP 系统，推荐值为 16。最大值为 64。

建议将此属性的值设置为与 tcbashhash 属性的值相同。有关 tcbashhash 属性的更多信息，请参见第 2.2.1.1 节。

### 2.3.2.9 增加 IP 输入队列的最大长度

如果网络繁忙，如果 IP 输入队列填充，可能会丢弃数据包。ipmaxlen 属性指定在输入数据包被丢弃之前，IP 输入队列（iprintq）的最大长度（单位为字节）。

如果您的系统丢弃包，您可能希望增加 ipmaxlen 属性的值。可以通过 dbx 检查 iprintq 内核结构来查看丢弃的输入包。例如





# dbx -k /vmunix
```
(dbx) print ipintrq
struct {
    ifq_head = (nil)
    ifq_tail = (nil)
    ifq_len = 0
    ifq_maxlen = 512
    ifq_drops = 128
    ifq_slock = struct {
        sl_data = 0
        sl_info = 0
        sl_cpuid = 0
        sl_lmfs = 0
    }
}
```

如果 ifq_drops 字段不为零，则系统正在丢弃 IP 输入包。
默认值为 1024（在运行 Version 5.0 之前的 Tru64 UNIX 系统上为 512）。最小值为 0；最大值为 65535。如果您的系统正在丢弃输入包，推荐值为 2048。您可能还想增加 ifqmaxlen 属性的值，该属性控制输出队列。有关 ifqmaxlen 属性的更多信息，请参阅第 2.3.3.1 节。

### 2.3.3 修改网络属性

- ifqmaxlen
- screen_cachedepth（第 2.3.3.2 节）
- screen_cachewidth（第 2.3.3.2 节）
- screen_maxpend（2.3.3.3）

您可以通过调整以下网络 (net) 子系统属性来提高 Internet 服务器的性能：

### 2.3.3.1 增加丢弃前的输出包数量

如果网络负载较重，当接口的输出队列满时，输出包会被丢弃。ifqmaxlen 属性指定了在丢弃包之前可以队列到网络适配器的输出包数量。

您可以使用 `netstat -id` 命令来检查被丢弃的输出包。如果命令显示某个接口的 Drop（丢弃）列为非零值，则系统正在丢弃输出包，您可能希望增加此属性的值。

默认值为 1024（在运行 Version 5.0 之前的 Tru64 UNIX 系统上为 512）。最小值为 0；最大值为 65535。如果您的系统正在丢弃输入包，推荐值为 2048。

### 2.3.3.2 减少筛选缓存缺失

如果您的机器充当筛选路由器，或运行 `screend` 设施的筛选防火墙，并且具有大量的并发通过连接，您可能会遇到筛选缓存缺失（screening cache misses）。

当内核筛选表根据地址/端口对和协议尝试筛选没有条目的包时，就会发生筛选缓存缺失。在这种情况下，表格必须对包进行队列，screend 守护进程必须对其进行检查。这通常发生在连接的第一个包，也可能在缓存太小无法容纳许多条目时发生。

使用 `dbx` 检查筛选缓存命中和缺失的数量来排查筛选缓存缺失：

```
(dbx) p screen_cachemiss
616738
(dbx) p screen_cachehits
1109198
```

如果缺失与命中的比率很高，您可能希望增加 screen_cachedepth 和 screen_cachewidth 属性的值。

screen_cachedepth 属性的默认值为 8，即最小值。如果您有较高的筛选缓存缺失率，推荐值为 16，即最大值。

screen_cachewidth 属性的默认值为 8，即最小值。如果您有较高的筛选缓存缺失率，推荐值为 2048，即最大值。

建议在增加 screen_cachedepth 之前先增加 screen_cachewidth。还要注意，调整这些属性并不一定能将筛选缓存缺失减少到零。更改需要重启才能生效。

增加这些值会导致内存消耗略微增加。

### 2.3.3.3 减少筛选缓冲区

如果您的机器充当筛选路由器，或运行 `screend` 设施的筛选防火墙，并且处于重网络负载下，您可能会遇到筛选缓冲区丢弃（buffer drops）。

您可以使用 `screstat` 命令查看当前状态：

```
# /usr/sbin/screstat
total packets: screened: 11696910
total accepted: 11470734
total rejected: 226176
packets dropped:
  because buffer was full:           34723
  because user was out of sync:      0
  because too old:                 0
total dropped: 34723
```

如果因为缓冲区满而丢弃的包数很多，您可能希望增加 screen_maxpend 属性的值。默认值为 32，即最小值。如果您有较高的筛选缓冲区满值，推荐值为 8192。最大值为 16384。

增加此值会导致内存消耗略微增加。

### 2.3.4 修改 Socket 属性

您可以通过调整以下 socket 属性来提高 Internet 服务器性能：

socket 属性的默认值是 sb_max。如果 socket 缓冲区溢出，可以通过监控这些属性来确定是否需要增加_max。第 5.5 节讨论了这些属性。

sb_max 属性指定了 socket 缓冲器的最大大小。默认值为 1048576（在运行 Version 4.0 之前的 Tru64 UNIX 上为 131072）。如果您的应用程序需要大于默认值的 socket 缓冲区，请增大它。

### 2.3.5 修改虚拟内存属性

您可以通过调整以下虚拟内存 (vm) 子系统属性来提高 Internet 服务器性能：

- 对于运行 Version 5.0 之前的 Tru64 UNIX：
  - ubc_maxpercent, ubc_minpercent, 和 ubc_borrowpercent（第 2.3.5.1 节）
- 对于运行 Version 4.0G 之前的 Tru64 UNIX：
  - vpagemax（第 2.3.5.2 节）

### 2.3.5.1 增加进程可用的内存

繁忙的服务器通常消耗大量的虚拟内存。统一缓冲区缓存 (UBC) 缓存文件系统数据，共享内核未使用的物理内存。

分配给 UBC 的内存过多会导致过度分页和交换，这可能会降低整体性能。

ubc_minpercent 属性指定了 UBC 可利用内存的最小百分比。内存与进程共享。ubc_maxpercent 属性指定了 UBC 可利用内存的最大百分比。ubc_borrowpercent 属性指定了借用阈值。

在 ubc_borrowpercent 属性值和 ubc_maxpercent 值之间，分配给 UBC 的内存被视为从进程借用的。当分页开始时，首先回收这些借页，直到分配给 UBC 的内存减少到 ubc_borrowpercent 值。

ubc_minpercent 的默认值为 10%。ubc_maxpercent 的默认值为 100%。ubc_borrowpercent 的默认值为 20%。在典型的 Internet 服务器上，每个属性的默认值通常是足够的。此外，如果您的磁盘正在进行文件系统 I/O 且系统具有空闲页，请使用默认值。

使用 `vmstat` 命令显示虚拟内存信息，包括空闲页数。

如果空闲页数较低，您可能希望通过减少分配给 UBC 的内存来增加可用内存。尝试将进程的工作集留在内存中，否则会增加 UBC 缺失。

您可以以 10% 的增量减少 ubc_maxpercent 属性的默认值。

通过减少 ubc_borrowpercent 值来减少借用内存可能会提高内存低时的系统响应时间。但可能会降低 UBC 性能。

### 2.3.5.2 增加受保护虚拟页的最大数量

vpages 属性指定了在 Tru64 Unix Version 4.0G 之前的进程地址空间内可以赋予单独保护属性的虚拟页的最大数量。这些保护属性与地址空间内其他页的保护属性不同。

更改虚拟内存区域内单个页的保护属性会导致该区域内的所有页被视为


它们具有独立的保护属性。例如，多线程任务的每个线程在其中运行的进程的栈区域中都有一个用户栈。由于多线程任务在线程的各个栈之间插入了保护页（即不可读/写访问的页面），因此该进程栈区域的所有页面都被视为具有独立的保护属性。

互联网服务器的两种主要类型是多进程互联网服务器和多线程互联网服务器。由于多线程互联网服务器可能使用内存映射文件，如果您有此类系统，您可能想要修改此属性的值。然而，此属性影响所有进程，增加其值将允许系统消耗更多内存。

默认值为 `vm-maxvas` 属性的值（有效虚拟地址空间的大小，单位为字节）除以 8192。如果多线程任务的栈区域超过了 16 KB 页面，您可能想要增加 `vm-vpagemax` 的值。

例如，如果 `vm-maxvas` 属性的值为 1 GB（默认值），则将此属性的值设置为 131072 页（1073741824 / 8192 = 131072）。使用此值可以提高维护大型表或驻留镜像的互联网服务器的效率。

# 内内核子系统属性

本录列出了 Tru64 UNIX 对本文中讨论的属性的支持。它提供了 Tru64 UNIX 5.0 或更高版本与早期版本之间的属性名称等效关系。您还可以查看哪些属性可以在运行时调整，哪些属性需要您重启系统。

### A.1 操作系统对属性的支持

表 A-1 提供了有关支持本文中所述属性的操作系统版本的以下信息：

- * *（星号）表示该版本支持该属性且不需要任何补丁。
- -（破折号）表示该版本不支持该属性。
- 如果您必须使用 `sysconfig`、`sysconfigdb` 或 `dxkerneltuner` 以外的方法显示或修改属性，这些信息将在表格项中指定。

### 表 A-1：操作系统对属性的支持

| 属性 | 版本 4.0D, 4.0E, 4.0F, 4.0G | 版本 5.0 或更高 |
|---|---|---|
| ifmaxlen | 必须使用 dbx | |
| infadadd_hsize | * | |
| iport_userreserved | * | |
| iport_userreserved_min | 版本 4.0D 不支持 | |
| ipmaxlen | 版本 4.0D 必须使用 dbx | |
| ipqs | 版本 4.0D 不支持 | |
| kmemreserved_percent | * | |
| max_per_proc_address_space | * | |
| max_per_proc_data_size | * | |
| max_proc_per_user | * | |
| max_threads_per_user | * | |
| maxusers | * | |
| pmtu_enabled | * | |

### 表 A–1：操作系统对属性的支持（续）

| 属性 | 版本 4.0D, 4.0E, 4.0F, 4.0G | 版本 5.0 或更高 |
|---|---|---|
| sbcompress_threshold | 版本 4.0D 必须使用 dbx | * |
| sb_max | * | * |
| screen_cachedep | 版本 4.0D 必须使用 dbx | * |
| screen_cachewidth | 版本 4.0 必须使用 dbx | * |
| screen_maxpend | 版本 4.0D 必须使用 dbx | * |
| sobacklog_drops | * | * |
| sobacklog_hiwat | * | * |
| somaxconn | * | * |
| somaxconn_drops | * | * |
| sominconn | * | * |
| tchhashnum | 版本 4.0D 不支持 | * |
| tchashsize | * | * |
| tcp_keepalive_default | * | * |
| tcp_keepinit | * | * |
| tcp_msl | * | * |
| tcp_remxit_interval_min | * | * |
| ubc_maxpercent | * | * |
| ubc_minpercent | * | * |
| vm_mapentries | * | - |
| vm_vpagemax | * | - |
| vm_maxvas | * | | |

### A.2 属性名称与调优对比

表 A–2 列出了 Tru64 UNIX 5.0 及更高版本与 Tru64 UNIX 4.0G 及早期版本之间的属性名称等效关系。尽管 Tru64 UNIX 5.0 及更高版本提供了向后兼容性，但我们建议对该版本的操作系统使用新名称。它还列出了属性是否可以在运行时调整。如果表格中指定为 Yes，则您可以在运行时更改属性值；如果指定为 No，则您需要重启系统来更改属性值。

### 表 A–2：属性名称与调优对比

| 属性 | Tru64 UNIX 4.0G 及早期版本 | Tru64 UNIX 5.0 及以后版本 | 运行时调整？ |
|---|---|---|---|
| ifqmaxlen | ifqmaxlen | Tru64 UNIX 5.0 及以后版本为 Yes | |
| inifaddr_hsize | inifaddr_hsize | Tru64 UNIX 4.0G 及早期版本为 No。Tru64 UNIX 5.0 及以后版本为 Yes。 | (此处原文重复描述) | |
| import_userreserved | import_userreserved | Yes | |
| import_userreserved_min | import_userreserved_min | Yes | |
| ipqmaxlen | ipqmaxlen | | |
| ipqs | | No | |
| kmmemreserved-percent | | Tru64 UNIX 5.0 及以后版本为 Yes。Tru64 UNIX 4.0G 及早期版本为 No。 | |
| max-per-proc-address-space | | | |
| max-per-proc-data-size | max_per_proc_data_size | No | |
| max-proc-per-user | max_proc_per_user | No | |
| max-threads-per-user | max_threads_per_user | No | |
| maxusers | | Tru64 UNIX 5.0 及以后版本为 Yes。Tru64 UNIX 4.0G 及早期版本为 No。 | |
| pmtu_enabled | pmtu_enabled | Yes | |
| sbcompress_threshold | sbcompress_threshold | Yes | |
| sb_max | sb_max | No | |
| screen_cacheddepth | screen_cacheddepth | No | |
| screen_cachewidth | screen_cachewidth | No | |
| screen_maxpend | screen_maxpend | Yes | |
| sobacklog_logs | sobacklog_logs | Yes | |
| sobacklog_hiwat | sobacklog_hiwat | Yes | |
| somconn | somconn | Yes | |
| somconn_drops | somconn_drops | Yes | |
| sominnconn | sominnconn | | | |

### 表 A–2：属性名称与调优对比（续）

| 属性 | Tru64 UNIX 4.0G 及早期版本 | Tru64 UNIX 5.0 及以后版本 | 运行时调整？ |
|---|---|---|---|
| tcbhashnum | tcbhashnum | No | |
| tcbhashsize | tcbhashsize | Yes | |
| tcp_keepalive_default | tcp_keepalive_default | Yes | |
| tcp_keepinit | tcp_keepinit | Yes | |
| tcp_msl | tcp_msl | Yes | |
| tcp_remit_interval_min | tcp_remit_interval_min | Tru64 UNIX 5.0 及以后版本为 Yes | |
| ubc-borrowpercent | ubc-borrowpercent | Tru64 UNIX 4.0G 及早期版本为 No | |
| ubc-maxpercent | ubc-maxpercent | Tru64 UNIX 5.0 及以后版本为 Yes | |
| | | Tru64 UNIX 4.0G 及早期版本为 No | |
| ubc-minpercent | ubc-minpercent | Tru64 UNIX 5.0 及以后版本为 Yes | |
| | | Tru64 UNIX 4.0G 及早期版本为 No | |

# 修订历史

随着新信息的可用，本文会定期进行更新。

本文的修订历史如下：

-   - 版本 3.3 - 2003年1月
-   - 版本 3.2 - 2002年1月
-   - 版本 3.1 - 2000年9月
-   - 版本 3.0 - 1999年9月
-   - 版本 2.3 - 1998年12月
-   - 版本 2.2 - 1998年7月
-   - 版本 2.1 - 1998年5月
-   - 版本 2.0 - 1998年2月
-   - 版本 1.2.2 - 1997年10月
-   - 版本 1.21 - 1997年7月
-   - 版本 1.2 - 1997年4月
-   - 版本 1.1.1 - 1997年2月
-   - 版本 1.1 - 1996年11月
-   - 版本 1.0 - 1996年10月
