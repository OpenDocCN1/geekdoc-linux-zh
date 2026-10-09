
该区域列出了另外两台机器的地址和邮件交换记录：`rabbit.mytrek.com` 和 `lizard.mytrek.com`。你可以为这些条目添加 `HINFO`、`TXT`、`MINFO` 或别名记录。

## IPv6 区域文件示例

这是使用 IPv6 地址的相同区域文件。地址是唯一本地（FC00），而不是全局（3），提供了私有网络地址。环回设备由 IPv6 地址 `::1` 表示。使用了 `AAAA` IPv6 地址记录。

```
; turtle.mytrek.com 的权威数据，IPv6 版本
; TTL 1d
@ IN SOA turtle.mytrek.com. hostmaster.turtle.mytrek.com. (
93071200 ; 序列号
10800 ; Refresh 3 小时
3600 ; Retry 1 小时
3600000 ; Expire 1000 小时
86400 ) ; Minimum 24 小时
```

```
IN NS turtle.mytrek.com.
IN AAAA FC00:8:800:202:C17A
IN MX 10 turtle.mytrek.com.
IN MX 15 rabbit.mytrek.com.
```

```
turtle IN AAAA FC00:8:800:202:C17A
gopher IN INFO PC-686 LINUX
ftp IN CNAME turtle.mytrek.com.
www IN AAAA turtle.mytrek.com.
FC00:8:800:202:C17A
```

```
rabbit IN AAAA FC00:FEDC:BA98:7654:3210
lizard IN AAAA FC00:EE18:F7:3466:7D
IN HINFO MAC_OS
```

## 反向映射文件

反向映射查询通过反向映射文件启用。反向映射文件将完全限定域名完全转换为 IP 地址。这种反向查询能力并非必须的，但拥有它非常方便。通过反向映射，当用户访问远程主机时，可以使用他们的域名地址来识别他们自己的主机，而不是 IP 地址。文件名可以是任何名称。在大多数当前的发行版中，它是区域的域名地址（区域的网络部分）。IP 地址为 `192.168.0.1` 的区域的反向映射文件是 `1.0.168.192`。其路径类似于 `/var/named/168.0.db`。在某些旧版 BIND 实现的系统上，反向映射可能由区域根加上 `.rev` 扩展组成。例如，如果区域名为 `mytrek.com`，则反向映射文件将名为 `mytrek.rev`。

## IPv4 in-addr.arpa 反向映射

在 IPv4 中，`named.conf` 中反向映射的区域条目使用特殊名称，由反向 IP 地址加上 `in-addr.arpa` 组成。该 IP 地址成为反向映射文件中 `@` 所引用的域名。例如，IP 地址为 `192.168.43` 的域名的反向区域名称为 `43.168.192.in-addr.arpa`。在接下来的示例中，地址 `192.168.0` 的反向域名是 `0.168.192.in-addr.arpa`。

```
zone "168.192.in-addr.arpa" {
  type master;
  file "192.168.0.db";
};
```

反向映射文件以 SOA 记录开头，这与正向文件中相同。随后是正向文件中定义的每台机器的资源记录。这些资源记录是 PTR 记录，指向区域内的主机。这些必须是实际主机，而不是由 CNAME 记录定义的别名。反向映射记录以反转的 IP 地址开始。IP 地址中的每个段都按顺序反转。每个段以主机 ID 开头，随后是反转的数字。

```
; 域 1.168.192.in-addr.arpa 的反向映射
; TTL 86400
@ IN SOA turtle.mytrek.com. (
  92050300 ; 序列 (yyymmdd 格式)
  10800 ; Refresh 3 小时
  3600 ; Retry 1 小时
  3600000 ; Expire 1000 小时
  86400 ) Minimum 24 小时

@ IN NS turtle.mytrek.com.
1 IN PTR turtle.mytrek.com.
2.168.192 IN PTR rabbit.mytrek.com.
3 IN PTR lizard.mytrek.com.
```

如果你只列出主机 ID 而没有末尾点号，则会自动附加区域域名。在反向映射文件中，区域语句中指定的区域域名是括号中的 IP 地址。对于 IP 地址为 `192.168.0.1` 的区域，反向映射文件是 `1.0.168.192`。`turtle.mytrek.com`、`lizard.mytrek.com` 和 `rabbit.mytrek.com` 都是反向映射别名。在下面的示例中，地址 `192.168.0` 的反向域名是 `0.168.192.in-addr.arpa`。用户输入这些 URL 将自动访问 `turtle.mytrek.com` 机器上的相应服务器。

## IPv6 ARPA 反向格式

使用 IPv6 的格式。

```
FC00:0000:0000:00E0:18F7:3466:007D lizard
FC0000000000000000000000000000666660
```

```
zone "FC00:8:800:202:C17A"
```

```
 "....pa";
};
```

反向映射文件使用使用格式的格式级格式。

```
$TTL 1d

@ IN SOA turtle.mytrek.com. hostmaster.turtle.mytrek.com. (

    92050300 ; Serial (yyymmdd 格式)
    10800 ; Refresh 3 小时
    3600 ; Retry 1 小时
    3600000 ; Expire 1000 小时
    86400 ) Minimum 24 小时
```

```
@
[FC00:8:800:202:C17A/64] IN NS turtle.mytrek.com.
[FEDCBA9876543210/64] IN PTR rabbit.mytrek.com.
[00E018F73466007D/64] IN PTR lizard.mytrek.com.
```

