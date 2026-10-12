
# LAMP 开源 Web 开发：Linux、Apache、MySQL、Perl 和 PHP 使用指南

005.1–dc21

献给我的妻子 Kelli 以及我们的三个孩子 Ryan, Christian 和 Madeline。

献给我的朋友 Hanchau。抱歉我错过了许多 J.L. 和 B.W。

## 前言

### xxi

- MySQL 是一个 SQL 数据库程序。它是“世界上最流行的开源数据库”（他们的网站上是这么说的）。
- Perl 是处理文本文件、Shell 脚本以及无数种事务的首选编程语言。（Python 在功能上与 Perl 相似；然而，出于我们的考虑，我们选择了 Perl，因为我们更熟悉它也更喜欢它。）
- CGI 是生成动态内容的久经考验的方法。
- mod_perl 是一种生成动态内容的更好、更快、更强大的方法；mod_perl 结合了开源两大支柱：Apache 和 Perl。
- 服务器端包含 `SSI` 内置在 Apache 中。它的作用是预处理 HTML 文件，将 SSI 指令转换为 HTML 文本；它允许优秀的程序员将可执行代码嵌入到 HTML 文件中。
- Embperl 和 Mason 是用于构建嵌入式 Web 内容的 Perl 模块。
- PHP 是另一种在 HTML 文件中嵌入可执行代码的方法。PHP 做了 Embperl 和 Mason 做的事，只是方式不同。

那么为什么有这么多选择呢？亲爱的读者，请继续读下去，你会发现，万千选择正是开源之道！

### 自由软件带有 .docs 文档吗？

