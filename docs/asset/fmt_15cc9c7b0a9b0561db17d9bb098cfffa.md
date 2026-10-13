
| 1 物理 | 物理硬件规范 |

任何高于第 3 层或第 4 层的内容都只是一个表示网络对话中端点的整体或云。另一方面，系统管理员倾向于将互联网络的范围扩展到包括协议和上层服务组合，从而在协作系统之间实现有意义的互操作单元。例如，用于在平台“A”和平台“B”之间共享文件的协议和服务集合。只要能找到一组通用的受支持协议，通常就可以构建相应的软件服务集合，以促进即使在相当不同的操作系统之间也实现资源共享。进入“Samba”，它代表了这样一套软件服务，与标准协议如 `服务器消息块 (SMB)`、`通用互联网文件系统 (CIFS)`、`NetBIOS` 和 `传输控制协议 (TCP)` 协同工作，以互联 UNIX 和基于 Windows 的资源（图 1.1）。因此本书的标题：`Samba: UNIX 和 Windows 互联网络。`

![](img/7684008b1d7775727df27d44aed5b3f0_6_0.png)

图 1.1：UNIX、Windows 和 Samba

为什么我们要谈论 UNIX 和 MS Windows 互联网络？如今在大多数组织中发现 UNIX 和基于 Windows 的系统以好坏参半的方式共存已变得并不罕见。这可能看起来有点奇怪，因为这些操作系统是相当不同的开发历史和哲学（`表 1.2` 和 `表 1.3`）的产物。一个是从开放系统和标准角度驱动的，另一个代表了更专有的态度，专注于商业和个人使用需求。这并不是说随着时间的推移，每个操作系统都没有不得不解决所有这些问题以在市场上竞争。每个都有其自身的优势和劣势。这可能是为什么我们今天在大多数企业中看到这些平台结合的原因。一个在解决企业、学校甚至家庭中发现的复杂异构计算环境的需求方面互为补充。

无缝互联这两个世界的重要性已引起传统“仅限 UNIX”用户群如 USENIX 协会的关注。过去几年 USENIX 举办了专门针对 UNIX 和 Windows NT 集成的特别研讨会。USENIX `大型安装系统管理 (LISA)` 组织还举办了关于 UNIX 和 Windows 主题的会议。在大多数情况下，这些会议的出席率接近爆满。

### 表 1.2 UNIX 开发历史

| 年份 | 描述 |
|------|-------------|
| 1969 — | Thompson 在 DEC PDP-7 上开发单用户系统 |
| 1970 — | Kernighan 创造了 UNIX 的名称 |
| 1973 — | Ritchie 开发 C 语言<br>UNIX 用 C 重写 |
| 1974 — | ACM 发表了 Thompson 和 Ritchie 关于 UNIX 的论文 |
| 1975 — | Bell 实验室将 UNIX V6 授权给大学 |
| 1977 — | SCO 和 Interactive Systems 成立<br>Thompson & Joy 开发 BSD 1.0 |
| 1978 — | UNIX 第 7 版<br>BSD 2.0 |
| 1979 — | 伯克利 ARPAnet 合同<br>BSD 3.0 |
| 1980 — | BSD 4.0<br>Microsoft 开发 XENIX |
| 1981 — | SUN 成立 |
| 1982 — | AT&T System III<br>SUN 成为 Sun Microsystems |
| 1983 — | AT&T System V<br>BSD 4.2<br>SUN SunOS<br>Hewlett-Packard HP-UX<br>GNU 项目构想 |
| 1984 — | AT&T System V.2<br>DEC ULTRIX<br>X/Open 成立 |
| 1985 — | Sun NFS<br>POSIX 1003.1 发布 |
| 1986 — | AT&T SYSV.3, Streams, RFS<br>BSD 4.3<br>IBM AIX RT |

## 商业 UNIX 发布

1987 —

AT&T SYSV.3.1

1988 —

AT&T SYSV.3.2

BSD 4.3 Tahoe

1989 —

AT&T SYSV.4

开放软件基金会成立

OSF Motif

UNIX 国际组织成立

11 月 2 日互联网蠕虫

1990 —

BSD 4.3 Reno

IBM AIX RS/6000

OSF/1

1991 —

苹果、IBM、摩托罗拉合资企业

Sun Solaris 1.0

