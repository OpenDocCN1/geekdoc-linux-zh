

## 附录 H Red Hat 与自由分发的软件
### H.1 自由软件模式
### H.2 “自由软件”的演变
### H.3 GNU 通用公共许可证
### H.4 Linux 会取代商业操作系统吗？
### H.5 Red Hat Software, Inc. 在 Linux 开发中的角色
### H.6 延伸阅读

## 附录 I 许可证
### I.1 BSD 版权声明
### I.2 X 版权声明
### I.3 GNU 通用公共许可证

# 前言

## 什么是 Red Hat Linux？

Red Hat Linux 是一个基于 Linux 内核的完整操作系统，该内核最初由 Linus Torvalds 创建。Linux 继续由一个由 Linus 领导的全球团队通过互联网进行开发，并且仍在快速向前发展。当前稳定的 2.0.x 内核（Red Hat Linux 4.1 基于此内核）展示了 Linux 开发社区的非凡才华和创造力，以及协作开发模式的价值。有关此主题的更多信息，请参阅附录 H，《Red Hat 与自由分发的软件》。

自 4.0 版本发布以来，Red Hat Linux 运行在三大主流计算平台上：Intel 兼容 PC、Digital Alpha 计算机和 Sun SPARC 设备。我们统一的源代码树以及 RPM（Red Hat 包管理）技术带来的优势，使我们能够保持针对这三个平台的 Red Hat Linux 版本同步发布，从而使用户能够以最小的努力在这些平台之间管理和移植软件。

我们很高兴地注意到，在 Linux 操作系统上可用的应用程序数量正在增长，其中一些来自 Red Hat Software。我们通过网站上的无限制 FTP 以及互联网上的许多镜像站点提供我们的 Linux 操作系统版本。Red Hat Linux 也可以 CD-ROM 形式获取。有关我们产品提供的最新信息以及其他 Linux 资源的链接，请访问 Red Hat Software 的网站 http://www.redhat.com。

在大多数系统上，Red Hat Linux 安装很容易：安装程序可以在短短 15 分钟内引导您完成整个过程。系统本身非常灵活：您只需几次鼠标点击即可安装或卸载单个软件“包”。维护也很简单：包安装可以验证和纠正，并且包可以简单可靠地安装和卸载。此外，Red Hat Linux 管理也很方便：捆绑在“控制面板”中的一组图形化管理工具减少了日常系统管理的麻烦。系统自由分发组件的完整源代码均已提供。

## 本书概述

本手册的组织结构如下：

- 第 1 章，快速入门，包含足够的信息，使有经验的用户可以轻松地完成 Red Hat Linux/Intel 的基本安装。我们建议新的 Linux 用户在安装之前通读手册，以便对系统有一个良好的理解。
- 第 2 章，安装 Red Hat Linux/Intel，包含在 Intel 或兼容 PC 上安装 Red Hat Linux 的详细说明。
- 第 3 章，安装 Red Hat Linux/Alpha，包含在 Digital Alpha 上安装 Red Hat Linux 的说明。
- 第 4 章，安装 Red Hat Linux/SPARC，包含在 Sun SPARC 机器上安装 Red Hat Linux 的说明。
- 第 5 – 10 章解释了在安装了 Red Hat Linux 之后如何配置各种服务，如何在系统上查找文档，以及如何使用伴随 Red Hat Linux 的各种系统管理和管理工具。它们还解释了您的 Red Hat Linux 系统的特殊之处，包括特殊文件存放的位置以及如何关闭 Red Hat Linux。
- 附录包含关于 Red Hat Linux 的额外信息，包括硬件要求列表、伴随 Red Hat Linux/Intel 的 MetroLink X 服务器手册、Red Hat Linux 常见问题解答（FAQ），以及获取技术支持的说明。

# 致谢

我们要感谢所有 beta 测试者，他们将他们的系统托付给 Red Hat Linux 的早期版本，并花时间提交 bug 报告，特别是那些自“万圣节”版本甚至更早时期就与 Red Hat 一起工作的人。我们还要感谢 Linus Torvalds 以及世界各地数以百计的开发者，他们真正创造了分布式开发的奇迹。

再次感谢，欢迎来到精彩的 Linux 世界！

Red Hat 开发团队

# 第 1 章
## 快速入门

本章总结了如何安装或升级 Red Hat Linux/Intel；它面向已经熟悉安装 Linux 的用户。如果本章没有提供足够的信息，请阅读第 2 章，*安装 Red Hat Linux/Intel*。

