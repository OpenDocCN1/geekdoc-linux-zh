

# 第17章 ✦ 运行 Ubuntu Linux 453

音频与视频 — 与其他商业 Linux 发行版一样，Ubuntu 不包含播放商业 DVD 电影或 MP3 音乐所需的软件。然而，它带有一个简单的 CD 播放器Rhythm Music Player、Sound Juicer CD 刻录软件以及 Serpent 音录制应用程序。还有音量和录制电平的控制。

系统工具 — 系统工具菜单中安装了实用工具。网络工具程序允许你运行各种工具来检查网络（查看接口、对等远程系统或运行扫描以检查未保护的端口）。要进入 shell，你可以启动终端（Terminal）应用程序。菜单上的其他工具可以处理软磁盘、重新登录桌面、监控系统活动以及检查日志文件。

菜单会记录你去过的地方，允许你连接到远程服务器，你可以看到（如果已连接的话）最近打开的文档。还有一个可以在你的系统上搜索文件的选项。

# 添加更多软件

虽然 Ubuntu 能够从一张 Ubuntu CD 安装 1.7GB 的应用程序，但这只有 1.7GB。相比之下，Fedora Core 四光盘版系统可以安装高达 7GB 的应用程序。要为 Ubuntu 添加更多软件，你可以使用常用的 Debian 软件包（apt-get 和 dpkg）。不过，你也可以使用 Synaptic 软件包管理器来添加和删除软件包。

要打开 Synaptic 软件包管理器，选择系统 ⟷ Synaptic Package管理器。图 17-3 显示了 Synaptic 软件包管理器窗口。

使用 Synaptic 软件包管理器，你可以通过选择下一列中的“未安装”（Not Installed）项，然后选择左侧你想安装的软件包来安装更多软件。选中一个或多个软件包后，选择应用（Apply），你选择的软件包将从 Internet 仓库下载并安装。

# 454 第三部分 ✦ 选择并安装 Linux 发行版

![](img/a2d958d7eab32ca5b89b2b8af808aa70_485_0.png)

图 17-3：Synaptic 软件包管理器显示并安装 Ubuntu 软件。

在安装 Ubuntu 时，它只会检查 Ubuntu 软件源来查找并下载你添加到 Ubuntu 的软件。然而，当你想要添加官方发行版之外的社区构建软件时，这些被称为 Universe（宇宙）和 Multiverse（多元宇宙）：

- **Universe** — 存储在 Universe 仓库中的软件包包含了尚未稳定到包含在项目中的软件。尽管 Ubuntu 社区已针对 Ubuntu 库对这些软件进行了构建，并且在大多数情况下运行良好，但它们不提供支持或安全修复的保证。

- **Multiverse** — Multiverse 仓库中的软件包包含非免费软件。这意味着软件许可可能不符合 Ubuntu 的要求，软件可能受到专利问题的限制，或者只有二进制版本可用。鼓励用户在使用这些仓库的软件之前，自行研究许可和其他法律问题。

按照以下步骤将 Universe 和 Multiverse 仓库添加到 Synaptic 软件包管理器，这样你就可以使用它们来获取可能尚未稳定到成为 Ubuntu 发布部分的额外 Ubuntu 软件：

- 1. 从 Synaptic 软件包管理器主窗口，选择设置（Settings）⟷ 软件（Repositories）。出现软件偏好窗口，显示你系统中激活的软件。
- 2. 选择设置（Settings）。出现一个设置弹出窗口，如图 17-4 所示。

# 第17章 ✦ 运行 Ubuntu Linux 455

![](img/a2d958d7eab32ca5b89b2b8af808aa70_486_0.png)

图 17-4：添加仓库以获取发行版外的软件。

- 3. 选择“显示禁用的软件源”（Show disabled software sources）并点击关闭（Close）。软件偏好窗口上将显示额外的社区维护软件仓库。
- 4. 选择一个二进制社区维护仓库（Binary Community maintained repositories），使其旁边的框出现复选标记。点击确定（OK）。你会收到警告，你的仓库列表已更改，原始列表的备份包含在 `/etc/apt/sources.list.save` 中。
- 5. 选择重新加载（Reload），新的软件包将下载到你的电脑。
- 6. 从 Synaptic 主窗口选择重新加载（Reload）。来自已添加仓库的软件现在出现在你系统中可以安装的软件列表中。

