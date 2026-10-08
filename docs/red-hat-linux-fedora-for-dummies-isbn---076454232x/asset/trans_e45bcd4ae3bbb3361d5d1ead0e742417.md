
## 理解 URL

你是否曾好奇过 URL 的各个部分是什么意思？通过访问像 `http://localhost:8000/track1.ogg` 这样的 URL 来连接流媒体音频服务器，我们想分析一下这些部分各自意味着什么以及它们的作用。以下列表描述了每个 URL 元素的功能：

- **协议（Protocol）：** Icecast2 使用超文本传输协议（HTTP）数据包来封装音频流。HTTP 是一个不错的选择，因为配置防火墙以允许 HTTP 连接非常容易。
- **地址（Address）：** Icecast2 服务器的 IP 地址。地址可以是域名形式，也可以是数字形式。例如，你可以将 localhost 替换为其数字地址 `127.0.0.1`。
- **端口（Port）：** Icecast2 用于监听 TCP 连接请求的端口号。Icecast2 默认使用端口 `8000`；你可以通过修改 Icecast2 配置文件轻松地更改端口。
- **挂载点（MountPoint）：** 此组件指定要连接的 Icecast2 流。Icecast2 能够播放两个流。在这个示例中，你使用的是内容文件 `track1.ogg`，你可能在前一节中已经创建了该文件。

以下步骤描述了如何配置你的 Icecast2 服务器以在你的私有网络上进行广播。

1. 以 root 身份登录，并通过点击 GNOME 菜单并选择**配件 文本编辑器（Accessories Text Editor）**来打开 Gedit 文本编辑器。
2. 在 Gedit 窗口中，选择**文件 打开（File Open）**。
3. 选择 `/usr/local/etc/icecast.xml` 并点击**确定（OK）**。
4. 更改回环地址 `127.0.0.1` —— 即你 Icecast2 服务器的 IP 地址。例如，如果你的服务器 IP 地址是 `192.168.1.1`，请按照此处所示修改文件；同时也请相应地更改主机名：

```xml
<hostname>veracruz</hostname>
<port>8000</port>
<bind-address>192.168.1.1</bind-address>
<master-server>192.168.1.</master-server>
```

注意端口号没有改变。

5. 更改默认密码。否则，任何下载 Icecast2 软件包的人都可以确定你的密码：

```xml
<source-password>givememusic</source-password>
<relay-password>givememusic</relay-password>
```

6. **修改电子邮件和位置信息以匹配你的网络。**

这能让任何听众大致了解你是谁以及你来自哪里。

```xml
<location>Hi-Fi Paunchy</location>
<admin>oldgomez@paunchy.net</admin>
```

7. **点击保存按钮保存你的更改，并在 Gedit 中打开 /usr/local/etc/ices-playlist.xml 文件。**

8. **修改文件，使 Ices2 联系 Icecast2 服务器：**

```xml
<hostname>veracruz</hostname>
<port>8000</port>
<password>givememusic</password>
<mount>/track1.ogg</mount>
```

9. **保存你的更改并关闭 Gedit 窗口。**

10. **打开一个 GNOME 终端窗口并启动服务器：**

```bash
killall -9 icecast ices
icecast -c /usr/local/etc/icecast.xml &
ices /usr/local/etc/ices-playlist.xml &
```

11. **输入此命令以启动 XMMS 并连接到新配置的 Icecast2 流：**

```bash
xmms http://192.168.1.1:8000/track1.ogg
```

如果你愿意，也可以使用 MPlayer 来监听流媒体：

```bash
mplayer http://192.168.1.1:8000/track1.ogg
```

## 第五部分

## 十项精选

## 第 $5^{th}$ 浪潮

作者 Rich Tennant

![](img/8c094d1b36276212c03d10d898508a6e_312_0.png)

*“我们来这里清理代码。”*

## 在本部分……

啊，这是每本 For Dummies 书里都会有的部分：十项精选。在这里，我们可以随意浏览，整理出十个这个和十个那个。

在第 20 章中，我们列出了一些经常遇到的问题（及其解决方案）。

不幸的是，世界仍然是一个充满危险的地方。第 21 章概述了十种计算机安全威胁。我们描述如何在被称为互联网（Internet）的“狂野西部”中变得更安全一点。

# 第 20 章

## 十个问题领域及解决方案

### 本章内容

- 查找有关 Linux 的信息
- “我忘记密码了”
- “我忘记 root 密码了”
- “我需要破解我自己的计算机！”
- “我想更改 GRUB 启动顺序”
- “当我启动进入 Windows 时，会进入恢复过程”
- “我的网络在工作，却又没在工作”
- “我想制作一个紧急启动盘”
- “我无法从我的 DVD 启动”
- “Linux 找不到 shell 脚本（或程序）”
- “我不知道如何让 X 窗口系统在启动时启动”
- “我的时间似乎总是不对”

