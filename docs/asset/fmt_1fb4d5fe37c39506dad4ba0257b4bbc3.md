
# 引言

## 谁应该使用本书

在过去的几年里，Oracle 数据库环境已成为世界上最流行的数据库平台之一。尽管 Oracle 数据库仍然主要面向需要海量数据能力的大型企业或政府机构，但 Oracle 已经提供了许多新产品，将 Oracle 环境引入了较小的组织。随着在流行的 Microsoft Windows NT 平台上可以使用强大的 Oracle 数据库的可用，将 Oracle 集成到所有类型的业务和组织中的工作正在进行。这意味着需要更多接受过 Oracle 技术培训的知识丰富且经验丰富的 IT 专业人员——而不仅仅是在财富500 强公司。

本书是为 Oracle 数据库专业人士编写的。它从中高级 Oracle 数据库管理员（DBA）开始，但对其他数据库专业人士如开发人员、设计人员、工程师或架构师也很有用。在这些页面中，你将找到实现某技术所需的信息，而不是关于它“应该”如何运行的教条。最后也会发现这本书非常有用的，特别是对于那些具有某些 Oracle 或关系型数据库管理系统（RDBMS）经验的人。想要将数据存储在构建良好、维护良好且调过的 Oracle 数据库中的 Web 管理和开发者也应该考虑本书。UNIX 和 NT 系统管理员（SA）如果必须管理运行 Oracle 产品的系统，将发现这本书非常有用。最后，必须管理使用 Oracle 的 DBA 及其他数据库相关专业的技术经理将发现本书的大部分内容在做出 Oracle 产品相关的关键决策方面是无价的。

本书主要关注 Oracle 的实现和使用，涵盖管理、开发、维护和调优。然而，本书还提供了关系型数据库理论和设计的坚实背景，这是每个数据库专业人士都应该理解的。本书的作者是来自行业、政府、学术界和 Oracle 公司的经验 Oracle 专业人士。除了每章的内容外，本书提供了非常有用且精炼的信息，包括提示、注释、侧栏和警告。书中包含的信息是多年在 Oracle 环境中实战经验的结果。虽然本书是关于 Oracle 的总体介绍，但它聚焦于 Oracle 最新的 RDBMS 产品线。特别是，对于那些想要快速学习 Oracle8 和 Oracle8i 的人来说，这本书是不可或缺的。本书提供了坚实的 Oracle7 背景、对 Oracle8 特性的全面覆盖，以及对 Oracle8i 特性的广泛概述。

## 应该使用哪个版本：Oracle7、Oracle8、Oracle8i

简要讨论 Oracle RDBMS 的演变将帮助您更好地规划在书中穿行的路线。提供这一概述是因为围绕 Oracle8i 发布版本的困惑并不罕见。首先，您需要一些说明。当本书提到 Oracle7 时，指的是 Oracle7x，更具体地说，是 Oracle7.3.x。当它提到 Oracle8 时，指的是 Oracle8.0.x。当它提到 Oracle8i 时，指的是 Oracle8.1.x。当它仅提到 Oracle8.x 时，同时指 Oracle8 和 Oracle8i，换句话说，同时指 Oracle8.0.x 和 Oracle8.1.x。如果这让您感到困惑，想象一下销售人员的感受。

当 Oracle8 最初发布时，它比 Oracle7 提供了许多新功能和选项。然而，基础的 RDBMS Oracle 引擎并没有完全重写。尽管如此，这是从 Oracle7 到 Oracle8 的重大迁移。由于 Oracle8 现在处于发布过程中，其基础 RDBMS 引擎与 Oracle8 相比很大保持不变，甚至比 Oracle7 到 Oracle8 的变化更小。Oracle8i 可以被认为是 Oracle8 的功能超集。

