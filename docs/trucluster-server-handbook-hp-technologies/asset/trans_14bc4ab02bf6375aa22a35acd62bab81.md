

## 1.5 本书涵盖的内容

本书将涵盖大量内容，但也有一些主题不会涉及。例如，虽然我们了解部署 Stretch Clusters 和容灾容错（DT）集群的各种技术，但目前 Compaq 既不推荐也不普遍支持这些技术。我们也不会在本書中涵盖 Compaq 的 AlphaServer SC 超级计算机实现，因为该主题本身就足以构成一整本书。

当我们决定撰写本书时，我们的目标是提供一份全面的技术指南，可用于设计、实现、部署和管理 TruCluster Server 环境。我们还希望消除 UNIX 集群的神秘感和“魔力”，并解释 IT 管理员为何可能希望使用这项技术来帮助他们降低整体系统管理成本，同时提高 UNIX 服务器基础设施的可管理性和可用性。为此，我们将本书组织为十个章节和一个附录，便于查阅。

- Section 1 - 这是引言部分，提供了关于 UNIX 集群的背景信息，以及 Tru64 UNIX 和 TruCluster Server 的良好概述。对于不熟悉 UNIX 集群和/或 Compaq 的 Tru64 UNIX 的读者，我们强烈建议从本节开始，因为它为后续内容奠定了基础。
- Section 2 - 本节介绍 Tru64 UNIX 集群的设计与配置，是一个非常重要的部分，因为它讨论了 TruCluster Server 环境的设计、规划和配置。我们建议在考虑部署 Tru64 UNIX 用于 TruCluster Server 环境的具体操作之前，先设计并仔细规划您的环境。正如大多数工作一样，前期投入一点设计和规划，将在长期内为您节省大量工作。
- Section 3 - 本节提供有关如何构建和配置 Tru64 UNIX 的信息，以便安装和配置 TruCluster Server。
- Section 4 - Cluster Hooks 涵盖了 Tru64 UNIX 操作系统中实现集群的关键特性。本节提供了理解在 UNIX 上实现集群所需的操作系统基础的背景知识。
- Sections 5 & 6 - TruCluster Server 环境的实际规划、安装和部署。本节对系统架构师和系统管理员尤其有用。

## Tru64 UNIX & TruCluster Server 概述

在深入设计和配置 Tru64 UNIX 集群的世界之前，对 Tru64 UNIX 操作系统进行简要概述将有助于做好准备。将本章视为开胃菜，后续章节则是主菜。为了帮助您消化本书的主要内容，我们将通过讨论 Tru64 UNIX 的几个概念和特性以及现在已成为操作系统一部分的 TruCluster Server 软件来为您做准备。

### 2.1 Tru64 UNIX 概述

该操作系统的名称意义深远。首先，它是一个基于 UNIX 的操作系统。它位于 UNIX 家族树的中间，因为它既汲取了 BSD¹ 和 System V² 家族两方面的特性，也融入了 Compaq 工程师创建的大量核心代码。

图 2-1 描绘了几种常见的 UNIX 变体。请注意图底部位置的 Tru64 UNIX。

其次，Tru64 Unix 确实是一个 64 位操作系统。系统中使用的虚拟地址确实是 64 位的，提供了巨大的虚拟地址空间，并支持大文件偏移量和大小。那就这样了吗？这些就是该系统的区别特征吗？实际上，操作系统还有许多其他特性，我们将在本章的第一部分介绍。如果您熟悉其他 UNIX 系统，您可能想快速浏览本章的第一部分，但请计划放慢速度，仔细阅读 TruCluster Server 概述（第 2.7 节）。

¹ Berkeley Standard Distribution（BSD），由加州大学伯克利分校开发。
² UNIX System V，由 AT&T 的 UNIX 系统开发实验室开发。

