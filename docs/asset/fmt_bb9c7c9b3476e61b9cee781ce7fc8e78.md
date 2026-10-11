
## 总结

Debian GNU/Linux 的可靠性，结合其大量的高质量软件包，使得 Debian 成为工作站和服务器的极佳选择。精心执行的发布以及无需重启即可升级大多数软件的能力，进一步增强了其作为服务器操作系统的适用性。

`APT` 是安装、删除和升级软件包的主要工具。本章探索了如何使用 `aptitude`、`apt-get` 和 `apt-cache` 实用进行包管理。本章还涵盖了使用 `tasksel` 工具安装包集（任务），以及使用 `dpkg-reconfigure` 工具管理包配置。

## 第 20 章

## 运行 SUSE 和 openSUSE Linux

在过去的几年里，SUSE Linux 发行版一直是欧洲最流行的 Linux 发行版。自从美国网络公司 Novell 于 2003 年 11 月收购 SUSE 后，SUSE Enterprise (SLE) 产品定位为挑战 Red Hat，成为全球大型企业计算环境的主导性 Linux 发行版。

与 Fedora 和 Red Hat Enterprise 一样，openSUSE 和 SUSE Enterprise 对于寻求 Linux 系统职业的人来说是非常极的选择。由于 Novell 的 Linux 产品线面向企业计算，因此你在家中的 Linux 系统上使用 SUSE 所获得的技能在商业环境中同样有用。

SUSE 系统拥有精良的图形化安装程序，可以引导用户完成安装，并提供直观的管理工具，这些工具整合在一个名为 Yaast 的设施下。SUSE 及其母公司 Novell 提供了一系列 Linux 产品和支持计划，范围从具有社区支持的免费 openSUSE 版本，到支持企业桌面的 SUSE 发行版（SUSE Linux Enterprise Desktop，或 SLED），一直到 SUSE 的 Linux Enterprise Server (SLES) 产品。

2005 年，Novell 放弃了像 Red Hat 对 Red Hat Enterprise Linux 产品和 Fedora 项目那样的开发模式：Novell 开放了 openSUSE 项目，该项目与 Fedora 项目一样，产生一个免费的社区驱动的 Linux 系统，并为 Novell 的营性 Linux 系统提供支持。Novell 提供的 openSUSE 盒装仅提供 90 天的安装支持，而对于 SUSE Linux Enterprise 则提供多种支持选项。更多差异请访问 www.novell.com/products/opensuse/comparative.html 查看比较特性页面。

### 本章内容

- 了解 SUSE
- 获取 SUSE 支持
- 安装 openSUSE

## 选择和安装不同的 Linux 发行版

随书附的 DVD 包含了 openSUSE 11 kde 现场/安装 CD。

本章描述了让 SUSE Linux Enterprise 区别于其他 Linux 发行行的特性和方法。它还解释了如何安装随书提供的 openSUSE Linux 11 发行版。

openSUSE 的当前版本（发布 11）具有 YaAST 安装程序，以及当前的 KDE 4 桌面环境、GNOME 2.2、Firefox 3.0、GIMP 2.4、Apache 2.2.8、MySQL 5.0.51a 和 OpenOffice 2.4.0。要查看 openSUSE 的所有软件包，请访问一个 open-SUSE 镜像站点（http://en.opensuse.org/Mirrors_Released_Version）。

## 与敌共存：SUSE/微软交易

2006 年 11 月，Novell 宣布其已与微软达成协议，以便进一步与微软产品进行合作并实现互操作性。该协议包括针对专利相关诉讼的赔偿，在开源社区引起了相当大的关注和争议。事实上，Novell 并没有承认也没有看到任何 Linux 中使用微软知识产权 (IP) 的证据，但自从 SCO 对 Linux 发起一系列可疑的知识产权诉讼以来，专利责任免责已成为 Linux 领域的重要部分。Red Hat 和 Oracle 已经提供了此类问题的赔偿，因此这是一种更广泛的保护。

抛开疑虑不谈，这笔交易非常重要，至少它是微软 的一个声明，表明 Linux 对其客户是免责保护的，并且是一个可行的企业操作系统。一如既往，这项交易的长期影响仍有待观察，但对所有人来说都是件好事。许多成员担心微软将将其知识产权悄悄引入 GNU/Linux 代码库，为未来针对非合作伙伴的诉讼铺平道路。与 Xandros（一家领先的商业 Linux 桌面生产商）的协议也被视为重大威胁。（请查看第 25 章关于 Xandros 及其近期收购另一个领先 Linux 商业桌面生产商 Linspire 的描述）。

## 了解 SUSE Linux Enterprise 和 openSUSE

