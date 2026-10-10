

**提示**：如果您希望在使用不同的 Linux 发行版时获取最新功能，请比较上面显示的版本号。Debian、SUSE 和 Fedora 等 Linux 发行商为其发布版本关联的版本号和名称可能是任意的。通过比较它们正在使用的内核、KDE 和 GNOME 桌面以及 GNU 编译器的版本，您可以判断哪个发行版实际上具有最新的功能。

以下章节描述了 Fedora 8 的主要新功能（除了上述基本组件的最新版本之外）。

### 获取自定义 Fedora 版本

Fedora 过去是以一组 CD 或包含所有可安装 Fedora 软件包的 DVD 形式发布的。最初在 Fedora 7 中新增的用于创建自定义软件库（Pungi）和自定义 Live CD（livecd-creator）的结果，正在 Fedora 8 中以日益增长的自定义版本集合的形式逐渐成熟。

Fedora 的自定义版本是 CD、DVD 或 USB 闪存盘镜像，可以作为 Live CD 和/或 Fedora 安装程序运行。官方的 Fedora 版本包括：

- **Fedora DVD** — 包含约 2.9GB 的桌面、服务器和软件开发软件包横截面，类似于过去 Fedora Core 中的内容。
- **Fedora 桌面 Live CD (GNOME)** — 从这个单独的 700MB Live CD，您可以运行 GNOME 桌面的 Fedora 8 系统。桌面上的安装图标随后允许您将该桌面系统安装到硬盘上。（此 CD 随本书附带。）
- **Fedora 桌面 Live CD (KDE)** — Fedora 通过提供 Fedora 8 的 KDE 桌面 Live/安装 CD，向 KDE 表达了支持。与 GNOME 桌面一样，您可以选择安装图标将 KDE 桌面系统安装到硬盘上。
- **全部 DVD 套装** — 包含整个 Fedora 8 仓库（超过 8GB）的“全部”双 DVD 套装预计在 Fedora 8 发布后不久生产。此套装适用于希望拥有 Fedora 8 中所有可安装软件包的人。（随本书附带的 DVD 包含两个全部 DVD 的大部分内容，重新泵送到大容量 DVD-9 上。）

随本书附带的 GNOME 桌面 CD 和几乎全部 DVD 适用于标准的 32 位 PC（i386）。如果您需要在 PowerPC（PPC）或 64 位 PC（X86\_64）计算机架构上安装 Fedora 的媒体，您可以使用 BitTorrent（http://torrent.fedoraproject.org）或官方 Fedora 公共镜像站点（http://mirrors.fedoraproject.org）下载这些媒体的 ISO 镜像。有关如何使用和从这些不同媒体安装 Fedora 的信息，请参阅第 2 章。

非官方的自定义版本也可从自定义版本页面（http://fedoraproject.org/wiki/CustomSpins）获取。目前已经有 Fedora Live 开发者版、游戏版、艺术版、Xfce 桌面版和电子实验室版。（术语 spin 指的是从 Fedora 软件仓库编译的软件组合，结合成一个或多个可启动镜像（通常适合放在 CD 或 DVD 上）的形式，允许您实时运行或安装该软件集合。）

### 创建自己的版本

Fedora Project 用于构建软件包和创建 Live CD 及安装 CD 的相同工具本身也随 Fedora 分发。这意味着任何人都可以使用这些工具创建自己的安装包集合，然后将这些包集合转换为他们自己的软件库。使用这些软件库，您可以创建自己的 CD 或 DVD 镜像，以便稍后安装或实时运行。

Pungi（http://fedoraproject.org/projects/pungi）是为 Fedora 8 创建的项目，用于构建 Fedora 系统本身。pungi 软件包包含 pungi 命令和相关配置文件。您可以使用 pungi 命令制作自己的安装树，从而生成可安装的 ISO 镜像。

