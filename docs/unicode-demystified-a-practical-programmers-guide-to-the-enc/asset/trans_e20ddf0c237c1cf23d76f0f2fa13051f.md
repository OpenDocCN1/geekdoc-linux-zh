

# Usenet

Usenet 是互联网上最早的信息服务之一，是一个电子公告板，允许具有共同兴趣的用户交换信息。Usenet 是一个非正式的、松散连接的系统网络，用于交换电子邮件和新闻（通常称为 netnews）。Usenet 于 1979 年形成，当时少数站点决定共享某些共同主题的软件和信息。他们同意彼此连接，并通过拨号电话线传输信息（当时最快运行速度仅为 1200 波），使用 UNIX uucp 实用程序（Unix 到 UNIX 复制程序）。

Usenet 的流行导致 uucp 发生了重大变化，以处理日益增长的消息和站点。今天，大部分新闻通过一种专门为此设计的复杂协议传输：NNTP（网络新闻传输协议）。消息以标准格式存储，许多流行的领域程序可以让你阅读。一个旧简单的界面名为 readnews。其他的如 rn、其 Window 系统兄弟 rin、tin 和 xx 许多帮助你浏览和回复可用文章或创建自己文章的功能。此外，Netscape 和 Mozilla 包含一个可以在 Web 浏览器中使用的新闻阅读界面（Netscape/Mozilla）。选择哪种程序来读取 netnews 大程度上取决于个人喜好。

因为读取 netnews 文章的程序已移植到非 UNIX/Linux 系统，netnews 用户社区已变得多样化。在 UNIX 传统中，新闻组按分级结构分类。顶层包括分类如 comp（计算机相关）、mis（杂项）、rec（娱乐）、sci（科学）、soc（社会问题）和 talk（进行中的讨论）。通常至少有一个区域类别位于顶层，例如 ba（旧金山湾区），并包含有关本地事件的信息。许多新类别不断被添加到超过 30,000 个新闻群组中。新闻组的名称代表域名，但从左到右读取（类似于 GNU/Linux 文件名）：comp.UNIX.misc、comp.lang.c、misc.jobs.offered、rec.skiing、sci.med、soc.languages。以下文章出现在 linux.redhat.install：

> 我刚刚安装了 linux redhat 7.2，当我尝试启动 X 时，得到了
> 以下错误消息：
>
> 致命服务器错误 (Fatal Server Error)
> 未找到屏幕 (no screens found)
>
> XIO: 致命 IO 错误 104 (由对端重置连接) 在 X 服务器 "0.0" 上，
> 经过 0 个请求 (0 个已处理)，剩余 0 个事件。
>
> 我该如何解决这个问题？
>
> 谢谢，
> Fred

# Fred，

似乎你的 X 配置不正确或缺失了。你应该运行 XConfigure 并为你的显卡和显示器设置配置。你可能还需要运行 mouseconfig 来进行设置。

# Carl

Usenet 上提供了许多有用的信息，但你需要耐心和毅力才能找到你寻找的内容。你可以提问（正如上一个例子中的用户做的那样），来自地球另一端的人可能会回答它。在提出这样一个简单的问题并使其出现在世界上成千上万个系统中之前，问问自己是否可以通过不具侵入性的方式获得帮助。

- 参考 man 手页（man pages）和 info。
- 浏览 /usr/share/doc 下的文件。
- 向你的系统管理员或其他用户寻求帮助。
- 所有热门新闻组都有 FAQs（常见问题列表）。查阅这些列表，看看你的问题是否已被解答。FAQs 定期发布在新闻组；此外，FAQs 还归档在互联网各处的站点，包括 http://ftp.uu.net、ftp://rtfm.mit.edu/pub/usenet-by-hierarchy,22 以及 Usenet 新闻组 comp.answers。
- 可能有人在你之前问过相同的问题，请搜索 netnews 存档寻找答案：尝试查看 groups.google.com，那里有完整的 netnews 存档。
- 使用搜索引擎寻找答案。获取帮助的好方法之一是搜索错误信息。
- 查看 www.redhat.com 上的支持文档。
- 联系 Red Hat Linux 用户组。

