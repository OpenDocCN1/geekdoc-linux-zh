
# 第 25 章

## 25.1
不，该修改引入了错误。问题在于 `nqueue` 在处理数组项 `dg[iget]` 之前就减了，这允许信号处理程序将新的数据报读入该数组元素。

# 第 26 章

## 26.1
在 `fork` 示例中，将 101 个正在使用的描述符、一个监听套接字和 100 个连接套接字。但 101 个进程中的每一个（一个父进程，100 个子进程）都只打开了一个描述符（忽略其他任何，如果服务器没有守护化，则是标准输入）。然而，在线程服务器中，单个进程中有 10 个描述符。每个线程（包括主线程）都在处理一个描述符。

## 26.2
TCP 连接终止的最后两个分段——服务器的 `FIN` 和客户端对该 `FIN` 的 `ACK`——将不会交换。这导致客户端的连接端处于 `FIN WAIT_2` 状态（图 2.4）。源自 Berkeley 的实现在客户端端处于此状态略超过 11 分钟后将会对客户端端进行超时处理（TCPv2 第 825–827 页）。服务器最终也会耗尽描述符。

## 26.3
当主线程从套接字读取到 EOF 且另一个线程仍在运行时，它应该打印此消息。实现此点的一种简单方法是声明另一个外部命名的变量 `done` 并将其初始化为 0。在线程返回之前，它将此变量设置为 1。主线程检查此变量，如果为 0，则打印错误。由于只有一个线程设置该变量，因此不需要同步。

# 第 27 章

## 27.1
没有任何变化；所有系统都是邻居，因此严格源路由（strict source route）与松散源路由（loose source route）是相同的。

## 27.2
我们会在缓冲区末尾放置 EOL（一个字节的 0）。

## 27.3
由于 `ping` 创建了原始套接字（第 28 章），它在通过 `recvfrom` 读取每个数据报时，都会接收完整的 IP 头部，包括任何 IP 选项。

## 27.4
`reread` 由 `inetd`（第 13.5 节）调用，因此描述符 0 是指向客户端的套接字。

## 27.5
问题在于 `setsockopt` 的第五个参数是长度的指针，而不是长度本身。这个 bug 可能在使用 ANSI C 原型时已经修复。事实证明，这个 bug 是无害的，因为正如我们提到的，为了清除 `IP_OPTIONS` 套接字，我们可以在第四个参数指定空指针，或者指定第五个参数（长度）为 0（TCPv2 第 269 页）。

# 第 28 章

## 28.1
IPv6 头部中的版本号字段和下一个头部字段不可用。有效负载长度字段可以作为输出函数的参数或返回值可用。如果需要巨型负载选项（jumbo payload option），该选项本身对应用程序不可用。分片头部也不可用。

## 28.2
最终，客户端的接收缓冲区将填满，导致守护进程的 `write` 阻塞。我们不希望发生这种情况，因为这会停止守护进程处理其套接字上的更多数据。最简单的解决方案是让守护进程将其 Unix 连接的末端设置为非阻塞。此时守护进程必须调用 `write` 而不是封装函数，并直接忽略 `EWOULDBLOCK` 错误。

## 28.3
源自 Berkeley 的内核默认在原始套接字上允许广播（TCPv2 第 157 页）。`SO_BROADCAST` 套接字选项仅在 UDP 套接字需要指定。

## 28.4
我们的程序没有检查多播地址，也没有设置 `IP_MULTAST_IF`。因此，内核通过在路由表中查找 224.0.1. 来选择出站接口。我们也没有设置 `IP_MULTAST_TTL` 字段，所以它默认值为 1，这是可以接受的。

# 第 29 章

## 29.1
该标志表示缓冲区已通过 `sigsetjmp` 设置（图 29.10）。虽然该标志似乎是多余的，但信号可能会在信号处理程序建立之后、但在调用 `sigsetjmp` 之前传递。即使程序没有产生信号，也可以通过其他方式产生信号，例如使用 `kill` 命令 命令。

# 第 30 章

## 30.1
父进程保持监听套接字打开，以防在以后某个时刻需要 `fork` 额外的子进程（这将是对我们代码的增强）。

## 30.2
是的，可以使用数据报套接字来传递描述符，而不是使用流套接字。使用数据报套接字时，当子进程提前终止时，父进程在其流端不会接收到 EOF，但父进程可以使用 `SIGCHILD` 实现此目的。在这种场景下，使用 `SIGCHILD` 与第 28.7 节中 `icmpd` 的一个区别是，在后者，客户端和服务器之间没有父/子关系，因此流上的 EOF 是服务器检测客户端消失的唯一方法。

