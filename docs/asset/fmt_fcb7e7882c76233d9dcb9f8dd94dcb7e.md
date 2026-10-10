
> 提示：大多数这些邮件程序都使用你的 `$MAIL` 环境变量的位置作为你的本地邮箱。通常，该位置是 `/var/sp/mail/user`，其中 `user` 是你的名字。要设置 `$MAIL` 指向你的邮箱（以便你可以使用基于文本的邮件程序或图形化邮件客户端），请向你的一个启动文件之一添加以下行：
>
> `export MAIL=$HOME/.mozilla/default/*/Mail/hostname/Inbox`

如果你使用 Mozilla 邮件，可以临时设置此变量来尝试这些邮件程序。

## 邮件阅读器和管理器

后续章节描述的邮件阅读器是基于文本的并使用整个屏幕。虽然某些功能有所不同，但菜单栏直接在屏幕上显示可用选项。

### Mutt 邮件阅读器

> 注意：要使用 mutt 邮件阅读器，你必须从书中附带的 DVD 安装软件包或通过网络使用 `yum` 安装。

`mutt` 命令是一个基于文本的、全屏的邮件用户代理，用于读取和发送电子邮件。该界面快速高效。输入 `mutt` 开始邮件程序。点击向上和向下方向键从列出的消息中选择。按回车键发送邮件消息，输入 `i` 返回主菜单。

菜单栏指示了如何标记消息删除或取消删除、将消息保存到目录或回复消息。输入 `m` 编写新消息，它会打开你的默认编辑器（对我来说是 `vi`）来创建消息。输入 `y` 发送消息。如果你想在手指离开键盘的情况下阅读邮件，`mutt` 是一个不错的选择。（它甚至能处理附件！）

### Pine 邮件阅读器

> 注意：`pine` 包没有随 Fedora 或 RHEL 分发，但你可以从 Pine 项目网站获取 pine：http://www.washington.edu/pine/getpine/linux.html。较旧版本 Fedora 或 RHEL 的 RPM 包可以从 http://rpmforge.net/user/packages/pine 获取。

`pine` 邮件阅读器是另一个全屏邮件阅读器，但它提供的功能比 `mutt` 多得多。通过 `pine`，你可以管理多个文件夹。你还可以管理新闻组消息以及邮件消息。作为基于文本的应用程序，`pine` 非常易于使用。它由华盛顿大学的一个小组开发，供学生使用。

通过输入 `pine` 此程序。显示以下菜单，你可以通过关联字母选择项目：

- HELP 获取 Pine 的帮助
- COMPOSE MESSAGE 编写并发送消息
- MESSAGE INDEX 查看文件夹中的消息
- FOLDER LIST 选择文件夹
- ADDRESS BOOK 更新地址簿
- SETUP 配置 Pine
- QUIT 退出 Pine

### 邮件阅读器

`mail` 命令是 UNIX 的第一个邮件阅读器。它是基于文本的，但不是面向屏幕的。输入 `mail` 你将看到邮箱中的消息。由于 `mail` 不是面向屏幕的，你在消息标题后只会得到提示符。输入 `?` 查看可用命令。

在 `mail` 期间，输入 `h` 查看邮件标题。只需输入消息编号即可查看消息。输入 `d#`（用消息编号替换 `#`）删除消息。要创建新消息，输入 `m#`（用消息编号替换 `#`）。输入 `man mail` 了解更多关于 `mail` 命令的信息。

## 参与新闻组

使用新闻器，甚至是普通的邮件阅读器，你可以从成千上万的主题中选择并参与讨论。要参与，你只需阅读人们发布到组内的消息。

要要开始，你基本上需要一个阅读器以及对新闻服务器的访问权限。Thunderbird 邮件客户端包含了访问 Usenet 账户的支持。RHEL 自带的一种流行的新闻器叫做 Pan。

> 提示：如果你从未用过新闻组，请查看 `news.announce.newusers` 新闻组。该组的存在是为了回答新用户的问题。

Pan 新闻器是一个用于读取、管理和与新闻组交互的图形应用程序。它特别擅长显示附件图片和下载二进制文件。界面非常直观易于使用。使用 Pan 而不是 Thunderbird 访问新闻组的一个大优势是 Thunderbird 无法合并和拆分 split yenc

> 注意：你可以通过输入 `yum install pan` 获取 pan 包

尽管 Pan 最初是为 GNOME 桌面设计的，但现在运行 Pan 不再需要 GNOME 库。因此，Pan 现在可以在 KDE、Window Maker 或其他桌面环境中运行，无需任何特殊软件。

