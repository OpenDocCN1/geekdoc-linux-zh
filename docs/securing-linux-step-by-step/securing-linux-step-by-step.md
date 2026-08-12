# LINUX 安全分步指南







![](img/0aaa698c422b2f7ffe93bff50cbbef96_0_0.png)



# 引言

![](img/0aaa698c422b2f7ffe93bff50cbbef96_1_0.png)

计算机专业人士社区生产力和效率的巨大来源之一，是活跃从业者愿意从忙碌生活中抽出时间，分享他们学到的教训和完善的技术。许多共享通过在线新闻组、网页发布以及技术会议上的演讲进行，那些有时间浏览新闻组、浏览网络和参加会议的人，往往能从这些互动中获得无价的信息。

SANS 的“分步”系列将信息共享提升到了一个新的水平，专家们在此分享他们认为有效的技术。SANS 学院将这些技术整合到一个分步计划中，并让其他专家对该计划进行详细的严格审查。这一过程持续到达成共识。这是一项艰巨的任务。许多人花费大量时间确保信息既有用又准确。

## Linux 安全
分步指南版本 1.0

Linux 从一个由赫尔辛基大学学生林·托瓦尔斯（Lin Torvalds）领导的小型协作项目，已发展变成一种全球现象，推动了发行、培训和支持的新行业出现。除了 Windows NT 之外，它是唯一在企业信息技术基础设施中获得市场份额的操作系统。分发商正积极营销更易安装、更易用的 Linux 系统，并真正进入了企业、政府和教育用户的桌面。根据估计，全球实际有 800 万 Linux 用户。

Linux 是一个“开源”操作系统。内核和系统程序的源代码供下载、检查和修改。这是一把双刃剑：系统开发者和普通用户可以访问代码，因此能更快修复漏洞；系统破解者也可以访问代码，他们可以利用这些知识更快速、可靠地开发漏洞。这并没有让 Linux 比它的专有竞争对手更安全。相反，漏洞在开放环境中被发现，Linux 软件也会很快发布补丁和更新。遗憾的是，大多数用户从 CD-ROM 介质安装 Linux，而等到标签上的墨水干透，里面通常已经包含了漏洞程序。安装商业 Linux 发行版的另一个遗憾方面是，为了方便使用，这些 Linux 系统被配置为计算机启动后立即运行大部分（甚至全部）网络服务，且没有任何控制。例如，多年来所有 Linux 发行版都带有 TCP 封装，但 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件是空的，这意味着在互联网上无法连接到受 TCP 封装的服务。

本指南面向新手家庭用户和经验丰富的系统管理员。它涵盖了 Linux 在两种基本运行模式下的安装和操作：作为工作站和作为服务器。它没有配置 Linux 执行的性能良好的其他特殊功能，例如路由器、防火墙、防火墙处理等。示例和指令基于 Red Hat (红帽) 6.0 版本。选择 Red Hat 是因为它拥有最大的 Linux 份额，而选择 6.0 版本是因为它包含了最新的稳定版 Linux 内核、系统库、实用等。然而，本指南中的概念、建议和程序可以很容易转换到其他发行版。你可能需要稍微探索你的系统，以找到不同目录下的配置文件，并确定安装了哪些版本的软件包，但探索过程本身就是一个很好的教学工具。

本指南将引导你（读者）完成安装过程，然后分为设置工作站和设置服务器的独立步骤。指南讨论了用于监控和测试系统安全的一些有用工具。我们努力遵循“深度防御”原则。没有任何一个步骤是针对系统攻击的“灵银弹”，但作为一个整体来看，它们构建了多层防御，这让“脚本小子”（script kiddies）和专职的计算机犯罪分子的生活变得困难得多。

![](img/0aaa698c422b2f7ffe93bff50cbbef96_2_0.png)

## Linux 安全

# 引言

我们尽可能解释加固 Linux 机器的选项及其影响。然而，这并不是一本关于安全的书。在可能的情况下，我们在正文或附录 A 中包含了指向文档和资源的指引。我们鼓励你在设置 Linux 机器之前学习这些资源，并跟踪来自分发商、SANS 学院和其他安全参考的最新信息。

按照惯例，root 用户执行的命令前带有命令行提示符 `[root]#`。在系统正文中，命令和文件名使用 Courier 等宽字体。命令序列和文件内容与正文分开，也使用 Courier 等宽字体。参考手册采用传统样式，页码（节），例如 `inetdconf(5)`。若要在 Red Linux 以及大多数其他发行版中阅读手册，请执行命令：

```bash
[root]# man 5 inetd
```

**重要提示：** 每当这些步骤需要更改时，都会建议进行更新，并定期发布新版本。

本书由以下人员编写和编辑：
Lee E. Brotzman, David A. Rauch, Trinity Designs

| SANS 学院热烈感谢专业人士的工作及其使用的技术 | Robin Felix, Luther Technologies, Bangalore | Stephen Northcott, SANS Institute |
| --- | --- | --- |
| 以及他们使用的技术 | William James Hudson, Robert Mann | David Ottheimer, Data Services |
| Tyler J. Allison, Awerpoint Communications | Det. Ted Iesen, Seattle Police Department | Jane Pirtoni, Business Communications. |
| Ofer Arkin, Linuxpower.com | Roy Kidder, Corecom | Jesse E. Pollett, II, Logical Information Systems |
| Scott Barry, MostlyLinux, Inc. | Alexander Kouzeikis, Bit Net Services | Patrick O. Gray, Ramirez, Plotter Network Services |
| Marion Bion, Geotechnics Inc. | Chet Kress, Apex-Communications | David Renner, SERVERTECH Inc. |
| Daniel T. Air Force Laboratory, Research Site, | Leon E. Hull, University of Illinois at Urbana-Champaign | Andy Rudy, Concept Computing |
| Information Assurance Office | | |
| | | | |
| David Bradley, Stanford University Security Team | Jonathan Lasher, University of Maryland, Baltimore County (UMBC) | David Saunders, University of Virginia |
| Richard Casey, Science Applications Corporation | Bill Lavnette, Network Recovery Systems | Kurt Sefried, SecurityPortal.com and sefried.org |
| Ian C. Campbell, State University of New York at Albany | Manuel Lopez, Universidad de Baja California | J. J. Harold, Sertlio, Ltd. |
| John Coleman, Yale University Library Systems | Chandrashek Marathi, Luther Technologies | Andres and J Silva, III, Collective Technologies |
| Andrew Cormack, JANT-CERT | Rose Malnason | Dev Commel, Software Engineering Inc, Carnegie |
| Patrick Graham, Athens Regional Medical Center | Mike Carney, Robins Air Force Base | Miller University |
| Clement DuBois, UniGlobal, Montreal Canada | John E. Miller, Jr., Intermeec Communications | Len Smith, University of Chicago of CSE |
| John F. Feast, National Warfare Center | Shane B. Miller, Science Systems and Applications, Inc. | Robert Thomas, U.S. Census Bureau |
| | P. Larry Netelson, University of Illinois at Urbana-Champaign | Bob Todd, Advanced Research Corporation |

![](img/0aaa698c422b2f7ffe93bff50cbbef96_3_0.png)










# 第二步：安装 Linux



- 2.3.3 步骤：记录分区方案。






# 2.7 步骤：设置系统访问安全策略。



# 第三步：加固工作站网络配置

# 3.1 步骤：禁用 Internet 守护进程服务。


# 3.2 步骤：使用 TCP Wrappers 控制对剩余 INET 服务的访问。


# 3.3 步骤：禁用未使用的网络服务。


# 3.4 步骤：获取软件最新版本。




- 3.6 步骤：电子邮件 ........................................................................................... 33
- 3.7.1 步骤：关闭 NFS 守护进程 ............................................................................ 35
- 3.7.2 步骤：配置 NFS 挂载 ............................................................................ 35

# 第四步：加固服务器配置


- 4.3.3.3 步骤：拷贝配置文件和程序 ................................................

- 4.4 步骤：电子邮件 ............................................................
- 4.4.5.6 步骤：为安全的 POP/IMAP 连接安装 SSL 封装器 ...................

- 4.5.1 步骤：在 `/etc/losts.lpd` 中列出远程主机 ........................







## 步骤 4.7：服务器消息块 (SMB) SAMBA 服务器 ................................................................ 56


## 步骤 4.8：中央 syslog 主机 ................................................................................................ 58


## 步骤 4.9：文件传输协议 (FTP) ............................................................................ 59


## 步骤 4.10：超文本传输协议 (HTTP) 服务器 ................................................... 61

## 步骤 5 调优与包防火墙 ........................................................ 64

## 步骤 5.1：内核：关于配置、重新编译和安装新内核的思考 .65

## 步骤 5.2：系统优化 ................................................................... 66

- 步骤 5.2.1. TCP/IP 接收窗口大小 .......................................... 66

## 步骤 5.3：包防火墙与 Linux IP 伪装

- 步骤 5.3.1. 通过 IP 伪装从外部连接获取更多收益 . . 67
- 步骤 5.3.2. 强大的 etc/dr/rc.firewall 规则集 . . . . 67

## 步骤 6 工具

## 步骤 6.1：基于主机的监控与入侵检测


## 步骤 6.2：基于主机的漏洞分析：从内向外看


## 步骤 6.3：基于网络的漏洞分析：从外向内




## 步骤 1
### 安装之前

### 步骤 1.1 确定安全需求

任何操作系统上的系统安全都需要预先考虑。具有安全意识的家庭用户和企业在安装之前，都需要确定以下内容：

1. 你正试图保护什么？机密数据（医疗记录、信用卡号等）、对基本服务的访问（DNS、邮件等）、计算资源（用户 shell 账户、软件开发工具等）。

2. 在安全措施的成本超过受保护原始数据和/或服务的价值之前，应该实施安全到何种程度？

你需要确定这台机器的主要用途。一旦确定，请尽量坚持你的原始计划。本指南涵盖的两个主要用途是：

1. 工作站：X-Windows、网络浏览器、电子邮件、文字处理、电子表格、数据库等用户应用程序。工作站不需要提供 TELNET、FTP、HTTP 等服务。这些服务应该关闭或完全移除。

2. 服务器：无 X-Windows，运行如 NFS、Samba、HTTP、FTP、SMTP、DNS、shell 账户、防火墙等网络服务。

服务器应配置为尽可能运行尽可能少的服务。这将为管理员提供更好的安全性、容错能力以及根据所需服务扩展性能的能力。然而，必须考虑额外的硬件和管理成本。

## 步骤 1.1 定义安全策略

这一步主要针对安全专业人员和企业 IT 经理，但对关注安全的私有用户也很有帮助。企业和政府组织需要制定、记录并执行策略。该策略应适用于内部和外部用户。用户应通过书面交流了解该策略。拥有良好记录策略的主要原因是，当安全违规或滥用发生时，你拥有具有法律约束力的文件。如果没有策略和相应的文档，策略的执行可能会面临挑战。





### 步骤 1.3.3. 设置 BIOS 密码

设置 BIOS 密码以确保恶意用户无法更改系统的 CMOS 设置。使用包含大写字母、小写字母和数字的密码。选择强密码的建议请参见下文步骤 2.5。互联网上有很多 BIOS 破解程序，因此不要在 BIOS 设置中使用相同的密码来保护 LILO（步骤 2.6.3）或 Linux 操作系统中的 root 或用户账户（步骤 2.5.2）。

### 步骤 1.3.4. SCSI BIOS 设置

某些 SCSI 控制器拥有自己的 BIOS。例如，Adaptec 控制器使用 Control-A 键盘序列进入 SCSI BIOS 提示。请确保你已禁用了从 CD-ROM 等其他介质启动的能力。对于 Adaptec SCSI BIOS 的最新版本，目前没有办法对 SCSI BIOS 设置进行密码保护。因此，如果用户可以重启电脑、进入 SCSI BIOS 并启用 CD-ROM 启动，唯一阻止其进入你系统的办法就是锁定的 CD-ROM 物理机匣。

### 步骤 1.3.5. 记录 BIOS 设置

记录硬件和软件支持所需的 BIOS 设置。在发生故障或管理员缺席的情况下，硬件驱动器几何结构、任何非默认系统设置等的文档将记录该系统的初始设置。将此文档与其他硬件手册一起存放在安全的地方。

一旦明确了你的需求并记录了安全策略，就是安装 Linux 操作系统系统的时候了。Linux 提供了多种发行版可供选择，每种发行版都有特定的优缺点。虽然这超出了本文的范围，但我们强烈建议你仔细考虑所选择的 Linux 发行版，因为这将影响未来的管理和易用性。对于本指南，我们主要选择 Red Hat 6.0，是因为由于 Red Hat 的市场份额以及我们尽可能覆盖更多用户的目标。如果你打算使用其他发行版或更早版本的 Red Hat，你应该意识到系统管理和安全相关配置的差异。例如，旧版本的 Red Hat 默认不使用密码，系统文件可能位于不同的目录，Slackware 不使用 SYSV init 启动等。无论你选择哪种发行版，都应升级到最新版本，以获得更好的安全性、功能和性能的所有优势。

## 步骤 2 安装 Linux

### 步骤 2.1 断开机器的网络连接

大多数 Linux 发行版在安装期间都会启动网络接口，尽管此时系统的安全防护非常有限。鉴于此，最佳的安全实践是在开始安装之前断开网卡。如果你是从网络服务器安装，请确保在安装运行期间你使用的网络是安全的。如果你是从互联网上的公共 FTP 站点安装，请务必小心，因为你的系统可能在你意识到之前就被攻破解了。

### 步骤 2.2 选择安装类型：工作站、服务器或自定义

Red Hat 安装程序允许从这三个选项中选择其一。“工作站（Workstation）”和“服务器（Server）”选择根据硬盘总大小的百分比对系统硬盘进行自动分区。此外，这两个设置会安装许多你或你的用户可能永远不会使用的软件包包。使用“自定义（Custom）”安装选项可以对安装过程获得最大的控制权，无论你是在设置工作站还是服务器。

### 步骤 2.3 定义分区

分区是 UNIX 管理员之间一个相当具有宗教色彩的辩题。为什么呢？理论认为，系统拥有的分区越多，可靠性就越高。例如，如果某个分区损坏或拒绝服务攻击由于分区日志消息而失败，问题将仅隔离在该特定分区中。

人们通常认为 Linux 工作站只需要三个分区：根分区 `/`；家分区 `/home`；以及用于虚拟内存的交换分区（swap）。服务器的分区取决于服务的类型。确定交换分区大小的通用规则是分配物理内存的两倍。……（此处省略重复内容，保持翻译逻辑）如果你打算使用其他发行版或更早版本的 Red Hat，你应该意识到系统管理和安全相关配置的差异。例如，旧版本的 Red Hat 默认不使用密码，系统文件可能位于不同的目录，Slackware 不使用 SYSV init 启动等。无论你选择哪种发行版，都应升级到最新版本，以获得更好的安全性、功能和性能的所有优势。

（注：由于原文文本中存在大量重复的段落，译文已根据指令“不要重复输出原文”的原则，对核心逻辑进行了整合和翻译。）




Syslog: 集中式日志主机存储来自其他计算机的 syslog 消息。你可以想象，日志主机需要大量的磁盘空间来存放 `/var/log`。良好的做法是将 `/var/log` 放在一个快速的 SCSI 设备上。日志主机不应运行任何服务，并且要安全，这样系统所需的磁盘空间会比其他服务器小。

Shell: Unix 服务器提供了 `/tmp` 和 `/var` 的独立分区。这将减少由于经典攻击填充 `/tmp` 目录，导致根分区满，使得系统无法写入更多文件并通常会崩溃的影响。

我们建议服务器为 `/var`（或者 `/var` 和 `/var/spool` 的独立分区）、根分区 `/` 以及用户分区 `/home` 准备独立分区。某些管理员可能还会为 `/usr` 考虑一个分区。某些发行版将大型系统软件包（如 KDE、Netscape 和 DBMS）存储在 `/opt` 目录，这些分区的相对大小完全取决于管理员的需求和个人经验。例如：一台拥有 256MB 内存和 2GB 硬盘的高端 PC 主要用于 NNTP 服务，可以分区如下：

| 第一块硬盘 | | 大小 |
| :--- | :--- | :--- |
| 第一块硬盘 | | 500MB |
| 第一块硬盘 | `/usr` | 100MB |
| 第一块硬盘 | `/usr/local` | 1500MB |
| 第一块硬盘 | `/tmp` | 2000MB |
| 第一块硬盘 | `/var/spool/news` | 4000MB |
| 第二块硬盘 | `swap` | 500MB |
| 第二块硬盘 | `/home` | 5500MB |
| 第二块硬盘 | `var` | 3000MB |

##  2 安装 Linux

### 步骤 2.3.3. 记录分区方案

一旦为特定环境完成分区，请记录分区布局。这样，如果分区表意外损坏或删除，恢复它将变得更容易。要记录各种表，请在每个物理磁盘（sda, sda 等）上运行 `fdisk` 并输入 `p` 打印。将结果记录在纸上并存在安全的地方以备后参考。例如：

```
[root]# fdisk /dev/hda
Using /dev/hda as default device:
Command (m for help): p
Disk /hda: 255 heads, 63 sectors, 2193 cylinders
Units = 16065 * 512 bytes
```

| 设备 | 启动 | 开始 | 结束 | 扇区 | Id | 系统 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda | * | | 1913 | 156611 | 83 | Linux |
| /dev/hda2 | | 1914 | 1946 | 265072+ | 82 | Linux swap |
| /dev/hda3 | | 1947 | 2193 | 1984027+ | 83 | Linux |

```
Command (m for help): q
```

## 2.4 选择安装软件包

与设置磁盘分区一样，选择安装的软件包取决于系统的用途。通过此部分的最佳方法是了解你的用户以及系统将如何被使用。确定系统中将包含和不包含的内容，并相应地选择软件包。仔细检查安装程序的每个部分，每当你不知道某个软件包是什么，或者不确定是否需要它时，按下“F”。如有疑问，就跳过它。当需要出现时，以后添加该软件包。如果你没有选择 Red Hat 某些工具所需的软件包，它会在安装过程实际开始之前警告任何软件依赖关系。

![](img/0aaa698c422b2f7ffe93bff50cbbef96_18_0.png)

### 步骤 2.4.1. 工作站软件包

工作站用户通常分为三类之一：

- 1. 商务。系统用于文字处理、电子表格、电子邮件和 WWW 浏览等业务目的。对于这些系统，不需要安装 NFS 或 HTTP 服务器，或像 GCC 和 EGCS 这样的编译器。
- 2. 软件开发。对于此类系统，软件包的选择取决于开发类型。Web 开发人员可能需要 Web 服务器、PHP、Perl。软件开发者可能需要 GCC 或 EGCS、G++、Python、Perl 等，以及 TeX 和 Ghostscript 等文档工具。
- 3. 通用。这一类可能符合大多数用户的需求。商务工具、开发工具、多媒体播放器、游戏、图形实用程序都加载在系统中。通用型用户不希望受限于未在机器上安装 Web 服务器或 GCC 的事实。虽然这种安装最为灵活，但以后需要时很容易添加软件包。

### 步骤 2.4.2. 服务器软件包

服务器配置为性能和安全。为了提高安全性，我们建议在服务器上只安装必要的软件包。例如，一个 Web 服务器需要 Web 服务器、PHP、Perl。如果允许，不要在系统上运行不必要的服务如NFS、Samba、图形实用程序等，以减少攻击面。

### 步骤 2.4.3. 让安装程序进行

一旦你选择了所有必要的软件包，Red Hat 安装程序将确定软件包之间的依赖关系。在这一点上，你可以从列表中移除所选的软件包。

最后，安装程序将提示你进行网卡等额外设置。涵盖这些步骤超出了本指南的范围。

## 2.5 配置系统安全和策略

### 步骤 2.5.1. 使用 MD5 哈希的影子密码

Red Hat 向用户提示的最终安装选项之一是使用带有或不带 MD5 哈希的“影子”密码。传统的 UNIX 用户密码使用“crypt”算法加密并存储在全局可读的文件 `/etc/passwd` 中。这使得使用工具进行字典攻击很容易。影子密码存储在 `/etc/shadow`，仅 root 可读，使得获取加密密码变得困难得多。使用 MD5 加密哈希为影子密码增加另一层安全。保持 `/etc/shadow` 安全非常重要。

### 步骤 2.5.2. 为 root 和所有用户设置密码

系统重启之前的最后步骤之一是设置 root 密码。Linux 密码是敏感的，安装程序建议 root 密码是大小写字母、数字和特殊字符的组合，包括：

```
[ ~!#$%^&*()-_={}]|\;':.<>? ]
```

密码不基于任何个人信息，如姓名、公司、社会安全号码、生日、车牌号等。由于攻击者可以发现关于用户的惊人个人信息，特别是在内部攻击的情况下。

永远不要使用任何语言的字典中都能找到的常用词，例如英语单词“ridge”。使用数字替换字母（例如“r1dg3”）没有帮助，因为常见的密码破解工具也考虑了这种技巧。

那么什么是好密码呢？独特且使用组合；想一个短语和缩写（尽管不要使用你日常用语的缩写）。例如，一个好密码可以用 B+ 树和 Patricia 树的计算机科学算法名称构造，“B+paTas..”。要有创意，但要使用你能记得住的东西！




