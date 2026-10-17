
随着当前版本的 Linux 服务器，大多数硬件厂商提供驱动程序和支持。可以构建具有大量内存（64GB）和使用 SCSI 或 SAN 存储的数 TB（太字节）磁盘存储的 Linux 系统。除了这种健壮性和广泛的硬件支持外，还有来自 Oracle 等厂商的广泛支持。今天，Oracle 在 Linux 操作系统上支持其所有主流产品，许多与 Oracle 互补的产品也支持 Linux。

## Linux 和 Unix 时间线

以下是前几节所述历史的总结：

- **1969** Ken Thompson 和 Dennis Ritchie 在 AT&T Bell Labs 使用 PDP-7 开始开发 UNIX 操作系统。
- **1971** 发布了第 1 版。
- **1973** 第 4 版用“C”重写并发布，同时发布了“C”语言本身。
- **1975** 第 6 版在 Bell Labs 外发布。
- **1980** Microsoft 发布了 Xenix。
- **1982** AT&T 的 Unix 系统组（USG）发布了 System III。
- **1983** 发布了 UNIX System V，即第一个受支持的 UNIX。
- **1984** 自由软件基金会开始着手 GNU “C” 编译器的工作。
- **1984** 加州大学伯克利分校发布了 4.2BSD。
- **1989** 发布了 UNIX System V 第 4 版，统一了 System V、BSD 和 Xenix。
- **1991** USL（Unix 系统实验室）被剥离。
- **1991** Linus Torvalds 在芬兰赫尔辛基大学开始着手 Linux 工作并发布了第一个版本。
- **1993** Novell 收购了 USL。
- **1993** Novell 将 UNIX 商标和规范的权利转让给了 X/Open。
- **1994** 发布了 Linux 内核 1.0；Red Hat Linux 首次亮相。
- **1996** Linux 内核 2.0 首次亮相，支持多处理器。
- **1996** Los Alamos 国家实验室使用 68 台运行 Linux 的 PC 创建了一个并行处理超级计算机。
- **1999** 发布了 Linux 2.2 版本内核。
- **2001** 发布了 Linux 2.4 版本内核。
- **2004** 发布了 Linux 2.6 版本内核。

正如你所见，Linux 在短时间内取得了长足的进步。

## Linux 变种

一旦 Linux 的流行变得明显，许多公司开始商业分发 Linux。即使硬核 Linux 拥护者可能更愿意下载源代码并手工构建 Linux 操作系统，但这并不是向大众分发软件的实用方式。此外，公司开始探索在公司内部部署 Linux、运行关键任务应用程序的想法。除了需要更稳定和经过测试的 Linux 发行版外，这些公司还需要易于部署和支持的东西。

Linux 最早的发行版之一是 MCC Interim Linux，于 1992 年由曼彻斯特大学提供。几乎在同一时间，德克萨斯农工大学提供了一个名为 TAMU 的 Linux 发行版。然而，这两种发行版都不是真正商业质量的。为了应对自己对软件更新的挫败感，Patrick Volkerding 创建了 Slackware 发行版。该发行版于 1993 年 7 月发布，是至今仍在使用最古老的 Linux 发行版。Slackware Linux 也以其纯粹的 Linux 发行版而闻名，因为它不会添加其他 Linux 发行版中不可用的应用程序和 GUI 工具。

今天，市面上有数百种 Linux 发行版。然而，为了以 Oracle 支持所知名的质量来正确支持 Linux 操作系统，Oracle 选择了少数几个 Linux 发行版供您选择。Oracle 的选择基于发行版的质量、其流行度以及操作系统厂商的支持可用性和质量。在今天可用的 Linux 发行版中，Oracle 支持 Red Hat 和 United Linux。

Red Hat Linux 成立于 1993 年，是最大的 Linux 公司之一。Red Hat Linux 的流行在很大程度上源于其与各种硬件厂商的合作伙伴关系。Dell、HP 和 IBM 都支持 Red Hat Linux。Red Hat Linux Enterprise 3.0 和 Red Hat Linux Advanced Server 是 Oracle Database 10g 的优秀平台。