Fedora Live CD 项目（http://fedoraproject.org/wiki/FedoraLiveCD）生产了用于从 Fedora 软件仓库构建您自己的 Live CD 的工具。创建这些 Live CD 的主要工具称为 livecd-creator。有关使用 livecd-creator 的信息，请参阅 Live CD HOWTO（http://fedoraproject.org/wiki/FedoraLiveCD/LiveCDHowTo）。

Fedora 8 中 livecd-creator 的一个不错的附加功能是，您可以创建 kickstart 文件（在第 2 章中描述）来指导 Live CD 的创建。这意味着您用于使用 anaconda 自动执行安装的相同格式也可以用于保存创建 Live CD 时使用的软件包列表和其他设置。

### GNOME 在线桌面

通过将 Big Board 侧边栏项目与您最常使用的在线服务（如 Facebook、Moshupshot、YouTube、Netflix 等）分组功能相结合，GNOME 在线桌面项目向 Web 连接桌面计算的未来迈出了重要一步。您首先设置 Moshupshot 的帐户（以收集您的个人在线服务）和 GNOME.org 的帐户（以收集有关您使用的应用程序的信息）。然后登录到您的在线桌面，即可从 GNOME 桌面访问您所有的个人文件、应用程序和在线服务。虽然在线桌面仍被视为实验性功能，但它已经非常好玩。

### Infinity 外观和 Nodoka 主题

在 Fedora 8 中，Fedora 桌面、启动屏幕、登录屏幕、背景和其他视觉元素的外观已使用新的 Infinity 外观（http://fedoraproject.org/wiki/Artwork/F8Themes/Infinity）和 Nodoka 主题（http://fedoraproject.org/wiki/Artwork/NodokaTheme）大大简化。

### PulseAudio 声音系统

PulseAudio 声音系统（www.pulseaudio.org）已取代 ALSA 成为 Fedora 使用的默认声音系统。通过提供插件，PulseAudio 可以为期望使用 ALSA 或其他 Linux 声音系统的音频应用程序提供接口。

### Cocomac 工具用于获取编解码器

Cocomac 工具提供了一种获取合法软件的方法，用于播放 MP3、Windows Media、MPEG4 和其他因软件专利而无法与 Fedora 自由分发的多媒体软件。使用 Cocomac，您可以连接到 Fluendo.com 站点并下载免费的 MP3 解码器或购买其他多种多媒体编解码器。

> **注意**：Cocomac 的加入揭示了一个所有 Linux 发行版都面临的重大问题：如何向需要或想要非自由软件的人提供它。帮助将用户与商业软件供应商联系起来，已经引发了关于 Fedora 应如何处理该问题的许多问题。应以什么标准让一个供应商获得比另一个供应商更特殊的待遇？Fedora 应如何控制这些供应商的影响力？例如，如果一个供应商试图破坏与其支持的产品相竞争的应用程序怎么办？虽然目前还没有完美的答案，但在此期间，至少有一个解决方案可以克服过去阻碍很多人完全采用 Fedora 的多媒体问题。

### 包管理器

最新版本的包管理器提供了多项改进。一方面，您应该从底层的 yum 设施获得更好的性能。其次，包管理器中的新功能允许您向可以从 Fedora 系统安装软件的软件库列表中添加更多软件库。

### IcedTea Java 环境

IcedTea 项目在此版本中致力于创建一个完全免费的 Java 环境。IcedTea 试图通过用兼容的开源插件替换与 OpenJDK 一起使用的二进制 Java 插件来实现这一目标。第 7 章描述了如何启用 IcedTea 以便在 Firefox 浏览器中播放您的 Java 内容。

### 防火墙配置

新的防火墙配置窗口取代了之前版本中使用的安全级别配置窗口。使用新窗口，您不仅可以打开和关闭端口的访问权限。您还可以配置防火墙配置窗口以创建自定义防火墙规则，甚至配置 IP 伪装。

### 自由软件文化

如果我不说些什么关于 Linux 蓬勃发展且将继续蓬勃发展的自由软件开发文化，那我就会失职。Fedora 和 Red Hat 的版权

