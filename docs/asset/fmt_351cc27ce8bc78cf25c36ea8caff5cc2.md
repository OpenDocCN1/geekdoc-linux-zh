
## 最佳实践：内核安全风险缓解

在保护 Linux 系统安全的战斗中，工具可能是内核。这是合理的，因为内核是 Linux 操作系统的核心。主流 Linux 发行版的开发者在创建和更新用于二进制格式的安全内核方面做得非常好，可以快速安装。

# 第二部分 分层安全与 Linux

不同发行版的背后开发人员可能将精力放在其他功能层级上。例如，Ubuntu 发布了针对服务器、客体虚拟机、Xen 宿主机，甚至是亚马逊企业云的发行版。所有 Linux 发行版都从由 Linux Torvalds 领导的内核组织（Kernel Organization）开发的原生内核开始。

原生内核的发布遵循主版本.修订版本.更新版本.补丁的格式。大约每三个月发布一次新更新。稳定版本会同时进行维护。想要更新原生内核的管理员可以使用内核组织发布的补丁。

位于 `http://linux.org/` 上的 Linux 内核邮件列表可以帮助你监控与原生内核相关的安全问题。Linux 发行版的背后开发人员维护着自己的邮件列表，突出显示与为其发行版构建的自定义内核相关的安全问题。由于并非所有的内核更新都与安全问题有关，你可能不想安装所有更新。如果你安装了内核更新，那么保留当前安装的内核是非常重要的，以防更新为你的系统带来麻烦。

如果你想自定义 Linux 内核，可以从原生内核或 Linux 发行版开发人员发布的源代码开始。你还需要开发软件来定制内核并编译定制后的代码。

在定制内核之前，务必使用如 `make clean` 等命令检查与源代码相关的目录。考虑从 `configs/` 子目录或 `/boot/` 目录等基准开始。即使你倾向于将这项工作交给 Linux 发行版的开发人员，也要通过可以通过 `make menuconfig` 命令访问的控制台工具来查看 Linux 内核的可用选项。

自定义内核配置保存在源代码目录下的 `.config` 文件中。自定义扩展可以在该目录下的 `Makefile` 中进行配置。配置自定义内核所需的命令因发行版而异。原生内核可能使用其他方法。完成后，请确保自定义内核不会覆盖 `/boot/` 目录中当前运行的内核以及任何相关的引导器配置文件。

当你对某个内核满意时，你可以在 `/proc/` 文件系统中执行更多操作来加固系统。动态内核配置选项可以在 `/proc/sys/` 子目录的布尔（Boolean）文件中可用。这些选项中的某些可以保护系统免受 DoS 攻击、伪造源和目的地址、路由表远程重配置等影响。你可以在 `/etc/sysctl.conf` 文件中配置相同的选项，使所需的更改在重启后依然有效。

## 第 10 章 | 内核风险缓解

### 本章总结

作为 Linux 操作系统的中心，Linux 内核处于 Linux 安全的核心。尽管大多数用户是从发行版开发人员创建的内核开始的，你也可以从 Linux 内核组织开发者创建的原生内核开始。无论选择哪一种，通过适当的补丁和更新保持该内核更新都是关重要的。然而，并非所有更新都与安全有关。由于内核更新可能会影响系统的功能，因此需要谨慎处理。

你可以根据 Linux 内核组织或所选发行版开发人员发布的源代码来定制内核。通过正确的开发工具，你可以定制与内核相关的选项，然后将其编译为二进制格式。你需要注意保留任何现有的内核，否则新定制内核的问题可能会导致系统无法启动。

### 核心概念与术语

| | |
| :--- | :--- |
| 回溯 (Backport) | 混乱简化强制访问 (Mangled Simplified mandatory access) |
| Greg Kroah-Hartman | 火星数据包控制内核 (SMACK) |
| iSeries Meta 包 | 伪造 (Spoofed) |
| Itanium 虚拟化 (Itanium Paravirtualization) | 原生内核 (Stock kernel) |
| Linux Torvalds | pSeries TOMOYO |
| Linux 安全模块 (LSMs) | |

