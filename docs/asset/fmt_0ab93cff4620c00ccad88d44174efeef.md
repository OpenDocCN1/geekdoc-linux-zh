
SGI 在 2006 年 10 月 17 日申请破产保护。其当时的产品 `SGID.pc` 被放弃，新股以 `SGIC` 为代码在纳斯达克交易所上市。这些新股分发给了公司的债权人，而 `SGID` 的普通股东仅剩下无价值的股份。年底，该公司将总部迁往加州山景市（`Mountain View`）。

对于 `VMware Inc.` 而言，并不意味着 Linux。

`ESX` 用户空间生态系统（类似于“服务控制台”（`Service Console`，或称为 '`COS`'，或 '`vmnix`'）是基于 `Red Hat Linux` 的变体版本（`ESX 2.x` 使用 `Red Hat 7.2`，`ESX 3.x` 使用 `Red Hat Enterprise Linux 3`）。通常，此服务控制台提供管理交互（`CLI`、网页 `MUI`、远程控制台）。

作为一个区分 `ESX` 与其他 `VMware` 虚拟化产品的特殊特性：`ESX` 辅助了 `VMware` 专有的文件系统配置 `VMFS`。`VMFS` 允许多个持有者并发访问相同的 `SAN LUN`，同时通过文件级安全简单防御来确保文件系统的稳定性。

## 红帽企业级 Linux

“`Red Hat Enterprise Linux`”(`RHEL`) 是一种由 `Red Hat` 开发并面向企业|商业贸易的 Linux 发行版。`Red Hat Enterprise Linux` 适用于 `x86`、`x86-64`、`Itanium`、`PowerPC` 和 `IBM System Z` 的服务器版本，以及 `x86` 和 `x86-64` 的桌面版本。`Red Hat` 的所有官方支持和文档以及红帽认证计划中心都围绕 `Red Hat Enterprise Linux` 程序展开。`Red Hat Enterprise Linux` 经常缩写为 `RHEL`，尽管这不是正式名称。

带有该名称的 `Red Hat Enterprise Linux` 最早版本最初出现在市场上的 `Red Hat Linux Advanced Server` 上。2003 年，红帽将 `Red Hat Linux Advanced Server` 改名为 `Red Hat Enterprise Linux AS`，并增加了另外两个版本：`Red Hat Enterprise Linux ES` 和 `Red Hat Enterprise Linux WS`。

虽然红帽使用严格的品牌指令来限制其官方维护的 `Red Hat Enterprise Linux` 软件的免费分发，但即使在没有强制要求的情况下，红帽也会保留地提供原始代码。因此，一些分发版重新生成了经过品牌的社区支持的 `Red Hat Enterprise Linux` 重构版本，这些版本在法律上可以公开，但没有红帽的官方支持。`CentOS`、`Scientific Linux` 和 `Oracle Linux` 旨在与 `Red Hat Enterprise Linux` 保持 100% 的一致性（但在它们的 `Red Hat` 兼容内核之外，`Oracle` 还提供并推广了其非 100% 兼容的 `Oracle_Linux#RHEL_compatibility | Unbreakable Enterprise Kernel`）。此外还有 `Red_Hat_Enterprise_Linux` 的衍生品 | 以及一些不同的著名副产品。

## 红帽目录服务器

“`389 Directory Server`”（以前称为“`Fedora Directory Server`”）是红帽作为红帽社区支持的 `Fedora` 项目组成部分而开发的 `LDAP`（轻量级目录访问协议）服务器。`389` 这个名称源于 `LDAP` 的标准端口。红帽通过 `Red Hat Enterprise Linux`(`RHEL`) 之上的额外订阅提供了一个名为“`Red Hat Directory Server`”的 `389` 版本。`Red Hat Directory Server` 与 `389` 的不同之处在于后者带有红帽标记，包含经过认证的稳定结构、用户便利性和技术支持。红帽必须定期将红帽版本与稳定的上游 `389` 分支进行重基基/rebase，并根据需要回port特定的、跨时代的属性和严重错误修复。`389` 项目的目标是快速获取特定的属性，而红帽文章偶尔冲突的目标是建立稳定性和可靠性。`389` 源代码通常在 `GPL2`# 版本 2)(`GPLv2`) 许可下可用。某些部分具有插件异常，而其他部分使用 `LGPLv2` 或 `Apache` 许可|`AAPL`。

