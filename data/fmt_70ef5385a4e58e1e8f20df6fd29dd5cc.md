
### IN THIS CHAPTER

- What Is Ubuntu?
- Ubuntu for Business
- Ubuntu in Your Home
- 64-Bit Ubuntu
- Ubuntu on the PPC Platform
- Ubuntu on Multi-Core Machines
- Getting the Most from Ubuntu and Linux Documentation
- Ubuntu Developers and Documentation
- Reference

甚至还有 Edubuntu，这是一个专门为教育和学术机构设计的 Ubuntu 版本。它们都共享一个共同的代码库，每个版本都附带一张安装光盘，使其易于重新分发 Ubuntu 副本。事实上，如果你想要额外的副本，Ubuntu 实际上会免费寄送光盘。目前，你只能收到 Ubuntu 发行版，但你可以申请 x86 或 PPC 版本，每个包装都包含一张安装光盘和一张 Live CD。正在努力通过相同的光盘分发计划提供 Kubuntu 发行版。

### About Debian

如前所述，Ubuntu 建立在 Debian Linux 之上并借鉴了许多功能。Debian 本身是 Linux 发行版中最古老的之一，其开发可追溯到 1993 年。Ian Murdock 建立了 Debian 宣言，呼吁对 Linux 发行版进行开放和协作式开发，并使用自己的名字和他当时女友、现任妻子 Debra 的名字来命名。

Debian 发行版通常被认为是最稳定和最安全的发行版之一。它也是完全非商业化的，有严格的指导方针以确保只有真正的自由软件（在言论意义上）才能通过 Debian 获取。

拥有如此坚实的基础，其他发行版以 Debian 为基础也就不足为奇了；截至撰写本文时，约有 52 个发行版可以追溯到 Debian 的血统。流行的发行版如 Linspire、Xandros，以及非常有用的 Knoppix Live CD 都以 Debian 为核心。

Linux 成功的理由有很多。也许最重要的一点是它满足了真正的需要。人们不仅可以按原样部署软件，而且如果需要以特定方式工作，他们可以与源代码，即软件的构建基块一起工作，以操纵程序本身并改变其工作方式。这种开放性在软件世界中是闻所未闻的，但它是 Linux 的关键优势。Linux 在服务器机房的早期进展中运行了诸如 Web、电子邮件和文件服务器等应用程序。随着各种发行版以及应用程序和窗口管理器的持续开发，Linux 在桌面上变得越来越常见。

UNIX 在 20 世纪 70 年代问世时也非常流行。然而，限制性的许可和后来被称为 UNIX 战争的东西扼杀了重大的开发和标准化，导致微软通过后门进入并以远逊于 Windows NT 的产品进入。如今，微软正面临真正的挑战，以阻止 Linux 主导服务器市场。

归根结底就是这样：你手中的软件如果商业开发的话估计价值 19 亿美元。Linux 中存在超过 5500 万行源代码，来自世界各地的数千名开源开发者的集体开发工作直接贡献于 Linux。

如今，看到公司转向 Linux 的报道已相当常见。事实上，更可能是政府机构寻求摆脱

摆脱了雷德蒙德的掌控。随着更多选择和显著的成本节约，越来越多的企业意识到 Linux 是明智的选择。如今，你很难找到一家公司不以某种形式使用 Linux，即使只是作为路由器或防火墙的机器。

> **NOTE**
>
> Linux 项目、努力和合作伙伴的名单读起来就像软件行业的 *名人录*：亚马逊、Ameritrade、Borland、Computer Associates、Dell、Hewlett-Packard、IBM、Oracle 和 SAP 只是使用 Linux 的一些企业级参与者。Linux 也是关键组成部分，并占据了所有大型厂商服务器硬件销售中不断增长的份额，例如 IBM、Hewlett-Packard 和 Dell。成本节约是显著的，尤其是考虑到 Linux 在刀片服务器环境中的使用，其中 1 个机箱可容纳 14 台服务器。仅在许可费用上节省的资金就达数千美元，与 Windows 相比。

## What Is Ubuntu?

Ubuntu 是 Linux 世界中的一个新发行版。然而，尽管它仅在 2004 年中才出现，Ubuntu 已迅速在新手和资深用户中流行起来。原因有很多，但可以归结为易用性和谨慎的开发以确保最大兼容性。Ubuntu 的一个关键信念是“一切都应该只是工作”，在很大程度上这是正确的。Ubuntu 本身基于 GNOME 窗口管理器，配备标准的应用软件套件以及访问来自更广泛 Debian 软件宇宙中 17,000 多个应用程序的手段。