# 第 31 章

## 31.1
我们在这里假设协议的默认行为是在流关闭时进行有序释放，这对于 TCP 来说 true。

# 参考文献

所有的 RFC 均可以通过电子邮件、匿名 FTP 和万维网免费获取。一个起点是 `http://www.ietf.org`。目录 `ftp://rfc-editor.org/in-notes` 是 RFC 的一个位置。RFC 未指定 URL。

标记为 "Internet Draft" 的项目在 IETF 正在进行中。这些草案在发布六个月后过期。在本书出版后，草案的相应版本可能会发生变化，或者草案可能会发布为 RFC。它们与 RFC 一样通过互联网免费获取。`http://www.ietf.org` 是 Internet 草案的主要仓库。我们包含了每个 Internet 草案 URL 的文件文件名部分，因为文件名包含版本号。

每当本参考文献引用的论文或报告有电子副本时，都会包含其 URL。请注意这些 URL 可能会随时间变化，鼓励读者检查书籍主页上本文的勘误（Errata）以获取任何更改（`http://www.unbook.com/`）。可以在 `http://citeser.nj.com/cs` 找到一个极好的在线论文数据库。

Butofen, D. R. 1997. 《基于 POSIX 线程的编程》，ison-Wesley, Reading, MA.

Cain, B., Bering, S. E., Kouvelas, I., Jenner, B., and Thyagarajan, A. 2002. “组组协议第3版”, RFC 3376.

Carpenter, B., and Moore, K. 2001. “通过 IPv4 连接 IPv6 地址”, RFC 3056.

CERT, 1996a. “UDP 端口拒绝服务攻击”, Advisory CA-96.01, 计算机应急响应小组, Pittsburgh, PA.

CERT, 1996b. “TCP SYN 洪水攻击与 IP 欺骗攻击”, Advisory CA-96.21, 计算机应急响应小组, Pittsburgh, PA.

Cheswick, W., Belovin, S. M., and Rubin, A. D. 2003. 《防火墙与互联网安全：击败黑客》，Addison-Wesley, Reading, MA.

Conta, A. and Deering, S. E. 1999. “针对互联网协议版本6 (IPv6) 的互联网控制消息协议 (ICMP6)规范”, RFC 2463.

Conta, A. and Deering, S. E. 2001. “针对互联网协议版本6 (IPv6) 的互联网控制消息协议 (ICMP6)”, draft-ietf-ipv6-icmp-v3-02.txt（互联网草案）。这是 [Conta and Deering 1999] 的修订版，预计将取代它。

Crawford, M. 1998a. “通过以太网传输 IPv6 数据包”, RFC 2464.

Crawford, M. 1998b. “通过 FDDI 网络传输 IPv6 数据包”, RFC 2467.

Crawford, M., Narten, T., and Thomas, S. 1998. “通过令牌环形网络传输 IPv6 数据包”, RFC 2470.

Deering, S. E. 1989. “ip 多组播主机扩展”, RFC 1112.

Deering, S. E. and Hinden, R. 1998. “互联网协议版本6 (IPv6 规范), RFC 2460.

Daves, R. 2003. “互联网协议版本6 (IPv6) 的默认地址选择”, RFC 3484.

Eriksson, H. 1994. “MBONE：多组播骨干”,*Communications of the ACM*, 第 37 卷，第 8 期，第 54-60 页。

Fink, R. and Hinden, R. 2003. “6bone (IPv6 测试地址分配)淘汰”, draft-fink-6bone-phase-04.txt（互联网草案）。

Full, V., Li, T., Yu, J., and Varadhan, K. 1993. “无类域间路由 (CIDR): 地址分配与聚合策略”, RFC 1519.

Garfinkel, S. L., Schwartz, A., and Spafford, E. H. 2003. 《实用 UNIX 与互联网安全，第 3 版》。O’Reilly & Associates, Sebastopol, CA.

Getty, J. and Nielsen, H. F. 1998. SMUX 协议规范 (`http://www.w3.org/TR/WDmux`).

Gierth, A. 1996. 私人通信。

Gilligan, R. E. and Nordmark, E. 2000. “IPv6 主机与路由器的转换机制”, RFC 2893.

Gilligan, R. E., Thomson, S., Bound, J., McCann, J., and Stevens, W. R. 2003. “IPv6 基础套接扩展”, RFC 3493.

