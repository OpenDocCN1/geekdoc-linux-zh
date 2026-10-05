
[25] 计算机网络：自上而下的方法面向互联网，J. Kurose, K. Ross, Addison Wesley, 2001.

[26] “点击模块化路由器，”Eddie Kohler, Robert Morris, Benjie Chen, John Jammotti, and M. Frans Kaashe, ACM Transactions on Computer Systems Vol. 18, No. 3, pp. 263–297, 2000年8月

[27] Linux路由器：网络管理员入门指南，Tony Mancill, Prentice Hall, 2001.

[28] 防火墙与互联网安全：防御狡猾黑客，William R. Cheswick, Steven M. Bellovin (贡献者)，第2版，Addison-Wesley, 2001年10月

# 代码中引用的 RFC

RFC 是关于互联网协议族的、著名的“请求意见”（Request for Comments）系列文档。其中一些是标准，一些是纯信息性的（有些是历史性的，或者仅仅是为了娱乐）。Linux 内核代码（以及其他地方）中的许多点，实现者都会引用相关的 RFC。在这里我们列出该列表。请访问 http://www.ietf.org 获取这些文档以及它们描述的协议和服务的可用性和状态信息。

- 0791 互联网协议。J. Postel. 1981年9月1日。
- 0793 传输控制协议。J. Postel. 1981年9月1日。
- 0815 IP 数据报重组算法。D. D. Clark. 1982年7月1日。
- 0826 以太网地址解析协议。D. C. Plummer. 1982年11月1日。
- 0950 互联网标准子网划分程序。J. C. Mogul, J. Postel. 1985年8月1日。
- 0961 官方 ARPA-互联网协议。J. C. Reynolds, J. Postel. 1985年12月1日。
- 1042 在 IEEE 802 网络上传输 IP 数据报的标准。J. Postel, J. K. Reynolds. 1988年2月1日。
- 1048 BOOTP 厂商信息扩展。P. A. Prindville. 1988年2月1日。
- 1051 在 ARCNET 网络上传输 IP 数据报和 ARP 包的标准。P. A. Prindville. 1988年3月1日。
- 1063 MTU 发现选项。J. C. Mogul, C. A. Kent, C. Partridge, K. McClaugh. 1988年7月1日。
- 1112 IP 多组播主机扩展。S. E. Deering. 1989年8月1日。
- 1122 互联网主机需求——传输层。R. T. Braden. 1989年10月1日。
- 1191 路径 MTU 发现。J. C. Mogul, S. E. Deering. 1990年11月1日。
- 1201 在 ARCNET 网络上传输 IP 流量。D. Provan. 1991年2月1日。
- 1323 高性能 TCP 扩展。J. Jacobson, R. Braden, D. Berman. 1992年5月。
- 1337 TCP 中的 TIME-WAIT 杀害风险。R. Braden. 1992年5月。
- 1390 FDDI 网络上的 IP 和 ARP 传输。D. Katz. 1993年1月
- 1414 标识 MIB。M. St. Johns, M. Rose. 1993年1月。
- 1469 令牌环形局域网上的 IP 多组播。T. Pusateri. 1993年6月。
- 1483 在 ATM 适配层 5 上的多协议封装。Juha Heinan. 1993年7月。
- 1490 帧中继上的多协议互连。T. Bradley, C. Brown, A. Malis. 1993年7月。
- 1512 FDDI 管理信息库。J. Case, A. Rijingsinhani. 1993年9月。
- 1577 ATM 经典 IP 和 ARP。M. Laubach. 1994年1月。
- 1584 OSPF 的多组播扩展。J. Moy. 1994年3月。
- 1589 用于计时的内核模型。D. Mills. 1994年3月。
- 1626 用于 ATM AAL5 的默认 IP MTU。R. Atkinson. 1994年5月。
- 1701 通用路由封装 (GRE)。S. Hanks, T. Li, D. Farinacci, P. Traina. 1994年10月。
- 1702 IPv4 网络上的通用路由封装。S. Hanks, T. Li, D. Farinacci, P. Traina. 1994年10月。
- 1762 PPP DECNet 第 IV 期控制协议 (DNCP)。S. Senum. 1995年3月。
- 1812 IP 版本 4 路由器需求。F. Baker. 1995年6月。
- 1826 IP 身份验证头。R. Atkinson. 1995年8月。
- 1883 互联网协议版本 6 (IPv6)规范。S. Deering, R. Hinden. 1995年12月。
- 1885 用于互联网协议版本 6 (IPv6) 的互联网控制消息协议 (ICMPv6)。A. Conta, S. Deering. 1995年12月。
- 1945 超文本传输协议—HTTP/1.0。T. Berners-Lee, R. Fielding, H. Frystyk. 1996年5月。
- 2003 IP 内部封装。C. Perkins. 1996年10月。
- 2067 HIPPI 上的 IP。J. Renwick. 1997年1月。
- 2131 动态主机配置协议。R. Droms. 1997年3月。
- 2133 IPv6 基础套接接口扩展。R. Gilligan, S. Thomson, j. Bound, W. Stevens. 1997年4月。
- 2207 IPSEC 数据流 RSVP 扩展。L. Berger, T. O'Malley, 1997年9月。
- 2402 IP 身份验证头。S. Kent, R. Atkinson. 1998年11月。
- 2460 互联网协议版本 6 (IPv6)规范。S. Deering, R. Hinden. 1998年12月。
- 2481 显式拥塞通知 (ECN) 建议。K. Ramakrishnan, S. Floyd. 1999年1月。
- 2516 通过以太网传输 PPP (PPPoE)。L. Makamos, K. Lidl, D. Evarts, D. Carrel, D. Simon, R. Wheeler. 1999年2月。
- 2553 IPv6 基础套接接口扩展。R. Gilligan, S. Thomson, j. Bound, W. Stevens. 1999年3月。
- 2581 TCP 拥塞控制。M. Alman, V. Paxson, W. Stevens. 1999年4月。
- 2582 TCP 新 Reno 算法修改。S. Floyd, T. Henderson. 1999年4月。
- 2861 TCP 拥塞窗口验证。M. Handley, J. Padhye, S. Floyd. 2000年6月。
- 2988 TCP 重传计时器。V. Paxson, M. Allman. 2000年11月。

# 代码作者

```
<chexum@bankinf.banki.hu>
<Tim_Alpaerts@toyota-motor-europe.com>
Aage Kvalnes <aage@cs.uit.no>
Adam Sulmicki <adam@cfar.umd.edu>
Al Longyear <longyear@netcom.com>
Alan Cox <alan.cox@linux.org>
Alexey Kuznetsov <kuznet@ms2.inr.ac.ru>
Andrey V. Savochkin <saw@msu.ru>
Arnaldo Carvalho de Melo <acme@connectiva.com.br>
Arnt Gulbrandsen@nvg.unit.no>
```

# 参考文献

Charles Hedrick <hedrick@klinzhai.rutgers.edu>
<chihjenc@scf.net>
Aage Kvalnes <aage@cs.uit.no>
Adam Sulmicki <adam@cfar.umd.edu>
Al Longyear <longyear@netcom.com>
Alan Cox <alan.cox@linux.org>
Alexey Kuznetsov <kuznet@ms2.inr.ac.ru>
Andrey V. Savochkin <saw@msu.ru>
Arnaldo Carvalho de Melo <acme@connectiva.com.br>
Arnt Gulbrandsen@nvg.unit.no
