
## 第四部分 额外章节

接下来的两个章节将介绍如何通过使用 P2P 客户端参与言论自由革命，例如 `gtk-gnutella`（一种流行的 Gnutella 文件共享网络 Linux 客户端）和 `gnome-download`（一个用于 BitTorrent 下载的简单 Linux 客户端）。与本章的其他部分一样，这些章节侧重于使用客户端软件检索文件，而不是如何从你的系统发布文件——当然，在这一过程中你也在进行分享，但在这里我们侧重于检索它们。

## 安装与使用 Gtk-gnutella

Gnutella 网络（不要与 Nutella 混淆，那是一种美味的欧洲榛子巧克力涂酱）是一个广泛且极受欢迎的 P2P 网络。许多人并没有意识到像 LimeWire 和 BearShare 这样的 P2P 客户端实际上是 Gnutella 客户端。Gnutella 客户端最酷的功能之一是它的搜索功能，我稍后会详细解释，它使得你能够轻松查询整个网络以查找匹配搜索条件的文件。正如本节引言所述，该搜索功能并不咨询单一的中央数据库，如果没有这种酷的“朋友的朋友”机制，将很容易终止 Gnutella 流量。你的查询最初发送到单个 Gnutella 节点，该节点将你的原始查询传递给它知的其他节点，每个节点再将你的查询传递给它知的其他节点，直到大部分 Gnutella 网络因你的搜索查询而活跃起来。

### 安装 gtk-gnutella

由于每个人都想或需要进行 P2P 文件共享，Ubuntu 默认没有安装 `gtk-gnutella` 客户端。要安装 `gtk-gnutella`，请使用第 23 章中讨论的任何包管理工具安装 `gtk-gnutella` 包及其任何依赖项。Ubuntu 用户不应担心安装 `gtk-gnutella` 会在系统上安装大量 GN 相关的包（如果它们尚未存在的话）。

### 使用 Gtk-gnutella

按照上一节的方法安装 `gtk-gnutella` 后，会在“应用程序 » 互联网”菜单中创建一个菜单项。要启动 `gtk-gnutella`，请点击此菜单上的 Gnutella 项目，这将启动应用程序并显示类似图 B-23 所示的窗口。

第一次运行 `gtk-gnutella` 时，它会在你的主目录下创建 Gnutella 下载目录，该目录将存储它下载的文件。该目录包含三个子目录：`complete`（已完成），下载完成后存储成功下载的文件的地方；`incomplete`（未完成），存储正在下载中的文件的地方；以及 `corrupt`（损坏），存储与 Gnutella 校验和不匹配的文件的地方。不过，`corrupt` 目录本身并不是坏的，只是不该出现在在这里。

> 当你启动 `gtk-gnutella` 时，可能还会看到一个名为“检测到旧版本”的对话框，它指出 Ubuntu 仓库中提供的 `gtk-gnutella` 版本不是最新版本，并引导你访问 `gtk-gnutella` 的 SourceForge 获取最新版本。虽然事实确实如此，但除非 Ubuntu 仓库提供的版本真的出了问题，否则我不会费力从 SourceForge 获取最新版本。因为你不仅需要手动编译它，而且无法像使用 Ubuntu 仓库的标准版本并在新版本发布时那样自动升级它。

#### 图 B-23

`gtk-gnutella` 启动窗口

![](img/e3248f698da647444405a34229bd9df5_1258_0.png)

除了菜单栏外，图 B-23 所示的 `gtk-gnutella` 屏幕最有趣的部分如下：

- **摘要区域（左下角）：** 显示连接客户端数量、正在进行的上传和下载数量、该应用程序看到的本地 HTTP（Web）流量，以及目前通过网络通过的 Gnutella 流量数量的区域。
- **详情窗口（左上角）：** 包含可折叠/展开条目的窗口，允许你获取其列出的任何项目的详细信息：网络状态、已完成的上传、活动和排队中的下载，以及你发起的任何搜索状态。
- **搜索栏（左上角，菜单栏正下方）：** 允许你搜索名称匹配特定字符序列的文件。
- **连接状态窗口（右中间）：** 显示任何活动连接的状态、执行搜索时的搜索结果，以及在查看或排队下载时活动下载的状态。此窗口中显示的信息类型取决于控制窗口中选中的项目。
- **控制窗口（右下角）：** 允许你控制从你的机器支持并端口化的连接数量。

