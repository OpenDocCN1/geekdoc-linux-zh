
简单，但对我们能做的事情是一个很好的说明。

# 第七部分

# 附录

本部分包含

- 附录 A Novell SUSE Linux 的版本 587
- 附录 B SUSE 和 Linux 上的网络资源 591

## 附录 A Novell SUSE Linux 的版本

恭喜你！通过阅读这本书，你已经成功地探索了 SUSE Linux 系统并对其有了初步的了解。也许你现在正在寻找关于你当前使用的版本或其他可能符合你需求的其他版本的更多信息，例如 SUSE Linux 操作系统的服务器版本——被称为 SUSE 企业版服务器（或 SLES）；它更偏向于服务器类，更符合服务器操作系统的需求。书中介绍的 SUSE 版本是基于 SUSE Linux 10 的，这被认为是一个桌面级操作系统。在本附录中，我们将查看 SUSE Linux 的当前版本第 10 版，以及相关的 SUSE 和 Novell 产品家族。

> 要了解有关 Novell 对 Linux 的总体支持和开发，请访问以下 URL。Novell/Linux 网站充满了大量的文档和信息，你可以利用这些信息根据你的个人以及可能存在的业务需求，对部署哪个版本的 Linux 做出明智决策。

`http://www.novell.com/linux/index.html`

- `SUSE Linux 10`
- `SUSE Linux Enterprise Server (SLES)`
- `Novell Linux Desktop (NLD)`
- `Open Enterprise Server (OES)`

### SUSE Linux 10

`SUSE Linux` 目前处于 10.0 版本，是一个先进的桌面操作系统，它能为你提供生产力工具、互联网连接以及更多功能。`SUSE` 一直以来以在各大“主流”发行版中拥有最大的发行量而闻名。数百个开源应用程序被包含在 `SUSE Linux` 中——多到需要 5 张 CD-ROM（或 2 张 DVD）才能装下它们。其中一半包含了应用程序的源代码，但可用程序仍然比你可能用到的要多。某些可用工具是用于系统的深度开发。如果你的个人需求发生变化，需要某些其他软件来完成任务（例如，你在书中学到的众多工具之一），你完全不需要翻阅清单就能获得所需的功能。你只需要启动 `YaAST` 并搜索合适的工具，几分钟后就能准备就绪。

> 你可以查看 `SUSE Linux` 已安装程序的在线列表。你也可以查看随 `SUSE Linux` 附带的每个包并查看详情。

`http://www.novell.com/products/linuxpackages/professional/index.html`

产品种类不断扩大，包含了更多办公生产力和协作工具，以及编程、开发和网络工具；列表层出不穷。

> `SUSE Linux` 还附带两个完整的办公套件（`OpenOffice` 和 `KOffice`）、一个微套件（`GNOMEOffice`、`AbiWord` 文字处理器、`gnome-db` 数据库和 `Gnumeric` 表格）、两个工业级开源关系型数据库管理系统（`PostgreSQL` 和 `MySQL`）、两个财务程序（`GNuCash` 和 `KMyMoney`）以及个人信息管理器（`Ximian Evolution` 和 `Contact`），以及你提高效率所需的一切。

你也可以将 `SUSE` 称为从事 Linux、Unix、C++、LAMP 等工作的程序员的非常坚固的开发工具。所有水平和经验的程序员都能在 `SUSE Linux` 中找到其工艺所需的全部工具。这里有编辑器，包括德老的 `GNU Emacs` 以及许多其他近期版本；`GNU C` 编译器 (`gcc`)，以及用于 `Perl`、`Python`、`Ruby`、`PHP`、`Java` 以及你所想到的任何其他语言的编译器；以及 `KDevelop` 和 `Eclipse` 这两个集成开发环境 (`IDE`)。你还可以使用并发版本系统 (`CSV`) 或 `Subversion` 来管理你的大型项目。

除了所有这些应用程序以及所有常规命令、字体和桌面系统所需的各种视觉元素外，`SUSE` 还附带了扩展的打印文档。《管理指南》（`Administration Guide`）涵盖了具有 root 权限的用户的安装和其他管理任务。《用户指南》（`User Guide`）是一本关于配置和使用桌面环境、办公应用、电子邮件和其他工具的友好手册。你也可以通过 `SUSE` 帮助中心阅读这些书籍的完整内容。

`SUSE Linux` 每更新两次点版本（point releases），但由于应用程序不断进行漏洞修复、安全修复和功能增强，你可以保持在技术前沿。许多开发者使用红帽软件包管理系统 (`RPM`) 来为他们的应用程序打包。`SUSE` 一直使用这种方法来构建其发行版，并编写了许多 `SUSE` 特定的 `RPM` 包。你可以使用 `YaST` 在线更新 (`YOU`) 或为 Debian 系统创建并适配 `RPM` 的高级软件包工具 (`APT`)，因为 `RPM` 绝对是最常用的包格式。无论你选择哪一个，你都可以使用 `SUSE Linux` 打包你的应用程序。

### 10.0 版本

在本书编写期间，`SUSE Linux` 处于 10.0 版本。根据作者对它的经验，很明显 10.0 版本是一个稳健、可靠且安全的桌面操作系统。当前版本易于安装、易于配置且非常稳定。

由于 `SUSE Linux` 主要是一个桌面操作系统，你可以预期它在浏览网页、发送电子邮件、通过即时通讯程序与朋友聊天、设计并发布网页、整理数字照片、播放电影以及创建文档、网页和表格时运行得稳固。你甚至可以用它来托管博客或开发自己的应用程序。

虽然它并非用于业务部署，但 `SUSE Linux 10` 为企业评估人员提供了诸如 `XEN`（虚拟化）、`OpenOffice 2.0`（办公套件）、`Beagle`（桌面搜索）和 `Mono`（开源开发环境）等技术的卓越视角。这些技术在完善并获得支持后，可能会出现在未来的 Novell 产品中。

> 注意：尽管尚未定稿，但预计 `SUSE 10.0` 将提供下载版和盒装版。

### SUSE Enterprise Server (SLES)

`SUSE` 企业版服务器 (`SLES`) 9 是一种企业级操作系统，允许你将“服务器”组件应用于你的 `SUSE Linux` 知识中。正如书中所述，`SUSE Linux` 主要用于桌面操作系统。如果你需要更高级的组件和服务（例如集群化 `SUSE Linux` 知识的能力），`SLES` 提供了必要的工具。通过 Novell `OES`，用户将获得与 `SUSE Linux` 类似的许多功能，如前所述，Novell OS 是专为服务器服务构建的。

### Novell Linux Desktop (NLD)

`Novell Linux Desktop (NLD)` 是一种用于企业环境的桌面系统。它基于 `SUSE Linux` 构建，包含了那里的所有功能——包括 `YaAST`、`YOU` 和 `OpenOffice`。`NLD` 不通过零售渠道销售，而是面向 Novell 客户营销。在本书编写期间，`NLD 9` 是该系统的最新版本，但 10.0 正在开发中。

# 附录 B

## SUSE 与 Linux 互联网资源

### 本附录内容

- Novell SUSE Linux 参考
- 邮件列表
- Unix 通用参考
- Linux 通用资源
- Linux 新闻参考
- Linux 搜索参考
- 通网页链接参考
- Novell 网络与安全参考
- LAMP 及其他编程参考
- 全球 Linux 新闻组（Newsgroups）

现在你已经非常熟悉了 `SUSE Linux` 的操作，你应该通过访问和研究许多免费的在线资源来进一步了解它。互联网是寻找 Unix 和 Linux 信息的资源，特别是如果你是初学者并需要快速找到信息时。

随着 Novell 收购 `SUSE`，一个全新的机遇世界已向你敞开。当你努力学习新的桌面环境、精通 shell，或只是想了解更多关于 Linux 的通用知识时，`SUSE Linux` 的发布为 Linux 桌面运动开辟了许多机会。`SUSE Linux` 不仅由一家在服务器平台方面拥有长期成功的公司开发，而且还得到了该公司的支持。Novell 花了大量时间来确保在线文档的开发，并让操作系统获得其所需的支持。除了从 Novell 获得的支持外，`SUSE` 在公共互联网上也得到了很好的支持，这就是本附录将涵盖的内容。

在第 1 章“欢迎来到 `SUSE Linux`”中，本书首先为你提供了在遇到问题时的搜索途径。例如，第 1 章涵盖了 Novell `SUSE` 在线帮助以及查找 Linux 用户组（LUGs）的地方。正如我们提到的，《Linux Gazette》杂志托管了“各地的 Linux 用户小组”（GLUE）网站，地址为 `http://glue.linuxgazette.com`。该网站按地理位置组织，你可以浏览列表并从主页进行搜索。每个小组都有电子邮件联系方式，许多小组还列出了 URL。

## 附录 B SUSE 与 Linux 互联网资源

本附录基于第一章内容，扩展了你可以在线搜索的信息列表，并将其保持在一个易于使用的参考资料中。这里提供的信息列表是进入无尽信息海洋的门户，只要你搜索得足够仔细，就能找到真实的信息。请注意，这些网站可能很有帮助，但验证你访问的每个网站的合法性取决于你。。像 `Novell.com` 这样的网站可能比由爱好者运行的网站更多（且可能更准确）的信息。如果你不确定，请务必仔细使用网络参考并验证你的信息来源。

当你进入互联网进行研究后，请确保在研究过程中尽可能地继续通过实践来学习 Unix 和 Linux。记住，练习越多，就越容易；当你熟悉了命令、如何导航系统以及各个物品存放在何处后，你对 Unix 的控制力就会增强。

注意互联网上的漏洞软件和受病毒感染的软件。Unix 和 Linux 有太多需要学习的内容，你实际上可以搜索几个月，并且每天都能发现新的信息源。确保不要下载病毒、木马或其他形式的恶意软件。保持你的防病毒软件（以及你可能运行的任何其他形式的反间谍软件）更新更新并打好补丁。你可能还需要注意（并警惕）“孤儿”（orphanware）。这是由某个实体创建的软件，该实体由于某种原因不再支持该产品并离开了，留下了你处于孤儿状态——无解决方案可寻。

在本附录中，你将找到一个用于学习本书涵盖主题的互联网资源列表，并扩展你可能在那里找到更多关于你使用的 Linux 版本的信息，或者任何通用的基于 Linux 的信息。

## Novell SUSE Linux 参考

在第 1 章中，我们涵盖了在哪里可以找到 `SUSE Linux` 特定帮助的基础知识。你可以使用 `SUSE Linux` 操作系统自带的文档源获取帮助，包括帮助中心（Help Center），它通过搜索你刚刚安装的 Linux 版本（如 9.3）自带的文档来为你查找信息。

由于发行版包含了文档以及超过 1000 多个程序的来源，即使是这种长度的书也无法涵盖你的 `SUSE Linux` 中所有内容的基础。有很多地方可以学习更多关于 Linux 的知识，并帮助你排除应用程序的故障。打印文档以及之前提到的 `SUSE` 帮助中心将将帮助你找到许多书中未被回答的通用问题的答案。你也可以尝试通过 `SUSE` 网站 `http://www.novell.com/linuxprofessional/support/` 使用 `SUSE` 在线支持。这项支持是获取帮助的极佳资源。第一组是付费的，第二组是自学（DIY）在线支持。

当你尝试为问题寻找解决方案时，请点击 `sdb/en/index.html` 中的 Support Database（支持数据库），或直接访问 `http://portal.suse.com/` 中的支持数据库。

## Linux 通用资源

该数据库可以通过关键词或全文进行搜索。除了德语和英语外，该数据库还存在法语、西班牙语、捷克语和匈牙利语（Magyar）。主支持页面上的在线支持菜单链接到了一些有趣的 HOWTO 文档，向你一步步演示如何处理大小问题，从划分硬盘分区到配置 HTML 编辑器再到加密电子邮件。

在 `http://www.opensuse.org` 你将找到许多与 `SUSE` 和开源运动相关的信息。你不仅能找到文档和其他链接，这里也是发布测试版和开发发布的地方。你可以报告漏洞、以开发人员身份参与以及进行更多操作。

`man pages`（帮助手册）也是你需要时获取帮助的好方法。如果你正在运行 `SUSE Linux` 并需要帮助，请尝试 `man pages`。`man pages` 是压缩的文本文件，位于 `/usr/share/doc`。它们通常由程序员编写，并概述了每个选项的功能。

## 邮件列表

你可以使用通用 Linux 或 `SUSE` 特定的邮件列表获取更多帮助。

- `http://lists.suse.com/`
- `http://www.suse.com/en/support/mailinglists/`

## Unix 通用参考

以下链接是特定的 Unix，或者让你找到基于 Unix 的通用信息。

- `http://www.ugu.com/`
- `http://www.unix.org/`
- `http://www.sco.com/`
- `http://www.unixreview.com/`
- `http://www.freebsd.org/`

## Linux 通用资源

要获取大量的免费 Linux（SUSE 等）白皮书和其他帮助，请访问 rsnetworks.net。

- `http://www.rsnetworks.net/masterunix/`

Linux 文项目（Linux Documentation Project）是获取 HOWTO 指南和其他各种 Linux 主题信息的良好来源。

- `http://www.tldp.org/`

Linux 笔记本（Linux on Laptops）提供了在特定品牌和型号的笔记本上安装 Linux 的信息。

- `http://www.linux-laptop.net/`

寻找你附近的 LUG（Linux 用户组）。Linux 小组经常举办“安装会议”。你带上你的电脑，他们会帮助你在电脑上安装 Linux。此外，LUG 的会议上会有有趣的演讲者。

GNU 项目和自由软件基金包含了 Linux 发行版中使用的许多工具的源代码和文档。

- `http://www.gnu.org/`

## Linux 新闻参考

- `slashdot.org`
- `http://www.linuxgazette.com/`
- `http://www.linuxworld.com`
- `http://www.linux.com/`
- `http://www.linuxjournal.com/`
- `http://www.linuxquestions.org/`

## Linux 搜索参考

- `http://www.novell.com/linux/`
- `http://www.google.com/linux`
- `http://portal.suse.com/sdb/en/index.html`

使用上述在线搜索引擎（或你的其他特定于或非特定的搜索引擎）并搜索关键词。

关键词示例：`suse`, `linux`, `ftp`, `nfs`, `rpm`, `distribution`, `iso images`, `novell`, `unix`。`SUSE Linux` 包列表可以在 Novell 网站上找到。

- `http://www.novell.com/products/linuxpackages/professional/diff_cd_dvd.html`

## 通网页链接参考

在附录的下一个部分中，我们将按分类查看参考列表。如果你在编辑方面遇到问题并想了解更多关于 vi 编辑器的信息，请搜索附录中的编辑标题，例如。

