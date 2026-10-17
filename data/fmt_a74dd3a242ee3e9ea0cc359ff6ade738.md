
每个仓库都有自己的 APT 行，其中包含有关该仓库的额外信息，APT 使用这些信息来确定它包含什么类型的包。您需要从尝试添加的仓库网站上获取正确的 APT 行，因此请选一个例子来看看它是如何工作的。打开 Firefox，并进入 `http://www.getdeb.net/updates/Ubuntu#how_to_install`。GetDeb 专门为尚未正式发布到 Ubuntu 的软件制作包。页面顶部的框中应该有关于从 GetDeb 安装包的说明，跳到列表的第二项并找到 APT 行，它看起来像这样：`deb http://archive.getdeb.net/ubuntu/lucid-getdeb-apps`。它遵循所有 APT 行的相同格式：单词 `deb`，后面跟着一个 Web 地址，然后是另外几个指定 APT 应该检查仓库哪个部分的几个单词；右键点击它，并从弹出菜单中选择“复制”。在操作 Firefox 的时候，您还需要获取仓库的 GPG 密钥（我将在结尾详细解释）。它应该链接到您获取 APT 行时所在的同一个网站；以 GetDeb 为例，访问 `http://archive.getdeb.net/getdeb-archive.key`，当 `getdeb-archive.key` 窗口打开时，选择“保存”并点击“确定”。现在您已经拥有了这些关键信息，将仓库添加到您的系统中就非常简单了：

1. 选择“系统” > “软件源”。如果提示，输入您的密码，然后点击出现的“软件源”窗口中的“其他”选项卡。
2. 点击“添加”。系统将提示您输入 APT 行，将其粘贴到框中，然后点击“添加”（图 6-7）。“其他”列表中应该出现一个新项。
3. 选择“身份验证”选项卡，点击“确定”。使用出现的窗口找到您之前下载的 `.key` 文件（它可能在您的“下载”文件夹中）。
4. 选择 `.key` 文件并点击“确定”。现在您已经拥有了这些关键信息，将仓库添加到您的系统中就非常简单了：

APT 行包含了仓库的类型、位置和组件，如图 6-8 所示：`deb http://archive.ubuntu.com/ubuntu main`。APT 行：`http://archive.getdeb.net/ubuntu-lucid-getdeb-apps`

5. 关闭“软件源”窗口。`deb http://archive.getdeb.net/ubuntu/lucid-getdeb-apps` 可能会提示软件信息已过时，点击“刷新”以获取最新信息。
6. 关闭“软件源”窗口（它已经打开的话请重新打开），并在软件中心搜索您想要从新仓库的程序。例如，搜索 Writer，一个帮助您写小说的趣味程序。它应该像其他应用程序一样出现在搜索结果中，您可以按通常的方式安装它。

这似乎需要很多步骤，但过此就了。这比去当地电脑商店买一个新程序要好得多，不是吗？

### 鸟书 87 结语

最后一点：还记得所有关于身份验证和 GPG 密钥的事务吗？它们与安全措施有关，用于检查包是否来自您所认为的地方。（理论上，有人可能会劫持仓库并在其中放入有害包）。如果您不添加 GPG 密钥，Ubuntu 软件中心将拒绝安装该仓库的任何包。不过，拥有 GPG 密钥并不足以让您免受意外。在使用第三方（即非 Ubuntu）仓库时，您应该始终保持谨慎；在添加之前确保它是可信的。

许多 Ubuntu 爱好者感染了编程热，并决定编写自己的软件。世界上有各种人们为了满足自己的需求而编写的软件，只要您知道从哪里获取，其中许多软件都可以免费供您使用。幸运的是，大多数软件现在都可以在 Ubuntu 的个人包存档 `PPA` 中找到。Ubuntu 的项目网站为 Launchpad。PPAs 是微型软件仓库，是人们与其他分享自制软件的简单方式（需要强调的是，来自 PPA 的软件并不总是可用）。你可以访问 `https://launchpad.net/ubuntu/+ppas` 并搜索你想要的内容来查找这些软件。

在本示例中，你将看到如何安装 OpenSonic，它是经典游戏《刺猬索尼》的开源重制版（见图 6-10）：