## 第 10 章评估

- 1. 在许多 Linux 发行版中，以下哪项功能不再与独立的内核相关？

- 2. 当发布带有安全更新的更新内核时，内核中的下列哪个数字发生了变化？
- A. 虚拟机宿主机
- B. Xen
- C. SMP
- D. 服务器

- A. 主版本
- B. 次要版本
- C. 更新版本
- D. 补丁号

- 3. 下列哪条命令可以用于解包和解压 `.xz` 格式的原生内核？
- A. `tar xzf`
- B. `tar xjf`
- C. `tar xbf`
- D. `tar xuf`

- 4. 与内核组织相关的网站是 _________。

- 5. 在实施新内核时，你应该采取以下哪项操作？
- A. 升级 (Upgrade)
- B. 安装 (Install)
- C. 补丁 (Patch)
- D. 编译 (Compile)

- 6. 下列哪个目录包含本地系统当前运行内核的配置文件？
- A. `/usr/src/redhat/BUILD/kernel-r / linux-uname -r /`
- B. `/usr/src/linux-uname -r /configs/`
- C. `/usr/src/linux-uname -r /`
- D. `/boot/`

- 7. 下列哪条命令启动用于定制内核的基于控制台的菜单驱动工具？
- A. `make config`
- B. `make menuconfig`
- C. `make xconfig`
- D. `make gconfig`

- 8. 下列哪个内核选项与强制访问控制无关？
- A. SELinux
- B. TOMOYO
- C. 加密 API (Cryptographic API)
- D. AppArmor

- 9. 写出与 ext2 和 ext3 等格式相关的内核配置工具的文件名。
- A. 文件系统 (Filesystems)
- B. 设备驱动程序 (Device Drivers)
- C. 网络 (Networking)
- D. 安全特性 (Security Features)

- 10. 你可以在哪个配置文件中自定义内核？
- A. Filesystems
- B. Device Drivers
- C. Networking
- D. Security Features

- 11. 在编译并安装新内核时，哪个文件应该包含？
- A. `/boot/`
- B. `/etc/`
- config
- D. `Makefile`

- 12. 如果 `/etc/sysctl.conf` 中看到 `ipv4.icmp_echo_broadcasts = 1`，哪个文件包含该布尔选项？
- A. `/proc/net/ipv4/icmp_echo_broadcasts`
- B. `/proc/net/ipv4/`
- C. `/etc/`
- D. `/proc/sys/`

- 13. `/etc/sysctl.conf` 中的下列哪个指令应设置为 0 以禁用本地系统的路由？
- A. `net.ipv4.forward`
- B. `net.sys4.route`
- C. `net.ipv4.routing`
- D. `net.sys4.source`

## 第三部分 构建分层策略

- 第 11 章 管理告警与更新
- 第 12 章 构建与维护安全基线
- 第 13 章 测试与报告
- 第 14 章 检测与响应安全违规
- 第 15 章 最佳实践与新兴技术

## 管理告警与更新

计算机安全是一场持续的战斗。从安全告警发布的一刻起，寻找漏洞系统的攻击者与安装更新修复漏洞的管理员之间就开始了竞争。由于某些更新可能会带来风险，这种竞争被放缓了。

战斗始于发行版。发行版的背后开发人员在及时发布安全更新方面表现出色。由于他们以二进制包的形式在结构化存储中发布更新，因此安装非常容易。发行版开发人员还整合了来自 OpenOffice.org 等软件的更新。Linux 管理员在此过程中也有盟友，包括安全与开放方法研究所 (ISECOM)、美国国家安全局 (NSA) 以及开源社区。

## 第 11 章主题

本章涵盖了以下主题和概念：

- 如何跟进发行版安全
- 如何跟进应用安全
- Linux 系统提供哪些防杀病毒选项
- 如何使用漏洞报告
- 开源世界中的安全机制是如何运作的
- 如何决定使用自动更新还是分析后的警报
- 如何管理 Linux 补丁
- 更新管理器的选项有哪些
- 什么是商业更新管理器
- 安全操作管理的最佳实践是什么