正如你在本章中学到的那样，Ubuntu 是互联网上最新、最快速发展的 Linux 发行版之一。在这里，你将看到为什么 Ubuntu 是各种计算环境的良好选择，以及当它与最新 Linux 内核提供的进步相结合时，它如何为从学术、家庭、小型企业到企业和大型企业用户提供支持的巨大范围。

### Inside Ubuntu

Ubuntu 发行版的拷贝只需要一张 CD，在 Linux 世界中这已是罕见。在这张 CD 上，你可以获得启动所需的一切，包括应用程序软件以及几个程序，可让你直接访问通过 Debian 软件宇宙提供的 17,000 多个软件项目。Ubuntu 也提供 DVD 安装，其中包含数百个额外的软件包，可通过 `Synaptic` 安装。

Ubuntu 提供了一个基础或核心框架操作系统和桌面，完全由自由软件组成。Ubuntu 包含 Human 桌面主题，并且默认随附 GNOME 窗口管理器。如果你更喜欢 Xfce 甚至 KDE，你可以轻松获取并安装 Xubuntu 或 Kubuntu，两者都以 Ubuntu 发行版为核心，但使用替代窗口管理器。

从单张 CD 到庞大的软件仓库，你可以期待花费数小时探索 Ubuntu 提供的软件。`synaptic` 包管理器使安装和维护软件变得轻松，只需了解有哪些可供选择即可。

NOTE

有关 GNOME 和 KDE 的更多信息，请阅读第 6 章“X Window System”。

Ubuntu 提供 X Window System 的最新版本及其服务器 `X11R7`，具有改进且集成的字体处理。Linux 桌面从未如此出色，你在浏览网页、使用 Ubuntu 提供的十几种文字处理器和文本编辑器之一，或在终端窗口的命令行中查看文本时都会注意到差异。

Ubuntu 还附带一套管理和管理工具，使你能够管理系统的每个部分。

### TABLE 1.1 Ubuntu Graphical Administration Tools

| Name | Description |
|---|---|
| `network-admin` | 创建、编辑和管理网络设备 |
| `synaptic` | 管理软件和更新 |
| `gnome-cups-manager` | 配置本地和网络打印机 |
| `users-admin` | 管理用户和组 |
| `update-manager` | 提供一键访问系统更新 |
| `disks-admin` | 处理和配置连接的磁盘 |
| `gnome-language-selector` | 配置 Ubuntu 使用众多语言之一 |
| `services-admin` | 管理系统服务 |
| `shares-admin` | 使用 Samba 和 NFS 创建和管理共享目录 |
| `system-config-language` | 设置系统语言 |
| `gnome-mouse-properties` | 配置鼠标类型和功能 |
| `gnome-system-monitor` | 监控系统活动以帮助故障排除和维护 |

Ubuntu 包含 Internet 程序，如 Mozilla 的开源网页浏览器 Firefox，以及生产力应用程序，如 Ximian 的 Evolution（邮件、联系人和日历客户端）和 OpenOffice.org（与 Microsoft 兼容的开源办公套件）。你会在本书的 DVD 上找到这些以及更多应用程序。

其他主要功能包括最新 GNU `gcc` 编译器系统的包含，支持 C/C++ 语言程序开发。你还获得了 Apache Web 服务器的最新版本，以及 Common Unix Printing System（`CUPS`），它支持超过一千种不同的打印机。

根据 Ubuntu 社区，Ubuntu 计划至少每两年升级一次。实际上，由于开源开发人员的工作从未停止，发行版的开发从未停止

为 Ubuntu 提供软件包升级、安全更新和错误修复。Ubuntu 的免费在线升级系统可通过 Internet 使用。借助 Debian 的强大功能，Ubuntu 不同版本之间可直接升级。

作为 Ubuntu 用户，您可以使用各种命令和软件管理工具随时获取系统的最新软件：

- **`synaptic`**—强大的 `apt-get` 图形前端，`synaptic` 使您能够轻松浏览并快速从 Ubuntu/Debian 仓库安装或获取软件。
- **`aptitude`**—命令行工具 `aptitude` 速度极快且功能非常多样化，可轻松在发行版之间升级。推荐使用它来替代旧的 `apt-get` 工具。
