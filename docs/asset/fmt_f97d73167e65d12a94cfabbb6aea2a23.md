
# 在 Ubuntu 上使用 Empathy 进行即时消息

## Windows

适用于 Ubuntu 系统的 Pidgin IM 客户端版本适用于 Windows（`www.pidgin.im/download`），因此这是我推荐的软件包。另一个流行的 Windows 源 IM 客户端是 Miranda-IM（`www.miranda-im.org`）。在专利闭源 IM 客户端方面，Windows 最流行的原生多协议客户端是 Trillian（`www.ceruleanstudios.com`），它也在移植到 Mac OS X。另一个流行的 Windows 多协议客户端是 Qnext（`www.qnext.com/universal_messenger.shtml`）。

## Mac OS X

Ads 仅通过巨大的软件包 Fink（`http://www.pidgin.im/download/mac/`），因此 Mac 用户应该使用 Adium（`www.adium.com`），它是平台上最流行的多协议客户端。

有关 IM 客户端的详尽信息，请参考维基百科上的即时消息对比：`http://en.wikipedia.org/wiki/Comparison_of_Instant_messaging_clients`。

如果你不确定，大问题是“我应该和谁注册？”这个问题的答案是“你的朋友在哪里？”虽然 Empathy 和 Pidgin 等多协议客户端允许你发送和接收来自多个服务的即时消息，但你仍然需要注册这些服务，人们才能通过它们发送即时消息。

虽然使用有限协议、闭源协议站点（如 AIM、MSN Messenger 或 Yahoo）只会鼓励专有协议和工具的持续，能够与你的

## 第二部分：面向桌面用户的 Ubuntu

这可能比哲学更重要。消息是，由于大多数即时消息账户都是免费的，你可以注册任意数量的即时消息服务，并使用多协议客户端与你的所有朋友通信。

### 注意

如果你已经在使用如 AOL、Microsoft Live/Hotmail、Google 或 Yahoo 等免费互联网服务，你可能已经通过该服务拥有了一个即时消息账户。登录你的 Web 账户并查找 FAQ（常见问题解答）或关于 IM 支持的常规信息。在大多数情况下，你的用户 ID 与你的电子邮箱地址相同，但不包含任何域名信息。例如，如果你的电子邮箱地址是 `wonhagen@yahoo.com`，那么你的 Yahoo ID 几乎肯定是 `wonhagen`。

以下是一些可以免费注册即时消息账户的流行地点列表：

- AOL：Mirabilis 的 ICQ 软件的账户，称为 AIM (AOL Instant Messenger)，它是即时消息领域的原始先驱，目前仍然是最流行的 IM 站点之一。你可以从 `www.aim.com` 获取免费的 AIM 身份（因为其根源于 AOL，所以有一个显示名称），它附带了一个 `aim.com` 邮件邮箱账户。同样，你可以通过 `www.aol.com` 注册免费电子邮件来获取 AIM 账户。AIM 的底层通信协议称为 Oscar。

- Google：为了让 Google 不错过在线生活的任何方面。Google Talk (`www.google.com/talk`) 是一个即时消息平台，你可以通过用于 Gmail 的同一个 Google 账户访问它。如果你没有 Google 账户，启动 Google Talk 会提供创建账户的链接。并不意外的是，Google Talk 使用浏览器界面进行即时消息和聊天，因此它几乎都能运行。Google Talk 使用 XMP（可扩展消息和存在协议）作为其底层协议。

- ICQ：尽管使用数字 ID，但 ICQ 普及了即时消息并且仍然是一个流行的站点。你可以在 `https://www.icq.com/register` 注册 ICQ 账户。由于 AOL 在很久以前买下了 ICQ，它也使用 Oscar 作为底层协议。

- Jabber：Jabber 是一个开源即时消息平台，其宣传材料显示，“……你的消息不会被 AOL、Microsoft 或 Yahoo 等任何公司监控。”（即时，由一家非常小的公司监控）。Jabber 使用 XMPP（可扩展消息和存在协议），Google Talk 也在使用该协议。要注册 Jabber，当你使用 Jabber 使用的任何站点时，你的 IM 客户端将自动为你创建一个账户（列表参见 `www.jabber.com/im-services`）。

