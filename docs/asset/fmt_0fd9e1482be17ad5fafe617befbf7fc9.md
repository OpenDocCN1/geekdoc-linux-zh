
它将 `ipv4` 地址编码在以 `2002` 开头的 `ipv6` 地址中。例如，`192.168.1.42/24` 将被编码为：

## ipv6 简介

```
2002:c0a8:12a1::1::
```

你可以使用该命令将任何 `ipv4` 地址转换为此范围。

```bash
paul@ubi1010:~$ printf "2002:%02x:%02x:%02x:%04x:%1\n" echo 192.168.1.42/24 | tr tr /:/:'
2002:c0a8:012a:0018::1
```

## 21.9. ISP

如果你足够幸运从 ISP 获取了一个 `ipv6` 地址，那么它将以 `2001` 开头。

## 21.10. 不可路由地址

类似于 DNS 中的 `example.com`，`ipv6` 地址被预留用于示例，且在互联网上是不可路由的。

```
ffff::32
2001:db8::32
```

## 21.11. ping6

使用 `ping6` 测试 `ipv6` 主机之间的连接性。你需要指定接口（对于“随机”生成的地址没有路由表）。

```bash
[root@fedora4]# ping6 -I eth0 fe80::a00:27ff:fec:(fe80::a00:27ff:fec) from fe80::a00:27ff:3c:4346 eth0: 56
64 bytes from fe80::a00:27ff:fec icmp_seq=1 ttl=64 time=0.58 ms
64 bytes from fe80::a00:27ff:fec icmp_seq=2 ttl=64 time=3.95 ms
64 bytes from fe80::a00:27ff:fec icmp_seq=3 ttl=64 time=1.53 ms
```

以下多播接收了来自网络上三个 `ipv6` 主机的回复。

```bash
[root@fedora4]# ping6 -I eth0 ff02::1
ff02::1 (ff02::1) from fe80::a00:27ff:fec:4346 eth0: 56
64 bytes from fe80::a00:27ff:fec icmp_seq=1 ttl=64 time=0.59 ms
64 bytes from fe80::a00:27ff:fec icmp_seq=2 ttl=64 time=1.87 ms (DUP!)
64 bytes from fe80::a00:27ff:fec icmp_seq=3 ttl=64 time=1.53 ms (DUP!)
64 bytes from fe80::e87b:9dd:ffec2 icmp_seq=1 ttl=64 time=5.35 ms (DUP!)
64 bytes from fe80::a00:27ff:fec:3c:4346 icmp_seq=2 ttl=64 time=0.106 ms
64 bytes from fe80::e87b:9dd:ffec2 icmp_seq=2 ttl=64 time=1.79 ms (DUP!)
64 bytes from fe80::a00:27ff:fec icmp_seq=2 ttl=64 time=2.48 ms (DUP!)
```

## 21.12. 比利与 ipv6

关于比利 `ipv6` 的大量信息可以在 `www.ipv6council.be` 找到。

像 `ipv6.belgium.be`、`www.bipt.be` 和 `www.bricozone.be` 等网站已启用 `ipv6`。一些大学也是如此：`up.ac.be` (那穆) 和 `ulg.ac.be` (列日)。

## 21.13. 其他网站

测试 `ipv6` 的其他有用网站有：

```
test-ipv6.com
ipv6-test.com
```

访问 `ipv6-test.com` 网站将测试你是否有一个有效的 `ipv6` 地址。

![](img/1d499a6177836f6f088a9e2a53e11a14_247_0.png)

访问 `test-ipv6.com` 网站也将测试你是否有一个有效的 `ipv6` 地址。

## 测试你的 IPv6 连接性。

你在公网上的 `IPv4` 地址

世界 `IPv6` 日是 2011 年 6 月 8 日，即 `IPv6` 协议出版的周年。

恭喜！你似乎同时拥有 `ipv4` 和 `ipv6` 互联网连接。如果发布者发布了 `ipv6` 版本，你的浏览器将回退到 `IPv4`。如果你在选择时优选 `ipv6` 而非 `ipv4`，这在未来可能会影响猜测你位置网站的准确性。