## SUSE 与 Linux 及其资源

本书的每一章都包含一个参考部分，其中提供了与章节主题相关的更多或相关信息的链接。利用它建立一套书签，帮助你学习更多关于 Linux 的知识，特别是 `SUSE Linux`。

在本节中，参考资料分为三个大部分：系统管理，涵盖了 X Windows、办公应用程序等；网络安全参考，涵盖了 IP 划分、名称服务等教程和信息；以及编程和 LAMP 参考，如果你正准备在 Linux 上进行开发，这些资源将对你的开发工作大有帮助。

以下是在深入研究其他资源之前，可以先查看的几个通用网站。我们认为这些是你的最佳选择。

- * `http://www-1.ibm.com/linux/` —IBM 的 Linux 门户。与这个重要的 Linux 参与者相关的新闻、报告和白皮书。检查“Linux 发行版（Linux Distributors）”下的 `SUSE Linux` 链接，可获取与 IBM 支持 `SUSE Linux` 产品相关的材料。
- * `http://www.suse.com/` —`SUSE Linux` 的英文主页。新闻、下载、支持。
- * `http://www.suse.com/us/private/support` —搜索支持数据库、阅读 HOWTOs、订阅邮件列表。
- * `http://portal.suse.com/sdb/en` —指向 `SUSE` 支持数据库的直接链接。

## 安装、磁盘工具和通用系统管理

这组链接指向关于 Linux 安装、引导、分区以及安装和系统管理工具的有用资源。

- * `http://irc.freedesode.net` —获取 `SUSE`、`Linux` 或任何相关信息的绝佳起点。
- * `http://linux.dell.com` —Dell 社区主页。Dell 专注于企业级 Linux，并将向你销售 `SUSE Enterprise Server` 或 `Red Hat Enterprise Server`，但社区也提供了邮件列表来支持桌面和笔记本电脑上的 Linux 用户。
- * `http://linuxshop.ru/linuxbegin/win-lin-soft-en/table` —寻找 Windows 应用程序的 Linux 等品。
- * `http://cdb.suse.de` —`SUSE` 硬件兼容性数据库。
- * `http://www.linuxprinting.org` —想看看你的打印机在 Linux 下是否工作吗？去这里就对了。
- * `http://www.linux-usb.org` —Linux-USB 项目，包含支持设备和驱动程序的信息。
- * `http://www.qbik.ch/devices` —Linux USB 设备数据库；搜索兼容设备。
- * `http://www.linmodems.org` —基于软件介质的 Linux 驱动程序。
- * `http://www.linuxcertified.com` 和 `http://emperorolux.com` —提供提供预装 Linux 笔记本电脑的公司。
- * `http://linux-laptop.net` —关于 Linux 友好笔记本电脑的更多信息。
- * `http://www.linux1394.org` —Linux 火线（FireWire）项目，包含此类设备驱动程序的信息。
- * `http://elks.sourceforge.net` —嵌入式 Linux 内子集（ELKS），一种尝试构建可以在 Intel 286 及更早处理器上运行 Linux 的尝试。
- * `http://www.lnx-bbc.org` —Linuxable 商务卡项目主页，制作标准名片形状的“LIVE CD”。
- * `http://www.gnu.org/software/parted/parted.html` —GNU Parted 主页，免费的磁盘分区工具。
- * `http://tldp.org/HOWTO/Installation-HOWTO/index.html` —这篇 Linux 安装 HOWTO 写于 2000 年，由程序员 Eric S. Raymond 编写。
- * `http://www.gnu.org/software/grub` —GRUB 引导加载器主页。
- * `http://www.pathname.com/fhs` —关于新的 Linux 文件系统层次级标准，这里提供的信息可能比你想了解的得多。
- * `http://standards.ieee.org/regauth/posix` —IEEE POSIX 信息页面。
- * `http://cnssw.cns.cwru.edu/~bash/basht.html` —Ramey 的 Bash 页面。他是目前 bash 项目的维护者。
- * `http://www.tldp.org/LDP/Bash-Beginners-Guide/html/` —网页版的《Bash 初学者指南》。如果你访问该网站，可以获取其他格式的内容，以及其他优秀的 Linux 资源。
- * `http://www.tcsh.org/Welcome` —tcsh Wiki。学习更多并贡献你关于这种 C Shell 的知识。
- * `http://www.zsh.org/` —Z Shell 主页。选择一个最近的镜像站点。
- * `http://www-106.ibm.com/developerworks/linux/library/l-z.html` —来自 IBM 的关于 Z Shell 的良好介绍。
- * `http://www.ibilio.org/` —Midnight Commander（午夜命令）主页。截图、常见问题（FAQs）以及开发者的待办事项。
- * `http://www.dotfiles.com` —探索各种 shell、编辑器和其他工具的贡献配置文件。
- * `http://www.shellordado.com/` —Heiner Shellordado。包含关于所有 shell 的大量脚本信息以及一个良好的介绍。
- * `http://www.gnu.org/software/emacs/emacs.html` —GNU/Emacs 主页。

# 通用网络链接参考 599

- `http://www.gnome.org/gnome-office` —GO 套件的伞中心。
- `http://www.abisource.com` —AbiWord 页面。
- `http://www.gnumeric.org` —Gnumeric 页面。
- `http://www.softmaker.de/index_en.htm` —Softmaker Office。
- `http://en.hancom.com/products/hancomoffice20.html` —韩字 Office（Hancom Office）。
- `http://kymonery2.sourceforge.net/index.html` —Kymonery2。
- `http://www.gnucash.org` —GnuCash。
- `http://www.scribus.net` —Scribus 桌面出版工具主页。务必查看 docs.scribus.net 上详细且非常有用的教程。
- `http://www.gnome.org/projects/dia/` —**Dia 绘图工具**。软件包中未包含实用的文档。
- `http://www.insimilil.de/vym/` —**View Your mind 页面。使用 VYM 编写并导出为 HTML。看看程序是如何运行的非常有意思。
- `http://www.alsa-project.org/alsa-doc/` —**高级 Linux 声音架构（ALSA）卡矩阵**。在此查看更多关于你的显卡支持的信息。
- `http://www.linux-sound.org` —从用 Linux 制作音乐到音乐人邮件列表，再到播放器和制作软件，Linux 下音频和音乐的跳点。
- `http://www.xmms.org/` —**X 多媒体系统（XMMS）主页**。为这个多功能播放器提供新闻、下载、插件、皮肤和支持。
- `http://www.vorbis.com` —以及我们如何将其用于 Ogg Vorbis 音频格式。
- `http://www.exploits.org/v4l/` —****Linux 相关信息页面**。关于 V4L API 的技术信息、支持的显卡驱动程序以及个人视频录像机。指向制作各种类型视频的软件链接。在手动输入此 URL 时，请注意最后一个字符是 L（如 Video4Linux 所示），而不是数字 1。如果你输入了参数，会收到一个相当迅速的错误信息。
- `http://www.mythtv.org` —MythTV 个人视频录像机软件。安装说明，MythTV 的运行示例。
- `http://www.anandtech.com/linux/showdoc.aspx?i=2190&p=1` —关于在 `SUSE Linux` 上成功安装 MythTV 的详细且诚实的解释。
- `http://www.mplayerhq.hu` —MPlayer 总部，提供那个功能多样且功能 de视频播放器。
- `http://www.xinehq.de` —Xine 总部；该视频播放器的新闻和下载。
- `http://www.gphoto.org/` —****数码相机图像的 Linux 管理软件**。

# 附录 B

## SUSE 和 Linux 互联网资源

- `http://www.gphoto.org/proj/libgphoto2/support.php` —gphoto 支持的相机列表。
- `http://www.teaser.fr/-hfiguiere/linux/digicam.html` —Unix、Linux 和 BSD 的数码相机支持。如果你的相机不在 gphoto 列表中，该网站可能帮助你找出原因并提供建议。
- `http://www.digikam.sourceforge.net` —用于 gphoto 的 KDE DigiKam 前端。在此查看插件和新版本，它们似乎每两个月发布一次。
- `http://www.gimp.org` —GNU 图像处理程序（GIMP）组织极其良好的主页。查看“教程”部分，包含从初学者到专家的所有水平的步进指南。
- `http://gug.sunsite.dk` —全球 GIMP 用户组。包含邮件列表、大量的图像和纹理库、教程以及文章，帮助你成为一名更出色的 GIMP 使用者。
- `http://iculus.org/1fqag` —Linux 游戏玩家常见问题解答（FAQ）；在此获得问题的答案。
- `http://www.happyppenguin.org` —Linux 游戏大全，各种 Linux 游戏的目录。包含玩家评分、新闻和论坛。
- `http://www.linuxgames.com` —Linux 游戏，包含与该主题相关的各种新闻。
- `http://www.kde.org/kegames` —KDE 游戏区域，包含 KDE 自带的所有游戏的描述。
- `http://www.gggamingzone.org` —免费在线玩 Linux 游戏。
- `http://www.freeciv.org` —Freeciv wiki。所有 Freeciv 内容均提供七种语言翻译。
- `http://www.winehq.org` —Wine 项目总部。在“应用程序数据库”部分，务必为你喜欢的 Windows 投票，以便使用 Wine 进行移植。
- `http://www.von-thadden.de/Joachim/WineTools` —WineTools 提供了相对不痛苦的 Wine 安装方法以及一系列著名的免费应用程序，包括远程浏览器（Internet Explorer）。
- `http://www.codewavers.com` —Codewavers 公司，Crossover Over 的制作者。
- `http://frankscscorner.org` —该网站帮助你最充分利用 Wine。包含 FAQ 和 HOWTO 指南，引导你解决大部分问题。
- `http://www.vmware.com` —VMWare 公司，你可以在这里获取信息以及该虚拟机的免费 30 天试用版。
- `http://www.win4lin.com` —Win4Lin，帮助人们运行 Windows 98，现在是 Windows 2000/XP。
- `http://www.dosbox.sourceforge.net` —DOSBox 网站。检查对你游戏的支持，甚至可以找到古老游戏。

## 通用网络链接

- `http://dose..org` —dosemu 的主页。
- `http://freedos.org` —FreeDOS 模拟器。
- `http://www.ac../basilisk.ac.com/tu/basilisk` —在 Linux 上安装和运行 Basilisk 的教程。
- `http://www.gnome.org/projects/evolution` —关于文件系统的维基（此处原文疑为分类误）。
- `http://en.wikipedia.org/Filesystem` —关于文件系统的维基。
- `http://en.wikipedia.org/Comparison_of_systems` —文件系统的对比。
- `http://www.linux-project.org/faq` —ReiserFS 的常见问题解答。
- `http://sources.redhat.com/projects/ext3` —关于 ext3 的信息。
- `http://www.sap.com/lvm` —逻辑卷管理器（LVM）。
- `http://www.linux.org/HOWTO` —关于 LVM 的 指南。
- `http://www.gnu.org/projects/parted` —GNU Parted。
- `http://www.nvu.com/vym` —nvu (View Your mind)。
- `http://www.quanta.sourceforge.org` —Quanta。
- `http://www.kde.org/kddev` —KDE 开发。
- `http://www.bluefish.org` —基于 GTK 的 Bluefish。
- `http://www.bluefish.net` —Bluefish 维基。
- `http://www.scribe.org` —Scribe，用于 HTML 和 XML 的编辑器。
- `http://www.ndeepak.info/stuff/FrontPage` —不是 FrontPage，而是博客工具。
- `http://www.blosom.com` —Blom，基于 CGI 的博客工具。
- `http://www.billstar.com/blogmax` —Emacs 的 Blogmax 插件。
- `http://www.wordpress.org` —WordPress 博客和内容管理工具。
- `http://www.blogger.com` —谷歌托管的博客。
- `http://www.sixapart.com` —Movable Type 和 Typepad 的背后公司。
- `http://www.livejournal.com` —LiveJournal 是创建个人博客和建立志同道合社区的地方。
- `http://www.gnome.org/projects/evolution` —Evolution 邮件。
- `http://www.mozilla.org/products/thunderbird` —Thunderbird 页面。指向 MozillaZone 知识库和帮助论坛。
- `http://pim.kde.org` —KDE 个人信息管理件：Contact、KMail、Organizer 以及所有辅助工具。
- `http://www.sylpheed.good-day.net` —Sylpheed，另一个基于 GTK 的邮件客户端。
- `http://www.mutt.org` —文本邮件客户端的聚集地。

`http://www.yenc.org/linux.htm` —用于 yEnc 编码格式的 Linux 阅读器写入器。

`http://email.about.com/cs/standards/a/base64_encoding.htm` —关于 base64 编码的优秀描述。

`http://www.postfix.org/start.html` —Postfix 首页。请务必点击“Web Sites”链接以查找附近的镜像站点。

`http://www.seaglass.com/postfix/faq.html` —Postfix 邮件列表常见问题解答（FAQ），由《Postfix: The Definitive Guide》作者 Kyle Dent 维护。

`http://www.sendmail.org` —Sendmail 首页。

`http://cat.org/~esr/fetchmail` —Fetchmail 首页。

`http://www.paulgraham.com/spam.html` —Paul Graham 的原始文章《垃圾邮件计划》，概述了贝叶斯过滤理论。

`http://spamassination.apache.org` —SpamAssassin 首页。查看 wiki 页面以获取可下载的规则集。

`http://www.bogofiller.org` —Eric Raymond 的 Bogofiller 项目。

`http://www.nidelven-it.no/articles/introduction_to_thunderbird_5` —使用 Mozilla Thunderbird 进行垃圾邮件过滤的良好介绍。

`http://www.iki.fi/era/procmail/mini-faq.html` —Procmail FAQ。用作者的话说：“作者想把这个叫作‘Mini-FAQ’，但它变得越来越大。计划将其重命名为‘Bronto-FAQ’。”

`http://pm-doc.sourceforge.net` —Procmail 文档项目。访问 PM-Tips 页面查看示例规则集和许多其他好主意。

`http://www.clamav.net` —开源 Clam 防病毒程序的首页。

`http://groups.google.com` —Google Groups。在 Web 上阅读 Usenet 并创建你自己的组。

`http://www.iscg.org/index.pl/?products/inn` —InterNet Usenet 节点和阅读器。

`http://slrn.sourceforge.net` —“s-lang read news，”slrn 新闻阅读器。

`http://knode.sourceforge.net` —Contact 和 KDE 中的 KNode 新闻阅读器。

`http://pan.rebelbase.com` —适用于 GNOME 的 Pan 新闻阅读器。

`http://i2.com/cgi/wikiWikiWikiWikiWeb` —Ward Cunningham 的原始协作站点。

