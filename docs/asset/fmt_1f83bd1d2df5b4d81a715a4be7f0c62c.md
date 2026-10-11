
- 排序、搜索和显示 —— 再次，如果你管理数千封邮件，搜索功能可能是关重要的。某些客户端允许按日期、发送者、主题进行排序。
- 邮件编写 —— 某些编辑器允许你在邮件中包含 HTML，让你能够添加图像、链接、表格、颜色和其他视觉增强。警告：某些客户端仅允许发送纯文本。
- 多账户 —— 许多邮件客户端允许你同时配置多个账户。
- 性能 —— 特别是 Sylpeed 邮件客户端（随 Damn Small Linux 设计）是为了尽可能减少内存和处理能力，同时提供图形界面。从键盘运行的邮件客户端，特别是 `mut` 邮件客户端，其运行速度比完整的图形化邮件客户端（如 `Evolution`）快得多。

![](img/7021538f323e6521c571e727b770a451_180_0.png)

对于大多数用户和小企业用户，`Evolution` 和独立的 `Thunderbird` 通常可以在 Linux 桌面上可用，并带给你与你在 Microsoft Windows 客户端（如 Outlook Express）中相同的体验。如果你使用的是 KDE 桌面，可以使用 KDE 客户端 Contact，它包含了 `Kmail`（邮件客户端），以及联系人管理器、日历、事项列表等。

## 从 Windows 迁移

要了解如何将邮件客户端从 Windows 迁移到 Linux，你需要了解你的邮件客户端设置。无论你是使用 Outlook、Outlook Express 还是 Linux 中的其他客户端，以下是你应该：

- 服务器类型 —— 你的邮件服务器是 POP3 服务器还是 IMAP 服务器？如果是 IMAP 服务器，所有邮件都存储在服务器上。迁移到不同的邮件服务器可能意味着将新的邮件客户端指向你的服务器，并像一直以来那样使用邮件。如果是 POP3 服务器，你的邮件可能已经下载到了本地客户端。为了保留旧邮件，你需要以某种方式将当前的邮件文件夹转移到新客户端，这是一项具有挑战性的任务。

### 运行 Linux 桌面

（当你注册电子邮件帐户或互联网服务时，服务提供商应该告知你该服务是 POP3 还是 IMAP）。

- 通讯录 — 你需要将当前的通讯录导出为新电子邮件客户端可以读取的格式，并将其导入到新的电子邮件客户端中。

在过渡到 Linux 时，你可能希望在 Windows 系统中添加如 `Thunderbird` 之类的跨平台电子邮件客户端，以便在过渡到新邮件客户端期间能够获取你的资源（地址、存储的邮件消息等）。当你最终彻底离开 Windows 时，Linux 版本的 `Thunderbird` 的工作将与 Windows 版几乎完全相同。

如果你当前的电子邮件服务器是 Microsoft Exchange 服务器（2000、2003 或 2007），你需要获取 Microsoft Exchange 的 Evolution 插件（Evolution Plug-in），以允许 `Evolution` 访问该服务器的信息。对于 Fedora，你需要安装 `evolution-exchange` 软件包，然后在创建新电子邮件帐户时识别出你的 Microsoft Exchange 服务器。

## 开始使用电子邮件

大多数 Linux 系统都包含一个电子邮件客户端，你可以在面板上选择它，或者通过左键点击桌面调出菜单。在面板上寻找信封图标，或标记为“Internet”（互联网）的子菜单。如果你有图形化邮件阅读器，可以开始寻找这些客户端之一：`Evolution`、`Mozilla SeaMonkey`、`Thunderbird` 或 `KMail`。

启动选择的电子邮件客户端后，你需要一些信息来使用它。当你首次启动大多数图形化电子邮件客户端时，某种配置屏幕会帮助你设置帐户。以下是为本章描述的电子邮件客户端开始设置邮件帐户的方法：

