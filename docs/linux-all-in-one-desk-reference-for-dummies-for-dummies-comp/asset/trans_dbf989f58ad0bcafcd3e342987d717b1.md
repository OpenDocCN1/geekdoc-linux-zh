

- X 窗口系统：它是图形用户界面。
- 一个或多个图形桌面环境：其中最受欢迎的包括 GNOME 和 KDE。
- 一系列应用程序：Linux 程序以即插即用的软件形式提供，但源代码（即我们人类用来指示计算机执行操作的命令）是包含在内的（或易于获取的），其文档也同样如此。

当前的 Linux 发行版包含了海量的软件选择——多到一些发行版通常需要多张 CD-ROM 或一张 DVD-ROM（本书附带了一张 DVD-ROM）。

![](img/11709a8f88c8cd03868a929dc94c0e2b_36_0.png)

Linux 内核、Linux 发行版中的软件包以及 Linux 发行版本身的开发和维护都是作为开源项目组织的。简而言之，开源意味着有权访问源代码，并有权在任何限制下自由再分发软件。开源的定义远比我简洁的注记所涵盖的要复杂得多。若要了解开源的更多细节以及可接受的开源许可证，您可以访问位于 www.opensource.org 的开源促进组织（Open Source Initiative）网站。

表 1-1 列出了一些主要的 Linux 发行版，并对每个发行版进行了简要描述。除了我在表 1-1 中列出的这些发行版外，还有许多其他的 Linux 发行版。

![](img/11709a8f88c8cd03868a929dc94c0e2b_36_1.png)

若想了解更多关于 Linux 发行版的信息，请访问 Distrowatch.com，网址为 www.distrowatch.com。在该网站上，您可以阅读特定发行版的资料，并找到订购特定发行版 CD 或 DVD 的链接。

**表 1-1 主要 Linux 发行版**

