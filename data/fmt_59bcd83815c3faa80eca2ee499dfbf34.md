
## 第一部分：Fedora 和 RHEL 入门

有许多桌面环境甚至更多的桌面管理器可供选择。（Fedora 和 RHEL 侧关注 GNOME 和 KDE 桌面环境，但也提供了其他几种桌面环境和窗口管理器。）

- 应用支持 —— 由于兼容 POSIX 以及多种不同的应用程序编程接口（API），Linux 系统拥有大量的免费和开源软件。与 GNU C 语言库（glibc）的兼容性是其广泛应用支持的主要原因。通常情况下，要让一个开源应用程序适用于特定版本的 Linux，只需只需将源代码重新编译为该 Linux 版本即可。

## Linux 的主要优势

与其它商业操作系统相比，Linux 最大的资产是它的价格、可靠性以及它带给你的自由。凭借最新的 2.6 Linux 内核，你还可以获得作为其最大资产之一的扩展性。

大多数人知道它的初始价格是免费的（或者在盒装版或附带书籍时至少为 50 美元）。然而，当人们谈论 Linux 的经济性时，他们通常指的是它的总成本，其中包括（无或低廉）许可费用、重用你选择的任何代码的能力，以及使用廉价硬件和兼容的免费附加应用程序的能力。尽管商业操作系统倾向于鼓励升级到强大的硬件，但 Linux 并不需要（尽管更快的硬件和更大的磁盘会很不错）。

在可靠性方面，共识是 Linux 与许多商业 UNIX 系统不相上下，但比大多数大多数面向桌面的操作系统更可靠。如果你依赖计算机保持持续运行（例如作为 Web 服务器或文件服务器），这一点尤为真实。（你不需要在每次更改某些设置时都重启，除非你替换了内核本身。）

这种可靠性还延伸到了安全领域。虽然 Linux 软件曾出现过漏洞，但 Linux 用户在很大程度上免受困扰 Windows 的恶意软件和病毒文化的侵害。大规模的 Linux 部署不需要安装杀毒软件，这种情况在企业环境的 Windows 中是不被允许的。此外，当人们在 Linux 上安装杀毒软件时，通常是为了为 Windows 用户扫描文件和电子邮件，以帮助那些苦恼的 Windows 用户。

由于你可以获得源代码，你可以自由地以任何选择的方式更改 Linux 系统的任何部分以及随附的任何开源软件。与许多自成一体的商业产品不同，开源软件倾向于以旨在相互作用的组件进行构建，你可以根据自己的喜好混合并组合组件。正如我之前提到的，Linux 是一种鼓励互操作性的文化。例如，如果你不喜欢某个窗口管理器，你可以插件一个新的，因为有许多管理器都是为了在同一个框架内运行而构建的。

## 第一章：Fedora 和 Red Hat Linux 概述

使用 Linux 的另一个优势是互联网上随时可以获得帮助。Linux 新闻组或邮件列表中可能有人愿意帮助你解决问题。由于源代码是可用的，如果你需要修复某些内容，甚至可以自己编写代码补丁！另一方面，我见过操作系统供应商对报告的问题置之数月而不予修复。记住，Linux 的文化是在人助人的氛围中蓬勃发展的。

### Red Hat Enterprise Linux 是 Red Hat Fedora 吗？

让源代码在互联网上自由流动并不是黑客分享软件的一种坏坏方法。然而，为了让 Linux 被技术类计算机用户群体所接受，它需要易于安装和使用。同样，那些考虑将其任务关键型应用程序提交给计算机系统的企业也希望知道该系统经过仔细测试并有良好的支持。

为了这些目标，许多公司和组织开始收集并将 Linux 软件打包成可用的形式，即“发行版”。Linux 发行版的主要目标是让组成 Linux 的数百（或数千）个互不相关的软件包协同工作，成为一个凝聚的整体。流行的 Linux 发行版包括 Debian、Ubuntu、openSUSE、SUSE Linux Enterprise、Slackware、Damn Small Linux、Gentoo 和 Mandriva。多年来，最受欢迎的商业发行版是 Red Hat Linux。

2003 年 9 月，Red Hat, Inc. 改变了其业务模式。这一改变导致了 Red Hat 赞助的 Fedora 项目的形成，将 Red Hat 技术的发展推向未来。但对于必须依赖 Red Hat Linux 的个人和企业来说，这意味着什么呢？

### Red Hat 成立 Fedora 项目

