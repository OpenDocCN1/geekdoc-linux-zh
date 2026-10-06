
## A.3.6. Subversion 镜像站点

FreeBSD 的 Subversion 仓库地址为：

`svn.FreeBSD.org`。

这是一个公共访问的镜像网络，它使用 GeoDNS 选择合适的后端服务器。要通过浏览器查看 FreeBSD Subversion 仓库，请使用 `https://svnweb.FreeBSD.org/`。

HTTPS 是首选协议，但需要安装 `security/ca_root_nss` 包才能自动验证证书。

### A.3.7. 更多信息

关于 Subversion 的其他信息，请参阅名为《Version Control with Subversion》的 Subversion 书籍或 Subversion 文档。

### A.4. 使用 rsync

这些站点通过 rsync 协议提供 FreeBSD 服务。`rsync` 工具仅传输两个站点之间的差异。这对于 FreeBSD FTP 服务器的镜像站点非常有用。`rsync` 套件适用于许多操作系统，在 FreeBSD 上，请查看 `net/rsync` 端口或使用该包。

捷共和国
`rsync://ftp.cz.FreeBSD.org/`
可用集合：
- `ftp`: FreeBSD FTP 服务器的部分镜像
- `FreeBSD`: FreeBSD FTP 服务器的完整镜像。

荷兰
`rsync://ftp.nl.FreeBSD.org/`

可用集合：
- `FreeBSD`: FreeBSD FTP 服务器的完整镜像。

俄罗斯
`rsync://ftp.mtu.ru/`

可用集合：
- `FreeBSD`: FreeBSD FTP 服务器的完整镜像。
- `FreeBSD-Archive`: FreeBSD Archive FTP 服务器的镜像。

瑞典
`rsync://ftp4.freebsd.org/`

可用集合：
- `FreeBSD`: FreeBSD FTP 服务器的完整镜像。

台湾
`rsync://ftp.tw.FreeBSD.org/`
`rsync://ftp2.tw.FreeBSD.org/`
`rsync://ftp6.tw.FreeBSD.org/`

可用集合：
- `FreeBSD`: FreeBSD FTP 服务器的完整镜像。

英国
`rsync://rsync.mirrorservice.org/`

可用集合：
- `ftp.freebsd.org`: FreeBSD FTP 服务器的完整镜像。

美国
`rsync://ftp-master.FreeBSD.org/`
此服务器仅可供 FreeBSD 主镜像站点使用。

可用集合：
- `FreeBSD`: FreeBSD FTP 服务器的主归档。
- `acl`: FreeBSD 13.FreeBSD 主 ACL 列表。
`rsync://ftp13.FreeBSD.org/`
可用集合：
- `FreeBSD`: FreeBSD FTP 服务器的完整镜像。

## 附录 A. 获取 FreeBSD

## 附录 B. 参考文献

虽然手册页为 FreeBSD 操作系统的各个部分提供了权威参考，但它们很少说明如何将这些部分组合起来使整个操作系统顺畅运行。对于这一点，没有任何关于 UNIX® 系统管理的优秀书籍或用户手册可以替代。

### B.1. 针对 FreeBSD 的书籍

国际性书籍：
- 《Using FreeBSD》（繁体中文），由 Drmaster 出版，1997年。ISBN 9-578-39435-7。
- 《FreeBSD Unleashed》（简体中文译本），由机械出版社出版，ISBN 7-111-10201-0。
- 《FreeBSD From Scratch 第二版》（简体中文），由机械出版社出版。ISBN 7-111-10286-X。
- 《FreeBSD Handbook 第二版》（简体中文译本），由邮信出版。ISBN 7-115-10541-3。
- 《FreeBSD & Windows》（简体中文），由中国铁路出版社出版。ISBN 7-113-03845-X
- 《FreeBSD Internet Services HOWTO》（简体中文），由中国铁路出版社出版。ISBN 7-113-03423-3
- 《FreeBSD》（日文），由 CUTT 出版。ISBN 4-906391-22-2 C3055 P2400E。
- 《Complete Introduction to FreeBSD》（日文），由日本书社出版。ISBN 4-88135-473-6 P3600E。
- 《Personal UNIX Starter Kit FreeBSD》（日文），由 ASCII 出版。ISBN 4-7561-1733-3 P3800E。
- 《FreeBSD Handbook》（日文译本），由 ASCII 出版。ISBN 4-7561-1580-2 P3800E 3-932311-31。
- 《FreeBSD de Luxe》（德文），由 Verlag Industrie 出版，2003年。ISBN 3-8266-1343-0。
- 《FreeBSD Install and Utilization Manual》（日文），由每日通信出版有限公司，1998年。ISBN 4-8399-0112-0。
- 《FreeBSD 安装...》（印尼文），由 Elex Media 出版。1-15592-126-7。
- 《FreeBSD...》（繁体中文），由 GrandTech 出版，2003年。ISBN 9944-5。
- 《FreeBSD...》（中文），由 Drmaster 出版，2006年。ISBN 9-575-2。

