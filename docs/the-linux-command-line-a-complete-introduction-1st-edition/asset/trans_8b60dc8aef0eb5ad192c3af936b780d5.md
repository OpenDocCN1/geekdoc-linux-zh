

```
64 bytes from vhost.sourceforge.net (66.35.250.210): icmp_seq=1 ttl=43 time=107 ms
64 bytes from vhost.sourceforge.net (66.35.250.210): icmp_seq=2 ttl=43 time=108 ms
64 bytes from vhost.sourceforge.net (66.35.250.210): icmp_seq=3 ttl=43 time=106 ms
64 bytes from vhost.sourceforge.net (66.35.250.210): icmp_seq=4 ttl=43 time=106 ms
64 bytes from vhost.sourceforge.net (66.35.250.210): icmp_seq=5 ttl=43 time=105 ms
64 bytes from vhost.sourceforge.net (66.35.250.210): icmp_seq=6 ttl=43 time=107 ms
--- linuxcommand.org ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 6010ms
rtt min/avg/max/mdev = 105.647/107.052/108.118/0.824 ms
```

在按下 CTRL-C 中断（此处是在第六个数据包之后）后，ping 会输出性能统计信息。网络运行正常时，数据包丢失率应为百分之零。ping 成功通常表明网络的各个组成部分（接口卡、线缆、路由和网关）大体处于良好的工作状态。

## traceroute——追踪网络数据包的路径

traceroute 程序（某些系统使用类似的 tracepath 程序代替）会列出网络流量从本地系统到达指定主机所经过的所有“跳点”。例如，要查看到达 http://www.slashdot.org/ 的路径，我们可以执行：

```
[me@linuxbox ~]$ traceroute slashdot.org
```

输出如下所示：

```
traceroute to slashdot.org (216.34.181.45), 30 hops max, 40 byte packets
1  ipcop.localdomain (192.168.1.1)  1.066 ms  1.366 ms  1.720 ms
2  * * *
3  ge-4-13-ur01.rockville.md.bad.comcast.net (68.87.130.9)  14.622 ms  14.885 ms  15.169 ms
4  po-30-ur02.rockville.md.bad.comcast.net (68.87.129.154)  17.634 ms  17.626 ms  17.899 ms
5  po-50-ur02.rockville.md.bad.comcast.net (68.87.129.158)  15.992 ms  15.983 ms  16.256 ms
6  po-30-ar01.howardcounty.md.bad.comcast.net (68.87.136.5)  22.835 ms  14.23 ms  14.405 ms
7  po-10-ar02.whitemarsh.md.bad.comcast.net (68.87.129.34)  16.154 ms  13.600 ms  18.867 ms
8  te-0-3-0-1-cr01.philadelphia.pa.ibone.comcast.net (68.86.90.77)  21.951 ms  21.073 ms  21.557 ms
9  pos-0-8-0-0-cr01.newyork.ny.ibone.comcast.net (68.86.85.10)  22.917 ms  21.884 ms  22.126 ms
10  204.70.144.1 (204.70.144.1)  43.110 ms  21.248 ms  21.264 ms
11  cr1-pos-0-7-3-1.newyork.savvis.net (204.70.195.93)  21.857 ms  cr2-pos-0-0-3-1.newyork.savvis.net (204.70.204.238)  19.556 ms  cr1-pos-0-7-3-1.newyork.savvis.net (204.70.195.93)  19.634 ms
12  cr1-pos-0-7-3-0.chicago.savvis.net (204.70.192.109)  41.586 ms  42.843 ms  cr2-tengig-0-0-2-0.chicago.savvis.net (204.70.196.242)  43.115 ms
13  hr2-tengigabitethernet-12-1.elkgrovech3.savvis.net (204.70.195.122)  44.215 ms  41.833 ms  45.658 ms
14  csr1-ve241.elkgrovech3.savvis.net (216.64.194.42)  46.840 ms  43.372 ms  47.041 ms
15  64.27.160.194 (64.27.160.194)  56.137 ms  55.887 ms  52.810 ms
16  slashdot.org (216.34.181.45)  42.727 ms  42.016 ms  41.437 ms
```

从输出中可以看到，从我们的测试系统连接到 http://www.slashdot.org/ 需要经过 16 个路由器。对于提供标识信息的路由器，我们会看到它们的主机名、IP 地址和性能数据，其中包括从本地系统到该路由器的三次往返时间采样。对于不提供标识信息的路由器（由于路由器配置、网络拥塞、防火墙等原因），我们会看到星号，如第二跳那一行所示。

## netstat——检查网络设置和统计信息

netstat 程序用于检查各种网络设置和统计信息。通过使用它的众多选项，我们可以查看网络配置中的各种特性。使用 `-ie` 选项，我们可以检查系统中的网络接口：

```
[me@linuxbox ~]$ netstat -ie
eth0
Link encap:Ethernet HWaddr 00:10:9b:99:67
inet addr:192.168.1.2 Bcast:192.168.1.255 Mask:255.255.255.0
inet6 addr: fe80::214:ff:fe9b:967/64 Scope:Link
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:238488 errors:0 dropped:0 overruns:0 frame:0
TX packets:403217 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:100
RX bytes:15308921 (14.6 MB) TX bytes:261035246 (248.9 MB)
Memory:fdc00000-fdfe0000

lo
Link encap:Local Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
inet6 addr: ::1/128 Scope:Host
UP LOOPBACK RUNNING MTU:16436 Metric:1
RX packets:2208 errors:0 dropped:0 overruns:0 frame:0
TX packets:2208 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0
RX bytes:111490 (108.8 KB) TX bytes:111490 (108.8 KB)
```

在上面的示例中，我们看到测试系统有两个网络接口。第一个名为 eth0，是以太网接口；第二个名为 lo，是回环接口，一种系统用来“与自己通信”的虚拟接口。

