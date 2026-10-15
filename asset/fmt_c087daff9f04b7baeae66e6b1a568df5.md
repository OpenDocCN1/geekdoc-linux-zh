
| 1999 | TruCluster Available Server Software version 1.6<br>TruCluster Memory Channel Software version 1.6<br>TruCluster Production Server Software version 1.6<br>TruCluster Server version 5.0 | Tru64 UNIX version 4.0F and 4.0G<br>Tru64 UNIX version 5.0 | Digital UNIX 更名为 Tru64 UNIX。<br>TruCluster Server 5.0 版是一个非常有限的预先发布版本。 |

| 2000 | TruCluster Server version 5.0A<br>TruCluster Server version 5.1 | Tru64 UNIX version 5.0A<br>Tru64 UNIX version 5.1 | |

| 2001 | TruCluster Server version 5.1A | Tru64 UNIX version 5.1A | |

| 2002 | TruCluster Server version 5.1B | Tru64 UNIX version 5.1B | Hewlett-Packard Company 收购 Compaq Computer Corporation。 |

### 表1-1：集群年表

同年晚些时候，Compaq 悄然发布了 TruCluster Server 5.0 版，这是一个面向特定客户群的有限发布。TruCluster Server 5.0 是第一个具备 SSI 系统集群特性的 TruCluster Server 版本。从 UNIX 的角度来看，这一版本的 TruCluster Server 不再是演进式的，而是革命性的！能够从一台服务器向公共集群文件系统写入文件，然后几乎瞬间就能从另一台服务器读取该文件，这真是一场革命。

2000 年标志着 TruCluster Server 5.0A 以及后来的 5.1 版向客户发布。这是 TruCluster Server 软件首次正式发布具有 SSI 系统集群特性的版本。自 TruCluster Server 5.0A 发布起，任何新版本的 TruCluster Server 软件都将随任何新版本的 Tru64 UNIX 一起发布。

Tru64 UNIX 5.1A 和 TruCluster Server 5.1A 于 2001 年秋季发布。

这大致将我们带到了现在（2002 年夏季）。在撰写本文时，我们预计 Tru64 UNIX 5.1B 和 TruCluster Server 5.1B 将于 2002 年秋季发布。

## 1.4 什么是 TruCluster Server？

既然我们已经知道了什么是集群，那么什么是 TruCluster Server？TruCluster Server 是 Tru64 UNIX 软件、存储设备、集群互连以及两个或更多 AlphaServer 系统的融合体，它们作为一个单一的虚拟系统协同运行。每个集群成员都可以在单一系统管理域下共享资源、存储和集群范围内的文件系统。

TruCluster Server 5.0A、5.1 和 5.1A 版本提供以下特性：

- 集群范围命名空间。
- 集群范围磁盘和磁带存储访问。
- 集群范围逻辑存储管理器（LSM）。
- 连接管理器⁶。
- 集群应用程序可用性（CAA）。
- 集群别名。
- 使用集群别名的高可用性 NFS 服务器。
- 集群通信互连。
- 分布式锁管理器（DLM）⁵。
- 单一系统管理。
- 单一安全域。
- 滚动升级/补丁。
- 扩展进程 ID（PID）。

再次强调，通过 TruCluster Server，你可以从独立的 Tru64 UNIX 服务器创建真正的单一系统映像系统集群。我们将在第 2 章中对 Tru64 UNIX 和 TruCluster Server 进行更深入的概述。

⁵ 分布式锁管理器将在第 18 章中详细讨论。

⁶ 连接管理器将在第 17 章中详细讨论。

## 1.5 本书涵盖的内容

本书将涵盖大量内容，但也有一些主题不会涉及。例如，虽然我们了解部署 Stretch Clusters 和容灾容错（DT）集群的各种技术，但目前 Compaq 既不推荐也不普遍支持这些技术。我们也不会在本書中涵盖 Compaq 的 AlphaServer SC 超级计算机实现，因为该主题本身就足以构成一整本书。