此时，你可以安装已添加到你的软件列表中的任何软件。请记住，由于这些软件没有得到 Ubuntu 的完全支持，它们将不会收到 Ubuntu 开发团队的官方补丁或安全更新。换句话说，你需要自担风险。

如果你想偏离官方支持的 Ubuntu 软件，可以向你的 Ubuntu 仓库列表添加自定义仓库。这里你需要特别小心，务必在继续操作之前阅读警告。

# 456 第三部分 ✦ 选择并安装 Linux 发行版

> 警告

> 与任何 Linux 发行版一样，每当你渴望使用该发行版支持的官方仓库之外的仓库时，你都应该仔细检查该仓库。非官方仓库可能会破坏软件兼容性，可能包含你无法合法使用的软件，甚至可能包含恶意软件。尽管仍然无法保证安全，但在在使用之前，请检查 Ubuntu 论坛和邮件列表，寻找他人认为可靠的外部仓库。此外，寻找特定于你 Ubuntu 版本的仓库，因为来自较早 Ubuntu 版本或特定 Debian 版本的软件可能无法运行。

要向 Ubuntu 添加自定义仓库，请在 Synaptic 软件包管理器中执行以下操作：

- 1. 选择设置（Settings）：出现软件偏好窗口。
- 2. 选择添加（Add）：出现编辑仓库（Edit Repository）窗口。
- 3. 选择自定义（Custom）：你被要求添加一行。
- 4. 输入标识仓库的行，例如：
deb http://example.com/ubuntu main
- 5. 点击确定（OK）：仓库列表已更新。
- 6. 点击确定（OK）：你收到警告，你的仓库列表已更改。
- 7. 点击重新加载（Reload）：软件包信息已下载。

此时，你可以安装已添加到你的软件列表中的任何软件。（点击左侧的“未安装”以查看任何感兴趣的软件包。）

# 获取更多关于 Ubuntu 的信息

Ubuntu 日益增长的普及带来了许多在线支持资源。学习 Ubuntu 的起点之一是 Ubuntu 论坛（www.ubuntuforums.org）。要开始参与该网站，我建议你阅读 ubuntuforums.org/faq.php 中的 Ubuntu 常见问题解答（FAQ）。

# 第17章 ✦ 运行 Ubuntu Linux 457

此 FAQ 描述了规则并提供了回答技术问题的最佳方法。与大多数论坛一样，浏览主题或进行搜索是寻找所需信息的好方法。

Ubuntu 提供的几个资源对于初学者来说特别有用。我推荐以下内容：

- **Tweaking Ubuntu** (www.ubuntuforums.org/showthread.php?t=3713)—此列表显示了许多人在安装 Ubuntu 后执行的步骤，例如添加对某些显卡或多媒体软件的支持。

- **Absolute Beginner** (www.ubuntuforums.org/forumdisplay.php?f=73)—该论坛中的帖子可以帮助你理解 Linux 的本质，以及 Ubuntu 是否符合你的需求。

- **Community Chat** (www.ubuntuforums.org/forumdisplay.php?f=11)—为了感受 Ubuntu 社区的精神，你可以查看社区聊天（Community Chat），并了解一下大家的想法。

Ubuntu 社区还有一个 Wiki (https://wiki.ubuntu.com)，它继续为使用 Ubuntu 的人员提供有用内容。目前，Wiki 包含了文档、社区信息、不同语言支持和活动区域。还设有针对每个 Ubuntu 版本的特定区域。

# 总结

Ubuntu 无疑是去年 Linux 发行版中的异起之星。Ubuntu 起于 Debian（最受推崇但对初学者来说具有挑战性的发行版之一），并简化了打包和安装。通过单一安装 CD，用户可以安装一组实用的桌面软件或一个精简的服务器系统。

虽然安装过程是基于文本的（安装期间没有华丽图形或鼠标），但与 Debian 系统相比，该过程大大简化了。安装过程中为你提供了有限的选择，使得安装过程变得简单，尽管不像你想要的那样可定制。（当然，你可以在安装后更改你的系统。）

随着 Ubuntu 普及程度的提高，出现了一个活跃的开发者和用户社区。要参与 Ubuntu，良好的起点是社区论坛和 Ubuntu Wiki。

