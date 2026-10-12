
# Oracle Database 10g Linux 管理

## 关于作者

**Edward Whalen** 是 Performance Tuning Corporation (www.performtuning.com) 的创始人，该公司是一家专门从事数据库性能、管理和备份/恢复解决方案的咨询公司。在创立 Performance Tuning Corp. 之前，Mr. Whalen 在 Compaq Computer Corporation 工作，先担任操作系统开发人员，后担任数据库性能工程师。他在数据库系统设计和为最佳性能调优方面拥有丰富的经验。他的职业生涯包括为许多不同公司进行的硬件、操作系统和数据库开发项目。Mr. Whalen 已撰写了另外三本关于 Oracle RDBMS 的书籍和四本关于 MS SQL Server 的书籍。他还与 Oracle 和 MS SQL Server 共同完成了许多基准测试和性能调优项目。Mr. Whalen 被公认为数据库性能调优和优化领域的领导者。除了在 Solaris、AIX、HP-UX 和 Windows 等许多不同操作系统平台上使用 Oracle 的经验外，他最近花费了大量时间在 Linux 上使用 Oracle，包括在 Linux 上部署一些最早的 RAC 集群。他与 Red Hat 和 Novell/SUSE 密切合作，使用多种 Linux 发行版。

## 关于撰稿作者

**Robert Bryan Thomas** 是 Performance Tuning Corporation 的高级性能顾问。他在数据库性能、Oracle RAC、数据仓库和 SAN 存储方面拥有多样化的背景。他目前专门从事多个操作系统平台上的 Oracle10g RAC。Robert Thomas 从 Texas A&M University 获得计算机科学学位。

**Fraser Talbot** 是 Performance Tuning Corporation 的高级性能顾问。他的背景包括数年的数据库管理经验，专门从事 Oracle 和 Oracle E-Business Suite。他和他的妻子 Virginia 以及三个女儿 Margaret、Susan 和 Elizabeth 住在休斯顿，德克萨斯州。

**Dan Hotka** 是一名培训专家，在计算机行业拥有超过 27 年的经验，在 Oracle 产品方面拥有超过 22 年的经验。他是一位国际公认的 Oracle 专家，其 Oracle 经验可追溯到 Oracle V4.0 时代。他也是 Que 出版的 *Oracle9i Development by Example* 和 *Oracle8i from Scratch* 的作者，并合著了另外六本畅销书。他经常在 Oracle 贸易期刊上发表文章，并在世界各地的 Oracle 会议和用户组中定期演讲。访问他的网站 www.DanHotka.com。您也可以通过 dhotka@earthlink.net 联系 Dan。

## 致谢

![](img/9479df2d00f5e62b87366b125224950f_16_0.png)

承认所有使本书成为可能的人并不容易。不仅有本书本身所付出的工作，还有朋友和家人的支持与鼓励，他们帮助推动了本书的进展。

我要感谢以下人员：撰稿作者 Robert Bryan Thomas、Fraser Talbot 和 Dan Hotka；McGraw-Hill/Osborne 的 Lisa McClain 和 Carolyn Welch；以及技术编辑 James Petts 和 Michael New。如果没有 Oracle Press 的优秀编辑团队的帮助，本书不会成为现在的样子。

我还要感谢 Larry Ellison。如果没有他，Oracle 今天不会成为现在的样子。感谢 Jim Enright，在我需要帮助时帮助我。我还要感谢 Wjm Coekaerts，他推出了一款优秀的产品，以及 Ken Jacobs，我很荣幸认识他，并从他那里获得了对 Oracle RDBMS 的新的认识。

写书需要大量的时间和精力。我要感谢我的妻子 Felicia，她忍受了写这本书所必需的牺牲。

## 引言

![](img/9479df2d00f5e62b87366b125224950f_18_0.png)

Linux 的流行以惊人的速度增长。但就在几年前，Linux 甚至还不存在。要了解 Linux 的运作原理，有必要回顾 Linux 的历史。Linux 是根据 UNIX 操作系统打造的，因此要完全了解 Linux 的历史，你也必须了解 UNIX 的历史。

### UNIX 历史

