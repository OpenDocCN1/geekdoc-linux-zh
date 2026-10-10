
- `tcpdump`....................................................................................................... 785

- `netstat`........................................................................................................... 785

- Nagios.............................................................................................................. 786

# 录 A：获取与升级 Fedora ................................................................ 787

- 下载镜像................................................................................ 787

- Fedoraproject.org 下载.................................................................. 788

- 直接下载位置................................................................................ 790

- 使用 BitTorrent............................................................................... 790

- 元链接............................................................................................... 791

# 表列表.................................................................................... 793

# 图列表............................................................................................... 799

# 索引......................................................................................... 807

# 第一部分：系统管理

- 简介

- 基础系统管理

- 软件管理

- 服务管理

- 系统信息

- 用户管理

- 内核管理

- 虚拟化

# 11. Fedora 11 简介

- Linux 概述

- Fedora Linux

- Fedora 文档

- Fedora 11 更改

- 标准 Fedora 功能

- Fedora 桌面

## 第1章：Fedora 11 简介

特定主题的文档，如安装和桌面用户指南可以在 http://doc.fedoraproject.org 查看（见表 1-1）。

| 网站 | 名称 |
| --- | --- |
| http://fedoraproject.org | Fedora 资源 |
| http://download.fedoraproject.org | Fedora 软件库，镜像链接 |
| http://mirrors.fedoraproject.org | Fedora 镜像列表 |
| http://download.fedora.redhat.com | Fedora 仓库站点 |
| http://fedoraproject.org/wiki/Fedora_11_tour | Fedora 11 导览，包含图片和视频 |
| http://fedoraproject.org/wiki/Tools/yum | YUM 工具 |
| http://docs.fedoraproject.org/install-guide/f11 | Fedora 安装指南 |
| http://fedoraproject.org/wiki/CommunityWebsites | 社区网站 |
| http://fedoraproject.org/wiki/Overview | Fedora 项目概述 |
| http://fedoraproject.org/wiki/FAQ | Fedora 常见问题解答 |
| http://docs.fedoraproject.org | Fedora 发行版的文档和支持教程。 |
| http://fedoraforum.org | 用户讨论支持论坛，由 Fedora 项目支持。包含 FAQ 和新闻链接。 |
| http://fedoraproject.org/wiki/FWN | 收集 Fedora 的最新新闻和进展。 |
| www.linuxfoundation.org | Linux 基金会，官方 Linux 开发。 |
| http://kernel.org | 最新的 Linux 内核。 |
| www.redhat.com | 红帽官方网站 |
| http://magazine.redhat.com/ | 红帽杂志，包含关于最新进展的专业文章。 |
| www.centos.org | 社区企业级操作系统，CENTOS（基于红帽） |

表 1-1：Fedora 版本

Linux 版本是完全免费的。你可以从 http://fedoraproject.org 或 http://download.fedoraproject.org 下载最新版本（包括测试版）。http://download.fedoraproject.org 地址将链接到最适合你的可用镜像。你可以使用更新系统（`PackageKit`）更新 Fedora 以访问 Fedora 仓库。访问将在安装期间自动配置。

### Fedora 文档

Fedora 的文档可以在 http://docs.fedoraproject.org/wiki/Docs 找到（见表 I-1）。Fedora 安装指南提供了对所有安装程序的详细描述。Fedora 桌面用户指南涵盖了登录等基本桌面操作。

http://fedoraforum.org 站点是一个由 Fedora 赞助的终端支持论坛。你可以在这里发布问题并检查常见问题的回复。

你的 Firefox 浏览器将配置有面板，用于访问常用的文档和支持网站。这些包括 Fedora 项目主页、Fedora 周报、来自 Fedora 论坛和社区的社区支持，以及红帽杂志。

Fedora 维护着详细的专业文档，关于理解如何配置 `SELinux` 的信息。对于大部分文档，你可能需要依靠位于 `/usr/share/doc` 的安装文档、Man 页和 info 页面，以及桌面上运行的不同应用程序的上下文帮助。`GNOME`、`KDE` 和 `OpenOffice` 的官方网站将提供大量的相关文档。对于安装，你可以使用 http://docs.fedoraproject.org/install-guide 上的 Fedora 安装指南。

红帽还维护着庞大的红帽企业 Linux（`RHEL`）文档库，这适用于 Fedora。从红帽主页，你可以点击进入支持页面，然后进入文档页面。文档页面提供了一个弹出菜单，从中可以选择产品。文档涵盖了虚拟化、全局文件系统 (`GFS`)、逻辑卷管理 (`LVM`) 和安装指南等主题。还提供了 Tip、HOW 和 FAQ 文档。所有红帽文档均根据 GNU 通用公共许可协议免费提供。在你的系统上安装红帽 Linux 之前，你可能想检查在线安装指南。红帽杂志提供了有关最新功能的信息。

### Fedora 11

Fedora 的新版本对关键应用程序进行了主要更新，并替换了以前的程序。有一个新的用于管理防火墙的配置工具 `system-config-firewall`。默认音频接口是 `PulseAudio`，尽管 `ALSA` 仍提供驱动程序。`GNOME` 在线桌面的演示提供了访问邮件、Google 文档和 flick 等在线服务的便利。

安装 Fedora 的过程持续简化。你可以从安装 DVD 或 Live CD 进行安装。系统会安装一套核心应用程序，你可以根据意愿添加它们。安装后，添加的软件将根据哪个版本较新从磁盘或在线仓库获取。你会发现磁盘上的软件会很快过时。大多数软件将从在线 Fedora 仓库获取。安装界面已减少到仅几个屏幕，可以快速通过默认分区、网络检测和时间设置，然后进入软件包选择。防火墙和 `SELinux` 配置属于安装后配置程序的一部分。
