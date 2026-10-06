

## 第 1 章：Fedora 与 Red Hat Enterprise Linux 19 概述

替代了 Red Hat 开发的包更新器 (pup) 和包管理器 (pirit) 程序的系统。

通过 PackageKit，顶部栏上的图标会在有可用软件更新时提醒您。或者，您也可以使用 GNOME 的 PackageKit 管理器来搜索并安装额外的软件包。PackageKit 将在第 5 章中介绍。

## Firefox 3 Web 浏览器

此版本的 Firefox Web 浏览器在安全性、易用性、个性化和性能方面进行了改进。当网站使用扩展验证 (EV) SSL 证书时，可以点击（通过地址栏中的图标）直接访问网站的安全信息。通过 EV SSL 证书，证书颁发机构会验证您访问的正是该网站声称的网站。密码信息栏可以显示之前的密码。

在个性化方面，书签通过添加标签得到了改进，以便按主题进行排序。您可以使用智能书签立即访问最近标记或创建的书签。在地址栏中，自动补全功能得到了改进，在您输入 URL 时会显示频繁和最近访问的地址。

## 升级前准备 (Preupgrade)

升级前准备功能允许您安装并运行一个准备程序，将 Fedora 9 系统准备升级到 Fedora 10。该功能让您在仍使用现有系统时，就能完成升级过程中大部分耗时的下载和依赖关系检查。升级前准备将在第 2 章中介绍。虽然您可以在 Fedora 8.1 上运行 preupgrade，但我建议在尝试使用它之前，先完全升级到 Fedora 9。

## Ext4 文件系统

系统添加了支持，使 Fedora 可以处理 ext4 文件系统类型。ext4 文件系统旨在提供比 ext3 系统更好的性能和可扩展性。虽然在用户 ext4 文件系统的方式上应该没有区别，但 Fedora 10 包含了一套用于创建、检查和维护 ext4 文件系统的工具。

## 加密文件系统

通过使用 Fedora 10 中的 cryptsetup 和 LUKS 功能，您可以加密除根 (/) 和 /boot 分区以外的文件系统。加密文件系统对于保护笔记本电脑系统上的数据尤为重要。

## 使用 freeIPA 进行身份管理

Fedora Linux 添加了用于跨企业级管理身份、策略和审计功能的 freeIPA 框架。freeIPA 的长期目标是提供一种开源机制，用于集中维护这些关键的安全和监控功能。第 14 章包含了对 freeIPA 的描述。

## 第一部分：在 Fedora 和 RHEL 中入门

## NetworkManager

为了简化连接有线和无线网络的过程，NetworkManager 正在提供持续改进。在 Fedora 10 中，它是连接和管理有线及无线接口的默认方法。

## 获取自定义版本 (Spins)

Fedora 过去以一组 CD 或 DVD 发布，其中包含所有 Fedora 软件包，可以从这些介质进行安装。 Fedora 7 首次添加的用于创建自定义软件仓库 (Pungi) 和自定义现场 CD (livecd-creator) 的新工具，其结果以不断增长的自定义版本 (spins) 集的形式持续改进。

自定义版本是一个 CD、DVD 或 USB 闪存盘镜像，可以作为现场 CD 或 Fedora 安装程序运行。官方版本包括：

-   **Fedora DVD**：包含至少 4GB 的内容，涵盖桌面、服务器和软件开发软件包的交叉部分，您可以将其安装到硬盘上。该磁盘的内容与您在 Fedora Core 中使用的类似。
-   **Fedora CD Set**：这套 6 张 CD 包含了 Fedora 安装 DVD 的所有内容。这是为那些电脑上没有 DVD 驱动器的人准备。
-   **Fedora Desktop Live CD (GNOME)**：从这一张 700MB 的 DVD 中，您可以运行 Fedora 10 的 Gnome 桌面现场/安装 CD。桌面上有一个安装图标，随后即可将该桌面系统安装到硬盘中。
-   **Fedora Desktop Live CD (KDE)**：Fedora 通过提供 Fedora 10 的 KDE 桌面现场/安装 CD 来展示 KDE。在 GNOME 桌面上，您可以选择安装图标将 KDE 桌面系统安装到硬盘中。书中附带这张 CD。
-   **Everything DVD**：一套“全能”2-DVD 套装包含整个 Fedora 10 仓库 (11GB)，预计在 Fedora 10 发布后不久产出。这套组件适用于想要获取 Fedora 10 每一个可安装软件包的人。。随这套组件提供的 DVD 包含了两张 Everything DVD 的大部分内容，录制在高容量 DVD-9 上。

书中包含的 KDE 桌面和 Nearly-Everything DVD 适用于标准的 32 位 PC (i386)。如果您需要介质在 PowerPC (PPC) 或 64 位 PC (X86, 64) 计算机架构上安装 Fedora，可以使用 Bittorrent (http://spin.fedoraproject.org) 或官方 Fedora 公共镜像站点 (http://mirrors.fedoraproject.org) 下载这些介质的 ISO 镜像。有关从这些不同介质使用和安装 Fedora 的信息，请参考第 2 章。

自定义版本页面上也可以获取非官方的自定义版本。到目前，已有 Fedora (http://fedoraproject.org/wiki/CustomSpins) 现场开发者、游戏、Xfce 桌面和电子实验室版本。（spin 一词的意思是

## 第 1 章：Fedora 与 Red Hat Enterprise Linux 21 概述

从 Fedora 软件仓库编译软件，并组合成一个更多的可启动镜像（通常为了适应 CD 或 DVD），让您能够运行或安装。

## 创建您自己的版本 (Spins)

项目用于构建软件包和创建现场 CD 的相同工具随 Fedora 一起发布。这意味着任何人都可以这些工具创建自己的安装 CD，然后将软件包集转换为自己的仓库。使用这些仓库，您可以安装或运行。

Pungi (hosted.fedaproject.org/projects/pungi) 是为 Fedora 构建系统本身的项目。pungi 软件包包含 pungi 命令和相关的配置文件。您可以使用 pungi 命令制作自己的安装树，生成可安装的镜像。

Fedora 现场 CD 项目 (http://fedoraproject.org/wiki/FedoraLiveCD) 生成了从 Fedora 软件仓库构建现场 CD 的工具。创建这些现场 CD 的主要工具是 lived-creator。请参考 Live CD HOWTO (http://fedoraproject.org/wiki/FedoraLiveCD/LiveCDHowTo) 获取使用 lived-creator 的信息。

lived-creator 的最新功能可以使用 kickstart 文件（第 2 章描述）来指导现场 CD 的创建。这意味着您用于 anaconda 自动化安装的格式也可用于保存创建现场 CD 的软件包列表和其他设置。

## 防火墙配置

防火墙配置窗口进行了增强，提供了以前需要手动添加到 iptables 中的功能。特别是，您可以选择端口进行端口转发（例如，如果您想在防火墙后的私有地址上运行 Web 服务器）。您还可以指定您支持的 ICMP 类型，例如常用的 echo `ping` 和 echo `pong`。

## 自由软件文化

我无需多说 Linux 的自由软件开发文化已经繁荣并将继续繁荣。Fedora 和 Red Hat Enterprise Linux 系统的版权受 GNU 公共许可证保护。大多数自由软件遵循的该许可证提供了以下内容：

-   **作者权利**：原始作者保留对其软件的权利。
-   **自由分发**：人们可以在自己的软件中使用 GNU 软件，并根据意愿进行更改和重新分发。他们必须在分发版中包含源代码（或使其易于获取）。
-   **维护版权**：即使您重新包装并销售该软件，也必须维护原始的 GNU 协议。这意味着所有