`389 Directory Server` 在 `Fedora`（操作系统)|`Fedora` 之上构建，但支持许多包含 `Red Hat Enterprise Linux 3` 及以后的操作系统、`Debian`、`Solaris`（操作系统)|`Solaris 8` 及以后以及 `HP-UX 11i`。

## 红帽企业虚拟化

“`Red Hat Enterprise Virtualization`”(`RHEV`) 是一种由红帽创建的组织平台虚拟化|虚拟化文章，`http://www.redhat.com/virtualization/rhev-server/` 红帽企业虚拟化 `Red Hat Enterprise Virtualization for Servers`，redhat.com 基于内核的虚拟机|`KVM` 虚拟机管理程序。`Red Hat Enterprise Virtualization` 利用 `SPICE`（协议)| `SPICE` 过程和 `VDSM`（虚拟服务器管理器）以及一个基于红帽企业级 `Linux`(`RHEL`) 的集中管理服务器。它可以利用作为 `Active Directory` 功能类似的 `FreeIPA Active Directory` 模拟器的资源管理器和集群数据，[`RHEV 安装指南|如何管理域`](http://access.redhat.com/knowledge/docs/en-US/Red_Hat_Enterprise_Virtualization/3.0/html-single/Installation_Guide/index.html#References_RHEV_3_Manage_Domains)，但它不支持像 `OpenLDAP` 这样的基于标准的 `LDAP` 服务器。`http://access.redhat.com/knowledge/docs/en-US/Red_Hat_Enterprise_Virtualiza-tion/3.0/html-single/Installation_Guide/index.html#chap-Installation_Guide-Directo-ry_Services` 服务安装指南

`Red Hat Enterprise Virtualization` 工具和方法的一些应用出现在红帽收购 `Qumranet` 之后。`http://www.redhat.com/about/news/prarchive/2008/kumranet.html` 红帽通过收购 `Qumranet, Inc.` 推进虚拟化领先地位。其他部分包括 `oVirt`。`http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/5/html/Hypervisor_Deployment_Guide/chap-Deployment_Guide-Understanding_the_Red_Hat_Enterprise_Virtualization_Hypervisor.html` `RHEL 5` 服务器部署指南，第 2

## Fedora（操作系统）- 发行版

`Fedora` 项目以几种不同的方式分发 `Fedora`：

- `Fedora DVD/CD` 集 - 一套用于安装的 `DVD` 集；
- `Live` 镜像 - 一个可以应用于 `USB` 闪存盘的 `Live` 镜像；
- `Minimal CD` - 应用于 `HTTP`、`FTP` 或 `NFS` 的精简 `CD`。

`Fedora` 项目还发布了一些名为 `Fedora` 的差异化变体。

`Extra Packages for Enterprise Linux` (`EPEL`) 是一个基于社区的尝试，旨在为基于 `Fedora` 的 `Linux` 提供高质量的软件包。

## Fedora（发行版）- 历史

`Fedora` 项目成立于 2003 年末，当时 `Red Hat Linux` 已经结束。`Red Hat Enterprise Linux` 将是红帽唯一维护的 `Linux` 发行版，而 `Fedora` 将是一个社区发行版。红帽将其交付物分叉为 `Fedora`。

带有该名称的第一个版本最初是 `Red Hat Linux Advanced Server`。2003 年，红帽将 `Red Hat Linux Advanced Server` 改名为 `Red Hat Enterprise Linux AS`，并增加了另外两个版本：`Red Hat Enterprise Linux ES` 和 `Red Hat Enterprise Linux WS`。

`Fedora` 的名称源于 2002 年的 `Fedora Linux`，作为一个志愿者项目，旨在为测试的软件包提供单一的仓库。`Fedora` 的名称也源于 `Red Hat Linux` 的 `Fedora Linux`，以及典型的 `Shadowman` 标志。