## 第 11 章目标

当你完成本章学习后，你将能够：

- 跟进 Linux 安全问题
- 选择合适的防杀病毒系统
- 从开源社区中获取帮助
- 选择一个更新管理系统

## 跟进发行版安全

尽管 Linux 仍然是 Linux，但许多安全问题是特定于发行版的。在本节中，你将回顾用于跟进每个发行版最新安全问题的各种方法。本节回顾了与 Red Hat、Ubuntu 及其衍生发行版相关的安全列表。

虽然 Red Hat Enterprise Linux (RHEL) 是基于 Red Hat 软件的稳定企业级发行版，但某些企业会选择基于 Red Hat 的发行版。两个主要选项是 Fedora Core（它是未来 Red Hat Enterprise 版本的开源开发测试平台）和 CentOS（它基于根据 GNU 通用公共许可证发布的 Red Hat Enterprise Linux 源码）。CentOS 与 Red Hat Enterprise Linux 在二进制层面是完全一致的。这意味着尽管

> 注意
这里引用的 URL 可能会随时间推移而变化。

它可能使用不同的标识（图标、壁纸等），但可执行文件与 RHEL 中提供的文件是相同的。

本节中提出的挑战应该激励你将系统标准化为一种 Linux 发行版。

## Red Hat 警报

Red Hat 不仅仅是 Red Hat Enterprise Linux (RHEL)。虽然 RHEL 是 Red Hat 的旗舰发行版，但它并不是与 Red Hat 软件相关的唯一选项。CentOS Linux 将面临与 RHEL 相同的问题，因此任何 RHEL 警报都适用于 CentOS。

## Red Hat Enterprise Linux

对于 RHEL，有两种方法可以监控安全公告：

- Red Hat 安全通告 (RHSAs) 列表：`https://www.redhat.com/security/security/rhsa`
- Red Hat 安全通告 (RHSAs) 列表：`https://www.redhat.com/security/security/rhsa`

此外，安全简单摘要 (RSS) 馈也是可用的。如果你发现 RHEL 的安全问题，可以联系 Red Hat 安全团队：`https://access.redhat.com/security/team/contact`。

在提供企业级支持的方面，Red Hat 为 RHEL 提供至少七年的安全更新。

## CentOS Linux

CentOS 的开发者使用根据开源许可证发布的 Red Hat 源码。正因如此，CentOS 发行版在二进制层面与 RHEL 是完全一致的。这意味着 CentOS 中的二进制文件与 RHEL 中的文件是相同的。

大多数 CentOS 软件问题也适用于此类。为了避免商标问题，CentOS 修改了 RHEL 源码以移除商标。

## 第 11 章 | 管理安全警报与更新

此外，Red Hat 更新与 CentOS 更新之间通常存在时间滞。当 RHEL 源码公开发时，CentOS 后面的志愿者需要一些时间对源码进行编译和测试。

（重建是指基于另一个发行版的源码的 Linux 发行版。例如，CentOS 是 Red Hat Enterprise Linux 的重建。）

CentOS 有一个安全公告邮件列表：`http://lists.centos.org/mailman/listannounce/`。等效信息也可以在 CentOS 论坛上获得。CentOS 公告和更新包通常后于 Red Hat 几天。当然，CentOS 比 Red Hat Free。

> 注意
选择权在于你：订阅 RHEL 的成本是否值得获得更快的更新？

## Fedora Core Linux

Fedora Core 是 RHEL 的测试平台。RHEL 的版本大约每一到三年发布一次。此外，RHEL 获得企业级支持和与其相关的优势。另一方面，Fedora Core 的版本大约每六个月发布一次。

Fedora Core 通常随最新 Linux 内核发布。然而，由于 Linux 内核组织的开发者为多个内核版本创建安全补丁，拥有最新内核并不意味着具有安全优势。