英文书籍：
- 《Absolute FreeBSD 完整版》，由 Noarch Press 出版，2007年。ISBN 0-159327-1-5
- 《FreeBSD...》，由 O'Reilly 出版，2003年。ISBN 0-201-79940-5
- 《FreeBSD...》，由 Addison-Wesley 出版，2000年。ISBN 021144
- 《The C Programming Language 第二版》，由 PTR Prentice Hall 出版，1998年。ISBN 0-13-110362-8
- 《Porting UNIX Software》，由 O'Reilly, Inc. 出版，1995年。ISBN 1-56592-126-7
- 《The Standard C Library》，由 Prentice Hall 出版，1992年。ISBN 0-13-131509-9
- 《Code Reading: The Open Source Perspective》，由 Addison-Wesley 出版，2003年。ISBN 0-201-79940-5
- 《Code Quality: The Open Source Perspective》，由 Addison-Wesley 出版，2006年。ISBN 0-321-16607-8
- 《Advanced Programming in the UNIX Environment 第二版》，由 Addison-Wesley 出版，2005年。ISBN 0-201-43307-9
- 《UNIX Network Programming 第二版》，由 PTR Prentice Hall 出版，1998年。ISBN 0-13-490012-X

### B.2. 用户指南
- Ohio State University 提供了一份 HTML 格式的。
- 日本项目编写了 FreeBSD 用户文本文，由每日通信出版有限公司，1998年。ISBN 4-8399-0109-0 P3300。

### B.3. 管理员指南
- 日本项目编写了 FreeBSD 系统管理员指南（德文），由 Eyross 出版，2004年。ISBN 2-211

### B.4. 程序员指南
- Computer Systems Group, UC Berkeley，《4.4BSD 程序员手册》，由 O'Reilly & Associates 出版，1994年。ISBN 1-56592-078-3
- Computer Systems Group, UC Berkeley，《4.4BSD 程序员补充文档》，由 O'Reilly & Associates 出版，1994年。ISBN 1-56592-079-1
- Harbison, Samuel P. and Steele, Guy L. Jr. 《C: 参考手册》第四版，由 Prentice Hall 出版，1995年。ISBN 0-13-326224-3
- Kernighan, Brian and Dennis M Ritchie，《C语言语言》第二版，由 PTR Prentice Hall 出版，1988年。ISBN 0-13-110362-8
- Lehey, Greg，《Porting Software》，由 O'Reilly, Inc. 出版，1995年。ISBN 1-56592-126-7
- Plauger, P. J.Standard C Library》，由 Prentice Hall 出版，1992年。ISBN 0-13-131509-9
- Spinellis, Diomidis，《Code Reading: The Open Source Perspective》，由 Addison-Wesley 出版，2003年。ISBN 0-201-79940-5
- Spinellis, Diomidis，《Code Quality: The Open Source Perspective》，由 Addison-Wesley 出版，2006年。ISBN 0-321-16607-8
- Stevens, W. Richard and Stephen A. Rago，《Advanced Programming in the UNIX Environment 第二版》，由 Addison-Wesley 出版，2005年。ISBN 0-201-43307-9
- Stevens, W. Richard，《UNIX Network Programming 第二版》，由 PTR Prentice Hall 出版，1998年。ISBN 0-13-490012-X