SUSE Linux 主要在欧洲和亚洲变得非常流行，但其流行度迅速在全球传播。2003 年 Novell 收购了 SUSE Linux，使其重新成为 UNIX/POSIX 操作系统领域的领先者。SUSE Linux Enterprise Server 9（SLES 9）是首个大规模商业发行版的 2.6 内核。Dell、HP 和 IBM 也支持 SUSE Linux。与 Red Hat Linux 一样，SUSE Linux Enterprise Server（SLES）是 Oracle Database 10g 的优秀平台。

在购买用于运行 Oracle 的 Linux 发行版时需要记住的重要一点是，找到一个能提供您所需支持的发行版。这些发行版公司中的许多都与您的硬件供应商有合作安排，因此如果出现问题，您只需打一个电话即可解决，无论是硬件还是软件出现故障。重要的是，您要找到能够为您的公司和需求提供所需类型支持的供应商。

## History of Oracle

与 Linux 操作系统相比，Oracle 拥有非常悠久而丰富的历史。在本节中，您将了解 Oracle 的历史，而在下一节中，您将了解 Oracle 在 Linux 上的历史。

- **1977** Larry Ellison、Bob Miner 和 Ed Oates 成立了一家名为 Relational Software Inc.（RSI）的公司。在这里，他们决定构建一个名为“Oracle”的 RDBMS，尽可能使用“C”编程语言和 SQL 接口。不久之后，版本 1（仅原型）发布。
- **1979** RSI 向客户交付了第一个产品。“Oracle” RDBMS 版本 2 运行在运行 RSX-11 操作系统的 Digital PDP-11 上，很快被移植到 DEC VAX 系统。
- **1983** 版本 3 推出，宣传了 SQL 语言的更改以及性能增强和其他改进。与早期版本不同，版本 3 几乎完全使用“C”编程语言编写。此时 RSI 将其名称更改为我们今天所知的 Oracle Corporation。
- **1984** Oracle 版本 4 发布。Oracle RDBMS 版本 4 同时支持 VAX 系统和 IBM VM 操作系统。版本 4 是第一个引入读一致性的版本。
- **1985** Oracle 推出 Oracle RDBMS 的版本 5。版本 5 是一个里程碑，因为它通过使用 SQL*Net 将客户端/服务器计算引入市场。版本 5 也是第一个突破 640K 限制的 MS-DOS 产品。
- **1988** Oracle 推出版本 6。版本 6 引入了低级锁定以及各种性能改进和功能增强，包括序列生成和延迟写入。此外，还引入了 PL/SQL 和热备份。我第一次接触 Oracle6 是在我们以前运行 TP1、TPC-A 和 TPC-B 基准测试的年代。此时，Oracle 运行在大量不同的平台和操作系统上。
- **1991** Oracle 在 DEC VAX 平台上于 Oracle RDBMS 版本 6.1 中引入了 Oracle Parallel Server 选项。不久，Parallel Server 选项可在多种平台上使用。
- **1992** Oracle 推出 Oracle7。Oracle7 在内存、CPU 和 I/O 利用率方面包含了许多架构变更。Oracle7 是大家熟悉并使用了多年的功能齐全的 RDBMS。Oracle7 在易用性方面引入了许多进步，例如 SQL*DBA 工具和数据库角色。
- **1997** Oracle 推出 Oracle8。Oracle8 增加了对象扩展以及大量新功能和 administration 工具。
- **2001** Oracle 推出 Oracle9i 版本 1。这是 Oracle9i 产品的首次发布，包含诸如 Oracle RAC（Real Application Clusters）产品等功能。
- **2002** Oracle 推出 Oracle9i 版本 2。此版本在 Oracle9i 版本 1 的基础上构建，并包含诸如 Oracle9i RAC 的集群文件系统等新功能。
- **2004** Oracle 发布用于网格计算的 Oracle10g。此版本将 Oracle 的功能、稳定性和性能提升到新的水平。

## History of Oracle on Linux
