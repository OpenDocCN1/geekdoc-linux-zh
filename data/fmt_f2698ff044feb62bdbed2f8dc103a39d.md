
# 3.4.1 在线路上传输

```
16:25.49.74720 d230-17.uregon.edu.1025 > 224.2.163.188.2384 udp 332
16:25.49.79001 hocus.cs.ucl.ac.uk > 224.1.127.255 igmp nreport 224.1.127.255 [1]
16:25.49.82979 d230-17.uregon.edu.1025 > 224.2.163.188.234 udp
16:25.49.85364 d230-17.uregon.edu.1025 > 224.2.163.188.234 udp
16:25.49.89874 d230-17.uregon.edu.1025 > 224.2.163.188.234 udp
16:25.49.92876 d230-17.uregon.edu.1025 > 224.2.163.188.234 udp
16:25.50.14227 d230-17.uregon.edu.1025 > 224.2.163.188.234 udp
16:25.50.13576 d230-17.uregon.edu.1025 > 224.2.163.188.234 udp
16:25.51.21101 d230-17.uregon.edu.1025 > 224.2.163.188.234 udp
16:25.50.27045 d230-17.uregon.edu.1025 > 224.2.163.188.234 udp
16:25.27.26215 Ez.Stanford.edu.332 * 224.2.163.188
```

# TCP/IP 与 Linux 协议实现

## 3.4.2 但路径上有路由器...

我们知道要去哪里，但不知道如何到达那里——路径上的某些东西会有帮助。关于 Linux 作为路由器的更多细节，请参见第 8 章和第 9 章。Linux 作为一个路由器工作得很好。基本上，你需要考虑输入，然后是输出，在 `route.c` 中发现了数据包，验证源地址，判断它是用于组播、环回还是其他，并将其添加到最近路由的哈希表中。`ip_forward` 执行各种检查（路由选项等）、处理、分片并在必要时生成 ICMP 错误，然后调用 `NF_HOOK`（过滤器工作，再次参见第 10 章），调度调用 `ip_forward_finish`，它检查快速路由决策，然后执行 `ip_send(skb)`。然后 `ip_send()` 执行分片，并调用 `ip_finish()`。

## 3.5 追踪的三种视图

作为实际 API 的示例，包括另一种用于获取 ICMP 访问的原始套字，让我们看看 `ping` 程序的追踪，如图 3.16 所示。

**图 3.16 ping 的使用。**
`PING bells.cs.ucl.ac.uk (128.16.6.31) from 128.16.6.226 : 56(84) bytes of data.`
`64 bytes from bells.cs.ucl.ac.uk (128.16.6.31): icmp_seq=0 ttl=255 time=819`

**图 3.17 ping 的链路视图。**
`10:38:11.70142 0:c0:4f:d3:c3 0:20:af:b1:e6: ip 98: ovavu.cs.ucl.ac.uk > brahms.cs.ucl.ac.uk.: icmp: echo request`
`10:38:11.70270 0:20:af:b1:e6 0:c0:4f:d3:c3 ip 98: brahms.cs.ucl.ac.uk > ovavu.cs.uac.ac.uk.: icmp: echo reply`

# 数据包的短暂生命

在此追踪中，你还可以看到查找目标 IP 地址的阶段，因为 `ping` 命令（如上）给了一个 DNS 名称——对于所考虑的系统，可以将其配置为本地查找、`/etc/hosts` 查找或 DNS 查找，并有一套当某种类型查找失败时的后续操作序列。

图 3.18 ping 的追踪。

```
1  open("/bin/ping", "ping", "c", "1", "bells") [/* 24 vars */]) = 0
2  open("/lib/resolv.so.2", O_RDONLY) = 3
3  getpid() = 4510
4  getuid() = 0
5  socket(PF_INET, SOCK_RAW, IPPROTO_ICMP) = 3
6  socket(0) = 0
7  gettimeofday(96037553,314449, NULL) = 0
8  open("/etc/resolv.conf", O_RDONLY) = 4
9  read(4, "search cs.ac.uk;nameserver ... 43)
10 socket(PF_INET, SOCK_STREAM, 0) = 0
11 connect(4, family=AF_INET, path="/var/run/socket.0.", 110) = -1 (Connection refused)
12 open("/etc/nwitch.conf", O_RDONLY) = 4
13 open("/etc/hosts", O_RDONLY) = 4
14 open("/etc/hosts", O_RDONLY) = 4
15 open("/lib/ns.so.2", O_RDONLY) = 6
16 uname("Linux", node="ox2.cs.ac.uk", ...) = 0
17 read("/dev/sda1", BIOS_START, ) = -1 (No such file or directory)
18 socket(PF_INET, SOCK_DGRAM, IPPROTO_IP) = 4
19 connect(4, family=AF_INET, sin_port=htons(53), sin_addr=addr(128.16.5.31)) = 16
20 send(4,"\x00\x00\x00\x00\x00\x00\x00\x00") = 36
21 time(NULL) = 96037153
22 poll({fd=4, events=POLLIN}, 5000) = 1
23 recvfrom(4,"\x00\x00\x00\x00\x00\x00\x00\x00", 1024, 0, {family=AF_INET, sin_port=htons(53), sin_addr=addr(128.16.5.31)}, [16]) = 215
24 close(4)
25 socket(PF_INET, SOCK_DGRAM, IPPROTO_UDP) = 4
26 connect(6, family=AF_INET, sin_port=htons(53), sin_addr=addr(128.16.5.31)}, [16]) = 0
27 getsockname(4, family=AF_INET, sin_port=htons(026), sin_addr=addr(128.16.626)) = 0
28 close(4)
29 bind(3, family=AF_INET, sin_port=htons(026), sin_addr=addr(128.16.626)) = 16
30 setsockopt(3, (SA_REUSEADDR), [SO_REUSEADDR=0x40000000], NULL) = 0
31 signal(2, SIGALRM(0x40000000), NULL
32 gettimeofday(96037153,465533, NULL) = 0
33 sendmsg(3, msg={family=AF_INET, sin_port=htons(0), iov={base=ptr\x00\x00\x00\x00\x26\x31\x00\x33\x39\x78\x70\x7c\x21...", len=64}]) = 0
34 close(6, msg={}, flags=0) = 0
35 signal(16, SIGALRM(0x40000000), *)
36 setimer(ITIMER_REAL, it_interval={0, 0}, it_value={10, 0}, NULL) = 0
37 time(NULL) = 96037153
38 recvfrom(3, "E\x70\x61\x78\x31\x73\x60\x60\x63\x42...", 192, 0, {family=AF_INET, sin_port=htons(4288), sin_addr=addr(128.16.5.31)}, [16]) = 84
39 gettimeofday(960371553,407464, NULL) = 0
40 uname({"linux", node=ovavu.cs.ucl.ac.uk", ...}) = 0
```