### 步骤 2.6 最后的 LINUX 安装建议

### 步骤 2.6.1. 创建启动软盘

许多 Linux 用户跳过的一个步骤是创建应急启动软盘。Red Hat 安装程序会创建一个包含 Linux 内核的可启动软盘，该内核包含了对你计算机上所有特定硬件和配置的支持。虽然创建启动盘并非强制步骤，但当系统最终发生紧急情况时，你会庆幸自己之前创建了它。请确保启动软盘已正确标记，并妥存放在安全的地方，例如计算机机房的磁带柜或锁好的办公桌抽屉。

尽管我们强烈建议你**现在**创建应急软盘，但如果你决定稍后再做，在 Red Hat Linux 中，脚本 `/sbin/mkbootdisk` 将为你创建磁盘。更多信息请参见 mkbootdisk(8) 页面。

### 步骤 2.6.2. 收紧 /etc/inittab 中的设置

`/etc/inittab` 定义了 SYSV init 进程（进程号 1）的启动行为（关于 SYSV init 启动脚本的更多信息请参见步骤 3.3）。使用 `/etc/inittab` 可以禁用通过“Control + Alt + Del”键序列从控制台重启，并要求进入单用户模式时输入 root 密码。

要禁用“Control + Alt + Del”键序列，请修改 `/etc/inittab` 文件中的以下行：

```
ca::ctrlaltdel:/sbin/shutdown -t3 -r now
```

修改为：

```
#ca::ctrlaltdel:/sbin/shutdown -t3 -r now
```

要要求在进入单用户模式时输入 root 密码，请在 `/etc/inittab` 的 `si::sysint:::` 条目后添加以下行：

```
~:S:wait:/sbin/login
```

要使这些更改立即生效，输入以下命令：

```
[root]# init q
```

## 步骤 2 安装 Linux

### 步骤 2.6.3. 为 LILO 启动设置密码保护

Linux Loader (LILO) 是启动 Linux 的主要机制。如果无法保证 Linux 机器的安全，除了要求进入单用户模式需要 root 密码外，还要对 LILO 提示进行密码保护。注意，对 LILO 提示进行密码保护可能会干扰系统在断电或系统崩溃后的自动重启。受控机房环境中的关键任务服务器管理员可能不需要此功能。

要保护 LILO 提示，请编辑 `/etc/lilo.conf` 并在提示行后添加以下内容：

```
password = your-password
restricted
```

将 "your-password" 替换为步骤 2.5.2 所示的强密码。保存 `/etc/lilo.conf` 并更改该文件的权限，因为 LILO 密码是以明文形式保存的：

```
[root]# chmod 600 /etc/lilo.conf
```

使更改生效：

```
[root] # /sbin/lilo
```

完成这些更改后，系统将像以前一样启动，但如果你在 LILO 提示处给 LILO 任何命令行选项（例如使用 `single` 在单用户模式启动），它将在继续执行之前要求输入密码。

### 步骤 2.7 设置系统访问安全策略

大多数 Linux 发行版都允许配置哪些用户允许在何时、什么时间、什么日期以及通过哪些服务（TELNET、FTP 等）登录系统。大多数 Linux 发行版开箱即用的配置是正确的（尽管有些松散），确认所有这些设置是非常重要的。

### 步骤 2.7.1. 检查是否禁用 TELNET root 登录

`/etc/securetty` 文件包含了允许 root 登录的所有 TTY 接口列表。在 Red Hat Linux 和大多数发行版中，该文件默认只包含控制台 TTY（tty1, tty2, ... tty8，包含）。如果远程用户需要该系统的 root 权限，他们只需登录自己的账户并使用 "su -" 命令变为 root。

### 步骤 2.7.2. 检查是否禁用 FTP  root 登录

`/etc/ftusers` 文件包含了所有不允许通过 FTP 登录的用户账户列表。确保 root 账户和所有额外的系统守护进程账户都列在此文件中。你还可以输入其他你不希望通过 FTP 访问机器的用户账户名。

### 步骤 2.7.3. 配置允许/不允许登录系统的系统账户

`/etc/security/access.conf` 包含系统中所有账户的登录参数。你可以类似于第 3.2 节描述的 TCP wrappers 方式，配置哪些用户通过哪些服务登录。要禁用 root 账户和管理员以外的所有控制台登录，请在 `/etc/security/access.conf` 中放入：

```
:ALL EXCEPT root admin :console
```

### 步骤 2.7.4. 配置允许/不允许使用特定资源的系统组

`/etc/security/group.conf` 定义了哪些用户可以访问具有特定的文件。

`/etc/security/limits.conf` 定义了特定用户或组的系统资源限制（CPU 时间、磁盘空间等）。

`/etc/security/times.conf` 定义了允许用户访问系统的时间段。可以限制普通用户的登录时间。

### 步骤 2.8 配置日志记录

Red Hat 和大多数其他发行版使用 syslog 生成日志。syslog 守护进程根据“设施”（Facility）和“级别”（Level）解析消息。syslog 存在一些安全问题，特别是没有内置方法可以判断日志是否被篡改。有几种替代守护进程可以为日志添加数字签名并对远程日志进行加密。参见附录 A 获取这些守护进程。

### 步骤 2.8.1. 优化 SYSLOG 设置

Red Hat 的默认日志设置良好，但可以做得更好。为了改进它，请编辑配置文件 `/etc/syslog.conf` 并添加以下内容：

```
*.warn;*.err      /var/log/syslog
kern.*           /var/log/kernel
```

注意：第一列 syslog facility 与第二列 syslog 文件之间的分隔符必须是制表符（tabs）。如果是空格，syslog 将无法加载。

### 步骤 2.8.2. 配置 VTY 实时日志

在 VTY 7 和 8 上实时显示系统日志（Alt-F7 和 Alt-F8 屏幕）非常有用。要实现此功能，请向 `/etc/syslog.conf` 追加内容：

```
*.info;mail.none;authpriv.none  /dev/tty7
authpriv.*               /dev/tty7
*.warn;*.err              /dev/tty7
kern.*                   /dev/tty7
mail.*                   /dev/tty8
```

更新 `/etc/syslog.conf` 后，你需要创建新的 syslog 文件并修复它们的权限：

```
[root]# touch /var/log/syslog /var/log/kernel
[root]# chmod 700 /var/log/syslog /var/log/kernel
```

要让 syslog 立即使用新配置，执行以下命令：

```
[root]# killall -HUP syslog
```

### 步骤 2.8.3. 配置日志轮转

Red Hat Linux 以及其他发行版使用 logrotate 工具将日志文件保持在合理的范围内，并保留指定时间。有关该命令和配置文件，请参见手册页 logrotate(8)。

要调整默认的 Red Hat 日志轮转配置并轮转步骤 2.8.1 中创建的 syslog 和内核日志，请编辑 `/etc/logrotate.d/syslog` 并添加以下内容：

```
/var/log/kernel {
  compress
  postrotate
  /usr/bin/killall -9 klogd
  /usr/sbin/klogd &
  endscript
}
```

```
/var/log/syslog {
  compress
  postrotate
  /usr/bin/killall -HUP syslogd
endscript
}
```





# 第 2 步
安装 Linux

接下来，编辑 /etc/logrotate.conf 以修改日志轮转以以你的需求。在下面的示例中，logrotate 将每周轮转日志，在删除之前保留最后四周的日志，压缩轮转后的日志，并且不旋转 utmp 和 wtmp 文件：

```
# 详情请参阅 "man logrotate"
# 每周轮转日志文件
weekly
# 保留4周的备份
rotate 4
```

```
# 将错误发送给 root
errors root
# 在轮转旧日志后创建新的（空）日志文件
create
```

```
# 如果你想压缩日志文件，取消此行的注释
compress
```

```
# RPM 包将日志轮转信息放入此目录
include /etc/logrotate.d
```

```
# ## 没有包拥有 lastlog 或 wtmp -- 我们将在这里轮转它们
#/var/log/wtmp {
# compress
# monthly
# rotate 1
}
```

```
#/var/log/lastlog {
# compress
# monthly
# rotate 1
}
```

一旦这些更改完成，它们将每天从 crontab 文件 /etc/cron.daily/logrotate 自动执行（Red Hat 6.0 的默认设置）。

# 第 2 步
安装 Linux

### 步骤 2.8.4. 配置远程日志

在任何相当规模的组织中，使用集中式日志主机都有许多益处。从安全角度来看，远程日志非常重要，因为攻击者在获取机器访问权限后的第一件事之一就是擦除或修改系统日志以掩盖其踪迹。如果日志消息的副本存储在另一个高安全的系统中，管理员可能仍然能够重现发生的情况。如果日志丢失，来自入侵的重要取证证据也会随之丢失。

若要将 syslog 消息发送到集中式日志主机，请编辑 /etc/syslog.conf 并根据组织安全策略指定的设施（facilities）和日志级别添加行。例如，要将所有警告和错误消息以及所有认证设施发送到中心（日志主机），请添加以下：

```
*warn.*;*.err @loghost
authpriv.*;.auth.* @loghost
```

### 步骤 2.8.5. 同步系统时钟与日志服务器

PC 类计算机中的硬件时钟以不准确著称。当许多工作站向中央服务器提供日志消息时，同步它们的时钟是非常重要的，这样日志消息上的时间戳才是准确的。在发生全网扫描或攻击时，同步的日志文件时间将更容易构建攻击时间线。网络时间协议（NTP）是为了精确同步计算机网络的系统时钟而开发的。设置系统时钟的一种简单方法是设置一个 cron 每小时运行一次 ntpdate。将以下命令放入 /etc/cron.hourly/set-ntp 文件：

```
/usr/bin/ntpdate -bu -t 3 loghost.example.org
sbin/hwclock --systohc
```

"b" 选项设置当前时间而不是交错时间，"u" 表示使用非特权端口，"t 3" 将时间设置为 3 秒，而不是默认的 1 秒。第二行将硬件 CMOS 值设置为当前系统时间。一旦保存了该文件，请设置权限：

```
[root]# chmod 700 /etc/cron.hourly/set-ntp
```

当然，这假设 loghost.example.org 正在运行 ntpd 守护进程。ntp3 RPM 包在 /usr/doc/ntp3* 目录下包含大量的 HTML 格式文档。另请访问 http://www.ecis.udel.edu/~ntp/ 获取 NTP 的最新信息以及主备服务器列表。

# 第 3 步
工作站网络配置的安全

工作站的安全主要是一个消除网络服务并严格限制对剩余部分访问的过程。典型的工作站运行在服务器-网络通信的客户端端。几乎不需要提供任何服务。在工作站上需要服务的远程情况下，它也应该仅向局域网内的一小组其他工作站或服务器提供。在第 3 步中，我们专注于移除服务，然后如果某些服务对于工作站的运行绝对必要，我们将提供如何增加所选服务安全性的建议。

# 第 3.1 禁用互联网守护进程服务

互联网守护进程 inetd 控制在需要时才启动的网络服务的访问，例如 telnet 和 ftp。典型的工作站不需要在守护进程配置文件 /etc/inetd.conf 中提供服务。如果你需要通过网络远程访问工作站，请考虑安装安全 Shell（SSH；见下文步骤 4.2）。请查看手册页 inetd.conf(8) 以获取 /etc/inetd.conf 格式的完整说明。

- 步骤 3.1. 编辑 /etc/inetd.conf 并注释掉所有服务

查看附录 B 获取 Red Hat 6.0 安装的 /etc/inetd.conf 副本。开启的服务是第一列没有哈希符号 "#" 的服务。编辑这些行并通过在第一列放置注释字符 "#" 将其注释掉。保存编辑后的文件并通过发送 HUP 信号让 inetd 进程重新加载配置文件：

```
[root]# killall -HUP inetd
```

如果你没有注释掉其他服务，至少确保该 shell 和登录服务是禁用的。Berkeley "r" 程序 rsh 和 login 有长期的滥用和安全问题历史。即使禁用了服务，你也应该检查确保没有用户在其主目录下有 .hosts 文件，并且没有 /etc/hosts.equiv 文件。这些文件是 "r" 程序用于向其他计算机上的用户分配“信任”。以下短脚本将检查每个家目录并告诉你哪个目录包含 .hosts 文件。

```
for i in sh
  [ cut -d: -f6 /etc/passwd]; do
    if [ -e $i/.hosts ]; then
      echo "SECURITY CHECK found .hosts in $i"
    fi
done
```

### 步骤 3.1.2. 如果没有服务则关闭 inetd

如果确实需要 /etc/inetd.conf 中的服务，可以关闭 inetd 进程本身：

```
[root]# /etc/rc.d/init.d/inetd stop
[root]# /sbin/chkconfig inet off
```

对于没有 chkconfig 的发行版，管理员管理员可以直接删除 init 脚本：

```
[root]# /bin/rm /etc/rc.d/rc[345].*inetd
```

如果由于某些原因，稍后需要由 inetd 控制的某个服务，可以通过运行 SYSV init 脚本临时开启：

```
[root]# /etc/rc.d/init.d/inetd start
```

# 第 3.2 使用 TCP WRAPPERS 控制对剩余 INETD 服务的访问

如果你绝对需要 /etc/inetd.conf 中的某一个或多个服务，请使用 TCP wrappers 将访问限制在有限的主机上。TCP wrapper 守护进程 /usr/sbin/tcpd 是一个小型程序，它根据 /etc/hosts.allow 和 /etc/hosts.deny 中的访问列表检查请求的源地址。如果列表允许，会将连接传递给相应的服务。Red Hat 和其他 Linux 发行版默认安装了 wrappers。参见手册页 hosts_access(5)。

### 步骤 3.2.1. 设置默认拒绝所有

编辑 /etc/hosts.deny 使默认规则变为：

```
ALL: ALL
```

只有当你有网络信息系统 (NIS) ypserv 包时，第二行才是必要的。

### 允许对特定主机访问特定服务

例如，要允许来自 host.example.org 的 ftp 访问，编辑 /etc/hosts.allow 并添加：

```
in.ftptd: host.example.org
```

在 /etc/hosts.allow 中输入语句后，编辑 /etc/inetd.conf 并移除 ftp 服务的注释字符：

```
ftp stream nowait root /usr/sbin/tcpd in.ftptd -a
# killall -HUP inetd
```

尽可能避免允许整个域名或子网的访问，例如 "example.org" 或 "192.168.1.0"。仅使用允许机器的主机或 IP 地址。

### 步骤 3.2.3. 使用 tcpchk 检查访问列表的语法

TCP wrapper 包含一个简单的程序用于检查 /etc/inetd.conf、etc/hosts.allow 和 /etc/hosts.deny 文件的语法，确保没有错误且文件一致。假设 /etc/hosts.allow 和 /etc/hosts.deny 所示，以下是 tcpchk 的示例运行：

```
[root]# tcpchk -v
Using network configuration file: /etc/inetd.conf
```

```
>> Rule         /etc/hosts.allow line 6:
daemons:        in.ftptd
clients:       host.example.org
warning:        /etc/hosts.allow, line 6: host.example.org: host not found
access:         granted
```

```
>> Rule         /etc/hosts.deny line 9:
daemons:        all
clients:       all
access:         denied
```

注意关于 host.example.org 未找到的查找警告。这提示你可能输入错误或错误输入了主机名（在此情况下该主机名是虚构的）。注意 tcpchk 会对 /etc/inetd.conf 中未列出但编译了 TCP wrappers 支持的服务发出警告，例如用于 RPC 错误的 portmap（见步骤 4.6.1）和用于 Secure Shell 的 sshd（见步骤 4.2.3）。这些警告可以忽略。





## 步骤 3
## 工作站网络配置

### 步骤 3.2.4. 为 TCP wrapped 服务设置横幅（banners）

TCP wrapped 的重要选项是“横幅（banners）”。大多数政府机构和许多商业组织要求在系统访问点（如 TELNET 和 FTP 端口）设置横幅。为了能够成功起诉闯入计算机的人员，通常需要设置登录横幅，警告未经授权的人员禁止访问该系统。TCP wrapped 服务可以配置为显示标准的登录横幅。TCP wrappers 文档附带了一个 Makefile，可以方便横幅的维护。要创建初始横幅，请执行以下命令：

```bash
# mkdir /etc/banners
# cp /usr/doc/tcp-wrappers-7.6/Banners.Makefile /etc/banners/Makefile
# cd /etc/banners
# echo "This is only the prototype banner. Replace with the real banner." > prototype banner
# make
```

默认情况下，Makefile 会为 `in.telnet`、`in.ftpd` 和 `in.logmind` 服务创建横幅文件。阅读 Makefile 中的注释以获取其他服务的横幅信息。横幅的具体措辞通常取决于本地安全策略。计算机事件咨询能力（CIAC）小组已发布了一份包含示例措辞的横幅公告。URL 请参见附录 A。

要激活横幅，编辑 `/etc/hosts.allow`。对于所有允许横幅服务的行，添加 `/etc/banners` 选项，随后是 `allow` 选项。在 `/etc/hosts.allow` 的底部添加另一个选项行，为被拒绝的服务设置横幅。例如，允许来自 `work.example.org` 的 telnet 会话：

```text
in.telnet: work.example.org : banners /etc/banners : allow
all : all : banners /etc/banners : deny
```

TCP wrappers 有大量丰富的选项，包括调整 syslog 设施和级别、调整守护进程的运行时特性、“陷阱”等。更多信息请参阅手册页 `hostsosts_options(5)` 和附录 A。

## 步骤 3 禁用运行时网络服务

## 步骤 3 工作站网络配置

Internet 守护进程（daemon）处理瞬时的、“一次性”网络连接，还有其他在启动时启动并一直运行到系统关闭的守护进程，例如用于 Web 的 `httpd`、用于 DNS 服务的 `named` 以及用于 Samba SMB 网络服务的 `smbd`。它们由 init 进程（进程 1）在启动时启动。Red Hat Linux 以及除 Slackware 以外的大多数发行版使用 Sys 风格的 init，它使用运行级别概念和运行时控制脚本来管理进程的启动和关闭。关于 init 配置文件 `/etc/inittab` 的讨论，请参见步骤 2.6.2。

参阅手册页 `init(8)` 可获取更多关于 init 的信息以及对六种正常运行级别的描述。正常运行有两个级别：运行级别 3 是用于登录的字符模式控制台；运行级别 5 启动 X 窗口服务器并使用 X 显示管理器 (xdm) 登录。控制运行级别 3 进程启动和关闭的脚本位于 `/etc/rc.d/rc3.d` 目录，运行级别 5 位于 `/etc/rc.d/rc5.d`。准确来说，这些目录中的脚本是 `/etc/rc.d/init.d` 中用于每个运行级别的通用脚本的符号链接。

脚本名称以数字为前缀，表示它们的执行顺序，例如，`s10network` 在 `s5named` 之前执行，`s5named` 在 `s85httpd` 之前执行，依此类推。“S”告诉 init 该脚本用于启动，“K”告诉该脚本用于关闭（“S”类脚本接收单个参数 `start`，“K”类脚本接收参数 `stop`）。在任何时刻，root 都可以通过执行 `/etc/rc.d/init.d` 中的脚本来启动或停止服务，例如关闭 Web 服务器。

```bash
[root]# /etc/rc.d/init.d/httpd stop
```

### 步骤 3.3.1. 确定哪些网络服务正在运行

使用 `/bin/netstat` 列出正在“监听”连接的端口：连接（服务器和已建立的）

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| tcp | 0 | 0 | *:netbios-ssn | *:* | LISTEN |
| tcp | 0 | 0 | *:www | *:* | LISTEN |
| tcp | 0 | 0 | *:smtp | *:* | LISTEN |
| tcp | 0 | 0 | *:1040 | *:* | LISTEN |
| tcp | 0 | 0 | *:702 | *:* | LISTEN |
| tcp | 0 | 0 | *:697 | *:* | LISTEN |
| tcp | 0 | 0 | *:692 | *:* | LISTEN |
| tcp | 0 | 0 | *:673 | *:* | LISTEN |
| tcp | 0 | 0 | *:printer | *:* | LISTEN |
| tcp | 0 | 0 | 192.168.1.3:domain | *:* | LISTEN |
| tcp | 0 | 0 | localhost:domain | *:* | LISTEN |
| tcp | 0 | 0 | *:sunprpc | *:* | LISTEN |

在“Local Address”下，如果服务在 `/etc/services` 文件中找到，端口号将以名称报告，否则仅给出端口号。正如我们所看到的，即使在 `/etc/inetd.conf` 中注释掉所有服务后，默认安装仍然有许多服务在运行。

## 逐步加固 LINUX

## 步骤 3 工作站网络配置

遗憾的是，`netstat` 不显示进程在哪个端口上的列表。另一个名为 `lsof` 的工具用于“列出所有打开的文件（List Open Files）”，它可以列出任何进程的所有打开文件，包括网络套字。取决于在步骤 2 中遵循的安装过程，`lsof` 可能未安装。对于 Red Hat，该软件包位于安装 CD-ROM 上，源代码可以在附录 A 中列出的主要存档中找到。`lsof` 有很多选项和灵活性。更多信息请参阅手册页 `lsof(8)`。列出所有打开的网络套字：

