

FE C0:0000:0000:0000:00E0:18F7:3466:007D      lizard IPv6 地址 \[xFEC0000000000000/64]                     lizard 网络地址 \[x00E018F73466007D/64]                     lizard 接口地址

在 named.conf 文件中带有 IP6.ARPA 扩展的反向映射区域条目将使用网络地址的位级表示。

```
zone "\[x fec0000000000000/64].IP6.ARPA" in {
    type master;
    file "fec.ip6.arpa";
};
```

反向映射文件随后对接口地址使用相同的位级格式。

```
@ IN SOA turtle.mytrek.com. hostmaster.turtle.mytrek.com. (
    92050300 ; Serial (yymmddxx format)
    10800   ; Refresh 3Hours
    3600    ; Retry 1 hour
    3600000 ; Expire 1000 hours
    86400 ) ; Minimum 24 hours
```

```
[x000808002000C417A/64] IN PTR turtle.mytrek.com.
[\xFEC0DA9876543210/64] IN PTR rabbit.mytrek.com.
[\x00E018F73466007D/64] IN PTR lizard.mytrek.com.
```

## IPv6 IP6.INT 反向映射格式

较旧的 IP6.INT 格式对 IPv6 地址使用半字节格式。十六进制地址被分割为每个十六进制数字，以句点分隔并反向书写。这给你 32 个反向顺序的十六进制数字。lizard 地址的 IP6.INT 版本如下所示。

FEC0:0000:0000:0000:00E0:18F7:3466:007D      lizard IPv6 地址
0.0.0.0.0.0.0.0.0.0.0.0.0.0.c.e.f          lizard 网络地址
D.7.0.0.6.6.4.3.7.F.8.1.0.0.E.0            lizard 接口地址

在 named.conf 文件中带有 IP6.INT 扩展的反向映射区域条目将使用网络地址的反向半字节格式。

```
zone "0.0.0.0.0.0.0.0.0.0.0.0.0.0.c.e.f.IP6.INT" in {
    type master;
    file "fec.ip6.int";
};
```

反向区域文件随后对每个接口地址使用反向半字节格式。

```
@ IN SOA turtle.mytrek.com. hostmaster.turtle.mytrek.com. (
    92050300 ; Serial (yymmddxx format)
    10800   ; Refresh 3Hours
    3600    ; Retry 1 hour
    3600000 ; Expire 1000 hours
```

```
$ORIGIN 0.0.0.0.0.0.0.0.0.0.0.0.0.0.c.e.f IN NS turtle.mytrek.com.
A.7.1.4.C.0.0.2.0.0.8.0.8.0.0.0 IN PTR turtle.mytrek.com.
0.1.2.3.4.5.6.7.8.9.A.B.C.D.E.F IN PTR rabbit.mytrek.com.
D.7.0.0.6.6.4.3.7.F.8.1.0.0.0 IN PTR lizard.mytrek.com.
```

## Localhost 反向映射

localhost 反向映射文件实现了对本地回环接口的反向映射，该接口称为 localhost，其网络地址为 127.0.0.1。此文件可以是任何名称。在大多数系统上，localhost 被命名为 named.local。在其他系统上，localhost 可能使用 IP 地址的网络部分 127.0.0。此文件允许将域名 localhost 映射到 localhost IP 地址，该地址在每台机器上始终为 127.0.0.1。地址 127.0.0.1 是一个特殊地址，可用作机器的本地地址。它允许机器寻址自身。在此文件的区域语句中，区域的名称为 0.0.127.IN-ADDR.ARPA。IP 地址的域名部分以反向顺序输入，并附加 IN-ADDR.ARPA，0.0.127.IN-ADDR.ARPA。named.conf 条目如下所示：

```
zone "0.0.127.IN-ADDR.ARPA" {
    type master;
    file "named.local";
};
```

用于 localhost 反向映射文件的名称通常为 named.local，尽管它可以是任何名称。NS 记录指定 localhost 应使用的名称服务器。此文件具有 PTR 记录，可将 IP 地址映射到 localhost。用作名称的 1 会扩展为附加区域域名——在这种情况下，给出 1.0.0.127，一个反向 IP 地址。named.local 文件的内容如下所示。请注意 localhost 的尾随句点：

```
@ IN SOA localhost. root.localhost. (
    1997022700 ; Serial
    28800 ; Refresh
    14400 ; Retry
    3600000 ; Expire
    86400 ) ; Minimum

    IN NS turtle.mytrek.com.
1 IN PTR localhost.
```

在 IPv6 中，本地主机反向映射使用 IPv6 localhost 地址的反向指定。此地址由 31 个零和一个 1 组成，可以简写为 ::1，其中 :: 表示 31 个零的序列。使用 IPv6 IP6.ARPA 格式，这些可以用位级格式书写，其中前 64 位由全零的网络地址组成，而接口地址的值为 1。

```
0000:0000:0000:0000:0000:0000:0000:0001 localhost IPv6 地址
\[x0000000000000000000000000001/128] localhost 地址
```

