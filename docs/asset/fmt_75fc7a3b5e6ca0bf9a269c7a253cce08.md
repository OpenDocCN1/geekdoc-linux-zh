
### `netstat -ni` 接口统计

```bash
freebsd % netstat -ni
| Name | Mtu | Network Address | Ipkts | Ierrs | Opks | Oerr |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| hme0 | 1500 | <Link#1> | 08:00:20:a7:68:6b | 29100435 | 35 | 4651648 |
| hme0 | 1500 | 12.106.32/24 | 12.106.32.254 | 28746630 | - | 46617260 |
| hme0 | 1500 | fe80:1::a200:2ff:fea7:68b/64 | | | | |
| fe80:1::a200:2ff:fea7:68b | | | | | - | 0 |
| hme0 | 1500 | 3ffe:b80:1f8d:1::/64 | 0 | - | | | |
| 3ffe:b80:1f8d:1::1 | | | | | - | 0 |
| hmel1 | 1500 | <Link#2> | 08:00:20:a7:68:6b | 51092 | 0 | 31537 |
| hmel1 | 1500 | fe80:2::a200:2ff:fea7:68b/64 | | | | |
| fe80:2::a200:2ff:fea7:68b | | | | | - | 90 |
| hmel1 | 1500 | 192.168.42 | 192.168.42.1 | 43584 | - | 24173 |
| hmel1 | 1500 | 3ffe:b80:1f8d:2::/64 | 78 | - | | | |
| 3ffe:b80:1f8d:2::1 | | | | | | | | |
| lo0 | 16384 | <Link#6> | 10198 | 0 | 10198 | | | | |
| lo0 | 16384 | ::1/128 | 10 | - | 10 | | | | |
| lo0 | 16384 | fe80:6::1/64 | fe80:6::1 | 0 | - | 0 | | |
| lo0 | 16384 | 127 | 127.0.1 | 10167 | 10167 | | | |
| gif0 | 1280 | <Link#> | 6 | - | 5 | | | |
| gif0 | 1280 | 3ffe:b80:1f8d:3:ad1::2/128 | | | | | |
| 3ffe:b80:1f8d:3:ad1::2 | | | | | - | 0 | | |
| gif0 | 1280 | fe80::a200:2ff:fea7:68b/64 | | | | | | |
| fe80::a200:2ff:fea7:68b | | | | | - | 0 | | |
```

2. `netstat -r` 显示路由表，这是另一种确定接口的方法。`-n` 标志打印数字地址。这也显示了网关的 IP 地址。

```bash
freead % netstat -nr
```

路由表

Internet:

| Destination | Gateway | Flags | Reps | Exp |
| :--- | :--- | :--- | :--- | :--- |
| default | 12.106.32.1 | UGSC | 10 | 6877 |
| 12.106.32/24 | link#1 | UC | 3 | hme0 |
| 12.106.32/31 | 00:b8:e9:22:c0:00 | UHLW | 9 | hme0 1 |
| 12.106.32.253 | 08:00:b7:e7:00 | UHLW | 0 | hme0 |
| 12.106.32.254 | 08:00:a7:e6:b8 | UHLW | 0 | lo0 |
| 127.0.0.1 | 127.0.0.1 | UH | 1 | 10167 | lo0 |
| 192.168.42 | link#2 | UC | 2 | hme0 |
| 192.168.42.1 | 08:00:a7:68:b6 | UHLW | 0 | 11 | lo0 |

Internet6:

| Destination | Gateway | Flags |
| :--- | :--- | :--- |
| ::9 | :: | UGSC |
| default | ::1 | UH |
| ::1 | ::1 | UH |
| :ffff:0.0.0/9 | ::1 | UGSC |
| 3ffe:b80:3:9ad1::1 | 3ffe:b80:3:9ad1::1 | UH |
| 3ffe:b80:3:9ad1::2 | link# | UHLW |
| 3ffe:b80:1f8d::40 | | US |
| 3ffe:b80:1f8d::64 | link#1 | UC |
| 3ffe:b80:1f8d::1 | 08:00:20:a7:68:b6 | UHLW |
| 3ffe:b80:1f8d::64 | link#2 | UC |
| 3ffe:b80:1f8d::1 | 08:00:20:a7:68:b6 | UC |
| 3ffe:b80:1f8d::2 | 00:04:ac:17:bf:38 | UHLW |
| fe80::/10 | | UGSC |
| fe80::%64 | link#1 | UC |
| fe80::a000:22:fea768b%hme0 | | UHL |
| fe80::%64 | link#2 | UC |
| fe80::a000:22:fea768b%hme0 | 08:00:20:a7:68:b6 | UC |
| fe80::lo0/64 | lo0 | UHL |
| fe80::100 | link#6 | UHL |
| fe80::%gif/60 | link#8 | UC |
| fe80::a000:22:fea768b%gif0 | link#8 | UC |
| ff02::/32 | ::1 | UG |
| ff02::/16 | ::1 | UC |
| ff02::%hme/32 | link#1 | UC |
| ff02::%hme1/32 | link#2 | UC |
| ff02::%lo0/32 | ::1 | UC |
| ff02::%gif/32 | link#8 | UC |
```

3. 给接口名称，我们执行 `ifconfig` 获取每个接口的细节。

```bash
linux % ifconfig eth0
eth0 encap:Ethernet HWaddr 00:C0:9F:06:B0:E1
inet 206.168.112.96 Bcast:206.168.112.127 Mask:255.255.255.0 BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:4921439  bytes:109806974 (104.7 Mb)
TX packets:4054399  bytes:336054672 (320.8 Mb)
```

显示了 IP 地址、子网掩码和广播地址。`MULTICAST` 标志表示主机支持多播。某些实现在所有配置的接口上提供 `-a` 标志。

4. 本地网络上许多主机 IP 地址的一种方法是 ping 上一步找到的广播地址。

```bash
linux % -b 206.168.112.127 address
WARNING: pinging broadcast 206.168.112.127 (206.168.112.127) : 56(84) bytes
64 bytes from 206.168.112.40: icmp_seq=0 ttl=255 time=2.566 msec (DUP!)
64 bytes from 206.168.112.14: icmp_seq=0 ttl=255 time=3.089 msec (DUP!)
64 bytes from 206.168.112.118: icmp_seq=0 ttl=255 time=2.973 msec (DUP!)
64 bytes from 206.168.112.71: icmp_seq=0 ttl=255 time=3.311 msec (DUP!)
64 bytes from 206.168.112.126: icmp_seq=0 ttl=255 time=3.200 msec (DUP!)
64 bytes from 206.168.112.71: icmp_seq=0 ttl=255 time=3.311 msec (DUP!)
64 bytes from 206.168.112.31: icmp_seq=0 ttl=64 time=3.641 msec (DUP!)
```