如果你正在寻找一个可以信赖其业务稳定性和支持的 Linux 系统，一家公司（Novell），

## 运行 SUSE 和 openSUSE

SUSE（原名 S.）始于 1992 年，是一个基于德国的 Linux 发行版。在 90 年代初，它还没有以开源形式提供。然而，为了在主要计算客户中获得更广泛的作为管理一系列服务的认可，Novell 于 2004 年 3 月根据 GPL 协议发布了 YaST。

## 运行 SUSE 和 openSUSE Linux

启动 YaST 实用实际上涉及到运行 `/sbin/yast2` 命令。当你运行 `/sbin/yast2` 时，YaST 默认以图形模式启动。（另一种替代方法是在终端窗口中以 root 用户身份运行 `/sbin/yast`，这将以文本模式启动 YaST。）图 20-2 显示了在终端窗口中以文本模式启动时 YaST 的外观。

## 图 20-2

使用方向键和 `Tab` 键在文本模式下于 YaST 中进行导航。

![](img/7021538f323e6521c571e727b770a451_606_0.png)

YaST 为你提供了一些直观的工具来配置系统，并进行了预先配置，因此你可以从一组非常好的默认设置开始。YaST 在检测你的硬件、查找分区等方面也做得很好，因此新用户可以直接接受 YaST 选择的设置。以下是 YaST 执行某些操作的示例：

- *检测硬件* —— 你无需检查 `/etc` 配置文件，或运行 `lsmod`、`lspci` 或 `hwinfo` 来查看硬件驱动程序或硬件在 SUSE 中的配置情况。从“硬件”部分，你可以选择代表显卡、打印机、热点、扫描仪、声卡和鼠标的图标。点击“硬件信息”图标可以查看检测到的完整硬件列表。

- *管理系统配置* —— 像 Red Hat Enterprise Linux 一样，SUSE 在 `/etc/sysconfig` 目录下存储了许多启动时配置服务的信息。这些文件中的信息以 `VARIABLE=""` 的形式存在。

在 YaST 系统标题（位于左侧面板中）下，你可以选择 `sysconfig` 编辑器，它可以让你选择每个文件并可能更改每个变量，这样你就不必猜测每个配置可用哪些变量。对于更高级的系统管理员来说，这是精调系统启动服务的一种极佳方法。

## 选择和安装不同的 Linux 发行版

SUSE 还包含一个系统配置描述管理 (SCPM) 小工具，它可以让你存储和管理一组系统设置，以便以后再次使用。

- 配置网络设备 —— YaST 检测你的拨号调制解调器、以太网卡、DSL 调制解调器或 ISDN 硬件，并让你有机会配置每件硬件。SUSE 在让 Windows 在 Linux 上运行方面比大多数发行版都做得好得多，这对于带有廉价内置调制调器的笔记本电脑拨号功能特别有用。
- 定义网络服务 —— 在连接到局域网或广域网后，YaST 提供了一些实用的图形工具，用于配置某些从命令行配置可能不那么直观的服务。
- 更改安全设置 —— Linux 中的安全设置通常是最直观的，同时也是最重要的。尽管像 `iptables` 等功能对于大多数 Linux 专家设置防火墙来说效果非常好，但习惯于图形界面的人可能会发现它们具有挑战性。

从 YaST “安全和用户”选择中，“防火墙”图标允许你逐步处理网络接口，并通过端口号（如 Web 服务器、邮件服务器和其他服务）添加对这些服务的访问。它甚至允许你对更复杂的防火墙功能进行初始设置，例如数据包转发、IP 伪装（IP Masquerading）和日志记录。

为了图形 YaST 界面操作，你只需点击鼠标并使用 `Tab` 键在字段之间移动。对于文本的 YaST 界面，你可以使用 `Tab` 键和方向键在选项之间移动，并使用 `Enter` 键选择当前高亮的项。

## RPM 包管理

像 Red Hat Enterprise Linux 和 Fedora 一样，SUSE 使用 RPM 管理文件和相关工具对其软件打包。RPM 包含了许多在 SUSE 中添加、删除和管理软件的功能。虽然 Red Hat 和 SUSE 发行版中的软件包不同，但你在那两个发行版中使用命令行管理软件包的工具是非常相同的。

你使用 `rpm` 工具来管理软件包。以下是 `rpm` 工具的一些功能：

- 安装本地或远程软件包 —— 你可以使用 `rpm` 命令从本地目录、CD 或远程计算机安装软件包（只要你有网络访问）。SUSE 软件包位于 Web 服务器（http://）或 FTP 服务器（ftp://）。以下是使用 `rpm` 从 FTP 服务器安装软件包的示例：

```
```