`gtk-gnutella` 的有趣之处实际上是搜索某些内容，匹配你找到的内容，然后下载结果。所以，让我们开始搜索吧。为了证明外面有很多合法且实用的内容，请搜索“Linux ISO”。这样做是将光标置于搜索栏的搜索字段中，输入 Linux ISO 并回车。搜索开始，匹配搜索字符串的项显示在连接状态（现在是搜索结果）窗口中。一旦显示搜索结果，你可以通过将光标悬停在任何一个项目的名称上来查看其摘要信息。

如果过了一会儿还没有看到结果，你可能需要获取更高版本的 `gtk-gnutella`；Gnutella 网络经常会禁止自己访问网络。你可以在 `http://archive.ubuntu.com/pool/universe/g/gtk-gnutella` 找到 `gtk-gnutella` 的最新版本，并使用 `dpkg -i` 手动安装。

一旦你发现了想要下载的文件，可以右键点击其名称并从弹出菜单中选择下载来下载。一旦开始下载，你可以随时通过详情窗口中的 Active 条目查看状态。如果下载没有列出，说明它正在排队中，你可以通过 Queue 条目查看它在等待什么。如果我发现多个匹配项，我通常会下载多个以尽快获取文件。一旦其中一个开始下载，你就可以停止其他的以节省网络带宽。

> 如果你在定位或下载文件时遇到问题，请确保你运行的任何防火墙都没有阻止 Gnutella 使用的端口。如果你位于可配置网关或路由器之后，你可能需要将这些端口从外部接口转发到运行的主机。更多信息请见 `gtknutella.sourceforge.net/en/pagefaq`。关于各种路由器端口转发的通用讨论请访问 `http://www.portforward.com`。

## 使用 BitTorrent

BitTorrent 由 Bram Cohen 发明，已经存在很久，是一种非常强大的 P2P 文件共享协议。原始 BitTorrent 软件是 GPL 许可的并用 Python 编写的。坦率说，我使用 BitTorrent 的命令行版本（`bittheadless.py`），因为它“运行良好”。不用担心，我会在这里告诉你如何操作——你可以通过安装 Torrent 包来安装 BitTorrent 的命令行版本。

BitTorrent P2P 机制的秘诀在于使用 torrent 文件，这些文件提供了作为 torrent 分发的文件信息（BitTorrent 的通用术语，指作为一组共享的每个文件集合），以及使用跟踪与 torrent 相关活动的计算机系统（在 BitTorrent 中称为 tracker）。Napster 的方法使用中央服务器，它对 torrent 内容并不了解，只知道哪些节点参与了特定 torrent 的下载、上传和共享。tracker 跟踪感兴趣的 peer 之间的通信——一旦 peer 之间开始通信，就不再需要 tracker。正如你所期的，初始化 torrent 时，至少有一个 peer 提供 torrent 中完整的文件集，这在 BitTorrent 术语中被称为种子（seeding）。

## 文件传输与共享

### B2

BitTorrent 的一个有趣的优化是节点以随机顺序的块来接收并共享 torrent 中的文件。这意味着许多节点可能正在下载组成 torrent 的文件集合，正常情况下，你应该预期两个节点都在共享同一个文件的部分。这使得 torrent 变得多样化——即使 tracker 消失，所有节点也拥有文件的完整集合——它们相互交换块。这在 BitTorrent 术语中被称为分布式复制。

BitTorrent 是一款非常棒的软件、一种令人深刻的协议、一种优秀的分发机制，并可以在网络上保证任何共享。它是免费的。如果你觉得它有用，可能考虑通过 `http://bittorrent.com/donate` 捐赠以帮助其发展。