`http://i2.com/cgi?ChoosingWiki` —在 Ward Cunningham 聚集的帮助下选择 Wiki 引擎。

`http://zwiki.org` —Zwiki，包含在 `SUSE Linux` 中的基于区域的邮件引擎。文档进行中。

## 附录 B SUSE 和 Linux 资源

- `http://twiki.org` —另一个流行的 wiki 引擎。
- `http://en.wikipedia.org` —维基百科首页，也许是 wiki 如何工作的最佳示例。
- `http://www.list.org` —Mailman 列表管理器首页。
- `http://www.greatcircle.com/majordomo` —Majordomo 列表管理器。
- `http://www.siliconex.org/MajorCool` —Majordomo 的 Web 界面。
- `http://www.irchelp.org` —获取 IRC（网络中聊天）帮助的地方。
- `http://www.irc.org/links-html` —IRC 频道、网络和机器人。可以在这里找到。
- `http://tldp.org/HOWTO/IRC` —Linux 迷你 HOWTO。
- `http://kopete.kde.org` —Kete，KDE 即时通讯工具和 IRC 客户端。
- `http://www.jabber.org/user/userguide` —Jabber 用户指南，用于学习这种开源 IM 协议。Jabber.org 还托管了一个公共 IM 节点供你连接。
- `http://gabber.sourceforge.net` —GNOME Jabber 客户端。
- `http://xchat.org` —Xchat 首页。
- `http://www.liq.org` —LICQ，所有 Linux 即时通讯工具之母。
- `http://gaim.sourceforge.net` —这个 IM 最初是 AOL 即时通讯 (AIM) 的克隆，现在也支持其他 IM 网络。
- `http://www.gnomemeeting.org` —GnomeMeeting 视频会议首页。
- `http://www.kernel.org` —Linux 内核存档。查找最新内核和更多信息的地方。
- `http://www.kernel.org/mirrors` —从你附近的服务器下载内核。
- `http://www.kernel.org/traffic.org` —Kernel Traffic 通讯杂志，内核邮件列表发生事件的每周总结。
- `http://www.gnu.org` —GNU 不是 Unix。许多内核相关项目的首页。在这里获取软件和文档，以及浓郁的免费软件哲学。
- `http://www.gnu.org/software/make/manual/manual.html` —make 手册。此工具远不止源码编译环境。
- `http://kniggit.net/wwool26.html` —《Linux 2.6 的精彩世界》，由 Joseph Pranevich 编写的关于最新版本内核的指南。
- `http://www.kernelnewbies.org` —面向想要尝试内核黑客的人。Kernel Newbies 是一个 IRC 聊天频道 #kernelnewbies 以及来自该站的 wiki。
- `http://tldp.org/LDP/lki` —Linux 内核 2.4 内部指南。深入了解内核是如何运作的。
- `http://tldp.org/HOWTO/HOWTO-INDEX/os` —操作系统的 HOWTO-INDEX。
- `http://www.iki.fi/era/procmail/mini-faq.html` —Procmail FAQ。用作者的话说：“作者想把这个叫作‘Mini-FAQ’，但它变得越来越大。计划将其重命名为‘Bronto-FAQ’。”
- `http://pm-doc.sourceforge.net` —Procmail 文档项目。访问 PM-Tips 页面查看示例规则集和许多其他好主意。
- `http://www.clamav.net` —开源 Clam 防病毒程序的首页。
- `http://groups.google.com` —Google Groups。在 Web 上阅读 Usenet 并创建你自己的组。
- `http://www.iscg.org/index.pl/?products/inn` —InterNet Usenet 节点和阅读器。
- `http://slrn.sourceforge.net` —“s-lang read news，”slrn 新闻阅读器。
- `http://knode.sourceforge.net` —Contact 和 KDE 中的 KNode 新闻阅读器。
- `http://pan.rebelbase.com` —适用于 GNOME 的 Pan 新闻阅读器。
- `http://i2.com/cgi/wikiWikiWikiWikiWeb` —Ward Cunningham 的原始协作站点。
- `http://i2.com/cgi?ChoosingWiki` —在 Ward Cunningham 聚集的帮助下选择 Wiki 引擎。
- `http://zwiki.org` —Zwiki，包含在 `SUSE Linux` 中的基于区域的邮件引擎。文档进行中。
- `http://tldp.org/LDP/lki` —Linux 内核 2.4 内部指南。深入了解内核是如何运作的。
- `http://tldp.org/HOWTO/HOWTO-INDEX/os` —操作系统的 HOWTO-INDEX。
- `http://www.troubleshooters.org/linux/grub/grub.htm` —“从零开始的 GRUB，”关于如何创建 GRUB 软盘并在禁用的机器上启动的精彩解释。
- `http://www.gnu.org/software/grub/manual` —GRUB 手册，提供多种格式。
- `http://tldp.org/HOWTO/LILO` —LILO 迷你 HOWTO。
- `http://tldp.org/LDP/lame/linux-admin-made-easy-easy` —Linux 管理简易。查看第 4.8 节关于使用 LILO 启动的内容。
- `http://www.linux.com/article.pl?id=04/05/17/1832239` —对 KsysGuard 的短评评。
- `http://docs.kde.org/en/3.3/kdebase/ksysguard` —KSysGuard 手册。
- `http://www.gkrell.net` —GKrellm 的首页。

## Linux 网络与安全参考

这组链接指向了关于 IP 地址、网络以及 Linux 安全性的有用资源。

- `http://arin.net` —美国互联网数字注册机构（American Registry for Internet Numbers），负责分配美国公共 IP 地址的机构。
- `http://www.ietf.org/rfc.html` —搜索或获取互联网工程任务请求（Internet Engineering Task Requests for Comment）列表。
- `http://www.tldp.org/HOWTO/Linux+IPv6-HOWTO` —Linux IPv6 指南。
- `http://www.ietf.org/rfc/rfc2460.txt` —IPv6 标准文档。
- `http://linuxreviews.org/ipv6` —关于“为什么你想要 IPv6”的有趣文章。
- `http://www.iana.org/assignments/port-numbers` —在互联网数字分配机构（Internet Numbers Authority）网站学习哪些端口分配给了应用程序。
- `http://directory.google.com/Top/Computers/Software/Internet/Servers/Address_Management/Dynamic_DNS_Services/` —查找动态 DNS（Dynamic DNS）提供商的地方。
- `http://www.isc.org/sw/dhcp` —`SUSE Linux` 默认 DHCP 包及可选客户端的维护者。你可以在 ISC 网站找到当前的 DHCP README。
- `http://dhcp-monger.est-unique.net/wakka.php?wiki=Welcome` —DHCP-Mongers 维。阅读页面、搜索列表、提交新信息。
- `http://nfs.sourceforge.net` —网络文件系统（Network File System）项目页面，包括常见问题解答（FAQ）列表。
- `http://www.samba.org` —Samba 主页。在文档部分查看 HOWTO 集合和 Samba 示例指南（Samba-By-Example Guide）。
- `http://www.wi-fizon.org` —在该网站可以找到你所在地的无线热点，该网站由 Wi-Fi 联盟赞助。
- `http://standards.ieee.org/getieee802` —获取任何 802.xx 网络规范的官方 IEEE 标准文档。涵盖从以太网（802.3）到 WiFi（802.11）及以上的内容。
- `http://portal.samba.org/sdb/en/2002/11/wavelen.html` —来自 `SUSE` 支持数据库的无线网络设置。
- `http://www.hpl.hp.com/personal/Jean_Tourliches/Linux/Wireless.html` —关于 Linux 网络教程的许多素材。
- `http://www.securityfocus.com/unix/` —这个全面的安全网站提供新闻、邮件列表，甚至一些防火墙规则集。

## 附录 B SUSE 和 Linux 互联网资源

- `http://www.linuxsecurity.com` —获取每周 Linux 警报和 Linux 安全周报，以跟踪最新信息和补丁。包含初学者的教程和针对安全专业人士的文章。
- `http://www.insecure.org` —nmap 安全扫描器的主页。
- `http://www.ethereal.com` —免费以太网协议分析器和数据包嗅器。
- `http://www.tldp.org/HOWTO/DNS-HOWTO.html#toc1` —Linux 文档项目（Linux Documentation Project）。这里也有关于如何使用 DNS 通用信息的深度指南。
- `http://www.isc.org/index.php/?sw/bind/` —互联网系统协会（ISC）是一家致力于支持全球连接自组织互联网基础设施的非营利公益机构。这里也有关于 DNS/BIND 通用信息的深度 DNS/BIND 实践指南。
- `http://www.arin.net` —美国互联网数字注册机构。一家非营利注册机构，负责北美、南美、南非、加勒比海以及所有其他由 Network Solutions, Inc. 集中管理的区域的互联网协议（IP）数字的管理和注册。
- `http://www.isc.org/bind.html` —Berkeley 互联网名称信息直。由加州大学伯克利分校开发的 BIND 软件实现了 DNS 服务器和解析器库，允许客户端存储和检索对象并在网络与其他资源共享这些信息。此链接涵盖了 BIND 的详细信息。
- `http://www.iana.org/` —互联网数字分配机构（IANA）。IANA 是一个政府资助机构，负责分配和发布国际域名和 IP 数字（或互联网地址），并监督官方许可根的互联网软件协议。
- `http://www.internic.net/` —以下顶级域名名称注册机构：COM, EDU, NET, GOV 和 OR 的注册机构。
- `http://linuxprinting.org` —Linux 打印信息中心仓库。下载官方和非官方开源驱动程序。如果你打算购买新打印机，可以阅读“建议打印机列表”中的建议。可以在论坛中提问。
- `http://h00188.www.hp.com/wsolutions/linux/products/printing_imaging` —惠普（Hewlett Packard）的 Linux 驱动程序。
- `http://www.tldp.org/HOWTO/Printing-HOWTO` —“如何在 GNU/Linux 下生成、打印和传真任何内容的信息的集合”。
- `http://www.cups.org` —关注通用 Unix 打印系统（Common Unix Printing System）的地方。

## Linux 网络与安全参考 609

- `http://www.pwg.org/ipp` —IETF 打印工作组关于互联网打印协议（IPP）的页面。
- `http://www.tldp.org/HOWTO/User-Authentication-HOWTO` —设置密码。
- `http://www.tldp.org/Shadow-Password-HOWTO.` —影子密码系统（shadow password system）。
- `http://www.novell.com/coolsolutions/feature/1185` —关于权限的简短但良好的概述。
- `http://www.gratis.org/sudo` —超级用户执行（SuperUser Do），如何在交付 Root 权限的情况下向特定用户授权任务。
- `http://www.kernel.org/pub/linux/pam` —可插认证模块（Pluggable Authentication Modules）。
- `http://pub.builder.ibm.com/infocenter/pseries/index.jsp?topic=com.ibm.aix.aixman/security/pam_overview` —针对 AI 系统的 PAM 指南对 Linux 用户很有帮助。
- `http://www-106.com/devdevelopers/linux/sc7.html` —实用 Linux 对处理用户提供了独特的视角。
- `http://searchenterpriseline.techtarget.com/originalContent/0_289142,sid39_gc2846_00.html` —这份安全指南涵盖了各种安全主题的文章和链接。
- `http://www.schneider.com/blowfish.htm` —Blowfish 加密算法主页。
- `http://linuxgazette.org/issue81/vikas.html` —魔法键（SysRq）过程的总结。
- `http://www.learntsubnet.com` —学习使用和提交 IP 地址的良好资源。

## LAMP 及其他编程参考

如果你需要查找更多关于 Linux 编程、Web 开发、LAMP 等信息，请参考以下链接和资源。

- `http://www.apache.org` —Apache 软件基金会伞网站。在此访问所有 Apache 项目。
- `http://httpd.apache.org` —获取 Apache Web 服务器信息的起点。新闻、下载、常见问题。可以在 Docs 子项目中查看 PDF 用户指南。
- `http://modules.apache.org` —Apache 模块注册。查找要安装的模块，并贡献你创建的模块。

# 附录 B SUSE 与 Linux 互联网资源

- `http://www.apachetoday.com` —ServerWatch 的 Apache Today 网站广受关注和使用，是获取 Apache 新闻和教程的优秀来源。
- `http://tldp.org/HOWTO/HOWTO-INDEX/index.html#SERVERHTTP` —与 Web 服务器相关的 HOWTO 索引。主要处理 Apache，但也涉及其他几个项目。
- `http://usefaq.sourceforge.net/faq/apache.html` —非官方 SUSE 常见问题解答（FAQ）列表包含了实用的 SUSE 特定 Apache 信息。
- `http://news.netcraft.com/archives/web_server_survey.html` —Netcraft 对流行 Web 服务器的调查。该调查正在编写，70% 的 Web 运行在 Apache 上。
- `http://modpython.org` —mod_python Apache 模块主页。
- `http://modubry.net` —mod_ruby 页面。
- `http://www.acme.com/software/htttpd` —httpd 主页。
- `https://helix-server.helixcommunity.org` —开源流媒体服务器。
- `http://www.zope.org` —来自 Zope 社区的所有最新精彩动态。
- `http://gcc.gnu.org` —GNU 编译器集合（GCC）主页。
- `http://www.gnu.org/gcc-4.0/changes.html` —GCC 4.0 的新特性。
- `http://www.gnu.org/software/autoconf` —Autoconf 配置系统。
- `http://gcc.gnu.org/java` —GCC 的 Java 编译器 GCJ。
- `http://subversion.org` —设计非常良好的 Subversion 站点。
- `http://svnbook.red-bean.com/en/1.0` —在线书籍《使用 Subversion 进行版本控制》。
- `https://www.cvsome.org` —CVS 站点，安全且组织良好。
- `http://www.linux.ie/articles/tutorials/cvs.php#` —一个略带幽默的 CVS 教程。
- `http://eclipse.org` —Eclipse 社区中心。你启动并保持良好状态所需的一切这里都有。
- `http://www.eclipsecentral.com` —寻找所需的 Eclipse 插件的所在地，同时也提供新闻。
- `http://www.kdevelop.org` —新闻、论坛、文档，以及一个显示该 IDE 每小时下载量的实时图表。
- `http://anjuta.sourceforge.net` —net——GNOME/GTK+ IDE。
- `http://www.digitalfanatics.org/projects/qt_tutorial` —C++ 开发者学习 Qt 的教程。

# LAMP 及其他编程参考 613