### B.5. 操作系统内部机制
- Andleigh, Prabhat K.UNIX System Architecture》，由 Prentice-Hall, Inc. 出版，1990年。ISBN 0-13-949843-5
- Jolitz, William. 《将 UNIX 移植到 386》. Dr. Dobb's Journal. 1991年1月-1992年7月。
- Leffler, Samuel J., Marshall Kirk McKusick, Michael J Karels and John Quarterman. 《4.3BSD UNIX 操作系统的设计与实现》. Reading, Mass. : Addison-Wesley, 1989. ISBN 0-201-06196-1
- Leffler, Samuel J., Marshall Kirk McKusick. 《4.3BSD UNIX 操作系统的设计与实现：问答》. Reading, Mass. : Addison-Wesley, 1991. ISBN 0-201-54629-9
- McKusick, Marshall Kirk, Keith Bostic, Michael J Karels, and John Quarterman. 《4.4BSD 操作系统的设计与实现》. Reading, Mass. : Addison-Wesley, 1996. ISBN 0-201-54974-4
- Marshall Kirk McKusick, George V. Neil-Neil. 《FreeBSD 操作系统的设计与实现》. Boston, Mass. : Addison-Wesley, 2004. ISBN 0-201-70245-2
- Marshall Kirk McKusick, George V. Neil-Neil, Robert N. M. Watson. 《FreeBSD 操作系统的设计与实现》，第 2 版. : Westford, Mass. : Pearson Education, Inc., 2014. ISBN 0-321-96897-2
- Stevens, Richard. 《TCP/IP 图解：第 1 卷：协议》. Reading, Mass. : Addison-Wesley, 1996. ISBN 0-201-63346-9
- Schimmel, Curt. 《现代架构 Unix 系统》. Reading, Mass. : Addison-Wesley, 1994. ISBN 0-201-63338-8
- Stevens, W. Richard. 《TCP/IP 图解：第 3 卷：用于事务、HTTP、NNTP 和 UNIX 域协议的 TCP》. Reading, Mass. : Addison-Wesley, 1996. ISBN 0-201-63495-3
- Vahalia, Uresh. 《UNIX 内部：新前沿》. Prentice Hall, 1996. ISBN 0-13-101908-2
- Wright, Gary R. and W. Richard Stevens. 《TCP/IP 图解：第 2 卷：实现》. Reading, Mass. : Addison-Wesley, 1995. ISBN 0-201-63354-X

### B.6. 安全参考
- Cheswick, William and Steven M. Bellovin. 《防火墙与互联网安全：防御狡猾黑客》. Reading, Mass. : Addison-Wesley, 1995. ISBN 0-201-63357-4
- Garney, Simon. 《PGP 极好的隐私》. O'Reilly & Associates, Inc., 1995. ISBN 1-56592-098-8

### B.7. 硬件参考
- Anderson, Don and Tom Stanley. 《奔腾处理器系统架构》.第 2 版. Reading, Mass. : Addison-Wesley, 1995. ISBN 0-201-40992-2
- Ferraro, Richard F. 《程序员的 EGA、VGA 和 Super VGA 卡指南》.第 3 版. Reading, Mass. : Addison-Wesley, 1995. ISBN 0-201-62490-7
英特尔公司在其开发者网站上发布其 CPU、芯片组和标准的文档，通常以 PDF 文件形式存在。
- Shanley, Tom. 《80486 系统架构》.第 3 版. Reading, Mass. : Addison-Wesley, 1995. ISBN 0-201-40994-1
- Shanley, Tom. 《ISA 系统架构》.第 3 版. Reading, Mass. : Addison-Wesley, 1995. ISBN 0-201-40996-8
- Shanley, Tom. 《PCI 系统架构》.第 4 版. Reading, Mass. : Addison-Wesley, 1999. ISBN 0-201-30974-2
- Van Gulike, Frank. 《未公开的 PC》，第 2 版. Reading, Mass: Addison-Wesley Pub. Co., 1996. ISBN 0-201-47950-8

## 附录 B. 参考文献
- Messmer, Hans-Peter. 《不可缺的 PC 硬件书》，第 4 版. Reading, Mass : Addison-Wesley Pub. Co., 2002. ISBN 0-201-59616-4

### B.8. UNIX® 历史
- Lion, John. 《Unix 评 Unix》，第 6 版. 附带源码. ITP Media Group, 1996. ISBN 1573980137
- Raymond, Eric S. 《新黑客字典》，第 3 版. MIT Press, 1996. ISBN 0-262-6809-4
- Salus, Peter. 《Unix 的一个世纪》. Addison-Wesley, 1994.

## C.1. 网站

## C.2. 邮件列表

邮件列表是解决问题或向 FreeBSD 受众发起讨论的最直接方式。针对许多不同主题有各种列表。将问题发送到最合适的列表将确保获得更快、更准确的回复。

