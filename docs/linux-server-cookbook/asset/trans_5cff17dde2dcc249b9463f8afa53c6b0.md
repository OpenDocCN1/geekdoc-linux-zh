

## Linux 的光明前景

如前所述，Linux 目前是各个 IT 领域的关键因素，并且随着企业对开源的依赖以及 Linux 所提供功能的支持，它将继续成为大多数新兴技术解决方案的操作系统。在不久的将来，容器将继续被用于部署新服务；像 ARM 这样的新架构将更广泛地进入市场，并且随着企业持续从本地基础设施向云端迁移，公有云和云的使用将继续增长。目前普遍可用的发行版具有以下特点：

-   **架构**：Linux 内核适用于大多数架构；一些示例包括：*ARM/ARM64、IA-64、MIPS、PowerPC、RISC-V* 和 *x86*。
-   **云镜像就绪**：大多数 Linux 发行版提供可在公共云（*AWS、Azure 和 Google Cloud*）和私有云（*OpenStack*）中直接启动的云就绪镜像。
-   **容器镜像**：Linux 发行版提供用于运行容器的官方镜像，例如使用 *Docker* 或 *Kubernetes*。

## 结论

在过去几十年以及当下，Linux 一直是 IT 领域最重要的操作系统。未来将在新兴技术领域带来新的创新，Linux 将成为其中大多数实现的不可或缺的，甚至可能是主要的组成部分。普通桌面用户越来越习惯于将 Linux 发行版作为主要操作系统使用，而开发人员也决定从其他操作系统迁移到 Linux。

## 关键事实

-   Linux 是世界上最流行的操作系统。
-   Linux 适用于大多数可用的架构。
-   Linux 在所有主流云平台上可用。
-   大多数新兴技术都在使用 Linux。
-   容器基于 Linux。

## 问题

1. 所有世界 500 强最快超级计算机列表中的超级计算机都运行 Linux。
    - a. 正确
    - b. 错误
2. Android 是 Linux 的一个修改版本。
    - a. 正确
    - b. 错误
3. SaaS 代表什么？
    - a. Service as a Service（服务即服务）
    - b. System as a Service（系统即服务）
    - c. Software as a Service（软件即服务）
4. PaaS 代表什么？
    - a. Programming as a Service（编程即服务）
    - b. Platfomr as a Service（平台即服务，注：原文拼写为 Platfomr）
    - c. Program as a Service（程序即服务）
5. IaaS 代表什么？
    - a. Innovation as a Service（创新即服务）
    - b. Integration as a Service（集成即服务）
    - c. Infrastructure as a Service（基础设施即服务）

## 答案

1. a
2. a
3. c
4. b
5. c

## 第 2 章

# 安装 Linux

## 引言

安装 Linux 发行版是一项简单的任务，所需时间不多。目前积极维护的发行版数量超过 300 个，每个发行版都具有相同的主要组件（Linux 内核以及通用系统和系统库），但用途和特定的系统工具有所不同。不同发行版之间的差异通常与包管理器、桌面环境和系统服务（如防火墙和网络服务）有关。

流行的 Linux 发行版可以安装在不同的架构和设备上。其他发行版则经过优化，专门用于特定环境，例如 Raspberry Pi Linux OS（用于 Raspberry Pi 设备）或 OpenWrt（用于路由器）。

流行网站 distrowatch.com 包含活跃发行版的列表，其中提供了有关当前版本、支持的架构、默认包含的软件以及其他许多有用信息。

本章将重点介绍流行发行版的安装，特别是因为它们对企业有支持。它涵盖了可用的安装方法、安装步骤、高级选项以及这些发行版之间的差异。

## 结构

在本章中，我们将讨论以下主题：

-   Linux 支持级别
-   安装方法
-   常见安装步骤
-   高级安装步骤
-   Debian GNU/Linux
-   Ubuntu Server
-   Red Hat Enterprise Linux
-   CentOS 和 CentOS Stream
-   Rocky Linux 和 Alma Linux
-   SUSE Linux Enterprise Server 和 openSUSE
-   其他具有商业支持的发行版