- `http://doc.trolltech.com/3.3` —当前版本 Qt 的官方参考文档。
- `http://www.rpm.org` —Red Hat 软件包管理系统信息主页。该网站包含 Ed Bailey 2000 年著作《Maximum RPM》的在线版本。
- `http://www.mysql.com/` —MySQL 数据库主页。世界上最开源的数据库。软件的官方主页，包含新闻、下载和文档。
- `http://dev.mysql.com/doc/` —MySQL 数据库主页仓库。如果你想了解更多关于 MySQL，请访问文档中心。
- `http://www.postgresql.org/` —PostgreSQL 数据库主页。PostgreSQL 是世界上最先进的开源数据库之一，支持几乎所有的 SQL 结构，包括 select、事务、用户定义类型等。
- `http://www.postgresql.org/docs/` —PostgreSQL 数据库主页仓库。这里有丰富的 PostgreSQL 在线信息，可以从这里开始。网站的这一部分包含 PostgreSQL 用户和管理员的当前及存档手册。
- `http://www.knoda.org/` —下载 Knoda 客户端或了解其信息的主页。
- `http://www.perl.com` —Perl 源码。新闻、文章、博客等。
- `http://www.perl.org` —Perl 目录。通往 Perl 宇宙的链接。
- `http://www.cpan.org` —综合 Perl 归档网络。CPAN 是下载模块和其他必选 Perl 资源的地方。如果你写了有用的东西，请上传到这里。
- `http://use.perl.org` —Perl 新闻中心。了解会议、用户组会议和各种事实。
- `http://learn.perl.org` —从何开始 Perl。针对所有专业水平的教程、书籍推荐，以及初学者邮件列表。
- `http://www.tpj.com` —《Perl Journal》月刊。
- `http://www.pm.org` —PerMongers 用户组。
- `http://dev.perl.org/perl6` —Perl 6 枢。在这里获取整体设计信息，以及 Perl 6 和解释器开发的最新进展。
- `http://python.org` —Python 宇宙中心。几乎所有的 Python 链接都指向这里。
- `http://www.pythonware.com/daily` —Daily Python URL，来自整个网络和博客世界的 Python 新闻和评论。
- `http://www.python.org/moin/BeginnersGuide` —面向新编程者的 Python 指南。
- `http://docs.python.org/tut/tut.html` —这个教程承诺在一个下午内教你 Python。
- `http://www.dieoffenbach.de/dev/eric3.html` —Eric IDE 主页。
- `http://www.pyzine.com` —一份在线 Python 杂志。
- `http://en.wikipedia.org/wiki/Python_programming` —一个长而详细的条目，是 Python 语言值得的介绍。
- `http://www.php.net` —PHP 主页。
- `http://www.phpbuilder.com` —教程和新闻网站。
- `http://www.codewalkers.com` —另一个新闻网站，偶尔会举办带有有趣实物奖励的 PHP 竞赛。
- `http://www.phpresourceindex.com` —PHP 资源索引。该网站的主要吸引力是数千个现成的 PHP 脚本、函数和类。你也可以找到其他的以及更大的 PHP 社区。
- `http://www.zend.com` —Zend Technologies，PHP 4 和 5 核心 Zend 引擎的所有者。
- `http://www.weber.com` —更多代码、教程、网页博客。
- `http://www.hotscripts.com` —满足每个 Web 管理员需求的脚本，主要是 PHP，也有 Perl、JavaScript 甚至 C++。内容不断更新，这里是寻找资源的好地方。
- `http://phpdeveloper.org` —面向所有类型 PHP 编码者的新闻和论坛。
- `http://www.thelinuxancy.co.uk/php.php` —可过滤的 PHP 资源。
- `http://www.php.org/modin/php.php` —PHP 模块。
- `http://subversion.org` —设计非常良好的 Subversion 站点。
- `http://svnbook.red-bean.com/en/1.0` —在线书籍《使用 Subversion 进行版本控制》。
- `https://www.cvsome.org` —CVS 站点，安全且组织良好。
- `http://www.linux.ie/articles/tutorials/cvs.php#` —一个略带幽默的 CVS 教程。
- `http://eclipse.org` —Eclipse 社区中心。你启动并保持良好状态所需的一切这里都有。
- `http://www.eclipsecentral.com` —寻找所需的 Eclipse 插件的所在地，同时也提供新闻。
- `http://www.kdevelop.org` —新闻、论坛、文档，以及一个显示该 IDE 每小时下载量的实时图表。
- `http://anjuta.sourceforge.net` —net——GNOME/GTK+ IDE。
- `http://www.digitalfanatics.org/projects/qt_tutorial` —C++ 开发者学习 Qt 的教程。

# LAMP 及其他编程参考 613

- `http://doc.trolltech.com/3.3` —当前版本 Qt 的官方参考文档。
- `http://www.rpm.org` —Red Hat 软件包管理系统信息主页。该网站包含 Ed Bailey 2000 年著作《Maximum RPM》的在线版本。
- `http://www.mysql.com/` —MySQL 数据库主页。世界上最开源的数据库。软件的官方主页，包含新闻、下载和文档。
- `http://dev.mysql.com/doc/` —MySQL 数据库主页仓库。如果你想了解更多关于 MySQL，请访问文档中心。
- `http://www.postgresql.org/` —PostgreSQL 数据库主页。PostgreSQL 是世界上最先进的开源数据库之一，支持几乎所有的 SQL 结构，包括 select、事务、用户定义类型等。
- `http://www.postgresql.org/docs/` —PostgreSQL 数据库主页仓库。这里有丰富的 PostgreSQL 在线信息，可以从这里开始。网站的这一部分包含 PostgreSQL 用户和管理员的当前及存档手册。
- `http://www.knoda.org/` —下载 Knoda 客户端或了解其信息的主页。
- `http://www.perl.com` —Perl 源码。新闻、文章、博客等。
- `http://www.perl.org` —Perl 目录。通往 Perl 宇宙的链接。
- `http://www.cpan.org` —综合 Perl 归档网络。CPAN 是下载模块和其他必选 Perl 资源的地方。如果你写了有用的东西，请上传到这里。
- `http://use.perl.org` —Perl 新闻中心。了解会议、用户组会议和各种事实。
- `http://learn.perl.org` —从何开始 Perl。针对所有专业水平的教程、书籍推荐，以及初学者邮件列表。
- `http://www.tpj.com` —《Perl Journal》月刊。
- `http://www.pm.org` —PerMongers 用户组。
- `http://dev.perl.org/perl6` —Perl 6 枢。在这里获取整体设计信息，以及 Perl 6 和解释器开发的最新进展。
- `http://python.org` —Python 宇宙中心。几乎所有的 Python 链接都指向这里。
- `http://www.pythonware.com/daily` —Daily Python URL，来自整个网络和博客世界的 Python 新闻和评论。
- `http://www.python.org/moin/BeginnersGuide` —面向新编程者的 Python 指南。
- `http://docs.python.org/tut/tut.html` —这个教程承诺在一个下午内教你 Python。
- `http://www.dieoffenbach.de/dev/eric3.html` —Eric IDE 主页。
- `http://www.pyzine.com` —一份在线 Python 杂志。
- `http://en.wikipedia.org/wiki/Python_programming` —一个长而详细的条目，是 Python 语言值得的介绍。
- `http://www.php.net` —PHP 主页。
- `http://www.phpbuilder.com` —教程和新闻网站。
- `http://www.codewalkers.com` —另一个新闻网站，偶尔会举办带有有趣实物奖励的 PHP 竞赛。
- `http://www.phpresourceindex.com` —PHP 资源索引。该网站的主要吸引力是数千个现成的 PHP 脚本、函数和类。你也可以找到其他的以及更大的 PHP 社区。
- `http://www.zend.com` —Zend Technologies，PHP 4 和 5 核心 Zend 引擎的所有者。
- `http://www.weber.com` —更多代码、教程、网页博客。
- `http://www.hotscripts.com` —满足每个 Web 管理员需求的脚本，主要是 PHP，也有 Perl、JavaScript 甚至 C++。内容不断更新，这里是寻找资源的好地方。
- `http://phpdeveloper.org` —面向所有类型 PHP 编码者的新闻和论坛。
- `http://www.thelinuxancy.co.uk/php.php` —可过滤的 PHP 资源。

# 索引

## 符号
- `&`, 132
- `*` 在 Perl 中, 539
- shell 脚本中的转义字符,
- 在 Perl 中, 539
- `^` 在 Perl 中, 539
- `$` 在 Perl 中, 539
- 在 Perl 中, 539
- 作为 DNS 根域, 481
- 内置变量, 137-139
- `$*` 内置变量, 139
- `$0` 内置变量, 139
- `$?` 内置变量, 139
- 在 bash 中, 135
- `%` 在 Perl 中, 536
- `|` 在 Perl 中, 539
- `+` 在 Perl 中, 539
- `?` 在 Perl 中, 539

## 数字
- 10/100 Base以太网网络, 447
- 64 位处理器, 14

## A
- A (地址) 资源记录, 483
- AbiWord, 151-152
- ac 命令, 348
- ac 补丁, 434
- 访问时间, 禁用, 571