20 世纪 60 年代末，UNIX 操作系统的开发在 AT&T Bell Labs 开始，目的是为 PDP-7 计算机创建一个新的操作系统。这项开发由 Ken Thompson 和 Dennis Ritchie 完成，并在 1971 年 culminated 为 UNIX 操作系统的首次发布。此后，又相继发布了几个版本，但下一个主要版本是 1973 年的第 4 版。第 4 版的意义在于它是使用“C”编程语言编写的 UNIX 操作系统的第一个版本。有趣的是，“C”编程语言与 UNIX 操作系统并行开发；然而，直到“C”语言足够稳定，UNIX 操作系统才用“C”重写。

1975 年，UNIX 的第 6 版发布。这是首次在 Bell Labs 外发布的版本。这开启了 UNIX 向其他公司和不同开发社区的初步流行和传播。随后，发布了几种不同风格或品牌的类 UNIX 操作系统。这些操作系统具有共同的命令集和编程 API，但由于商标和所有权问题，这些不同类型的 UNIX 许多以不同的名称发布，并具有略有不同的变化和市场定位。

例如，1980 年，微软发布了一个名为 Xenix 的类 UNIX 操作系统。Xenix 设计用于使用 Intel 处理器的 PC 计算机。1982 年和 1983 年，AT&T UNIX 系统组 (USG) 发布了 System III，然后是 System V（第一个受支持的 UNIX 版本）。两者都旨在用于小型计算机。1984 年，加州大学发布了自己的 UNIX 操作系统 UNIX 4.2BSD。这种 UNIX 操作系统的变种在数字设备公司（Digital Equipment Corporation）和 Sun Microsystems 等计算机系统制造商中变得流行。

在不同变种的 UNIX 之间竞争数年后，UNIX System V 第 4 版发布。此版本吸收了 USG UNIX、BSD UNIX 和 Xenix 的特性，并将其整合为一个 UNIX 规范。不久之后，AT&T 将 UNIX 系统组剥离为一个独立的组织，称为 UNIX 系统实验室或 USL。就在此时，Linux 的第一个版本发布了。

1993 年 Novell 收购了 UNIX 系统实验室，并将 UNIX 商标和规范的权利转让给了 X/Open 组织。至今，世界各地仍在开发和使用许多种类的 UNIX 和类 UNIX 操作系统。对于其中许多操作系统而言，UNIX 操作系统与类 UNIX 操作系统之间的唯一区别在于是否使用 UNIX 商标。

## Linux 的诞生

1991 年，在芬兰赫尔辛基大学，Linus Torvalds 开始着手开发一个新操作系统，其外观和工作方式与 UNIX 操作系统相似，但没有与其相关的专利和商标负担。Torvalds 先生希望开发一个可以进入公共领域的操作系统，在该领域源代码可以无需许可费分发，并且不会侵犯他人的商标。因此，Linux 操作系统诞生了。

Linux 操作系统在一定程度上基于 GNU 项目的原则，即所有软件和源代码都应置于公共领域。GNU 项目于 1984 年开始着手开发公共领域的“C”编译器。到 1991 年 Torvalds 开始着手其操作系统时，GNU C 编译器（GCC）已经可用并且可免费用于他的项目。

GNU 项目源于自由软件基金会。自由软件基金会（FSF）是一个于 1985 年成立的非营利组织。其目标是支持自由软件运动，特别是 GNU 项目。GNU 通用公共许可证（GPL）旨在促进和保护自由软件。FSF 持有 GNU 软件的大部分版权并执行这些版权。GNU 项目至今仍然非常流行。

这很快随后是 Linux 向世界发布的。但 Linux 的早期版本主要用作开发和桌面系统。Linux 的早期版本不适合服务器系统，因为缺乏对更大系统的支持。为了使 Linux 能够在服务器上得到支持，需要支持多处理器、大量的内存以及各种硬件组件和应用程序，例如 Oracle。对更强大和更大系统支持的支持始于后来的 Linux 内核。

1994 年发布了 Linux 内核 1.0 版本。虽然这为桌面用户和开发人员提供了可用的东西，但它并未提供服务器所需的支持。1996 年终于发布了 2.0 内核。2.0 内核支持多处理器系统并包含更强大的 I/O 子系统。1999 年 2.2 内核增强了这一支持，而 2001 年 2.4 内核提供了稳定、高性能的操作系统。此操作系统支持增强了 2.2 内核中的支持。凭借 2.6 内核（请注意只有偶数版本会发布），I/O 子系统得到了极大增强并提供了更大的内存量。