Gilligan, R. E., Thomson, S., Bound, J., and Stevens, W. R. 1997. “IPv6 基础套接扩展”, RFC 2133（已被 RFC 2553 取代）。

Gilligan, R. E., Thomson, S., Bound, J., and Stevens, W. R. 1999. “IPv6 基础套接扩展”, RFC 2553（已被 RFC 3493 取代）。

Haberman, B. 2002. “IPv6 多组播分配”, RFC 3307.

Haberman, B. and Thaler, D. 2002. “基于前缀的 IPv6 地址”, RFC 3306.

Handley, M. and Jacobson, V. 1998. “SDP: 会话描述”, RFC 2327.

Handley, M., Perkins, C., and Whelan, E. 2000. “会话”, RFC 2974.

Harkins, D. and Carrel, D. 1998. “互联网密钥交换 (IKE), RFC 2409.

Hinden, R. and Deering, S. E. 2003. “互联网协议版本6 (IPv6) 址”, RFC 3513.

Hinden, R., Deering, S. E., and Nordic, M. 2003. “IPv6 全单播格式”, RFC 3587.

Hinden, R., Fink, R., and Postel, J. 1999. “大规模应用的 IPv6 测试”, Communication Review, 第 29 卷，第 4 期，第 65–78 页。

Huitem, C. 2001. “路由器转发前缀”, RFC 3068.

IANA, 2003. 协议/编号 (`http://www.iana.org/numbers`)。

IEEE, 1996. “信息技术—可移植操作系统 (POSIX)—第 1 部分：系统接口 (API), IEEE Std. 1003.1996，电气工程师, Paterson, NJ。此版本的 POSIX 包含了 1990、1003.1 实时 (1993) 以及 1003-1 技术修正 (1995)。这是国际标准 ISO/IEC 9945-1 (1996)。IEEE 标准和草案请访问 `http://www.ieee.org`。

IEEE, 1997. “全局位标识符 (EUI-64) 注册机构”。电气工程师, Paterson, NJ (`http://standards.ieee.org/regauth/EUI64.html`)。

Jacobson, V. 1988. “拥塞避免与控制”, Communication Review, 第 18 卷，第 4 期，第 314–329 页 (`http://ftp.ieee.org/papers/congestionav.`)。描述 TCP 慢启动和拥塞避免算法的经典论文。

Jacobson, V., Braden, R. T., and Borman, D. A. 1992. “高性能 TCP 扩展”, RFC 1232。描述了窗口选项、时间戳选项以及 PAWS 算法，以及需要这些修改的原因。

Jacobson, V., Braden, R. T., and Zhang, L. 1990. “高速路径 TCP 扩展”, RFC 1185（已被 RFC 1233 取代）。

Jose, A., ed. 1997. 《Solo 2：单一 Unix 规范第 2 版指南》。Prentice Hall, Upper Saddle River, NJ.

Jose, A., ed. 2002. 《单一 Unix 规范—第 3 版指南》。Open Group, Berkeley, CA.

Joy, W. N. 1994. 私人通信。

Karn, P. and Partridge, C. 1991. “可靠传输协议中往返时间估计的改进”, ACM Transactions on Computer Systems, 第 9 卷，第 4 期，第 364–373 页。

Kelly, D. 1993. “通过 FDDI 网络传输 IP 和 ARP”, RFC 1390.

Katz, D. 1997. “IP 路由器告警选项”, RFC 2113.

Kent, S. T. 1991. “美国国防部针对互联网协议的安全选项”, RFC 1108.

Kent, S. T. 2003a. “IP 认证头部”, draft-ietf-ipsec-rfc2402bis-04.txt（互联网草案）。

Kent, S. T. 2003b. “封装安全载荷 (ESP), draft-ietf-ipsec-esp-v3-06.txt（互联网草案）。

Kent, S. T. and Atkinson, R. J. 1998a. “互联网协议安全架构”, RFC 2401.

Kent, S. T. and Atkinson, R. J. 1998b. “IP 认证头部”, RFC 2402。截至本文写作，该 RFC 正在由 IETF IPSec 更新（见 Kent 2003a）。

Kent, S. T. and Atkinson, R. J. 1998c. “封装安全载荷 (ESP), RFC 2406。截至本文写作，该 RFC 正在由 IETF IPSec 更新（见 Kent 2003b）。

Kernaghan, B. W. 1984. 《UNIX 环境》。

Kernaghan, B. W. and Ritchie, M. 1988. 《C 语言》，第二版。Prentice Hall, Englewood Cliffs, NJ.