```bash
[root]# lsof -i -M
COMMAND PID USER FD TYPE DEVICE NODENAME
portmap 3264 root 3u 4546 UDP :*:nrpc[portmap]
portmap 3264 root 4u 4547 UDP :*:nrpc[portmap]
*(注：此处原文中 lsof 输出部分存在乱码，已根据逻辑修正格式)*
```

要将此列表缩小为仅列出守护进程名称：

```bash
[root]# lsof -i -Fc | grep '^c' | cut -b2-20 | sort -u
httpd
lnpd
named
nmbd
portmap
rpc.mountd
rpc.quotad
rpc.statd
sendmail
smbd

### 步骤 3.3.2. 消除不需要的服务

技巧在于知道哪个 init 脚本控制哪个守护进程。大多数守护进程由命名脚本控制，其他的可以通过使用 `grep` 在 `/etc/rc.d/init.*` 中搜索名称来找到。要消除服务，首先使用其 init 脚本关闭，然后从运行级别目录中删除脚本。对于 Red Hat Linux，删除运行级别链接的最简单方法是使用 `/sbin/chkconfig` 程序，或者你可以直接删除它们。默认情况下，`chkconfig` 在级别 3、4 和 5 中添加或删除链接。它不会删除 `/etc/rc.d/init.d` 中的实际脚本。如果你手动操作运行级别脚本，请务必始终从运行级别 3 和运行级别 5 目录中删除启动脚本，这样更改运行级别就不会意外打开你认为已经关闭的网络服务。





以下操作将关闭上述步骤 3.3.1 中列出的所有服务：

```
[root]# /etc/rc.d/init.d/httpd stop
[root]# /sbin/chkconfig httpd off
[root]# /etc/rc.d/init.d/lpd stop
[root]# /sbin/chkconfig lpd off
[root]# /etc/rc.d/init.d/named stop
[root]# /sbin/chkconfig named off
[root]# /etc/rc.d/init.d/netfs stop
[root]# /sbin/chkconfig netfs off
[root]# /etc/rc.d/init.d/smb stop
[root]# /sbin/chkconfig smb off
[root]# /etc/rc.d/init.d/nfs stop
[root]# /sbin/chkconfig nfs off
[root]# /etc/rc.d/init.d/portmap stop
[root]# /sbin/chkconfig portmap off
[root]# /etc/rc.d/init.d/sendmail stop
[root]# /sbin/chkconfig sendmail off
```

若要手动删除启动脚本，请将 `chkconfig` 替换为 `rm`，如下所示：

```
[root]# /bin/rm /etc/rc.d/rc[345].*sendmail
```

一旦服务关闭，可以考虑完全删除该软件包。这可以释放磁盘空间并增强安全性，因为本地用户无法滥用不存在的服务。

### 步骤 3.3.3. 检查是否存在剩余服务

返回步骤 3.3.1，并使用 `netstat` 和 `lsof` 命令重复操作，检查是否有任何剩余的网络服务，并禁用它们，直到所有网络服务都关闭。

## 步骤 3.4 获取软件的最新版本

在接下来的步骤中，我们将讨论如何提高所选服务的安全性。你应该只启用完成工作所需的极少数服务集。在启用任何服务之前，请确保你已拥有最新版本的软件。所有的 Linux 发行版在跟进安全相关的漏洞修复方面做得很好，并定期更新其 FTP 站点以发布最新软件版本。

- 步骤 3.4.1. 查找安全相关的更新

更新的软件（在 Red Hat 的术语中称为“errata”）可以在其网站 http://www.redhat.com/corp/support/errata 上找到，其他发行版的更新位置请参见附录 A。Red Hat 重新设计了 Red Hat 6.0 的 errata 页面，其中一列是安全相关的更新，另一列是其他软件包更新。至少，你应该检查并获取所有安全相关的更新。

- 步骤 3.4.2. 下载更新

更新软件包的 FTP URL 直接包含在 errata 页面中，因此可以直接通过你的 Web 浏览器下载软件包。一种良好的做法是创建一个单独目录（例如 `/usr/local/updates`），并将更新的软件包放在那里。也可以从 http://updates.redhat.com 批量下载更新软件包。选择对应版本和架构的目录，例如 `6.0/i386`，并将所有文件下载到 `/usr/local/updates`。周复复地这样做可能会非常枯燥，有关自动化此过程的信息，请参阅步骤 3.4。

RPM 能够通过提供包名的 URL 直接在网络上安装软件包；这消除了对独立下载目录的需求。对于连接较慢且/或不可靠的网络连接（如现代线路）的工作站，最好下载软件包并从本地副本安装，而不是在更新过程中让网络连接断开或挂起。

## 步骤 3 安全工作站网络配置

### 步骤 3.4.3. 安装更新

使用 `rpm` 安装更新的说明包含在 errata 页面中。通常，可以如下所示更新软件包：

```
[root]# rpm -Uvh <package-name>
```

例如更新 Samba：

```
[root]# rpm -Uvh samba-2.0.5a-1.i386.rpm
```

若要直接通过网络更新，请提供包包名的 URL：

```
[root]# rpm -Uvh ftp://updates.redhat.com/6.0/i386/samba-2.0.5a-1.i386.rpm
```

如果你已将所有最新更新下载到 `/usr/local/updates`，可以使用以下命令对系统中已安装的软件包进行“刷新（freshen）”：

```
[root]# rpm -F /usr/local/updates/
```

这将只会升级 `/usr/local/updates` 中已安装且版本号较旧的软件包。

注意，更新内核时请使用 `-i` 表示“安装（install）”而不是 `-U` 表示“升级（upgrade）”。这将保留之前的内核版本（`-U` 选项移除之前的内核），因此如果由于某些原因新内核无法运行，仍可以使用旧内核启动。此外，如果你正在运行模块化内核（特别是在基于 SCSI 的系统上），在启动更新后的内核之前可能需要重新运行 `mkinitrd`。更多信息请参阅 `mkinitrd(8)` 手页。

![](img/0aaa698c422b2f7ffe93bff50cbbef96_38_0.png)

![](img/0aaa698c422b2f7ffe93bff50cbbef96_38_1.png)

## 步骤 3 安全工作站网络配置

### 步骤 3.4.4. 自动化流程

在将工作站用于日常工作之前更新软件包是重要的，但随着时间的推移，保持更新也同样关键。新的漏洞修复和增强不断产生。尝试让本地工作站与更新保持同步可能既枯燥又耗时。

幸运的是，有几个第三方工具可以自动化检查 FTP 站点是否有新包的过程，甚至可以在无需人工干预的情况下安装更新。你可以在 Metab FTP 站点的 `/utils/package/` 子目录、Freshman 以及其他流行的 FTP 站点找到这些工具。特定 URL 请参见附录 A。我们在这里只讨论一个程序，但还有其他几个。

### 步骤 3.4.4.1. 使用 AutoRPM 自动化更新

请参附录 A 获取 AutoRPM 主页的 URL。引用 AutoRPM 手页的内容：

AutoRPM 是一个可以执行以下任意组合的程序：从 FTP 站点镜像 RPM、保持已安装的 RPM 与 FTP 站点或本地目录一致，以及保持集群或网络系统中已安装的 RPM 一致。它非常灵活。

要运行 AutoRPM，必须首先安装 `libnet` 库，可以从任何 CPAN 站点获取。如果你不熟悉 Perl CPAN，AutoRPM 的作者贴心地从其网站提供了一个 RPM 版本。在指南中测试 AutoRPM 时，我们发现该程序确实非常灵活，但安装起来有点复杂。压缩包可能可以使用 Makefile 来简化安装。默认配置对 Red Hat Linux 效果良好，在浏览手册页后，更改配置以适应其他发行版并不困难。![](img/0aaa698c422b2f7ffe93bff50cbbef96_39_0.png)

![](img/0aaa698c422b2f7ffe93bff50cbbef96_39_1.png)

要安装 AutoRPM，请下载压缩 tar 包并解压：

```
[root]# cd /usr/local/src
[root]# tar xzf <download-dir>/autorpm\*.tar.gz
[root]# cd autorpm
```

其中 `<download-dir>` 是下载 tar 包的位置。命令中的通配符是为了避免输入实际版本号（该指南出版时可能已经更改）。

创建配置文件并安装配置文件、程序和主页：

```
[root]# mkdir --mode 700 /etc/autorpm.d
[root]# cp autorpm.conf autorpm.d/* /etc/autorpm.d
[root]# mkdir --mode 700 /etc/autorpm.d/pools
[root]# cp pools/* /etc/autorpm.d
[root]# install --owner=root --group=bin --mode=0700 autorpm.pl /usr/sbin/autorpm
[root]# cp autorpm.8 /usr/local/man/man8
[root]# cp autorpm.conf.5 /usr/local/man/man5
```

阅读 `autorpm(8)` 和 `autorpm.conf(5)` 手册页，但默认设置适用于 Red Linux。

以交互模式手动运行 AutoRPM 以检查更新的 RPM：

```
[root]# autorrpm --interactive
```

AutoRPM 将从 `/autorpm.d/pools/redhat-updates` 中列出的 FTP 站点下载包名，并将其与当前安装的软件包集进行比较。默认的 FTP 站点列表很长。良好的做法是编辑列表，仅保留你已知并信任的站点，例如 `ftp://updates.redhat.com` 以及可能的本地镜像。





# 第 3 
安全工作站网络配置

在尝试运行 AutoRPM 自动下载并安装更新之前，请编辑 `/etc/autorpm.d/redhat-updates` 并在标记为 `action (updated)` 的动作块中添加命令 `PGP_Require Yes`。这将强制在安装 RPM 包之前对其进行 PGP 签名检查。在配置生效之前，您需要安装 PGP 或 GPG 并下载 Red Hat 的公钥。更多信息请参阅 `rpm(8)` 帮助页的“PGP SIGNATURES”部分。

AutoRPM 还带有一个 cron 任务，可以将其放在 `/etc/cron.daily` 或您喜欢的任何目录下：

```
[root]# cp autorpm.cron /etc/cron.weekly/autorpm
```

该 cron 任务被设置为将需要执行的操作报告发送到 `/etc/autorpm.d/autorpm.conf` 中 `ReportDest` 变量列出的地址。

配置 AutoRPM 以适用于其他发行版简单，只需更改 `/etc/autorpm.d/pools/redhat-updates` 文件中的 FTP 站点列表。然而，您可能希望将文件名更改为您的发行版名称。如果是这样，您需要编辑 `/etc/autorpm.d/autorpm.conf` 并更改 `ConfigFile` 条目以反映新名称。

- 3.4.5. 订阅安全相关邮件列表

有许多邮件列表分发有关计算机安全、新发现的漏洞和利用程序、错误修复以及更新的信息。即使有自动化过程来寻找更新的 RPM 包，对于可能没有可用更新软件的安全相关问题，保持信息灵通也至关重要。至少您会知道在修复程序出现之前关闭易受攻击的服务。

请参阅附录 A 以获取安全相关邮件列表列表及订阅说明。对于典型的工作站用户来说，像 Bugtra 这样高流量的邮件列表可能会导致信息过载。至少请订阅您所在 Linux 发行版的“announce”列表。

# 第 3.5 节 仅缓存的域名服务 (DNS)

Red Hat 6.0 包含了最新版本的伯克利互联网域名系统（BIND）软件，版本 8.2。此版本包含了几个与安全相关的错误修复和额外的安全增强。无论如何，Linux 工作站没有需要运行自己的名称服务器，即使在仅缓存模式下也是如此。永久禁用并删除该软件。

- 步骤 3.5.1. 禁用并删除 DNS 服务器软件

如果在上面的步骤 3.3.2 中未执行，请停止 `named` 守护进程并从工作站移除软件：

```
[root]# /etc/rc.d/init.d/named stop
[root]# rpm -e caching-nameserver
[root]# rpm -e bind
```

- 步骤 3.5.2. 设置主、备名称服务器

如果在安装过程中未执行此操作，请编辑 `/etc/resolv.conf` 并添加主名称服务器以及（如果有）备名称服务器的 IP 地址。每个名称服务器都用如下行表示：

```
nameserver www.xxx.yyy.zzz
```

逻辑上，主名称服务器的 IP 列在前面，然后是备名称服务器。由于仅缓存域名服务已移除，请确保没有指向您的本地 IP 地址或 127.0.0.1 的 `nameserver` 行。

# 第 3.6 节 电子邮件

典型的工作站不需要以守护模式运行如 `sendmail` 这样的邮件传输代理（MTA）。
大多数互联网服务提供商、大学、政府和商业组织都提供邮件服务器。

- 步骤 3.6.1. 关闭 sendmail 守护模式

编辑 `/etc/sysconfig/sendmail` 使内容如下：

```
DAEMON=no
QUEUE=15m
```

`QUEUE` 选项控制 `sendmail` “唤醒”处理出站邮件队列的频率，默认设置为 15 分钟。在保存修改后的 `/etc/sysconfig/sendmail` 后，重启守护进程：

（此处由于原文存在大量重复和逻辑混乱，翻译遵循原文语序）
以守护模式运行如 `sendmail` 这样的邮件传输代理。
大多数互联网服务提供商、大学、政府和商业组织都提供邮件服务器。

- 步骤 3.6.1. 关闭 sendmail 守护模式...（略）

- 步骤 3.6.2. 设置主、备名称服务器...（略）

... 
逻辑上，主名称服务器的 IP 列在前面，然后是备名称服务器。由于仅缓存域名服务已移除，请确保没有指向您的本地 IP 地址或 127.0.0.1 的 `nameserver` 行。

# 第 3.6 节 电子邮件

（注：由于提供的原文从 3.6 节开始出现严重的文本重复和无意义片段，译文已尽可能根据“不重复输出原文”的原则，对核心指令部分进行了翻译，并跳过了无意义的重复循环。）





# 第 3 
工作站安全
网络配置

例如：

```
[root]# mkdir /mnt/devel
[root]# mount -t nfs -o rw,hard,noexec,nosid,nodev project:/usr/src/devel /mnt/devel
```

注意，NFS 挂载目录的读写权限是由服务器（project）上所有者的 UID 和 GID 定义的，而不是由客户端（你的工作站），两台机器上的 UID 和 GID 需要保持一致。

为了在每次启动工作站时都自动挂载此目录，`/etc/fstab` 中的挂载点应如下所示配置：

```
/mnt/devel project:/usr/src/devel nfs rw,hard,noexec,nosid,nodev,bg,auto 0 0
```

添加 `auto` 选项允许初始化脚本在启动时挂载 NFS 目录（即通过 `mount -a`）。但请注意，指定 `hard` 挂载（硬连接）意味着如果 NFS 服务器未运行，工作站将会挂起。因此，我们添加了 `bg` 和 `/bin/mount` 以在后台执行挂载，并在服务器未立即可用时允许继续操作。你也可以添加另一个选项 `intr`，以便在挂起时中断挂载点。如果 NFS 服务器或本地网络存在可靠性问题，请考虑使用 `soft` 挂载而非 `hard` 挂载。优点是当 NFS 服务器宕或不可用时，工作站不会挂起；缺点是如果服务器宕且客户端超时，可能会丢失 NFS 服务器上的数据。

如果 NFS 挂载的明确目的是共享可执行程序（例如 NFS 服务器上的 `/usr/local/bin`），你需要将 `noexec` 改为 `exec`。在将 `nosuid` 改为 `suid` 以允许 set-uid 和 set-gid 权限之前，请务重考虑。注意，`nosuid` 和 `noexec` 选项仍然可能被 `suidperl` 等程序破解，它可以将脚本作为普通数据文件复制，然后用 SUID 权限执行它。更多信息请参见 `mount (8)` 和 `fstab(5)` 的手册页。

# 第 3.8 将万维网服务限制在本地主机

与其他许多发行版一样，Red Hat 6.0 安装了一个功能完整的 Apache Web 服务器，默认情况下允许来自互联网上任何计算机的连接。对于典型的工作站设置，这是没有必要的。不过，如果你是 Web 开发者，拥有一个完全本地化的 Web 服务器对于在部署到运行中的网站之前测试设备、CGI 脚本、applet 等非常有用。

### 步骤 3.8.1 关闭 HTTP 并移除服务器软件

如果不需要本地 Web 服务器，直接从工作站中移除即可：

```
[root]# /etc/rc.d/init.d/httpd stop
Shutting down http:                   [ OK ]
[root]# rpm -e apache
[root]# rpm -e apache-devel
```

### 步骤 3.8.2 将 HTTP 访问限制为 localhost

Apache HTTP 守护进程可以绑定到特定的网络接口。如果接口是 `localhost`（IP 127.0.0.1），则从外部网络尝试连接 80 端口的任何操作都会导致连接被拒绝。从错误信息来看，机器上似乎没有任何 Web 服务器。

编辑 `/etc/httpd/conf/httpd.conf`，查找底部附近带有 `Listen` 选项的区域——它应该紧邻 `VirtualHost` 区域之前。添加以下行：

Listen 127.0.0.1:80

保存 `/etc/httpd/httpd.conf` 并重启 Web 服务器：

```
[root]# /etc/rc.d/init.d/httpd restart      [ OK ]
Shutting down http:                               [ OK ]
Starting http:
[root]# netstat -a | grep www
tcp        0       localhost:www             *LISTEN
```

`netstat` 命令显示 Web 守护进程仅在环回设备上监听，而不是普通的网络设备。要测试访问是否被拒绝，请从另一台计算机上尝试：

$ telnet workstation 80
Trying 192.168.1.3...
tel: unable to connect to remote host: Connection refused
Web 服务器现在对工作站本身的用户以外的所有人都都关闭了访问。

![](img/0aaa698c422b2f7ffe93bff50cbbef96_47_0.png)

# 第 3.9 移除匿名 FTP 服务

尽管你可能在上面的步骤 3.1.1 中关闭了 FTP 服务，或者在步骤 3.2.1 中使用 TCP 封装限制了其访问，你仍应该消除匿名 FTP 功能。首先编辑 `/etc/ftpaccess` 并修改以下行：

```
class all real,guest,anonymous *
to read:
class all real *
```

最后，移除用于匿名 FTP 的家目录：

```
[root]# rpm -e anonftp
```

# 第 4
服务器安全
网络配置

# 第 4.1 服务器：请参考步骤 3.1、3.2、3.3 和 3.4 以禁用所有不必要的服务、设置封装并更新软件

与工作站一样，服务器也应该只运行少数网络服务以满足其目的。信息服务器可以被设置为运行 HTTP 和 FTP，但不应同时承担运行大型邮件列表或通过 Samba 或 NFS 向多个客户端共享文件的负担。虽然本节的其余部分提供了保护多个服务的步骤，但……

# 第 4.2 为远程访问安装 SSH

Secure Shell (SSH) 最初在赫尔辛基理工大学开发。它使用 RSA 公钥算法提供强身份验证，并对登录和文件复制进行自动加密。版本 1 的源代码免费供非商业使用。版本 2 的限制更多，未经商业许可禁止在商业或政府组织使用。参见 http://www.ssh.fi/ssh2/download.html 获取链接。

### 步骤 4.2.1 下载、编译并安装 SSH

SSH 版本 1 可以从 ftp://ftp.cs.hut.fi/pub/ssh/ 下载，如果该地繁忙，SSH 下载页面上有镜像站点列表。在编写本文时，`ssh-1.2.27.tar.gz` 是最新版本，我们在下面的示例中使用该版本。检查 FTP 获取更新版本，因为版本 1 源经常修复问题和漏洞。

```
[root]# wget ftp://ftp.cs.hut.fi/pub/ssh/ssh-1.2.27.tar.gz
[root]# xzf ssh-1.2.27.tar.gz
[root]# cd ssh-1.2.27
[root]# ./configure --with-libwrap --without-rsh --disable-suid-ssh --disable-scp-stats
[root]# make
[root]# make install
```

`configure` 脚本的选项执行以下操作：编译 SSH 守护程序的 TCP 封装支持；禁用所有 rsh 回退支持；禁用 SSH 客户端的 set-uid 位；关闭安全复制程序 scp 的屏幕统计信息打印（以模拟 rcp 的行为）。

执行以下命令查看已安装包：

```
[root]# rpm -qa >/root/package.list
[root]# chmod 400 /root/package.list
```

这将导出包列表以及每个包的文件。

![](img/0aaa698c422b2f7ffe93bff50cbbef96_49_0.png)





## Step 4.2.2. 启动 SSH 守护进程

SSH 守护进程 sshd 应该在启动时启动，并在服务器运行期间保持运行。实现此点的一种简单方法是将此行：

```
/usr/local/sbin/sshd
```

添加到 /etc/rc.d/rc.local 中，它将在所有其他启动时程序启动后执行。

请参录录 C，获取使用 daemon 和 killproc 函数的以 Red Hat 为中心的 SYSV-init 脚本。将此复制到 /etc/rc.d/init.d/sshd，并将其链接到运行级别目录：

```bash
[root] for i in /etc/rc.d/rc[345].d; do (cd $; ln -s ../init.d/sshd S50sshd); done
```

或者，替代方案：
```bash
[root] chkconfig sshd on
```

