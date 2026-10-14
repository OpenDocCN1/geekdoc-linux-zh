
# 第三部分：面向系统管理员的 Ubuntu

## 第28章：文件的备份与恢复

如果你不想将云端作为正在处理文件的主要存储设备，那么“存储即服务”（Storage-as-a-Service）将是执行备份的极佳方法，而且非常有用。它从本质上满足了备份介质最基本的要求之一，即将备份存储在异地，这样本地发生的灾难就无法抹掉你的计算机和你的备份文件。Canonical 提供的 Ubuntu One 存储服务对于 Ubuntu 用户来说特别易于利用：

- 它为任何 Ubuntu 用户提供 `2GB` 的免费存储空间。
- 它是直接内置在 Ubuntu Linux 发行版中的软件。

Ubuntu One 并非纯粹的备份机制，因为它的重点实际上是监控特定文件在你使用的任何机器上的内容。然而，如果你只在单台或少数机器上使用它，那么对于关键文件来说，这是一个非常好的个人备份解决方案，只要你记得将它们复制到家目录下的 Ubuntu One 文件夹中（或直接在其中进行操作）。

在你的 Ubuntu 系统上安装 Ubuntu One 就像在你桌面 Ubuntu 系统上使用常用的包管理软件安装 `ubuntu-client-gnome` 包一样简单，该包还会同时安装底层的 `ubuntu-client` 包。安装这些包将在你的家目录中创建一个 Ubuntu One 文件夹，并在 GNOME 面板中安装一个 Ubuntu One 应用程序插件。

为了使用 Ubuntu One，你需要在 Canonical 的 Launchpad 上创建一个账户，你可以从此页面 `https://one.ubuntu.com/plans` 获取该账户。该页面列出了可用的 Ubuntu One 计划：`2GB` 免费存储或 `50GB` 非免费存储（目前为每月 `10` 美元）。Launchpad 是 Canonical 用于与 Ubuntu 和 Canonical 交互、报告错误（bug）等内容的中心站点。一旦你有了 Launchpad 账户，就可以返回你的计算机系统，使用你的 Launchpad 登录名和密码连接到 Ubuntu One。当你第一次从使用的任何计算机系统连接到 Ubuntu One 时，你必须授权该计算机访问 Ubuntu One，这通过使用 Ubuntu One 网页即可轻松完成。

此时，你存放在家目录下 Ubuntu One 文件夹中的任何文件都将自动镜像到你的 Ubuntu One 账户。要从任何其他 Ubuntu 系统访问它们，只需右键点击 Ubuntu One 插件，选择“Connect”（连接）以授权该机器访问 Ubuntu，你 Ubuntu One 文件夹中的文件将自动同步到你正在使用的计算机。你可以通过网页 `https://ubuntu.com/files` 访问你的文件。

Ubuntu 还提供了一个名为 `usync` 的命令行工具，其名称中包含“sync”（同步）一词，用于自动同步 Ubuntu One 目录以外的文件和目录。为了使用此工具，你必须安装 `ubuntu-client-tools` 包。

一旦安装了该工具，你可以通过执行 `usync --init DIRECTORY` 命令来识别想要从你的 Ubuntu One 账户同步/到的目录，其中 `DIRECTORY` 是你希望作为 Ubuntu One 文件夹镜像的目录名称。执行此命令将显示一个对话框，请求授予访问你的 GNOME 密钥环（GNOME 存储授权信息的地方）。点击“Always Allow”（始终允许）。然后你就可以使用 `usync --action-upload` 命令上传文件，使用 `usync --action-download` 命令将文件下载到机器，使用 `usync --sync` 命令进行同步，以此此类推。更多详情请参阅 `usync` 命令的帮助页（man page）。

关于 Ubuntu One 的更多信息，请参考 `https://wiki.ubuntu.com/UbuntuOne` 中的 UbuntuOne wiki 主题。

### Linux 时机器

