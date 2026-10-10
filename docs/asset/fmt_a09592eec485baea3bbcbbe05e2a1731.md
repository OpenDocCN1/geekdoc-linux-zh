
`export MAIL=$HOME/.mozilla/default/*/Mail/hostname/Inbox`

如果您通常使用 Mozilla 发送邮件，请临时设置此变量以尝试这些程序。

## 邮件阅读器和管理器

后续章节中描述的邮件阅读器是基于文本的并使用整个屏幕。尽管某些功能不同，但菜单栏在右侧显示可用选项。

## Mutt 邮件阅读器

> 注意：要使用 mutt 邮件阅读器，您必须从书中附带的 DVD 或通过网络 `yum` 安装 `mutt` 软件包。

`mutt` 命令是一个基于文本的、全屏的邮件用户代理程序，用于读取和发送电子邮件。该界面快速且高效。输入 `mut` 启动邮件程序。点击向上和向下箭头键从列出的消息中选择。按回车键选择邮件消息，输入 `i` 返回主菜单。

菜单栏指示如何标记消息删除和取消删除、将消息保存到目录，或回复消息。输入 `m` 撰写新消息，它会打开您的默认编辑器（对我来说是 `vi`）来创建消息。输入 `y` 发送消息。如果您想在手指不离开键盘的情况下进行阅读，`mutt` 是一个不错的选择。（它甚至能处理附件！）

## Pine 邮件阅读器

> 注意：`Pine` 软件包未随 Fedora 或 RHEL 分发，但您可以从项目网站获取 pine：`www.washington.edu/pine/getpine/linux.html`。旧版本 Fedora 或 RHEL 的 RPM 包可以从 `http://rpmforge.net/user/packages/pine` 获取。

`pine` 邮件阅读器是另一个全屏邮件阅读器，但它提供的功能比 `mutt` 多得多。通过 `pine`，您可以管理多个邮件文件夹。您还可以管理新闻组消息以及邮件消息。作为基于文本的应用程序，`pine` 非常易用。它由华盛顿大学的一个小组开发，供校园学生使用，已在 UNIX 和 Linux 环境中广泛使用。

输入 `pine` 启动此邮件程序。显示以下菜单，您可以从中进行：

- `?` - 获取帮助
- `COMPOSE` - 消息
- `INDEX` - 查看文件夹中的消息
- `LIST` - 选择文件夹
- `ADDRESS BOOK` - 更新地址簿
- `SETUP` - 配置选项
- `QUIT` - 退出

只需使用 Pine 即可读取邮件。可用按键：

- 左 `<-` 和 右 `->` 键切换消息
- 回车键选择消息
- `d` 删除消息
- `u` 取消删除消息
- `h` 查看帮助
- `m` 撰写新消息
- `r` 回复消息
- `man` 了解更多命令信息

## 邮件阅读器

`mutt` 命令是一个基于文本的、全屏的邮件用户代理，用于读取和发送电子邮件。界面快速且高效。

## 参与新闻组

Usenet 新闻是另一个几乎与互联网一样老的功能。使用阅读器和许多邮件管理器，您可以从数千个主题中选择并参与讨论。要参与，只需阅读人们发布的消息，对您有想法的消息进行回复，并开始讨论。

要开始，您基本上需要一个阅读器和新闻服务器的访问。`Thunderbird` 电子邮件客户端包含对 Usenet 账户的支持。RHEL 中流行的阅读器是 `Pan`。

> 提示：如果您从未用过新闻组，请查看 `news.announce.newers` 新闻组。该组的存在是为了回答新用户的问题。

`Pan` 阅读器是一个用于读取、管理和与新闻组交互的图形应用程序。它特别擅长显示图片和下载二进制文件。界面直观易用。使用 `Pan` 代替 `Thunderbird` 处理小组的一个大优势是 `Thunderbird` 可以解码 yenc 帖子。

> 注意：可以通过输入 `yum install pan` 获取软件包。

尽管 `Pan` 最初设计用于 GNOME 桌面，但运行 `Pan` 不再需要 GNOME 库。由于原因，`Pan` 现在可以在 KDE、Window Maker 或其他桌面环境中运行，无需特殊软件。

在 shell 中输入 `pine` 启动邮件阅读器。首次启动 `Pan` 时，`Pan` 向导会引导设置阅读器。您需要准备好电子邮件地址和新闻服务器名称。向导完成后，您可以从新闻服务器下载可用的新组列表。

## 使用 Pidgin（原 GAIM）即时消息

`Pidgin` 是 Linux 中主要的即时消息客户端。最初基于美国在线（AOL）Open IM 架构，该项目最近将名称从 GAIM 改为 Pidgin。`Pidgin` 现在支持多种即时消息协议，包括：