Linux 0.02

1992 —

BSD 4.4

1993 —

Novell 收购 UNIX System Laboratories

Novell 将 UNIX 商标授予 X/Open

386BSD 1.0

FreeBSD 1.0

NetBSD 0.8

1994 —

Linux 1.0

Linux 国际组织

1998 —

开源计划

UNIX 已存在约 30 年。最初主要出现在学术和研究环境中，它是一种功能强大的多用户、多任务操作系统，适用于各种应用。它可以轻松扩展，从小型单用户工作站到支持数千名同时用户和进程的非常大的大型机、多处理器和集群计算架构。由于源代码可用、内置编程环境以及对标准接口和协议的坚定关注，UNIX 可以轻松移植到大多数硬件平台。这导致了丰富的公共和厂商实现。尽管如此，源代码的通用访问也使 UNIX 在一定程度上保持厂商独立。当我们使用“UNIX”一词时，我们通常指的是市场上可用的全部公共和厂商版本。确实，每个 UNIX 版本往往都有其自身的细微差别、附加功能以及对基本主题的变体，但在其漫长的开发历史中，功能总体上在各平台间保持相当一致。事实上，这一庞大开发社区的集体专业知识极大地促进了操作系统的整体成熟度、互操作性和健壮性。

另一方面，关于 UNIX 最突出的抱怨指向其基于字符的命令行用户界面。尽管丰富的命令、解释性 shell 和脚本语言为程序员和系统管理员提供了大量功能，但其使用和存在对新手用户来说并不容易。大多数命令都是晦涩的缩写字符串，并且通常从调用它们的 shell 中获取上下文。这对除经验丰富的用户外的所有人来说都可能非常令人困惑。可以向操作系统添加名为 X Windows 的图形用户界面，但它并不能完全屏蔽用户免受命令行界面的复杂性。另一个批评是，尽管大多数应用程序可以在各种 UNIX 版本之间轻松移植，但它们通常在不同厂商平台之间不具备二进制兼容性。这往往限制了某些产品在所有 UNIX 平台上的可用性。

由于其开放接口和与互联网技术的紧密集成，UNIX 在许多企业中找到了立足之地。UNIX 和互联网一起成长。随着像 TCP/IP 这样的互联协议规范的开发，它们迅速融入了 UNIX 的网络结构。我们对互联网上基本信息共享服务所期望的大部分内容都是在 UNIX 下开发的。这使得 UNIX 能够作为协议和服务器瑞士军刀，快速且经济高效地将遗留的专有计算基础设施连接到互联网。

## 表 1.3 Windows 开发历史

| 年 | 事件 |
|------|--------|
| 1980 — | IBM 与微软签订 PC 操作系统合同<br>比尔·盖茨收购 QDOS<br>MS-DOS 由 QDOS 创建 |
| 1981 — | 首台 IBM PC<br>微软开始 "Interface Manager" 开发 |
| 1983 — | Windows 宣布<br>MS-DOS 2.0 |
| 1985 — | Windows 1.0<br>下拉菜单<br>鼠标支持 |
| 1987 — | Windows 2.0<br>图标和重叠窗口<br>微软与 IBM 开始 OS/2 工作<br>微软与 IBM 在 OS/2 和 Windows 开发上分道扬镳<br>Windows/386 |
| 1990 — | Windows 3.0<br>程序管理器和文件管理器<br>网络支持 |
| 1991 — | Windows 3.1<br>对象链接与嵌入 (OLE)<br>多媒体 |
| 1993 — | 微软开始 "New Technology" 操作系统工作 |
| 1994 — | Windows NT 3.1 32 位操作系统<br>保护模式<br>安全<br>Windows for Workgroups 3.11<br>Win32s |
| 1995 — | Windows 95<br>抢占式多任务<br>线程 |
| 1996 — | Windows NT 4.0<br>Windows CE<br>IBM 结束 OS/2 开发 |
| 1997 — | Windows 95 OSR2<br>活动桌面<br>FAT32<br>包含 Internet Explorer 3.0 |
| 1998 — | Windows 98<br>集成 Internet Explorer 4.0 |
| 1999 — | Windows 98 SE<br>Internet Explorer 5.0<br>Windows NT 5.0 更名为 Windows 2000<br>Windows 2000 Beta 3 发布候选版 1 |
