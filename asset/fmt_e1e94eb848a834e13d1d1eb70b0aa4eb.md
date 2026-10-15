
IPv4 兼容 IPv6 地址也被计划在 IPv4 到 IPv6 的过渡期间使用（RFC 2893 [Gilligan and Nordmark 2000]）。对于没有 IPv6 路由器的支持 IPv4 和 IPv6 的主机应该创建一个包含 IPv4 兼容 IPv6 地址的 DNS `AAAA` 记录。具有 IPv4 数据的 IPv6 主机通过 IPv4 头部封装 IPv6；这被称为自动隧道。然而，部署考虑减少了这一功能的使用。我们将在 B.3 中更多地讨论隧道，并在 B.2 中显示封装在 IPv4 头部中的这种类型 IPv6 的示例。

### 图 A.11. IPv4 兼容 IPv6 地址。

| 0000 | 0000 | 0000 | IPv4 地址 |

| --- | --- | --- | --- |

| 80 位 | | 16 | 32 |这种类型地址的示例是 `::12.106.32.254`。

IPv4 兼容 IPv6 地址也可能在使用 `SIIT/IPv6` 转换机制时（RFC 2765 [Nordmark 2000]）出现在未隧道化的 IPv6 报文的源或目的中。

## 回环地址

由 127 位零和单个 1 位位组成的 IPv6 地址，写为 `::1`，是 IPv6 回环地址。

## 未指定地址

由 128 位零组成的 IPv6 地址，写为 `0:0` 或仅 `::`，是 IPv6 未指定地址。

绑定一个监听 TCP 套接字，表示套接字将接受发往节点任何地址的连接。它被引用为 `inaddr_any` 或 `IN6ADDR_ANY_INIT`。

## 链路本地地址 (Link-Local Address)

链路本地地址用于单链路，当已知数据报不会被转发到链路网络之外时使用。其用例包括启动时时的自动地址配置和邻居发现（类似于 IPv4 的 ARP）。图 A.12 显示了这些地址的格式。

### 图 A.12. IPv6 链路本地地址。

| | | | | |

|---|---|---|---|---|

| 11111110 | 0000 | . | 0000 | 接口 ID |

| 10 bits | | 54 | 64 | |

这些地址始终以 `0xfe80` 开头。IPv6 路由器不得将具有链路本地源地址或目的地址的数据报转发到另一个链路。在第 11.2 节中，我们展示了与名称 `aix-611` 相关的链路本地地址。

## 站点本地地址 (Site-Local Address)

截至本文撰写时，IETF IPv6 工作组已决定废弃当前形式的站点本地地址。未来的替代方案可能也可能使用与最初为站点本地地址定义的相同地址范围 (`fec0/10`)。站点本地地址旨在用于站点内的寻址，而无需全局前缀。图 A.13 显示了这些地址最初定义的格式。

| | | | | | | | |

|---|---|---|---|---|---|---|---|

| 1111111011 | 0000 | . | 0000 | 子网 ID | 接口 ID |

| 10 bits | | 38 | 16 | 64 | |

IPv6 路由器不得将具有站点本地源地址或目的地址的数据报转发到该站点之外。

## A.6 互联网控制消息协议 (ICMP4 和 ICMPv6)

ICMP 是任何 IPv4 或 IPv6 实现中必须且不可不可缺的一部分。ICMP 通常用于在 IP 节点（包括路由器和主机）之间通信错误或信息消息，但偶尔也会被应用程序使用。例如，`ping` 和 `traceroute` 应用程序（第 28 章）都使用了 ICMP。

ICMP4 和 ICMP6 消息的前 32 位是相同的，如图 A.14 所示。RFC 792 [Postel 1981b] 文档了 ICMP4，RFC 2463 [Conta and Deering 1998] 文档了 ICMPv6。

### 图 A.14. ICMP4 和 ICMPv6 消息的格式。

| 0 | 7 8 | 15 16 | 31 |

|---|---|---|---|

| type | code | checksum | |

| | | | |

| | (剩余部分取决于类型、代码以及/具体的 ICMPv4 或 ICMPv6) | | |

8 位的 `type` 是 ICMPv4 或 ICMPv6 消息的类型，某些类型带有 8 位的 `code` 包含额外信息。校验和是标准的互联网校验和，尽管在 ICMP4 中，校验和仅覆盖从 `type` 字段开始的 ICMP 负载，而 ICMPv6 校验和还包含了 IPv6 伪头部。

从网络编程的角度来看，我们需要理解哪些 ICMP 消息可以返回给应用程序、什么会导致错误，以及如何将错误返回给应用程序。图 A.15 列出了所有的 ICMP4 消息以及 FreeBSD 如何处理它们。图 A.16 列出了 ICMPv6 消息。第三列指示了触发返回给应用程序错误的消息所返回的 `errno` 值。使用 TCP 时，错误会被记录但不会立即返回。如果 TCP 随后由于超时放弃连接，则会返回任何 ICMP 错误指示。使用 UDP 时，下一次发送或接收操作会接收到错误，但仅在使用如第 6.9 节描述的连接套接字时。

### 图 A.15. FreeBSD 对 ICMP 消息类型的处理。

| type | code | 说明 | 处理方式或 errno | 参见 RFC |

|---|---|---|---|---|

| 0 | echo request (Ping) | | 用户进程 (Ping) | 792 |

| 3 | destination unreachable: | | | 792 |

| 0 | network unreachable | `ICMP_UNREACH` | 792 |

| 1 | protocol unreachable | `ICMP_PROTOUNREACH` | 792 |

| 2 | port unreachable (reachable) | `ICMP_CONNREFUSED` | 792 |

| 4 | fragmentation needed DF bit set | `ICMP_SIZE` | 792, 1191 |

| 5 | source address failed | `ICMP_UNREACH` | 792 |

| 6 | source unreachable | `ICMP_UNREACH` | 792 |

| 7 | destination unreachable | | 792 |

| 8 | destination administratively prohibited | | 792, 1191 |

| 9 | host unreachable | `ICMP_UNREACH` | 792 |

| 10 | network unreachable | `ICMP_UNREACH` | 792 |

| 11 | host unreachable | `ICMP_UNREACH` | 792 |

| 12 | communication administratively prohibited | | 1812 |

| 14 | protocol violation | | 1812 |

| 15 | precedence exceeded | | 1812 |

| 0 | fragment re | | 792 |

| 1 | time exceeded | | 792 |

| 2 | parameter problem | | 792 |

| 3 | port unreachable | | 792 |

| 4 | source error | | 792 |

| 5 | source route failed | | 792 |

| 6 | destination route obsolete | | 792 |

| 7 | time to live exceeded | | 792 |

| 8 | parameter unreachable | | 792 |

| 9 | destination network unreachable | | 792 |

| 10 | destination port unreachable | | 792 |

| 11 | destination administratively prohibited | | 792 |

| 12 | destination timeout | | 1812 |

| 13 | parameter problem | | 1812 |

| 14 | bad message | | 1812 |

| 15 | ICMP rate | | 792 |

### 图 A.16. ICMPv6 消息。

| type | code | 说明 | 处理方式或 errno | 参见 RFC |

|---|---|---|---|---|

| 1 | destination unreachable | `EOTUNREACH` | 2463 |

| 1 | route administratively prohibited | `EOTUNREACH` | 2463 |