- Oscar 因为 Oscar 是 AOL 的官方 IM 协议，它是 `Pidgin` 最常用的协议。为了在 `Pidgin` 中工作，必须对 Oscar 进行反向工程，因为它是 AOL 的专利协议。因此，不支持 AOL 自有即时软件的所有功能。消息通过基于 TCP 的网络（通常是互联网）进行，所有消息都通过 AOL 服务器，除非是直接连接（直接连接很难正常工作）。

# 第 9 章：使用互联网和 Web 389

- MSN Messenger — 该协议最初基于 MSN Messenger Service 1.0 协议（`www.hypothetical.org/docs/msn/ietf-draft.txt`）。自该协议首次发布以来，微软对其进行了大量的“增强”，因此 `Pidgin` 包含的版本需要经过逆向工程处理。要了解更多关于 MSN Messenger（通过 Pidgin 或其他方式），请访问 MSN Messenger 协议资源/链接页面（`www.hypothetical.org/docs/msn/resources/links.php`）。
- ICQ — `Pidgin` 使用源码 `icqllib` 实现 ICQ 协议。由于 ICQ 协议最近发生了变化，通常建议使用 Oscar 连接 ICQ 网络，而不是 icql。
- IRC — 互联网中继聊天协议基于互联网标准 RFC 1459。尽管不同的 IRC 服务器在该标准的实现上存在差异，但这种基于 TCP 的协议在大多数 IRC 服务器上都应该运行良好。
- Yahoo! Messenger — 这允许您使用 Yahoo! Messenger 服务器与其他进行通信。

`Pidgin` 同时也支持其他消息协议。这些包括 Jabber（由 GoogleTalk 使用，可在 `www.jabber.org` 获取）、Napster（即时消息和联系人列表，但不支持下载）、Groupwise Messenger（Novell 的即时消息）、Sametime（来自 `mean.sourceforge.net` 的 Lotus 消息服务）、TOC（用于非官方客户端的罕用 AOL AIM 服务）、Zephyr（来自 MIT 的 IM 系统）。`Pidgin` 不仅支持多种协议，还允许您同时通过多个协议进行通信。还有一些可用的 Jabber 服务器可以供您运行自己的 Jabber 消息服务器，例如 Ejabber（`http://ejabber.jabber.ru`）。输入 `install ejabberd` 来安装该包）。

要在应用程序菜单中启动 `Pidgin`，选择 Internet（互联网）→ Messenger（消息）。图 9-8 包含了 `Pidgin` 好人列表和其他窗口的示例。

如果您从未用过即时消息，可以从 AOL（`https://my.screenname.aol.com/`）或 MSN（`http://messenger.msn.com`）注册免费账户。在 `Pidgin` 初始窗口中点击 Accounts（账户）并添加您的账户。从账户列表中选择您的账户，输入密码并点击 Sign On（登录）。

一旦登录（例如登录 AOL），从弹出的好人列表中点击 IM 按钮可以连接到另一位在线的 IM 用户。或者选择 Chat（聊天）来更改您想要进入的聊天室的名称。您可以根据需要将好人添加到您的列表中。

当 `Pidgin` 运行时，桌面的系统托盘中会出现一个黄色小人形状的小图标。点击该图标可以让您的好人列表显示或隐藏。右键点击该图标弹出的菜单允许您选择发送新消息、加入聊天，或处理 `Pidgin` 账户和偏好设置。

390 第二部分：使用 Fedora RHEL

![](img/74f214fbb2938b570bec5f957507ac66_423_0.png)

9-8：使用 `Pidgin` 访问您的 AOL 或其他即时消息账户。

# 使用 BitTorrent 分享文件

`BitTorrent` 是一种通过网络向大量客户端分发软件内容的工具。`BitTorrent` 之所以独特之处在于，当你将文件下载到电脑上时，其他人也可以从你的电脑下载同一个文件。这样一来，原始提供文件的服务器就不会被挤垮，可能无限多的人可以快速获取该文件。

`BitTorrent` 是自由开源软件社区的极佳工具。例如，当 Fedora 的新版本发布时（通常是 600+MB 的 CD），使用 `BitTorrent` 意味着你不需要等待几天时间让 Red Hat 服务器的流量冷却。同样，想要向世界分享家庭视频的人也可以做到这一点，而不需要工业级的服务器和带宽。当然，也有人担心 `BitTorrent` 让人们分享那些不应该分享的文件变得轻而易举，如商业电影、音乐和软件。

Fedora 存储库中提供了文本界面和图形界面（`bittorrent-gui`）的 `BitTorrent` 客户端。您可以在终端窗口中以 root 用户身份输入以下命令来获取这两个客户端：

```
