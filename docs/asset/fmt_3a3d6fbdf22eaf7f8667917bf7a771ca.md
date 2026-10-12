
## 5. 描述 NetStorage 的作用和功能

## 6. 安装和配置 NetStorage

### 简介

大多数用户在多台计算机上工作，以创建、管理和使用他们的个人文件。然而，在所有这些不同的计算机（可能运行不同的平台）上访问、存储、管理和同步这些文件可能是一项艰巨的任务。

Novell Nterprise Linux Services 从 Linux 服务器提供以下文件服务：

- `Novell iFolder`。此产品提供工作站与中心 iFolder 服务器之间文件的访问、存储和同步。
- `NetStorage`。此产品通过浏览器提供对网络中 Linux 服务器上的文件和文件夹的安全基于 Internet 的访问。
- `Samba`。此产品使用 Microsoft® SMB/CIFS 网络协议提供 Windows® 兼容的文件共享。

在本章中，您将学习 iFolder、NetStorage 和 Samba 如何帮助您提供网络文件访问和管理解决方案。

### 目标 1

### 描述 iFolder 的用途和架构

Novell iFolder 是一个 Net 服务软件解决方案，它允许移动专业人士在任何地方——在线、离线、全天候——跨多台工作站和 Net 访问他们的本地文件。

iFolder 自动且智能地更新您在台式机、笔记本电脑和其他连接设备上使用的文件，让您可以在任何地方使用它们——在办公室、在家或在酒店。

您只需一个活动的网络或 Internet 连接以及 iFolder 客户端、Web 浏览器或 NetDrive 即可。

对于用户而言，iFolder 就像一个可从任何计算机访问的单一虚拟工作文件夹。它提供了一种简单、方便且安全的方式来访问、备份和同步文件。

当连接到 iFolder 服务器时，iFolder 会自动将本地文件上的工作备份到 iFolder 服务器上的账户。如果本地数据丢失，文件始终受到保护并且可以轻松恢复。

如果用户转移到不同的位置和使用不同的计算机，iFolder 会自动同步这些文件以反映在其他地方完成的工作——无需手动磁盘复制或文件传输。

要描述 iFolder 的用途和架构，您需要了解以下内容：

- iFolder 优势
- iFolder 特性
- iFolder 组件
- iFolder 架构

### iFolder 优势

分析师一致认为，高达 80% 的公司关键业务数据存放在 PC（台式机和笔记本电脑）上，而不是网络存储中。

然而，高达 96% 的所有商务 PC 都没有进行备份（战略研究公司）。

根据 IDC 数据：

- 美国、西欧和拉丁美洲的移动劳动力预计将从 2001 年的 3470 万增长到 2004 年的 6080 万。
- 销售给商业组织的 PC 中有 35% 是笔记本电脑。

#### iFolder 的优势

由于本地数据备份的缺乏以及移动办公力量的不断壮大，企业需要一种能够轻松访问存储在网络上个人文件的产品，以及一个可以自动从任何位置同步这些文件的系统。

iFolder 满足了企业和用户的这些需求（以及其他需求）。它提供了以下优势：

- **无缝的数据访问。** iFolder 以这样的方式存储和同步用户的工作数据：无论用户从哪个客户端或哪个位置登录，他们的文件都是可用的，并且处于他们期望的状态。
- **数据保护与数据恢复。** 当用户在本地保存文件时，iFolder 客户端可以自动将数据更新到 iFolder 服务器，在那里数据立即可用于组织的常规网络备份操作。

iFolder 还赋予互联网服务提供商（ISP）的能力，使其能够为客户提供用户值得信赖的备份解决方案，用于保护关键的商业或个人数据。

- **可靠的数据安全。** 借助 iFolder 加密，存储的数据能够免受未经授权的网络访问。

iFolder 在数据跨越互联网之前对其进行加密，并将其存储在 Novell iFolder 服务器上，从而防止未授权用户获取。

- **高效的移动用户。** iFolder 消除了版本不一致的问题，使用户能够轻松地从任何连接的台式机、笔记本电脑或 Web 浏览器访问其文档的最新版本。

在准备出差或在家办公时，用户不再需要从各种台式机和网络位置将所需数据复制到他们的笔记本电脑中。