各种列表的章程位于本文底部。在加入或向任何列表发送邮件之前请阅读章程。大多数列表订阅者每天收到数百封邮件，章程和使用规则旨在保持列表的高信噪比。如果不这样做，邮件列表将无法作为项目的有效媒介。

注意：要测试向 FreeBSD 列表发送电子邮件的能力，请向 `freebsd-test` 发送测试消息。请勿向其他列表发送测试消息。

如果不确定将问题发布在哪个列表，请参见《如何从 FreeBSD-questions 邮件列表获得最佳结果》。

在向任何列表之前，通过阅读邮件列表常见问题（FAQ）文档了解如何更好地使用邮件列表，例如如何避免频繁的重复讨论。

所有列表都有存档，可以通过 FreeBSD 万维网服务器进行搜索。关键词搜索存档是寻找常见问题的绝佳方法，在发布问题之前应查阅存档。

### C.2.1. 列表摘要

通用列表：以下任何人都可以自由并鼓励加入的通用列表：

| 列表 | 目的 |
| :--- | :--- |
| freebsd-advocacy | FreeBSD 宣传 |
| freebsd-announce | 重要事件和项目里程碑（受审核） |
| freebsd-arch | 架构和设计讨论 |
| freebsd-bugbusters | 关于维护 FreeBSD 问题报告数据库及相关工具的讨论 |
| freebsd-bugs | Bug 报告 |
| freebsd-chat | 与 FreeBSD 社区相关的非技术项目 |
| freebsd-chromium | 针对 FreeBSD 的特定 Chromium 问题 |
| freebsd-current | 关于使用 FreeBSD-CURRENT 的讨论 |
| freebsd-isp | 使用 FreeBSD 的互联网服务提供商的问题 |
| freebsd-jobs | FreeBSD 的就业与咨询机会机 |
| freebsd-quarterly-calls | 季度状态报告的征集（已审核） |
| freebsd-questions | 用户提问与技术支持 |
| freebsd-security-notifications | 安全通知（已审核） |
| freebsd-stable | 关于使用 FreeBSD-STABLE 的讨论 |
| freebsd-test | 用于发送测试消息的地方，而不是实际的列表之一 |
| freebsd-women | FreeBSD 对女性的支持与倡议 |

技术列表：以下列表用于技术讨论。在加入或向这些列表发送邮件之前，请仔细阅读每个列表的章程，因为它们对使用和内容有严格的准则。