尽管它们代表两个不同的产品，如 Oracle7 和 Oracle8，但 Oracle8 和 Oracle8i 有并行的开发路径，使得它们的发布大致在同一时间。例如，在 Oracle8.0.5 发布后不久，Oracle8.1.5 也发布了。后续版本是 8.0.6 和 8.1.6。显然，Oracle8.x 技术构成了 Oracle8.1.x 的基础，比 Oracle7.3.x 对 Oracle8.x 的基础还要深。

考虑以下问题：Oracle8 能做什么 Oracle8i 做不到的？因为 Oracle8 是 Oracle8i 的功能子集。Oracle8i 能做什么 Oracle8 做不到的？它提供了许多与互联网相关的能力，等等。最重要的是，它整合了 Java 作为原生数据库语言，可以作为 SQL 的补充或替代，并整合了 Web 服务器和开发平台（WebDB）。根据 Oracle 的说法，Oracle8.0.x 的开发（而非支持）可能会随着 8.0.6 的发布而终止，Oracle8.1.x 将完全取代 Oracle8.0.x。换句话说，Oracle8i 将将完全取代 Oracle8。

随着 Oracle8i 的出现，Oracle8i 满足了什么目的（此处原文重复，已按要求处理），what purposes are served by Oracle8i, what purposes are served by Oracle8i, what purposes are served by Oracle8i, what purposes are served by Oracle8i, what purposes are served by Oracle8i, what purposes are served by Oracle8i, what purposes are served by Oracle8i, what purposes are served by Oracle8i, what purposes are served by Oracle8i...

## 本书中包含哪些内容

本书分为 9 部分、41 章和 2 个附录。每个部分在概念上都相互构建。特别是，第二部分涉及 Oracle7.x RDBMS，而第三部分延续第二部分，解释了 Oracle 的主要功能和选项。接下来的章节为您提供了每个章节的概述。

### 第二部分：Oracle7 RDBMS

第 5 章，“Oracle 数据库架构”是对 Oracle 数据库内部存储机制的解释。在这里，涵盖了关于数据库数据文件、表、索引和其他存储对象的信息，以及关于这些对象如何工作和相互作用的详细信息。

第 6 章，“Oracle 实例架构”完成了对 Oracle 数据库服务器的覆盖，解释了 Oracle 数据库涉及的内存结构和进程。第 5 章和第 6 章对 Oracle RDBMS 的内部运作提供了全面的解释。

第 7 章，“探索 Oracle 环境”远离了前两章的抽象主题，并解释了 Oracle 如何在数据库服务器上实现和安装。优化灵活架构（OCI）作为 Oracle 设置托管生产数据库的服务器的标准也在涵盖范围内。

第 8 章，“Oracle 数据库管理概述”涵盖了许多 Oracle 贸易书中没有的内容：数据库生命周期概述、数据库管理员（DBA）及其他数据库相关职位的定义和职责，以及 DBA 为了正确构建 Oracle 数据库需要遵循的功能性任务概述。

### 第三部分：Oracle 8.X RDBMS

第 9 章“从 Oracle 7.x 迁移到 Oracle 8.x”涵盖了三种主要的迁移方法、迁移工具、迁移前任务、一些常见问题以及迁移后任务。

第 10 章“分区”涵盖了 Oracle 逻辑分区表的新功能、分区索引维护，并提供了一些额外功能，例如集成并行化。

第 11 章“大对象 (LOBs) 历史”回顾了从 Oracle 7 到 Oracle 8 的 LOB 历史、Oracle 8 中 LOB 与 BFILES 的区别、DBMS_LOB 软件包，以及许多作为创建和使用示例的代码列表。

第 12 章“面向对象特性”提供了面向对象技术的复，介绍了 Oracle 8 对象，并讨论了这一新选项的许多特性，如 REFs、方法（Methods）、集合（Collections）和对象视图（Object Views）。包含了许多示例代码列表。

## 如何使用本书

在本章中

- 谁应该使用本书 2
- 应该使用哪个版本：Oracle7、Oracle8 还是 Oracle8i 2
- 本书中包含哪些内容 3
- 如何使用本书 8
