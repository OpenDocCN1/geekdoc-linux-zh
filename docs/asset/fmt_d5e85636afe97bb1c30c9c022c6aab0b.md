
# 第一部分：在 Fedora 和 RHEL 中入门

## 第 1 章：Fedora 和 Red Hat Enterprise Linux 概述

### 介绍 Fedora 9 和 Red Hat Enterprise Linux

### 什么是 Linux?

### Linux 在 UNIX 中的根源

### 什么是操作系统?

### 常见的 Linux 特性

### Linux 的主要优势

### 什么是 Red Hat Enterprise Linux 和 Fedora?

### Red Hat 到 Red Hat Enterprise Linux

### 在 Fedora 和企业版之间选择

### 为什么选择 Fedora 或 Red Hat Enterprise Linux?

### Fedora 9 的新功能

### K 桌面环境 (KDE) 4

### PackageKit 软件管理

### Firefox 3 浏览器

| 章节 | 页码 |
| :--- | :--- |
| 介绍 Fedora 9 和 Red Hat Enterprise Linux | 4 |
| Linux 在 UNIX 中的根源 | 6 |
| 常见的 Linux 特性 | 8 |
| 什么是 Red Hat Enterprise Linux 和 Fedora? | 11 |
| 在 Fedora 和企业版之间选择 | 14 |
| Fedora 9 的新功能 | 17 |
| PackageKit 软件管理 | 18 |

本书包含三个附录。附录 A 描述了配套媒体的内容。附录 B 提供了设置和运行服务的概述。附录 C 涵盖了 Red Hat Enterprise Linux 5 中的功能。

# 关于配套媒体

随书附赠的 Fedora 9 DVD 提供了运行一个完整 Fedora 系统所需的软件。通过这些软件，您可以安装一系列软件包，安装后的空间从几兆字节到一百 GB 不等。

本书描述了如何配置和使用这些不同媒体的软件。

本版本的《Fedora 和 RHEL 圣经》配套网站的一项功能是高级链接页面，旨在帮助您解决在使用 Fedora 时遇到的常见问题。如果您在书中没有找到答案，请访问书籍网站 `www.wiley.com/go/fedora9bible`，查看有关该主题的一些新信息。

即使在本书长达 1,000 页的情况下，仍有几个主题似乎未收录。配套网站包含了关于 X Windows 系统、寻找附加软件、探索替代性管理界面、Logsentry 和 Portenz 等主题的额外材料。

由于 LILO 启动加载程序在最近的几个发行版中已从 Fedora 中移除，我决定将 LILO 的描述移出本书并放到网站。从之前的版本移动到网站的其他主题包括：遗留 UNIX 远程命令（`login`、`rcp` 等）、运行 Tripwire 管理系统安全、在 Linux 中运行 NetWare 服务器（`mars_nwe`）以及使用 `crack` 和其他密码保护工具。从紧邻上一版本移动过来的功能包括：`wu-FTPd` FTP 服务器、`own server` 以及 `sendmail cf` 文件的描述。

特别感谢 Red Hat, Inc. 的人员以及 Fedora 项目的成员。特别是 Paul Fields（新任 Fedora 项目负责人）、Max Spevack（离任的 Fedora 项目负责人）和 Greg DeKoeningberg（Fedora 社区领袖），他们在生产持续高质量 Linux 发行版方面的领导值得赞誉。

特别感谢 Jessie Keating（Red Hat Fedora 工程师）帮助我使用他的 Penguin 工具制作了随书附赠的 8GB Fedora DVD。还要感谢在这一版本的开发期间回答我问题的 Fedora 项目成员：Christopher Allison、Rahul Sundaram、Seth Vidan、Ian Weller、Dan Williams 和 David Zeuten。

在 Wiley，我要感谢 Jenny Watson、Colleen Hauser 和 Laura Moss-Hollister，处理了与本书相关的宣传、媒体和封面问题。感谢 Sara Shlaer 对本书的持续编辑和制作工作，并确保了进度，以便我们能将这书带给你们。

感谢 Debra Banning 在制作的最后阶段为本书提供保护。Tim Boronczyk 提供了详尽的技术编辑建议。感谢 Waterside Productions 的 Margot Maley Hutchison 等人让我加入了这个项目。

一如既往，感谢我的家人帮助我完成这个项目。

最后，特别感谢购买了本书及更早版本《Red Hat Linux 圣经》的读者。在你们的工作、家庭和社区中成为 Linux 的力量吧。如果您想扩展您的 Linux 视野，请尝试我写的其他书籍：

- `Linux Bible 2008 Edition` —— 包含 DVD 和 CD 上 16 个不同的可启动和可安装的 Linux 发行版，并对这些和其他流行的有趣的 Linux 发行版进行了描述。
- 与 François Caen 合作的 `Fedora Linux Toolbox` —— 包含 1000 多条命令，帮助 Fedora、RHEL 和 CentOS 用户充分利用 Linux。如需尝试其他类似的发行版，请查看同一作者的 Ubuntu Linux Toolbox、SUSE Linux Toolbox 和 BSD Toolbox。
- 与 Thomas Weiss 合作的 `Troubleshooting Bible` —— 超出本书，帮助您安全地部署和排除 Linux 系统的故障。
- `Linux II` —— 如果您正在寻找一些好玩的 Linux，这本书包含了九个你可以用 PC 和开源软件构建的优秀项目。

| 标题 | 页码 |
| :--- | :--- |
| 使用 Metacity 窗口管理器 | 100 |