| 列表 | 目的 |
| :--- | :--- |
| freebsd-acpi | ACPI 和电源管理开发 |
| freebsd-amd64 | 将 FreeBSD 移植到 AMD64 系统（已审核） |
| freebsd-apache | 关于 Apache 相关端口移植的讨论 |
| freebsd-arm | 将 FreeBSD 移植到 ARM® 处理器 |
| freebsd-atm | 在 FreeBSD 中使用 ATM 网络 |
| freebsd-bluetooth | 在 FreeBSD 中使用蓝牙® 技术 |
| freebsd-cloud | 云平台上的 FreeBSD (EC2, GCE, Azure 等) |
| freebsd-cluster | 在集群环境中使用 FreeBSD |
| freebsd-database | 讨论 FreeBSD 下的数据库使用和开发 |
| freebsd-desktop | 在桌面上使用和改进 FreeBSD |
| dev-ci | 来自持续集成（CI）服务器的构建和测试报告 |
| dev-reviews | FreeBSD 审核系统的通知 |
| freebsd-doc | 创建 FreeBSD 相关的文档 |
| freebsd-drivers | 为 FreeBSD 编写设备驱动程序 |
| freebsd-dtrace | 在 FreeBSD 中使用和研究 DTrace |
| freebsd-eclipse | 使用 Eclipse IDE、工具、富客户端应用和端口的 FreeBSD 用户 |
| freebsd-elastic | FreeBSD FreeBSD 的 ElasticSearch 讨论 |
| freebsd-embedded | 在嵌入式应用中使用 FreeBSD |
| freebsd-col | 对 FreeBSD 项目不再支持的 FreeBSD 相关软件进行同伴支持 |
| freebsd-emulation | 其他系统的仿真，如 Linux/MS-DOS®/Windows® |
| freebsd-enlightenment | 移植 Enlightenment 和 Enlightenment 应用 |
| freebsd-erlang | FreeBSD FreeBSD 的 Erlang 讨论 |
| freebsd-rewire | FreeBSD FireWire® (iLink, IEEE 1394) 技术讨论 |
| freebsd-fortran | FreeBSD  Fortran |
| freebsd-fs | 文件系统 |
| freebsd-games | FreeBSD 游戏支持 |
| freebsd-gecko | Gecko 渲染引擎问题 |
| freebsd-geom | 针对 GEOM 的讨论和实现 |
| freebsd-git | FreeBSD 项目中 git 使用讨论 |
| freebsd-gnome | 移植 GNOME 和 GNOME 应用 |
| freebsd-hackers | 通用技术讨论 |
| freebsd-haskel | FreeBSD 特有的 Haskell 问题和讨论 |
| freebsd-hardware | 运行 FreeBSD 的硬件通用讨论 |
| freebsd-i18n | FreeBSD 国际化 |
| freebsd-infiniband | FreeBSD  Infiniband |
| freebsd-ipfw | 关于 IP 防火墙代码设计的的技术讨论 |
| freebsd-isdn | ISDN 开发者 |
| freebsd-jail | 关于 jail(8) 功能的讨论 |
| freebsd-java | Java™ 开发者以及将 JDK™ 移植到 FreeBSD 的人员 |
| freebsd-kde | 移植 KDE 和 KDE 应用 |
| freebsd-lfs | 将 LFS 移植到 FreeBSD |
| freebsd-mips | 将 FreeBSD 移植到 MIPS® |
| freebsd-mono | FreeBSD 上的 Mono 和 C# 应用 |
| freebsd-multimedia | 多媒体应用 |
| freebsd-new-bus | 关于总线架构的技术讨论 |
| freebsd-net | 网络讨论和 TCP/IP 源码 |
| freebsd-numerics | libm 函数高质量实现相关的讨论 |
| freebsd-ocaml | FreeBSD 特有的 OCaml 讨论 |
| freebsd-office | FreeBSD 上的办公应用 |
| freebsd-performance | 高性能/高负载安装的性能调优问题 |
| freebsd-perl | 若干 Perl 相关端口的维护 |
| freebsd-pf | 关于数据过滤防火墙系统的讨论和问题 |
| freebsd-pkg | 二进制包管理和包工具讨论 |
| freebsd-pkg-fallout | 软件包构建的 Fallout 日志 |
| freebsd-pkgbase | FreeBSD 系统的打包 |
| freebsd-platforms | 关于向非 Intel 架构平台的移植 |
| FreeBSD freebsd-ports | 端口集合（Ports Collection）的讨论 |
| freebsd-ports-announce | 关于端口集合的重要新闻和指令（已审核） |
| freebsd-ports-bugs | 端口 Bug/PR 的讨论 |
| freebsd-ppc | 将 FreeBSD 移植到 PowerPC |
| freebsd-proliant | ProLiant 平台上的 FreeBSD 技术讨论 |
| freebsd-python | FreeBSD 特有的 Python |
| freebsd-rc | 关于 rc.d 系统的讨论 |
| freebsd-realtime | 实时扩展开发 |
| freebsd-riscv | 将 FreeBSD 移植到 RIS-V |
| freebsd-ruby | FreeBSD 特有的 Ruby |
| freebsd-scsi | FreeBSD 子系统 |
| freebsd-snapshots | 快照公告 |
| freebsd-sparc64 | 将 FreeBSD 移植到 SPARC64 |
| freebsd-standards | FreeBSD C99 标准 |
| freebsd-sysinstall | sysinstall(8) 开发 |
| freebsd-tcltk | FreeBSD 特有的 Tcl/Tk |
| freebsd-testing | FreeBSD 的测试 |
| freebsd-threads | FreeBSD 中的线程 |
| freebsd-tilera | 将 FreeBSD 移植到 Tilera 系列 CPU |
| freebsd-tokenring | FreeBSD 令牌环支持 |
| freebsd-toolchain | 集成工具链维护 |
| freebsd-translators | 翻译器的 FreeBSD |
| freebsd-transport | 关于传输层协议的讨论 |
| freebsd-usb | FreeBSD 的 USB |
| freebsd-virtualization | FreeBSD 支持的虚拟化技术 |
| freebsd-vuxml | VuXML 基础设施 |
| freebsd-x11 | FreeBSD 上 X11 的维护和支持 |
| freebsd-xen | 关于 Xen 的实现和使用 |
| freebsd-xfce | FreeBSD 的 XFCE 及维护 |
| freebsd-zope | FreeBSD 的 Zope 及维护 |