- Microsoft：Microsoft 提供 Live 账户（以前称为 Hotmail），这些账户附带免费的 Windows Live Messenger（以前称为 MSN Messenger）账户，因为你所有的 Microsoft 账户都共享同一个身份。访问 `http://login.live.com` 注册账户。我知道你会发现 Microsoft 使用它自己的专有 IM 协议进行即时消息通信。

- Yahoo：Yahoo 提供即时消息服务已经很长时间了，Yahoo Messenger 软件非常流行。当你注册 Yahoo 电子邮件账户 (`www.yahoo.com`) 时，你就获得了即时消息功能。像 Microsoft 一样，Yahoo 使用自己的协议进行即时消息。

## 第 10 章：发送和接收即时消息

这些只是 IM 领域的大线条。请参考本章关于 Pidgin 和 Empathy 的后续章节，获取有关这些即时消息客户端所支持的协议的信息。

尽管我承认有点害怕“谷歌巨兽”（Googlezilla），但如果让我为你自己的 IM 推荐这些站点之一，我会推荐 Facebook Google Talk，仅仅因为你可以使用 Gmail 以及许多其他实用的 Google 工具。因为它是一个使用标准协议的开源软件，Jabber 紧随其后，如果你的大多数朋友也是 Linux 粉丝的话。如果不是，Yahoo 和 AIM 是你的最佳选择。

Empathy 是最新 Ubuntu 桌面系统默认安装的即时消息客户端。Empathy 替换了一个名为 Pidgin 的旧版即时消息客户端，Pidgin 仍然流行，因此在本章的后续章节中进行了讨论。毕竟，开源软件的核心在于选择！

Empathy 是一个多协议即时消息客户端，允许你从 AIM、Facebook Chat、Google Talk、Groupwise、ICQ、IRC、Jabber、MSN、Skype、SIP、Yahoo! 以及许多其他即时消息服务发送和接收即时消息。Empathy 使用名为 Telepathy 的底层框架，与 Linux 系统交换消息的标准低级通信机制接口。对于像你这样的用户，这意味着 Empathy 不仅限于即时消息，还可以处理视频聊天和 IP 语音（VoIP）。Telepathy 还可以扩展以处理来自大学、开源社区以及明天初创公司的新型通信机制和相关协议。

### 启动 Empathy

Ubuntu 提供了两种与 Empathy 交互的方式：

- 通过选择“应用程序-互联网-Empathy IM”项目来实际启动 Empathy

- 使用图 10-1 所示的面板菜单组件（Menulet）。此应用允许你在 Empathy 中配置激活的即时消息账户，显示你的当前状态，并监控传入的对话，当从任何激活即时消息账户的任何好友处接收即时消息时，显示 OSD（屏幕显示）通知。

此应用仅向你告知传入的消息——它不会替你启动 Empathy。OSD 通知同时显示消息内容和发起消息的好友名称。一旦你启动了 Empathy，任何来自传入的未应答消息的好友将在 Empathy 中闪烁。

### 第二部分：面向桌面用户的 Ubuntu

图 10-1

Ubuntu 的菜单组件

![](img/c20ef7a2778ee7a3a4ec401.png)

如果你已经在使用如 AOL、Microsoft Live/Hotmail、Google 或 Yahoo 等免费互联网服务，你可能已经通过该服务拥有了一个即时消息账户。登录你的 Web 账户并查找 FAQ（常见问题解答）或关于 IM 支持的常规信息。在大多数情况下，你的用户 ID 与你的电子邮箱地址相同，但不包含任何域名信息。例如，如果你的电子邮箱地址是 `wonhagen@yahoo.com`，那么你的 Yahoo ID 几乎肯定是 `wonhagen`。

以下是一些可以免费注册即时消息账户的流行地点列表：

……上……

## 第 10 章：发送和接收即时消息

这些只是 IM 领域的大线条。请参考本章关于 Pidgin 和 Empathy 的后续章节，获取有关这些即时消息客户端所支持的协议的信息。

尽管我承认有点害怕“谷歌巨兽”，但如果让我为你自己的 IM 推荐这些站点之一，我会推荐 Facebook Google Talk，仅仅因为你可以使用 Gmail 以及许多其他实用的 Google 工具。因为它是一个使用标准协议的开源软件，Jabber 紧随其后，如果你的大多数朋友也是 Linux 粉丝的话。如果不是，Yahoo 和 AIM 是你的最佳选择。