如果你在运行 BitTorrent 时遇到问题，请确保你的任何防火墙都没有阻止 BitTorrent 端口（6881），这些是在路由器或网关后面使用的端口。如果你在路由器或网关后面遇到性能问题，你可能需要从你的外部接口将这些端口转发到运行 BitTorrent 客户端的主机。Michael Ingram 有一篇关于解决下载问题以及配置特定路由器和网关的文章，可以在 `www.slyck.com/news.php?story=493` 查看。关于各种路由器端口转发的通用讨论可以在 `www.forward.com/routers` 查看。

![](img/3248f698da64744405a3422bd9df5_0)

### 在 Ubuntu 系统上使用 Transmission

由于 Transmission 是作为基础 Ubuntu 发行版的一部分安装的，你不需要任何操作即可访问或配置它。要启动 Transmission，选择应用程序菜单中的 BitTorrent Client 命令。这将显示 B2-24 所示的初始对话框。

#### B2-24

初始对话框

![](img/3248f698da64744405a3422bd9df5_1)

点击 Open 图标（或选择文件菜单命令），使用浏览器导航到包含你已下载的 torrent 文件的目录，选择一个并点击 Open 开始下载和共享其内容。Transmission 对话框将显示你的下载状态，如 B2-25 所示。

59

## 第四部分

## 额外章节

#### 图 B2-25

正在下载

![](img/3248f698da64744405a3422bd9df5_0)

在进度条上方，torrent 的名称显示了你当前下载的 torrent 数量、torrent 中文件的完整大小以及你当前下载的 torrent 文件的百分比。进度条下方显示了你正在下载 torrent 部分的节点数量。

一旦你下载了 torrent 中的完整文件集，Transmission 将开始种子该 torrent，这意味着你正在向尝试下载它的其他人提供 torrent 中的文件。通常情况下，种子 torrent 是很好的做法，直到其他用户从你的 torrent 下载的数据量——等于 torrent 的大小（只要人们仍在尝试下载该 torrent——不需要永远等待）。文件共享确实意味着共享，正如罗杰斯先生一直说过的，爱是

> 如果你正在下载或种子某个 torrent，并且你需要所有的网络带宽用于更高优先级的任务（例如从工作中传输文件或在 YouTube 上看视频），你可以通过选择每个 torrent 并点击 Transmission 工具栏中的 Pause 来临时暂停 BitTorrent。当你完成重要事项后，可以通过选择想要恢复的每个 torrent 并点击 Transmission 工具栏中的 Start 来恢复下载和/或种子。

Transmission 允许你同时下载和种子多个 torrent。默认情况下，Transmission 对话框显示所有 torrent 的状态，无论你是在下载还是种子。要限制 Transmission 中的 torrent 仅显示特定状态的 torrent，你可以点击状态窗口上方的任何按钮。点击 Active 显示所有未暂停的 torrent。点击 Downloading 显示所有仍在下载的 torrent，而 Seeding 显示所有下载已完成但你正在提供给其他人的 torrent。正如你可能猜到的，点击 Paused 只显示你显式暂停的 torrent。

文件共享愉快！如果你发现 Transmission 界面对于你的任务来说过于简单，Ubuntu 仓库中有许多其他 BitTorrent 客户端可供选择。最广为人知的有 azure，一个基于 Java 的客户端，它还包含一个 tracker，因此可以用于种子 torrent；bittorrent-gui，一个快速强大且轻量级的客户端；以及 qtorrent，一个使用 QT 图形界面的图形化客户端。

66

## 在 Kubuntu 上使用 KTorrent

由于 KTorrent 是作为基础 Kubuntu 发行版的一部分安装的，你不需要任何特殊操作即可访问它。要启动 KTorrent，选择 Internet 中的 BitTorrent 命令。这将显示 B2-26 所示的初始对话框。

#### B2-26

初始对话框

![](img/3248f698da64744405a3422bd9df5_0)

点击 Open 图标（或选择文件菜单命令），使用浏览器导航到包含你已下载的 torrent 文件的目录，选择一个并点击 Open 开始下载和共享。Transmission 对话框将显示你的下载状态，如 B2-27 所示。

#### B2-27

关于所选 torrent 的信息

![](img/3248f698da64744405a3422bd9df5_1)