目前，Fedora 安全警报 wiki 页面位于 `http://fedoraproject.org/wiki/Security`。尽管 Fedora Core 主要由社区支持，但 Red Hat 工程师是由一组志愿者开发的。安全更新取决于开发者的可用性以及团队分配的时间。

## Ubuntu 警报

严格来说，Ubuntu 发行版是用户界面 (GUI) 的 GNU 桌面环境 (GNOME)。最后，Ubuntu 发行版包含了 KDE。

一个主要的供应商漏洞公告来源是由 MITRE 公司（一家非营利研究机构）代表美国国土安全部网络安全局维护的。MITRE 的漏洞列表被称为常见漏洞与披露 (CVE) 列表。相关信息请参阅 `http://cve.mitre.org/cve/`。你可以使用 CVE 编号轻松查找有关漏洞的信息。这对于已安装的包尤为重要。

## 第11 章 | 管理安全告警与更新

在多个 Linux 发行版中。每个发行版可能会发布自己的安全公告，但它们通常会引用通用的 CVE 公。

本节重点关注用户应用程序，主要是那些位于 GUI 桌面环境的程序。事实上，本节列出的三个示例都是 GUI 应用程序。OpenOffice 套件是 Microsoft Office 的一个开源替代方案。LibreOffice 是另一个。如果你使用基于控制的应用程序（例如用于电子邮件的 `matt` 或用于 Web 的 `el`），你也可以考虑监控这些应用程序开发者提供的邮件列表或类似的通知系统。

## OpenOffice 软件件

作为标准的 Linux 发行版，OpenOffice.org 拥有自己的安全团队。当发现问题时，它们会在安全公告中在网上突出显示。你可以在 `http://www.openoffice.org/security/alerts.html` 订阅 OpenOffice.org 安全告警。

OpenOffice.org 背后的开发者会定期更新他们的软件。在可用的情况下，OpenOffice.org 可能会出现在与某个 OpenOffice.applications 相关的告警中。某些安全告警可能通过对 OpenOffice.org 网站的更新来解决。另一些可能通过策略来解决。例如，如果病毒通过某种图像格式传输，该格式可能会建议你和你的成员避免加载此类类型的文件——直到 OpenOffice.org 网站的下一个版本可用为止。

可能的情况下，从与发行版相关的存储库实施更新更为简单。然而，发行版并不总是与其上游开发者保持同步。在某些情况下，上游软件可能会更新到更高的版本，但 Linux 发行版可能选择不更新包。对于系统管理员来说，跟踪所有底层包及其最新发布版本需要更多工作。然而，在某些情况下，这是必要的。

## 浏览器

Web 浏览器是一个选择可能会让安全专业人员的工作变得更复杂的领域。标准的 Ubuntu 存储库提供了六种浏览器，可以通过直接在线访问轻松获取。因此，限制用户可以下载和安装的内容可能符合你的利益。一种基于自定义存储库的方法在本章的后半部分描述。

- 许多浏览器。Mozilla Firefox 是在 Microsoft 和 Apple 操作系统上常见的源浏览器之一；它在 Linux 下也运行。Firefox 还是 Iceasel 浏览器的基础，该浏览器可能安装在某些 Linux 发行版上。

Mozilla 基金会是 Firefox 浏览器以及其他开源工具如 Thunderbird 电子邮件管理器和 SeaMonkey 应用程序套件背后的开源组织。Mozilla 在 `http://www.mozilla.org/security/announce/` 维护一份安全公告列表。此类公告在 `http://www.mozilla.org/security/known-vulnerabilities/` 按产品分类。

相比之下，Conqueror 是 KDE 桌面环境的一部分。因此，KDE 基金会的开发者处理安全问题。对于 KDE 来说，很少有与该桌面环境直接相关的安全问题。正如你在 `http://www.kde.org/info/security/` 看到的，在过去的十年中 KDE 软件发布了几十份公告，包括 Conqueror 浏览器。