以便在不重启的情况下现在启动守护进程：

```bash
[root]# /etc/rc.d/init.d/sshd
```

## Step 4.2.3. 设置 /etc/hosts.allow 用于 SSH 访问

使用 -with-libwrap 配置选项编译 SSH 允许 sshd 执行 TCP-wrapper 风格的访问控制，为每个请求检查 /etc/hosts.allow 和 /etc/hosts.deny 文件。其语法和选项与任何 TCP-wrapped 服务完全相同，且服务名称为 sshd。例如：

```
# 允许我们域名或 goodguys.org 域名中的任何人进行 SSH 访问
sshd: LOCAL .goodguys.org
```

## Step 4.2.4. 生成 SSH 密钥

SSH 使用 RSA加密公钥执行用户身份验证和会话加密密钥的交换。每个允许访问服务器的用户都必须在其用于访问服务器的工作站上生成公/私钥对，并将公钥存放在服务器上其想要登录的账户中。

在远程工作站上，按照说明安装 SSH，然后在你的普通用户账户中执行：

```bash
[user]$ ssh-keygen
```

密钥生成器将计算公钥和私钥对，并提示保存它们的文件，默认为家目录下的 ./identity。接受默认位置。然后你将被要求输入密码短。

关于密码短：你并不需要输入一个，如果你不输入，SSH 在使用密钥时将不会提示输入密码短（例如在启动登录会话时）。如果你计划在脚本中自动化 ssh 或 scp（SSH 安全复制），这特别有用。缺点是，如果你的工作站和账户被破解，攻击者将无需输入密码短即可访问服务器。

对于对服务器的普通 shell 和文件复制访问，最好使用密码短，并记住选择良好密码的所有规则。如果需要使用 SSH 进行自动化、非交互式的访问服务器，请考虑 ssh-agent 和 ssh-add。agent 是一个处理 ssh 使用私钥的进程，ssh-add 程序与 ssh-agent 通信并向其发送密钥，必要时提示密码短。在你的密钥被 ssh-agent 存储后，在登录会话剩余时间内你不需要再次输入密码短。更多信息请参见 ssh-agent(1) 和 ssh-add(1) 的手册。

当 ssh-keygen 完成后。.ssh 目录下有两个文件：identity 和 identity.pub。前者是你的二进制私钥，后者是带有公钥的 ASCII 文件。在可以使用 SSH 登录之前，必须将公钥存储在服务器上。

## STEP 4 安全服务器网络配置

将公钥传输到服务器的最安全方法是“肉体网络”，即将密钥拷贝到软盘并带到服务器。尽管如此，通过网络传输公钥通常是安全的。即使公钥在网络上被截获，没有私钥它也是无用的，而且从其他密钥推导出极其困难，甚至是不可能的。永远不要通过网络发送私钥，并确保 .ssh/identity 文件具有 0600 权限并归你所有。

一旦密钥复制到服务器，将其放在你想要访问的账户的家目录下（我们在示例中使用 root 账户），假设公钥位于家目录下的 identity.pub 文件中。

```bash
[root] cd ~
[root] mkdir .ssh
[root] cat identity.pub >> .ssh/authorized_keys
[root] chmod 600 .ssh/authorized_keys
```

authorized_keys 文件持有每个授权访问用户的公钥。如果你使用上述方法复制了多个密钥，请小心重定向；确保是追加 (>>) 到文件，而不是覆盖它 (>)。

### 4.5. 使用 ssh 和 scp 进行远程访问

当服务器上运行 SSH 守护进程，且工作站账户的公钥位于 /root/.authorized_keys 时，你现在可以使用 SSH 从工作站访问服务器。ssh 命令的工作原理类似于 rsh。要打开登录 shell 或执行命令：

```bash
[user@workstation]$ ssh -l root server "ls"
```

scp 命令的工作原理类似于 rcp。要将文件复制到服务器：

```bash
[user@workstation]$ scp File root@server:~
```

要从服务器拷贝大量文件：

```bash
[user@workstation]$ scp root@server:* ./backup_dir
```

## Step 4.2.6. 用 SSH 替换 “r”程序

一旦 SSH 安装并正常运行，就不再需要在工作站或服务器上保留任何“r”客户端（login, rsh 或 rcp）或服务器守护进程（in.login, in.rsh, in.rexec）。即使它们在 /etc/inetd.conf 中被注释掉，删除这些程序也是安全的。

```bash
[root]# rpm -e rsh
```

一旦“r”程序被删除，可以将 SSH 程序放在它们的位置：

```bash
[root]# ln -s /usr/local/bin/ssh /usr/bin/rsh
[root]# ln -s /usr/local/bin/ssh /usr/bin/rlogin
[root]# ln -s /usr/local/bin/scp /usr/bin/rcp
```

## STEP 4.3 域名服务和 BIND 版本 8

Red Hat 6.0 带有 BIND 8.2 版本，这是本文当时的最新版本。早期 Red Hat 及其他发行版的管理员应该检查他们运行的 BIND 版本。如果你运行 BIND 版本 4，请升级到 BIND 8.2。如果你运行 8.1.1 或更早版本，必须升级到 BIND 8.1.2 或更高版本，早期版本存在远程 root 漏洞。检查你发行版的更新，或从 http://www.isc.org 下载最新源码。

## Step 4.3.1. 限制区域传输

配置主服务器仅向从服务器执行区域传输，在 /etc/named.conf 的区域中使用 allow-transfer 选项，并为区域指定仅从服务器的 IP 地址：

```
zone "notransfer.com" {
	type master;
	file "db.notransfer.com";
	allow-transfer ( 192.168.1.1; 192.168.2.1; );
};
```

```
zone "notransfer.com" {
	type slave;
	masters ( 192.168.0.1; );
	allow-transfer ( none );
};
```





# 第 4 步
## 安全服务器网络配置

### 步骤 4.3.2. 限制查询

你可以使用 `allow-query` 选项限制允许查询名称服务器的主。可以使用 `listen-on` 选项限制允许查询的接口。这些选项可以全局应用于 `/etc/named.conf` 中的 `options` 列表：

```
options {
  allow-query ( 192.168.0/24 );
  listen-on ( 192.168.0.1; 127.0.0.1 );
};
```

或者也可以针对特定区域进行限制：

```
zone "notransfer.com" {
  type slave;
  masters ( 192.168.0.1;
  allow-transfer ( none );
  allow-query ( 127/8; 192.168.0/24 );
};
```

这对于保护防火墙环境中堡垒机上的区域信息非常有用。它允许只允许来自内部网络主名称服务器的查询，而影子主名称服务器则处理来自互联网的查询，并提供受限的防火墙网络视图。更多信息请参见《DNS and BIND》，第三版，Ablitz and Liu, O'Reilly and Associates, 1998（这本书对于任何名称服务器都是必不可少的）。

### 步骤 4.3.3. 在 chroot 狱中运行 named

BIND 版本 8.1.2 和 8.2 有以 root 以外的用户运行的能力，这有所帮助，但如果名称服务器被破坏，系统仍然会面临风险。为了提高安全性，可以将服务设置为在它自己的 chroot 目录树中运行。设置正确的 chroot 狱必须非常小心。不仅区域文件和其他配置文件需要位于 chroot 目录树中，运行 named 所需库、设备和可执行文件也必须放在那里。在以下示例中，用户名 (dns)、UID、GID 和家目录是随机选择的。请根据你的站点使用任何意义合理的唯一值。

### 步骤 4.3.3.1. 创建新用户和组

```bash
[root]# groupadd -g 150 dns
[root]# useradd -u 150 -g 150 -M dns
```

### 步骤 4.3.3.2. 准备 chroot 目录

```bash
[root]# mkdir -m 0700 /home/dns
[root]# cd /home/dns
[root]# mkdir -p etc lib dev usr/sbin var/named/run
[root]# mknod -m 666 dev/null c 1 3
```

### 步骤 4.3.3.3. 拷贝配置文件和程序

```bash
[root]# cp /etc/named.conf etc
[root]# cp -R /var/named/* var/named
[root]# chown -R dns.dns var/named var/run
[root]# cp /usr/sbin/(named,named-xfer) usr/sbin
```

### 步骤 4.3.3.4. 拷贝共享库

首先，输出需要的哪些库：

```bash
[root]# lld libc.so.6 => /lib/libc.so.6 (0x401c0000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

```bash
[root]# cp /lib/libc.so.6 lib
[root]# cp /lib/ld-linux.so.2 lib
```

### 步骤 4.3.3.5. 设置 syslog 监听 named 日志

named 通过 /dev/log 与 syslog 通信，但在 root 狱中是不可能的。必须告诉 syslog 守护进程创建一个新的字字字 named 写入。编辑 /etc/rc.d/init.d/syslog，重写启动 syslog 守护进程的行：

`daemon syslog -a /home/dns/dev/log`

并重启守护进程：

```bash
[root]# /etc/rc.d/init.d/named stop
[root]# /etc/rc.d/init.d/named start
```

### 步骤 4.3.3.6. 修改 named init 脚本

编辑 /etc/rc.d/init.d/named 以在 chroot 狱中使用新的 UID/GID 启动守护进程：

```bash
# Start daemons.
echo -n "Starting named:
daemon named -u dns -g dns -t /home/dns
echo
touch /var/lock/subsys/named
;;
```

并重启名称服务器：

```bash
[root]# /etc/rc.d/init.d/named stop
[root]# /etc/rc.d/init.d/named start
```

为了确保运行正常，检查 /var/log/messages，named 应该写入类似条目：

```
Jul 25 01:08:00 server named[1782]: chrooted to /home/dns
Jul 25 01:08:00 server named[1782]: group = dns
Jul 25 01:08:00 server named[1782]: user = dns
```

使用 nslookup 测试名称服务器是否按预期运行。

## 步骤 4.3.3.7. 为 ndc 指定新的新的控制通道

如果你需要运行名称服务器控制程序 ndc，则需要在 chroot 狱内指定新的控制通道：

```bash
[root]# ndc -c /home/dns/var/run/ndc
```

使用 shell 别名或带有新控制通道的短脚本可以减少按键。

## MAIL

如步骤 3.6 所示，sendmail 是一个邮件传输代理 (MTA)，适用于 Red Hat 6.0 和其他发行版。Red Hat 6.0 附带 sendmail 8.9 版本，这是编写时的最新版本。Red Hat 或其他发行版的管理员应升级到 8.9.3 版本。8.9 版本的 sendmail 默认允许使用你的服务器中发垃圾邮件。

sendmail 的配置和操作非常复杂。所有的 sendmail 管理员都应该有一本 Allman, O'Reilly & Associates, 1997 (the Sendmail Book)。对于初来说，手动修改 /etc/sendmail.cf 非常困难且容易出错。最好的方法是使用 m4 处理器，Red Hat 发行版中的 sendmail-cf* 软件包。关于 m4 的详细信息可以在 Sendmail Book 中找到。

### 4.4.1. 关闭 /etc/sendmail.cf 中的 SMTP 和 accept 命令

SMTP 命令允许远程用户验证服务器上的电子邮件。accept 命令扩展别名列表：本地地址和别名应被视为机密或敏感。要关闭这些命令，更改 /etc/sendmail.cf 并搜索 PrivacyOptions 行。将其改为：

`PrivacyOptions=none`

none 是匿名、无接受、无访问的简写。每个隐私选项的完整描述可以在 Sendmail Book 中找到。要使用 m4 设置此，将以下内容添加到构建宏（对于 Red Hat Linux，这是 /usr/lib/sendmail-cf/cf/redhat.mc）并重建 /etc/sendmail.cf：

```
define(PRIVACY_FLAGS, `none`)
```

此示例步骤如下：

```bash
[root]# cp /etc/sendmail.cf /etc/sendmail.cf
[root]# cd /usr/lib/sendmail-cf/cf
[root]# echo "PRIVACY_FLAGS, `none`" >>redhat.mc
[root]# m4 redhat >/etc/sendmail.cf
[root]# /etc/rc.d/init.d/sendmail stop
[root]# /etc/rc.d/init.d/sendmail start
```

## 第 4 步
## 安全服务器网络配置

## 步骤 4.4.2. 定义允许转发邮件的主

Sendmail V8.9 有内置停止邮件转发的检查。使用不知情的邮件服务器转发未经请求的邮件是垃圾邮件者的常用做法。组织邮件服务器允许组织内部的转发。转发通过访问数据库控制，在 Red Hat Linux 中位于 /etc/mail/access。其他发行版可能通过 /etc/mail/relay-domains 控制转发。下面讨论了两种方法。

### 步骤 4.4.2.1. 检查访问数据库是否激活

为了确保 sendmail能够使用访问数据库，检查 /etc/sendmail.cf 中的数据库名称：

```bash
[root]# grep access /etc/sendmail.cf
access -o /etc/mail/access
```

如果没有找到该行，添加此功能的唯一方法是使用 m4 宏 FEATURE('access_db')。参见步骤 4.4.1 中的示例。

如果你的发行版使用的是 relay-domains 文件，请检查 sendmail 是否正在使用该文件：

```bash
[root]# grep relay-domains /etc/sendmail.cf
relay-domains -o /etc/mail/relay-domains
```

如果没有找到该行，请编辑 /etc/sendmail.cf 并按上述所示方式添加该行，创建 relay-domains 文件并重启 sendmail 守护进程。

```bash
[root]# touch /etc/mail/relay-domains
[root]# chmod 600 /etc/mail/relay-domains
[root]# /etc/rc.d/init.d/smtp restart
```

## 步骤 4.4.2.2. 为允许的域名设置访问

访问数据库具有简单的“键值”格式：键是完全限定的主机、子域名、域名或网络；值是操作，REJECT、DISCARD、OK、RELAY 或任意消息。只有具有 RELAY 操作的主或域名被允许使用邮件服务器作为转发。例如，如果你的域名是 example.org，且你的服务器还处理 128.184.x 网络上所有主邮件，编辑 /etc/mail/access 为：

```
example.org              RELAY
128.184.x               RELAY
```

对于使用 relay-domains 的发行版，相反，应向 /etc/mail/relay-domains 文件添加内容，仅包含允许通过服务器转发邮件的主机和域名，不再包含其他。记住在修改数据库后重启 sendmail 守护进程。

关于转发和反垃圾邮件配置控制的更多信息可以在 http://www.sendmail.org/m/readme.html 找到。

## Steps 4.4.3. 设置域名伪装

许多组织倾向于为所有人员设置统一地址，例如 Joe.Schmo@example.org。某些客户端可以设置为在所有发送邮件上使用统一地址，但即使是小小组的所有邮件客户端也很麻烦。sendmail 可以配置为重写所有发送邮件的头部，使其伪装成中央服务器。要定义伪装地址，编辑 /etc/sendmail.cf 并查找 1-2 列的 DM：

DMexample.org

或者，为了完整，使用 m 宏并添加以下内容：

```
MASQUERADE_AS ('example.org')
FEATURE(masquerade_entire_domain)
FEATURE(allmasquerade)
FEATURE(masquerade_envelope)
```





### 步骤 4.4.4. 安装替代 MTA

有多个邮件传输代理（MTA）可以替换 sendmail。两个流行的替代方案是 David Bernstein 开发的 Qmail (www.qmail.org) 和 Wese Venena 开发的 Postfix (www.postfix.org)。这两种 MTA 在设计和编写之初就充分考虑了安全性和性能。获取如何安装和配置这些替代方案的详细信息已超出本指南的范围；互联网上有大量丰富的信息。

## 步骤 4.4.5. 加固 POP 和 IMAP 守护进程

对于收集组织所有入邮件的邮件服务器，将邮件交付给客户端的常用方法是让它们使用邮局协议 (POP) 或互联网消息访问协议 (IMAP) 获取邮件。POP 是两个协议中较旧且更简单的，提供了身份验证、检索和从邮件服务器删除邮件消息的基本命令。IMAP 则更加灵活，支持创建、删除和重命名邮件文件夹（邮箱）、选择性检索消息属性等。

### 步骤 4.4.5.1. 获取最新版本的 POP 和 IMAP 守护进程

许多 POP 和 IMAP 守护进程实现一直受到漏洞的困扰，这些漏洞会导致许多平台上的服务器被 root 攻破。目前有几个已知的利用程序可以破解有漏洞的 Linux POP 和 IMAP 守护进程。希望大多数问题已经被发现并修复，在服务器上拥有最新版本的守护进程程序是非常重要的。

### 步骤 4.4.5.2. 使用 TCP wrappers 控制对 POP 和 IMAP 的访问

POP/IMAP 传统运行在 inetd 中，因此通过 TCP wrappers 进行访问控制既简单又重要。将访问限制为仅对该服务有合法需求的主机。一个持有整个 example.org 域和 128.184 网络邮件、并通过 POP 3 或 IMAP 向客户端交付邮件的邮件枢纽，请在 /etc/hosts.allow 中写入此内容（回想步骤 3.21，而 /etc/hosts.deny 仅包含 "ALL: ALL" 以默认拒绝所有服务）：

```
ipop3d   .example.org 128.184.
imimapd   .example.org 128.184.
```

![](img/0aaa698c422b2f7ffe93bff50cbbef96_62_0.png)

## 步骤 4 加固服务器网络配置

### 步骤 4.4.5.3. 安装替代的 POP 或 IMAP 守护进程

有多个替代守护进程。最流行的之一是来自高通公司的 Qmail。此版本支持 POP3 扩展、APOP 和 Kerberos。查看附录获取 Qpopper 主页的 URL。在编写时，当前的稳定版本为 2.5，3.0 版本处于测试发布阶段。一个流行的 IMAP 守护进程替代品是来自卡内基梅隆邮件项目的 Cyrus。查看附录 A 获取有关如何找到这些软件包的信息。

### 步骤 4.4.5.4. 为安全的 POP/IMAP 连接安装 SSL 封装

有多个第三方程序可以使用安全套接层 (SSL) 封装 TCP 服务，以提供强身份验证和端到端加密。列表请参见 http://www.openssl.org/related/apps.html。两个用于提供安全 POP/IMAP 连接的实用应用程序是 stunnel 和 sslwrap（这些软件包参见附录 A）。这两个软件包都需要 OpenSSL 软件包。有关下载和编译的信息请参见步骤 4.9。

## 步骤 4.5 打印服务

Red Linux 自带了伯克利行打印机系统。在过去的几年里，在连接的客户端 `lpr` 和 `lp` 命令中都发现了缓冲区溢出漏洞。如果你运行的是早于 6.0 版本的 Red Linux，最好更新到最新的 lpr 软件包。

### 步骤 4.5.1. 在 /etc/hosts 中列出允许的远程主机

通过在 /etc/hosts 中列出允许使用此打印服务器的主机名称，与 BSD "r" 程序、rsh、login 等结合使用具有严重影响（参见步骤 4.2 了解如何用 SSH 替换 "r" 程序）。

### 步骤 4.5.2. 用 LPRng 替换伯克利 lpr/lpd

伯克利 lpr/lpd 系统的流行替代方案是 LPRng。它符合 RFC1179 关于网络打印的要求，为管理员定义特定操作的权限提供了极大的灵活性，并支持通过 Kerberos 和 PGP 进行身份验证。Debian 已经内置了 LPRng，这些发行版的管理员可以跳过安装步骤。

![](img/0aaa698c422b2f7ffe93bff50cbbef96_63_0.png)

### 步骤 4.5.2.1. 下载并安装 LPRng

最新稳定版本的链接可以在 http://www.sourceforge.com/LPRng.html 找到。下载此版本，并从压缩文件中提取文件。按照源目录下 INSTALL 文件中的说明编译并安装 LPRng。

### 步骤 4.5.2.2. 设置允许访问的远程主机和/或网络

/etc/lpd.perms 文件控制对特定主机或网络的访问，同时也控制特定的操作，例如，可以允许或拒绝特定用户从打印队列中删除作业。LPRng 安装的默认 /etc/lpd.perms 带有详细注释，且软件包附带了大量文档。查看 lpd.perms(5) 手册页获取有关权限配置文件的更多信息。

要限制 lpd 仅 example.org 域下的 128.184 访问，请在 /etc/lpd.perms 中写入内容：

```
REJECT SERVICE=X NOT REMOTEIP=128.184
REMOTEHOST=*.example.org
```

## 4.6 网络系统

NFS 由其设计本身就存在一些严重的安全问题。RPC 服务依赖于 UID/GID 授权，而这些都是很容易被伪造的。NFS 协议通过 Secure RPC 进行了增强，但到目前为止还没有 Secure RPC 实现。

Red Hat 6.0 已从“用户空间” NFS 实现转向了“内核空间”实现。最近在用户空间 NFS 代码中发现了漏洞。Red Hat 6.0 附带的内核空间代码存在一个错误，导致非 Linux 系统无法挂载目录。请访问 ftp.kernel.org/pub/linux/devel 获取最新版本，它修复了此问题。

![](img/0aaa698c422b2f7ffe93bff50cbbef96_64_0.png)

### 步骤 4.6.1. 在 /etc/hosts.allow 中设置 RPC 服务

RPC 服务通过 portmap 进程注册并访问。Linux 发行版提供的 portmap 使用 TCP wrapper 来允许或拒绝 RPC 服务（如 NFS）。与其它 TCP 封装服务的区别在于，来自本地主机的请求总是授权的，无论 hosts.allow 或 hosts.deny 文件如何设置。portmap 没有主机名查找，因此 hosts.allow 必须指定 IP 地址或子掩码。

例如，允许 client1.example.org 和 client2.example.org 访问 NFS，IP分别为 192.168.1.10 和 192.168.1.11，以及整个 128.184 网络，但在 /etc/hosts.allow 中写入：

```
portmap: 192.168.1.10 192.168.1.11 128.184.0.255.255
```

### 4.6.2. 使用特定权限限制导出导出

/etc/exports 文件控制哪些目录用于 NFS 挂载以及允许挂载的主机。格式为：

```
exported-dir      [host] (options)
```

如果不提供主机，该目录将导出到互联网上的任何主机，请务必提供主机名，并记住该主机的 IP 地址必须与 /etc/hosts.allow 中的匹配。

除非有其他理由，否则使用 "ro" 选项以读模式导出目录。导出目录的文件权限由远程主机挂载目录的用户 UID/GID 决定。如果远程主机被攻破，攻击者可以模拟任何所需的 UID/GID。因此，读写导出 NFS 目录上的任何文件都可以被创建、修改或删除。NFS 服务器管理员不应允许其控制之外的主机访问 NFS，除非是只读模式。

如果可能，避免使用 NetWare 服务器来挂载任何 Unix 文件系统、Linux、Solaris，因为 NetWare NFS 服务存在重大安全问题，例如无论导出限制如何都具有读写权限。

查看 exports (5) 手册页详细了解 /etc/exports 的选项。





## 第 4 节 保护服务器网络配置

## 第 4.7 节 服务器消息块 (SMB) SAMBA 服务器

SMB 协议是微软开发的用于文件和打印机共享的通用网络文件系统（CIFS）的核心。Samba 的理念是让 UNIX 服务器在网络邻域中的客户端看来与任何 NT 服务器完全相同。安装 Samba 软件本身相对简单，但要将其成功集成到办公环境中还有许多细节需要注意。Samba 服务器管理员应审阅随服务器提供的详尽文档，以及书籍《Samba: Integrating UNIX and Windows》（Blair, SSC, Inc. ISBN 1-57831-006-7）。

### 第 4.7.1 节 获取最新版本的 Samba

截至本文编写时，Red Hat 6.0 版本已发布了 Samba 的更新包以修复问题。请检查你发行版的更新，并确保你已安装 Samba 2.0.5a 或更高版本。

### 第 4.7.2 节 限制对特定主机的访问

编辑 `/etc/smb.conf` 中的 `[global]` 部分，设置允许访问 Samba 服务器的主机列表以及 Samba 服务器监听的接口：

```
hosts allow = .example.org 128.184.
interfaces 192.168.0.1/24 127.0.0/32
bind interfaces only = true
```

### 第 4.7.3 节 使用加密密码

在设置 Samba 使用加密密码之前，请阅读 `/usr/doc/samba-2.0.5a/docs/textdocs/ENCRYPTION.txt`。

Red Hat Linux 6.0 默认在 `/etc/smbpasswd` 中查找 Samba 密码。其他发行版可能使用 `/etc/samba.d/smpasswd` 或完全不同的路径。该路径定义在配置文件 `/etc/smb.conf` 中。你可以通过以下命令创建一个模板 `/etc/smbpasswd`：

```
[root]# mksmbpasswd.sh < /etc/passwd >/etc/smbpasswd
[root]# chmod 006 /etc/smbpasswd
```

编辑该模板以移除 `bin`、`daemon` 和 `ftp` 等系统账户的条目。管理员应为每个账户设置默认密码。如果你希望用户设置自己的密码，则需要编辑 `/etc/smbpasswd`，在密码字段的前十一个字符中输入字符串“NO PASSWORD”，保留剩余的21个“X”字符。然后通过 `/etc/smb.conf` 的 `[global]` 部分添加以下行来启用空密码：

```
null passwords = true
```

重启 smb 服务器。如果你决定使用这种方法，请只给用户留出很短的时间重置密码。如果截止日期后 `/etc/smbpasswd` 中的任何条目仍包含字符串“NO PASSWORD”，则请为这些用户设置密码。

### 第 4.7.4 节 移除“guest”或匿名共享

Red Hat 6.0 默认的 `/etc/smb.conf` 仅启用了本地主机上每个用户家目录的用户级共享。其他发行版可能启用了其他公共可读的共享。在启用 Samba 之前，请仔细检查 `/etc/smb.conf` 中定义的共享，并禁用任何绝对非必要的共享。对于剩余的共享，仅在绝对必要时允许写入访问。考虑仅为需要权限的用户设置写入权限，而不是为任何连接服务的服务的用户。

### 第 4.7.5 节 设置默认文件创建掩码

默认的文件创建掩码使文件对所有人可读。编辑 `/etc/smb.conf` 并搜索以下行，将掩码改为清除“其他”权限位：

```
create mask = 0770
directory mask = 0750
```

## 第 4.8 节 集中 syslog 主机

如第 2.8.3 节所述，对于拥有多台机器的组织来说，集中日志主机非常重要。它们在保存有关异常和中断的信息及证据方面提供了额外的防御线。由于这一重要的安全功能，日志主机应尽可能安全。除了用于远程管理的 SSH 外，不应在机器上运行或安装任何其他服务。应只安装最少的系统工具集。主机应该有一个大且快速的磁盘专门用于 `/var/log` 目录以收集 syslog。应提供快速、大容量的备份设备。日志轮转（见第 2.8.4 节）应关闭或设置为很长的间隔，并且所有日志文件应保留较长时间。

如上述第 2.8 节提到的，有几种替代的 syslog 守护进程实现，它们比 Red Hat 安装光盘上提供的最常见的 syslogd 更安全。请参阅附录 A 第 2 节获取某些替代方案的参考。

### 第 4.8.1 节 配置 syslog 接受远程日志消息

Red Hat Linux 中大多数 syslog 守护进程的默认行为是不接受日志消息。这与大多数 BSD 风格守护进程的行为相反。要开启此功能，请编辑 `/etc/rc.d/init.d/syslog`，并在启动 syslog 守护进程的行添加 `-r` 选项：

```
start
daemon syslogd -r
```

然后，重启服务：
[root]# /etc/rc.d/init.d/syslog restart

### 第 4.8.2 节 配置日志轮转

如第 2.8.4 节所述，`logrotate` 程序旨在在一段时间后对日志文件进行轮转、保存和删除。当日志文件达到特定大小时，应关闭日志轮转（通过删除 `/etc/cron.daily/logrotate`），或者编辑 `logrotate.conf` 文件以保留日志文件。例如，如果你的组织安全策略要求保留一年的日志，编辑 `logrotate.conf` 将前几行改为：

```
# rotate log files monthly
monthly