在进度条上方，torrent 的名称提供了你当前下载的 torrent 数量、torrent 中文件的完整大小、你的近似下载速度、你正在下载 torrent 部分的节点数量、种子 torrent 的时间以及你当前下载的 torrent 文件的百分比。

如果你想将 torrent 下载到主目录以外的特定位置，可以使用对话框顶部右侧的 Browse 按钮导航到你想存储的位置。如果你只想下载 torrent 中的特定文件，可以取消勾选左侧的复选框。一旦你完成了任何更改，点击 OK 开始下载与 torrent 关联的文件。然后你可以点击 Download 标签查看你正在下载的 torrent(s) 状态，如 B2-28 所示。

#### B2-28

KTorrent 中正在下载

![](img/3248f698da64744405a3422bd9df5_0)

关于 torrent 的信息提供了你当前下载的 torrent 数量、torrent 中文件的完整大小、你的近似下载速度、正在种子 torrent 的节点数量以及正在下载 torrent 的节点数量（在 BitTorrent 术语中称为 leech）、你当前下载的 torrent 文件的百分比、你上传与下载数据的比例（如果后者不为零）、以及你下载或种子的持续时间。

一旦你下载了 torrent，你可以选择种子它。如果你这样做，KTorrent 将开始种子该 torrent，这意味着你正在向尝试下载它的其他人提供文件。KTorrent 允许你同时下载和种子多个 torrent，可以通过分别点击 Downloading 或 Uploading 标签来实现。当你开始种子 torrent 时，它会从 Downloading 标签移并在 Uploading 标签中。通常情况下，种子 torrent 是很好的做法，直到其他用户从你的 torrent 下载的数据量——等于 torrent 的大小（只要人们仍在尝试下载该 torrent——不需要永远等待）。

## 寻找 Torrent

此时，我希望你正在想：“好吧，BitTorrent 听起来极了，但我从哪里获取这些 torrent 呢？”由于 BitTorrent 不像 Gnutella 等 P2P 网络那样提供类似的搜索功能，你必须有一个 torrent 文件才能使用它。你可能需要

62

# 文件传输与共享 B2

我注意到我在上一节中作为示例的 torrent 是 Grateful Dead（感激死乐队）的一场现场录音，他们以允许粉丝自由分享现场录音而闻名。在网上搜索“Grateful Dead”和“torrent”会有数以亿计的命中，但在寻找你喜爱的乐队的现场录音或其他免费下载资源时，这并不是最高效的搜索机制。

许多网站可能提供了专为寻找 torrent 设计的搜索引擎。我最喜欢的有以下几个：

- btjunkie: `http://btjunkie.com`
- isoHunt: `http://isohunt.com`
- Torrent Scan: `http://www.torrentscan.com`

开始时，你可能还想访问 `http://netforbeginners.about.com/od/peersharing/torrent_search.htm`，它提供了一个由用户提交的 BitTorrent 搜索引擎列表。

由于 BitTorrent 是一种非常高效的 P2P 机制，许多 Linux 发行版（包括 Ubuntu）为最新的发行版提供 torrent，同时支持标准的基于 Web 的下载。BitTorrent 是下载你喜欢的 Linux 发行版的 CD 或 DVD 镜像（ISO 文件）的快速方法——例如 Ubuntu 或 Kub。你可以在 `www://ubuntu.com/download` 找到提供最新版本 torrent 的网站，可以在 `www.ubuntu.org/getubuntu` 查找 Ubuntu 信息。

# 获取更多关于 BitTorrent 的信息

由于这是一本关于 Ubuntu 和 Kub 发行版的通用型书籍，而不是 BitTorrent 圣经，因此本节仅触及了 BitTorrent 可用信息的皮毛。我敢打赌，一旦你开始使用 BitTorrent，你就会额外的问题，或者仅仅想了解更多。以下是一些关于 BitTorrent 的优秀专门来源：

- BitTorrent FAQ 指南：`http://wiki.etree.org/index.phppage=BitTorrent`。这是一个非常好的链接集合，包含了来自一个用于法律无损音频录音的共享网站的 Web 上 BitTorrent 信息。
- BitTorrent FAQ 帮助：`http://www.vadd44.com/torrent`。一份关于使用 BitTorrent 和解决常见问题的实用指南。
- Brian Dissent 的 FAQ：`http://dissent.net/btfaq`。尽管部分内容有些过时，但该 FAQ 提供了许多有用信息。