将全球 Usenet 社区作为最后的手段。如果你在 GNU/Linux 问题上卡住了且找不到任何其他帮助，请尝试将其提交给这些新闻组之一：

- linux.redhat.development
- linux.redhat.install
- linux.redhat.misc

对于更通用的问题，尝试这些列表：

- comp.os.linux.misc
- comp.os.linux.networking
- comp.os.linux.security
- comp.os.linux.setup
- linux.dev.newbie
- linux.redhat.rpm

发现新工具和服务的的一种方法是阅读 Usenet 新闻。comp.os.linux.hierarchy 对 GNU/Linux 用户特别感兴趣；例如，关于新发布的 GNU/Linux 软件的新闻发布在 comp.os.linux.announce。人们经常在那里发布免费软件的可用性，并附带如何使用匿名 FTP 获取个人副本的说明（第 380 页）。网络上还存在其他帮助你发现新旧资源的工具；见附录 B。

## 教程：使用 pine 作为新闻阅读器

pine 新闻界面类似于 pine 邮件界面（第 88 页），在命令、屏幕显示和文件夹组织之间尽可能保持一致性。这种一致性使得习惯了 pine 的人更容易将 pine 作为新闻阅读器。如果你正在使用 Mozilla，你可能更倾向于使用 Mozilla News（第 405 页）。

为了使用任何新闻阅读器，你必须访问 Usenet 新闻。向你的 ISP 或系统管理员询问新闻服务器地址。

启动 pine 并从 MAIN MENU 选择 SETUP。在 SETUP 屏幕上输入 c (Config) 显示 SETUP CONFIGURATION 屏幕，你可以在其中查看并修改 pine 行为的许多配置方面（图 9-4）。高亮 pine 变量 ntp-server，选择 a (Add Value) 并输入你的新闻服务器的 URL。

在大多数情况下，这就是开始使用 pine 作为新闻阅读器所需的所有操作。当你下次运行 pine 时，它发出读取和发布新闻的命令时将为你联系新闻服务器。

# 第 9 章 网络与互联网

![](img/aa8214d49e1cf50152c432845129fb3b_451_0.png)

图 9-4 pine 的设置/配置屏幕

如果你使用 pine，你可能习惯了包含 INBOX（收件箱）、sent-mail（已发送）和 saved-messages（保存的消息）的 F LIST 屏幕。如果这个组或集合只有一个文件夹，pine 将显示 FOLDER 屏幕。一旦设置了新闻，会自动定义额外的集合——News，F LIST 屏幕变为显示两个文件夹：Mail 和 News。高亮 News 行并按 RETURN。

FOLDER LIST 显示文件夹，每个文件夹对应一个你订阅的新闻组。你可以使用方向键在新闻组之间移动；按 RETURN 选择任何新闻组。

![](img/aa8214d49e1cf50152c432845129fb3b_451_1.png)

图 9-5 pine 的文件夹列表

## 订阅新闻组

位于主目录下的新闻订阅文件 .newsrc 被 pine 用于跟踪你的新闻订阅。它是许多新闻阅读器都可以使用的标准格式。你可能会在主目录下发现此文件，它初始化了一些认为感兴趣的新闻组列表。如果没有，pine 将你第一次订阅新闻组时为你创建该文件。

此时可能很有用的新闻组是 comp.mail.pine。要订阅此新闻组，在仍在新闻组 F LIST 屏幕时，在提示符处输入 a (Add) 以及 comp.mail.pine 并按 RETURN。过一会儿，pine 会在消息行显示 Subscribed to "comp.mail.pine"，并将新新闻组添加到 F LIST 屏幕显示的新闻组列表中。取决于你的环境，订阅新闻组的每个步骤可能需要一段时间。

要显示所有标题中包含 Linux 的新闻组，在给出 (Add) 命令的提示符处输入 linux。（图 9-6 显示了查询的部分结果）。在给出显示所有组列表的命令后立即按 RETURN（列表很长，显示需要时间）。

## 阅读新闻

使用 ARROW（方向）键高亮 F LIST 屏幕上显示的一个新闻组，然后按 RETURN 显示消息索引屏幕。如果你看到消息“Group 正在下载”，请稍后再试，< 返回

