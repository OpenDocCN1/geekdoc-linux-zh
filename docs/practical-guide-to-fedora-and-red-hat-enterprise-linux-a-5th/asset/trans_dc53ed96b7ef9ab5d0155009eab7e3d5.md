
## RPC 客户端/服务器通信

RPC 客户端和服务器之间通信的事件序列如下：

- 1. 客户端系统上的客户端程序发起 RPC 调用，以从（远程）服务器系统获取数据。（客户端发出“从文件读取记录”的请求。）
- 2. 如果 RPC 尚未为客户端程序与服务器系统建立连接，它会联系服务器 111 端口上的 `rpcbind`/`portmap`，询问目标 RPC 服务器正在监听哪个端口（例如 `rpc.nfsd`）。
- 3. 远程服务器上的 `rpcbind`/`portmap` 守护进程查询其表，并向本地系统（客户端）返回一个 UDP/TCP 端口号（对于 `nfs` 通常是 `2049`）。
- 4. 服务器系统上的 RPC 库接收来自客户端的调用，并将请求传递给适当的服务器程序。服务器程序对请求的来源是透明的。（文件系统接收“从文件读取记录”的请求。）
- 5. 服务器响应请求。（文件系统读取该记录。）
- 6. 远程服务器上的 RPC 库通过网络将结果返回给客户端程序。（读取的记录被返回给调用程序。）

### RHEL

由于标准的 RPC 服务器通常由 `xinetd` 守护进程（第 445 页）启动，因此必须在调用 `xinetd` 守护进程之前启动 `portmap` 守护进程。init 脚本（第 426 页）确保 `portmap` 在 `xinetd` 之前启动。您可以通过查看 `/etc/rc.d/*/S*portmap` 和 `/etc/rc.d/*/S*/xinetd` 相关的数字来确认此顺序。如果 `portmap` 守护进程停止，您必须重启本地系统上的所有 RPC 服务器。

## USENET

Usenet 是互联网上最早可用的信息源之一，它是一个电子公告板，允许具有共同兴趣的用户交换信息。Usenet 由一个非正式的、松散连接的系统网络组成，这些系统交换电子邮件和新闻项目（通常称为 *netnews*）。它形成于 1979 年，当时一些站点决定共享一些软件以及关于共同兴趣主题的信息。他们同意相互联系，并通过拨号电话线路（当时最高运行速度为 1,200 波特）传递信息，使用 UNIX 的 `uucp` 实用程序（UNIX-to-UNIX copy program）。

Usenet 的流行导致 `uucp` 发生重大变化，以处理不断升级的消息量和站点数量。如今，大量的新闻通过网络链路流动，使用一种专为此目的设计的复杂协议：NNTP（Network News Transfer Protocol，网络新闻传输协议）。新闻消息以标准格式存储，并且有许多可用的公共领域程序让您读取它们。一个古老且简单的接口名为 **readnews**。其他接口，如 `rn`、其 X 窗口系统表亲 `xrn`、`tin`、`nn` 和 `xnews`，具有许多功能，可帮助您浏览或回复可用的文章，或创建您自己的文章。此外，Netscape 和 Mozilla 包含一个接口，您可以将其作为其 Web 浏览器的一部分来读取新闻（Netscape/Mozilla News）。读取 netnews 最简单的方法之一是访问 groups.google.com。您选择用于读取 netnews 的程序在很大程度上取决于个人喜好。

随着读取 netnews 文章的程序被移植到非 UNIX 和非 Linux 系统，netnews 用户社区变得越来越多样化。遵循 UNIX 传统，netnews 组的分类结构具有层次性。顶级包括 **comp**（计算机相关）、**misc**（杂项）、**rec**（娱乐）、**sci**（科学）、**soc**（社会问题）和 **talk**（持续讨论）等指定。通常，至少有一个区域分类位于顶级，例如 **ba**（旧金山湾区），并包含当地活动的信息。新的分类不断添加到超过 30,000 个新闻组中。新闻组的名称类似于域名，但从左到右读取（类似于 Linux 文件名）：`comp.os.unix.misc`、`comp.lang.c`、`misc.jobs.offered`、`rec.skiing`、`sci.med`、`soc.singles` 和 `talk.politics` 仅是一些示例。以下文章出现在 `linux.redhat.install` 中：

> 我刚安装好 Fedora 12，当我尝试启动 X 时，我得到了
> 以下错误消息：
>
> Fatal Server Error.
> no screens found
>
> XIO: Fatal IO error 104 (connection reset by peer) on X server "",0.0" after
> 0 requests (0 known processed) with 0 events remaining.
>
> 我如何解决这个问题？
>
> 谢谢，
> Fred

Fred，

看起来您的 X 配置不正确或缺失。您应该运行 `system-config-display` 并为您显卡和显示器设置配置。

Carl