当我们决定撰写本书时，我们的目标是提供一份全面的技术指南，可用于设计、实现、部署和管理 TruCluster Server 环境。我们还希望消除 UNIX 集群的神秘感和“魔力”，并解释 IT 管理员为何可能希望使用这项技术来帮助他们降低整体系统管理成本，同时提高 UNIX 服务器基础设施的可管理性和可用性。为此，我们将本书组织为十个章节和一个附录，便于查阅。

- Section 1 - 这是引言部分，提供了关于 UNIX 集群的背景信息，以及 Tru64 UNIX 和 TruCluster Server 的良好概述。对于不熟悉 UNIX 集群和/或 Compaq 的 Tru64 UNIX 的读者，我们强烈建议从本节开始，因为它为后续内容奠定了基础。
- Section 2 - 本节介绍 Tru64 UNIX 集群的设计与配置，是一个非常重要的部分，因为它讨论了 TruCluster Server 环境的设计、规划和配置。我们建议在考虑部署 Tru64 UNIX 用于 TruCluster Server 环境的具体操作之前，先设计并仔细规划您的环境。正如大多数工作一样，前期投入一点设计和规划，将在长期内为您节省大量工作。
- Section 3 - 本节提供有关如何构建和配置 Tru64 UNIX 的信息，以便安装和配置 TruCluster Server。
- Section 4 - Cluster Hooks 涵盖了 Tru64 UNIX 操作系统中实现集群的关键特性。本节提供了理解在 UNIX 上实现集群所需的操作系统基础的背景知识。
- Sections 5 & 6 - TruCluster Server 环境的实际规划、安装和部署。本节对系统架构师和系统管理员尤其有用。

# Tru64 UNIX & TruCluster Server 概述

在深入设计和配置 Tru64 UNIX 集群的世界之前，对 Tru64 UNIX 操作系统进行简要概述将有助于做好准备。将本章视为开胃菜，后续章节则是主菜。为了帮助您消化本书的主要内容，我们将通过讨论 Tru64 UNIX 的几个概念和特性以及现在已成为操作系统一部分的 TruCluster Server 软件来为您做准备。

## 2.1 Tru64 UNIX 概述

该操作系统的名称意义深远。首先，它是一个基于 UNIX 的操作系统。它位于 UNIX 家族树的中间，因为它既汲取了 BSD¹ 和 System V² 家族两方面的特性，也融入了 Compaq 工程师创建的大量核心代码。

图 2-1 描绘了几种常见的 UNIX 变体。请注意图底部位置的 Tru64 UNIX。

其次，Tru64 Unix 确实是一个 64 位操作系统。系统中使用的虚拟地址确实是 64 位的，提供了巨大的虚拟地址空间，并支持大文件偏移量和大小。那就这样了吗？这些就是该系统的区别特征吗？实际上，操作系统还有许多其他特性，我们将在本章的第一部分介绍。如果您熟悉其他 UNIX 系统，您可能想快速浏览本章的第一部分，但请计划放慢速度，仔细阅读 TruCluster Server 概述（第 2.7 节）。

¹ Berkeley Standard Distribution（BSD），由加州大学伯克利分校开发。

² UNIX System V，由 AT&T 的 UNIX 系统开发实验室开发。

### 2.1.1 操作系统特性

Tru64 UNIX 的功能已迅速扩展到足以提供单系统映像 Single System Image (SSI) 集群选项的能力（正如前一章所讨论的那样）。Tru64 UNIX 多年来一直是许多站点计算机组合中的重要组成部分——甚至在完整集群 SSI 可用之前就已如此。

在集群出现之前，哪些特性吸引了客户使用 Tru64 UNIX？正如你将看到的，有很多。我们将在接下来的几个部分中指出一些特性，并将这些特性与 TruCluster Server（本书的重点）联系起来。

### 2.1.2 Mach 内核

潜藏在 Tru64 UNIX 最核心之处的是 Mach 内核的元素。Mach 是在卡内基-梅隆大学创建的系统。它包含了任务和线程的概念，这些概念在 Tru64 UNIX 的运行中占据重要地位。“任务”代表一个正在运行的程序，而‘线程’则是该程序内的可调度实体。历史上，程序都是以单线程编写。大多数先进的 UNIX 变体都提供了创建多线程程序的能力，以便更好地利用多 CPU 系统。
