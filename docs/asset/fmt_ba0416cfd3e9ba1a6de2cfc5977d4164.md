
在外观上，Mosaic for X 与任何 Windows 或 Macintosh 都非常相似。（见下图。）

![](img/b0bfb2d724c393178bf462832858a65d_266_0.png)

几乎所有的 Mosaic 功能都可以通过下拉菜单使用。（许多功能也可以通过主屏幕上的按钮使用。）当然，如果你正在进行研究，Mosaic 是一个极佳的选择。它快速、可靠且轻量级。

Mosaic 的二进制文件存在于以下 UNIX 系统中：

- AIX
- Apple A/UX
- Bull DPX/23xx
- ConvexOS 11.0
- DESview/X
- DG AVIION
- HP9000 (HP-UX)
- Linux
- NeXT
- SunOS and Solaris
- UNIXWare

Mosaic for X 目前版本为 2.6（尽管存在 2.7 贝塔版），并可以在 `http://www.ncsa.uiuc.edu/SDG/Software/XMosaic/` 获取。

优点：Mosaic 快速、免费、可靠、稳定且易于使用。

缺点：Mosaic 已经过时，且不符合许多之后实现的标准。

# Netscape Navigator 和 Communicator

Netscape Communications Corporation

501 E. Middlefield Road

Mountain View, CA 94043

`http://home.netscape.com`

Netscape Communicator 及其早期版本 Navigator 都是出色的 Web 浏览器。除了保持更新（它们支持大多数新技术）外，这些浏览器还有几项重要的便利功能：

- 集成电子邮件和 USENET 新闻——Navigator 和 Communicator 都内置了邮件和新闻客户端，允许你无需离开应用程序即可查看和接收消息。
- 集成文档编辑器——如果你突然产生开发自己的 Web 页面的冲动，Navigator 和 Communicator 可以立即满足你的需求。两个应用程序都内置了 HTML 编辑器，允许你构建自己的页面。
- 书签文件——Netscape Communicator。这些文件有指向业务、金融、教育、体育、购物和休闲的无限链接。

此外，Netscape 的界面非常友好。（见下图。）

## 第 18 章 ► WWW：UNIX 浏览器

![](img/b0bfb2d724c393178bf462832858a65d_267_0.png)

Netscape Navigator 和 Communicator 都支持 JavaScript、表格、图形、声音和视频。

你使用的浏览器取决于你使用 WWW 的目的。如果你是在进行研究且主要寻找文本，那么使用哪种浏览器其实并不重要。然而，如果你是为了个人享和和娱乐而浏览 Web，最好的选择可能是 Netscape Navigator 或 Communicator。这两款产品都支持 Web 媒体中的绝大多数最新技术。

优点：Netscape 免费、全面、方便且最新。

缺点：体积大、下载慢，且占用磁盘空间。

# Lynx

堪萨斯大学

分布式计算小组

Lawrence, KS 66045

`http://www.ukans.edu/about_lynx/`

Lynx 是一个适用于 UNIX 的文本浏览器，运行在以下系统：

- Windows 95
- Windows NT
- VMS
- OS/2

现在可能疑惑为什么还会开发和维护文本浏览器。毕竟有了 Mosaic、Netscape Navigator 等图形浏览器，文本浏览器似乎过时了。然而，在某些情况下，文本浏览器是有价值的工具。例如，许多图书馆提供互联网访问，但仅通过连接到服务器的哑终端。在这种环境下，文本浏览器可能是唯一的替代方案。

## 使用 Lynx

要使用 Lynx，请输入 `lynx` 命令并带上目标地址，如下：

```
lynx http://www.mcp.com
```

Lynx 会加载请求的页面，你就可以开始浏览了。（见下图。）

![](img/b0bfb2d724c393178bf462832858a65d_269_png)

通常，活动链接以反色显示，以便查看。尽管 Lynx 不支持表格，但它支持大多数 HTML 表单。导航完全通过按键实现。表格 18.2 总结了各种导航按键。

### 表 18.2. 一些 Lynx 按键

