
因为 Linux 中通常安装的 `traceroute` 命令不允许用户访问 IP 数据包选项，另一种使用方法是 `ping`。`ping` 用于验证主机是否可达。出于此目的，它向目标计算机发送 ICMP 请求并等待 ICMP 消息形式的回应。今天，仍有 `ping` 实现允许使用源路由和互联网时间戳。由于大多数实现的原因只保留了路由记录选项。下面的示例显示了如何使用带路由记录的 `ping`。在第一个请求之后：

```
# ping -R rzstud1.rz.uni-karlruhe.de
rzstud1.rz.uni-karlruhe.de (129.13.197.1): 56 data bytes
64 bytes from 129.13.197.1: icmp_seq=0 ttl=253 time=235.977 ms
RR: isdn216-10.rz.uni-karlruhe.de (129.13.216.100)
rzasc01.rz.uni-karlruhe.de (129.13.92.1)
129.13.197.62
rzstud1.rz.uni-karlruhe.de (129.13.197.1)
r-ascend-netz.rz.uni-karlruhe.de (129.13.92.254)
rzasc01.rz.uni-karlruhe.de (129.13.92.1)
isdn216-10.rz.uni-karlruhe.de (129.13.216.100)
64 bytes from 129.13.197.1: icmp_seq=1 ttl=253 time=47.171 ms (same route)
64 bytes from 129.13.197.1: icmp_seq=2 ttl=253 time=48.728 ms (same route)
---
rzstud1.rz.uni-karlruhe.de ping statistics --
9 packets transmitted, 9 packets received, 0% packet loss
round-trip min/avg/max = 45.100/70.5/235.97 ms
```

如果本地计算机拥有 root 权限，`tcpdump` 的详细模式允许用户查看所有 IP 数据包的选项。`tcpdump` 在网络适配器上监控数据流量。下面的示例使用详细模式下的 `tcpdump` 监控之前的 `ping` 示例。

```
# tcpdump -v
User level filter, protocol ALL, datacagram packet
tcpdump: listening on eth0
15:37:56.025267 isdn216-10.rz.uni-karlruhe.de > rzstud1.rz.uni-karlruhe.de:
icmp: echo request (tt 64, id 1284, optlen=40 RR{isdn216-10.rz-
# ksruhe.de#0.0.0.0 0.0.0.0 0.0.0.0 0.0.0.0 0.0.0.0 0.0.0.0)

EOL

15:37:56.261172 rstud1.rz.uni-ksruhe.de > isdn216-10.rz.uni-ksruhe.de:
icmp: echo reply (ttl 253, id 28562, optlen=40 RR|isdn216-10.rz.uni-ksruhe.de=rzasc01.rz.uni-ksruhe.de 129.137.96 rzstud1.rz.uni-ksruhe.de# r-ascend-netz.rz.uni-ksruhe.de rzasc01.rz.uni-ksruhe.de#
0.0.0.0 0.0.0.0 0.0.0.0 (EOL)
```

## 编程访问

我们将向你如何在如何在过程中访问 IP 数据包选项。本示例使用了版本 1.38。当 `ping` 启动时，首先会检查传递的参数。如果包含 `-R`，则回显请求（Echo Request）包必须包含路由记录（Record Route）IP 选项。为此，`ping` 使用 `setsockopt()` 函数来通知现有 socket 数据包选项。

以下示例显示了如何在 `ping` 的源码内部调用此函数：

```
if (setsockopt(s, IPPRTO_IP, IP_OPTIONS, rspace, sizeof(rspace)) < 0)
{
    perror("ping: record route");
    exit(1);
}
```

指定的选项将设置在未来通过该 socket 发送的每个数据包。`IPPRTO_IP` 参数意味着要设置的数据包选项是一个 IP 选项。这并不一定意味着它在真意义上是一个 IP 选项。它可能存在于 IP 头的其他位置（例如，`IP_TTL` 也属于 `IPPRTO_IP` 组）。从编程的角度来看，我们必须假设当前的内核实现不支持所需的 IP 选项。在这种情况下，`setsockopt()` 返回值 1 并输出错误消息。随后，将通过该 socket 发送任意数量设置了数据包选项的数据包。

`ping` 发送的入站 ICMP 包将如下方式检查其选项：计算指向协议头中第一个字段的选项指针。增加选项指针以指向下一个字段。路由记录（Record Route）选项指针必须指向一个包含数字“7”的字节。`ping` 实际上并不需要 care 这个值；像所有其他特定选项的常量一样，它被定义在 `<linux/ip.h>` 中：

```
#define IPOPT_END (0 |IPOPT_CONTROL)
#define IPOPT_NOOP (1 |IPOPT_CONTROL)
#define IPOPT_SEC (2 |IPOPT_CONTROL|IPOPT_COPY)
#define IPOPT_LSRR (3 |IPOPT_CONTROL|IPOPT_COPY)
#define IPOPT_TIMESTAMP (4 |IPOPT_CONTROL|MEASUREMENT)
#define IPOPT_RR (7 |IPOPT_CONTROL)
#define IPOPT_SID (8 |IPOPT_CONTROL|IPOPT_COPY)
#define IPOPT_SWRR (9 |IPOPT_CONTROL|IPOPT_COPY)
#define IPOPT_RA (20|IPOPT_CONTROL|IPOPT_COPY)
```

如果发现了其中一个这些数据包选项，则将其输出。

## 14.3.3 Linux 内核中的 ip_options 类

本节描述了 Linux 内核中实现的 `ip_options` 类的所有函数。如果选项被传递给函数或从函数返回，通常是通过使用 `ip_options` 数据类型完成的。该类型定义在 `<linux/ip.h>` 中，包含了所有数据包选项所需的变量、指针和常量。

### `ip_options_build()`

此函数从 socket 对象获取 IP 选项信息，并在 IP 头中创建选项部分。

这里传递的参数包括 socket 缓冲区、数据包选项、数据包目的地址、路由表以及 `is_frag` 变量。socket 缓冲区包含一个带有尚未完成的协议头的数据报。传递的数据包选项被复制到协议头的末尾。如果存在严格源路由（Strict Source Routing），则数据包的地址将写入数据包选项的地址列表中。如果数据包不是分片，且存在互联网时间戳（Internet Timestamp）或路由记录（Record Route），则所需数据被插入相应的列表中。如果数据包是分片且存在这两个选项之一，则这些选项将被替换为无操作（No Operation）。

### `ip_options_echo()`

`ip_options_echo()` 例程获取接收到的 IP 数据包的选项，并使用它们来创建一个回显包（即对入站消息进行回复）。此函数通常用于在接收带有 IP 选项的数据包时发送回复——例如，插入严格路由选项。这里传递的参数是 socket 缓冲区和目的选项。

### `ip_options_fragment()`

此函数获取作为 socket 缓冲区传递的分片，并用无操作（No Operation）选项覆盖所有数据包选项，且不设置复制（Copy）标志。如第 14.3.1 节所述，该标志在互联网时间戳和路由记录选项中被设置。用无操作替换的好处是协议头的长度不会改变。

### `ip_options_compile()`

此函数编译 IP 头末尾的选项字段。`ip_options_build()` 使用预先准备好的数据包选项数据结构，而 `ip_options_compile()` 必须编译所有选项。此函数通过选项处理，直到到达选项列表结束（End-of-Option List）或协议头结束。列表中的任何无操作都会被跳过。如果在此过程中发生错误，将向发送者返回 ICMP 消息。

### `ip_options_undo()`