随着最新的 Fedora 和 Red Hat Enterprise Linux 发行版，Red Hat 对开源社区以及 Red Hat 商业客户的承诺开始固化。Red Hat Enterprise 产品提供看起来像是一个用于在大机构中部署 Linux 的稳固、可靠的系统。随着 Fedora 项目合并了 Fedora Core 和 Fedora extras，Fedora 用户可以使用大量的高质量软件包。

几年前，情况看起来并不乐观。

Red Hat, Inc. 发布 Fedora 项目首先引发了人们对公司方向及其旗舰产品 Red Hat Linux 的更多质疑。事实上，似乎 Red Hat 已经不再存在了。相反，曾经的 Red Hat Linux 将通过两条路径的 Linux 发行版体现：

- Fedora 项目（www.fedoraproject.org）—— 一个开源项目，从 Red Hat Linux 9 开始，产生自己的 Linux 发行版。虽然该项目由 Red Hat, Inc. 赞助，但该项目产生的 Linux 发行版（简称 Fedora）没有官方支持。
- Red Hat Enterprise Linux（www.redhat.com/rhel）—— 由 Red Hat, Inc. 提供的官方商业产品系列，按年度订阅提供。Red Hat 通过技术支持、培训和文档为其企业级产品提供支持。

Fedora 项目的主要成果是一系列二进制和源代码包（以 DVD 形式分发），称为 Fedora 的 Linux 发行版。在名称更改之前，该发行版被测试为 Red Hat 系列的下一代（即 Red Hat Linux 10）。书中提供的 DVD 和 CD 包含的软件包作为官方版本发布：Fedora 9。

然而，从 Red Hat Linux 改名为 Fedora Core（简称 Fedora）并不是 Fedora 和 Red Hat Enterprise Linux 之间的唯一区别。Red Hat, Inc. 还以下方式改变了与 Fedora 的关联：

- 无盒装 —— Red Hat 决定不通过零售渠道销售 Fedora。缩短的发布周期使得几个月管理一次零售渠道的盒装变得困难，Red Hat 认为 Linux 技术的早期采用者足够聪明自己获取软件。
- 短保证更新周期 —— 每个 Fedora 版本的关键修复和安全补丁有效期比 RHEL 产品短得多。因此，用户必须更频繁地升级或重启系统。
- 无技术支持 —— Red Hat 没有为 Fedora 提供技术支持计划。
- 无 Red Hat 文档 —— 之前的 Red Hat Linux 产品手册未引入 Fedora。相反，正在以文章格式为项目收集一系列面向特定的文档。然而，Fedora 文档项目（http://fedaproject.org/wiki/DocsProject）正在遵循一条根据开源许可开发和发布 Red Hat 文档的路径。

通过在周围建立广泛的支持行业，项目可以以更短的时间（通常为六个月的发布周期）发布软件。这使得 Fedora 用户始终从最新的操作系统版本中获得最新的软件功能和修复。但 Fedora 项目不仅仅是 Fedora 发布版。它实际上是一系列项目（http://fedaproject.org/wiki/Projects）的集合，还包括以下内容：

### 第1章：Fedora 与 Red Hat Enterprise Linux 概述

- 每个孩子一台电脑（OLPC） — Fedora 项目正与红帽公司（Red Hat, Inc.）以及 OLPC 项目（www.laptop.org）合作，为全球儿童提供笔记本电脑。Fedora 软件被作为 OLPC 软件部分的基础。
- Fedora 大使与营销 — 专注于向世界推广 Fedora。大使被分配到美国不同地区和世界各个国家，代表其所在地区展示 Fedora。营销项目通过鼓励举办演讲、开发者会议和其他倡议来提高 Fedora 的知名度。
- Fedora Live CD 工具 — Fedora Live CD 中心是一套名为 `live-creator` 的工具。通过 `live-creator`，Fedora 项目制作其官方的 Fedora live CD。Live CD 提供了一种在不安装到硬盘的情况下，在电脑上运行 Linux 系统的方法。它提供了一种在不干扰硬盘上任何内容的情况下尝试 Fedora 的绝佳方式。由于 `live-creator` 是一个开源项目，你可以使用这些工具创建自己的 live CD。在本次 Fedora 版本中，live CD 技术取得了许多进展，包括 liveUSB 版本以及与 kickstart 文件的集成。
- Fedora 艺术 — 创建 Fedora 使用的图形（背景、标志、屏幕等），主要使用由 Fedora 分发的工具制作。