- 1. 在 `https://launchpad.net/ubuntu/+ppas` 的搜索框中输入 `lucid games`，点击 `Search`（搜索）开始。
- 2. 第一个搜索结果应该是 Games (Lucid)，点击该链接，并查看加载页面上标题为 *Adding this PPA to your system*（将此 PPA 添加到你的系统）的部分。
- 3. 复制 `ppa:fake-t-j/games` 部分——这是一个你可以用于添加到库的快捷方式，而无需使用更复杂的 APT 命令。（如果你好奇，仍然可以通过 `Technical details about this PPA`（关于此 PPA 的技术细节）链接来查看 APT 命令。）
- 4. 选择 `System > Administration > Software Sources`（系统 > 管理 > 软件源），并选择 `Other Software`（其他软件）选项卡。
- 5. 点击 `Add`（添加），并将 PPA 快捷方式粘贴到提供的框中。然后点击 `Add Source`（添加源）。
- 6. 此时会自动添加 GPG 密钥，现在关闭软件源窗口。
- 7. 在提示更新包信息时点击 `Reload`（刷新），然后打开 Ubuntu 软件中心像安装任何包一样安装 OpenSonic。

![](img/35405f17cef8b43ddf1af3fc22de194c_125_0.png)

图 6-10：运行 OpenSonic

这只是一个例子——PPAs 不仅供爱好者用于发布怀旧软件。一些 Ubuntu 开发人员使用 PPAs 来制作最新版本的软件，尽管是以非官方且未经测试的方式。例如，如果 OpenOffice.org 或 Firefox 发布了重大新版本，请关注 Ubuntu 论坛 (`http://www.ubuntuforums.org/`)，看看是否有人通过他们的 PPA 提供了最新最强大的版本。

## 项目 6C：安装 Ubuntu 仓库中未提供的 DEB 包：Skype

你可能还记得，通过 Ubuntu 软件中心从仓库安装的应用是以 DEB 包的形式存在的。尽管这些仓库似乎包含了几乎可能的软件，但由于某些原因，某些包永远不会进入仓库。Skype 就是这些包之一。

如图 6-11 显示，Skype 是一种网络电话（VoIP）软件，允许你通过互联网与其他 Skype 用户通话，清晰度堪比普通电话线。最棒的部分是，它是免费的——即使你拨打给海外用户。Skype 还提供一些服务，例如 SkypeOut，它允许你从电脑拨打普通手机和固电话号码，费用只有普通电话的一小部分。

![](img/35405f17cef8b43ddf1af3fc22de194c_126_0.png)

图 6-11：Skype

虽然 Ubuntu 中确实有 Ekiga Softphone 等开源 VoIP 包，但它们与知名度更高、更更广泛的 Skype 不兼容。由于你认识的大多数人都在使用像 Skype 这样的 VoIP 软件包，因此使用 Skype 才能方便地与他们交流，这才是有意义的。

Ubuntu 仓库中没有 Skype，你需要从 Skype 网站 (`http://www.skype.com/`) 自己获取。点击 Download 按钮，它将自动带你进入 Linux 版本 Skype 的下载页面。在该页面，点击 Ubuntu 链接，并在弹出窗口中点击 Save File 按钮。

下载完成后，你将在硬盘上（通常在 Downloads 文件夹中）找到该 DEB 包。双击该包打开安装程序窗口（图 6-12）。点击 Install，随后会提示你输入密码。安装完成后，点击出现窗口中的 Close 按钮，再次点击软件包安装窗口中的 Close。

与所有 APT 前端一样，当另一个 APT 前端打开时，无法使用软件包安装。此外，在使用软件包安装之前，请确保更新管理器（Update Manager）和 Ubuntu 软件中心已关闭。

所有组件安装完毕后，你可以通过 `Applications ▸ Internet ▸ Skype` 来运行 Skype。如果你发现无法拨打电话或声音工作不正常，请查看 `https://help.ubuntu.com/community/Skype/` 获取故障排除提示。此外，既然谈到了声音，请记住使用 Skype 时最好使用耳机。尝试使用廉价的麦克风可能会导致反馈或回声，因为麦克风会拾取并传输扬声器的声音。

![](img/35405f17cef8b43ddf1af3fc22de194c_127_0.png)

**图 6-12：** 软件包安装窗口

# 7

## 整洁的层级

*Ubuntu 中的文件和磁盘处理*

![](img/35405f17cef8b43ddf1af3fc22de194c_129_0.png)

无论你使用哪种系统，都有其他视图供你选择，例如 Tree（树），它提供了一个可展开的文件系统层级视图，以及 History（历史），它显示你最近在文件系统中的位置，就像浏览器中的历史记录功能一样。
