
# C 系统调用接口

**POSIX 程序员指南：编写可移植的 Unix 程序**
Lewine, Donald. O’Reilly，1992 年。ISBN 0-937175-73-0。607 页。

参见 [http://www.ora.com/catalog/posix/noframes](http://www.ora.com/catalog/posix/noframes)

一本关于 POSIX 1 标准的优秀程序员参考书。我更喜欢这本，而不是 JH 选择的那本。

**POSIX.1 标准：程序员指南**  Zlotnick, Fred. Benjamin/Cummings，1991 年。ISBN 0-8053-9605-5。379 页。$35.95。

JH：“当我抱怨 Linux 缺少第 2 卷 man 手册页时，有人告诉我只需去弄一本 POSIX 书，因为 Linux 就是这么做的。我喜欢这本书，因为我不是职业程序员，而作者提供了详尽的解释和示例。”

# 网络相关书籍

**Unix 网络编程**  Stevens, W. Richard. Prentice Hall，1990 年。ISBN 0-13-949876-1。772 页。$54。

涵盖了该主题你可能想要知道的一切，以及一些你可能并不想知道的内容（真的，XNS!?）。通常被认为在基础知识方面具有权威性，尽管它是 Web 出现之前的作品。

**Linux 网络管理员指南**  Kirch, Olaf. O’Reilly，1995 年。ISBN 1-56592-087-2。335 页。参见 [http://www.ora](http://www.ora)

一份关于 Linux 的 TCP/IP 及相关服务的实用指南。可在 Linux 文档项目（[http://Metalab.unc.edu/LDP/](http://Metalab.unc.edu/LDP/)）页面上通过 Web 访问，或直接访问 [http://Metalab.unc.edu/LDP/LDP/nag/nag.html](http://Metalab.unc.edu/LDP/LDP/nag/nag.html)。

**TCP/IP 网络管理**
Hunt, Craig, O'Reilly，1992 年。ISBN 0-937175-82-X。472 页。参见 `http://www.ora.com/catalog/tcp2/no_frames.html`。

相比 Kirch 的书，对 Linux 的特异性较少。深入涵盖了 TCP/IP 核心，包括路由和 BGP。

**DNS 和 BIND（第二版）**
Albitz, Paul, and Cricket Liu, O'Reilly，1996 年。ISBN 1-56592-236-0。438 页。$32.95。参见 `http://www.ora.com/catalog/dns2/no_frames.html`。

深入介绍了 DNS；对于运行复杂多子网安装的人很有用。涵盖了 BIND 库编程。

**Sendmail（第二版）**
Costales, Bryan, and Eric Allman. O'Reilly，1997 年。ISBN 1-56592-222-0。1,050 页。$32.95。参见 `http://www.ora.com/catalog/sendmail2/no_frames.html`。

一本详尽（且令人疲惫）的指南，介绍了 Linux 和 Unix 的默认邮件传输代理。

# Unix 内核实现书籍

在这里你可以找到关于 Linux 及其祖先和亲属的书籍。

## Linux 的祖先

**Unix 操作系统的设计**
Bach, Maurice J. Prentice-Hall. ISBN 0-13-201799-7。470 页。$60。

正是这本书开启了 Linux 的诞生。

**操作系统：设计与实现**
Tannenbaum, Andrew S. Prentice-Hall，1987 年。

Alan Cox（内核核心开发人员之一）喜欢这本书。Tannenbaum 设计了 Minix，这是 Linux 引导其发展起来的系统。

# Linux

**Linux 内核黑客指南**  Johnson, Michael K.

可在 Linux 文档项目页面（[http://MetaLab.unc.edu/LDP](http://MetaLab.unc.edu/LDP)）上通过 Web 访问，或直接访问 [http://www.redhat.com:8080/HyperNews/get/khg.html](http://www.redhat.com:8080/HyperNews/get/khg.html)。

**Linux 内核内幕（第二版）** Beck, Michael, Harold Bohme, Dżiedzka Clich, Ulrich Kuntz, Robert Magnus, Dick Verwormer. Addison-Wesley，1998 年。ISBN:0-201-33143-8。480 页。参见 [http://heg-school.awt.com/csen g/authors/beck.m/linux/linux.html](http://heg-school.awt.com/csen g/authors/beck.m/linux/linux.html)。

一份 Linux 内核编程指南；涵盖了 2.0 版本。

# Linux 的亲属

**4.4BSD Unix 操作系统的设计与实现** McKusick, Marshall Kirk, Keith Bostic, Michael J. Karels, and John S. Quarterman. Addison-Wesley，1996 年。ISBN 0-201-54979-4。608 页。参见 [http://heg-school.awt.com/csen g/authors/mckusick/4.4bsd/4.4bsd.html](http://heg-school.awt.com/csen g/authors/mckusick/4.4bsd/4.4bsd.html)。

这是关于 4.3BSD 内核实现的经典书籍的继任者，该书影响了 Linux 的设计（尤其是在套接字和网络方面）。本书涵盖了 BSD/OS、FreeBSD 和 NetBSD 的基础 4.4BSD。

**将 Unix 移植到 386 上** Jolitz, William F., and Lynne G. Jolitz. Dr. Dobb’s Journal（1991 年 1 月 – 1992 年 7 月）。

# Intel 处理器架构与编程书籍

**80386 程序员参考手册** Intel，1986 年。ISBN 1-55512-022-9。

第一部分：应用程序编程、数据类型、内存模型、指令集。第二部分：系统编程、架构、内存管理、保护、多任务、I/O、异常和中断、初始化、协处理和多处理。第三部分：兼容性（与早期 x86 机器）。第四部分：指令集。

**80386 系统软件编写者指南**	Intel，1987 年。ISBN 1-55512-023-7。

这解释了 386 的功能，面向操作系统编写者。它包含一章关于 Unix 实现的讨论。80386 架构的许多设计似乎都考虑到了 Multics；这些功能不被 DOS 或 Unix 使用。

**编程 80386**	Crawford, John H., Patrick P. Gelsinger. Sybex. ISBN 0-89588-581-3。774 页。$26.95。

这就是 Jolitz 夫妇在将 BSD 移植到 386 架构时使用的书。

**Pentium 处理器用户手册：第 3 卷，架构与编程手册**	Intel，1993 年。ISBN 1-55512-195-0。

基本上是上述 80386 程序员手册的 Pentium 版本。

# PC 级硬件书籍

![](img/a3584dae761d2e3abed8bf40d7637389_954_0.png)

**警告**
这些书已有四五年历史，可能已经过时。我其实也不太懂硬件...

**80386 硬件参考手册**	Intel，1986 年。ISBN 1-55512-024-5。

引脚连接、时序、波形、框图、电压，等等诸如此类的内容。

**不可或缺的 PC 硬件书**	Messmer, Hans-Peter. Addison-Wesley，1993 年。ISBN 0-201-62424-9。1,000 页。

JH：“涵盖了像 EIDE 和 PCI 等较新的内容。”

# 行政事项

本节包含本附录的使用条款及其历史。

# 使用条款

本文档版权归 Eric S. Raymond 所有 ©1997。您可以自由使用、传播和复制它，前提是您

- 不删除或更改此版权声明。
- 不删除或更改版本号和日期。
- 不删除或更改指向当前 WWW 版本的文档指针。
- 明确标记任何浓缩或修改过的版本。

这些限制旨在保护潜在的读者免受过时或损坏版本的侵害。如果您认为自己有正当理由例外，请询问我。

# 历史

这最初是由 Jim Haynes 维护的一个迷你 HOWTO。我稍微改变了侧重点，试图使其更像是一个独立文档，减少对各种 Usenet 参考文献条目的依赖。未署名的简短评论是我的，而不是他的。

# 附录 C

# Linux HOWTO 索引

“Linux HOWTO 索引”重印自 Linux HOWTO 索引，1999 年 3 月 28 日第 2.10.98 版，作者 Tim Bynum <linux-howto@metalab.unc.edu>。

本文档包含 Linux HOWTO 和迷你 HOWTO 的索引，以及关于 HOWTO 项目的其他信息。

# 什么是 Linux HOWTO？

Linux HOWTO 是详细描述配置或使用 Linux 某一方面内容的文档。例如，有安装 HOWTO，提供了安装 Linux 的说明；还有邮件 HOWTO，描述了如何在 Linux 下设置和配置邮件。其他示例包括 NET-5 HOWTO 和打印 HOWTO。

HOWTO 是综合性的文档——类似于 FAQ，但通常不是问答格式。然而，许多 HOWTO 在末尾包含一个 FAQ 部分。

有几种可用的 HOWTO 格式：纯文本、PostScript、DVI 和 HTML。

除了 HOWTO 之外，还有许多关于简短特定主题的迷你 HOWTO。它们仅提供纯文本和 HTML 格式。

# 哪里可以获得 Linux HOWTO？

可以通过匿名 FTP 从以下站点获取 HOWTO：

- `ftp://metalab.unc.edu/pub/Linux/docs/HOWTO`
- `ftp://tsx-11.mit.edu/pub/linux/docs/HOWTO`

还有许多镜像站点（参见 `ftp://metalab.unc.edu/pub/Linux/MIRRORS.html`）。

您还可以浏览 HTML 格式的 HOWTO（参见 `http://metalab.unc.edu/LDP/HOWTO/`）。许多镜像站点都镜像了 HTML 文件（参见 `http://metalab.unc.edu/LDP/hmirrors.html`）。

`metalab.unc.edu` 使用率很高，因此如果可能，请使用镜像站点。

HOWTO 通常在每月初发布到 Usenet 新闻组 `comp.os.linux.answers`。有一个名为 NewstoHOWTO 的工具可以汇编这些帖子（参见 `ftp://metalab.unc.edu/pub/Linux/system/news/misc/`）。