Chromium 是另一个在 Linux 下运行的浏览器。它是 Google Chrome 浏览器的开源版本。Chromium 看起来和操作起来和 Chrome 一一样。如果你在它运行的某个平台上习惯 Chrome，你会非常习惯 Chromium。

## Adobe 应用程序

鉴于便携文档格式 (PDF) 和 Flash 播放器等 Adobe 格式的流行，Linux 管理员监控此类应用程序的状态至关重要。可以在网上 `http://www.adobe.com/support/security/` 找到 Adobe 安全公告。

更新可能会出现问题。旧版 Ubuntu 的存储库可能甚至没有 Adobe Reader 的最新包。然而，Adobe 同时以 Debian 和 Red Hat 包管理格式进行打包，这使得将这些包整合到本地存储库并在稍后的章节中成为可能。

或者，Linux 有原生的 PDF 阅读器，以及针对 Flash 播放器等 Adobe 技术的开源替代方案。此类包通常通过标准的 Ubuntu 和 Red Hat 存储库更容易获得。标准的 GNOME 和 KDE 替代方案被称为 evince 和 KPDF。有关更多信息，请参阅 `http://projects.gnome.org/evince/` 和 `http://kpdf.kde.org/`。这些开源应用程序偶尔会出现安全问题。

## 服务应用程序

对于那些不需要管理 Linux 桌面环境的人来说，挑战会小一些。在这种情况下，你只需要监控与服务器上运行的应用程序相关的安全告警。

开源服务应用程序的安全基本模式是一致的。随着开源开发在公众面前进行，开源安全告警和更新公开可用。为此，本节描述了你如何跟踪与 Apache Web 服务器、Samba 文件服务器以及各种文件传输协议 (FTP) 服务器相关的安全问题。

大多数 Linux 发行版（包括 Red Hat 和 Ubuntu）背后的开发者通过提供适当的二进制格式包来支持这些服务的安装。此类包包含许多预配置选项。

## 第11 章 | 管理安全告警与更新

## Apache Web 服务器

运行 Apache Web 服务器的管理员可以通过 Apache 服务器公告与相关安全问题保持同步。要订阅，请向 `announce-subscribe@http.apache.org` 发送电子邮件。有关当前的漏洞列表，请导航到 `http://http.apache.org/security_report.html`。

Apache 开发者以类似于 Linux 内核开发者的方式维护其多个版本的 Web 服务器软件。可能同时有两个 Apache 版本分支（“分支”是指某个特定版本的一种方式，以防同时开发了多个版本）。Apache 的首选是 1.x 版本分支，第二个是 2.x 版本分支。你在 Linux 发行版上通常安装 2.x 版本分支。在 Ubuntu 的情况下，安装 HTTP 服务器的包称为 `apache2`，而包含 1.x 版本的包已不再可用。

Apache 有一份关于服务器 Web 站优秀指南。有关更多信息，请参阅 `http://http.apache.org/docs/2.4/misc/security_tips.html`。这些提示随每个新版本进行更新。

如果你发现了尚未报告的安全问题，Apache 安全团队鼓励通过私有邮件列表进行报告。有关程序的信息，请参阅 `http://www.apache.org/security/`

Apache 2.4 包含了多个增强功能，包括通过在线证书状态协议 (OCSP) 服务器检查数字证书当前状态。OCSP 允许 Apache 判断用户是否可靠。如果攻击者意味着，OCSP 访问可以保护用户。OCSP 允许实现软件检查证书是否已被撤销。证书可能由于多种原因被撤销。撤销的证书不应被信任。如果用户为了验证目的展示证书，不应被信任。

为了方便，Apache 未为 Red Hat 和 Ubuntu 系统提供二进制包（适用于 rpm 和 dpkg 命令的格式）。然而，此类包可能并非由发行版开发者开发。

## Samba 文件服务器

运行 Samba 文件服务器的管理员可以通过 `http://samba.org/samba/history/security.html` 保持同步。更新以补丁格式提供。要整合这些更新，你需要等待发行版开发者将补丁处理成他们自己的二进制文件。更新后，可以使用相应的包管理工具下载并升级新的 Samba 软件。