### 总结

商业和学术环境通常提供文件服务器，用于集中收集企业文档、项目目录，甚至是支持的软件。许多网络计算环境也同样这样做，为家庭照片、音乐和文档提供中心位置。本章解释了如何使用 FTP 等软件运行在 Microsoft Windows、Mac OS X 和 Linux 系统上的远程文件服务器，以及如何使用 Samba 和 NFS 挂载共享文件夹和网络目录。本章最后一节讨论了 Ubuntu 上的点对点 (p2p) 文件共享，这是目前常用的最流行且最节省资源的文件共享机制。

赠送章节 3 进入了 Linux 系统的传统负担领域——如何在 Ubuntu 或 Kubuntu 系统上编译你自己的软件。Ubuntu 和 Kubuntu 系统在默认安装中不包含编译环境，因为并不是每个人都需要它们，但重要的是，Ubuntu 仓库提供了如此丰富的软件选择，以至于除非你想（或你是一个开发者），否则你很少需要这样做。在 Linux 系统上自行编译应用版本的需求是 FUD（恐惧、不确定性、怀疑）的传统组成部分，Linux 贬低者利用这些部分来支持他们关于“Linux 很难用且仅供极客使用”的说法。这完全不是如此。现在构建自己的应用不仅是可选的，而且正如你将在第 23 章中看到的，像 `apt-get`、`aptitude`、`Adept` 和 `Synaptic` 这样的包管理软件在你需要时可以轻松构建工具和强大的 IDE。

# 赠送章节 3

## 在 Ubuntu 和 Kubuntu 上进行开发

正如网站和整本书指出的，Ubuntu 和 Kubuntu 是适合每个人的发行版。这包括开发！仅仅因为 Ubuntu 和 Kubuntu 易于使用，并不意味着严肃、硬核开发者无法在这些系统上完成实际工作——事实上恰恰相反。这种递归的力量正是 Ubuntu 和 Kubuntu 发行版。此外，Ubuntu 和 Kubuntu 都提供了如此出色的用户体验，你可能花在调整和微调 Linux 桌面以及已安装软件的时间可以投入到更有生产力的追求中，例如开发你的个人代码项目。整个世界可能都在等待你的软件！

# 本内容

- 安装和使用 GCC
- 使用 make 简化重新编译
- 编译开源软件
- 安装和使用 Eclipse IDE
- 配置和使用 Subversion

总来说，Linux 在 Microsoft Windows 和 Mac OS 等其他平台的用户中名誉不好，他们经常将 Linux 视为使用 VT100 终端和命令行的穴穴居民。虽然有很多话可以说明 Linux 在提供用于一切的图形化工具与在需要时提供命令行访问之间取得了恰好的平衡。现代 Linux 模型与 OS X 提供的用户模型惊地相似，而最近版本的 Microsoft Windows 包含了“新”工具来支持广泛的命令行使用和复杂的命令脚本支持。这些内容有什么让你听起来耳熟的？

本章解释了如何安装 Linux 软件项目所需的包，从安装世界上最好的编译器（`gcc`，作为自由软件基金会 GNU 编译器集 GCC 的一部分提供的 C 编译器）的基础开始，然后介绍你将在 Ubuntu 或 Kubuntu 系统上提供完整软件环境所需的相关工具，最后扩展到讨论许多人在 Linux 上创建和维护时使用的其他软件包。这些其他软件包包括了集成开发环境 (IDEs)，它们为现代软件开发提供了一个易于使用的界面，以及你在 Linux 上创建和维护时需要的版本控制和管理软件。

# 安装和使用开发软件

正如网站和书中指出的，Ubuntu 和 Kubuntu 共享版通过提供一个名为 `build-essential` 的软件包（它包含了 GCC 和 C++ 编译器、强制库、`make` 工具以及当前 Linux 头文件）来提供构建基础环境。

