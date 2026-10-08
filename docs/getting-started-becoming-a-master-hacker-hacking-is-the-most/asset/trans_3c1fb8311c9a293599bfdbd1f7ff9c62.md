
扫描，但其通用性使其成为主动侦察工具箱中一个有价值的工具。

## Hping3 帮助

让我们从获取 hping3 的帮助屏幕开始。我们可以通过输入 `kali > hping3 -h` 来实现。当我们这样做时，hping3 会返回一个长长的选项和开关列表。由于篇幅较长，我将其分成了两个截图。

如您在上方截图中所见，hping3 拥有众多开关选项，而这仅仅是其中的一小部分。我想让您在此注意以下几个：

- -c count：指定包的数量
- -i wait：等待 X 秒
- -flood：用数据包淹没目标

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_210_0.png)

- -q：安静模式
- -a：欺骗 IP 地址
- -rand-source：发送带有随机源 IP 地址的数据包
- -f：对数据包进行分片
- -x：在 IP 头部设置更多分片标志
- -y：在 IP 头部设置不分片标志

请注意，hping3 的默认模式是 TCP 数据包。这与 nmap 不同，nmap 默认发送 ICMP ping，而这些 ping 经常被防火墙和网关阻止。

上述截图向我们展示了更多的选项。我想吸引您对以下选项的注意：

- -p：指定目标端口
- -Q：获取 TCP 序列号
- -tcp-timestamp：获取 TCP 时间戳并将其转换为天、小时和分钟。

另外请注意，我们可以设置任何 TCP 标志（S、A、F、P、R、U），以及 XMAS（-X）扫描（设置 P、U、F 标志）。

```
root@kali-2019:~# hping3 -S 192.168.0.114 -p 80
Hping 192.168.0.114 (eth0 192.168.0.114): S set, 40 headers + 0 data bytes
len=46 ip=192.168.0.114 ttl=128 DF id=1857 sport=80 flags=RA seq=0 win=0 rtt=6.8 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1858 sport=80 flags=RA seq=1 win=0 rtt=5.9 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1859 sport=80 flags=RA seq=2 win=0 rtt=4.9 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1860 sport=80 flags=RA seq=3 win=0 rtt=3.2 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1861 sport=80 flags=RA seq=4 win=0 rtt=3.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1862 sport=80 flags=RA seq=5 win=0 rtt=2.9 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1863 sport=80 flags=RA seq=6 win=0 rtt=2.2 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1864 sport=80 flags=RA seq=7 win=0 rtt=2.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1865 sport=80 flags=RA seq=8 win=0 rtt=1.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1866 sport=80 flags=RA seq=9 win=0 rtt=9.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1867 sport=80 flags=RA seq=10 win=0 rtt=7.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1868 sport=80 flags=RA seq=11 win=0 rtt=7.7 ms
```

```
root@kali-2019:~# hping3 -S 192.168.0.114 -p 445
Hping 192.168.0.114 (eth0 192.168.0.114): S set, 40 headers + 0 data bytes
len=46 ip=192.168.0.114 ttl=128 DF id=1874 sport=445 flags=SA seq=0 win=8192 rtt=8.7 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1874 sport=445 flags=SA seq=1 win=8192 rtt=7.8 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1875 sport=445 flags=SA seq=2 win=8192 rtt=6.7 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1876 sport=445 flags=SA seq=3 win=8192 rtt=6.0 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1877 sport=445 flags=SA seq=4 win=8192 rtt=5.2 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1878 sport=445 flags=SA seq=5 win=8192 rtt=4.9 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1879 sport=445 flags=SA seq=6 win=8192 rtt=4.8 ms
```

## 使用 Hping3 默认模式进行端口扫描

在最基本的层面上，hping3 是一个类似于 nmap 的端口扫描器。语法相似，但输出不同。与 nmap 不同，hping3 不会返回汇总的输出，而是返回响应数据包的详细规范。让我们看看当我们尝试对 Windows 7 系统的 80 端口进行 hping3 扫描时会发生什么。这里，让我们使用 SYN（-S）标志。此扫描类似于 `nmap -sS <IP> -p 80` 扫描。

```
kali > hping3 -S 192.168.1.116 -p 80
```

使用 Ctrl+C 终止 hping3。

如您在上方的第六列所见，标志字段返回 RA。这表明 RST 和 ACK 标志已被设置。返回 RST 标志是 TCP 通信端口已关闭的标准方式。在这个 Windows 7 系统上，我们可以得出结论：端口 80 是关闭的。虽然不寻常，但也并非闻所未闻。