你似乎正在使用 `IPv6` 网关；你的路由器可能正在自动完成。这种方法可能存在局限性。最好从你的 ISP 获取原生 `ipv6` 地址。

你的 `ipv6` 服务器（由你的 ISP 提供）似乎无法访问 `ipv6` 互联网，或者没有配置使用它。这在未来可能会限制你访问仅限 `ipv6` 的网站。

- 为了你的 `ipv4` 稳定性和就绪，当发布者提供 `ipv4` 和 `ipv6` 时
- 为了你的 `ipv6` 稳定性和就绪，当发布者强制仅使用 `ipv6` 时

## 21.14. cto4 网关

如果你使用 `sixxs.net` (具体为 `http://www.sixxs.net/tools/`) 作为网关，则仅 `ipv4` 可用。

例如使用 `http://www.dashdot.sixxs.org/`

## 21.15. ping 和 dns

以下来自 `cto4` 的 `ping` 记录。

| 源 | 目的 | 协议 | way |
| :--- | :--- | :--- | :--- |
| | | | |
| `81.105.101.125` | `199.130.111.4` | `DNS` | 标准查询 `ipv6-test.com` |
| `199.130.131.4` | `81.105.101.125` | `DNS` | 标准查询 `AAAA` `2001:41d0:67d1:7e57:1` |
| `2002:55a:657d1` | `2001:41d0:67d1:7e57:1` | `TCP` | `Echo` `request` |
| `2001:41d0:67d1:7e57:1` | `2022:55a:657d1` | `TCP` | `Echo` `reply` |

## 21.16. ipv6 和 tcp/http

以下通过 `ipv6` 的握手连接记录。

| 源 | 目的 | 协议 | 信息 |
| :--- | :--- | :--- | :--- |
| | | | |
| `2002:55a:657d1` | `2001:41d0:67d1:7e57:1` | `TCP` | `[SYN]` `Seq=0` `Win=5648` |
| `2001:41d0:67d1:7e57:1` | `2002:55a:657d1` | `TCP` | `[ACK]` `Seq=1` `Ack=5648` |
| `2002:55a:657d1` | `2001:41d0:67d1:7e57:1` | `TCP` | `GET` `/index.html` |
| `2001:41d0:67d1:7e57:1` | `2002:55a:657d1` | `TCP` | `[ACK]` `Seq=1` `Ack=708` |

## 21.17. ipv6 PTR 记录

如 DNS 章节所示，`ipv6` `PTR` 记录位于 `ipv6.net`，并生成域名。

```
> Frame 64 bytes on 132 bytes) Ethernet, Src:2002:55a:657d1;Dst:00:26:b0:5d:22;Dst:cf:6a:10 (00:b0:6a:10) Protocol, Src:181.105.101.125 (81.105.101.125), Dst:195.130.131.4 (195.130.131.4) Dataagram Protocol, Src Port:34361 (34361), Dst Port:53 (domain) Domain Name System (query) [Response: no answer]
   Transaction ID: 0xfec3
   Flags: 0x8100 (Standard query)
   Questions: 1
   Answers: 0
   Authority RR: 0
   Additional RR: 0
   Query > 10.0.0.5.7.e.7.0.0.1.6.7.2.0.0.0.1.4.0.0.ip6.arpa: type: ptr, CLASS IN
```

## 21.18. Linux cto4 配置

以下是 Linux 上 `cto4` 配置的记录。

感谢 `http://www.anynode.cz/v6linux6to4` 和 `https://mirrors.bieringer.de/Linux+IPv6-HOWTO/`; 以及 `tldp`。

```bash
root@mac:~# ifconfig
eth0 link enc:Ethernet Waddr 00:26:b0:5d:22:5e
      inet addr:81.105.101.125 Bcast:255.255.255.255 Mask:255.255.255.248
```