## 第二部分：使用 Fedora RHEL

要打开 Pan 新闻客户端，请在 shell 中输入 `pan`。第一次启动 Pan 时，Pan 向导将让您设置新闻阅读器。当您的电子邮件地址和新闻服务器名称准备就绪后，当向导完成后，您就可以从您的新闻服务器下载可用的新闻群组列表。

## 使用 Pidgin 进行即时通讯

Pidgin 是 Linux 中主要的即时通讯客户端。该项目最初基于美国在线 (AOL) 的开放 IM 架构 (www.aim.com)，最近它将其名称从 GAIM 改为 Pidgin。Pidgin 现在支持多种即时通讯协议，包括：

- `Oscar` —— 因为 Oscar 是 AOL 提供的官方 AIM 协议，因此它是 Pidgin 使用的最流行的协议。为了在 Pidgin 中运行，必须对 Oscar 进行反向工程，因为它是 AOL 的私有协议。因此，您在 AOL 自己的即时通讯软件中找到的所有功能并不都支持。消息通过基于 TCP 的网络（通常是互联网）传输，所有消息都通过 AOL 服务器传输，除非是直接连接的情况（这很难正确建立）。
- `MS Messenger` —— 该协议最初基于 Messenger Service 1.0 协议 (www.hypothetic.com/docs/msn/ietf_draft.txt)。自该协议首次发布以来，微软已对其进行了“增强”，因此 Pidgin 自带的版本必须经过反向工程。如需了解更多关于 MSN Messenger（通过 Pidgin 或其他方式），请查看 Messenger 协议资源/链接页面 (www.hypothetic.com/docs/msn/resources/links.php)。
- `ICQ` —— Pidgin 使用开源的 icqlib 实现 ICQ 协议。由于 ICQ 协议最近发生了变化，通常建议使用 Oscar 连接 ICQ 网络，而不是 icql。
- `IRC` —— 互联网中继聊天（IRC）协议基于互联网标准 RFC 1459。尽管不同的 IRC 服务器对该标准的实现存在差异，但这种基于 TCP 的协议在大多数 IRC 服务器上都应该正常工作。
- `Yahoo! Messenger` —— 这允许您使用 Yahoo! Messenger 与他人通信。

Pidgin 还支持其他消息协议。这些包括 Jabber（GoogleTalk 使用，可从 www.jabber.org 获取）、Napster（即时通讯和好友列表）、Groupwise Messenger（Novell 的即时通讯）、Sametime（来自 mentre.sourceforge.net 的 Lotus 消息）、TOC（用于非官方客户端的 AOL AIM 服务）以及 Zephyr（MIT 的 IM 系统）。Pidgin 不仅支持多种协议，还允许您同时通过多种协议进行通信。还有可用的 Jabber 服务器可以让您运行自己的 Jabber 即时通讯服务器，例如 Ejabber (http://ejabber.jabber.ru)。（输入 `yum install ejabber` 来安装该包。）

要从应用程序菜单启动 Pidgin，选择“互联网 -> 即时通讯”。图 9-8 包含了 Pidgin 好人列表和其他窗口的示例。

![](img/ec54a77854df1c8d0311d04a1e6b8d3c_436_0.png)

图 9-8：使用 Pidgin 访问您的 AOL或其他即时通讯账户。

如果您从未用过即时通讯，可以从 AOL (https://my.screenname.aol.com/) 或 MSN (http://messenger.msn.com) 免费注册账户。在 Pidgin 初始窗口中点击“账户”并添加您的账户。从账户列表中选择您的账户，选择并点击“登录”。

一旦您登录（例如登录 AOL），可以在“好人列表”选择 IM 按钮以连接到另一位在线的 IM 用户。或者选择“聊天”输入您想要进入的聊天室名称。您可以根据需要将好友添加到列表中。

当 Pidgin 运行时，桌面桌面上方的系统托盘中会出现一个黄色人形状的小图标。点击该图标可以使您的好人列表显示或隐藏。右键点击该图标会弹出菜单，您可以选择发送新消息、加入聊天或处理 Pidgin 账户和偏好设置。

## 使用 BitTorrent 文件

BitTorrent 是一种通过网络向大量客户端分发软件内容的工具。BitTorrent 的独特之处在于，当您向电脑下载文件时，其他人也可以从您的电脑下载同一个文件。这样一来，原始提供文件的服务器就不会被挤爆，可能无限数量的人可以快速获取该文件。