取决于你编译的软件或软件包的构建需求，可能会发现你将需要安装其他软件包。例如，`autoconf` 和 `make` 等配置相关的工具并不在 `build-essential` 软件包中。同样，`build-essential` 包仅提供 GCC 和 C++ 编译器——如果你想编译 GCC 支持的任何语言的应用程序，你将单独安装那些编译器和任何相关库。这些额外的包可以使用与 `build-essential` 软件包相同的方法安装。

# 安装 GCC 编译器、make 和其他

GCC 仓库由 Ubuntu 和 Kubuntu 共享，通过提供一个名为 `build-essential` 的软件包来轻松安装构建环境的核心元素。正如下一节所示，安装这个单一软件包会将构建环境的所有成分整合在一起，你可以通过任何其他工具来增强它。

# GCC 编译器概述

在实践中，`gcc` 是 GNU Compiler Collection 的缩写。在小写时，`gcc` 是 GNU Compiler Collection 中的一个特定编译器，即 GNU C Compiler。GCC 是一个针对后端编译引擎的编译器前端集合。GCC 的编译器列表包括 `g(gcc)`、`(g++)`、Objective C（带有特殊库的 `gcc`）、Fortran (`gfortran`) 和 Java (`gcj`)。GCC 还有针对 Pascal、Modula-3 和 Ada 的前端。C 编译器支持多种不同的 C 方言，包括传统的 C 和 ANSI C。C++ 编译器是一个真正的 C++ 编译器——换句话说，它不是在编译之前先将 C++ 代码转换为中间表示，而是像 GCC C++ 编译器那样直接从 C++ 源代码生成原生可执行代码。

## 在 Ubuntu 和 Kubuntu 上进行软件开发

GCC 是 GNU 项目，由自由软件基金会（FSF）指导。FSF 拥有在 GPL 协议下的编译器和链接器的版权。个人或 FSF 拥有其他组件（如运行时库和测试套套件）的版权，而其他组件则根据各种自由软件许可协议授权。FSF 还负责处理 GCC 项目的法律事务。

# 获取源码包（Source Packages）

在整本书中，关于安装软件包的信息一直集中在获取和安装二进制包上，二进制包是包含可执行程序、相关的预编译库以及可能是文本或二进制格式的关联配置数据的包。由于本章讨论的是构建工具，因此至少提及如何获取与任何 Ubuntu 或 Kubuntu 二进制包相关的源码是合理的。简而言之，这本质上有两个步骤，这两个步骤最易通过使用命令行 `apt-get` 完成：

- 获取你想要构建的包的源码。
- 满足构建特定软件包所需的对其他软件、库等的任何依赖关系。

要获取任何 Ubuntu 或 Kubuntu 包的源码，请使用 `apt-get source <package>` 命令，其中 `<package>` 是你想要从源码构建的包名。要安装从源码构建该包所需的其他工具、库、头文件等，请使用 `apt-get build-dep <package>` 命令，其中 `<package>` 是你想要构建的包名。

> 请参阅第 23 章“添加、删除和更新软件”，以获得关于使用 `apt-get` 工具满足依赖关系和获取包源码的更详细讨论。

# 使用 GCC 的 C 编译器

`gcc` 支持大量的命令行选项来控制其行为。它既接受单字母选项（例如 `-n`），也接受多个字母的选项（例如 `-ansi`）。由于它接受所有类型的选项，因此你不能将多个单字母选项组合在一起，就像你可能在 `ps` 等许多 GNU 和 UNIX/Linux 程序中所做的那样。例如，多个字母的 `-pg` 与单字母选项 `-pg` 是等等的。`-pg` 选项会在最终的二进制文件中创建额外的代码，用于为 GNU 代码分析器 `gprof` 输出分析信息。另一方面，`-p -g` 选项会在生成的二进制文件中生成额外的代码，为性能分析器（`profile coder`，`-p`）产生分析信息，并导致 `gcc` 使用操作系统的标准格式生成调试信息（`-g`）。

尽管它对多个单字母选项的组合很敏感，但你可以在 `gcc` 命令行上自由混合这些选项和编译器参数的顺序。以下两个命令在告诉 `gcc` 的信息方面是相同的：

```