在任何技术场景中，人们最终都会遇到需要帮助的问题和困境。本章旨在帮助回答人们在使用 Red Hat Linux 时遇到的最常见的问题。

### “救命！我需要帮助！”

在深入解决具体问题之前，本章首先介绍了几个信息来源。因为我们要无法涵盖超过几个最常见的问题，所以我们首先为你指出可以找到更多信息和帮助的方向。

### 书籍及更多书籍

多年前当我们使用计算机时，关于计算机的书籍数量还填不满一个书架，而且它们大多讲述的是硬件本身的电子学知识。网络书籍专注于诸如两个以太网数据包碰撞的概率等主题，而不是如何构建简单的网络。几乎没有关于计算机的书籍出现在大众书店里。如今有数千本关于计算机的书籍可供参考；大多数描述的是软件及其交互，硬件则退居次要地位。像*For Dummies*系列这样的书不再仅限于书店。你还可以在大众市场场所找到它们，例如当地的超级市场。

![](img/8c094d1b36276212c03d10d898508a6e_315_0.png)

关于*For Dummies*书籍的一个绝佳信息来源是电视系列剧*The Simpsons*（《辛普森一家》）。该节目特别喜欢*For Dummies*的作者，并为我们提供了惊人的准确描绘。哎呀！

也许你在购买这本书之前看过其他书籍，却被它们使用的技术术语吓到了。或者，你认为其他书对于你想做的事情来说太通用了，你想要一些更具任务导向的内容。你可能想再看看那些书，因为读完这本书后，你的知识水平应该会更高。TCP/IP 网络、编译器设计、操作系统理论、形式语言理论、计算机图形学和系统管理培训都是当你拥有一台 Linux 计算机时可以深入研究的话题。

许多专门关于 Unix 操作系统的书籍在部分或全部方面都适用于 Linux，例如关于 Perl（一种全面的解释器）的书籍。通过获取一本（或多本）关于 Perl 的书籍并与你的 Linux 系统坐在一起，你不仅拥有了一个新的工作工具，还对一种完整的编程语言有了新的 appreciation（欣赏/理解）。如果你想了解如何编写 Perl，你可以直接查看源代码。

### Linux HOWTOs 和 Red Hat 手册

别忘了随 Red Hat Linux 商业版本提供的 Linux HOWTOs。这些优秀的 Linux 指南受 Linux 文档项目（LDP）的*版权保留（copyleft）*保护，这意味着你可以打印它们。

Red Hat 还提供了在线版本的手册，这是你购买其完整发行版时获得的手册。查看 `www.redhat.com/docs/manuals/linux/RHL-10-Manual` 以获取有关 Red Hat Linux 几乎每个方面的信息。

### 校园时光

获取更多关于 Unix 和 Linux 信息的另一种方式是上课，也许是在当地的社区大学。许多大学提供 Unix 课程，一些大学已经开始使用 Linux 来教授它们的 Unix 课程。你可以在家里的系统上做作业，或者，如果你有一台笔记本电脑（laptop computer），你可以在任何地方工作。（Jon 在本书第一版中是在新西兰奥克兰的一家酒店输入文字的，并在美国航空公司的芝加哥休息室更新了第二版的文字。）我们在大学时多么希望有机会坐在自己舒适的酒吧——呃，宿舍房间里做计算机项目。相反，我们不得不坐在一个堆满了打孔卡机器的房间里——好吧，不说了。如果我们有一个 Linux 系统，我们会更舒服、更高效。

### 在新闻中

你可以从互联网上的邮件列表和新闻组获取有关 Linux 操作系统的额外信息。事实上，互联网最早流行的用途之一就是 Usenet 信息共享系统。Usenet 类似于万维网，因为它使用一组协议在通用互联网上进行特殊类型的通信。Usenet 提供了让人们通过电子邮件参与讨论的能力。人们将消息发布到一个特定的兴趣组，任何人都可以查看和回复。

新闻组和邮件列表专注于特定主题：技术或两个以上的人（或一个拥有多重人格的人）感兴趣的任何主题。几十个个新闻组和邮件列表专门致力于 Linux 主题。搜索这些组通常能为你的问题提供如激光般精准的答案。这是因为其他人很有可能已经遇到过你的问题并找到了解决方案。必要时，你也可以将你的问题发布到新闻组。

你可以例如在 www.dejanews.com 和 www.mailgate.org 搜索新闻组。Google 也提供了一个名为 Google Groups 的优秀机制来搜索小组，位于 www.google.com/advanced\_group\_search。

别忘了直接查看 Red Hat 邮件列表，地址为 https://listman.redhat.com/mailman/listinfo。此网页提供了所有 Red Hat 组的摘要。