Usenet 上有很多有用的信息，但您需要耐心和毅力才能找到您正在寻找的内容。您可以提出问题，就像前一个例子中的用户那样，世界上另一半的某人可能会回答。然而，在提出这样一个简单的问题并使其出现在全球成千上万的系统上之前，请先问问自己是否可以用侵入性较小的方式获得帮助。尝试以下方法：

- 参考 `man` 页面和 info。
- 浏览 `/usr/share/doc` 中的文件。
- 请求系统管理员或另一位用户的帮助。
- 所有流行的新闻组都有 FAQ（常见问题列表）。查阅这些列表，看看您的问题是否已被回答。FAQ 定期发布到新闻组；此外，所有 FAQ 都归档在互联网上的站点，包括 Google 群组（[groups.google.com](http://groups.google.com)）。
- 因为有人可能之前已经问过同样的问题，请在 netnews 档案中搜索答案。尝试查看 [groups.google.com](http://groups.google.com)，它拥有完整的 netnews 档案。
- 使用搜索引擎查找答案。获取帮助的一个好方法是搜索错误消息。
- 审阅 **www.redhat.com** 上的支持文档。
- 联系 Fedora/RHEL 用户组。

将查询发布到全球 Usenet 社区应作为最后的手段。如果您卡在 Linux 问题上且找不到其他帮助，请尝试将其提交到以下新闻组之一：

- `linux.redhat.install`
- `linux.redhat.misc`

对于更通用 的问题，尝试这些列表：

- `comp.os.linux.misc`
- `comp.os.linux.networking`
- `comp.os.linux.security`
- `comp.os.linux.setup`
- `linux.redhat.rpm`

了解新工具和服务的一种方式是通过阅读 Usenet 新闻。`comp.os.linux` 层次结构对 Linux 用户特别有趣；例如，关于 Linux 新发布软件的消息会发布在 `comp.os.linux.announce` 中。人们经常在那里宣布免费软件的可用性，并附上说明如何使用匿名 FTP（第 649 页）获取副本以供自己使用的说明。网络上还存在其他帮助寻找资源的工具，无论是旧的还是新的；参见附录 B。

## WWW：万维网

万维网（WWW、W3 或 Web）为存储在世界各地计算机上的大量信息提供了统一、互连的接口。催生万维网的理念来自欧洲粒子物理实验室（CERN）的 Tim Berners-Lee（www.w3.org/People/Berners-Lee），他是为了响应改善高能物理界通信需求而提出这一理念的。第一代解决方案是一个名为 Enquire 的笔记本程序（*Enquire Upon Everything* 的缩写，这是 Berners-Lee 童年时期一本书的名字），他于 1980 年在一台 NexT 计算机上创建，并支持命名节点之间的链接。直到 1989 年，这一概念才作为一个全球超文本项目被提出，即后来被称为万维网的项目。1990 年，Berners-Lee 撰写了一份关于超文本项目的提案，最终产生了 HTML（Hypertext Markup Language，超文本标记语言），即 Web 的通用语言。万维网程序于 1991 年夏天在互联网上可用。通过设计能与现有协议（如 FTP 和 gopher）协同工作的工具，创建 Web 的研究人员产生了一个通常对许多类型的信息和许多类型的硬件及操作系统都有用的系统。

WWW 是客户端/服务器范式的另一个例子。您使用 WWW 客户端应用程序，或称 *浏览器*，来检索和显示存储在服务器上的信息，该服务器可能位于您的本地网络或互联网的任何地方。WWW 客户端可以与许多类型的服务器交互。例如，您可以使用 WWW 客户端联系远程 FTP 服务器并显示其提供的用于匿名 FTP 的文件列表。最常见的是，您使用 WWW 客户端联系 WWW 服务器，该服务器提供支持本章剩余部分描述的万维网特殊功能。

Web 的强大功能源于其对 *超文本* 的使用，这是一种通过遵循交叉引用（称为 *链接*）从一个信息片段导航到另一个信息片段的方式。要有效地使用 Web，您需要运行交互式网络应用程序。浏览 Web 的第一个 GUI 是一个名为 Mosaic 的工具，它于 1993 年 2 月发布。它在伊利诺伊大学国家超级计算应用中心设计，其引入引发了万维网用户数量的急剧增加。参与伊利诺伊大学 Mosaic 项目的 Marc Andreessen 后来与 Silicon Graphics 的创始人 Jim Clark 共同创立了 Netscape Communications。两人创建了 Netscape Navigator，这是一个设计得比 Mosaic 浏览器性能更好、支持更多功能的 Web 客户端程序。Netscape Navigator 取得了巨大的成功，是探索万维网的流行选择。对 Linux 用户来说，重要的是从一开始 Netscape 就提供了在 Linux 上运行的工具版本。此外，Netscape 创建了 Mozilla（mozilla.org）作为一个开源浏览器项目，Firefox 正是从 Mozilla 衍生而来。

这些浏览器提供了 GUI，允许您收听声音、观看电视活动或实时新闻报道，并显示图片以及文本，从而为您提供访问