iFolder 客户端可以自动将用户最当前的文件版本更新到他们的笔记本电脑和台式机上。即使用户丢失了笔记本电脑，所有那些文件仍可通过任何连接到互联网的计算机进行访问。

- **跨平台支持。** iFolder 服务器可与运行在 NetWare® 和 Linux 上的 Apache Web 服务器，或运行在 Windows 2000 上的 Microsoft Internet Information Servers (IIS) Web 服务器集成。

此外，iFolder 对用户身份验证的 LDAP 支持允许您利用运行在 NetWare、Linux 和 Windows 2000 服务器上的 Novell eDirectory™，或运行在 Windows 2000 服务器上的 Microsoft Active Directory™。

- **简单数据和账户管理。** iFolder 旨在允许网络管理员轻松设置和管理。

iFolder 服务器可以通过标准 Web 浏览器在任何位置进行管理。凭借其自动文件更新、同步和加密功能，iFolder 还使 IT 部门从常规维护任务中解放出来。

网络管理员还有选择使用 eDirectory 或 Microsoft Active Directory（仅在 Windows 2000 服务器上）来管理 Novell iFolder 账户。

- **大规模部署。** iFolder 的关键功能之一是其能够扩展到一个庞大且不断增长的环境。您可以在多台服务器上安装 iFolder，使您的 iFolder 环境能够随着业务的成长而扩展。

在您拥有的 iFolder 网络中，iFolder 服务器的数量没有实际限制——单个 iFolder 服务器可处理多达 10,000 个用户账户。反过来，这些服务器中的每一个共同作用作为一个系统。

由于 iFolder 负责将用户身份验证请求重定向到正确的 iFolder 服务器，登录过程对于用户来说是无缝的体验。

此外，随着您的 iFolder 网络的增长，您的管理成本保持不变，因为所有 iFolder 服务器的管理都通过 iFolder 管理控制台进行集中处理。

- **用户优势。** Novell iFolder 为用户提供以下优势：

    - 通过将本地文件自动备份到 iFolder 服务器和您的多台工作站，防范本地数据丢失。
    - 自动更新您经常使用的机器（工作场所、笔记本电脑、家庭）之间的文件，使所有机器上的数据视图保持一致。
    - 允许您将在本地目录（例如“我的文档”）中的文件，您可以像往常一样使用它们。
    - 允许您使用 Web 浏览器在任何地方访问您的文件。
    - 跟踪并记录您离线工作时所做的更改，并在您上线时同步这些更改。
    - 启用加密后，保护数据在传输过程中以及在 iFolder 服务器上存储期间的安全。

### iFolder 的功能

除了 iFolder 提供的优势外，以下是使 iFolder 成为高效个人文件访问和同步服务的关键功能：

- **支持以下网络操作系统：**

    - 带有支持包 5 或更高版本的 NetWare 5.1
    - 带有支持包 2 或更高版本的 NetWare 6.0
    - NetWare 6.5 或更高版本
    - 带有服务包 3 或更高版本的 Microsoft Windows 2000 Server
    - Red Hat® Linux AS 2.1 Enterprise
    - SuSE® SLES 8

- **对以下系统的 LDAP 支持：**

    - 适用于 NetWare、Windows 2000 和 Red Hat 或 SLES 8 Linux 服务器的 Novell eDirectory
    - 适用于 Windows 2000 服务器的 Microsoft Active Directory

- **大规模部署支持** 使用多台 iFolder 服务器作为单一系统运行
- **报告生成器** 供管理员查看 iFolder 用户和 iFolder 系统的统计数据
- **通过 NNLS 中的 Red Carpet™ 守护进程进行自动升级**
- **支持以下工作站操作系统的客户端：**

    - Windows 98/ME
    - Windows NT® 4/2000 Professional
    - Windows XP Home 和 Professional

- **使用 Novell NetDrive 将驱动器映射到 iFolder 服务器，以并发访问多个 iFolder 账户**
- **通过 Novell NetDrive 支持瘦客户端**，适用于 Citrix® MetaFrame® 服务器、Windows 2000 Terminal Server 和 ZENworks® OnDemand Services