- `Evolution` — 当用户第一次打开 `Evolution` 时，会启动 `Evolution` 设置向导。之后，在 `Evolution` 主窗口中选择“Edit（编辑）-> Preferences（偏选项）”。然后选择“Mail accounts（邮件帐户）”并双击你想修改的邮件帐户，或选择“Add（添加）”添加新帐户。
- `SeaMonkey Mail` — 第一次使用 `SeaMonkey Mail` 时会启动帐户向导。之后，你可以通过点击 `SeaMonkey Mail` 窗口中的“Edit Mail & Newsgroups Account Settings（编辑邮件与新闻组帐户设置）来设置或修改帐户。
- `Thunderbird` — 这是一个由使用 Firefox 和 Mozilla (`mozilla.org`) 的人员开发的下一代邮件客户端。目前已达到 2.0 版本，并具有更先进的功能，你可以考虑使用 `Thunderbird`。它不仅比 `SeaMonkey Mail` 和 `Evolution` 更快，而且是 Mozilla Firefox 浏览器的理想补充。Firefox 和 `Thunderbird` 运行在多种操作系统上，包括 Linux、Solaris、Microsoft Windows 和 Mac OS。
- `Sylphed` — `Sylphed` 电子邮件客户端 (`http://sylphed.sraoss.jp/en/`) 用于某些微型桌面发行版，例如 Damn Small Linux。`Sylphed` 特别快速高效，并支持强大的功能，如过滤、搜索、垃圾邮件控制以及数字签名和加密（使用 GnuPG）。
- `KMail` — 在 `KMail` 窗口中，选择 Settings（设置）Configure KMail（配置 KMail）。在出现的 Configure KMail 窗口中，选择 Network（网络）图标。从那里，你可以点击 Sending（发送）或 Receiving（接收）来配置你的发送和接收电子邮件设置。

基于文本的客户端的初始配置将在本章后面描述。

配置电子邮件帐户所需的信息对于本章涵盖的不同图形化电子邮件客户端是相同的：

- `Name（名称）` — 输入你希望在发送时显示的名称。
- `Email Address（电子邮件地址）` — 输入你发送时的电子邮件地址。如果你希望回复到发送地址以外的地址，系统也可能为你提供提供不同的回复地址的机会。
- `Mail server type（邮件服务器类型）` — 大多数邮件服务器都是 POP3 或 IMAP 服务器。（配置这些类型的服务器将在第 14 章中讨论）。
- `Server names（服务器名称）` — 输入你用于发送和接收电子邮件的服务器名称。这些名称可以是完全限定域名（例如 `mail.linuxoys.net`）或 IP 地址。在许多情况下，入站和出站邮件服务器是同一个。
- `Username（用户名）` — 输入服务器识别你时的名称。例如，如果电子邮件地址是 `chris@linuxoys.net`，那么你在 `mail.linuxoys.net` 服务器上的用户名可能只是 `chris`。不过，你在邮件服务器上的用户名可能不同，因此你应该向邮件服务器的管理员核实。
- `Account title（帐户标题）` — 输入你想要给此邮件帐户起的名称，以便稍后在邮件和新闻组帐户列表中引用它。
- `Authentication type（身份验证类型）` — 指定你在接收邮件时使用的身份验证类型（有时发送邮件时也需要身份验证）。密码验证是正常的。如果你愿意，通常可以让电子邮件客户端记住你的密码。通常，在你第一次连接邮件时，系统会提示输入密码。

这就是你开始并获取电子邮件所需的大部分基本信息。然而，你可能想调整电子邮件客户端在获取和发送邮件时的交互方式。

## 调整电子邮件

完成基础设置后，你应该准备好开始发送和接收电子邮件了。在此之前，你应该考虑一些影响你使用邮件的其他设置：

- `Automatically check messages（自动检查邮件）` — 你可以设置电子邮件客户端自动检查并下载电子邮件。

### 运行 Linux 桌面

- Leave messages on server（在服务器上保留邮件） — 如果使用 POP3，可以将邮件留在服务器上。
- Certificates（证书） — 许多电子邮件客户端使用证书签名证明身份。

## 使用 Thunderbird 阅读邮件

`Thunderbird` 电子邮件客户端是一个强大的工具。它包含以下功能：

- 发送、接收和阅读邮件
- 管理新闻组帐户
- 编写 HTML 消息
- 控制垃圾邮件

### 电子邮件与网页浏览

## 设置电子邮件帐户

当你首次启动 `Thunderbird` 时，应用程序显示“New Account Setup（新帐户设置）”，引导你设置电子邮件帐户。图 6-1 显示了此窗口。

图 6-1

Thunderbird 新帐户设置![](img/7021538f323e6521c571e727b770a451_184_0.png)

按照以下步骤创建你的电子邮件帐户：

1. `创建电子邮件帐户。` 要开始设置电子邮件帐户，选择“Email Account（电子邮件帐户）”并点击“Next（下一步）”。出现身份屏幕。
