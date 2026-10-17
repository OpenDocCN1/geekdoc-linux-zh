
我们感谢以下人员，他们都阅读并评论了书的草稿：Eric Allman（Alias Research）、Mark Andrews（BSD开发者）、Mike Beede（Secure Computing Corporation）、Paul Borman（Hill Systems）、Ben Cottrell（NetBSD 项目）、Patrick Dea（La Salle University）、David Dyson（FreeBSD 项目）、Sean Eagan（Medius Systems）、Mike Fester（Silicon Graphics）、Gordon Hathaway（Auspex）、John Hongi（BSD Design）、Gordon Irlam（Cygnus Support）、Casimir Lesiak（NASA/Ames Research Center）、Gavin Lim（Sequent, UK）、Steve Lucco（Carnegie Mellon University）、Jan-Simon Pedro（命令行）、Arnold Robbins（Georgia理工学院）、Peter Salus（Unix历史学家）。

本书使用 James Clark 实现的 `pic`、`tbl`、`eqn` 和 `groff` 制作。索引由 Jon Bentley 和 Brian Kernaghan 编写的 `awk` 脚本生成 [Bentley & Kernaghan, 1986]。大部分艺术作品使用 `xfig` 创建。图片放置和孤行消除由 `groff` 处理，但偶数页底部消除是手工完成的。

我们鼓励读者对书中发现打印或其他错误发送建议或意见；请发送电子邮件至 dsbook-bugs@McKusik.COM。

# 关于作者

![](img/1f7d287e076fdb19873672db2d794e2f_15_0.png)

从左到右：Mike Karels, Keith Bostic, Kirk McKusick 和 John Quarterman 在圣地亚的一次 Usenix会议上首次聚首。

Marshall Kirk McKusick 编写书籍和文章，提供咨询并教授与UNIX和BSD相关的课程。在加州大学大学伯克利分校就读期间，他实现了4.2BSD快速文件系统，并担任伯克利计算机系统研究小组（CSRG）的研究计算机科学家，负责4.3BSD和4.4BSD的开发与发布。他特别感兴趣的领域是虚拟内存系统和文件系统。有一天，他希望看到它们被无缝合并。他在康奈尔大学获得电气工程学学士学位，在加州大学大学伯克利分校攻读研究生，获得计算机科学和工商管理硕士学位以及计算机科学博士学位。他曾任Usenix协会主席，也是ACM和IEEE的成员。在空闲时间，他喜欢游泳、潜水和收藏葡萄酒。这些葡萄酒储存在一个专门建造的酒窖中（可以通过 `http://wine.mckusick.com/cgi-bin/read` 访问，该酒窖位于他与Eric共同居住的地下室）。

Keith Bostic 是 Berkeley Software Design, Inc.的技术团队成员。他在CSRG工作了8年，监督了400多个可自由发布的Unix兼容工具的开发，并因使加州大学大学伯克利分校的4-BSD自由发布而获得该校1991年卓越成就奖。同时，他是PDP11版本的2.1BSD首席架构师，也是Berkeley日志结构文件系统和Berkeley数据库包（DB）的合著者。他还是广泛使用的 `nvi` 的作者。他在乔治华盛大学获得了统计学学士学位和电气工程硕士学位。他是ACM、IEEE以及多个POSIX工作组的成员。在空闲时间，他喜欢在南太平洋潜水、骑山地车，并研究Kirk和Eric专门建造的酒窖。他与妻子Margo Seltzer住在马萨诸塞州。

Michael J. Karels 是Berkeley Software Design, Inc.的系统架构师兼总裁。他在加州大学大学伯克利分校的CSRG工作了8年，担任4.3BSD的系统架构师。Karels在圣母大学获得了微生物学学士学位。在加州大学大学伯克利分校攻读分子生物研究生学位期间，他是PDP11版本2.9BSD Unix发布的首席开发人员。他是ACM、IEEE以及多个POSIX工作组的成员。他与妻子Teri Karels住在明尼苏达州的森林地区。