既然这是一台 Windows 机器，它可能启用了 SMB 或端口 445。让我们尝试该端口。

```
kali > hping3 -S 192.168.1.116 -p 445
```

如您在上方的截图中所见，当我们扫描此系统的 445 端口时，它返回了一个设置了 SA 标志（SYN (S) 和 ACK (A)）的数据包，表明它是开放的。

最后，如果我们想扫描所有端口，我们可以使用递增语法 `++1`，形成如下命令：

```
kali > hping3 -S 192.168.1.116 -p ++1
```

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_213_0.png)

此扫描从端口 1 开始，并以 1 为步长（`++1`）递增，以测试每个端口的响应。

```
root@kali-2019:~ # hping3 -S 192.168.0.114 -p ++1
HPING 192.168.0.114 (eth0 192.168.0.114): S set, 40 headers + 0 data bytes
len=46 ip=192.168.0.114 ttl=128 DF id=1883 sport=1  flags=RA seq=0 win=0 rtt=4.4 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1884 sport=2  flags=RA seq=1 win=0 rtt=4.8 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1885 sport=3  flags=RA seq=2 win=0 rtt=4.0 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1886 sport=4  flags=RA seq=5 win=0 rtt=4.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1887 sport=5  flags=RA seq=4 win=0 rtt=3.0 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1888 sport=6  flags=RA seq=5 win=0 rtt=2.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1889 sport=7  flags=RA seq=7 win=0 rtt=1.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1890 sport=8  flags=RA seq=7 win=0 rtt=9.4 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1891 sport=9  flags=RA seq=8 win=0 rtt=7.6 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1892 sport=10 flags=RA seq=9 win=0 rtt=6.7 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1893 sport=11 flags=RA seq=10 win=0 rtt=6.9 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1894 sport=12 flags=RA seq=11 win=0 rtt=6.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1895 sport=13 flags=RA seq=12 win=0 rtt=5.9 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1896 sport=14 flags=RA seq=13 win=0 rtt=5.9 ms
```

```
root@kali:~$ hping3 -S -f 192.168.1.116 -p 445
HPING 192.168.1.116 (eth0 192.168.1.116): S set, 40 headers + 0 data bytes
len=46 ip=192.168.1.116 ttl=128 DF id=18306 sport=445 flags=SA seq=0 win=8192 rtt=1.8 ms
len=46 ip=192.168.1.116 ttl=128 DF id=18307 sport=445 flags=SA seq=1 win=8192 rtt=1.5 ms
len=46 ip=192.168.1.116 ttl=128 DF id=18308 sport=445 flags=SA seq=2 win=8192 rtt=1.3 ms
len=46 ip=192.168.1.116 ttl=128 DF id=18309 sport=445 flags=SA seq=3 win=8192 rtt=1.1 ms
len=46 ip=192.168.1.116 ttl=128 DF id=18310 sport=445 flags=SA seq=4 win=8192 rtt=1.4 ms
len=46 ip=192.168.1.116 ttl=128 DF id=18311 sport=445 flags=SA seq=5 win=8192 rtt=1.8 ms
len=46 ip=192.168.1.116 ttl=128 DF id=18312 sport=445 flags=SA seq=6 win=8192 rtt=6.5 ms
```

请注意第五列，它从扫描端口 1 开始，然后是端口 2，接着是端口 3……它将继续扫描所有 65535 个端口，直到结束或您按下 Ctrl+C。

### 分片数据包

正如我在 hping3 的介绍中提到的，有时您可以通过分片数据包来绕过 IDS 和防火墙等安全设备。我们可以使用 hping3 的 `-f` 开关来实现这一点，例如：`kali > hping3 -S -f 192.168.1.116 -p 445`。

由于数据包被拆分为原始数据包的许多小片段，在某些情况下，IDS 或防火墙的攻击签名不会匹配这些分片数据包。

```
root@kali:-# hping3 -Q 0 google.com -p 80
HPING google.com (eth0 74.125.239.130): S set, 40 headers + 0 data bytes
229375066 +229375066
141258272 +4206850501
2288187613 +2146929341
849247683 +2856027365
1247146679 +397898996
3673440894 +2426294215
1072409767 +1693936168
2485301374 +1412891607
2770603782 +285302408
3069831418 +299227636
```

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_214_0.png)

### 预测序列号

TCP/IP 使用序列号来确保数据包