| 发行版 | 描述 |
| :--- | :--- |
| Debian GNU/Linux | 这是一个非商业发行版，始于 1993 年，至今依然是一个广受欢迎的发行版，世界各地有许多志愿者开发者为该项目做出贡献。Debian 是一个庞大的发行版。仅二进制软件包就需要 14 张 CD 或 2 张 DVD。但是，如果您拥有互联网连接，可以使用单张 Debian 网络安装 CD 来安装基础系统，该 CD 可在 www.debian.org/CD/netinst 获取。安装好基础的 Debian 系统后，您可以使用名为 apt-get 的软件包安装工具轻松安装和升级 Debian 软件包，其中 apt 代表 Advanced Package Tool（高级软件包工具）。Debian 可免费下载，网址为 www.debian.org。Debian 是其他几个近期发行版的基础，包括 Knoppix、MEPIS、Ubuntu 和 Xandros。 |
| Fedora Core | 该发行版是 Red Hat Linux（即来自 Red Hat 公司的 Linux 发行版）的继任者。2003 年 11 月发布的 Fedora Core 1 是 Red Hat Linux 9 的继任者。Fedora Core 可免费获取。Fedora Core 使用 Red Hat 软件包管理器（RPM）格式来管理其软件包。您可以从 `http://fedora.redhat.com` 下载 Fedora Core。 |
| Gentoo Linux | 这是一个非商业的、基于源代码的（意味着所有软件均以源代码形式提供）发行版，首次出现在 2002 年。安装程序提供一些二进制软件包以启动 Linux，但其核心理念是在用户的计算机上编译所有源代码软件包。这使得构建一个包含最新图形桌面、多媒体和开发工具的完整 Gentoo 系统耗时较长，因为所有软件包都必须下载并编译。Gentoo Linux 可免费从 `www.gentoo.org` 获取。 |
| Knoppix | 这个 Live CD 发行版基于 Debian，以其开发者、德国人 Klaus Knopper 的名字命名。Knoppix 可以作为恢复工具使用（用于修复已安装的 Linux 系统中的问题），因为您可以直接从 CD 运行 Knoppix，而无需先将其安装到硬盘上。Knoppix CD 以压缩格式存储软件，Knoppix 会在运行时动态解压程序。采用这种方法，Knoppix 可以在一张 CD 上容纳多达 2 GB 的软件。Knoppix 使用 Debian 软件包管理。若想了解如何免费下载 Knoppix，请访问位于 `www.knopper.net/knoppix/index-en.html` 的 Knoppix 网站。 |
| Linspire | 这个商业发行版最初于 2002 年以 LindowsOS 的名称发布。Linspire 使用 Debian 软件包格式，并通过其所谓的 Click-N-Run 基于 Web 的界面提供付费软件下载。您可以通过 BitTorrent（一种点对点文件共享系统）下载名为 LindowsLive! 的 Live CD 版本。若想了解有关 Linspire 的更多信息，请访问 `www.linspire.com`。 |
| Mandriva Linux | 这个流行的发行版最初是 1998 年发布的 Red Hat Linux，带有易于使用的安装程序，并默认使用 KDE 桌面。直到最近，这个发行版还被称为 MandrakeLinux。Mandriva Linux 使用 Red Hat 软件包管理器（RPM）格式来管理其软件包。您可以在 `www.mandrivalinux.com` 获取 Mandriva Linux 下载版（一套 3 张 CD/DVD）。点击 Download（下载）链接以获取更多信息。 |
| MEPIS Linux | 这个基于 Debian 的 Live CD 发行版首次发布于 2003 年 7 月。它还包含一个图形化安装程序，可以从 Live CD 启动以将 MEPIS 安装到硬盘上。MEPIS 具有良好的硬件检测功能，并附带 Java 和多媒体软件，这使其广受欢迎。MEPIS 使用 Debian 软件包格式。您可以从 `www.mepis.org` 免费 SimplyMEPIS Live CD。 |
| Slackware Linux | 这是最古老的发行版之一，最早发布于 1992 年。Slackware 使用压缩 tar 文件作为其软件包，并提供一个基于文本的安装程序，硬件自动检测功能有限。您需要通过编辑文本文件来完成所有软件配置。Slackware 可免费从 www.slackware.com 获取。 |
| SUSE Linux | 这个商业发行版在 2005 年 8 月转变为一个名为 openSUSE 的社区开发项目。SUSE Linux 开源软件（OSS）现在可免费获取，零售版的 SUSE Linux 基于开源版本。SUSE 附带 YaST 安装和配置工具。SUSE Linux 使用 RPM 软件包。openSUSE 项目提供来自各种镜像站的 SUSE Linux OSS 的 ISO 映像文件（参见 www.opensuse.org/Download）。请访问 www.opensuse.org 了解更多关于 SUSE Linux 的信息。 |
| Ubuntu Linux | 这是一个相对较新的基于 Debian 的非商业 Linux 发行版，自 2004 年首次发布以来，在很短的时间内变得非常流行。Ubuntu 既有安装 CD 也有 Live CD 版本。由于它是基于 Debian 的，您可以从安装 CD 安装基本桌面系统，然后使用 apt-get 工具安装其他软件包，并以此保持系统更新。您可以从 www.ubuntu.com 免费下载 Ubuntu。 |
| Xandros Desktop OS | 该发行版是 Corel Linux 的继任者，并基于 Debian。Xandros 面向首次使用 Linux 的用户，其安装程序可以重新分区硬盘。功能强大的 Xandros 文件管理器是 Xandros 的一个主要卖点。然而，Xandros 包含一些专有组件，阻止了再分发。通过 BitTorrent 可以获得一个免费的 Xandros Desktop 受限版本，称为 Open Circulation Edition（开放流通版）。请访问 www.xandros.com 了解更多关于 Xandros 的信息。 |

正如您在表 1-1 的简要描述中看到的，一些 Linux 发行版，如 Knoppix 和 MEPIS，是以 Live CD 的形式存在的。Live CD（或 Live DVD）包含一个 Linux 内核，您可以直接从 CD 或 DVD 启动并运行，而无需先将其安装到硬盘上。如果您想在决定是否安装之前先试用某个发行版，这类 Live CD 发行版会非常方便。

本书附带的配套 DVD 可用作 Knoppix Live DVD。您只需从 DVD 启动 PC 并按 Enter 键即可运行 Knoppix。

许多 Linux 发行版，如 SUSE Linux 和 Xandros Desktop，都是商业产品，您可以在线或在计算机商店和书店购买。如果您听说过开源和 GNU（GNU's Not UNIX）许可证，您可能会认为没有人可以为了利润而销售 Linux。对于销售 Linux 发行版的公司来说，幸运的是，GNU 许可证——也被称为