## 附录 C. 上的资源

### 列表目的
- freebsd-hubs: 镜像站运行者（基础设施支持）
- freebsd-user-groups: 用户组协调
- freebsd-wip-status: FreeBSD 工作进展状态
- freebsd-wireless: 802.11 栈、工具、设备驱动开发

限制列表：上述列表针对更专业且要求更高的受众，可能对普通公众没有吸引。在加入这些限制列表之前，最好先在技术列表中建立联系，以了解涉及的通信情况。

摘要列表：上述所有列表均提供摘要格式。订阅某个列表后，可以在账户选项中更改摘要设置。

提交消息列表：以下列表适用于感兴趣查看源码树各个区域变更日志消息的人员。

注意：SVN 日志消息发送到 SVN 列表。

| 列表 | 区域描述（源自） |
| :--- | :--- |
| dev-commits-doc-all | `/usr/doc` 文档仓库的所有更改 |
| dev-commits-ports-all | `/usr/ports` 端口仓库的所有更改 |
| dev-commits-ports-main | `/usr/ports` 端口仓库主分支的所有更改 |
| dev-commits-ports-branches | `/usr/ports` 端口仓库季度分支的所有更改 |
| dev-commits-src-all | `/usr/src` 源码仓库的所有更改 |
| dev-commits-src-main | `/usr/src` 源码仓库主分支的所有更改（FreeBSD-CURRENT） |
| dev-commits-src-branches | `/usr/src` src 仓库中所有稳定分支的更改 |

SVN 列表：以下列表适用于感兴趣查看源码树不同区域更改 SVN 日志消息的人员。

注意
只有 SVN 日志消息会被发送到 SVN 列表。在 SVN 迁移到 Git 后，以下列表将不再接收新的提交消息。

| 列表名称 | 源区域 | 区域描述（来源） |
| :--- | :--- | :--- |
| svn-doc-all | `/usr/doc` | doc Subversion 仓库中所有分支的所有更改（用户、projects 和翻译外） |
| svn-doc-head | `/usr/doc` | doc Subversion 仓库“head”分支的所有更改 |
| svn-doc-projects | `/usr/doc/projects` | doc Subversion 仓库中 projects 区域的所有更改 |
| svn-doc-svnadmin | `/usr/doc` | doc Subversion 仓库管理脚本、钩子和其他配置数据的所有更改 |
| svn-ports-all | `/usr/ports` | ports Subversion 仓库的所有更改 |
| svn-ports-head | `/usr/ports` | ports Subversion 仓库“head”分支的所有更改 |
| svn-ports-svnadmin | `/usr/ports` | ports Subversion 仓库管理脚本、钩子和其他配置数据的所有更改 |
| svn-src-all | `/usr/src` | src Subversion 仓库的所有更改（用户和 projects 除外） |
| svn-src-head | `/usr/src` | src Subversion 仓库“head”分支的所有更改（FreeBSD-CURRENT 分支） |
| svn-src-projects | `/usr/projects` | src Subversion 仓库中 projects 区域的所有更改 |
| svn-src-release | `/usr/src` | src Subversion 仓库中 releases 区域的所有更改 |
| svn-src-releng | `/usr/src` | src Subversion 仓库 releng 分支的所有更改（安全/发布工程分支） |
| svn-src-stable | `/usr/src` | src Subversion 仓库中所有稳定分支的所有更改 |
| svn-src-stable-6 | `/usr/src` | src Subversion 仓库 stable/6 分支的所有更改 |
| svn-src-stable-7 | `/usr/src` | src Subversion 仓库 stable/7 分支的所有更改 |
| svn-src-stable-8 | `/usr/src` | src Subversion 仓库 stable/8 分支的所有更改 |
| svn-src-stable-9 | `/usr/src` | src Subversion 仓库 stable/9 分支的所有更改 |
| svn-src-stable-10 | `/usr/src` | src Subversion 仓库 stable/10 分支的所有更改 |
| svn-src-stable-11 | `/usr/src` | src Subversion 仓库 stable/11 分支的所有更改 |
| svn-src-stable-12 | `/usr/src` | src Subversion 仓库 stable/12 分支的所有更改 |
| svn-src-stable-other | `/usr/src` | src Subversion 仓库中较旧稳定分支的所有更改 |
| svn-src-svnadmin | `/usr/src` | src Subversion 仓库管理脚本、钩子和其他配置数据的所有更改 |
| svn-src-user | `/usr/src` | src Subversion 仓库实验 user 区域的所有更改 |
| svn-src-vendor | `/usr/src` | src Subversion 仓库 vendor 工作区域的所有更改 |

