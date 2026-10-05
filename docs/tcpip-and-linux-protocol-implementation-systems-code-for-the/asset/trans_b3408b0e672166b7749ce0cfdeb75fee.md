

# 索引 917

描述， 112
封装， 110
IRQs (中断请求)，见 IRQs (interrupt requests)
ISR (中断服务例程)，见 ISR (interrupt service routine routing)
协议公平性 vs. 不公平性，110
可靠性，106–108
资源控制，109–110
软 IRQs (中断请求)，114–121
任务，117–119

Tq (任务队列)
内联函数，114
映射，113
ioctl(1) 套接字层，162–183
IP 命令，637–638
IP 封装在 IP 名称中，384–402
ip_build(), 482–483

IPC (进程间通信)，894
描述，91–92
FIFO (先进先出)，见 FIFO (first out messages)
消息，92
命名管道，92
管道，91–92
道路，信号量，92
共享内存，92

socket APIs (应用编程接口)
替代编程，103–105
调用，93–98
描述，92
示例，98
非阻塞 IO，102–103
轮询，101–102
系统文件，105–106
使用，98–101

IPs (互联网协议)
地址分配，547–551
描述，1–5
流，见 flow
头部定义，110–111
基础设施协议，见 infrastructure protocols
输入，IP

IPv4 (网协议版本 4)，见 IPv4 (Internet protocol version 4)
IPv6 (网协议版本 6)，见 IPv6 (Internet protocol version 6)
内核协议实现，见 kernel protocol implementation

LAN 结构，5, 645, 894
层链接，479–480
输出，见性能
描述，17
差异化服务，18–20
集成服务，18
编程语言与方法论
抽象，9
C 结构、内存和线缆，7–9
C 集合，6–7
描述，5–6

协议栈，9–10
路线图，1
路由与路由选择
描述，11–12，见 routing
数据包交换模式，14–16，见也 packets

性能趋势，16–17
TCP，12–14，见也 TCP (transmission control protocol)
路由，见 routing
安全，见也 security
表，883

IPSec (网协议安全)，883, 894
IPv4 (网协议版本 4)
地址分配，数据结构，286
地址格式，228

ARP 初始化，287–291
ARP 接收，286–301
ARP 询问，291–293
IP 用户接口，308–311
配置与管理，286
描述，286

定义，284
描述，315
转发，241–244，见也 forwarding
分片，225–254, 56，见也 fragmentation

ICMP (网控制消息协议)，308–311, 894
IGMP (网组管理协议)
描述，332–333, 66
组/接口状态管理，
多播转发，347
多播初始化，381
多播路由，616–620
多播传输，367–374
PIM (协议无关多播)
规范，374–381
接收，336–338

NAT (网络地址转换)，381–382，见也
NAT (网络地址转换)，308–311, 894
网络层级发现，256–270
选项与配置，见也输出
添加头部并见， 215–216

校验和，217
拆分，219
最终检查，216–217
分片，225–234, 56，见也 fragmentation
初始化，224–235
环回，217
多播复制，218
非连续缓冲区，232–234
标记传输，227–232

数据包，229–231
远程，218
sockets
选项，275–286
socket glue (胶接层)，270–280
subidor 树结构，43