### 1.1 Red Hat Linux 勘误表

偶尔，我们会发现 Red Hat Linux 发布版本中存在一些问题，其中一些问题可能会影响安装。当我们发现问题时，我们会在 Red Hat Linux 勘误表中发布有关该问题及其解决方案的信息，我们通过以下几种方式提供该表：

- 通过万维网：`http://www.redhat.com/errata`
- 通过电子邮件：`errata@redhat.com`

请注意，勘误表中列出的问题的解决方案可能需要您使用与下面提到的或随您的 Red Hat Linux CD-ROM 提供的不同的启动或安装磁盘映像。

### 1.2 获取 Red Hat Linux

获取 Red Hat Linux 有几种方法；最简单的方式是通过 CD-ROM。如果您没有 CD-ROM 驱动器，这可能不切实际，因此我们通过 FTP 免费提供；您可以从附录 F 中列出的任何 Red Hat 镜像站点下载它，*Red Hat Linux FAQ*。

这些镜像站点是为希望通过 FTP 安装或希望获取包升级的人提供的。将发行版下载到硬盘并从中安装是可能的，但对于大多数情况来说这是非常不切实际的，并且超出了本文档的范围。

如需购买 CD-ROM 版本的 Red Hat Linux，请通过附录 F 中列出的任何联系方式联系 Red Hat Software。

### 1.3 制作软盘

如果您拥有随官方 Red Hat Linux 4.1 附带寄送的启动和补充软盘，请跳至以下第 1.4 节。

如果您的 Red Hat Linux/Intel 版本未包含启动软盘和补充软盘，您需要创建它们。如果您的 CD-ROM（或 FTP 站点）上有 README 文件，请立即阅读；它包含有关 Red Hat Linux 4.1 的最新信息，其中一些可能与您即将阅读的内容不同。

启动和补充磁盘映像位于 CD-ROM 和 FTP 站点上的 **images** 目录中。如果您进行 CD-ROM 或 NFS 安装，您只需要制作一个启动软盘。所有其他安装方法还需要补充软盘。您可以使用 Linux 下的 *dd* 或 DOS 下的 *rawrite.exe*（在 *dosutil* 目录中找到）将每个磁盘映像文件写入格式化的高密度（1.44 MB）3.5 英寸软盘。

### 1.4 安装

要安装 Red Hat Linux，请将启动软盘插入 A 驱动器，并将 CD 插入 CD-ROM 驱动器（对于 CD-ROM 安装）或连接到您的网络（对于 FTP 或 NFS 安装）。然后重新启动您的机器，并回答显示的所有问题。如果您从 PCMCIA、FTP 或硬盘安装，请在提示时插入补充软盘。

### 1.5 从先前版本升级

Red Hat Linux 4.1 的安装过程包括从先前的 Red Hat Linux 版本（基于 RPM 技术的 2.0、2.1、3.0.3 和 4.0）进行升级的能力。升级您的系统将安装模块化的 2.0.x 内核以及安装在您机器上的包的更新版本。升级过程使用 `.rpmsave` 扩展名（例如，`sendmail.cf.rpmsave`）保留现有的配置文件，并留下一个日志，记录它在 `/tmp/upgrade.log` 中采取了哪些操作。随着软件的发展，配置文件格式可能会发生变化，因此您应该在集成更改之前仔细比较您的原始配置文件和新文件。

要升级 Red Hat Linux 系统，您必须使用启动软盘（以及可能的补充软盘），就像执行完全安装一样。在选择安装介质（并在需要时设置网络信息）之后，安装程序会提示您选择 **Install**（安装）或 **Upgrade**（升级）；请选择 **Upgrade**。此升级过程在功能上等同于在先前版本的 Red Hat Linux 中运行 `upgrade` 脚本。

请注意，一些升级的包可能“依赖”于可能未安装在您的系统上的其他包。升级过程会处理这些 *dependencies*（依赖项），但它可能需要安装额外的包以满足这些依赖项。

### 1.6 直接从 CD-ROM 运行

先前版本的 Red Hat Linux 在 CD-ROM 上附带一个“实时文件系统”；这允许用户在不首先将其安装到硬盘上的情况下直接从 CD-ROM 运行 Red Hat Linux。

不幸的是，随着模块化的 Linux-2.0.x 内核，添加“实时”启动功能变得太复杂，不再支持。我们对造成的不便表示歉意。