## C.2.2. 如何订阅

如需订阅列表，请点击 `http://lists.FreeBSD.org/mailman/listinfo` 中的列表名称。显示的页面应包含该列表所需的所有订阅说明。

如需实际向给定列表发布内容，请向 `<listname@FreeBSD.org>` 发送邮件。随后，该邮件将分发到全球邮件列表。

如需从列表中退订，请点击收到的该列表每封邮件底部的 URL。也可以通过向 `<listname-unsubscribe@FreeBSD.org>` 发送邮件来退订。

在技术邮件列表中保持讨论的技术性轨道上是非常重要的。如果只想接收重要公告，请加入 FreeBSD 公邮件列表，该列表专为低频率流量设计。

## C.2.3. 列表章程

所有 FreeBSD 邮件列表都有使用者必须遵守的某些基本规则。未能遵守这些准则将导致来自 FreeBSD Postmaster `<postmaster@FreeBSD.org>` 的两次（2）书面警告，第三次违规后，发布者将从 FreeBSD 邮件列表中移除并被过滤无法再次发布。我们很遗憾需要此类规则和措施，但今天的互联网似乎是一个严酷的环境，许多人并没有意识到某些东西是多么脆弱。

规则：
- 所有消息都应保持严格的技术性质。如果只想接收重要公告，请加入 FreeBSD 公邮件列表，该列表专为低频率流量设计。
- 严禁任何与 FreeBSD 无相关的产品或服务，如果是明显的垃圾邮件，将导致立即封禁。
- 过度的攻击或无关内容会损害邮件列表的价值。
- 不允许人身攻击和脏话。
- 不允许跨多个列表发布。
- 如果收到包含多个列表的邮件，回复前请修剪主题。
- 所有消息都应遵守列表章程。
- 设计问题应保持在适当的邮件列表中。
- 不容忍过度的攻击或攻击。

## C.2.4. 邮件列表过滤

FreeBSD 邮件列表通过多种方式进行过滤，以避免传播垃圾邮件、病毒和其他不需要的邮件。本节中描述的过滤操作不包括所有用于保护邮件列表的操作。邮件列表仅允许特定类型的附件。所有 MIME 内容类型不在下列表中的附件将在邮件发送到邮件列表之前被剥离。

- `application/octet-stream`
- `application/pdf`
- `application/pgp-signature`
- `application/x-pkcs7-signature`
- `message/rfc822`
- `multipart/alternative`
- `multipart/related`
- `multipart/signed`
- `text/html`
- `text/plain`
- `text/x-di`
- `text/x-patch`

注意：某些邮件列表可能允许其他 MIME 内容类型的附件，但上述列表适用于大多数邮件列表。

如果邮件同时包含 HTML 版本和纯文本版本，将移除 HTML 版本。如果邮件仅包含 HTML 版本，则会将其转换为纯文本。

### C.3. Usenet 新闻组

除了两个 FreeBSD 特有的新闻组外，还有许多其他新闻组在其中讨论了 FreeBSD，或者与 FreeBSD 用户其他相关。

### C.3.1. BSD 特有的新闻组
- `comp.unix.bsd.freebsd.announce`
- `comp.unix.bsd.freebsd.misc`
- `de.comp.os.unix.bsd`（德语）
- `fr.comp.os.bsd`（法语）

### C.3.2. 其他感兴趣的 UNIX® 新闻组
- `comp.unix`
- `comp.unix.questions`
- `comp.unix.admin`
- `comp.unix.programmer`
- `comp.unix.shell`
- `comp.unix.misc`
- `comp.unix.bsd`

### C.3.3. X Window 系统
- `comp.windows.x`

### C.4. 官方镜像

中央服务器，亚美尼亚、澳大利亚、奥地利、捷克、丹麦、芬兰、法国、德国、香港、爱尔兰、日本、拉脱维亚、立陶宛、荷兰、挪威、俄罗斯、斯洛文尼亚、南非、西班牙、瑞典、瑞士。台湾、英国、美国。（截至 UTC 时间）