> 警告
不稳定版本可能会导致不可预测的结果。安全很重要，不稳定发行版的开发人员专注于为该软件添加功能和删除错误，这可能会推迟解决安全问题的更改。

# 第 3 部分构建分层 Linux 安全策略

Samba 网站上描述的补丁发布版本与发行版开发人员发布的版本有所不同。这些开发人员可能需要进行额外工作，以一种与发行版相关的其他包兼容的方式来整合新发布的补丁。

Samba 后后的开发人员以类似于 Linux 内核开发人员的方式维护着其文件服务器软件的多个版本。Linux 内核的开发人员可能会将这些补丁的代码整合到 Samba 的较早版本中。这种过程通常[频繁]被称为“回移植”（backport），即将软件新版本的功能或代码放置到旧版本中。

如果你认为在某个 Samba 版本中发现了重大的安全问题，开发者鼓励你向 `security@samba.org` 发送电子邮件报告。

## 文件传输协议服务器

绝大多数管理员在 Linux 上倾向于使用 Apache 作为 Web 服务器，并使用 Samba 提供微软风格的文件共享服务。相比之下，Linux 管理员在安装用于 FTP 文件的服务器时会有多种选择。虽然非常安全文件传输协议（vsftpd）是 Red Hat、SUSE 甚至 Linux 内核组织的默认选择，但还有其他选项，如下：

- **Pure File Transfer Protocol daemon (Pure-FTPD)**——Pure 文件传输协议守护进程（Pure-FTPD）是一个活跃支持的服务器，可以 100% 以非 root 账户运行。更多信息请参阅 `http://www.pureftpd.org/`。
- **Pro File Transfer Protocol daemon (ProFTPD)**——Pro 文件传输协议守护进程（ProFTPD）是一个活跃支持的服务器，在虚拟 FTP 服务器配置方面，其基础配置类似于 Apache Web 服务器。更多信息请参阅 `http://www.proftpd.org/`。
- **Washington University File Transfer Protocol daemon (WU-FTPD)**——华盛顿大学文件传输守护进程（WU-FTPD）在 2000 年初非常常用。尽管它不再被维护，但仍然可以在 Ubuntu Universe 仓库获取。

> 警告
仅仅因为可以从发行版相关的仓库下载并安装软件，并不意味着它是受支持或安全的。例如，截至本文编写时，WU-FTPD 服务未经过维护也不安全。尽管它自 2004 年以来未进行维护，但在某些主流 Linux 发行版的不受支持仓库中仍然可用。

## Linux 系统的杀病毒软件选项

广义地说，杀病毒系统包括可以检测所有类型恶意软件的系统。虽然并非所有恶意软件都会影响操作系统，但它们可以通过电子邮件传输并由常见格式的文件携带。本节介绍了一些 Linux 可用的恶意软件系统。

## 第 11 章 | 管理安全告警和更新

在任何计算机系统中，恶意软件分为以下几类：

- **Rootkit (根内核包)**——Rootkit 是一种可以帮助攻击者获取计算机系统管理权的恶意软件。
- **间谍软件 (Spyware)**——收集用户信息的恶意软件称为间谍软件。这可能包括击键记录。
- **木马 (Trojan horse)**——木马是一种隐藏了理想程序但便于未经授权访问的恶意软件。
- **病毒 (Virus)**——严格来说，病毒是一种可以自我复制并感染计算机的程序。广义地说，计算机病毒指的是所有恶意软件。
- **蠕虫 (Worms)**——可以自己发送到其他系统的自我复制恶意软件被称为蠕虫。蠕虫与病毒的区别在于，它不需要用户直接参与即可传播。