# keep years worth of logs
```

## 第 4.9 节 文件传输协议 (FTP)

Red Hat Linux 以及大多数其他发行版都有名为“anonftp”的包，它可以设置具有适当权限的匿名 目录。为了确保安全，检查 `/home/ftp`；`bin` 和 `etc` 目录应由 root 所有，权限为 `111`。

### 第 4.9.1 节 使用 TCP wrappers 限制访问

FTP 守护进程通过 inetd 调用并由 TCP wrappers 保护。如果 FTP 服务器仅对一组机器开放，请在 `/etc/hosts.allow` 中设置限制：

```
.example.org 128.184.
```

FTP 守护进程应对所有人开放：

```
ftpd: ALL
```

### 第 4.9.2 节 在 /etc/ftpaccess 中限制允许的操作

Red Hat 自带的 WU-FTP 守护进程通过 `ftpaccess` 文件进行精细控制。更多信息请参阅 `ftpaccess(5)` 手页。在此文件中，你可以根据用户连接的来源、并发用户数定义用户类，限制类允许的操作等等。

如果需要可写目录（见下文），可以通过在 `/etc/ftpaccess` 中放入以下内容来阻止匿名用户修改内容，无论目录权限如何：

```
```

### 第 4.9.3 节 保护进入的目录

通常情况下，允许匿名 FTP 目录具有写入访问不是一个好主意，但有时必须这样做。这种目录传统上被称为“进入目录”。FTP 守护进程具有许多控制功能，可以帮助防止进入目录变成资源站点。

首先，创建一个可写入但不可进入的进入目录：

```
[root]# mkdir -m 333 /home/ftp/incoming
```

然后，编辑 `/etc/ftpasswd` 并添加这些行：

```
path-filter anonymous /etc/ftpassmsg ^[-A-Za-z0-9]*$ \
^-
upload /home/ftp /incoming yes root ftp 0600 nodirs
nretrieve /home/ftp/incoming/
```

第一行限制了上传名称为字母、数字、连字符、点和下划线，并限制文件名以点或连字符开头（因此匿名用户无法创建一个名为例如等的文件）。第二行表示允许上传到进入目录的文件，这些文件将具有 UID GID ftp，模式为 0600，且不允许用户创建子目录。最后一行完全禁止从进入目录下载内容，因此一旦文件被写入那里，另一个匿名用户就无法获取它。





## 第 4.10 节 超文本传输协议 (HTTP) 服务器

所有主要的 Linux 发行版都带有 HTTP 服务器软件。Apache 的设计具有灵活性，并拥有丰富的功能。在 Red Hat Linux 中，大多数与安全的设置位于 /etc/httpd/conf 中的主配置文件中。`httpd.conf` 文件设置 HTTP 守护进程的基本运行参数，`access.conf` 设置访问规则；`ssl.conf` 设置基本的服务器配置参数，如文档根、允许的目录、CGI 脚本请求以及索引图标。

请参阅 Red Hat 6.0 附的 Apache 手册，特别是[安全提示](http://localhost/manual/misc/security_tips.html) 以及关于章节如何工作的[说明](http://localhost/manual/sections.html)。Apache 手册也可以通过 Apache 网站 http://www.apache.org/docs/ 获取。

- 第 4.10.1 节。将基础访问设置为默认拒绝（default deny）

```
access.conf, 将根目录的访问和选项设置为：
```
<Directory /
Options None
AllowOverride None
order deny,allow
deny from all
</Directory>
```

默认情况下，对服务器上所有目录和文件的访问都是拒绝的。

- 第 4.10.2 节。选择性地开放特定目录的访问

在 access.conf 的剩余部分中，仅指定绝对必要的访问和选项。对于内网服务器，应允许来自内部网络 IP 地址的访问：

```
<Directory /home/httpd/
Options None
AllowOverride None
order deny,allow
deny from all
allow from 192.168.
</Directory>
```

## 第 4 节 服务器服务器配置

### 第 4.10.3 节。在特定目录上选择性地允许选项

在 <Directory> 指令中设置以下任何 Options 之前，请考虑其带来的影响：

- ExecCGI: 应该只允许 CGI 目录
- FollowSymLinks: 如果用户对 HTML 目录有访问权限，他们可以设置符号链接指向包含敏感数据的区域
- Includes: 服务器端包含（side includes）可用于绕过默认访问限制
- IncludesNOEXEC: Includes 的安全版本，它禁用了 #exec 语句和对 CGI 脚本的 #include
- Indexes: 守护进程将为没有索引文件（index.html）的目录打印目录列表。这可能会暴露通常被隐藏的文件名。

### 第 4.10.4 节。选择性地使用 .htaccess 覆盖访问控制

将 AllowOverride 指令从 None 改为 All 会告诉 Apache 在请求文件所在的目录中查找名为 .htaccess 的文件，并解释该目录中任何默认访问和选项指令的内容。优点是可以动态地设置访问和选项，而无需编辑配置文件并重启服务器。缺点是安全和选项设置不再指定在单处位置，而是分散在整个目录结构中。这可能会使对 网站安全策略的审计变得更加困难。此外，每次访问都会产生性能影响，因为服务器必须为每个请求查找、打开并解释该文件的内容。

### 第 4.10.5 节。对敏感数据使用密码保护

Apache 允许使用用户名/密码身份验证来保护目录和文件。这提供了中等程度的安全性，尽管用户名和密码是以明文在网络上传的，可能会被嗅探。更多信息请参阅本地安装的 Apache 手册，http://localhost/manual/mod/directives.html，关于 AuthType、AuthUserFile 以及其他身份验证指令。

## 第 4 节 服务器网络配置

### 第 4.10.6 节。使用 SSL 进行安全的 HTTP 通信

套接层（SSL）协议为 TCP 套接字提供了强身份验证和端到端加密。它通常与安全的 Web 结合使用。SSL 的开源实现作为 Apache Web 服务器的编译扩展。

**注意：** 美国及其他国家的商业网站管理员可能受到专利法和许可限制，在使用 SSL 的 RSA 加密软件。商业网站运营商应认真考虑购买具备 SSL 能力的商业 Web 服务器。参见附录 A 以确保 Web 的安全。