Lanciani, D. 1996. “Re: sockets: AF_INET vs. PF_INET”, Message-ID:<35661@news.IPSS.COM> USENET comp.protocols-ip.

Maslen, T. 1997. “gethostby() and Threads”, Message-ID:<maslen.8624@shellx> USENET comp.threads.

McCann, J., Deering, S. E., and Mogul, J. C. 1996. “IP 路径 MTU 发现”, RFC 1981.

McCanne, S. and Jacobson, V. 1993. “BSD 数据包过滤器：一种新的用户级捕获架构”,1993 年冬季 UNIXIX 会议，San Diego, CA，第 259-269 页。

McDonald, D. L., Metz, C., and Phan, B. G. 1998. “PF_KEY 密钥管理 API，第 2 版”, RFC 2367.

Kusick, M. K., Bostik, K., Kales, M.J., and Quarterman, J. 1999. 《4.4BSD 操作系统的设计与实现》。Addison-Wesley, Reading, MA.

Meyer, D. 1992. “管理范围 IP 多组播”.

Mills, D. L. 1992. “网络时间协议（第 3 版）规范、实现”, RFC 1305.

Mills, D. L. 1996. “简单网络时间协议 (SNTP) 第 4 版适用于 IPv4、IPv6 和 OSI”, RFC 2030.

Mogul, J. C. and Deering, S. E. 1990. “路径 MTU 发现”, RFC 1191.

Narten, T. and Daves, R. 2001. “IPv6 无状态地址自动配置的隐私扩展”, RFC 3041.

Nemeth, E. 1997. 私人通信。

Nichols, K., Blake, S., Baker, F., and Black, D. 1998. "IPv4 和 IPv6 头部中的区分服务字段（DS 字段）定义," RFC 2474.

Nordemark, E. 2000. "无状态 IP/ICMP 翻译算法 (SIIT)," RFC 2765.

Ong, L., Rytina, I., Garcia, M., Schauspieler, B., Coene, L., Lin, H., Juhasz, I., Holdregge, M., and Sharp, C. 1999. "信令传输的框架架构," RFC 2719.

Ong, L. and Yoakum, 2002. "流控制传输协议 (SCTP) 简介," RFC 3286.

The Open Group, 1997. CAE 规范，网络服务 (XNS), 5. The Open Group, 英国伯克夏郡。这是 Unix 98 中 sockets 和 XTI 的规范，已被《单索引规范第三版》取代。该规范还包含描述了 XTI 与 Net-BIOS、OSI 协议、SNA 以及 Netware IPX 和 SPX 协议使用的附录。三个附录涵盖了 sockets 和 XTI 用于 ATM。

Partridge, C. and Jackson, A. 1999. "IPv6 路由器告警选项," RFC 2711.

Partridge, C., Mendez, T., and Milliken, M. 1993. "主机任播服务," RFC 1546.

Partridge, C. and Pink, S. 1993. "更快的 UDP," IEEE/ACM Transactions on Networking, v. 1, no. 4, pp. 42–490.

Paxson, V. 1996. "互联网中的端到端路由行为," Computer Communication Review, v. 26, no. 4, pp. 25–38 (`http://ftp.ietf.org/papers/routing.SIGCOMM.ps.z`).

Paxson, V. and Allman, M. 2000. "连接 TCP 的重传计时器," RFC 2988.

Plauger, J.J. 1992. 标准库。Prentice Hall, Englewood Cliffs, NJ.

Postel, J. B. 1980. "用户数据报协议," RFC 768.

Postel, J. B. 1981a. "IP协议," RFC 791.

Postel, J. B. 1991b. "互联网控制消息协议," RFC 792.

Postel, J. B. 1981c. "传输控制协议," RFC 793.

Pasteri, T. 1993. UNIX 系统 V 网络编程。Addison-Wesley, Reading, MA.

Rago, S. A. 1993., Conta, A., Carpenter, B., and Deering, S. E. 2003. "IPv6 流标签规范," draft-iet-ipv6-flow-label-07.txt (互联网草案).

Ramakrishnan, K., Floyd, S., and Black, D. 2001. "在 IP 中增加显式拥塞通知 (ECN)," RFC 3168.

Rekheter, Y., Moskowitz, B., Karenberg, D., de Groot, G. J., and Lear, E. 1996. "私有网络的地址分配," RFC 1918.

Reynolds, J. 2002. "分配的数字：RFC 1700 由在线数据库取代," RFC 3232。此 RFC 中提到的数据库是 [IANA 2003]。