负责的 Linux 管理员会在系统中包含杀病毒软件。虽然针对 Linux 的病毒较少，但它们确实存在。与 Windows 操作系统相关的一个问题是使用管理员权限运行它的用户很多。虽然 Linux 配置为不鼓励使用管理员权限运行命令，但可以将 Linux 配置为仅使用 root 账户。因此，Linux 并不是不可免疫的。Linux 对攻击者来说可能是一个更困难的目标；然而，某些 Linux 应用（如 Apache Web 服务器）拥有主导的市场份额。

尽管攻击者为 Linux 系统[找到]的恶意软件组件较少，但 Linux 仍可能被感染甚至作为载体。换句话说，如电子邮件服务器、FTP 服务器、文件服务器等 Linux 服务可以携带恶意软件，这些软件在暴露于微软或苹果操作系统之前一直保持休眠。正如所述，也存在感染 Linux 系统的恶意软件。

对于 Linux 系统最常见的恶意软件可能是基于 rootkit 的：替换系统级二进制文件以隐藏恶意软件的存在的软件。Rootkit 还可能在系统中安装后门，以便攻击者即使在原始入口点被修复的情况下也能保持访问权限。事实上，某些攻击者会修复允许他们进入系统的漏洞，以防止其他攻击者尾随其后。Rootkit 使他们即使在原始漏洞不再有效后也能保持访问权限。

> 注意
本节描述的某些杀病毒工具是根据通用公共许可证（GPL）发布的。

## ClamAntivirus 系统

ClamAntivirus (ClamAV) 系统是一种用于 Linux 的杀病毒软件。尽管你可以用它执行常规文件扫描，它最初设计用于邮件网关——带有如 sendmail、Postfix 和 Exim 等服务器。它运行在 Unix 类型操作系统上，包括 Solaris、伯克利标准发行版 (BSD)-(Solaris 是由 Sun 公司最初开发的 Unix 变体；BSD 是 Unix 的克隆，类似于 Linux）。ClamAV 支持对存档、压缩文件的搜索。它定期更新。如果你使用 ClamAV，订阅 `http://lists.clamav.net/` 相关的邮件列表可能对你有利。

## AVG Antivirus

尽管 AVG Technologies 专注于微软杀病毒市场，但也为 Linux 制作反恶意软件工具。成本和支持程度各异。这些工具包括：

- **Linux 版 AVG Antivirus**——AVG 了一针对 Linux 用户的免费下载杀病毒工具。该软件有多种格式，包括基于 Red Hat 和 Ubuntu (Debian) 包系统的。正如 AVG 所述，此软件供个人非商业用途使用。尽管 AVG 为该软件维护了论坛，但这些论坛上的信息很少与 Linux 相关。
- **Linux 版 AVG Antivirus Server Edition**——AVG 还制作了商业杀病毒工具。该版本包含了杀病毒、反间谍软件和反垃圾邮件工具。

## 卡巴斯基杀病毒替代方案

**Kaspersky Lab** 有一套适用于 Linux 的反恶意软件产品。这些是商业产品：Linux 系统的 Kaspersky Endpoint Security for Business Core。它提供单一管理控制台，用于控制组织内所有不同类型的终端。更多信息请参阅 `http://www.kaspersky.com`

## SpamAssassin

虽然有多种商业解决方案可以减少垃圾邮件，但 SpamAssassin 实际上是 Red Hat Enterprise Linux 7 (RHEL 7) 标准仓库的一部分。这意味着它受 Red Hat 支持。换句话说，如果你拥有相应的 Red Hat 网络订阅，Red Hat 工程师可能会支持你对 SpamAssassin 的使用。

有关 SpamAssassin 的更多信息，请参阅 `http://spamassassin.apache.org`

> 注意
SpamAssassin 的正式名称为 Apache SpamAssassin 项目。这是因为它的开发者由同一个 Apache 项目 Web 服务器赞助。

## 第 11 章 | 管理安全告警与更新

如果你想使用 Google 在邮件列表的公共存档中搜索，请使用 `site:tag` 标签。例如，在 Google 中进行以下搜索，可以在红帽企业 Linux 7 邮件列表中搜索所有单词“Samba”实例：

```
site:tag
```