John S. Quarterman 是Texas Internet Consulting (TIC)的合伙人，提供网络和开放系统咨询，特别关注TCP/IP网络、Unix系统和标准。他是《矩阵：全球计算机网络与会议系统》（Digital Press, 1990）的作者，以及《UNIX、POSIX与开放系统：开放标准之谜》（1993）、《TCP/IP与Unix的实用互连》（1993）、《互联网连接：系统连接与配置》（1994）以及《电子邮件伴侣：通过互联网和其他全球网络进行有效通信》（1994）的合著者，这些书籍均由Addison-Wesley出版。他是……的编辑。

- 5.2 4.4BSD 虚拟内存系统概述 123
  - 内核映射与子映射 127
  - 内核内存分配 (Malloc) 129
  - 映射到对象 134
  - 从对象到页 137
  - Mmap 模型 139
  - 私有映射 142
  - 预留内核资源 147
  - 不通过拷贝创建新进程 149
  - 崩溃恢复 332
- 参考文献 334

# 第5部分 系统运行

- 设备探测 498

## 概述

## 历史与目标

### 1.1 UNIX 系统的历史

UNIX 系统已广泛使用了 20 多年，它帮助定义了许多计算领域。尽管许多机构对 UNIX 系统的开发做出了（并在持续做出）贡献，但本书将主要关注 BSD 开发支线：

- *发明了 UNIX 的贝尔实验室*
- *加州大学伯伯克利分校的计算机系统研究小组 (CSRG)，它为 UNIX 提供了虚拟内存和 TCP/IP 的参考实现*
- *Berkeley Software Design, Incorporated (BSDI)、FreeBSD 项目和 NetBSD 项目，它们继续了 CSRG 开始的工作*

### 起源

UNIX 系统的第一个版本是由肯·汤普森（Ken Thompson）于 1969 年在贝尔实验室开发的，起初作为一个私人研究项目，用于利用一台闲置的 PDP-7。不久后，丹尼斯·里奇（Dennis Ritchie）加入了他，他不仅为系统的设计和实现做出了贡献，还发明了 C 语言。该系统完全用 C 语言重写，几乎没有留下汇编语言。系统的原始设计 [Ritchie, 1978] 以及过去 15 年的发展 [Ritchie, 1984a; Compton, 1985] 使得 UNIX 系统成为一个重要且强大的操作系统 [Ritchie, 1987]。

里奇、汤普森以及贝尔实验室的其他早期 UNIX 开发者此前参与过 Multics 项目 [Peirce, 1985; Organick, 1975]，该项目对这个新的操作系统产生了深远影响。甚至 UNIX 这个名字仅仅是对 Multics 的一个双关语；在 Multics 试图完成许多任务的领域，UNIX 则试图将某一项任务做好。UNIX 文件系统的基本结构、使用用户进程作为命令解释器的想法、文件接口的通用结构以及许多其他系统特性都直接源自 Multics。

同时也吸收了其他操作系统的思想，例如麻省理工学院（MIT）的 CTSS。创建新进程的 `fork` 操作源自伯克利的 GENIE (SDS-940) 操作系统。它允许用户通过每个命令使用一个进程来廉价地创建进程，而不是像 Multics 那样将命令作为过程运行。

UNIX 系统至少有三条发展路线。图 1.2（见第 6 页）勾勒了它们最近的发展，特别是通 4-BSD 和 System V 的分支 [Chambers & Quarterman, 1983; Udniewski, 1985]。给出的日期是近似值，我们没有尝试显示所有的包含项。图中列出的某些系统在文中未提及，但包含它们是为了更清楚地展示我们所研究系统之间的关系。

### 研究 UNIX

UNIX 的早期版本是贝尔实验室的研究系统（Research systems）。除了系统的最早版本外，这些系统还包括 UNIX 时间共享系统第六版（通常称为 V6），它是 1976 年第一个在贝尔实验室之外被广泛使用的版本。系统通过发行时现行的《UNIX 程序员手册》中的版本号来标识。

UNIX 系统在三个重要方面与其他操作系统区分开来：

1. UNIX 系统是用高级语言编写的。
2. UNIX 系统以源码形式分发。
3. UNIX 系统提供了强大的原语，这些原语通常只在更昂贵硬件上的操作系统中才能存在。