Apple 的 Mac OS X 是一个极好的计算环境——它在强大的类 UNIX 操作系统之上提供了一个易于使用的图形界面。还想起了什么吗？Apple 一直拥有创新型、用户友好的软件，随着 Mac OS X 10.5 Leopard 的发布，他们引入了一个令人印象深刻的既友好又强大的备份包，名为 Time Machine（时光机器）。Time Machine 会自动跟踪你系统上的文件并将其备份到异地。如果你删除了某个文件，或者只是想查看旧版本，可以使用 Time Machine 进行令人印象深刻的友好且强大的恢复。正如俗话说，“模仿是赞诚的形式”（Charles Colton）。在 Linux 系统上，类似的图形 Time Machine 软件已经出现，它们可以备份到外部磁盘或网络位置。

以下 Time Machine 类的备份工具在 Ubuntu 上非常值得关注：

- **Back In Time**：Back In Time 是一个优秀的基于 GTK 的软件包，提供了图形化的快照浏览和恢复。图 28-7 显示了 Back In Time 的界面。Back In Time 是我喜欢的 Linux Time Machine 实现之一，也是我个人推荐的，可以通过其主页 `http://backintime.sourceforge.net/` 获取 Ubuntu 包。
- **FlyBack**：FlyBack 最初是一个 Google Summer of Code 项目，在我所知道的 Time Machine 类应用中活跃度最低的，但运行良好，值得一试。FlyBack 通过 Subversion 或解压包安装，其配置界面提供了一些实用的功能，例如自动识别文件系统作为可能的快照存储位置。关于 FlyBack 的更多信息，请访问 `http://code.google.com/p/flyback` 和 `flyback-project.org`。

本章讨论了备份，这是你的个人计算机系统需要执行的最耗时、最无聊但也最有价值的事情。Ubuntu 拥有大量的优秀软件，你可以用它们执行各种类型的备份，从备份到存储在可移动介质上或移动到其他系统。随后，我们讨论了通过网络进行简单备份，并介绍了 BackupPC，这是一款用于对多个系统进行定期网络备份到中央备份服务器的优秀开源备份程序。本章最后介绍了类似于 Apple 受喜爱的 Time Machine 备份恢复软件的 Linux 备份软件包。

第 29 章“设置 Web 服务器”将讨论如何在你的 Ubuntu 系统上设置 Apache 2 Web 服务器。本章将首先提供有关 Web 和 Web 服务器的背景信息，然后介绍安装、配置和监控 Apache 2 的细节——这是传奇 Apache 项目提供的最新、最强大的 Web 服务器。

## 第29章 设置 Web 服务器

计算技术的大多数重大进展都有所谓的“杀手级应用”（killer app）——这是一种极具独特性、强大且具有吸引力的应用程序类型，它能吸引人们对技术的追求，并使其在可预见的未来成为计算格局的一部分。对于一般的个人电脑而言，这种应用是电子表格。对于 Apple Macintosh 而言，这种应用是桌面出版。对于互联网而言，这种应用是万维网（World Wide Web）。当然，每个人都喜欢电子邮件，但万维网将互联网变成了一个充满电子商务、个人和技术信息、社交网络，以及谁知道未来还会出现什么东西的沸腾池。

“使用 Firefox 冲浪网页”解释了如何使用世界上最好的 Web 浏览器 Firefox 来浏览网页。本节将介绍浏览网页的另一面，即如何设置 Web 服务器，以便你能够通过 Web 向任何可以访问你服务器的任何人发布网页和其他内容。大多数企业和学术环境都拥有外部可访问和仅内部使用的 Web 服务器。许多人会在家庭网络上建立 Web 服务器，以便于基于 Web 的调度、文档共享、照片中心存储以及几乎你能想到的任何其他功能。

本章从 Web 的背景知识开始，介绍 Web 服务器的工作原理，以及目前最流行的 Web 服务器 Apache 的历史。后续章节将解释如何安装 Apache、如何配置它、Web 内容位于 Apache 服务器的什么位置、如何扩展和自定义 Apache Web 服务器，以及如何排除连接或权限问题。

### 本章内容

- WWW 101
- Apache 简介
- 安装 Apache
- 配置 Apache
- Web 服务器故障排除

### 万维网 101

这里有许多关于万维网和 HTML 的优秀书籍，但这本书的设计并不是成为其中之一。然而，如果你是 Web 新手，本节将提供一些简要的历史和专业术语（Buzzwords）的示例，这样我就不会在随机使用新术语时让你感到意外。