## 辅助模块 (GNOME)
- 辅助模块 (GNOME), 107
- ACPI (高级配置和电源接口, 55-56
- 添加新用户屏幕, 40
- add 命令 (CVS), 510
- 地址 (A) 资源记录, 483
- 通讯录, 235
- 管理模式按钮 (KDE 控制中心), 106
- Adobe Reader, 122-123
- 高级 Linux 架构 (ALSA), 163-164
- 高级软件包工具 (APT), 388-391
- 高级电源管理 (APM), 55
- AFPL Ghostscript, 114
- KDE Akregator, 259
- 别名, 73
- bash shell, 74, 33-135
- CNAME (规范别名) 资源记录, 483
- 别名配置, 264
- 允许目录 (Apache2/httpd.conf), 465-466
- Almquist shell (ash), 78
- ALSA (高级 Linux 架构), 163-164
- AMD 64 位处理器, 14
- 美国互联网数字注册机构 (ARIN), 444, 494
- Ampersands (&), 132
- 创建 Anjuata GNOME 应用, 506-508
- 匿名 FTP, 290, 301-303
- 杀病毒工具, 246-266, 273
- AOL 即时通讯/ICQ, 285
- Apache 软件基金会, 460
- Apache SpamAssassin 项目, 265
- Apache 服务器
    - 访问限制, 465-466
    - 身份验证, 466-468
    - 配置设置, 463-465
    - 动态内容生成, 472-474
    - 历史, 459-460
    - 安装 Apache, 460-461
    - 模块, 468-469. 另另特定模块
    - 在线参考, 475-476
    - 运行级别设置, 462
    - 源代码下载, 460-461
    - 测试, 462
    - 升级 Apache 源码版本, 462
    - 虚拟主机实现, 469-472
- apache2-MPMs, 460-463
- Apache2/httpd.conf 文件, 463-465
- APM (高级电源管理), 55
- APOL pop 协议, 263
- 外观与主题区域 (KDE 控制中心), 104
- 外观设置
    - GNOME, 107
    - KDE, 104
- Apple
    - Gs 作为 64 位处理器, 14
    - MacOS Classic Basil 模拟器, 195-196
- 应用
    - DOS, 运行, 196
    - 创建 GNOME 应用, 506-508
    - 查看已安装应用, 393
    - 安装
        - 使用 APT (高级软件包工具), 388-91
        - 命令行, 378
        - 从互联网下载, 372-382
        - 在线参考, 395-396
        - 使用 Red Carpet, 391-393
        - RPM (Red Hat 包管理), 382-383, 510-514
        - 使用 YaST 安装和移除软件模块, 375-376
        - 使用 YOU (YaST 在线更新) 模块, 382-388
    - Java 应用, 501-503
    - KDE 应用, 506
    - 启动
        - 在 FVWM 中, 108-109
        - 在 GNOME 和 KDE 中, 96
        - 在 WindowMaker 中, 109-110
        - MacOS Classic, 运行, 195-196
        - 源代码编译, 394-395
        - 使用 YOU 更新, 386
    - Windows, 运行
        - 使用 Crossover Office, 190
        - 使用 VMware, 193-195
        - 使用 Win4Lin, 191-192
        - 使用 Wine, 187-190
- 网络广播电台, 164-167
- 录制工具, 167
- 声卡配置, 163-164
- 流媒体传输, 166
- Application Dock (WindowMaker), 109-110
- Apache PAM (可插件认证模块), 346-347
- APT (高级软件包工具), 388-391
    - 更改默认位置, 362
    - 提取到源码, 394-395
    - 选择格式, 359
    - 磁带驱动, 365
    - tar 工具, 363
- bash shell, 619
    - 身份验证
    - 应用, 154
    - apropos, 17
    - 自动补全 (OpenOffice.org), 147
    - 使用脚本自动化任务, 137-139
    - Autoconf 工具, 498
    - Auto Pilots (OpenOffice.org), 243-244
- Azure, 300-301

## B
- ARIN (美国互联网数字注册机构), 444, 494
- 算术运算符, 538
- 数组 (Perl), 536-542
- ascii 命令 (FTP), 291
- ash shell, 78
- 辅助技术 (GNOME), 107
- 异步通信, 271
    - 邮件流量, 262
    - 邮件列表, 281-283
    - 在线参考, 287-288
    - Usenet 新闻, 272-278
    - Wikis, 279
- ATA 硬盘, 566-567
- Atom, 222, 255, 259
- 备份
    - GNOME, 107
    - KDE, 104
    - 需求和资源, 354-355
    - 双启动系统, 360
    - File Roller (GNOME), 365-366
    - 镜像磁盘, 357, 366
    - 网络存储, 358
    - RAID 数组, 366-368
    - 可移动式存储, 323-358
    - SOHO (小型/家庭办公) 策略, 355-356
    - 系统备份 (YaST), 359-362
    - 磁带驱动, 359
    - tar 文件, 364
    - Windows, 355
- Base (OpenOffice.org), 143
- Base Setup (Wine), 188
- base 系统安装, 73
- Base shell, 72-78
- 创建别名, 133-135
- 为变量赋值, 136
- Base64/MIME, 241
    - 发送, 239-240
    - 查看 TNEF 文件, 240
    - UUEncode/UUDecode, 240-241
- 音频攻击, 419
    - 转换文件, 166
    - 文件格式, 165-166
- bash shell, 620
    - 自动化任务, 137-139
    - 内置变量, 139
    - 注释, 135
    - 生成可执行文件, 135
    - 位置参数, 136-137
    - 特殊字符, 130
- Blossom, 255-256
- Blowfish 加密, 38
- Bluefish, 245-247
- Bluetooth, 57, 104
- bluez, 57
- BMP 文件, 180
- 使用 bonnie, 562
- .bashrc 文件, 73-75
- 身份验证 (Apache), 466-468
- Basilik II, 195-196
- 电池环按钮, 56
- Beagle 文件, 226-329
- Behlendorf, Bob, 459
- 执行基准测试, 562
- bin 命令 (FTP), 291
- 启动磁盘模块 (YaST), 370
- 启动磁盘, 370
- Boot Loader 配置模块 (YaST), 401
- 启动顺序设置, 34
- 启动过程, 399
- BIOS, 400
- 启动管理器, 400, 439
- 安全失败模式, 401
- 加载内核, 403-405
- 在线参考, 414-415, 595-606
- 救援磁盘, 370
- 检查 SUSE LINUX 安装, 34-35
- 端口号, 446
- BIND (Berkeley 域名系统), 489-493
- BitTorrent, 299
- 创建空白图像文件, 330
- 块设备文件, 333-334
- 块, 308-309
- 聚合器, 259
    - 使用 Blossom, 255-255
    - 使用普通网站, 254
    - 使用 Movable Type, 256-257
    - 使用 Notepad, 257
    - 使用 WordPress, 257
- 博客行, 295
- 博客列表, 255
- 引导扇, 308
- 创建可引导内核, 736
- 桥接, 448-449
- 芯片组驱动, 174
- Build 部分 (RPM 文件), 512
- 内置频, 555-557
- 内置变量, 135, 139
- bye 命令 (FTP), 290
- zip 存档格式, 359

## C
- Calc (OpenOffice.org), 143
- CalDAV (日历编写与版本控制) 标准, 267
- 日历
    - 图形, 293-295
    - 文本文本, 290-292
- 剪贴板, 97
- CNAME (规范别名) 资源记录, 483
- 密码, 190
- ColdFusion, 275
- 协作工具, 271
- 即时消息, 285-286
- IRC (互联网中继聊天), 284-285
- 邮件列表, 281-283
- 在线参考, 287-288
- Usenet 新闻, 272-278
- 视频会议, 286-287
- Evolution, 234
- KOrganizer, 235-237
- Mozilla 日历, 237
- Perl 中的 caret符号, 539
- 使用 cat, 575-576
- Caudium WebServer, 474
- 更改目录, 576-577
- 硬盘
    - 备份到, 358
    - BIOS 设置, 34-35
    - 挂载, 59-60
    - 使用 DMA 加速, 60-61
- CD-ROM 模块 (YaST), 59-60
- CD-R/RW 磁盘, 172, 358
- CDs
    - 刻录
    - 从 shell, 170-173
    - 在 GNOME 中, 170
    - 在 KDE 中, 168-170
    - 概述, 167-168
    - 数据包写入, 173-174
    - 会话写入, 173
- CDDB (数据库)
- Cedeba, 181
- Cervisia, 150
- CGI (通用网关接口), 472, 535
- changelog (RPM 文件), 513
- channels (Red Carpet), 391-393
- 字符设备文件, 创建, 333-334
-  checkout 命令 (CVS), 510
- chgrp 命令, 84-85
- chmod 命令, 85-86, 577
- chow 命令, 84
- Christians, Tom, 140
- Civilization, 182-183
- ClAM, 267
- Class A/B/C/D 网络, 444-444
- class statements (Python), 543
- Cleanup 部分 (RPM 文件), 513
    - 协作软件开发, 509-510
- com. domain, 481
- 命令联盟, 创建, 133-135
- 命令行 shell. 另另 刻录
- CDs, 刻录, 170-172
- DVDs
    - 刻录, 172-173
    - 数据包写入, 173-174
    - 会话写入, 173
- commands. 另另个人命令
    - 别名, 创建, 133-135
    - FTP 命令, 290-291
    - 组相关命令, 342
    - 历史, 72
    - 在 CVS, 510
    - Linux shell 命令, 574-575
    - Mailman 命令, 283
    - 打印命令, 124-125
    - shell 命令, 128. 另另 Linux shell
- 安装应用从, 378
- YaST, 运行, 从 78-79

## 比较运算符 (Perl)

比较运算符 (Perl), 537
编译器 (C 程序), 500
编译
内核, 436-437
故障排除, 438-439
何时编译, 432-433
源码, 394-395

复杂配置对话框 (NTP), 53-54
复合运算符 (Perl), 537
压缩, 359

Config 模块 (FVWM), 109
配置文件, 在 /etc 目录中编辑, 69-70
配置
- Apache, 463-465
- 桌面环境, 104-107
DHCP, 452
DNS
- 在本地客户端上, 483-486
- 基于服务器的服务, 489-493
测试配置, 487-489
使用 hosts 文件, 486

GNOME, 106-107
硬件, 46
CD 驱动器, 59
GNOME, 107
HDC 事件, 46-47
信息报告, 显示, 46
- 摇杆, 47
KDE, 105
键盘布局, 28
鼠标设备, 48-49
打印机, 115-119
扫描仪, 49

电视和收音机卡, 49-50
IceWM, 111-112
Internet 连接
- 拨号, 38-39, 206-210
- DSL (数字用户用户线), 211-215
在 SUSE Linux 安装期间, 38-39

KDE, 104-106
带有系统调用的内核, 439-440
KOOffice, 149
笔记本电脑
- 蓝牙支持, 57
IrDA 模式, 58-59
PCMC 卡, 57
电源管理, 56-57
本地回接口, 205-206
Mailman, 282-283
MTA, 263-264
MySQL 服务器, 525

NFS 服务器, 454
OpenOffice.org, 144-146
声卡, 163-164
显卡, 163-174
WindowMaker, 110
无线网卡, 217-218

X Window 系统, 92-94
xinetd, 455

连接
数码相机, 177
Internet 连接, 203
在 SUSE Linux 安装期间配置, 38-39
拨号, 38-39, 206-210
DSL (数字用户用户线), 211-215
IP 地址, 204-205
本地回接口, 205-206
控制台 shell
上下文切换, 562
控制中心 (MySQL), 525
社区网站, 17

cp 命令, 利用, 579
CPAN 模块 (Perl), 539-540
Creative Labs SoundBlaster, 163
跨平台计算, 另见 模拟器
误解, 187
在线参考, 199-200
虚拟机
Win32, 193-195
Win4Lin, 191-192
Xen, 196-199

Windows 文件系统, 185-186
Crossover Office, 190

## DNS (域名系统) 623

CUPS, 114-115, 122
管理指南, 125
配置, 119
默认设置, 更改, 121-122
网络打印机, 121
shell 令, 124-125
网站, 608
CVS (并发版本控制), 160, 509-510
Cyrus IMAP 服务器, 264

/dev 目录, 68-69
设备驱动程序, 431
设备号, 333
DHCP, 204, 451-453
Dia, 159
网络绘图
Dia, 159
Kivio (KOOffice), 149
拨号 Internet 连接
配置, 38-39, 206-210
故障排除, 218-219
dialout 组, 342
dig (域名接口网关), 487
dig 认证 (Apache), 466-468
digam, 177
dig 相机, 176-180
dig 数字用户用户线 (DSL) Internet 连接, 215-211

## D

\d 元字符 (Perl), 539
DALNet Inc 网络, 284
数据传输硬盘速率, 567
数据库
- 客户端, 527-529
GNOME DB, 151
MySQL 安装, 519-521
关系型, 517-519
SQL (结构化查询语言), 588
Date and Time 模块 (YaST), 50-51
设置, 50-52
DCOM, 189
dd 命令, 330
Dell Linux , 32
deny 指令 (Apache/httpd.conf), 465-466
depmod 命令, 432
DES 加密, 388
桌面环境, 94-96
配置, 104-107
GNOME 硬件配置, 41
键盘设置, 48
鼠标设置, 49
多个桌面, 95, 104
time/date 设置, 51
Word, 148
scribus, 157-158
Textmaker (Softmaker), 152
目录
文件系统, 66
内核源码树, 430
使用 ls 列出文件, 579
分区, 31
directory 指令 (Apache/httpd.conf), 465
磁盘控制器, 46-47
磁盘硬盘速度, 567
磁盘空间, 使用 du, 578
Disk Device Wizard (YaST), 211-225
DMA (直接内存访问), 60-61
DNS (域名系统), 477-480
DNS 客户端, 483-486
DNS 服务器, 489-493
测试配置, 487-489
层次结构, 480-482
日志, 493-494
在线资源, 494
资源记录, 483, 492

## DNS (域名系统)

zone 文件, 482-483
添加/删除, 491-492
编辑, 492-493
DNS and Host Name 模块 (YaST), 452
Documentation 目录, 430
DocumentRoot 指令 (Apache/httpd.conf), 465
Documents and Templates (OpenOffice.org), 144
Domain Internet Gateway (dig), 487
dig (Domain Internet Gateway), 387
FQDNs (完全限定域名), 480
顶级, 480-482
虚拟域名, 264
Dornfest, Rael, 255
DoS 攻击, 455
DOSBox, 196
dosemu, 196
拖放文件管理, 135
Draw (OpenOffice.org), 143
绘程序
Draw (OpenOffice.org), 143
Karbon14 (KOffice), 149
DSL (数字用户线) Internet 连接, 211-215
命令, 578
跨平台计算
哑网关, 448
备份到, 358
BIOS 设置, 34-352
挂载, 59-60
DVD+RW 磁盘, 358
DVDs
刻录
从 shell, 170-173
在 GNOME 中, 170
在 KDE 中, 168-170
概述, 167-168
数据包写入, 173-174
会话写入, 173

动态主机配置协议, 204, 451-453
动态 IP 地址, 451-453
动态网站, 472-474

## E

- Eclipse, 501-503
ed 编辑器, 82
编辑
图像, 178-180
分区, 314-315
edu 域名, 482
EFNet IRC 网络, 284
elm, 238-239
- Emacs 文本编辑器, 81-82
网站创建, 248
邮件
帐户, 设置, 227-228
异步流量, 262
反病毒工具, 264-267
附件
BinHex, 240
解码, 241
MIME/Base64, 241
发送, 239-240
TNEF 文件, 写入, 240
UEncode/UUDecode, 240-241
yenc, 240
客户端
- Evolution, 229
- Mail, 232-234
- Contact, 234
- mutt, 238
- Thunderbird, 237
Fetchmail, 228
认证, 263
投递, 264
入邮件, 263
伪装, 263
远程连接, 264
垃圾邮件, 266
Postfix, 227
Usenet 新闻, 274

## File Roller (GNOME)

- 网络客户端, 274
以太网卡, 配置, 38-39
epiphany, 225
启用挂按钮, 56
专家模式, 410
专家分区工具, 311-312
创建分区, 313
删除分区, 315
编辑分区, 314-315
加密分区或文件, 315-317
RAID 分区, 368
读取分区, 317
调整分区大小, 315
- ext2/3 文件系统, 310
扩展守护进程, 203
服务集标识符 (ESSID), 217
扩展分区, 312
网络服务安全, 455
蓝牙通信, 315
Root 用户密码, 38
环境变量
可访问值, 136
命令别名, 133-135
声明与初始化, 136

## F

- F-Prot, 267
安全模式, 401
伪 Windows 目录 (Wine), 184
误报, 265
FAT 文件系统, 30, 186, 308
收藏, 224
传真应用, 160-161
订阅, 259
Fetchmail 配置, 228
光纤布线, 447-448
文件共享

文件共享, 295-296
BitTorrent, 299-301
Napster 风格, 296-298
文件系统, 308

使用 locate, 321
使用 whereis, 324
使用 which, 323
图形格式, 180
使用 Midnight Commander 管理, 76-77
操作, 577
权限, 82-86, 341-342
符号链接, 68

选择, 311
为测试创建, 329-331
ext2/3, 310
JFS, 310
日志文件系统, 309-310
Linux, 66-7
使用 Expert Partitioner 管理, 311-313

创建分区, 313-314
删除分区, 315
编辑分区, 314-315
加密分区或文件, 315-317
调整分区大小, 315

文件 (RPM spec 文件), 513
财务软件, 155-156
find 实用, 320-321
finger 命令, 71-72

Firebox
挂载, 317, 330
stab (文件系统表), 319-320
mount 命令, 318
在线参考, 89, 335
物理磁盘结构, 308-309
Reiser4, 310
ReiserFS, 13, 309-310
卸载, 318
Windows, 30, 186

新闻源聚合器, 259
概览, 422-424
防火墙, 422-424
FireWire 驱动器, 358
软盘镜像文件, 332
流程图程序

Dia, 159
Kiv (KOOffice), 149
字体安装器 (KDE), 106
字体

GNOME, 107
Windows 字体（包括 Linux 中的字体）, 106
公式编辑器
KFormula (KOOffice), 149
Math (OpenOffice), 143
论坛, 555-557
正向查找区域, 482-483
转发 (DNS), 配置, 489-491
FQDNs (完全限定域名), 480
帧采集器, 175

文件传输
FTP
图形化客户端, 293-295
sftp (安全 FTP) 客户端, 292-293
基于文本客户端, 290-292
在线参考, 303-304
点对点, 295
BitTorrent, 299-301
Napster 风格, 296-298

另见单个文件名/类型
音频文件, 165-166
备份. 见备份
内容，显示, 575-576
使用 rm 删除, 580-581
查找
使用 Beagle, 326-329
使用 find, 320-321
使用 kfind, 324-326

自由软件项目, 594
Freeciv, 182-183
FreeDOS, 196
freshmeat.net 基准测试包, 562
stab (文件系统表)
描述, 69
挂载文件系统, 319-320

# FTP

客户端
图形化, 293-295
sftp, 292-293
基于文本, 290-292
服务器
匿名, 290, 301-303
标准, 301
ftp 命令, 290
FTP 服务器端口号, 446
全量备份, 356
完全限定域名 (FQDNs), 480
C 程序中的函数, 498
FVVM, 108-109

配置, 106-107
默认桌面, 98
Epiphany, 225
File Roller, 365-366
游戏, 182
gtkam, 177
人机交互指南 (HIG)
文档, 96
多个虚拟桌面, 95
autilus, 103-104
概览, 94-99
新闻阅读器, 275-276
PDAs, 连接, 155
时间/日期, 51
GNOME 控制中心, 106-107
键盘设置, 48
鼠标设置，配置, 49

# G

作为 64 位处理器的 G 芯片, 14
GAIM 即时通讯, 286
Galeon, 225-226
游戏类, 180-182
GCC (GNU 编译器集), 499
编译源码, 394-395
make 实用, 395
gdb (GNU 调试器), 498
get 命令 (FTP), 291
gFTP 客户端, 293-294
Ghostscript, 114
GIMP (GNU 图像处理程序), 178-180
given 语句 (Perl), 541
GLUE (到处 Linux), 19, 591
Gmail (Google), 358
应用程序
创建, 506-508
启动, 96
CD/DVD, 刻录, 190
会议, 286-287
AbiWord, 152
安装, 151
在线文档, 152
包含程序, 151
GNU 编译器, 499
编译源码, 394-395
make 实用, 395
GNU 调试器 (gdb), 498
GNU 图像处理程序 (GIMP), 178-180
GNU Parted, 296
GNU 项目, 594
GCash, 11-155
数值, 151
Gnutella, 421
Gnutella 网络, 298
GNUZip, 359
Google, 358
组, 273-274
gov 域名, 482
密码命令, 342
gphoto, 177
表 (MySQL), 521-522
图形化 FTP 客户端, 293-295

# 图形

图形, 176-180
图形交换格式 (GIF)文件, 180
格林治时间, 51
grep 命令, 578
groupadd/del 命令, 342
组, 342-343
到处 Linux (GLUE), 19, 591
gdisk 命令, 342
GRUB (统一引导加载程序), 400
菜单, 402-403
故障排除, 439
GTK-Gnutella, 298
gtam, 177
vim 编辑器, 81

调优, 566
文件访问时间，禁用, 571
hdparam 实用, 569-571

硬件
配置
CD 驱动器, 59
GNOME, 107
HDC 设置, 46-47
信息报告, 75
摇杆, 47
KDE, 105
键盘布局, 48-49
鼠标设备, 48-49
打印机, 115-119
扫描仪, 49
电视 和收音卡, 49-50

# H

黑客，恢复, 425-426
Hancom Office, 154
硬盘

选择, 566-567
数据传输速率, 567
磁盘旋转速度, 567
磁盘空间，使用 KDisk 查看, 413
驱动器接口, 566-567
IDE/ATA, 566-567
MBR (主引导记录), 400
多个硬盘，利用, 571
分区, 29-31
- 添加分区, 36, 313-314
- 更改文件系统, 36
- 删除分区, 315
- 编辑分区, 314-315
- 加密分区, 315, 317
- 扩展分区, 312
dfsck 实用, 311
- 在线参考, 32, 595-606
建议分区大小, 29
调整分区大小, 315
- 交换分区, 30
物理结构, 308-309
RAID 阵列，设置, 366-368

网络中
桥接, 448-449
布线, 448
集线器, 448
初始化, 449-451
NICs (网络接口卡), 447-488
路由器, 448-449
旧硬件, 26-27
SUSE Linux 安装
内置外设, 28
旧硬件考虑量, 26-27
在线参考, 32
基于软件的介质, 27-28
SUSE Linux Database, 24-26

硬盘控制器, 46-47
硬件信息模块 (YaST), 46
hash 命令 (FTP), 291
hashes (Perl), 536-537
dbchen, 562
HDC 设置，修改, 46-47
hdparam 实用, 569-571
头文件 (C 程序), 498
头部区域 (RPM spec 文件), 511
Helix 社区, 166
Hello World 程序
- C 语言, 499-500
- Java 语言, 502-503
- KDevelop 语言, 505-506

帮助

帮助中心, 15-16, 59
info 页面, 16

ImageMagick, 180
图像, 176-180
IMAP (互联网邮件访问), 262
Impress (OpenOffice), 143
增量备份, 356
缩进规则 (Perl), 54
日志文件系统 (JFS), 310
info 页面, 16
初始化过程, 404
喷墨打印机, 126
日志文件系统, 309
输出重定向, 131
节点, 309
分区格式 (spec 文件), 512
默认设置, 35
双系统启动，Windows, 35
调文件系统, 548
脆弱性, 221

IANA (互联网分配数字), 49
Icecast, 167
IceWM, 111
界面和网络区域 (KDE 控制), Center, 104
Internet  way
安装, 189
运行, 190
在网页上测试, 247
脆弱性, 221

互联网邮件, 262
互联网收音机, 164
中继聊天 (IRC), 284-285
互联网系统联盟 (ISC), 494
互联网时间, 51
中断请求, 562

文本编辑器, 82
网站创建, 248
日志文件系统 (JFS), 310
联合图像专家组 (JPEG), 180

I

IDE 硬盘, 566-567
互联网/网络连接, 38-39
在笔记本上, 295-606
硬盘分区, 29-31, 36
规划考虑, 22-23
Root 用户，创建, 37-38
启动, 35

集成开发环境. 见 IDEs

IDEs, 506-508
Eclipse, 501-503

# 安装 SUSE Linux

系统要求, 23-26
时区，设置, 36
故障排除, 45-46
用户，创建, 40
即时消息, 285-286

IP 别名, 471
IP 包, 443-444
基于 IP 地址的虚拟主机,
实现, 204
ipconfig 命令, 204
IPv4 (互联网协议, 版本 4), 444-445
IPv6 (互联网协议, 版本 6), 445-446
IRC (中继聊天), 284-285
IrDA (红外数据关联),
配置, 58-59
ISC (互联网系统联盟), 494
ISO9660 文件系统, 308

互联网连接, 203
拨号
配置, 38-39, 206-210
故障排除, 218-219

DSL (数字用户线路), 211-215
从...安装应用程序, 379-382
IP 地址，确定, 204-205
本地接口, 205-206
在线资源, 219
问题, 218-219

# J

J-Pilot, 155
Jabber 协议, 286
Java 应用程序，构建, 501-503
JEdit

界面和网络区域 (KDE 控制), Center, 104
Internet 浏览器
安装, 189
运行, 190
在网页上测试, 247
脆弱性, 221

## Ksirc IRC 客户端

631

- 日历 (calendars), 237
- CD/DVD 刻录, 168-170
- 配置 (configuring), 104-106
- 默认桌面, 96-97
- Digikam, 177
- 邮件客户端 (email clients)
  - KMail, 235-237
  - 联系人 (Contact), 234-237
- 传真应用 (fax applications), 160-161
- 游戏 (games), 182
- KDevelop, 506
- Conqueror
  - 利用 (utilizing), 99-101
  - 作为网页浏览器, 224
- Krusader, 101-103
- KSysGuard, 412
- KwikDisk, 413
- 多个虚拟桌面, 95, 104
- 概述 (overview), 94-97
- PDA 连接, 155
- 安全 (security), 105
- 时间/日期设置, 51

- 内核源码包 (kernel-sources package), 430
- 键缓冲区使用 (key buffer usage), 531-532
- 键盘布局模块 (YaST), 48
- 键盘 (keyboards)
  - 配置 (configuring)
    - GNOME, 107
    - KDE, 105
  - 布局调整 (layout, adjusting), 48
- 密钥驱动器 (keychain drives), 357-358
- kfind 实用工具, 324-326
- KFormula, 149
- KHotkeys, 105
- Kicker (KDE), 96, 104
- Kivio, 149
- Klipper 实用工具, 97
- KMail (邮件用户代理), 235-237
- KMLdon, 297-298
- KMyMoney, 115-156
- Knada 数据库客户端, 529
- 节点 (Node), 235
- KNode 新闻阅读器, 276-278
- 笔记 (notes), 235
- KOffice, 111
  - 配置/安装 (configuring/Installing), 149
  - 包含的程序, 148
- Kolab/Kroupner, 268

- KDE CD 播放器, 165

- KDE 控制中心 (KDE Control Center), 104-106
- 键盘设置配置, 48
- 鼠标设置配置, 49

- KDevelop, 505-506
- KDiskFree, 413

- 内核 (kernel)
  - 创建可启动内核, 437
  - 编译 (compiling), 436-438
  - 故障排除 (troubleshooting), 438-439
  - 何时需要重新编译, 432-433
  - 下载选项, 434-335
  - 加载 (loading), 403-405
  - 模块管理 (module management), 431
  - 在线参考 (online references), 440-441
  - 补丁 (patching), 435-436
  - 源码树 (source tree), 430
  - 污染内核 (tainted kernels), 438
  - 故障排除 (troubleshooting), 438-439
  - 使用 sysctl 实用工具调整参数, 439-440
  - 类型, 430-431
  - 版本号, 433-434

- Conqueror
  - 作为网页浏览器, 224
  - 利用 (utilizing), 99-101
- 联系人 (Contact), 11, 234-237
- Kopete 即时通讯软件, 268
- KOrganizer, 235-237
- Koshell, 148
- KParts, 148
- Katience, 181
- KPilot, 235
- KPOP 邮件协议, 263
- KPresenter, 146
- krells, 413
- rita, 149
- Krusader (KDE), 101-103
- KSCD, 165
- sh shell, 77
- Ksirc IRC 客户端, 284

我们如何让这个索引变得更有用？请发送邮件至 indexes@sampublishing.com

## KSpread

- KSpread, 148-151
- KSysGuard, 412
- Kugar, 149
- Kvim 编辑器, 81
- Kvirc IRC 客户端, 284
- KwikDisk, 413
- KWord, 148-151

- ls, 579
- man, 579-580
- mdir, 576-577
- mv, 577
- ps, 580
- rm, 580-581
- tail, 581
- top, 581-582
- which, 582

## L

## LAMP

- Linux 标准基础 (LSB), 67
- Linux 用户组 (LUGs), 19, 594
- Linux 白皮书, 593
- LinuxSecurity.com, 427
- 实时书签 (Firefox), 259
- LiveJournal, 258

- 在线参考 (online references), 611-614
- 概述 (overview), 535

- 本地组 (Local groups), 342-343
- 主机接口 (hosthost interface), 205-206
- locate 实用工具, 321
- 日志输入输出 (logging in/out)
  - Linux shell (Linux shell), 66
  - 以 root 身份 (as root), 309

- 局域网地址 (LAN addresses), 444-445. 另见无线网络

- 笔记本电脑 (laptops)
  - 蓝牙设置 (Bluetooth setup), 57
  - Irda 模式 (Irda mode), 58-59
  - PCMIA 卡卡, 57
  - 电源管理 (power management), 56-57
  - SUSE Linux 安装, 26
  - SUSE Linux, 42-43
  - X Window 系统, 320

- Linux Loader (Linux Loader), 400-402
- Linux 可启动卡 (Linux Bootable Card), 32
- Linux 文档项目 (Linux Documentation Project), 17-18, 593
- Linux 火线 (Linux Firewire), 32
- Linux 新闻组 (Linux newsgroups), 615-616
- 笔记本上的 Linux (Linux on Laptops), 594
- Linux shell 命令 (Linux shell commands), 573-575

- 逻辑卷管理 (Logical Volume Management (LVM)), 320
- LUGs (Linux 用户组), 19, 594
- LVM (逻辑卷管理 (Logical Volume Management)), 320

- 最后命令 (last command), 349
- 租赁 (leases (DHC)), 26-27
- 遗留硬件 (legacy hardware), 291
- libga (GNOME), 151
- libpt 命令, 291
- 回环接口 (loopback interface), 205-206
- losetup, 330
- ip 命令, 125
- ipstat 命令, 125
- is -dl 命令, 86
- is -l 命令, 83
-ismod 命令, 579
-ismod 命令, 431 (注：此处原文可能有重复或拼写错误，已按原样翻译)

- cat, 575-576
- cd, 576-577
- chmod, 577
- cp, 577
- d, 578
- grep, 578
- locate, 579

## M

- MAC (介质访问控制 (Media Access Control)) 地址, 447
- 64 位处理器上的 Mac (Macs as 64-bit processors), 144
- Basilisk II 模拟器, 195-196
- 邮件客户端 (mail clients), 229
- KMail 地址, 235-236
- 邮件 概述 (overview), 18-19, 281-283, 593
- Mailman, 282-283

- C 程序中的 main() 函数 (main() function in C programs), 499
- Java 程序 (Java programs), 503
- 主要数字 (major numbers), 335
- make 编译内核 (make compiling kernel), 436-438
- make 实用工具, gcc (make utility, gcc), 395
- makefiles, 430
- man 命令, 579-580
- man 手页 (man pages), 16, 579-580
- 主引导记录区 (Master Root Book (MBR)), 400
- 添加 DNS 区域 (master zones (DNS), adding), 491
- MaxClients 指令 (MaxClients directive (Apache/2/httpd.conf)), 465
- 主引导启动 (MBR (Master Root Boot)), 400
- 介质访问控制 (Media Access Control (MAC)) 地址, 447
- Helix 媒体质播放器社区 (media players Helix Community), 166-167
- Mplayer, 174-176
- RealPlayer, 166-176
- Xine, 174-216
- XMMS (X 多媒体系统 (X Multimedia System)), 164-166
- Meier, Sid, 182

- 内存 (memory), SU Linux 要求 (SU Linux requirements), 24
- GNOMEDB 菜单模块 (Menu module (GNOMEDB)), 151
- Perl 中的 mergefile (mergefile in Perl), 538-539
- mget 命令 (FTP), 291
- Microsoft Exchange 服务器替代方案, 468

- Midnight Commander 的优势 (Midnight Commander advantages of), 101
- 文件管理 (managing files), 76-77
- .mil, 482
- MIME/Base64, 241
- 脑力图谱 (mindmapping), 159
- minicom, 210
- Minix 文件系统, 308
- 镜像磁盘 (mirror disks), 357, 366
- mkdir, 576-577
- MDLDonkey, 297-298

- 调制解器向导 (Modem Wizard (YaST)), 208-210
- 调制解器拨号连接 (modems dial-up-connections)
- 拨号 (dial-up), 209-211
- 挂载点 (mount points), 208
- 测试连接 (testing connections), 210
- 超时 (timeouts), 209
- USE Linux 安装 (USE Linux installation, and), 27-28
- modinfo 命令, 432
- modprobe 命令, 432
- modprobe.conf, 69
- modprobe.conf 文件, 132

- 模块 (modules)
- Apache 模块 (Apache modules), 468-469
- 内核模块管理 (kernel modules, managing), 431-432
- Perl 模块 (Perl modules), 539-540
- mod_auth Apache 模块 (mod_auth Apache module), 467
- mod_perl Apache 模块 (mod_perl Apache module), 473-474
- mod_php4 Apache 模块 (mod_php4 Apache module), 474
- mod_python Apache 模块 (mod_python Apache module), 474
- mod_ruby Apache 模块 (mod_ruby Apache module), 474
- mod_vhost_alias Apache 模块 (mod_vhost_alias Apache module), 496

- 监控系统 (monitoring systems), 411
- GKReim, 413-414
- KSysGuard, 412
- KwikDisk, 413
- 监控用户活动 (monitoring user activity), 348-349
- mount 命令, 318
- 挂载 (mounting)
- CD 硬盘 (CD drives), 59-60
- DVD 硬盘 (DVD drives), 59-60
- 文件系统 (file systems), 317
- 救援系统硬盘 (hard drives from rescue system), 370-371
- stab, 319-320
- 设备配置 (devices, configuring), 48-49
- KDE 

## O

- Python 中的对象 (objects in Python), 543
- 字节 (octets), 444-445
- OES, 590

- 软件 (Applizware), 154
- GNOME 办公 (GNOME Office), 151-152
- 韩文 Office (Hancom Office), 154
- KOffice, 148-149
- 在线文档 (online documentation), 162
- OpenOffice.org, 141-142
- 自动补全模式 (autocompletion mode), 147
- 配置 (configuring), 144-146
- 安装 (installing), 143

- 新源聚合器 (newsfeed aggregators), 259
- 新闻组 (newgroups), 615-616
- 新闻阅读器 (newsreaders). 另见 Uosit

- 在线菜单 (Online menu), 17
- open 命令 (open command (FTP)), 290
- 开放企业级服务 (Open Enterprise Service (OES)), 590
- Open-SSH 工具, 422
- OpenGL 引擎, 181
- Open 组 (Opengroup (Ogo)), 269
- OpenOffice.org, 11, 142

- KNode, 235
- 独立 GUI, 275-278
- 基于文本的 (text-based), 278
- 网络文件系统 (NFS (Network File System)), 308, 453-454
- 网络接口卡 (NICs (network interface cards)), 447-451
- NLD (Novell Linux 桌面), 91
- nmap 映射 (nmap mapping), 420-421
- 非交互式文件传输 (noninteractive file transfers), 292
- Novell GroupWise, 268
- Novell Linux 桌面 (NLD), 91, 590
- Novell 网站 (Novell websites)
  - 酷社区 (Cool Communities), 177
  - novell.com, 17
  - 订阅支持组 (support groups, subscribing to), 376
- nslookup 命令, 487

## OpenSSH
- OpenSSH, 292-293
- OpenSUSE 项目, 12-13
- opensuse.org, 593

## Opera
- 新闻聚合器, 259
- 概述, 226
- 操作符 (Perl), 537-538
- /opt 目录
  - 描述, 70
  - 独立的挂载点, 31
  - 优化, 561
  - 硬盘, 566-567
  - 硬盘驱动, 568-571
  - MySQL, 531-533
  - PowerTweak, 564-565
  - 查询 (SQL), 533-534
  - 服务, 562-563
- .org 域名, 481
- 组织架构图
  - Dia, 159
  - Kivio (KOffice), 149
  - 孤儿软件, 592
  - Outliner (Eclipse Workbench), 502
  - Outlook 风格邮件客户端, 229-234
- 输出重定向, 131
- 所有者, 83-84
- 使用 YaST 安装和删除软件
  - 模块, 375-376
- 使用 YOU (YaST 在线更新)
  - 模块, 384-388
- 在线列表, 594
- 数据包写入 (DVDs), 173-174
- 数据包 (IP), 444-444
- 绘图程序, 154-155
- PAM (可插身份模块), 346-347
- 饼 查看器, 275-276
- Parrot 解释器, 541
- 硬盘分区, 29-31
  - 添加分区, 36, 313-314
  - 更改文件系统, 36
  - 创建分区, 313-314
  - 删除分区, 314-315
  - 编辑分区, 314-315
  - 加密分区, 315-317
  - 扩展分区, 312
  - fdisk 实用, 311
  - 行引用, 32, 595-606
  - 只读、挂载, 331
  - 推荐的分区大小, 29
  - 调整分区大小, 315
  - 交换分区, 30
- passwd 命令, 70, 88
- 密码, 344
- Apache, 466-468
  - 创建, 37-38, 88
  - 重要性, 422
  - PAM (可插身份模块), 346-347
  - 选择, 345

## P
- P2P, 295
  - BitTorrent, 299-301
  - Napster 风格, 296-298
- Package Explorer (Eclipse Workbench), 502
- 包安装界面, 37
- 软件包
  - 定义, 552
  - 安装
    - 使用 APT (高级包工具), 388-391
    - 在线引用, 395-396
    - 使用 Red Carpet, 391-393
    - RPM (红帽包管理), 382-383
- 补丁
  - 使用 YOU 下载, 384
  - 内核, 434-436
- PCMCIA 卡, 57
- dd-ksh shell, 78
- PDA (个人携电脑), 154-155
- PDF 文档, 122-124
- PECL 库, 552
- 点对点文件传输, 295
  - BitTorrent, 299-301
  - Napster 风格, 296-298
- Procmail, 637
- 性能调优, 561。另见优化
- 外围区域 (KDE 控制中心), 105
- PortSentry, 425
- 位置参数, 136-139
- Perl
  - 与 Python 比较, 535
  - CPAN 模块, 539-540
  - 模块, 539-540
  - 在线引用, 544-545
  - 操作符, 537-538
  - 概述, 536
  - 正则表达式, 538-539
  - 变量, 536-537
- Postfix
  - 替代方案, 267-269
  - 配置, 227, 263-264
  - PostgreSQL, 11
- Postscript 文件, 113-114
- 电源控制设置 (KDE), 105
- 电源管理, 55
  - 笔记本电脑, 56-57
  - KDE, 105
- perl 版本 Perl, 536
- Perl, 541
- 权限
  - 更改, 84-86
  - 目录权限, 86
  - 显示, 83
  - PowerDesk 5 管理器, 190
  - PowerTweak, 564-565
- PP (点对点协议), 206-207
  - pppd 守护进程, 207
- PPPoE
  - 概述, 82, 341-342
- 个人设置 (GNOME), 107
- 个人视频录制器, 174-176
- 视角 (java), 503
- Photoshop, 179-180
- PPPoE (通过以太网 PPP), 211
- PHP
  - 函数, 552
  - 阻塞, 548-549
  - 在线引用, 559-560
  - 概述, 547-548
  - 脚本, 549-552
- 演示程序
  - Impress (OpenOffice.org), 143
  - PHP 5, 552-553
  - phpBB, 255-557
  - phpGroup, 269
- Planmaker, 152-153
- 可插身份模块 (PAM), 346-347
- 打印机
  - 喷墨, 126
  - 多点设备, 125
  - 网络打印机, 121
  - 通过蓝牙, 57
- CUPS, 114-115
  - 默认设置, 121
  - 网络打印机, 121
- PNG (便携图形) 文件, 180
- 点对点协议, 206-207
- PTR (指针) 资源记录, 483
- 公共 IP 地址, 444
- put 命令 (FTP), 291
- PVRs, 174-176
- PySol, 181
- RAID 阵列, 357, 366-368
- Ramey, 139
- Raw 文件, 165
- RDBMS, 518
- 读取权限, 83-86, 341
- 只读分区, 331
- 实时通信
  - 即时消息, 285-286
  - IRC (互联网即时聊天), 284-285
  - 在线引用, 287-288
  - 视频会议, 286-287
- Really Simple Syndicate (RSS), 255, 259
- RealPlayer Gold, 166
- 重启命令, 66
- 重启, 42, 89
- 录制工具, 167
- Red Carpet
  - 命令行操作, 392-393
  - GUI 操作, 393
  - 查看已安装应用, 393
  - 安装, 391-392
- 红帽包管理。另见 RPM
- 重定向 (输入/输出), 131
- 引用
  - 类语句, 543
  - 与 Perl 比较, 535
  - IDE, 543-544
  - 缩进, 543
  - 交互式 shell, 543
  - 概述, 541-542
  - 变量, 542
  - 应用安装, 395-396
- 备份, 373
- 引导过程, 414-415, 595-606
- 协作工具, 287-288
- 跨平台计算, 199-200
- 数据库, 534
- DNS, 494
- 邮件, 242, 269-270
- 文件系统, 89
- 文件系统, 335
- 通用信息, 593-595
- 安装 SUSE Linux, 32, 595-606
- 连接, 219

## Q – R
- Quantum Plus, 245-253
- 查询 (SQL), 优化, 533-534
- 查询缓存 (MySQL), 532-533
- Quicker 文件, 导入, 155-156
- QuickStarter (OpenOffice.org), 144
- quit 命令 (FTP), 290
- RSS (互联网), 164-167
- RSS 卡, 配置, 49-50
- IP 地址分配, 607-611
- 内核, 440-441
- Linux 新闻, 594
- 多媒体, 183-184
- 网络, 456-557
- 组, 515-516
- 办公套件, 162
- 硬盘分区, 32, 595-606
- Perl, 544-545
- PHP, 559-560
- 编程, 514
- Root 用户, 900
- 搜索引擎, 594
- 安全文件传输, 303-304
- 安全, 607-611
- shell, 139-140
- shells, 89
- 系统管理, 595-606
- 文本编辑器, 90
- 关, 88-89
- 用户执行的任务, 87
- 用户删除, 27-88
- Rootkit Hunter, 426
- 路由器, 448-449
- RPM (红帽包管理), 382-383
  - 从源代码创建包, 510-514
  - 在 YaST 之外下载包, 383
- spec 文件, 511-513
- RSS (Really Syndication), 255, 259
- RSS/Atom 馈源, 235
- rug 实用, 392-393
- Runlevel 5, 404-405
- Runlevel Editor (YaST), 408-411
- 级别, 405
- Apache 运行时, 462
- 运行时错误, 439
- X Window System, 112
- 区域和可访问设置 (KDE), 105
- Perl 中的正则表达式, 538-539
- Reiser 文件, 13, 309-310
- 关系型数据库, 517-519
- 备份用移动存储设备, 357-358
- 删除命令 (CVS), 510
- 存储库 (CVS), 509-510
- 修复系统, 370-372
- 资源记录 (DNS), 483-492
- 资源使用, 581-582
- 启动 SUSE Linux, 43
- 还原点, 562
- 恢复 (YaST), 472-483
- 反向查找区域, 482-493
- Rich Site Summary (RSS), 259
- rm 命令, 86-87, 580-581
- rm 实用, 575
- rmmod 命令, 431
- Robertson, Michael, 245
- Root 域名 (DNS), 481
- Root 用户, 71

## S
- s 元字符 (Perl), 539
- Samba, 445-455
- samsung Connect, 268
- SANE, 160
- SATA 硬盘, 567
- SaX, 配置, 92-94
- /sbin 目录, 68
- 可缩矢量图形 (SVG) 文件, 180
- scalar (Perl), 536-537
- 扫描仪应用程序, 160
- 扫描仪
  - 配置, 49
  - CVS 支持, 160
- 屏幕保护
  - GNOME, 107
  - KDE, 104
- Scrib, 155-178
- script kiddies, 417
  - 创建, 37-38
  - 授予 Root 权限, 350-351
  - 登录为, 349
  - 在线引用, 90
  - 重启系统, 89

## Script-fu
- Script-fu, 179
- 脚本。另见各种脚本语言的危险, 418
- shell
  - 别名,创建, 133-135
  - 为变量赋值, 136
  - 自动化任务, 137-139
  - 内置变量, 135, 139
  - 注释, 135
  - 变为可执行, 135
  - 位置参数, 136-137
  - 特殊字符, 130
  - 存储, 132
  - 文字处理和, 132
- SCSI 磁盘收集器, 567
- SDPS 邮件协议, 264
- 搜索引擎, 594
- 权限, 342
- 安全 FTP, 292-293
- 安全
  - 攻击,理解, 418-419
  - 文件传输
    - 图形 FTP 客户端, 293-295
    - 在线引用, 303-304
    - 点对点, 295-301
    - 文本 FTP 客户端, 293-295
- gnutella, 421
- 攻击,恢复, 425-426
- KDE, 105
- MySQL 用户帐户, 524
- 网络服务, 455
- nmap 网络实用程序, 420-421
- 在线引用, 607-611
- Open-SSH 工具, 422
- 补丁,下载, 384
- PortSentry, 425
- 资源, 426-427
- Rootkit Hunter, 426
- Snort, 425
- SUSE 防火墙, 配置, 422-424
- SUSE Linux
  - 优化的, 587-589
  - 其中的文件系统, 13-14
- 帮助中心, 15-16, 592
- info 页面, 16
- Linux 文档项目, 17-18, 593
- Linux 用户组 (LUGs), 19, 594
- 邮件列表, 18-19, 593
- man 页面, 16, 593
- 在线支持, 17, 592
- 打印文档, 14-15
- 历史, 9
- 安装程序, 13
- 登录/输出, 66
- 登录/输出, 42-43
- 概述, 9-10
- SUSE Linux 硬件数据库, 24-26
- SUSE Linux 安装
  - BIOS 设置, 34-35
  - 默认设置, 35
  - 与 Windows 双系统启动, 29-30
  - 硬件考虑
    - 内置外设, 28
    - 针对 Window 系统, 41
    - 传统硬件, 26-27
    - 软件模型, 27-28
  - USB 设备, 28
  - Internet/网络连接, 38-39
  - 笔记本电脑, 26
  - 在线参考, 32, 595-606
    - 硬盘分区, 29-31
  - 规划, 22-23
  - Root 用户, 37-38
  - 软件包, 37
  - 启动, 35
  - 系统要求, 23-26
  - 时区, 36
  - 故障排除, 45-46
  - 用户, 40
- SUSE Linux Professional, 10-12, 33
- SUSE Linux Professional CD, 启动, 370
- SUSE 用户组, 19
- use-linux-e 邮件列表, 18
- use.com, 17
- SUSEConfig (Apache), 463-465
- use 命令, 15
- useWatcher, 97, 386-387
- SVG (可矢量图形) 文件, 180
- 交换分区, 30
- 切换 时间, 51
- 切换到待机模式, 57
- 切换, 237-324
- 符号链接, 68
- 同步博客, 258-259
- sysctl 工具, 439-440
- 系统管理工具 (KDE), 106
- 系统备份 (YaST), 359-362
- 系统组, 342
- 系统菜单 (GNOME), 106-107
- 系统恢复 (YaST), 370-372
- 系统设置 (GNOME), 107
- 系统状态, 399
- 系统运行级别, 462
- 概述, 408
- 系统用户, 341
- 监控工具, 411-744
- 救援, 370-372
- 元字符 (Perl), 539
- 标签页浏览, 222
- 标记图像文件 (TIF), 180
- tail 命令, 581
- 污染的, 663
- tail, 182
- 磁带驱动器, 359

- 上行端口

- tar 文件, 备份, 363-364
- TCP/IP, 445
- IP 数据包, 433-444
- localhost 接口, 205-206
- NAT, 447
- 子网掩码, 446
- tcsh shell, 75-78
- 电视, 174-176
- 模板 (OpenOffice.org), 144
- TeX 发布工具, 123
- 文本编辑器, 79
- Emacs, 81-82
- Gvim, 81
- JEdit, 82
- KNodes, 235
- Kvim, 81
- vi, 80
- vim, 80-81
- tin 新闻阅读器, 278
- tk IRC , 284
- TLS, 482
- TEF (传输封装) 文件, 240
- 令牌环网络, 447
- TomCat, 475
- top 命令, 581-582
- 顶级域名, 480-482
- 拓扑，网络, 447-488
- Torvalds, Linux, 9
- tree 命令, 67
- 内内核故障排除, 438-439
- 救援系统, 370-372
-  卡模块 (YaST), 49-50
- 调优, 257-258
- 设置为一, 570
- UDF (通用磁盘格式) 系统, 308
- UDP (用户数据报协议), 443-444
- UIDs, 使用 YaST, 340
- umount 命令, 318
- 卸载文件系统, 318
- 通用时间, 51
- update 命令 (CVS), 510
- 更新管理器 (Eclipse), 501
- 更新应用程序
  - 使用 APT (高级包工具), 388-391
  - 使用 Red Hat, 391-393
  - 使用 RPM (红帽包管理), 382-383
  - 使用 YaST, 375-377, 384-388
- 上行端口, 448
- 文本 客户端, 290-293
- 文本新闻阅读器, 278
- Textmaker, 152
- THE (Shell 编辑), 82
- 主题
  - GNOME, 107
  - KDE, 105
  - ThinkFree Office, 154
  - 节流, 474
- Web 服务器, 474
- Thunderbird
  - 概述, 237
  - 垃圾邮件, 266
- 标记图像文件 (TIF), 180
- 时间, 50-52
- 时区, 36

## 设备

- 备份, 357-358
- 打印机, 226
- SUSE 安装，以及 28
- /var/log/messages, 45-46
- 矢量绘图程序
  - Draw (OpenOffice.org), 143
  - Karbon14 (KOOffice), 149
- Very Secure FTP, 301-303
- vi 编辑器, 80
- 视频 (PVRS), 174-176
- 声卡，配置, 163-164
- 视频文件, 186
- Video for Linux (V4L) API, 174
- 视频组, 342
- 视频会议, 286-287
- 查看启动日志模块 (YaST), 405
- View Your Mind, 159-160
- vim 文本编辑器, 81
- vim 网站创建器, 248
- 虚拟域名, 264
- Usenet, 272
- 邮件客户端, 274-275
- Google Groups, 273-274
- GUI 新闻阅读器, 275-278
- KNode, 235
- 公共新闻服务器, 273
- 文本新闻阅读器, 278
- User Data Protocol, 443-444
- 用户选项, 522
- 用户变量, 135
- uradd/del 命令, 88
- UserDir 指令 (Apache/2/httpd.conf), 465
- 活动, 348-349
- 在 SUSE 安装期间, 28
- 在 YaST 中, 338
- 删除, 88
- de-MySQL，安全, 524
- 密码。参见 Root
- 系统用户, 341
- 带有 WordPress, 554
- 虚拟主机, 469-472
- 虚拟机, 187-200
- 虚拟计算, 219
- /usr/src/, 430
- 描述, 70
- 挂载点, 31
- /root, 663
- 病毒, 264
- vmstat, 350-351
- vmware, 193-194
- 卷, 320
- vsftpd, 301-303
-  Video for Linux, 174

## 646 实用程序

which utility, 323
白皮书, 593
Wiki

- 无线网络, 448
- 连接, 217-218
- 安全保护, 421-422

文字处理器

- 定义, 13
- Novel's Cool Communities 网站, 17
- WikiEngines, 279
- Wikipedia.org, 279
- Wikis, 279-281
- 通配符, 130
- Win4LIn, 191-192
- 窗口管理器, 107
- 登录时选择, 108
- FVMWM, 108-109
- IceWM, 111-112
- 运行原因, 108
- WindowMaker, 109-110

- AbiWord (GNOME Office), 151-152
- Kword (KOOffice), 148-151
- Textmaker (SoftwareOffice), 152
- Writer (OpenOffice.org), 142, 146-147
- WordPerfect, 154
- WordPress, 257, 553-555
- Workbench (Eclipse), 501-502
- Wspaces Clip (WindowMaker), 109
- Wprefs 实用程序, 110
- Writer 权限, 83-341
- Writer (OpenOffice.org), 142, 146-147
- Writer/Web (OpenOffice.org), 243-244

- WindowMaker, 109
Windows
- 应用程序，安装
- 在 VMware 下, 195
- 在 Win4Lin 下, 192
- 在 Wine 下, 180-190
- 备份, 355
- 双启动 SUSE Linux, 29-30
- 文件系统, 30, 186, 308
- 字体，包括 Linux, 106
- 安装 Windows 应用程序
- 在 VMware 下, 195
- 在 Win4Lin 下, 192
- 在 Wine 下, 189-190
- 运行应用程序
- 跨平台计算
- 误解, 187
- 使用 Crossover Office, 190
- 使用 VMware 下, 193-195
- 使用 Win4Lin 下, 191-292
- 使用 Wine 下, 187-190

## X - Y - Z

- X 服务器, 11
X Terminal, 66
X Window System

- 客户端/服务器模型, 91
- 配置, 92-94
- 硬件, 41
- 登录, 94
- 非线性引用, 112
- 目的, 92
- 窗口管理器, 107-112
- Xchat IRC 客户端, 284
- XEmacs 文本, 82
- n 虚拟虚拟机监视器, 196, 199
- XF86Config 文件, 92
- XFS 文件系统, 310
- Ximian, 11, 91, 234
- Xine, 174-176

- xineted
- 配置安全文件传输, 301-392
- 保护网络服务, 455
- Xitami, 474
XML
- Abiword 文档, 152
- PHP 5 支持, 552
- XMMS (X 多媒体系统), 164-166
- xterm, 66

- Samba, 454-455
- Windows 音视频 (WAV) 文件, 166
- Wine, 187-190
- WineFile 文件管理器, 190
- Winer, 259
- WinTools 包, 188
- 无线卡，配置, 217-218

## Yahoo Messenger, 285 YaST

- 安装 Anuta, 507
- 配置 Apache, 463-465
- 日期/时间设置, 50
- 配置 DHCP, 452
DNS

- 客户端配置, 483-486
- 服务器配置, 489-493
- 电子邮件账户，配置, 263-264
- 文件系统管理, 311-312
- 创建分区, 315
- 删除分区, 315
- 编辑分区, 314-315
- 加密分区, 315-317
- 调整分区大小, 315

- 分组，添加, 342-343
- 配置硬件
- CD 驱动器, 59-60
- DVD 驱动器, 59-60
- HDC 设置, 46-47
- 信息报告，显示, 46
- 初始化硬件, 449
- njoysticks, 47
- 键盘布局, 48
- 鼠标设备, 48-49
- 打印机, 115-19
- TV 和收音机卡, 49
Internet 连接
- 拨号, 207-210
- DSL, 215
- KOffice 安装, 149
- 笔记本电脑，配置, 56-59
- Mailman，配置, 282-283
- 概述, 10
- 安装和删除软件模块, 375-376
- YaST 在线更新, 348-388
- 分区硬盘, 30-311
- 电源管理, 55
- RAID 阵列，设置, 368
- 恢复文件, 370-372
- 从 shell 运行, 78-79
- 声卡，配置, 164
- SUSE Linux 安装
- 默认设置, 35
- 软件包，安装, 37
- 系统备份, 359
- Root 用户，创建, 88,338
- 更新应用程序, 386
- Zip 驱动器, 355-357
- zone (DNS), 482-483
- Zope 应用程序, 491
- ZWiki, 279
- Zwiki 引擎, 279

如何让这个索引更有用？
publishing.com.

DVD 包含了 SUSE Linux 10.0 的完整二进制版本的五张 CD。

### 娱乐
- FreeCiv
- KDE 游戏集
- Maelstrom
- SuperUX
- Tux Racer

### 文档（继续）
- 虚拟化
- 在线手册

### 数据库（继续）
- Merchant
- MySQL
- Recall
- SQLite
- UnixBC

### 多媒体（继续）
- cdparanoia
- CDRDAO
- cdrec
- Cecilia
- dvd-rw
- FluidSynth
- K3b
- Kaffine
- KDE Multimedia
- Kino
- Mksofofs
- RealPlayer
- Rymbox
- Sound
- Totem
- Xine

### 语言
- Bison
- Flex
- GCC
- Guile
- Java
- Mono
- Perl
- Ruby
- Tcl
- TK

### 硬件
- ALSA
- Bluetooth 和库
- CUPS
- 打印机过滤器
- GNOME Architecture
- gPhoto
- GTK+
- hdparam
- KDE Digital Call
- Kooka
- klips
- LIRC
- mgetty
- motv

### PCI 实用程序
- SCSI 工具
- sendfax
- 无线工具
- Xsane

## 编辑器
- GNU Emacs
- AUC Text
- vim
- Gedit
- JOE
- Mined
- PicoTex
- XSLIDE

### 文件实用程序
- GNU Find
- KDE 实用程序
- Midnight Commander
- Nautilus

### 工具
- Ant
- Automake
- cscope
- CVS
- DDD
- ElectricFence
- Expect
- GDB
- Libtool
- Ltrace
- Make
- Stacey
- Subversion

### 网络
- Apache 2
- BIND
- BitTorrent
- Bogofiler
- Curl
- Dante
- DHCP 客户端/服务器
- Dirnmgr
- EPIC
- Epiphany
- Ethereal
- Fetchmail

## 网络（继续）

## 科学

## 基准测试

## GUI（继续）
- mICQ
- Mozilla
- Mozilla Firefox
- MRTG
- mutt
- Netcat
- OpenLDAP
- Opera
- PHP
- Pine
- PostFix
- PPG
- PTTP
- procmail
- Quagga
- RADVD
- rDesktop
- spassassim
- Squid
- SuFirewall2
- Telnet
- Tomcat 5
- Wget
- Whois
- Xineted

- Bc
- Convert
- FFTW
- GNOME Calculator
- Xphem

- BonnieDBench
- bootsplash
- gfbox
- GRUB
- memtest86
- preload
- SYLINUX

- Evince
- FVWM 2
- Gail
- GNOME 2
- KDE 3
- Metacity
- Window Maker

## 安全
- 高级入侵检测环境 (AIDE)
- AntVir
- chkroot
- PPG
- OPI
- 权限

## 管理
- checkmedia
- kiostool
- LiMal

## 控制台
- Cabtextract
- FBSet
- gpm
- initocs
- kbd

## 监控
- procinfo
- props
- psmisc
- sensors
- Sitar

## 遥测
- GNOMeting
- KPhone

## 守护进程
- ACPID
- at
- autofs
- cron
- Fam
- Galago
- Gamin

## 软件包
- apt
- deltarm
- Kyum
- RPM
- Yum

## Text
- Aztecs
- dicts
- diffstat
- diffutils
- Enchant
- Festival
- GNU awk
- GNU grep
- Ispell
- Less
- GNU patch
- Quilt
- Wiggle

## 模拟器
- WINE

## 壳
- ash
- bash
- sash
- tsch

## 办公
- AbiWord
- Evolution
- Gnumeric
- OpenOffice.org
- Planmaker
- Planner
- Tomboy

## 音频守护进程
- esound
- jack
- Window Maker SoundServer

## 发布
- Adobe Reader
- Cedilia
- Conglomerate
- Docbook Edition 4.x
- DVI Units
- Encript
- Gnome Ghostview
- Effect
- JadeTex
- Lacheck
- LaTeX2HTML
- LyX
- MuseXT
- Openjade
- Tex-Guy
- Xalan
- Xerces

### 文档
- BIND 文档
- GNU C Library HTML Documentation
- GNOME 2.x Desktop Linux and POSIX manual pages
- Project man pages
- QT 3 Document Kit and man pages
- Samba 文档
- SuSE Help System

### 力
归档
- Bzip
- cpio
- GNU Zip Utilities
- conserve
- Pack Program
- Pax
- Star
- Unzip
- Zip

### 数据库
- db-util
- Knode
- GNU Data Access (GDA) Library
- PostgreSQL C++ Client Library

### 多媒体
- ALSA Tools
- amaroK
- acts
- aumix
- banshee

- htop
- imap
- INN
- iproute2
- iptables
- iputils
- Lynx
- Mail
- MediaWiki

# SUSE™ Linux®10 深度解析

《SUSE Linux 10 深度解析》全面介绍了 SUSE Linux 的最新版本，它是全球最受欢迎且功能最完整的 Linux 发行版之一。

本书提供了关于安装、使用和管理 SUSE Linux 的详细信息。你将学习如何释放 SUSE Linux 中海量软件产品的潜力，使其能够作为桌面电脑、专业工作站或强大的服务器来使用。

《SUSE Linux 10 深度解析》涵盖了广泛的内容：从日常所需的软件——如电子邮件客户端、Web 浏览器以及包括 OpenOffice.org 办公套件在内的生产力软件——到配置和管理各种网络和服务器产品，例如 Apache Web 服务器和 MySQL 数据库。

此外，本书还详细介绍了 SUSE 宣称的管理工具、Web 编程、网络技术，以及如何从众多的图形界面和桌面环境（包括 KDE 和 GNOME）中进行选择。

Michael McAllister 一直致力于 SUSE Linux 5.3 版本的工作。他是 Mijenix 的技术支持人员，同时也是威斯康星州麦迪逊 Istmus 报的技术记者、自由撰稿以及 Ontrack 的技术作家。他的技术文章发表在《Linux Business》、《Java Developers Journal》、《Internet Voyager》和《Istmus》上。他曾任 NetWork 系统管理员，并具有其他 Novel 产品的经验。他的专业会员身份包括技术传播学会、密尔沃基 Linux 用户小组和国家作家联盟。

- 根据你的计算需求规划 SUSE Linux 安装计划
- 配置并使用 X Window 系统、Linux 图形界面，以及 Linux 的两个主要桌面环境——KDE 和 GNOME
- 运行 OpenOffice 和其他生产力工具
- 创建你自己的网站和网络博客
- 管理内核及其模块
- 设置网络
- 运行 Apache Web 服务器
- 运行 LAMP Web 编程套件：Linux、Apache、MySQL 以及脚本语言 Perl、Python 和 PHP
- 播放音乐、视频和游戏
- 保留现有的 Windows 安装以实现双启动

# DVD 光盘内包含：

- SUSE Linux 10.0 二进制发行版——等同于 5 张 CD——内装了数千个应用程序和实用，包括：
- 最新版本的 Apache Web 服务器
用于基于 Windows 文件和打印机共享的 Samba
- 免费的 OpenOffice.org 办公套件
- 桌面游戏
- 数百个额外的程序、实用程序和开发工具

| 类别 | 操作系统/Linux |
| :--- | :--- |
| 涵盖范围 | SUSE Linux 10.0 Professional/openSUSE 10.0 |
| 用户级别 | 中级–高级 |

$49.99 美国
$69.99 加拿/£35.99 英国（含增值税）
ISBN 0-6722-3276-0

封面版权所有 © ISAS