## Linux 支持类型

了解服务器的用途是决定使用哪个 Linux 发行版的最重要因素。需要运行高可用服务、关键任务应用程序，或需要运行在特定发行版中经过认证的应用程序的客户，将需要一个商业发行版，由具备高级工程技能的专业人员提供支持。提供专业支持的主要公司及其关联发行版如下：

-   **Red Hat** 提供 Red Hat Enterprise Linux，具有三个支持级别：
    -   自助支持：访问 Red Hat 产品以及客户门户中的知识库和工具。
    -   标准支持：在工作时间内访问工程师支持。
    -   高级支持：针对高严重性问题，提供 24 × 7 全天候的工程师支持访问。
-   **Canonical** 为 *Ubuntu Server* 提供商业支持，有两个选项：
    -   Ubuntu Advantage for Applications：为开源数据库、日志、监控和聚合服务（LMA）、服务器和云原生应用程序提供安全和支持。
    -   Ubuntu Advantage for Infrastructure：为开源基础设施提供安全和 IaaS 支持。
-   **SUSE** 为 SUSE Linux Enterprise Server 提供两种商业支持：
    -   **标准版：** 包括软件升级和更新，通过聊天、电话和网络提供 12 × 5 的无限支持。
    -   **优先版：** 与标准版支持相同，但提供 24 × 7 全天候支持。
-   **Oracle** 为 **Oracle Linux** 提供两种商业支持：
    -   **基本支持：** 包括 24 × 7 全天候的电话和在线支持，包括对使用 *Oracle Clusterware*、*Oracle Linux 负载均衡器* 和 *Oracle 的 Docker 容器运行时* 的高可用性提供支持。
    -   **高级支持：** 在基本支持的基础上，增加了 *Oracle Linux 虚拟化管理器*、*Oracle Linux 的 Gluster 存储* 和 *Oracle Linux 软件集合* 等应用程序的支持。

其他流行的服务器发行版拥有安全团队来处理严重漏洞，而 bug 和问题则由志愿者提供支持。

-   **Debian：** 安全团队在下一个稳定发行版发布后，大约一年时间内仍为稳定发行版提供支持。
-   **Alma Linux：** CloudLinux 致力于支持 AlmaLinux 10 年，包括稳定且经过彻底测试的更新和安全补丁。
-   **Rocky Linux：** 提供坚实的基础稳定性，定期更新以及 10 年的支持生命周期，且全部免费。

选择要安装的发行版和版本时，与支持相关的另一个重要关键点是 **长期支持（LTS）** 服务。这对于运行关键应用程序的公司至关重要，因为在这种情况下，升级发行版并不总是可行或推荐的，并且在长时间内获得支持的要求是必不可少的。

## Red Hat Enterprise Linux 的长期支持

随着 Red Hat Enterprise Linux 版本 8 的引入，Red Hat 将 RHEL 产品阶段从四个简化为三个阶段：完全支持（五年）、维护支持（五年）和扩展生命周期阶段（两年）。下图显示了 Red Hat 支持的生命周期：

![](img/863afa537de4eed7deb11978bfbfa90e_45_0.png)

*图 2.1：* *Red Hat Enterprise Linux 的生命周期支持。来源：Red Hat*

## Ubuntu Server 的长期支持

对于每个 Ubuntu LTS 版本，**Canonical** 维护基础软件包，并在 10 年的时间内提供安全更新。生命周期包括前五年的维护期和五年的 **扩展安全维护（ESM）**。下图显示了 Ubuntu 支持的生命周期：

![](img/863afa537de4eed7deb11978bfbfa90e_45_1.png)

*图 2.2：* *Ubuntu Server 的生命周期支持。来源：Ubuntu*

## SUSE Linux Enterprise Server 的长期支持

长期服务包支持是对现有 SUSE Linux Enterprise Server 订阅的补充。LTS 包支持提供以下选项：

-   当您推迟或延迟迁移到最新的服务包时，额外提供 12 到 36 个月的缺陷解决和支持。