Reynolds, J. K. and Postel, J. B. 1994. "分配的数字," RFC 1700 (已被 RFC 3232 废弃)。此 RFC 是“分配的数字”RFC 系列中的最后一个一个。由于信息变化频繁，因此决定简单地保持目录在线。更多解释请参见 [Reynolds 2002]，数据库本身请参阅 [IANA 2003]。

Ritchie, D. M. 1984. "一种流输出系统," AT&T 贝尔实验室杂志, vol. 63, no. 8, pp. 897–910.

Salus, P. H. 1995. "一个世纪的 Unix," Addison-Wesley, Reading, MA.

Salus, P. H. 1995. "撒网：从 ARPANET 到互联网,"Addison-Wesley, Reading, MA.

Schimmel, C. 1994. "现代架构的 UNIX 系统：内核的对称多处理与缓存,"Addison-Wesley, Reading, MA.

pero, S. 1996. "会话控制协议 (SCP)," `http://www.w3.org/Protocols/scp.html`.

Srinivasan, R. 1995. "外部数据表示," RFC 1832.

Stevens, W. R. 1992. "在 Unix 环境下编程,"Addison-Wesley, Reading, MA. 关于 Unix 编程的所有细节。

Stevens, W. R. 1994. "TCP/IP 彻底详解，第一卷：协议,"Addison-Wesley, Reading, MA. 互联网的介绍。

Stevens, W. R. 1996. "TCP/IP 彻底详解，第二卷：实现,"Addison-Wesley, Reading, MA. 4.4BSD-Lite 操作系统中的协议的实现。本文称为 TCPv2。

Stevens, W. R. and Thomas, M. 1998. "用于 IPv6 的高级 sockets," RFC 2292 (已被 RFC 3542 废弃)。

Stewart, W. R., Thomas, M., Nordemark, E., Jin, T. 2003. "用于 IPv6 的高级 sockets," RFC 3542.

Stewart, W. R., Bestler, C., Jim, J., Gulandy, S., Kashyap, V. 2003. "流控制传输协议 (SCTP) 远程内存访问 (RDMA) 直接数据放置," draft-wart-dctp-02.txt (互联网草案).

Stewart, W. R., Xie, Q., Malalho, M., Rytina, I., 康rad, P. 2003. "流控制传输协议 (SCTP) 动态地址重配置," draft-iest-tsp-07.txt (互联网草案).

Stewart, W. R., Xie, Q., Morault, K., Sharp, C. 2001. "流控制传输协议 (SCTP) 参考指南,"Addison-Wesley, Reading, MA.

Stewart, W. R., Xie, Q., Schwarzbauer, H., Paxson, V., Zhang, L., Stone, J. 2000. "流控制传输协议 (SCTP)," RFC 2960.

Stone, J., Stewart, W. R., and Otis, D. 2002. "流控制传输协议 (SCTP) 校验和更改," RFC 3309.

Tanenbaum, A. 1987. 操作系统设计与实现。Prentice Hall.

Thomson, S. and Huiteman, 2005. "支持 IP 版本 6 的扩展," RFC 1886.

Torek, C. 1994. "TCP/IP 中的 Relay-relay," Message-ID: <19950110028.QAA1683@elf.body.com>; USENET net.com/newsgroups (`http://www.unbook.com/torek.94dec31.txt`).

Touch, J. 1997. "TCP 控制相互依赖," RFC 2140.

Unix International, 1991. 数据链路提供接口规范。Unix International, Parsippany, NJ, Revision 2.0.0 (`http://www.unbook.com/dlpi.2.0.0.os`)。该规范的新版本可以在 The Open Group 在线获取 `http://www.rdg.opengroup.org/pubs/catalog/web.htm`。

Unix International, 1992a. 网络提供接口规范。Unix International, Parsippany, NJ, Revision 2.0.0 (`http://www.unbook.com/npi.2.0.0.ps`).

Unix International, 1992b. 传输提供接口规范。Unix International, Parsippany, NJ, Revision 1.5 (`http://www.unbook.com/tpi.1.5.ps`)。该规范的新版本可以在 The Open Group 在线获取 `http://www.rdq.opengroup.org/pubs/catalog/web.htm`。

Vixie, P. A. 1996. 私人通信。

Wright, G. R. and Stevens, W. R. 1995. "TCP/IP 彻底详解，第二卷：实现."Addison-Wesley, Reading, MA. 4.4BSD-Lite 操作系统中互联网协议的实现。本文称为 TCPv2。