**同样注意：** 商业网站应拥有受证书机构认可的数字证书。商业证书的两个主要来源是 Thawte Consulting (http://www.thawte.com) 和 Verisign, Inc. (http://www.verisign.com)。

### 第 4.10.6.1 节。下载 OpenSSL 和 mod_ssl

从 SRPM 中提取 Apache 服务器源码，或从 ftp://ftp.apache.org 下载最新版本。下面示例中的版本号是编写本指南时的最新版本。请检查每个包的版本列表。

```
[root] # cd /usr/local/src
[root] # wget http://ftp.apache.org/dist/apache-1.3.6.tar.gz
[root] # wget http://ftp.modssl.org/source/mod_ssl-2.3.10-1.3.6.tar.gz
[root] # wget http://ftp.openssl.org/source/openssl-0.9.3a.tar.gz
[root] # tar xzf apache-1.3.6.tar.gz
[root] # tar xzf mod_ssl-2.3.10-1.3.6.tar.gz
[root] # tar xzf openssl-0.9.3a.tar.gz
```

### 第 4.10.6.2 节。构建 OpenSSL

OpenSSL 的 Makefile 假设 Perl 解释器位于 /usr/bin/perl5。要么修改 Makefile 更改为 /usr/bin/perl，要么在命令行中重新定义它。

```
[root] # cd openssl-0.9.3a
[root] # make PERL=/usr/bin/perl
[root] # ./Configure
[root] # make
```

### 第 4.10.6.3 节。使用 mod_ssl 构建 Apache

直接从 mod_ssl 目录完成 Apache 使用 mod_ssl 的配置：

```
[root] # cd mod_ssl-2.3.10-1.3.6
[root] # ./configure --with-apache=../apache_1.3.6 \
--with-ssl=../openssl-0.9.3a --prefix=/usr/local/apache
[root] # cd ../apache_1.3.6
[root] # make
[root] # make TYPE=test
[root] # make
```

### 第 4.10.6.4 节。启动带 mod_ssl 的 Apache 并测试

在启动 SSL 版本的 Apache 之前，停止旧的守护进程。

```
[root] # /etc/rc.d/init.d/httpd stop
[root] # /usr/local/apache/sbin/apachectl startssl
```

从另一台主机测试服务器，输入：

```
[root] # netscape://server-name/
```

在 netscape 提示接受证书后，应显示“It Worked!”的屏幕。

### 第 4.10.6.5 节。阅读 mod_ssl 文档

仔细阅读 https://server-name/manual/mod/mod_ssl/。你可能特别想阅读此手册中的 FAQ 以学习如何创建数字证书。

## Linux 安全分步指南版本 1.0

## 第 5 节 调整与数据包防火墙

## 第 5.2 节 系统优化

开箱即用的 Red Hat 以及大多数发行版没有充分利用现代硬件。通过最小化优化，Linux 可以在更旧的硬件上运行。通过一次调整一步，可以保持可靠性和提高性能。

### 第 5.2.1 节。TCP/IP 接收窗口大小

TCP/IP 确认（ACK）接收窗口或 RWIN 默认值为 0。对于现代以太网和快速以太网，这不是最优的。要修复此问题，请编辑 /sbin/ifup 并以下更改：

- 行 110：route add -net $(NETWORK) netmask $(NETMASK) $(DEVICE)
route add -net $(NETWORK) netmask $(NETMASK) window 16384 $(DEVICE)

- 行 112：route add -host $(IPADDR) $(DEVICE)
route add -host $(IPADDR) window 16384 $(DEVICE)

- 行 117：route add default gw $(GATEWAY) metric 1 $(DEVICE)
route add default gw $(GATEWAY) window 16384 $(DEVICE)

- 行 125：route add default gw $(GATEWAY) $(DEVICE)
route add default gw $(GATEWAY) window 16384 $(DEVICE)

- 行 134：route add default gw $gw $(DEVICE)
route add default gw $gw window 16384 $(DEVICE)





## 第 5 步 调整与数据包防火墙

## 第 5.3 步 数据包防火墙与 LINUX 伪装 (MASQUERADING)

运行着配置良好的防火墙的 Linux 服务器是保护本地服务器及其背后的内部网络最有效的方法之一。Linux 2.2.x 内核具有非常稳定的防火墙实现，它通过一个名为 `iptchains` 的工具进行管理。该工具允许管理员灵活地定义允许进入和离开防火墙的流量类型。然而，在 2.2.11 版本之前的内核在 IP 分段代码中存在一个漏洞，允许攻击者发送经过精心构造的 IP 分段，从而绕过 `iptchains` 规则。我们在编写本文时，建议企业系统的管理员安装最新版本的内核（版本 2.2.12）。

防火墙技术本身就是一门学问（例如，“*Building Internet Firewalls》，Chapman & Zwicky, 1995, O'Reilly & Associates, ISBN 1-56592-124-0），且远超本指南的范围。请参阅“资源”部分以获取 IPCHAINS 和 IP-MASQ HOWTO 的 URL，进行深入讨论。

### 第 5.3.1 步 通过外部连接实现 IP 伪装以获取更多功能

防火墙可以很好地保护独立服务器，也可以保护内部计算机。这种配置的一个常见例子是个人或公司将家中的/办公室网络连接到互联网。这里的复杂之处在于，互联网上使用的 TCP/IP 地址正成为一种稀缺且昂贵的资源。因此，为所有内部计算机获取 TCP/IP 地址可能会花费一些费用。网络地址翻译 (NAT) 的开发是为了在节省 TCP/IP 地址的同时，仍允许内部计算机访问互联网。对于 Linux，开发出了一种名为 `Masquerade`（伪装）的 NAT 形式，许多 Linux 用户都在广泛使用它。

### 第 5.3.2 步 一个强有力的 /etc/rc.d/rc.firewall 规则集

请参阅附录 D 获取通过以太网连接到电缆调制解调器或其他持久网络连接到互联网的 IP 伪装机器的强数据包防火墙脚本完整列表。其中包含大量的嵌入注释，用于解释各种规则的作用以及如何修改这些规则以适应你的特定需求。

### 第 5.3.3 步 检查、安装并测试防火墙

一旦将 `/etc/rc.d/rc.firewall` 规则集复制到机器中，针对你的特定环境进行定制至关重要。确保内部和外部接口的名称正确。确保你内部网络的 TCP/IP 命名方案配置正确。

接下来，测试规则集以确保它在没有错误的情况下加载，不会阻塞你环境中所需的任何特定流量，并且在服务器每次重启时都会加载。

### 第 5.3.3.1 步 赋予规则集具有可执行权限

为了能够运行规则集，你需要将 `/etc/rc.d/rc.firewall` 脚本设置为可执行文件：

```bash
[root]# chmod 700 /etc/rc.d/rc.firewall
```

### 第 5.3.3.2 步 在 Linux 服务器控制台处加载规则集

如第 2.8 步所示，监控 VTY7 和 VTY8 上的控制台日志。如果防火墙脚本运行没有任何可见可见错误，系统应该立即开始拦截你想要的流量。控制台日志将向你显示哪些流量被拦截了，哪些没有。

当你执行 `/etc/rc.d/rc.firewall` 时，脚本的输出可能如下：

```bash
[root]# /etc/rc.d/rc.firewall
```

#### 加载 IPCHAINS 防火墙版本 3.12

外部 IP: 192.168.0.14
外部广播: 192.168.1.255
默认网关: 192.168.0.1

- 添加组播路由。
- SIOCADRT: 文件存在
- 启用 IP 转发。
- 启用动态 TCP/IP 地址欺骗。
- 修改 IP 伪装超时。
- 加载伪装模块。
- 清空所有旧规则并将所有默认策略设置为 REJECT（拒绝）

输入规则：

- 为来自内部局域网的流量设置输入过滤器。
- 为特定的内部主机设置输入过滤器。
- 为外部接口的流量设置输入过滤器。
- 为公共服务（所有接口）设置输入过滤器。
- 为显式的外部主机设置输入过滤器。
- 最终输入全部捕获规则。

输出规则：

- 为内部局域网的流量设置输出过滤器。
- 为特定的内部主机设置输出过滤器。
- 为指向外部接口的流量设置输入过滤器。
- 为公共服务（所有接口）设置输出过滤器。
- 拒绝特定的输出。
- 为显式的外部主机设置输出过滤器。
- 最终输出全部捕获规则。

转发规则：

- 启用来自内部局域网的 IP 伪装。

防火墙已实施。

### 第 5.3.3.3 步 测试防火墙规则集

在 Linux 服务器控制台处，尝试使用各种网络应用（如 TELNET、FTP、SSH 等）连接到互联网和内部局域网上的计算机。如果测试良好，请尝试在其中一台计算机上进行类似的测试。如果由于任何原因机器没有正常响应，请检查 `/var/log/messages` 文件或在控制台上观察 VTY7 上的防火墙命中记录。

### 第 5.3.4 步 分析典型的 IPCHAINS 规则集

现在你开始在 `/var/log/messages` 中看到 `IPTABLES` 了。现实中，这种情况发生是因为你的规则集对你的环境来说过于严格，或者它正在正常工作。





## 步骤 6 工具

要从命令行检查 `/var/log/messages`，请执行：

```bash
[root]# swatch -c testrc -f /var/log/messages
*** swatch-2.2.2 (pid:323381) started at Fri Jul 25 15:12:08 1999
Jul 25 10:32:42 localhost sshd[16508]: refused connection from 192.168.1.1
Jul 25 10:33:31 localhost sshd[16530]: log: Rsa authentication refused for bad modes for /root/.ssh/authorized_keys
Jul 25 20:11:22 localhost sshd[2312]: error: Fwd X11 connection from 127.0.0.1 refused by tcp_wrappers.
```

在 Red Hat 下，控制文件的起点是 `/usr/doc/swatch-2.2/config_files/swatchrc.personal`。它由一组用于生成操作的正则表达式列表组成，随后是一组要忽略的正则表达式列表，最后的操作是默认回显所有其他内容。通过添加操作和忽略项并反复遍历 `/var/log/messages`，可以对该文件进行调优，直到获得可以管理的结果为止。

Swatch 可以配置为单次通过单个日志文件运行，也可以作为守护进程运行，持续监控新记录的日志消息。它可以被配置为使用不同的控制文件来监控邮件日志、防火墙日志、Samba 日志等。更多信息请参阅 `swatch(8)` 的手册页。

### 步骤 6.1.2. Psionic Logcheck

在许多日志文件监控器中的另一个是来自 Psionic Software Systems 的 Logcheck。请参阅附录 A 获取 Psionic Logcheck 主页以及 MetaLab 站点中其他日志监控器的 URL。

Logcheck 带有完善的文档。在安装和运行它之前，请彻底阅读 `INSTALL` 文件。安装非常简单。解压压缩文件后，在源目录下执行 `make linux` 以将 Linux 特定的配置文件和脚本复制到 `/usr/local/etc/`。

Logcheck 生成的报告包含三个部分：系统攻击、安全违规和异常系统事件。系统攻击警告是由匹配 `logcheck.hacking` 中任何模式的 syslog 日目生成的；安全违规由 `logcheck.violations` 中的模式生成；而异常事件则由任何不匹配 `logcheck.ignore` 中模式的行生成。阅读 `logcheck.sh` 中的注释以获取有关这些配置文件的更详细描述。

在使用 swatch 时，管理员需要耐心和坚持，以剔除那些未指示真实事件的记录，并将模式添加到 `logcheck.ignore` 中。起初，可能会有很多虚假警报。调查每个报告的实例，以确定所报告的事件是否需要关注。如果不需要，可以将匹配该事件的模式放入 `logcheck.ignore` 中，这样你就不会再看到它了。最好的方法是让模式尽可能具体，这样事件的异常变体就会被报告出来。

### 步骤 6.1.3. Tripwire

Tripwire 最初由普渡大学（University of Purdue Academic）的 Gene Kim 和 Gene Pfaff 开发。Tripwire 背后的理念是：为了成功入侵系统，必须更改、添加或删除文件，以放置后门、木马和利用脚本。Tripwire 为重要的系统二进制文件和配置文件生成加密签名数据库，并记录这些文件中任何随时间推移的变化。

请参阅附录 A 获取 Tripwire 1.3 版本和 2.0 版本源码的 URL。但必须注意的是，Tripwire 2.0 不支持 Red Hat 6.0，仅支持之前的版本。截至编写时，只有 Release 1.3.1 适用于 Red Hat 6.0。阅读每个版本附带的文档获取有关编译、安装和维护 Tripwire 的信息。

#### 步骤 6.1.3.1. Tripwire 数据库

在 Tripwire 之前，测试系统文件完整性的唯一方法是检查 CRC 校验和。遗憾的是，CRC 位校验和很容易被伪造。Tripwire 构建了一个加密校验和数据库（如 MD5），这些校验和几乎无法伪造，并定期进行检查。如果校验和失败，则强有力地表明相关文件已被修改。

Tripwire 最大的弱点是，如果攻击者能够获得机器的权限，他可能会修改或重建 Tripwire 数据库以掩盖他的入侵。针对此唯一的防御方法是将数据库放在只读介质上，例如写保护的软盘或 CD。版本 2 中最重要的创新之一是对数据库和配置文件进行加密签名，这消除了对将 Tripwire 数据库放在只读介质上的需求。希望在发布此版本时已经支持了 Red Hat 6.0。

#### 步骤 6.1.3.2. 运行 Tripwire

第一次运行 Tripwire 时，它会为配置文件列出的文件和目录构建一个校验和和其他信息（UID、GID、模式、大小等）的数据库。之后每次运行时，它会将数据库中的信息与系统的当前状态进行比较。然后当通过命令行进行交互式运行时，它会提供更新每个更改文件的数据库的选项。因此，如果 `/etc/group` 发生了变化且你是你更改它的，你可以更新数据库，这样在下次发生变化（可能由攻击者引起）之前，你不会收到通知。

#### 步骤 6.1.3.3. 使用 rpm 验证包文件

Red Hat 软件包管理器 (rpm) 在安装包时构建的数据库包含了 MD5 校验和、UID、GID、模式、大小等。你可以使用 rpm 将数据库内容与磁盘上文件的当前状态进行验证，并报告任何不同的文件。这与 Tripwire 方法不同，因为使用 rpm 无法测试安装以来的变化，无法在管理员知情和批准的情况下更新数据库条目。

要验证所有包文件，请运行：

```bash
[root]# rpm -Va
S.5....TC /etc/exports
S.5....TC /etc/hosts.allow
S.5....TC /etc/hosts.deny
M....UG /mnt/cdrom
```

`/etc` 中文件的条目告诉你 MD5 校验和和修改时间已更改；对于 `/mnt/cdrom`，模式、用户和组组发生了变化。

### 步骤 6.1.4. Psionic PortSentry

有多种工具可以检测端口扫描，而 Psionic PortSentry 增加了一个意料之外的转折：当检测到扫描时，它可以立即采取行动，阻止扫描主机对机器的任何进一步访问。它与 Psionic Logcheck（步骤 6.1.2）结合良好。请参阅附录 A 获取其主页的 URL。

PortSentry 带有完善的文档。在编译和安装之前，请彻底阅读 `README.install`、`README.methods` 和 `README.qa`。PortSentry 无需任何更改即可“开箱即用”编译。程序和配置文件默认安装在 `/usr/local/psionic/portsentry`。

PortSentry 不仅可以检测简单的 TCP 连接类型扫描，还可以检测许多类型的隐身扫描，例如 SYN/半开、FIN 和 NULL 扫描。

在运行 PortSentry 之前，请检查 `portsentry.conf`。所有条目在配置文件和 `README.install` 中都有说明。针对扫描主机唯一的操作是在 `/etc/hosts.deny` 的末尾添加：

```
ALL: <attacker-IP>
```

由于你在 `/etc/hosts.deny` 的末尾已经有了 "ALL: ALL"，因此这样做是无效的。事实上，如果在 `/etc/hosts.allow` 中允许了攻击主机访问任何服务，那么这种方法完全无效无效，因为 TCP wrappers 在读取 `/etc/hosts.deny` 之前会先读取 `/etc/hosts.allow`。





## 步骤 6.2 基于主机的漏洞分析：从内向观察

### 6.2.1. Tiger，德州 A&M 系统检查器

Tiger 是一个检查 UNIX 计算机安全相关系统的工具。Tiger 最近进行了升级（自 1994 年以来首次），以支持对 Red Hat Linux 系统的检查。Tiger 主页的 URL 和源代码请参阅附录 A。

### 6.2.2. 安装并配置 Tiger

安装非常简单：解压压缩的 tiger 文件并执行 `make install`。这将配置和脚本文件放置在 `/usr/local/tiger` 中。Makefile 不会创建 Tiger 依赖的中间目录，因此在安装后请执行以下命令：

```
[root]# mkdir -m 700 -p /var/spool/tiger/bin
[root]# mkdir -m 700 -p /var/spool/tiger/logs
[root]# mkdir -m 700 -p /var/spool/tiger/work
```

此外，如果你运行的是默认的 Bash 2，将需要编辑 `/usr/local/tiger/systems/linux2/config` 并注释掉以 "GROUPS" 开头的行。在 Bash 2 中，GROUPS 是一个只读变量，如果脚本尝试给它赋值将将终止。

Tiger 执行的检查列在 `/usr/local/tiger/tigerrc` 中。源码目录中有几个 `tigerrc` 文件，并且附有详细的注释。默认的 `tigerrc` 几乎尝试测试其中的所有内容。对于 Red Hat Linux 版本 6，大多数检查都将如预期那样工作，签名检查除外。你可以通过编辑 `tigerrc` 将 `Tiger_Check_SIGNATURES=Y` 修改为 `Tiger_Check_SIGNATURES=N` 来关闭它。同样，你可以通过编辑 `Tiger_Run_CRACK` 条目来关闭对密码文件运行 Crack。

### 6.2.3. 运行 Tiger

运行 Tiger：

```
[root]# cd /usr/local/tiger
[root]# ./tiger
```

在 Tiger 运行检查期间，标准输出上会打印许多信息。当运行完成后，结果将存储在 `/var/spool/tiger/logs/security.report.<host>.<domain>.<date>-<time>` 中。准备好第一份安全报告会有大量信息。报告的问题看起来如下：

- -WARN- [acc001w] 登录 ID postgres 已禁用，但仍具有有效的 shell (/bin/bash)。
- -FAIL- [perm007f] /etc/aliases 不应有组读权限。
- -FAIL- [perm007f] /etc/aliases 不应有世界读权限。

WARN 条目表示某些不理想的内容，但并不糟糕。FAIL 条目表示 Tiger 认为你应该更改的内容。方括号中的字符串指示如何使用 `tigexp` 程序获取有关特定警告的更多信息：

```
[root]# ./tiger acc01w
```

列出的登录 ID 以某种方式被禁用（`passwd` 字段中为 `**` 等），但该登录 ID 的登录 shell 是一个有效的 shell（来自 `/etc/shells` 或系统等效项）。有效的 shell 可能会允许该登录 ID 继续使用。应该将登录 shell 更改为不存在的内容，或者类似于 `/bin/false` 的内容。

## 步骤 6 工具

### 6.2.4. 修改 Tiger 检查项

通过查看安全报告，你可能会发现一些你认为完全没问题的警告和失败。Tiger 用于比较的基础信息可以在 `/usr/local/tiger/systems/Linux/2` 中找到。例如，`file_access` 列表包含了许多系统文件的建议所有权和位位。如果你发现 `/etc/aliases` 允许组读和世界读权限，你可以编辑此文件以设置适当的模式位，这样你将不会再收到关于这些权限的 FAIL 消息。

再次强调，这里需要耐心和坚持。遵循安全报告中建议的更改，并明智地修改基础信息，直到 Tiger 的安全报告为你的站点返回最有意义的信息。

### TARA，Tiger 的更新版本

由于 Tiger 最近才开始有新的开发，Advanced Research Corporation 获取了基础代码并对其进行了增强，生成了 Tiger 分析研究助手 (TARA)。此处附加 TARA 主页的 URL。

TARA 的安装、配置和操作与原始 Tiger 完全相同，甚至目录名称也相同。请注意，默认的 `tigerrc` 启用的系统比 Tiger 少且速度更快。在运行 TARA 之前检查此文件，并启用与你相关的检查。

## 步骤 6.3 基于网络的漏洞分析：从外向观察

有许多工具旨在扫描网络上的主机以开放端口、通用安全漏洞或特定的可利用服务。在进行任何网络扫描之前，最重要的事情是保护好自己的安全……如果可能的话，获取执行扫描的授权。政府和商业机构对于谁可以执行扫描、扫描范围以及哪些可以和不能被扫描有特定的政策。未经授权而违反这些政策可能导致制裁、失业以及任何法律行动。

获得授权后，发布通知告知将进行扫描以及何时进行。某些管理员认为，让其他人知道即将到来的扫描会给用户提供一个预先修补漏洞的机会，从而偏斜扫描结果。嗯，至少结果是在正确的方向上被偏斜了，而且你将避免本地用户的入侵检测程序意外触发红警引起的问题。

在扫描之前，在隔离的网段上运行扫描软件，以确保扫描工具不会对所扫描的机器产生负面影响。扫描完成后，发布通知告知扫描结果以及哪些机器被扫描了。在Nessus 扫描后，总结发现的漏洞信息。此外，Nessus 扫描器在扫描机器方面是非常高效的。

### 6.1. SATAN 的衍生品：SARA 和 SAINT

网络分析安全工具 (SATAN) 在 1994 年由 Dan Farmer 和 Wiest 发布时引起了轰动。它使用 Web 技术具有了一种创新的用户界面，扫描已知漏洞和利用程序。然而，这种设计允许对其进行增强。SATAN 的两个更新版本可用：安全审计研究助手 (SARA) 以及安全管理员集成工具 (SAINT)。

这两个版本都处于活跃开发中。获取最新的 SATAN 版本，请咨询 SARA 或 SAINT。

### 6.3.2 Nessus

Nessus (http://www.nessus.org) 是一种使用客户端/服务器架构的开源扫描器。Nessus 守护进程 `nessusd` 运行扫描并检查，由具有 Gtk GUI 界面的客户端控制。Nessus 拥有用于执行漏洞测试的“插件”库。目前有 208 个插件，测试诸如 IMAP 和 RPC 溢出、CGI 脚本、RPC 服务以及一系列拒绝服务攻击。

编译和安装非常简单：

```
[root]# ./configure; make; install
```

必须先运行 `nessusd` 服务器。当 `nessusd` 首次运行时，它会创建一个主机密钥并构建默认用户文件 `/usr/local/nessus/nessus.users`。该文件控制谁可以连接到服务器。要为 root 添加条目，再次运行 nessusd：

```
[root]# nessusd -P root,pass
```

其中 `pass` 是初始密码。启动客户端 `nessus`，你必须连接到服务器。在“Login:”窗口中输入“root”并点击“Log in now!”只有在第一次登录时才会提示输入上述密码，之后对于所有后续登录将生成私钥。

请注意，Nessus 默认测试拒绝服务漏洞，我们的测试表明，如果启用此选项，你可能会崩溃你扫描的每台机器。在执行扫描之前，转到 Plugins 标签并禁用 Denial of。

扫描完成后，Nessus 会弹出一个报告窗口显示每个扫描主机的信息。安全问题用红色圆点标记，关注区域用黑色圆点标记。在这两种情况下，都会打印简要描述。报告可以保存到磁盘以便日后研究和比较。





## Step 6.3.3 Nmap 端口扫描器

Nmap 扫描主机的开放端口。与 SARA/SAINT 和 Nessus 不同，它不测试特定的漏洞。Nmap 可以从 http://www.insecure.org/nmap/ 免费获取。它有很多扫描选项：TCP connect() 扫描、SYN 半开、FIN、NULL、UDP、ICMP，以及带有 IP 分片的 SYN/FIN 扫描，以绕过数据包过滤器。它可以通过使用 TCP/IP 栈指纹来识别主机的操作系统类型。

编译和安装在源目录中运行一样简单。例如，要扫描 localhost 的所有 TCP 和 UDP 端口，以双检你在步骤 3、1、2 和 3 中的工作，执行：

```
[root]# ./nmap -tS -sU 127.0.0.1
WARNING: -SU 现在是 UDP 扫描 - TCP 扫描请使用 -s
```

由 Fyodor 启动 nmap V.2.22-BETA4 (fyor@dhp.com, www.insecure.org/nmap/)
localhost (127.0.0.1) 上的有趣端口：

| 端口 | 状态 | 协议 | 服务 |
|---|---|---|---|
| 21 | open | tcp | ftp |
| 22 | open | tcp | ssh |
| 23 | open | tcp | telnet |
| 25 | open | tcp | smp |
| 80 | open | tcp | http |
| 98 | open | tcp | linuxconf |
| 111 | open | udp | sunprpc |
| 111 | open | tcp | sunprpc |
| 113 | open | tcp | auth |
| 608 | open | udp | sift-uft |
| 610 | open | tcp | npmp-local |
| 618 | open | udp | unknown |
| 627 | open | udp | unknown |
| 629 | open | tcp | unknown |
| 632 | open | udp | unknown |
| 634 | open | tcp | ginad |
| 637 | open | udp | unknown |
| 639 | open | tcp | unknown |
| 1024 | open | udp | unknown |
| 1024 | open | tcp | unknown |
| 1026 | open | udp | unknown |
| 2049 | open | udp | nfs |

Nmap运行完成 - 5 秒内扫描了 1 个 IP 地址 (1 个主机)

## 步骤 6 工具

当然，如果你的主机有很多开放的端口，你仍然会有工作要做。若要尝试猜测 192.168.1.1 主机的操作系统，执行：

```
[root]# /nmap -O 192.168.1.1
```

由 Fyodor 启动 nmap V. 2.2-BETA4 (fyodor@dhp.com, www.insecure.org/nmap)
girth (192.168.1.1) 上的有趣端口：

| 端口 | 状态 | 协议 | 服务 |
|---|---|---|--|
| 21 | open | tcp | ftp |
| 23 | open | tcp | telnet |
| 25 | open | tcp | smtp |
| 111 | open | tcp | sunprpc |
| 113 | open | tcp | auth |
| 515 | open | tcp | printer |
| 6000 | open | tcp | X11 |

TCP 序列预测：类别=随机正增量
难度=6118242 (好运!) 2.2.0-pro - 2.2.2
远程操作系统猜测：Linux 2.1.122 - 2.1.132;
Nmap 运行完成 - 2 秒内扫描了 1 个 IP 地址 (主机在线)

Nmap 版本 2.2-BETA4（本文写作时的最新版本）带有一个名为 mape 的 Gtk GUI 前端。GUI 可以方便地选择要扫描的主机/网络并配置扫描选项。nmap 运行的输出打印在自己的窗口中，并存储在日志中以便稍后比较和研究。

### 步骤 6.3.4 商业产品

Internet Security Systems (http://www.iss.net) 销售基于主机的安全评估工具 System Scanner™、基于主机和网络的入侵检测 (RealSecure™) 以及网络漏洞扫描 (Internet Scanner™)。ISS 产品是成熟的专业软件。System Scanner 和 Internet Scanner 的评估版可免费下载。评估版仅在 localhost 上运行。

Network Associates, Inc. (http://www.nai.com) 销售 CyberScanner，它可以对主机、防火墙、集线器和交换机进行网络漏洞扫描。CyberCop可以通过自定义脚本语言 (CASL) 进行扩展。它具有自动更新功能以保持软件和漏洞数据库的更新。

![](img/0aaa698c422b2f7ffe93bff50cbbef96_93_0.png)

## 附录 A
资源和参考

本指南所有附录的内容可以在网上 http://www.sans.org/linux 获取。

### 步骤 2:

- 安装 HOWTO: http://metalab.unc.edu/pub/Linux/docs/HOWTO/Installation-HOWTO
- TrinityOS http://www.ecstucho.edu/~dranch/LINUX-index.html
- Secure-syslog http://www.core-sdi.com/syslog/
- Syslog-ng http://www.balabit.au/products/syslog-ng
- Nsyslog http://anu.edu/~avalon/nsyslog.html

### 步骤 3:

- CIAC 登录公告 http://ciac.iac.gov/bulletins/04.shtml
- Linux Journal 关于 TCP Wrappers 的文章 http://linuxjournal.com:8080/issues/
- Linux 存档:
    - Metalab http://metalab.unc.edu/pub/Linux/
    - Freshmeat http://www.freshmeat.net/
    - AutoRPM 主页 http://www.kaybee.org/--kirk/html
- Linux Security HOWTO http://metalab.unc.edu/pub/Linux/docs/HOWTO/Security
- Linux 管理员指南 http://www.securityport.com/lasg/
- RedHat Security http://www.redhat.com/core/support/docerr.html (根据你的版本，查看 Web 页面 "security")
- 订阅 Red Hat 列表以获取安全更新:
```
$ Mail -s redhat-announce-list@redhat.com <dev/null
```
- Caldera 系统安全公告 http://www.calderasystems.com/security/index.html
- Caldera-announce 列表 http://www.calderasystems.com/forums/caldera-announce.html
- SUSE 电子邮件警报 http://www.suse.com/MailingLists/index.html
- Debian 安全 http://www.debian.org/security/
- 订阅 Debian 安全列表：
```
$ Mail -s debian-security-request@lists.debian.org <dev/null
```
![](img/0aaa698c422b2f7ffe93bff50cbbef96_94_0.png)

### 步骤 4:

- ftp/ftp.hut.fi/pub/ssh
- SSH http://www.isc.org/view.cgi?products/BIND/index.html
- BIND http://www.linux.com/security/articles/july/sec_bind.html
- named chroot jail
- http://www.sendmail.org/current-release
- Sendmail http://www.qmail.org
- Qmail http://www.porcut.org
- Postfix http://www.eudora.com/free/servers.html
- Eudora Qpopper http://as.webmu.edu/query/imapd
- Cyrus IMAPD http://www.sendmail.org/tips/relaying
- sendmail relaying http://mike.daewoo.com/computer/stunnel/stun
- stun http://www.rickk.com/sslwrap/
- sslwrap http://www.astart.com/LPRng
- LPRng http://www.samba.org
- Samba http://www.apache.org
- Apache Commercial SSL 模块：http://www.covalent.net/ssl/
- Covalent Raven SSL 模块：http://www.store.redhat.com/commerce
- Red Hat Linux 电子商务服务器：http://www.roxen.com
- Rosenen http://www.c2.net/products/sh/index.php
- Stronghold: http://www.zeustech.net
- Zeus:

### 步骤 5:

- http://www.kernel.org/Linux kernels
- http://www.kernelnotes.org
- http://ipmasq.jb.net/IP Masquerade HOWTO http://www.rustcorp.com/linux/ipchains/
- IP CHAINS

![](img/0aaa698c422b2f7ffe93bff50cbbef96_95_0.png)

### 步骤 6:

- Psionic Logcheck http://www.psionic.com/abacus/logcheck
- 其他 syslog 过滤器 http://metalab.unc.edu/pub/Linux/system/log/
- Tripwire 安全页面 http://www.tripsecurity.com
- Tripwire ASR 1.3.1 http://www.tripsecurity.com/products/ASR_1.3.html
- Tripwire 2.0 http://www.tripsecurity.com/products/2_0.html
- TripARA 页面 http://www.arc.com/tara/
- Psionic PortSentry http://www.psionic.com/abacus/portsentry
- Tiger 主页 http://www.net.tamu.edu/network/tools/tiger.html
- Tiger 源码 http://www.net.tamu.edu/ftp/security/
- SAINT 页面 http://www.wwdsi.com/saint/
- ARA 页面 http://www.arc.com/sara/
- Nmap http://www.insecure.org/nmap/

用于安装、管理等的书籍和文章：
- "Building Internet Firewalls," Chapman and Zwicky, O’Reilly & Associates, 1995, ISBN 1-56592-124
- "DNS and BIND," 第3版, Ablitz and Liu, O’Reilly and Associates, 1998
- "sendmail," Costales and Allman, O’Reilly & Associates, 1997
- Samba: ISBN 57831-006

##附录 B
Stock Red 6.0
/etc/inetd.conf

以下是 Red Hat 6.0 安装的默认 /etc/inetd.conf。任何以注释字符 "#" 开头的行对互联网都是有效的。参见步骤 3.1 了解更多信息。

```
# inetd.conf
# 此文件描述了通过 INETD TCP/IP 超服务器提供的服务。
# 版本: (@)/etc/inetd.conf    3.10 05/27
# 作者: 取自 BSD UNIX 4.3/TAHOE.
                     Fred N. van Kempen, <waltje@uw.nl>

# 由 Debian 修改要重新配置运行中的 INETD，只需编辑此文件，然后向 INETD 进程发送 SIGHUP 信号。
# 由 RHS Linux 修改 Olaf Kirch <okir@caldera.com> 用于 Caldera Open Linux
# <server_name> <sock_type> <proto> <flags> <user> <server_path> <args>
# Echo, discard, daytime, 和 charge 主要用于测试。
# 要重新读取此文件的更改，只需执行 'killall -HUP inetd'
# 注意：内置的 UDP 服务现在会静默丢弃端口小于 512 的数据包。
#echo               tcp       nowait      root       internal
#echo               dgram      udp        wait       root
```

```
# 这些是标准服务。
```

```
ftp                stream       nowait      root       /usr/sbin/tcpd in.ftpd -l -a
telnet             stream       nowait      root       /usr/sbin/tcpd in.telnetd
gopher             stream       nowait      root       /usr/sbin/tcpd in.gopherd
```





# 附录 B
库存版 Red Hat 6.0
/etc/inetd.conf

```
# 除非你*真的*知道自己在做什么，否则不要取消注释 smtp。
# smtp 现在由 sendmail 守护进程处理，而不是 smtpd。它不会
# 在此处运行，而是在系统启动时从 /etc/rc.d/rc 启动的。
# smtp stream tcp nowait root /usr/sbin/smtpd
# nntp stream tcp nowait root /usr/sbin/nntpd
```

```
# shell, login, exec 和 talk 是 BSD 协议。
shell stream tcp nowait root /usr/sbin/tcpd in.rshd
login stream tcp nowait root /usr/sbin/tcpd in.rlogind
exec stream tcp nowait root /usr/sbin/tcpd in.rexec
#talk dgram udp wait nobody /usr/sbin/tcpd in.talkd
#ntalk dgram udp wait nobody /usr/sbin/tcpd in.ntalkd
#dtalk stream tcp wait nobody /usr/sbin/tcpd in.dtalkd
```

```
# pop 和 im 邮件服务等
```

```
#pop2 stream tcp nowait root /usr/sbin/tcpd ipop2
#pop stream tcp nowait root /usr/sbin/tcpd ipop3
#imap stream tcp nowait root /usr/sbin/tcpd imapd
```

```
# 互联网 UUCP 服务。
```

```
#uucp stream tcp nowait uucp /usr/sbin/ucc-1
```

```
# Tftp 服务用于启动。大多数情况下
# 仅在作为“启动服务器”的机器上运行此项。除非你
# “需要”它，否则不要取消注释。
```

```
#tftp dgram udp wait root /usr/sbin/tcpd in.tftpd
#bootps dgram udp wait root /usr/sbin/tcpd bootpd
```

```
finger stream tcp nowait nobody /usr/sbin/tcpd in.fingered -u
#cfinger stream tcp nowait root /usr/sbin/tcpd in.cfingerd
```

# Finger、system 和 meta 提供的用户输出信息可能对
# 潜在的“系统破解者”有用。许多城市选择禁用
# 部分或全部这些服务以确保安全。

```
#systat stream tcp nowait nobody /usr/sbin/tcpd /bin/ps -30
#netstat stream tcp nowait nobody /usr/sbin/tcpd /bin/netstat -inet
```

```
# 认证
```

```
#auth stream tcp nowait root /usr/local/sbin/identd -i -30
auth stream tcp nowait nobody /usr/local/sbin/identd -i
swat stream tcp nowait 400 root /usr/sbin/tcpd swat
```

```
# inetd.conf 结束
```

接下来的 SYSV init 启动脚本遵循 Red Hat 6.0 init 脚本的通用规范，具体如在线文档 /usr/doc/initscripts-4.16/sysvinitfiles 中。

```bash
!/bin/bash
# /etc/rc.d/init.d/sshd
# sshd
# 启动 Secure Shell 守护进程
# chkconfig: 345 50 50
# description: Secure Shell 守护进程, sshd, 允许对
# 使用 Secure Shell 协议的客户端进行强身份
# 验证并进行加密通信

# processname: sshd
# pidfile: /var/run/sshd.pid
# config: /etc/rc.d/sshd_config

# 来源函数库。
/etc/rc.d/init.d/functions
SSHD=/usr/local/sbin/sshd
SSHD_CONFIG=/etc/rc.d/sshd_config

case "$1" in
start)
    echo -n "Starting SSH services:"
    if [ -x $SSHD -f $SSHD_CONFIG ];
    then
        daemon $SSHD
    else
        echo
        echo_failure
    fi
    touch /var/lock/subsys/sshd
    ;;
  stop)
    echo -n "Shutting down SSH services: "
    echo
    killproc sshd
    rm -f /var/lock/subsys/sshd
    ;;
  status)
    status sshd
    ;;
  restart)
    $0 stop; $0 start
    ;;
  reload)
    killall -HUP sshd
    ;;
  *)
    echo "Usage: sshd {start|stop|status|reload|restart}"
    exit 1
    ;;
esac
```

# 附录 D
一套强力数据防火墙规则集

```bash
#!/bin/sh

# 作者: David A. Ranch
# 基于 TrinityOS IPCHAINS 防墙 v3.12
# http://www.ecst.csuucho.edu/~dranch/linux/index-linux.html

# 此配置假设以下情况 (DSL / 猫调制调器设置):

1) 外部接口运行在 "eth0" 上
2) 外部 IP 地址是动态分配的
3) 内部 IP 掩装网络接口是 "eth1"
4) 内部网络地址位于 RFC1918 的私有
   192.168.1.x TCP/IP 方案范围内

****

注意：在 2.2.1 之前的所有 2.2.x Linux 内核都存在分段
   错误，这使得所有强力 IPCHAINS 规则集失效。
   用户必须将 Linux 内核升级到 2.2.1+ 
   以确保正确的防火墙安全。

************************************
# 初始化

echo -e "\nLoading IPCHAINS Version 3.12"
echo ""

# 变量

# 回环接口和地址
LOOPBACK="lo0"
LOOPBACKIP="127.0.0.1"

# 外部接口设备。
# 注意：PPP 用户可能希望将此接口
# 与正确的调制调器接口替换为 "ppp0" 或 "eth0"

EXTIF="eth0"
echo 外部接口: $EXTIF
# 附录 D
强力数据防火墙规则集

# 外部接口的地址
附录 D
强力数据防火墙规则集

# 外部接口的地址
EXTIP=$(ifconfig | grep inet | awk '{ print $2 }')
echo 外部 IP: $EXTIP

# 外部接口的地址
# 注意：IP 地址是 DHCP 的
# 默认网关
EXTGW=$(route -n | grep default | awk '{ print $2 }')
echo 默认网关: $EXTGW

# 内部接口设备。
INTIF="eth1"
echo 内部接口: $INTIF

# 内部接口的地址
INTIP="192.168.1.1"
echo 内部 IP: $INTIP

# 内部网络地址
INTLAN="192.168.1.0/24"

# 端口转发地址

# 内部主机的 IP 地址
# 端口转发允许外部
# 用户直接连接 MASQ 机器。例如
# 端口转发是为了
# 后到 MASQ 服务器。

# 注意：端口转发远超
# 本文档此类访问的安全范围。
# 请参阅附录 A 以获取完整解释。

# 默认禁用。
PORTFWIP="192.168.1.20"

# 所有 IP 地址的掩码
UNIVERSE="0.0.0.0/0"

# 广播传输的掩码
BROCAST="255.255.255.255"

# 高权限端口的规范。
UNPRIVPORTS="1024:65535"

# X Window 系统 (TCP) 端口的规范。
XWINDOWS_PORTS="6000:6010"

# 备用 DNS 服务器的 TCP/IP 地址（如果有）。
# 这是可选的！
# 默认禁用。
SECONDARYDNS="172.31.44.22"

# 特别允许的外部主机的 TCP/IP 地址
# 默认禁用。
SECUREHOST="172.20.2.11"
SECUREHOST2="172.20.2.12"

# 允许直接连接 Linux 服务器的内部主机 TCP/IP 地址
# 默认允许所有内部主机。
# 默认禁用。
HOSTTIIP="192.168.1.10"
HOSTZIP="192.168.1.11"

# 日志状态。
# 取消 " " 行并注释 "-l" 行，如果你想
# 禁用某些重要的 IPCHAINS 规则集的日志记录。
# 此日志的输出可以在 /var/log/messages
# 文件中找到。建议保持此设置开启。
# 如果你需要减少某些日志，请编辑你不感兴趣的
# 规则集，从你不感兴趣的规则集中删除 "LOGGING" 语法。
#
# LOGGING=""
LOGGING="-l"
```




## 附录 D

强数据包防火墙规则集

```
#-
# 调试部分
# 如果你在防火墙方面遇到问题，请取消以下行
# 并重新运行防火墙，以确保防火墙
# 没有产生任何错误等。此调试
##的输出将存储在名为 /tmp/rc.firewall.dump 的文件中。

#echo " - Debugging."
#echo Loopback IF: $LOOPBACK >> /tmp/rc.firewall.dump
#echo 回环接口名称: $LOOPBACK >> /tmp/rc.firewall.dump
#echo 内部接口名称: $INTIF >> /tmp/rc.firewall.dump
#echo 内部 IP: $SINTIF >> /tmp/rc.firewall.dump
#echo LAN 地址: $INTLAN >> /tmp/rc.firewall.dump
#echo-
#echo 外部接口名称: $SEXTIF >> /tmp/rc.firewall.dump
#echo 外部接口 IP: $SEXTIF >> /tmp/rc.firewall.dump
#echo 外部广播 IP: $EXTBROAD >> /tmp/rc.firewall.dump
#echo 外部接口默认网关: $SEGTGW >> /tmp/rc.firewall.dump
#echo-
#echo 防墙: /tmp/rc.firewall.dump
#echo 外部备用 DNS: $SECONDARYDNS >> /tmp/rc.firewall.dump
#echo 外部安全主机: $SECUREHOST >> /tmp/rc.firewall.dump

# 通用
# 执行通用处理，如设置组播路由
# 和 DHCP 地址。

# 组播是 TCP/IP 中强大但很少使用的特性，用于多媒体
# 数据。虽然现在使用得不多（大多数 ISP 都没有在其
# 网络中启用组播），但在未来几年内将变得非常常见。请访问
# www.mbone.com 获取详情。

# 添加此功能是可选的。

# 默认禁用。
#echo " - Adding multicast route."
#/sbin/route add -net 224.0.0.0 netmask 240.0.0.0 dev $SEXTIF
```

# 附录 D
强数据包防火墙规则集

```
# 在 Linux 内核中开启 IP 转发
# 开启此功能有两种方法。第一种是
# Red Hat 方式。编辑 /etc/sysconfig/network 文件，并将
# "FORWARD_IPV4" 行改为：

    FORWARD_IPV4=true

# 第二种方法如下所示，可以在系统运行时随时执行。

echo " - Enabling IP forwarding."
echo "1" > /proc/sys/net/ipv4/ip_forward

# 禁用 IP 伪装攻击。

# 这会丢弃针对某个网络的流量，尽管它是在另一个
# 接口上接收的。

echo " - Disabling IP Spoofing."
for file in /proc/sys/net/ipv4/conf/*rp_filter
do
    echo "1" > $file
done

# 如果你不使用动态地址，请注释此处
echo " - Enabling dynamic TCP/IP address hacking.
echo "1" > /proc/sys/net/ipv4/ip_dynaddr

# 伪装超时
# 设置伪装会话的超时值（秒）。
# 项目 #1 - TCP 会话超时为 2 小时
# 项目 #2 - 接收到 TCP/IP "FIN" 包后流量超时 10 秒
# 项目 #3 - UDP 流量超时为 60 秒

echo " - Changing IP masquerading timeouts."
/sbin/ipchains -M S 7200 10 60
```

# 附录 D
强数据包防火墙规则集

```
# 伪装模块

# 大多数支持 TCP/IP 的应用程序在 Linux IP
# 伪装服务器后运行良好。但某些应用程序需要特殊的
# 模块才能让其流量正常进出。
```

```
# 注意：某些应用程序**无法**通过 IP 伪装服务器工作，
# 例如任何基于 H.323 的程序。请阅读 IP-MASQ HOWTO 获取更多详情。
```

```
# 注意 #2：仅取消注释你需要**加载的模块。
# FTP 模块默认加载。
```

```
# echo " Loading masquerading modules."
# /sbin/modprobe ip_masq_cascade
# /sbin/modprobe ip_masq_ftp
# /sbin/modprobe ip_masq_irc
# /sbin/modprobe ip_masq_quake
# /sbin/modprobe ip_masq_audio
# /sbin/modprobe ip_masq_vdolvideo
```

```
# 默认策略
# 将所有默认策略设置为 REJECT 并清空所有旧规则。
```

```
# echo " Flushing all old rules and setting all default policies to REJECT "
# 清空所有旧规则集
# /sbin/ipchains -F input
# /sbin/ipchains -F output
# /sbin/ipchains -F forward
```

```
# 将默认策略改为 REJECT
# 我们只想**显式地**允许进入和离开防火墙的流量。
# 所有其他流量都将被隐式拦截。
# /sbin/ipchains -P input REJECT
# /sbin/ipchains -P output REJECT
# /sbin/ipchains -P forward REJECT
```

```
# *****************************************************
# 输入规则
# *****************************************************
echo ""
echo "Input Rules:"
```

```
# 内部内部局域网的入站流量
# 此部分控制允许在内部局域网内流的 INPUT 流量。
# 这意味着本地网络上的所有输入流量都是有效的。
# 如果你想更改此默认设置并仅允许网络中某些
# 类型的流量，你需要注释掉此行
# 并为你想要通过的每个 TCP/IP 地址配置单独 ACCEPT 规则。
# 提供了一些 ACCEPT 规则示例。
```





## 附录 D
强数据包防火墙规则集

# 远程接口声称为本地机器、IP 欺骗、拒绝并日志
`/sbin/ipchains -A input -j REJECT -i $EXTIF -s $INTLAN -d $UNIVERSE $LOGGING`

# DHCP 客户端。

# 如果你的 ADSL 或电缆调制解调器连接动态 IP 地址，
# 你需要启用这些行。

# 默认启用。
`/sbin/ipchains -A input -j ACCEPT -i $EXTIF -p udp -s $UNIVERSE -d $BROCAST/0`
`/sbin/ipchains -A input -j ACCEPT -i $EXTIF -p tcp -s $UNIVERSE -d $BROCAST/0`

# FTP: 允许外部用户连接到 Linux 服务器本身以提供
# 端口类型的 FTP 服务。这无法适用于 PASV FTP 传输。

# 默认禁用。
`/sbin/ipchains -A input -j ACCEPT -i $EXTIF -p tcp -s $UNIVERSE -d $EXTIF ftp`
`/sbin/ipchains -A input -j ACCEPT -i $EXTIF -p tcp -s $UNIVERSE -d $EXTIF ftp-data`

# HTTP: 允许外部用户连接到 Linux 服务器本身以提供
# HTTP 服务。

# 默认禁用。
`/sbin/ipchains -A input -j ACCEPT -i $EXTIF -p tcp -s $UNIVERSE -d $EXTIF http`

# ICMP: 允许来自所有外部 TCP/IP 地址的 ICMP 数据包。

# 注意：通过防火墙规则启用 ICMP 数据包的作用不仅仅是
# 防止人们 ping 你的机器。
# 关联应用程序依赖于各种 ICMP 消息。如果没有 ICMP，
# 你的 Linux 服务器和内部隐藏（Masqueued）计算机可能无法工作。

`/sbin/ipchains -A input -j ACCEPT -i $EXTIF -p icmp -s $UNIVERSE -d $EXTIF`

# NFS: 拒绝来自和指向外部机器的 NFS 流量。

# 注意：NFS 是管理员面临的最大安全问题之一。
# 除非你完全清楚自己在做什么，否则不要在互联网或任何非可信网络上启用 NFS。

`/sbin/ipchains -A input -j REJECT -i $EXTIF -p tcp -s $UNIVERSE -d $EXTIF 2049`
`/sbin/ipchains -A input -j REJECT -i $EXTIF -p tcp -s $UNIVERSE 2049 -d $EXTIF`

# NNTP: 允许外部计算机连接到 Linux 服务器本身以提供
# NNTP（新闻）服务。

# 默认禁用。
`#/sbin/ipchains -A input -j ACCEPT $EXTIF -p tcp -s $UNIVERSE -d $EXTIP ntp`

# NNTP: 允许外部计算机连接到 Linux 服务器本身以进行
# NTP（时间）更新

# 默认禁用。
`#/sbin/ipchains -A input -j ACCEPT $EXTIF -p tcp -s $UNIVERSE -d $EXTIP ntp`

# TELNET: 允许外部计算机连接到 Linux 服务器本身以进行
# TELNET 访问。

# 默认禁用。
`#/sbin/ipchains -A input -j ACCEPT $EXTIF -p tcp -s $UNIVERSE -d $EXTIP telnet`

# SSH 服务器: 允许外部计算机连接到 Linux 服务器以进行
# SSH 访问。

# 默认禁用。
`#/sbin/ipchains -A input -j ACCEPT $EXTIF -p tcp -s $UNIVERSE -d $EXTIP ssh`

# 所有接口上的入站流量

# 这控制所有接口的输入流量。这通常
# 用于可以被认为是公共的服务。

`echo "" - 正在公共服务设置输入过滤器（所有接口）。"`

# AUTH: 允许认证协议 indent 在所有接口上工作，但# 在 /etc/inetd.conf 中禁用它。通过 iptables 块
# 允许这种流量的原因是，某些旧的 TCP/IP 栈无法正确
# 处理被 REJECT 的“auth”请求。
`#/sbin/ipchains -A input -j ACCEPT -p tcp -s $UNIVERSE -d auth`

# BOOT/DHCP: 拒绝所有散乱的启动流量。

# 默认禁用。
`#/sbin/ipchains -A input -j REJECT -p udp -s $UNIVERSE bootpc`

- DNS: 如果你运行权威 DNS 服务器，你必须在所有接口上打开 DNS 端口以允许查询。如果你运行缓存 DNS 服务器，你至少需要为内部接口打开 DNS 端口。

- 建议按照第 4 节的文档通过限制区域传输和服务器来保护 DNS。默认禁用。
`#/sbin/ipchains -A input -j ACCEPT -p tcp -s $UNIVERSE domain`
`#/sbin/ipchains -A input -j ACCEPT -p udp $UNIVERSE domain`

- RIP: 拒绝所有 RIP 流量。许多配置良好的网络会将路由协议传播到网络边缘。下一行将允许显式过滤它，而不记录到 SYSLOG。默认禁用。
`#/sbin/ipchains -A input -j REJECT -p udp $UNIVERSE route`

- Samba: 拒绝所有 Samba 流量。许多网络会将冗杂的 SMB 协议传播到网络边缘。下一行允许在此处显式过滤它，而不记录到 SYSLOG。默认禁用。
`#/sbin/ipchains -A input -j REJECT -p udp $UNIVERSE netbios-ns`
`#/sbin/ipchains -A input -j REJECT -p udp $UNIVERSE netbios-d`

- SMTP: 如果此服务器是权威邮件服务器，你必须允许所有接口的 SMTP 流量。默认禁用。
`#/sbin/ipchains -A input -j ACCEPT -p tcp $UNIVERSE -d smtp`

- 来自外部主机的显式入站访问：这控制来自特定外部主机（安全主机）的外部访问。此示例中的 FTP、FTP-DATA、SSH、POP3 和 TELNET 流量从安全主机进入防火墙。除了这些入站规则外，我们还必须显式允许来自远程主机的流量出去。详细信息请参见输出部分中的规则。
`echo - 正在为外部主机设置过滤器。`

- 安全主机
`/sbin/ipchains -A input -j ACCEPT -i $EXTIF -p tcp -s $SECUREHOST ftp`
`/sbin/ipchains -A input -j ACCEPT -i $EXTIF -p tcp -s $SECUREHOST ftp-data`
`/sbin/ipchains -A input -j ACCEPT -i $EXTIF -p tcp -s $SECUREHOST ssh`
`/sbin/ipchains -A input -j ACCEPT -i $EXTIF -p tcp -s $SECUREHOST pop3`
`/sbin/ipchains -A input -j ACCEPT -i $EXTIF -p tcp -s $SECUREHOST telnet`
`/sbin/ipchains -A input -j ACCEPT -i $EXTIF -p tcp -s $SECUREHOST2 ftp`
`/sbin/ipchains -A input -j ACCEPT -i $EXTIF -p tcp -s $SECUREHOST2 ftp-data`

# 端口转发

# 端口转发允许外部流量直接连接到内部隐藏（Masqued）机器。端口转发的一个示例需求是外部用户需要直接连接到 MASQ 服务器后的 WWW 服务器。

> 注意：端口转发超出了本文文档的范围，无法解释开启此类访问所涉及的安全问题。请查看附录 A 以阅读 IP-MASQ-HOWTO 的完整解释。

# 不要使用大于 1023 的端口作为重定向端口。

# 默认禁用。
`echo " 正在开启到内部主机的端口转发。"`
`/usr/sbin/ipmasqd portfw -f -`
`#echo " 将端口 26 的 SSH 流量转发到 $PORTFWIP"`
`/usr/sbin/ipmasqd portfw -a -p tcp -l $EXTIP 26 -R $PORTFWIP`

# 高端口：

# 为所有响应的 TCP/UDP 流量启用所有高特权端口

> 注意：使用 "-y" 标志处理没有 SYN 位的 TCP 流量。换句话说，这意味着任何尝试在高端口向你的服务器发起流量的流量都被拒绝。

# 将被接受的高端口流量只能是服务器发起的返回流量或基于 UDP 的流量。

# 注意2：请注意，活动 FTP 会话的端口 20 不应使用 SYN 过滤。由于此，我们必须显式地允许其进入。
`echo " 正在开启高端口上的入站响应 (TCP/UDP) 流量。"`

`/sbin/ipchains -A input -j ACCEPT ! -y -p tcp -s UNIVERSE -d $EXTIP $PRIVPORTS`
`/sbin/ipchains -A input -j ACCEPT -p tcp -s UNIVERSE ftp-data -d $EXTIP $PRIVPORTS`
`/sbin/ipchains -A input -j ACCEPT -p udp -s UNIVERSE -d $EXTIP $PRIVPORTS`

# 入站捕获规则

`echo " - 最后入站捕获规则。`

# 所有其他入站流量被拒绝并记录。
`/sbin/ipchains -A input -j REJECT -s UNIVERSE -d $UNIVERSE $LOGGING`

*****************************************************************\*\***
# 输出规则
*****************************************************************\*\*\***
echo ""
echo "输出规则:"

# 内部局域网出站流量
# 此规则集为内部局域网的出站流量提供了策略。

# 在此示例中，所有流量出站。因此没有要求实现单独的过滤器。然而，与上面的输入部分一样，给出的示例仅供参考。同样注意，上述规则也适用于过滤规则的顺序。

echo " - 正在为内部局域网流量设置输出过滤器。"`

# 本地接口，任何指向本地网络的源都是有效的。
`/sbin/ipchains -A output -j ACCEPT -i $INTIF -s UNIVERSE -d $INTLAN`

# 回环接口是有效的。
`/sbin/ipchains -A output -j ACCEPT -i $LOOPBACKIF -s UNIVERSE -d $UNIVERSE`





## 附录 D
## 强力数据包防火墙规则集

```
# DHCP：如果你在这台 Linux 机器上配置了 DHCP 服务器，
# 你需要启用以下规则集。
```

```bash
# 默认禁用。
#/sbin/ipchains -A output -i $INTIF -p udp -s $INTIF/32 bootps -d $BROADCAST/0 bootpc
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $INTIF/32 bootps -d $BROADCAST/0 bootpc
```

```bash
# HTTP：以下示例了如何允许 HTTP 流量访问内网
# WWW 服务器，同时不允许从外部
# 网络进行访问。
```

```bash
# 默认禁用。
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $INTIF/32 http -d $INTLAN
```

```bash
# 内部局域网主机的显式输出
```

```bash
# 此规则集仅允许内部局域网上的特定主机
# 访问此防火墙服务器本身。许多人可能认为
# 这些是极端的，但许多系统攻击也发生在内部网络中。
```

```bash
# 给出的示例允许通过 FTP、FTP-DATA、SSH 和 TELNET 访问。
```

```bash
# 为了使此规则集生效，你必须先注释掉上面那行
# 提供所有内部主机对内部局域网拥有完全访问权限的行。
```

```bash
# 默认禁用。
```

```bash
#echo " 为特定主机设置输出过滤器。"
```

```bash
# 第一个主机
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST1/32 -d $ftp
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST1/32 -d $ftp-data
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST1/32 -d $ssh
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST1/32 -d $telnet
```

```bash
# 第二个主机
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST2/32 -d $ftp
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST2/32 -d $ftp-data
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST2/32 -d $ssh
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST2/32 -d $telnet
```

## 附录：强力数据包防火墙规则集

```bash
# 外部接口上的出站流量
```

```bash
# 此规则集将控制哪些流量可以从外部出去。
```

```bash
echo " - 为外部接口的流量设置输入过滤器。"
```

```bash
# 拒绝从远程接口到本地网网的出站流量，
# 填充路由；拒绝并记录
/sbin/ipchains -A output -j REJECT -i $EXTIF -s $UNIVERSE -d $INTLAN LOGGING
```

```bash
# 拒绝从外部接口到本地网的出站流量，
# 填充伪装，拒绝并记录
/sbin/ipchains -A output -j REJECT -i $EXTIF -s $INTLAN -d $UNIVERSE LOGGING
```

```bash
# DHCP 客户端：如果你的 Linux 服务器通过 DSL 或电缆调制解调器
# 连接并且获取动态 DHCP 地址，你需要
# 启用以下规则集。
```

```bash
# 默认启用
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $UNIVERSE bootpc -d $UNIVERSE bootps
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p udp -s $UNIVERSE
```

```bash
# FTP：允许 FTP 流量（该 Linux 服务器是 FTP 服务器）
```

```bash
# 默认禁用。
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $EXTIP ftp-data -d $UNIVERSE
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $EXTIP ftp-data -d $UNIVERSE
```

```bash
# HTTP：允许 HTTP 流量（该 Linux 服务器是 WWW 服务器）
```

```bash
# 默认禁用
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $EXTIP http -d $UNIVERSE
```

```bash
# NTP：允许 NTP 更新（该 Linux 服务器是 NTP 服务器）
```

```bash
# 默认禁用
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $EXTIP ntp -d $UNIVERSE
```

```bash
# TELNET：允许 telnet 流量（该 Linux 服务器是 TELNET 服务器）
```

```bash
# 默认禁用
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $EXTIP telnet -d $UNIVERSE
```

```bash
# SSH 服务器：允许出站 SSH 流量（该 Linux 服务器是 SSH 服务器）
```

```bash
# 默认禁用
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $EXTIP ssh -d $UNIVERSE
```

## 附录 D：强力数据包防火墙规则集

```bash
# 所有接口上的出站流量
# 此规则集将控制所有接口的流量。这通常
# 被认为是公共服务的。
# 我们提供了一些拒绝规则集作为示例，
# 但由于上面的 REJECT 语句，这些并不是必须的。
```

```bash
echo " 为所有接口的公共服务设置输出过滤器。"
# AUTH：允许所有接口身份验证（在 /etc/inetd.conf 中禁用）。
/sbin/ipchains -A output -j ACCEPT -p tcp -s $UNIVERSE -d $UNIVERSE
```

```bash
# DNS：如果你的 Linux 服务器是权威服务器，
# 你必须启用此规则集
# 默认禁用
#/sbin/ipchains -A output -j ACCEPT -p tcp -s $EXTIP domain -d $UNIVERSE
#/sbin/ipchains -A output -j ACCEPT -p udp -s $EXTIP domain -d $UNIVERSE
```

```bash
# ICMP：允许输出 ICMP 流量
# 注意：通过防火墙规则集禁用 ICMP 包的作用
# 不仅仅是防止人们 ping 你的机器。许多
# TCP/IP 及其应用程序依赖 ICMP。没有 ICMP，
# Linux 服务器和内部计算机可能无法工作。
#/sbin/ipchains -A output -j ACCEPT -p icmp -s $UNIVERSE -d $UNIVERSE
```

```bash
# NNTP：允许基于 NNTP 的新闻。
# SMTP：如果 Linux 服务器是权威服务器，
# 你必须允许此规则集。
#/sbin/ipchains -A output -j ACCEPT -p tcp -s $EXTIP smtp -d $UNIVERSE
```

## 附录 D：强力数据包防火墙规则集

### 特定输出拒绝
# 这些规则集拒绝你不想离开系统的流量。
# echo " - 拒绝特定的输出。"
# RPC。
/sbin/ipchains -A output -j REJECT -i $EXTIF -p udp -s $EXTIF -d $UNIVERSE LOGGING
/sbin/ipchains -A output -j REJECT -i $EXTIF -p udp -s $EXTIF -d $UNIVERSE LOGGING
# Mount.
/sbin/ipchains -A output -j REJECT -i $EXTIF -p udp -s $EXTIF -d $UNIVERSE 635 LOGGING
/sbin/ipchains -A output -j REJECT -i $EXTIF -p udp -s $EXTIF -d $UNIVERSE 635 LOGGING
# PTTP.
/sbin/ipchains -A output -j REJECT -i $EXTIF -p tcp -s $EXTIF -d $UNIVERSE 1723 LOGGING
/sbin/ipchains -A output -j REJECT -i $EXTIF -p udp -s $EXTIF -d $UNIVERSE 1723 LOGGING
# Remote Winsock.
/sbin/ipchains -A output -j REJECT -i $EXTIF -p tcp -s $EXTIF -d $UNIVERSE 1745 LOGGING
/sbin/ipchains -A output -j REJECT -i $EXTIF -p udp -s $EXTIF -d $UNIVERSE 1745 LOGGING
# NFS.
/sbin/ipchains -A output -j REJECT -i $EXTIF -p tcp -s $EXTIF -d $UNIVERSE 2049 LOGGING
/sbin/ipchains -A output -j REJECT -i $EXTIF -p udp -s $EXTIF -d $UNIVERSE 2049 LOGGING
/sbin/ipchains -A output -j REJECT -i $EXTIF -p udp -s $EXTIF -d $UNIVERSE 2049 LOGGING
/sbin/ipchains -A output -j REJECT -i $EXTIF -p udp -s $EXTIF -d $UNIVERSE 2049 LOGGING
# Anywhere.
/sbin/ipchains -A output -j REJECT -i $EXTIF -p tcp -s $EXTIF -d $UNIVERSE 5631 LOGGING
/sbin/ipchains -A output -j REJECT -i $EXTIF -p udp -s $EXTIF -d $UNIVERSE 5631 LOGGING
/sbin/ipchains -A output -j REJECT -i $EXTIF -p tcp -s $EXTIF -d $UNIVERSE 5632 LOGGING
/sbin/ipchains -A output -j REJECT -i $EXTIF -p udp -s $EXTIF -d $UNIVERSE 5632 LOGGING
# Xwindows.
# 注意：请查看上方变量部分的示例（默认为 6000:6010）
# Xwindows 使用的端口比 6000-6010 远得多。
```bash
/sbin/ipchains -A output -j REJECT -i $EXTIF -p tcp -s $EXTIF -d $UNIVERSE_X_PORTS LOGGING
/sbin/ipchains -A output -j REJECT -i $EXTIF -p udp -s $EXTIF -d $UNIVERSE_X_PORTS
```

## 附录 D：强力数据包防火墙规则集

### 输出到显式主机的输出
# 控制输出到显式主机的流量。
# Net。
/sbin/ipchains -A output -j REJECT -i $SEXTIF -p tcp -s $SEXTIF 12345
/sbin/ipchains -A output -j REJECT -i $SEXTIF -p tcp -s $SEXTIF 12346
```bash
# Net Pro.
/sbin/ipchains -A output -j REJECT -i $SEXTIF -p tcp -s $SEXTIF 20034
```

```bash
# Backor
/sbin/ipchains -A output -j REJECT -i $SEXTIF -p udp -s $SEXTIF 3137
```

```bash
# New Trojan.
/sbin/ipchains -A output -j REJECT -i $SEXTIF -p tcp -s $SEXTIF 5742
```

```bash
# Socket Troy.
/sbin/ipchains -A output -j REJECT -i $SEXTIF -p tcp -s $SEXTIF 30303
```





# 附录 D
强数据包防火墙规则集

```bash
# 允许所有高端口的流量。
# echo " - 启用高端口所有输出拒绝 (TCP/UDP) 流量。"
/sbin/ipchains -A output ACCEPT -j tcp -s $EXTIP $UNPRIVPORTS -d $UNIVERSE
/sbin/ipchains -A output -j ACCEPT -p udp -s $EXTIP $UNPRIVPORTS -d $UNIVERSE
```

```bash
# 全局捕获规则
# echo " - 最终输出捕获规则。"
# 所有其他输出流量均被拒绝并记录。此规则集应该捕获
# 包括 samba 在内的尚未被拦截的内容。
/sbin/ipchains -A output -j REJECT -s $UNIVERSE -d $UNIVERSE $LOGGING
```

```bash
# 转发规则
# echo " - 转发规则: ""
echo "转发规则:"
```

```bash
# 从内部 LAN 启用 TCP/IP 转发和地址伪装
# 从本地接口的本地网络到任何地方进行地址伪装。
# - 从内部 LAN 启用 IP 伪装。
/sbin/ipchains -A forward -j MASQ -i $EXTIF -s $INTLAN -d $UNIVERSE
# 全局捕获规则，所有其他转发将被拒绝。
```

```bash
/sbin/ipchains -A forward -j REJECT -s $UNIVERSE -d $UNIVERSE $LOGGING
# 结束
# echo " -e "防火墙已部署。\n"
```

# 附录 E 修改系统二进制文件默认权限的脚本

大多数 Linux 发行版的默认文件权限向用户暴露了过多信息，或者允许普通用户执行他们不该执行的操作。这些设置可能过于偏执，但防患于未然胜。

注意：这些权限对于普通安装是有效的，但根据创建和未安装的包，某些文件可能不存在。每当重新安装 Linux 或安装更新的包时运行此脚本。

```bash
#!/bin/sh

# 作者: David A. Ranch
# 基于 TrinityOS 文件权限修正

MODE="o-rwx"

# /bin 下目录文件
cd /bin
chmod $MODE linuxconf mt setserial umount

```

```bash
# /sbin 下目录文件
cd /sbin
chmod $MODE badblocks ctrlldet chkconfig debugfs depmod dump
chmod $MODE fdisk fck* halt hwclock if* insist insmod isnapping
chmod $MODE kerneldell killall* lilo getty mk* mod* netreport
chmod $MODE pam pcinitrd pndump portmart quota restore runlevel
chmod $MODE stinit swapon tun2fs ugetty
```

```bash
# /usr/bin 下目录文件
cd /usr/bin
chmod $MODE control-panel comanche eject gnome* gpasswd kernelcfg

chmod 755 lpr*
chmod 4755 lpr

# 注意：我觉得将 "lpr" 设置为允许任何组执行它
# 是一件坏事。

# 我想将 UNIX 用户和 Samba 进程添加到
# /etc/groups 中已定义的 "lpr" 组中，然后能够
# 将权限改回 4750。但是……这真的不可行。
# Linux 尚不支持多组文件，且 Linux
# 尚不支持访问控制列表 (ACL)。所以……你要么
# 要么保留这些文件的 SUID，要么运行 LPRng。

chmod $MODE minicom netcfcg
```

```bash
# /usr/sbin 下目录文件
cd /usr/sbin
chmod $MODE at* crond dhc edquota exportfs ftpshut group* grp*
chmod $MODE imapd in.* inetd ipop* klogd logotrate lp*
chmod 755 lsof
chmod $MODE makemap mouseconfig named* nmbd newusers ntp* n-tsysv
chmod $MODE pppd pw* quota* rdev repquota rotatelogs rpc* samba
chmod $MODE setup showmount smb* squid syslogd taper tcpd* time*
chmod $MODE tmpwatch tunelp user* vi* xntp*
```

# 来自 SANS 学院的附加资源

## 电子简报

## 合作研究报告与项目

**入侵检测影子：分步指南**
这是一本关于执行高级入侵检测的指南。它使用由海军水面作战中心开发的开源 Cisco Shadow 软件，通过高速入侵检测和分析保护超过 15,000 台主机。

**SANS 网络安全简报**
每月发布一次，通过电子邮件发送。SANS 网络安全简报报告了最重要的新安全威胁，并就从哪里找到最新补丁或威胁信息提供了指导。每条目都可以在线阅读或通过邮件阅读。SANS 简报由 Michele Guile 撰写，并在 Mark Maurer, Gary Green, Steve Black, Bill Chechek, Gene Schulz, Marcus Rubin, Rob Kolb, Hal Homer, Penny Denny 等其他领先编辑的协助。向 digest@sans.org 发送主题为 "subscribe" 的邮件订阅。

**SANS 薪资报告**
每年发布。报告涵盖了网络管理员和安全专业人员在其主要运行环境（UNIX、NT 或组合）中的薪资、所在地组织类型和规模、是员工还是顾问以及其他特征。它还报告了团队规模、各级别的加薪情况以及平均加薪的主要报告依据。1999 年的调查有 15,000 多人参与。

SANS 学院是一个合作研究与教育机构，系统管理员、安全专业人员和网络管理员在此分享他们学到的经验。

**Windows NT：分步指南**
这是一本来自来自十七个国家的安全专业人员的共识报告，他们制定了安全 NT 应该执行的九十问题和八个阶段。36 页。

它提供教育会议、深度课程、合作研究报告以及权威问题的简报。

**计算机事件处理：分步指南**
来自领先处理机构和专家以及五十名经验事件处理人员的共识报告。44 页。

**NT 简报**
针对 NT 分步指南的更新，关于应该或不应该实施的最新补丁和安全包的最新指导。它总结了许多 NT 及其服务的新威胁和漏洞。向 digest@sans.org 发送主题为 "subscribe nt digest" 的邮件订阅此简报。

**Windows NT 工具：管理员共识**
是一份共识报告，两百 NT 管理员分享了他们在实施和使用提高 Windows 系统效率和安全的流行工具方面的经验。

# 安全路线图海报

**Solaris 安全：分步指南**
这是一份关于如何让 Solaris 系统准备就绪的极价值专家知识集合。

**SANS 安全路线图墙海报**
每年更新两次，这些海报展示了针对常见问题的“十大”列表：最佳的安全书籍、最佳的安全网站、最大的威胁、供应商联系方式、顶尖工具等。它们会自动发送给所有网络安全简报的订阅者和参加学院会议的人员。

**Linux 安全：分步指南**
红帽和其他 Linux 变体拥有极佳的技术。但要在业务世界中使用它们，它们也需要出色的安全防护。本手册提供了路线图。

订购：
http://www.sansstore.org/

