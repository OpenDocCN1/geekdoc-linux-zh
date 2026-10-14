# Linux 傻瓜指南 第二版 附 CD-ROM





要访问内容，请点击章节和节标题。



搜索本书：


## 关于作者




















































产品 | 联系我们 | 关于我们 | 隐私 | 广告信息 | 首页


要访问内容，请点击章节和节标题。



搜索本书：


欢迎使用 Linux！它是一款正吸引世界关注的可靠且强大的操作系统（OS）。在撰写本文时，Linux 和 Windows NT 是唯一正在获得市场份额的操作系统。大多数其他操作系统要么停滞不前，要么正在失去份额给 Linux 或 Windows NT。

## 如何使用本书

本书是对 Linux 的温和介绍，因此并非旨在作为全面指南。相反，本书付出了很大努力以避免成为又一本综合参考指南。我在选择覆盖主题时有所甄别，这些主题是你最有可能在 Linux 入门阶段使用的。

Linux 以及 UNIX 的一个有趣之处在于，学习新方法和工具几乎是一项无止境的任务。有许多工具——太多以至于即使在几本“综合”卷中也无法涵盖。Linux 的大量综合和详尽参考资料以各种形式 readily 可用，其中一些将在安装过程中作为安装过程的一部分安装到你的计算机中。

相比之下，本书侧重于如何让你自给自足。它教你两种使用 Linux 的方法：使用 X 图形环境（带 KDE）和使用 shell，即与 UNIX 紧密相关的命令行解释器。而且，如果你管理自己的 Linux 计算机，还有一些管理任务需要你学习如何完成。

那么本书是如何组织的？安装和首次配置说明位于附录 A，“Linux 安装”。附录 B，“OpenLinux 兼容性指南”，为你提供了不断增长和不断变化的已知与 Linux 兼容的硬件的最新列表。在规划安装时，你应核实你的硬件是否在列表中并且已知与 OpenLinux 兼容。

完成初始 Linux 安装和配置后，从第 1 部分“在图形环境中工作与 Linux——KDE 桌面”开始，按顺序阅读章节。（我们构建章节时假设你会这样做。）第 2 部分“在命令行上工作”介绍了与第 1 部分类似的概念，这次使用 shell 而不是图形用户界面。最后，第 3 部分“Linux 下的基本系统任务”侧重于你偶尔需要执行的各种管理任务。请记住，在学习 Linux 的同时，你也在学习 UNIX。你在这里学到的知识只需少量修改即可转移到其他 UNIX 环境中。

享受认识你新操作系统的乐趣！

## 为什么是 Linux？

那么为什么会受到如此多的关注？UNIX 已经存在多年，尽管被一些人认为是在真正的操作系统中唯一的选择，但直到最近它一直停留在垂直市场领域。但这意味着什么？UNIX（或基于 UNIX 的 Linux）提供了一个非常强大的运行和部署应用程序的环境。按设计，它提供以下功能：

- 多用户支持
- 安全
- 完全多任务处理
- 客户端和服务器应用程序的网络支持
- 源代码

这些是当今一些 PC 操作系统所不提供或作为事后想法添加的功能。这些都是非常重要的功能，尤其是在当今的网络环境中，计算机共享信息。

与基于 Windows 的系统不同，UNIX 能够同时支持多个用户。单台 UNIX/Linux 计算机可以让多个用户同时在其上工作（运行程序、访问文件和其他服务），无论是通过网络无缝连接还是通过直接连接的控制台（屏幕和键盘）。

因此，UNIX 和 Linux 提供了一个环境，其中许多（数百）用户可以同时访问系统，如果系统有足够的资源。随着如此多的潜在用户，你如何保护重要文件免受未经授权的访问？Linux 的 UNIX 根源以透明的方式处理安全，而不是作为事后想法，而是作为 Linux 生活方式的一部分。为了在计算机上工作，你必须登录。

安全不是 Linux 的唯一优点。它也是一个专家杂耍者！否则你如何同时支持多个用户？Linux 是一个多任务操作系统。它同时处理多个程序和用户，创造出每个用户都在自己的计算机上工作的错觉。显然，在一小段时间片内只能完成一点点工作，但这种错觉得到了很好的维持。其他声称是多任务的操作系统通常扩展性不佳。当少数用户访问服务时，性能迅速下降。杂耍的错觉对于支持多处理器的平台来说成为现实。计算机实际上可以同时处理多项任务。Linux 操作系统利用这些硬件配置并利用额外的处理能力将性能提高到新水平——通常比硬件最初设计的操作系统效果更好。

当今许多计算机依赖于网络环境。“网络即计算机”℠是 Sun Microsystems 的著名口号，Sun Microsystems 是一家大型 UNIX 供应商。网络确实是计算机。通过电子邮件、网络和其他机制进行信息交换是日常事实。Linux 不仅可以作为此类服务的客户端参与，还可以向其他 PC 和工作站提供这些服务。事实上，Linux 为许多互联网服务提供商（ISP）和访问 ISP 服务的用户提供支持。它经过充分测试且可靠。

很少有商业环境提供其工作原理的源代码，并且是免费提供的。这就是 Linux 脱颖而出的地方！拥有源代码允许信息服务（IS）部门或黑客同样自定义操作系统或随附的程序的特定行为以满足特定需求。关心安全问题的公司可以检查软件的实际工作原理并做出自己的评估和调整。在出现问题时，具有正确背景的人可以在问题或安全问题发现后的数小时内生成修复程序。将其与等待数天、数周或数月进行错误修复相比——这是我们对其他操作系统所期望的常态。对于学生来说，访问源代码提供了对系统如何制作和构建的洞察。

在缺点方面，UNIX 和类 UNIX 操作系统在表面上缺乏人机工程学，提供令人困惑的界面，这些界面因程序和供应商而异，并且通常对非专家用户来说不直观。主流应用程序开发人员在这些环境中看不到盈利能力，选择将他们的产品保留在其他更有利可图的操作系统平台上。但这种态度在 Linux 市场中正在迅速改变。

随着其新获得的流行，Linux 鼓励了 Oracle、Sybase、Corel 等大型软件开发商为 Linux 系统开发其应用程序的版本。世界开始认真对待 Linux——一点赞助就能走很远！这本身就产生了额外的媒体兴趣，Linux 的报道已从晦涩出版物中的好奇心转变为对其他公司重量级产品的可行商业选择和替代方案。这是个好消息，因为进入 Linux 领域的开发人员越多，这个操作系统环境就越受欢迎和易于访问！





随着 Linux 的出现，基础设施（即使 UNIX 如此稳健的核心部分）突然可以免费获得。在一个普通商业 UNIX 的桌面许可费用高达数千美元的世界里，这无疑是一个非常好的突破。它使 Linux 进入了那些因价格限制而从未考虑过 UNIX 的环境。

毫无疑问，其受欢迎程度很大程度上源于其价格：免费下载，或如果您想要包装成 CD，则不到 50 美元——或者如果您购买了本书，您就获得了更好的交易！它绝对是为销售而定价的。Linux 的商业发行版包含额外的商业软件，进一步增强了其解决额外业务类型问题的价值。

帮助 Linux 热潮的另一个因素是互联网的出现。许多需要稳健环境来处理其互联网服务（如万维网、电子邮件等）的人，传统上认为 UNIX 是这种用途的自然选择。从一开始，今天我们听到的关于它的大多数事情都是在那里首先可用并开发的。Macintosh 和基于 Windows 的机器直到最近（按 UNIX 的时间尺度）才联网。但即使在今天，它们在担任服务器角色时仍然没有同样的稳健性。UNIX 机器几乎从网络诞生之初就参与了网络。

Linux 对于 UNIX 来说是一个新概念。它可以免费获得，支持尖端硬件，更不用说它比之前的 UNIX 系统更容易使用。这并不意味着没有粗糙的边缘。然而。尽管 Linux 并不是特别难以学习，任何困难都伴随着功能增加。所有强大且灵活的东西通常都很复杂；说 Linux 不强大就会否认其灵活性和复杂性。新的桌面环境，例如 K 桌面环境（简称 KDE），承诺提供高质量的用户界面，提供以前对类 UNIX 系统不可用的尖端功能。焕然一新的人体工程学提供了以前不可能的价格-功能比较。

本书附带了 Caldera 的 OpenLinux 1.3。Caldera 将其 Linux 发行版定位为商业级、可靠的 Linux 版本。与其他流行发行版（RedHat）相比，其某些功能非常不错。Caldera 提供的额外附加组件（Sybase、NetWare 支持等）使 OpenLinux 很容易迁移到您的职场。

最近，华盛顿州梅迪纳市（人口 3,082 人）选择 OpenLinux 来实施其文档管理系统。做出这一举措的原因与与微软比尔·盖茨在那里建造的 5300 万美元豪宅相关的 40,000 多份建筑许可证、蓝图、变更订单和其他文件有关。城市的选择是在意识到再也没有空间容纳任何未来的文书工作，要么必须建造新的市政厅，要么安装文档管理系统。自然地，微软 Windows NT 被视为潜在解决方案，但在意识到 OpenLinux 解决方案的成本不到 NT 解决方案的 10% 后，OpenLinux 赢得了该市的业务。谈论讽刺！

在如此有说服力的论证下，Linux 是一个冉冉升起的操作系统，你难道不想开始了吗？这正是本书旨在帮助你做的——开始使用 Linux。如果你有其他操作系统的经验，本书将培养你的 Linux 基础技能。我们的一个目标是让你从一开始就变得高效。本书将带你从安装 Linux 到做基本的事情，甚至做一些系统管理的事情。

## Conventions

*The Complete Idiot’s Guide to Linux* 旨在帮助你启动并运行你的新 Linux 操作系统。为此，本书使用了以下约定：

- **Bold** 表示你输入的文本、你选择、点击和按下的项目，以及你在屏幕上看到的文本。
- 你会看到 `monospace` 文本用于 URL、屏幕信息和命令输出。
- 任何正在定义或强调的词语都会以 *italics* 出现。

另外，请注意以下功能：

> **Check This Out:**
> 你会在整本书中发现“Check This Out”部分。我会用它们来指出值得注意的事情、需要警惕的东西、绝佳的技巧——基本上，它们将充满信息，增加你对 Linux 的理解，甚至可能让你说，“哇！”

> **Techno Talk:**
> 每个人都知道技术主题有时会让你抓头挠耳，想知道那冗长的解释到底是什么意思。好吧，不用担心。我会转向“Techno Talk”框来提醒你仔细阅读。这是会突出术语、方法或聪明的东西的地方，你不一定需要知道，但这确实有助于你更好地理解 Linux。

> **Note:**
> “Note”框将用于传递交叉引用，指向本书的其他部分，或我认为你应该看一下的任何内容。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_15_0.png)

要访问内容，请点击章节和节标题。



Search this book:


## About the Author

Manuel Alberto Ricart 是 Paradigm Research, Inc.（http://www.pri.com）的培训师和工程师，Paradigm Research, Inc. 是一家位于硅谷的培训公司。Alberto 为 Java 和互联网编程技术开发教学材料。Paradigm Research, Inc. 将其培训材料交付给众多财富 500 强和知名高科技公司，包括 Hewlett-Packard、MCI、Ford 和 Netscape Communications, Inc.

Alberto 自 20 世纪 70 年代末起就开始接触计算机，当时他在当时最先进的 IBM system 32 上接触到编程，该系统拥有惊人的 32KB RAM 和一个微小的硬盘。从那时起，他为 Macintosh 操作系统（OS）、NEXTSTEP OS 以及最近的 Java 开发了许多软件产品。Alberto 自 20 世纪 80 年代中期以来一直为各种客户提供 UNIX 和互联网网络支持。他拥有威斯康星大学密尔沃基分校的学士（1987 年）和硕士（1989 年）学位。

1992 年，他创立了软件公司 SmartSoft, Inc.，该公司为 NEXTSTEP/OPENSTEP（UNIX）操作系统开发了各种商业面向对象软件工具。他的产品在全球销售。

1995 年，他共同创立了第二家公司，致力于构建互联网解决方案，使公司能够利用互联网开展业务。他的专长是动态内容驱动的内部网和电子商务解决方案。他开发的定制技术被 Oshkosh B’Gosh 和 Warburg Pincus Funds 等知名公司使用。

Alberto 专注于软件产品和工具的发明与设计。他的重点是互联网和网络核心技术，如 Apache 和 Netscape Web 服务器、Perl、JavaScript、Java，以及支持它们的各种技术，如 UNIX 网络连接和管理。自 1996 年以来，Alberto 在开发和部署许多互联网网站和内部网项目中大量使用 Linux。

他的著作 *Apache Server Survival Guide*（由 sams.net 出版，ISBN 1-57521-175-0）已以印刷版出版，并包含在与 RedHat LINUX 操作系统相关的另外两个电子出版物中。

可以通过 `alberto@pri.com` 联系 Alberto，他通常在那里整天摆弄技术。

## Dedication

*献给 Diana、Julisa、Isabella 和 Viviana：你们让这一切成为可能。*

## Acknowledgments

写一本书是一项影响许多人生活的巨大任务。像往常一样，我的个人重大任务在那些我本已有很多事情要做的时候排队。我仍在努力弄清楚如何让这个过程对我和我的家人都容易一些。理想是美好的东西。

献给我美丽而美好的妻子 Diana 和我三个美丽的女儿 Julisa、Isabella 和 Viviana，这本书献给你们。我知道我第二次浪费了一个夏天。我想我知道你们的感觉。

知道单个人无法完成巨大的任务，我还要感谢那些我从未见过面的人，但他们的定期电子邮件和电话让他们感觉比实际更近：

- Laura Bulcher 确保我写下了我想说的话。
- Grace Buechlein 促成了许多机会并使这一切成为可能。
- Aron Hsiao 和 Jeff Perkins 扮演了读者的角色并验证了我的写作不是虚构的，并且我所说的内容正如我所说那样工作。（任何差异都是他们的错，而不是我的 A.）
- 所有其他匿名编辑和排版人员，我不知道他们的名字，他们使这本书的出版成为现实。

最后，Mr. Zero，Stephen Asbury——自 NeXT 时代以来的朋友，我们分享了对技术中善与恶的独特务实理解——在开发这本书的“上坡”部分时耐心倾听我五彩缤纷的抱怨。

**Note:**
Linux 是一个不断发展的操作系统。这就是为什么它越发





对你来说，定期检查 Caldera Systems 网站以获取公司公告和软件补丁非常重要。以下是你可以找到本书附带的 Linux 版本相关信息的网址：http://www.calderasystems.com 请务必查看“News & Features”栏目以获取新闻、评论和产品更新。

## Tell Us What You Think!

作为本书的读者，你是我们最重要的批评者和评论者。我们重视你的意见，想知道我们做得对的地方、可以做得更好的地方、你希望我们出版的领域，以及你愿意传达给我们的任何其他智慧之言。

作为 Macmillan Computer Publishing 操作系统团队的执行编辑，我欢迎你的评论。你可以通过传真、电子邮件或直接写信给我，让我知道你喜欢或不喜欢本书的内容——以及我们可以如何让我们的书籍更出色。

> 请注意，我无法帮助你解决与本书主题相关的技术问题，并且由于我收到的邮件数量很大，我可能无法回复每一条消息。

写信时，请务必包含本书的标题和作者，以及你的姓名和电话或传真号码。我会仔细审阅你的评论，并与本书的作者和编辑分享。

Fax: 317-581-4663
E-mail: opsys@mcp.com
Mail: Executive Editor
Operating Systems
Macmillan Computer Publishing
201 West 103rd Street
Indianapolis, IN 46290 USA


## SPIDER KILLER

## spider catcher

HOME ACCOUNT INFO SUBSCRIBE LOGIN SEARCH MY ITKNOWLEDGE FAQ SITEMAP CONTACT US

SEARCH ITKNOWLEDGE

To access the contents, click the chapter and section titles.



Bookmark it

Search this book:

Previous Table of Contents Next


好吧，你已经安装了 Linux（第 4 部分会指导你完成安装），并且准备好面对这头猛兽了。猜猜怎么着：你会感到惊讶！第 1 部分带你领略 Linux 更温和的一面——K 桌面环境，或称 KDE。本节中的章节会指导你使用应用程序、管理文件，以及在网上交流。我们甚至还会看看如何自定义 KDE，使其外观和操作方式符合你的喜好。你准备好开始这场冒险了吗？换上你的步行鞋，准备一些路上的零食，让我们出发吧！


本节假定你已经安装了 Caldera OpenLinux。如果你没有阅读前言，我建议你现在就阅读，因为前言解释了本书的逻辑顺序以及通篇使用的一些约定。



BROWSE BY TOPIC

Keyword
Brief Full
Advanced Search
Search Tips

在本章中，你将学习如何使用 K 桌面环境，或简称 KDE，进入和退出 Linux。KDE 是一个图形用户环境，你可以使用图标、菜单和窗口来完成工作。你将对屏幕和 KDE 环境提供的一些用户界面（UI）元素进行简短的游览。


在使用 Linux 之前，你必须登录。登录允许你使用计算机，并通过仅允许你访问自己的文件来保护你的工作免受其他用户的影响。Linux 是一个多用户操作系统，多个用户可以同时工作。登录确保只有授权用户才能使用计算机。

如果你按照我在附录 A 中建议的方式安装了 Caldera OpenLinux 和 KDE（标准系统安装时默认已安装 KDE），你的登录提示将类似于这样：

```
Caldera OpenLinux(TM)
Version 1.3
Copyright 1996-1998 Caldera Systems, Inc.

login:
```

登录过程很简单：你提供用户名和密码。你的用户名和密码是在安装系统时设定的。如果你使用的是已配置好的系统，你需要联系系统管理员以了解这些信息。

如果你在输入用户名或密码时出错，可以按 Backspace 键删除想要重新输入的字符。请注意，输入密码时屏幕上不会显示你的密码。不回显密码有助于保护你和你的账户免受附近窥视的眼睛。

在你输入正确信息后，登录面板将消失，你将进入桌面。如果你输入密码有误，你会看到一条消息，提示登录不正确，需要重新输入登录名和密码。

登录成功后，你将被允许进入系统。然而你将面对的是文本界面。要启动图形界面，在提示符下输入 kde。（注意：手动启动 kde 看起来像是 Caldera OpenLinux 1.3 的一个错误，未来 Caldera 网站上的补丁可能会修复它。）
## The KDE Desktop

*桌面* 是你在计算机上工作的地方。它是你启动和运行程序、创建文件、组织文件以及做你想用计算机做的任何事情的工作区。当你第一次进入桌面时，它看起来会与以下图所示类似。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_21_0.png)

Linux 在 KDE 桌面激活时的外观。

如果你使用过其他具有图形用户界面（GUI——你可能会听到有人把它读作“gooy”，但正确用法是“G-U-I”）的操作系统，你可能可以直接上手并开始工作。KDE 桌面与 Windows 的任何版本或 Macintosh 等其他窗口化环境相似；然而，一些东西的工作方式存在一些大大小小的差异。

让我们看看 KDE 桌面的组件：

- 屏幕底部的 *面板*
- 屏幕顶部的 *任务栏*
- *桌面*


*面板* 是屏幕底部带有图标的条。它用于启动应用程序；每个图标代表一个应用程序、一个命令或一个菜单（菜单上有一个黑色三角形）。菜单提供对其他功能和应用程序的访问。

面板提供在各种 *虚拟桌面* 之间切换的功能。通过虚拟桌面，你可以通过在不同的桌面下运行应用程序来减少屏幕上的杂乱。你可以通过单击按钮（在面板上这些按钮标记为 One、Two、Three 和 Four）在桌面之间轻松切换。你将在第 4 章“Working with Applications”中了解更多关于虚拟桌面的内容。

面板为你提供对应用程序和虚拟桌面的访问。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_21_1.png)

Application Starter 为你提供对应用程序的访问以及退出系统的能力。
### The Taskbar

屏幕顶部的条称为 *任务栏*。每当你启动一个新应用程序时，就会显示一个以该应用程序命名的按钮。这些按钮中的每一个都代表在 KDE 环境中执行的任务或应用程序。单击鼠标上的任务按钮即可进入该应用程序。看起来被按下的按钮属于当前活动的应用程序。如果应用程序被隐藏，其名称会显示在括号中。要显示该应用程序，只需单击其按钮。右键单击按钮会显示一个菜单，允许你控制应用程序窗口的一些选项。

任务栏上的每个按钮代表一个正在运行的应用程序。

面板和任务栏都是由一个名为 KPanel 的应用程序提供的服务，该应用程序在你登录系统并在 KDE 下工作时始终运行。

Previous Table of Contents Next







要访问内容，请点击章节和节标题。

搜索本书：


桌面是任务栏和面板之间的彩色区域。单个程序窗口浮动在其上方。在 KDE 中你有多个桌面。你通过点击面板上标有“One”、“Two”、“Three”和“Four”的按钮来控制当前所在的桌面。

切换桌面的另一种方法是中键点击桌面上的空白区域。这样会显示一个菜单，允许你在桌面和应用程序之间切换。

桌面可作为临时位置放置你正在处理的文档和其他东西。


应用程序是呈现信息在窗口中的程序，你可以从桌面打开或关闭它们。以下图所示的 KEdit 应用程序就是一个简单的文本编辑器，可用于编辑文件。要启动 KEdit，只需点击面板上的其图标即可。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_23_0.png)

KEdit：一个简单易用的文本编辑器。

KEdit 与大多数应用程序一样有菜单。菜单位于应用程序标题栏的正下方。（KEdit 的菜单包括 File、Edit、Options 和 Help。）菜单列出了你可以选择的命令，让应用程序执行某些操作。


光标通常是一个小黑箭头，随着你移动鼠标而移动。你使用光标指向对象。光标的外观会根据你指向的内容而改变。

光标的其他变体包括：

- 编辑文本时的 I 形光标
- 光标位于桌面上方时的 X

桌面上的其他居民是图标。图标是文件、应用程序或计算机中其他事物的图形表示。

除了输入文本外，你几乎可以用鼠标完成计算机上的所有操作。鼠标控制光标的位置。你滑动鼠标以指向屏幕上的对象。如果滑动鼠标时空间不够，你可以将其拿起并放在鼠标垫上的其他位置；鼠标在空中时光标不会移动。无论你移动鼠标多远，光标都会停留在屏幕上。
## 基本鼠标操作

当你让鼠标指向某物、某个图标或某个单词时，你使用鼠标按钮执行以下操作之一：

- 单击：不移动鼠标，按下并释放左鼠标按钮。
- 右键单击：不移动鼠标，按下并释放右鼠标按钮。
- 中键单击：不移动鼠标，按下并释放中键鼠标按钮。如果你的鼠标只有两个按钮，同时按下两个按钮即可模拟中键单击。（使用三键鼠标感觉更好。）
- 按住：不移动鼠标，按下左鼠标按钮并保持按住。
- 拖动：按住鼠标按钮，移动光标（你仍在按住按钮，对吧？），然后释放鼠标按钮。成功拖动的秘诀是抵制松手的诱惑，直到你拖动的对象正好位于想要的位置。
- 双击：快速连续单击两次。如果你单击在文本上，I 形光标会被放置在字符之间。如果你双击，你会选中正在操作的单词。某些应用程序可能会使用三击来选择段落或执行其他应用程序定义的函数。


现代 UI 的基本控件可分为三类：

- 按钮
- 列表和菜单
- 文本字段
## 按钮

按钮通常位于应用程序窗口中，以便你轻松访问某些命令。按钮有各种形状和大小。它们通常用文字和图形标记以指示其功能。要激活按钮，只需单击它即可。如果按钮只是图像，当你将光标移过它时，按钮可能会在其周围绘制边框，以让你知道它确实是一个按钮并且可以单击它。如果你将光标悬停在按钮上一段时间，按钮可能会显示一个“工具提示”，告诉你按钮的作用。

变暗的按钮处于非活动状态，无法单击。（好吧，你可以单击它们，但不会发生任何事情。）按钮变暗是因为其功能不可用或其功能在当前情况下不适用。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_25_0.png)

按钮通常看起来像这样；注意激活按钮时的颜色变化。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_25_1.png)

这些图标也是按钮！

![](img/edf072a03d4de1f8f4a13465ac79e7fb_25_2.png)

大多数应用程序都有一个带按钮的工具栏。将光标移过图标，按钮周围会出现边框以及工具提示，或文字告诉你按钮的作用。

如果你在开始单击按钮后决定最终不想单击它，只需在释放鼠标之前将光标移离按钮即可。

某些按钮称为*复选框*，允许你启用应用程序可用的多个选项。X Windows 下的复选框以方块形式呈现。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_25_3.png)

你可以在一组中选择多个复选框。

其他按钮称为*单选按钮*，允许你在组中仅启用一个选项。单击不同选项会禁用先前选中的选项，同时启用新选项。X Windows 下的单选按钮以菱形呈现。

> **注意：**
> 单选按钮之所以得名，是因为它们就像你汽车音响中的收音机按钮：它们一次只能设置为一个选项。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_26_0.png)

你在一个组中只能选择一个单选按钮。

*标签*是另一种按钮。它们允许应用程序在有限的空间中分组并显示信息和控件。通过单击标签，你可以显示不同的控件和信息集。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_26_1.png)

Options 标签存储了一些控件…

![](img/edf072a03d4de1f8f4a13465ac79e7fb_26_2.png)

…而同一面板中的 Desktops 标签则存储了完全不同的控件集。

*滑块*用于设置一个范围内的值。要使用滑块，将其旋钮拖动到所需的值或位置。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_26_3.png)

滑块允许你在受限范围内设置值，例如在你的音响上选择音量级别。
## 列表和菜单

你通过命令告诉应用程序做什么。命令通常位于菜单中。应用程序的菜单位于其窗口标题栏正下方。

使用菜单与使用按钮类似。如果你单击菜单按钮（也称为菜单项），菜单会打开，然后你可以单击其中一个命令。

你也可以在菜单上单击并拖动。你在释放鼠标时光标下的选项将成为所选命令。

如果菜单显示箭头，则该命令提供子菜单。你可以以与菜单相同的方式处理子菜单。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_27_0.png)

在分层菜单中，单击显示箭头的菜单项会打开一个包含附加命令或子菜单的子菜单。

省略号 (...) 标记打开窗口或对话框的命令。永远不要害怕探索带有省略号的菜单命令，因为你始终可以用无害的方式取消对话框。

命令也可以通过输入键盘快捷键来调用。例如，你可以在 K 文件管理器（或 KFM）窗口处于活动状态时通过输入 Ctrl+T 来调用打开终端命令，如前图所示。





不同的应用程序可能会将 Ctrl+T 用于不同的目的。

带有下划线 (_) 的菜单项可以通过按 Alt+字母 的方式使用键盘打开。

变暗的命令当前不可用，无法选择。

*Choice lists* 与菜单类似。它们会打开一个下拉选项列表供您选择。在按住鼠标按钮的同时，将鼠标拖动到要选择的选项上。释放鼠标以选择该选项。带有文本字段（接下来描述）的选择列表称为“Combo Boxes”，因为它们允许您从菜单中选择或输入新选择，它们是控件的组合。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_28_0.png)

选择列表在激活前看起来像这样…

![](img/edf072a03d4de1f8f4a13465ac79e7fb_28_1.png)

…在您进行选择时看起来像这样…

![](img/edf072a03d4de1f8f4a13465ac79e7fb_28_2.png)

…and like this after you release the mouse.


当应用程序需要以文本形式输入额外信息时，您会将该信息输入到文本字段或其较大的表亲文本区域中。标签通常会指示文本字段的用途。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_28_3.png)

此对话框需要文本输入。

在使用文本字段时，会显示 I-beam 形光标，表示您可以在此处输入文本。要移动到另一个字段或使字段获得焦点，请单击它。

要选择文本的一部分，请在要开始选择的位置单击鼠标按钮并拖动到要结束的位置。（在某些应用程序中，您也可以单击然后 Shift+单击 选择的末尾。）

![](img/edf072a03d4de1f8f4a13465ac79e7fb_28_4.png)

要选择文本，请单击鼠标以开始选择…

![](img/edf072a03d4de1f8f4a13465ac79e7fb_28_5.png)

...and then drag to where you want the selection to end. The selected text is highlighted, and typing replaces the current selection.


您可以通过按 Tab 键在控件和表单（控件的集合）之间移动。当前活动的控件会显示黑色轮廓以指示其已被选中。然后您可以使用键盘更改其当前设置，如果控件是文本字段则输入数据，或如果它是某种按钮则选择它。

您可以使用键盘上的箭头键更改滑块的设置。

如果控件可以被单击，您也可以在控件被选中的情况下按空格键来激活它。

要向后移动，您可以按 Shift+Tab。


在工作会话结束时，您可以注销。如果您几天内不打算使用计算机，则应将其关闭。记住在执行这些操作之前保存您的工作。关闭系统的过程对磁盘的健康至关重要，所以不要直接关闭电源按钮！

> Check This Out:
> Don’t turn off the power to your computer until the computer says that the system has been halted. Otherwise, you can damage your computer.

要注销，请从应用程序启动器（X 图标）中选择注销，或单击 KDE 面板中的注销图标。如果您有应用程序处于打开状态，您将收到“Session prepared for logout”对话框，显示您可能丢失的数据。此时您可以改变主意，如果需要返回保存信息。

要关闭计算机，首先注销，然后在登录面板上选择关机。在出现的面板上再次选择关机。计算机停止后，您可以关闭电源。

要重新启动计算机而不是简单地停止它，请注销，然后在登录面板上选择关机。在 resulting 对话框中，选择重启。

如果由于某种奇怪的原因您的桌面停止响应，您可以通过按 Ctrl+Alt+Backspace 强制退出。这样做将终止 X 服务器（KDE）并带您返回控制台。这里再次体现了 Linux 的一个优点：您可以在不重新启动机器的情况下退出卡住的 GUI。

要访问内容，请单击章节和节标题。



Search this book:




在 Linux 下，您可以选择在以下界面中工作：一种是控制台（由多个 shell 程序之一生成的基于文本的界面）；另一种是使用图形用户界面（GUI），例如 X Window System，更 commonly known as X Windows。在 GUI 中，窗口代表应用程序和文档。即使窗口只是控制台的花哨界面，窗口化环境也能让您更高效，因为您可以同时与多个应用程序和程序交互。

> Techno Talk:
> Unlike other operating systems, X Windows, the windowing environment on UNIX and UNIX-like environments like Linux, allows you to choose your interface. In X Windows terms, the look and feel of your windows are provided by a window manager.

窗口管理器定义了用户界面的外观和感觉。KDE 是一个具有许多额外且 desirable 功能的窗口管理器，但您可以用其他管理器替代它。有些已经内置在您的系统中。


KDE 窗口的行为与其它操作系统中的对应窗口相似。窗口通常分为两类：

- Standard application windows
- Dialogs and panels

标准应用程序窗口是您在应用程序中工作的窗口。例如，如果您正在写一封信，通常会在像下一张图所示的标准窗口上进行。每个应用程序在窗口上呈现不同的功能。Web 浏览器在窗口中显示网页。文件管理器，用于管理文件和文件夹，也在窗口中工作。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_32_0.png)

KEdit，一个文本编辑器，是应用程序窗口及其元素的良好示例。

窗口顶部有一个标题栏，显示窗口的名称。通常，此名称将是应用程序或您正在工作的文档的名称。有时，对话框可能会在此区域显示其他信息性消息。标题过长的 KDE 标题栏会显示有趣的动画：标题在疯狂的乒乓舞中来回弹跳。

窗口通常还具有滚动条，沿窗口右侧和底部的滑块型控件，用于在文档视图中移动。当文档大于窗口可显示的内容时会出现滚动条。

对话框和面板是让您输入信息以告诉应用程序该做什么的窗口。您通常会在发出菜单命令或激活需要您确认的某些应用程序功能时看到它们，例如退出应用程序、保存文件等。

其他面板允许您输入命令所需的额外信息。例如，KEdit 应用程序中的查找面板需要有关要查找文本的信息。

一些面板，称为对话框，会向您提问并提供按钮供您提供答案。其他对话框只是通知您正在发生的某些事件，需要您确认以关闭该框。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_32_1.png)

面板可以具有文本字段，您在其中为命令提供额外的文本信息，以及控件，您在其中为命令指定额外的选项。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_33_0.png)

一些面板只是为您提供按钮以便从多个选项中进行选择。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_33_1.png)

一些对话框框只需您确认即可将其关闭。
## Window Controls

窗口提供多个操作控件。其中许多控件显示在窗口的标题栏区域。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_33_2.png)

KDE 窗口的标题栏区域有几个按钮。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_33_3.png)

窗口按钮显示一个包含窗口操作命令的菜单。您在那里看到的大多数命令也可以通过标题栏中的其他按钮访问。有时此按钮显示为代表应用程序的小图标。在这种情况下，小图标就是窗口按钮。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_33_4.png)

固定或固定按钮将“固定”窗口，以便窗口可从任何虚拟桌面访问。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_33_5.png)

图标化按钮将窗口折叠到任务栏。单击任务栏上的其任务按钮将使窗口重新出现在桌面上。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_33_6.png)

最大化/还原按钮将窗口扩展到屏幕上可能的最大尺寸。再次单击它会将其还原到之前的大小。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_33_7.png)

关闭按钮关闭窗口并终止应用程序。





要访问内容，请点击章节和节标题。



搜索本书：

上一页 目录 下一页


要使用一个窗口，该窗口需要获得焦点或处于活动状态。活动窗口是标题栏为深色的那个。如果开始输入，它将接收按键。同一时间只能有一个活动窗口。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_34_0.png)

活动窗口具有深色标题栏并且能够接收键盘输入。非活动窗口的标题栏为灰色。

如何激活窗口取决于焦点策略。基本上，有两种主要方式可以激活窗口：第一种是通过点击窗口（KDE 中的默认设置）；另一种是通过将光标移动到你想要激活的窗口上（其他窗口管理器的默认设置）。

我喜欢点击来切换活动窗口，因为我可以通过点击窗口上的任意位置来激活窗口并将其置于前台。另一种策略虽然在一天中可能为你节省一些点击次数，但要求你小心放置鼠标。


窗口可能完全重叠，以至于一个完全覆盖另一个。在这种情况下，你可能需要将窗口图标化以将其移开，或者通过菜单或任务栏访问你想要的窗口。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_35_0.png)

面板中的 Windowlist 菜单为你提供了访问所有打开窗口的方式。它提供了一种方便的方式来访问被其他窗口覆盖的窗口。

## 滚动条

如果窗口太小而无法显示你正在查看的文档内容，窗口将显示滚动条。如果文档比窗口更宽，滚动条会放在底部；如果文档比窗口更高，滚动条会放在右侧。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_35_1.png)

滚动条允许你查看大于窗口容纳范围的文档。

滚动条的工作方式类似于滑块：你上下（或左右）移动其滑块（也称为“拇指”），文档就会向该方向滚动。你也可以按下滚动条两端的箭头按钮来连续滚动。如果你点击滚动条区域，文档将滚动一个单位、一行或一页，具体取决于应用程序的行为。

## 调整窗口大小

可以通过抓住窗口的边缘或角落来调整窗口大小。当你处于调整大小区域时，光标会变为窗口调整大小光标（参见第 1 章，“KDE 桌面上的首次登录。”

![](img/edf072a03d4de1f8f4a13465ac79e7fb_35_2.png)

要在一维上调整窗口大小，请抓住其边缘之一。要同时在两个维度上调整大小，请从角落拖动。

## 移动窗口

你可以通过其标题栏拖动来在周围移动窗口。随着拖动，窗口会跟随你的光标。当你将窗口放置到想要的位置时，释放鼠标按钮。

移动窗口的另一种方式是通过窗口菜单下的移动命令。（你也可以通过右键单击窗口的标题栏来获得窗口菜单。）

最后，如果你按下 Alt 键并在窗口的任何位置（不仅仅是标题栏）按下鼠标按钮，窗口将跟随你拖动鼠标到任何位置。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_36_0.png)

通过拖动其标题栏移动窗口。

## 关闭窗口

当你完成对文档或应用程序的工作时，可以通过点击标题栏上的关闭按钮来关闭它。如果文档需要保存，应用程序应提示你保存更改。你通常不必担心关闭应用程序而意外丢失工作！但由于某些应用程序可能不一致，最好在关闭窗口前保存文档；否则，更改可能会丢失。窗口也可以通过从窗口菜单发出关闭命令来关闭。

要访问内容，请点击章节和节标题。

## Linux完全傻瓜指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 第 3 章
浏览文件系统

## 本章内容

- 介绍 Linux 文件系统
- 通过 KFM 查看的文件系统
- 打开文件和文件夹
- 介绍文件权限

计算机在文件和文件夹中保存和组织信息。文件可以是你畅销小说的章节，也可以是你最喜欢的地球地点的图像扫描。文件也可以是用于创建其他文件的程序或应用程序。文件夹可以包含其他文件夹和文件，而这些文件夹和文件又可以包含更多文件夹和文件，嵌套的层级可以任意多。

你计算机中的文件和文件夹构成了文件系统。在你计算机的文件系统最顶层是一个根文件夹，其中包含计算机中存储的所有文件和目录。

你计算机中的每个文件和文件夹都有一个名称来标识其内容。例如，包含你的电子邮件文件的文件夹可能恰当地命名为 "Mail"。包含你的待办事项列表的文件可能称为 "todo"。

Linux 中的文件名长度可达 256 个字符。它们可以包含数字和大小写字母。你可以使用大多数字符；然而，有一些字符应避免使用。星号 (*)、问号 (?)、与号 (&)、竖线 (|)、脱字符 (^)、引号 (") 和撇号 (') 等字符永远不应使用，因为这些字符对 shell 来说是特殊的。连字符 (-) 和空格等字符也不应使用，因为它们在 shell 中难以处理和删除。（连字符用于指定程序参数。一些工具在文件名以连字符开头时会感到困惑，因为它们会认为你是在指定参数而不是文件名。）空格会使 shell 认为你是在指定两个不同的文件。（用引号将其括起来以便从 shell 访问。）即使你只打算通过 KDE 或其他图形环境工作，也应避免这些字符。

除了描述性名称外，文件和文件夹还有一个路径名，用于标识其在文件系统中的位置。路径名列出了从根开始你必须遍历以到达该文件的所有文件夹。文件路径中的所有名称均以斜杠 (/) 分隔。路径名开头的斜杠代表根文件夹。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_38_0.png)

这是 Linux 的分层文件系统。

在 Linux 下你所做的一切都需要与文件系统交互。在 Linux 下有两种访问文件的方式：

- 通过 KDE 等图形环境
- 通过 shell 或命令提示符

本节重点介绍使用图形工具 K File Manager (KFM)，它是 KDE 环境的一部分。其他 X 环境提供自己的工具，或作为最后的手段提供 xfm（X 文件管理器）。

## 通过 KFM 的文件系统

KFM 是 KDE 的文件管理器。KFM 提供网络透明的文件访问。此术语意味着如果你的计算机连接到网络，你可以使用图形界面通过 FTP（文件传输协议）或 HTTP（超文本传输协议，Web 使用的协议）等标准互联网协议访问存储在其他计算机上的资源。此功能非常强大，因为它允许你以同等的轻松浏览位于你磁盘上的信息或位于中国计算机上的信息。

> 查看此内容：
> 通过 shell 访问文件在第 11 章“Shells and Consoles”中有详细介绍。

在 KFM 中，图标代表文件和文件夹。统一资源定位符（URLs）代表文件路径。URL 就像加强版的文件路径：它指定你可以使用各种协议访问的文件（资源）的位置。URL 通常提供



- 协议（如何访问资源）
- 机器名（存储资源的机器）
- 资源路径

除非你在过去几年里与世隔绝，否则你一定听说过互联网——并且可能熟悉像 http://www.aol.com 或 http://www.yahoo.com 这样的互联网地址。这些地址就是 URL。

文件 URL 看起来与 HTTP URL 相似：file:/home/alberto。明显的区别之一是使用的协议称为 file 而不是 http。文件协议指定本地计算机、你的计算机中的一个文件。另一个区别是冒号后只有一个斜杠，而不是你在访问网络时可能看到或使用过的两个斜杠。

KFM 窗口为你提供菜单、带有导航工具的工具栏、输入文件路径和 URL 的位置字段，以及用于消息和文件额外信息的状态区域。

通常你通过点击面板上的主页按钮来打开 KFM 窗口。KFM 窗口的其他功能包括：

- Toolbar — 为你在文件系统中移动和操作文件提供快捷方式。
- Location field — 指定你正在浏览的 URL。
- Status area — 显示有关文件和文件选择的信息。（在窗口底部）
- Home button (KFM) — 点击此按钮可创建文件查看器窗口。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_39_0.png)

KFM 显示的根目录如下所示。注意状态区域中为 vmlinuz 文件显示的额外信息。

## The KFM Navigation Toolbar

KFM 工具栏为你在目录之间移动和操作文件提供了方便的按钮：

- Up 按钮将使你从当前位置向上移动一个文件夹。
- Back 按钮将使你返回到上一个位置。如果你已在位置栏中输入了目录，后退按钮将按你导航历史的相反顺序移动你。
- Forward 按钮将在你的导航历史中向前移动。（你必须先使用过后退按钮，此按钮才会被启用。）
- Home 按钮将带你到你的主目录。
- Refresh 按钮将重新加载目录并使你所做的任何更改可见。
- Copy 和 Paste 按钮在第 6 章“组织你的文件”中进行了解释。
- Help 按钮打开帮助程序，其中包含有关 KDE 的信息。
- Task 按钮在进行长时间任务时会动画显示。如果你点击它，可以创建一个新的 KFM 窗口。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_40_0.png)

KFM 的工具栏提供各种按钮来帮助你在文件系统中导航。

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

Search this book:

Previous Table of Contents Next

## Opening a Folder

你打开一个文件夹是为了查看其中包含的其他文件和文件夹。当你打开一个文件夹时，KFM 窗口会显示新目录的内容。最初，KFM 将文件显示为大图标。其他视图格式可从 View 菜单获得。

要打开一个目录，只需点击它。你也可以使用键盘的箭头键在图标之间移动。要打开所选文件，按 Enter。键盘技术允许你“选择”一个文件。由于 KFM 使用单击来打开文件，因此用鼠标选择文件很困难：一次单击可能会带你进入你本不想打开的目录。KFM 的未来版本将允许你使用双击来打开目录。

要在一个新窗口中查看文件夹的内容，右键单击该文件夹。

要选择一个文件夹而不打开它，按住 Ctrl 键的同时点击它。

点文件——以句点 ( . ) 开头的名称的文件——通常会从文件列表中省略。要使用 KFM 查看点文件，请从 View 菜单中选择 Show Dot Files 命令。

当你打开一个目录时，显示前一个文件夹内容的视图将被新文件夹的内容所取代。

## Opening a File

你打开一个文件是为了查看其内容，就像文件夹一样。当你打开一个文件时，KFM 会通过运行与该文件关联的应用程序来打开文件。如果应用程序当前未运行，KFM 会为你启动它。当应用程序打开时，它会显示你的文件。

如果文件是一个应用程序，KFM 只会启动该应用程序。

要选择一个文件而不打开它，按住 Ctrl 键的同时点击它。

KFM 使用各种方法来尝试确定文件的类型。它使用的一种方法是查看文件扩展名（通常是文件名末尾句点后跟随的三个字符名称）。另一种方法会查看文件的内容。

如果 KFM 无法确定你的文件由哪个应用程序打开，该文件将显示一个带有问号的图标。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_42_0.png)

未知文件图标看起来像这样。

如果你尝试打开此类文件，KFM 会提示你使用哪个应用程序。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_42_1.png)

当 KFM 不知道如何打开文件时，它会提示你输入要使用的程序名称，你可以在提供的文本字段中输入。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_42_2.png)

如果你点击此面板上的 Browser 按钮，KFM 会显示它所知道的应用程序列表。

## A Tree View

KFM 提供了一个树视图，你可以用它轻松地在文件夹之间跳转。你可以通过 View 菜单中的 Show Tree 选项启用树视图。

> **Check This Out:**
> 要将文件与 KDE 应用程序关联，请参阅第 10 章“自定义 KDE。”

Show Tree 命令显示三个文件夹：根文件夹（/）、一个名为“My Home”的指向你自己主目录的快捷方式，以及一个名为“Desktop”的目录。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_43_0.png)

树视图允许你轻松地在文件夹之间移动。已打开的文件夹会显示一个向下箭头。

## A File List

你可以以包含每个文件的额外信息的方式列出当前文件夹的内容，例如其大小、所有者、权限和最后修改时间。要查看额外的文件详细信息，请在 View 菜单中选择 Long View 选项。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_43_1.png)

Long View 选项提供有关文件的更多信息。

## What the Listing Means

当你使用 Long View 显示文件夹的内容时，以下额外信息会以表格格式显示：

- 文件名
- 权限
- 文件所有者
- 文件组
- 文件大小
- 最后修改时间

让我们更详细地检查这些组件。

### File Size

这指的是文件的大小，以字节为单位。一个字节代表一个字符的信息。1024 个字符代表 1K（千字节）的数据。一个兆字节是 1024K。

### Last Changed

显示文件最后修改的时间和日期。时间使用 24 小时军用时间显示，其中 6:00PM 表示为 18:00，午夜为 0:00。

### File Owner

用户名代表文件或文件夹的所有者。这通常是创建它的人。文件的所有者可以授予文件的权限，以便其他人能够访问和读取文件。

### File Group

在 Linux 这样的多用户系统上，多个用户可以分配到一个组。组允许其成员更轻松地共享文件。组和所有者与权限密切相关。

### Permissions

文件系统中的所有文件都有三组权限。一组用于文件所有者，一组用于文件的组，一组用于其他用户。这些权限集允许文件所有者控制谁可以访问他或她创建的文件。

权限之所以有效，是因为所有用户都必须在访问计算机之前登录到 Linux。每当你访问一个文件时，系统都会检查你是否对该文件具有适当的权限。如果没有，系统会拒绝你的请求。有几种权限级别：

- 读取权限 (r) 表示谁可以读取文件
- 写入权限 (w) 表示谁可以修改文件
- 执行权限 (x) 表示谁可以运行程序或读取目录
- 权限缺失由破折号 (-) 表示

权限指定为三组；以下是权限的读取方式：

-rw-r--r-- 所有者权限可读可写
-rw-r--r-- 组权限可读
-rw-r----- 其他人权限可读
drwxr-xr-x 一个“d”标记文件夹或“目录”
lrwxrwxrwx 一个“l”标记指向文件或文件夹的链接

## Bookmarks

KFM 能够通过“书签”记住你文件系统中的位置。书签允许你保存一个位置，以便无论它有多深，你都可以快速返回。在这方面，它们的功能类似于网络书签。

要创建书签：
1. 使用 KFM 导航到所需位置
2. 在 Bookmarks 菜单下选择 Add Bookmark 命令

书签可以通过 KFM 窗口中的 Bookmarks 菜单或通过右键单击桌面空白区域来访问。

## Selecting Files and Folders

在 KFM 中，如果按住 Ctrl



key while making your selection. From the keyboard, you can use the arrow keys to move among icons. To select an icon, press the Spacebar. To open the icon, press Enter.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_45_0.png)

Using the keyboard to select multiple files. The box around the icon indicates the current icon. To move to another icon, use the arrow keys.

Previous Table of Contents Next

## SPIDER KILLER

## spider catcher

HOME ACCOUNT INFO SUBSCRIBE LOGIN SEARCH MY ITKNOWLEDGE FAQ SITEMAP CONTACT US

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Bookmark it

Search this book:

Previous Table of Contents Next

## Chapter 4
Working with Applications

## In This Chapter

- Various ways you can launch and stop applications
- How to work with multiple applications
- How to use virtual desktops
- A list of some of the KDE applications that you might find in your application starter

Both KDE and Linux come with a number of applications ready to use. This chapter teaches you how to work with applications in a graphical environment. You'll see that working with multiple applications at the same time is very easy under a graphical environment such as KDE.

> Techno Talk: Applications, Programs, and Tools
> So what is the difference between an application, a program, and a tool? All of them are programs. A program is something that runs in your computer.
> 
> In general, an application is a program that is interactive, uses a graphical user interface (GUI), and is flexible for a number of tasks.
> 
> A tool can sometimes be interactive and guide you through various steps, but it is more limited in scope. Typically, tools run in the command line, but depending on the tool, it could also have a GUI.
> 
> In this book I use the terms interchangeably; however, most of the time, an

### Manually Starting an Application

There are several ways you can start an application:

- If the application appears on the panel, you can click its icon.
- If you are browsing using KFM and you see the applications icon in a window, you can also click it to start it up.
- If you know the name of the application’s program file, or “binary,” you can type it into a shell to launch it. (You will get information on how to work with a shell in Part 2 of this book, “Working on the Command Line.”)
- Finally, if the application is available on the Application Starter (K Menu), you can launch it by picking the appropriate entry in the menu. The Application starter is shown in the following figure.

When an application is launched, Linux will load it into memory and start it. After a few seconds of disk activity, you will see its window appear. A task button is also added to the taskbar to represent it.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_47_0.png)

The KDE Desktop gives you several ways of starting an application.

Documents or applications stored in Autostart are launched when you start the session. Applications can also be started by typing their name on the command line.

An application can also be started by clicking on the icon for a document associated with it. If you click on a document, its application will start up and display the contents of the document.

> **Check This Out:**
> Applications and documents are associated via kdelnk files. Kdelnk files have a `.kdelnk` extension. These files provide information that allows KFM to associate icons, documents, and applications. Having these associations allows KFM to open your document with an application when you click on a document’s icon. For more information on `.kdelnk` files, see Chapter 10.

### Working with Multiple Applications

Linux is a multitasking operating system. Working and running with multiple applications at the same time is easy under a graphical environment such as KDE. Even though many applications can run at the same time, there’s only one active window.

The active window displays a differently colored title bar, and its button on the taskbar appears to be pressed. The active application is the one that is able to receive keyboard input. Even though some of your applications are running in the background, that does not mean they are idle. If you have a lengthy operation running in one application, you can work on a different application while the other task completes in the background.

### Switching Between Applications

There are two ways that you can switch between applications: If the application window you wish to make active is visible, you can click in it; or if the application is hiding or if its windows are displayed in a different desktop, click the task button representing the application in the taskbar (see the following figure).

![](img/edf072a03d4de1f8f4a13465ac79e7fb_48_0.png)

Switching between applications.

You can also switch between applications by pressing Alt+Tab. If you keep the Alt key pressed and then hit Tab, you will see a series of icons representing all running applications. Hitting Tab again (while still holding the Alt key) will display the next application on the list. When you have found the application you want to make active, let go of the Alt key.

### Hiding an Application

You can hide an application by clicking its iconify (also called minimize) button. The application is still running and available, but its windows are removed from the screen. A hidden application continues to display a button in the taskbar.

Say you’re working with multiple applications and you’re finished with one, but you think you will need the application again soon. It is faster and easier to hide it and keep it running than to quit and restart it later.

When you click the application’s button in the taskbar, the application and its windows are restored to their previous location.

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

### Virtual Desktops

In KDE you have the ability to work in more than one desktop at a time. This ability is useful if you perform different tasks that require various groups of applications running at the same time.

Using a virtual desktop is similar to hiding applications, except that when you move between desktops, all applications belonging to that desktop are restored to their previous state. For example, you can use one virtual desktop to compose your email and read Internet news, another for a task such as programming or writing, and yet another to play a game or do anything that strikes your fancy.

In KDE you can have up to eight different virtual desktops. By default, however, only four are available. (Later, in the section “Changing the Number of Virtual Desktops,” you’ll learn how to customize the number of desktops you have accessible.) Different desktops have different color backgrounds to help you tell them apart. By default, the virtual desktops are called One, Two, Three, and Four, but you can rename them as you see fit.

The Virtual desktops feature and KDE’s Workspace Auto-restore feature make a powerful combination. You will find more information on the KDE Workspace Auto-restore feature later in the section “The KDE Workspace Auto-restore Feature.”

### Switching Between Desktops

To switch between virtual desktops, click the desktop button in the panel (see the following figure). If you like keyboard commands, you can also press Ctrl+Fn, where n is the number of the virtual desktop you want to view. You can also press Ctrl+Tab to cycle between the various desktops.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_50_0.png)

To switch between desktops, click the button for the desktop you want to visit.

If you click on a task button for an application that is active in a different desktop, you will also switch to that desktop.

To switch between applications and desktops and get a list of the current tasks organized by desktop, press Ctrl+Esc. (Alt+Esc also works for this purpose. And, you can use the Windowlist menu in the panel for this purpose. See "Accessing Windows that Overlap" in Chapter 2, "Working with Windows.")

### Sending an Application to a Different Desktop

To send an application to a different desktop, you can use the window menu and pick the appropriate desktop from the To desktop submenu. The window menu is accessible from all KDE windows (see the following figure).

![](img/edf072a03d4de1f8f4a13465ac79e7fb_50_1.png)

Use the To Desktop submenu to move an application to a different desktop.

Alternatively, you can right-click the window’s title bar to display a number of menu commands, including the To desktop submenu. Note that the icon displayed for this menu will be different depending on the application you are running.

When you send an application to a different desktop, the application disappears from the current desktop and reappears in its new desktop. To see the application again, view the desktop to which you sent it.

### Sharing an Application Across Virtual Desktops

There are some applications that you must use in all desktops. A good example of this is the file manager. Instead of having multiple KFM windows in different desktops, it might be better to share the application with all desktops. You use the pin icon (also called the stick button) in a window for this purpose (see the following figure). Windows that have this button pressed will be accessible from all desktops.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_50_2.png)

To “pin” a window and make it visible from all desktops, click the pin icon on a window’s title bar.





![](img/edf072a03d4de1f8f4a13465ac79e7fb_51_0.png)

固定一个窗口会使其在所有桌面上显示。在此图中，KFM 窗口被所有虚拟桌面共享。

## 桌面分页器：切换应用程序和桌面

KDE 还包含一个名为 Desktop Pager 的桌面分页器应用程序。桌面分页器是一种应用程序，它提供所有虚拟桌面及其包含窗口的缩小视图。

在桌面和应用程序之间切换只需选择正确的按钮和所需的应用程序即可。应用程序窗口会根据其所属的应用程序进行标记。

Desktop Pager 可从应用程序启动器菜单中的系统应用程序组获得。您也可以通过在 shell 中发出命令 kwmpager 来启动分页器。

## 启用活动桌面边框选项

您可以配置虚拟桌面，以便在移动窗口并触及屏幕边缘时自动在桌面之间切换。此功能在跨桌面移动应用程序时可能感觉更自然。桌面按面板和 Desktop Pager 工具上显示的相同地理位置排列（参见上一图）。

要启用 Active Desktop Borders 功能，您需要从应用程序启动器菜单访问 KDE 控制中心应用程序。控制中心窗口出现后，通过单击其旁边的加号展开桌面类别，然后选择桌面选项。选中启用活动桌面边框选项（参见下一图）。（此项也可通过应用程序启动器中的设置菜单获得，选择桌面，然后从子菜单中选择桌面。）

![](img/edf072a03d4de1f8f4a13465ac79e7fb_51_1.png)

Desktop Pager（kwmpager）显示带有所有虚拟桌面缩略图视图的按钮。要更改桌面，只需单击所需的桌面按钮即可。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_52_0.png)

您可以在此对话框中启用 Active Desktop Borders。

Previous | Table of Contents | Next

Products | Contact Us | About Us | Privacy | Ad Info | Home

Use of this site is subject to certain Terms & Conditions. Copyright © 1996-2000 EarthWeb Inc. All rights reserved. Reproduction whole or in part in any form or medium without express written permission of EarthWeb is prohibited.

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

## Changing the Number of Virtual Desktops

根据您的工作习惯，您可能需要比 KDE 提供的初始四个虚拟桌面更多或更少。如果是这种情况，您最多可以拥有八个桌面。要向 KDE 环境添加更多桌面，请转到应用程序启动器（面板上的 K 菜单），选择面板，然后选择配置命令。这将显示 KPanel 配置窗口。选择桌面选项卡（参见下图）。可以通过滑动可见滑块添加或删除额外的桌面。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_53_0.png)

您可以使用 KPanel 配置窗口添加最多八个虚拟桌面。

## 自定义虚拟桌面的外观

您可以通过激活应用程序启动器，选择设置，选择桌面并选择背景工具来控制虚拟桌面的外观。您将看到如下所示的显示设置对话框：

![](img/edf072a03d4de1f8f4a13465ac79e7fb_54_0.png)

您可以在显示设置对话框中自定义虚拟桌面的外观。

## 自动启动应用程序

KDE 桌面有一个名为 Autostart 的特殊目录。Autostart 目录中的任何程序或文件在您启动 KDE 会话时都会自动启动。

要将文件放入 Autostart 目录，请使用 KFM 应用程序导航到包含所需文件的目录。单击该文件，将其拖到 Autostart 目录并释放鼠标按钮。KFM 将显示一个菜单，让您选择将文件复制、移动或链接到 Autostart 目录。选择链接。下次登录 KDE 时，文档将在登录时打开。

您可以在 Autostart 目录中放置目录和应用程序的链接。目录的链接会在登录时在桌面上显示指向该目录的文件夹窗口。应用程序的链接会在登录时启动该应用程序。

## KDE 工作区自动恢复功能

如果您在先退出所有打开的应用程序之前注销系统，KDE 将记住您留下的打开的应用程序和文档，并在下次登录时恢复它们。如果您使用多个应用程序并且在组织各个桌面时花费了很多精力，此功能会很有用。

要使此功能正常工作，应用程序必须能够与 KDE 桌面通信。通常，只有 KDE 感知（或 X11 感知）应用程序才能执行此功能；命令行程序没有此功能，因此无法使用。如果应用程序足够复杂，它可能还能够记住您正在编辑的文档并为您打开它。当您退出工作区时，KDE 会警告您不支持此功能的应用程序。

## KDE 应用程序帮助：kdehelp

大多数 KDE 应用程序都提供内置帮助。可以通过帮助菜单访问此帮助系统。从帮助菜单中选择内容命令将打开 kdehelp 查看器。此工具是用于帮助信息的专用浏览器。如果您熟悉使用 Web 浏览器，您将不会有任何问题来浏览此系统。简而言之，下划线文本是超链接。单击超链接将带您到文档中讨论该主题的位置。

kdehelp 工具也可以从面板访问（参见下图）。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_55_0.png)

kdehelp 工具是用于浏览 KDE 文档的专用 Web 浏览器。

此窗口的功能包括：

- 所有 KDE 应用程序都有帮助菜单。选择内容命令以打开 kdehelp 工具并选择内容。
- 单击下划线文本将向您显示有关下划线主题的更详细信息。
- kdehelp 工具也可以通过单击面板上前一图中指出的图标来启动。

## 退出应用程序

要退出应用程序，您可以单击主窗口的关闭按钮或使用文件菜单下的退出命令。由于您使用的某些应用程序的行为可能不一致，因此在单击窗口的关闭按钮之前始终保存文档是个好主意。行为良好的应用程序在退出前应给您保存工作的机会。

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Chapter 5
创建、编辑和保存文件

## 本章内容

- 创建新文件
- 打开现有文件
- 使用打开面板
- 保存文档的更改
- 编辑文本

文件将信息存储在计算机磁盘上。当您在编辑器窗口中给朋友打字时，您输入的文本存储在计算机内存中。您的信件通常被称为文档。如果您在先将文档保存到计算机磁盘上的文件之前退出程序，信息就会丢失。当您将文档保存到文件时，您以后可以打开它并继续编辑上次保存时中断的地方。

在本章中，您将学习如何在应用程序内部处理文件：如何打开和保存文件以及如何保存文件的不同副本。本章还作为如何使用原型应用程序的介绍，例如 KDE 提供的编辑器 KEdit。（KEdit 是随 KDE 捆绑的简单文本编辑器。）




## 创建和保存文件

所有 KDE 应用程序都使用相似的菜单和命令来保存和打开文件。如果你使用的应用程序不属于 KDE 或未针对 KDE 环境设计，界面会稍有不同。总体而言，它应该与 KDE 应用程序类似，你应该能够轻松地在其中导航。

### 创建新文件

通常，当你想要创建新文件时，你会打开一个应用程序并开始工作。通常，应用程序会以空文件开始（有时是文档，但不总是）。如果应用程 [已经运行]，你可能需要创建一个新的文档窗口，方法是运行新实例或使用应用程序的“新建”命令。通常，这个命令在 KDE 中会在“文件”菜单下找到。一些应用程序允许你同时工作于多个文档；一些则只允许你一次编辑一个文档。如果你的应用程序只支持单个文档，你可以通过启动另一个应用程序的实例来绕过这个限制。在下面的图中，你会看到 KEdit（一个文本编辑器）。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_57_0.png)

创建新文件的过程与选择菜单命令一样简单

这个窗口的特点包括：

- 文件菜单，提供处理文档和应用程序的命令，如“新建”用于创建新文件，“打开”用于打开现有文件，“保存”用于保存文件，“关闭”用于关闭文档，“退出”用于退出应用程序。
- 选择“新建”来创建新文档。如果你想同时工作于多个文档，可以使用“新建窗口”命令或启动另一个应用程序实例。
- KEdit 图标是右侧第二个图标（铅笔带绿色封面）：在面板上点击它的图标来启动 KEdit。
- 未保存窗口的标题是“Untitled”。

当你在应用程序中保存工作时，它会存储在文件中，以便你稍后读取或修改。第一次保存文件时，你需要为文件命名。

如果你在不保存的情况下关闭文档窗口，你的工作会丢失，因为你没有将它保存到磁盘。良好的程序会在你退出它们或关闭未保存窗口时提示你保存文档。一些不太严谨的程序会毫无警告地直接丢弃你的工作。远离表现出这种行为的程序。

### 打开现有文件

要打开现有文件，你可以从“文件”菜单中使用“打开”命令（见下面的图）。“打开”命令会显示一个面板，让你选择要使用的文档。你可以使用这个面板浏览你的文件夹（目录），直到找到想要编辑的文档。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_58_0.png)

“打开”面板允许你打开现有文件以查看、编辑，或者在某些情况下仅选择文件。

与使用用户界面控件在目录之间导航相比，有时直接在“位置”字段中输入路径和文件名可能更快更方便。

当你点击文件时，“打开”面板会消失，文档会加载到应用程序中。

### 自定义“打开”面板

“打开”面板提供了许多选项，你可以使用它们来配置文件的显示方式。要更改配置，请选择“配置”按钮（见下面的图）。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_58_1.png)

你可以在该对话框中自定义“打开”面板的许多元素。

### “打开”面板的自定义设置

大多数自定义设置都显而易见。我最喜欢的自定义是混合目录和文件（见下面的图）以及取消勾选单击一次打开文件或目录。（双击打开可以减少因单击误打开错误文件的可能性。）

![](img/edf072a03d4de1f8f4a13465ac79e7fb_59_0.png)

“打开”面板的显示，混合了目录和文件。

### 保存新文件

当你第一次保存文档时，你会创建一个文件。在过程中，你需要为文件命名。使用“保存”或“另存为”命令（在应用程序的“文件”菜单下）可以将文档保存为文件。选择“另存为”命令会提示你输入文件名和保存位置。文档保存后，使用“保存”命令会更新文件的内容，包含你所做的任何新修改。如果文件尚未保存，那么“保存”命令的行为与“另存为”命令相同：它会提示你输入文件名。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_59_1.png)

“另存为”面板允许你为文件命名

这个面板的特点包括：

- 类似“打开”面板的按钮，提供快速浏览文件和目录的方式
- 在“文件夹”窗口中，选择你想要放置文件的文件夹
- 在“位置”区域，输入文件的名称

点击“确定”保存文件。

当你保存文件时，你的工作会保存到指定目录的磁盘中。已保存文档的标题栏会从“Untitled”变为显示文件的名称和路径（见下面的图）。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_59_2.png)

已保存文档的标题栏显示文件名。

要查看内容，点击章节和节标题。

### 完整的傻瓜指南 to Linux

（出版社：Macmillan Computer Publishing）
作者（s）：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索这本书：

### 文件命名

你几乎可以为文件命名任何你想要的样子。但是，你需要遵守一些限制。

新文件名不能与同一目录中的另一个文件重复。如果发生这种情况，现有文件将被新文件替换。

文件名区分大小写；也就是说，Linux 将 introduction.txt 和 Introduction.txt 视为不同的文件。

某些字符——如星号（*）、问号（?）、井号（&）、竖线（|）、脱落号（^）、双引号（"）和撇号（'）——绝对不要使用，因为这些字符对 shell 具有特殊意义。

像破折号（-）和空格这样的字符不应使用，因为它们在使用 shell 时会带来困难，并且在删除时会很麻烦。破折号用于指定程序参数。一些工具在文件名以破折号开头时会出错，因为它们会误以为你是在指定参数而非文件名。空格会让 shell 认为你指定了两个不同的文件（通过引号将它们括起来可以在 shell 中访问它们）。即使你只通过 KDE 或其他图形界面工作，也应避免这些字符。

文件名通常包含一个扩展名，用于指示文件类型。这个扩展名很重要，因为它告诉 KFM 在点击文件时使用哪个应用程序打开它。

一些常见的文件类型如下：

- .txt 用于文本文件
- .gif 用于 GIF 图像
- .jpeg 或 .jpg 用于 JPEG 图像
- .zip 用于压缩文件
- .gz 用于 gzip 压缩文件
- .tar 用于 tar 归档
- .pl 用于 Perl 脚本

### 保存文档的修改

如果你在创建文件后对其进行修改，你需要再次保存它以存储新修改。为此，你可以使用应用程序“文件”菜单中的“保存”命令。

在工作会话期间，你应该频繁保存文件，以防止因程序错误或电源故障导致工作丢失。

### 保存新版本

许多时候，在创建文档时，直接基于现有文件创建新文档更为方便。你可以使用“另存为”命令将文档保存到另一个文件中，从而重用和修改现有文档，同时保留旧文档。你也可以使用“另存为”命令创建文档的不同版本。这样，你可以回到之前的编辑版本。

### 文本编辑基础

除了打字，还有一些文本编辑基础你应该学习，以便更有效地使用计算机。请记住，有些描述的操作在所有应用程序中可能不适用。

大多数文本编辑都基于“选择”的概念。选择是指通过点击并拖动来高亮的文本。通常，高亮文本是因为它是其他命令的目标。继续阅读，了解更多关于选择文本的信息。

### 选择文本

要选择文本，点击你想要开始选择的位置，然后拖动鼠标到你想要结束的位置（见下面的图）。高亮区域即为选择。你可以对当前选择应用格式和编辑命令。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_61_0.png)

要选择文本，点击你想要开始的位置，然后拖动到你想要结束的位置。

一些应用程序允许你通过点击来定义选择，然后拖动。





begin the selection and then Shift+clicking where you’d like to end it.

To select a word, you can double-click the mouse while the cursor is over a word. Some applications allow you to select a sentence if you triple-click over it, and some even allow you to select an entire paragraph if you click your mouse four times over the paragraph.

## Copying and Moving Text

The commands to copy and move text in your document are in the Edit menu. To copy text from your document, select the text and choose the Copy command (see the following figure).

![](img/edf072a03d4de1f8f4a13465ac79e7fb_62_0.png)

To copy information, select the text you want to copy and choose the Copy command from the Edit menu.

To move text, first select the text and then choose Cut from the Edit menu. Then click your mouse where you want to place the information and choose Paste from the Edit menu. Paste will insert text that you copied or cut. You can even use this technique to move text between applications.

> Check This Out:
> Under X (and KDE!), a shortcut to the copy and paste routine is to select text as you normally do, move your cursor where you want to place a copy, and then middle-click the mouse. (Or as you learned in Chapter 1, “The First Login on the KDE Desktop,” if you are using a two-button mouse, you can click both buttons simultaneously to simulate a middle click. However, for this to work, you must have specified the correct settings when you configured X Windows. See Appendix A, “Linux Installation.”)

Text and information that you move in this way is placed in the clipboard. The clipboard is shared between running applications. This means that a selection you copy or move from one application can be inserted into another open application. Although this is true for most applications, some not-so-friendly applications don’t make their clipboard available to the rest of the system.

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

## Chapter 6
Organizing Your Files

## In This Chapter

- Creating Folders
- Working with Files and Folders
- Emptying the Trash
- Setting File and Folder Permissions
- KDE Templates

## Getting Organized: Creating a Folder

Folders, or directories, allow you to group your files along some criteria. (For example, files for a book project all go in one folder, and files for your correspondence go in another.) This grouping capability will help you locate your files more easily. This will be more important as the number of files you create and store grows.

To create a folder using KFM, in an open KFM window, navigate with your mouse to the location where you want to create the new folder. Choose New from the File menu and choose Folder from the submenu.

After you have selected Folder from the submenu, a panel asking you for the name of the folder will be displayed (see the following figure). Type the name for the folder. (Pick a name as suggested in the section "File Naming" in Chapter 5, “Creating, Editing, and Saving Files.”) Then press Enter.

New folders are empty by default and ready for you to add files and other folders to it. In the “KDE Templates” section later in the chapter, you’ll learn how to customize the New command so that you can create files and folders that already contain other documents.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_64_0.png)

The New command under the File menu is customizable, which is why you have to navigate two menus to find the Folder option

![](img/edf072a03d4de1f8f4a13465ac79e7fb_64_1.png)

In this panel, type the name of the new folder you want to create.

## Copying Files and Folders

You can copy files and folders into other folders. When you copy a folder, all the files and folders it contains are copied, too. In KFM, there are two ways that you can copy files and directories: using drag-and-drop and using the Clipboard with Copy and Paste.

## Copying Files Using Drag and Drop

When you copy files using drag and drop, you click and drag the file you want to copy into another directory, onto the desktop, or into another KFM window. A menu appears asking you if you want to copy, move, or link the item (see the next figure).

## Copying Files Using the Clipboard

You can also copy files and folders using the clipboard. To copy a file, select it (Ctrl+Click) and then choose Copy from the Edit menu. Navigate in the KFM window to the directory where you would like to place the copy and choose Paste from the Edit menu.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_64_2.png)

Copying a folder using drag-and-drop.

## Moving Files and Folders

Moving files and folders is almost the same as copying the files using drag-and-drop. Instead of picking Copy from the pop-up menu, you pick Move (see the previous figure). Similar to copying a folder, if you move a folder, all files and folders inside the directory are also moved.

## Linking Files and Folders

If you often find yourself copying files in order to have easy access to them, Linux has a better solution: links.

A link is a pointer to a file or folder that is somewhere else in the file system. A link looks and acts like the file or folder it points to. If you are viewing it through KFM, it will have the same icon (with the exception that it will have a little arrow next to it). When you open a link, you see the same file contents as the file the link points to.

Links are created in the same way you copy or move files using drag and drop. You click and drag the file you want to link into another folder or the desktop, and when you let go of the mouse button, you choose Link from the menu that is displayed.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_65_0.png)

## Replacing a File or a Folder

If you drag and drop a file whose name already exists in the directory, KFM will ask you if you would like to replace the original file or abort the operation (see the next figure).

Replacing a folder or a file permanently removes the file you are replacing. When you go to replace a file, KFM presents you with a dialog box that allows you to do one of three things: Rename the file (if you don’t want to replace the original), skip the operation, or overwrite the file. If you drag multiple files, you can answer the dialog box a file at a time, or you can overwrite all files without any additional warnings.

Be careful when you replace files. It’s important to remember that files that you overwrite are not recoverable.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_65_1.png)

## Deleting a File or Folder

To delete a file or a folder, select it and then choose Delete from the Edit menu. The file or folder will be destroyed after you confirm your action (see the following figure). Deleted files are not recoverable.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_65_2.png)

box.

## Moving a File or Folder to the Trash

A safer way to remove files than using Delete is to move them to the Trash. The Trash is a special folder on your Desktop where you can put files you want to get rid of. Instead of immediately being deleted, the file remains in the trash until you empty it. This allows you some extra time to ensure that you won’t be needing the file.

To move a file to the trash, select it and then choose the Move to Trash command from the Edit menu.

You can also move files to the Trash using drag and drop. Just click on the file you want to move to the trash and, without letting go of the mouse button, drag the mouse over the Trash icon on your desktop; then release the mouse.

## Retrieving a File or Folder from the Trash

Files moved into the Trash remain there until you empty the Trash. If you haven’t emptied the Trash since you moved a file there, you can get it back. The Trash is just a special folder for holding documents you are about to delete. You can open it as you do other folders by clicking on it. To rescue a file, just click it and move it out of the Trash.

## Emptying the Trash

As the amount of trash grows, you might wish to empty it to regain the disk space consumed by trashed files. To empty the Trash, right-click its icon and choose Empty Trash Bin from the menu that is displayed (see the following figure).

![](img/edf072a03d4de1f8f4a13465ac79e7fb_66_0.png)

To empty the Trash, right-click the Trash Bin icon and choose Empty Trash Bin from the resulting menu.





要访问内容，请单击章节和节标题。

## 完全傻瓜的 Linux 使用指南

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

### 文件属性

创建文件或文件夹后，你执行的大多数操作将以重命名或更改权限的形式进行。KFM 通过在其图标上右键单击为上一节中描述的一些操作提供了快捷方式。上下文菜单将弹出以显示多个选项（见下图）。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_67_0.png)

KFM 上下文菜单在你右键单击文件或文件夹时显示各种选项。

上下文菜单中的命令取决于你单击的内容——因此得名。

- Open with—显示一个面板，你可以在其中输入要用于打开所选文件的应用程序的名称。
- Up—向上导航一个目录。
- Back—导航到上一个目录。
- Forward—如果你使用 Back 来到达此目录，可以使用 Forward 返回到上一个位置。
- Cd—将当前窗口聚焦到所选目录。
- New View—在新的 KFM 窗口中打开目录。
- Copy—将文件或目录复制到剪贴板。然后你可以使用 Paste 命令将复制的文件或目录放置在当前目录中。
- Move To Trash—将所选文件或目录移动到名为 Trash 的特殊目录。这会将文件从当前位置移除，但不会删除它们。
- Delete—删除所选项目。
- Add To Bookmarks—将所选文件夹添加到你的书签列表中。
- Properties—弹出一个面板，允许你检查和更改有关文件的信息，例如其权限设置和名称。

### 重命名文件或文件夹

要重命名文件或文件夹，请右键单击该文件或文件夹并从显示的菜单中选择 Properties。这将显示一个面板，允许你重命名文件（见下图）。

重命名文件时，请注意不要更改文件的扩展名（如果有）。文件扩展名由文件名末尾的句点后跟的三个或更多字符组成。扩展名将文件与应用程序关联起来。

有很多东西你不应该重命名。你主目录中的所有内容都是你的，可以随意重命名。但是，Linux 根目录或其他系统相关区域中的文件应保持不变。大多数用户无需担心；一般来说，除非你在超级用户（root）账户下工作，否则 Linux 不会允许你更改不应更改的任何内容。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_68_0.png)

General 选项卡显示有关文件的通用信息，例如其名称和路径。要重命名文件或文件夹，请在名称文本字段中输入新名称并按 Enter。

### 设置文件和文件夹权限

Properties 面板还允许你修改和设置创建的文件和文件夹的权限设置。权限在第 16 章“Permissions: Protecting and Sharing Your Work”中有详细说明。如果你觉得需要控制权限，我建议你先阅读本章以了解更改设置的影响，因为权限是一个高级主题。本节解释如何使用 KFM 更改权限，并假设你了解这些影响。

权限允许你保护文件和文件夹免受其他用户的访问。默认情况下，你创建的文件会分配一组权限。在使用 KDE 时，你可以使用图形控件更改文件权限。要进入权限面板，请右键单击文件或文件夹并从出现的菜单中选择 Properties。然后选择 Permissions 选项卡（见下图）。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_69_0.png)

Permissions 选项卡显示用于设置文件或文件夹权限的多个控件。每个设置都为文件的所有者（User）、分配给文件的组的成员（Group）以及其他人（Others）重复。通过设置值，你可以为不同用户控制不同级别的访问。

权限可以在 Permissions 选项卡中以多种方式更改：

- User 行设置目录所有者的权限。
- Group 行设置组成员的权限。
- Others 行设置既不是所有者也不是组成员的用户权限。
- Owner 字段显示拥有该文件的用户名称。
- Group 选择菜单显示分配给此文件的组名称。如果你是文件所有者并且属于多个组，则会显示选择菜单。
- Show Entries 列允许用户查看目录内容。
- Write Entries 列允许用户向目录添加或删除文件。
- Change Info 列允许用户遍历目录。
- Special 列启用特殊设置

面板的外观会根据你操作的是文件还是文件夹而略有不同。如果你操作的是文件，权限列将称为 Read、Write 和 Execute 权限。否则，它们将称为 Show Entries（Read）、Write Entries（Write）或 Change Into（Execute）。尽管标签不同，但其功能完全相同。

#### Techno Talk：每个权限控件的作用

每个文件与用户在一种或多种角色相关（见下图）：

- 用户可以是文件的所有者
- 用户可以是被授予文件权限的组的成员
- 用户既不是所有者也不是组的成员

这些角色中的每一个都可能具有 Read、Write 或 Execute 权限，或其组合。

对文件或文件夹的 Read 权限允许你查看（读取）其内容。

对文件或文件夹的 Write 权限允许你更改其内容。对于文件夹而言，这可能意味着你有权向目录添加文件。

Execute 权限是特殊的。当设置在文件上时，表示该文件是一个程序。如果你的角色具有 Execute 权限，你就可以运行该程序。对于目录，Execute 权限还控制谁可以进入目录。如果你打算将文件复制到目录中，你的角色必须对该目录具有 Execute 权限。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_70_0.png)

### 理解权限面板。

在前述的 Permissions Panel 图中，用户（文件所有者）具有 Read 和 Write 权限；分配给文件的组的成员具有 Read 和 Write 权限；其他用户能够读取文件，但由于缺乏写权限而无法修改它。

如果权限设置被选中，则表示已启用。权限只能由文件所有者或超级用户（root）分配。

除非你知道自己在做什么，否则不要更改文件或文件夹的权限。例如，如果你删除文件夹的 Change Into 设置（Execute 权限），你将使任何用户都无法导航或打开该文件夹中的文件。

+ Previous | Table of Contents | Next

### 更改文件或文件夹的组

如果你与一组其他用户协作进行项目，你可能希望授予他们访问一组文件和文件夹的权限。当你创建文件或文件夹时，它们会自动分配给你的默认组。如果你是其他组的成员，你可以重新分配对文件和文件夹的不同组访问权限。

要更改文件或文件夹的组成员身份，请右键单击它并选择 Properties；然后从显示的面板中选择 Permissions 选项卡。

要更改文件的组，请单击组选择菜单以显示你所属的组并选择你想要的组（见下图）。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_71_0.png)

如果你属于多个组，你可以为你的文件分配不同的组。

### KDE 模板

KDE 提供了一个有用的功能：Templates。模板允许你创建原型文档和文件夹结构，以便轻松重复使用和自定义。





当你在桌面上的 Templates 目录中放置文件和文件夹时，你是在自定义在文件菜单中的 New 命令下会看到的内容。你放置在其中的文件或文件夹的名称将显示在子菜单中。当你想要创建一个模板的自定义副本时，只需从菜单中选择其名称。系统会为你创建一个文档或文件夹结构的副本以供自定义。这在你想要重新创建某种目录或文件组织时很有用。如果你在此目录中放置普通文件，你就可以将这些文件用作新文档的起点，而无需搜索目录。

Previous | Table of Contents | Next

要访问内容，请单击章节和节标题。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Chapter 7
Working with Disks

## In This Chapter

- Starting a Superuser Session
- Configuring Floppy and CD-ROM Drives
- Granting Access to Disk Devices
- Working with Floppies and CD-ROMs

在 Linux 中使用磁盘与在其他操作系统中略有不同。在 Linux 和 UNIX 中，磁盘被挂载到文件系统中。挂载文件系统会将磁盘的内容合并到目录树中。当你完成对磁盘的操作后，通常会卸载它。卸载文件系统会将其从文件树中移除。挂载不仅仅限于磁盘。通过网络可用的卷（网络驱动器）也可以被挂载和卸载。

卷可以挂载在文件系统的任何位置。在 Linux 下，它们默认的挂载位置是 /mnt。/mnt 目录将至少为你的软盘和 CD-ROM 驱动器各有一个目录；这些目录通常分别命名为 floppy 和 cdrom。floppy 和 cdrom 目录是空的，只有在磁盘或卷被挂载到该目录时才会包含文件和文件夹。如果你将卷挂载到包含文件的目录上，该目录的内容将被隐藏且无法访问，直到卷被卸载为止。

默认情况下，将磁盘挂载到文件系统中是一个受限操作。为了使普通用户能够访问这些设备，你需要告诉系统允许用户挂载该设备。你将在下一部分学习如何操作。

## Configuring the System to Allow Users to Access the CD-ROM and the Floppy

系统在 /etc/fstab 中保存磁盘及其挂载位置的配置文件。此配置文件只是一个普通文本文件，你可以使用任何文本编辑器（包括 KEdit）进行编辑。然而，修改此文件的权限仅限于 root，即超级用户；要更改和修改此文件，你需要拥有此权限。

你可以通过两种方式获得此权限：

- 你可以退出系统，以 root 身份登录，然后重新进入系统
- 你可以启动一个具有超级用户（root）权限的文件管理器

为了学习一个新技巧，让我们逐步介绍第二个选项。

## Starting a Superuser KFM Session

要以超级用户身份启动 KFM 窗口，你可以进入 Application Starter|System 并选择 File manager (Superuser Mode) 命令（见下图）。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_74_0.png)

从 System 子菜单启动具有超级用户权限的 KFM 窗口。

这将显示一个要求输入 root 密码的窗口。输入后，将显示一个与你之前使用过的类似的 KFM 窗口。

超级用户 KFM 窗口与普通 KFM 窗口的区别在于一个红色标签，提醒你在操作文件和目录时要谨慎（见下图）。一次错误的操纵就可能破坏你的系统。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_74_1.png)

超级用户 KFM 窗口在菜单栏面板上有一个红色标签。

在 root KFM 窗口的位置字段中输入 /etc/fstab 并按 Enter。将会启动一个新的 KEdit。此实例继承了超级用户权限，允许你修改文件。

在完成文件编辑后，如“Creating kdelnk Files for the Floppy and CD”一节所述，关闭 KEdit 窗口和 KFM root 窗口，以确保你不会无意中使用这些具有权限的应用程序。

## Enabling Regular Users to Access Disk Devices

你的 /etc/fstab 将包含类似以下内容的文本：

```
/dev/hda1 / ext2 defaults 0 1
/proc /proc proc defaults 0 0
/dev/hda5 none swap defaults 0 0
/dev/hdd /mnt/cdrom iso9660 ro,noauto,user 0 0
/dev/fd0 /mnt/floppy ext2 defaults,noauto 0 0
```

要使任何用户都能访问软盘，你需要修改以 /dev/fd 开头的行。通常，它被称为 /dev/fd0，即代表软盘的设备。如果你有多个软盘驱动器，/dev/fd0 代表 DOS 驱动器 A:（第一个软盘驱动器），/dev/fd1 代表 DOS 驱动器 B:（第二个软盘驱动器），以此类推。/etc/fstab 中软盘驱动器的条目需要修改为如下所示：

```
/dev/fd0 /mnt/floppy auto user,defaults,noauto 0 0
```

在此条目中，我将 ext2 改为 auto；这将允许系统检测并读取 DOS 和 Windows 软盘，以及原生 Linux 软盘。我还通过在 defaults 选项前添加 user 选项来修改选项列表。这将使普通用户能够挂载软盘。请注意，逗号和选项之间没有空格。

### Techno Talk:

/etc/fstab 文件中的每一行具有以下格式：

```
device mountpath fstype options dump_order check_order
```

- device 指定代表磁盘的设备文件的名称。UNIX 设备如你的软盘由设备文件表示。这些是特殊文件，当被访问时，它们实际上与你的硬件交互。设备文件位于 /dev 目录中。当程序需要使用设备时，它会像操作普通文件一样对其进行读写。这简化了程序与不同硬件通信的方式。对于软盘，设备文件名以 /dev/fd 开头。文件名末尾的数字允许使用同一种类的多个设备。你的 CD-ROM 通常为 /dev/cdrom，这实际上是一个链接到更具体的<|message|>
- mountpath 指定设备挂载的位置。通常，这将是 /mnt/floppy 或 /mnt/cdrom，分别对应你的软盘和 CD-ROM 驱动器。
- fstype 指定文件系统的格式。如果你指定 auto，系统将尝试为你检测磁盘类型。
- options 指定一个以逗号分隔的选项列表，告诉系统如何处理设备。例如，有选项告诉系统以下内容：是否应解释文件上的某些位，是否允许用户挂载设备，设备是否应在启动时自动挂载，或设备应以读写方式还是只读方式挂载。要了解所有选项，你可以使用 kdehelp（在第 4 章“Working with Applications”中讨论）或 man 命令（第 15 章“Help Please”），并在 UNIX 手册页中搜索 fstab 和 mount。
- dump_order 指定 dump 程序转储文件系统的顺序，dump 程序用于将文件系统备份到磁带（见第 19 章 "Backups: Safeguarding Your Work"）。
- check_order 为 fsck（文件系统检查）提供信息，指定检查磁盘的顺序。如果系统被不适当关闭，下次启动系统时，你的磁盘将被检查是否有错误。此选项指定的数字告诉系统以何种顺序执行检查。有关 fsck 的更多信息，请使用 man 命令（第 15 章）。

Previous Table of Contents Next

Products | Contact Us | About Us | Privacy | Ad Info | Home

Use of this site is subject to certain Terms & Conditions. Copyright © 1996-2000 EarthWeb Inc. All rights reserved. Reproduction whole or in part in any form or medium without express written permission of EarthWeb is prohibited.





要访问内容，请单击章节和节标题。

## Linux完全傻瓜指南

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

上一页 目录 下一页

要使普通用户能够挂载 /mnt/floppy 中的软盘，您需要在软盘设备的选项列表中添加一个逗号（,）然后添加 user 选项。

要使普通用户能够使用 CD-ROM，您需要修改包含文本 /mnt/cdrom 和文件系统类型 iso9660 的条目。在我的例子中，我的 IDE CD-ROM 的条目以 /dev/hdd 开头。要允许普通用户挂载 CD-ROM 驱动器，请在 CD-ROM 设备的选项列表中添加一个逗号（,）然后添加 user 选项，如下所示：

```
/dev/hdd /mnt/cdrom auto ro,noauto,user 0 0
```

完成修改后，保存文件并退出 KEdit 和 root KFM 窗口。

## 为软盘和 CD 创建 kdelnk 文件

在您使 CD 和软盘驱动器对所有用户可访问后，您将希望通过图标轻松访问设备。这将允许您使用鼠标挂载卷，而不必使用命令行工具。

KDE 有特殊的文件，其名称具有 .kdelnk 扩展名。这些文件用于多种用途，包括将设备与图标关联。虽然创建其中一个文件有点笨拙，但如果我们使用内置于 KDE 的设备模板，则并不难做到。

要为您的软盘驱动器创建图标，首先在桌面上右键单击。在出现的弹出菜单中，选择 New，然后选择 Device。会出现一个窗口，要求为您的图标输入文件名。将默认名称 "Device.kdelnk" 替换为代表您的软盘驱动器的名称，例如 "Floppy.kdelnk"。桌面上会出现一个新图标；图标将是一个问号，表示新设备尚未配置。

要配置设备，右键单击图标并从弹出菜单中选择 Properties。这将导致 KFM 显示其用于配置 .kdelnk 文件的窗口。选择窗口顶部的 Device 选项卡以显示与挂载相关的选项。在标记为 Device 的框中，输入 /dev/fd0，但不要按 Enter。不要在 Mount Point 或 Filesystems 框中输入任何内容。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_78_0.png)

新设备图标必须在工作前进行配置。由于它尚未配置，因此显示为问号。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_78_1.png)

KFM 使用特殊窗口来配置 .kdelnk 文件。

要配置设备图标：
- 选择窗口顶部的 Device 选项卡。
- 在 Device 框中输入设备文件名。
- 选择设备挂载时的图标。
- 选择设备未挂载时的图标。

您需要为设备选择两个新图标：一个在软盘驱动器挂载时显示，另一个在未挂载时显示。要选择图标，请单击标记为 Mounted Icon 的按钮。选择看起来像旁边有一个小绿灯的软盘的图标，然后单击 Ok。现在，单击标记为 Unmounted Icon 的按钮。这次，选择看起来像旁边没有小绿灯的软盘的图标，然后单击 OK。现在，单击 KFM 窗口底部的 OK 按钮以接受您的更改。在桌面上，您应该会看到一个看起来像软盘的图标。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_78_2.png)

选择图标窗口。当您单击按钮选择图标时，KDE 会向您展示一个面板，您可以在其中选择代表设备的图标。通常每种类型有两个图标。旁边有绿色方块的图标代表活动设备。如果您分配该对，KDE 将更改图标以提供已挂载设备的视觉反馈。

要配置您的 CD-ROM 驱动器，请按照相同的步骤进行操作，但将您的图标文件命名为 **CD-ROM.kdelnk**，在 Device 框中输入 **/dev/cdrom**，并选择与个人 CD 播放器中的 CD 非常相似的图标。

要测试设备图标，请插入 CD-ROM 或软盘并单击匹配的图标。会出现一个窗口，通知您磁盘正在挂载。片刻之后，将出现一个 KFM 窗口，显示磁盘的内容，现在位于 **/mnt/floppy** 或 **/mnt/cdrom**，具体取决于您正在测试的设备。请注意，桌面上的图标旁边出现了一个小绿灯；这表示磁盘当前已挂载。

在弹出软盘或 CD 之前，您必须始终确保它已卸载，否则您可能会丢失数据。要卸载磁盘，请右键单击设备图标并选择 Unmount 命令。小绿灯现在消失，表示您的设备已卸载。现在可以安全地弹出设备。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_79_0.png)

列出 CD-ROM 磁盘上包含的文件的 KFM 窗口。图标已更改以指示设备已挂载。

## 复制文件到或从软盘

要将文件复制到软盘或从软盘复制文件，首先需要单击软盘图标以显示聚焦于设备的 KFM 窗口。然后，您可以在两个 KFM 窗口之间拖放文件。请记住，软盘的容量有限。如果您尝试复制的文件大于软盘的容量，复制过程将失败。

目前，使用图形工具无法确定磁盘上可用多少可用空间。第 22 章“系统监控：关注您的系统”中的“监控您的磁盘”部分解释了如何使用命令行确定可用空间信息。您将在本章末尾学习如何格式化软盘。

## 打开和保存文件到软盘

打开和保存文件到软盘与在目录之间保存相同。只需挂载软盘并将文件保存在 **/mnt/floppy** 目录中。确保您保存的文件适合磁盘上的可用空间。

要访问内容，请单击章节和节标题。

## Linux完全傻瓜指南

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 访问 CD-ROM

访问 CD-ROM 本质上与访问软盘相同。要访问磁盘，您必须已挂载 CD。CD-ROM 的默认挂载点为 /mnt/cdrom。如果您单击与 CD-ROM 关联的 kdelnk 文件，KFM 将打开一个聚焦于 /mnt/cdrom 的窗口，您可以在其中访问文件。

## 准备新的软盘

KDE 为您提供了一个用于格式化软盘的应用程序，kfloppy。kfloppy 可从应用程序启动器实用程序组访问（参见下图）。

该应用程序允许您选择驱动器和用于软盘的文件系统格式。请注意，kfloppy 只能在磁盘未挂载时格式化磁盘。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_81_0.png)

Kfloppy 允许您格式化软盘。

> 查看此内容：
> 当您格式化磁盘时，您会擦除磁盘包含的所有文件。在格式化之前，请确保软盘不包含您将来需要的任何文件。

KDE 软盘格式化程序在您想要准备软盘时向您提供以下选项：
- 选择软盘的大小和驱动器。
- 选择密度格式。高密度磁盘（HD）可存储 1440K 的信息。双密度磁盘（DD）可存储 720K。
- 文件系统选择为 ext2fs（Linux 原生文件系统，DOS 和 Windows 无法读取）或 DOS 格式。DOS 格式将创建可在 Windows 95/98 长文件名或旧系统上的 MS-DOS 文件名下同样工作的磁盘。
- 选择选项后，单击 format 以初始化磁盘。
- 快速擦除不会执行低级格式化，它只是在磁盘上创建新的文件系统。
- 完全格式化对软盘执行低级格式化并在其上创建新的文件系统。
- 单击以退出应用程序。





要访问内容，请点击章节和节标题。

## Linux完全傻瓜指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 第8章
访问网络

## 本章内容

- 连接到网络
- 配置新的拨号账户
- 设置调制解调器

如今，一台无法访问网络或互联网的计算机毫无意义。Linux 提供的网络服务和网络可靠性比许多其他操作系统都要多。个人电脑今天所拥有的许多网络技术很大程度上都归功于 UNIX。有了 Linux，你不仅能够作为客户端访问网络服务，还能作为服务器提供这些服务。互联网上许多 Web 服务器都在 Linux 下运行，这得益于其可靠性和灵活性。

本章介绍如何使用 Linux 连接到互联网的基础知识。

你如何将计算机连接到网络取决于你拥有的硬件。如果你的计算机已参与网络并且可以通过网络直接访问互联网，你只需要一块以太网卡即可。如果你在安装 Linux 之前就安装了该卡，安装程序会配置该卡以便你使用。你可能需要做的唯一事情是配置你的名称服务，以便你的计算机知道如何访问域名系统（DNS；本章后面“配置 DNS 服务器”部分会详细介绍）。如果你在添加网络卡之前就安装了 Linux，你将不得不使用 lisa 来更改硬件配置（有关如何使用 lisa 的提示，请参阅第 21 章“ LISA—Linux 安装和系统管理实用程序”）。

如果你的计算机没有直接访问互联网，你需要使用调制解调器并与互联网服务提供商（ISP）建立点对点协议（PPP）连接。ISP 以适中的月费提供到互联网的连接服务。当你连接到 ISP 时，你的计算机将“上网”，你就可以使用 http（www）、ftp、news 等网络服务。

### 使用拨号（PPP）连接连接到网络

Linux 包含 PPP 和其他协议，可用于连接到互联网和私有网络。PPP 是目前 ISP 支持的最流行的拨号网络协议。通常，在 UNIX 下设置 PPP 对新手来说是一项艰巨的任务。幸运的是，KDE 提供了一个图形工具 kppp，你可以用它轻松配置拨号连接。

在你能够连接之前，你需要知道 ISP 的连接详细信息，例如拨号号码、登录名、密码、网关和 DNS 服务器 IP 地址。

### 使用 Kppp 添加互联网连接

在使用 kppp 配置 PPP 连接之前，你需要编辑 /etc/ppp/options 文件。默认情况下，此文件可能包含带有 lock 选项的行。此选项用于 PPP 软件管理对连接和硬件的锁定。kppp 本身就会执行此操作，因此你需要删除此选项。要编辑 /etc/ppp/options 文件，你需要具有超级用户（root）权限。为此，你可以注销系统并以 root 身份登录，或按照第 7 章“使用磁盘”中概述的“启动超级用户 KFM 会话”程序进行操作。

你可能需要对文件进行的唯一更改是注释掉 lock 选项（/etc/ppp/options 文件默认的唯一选项）。要注释掉某行，请在该行的第一字母前加上井号或哈希符号（#）。编辑后的文件应如下所示：

```
#lock
```

井号告诉 PPP 忽略该行的其余部分。保存文件并退出任何超级用户 KFM 窗口和 KEdit 会话。如果你选择以 root 身份登录，你应该再次使用自己的账户登录。现在你已准备好开始配置到 ISP 的 PPP 连接。

要启动 kppp，你可以进入应用程序启动菜单并在 Internet 程序组下选择 kppp。选择 kppp 后，你会看到下一幅图所显示的对话框。

如果已定义连接，你可以选择它，提供 PPP 账户的登录名和密码，然后单击 Connect 拨号。默认情况下，不会为你设置任何可用的连接，因此你必须定义一个。你可以通过单击 Setup 按钮来完成。这将为你呈现一个如以下图所示的窗口。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_85_0.png)

kppp 可以从应用程序启动菜单下的 Internet 程序组启动。

### Techno Talk：迷你命令行

KDE 桌面为你提供了一种无需使用 shell 即可输入命令的简便方法。迷你命令行是一个小型面板，你可以在其中输入命令、程序名称，甚至是文件路径以启动新的 KFM 窗口。输入命令并按 Enter 后，minicli（该程序的名称）将消失并执行你的命令。

要访问 minicli 窗口，请在键盘上按 Alt+F2。在显示的小面板上，输入你想要访问的命令或程序的名称。例如，输入 kppp 以启动该程序。

Minicli 还可以打开 KFM 窗口。要打开聚焦到目录的 KFM 窗口，请在 minicli 面板中输入该目录的路径并按 Enter。如果指定的是文件名而不是目录，则将打开为该文件类型注册的应用程序（在许多情况下，这将是 KDE 编辑器 KEdit）。

要阅读 man 文档页面，请输入 man:programname，其中 programname 是你想要了解的工具或命令的名称。有关使用 man 的更多信息，请参阅第 15 章“Help Please”。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_85_1.png)

kppp 窗口。Connect to 菜单允许你选择要连接的 ISP。Login ID 和 Password 对应于 ISP 分配给你的信息。Show Log Window 框对于调试连接很有用，因为你可以实时查看连接的详细信息。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_85_2.png)

kppp 配置窗口是配置 ISP 设置的地方。

Products | Contact Us | About Us | Privacy | Ad Info | Home

使用本网站须遵守特定条款和条件。版权所有 © 1996-2000 EarthWeb Inc。
保留所有权利。未经 EarthWeb 明确书面许可，不得以任何形式或媒介全部或部分复制。

要访问内容，请点击章节和节标题。

## Linux完全傻瓜指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

这是管理当前账户并添加新账户的地方。此窗口的其他功能包括：

- Accounts 选项卡—显示所有当前定义的条目。
- Device 选项卡—单击以设置调制解调器连接的设备。
- Modem 选项卡—单击以设置特殊调制解调器选项。
- PPP 选项卡—单击以设置 kppp 的一些选项。
- About 选项卡—单击以了解有关 kppp 的更多信息。
- 条目列表—选择一个条目并单击 Edit 以编辑它。
- Edit 按钮—单击以编辑当前选中的条目。
- New 按钮—单击以定义新账户。
- Copy 按钮—单击以复制现有条目。
- Delete 按钮—单击以删除选中的条目。
- Phone Costs、Reset Costs 按钮和 View Logs 按钮—允许你跟踪在线花费的时间。如果你的连接按分钟计费，这对于跟踪你的费用非常有用。

当你单击 New 按钮时，新账户窗口会出现，如下图所示。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_87_0.png)

拨号配置提供多个面板来设置拨号信息、机器的 IP 地址和 DNS 服务器设置等。

## 添加新的拨号配置

创建账户时，你需要定义几件事。首先你需要通过新账户窗口中的 Dial 选项卡配置拨号设置。此窗口要求你为 ISP 提供一个名称。此名称由 Connect to 菜单显示。你需要提供的其他信息是 ISP 调制解调器组的电话号码。Authentication 菜单选择如何连接到 ISP。如果你的 ISP 支持从 Windows 95/98/NT 的连接，很可能 PAP 认证是你所需要的。其他认证方法在该方法不起作用时可用，但它们要求你创建一个小的“chat”脚本。我将在后面“使用登录脚本”部分向你展示如何创建一个。

## 配置 IP 设置

接下来你需要为连接定义 IP 地址设置。特殊网络设备，称为路由器，负责在网络之间传递数据包。大多数 ISP 动态分配 IP 地址。当你的计算机连接到 ISP 时，它将被分配一个在会话持续时间内使用的 IP 地址。下次连接时，你会得到一个不同的号码。

PPP 协议可以处理动态分配的 IP 地址。面板中的 IP 选项卡允许你指定 kppp 应使用的设置，如下一图所示。

> **Techno Talk：那么所有这些 IP 东西到底是什么？**
> 
> 互联网是由网络组成的网络，由少数协议将其联系在一起，这些协议定义了信息如何在计算机之间路由和发送。计算机之间发送的信息被分解成许多小块（称为数据包或数据报）。
> 
> *数据包*类似于你通过邮局发送的邮件。每个数据包包含几条信息，包括应交付到的计算机的地址、发送消息的计算机的地址以及实际信息、文本、图像的位等。
> 
> 当你连接到互联网时，你就成为这个庞大网络的一部分。你的计算机被唯一标识（好吧，如果你不在防火墙后面），允许你和其他网络上的计算机相互通信。
> 
> 当你听到人们谈论 IP 时，他们实际上是在谈论 IP 地址。实际上，IP 代表 Internet Protocol，其功能是封装其他协议，以便它们可以使用网络传递到正确的计算机。IP 提供了一个信封，其中包含将数据包从一台计算机传递到另一台计算机所需的必要信息。因此，为了在互联网上联网，你需要某种方式唯一标识你的计算机。这就是为什么你需要 IP 地址。
> 
> 尽管 IP 提供了发送数据的信息，但它并不能说明计算机如何交换这些信息。运行在 IP 之上的其他协议负责此事。互联网上计算机之间的数据传输通常使用两种主要协议之一：TCP 或 UDP。





![](img/edf072a03d4de1f8f4a13465ac79e7fb_89_0.png)

新账户窗口的 IP 选项卡。

## 技术谈：好吧，聪明人，TCP、UDP 和 PPP 到底是什么？

TCP 代表传输控制协议。TCP 使用 IP 在计算机之间传递信息数据包。它是一种连接协议；计算机在发送信息之前会先相互连接。主要优点是该连接协议保证你发送的数据包会被送达，并且接收计算机能按正确顺序重新组装数据包。这是因为信息被拆分成许多小数据包。每个数据包都有一个序列号，表示其在数据流中的位置。

UDP 代表用户数据报协议。UDP 是一种无连接协议。它是一种最小化协议，速度非常快。唯一的问题是 UDP 不保证数据能到达目的地。通常，UDP 用于在计算机之间发送非常短的消息，其中建立 TCP 连接的时间成本远超需求。大多数通过 UDP 发送的信息只使用一个数据包发送。

PPP 是通过串行线路进行 IP 网络的一种机制。还有其他串行线路协议，例如 SLIP（串行线路互联网协议），但 PPP 部分是因为其灵活性而确立了主导地位，无需固定 IP 地址。PPP 连接通常在你连接到 ISP 时协商 IP 地址。

如果你的 ISP 动态分配 IP，请勾选动态 IP 地址按钮。如果你有一个专用 IP 地址（静态地址），请在静态 IP 地址部分输入该地址和子网掩码。如果你希望 kppp 在临时设置计算机的域名和主机名以匹配 ISP 分配的地址时，请点击从此 IP 自动配置主机名。

上一页 | 目录 | 下一页

要访问内容，请点击章节和节标题。

## Linux 完全 idiot's Guide

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 配置调制解调器设备

在配置好账户后，你需要将调制解调器设备标识给 kppp。你需要查看在 Windows 下调制解调器使用的 COM 端口的原始笔记。作为替代方案，你也可以尝试四种 COM 设置直到能正常工作。为了启用将调制解调器用作 /dev/modem，你需要使用 lisa（参见第 21 章）或简单地从 /dev/ttySx 创建到 /dev/modem 的链接（参见第 12 章，“在 Shell 上操作文件”）。

调制解调器设备位于 /dev/ttySx，其中 x 是 0 到 3 之间的数字。各种 /dev/ttySx 设备映射到各种 COM 端口。表 8.1 显示了它们的列表。

### 表 8.1 设备到 COM 端口映射

| 调制解调器设备 | COM 端口 |
|---|---|
| /dev/ttyS0 | COM1 |
| /dev/ttyS1 | COM2 |
| /dev/ttyS2 | COM3 |
| /dev/ttyS3 | COM4 |

![](img/edf072a03d4de1f8f4a13465ac79e7fb_91_0.png)

使用 kppp 面板设置调制解调器设备。

要配置你的调制解调器设备，必须设置以下选项。

- 调制解调器设备—选择代表你的设备的设备；参见表 8.1。
- 流量控制—选择 CRTSCTS 以启用硬件流量控制。
- 行终止—选择 CR/LF 行终止。
- 连接速度—选择适合你调制解调器的速度。使用 14.4 kbps 调制解调器的用户应选择 57600 bps。拥有更快调制解调器的用户应选择 115200 bps。如果你的调制解调器在你选择的速度下出现问题，你可以稍后降低它。
- 调制解调器锁文件—指定锁文件放置的位置；保持原样。如果尝试启动另一个连接并且找到此文件，kppp 将检查拥有该文件的进程是否存在。如果存在，它会告诉你调制解调器正忙。
- 调制解调器超时—指定放弃等待的时间。保持 60 秒默认值。

## 调试连接

如果你已进行到这里，你的配置应该已准备好进行测试。点击 kppp 配置窗口底部的确定以接受你的配置更改。在 kppp 窗口中，选择你的服务提供商，并勾选显示日志窗口选项。这将显示一个窗口，显示你从 ISP 接收的信息以及你的计算机或脚本发送的信息。此工具对于查看登录脚本中的问题点非常宝贵（参见接下来的两个图）。

大多数 ISP 使用 PAP，因为这是 Windows 驱动机器的默认身份验证方案。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_91_1.png)

测试连接。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_91_2.png)

调试窗口显示调制解调器发送和接收的信息。

## 通过本地网络连接

如果互联网接入就在网络线另一端，并且你的硬件在安装时已正确配置，你的网卡应该已经可以运行。你需要添加的唯一信息是关于你的 DNS 服务器的信息。DNS 服务器将 www.netscape.com 等机器名映射到 207.200.73.73 等 IP 地址。没有 DNS 服务器条目，你访问网络计算机的唯一方法是知道其 IP！

通过本地网络连接到互联网不使用前面章节中讨论的 PPP。

要搜索 DNS 服务器，你需要编辑名为 /etc/resolv.conf 的文件。正如你所料，此文件应在具有超级用户权限（root）的情况下编辑。或者你也可以使用 lisa。（参见第 24 章以定义这些网络设置。有时直接编辑文件更简单更快。）

在此文件中，你将指定由网络管理员提供的名称服务器的 IP 地址。我的 /etc/resolv.conf 看起来像这样：

```
domain execpc.com
nameserver 165.207.1.3
nameserver 204.29.202.6
```

关键字 domain 指定你的网络的域名。nameserver 关键字指定在将名称解析为其 IP 时要搜索的 DNS 服务器的 IP 地址。

编辑文件后，只要你的网络硬件在安装时已正确配置，你应该能够使用任何程序访问网络。如果没有，你将不得不使用 lisa—（参见第 21 章）来配置你的网卡和路由器（网关）信息。

上一页 目录 下一页

要访问内容，请点击章节和节标题。

## Linux 完全 idiot's Guide

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 第 9 章
通信：Web、FTP、电子邮件和新闻

## 本章内容

- 访问万维网
- 使用 FTP 传输文件
- 发送和接收电子邮件
- 参与新闻组

## 访问网络

现在你的连接已设置好，你可以访问网络。Caldera 的 OpenLinux 预装了 Netscape Communicator。Netscape Communicator 拥有你阅读新闻和电子邮件（Messenger）、访问网络（Navigator）、参与讨论（新闻）组（Collabra）所需的所有工具，甚至可以开发自己的 HTML 网络页面。

在 KDE 中，KFM（文件查看器）也是网络感知的。KFM 提供了一个基本浏览器，能够访问简单的网站。对于快速粗略的网络冲浪，KDE 可能已足够你需要。对于更广泛的冲浪，Navigator 提供了更多功能和能力，这些功能被更流行的网站使用。其中一些功能使查看网站成为更具交互性的体验。Netscape 还充分利用了 Linux 提供的强大网络能力和多任务处理。网站似乎比在 Windows 或 Macintosh 等其他平台上下载和显示得更快（参见下图）。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_94_0.png)

KFM 对 www.yahoo.com 网站的描绘。

要使用 KDE 访问网络，请连接到你的 ISP 并在 KFM 浏览器的位置字段中输入任何网络地址。KFM 将按适当方式渲染该页面。要移动到不同页面或网站的不同部分，请点击链接。链接通常显示为带下划线的文本甚至是图像。链接是进入另一页的入口点（超文本引用），提供额外信息。链接可以是本地网站，也可以是不同网站的一部分。链接使网络成为网络。

并非所有浏览器都以相同方式渲染信息。请注意 KFM（在前一图中）和 Netscape 渲染页面的差异（在下图中）。更好的网站利用了 Netscape 和 Internet Explorer 上的功能。要获得这些增强页面，你必须使用 Netscape Navigator。（Internet Explorer 尚未适用于 Linux，尽管一些 UNIX 端口开始出现。）

标准浏览器窗口的功能包括：

- 位置栏—输入 URL 并按 Enter 前往该站点。
- 后退和前进按钮—后退按钮使你能够返回到之前访问的页面。如果你后退，前进按钮允许你返回到上次所在的位置。
- 主页按钮—默认情况下带你到 www.netscape.com，但你可以使用编辑菜单中的首选项命令更改此操作的 Navigator 首选项。
- 书签图标—使你能够将当前页面的地址拖到书签区域（位置栏正下方的区域），以便轻松返回此页面。
- 书签区域—书签站点可从这些图标获得。
- 状态区域—显示消息和鼠标悬停的链接地址。
- 链接—图像或带下划线的文本可以代表到另一页的链接。点击链接前往该页面。
- 搜索按钮—带你到各种搜索引擎，你可以使用它们查找你感兴趣的信息。
- Navigator 图标—点击以打开新的 Navigator（浏览器）窗口。
- Messenger 图标—点击以访问 Netscape Communicator 的电子邮件组件 Messenger。
- Collabra 图标—点击以使用 Collabra 组件打开讨论组（新闻组）列表。





- Composer 图标—点击打开文本编辑器
dlike application you can use for designing your own Web pages.

要使用 Netscape 访问 Web，请调用一个 minicli 窗口（参见第 8 章“访问网络”中的“Mini Command Line”）并输入 `netscape`。你也可以从应用程序开始菜单下的 Applications 中访问 Netscape Communicator。几秒钟后，你会看到 Netscape 的一些面板，告诉你它正在为你创建配置文件以及放置缓存文件的位置。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_95_0.png)

Netscape 对 www.yahoo.com 网站的描绘。请注意信息的呈现方式与前一图不同。

Previous Table of Contents Next

## SPIDER KILLER

## spider catcher

- HOME
- ACCOUNT INFO
- SUBSCRIBE
- LOGIN
- SEARCH
- MY ITKNOWLEDGE
- FAQ
- SITEMAP
- CONTACT US

## SEARCH ITKNOWLEDGE

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Bookmark it

Search this book:

- Previous
- Table of Contents
- Next

## FTP

FTP (File Transfer Protocol) is a protocol used to move files between computers. FTP under KDE is very simple: To go to a site, just enter an FTP URL in the location bar of a KFM window, like this:

```
ftp://somehost.somedomain.com
```

Somehost.somedomain.com is the fully qualified name of the machine you want to connect to. If that machine supports anonymous FTP, connections for which you don’t need a login and password, KFM will display the contents available at that location. To navigate, use KFM as if it was your local hard disk. You can copy files between your local machine and the server or from the server to your local machine by dragging and dropping files between KFM windows (see the next figure).

![](img/edf072a03d4de1f8f4a13465ac79e7fb_96_0.png)

To FTP a file using KFM, type the URL for the FTP site and browse for the file you want. Then click and drag the file to your desktop or to another KFM window focused to your local computer.

Because some files you transfer will be large, the speed of the copy will be much slower than you normally experience. But don’t despair— the file will be transmitted across the wire.

## BROWSE BY TOPIC

If the server doesn’t allow anonymous connections, you’ll need to specify your login name, like this:

ftp://user@somehost.somedomain.com

user is your user name, followed by an at symbol (@), then followed by the fully qualified name of the machine. When you enter FTP URLs like this, more advanced programs raise a panel that asks you for your password.

You can also enter your password right in the URL; however, I don’t recommend that you do this, as the password might be displayed for other people to see in the URL. KFM removes the password from the URL when you have connected. To supply your password on the URL, enter it like this:

ftp://user:password@somehost.somedomain.com

The username and password are separated by a colon (:), like this:

ftp://me:mypassword@ftp.netscape.com

The same technique for accessing files using FTP can be used with a browser such as Netscape Navigator. To access the site, enter the URL, and you are delivered. Instead of clicking and dragging to move files across the network, just right-click on the link and choose the Save Link As command from the context-sensitive menu that is displayed. Use the Save panel that is displayed to navigate your way to the location where you want to save the file.

## Email

KDE provides an email program called kmail that you can use to read and write email messages. Although this program gets the job done, I am a little partial toward Netscape Messenger, as it provides more features than kmail. One nice feature of kmail over Netscape Messenger, however, is that kmail can manage multiple email accounts for you. Netscape allows you to set up multiple remote IMAP mailboxes but only a single POP mail account. Most users have several POP mailboxes. IMAP, though more powerful and useful to power users, is not as popular between ISPs. I also like having a spell-checker accessible right from the application, as Netscape Messenger offers. At the time of this writing, kmail doesn’t allow me to spell-check my messages. In this section, you will learn how to set up Netscape Messenger to handle your email.

Techno Talk: POP and IMAP? What’s that?

IMAP and POP are two different protocols used to access your email.

IMAP stands for Interactive Message Access Protocol. It allows you to manipulate and organize a remote mailbox as if it were local to your computer—and it does it without the need to transfer your entire mailbox to your computer. This is cool because your mailbox is then centralized on the network. No matter what computer you use and where you are, your entire mailbox is accessible. Many ISPs don’t like giving IMAP mailboxes, because users tend to collect copious amounts of email. For example, yours truly has an 80MB mailbox—yeah, there are things I should delete. But then again, disk space is cheap.

POP, which stands for Post Office Protocol, is a much simpler interface to

your mailbox. It doesn’t allow you to organize your inbox in any way, but it allows you to download your messages to a local mailbox for reading.

The process of setting up your email reader is very similar for most email applications. You will need to know the following:

- Your email address
- The type of email account that you have (IMAP or POP)
- The username and password needed to access your account
- The name of the machine where your incoming mail is stored
- The name for the SMTP (outgoing) mail server

Previous Table of Contents Next

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Configuring Your Identity for Netscape Messenger

In the identity panel, you provide information that will be included in your email, such as your “real” name and your email address (see following figure).

![](img/edf072a03d4de1f8f4a13465ac79e7fb_99_0.png)

Identity panel in Netscape Preferences.

## Configuring Your Mail Server

The next step in configuring your email program is to configure your mail servers so that Messenger can receive and send your email (see the following figure). Information to be entered here includes:

- Name of your email account (don’t put a domain name on it).
- Name of mail server that sends your mail (SMTP).
- Name of mail server that stores email sent to you.
- Type of mail server. If it’s a POP account, check whether if you want to leave incoming messages on the server (Otherwise messages are deleted from your ISP’s server after they are downloaded. If it’s an IMAP server, your mailboxes are kept on the server.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_100_0.png)

Messenger’s Mail Server Configuration panel stores information about sending and receiving your email.

## Reading Email

After configuring your identity and mail server settings, Messenger is ready to send and receive email. To start a Messenger session, choose the Messenger Mailbox command under the Communicator menu in a Navigator window. Messenger displays four main areas (from top to bottom):

- Menus and buttons—Access to commands and functions
- Mailboxes—Access to separate mailboxes
- Mailbox contents
- Message body

See the following figure for a description of the most important buttons and areas.

Different buttons in the Messenger window include:

- Get Msg—Click to download new messages.
- New Msg—Click to compose a new message.
- Reply—Click to reply to sender of the current message.
- Forward—Click to send a copy of the current message to another person.
- Delete—Click to delete the message from your mailbox.

You can also organize your messages into different boxes. To select a different message box, click the Inbox menu.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_100_1.png)

The Netscape Messenger window.

## Composing an Email Message

Sending email is just as easy as reading email. To send a message, click the New Msg button (see the previous figure). This will present you with a window where you can compose and address an email message like the one shown in the following figure. When done composing a message, click Send Now to forward your email message to your mail server for delivery.





![](img/edf072a03d4de1f8f4a13465ac79e7fb_101_0.png)

Messenger 的撰写窗口——在这里输入新的电子邮件信息。

Kmail 在界面上与 Netscape 的 Messenger 组件非常相似。然而，目前 Messenger 是一款更精致的产品，工具和功能更好。

## 新闻

如果你有时间在 Usenet 上闲逛，无疑会找到很多有用和无用的东西。如果你想冲浪，你需要一个像样的新闻阅读器。同样，你的选择有几种：在 KDE 下你有 knews，在任何 X-Windows 下，包括 KDE，你有 Netscape 的 Collabra。

> Techno Talk：什么是 Usenet？
> Usenet 是一个全球分布式讨论系统。它由按主题分类的主题层级组成（新闻组）。信息在新闻服务器之间广播和传播。一些组是经过审核的，这意味着用户发布的信息需要在发布前得到批准。其他组则未经过审核。
> 
> 有关 Usenet 是什么以及不是什么的详细描述，请参阅 http://www.cis.ohio-state.edu/hypertext/faq/usenet/usenet/what-is/part1/faq.html

Collabra 对电子邮件和新闻的区别不大。虽然访问它们的配置不同，但结果相似。你使用 Collabra 订阅你感兴趣的新闻组，然后使用 Messenger 阅读和发布信息。但是，在阅读新闻之前，你需要先下载一份可用的信息列表。当你点击其中一个时，该信息将被下载，你就可以查看它。如果你想发布信息，你基本上像撰写电子邮件一样撰写，但它会被发布到新闻服务器。从那里，信息会在全球范围内传播。

将你的系统配置为使用新闻很简单：你连接到一个新闻服务器（nntp 服务器；该机器的名称由你的 ISP 提供），并从该服务器下载一份非常长且很大的可用新闻组列表。（有成千上万个不同的组。）然后你选择所有感兴趣的组并开始阅读（见接下来的三个图）。作为 sanity check，你可能想为每天做这件事分配一定的时间。很容易沉迷于阅读新闻而没有意识到几个小时已经过去了。作为选择，我倾向于除非在搜索特定信息时，否则不查看新闻组。几年前，我曾经花费比任何人份额都多的时间阅读新闻。今天我尽量远离；很容易被噪音淹没。

如果你的 ISP 在特殊端口下提供新闻服务，请在 Port 空间中输入；否则保留默认的 119。组织也使用新闻来分发信息。其中一些新闻组只能通过需要身份验证的安全服务器访问：如果你的新闻服务器需要此功能，请在 Port 空间旁边的 Secure 复选框中进行勾选。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_102_0.png)

新闻配置面板。要配置你的新闻，请在 Communicator 的任何窗口中使用 Edit 菜单下的 Preferences 命令。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_102_1.png)

在你定义新闻服务器后，你将看到此窗口。在这里，你可以从你的新闻服务器提供的组中选择要加入的组。

如果你知道感兴趣的新闻组名称，请在 Discussion Group 旁输入并点击 Join。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_102_2.png)

Messenger 显示的新闻组列表。

使用 Reply 按钮回复帖子。如果你按住它，会出现一个菜单，允许你选择回复方式：回复到组、回复给发帖人，或两者兼顾。加粗列出的帖子表示尚未阅读。

## Telnet

Telnet 是与 Internet 上另一台计算机交互的另一种方式。它是一个仅限命令行程序，允许你通过命令行界面访问远程类 UNIX 计算机。Telnet 在第 17 章“Command Toolbox: Useful Shell Commands and Shortcuts”中讨论。

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 第 10 章
自定义 KDE

## 本章内容

- 将应用程序添加到面板或应用程序启动器
- 其他 KDE 选项
- KDE 控制中心

KDE 具有相当高的可定制性；以下是你可以自定义桌面的快速指南。KDE 大部分是通过使用 kdelnk 文件进行自定义的（文件扩展名为 kdelnk）。这些文件提供 KDE 用于将文件与应用程序关联、将图标与应用程序和文档关联、将磁盘驱动器等设备与图标关联（见第 7 章“Working with Disks”）等配置信息。

KDE 面板可以通过多种方式进行自定义。以下各节介绍了其中一些最有用的方法。

## 将应用程序添加到面板或应用程序启动器

将应用程序添加到面板是一个简单的两步过程。首先，你需要创建一个提供有关要添加应用程序信息的 kdelnk 文件。该文件将可执行程序与图标及其文件关联。然后你通过将其拖入面板或将其放在应用程序启动器会找到的特殊目录中来安装 kdelnk 文件。

### 创建代表应用程序的 Kdelnk 文件

为应用程序创建 .kdelnk 文件很容易。该过程与我们在第 7 章“Working with Disks”中为软盘和 CD-ROM 驱动器创建 .kdelnk 文件的过程非常相似。右键单击桌面上的空白区域。当弹出菜单出现时，选择 New 然后 Program。会出现一个窗口，要求你为此 kdelnk 文件提供名称。将名称从默认的“Program.kdelnk”更改为代表你的程序的名称，例如“Netscape.kdelnk”。一个看起来像齿轮的图标出现在你的桌面上。

创建图标后，右键单击它并选择 Properties 命令。这将为你呈现一个面板，如下图所示。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_104_0.png)

此窗口控制 kdelnk 文件的属性。

点击 Execute 选项卡以更改将图标与实际程序关联的设置。Execute 面板看起来像下一个图中的那样。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_104_1.png)

执行选项卡允许你将程序与 kdelnk 文件关联。

如果你知道程序文件的位置，只需将其输入 Execute 字段即可。例如，Netscape 程序的路径是 /opt/netscape/communicator/netscape。如果你不知道确切路径，你也可以使用 Browse 按钮手动查找文件。

一些程序使用特殊目录作为其工作目录，在那里保存文件。当程序这样做时，它们会常规地在该工作目录中查找与程序关联的文件。这样的程序需要填写 Working directory 字段。

Swallowing on 面板选项适用于运行后成为面板上小图标的应用程序，如 CD 播放器。Run in terminal 按钮适用于你想为其提供图标的命令行程序。

要将图标与文件关联，请点击包含齿轮图标的按钮。这将打开一个面板，你可以用它为你的程序选择图标（见下图）。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_105_0.png)

使用 Select icon 面板为你的程序关联图标。

Select icon 面板有一个弹出菜单，你可以用它在 KDE 的图标区域 /opt/kde/share/icons 或你的主目录中的 kde/share/icons 目录中找到图标。请注意，此目录通常不可见，因为它以句点开头；要在 KFM 窗口中显示它，请在 View 菜单中激活 Show Dot Files 选项。点击你喜欢的图标，然后点击 OK。（Netscape 的图标看起来像船舵。）

> **Check This Out:**
> 你可以使用 Paint 应用程序添加自己的图标。图标使用 XPM 格式保存，大小为 32 像素宽乘 32 像素高。如果你将它们存储在主目录中的 kde/share/icons 目录中，你将能够将它们关联起来。

配置 kdelnk 文件的最后一步是将文件类型和程序名称与 kdelnk 文件关联。这将允许 KFM 在你浏览文件系统时将图标与程序关联（见下图）。

要将你的图标与实际程序关联，请在 Binary Pattern 字段中输入程序名称后跟分号（;）。KDE 将使用此名称在你浏览文件系统时显示图标。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_105_1.png)

Application 选项卡将文件类型和图标与程序关联。注释区域在将光标悬停在图标上时显示为 ToolTip。

注释字段在将鼠标悬停在显示此图标的项目上时显示为 ToolTip。

应用程序名称是程序在你语言中的名称。如果你手动编辑此 .kdelnk 文件，你将能够为应用程序名称提供多种翻译。

底部两个列表是特殊的。左侧列表代表应用程序能够打开的 MIME（Multimedia Internet Mail Extensions）类型。MIME 类型有时很难确定，但在 Netscape 的情况下，你需要关联 text/html 类型。要消除



associations that don’t match, select them from the left list and click the arrow pointing right (->). To add an association from the list, select the type you want and click the arrow pointing left (<-).

When you are done with your selections, click OK to save and dismiss the panel. The icon will change from a gear to the icon you selected for this program. The next step will make it visible to KFM.

Previous Table of Contents Next

To access the contents, click the chapter and section titles.

## 完全傻瓜Linux指南

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

## 将应用程序与 KFM 和应用程序启动器关联

要使 KFM 使用 kdelnk 文件，需要将其放置在特殊目录中。此目录会根据您是希望使关联对系统范围有效还是仅对个人工作区有效而有所不同。

要将文件安装到个人工作区，请将其移动到主目录中的 `.kde/share/applnk` 目录或其子目录之一。注销后重新登录，您在浏览 `/opt/netscape/communicator/netscape` 时将能够看到正确的图标。此操作还具有将项目添加到个人应用程序菜单的效果。

要使关联对系统中的所有用户生效，请将链接文件放置在 `/opt/kde/share/applnk` 目录或其子目录之一中。请注意，您必须以超级用户（root）身份执行此操作。这也具有将应用程序添加到应用程序启动器菜单的效果。请确保您添加的文件权限模式设置为 644（root 可读写，组和其他用户可读）。请参阅第 16 章“Permissions: Protecting and Sharing Your Work.” 中的“Changing File Permissions”。

## 面板管理：添加和删除应用程序

要将应用程序添加到面板（屏幕底部的图标栏），将上一节中创建的 kdelnk 文件拖到面板上。将显示一个按钮，您可以单击它来启动应用程序。

要删除应用程序，只需在其面板按钮上右键单击并选择 Remove 即可。

## 其他 KDE 选项

KDE 允许您配置与面板和任务栏相关的其他设置。要配置这些设置，请在空白区域右键单击面板并选择 Configure。您也可以使用应用程序启动器中面板菜单中的 Configure 命令。各种选项包含在三个选项卡中（见接下来的两幅图）：

- Panel 提供面板的位置和外观配置设置
- Options 提供用于配置菜单 ToolTips、Clock 和面板及任务栏的自动隐藏设置的设置
- Desktop 提供用于控制虚拟桌面数量的选项（见第 4 章，“Working with Applications”）

![](img/edf072a03d4de1f8f4a13465ac79e7fb_108_0.png)

KPanel Configuration 面板允许您自定义面板和任务栏的位置、行为和外观。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_108_1.png)

Options 选项卡允许您配置设置，例如 ToolTips（信息标签，告诉您按钮或图标的作用）的显示。您还可以自定义面板和任务栏是否自动隐藏以及时钟是否显示。Personal First 按钮控制应用程序启动器中菜单的顺序。个人菜单具有球体图标。

## KDE 控制中心

KDE 控制中心提供了一个统一的位置来更改与 KDE 相关的许多设置。在这里您可以自定义颜色设置、语言偏好、屏幕保护程序、字体等。此外，您还可以微调一些硬件设置，例如鼠标加速和键盘重复设置。

KDE 控制中心可从应用程序启动器访问，并为您提供机会根据自己的偏好自定义系统。以下是 KDE 控制中心的外观：

![](img/edf072a03d4de1f8f4a13465ac79e7fb_109_0.png)

KDE 控制中心提供对许多可个性化设置的集中访问。

> **Check This Out: What else can you do with KDE?**
> Well, let’s say you aren’t comfy-cozy with English. Guess what—KDE can be customized to the language of your choice! At last count, KDE supported about 25 different languages.

随着 KDE 环境的成熟，您可以预期 KDE 控制中心将提供更多设置。

本章结束了对 KDE 环境的巡览。在第 2 部分“Working on the Command Line”中，您将学习通过 UNIX shell 使用 Linux。虽然 UNIX shell 不像 KDE 那样直观或性感，但它确实非常强大。shell 的另一个巨大优势是它在所有 UNIX 实现中都可用。因此，您在下一节中学到的内容将适用于您可能在其他版本的 UNIX 中从事的工作。

Previous Table of Contents Next

To access the contents, click the chapter and section titles.

Complete Idiot's Guide to Linux
(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

## Part 2
Working on the Command Line

Now that wasn’t so bad was it? As you saw in Part 1, KDE helps make using Linux a breeze. But maybe you’re thinking to yourself, “What did users do before KDE?” or “What if I’m just a rebel and I want to see the nuts and bolts of Linux?” We’ve got you covered! Part 2 shows you Linux features without the glitz of KDE—you get to try your hand at working on the command line. The chapters in this section talk about consoles, getting help, and shells (sorry, not the kind you find on the beach—it’s not that kind of adventure). We even take a peek in the command toolbox at some useful shell commands and shortcuts. Well, if you’re ready, the command line awaits!

## Chapter 11
Shells and Consoles

## In This Chapter

- Introduction to the UNIX shell
- Basic shell navigation commands

Throughout the previous chapters I have focused on using Linux by using a graphical user interface (GUI or UI for short). If you use your computer as a workstation, that is how you’ll use it most of the time. However, that is only half the story. Although KDE’s ergonomics are nice, they are not yet as

polished as the graphical environment available to Windows or Macintosh users; but it is an excellent start.

At this point, you know how to work under Linux using KDE. And while the tour was not really technologically driven, I hope you feel confident enough to do quite a few things without the command line.

In this section of the book, I will tell you how to work on Linux (and UNIX!) using a command line. No matter how much you want to stay away from the command line, the truth is that this evil interface is actually quite powerful, and in certain ways it is indispensable. (Of course, the shell’s interface isn’t really evil; it just isn’t as intuitive as a graphical environment such as KDE.) When you learn how to use a shell, you will have a powerful tool in your bag of tricks. Let’s get our hands dirty for the first time using a shell.

## The UNIX Command Prompt

The UNIX command prompt, or *shell*, as it’s also called, provides you with direct access to the operating system. It is a command interpreter: It interprets and executes all of your commands. The shell is really just another program that sits between your keyboard, the operating system, and other programs. Unlike DOS, the shell is a separate program from the operating system, or kernel.

Though powerful, shells are lacking in the ergonomics department: They just don’t provide a friendly and intuitive GUI. And no matter how ergonomic the shell, the fact remains it is a shell, and it wants you to type in commands.

Yes, shells are by nature arcane and typing intensive, but they also are powerful. Shells provide many options unavailable to GUI-only systems. When you learn how to use a shell, you won’t be able to do without one! Granted, most things are easier to do with a GUI application, but many other things are not. The shell is then the right interface for certain kinds of problems.

If you are accessing an UNIX box remotely, you will more than likely do so through a shell interface. Shells come in different flavors and knowing how to use a shell is a good thing. It is a wise person who is familiar with at least two different shells. It will be of tremendous help if you ever have shell access to a system that doesn’t sport your favorite shell.

Most shells in UNIX are programmable, so if you find yourself writing the same commands over and over, it is easy to create a shell program (similar to a `.bat` file in DOS and Windows) that automates those commands for you. But you can worry about this when the time comes.

Shells are accessible through a terminal program. In KDE, there’s an application that provides you with shell access from within the graphic environment. This useful program is called kvt.

Shells are also accessible through a terminal program or a console. Remember when Linux first booted? It had a text interface. That’s the console. Linux also provides virtual consoles, which are discussed later in this chapter.





## Shell 种类

可供选择的 shell 有很多。为什么？因为人们喜欢以不同的方式做事，而且许多程序员创建了新的 shell 来解决他们喜欢的 shell 中的某些不足。这里列出的内容实际上是一棵多物种的 shell 进化树。第一个 shell（sh）的特性进行了交叉授粉，帮助了特性的演进：

- sh—起初，这是你唯一的选项。它被称为 Bourne shell。不幸的是，它没有提供你在 shell 中真正想要的东西，例如命令行编辑。
- ksh—Korn shell。这是一个非常流行的 UNIX shell。在过去，如果你安装了特定品牌的 UNIX，才能使用这个 shell。
- csh—C shell。这个 shell 在交互使用（在屏幕上输入）方面与其他两个相似，但在其编程语法上却非常不同。C shell 是第一个提供作业控制（一种管理运行命令的方式）和命令历史的 shell。
- tcsh—tcsh 是增强版的 C shell（csh）。这个 shell 与 csh 相似，但提供了命令和文件名补全以及一些命令行编辑功能。
- bash—这是大多数 Linux 发行版中的默认 shell。它被称为“Bourne Again Shell”，由自由软件基金会（GNU）创建和分发。这是一个非常好的 shell 可供学习；它具有命令行编辑和文件名补全，并且与原始的 Bourne shell 兼容。
- zsh—这是所有 shell 中最新的一种。它与 Bourne shell 兼容。

Check This Out:
大多数 shell 都提供自己的编程语言。你在 Linux 下运行的许多程序实际上都是为这里介绍的 shell 或其他命令解释器（如 Perl 和 Python）编写的 shell 脚本。

要访问内容，请单击章节和节标题。

## Complete Idiot's Guide to Linux

（Publisher: Macmillan Computer Publishing）
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

## Graphic Consoles

即使你正在运行图形终端，终端也只是让 shell 与你通信的花哨前端。KDE 提供了一个名为 kvt 的应用程序，你可以用它来访问 shell。你可以通过单击面板上的 kvt 图标来启动终端。该图标如图下一图所示。

面板上的 kvt 按钮看起来像这样。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_113_0.png)

kvt 终端程序通过 KVT 提供对 shell 的直接访问。（其他终端仿真器，例如称为 xterm 的仿真器，也可供你使用。）

如果你正在运行 X，现在按 Ctrl+Alt+F2 进入控制台。我希望你能充分体验在命令行上工作的感觉，并放弃图形环境提供的一些便利。这会让你的体验更“纯粹”。

## Check This Out:

如果你在控制台上工作，你可以同时在多个控制台上工作。每次切换时，你可以通过按 Alt+Fn 来访问虚拟控制台，其中 Fn 为 F1–F6。你将获得一个全新的虚拟控制台，包含登录提示等一切内容。

如果你已登录 X（KDE），你仍然可以访问虚拟控制台。你可以通过按 Ctrl+Alt+Fn 来激活虚拟控制台，其中 Fn 为 F2–F6。要返回到运行 KDE 的 X 会话，请按 Alt+F7。（默认情况下 X 会话在终端 7 下运行。）

## Logging in Through a Console

通过控制台登录与登录 KDE 或 X Windows 并无太大不同。显而易见的区别是，与使用漂亮的 GUI 不同，你会得到一个文本界面：

```
Caldera OpenLinux(TM)
Lite
Version 1.2
Copyright 1996–1998 Caldera, Inc.

login: username
Password: mypassword
```

通常，你的密码不会回显到屏幕上，以保护你和你的账户。如果你正确输入了登录名和密码，你就可以开始了。

## What Shell Are You Running?

默认情况下，除非你的系统由其他人配置，否则你应该正在运行 bash。要检查你正在运行什么 shell，请输入 echo $SHELL。

前面带有美元符号的词表示该词实际上是一个变量的名称。echo 命令将打印该 $SHELL 环境变量中找到的值。结果应类似于此处所示的内容：

```
[alberto@digital alberto]$ echo $SHELL
/bin/bash
```

如果由于某种奇怪的原因你运行的不是 bash，请在提示符下输入命令 bash 以在本次会话的剩余时间内开始使用 bash shell。

> Check This Out:
> 在向 shell 输入命令时，请记住 Linux 是区分大小写的，因此 BASH、bash、Bash 和 BaSH 对 shell 来说是不同的命令。通常你输入的命令将全部为小写。

## Command Line Program Syntax

大多数命令行程序使用以下语法：

```
commandname [flags] arg1 arg2 argn
```

术语定义如下：

- *commandname* 是命令的名称。
- *flags* 或参数是在程序名称之后给出的选项，用于控制程序的行为。标志通常通过前导的破折号或双破折号与其它类型的参数区分开，如 `-h` 或 `--help`。其他类型的参数可以是文件名或某些程序定义的关键字。标志是区分大小写的，并且具有许多选项的工具会使用大小写字母来命名其选项。
- *arg1-argn* 是程序要处理的参数列表。通常这将是文件列表、目录名称或程序所需的东西。

一些常用命令，例如 `ls` 和 `pwd`，也内置于某些 shell 中以提高性能。我们将在下一节讨论这些命令。

> **Note:**
> 要永久更改你的 shell，请参阅第 17 章“Command Toolbox: Useful Shell Commands and Shortcuts”中的“Changing Your Shell”部分。

## Navigating the File System

你需要学习的第一件事是如何使用 shell 导航。你知道如何使用 KFM 在文件系统中移动并访问文件；通过 shell 做同样的事情并不困难太多。然而，你需要学习一些命令：

- `pwd`
- `ls`
- `cd`

## Where Are You?: pwd

你可能想知道的第一件事是你在哪一个文件系统中。如果你刚登录，你可能在你的主目录中。即使我们知道这一点，为了学习体验，在提示符下输入 pwd：

```
[alberto@digital alberto]$ pwd
/home/alberto
```

`pwd` 代表“print working directory”。shell 将通过列出你当前位置的绝对路径来响应。绝对路径是指从根（`/`）目录指定的路径。

Products | Contact Us | About Us | Privacy | Ad Info | Home

Use of this site is subject to certain Terms & Conditions. Copyright © 1996-2000 EarthWeb Inc.
All rights reserved. Reproduction whole or in part in any form or medium without express written permission of EarthWeb is prohibited.

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

（Publisher: Macmillan Computer Publishing）
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Listing Files

接下来你想做的事情是列出当前目录中的文件。这是通过 ls 命令完成的，其代表 list：

```
[alberto@digital alberto]$ ls
Desktop      images      linkToImages  test.txt
Mail         kde         nsmail        test.txt<
html         lg          test.rc       todo.txt
```

正如你所见，ls 的普通调用并不能很好地区分目录（文件夹）和文件。

要让 ls 为你提供有关找到的文件的更多信息，你需要指定 -F 标志。此选项使 ls 在文件名后附加一个字符以指示其类型。

文件类型指示符为

- * 用于程序或可执行脚本
- / 用于目录
- @ 用于符号链接
- | 用于管道
- = 用于套接字
- 无用于普通文件

```
[alberto@digital alberto]$ ls -F
Desktop/      images/      linkToImages@  test.txt
Mail/         kde/         nsmail/        test.txt<
html/         lg/          test.rc        todo.txt
```

现在你可以区分基本类型。ls 提供了许多更多选项。更有用的选项在下表中列出。

## Useful ls Options

| Option | Action |
|--------|--------|





-F	标记文件类型
-l	显示长列表
-a	列出所有文件包括隐藏文件
-s	打印文件大小
-t	按文件时间排序，新文件在前
-R	递归列出文件包括其他目录的内容
-i	列出文件 inode

你可以将多个标志组合在一起，如 ls -Flai。这与 ls -F -l -a -i 相同，只是节省了一些击键。以下是该选项的输出：

```
[alberto@digital alberto]$ ls -Flai
total 9
157289 drwxrwxr-x  9 alberto alberto 1024 Sep  1 10:25 ./
169675 drwxrwxr-x 16 alberto alberto 1024 Sep  1 10:24 ../
157290 drwxrwxr-x  2 alberto alberto 1024 Sep  1 10:24 Desktop/
157291 drwxrwxr-x  2 alberto alberto 1024 Sep  1 10:24 Mail/
157292 drwxrwxr-x  2 alberto alberto 1024 Sep  1 10:24 html/
157293 drwxrwxr-x  2 alberto alberto 1024 Sep  1 10:24 images/
157294 drwxrwxr-x  2 alberto alberto 1024 Sep  1 10:24 kde/
157295 drwxrwxr-x  2 alberto alberto 1024 Sep  1 10:24 lg/
157296 lrwxrwxrwx  1 alberto alberto    6 Sep  1 10:24 linkToImages -> images/
157297 drwxrwxr-x  2 alberto alberto 1024 Sep  1 10:24 nsmail/
157298 -rw-rw-r--  1 alberto alberto    0 Sep  1 10:25 test.rc
157299 -rw-rw-r--  1 alberto alberto    0 Sep  1 10:25 test.txt
157300 -rw-rw-r--  1 alberto alberto    0 Sep  1 10:25 test.txt<
157301 -rw-rw-r--  1 alberto alberto    0 Sep  1 10:25 todo.txt
```

此列表包含大量信息，我将在本章和其他章节中分段介绍。为了完整起见，列表中列出的项目如下（从左到右）：

- 文件的 inode
- 文件的权限
- 文件的硬链接数
- 文件的所有者
- 文件所属的组
- 文件的大小
- 文件的最后修改日期
- 文件的名称

## Techno Talk: Links, Sockets, and Inodes???

- 这是什么链接？符号链接（在其他操作系统中也称为别名或快捷方式）是一个指向另一个文件的文件，是常用的工具。硬链接很少由用户创建，是指向具有多个其他文件名的同一数据块的文件名。
- 这是什么管道和套接字？管道和套接字是程序之间通信创建的特殊文件。它们很少被看到，但你可能在 /dev 目录中看到一两个套接字。
- 这是什么 inode？inode 是磁盘块的地址。当你通过 ls 请求查看 inode 信息时，ls 会打印文件中第一个块的地址。你可以使用此信息来判断两个文件是否实际上是具有不同名称的同一文件。我们在谈论链接时会再多谈一点。

你不需要进入一个目录就可以列出它。如果你向 ls 提供文件或目录的路径名，ls 将列出请求的文件或目录：

```
[alberto@digital alberto]$ ls /opt
bin/        kde/        man/        netscape/
[alberto@digital alberto]$ pwd
/home/alberto
```

## ls in Technicolor

随 Linux 发行的 ls 版本具有以不同颜色显示不同文件类型的功能。此功能非常有用，因为它使区分文件、目录和程序变得容易。

要启用此行为，你可以输入 ls --color，事情就会发生。最流行文件类型的颜色在下表中列出。

### Typical File Colors (ls --color)

| File Type | Color |
|---|---|
| Regular Files | White |
| Programs | Green |
| Directories | Blue |
| Links | Aqua |

很不错吧？它如此好用，你可能希望文件类型始终以颜色显示。幸运的是，你可以。继续阅读以了解如何更改某些 shell 命令的默认选项。

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Making Shell Options the Default

如果你发现这些选项有用，很可能你会想让它们成为默认值。当你运行 shell 时，有许多环境变量控制 shell 的行为。对于 bash shell，Linux 中的默认 shell，此默认信息存储在 /etc/profile 文件上。

你可以通过向主目录中的 .bashrc 文件添加条目来覆盖某些选项。由于此文件名以点开头，默认情况下它是不可见的（并称为点文件——你以为 Linux 名称会很困难！），但它确实存在。要使 ls 默认以颜色工作，将类似以下条目添加到你的 .bashrc 文件末尾。（使用 KEdit，因为你还不知道如何使用命令行编辑器。）以下是一些示例：

```
alias ls='ls --color'
```

要使 ls 使用 -F 选项，添加类似以下的行：

```
alias ls='ls -F'
```

要使 ls 同时使用 -F 和 --color 选项，添加类似以下的行：

```
alias ls='ls -F --color'
```

正如你所猜测的，alias 将名称与命令关联。要在 bash 中创建别名，你使用关键字 alias，后跟别名的名称，后跟等号 (=) 标志，后跟命令的名称。如果命令长于一个词（即它有参数），你需要用单引号 (') 括起命令及其参数。你可以为别名使用任何你喜欢的名称。如果别名的名称与某个系统命令相同，则别名是执行的命令。

查看你的 .bashrc 以查看已为你定义的别名。

## Changing Directories: cd

现在你知道如何找出你所在的位置以及列出目录中的文件，是时候学习如何去某个地方了。为此，你使用 cd 命令。cd 代表 change directory。要去某个地方，输入 cd 命令，后跟你想去的目录的名称：

```
[alberto@digital alberto]$ cd /
[alberto@digital /]$ ls
amd/      dev/      install@  opt/      tmp/
auto/     etc/      lib/      proc/     usr/
bin/      home/     lost+found/ root/     var/
boot/     initrd/   mnt/      sbin/     vmlinuz
```

此示例带你到根 (/) 目录。

要返回到你的主目录，输入不带任何参数的 cd 命令：

```
[alberto@digital /]$ cd
[alberto@digital alberto]$ ls
Desktop/    images/    linkToImages@  test.txt
Mail/       kde/       nsmail/        test.txt<
html/       lg/        test.rc        todo.txt
```

## Relative and Absolute Paths

如果你在指定的路径中不提供前导斜杠 (/)，路径就是相对的。shell 会将当前工作目录附加到你指定的路径，如下所示：

```
[alberto@digital alberto]$ cd images/anotherdir
[alberto@digital anotherdir]$ pwd
/home/alberto/images/anotherdir
```

如果目录 images 位于 /home/alberto/images，则第一行等同于指定以下内容：

```
cd /home/alberto/images/anotherdir
```

指定相对路径时，有用的是知道当前目录可以用句点 (.) 指定，而父目录，即包含当前目录的目录，可以用两个句点 (..) 指定，给定如下目录结构：

```
[alberto@digital alberto]$ ls
Desktop/    images/    linkToImages@  test.txt
Mail/       kde/       nsmail/        test.txt<
html/       lg/        test.rc        todo.txt

[alberto@digital alberto]$ cd images (goes down to images)
[alberto@digital images]$ pwd
/home/alberto/images
[alberto@digital images]$ cd ../kde (up one and down kde)
[alberto@digital kde]$ pwd
/home/alberto/kde
[alberto@digital kde]$ cd .. (up one)
[alberto@digital alberto]$ cd ./kde (down kde in the current dir)
[alberto@digital kde]$ pwd
/home/alberto/kde
```

## Techno Talk: The PATH Environment Variable

shell 在 PATH 环境变量中存储的文件路径列表中查找命令和程序。环境变量存储其他程序和命令可以访问的信息。环境变量存储诸如你使用的 shell、你的登录名和你的当前


working directory. 要查看当前已定义的所有环境变量的列表，请在提示符下输入 set。

当你在 shell 提示符下输入命令时，shell 会按顺序在 PATH 变量列出的每个目录中查找该命令的程序文件。找到的第一个与你输入的命令匹配的程序将被运行。如果命令的程序文件不在你的 PATH 环境变量列出的目录中，shell 会返回 “command not found” 错误。

默认情况下，shell 不会在你的当前工作目录或主目录中查找命令。这实际上是一种安全机制，可以防止你意外执行程序。如果恶意用户在你的主目录中放置了一个名为 ls 的有害程序怎么办？如果你输入 ls 而 shell 在 /bin 目录中的真实程序之前先在你的主目录中查找假程序，你认为会发生什么？如果你认为会发生坏事，你的想法是对的。

由于你的 PATH 中没有当前目录 (.) 作为搜索位置，因此当前目录中的程序必须使用绝对路径或相对路径 ./programname 指定调用。

要查看哪些目录是你的 PATH 的一部分，输入以下命令：

```
echo $PATH
```

```
[alberto@digital alberto]$ echo $PATH
/bin:/usr/bin:/opt/bin:/usr/local/bin:/usr/X11R6/bin:/opt/kde/bin:
```

请注意，目录路径之间用冒号 (:) 分隔。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Filename Expansion: Tab

正如我前面所说，shell 并不是很符合人体工学，大多数人都不喜欢经常输入命令或长路径名。根据你使用的 shell，你可能有 shell 为你补全文件名和命令名的能力。每当你指定的路径部分不会引起混淆时，shell 就会这样做。

要在 bash 上激活补全，你所需要做的就是在输入足够字符后按 Tab。如果你想要列出 /usr/local/bin 目录的内容，你可以输入 ls /u<Tab>/lo<Tab>/b<Tab>，shell 会为你展开每条路径，节省你的按键次数。

如果 shell 无法完成扩展，因为存在多个可能的补全，再次按 Tab 会列出所有可能的匹配项。这在你忘记命令名称时非常有用。例如，如果你输入 l<Tab><Tab>，shell 会响应并列出所有以 l 开头的程序：

```
[alberto@digital alberto]$ l<Tab><Tab>
laser        lesskey      lkbib        lockfile     lpr
last         let          lmorph       logger       lprm
lastb        lex          ln           login        lptest
lastcomm     lha          lnd ir       logname      ls
latex        lightning    loadkeys     logout       lsattr
lbxproxy     lintopvf     loadunimap   look         lsdev
ld           lisa         local        lookbib      lynx
ld86         lispm tpgm   locale       lout         lz
ldd          listalias    localedef    lpq
less         listres      locate       lpqall.faces
```

## Exiting the Console

要退出控制台，请发出 logout 命令。此命令将结束你的会话，清除屏幕并返回到登录提示符。要从控制台重新启动计算机，可以按 Ctrl+Alt+Delete。

如果使用 kvt 或 xterm 等终端模拟器，你只需关闭窗口并像以前一样退出系统即可。

如果你让系统保持登录状态（这在你的家庭机器上可能是可以接受的），请记住任何人都可以查看和编辑你的文件。然而，永远不要让 root 会话保持打开状态，因为这可能导致致命的安全问题甚至灾难性的用户错误。

通常，Linux 系统会永久运行，只有在升级或某种软件故障需要时才关闭。

## Shutting Down a Linux Box

关闭系统与你在 PC 上习惯的方式有点不同。与 DOS 或其他一些系统不同，类 UNIX 系统需要温和地关闭。即使没有人登录，也会运行许多进程。这些进程需要正确停止，否则会发生坏事。关闭是通过 shutdown 命令完成的。

在使用 shutdown 命令之前，你需要拥有 root 权限。这意味着你需要在使用该命令之前以 root 身份登录。

shutdown 命令接受多个参数。这些选项指定系统将如何关闭以及何时关闭。此处必需的选项是 -h，表示“halt”，以及关键字 now，表示系统应立即开始关闭。

要在 root 控制台上优雅地关闭系统，输入以下内容：

```
[root@digital root]# shutdown -h now
```

## Rebooting a Linux Box

重启只是重新启动计算机的 fancy 名称。前面显示的 shutdown 命令可用于重启，如果你指定 -r 选项而不是 -h 选项。-r 选项表示 reboot：

```
[root@digital root]# shutdown -r now
```

重启系统的最简单方法是同时按下 Ctrl+Alt+Del 键，使系统进入重启序列。你可以在未登录控制台的情况下执行此操作。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

To access the contents, click the chapter and section titles.

## Chapter 12
Working with Files on the Shell

## In This Chapter

- How to Manage and Organize Your Files Using a Shell
- How to Read Files

## Working with Files and Folders

在第 11 章“Shells and Consoles”中，你学习了如何登录和注销以及如何使用 shell 导航文件系统。在本章中，你将继续探索 UNIX shell 并学习如何使用它来操作文件和目录。

## Creating a New Empty File: touch

大多数时候，你会通过使用某些应用程序或 shell 程序来创建文件。出于教学目的，我在这里介绍一个允许你创建空文件的命令。这种凭空生成文件的能力将使你的探索更有趣一些。

如果你需要创建空文件，可以轻松使用 touch 命令完成。touch 的目的是修改文件的访问和创建时间，但作为副作用，如果文件尚不存在，它会创建文件。

要创建文件，输入命令 touch 后跟文件名：

```
[alberto@digital alberto]$ touch afile
```

要验证文件是否已创建，你可能想使用第 11 章中解释的 ls 命令。

你可以向该命令提供多个文件名。文件名可以使用相对或绝对路径，或两者混合指定。命令执行时，它会创建指定的文件。

## Removing Files: rm

要删除文件，使用 rm 命令。这个命令非常危险，原因只有一个：在 Linux（或通常的 UNIX）下删除的文件，除非你在磁带、软盘或其他介质上有备份，否则无法恢复。

要删除文件，输入以下内容：

```
[alberto@digital alberto]$ rm afile
```

由于其固有的危险，rm 命令提供了一个选项，可以询问你尝试删除的任何文件。如果你提供 -i 选项，它会先询问你的意图：

```
[alberto@digital alberto]$ rm -i afile
rm: remove `afile'? y
```

命令别名在第 11 章“Making Shell Options the Default”部分描述。要查看已激活的命令别名列表，在命令提示符下输入 alias。所有活动的别名列表将被打印出来供你检查。

> Check This Out:
> Oops! I deleted file x rm on tape or another disk, can I get it back?
> Is there a backup on tape or another disk?
> • Yes: yes, you can.
> • No: nope, the file is gone.

## Creating a Directory: mkdir

要创建目录，使用命令 mkdir 并指定目录名称（通常，名称可以是“相对”文件名或绝对路径）：

```
[alberto@digital alberto]$ mkdir adir
```

如果你需要创建整个目录树，指定选项 -p 和你需要的路径：

```
[alberto@digital alberto]$ mkdir -p
adir/anotherdir/yetanother
```




如果路径的某些部分已经存在，则保留这些部分并将缺失的部分添加到路径中。

## 重点关注：谨防 root 的强大权限！

如果你以 root 身份登录，这条规则适用于你：root 是一个特殊的管理员账户，可授予对整个系统的无限制访问权限。在需要执行系统管理类型任务时，这非常有价值，但这不是你用于其他任何目的的账户。root 账户可以执行某些不可逆的操作，例如擦除磁盘上的所有文件或其他某种灾难性操作。

在你了解更多关于 Linux 和 UNIX 的一般知识之前，我建议你除非绝对必要，否则不要使用 root 账户，例如添加软件或配置某种设备的情况。

如果你没有登录到自己的账户，立即创建一个！有关更多信息，请参阅第 18 章“用户、组和密码”。

## 删除空目录：rmdir

要删除空目录，请使用 rmdir 命令。rmdir 命令是“安全”的，因为它只会在目录为空时才删除目录。其用法如下：

```
[alberto@digital alberto]$ mkdir empty
[alberto@digital alberto]$ rmdir empty
```

## 同时删除文件和目录：rm -R

通常当你想要擦除一个目录时，你也想处理掉它包含的所有文件。在 UNIX 和 Linux 中，此任务使用你之前看到的 rm 命令完成。

要产生这种效果，rm 需要在删除目录之前递归删除找到的文件。虽然这是正确的做法，但要小心：你很容易在意识到发生了什么之前就擦除大量内容。不要忘记，shell 操作非常快。在删除文件时要小心；当你以 root 身份登录时尤其重要，因为一条命令就可能摧毁你的整个文件系统。

要访问内容，请点击章节和节标题。

## Linux 完全傻瓜指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 复制文件：cp

要复制文件，请使用 cp 命令。cp 的语法如下：

```
cp [options] source destination
```

source 是你想要复制的文件名，destination 是你创建的副本的名称。

如果 destination 是一个目录（路径未指定文件名），文件将以其原始名称复制到指定目录中。

options 参数用方括号括起来，表示选项是可选的。我们将在下一节中使用 cp 命令的一个选项。

这里有一个例子：

```
[alberto@digital alberto]$ ls -F
Xrootenv.0  afile  anotherlink  helloworld*
ad ir/  alink@  hello

[alberto@digital alberto]$ cp helloworld /tmp

[alberto@digital alberto]$ ls -F /tmp
fvw mrca00455  helloworld*  install.log  screens/
```

你可以通过在单个命令中列出多个用空格分隔的源文件，将多个文件复制到单个目录中。唯一的要求是最后一个参数（destination）必须是目录。

## 复制目录

复制目录的方式与复制文件非常相似。复制目录时，你需要告诉 cp 你想要递归复制源目录包含的所有文件和目录。这可以通过 -R 选项轻松完成。语法如下：

## 移动文件和目录：mv

要移动文件或目录，你使用 mv 命令。移动文件与复制文件类似。最大的区别是新副本创建后原始文件会被删除。mv 命令遵循以下语法：

```
mv [options] source destination
```

```
[alberto@digital alberto]$ ls
Xrootenv.0  adir/      afile      alink@     anotherlink
    helloworld*
[alberto@digital alberto]$ mv afile file2
[alberto@digital alberto]$ ls
Xrootenv.0  adir/      alink@     anotherlink  file2
    helloworld*
```

mv 命令也可以用于移动整个目录树。

mv 命令提供多个选项。有关更多信息，请参阅其手册页。

> 注意：
> 要阅读 UNIX 工具或命令的文档，请参阅第 15 章“帮助请”。

## 技术谈：符号链接

链接是指向文件系统其他位置的文件或文件夹的指针。链接看起来并像它指向的文件或文件夹一样工作。如果你通过 KFM 查看它，它将具有相同的图标（区别是它旁边会有一个小箭头）。如果你对 ls 命令指定 -F 标志，你会看到一个 at 符号（@）附加在链接文件名的末尾。当你打开一个链接时，你会看到链接指向的文件的相同文件内容。

链接作为组织工具非常有用。它们允许你方便地访问可能存储在文件系统深处（因此具有长而难以输入的文件路径）或甚至在网络不同部分的<|message|>。无需遍历长路径来访问文件，你只需访问一个方便位置的链接即可。

链接也可以用于节省磁盘空间。不要复制大文件以便随时使用，你可以在方便的地方创建指向它们的链接。链接占用非常少的磁盘空间，只有几个字节。

符号链接存储它指向的文件的文件路径。你可以移动和重命名链接而不影响它。然而，如果原始文件——链接指向的文件——被移动、删除或重命名，链接就会断开。断开的链接可以通过将原始文件恢复到其正确位置和名称来修复。否则它们可能应该被删除。符号链接将文件路径与文件关联起来。

## 技术谈：硬链接

还有另一种类型的链接称为硬链接。硬链接与符号（或软）链接类似，因为它为访问文件提供了不同的名称。然而，相似之处到此为止。硬链接有一个优势：与软链接不同，如果你移动、删除或重命名原始文件，软链接会断开，而硬链接不会。

硬链接实际上并不指向文件路径，如软链接那样；相反，它们指向磁盘上存储的实际数据。因此，所有文件至少有一个链接：文件创建时分配给它的名称。当你为文件添加另一个硬链接时，文件系统将其视为文件具有不同的名称，但链接指向的数据与原始文件相同。如果你删除原始文件，剩余的链接仍然指向磁盘上的相同数据。

正如你所见，硬链接与文件写入的实际磁盘存储绑定。因此，硬链接不能跨越磁盘边界。

另一个小的区别是硬链接只引用文件——永远不引用目录。唯一能区分硬链接和文件的方法是使用 ls 的 -i 和 -l 选项，并且 ls 报告硬链接计数大于一并且打印的 inode 地址相同：

```
[alberto@digital alberto]$ ls -il
169688 -rwxrwxr-x  2 alberto  alberto      74 Aug 26 12:19 bye.pl
169972 -rwxrwxrwx  1 alberto  alberto      65 Aug 30 14:49 capture.pl
169688 -rwxrwxr-x  2 alberto  alberto      74 Aug 26 12:19 hello.pl
```

在前面的例子中，hello.pl 和 bye.pl 具有相同的 inode：169688。注意，两者都说它们有两个硬链接。两个文件实际上是同一个文件，只是名称不同！

## Linux 完全傻瓜指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

要访问内容，请点击章节和节标题。

## 创建链接：ln

链接是使用 ln 命令创建的。ln 用于创建软链接和硬链接。命令的语法是

```
ln [options] source destination
```

要创建符号（软）链接，你指定 -s 选项，表示 symbolic。以下是列出目录的示例：

```
[alberto@digital alberto]$ ls -l
total 2
drwxrwxr-x  3 alberto alberto      1024 Aug  1 20:41 adir/
-rw-rw-r--  1 alberto alberto        57 Aug  2 13:12 file
```

以下是创建硬链接的示例：

```
[alberto@digital alberto]$ ln file file2
```

以下是创建软链接的示例：

```
[alberto@digital alberto]$ ln -s file file3
```

以下是再次列出目录的语法。注意 file3 指向 file：

```
[alberto@digital alberto]$ ls -l
total 3
drwxrwxr-x  3 alberto alberto      1024 Aug  1 20:41 adir/
-rw-rw-r--  2 alberto alberto        57 Aug  2 13:12 file
-rw-rw-r--  2 alberto alberto        57 Aug  2 13:12 file2
lrwxrwxrwx  1 alberto alberto         4 Aug  2 13:15 file3 -> file
```

以下是删除原始文件的语法：

```
[alberto@digital alberto]$ rm file
```



这里是再次列出文件的语法。请注意 file3 现在指向一个不存在的文件！

```
[alberto@digital alberto]$ ls -l
total 2
drwxrwxr-x   3 alberto alberto      1024 Aug  1 20:41 adir/
-rw-rw-r--   1 alberto alberto         57 Aug  2 13:12 file2
lrwxrwxrwx   1 alberto alberto          4 Aug  2 13:15 file3 -> file
```

链接在 Linux 中经常被使用，以便文件可以同时放置在多个目录中。例如，目录 /usr/X11R6 包含 X Windows 使用的文件。一些较旧的 X Windows 程序安装到 /usr/X11R5 或 /usr/X11R4 中。通过一系列符号链接，Linux 可以使来自三个目录中的文件都出现在更通用的 X Windows 目录 /usr/X11 中，以便于访问。这种组织方式是符号链接的主要用途之一。

## 读取文件

能够移动和组织文件是一项重要的技能。最终，计算机主要用于存储和检索信息。以下是当你在终端上时可用于读取文件的几个命令：

- cat: 将文件内容复制到终端
- less: 一屏一屏地分页显示内容
- head: 查看文件中的前几行
- tail: 查看文件中的后几行

## 拼接：cat

cat 命令读取一个或多个文件并将结果打印到屏幕上。 （它将所有文件拼接至屏幕。）cat 是一个通用命令，在将多个命令链接在一起时使用频率非常高。当我们在第 14 章“让 Shell 发挥作用”中探讨重定向时，我会向你展示 cat 的真正用法。

cat 的基本语法是

```
cat [options] files
```

以下是使用 cat 查看 /etc/passwd 文件的示例（这是存储用户信息的文件）：

```
[alberto@digital alberto]$ cat /etc/passwd
root:UGQD...:0:0:root:/root:/bin/bash
bin:*:1:1:bin:/bin:
daemon:*:2:2:daemon:/sbin:
adm:*:3:4:adm:/var/adm:
lp:*:4:7:lp:/var/spool/lpd:
sync:*:5:0:sync:/bin:/bin/sync
shutdown:*:6:0:shutdown:/sbin:/sbin/shutdown
halt:*:7:0:halt:/sbin:/sbin/halt
mail:*:8:12:mail:/var/spool/mail:
news:*:9:13:news:/var/spool/news:
uucp:*:10:14:uucp:/var/spool/uucp:
operator:*:11:0:operator:/root:
games:*:12:100:games:/usr/games:
gopher:*:13:30:gopher:/usr/lib/gopher-data:
ftp:*:14:50:FTP User:/home/ftp:
nobody:*:99:99:Nobody:/:
postgres:!!:100:101:PostreSQL Server:/var/lib/pgsql:/bin/bash
alberto:YMMhuMSrulhME:501:501:AlbertoRicart:/home/alberto:/bin/bash
```

正如你所见，cat 打开了文件 /etc/passwd 并将每一行打印到控制台。

cat 命令提供了几个选项；最有用的列在表 12.1 中。

## 表 12.1 cat 命令选项

| Option | Description |
|--------|-------------|
| -n | Number all lines |
| -s | Squeeze multiple blank lines into one |
| -v | Display all characters (invisible characters, too, with the exception of tabs and newlines) |
| -A | Display all characters (invisible characters, too) |

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## 一次查看一页：less

当你使用 cat 时，你可能已经发现如果文件大小超过屏幕所能容纳的范围，内容滚动得太快而无法阅读。处理这种情况的一种方法是使用分页命令。

分页器允许你一次查看一屏（或一页）信息。有两个命令可以使用：原始分页器 more 和更好的分页器 less。在这些程序的情况下，less 实际上是 more。例如，less 允许你“后退”并向上滚动，而 more 不允许。less 也不会在你告诉它之前退出。

当 less 打印一屏内容时，它会在屏幕底部放置一个冒号 (:)。这意味着当前页之后还有更多信息。在冒号显示时，你可以与 less 交互并向其发送命令。以下是一些更有用的命令：

- 要向前（或向下）滚动另一屏，请按空格键
- 要向后（或向上）滚动一屏，请按 B
- 要显示当前正在查看的文件名以及你在文件中的位置信息，请按 =
- 要停止阅读，请按 Q

当你到达文件末尾时，less 会恰当地在屏幕底部打印“END”；如果想退出程序，请按 Q。

## 查看前几行：head

有时你不想读取整个文件，只想看前几行。用于此的命令称为 head，它打印文件中的前十行：

```
[alberto@digital alberto]$ head /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:
adm:x:3:4:adm:/var/adm:
lp:x:4:7:lp:/var/spool/lpd:
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:11:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:
news:x:9:13:news:/var/spool/news:
```

如果传递 -n 选项，你可以控制 head 打印的行数：

```
[alberto@digital alberto]$ head -n 1 /etc/passwd
root:x:0:0:root:/root:/bin/bash
```

## 查看最后几行：tail

head 的对应物是 tail。默认情况下它打印最后十行。如果提供 -n 选项，head 将从文件末尾打印该数量的行：

```
[alberto@digital alberto]$ tail -n 1 /etc/passwd
alberto:x:100:100:Alberto Ricart:/home/alberto:/bin/bash
```

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

## Chapter 13
在 Shell 下进行文本编辑

## 本章内容

- 使用 Vim 视觉编辑器
- 使用 XEmacs
- 运行 Ispell

在命令行下使用编辑器是必须的。这些编辑器的用户界面通常非常别扭，尤其是当你来自 Macintosh 或 Windows 等环境时。你可以在计算机上安装的字面上一百种不同的编辑器。它们各有优缺点。在我看来，你应该学习的两个命令行编辑器是。为什么两个？因为在某些系统下只有一个或另一个可用，你应该能够使用任一个进行工作。

最受欢迎的编辑器是

- 视觉编辑器 (vi)
- Emacs

vi 是任何类 UNIX 操作系统上最广泛可用的编辑器。仅凭这一点，它就应该是你需要学习的编辑器。知道 vi 可以在所有系统中找到是一个令人安心的想法；无论你明天使用什么版本的 UNIX，你都将能够编辑文件。

> Techno Talk:
> 通常，当你使用终端时，你应该能够按 Backspace 键并删除最后一个字符。如果你按 Backspace 却得到像 "^?" 这样的奇怪字符，你的终端没有正确设置。
> 
> 通常，这种配置问题会在你通过 telnet 远程工作时出现。修复问题实际上非常容易，有 stty 程序的帮助。 （stty 程序实际上非常复杂，但你不需要知道太多关于它如何工作的细节——只需要足够修复你的问题。）

stty 程序遵循此格式：stty command characters，其中 command 是选项的名称，characters 是你在 shell 或编辑器中使用它们时看到打印的字符。

经常使用的命令是

- erase （将退格键关联）
- kill （删除光标左侧的字符）
- `intr` （中断程序）
- `susp` （挂起程序）

对于我在 UNIX 下的日常工作，我使用 Emacs 或其表亲 XEmacs。两者编辑器之间的主要区别是 vi 比 Emacs 小约 20 倍。如果你曾经（希望你永远不会）需要进行灾难恢复，vi 可以放入软盘；Emacs 不能。就功能而言，Emacs 拥有全部，而且这不是夸张。

## 改进的视觉编辑器：Vim

Linux 发行版将 vi 作为 vim 的链接。Vim 是 vi 的改进版本（见下图）：最初名称为 Vi Imitation，但现在不再如此。Vim 提供了原始程序中缺少的一系列功能，但基本命令相同。因此，如果你学习更新的 vim 编辑器，你将不会有使用 vi 的问题，只是你会错过额外的功能。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_137_0.png)

你可以在这里看到一个运行在 KDE 内的 vim 的图形版本。

## 交互式 Vim 教程

学习 vim 的最简单方法是使用在线教程。就 vim 而言，此教程（系统中的一个文件）比阅读书籍更好也更有趣，因为它是一个交互式教程。以下是如何访问它。

要通过教程，你首先需要将一个文件复制到你的主目录。教程只是一个包含如何使用 vim 的说明的文本文件。

要安装教程，将 `/usr/doc/vim-4.5-2/tutor/tutor` 复制到你的主目录。你的安装中版本号可能已更新，因此这样复制：

```
cp /usr/doc/vim*/tutor/tutor ~/ 
```

此过程会将教程文件 tutor 放入你的主目录。

要开始教程，输入以下两个命令：

```
alberto@digital alberto]$ cd
[alberto@digital  alberto]$ vim tutor
*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*
* W e l c o m e   t o   V I   T u t o r   -   V e r s i o n   1 . 2 *
*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*

               ***************
                * Lesson 1.0 *
               ***************

Vim is a very powerful editor that has many commands, too many to
explain in a tutor such as this.  This tutor is designed to describe
enough of the commands that you will be able to easily use Vim as
an all-purpose editor.

The approximate time required to complete the tutor is 25-30
minutes, depending upon how much time is spent with experimentation.

It is important to remember that this tutor is set up to teach by
use.  That means that the student needs to execute the commands
to learn them properly.

Now, make sure that your Shift-Lock key is NOT depressed and
```





## 《Linux 完全傻瓜指南》：在 Shell 下进行文本编辑

```
press the j key enough times to move the cursor so that Lesson 1.1 completely fills the screen.
```

正如你所见，输入这些命令会让你直接进入 vim 会话，教程显示在屏幕上。按照说明操作，你就开始了。教程所需时间大约为 20 到 60 分钟，取决于有多少干扰（例如电话）。

+   上一页 | 目录 | 下一页

+   产品 | 联系我们 | 关于我们 | 隐私 | 广告信息 | 首页

使用本网站须遵守特定条款和条件。版权所有 © 1996-2000 EarthWeb Inc。保留所有权利。未经 EarthWeb 书面明确许可，不得以任何形式或媒介全部或部分复制。

要访问内容，请点击章节和节标题。

## 《Linux 完全傻瓜指南》

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## Vim 基础

如果你只是想掌握其用法，这里有一个最基本的教程。

Vim 是一个模式编辑器。这意味着当你使用 vim 时，程序的行为会根据你处于命令模式还是编辑模式而有所不同。

开始吧。用 vim 创建并编辑一个文件。在你的命令行中执行以下操作：

```
[alberto@digital alberto]$ vim tutorial
~
~
~
"tutorial" [New File]
```

图形版本的 vim 可以通过在 KDE 中发出命令 gvim（图形 vim）启动。

发出命令后，编辑器将接管你的终端。空行用波浪号（~）标记。Vim 目前处于其命令模式。它正在等待你告诉它该做什么。

在命令模式下，你可以移动文档（假设有一些文本可供导航，在新文档中不会有这种情况）并发出命令。表 13.1 列出了所有光标移动命令。（正如你所见，其中一些映射到键盘上的特殊键。）

### 表 13.1 在文档中移动

| 键 | 功能 |
|---|---|
| l 或 右箭头 | 向前移动到下一个字符 |
| h 或 左箭头 | 向后移动一个字符 |
| j 或 下箭头 | 向下移动一行 |
| k 或 上箭头 | 向上移动一行 |
| w | 向前移动一个词 |
| b | 向后移动一个词 |

通常，你通过使用箭头键（或其 hjkl 对应键——我很少能记住这些）来移动光标。要滚动文档，你使用 Page Up 和 Page Down。

光标不会换行或移动到行首或行尾之外。当你到达末尾时，计算机将会鸣响。要转到下一行或上一行，请分别使用向下或向上箭头键。

当你开始一个新空白文档时，你没什么可做的；没有文本可编辑或导航。要添加文本，你需要进入插入模式。此模式允许你像在其他程序中一样输入文本；你仍然可以使用箭头键移动。（在插入模式下，hjkl 键会输入字母。）输入 i 进入插入模式。表 13.2 列出了你在命令模式下可以使用的一系列编辑命令。

### 表 13.2 Vi（Vim）编辑命令

| 命令 | 描述 |
|---|---|
| i | 插入文本（开始编辑） |
| x | 删除光标下的字符（命令模式） |
| dw | 删除字符直到词尾 |
| d$ | 删除文本直到行尾 |
| dd | 删除当前行 |
| u | 撤销上一个命令 |
| U | 撤销对该行的任何更改 |
| Ctrl+R | 重做任何撤销操作 |
| Esc | 返回命令模式，取消当前操作——重复直到 vim 发出蜂鸣声 |

要返回命令模式，按住 Esc 键直到 vim 向你发出蜂鸣声。然后你可以输入 : + 命令。命令是通过按冒号（:）后跟命令名称发出的。表 13.3 列出了让你退出 vim 的基本命令。

### 表 13.3 Vi（Vim）退出命令

| 命令 | 描述 |
|---|---|
| :q! | 不保存退出 |
| :wq | 保存并退出 |
| :wfilename | 将缓冲区写入 filename |

Vim 有一些编辑命令——以及至关重要的撤销。这些编辑命令在 vim 处于命令模式时有效。

### 命令乘数：重复操作多次

诸如删除之类的命令可以指定乘数。如果你先输入一个数字，命令将被重复该次数。

考虑以下文本：

```
This is one line of text.
This is another line of text.
```

要删除单词 This 和 is，将光标移至 T 下。确保你处于命令模式，按 Esc 直到 vim 发出蜂鸣声；然后输入 2dw。要删除两行文本，将光标放在第一行的任何位置并输入 2dd。

乘数也适用于在文档中移动。要向下移动五行，你可以输入 5，然后是向下箭头。

### 从 Vim 访问 Shell

你可以通过在命令前加上感叹号（!）来执行 shell 命令：

```
:!shellcommand
```

命令执行完毕后，会提示你按 Enter 返回编辑器。要获得交互式 shell，将 shell 的名称作为 shellcommand 输入（bash）。完成 shell 工作后，在 shell 提示符下输入 exit，你将返回编辑器。

### 其他内容

Vim 相当强大。它支持多个文档——或称为缓冲区——以及许多其他功能。这里介绍的命令只是你使用终端编辑文件所需的最基本知识。我鼓励你通过教程并访问 vim 的主页 http://www.vim.org。你会很高兴你这样做了。

要访问内容，请点击章节和节标题。

## 《Linux 完全傻瓜指南》

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## XEmacs

XEmacs 是 Emacs 的变体，Emacs 是 GNU 超级编辑器，随 Caldera OpenLinux 提供。XEmacs 在图形环境（如 X（KDE））下使用时提供额外的增强功能——因此得名“X”。在终端下，它几乎与常规 Emacs 完全相同。任何关于 Emacs 的引用在用法上都适用于 XEmacs。

Emacs 是最强大的编辑器之一。它适用于 UNIX、Windows 和大量其他操作系统。它提供的功能多到足以单独写一本 500 页的书来介绍！

Emacs 是一个可扩展的编辑器。使用一种名为 Lisp 的编程语言，Emacs 可以轻松扩展以完成几乎任何可想象的事情。

许多硬核 UNIX 用户只使用一个程序：Emacs。他们在开始工作会话时启动它，并在退出系统时关闭它。几乎所有工作都通过 Emacs 处理，包括访问 shell。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_143_0.png)

XEmacs 在控制台上看起来像这样。

从 Emacs 你可以阅读、编写和组织你的电子邮件和日历，管理和组织你的文件，浏览网络，阅读新闻，开发软件，通过网络传输 FTP 文件等等。不管你在 UNIX 下做什么，很可能你都可以通过 Emacs 来做。当然，Emacs 也编辑文件。如果你觉得 Emacs 实际上是一个环境，你是对的。这就是 Emacs 与其他编辑器的区别。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_144_0.png)

这是通过 X 的 XEmacs——注意所有的按钮和菜单！

Emacs 通过模式完成所有操作。模式只是一种专门用于与特定程序交互或处理特定文件格式（如文本或编程源代码）的界面。模式根据特定任务的需求量身定制。如果听起来很复杂，其实并不复杂。模式由 Emacs 根据你正在做的事情和你正在编辑的文件自动处理。

### 启动 XEmacs 和 XEmacs 教程

要进入 Emacs（XEmacs），只需在命令提示符下输入 xemacs。Emacs 会用欢迎信息和选项列表迎接你。Emacs 下的大多数按键操作如下：

```
Ctrl+letter letter
```

当你看到命令列为 C-t h 时，意味着你必须先按 Ctrl+t，然后单独按 h。是的，Emacs 有很多命令键，需要一点时间来适应；不过这段时间是值得的。

要退出 Emacs，输入 Ctrl+c Ctrl+x；这会将你返回到 shell。教授 Emacs 超出了本书的范围，但可以说，如果你要进行大量文本编辑，探索它是值得的。

Emacs 的一个令人印象深刻的功能是，你可以通过 FTP 编辑文件，就像它们在你的磁盘上本地一样。对于从事 Web 相关服务工作的用户来说，这个功能非常棒。如果你的文件可以通过 FTP 访问，它们就可以像本地文件一样进行编辑和操作。然而，这是一个高级主题，留待另一本书讨论。

如果你是程序员，Emacs 会即时进行源代码格式化，因此你的源代码始终以可读的方式格式化。在阅读他人的代码时，能够以你可读的方式重新格式化代码的能力非常宝贵。Emacs 还提供了一个 IDE（集成开发环境）：你可以直接从 Emacs 构建程序并调试它。

Emacs 还有一个在线教程。要访问教程，启动 Emacs，并在欢迎窗口中输入 C-h t。





## 检查拼写：Ispell

在 Linux 中，可以使用一个名为 Ispell 的程序从命令行进行拼写检查。Ispell 代表交互式拼写检查。Ispell 使您能够使用编辑器编写文档（该编辑器可能直接与 ispell 集成），然后从 shell 中检查它，如下所示：

```
ispell filenames
```

如果您提供多个文件，Ispell 可以同时检查多个文件。您可以将单词添加到自己的私人词典中。如果未发现拼写错误，程序将不带任何消息退出。

Ispell 非常友好且易于使用。下面的图显示了正在运行 ispell 的终端。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_145_0.png)

Ispell，即交互式拼写检查器，从 shell 中使用起来很容易。

Ispell 会突出显示有问题的单词并显示其出现的上下文。如果它找到可能的更正，它会显示它们的列表。要接受其中一个建议的替换，只需键入其编号即可。其他操作如窗口或屏幕底部所列。

要访问内容，请单击章节和节标题。

## Linux 完全傻瓜指南

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 第 14 章

## 让 Shell 发揮作用

## 本章内容

+   - 输出和输入重定向
+   - 将命令链接在一起
+   - 正则表达式
+   - 命令历史

在第 11–13 章中，您学习了一些关于命令和 shell 的基础知识。虽然单个命令很可能就是您要做的最多的事情，但 shell 的真正威力在于您能够将一系列命令串联起来执行比任何单个命令都能完成的更复杂的任务。Shell 允许您这样做，在本章中，您将学习如何利用这种能力，以及一些其他不错的命令 shell 技巧。

## 同时使用多个命令

您可以同时发出多个命令；只需用分号（;）分隔每个命令即可。以下是一个示例：

```
[alberto@digital alberto]$ pwd; cd ..; pwd; ls -lg
/home/alberto
/home
total 3
drwxr-xr-x 14 alberto users 1024 Aug 18 19:01 alberto/
drwxr-xr-x 5 root root 1024 Aug 14 08:09 ftp/
drwxr-xr-x 7 root root 1024 Aug 14 08:09 httpd/
[alberto@digital home]$
```

在这个例子中我做了几件事：

我使用 pwd 列出了当前工作目录，然后我通过键入两个句点（ . . ）将目录更改为父目录（向上一级）。我还列出了新的当前工作目录并要求列出其中的文件。

当我要求 cd 向上一个目录时，它就这样做了，当所有命令执行完毕后，我被留在最后一个影响我当前目录的命令停止的地方（/home 目录——如果您查看我 shell 提示符的末尾，您可以看出这一点）。

## 命令组和子 Shell

*命令组* 允许您在子 shell 中执行一系列命令。当您创建命令组时，Linux 会启动一个新的 shell 子进程，与您的当前 shell 不同，以执行它。当命令组执行完毕后，它会将控制权返回给您的 shell。

您可以通过用括号括住命令来创建命令组，如下所示：

```
[alberto@digital alberto]$ (pwd; cd ..; pwd; ls -lg)
/home/alberto
/home
total 3
drwxr-xr-x 14 alberto users 1024 Aug 18 19:01 alberto/
drwxr-xr-x 5 root root 1024 Aug 14 08:09 ftp/
drwxr-xr-x 7 root root 1024 Aug 14 08:09 httpd/
[alberto@digital alberto]$
```

如果您真的很注意，您还会注意到当您执行命令组时，当前环境不会受到影响。请注意我的起始目录是 alberto，而命令组结束后的最终目录仍然是 alberto...尽管其中一个命令向上移动了一个目录！

这种移动的原因是命令组的执行会创建子 shell。子 shell 有自己的环境。 （其初始环境与您当前的环境相匹配。）当子 shell 执行 cd 命令时，它会更改子 shell 的环境。但是，它不会影响父 shell 的环境，即我键入命令的 shell。

## 重定向

Shell 的大部分有用性来自于将输入和输出重定向到和来自文件的能力。大多数 shell 程序设计为使用流处理数据。

流只不过是作为输入或输出流动的数据。例如，命令的输入流通常来自键盘，其输出流通常流向终端显示。在 UNIX 下，所有程序都使用三个流与外部世界通信：

+   - STDOUT—标准输出流（通常是显示器）
+   - STDIN—标准输入流（通常是键盘）
+   - STDERR—标准错误流（通常是显示器

流可以通过 shell 轻松互连或以不同的方式连接。您的 shell 可以使程序使用文件作为其输入流，并使用输出流将结果写回文件。这称为重定向。

要访问内容，请单击章节和节标题。

## Linux 完全傻瓜指南

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

上一页 目录 下一页

## STDOUT

您迄今为止使用的大多数程序都会将其结果发送到标准输出流 STDOUT，该流通常“连接”到您的控制台。只要您在控制台（屏幕）上看到打印的内容，很可能它是通过 STDOUT 流发送的。

让我们尝试一下将 STDOUT 重定向到文件。

## 重定向到文件：>

要将输出重定向到文件，您使用大于号（>）并提供一个接收输出的文件名：

```
[alberto@digital alberto]$ ls -l > /tmp/listing
[alberto@digital alberto]$ cat /tmp/listing
total 2
-rw-rw-r-- 1 alberto alberto 388 Jul 29 19:03 Xrootenv.0
-rw-rw-r-- 1 alberto alberto 0 Aug 5 20:16 file
drwxrwxr-x 2 alberto groupfil 1024 Aug 4 22:13 groupfiles
```

在这个例子中我就是这样做的。我要求列出我的文件，但不是将列表显示在屏幕上，而是将 ls 命令的输出重定向到文件 /tmp/listing。为了证明它有效，我随后使用您在第 12 章“Shell 上的文件操作”中学习过的 cat 命令将 /tmp/listing 文件的内容发送到屏幕。这种技术对于创建目录中文件的列表很有用。

注意：安全第一！避免文件被覆盖：noclobber
重定向流有一个危险的副作用：它会杀死文件。在将输出重定向到文件时，如果文件不存在，Linux 会自动创建它。这种好处也带来了一个问题。如果文件已经存在会怎样？现有文件会被自动覆盖。这意味着 shell 会用新数据替换现有文件的数据——无需提示甚至通知您！

大多数 shell 都有设置 noclobber 变量的能力。此变量告诉 shell 拒绝会导致文件被销毁的重定向，并拒绝在文件不存在时追加到文件。

在处理 shell 时启用此功能是一个好主意，因为它使 shell 产生您未打算的副作用的可能性降低。

要在 bash shell 中启用 noclobber，键入以下内容：

```
noclobber=1
```

如果您使用的是不同的 shell，例如 C shell，您可能想尝试以下操作：

```
set noclobber=1
```

要测试命令是否生效，键入以下内容：

```
[alberto@digital alberto]$ noclobber=1
[alberto@digital alberto]$ touch file
[alberto@digital alberto]$ date > file
bash: file: Cannot clobber existing file
```

如果您收到相同的错误，则 noclobber 已正确设置。我尝试将 date 命令的输出重定向到 file。由于 file 已存在，这种重定向会导致 file 的内容被 date 打印的内容替换。当您在环境中定义了 noclobber 时，不允许执行此类操作。 （date 命令在第 17 章“命令工具箱：有用的 Shell 命令和快捷方式”中介绍。）

现在您知道了重定向，让我向您展示一个不错的技巧：让我们使用 cat 命令作为最小文本编辑器。我们可以通过发出 cat 命令然后将输出重定向到文件来实现，如下所示：

```
[alberto@digital alberto]$ cat > /tmp/message.txt
This is a test. Until I type a Ctrl+D, I can type all that I want.
I can even enter new lines.

-- Alberto
[alberto@digital alberto]$ cat /tmp/message.txt
This is a test. Until I type a Ctrl+d, I can type all that I want.
I can even enter new lines.

-- Alberto
[alberto@digital alberto]$
```

使用重定向，您可以将 cat 用作简单的编辑器。您可以编辑正在处理的当前行，因为 shell 不会在您按 Enter 之前捕获字符。要完成输入文本，只需按 Ctrl+D 即可。

## 追加文件：>>

重定向非常有用，但有时您不想替换文件的先前内容。相反，您可能想要在文件末尾添加信息。也许您想维护一个您最喜欢的网站列表。在这种情况下，添加新条目不应替换整个文件，而应对其进行扩充。

而不是使用单个 >，您使用 >> 来告诉 shell 追加新输出而不是覆盖。如果文件不存在，它将被创建，如下所示：

```
[alberto@digital alberto]$ cat > /tmp/websites
www.caldera.com
www.redhat.com
[alberto@digital alberto]$ cat >> /tmp/websites
www.mcp.com
[alberto@digital alberto]$ cat /tmp/websites
www.caldera.com
```





## 《Linux 完全傻瓜指南：让 Shell 发光发热》

www.redhat.com
www.mcp.com

为什么我不能对第一个 cat 使用 append (>>)？因为我启用了 noclobber 功能，>> 命令会导致错误。当 noclobber 设置时，追加到不存在的文件会产生错误。 （另一种选择是在使用 cat 之前发出 touch /tmp/websites。）

Previous Table of Contents Next

To access the contents, click the chapter and section titles.

## 《Linux 完全傻瓜指南》

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## STDERR

标准错误流，或 STDERR，是错误消息发送到的地方。随着你在 shell 上输入更复杂的命令，你可能希望将诊断或警告消息发送到日志文件。将错误消息重定向到新文件在调试 shell 脚本时尤其有用。

### Redirecting Errors

默认情况下，STDERR 和 STDOUT 都指向你的控制台，以便你可以看到诊断消息。当你重定向 STDOUT 时，STDERR 仍指向你的控制台，任何错误仍会打印在那里。要重定向错误，你需要指定一个文件号。

在 shell 中，输入、输出和错误流有分配的文件号：STDOUT 为 0，STDIN 为 1，STDERR 为 2。你可以组合文件号和重定向操作符。要将错误重定向到其他位置，你可以这样指定重定向：

```
command > outputfile 2> errorfile
```

打印到标准错误流 STDERR 的消息将进入 errorfile，而标准输出到 STDOUT 将重定向 outputfile。

例如，假设你想创建一个系统中所有文件的列表。根据你的用户 ID，你可能无权进入某些目录。以下命令行将权限访问错误重定向到不同的文件，同时将好的输出捕获到单独的文件中：

```
ls -R / > filelist.txt 2> error.txt
```

### Command Groups and Redirection

如果你想重定向多个命令的输出，似乎合理地认为你可以使用这样的命令：

```
pwd; cd ..; pwd; ls -l > /tmp/listing
```

然而，该命令行只重定向最后一个命令的输出。要重定向所有命令的输出，你需要创建一个命令组并重定向整个组的标准输出：

```
(pwd; cd ..; pwd; ls -l) > /tmp/listing
```

这会将每个程序的输出依次放入 /tmp/listing 文件中。

### Pipes: One Program’s Output Is Another’s Input

Shell 的真正威力在输出从一个程序变成另一个程序的输入时显现出来...其输出然后又成为另一个程序的输入，等等。你可以在一系列有用的信息中互连多个程序的输入和输出。此时，你可能会设想一种使用一系列输入和输出重定向命令的方案，通过临时文件传递信息。

但以更直接的方式，你可以用管道互连程序。管道非常有用：它们允许你使用一个程序的输出流作为另一个程序的输入流，而无需临时文件。

例如，如果你想列出当前登录系统的所有用户，可以使用 who 命令。who 命令按每行一个用户显示每个活动用户的信息。如果你只想知道系统上有多少用户，但不需要 who 提供的所有额外信息，你需要使用一些技巧。UNIX 有一个名为 wc 的命令，可以计算文件包含的单词数、行数和字符数。知道 who 输出每行一个用户的信息，你很快意识到你希望 wc 统计 who 显示的行数。你可以通过管道将 who 和 wc 连接起来实现：

```
[alberto@digital alberto]$ who | wc
-1
1
```

正如你所见，who 和 wc 命令可以通过连接竖线 (|) 进行管道。你可以连接任意多的程序。然而，鉴于我们有限的命令词汇，目前我们能做的还不多。

### Check This Out: Throwing unwanted output away

有时你不想在显示器上看到程序的输出，但你也不想将其发送到文件。也许你根本就不想要它。例如，在列出系统中的所有文件时：

```
ls -R / > filelist.txt >
error.txt
```

你知道这个命令将计算机中所有文件的列表发送到 filelist.txt，并将其遇到的访问错误发送到 error.txt。如果你只想保存或知道错误，有什么办法可以在命令运行时丢弃长长的文件列表吗？

UNIX 计算机在 /dev 目录下都有一个特殊文件，称为 /dev/null，也 commonly 称为位桶。发送到 /dev/null 的任何数据流都会立即被丢弃。要丢弃文件列表并只保留错误，你需要输入：

```
ls -R / > /dev/null 2>
error.txt
```

错误仍会保存在 error.txt 中，但现在你不必处理长长的文件列表。

管道与 ls 命令结合使用是一种常见用法。如果你列出包含许多文件的目录，例如 /dev 目录，输出会比你能看到的速度更快地滚动过去。你认为解决方案是什么？

如果你想到在 ls 和分页器如 less 之间建立管道，你就对了！列出 /dev 目录的命令是：

```
ls -l /dev | less
```

To access the contents, click the chapter and section titles.

## 《Linux 完全傻瓜指南》

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Getting the Needed Input: Input Redirection

你可以以与重定向输出相同的方式重定向输入。当程序的输入流从文件重定向时，程序使用文件中包含的字符，就好像你已在键盘上输入它们一样。

输入重定向最好用示例来说明。假设你的工作是准备备忘录以便传阅。每次你的老板告诉你备忘录准备好处理时，你都会执行一系列复杂的任务。首先，你将文件 /incoming/memo.txt 加载到 vi 中。然后，你删除包含一些控制信息的前十行文本，并保存文件。最后，你将文件复制到 /outgoing/memo.txt，你的老板在那里检索它并发送给其他人。有没有更简单的方法来做这件事？

意识到你一次又一次使用相同的按键序列，你决定使用输入重定向简化你的任务。利用你在第 13 章“在 Shell 下的文本编辑”中学到的关于 vi 的知识，你创建一个名为 prepare.txt 的文本文件，其内容如下：

```
10dd
:w/outgoing/memo.txt
:q!
```

创建此文件后，你尝试使用以下命令向 shell 准备备忘录：

```
vi /incoming/memo.txt < prepare.txt
```

当你按 Enter 执行命令时，vi 响应：

```
Vim: Warning: Input is not from a terminal
```

这是在告诉你 vi 将其标准输入流从你创建的文件重定向。几分钟后，你的 shell 提示符返回。检查文件 /outgoing/memo.txt 后，你确认备忘录已正确处理。使用输入重定向，复杂任务变得更简单。

## Regular Expressions

虽然正则表达式是一个高级主题，但如果你理解它们，它们会非常有用。那么正则表达式到底是什么？它是一种模式定义，也称为通配符，可用于定义文本应是什么样并允许 shell 找到匹配项。你可以在 shell 提示符上使用正则表达式来选择与模式匹配的文件组，而无需显式键入每个文件的名称。

正则表达式，或 REGEXs，正如它们也被称为，被各种程序使用——包括你的 shell。有时用于表示模式的符号含义会略有变化，但总的来说，基本语法是相同的。

这里有一个你可能想用 REGEXs 做的事情的例子：假设你有一个包含四个文件 file1.txt、file2.txt、file3.txt 和 info.txt 的目录，你想将它们移动到另一个目录。你会怎么做？

你可以执行此命令：

```
mv file1.txt file2.txt file3.txt info.txt ../somedirectory
```

毫无疑问，该命令会做你想要的，但这不是你想要经常输入的东西，尤其是如果你有 400 个文件而不是只有四个！正则表达式可以用来解决这类问题。不是输入一个庞大的命令，你可以输入：

```
mv * ../somedirectory
```

看起来更容易，不是吗？

星号，或星，是一组称为元字符中的特殊字符。星号定义一种匹配任何内容的模式。让我们看看元字符以及如何使用它们。

## Match Anything: *

星号匹配任何字符序列。这就是我可以说 mv * 来移动所有文件的原因。你可以在其他字母之间放置星号，以便它匹配可能包含其他字符的单词。参见表 14.1，了解使用星号的示例。

Table 14.1 Examples of Using the Star

| Examples | Description |
|---|---|



| *.txt | 匹配所有以 .txt 结尾的文件 |
| file* | 匹配所有以单词 file 开头的文件 |
| file*.txt | 匹配所有以单词 file 开头并以 .txt 结尾的文件 |

## Match Any Letter: ?

星号非常强大，无可否认。有时，事实上它太强大了。因为它可以代表任意数量的字符，它可能会匹配你不想匹配的内容。幸运的是，有一个更克制的元字符：? 将精确匹配一个字母，无论该位置的字符是什么。但是，如果你指定的位置没有字母，就不会匹配。参见表 14.2 中的示例。

## Table 14.2 Examples of Using the Question Mark

| Example | Description |
| file?.txt | 匹配所有以 file 开头，其后跟一个字符并以 .txt 结尾的文件 |
| ? | 匹配所有名称为一个字母的文件 |
| ?? | 匹配所有名称为两个字母的文件 |

## Match in a Range: []

有时你想要匹配多种选项。假设你想使用元字符来查找 file1.txt 和 file2.txt 但不查找 file3.txt。在这种情况下，你需要提供一组用括号括起来的选项，像这样：

```
file[12].txt
```

此模式将匹配 file1.txt 和 file2.txt——其他文件不会匹配。

如果你想查找连续的字符范围——比如你想匹配 0 到 5 的数字——你可以将它们指定为 [0–5] 而不是 [012345]。

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

## Negating a Range: !

有时指定你不想匹配的内容更容易。例如，如果你有名为 f11、f12、f13、f14 和 f15 的文件，并且你只想移动 f12-f15，你可以像我在这里做的那样指定范围。但使用 f11[!1] 指定你不想的文件可能更容易。在这种情况下，除了 f11 之外的每个文件都会被匹配。

## Command History

每当你在 shell 上输入命令时，shell 都会在称为历史列表的内容中记住它。你可以通过在 bash 提示符下输入 history 来查看历史记录。所有你输入的命令列表将被列出。每个命令都有一个与其关联的编号。

你可以“回收”历史记录中出现的命令，以避免重新输入它们。要重新执行出现在命令历史记录中的命令，只需输入感叹号 (!) 后跟你想要重新执行的命令的编号：

```
[alberto@digital alberto]$ !138
```

你输入的最后一个命令是特殊的。如果你想重复它，只需输入两个感叹号 (!!)。例如，你可以输入：

```
[alberto@digital alberto]$ !!
```

你可以通过使用键盘上的向上箭头向上浏览命令历史记录。这样会将命令放在你的提示符上，以便你在重新执行之前有机会编辑它。

你的历史记录保存多少个命令取决于 HISTSIZE 环境变量的设置。默认情况下，它设置为记住你最后 100 个命令。

## Jobs: Working on Multiple Things Using a Shell

某些命令行作业完成需要一段时间。例如，命令 ls -R / > filelist.txt 2> error.txt 在完成之前可能需要几分钟。如果有很多文件并且正在列出多个网络驱动器，预计它会运行半个小时左右。

由于 Linux 是多任务的，你可能希望在命令运行时做其他事情。你可以通过并发运行命令或在后台运行命令非常轻松地做到这一点。要在后台执行相同的命令，输入以下内容：

```
ls -R / >filelist.txt 2>error.txt &
```

关键是命令行的末尾的与号 (&)。这告诉 shell 在后台运行作业。发出命令后，你会看到如下内容：

```
[alberto@digital alberto]$ ls -R / > filelist.txt 2> error.txt &
[1] 872
[alberto@digital alberto]$
```

作业开始，你的命令行返回。方括号中的数字是分配给你的命令的作业编号或进程 ID。872 是系统范围进程列表中作业的进程 ID。作业的进程 ID 在你需要终止作业时很有用（参见第 22 章“系统监控：关注你的系统”中的“终止进程：kill”）。作业比 872 的进程 ID 更容易记住。当引用作业编号时，始终在前面加上百分号 (%) 符号。两者都为你提供了一种控制命令并将其返回前台的方法。当作业完成后，你会看到如下行：

```
[1]-  Done              ls -R / >filelist.txt 2>errors.txt
```

这意味着你的作业已完成运行。请注意，产生大量显示输出的程序不应在后台运行，除非输出被重定向。否则，你的命令提示符将难以使用，因为来自后台命令的输出会在你输入时继续出现！

一些程序需要交互式输入，所以偶尔你会看到这个：

```
[1]+  Stopped (tty output)    telnet localhost
```

这意味着作业需要输入，并已暂停等待你的按键。要将作业带回前台并输入所需的按键，请使用 fg 命令：

```
[alberto@digital alberto]$ fg %1
```

这会将作业编号一 (%1) 带回前台。请注意，作业编号前有一个百分号 (%)。

要列出从当前 shell 启动的所有作业，请使用 jobs 命令，如下所示：

```
[alberto@digital alberto]$ jobs
[1]+  Stopped (tty output)    telnet localhost
```

## Suspending a Job

你可以通过按 Ctrl+Z 来暂停在前台运行的进程。这会使进程进入睡眠状态：

```
[alberto@digital alberto]$ ls -R / > filelist.txt 2> errors.txt

[1]+  Stopped                ls -R / >filelist.txt 2>errors.txt
[alberto@digital alberto]$ bg %1
```

```
[1]+ ls -R / >filelist.txt 2>errors.txt &
```

在此列表中，我在前台启动了一个冗长的进程。然后我通过按 Ctrl+Z 将其置于睡眠状态（停止它），并使用 bg %1 在后台将其恢复。bg 与 fg 命令相反。

## Killing a Job

要终止当前前台进程，你可以发出 Ctrl+C。这将终止进程。要终止在后台运行的作业，你可以使用 kill 命令，后跟其作业编号或其进程 ID：

```
[alberto@digital alberto]$ kill %1
[alberto@digital alberto]$ kill 872
```

正如你所见，shell 既强大又复杂。即使我们只触及了它的皮毛，你所知道的知识也能帮助你完成大量工作！

## SPIDER KILLER

## spider catcher

HOME ACCOUNT INFO SUBSCRIBE LOGIN SEARCH MY ITKNOWLEDGE FAQ SITEMAP CONTACT US

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)

Author(s): Manuel Ricart

ISBN: 078971826x

Publication Date: 12/22/98

Bookmark It

Search this book:

Previous Table of Contents Next

## Chapter 15
Help Please

## In This Chapter

- Accessing the UNIX Manual Pages
- Searching for Help by Keyword
- The Whatis Database
- Getting Online Help
- Finding Your Answer with HOWTO Documents
- The Linux Documentation Project (LDP)
- Reading Info Pages

到目前为止，你一直依赖这本书来获取有关 Linux 的信息。讨论的命令只是可用命令的一小部分。这本书没有解释如何配置或使用你最终想要在系统上运行的许多东西；为此我需要另外 400 页。

在你绝望之前，请记住，这本书旨在让你快速掌握与 Linux 和 UNIX 相关的许多基本主题。为了让你获得全面的理解，你将不得不通过额外的来源补充你在这里找到的信息。其中一些来源已在你的计算机中；其他来源可从其他书籍或通过互联网免费获得的资源中获得。

在本章中，你将对可以利用的各种资源进行简短的巡视，以掌握 Linux。这将使你能够自行查找和解决问题。通过阅读和根据需要进行试验，你将学到很多东西。

Linux 有趣的一点是它文档齐全。其他操作系统（OS）为你提供有关系统某些方面的详细信息的，而你很快就会意识到 Linux 提供了关于其中几乎所有已安装内容的丰富信息。这主要是由于 Linux 的开放性质。在一个工具由分散的程序员集合添加的世界中，


唯一能带来秩序的方式就是通过文档。Linux 有大量文档——如果你知道去哪里找的话。

Linux 在类 Unix 系统中算是相当“标准”的 Unix。有几本通用的 Unix 书籍可以帮助你获得更深入的知识和更高级的主题。本章末尾列出了推荐阅读书目。此外，如果你能访问互联网，还有几个有价值的信息来源可以利用，包括邮件列表和 Usenet 新闻组。正确使用它们将帮助你获得所需的答案。

## UNIX 手册页

你获取信息的第一个地方是 UNIX man 手册页。如果你在使用某个命令或其他系统工具时遇到问题，那么该工具很可能附带了以 man 手册页形式提供的文档。man 手册页是 man 程序使用的标准 UNIX 在线文档格式。

UNIX 手册正慢慢变得像恐龙一样，因为已有更好的程序来阅读文档。UNIX 手册唯一积极的一点是它存在于所有 Unix 系统中，无论是 Linux 还是其他。因此，学会正确使用它很重要。

要阅读 UNIX 手册，你使用 man 命令，并作为参数给出你想了解的程序名称。以下示例显示了当你请求有关 bash shell 的信息时 man 输出的一部分：

```
[alberto@digital alberto]$ man bash
BASH(1)                                                                 BASH(1)

NAME
    bash - GNU Bourne-Again Shell

SYNOPSIS
    bash [options] [file]

COPYRIGHT
    Bash is Copyright (c) 1989, 1991 by the Free Software Foundation, Inc.

DESCRIPTION
    Bash is an sh-compatible command language interpreter that executes commands read from the standard input or from a file. Bash also incorporates useful features from the Korn and C shells (ksh and csh).

    Bash is ultimately intended to be a conformant implementation of the IEEE Posix Shell and Tools specification (IEEE Working Group 1003.2).
:
```

如你所见，man 命令提供了在线手册的格式化版本。列表末尾的冒号 (:) 表示还有更多信息。Man 信息会通过一个名为 less 的分页程序传递。你可能记得 less 会一次显示一屏信息。以下是你可以用 less 做的事情：

- 按空格键查看下一页。
- 输入 /word 其中 word 是你要查找的词。这将在文档中搜索你指定的词，并在该词的首次出现处停止分页。
- 输入 q 返回到命令提示符。

尝试使用 man 命令阅读有关 man 命令本身的一些信息（man man）。

## Linux 完全傻瓜指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 搜索工具：apropos

如果你知道感兴趣的命令名称，Man 非常有用。你可以执行 man commandname，然后就可以开始了。但如果不知道要找的命令名称怎么办？

这时 apropos 命令就派上用场了：它允许你按关键字搜索。结果，它会显示可能与你的问题相关的文档列表。

太好了！只有一个小问题：apropos 搜索的数据库，即 whatis 数据库，在你创建它之前并不存在。（你将在“构建 whatis 数据库：makewhatis”一节中学习如何做到这一点。）构建完成后，你就可以用 apropos 命令查询数据库，例如查找与你的磁带驱动器相关的命令：

```
[alberto@digital alberto]$ apropos tape
mt (1)              - control magnetic tape drive operation
smtbar (1)          - shell script for backing up SMB shares directly to UNIX tape drive
st (4)              - SCSI tape device
```

从这些信息中，你知道至少有三页手册（使用 man 命令）与你的磁带驱动器相关。你看到的括号中的数字表示手册章节。

UNIX 手册分为几个章节。每个章节按主题组织。表 15.1 列出了这些章节。

### 表 15.1 Linux 下 UNIX 手册页的章节

| 章节编号 | 主题 |
|---|---|
| 1 | 用户命令、程序和应用程序 |
| 2 | 系统调用和内核错误代码 |
| 3 | 库函数调用 |
| 4 | 特殊文件（/dev 目录中的内容） |
| 5 | 标准文件格式 |
| 6 | 游戏和其他有趣类型的程序 |
| 7 | 各种不属于其他地方的东西 |

如果你未指定章节，man 会先搜索涵盖命令的章节；通常顺序为第 1、8 和 6 章。

一个命令可能在手册的多个章节中都有描述。要查看特定章节的文档，请这样指定 man 命令：

```
man section command
```

在前面的示例中，man 命令被列了两次：第 1 章和第 7 章。要阅读第 7 章的信息，输入此命令：

```
man 7 man
```

## 获取简要命令描述：whatis

有时你不想读五段 UNIX 手册的文字只为弄清某个命令的作用。在这种情况下，whatis 工具也可以用来获取命令的简要描述。要以此模式运行，你需要提供工具名称作为参数。

试试这个：构建 whatis 数据库：makewhatis
要构建 whatis 数据库，你需要使用 makewhatis 命令。要开始构建数据库，输入此命令：

```
/usr/sbin/makewhatis
```

请注意，你必须是 root（你也可以是 su 并执行该命令），否则该程序无法正常工作。几分钟后，数据库将被构建。如果你的计算机较旧，此操作可能需要一段时间。

whatis 会打印出命令做什么的一行描述。我发现 whatis 是一个很棒的探索工具。如果你进入 /sbin 等程序目录，可以通过发出以下命令快速了解那里的命令的作用：

```
cd directory; whatis *
```

这会带你进入你指定的 directory 目录，并在该目录中找到的所有文件上执行 whatis。* 是一个正则表达式，指定该目录中找到的所有文件：

```
[alberto@localhost alberto]$ cd /sbin; whatis *
adjtimex (2)          - tune kernel clock
adjtimex (8)          - display or set the kernel time variables
arp (8)               - manipulate the system ARP cache
(And more...)
```

## 搜索标准位置：whereis

有时你需要的帮助是定位你要找的文件或程序。如前所述，你的 shell 通过查找环境变量来找到命令。当你发出命令名称时，PATH 环境变量中列出的目录会被搜索以匹配命令。如果找到，命令将被执行；否则，你会得到令人讨厌的“command not found”响应。

由于某些存放工具的目录未包含在默认用户路径中，你的 shell 将看不到它们。在这种情况下，你可以使用 whereis 工具来找到你要使用的工具的实际路径。

注意：
有关正则表达式的更多信息，请参阅第 14 章“让 Shell 工作”。

whereis 不仅能定位二进制文件，还能定位你提供的名称的源代码和手册页。命令格式如下：

```
whereis command
```

在以下示例中，我搜索 passwd 命令：

```
[alberto@digital alberto]$ whereis passwd
passwd: /usr/bin/passwd /etc/passwd /etc/passwd.OLD
/usr/man/man1/passwd.1 /usr/man/man5/passwd.5
```

## 内置命令信息

大多数最新命令都在程序内部存储了基本的使用信息。在 Linux 下，你始终可以尝试对命令名称加上 --help 或 -h 参数。通常列出的信息会超过一屏，因此请记住将输出通过管道传递给 less：

```
commandname --help | less
```

如果你使用的命令是一个“智能”的 UNIX 命令，即使它不理解 --help 标志，它也会以合理的方式响应。通常，当程序遇到未知参数时，它会退回到输出其使用信息。使用信息会告诉你命令的基本格式以及它支持的标志。显然，这并不会告诉你程序做什么（除非你已经知道），但总比没有信息好。如果 man 失败了，你可能需要上网查找一些信息。我发现用 Yahoo 等搜索引擎搜索命令名称通常能把我引向正确的方向。




要访问内容，请单击章节和节标题。

## Linux完全傻瓜指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

上一页 目录 下一页

## 通过 /usr/doc 在线帮助

Linux 将许多文档和补充信息文件存储在 /usr/doc 中。该目录布满了按所属程序或工具命名的系列目录。在每个目录中，你通常会找到一个 README 文件，其中包含有关该程序的最后一刻信息以及有关该程序功能或问题的常见问题解答（FAQs）。这些信息除了你可能通过 man 或其他文档阅读器找到的任何文档之外。

/usr/doc 目录中的在线帮助还包含计算机上最重要的通用 Linux 信息：

- Linux 安装和入门指南—这是 Linux 文档项目为 Linux 初学者创建的“入门”手册。Linux 文档项目是一项旨在为 Linux 计算机创建完整的在线手册集的计划。
- Linux 系统管理员指南—该手册关于 UNIX 系统管理，由 Linux 文档项目创建。
- Linux 网络管理员指南—该手册描述了如何在网络环境中使用 Linux 以及如何管理大型基于 Linux 的网络。该手册也是由 Linux 文档项目创建的。
- Linux 文档项目作者创建的其他功能文本。

• HOWTO 文档—这些是关于如何完成某些高级任务的功能指南，例如配置软件或某些有趣的网络工具。

这些文档位于 /usr/doc/html 中，但它们以 HTML 格式存储，这意味着你不想用 less 等分页器来阅读它们。你可以通过两种方式访问它们，具体取决于你是在 KDE（X）会话中还是在控制台中。在 KDE 会话中，启动 Netscape Navigator 以查看在线手册。实际 URL 是 file:/usr/doc/html/index.html；按原样提供时，Navigator 配置为默认打开指向此页面的链接。如果你正在从控制台工作，通过在命令行输入“lynx”启动基于文本的 Lynx 浏览器。Lynx 也配置为默认转到此页面。

除了使用 Navigator 和 Lynx，如果你在 KDE 中，你可以将 URL 输入到 KFM 的 URL 位置字段中，KFM 将为你显示文档。

## 更多关于 HOWTO 文档

大多数标准 Linux 发行版都包含 HOWTO 文档。这些文档解释了如何做许多事情，例如如何在你的机器上设置 DNS 服务器以及如何配置声卡。其中大多数文档由其他用户或工具的开发人员编写，作为对 Linux 社区的帮助。

其中许多文档是无价的。然而，大多数文档太长（平均文档长约 60 页！）并且往往包含大量外围信息。这可能会给 Linux 新手带来一些困难；他们的背景水平与黑客不同。但这就是你得到的。在一个免费的操作系统中，很难找到一位优秀的技术作家，能够从你需要知道的内容中提炼出你想要知道的内容。

OpenLinux 1.3 系统上的 HOWTO 文档可以通过访问我们在上一节中讨论的 /usr/doc 中的在线文档 URL 来找到。

## Mini HOWTOs

迷你 HOWTO 在精神上与 HOWTO 文档相似；然而，迷你 HOWTO 往往更自由形式且更短。HOWTO 文档遵循某些格式标准，而这些标准并不约束迷你 HOWTO。

迷你 HOWTO 可以在你的 OpenLinux 1.3 计算机上的 HOWTO 索引页面上找到，并在标题中的某个位置以“Mini”标识。

## LDP—Linux 文档项目

LDP 可能是关于 Linux 的最有用和最有帮助的在线信息。LDP 的目标是为 Linux 创建可靠的文档，涵盖安装、内核开发、内核信息、网络管理、系统管理和用户指南。LDP 的作者确保随 Linux 分发的文档准确且最新。

正如我们已经讨论过的，LDP 开发的一些手册可在你的系统上在线获得。其他则可通过互联网获得。如果你有互联网访问权限，你可以在 http://sunsite.unc.edu/LDP 查看最新文档。

除了提供在线手册和 HOWTO 文档外，LDP 还负责维护许多关于 Linux 的常见问题解答（FAQ）文档。这些可以在互联网上的 LDP 主页上找到。

## 阅读压缩文档：zless

偶尔，你可能会在 /usr/doc 或 Linux 计算机上的其他帮助区域遇到压缩文档。压缩文档可以通过以下文件名扩展名来识别：.gz、.z 或 .Z。

当你在 Linux 计算机上遇到压缩文档时，你需要先将其解压缩后再阅读，或使用一种可以窥视压缩文档的特殊实用程序。

zless 是一个工具，允许你使用 less 分页器查看压缩文本文件（文件名以 .gz、.z 或 .Z 结尾）。如果 zless 命令不可用，你可以通过使用 zcat 和 less 管道来实现相同效果：

```
zcat filename | less
```

要访问内容，请单击章节和节标题。

## Linux完全傻瓜指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

上一页 目录 下一页

## Info 页面

越来越多的开发人员开始使用 GNU 的 info 来编写文档。GNU info 系统使用超文本来关联不同的信息片段。info 的目标是通过提供在文档的不同部分之间跳转的方式，使阅读文档页面变得更容易。

这个概念类似于使用 Web 浏览器。要阅读文档，你使用 info 命令，后跟你感兴趣的工具的名称。如果你没有提供工具名称，info 将向你显示它所知道的所有命令的列表以及 info 文档本身的一些入口点。以下图示显示了 info 中的一个屏幕。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_170_0.png)

info 程序。

在 info 中移动的基本命令列在表 15.2 中。

## 表 15.2 Info 命令

| Key | Description |
| --- | ----------- |
| Space | Page down |
| Backspace | Page up |
| b | Beginning of the page |
| ? | Help |
| n | Next node |
| u | Previous node |
| l | Last node |
| u | Up |
| m | Menu (type menu name or ? for a list of options) |
| Ctrl+g | Cancel current operation (or menu) |
| f | Cross reference (type cross reference name or ? for a list of options) |
| d | Show a directory of all the documents info knows about |

info 文档中的每个页面都称为一个节点。节点可以包含菜单和交叉引用。菜单是同一文档内的相关节点。交叉引用通常位于不同文档中的节点。

学习如何使用 info 的最简单方法是完成其交互式教程。要访问教程，在命令提示符下输入 info，然后键入 h 以遵循说明。在 Emacs 中，你可以通过键入 Ctrl+h i 进入 info。

## Usenet：互联网新闻组

如果你可以访问互联网和新闻组，你可以在许多地方找到有关 Linux 的信息。组是按主题组织的。世界各地的人们向他们感兴趣的组发布问题和答案。

有数千个新闻组涵盖所有主题和兴趣。但在像 OpenLinux 1.3 随附的 Netscape Communicator 的 Colabra 这样优秀的阅读器的帮助下，你可以浏览多个帖子，直到找到你想要的内容。（执行 man -k news 以查找系统上安装的控制台功能新闻工具。）

一些新闻组是经过审核的。经过审核的组会由组的维护者审查帖子，然后决定你的帖子是否值得分发。

Usenet 新闻组充满了噪音，因为很多用户在没有自己研究问题的情况下盲目发布。如果你已经查看了本章中提到的所有资源并且仍然没有问题的解决方案，这可能是一个有效的问题。

发布问题时，始终建议说明你的软件的版本和发行版，然后说明你遇到问题的工具（包括版本信息）。有时不同的软件版本可以决定对你的问题的正确答案是什么。简明扼要但描述性强，并且每条消息只问一个问题。

一些 Linux 组如下：

- comp.os.linux.advocacy—一个专门用于争论 Linux 比其他操作系统更好的新闻组。





- `comp.os.linux.announce`—这是一个经过审核的组，用于发布关于 Linux 开发、错误修复、软件发布等公告。这可能是所有组中最“信息性”的，关于 Linux 世界正在发生的事情。
- `comp.os.linux.development.apps`—该组面向有兴趣将应用程序移植到 Linux 的程序员。
- `comp.os.linux.development.system`—该组面向有兴趣开发内核和系统软件的程序员。
- `comp.os.linux.hardware`—这个组用于硬件问题、支持，以及为什么 Linux 在硬件 x 上无法工作。
- `comp.os.linux.misc`—这是一个用于所有无法归入其他地方的主题的组。
- `comp.os.linux.networking`—该组关于网络和网络硬件。
- `comp.os.linux.setup`—这个组用于安装 Linux、如何让服务 X 运行等。
- `comp.os.linux.x`—该组专门用于在 Linux 下安装、配置和运行 X。
- `alt.os.linux.caldera`—该组用于 Caldera OpenLinux 特定问题。

跨贴（将同一个问题发送到多个组）是不好的。只在与你的查询主题具体相关的组中提问：你更有可能收到答复。

## 有用的书籍

最后，Linux 和 UNIX 有大量商业文献。质量和信息的多样性因书而异。你选择的书籍取决于你想用 UNIX 做什么。找到适合你需求的书籍的最佳方法是访问在线书店，如 Amazon.com、 BarnesAndNoble.com 或 Borders.com 并搜索“linux”和“unix”这两个词。

要访问内容，请单击章节和节标题。

## Linux 完全 idiot's Guide

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 第 16 章

## 权限：保护和共享你的工作

## 本章内容

- 处理权限
- 用户类别
- 按数字分配权限
- 按符号分配权限

如你所知，Linux 是一个多用户系统。这意味着许多人可以同时访问并在同一台计算机上工作。正因为如此，需要提供一种机制，允许用户根据需要共享和保护文件，以便协作和安全正常工作。实现这一点的机制是内置于文件系统中的权限机制。

本章解释了权限以及与其它用户共享文件的策略。如果你的系统有多于一个用户，你可能需要保护你的文件。如果你的系统是一台仅你有权访问的独立机器，本章提供了信息性概述。

## 权限是如何工作的？

当你向系统添加一个用户时，会发生几件事，包括以下内容：

- 为用户的文件创建一个主目录
- 系统在其中一个数据库上添加条目，以便用户创建的文件被标记为由该用户拥有
- 用户被添加到至少一个默认用户组 添加用户和组的内容在第 17 章“用户、组和密码”中介绍。

所有这些步骤服务于一个目的：给你一个机制来防止私有或组拥有的文件被公开查看或使用。在 Linux 下，鉴于适当的硬件资源，你可以在一台机器上舒适地容纳数千名用户。我知道一个地方，两台小型的 Pentium 机器，配备 128MB RAM 和数 GB 存储，服务超过 400 名用户，外加 200 个不同的 Internet 服务——每个服务都在自己的虚拟域名下运行并为大量用户服务！（每台机器实际上可以处理全部负载再多，但出于安全原因，服务可从两台机器获得。）

现在想象一下 400 个陌生人翻阅你的文件！你有两个解决方案：

1. 不要保留或编写你不想让他人阅读的任何敏感材料——这是一种激进但非常安全的方法。
2. 利用 UNIX 权限机制来避免大多数不必要的窥探。

我们将探讨第二个选项。每个用户在账户创建时被分配一定的访问级别。访问级别由用户的组成员身份表示。系统的管理员（root）可以随时更改这些成员身份。当用户登录时，系统会将用户与特定的身份关联起来。利用此身份和文件权限系统，Linux 决定用户被允许做什么以及用户被允许读取或操作哪些文件。

在最基本层面上，权限系统实际上非常简单。系统中的每个文件都由恰好一个用户拥有并与恰好一个组相关。每个文件还具有九个开关的集合，控制谁可以读取、写入或执行该文件。（还有更多开关，但我将在下一节“有效用户 ID”中讨论它们。）

对于给定的文件，任何用户都可能在以下一种或多种角色中：

- 所有者或用户角色：所讨论的用户是此文件的拥有者（通常是其创建者）。所有者可以根据自己的意愿分配文件的权限。
- 组角色：所讨论的用户是与文件相关的组的成员。组旨在帮助在多用户协作中控制对文件的访问。通过将文件与一组人关联，可以一次控制许多人的文件访问。任何用户可以属于任意数量的组，但一个文件一次只与一个组相关。
- 其他角色：此用户不是此文件的拥有者，也不是与此文件相关的组的成员。

对于 Linux 系统中的每个文件，存在三个权限“开关”对应于这三个角色（总共九个开关）：

- 读取（R）—此开关授予查看文件内容的权限。
- 写入（W）—此开关授予更改文件内容或删除文件的权限。
- 执行（X）—此开关授予将文件作为程序运行的权限。对于目录而言，这也意味着进入目录的权限。

默认情况下，即使没有有意分配，文件也会有一些权限设置。将权限视为如下图所示的表格非常有用。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_174_0.png)

勾选表示授予的权限，破折号表示缺乏此类权限。

因此根据表格，所有者被允许读取、写入和执行文件。

组成员仅被允许读取和执行权限。任何不是所有者或组成员的人都不能读取、写入或执行程序；如果所讨论的文件是目录，则此类用户也不能遍历它。

让我们看一个例子来演示权限通常如何表示。你可以使用带有 -l 选项的 ls 命令显示文件的权限信息：

```
[root@digital alberto]# ls -l
total 2
-rw-rw-r--  1 alberto alberto      388 Jul 29 19:03 readme.txt
drwxrwxr-x  4 alberto alberto     1024 Aug  2 14:39 stuff
```

Previous | Table of Contents | Next

Products | Contact Us | About Us | Privacy | Ad Info | Home

Use of this site is subject to certain Terms & Conditions, Copyright © 1996-2000 EarthWeb Inc.
All rights reserved. Reproduction whole or in part in any form or medium without express written permission of EarthWeb is prohibited.

要访问内容，请单击章节和节标题。

## Linux 完全 idiot's Guide

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

Previous Table of Contents Next

权限显示为每行开头的十个破折号和/或字母的序列。

- 第一个字符位置告诉你文件的类型。普通文件如 readme.txt 在此位置显示破折号（–）。目录如前例中的“stuff”显示 d。链接显示 l，而其它特殊文件——如设备、套接字和管道——分别显示 c 或 b、s 和 =。
- 接下来的九个位置代表九个权限开关。前三个开关适用于文件的所有者，中间三个适用于文件组的成员，最后三个适用于“其他”用户。每组三个开关包含一个读取开关、一个写入开关和一个执行开关，按此顺序。当开关打开（授予权限）时，会出现字母：r 表示读取，w 表示写入，x 表示执行。当开关关闭（拒绝权限）时，会出现破折号（–）。在上面的 readme.txt 中，你可以看到所有者有权读取和写入，组有权读取和写入，其他人只有读取权限。在上面的名为 stuff 的目录中，所有用户都有读取和执行权限（这意味着所有用户都可以 cd 进入该目录）。然而，只有所有者和组具有写入权限，并且只有他们被允许在 stuff 目录中创建文件。

## 有效用户 ID

对文件和进程的访问将取决于你的当前用户名和当前组成员身份。我说“当前”是因为在会话期间，你可以假设另一个用户的 id（即，如果你知道该用户的密码）。

要查看你的有效用户 id 和组成员身份列表，你可以使用 id 工具。id 命令打印有关你的当前用户名、当前组的信息和



你所属的所有组列表。此信息也可以使用 whoami 和 groups 命令获得。然而，id 命令提供的信息更多，并且也可以用于其他目的。

要查看你所属的组，在 shell 中，输入 id：

```
[alberto@digital alberto]$ id
uid=501(alberto) gid=501(alberto) groups=501(alberto)
```

正如你通过执行此命令所看到的，我的用户名 alberto 被分配了用户 ID（UID）501 和组 ID（GID）501。操作系统通过数字来跟踪你的用户名和组归属。这种系统更高效，并且可以跟踪大约 65,536 个不同的 UID！

以超级用户（root）运行相同的命令会得到不同的信息：

```
[root@digital alberto]# id
uid=0(root) gid=0(root) groups=0(root)
```

正如你所看到的，root 的 UID 和 GID 都是 0。任何 UNIX 系统上的 root 用户的 UID 都是 0，并且始终至少属于一个组，其 ID 也是 0。root 也可以属于更多组。

## 替代用户：su

在工作和配置软件时，通常需要成为 root 用户——或者其他任何用户。与其注销后再次以不同用户登录，更好的替代方案可能是使用 su 命令。此命令有效地将你当前的 UID 和 GID 替换为你要成为的用户的 UID 和 GID，并授予你 su 到该用户的所有权限。以下是一个示例：

```
[alberto@digital alberto]$ su root
Password:
[root@digital alberto]# cd
[root@digital /root]# exit
exit
[alberto@digital alberto]$
```

在此示例中，我执行了 su 命令。作为参数，我提供了我想要成为的用户名。在本例中我指定了 root；请注意，单独使用 su 默认假设为 "su root"。

请注意，su 将要求你要 su 进入的用户的密码。为了返回到我的常规用户账户，我执行了 exit 命令（你也可以按 Ctrl+D）。此操作终止了 root shell 并将我返回到原始会话。完成需要 su 的任务后，务必记得返回到你的用户账户。

## 当心 root 的权力！

Root 是一个特殊的管理员账户，授予对整个系统的不受限制的访问权限。当你需要执行系统管理类型的任务时，这种权力非常宝贵，但这不是你希望用于其他任何目的的账户。root 账户可以执行某些不可逆的操作，例如擦除磁盘上的所有文件或其他某种灾难性操作！

在你对 Linux 和 UNIX 有更多了解之前，我建议你不要使用 root 账户，除非绝对必要。示例包括添加软件或配置系统中的某些方面，这些方面 specifically 要求你以 root 身份登录。

## 更改组：newgrp

每当你创建文件时，你的默认组是分配给文件组所有权的组。如果你是多个组的成员，可以使用 newgrp 工具更改你的有效 GID。newgrp 工具类似于 su，因为你提供你想要作为会话默认使用的组的名称。如果你不是该组的成员，则不允许更改你的有效 GID。

## 特殊用户

你的 Linux 系统已经预先创建了几个账户。

其中许多账户（bin、adm、lp、sync、halt、mail 等）是为了程序或某些其他系统功能而存在的。这些所谓的伪用户账户对于系统能够在仍然维护权限机制的同时执行某些任务非常重要。

## 主目录

每个用户名都有自己的主目录。默认情况下，Linux 将主账户放在 /home 目录下。唯一明显的例外是伪用户的账户。（你不应尝试更改这些账户的位置。）

传统上，类 UNIX 操作系统并未开箱即用如此彻底地配置。相反，系统管理员必须自行明确组织主目录。然而，标准 Linux 系统将用户账户保存在 /home 中。

## 更改文件权限

如果你是文件的拥有者或超级用户，你可以更改文件上的权限。为此，你使用 chmod 命令。

chmod 命令提供了一种符号模式，在其中你可以添加或减去权限，以及一种数字模式，在其中你可以指定你想要的文件权限。在使用 chmod 命令之前，你需要知道如何使用其数字和符号模式。

## 按数字设置权限：4、2、1 和 0

权限可以设置为数字。虽然这种方法对初学者来说可能看起来有点复杂，但实际上并不复杂。首先，你只需要担心四个数字：

- 数字 4 指定读权限
- 数字 2 指定写权限
- 数字 1 指定执行权限
- 数字 0 指定没有任何权限

如果你想启用读和写权限，你将值相加：4+2=6，所以你分配数字 6。

如果你想启用读和执行权限，你再次将值相加：因为 4+1=5，所以你使用值 5。

如果你想启用读、写和执行，你将 4+2+1 相加得到 7，这是你应该分配的值。各个权限的值被设计成在各种组合中形成唯一值。

简单吗？我认为很简单。然而，可能使事情复杂化的一点是，你需要同时为所有三个角色指定权限：拥有者、组和其他人。为此，将这三个权限的序列串联起来。结果是一个称为模式的数字。

要给文件的拥有者和组读和写权限，但只给所有其他用户读权限，将模式指定为 664：拥有者为 (4+2)，组为 (4+2)，其他人为 (4)。

## 使用符号设置权限：u、g、o、r、w 和 x

有时使用符号设置权限很有用，因为它们允许你一次设置一个角色的权限或一次设置一个权限。例如，你可以在不知道文件拥有者或其他用户的权限的情况下授予文件组读权限。

为了使用符号设置权限，你必须记住与某些单词对应的字母：用户或拥有者 (u)、组 (g)、其他人 (o)、读 (r)、写 (w) 和执行 (x)。

基于符号的权限字符串遵循以下两种格式之一：

- `identity-permissions` 用于拒绝权限
- `identity+permissions` 用于授予权限

以下是一些示例权限字符串；其含义应该会变得越来越清晰。

## 表 16.1 使用符号授予权限

| string | Permissions | Granted to |
|---|---|---|
| ugo+rwx | read, write, execute | owner, group, and others |
| ug+w | write | owner and group |
| g+rx | read and execute | group |

## 表 16.2 使用符号拒绝权限

| string | Permissions | Denied to |
|---|---|---|
| ugo-rwx | read, write, execute | owner, group, and others |
| o-rw | read and write | others |
| go-x | execute | group and others |

请注意，字符串 "ugo" 可以用 "a" 代替，表示 "all"。例如，"ugo+w" 和 "a+w" 都授予每个人写权限。

## 使用 chmod 更改权限

要更改文件的权限，你取计算出的模式或所需的符号并使用 chmod 命令。语法是 chmod [options] mode filename [filename...]

让我们在计算机上试试。让我们创建以下内容：

- 两个普通文件，名为 fileone 和 filetwo
- 一个名为 adir 的目录
- 一个名为 filethree 的符号链接

```
[alberto@digital alberto]$ touch fileone filetwo
[alberto@digital alberto]$ mkdir adir
[alberto@digital alberto]$ ln -s fileone filethree
[alberto@digital alberto]$ ls -l
total 2
-rw-rw-r-- 1 alberto alberto 388 Jul 29 19:03 Xrootenv.0
drwxrwxr-x 2 alberto alberto 1024 Aug 4 18:05 adir
-rw-rw-r-- 1 alberto alberto 0 Aug 4 18:05 fileone
lrwxrwxrwx 1 alberto alberto 7 Aug 4 18:05 filethree -> fileone
-rw-rw-r-- 1 alberto alberto 0 Aug 4 18:05 filetwo
```

现在让我们将 filetwo 和 filethree 更改为模式 644。我们还将拒绝（移除）adir 的所有写权限。





```
[alberto@digital alberto]$ chmod 644 filetwo filethree
[alberto@digital alberto]$ chmod ugo-w adir
```

现在让我们列出结果：

```
[alberto@digital alberto]$ ls -l
total 2
-rw-rw-r-- 1 alberto alberto 388 Jul 29 19:03 Xrootenv.0
dr-xr-xr-x 2 alberto alberto 1024 Aug 4 18:05 adir
-rw-r--r-- 1 alberto alberto 0 Aug 4 18:05 fileone
lrwxrwxrwx 1 alberto alberto 7 Aug 4 18:05 filethree -> fileone
-rw-r--r-- 1 alberto alberto 0 Aug 4 18:05 filetwo
```

发生了什么？filetwo 和 adir 的权限按预期发生了变化，但 filethree 的模式保持不变。出现这种奇怪现象的原因是 chmod 不会更改符号链接的模式——符号链接的权限永远不会被使用。它所做的是更改链接指向的文件的模式——fileone！因此 fileone 和 filetwo 的模式为 644 (4+2) (4) (4)，即所有者可读写，组和其他用户只读。adir 的所有 w，即写开关都已关闭。

上一页 目录 下一页

## Linux 完全傻瓜指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

要访问内容，请点击章节和节标题。

## Setuid、Setgid 和 Sticky 位

除了“按数字设置权限：4、2、1 和 0”一节中描述的权限位之外，UNIX 还提供了另外三个用于其他目的的位。setuid 位将正在运行程序的用户 ID 设置为程序所有者的用户 ID。这样，程序就可以使用程序使用者本身不一定拥有的权限运行。程序在运行时有效地具有与文件所有者相同的用户 ID。类似地，setgid 位以程序所属组的组 ID 运行程序。这种分配允许程序访问文件和进程，而运行程序的用户通常无权访问。

在 Linux 下，setgid 位还有一个特殊用途。当设置在目录上时，它会设置添加到该目录的文件的组所有权。这样，即使特定用户的默认组与该组不同，它也会被分配给项目目录——确保在其中创建的文件可供组成员访问。

Sticky 位与目录结合使用以保护目录包含的文件，尽管它最初是为不同目的设计的。设置后，它只允许目录所有者、文件所有者或超级用户删除目录包含的文件。Sticky 位的存在就是像 /tmp 这样由许多用户共享的目录比使用标准权限设置时具有更多隐私的原因。

setuid、setgid 和 sticky 位的值分别为 4000、2000 和 1000，并使用 chmod 命令设置。要使用它们，只需将

搜索本书：

上一页 目录 下一页

文件模式添加到您想要的值（或组合）中。要使用符号模式授予或拒绝 setuid/setgid 或 sticky 权限，请使用 s 表示 setuid 和 setgid，使用 t 表示 sticky。

例如，如果目录的模式为 777（意味着所有用户都有 RWX 权限），您可以通过将其模式更改为 1777 来设置 sticky 位。要设置 setgid，您将把同一目录的模式更改为 2777。使用符号，设置文件的 suid 位，您将使用 "u+s"。要设置 setgid 位，请使用 "g+s"。要设置 sticky 位，请使用 "a+t。"

## 默认文件模式：umask

所有文件都是根据文件类型（普通文件或目录）以默认模式创建的。如果您可以以某种方式定义创建文件时想要的设置，那不是很酷吗？好吧，您可以！

此过程涉及使用 umask 命令。您提供给 umask 命令的数字与模式的数字类似，只是它们的位已被反转。这意味着它们的工作方式并不那么直接。不要问我为什么没有更不奇怪的方式设置这些位；这就是它的方式。

要查看当前的 umask，请在 shell 中输入 umask：

```
[alberto@digital alberto]$ umask
022
```

为了方便您，我提供了一个包含合理 umask 值的表格，您可以设置（见表 16.3）。如果表中没有您需要的数值，您可以使用 chmod 命令即时设置这些权限。（当 umask 命令需要太多思考时，我就是这么做的。）

### 表 16.3 常见 umask 值

| umask | User | Group | Other |
|---|---|---|---|
| 000 | rwx | rwx | rwx |
| 002 | rwx | rwx | r-x |
| 007 | rwx | rwx | --- |
| 022 | rwx | r-x | r-x |
| 037 | rwx | r-x | --- |
| 077 | rwx | --- | --- |

现在您只需输入 umask 命令，后跟您想要设置的值。从那时起，您在当前会话期间创建的所有文件都将具有这些属性。

私有组（见“组所有权和用户私有组”）。如果您的帐户有 UPG，默认 umask 为 002；否则为 022。

## 组所有权和用户私有组

有时您会想与不同用户在项目上协作。这种情况可能意味着您希望编辑他人创建的文件，他们也希望编辑您创建的文件。为了在保护工作不被其他用户访问的同时使这种协作工作，您需要使用组。

通常，为项目创建一个组，并将用户添加到该组。用于组协作的文件将放在系统中的“中性”目录中。该目录将允许组成员读取、写入和执行特权。为了确保在目录中创建的文件属于该组，将在目录上设置“Setuid、Setgid 和 Sticky 位”一节中提到的 setgid 位。（创建组在第 18 章“用户、组和密码”中讨论。）

这种方法唯一的问题是文件的权限将根据用户的 umask 设置，并且反过来取决于用户是否具有用户私有组（UPG）。

当使用 UPG 时，而不是用户属于通用组“users”，Linux 会在帐户添加时为用户创建一个 UPG。用户是（并且应该是）其自己组的唯一成员。这种排他性允许用户使用 002 的 umask，而不会损害任何个人文件的安全性。默认情况下，umask 为 002 允许文件所有者和与文件关联的组完全控制文件。在 UPG 的情况下，与文件关联的组也是所有者，因此是安全的。

如果未使用 UPG 机制，组成员将不得不系统地使用创建项目文件时使用的 umask。鉴于人性，结果是一系列文件只能由所有者编辑，要求所有者对文件执行 chmod 以允许其他组成员修改文件。UPG 机制为此问题提供了解决方案——因此它非常酷。

要访问内容，请点击章节和节标题。

## Linux 完全傻瓜指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 第 17 章
命令工具箱：有用的 Shell 命令和快捷方式

## 本章内容

- 用户实用程序
- 查找文件
- 文本和文件实用程序
- 将文件拆分为较小文件：split
- 通过网络访问计算机：telnet
- 在控制台上工作：setfont
- UNIX 打印入门
- UNIX 文本处理

本章介绍了一些在 shell 上工作时可以使用的基本工具和命令行程序。还有许多其他工具可用，但这些是其中一些更基础的工具。您已经在每个类别中学习了一些。尽管本章并不全面，但它会让您了解您会发现什么。还有许多其他工具——事实上多到可以成为一整本书的主题。

## 用户实用程序

在您的工作过程中，有时您会想要更改密码、更改 shell、查找文件、搜索文件等等。以下是一些可以帮助您的命令。

## 更改密码：passwd

使用 passwd 命令更改您的密码。由于该命令是交互式的，它会要求您输入当前密码（以确保其他用户在您离开计算机时不会更改您的密码），然后要求您输入新密码。成功确认密码后，系统会接受它。请注意，出于避免被附近的人窥视的原因，密码永远不会回显到屏幕上，如以下代码所示：



```
[alberto@digital alberto]$ passwd
Changing password for alberto
(current) UNIX password: ********
Enter new UNIX password: ********
Retype new UNIX password: ********
passwd: all authentication tokens updated successfully
```

超级用户 root 可以使用相同的 passwd 命令更改系统中的任何密码。当超级用户向命令提供用户名作为选项时，他或她可以更改系统中的任何用户的密码。超级用户无需验证用户的密码。作为超级用户更改用户密码看起来像这样：

```
[root@digital /root]# passwd alberto
Enter new UNIX password: ********
Retype new UNIX password: ********
passwd: all authentication tokens updated successfully
```

## 更改你的 Shell：chsh

如果你不喜欢你的 shell，可以使用 chsh 命令来更改它。只有 /etc/shells 中列出的 shell 才可接受使用。它可以交互式使用，如下所示：

```
alberto@digital alberto]$ more /etc/shells
/bin/bash
/bin/sh
/bin/ksh
/bin/csh
/bin/tcsh
[alberto@digital alberto]$ chsh
Changing shell for alberto.
Password: ********
New shell [/bin/tcsh]: /bin/bash
Shell changed.
```

如果喜欢的 shell 未列出，请在 /etc/shells 文件中添加一个条目，然后你就可以设置它了。

## 更改个人信息：chfn

chfn（change finger name）命令更改有关你的附加信息，例如你的全名、办公室地址以及办公室和家庭电话号码。此信息可使用 finger 命令访问（该命令在大多数系统中通常被禁用，因为它存在某些安全风险）。一些程序使用它来确定你的全名和其他信息。chfn 命令与 passwd 命令类似，是交互式的：

```
[alberto@digital alberto]$ chfn
Changing finger information for alberto.
Password: *********
Name [Caldera OpenLinux User]: Alberto Ricart
Office []: Rm. 3210 Left Wing
Office Phone []: 800 555 1212 ext 800
Home Phone []: not listed

Finger information changed.
```

## 系统上有哪些人：who 和 w

who 和 w 命令可用于查看谁登录到系统。w 会告诉你谁登录上了以及他们在做什么：

```
[alberto@digital /etc]$ w
17:17:07 up 5:42, 2 users, load average: 0.05, 0.13, 0.09
USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT
alberto tty1 11:51am 5:25m 33.95s 0.13s xinit /etc/X11/
alberto ttypo 192.168.0.10 5:07pm 1.00s 0.50s 0.08s w
```

who 命令只是告诉你谁登录到系统：

```
[alberto@digital /etc]$ who
alberto tty1 Sep 20 11:51
alberto ttypo Sep 20 17:07 (192.168.0.10)
```

这两个命令都指出了通过远程终端登录的用户。w 命令中的 FROM 列（上一节中的第一个示例）列出了远程用户的 IP 地址。who 命令也在括号之间显示远程用户的地址。

上一页 目录 下一页

## 完全傻瓜 Linux 使用指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

上一页 目录 下一页

## 查看和设置日期和时间：date

date 命令允许你读取当前日期和时间，以及设置系统的时钟（如果你以 root 身份运行）。它提供了大量选项，允许你使用多种格式来表示日期和时间。

默认情况下，如果你输入 date 命令，它会打印当前日期和时间。要格式化日期，请提供 + 参数，后跟一个格式化字符串。格式化字符串的各种选项（见表 17.1）前面都有一个百分号（%）符号。

### 表 17.1 日期选项

| Option | Description |
|---|---|
| %H | Print hour in 24-hour format with leading zeros (00..23) |
| %I | Print hour in 12-hour format with leading zeros (01..12) |
| %k | Print hour in 24-hour format (0..23) |
| %l | Print hour in 12-hour format (1..12) |
| %M | Print minutes (00..59) |
| %p | Print AM or PM |
| %r | Print time in 12-hour format with AM/PM (hh:mm:ss AM) |
| %s | Print the number of seconds since 1/1/70 |
| %S | Print second (00..61) |
| %T | Print time in 24-hour format (hh:mm:ss) |
| %X | Print time in locale's time representation (%H:%M:%S) |
| %Z | Print time zone (e.g., CST) |
| %a | Print locale's abbreviated weekday name (Sun) |
| %A | Print locale's full weekday name, variable length (Sunday) |
| %b | Print locale's abbreviated month name (Jan) |
| %B | Print locale's full month name (January) |
| %d | Print day of month (01..31) |
| %D | Print date as mm/dd/yy |
| %j | Print the number of the day in the year (001..366) |
| %m | Print the month (01..12) |
| %U | Print week number of year (00..53) |
| %w | Print day of week (0..6), with 0 corresponding to Sunday |
| %W | Print week number of year with Monday as first day of week (00..53) |
| %x | Print locale's date representation (mm/dd/yy) |
| %y | Print last two digits of year (00..99) |
| %Y | Print the year using 4 digits (1970...) |

例如，要以长格式打印日期，你需要输入：

```
[alberto@digital alberto]$ date "+%A %B %d %Y"
Sunday September 20 1998
```

请注意，格式字符串 %A %B %d %Y 用引号括起来。 （用引号括住字符串是必要的，这样 shell 就不会认为它接收到四个单独的参数。）当你用引号括住字符串时，你可以在字符串内部添加任何文本作为分隔符。例如，要在日期后添加逗号，你需要输入：

```
[alberto@digital alberto]$ date "+%A, %B %d %Y"
Sunday, September 20 1998
```

要以 YYYYMMDD 模式将日期打印为数字，请执行以下操作：

```
[alberto@digital alberto]$ date +%Y%m%d
19980920
```

要设置系统时钟，你需要提供以下格式的日期：

```
date MMDDhhmmYYYY
```

- MM 是月份的两位数（01–12）
- DD 是日期的两位数（01–31）
- hh 是 24 小时制下的两位数小时（00 为午夜，23 为晚上 11 点）
- mm 是两位数分钟（00–59）
- YYYY 是四位数年份（1998）

## 获取日历：cal

cal 命令打印日历。默认情况下，它会打印当前月份的日历：

```
[alberto@digital alberto]$ cal
    September 1998
Su Mo Tu We Th Fr Sa
      1  2  3  4  5
 6  7  8  9 10 11 12
13 14 15 16 17 18 19
20 21 22 23 24 25 26
27 28 29 30
```

如果你提供一个参数，它将被视为年份：

```
[alberto@digital alberto]$ cal 1998
1998
January          February          March
April
May
June
July
August
September
October
November
December
```

请注意，cal 98 和 cal 1998 将打印出非常不同的日历，因为 98 和 1998 是完全不同的年份。

要显示某一年中的特定月份，请提供两个参数。第一个被视为月份，第二个被视为年份：

```
[alberto@digital alberto]$ cal 12 1998
December 1998
Su Mo Tu We Th Fr Sa
      1  2  3  4  5
 6  7  8  9 10 11 12
13 14 15 16 17 18 19
20 21 22 23 24 25 26
27 28 29 30 31
```

## 完全傻瓜 Linux 使用指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

要访问内容，请点击章节和节标题。

搜索本书：

## 查找文件

在第 15 章“Help Please”中，你学习了 whereis 和 which 命令，它们可用于在特定位置查找程序和其他系统相关文件。UNIX 还提供了其他工具，以便你可以使用更离散的标准搜索文件。

在本节中，你将学习如何使用 find 和 locate 命令。

### 按名称查找文件：find

UNIX find 命令是一个难以掌握的命令。它提供了大量选项，可能令许多用户望而生畏。然而，经过一点指导，你就可以学会如何使用 find 来满足你 90% 的需求。find 命令的基本语法是

```
find paths expression
```

find 命令在提供的 paths 中搜索与 expression 匹配的文件。你可以搜索多个路径的文件，因为表达式列表直到 find 找到以破折号（-）开头的参数时才开始。

最基本的选项是 -name。它告诉 find 这是你正在搜索的文件名。如果使用通配符（*、? 和 []）指定名称，此选项会更强大。（参见第 14 章“Putting the Shell to Work”中的“Regular Expressions”部分。）

-print 选项告诉 find 将任何匹配项打印到终端。在 Linux 下这是可选的，但在其他 UNIX 系统中的某些 find 版本需要它，因为默认情况下 find 不会打印任何结果。
这是一个简单的示例：

```
[alberto@digital alberto]$ find /home/alberto /tmp -name "*.txt" -print
/home/alberto/intro.txt
/home/alberto/Desktop/Trash/intro.txt
/home/alberto/.netscape/cache/0F/cache3603EFAF0010427.txt
/home/alberto/intro2.txt
/home/alberto/kdetools.txt
/home/alberto/Hello World.txt
/home/alberto/test/test.txt
```





```
/home/alberto/test/todo.txt
/home/alberto/file.txt
/home/alberto/file3.txt
/home/alberto/file1.txt
/home/alberto/file2.txt
/home/alberto/afile.txt
find: /tmp/XF86Setup5909: Permission denied
find: /tmp/kfm-cache-0: Permission denied
find: /tmp/kfm-cache-100: Permission denied
find: /tmp/XF86Setup6565: Permission denied
find: /tmp/otherMail: Permission denied
find: /tmp/XF86Setup514: Permission denied
/tmp/file.txt
```

在这个示例中，我想查找 /home/alberto 或 /tmp 中所有文件名以 .txt 结尾的文件。请注意，我用引号将表达式括起来，以避免 shell glob（解释并展开）星号本身。请注意，在结果中，find 无法搜索我没有权限的目录。

尽管正则表达式有助于查找匹配项，但它仍然区分大小写；扩展名为 .TXT 的文件不会被找到。将 -name 选项替换为 -iname 可使搜索不区分大小写，因此以 .txt 和 .TXT 结尾的文件都会被找到：

```
[alberto@digital alberto]$ find /home/alberto /tmp -iname "*.txt" -print
/home/alberto/intro.txt
/home/alberto/Desktop/Trash/intro.txt
/home/alberto/FILE.TXT
/home/alberto/.netscape/cache/0F/cache3603EFAF0010427.txt
/home/alberto/intro2.txt
/home/alberto/kdetools.txt
/home/alberto/Hello World.txt
/home/alberto/test/test.txt
/home/alberto/test/todo.txt
/home/alberto/file.txt
/home/alberto/file3.txt
...
```

find 命令提供了多种选项，包括按修改日期和访问日期搜索文件的功能。此外，find 还能够使用找到的文件作为命令的参数来执行命令。这是通过 -exec 选项完成的。以下是一个示例：

```
[alberto@digital alberto]$ find /home/alberto -iname "*.txt" -exec wc {} \;
     22      329     1896 /home/alberto/intro.txt
     22      329     1896 /home/alberto/Desktop/Trash/intro.txt
      0        0        0 /home/alberto/FILE.TXT
     10       50      785 /home/alberto/.netscape/cache/0F/cache3603EFAF0010427.txt
     44      329     1894 /home/alberto/intro2.txt
    197      330     2403 /home/alberto/kdetools.txt
      1        1        8 /home/alberto/Hello World.txt
      0        0        0 /home/alberto/test/test.txt
      0        0        0 /home/alberto/test/todo.txt
      0        0        0 /home/alberto/file.txt
      0        0        0 /home/alberto/file3.txt
      0        0        0 /home/alberto/file1.txt
      0        0        0 /home/alberto/file2.txt
      0        0        0 /home/alberto/afile.txt
```

请注意，在此示例中，在调用 wc 命令之后，有一对大括号 ({ })。这些大括号会被与搜索匹配的文件名替换——然后它就成为 wc 命令的参数。还请注意，在末尾有一个分号 (;)。它告诉 find -exec 选项已完成。为了避免 shell 将分号解释为命令组，分号后面跟着反斜杠 (\ )。

Previous Table of Contents Next

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

To access the contents, click the chapter and section titles.

## Locating Files: locate

正如你所能看出，查找文件需要很长时间。find 命令需要搜索磁盘以查找你指定的文件。如果你是在文件名上进行搜索，有更好的、更快的办法：locate。

locate 命令通过预先构建所有已知文件名的数据库来获得其速度。不是扫描磁盘来匹配，而是使用复杂的数据库技术来瞬间找到文件——或者接近瞬间。这一特性的缺点是，如果你要搜索的文件是在数据库更新后创建的，数据库中就不会有它的条目，因此 locate 就无法找到它。通常这不是问题，因为 locate 每天大约在凌晨 5:55 更新其数据库。什么，你的电脑在那个时间没有开机？好吧，你也可以手动运行该命令。

## Building the locate Database: updatedb

要创建 locate 数据库，你必须以 root 身份并发出命令 /usr/bin/updatedb。该程序运行需要一段时间，但完成后，你就可以开始使用了。

## Finding a File: locate

要搜索文件，只需输入其名称或其部分名称（无通配符），任何与搜索匹配的文件路径都将被打印出来。以下是一个示例：

```
[root@digital alberto]# locate telnet
/mnt/cdrom/col/install/RPMS/netkit-telnet-0.12-1.1386.rpm
/usr/bin/telnet
/usr/include/arpa/telnet.h
/usr/lib/xemacs-19.16/etc/w3/telnet.xbm
/usr/lib/xemacs-19.16/lisp/comint/telnet.elc
/usr/man/man1/telnet.1.gz
/usr/man/man8/in.telnetd.8.gz
/usr/man/man8/telnetd.8.gz
/usr/sbin/in.telnetd
/var/lib/LST/contents/netkit-telnet
/var/lib/LST/installed/netkit-telnet
```

剩下的就是你决定想要哪个文件了！不坏。相同的命令如果使用 find 命令可能需要 10 分钟才能完成。

## Finding Files that Contain a Word or Pattern: grep

而 find 命令根据文件系统属性（文件名、修改时间等）查找匹配项，grep 命令则在文件中搜索模式。例如，如果你想查找包含单词 command 的文件，可以这样用 grep：

```
[alberto@digital alberto]$ grep command *.txt
intro.txt:Through a command line interface
intro.txt:The UNIX shell is not going away anytime soon. For this reason it is a lso covered in detail. In order for you to gain expertise an facility using Linux you have to be as comfortable in a command line environment as you are in a graphical one.
intro2.txt:Through a command line interface
intro2.txt:using Linux you have to be as comfortable in a command line
```

请注意，grep 会打印找到匹配的文本行。如果文件中有多个匹配项，它们都会被打印。一个特殊的选项 -c 会打印该单词在文件中匹配的次数：

```
[alberto@digital alberto]$ grep command -c *.txt
Hello World.txt:0
afile.txt:0
file.txt:0
file1.txt:0
file2.txt:0
file3.txt:0
intro.txt:2
intro2.txt:2
kdetools.txt:0
```

grep 命令也可以与管道一起使用，以过滤从其他程序获得的输出。例如，要查看系统中来自以 192.168 开头的 IP 的用户列表，你应该输入以下内容：

```
[alberto@digital alberto]$ w | grep 192.168
alberto tty p0 192.168.0.10 5:07pm 4:53 1.17s 1.03s -bash
alberto tty p1 192.168.0.10 5:54pm 0.00s 0.64s 0.09s w
```

grep 命令非常强大，你可以将其与正则表达式结合起来进行搜索。有关更多信息，请参阅手册页。

## Text and File Utilities

以下是用于处理文本信息的实用程序。其中许多实用程序可以创造性地用于与文本处理完全不同的目的。

## Counting Lines, Words, and Characters: wc

词计数 wc 实用程序在许多方面都很有用——它允许你统计一个或多个文件中出现的单词、行数和字符数。其语法很简单：

```
wc [options] files
```

wc 提供的选项有

- -c 仅打印字节数（字符数）
- -w 仅打印单词数

### Print only the number of lines

如果你提供多个文件，wc 很乐意为你提供所有文件的汇总报告。如果你不提供选项，它会打印所有信息，行数、单词数和字符数——按此顺序。以下是使用此命令处理 /etc/passwd 和 /etc/group 文件的示例：

```
[alberto@digital alberto]$ wc /etc/passwd /etc/group
      21      28     770 /etc/passwd
      26      26     346 /etc/group
      47      54    1116 total
```

虽然乍一看你可能认为你不需要这个命令（你可能是对的），但在许多情况下，创造性地使用 wc 命令可以为你提供所需的信息。

Previous Table of Contents Next





## 完全傻瓜指南 Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

To access the contents, click the chapter and section titles.

Search this book:

## 对文本行进行排序：sort

sort 命令允许你根据数值、字母顺序或电话簿顺序对文件中的行进行排序。sort 命令使用了“字段”的概念，其中文本行代表各种位（字段）的数据，而文件中的每一行代表一条记录。字段通常由特殊字符分隔，例如冒号、制表符、逗号或文件开发者想到的任何其他字符。

sort 最常用的选项是

- `-t` 指定字段分隔符
- `-n` 指定数值排序
- `-k` 指定排序将进行的字段（默认为行的第一个字符）
- `-f` 忽略大小写（字母“B”和“b”被视为相等）
- `-r` 反转结果

如果你想根据用户名对 /etc/password 文件进行排序，可以输入以下命令：

```
[alberto@digital alberto]$ sort /etc/passwd
adm:x:3:4:adm:/var/adm:
alberto:x:501:501:Caldera OpenLinux
User:/home/alberto:/bin/bash
bin:x:1:1:bin:/bin:
...
shutdown:x:6:11:shutdown::/sbin::/sbin/shutdown
sync:x:5:0:sync:/sbin:/bin/sync
uucp:x:10:14:uucp:/var/spool/uucp:
```

要根据 UID（用户 ID，用户在第三个字段）对文件进行数值排序，请使用以下命令。请注意，在 /etc/passwd 文件中，字段由冒号分隔：

```
[alberto@digital alberto]$ sort -t : -k 3 -n /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:
adm:x:3:4:adm:/var/adm:
...
nobody:x:65534:65534:Nobody::/bin/false
```

## 格式化文本：fmt

如果你使用基于控制台的编辑器编写文件，编辑器可能不会将你的文本换行成行。如果你要打印该文件，文本可能不会为你换行。大多数用户喜欢文件行宽约为 75 个字符，因为那是文本终端中可容纳的文本量。你可以使用 fmt 命令对任何文件应用换行。以下是一个示例：

```
[alberto@digital alberto]$ cat intro.txt
What This Book Is About (Paraphrasing Randal L. Schwartz in Learning Perl)

Among other things, this book is about 300 pages (and then some). This book is also
a gentle introduction to Linux. By the time you’ve gone
through this book, you’ll
have touched on the majority of the most common operations found
in Linux.

This book is not intended as a comprehensive guide to Linux  - on
the contrary,
in order to keep the book from being yet another comprehensive
reference guide,
I’ve been selective about covering the things you are
most likely to
use early in
your Linux hacking career. For more information, check out the
voluminous and
readily available Linux and UNIX reference material.
...
```

如果查看输出，你会注意到单词在错误的位置被断开了。使用 fmt 命令，我可以轻松地重新格式化此文件，以便更好地打印和在屏幕上阅读：

```
[alberto@digital alberto]$ fmt -w 68 intro.txt
What This Book Is About (Paraphrasing Randal L. Schwartz in Learning Perl)

Among other things, this book is about 300 pages (and then some). This book is also a gentle introduction to Linux. By the time you’ve gone through this book, you’ll have touched on the majority of the most common operations found in Linux.

This book is not intended as a comprehensive guide to Linux - on the contrary, in order to keep the book from being yet another comprehensive reference guide, I’ve been selective about covering the things you are most likely to use early in your Linux hacking career. For more information, check out the voluminous and readily available Linux and UNIX reference material.
```

好多了！fmt 命令有许多选项；然而，-w 和 -s 选项是最重要的。-w 选项告诉 fmt 行宽应为多少。如果不提供 -w 选项，fmt 将恢复使用 75 个字符作为行宽。-s 选项告诉 fmt 仅拆分行。如果你有一些较短的示例文本，默认行为是 fmt 先连接行，然后根据其内部规则拆分它们。

Previous Table of Contents Next

Products | Contact Us | About Us | Privacy | Ad Info | Home

Use of this site is subject to certain Terms & Conditions. Copyright © 1996-2000 EarthWeb Inc. All rights reserved. Reproduction whole or in part in any form or medium without express written permission of EarthWeb is prohibited.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

## 将文件拆分为较小文件：split

Check This Out:
Compression is discussed in Chapter 20, "Installing Programs and Applications," in the section "UNIX Compressed Archives: Gzip and Compress."

假设你想将一个文件复制到软盘上，但该文件即使压缩后也远大于单张磁盘的容量。你如何处理这个问题？一种方法是使用 split 命令。split 命令的语法如下：

```
split [option] size file outfile name
```

选项有 -l 用于按行数拆分文本文件，以及 -b 用于按字节数拆分文件。选项之后指定大小。使用字节选项时，可以添加 b 表示字节、k 表示千字节或 m 表示兆字节。File 是你要拆分的文件名，outfile name 是命令将用于命名所有块的基础名称。不同的文件名是通过在文件后附加扩展名生成的。

要将一个大文件拆分为 1395K 的块，以便每个块都能放入标准软盘：

```
[alberto@digital splitter]$ ls -l
 total 5801
 -rw-r--r-- 1 alberto alberto 5915554 Sep 20 11:51 book.zip
[alberto@digital splitter]$ split -b 1395k book.zip book.zip.
[alberto@digital splitter]$ ls -l
 total 11607
 -rw-r--r-- 1 alberto alberto 5915554 Sep 20 11:51 book.zip
 -rw-rw-r-- 1 alberto alberto 1428480 Sep 20 18:39 book.zip.aa
 -rw-rw-r-- 1 alberto alberto 1428480 Sep 20 18:39 book.zip.ab
 -rw-rw-r-- 1 alberto alberto 1428480 Sep 20 18:39 book.zip.ac
 -rw-rw-r-- 1 alberto alberto 1428480 Sep 20 18:39 book.zip.ad
 -rw-rw-r-- 1 alberto alberto 201634 Sep 20 18:39 book.zip.ae
```

没有 join 命令，因此要将文件连接成一个大文件，使用你已知的命令 cat：

```
cat book.zip.?? > book.zip
```

文件将被串联（复制）到一个大文件中。表达式 ?? 匹配任意两个字符（上例中为 aa 到 ae）。这之所以有效，是因为 shell 按字母顺序排列文件，因此 ab 有保证跟在 aa 之后。

## 通过网络访问计算机：telnet

telnet 命令允许你使用 shell 登录到远程计算机。就实际用途而言，你正在远程计算机的控制台上工作，并且可以像物理上坐在该计算机键盘前一样使用任何命令。telnet 命令非常易于使用：只需输入 telnet 后跟你想要工作的系统的主机名。这将为你提供一个登录提示，与过去几节中使用的提示大致相同。

telnet 会话的一个问题是，有时你的键盘不会按预期工作。要修复此问题，请参阅第 13 章“在 Shell 下进行文本编辑”中关于 stty 命令的边栏讨论。

要退出 telnet 会话，输入 exit 或在提示符下按 Ctrl+D。

## 在控制台上工作：setfont

如果你使用文本界面在 EGA/VGA 控制台上工作，你可能会想知道为什么你只能看到 24 行文本。好吧，有办法修复这个问题：setfont 命令。

setfont 命令更改控制台使用的字体大小。更改字体大小也会更改最大行宽和你可以看到的行数；因此，你选择的字体将决定你的可见工作空间。

许多字体安装在 /usr/lib/kbd/consolefonts 目录中。字体文件使用类型命名；通常，你希望选择名称以 default 开头的一个（因为字符类型会根据字体而变化）以及一个大小。标准 VGA 字体大小为 16（高 16 像素），因此使用更小的字体会带来巨大差异。字体类型/大小组合也会极大地影响可读性，相同大小的不同字体在屏幕上看起来会非常不同。一些字体文件包含三种大小：8、14 和 16。要指定正确的大小，只需提供一个连字符 (-) 后跟大小（setfont 在需要时会提示你）。如果你的屏幕出现混乱，只需再次输入 setfont 即可返回默认设置。

要更改字体，指定字体文件名（你不需要给出完整路径）：

```
setfont fontname
```

其中一个更受欢迎的字体，可以大大增加你的显示大小，使用以下方式选择：

```
Setfont /usr/lib/kbd/consolefonts/alt-8x8
```

尝试不同类型和大小，直到找到最适合你的可读性。





## 完全傻瓜的 Linux 使用指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## UNIX 打印入门

在这本书中，我有点忽略了告诉你如何打印文件，部分原因是如果你使用的是 StarOffice、WordPerfect 或 Applix 等文字处理器，这些程序已经知道如何打印而无需经过这些麻烦（StarOffice 包含在这本书附带的 CD 上。）

如果你想从命令行进行 UNIX 文本处理（与在 GUI 中进行文字处理相对），有几件事你需要知道，这会影响你打印的文档的最终呈现。Linux 和 UNIX 下的打印与 Windows 或 Macintosh 下的打印截然不同。从命令行打印涉及三个步骤：

- 1. 使用文本编辑器创建文档，并在需要时添加格式命令。这些格式命令或宏将取决于你使用的格式化程序。然而，文本标记（UNIX 人喜欢称之为文本处理）的概念是相同的。
- 2. 将你的文档通过一个或多个过滤器运行（某些过滤器可能像我之前提到的 fmt 命令一样基础）；最终的过滤器通常会生成一个包含所有必要打印机控制代码以呈现文档的文件。有时，过滤器可以直接将此输出发送到打印机。
- 3. 使用名为 lpr 的程序将过滤后的文件发送到打印机。

如果你只需要打印一个纯文本文件，你必须做几件事。你使用的程序将取决于你拥有的打印机类型。通常，打印机分为两类：具有 PostScript 的和不具有 PostScript 的。

如果你的打印机具有 PostScript 支持，你可能会使用一个名为 enscript 的程序。如果没有，你将使用一个名为 pr 的程序。在表面上，这些程序是等效的——只是 enscript 利用了 PostScript 可用的功能，因此功能更多。这些程序在基本层面上允许你指定页边距、页眉和文本行的长度。

不花哨，但它们提供了生成一个相当朴素外观文档所需的基本格式化功能。

这里有一个例子。如果你想打印一个名为 intro.txt 的文本文件，你会将其发送给 pr：

```
pr intro.txt
```

将同一文件发送到 PostScript 打印机将是这样做的：

```
enscript intro.txt
```

pr 和 enscript 都可以将输出发送到打印机，并且默认情况下它们就是这样做的。抛开这一点，这些基本调用几乎不会产生你期望的输出。页边距是什么？行在哪里折叠？你明白了。你需要在 pr 或 enscript 上设置所有这些选项，否则你的文档将使用打印机的默认设置。你的默认值将类似于从纸张边缘起左侧和顶部页边距为 1/2"，行长度约为 72 个字符宽，以及 Courier（打字机）字体——很可能不是你想要的。那你该怎么办？

你需要做的第一件事是阅读 man 手册并弄清楚你想要的 pr 或 enscript 的默认设置。除此之外，你可能还必须使用另一个格式化命令，例如 fmt。当你弄清楚各种设置后，你只需反复使用它们。

我的典型 enscript 会话大致如下：

```
[alberto@digital alberto]$ fmt -w 65 intro.txt | enscript --margins=100:100:100:100 -h -B
[ 1 pages * 1 copy ] sent to printer
```

我使用 fmt 创建约 65 个字符宽的行，然后将输出通过管道传递给 enscript。我将页边距选项设置为 100 像素（72 像素 = 1"），并且使用 -h 选项，抑制横幅页的打印（该页说明谁打印了文件并浪费纸张）。-B 选项抑制通常显示文档标题、上次保存时间和页码的页眉行的打印。

我也可以使用 pr 产生类似的输出，如下所示：

```
fmt -w 65 intro.txt | pr -o 15
```

-o 选项指定左侧页边距的字符数；15 个字符约为 1.5"。

要访问内容，请点击章节和节标题。

## 完全傻瓜的 Linux 使用指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## UNIX 文本处理

要生成更精美的输出，例如粗体文本、不同字体等，你需要使用 UNIX 的格式化程序之一，例如 groff（传统 troff 格式化程序的 GNU 版本）。如果你查看 man 页的源代码，你会看到你在使用 groff 时使用的格式化代码。（要查看源代码，请对 /usr/man/man1/ 中的任何文档使用 zless。）这是一个你会看到的例子：

```
.TH man 1 "September 2, 1995"
.LO 1
.SH NAME
man \- format and display the on-line manual pages
.br
manpath \- determine user's search path for man pages
.SH SYNOPSIS
man [\-acd fhkKtwW] [\-m system] [\-p string] [\-C config_file] [\-M path] [\-P pager] [\-S section_list] [section] name ...
.SH DESCRIPTION
.B man
formats and displays the on-line manual pages. This version knows about the
.B MANPATH
and
.B (MAN) PAGER
environment variables, so you can have
your own set(s) of personal man pages and choose whatever program you like to display the formatted pages. If
.I section
is specified,
.B man
only looks in that section of the manual.
You may also specify the order to search the sections for entries
```

正如你从此源文本中看到的，groff（troff！）格式化的文件没有任何空行。格式化命令（宏）必须从左边缘开始。宏的名称通常以点（.）或撇号（'）开头。格式化一直持续到另一个宏覆盖它为止。

你使用的宏将取决于你设计的文档类型。前面列表中的宏是为格式化 UNIX 手册页而设计的。例如，Man 定义了诸如 .B 用于粗体和 .I 用于斜体以及更复杂的用于定义标题、描述等的宏。如果你曾经使用文本编辑器编写过 HTML 页面，从 UNIX 命令行格式化文本在概念上并没有那么不同，只是标记标签不同。标记标签会根据你使用的宏包而改变。例如，另一个名为 ms 的包提供了论文的格式化。

正如你可能已经猜到的，你实际上能做什么取决于你拥有的宏。除了前面提到的 man 宏之外，其他库如 ms、mm 和 me 用于格式化其他类型的文档（请参阅 UNIX 手册第 7 节中的 groff_ms、groff_mm、man 和 me；要进入那里，输入 man 7 keyword）。代码以及它们如何格式化文档因包而异。

当你的文本以这种（有些别扭）的方式格式化时，你可以使用 groff 命令生成文本、PostScript、HTML、LaserJet 打印机和其他格式的输出。然后你将生成的此文件发送给 lpr 命令以打印它。lpr 命令接受你提供的内容并将其排队到打印机。语法如下所示：

```
nroff -Tps -macropackage filename | lpr
```

将 macropackage 替换为宏的名称（man 用于手册页，ms、me、mm 等）和 filename 替换为你的文件名。

正如你所知，要生成一个简单格式化的文档，你需要知道很多东西。UNIX 文本处理并不止于 groff。其他更复杂的排版系统如 TeX 和 LaTeX 可以生成专业格式的文档。许多印刷的技术出版物都是使用 TeX 和 LaTeX 开发和印刷的。

那么为什么这么复杂？UNIX 命令行打印系统的意图是使用任何可以显示和正确打印到各种设备的文本编辑器生成文件。因此，你可以生成手册页，在纸上打印它们，生成 HTML 页面，并生成 pdf（Adobe Acrobat）文件，所有这些都来自同一个格式化的文件。如果你只是想使用文字处理或桌面出版，请坚持使用 GUI 文字处理器，例如 StarOffice 中包含的文字处理器。当你只需要一份漂亮的纸质文档时，它会为你节省时间。





To access the contents, click the chapter and section titles.

## 完全傻瓜Linux指南

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Part 3
Linux下的基本系统任务

你已经体验过 KDE，并且已经深入使用命令行。接下来还要做什么？与生活中的其他事情一样，在 Linux 中也有那些必须做的事情。别担心，情况并没有听起来那么糟糕——第 3 部分的信息会帮助你。 这些章节会指导你备份你的机器、安装软件、监控系统，你甚至会认识 LISA。还有一章专门为真正喜欢冒险的人介绍如何定制你的 Linux 系统。先给你提个醒，现在就开始吧！

## Chapter 18
用户、组和密码

## In This Chapter

- Adding Users
- Modifying Users: usermod
- Deleting Users: userdel
- Adding, Modifying, and Removing Groups
- Users and Passwords
- Linux and Shadow Passwords

如果你有一台独立系统，你可能不必太担心管理多个用户和账户。你很可能还会继续使用安装系统时创建的同一个账户。

然而，如果你处于网络环境中，你可能想要授予其他用户访问你系统的权限。因此，本章的主题对你来说具有中等重要性。如果你管理的是具有多个账户的系统，你应该确保阅读本章并理解其中的内容。如需进一步帮助，请务必参考第 15 章“Help Please”中讨论的 Linux System Administrator’s Guide。

登录和密码存在的全部原因是为了安全。在 UNIX 中，我们希望保护自己的工作不被他人侵犯。与基于 Windows 95/98/NT 的 PC 不同，UNIX 系统可以支持大量并发用户。换句话说，多位用户可以通过网络或其他连接的终端同时使用你的计算机及其服务，而你也在使用它。如果你还没有阅读第 16 章“Permissions: Protecting and Sharing your Work”，现在可能是个好时机。

添加、删除和管理用户是一项管理任务。幸运的是，如今这项任务已相当自动化，因为工具更灵活，能够处理许多步骤。在早期，你必须手工添加、删除和管理用户，或许借助自己开发的自定义脚本。

尽管工具在某种程度上自动化了流程，了解幕后发生的事情仍然很有用。这些活动的核心是 /etc/passwd、/etc/shadow 和 /etc/group。这些文件实际上是包含用户和组信息的系统数据库。/etc/passwd 文件存储以下内容：

- 用户名列表（登录名）
- 代表登录的 User ID（UID）号码
- 代表登录默认组成员资格的 Group ID（GID）
- 有关用户的可选信息，如电话号码、办公室等
- 主目录的位置
- 用户的默认 shell

组数据库 /etc/group 存储以下内容：

- 用户组列表
- 组的密码（组名可以被启用为账户工作，尽管这种类型的公共使用账户通常是非常糟糕的主意）
- GID 号码
- 属于该组的所有用户名列表，以逗号分隔

仅 root 可读的 shadow 密码文件 /etc/shadow 存储每个登录的加密密码

让我们看看如果你不使用工具需要做什么。当你添加一个用户时，你需要在 /etc/passwd 和 /etc/group 文件中输入适当的信息。你还必须创建用户的主目录，将所有必要的初始化文件复制到新主目录（“rc”文件如 .bashrc、.login、.logout 和 .profile），为用户创建邮箱，如果用户属于某种邮件别名，则添加别名。至关重要的是，你必须保持 UID 和 GID 的唯一且不重复。完成所有这些后，你必须验证为用户创建的目录，如用户主目录，具有适当的权限等等。最终，这是一项繁琐的工作，尤其是当你需要添加不止几个用户时！

幸运的是，如今 UNIX 工具管理了大部分繁琐工作。有些工具做得比其他工具更好。你用于管理的工具取决于你的选择以及你需要管理的用户数量。其中一些工具，如 useradd，表现平平，而有些，如 adduser，则非常出色！

useradd 和 adduser 工具安装在 /usr/sbin 目录中。如果你以 root 登录，你的 shell 应该能看到这些程序。管理用户账户是超级用户的特权角色。

### Adding Users

所以你需要添加一个用户。你该怎么做？你的选择是使用 adduser 和 useradd。

#### adduser

adduser 是一个用于添加用户账户的命令行工具。它很有趣，因为它同时管理 /etc/passwd 和 /etc/group 来实现 User Private Groups（UPGs；参见第 16 章），这是一种策略，即每个用户都被设为仅他自己所属的组的成员。使用 UPGs 简化了用户之间共享文件的过程，仅凭这一点，adduser 就应该是你为系统添加账户时使用的程序。如果你按照指示使用标准安装选项安装了 OpenLinux，adduser 应该已经在你的系统上。如果没有，你可以从 CD 安装它。

要添加新用户，只需输入 adduser username，像这样：

```
[root@digital alberto]# adduser flower

Looking for first available UID... 502
Looking for first available GID... 502

Adding login: flower...done.
Creating home directory: /home/flower...done.
Creating mailbox: /var/spool/mail/flower...done.

Don't forget to set the password.
```

此命令迅速找到了下一个可用的 UID 和 GID，并在 /etc/passwd 和 /etc/group 中为它们创建了条目。它创建了主目录 /home/flower，从 /etc/skel 复制了所有启动文件，然后创建了邮箱。

尽管这是工作的主体，但关于用户的可选细节，如用户的真实姓名，并未设置。要设置这些细节，你可以使用 chfn 命令。参见第 17 章“Command Toolbox: Useful Shell Commands and Shortcuts”中“Changing Your Personal Information: chfn”部分。

一个更重要的未默认设置的细节是账户密码。要为账户设置密码，请参见第 17 章中“Changing Your Password: passwd”部分。

添加用户时需要注意的一点是，用户名应保持在八个字符或更少。较长的用户名无法被系统和/或其他程序正确处理。

#### Useradd

Useradd 与 adduser 类似；唯一的问题是它不管理组数据库，也不实现 UPG 方案，这可以在长远来看简化你所做的大部分工作。要通过 useradd 添加账户，只需输入以下内容：

```
useradd -m username
```

-m 选项创建主目录。账户的密码仍需设置，用户的真实姓名和其他用户信息也必须设置。

### Modifying Users: usermod

随着时间的推移，一些用户需要对其账户进行某些更改。使用 usermod 进行更改很容易，因为它提供了各种可设置的选项。

#### Moving a Home Directory

要移动主目录，使用以下语法：

```
usermod -d newdirpath -m login
[root@digital root]# usermod -d /home/newflower -m flower
```

此选项修改 /etc/passwd 文件指定的主目录位置，使其指向 -d 选项指定的目录。它还会创建主目录（如果不存在）。-m 选项将旧主目录的内容移动到新目录中。

如果你更改主目录的名称，你可能还想更改用户的登录名。此选项仅更改主目录名称；登录名保持不变。

#### Changing a Login Name

要更改登录名，输入以下内容：

```
usermod -l newlogin currentlogin
[root@digital root]# usermod -l newflower flower
```




此选项更改用户的登录名。所有其他信息保持不变。通常，当你更改登录名时，你也希望更改或移动主目录，如前一节所述。在这里显示的示例中，登录名 flower 被更改为 newflower。

## 更改次要组隶属关系

要更改次要组隶属关系，输入以下命令：

```
usermod -d newdirpath -m login
usermod -d /home/newflower -m flower
[root@digital root]# groups flower
flower : flower users
[root@digital root]# usermod -G wheel,database flower
[root@digital root]# groups flower
flower : flower wheel database
```

groups 命令打印用户当前所有组隶属关系的列表。如果未提供登录名，它会假设你想知道当前用户的组隶属关系。

要更改所有次要组隶属关系（不是默认组），提供一个用逗号分隔的组名列表，且中间没有空格。如果省略某个组，则该成员资格将被移除。唯一的例外是用户的首要组。

## 删除用户：userdel

要从系统中删除用户，可以使用 userdel 命令。userdel 以用户的登录名作为参数。这将从 /etc/passwd 文件中删除指定的用户。然而，用户的主目录、邮箱、UPG 以及其他组隶属关系仍会被保留。语法如下：

```
[root@digital root]# userdel newflower
```

通常，在删除用户之前，你应该备份相应的账户和邮箱，或在删除账户前请用户自行备份。在采取必要的预防措施后，使用 userdel 删除用户。然后使用 groupdel 删除用户的 UPG 条目。你还必须使用文本编辑器从 /etc/group 文件中的所有其他条目中删除已移除的登录名。

如果你使用 UPG 并且用户的默认组是对应的 UPG，可以通过输入以下命令减少步骤数：

```
usermod -G username username
```

这将移除用户除 UPG（默认组）之外的所有组隶属关系。默认组作为 -G 的参数提供，因为 usermod 需要它。在完成上一步后，你可以输入以下命令：

```
userdel username
```

这会从 /etc/passwd 文件中删除用户。你可以通过从 /etc/group 中删除 UPG 来完成任务。最后通过删除用户的主目录和他的邮箱来完成移除（确保你先备份了！），如下所示：

```
rm -R /home/username /usr/spool/mail/username
```

Previous Table of Contents Next

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## 添加、修改和删除组

管理组与管理账户类似。请注意，这些命令提供的一些功能也可以通过 usermod 等程序实现。你选择的取决于你当时正在做什么。

### Groupadd

在你使用组之前，需要先创建它。创建组很容易；只需使用 groupadd 命令：

```
groupadd -g GID groupname
[root@digital alberto]# groupadd -g 600 weirdgroup
```

使用 groupadd 的唯一需要注意的是，你需要提供一个 /etc/group 文件当前未使用的 GID。为了便于编号，你可能希望将自定义组指定为从 GID 30000 或其他小于 65536（最大值）的较大数字开始。

### 管理组成员资格：gpasswd

gpasswd 程序用于管理组文件。添加和删除用户的[content]

此选项更改用户的登录名。所有其他信息保持不变。通常，当你更改登录名时，你也希望更改或移动主目录，如前一节所述。在这里显示的示例中，登录名 flower 被更改为 newflower。

## 更改次要组隶属关系

要更改次要组隶属关系，输入以下命令：

```
usermod -d newdirpath -m login
usermod -d /home/newflower -m flower
[root@digital root]# groups flower
flower : flower users
[root@digital root]# usermod -G wheel,database flower
[root@digital root]# groups flower
flower : flower wheel database
```

groups 命令打印用户当前所有组隶属关系的列表。如果未提供登录名，它会假设你想知道当前用户的组隶属关系。

要更改所有次要组隶属关系（不是默认组），提供一个用逗号分隔的组名列表，且中间没有空格。如果省略某个组，则该成员资格将被移除。唯一的例外是用户的首要组。

## 删除用户：userdel

要从系统中删除用户，可以使用 userdel 命令。userdel 以用户的登录名作为参数。这将从 /etc/passwd 文件中删除指定的用户。然而，用户的主目录、邮箱、UPG 以及其他组隶属关系仍会被保留。语法如下：

```
[root@digital root]# userdel newflower
```

通常，在删除用户之前，你应该备份相应的账户和邮箱，或在删除账户前请用户自行备份。在采取必要的预防措施后，使用 userdel 删除用户。然后使用 groupdel 删除用户的 UPG 条目。你还必须使用文本编辑器从 /etc/group 文件中的所有其他条目中删除已移除的登录名。

如果你使用 UPG 并且用户的默认组是对应的 UPG，可以通过输入以下命令减少步骤数：

```
usermod -G username username
```

这将移除用户除 UPG（默认组）之外的所有组隶属关系。默认组作为 -G 的参数提供，因为 usermod 需要它。在完成上一步后，你可以输入以下命令：

```
userdel username
```

这会从 /etc/passwd 文件中删除用户。你可以通过从 /etc/group 中删除 UPG 来完成任务。最后通过删除用户的主目录和他的邮箱来完成移除（确保你先备份了！），如下所示：

```
rm -R /home/username /usr/spool/mail/username
```

Previous Table of Contents Next

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Adding, Modifying, and Removing Groups

Managing groups is similar to managing accounts. Note that some of the functionality provided by these commands can also be attained through programs like usermod. Your choice of which one to use will depend on what you are doing at that moment.

### Groupadd

Before you can work with a group, you need to create it. Creating a group is easy; just use the groupadd command:

```
groupadd -g GID groupname
[root@digital alberto]# groupadd -g 600 weirdgroup
```

The one catch with groupadd is that you need to supply a GID that your /etc/group file is not currently using. To make numbering easy on you, you might want to designate custom groups to start with a GID of 30000 or some other large number less than 65536 (the maximum number).

### Managing Group Memberships: gpasswd

The gpasswd program is used to manage the group file. The basic functionality for adding and removing users is straightforward. The -a flag is used to add users (note that the group must already exist), like this:

```
gpasswd -a username groupname
```

```
[root@digital alberto]# gpasswd -a flower users
```

The -d flag is used to delete users, like this:

```
gpasswd -d username groupname
```

## Users and Passwords

UNIX (and Linux) security begins with proper password selection. Therefore, it is a good idea to use passwords that cannot be easily guessed. Using simple scripts and available programs, a deviant hacker can test several thousand passwords in a few seconds.

### Password Don'ts

- Do not use birthdays, social security numbers, or phone numbers.
- Do not use names of relatives or pets.
- Do not use words that appear in a dictionary.
- Do not give your password to anyone—not even to a system administrator. If this person is really an administrator, he or she doesn’t need your password!

### Password Do's

- Mix upper- and lower-case.
- Add numbers and punctuation marks to make it harder to guess. Your final password should probably be random letters and numbers.
- Change your password every two months or any time that you think your password might have become compromised.
- Good passwords should roll out of your fingers and be easy to type. Many people are very adept at telling what you type from the motion of your fingers. If you have to think about it, it is probably not a good password for you.

## Linux and Shadow Passwords

If you are managing a computer that is connected to the Internet and that supports several users, you should consider enabling shadow passwords in your system. Shadow passwords are installed by default as a part of the standard installation. To see if shadow passwords are currently installed on your system, try this:

```
$ ls /etc/shadow
/etc/shadow
$
```

You should have received the same response. If ls responds instead like this, you should install shadow password support immediately:

```
ls: /etc/shadow: No such file or directory
```

Shadow passwords protect system passwords by making the file that actually contains passwords (/etc/shadow) readable only by root. The /etc/passwd file will contain stars (*) where the encrypted password was previously found. This is because even though passwords are encrypted in the /etc/passwd file, low-end computers have become very fast and able to decrypt them in a short amount of time. In the late 1980s, it probably would have taken days or weeks to decrypt this information. With today’s technology, however, it can take only a few minutes. By making the password file readable only by root, this establishes yet another security layer around this information.

For more information on shadow passwords and how to enable them, you should take a look at your man documentation for shadow (section 5 of the UNIX manual, man 5 shadow), pwconv, and pwunconv.

## SPIDER KILLER

## spider catcher

HOME ACCOUNT INFO SUBSCRIBE LOGIN SEARCH MY ITKNOWLEDGE FAQ SITEMAP CONTACT US

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Bookmark it

Search this book:

Previous Table of Contents Next

## Chapter 19
### Backups: Safeguarding Your Work

## In This Chapter

- Media Are Just Devices
- What to Back Up
- Simple Backups
- Tape Archive: tar
- A Backup Strategy
- Graphical Backup Programs

Without a doubt the most important maintenance task that you can perform on any computer is a backup. Backups can be tedious tasks, but it’s usually when you have neglected to do it that you most need it! Having a backup for your data can mean the difference between an inconvenience and a catastrophe. Without a backup, you’ll have a déjà vu experience recreating the work you lose. As you might already know, that is no fun. Restoring your system from a backup can be an inconvenience, and maybe a few hours of work will be lost, but it is much different than losing work you’ve created throughout past weeks, months, or even years!

A backup might be required even for simple user errors such as deleting important files. Unlike Windows or other operating systems, under UNIX/Linux there’s no “undelete” program, Norton Undelete, or any other tool to restore deleted files. If the file is deleted, it is gone. The reason these


utilities don’t exist for UNIX/Linux is the way that disk space is allocated: When you delete a file and release its storage space, this space will probably be written over next. So even if such tools existed, it is likely that they would be useless. Your only guarantee of getting a file back is to have a backup.

Although backing up is not difficult, it can be tedious and time-consuming. However, you should consider it an essential task and time investment. To put it in perspective, some backup is better than none at all. How often you should do it will depend on many issues. The answer is that it depends. A server that constantly has new information on it needs to be backed up more often than a standalone user workstation that rarely changes. If your system acts as a file server on which users or other programs store data, all bets are off. You don’t have the luxury of determining what is a good interval; you should back it up daily.

On a multiuser system such as Linux, proper backup is even more important. A crashing disk could take away the work of many, potentially hundreds of, users. Losing other people’s work is a good way to have a lot of people mad at you! Regardless of the type of system you have, you’ll need to back up the data. Linux can make it easier than you thought, provided you have the right equipment.

Your backup hardware needs might be as simple as floppy disks or tape media, or as complicated as requiring specialized hardware that maintains redundant systems in which a secondary disk is ready and waiting to transparently take the place of the failed one. This chapter covers simple backups. Specialized hardware is better administered by an experienced administrator. In terms of media, you can use floppies, although in the long run tapes are much more reliable, and in turn some optical media might be more reliable than a tape. How reliable information is will depend on the length of time that you’ll need to keep data around.

To see a list of compatible tape drives, see Appendix B, “OpenLinux Compatibility Guide.”

## Media Are Just Devices

The programs you can use for backing up under UNIX/Linux have been around for a long time and are very stable. None of these programs rely on a particular piece of hardware to perform their function and can all work equally well outputting their data to a floppy, a tape, any kind of disk, or a file. The file used for a backup is often just the device (/dev) file where you point your backup to go.

How you handle your backup strategy is really a matter of personal preference. If you establish policies, such as describing what you back up, it becomes easier to do many system administration tasks. Also, it is important to have the right hardware for making backups. By “right hardware” I mean that the disks you back up must fit onto a convenient backup medium; otherwise, you’ll have more tapes or disks than you’ll know what to do with. If you can afford it, buy a tape drive. This medium is inexpensive and can hold a lot of data. Other backup solutions might also work on your network, depending on how much data you need to back up.

## Complete Idiot's Guide to Linux

Publisher: Macmillan Computer Publishing
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

## Backup Media

There is an incredible array of choices for backup media these days:

- Floppy disks
- Floptical disks
- Magneto-optical (MO) disks
- Quarter-inch cartridge tapes (QIC)
- Minicartridge QIC and Travan tapes
- Write-once CD-ROMs (CD-Rs)
- Rewritable CD-ROMs (CD-RWs)
- Iomega Jaz and Zip drives
- Nine-track magnetic tapes
- 4mm Digital Audio Tapes (DATs)
- 8mm cartridge tapes
- DLT cartridge tapes

These media are described in the following sections.

### Floppy Disks

Floppy disks are the most convenient backup medium available because your system likely has a built-in floppy disk drive. The standard capacity is 1.44MB. Some 2.88MB drives made it into the market a few years back, but they never caught on. The drawback of floppy disks is that they are slow, fairly expensive (about 30–60 cents per disk), and not very useful for backing up anything that requires more than a couple of disks. The one advantage is that most computers are equipped with one.

### Floptical Disks

These higher-capacity disks take advantage of optical tracking technology to improve head positioning and therefore maximize the amount of data that can be packed onto the surface of a disk. Floptical drives can read standard 1.44MB and 720KB floppy disks. Density of information can be anywhere from a few megabytes to 200MB per disk.

### Magneto-Optical Disks

Magneto-optical disks have a plastic or glass substrate coated with a compound that, when heated, allows a magnetic source to realign the polarity of the material. When the material cools, its polarity is frozen. The material can be rewritten by a subsequent write operation.

Data is read by a lower-intensity beam, and the polarization pattern is interpreted as a byte stream. A wide variety of these devices are commercially available, ranging in format from 5 1/2 inches to 3 1/2 inches. These devices can store information ranging in size from 128MB to more than 2GB.

Read speed on MO disks is as fast as that on a hard disk. Write operations usually take a little longer but are still faster than write operations on a slow hard disk or a standard floppy disk. Medium reliability is very high.

### Quarter-Inch Cartridge Tapes

QIC tapes get their name from the fact that the tape’s width is 0.25, or one quarter, of an inch. Many PC users are familiar with minicartridge QIC drives, but these are discussed in the next session, alongside Travan tapes.

QIC drives originally shipped as standard equipment on a number of older UNIX workstations and were the primary means for booting an “empty” system and for data interchange. The original QIC drives stored very small amounts (20-60 megabytes), but QIC-SCSI drives in the range of 250MB-525MB are currently popular. The largest QIC-SCSI drives shipping at the moment store 26GB (gigabytes) and store data at around 60MB per minute.

True QIC drives are exceedingly reliable and are favorites of many UNIX workstation users. The cartridges themselves are built like (heavy) tanks and can be read thousands of times.

### Travan Tapes

A minicartridge QIC tape is a low-end, PC-market backup storage solution that uses the same .25-inch tape width found in true QIC drives. Some vendors are pushing the minicartridge format to store up to 1600MB by using a .315-inch format, resulting in Travan tapes.

Standard QIC tapes can hold anywhere from 11MB to 150MB and are usually designated as QIC-11 or QIC-24, depending on the amount of storage space they provide. Storage space in megabytes is indicated by the number following the QIC portion of the designation.

Sometimes tapes created on one vendor’s drive are not readable by another vendor’s drive. This is due to byte ordering and other special formatting issues. Within a vendor, tapes are usually backward compatible, meaning that you might be able to read lower-density tapes on a higher-density drive; however, you should verify this before you upgrade to a new drive in the same product line and discard your old one.

Travan tapes are similar in size to minicartridge QIC tapes but store 120–8000MB per tape depending on the type of tape drive mechanism used. Travan tapes are compatible with the minicartridge QIC tape formats, making them attractive if you have legacy minicartridge QIC tapes. Its price, capacity, and performance make this system a very attractive option.





To access the contents, click the chapter and section titles.

## 完全傻瓜的 Linux 使用指南

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## 一次性写入 CD-ROM

新技术和价格下降使得 CD-R 成为多媒体爱好者的热门选择。CD-R 使用的技术与普通 CD 相似，但不是“压制”而成，而是使用类似于 MO 磁盘的过程进行刻录。用 CD-R 创建的 CD 不像压制 CD 那样坚固，但如果妥善保管磁盘，它们可以使用很长时间。这些磁盘与任何具有 CD-ROM 的桌面系统兼容，这有助于使其成为一种流行的写入一次读取多次 (WORM) 格式。当前容量约为 600MB。记录速度较慢——通常为 2–8X 速度，而大多数 CD-ROM 的读取速度可达 32X。正在研发中的新型 CD-ROM 格式将提供 17GB 的存储空间，使其成为备份和归档任务的非常有趣的解决方案。

## 可重写 CD-ROM

CD-R 的流行为一种更新的介质铺平了道路：CD-RW。基于 CD-R 的相同技术，CD-RW 是一种可以重复使用的介质，很像软盘。CD-RW 使用的介质材料和驱动器与标准 CD-R 不同，但过程基本上是相同的概念。

## Iomega Jaz 和 Zip 驱动器

Zip 是一种流行的可移动磁盘驱动器。它们价格非常便宜：驱动器约 $150，每张磁盘 $10-$15。每张磁盘可存储约 100MB。它们有 SCSI（小型计算机系统接口——读作“skuzzy”）、并行和组合版本。

SCSI 驱动器需要 SCSI 接口（一种特殊类型的磁盘控制器，也称为主机适配器，使用标准化命令访问硬件）。

Jaz 驱动器是 Zip 驱动器的更高性能、更高容量版本。Jaz 驱动器价格稍贵，约 $350，并需要 SCSI 接口。磁盘价格超过 $99，可提供 1GB+ 的快速存储空间。这是一款热门产品。

## 九轨磁带

这是一种旧的磁带格式，以 800、1600 或 6250BPI（每英寸位数）密度写入。今天这种格式除在旧大型机上外已不常用。一些程序如 dump，一种备份程序，使用这种格式作为其磁带容量计算的基础。

## 4mm 数字音频磁带

DAT，可在 60 米磁带上存储 1.3GB 的信息（90m 为 1.95GB，120m 为 2.6GB），最初是为音频市场设计的。数字数据存储 (DDS)，即 DAT 的计算机版本，提供所有存储方案中最小的存储解决方案。其容量通常通过使用压缩而翻倍以上。带硬件压缩的驱动器可存储多达 8GB。对大多数 UNIX 用户而言，首选的磁带备份系统是 DDS。这些驱动器中的许多价格约为 $400，需要 SCSI 接口。这就是我自己系统上使用的磁带驱动器类型，而且非常棒！

## 8mm 卡式磁带

8mm 卡式磁带（也称为“Exabytes”，为唯一制造它们的公司）与它们的视频对应产品尺寸相同。许多管理员购买高质量的“视频级”磁带，而不是高级数据版本。驱动器可存储 2–5GB，当前版本可将多达 40GB 压缩到单个磁带中，写入速度高达每分钟 360MB。由于需要的磁带更少，这是一种非常方便的格式，尤其适用于服务器系统。8mm 驱动器通常出现在多驱动器库中，存储容量超过 300GB。

## DLT 卡式磁带

## 要备份的内容

通常，您不需要备份整个系统，因为磁盘上相当多的内容（至少最初）您已经作为安装 CD 的一部分拥有。这为您提供了双重好处：您的备份会更小（因为要备份的内容更少），并且速度更快（同样由于数据量减少）。Linux 对重要配置文件提供了良好的组织，通常保存在一个共同位置。随着您配置和更改系统，您应该维护一份日志（一个简单的账户，您可以向其发送电子邮件，可以作为记录您对系统所做更改的简单但有效的方式），并用它来驱动您的备份策略。至少，您应该备份以下目录：

- `/etc`
- `/usr/lib`
- `/usr/X11R6/lib/X11` (if you use X Windows)
- `/usr/src/linux` (if you have modified your kernel sources)
- `/home`
- `/var/spool/mail`

备份这些目录很重要，因为它们包含系统配置文件、用户文件和用户邮件 spool 目录。鉴于今天磁带驱动器的低成本，您可能应该投资一个。容量应与您拥有的硬盘大小相匹配。虽然将备份分散到多个磁带上是非常常见的事情，但没有比丢失磁带或磁带损坏更糟糕的了。通过将所有数据放在一张磁带上，您知道您拥有它，并且不必担心部分备份问题。

## 简单备份

简单备份是指将文件复制到另一种介质上。没有策略，因此操作简单——前提是您知道要保存什么。您可以使用 cp 命令复制文件，也可以使用 tar 等归档工具，我将在后面描述。

## 磁带归档：tar

最简单的备份实用程序是 tar。它的功能相当简单：它创建归档其他文件的归档文件。在 UNIX 中，分发程序通常以 tar 文件形式出现。（tar 文件类似于 PC 世界中的 zip 文件。）现代版本的 tar 不仅可以归档，还可以压缩数据，使 tar 文件更小。请注意，在磁带上压缩 tar 文件是不推荐的，因为 tar 然后无法从磁带错误中恢复。

tar 程序有许多选项。我建议您阅读其 man 手册页以了解它提供的功能（请参阅第 15 章“Help Please”，了解访问 man 手册页的信息）。在下一节中，您将学习使用 tar 所需的最少知识。

## 创建 tar 文件

tar 命令的格式遵循以下模式：

```
tar options destination source
```

要将我的主目录 /home/alberto 备份到文件 /tmp/bkup.tar，我会输入以下内容：

```
tar cvf archiveName pathsToArchive
```

```
tar cvf /tmp/bkup.tar /home/alberto
```

在 tar 中，参数通常不带破折号给出。选项 (cvf) 的顺序及其后跟随的参数很重要。在我们的例子中，cvf 选项告诉 tar

- 创建一个归档 (c 选项)
- 详细显示并列出其操作 (v 选项)
- 将归档放在文件或设备上 (f 选项)

f 选项期望下一个参数为 tar 文件将被创建的文件名或设备。在我们的例子中，它是 /tmp 目录中的一个常规文件，名为 bkup.tar：/tmp/bkup.tar 该文件可以被替换为您要写入文件的备份设备的名称。（我将在本节后面讨论这一点。）

f 命令会将我的主目录中的所有文件备份到我称为 bkup.tar 的文件中。关于 tar 的一个重要点是，如果我提供一个要备份的路径，该路径会被保留。因此当我“解包”文件时（我们将在后面“从 tar 归档中提取文件”一节中看到），它会在不存在时创建一个 home/alberto 目录。请注意，起始的正斜杠 (/) 被删除。

在文件参数之后指定的所有路径和文件都会被忠实地复制。在我的例子中，我只提供了 /home/alberto，但我同样可以输入：

```
tar cvf /tmp/bkup.tar /home/alberto /var/spool/mail/alberto
```

该命令会将我的主目录和我的邮箱备份到同一个归档中。

## 从 tar 归档中提取文件

没有“untar”命令。要提取文件，您使用 tar 命令并提供不同的选项。要提取我在前一节中创建的 tar 文件中的文件，我会输入：

```
tar xvf archive destination_or_name_of_file_to_extract
tar xvf /tmp/bkup.tar /
```

第一个参数包含 tar 命令的选项。在这种情况下，xvt 选项告诉 tar

- 提取文件 (x 选项)
- 详细显示并列出其操作 (v 选项)
- 从提供的归档文件读取 (f 选项)

第二个参数指定归档的名称 (/tmp/bkup.tar)。

最后一个参数 (/) 是可选的，指定我希望从归档中提取的文件的放置路径。如果我不提供此选项，归档将在我的 shell 当前所在位置提取。请记住，当我创建文件时，我指定了 /home/alberto。当 tar 创建归档时，它删除了开头的 /，以便归档可以提取到任何目录。出于选择，我将归档提取回 /，这将把所有文件放入 /home/alberto，有效地替换任何同名文件。

如果您提供的路径既不是绝对路径也不是相对路径，则被视为要提取的归档中的特定文件，tar 将只尝试提取此文件。唯一的注意事项是您需要知道归档中文件的路径。如果我知道我想恢复 /home/alberto/nsmail，我可以输入：

```
tar xvf bkup.tar home/alberto/nsmail
```

Tar 只会提取路径 home/alberto/nsmail，并将其放入当前目录（请记住，tar 默认会删除您提供的任何路径的起始斜杠 [/]）。





要访问内容，请点击章节和节标题。

## Linux 完全傻瓜指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 提取文件到设备

虽然创建 tar 文件很容易，但这并不是 tar 的用途。更重要的是，你可以直接提取到设备中。设备（通常是磁带驱动器）不会有文件系统，因此无法像访问磁盘那样挂载或访问它。但是，它会像文件一样存储数据。因此，如果你将数据 tar 到磁带或软盘，整个磁带或软盘将被视为一个大型 tar 文件。（可以在磁带上放置多个 tar 文件；我稍后会谈到这一点。）在软盘的情况下，你将无法挂载它，因为它没有可以存储文件的文件系统。（请记住，我们在第 7 章“使用磁盘”中讨论过挂载。）

## 将数据 tar 到设备

将数据 tar 到设备与将数据 tar 到文件相同。唯一的区别是归档的存储位置是代表备份硬件的设备的路径。你想要使用的基本设备是软盘和磁带驱动器。

### 软盘设备

要在软盘上创建 tar 文件，你使用 /dev/fd x 设备，其中 x 是你的软盘驱动器的编号。通常，如果你只有一个软盘，这将是 0，或者如果你有两个软盘，则是 0 或 1：

```
tar cvf /dev/fd0 /etc /home/alberto/nsmail
```

此命令会将 /etc 和 /home/alberto/nsmail tar 到软盘驱动器。它应该全部适合备份介质；如果不适合，你会收到错误。我将在本章后面的“跨多个磁盘或磁带”部分向你展示如何跨多个磁盘或磁带。

### 磁带设备

磁带驱动器通常挂载在两个不同的设备下（你的硬件可能指定其他名称）：

- `st`
- `rft`

`st` 设备对应 SCSI 磁带驱动器。`rft` 设备对应使用软盘控制器或“软盘-磁带”设备的磁带驱动器。（廉价的 PC 磁带驱动器，例如 QIC 类型驱动器，通常使用此选项。）与其他设备一样，可能不止一个，因此设备通过它们使用的驱动器编号来区分。

> **技术谈：**
> 如果你使用的是软盘磁带设备，你可能需要重新构建内核以提供对其的支持。如果你的磁带驱动器似乎不受支持，请查看第 24 章“自定义你的 Linux 内核”以获取如何操作的说明。

因此，SCSI 磁带的标准设备文件为 `/dev/st0` 和 `/dev/st1`。软盘-磁带驱动器的标准设备文件为 `/dev/rft0` 和 `/dev/rft1`。

因此，要备份到我的磁带设备（SCSI 驱动器），我输入以下命令：

```
tar cvf /dev/st0 /etc/alberto/nsmail
```

这些磁带设备的默认行为是在写入操作完成后倒带磁带。如果你的磁带驱动器能够存储几 GB 的数据，这可能会相当浪费，因为磁带的大部分可能仍然为空。出于这个原因，有不倒带的设备版本，允许你将多个文件放在同一磁带上。

不倒带的磁带设备为 SCSI 设备的 `/dev/nst0` 和 `/dev/nst1`，以及软盘-磁带设备的 `/dev/nrft0` 和 `/dev/nrft1`。当你使用这些设备向磁带写入时，磁带不会被倒带，从而允许你向其写入另一个归档。在每个文件之间，你会向磁带写入标记。你可以通过使用 `mt` 命令将磁带倒带和快进到所需的归档。

## mt 命令

`mt` 命令允许你对磁带执行许多操作，包括使用不倒带设备接口按文件（按其包含的归档）倒带和快进磁带。

要倒带磁带，使用以下语法：

```
mt /dev/nst0 rewind
```

要将磁带向前快进两个下一个归档，输入以下命令：

```
mt /dev/nst0 fsf 2
```

使用此命令的一个技巧是意识到 mt 没有当前归档的概念，因此你需要确保你有一份磁带上归档的列表。此外，作为健全性检查，你需要在将磁带向前快进之前发出倒带命令，以确保你是从磁带的开头开始计数。

同样，重要的是要记住磁带驱动器会在不同归档之间写入标记。这是 mt 用于检测不同归档的信息。在你从一个归档中提取数据后，为了处理其他归档，你需要通过发出以下命令将磁带向前移动到下一个归档：

```
mt /dev/nst0 fsf 1
```

无论如何，请不要替换磁带上的归档，除非你正在替换磁带的全部内容。你绝对不想做的是用一个较长的归档替换一个较短的归档，从而覆盖一个归档的开头。

## 从设备提取

从设备提取与从文件提取的方式基本相同：

```
tar xvf device path
```

如果不提供目标位置，所有文件都将提取到当前目录，同时保留其路径组织。如果提供绝对或相对路径，文件将被放置在那里。如果提供的路径既不是绝对也不是相对，则被视为要提取的归档中的文件。

从多归档磁带提取时，请记住使用不倒带接口和 mt 来快进磁带。

## 跨多个磁盘或磁带

如果要归档的文件不适合单个软盘或磁带，你需要为 tar 指定 M 选项。M 选项告诉设备跨多个磁盘或磁带。每个磁带或磁盘都是一个完整且独立的归档（唯一例外是任何磁盘或磁带上的最后一个文件可能被分割在磁盘或磁带之间）。这意味着你可以像处理自己的归档一样提取和处理每个磁盘或磁带。

要将我的 nsmail 目录备份到多个软盘，我输入以下命令：

```
tar cMvf /dev/fd0 /home/alberto/nsmail
```

当第一个软盘满时，它会要求你插入新的软盘。重要的是，你要按写入顺序对每个软盘或磁带进行编号，以便在提取时数据不会损坏。

要提取多卷归档，输入以下命令：

```
tar xMvf /dev/fd0
```

Tar 会按顺序要求每个卷（在这种情况下为软盘）。确保你拥有全部。

tar 的一个缺点是它不会跟踪需要备份的文件。为了使用 tar，你需要决定要备份哪些文件并向程序提供这些文件列表。虽然它提供了一些解决此限制的设施，但有更好的程序可用于此任务。如果你想进行增量备份并让程序跟踪需要备份的文件，你需要使用 dump。

## 备份策略

在 UNIX/Linux 下进行增量备份意味着使用 dump 实用程序。此实用程序功能强大。它可以处理跨多个磁带的备份并可以创建增量备份。如果你可以将整个备份放入单个磁带中，你将能够自动化备份。只需启动备份，让它运行即可。因为 dump 实际上会跟踪之前已转储的内容，并且只备份已更改的内容，所以你可以使用一些技巧来仅备份自安装系统以来添加和修改的项目（不包括“未配置”的操作系统）。

我的策略是在明确的时间进行备份：

- 系统软件安装后但在配置之前
- 系统软件安装并配置后
- 任何时候安装和配置了额外软件

使用此策略，事情的顺序是系统安装后立即备份系统。这是通过一个名为 /dev/null 的特殊设备文件完成的，该文件只是丢弃发送给它的任何数据。因为 dump 会跟踪上次转储的日期，后续备份将只存储在此日期之后修改过的内容。这是一个巧妙的技巧，因为你的备份集不会包含系统的软件发行版。这将为 dump 实用程序设置操作的时间起点。此转储的备份级别应为 0 级；它必须包含新安装系统中的所有内容。

Dump 使用级别的概念来确定要备份的内容。0 级（零）备份所有内容。1 级备份 0 级转储后修改的所有内容。2 级仅转储自上次较低级别转储以来更改的备份项目，以此类推。

后续备份应以 8 级或 9 级执行。这将有效地备份自第一次备份以来机器中修改过的所有内容。





要恢复使用 `dump` 实用程序创建的磁带上存储的文件，请使用本章后面所述的 `restore` 程序，见“`restore` 命令”一节。

使用本网站须遵守特定条款和条件。版权所有 © 1996-2000 EarthWeb Inc. 保留所有权利。未经 EarthWeb 明确书面许可，不得以任何形式或媒介全部或部分复制。

要访问内容，请单击章节和节标题。

## Linux 完全傻瓜指南

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## dump 命令

`dump` 实用程序默认未安装在您的系统上，但包含在您的 CD 上。在 col/install/rpms 目录中，它应命名为类似 dump-x.i386.rpm，其中 x 将是与程序版本相关的某些数字。要安装程序，请访问 CD 上的 col/install/rpms 目录。作为 root，发出以下命令：

```
rpm -i dump*.rpm
```

`dump` 命令使用以下语法：

```
/usr/etc/dump [options[argument ...]
filesystem]
```

`dump` 命令通过为每个备份分配一个级别来跟踪备份的范围。级别范围从 0 到 9。级别 0 复制整个文件系统。后续的 dump 级别仅复制自最近一次具有更低级别编号的 dump 以来已更改的文件。

典型的策略是以级别 0 dump 开始，然后定期进行增量备份。应极其谨慎地执行级别 0 dump；它们应在单用户模式下运行机器，并且在 dump 之前应运行 fsck（文件系统一致性检查器）以验证文件系统是否一致。这很重要，因为如果您不打算用 CD 替代级别 0 备份，您恢复的大多数文件将来自 dump 级别 0 磁带！有关更多信息，请参阅 fsck 和 dump 手册页。

值得注意的一个缺点是 `dump` 无法备份单个目录或文件；它只能用于备份整个文件系统。要备份单个文件或目录，请使用 tar 或 cpio。有关如何使用这些程序的信息，请参阅您的 Linux 文档。

### Techno Talk：以单用户模式启动

Linux 可以以单用户模式启动。此设置跳过所有系统配置，并在询问您的 root 密码后启动 root shell。此模式仅应用于特殊维护任务，例如执行级别 0 dump 或其他紧急类型任务。要以单用户模式启动系统，在启动提示符下，键入 Linux 映像的名称（按 tab 查看可用映像列表）后跟单词 single。

正在运行的系统也可以使用 shutdown 命令“降级”到单用户模式，不带 -r（重启）或 -h（停止）选项，通过在命令提示符下发出以下命令：

```
shutdown now
```

片刻后，您将被要求输入 root 密码，然后您将被“丢弃”到单用户模式。

请注意，在一种硬件/软件配置下创建的磁带通常不能移植到其他操作系统或驱动器。在某些环境中，甚至使用旧版本 dump 程序创建的磁带也无法被 restore 程序的新版本读取。因此，在升级时测试您的备份，并保留旧版本的程序。

## 磁带容量

`dump` 的一个问题是它不会为您计算磁带可以容纳多少数据。因此，您需要自己计算容量，以便正确使用磁带。

这似乎很容易——但事实并非如此。每种磁带系统都有不同的密度（每英寸磁带可写入的数据量）。磁带长度不同，且 dump 根据九轨磁带以 1600 字节/英寸运行且默认磁带长度为 2300 英尺来计算所有这些设置。听起来很 confusing？不要放弃。

计算您的磁带驱动器容量的基本数学如下：

- 1. 写下磁带的容量（GB），（确保您不使用压缩容量用于此目的，因为该“最大”容量将取决于您的数据可压缩性！如果您的磁带容量以兆字节为单位表示，将该容量除以 1024。
- 2. 将您的磁带长度转换为英寸。如果您的磁带长度以米为单位，将其乘以 39.37 以获得英寸数。如果您的磁带长度以英尺为单位，将此数字乘以 12。
- 3. 将步骤 1 中的磁带容量乘以 1,073,741,824 以获得磁带以字节为单位的容量。
- 4. 将步骤 3 的计算结果除以步骤 2 中计算的数字。这就是您的磁带密度。
- 5. 将步骤 3 中的数字除以 32,768。这就是您的磁带能够容纳的 32K 块数。
- 6. 将步骤 5 计算的数字乘以 21.18。这就是基于 1600 字节/英寸的磁带大小。
- 7. 将步骤 6 中的数字除以 12 并舍去任何小数部分。这就是您应为 dump 指定的磁带长度。

以下是一个 90m 1.95GB DDS 磁带的示例：

- 1. 磁带容量（GB）：1.95GB
- 2. 磁带长度（英寸）：90m × 39.37 = 3,543
- 3. 磁带容量（字节）：1.95 × 1,073,741,824 = 2,093,796,556
- 4. 磁带密度：2,093,796,556 / 3,543 = 590,967
- 5. 磁带 32K 块容量：2,093,796,556 / 32,768 = 63,897
- 6. 磁带大小（按 1600 字节/英寸）：63,897 × 21.18 = 1,353,338
- 7. 调整后的磁带长度（英尺）：1,353,338 / 12 = 112,778

哇！在磁带密度可以通过查询设备自动计算的世界里，似乎很傻要做这个。但嘿，这个程序最初是在很久以前完成的，并且鉴于不同类型的磁带设备（SCSI 或其他），开发这项任务也可能具有挑战性！另外，请记住检查您制造商的网站。它可能发布了如何使用其硬件与 dump 的信息。

无论如何，请记住写下这个数字并将其贴在驱动器的底部。这样您就不会再次计算它。如果您手边没有计算器，请记住 KDE 有一个应该可以正常工作。

## dump 示例

以下命令将在由 -f 标志指定的设备上（在本例中为 /dev/nst0）创建级别 0 dump（由 0 表示），针对指定的磁盘 /dev/hda1（请参阅 /etc/fstab 以获取您的磁盘设备名称）：

```
dump -0u -f /dev/nst0 -s 112778 /dev/hda1
```

用您磁带设备的适当名称替换 nst0，并用您的根分区使用的设备替换 hda1。此 dump 将包括设备上找到的所有文件。如果您有额外的磁盘，您将必须为每个磁盘再次运行 dump。如果您指定 u 选项并且备份成功完成，dump 将记住此备份的日期、时间和级别。这有效地设置了一个起点，可用于评估下次需要转储哪些文件。

要创建仅包括自上次较低级别备份以来修改过的文件的增量备份，在本例中为 0，请使用更高级别的 dump：

默认情况下，dump 将其输出写入默认磁带单元；您需要记住指定 -f 选项，后跟您的磁带驱动器的设备。

您可以使用 -f 选项将备份重定向到文件：

```
dump -9uf /tmp/backup /dev/hda1
```

前面的命令将在 /tmp 目录中创建一个名为 backup 的文件。要将 dump 的输出重定向到 STDOUT（标准输出），请指定破折号 (-) 而不是文件名：

```
dump -9uf - /dev/hda1 | gzip > /dev/st0
```

在前面的示例中，dump 的输出被发送到 STDOUT 并通过管道传输到 gzip（见第 20 章，“安装程序和应用程序”）程序进行压缩。如果您的磁带不提供硬件压缩，使用前面的命令可以有效增加磁带容量。

有关 dump 提供的众多选项的完整信息，请阅读您系统的文档。

## restore 命令





要提取使用 dump 备份的文件，请使用 restore。restore 会将存储在 dump 磁带或文件中的文件复制到当前目录。需要注意的是，使用 restore 会覆盖同名已存在的文件。restore 在提取文件之前也会创建所需的任何目录或目录树。如果您知道自己在做什么，此功能非常强大。如有疑问，请将文件使用 restore 提取到一个空目录，然后手动移动文件。restore 的语法如下：

```
restore [options [argument ...]]
```

要指定备份所在的设备，请使用 -f 选项并在其后跟上 dump 的位置。

restore 命令具有易于使用的交互式 shell 类似界面，允许您像在文件系统一样浏览 dump 磁带。通过使用 -i 选项启动交互式会话：

```
restore -f /dev/nst0 -i
```

当 restore 加载后，您可以使用诸如 cd 和 ls 之类的命令在磁带目录中移动。这些命令是 restore 内置的，与 shell 中使用的命令不同。

要将文件添加到要提取（恢复）的文件列表中，输入 add filename，其中 filename 是您要提取的文件名。如果添加一个目录，其包含的所有文件和目录都会被添加。要从列表中删除文件，输入 del filename。此命令不会从磁带中删除文件；它只是将其从提取列表中移除。要提取文件，只需输入 extract。提取结束时，会询问您是否要为 '.' 设置所有者/模式？[yn] 您应回答 no，因为这可能会更改 restore 将要提取文件的目录的所有者和模式。

下面是一个示例会话：

```
1: [root@digital /tmp]# restore -i -f /dev/nst0
2: restore > ls
3: :.
4: auto/ dev/ etc/ home/ root/ tmp/ var/
5: restore > add home
6: restore > ls
7: :.
8: auto/ dev/ etc/ *home/ root/ tmp/ var/
9:
10: restore > del home
11: restore > ls
12: :.
13: auto/ dev/ etc/ home/ root/ tmp/ var/
14:
15: restore > cd home/alberto/test
16: restore > ls
17: ./home/alberto/test:
18: afile
19:
20: restore > add afile
21: restore > extract
22: You have not read any tapes yet.
23: Unless you know which volume your file(s) are on you should start
24: with the last volume and work towards the first.
25: Specify next volume #: 1
26: restore > quit
27: [root@digital /tmp]# ls
28: home
29: [root@digital /tmp]# cd home/alberto/test
30: [root@digital test]# ls
31: afile
```

我使用的 Linux 版本附带的 restore 有一个问题。如果您尝试添加一个文件，它会给出错误信息。解决方法是添加一个目录，例如 home（参见上一列表的第 5 行）。请注意，当您添加文件或目录时，restore 会在旁边放置一个星号 (*) 来标记它（参见第 8 行）。添加此目录后，删除它（参见第 10 行）。然后您可以按需添加文件。父目录将被自动添加。当您完成文件选择后，输入 extract（参见第 21 行）。Dump 会要求您读取磁带。如果您的 dump 仅跨越一个磁带，输入 1；否则，输入用于此 dump 的最后一个磁带的编号。要获取 dump 的信息，输入 what。要获取交互式 restore 的帮助，输入 help 或 ?，它会打印以下信息：

```
restore > ?
Available commands are:
    ls [arg] - list directory
    cd arg - change directory
    pwd - print current directory
    add [arg] - add `arg' to list of files to be extracted
    delete [arg] - delete `arg' from list of files
        to be extracted
    extract - extract requested files
    setmodes - set modes of requested directories
    quit - immediately exit program
    what - list dump header information
    verbose - toggle verbose flag (useful with `ls')
    help or `?' - print this list
If no `arg' is supplied, the current directory is used
```

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## restore Examples

交互式恢复比使用命令行更容易。然而，您也可以这样做。要恢复特定文件，请指定 -x 选项并提供相对于根的路径，如下所示：

```
restore -x home/alberto/file.rtf -f /dev/nst0
```

前面的命令将提取 (-x) 指定的文件 (/home/alberto/file.rtf) 从磁带到当前目录。如果目录路径不存在，restore 将创建它们。最好将目录更改为 /tmp，这样恢复的文件会进入安全位置，并且不会覆盖现有文件。文件恢复后，您可以将文件移动到最终目的地。

要从 dump 磁带上的文件创建目录列表，请使用 -t 选项。除非您知道磁带驱动器支持读写后验证，否则最好始终从磁带创建目录列表。这将确保您制作的备份磁带包含正确的信息并且磁带可读。

要创建目录列表，输入以下内容：

```
restore -t -f /dev/nts0 > tapecat.txt
```

这将创建一个名为 tapecat.txt 的文件，其中包含磁带上文件的列表。

## Graphical Backup Programs

有几个图形备份程序可用：BRU2000，包含在您的 CD 上，以及 KDat，一个 KDE 备份应用程序（有关 KDat 的更多信息，请访问 http://www.kde.org）。

## BRU2000

目前，OpenLinux 包含 BRU2000 的许可证，这是一个可以通过命令行和图形界面执行类似 dump 的系统备份的程序。与 dump 相比，其最大的优势在于使用其图形用户界面，因此易于使用。无需担心磁带大小和其他棘手细节，这可能非常值得。程序的使用是自解释的。您首先选择备份设备（/dev/nst0 或适用于您的设备）。要创建备份设备，只需在文件菜单下使用新建设备命令。在选择备份设备后，您需要从选项菜单下的备份命令中选择备份选项。对话框将要求各种设置。然后点击备份按钮。这会提示您选择要备份的文件。从那里，点击开始备份按钮，您就可以开始了。

与 dump 一样，BRU 支持增量备份，因此您可以实施“备份策略”一节中讨论的备份策略。

以下是该程序的一些屏幕截图：

![](img/edf072a03d4de1f8f4a13465ac79e7fb_242_0.png)

![](img/edf072a03d4de1f8f4a13465ac79e7fb_242_1.png)

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Chapter 20
Installing Programs and Applications

## In This Chapter

- RPM: The Red Hat Package Manager
- Installing, Upgrading, Downgrading, and Removing Software
- Verifying Your System
- Graphical Front Ends to RPM
- Non-RPM Packages

通过使用 RPM，Linux 上的软件安装相当复杂。尽管您可以安装由 tar 和其他程序归档的软件，但大多数时候您希望安装 RPM 包。毋庸置疑，当您可以选择要安装的包格式时，请选择 RPM 版本。RPM 包提供了众多好处，这就是为什么我们会详细介绍它。

## RPM: The Red Hat Package Manager

RPM 是一个开放的软件和源代码打包系统。它最初为 Linux 开发，但此后已在 GPL 下向任何人提供使用。

RPM 是一个很棒的打包系统，因为它不仅像其他系统多年来所做的那样处理软件安装，而且还维护一个数据库



已安装的软件及其相互依赖关系。此数据库可搜索，因此您可以查找文件属于哪个软件包，甚至可以检查文件自初始安装以来是否已被修改、意外损坏或删除。就依赖关系而言，RPM 确保您安装其他软件运行可能需要的任何必需软件包。

RPM 可以通过 FTP 工作，因此您无需下载软件即可安装它；RPM 可以同时完成这两项工作。它还管理着配置文件，因此当您升级软件或系统时，这些自定义设置会得以保留。这是自升级开始以来所有操作系统和软件安装一直存在的问题。

对于开发人员和程序员，RPM 允许将二进制文件（程序）和源代码打包供用户使用。如果开发人员修改了程序的源代码，这些称为“补丁”的内容会与“原始”或原始源代码分开维护。这使得升级基本源并将补丁重新应用到新版本变得容易。

对于管理员，RPM 允许他们升级系统，而无需重新安装所有内容然后进行配置。RPM 能够高效地仅升级已更改的软件包，而不会丢失您的自定义设置。

有关 RPM 的最新信息，请访问 Web 上的 http://www.rpm.org。

## 安装、升级、降级和删除软件

仅凭您可以在系统上安装、升级和降级软件，并在无需手动操作的情况下将其从系统中删除这一事实，就足以成为安装 rpm 软件的理由。

## 安装

安装软件包极其简单。以下是语法：

```
rpm -i mypackage-1.0-2.i386.rpm
```

通常，您可能需要具有 root 权限才能安装软件包。RPM 会负责安装所有内容——软件和文档——将所有内容放在正确的位置。

安装时可能会出现一些错误。如果 RPM 检测到新软件包将覆盖另一个软件包的文件，它会通知您冲突。要覆盖，可以提供 --replacefiles 选项：

```
rpm -i --replacefiles mypackage-1.0-2.i386.rpm
```

如果软件包依赖于另一个软件包，您会看到一个错误，提示该软件包需要另一个软件包。您应该获取所需的软件包，然后重试软件的安装。您也可以使用 --nodeps 选项覆盖此警告；但是，这样做会给自己带来问题。

如果软件已经安装，您会收到一个错误，提示该软件包已安装。要覆盖安装该软件包，您应提供 --replacepkgs 选项，如下所示：

```
rpm -i --replacepkgs mypackage-1.0-2.i386.rpm
```

## 升级

升级应用程序与安装一样简单。不是指定 -i 选项，而是指定 -U 选项，如下所示：

```
rpm -U mypackage-1.0-4.i386.rpm
```

需要记住的是，升级软件包实际上会卸载之前的安装。如果升级版本的配置文件不兼容，您会看到一条消息告知您。RPM 会为您保存原始配置文件，以便您与新文件进行核对。

## 降级

有时升级实际上是升级到新的不良错误。要降级回您在获取错误之前使用的软件，只需升级到旧软件包并提供 --oldpackage 选项即可。

```
rpm -U --oldpackage myoldpackage-1.0-1.i386.rpm
```

## 卸载

如果您发现自己不需要已安装的软件，请使用 -e（Erase）标志。这次，只提供软件包的基本名称。对于名为 mypackage-1.0-4.i386.rpm 的软件包，只需输入以下内容：

```
rpm -e mypackage
```

## SPIDER KILLER

## spider catcher

HOME ACCOUNT INFO SUBSCRIBE LOGIN SEARCH MY ITKNOWLEDGE FAQ SITEMAP CONTACT US

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Bookmark It

Search this book:

Previous Table of Contents Next

## 已安装软件的数据库

RPM 中最有趣的功能是能够查询有关系统上已安装文件和软件包的信息。此功能非常强大，因为您可以查询 RPM 以搜索已安装软件列表中的许多内容。查询（搜索）使用 -q 选项进行。

## 查找有关软件包的信息

要查找有关软件包文件的信息，请对软件包执行 rpm 查询。您应输入以下内容：

```
rpm -qip packagefile
[alberto@digital alberto]$ rpm -qip DUMP-0_4.RPM
Name        : dump                          Distribution: OpenLinux 1.2
Version     : 0.4b4                          Vendor: Caldera, Inc.
Release     : 1                              Build Date: Wed Jan 07
                                            01:15:34 1998
Install date: (not installed)                Build Host: '
                                            buildmeister.caldera.com
Group       : Administration/Archiving      Source RPM: dump-0.4b4-1.
                                            src.rpm
Size        : 295767
Packager    : Raymund Will <ray@lst.de>
Summary     : BSD dump/restore backup system (BETA).
Description :
 dump and restore, as known from BSD/SunOS/..., is a quite
 reliable method for backup, because 'dump' gets all needed
 information directly from the storage media -- not via
 the high-level filesystem-interface (as tar, cpio, etc. do).

 Additionally the output format of dump is readable on
 other platforms (like SunOS, BSD) and vice versa.

 But BEWARE, this software is still under development (BETA)!!!
 Don't rely too much on it -- but without testing, there would be
 no further improvement! Interleave with another backup method
would be a good idea.

## 查找拥有文件 的软件包

如果您想知道文件来自哪个软件包，请输入以下命令：

```
rpm -q -f filepath
[alberto@digital alberto]$ rpm -q -f /sbin/restore
dump-0.4b4-1
```

## 查找由软件包拥有的文件

要查看软件包拥有的所有文件，只需输入以下内容：

```
rpm -q -l packagename
[alberto@digital alberto]$ rpm -q -l dump
/etc/dumpdates
/etc/rmt
/sbin/dump
/sbin/rdump
/sbin/restore
/sbin/rmt
/sbin/rrestore
/usr/doc/dump-0.4b4-1
/usr/doc/dump-0.4b4-1/CHANGES
/usr/doc/dump-0.4b4-1/COPYRIGHT
/usr/doc/dump-0.4b4-1/KNOWNBUGS
/usr/doc/dump-0.4b4-1/THANKS
/usr/doc/dump-0.4b4-1/TODO
/usr/doc/dump-0.4b4-1/dump-0.4b1.announce
/usr/doc/dump-0.4b4-1/dump.lsm
/usr/man/man8/dump.8.gz
/usr/man/man8/rdump.8.gz
/usr/man/man8/restore.8.gz
/usr/man/man8/rmt.8.gz
/usr/man/man8/rrestore.8.gz
```

## 查找与软件包相关的文档

假设您想了解与特定软件包一起安装的所有文档来源。RPM 也能在这里提供帮助。只需输入以下内容：

```
rpm -q -d packagename
[alberto@digital alberto]$ rpm -q -d dump
/usr/doc/dump-0.4b4-1
/usr/doc/dump-0.4b4-1/CHANGES
/usr/doc/dump-0.4b4-1/COPYRIGHT
/usr/doc/dump-0.4b4-1/KNOWNBUGS
/usr/doc/dump-0.4b4-1/THANKS
/usr/doc/dump-0.4b4-1/TODO
/usr/doc/dump-0.4b4-1/dump-0.4b1.announce
/usr/doc/dump-0.4b4-1/dump.lsm
/usr/man/man8/dump.8.gz
/usr/man/man8/rdump.8.gz
/usr/man/man8/restore.8.gz
/usr/man/man8/rmt.8.gz
/usr/man/man8/rrestore.8.gz
```

现在您知道要为您的软件包阅读什么了！

## 验证您的系统

很多时候您可能需要能够检查文件或应用程序，甚至整个系统是否存在损坏的迹象。RPM 会跟踪校验和（一种计算出可用于确定文件内容是否更改的唯一数字的复杂计算）。通过发出一个简单的命令（rpm -Va）您可以验证整个系统！

如果 RPM 打印出某些内容，很可能该软件包需要重新安装。如果您看不到任何消息，则验证过程成功。指定 rpm -Vf 将仅验证单个文件。请注意，您修改的一些配置文件将被列出，但这是正常的。

要将已安装的软件包与软件包文件进行比较，您将输入 rpm -Vp fullpackagename，如以下示例所示

```
rpm -Vp mypackage-1.0-4.i386.rpm
```

## RPM 的图形前端

有几个 RPM 的图形前端可用：一个是 KDE 环境的一部分，称为 kpackage（kpackage-0.9.02-1.i386.rpm；请参阅下图），另一个称为 glint（glint-2.3-3.rpm）。虽然拥有 UI 版本的程序是朝着正确方向迈出的一步，但命令行工具提供了 UI 中无法访问的许多功能。出于这个原因，我将介绍该程序的命令行版本。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_248_0.png)

这是 kpackage 工具的屏幕截图。它为安装 RPM 软件包提供了一个不错的前端；然而，它缺乏 RPM 程序提供的许多强大的查询功能。





## Linux完全傻瓜指南

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

## 非 RPM 包

虽然 RPM 很棒，但有时你要安装的软件不会以 RPM 包的形式提供。像 http://sunsite.unc.edu/pub/Linux/distributions/redhat/contrib/i386/ 这样的 FTP 站点上有大量已经打包成 RPM 的程序，所以你应该先去那里查看你需要的东西是否已以包格式提供。

如果没有，很可能它会以 tar 或压缩 tar 文件的形式提供。关于使用 tar 程序进行备份的讨论在第 19 章“备份：保护你的工作”中有详细说明。如果你需要安装一个不以 RPM 格式打包的程序，最好将此程序安装到 /opt 目录下的独立目录中。/opt 目录主要包含第三方软件，例如 KDE、Netscape 等。为了使程序对 shell 可见，你可以在 /opt/bin 目录中为其可执行文件创建一个链接。如果该目录不存在，你应该创建它并将其添加到你的 PATH 环境变量中。

## Tar

要从 tar 文件中提取文件，请按以下步骤操作：

- 1. 创建一个用于存放归档文件内容的目录。tar 文件可能会将许多文件散布到当前目录，因此最好创建一个新目录来接收文件。
- 2. 将 tar 归档移动到目标目录。
- 3. 使用 cd 进入该目录。
- 4. 使用 tar 提取文件：tar xvf afile.tar。

如果制作 tar 文件的人足够细心，将所有文件都放在一个目录中，你就准备好了。有时 tar 文件会包含一个名为 install.sh 或其他安装脚本的文件。请按照任何自述文件中的说明进行操作（使用 less 等分页器查看它们）。

## UNIX 压缩归档：Gzip 和 Compress

很多时候 tar 文件会以压缩格式分发；压缩文件的典型扩展名为 .gz（gnu zip 或 gzip）、compress 程序的 .Z 以及 Windows zip 压缩归档的 .zip。如果文件名为 file.tar.gz，则该文件是 gnu zip 压缩的 tar 文件。要提取它，你需要向 tar 指定 z 选项：

```
[alberto@digital /tmp]$ tar -xzvf file.tar.gz
nsmail/
nsmail/Drafts
nsmail/.Drafts.summary
nsmail/Trash
nsmail/.Trash.summary
nsmail/Sent
nsmail/.Sent.summary
nsmail/Unsent Messages
nsmail/.Unsent Messages.summary
nsmail/Inbox
nsmail/.Inbox.summary
```

另一种完成相同任务的方法是使用管道使用 gzcat 程序（类似于 cat）。该程序读取压缩归档中的信息，对其进行解压缩，然后将其复制到 STDOUT。以下是如何将 gzcat 和 tar 一起使用的示例：

```
gzcat file.tar.gz | tar -xf -
```

在此示例中，gzcat 将结果输出，即一个 tar 文件，通过管道传递给 tar 程序。tar 程序会在其 STDIN 流中查找数据，因为 - 提供了给 f 选项作为参数。

另一种方法是先解压缩 gzip 文件，然后再正常使用 tar。这效率更低，如果磁盘空间不足，可能会导致空间耗尽：

```
gunzip file.tar.gz; tar -xf file.tar
```

gunzip、gzcat 和 tar 的 z 选项可以处理 .gz 或 Z 扩展名的文件。如果你找到一个非常旧的归档，你可能会发现它带有 .z 扩展名；这也是一个 gzip 压缩文件。

如果文件不是用 tar 压缩的，它只是带有 .gz 扩展名。你可以使用 gunzip 来解压缩它，如下所示：

```
gunzip file.gz
```

## Windows 压缩归档：Zip

zip 归档格式（.zip）最初由 Phil Katz 为 DOS 开发，现已被几乎每台 Windows 计算机使用。Linux 用户也可以使用 unzip 和 zip 工具提取和创建这种文件格式。

要解压文件，只需使用 unzip 命令：

```
[alberto@digital /tmp]$ unzip file.zip
Archive:  file.zip
  creating: nsmail/
 extracting: nsmail/Drafts
  inflating: nsmail/.Drafts.summary
  inflating: nsmail/Trash
  inflating: nsmail/.Trash.summary
  inflating: nsmail/Sent
  inflating: nsmail/.Sent.summary
 extracting: nsmail/Unsent Messages
  inflating: nsmail/.Unsent Messages.summary
  inflating: nsmail/Inbox
  inflating: nsmail/.Inbox.summary
```

## 第 21 章
LISA: Linux 安装和系统管理实用程序

## 本章内容

- LISA 的基本功能
- 详细系统分析
- 软件包管理
- 系统配置
- 网络配置区域

Caldera OpenLinux 包含一个名为 LISA 的管理和配置工具。LISA 为用户管理、软件包安装和系统配置提供接口。其中一些任务在其他部分有描述，因为直接使用主机程序比通过 LISA 使用它们更快、更强大。LISA 不是自由分发的软件，因此不是其他 Linux 发行版的常见组成部分。对于简单网络，它提供了对系统和软件配置的各个常见方面的访问。

要使用 LISA，你必须以 root 身份登录。LISA 通过控制台提供 UI；因此，即使你没有使用 X Window 系统，也可以进行系统配置。导航和操作是通过使用箭头键选择命令选项来完成的。Enter 键用于选择所选命令，Esc 键用于向上返回一级或退出程序。在显示控件的屏幕上，你可以使用空格键标记突出显示的选项。

## LISA 的基本功能

LISA 将其功能分为三个类别：

- 系统分析
- 软件包管理
- 系统配置

该实用程序还提供了一个帮助系统，讨论了系统管理员感兴趣的多个主题。你应该浏览此部分以获取更多信息和帮助资源。

以下是启动时显示的主屏幕。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_253_0.png)

主 LISA 屏幕。使用箭头键突出显示一个类别并按 Enter 进入。按 Esc 退出程序。要查看有关使用 LISA 的在线帮助，请按 F1。可以通过按 F2 获得有关当前选择的详细信息。

## 详细系统分析

系统分析区域可以为你提供有关硬件和配置设置的信息。这些信息对于评估当前硬件和配置设置非常有用。

系统分析区域细分为几个其他区域：

- **自动系统分析**：此区域显示基本系统信息，例如系统上次启动时间、当前负载、主机名以及计算机的 IP 地址。
- **自动内核分析**：内核分析显示系统当前使用的内核信息。它包括内核版本、构建者、用于构建的编译器、支持的文件系统和当前设备等信息。
- **自动硬件分析**：硬件区域显示有关硬件的更详细信息，例如已安装的处理器的类型、RAM 数量、交换磁盘的大小、有关显卡、磁盘驱动器、PCMCIA 和其他硬件设备的信息。
- **自动分区分析**：此区域显示计算机中磁盘分区的信息。它按设备名称列出分区，并为每个分区提供大小和类型。
- **自动网络分析**：网络区域提供



有关您的网络设备和配置的信息。它显示了以太网设备处理的流量信息以及详细的配置信息（IP、网络掩码、广播地址等）。
此外，它还显示当前的路由表。（此信息显示数据包如何从您的计算机转发到其他网络。）

- **显示启动过程消息**：此区域显示上次启动的启动消息。在安装新内核后检查此区域可以告诉您硬件是否被正确识别。当计算机启动时，很难跟上这些消息，因为它们滚动得太快。此信息也可以从 `/var/log/messages` 获取，但该文件包含每次启动以及其他运行信息。启动过程区域更为简洁。
- **显示脚本配置文件**：此区域显示 `/etc/lst.cnf` 文件。该文件包含软件包用来查找有关系统信息的资料。您不应手工编辑此文件。它会根据您的兴趣提供有趣或无聊的阅读内容。
- **显示系统配置文件**：此区域显示另一个配置文件 `/etc/system.cnf`，系统用它来配置自身。您不应手工更改此文件。

## 软件包管理

此区域是 RPM 的前端（在第 20 章“安装程序和应用程序”中讨论）。您可以使用 LISA 执行与使用 RPM 相同的任务。对于新手用户来说，这可能是一种更简单的方式来执行这些任务。

软件包管理区域细分为四个部分：

- **选择安装源**：这允许您选择 RPM 软件包的来源。您可以使用本地硬盘上的路径或特定 CD-ROM，或通过网络经 NFS 可用的方式安装软件包。截至本文撰写时，Caldera 在 IP 207.179.39.2 上提供了一个公共 NFS 服务器；路径为 `/OpenLinux-1.3`。如果您有足够的带宽，可以使用此方法升级和安装新软件包。此安装方法依赖于快速的网络访问，因此通过调制解调器的 PPP 连接可能不够快。
- **有关可用软件包的信息**：此区域显示一个列出所有已安装软件包的屏幕。选择其中一个以查看详细信息。这类似于进入 RPM 并发出 `rpm -qi packagename`。
- **安装额外的软件包**：如果您提供安装路径（CD-ROM 或 NFS）卷，则可以使用此区域安装额外的软件包。这是 RPM 的安装界面。
- **删除已安装的软件包**：这是 RPM 的卸载界面。

## Linux 完全傻瓜指南

出版社：Macmillan Computer Publishing
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

## 系统配置

系统配置区域提供了一个配置系统的简化界面。这比直接处理配置文件要容易得多。像往常一样，您应该了解自己在做什么，否则可能会使系统无法启动。

系统配置区域细分为四个主要区域：

- 硬件配置区域
- 系统配置区域
- 网络配置区域
- 启动管理器配置

### 硬件配置区域

硬件配置区域为配置磁盘、键盘、调制解调器、鼠标、打印机、磁带驱动器和 X11 服务器提供其他配置屏幕：

- **软盘驱动器：** 提供指定已安装驱动器的选项。
- **硬盘：** 提供配置磁盘、更改分区信息和格式化新磁盘的选项。
- **键盘映射：** 允许您选择键盘区域映射。
- **调制解调器：** 允许您选择调制解调器类型和配置。
- **鼠标：** 选择并配置您的鼠标。
- **打印机：** 您可以在此区域轻松向系统添加打印机。提供了更受欢迎打印机的打印机驱动程序。如果您的打印机未列出，请不要绝望。选择您制造商的类似型号可能就能解决问题。另外，请查看 http://www.caldera.com 以获取更多打印机配置技巧和说明。
- **CD-ROM：** 提供可供 Linux 使用和配置的 CD-ROM 列表。
- **串行磁带机：** 允许您配置磁带备份驱动器。
- **X11 服务器：** 允许您为显卡选择合适的 X11 服务器并创建自定义配置文件。

### 系统配置区域

系统配置区域提供以下界面的接口：

- **用户管理：** 您可以添加、删除和管理用户和组，以及为通过 LISA 添加的用户设置默认值。此界面对于新手用户非常实用。LISA 用户管理区域目前尚未利用 UPG 方案，后者可简化用户协作。有关更多信息，请参阅第 18 章“用户、组和密码”。
- **配置挂载表：** 这为您提供了一个修改 `/etc/fstab` 文件以添加网络挂载的界面。
- **配置交换区：** 此区域允许您格式化指定为交换分区的分区并将其添加到交换区列表中。Linux 支持多个交换分区。
- **设置主机名：** 为您提供分配机器主机名的界面。此处输入的信息会在启动时通过脚本传播。这是设置计算机名称和域的首选方式。使用完全限定域名，例如 `host.domain.dom`。
- **配置时区：** 允许您配置应如何读取计算机上的硬件时钟。如果您有双启动计算机，很可能您的其他操作系统（OS）将时钟设置为本地时间。UNIX 和类 UNIX 系统通常将时钟设置为格林威治标准时间（GMT），然后根据您的时区计算本地时间。通过此控件，您可以告诉 Linux 如何读取您的时钟，以便您可以与其他操作系统共享。
- **配置守护进程/服务器自动启动：** 此屏幕允许您启用和禁用在计算机启动时启动的服务。如果您未使用某项服务，最好将其关闭，以节省资源。您只应禁用您确定对计算机的正常使用不必要的项目，否则会出现一些故障。
- **内核模块管理：** 此区域显示内核可用的模块信息。在此您可以添加和删除模块。显示的模块名称很晦涩，因此熟悉模块会有所帮助。您应该查看第 24 章“自定义您的 Linux 内核”。熟悉内核配置程序可能会有所帮助。

## 网络配置区域

此区域配置各种网络选项，从网络卡到您在网络上协作所需的服务。基本子区域如下：

- 将计算机添加到主机表
- 配置网络访问
- 配置通用网络服务

### 主机表配置

此选项允许您通过界面查看和操作 /etc/hosts 文件。它具有以下命令

- 显示当前的 /etc/hosts 文件
- 向 /etc/hosts 文件添加新条目
- 从 /etc/hosts 文件中删除条目

/etc/hosts 文件跟踪网络上的计算机，以便用户可以通过名称而不是 IP 地址引用它们。如果您的网络很大，您将不会使用 /etc/hosts；您将使用域名系统（DNS）系统来提供名称到 IP 和 IP 到名称的转换。如果没有 /etc/hosts 文件或 DNS 提供的此类转换服务，您将需要知道您想要通信的每台机器的 IP 地址。

如果您有一个小型网络（用于家中几台 PC 的微型局域网，或 TAN），您可以使用 /etc/hosts 来提供您的



Linux 机器需要能够通过 TCP/IP 访问你的其他计算机。 （请注意 LAN 并不是一个技术术语，但我投票认为它应该是。许多家庭开始将多台计算机用线连接在一起。）

## 网络访问配置

网络访问配置区域允许你配置以太网卡并输入路由器信息。

它提供两个选项：

- 配置网络卡
- 输入路由器

有关你的网络的信息应使用此组件添加或修改。

## 通用网络服务配置

通用网络服务配置区域允许你配置网络卡、基本网络服务如 DNS、NIS 和电子邮件。

它有三个子区域：

- **配置域名服务：** 此区域允许你定义你的 DNS 服务器。
- **配置 NIS：** 这允许你配置你的工作站以使用 NIS（网络信息服务）作为客户端或作为服务器。
- **选择邮件传输代理：** 此区域允许你配置你首选的邮件传输代理。目前它只提供一个选项：sendmail。

## 启动管理器配置

此区域显示有关 lilo（Linux Loader）的信息。在具有多个分区的系统上，这将允许你配置启动分区和其他设置。你将在第 24 章学习有关 lilo 的内容。

## 完全傻瓜 Linux 指南

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

要访问内容，请点击章节和节标题。

搜索本书：

## 第 22 章
系统监控：关注你的系统

## 本章内容

- 监控内存
- 监控进程
- 监控你的磁盘
- 日志文件

你的系统上运行着许多进程。在本章中，你将概述如何监控和控制你的系统正在做什么的工作。对于大多数情况，除非你怀疑存在问题或试图弄清楚如何微调你的系统，否则你不需要使用这些命令。尽管如此，很酷的是知道你可以查看不同的东西来确定性能或安全方面的问题，或只是关注正在发生的事情。

就性能而言，Linux 作为操作系统来说相当精简高效。事实上，它让许多其他昂贵的操作系统相形见绌。虽然额外的 CPU 速度无疑会使你的计算机更快，但额外的 RAM 可能在你认为事物发生的速度方面产生更大的影响。能最慢化你的计算机的单一因素是同时运行的程序没有足够的 RAM。Linux 在 RAM 不足时会通过交换来应付。

交换将当前在计算机内存（RAM）中的数据和程序复制到磁盘上，这被称为虚拟内存。这为计算机的真实内存（RAM）腾出空间，让另一个进程做它需要做的事情。当被交换的任务需要再次执行时，Linux 内核会将其放回 RAM，交换出其他进程。你可以运行的进程和任务的数量取决于你分配给交换磁盘（虚拟内存）的空间量以及你安装的 RAM 量。你可能会用完交换磁盘上的空间，在这种情况下，一些程序将停止工作。正如你所能告诉的，交换听起来不像是你希望在计算机上发生的事情。交换会使你的计算机变得极慢；如果你听到硬盘在狂转（一直发出噪音），就可以判断这种情况正在发生。你计算机上的 RAM 越多，同时可以不进行交换运行的程序就越多。

## 监控内存

有几个程序可以告诉你计算机内存发生了什么。

### 内存有多少：free

这些程序中最简单的是 free。它显示你可用的内存量，既有真实的 RAM 也有虚拟内存，如以下代码所示：

```
[alberto@digital alberto]$ free
              total       used       free     shared    buffers     cached
Mem:         38956     10196     28760      8468        836      5292
-/+ buffers/cache:          4068     34888
Swap:        39276          0     39276
```

### Procinfo

Procinfo 显示与 free 类似的信息，外加更多信息。procinfo 显示的信息由内核在 /proc 目录中收集。以下是我的轻负载 Linux 笔记本电脑显示的屏幕转储：

```
[alberto@digital alberto]$ procinfo
Linux 2.0.33 (root@buildmeister.caldera.com) (gcc 2.7.2.3) #1  [digital]

Memory:     Total      Used      Free    Shared    Buffers    Cached
Mem:        38956     10316     28640      8540        836      5356

Swap:       39276         0     39276
Bootup: Sat Oct 03 09:46:52 1998 Load average: 0.00 0.01 0.00 2/32  544

user  :      0:00:07.88   0.2%  page in : 5623   disk 1: 1563r 633w
nice  :      0:00:00.00   0.0%  page out:    787
system:      0:00:11.74   0.2%  swap in :        1
idle  :      1:23:49.60  99.6%  swap out:       0
uptime:      1:24:09.21          context :    31137

irq  0:     504922 timer                 irq  8:          0
irq  1:         2 keyboard               irq  9:          1
irq  2:         0 cascade [4]            irq 10:          1
irq  3:      1872 smc91c92_cs            irq 11:      1 182365
irq  4:         1                        irq 12:          0
irq  5:         1                        irq 13:          1  math error
irq  6:         2                        irq 14:     12829 ide0+
irq  7:         1                        irq 15:          0
```

除了当前的内存使用情况外，它还会告诉你系统上次启动的时间以及过去 1、5 和 15 分钟的负载平均值（0.00、0.01 和 0.00）。此信息后面跟着可运行进程的数量（列表中的 2/32），以及最后运行的进程（544）。

接下来，procinfo 显示系统在用户代码、系统代码或空闲中花费的时间。Nice 时间是优先级较低运行的用户代码。它还给出机器已运行的总时间。

下一列显示有关虚拟内存和磁盘活动的信息。Page in 和 page out 表示有多少数据已从磁盘移入或移出到内存中。一个页面等于 1K 的数据。Swap in 和 swap out 表示从磁盘交换到内存和从内存交换到磁盘的页面数。Context，如前面的屏幕转储所示，是已发生的上下文切换次数。磁盘列（如果你有多个磁盘，它会显示更多磁盘）将显示自系统启动以来读取次数（1564r）和写入次数（633w）。

## 完全傻瓜 Linux 指南：系统监控：关注你的系统

接下来是连接到 IRQ 的设备（如键盘或串行端口）的活动信息。
`Procinfo` 还应该能够在你提供 `-a` 标志时显示有关模块（内核包，直到需要时才加载）和活动在其他设备上的额外信息。在本书撰写时，随 COL 1.3 发行的 `procinfo` 版本损坏，未显示此信息。

上一页 目录 下一页

要访问内容，请点击章节和节标题。

## 完全傻瓜 Linux 指南

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 监控进程

你的系统持续运行进程。要了解系统上发生了什么，有许多程序可以使用。

### 列出当前前台进程：top

Top 为你提供对计算机正在做什么的实时查看。在你启动它后，它每秒刷新一次，显示计算机上主要进程的信息。

这里是一个示例屏幕：

```
20:33:53 up  2:05,  2 users,  load average: 0.17, 0.07, 0.02
35 processes: 34 sleeping, 1 running, 0 zombie, 0 stopped
CPU states: 4.6% user,  6.3% system, 0.0% nice, 88.6% idle
Mem:  38956K av, 12376K used, 26580K free, 10640K shrd, 1156K buff
Swap: 39276K av,     0K used,  39276K free       5908K cached

PID USER      PRI  NI  SIZE  RSS SHARE STAT LIB %CPU %MEM   TIME COMMAND
655 alberto   20   0   612  612  452 S    0  9.7  1.5   0:10 top
656 root       8   0   592  592  436 R    0  1.7  1.5   0:00 top
1   root       0   0   340  340  268 S    0  0.0  0.8   0:02 init
2   root       0   0     0    0    0 SW   0  0.0  0.0   0:00 kflushd
3   root     -12 -12    0    0    0 SW<  0  0.0  0.0   0:00 kswapd
444 alberto    0   0   696  696  404 S    0  0.0  1.7   0:00 login
363 root       0   0   344  344  272 S    0  0.0  0.8   0:00 getty
177 root       0   0   304  304  240 S    0  0.0  0.7   0:00 rpc.rstatd
19  root       0   0     0    0    0 SW   0  0.0  0.0   0:00 nfsiod
20  root       0   0     0    0    0 SW   0  0.0  0.0   0:00 nfsiod
21  root       0   0     0    0    0 SW   0  0.0  0.0   0:00 nfsiod
22  root       0   0     0    0    0 SW   0  0.0  0.0   0:00 nfsiod
107 root       0   0   328  328  260 S    0  0.0  0.8   0:00 inetd
57  root       0   0   260  260  208 S    0  0.0  0.6   0:00 update
109 bin        0   0   312  312  244 S    0  0.0  0.8   0:00 rpc.portmap
116 root       0   0   356  356  276 S    0  0.0  0.9   0:00 syslogd
```





```
119 root      0  0  476  476  276 S      0  0.0  1.2   0:00 klogd
```

在列表开头，top 会显示有关系统的总体信息。第一行显示当前时间、系统已运行的时间、用户数量以及过去 1、5 和 15 分钟的负载平均值。

第二行显示系统中运行的总进程数以及它们正在做什么：睡眠进程，即当前未执行任何操作的进程；僵尸进程，即本应已死亡但由于某种原因仍存在的进程；以及停止的进程。

第三行显示各种 CPU 状态，例如计算机执行用户代码或系统代码所花费的时间，或 nice 时间。Nice 时间表示以较低优先级执行的进程所花费的时间。这些进程用正优先级表示，因为它们对其他进程友好（典型优先级为 0）。负优先级进程会分配更多 CPU，因此具有更高优先级并获得更多运行机会。

在第四行和第五行，你可以看到有关实际内存和虚拟内存的信息。虚拟内存是使用交换磁盘来容纳比 RAM 所能运行的进程更多的进程的那种内存。

在总体信息区域之后，是所有主要进程的列表，包括进程的 ID（PID）、所有者和优先级以及 CPU 和内存的资源消耗。

当 top 运行时，你可以指定许多选项来自定义其显示的信息。其中一些更有用的选项如表 22.1 所示。

## 表 22.1 Top 选项

| 交互命令 | 描述 |
|---|---|
| Space | 更新显示 |
| Ctrl+L | 重新绘制屏幕 |
| ? | 打印帮助 |
| i | 切换是否显示空闲进程 |
| c | 切换是否显示命令名称/行 |
| l | 切换是否显示负载平均值 |
| m | 切换是否显示内存信息 |
| t | 切换是否显示摘要信息 |
| k | 终止一个任务（使用任意信号） |
| r | “重新 nice”一个任务（更改其当前优先级） |
| P | 按 CPU 使用率排序 |
| M | 按常驻内存使用率排序 |
| T | 按时间/累计时间排序 |
| n | 设置要显示的进程数 |
| s | 设置刷新率 |
| q | 退出 |

要访问内容，请单击章节和节标题。

## Linux 完全 idiot's Guide

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

上一页 目录 下一页

## 进程状态：ps

ps（process status）命令也显示与 top 命令类似的有关进程的信息。ps 命令对于查找进程的 PID 很有用，以便你可以终止或重新 nice 它。 （重新 nice 一个进程会更改其当前优先级。我将在后面的“为进程 nice：nice 和 renice”部分更详细地谈论重新 nice。）要显示系统中运行的所有进程的列表，请输入以下内容：

```
ps aux
```

此命令将列出所有进程（包括其他用户），使用用户格式并包括与终端无关的进程，如下所示：

```
[alberto@digital /]$ ps aux
USER       PID %CPU %MEM   SIZE   RSS TTY STAT START   TIME COMMAND
alberto    371  0.0  1.8  1072   712 p0  S   10:56   0:00 /bin/login -
h 192.168
alberto    372  0.0  1.6  1152   624 p0  S   10:56   0:00 -bash
alberto    566  0.0  1.8  1072   716 p1  S   11:23   0:00 /bin/login -
h 192.168
alberto    567  0.0  1.5  1152   620 p1  S   11:24   0:00 -bash
alberto    630  0.0  1.0   904   392 p1  S   11:41   0:00 man 7 signal
alberto    641  0.0  1.2  1124   480 p1  S   11:41   0:00 sh -c  /bin/
gunzip -c
alberto    643  0.0  1.2  1148   500 p1  S   11:41   0:00 /usr/bin/
less -is
alberto    657  0.0  0.9   856   372 p0  R   11:43   0:00 ps aux
alberto    658  1.0  1084   420 p0  R   11:43   0:00 more
bin        108  0.0  0.8   836   312 ?   S   09:47   0:00 rpc.portmap
daemon     160  0.0  0.8   824   324 ?   S   09:47   0:00 atd
root         1  0.0  0.8   824   340 ?   S   09:46   0:02 init
root         2  0.0  0.0     0     0 ?   SW  09:46   0:00 (kflushd)
root         3  0.0  0.0     0     0 ?   SW< 09:46   0:00 (kswapd)
root        19  0.0  0.0     0     0 ?   SW  09:46   0:00 (nfsiod)
root        20  0.0  0.0     0     0 ?   SW  09:46   0:00 (nfsiod)
root        21  0.0  0.0     0     0 ?   SW  09:46   0:00 (nfsiod)
root        22  0.0  0.0    0    0 ?  SW   09:46   0:00 (nfsiod)
root        57  0.0  0.6  804  260 ?  S    09:47   0:00 update
          (bdflush)
root       106  0.0  0.8  824  328 ?  S    09:47   0:00 inetd
root       188  0.0  1.5 1108  604 ?  S    11:51   0:00 httpd -f
/etc/httpd/a
```

## 终止进程：kill

你可以使用 kill 命令终止进程。kill 命令应作为终止未正确工作的程序的最后手段。kill 命令向程序发送信号（有许多种信号；kill 只是其中之一），这应该会导致它做出适当的反应。否则，它将被杀死：

```
kill pid
```

假设我想杀死我的 Web 服务器（前面列出的 httpd 进程），我将发出此命令：

```
[root@digital /]# kill 188
```

如果你不是该进程的所有者（请参阅 ps 输出的第一列中的所有者），你需要是 root 才能杀死它。

有时， rogue 程序不会对默认的 kill 信号做出适当响应。在这种情况下，有时有必要使用更强的 kill，即 KILL（无条件 kill）信号，也称为 Linux 中的“信号 9”。信号 9 是一种非常强的药剂，只有在 rogue 程序拒绝以其他任何方式死亡时才应使用。要在 Linux 中使用 KILL 信号杀死程序，请使用以下任一方法：

```
kill -KILL pid
kill -9 pid
```

用你要终止的进程的编号替换 pid。没有进程可以忽略或逃脱 KILL 信号。

一些作为守护进程运行的进程，例如 httpd，可以通过发送 -HUP（挂断）信号来重新启动。重新启动将使进程重新读取其配置文件并重新启动，如下所示：

```
[root@digital /]# kill -HUP 188
```

## “为进程 nice”：nice 和 renice

有时你会有大作业要运行——比如你需要处理几百兆的日志文件以获取有关 Web 服务器的一些统计信息。也许你想要信息尽快获得，但让计算机全力以赴地获取它会不利地影响系统中其他所有内容的性能。也有可能是你需要该作业尽可能快地运行，将其他所有内容置于第二优先级。

要以较低优先级启动此类进程，只需在命令名称前输入 nice。这将以 nice 状态启动命令：

```
nice dobigjob
```

使用 nice，可以设置进程执行的优先级。优先级范围从 19（最 nice 的程序）到 -20（最高优先级）。只有 root 才能为进程分配较高的（负）优先级。

Nice 设置为将任何默认优先级为零的进程的当前优先级增加 10。

你也可以通过提供 -n 标志和优先级设置后跟 PID 来指定优先级：

```
nice -n 12 dobigjob
```

Nice 仅对尚未启动的作业有效。要使现有进程 nice，你使用 renice。如果你想让 Web 服务器优先于所有其他进程，root 可以这样调整它：

```
[root@digital httpd]# renice -10 188
188: old priority 0, new priority -10
```

## 监控你的磁盘

Linux 不喜欢磁盘空间用完。监控磁盘空间很容易。你可以使用两个程序：du 和 df。

上一页 | 目录 | 下一页

要访问内容，请单击章节和节标题。

## Linux 完全 idiot's Guide

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 找出磁盘文件占用多少空间：du

磁盘使用程序 du 允许你获取目录占用多少空间的列表，以 1K 为增量。默认情况下，它会为找到的每个目录打印一个条目，如下所示：

```
[alberto@digital alberto]$ du
14      ./seyon
3       ./lg/lg_layouts
1       ./lg/lgDESKTOP
1       ./lg/lg3_hosts
15      ./lg
40      ./kde/share/config
1       ./kde/share/apps/kfm/tmp
1       ./kde/share/apps/kfm/bookmarks
6       ./kde/share/apps/kfm
4       ./kde/share/apps/kdehelp
2       ./kde/share/apps/knotes/notes
1       ./kde/share/apps/knotes/xyalarms
5       ./kde/share/apps/knotes
1       ./kde/share/apps/kppp/Rules
```

要汇总输出，请指定 -s 选项，如下所示：

```
[alberto@digital alberto]$ du -s
23670   .
```

要指定要列出的特定目录或文件，请将其名称作为参数提供，如下所示：

```
[root@digital /home]# du -s *
23670   alberto
32      cool
32      digital
35      flower
583     ftp
1582    httpd
1       public
```




1       samba
1       test_project

In this example, all home directories are summarized.

## Finding the Amount of Free Disk Space: df

To find the amount of disk space to devices available in your system, use the df (disk free) command, as shown in the following:

```
[root@digital /home]# df
Filesystem           1024-blocks   Used Available Capacity Mounted on
/dev/hda1             686892  606189    45223      93% /
```

The command produces a nice table specifying how much space is available. Numbers are expressed in kilobytes.

In UNIX/Linux, just because there’s free space doesn’t mean that you can create files. If the file system’s inode table fills up (unlikely, but possible if a disk holds a great deal of tiny files), your system would be unable to create additional files. To see how you are doing on inodes, provide the -i option to df:

```
[root@digital /home]# df -i
Filesystem     Inodes   IUsed   IFree %IUsed Mounted on
/dev/hda1       177480   34971  142509    20% /
```

If you compare the regular df output, you’ll see that under normal circumstances, there are plenty of inodes left. On my disk, I have used 93% of my disk, yet only 20% of the inodes.

## Log Files

Many of the programs that run in the background, Web server, email, FTP, and so on generate logs for errors or just as a record of someone accessing it. This type of information is recorded, for example, every time a user logs in or out of the system.

## Monitoring Logins: last

Linux keeps very good track of users and their logins. This information is particularly useful when you are in a networked environment, and as a security precaution, you check to make sure that no “weird” traffic is going on in your machine.

By default, Linux is set up to keep track of logins and logouts. You can browse the login record using the last command.

To filter output to a specific user, provide the username as an argument to last:

```
[alberto@digital log]$ last alberto
alberto  tty p0     192.168.0.3   Fri Oct  2 18:32   still logged in
alberto  tty p0     192.168.0.3   Fri Oct  2 18:29 - 18:32
alberto  tty2       192.168.0.3   Fri Oct  2 15:20 - 17:01   (01:40)
alberto  tty p1     192.168.0.3   Fri Oct  2 14:55 - down     (03:32)
alberto  ftp       192.168.0.3   Fri Oct  2 13:41 - 13:42   (00:00)
alberto  ftp       192.168.0.3   Fri Oct  2 13:12 - 13:28   (00:16)
alberto  tty1       Fri Oct  2 13:02 - down     (05:25)
alberto  tty1       Wed Sep 30 17:41 - down     (00:18)
alberto  tty1       Tue Sep 29 11:10 - down     (00:10)
alberto  tty1       Mon Sep 28 17:36 - down     (00:47)
```

The last command prints the username, the terminal used to access the system, where the user came from (IP address) if the login was remote, and the date and duration of the session.

If the log file /var/log/wtmp doesn’t exist in your system, the system will not keep track of login information. To enable (or disable) this feature, just create or delete this file.

## Monitoring Bad Logins: lastb

The lastb command keeps track of bad (unsuccessful) logins. To enable bad login accounting, as root create the file /var/log/btmp. You can do this using the touch command (touch /var/log/btmp).

To review bad logins, use the lastb command. Unfortunately, Caldera OpenLinux doesn’t currently support lastb use.

If an account has an unusual number of bad logins, it is possible that the account is under attack by someone. Such accounts should be disabled and the user owning the account should be notified.

## Disabling an Account

The easiest way to disable an account is to put an asterisk (*) before the encrypted password in the /etc/passwd file. (The password is the second field in /etc/passwd.) Fields are separated by colons (:), like this:

```
me:*Ms.7kvaAYyHbU:500:100:Me:/home/me:/bin/sh
```

If you are using shadow passwords, the easiest way to disable an account is to use usermod and expire it with a date in the past:

```
usermod -e MM/DD/YY login
[root@digital alberto]# usermod -e 09/01/98 me
```

(Usermod is introduced in Chapter 18. "Users, Groups, and Passwords.")

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Chapter 23
Sharing Files over the Network

## In This Chapter

- The Network File System
- Using the mount and umount Commands
- Navigating the File System with FTP
- Uploading and Downloading Files
- Controlling File Access

Sharing files over the network allows you to collaborate more easily with others. Linux has the capability to provide file-sharing services in many ways. You can also be a client to almost all popular network file-sharing schemes.

The most popular ways for sharing files under UNIX are FTP (File Transfer Protocol), NFS (Network File System), and HTTP (the Web). Other protocols, such as Gopher, have given way to Web counterparts. Windows-based PCs share files using the SMB (Server Message Block) protocol. Linux can easily be a client to an SMB server and provides you with an FTP-like interface to a server.

If the information here should awaken your interest, feel free to read the online documentation (see Chapter 15, “Help Please”). Accessing a service (being a client) is easy. Setting up a server is slightly (a few orders of magnitude) more complicated, and entire books have been written on the various subjects. Given

the limited space, I have covered what I consider the least you should need to know to publish data and to access data from other servers.

## NFS

The NFS is how you share files between UNIX-based machines. Originally developed by Sun, NFS is very flexible and could be used to share information between networks. However, exporting directories to networks outside your control requires careful security considerations. By design, NFS was not intended for sharing across the Internet, but given today’s high-speed communication networks, it is feasible to share files over the Net.

NFS allows a directory tree to be grafted into the file system by other computers on the network in much the same way you mount a floppy disk or CD-ROM.

One issue with NFS is that file system security is based on the same mechanism your local file system uses: User IDs (UIDs) and Group IDs (GIDs) of files. If the UID of a user accessing a remote NFS volume doesn’t match the user’s own, the user will lack the necessary privileges. This means that in order to use NFS effectively, there needs to be a mechanism that shares login and password information. Luckily, such a system does exist; it is called NIS (Network Information Services). A long time ago, NIS was called Yellow-Pages. Configuring NIS and NFS requires more depth of information than a few paragraphs can offer. This section will only show you how to export and import an NFS volume. For in-depth configuring information, you should consult the online documentation and how-to guides and perhaps even acquire a book on NIS and NFS. Linux implementation is fairly standard, and you should have no problem adapting that information to your system.

## Exporting an NFS Volume

Before you can export NFS volumes, you’ll need to enable the NFS Server services in your computer. This is done through LISA under Configure daemon/server autostart under the System Configuration area; then you’ll need to reboot your computer. LISA, as you learned in Chapter 21, “LISA: Linux Installation and System Administration Utility,” is a command line program that manages your hardware and software configuration for the more important portions of your system.

With NFS, you don’t need to export an entire disk volume; a directory of your choosing will suffice. To export a directory, you merely need to edit the file /etc/exports. When you export a directory, you choose how you make it available and the permissions that others may have on the volume. Typically, unless you know what you are doing, you should just export the volume read-only. This way, users can see and access files, but they won’t be able to modify or delete files.

```
/share   (ro,insecure,all_squash)
```

In the entry shown, /share is exported with several options; here’s what they

mean. `ro` 选项请求将文件系统导出为只读：用户可以查看和访问文件，但不能修改它们。`Insecure` 允许不使用保留端口的 NFS 客户端访问此卷。通常，NFS 希望只允许在特定端口上连接的服务客户端。`all_squash` 选项将 `/share` 中找到的所有 UID 和 GID 映射到匿名用户的那些。 此设置会将 `/share` 目录导出到全世界！

有关其他选项的更多信息，请阅读 `exports` 的手册页。

Previous Table of Contents Next

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

To access the contents, click the chapter and section titles.

Search this book:

## Mounting an NFS Volume

挂载 NFS 卷与挂载 CD-ROM 或软盘驱动器非常相似。通常，mount 命令是特权的，只有超级用户或 root 才能指定它。用户唯一能挂载文件系统的方式是如果 /etc/fstab 文件中的挂载描述包含 user 选项。

### The mount Command

mount 命令将设备或网络中的文件系统 graft 到本地系统的目录中。如果该目录有文件，则在挂载移除之前这些文件会被隐藏。文件 /etc/fstab 包含计算机中所有挂载的列表。如果 fstab 文件的一行包含 user 选项，则非 root 用户可以使用 mount 命令挂载它。只需指定设备或挂载的名称或其挂载点即可访问文件系统。考虑以下内容：

```
[root@digital nfs]# more /etc/fstab
/dev/hda1 / ext2 defaults 0 1
/proc /proc proc defaults 0 0
/dev/hda5 none swap defaults 0 0
/dev/fd0 /mnt/floppy auto user,defaults,noauto 0 0
digital://share /net/digital nfs ro
/
```

我的 /etc/fstab 文件包含我的根分区 (/dev/hda1) 的挂载条目，以及其他东西，例如我的软盘 (/dev/fd0)。软盘可由任何用户挂载（参见 user 选项），并且它们挂载在 /mnt/floppy 目录中。网络挂载以机器名称开头，后跟冒号 (:) 和它们导出的路径，后跟挂载点、其类型 (nfs) 和 ro 选项（只读）。

要挂载我的软盘，我只需要输入以下内容：

```
mount /mnt/floppy or mount /dev/fd0
```

要挂载 NFS 卷，也差不多：

```
mount host:/path dir
mount -ro digital://share /net/digital
```

如果您只计划临时挂载 NFS 卷，则无需将其添加到 /etc/fstab 文件中。

但是，经常挂载的卷应为方便和正确性而添加。

### The umount Command

要从文件系统移除挂载，您使用 umount 命令。作为参数提供挂载位置：

```
umount mountpath
umount /net/digital
```

## FTP

在第 9 章“通信：Web、FTP、电子邮件和新闻”中，您学习了如何使用 KDE 和 Netscape 从 FTP 站点下载文件。正如您所想象的，有一个命令行等价物可用于下载文件，称为 ftp。

FTP 既是一项服务，也是终端用户工具。首先，我们将看看如何使用 ftp 命令，然后，我们将讨论如何启用用户使用 ftp 进入您的机器。

### Connecting to an FTP Site

ftp 命令易于使用。只需指定您要连接的主机名称，如下所示：

```
ftp hostname
[root@digital /etc]# ftp localhost
Connected to localhost.
220 digital.bordersoft.com FTP server (Version wu-2.4.2-academ[BETA-15] (1) Wed J
an 7 01:03:55 MST 1998) ready.
Name (localhost:alberto): alberto
331 Password required for alberto.
Password:********
230 User alberto logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful.
150 Opening ASCII mode data connection for /bin/ls.
total 7931
-rw-r--r-- 1 alberto alberto 7165 Sep 16 20:48 #registrar.cgi#
-rw------ 1 alberto alberto 14 Sep 1 13:22 .rm.sh#
drwxr-xr-x 24 alberto alberto 2048 Sep 26 15:01 .
drwxr-xr-x 10 root root 1024 Sep 25 21:39 ..
-rw-rw-r-- 1 alberto alberto 998 Sep 26 15:42 .bash_history
```

连接后，您需要登录。如果您在要连接的系统上拥有帐户，您可以使用您的登录名和密码，您将被带到您的主目录。如果您没有帐户，您可以尝试以用户 "ftp"（有时是 "anonymous"）登录，密码与您的电子邮件地址匹配。这称为匿名 FTP。匿名 FTP 仅限于系统的特定区域。

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Hosting an FTP Service

虽然大多数时候您将是 FTP 站点的客户端，但您可能希望通过 FTP 使一些文件可用。要从其他机器启用 FTP 访问，您必须在 /etc/inetd.conf 中启用 FTP 服务。有关如何启用这些服务的详细信息，请参阅“网络服务”注释。）在 /etc/inetd.conf 中启用服务后，您可以使用 FTP 访问您的机器并使用您的登录名和密码。

要启用 FTP 服务，您需要确保已安装 wu-ftpd 包。如果您进行了标准安装，它已安装。

Linux 默认安装的 FTP 服务称为 wu-ftpd。Wu-ftpd 最初在华盛顿大学圣路易斯分校开发。这种强大的 FTP 服务器软件被支持数千用户的站点使用。

提供匿名 FTP 默认情况下已启用，因为您的 /etc/passwd 包含 FTP 用户的条目。以 FTP 登录到系统的用户将被放入 /home/ftp 目录。该目录由 FTP 守护进程（运行 FTP 服务的软件）以不同的方式处理。就匿名用户而言，/home/ftp 看起来像一个根文件系统。用户无法更改到它之外的目录，并且只能访问其中的目录。FTP 守护进程通过将 FTP 进程的服务器根更改为 /home/ftp 目录来实现这一点。该目录包含最小的 /etc 和 /bin 目录，其中包含足够的信息和软件以允许匿名用户访问系统。您不应修改 /home/ftp/etc 和 /home/ftp/bin 目录的内容，除非您知道自己在做什么。

要发布文件，以 root 身份在 /home/ftp/pub 内创建一个目录，并确保目录权限为 755。匿名用户将能够从那里下载文件，但不能写入（put）文件。

### Techno Talk: Network Services: /etc/inetd and tcpd

网络服务由一个名为 inetd 的程序处理。Inetd 侦听网络连接，并在收到连接时确保正确的服务器与客户端连接。

由于安全问题，您可能希望仅向特定客户端提供某些服务。例如，您可能不希望每个人都能尝试通过 FTP 连接到您的系统。为满足此类需求，有一个名为 tcpd 的程序处理 FTP 和 Telnet 等程序的请求。当收到连接请求时，系统会尝试根据用户来自何处确定是否应允许连接。Tcpd 会咨询文件 /etc/hosts.allow 和 /etc/hosts.deny，以查看客户端（尝试连接的系统）是否属于这些类别。默认情况下，未明确允许的任何客户端将被明确拒绝访问。

要为其他主机启用访问，您需要编辑 /etc/hosts.allow 文件。这些文件的配置信息可在在线手册中找到。（执行 man 5 hosts_access 以阅读有关配置格式的信息。）

例如，要为所有域的所有服务启用访问，您将在 /etc/hosts.allow 文件中输入以下内容：

```
ALL: ALL
```

阅读 tcpd、inetd 和 hosts_access 的手册页以获取更多信息。

创建传入目录（匿名用户可以放置文件的目录）有点棘手。如果您的计算机在互联网上并且您在没有采取充分预防措施的情况下放置了此类目录，那么在您意识到之前，您的计算机就会成为盗版软件和可疑文档和图像的分发节点。要创建不易受此类型问题影响的传入目录，请输入以下内容：

```
[root@digital /root]# cd /home/ftp/pub
[root@digital pub]# mkdir incoming
[root@digital pub]# chmod 1733 incoming
```

这将创建一个目录，允许匿名用户放置文件，但他们无法列出他们上传的文件。知道传入目录中文件名称的用户仍然能够下载它，但他们无法列出目录的内容。

您可以对匿名用户施加许多选项和限制来控制对站点的访问，包括控制并发用户数量和他们来自何处。Ftpd 还有许多选项可以记录所有进出内容。要利用这些功能，请阅读 ftpd 的手册文档。（执行 rpm -qd wu-ftpd 以查看所有文档的列表及其安装位置。）





Products | Contact Us | About Us | Privacy | Ad Info | Home

Use of this site is subject to certain Terms & Conditions. Copyright © 1996-2000 EarthWeb Inc.
All rights reserved. Reproduction whole or in part in any form or medium without express written permission of EarthWeb is prohibited.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

To access the contents, click the chapter and section titles.

Search this book:

## HTTP

HTTP stands for Hypertext Transfer Protocol. This is the protocol that drives the Web. When you load a file into your Web browser, you are using HTTP. HTTP provides a very secure way of publishing information for others to see. If you want to share information, your Linux system is more than capable of serving to thousands of users.

There are many popular Web servers that run on a variety of systems. By far, the most popular is Apache. Apache is a freely available Web server software distributed under the GNU Public License. Apache powers about 50% of all Web servers on the Internet. If that figure doesn’t seem high to you, consider that the second most popular server is Microsoft’s Internet Information Server, which only absorbs 22% of the market. Netscape servers follow at 8%, and the rest of the server software is under 2% and powers less than 1% of the sites. These statistics are based on more than 3 million Web sites (see www.netcraft.com). Apache is very good indeed. Your system already has it running, even if you didn’t know it.

## Configuring an Apache Server

Apache’s default configuration, as installed, is fairly adequate and secure. If you need to tinker and you are maintaining a public Web server, you should really take a look at a book on Apache. A good one is my book The Apache Server Survival Guide, ISBN: 1-57521-175-0. It covers all the topics that you need to know about setting up and maintaining an Internet server. It doesn’t assume much but provides in-depth information and many examples. It also orients you on HTML and CGI programming.

Apache’s configuration files can be found at /etc/httpd/apache/conf. Configuration of an Apache server is done in three text files: httpd.conf, access.conf, and srm.conf. Configuration for Apache is straightforward. Directives appear one per line. The first word on the line is the directive; the rest are the parameters or configuration settings. Fire up your editor and open /etc/httpd/apache/conf/httpd.conf to see what I am talking about. You’ll see the following:

- The httpd.conf file is the primary Web server configuration file. This file sets the default behavior of the server, such as its name, the port it runs under, the location of configuration, logs, and error files. Without getting into the depths of it, here is the only directive that you need to change in this file:
  - ServerName—This should reflect a valid DNS name for your system. If you don’t know the fully qualified DNS name for your system, leave this as localhost.
- The srm.conf configuration file keeps track of where information published by the Web server resides. It also provides a mapping between icons and files that the Web server uses when generating automatic file indexes. There are two directives that are important for you to know about:
  - DocumentRoot—This directive specifies where your HTML documents are found. By default on Linux, this points to /home/httpd/html. This directory contains HTML help Linux documentation pages (if you are running Caldera’s distribution) or the Apache Server documentation.
  - UserDir—This directive specifies the name of a directory users can create in their accounts. Files in this directory are accessible using a browser and a URL such as http://servername/~username/ (note the tilde (~) before the username).
  - DirectoryIndex—This directive specifies the name of files that will be loaded when a user requests a directory instead of an HTML file. If you take a look at the URL in the preceding item (http://servername/~username/), this URL doesn’t request a file, it requests a directory. (This is similar to when you request http://www.caldera.com; this is just the name of a machine!). This directive specifies a filename to search when incomplete URLs are specified; if the file is found, it is sent to the browser. Otherwise, the server will generate an automatic server index, listing all files contained in the directory. You can define multiple DirectoryIndex files like this:

```
DirectoryIndex index.html index.htm dir.html dir.txt
```

Maintaining a Web server or any other sort of public Internet service is serious business. In the coziness of an intranet, you only have to worry about security from your peers. On the Internet, you need to worry about the entire world. There are some evil people out there that could do serious damage to your system.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

To access the contents, click the chapter and section titles.

Search this book:

## Controlling Access

Another skill that you’ll need when publishing Web pages is to protect materials from general users, unless they are able to provide an acceptable login and password. This is very simple to do, and it requires that you do a couple of things.

To protect a number of documents, create a directory. You can call it anything you want. Inside this directory, create a file called .htaccess (note that the name of the file begins with a period [ . ]).

Inside this file, put the following text:

```
AuthUserFile /home/yourusername/.htpasswd
AuthName Alberto's Secured Area
AuthType Basic
require valid-user
```

AuthUserFile specifies the location for a password file that will be used to validate users. Note that this file lives outside the public_html directory or the DocumentRoot tree. Replace yourusername with your login name.

AuthName is a name that identifies this set of documents. It’s typically displayed by the browser on the password request dialog.

AuthType defines the type of authentication used. We’ll use Basic.

Require specifies that the only authenticated users should be let in (valid-user option).

After you put this file in the secured directory, all files and directories under this are protected.

## Creating an htpasswd File

Web server passwords are managed by a tool called htpasswd. This tool exists in /home/httpd/bin/htpasswd. The arguments are simple:

```
htpasswd [-c] filename username
```

The -c option creates the password file using the filename specified (in my case, I defined mine in /home/yourusername/.htpasswd), followed by the name of the user to add to the file:

```
[alberto@digital stuff]$ /home/httpd/bin/htpasswd -c /home/alberto/.htpasswd alberto
Adding password for alberto.
New password:**********
Re-type new password: **********
```

That's all. Anyone trying to access the directory will be asked to authenticate. If the authentication succeeds, they have access to the page(s).

## SMB: Sharing Disks and Printers to PCs

If your computer is on a heterogeneous network, more than likely there are Windows-based PCs sharing the network with you. Linux, again, can provide file sharing to other OSs, such as those running Windows. Windows PCs see the file shares as another PC sharing a network drive. As a client, Linux can connect to a Windows PC, allowing you to transfer files to your Linux box.

SAMBA is the common name for the service that allows you to do this. SAMBA is an acronym for the SMB protocol (Server Message Block), which allows Windows-based PC access to disks and printers from Linux and from Linux to Windows-based PC printers and disks.

This service is complex and well-developed; however, it has many gotchas—especially if you are trying to connect to Windows NT 4.0 SP3 or Windows 98 computers.

To use SAMBA, you first need to download the latest version from http://samba.gorski.net/samba/samba.html. The versions shipped by most manufacturers are out of date. There are RPM packages you can install available right at the site.

## Accessing a PC Network Drive from Linux: smbclient

You use smbclient to access a PC network drive. The command has many options, and some systems—such as Windows NT and Windows 95—are picky about wanting to talk with Linux. For this reason I will refer you to the SAMBA documentation in the /usr/doc/samba-1.9.18p8-Caldera.1 directory for more information on installation and configuration.

## Listing Services

To see a list of the services provided by a PC host, provide the -L option to the smbclient command. By default, Linux will attach your UNIX login name. If your login is different on the PC, specify it with the -U option, like this:

```
smbclient -L smbhostname -U pcloginname
```

It is possible that some hosts will give you grief if you supply a login name that is not in all caps. Here's a transcript of such a session with an NT4.0 Workstation. Note that the NT host required me to provide a password:

```
[alberto@digital alberto]$ smbclient -L pri -U ARICART
Added interface ip=192.168.0.2 bcast=192.168.0.255 nmask=255.255.255.0
Got a positive name query response from 192.168.0.1 ( 192.168.0.1 )
Server time is Sat Sep 26 18:39:17 1998
Timezone is UTC-5.0
Password: ******
Domain=[WORKGROUP] OS=[Windows NT 4.0] Server=[NT LAN Manager 4.0]
security=user
Server=[PRI] User=[] Workgroup=[WORKGROUP] Domain=[]
```

| Sharename | Type | Comment |
|------------|------|---------|
| ADMIN$     | Disk | Remote Admin |
| C$         | Disk | Default share |
| CD         | Disk |  |





This machine has a browse list:

| Server | Comment |
| --- | --- |
| DIGITAL | Samba 1.9.18p8 |
| PRI |  |

This machine has a workgroup list:

| Workgroup | Master |
| --- | --- |
| WORKGROUP | PRI |

From the listing, I know that this machine has several resources I can use, including a printer and access to a disk.

|  |  |
| --- | --- |
| HD | Disk |
| HPLaserJ | Printer HP LaserJet 4/4M Plus PS 600 |
| IPC$ | IPC Remote IPC |
| print$ | Disk Printer Drivers |
| shared | Disk |

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Chapter 24
Customizing Your Linux Kernel

## In This Chapter

+ - Customizing your kernel with LISA
+ - Customizing your kernel by recompiling
+ - Building a new kernel
+ - Configuring, compiling, and installing new kernels and modules

### Customizing Your Linux Kernel with LISA

The easiest way to customize your kernel is to add and remove driver modules using LISA. The standard installation of Caldera OpenLinux contains a large number of drivers for various types of hardware. These drivers can be inserted and removed from your system automatically by LISA without the need for further work on your part. Although some users—such as those requiring advanced power management—will need to recompile their kernel to make use of their hardware, others will be served just as well by the kernel-management facilities offered by LISA.

For more information on using LISA to configure your system, see Chapter 21, "LISA: Linux Installation and System Administration Utility."

> Note:
> This chapter is not for the faint of heart. It gets into the nitty gritty about working with kernels...something Linux beginners need to take great caution with. It might even be something you should wait to tackle until after you've had more hands-on experience with Linux.

### Customizing Your Linux Kernel by Recompiling

Kernel configuration sounds like a scary topic, but it really isn't. The one caveat is that if you are not careful, you can make your system unbootable. But then again, understanding Linux and avoiding problems are the reasons why you bought this book.

As you already know, the Linux kernel installed on your system by default seems to provide support for most of the hardware installed by most machines. This is very cool because it enabled you to do a great number of

things before you even knew that kernel building was something you wanted to do. If you are happy with what you’ve got, read no further, you don’t need to customize your kernel. Even Caldera will tell you this.

Customizing your kernel can improve the performance of your system, but given today’s speedy boxes it is not likely that you’ll be able to tell a great difference between a custom kernel and a generic one. There are several reasons why you’d want to build your own kernel:

+ - You have a laptop and need power management support.
+ - You want to enable file system quotas.
+ - You need Symmetric Multi-Processing support.
+ - Amateur Radio Network drivers.
+ - You want a kernel that is customized for your processor.
+ - You have some other special hardware or needs.

Kernel building is especially important if you have special hardware, such as a laptop. Building a new kernel for a laptop enables you to include support for the power management features provided by Linux.

If you want to see how fast Linux can go, customizing the kernel gives you a glimpse of this. A custom kernel requires less memory, speeds up the bootup process, and increases performance. The kernel will be built to take advantage of your processor (instead of an i386 processor); that alone will help zip a few things along.

In order for you to be able to build your kernel, you need to have a compiler installed. Warning: this process takes a while, and the actual compilation itself can take an hour, depending on the hardware you have and how much you need to support.

### Getting Started

There are several steps that you need to accomplish in order to build and install a new kernel:

+ 1. Selecting drivers and feature support
+ 2. Compiling the kernel and any necessary modules
+ 3. Copying the kernel to its proper place
+ 4. Installing the new modules
+ 5. Configuring and reinstalling LILO to see the new kernel
+ 6. Configuring the new modules and rebooting

```
In addition to the gcc compiler, you need the following packages.
(Note that the version of your package might be better than the one
I list.) The linux-source-doc package is not necessary to build the
kernel but is good to have around. If you do a standard install, this
package is already on your disk; otherwise it is included on your
CD.linux-kernel-include-2.0.35-1.i386.rpm
linux-source-common-2.0.35-1.i386.rpm
linux-source-1386-2.0.35-1.i386.rpm
linux-source-doc-2.0.35-1.i386.rpm
```

If you do a standard install, your kernel sources will be located in the /usr/src/linux directory. This directory is just a link to the current kernel sources Linux-2.0.35 or whatever you have.

As usual, it is a good idea to read the documentation included with the kernel. A nice README file contains information on how to build the kernel. Some steps might be missing or not as well elaborated, but between this book and that document you will have enough support to build your own kernel.

### Kernel Building Approaches

As you configure your kernel, you’ll be offered the option to include support of a feature in two different ways:

+ - Building the support into the kernel itself
+ - Building the support as an external module

Use built-in support instead of module support when the supported device is required in order to boot your computer. If you have a specific networking or SCSI card, and you make use of that card as the computer is starting, compile support into the kernel. This makes the kernel bigger, so limit it to things you know will be loaded no matter what.

Features that you might use on and off (such as PPP support) might be better as a module. When not in use for extended periods of time the module can be removed from memory using LISA, thus releasing your valuable resources.

Caldera uses the module approach for its generic kernel. If your hardware requires the service, the module is loaded. If not, it just occupies a little of your disk.

Previous Table of Contents Next

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

To access the contents, click the chapter and section titles.

Search this book:

### Configuring the New Kernel

Kernel compiling is done with special tools included in the Linux kernel source. You have three tools to choose from:

+ - config
+ - menuconfig
+ - xconfig

Config is an interactive script that asks you questions for each of the options about which it needs information to configure properly. I find an interactive program is better for this sort of exercise. Use menuconfig if you are using a shell or xconfig if you are working under X (or KDE as it is also called).

To start the configuration tool, first change to the /usr/src/linux directory and enter:

```
make toolname
```

![](img/edf072a03d4de1f8f4a13465ac79e7fb_289_0.png)

Xconfig provides buttons to configure the various options.

Where toolname is the name of the tool you want to use. Here's the screen you'll see if you use xconfig.

In this window, take a look at the options included. Xconfig gives you buttons for the following configuration settings:

+ - Code maturity level options
+ - Loadable module support
+ - General setup
+ - Floppy, IDE, and other block devices
+ - Networking options
+ - SCSI support
+ - SCSI low-level drivers
+ - Network device support
+ - ISDN subsystem
+ - CD-ROM drivers (not for SCSI or IDE/ATAPI drives)
+ - Filesystems
+ - Character devices
+ - Sound
+ - Kernel hacking
+ - STREAMS subsystem

If you know for a fact that your system doesn’t contain specific hardware, disable it in the configuration. If you aren’t positive, it’s best to leave the default setting. Limit your initial experimentation with kernel building to the general setup, networking options, sound, SCSI support and SCSI low-level drivers. Provided that you know the hardware you have, you will be able to eliminate a lot from these options and leave only those items that apply to your specific hardware. If you are unsure about an item, leave it be. (It’s not a bad idea to check out the online help system if you come across something you need to know more about…it’s what it’s there for!)

After you have configured all your drivers, click the Save, then the Exit button. This saves a new configuration file.

### Check This Out: Say what? You want sound?

With Linux, you either have sound or you don’t. I know, it seems like a joke, but it’s the truth. Sound cards for all Linux users are either easy or hard to configure (not much gray area to that).

If you happen to be among those who have an easy sound card, then the process of recompiling the kernel discussed in this chapter will get you on the road to cranking out sound. During the recompilation configuration process, you’ll see a series of sound questions such as the following:

```
Sound card support (CONFIG_SOUND) [Y/n/m/?]
/dev/dsp and /dev/audio support (CONFIG_AUDIO) [Y/n/?]
MIDI interface support (CONFIG_MIDI) [Y/n/?]
FM synthesizer (YM3812/OPL-3) support (CONFIG_YM3812) [Y/n/?]
ProAudioSpectrum 16 support (CONFIG_PAS) [N/y/?]
Sound Blaster (SB, SBPro, SB16, clones) support (CONFIG_SB)
[Y/n/?]
Generic OPL2/OPL3 FM synthesizer support (CONFIG_ADLIB) [Y/n/?]
Gravis Ultrasound support (CONFIG_GUS) [N/y/?]
```

For basic sound support, always answer yes to the CONFIG_SOUND, CONFIG_AUDIO, and CONFIG_ADLIB options. You’ll also need to choose at least one sound card to support. If you know the model and make of your sound card, then you’re in good shape and can answer Y to the right one. After you choose your card, you’ll need to answer a couple of questions about it (IRQ, base address, and so on). With an easy sound card, the setup isn’t much different than setting up SCSI controllers, multiport serial boards, or parallel devices.

If you’re one of the unfortunate souls who has a hard sound card, like the Creative AWE Plug’N’Play cards, you’re better off without sound for a while. The concepts you’ll need to know to get this type of sound card going are something for the more seasoned Linux user rather than the beginner, so hang in there!

### Compiling the Kernel and Necessary Modules

Compiling builds binary files that your computer is able to execute. To build your new kernel, enter the following commands in a root shell. Note that these commands generate a lot of output that I have omitted:

```
[root@digital linux]# make dep
```




## 《Linux 完全傻瓜指南》：自定义 Linux 内核

```
[root@digital linux]# make clean
[root@digital linux]# make zImage
[root@digital linux]# make modules
```

前面的命令（尤其是 make zImage）会花费一段时间。所需时间从几分钟（在 Pentium 计算机上）到数天（在 386 计算机上）不等，具体取决于你的选择和硬件速度。如果它们全部在没有任何错误的情况下完成，你就可以准备安装新的内核了。

## 安装新内核

新编译的内核位于 /usr/src/linux/arch/i386/boot/zImage。在安装它之前，你需要确保不会覆盖现有的内核。这些内核存储为 /vmlinuz 以及 /boot/vmlinuz-2.0.35-modular（版本取决于你的安装）。你不需要移动它们，只需确保不要覆盖它们。如果这样做并且新内核无法正常工作，你的系统可能会无法启动。

将新内核复制到 /boot 目录，并使用新名称：

```
# cp /usr/src/linux/arch/i386/boot/zImage /boot/vmlinuz-2.0.35-apm
```

我为新内核命名了其版本并添加了 apm（高级电源管理）部分，以便将其与现有内核区分开来。任何附加名称都可以，只要不覆盖现有内核即可。

## 《Linux 完全傻瓜指南》

Publisher: Macmillan Computer Publishing
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

## 安装新模块

模块的安装稍微棘手一些，因为默认情况下，模块安装会想要覆盖现有模块。模块安装在 /lib/modules 目录中，位于一个以内核版本命名的目录下。（内核版本可通过 uname -r 命令获得。）对于我的设置，这意味着路径为 /lib/modules/2.0.35。

为保存当前模块，将它们移开：

```
[root@digital linux]# mv /lib/modules/2.0.35 /lib/modules/2.0.35-old
```

使用以下命令安装新模块

```
[root@digital linux]# make modules_install
```

在新模块安装后，将事物恢复原状，以便旧内核仍能找到它们。你可以通过以下操作实现

```
[root@digital linux]# mv /lib/modules/2.0.35 /lib/modules/2.0.35-apm
[root@digital linux]# mv /lib/modules/2.0.35-old /lib/modules/2.0.35
```

如果正在安装的新内核是不同版本，则此步骤是不必要的，因为新模块将具有不同的版本和目录。

## 配置 LILO

安装内核的最后一步是设置 LILO。LILO（Linux Loader）是用于从磁盘启动 Linux 的程序。LILO 配置文件看起来会像这样：

```
[root@digital /]# more /etc/lilo.conf
#
# general section
#

boot = /dev/sdb1
install = /boot/boot.b
```

```
# default entry
#
image = /vmlinuz
    initrd = "/boot/initrd.gz"
    label = OpenLinux
    root = /dev/sdb1
    read-only
    append = "load_ramdisk=1 ramdisk_size=2880"
#
# additional entries
#
```

根据系统的配置，你可能看不到与示例完全相同的行。但从示例中可以看出，至少已定义了一个 Linux 条目。默认条目是在超时时间过去后启动的条目。你可以将新内核安装为默认项，只要保存之前的条目，以防新内核的行为与你预期不同即可。

在旧内核条目之上插入新内核的条目。以旧条目作为部分指南。你需要为 image（内核文件）、label（启动时显示的名称）和 root（与旧内核条目相同）指定值。在末尾添加 "read-only" 行，以指定每次启动此内核时都要检查文件系统。 resulting /etc/lilo.conf 将类似于

```
[root@digital /]# more /etc/lilo.conf
#
# general section
#
boot = /dev/sdb1
install = /boot/boot.b
# default entry
#
image = /boot/vmlinuz-2.0.35-apm
label = newkernel
root = /dev/sdb1
read-only
image = /vmlinuz
    initrd = "/boot/initrd.gz"
    label = OpenLinux
    root = /dev/sdb1
    read-only
    append = "load_ramdisk=1 ramdisk_size=2880"
#
# additional entries
#
```

编辑 /etc/lilo.conf 文件后，使用 [root@digital /boot]# lilo -v -t 测试它是否有效
LILO version 20, Copyright 1992-1997 Werner Almesberger
Reading boot sector from /dev/hda
Merging with /boot/boot.b
Mapping message file /boot/message
Boot image: /boot/vmlinuz-2.0.35-apm
Added vmlinuz-apm *
Boot image: /boot/vmlinuz-2.0.35-modular
Added modular
Boot image: /vmlinuz
Added linux
The boot sector and the map file have *NOT* been altered.

如果一切正常，那么你可以通过发出以下命令创建引导扇区

```
[root@digital /boot]# lilo -v
LILO version 20, Copyright 1992-1997 Werner Almesberger
Reading boot sector from /dev/hda
Merging with /boot/boot.b
Mapping message file /boot/message
Boot image: /boot/vmlinuz-2.0.35-apm
Added vmlinuz-apm *
Boot image: /boot/vmlinuz-2.0.35-modular
Added modular
Boot image: /vmlinuz
Added linux
/boot/boot.0300 exists - no backup copy made.
Writing boot sector.
```

你现在可以测试新内核了。关闭系统并重新启动以开始模块配置。如果遇到任何问题，在重新启动时按 Tab 并输入之前内核的标签。

## 配置新模块并重新启动

一旦成功启动到新内核，你可能会认为自己完成了，但事实并非如此。你编译为模块的驱动程序尚未激活。要使它们激活，你需要进行一些配置。

Caldera 启动系统会在 /etc/modules 目录中查找一个以你构建的内核版本命名的目录。（在我示例中，此目录的完整路径为 /etc/modules/2.0.35。）在此目录中，它期望找到一个以内核构建时间和日期命名并以 .default 结尾的文件：

```
#1 Tue Jan 6 16:44:51 MET 1998.default
```

这是一个奇怪的文件名。系统期望的名称存储在内核本身中。要访问它，你可以使用以下命令：

```
[alberto@digital 2.0.35]$ uname -v
#2 Sat Oct 3 13:17:24 CDT 1998
```

使用此文本，你将创建新的模块列表，以便系统每次启动时加载你的模块。你将使用的命令有点复杂，但查看 BASH 手册页后，你可能会发现你正在使用一种称为命令替换的技术：

```
# find /lib/modules/2.0.35-apm -name "*.o" -print > " /etc/modules/2.0.35/ $(uname -v).default"
```

此命令查找新模块目录中的所有模块，列出它们，并将列表发送到 /etc/modules/2.0.35 目录中的正确文件。如果没有这样复杂的命令，这项工作会很繁琐，目前没有任何工具可以自动化此过程。如果你不这样做，你的新模块在计算机启动时不会自动加载。

完成此操作后，再次关闭并使用新内核重新启动。如果一切按计划进行，你的新模块现在将处于活动状态。欢迎使用你的新系统！

要访问内容，请点击章节和节标题。

## 《Linux 完全傻瓜指南》

Publisher: Macmillan Computer Publishing
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Part 4
Appendixes

准备好冒险了吗？渴望检查 Linux 并看看它能做什么？那么让我们通过安装 Linux 为你指明正确的道路。附录 A 中的信息可帮助你将 Linux 操作系统安装并运行起来。附录 B 是硬件兼容性指南，可帮助你判断你的机器的任何部分是否与 Linux 不兼容。现在，让我们开始吧，为你的计算机注入活力！

## Appendix A
Linux Installation

## In This Appendix

- Getting to Know Your Hardware
- Basic Requirements for Installing Caldera OpenLinux
- The Multiboot System
- Installing Linux
- Starting the Install
- Configuring X-Windows

在计算机上安装 Linux 并不会比安装 Windows 或任何其他操作系统（OS）更困难。如果你曾经



安装操作系统到一台 PC 上，你一定知道这有多令人沮丧。原因不明，“即插即用”设备有时无法被识别，或者随硬件提供的驱动程序与你正在安装的操作系统版本并不真正兼容；更糟的是，随操作系统一起提供的驱动程序与你的硬件不兼容。正如你所知，安装操作系统是一件棘手的事情。

只要遵循一些基本准则并为即将进行的任务做好准备，你就可以为自己节省大量麻烦和沮丧。首先，你最好对正在安装操作系统的硬件有所了解。如果你不知道，你可以尝试安装 Linux，但我敢打赌你会花大量时间来弄清你拥有什么硬件。为了降低你的整体压力水平，你确实需要比你可能愿意的更了解你的硬件。

安装的基本步骤如下：

- 收集有关硬件的信息
- 检查兼容性列表以确保硬件得到支持
- 决定你的 Linux 安装是否将与另一操作系统共享计算机
- 安装软件
- 提供一些配置

## 了解你的硬件

在你甚至尝试做任何事情之前，列出内部情况会为你节省无数时间。安装操作系统的用户通常知道盒子里有什么，并且他们拥有每件硬件的文档。以身作则——像他们一样做！

## 信息来源

你可以利用以下几个信息来源来识别你的硬件：

- **原始设备手册：**（你保存它们了，对吧？）
- **制造商提供的硬件规格：**网络可以是获取此信息的非常好的起点。越来越多的制造商将完整的规格放在网上。在开始安装之前，最好查阅它们。并且在系统运行后，也不要忘记定期检查更新的驱动程序和信息。
- **制造商本身：**你可以向系统制造商询问机箱内部的情况。如果你丢失了手册，你也可以要求制造商为你出售一份替换手册。（越来越多的制造商也在网上提供手册或其部分内容。）
- **你购买电脑的商店：**如果不是连锁店或来路不明的商家，其销售人员很可能知道他们卖给了你什么。
- **软件工具如 msd**（Microsoft System Diagnostics）：这些工具可以深入检查你的硬件并提供大量信息。过去，msd 随 DOS、Windows 和零售版 Windows 95 一起提供。你也可以从 ftp://ftp.microsoft.com/Softlib/MSLFILES/MSDZIP.EXE 获取它。最好从 DOS 运行 msd，因此将其复制到可启动的 DOS 软盘并用它启动计算机。当计算机启动后，输入 a:\msd，你应该会看到如下图所示的屏幕。（设备管理器，一个 Win95/98 控制面板工具，可能能够提供与 msd 一样多的信息。对于 WinNT，你也可以尝试 Windows NT Diagnostics。或者，如果你有 Norton Utilities，你也可以尝试一下。）如果你想将 msd 的输出保存到文件中，输入命令 a:\msd /F a:\report。
- **电脑内部：**最后，作为最后的手段，你始终可以拆开电脑并在内部查看一下。然而，这仅推荐给那些以前做过并知道如何处理静电敏感元件的人。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_298_0.png)

Msd 可以为你提供有关计算机硬件的许多信息。

特别是，你需要了解有关你的卡和设置的详细信息——你知道，像芯片组（计算机芯片的类型）之类的东西，对于你的视频设置很重要。例如，下图给你一个你需要了解的信息示例。这些细节应包括卡的品牌和型号，如果有的话，了解其 IRQ 和内存地址也不错。如果你的硬件是相当标准的 PC 硬件，msd 可以提供很大帮助；然而，像 SCSI、声卡和网卡之类的东西并不总是能被正确识别。唉，拥有电脑的传奇继续。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_298_1.png)

注意 msd 如何能够提供有关视频卡芯片组的信息。芯片组信息在带有 S3 86C375/86C385 的那一行上找到。寻找有关你自己硬件的此类信息。

## 硬件和网络清单

在继续之前，先列出清单——并仔细核对！为了帮助你，你可以使用表 A.1 和 A.2 作为指导。

### 表 A.1 硬件清单

| 设备 | 品牌 | 型号 | 备注 |
|---|---|---|---|
| CD-ROM |  |  |  |
| 以太网卡 |  |  |  |
| 鼠标 | COM（串行）端口号或 PS2 |
| 显卡 | 内存大小（MB） |
| 显示器 | 最大扫描频率和分辨率 |
| 调制解调器 | COM（串行）端口号 |
| RAM | 你有多少 RAM？ |

### 表 A.2 网络信息

| 项目 | 地址 |
| 机器的主机名 | |
| 你的网络的域名 | |
| 分配给你的计算机的 IP 地址 | |
| Netmask | |
| 广播地址 | |
| 网关/路由器地址 | |
| DNS 名称服务器（2） | |

在安装之前，了解有关硬件的信息至关重要。但如果你的计算机不支持从 CD-ROM 磁盘启动，你可能需要两张 3 1/2" 软盘（1.44MB），格式为 PC 格式。

## 安装 Caldera OpenLinux 的基本要求

那么，你需要什么样的硬件来安装 Linux？Linux 运行在大量平台上。本书附带的 CD 仅适用于基于 Intel 的 PC。其他发行版有适用于 Digital Alpha 硬件、Sun SPARC、PowerPC 和惠普 PA-RISC 工作站的软件。但请记住，基本的 PC 要求是任何 386、486、Pentium、Pentium Pro 或兼容的 PC 或克隆机。

就内存而言，安装的基本要求实际上相当适中，尤其是与其它操作系统相比。你应该能够在具有 8MB RAM 的基于 Intel 的计算机上安装 Linux。如果你打算使用图形环境，我强烈建议你将 16MB 视为合理的最低限度。虽然这在是否足够方面有些可疑，但对于最小安装来说可能已经足够了。不要期望最小系统运行迅速，因为资源将被用到最大限度。鉴于今天合理的内存价格，32MB 系统应该是你考虑的最低限度，如果你将使用图形环境在 Linux 上工作。拥有 32–40MB 将使 Linux 飞速运行，并且响应速度应该比你当前的操作系统更快。

就磁盘空间而言，最小安装可能可以装入 54MB（如果你安装 X Windows，则为 100MB），但在此大小下，许多重要功能将被省略。小安装大约需要 136MB。但请记住，标准安装推荐的空间为 418MB；本书假设你至少有这么多。所需或多或少的空间取决于你选择安装的选项。完整安装大约需要 1000MB，但大多数用户永远不需要这些额外功能。

除了这些基本要求之外，如果你打算利用图形界面，你还需要一台鼠标和受支持的显卡。

如果你的计算机满足或超过这些标准（任何现代的 350 美元 PC 似乎都能做到），你就可以检查你的硬件是否得到支持。

作为经验法则，Win 设备（Winmodems、Winprinters 等）不受支持。领先边缘硬件，与领先硬件相反，也可能不受支持。标准克隆设备将能工作，因为高质量的标准组件和广泛的可用性。

请参阅附录 B，“OpenLinux 兼容性指南”，以了解截至本书撰写时的最新兼容硬件列表。列出所需的模块，如果有的话。如果你的硬件未列出，它可能不受支持。某些组件，如以太网卡，如果你尝试 NE2000/NE1000 并提供卡的 IRQ 和内存地址，则可以使用。

## 多启动系统

如果你的硬件得到支持，在安装之前你只需要再做一个决定。如果你不确定 Linux 是否适合你，可以将 Linux 与当前操作系统一起安装。这需要多一点准备，但可以让你用 Linux 或其他操作系统启动计算机。

如果你考虑拥有双启动计算机，并且尚未安装其他操作系统，现在就继续安装吧。如果其他操作系统已经存在，你的安装会更容易。Linux 很可能能够识别其他操作系统，但你的其他操作系统可能不知道如何处理 Linux。

## 与另一操作系统共享磁盘

无论你是否考虑与另一操作系统共享磁盘，你都需要为 Linux 创建至少两个新的分区。分区是磁盘上由单个操作系统拥有和使用的部分。一个分区将容纳 Linux 本身，另一个将用于虚拟内存存储（交换空间）。交换分区的最小大小为 16MB，但通常，你希望分配与你拥有的 RAM 内存大小相同的交换空间。因此，如果你有 32MB RAM，你将需要 32MB 的交换区。

如果你的当前操作系统的分区使用所有可用磁盘空间，你仍然可能能够安装 Linux，前提是在分区内有可用空间。随 Linux 发行版一起提供有软件，允许你在不破坏磁盘当前内容的情况下重新分区硬盘。该软件称为 fips。

在运行 fips 之前，你需要对磁盘进行碎片整理，以确保重新分区过程有足够的空间。你的操作系统应该有这样的工具


as defrag.exe 或 optimize.exe 用于此目的。如果没有，有几种商业厂商提供的可用工具（Norton Utilities 就是其中之一）可以完成工作。Fips 只能处理 DOS 和 Windows 95 风格的分区。如果你运行的是 Windows NT 或 OS2，可能需要查看像 PartitionMagic（见 http://www.powerquest.com）这样的商业产品，它还支持 NTFS 和 HPFS——甚至 Linux 驱动器。

fips 程序连同一些你在安装前应 definitely 阅读的 readme 文件，位于 CD-ROM 上的 col\tools\fips15。让我们快速了解一下如何使用 fips 重分区你的磁盘空间：

- 1. 在重分区之前备份任何重要数据。如果出现问题，你将丢失所有现有数据。
- 2. 对系统进行碎片整理。
- 3. 将计算机启动到 DOS。（你可能需要创建一个 DOS 启动软盘；按照计算机手册操作即可。）
- 4. 将 Linux CD-ROM 插入计算机。如果你的启动软盘未启用 CD-ROM 使用，你可能需要将 fips 程序复制到另一张软盘。
- 5. 如果你的 CD-ROM 位于 D 盘，在提示符下输入 d:col\tools\fips15\fips.exe。如果你的 CD-ROM 可通过其他字母访问，请将其替换为正确的驱动器。

按照屏幕上的说明为 Linux 预留你预计需要的空间。合理的估计应包括 Linux 安装的大小（通常为 418MB）、交换空间的大小（与内存大小相同），以及使用 Linux 时创建的数据的额外空间（通常为几百兆字节）。要调整 DOS 分区的大小，请使用键盘上的方向键。按 Enter 设置适当大小。确认你的更改并重新启动计算机。

## 安装 Linux

你如何安装 Linux 将取决于你的 BIOS 是否支持从 CD-ROM 启动。如果你的计算机 BIOS 不支持从 CD-ROM 启动，你将需要创建两张软盘：一张是启动盘，另一张是模块（驱动程序）盘。

如果你的计算机支持从 CD 启动，可以跳过制作软盘的步骤；直接进入“开始安装”部分。

## 制作启动和模块软盘

如果你的计算机不支持从 CD-ROM 设备启动，你需要创建两张启动 Linux 安装的软盘。一张磁盘用于启动计算机（启动盘）。另一张磁盘（模块或驱动程序盘）将包含安装时如果需要访问 PC 卡（PCMCIA 设备支持）而必要的额外软件。（也许你正在使用 PCMCIA 网络或 SCSI 卡或其他外设。）
- 从网络安装。
- 从 SCSI CD-ROM 安装。

如果你的系统相当标准，很可能不需要第二张磁盘，但还是制作一份以防万一。要制作软盘，请按照以下步骤操作：

- 1. 将计算机启动到 DOS 或 Windows。
- 2. 将 Linux CD-ROM 插入计算机。（我假设你的 CD-ROM 位于 D 盘。如果位于其他位置，请替换为正确的驱动器号）。
- 3. 将 3 1/2" 1.44MB 软盘插入软盘驱动器。
- 4. 在 DOS 提示符下，输入 `d:\col\launch\floppy\rawwrite3`。
- 5. 输入磁盘映像文件的完整路径名：`d:\col\launch\floppy\install.144`。
- 6. 提供软盘的驱动器号（通常为 A）并按 Enter。

要制作模块软盘，请重复步骤 3–6，但提供模块映像的名称：`d:\col\launch\floppy\modules.144`。

请注意，`rawrite3` 有时在 Windows NT 4.0 系统和某些计算机系统 BIOS 芯片上会出现问题。如果 `rawrite3` 在你的计算机上无法制作出可用的磁盘，你可能需要借用朋友的计算机几分钟来制作可用的安装和模块磁盘。

## 开始安装

如果你的计算机不支持从 CD-ROM 启动，请插入安装软盘并启动计算机。几秒钟后你会看到 Linux 启动提示。按回车开始安装过程。

如果你的计算机支持从 CD 启动，将 CD 放入 CD-ROM，验证你的 BIOS 是否设置为从 CD 启动（参见计算机手册），并启动计算机。从 CD 启动是安装 Linux 到计算机的最快方式。

无论哪种方式，几秒钟后你会看到安装屏幕和一个 `boot :` 提示。按 Enter 以加快进程；否则，你将不得不等待约 20 秒后安装启动才开始。启动过程开始后，你会看到文本在显示器上滚动长达一分钟；可以安全地忽略这些进度报告。

## 语言选择

启动过程完成后，你将被提示选择安装期间使用的语言。选择适合你的语言。使用方向键更改选择。当你想要的选项被高亮显示时，按 Enter。请注意，在安装过程中，带白色文字的按钮是所选选项。这并不总是很明显。

## 键盘布局选择

接下来你将被要求选择与你的地区（国家）匹配的键盘布局。选择后按 Enter。

## 使用先前保存的配置

接下来，你将被问及是否要从已知配置恢复安装。应选择 No 选项（白色字母）；按 Enter。如果你是系统管理员类型的人，可能需要知道的是，在安装结束时，你可以将配置保存到磁盘。如果你要在多台机器上安装 Linux，可以使用磁盘上的配置信息，这样你就不必重复相同的配置选择数据。

## 更改 LISA 设置

下一个屏幕将提供 LISA（Linux 安装和系统管理实用程序）用于获取配置信息的各种选项。此屏幕上显示的选项如下：

- 禁用“即插即用”卡：操作系统以不同的方式处理即插即用卡，因此目前，你应避免更改任何即插即用设置。默认设置应是最安全的。
- 使用 BOOTP 进行自动网络配置：这会搜索来自启动参数服务器的信息。将其关闭。
- 使用 netprobe 进行自动网络配置：也将其关闭。此设置和前一个设置适用于拥有配置网络的系统管理员。
- 使用此设置并继续：此选项设置之前的设置并继续安装。

选择“使用此设置并继续”选项并按 Enter。LISA 现在将探测你的计算机并尝试定位一些基本硬件。

## 硬件发现（IDE/ATAPI）

初始探测后，LISA 将报告它找到的 IDE 和 ATAPI（CD-ROM）磁盘。验证你的 IDE 和 ATAPI 设备是否被找到。

按 Enter 并确认所有设备已被识别。如果没有，LISA 将对你的系统进行更详细的探测。

## 谨慎自动探测

如果你在被问及是否找到所有 IDE 和 ATAPI 设备时回答了 No，LISA 将探测更多设备。请继续谨慎自动探测。几分钟后，LISA 将显示探测期间找到的额外设备（如有）。注意找到的设备。（你可能需要使用上下箭头查看全部。）按 Enter 继续。

如果你的系统在谨慎探测期间冻结，你可以按重置按钮并重试安装。如果第二次尝试时系统仍然冻结，你可能发现了一个需要解决的硬件冲突——这是本书范围之外的主题。现在，你要么不得不忍受 Linux 未找到的设备，要么不得不查看 Caldera 的技术支持选项。（Linux 用户组也可能提供一些很好的信息资源。）

## 硬件发现（硬盘/CD-ROM/以太网）

如果所有设备都被找到，请回答“已识别硬件”问题的 Yes。否则，回答 No 以使用内核模块管理器手动加载额外的内核模块。

## 内核模块管理器

如果并非所有硬件都被找到，你需要手动指定缺失的设备并为其选择适当的模块（驱动程序）。如果你制作了列表并验证了组件与 Linux 兼容，这并不算太困难。

选择“加载内核模块”选项并按 Enter 手动选择任何缺失的设备。在显示的“加载内核模块”面板上，选择你想要加载的驱动程序类型。例如，如果你的以太网卡未被识别，选择“加载网络卡驱动程序”并按 Enter。

然后你将被提供一份所有可用驱动程序的列表。如果你的卡在列表中，选择它并按 Enter 继续。你可能需要在卡被成功识别前提供一些参数。如果是这样，请阅读下一节“模块选项”。

## 模块选项

在键盘上按 Alt+F2 并在登录提示符下输入 help。这将显示安装帮助系统。选择“列出模块加载的可能参数”选项。将显示模块和所需参数的列表。按 j 逐行向下滚动，按 k 逐行向上滚动。要一次移动整个屏幕，请按 f 或 b 分别向前或向后移动。找到你需要的驱动程序的文档。

例如，我的网络卡是 LynkSys Ether16，这张卡未被 Linux 自动识别。然而，许多 PC 以太网卡与 NE2000/NE1000 兼容。如果你向下滚动文档，你会看到它的条目，告诉你 NE2000/NE1000 需要两个参数——IO 和 IRQ 设置。记下这一点，然后按 q 退出帮助文档。这将返回到安装帮助系统。选择“退出此帮助系统（退出）”选项并按 Enter。按 Alt+F1 返回到安装窗口，选择正确的模块（就我而言是 NE2000/NE1000），并根据你的安装列表提供参数。

如果你绝对无法弄清楚要为模块提供哪些正确参数，请尝试在不指定任何参数的情况下使用该模块。虽然


this is not recommended, some modules will work this way.

When you attempt to load the module, you will be informed whether this worked. Keep in mind that you might be prompted to insert the modules floppy at some point. Press Alt+F6 to see any diagnostic errors that might have been raised when the module was loading. Press Alt+F1 to return to the installation screen. You should see a message indicating whether your card was recognized. Repeat the process for any other devices that weren’t recognized.

The Hardware found screen should now list any added devices. Press Enter to continue the installation. If you are done loading modules, select Return to previous menu and press Enter. Then select Finish kernel module management and press Enter.

## Changing the Partition Table

At this point you might need to define partitions for Linux and its swap area. If you do, answer Yes to the Change Partition Table panel.

This will prompt you to select a disk. Pick the disk you want to change, and answer Yes to the Change Partition Table panel.

## Using Fdisk

You will be dumped into an fdisk session. Fdisk is used to define partitions. It is a dangerous program because it gives you the ability to delete a partition that contains data.

## Creating the Primary Linux Partition

Follow these steps to create the primary partition:

- 1. Enter p to list all current partitions. Make a note of where the partition ends.
- 2. To create the main Linux partition, enter n.
- 3. Enter p to create a primary partition. You’ll then be asked to provide a primary partition number. Disks are only allowed to have four primary partitions. Enter a number one higher than the existing number of partitions on your disk. For example, if your disk currently contains a single partition, enter the number 2. If there are no partitions on your disk, enter the number 1.
- 4. When it asks you for the first cylinder, enter the first number you see in the parentheses. This should be a number larger than the ending cylinder of the existing partition. If there is no partition already on your disk, enter the number 1.
- 5. Specify the size of the new partition in megabytes by entering, for example, +1024MB—making sure that you create a partition large enough for the type of installation that you intend to do plus some extra space for your files.
- 6. Enter p to list all partitions. Your new partition should be listed there.

## Creating the Swap Partition

Follow these steps to create the swap partition:

- 1. To create a new partition, enter n.
- 2. Enter p to create a primary partition. When prompted for a partition number, enter a number one higher than the number of partitions that exist so far, including the primary partition you just created.
- 3. Enter the number suggested for the first cylinder. This number should be one higher than the end cylinder in the previous partition.
- 4. Your swap partition should be at least 16MB. I suggest that you allocate a partition the same size as the amount of real RAM you have installed. If you have 64MB of RAM, enter +64M.
- 5. Enter t to change the partition type. When prompted, enter the number of your swap partition. Then, enter the type code for a swap partition: 82.

## Saving Your Changes

To save your changes, enter w. This will write your new partitions to disk and exit the program. When returned to the Hard Disk Selection panel, select No further hard disk changes and press Enter.

You will now be warned that you might need to reboot your system to ensure that your partitions were properly allocated on disk. This is not normally necessary with recent computers; most users can continue with the install process safely. If you do have an older system and decide to reboot, you’ll have to redo many of the Linux install steps up to this point.

## The Configure Swap Space Panel

The partition that you designated for the swap area should be highlighted. Click Continue to initialize it. This will enable Linux to access it.

## Installation Source Selection

Next, you are prompted for the Installation Source Selection; don’t freak out—this is just a fancy way of asking you where your Linux installation disk is. Select CD and press Enter. A window with a list for all possible CD devices is displayed. If you have a standard ATAPI CD-ROM, you should see your CD-ROM selected. Otherwise, select the appropriate drive as per your configuration list.

LISA will confirm the version of the CD you are using for installation. Press Enter to acknowledge that this is what you want.

## Creating the Root Partition

Next, you are asked to select the root partition. LISA should highlight the partition you created earlier for this purpose; press Enter.

LISA will confirm that the selected partition will be erased and all data it currently contains will be lost. Press Enter to confirm your choice or press your arrow key to select No to cancel the operation.

LISA will ask you if you want to check the new partition for errors. This is generally necessary only for older 386 or 486 computers or for cautious individuals. If your computer is a newer system, you can safely skip the error check. (This type of error check can take many hours if you happen to be running it on the newer, larger hard drives.) After a few moments, you’ll be asked if you want to mount additional partitions. Select No. You will see information as LISA formats and prepares the partition. The format process can take anywhere from a few moments to a few hours, depending on the size of the disk and whether you chose to verify the format.

## Selecting the Installation Type

You are then prompted to select the type of install. Select standard system. This book assumes that you will use this type of installation. (Note that 418MB of disk space is required for this installation, and that this number does not include space for your own data files.)

## Selecting the X-Server

Next, you need to pick the X11 server appropriate for your video card. The X11 server is the software that displays a graphical user interface on your screen. This software is matched to the type of video card you have. Moving up and down through the list with your arrow keys, use the Spacebar to select both of the following servers:

- The server that matches the chipset on your video card
- The server called XFree86-SVGA

By default, the XFree86-VGA16 server will also be installed. This 16-color server will allow you to configure the server that more closely matches your card. If the server that matches your card doesn’t work, you can then try the SVGA server. If you are unable to find another server that works with your card, the generic VGA16 server will always be available. Keep in mind, however, that choosing this type of server will limit you to a small screen with only 16-color support.

From here on, Linux will begin to copy and install files. When it finishes doing so, it will ask you for some additional information. In the meantime, go and take a coffee break. This process will take anywhere from 10 minutes to several hours, depending on the speed of your CD-ROM drive, speed of your CPU (386, 486, or faster), and type of install you selected (although you shouldn’t have chosen any other type of install when we’ve coached you to choose standard system).

## Configuring the Network

When file copying is completed, you will be prompted for various Network settings.

## Hostname Entry

In the Hostname Entry panel you are asked for the fully qualified domain name of your computer. If your computer is in a networked environment, enter that name here. Otherwise, name your computer anything you want, but use a domain like the default .nodomain.nowhere (a domain that doesn’t exist).

## Network Card Configuration

Next, you are asked if you have a network card. Enter Yes if you do, No otherwise. If you have a network card, its name is probably eth0 (multiple network cards are named by exchanging the 0 for some other number). Enter eth0 as the device name for the network interface.

The next step is to provide an IP address for the card. If your computer is on a small, local network without a registered IP number(s), use an IP like 192.168.0.1 or 10.0.0.1. (You can replace the 1 with any number up to 254, depending on this machine’s location in the network.) These IP sets are reserved for private networks that are not registered with Internet IP numbers. If this computer will have a registered IP number on the Internet, provide a real IP number.

Enter a network mask if yours differs from the one that Linux calculated for you; same for the broadcast address. If you have a router or gateway, press Enter to set its IP; otherwise, select No and press Enter.

If you have a DNS name server, press Enter to enter this IP; otherwise, answer No. Or, if you have NIS information from your system administrator, enter it now. Otherwise, you should select Do not use NIS and press Enter.

## Configuring the Clock

If your clock is set to Greenwich Mean Time, select this option. If not, select Local Time. If you don’t know, your computer is almost certainly set to local time. When asked to do so, pick your time zone.

## Configuring the Mouse Type

In the Configure Mouse Type panel, you get to pick the type of mouse you have. Select the appropriate setting and press Enter. If you’re asked to select a serial port for your mouse, select the port to which your mouse is connected.

## Selecting your Printer

Select your printer from the list of available printer types. If a driver or module for your exact printer is not available, select another model by the same manufacturer. I have an Epson Photo Stylus 700 printer and use the Epson Stylus Color setting. You’ll then be asked for the port to use in communicating with the printer, the default resolution, and the default paper size. Provide the appropriate values.

## Setting the Root Password





在提示输入 root 密码时，你猜会问什么？这里就是设置 root 密码的地方。现在，你可能会问，世界上 root 到底是什么？Root 是一个特殊的管理员账户，只能用于系统配置。这个密码至关重要。不管你把它设成什么，都一定要记住。否则，你可能不得不重新安装系统。请注意，在输入密码时你的字符不会显示出来。这样别人就无法从你身后窥视并窃取你的密码。输入一次后，系统会要求你再次输入，以确保你输入正确。

账户将在本书的前几章中详细介绍。目前，只要记住这个密码即可。

## 创建第一个账户

如果只能使用 root 账户进行系统配置，那么日常使用时你用哪个账户呢？在 root 密码设置之后，下一步就是创建你自己的主账户。这就是你在 Linux 中工作时通常使用的账户。选择一个用户名（八个字符，无空格）。通常，你的账户将是你的名字或你名字和姓氏的组合，尽管也可以是你的昵称。输入你名字的首字母后跟你的姓氏，或你喜欢的任何内容。

将显示的 UID 保持不变（100）。

选择用户标准组。

按 Enter 设置用户的 home 目录。它应显示为 /home/username，其中 username 是你为账户选择的用户名。

在 shell 选择中，将 GNU bash 保留为默认选项。

输入你的全名并为你的账户提供一个密码。同样，在输入时你的字符不会显示，并且系统会要求你输入两次密码。

不要忘记你的用户名和密码；你需要它们来登录。请注意，密码和登录名区分大小写。

## 配置 LILO

接下来的几个步骤配置 LILO 启动管理器。LILO 是在你使用 Linux 时负责启动计算机的软件。如果 Linux 与另一台操作系统共享你的计算机，LILO 可以在启动计算机时为你提供操作系统选择。要做到这一点，LILO 必须安装在第一块硬盘的 MBR（主引导记录）上。

有些操作系统，比如 Windows NT，很不喜欢 LILO。对于带有 NT 的多启动系统，你需要将 LILO 安装在 Linux 根分区上而不是 MBR，并配置 NT 加载程序，以便在启动计算机时为你提供选择。其他操作系统如 MS-DOS、Windows 95 和 Windows 98 与 LILO 安装在 MBR 上配合良好。

安装 LILO 时，系统会要求你为系统选择一个 Linux 内核。选择默认项（/boot/vmlinuz）并按 Enter。如果要求提供初始 ramdisk 文件映像，请按 Enter 选择默认文件。如果要求命名启动映像，默认名称 linux 应该使用。在启动参数框中，按 Enter 接受默认显示的值，除非你确实需要为硬件添加一些特殊参数。当 LILO 安装菜单再次显示时，选择 No further entries to add to LILO 并按 Enter 以显示 LISA 为你构建的配置文件。按 Enter 继续，并在显示 Install LILO as configured 对话框时，再次按 Enter 安装 LILO。

## 配置守护进程服务

对守护进程/服务器自动启动所列的选项说 OK。除非你知道自己在做什么，否则应保持这些选项不变。如果将来某个时候需要更改这些设置，你可以使用 LISA 在无需重新安装 Linux 的情况下进行更改。

## 配置 X Windows

要配置 X Windows，请选择适合你的卡的 X11 服务器并按 Enter。

选择 Yes 立即调用 XF86Setup。对于 LISA，“立即”实际上意味着“推迟到安装完成之后”，因此你将在稍后才看到 XF86Setup。

如果你手边有另一张软盘，可以将配置保存到软盘，以防将来需要恢复。这样可以避免手动重新配置安装。

恭喜！你已在系统上安装了大部分 Linux。你的计算机现在将启动到 Linux，之后你将能够设置 X 服务器。在启动过程中，你会注意到 Linux 启动时滚动的状态信息。此过程所需的时间从几秒到几分钟不等，具体取决于计算机的速度。

## XF86Setup

在计算机完成启动到 Linux 后，你应该会看到一个带有 X 形鼠标指针的图形屏幕。几秒钟后，XF86Setup 程序将被显示。

如果你的鼠标可以使用，你可以用鼠标单击方框并选择各种选项。否则，你可能必须使用箭头和 Tab 键在各种选项之间移动。使用 Enter 键激活选项。

## X Windows 的鼠标设置

鼠标配置屏幕允许你设置有关鼠标的详细信息（见下图）。Linux 喜欢具有三个按钮的鼠标设备。如果你的鼠标只有两个，你可能需要考虑购买一个价格便宜的三按钮鼠标。你的另一个选择是选择 Emulate3Buttons 选项。这要求你同时按下两个鼠标按钮来模拟中间按钮。

请注意，配置一个无法工作的鼠标可能很棘手。例如，一些较新的 Logitech 鼠标设备使用 Microsoft 协议，而一些较旧的 Microsoft 鼠标设备使用 Logitech 协议。如果你的鼠标较旧，请尝试将鼠标名称与协议名称匹配。如果你的鼠标是较新的串行鼠标，它很可能是一个 Microsoft 鼠标，无论其制造商如何。如果你的鼠标已连接到 PS/2 鼠标端口，请选择 PS/2 协议。如果你的鼠标已经可以工作，就让它保持原样吧！

![](img/edf072a03d4de1f8f4a13465ac79e7fb_311_0.png)

鼠标配置选项允许你微调和配置鼠标设置。如果你的鼠标可以工作，你应该将大多数设置保持为默认设置。

## 键盘配置

要开始键盘配置，请选择显示顶部（见下图）的 Keyboard 按钮。很可能你的键盘已经正常工作。许多人喜欢的一项设置是将 Caps Lock 键（A 键右侧）分配为 Ctrl 键。这只是众多可能选项中的一个。键盘选择还具有来自 Dell 和其他厂商的特定键盘设置，包括笔记本型号。检查此选项，看看你是否列出了其中之一。完成配置后单击 Apply 按钮。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_311_1.png)

键盘选项允许你选择键盘并控制各种选项，例如 Ctrl 键的位置。

## 视频卡配置

要开始视频卡配置，请选择显示顶部的 Card 按钮。下图显示了你的视频卡配置。只要你选择了与卡匹配的适当 X11 服务器，你应该能够指定最少的设置来识别你的卡。你需要指定你拥有的视频 RAM 数量和芯片组。如果你知道确切的卡和芯片设置（例如 S3 86C375/86C385 类型），你可以单击 Card List 按钮，选择正确的卡，然后按 Detailed Setup。

如果你不知道特定值，请使用 Probed 选项。XF86Setup 将尝试查询卡以获取未知信息。如果你的卡未知，你可能需要尝试 SVGA 设置。系统将无法使用卡可用的高级功能，但你可以在找到有关系统的更多信息时工作。

## 配置你的显示器

要开始显示器配置，请选择显示顶部的 Monitor 按钮，如下图所示。你需要知道显示器的规格并提供水平和垂直刷新率的适当范围。如果你不知道，可以从列出的选项中选择一个。请注意，为显示器提供正确的选项非常重要。使用错误的刷新率会使显示器超频，可能损坏它。对于非多同步型显示器来说，这更成问题。如果你有显示器手册，你应该手动输入设置。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_312_0.png)

这是你的视频卡的配置屏幕。请注意，你可以通过单击 Card List 按钮并选择你的卡来分配多个设置。

笔记本显示器尤其棘手。较新的笔记本可能使用标准的 640×480、800×600 或 1024×768 模式而无需问题工作。（选择与笔记本显示器匹配的分辨率。）另一方面，一些笔记本可能会出现显示问题。在我的笔记本上我一直无法找到正确的设置，因此当我启动到 X-Windows 时，我的屏幕会跳动。多年来我的解决方法是在显示器输出选项（内部和外部）之间切换，这 somehow 在会话中修复了问题。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_312_1.png)

显示器分辨率选择显示器能够支持的刷新率。超频刷新率会损坏显示器。

## 选择分辨率

要开始分辨率配置，请选择显示顶部的 Modeselection 按钮。你将看到下图所示的屏幕。根据视频卡拥有的视频 RAM 数量，可能可以指定各种分辨率和颜色设置。默认情况下，X-Windows 将使用卡可以处理的最大的分辨率。在某些环境中，这意味着启用虚拟屏幕，其中屏幕从右侧和底部边缘掉落。将光标移动到右侧或底部边缘会滚动你所看到的内容。对我来说，这种设置很令人不安，所以我指定与我的显示器功能相匹配的设置。





颜色深度选择由面板底部的四个按钮激活：8 bpp（每像素位数）将产生 256 种颜色，16bpp 将产生 32768 种颜色，而 24 和 32bpp 分别将产生 65535 和数百万种颜色。请注意，并非所有显卡都支持所有显示深度。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_313_0.png)

Modeselection 面板允许您设置要在监视器上使用的分辨率以及默认颜色深度。

## 其他配置

其他配置涉及切换分辨率和退出 X 服务器的选项（参见下图）。Ctrl+Alt+数字键盘上的加号 (+) 和减号 (-) 键允许您即时在不同显示分辨率之间切换。Ctrl+Alt+Backspace 序列用于立即退出 X 服务器。如果您启动到 X Windows 而无法读取屏幕，Ctrl+Alt+Backspace 将带您返回到命令行提示符。您可能需要在配置正确之前这样做一次或两次。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_313_1.png)

其他配置面板允许您设置有关切换分辨率和退出 X-Windows 的选项。

## 完成配置

当您单击“完成”退出 XF86Setup 程序时，XF86Setup 会提示您确认是否已完成系统设置。如果您选择“确定”，XF86Setup 将尝试使用您为监视器和显卡指定的设置启动您卡专用的 X 服务器。如果您的设置看起来正常，您就完成了。如果您的屏幕被挤压并且监视器几何按钮无法纠正问题，您可能需要使用 xvidtune，这是一个可以微调视频速率的程序。Xvidtune 是一个潜在危险的程序，只有在您无法使用监视器的控件调整画面时才应使用。

如果您的设置正确，您应该会看到黑白网格作为屏幕的背景，以及一个没有标题栏的窗口，其与屏幕左上角对齐。如果正确，请单击“保存配置并退出”按钮。您的系统现在将启动到多用户模式并准备使用。

恭喜！现在您已经安装并配置了 Caldera OpenLinux，请转到第 1 章“在 KDE 桌面上的首次登录”，开始使用您的新操作系统。

目录

Products | Contact Us | About Us | Privacy | Ad Info | Home

使用本网站须遵守某些条款和条件。Copyright © 1996-2000 EarthWeb Inc.
保留所有权利。未经 EarthWeb 明确书面许可，不得以任何形式或媒体复制全部或部分内容。

## SPIDER KILLER

## spider catcher

- HOME
- ACCOUNT INFO
- SUBSCRIBE
- LOGIN
- SEARCH
- MY ITKNOWLEDGE
- FAQ
- SITEMAP
- CONTACT US

要访问内容，请单击章节和节标题。

## Complete Idiot's Guide to Linux

（出版商：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

Bookmark It

Search this book:

目录

## 附录 B
OpenLinux 兼容性指南

本附录经 Caldera 网站许可转载。如需最新信息，请访问 http://www.calderasystems.com/products/openlinux/hardware.html。如果您的硬件未列出，很可能不受支持。请联系制造商获取更多信息或购买兼容的替代品。确保您的型号与受支持的指定完全匹配非常重要。

## CD-ROM 驱动器

以下是 Caldera OpenLinux 1.3 版支持的 CD-ROM 驱动器和接口卡列表。

## CD-ROM 驱动器

## 支持的 CD-ROM 驱动器

| Company | Model |
|---|---|
| Aztech | CDA268-01A |
| Conrad | TXC |
| Creative Labs | CD-200F (CD-200 not fully supported) |
| CyCDROM | CR520 |
|  | CR520ie |
|  | CR540 |
|  | CR940ie |
| ECS-AT | Vertos 100 |
| Funai | E2550UA |
|  | MK4015 |
|  | 2800F |
| Goldstar/Reveal | R420 |
| IBM | External ISA drive |
| Kotobuki | See Panasonic |
| Laseramate | CR328A |
| Longshine | LCS-7260 |
| Matsushita | See Panasonic |
| Mitsumi | CRMC LU005S |
|  | FX001S (single speed) |
|  | FX001S (multisession) |
|  | FX001D (double speed) |
|  | FX001D (multisession) |
| Okano/Wearnes | CDD110 |
| Optics Storage | DOLPHIN 8000 AT |
| Orchid | CDS-3110 |
| Panasonic | CR-521 |
|  | CR-522 |
|  | CR-523 |
|  | CR-562 |
|  | CR-563 |
| Philips/LMS | cm206 (w/ cm206 card) |
| Sanyo | CDR-H94A |
| Sony | CDU-31A (not auto-probed) |
|  | CDU-33A (not auto-probed) |
|  | CDU-510 |
|  | CDU-515 |
|  | CDU-531 |
|  | CDU-535 |
| Teac | CD-55A |

## 支持的 CD-ROM 接口卡

## 支持的 CD-ROM 接口卡

## Company

- ISP16
- MAD16
- Mozart

大多数具有 512 或 2048 字节块大小的 SCSI 驱动器应该可以工作。您需要有受支持的 SCSI 控制器卡才能使用其中一个驱动器。注意：一些 CD-ROM 驱动器随附非标准的 SCSI 适配器，可能不受支持。

大多数通过 IDE/ATAPI 接口连接的驱动器应该可以工作。目前销售兼容驱动器的一些厂商包括 Aztech、Mitsumi、NEC、Sony、Creative Labs 和 Vertos。一些多 CD 换带机，如 NEC CDR-251 和 Sanyo 的“非标准”3-CD 换带机作为 ATAPI 驱动器受支持，因此在前面的列表中没有特殊的驱动程序。以下文档末尾包含了一个示例 CD 更换程序：

/usr/src/linux/Documentation/cdrom/ide-cd

CyCDROM 940i 和 520ie 驱动器，虽然连接到 IDE 接口，但不是 IDE 设备；它们使用 Aztech 驱动程序。

## 并行端口 CD-ROM 驱动器

## 兼容的并行端口 CD-ROM 驱动器

| Company | Model | Module |
|---|---|---|
| Arista | ParaCD 525 (4/8 bit only) | arcd |
| DataStor | EP2000 | dscd |
| Freecom | Power CD* | pwcd |
| KingByte Information Sys. | KBIC-951A | kicd |
| Microsolutions | Backpack (modern) | bpcd |
|  | Backpack (old) | bpmcd |
| OnSpec Electronics | 90c26 | oicd |
| Shuttle Technologies | EPIA | eicd |
|  | EPAT | epcd |
|  | EPEZ | epcd |

*必须先在 DOS 中使用 POWER-CD.SYS 初始化；然后使用 LOADLIN 启动到 Linux。

## 网络卡

以下是 Caldera OpenLinux 1.3 版（包括 Standard、Base 和 Lite）支持的以太网、帧中继、令牌环和无线调制解调器卡列表。

## 以太网卡

## 以太网卡

| Company | Model | Module |
|---|---|---|
| 3Com | Etherlink | 3c501 |
| 3Com | Etherlink II | 3c503 |
| 3Com | Etherlink II/16 | 3c503 |
| 3Com | Etherlink Plus | 3c505 |
| 3Com | Etherlink16 | 3c507 |
| 3Com | Etherlink III (3c509) | 3c509 |
| 3Com | Etherlink III (3c579) | 3c509 |
| 3Com | Fast Etherlink (3c590, 3c592, 3c595, 3c597) | 3c59x |
| 3Com | Fast Etherlink XL (3c900, 3c905, 3c905B) | 3c59x |
| 3Com | Corkscrew Etherlink XL (ISA) | 3c515 |
| Accton | EtherDuo PCI | tulip |
| Accton | EN1207 (all three types) | tulip |
| Adaptec | ANA6901/C | tulip |
| Adaptec | ANA6911/TX | tulip |
| Allied Telesis | AT1500 | lance |
| Allied Telesis | AT1700 (ALPHA) | at1700 |
| Allied Telesis | LA100PCI-T | tulip |
| AMD Lance | PCnet-ISA | lance |
| AMD Lance | PCnet-ISA+ | lance |
| AMD Lance | PCnet-PCI | lance32 |
| AMD Lance | PCnet-PCI II | lance |
| AMD Lance | PCnet-32 | lance32 |
| Ansel Com. | AC3200 EISA | ac3200 |
| Apricot | Xen-II | apricot |
| ARCnet | All (ALPHA) | arcnet |
| AT-Lan-Tec/Realtek | RTL8002 (chipset) | atp |
| AT-Lan-Tec/Realtek | RTL8012(chip) | atp |
| Bay Networks | Netgear FX310 TX 10/100 | tulip |
| BOCA | AMD 79C960 based cards | lance |
| Cabletron | E2100 | e2100 |
| C-NET | CNE-935 | tulip |
| Cogent | EM100 | tulip |
|  | EM110 | tulip |
|  | EM400 | tulip |
|  | EM960 | tulip |
|  | EM964 Quartet | tulip |
| Compaq | Netelligent 10(PCI) | tlan |
|  | Netelligent 10/100(PCI) | tlan |
|  | Integrated NetFlex-3/P(PCI) | tlan |
|  | NetFlex-3/P(PCI) | tlan |
|  | ProLiant Netelligent 10/100(PCI) | tlan |
|  | Dual Port Netelligent 10/100(PCI) | tlan |
|  | Deskpro 4000 5233MMX (PCI) | tlanCompex |
|  | Readylink ENET100-VG4(EISA/PCI) | hp100 |
| Danpex | EN-9400P3 | tulip |
| D-Link | DE-530CT | tulip |
|  | DE-600 | de600 |
|  | DE-620 | de620 |
|  | DFE500-Tx | tulip |
| DEC | DEPCA | depca |
|  | DE-100 | depca |
|  | DE-101 | depca |
|  | DE-200 Turbo | depca |
|  | DE-201 Turbo | depca |
|  | DE-202 Turbo (TP BNC) | depca |
|  | DE-203 Turbo (BNC) | ewrk3 |
|  | DE-204 Turbo (TP) | ewrk3 |
|  | DE-205 Turbo (TP BNC) | ewrk3 |
|  | DE-210 | depca |
|  | DE-422 (EISA) | depca |
|  | DE-425 (TP BNC EISA) | de4x5 |
|  | DE-434 (TP PCI) | de4x5 |
|  | DE-435 (TP BNC AUI PCI) | de4x5 |
|  | DE-450 (TP BNC AUI PCI) | de4x5 |
|  | DE-500 10/100 | de4x5 |
|  | EtherWORKS | depca |
|  | EtherWORKS III | ewrk3 |
|  | EtherWORKS 10 (PCI) | tulip |
|  | EtherWORKS 10/100 (PCI) | tulip |
|  | QSILVER | tulip |
|  | DEC chips 21040/21041/21140 | tulip |
|  | DEC chips 21142/21443 | tulip |
|  | DEC chips 21040(no SROM)/21041A | de4x5 |
|  | DEC chips 21140A | de4x5 |





| 厂商 | 型号 | 驱动程序 |
|---|---|---|
| Digi | RightSwitch SE/x | dgrs |
| Fujitsu | FMV-181 | fmv18x |
| Fujitsu | FMV-182 | fmv18x |
| Fujitsu | FMV-183 | fmv18x |
| Fujitsu | FMV-184 | fmv18x |
| Hewlett-Packard | 100VG-AnyLan | hp100 |
| Hewlett-Packard | 27248B (Cascade) | hp100 |
| Hewlett-Packard | AMD 79C960 based cards | lance |
| Hewlett-Packard | J2405A | lance |
| Hewlett-Packard | J2577 (Cascade) | hp100 |
| Hewlett-Packard | J2577 (REVA Cascade) | hp100 |
| Hewlett-Packard | J2573 (Cascade) | hp100 |
| Hewlett-Packard | J2573 (REVA Cascade) | hp100 |
| Hewlett-Packard | J2585 | hp100 |
| Hewlett-Packard | J2585[AB] | hp100 |
| Hewlett-Packard | J2970 | hp100 |
| Hewlett-Packard | J2973 | hp100 |
| Hewlett-Packard | PC-Lan | hp |
| Hewlett-Packard | PC-Lan Plus | hp-plus |
| ICL | EtherTeam 16i | eth16i |
| ICL | EtherTeam32 (EISA) | eth16i |
| Intel | EtherExpress Pro/10 | eepro |
| Intel | EtherExpress Pro/10(PCI) | eep10pci |
| Intel | EtherExpress Pro/100B | eepro100 |
| Intel | EtherExpress 16 | eexpress |
| Intel | Other i82557 based cards | eepro100 |
| Kingston | DEC 21x4x based cards | de4x5 |
| Kingston | AMD 79C960 based cards | lance |
| Kingston | EtherX KNE100TX | tulip |
| Kingston | EtherX KNT40T | tulip |
| Linksys | AMD 79C960 based cards | lance |
| Linksys | DEC 21x4x based cards | de4x5 |
| Linksys | EtherPCI | tulip |
| NE1000 |  | ne |
| NE1500 |  | lance |
| NE2000 |  | ne |
| NE2100 |  | lance |
| NI5210 |  | ni52 |
| NI6510 |  | ni65 |
| Pure Data | PDI8023-8 | wd |
| Pure Data | PDUC8023 | wd |
| Pure Data | PDI8023-16 | wd |
| RealTek | See AT-Lan-Tec |  |
| Schneider & Koch | G16 | sk_g16 |
| SMC | 83c790 chips | smc-ultra32 |
|  | 8432 | de4x5 |
|  | 8432BT | tulip |
|  | 9000 Series | smc9194 |
|  | Ultra | smc-ultra |
|  | EtherEZ | smc-ultra |
|  | EtherPower 10 (PCI) | tulip |
|  | EtherPower 10/100 (PCI) | tulip |
|  | Ultra32 EISA | smc-ultra32 |
|  | EtherPower II | epic100 |
| Surecom | EP-320X | tulip |
| Thomas Conrad | TC5048 | tulip |
| Western Digital | WD80x3 based cards | wd |
| Zenith | Z-Note | znet |
| Zynx | ZX312 EtherAction | tulip |
|  | ZX314 | tulip |
|  | ZX315 EtherArray | tulip |
|  | ZX316 10/100 4 port | de4x5 |
|  | ZX34x/351 | tulip |

## 帧中继卡

| 公司 | 型号 | 模块 |
|---|---|---|
| Sangoma | S502A | sdl a |
|  | S502E | sdl a |
|  | S507 | sdl a |
|  | S508 | sdl a |

## FDDI 卡

| 公司 | 型号 | 模块 |
|---|---|---|
| DEC | FDDI controller (EISA/PCI) | defxx |

## 无线调制解调器/网络卡

| 公司 | 型号 | 模块 |
|---|---|---|
| AT&T | GIS Wavelan | wavelan |
| Baycom | par96 | baycom |
|  | par97 | baycom |
|  | picpar | baycom |
|  | ser12 | baycom |
| Creative Labs | SoundBlaster | sm |
| Gracilis | PackeTwin | pt |
| Ottawa Amateur Radio Club | PI | pi2 |
|  | PI2 | pi2 |
| WSS | WSS(half duplex) | sm |
| z8530 SCC |  | scc |

## 令牌环卡

| 公司 | 型号 | 模块 |
|---|---|---|
| IBM | Any non-DMA cards | ibmtr |

## 软盘驱动器

OpenLinux 不支持的软盘驱动器数量如此之少，以至于几乎不值得一提。无论如何，在内核源代码中，提到了一些笔记本驱动器，因为需要特殊的引导/模块参数才能使其正确工作。此外，还有一些可以用于调整软盘支持的引导参数。OpenLinux Base 和 OpenLinux Standard 客户可以联系 Caldera 了解这些参数的详细信息，或查看 BootPrompt-HOWTO。

## 兼容的笔记本软盘驱动器

| 公司 | 型号 | 模块 |
|---|---|---|
| HP | Omnibook | floppy |
| IBM | L40SX ThinkPad | floppy |

## IDE 驱动器

以下是 Caldera OpenLinux 版本 1.3 支持的 IDE 驱动器列表。

## IDE 硬盘驱动器、CD-ROM 驱动器和磁带驱动器

“255 个磁头”的磁盘几何转换被检测到并由 genhd 模块支持。

这些驱动程序支持一个或多个 IRQ 上的最多四个 IDE 接口，最多可使用八个磁盘/CD-ROM/磁带/软盘驱动器。OpenLinux 默认情况下随附对前两个控制器上的 IDE 硬盘驱动器的支持（每个控制器 2 个驱动器 = 总共 4 个驱动器），并包含多达四个额外设备而无需分区的文件。唯一可以在不创建新设备文件的情况下使用分区的设备是连接到前两个 IDE 控制器的前四个硬盘驱动器。

将硬盘驱动器连接到声卡 IDE 接口的用户需要制作新的设备文件。OpenLinux Base 和 OpenLinux Standard 客户可以联系技术支持，了解如何制作这些设备文件的详细信息。

## 兼容驱动器

| 型号 | 模块 |
| --- | --- |
| 硬盘驱动器 | ide |
| CD-ROM 驱动器 | ide-cd |
| 磁带驱动器 | ide-tape |

## IDE 软盘（可移动）驱动器

警告：此硬件支持领域被认为在当前“完整发布”内核中相当不稳定，包括 2.0.35（OpenLinux 1.3 系统默认运行的版本）。使用可移动 IDE 驱动器支持时请谨慎操作，如果这要在生产或任务关键型系统上运行，请考虑使用其他类型的硬件。

## 软盘驱动器

| 公司 | 型号 | 模块 |
| --- | --- | --- |
| EASYSTOR | LS-120 | ide-floppy |
| Iomega | ZIP Drive | ide-floppy |

## 鼠标指针设备

Linux 内核中的通用串行端口驱动程序支持串行鼠标设备。如果端口被识别，则连接到它的鼠标也应被识别。请注意，假设总线鼠标在 IRQ 5 上运行，而 PS/2 鼠标设备假设在 IRQ 12 上运行。任何变化都可能需要在内核源代码中进行一些调整，以使鼠标设备被识别并正常工作。

## 鼠标指针设备

| 公司 | 型号 | 模块 |
|---|---|---|
| ATI | XL | atixlmouse |
| Logitech | Busmouse | busmouse |
| Microsoft | Busmouse | msbusmouse |
| PS/2 | Compatibles | psaux |

## PC 卡支持（PCMCIA）

大多数 PC 卡都受支持。有关更多信息，请参阅 http://www.caldera.com/LDP/HOWTO/PCMCIA-HOWTO.html。

## SCSI 适配器

以下是 Caldera OpenLinux 版本 1.3 支持的 SCSI 适配器列表。

## SCSI 适配器

| 公司 | 型号 | 模块 |
|---|---|---|
| AMD | AM53C974 | AM53C974 |
|  | AM79C974 | AM53C974 |
| Adaptec | 1520 | aha152x |
|  | 1522 | aha152x |
|  | 1542(A,CP,CF,?) | aha1542 |
|  | 1740 | aha1740 |
|  | 274x/274xT | aic7xxx |
|  | 284x | aic7xxx |
|  | 2910B | aic7xxx |
|  | 2920 (PCI) | fdomain |
|  | 294x | aic7xxx |
|  | 3940 | aic7xxx |
|  | 3985 | aic7xxx |
|  | aic7770 (motherboard) | aic7xxx |
|  | aic7850 (motherboard) | aic7xxx |
|  | aic7855 (motherboard) | aic7xxx |
|  | aic7860 (7850 ultra) | aic7xxx |
|  | aic7870 (motherboard) | aic7xxx |
|  | aic7880 (motherboard) | aic7xxx |
|  | aic7895 (motherboard) | aic7xxx |
| Advansys | ABP-510 | advansys |
| Advansys | ABP-542 | advansys |
| Advansys | ABP-742 | advansys |
| Advansys | ABP-752 | advansys |
| Advansys | ABP-842 | advansys |
| Advansys | ABP-852 | advansys |
| Advansys | ABP-920 | advansys |
| Advansys | ABP-930 | advansys |
| Advansys | ABP-930U | advansys |
| Advansys | ABP-930UA | advansys |
| Advansys | ABP-940 | advansys |
| Advansys | ABP-940U | advansys |
| Advansys | ABP-940UW | advansys |
| Advansys | ABP-950 | advansys |
| Advansys | ABP-960 | advansys |
| Advansys | ABP-960U | advansys |
| Advansys | ABP-970 | advansys |
| Advansys | ABP-970U | advansys |
| Advansys | ABP-980U | advansys |
| Advansys | ABP-5140 | advansys |
| Advansys | ABP-5142 | advansys |
| Advansys | ABP-5150 | advansys |
| Always | IN2000 (ISA) | in2000 |
| BusLogic | BT-445C | BusLogic |
| BusLogic | BT-445S | BusLogic |
| BusLogic | BT-540CF | BusLogic |
| BusLogic | BT-542B | BusLogic |
| BusLogic | BT-542D | BusLogic |
| BusLogic | BT-545C | BusLogic |
| BusLogic | BT-545S | BusLogic |
| BusLogic | BT-742A | BusLogic |
| BusLogic | BT-747C | BusLogic |
| BusLogic | BT-747D | BusLogic |
| BusLogic | BT-747S | BusLogic |
| BusLogic | BT-757C | BusLogic |
| BusLogic | BT-757CD | BusLogic |
| BusLogic | BT-757D | BusLogic |
| BusLogic | BT-757S | BusLogic |
| BusLogic | BT-946C | BusLogic |
| BusLogic | BT-948 | BusLogic |





|  |  |  |
|---|---|---|
| BT-956C | BusLogic |  |
| BT-956CD | BusLogic |  |
| BT-958 | BusLogic |  |
| BT-958D | BusLogic |  |
| Flashpoint | BusLogic |  |
| Control Concepts | SCSI/IDE/SIO/PIO/FDC cards | qlogicfas |
| DPT | EATA_PIO/DASD devices | eata_pio |
|  | PM2011 | eata_dma |
|  | PM2011B/9X | eata |
|  | PM2012A | eata |
|  | PM2012B | eata |
|  | PM2021 | eata_dma |
|  | PM2021A/9X | eata |
|  | PM2022 | eata_dma |
|  | PM2022A/9X | eata |
|  | PM2024 | eata_dma |
|  | PM2041 | eata_dma |
|  | PM2042 | eata_dma |
|  | PM2044 | eata_dma |
|  | PM2122 | eata_dma |
|  | PM2122A/9X | eata |
|  | PM2124 | eata_dma |
|  | PM2144 | eata_dma |
|  | PM2322 | eata_dma |
|  | PM2322A/9X | eata |
|  | PM3021 | eata |
|  |  | eata_dma |
|  | PM3122 | eata_dma |
|  | PM3222 | eata |
|  |  | eata_dma |
|  | PM3224 | eata |
|  |  | eata_dma |
|  | PM3222W | eata |
|  | PM3224W | eata |
|  | PM3332 | eata_dma |
|  | PM3334 | eata_dma |
| DTC | 3180 | dtc |
|  | 3280 | dtc |
| Future Domain | TMC-885 | seagate |
|  | TMC-950 | seagate |
|  | TMC-1610M | fdomain |
|  | TMC-1610MER | fdomain |
| TMC-1610MEX |  | fdomain |
| TMC-1650 |  | fdomain |
| TMC-1660 |  | fdomain |
| TMC-1670 |  | fdomain |
| TMC-1680 |  | fdomain |
| TMC-3260 (PCI) |  | fdomain |
| GVP | Series II SCSI | gvp11 |
| HP | 4020i CD-R card | advansys |
| IBM | TMC-1680 based | fdomain |
| ICP vortex Computersysteme GmbH | GDT3000/3020 | gdth |
|  | GDT3000/3020 | gdth |
|  | GDT3000A/3020A/3050A | gdth |
|  | GDT3000B/3010A | gdth |
|  | GDT2000/2020 | gdth |
|  | GDT6000/6020/6050 | gdth |
|  | GDT6000B/6010 | gdth |
|  | GDT6110/6510 | gdth |
|  | GDT6120/6520 | gdth |
|  | GDT6530 | gdth |
|  | GDT6550 | gdth |
|  | GDT6117/6517 | gdth |
|  | GDT6127/6527 | gdth |
|  | GDT6537 | gdth |
|  | GDT6557/6557-ECC | gdth |
|  | GDT6115/6515 | gdth |
|  | GDT6125/6525 | gdth |
|  | GDT6535 | gdth |
|  | GDT6555/6555-ECC | gdth |
|  | GDT6117RP/GDT6517RP | gdth |
|  | GDT6127RP/GDT6527RP | gdth |
|  | GDT6537RP | gdth |
|  | GDT6557RP | gdth |
|  | GDT6111RP/GDT6511RP | gdth |
|  | GDT6121RP/GDT6521RP | gdth |
|  | GDT6117RP1/GDT6517RP1 | gdth |
|  | GDT6127RP1/GDT6527RP1 | gdth |
|  | GDT6537RP1 | gdth |
|  | GDT6557RP1 | gdth |
|  | GDT6111RP1/GDT6511RP1 | gdth |
|  | GDT6121RP1/GDT6521RP1 | gdth |
|  | GDT6117RP2/GDT6517RP2 | gdth |
|  | GDT6127RP2/GDT6527RP2 | gdth |
|  | GDT6537RP2 | gdth |
|  | GDT6557RP2 | gdth |
|  | GDT6111RP2/GDT6511RP2 | gdth |
|  | GDT6121RP2/GDT6521RP2 | gdth |
| Iomega | Jazz Jet PCI | advansys |
|  | PPA3 (parallel port Zip drive) | ppa |
| NCR | 5380 | g_NCR5380 |
|  | 53c400 (no DMA) | g_NCR5380 |
|  | 53c406a | NCR53c406a |
|  | 53c700 (chipset) | 53c7,8xx |
|  | 53c720 (chipset) | 53c7,8xx |
|  | 53c810 (chipset) | ncr53c8xx |
|  |  | 53c7,8xx |
|  | 53c810A (chipset) | ncr53c8xx |
|  | 53c815 (chipset) | ncr53c8xx |
|  | 53c820 (chipset) | ncr53c8xx |
|  |  | 53c7,8xx |
|  | 53c825 (chipset) | ncr53c8xx |
|  | 53c825A (chipset) | ncr53c8xx |
|  | 53c860 (chipset) | ncr53c8xx |
|  | 53c875 (chipset) | ncr53c8xx |
|  | 53c876 (chipset) | ncr53c8xx |
|  | 53c895 (chipset) | ncr53c8xx |
| Pro Audio | Spectrum 16 | pas16 |
|  | Studio 16 | pas16 |
| Qlogic | FastSCSI! (ISA VLB) | qlogicfas |
|  | FastSCSI! (PCMCIA-must be initialized by QL41DOS.SYS and QL40ENBL.SYS in DOS first; then reboot to Linux w/LOADLIN) | qlogicfas |
|  | IQ-PCI (no disconnect) | qlogicisp |
|  | IQ-PCI-10 | qlogicisp |
|  | IQ-PCI-D | qlogicisp |
|  | PCI-Basic | AM53C974 |
| Quantum | ISA-200S | fdomain |
|  | ISA-250MG | fdomain |
| Seagate | ST01 | seagate |
|  | ST02 | seagate |
| SIIG | i540 SpeedMaster | advansys |
| i542 SpeedMaster | advansys |
| Fast SCSI Pro PCI | advansys |
| TekRam | DC390 | tmscim |
|  | DC390 | scsi iom |
| Trantor | T128 | t128 |
|  | T128F | t128 |
|  | T130B | g_NCR5380 |
|  | T228 | t128 |
| UltraStor | 14F | u14-34f |
|  |  | ultrastor |
|  | 24F | ultrastor |
|  | 34F | u14-34f |
|  |  | ultrastor |
| Western Digital | WD7000-FASST2 | wd7000 |
|  | WD7000-ASC | wd7000 |
|  | WD7000-AX (ALPHA) | wd7000 |
|  | WD7000-MX (ALPHA) | wd7000 |
|  | WD7000-EX (ALPHA) | wd7000 |

## IDE-SCSI 设备

使用 IDE-SCSI 驱动程序时，您可以使用 Linux SCSI 驱动程序代替原生的 IDE ATAPI 驱动程序。这些驱动程序支持尚未编写原生驱动程序的 ATAPI 设备（例如 ATAPI PD-CD 驱动器）。

## 串行板

以下是 Caldera OpenLinux 1.3 版本支持的串行板列表。

## 串行板

| 公司 | 型号 | 模块 |
|---|---|---|
| Cyclades | Cyclom-Y Boards | cyclades |
| DigiBoard | PC/Xe | pcxx |
|  | PC/Xeve | pcxx |
|  | PC/Xi | pcxx |
| SDL Comm | RISCom/8 | riscom8 |
| Stallion | Brumby | istallion |
|  | EasyIO | stallion |
|  | EasyConnection 8/32 | stallion |
|  | EasyConnection 8/64 | istallion |
|  | ONboard | istallion |
|  | Stallion | istallion |

## 磁带驱动器

大多数 QIC-40、QIC-80 和 QIC-117 软盘式磁带驱动器都应由 ftape 驱动程序支持。以下是在 ftape 源代码中按名称提及的驱动器列表。与 SCSI 或以太网卡不同，没有单独的、按驱动器划分的驱动程序；所有驱动器都在同一个驱动程序下覆盖。

## 磁带驱动器

| 公司 | 型号 | 模块 |
|---|---|---|
| AIWA | CT-803 | ftape |
| Archive | 31250Q (Escom) | ftape |
|  | 5580i | ftape |
|  | S.Hornet (Ident./Escom) | ftape |
|  | XL9250i (Conner/Escom) | ftape |
| CMS | 11c3 | ftape |
|  | 11c5 | ftape |
| Colorado | 700 | ftape |
|  | 1400 | ftape |
|  | DJ-10 | ftape |
|  | DJ-20 | ftape |
|  | T1000(HP) | ftape |
| Conner | C250MQ | ftape |
|  | C250MQT | ftape |
|  | TSM420R | ftape |
|  | TSM850R | ftape |
|  | TSM1700R | ftape |
|  | TST800R | ftape |
|  | TST3200R | ftape |
| COREtape | QIC80 | ftape |
| Exabyte | EXB-1500 | ftape |
| Iomega | 250 | ftape |
|  | 700 | ftape |
|  | 3200 | ftape |
|  | Ditto 800 | ftape |
| Insight | 80mb | ftape |
| Irwin | 80SX | ftape |
| Jumbo | 700 | ftape |
| Mountain | FS8000 | ftape |
| Reveal | TB1400 | ftape |
| Summit | SE 150 | ftape |
|  | SE 250 | ftape |
| Teac | 700 | ftape |
| Wangtek | 3040F | ftape |
|  | 3080F | ftape |
|  | 3200 | ftape |

## SCSI 和 IDE 磁带驱动器

SCSI 和 IDE 磁带驱动器没有特定的驱动程序；对它们的支持会随它们所连接的接口的驱动程序一起加载，因此使用它们不需要特殊的模块或驱动程序。如果接口正常运行（SCSI 或 IDE），则连接到它的驱动器应该可以使用。

## XFree86 v3.3.2 支持的视频卡

以下是 XFree86 3.3.2 服务器支持的视频卡列表。市场上大多数视频卡至少由 XFree86 发行版中提供的服务器包之一支持。

## XFree86 v3.3.2 支持的视频卡

| 公司 | 卡 | 服务器 |
|---|---|---|
| 2 the Max | MAXColor S3 Trio64V+ | S3 |
| 928Movie |  | S3 |
| AGX (Generic) |  | AGX |
| ALG-5434(E) |  | SVGA |
| ASUS | 3Dexplorer | SVGA |
|  | PCI-AV264CT | Mach64 |
|  | PCI-V264CT | Mach64 |
|  | VideoMagic PCI V864 | S3 |
|  | VideoMagic PCI VT64 | S3 |
| AT25 |  | SVGA |
| AT3D |  | SVGA |
| ATI | 3D Pro Turbo | Mach64 |
|  | 3D Xpression | Mach64 |
|  | 3D Xpression+ PC2TV | Mach64 |
|  | 8514 Ultra (no VGA) | Mach8 |
|  | All-in-Wonder | Mach64 |
|  | Graphics Pro Turbo | Mach64 |
|  | Graphics Pro Turbo 1600 | Mach64 |
|  | Graphics Ultra | Mach8 |
|  | Graphics Ultra Pro | Mach32 |
|  | Graphics Xpression w/ 68875 RAMDAC | Mach64 |
|  | Graphics Xpression w/ AT&T 20C408 RAMDAC | Mach64 |
|  | Graphics Xpression w/ CH8398 RAMDAC | Mach64 |
|  | Graphics Xpression w/ Mach64 CT (264 CT) | Mach64 |
|  | Graphics Xpression w/ STG1702 RAMDAC | Mach64 |
|  | Mach32 | Mach32 |
|  | Mach64 | Mach64 |
|  | Mach64 3D RAGE II, Internal RAMDAC | Mach64 |
|  | Mach64 3D RAGE II+, Internal RAMDAC | Mach64 |
|  | Mach64 CT (264 CT), Internal RAMDAC | Mach64 |
|  | Mach64 GT (264 GT), aka RAGE, Internal RAMDAC | Mach64 |
|  | Mach64 VT (264 VT), Internal RAMDAC | Mach64 |
|  | Mach64 w/ AT&T 20C408 RAMDAC | Mach64 |
|  | Mach64 w/ CH8398 RAMDAC | Mach64 |
|  | Mach64 w/ IBM RGB514 RAMDAC | Mach64 |
|  | Ultra Plus | Mach32 |
|  | Video Xpression | Mach64 |
|  | Win Boost w/ AT&T 20C408 RAMDAC | Mach64 |
|  | Win Boost w/ CH8398 RAMDAC | Mach64 |
|  | Win Boost w/ Mach64 CT (264CT) | Mach64 |
|  | Win Boost w/ STG1702 RAMDAC | Mach64 |
|  | Win Turbo | Mach64 |
|  | Wonder SVGA | SVGA |
|  | Xpert@Play PCI and AGP, 3D RAGE Pro | Mach64 |
|  | Xpert@Work 3D RAGE Pro | Mach64 |
| ATtrend | ATC-2165A | SVGA |
| Actix | GE32+ 2MB | S3 |
|  | GE32i | S3 |
|  | GE64 | S3 |
|  | ProStar | SVGA |
|  | ProStar 64 | SVGA |



| 制造商 | 型号 | 兼容性 |
|---|---|---|
|  | Ultra | S3 |
| Acumos | AVGA3 | SVGA |
| Alliance | ProMotion 6422 | SVGA |
| Ark Logic | ARK1000PV (通用) | SVGA |
|  | ARK1000VL (通用) | SVGA |
|  | ARK2000MT (通用) | SVGA |
|  | ARK2000PV (通用) | SVGA |
| Avance Logic | 2101 | SVGA |
|  | 2228 | SVGA |
|  | 2301 | SVGA |
|  | 2302 | SVGA |
|  | 2308 | SVGA |
|  | 2401 | SVGA |
| Binar Graphics | AnyView | SVGA |
| Boca | Vortex (Sierra RAMDAC) | AGX |
| California Graphics | SunTracer 6000 | SVGA |
| Canopus Co. | PowerWindow 3DV | SVGA |
|  | Total-3D (未完全支持) | VGA16 |
| Cardex | Challenger (Pro) | SVGA |
|  | Cobra | SVGA |
|  | Trio64 | S3 |
|  | Trio64Pro | S3 |
| Chips & Technologies | CT64200 | SVGA |
|  | CT64300 | SVGA |
|  | CT65520 | SVGA |
|  | CT65525 | SVGA |
|  | CT65530 | SVGA |
|  | CT65535 | SVGA |
|  | CT65540 | SVGA |
|  | CT65545 | SVGA |
|  | CT65546 | SVGA |
|  | CT65548 | SVGA |
|  | CT65550 | SVGA |
|  | CT65554 | SVGA |
|  | CT65555 | SVGA |
|  | CT68554 | SVGA |
| Cirrus Logic | GD542x | SVGA |
|  | GD543x | SVGA |
|  | GD544x | SVGA |
|  | GD5462 | SVGA |
|  | GD5464 | SVGA |
|  | GD62xx (笔记本) | SVGA |
|  | GD64xx (笔记本) | SVGA |
|  | GD754x (笔记本) | SVGA |
| Colorgraphic | Dual Lightning | SVGA |
| Compaq | Armada 7380DMT | S3 |
| Compaq | Armada 7730MT | S3 |
| Creative Labs | 3D Blaster PCI (Verite 1000)(未完全支持) | VGA16 |
| Creative Labs | Graphics Blaster 3D | SVGA |
| Creative Labs | Graphics Blaster MA201 | SVGA |
| Creative Labs | Graphics Blaster MA202 | SVGA |
| Creative Labs | Graphics Blaster MA302 | SVGA |
| Creative Labs | Graphics Blaster MA334 | SVGA |
| DFI-WG1000 |  | SVGA |
| DFI-WG5000 |  | SVGA |
| DFI-WG6000 |  | SVGA |
| DSV3325 |  | SVGA |
| DSV3326 |  | S3 |
| DataExpert | DSV3325 | SVGA |
| DataExpert | DSV3365 | S3 |
| Dell | S3 805 | S3 |
| Dell | onboard ET4000 | SVGA |
| Diamond | Edge 3D | SVGA |
| Diamond | Stealth 3D 2000 | SVGA |
| Diamond | Stealth 3D 2000 Pro | SVGA |
| Diamond | Stealth 3D 3000 | SVGA |
| Diamond | Speedstar (Plus) | SVGA |
| Diamond | Speedstar 24 | SVGA |
| Diamond | Speedstar 24X (未完全支持) | SVGA |
| Diamond | Speedstar 64 | SVGA |
| Diamond | Speedstar HiColor | SVGA |
| Diamond | Speedstar Pro (not SE) | SVGA |
| Diamond | Speedstar Pro 1100 | SVGA |
| Diamond | Speedstar Pro SE (CL-GD5430/5434) | SVGA |
| Diamond | Speedstar 64 Graphics 2000/2200 | SVGA |
| Diamond | Stealth 24 | S3 |
| Diamond | Stealth 32 | SVGA |
| Diamond | Stealth 64 DRAM SE | S3 |
| Diamond | Stealth 64 DRAM w/ S3 SDAC | S3 |
| Diamond | Stealth 64 DRAM w/ S3 Trio64 | S3 |
| Diamond | Stealth 64 VRAM | S3 |

| 设备 | 兼容性 |
|---|---|
| Stealth 64 Video VRAM (TI RAMDAC) | S3 |
| Stealth Pro | S3 |
| Stealth VRAM | S3 |
| Stealth Video 2500 | SVGA |
| Stealth Video DRAM | S3 |
| Stealth 64 Graphics 2001 series | SVGA |
| Stealth 64 Graphics 2xx0 series (864 + SDAC) | S3 |
| Stealth 64 Graphics 2xx0 series (Trio64) | S3 |
| Stealth 64 Video 2001 series (2121/2201) | S3 |
| Stealth 64 Video 2120/2200 | S3 |
| Stealth 64 3200 | S3 |
| Stealth 64 Video 3240/3400 (IBM RAMDAC) | S3 |
| Stealth 64 Video 3240/3400 (TI RAMDAC) | S3 |
| Viper 330 | SVGA |
| Viper PCI 2MB | P9000 |
| Viper VLB 2MB | P9000 |
| EIZO (VRAM) | AGX |
| ELSA |  |
| Gloria-4 | S3 |
| Gloria-8 | S3 |
| Victory ERAZOR | SVGA |
| Victory 3D | SVGA |
| Victory 3DX | SVGA |
| Winner 1000/T2D | S3 |
| Winner 1000AVI (AT&T 20C409 version) | S3 |
| Winner 1000AVI (SDAC version) | S3 |
| Winner 1000ISA | S3 |
| Winner 1000Pro w/ S3 SDAC | S3 |
| Winner 1000Pro w/ STG1700 or AT&T RAMDAC | S3 |
| Winner 1000Pro/X | S3 |
| Winner 1000TRIO | S3 |
| Winner 1000TRIO/V | S3 |
| Winner 1000TwinBus | S3 |
| Winner 1000VL | S3 |
| Winner 2000 | S3 |
| Winner 2000AVI | S3 |
| Winner 2000AVI/3D | SVGA |
| Winner 2000PRO-2 | S3 |
| Winner 2000PRO-4 | S3 |
| Winner 2000PRO/X-2 | S3 |
| Winner 2000PRO/X-4 | S3 |
| Winner 2000PRO/X-8 | S3 |
| Winner 3000 | SVGA |
| Winner 3000-L-42 | SVGA |
| Winner 3000-M-22 | SVGA |
| Winner 3000-S | SVGA |
| ET3000 | (通用) | SVGA |
| ET4000 | (通用) | SVGA |
| ET4000/W32i, W32p | (通用) | SVGA |
| ET4000/W32 |  | W32 |
| ET6000 | (通用) | SVGA |
| ET6100 | (通用) | SVGA |
| ExpertColor | DSV3325 | SVGA |
|  | DSV3365 | S3 |
| Generic VGA |  | VGA16 |
| Compatible |  |  |
| Genoa | 5400 | SVGA |
|  | 8500VL (-28) | SVGA |
|  | 8900 Phantom 32i | W32 |
|  | Phantom 64i w/ S3 SDAC | S3 |
|  | VideoBlitz III AV | S3 |
| Hercules | Dynamite | W32 |
|  | Dynamite 128/Video | SVGA |
|  | Dynamite Power | SVGA |
|  | Dynamite Pro | SVGA |
|  | Graphite HG210 | AGX |
|  | Graphite Power | AGX |
|  | Graphite Pro | AGX |
|  | Graphite Terminator 64 | S3 |
|  | Graphite Terminator 64/DRAM | S3 |
|  | Graphite Terminator Pro 64 | S3 |
|  | Stingray | SVGA |
|  | Stingray 64/V w/ ICS5342 | SVGA |
|  | Stingray 64/V w/ ZoomDAC | SVGA |
|  | Stingray Pro | SVGA |
|  | Stingray Pro/V | SVGA |
|  | Terminator 3D/DX | SVGA |
|  | Terminator 64/3D | SVGA |
|  | Terminator 64/Video | S3 |

| 制造商 | 型号 | 类型 |
|---|---|---|
| Integral | Flashpoint | SVGA |
| Intel | 5430 | SVGA |
| Interay | PMC Viper | SVGA |
| JAX | 8241 | S3 |
| Jaton | Video 58P | SVGA |
|  | Video 70P | SVGA |
| Jazz Multimedia | G-Force 128 | SVGA |
| LeadTek | WinFast 3D S600 | SVGA |
|  | WinFast 3D S680 | SVGA |
|  | WinFast S200 | SVGA |
|  | WinFast S430 | S3 |
|  | WinFast S510 | S3 |
| MELCO | WGP-VG4S | S3 |
|  | WGP-VX8 | S3 |
| Matrox | Comet | SVGA |
|  | Marvel II | SVGA |
|  | Millennium (MGA) | SVGA |
|  | Millennium II | SVGA |
|  | Millennium II AGP | SVGA |
|  | Mystique | SVGA |
| MediaVision | Proaxcel 128 | SVGA |
| Mirage | Z-128 | SVGA |
| Miro | Crystal 10SD w/ GenDAC | S3 |
|  | Crystal 12SD | S3 |
|  | Crystal 16S | S3 |
|  | Crystal 20SD PCI w/ S3 SDAC | S3 |
|  | Crystal 20SD VLB w/ S3 SDAC (BIOS 3.xx) | S3 |
|  | Crystal 20SD w/ ICD2061A (BIOS 2.xx) | S3 |
|  | Crystal 20SD w/ ICS2494 (BIOS 1.xx) | S3 |
|  | Crystal 20SV | S3 |
|  | Crystal 22SD | S3 |
|  | Crystal 40SV | S3 |
|  | Crystal 80SV | S3 |
|  | Crystal 8S | S3 |
|  | MiroVideo 20TD | SVGA |
|  | Video 20SV | S3 |
|  | MiroMedia 3D | SVGA |
| NeoMagic | (未完全支持) | VGA16 |
|  |  | (笔记本/便携式) |
| Number Nine | FX Motion 331 | S3 |
|  | FX Motion 332 | SVGA |
|  | FX Motion 531 | S3 |
|  | FX Motion 771 | S3 |
|  | FX Vision 330 | S3 |
|  | GXE Level 10/11/12 | S3 |
|  | GXE Level 14/16 | S3 |
|  | GXE64 | S3 |
|  | GXE64 Pro | S3 |
|  | GXE64 w/ S3 Trio64 | S3 |
|  | Imagine I-128 (2-8MB) | I128 |
|  | Imagine I-128 Series 2 (2-4MB) | I128 |
|  | Visual 9FX Reality 332 | SVGA |
| Oak (通用) |  | SVGA |
| Ocean (octek) | VL-VGA-1000 | SVGA |
| Orchid | Celsius (AT&T RAMDAC) | AGX |
|  | Celsius (Sierra RAMDAC) | AGX |
|  | Fahrenheit 1280 | S3 |
|  | Fahrenheit VA | S3 |
|  | Fahrenheit 1280+ | S3 |
|  | Fahrenheit Video 3D | SVGA |
|  | Kelvin 64 | SVGA |
|  | Kelvin 64 VLB Rev. A | SVGA |
|  | Kelvin 64 VLB Rev. B | SVGA |
|  | P9000 VLB | P9000 |
| Paradise | Accelerator Value | SVGA |
| Paradise/WD | 90CXX | SVGA |
| Rendition | Verite 1000 (未完全支持) | VGA16 |
| RIVA128 |  | SVGA |
| S3 | 801/805 (通用) | S3 |
|  | 801/805 w/ ATT20C490 RAMDAC | S3 |
|  | 801/805 w/ ATT20C490 RAMDAC and ICD2061A | S3 |
|  | 801/805 w/ Chr ontel 8391 | S3 |
|  | 801/805 w/S3 GenDAC | S3 |
|  | 801/805 w/ SC1148{2,3,4} RAMDAC | S3 |
|  | 801/805 w/ SC1148{5,7,9} RAMDAC | S3 |
|  | 864 (通用) | S3 |
|  | 864 w/ ATT20C498 or 21C498 | S3 |
|  | 864 w/ SDAC (86C716) | S3 |
|  | 864 w/ STG1703 | S3 |
|  | 868 (通用) | S3 |
|  | 868 w/ ATT20C409 | S3 |
|  | 868 w/ ATT20C498 or 21C498 | S3 |
|  | 868 w/ SDAC (86C716) | S3 |
|  | 86C260 (通用) | SVGA |
|  | 86C325 (通用) | SVGA |
|  | 86C357 (通用) | SVGA |
|  | 86C375 (通用) | SVGA |
|  | 86C385 (通用) | SVGA |
|  | 86C764 (通用) | S3 |
|  | 86C765 (通用) | S3 |
|  | 86C775 (通用) | S3 |
|  | 86C785 (通用) | S3 |
|  | 86C801 (通用) | S3 |
|  | 86C805 (通用) | S3 |
|  | 86C864 (通用) | S3 |
|  | 86C868 (通用) | S3 |
|  | 86C911 (通用) | S3 |
|  | 86C924 (通用) | S3 |
|  | 86C928 (通用) | S3 |
|  | 86C964 (通用) | S3 |
|  | 86C968 (通用) | S3 |
|  | 86C988 (通用) | SVGA |
|  | 86CM65 | S3 |
|  | 911/924 (通用) | S3 |
|  | 924 w/ SC1148 DAC | S3 |
|  | 928 (通用) | S3 |
|  | 964 (通用) | S3 |
|  | 968 (通用) | S3 |
|  | Aurora64V+ (通用) | S3 |
|  | Trio32 (通用) | S3 |
|  | Trio64 (通用) | S3 |
|  | Trio64+ (通用) | S3 |
|  | Trio64V2 (通用) | S3 |





| 制造商 | 型号 | 兼容性 |
|---|---|---|
|  | Trio64V2/DX (Generic) | S3 |
|  | Trio64V2/GX (Generic) | S3 |
|  | ViRGE | S3V |
|  | ViRGE (Generic) | SVGA |
|  | ViRGE/DX (Generic) | SVGA |
|  | ViRGE/GX (Generic) | SVGA |
|  | ViRGE/GX2 (Generic) | SVGA |
|  | ViRGE/VX (Generic) | SVGA |
|  | Vision864 (Generic) | S3 |
|  | Vision868 (Generic) | S3 |
|  | Vision964 (Generic) | S3 |
|  | Vision968 (Generic) | S3 |
| SNI | PC5H W32 | SVGA |
|  | Scenic W32 | SVGA |
| SPEA | Mercury 64 | S3 |
|  | Mirage | S3 |
| SPEA/V7 | Mercury | S3 |
|  | Mirage P64 | S3 |
|  | Mirage P64 w/ S3 Trio64 | S3 |
|  | Mirage VEGA Plus | SVGA |
|  | ShowTime Plus | SVGA |
| STB | Horizon | SVGA |
|  | Horizon Video | SVGA |
|  | LightSpeed | SVGA |
|  | LightSpeed 128 | SVGA |
|  | MVP-2 | SVGA |
|  | MVP-2 PCI | SVGA |
|  | MVP-2X | SVGA |
|  | MVP-4 PCI | SVGA |
|  | MVP-4X | SVGA |
|  | Nitro (64) | SVGA |
|  | Nitro 3D | SVGA |
|  | Nitro 64 Video | SVGA |
|  | Pegasus | S3 |
|  | Powergraph 64 | S3 |
|  | Powergraph 64 Video | S3 |
|  | Powergraph X-24 | S3 |
|  | Powergraph 3D | SVGA |
|  | Velocity 3D | SVGA |
|  | Velocity 64 Video | S3 |
|  | Velocity 128 | SVGA |
| SiS | SG86C201 | SVGA |

| 制造商 | 型号 | 兼容性 |
|---|---|---|
| Sierra | Screaming 3D (not fully supported) | VGA16 |
| Sigma | Concorde | W32 |
| Sigma | Legend | SVGA |
| Spider | Black Widow | AGX |
| Spider | Black Widow Plus | AGX |
| Spider | Tarantula 64 | S3 |
| Spider | VLB Plus | SVGA |
| TechWorks | Thunderbolt | W32 |
| TechWorks | Ultimate 3D | SVGA |
| Toshiba | Tecra 540CDT | SVGA |
| Toshiba | Tecra 550CDT | SVGA |
| Toshiba | Tecra 750CDT | SVGA |
| Toshiba | Tecra 750DVD | SVGA |
| Trident | 8900/9000 (Generic) | SVGA |
| Trident | 8900D (Generic) | SVGA |
| Trident | Cyber9382 (Generic) | SVGA |
| Trident | Cyber9385 (Generic) | SVGA |
| Trident | Cyber9388 (Generic) | SVGA |
| Trident | Cyber9397 (Generic) | SVGA |
| Trident | TGUI9400CXi (Generic) | SVGA |
| Trident | TGUI9420DGi | SVGA |
| Trident | TGUI9430DGi | SVGA |
| Trident | TGUI9440 (Generic) | SVGA |
| Trident | TGUI9660 (Generic) | SVGA |
| Trident | TGUI9680 (Generic) | SVGA |
| Trident | TGUI9682 (Generic) | SVGA |
| Trident | TGUI9685 (Generic) | SVGA |
| Trident | TVGA9200CXR (Generic) | SVGA |
| Unsupported VGA compatible |  | VGA16 |
| V1720 |  | SVGA |
| VL-41 |  | S3 |
| VidTech | FastMax P20 | S3 |
| VideoLogic | GrafixStar 300 | S3 |
| VideoLogic | GrafixStar 400 | S3 |
| VideoLogic | GrafixStar 500 | S3 |
| VideoLogic | GrafixStar 550 | SVGA |
| VideoLogic | GrafixStar 600 | SVGA |
| VideoLogic | GrafixStar 700 | S3 |
| ViewTop PCI |  | SVGA |
| WD | 90C24 (Laptop) | SVGA |

90C24A or 90C24A2 (Laptop) | SVGA
XGA-1 (ISA bus) | AGX
XGA-2 (ISA bus) | AGX

有关 XFree86 支持的硬件的信息是从随 XFree86 v 3.3.1 提供的 XF86Setup 配置实用程序中提取的。

有关更多信息，请参阅 http://www.xfree86.org/ 上的主要 XFree86 网页。

## 兼容的 XT 硬盘

以下是 Caldera OpenLinux 1.3 版本支持的 XT 硬盘列表。

## 兼容的 XT 硬盘

| 公司 | 型号 | 模块 |
|---|---|---|
| DTC | 5150CX | xd |
|  | 5150X | xd |
| OMTI | 5520 | xd |
| Seagate | ST11M/R | xd |
|  | ST11R | xd |
| Western Digital | WD1002-27X | xd |
|  | WD1002AWX1 | xd |
|  | WD1004A27X | xd |
|  | WDXT-GEN2 | xd |
| XEBEC |  | xd |

## 声音卡

以下内容并非详尽无遗，但列出了一些已知在 Caldera OpenLinux Release 1.3 中开箱即用无法工作的硬件。其中一些可能在使用其他厂商提供的额外软件或内核补丁后可以工作。列表如下：

- Microchannel-based PCs
- Parallel Port Tape Drives
- Xircom Ethernet Cards
- “WinModems” (modems made specifically for Windows systems)
- “WinPrinters” (printers made specifically for Windows systems, like the Lexmark 2070 printer)

## 目录

Products | Contact Us | About Us | Privacy | Ad Info | Home

使用本网站须遵守特定条款和条件。Copyright © 1996-2000 EarthWeb Inc.
保留所有权利。未经 EarthWeb 明确书面许可，禁止以任何形式或媒介全部或部分复制。

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## 索引

## 符号

- & (ampersand), running jobs in background, 161
- [ ] (brackets) metacharacter, 160
- /etc/group database, 208
- /etc/passwd file, 208
- ! (exclamation mark) metacharacter, 160
- ? (question mark) metacharacter, 160
- * (star) metacharacter, 159
- /usr/doc directory and online documentation, 168-169

## A

- absolute paths, shells, 124-125
- access
  - CD-ROM and floppy, configuration file for, 71-72
  - kdelnk files, 73, 75
  - superuser KFM sessions, 70
  - controlling for Web pages, 272-273
- access levels. See permissions mechanism
- accessibility of shells, 116

accessing
  accounts
    creating after installing Linux, 303
    disabling, 261
    permissions mechanism, 178
    root, 131, 177
  CD-ROM, 76
  computers through networks, 199
  email, 97-98
  files, 30
  FTP (File Transfer Protocol) sites, 96-97
  networks, 79
  overlapping windows, 26
  virtual consoles, 118
  Web, 93-95
activating
  buttons, 14
  filename expansion with Tab, 126
  windows, 25
Active Desktop Borders feature and virtual desktops, 45
active windows, 25, 42
Add Bookmark command (Bookmarks menu), 37
adding
  groups, 212
  users, 174-175, 209-210
adduser tool, 209
ampersand (&), running jobs in background, 161
Apache Web server, configuring, 271-272
Application Launcher, adding applications to, 105
  kdelnk file, creating, 106-108
  kdelnk file, using, 108
Application Starter command (K menu), 40
applications
  description of, 13, 40
  downgrading, 237
  exiting, 50
  graphical font ends, 240
  help system, kdehelp viewer, 49
  hiding, 42
  installing, 235-236

kvt, using, 117
multiple, working with, 41
non-RPM packages
    overview of, 240
    tar files, extracting files from, 241
    UNIX compressed archive files, extracting files from, 241-242
    Windows compressed archive files, extracting files from, 242
querying database, 237-239
restoring using Auto-restore feature, 48
starting, 40-41, 48
switching between, 42
uninstalling, 237
upgrading, 237
verifying system, 240
virtual desktops
    changing number of, 47
    configuring with Active Desktop Borders feature, 45
    customizing, 47
    Desktop Pager, 45
    sending application to other desktop, 44
    sharing applications across, 44
    switching between, 43
apropos command, 165
arrow keys, changing slider settings, 18
Auto-restore feature, starting applications with, 48
Autostart directory, starting applications automatically with, 48

## B

Back button (KFM toolbar), 32
Backspace key, testing for proper configuration, 142
backups
    dump command, 227-229
    extracting, files backed up with dump, 230-232
    files, selecting for, 220-221
    graphical programs, 232
    media for
        cartridge tapes, 218, 220
        CD-ROMs, 219
        digital audio tapes, 219

disks, 217
Iomega Jaz and Zip drives, 219
magnetic tapes, 219
travan tapes, 218
overview of, 215-216
programs for, 216
simple backups, 221
strategies for, 226
tar utility
extracting files from, 222-223
extracting from devices, 225
extracting into devices, 223
extracting into floppy devices, 223
extracting into tape devices, 224
making tar files, 221-222
spanning multiple disks or tapes, 225-226
bash, default shell, 119
bash (Bourne Again shell), 117
Bourne Again shell, 117
Bourne shell, 116
brackets ([ ]) metacharacter, 160
browser window, features of, 94-95
BRU2000 (graphical backup program), 232
building
kernels, 278-279
locate database, 193
whatis database, 166
buttons
check box type, 15
radio type, 15
slider type, 16




## C

+   - 标签类型，16
+   - 用法，14
+   - C shell，117
+   - cal 命令，189-190
+   - 计算磁带驱动器容量，228
+   - Caldera 网站
+     - OpenLinux，311
+     - PC Card 支持，321
+     - 声音卡兼容性，342
+   - 日历，打印，189-190
+   - 盒式磁带和备份，218，220
+   - 大小写敏感，119
+   - cat 命令，137-138，198
+   - cd 命令，123
+   - CD-ROM
+     - 访问，76
+     - 配置系统以允许用户访问，71-72
+       - kdelnk 文件，73，75
+       - 超级用户 KFM 会话，70
+   - CD-ROM 驱动器
+     - 并行端口，由 Caldera OpenLinux Release 1.3 支持，313
+     - 由 Caldera OpenLinux Release 1.3 支持，311-312，320
+   - 更改
+     - 目录，123
+     - 文件和文件夹的用户组，67
+     - 组，177
+     - 登录名，211
+     - 密码，186
+     - 权限，178，180
+     - 个人信息，187
+     - 次要组成员身份，211
+     - shell，186
+   - 聊天脚本，87
+   - 复选框，15
+   - chfn 命令，187
+   - chmod 命令，178，180
+   - 选择列表，操作，17
+   - chsh 命令，186

点击鼠标，14
剪贴板，58
时钟，安装 Linux 时配置，302
关闭按钮，25
关闭窗口，28
文件类型的颜色显示，122-123
命令别名，查看，130
命令组
  描述，152
  重定向和，156
命令行
  程序，语法，119
  shell，116
  UNIX 命令提示符，116
  使用命令行操作 Linux，115
命令乘数，vim，146
命令
  apropos，165
  书签菜单，添加书签，37
  内置信息，167
  cal，189-190
  cat，137-138，198
  cd，123
  chfn，187
  chmod，178，180
  chsh，186
  cp，132
  date，188-189
  dump，227-229
  编辑菜单
    复制，57
    剪切，58
    粘贴，58
  文件菜单
    打开，53-54
    另存为，57
    保存与另存为的区别，55
  find，191-192
  fmt，197
  gpasswd，212

+   grep，194-195
+   groupadd，212
+   head，139
+   历史列表，160
+   id，176
+   info，170-171
+   K 菜单，40
+   less，138
+   ln，136
+   locate，193-194
+   注销，126
+   ls，120-123
+   man，164-166
+   菜单，使用，16-17
+   mkdir，130
+   mt，224-225
+   mv，133
+   passwd，186
+   pwd，120
+   restore，230-232
+   rm，130
+   rm -R，131
+   rmdir，131
+   setfont，199
+   shutdown，127
+   sort，196
+   split，198
+   字符串一系列命令，151-152
+   stty 程序，142
+   su，176
+   tail，139
+   tar
+     从设备提取，225
+     提取到设备，223
+     提取到软盘设备，223
+     提取到磁带设备，224
+     简单备份和，221-223
+     跨多个磁盘或磁带，225-226
+   telnet，199
+   touch，129-130

umask，181-182
updatedb，193
userdel，211-212
usermod，210-211
视图菜单
  长视图，35-36
  显示树，35
whatis，166
whereis，167
who 和 w，187
编译内核，281，283
撰写电子邮件消息，100
压缩文件
  从中提取文件，241-242
  读取，169
计算机
  重启，127
  重新启动，19
  关闭，127
  关机，19
磁盘配置文件
  启用普通用户访问，71-73
  kdelnk 文件，73，75
  超级用户 KFM 会话，70
配置
  控制台，199
  内核，工具，280-281
  终端，stty 程序，142
连接网络，79
  调试连接，89
  拨号配置，添加，83，85-87
  kppp，使用，80，83
  本地网络，使用，90-91
  调制解调器设备，配置，88-89
  点对点协议 PPP，使用，80
控制台
  配置，199
  退出，126
  图形，117
  登录，118

从控制台重启计算机，126
虚拟，访问，118
上下文相关菜单，KFM，63-64
窗口控件，24-25
复制
目录，132
文件，60，132
文本，57-58
计数行、词和字符，195
cp 命令，132
csh（C shell），117
光标，类型，13
自定义
KDE
应用程序，添加到面板或从面板移除，109
应用程序，添加到面板或应用程序启动器，105-108
控制中心设置和，110
选项，109
内核，277-278
打开面板，54
虚拟桌面，47
剪切命令（编辑菜单），58
D
守护进程服务，配置，304
数据备份
BRU2000（图形程序），232
盒式磁带，218，220
CD-ROM，219
数字音频磁带，219
磁盘，217
从 dump 备份中提取文件，230-232
文件，选择，220-221
图形程序，232
Iomega Jaz 和 Zip 驱动器，219
磁带，219
概述，215-216
程序，216
简单备份，221
策略，226-229

tar 实用程序，221-226
Travan 磁带，218
日期和时间，查看和设置，188-189
date 命令，选项，188-189
使用 kppp 调试连接，89
默认文件模式，181-182
默认值
  shell 选项，使其成为默认值，123
  shell，119
分区前先对磁盘进行碎片整理，294
删除
  目录，131
  文件，62，130-131
  文件夹，62
  用户，211-212
桌面分页器和虚拟桌面，45
桌面，10-12
设备图标，配置，74
设备
  从中提取文件，225
  提取文件到，223
  IDE-SCSI，327
  鼠标指向，321
  跨多个，225-226
对话框窗口，23
对话框，显示设置，47
使用 kppp 添加拨号配置
  DNS 服务器，85-86
  网关，配置，86
  IP 设置，83，85
  登录脚本，使用，87
数字音频磁带（4mm）和备份，219
目录
  /usr/doc，168-169
  更改，123
  复制，132
  创建，130
  删除，131
  远程列出，122
  移动，133

打开，33
选择备份，220-221
禁用账户，261
磁盘空闲 df 命令，使用监控磁盘，259
磁盘空间，安装 Linux 的要求，293
磁盘使用 du 程序，使用监控磁盘，258-259
磁盘
CD-ROM，访问，76
配置文件
kdelnk 文件，73，75
超级用户 KFM 会话，70
配置文件，71-73
复制文件到或从软盘，76
监控，258-259
已挂载与未挂载，69
打开和保存文件到软盘，76
准备新软盘，77
网络内共享，273-275
显示设置对话框，47
显示信息，175
DNS 设置，配置，85-86
Linux 文档，164
文档，导航，145
双击鼠标，14
降级应用程序，237
从 FTP 站点下载文件，267-268
拖拽鼠标，14
驱动程序，安装内核时使活动，286
Caldera OpenLinux Release 1.3 支持的驱动器
CD-ROM，311-312
CD-ROM IDE，320
CD-ROM 并行端口，313
IDE，320
笔记本软盘，319
磁带，328-329
XT 硬盘，341
dump 命令
示例，229
语法，227
磁带容量，228

dump 实用程序，226

E

编辑菜单命令
复制，57
剪切，58
粘贴，58
编辑
文件，144-145
文本，57
Emacs。另见 XEmacs
模式，148
概述，142
电子邮件
访问，97-98
撰写消息，100
阅读，99
清空回收站 KFM，63
增强型 C shell，117
环境变量，125
人体工程学和 Linux，115
错误，登录，10
/etc/group 数据库，208
/etc/passwd 文件，208
Caldera OpenLinux Release 1.3 支持的以太网卡，314-318
感叹号 ！ 元字符，160
执行权限，66
退出
应用程序，50
控制台，126
vim，146
导出 NFS 卷，264
提取文件
dump 备份，230-232
从设备，225
从 tar 文件，241
从 UNIX 压缩归档文件，241-242
从 Windows 压缩归档文件，242
到设备，223-224

F

Caldera OpenLinux Release 1.3 支持的 FDDI 卡，318
fdisk，安装 Linux
  分区，创建，299
  保存分区更改，300
文件扩展名，56
文件组，37
文件列表组件，35
  文件组，37
  文件所有者，37
  文件大小，36
  最后更改，36
  权限，37
文件菜单命令
  打开，53-54
  另存为，57
  保存与另存为的区别，55
文件所有者，37
文件大小，36
文件系统，69
文件类型指示器，120
文件类型，颜色显示，122-123
文件名扩展，Tab 键激活，126
文件名，29
文件
  访问，30
  更改组，67
  复制，60，132
  创建，52，129-130，144-145
  删除，62，130-，131
  从 FTP 站点下载，267-268
  编辑，144-145
  查找，191-192，194-195
  htpassword，创建，273
  连接，198
  KDE 模板，68
  kdelnk，41
  KFM，31
  链接，61
  列出，120-122
  定位，193-194




使用上下文菜单管理，63-64
移动，133
移动到废纸篓，62
命名，29，56
打开，33-34，53-54
路径名，30
读取，137-139
重命名，64
替换，61
从废纸篓恢复，63
保存，53，55-56
选择，38
选择备份，220-221
设置权限，65-67
项目共享，182-183
网络共享，263
FTP（文件传输协议），266-270
HTTP（超文本传输协议），271-273
NFS（网络文件系统），264-266
拆分，198
tar，241
UNIX 压缩归档，241-242
上传到 FTP 站点，269
Windows 压缩归档，242
使用，51
find 命令，191-192
查找文件，191-192，194-195
运行 fips 程序，294
标志，119
从软盘设备提取文件，223
软盘
备份与，217
配置系统以允许用户访问，71-72
kdelnk 文件，73，75
超级用户 KFM 会话，70
复制文件到或从，76
为多启动系统创建，295
打开和保存文件到，76
准备新的，77
Caldera OpenLinux Release 1.3 支持的软盘驱动器，319-320

软盘光驱和备份，217
fmt 命令，197
文件夹
  更改组，67
  创建，59-60
  删除，62
  KDE 模板，68
  链接，61
  使用上下文菜单管理，63-64
  移动到废纸篓，62
  打开，33
  重命名，64
  替换，61
  从废纸篓恢复，63
  选择，38
  设置权限，65-67
强制退出，19
格式化
  文本，197
  在 Linux 和 UNIX 下，201-203
Forward 按钮（KFM 工具栏），32
Caldera OpenLinux Release 1.3 支持的帧中继卡，318
free 程序，使用监控内存，252
FTP（文件传输协议）站点
  访问，96-97
  连接到，266
  从中下载文件，267-268
  主办 FTP 服务，269-270
  msd（Microsoft System Diagnostics），290
  导航，267
  Red Hat，240
  上传文件到，269
ftp 命令，266
函数，175
G
网关，配置，86
通用网络服务配置，248
gpasswd 命令，使用管理组文件，212
图形控制台，117

图形备份程序，232

图形字体结束，240

图形用户界面（GUI）和桌面，11

grep 命令，194-195

groff 格式化程序，201-203

组，更改，67

groupadd 命令，212

组

添加，212

更改，177

管理文件，212

权限机制，182-183

GUI（图形用户界面）和桌面，11

gzip 文件，从中提取文件，241-242

## H

Caldera OpenLinux Release 1.3 支持的硬盘

IDE，320

XT，341

硬链接，135

硬件

备份，216

安装 Linux 前识别，290-291

安装 Linux 前盘点，292

安装 Linux 的最低要求，292-293

不支持，342

硬件配置区域（LISA），246

head 命令，139

Help 按钮（KFM 工具栏），33
帮助来源

/usr/doc，168-169

隐藏应用程序，42
历史列表，160
Home 按钮（KFM 工具栏），32
主目录
  移动，210
  权限机制，178
主机表配置，248
托管 FTP 服务，269-270
HOWTO 文档，169
创建 httpassword 文件，273
HTTP（超文本传输协议）
  Apache 服务器，配置，271-272
  控制访问，272-273
I
Iconify 按钮，24
图标化窗口，26
图标，13
id 命令，176
Caldera OpenLinux Release 1.3 支持的 IDE 驱动器，320
Caldera OpenLinux Release 1.3 支持的 IDE-SCSI 设备，327
安装 Linux 前识别硬件，290-291
IMAP（交互式邮件访问协议），97
inetd 程序和网络服务，270
info 系统（在线文档），170-171
inode，122
输入和输出
  互连，157-158
  重定向
    命令组，156
    STDERR 流，156
    STDOUT 流，153，155
安装源选择，安装 Linux，300
安装
  应用程序，235-236
  内核
    配置 LILO，284-285
    使驱动程序激活，286
    安装新模块，283
Linux

构建启动和模块软盘，295
谨慎自动探测，297
更改 LISA 设置，296-297
更改分区面板，299
时钟，配置，302
守护进程服务，配置，304
创建第一个账户，303
识别硬件，290-291
安装源选择，300
盘点硬件，292
Kernel Module Manager，298
语言选择，296
LILO 启动管理器，配置，303-304
硬件最低要求，292-293
鼠标类型，配置，302
多启动系统，293-294
网络设置，301-302
概述，289
创建分区，299
先前保存的配置，296
打印机，选择，302
创建根分区，300
设置 root 密码，303
保存分区更改，300
开始安装，296
步骤，290
选择 X-server，301
配置 X Windows，304-306，308-309
交互式邮件访问协议（IMAP），97
互连输入和输出，157-158
Caldera OpenLinux Release 1.3 支持的接口卡，313
Internet，84
Internet 协议（IP），84
Internet 服务提供商（ISP），80
安装 Linux 前盘点硬件，292
Iomega Jaz 和 Zip 驱动器和备份，219
IP（Internet 协议），84
配置 IP 设置，83，85
ispell 程序，149

## J-K

作业
  杀死或挂起，162
  使用 shell 同时处理多个，161-162
连接文件，198
K 桌面环境。参见 KDE
K 文件管理器。参见 KFM
K 菜单命令，Application Starter，40
KDE（K 桌面环境）
  Auto-restore 功能，48
  Autostart 目录，48
  组件，11-12，22
  自定义
    添加到或从 Panel 移除应用程序，109
    添加应用程序到 Panel 或 Application Launcher，105-108
    Control Center 设置与，110
    选项，109
  描述，9-10，12
  使用邮件访问，97
  使用 FTP（文件传输协议）站点访问，96-97
  帮助系统，49
  使用 kvt 应用程序，117
  Mini Command Line，81
  新闻阅读器，101
  虚拟桌面
    更改数量，47
    使用 Active Desktop Borders 功能配置，45
    自定义，47
    Desktop Pager，45
    发送应用程序到其他桌面，44
    跨桌面共享应用程序，44
    在之间切换，43
  使用 Web 访问，93-94
KDE 应用程序，使用，52
KDE Control Center，使用自定义选项，110
KDE 软盘格式化程序，77
KDE 模板，68
kdehelp 查看器，访问，49
kdelnk 文件，41，106-108

KEdit 文本编辑器，13
Kernel Module Manager，298
内核
  构建，原因，278-279
  编译，281，283
  配置，280-281
  自定义，277-278
  安装
    配置 LILO，284-285
    使驱动程序激活，286
    安装新模块，283
  测试，286
键盘，为 X Windows 配置，305
KFM（K 文件管理器）
  书签，创建，37
  文件列表，35
  组件，36
  文件组，37
  文件所有者，37
  文件大小，36
  最后更改，36
  权限，37
文件
  更改组，67
  复制，60
  删除，62
  链接，61
  移动到废纸篓，62
  重命名，64
  替换，61
  从废纸篓恢复，63
  选择，38
  设置权限，65-67
文件夹
  更改组，67
  创建，59-60
  删除，62
  链接，61
  移动到废纸篓，62
  重命名，64

替换，61
从废纸篓恢复，63
选择，38
设置权限，65-67
KFM 的网络感知，93
概述，31
树视图，35
URL 和，31
窗口，31
KFM 上下文菜单，63-64
KFM 工具栏按钮，32
KFM 窗口，启动，70
kill 命令，使用监控进程，257
杀死作业，162
kmail，使用邮件访问，97
knews，使用阅读邮件，101
Korn shell，117
kppp
  使用连接网络
    Configuration 窗口，80
    New Account 窗口，83
  调试连接，89
  添加拨号配置
    DNS 服务器，85-86
    配置网关，86
    IP 设置，83，85
    使用登录脚本，87
    配置调制解调器设备，88-89
ksh（Korn shell），117
使用 kvt 应用程序，117
L
安装 Linux 时语言选择，296
Caldera OpenLinux Release 1.3 支持的笔记本软盘驱动器，319
last 命令，使用监控日志文件，260
lastb 命令，使用监控日志文件，261
LDP（Linux 文档项目），169
less 命令，138
LILO（Linux Loader），安装内核时配置，284-285
LILO 启动管理器，安装 Linux 后配置，303-304




链接文件和文件夹，61
链接
  创建，136
  描述，61，94
  硬链接，135
  符号链接，134
Linux，安装。参见安装，Linux
Linux 文档项目（LDP），169
Linux 安装与系统管理。参见 LISA
Linux 新闻组，172
LISA（Linux 安装与系统管理）
  启动管理器配置区域，249
  谨慎自动探测，297
  更改安装设置，296-297
  功能
    软件包管理区域，245
    系统分析，244-245
    系统配置区域，246
  内核，使用自定义，277
  网络配置区域，247-248
  概述，243
  系统配置区域，246-247
列出
  远程目录，122
  文件，120-122
列表，操作，17
ln 命令，136
本地网络，通过本地网络连接到互联网，90-91
locate 命令，193-194
locate 数据库，构建，193
定位文件，193-194
日志文件，监控
  last 命令，260
  lastb 命令，261
登录
  控制台，使用，118
  错误，10
注销，19
登录名，更改，211
登录脚本，使用，87
logout 命令，126
Long View 命令（View 菜单），35-36
ls 命令，120
  文件类型彩色显示，122-123
  列出远程目录，122
  选项，121-122
M
磁光盘和备份，217
man 命令，164-166
管理组文件，212
匹配任意字母元字符（?），160
匹配任意内容元字符（*），159
匹配范围元字符（[ ]），160
Maximize/Restore 按钮，25
备份媒体
  盒式磁带，218，220
  CD-ROM，219
  数字音频磁带，219
  磁盘，217
  Iomega Jaz 和 Zip 驱动器，219
  九轨磁带，219
  概述，217
  travan 磁带，218
内存
  监控，252-253
  安装 Linux 的要求，293
菜单，操作，16-17
元字符。参见正则表达式
Microsoft System Diagnostics（msd），使用其识别硬件，290
鼠标中键点击，14
Mini Command Line，KDE 桌面，81
mini HOWTO 文档，169
mkdir 命令，130
模态编辑器，144
调制解调器设备，使用 kppp 配置，88-89
模式，Emacs，148
修改用户，210
模块，在安装内核时安装，283
监视器，为 X Windows 配置，306
监控
  磁盘，258-259
  日志文件，260-261
  内存，252-253
  系统概述，251
进程
  kill 命令，257
  nicing，258
  ps 命令，256
  top 程序，254-255
挂载 NFS 卷，265-266
鼠标
  操作，14，38
  为 X Windows 配置，305
  Caldera OpenLinux Release 1.3 支持的指向设备，321
  类型，在安装 Linux 时配置，302
  使用，13
移动
  文件和目录，133
  将文件和文件夹移至回收站，62
  主目录，210
  文本，57-58
  窗口，27
msd（Microsoft System Diagnostics），使用其识别硬件，290
mt 命令，回绕磁带，224-225
多启动系统，安装 Linux，293
  构建启动和模块软盘，295
  谨慎自动探测，297
  更改 LISA 设置，296-297
  更改分区表，299
  时钟，配置，302
  守护进程服务，配置，304
  创建第一个账户，303
  安装源选择，300
  Kernel Module Manager，298
  语言选择，296
  LILO 启动管理器，配置，303-304
  鼠标类型，配置，302
  网络设置，301-302
分区，创建，294，299
先前保存的配置，296
打印机，选择，302
根分区，创建，300
根密码，设置，303
保存对分区的更改，300
开始安装，296
X-server，选择，301
X Windows，配置，304-306，308-309
多个应用程序
隐藏应用程序，42
在之间切换，42
虚拟桌面
更改数量，47
使用 Active Desktop Borders 功能配置，45
自定义，47
Desktop Pager，45
将应用程序发送到其他桌面，44
在之间共享应用程序，44
在之间切换，43
操作，41
mv 命令，133

## N

命名文件，29，56
导航
文档，145
shell，使用，120
Tab 键，使用，18
否定范围元字符（!），160
Netcraft 网站，271
Netscape Collabra，为其配置系统，101，103
Netscape Messenger
撰写电子邮件消息，100
配置，98
使用其访问电子邮件，97
阅读电子邮件，99
Netscape Navigator
Linux 与，94
使用其访问网络，95
网络透明文件访问，31
网络访问配置，248
网络配置区域（LISA）247-248
网络服务，inetd 程序，270
网络设置，在安装 Linux 时配置，301-302
网络
  访问，79
  通过网络访问计算机，199
  连接
    调试连接，89
    添加拨号配置，83，85-87
    使用 kppp，80，83
    使用本地网络，90-91
    配置调制解调器设备，88-89
    使用点对点协议（PPP），80
  共享磁盘和打印机，273-275
  在网络上共享文件，263
    FTP（文件传输协议），266-270
    HTTP（超文本传输协议），271-273
    NFS（网络文件系统），264-266
  用户
    添加，209
    管理，207-208
New Account 窗口，kppp，83
newgrp 工具，177
新闻阅读器，为其配置系统，101，103
新闻组，171-172
NFS（网络文件系统）
  导出卷，264
  挂载卷，265-266
nicing，使用其监控进程，258
九轨磁带和备份，219
noclobber 变量和重定向流，154
节点，171
非 RPM 包
  概述，240
  从中提取文件
    tar 文件，241
    UNIX 压缩归档文件，241-242
    Windows 压缩归档文件，242
虚拟桌面数量，更改，47
数字，设置权限，178-180

## O

在线帮助
/usr/doc，168-169
apropos 命令，165
内置命令信息，167
GNU 的 info 系统，170-171
UNIX man 页面，164-166
USENET，171-172
whatis 命令，166
whereis 命令，167

Open 面板
自定义，54
导航，53

打开
文件，33-34，53-54，76
文件夹，33

OpenLinux 网站，311
OS，安装 Linux 并行，293-294
输出，丢弃，157

## P

数据包，84

Panel
从中添加和删除应用程序，109
添加应用程序到，105
创建 kdelnk 文件，106-108
使用 kdelnk 文件，108

桌面上的面板，11
面板窗口，23
Caldera OpenLinux Release 1.3 支持的并行端口 CD-ROM 驱动器，313
分区表，在安装 Linux 时更改，299

分区
为多启动系统创建，294
在安装 Linux 时创建
主分区，299
根分区，300
交换分区，299
在安装 Linux 时保存更改，300
passwd 命令，186
密码
  更改，186
  指南，213
  登录，10
  阴影密码，213
Paste 命令（Edit 菜单），58
PATH 环境变量，125
文件路径名，30
路径，相对和绝对，124-125
PC 卡，Caldera 网站，321
性能监控，251
权限
  描述，37
  设置
    文件和文件夹，65-67
    使用符号，179-180
  类型，66
权限机制
  账户，178
  chmod 命令，178，180
  显示信息，175
  组，182-183
  组，更改，177
  主目录，178
  id 命令，176
  概述，173
  root 账户，177
  设置权限为数字，178-180
  su 命令，176
  umask 命令，181-182
  用户，174-175
个人资料，更改，187
管道
  描述，122
  互联输入和输出，157-158
点对点协议（PPP），使用其连接到网络
  调试连接，89
  描述，85
添加拨号配置，83，85-87
添加互联网连接，80，83
配置调制解调器设备，88-89
邮局协议（POP），97
PostScript 和打印，200
PPP。参见点对点协议
按下鼠标按钮，14
打印机
  在安装 Linux 时选择，302
  在网络内共享，273-275
打印
  日历，189-190
  在 Linux 和 UNIX 下，200-201
进程，监控
  kill 命令，257
  nicing，258
  ps 命令，256
  top 程序，254-255
procinfo 程序，使用其监控内存，252-253
编程语言和 shell，117
程序，40
项目，共享文件，182-183
ps 命令，使用其监控进程，256
pwd 命令，120
Q-R
四分之一英寸盒式磁带和备份，218
查询数据库，237-239
问号（?）元字符，160
单选按钮，15
Caldera OpenLinux Release 1.3 支持的无线电调制解调器/网络卡，319
RAM 和交换，251
读权限，66
阅读
  电子邮件，99
  文件
    cat 命令，137-138
    head 命令，139
    less 命令，138




+   tail 命令，139
+   重启计算机，127
+   重新编译，使用内核自定义，278
+   Red Hat FTP 站点，240
+   重定向
+     输入和输出
+       命令组，156
+       STDERR 流，156
+       STDOUT 流，153，155
+     流，noclobber 变量，154
+   刷新按钮（KFM 工具栏），32
+   正则表达式（REGEXs）
+     方括号（[ ]），160
+     描述，159
+     感叹号（!），160
+     问号（?），160
+     星号（*），159
+   相对路径，shells，124-125
+   重命名文件和文件夹，64
+   renicing，256
+   替换文件和文件夹，61
+   安装 Linux 时硬件要求，292-293
+   调整窗口大小，27
+   分辨率，为 X Windows 选择，308
+   重启计算机，19，126
+   restore 命令，230-232
+   恢复应用程序，48
+   从回收站检索文件和文件夹，63
+   回卷磁带，224-225
+   可重写 CD-ROM 和备份，219
+   右键单击鼠标，14
+   rm -R 命令，131
+   rm 命令，130
+   rmdir 命令，131
+   root 账户
+     权限机制，177
+     使用，131
+   安装 Linux 时创建 root 分区，300
+   安装 Linux 时设置 root 密码，303
+   RPM
downgrading with，237
graphical front ends to，240
installing with，236
overview of，235
querying database，237-239
uninstalling with，237
upgrading with，237
uses of，236
verifying system，240

## S
Save As 命令（文件菜单），55，57
Save 命令（文件菜单），55
保存
文件，53，55-56，76
注销前，19
滚动条
标准应用程序窗口，23
窗口，26
Caldera OpenLinux Release 1.3 支持的 SCSI 适配器，321-326
更改二级组成员身份，211
安全
监控，251
密码，213
用户管理，207-208
选择
文件，34
文件夹，33
文本，18，57
发送应用程序到其他虚拟桌面，44
Caldera OpenLinux Release 1.3 支持的串行板，327-328
服务器，271-272
setfont 命令，199
setgid 位，181
设置权限
文件和文件夹，65-67
作为数字，178-180
使用符号，179-180
setuid 位，181
sh（Bourne shell），116

shadow 密码，213
共享
  跨虚拟桌面共享应用程序，44
  网络内共享磁盘和打印机，273-275
  为项目共享文件，182-183
  通过网络共享文件，263
    FTP（文件传输协议），266-270
    HTTP（超文本传输协议），271-273
    NFS（网络文件系统），264-266
执行 shell 命令，146
shells
  可访问性，116
  使用 Tab 激活文件名扩展，126
  大小写敏感性，119
  更改，186
  默认，119
  使选项成为默认值，123
  使用进行导航，120
  编程语言和，117
  相对和绝对路径，124-125
  类型，116
  使用进行多任务处理，161-162
快捷键
  Alt+Fn（虚拟控制台），118
  Alt+Tab（在应用程序之间切换），42
  Ctrl+Alt+Backspace（强制退出），19
  Ctrl+Alt+Delete（从控制台重启计算机），126
  Ctrl+Alt+Fn（KDE 中的虚拟控制台），118
  Ctrl+C（终止作业），162
  Ctrl+Esc（在应用程序和桌面之间切换），43
  Ctrl+Fn（查看虚拟桌面），43
  Ctrl+Tab（在虚拟桌面之间切换），43
  Ctrl+Z（挂起作业），162
Show Tree 命令（视图菜单），35
shutdown 命令，127
关闭计算机，127
简单备份，221
单用户模式启动，227
站点。参见 FTP 站点；Web 站点
滑块
更改设置，18
描述，16
智能 UNIX 命令，167
SMB（服务器消息块），273-275
套接字，122
软件包管理区域（LISA），245
sort 命令，196
排序文本行，196
Linux 的声音支持，282
拼写检查器，ispell，149
split 命令，198
分割文件，198
标准应用程序窗口，22
星号（*）元字符，159
启动
  应用程序，40-41，48
  安装，296
STDERR 流，156
STDOUT 流
  追加文件，155
  重定向到文件，153
Stick or Pin 按钮，24
sticky 位，181
备份策略，226
  dump 命令，227
    示例，229
    使用 dump 备份的提取文件，230-231
    磁带容量，228
  restore 命令，232
流
  描述，153
  STDERR，156
  STDOUT
    追加文件，155
    重定向到文件，153
串联一系列命令，151-152
stty 程序，142
su 命令，176
子 shell，152
为用户访问配置系统以进行 superuser KFM 会话，70

挂起作业，162
交换，251
切换
  在应用程序之间，42
  在桌面之间，12
  在虚拟桌面之间，43
符号链接，122，134
使用符号设置权限，179-180
命令行程序语法，119
查看谁登录到系统，187
系统分析（LISA），244-245
系统配置区域（LISA），246-247

## T
Tab 键
  使用激活文件名扩展，126
  使用进行导航，18
标签，16
tail 命令，139
磁带归档（tar）实用程序和备份
  从中提取文件，222-223
  从设备中提取，225
  提取到设备，223
  提取到软盘设备，223
  提取到磁带设备，224
  制作 tar 文件，221-222
  跨多个磁盘或磁带，225-226
磁带设备，224-225
磁带驱动器
  容量计算，228
  Caldera OpenLinux Release 1.3 支持的 SCSI 和 IDE，329
  Caldera OpenLinux Release 1.3 支持的，320，328-329
tar 文件，从中提取文件，241
Task 按钮（KFM 工具栏），33
桌面上的任务栏，12
TCP/IP（传输控制协议/互联网协议），85
tcsh（增强型 C shell），117
Telnet，103
telnet 命令，199
模板（KDE），68

终端配置，142
测试内核，286
文本
  复制，57-58
  编辑，57
  格式化，197
  移动，57-58
  选择，18，57
  排序行，196
文本编辑器
  模式化，144
  概述，141
  vim
    命令乘数，146
    导航文档，145
    执行 shell 命令，146
    退出，146
    创建和编辑文件，144-145
    访问教程，143
  XEmacs，147-149
文本字段，18
文本处理（UNIX）
  groff 格式化程序，201-203
  打印，200-201
丢弃输出，157
标题栏
  标准应用程序窗口，23
  窗口控件和，24
Caldera OpenLinux Release 1.3 支持的令牌环卡，319
工具提示，15
工具，40
top 程序，使用监控进程，254-255
touch 命令，129-130
传输控制协议/互联网协议（TCP/IP），85
Trash（KFM）
  清空，63
  移动文件或文件夹到，62
  从中检索文件或文件夹，63
旅行者磁带和备份，218
树视图，35

## U
关闭计算机，19
UDP（用户数据报协议），85
umask 命令，181-182
统一资源定位符（URLs），31
卸载应用程序，237
UNIX，使用文本处理
  groff 格式化程序，201-203
  打印，200-201
UNIX 命令提示符，116
UNIX 压缩归档文件，从中提取文件，241-242
UNIX 手册页
  访问，164-165
  Linux 下的章节，166
Up 按钮（KFM 工具栏），32
updatedb 命令，193
升级应用程序，237
上传文件到 FTP 站点，269
URLs（统一资源定位符），31
USENET
  描述，101
  在线文档来源，171-172
Usenet 网站，101
配置系统以允许用户访问 CD-ROM 和软盘，71-72
  kdelnk 文件，73，75
  superuser KFM 会话，70
用户数据报协议（UDP），85
用户私有组（UPGs），权限和，183
useradd 工具，210
userdel 命令，211-212
usermod 命令，210-211
用户
  添加，174-175，209-210
  删除，211-212
  功能，175
  管理，207-208
  修改，210
  角色，174
/usr/doc 目录和在线文档，168-169

实用程序
  dump，226
  字数统计（wc），195

## V
变量
  环境（PATH），125
  noclobber，154
验证系统，240
视频卡
  为 X Windows 配置，306
  XFree86 3.3.2 服务器支持的，329-341
视图菜单命令
  长视图，35-36
  显示树，35
查看
  命令别名，130
  日期和时间，188-189
  文件夹，33
  谁登录到系统，187
vim（文本编辑器）
  命令乘数，146
  导航文档，145
  执行 shell 命令，146
  退出，146
  创建和编辑文件，144-145
  概述，143
  访问教程，143
  网站，147
虚拟控制台访问，118
虚拟桌面
  更改数量，47
  使用 Active Desktop Borders 功能配置，45
  自定义，47
  Desktop Pager，45
  面板和，11
  发送应用程序到其他桌面，44
  跨虚拟桌面共享应用程序，44
  在之间切换，43
虚拟内存，252





## W

- Visual Editor (vi)，141
- w command，187
- Web，访问
  - KDE，使用，94
  - Netscape，使用，95
  - 概述，93
- Web pages，控制访问，272-273
- Web sites
  - Caldera
    - OpenLinux，311
    - PC Card Support，321
    - sound card compatibility，342
  - Linux Documentation Project (LDP)，169
  - Netcraft，271
  - Usenet，101
  - vim，147
  - XFree86，341
- whatis command，166
- whatis database，166
- whereis command，167
- who command，187
- windowed environment，21-22
- windows
  - accessing overlapping，26
  - active，25
  - categories of，22
  - closing，28
  - controls，24-25
  - dialog boxes，23
  - KFM，31
  - moving，27
  - panel，23
  - resizing，27
  - scrollbars，26
  - standard application，22
- Windows compressed archive files，提取文件，242
- word count (wc) utility，195
- write-once CD-ROMs and backups，219

## X

- X-server，安装 Linux 时选择，301
- X Windows，21-22，304-306，308-309
- xconfig options，281
- XEmacs
  - overview of，147
  - tutorial，访问，148-149
- XF86Setup program，304
  - completing configuration，309
  - keyboard，配置，305
  - monitor，配置，306
  - mouse，配置，305
  - other configurations，308
  - resolutions，选择，308
  - video card，配置，306
- XFree86 Web pages，341
- XT hard drives supported by Caldera OpenLinux Release 1.3，341

## Y-Z

- zip files，提取文件，242
- zless tool，169
- zsh (shell)，117

目录