描述，381
GRE (通用路由封装)，402–428
IP 封装 IP，384–402
NAT (网络地址转换)，381–384,
ipv4 (IP 版本 4 代码)，42
IPv6 (网协议版本 6)，42
地址 (自动配置)，434–344
APIs (应用编程接口)，433–434
对传输的影响，472
流标签，467–469
转发，459–461，也是 IPv6 (Internet protocol version 6)
头部，228–233
扩展，469–471
输入，457–451
IPv6 (IP 版本 6 代码)，42
邻居发现，444–450
输出，451–459
路由器广告，446–450
SIT (简单隧道接口)，471–472
socket glue，461–467
IPv6 (IP 版本 6 代码)，42
定义，884
ipv6 (网协议)，430
ipv6 (Noel's IP 协议)，431
IRB (红外访问)，43
IRQs (中断请求)，584
描述，28–29
软，114–121
ISR (Internet socket route)，28–29
抖动，652, 654

内核模块，53–64
内核协议实现，121–123
设备驱动 API，123–127
网络接收，127
中断与任务调度，119–121
下半部，119–121
tasklets (任务链)，119–121
TQ (任务队列) 内联函数，114
TQ (任务队列) 映射，113–114
TQ (任务队列) 结构，112–113
多处理器，110–111
协议块，196
路线图，107
socket 缓冲区，185–187
从全局池释放，180–192
操作，185–187
sk_buff 结构，185–196
accept (函数)，170–173
异步事件，163–166
缓冲区，148–149
调用，派生，175–179
调用，其他，169–170
连接记账，173–175
创建 ascii，166
GNU General Public License (许可证)，144–146
ioctl(1) 套接字层，163–183
列表: 0, 170–173
锁定套接字，146–149
映射套接字与文件描述符，155–161
非递归，110
协议-socket 关联，181–184
虚拟文件系统，143–144
缓冲，110
通信栈，106–110
死锁，110
去封装，110
多路复用，109
封装，110
存活锁，110–111
下层调用，108
多路复用，109
生产者/消费者链，108–110
协议公平性 vs. 不公平性，110
可靠性，106–108
资源控制，109–110
上层调用，108
传输状态
BSD 风格架构，213–214
示例，196
示例，205–228
引用计数，212–213
socket 凭证接口，212–213
socket 清，205–206
sockets 和路由，208–212
内核 读/写锁，38
内核 留，42–55
内核-关键序列化，396
内核 (核心) 代码用于进程、模块和调度，42
mpsid (在内核空间中使用 HTTP 应用)，42
杀手资源问题，894

lapb (基于链路层的访问)，43
泄露缓冲区，685–686
最近使用，通过 LRU (recently-used)
lib/ (通用内核支持函数)，42
LIO (Linux Owner)，53–64, 894
链路方程，946–935
Linux Leader，见 LIO (Linux Owner)
Linux OS (操作系统)
应用支持，66
定义和描述
C 类型，31–38
并发控制，35–38
设备，39
I/O通信，29–30
简介，22–23
内核关键区域序列化，36
内核自旋锁，38
内存管理，38–39
多设备方面，27–29
多任务方面，24–26
多处理器方面，24
管道，30
处理器独立性，30–35
socks，38

自旋锁概述，37
块设备注册，57–58
字符设备注册，56–57
描述，56
网络设备注册，58–63
内核模块，63–64
LILO (本地输入输出)，53–54
事件排序，66
描述，66
PIT (可编程定时器)，67
RTC (实时时钟)，66
定时时钟，68
定时器结构，67
TSC (时间戳计数)，67
进程视图，44
描述，43–44
调度器，45–52
内核视图，44
SMP (对称多处理)，64
源代码，41–42
目录结构，42
IPv4 子目录，42–43
属性和优势，40–41
linux/2.4/include/net/socket.h, 479
linux/2.4/include/ipv4/tcp.c, 550–563
linux/2.4/include/ipv4/udp.c, 580–581
linux/2.4/include/ipv4/udp_skb.c, 469–470
linux/net/ipv6/ip_in.c, 450–451
linux/net/ipv6/ip_skb.c, 482–486
linux/net/ipv6/dev_alloc.c, 518–520
linux/net/ipv6/socket.c, 602–606
linux/net/misc/disc.c, 439–444
linux/net/kernel/hashtmap.h, 531–535
/net/sched/cls_api.c, 666–674
linux/net/sched/cls_fw.h, 708–712
linux/net/sched/route.c, 702–707
linux/net/sched/rvp.h, 689–700
linux/net/sched/cls_timer.c, 713–719
linux/net/sched/activator.c, 706–798
linux/net/sched/policy.h, 782–800
linux/net/sched/sch_api.c, 721–733, 748–749
linux/net/sched/dev_delta.c, 792–802
linux/net/sched/cls_cb.c, 758–787
linux/net/sched/cls_zeg.h, 791–793
linux/net/sched/asym.c, 812–814
linux/net/sched/generic.c, 758
linux/net/sched/igress.c, 830–831, 832–837
linux/net/sched/rt_rio.c, 815–823
linux/net/sched/sfq.c, 836–845
linux/net/sched/rt_codel.c, 853–855
linux/net/sched_taql.c, 846–854
linux/net/sched/smp.c, 322–334
linux/net/sched/ipv4/ip.h, 332–344
linux/net/sched/ipv4/ip.c, 341–343
linux/net/sched/ipv4/ipfrag.c, 241–244
linux/net/sched/ipv4/ip_raw.c, 402–407
linux/net/sched/ipv4/ip_route.h, 332–338
linux/net/sched/ipv4/ip_options.c, 257–269
linux/net/sched/ipv4/ip_output.h, 78, 215–240
linux/net/sched/ipv4/socket.c, 376–380
linux/net/sched/ipv4/netfilter.h, 439
linux/net/sched/ipv4/route.h, 627–628, 80–36
linux/net/sched/ipv4/tcp.c, 1062
linux/net/sched/ipv4/tcp_output.c, 77
linux/net/sched/ipv4/udp.h, 83–87
linux/net/sched/ipv4/udpconf.c, 43–47

