

# 图 21.17。
更改你的字体设置。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_445_0.png)

# 图 21.18.
自定义你访问的每个网页的外观。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_445_1.png)

下一个选项是“应用程序”（Applications，见图 21.19）。这些是 Navigator 在请求协议时启动的命令。我将把这些内容保持不变。如果你的 UNIX 配置与默认配置不同，你可能想要更改它们。请咨询你的管理员。

# 使用 Netscape 查看万维网

# 图 21.19。
你可以使用任何应用程序来查看网络上的站点。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_446_0.png)

辅助程序（Helpers，如图 21.20 所示）是解释 MIME 输入的工具，MIME 是 Web 服务器发送不同类型网页元素（如图形、音频等）的机制。在修改任何这些设置之前，我建议你极度谨慎，否则可能会无法显示常见的页面元素。

# 图 21.20。
辅助程序列表。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_446_1.png)

“常规偏好”（General Preferences）下的最后一个标签页是“图像”（Images），如图 21.21 所示。这些定义了图像如何显示；因为我不想看到不完整的图像，所以我点击“加载后显示图像”（Display Images After Loading）。

# 图 21.21。
设置图像显示方式。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_447_0.png)

Navigator 可以通过浏览器上的“选项”菜单进行完全自定义。虽然它通常被设置为标准的 UNIX 配置，但如果你与标准配置有不同，你需要自定义 Navigator。

# 总结

这一小时向你介绍了 Netscape Navigator 和万维网的基础知识。现在你已经学会了如何启动和使用 Navigator 访问互联网上的资源，以及如何通过不同的搜索引擎查找资源。

# 工作坊

工作坊总结了你学习的关键术语，并对本章介绍的主题提出了问题。它还为你预览了在下一小时将学习的内容。

# 关键术语

- **书签 (bookmarks)**：用于快速检索的收藏夹站点列表。
- **浏览器 (browser)**：设计用于加载超文本页面并跟踪超链接的程序。
- **超链接 (hyperlinks)**：文档中的规范，包含加载不同文档的指令。
- **冲浪 (surfing)**：与万维网交互的一种风格，通常是为了乐趣，通过超链接从一个网站跳转到另一个网站。

# 使用 Netscape 查看万维网

URL：万维网上文档的规范。通常它包含协议、机器名称和文件名。

**万维网 (World Wide Web)**：在互联网上提供超文本文档的站点集合。

# 问题

- 1. 你如何找到关于通用·库斯特（General Custer）的站点？
- 2. 萨加玛塔国家公园（Sagarmath National Park）在哪里？
- 3. 你如何更改你的默认主页？

# 下一小时预览

在下一小时中，我们将查看不同的工具，包括互联网电子邮件和网络新闻（Netnews）。

# 第 22 小时

# 互联网电子邮件、网络新闻和 IRC

我想你可能喜欢对互联网上一些令人惊叹的资源进行导览，这是一个由 UNIX 和其他计算机系统组成的全球网络——它们都通过高速链接连接。这些资源中的大多数要求你在连接到互联网的机器上拥有账户，但也有相当数量的资源提供了电子邮件替代方案，所以即使你没有账户，也不会完全被冷落。如果你无法访问互联网，我鼓励你阅读这最后一小时，只需感受一下在这个世界上增长最快的网络上，已经存在可用数量惊人且种类丰富的信息和服务。

# 本小时目标

- 在这一小时中，你将学习到：
- 向互联网用户发送电子邮件
- 与远程互联网用户交流
- 使用 WAIS 搜索数据库

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_449_0.png)

# 第 22 小时

通过 gopher 拥有世界
所有合适或不合适的新闻

这一小时旨在对通过互联网提供的许多服务提供快速且愉快的概览。从寻找失散已久的档案到在海外图书馆找书，其可用信息的范围无疑令人惊叹！

# 任务 22.1：向互联网用户发送电子邮件

互联网的常见用途实际上是在个人和邮件列表之间发送电子邮件。真正的利好是，从纽约到洛杉矶，从日本到德国，从南非到印度，每个人都有非常相似的地址，你在这里已经见过了。格式为 `user@host.domain`，其中 `user` 是账户名或全名，`host` 是用户机器的，`domain` 是用户在世界的位置。

从左到右读取主机和域名信息（实际上是从外向内），你可以通过查看人的电子邮件地址解码关于该人的信息。例如，我在名为 Netcom 的系统上的地址是 `taylor@netcom2.netcom.com`，从右到左看，它告诉我在一个商业站点 (com)，有一家名为 Netcom (netcom) 的公司，我使用的计算机名称是 `netcom2`。我在 Netcom 上的账户是 `taylor`。

有很多顶级域名，最常见的在表 22.1 中。

# 表 22.1. 常见的互联网顶级域名。

| 域名 | 站点或网络类型 |
|---|---|
| edu | 教育站点 |
| com | 商业业务 |
| mil | 军事或防御系统 |
| net | 通过互联网访问的备用网络 |
| org | 非营利组织 |
| us | 未另分类的美国系统 |

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_450_0.png)

- 1. 向互联网上的某人发送邮件很容易的，因为 @ 是一个特殊字符。如果你想给我发条消息，可以使用这个：
% mail taylor@netcom.com
Subject: _

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_450_1.png)

# 互联网电子邮件、网络新闻和 IRC

输入消息并用 `^d` 结束，就像你在发送任何电子邮件时做的那样。它会立即发送给我！

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_451_0.png)

> 如果你愿意，我鼓励你给我写便条，告诉我你觉得这本书怎么样，你可能遇到了什么问题，以及任何令你困惑的命令

- 2. 虽然电子邮件地址始终遵循相同的格式，但它们可以很大差异。为了让你对这种变化有个概念，我以前从这里处 grep：

```
% grep ^"From": /usr/spool/mail/taylor
- From Steve Frampton <frampton@vicuna.ca>
- From Joanna Tsang <tsang@sfsu.edu>
- From "Debra Ivar" <desis@oracle.com>
- From Jay Munro <72241,556@CompuServer.Com>
- From Linda Wei <jras.andahl.com
- From Cheryl <cheryl@vwlm.PURD.edu>
- From harris@mace.ute.tech (Wickey Harris)
- From v892127@nootebook.si..hhs_nl
- From "ean hosts" <ean_hosts@cget.infoworld.com>
- From harris@mace.ute.tech (Wickey Harris)
- From Barbara Maxwell <maxwellites.synergy.com>
- From Steve Mansour
- abhasin@itsmail.haniton.edu (Aditya Bhasin)
- From gopher@scorpio.kent.edu (Marvin Rao)
- From marv@netcom.com
```

邮件行的国家习惯显然各异。你在这一行中可以看到三种基本格式：地址，例如 `gopher@scorpio.kent.edu` 这种；带名字的地址，例如列表中间 Linda Wei 的消息；以及姓名后跟括号内的电子电子邮件地址的行，例如列表的第一行。

注意我过去几天收到的电子邮件的各种站点：SFSU.edu 是旧金山州立大学，oracle.com 是位于加州的甲骨文公司，PURD.edu 是普渡渡大学，CompuServer.Com 是运行 cc:Mail 的 InfoWorld 杂志网络，xalt.com 是 XALT 公司，kent.edu 是肯塔州立大学。这条信息来自荷兰的一个教育机构！

要解码这些信息，你需要大量的信息、优秀的猜测、查看消息中可能出现的 `Organization:` 行，或者如果你在一个拥有所有最新软件的系统上，调用 `netinfo` 命令来解释你好奇的站点。