| 按键 | 目的 |
| --- | --- |
| ! | 临时退出 shell |
| / | 在当前文档中搜索文本字符串 |
| ? | 获取 Lynx 帮助 |
| \ | 查看文档源 |
| Down arrow | 向下移动到下一个链接 |
| h | 获取 Lynx 帮助 |
| Insert | 向后移动两行 |
| m | 进入主菜单 |
| p | 打印当前文档 |
| Page Down | 移动到下一页 |
| Page Up | 移动到上一页 |
| Q | 紧急退出（当你遇到问题且绝对需要退出而不保存书签或打印数据时使用） |
| q | 退出 Lynx（Lynx 会提示你退出） |
| Right arrow | 遵循当前链接 |
| Up arrow | 回到最近的一个链接 |

## 第18 章 > WWW：适用于 UNIX 的浏览器

### Lynx 的可用性

Lynx 目前运行在以下 UNIX 系统上：

- AIX
- BSD（所有版本）
- Data General
- Digital UNIX
- HP-UX
- IRIX
- Linux
- NEXTStep
- Ultrix

可以在以下地址获取 Lynx 的二进制版本：

`http://www.crl.com/%7Esubir/lynx/binaries.html`。

优点：Lynx 速度快、免费、轻量级且资源利用率高。

缺点：Lynx 完全基于文本，不支持表格，也不支持现在 Web 上常见的许多不同媒体格式。

# Amaya

万维网联盟 (W3C)

马诸塞理工学院

计算机科学实验室

545 Technology Square

Cambridge, MA 02139

`http://www.w3.org/`

Amaya 是万维网联盟的结晶——即那些制定 WWW 标准的人。这个浏览器具有一些非常有前景的特性（此外大约二十个你可能永远用不到的特性）。例如，Amaya 可以编辑复杂的数学方程，这一特性对物理学家来说非常有吸引力。

Amaya 的其他功能包括：

- 严格遵守 W3C 标准。（为什么不呢？毕竟标准是 W3C 制定的。）
- 内置网页编辑器
- 支持层级样式表 (`CSS`)
- 支持 Java

## 第 4 部分 ► UNIX 的价值

Amaya 的界面也非常用户友好。（见下文。）

Amaya 界面。

| 文件 | 编辑 | 类型 | 链接 | 视图 | 特殊 | 帮助 |
|---|---|---|---|---|---|---|
| [ ] [ ] [ ] [ ] [ ] [ ] [ ] [ ] [ ] [ ] [ ] [ ] | | | | | | |
| Amaya | 地址 | `http://browser/Th/amaya/AmayaPage.html` | | | | |
| 标题 | 欢迎来到 Amaya | | | | | |

Amaya 既是浏览器又是编辑工具。它的设计初衷是在所见即所得（WYSIWYG）环境中解构 Web 技术。编辑器支持 HTML、CSS 和 HTTP。然而，你不需要 HTML 就可以操作网页、表格，甚至是高级功能。你可以在网页内创建和编辑复杂的数学表达式。你可以使用样式表对其进行样式设置。你可以通过 HTTP 协议在本地或远程服务器上发布文档。

浏览和编辑是无缝集成的。你可以同时浏览和编辑网页。正因如此，只需点击即可移动光标以进行文本编辑或跟踪链接。

本软件及其文档可供任何目的免费使用、复制、修改和分发，无需任何费用。

Amaya 是全球超级极客的选择，主要因为可以用于开发。（该程序拥有广泛的 API。）

![](img/b0bfb2d724c393178bf462832858a65d_271_0.png)

### API 到底什么是 API？

API 代表应用程序编程接口（Application Program Interface）。API 规定了程序员可以使用的所有允许规则和函数调用。通过使用这些规则和函数调用，程序员可以请求应用程序（或操作系统）执行特定任务。在大多数专有软件包中，至少有一部分（可能不是全部）的 API 是公开并供外部访问的。通过公开其 API，软件制造商允许程序员和用户访问增强软件功能的特殊函数。（这些增强功能通常超过应用程序的现成功能。）

## 第 18 章 > WWW：适用于 UNIX 的浏览器

优点：Amaya 支持所有认可的标准，具有内置编辑器，非常友好。

缺点：Amaya 有些生僻，且不支持许多新的媒体技术。

你可以从万维网联盟网站 `http://www.w3.org/` 获取 Amaya 的二进制文件。

# Chimera