## IPv6.INT 反向映射格式

旧的 `IPv6.INT` 格式对 IPv6 地址使用半字节格式。这后来已被 `IPv6.ARPA` 格式取代。十六进制地址被分割每个十六进制数，用点号分隔并反向写入。这为你提供了 32 个反转的十六进制数。`lizard` 地址的 `IPv6.INT` 版本如下：

```
FC00:0000:0000:00E0:18F7:3466:007D lizard
0.0.0.0.0.0.0.0.0.0.00.c.e.f lizard 网络地址
```

在 `named.conf` 文件中带有 `IP6.INT` 扩展的反向映射区域条目将使用网络地址的反向映射。

```
zone "0.0.0.0.0.0.0.0.0.0.0.0.c.e.f.IP6.INT" in (
    type master;
    file "fec.ip6.int";
);
```

反向区域文件则对每个接口地址使用反转的半字节格式。

## 第 30 章：域名系统

```
$TTL 1d
@ IN SOA turtle.mytrek.com. hostmaster.turtle.mytrek.com.
    92050300 ; Serial (ymymddxx format)
    10800 ; Refresh 3Hours
    3600 ; Retry 1 hour
    360000 ; Expire 1000 hours
    86400 ; Minimum 24 hours
$ORIGIN 0.0.0.0.0.0.0.0.0.0.c.e.f IN NS turtle.mytrek.com.
A.7.1.4.C.0.0.2.0.0.2.0.8.0.0.0 IN PTR turtle.mytrek.com.
0.1.2.3.4.5.6.7.8.9.A.B.C.D.E.F IN PTR rabbit.mytrek.com.
D.7.0.0.6.6.4.3.7.F.1.0.E.0.0 IN PTR lizard.mytrek.com.
```

# RFC 1912 私有地址管理：localhost

在 Fedora 上，地址空间（包括 localhost）的区域由 RFC 1912 配置文件处理，该文件命名为 `named.rfc1912.zones`。此文件由 `named.conf` 文件直接读取，并作为 BIND 配置的一部分包含，包括 `localhost.localdomain` 以及用于 IPv4 和 IPv6 服务的 localhost 反向映射区域。

# Localhost 区域文件：named.localhost

`named.localhost` 区域实现了名为 localhost 的本地回环接口的映射。该文件同时支持 IPv4 和 IPv6 寻。localhost 的 IPv4 地址是 `127.0.0.1`，IPv6 地址是 `::1`。这些是作为你机器本地地址的特殊地址。它允许机器进行自我寻。

IPv4 地址的类型为 A，地址为 `127.0.0.1`，而 IPv6 地址的类型为 AAAA `::1`。

```
A       127.0.0.1
AAAA      ::1
```

这里显示了 `named.localhost` 区域文件。

named.localhost

```
$TTL 1D
@ IN SOA @ rname.invalid. (
    0 ; serial
    1D ; refresh
    1H ; retry
    1W ; expire
    3H ) ; minimum
```

```
NS      @
A       127.0.0.1
AAAA    ::1
```

# named.rfc1912.zones

```
// named.rfc1912.zones:
//
// 由 Red Hat caching-nameserver 软件包提供
// ISC BIND 区域配置，用于 RFC
// 1912 第 4.1 节推荐的区域：localhost TLDs 和地址区域
// 详见 http://www.ietf.org/internet-drafts/draft-ietf-dnsop-default-local-zones-
02.txt
// ((c)2007 R W Franks
//
// 请参考 /usr/share/doc/bind*/sample/get示例 named 配置文件。
//
```

```
zone "localhost.localdomain" IN {
  type master;
  file "named.localhost";
  allow-update ( none );
};
```

```
zone "localhost" IN {
  type master;
  file "named.localhost"
  allow-update ( none );
};
```

```
zone "0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa"
IN IN {
  type master;
  file "named.loopback"
  allow-update ( none );
};
```

```
zone "1.0.0.127.in-addr.arpa" IN {
  type master;
  file "named.loopback"
  allow-update ( none );
};
```

```
zone "0.in-addr.arpa" IN {
  type master;
  file "named.empty"
  allow-update ( none );
};
```

# Localhost 反向映射：named.loopback

localhost 反向映射文件实现了名为 localhost 的本地回环接口的反向映射。该文件命名为 `named.loopback`。它被 IPv4 和 IPv6 映射区域引用。

在该文件的 IPv4 区域语句中，区域名称为 `0.0.127.in-addr.arpa`。IP 地址的域名部分反序输入，并附加 `in-addr.arpa`，即 `0.0.127.in-addr.arpa`。这里显示了 `named.rfc1912.zones` 的条目：

```
zone "0.0.127.in-addr.arpa" {
  type master;
  file "named.loopback";
  allow-update { none };
};
```

对于 IPv6 区域语句，Fedora 的实现使用了半字节格式（nibble format）处理反向地址：`0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa`。这里显示了 IPv6 区域语句：

```
zone "0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa" IN {
  type master;
  file "named.loopback";
  allow-update { none };
}
```

`named.loopback` 区域同时支持 IPv4 和 IPv6 地址。NS 记录指定了应该使用的名称服务器。该文件有一个 PTR 记录，将 IP 地址映射到 localhost。这里显示了 `named.localhost` 文件的内容：

```
$TTL 1D
IN SOA @ rname.invalid. (
    0 ; serial
    1D ; refresh
    1H ; retry
    1W ; expire
    3H ) ; minimum
  NS @
```