当然，对于自由软件，有免费文档——例如 [see.linuxdoc.org](http://see.linuxdoc.org) 和 [httpd.apache.org/docs/](http://httpd.apache.org/docs/)。最终文档——源代码，任何人都可以获取。（这就是开源笑话，“卢克，用源码！”由于庞大的开发者用户社区，有很多新闻组和讨论论坛，那里可能有人遇到过和你一样的问题，并发布了解决方案。使用 Google (https://www.google.com) 及其对 [Usenet 存档](https://groups.google.com) 的界面进行搜索。

### xxii

前言

如果你是从发行版安装的 Linux，大部分文档可能就在你的硬盘上。在一个理想的世界里，你只需要阅读它们——我们当时是这么做的。尽管它是极好的资源，但作为一种学习方法，它仍有不足之处。其中大部分内容是为了参考，而不是教学。部分文档没有随软件一起更新。（嘿，这些人是免费工作的。无论如何，这都是一个闭源软件也无法幸免的问题。）

### 古老的诱饵与调包

尽管我们谈了很多关于自成一体的话，但现实中，有两本书是你无法逃避隐藏的：《Hacking Linux Exposed》和《Unix System Administration Handbook》——或者更泛泛地说，一本关于安全的书和一本关于系统管理的书。这两本是我们的最爱（下简称 HLE 和 USAH）。这两个主题的内容都比这里能涵盖的要得多，而且两者都是不可避免的（但也很有趣）。买它们，读它们，理解它们。

### 伴随网站

在书中，我们向你展示了如何在活跃网站上实现我们讨论的所有操作示例（[www.opensourceceebook.com/](http://www.opensourceceebook.com/)），这样你就可以看到代码和结果，并被引导至额外的资源。我们努力做到自成一体，但我们喜欢书籍，并且经常告诉你可能想看的其他书。整个网站也可以从 [www.opensourceceebook.com/sourcecode](http://www.opensourceceebook.com/sourcecode) 下载。

### 致谢

首先，我们想感谢所有的开源黑客，他们花费大量时间创建了我们在书中讨论的程序：Linus Torvalds 和所有 Linux 黑客、Apache 团队、MySQL 团队、Larry Wall 和所有 Perl 黑客、Ralf S. Engelschall 负责 WML、Gerald Richter 负责 HTML::Embperl、Jonathan Swartz 负责 HTML::Mason 以及 PHP 团队。

如果没有我们评审者的卓越投入，这本书就不会有现在的样子：Ralf S. Engelschall（WML）、Gerald Richter（HTML::Embperl）、Jonathan Swartz（HTML::Mason）、Thomas Boutell、Richard Dice、Brian Hatch、Todd Haverkos、Lynn Milner、Gautam B. Singh、Daryl W-McBride、Stefan Winz 和 Sander van Zoest。感谢 Brian Hatch 是一位如此优秀的开源黑客。非常感谢 Daryl Lee 尝试了书中的所有示例，并提供了出色的评论。

非常感谢 BDGI（[www.bdgi.com](http://www.bdgi.com)）的所有人员，为 [www.opensourceebook.com](http://www.opensourceebook.com) 的平面设计、带宽支持，并在 James 写书的这几个月里忍受他：Ron Ballard、Mike Borchew、Gail Kimura、Deborah Sawyer、Tom Vanderkerkhove 和 Al Yalowowitz——特别是 Al。

感谢 Addison-Wesley 的编辑和优秀同事，帮助我们规范流程，并协助制作出一本让我们感到自豪的书：Alicia Carey、Mary O’Brien、Marilyn Rash、Jacquelyn Douette 以及其他不知道姓名的团队成员。

感谢我的妻子 Kelli 和我的孩子们 Ryan、Christian 和 Madeline，忍受了我的缺席。感谢 Brian Hatch 参与这个项目，感谢 Daryl Lee 参与 HLE，感谢 Polly Pistole 忍受我。

### 关于作者

James Lee（[james@opensourceweb.com](mailto:james@opensourceweb.com)）是一位黑客，住在伊利诺伊州。他在西北大学获得了物理学硕士学位。在 NASA 喷气推进实验室担任博士后研究员，他现在是一名科学家。他曾接触过多种操作系统，并是开源倡导者。他是《Hacking Exposed，第二版》的合作者。他喜欢 Perl，经常在 Web 上写文章。

Brent Ware（[brent@opensourcebook.com](mailto:brent@opensourcebook.com)）是一位黑客，最初是一名电气工程师。他放弃了充满前途的职业去攻读博士学位。在曾在不同的大学担任博士后之后，他现在是一名无偿系统管理员。他喜欢他的孩子，喜欢旅行。他是《Hacking Exposed》的合作者。

### xxviii

## 引言

### 1.1 所有可能世界中的最佳……

使用免费的开源程序，可以以 0.00 美元这一令人惊人的价格创建一个网站——零，完全，一分钱。³你可以下载 Linux、Apache、MySQL 和 Perl/PHP 来开发世界级、强大且实用的网站——这就是这几个缩写词的由来，以及将点亮我们道路的 LAMP。当然，你也可以投入你愿意的任何资金，使用商业软件运行网站，但我们认为，除了初始和后续开支外，使用免费的开源解决方案还有充分的理由。

对开源作为一种解决方案的常见批评是：它只有当你的时间一不值钱时，它才是免费的。这在某种意义上是真的，但在另一个方面并非如此。所有软件——无论是免费还是商业、开源还是闭源——都需要花费精力和时间学习和应用。

以下是当你转向开源软件时，这本书应该成为一个有价值的资源的几个原因：

- 它在同一个地方提炼了创建一个一个良好的、安全且符合标准的开源网站所需的精要知识。
- 它提供了商业解决方案的替代方案。
- 它记录了广泛使用的开源程序。
- 它分享了我们使用开源软件的乐趣。

### 1.2 开源软件

首先，什么是开源？这意味着什么？开源意味着，与你可能在“Bob's Computer Hut”买到的大多数带包装软件不同，你可以访问原始源代码——即人类可读的 C、C++、Perl 等文件，这些文件被编译成由计算机执行的二进制文件。这种可执行的二进制文件（.exe）就是你从闭源专有解决方案中得到的全部。如果你愿意，你可以查看这些文件，看看为什么那个该死的错误信息不断弹出，或者如何让该组件默认到不同的目录，或者如何添加新函数。一旦你开始查看源码，你就就开始了成为开源程序员的道路。这就是开源的魅力所在。

³至少，不需要现金支出，只需要投入大量的脑力劳动；而且当然，如果你的网站变得流行，会有明显的问题需要你的互联网服务提供商（ISP）解决。

### xxix