- 中央服务器
- `https://www.Freebsd.org/`
- 亚美尼亚
- `http://www1.am.FreeBSD.org/` (IPv6)
- 澳大利亚
- `http://www.au.FreeBSD.org/`
- `http://www2.au.FreeBSD.org/`
- 奥地利
- `http://www.at.FreeBSD.org/` (IPv6)
- 捷克
- `http://www.cz.FreeBSD.org/` (IPv6)
- 丹麦
- `http://www.dk.FreeBSD.org/`
- 芬兰
- `http://www.fi.FreeBSD.org/`
- 法国
- `http://www.fr.FreeBSD.org/`
- 德国
- `http://www.de.FreeBSD.org/`
- 香港
- 爱尔兰
- `http://www.ie.FreeBSD.org/`
- 日本
- `http://www.jp.FreeBSD.org/` (IPv6)
- 拉脱维亚
- `http://www.lv.FreeBSD.org/`
- 立陶宛
- `http://www.lt.FreeBSD.org/`
- 荷兰
- `http://www.nl.FreeBSD.org/`
- 挪威
- `http://www.no.FreeBSD.org/`
- 俄罗斯
- `http://www.ru.FreeBSD.org/` (IPv6)
- 斯洛文尼亚
- `http://www.si.FreeBSD.org/`
- 南非
- `http://www.za.FreeBSD.org/`
- 西班牙
- `http://www.es.FreeBSD.org/`
- 瑞典
- `http://www.se.FreeBSD.org/`
- 瑞士
- `http://www.ch.FreeBSD.org/` (IPv6)
- 台湾
- `http://www.tw.FreeBSD.org/`
- 英国
- `http://www.uk.FreeBSD.org/`
- 美国
- `http://www.us.FreeBSD.org/` (IPv6)

## 附录 D 密钥

## 附录 D 密钥

## 附录 D 密钥

### 安全团队
- FreeBSD.org

```
CgkQPLLQ/MPWxmZAew//et/LToMVR3q6/qp/pf9ob/QwQ3MgejkC0DY3Md7JBRI/
6GFySynOVm5IoJofcv1hbhc/y3OZeTvK4s+BOQSNokYe34mCxZG4dypNaepQi
x0mLuJe/n4Y0p0LTLjGLVDKina2dM9HmlgYr4KumTum58g6gxs20ZD6z5ty0L
viU5xt3l3o0c3I9soHR2RN2sNHvXNW0eWjWlFxFeLJbk/x3UY1/kXCTymMzLau
S5L5012uOEEvaZr5iDKjy+wOxY4SUCNfY0gPMsej68CbbbWHOF2XCWytZsm6hnNb3
5TRGCbOSFTI9MXf5lpdqdzdijmimuFsl8LySk2juXxjll7uKDNN+NlfODIPMpg
rdH0BSyKci6UzNz/Upq3e+aISq68k+Hk1fKIJG1UcBrIJedhes29FCzj3hoyZ
VDmf6OL60lY0Y1/4GjIkYtzlPJmp8J7K3GweOUkfFihhYlbiMe7z+oIWEc7
0fNScrAGF/+JN3L6mjXKB6Pv+ER5ztzfpfuhBJ/j7AV5BaNmMDXAVO4aTphW7Dje
icenUGTpTk8Ugv5cMCj4QJaWdk/9sAcc0EFigPo68KjvegKg5R8jUP8e8T6
IljBtlclVhaRu2Elx/Yt2Apbm+GAMD8M0dQ7IYIsOFLZNBW92jgLLLLCTWDW+p1A=
=5gJ7
```

-----END PGP PUBLIC KEY BLOCK-----

## D.1.3. 核心团队秘书 <core-secretary@FreeBSD.org>

```
pub rsa4096/D8C8C83B49F26F17 2020-06-26 [SC] [expires: 2022-06-30]
密钥指纹 = 4B64E90BDE9B3EC0C6B5C66D8C8C3B49F26F17
uid FreeBSD 核心团队秘书 <core-secretary@freebsbd.org>
sub rsa4096/377C97356E4821B 2020-06-26 [E] [expires: 2022-06-30]
```

```
-----BEGIN PGP PUBLIC KEY BLOCK-----
```
