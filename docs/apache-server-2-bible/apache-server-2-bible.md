# Apache Server 2 圣经


# 致谢

- **收购编辑**  
  特里·瓦弗里斯
- **项目编辑**  
  詹姆斯·H·拉塞尔
- **技术编辑**  
  格雷戈里·W·斯蒂芬斯
- **文字编辑**  
  理查德·H·阿丁
- **编辑经理**  
  凯尔·卢珀  
  阿米·弗兰克·沙利文
- **副总裁及执行集团出版人**  
  理查德·斯韦德利
- **副总裁及集团出版人**  
  鲍勃·伊普桑
- **编辑总监**  
  玛丽·贝德纳雷克
- **项目协调员**  
  雷吉娜·斯奈德
- **图形与制作专员**  
  贝丝·布鲁克斯  
  梅拉妮·德贾尔丹  
  乔伊斯·豪格海  
  贝蒂·舒尔特  
  杰瑞米·翁格
- **质量控制技术员**  
  劳拉·阿尔伯特  
  约翰·格林诺  
  安迪·霍兰德贝克  
  安赫尔·佩雷斯
- **媒体开发专员**  
  特拉维斯·西尔弗斯
- **插图画家**  
  凯特·肖
- **校对与索引**  
  TechBooks 制作服务
- **封面图像**  
  凯特·肖

# 作者简介

Mohammed Kabir 是 Evoknow, Inc. 的创始人兼首席执行官。他的公司专门从事 CRM 软件开发。在忙于管理软件项目或著书立说之余，他喜欢旅行。卡比尔在加州州立萨克拉门托大学学习计算机工程。你可以通过 kabir@evoknow.com 联系到他。

谨以此书纪念我的母亲，Nazma Bather。

# 前言

欢迎来到 Apache Server 2.0。你很可能已经听说过 Apache 服务器。事实上，超过 60% 的网络管理员使用 Apache。Apache 是世界上功能最强大的开源 Web 服务器平台。

作为一名实战派 Web 开发者、研究者和管理员，我发现 Apache 是大多数 Web 站点的完美选择。Apache 2.0 是 Apache 服务器的一次重大修订。Apache 团队在第一个版本中创建了一个高度可配置的 Web 服务器，它迅速变得流行起来；在版本 2 中，Apache 团队专注于可扩展性、可靠性和性能。为了创建一个非常可扩展的 Apache 架构，进行了主要的代码修订。

如今，Apache 作为使用最广泛的 Web 平台巍然屹立。每天，越来越多的企业接受这一开源奇迹并纳入其 IT 基础设施。许多大型 IT 公司，如 IBM，都在其产品系列中采用了 Apache。Apache 的未来看起来前景广阔。无论你是 Apache 的新手，还是已经是资深的 Apache 管理员，现在是开始使用 Apache 2.0 的最佳时机。这本书将帮助你做到这一点。

# 本书的组织结构

本书分为六部分。以下是对各部分的简要描述。

## 第一部分：入门

通过对全球排名第一的 Web 服务器的简要介绍，在本部分中，我将引导你完成获取和编译 Apache 的过程。我将向你展示如何在默认配置文件最少改动的情况下让 Apache 启动并运行，以便你能尽快在系统上运行 Apache。本部分以对 Apache 核心指令和标准模块的完整参考结尾，使你能够为严肃的 Apache 管理任务做好准备。




# 第二部分：网站管理

这部分重点介绍典型的 Web 管理任务，例如虚拟 Web 站点的创建、用户认证与授权任务、监控、日志记录、URL 重写与重定向、代理服务等等。您将在此深入了解创建和管理虚拟 Web 站点的相关知识。您将掌握各种用户认证、授权及访问控制技术。您还将学习如何监控 Web 服务器，并定制日志文件以供分析。

# 第三部分：运行 Web 应用程序

这部分重点介绍如何使用 Apache 提供动态内容。涵盖通用网关接口（CGI）、服务器端包含（SSI）、FastCGI、PHP、mod_perl 以及 Java Servlet。您将快速学会如何使用 Apache 搭配这些技术。

# 第四部分：保护您的网站安全

互联网上的任何计算机都可能遭受滥用或恶意利用的企图。采取安全预防措施总是明智之举。在这一部分，您将学习如何提高网站的安全性，使其更能抵御黑客攻击。您还将了解运行 SSI 和 CGI 程序的潜在风险，以及如何采取预防措施以避免这些风险。此外，您还将学习如何使用 Apache 模块启用安全套接字层（SSL）服务，从而实现安全的电子商务。

# 第五部分：在 Windows 上运行 Apache

Windows（Win32）平台上的 Apache 已变得非常流行；越来越多的人正在尝试在 Windows 平台上使用 Apache。随着 Apache 2.0 的推出，该平台下 Apache Web 服务器的性能表现变得非常有希望。在这一部分，您将学习如何在 Win32 平台上安装和配置 Apache。

# 第六部分：针对性能和可扩展性的调优

在本部分，我将讨论如何通过调整 Web 服务器系统和优化各种 Apache 服务器配置来加速 Apache。本章提供了大量关于如何从高性能硬件中获益的信息，以及如何调整 Linux 下的硬盘和文件系统以增强系统性能。它还涵盖了 Web 缓存以及与基于 Perl 的 Web 应用程序相关的调优问题。

# 本书中使用的约定

阅读本书不需要学习任何新的约定。只需记住，当被要求输入命令时，在命令提示符下键入命令后，您需要按下 Enter 或 Return 键。等宽字体用于表示配置或代码片段。

此外，请注意这些图标：

![](img/e11fcbd2818a3495ac70085e5d8d1c26_11_0.png)

“注”图标表示某些内容需要稍作额外解释。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_11_1.png)

“提示”图标告知您一些可能为您节省时间和精力的小窍门。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_11_2.png)

“警告”图标提醒您注意潜在的 dangers。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_11_3.png)

“光盘上的内容”图标提示您查看光盘中的文件、程序及其他有用资源。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_11_4.png)

“交叉参考”图标有助于您更好地导航全书，指引您查看与当前阅读内容相关的主题。

# 告诉我们您对这本书的看法

Hungry Minds 和我都希望了解您对这本书的看法。请在 Hungry Minds 网站（www.hungryminds.com）在线注册本书，并给我们提供反馈。如果您有兴趣直接与我沟通，请发送电子邮件至 kabir@evoknow.com。我将尽力及时回复。

# 书籍网站

本书的网站位于 http://www.evoknow.com/kabir/apache2。您可以访问该网站获取最新内容、勘误表和常见问题解答（FAQ）。

# 致谢

我想感谢 Apache 小组创造了世界上最强大、可扩展且模块化的 Web 服务器。我要特别感谢 Ralf S. Engelschall。作为 `mod_rewrite` 模块的作者，Ralf 在编写关于 URL 重写规则的第 9 章时提供了大量支持。该章中的实用示例源自他个人在其网站 www.engelschall.com/pw/apache/rewriteguide 上不断扩充的合集。

我也要感谢 Hungry Minds 团队，他们使这本书成为现实。不可能列出所有参与者，但我必须提及以下几位友善的同仁：

项目发展编辑 James Russell 维持了这一项目的推进。我不知道如果没有他在整个过程中慷慨的帮助和建议，我该如何完成这本书。谢谢你，James。

获取编辑 Terri Varveris 为我提供了这本书的机会，并确保我坚持到底。谢谢你，Terri。

我的妻子 Sheila Kabir 不得不在撰写这本书的几个月中忍受我许多长时间的工作。谢谢你，亲爱的。
# 入门指南

在本部分，我将向你展示为什么 Apache 是一个出色的 Web 服务器；从哪里获取它，以及如何安装和配置它。我还会让你快速掌握 Apache 代码指令以及许多流行模块，这些模块使 Apache 成为地球上可配置性最强的 Web 服务器。

## 本部分介绍

**第1章** Apache：排名第一的 Web 服务器

**第2章** 获取和安装 Apache

**第3章** 让 Apache 跑起来

**第4章** 核心和 MPM 指令

**第5章** Apache 模块

# Apache：排名第一的 Web 服务器

**W**elcome to Apache——全球排名第一的 Web 服务器。如果你正在考虑运行 Apache，那你来对地方了！本章介绍了 Apache 运行 Web 服务器的方式。

根据一家名为 Netcraft ([www.netcraft.co.uk/Survey/](http://www.netcraft.co.uk/Survey/)) 的知名 Web 服务器调查公司统计，世界上超过 60% 的 Web 服务器使用 Apache。Netcraft 定期发布 Top Server 统计数据。表 1-1 展示了本章撰写时可用的 Top Server 统计数据。如果你想了解这些数字背后的具体情况，可以访问 [www.apache.org/info/apache_users.html](http://www.apache.org/info/apache_users.html)。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_33_0.png)

## 本章概述

- 理解为什么 Apache 如此强大
- 深入了解 Apache 历史
- 浏览功能集
- 查看 Apache 架构
- 梳理许可选项

**表 1-1**
**Netcraft 发布的 Top Server 统计数据**

| 服务器 | 2001年11月 | 百分比 | 2001年12月 | 百分比 |
| :--- | :--- | :--- | :--- | :--- |
| Apache | 7750275 | 61.88 | 8588323 | 63.34 |
| Microsoft IIS | 3307207 | 26.40 | 3609428 | 26.62 |
| iPlanet | 431935 | 3.45 | 383078 | 2.83 |
| Zeus | 174052 | 3.45 | 172352 | 1.27 |

# Apache 性能卓越

Apache 取得的成就简直令人惊叹！谁曾想到一个开源 Web 服务器能持续击败两大主要商业竞争对手——微软和网景（Netscape）？每个人对 Apache 如此流行都有自己不同的理由。以下是我的观点：

- **Apache 是一个具有模块化设计的高可配置性 Web 服务器。** 扩展 Apache Web 服务器的功能非常容易。任何具备良好 C 或 Perl 编程专业知识的人都可以编写一个模块来执行特定功能。这意味着有大量可用的 Apache 模块。

- **Apache 是一项免费、开源的技术。** 免费很重要，但开源比免费更重要。

- **Apache 与 Perl、PHP 和其他脚本语言配合极佳。** 大多数 Web 应用仍然是脚本。Perl 在脚本领域表现出色，Apache 通过支持 CGI 和 *mod_perl*，让使用 Perl 变得轻而易举。

- **Apache 运行在 Linux 和其他 Unix 系统上。** Linux 曾被视为弱势操作系统，如今已置身企业计算领域。如今，Linux 和 Apache 在企业界相辅相成。我相信 Linux 在商业界的接受度使得 Apache 更容易进入该领域。然而，也有人认为，正是 Apache 的名声让 Linux 更容易进入商业世界。无论如何，Apache 和 Linux 是一个强大的组合。其他 Unix 系统如 FreeBSD 和 Solaris，以及新的 Mac OS X，也在扩展 Apache 用户基础方面发挥了巨大作用。

- **Apache 也运行在 Windows 上。** 虽然 Apache 在 Windows 平台上的 2.0 版本表现更佳，但 Apache 早在 1.3.x 版本时就已进入 Windows 市场。我们将看到许多 Windows 系统从 Microsoft Internet Information Server (IIS) 转向 Apache，因为 Apache 2.0 的架构赋予了它原生竞争所需的能力。




## Apache：起源

以下是关于 Apache 的一些历史背景。在互联网发展的早期，国家超级计算应用中心（NCSA）开发了一个 Web 服务器，该服务器在 1995 年初成为了排名第一的 Web 服务器。然而，NCSA Web 服务器的主要开发者大约在同时离开了 NCSA，服务器项目随后开始停滞不前。与此同时，正在使用 NCSA Web 服务器的人们开始互相交换针对该服务器的自定义补丁，并很快意识到需要一个论坛来管理这些补丁。Apache 小组应运而生。该小组使用了 NCSA Web 服务器的代码，并孕育出了一款名为 Apache 的新 Web 服务器。Apache 服务器最初衍生自 NCSA Web 服务器的核心代码以及一系列补丁，如今它已是 Web 服务器社区热议的话题。在短短三年内，它便在市场中获得了领先服务器的地位。

首个公开分发的 Apache 版本（0.6.2）发布于 1995 年 4 月。1.0 版本于 1995 年 12 月 1 日发布。Apache 小组规模不断壮大，并已注册为一家非营利组织。该小组完全通过互联网进行运作。然而，Apache 服务器的开发并不受该小组的任何限制。任何拥有参与服务器或其组件模块开发技术的开发者都可以参与其中，尽管该小组是决定哪些内容包含在所谓的 Apache Web 服务器标准发行版中的最终权威。这实际上让全球成千上万的开发者能够提出新功能、修复漏洞、移植到新平台等等。当新代码提交给 Apache 小组时，小组成员会调查细节、执行测试并进行质量控制检查。如果满足要求，该代码将被整合到主要的 Apache 发行版中。

## Apache 功能列表

Apache 提供的最显著特性之一是它几乎能在所有广泛使用的计算机平台上运行。起初，Apache 主要是一个基于 Unix 的 Web 服务器，但情况现已不再如此。Apache 不仅运行在大多数（如果不是全部）版本的 Unix 上，还运行在 Windows 2000/NT/9x 以及许多其他桌面和服务器级操作系统上，例如 Amiga OS 3.x 和 OS/2。

Apache 提供了许多其他功能，包括精美的目录索引、目录别名、内容协商、可配置的 HTTP 错误报告、CGI 程序的 SetUID 执行、子进程的资源共享管理、服务器端图像地图、URL 重写、URL 拼写检查以及在线手册。

Apache 的其他主要特性包括：

- **支持最新的 HTTP 1.1 协议：** Apache 是早期集成 HTTP 1.1 协议的 Web 服务器之一。它完全符合新的 HTTP 1.1 标准，同时向后兼容 HTTP 1.0。Apache 已准备好迎接新协议带来的所有精彩功能。

  例如，在 HTTP 1.1 出现之前，Web 浏览器必须等待 Web 服务器的响应后才能发出另一个请求。随着 HTTP 1.1 的出现，这种情况不再发生。Web 浏览器可以并行发送请求，通过不在每个请求中传输 HTTP 头来节省带宽。由于并行请求的文件在浏览器上显示得更快，这可能会在终端用户端提供性能提升。

- **简单而强大的基于文件的配置：** Apache 服务器并不附带图形用户界面供管理员使用。它带有一个名为 `httpd.conf` 的主要单一配置文件，你可以用它来按照自己的喜好配置 Apache。你只需要你最喜爱的文本编辑器。然而，它的灵活性足以让你将虚拟主机配置分散在多个文件中，以免单个 `httpd.conf` 文件在处理大量虚拟服务器配置时变得过于繁琐。

- **支持 CGI（通用网关接口）：** Apache 使用 `mod_cgi` 和 `mod_cgid` 模块支持 CGI。它符合 CGI 1.1 标准，并提供了自定义环境变量和调试支持等扩展功能，这些在其他 Web 服务器中很难找到。详细参见第 12 章。

- **支持 FastCGI：** 并非所有人都使用 Perl 编写 CGI，那么他们如何让 CGI 应用运行得更快呢？Apache 也有解决方案。使用 `mod_fastcgi` 模块可以在 Apache 中实现 FastCGI 环境，并使你的 FastCGI 应用运行得飞速快。详细参见第 14 章。

- **支持虚拟主机：** Apache 也是最早支持基于 IP 和基于名称的虚拟主机的 Web 服务器之一。详细参见第 6 章。

- **支持 HTTP 身份验证：** Apache 支持基于 Web 的基本身份验证。它也支持基于消息摘要的身份验证，这是一种流行的 Web 浏览器尚未实现的功能。Apache 可以使用标准密码文件、DBMS、SQL 调用或调用外部身份验证程序来实现基本身份验证。详细参见第 7 章。

- **集成 Perl：** Perl 已成为 CGI 脚本编程的事实标准。Apache 无疑是使 Perl 成为如此流行的 CGI 编程语言的因素之一。Apache 现在比以往任何时候都更加支持 Perl。使用其 `mod_perl` 模块，你可以将基于 Perl 的 CGI 脚本加载到内存中并无限次重用。这一过程消除了通常与 Perl 这类解释型语言相关的启动开销。详细参见第 16 章。

- **支持 PHP 脚本：** 这种脚本语言已被非常广泛地使用，Apache 使用 `mod_php` 模块为 PHP 提供了极佳的支持。详细参见第 15 章。

- **Java Servlet 支持：** Java servlets 和 Java Server Pages (JSP) 在动态网站中变得非常普遍。你可以使用屡获殊荣的 Tomcat 环境在 Apache 中运行 Java servlets。详细参见第 17 章。

Apache Server 2.0 使 Apache 成为比以往任何时候都更灵活、更具可移植性且更具可扩展性的 Web 解决方案。新的 2.0 版本提供许多改进，主要改进将在以下章节中讨论。

## 多处理模块

Apache 2.0 中的第一个重大变化是引入了多处理模块（MPMs）。为了理解为什么创建 MPMs，你需要了解 Apache 之前的工作方式。Apache 1.3 或更早版本使用预派生架构。在这种架构中，Apache 父进程派生出一组子进程，这些子进程处理实际请求。父进程只是监控子进程，并根据接收到的请求数量生成或终止子进程。不幸的是，这种模型在以进程为中心的平台（如 Windows）上运行不佳。因此，Apache 小组提出了基于 MPM 的解决方案。

每个 MPM 负责启动服务器进程，并根据 MPM 的实现，通过子进程或线程来服务请求。有多种 MPM 可用。它们将在以下章节中讨论。

### Prefork MPM

Prefork MPM 模拟 Apache 1.3 或更早版本的架构，创建一个子进程池来服务请求。每个子进程拥有单个线程。例如，如果 Apache 启动 30 个子进程，它可以同时服务 30 个请求。

如果出现问题且子进程死亡，仅丢失单个请求。子进程的数量通过最小值和最大值设置来控制。当请求数量增加时，新的子进程将被添加，直到达到最大值。类似地，当请求量下降时，多余的子进程将被终止。

### Threaded MPM

此 MPM 在 Apache 2.0 中启用线程支持。这与 Prefork MPM 类似，但每个子进程不再只有一个线程，而是允许每个子进程拥有一定数量的线程。子进程内的每个线程可以服务不同的请求。如果 Apache 启动 30 个子进程，且每个子进程最多允许拥有 10 个线程，那么 Apache 可以同时服务 30 × 10 = 300 个请求。

如果线程出现问题，例如一个实验性模块导致线程死亡，则整个进程死亡。这意味着由该子进程内线程服务的所有请求都会丢失。然而，由于请求分布在不同的子进程之间的线程上，子进程的死亡最多只会导致全部总连接数的 1/n 中断，其中 n 表示所有并发连接的数量。

通过监控其空闲线程数来添加或移除进程。例如，如果一个进程的空闲线程少于最小数量，则会添加一个新进程。类似地，当一个进程拥有最大数量的空闲线程时，它会被终止。

所有进程都在分配给 Apache 服务器的同一用户和组 ID 下运行。

由于线程比进程更节省资源，此 MPM 非常具有可扩展性。

### Perchild MPM

这也是 Apache 2.0 中的新特性。在此 MPM 模型中，启动固定数量的子进程，每个进程拥有指定数量的线程。随着请求负载增加，进程根据需要添加新线程。当请求数量减少时，进程使用最小和最大线程数设置缩减其线程数量。

此模块与 Threaded MPM 的关键区别在于，进程数量是静态的，并且每个进程可以使用不同的用户和组 ID 运行。这使得在不同用户和组 ID 下运行不同的虚拟网站变得非常容易。详细参见第 6 章。

### Winnt MPM

这是 Windows 平台（包括 Windows 2000、Windows NT 和 Window 9x）的 MPM。它是一个多线程模块。使用该模块，Apache 将创建一个父进程和一个子进程。子进程创建所有的线程，这些线程……


服务于该请求。此外，该模块现在还能利用一些仅适用于 Windows 的原生函数调用，这使得它在 Windows 平台上的性能优于早期版本的 Apache 服务器。

## I/O 过滤

Apache 2.0 现在提供了分层 I/O 架构。这意味着一个模块的输出可以成为另一个模块的输入。这种过滤效果非常有趣。例如，由 CGI 脚本生成的输出（由 `mod_cgi` 模块处理）现在可以传递给负责 SSIs 的 `mod_include` 模块。换句话说，CGI 脚本可以生成包含 SSI 标记的输出，这些标记可以在最终输出发送到 Web 浏览器之前进行处理。未来还将出现许多其他 I/O 过滤的应用。

## 新的 CGI 守护进程

由于许多 MPM 模块都使用线程，当线程接收到此类请求时，执行 CGI 脚本会变得更加繁琐。`mod_cgi` 模块仍然可以工作，但对于线程化的 MPM 来说并非最优方案，因此增加了 `mod_cgid`。`mod_cgid` 模块创建一个守护进程，该进程生成 CGI 进程，并与线程更高效地交互。图 1-1 展示了对名为 `myscript.pl` 的脚本的 CGI 请求是如何被处理的。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_39_0.png)

以下是 CGI 脚本的执行方式：

- 当 CGI 请求到达子进程内的线程时，该线程会将请求传递给 CGI 守护进程。
- CGI 守护进程生成 CGI 脚本，并将 CGI 脚本生成的数据输出到子进程中的线程。
- 线程将数据返回给 Web 浏览器。

当主 Apache 服务器启动时，它也会启动 CGI 守护进程并建立套接字连接。因此，当创建一个新的子进程时，它会继承该套接字连接，从而无需为每个请求单独创建到 CGI 守护进程的连接。整个过程改善了线程环境下的 CGI 执行效率。

# Apache 可移植运行时

为了践行 Apache 团队打造世界上最受欢迎的 Web 服务器的愿景，人们认识到 Apache 2.0 需要解决可移植性问题。在本次版本发布之前，Apache 一直在内部处理可移植性问题，这使得代码库难以管理。因此，Apache 团队引入了 Apache 可移植运行时（APR）。APR 的目的是为平台特定的函数提供单一的 C 接口，从而只需编写一次代码。

这使得 Apache 能够更原生地运行在 Windows、BeOS、Amiga 和 OS/2 等平台上。得益于 APR，许多程序（如 ApacheBench）也能在这些平台上运行。

# 理解 Apache 许可证

像 Apache、Perl（实用提取和报告语言）和 Linux（一种基于 x86 的类 Unix 操作系统）这样的免费软件，由于 Netscape 决定通过其 Mozilla 项目免费提供 Netscape Communicator（最受欢迎的 Web 浏览器之一），因此获得了大量媒体关注。不幸的是，像 Apache、Perl 和 Linux 这样的免费软件并不共享相同的许可协议，因此媒体将这些软件包归入同一许可类别造成了一定的混乱。

所有免费软件的初衷都是真正地为所有人免费提供。然而，各个软件许可证存在一些法律限制。例如，Linux 由 GNU 通用公共许可证（GPL）使其免费，该许可证要求对 Linux 所做的任何更改都必须公开。另一方面，Apache 并不要求任何人将所做的更改公开。

简而言之，可以将 Apache 视为由 Apache 团队发布的受版权保护的免费软件。它既不属于公共领域，也不是共享软件。还要注意，Apache 不受 GPL 覆盖。为便于阅读，Apache 软件许可证文件列在列表 1-1 中。

**列表 1-1：Apache 软件许可证**

```
/* ------------------------------------------------------------------ * The Apache Software License, Version 1.1 * Copyright (c) 2000-2001 The Apache Software Foundation. All rights reserved. * Redistribution and use in source and binary forms, with or without * modification, are permitted provided that the following conditions * are met: * 1. Redistributions of source code must retain the above copyright * notice, this list of conditions and the following disclaimer. * 2. Redistributions in binary form must reproduce the above copyright * notice, this list of conditions and the following disclaimer in * the documentation and/or other materials provided with the * distribution. * 3. The end-user documentation included with the redistribution, * if any, must include the following acknowledgment: * "This product includes software developed by the * Apache Software Foundation (http://www.apache.org/)." * Alternately, this acknowledgment may appear in the software itself, * if and wherever such third-party acknowledgments normally appear. * 4. The names "Apache" and "Apache Software Foundation" must * not be used to endorse or promote products derived from this * software without prior written permission. For written * permission, please contact apache@apache.org. * 5. Products derived from this software may not be called "Apache", * nor may "Apache" appear in their name, without prior written * permission of the Apache Software Foundation. * THIS SOFTWARE IS PROVIDED "AS IS" AND ANY EXPRESS OR IMPLIED * WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES * OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE * DISCLAIMED. IN NO EVENT SHALL THE APACHE SOFTWARE FOUNDATION OR * ITS CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, * SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT * LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF * USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND * ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, * OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT * OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF * SUCH DAMAGE. *
 * ------------------------------------------------------- * 
 * This software consists of voluntary contributions made by many 
 * individuals on behalf of the Apache Software Foundation.  For more
 * information on the Apache Software Foundation, please see 
 * <http://www.apache.org/>.
 * 
 * Portions of this software are based upon public domain software 
 * originally written at the National Center for Supercomputing Applications,
 * University of Illinois, Urbana-Champaign.
 */
```

# 获取和安装 Apache

![](img/e11fcbd2818a3495ac70085e5d8d1c26_43_0.png)

# 第 2 章

![](img/e11fcbd2818a3495ac70085e5d8d1c26_43_1.png)

# 本章内容

- 寻找最新的 Apache 源码
- Apache 的系统要求
- 下载软件
- 编译源码
- 在系统上安装二进制文件
- 跟进 Apache 的最新发展

![](img/e11fcbd2818a3495ac70085e5d8d1c26_43_2.png)

虽然编译自己的 Apache 二进制文件可能看起来有些麻烦，但这是值得付出的努力。随着您对 Apache 变得更加熟悉，您会发现它是唯一提供几乎所有（甚至更多）完整商业服务器功能的 Web 服务器，同时它还允许您查看这些功能在源码中是如何实现的。我觉得 Apache 的这一点非常迷人。

然而，对于非 C 程序员但依然需要强大且免费的 Web 服务器的人群来说，处理大量的 ANSI C 代码可能并不是什么爱好。幸运的是，您无需担心——Apache 既有源码版本，也有预编译的二进制包版本。本章将讨论从源码和预编译二进制文件安装 Apache 的方法。

## Apache 的官方来源

每当从互联网获取免费软件（源码或二进制文件）时，请确保您不是从一个未知的 Web 或 FTP 站点获取的。我所说的“未知”可以通过一个例子来更好地理解。假设您想获取由 Sun Microsystems 开发的基于 Java 的免费 Web 浏览器软件。您需要能够进行某种真实性检查，这在互联网上通常比较困难；因此，您应该坚持使用广泛认可的站点。例如，您不希望从一个主机名像 `dialup-666.someforeignisp.net.ch` 这样的 FTP 站点获取它；相反，您最好去 `java.sun.com` 网站上的某个地方寻找，因为您无法确定 `666.someforeignisp.net.ch` 是否已彻底检查该软件是否存在任何隐藏危险。您明白我的意思了。





对我们来说幸运的是，Apache 开发者和支持者们确保建立了一个官方的 Apache 软件获取平台。Apache 官方网站是 www.apache.org。该网站包含最新的稳定版 Apache、最新的发行版 Apache、补丁、贡献的 Apache 模块等等。这是满足你所有 Apache 需求的地方——尽管你可能会被重定向到地理位置离你较近的镜像站点，以帮助减少带宽和网络拥塞。你还可以使用该站点提供的 PGP 签名来验证源代码的真实性。如果你不知道如何使用 PGP，请访问 www.pgp.net 了解。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_44_0.png)

Windows 用户：请阅读第 20 章以了解关于你平台的详细信息。本章主要面向 Unix 安装，并使用 Linux 作为示例平台。本章中的说明适用于大多数 Unix 系统。

## 系统需求

Apache 几乎可以运行在当今任何可用的平台上，包括 Linux; FreeBSD; OpenBSD; NetBSD; BSDI; Amiga OS 3.x; Mac OS X; SunOS; Solaris; IRIX; HPUX; Digital Unix; UnixWare; AIX; SCO; ReliantUNIX; DGUX; OpenStep/Mach; DYNIX/ptx; BeOS; 和 Windows。

### 从源代码构建 Apache 的需求

如果你计划从源代码构建 Apache（我强烈建议你这样做，因为自己编译可以为你提供一个精简且性能强大的服务器），那么你需要确保你的系统满足表 2-1 中列出的需求。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_44_1.png)

这些需求仅适用于从源代码构建 Apache。关于在你的系统上运行 Apache，请参阅下一节中的需求。

## 表 2-1 从源代码构建 Apache 的需求

| 资源 | 是否必需 | 需求 |
| :--- | :--- | :--- |
| 磁盘空间 | 必需 | 从源代码包编译和安装 Apache 大约需要 12 MB 的磁盘空间。但是，如果你添加了许多不属于标准源代码包的模块，那么你的空间需求将会增加。安装完成后，Apache 只需要大约 5 MB 的磁盘空间。然而，我强烈建议你在读完这本书之前保留硬盘上的源代码。 |
| ANSI C 编译器 | 必需 | 需要 ANSI C 编译器。对于大多数系统，来自自由软件基金会 (Free Software Foundation) 的 GNU C 编译器 (GCC) 是高度推荐的。你拥有的版本应该是 2.7.2 或更高版本。可以在 www.gnu.org 找到 GCC。大多数 Linux 系统（如 Red Hat Linux）都附带了最新稳定版的 GCC 编译器。 |
| Perl 5 解释器 | 推荐 | 编译 Apache 不需要 Perl，但源代码包 support 子目录中的一些支持脚本，如 *apxs*、*split-logfile*、*log_server_status* 和 *dbmanage*，是 Perl 脚本。只有当你计划使用这些脚本时才需要 Perl。我强烈建议你在系统上安装 Perl。Perl 版本 5.003 或更高版本都可以正常运行。 |

**表 2-1（续）**

| 资源 | 是否必需 | 需求 |
| :--- | :--- | :--- |
| 动态共享对象 (DSO) 支持 | 可选 | 你可以选择在 Apache 二进制文件中编译模块，也可以创建称为 DSO 的动态模块，这些模块可以通过 `httpd.conf` 文件在启动时加载。DSO 模块使你可以比将所有内容编译到 httpd 中更自由地实验模块和配置。目前，DSO 支持以下平台：Linux, FreeBSD; OpenBSD; NetBSD; BSDI; SunOS; Solaris; IRIX; HPUX; Digital Unix, UnixWare, AIX, SCO, ReliantUNIX, DGUX, Darwin/Mac OS, OpenStep/Mach, 和 DYNIX/ptx。请注意，使用 DSO 模块的 Apache 服务器启动时速度可能慢约 20%，运行期间速度可能慢约 5%。此外，DSO 并非在所有平台上都可用。因此，我不建议在生产环境中使用 DSO。但是，在开发或测试环境中实验模块时，它是非常出色的。 |

### 运行 Apache Web 服务器的需求

在你的 Web 服务器上显示 Powered by Apache 标志之前，你希望确保你的 Web 服务器有足够的“动力”来运行它。

幸运的是，Apache 运行并不要求大量的计算资源。它可以在拥有 5 到 12MB 硬盘空间和 8MB RAM 的 Linux 系统上良好运行。然而，仅仅能够运行 Apache 可能并不是你的初衷。最有可能的是，你想运行 Apache 来提供 Web 页面、启动 CGI 进程，并利用 Web 的所有奇妙之处。在这种情况下，你需要反映负载需求的磁盘空间和 RAM 大小数值。你可以通过两种方法来完成这一点：你可以询问运行类似 Apache 站点的人，了解他们使用什么样的系统资源；或者，你可以在系统上安装 Apache 后，尝试弄清楚你的实际需求。

在后一种情况下，你可以使用 `ps`、`top` 等系统实用程序来显示特定 Apache 进程的内存使用情况。然后，你可以将单个进程的内存使用量乘以高峰时段运行的 Apache 进程总数（参见第 4 章中的 `MaxSpareServers` 指令），从而确定所需的总内存量。这应该能给你一个关于你的网站 Apache RAM 需求的合理估计。如果你计划在 Apache 服务器上运行多个 CGI 程序，你还必须确定这些程序的内存使用情况，并考虑这一额外需求。确定 CGI 程序内存需求的一种方法是运行该 CGI 程序并使用 `top` 实用程序观察它使用了多少内存，然后将该内存量乘以你需要同时处理的 CGI 请求数。

由于 Apache 二进制文件占用的空间不超过 1MB，源代码文件约为 5MB，因此对于大多数系统来说，Apache 源代码或二进制文件的磁盘需求应该不是问题。然而，你应该特别注意 Apache 创建的日志文件，因为每个日志条目约占 80 字节的磁盘空间。例如，如果你预计每天大约有 100,000 次访问，那么你的 Apache 访问日志文件可能是 8,000,000 字节。在第 8 章中，你将学习如何通过清空或归档日志文件并用新文件替换它来轮转日志文件。

最后，请考虑你是否有适合运行 Web 服务器的带宽。估计带宽需求并非易事，但你可以通过做一些数学计算得出大致数值。以下是你需要了解的内容：

-   **你的网站 Web 页面的平均大小：** 如果你还不知道这一点，你可以在文档根目录中运行以下命令来找出你的 Web 页面的平均大小：

```text
find_path_to_doc_root -type f -name "*.html" -ls | \
awk 'BEGIN{ FileCNT = 0; T_SIZE = 0;} \
{ T_SIZE += $7; FileCNT++} \
END{print "Total Files:", FileCNT, \
"Total Size:", T_SIZE, \
"Average Size:", T_SIZE / FileCNT;}'
```

**注意** 别忘了将 `path_to_doc_root` 替换为你网站的实际文档根目录。例如，对于一个文档根目录为 /www/mystsite/htdocs 的网站，上述脚本将返回以下输出：

```text
Total Files: 332 Total Size: 5409725 Average Size: 16294.4
```

-   **你可以提供的平均大小 Web 页面的数量**（假设 Apache 本身没有瓶颈，并完全忽略入站请求使用的带宽）：例如，假设你有 ISDN（128Kbits/sec）连接到互联网，且你的平均文件大小为 16K。由于 128 千比特/秒 = 128/8 千字节/秒 = 16 千字节/秒，你可以每秒发送一个平均大小的文件。如果包含其他开销，如入站请求流量所需的带宽，你可能每秒无法处理一个请求。在这种情况下，如果你想允许 *N*（其中 *N* > 1），网络开销将成为一个巨大的瓶颈



同时连接到您的 Web 站点的用户数量。例如，如果您拥有 ISDN 连接，并且希望在平均文件大小为 16K 时每秒服务 12 个并发用户，您需要 12 条 ISDN（128 kbps）连接，这相当于一条 T-1（1.53 Mbps）线路。

## 下载软件

在您第一次下载 Apache 软件之前，应该注意以下几点。您很有可能会发现有两个版本的 Apache 可用：一个是官方发布版本，另一个是拥有最新代码和功能的 Beta 发布版本。例如，如果您看到 Apache 2.0.2 版本和一个名为 2.3b3 的版本，那么第一个版本是官方发布版本，第二个版本是 Beta 版本。第三个 Beta 版本（如 2.3b3，在它之前有 2.3b1 和 2.3b2）可能比较稳定，但不建议在生产 Web 服务器上使用 Beta 版本。若要下载您想要的版本，请访问 www.apache.org/dist/httpd/。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_48_0.png)

> **提示**
> 若要找到地理位置最近的 Apache 镜像服务器，请运行位于 www.apache.org/dyn/closer.cgi 的镜像 Apache 查找脚本。

这是 Apache 软件的发行目录。在这里，您可以找到软件的各种压缩格式包，包括正式发布版本和 Beta 版本。例如：

```text
httpd_2.0.4.tar.Z
httpd_2.0.4.tar.gz
httpd_2.0.4.zip

httpd_2.3b3.tar.gz
httpd_2.3b3_win32.exe
```

这些是用于分发源代码的各种压缩格式的几个示例。您需要选择您的系统可以处理的压缩格式（换句话说，确保您有一个工具来解压缩代码）。通常，在 Linux 系统中，您只需要 `tar`、`gzip` 或 `gunzip` 实用工具即可解压缩文件。例如，要在 Linux 系统上解压缩 `httpd_version.tar.gz` 文件（其中 `version` 是您下载的版本号，例如 2.0.4），请使用 `tar xzvf httpd_version.tar.gz` 命令。您还可以使用 `gzip -d httpd_version.tar.gz ; tar xvf httpd_version.tar` 命令，该命令将在保留每个文件相对路径完整的情况下，在一个子目录中解压缩并提取所有文件。

自解压压缩文件通常是为 Windows 版本的 Apache 创建的。此类文件只需运行下载的文件即可解压。对于 Windows 特定的安装和配置详细信息，你应该跳过本章的其余部分，并阅读第 20 章。

二进制文件通常存放在另一个目录中，每个操作系统都有自己的子目录。请注意，如果您的操作系统没有出现在二进制文件目录中，这并不意味着该操作系统不受支持。这只是意味着 Apache 开发组或贡献组中还没有人为您的系统编译二进制文件。您可能会找到 Linux、FreeBSD、Solaris、NetBSD、OS2、AIX、Ultrix、HPUX 和 IRIX 系统的二进制文件。

### 从源代码安装 Apache

通过编译源代码发行版中的代码来安装 Apache 是首选的安装方法，因为它允许您根据需求配置服务器。您下载的任何二进制安装都包含别人的配置，您可能无法根据需求对其进行修改。

例如，如果您下载并安装了一个支持 CGI 的二进制文件，即使您从不运行 CGI 程序，您也可能不得不接受这种 CGI 支持。如果 CGI 模块被配置为动态共享模块，那么您可以轻松禁用它；但是，如果该支持是静态构建到二进制文件中的，那么您就只能忍受 CGI 了。然而，如果您从源代码发行版编译一个精简且高效的 Apache 服务器，您将获得所需的组件，而没有浪费进程或磁盘空间。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_49_0.png)

从官方 Apache 网站或指定的镜像站点下载源代码发行版。

### 配置 Apache 源代码

Apache 源代码发行版附带一个名为 `configure` 的脚本，允许您在编译和安装二进制文件之前配置源代码树。从 Apache 源代码发行版目录中，您可以按以下方式运行此脚本：

```sh
./configure --prefix=apache_installation_dir
```

`--prefix` 选项告诉 Apache 将二进制文件及其他必要的配置和支持文件安装在 `apache_installation_dir` 中。例如：

```sh
./configure --prefix=/usr/local/apache
```

这里，Apache 源代码将被配置为将所有二进制文件和支持文件安装在 `/usr/local/apache` 目录中。

`configure` 脚本可以使用许多选项。表 2-2 显示了所有可用的配置选项。

**表 2-2 Configure 脚本的选项**

| **选项** | **含义** |
| :--- | :--- |
| `--cache-file=file` | 在 `file` 中缓存测试结果 |
| `--help` | 打印此消息 |
| `--no-create` | 不创建输出文件 |
| `--quiet` 或 `--silent` | 不打印“正在检查……”消息 |
| `--version` | 打印创建 configure 的 autoconf 版本 |
| `--prefix=prefix` | 在 `prefix` 中安装与体系结构无关的文件 [`/usr/local/apache2`] |
| `--exec-prefix=eprefix` | 在 `eprefix` 中安装与体系结构相关的文件 [与 `prefix` 相同] |
| `--bindir=dir` | 在 `dir` 中放置用户可执行文件 [`EPREFIX/bin`] |
| `--sbindir=dir` | 在 `dir` 中放置系统管理可执行文件 [`EPREFIX/sbin`] |
| `--libexecdir=dir` | 在 `dir` 中放置程序可执行文件 [`eprefix/libexec`] |
| `--datadir=dir` | 在 `dir` 中放置只读的与体系结构无关的数据 [`eprefix/share`] |
| `--sysconfdir=dir` | 在 `dir` 中放置只读的单机数据 [`eprefix/etc`] |
| `--sharedstatedir=dir` | 在 `dir` 中放置可修改的与体系结构无关的数据 [`eprefix/com`] |
| `--localstatedir=dir` | 在 `dir` 中放置可修改的单机数据 [`eprefix/var`] |
| `--libdir=dir` | 在 `dir` 中放置目标代码库 [`eprefix/lib`] |
| `--includedir=dir` | 在 `dir` 中放置 C 头文件 [`eprefix/include`] |
| `--oldincludedir=dir` | 在 `dir` 中放置非 GCC 的 C 头文件 [`/usr/include`] |
| `--infodir=dir` | 在 `dir` 中放置 Info 文档 [`eprefix/info`] |
| `--mandir=dir` | 在 `dir` 中放置 Man 文档 [`eprefix/man`] |
| `--srcdir=dir` | 在 `dir` 中查找源代码 [`configure dir` 或 ...] |
| `--program-prefix=prefix` | 在已安装的程序名称前添加 `prefix` |
| `--program-suffix=suffix` | 在已安装的程序名称后添加 `suffix` |
| `--program-transform-name=program` | 对已安装的程序名称运行 `sed`（流编辑器）程序 |
| `--build=build` | 为在 `build` 上构建进行配置 |
| `--host=host` | 为主机进行配置 |
| `--target=target` | 为 `TARGET` 进行配置 [TARGET=HOST] |
| `--disable-feature` | 不包含 `feature`（与 `--enable-FEATURE=no` 相同） |
| `--enable-feature[arg]` | 包含 `feature` [arg=yes] |
| `--with-package[arg]` | 使用 `package` [arg=yes] |
| `--without-package` | 不使用 `package`（与 `--with-package=no` 相同） |
| `--x-includes=dir` | X 包含文件位于 `dir` |
| `--x-libraries=dir` | X 库文件位于 `dir` |
| `--with-optim=flag` | 已弃用（使用 `OPTIM` 环境变量） |
| `--with-port=port` | 监听端口（默认为 80） |
| `--enable-debug` | 开启调试和编译时警告 |
| `--enable-maintainer-mode` | 开启调试和编译时警告 |
| `--enable-layout=layout` | 启用目录布局 |
| `--enable-modules=module-list` | 启用一个或多个指定的模块 |
| `--enable-mods-shared=module-list` | 将一个或多个指定模块作为共享模块启用 |
| `--disable-access` | 禁用基于主机的访问控制 |
| `--disable-auth` | 禁用基于用户的访问控制 |
| `--enable-auth-anon` | 启用匿名用户访问 |
| `--enable-auth-dbm` | 启用基于 DBM 的访问数据库 |
| `--enable-auth-db` | 启用基于 DB 的访问数据库 |
| `--enable-auth-digest` | 启用 RFC2617 Digest 认证 |
| `--enable-file-cache` | 启用文件缓存 |





## 表 2-2（续）

| 选项 | 含义 |
| :--- | :--- |
| `--enable-dav-fs` | 启用文件系统 DAV 提供程序 |
| `--enable-dav` | 启用 WebDAV 协议处理 |
| `--enable-echo` | 启用 ECHO 服务器 |
| `--enable-charset-lite` | 启用字符集转换 |
| `--enable-cache` | 启用动态文件缓存 |
| `--enable-disk-cache` | 启用磁盘缓存模块 |
| `--enable-ext-filter` | 启用外部过滤模块 |
| `--enable-case-filter` | 启用示例大写转换过滤器 |
| `--enable-generic-hook-export` | 启用钩子导出器示例 |
| `--enable-generic-hook-import` | 启用钩子导入器示例 |
| `--enable-optional-fn-import` | 启用可选函数导入器示例 |
| `--enable-optional-fn-export` | 启用可选函数导出器示例 |
| `--disable-include` | 禁用服务器端包含 |
| `--disable-http` | 禁用 HTTP 协议处理 |
| `--disable-mime` | 禁用文件扩展名到 MIME 的映射 |
| `--disable-log-config` | 禁用日志配置 |
| `--enable-vhost-alias` | 启用多主机模块 |
| `--disable-negotiation` | 禁用内容协商 |
| `--disable-dir` | 禁用目录请求处理 |
| `--disable-imap` | 禁用内部映像图（imagemaps） |
| `--disable-actions` | 禁用请求触发的操作 |
| `--enable-spellings` | 启用常见 URL 拼写错误纠正 |
| `--disable-userdir` | 禁用用户请求映射 |
| `--disable-alias` | 禁用请求转换 |
| `--enable-rewrite` | 启用 URL 重写规则 |
| `--disable-so` | 禁用 DSO 功能 |
| `--enable-so` | 启用 DSO 功能 |
| `--disable-env` | 清除/设置 ENV 变量 |
| `--enable-mime-magic` | 自动确定 MIME 类型 |
| `--enable-cern-meta` | 启用 CERN 类型元文件 |
| `--enable-expires` | 启用 Expires 头控制 |
| `--enable-headers` | 启用 HTTP 头控制 |
| `--enable-usertrack` | 启用用户会话跟踪 |
| `--enable-unique-id` | 启用每个请求的唯一 ID |
| `--disable-setenvif` | 禁用基于头的底层 ENV 变量 |
| `--enable-tls` | 启用 TLS/SSL 支持 |
| `--with-ssl` | 使用特定的 SSL 库安装 |
| `--with-mpm=MPM` | 选择 Apache 使用的进程模型：MPM={beos threaded prefork spmp os2 perchild} |
| `--disable-status` | 进程/线程监控 |
| `--disable-autoindex` | 禁用目录列表 |
| `--disable-asis` | 禁用 As-is 文件类型 |
| `--enable-info` | 启用服务器信息 |
| `--enable-suexec` | 为生成的进程设置 UID 和 GID |
| `--disable-cgid` | 禁用 CGI 守护进程支持 |
| `--enable-cgid` | 启用 CGI 守护进程支持 |
| `--disable-cgi` | 禁用 CGI 脚本支持 |
| `--enable-cgi` | 启用 CGI 脚本支持 |
| `--enable-shared[=pkgs]` | 构建共享库 [默认=no] |
| `--enable-static[=pkgs]` | 构建静态库 [默认=yes] |
| `--enable-fast-install[=pkgs]` | 优化以实现快速安装 [默认=yes] |
| `--with-gnu-ld` | 假设 C 编译器使用 GNU ld [默认=no] |
| `--disable-libtool-lock` | 避免锁定（可能会破坏并行构建） |
| `--with-program-name` | 可执行文件的备用名称 |
| `--with-suexec-caller` | 允许调用 SuExec 的用户 |
| `--with-suexec-userdir` | 用户子目录 |
| `--with-suexec-docroot` | SuExec 根目录 |
| `--with-suexec-uidmin` | 允许的最小 UID |
| `--with-suexec-gidmin` | 允许的最小 GID |
| `--with-suexec-logfile` | 设置日志文件 |
| `--with-suexec-safepath` | 设置安全路径 |
| `--with-suexec-umask` | 进程的 Umask |

对于大多数站点，这些选项中的大多数都不是必需的。通常，您只需要指定 `--prefix` 选项以及启用或禁用一个或多个模块的选项。例如，假设您不想在系统上安装 CGI 模块。您可以使用 `--disable-cgi` `--disable-cgid` 选项运行 `configure` 脚本来禁用 CGI 支持。类似地，若要禁用 *服务器端包含 (SSI)* 支持，您可以使用 `--disable-include` 选项。

使用 `configure` 脚本配置 Apache 后，您可以使用 `config.status` 脚本替代 `configure` 来满足任何后续的配置需求。通过使用 `config.status` 脚本，您可以重用之前的配置并添加或减少新选项。例如，假设您使用以下命令行配置了 Apache：

```
./configure --prefix=/usr/local/apache --disable-cgi --disable-cgid
```

几天后决定禁用 SSI。您现在可以使用：

```
./config.status --disable-include
```

重新编译 Apache 时，CGI 模块仍然不会被包含在内，因为 `./config.status` 存储了您之前使用 `configure` 脚本指定的选项。

如果您希望重新开始，请每次都使用 `configure`。

### 高负载 Web 站点的高级配置选项

如果您在一个极其繁忙的服务器上运行 Apache，且要求每秒处理数百个请求，您可能需要更改所选 MPM 模块中设置的默认硬性限制。有关各种 MPM 模块的详细信息，请参见第 1 章。您要考虑更改的硬性限制是默认的 `HARD_SERVER_LIMIT` 和 `HARD_THREAD_LIMIT`。`HARD_SERVER_LIMIT` 设置 Apache 可以生成的子服务器最大数量。`HARD_THREAD_LIMIT` 设置 Apache 可以在其所有子进程中创建的线程总数。表 2-3 显示了默认限制及其查找位置。

> 表中提到的 `@APACHE_SOURCE@` 标签指 Apache 源发行版目录。例如，如果您将 Apache 源发行版解压到 `/usr/local/src/httpd_version` 目录中，请将 `@APACHE_SOURCE@` 替换为 `/usr/local/src/httpd_version` 以定位适当的 C 头（include）文件。

#### 表 2-3
各种 Apache MPM 模块的硬性限制

| MPM | 限制选项 | 默认值 | 备注 |
|---|---|---|---|
| threaded | 线程模式下的 HARD_SERVER_LIMIT | 8 | C 头（include）文件名：<br>`$APACHE_SOURCE%/server/mpm/threaded/mpm_default.h`<br>```c<br>#ifndef NO_THREADS<br>#define HARD_SERVER_LIMIT 256<br>#endif<br><br>#ifndef HARD_SERVER_LIMIT<br>#define HARD_SERVER_LIMIT 8<br>#endif<br>``` |
| threaded | 线程模式下的 HARD_THREAD_LIMIT | 64 | C 头（include）文件名：<br>`$APACHE_SOURCE%/server/mpm/threaded/mpm_default.h` |
| prefork | HARD_SERVER_LIMIT | 256 | C 头（include）文件名：<br>`$APACHE_SOURCE%/server/mpm/prefork/mpm_default.h`<br>```c<br>#ifndef HARD_SERVER_LIMIT<br>#define HARD_SERVER_LIMIT 256<br>#endif<br>``` |
| perchild | HARD_SERVER_LIMIT | 8 | C 头（include）文件名：<br>`$APACHE_SOURCE%/server/mpm/perchild/mpm_default.h`<br>```c<br>#ifndef HARD_SERVER_LIMIT<br>#define HARD_SERVER_LIMIT 8<br>#endif<br>``` |
| perchild | HARD_THREAD_LIMIT | 64 | C 头（include）文件名：<br>`$APACHE_SOURCE%/server/mpm/perchild/mpm_default.h`<br>```c<br>#ifndef HARD_SERVER_LIMIT<br>#define HARD_SERVER_LIMIT 8<br>#endif<br>``` |
| winnt | HARD_SERVER_LIMIT | 1 | C 头（include）文件名：<br>`$APACHE_SOURCE%/server/mpm/winnt/mpm_default.h`<br>`#define HARD_SERVER_LIMIT 1`<br>不应更改此设置。请改为更改硬性线程数。 |
| winnt | HARD_THREAD_LIMIT | 4096 | C 头（include）文件名：<br>`$APACHE_SOURCE%/server/mpm/winnt/mpm_default.h`<br>```c<br>#ifndef HARD_THREAD_LIMIT<br>#define HARD_THREAD_LIMIT 4096<br>#endif<br>``` |

将 `HARD_SERVER_LIMIT` 或 `HARD_THREAD_LIMIT` 更改为高于默认值时，请确保您拥有适当的系统资源。例如，将 `prefork` MPM 的 `HARD_SERVER_LIMIT` 更改为 1024 将使您能够通过指示 Apache 使用指令 `StartServers`、`MinSpareServers` 和 `MaxSpareServers` 创建该数量的子进程来创建 1024 个 Apache 子进程。

然而，如果您的系统内存不足，将硬性限制更改为更高的值不会带来太大好处。请记住，限制越高，您需要的资源越多。您还需要增加系统允许单个用户使用的文件描述符数量。在 Linux 和 Unix 系统上，您应该使用 `ulimit` 命令来查找（并可能设置）文件描述符限制。

另外请注意，`MaxClients` 指令设置创建的用于处理请求的子进程数量的限制。当服务器在没有线程的情况下构建时，同时服务的客户端数量不能超过此数字。若要配置超过 256 个客户端，您必须编辑 `mpm_default.h` 中的 `HARD_SERVER_LIMIT` 条目并重新编译。

### 编译和安装 Apache

使用 `configure` 脚本配置 Apache 源代码后，您需要按照以下步骤编译和安装 Apache：

- 运行 `make` 命令以编译源代码。





2.  运行 `make install` 命令，安装 httpd 和支持文件到你在使用 `--prefix` 选项时指定的目录。

3.  更改到安装目录并浏览该目录。你应该能看到诸如 `bin`、`cgi-bin`、`conf`、`htdocs`、`icons`、`include`、`lib` 和 `logs` 等子目录。例如，如果你在源代码树配置过程中使用 `configure` 脚本时采用了 `--prefix=/usr/local/apache`，那么 `make install` 将创建如下目录结构：

```
/usr/local/apache
+---include
+---lib
+---bin
+---conf
+---htdocs
    |
    +---manual
        +---developer
        +---howto
        +---images
        +---misc
        +---mod
        +---platform
        +---programs
        +---search
        +---vhosts
    |
+---icons
    |
    +---small
+---logs
+---cgi-bin
```

以下列表简要描述了 Apache 目录结构中的每个目录：

-   `include` — 包含所有 C 头文件（include 文件），这些文件仅在你开发集成 Apache 的 Web 应用程序，或希望使用需要头文件的第三方软件与 Apache 配合使用时才需要。在生产服务器上，你可以删除此目录。

-   `lib` — 存放 Apache 可移植运行时（APR）库文件、运行 Apache 所需的文件以及其他支持实用程序，例如 ab。

-   `bin` — 包含表 2-4 中列出的程序。

-   `conf` — 存放 Apache 的配置文件。它包含表 2-5 中列出的文件。

-   `htdocs` — 这是主 Apache 服务器的默认文档根目录。httpd.conf 文件将 DocumentRoot 指令设置为该目录。你将在第 3 章中了解如何设置你自己的文档根目录。默认情况下，htdocs 目录还包含安装在子目录中的完整 Apache 手册。

-   `icons` — 用于存储各种 Apache 图标，这些图标在动态显示构建目录列表时是必需的。

-   `logs` — 用于存储 Apache 服务器日志、CGI 守护进程套接字（cgisock）和 PID 文件（httpd.pid）。你将在第 3 章中了解如何更改日志路径。

-   `cgi-bin` — 默认的 CGI 脚本目录，通过在 httpd.conf 中使用 ScriptAlias 指令进行设置。默认情况下，Apache 附带两个简单的 CGI 脚本 — `printenv` 和 `test-cgi`。当通过 `http://server_name/cgi-bin/script_name` URL 请求时，这些脚本会打印出 CGI 环境变量。这些脚本非常适合测试你的 CGI 配置是否正常工作。

**注意**

强烈建议在你完成 CGI 配置并使其正常工作后，删除 `printenv` 和 `test-cgi` 脚本。让任何人都可以查看你的系统环境信息的脚本并不是一个好主意。你对世界透露关于你的系统如何工作或系统上有什么可用资源的信息越少，你的系统就越安全。

表 2-4 提供了你可以在 `bin` 目录中找到的程序列表。

### 表 2-4 bin 目录中的 Apache 程序

| Apache 程序 | 用途 |
| :--- | :--- |
| ab | 这是 ApacheBench 程序。它使你能够对 Apache 服务器进行基准测试。有关此程序的更多信息，请参阅第 22 章。 |
| apachectl | 这是一个便捷的脚本，使你能够启动、重启和停止 Apache 服务器。有关此脚本的更多信息，请参阅第 3 章。 |
| apxs | 这是一个用于构建和安装 Apache 扩展模块的工具。它允许你使用 `mod_so` 模块来构建可以在 Apache 中使用的 DSO 模块。有关此程序的更多信息，请参阅 `http://your_server_name/manual/programs/apxs.html`。 |
| htdigest | 当使用消息摘要（MD5）认证时，该程序创建和更新用户认证信息。有关此程序的更多信息，请参阅 `http://your_server_name/manual/programs/htdigest.html`。 |
| `htpasswd` | 该程序用于创建和更新用于基本 HTTP 认证的用户认证信息。详情见第 7 章。 |
| `httpd` | 这是 Apache Web 服务器程序。 |
| `logresolve` | 该程序将日志文件中的 IP 地址转换（解析）为主机名。详情见第 8 章。 |
| `rotatelogs` | 当 Apache 日志文件达到一定大小时，该程序会旋转这些日志文件。详情见第 8 章。 |

表 2-5 列出了 `conf` 目录的内容。

### 表 2-5 Apache 配置目录内容

| 配置文件 | 用途 |
| :--- | :--- |
| `httpd.conf` | 这是 Apache 配置文件。 |
| `httpd-std.conf` | 这是 `httpd.conf` 文件的示例副本，Apache 并不要求此文件。对于新的 Apache 用户，此文件可以作为恢复默认 `httpd.conf` 的手段。 |
| `highperformance.conf` | 这是一个示例配置文件，展示了一些配置 Apache 以获得高性能的要点。 |
| `highperformance-std.conf` | 这是 `highperformance.conf` 文件的示例副本，Apache 并不要求此文件。 |
| `magic` | 此文件存储 `mod_mime_magic` Apache 模块的魔术数据。 |
| `mime.types` | 此文件用于决定对于给定文件，哪些 MIME 类型头发送给 Web 客户端。有关 MIME 类型的更多信息，请阅读 RFC 2045、2046、2047、2048 和 2077。互联网媒体类型注册表位于 <ftp://ftp.iana.org/in-notes/iana/assignments/media-types>。 |

你可以从 `www.apache.org/dist/httpd/binaries` 目录下载适合你系统的 Apache 二进制文件。下载最新版本并将压缩文件解压到一个临时目录。要了解如何在你的特定平台上安装这些二进制文件，你必须阅读每个二进制发行版中附带的 `INSTALL.bindist` 文件。

如果你希望为你的 Linux 系统安装 Apache RPM（Red Hat Package Management）软件包，请执行以下操作：

1.  前往 `http://rpmfind.net` 网站，搜索字符串 *Apache* 以找到 Apache RPM 软件包。从搜索结果中找到二进制 Apache RPM 发行版的最新版本并下载。
2.  作为 root 用户，运行 `ivh apache_rpm_package.rpm` 命令来安装该软件包。例如，要为 Red Hat Linux（Intel）系统安装 `apache-2.0.4-i386.rpm`，请运行 `rpm -ivh apache-2.0.4-i386.rpm` 命令。

## 紧跟 Apache 开发步伐

你是否曾想过，等到你准备好安装下载的 Apache 源代码或二进制文件时，是否会有新版本发布，或者是否有安全补丁可用？如今软件变化非常快，更新接二连三——这是好事，但如果你有实际工作要做，总是难以紧跟步伐。有两个 Apache 资源你应该立即加以利用。

-   **ApacheToday** — 这是世界上最好的 Apache 新闻网站。你可以在 `www.apachetoday.com` 上获取所有你想要的 Apache 新闻。通过使用其 Your Apache Today 功能，你可以过滤新闻内容，只获取你最感兴趣的内容。你还可以利用触发器来获取那些你不希望错过的突发新闻。

-   **ApacheWeek** — 只需订阅（免费）名为 Apache Week 的优质 Apache 资源，所有 Apache 新闻都将直接通过电子邮件发送给你。Apache Week 网站位于 `www.apache.week.com`。这对于希望紧跟 Apache 开发新闻的 Apache 管理员来说是一个极佳的信息资源。你还可以阅读许多关于如何充分发挥服务器性能有用文章。我强烈推荐查看此网站。

# 第 3 章

# 让 Apache 运行起来

在上一章中，你学习了如何在 Unix 系统上编译和安装 Apache Web 服务器。现在你准备好让它运行起来！本章涵盖了让你的 Apache 服务器运行起来所需的基本配置细节。

# 配置 Apache

默认情况下，Apache 读取名为 httpd.conf 的单个配置文件。每个 Apache 源代码发行版都附带一组示例配置文件。在标准的 Apache 源代码发行版中，你会找到一个名为 conf 的目录，其中包含带有 .dist 扩展名的示例配置文件。

在修改此文件之前，你需要采取的第一个步骤是创建原始文件的备份副本。

httpd.conf 文件包含两种类型的信息：注释和服务器指令。以 # 字符开头的行被视为注释行；这些注释对服务器软件没有目的，但它们充当服务器管理员的一种文档形式。你可以添加任意数量的注释；服务器在解析文件时会忽略所有注释。

除了注释和空白行外，服务器将所有其他行视为完整或部分指令。指令就像是给服务器的命令。它告诉服务器以特定方式执行特定任务。在编辑 httpd.conf 文件时，你需要就你希望服务器如何行为做出某些决定。在以下部分中，你将了解这些指令的含义，以及如何使用它们来定制你的服务器。

# 本章内容

-   检查 Apache 服务器配置的基础知识
-   启动、停止和重启 Apache 服务器
-   测试运行中的 Apache 服务器

![](img/e11fcbd2818a3495ac70085e5d8d1c26_61_0.png)

你可以在第 4 章中找到关于所有核心指令的深入解释。





清单 3-1 展示了在 Apache 安装目录的 `conf` 文件夹中创建的默认 `httpd.conf` 文件。为了简洁起见，大部分注释已被移除，代码也经过 slight 编辑。

# 清单 3-1：从 httpd.conf-dist 创建的默认 httpd.conf

```text
### Section 1: Global Environment
ServerRoot "/usr/local/apache"
PidFile logs/httpd.pid

<IfModule !perchild.c>
ScoreBoardFile logs/apache_runtime_status
</IfModule>

Timeout 300
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 15

<IfModule prefork.c>
StartServers      5
MinSpareServers   5
MaxSpareServers  10
MaxClients        20
MaxRequestsPerChild  0
</IfModule>

<IfModule threaded.c>
StartServers      3
MaxClients        8
MinSpareThreads   5
MaxSpareThreads  10
ThreadsPerChild  25
MaxRequestsPerChild  0
</IfModule>

<IfModule perchild.c>
NumServers        5
StartThreads      5
MinSpareThreads   5
MaxSpareThreads  10
MaxThreadsPerChild 20
MaxRequestsPerChild  0
</IfModule>

### Section 2: 'Main' server configuration
Port 80
User nobody
Group #-1

ServerAdmin you@your.address

# Added
ServerName www.domain.com

DocumentRoot "/usr/local/apache/htdocs"

<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>

<Directory "/usr/local/apache/htdocs">
    Options Indexes FollowSymLinks MultiViews
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>
UserDir public_html
DirectoryIndex index.html
AccessFileName .htaccess

<Files ~ "^\\.ht">
    Order allow,deny
    Deny from all
</Files>

UseCanonicalName On
TypesConfig conf/mime.types
DefaultType text/plain

<IfModule mod_mime_magic.c>
    MIMEMagicFile conf/magic
</IfModule>

HostnameLookups Off
ErrorLog logs/error_log
LogLevel warn

LogFormat ">%h %l %u %t \"%r\" %>s %b\" %i {Referer}\" \"%{User-Agent}i\" combined
LogFormat ">%h %l %u %t \"%r\" %>s %b\" common
LogFormat ">{Referer}i\" -> \"%U" referer
LogFormat ">%{User-agent}i" agent
CustomLog logs/access_log common
ServerSignature On
Alias /icons/ "/usr/local/apache/icons/"

<Directory "/usr/local/apache/icons">
    Options Indexes MultiViews
    AllowOverride None
    Order allow,deny

    Allow from all

  </Directory>

  ScriptAlias /cgi-bin/ "/usr/local/apache/cgi-bin/"

  <Directory "/usr/local/apache/cgi-bin">

    AllowOverride None

    Options None

    Order allow,deny

    Allow from all

  </Directory>

  IndexOptions FancyIndexing VersionSort

  AddIconByEncoding (CMP,/icons/compressed.gif) x-compress x-gzip

  AddIconByType (TXT,/icons/text.gif) text/*

  # Many more AddIconByType directives follow in the

  # default httpd.conf but removed here to keep

  # this simple.

  AddIcon /icons/binary.gif .bin .exe

  # Many more AddIcon directives follow in the

  # default httpd.conf but removed here to keep

  # this simple.

  DefaultIcon /icons/unknown.gif

  ReadmeName README

  IndexIgnore .??* *~ \* HEADER\* README\* RCS CVS \*,v \*,t

  AddEncoding x-compress Z

  AddEncoding x-gzip .gz .tgz

  AddLanguage da .dk

  AddLanguage nl .nl

  AddLanguage en .en

  # Many more AddLanguage directives follow in the

  # default httpd.conf but removed here to keep

  # this simple.

  LanguagePriority da nl et fr de el it ja kr no pl pt pt-br lts ca es sv tw

  AddDefaultCharset ISO-8859-1

  AddCharset ISO-8859-1 .iso8859-1 .latin1

  AddCharset ISO-8859-2 .iso8859-2 .latin2 .cen

  # Many more AddCharset directives follow in the

  # default httpd.conf but removed here to keep
# this simple.

AddType application/x-tar .tgz
BrowserMatch "Mozilla/2" nokeepalive
BrowserMatch "MSIE 4\.0b2;" nokeepalive downgrade-1.0 force-response-1.0
BrowserMatch "RealPlayer 4\.0" force-response-1.0
BrowserMatch "Java/1\.0" force-response-1.0
BrowserMatch "JDK/1\..0" force-response-1.0

### Section 3: Virtual Hosts
# No virtual server defined in this chapter.
```

本章的目标是让服务器以最小配置运行起来，因此本章不会详细介绍这里的配置选项。你可以在第 4 章中了解所有细节。

`httpd.conf` 文件实际上没有任何章节分隔符。但如果你按照图 3-1 所示的方式理解它，会更便于理解该配置文件。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_65_0.png)

该图左侧展示了默认 `httpd.conf` 在脑海中的可视化结构。有一些配置指令用于创建应用于所有内容的全球服务器环境；有一些配置选项应用于 Apache 服务器的主要（默认）网站；还有一些配置指令仅应用于可选的虚拟主机。由于 Apache 使用单个配置文件，拥有大量虚拟主机的网站将拥有非常大的文件，配置管理也会变得非常繁琐。这就是为什么我也展示了另一种分解 `httpd.conf` 文件的方法。但我在第 6 章中讨论了这种方法（上述图的右侧很明显体现了这一点）。正如我之前所说，这里我们专注于让服务器运行起来。

> 每当我提到 `%directive%` 时，我指的是配置文件中设置的指令值。例如，如果名为 `ServerAdmin` 的指令被设置为 `kabir@domain.com`，那么对 `%ServerAdmin%` 的引用意味着“kabir@domain.com”。因此，如果我让你更改 `%ServerAdmin%`，我是要求你更改该电子邮件地址。

# 配置 Apache 的全局环境

本节讨论的指令为 Apache 服务器创建全局环境。这些指令按照它们在 `httpd.conf` 文件中出现的顺序进行讨论。第一个指令是 `ServerRoot`，其形式如下：

```text
ServerRoot "/usr/local/apache"
```

该指令指定 Web 服务器的顶级目录。指定的目录不是存储 Web 内容的地方。它实际上是一个目录，通常包含这些子目录：

```text
(ServerRoot Directory)
|----bin
|----conf
|----htdocs
|----htdocs/
|--manual
|----developer
|----howto
|----images
|----misc
|----mod
|----platform
|----programs
|----search
|----vhosts
|----icons
|  ↑---small
|----logs
\----cgi-bin
+----include
```

`/usr/local/apache` 是所有服务器相关文件的父目录。`ServerRoot` 的默认值设置为你在使用 `configure` 脚本进行源配置时为 `--prefix` 选项选择的值。默认情况下，服务器安装期间执行的 `make install` 命令会将所有服务器二进制文件复制到 `%ServerRoot%/bin`，将服务器配置文件复制到 `%ServerRoot%/conf`，等等。

> 注意
> 只有当你手动将整个目录从安装位置移动到另一个位置时，才应该更改此指令的值。例如，如果你简单地运行 `cp -r /usr/local/apache /home/apache` 并希望配置 Apache 服务器从新位置工作，你会将此指令更改为 `ServerRoot /home/apache`。注意，在这种情况下，你还必须将对 `/usr/local/apache` 的其他直接引用更改为 `/home/apache`。

还要注意，每当你在配置文件中看到相对目录名称时，Apache 会在路径前添加 %ServerRoot% 以构建实际路径。你将在下一节的指令中看到一个示例。

# PidFile

`PidFile` 指令设置 PID（进程 ID）文件路径。默认情况下，它被设置为 `logs/httpd.pid`，这对应于 `%ServerRoot%/logs/httpd.pid`（即 `/usr/local/apache/logs/httpd.pid`）。每当你想要查找以 `root` 身份运行并生成子进程的主 Apache 进程的 PID 时，你可以运行 `cat %ServerRoot%/logs/httpd.pid` 命令。别忘了将 `%ServerRoot%` 替换为适当的值。

> 警告
> 如果你将 %PidFile% 值更改为指向不同的位置，出于安全原因，请确保 `httpd.pid` 文件所在的目录仅允许 `root` 用户写入

# ScoreBoardFile

`ScoreBoardFile` 使用 `<IfModule ...>` 容器封装在一个 `if` 条件中，如下所示：

```text
<IfModule !perchild.c>
    ScoreBoardFile logs/apache_runtime_status
</IfModule>
```

这告诉 Apache 仅当你选择非 `perchild` 的多处理模块（`MPM`）时，才将 `ScoreBoardFile` 设置为 `%ServerRoot%/logs/apache_runtime_status` 文件。因为大多数操作系统的默认 MPM 是




# 超时、保持连接、最大保持连接请求数及保持连接超时

如果 MPM 包括 Linux 是多线程而非 `perchild`，则 `if` 条件为真，Apache 将设置 `ScoreBoardFile` 指令。该指令用于指向一个文件，该文件用于在 Apache 进程之间交换运行时状态信息。如果你有内存盘，可以考虑将此文件放在内存盘中以略微提高性能。在大多数情况下，你应该保持此指令不变。

`Timeout` 设置服务器超时时间（以秒为单位）。默认值应保持原样。接下来的三个指令 `KeepAlive`、`MaxKeepAliveRequests` 和 `KeepAliveTimeout` 用于控制服务器的保持连接行为。你无需更改它们。

# IfModule 容器

Apache 将根据你选择的 MPM 使用以下三个 `<IfModule ...>` 容器之一。例如，如果你在 Linux 系统上使用默认 MPM 模式（多线程）配置 Apache，那么将使用以下 `<IfModule ...>` 容器：

```
<IfModule threaded.c>
    StartServers      3
    MaxClients        8
    MinSpareThreads   5
    MaxSpareThreads  10
    ThreadsPerChild  25
    MaxRequestsPerChild 0
</IfModule>
```

另一方面，如果你在使用 configure 脚本进行源代码配置时选择了 `--with-mpm=prefork`，那么将使用以下 `<IfModule ...>` 容器：

```
<IfModule prefork.c>
    StartServers      5
    MinSpareServers  15
    MaxSpareServers  10
    MaxClients       20
    MaxRequestsPerChild 0
</IfModule>
```

类似地，`--with-mpm=perchild` 选项强制 Apache 使用最后一个 `<IfModule ...>` 容器。

# 用于线程 MPM 行为（默认）的指令

如果你遵循了上一章中的建议，即在源代码编译期间未更改默认 MPM 行为并使用了线程行为，那么下面讨论的是你需要考虑的指令。

**注意** 如果你更改了默认 MPM，你可以在第 4 章中找到关于你选择的 MPM 所需的指令的详细信息。

## StartServers

`StartServers` 告诉 Apache 在启动时启动三个子服务器。你可以启动更多服务器，但 Apache 能够很好地根据需要基于负载增加子进程数量。因此，无需更改此指令。

## MaxClients

在默认的线程 MPM 模式下，Apache 可以处理的同时请求总数为 `MaxClients * ThreadsPerChild`。因此，由于 MaxClients 的默认值为 8，ThreadsPerChild 的默认值为 25，所以默认的同时请求最大值为 200（即 8 乘以 25）。如果你使用预叉 MPM 模式，最大请求数限制为 `MaxClients`。200 个同时请求的默认最大值对大多数站点应该运行良好，因此保持默认值。

## MinSpareThreads

`MinSpareThreads` 指令指定最小空闲线程数。这些备用线程用于处理请求，并创建新的备用线程以维护最小备用线程池大小。你可以保持默认设置不变。

## MaxSpareThreads

`MaxSpareThreads` 指令指定最大空闲线程数；保持默认值不变。在默认线程模式下，Apache 通过终止子进程来控制最小和最大线程数。

## ThreadsPerChild

此指令定义每个子进程创建的线程数。

**注意** 如果你在 Windows 系统上运行 Apache，请将 `ThreadsPerChild` 设置为你希望处理的同时请求最大数，因为在该平台上只有一个子进程，它拥有所有线程。

## MaxRequestsPerChild

全局环境的最后一个指令是 `MaxRequestsPerChild`，它设置子进程在被终止之前可以服务的请求数量。默认值 0 使子进程永远服务请求。我不喜欢默认值，因为它允许 Apache 进程在存在有缺陷的 `mod_perl` 脚本，甚至是有缺陷的第三方 Apache 模块时，缓慢消耗大量内存。因此，我倾向于将其设置为 30。

**提示** 如果你不打算运行任何第三方 Apache 模块或 `mod_perl` 脚本，你可以保持默认值，或者将其设置为合理的数字。设置为 30 确保子进程在处理 30 个请求后被终止。当然，会按需创建新的子进程。

# 配置主服务器

主服务器配置应用于 Apache 服务的默认网站。这是当你运行 Apache 并在 Web 浏览器中使用服务器 IP 地址或主机名时显示的网站。

## Port

本节中的第一个指令是 *Port* 指令，它设置 Apache 监听连接用的 TCP 端口。默认值 80 是标准 HTTP 端口。如果你将其更改为其他数字，例如 8080，你只能使用诸如 `http://hostname:8080/` 这样的 URL 访问服务器。如果服务器运行在非标准端口上，你必须在 URL 中指定端口号。

在 非标准 端口上运行 Apache 有许多原因，但我能想到的唯一好的原因是你没有权限在标准 HTTP 端口上运行 Apache。作为非 root 用户，你只能将 Apache 运行在 1024 以上的端口。

在你决定使用端口运行 Apache 后，你需要告诉 Apache 它的用户名和组名是什么。

## User 和 Group 指令

*User* 和 *Group* 指令告诉 Apache 要使用的用户（UID）和组（GID）名称。出于安全原因，这两个指令非常重要。当主 Web 服务器进程启动一个子服务器进程以响应请求时，它根据这些指令设置的值更改子进程的 UID 和 GID。参见图 3-1，查看监听连接的主 Web 服务器进程如何作为 root 用户进程运行，以及子进程如何作为不同的用户/组进程运行。如果子进程作为 root 用户进程运行，将为黑客攻击打开潜在的安全漏洞。启用与 root 用户进程交互的能力会最大化系统中潜在的安全漏洞；因此，不建议这样做。相反，我强烈建议你选择将子服务器进程作为属于权限极低的组的权限极低的用户运行。在大多数 Unix 系统中，名为 `nobody`（通常 `UID = -1`）的用户和名为 `nogroup`（通常 `GID = -1`）的组权限较低。你应该查阅你的 `/etc/group` 和 `/etc/passwd` 文件来确定这些设置。

如果你计划将主 Web 服务器作为 *非 root*（普通）用户运行，它将无法更改子进程的 UID 和 GID，因为只有 root 用户进程可以更改其他进程的 UID 或 GID。因此，如果你将主服务器作为名为 `ironseek` 的用户运行，那么所有子进程将具有与 `ironseek` 相同的权限。类似地，你拥有的任何组 ID 也将是子进程的组 ID。

**注意** 如果你计划使用数字格式表示用户和/或组 ID，你需要在数值前插入 # 符号，该数值可在 `/etc/passwd` 和 `/etc/group` 文件中找到。

## ServerAdmin

`ServerAdmin` 定义服务器生成错误页面时显示的电子邮件地址。将其设置为你自己的电子邮件地址。

## ServerName

现在你需要使用 `ServerName` 指令设置服务器的主机名。此指令默认被注释掉，因为 Apache 安装无法猜测应使用你的系统的主机名。因此，如果主机名为 `www.domain.com`，请相应地设置 `ServerName` 指令。

**注意** 但是，务必确保你在此输入的主机名具有正确的域名服务器记录，将其指向你的服务器机器。

## DocumentRoot

与其他所有 Web 服务器一样，Apache 需要知道 Web 页面存放的顶级目录的路径。此目录通常称为文档根目录。Apache 提供了一个名为 `DocumentRoot` 的指令，可用于指定顶级 Web 目录的路径。

此指令指示服务器将提供的目录作为所有文档的根目录。这是一个对你来说非常重要的决定。例如，如果该指令设置为：

```
DocumentRoot /
```

那么系统中的每个文件都将可以通过 Web 服务器访问。当然，你可以通过提供适当的文件权限设置来保护文件，但将文档根设置为系统的物理根目录绝对是重大的安全风险。相反，你应该将文档根指向文件系统的一个特定子目录。如果你在使用配置 Apache 源代码时使用了 `--prefix=/usr/local/apache` 选项，此指令将设置为：

```
DocumentRoot "/usr/local/apache/htdocs"
```

然而，一个潜在的更好选择是为你的组织创建一个 Web 目录结构。图 3-2-2 展示了我喜欢的用于多用户、多域系统的 Web 目录结构。

如图 所示，我选择创建一个名为 `/www` 的分区，在其下，每个由我的系统托管的 Web 站点都有子目录。`/www/www.mycompany.com/` 有三个子目录：`public`、`stage` 和 `development`。这些子目录中的每一个都有两个子目录：`htdocs` 和 `cgi-bin`。`htdocs` 子目录是文档根目录，而 `cgi-bin` 子目录用于 CGI 脚本。因此，`www.mycompany.com` Web 站点的 `DocumentRoot` 设置是：

```
DocumentRoot "/www/www.mycompany.com/public/htdocs"
```





![](img/e11fcbd2818a3495ac70085e5d8d1c26_72_0.png)

## 图 3-2：我首选的 Web 目录结构。

这种目录结构的优势在于它将所有的 Web 文档和应用都集中在一个分区（`/www`）下。这使得备份变得容易，并且如果需要由网络中的另一台机器提供 Web 服务，该分区可以通过网络文件系统（NFS）挂载到不同的系统上。

> 我将在第 11 章中更详细地讨论设计良好的 Web 目录结构。

请注意，即使文档根目录指向某个特定目录，这并不意味着 Web 服务器无法访问文档树之外的目录。你可以轻松通过启用符号链接（需具备适当的文件权限）或使用别名来允许其访问（别名将在下一章中讨论）。

> 从组织和管理及安全性的角度来看，我不建议大量使用符号链接或别名来访问文档树外的文件和目录。尽管如此，有时确实需要将某些类型的信息保留在文档树之外，即使你需要定期让服务器能够访问这些目录的内容。如果你必须添加指向文档树外其他目录位置的符号链接，请确保在备份文件时，你的备份程序能够正确备份这些符号链接。

## 目录容器指令

下一组指令包含在 `<Directory ... >` 容器中，如下所示：

```apache
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```

内部指令的作用范围仅限于指定的目录（及其子目录）；不过，你只能使用在目录上下文中允许的指令（你将在下一章中详细了解这些指令）。

在这里，`Options` 和 `AllowOverride` 指令适用于 `%DocumentRoot%`，即根目录（`/`）或主 Web 站点的顶层目录。由于包裹在目录容器内的指令适用于指定目录下的所有子目录，因此这些指令适用于 `%DocumentRoot%` 内的所有目录。

`Options` 指令被设置为 `FollowSymLinks`，这指示 Apache 允许自己遍历 `%DocumentRoot%` 内的任何符号链接。因为 `Options` 指令仅设置为跟随符号链接，所以 `%DocumentRoot%` 内的任何目录都不提供其他选项。实际上，`Options` 指令等效于：

```apache
Options FollowSymLinks -ExecCGI -Includes -Indexes -MultiViews
```

其他选项将在下一章的 `Options` 指令部分中解释。不过，请确保这里的核心思想是创建一个非常封闭的服务器。由于只允许遍历符号链接，因此必须根据需要按目录显式启用其他选项。从安全角度来看，这是一件非常好的事情。下一个目录容器开放了 `%DocumentRoot%` 目录，如下所示：

```apache
<Directory "/usr/local/apache/htdocs">
Options Indexes FollowSymLinks MultiViews
AllowOverride None
Order allow,deny
Allow from all
</Directory>
```

如果你的 `%DocumentRoot%` 不同，请更改指定的目录路径。以下是上述配置对 Apache 的含义：

-   指定目录及其子目录可以被索引。如果存在索引文件，将显示该文件；如果不存在索引文件，服务器将为此目录创建一个动态索引。这是由 `Options` 指令指定的。
-   指定目录及其所有子目录可以拥有服务器可以跟随（即作为路径使用）的符号链接，以访问信息。这也是由 `Options` 指令指定的。
-   指定目录及其所有子目录可以成为内容协商的一部分。`Options` 指令的 `MultiViews` 选项设置了这一点。我并不是这个选项的拥趸，但也不至于将其移除。例如，当在 `%DocumentRoot%` 目录中启用了上述显示的 `Options` 指令时，对 `http://www.domain.com/ratecard.html` 的请求可以由名为 `ratecard.html.bak`、`ratecard.bak`、`ratecard.old` 等文件响应，如果在缺少 `ratecard.html` 的情况下。这可能并非总是令人期望的行为。

此处未指定任何选项可以被本地访问控制文件（由 `httpd.conf` 中的 `AccessFileName` 指令指定；默认值为 `.htaccess`）覆盖。这是通过 `AllowOverride` 指令指定的。

`Allow` 指令在 `Deny` 指令之前进行评估。默认情况下拒绝访问。任何不匹配 `Allow` 指令或匹配 `Deny` 指令的客户端都将被拒绝访问服务器。

允许所有访问。

默认设置应该足以满足需求。

> **注意**
>
> 如果你的服务器将连接到 Internet，你可能希望从 `Options` 指令行中移除 `FollowSymLinks` 选项。保留此选项会带来潜在的安全风险。例如，如果你的 Web 站点中的某个目录没有索引页面，服务器将显示一个自动索引，其中可能包含该目录中你拥有的任何符号链接。这可能会导致敏感信息被显示，甚至可能允许任何人运行位于粗心链接的目录中的可执行文件。

## UserDir

`UserDir` 指令告诉 Apache 将 `%UserDir%` 视为每个用户 Web 站点的文档根目录（`/username/%UserDir%`）。这只有在系统中有多个用户并且希望允许每个用户拥有自己的 Web 目录时才有意义。默认设置为：

```apache
UserDir public_html
```

这意味着，如果你将 Web 服务器名称设置为 `www.yourcompany.com`，并且你有两个用户（`joe` 和 `jenny`），他们的个人 Web 站点 URL 将是：

-   `http://www.yourcompany.com/~joe` 物理目录：`~joe/public_html`
-   `http://www.yourcompany.com/~jenny` 物理目录：`~jenny/public_html`

请注意，在 Unix 系统上，`~`（波浪号）扩展为用户的主目录。`UserDir` 指令指定的目录位于每个用户的主目录中，Apache 必须具有读取和执行权限才能读取 `public_html` 目录内的文件和目录。这可以通过在 Unix 系统上使用以下命令来实现：

```bash
chown -R <user>:<Apache server's group name> ~/<user>/<directory assigned in UserDir>
chmod -R 2770 ~/<user>/<directory assigned in UserDir>
```

例如，如果用户名是 `joe`，Apache 的组名为 `httpd`，并且 `UserDir` 指令中分配了 `public_html`，则前面的命令将如下所示：

```bash
chown -R joe:httpd ~/joe/public_html
chmod -R 2770 ~/joe/public_html
```

第一个命令 `chown` 更改了 `~/joe/public_html` 目录（以及其中所有文件和子目录）的所有权为 `joe:httpd`。换句话说，它授予用户 `joe` 和组 `httpd` 对 `public_html` 目录中所有文件和目录的完整所有权。下一个命令 `chmod` 将访问权限设置为 `2770`—换句话说，只有用户（`joe`）和组（`httpd`）在 `public_html` 及其下的所有文件和子目录中具有完整的读、写和执行权限。它还确保当在 `public_html` 目录中创建新文件或子目录时，新创建的文件设置了组 ID。这使得 Web 服务器能够在无需用户干预的情况下访问新文件。

> 如果你使用脚本（如 Linux 系统上的 `/usr/sbin/adduser` 脚本）在系统上创建用户账户，你可能希望将 Web 站点创建过程整合到该脚本中。只需添加一个 `mkdir` 命令来创建默认的 `public_html` 目录（如果这是你分配给 `UserDir` 指令的目录）以创建 Web 目录。添加 `chmod` 和 `chown` 命令以授予 Web 服务器用户读取和执行此 `public` 目录下文件和目录的权限。

## DirectoryIndex

接下来，你需要配置 `DirectoryIndex` 指令，其语法如下：

```apache
DirectoryIndex [ filename1, filename2, filename3, ... ]
```

该指令指定 Apache 服务器应将哪个文件视为被请求目录的索引。例如，当请求诸如 `www.yourcompany.com/` 这样的 URL 时，Apache 服务器确定这是对 Web 站点的 `/`（文档根目录）目录的访问请求。如果 `DocumentRoot` 指令设置为：

```apache
DocumentRoot "/www/www.yourcompany.com/public/htdocs"
```




## DirectoryIndex 配置

当请求一个目录时，Apache 服务器会查找名为 `/www/www.yourcompany.com/public/htdocs/index.html` 的文件；如果找到该文件，Apache 会通过将该文件的内容返回给请求的 Web 浏览器来处理此请求。然而，如果将 `DirectoryIndex` 指定为 `welcome.html` 而不是默认的 `index.html`，Web 服务器将改为查找 `/www/www.yourcompany.com/public/htdocs/welcome.html`。如果该文件不存在，Apache 将通过创建一个动态 HTML 页面来返回目录列表。图 3-3 展示了当目录中缺少 `index.html` 时，服务器为请求的浏览器生成目录列表时的情况。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_76_0.png)

**图 3-3：** 在缺失 index.html 时的动态目录列表

你可以在 `DirectoryIndex` 指令中指定多个索引文件名。例如：

```
DirectoryIndex index.html index.htm welcome.htm
```

这告知 Web 服务器检查这三个文件中的任意一个是否存在，如果找到其中任何一个文件，就将其返回给请求的 Web 客户端。

**注意** 将许多文件列为索引可能会带来两个问题。首先，服务器现在每次目录请求都必须检查许多文件的存在；这可能会使其比平时更慢。其次，将多个文件作为索引可能会使你的网站在组织管理上难以维护。然而，如果你的 Web 站点内容开发人员使用各种系统来创建文件，同时保留 `index.html` 和 `index.htm` 作为索引文件可能是一个实用的解决方案。例如，旧版 Windows 机器无法创建扩展名超过三个字符的文件名，因此在这种机器上工作的用户可能需要手动更新 Web 服务器上该用户所有的 `index.htm` 文件。使用推荐的索引文件名可以消除这种麻烦。

## AccessFileName

`AccessFileName` 指令定义了每目录访问控制配置文件的名称。默认名称 `.htaccess` 有一个前导点，用于在 Unix 系统的普通目录列表中隐藏该文件。更改名称的唯一原因是通过晦涩性来提高安全性，但这并不是一个强有力的理由。然而，如果你确实将文件名更改为其他名称，请确保将正则表达式 `"^\\.ht"` 更改为 `"^\\.whatever"`，其中 `.whatever` 是你为 `AccessFileName` 设置值的第一个可见字符。

## Files 容器

以下 `<Files . . . >` 容器指示 Apache 禁止访问任何以 `.ht` 开头的文件（即 `.htaccess` 或 `.htpasswd`）。这对应于默认的 `#AccessFileName`。

```
<Files ~ "^\\.ht"> 
    Order allow,deny
    Deny from all
</Files>
```

## UseCanonicalName

下一个指令是 `UseCanonicalName`，设置为 `On`。它指示 Apache 使用 `$ServerName:$Port%` 格式创建所有自引用 URL。保持开启是一个好主意。

## TypesConfig

`TypesConfig` 指令指向位于默认 `conf` 目录中的 mime 配置文件 `mime.types`。除非你移动了此文件，否则无需更改它。

## DefaultType

`DefaultType` 指令为无法从文件扩展名确定 MIME 类型的任何文件设置 `Content-Type` 头。例如，如果你有一个文件 `%DocumentRoot%/myfile`，那么 Apache 使用 `%DefaultType%`（设置为 `text/plain`）作为该文件的内容类型。这意味着当 Web 浏览器请求并接收到这样的文件作为响应时，它会以显示纯文本文件的方式显示其内容。现在，如果你认为大多数未知文件内容应被视为 HTML，则使用 `text/html` 代替 `text/plain`。

# IfModule 容器

下一个 `<IfModule . . . >` 容器指示 Apache 如果存在 MIME 魔术模块（mod_mime_magic）则启用它，并使用 `%MIMEMagicFile%` 作为识别 MIME 类型文件所需的魔术信息（字节模式）。除非你想更改魔术文件的路径，否则应保留默认设置。

```
<IfModule mod_mime_magic.c>
MIMEMagicFile conf/magic
</IfModule>
```

## HostnameLookups

HostnameLookups 指令告诉 Apache 如果设置为 `On` 则对每个请求启用 DNS 查找。然而，默认设置是 `Off`，因此处理请求时不会进行 DNS 查找，这加快了响应时间。执行 DNS 查找以将 IP 地址解析为主机名对于繁忙的服务器来说是一个耗时的步骤，应该仅使用第 8 章中讨论的 logresolve 实用工具进行。请保持默认设置不变。

## ErrorLog

`ErrorLog` 指令非常重要。它指向专门用于记录服务器错误的日志文件。默认值 `logs/errors` 转换为 `%ServerRoot%/logs/error_log`，这应该适用于你，除非你想在其他位置写入日志。通常，为日志创建单独的分区是一个好主意。此外，最好让日志分区位于一个或多个专用的日志磁盘上。如果你有这样的硬件配置，你可能希望更改指令以指向新的日志路径。

## LogLevel

`LogLevel` 指令设置日志记录级别。默认值 `warn` 对于开始使用已经足够了。`LogFormat` 指令决定了记录什么以及记录格式。在大多数情况下，你可以沿用默认设置，因此在你阅读第 8 章之前，不要进行任何更改。

## CustomLog

`CustomLog` 指令设置访问日志的路径，该日志存储你的服务器命中次数。默认情况下，它使用公共日志格式（CLF），该格式由前面的 `LogFormat` 指令定义。请考虑将日志保存在独立磁盘和分区上的建议，并在必要时更改路径。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_78_0.png)

对于所有日志，无论你将在哪个目录中保存日志，一条很好的建议是确保只有主服务器进程在该目录中具有写访问权限。这是一个重大的安全问题，因为允许其他用户或进程写入日志目录可能意味着未经授权的人员可能会接管你的主 Web 服务器进程 UID，这通常是 root 账户。

## ServerSignature

下一个指令是 `ServerSignature`，它显示服务器名称和版本号，以及服务器生成的页面，如动态目录索引页、错误页等。如果你不太愿意如此轻易地向所有人显示你的服务器信息，请将其设置为 `Off`。我通常会这样做。

## Alias

**Alias** 指令定义了一个新的目录别名，将 `/icons/` 指向 `/usr/local/apache/icons/`（即 `$ServerRoot%/icons/`）。存储在此目录中的图标图像用于在找不到该目录中由 `%DirectoryIndex%` 指定的文件时显示动态目录列表。除非你更改了图标目录的路径，否则应保留该别名。跟随别名定义的目录容器设置此图标目录的权限。我不喜欢它通过设置 `Options` 为 `Indexes` 来启用目录浏览（即动态目录索引）这一想法。你应该将 `Options` 更改为 `Options -Indexes`，不要担心 `MultiViews` 选项。

## ScriptAlias

**ScriptAlias** 指令用于设置广泛使用的 CGI 脚本别名目录 `/cgi-bin/` 指向 `/usr/local/apache/cgi-bin/`（即 `$ServerRoot%/cgi-bin/`）。如果你计划从主服务器使用 CGI 脚本，请保留它；否则，请删除此指令。或者，如果你想将 CGI 脚本目录更改到另一个位置，请更改指令中给出的物理路径以匹配你的设置。

> **警告**
> 
> 切勿将 CGI 脚本路径设置到你的文档根目录内的目录中，例如 `%DocumentRoot%/somepath`，因为在文档根目录中保留 CGI 脚本会使其面临各种安全问题。将你的 CGI 脚本路径和 `DocumentRoot` 设置在同一级别。换句话说，如果你将 `DocumentRoot` 设置为 `/a/b/c/htdocs`，则将 `ScriptAlias` 设置为指向 `/a/b/c/cgi-bin`，而不是 `/a/b/c/htdocs/cgi-bin` 或 `/a/b/c/htdocs/d/cgi-bin`。

接下来，一个目录容器对 `%ScriptAlias%` 目录施加限制，以确保不允许任何目录级别的选项。这里 `Options` 指令设置为 `None`，这意味着 `%ScriptAlias%` 的内容不可浏览，并且不遵循 `%ScriptAlias%` 目录中的符号链接。

## 其余指令

其余指令——`IndexOptions`、`AddIconByEncoding`、`AddIconByType`、`AddIcon`、`DefaultIcon`、`ReadmeName`、`HeaderName`、`IndexIgnore`、`AddEncoding`、`AddLanguage`、`AddCharset`、`BrowserMatch` 和 `AddType`——对于启动运行并不重要，因此暂时忽略它们。你可以在第 4 章中了解这些指令。然而，如果有必要，你可能需要考虑更改的两个指令是：`LanguagePriority` 和 `AddDefaultCharset`。

## LanguagePriority

默认情况下，`LanguagePriority` 指令将默认语言设置为 en（英语），这可能不适用于世界各地的每个人。因此，如果受支持，你可能希望将默认语言更改为你的母语。





# AddDefaultCharset

AddDefaultCharset 应设置为最适合您本地需求的字符集。如果您不知道该使用哪种字符集，可以保留默认设置，查明应该使用的字符集，之后再修改默认值。

# 启动和停止 Apache

在您自定义了 httpd.conf 之后，就可以运行服务器了。对于本节，假设您采纳了我在上一章中的建议（即将 --prefix 设置为 /usr/local/apache）。如果您没有采纳我的建议，请确保在以下讨论中，将所有对 /usr/local/apache 的引用替换为适合您的路径。

### 启动 Apache

运行 /usr/local/apache/bin/apachectl start 命令以启动 Apache Web 服务器。如果 apachectl 报告语法错误，您应该修复 httpd.conf 文件中的错误并重试。

此外，请检查 %ErrorLog% 日志文件（即 /usr/local/apache/logs/error_log）以查找错误消息（如果有）。如果您在日志文件中看到错误，需要先修复它们。最常见的错误包括：

- 未以 root 用户身份运行服务器。您必须以 root 用户身份启动 Apache。Apache 启动后，会生成子进程，这些子进程将使用 User 和 Group 指令指定的 UID 和 GID。大多数人对这个问题感到困惑，试图使用 User 指令中指定的用户账户来启动服务器。
- Apache 抱怨无法“绑定”到某个地址。要么另一个进程已经占用了您配置 Apache 使用的端口，要么您是以普通用户身份运行 httpd 但试图使用 1024 以下的端口（例如默认端口 80）。
- 缺少日志文件路径。请确保 %ErrorLog% 和 %CustomLog% 路径存在，并且除了 Apache 服务器外，任何人都不可写。
- 配置拼写错误。每次修改 httpd.conf 配置文件时，运行 /usr/local/apache/apachectl configtest 以验证配置文件中没有语法错误。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_80_0.png)

**提示**

检查服务器是否正在运行的最快方法是尝试运行此命令：

```
ps auxx | grep httpd
```

该命令使用 ps 实用程序列出所有处于进程队列中的进程，然后将此输出管道传输到 grep 程序。grep 在输出中搜索与关键字 **httpd** 匹配的行，然后显示每个匹配的行。如果您看到一行包含 *root* 字样，那就是您的主要 Apache 服务器进程。请注意，当服务器启动时，它会创建多个子进程来处理请求。如果您以 root 用户身份启动 Apache，父进程将继续以 *root* 身份运行，而子进程则按照 *httpd.conf* 文件中的指示切换为用户。如果您在 Linux 上运行 Apache，可以创建 Listing 3-2 中显示的脚本，并将其保存在 */etc/rc.d/init.d/* 目录中。此脚本允许您在系统重启时自动启动和停止 Apache。

# 清单 3-2：httpd 脚本

```
#!/bin/sh
#
# httpd  此 shell 脚本用于启动和停止 Apache 服务器
# 它接受 'start' 或 'stop' 参数，相应地
# 启动和停止服务器进程。
#
# 注意：您可能需要更改脚本中使用的路径信息，
# 以反映您系统的配置。

APACHECTL=/usr/local/apache/bin/apachectl

[ -f $APACHECTL ] || exit 0

# 查看脚本是如何被调用的。
case "$1" in
    start)
        # 启动守护进程。
        echo -n "Starting httpd: "
        $APACHECTL start
        touch /var/lock/subsys/httpd
        echo
        ;;
    stop)
        # 停止守护进程。
        echo -n "Shutting down httpd: "
        $APACHECTL stop
        echo "done"
        rm -f /var/lock/subsys/httpd
        ;;
    *)
        echo "Usage: httpd {start|stop}"
        exit 1
esac
exit 0
```

> **提示**
>
> 要在系统启动时自动启动 Apache，只需运行一次此命令：
>
> `ln -s /etc/rc.d/init.d/httpd /etc/rc.d/rc3.d/S99httpd`
>
> 该命令在 `/etc/rc.d/rc3.d`（运行级别 3）目录中创建一个名为 `S99httpd` 的特殊链接，指向 `/etc/rc.d/init.d/httpd` 脚本。当系统启动时，该脚本将以 `start` 参数执行，从而自动启动 Apache。

### 重启 Apache

要重启 Apache 服务器，请运行 `/usr/local/apache/bin/apachectl restart` 命令。

您也可以如下使用 `kill` 命令：

```
kill -HUP `cat /usr/local/apache/logs/httpd.pid`
```

当使用 `apachectl restart` 或通过 `kill` 使用 `HUP` 信号重启时，父 Apache 进程（以 root 用户运行）会终止其所有子进程，读取配置文件，并根据需要重启新一代的子进程。

> **注意**
>
> 这种重启方式对于当时由仍存活的子进程提供服务的 Web 客户端来说是突然的。因此，您可能需要考虑使用 `apachectl` 的 `graceful` 选项代替 `restart`，以及在 `kill` 命令中使用 `WINCH` 代替 `HUP` 信号。在这两种情况下，父 Apache 进程都会通知其子进程完成当前请求，然后终止，以便它可以重新读取配置文件并重启一批新的子进程。在繁忙的站点上，这可能需要一些时间。

### 停止 Apache

您可以在系统重启时自动停止 Apache，或在任何时间手动停止它。以下部分将讨论这两种停止 Apache 的方法。

## 自动停止 Apache

要在系统重启时自动终止 Apache，请运行一次此命令：

```
ln -s /etc/rc.d/init.d/httpd /etc/rc.d/rc3.d/K99httpd
```

该命令确保在系统关闭时，以 `stop` 参数运行 `httpd` 脚本。

## 手动停止 Apache 服务器

要停止 Apache 服务器，请运行 `/usr/local/apache/bin/apachectl stop` 命令。

Apache 服务器还为您方便地查找根 Web 服务器进程的 PID。该 PID 写入分配给 `PidFile` 指令的文件中。这是主 `httpd` 进程的 PID。不要尝试手动逐个终止子进程，因为父进程会在需要时重新创建它们。停止 Apache 服务器的另一种方法是运行：

```
kill `cat /usr/local/apache/logs/httpd.pid`
```

该命令使用 `-TERM` 信号（即 -15）运行 `kill` 命令，针对由 `cat /usr/local/apache/logs/httpd.pid`（即 `cat %PidFile%`）命令返回的进程 ID。

# 测试 Apache

在启动 Apache 服务器后，请使用合适的主机名通过 Web 浏览器访问它。例如，如果您在服务器本身上运行 Web 浏览器，则使用 `http://localhost/` 访问服务器。但是，如果您想从远程主机访问服务器，请使用服务器的完全限定主机名。例如，要访问名为 `apache.pcn1td.com` 的服务器，请使用 `http://apache.pcn1td.com`。如果您将 `Port` 指令设置为非标准端口（即 80 以外的端口），请记得在 URL 中包含 `:port`。例如，`http://localhost:8080` 将访问 8080 端口上的 Apache 服务器。

如果您没有对默认的 `htdocs` 目录进行任何更改，您将看到如图 3-4 所示的页面。该页面随 Apache 发行版一起提供，需要替换为您自己的内容。

最后，您需要确保日志文件正确更新。要检查您的日志文件，请输入 `log` 目录并运行以下命令：

```
tail -f `path_to_access_log`
```

该命令中的 `tail` 部分是一个 Unix 实用程序，允许查看正在增长的文件（当指定 -f 选项时）。请确保将 `path_to_access_log` 更改为访问日志的完全限定路径名。现在，使用 Web 浏览器访问该站点；如果您已经在该站点上，只需重新加载当前在浏览器上的页面。您应该看到屏幕上添加了条目。多按几次重新加载按钮，以确保访问文件适当更新。如果您看到更新的记录，您的访问日志文件正在正常工作。按 Ctrl+C 退出 `tail` 命令会话。如果您没有看到文件中的任何新记录，应该检查日志文件及其所在目录的权限设置。





![](img/e11fcbd2818a3495ac70085e5d8d1c26_84_0.png)

**图 3-4：** 默认的 Apache 主页

另一个需要检查的日志是错误日志文件。使用：

```bash
tail -f path_to_error_log
```

命令来实时查看错误日志条目。只需在 Web 浏览器中请求不存在的资源（例如您没有的文件），您就会看到有日志条目被添加。如果您观察到有日志条目被添加，则说明错误日志文件配置正确。

如果所有这些测试都成功，那么您已成功配置了您的 Apache 服务器。恭喜！

◆   ◆   ◆

## 使用 Winnt MPM 指令配置 Apache

指令简单来说就是供 Apache 执行的命令。Apache 从第 3 章中提到的配置文件中读取指令。通过使用指令，Apache 管理员可以控制 Web 服务器的行为。Apache 提供许多指令，这使得它成为一个高度可配置的 Web 服务器。Apache 基础安装中包含的指令被称为*核心指令*。这些指令始终可用。

> **交叉引用**
>
> 标准模块（它们是 Apache 标准发行版的一部分）中也提供了其他一些指令。有关这些基于标准模块的指令的讨论将在第 5 章中进行。

本章讨论指令（核心指令及其他所有指令）适用的标准上下文，详细讲解核心指令，以及 Apache 2.0 中引入的各种多处理模块（或 *MPM*）中可用的指令。我没有按字母顺序列出所有可能的核心指令，而是根据它们的用途对它们进行了分类；类别包括一般配置；性能和资源配置；标准容器；虚拟主机特定项；日志记录；以及身份验证和安全性。每个指令描述提供以下信息：

# 第 4 章

# 本章内容

- 理解 Apache 指令上下文
- 熟悉核心指令
- 使用线程式 MPM 指令配置 Apache
- 使用预派生（prefork）MPM 指令配置 Apache
- 使用 perchild MPM 指令配置 Apache

**语法：** 显示指令名称及其接受的所有可能参数或值。

**默认设置：** 该行显示指令的默认值。仅在适用时显示。

**上下文：** 指定指令适用的上下文（或范围）。

**AllowOverride：** 在每目录访问配置文件中启用该指令所需的值（默认为 `.htaccess`）。仅在适用时显示。

本章首先介绍您可以使用指令的上下文。

> **注意**
>
> 一些指令被列出了多次；除了其中一次之外，其余所有条目都指向该指令在章节其他位置的主要讨论。这是因为有些指令不属于单一类别，我希望您能够看到查看这些类型指令的各种方式。

## Apache 指令上下文

在使用任何核心指令之前，了解指令在哪个上下文中可用非常重要；换句话说，您需要知道指令的*上下文*（或*范围*）。在讨论核心指令所需的术语之后，我将描述核心指令本身。

使用指令主要有三个上下文，包括：

- **服务器配置上下文**：指令可以出现在主服务器配置文件中的任何位置（这是所谓的），且不在任何容器（看起来非常像 HTML 标签）内部。
- **容器上下文**：指令包含在看起来如下的容器中：
  ```html
  <Container_name>
      Directive
  </Container_name>
  ```
- **每目录上下文**：指令存储在目录内的文件（通常是 `.htaccess`）中。

## 服务器配置上下文

指令可以出现在主服务器配置文件中的任何位置，且不在任何容器内部。您可以将此上下文视为全局上下文或范围；也就是说，将未包含在容器中的指令视为*全局指令*。在此上下文中适用的指令默认会影响所有其他上下文。这些指令可用于服务器配置文件中的任何位置（例如 `httpd.conf`、`srm.conf` 和 `access.conf`），但不能用于任何容器或每目录配置文件（`.htaccess`）中。

## 容器上下文

要限制指令的范围，您可以使用容器，其外观类似于 HTML 标签对。容器标签对包围一组指令，限制容器内部指令的范围。Apache 提供这些标准容器：

- `\<VirtualHost ...> ... </VirtualHost>` 用于将一个或多个指令应用于容器开始标签中指定的虚拟主机。
- `\<Directory ...> ... </Directory>` 用于将一个或多个指令应用于特定目录。请注意，如果您使用此容器标签为目录指定一个或多个指令，这些指令将自动应用于所有子目录。然而，如果这不是您想要的副作用，您可以为每个子目录创建单独的目录容器，并不同地控制服务器在目录每个子级别上的行为。
- `\<DirectoryMatch regex> ... </DirectoryMatch>` 与 `\<Directory>` 容器完全相同；然而，它接受正则表达式（*regex*）作为参数，而不是普通目录名称。例如，`<DirectoryMatch "/^\www/mydir[1-3]/"> ... </DirectoryMatch>` 匹配所有命名为 /www/mydir1、/www/mydir2 和 /www/mydir3 的目录。

> **交叉引用**
>
> 正则表达式（*regex*）通常由普通字符和特殊字符组成，以创建模式。该模式用于匹配一个或多个子字符串或整个字符串。有关正则表达式的更多信息，请参阅附录 B。

- `\<Files ...> ... </Files>` 用于将一个或多个指令应用于特定文件或文件组。
- `\<FilesMatch regex> ... </FilesMatch>` 与 `<Files>` 容器完全相同；然而它接受正则表达式（*regex*）作为参数，而不是一个或多个文件名。例如，`<FilesMatch "\.(doc|txt)$"> ... </FilesMatch>` 将把一个或多个指令应用于所有以 .doc 或 .txt 扩展名结尾的文件。
- `\<Location ...> ... </Location>` 用于将一个或多个指令应用于特定 URL。

> **注意**
>
> *URI*（*统一资源标识符*）是统一资源标识符家族的通用术语，其中 URL 只是其中一员。其他成员包括统一资源名称（URN）、统一资源特征（URC）和位置无关文件名（LIFN）。然而，只有 URL 被广泛使用。

- `\<LocationMatch regex> ... </LocationMatch>` 与 `\<Location>` 容器完全相同；然而，它接受正则表达式（*regex*）作为参数，而不是 URL。
- `\<Limit ...> ... </Limit>` 用于将一个或多个指令应用于控制对 Web 站点特定区域或特定 HTTP 请求方法的访问。此容器拥有所有容器中最窄的范围。以下是容器范围的一个示例：httpd.conf 文件的一个片段：

```html
<VirtualHost 206.171.50.50>

    ServerName www.nitec.com
    DocumentRoot "/www/nitec/public/htdocs"
    DirectoryIndex welcome.html

    <Location /secured/>
       DirectoryIndex login.html
    </Location>

</VirtualHost>
```

在这个例子中，使用 `<VirtualHost>` 容器定义了一个名为 www.nitec.com 的虚拟主机。三个指令——ServerName、DocumentRoot 和 DirectoryIndex——位于虚拟主机上下文中，因此适用于整个虚拟主机。DirectoryIndex 指令指定，如果发出请求以访问此虚拟服务器中的目录，如果可用，应返回名为 welcome.html 的文件。然而，`<Location>` 容器指定，当有人尝试访问 www.nitec.com/secured/ URL 时，应返回另一个文件 login.html。因为 `<Location>` 容器定义了更窄的范围（在 /secured 子目录中），它覆盖了 `<VirtualHost>` 容器中 DirectoryIndex 指令的更高范围。

> **注意**  定义更窄范围的容器总是覆盖具有更高范围的容器。

在使用任何容器定义 Web 空间部分的行为时，您应该牢记一些规则：

- `<VirtualHost>` 容器不能嵌套在任何类型的其他容器内。
- 最窄上下文容器 `<Limit>` 内部不能包含任何容器。
- `<Files>` 容器内部只能包含最窄的容器 `<Limit>`。
- `<Location>` 和 `<Directory>` 容器不混合使用，因此不要在一个内部使用另一个。

## 每目录上下文

您还可以在每目录配置文件中包含指令。每目录配置文件（每目录配置的默认文件名为 .htaccess）是一个文本文件，包含一个或多个仅适用于当前的


目录。这些指令也可以封装在诸如 `<Files ...>` 或 `<Limit ...>` 等容器中。通过使用每目录配置文件，你可以控制当客户端对目录中的文件发起请求时 Apache 的行为。

**注意** AllowOverride 指令允许你禁用每目录配置文件中在服务器配置或虚拟主机上下文中可被覆盖的所有或部分设置。因此，根据当前生效的覆盖设置，此上下文中的所有指令可能不会被处理。

## 通用配置指令

本节讨论的指令属于基础性质，通常同时适用于主服务器（*服务器配置上下文*）和虚拟服务器（*虚拟主机上下文*）。

### AccessFileName

AccessFileName 指令指定每目录访问控制文件的名称。默认设置（*.htaccess*）使 Apache 在每次客户端系统发起访问请求时都会查找 .htaccess 文件。

**语法：** `AccessFileName filename [filename ...]`

**默认设置：** `AccessFileName .htaccess`

**上下文：** 服务器配置，虚拟主机

例如，假设名为 www.mycompany.com 的 Apache 网站其 DocumentRoot 指令设置为 `DocumentRoot "/www/mycompany/public/htdocs"`，而 Web 浏览器请求了 `http://www.mycompany.com/feedback.html`。这将导致 Apache 搜索以下访问控制文件：

- /.htaccess
- /www/.htaccess
- /www/mycompany/.htaccess
- /www/mycompany/public/.htaccess
- /www/mycompany/public/htdocs/.htaccess

只有在检查完所有这些文件后，Apache 才会查找 *feedback.html* 文件。如果你觉得这涉及大量的磁盘 I/O，那确实如此。你可以通过使用此指令指定访问文件名来避免所有这些不必要的操作。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_90_0.png)

如果你不使用*每目录访问控制*文件，并希望 Apache 停止检查它，只需使用 `<Directory>` 指令禁用覆盖权限如下所示：

```
<Directory />
    AllowOverride None
</Directory>
```

有关更多详细信息，请参阅本章中关于 `<Directory>` 容器和 `AllowOverride` 指令的章节。

### AddDefaultCharset

`AddDefaultCharset` 指令设置 Apache 发送给浏览器的 `Content-Type` 头中的默认字符集。

**语法：** `AddDefaultCharset On | Off | charset`

**默认设置：** `AddDefaultCharset Off`

**上下文：** 全部

当启用此指令（使用 `On` 选项）时，除非你指定字符集作为该指令的第二个参数，否则 Apache 会发送 `iso-8859-1`（西欧）作为默认字符集。例如，`AddDefaultCharset On utf-8` 将发送 UTF-8 作为默认字符集。常用的字符集包括：

- `ISO-8859-1`—西欧
- `ISO-8859-15`—支持欧元货币符号的西欧
- `Windows-1252`—西欧
- `CP850`—西欧
- `UTF-8`—8 位 Unicode
- `UTF-7`—7 位 Unicode

![](img/e11fcbd2818a3495ac70085e5d8d1c26_90_1.png)

如果你的 HTML 文档通过使用 `<META http-equiv="Content-Type" content="content_type; charset=character_set_name">` 标签设置了字符集，`AddDefaultCharset` 指令允许你覆盖它。

### ContentDigest

当设置了 `ContentDigest` 指令时，它会为整个正文内容生成一个消息摘要（MD5）头，这使得 Web 客户端能够验证页面的完整性。对于 Web 服务器来说，这是一个主要的性能负担，因为 MD5 摘要需要在 Web 服务器提供的每个静态页面上进行计算。

请注意，此摘要不为除核心模块以外的任何模块生成的任何输出生成。这意味着通用网关接口（CGI）输出无法使用此功能。由于对服务器性能的影响，除非你知道服务器有足够的余力，否则不建议使用此功能。

**语法：** `ContentDigest On | Off`

**默认设置：** `ContentDigest Off`

**上下文：** 全部

### DefaultType

`DefaultType` 指令用于建立默认的 MIME 类型，这样当 Apache 收到请求一个文件类型未知的文档（换句话说，无法从服务器可用的 MIME 类型映射中确定）时，它将使用预定的默认类型。

**语法：** `DefaultType mime-type`

**默认设置：** `DefaultType text/html`

**上下文：** 全部

**覆盖：** `FileInfo`

例如，如果你有一个目录用于存储大量没有扩展名的文本文件，你可以在指向该目录的 `<Directory>` 容器内使用 `DefaultType` 指令。在这种情况下，将 `DefaultType` 设置为 `text/plain` 可以告知对端（Web 浏览器）这些是纯文本文件。以下是一个示例：

```
<Directory /www/mycompany/public/htdocs/plaindata>
    DefaultType text/plain
</Directory>
```

这里，`/www/mycompany/public/htdocs/plaindata/` 目录中的所有文件都被视为纯文本文件。

### DocumentRoot

此指令指定的 `DocumentRoot` 目录将成为 Apache 服务的所有文档的顶层目录。

**语法：** `DocumentRoot directory_path`

**默认设置：** `DocumentRoot /usr/local/apache/htdocs`

**上下文：** `服务器配置，虚拟主机`

例如，如果为服务器 www.mycompany.com 设置了 `DocumentRoot "/www/mycompany/public/htdocs"`，那么对 www.mycompany.com/corporate.html 的访问请求将促使服务器查找以下文件：
`/www/mycompany/public/htdocs/corporate.html`

如果找到该文件，它将返回给客户端（即 Web 浏览器）。

> 注意：mod_dir 模块中的一个 bug 导致当 DocumentRoot 末尾带有斜杠时出现问题（例如，DocumentRoot /usr/web/），因此你应该避免在任何指令的路径末尾输入 / 字符。

> 提示：服务器可以查找 DocumentRoot 目录之外的目录中的文件。如果你想访问 DocumentRoot 树之外的某些文件，可以使用 Alias 指令创建一个虚拟目录名称，它可以指向服务器文件系统任何位置的实际目录。

### ErrorDocument

当服务器遇到问题时，它会生成一条包含错误代码的标准错误消息。然而，这对大多数人来说并不友好，因此更希望使用定制版本的错误消息，或者可能的恢复措施。如果你需要这种定制，请使用 ErrorDocument 指令覆盖标准错误消息。

- **语法：** `ErrorDocument error_code [filename | error_message | URL]`
- **默认设置：** 无
- **上下文：** 全部
- **覆盖：** `FileInfo`

该指令需要两个参数。第一个参数是标准 HTTP 错误代码，你可以在附录 A 中找到；第二个参数是错误对应的操作项。根据需求，你可以定义希望服务器针对特定错误状态采取的操作。

例如，如果你希望为所有导致标准“文件未找到”消息的请求提供自定义消息，你只需找到该错误状态的服务器状态代码并使用 ErrorDocument 指令即可。由于缺少文件的服务器状态代码为 404，以下指令设置可让 Apache 显示自定义消息：

```
ErrorDocument 404 "Sorry, this is an invalid request because %s "
```

请注意，整个消息被引号包围，服务器会用有关错误的可用信息替换 %s。然而，如果你觉得这有点限制，可以使用文件作为错误消息响应。例如：

```
ErrorDocument 404 /errors/404.html
```

每当发生文件缺失错误时，位于 DocumentRoot 目录下 errors 目录中的 404.html 文件将返回给客户端（Web 浏览器）。

如果你希望做的不仅仅是返回一个静态页面，你可以使用 CGI 脚本来执行某些特定操作。在这种情况下，你用调用 CGI 脚本替换文件名：

```
ErrorDocument 404 /cgi-bin/missingurl.cgi
```

每当发生 404 错误时，这会调用名为 missingurl.cgi 的 CGI 脚本。你也可以使用 URL 而不是文件名将客户端重定向到另一个网站：

```
ErrorDocument 404 http://www.newsite.com/we.moved.html
```

这可以用于页面或整个网站已迁移到另一位置的情况。

如果发生错误 401（未授权），你不能将客户端指向远程服务器。此指令的值必须是本地文件或消息。

### <IfDefine>

IfDefine 容器指令允许你创建条件配置。特殊命令行参数选项通过在与 httpd 程序一起使用 `-D` 选项来指定。

**语法：** `<IfDefine [!]special_command_line_param> ... </IfDefine>`

**默认设置：** 无

**上下文：** 全部

例如，如果你从 bin 目录运行 Apache 服务器，命令为 `./httpd -D something`，则可以使用：

```
<IfDefine something>
# #directives that should be executed only when
# -D something is specified
</IfDefine>
```

在特殊命令行参数前放置 ! 字符告诉 Apache 仅在命令行中未找到 -D something 时处理 IfDefine 容器内的指令。例如：

```
<IfDefine !something>
# directives that should be executed only when
# -D something is NOT specified
</IfDefine>
```




## <IfModule>

如果某些指令来自可能并不存在于你的 Apache 安装环境中的自定义模块，请使用 `IfModule` 容器指令。

- **语法：** `<IfModule [!]module_name> ... </IfModule>`
- **默认设置：** 无
- **上下文：** 全部

例如，如果你只想在某个模块可用时才使用某些指令，可以使用以下条件结构：

```
<IfModule module_name>
   # 如果该模块是 Apache 的一部分，则为以下指令分配相应的值
   # 在此处放置你的指令。
</IfModule>
```

其中，`module_name` 参数是该模块在编译时的文件名（例如，mod_rewrite.c）。

如果你需要一个与上述逻辑完全相反的条件语句，只需在模块名前插入一个 !（感叹号或bang）即可。`<IfModule>` 区域可以嵌套；这是一种可用于实现简单多模块条件测试的方法。例如：

```
<IfModule module_A>
   # 如果模块 A 是
   # Apache 的一部分，则在此处理指令

   <IfModule module_B>

      # 仅当模块 A 和 B 都是
      # Apache 的一部分时才进入此处

      <IfModule ! module_C>

         # 仅当模块 A 和 B 存在
         # 但模块 C 不是 Apache 的一部分时才进入此处
      </IfModule>

   </IfModule>
</IfModule>
```

## Include

Include 指令允许你将外部文件包含为配置文件。

- **语法：** `Include fileName`
- **默认设置：** 无
- **上下文：** 服务器配置

例如，如果你想使用外部文件来加载所有的虚拟主机配置，可以在 httpd.conf 中拥有以下配置：

```
NameVirtualHost IP_Address
Include virtual_host_1.conf
Include virtual_host_2.conf
Include virtual_host_3.conf
...
Include virtual_host_N.conf
```

在这些文件中的每一个，你都可以定义特定于该主机的 `<VirtualHost>` 容器。如果你有很多虚拟主机，这是组织 httpd.conf 文件的好方法。

## Options

Options 指令控制特定目录中可用的服务器功能。

- **语法：** `Options [+] [-]Option [+] [-]Option ...`
- **默认设置：** 无
- **上下文：** 全部
- **覆盖：** Options（见表 4-1）

当此指令设置为 `None` 时，该指令使用的上下文中不会启用任何额外功能。

此指令的所有可能设置都列在表 4-1 中。

**表 4-1: Options 指令设置**

| 设置 | 含义 |
| :--- | :--- |
| None | 无选项。 |
| All | 除 MultiViews 外的所有选项。 |
| ExecCGi | 允许执行 CGI 脚本。 |
| FollowSymLinks | 服务器跟随目录中的符号链接。但是，服务器不会更改用于与 `<Directory>` 部分进行匹配的路径名。 |
| Includes | 允许 SSI 命令。 |
| IncludesNOEXEC | 可以在 SSI 页面中嵌入一组受限制的 SSI 命令。不被允许的 SSI 命令是 `#exec` 和 `#include`。 |
| Indexes | 如果请求的 URL 映射到一个目录，且该目录中没有 DirectoryIndex（例如，index.html），则服务器返回目录的格式化列表。 |
| SymLinksIfOwnerMatch | 服务器仅跟随目标文件或目录的所有者与链接所有者相同的符号链接。 |
| MultiViews | 基于文档语言启用内容协商。 |

在 Options 指令中，使用 + 和 - 号来启用或禁用某个选项。例如，以下配置片段展示了单个配置文件（如 access.conf）中的两个目录容器：

```
<Directory /www/myclient/public/htdocs >
Options Indexes MultiViews
</Directory>

<Directory /www/myclient/public/htdocs>
Options Includes
</Directory>
```

/www/myclient/public/htdocs 将只设置 Includes 选项。然而，如果第二个 `<Directory>` 部分如下使用 + 和 - 号：

```
<Directory /www/myclient/public/htdocs>
Options +Includes -Indexes
</Directory>
```

则指定的目录将设置 MultiViews 和 Includes 选项。当应用多个 Options 时，请注意，最窄的上下文始终优先于较宽的上下文。例如：

```
ServerName www.domain.com

Options ExecCGI Includes

<VirtualHost 11.22.33.11.22.33.1.>
    ServerName www.myclient.com
    Options -ExecCGI -Includes

    <Directory /www/myclient/public/htdocs/ssi >
        Options Includes
    </Directory>

</VirtualHost>
```

在此示例中，主服务器通过将 `Options` 指令设置为 ExecCGI 和 Includes 来启用 CGI 执行和 SSI。虚拟主机 www.myclient.com 禁用了这两个选项，在其自身的 Options 指令中使用了 -ExecCGI 和 -Includes 设置。最后，该虚拟主机为 /www/myclient/public/htdocs/ssi 目录有另一个 Options 指令，用于启用 SSI 执行。请注意，Includes 是为 /www/myclient/public/htdocs/ssi 目录设置的唯一选项。

如你所见，如果 `Options` 指令使用 + 或 - 号，则值将被添加或从当前 `Options` 列表中减去。另一方面，如果 `Options` 指令不使用相对的 + 或 - 号，则该容器的值将完全覆盖之前的任何 `Options` 指令。

## Port

`Port` 指令为某个主机分配 0 到 65535 范围内的端口号。如果没有指定端口号的 `Listen` 或 `BindAddress` 指令，`Port` 指令将设置服务器监听的网络端口。如果有任何 `Listen` 或 `BindAddress` 指令指定了端口号，则 `Port` 指令对服务器监听地址没有影响。`Port` 指令设置 `SERVER_PORT` 环境变量（用于 CGI 和服务器端包含 (SSI)），并在服务器必须生成引用自身的 URL 时使用。

**语法：** `Port number`

**默认设置：** `Port 80`

**上下文：** 服务器配置

虽然你可以指定 0 到 65535 之间的端口号，但有一项限制你应该记住。1024 以下的所有端口号都保留给标准服务，如 TELNET、SMTP、POP3、HTTP 和 FTP。你可以在 `/etc/services` 文件中找到分配给标准服务的所有端口号。

或者，为了安全起见，为你的 Apache 服务器使用除 80 以外的任何端口号（例如使用高地址，如 8000）。

> **注意** 如果你是非 root 用户，并希望出于实验或其他高尚目的运行 Apache，你需要使用高于 1024 的端口，因为只有 root 用户才能在这些受限端口上运行 Apache 等服务。

> **提示** `<VirtualHost>` 容器也可以用于设置虚拟主机使用的端口。

## ServerAdmin

`ServerAdmin` 指令分配一个电子邮件地址，该地址会与服务器发出的许多错误消息一起显示。如果你托管了大量虚拟网站，你可能希望为每个虚拟主机使用不同的电子邮件地址，以便立即确定报告问题的用户指的是哪个服务器。

- **语法：** `ServerAdmin e-mail_address`
- **默认设置：** 无
- **上下文：** 服务器配置，虚拟主机

为了给你的虚拟网站应有的专业外观和感觉，请勿使用不包含虚拟网站作为地址主机部分的电子邮件地址。例如，如果你的公司是一家名为 mycompany.net 的互联网服务提供商 (ISP)，并且你有一个名为 www.myclient.com 的客户网站，请将 www.myclient.com 网站的 `ServerAdmin` 设置为 user@myclient.com 地址（如 webmaster@myclient.com），而不是 webmaster@mycompany.net。这样，当服务器向访问 www.myclient.com 的人显示错误消息时，访问者将看到属于 myclient.com 的电子邮件地址。这被认为更具专业性。

## ServerName

`ServerName` 指令设置服务器的主机名。当未使用此指令时，Apache 会尝试在启动时通过执行域名服务器 (DNS) 请求来确定主机名。然而，根据你的 DNS 设置，这可能不理想，因为 Apache 执行的查找可能会为你的服务器选择一个不期望的名称，例如，如果你的服务器有规范名称记录 (CNAME)。因此，最好将其设置为你喜欢的任何主机名。

- **语法：** `ServerName fully_qualified_domain_name`
- **默认设置：** 无
- **上下文：** 服务器配置，虚拟主机




**提示**

请确保输入完全限定的**域名**，而不仅仅是简写。例如，如果你的主机名为`wormhole.mycompany.com`，你不应该将`ServerName`设置为`wormhole`。有效的选择是：

```
ServerName wormhole.mycompany.com
```

## ServerRoot

`ServerRoot` 指令用于设置服务器文件所在的目录。请勿将其与 `DocumentRoot` 指令混淆，后者用于将服务器指向您的 Web 内容。`ServerRoot` 目录用于定位所有服务器配置文件和日志文件。标准发行版在 `ServerRoot` 目录下包含 `conf`、`bin`、`htdocs`、`icons`、`cgi-bin` 和 `logs` 目录。但是，如果您未指定 `ServerRoot` 指令，可以使用 `-d` 命令行选项告诉 Apache 您的 `ServerRoot` 目录位置。

语法：`ServerRoot directory`

默认设置：`ServerRoot /usr/local/apache`

上下文：Server config

## ServerSignature

通过使用 `ServerSignature` 指令，您可以为 Apache 生成的页面（如错误消息和目录列表）创建一个简单的页脚。除非您将 Apache 用作代理服务器，否则不建议使用此指令。另一方面，当用户收到错误消息时，如果用户的网络路径中存在一系列代理，通常很难确定是哪个代理服务器导致了该错误。在这种情况下，此页脚作为一个标识符。您可以在页脚中包含一个电子邮件地址，这样如果有问题，其他人就可以通过电子邮件联系您。

语法：`ServerSignature On | Off | e-mail`

默认设置：`ServerSignature Off`

上下文：All

## ServerTokens

在响应请求时，Apache 可以发送一个包含标识符的**头部**，该标识符告诉客户端您正在运行哪种服务器。`ServerTokens` 指令允许您控制该标识符标记。当使用 `Minimal` 选项时，Apache 发送 "Apache/version"；当使用 `ProductOnly` 选项时，仅发送字符串 "Apache"；当使用 `OS` 时，发送 "Apache/version (OS_Type)"；当使用 `Full` 时，Apache 发送 "Apache/version (OS_Type) _Available_Module_Info_"。

语法：`ServerTokens` `Minimal` | `ProductOnly` | `OS` | `Full`

默认设置：`ServerTokens` `Full`

上下文：Server config

![](img/e11fcbd2818a3495ac70085e5d8d1c26_100_0.png)

> 如果您希望避免基于漏洞的攻击带来的安全问题，我建议您仅使用 `Minimal` 选项；您不希望向外界宣扬您使用的服务器类型。

## SetInputFilter

`SetInputFilter` 指令设置用于处理发送到服务器的请求的过滤器。这些过滤器按照它们在此指令中出现的顺序应用。

语法：`SetInputFilter` `filter` [`filter` ...]

默认设置：无

上下文：Directory

## SetOutputFilter

`SetOutputFilter` 指令设置用于在响应发送到 Web 客户端之前处理响应的过滤器。这些过滤器按照它们在此指令中出现的顺序应用。

语法：`SetOutputFilter` `filter` [`filter`] ...

默认设置：无

上下文：Directory

在下面的示例中，`/www/mysite/htdocs/parsed` 目录中的所有文件都将使用 `INCLUDES` 输出过滤器进行处理，即 SSI 过滤器：

```
<Directory "/www/mysite/htdocs/parsed">
    Options +Includes
    SetOutputFilter INCLUDES
</Directory>
```

## 性能和资源配置指令

这些指令允许您对 Apache 进行微调，以实现更高的性能和更好的控制。您可以从许多方面对 Apache 进程进行微调。请注意，几乎所有这些指令都需要您对系统如何在操作系统、硬件等方面运行有清晰的理解；因此，您应该浏览操作系统手册和/或 `man` 页面，以了解您的系统如何限制进程的系统资源，如何控制 TCP/IP 连接等。本部分的指令进一步划分为子功能。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_101_0.png)

有关如何加速 Apache 的更多信息，请参阅第 22 章。

### 控制 Apache 进程

以下指令用于控制 Apache 在您的系统中的执行方式。使用这些指令，您可以控制 Apache 在系统中使用资源的方式。例如，您可以决定在系统中运行多少个子服务器进程，或者在 Windows 平台上允许 Apache 使用多少线程。在配置这些指令时，请记住以下几点：

- 运行的进程越多，您的 CPU 经历的负载越大。
- 运行的进程越多，所需的 RAM 越多。
- 运行的进程越多，使用的操作系统资源（如文件描述符和共享缓冲区）就越多。

当然，更多的进程也可能意味着服务更多的请求，从而为您带来更高的站点访问量。因此，设置这些指令应基于实验、需求和可用资源的结合。

#### ListenBacklog

请参阅“MPM 线程特定指令”部分下的 ListenBacklog 指令。

#### MaxClients

请参阅“MPM 线程特定指令”部分下的 `MaxClients` 指令。

#### MaxRequestsPerChild

请参阅“MPM 线程特定指令”部分下的 `MaxRequestsPerChild` 指令。

#### MaxSpareServers

请参阅“MPM prefork 特定指令”部分下的 `MaxSpareServers` 指令。

#### MinSpareServers

请参阅“MPM prefork 特定指令”部分下的 `MinSpareServers` 指令。

#### SendBufferSize

请参阅“MPM 线程特定指令”部分下的 `SendBufferSize` 指令。

#### StartServers

请参阅“MPM 线程特定指令”部分下的 `StartServers` 指令。

#### TimeOut

Apache 服务器响应的请求。请求和响应通过数据包传输。Apache 必须知道等待特定数据包的时长。`TimeOut` 指令允许您以秒为单位配置时间。这里指定的时间是 Apache 断开连接前的最大等待时间。默认设置允许 Apache 在断开与客户端的连接之前等待 300 秒。但是，如果您处于慢速网络环境中，您可能希望增加超时值以减少断开的次数。

- **语法：** `TimeOut number`
- **默认设置：** `TimeOut 300`
- **上下文：** Server config

目前，此 `TimeOut` 设置适用于：

- 接收 GET 请求所需的总时间。
- POST 或 PUT 请求中 TCP 数据包接收之间的时间。
- 响应中 TCP 数据包传输的 ACK 之间的时间。

#### 建立持久连接

通过使用本节讨论的 `KeepAlive` 指令，您可以指示 Apache 使用持久连接，以便单个 TCP 连接可用于多个事务。通常，每个 HTTP 请求和响应都使用单独的连接。这意味着每次服务器收到请求时，它都会打开一个连接来获取请求，然后关闭该连接。服务器收到请求后，它会打开另一个 TCP 连接进行响应，并在完成服务后最终关闭连接。这种方法增加了高性能的开销。重复使用单个连接进行多个事务减少了反复建立和关闭 TCP 连接所需的开销，从而提高性能。

但是，要建立持久连接，服务器和客户端都必须具备持久连接功能。大多数流行的浏览器，如 Netscape Navigator 和 Microsoft Internet Explorer，都内置了 `KeepAlive` 功能。

并非所有事务都能利用持久连接。持久连接的一个要求是正在传输的资源必须具有已知的大小。由于许多 CGI 脚本、SSI 命令和其他动态生成的内容在传输前没有已知长度，因此它们无法利用此功能。

### KeepAlive

KeepAlive 指令允许您启用/禁用 Apache 中 TCP 连接的持久使用。

- 语法：KeepAlive On | Off
- 默认设置：KeepAlive On
- 上下文：Server config

旧版 Apache 服务器（1.2 版本之前）在使用 KeepAlive 时可能需要数值而不是 On/Off。此值对应于您希望 Apache 在每个请求中处理的最大请求数。实施限制是为了防止客户端占用您所有的服务器资源。要在旧版 Apache 中禁用 KeepAlive，请使用 0（零）作为值。

### KeepAliveTimeout

如果将 KeepAlive 指令设置为 on，您可以使用 KeepAliveTimeout 指令来限制在关闭连接之前，Apache 等待后续请求的秒数。收到请求后，应用由 Timeout 指令指定的超时值。

- 语法：KeepAliveTimeout seconds
- 默认设置：KeepAliveTimeout 15
- 上下文：Server config

### MaxKeepAliveRequests

MaxKeepAliveRequests 指令限制了 KeepAlive 开启时每个连接允许的请求数。如果设置为 0（零），则允许无限请求。我建议您将此设置保持在较高值，以获得最大的服务器性能。

- 语法：MaxKeepAliveRequests number
- 默认设置：MaxKeepAliveRequests 100
- 上下文：Server config




## 控制系统资源

Apache 提供了相当灵活的机制，允许你控制其消耗的系统资源量（如 CPU 时间和内存）。这些控制功能对于提高 Web 服务器系统的可靠性和响应能力非常有用。许多典型的黑客攻击尝试让 Web 服务器像猪一样消耗所有系统资源，从而使系统失去响应甚至几乎停止运行。Apache 提供了一组指令来应对这种情况。以下章节将讨论这些指令。

## RLimitCPU

RLimitCPU 指令允许你控制 Apache 派生的子进程（如 CGI 脚本）的 CPU 使用情况。该限制不适用于 Apache 子进程本身或由父 Apache 服务器创建的任何进程。

**语法：** RLimitCPU n [ 'max' [ n [ 'max']]

**默认设置：** 未设置；使用操作系统默认值

**上下文：** 服务器配置，虚拟主机

RLimitCPU 指令接受以下两个参数：第一个参数为所有进程设置软资源限制，第二个参数（可选）设置最大资源限制。请注意，提高最大资源限制要求服务器以 root 身份运行或处于初始启动阶段。对于这两个参数中的每一个，都有两个可能的值：

- *n* 是每个进程的秒数
- *max* 是操作系统允许的最大资源限制。

## RLimitMEM

RLimitMEM 指令限制 Apache 派生的子进程（如 CGI 脚本）的内存（RAM）使用情况。该限制不适用于 Apache 子进程本身或由父 Apache 服务器创建的任何进程。

**语法：** RLimitMEM n [ 'max' [ n [ 'max']]

**默认设置：** 未设置；使用操作系统默认值

**上下文：** 服务器配置，虚拟主机

RLimitMEM 指令接受两个参数。第一个参数为所有进程设置软资源限制，第二个参数（可选）设置最大资源限制。请注意，提高最大资源限制要求服务器由 root 用户启动。对于这两个参数中的每一个，都有两个可能的值：

- *n* 是每个进程的字节数
- *max* 是操作系统允许的最大资源限制

## RLimitPROC

`RLimitPROC` 指令设置每个用户 ID 允许的最大同时运行的 Apache 派生进程数。

**语法：** `RLimitPROC n [ 'max' [ n | 'max'] ]`

**默认设置：** 未设置；使用操作系统默认值

**上下文：** 服务器配置，虚拟主机

`RLimitPROC` 指令接受两个参数。第一个参数为所有进程设置软资源限制，第二个参数（可选）设置最大资源限制。提高最大资源限制要求服务器以 *root* 身份运行或处于初始启动阶段。对于这两个参数中的每一个，都有两个可能的值：

- *n* 是每个用户的进程数
- *max* 是操作系统允许的最大资源限制

> **注意**
> 如果你的 CGI 进程与服务器进程使用相同的用户 ID 运行，使用 `RLimitPROC` 将限制服务器可以启动（或“fork”）的进程数。如果限制过低，你将看到错误日志文件中出现“无法 fork 进程”类型的消息。在这种情况下，你应该增加限制或保持默认设置。

## UseCanonicalName

`UseCanonicalName` 指令设置 Apache 如何构建自引用 URL。当设置为 `on` 时，Apache 使用 *ServerName* 和 *Port* 指令设置来创建自引用 URL。如果 `UseCanonicalName` 设置为 `off`，则 Apache 使用客户端提供的 *主机名* 和 *端口号*（来自报头信息）来构建自引用 URL。最后，如果 `UseCanonicalName` 设置为 `dns`，Apache 将对服务器的 IP 地址执行反向 DNS 查找，以确定自引用 URL 的主机名。由于反向 DNS 查找会减慢请求处理速度，因此不推荐此选项。

**语法：** `UseCanonicalName On | Off | dns`

**默认设置：** `UseCanonicalName On`

**上下文：** 服务器配置，虚拟主机，目录

**重写：** Options

## 使用动态模块

Apache 在启动时加载所有预编译模块；然而，它也提供了动态模块加载和卸载功能，这在某些情况下可能很有用。当你使用以下动态模块指令时，可以在不重新编译服务器的情况下更改活动模块列表。

## AddModule

AddModule 指令可用于启用当前未活动的预编译模块。服务器可能包含已编译但未主动使用的模块。此指令可用于启用这些模块。服务器自带一个预加载的活动模块列表；可以使用 ClearModuleList 指令清除此列表。然后可以使用 AddModule 指令添加新模块。

- **语法：** AddModule module module ...
- **默认设置：** 无
- **上下文：** 服务器配置

## ClearModuleList

你可以使用 ClearModuleList 指令清除活动模块列表并启用动态模块加载功能。然后使用 AddModule 指令添加你想激活的模块。

- **语法：** ClearModuleList
- **默认设置：** 无
- **上下文：** 服务器配置

## 标准容器指令

本节讨论构成基础 Apache 服务器一部分的标准容器。这些容器广泛用于将一组其他指令应用于特定目录、文件或位置。你不能随意混合使用这些容器。

处理这些指令的一般准则是：

- 使用 `<Directory>` 或 `<Files>` 容器来指定针对文件系统对象（如文件和目录）的指令。你不能在 .htaccess 文件中使用 `<Directory>`，因为 .htaccess 文件仅适用于其所在的目录。
- 使用 `<Location>` 容器来匹配 URL 对象。你不能在 .htaccess 文件中使用此指令。
- 当使用指令的正则表达式版本（例如 `<DirectoryMatch>`）时，请遵循与常规版本相同的准则。仅当你确信你的正则表达式表达紧凑时才使用容器的正则表达式版本。
- 由于 Apache 开发早期阶段的一个错误，代理控制仍然使用 `<Directory>` 容器进行，尽管 `<Location>` 容器更为合适。这可能在未来版本中得到修正。然而，这实际上不会造成任何伤害，除了使概念化稍微困难一些。

`<VirtualHost>` 容器将在本章后面的单独章节中讨论。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_107_0.png)

## <Directory>

`<Directory>` 和 `</Directory>` 容器标签用于包围一组仅应用于命名目录及其子目录的指令。可以在目录上下文中允许的任何指令都可以使用。参数可以是完全限定路径名。

**语法：** `<Directory directory>` ... `</Directory>`

**默认设置：** 无

**上下文：** 服务器配置，虚拟主机

在以下示例中，目录 `/www/mycompany/public/htdocs/download` 作为完全限定路径名使用。此示例在此目录中启用了目录索引。

```
<Directory /www/mycompany/public/htdocs/download>
Options +Indexes
</Directory>
```

你也可以在指定路径时使用通配符。在以下示例中，`?` 将匹配任何单个字符：

```
<Directory /www/mycompany/public/htdocs/downloa?>
Options +Indexes
</Directory>
```

因此，诸如 `/www/mycompany/public/htdocs/download` 和 `/www/mycompany/public/htdocs/downloa` 这样的目录将被匹配。你还可以使用 `*`（星号）来匹配 `/`（斜杠）字符以外的任何字符序列。还可以通过添加 `~`（波浪号）字符来使用扩展正则表达式。例如：

```
<Directory ~ "^/www/.*/">
```

将匹配 `/www/` 下的任何子目录。请注意，基于正则表达式的 `<Directory>` 容器可能必须等到所有常规（即不使用正则表达式的）`<Directory>` 容器和 `.htaccess` 文件应用后才生效。





然后，所有正则表达式将按照其在配置文件中出现的顺序进行测试。

> 提示
>
> 有关正则表达式的详细解释，请参见附录 C。

如果您为同一目录空间指定了多个 `<Directory>` 容器，则应用范围最窄的 `<Directory>` 容器将优先生效。例如：

```apache
<Directory /www>
    AllowOverride None
</Directory>
<Directory - "/www/mycompany/public/htdocs/*">
    AllowOverride FileInfo
</Directory>
```

根据此配置，当一个**针对** `/www/mycompany/public/htdocs/somefile.cvs` 的**请求到达**时，Apache 会禁用 `/www` 的每目录访问控制文件（*.htaccess*），**然后启用** `/www/mycompany/public/htdocs` 的控制文件。**它还会接受** 来自 `/www/mycompany/public/htdocs/.htaccess` **文件内的任何** `FileInfo` **指令，例如** `DefaultType`。

## `<DirectoryMatch>`

`DirectoryMatch` 容器与 `<Directory>` 容器几乎相同，只不过它接受正则表达式作为参数，并且不需要 `-`（连字符）：使用 `<DirectoryMatch>` 和 `</DirectoryMatch>` 包围一组仅应用于指定目录及其子目录的指令。

- **语法：** `<DirectoryMatch regex> ... </DirectoryMatch>`
- **默认设置：** 无
- **上下文：** 服务器配置，虚拟主机

以下示例将匹配 `/www/mycompany/public/htdocs` 下名称恰好由八个大写字母组成的所有子目录；因此，`/www/mycompany/public/htdocs/AAAABBBB/` 将匹配上述正则表达式。

```apache
<DirectoryMatch "^/www/mycompany/public/htdocs/[A-Z]{8}|/*">
```

> 交叉参考
>
> 有关正则表达式的更多细节，请参见附录 B。

## `<Files>`

为了通过文件名控制访问，您需要使用 Files 容器。`<Files>` 部分将按照其在配置文件中出现的顺序进行处理，这在读取 `<Directory>` 部分和 .htaccess 文件之后，但在读取 `<Location>` 部分之前发生。

- **语法：** `<Files filename> ... </Files>`
- **默认设置：** 无
- **上下文：** 服务器配置，虚拟主机，每目录

*filename*（文件名）参数应包含一个文件名或通配符字符串，其中 `?` 匹配任意单个字符，`*` 匹配除 `/` 字符外的任意字符序列。通过使用 `~`（波浪线）字符，您可以启用对参数的扩展正则表达式检查。例如：

```apache
<Files "\.(zip|tar|tgz|arj|zoo)$">
```

这将匹配任何扩展名为 .zip、.tar、.tgz、.arj 或 .zoo 的文件。与 `<Directory>` 和 `<Location>` 部分不同，`<Files>` 部分可以用于 .htaccess 文件中。当在 .htaccess 文件内使用这些配置时，您无需添加路径名，因为 .htaccess 文件仅适用于其所在的目录。

## `<FilesMatch>`

`FilesMatch` 容器与 `<Files>` 容器完全相同，只不过它接受正则表达式作为参数。

- **语法：** `<FilesMatch regex> ... </FilesMatch>`
- **默认设置：** 无
- **上下文：** 服务器配置，虚拟主机，每目录

例如，以下示例将匹配任何扩展名为 .zip、.tar、.tgz、.arj 和 .zoo 的文件。请注意，在这个容器中使用正则表达式时，不需要使用 `~`（波浪线）字符：

```apache
<FilesMatch "\.(zip|tar|tgz|arj|zoo)$">
```

## `<Location>`

`<Location>` 容器提供基于 URL 的访问控制。`<Location>` 容器将按照其在配置文件中出现的顺序进行处理，这在读取 `<Directory>` 容器和 .htaccess 文件之后发生。

- **语法：** `<Location URL> ... </Location>`
- **默认设置：** 无
- **上下文：** 服务器，虚拟主机

URL 参数不需要 `http://servername`。它可以使用通配符字符，例如 `?`（匹配任意单个字符）或 `*`（匹配除 `/` 字符外的任意字符序列）。您也可以在表达式前使用 `~`（波浪线）字符来使用扩展正则表达式。例如，`<Location ~ "/(my|your)/file">` 将匹配诸如 `/my/file` 或 `/your/file` 等 URL。

## `<LocationMatch>`

`LocationMatch` 容器与 `<Location>` 容器相同，只不过其参数（URL）是一个正则表达式，并且不需要在表达式前加 `~`（波浪线）。例如，`<LocationMatch "/(my|your)/file">` 将匹配诸如 `/my/file` 或 `/your/file` 等 URL。

- **语法：** `<LocationMatch *regex*> ... </LocationMatch>`
- **默认设置：** 无
- **上下文：** 服务器配置，虚拟主机

## 虚拟主机特定指令

这些指令用于创建虚拟主机。默认情况下，Apache 仅由 `ServerName` 指令指定的 Web 站点主机提供服务。然而，可以使用虚拟主机容器指令使 Apache 为其他 Web 站点提供服务。请注意，我之前在“通用配置指令”部分讨论的许多指令也适用于虚拟主机。

### `NameVirtualHost`

如果您计划使用基于名称的虚拟主机，则需要使用 `NameVirtualHost` 指令。虽然 `addr` 可以是主机名，但我建议您始终使用 IP 地址。

- **语法：** `NameVirtualHost *addr[:port]*`
- **默认设置：** 无
- **上下文：** 服务器配置

例如，对于名为 `www.mycompany.com` 且使用 IP 地址 192.168.1.200 的虚拟主机，该指令和虚拟主机定义如下：

```apache
NameVirtualHost 192.168.1.200
<VirtualHost 192.168.1.200>
  ServerName www.mycompany.com
  # Other directives go here
</VirtualHost>
```

如果您在多个地址上拥有多个基于名称的主机，请为每个地址重复该指令。在清单 4-1 中，第一个 `NameVirtualHost` 指令用于 `www.mycompany.com` 和 `www.friendscompany.com` 虚拟主机。第二个容器用于 `www.myclient.com` 和 `www.herclient.com` 虚拟主机。

**清单 4-1：NameVirtualHost 指令**

```apache
NameVirtualHost 192.168.1.200
#
# First virtual host that corresponds to the above directive
#
<VirtualHost 192.168.1.200>
    ServerName www.mycompany.com
    # Other directives go here
</VirtualHost>
#
# Second virtual host that corresponds to the above directive
#
<VirtualHost 192.168.1.200>
    ServerName www.friendscompany.com
    # Other directives go here
</VirtualHost>
#
# Another NameVirtualHost directive for a new set
# of name-based virtual hosts that
# use a different IP.
NameVirtualHost 192.168.1.100
#
# First virtual host that corresponds to 192.168.1.100
#
<VirtualHost 192.168.1.100>
    ServerName www.myclient.com
    # Other directives go here
</VirtualHost>
#
# Second virtual host that corresponds to 192.168.1.100
#
<VirtualHost 192.168.1.100>
    ServerName www.herclient.com
    # Other directives go here
</VirtualHost>
```

可选地，您可以指定基于名称的虚拟主机应使用的端口号。例如：

```apache
NameVirtualHost 192.168.1.100:8080
```

### `ServerAlias`

此指令允许您为服务器的主主机名定义别名。当您拥有一个具有多个 IP 名称（DNS 数据库中的 CNAME 记录）的基于名称的虚拟主机时，您可以使用单个虚拟主机定义来服务所有这些名称。

- **语法：** `ServerAlias host1 [host2 ...]`
- **默认设置：** 无
- **上下文：** 虚拟主机

在以下示例中，`www.sac-state.edu` 和 `www.csu.sacramento.edu` 是 `www.csus.edu` 虚拟主机的别名。

```apache
NameVirtualHost 192.168.1.100

<VirtualHost 192.168.1.100>
  ServerName www.csus.edu
  ServerAlias www.sac-state.edu www.hornerd.edu
</VirtualHost>
```

> 提示：在定义别名时，您也可以使用诸如 `*` 等通配符字符。

### `ServerPath`

`ServerPath` 指令为主机设置遗留的 URL 路径名称，用于基于名称的虚拟主机。通常，这用于支持不符合 HTTP 1.1 标准的浏览器。

- **语法：** `ServerPath pathname`
- **默认设置：** 无
- **上下文：** 虚拟主机

### `<VirtualHost>`

`VirtualHost` 容器指令指定虚拟主机配置。在 `<VirtualHost>` 和结束标签 `</VirtualHost>` 内部发现的所有包围指令仅应用于指定的虚拟主机。任何允许在虚拟主机上下文中使用的指令都可以使用。当服务器收到针对特定虚拟主机上文档的请求时，它使用 `<VirtualHost>` 内部包含的配置指令。





## 语法
`<VirtualHost addr∶port …> … </VirtualHost>`

**默认设置：** 无

**上下文：** 服务器配置

为了指定用于特定虚拟主机的 IP 地址或 IP 名称，你可以使用以下任何一种方式：

- **IP 地址。** 例如：
  ```
  <VirtualHost 192.168.1.100>
      # directives go here
  </VirtualHost>
  ```

- **带有端口号的 IP 地址。** 例如：
  ```
  <VirtualHost 192.168.1.100:8080>
      # directives go here
  </VirtualHost>
  ```

- **多个 IP 地址。** 例如：
  ```
  <VirtualHost 192.168.1.100 192.168.1.105>
      # directives go here
  </VirtualHost>
  ```

- **带有端口号的多个 IP 地址。** 例如：
  ```
  <VirtualHost 192.168.1.100:8000 192.168.1.105:10000>
      # directives go here
  </VirtualHost>
  ```

> 你可以用 IP 名称替换 IP 地址，但不建议这样做；如果确定地址所需的 DNS 查询因某种原因失败，服务器可能会感到困惑，从而完全无法提供该虚拟站点服务。

特殊名称 `default_` 可以使用，在这种情况下，此虚拟主机将匹配任何未在另一个虚拟主机中明确列出的 IP 地址。如果不存在任何 `default_virtual` 主机，当没有匹配时，将使用主服务器配置，该配置由所有位于任何 `VirtualHost` 部分之外的定义组成。

如果未指定端口，则端口号默认为最近的主服务器 `Port` 指令相同的端口。你还可以指定 `*` 以匹配该地址上的所有端口。

## 日志记录指令

对于任何运行 Apache 的系统来说，记录服务器事务都是必须的。服务器日志提供有价值的信息，例如谁访问了你的 Web 站点、访问了哪些页面，以及服务器生成了哪些错误。

### LogLevel

`LogLevel` 指令设置存储在 `error log file` 中的日志消息的详细程度。当你指定日志级别时，所有更高级别的消息都会被写入日志。因此，如果你指定级别为 `crit`，那么只有 `emerg`、`alert` 和 `crit` 错误会被记录。

**语法：** `LogLevel level`

**默认设置：** `LogLevel error`

**上下文：** `服务器配置, 虚拟主机`

表 4-2 显示了可用的级别（按降序排列）及其相应的含义。

**表 4-2 LogDirective 级别**

| 级别 | 含义 |
| :--- | :--- |
| Emerg | 极端紧急状况 |
| Alert | 需要立即采取行动 |
| Crit | 严重错误 |
| Error | 错误状况 |
| Warn | 警告消息 |
| Notice | 各种通知 |
| Info | 信息性消息 |
| Debug | 调试消息 |

`ErrorLog` 指令指定用于记录 `server` 产生的 `error messages` 的日志文件名。如果 `filename` 不以斜杠（`/`）开头，则假定它是相对于 `ServerRoot` 的。

**语法：** `ErrorLog filename`

**默认设置：** `ErrorLog logs/error_log`

**上下文：** `服务器配置, 虚拟主机`

如果你需要禁用错误日志记录，可以使用以下内容：

```
ErrorLog /dev/null
```

> **注意**
> 你的服务器日志目录的权限设置非常重要，这些设置必须表明只有 Apache 用户（由 `User` 指令指定）被允许进行读/写访问。允许其他任何人写入此目录可能会潜在地造成安全漏洞。

# PidFile

通过使用 `PidFile` 指令，你可以告诉 Apache 将主服务器（即守护进程）的进程 ID（*或 PID*）写入文件。如果文件名不以斜杠（`/`）开头，则假定它是相对于 `ServerRoot` 的。`PidFile` 指令仅在独立模式下使用。

- **语法：** `PidFile filename`
- **默认设置：** `PidFile logs/httpd.pid`
- **上下文：** 服务器配置

`PidFile` 指令的主要用途是为 Apache 管理员提供便利，以便找到主 Apache PID，发送信号给服务器需要用到这个 PID。例如，如果 PID 文件保存在 `/usr/local/httpd/logs` 目录中，且其名称为 `httpd.pid`，管理员可以通过在 shell 提示符下（以 root 身份）发送 `SIGHUP` 信号来强制 Apache 服务器重新读取其配置，如下所示：

```
kill -HUP `cat /usr/local/httpd/logs/httpd.pid`
```

相同的命令会使 Apache 重新打开 `ErrorLog` 和 `TransferLog`。

> **警告**
> 与其他任何日志文件一样，请确保 PID 文件不可被服务器进程以外的任何人写入或读取。为了增强安全性，你应该使日志目录仅允许 Apache 服务器用户进行读/写操作。

# ScoreBoardFile

`ScoreBoardFile` 指令设置用于存储内部进程数据的文件路径。如果文件名不以斜杠（`/`）开头，则假定它是相对于 `ServerRoot` 的。此文件由主服务器进程用于与子进程通信。

- **语法：** `ScoreBoardFile filename`
- **默认设置：** `ScoreBoardFile logs/apache_status`
- **上下文：** 服务器配置

如果你想了解你的系统是否需要此文件，只需运行 Apache 服务器并查看是否在指定位置创建了文件。如果你的系统架构需要该文件，你必须确保该文件不会被 Apache 的多次调用同时使用。此外，请确保没有其他用户对该文件或其所在目录拥有读或写访问权限。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_116_0.png)

> 由于进程必须执行磁盘 I/O 才能通信，这可能会造成性能瓶颈；因此，如果可能，你应该为此文件创建一个 RAM 磁盘。有关详细信息，请查阅你的操作系统手册。

## 认证和安全指令

以下部分讨论的认证和安全指令允许你为 Web 服务器定义认证和访问限制。你可以使用基于用户名和密码的认证来限制对网站某些部分的访问。此外，你可以使用基于用户名、IP 地址或主机名的访问控制，以确保只有有效的用户或系统被允许访问网站的某些部分。

### AllowOverride

`AllowOverride` 指令告诉服务器哪些在 .htaccess 文件中（由 `AccessFileName` 指定）声明的指令可以覆盖在配置文件中较早找到的指令。当 `Override` 设置为 `None` 时，服务器不读取由 `AccessFileName`（默认是 .htaccess）指定的文件。这可能会加快服务器的响应时间，因为服务器不必为每个请求查找 `AccessFileName` 指定的文件（详见 `AccessFileName` 部分）。

- **语法：** `AllowOverride option1 option2 . . .`
- **默认设置：** `AllowOverride All`
- **上下文：** 目录

如果你确实希望允许基于 `AccessFileName` 的控制，你可以指定一个或多个选项。覆盖选项如下：

- `AuthConfig` — 允许使用授权指令（如 `AuthDBMGroupFile`、`AuthDBMUserInfo`、`AuthGroupFile`、`AuthName`、`AuthType`、`AuthUserFile` 和 `Require`）。
- `FileInfo` — 允许使用控制文档类型的指令（如 `AddCoding`、`AddLanguage`、`AddType`、`DefaultType`、`ErrorDocument` 和 `LanguagePriority`）。
- `Indexes` — 允许使用控制目录索引的指令（如 `AddDescription`、`AddIcon`、`AddIconByEncoding`、`AddIconByType`、`DefaultIcon`、`DirectoryIndex`、`FancyIndexing`、`HeaderName`、`IndexIgnore`、`IndexOptions` 和 `ReadmeName`）。
- `Limit` — 允许使用控制主机访问的指令（`Allow`、`Deny` 和 `Order`）。
- `Options` — 允许使用控制特定目录功能的指令（`Options` 和 `XBitHack`）。





## AuthName

AuthName 指令用于设置需要身份验证的资源（例如目录）的验证域名称。当 Web 浏览器提示用户输入用户名和密码以访问受控资源时，通常会弹出一个对话框显示该域名称。默认的域名称为空。该标签的主要目的是告知客户端用户正在尝试访问的资源。

- **语法：** AuthName "authentication_realm_name"
- **默认设置：** 无
- **上下文：** 目录，.htaccess 配置
- **覆盖：** AuthConfig

例如，“AuthName Secured Game Zone”会告知用户，他们正在请求进入站点的“Secured Game Zone”区域。请注意，为了使该指令生效，必须伴随 AuthType、Require、AuthUserFile 和 AuthGroupFile 指令一起使用。

## AuthType

AuthType 指令用于选择目录的用户身份验证类型。目前，Apache 中仅实现了基本 HTTP 身份验证或摘要身份验证类型。对于严重的安全需求，不应使用基本身份验证；因为密码和用户名是以明文形式传输的。对于映射到同一受限目录或其子目录的每个后续请求，密码和用户名都会被重新传输。摘要身份验证比基本身份验证更安全，但并非所有 Web 浏览器都支持。详情见第 7 章。AuthType 指令必须伴随 AuthName 使用，并需要其他指令（如 AuthUserFile 和 AuthGroupFile）才能正常工作。

- **语法：** AuthType Basic | Digest
- **默认设置：** 无
- **上下文：** 目录，.htaccess 配置
- **覆盖：** AuthConfig

## HostNameLookups

HostNameLookups 指令指示 Apache 启用或禁用对每个请求进行 DNS 查找。当启用时，Apache 会在其运行的每个 CGI 和 SSL 进程中，将客户端的主机名存储在 REMOTE_HOST 环境变量中。

- **语法：** HostNameLookups on | off | double
- **默认设置：** HostNameLookups off
- **上下文：** 服务器，虚拟主机，目录，.htaccess 配置

on 和 off 值的作用与其名称所示一致。double 值指的是执行双重反向 DNS 查找——即，在执行反向查找后，再对该结果执行正向查找。正向查找中的至少一个 IP 地址必须与原始地址匹配。然而，CGI 和 SSI 进程不会获取双重 DNS 查找的结果。

> **注意**：无论你将此指令设置为何种值，当使用 `mod_access`（见第 7 章）来控制基于主机名的访问时，都会执行双重反向查找，这虽然速度不快，但对于确保安全性是必要的。

我建议保留此指令的默认设置。这将消除网络上大量不必要的 DNS 流量。如果你只是希望日志文件包含 IP 名称而不是 IP 地址而想开启此功能，可以考虑其他选项，例如运行 `logresolve` 实用程序将 IP 地址解析为 IP 名称。

## IdentityCheck

`IdentityCheck` 指令告诉 Apache 通过与远程用户的 `identd`（身份验证守护进程）进程或符合 RFC1413 标准的服务器进行交互，来记录远程用户名。由于并非所有系统都支持此功能，因此该指令很少有用。大多数系统并不运行 `identd` 进程向远程服务器提供用户身份标识。

- **语法：** IdentityCheck On | Off
- **默认设置：** IdentityCheck Off
- **上下文：** 服务器配置，虚拟主机，目录，.htaccess 配置

> **警告**：如果你决定在配置中使用此指令，请注意，你记录的信息除了用于使用量跟踪外，在任何情况下都不可信。此外，由于服务器必须对每个请求执行检查，此指令还可能导致严重的性能问题。而且，当远程用户未提供 `identd` 服务，或者位于防火墙或代理之后时，检查过程必须超时。

## <Limit>

<Limit> 容器指令用于包围一组访问控制指令，这些指令随后仅适用于指定的 HTTP 方法。列出的方法名称可以是以下之一或多个：GET、POST、PUT、DELETE、CONNECT 和 OPTIONS。如果使用 GET，它还将限制 HEAD 请求。如果你希望限制所有方法，请在 <Limit> 指令中不包含任何方法。请注意，此容器不能嵌套，且其中也不能出现 `<Directory>` 容器。方法名称区分大小写。

- **语法：** `<Limit method method ...> ... </Limit>`
- **默认设置：** 无
- **上下文：** 所有

## <LimitExcept>

`<LimitExcept>` 容器指令作为 `<Limit>` 指令的完全相反功能使用（`<Limit>` 限制具名的方法，即参数，而 `<LimitExcept>` 限制除参数之外的所有 *其他* 方法）。所有未列为参数的方法都受到限制。

- **语法：** `<LimitExcept method method ...> ... </LimitExcept>`
- **默认设置：** 无
- **上下文：** 所有

在下面的示例中，限制适用于除 GET 以外的所有 HTTP 方法。

```
<LimitExcept GET>
  # directives
</LimitExcept>
```

## LimitRequestBody

`LimitRequestBody` 指令允许你设置 Apache 将处理的 HTTP 请求的大小限制。默认限制为 0，意味着无限制。你可以将此限制设置为 0 到 2147483647（2GB）之间的值。

- **语法：** `LimitRequestBody bytes`
- **默认设置：** `LimitRequestBody 0`
- **上下文：** 服务器配置，虚拟主机，目录，.htaccess 配置

仅在你经历过基于 HTTP 的拒绝服务攻击，这些攻击试图通过大型 HTTP 请求使服务器不堪重负时，才建议设置此限制。这是一个增强服务器安全性的有用指令。

## LimitRequestFields

`LimitRequestFields` 指令允许你限制单个 HTTP 请求中允许的请求头字段的数量。此限制范围为 0 到 32767（32K）。此指令可以帮助你对抗基于大型请求的拒绝服务攻击，实施安全措施。

- **语法：** `LimitRequestFields number`
- **默认设置：** `LimitRequestFields 100`
- **上下文：** 服务器配置

## LimitRequestFieldsize

`LimitRequestFieldsize` 指令允许你限制请求头字段的大小（以字节为单位）。默认大小 8190（8K）对于大多数情况都足够了。但是，如果你经历过基于大型 HTTP 请求的拒绝服务攻击，你可以将此值更改为较小的数字，以拒绝超过限制大小的请求。值为 0 时，限制设为无限制。

- **语法：** `LimitRequestFieldsize bytes`
- **默认设置：** `LimitRequestFieldsize 8190`
- **上下文：** 服务器配置

## LimitRequestLine

`LimitRequestLine` 指令设置请求行的大小限制。这实际上限制了可以发送到服务器的 URL 的大小。默认限制对于大多数情况应该是足够的。如果你经历过使用设计用于浪费服务器资源的长 URL 的拒绝服务攻击，你可以降低此限制以拒绝此类请求。

- **语法：** `LimitRequestLine bytes`
- **默认设置：** `LimitRequestLine 8190`
- **上下文：** 服务器配置

## Require

通过使用 `Require` 指令，Apache 确定哪些用户或组可以访问受限目录。有三种可用的实体名称类型：`user`、`group`、`valid-user`。例如，`require user joe jenny` 告诉 Apache 在身份验证成功后，仅允许 joe 或 jenny 进入该区域。只有指定的用户才能访问该目录。

- **语法：** `Require entity_name entity_name...`
- **默认设置：** 无
- **上下文：** 目录，.htaccess 配置
- **覆盖：** `AuthConfig`

作为一个基于组的访问要求示例，在以下配置中，只有属于指定组的用户可以访问该目录：

```
Require group my-group your-group his-group her-group
```

使用以下行，所有有效用户都可以访问该目录。

```
require valid-user
```

如果 require 指令出现在 <Limit> 部分中，则它限制对指定方法的访问；否则，它限制对所有方法的访问。例如：

```
AuthType Basic
AuthName "Game Zone Drop Box."
AuthUserFile  /www/netgames/users
AuthGroupFile /www/netgames/.groups

<Limit GET>
    require group coders
</Limit>
```

如果上述配置出现在目录的 .htaccess 文件中，则只有名为 coders 的组被允许通过 HTTP GET 方法检索文件的指令进行访问。为了正常工作，Require 指令必须伴随 AuthName 和 AuthType 指令，以及 AuthUserFile 和 AuthGroupFile 等指令。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_121_0.png)

有关身份验证的详细信息，请参见第 7 章。

## Satisfy

如果你创建了一个基本的 HTTP 身份验证配置，其中同时使用了 Allow 和 Require 指令，你可以使用 Satisfy 指令来告诉 Apache 满足哪些身份验证要求即视为通过。

- **语法：** Satisfy Any | All
- **默认设置：** Satisfy all
- **上下文：** 目录，.htaccess 配置

Satisfy 指令的值可以是 all 或 any。如果值为 all，则只有当 Allow 和 Require 都成功时，身份验证才成功。如果值为 any，则只要 Allow 或 Require 其中一个成功，身份验证即成功。

Satisfy 指令仅在特定区域的访问同时受到用户名/密码和客户端主机地址限制时才有用。在这种情况下，



默认行为（`all`）要求客户端通过地址访问限制，并输入有效的用户名和密码。使用 `any` 选项时，如果用户通过主机限制或输入有效的用户名和密码中的任意一项，客户端即被授予访问权限。此指令可用于通过使用密码来限制对某个区域的访问，同时允许来自特定 IP 地址池（即一组 IP 地址）的所有客户端在无需输入密码的情况下获得访问权限。

### ScriptInterpreterSource

`ScriptInterpreterSource` 指令允许你指定 Windows 如何查找脚本的解释器。通常，脚本解释器是通过脚本中找到的 `#!` 行来检测的。然而，将此指令设置为 `registry` 将强制 Windows 在注册表中查找脚本扩展名以找到其关联程序（即解释器）。

- 语法：`ScriptInterpreterSource Registry | Script`
- 默认设置：`ScriptInterpreterSource script`
- 上下文：目录，.htaccess

### MPM threaded 特定指令

这类似于 prefork MPM，但每个子进程不再只有一个线程，而是允许每个子进程拥有一定数量的线程。由于线程比进程更具资源效率，因此这种 MPM 非常易于扩展。子进程内的每个线程可以处理不同的请求。

通过监控其空闲线程数量来添加或删除进程。例如，如果一个进程的空闲线程少于最小数量，则会添加一个新进程。同样，当一个进程拥有最大数量的空闲线程时，它会被终止。

> 所有进程都在分配给 Apache 服务器的同一用户和组 ID 下运行。

### CoreDumpDirectory

`CoreDumpDirectory` 指令设置 Apache 在崩溃并转储核心文件（即服务器的内存映像）之前尝试切换到的目录。默认位置是由 `ServerRoot` 指令指定的目录。

- 语法：`CoreDumpDirectory directory_path`
- 默认设置：服务器根目录
- 上下文：服务器配置

### Group

**Group** 指令应与 *User* 指令配合使用。**Group** 确定独立服务器处理请求所在的组。若要使用此指令，独立服务器最初必须以 root 身份运行。**Group** 指令也可以被分配一个组号。**Group** 在你的 */etc/group* 文件中查找组名称及其对应的数值。

- 语法：`Group Unix-group`
- 默认设置：`Group #=-1`
- 上下文：服务器配置，虚拟主机

![](img/e11fcbd2818a3495ac70085e5d8d1c26_123_0.png)

我稍后提供的关于 *User* 指令的所有警告和建议也适用于此指令。请确保阅读本章稍后关于 *User* 指令的详细信息。

### Listen

默认情况下，Apache 响应附加到服务器机器的所有 IP 地址上的请求，但仅响应由 *Port* 指令指定的端口地址。*Listen* 指令可用于使这种情况更具可配置性。你可以使用 *Listen* 指令告诉 Apache 响应特定的 IP 地址、IP 地址和端口组合，或仅响应端口本身。

- 语法：`Listen [IP address:] port_number`
- 默认设置：无
- 上下文：服务器配置

虽然 *Listen* 可以代替 *BindAddress* 和 *Port* 使用，但如果你的 Apache 服务器生成指向自身的 URL，你可能仍需要使用 *Port* 指令。

可以使用多个 *Listen* 指令来指定要监听的多个地址和端口。服务器将响应来自列出的任何地址和端口的请求。例如，要使服务器接受端口 80 和端口 8080 上的连接，请使用：

```
Listen 80
Listen 8080
```

以下示例使 Apache 接受两个 IP 地址和端口号上的连接：

```
Listen 192.168.1.100:80
Listen 192.168.1.101:8080
```

### ListenBacklog

`ListenBacklog` 指令通过允许你设置待处理连接队列的最大长度，使你可以针对一种名为拒绝服务（DoS）的已知安全攻击采取防御措施。如果你检测到正在遭受 TCP SYN 泛洪（DoS）攻击，请增加此值；否则，你可以保持默认值不变。

- **语法：** `ListenBacklog backlog`
- **默认设置：** `ListenBacklog 511`
- **上下文：** 服务器配置

### LockFile

如果 Apache 是使用 `USE_FCNRL_SERIALIZED_ACCEPT` 或 `USE_FLOCK_SERIALIZED_ACCEPT` 选项编译的，则使用锁文件。你可以使用 `LockFile` 指令设置锁文件文件名的路径。请确保只有 Apache 服务器具有该文件的读写访问权限。

- **语法：** `LockFile filename`
- **默认设置：** `LockFile logs/accept.lock`
- **上下文：** 服务器配置

> 将锁文件存储在通过网络文件系统（NFS）挂载的分区上不是一个好主意，因为 NFS 在文件锁定和安全性方面众所周知存在问题。

### MaxClients

`MaxClients` 指令限制 Apache 可以同时处理的请求数量。由于 Apache 为每个请求使用一个子服务器，因此这也是可以同时存在的子服务器的有效限制。

- **语法：** `MaxClients number`
- **默认设置：** `MaxClients 256`
- **上下文：** 服务器配置

默认限制实际上是 Apache 源代码发行版中 `httpd.h` 文件中设置的硬性限制。对于大多数中等负荷的网站，此设置应该足够了。Apache 程序员在那里设置硬性限制有两个原因：他们不希望服务器通过填满某些内核表而使系统崩溃，并且这个最大限制使记分板文件足够小，以便轻松读取。当服务器达到最大请求数时，它会进入等待状态，直到可以处理这些传入请求为止。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_125_0.png)

如果你拥有高性能服务器系统并具备必要的带宽，你可以通过修改适当的 MPM 头文件（`mpm_defaults.h`）来重新编译服务器，以提高硬性限制。参见第 2 章中的表 2-3。

### MaxRequestsPerChild

Apache 启动一个子服务器进程来服务请求；然而，子服务器可以处理多个请求。子服务器可以处理的请求数量由 `MaxRequestsPerChild` 指令限制。

- **语法：** `MaxRequestsPerChild number`
- **默认设置：** `MaxRequestsPerChild 0`
- **上下文：** 服务器配置

在提供最大数量的请求服务后，子进程将终止。如果 `MaxRequestsPerChild` 为 0，则该进程永远不会过期。如果你怀疑操作系统（例如，Solaris）上存在一些库包含内存泄漏代码，你可能希望将此指令设置为非零值。这使你可以为子进程定义一个生命周期，从而减少进程消耗泄漏内存并缓慢耗尽所有可用内存的可能性。它还为你的系统提供了较小的平均负载数，因为随着 Web 服务器变得不太繁忙，与 Apache 相关的负载会减少。

### MaxSpareThreads

`MaxSpareThreads` 指令设置空闲线程的最大数量。线程化 MPM 在服务器范围内处理空闲线程，这意味着如果服务器中有太多空闲线程，它会开始终止子进程，直到空闲线程数量减少到此处指定的数量为止。

- **语法：** `MaxSpareThreads number`
- **默认设置：** `MaxSpareThreads 10`（对于 Perchild MPM）或 `500`（对于线程化 MPM）
- **上下文：** 服务器配置

perchild MPM 按每个子进程计算空闲线程，这意味着如果某个子进程中有太多空闲线程，线程将被销毁，直到每个子进程的线程数小于由 `MaxSpareThreads` 指令指定的数量为止。

### MinSpareThreads

`MinSpareThreads` 指令设置空闲线程的最小数量。线程化 MPM 在服务器范围内处理空闲线程，这意味着当空闲线程少于此处指定的数量时，Apache 会创建新的子进程，使总线程数至少达到这个数量。




**语法：** `MinSpareServers number`

**默认设置：** `MaxSpareThreads` 5（用于 Perchld MPM）或 250（用于线程 MPM）

**上下文：** 服务器配置

`perchild` MPM 在每个子进程基础上处理空闲线程数；因此，当某个子进程的空闲线程数少于此处指定的最小线程数时，服务器会在该子进程中创建新的线程。

## SendBufferSize

`SendBufferSize` 指令将 TCP 发送缓冲区大小设置为指定的字节数。在高性能网络上，将该指令的值设置为高于操作系统的默认值可能会提高服务器性能。

**语法：** `SendBufferSize bytes`

**默认设置：** 无

**上下文：** 服务器配置

## StartServers

`StartServers` 指令设置启动时创建的子 Apache 服务器进程数量。特定时段内所需的 Apache 子进程数量是动态控制的。主 Apache 服务器（守护进程）在遇到更高的请求负载时会启动新的子进程。实际的子进程数量由 `MinSpareServers`、`MaxSpareServers` 和 `MaxClients` 指令控制。因此，调整此参数所带来的收益很小。

**语法：** `StartServers number`

**默认设置：** `StartServers` 5

**上下文：** 服务器配置

> **注意**
> 只有当 Apache 服务器作为独立服务器运行时，`StartServers` 指令才有效。换句话说，你需要将 `ServeType` 设置为 standalone 才能使此指令生效。

> **注意**
> 在运行 Microsoft Windows 时，此指令设置正在运行的子进程总数。由于 Windows 版本的 Apache 是多线程的，一个进程处理所有请求。其余进程保留备用，直到主进程终止。

## ThreadsPerChild

Windows 版本的 Apache 是一个多线程服务器。`ThreadsPerChild` 指令告诉服务器应该使用多少线程。它还决定了服务器在任何给定时间能处理的最大连接数。因此，应合理设置此值，以允许尽可能多的并发请求。

**语法：** `ThreadsPerChild number`

**默认设置：** `ThreadsPerChild` 50

**上下文：** 服务器配置（Windows）

## User

`User` 指令设置用于处理 HTTP 请求的 Apache 子进程的用户 ID。一旦 Apache 服务器启动，它就会启动子进程来响应请求。然而，这些子进程并不是以 `root` 身份运行的。父 Apache 进程（通常称为守护程序）会将子进程的用户 ID 更改为 `User` 指令中设置的任何值，只要它是一个有效的用户 ID。

**语法：** `User unix-userid`

**默认：** `User #1`

**上下文：** 服务器配置、虚拟主机

如果你以非 root 用户启动服务器，它无法更改为 `User` 指令指定的用户 ID，而是继续以原始用户身份运行。如果你以 `root` 身份启动服务器，父 Apache 进程保持以 `root` 身份运行是正常的；但是，它以 `User` 指令指定的用户身份运行子进程。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_127_0.png)

> 除非你完全知道自己在做什么以及其中的风险，否则永远不要将 `User`（或 `Group`）指令设置为 `root`。

你也可以使用用户 ID 编号，通常可以在 `/etc/password` 文件中找到。如果你计划使用数值而不是实际的用户名，该数值前面必须加上 # 符号。

许多 Apache 管理员使用默认的 `nobody` 用户来托管他们的网站。并非所有 Unix 系统都提供此用户，且它也不总是理想的。我强烈建议为你的 Apache 服务器使用独特的用户和组 ID（参见 `Group` 指令）。这样做可以更好控制服务器可以或不可以访问的内容。你决定用于 Apache 子进程的用户 ID 应具有非常有限的访问权限。它不应能访问那些不对外部世界可见的文件，同样，该用户也不应能执行那些不适用于 HTTP 请求的应用程序。

在 `<VirtualHost>` 容器中使用此指令需要一个配置正确的 `suEXEC` 包装器。当以这种方式在 `<VirtualHost>` 容器内使用该包装器时，仅影响 CGI 运行的用户。非 CGI 请求仍由主 `User` 指令指定的用户处理。因此，主 `User` 指令不能被完全覆盖。

### MPM perchild 专用指令

在此 MPM 模型中，启动固定数量的子进程，每个进程具有指定数量的线程。随着请求负载增加，进程会按需添加新线程。当请求数量减少时，进程使用最小和最大线程数设置来缩减其线程数。

#### AssignUserID

`AssignUserID` 指令将用户名和组名分配给虚拟主机。

*语法：* `AssignUserID username groupname`

*默认设置：* 无

*上下文：* 虚拟主机

例如，在下面，名为 `www.afatcat.com` 的虚拟主机被分配给用户 `mrbert` 和名为 `wheel` 的组。你必须使用 `ChildPerUserID` 来指定可以服务此虚拟主子的子进程数量。

```apache
<VirtualHost 192.168.1.100>
  ServerName www.afatcat.com
  AssignUserID mrbert wheel

  #
  ## 其他指令在此处
  #
</VirtualHost>
```

**username 和 groupname 必须存在于你的系统中。例如，在 Linux 系统上** `username` **和** `groupname` **必须分别存在于** `/etc/passwd` **和** `/etc/group` **文件中。**

#### ChildPerUserID

`ChildPerUserID` 指令为虚拟主机的指定用户名和组名分配一定数量的子进程。

**语法：** `ChildPerUserID number_of_child username groupname`

**默认设置：** 无

**上下文：** 虚拟主机

例如，在下面，虚拟主机 **www.afatcat.com** 将由 10 个以用户名 **mrbert** 和组 **wheel** 运行的 Apache 子进程处理：

```
ChildPerUserID 10 mrbert wheel
<VirtualHost 192.168.1.100>
ServerName www.afatcat.com
AssignUserID mrbert wheel

# 其他指令在此处
#
</VirtualHost>
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_129_0.png)

*username* 和 *groupname* 必须存在于你的系统中，Apache 才能使用它们。例如，在 Linux 系统上，*username* 和 *groupname* 必须分别存在于 `/etc/passwd` 和 `/etc/group` 文件中。

#### ConnectionStatus

*ConnectionStatus* 指令设置状态信息是否在内部存储。当设置为 on 时，使用状态信息的模块将正常工作。

**语法：** `ConnectionStatus On | Off`

**默认设置：** `ConnectionStatus On`

**上下文：** 服务器配置

#### CoreDumpDirectory

参见“MPM threaded 专用指令”部分中的 **CoreDumpDirectory** 指令。

#### Group

参见“MPM threaded 专用指令”部分中的 **Group** 指令。

#### Listen

参见“MPM threaded 专用指令”部分中的 **Listen** 指令。

#### ListenBacklog

参见“MPM threaded 专用指令”部分中的 `ListenBacklog` 指令。

#### LockFile

参见“MPM threaded 专用指令”部分中的 `LockFile` 指令。

#### MaxRequestsPerChild

参见“MPM threaded 专用指令”部分中的 `MaxRequestsPerChild` 指令。

#### MaxSpareThreads

参见“MPM threaded 专用指令”部分中的 `MaxSpareThreads` 指令。

#### MaxThreadsPerChild

`MaxThreadsPerChild` 指令设置每个子进程的最大线程数。默认数量是一个硬限制。如果你想更改此限制，必须修改相应的头文件。详见第 2 章中的表 2-3。

- 语法：`MaxThreadsPerChild number`
- 默认设置：`MaxThreadsPerChild 64`
- 上下文：服务器配置

#### MinSpareThreads

参见“MPM threaded 专用指令”部分中的 `MinSpareThreads` 指令。

#### NumServers

`NumServers` 指令设置 Apache 创建的并发子进程数量。

- 语法：`NumServers number`
- 默认设置：`NumServers 2`
- 上下文：服务器配置




每子进程 MPM 使用此指令设置的值来确定同时运行的子进程数量。默认值 2 可能并不适合大多数系统。您可能希望将其设置为更高的限制，例如 15 或 20。更高的数值会生成更多的 Apache 进程，这意味着可以处理更多的同时连接。

# PidFile

参见 “MPM 线程特有指令” 章节下的 `PidFile` 指令。

# ScoreBoardFile

参见 “MPM 线程特有指令” 章节下的 `ScoreBoardFile` 指令。

## SendBufferSize

参见 “MPM 线程特有指令” 章节下的 `SendBufferSize` 指令。

## StartThreads

`StartThreads` 指令设置每个子进程的初始线程数。由于线程数是动态控制的，在大多数情况下，没有必要将其设置为高于默认值的数字。

- **语法：** `StartThreads number`
- **默认设置：** `StartThreads 5`
- **上下文：** 服务器配置

## User

参见 “MPM 线程特有指令” 章节下的 `User` 指令。

## MPM Winnt 特有指令

这是适用于所有 Windows 平台版本的 MPM，包括 Windows NT/2000/XP 和 Windows 9x/ME。此模块是多线程的；使用该模块时，Apache 将创建一个父进程和一个子进程。子进程创建处理请求的所有线程。此模块现在利用了一些 Windows 专用的原生函数调用，这使其在 Windows 平台上的性能优于早期版本的 Apache 服务器。

## CoreDumpDirectory

参见 “MPM 线程特有指令” 章节下的 CoreDumpDirectory 指令。

## Listen

参见 “MPM 线程特有指令” 章节下的 Listen 指令。

## ListenBacklog

参见 “MPM 线程特有指令” 章节下的 ListenBacklog 指令。

## MaxRequestsPerChild

参见 “MPM 线程特有指令” 章节下的 MaxRequestsPerChild 指令。

# PidFile

参见 “MPM 线程特有指令” 章节下的 PidFile 指令。

## SendBufferSize

参见 “MPM 线程特有指令” 章节下的 SendBufferSize 指令。

## ThreadsPerChild

参见 “MPM 线程特有指令” 章节下的 ThreadsPerChild 指令。

## MPM prefork 特有指令

prefork MPM 创建一个子进程池来提供服务请求。每个子进程只有一个线程。例如，如果 Apache 启动 30 个子进程，它可以同时服务 30 个请求。

如果出现问题且子进程死亡，则只丢失单个请求。子进程的数量通过最小和最大设置进行控制。当请求数量增加时，将添加新的子进程，直到达到最大值。同样，当请求减少时，多余的子进程会被终止。

## CoreDumpDirectory

参见 “MPM 线程特有指令” 章节下的 CoreDumpDirectory 指令。

## Group

参见 “MPM 线程特有指令” 章节下的 Group 指令。

## Listen

参见 “MPM 线程特有指令” 章节下的 Listen 指令。

## ListenBacklog

参见 “MPM 线程特有指令” 章节下的 ListenBacklog 指令。

## LockFile

参见 “MPM 线程特有指令” 章节下的 LockFile 指令。

## MaxClients

参见 “MPM 线程特有指令” 章节下的 MaxClients 指令。

## MaxRequestsPerChild

参见 “MPM 线程特有指令” 章节下的 MaxRequestsPerChild 指令。

## MaxSpareServers

此指令允许您设置服务器上空闲的 Apache 子进程数量。

- **语法：** `MaxSpareServers number`
- **默认设置：** `MaxSpareServers 10`
- **上下文：** 服务器配置

如果空闲的 Apache 子进程数量超过 MaxSpareServers 指令指定的最大数量，则父进程会终止多余进程。只有在非常繁忙的站点上，才需要调整此参数。除非您知道自己在做什么，否则请勿更改默认值。

## MinSpareServers

`MinSpareServers` 指令设置期望的空闲子服务器进程的最小数量。空闲进程是指未处理请求的进程。如果空闲的 Apache 进程数量少于 `MinSpareServers` 指令指定的数量，则父进程将以每秒最多 1 个的速度创建新的子进程。只有在非常繁忙的站点上，才需要调整此参数。除非您知道自己在做什么，否则请勿更改默认值。

- **语法：** `MinSpareServers number`
- **默认设置：** `MinSpareServers 5`
- **上下文：** 服务器配置

# PidFile

参见 “MPM 线程特有指令” 章节下的 `PidFile` 指令。

# ScoreBoardFile

参见 “MPM 线程特有指令” 章节下的 `ScoreBoardFile` 指令。

## SendBufferSize

参见 “MPM 线程特有指令” 章节下的 `SendBufferSize` 指令。

## StartServers

参见 “MPM 线程特有指令” 章节下的 `StartServers` 指令。

## User

参见 “MPM 线程特有指令” 章节下的 `User` 指令。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_135_0.png)
![](img/e11fcbd2818a3495ac70085e5d8d1c26_135_1.png)

## Apache 模块

在第 4 章中，我讨论了核心和多处理器模块（MPM）指令。Apache 提供了更多来自标准源代码分发中可用的模块指令。这些模块通过指令的使用提供了大量的功能。本章讨论这些模块及其指令。

## 模块概览

我不按字母顺序列出所有模块，而是根据功能相似性对模块进行了分组。这些模块分为以下类别：

- **环境相关：** 这些指令允许您设置和重置环境变量。
- **认证和访问控制：** 这些指令允许您验证和授权用户对网站受限部分的访问。
- **动态内容生成：** 这些指令允许您运行外部程序（如 CGI 脚本或服务器端包含）以创建动态内容。
- **内容类型配置：** 这些指令允许您控制文件的 MIME 类型。
- **目录列表：** 这些指令允许您控制目录列表的格式。
- **响应头：** 这些指令允许您控制 HTTP 响应头。
- **服务器信息和日志记录：** 这些指令允许您控制服务器日志和状态信息。
- **URL 映射：** 这些指令允许您为 URL 进行映射、重写和创建别名。
- **杂项模块：** 这些指令允许您控制 Apache 的杂项方面，例如代理服务、WEBDEV 模块等。

# 本章内容

- 如何使用环境模块
- 如何使用认证和访问控制模块
- 如何使用动态内容生成模块
- 如何使用目录列表模块
- 如何使用内容类型模块
- 如何使用动态内容生成模块
- 如何使用响应头模块
- 如何使用服务器信息和日志记录模块
- 如何使用 URL 映射模块
- 如何使用其他杂项模块

## 环境相关模块

表 5-1 中列出的模块使您可以操作可供其他模块或外部程序（如 CGI（通用网关接口）脚本、SSI（服务器端包含）、mod_perl 脚本、PHP 脚本、Java 服务程序等）使用的环境。

**表 5-1 环境相关模块**

| 模块 | 目的 |
| :--- | :--- |
| `mod_env` | 将环境传递给 CGI 和 SSI 脚本等外部程序。 |
| `mod_setenvif` | 使用来自客户端的信息设置条件环境变量。 |
| `mod_unique_id` | 此模块为每个请求生成唯一 ID。它没有指令。此模块默认未编译。您必须使用 `-enable-unique-id` 选项通过 `configure` 脚本配置源代码，并编译和安装 Apache。 |

## mod_env

`mod_env` 默认被编译。它使您可以将环境变量传递给外部程序，如 CGI 脚本、SSI、`mod_perl` 脚本、PHP 脚本等。`mod_env` 具有以下指令。

## PassEnv

`PassEnv` 指令告诉该模块将服务器自身环境中的一个或多个环境变量传递给 CGI 和 SSI 脚本。

- **语法：** `PassEnv variable [...]`
- **上下文：** 服务器配置，虚拟主机

例如，以下指令将 HOSTTYPE 和 PATH 环境变量传递给程序。

`PassEnv HOSTTYPE PATH`





## SetEnv

SetEnv 指令将环境变量设置为给定值，然后将其传递给 CGI/SSI 脚本。每个 SetEnv 指令只能定义一个变量和值对。

- **语法：** SetEnv variable value
- **上下文：** 服务器配置，虚拟主机

例如，下面的 SetEnv 指令将 CURRENT_CITY 变量设置为 SACRAMENTO：

```
SetEnv CURRENT_CITY SACRAMENTO
```

## UnsetEnv

UnsetEnv 指令从传递给 CGI/SSI 脚本的环境变量中移除一个或多个环境变量。这可用于确保 Apache 服务器可用的某些环境变量对您的 CGI 脚本不可用。

- **语法：** UnsetEnv variable [ ... ]
- **上下文：** 服务器配置，虚拟主机

例如，下面的 UnsetEnv 指令从环境变量列表中移除 CURRENT_STATE 变量：

```
UnsetEnv CURRENT_STATE
```

## mod_setenvif

mod_setenvif 模块默认在 Apache 中编译。它允许您使用 HTTP 请求中的信息创建自定义环境变量。您可以在重写 URL 或将用户重定向到不同页面时使用此类信息。

## BrowserMatch

当正则表达式匹配 HTTP 请求 User-Agent 头部中的模式时，BrowserMatch 指令会设置和取消自定义环境变量。User-Agent 头部由 Web 客户端（如 Web 浏览器、Web 机器人等）发送。

- **语法：** BrowserMatch regex variable[=value] [ ... ]
- **上下文：** 服务器配置

例如，下面的设置如果 HTTP 请求的 User-Agent 头字段包含单词 Mozilla，则将名为 vbscript 的变量设置为 no，并且因为该变量未指定值，所以名为 javascript 的环境变量被设置为 1：

```
BrowserMatch ^Mozilla vbscript=no javascript
```

让我们看另一个例子：

```
BrowserMatch IE vbscript !javascript
```

这里，如果在 User-Agent HTTP 请求头中找到单词 IE，则移除变量 javascript 并将 vbscript 设置为 1。! 字符会从环境中移除变量。

> **注意**：正则表达式匹配是区分大小写的。

## BrowserMatchNoCase

BrowserMatchNoCase 指令与 BrowserMatch 指令相同，除了它提供正则表达式的非区分大小写匹配。

- **语法：** BrowserMatchNoCase regex variable[=value] [ ... ]
- **上下文：** 服务器配置

例如，下面的指令匹配 MSIE、msie、Msie 等：

```
BrowserMatchNoCase ^MSIE vbscript=yes
```

## SetEnvIf

与 BrowserMatch 和 BrowserMatchNoCase 指令类似，SetEnvIf 指令允许您设置和取消自定义环境变量。实际上，BrowserMatch 和 BrowserMatchNoCase 是 SetEnvIf 的两个特殊版本。这两个指令只能对 User-Agent HTTP 请求头字段执行正则表达式，而 SetEnvIf 可用于所有请求头字段以及其他与请求相关的信息，如远程主机名（Remote_Host）、远程 IP 地址（Remote_Addr）、请求方法（Request_Method）、请求 URI（Request_URI）和引用者（Referer）。

- **语法：** SetEnvIf attribute (regex envvar[=value] [ ... ])
- **上下文：** 服务器配置

例如，如果 Remote_Host HTTP 头设置为 yourdomain.com，则下面的 SetEnvIf 指令将 local_user 变量设置为 true。

```
SetEnvIf Remote_Host "yourdomain\.com" local_user=true
```

## SetEnvIfNoCase

SetEnvIfNoCase 指令与 SetEnvIf 相同，除了它提供非区分大小写的正则表达式匹配。

- **语法：** SetEnvIfNoCase attribute regex variable=value [...]
- **上下文：** 服务器配置

## mod_unique_id

mod_unique_id 模块为每个请求提供一个魔术令牌，在非常特定的条件下保证该令牌在所有请求中是唯一的。该唯一标识符即使在正确配置的主机集群中的多台机器之间也是唯一的。每个请求的环境变量 UNIQUE_ID 被设置为该标识符。此模块没有指令。

## 认证和访问控制模块

Apache 有许多模块用于执行认证和授权任务。在大多数情况下，认证模块使用基本 HTTP 认证，它使用明文密码。授权模块允许您通过用户名或 IP 地址控制对您网站目录的访问。表 5-2 中显示的模块允许您执行认证和访问控制任务。

### 表 5-2 认证和访问控制模块

| **模块** | **用途** |
| --- | --- |
| mod_auth | 这是标准认证模块，实现了基本 HTTP 认证。详情见第 7 章。 |
| mod_auth_anon | 允许匿名用户访问认证区域。 |
| mod_auth_dbm | 提供使用 DBM 文件进行用户认证。 |
| mod_auth_db | 提供使用 Berkeley DB 文件进行用户认证。 |
| mod_auth_digest | 此模块使用消息摘要 5 (MD5) 实现 Digest 认证。 |
| mod_access | 此模块允许您通过主机名或 IP 地址授权访问。详情见第 7 章。 |

## mod_auth_anon

mod_auth_anon 模块允许匿名访问认证区域。如果您熟悉匿名 FTP 服务器，这与该设置非常相似。所有用户都可以使用名为 "anonymous" 的用户 ID 及其电子邮件地址作为密码来获得访问权限。输入的电子邮件地址存储在日志文件中，可用于执行用户跟踪或创建潜在客户邮件列表。

您必须使用源代码发行版中 `configure` 脚本的 `-enable-auth-anon` 选项启用此模块，并编译和安装 Apache。

## Anonymous

使用 Anonymous 指令，您可以指定一个或多个可用于访问该区域的用户名。将用户名 "anonymous" 保留在您选择的列表中是个好主意，因为它与匿名访问密切相关。如果您选择的用户名中包含空格字符，请确保用户名用引号括起来。

- **语法：** Anonymous user user ...
- **上下文：** 目录，每目录访问控制文件 (`.htaccess`)
- **覆盖：** AuthConfig

例如，下面的指令允许用户输入 Unregistered User 或 anonymous 作为用户名进入匿名区域。

```
Anonymous "Unregistered User" anonymous
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_140_0.png)

> 用户名字符串不区分大小写。

## Anonymous_Authoritative

当设置为 On 时，匿名认证成为目录的权威认证方案。换句话说，如果您对目录有多个认证要求并且也设置了此指令，则其他方法将被忽略。

- **语法：** Anonymous_Authoritative On | Off
- **默认设置：** Anonymous_Authoritative Off
- **上下文：** 目录，每目录访问控制文件 (`.htaccess`)
- **覆盖：** AuthConfig

## Anonymous_LogEmail

当 Anonymous_LogEmail 指令设置为 On 时，在浏览器弹出认证窗口的密码字段中输入的任何内容都会记录在 Apache 访问日志文件中。

- **语法：** Anonymous_LogEmail On | Off
- **默认设置：** Anonymous_LogEmail On
- **上下文：** 目录，每目录访问控制文件 (`.htaccess`)
- **覆盖：** AuthConfig

## Anonymous_MustGiveEmail

当设置为 On 时，Anonymous_MustGiveEmail 指令使模块拒绝未提供电子邮件地址格式密码的访问请求。

- **语法：** Anonymous_MustGiveEmail On | Off
- **默认设置：** Anonymous_MustGiveEmail On
- **上下文：** 目录，每目录访问控制文件 (`.htaccess`)
- **覆盖：** AuthConfig

![](img/e11fcbd2818a3495ac70085e5d8d1c26_141_0.png)

当此指令设置为 On 时，您不应该信任人们输入的电子邮件地址，因为没有办法检查是谁输入了谁的电子邮件地址。

## Anonymous_NoUserID

如果您希望用户将弹出窗口中的用户名字段留空，请将 Anonymous_NoUserID 指令设置为 On；否则，需要与 Anonymous 指令中提供的值匹配的用户名。

- **语法：** Anonymous_NoUserID On | Off
- **默认设置：** Anonymous_NoUserID Off
- **上下文：** 目录，每目录访问控制文件 (`.htaccess`)
- **覆盖：** AuthConfig

## Anonymous_VerifyEmail

当 Anonymous_VerifyEmail 指令设置为 On 时，它要求密码是一个有效的电子邮件地址。然而，有效性检查是有限的。模块仅检查密码字段中的 @ 符号和点 .。如果输入的密码包含这两个符号，则接受。

- **语法：** Anonymous_VerifyEmail On | Off
- **默认设置：** Anonymous_VerifyEmail Off




## 上下文：目录，按目录的访问控制文件（`.htaccess`）

### 覆盖：AuthConfig

以下配置展示了如何使用前文所述的指令为目录提供匿名访问权限。

```
Anonymous_NoUserId off
Anonymous_MustGiveEmail on
Anonymous_VerifyEmail on
Anonymous_LogEmail on
Anonymous_anonymous guest "I do not know"
AuthName Use 'anonymous' & Email address for guest entry
AuthType basic
require valid-user
```

## mod_auth_dbm

基于文本文件的认证（使用 `mod_auth`）在处理速度上效率较低，当大量用户（超过 2000 人）需要认证访问受限的 Web 部分时，可能会负面影响 Web 服务器的性能。在这种情况下，`mod_auth_dbm` 模块是更好的选择。`mod_auth_dbm` 模块使用 DBM 文件而不是文本文件来存储数据。DBM 文件是一种特殊类型的数据文件，允许对存储的数据进行更快的随机访问。

> **注意** 实际上，如果你拥有大量用户，请考虑在第 7 章中讨论的基于 `mod_auth_mysql` 或 Apache::AuthDBI 的认证。只有在无法使用数据库时，才建议使用基于 DBM 的认证。

DBM 文件以键=值对的形式存储数据记录，并为文件中的键保持一个计算过的索引表。通过使用 DBM 文件中的索引表，检索与键关联的记录的速度比解析拥有数万条记录的大文本文件所需的时间更快。有许多 DBM 可用，最常见的包括 GDBM、NDBM、SDBM 和 Berkeley DB (BSD-DB)。表 5-3 列出了这些 DBM 的功能列表。

**表 5-3**
**DBM 功能**

| 功能 | NDBM | SDBM | GDBM | BSD-DB |
| :--- | :--- | :--- | :--- | :--- |
| 许可限制 | 未知 | 无 | 有 | 无 |
| 字节序无关 | 否 | 否 | 否 | 是 |
| 默认大小限制 | 4K | 1K | 无 | 无 |
| 创建 FTP 安全文件 | 否 | 是 | 是 | 是 |
| 速度 | 未知 | 慢 | 中 | 快 |
| 数据库大小 | 未知 | 小 | 大 | 中 |
| 代码大小 | 未知 | 小 | 大 | 大 |
| 源码包含在 Perl 中 | 否 | 是 | 否 | 否 |

此表格基于 Perl 5 文档中的信息。在使用任何 DBM 与 Apache 之前，请执行以下操作，以确保你选择的 DBM 已安装在你的系统中。通过确认 DBM 库文件位于你系统的默认库目录中来完成此操作。你需要带有 DBM 支持的 Perl。确保你拥有编译了所选 DBM 支持的最新版本 Perl。

> 你可以从 `www.perl.com` 下载 Perl。为 DBM 支持配置 Perl 非常容易。只需运行配置脚本，它会提示你关于 DBM 支持的信息。例如，如果你选择 `NDBM` 或 `GDBM` 作为你所需的 DBM，并且如果你的系统中安装了它们，Perl 配置脚本会询问你是否希望使用 `-ln dbm`、`-lgdbm` 和库标志来编译 Perl。

在你已在系统中安装了适当的 DBM 库之后，你需要配置 Apache 以支持 DBM 文件，因为标准的 Apache 发行版并未启用 DBM 支持。使用 `configure` 脚本配合 `--enable-auth-dbm` 选项配置 Apache 源代码，并按照常规编译和安装 Apache。

> 如果你在编译 Apache 时遇到困难，请尝试在 `configuration` 文件中的 `EXTRA_LIBS` 中添加 `-lyour_dbmaname`。例如，如果你正在使用 GDBM，你可以添加 `-lgdbm` 使 `EXTRA_LIBS=-lgdbm`。确保你重新运行 `configure` 脚本并在之后再次运行 `make`。如果有问题，最好尝试 GNU GDBM，因为它被许多不同的系统大量使用，并且你很可能在 USENET 新闻组中获得帮助。

在 Apache 正确编译以支持 DBM 文件后，你可以使用 dbmmanage 创建 DBM 用户文件。首先使用标准 Apache 发行版（或源代码发行版）支持目录中找到的 dbmmanage Perl 脚本，用于创建基于 DBM 的用户文件。dbmmanage Perl 脚本可以创建许多流行的 DBM 文件，如 NDBM、GDBM 和 Berkeley DB 文件。此脚本可用于创建新的 DBM 文件、添加用户和密码、更改密码、删除用户或查看用户信息。在使用脚本之前，你应该修改脚本中的以下行，以便你想使用的 DBM 列为 ISA 数组中的第一项：

```
BEGIN { @AnyDBM_File::ISA = qw(DB_File, NDBM_File, GDBM_File) }
```

例如，如果你计划使用 GDBM 文件，将该行更改为：

```
BEGIN ( $AnyDBM_File::ISA = qw( GDBM_File , DB_File, NDBM_File) )
```

要查看脚本提供的选项，请如下运行它：

```
./dbmanage
```

这会显示一条包含所有可能选项的语法行。要创建一个名为 /www/secrets/myuserdbm 的新 DBM 文件，并添加一个名为 reader 的用户，请输入以下命令：

```
./dbmanage /www/secrets/myuserdbm adduser reader
```

脚本将要求你输入（并重新输入）用户 reader 的密码。完成后，它将把用户名和加密后的密码添加到 myuserdbm DBM 文件中。不要使用 add 选项来添加用户，因为它不会加密密码。要查看 DBM 文件中所有用户的列表，请使用以下脚本：

```
./dbmanage /path/to/your/dbmfile view
```

在重新编译支持 DBM 的 Apache 后，你可以使用 mod_auth_dbm 模块来提供基于 DBM 的 Basic HTTP 认证。请注意，对于 Berkeley DB，你必须使用 mod_auth_db 而不是 mod_auth_dbm。

mod_auth_dbm 模块提供了指令 AuthDBMUserFile、AuthDBMGroupFile 和 AuthDBMAuthoritative。让我们来看看这些指令以及使用 mod_auth_dbm 模块的一些示例。

### AuthDBMUserFile

AuthDBMUserFile 指令设置用于 DBM 认证的用户文件的完全限定路径名。该文件每条记录包含一个键值对，其中用户名是键，而经过 crypt() 加密的密码是值。请注意，记录中的每个字段由冒号分隔，并且可以在初始的用户名和密码字段之后追加任意数据。

- **语法：** AuthDBMUserFile filename
- **上下文：** 目录，按目录的访问控制文件 (`.htaccess`)
- **覆盖：** AuthConfig

![](img/e11fcbd2818a3495ac70085e5d8d1c26_144_0.png)

> 切勿将用户数据库文件存储在你的 Web 文档树中，因为某人可能会下载整个用户数据库并滥用它。

### AuthDBMGroupFile

AuthDBMGroupFile 指令设置包含用户组列表的组文件的完全限定路径名。文件中的每条记录都是一个键值对，其中键是用户名，值是该用户所属的组名的逗号分隔列表。

- **语法：** *AuthDBMGroupFile* *filename*
- **上下文：** 目录，按目录的访问控制文件 (`.htaccess`)
- **覆盖：** *AuthConfig*

如果你不想使用单独的组文件，可以使用单个 DBM 文件来提供密码和组信息。该文件的格式如下：

```
*DBM_Record_Key(username) - encrypted_password; comma_separated_group_list*
```

这里，*username* 是键，而 *password* 和 *group* 列表是值的两个字段。如果需要，可以在 DBM 文件中的另一个冒号之后保留其他数据；认证模块会忽略这些数据。如果你使用单个 DBM 来提供组和密码信息，你必须将 `AuthDBMGroup` 和 `AuthDBMUserFile` 指令都指向同一个文件。

### AuthDBMAuthoritative

当在同一目录中使用多种认证方案（如 `mod_dbm` 和标准 `mod_auth`）时，可以使用 `AuthDBMGroupFile` 指令（注：原文此处可能有误，根据上下文应为 AuthDBMAuthoritative，但这里保留原文逻辑翻译，若原文确指 AuthDBMGroupFile 定义是否权威方案，通常是指 AuthDBMAuthoritative，但为了忠实原文翻译如下，若原文有误则译出原文含义）来定义 `mod_auth_dbm` 是否是权威的认证方案。

- **语法：** *AuthDBMAuthoritative* *On* | *Off*
- **默认设置：** *AuthDBMAuthoritative* *On*
- **上下文：** 目录，按目录的访问控制文件 (`.htaccess`)
- **覆盖：** *AuthConfig*

该指令的默认值使 `mod_auth_dbm` 成为该目录的权威认证。因此，如果基于 DBM 的认证对特定用户失败，该用户的凭证不会传递给较低级别的认证方案。当设置为 *off* 值时，认证失败的凭证将传递给下一个认证级别。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_145_0.png)

此模块的常见用途是结合基本的认证模块之一，如 `mod_auth.c`。虽然这个 DBM 模块提供了大部分的用户凭证检查，但一些（管理员）相关的访问会下降到较低级别，使用受良好保护的 `.htpasswd` 文件。

现在让我们来看一个如何使用基于 DBM 的用户名和密码的示例。假设你已经创建了用户 DBM 文件，你现在有能力限制访问你希望的任何 Web 目录。在以下示例中，我假设用户 DBM 文件是 `/www/secrets/myuser.dbm`。你可以使用 `<Directory>` 容器将认证方案添加到你的全局或虚拟服务器，或者你可以使用 `.htaccess` 文件——两者没有区别。示例配置如下所示：


AuthName "Apache Server Bible Readers Only"
AuthType Basic
AuthUserDBFile /www/secrets/myuserdbm
require valid-user

此时，Apache 使用 `mod_auth_dbm` 模块在此配置适用的目录中进行身份验证。

> **注意** 请确保只有 Apache 和文件所有者可以读取 DBM 文件。除 DBM 文件的所有者外，任何人都不应能够写入该文件。

### mod_auth_db

如果你的系统不支持使用 DBM，但可以使用 Berkeley DB 文件支持，你可以使用 `mod_auth_db` 来代替 DBM 模块使用 DB 文件进行 Apache 的身份验证。该模块在标准的 Apache 发行版中并未被编译包含。

在配置基于 DB 文件的身份验证模块之前，请确保你知道系统中 DB 库文件存储的位置。例如，在 Linux 系统中，这些文件位于标准的 `/usr/lib` 目录中。如果你的系统没有 DB 库，你将需要获取源代码并首先编译 DB 支持。你可以在 www.sleepycat.com 找到 DB 库的信息。

确认你的系统具有 DB 库后，你可以继续重新配置并重编译 Apache。使用 `configure` 脚本中的 `--enable-db` 选项为 Apache 源代码配置 Berkeley DB 支持，然后像平常一样编译和安装 Apache。

此时，你已准备好使用 `mod_auth_db` 模块。该 `mod_auth_db` 模块提供了 `AuthDBUserFile`、`AuthDBGroupFile` 和 `AuthDBAuthorize` 指令。

#### AuthDBUserFile

`AuthDBUserFile` 指令设置包含用户列表和加密密码的用户 DB 文件的完全限定路径名。

- **语法**：AuthDBUserFile *filename*
- **上下文**：Directory, per-directory access control file (`.htaccess`)
- **覆盖权限**：AuthConfig

与其 DBM 对应项类似，DB 用户文件也使用用户名作为键，而值则是经过 `crypt()` 加密的密码。

> **注意** 务必确保用户文件位于 Web 文档树之外，并且只有 Apache 可以读取。除所有者（即 Apache）外，任何人都不应拥有这些文件的写入权限。

#### AuthDBGroupFile

AuthDBGroupFile 指令设置组 DB 文件的完全限定路径名，该文件包含用于用户身份验证的用户组列表。与其 DBM 对应项类似，组文件使用用户名作为键，逗号分隔的组列表被视为值。值内部不能包含任何空白字符，且绝不应包含冒号。

- **语法**：AuthDBGroupFile *filename*
- **上下文**：Directory, per-directory access control file (.htaccess)
- **覆盖权限**：AuthConfig

如果你不希望使用单独的组文件，可以使用单个 DB 文件同时提供密码和组信息。该文件的格式为：

DB_File_Key(username) - encrypted_password; comma_separated_group_list

其中用户名是键，而密码和组列表是值的两个字段。在另一个冒号之后可以在 DB 文件中保留其他数据；身份验证模块会忽略这些数据。如果你使用单个 DB 文件同时提供组和密码信息，你必须将 AuthDBGroup 和 AuthDBUserFile 指令都指向同一个文件。

#### AuthDBAuthoritative

当在同一目录中使用多种身份验证方案（如 mod_db、mod_dbm 和标准 mod_auth）时，你可以使用 AuthDBAuthoritative 指令来定义 mod_auth_db 是否为权威身份验证方案。该指令的默认值使 mod_auth_db 成为该目录的权威身份验证方案。因此，如果基于 DB 的身份验证对特定用户失败，该用户的凭证不会传递给较低层级的身份验证方案。当设置为 Off 值时，身份验证失败的凭证会传递给下一个身份验证层级。

- **语法**：AuthDBAuthoritative On | Off
- **默认设置**：AuthDBAuthoritative On
- **上下文**：Directory, per-directory access control file (.htaccess)
- **覆盖权限**：AuthConfig

## 动态内容生成模块

此处讨论的模块使 Apache 能够运行 CGI 脚本、SSI、过滤器等。表 5-4 列出了这些模块。

**表 5-4**
**动态内容生成模块**

| 模块 | 用途 |
| :--- | :--- |
| *mod_cgi* | 运行 CGI 脚本。详细信息请参见第 12 章。 |
| *mod_include* | SSI 过滤器。详细信息请参见第 13 章。 |
| *mod_actions* | 基于媒体类型或请求方法执行 CGI 脚本。 |
| *mod_ext_filter* | 使用外部程序过滤输出。 |

### mod_actions

`mod_actions` 模块默认被编译。`mod_actions` 允许你基于 `MIME-type` 或 HTTP 请求方法运行 CGI 脚本。它提供以下指令。

#### Action

`Action` 指令允许你为特定的 MIME 类型关联一个操作。该操作通常是处理所请求文件的 CGI 脚本。这允许你为给定的 MIME 类型执行 CGI 脚本。

- **语法**：`Action` *MIME-type* *cgi_script*
- **上下文**：Server config, virtual host, directory, per-directory access control file (`.htaccess`)
- **覆盖权限**：`FileInfo`

例如，以下指令使 Apache 在请求 HTML 文件时始终运行指定的脚本：

```
Action text/html /cgi-bin/somescript.pl
```

该脚本通过标准环境变量 `CGI_PATH_INFO` 和 `PATH_TRANSLATED` 接收所请求文档的 URL 和文件路径。这在开发过滤脚本时很有用。本节讨论其中一个这样的过滤脚本。

当通过 Web 请求文本文件（`.txt`）时，它在 Web 浏览器上的显示格式并不理想，因为大多数 Web 浏览器不会以任何方式转换换行符。通常，大多数文本文件显示为一个大的段落。通过使用 `Action` 指令，你可以开发更好的解决方案。

举一个更有趣的例子，假设你现在想要开发一个解决方案，不仅要在 Web 浏览器上更好地显示文本文件，还要在每个文本文件的末尾插入版权声明。为了实现这一点，你需要做两件事。首先，在 httpd.conf 文件中添加以下指令：

```
Action plain/text /cgi-bin/textfilter.pl
```

然后，开发 Perl 脚本 textfilter，该脚本将以你希望的方式显示文本文件。列表 5-1 显示了这样一个脚本。你可以在随附 CD-ROM 的 Scripts/Chapter 5 目录中找到此脚本。

#### 列表 5-1：textfilter.pl

```perl
#!/usr/bin/perl
#
# Script: textfilter.pl
#
# Purpose: This filter script converts plain text files
#         into an HTML document but keeps the text layout
#         as is.
#
# Copyright (c) 2001 by Mohammed J. Kabir
#
# License: GPL
#
# The copyright message file is always stored in
# the server's document root
# directory and is called copyright.html.
my $copyright_file = $ENV{DOCUMENT_ROOT} . "/copyright.html";
# Get the requested document's path
my $path_translated = $ENV{PATH_TRANSLATED};

# Other variables needed for storing data
my $line;
my @text;
my @html;

# Store the path info and the file name of requested doc in an
array
@filename = split(/\/\/.{$path_translated};

# Because HTML tags are used to display the text file,
# lets print the text/html content header.
print "Content-type: text/html\n\n";

# Read the document requested and store the data
# in @text array variable
@text = &readFile($path_translated);
# Now print the following HTML document tags.
# These tags will be sent before the actual document content
#
print <<HEAD;
<HTML>
<HEAD><TITLE>$filename[-1] </TITLE> </HEAD>
<BODY BGCOLOR="white">
<BLOCKQUOTE>
<PRE>
HEAD
# Now print each line stored in the @text array
# (that is, the content of the document requested)
#
foreach $line (@text) { print $line; }
# Now read the copyright file and store the content
# in the @html array variable
#
@html = &readFile($copyright_file);
# Print each line stored in the @html array (that is,
# the content of the copyright message file)
#
foreach $line (@html){ print $line; }
# Exit the filter
exit 0;

sub readFile {
#
# Subroutine: readFile
# Purpose: Reads a file if it exists or else prints
# an error message and exits script
#
# Get the name of the passed file name and store
# it in variable $file
my $file = shift;
# Local buffer variable
my @buffer;
# If the file exists, open it and read all the
# lines into the @buffer array variable
if(-e $file) {
open(FP,$file) || die "Can not open $file:";
while(<FP>){
```





```perl
push(@buffer,$_);
}

close(FP);
} else {
push(@buffer,"$file is missing.");
}

# Return the content of the buffer.
return (@buffer);
}
```

前面的脚本读取请求的文本文件，并输出内容，内容被包裹在几个 HTML 标签内，以使其能够按原样显示。这是通过使用 HTML 标签 `<PRE>` 来实现的。在内容输出后，版权声明文件内容会被插入到输出的末尾。这使得每次请求的文本文件都能附带打印一条版权声明。图 5-1 展示了一个示例输出，其中文本文件正在 Web 浏览器上显示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_151_0.png)

正如你所见，请求的文件名显示为标题。文档被块引用（block quote），并打印了一条自定义的版权声明。版权声明文件存储在文档的根目录中。本例中使用的文件如下：

```html
</PRE>
</BLOCKQUOTE>
<CENTER>
<HR>
Copyright (c) 2001 Mohammed J. Kabir (kabir@mobidac.com)
</CENTER>
</BODY>
</HTML>
```

## Script

`Script` 指令类似于 `Action` 指令，但它不是将操作关联到 MIME 类型，而是将操作关联到 HTTP 请求，例如 `GET`、`POST`、`PUT` 或 `DELETE`。CGI 脚本通过标准的 CGI `PATH_INFO` 和 `PATH_TRANSLATED` 环境变量获取所请求文档的 URL 和文件路径。

**语法：** `Script method cgi-script`

**上下文：** 服务器配置、虚拟主机、目录

该指令定义默认操作。换句话说，如果你定义了如下配置：

```apache
Script POST /cgi-bin/default_post.pl
```

在 Apache 配置文件（如 `srm.conf`）中，那么每当通过 HTTP POST 方法发出请求时，它都会按常规处理，除非需要使用该指令指定的默认操作。例如，以下 HTML 表单没有指定 CGI 脚本作为其操作：

```html
<FORM METHOD="POST">
    Enter Name: <INPUT TYPE=TEXT NAME="name" SIZE=25>
    <INPUT TYPE=SUBMIT VALUE="Click Here">
</FORM>
```

如果用户通过此表单提交了一个姓名，由于没有指定用于处理该信息的 CGI 脚本，此时将运行默认的 POST 操作 `/cgi-bin/default_post.pl` 脚本。然而，如果将 `<FORM ...>` 标签修改为：

```html
<FORM ACTION="/cgi-bin/form_processor.pl" METHOD="POST">
```

那么每当表单提交时，将按常规调用 `/cgi-bin/form_processor.pl` 脚本。在默认操作脚本中执行什么操作取决于你。在 Internet 服务提供商的配置中，我建议让默认脚本打印有意义的消息，以便 HTML 表单开发人员能够意识到自己哪里做错了。

对于 GET 请求，只有当请求附带查询数据时才会使用默认操作。例如，`www.your_site.com/somefile.html` 将按常规处理，但如果收到类似 `http://www.your_site.com/somefile.html?some=data` 的请求，则 GET 的默认操作将被执行。

## mod_ext_filter

`mod_ext_filter` 模块使 Apache 能够使用外部程序作为输入和输出过滤器。任何能从 `STDIN` 读取输入并写入 `STDOUT` 输出的程序都可以使用。当然，为每个请求运行外部程序来处理输入或输出是一个耗时任务，在生产环境中应避免这样做。过滤器最好使用 Apache API（应用程序编程接口）开发，并在 Apache 服务器进程内运行。

### ExtFilterDefine

*ExtFilterDefine* 指令允许你定义一个过滤器，该过滤器随后可以通过此指令中指定的过滤器名称来使用。

**语法：** `ExtFilterDefine filter_name [mode=input | output]` `[intype=MIME-type]` `[outtype=MIME-type]` `[PreservesContentLength]`

**上下文：** `服务器配置`

在下面的示例中，定义了一个名为 `gzfilter` 的过滤器，它是一个输出过滤器（`mode=output`），当被调用时运行 `/usr/bin/gzip` 程序：

```apache
ExtFilterDefine gzfilter mode=output cmd=/usr/bin/gzip
```

这里，*mode* 只能设置为 *output*。*intype* 和 *outtype* 设置用于定义输入和输出使用的 MIME 类型。例如，如果一个过滤器接收 `intype=text/plain` 和 `outtype=text/html`，则该过滤器负责将数据从纯文本格式转换为 HTML 格式。当过滤器不改变数据的字节大小时，应使用 `PreservesContentLength` 参数。

假设你有一个名为 `/usr/local/bin/program` 的自定义过滤器程序，并希望将其用作名为 `/www/mysite/htdocs/mytxts` 的 Web 目录中所有纯文本文件的输出过滤器。以下是一个示例配置，允许你实现这一点：

```apache
ExtFilterDefine my_test_filter \
mode=output cmd=/usr/local/bin/program \
intype=text/plain \
outtype=text/html

<Directory "/www/mysite/htdocs/mytxts">
SetOutputFilter my_test_filter
AddType text/html
</Directory>
```

这里 `ExtFilterDefine` 定义了一个名为 `my_filter` 的过滤器，当被调用时运行 `/usr/local/bin/program`，它从 STDIN 接收 text/plain 数据，并将 text/html 数据写入 STDOUT。现在 `<Directory>` 容器将此过滤器设置为该目录的输出过滤器，并使用 `AddType` 指令告知 Apache 输出 MIME 类型是 text/html。如果你在此目录中存储文本文件，并且 Web 客户端请求它们，这些文件将通过 `/usr/local/bin/program` 转换为 HTML。

### ExtFilterOptions

*ExtFilterOptions* 指令为模块设置调试选项。当需要设置调试时，使用 `DebugLevel` 选项。将此选项设置为 `0` 会禁用调试，这是默认行为。将其设置为 `1` 会启用显示选项的调试日志条目。将其设置为 `9` 会启用过滤器处理的所有详细细节。

**语法：** ExtFilterOptions DebugLevel=*n* LogDebugr | NoLogStderr

**上下文：** 服务器

## Content-Type 配置模块

本节中介绍的模块（见表 5-5）使你能够配置、检测和协商适合服务请求的内容类型。

| 模块 | 用途 |
| :--- | :--- |
| mod_mime | 允许 Apache 通过文件扩展名确定 MIME 类型。 |
| mod_mime_magic | 允许 Apache 通过魔数（字节模式）确定 MIME 类型。 |
| mod_negotiation | 允许 Apache 执行内容协商，以发送客户端可接受的最佳类型内容。 |

## mod_mime

*mod_mime* 模块在 Apache 中默认编译。它为客户端提供关于文档的元信息。它还允许你为文档定义一个处理器，以确定 Apache 如何处理该文档。

### AddCharset

*AddCharset* 指令将一个或多个文件扩展名映射到 MIME 字符集。这允许你将一个字符集关联到一个或多个文件扩展名。

**语法：** AddCharset charset file_extension [file_extension ...]

**上下文：** 服务器配置、虚拟主机、目录、逐目录配置 (.htaccess)

**覆盖：** FileInfo

以下示例将使名为 `filename.utf8` 的文件映射为名为 UTF-8 的字符集。

```apache
AddCharset UTF-8 .utf8
```

### AddEncoding

`AddEncoding` 指令将一个或多个文件扩展名映射到 MIME *编码* 方案。换句话说，此指令将一个编码方案关联到一个或多个文件扩展名。

-   **语法：** `AddEncoding` *MIME* *file_extension* [*file_extension*...]
-   **上下文：** 服务器配置、虚拟主机、目录、逐目录配置 (`.htaccess`)
-   **覆盖：** `FileInfo`

例如，以下指令将使名为 `backup.gz` 的文件映射为 *x-gzip* 编码文件，而名为 `tarball.tar` 的文件映射为 *x-tar* 编码文件。

```apache
AddEncoding x-gzip gz
AddEncoding x-tar tar
```

### AddHandler

`AddHandler` 指令为一个或多个文件扩展名定义处理器。每当 Apache 遇到具有已定义处理器的文件时，它允许该处理器处理文件。

-   **语法：** `AddHandler` *handler-name* *file-extension* [*file-extension* ...]
-   **上下文：** 服务器配置、虚拟主机、目录、逐目录访问控制文件 (`.htaccess`)

在以下示例中：该指令指定所有 `.cgi` 文件由名为 `cgi-script` 的处理器处理。

```apache
AddHandler cgi-script .cgi
```

### AddLanguage

`AddLanguage` 指令将文件扩展名列表映射到 MIME 语言。当 Apache 遇到具有此类扩展名的文件时，它知道该文件支持什么语言。

-   **语法：** `AddLanguage` *MIME_language* *file_extension* [*file_extension*] [...]





**上下文：** 服务器配置、虚拟主机、目录、单目录访问控制文件 (`.htaccess`)
**可覆盖级别：** `FileInfo`

以下示例将扩展名为 `.en` 或 `.english` 的所有文件映射为英语语言文件。这在内容协商中非常有用，服务器可以根据客户端的语言偏好返回文档。

```
AddLanguage en .en .english
```

或者，在下面的示例中，如果客户端偏好英语文档，并且 `document.fr.html` 和 `document.en.html` 都可用，服务器应返回 `document.en.html`。

```
AddLanguage en .en
AddLanguage fr .fr
```

### AddType

`AddType` 指令将一组文件扩展名映射到一个 MIME 类型，以便当 Apache 遇到具有这些扩展名的文件时，知道应使用何种 MIME 类型。

**语法：** `AddType MIME file_extension [file_extension ...]`
**上下文：** 服务器配置、虚拟主机、目录、单目录访问控制文件 (`.htaccess`)
**可覆盖级别：** `FileInfo`

例如，以下行将名为 `text/html` 的 MIME 类型与 `htm`、`html`、`HTM` 和 `HTML` 扩展名关联。

```
AddType text/html htm html HTM HTML
```

### DefaultLanguage

`DefaultLanguage` 指令设置默认语言。

**语法：** `DefaultLanguage MIME_language`
**上下文：** 服务器配置、虚拟主机、目录、单目录访问控制文件 (`.htaccess`)
**可覆盖级别：** `FileInfo`

例如，在以下指令中，`/www/mysite/japanese` 目录中的所有内容都映射到默认语言：日语

```
<Directory /www/mysite/japanese>
DefaultLanguage .jp
</Directory>
```

### ForceType

**ForceType** 指令强制指定目录中所有文件的特定 MIME 类型。该目录可以通过 `<Directory>` 或 `<Location>` 容器来指定。

- **语法：** `ForceType MIME_type`
- **上下文：** 目录、单目录访问控制文件 (`.htaccess`)

例如，以下指令强制指定目录中所有文件的 MIME 类型为 `text/html`，无论其扩展名如何：

```
<Directory /www/nitec/public/htdocs/files/with/no/extensions>
  ForceType text/html
</Directory>
```

### SetHandler

**SetHandler** 指令为目录或 URL 位置定义一个处理器。然后使用该处理器来处理目录中的所有文件。

- **语法：** `SetHandler handler_name`
- **上下文：** 目录、单目录访问控制文件 (`.htaccess`)

例如，以下指令强制将 `/bin` 位置下的所有文件视为 CGI 脚本，由 `cgi-bin` 处理器处理：

```
<Location /bin>
  Options ExecCGI
  SetHandler cgi-bin
</Location>
```

### RemoveHandler

**RemoveHandler** 指令取消目录或 URL 位置的处理器。这对于限制 **SetHandler** 非常有用，因为 SetHandler 通常应用于目录中的所有文件。使用 **RemoveHandler**，您可以移除某些文件或甚至子目录的处理器。

- **语法：** `RemoveHandler handler_name`
- **上下文：** 目录、单目录访问控制文件 (`.htaccess`)

例如，在以下指令中，处理器 `my-handler` 在 `/www/mysite/htdocs/special` 目录之外被设置为 `.mjk` 扩展名，因此它会自动应用于该目录。然而，由于对**该目录应用了 RemoveHandler** 以取消 `my-handler` 与 `.mjk` 的关联，该目录中具有 `.mjk` 扩展名的文件将不会由 `my-handler` 处理：

```
SetHandler my-handler .mjk

<Directory /www/mysite/htdocs/special>
RemoveHandler .mjk
</Directory>
```

### TypesConfig

`TypesConfig` 指令指定默认的 MIME 配置文件。对于大多数 Apache 安装，默认值通常就足够了。如果您想添加自定义的 MIME 类型，请使用 `AddType` 指令，而不是修改此文件。

**语法：** `TypesConfig filename`

**默认设置：** `TypesConfig conf/mime.types`

**上下文：** 服务器配置

> **注意**
> 如果您需要额外的支持来处理 `MIME types`，您可能需要查看下一节中的 `mod_mime_magic` 模块。对于大多数 Apache 安装，这不是必需的，因此本书中未对其进行讨论。

### mod_mime_magic

`mod_mime_magic` 模块使 Apache 能够通过将文件的几个字节与存储在文件中的魔术值进行比较来确定文件的 MIME 类型。只有当 `mod_mime` 无法猜测文件的 MIME 类型时才需要此模块。在大多数情况下，您不需要此模块。该模块有一个名为 `MimeMagicFile` 的指令。

此指令启用 `mod_mime_magic` 模块并指向该模块所需的魔术文件。Apache 发行版在 `conf` 子目录中附带了一个魔术文件，因此如果您希望使用此模块，请将此指令设置为 `conf/magic`。

**语法：** `MimeMagicFile magic_file_filename`

**上下文：** 服务器配置、虚拟主机

### mod_negotiation

`mod_negotiation` 模块默认编译进 Apache。它提供对内容协商的支持。在典型的内容协商场景中，客户端提供关于其可处理的内容类型的信息，服务器则尝试提供最合适的内容。服务器借助类型映射表和 `MultiViews` 搜索来完成此操作。

*类型映射表*提供了对文档的描述。每个文档描述包含一个或多个标题。它还可以包含以井号 (#) 字符开头的注释行。文档描述之间以空行分隔。文档描述的标题如下：

- **Content-Encoding** — 指定文件的编码类型。目前仅允许 x-compress 和 x-gzip 编码。
- **Content-Language** — 文档的语言。
- **Content-Length** — 文件的字节长度。
- **Content-Type** — 文档的 MIME 类型。允许可选的关键值参数。允许的参数有 level，提供 MIME 类型的版本号（作为整数），以及 qs，表示文档的质量（作为浮点数）。
- **URI** — 相对于映射文件的文档路径。

MultiViews 搜索尝试利用从客户端获取的信息来确定缺失文档的最接近匹配项，并尽可能返回匹配项。当您在 Options 指令中启用 MultiViews 选项时，如果请求的文档未找到，服务器就能够执行 MultiViews 搜索。此模块提供以下两个指令。

### CacheNegotiatedDocs

CacheNegotiatedDocs 指令启用由代理服务器缓存经内容协商的文档。请注意，新的 HTTP 1.1 规范为缓存协商文档提供了更好的控制机制，且 CacheNegotiatedDocs 对 HTTP 1.1 请求没有影响。随着 HTTP 1.1 的广泛使用，此指令可能会消失。不推荐使用 CacheNegotiatedDocs。

**语法：** CacheNegotiatedDocs

**上下文：** 服务器配置

### LanguagePriority

LanguagePriority 指令指定在 MultiViews 搜索场景中，当客户端未提供语言偏好信息时，服务器应使用的语言偏好。

**语法：** LanguagePriority _MIME_language_ [_MIME_language_ ...]

**上下文：** 服务器配置、虚拟主机、目录、单目录访问控制文件 (`.htaccess`)

**可覆盖级别：** FileInfo

例如，在以下指令中，如果 MultiViews 选项已开启，且客户端对于缺失的文件未提供语言偏好信息，服务器首先尝试提供最接近匹配的英语版本，然后是法语版本，依此类推。与 CacheNegotiatedDocs 指令一样，此指令在 HTTP 1.1 环境中无效。

```
LanguagePriority en fr de
```

如果您的 Web 文档树中有一个目录没有目录索引文件（使用 `DirectoryIndex` 指令设置），那么如果您未使用 `Options -Indexes` 指令禁用自动目录列表，Apache 将自动生成分页列表。Apache 允许您自定义自动生成的目录列表。本节中的模块，如表 5-6 所示，使您能够配置目录列表的显示方式。

**表 5-6 目录列表模块**

| 模块 | 用途 |
| :--- | :--- |
| mod_dir | 基本目录处理 |
| mod_autoindex | 自动目录列表 |

### mod_dir

`mod_dir` 模块默认编译在 Apache 中。使用此模块，Apache 可以重定向任何不包含结尾正斜杠字符的目录请求。例如，此模块可以将 `www.yoursite.com/somedirectory` 重定向到 `www.yoursite.com/somedirectory/`。它还提供了 `DirectoryIndex` 指令来协助索引目录内容。

`DirectoryIndex` 指令指定在创建动态目录索引之前，Apache 应查找的文件名称。文件可以是 HTML 文件，也可以是 CGI 脚本。默认设置使 Apache 在请求以目录名结尾时查找 `index.html` 文件。

- **语法：** `DirectoryIndex local_URL [local_URL...]`
- **默认设置：** `DirectoryIndex index.html`
- **上下文：** 服务器配置、虚拟主机、目录、单目录访问控制文件 (`.htaccess`)
- **可覆盖级别：** `Indexes`

例如，`www.yoursite.com/some/directory/` 会导致 Apache 查找名为 `/some/directory/index.html` 的文件。如果文件存在，其内容将提供给客户端。如果该文件不存在，Apache 将创建动态目录列表。

您可以指定一个或多个文件作为默认目录索引文件。例如，以下配置告诉 Apache 为每个目录请求查找所有列出的文件：

```
DirectoryIndex index.html index.htm welcome.html welcome.htm
```





请注意，Apache 查找文件的顺序与上述配置中显示的顺序（从左到右）相同。换句话说，如果 Apache 找到了 `index.html`，它将不再查找 `index.htm`、`welcome.html` 或 `welcome.htm`。你还可以将 CGI 脚本名称指定为默认索引。例如，以下指令使 Apache 在处理目录请求时始终运行 `/cgi-bin/show_index.cgi` 脚本：

```
DirectoryIndex /cgi-bin/show_index.cgi
```

## mod_autoindex

mod_autoindex 模块在 Apache 中默认被编译。当 Apache 接收目录请求时，它会查找由 DirectoryIndex 指令指定的一个或多个目录索引文件。通常，此文件是 `index.html` 或 `index.htm`。然而，如果没有这样的索引文件，Apache 可以生成动态目录列表。该模块允许你控制 Apache 如何创建动态目录列表。

Apache 生成两种类型的动态目录索引：简单和详细。详细索引以及许多其他索引选项可从该模块获得。mod_autoindex 的指令如下。

### AddAlt

当启用 FancyIndexing 时，此指令将为参数中指定的一个或多个文件或文件扩展名设置的图标设置替代文本。这是针对非图形浏览器（如 Lynx）完成的。

- **语法：** AddAlt "text" filename [filename ...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令使 Apache 能够针对此处指定的每种图形文件类型显示替代文本“Pictures”以取代图标。对于图形浏览器，如 Netscape Navigator 或 Internet Explorer，替代文本在流行的 Windows 平台上显示为帮助文本。在这样的系统中，当用户将鼠标光标移动到代表某类文件的图标上方时，可以获得关于该文件的提示或帮助：

```
AddAlt "Pictures" gif jpeg jpg bmp
```

### AddAltByEncoding

如果你不想通过 AddAlt 指令为文件名或文件扩展名分配替代文本，你可以使用 AddAltByEncoding 指令为一个或多个 MIME 编码分配此类文本。与 AddAlt 一样，此指令也仅在启用 FancyIndexing 时可用。

- **语法：** AddAltByEncoding "text" MIME_encoding [MIME_encoding ...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令使 Apache 对所有 MIME 类型为 x-compress 的文件显示“Compressed File”替代文本。

```
AddAltByEncoding "Compressed File" x-compress
```

### AddAltByType

与 AddAltByEncoding 指令类似，AddAltByType 指令为文件设置替代文本，而不是为 FancyIndexing 设置图标。但是，它使用 MIME 类型而不是 MIME 编码。

- **语法：** AddAltByType "text" MIME_type [MIME_type ...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令针对非图形浏览器显示“HTML FILE”文本以取代图标。对于图形浏览器，此文本可能作为提示或帮助出现：

```
AddAltByType "HTML FILE" text/html
```

### AddDescription

当启用 FancyIndexing 时，AddDescription 指令为文件名、部分文件名或通配符文件名设置描述文本。

- **语法：** AddDescription "text" file [ file ... ]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令在生成的目录列表中显示所有 GIF、JPEG、JPG 和 BMP 文件的描述：

```
AddDescription "Graphics File" *.gif *.jpeg *.jpg *.bmp
```

### AddIcon

AddIcon 指令允许你为显示在 FancyIndexing 中的文件和目录名称分配图标。

- **语法：** AddIcon icon name file [filename ...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令告诉 Apache 在具有 .gif、.jpg 和 .bmp 等扩展名的文件旁边显示 /icons/picture.gif：

```
AddIcon /icons/picture.gif .gif .jpg .bmp
```

如果你还想为列出的文件扩展名提供替代文本，可以使用如下格式，其中 IMG 是为非图形浏览器显示的替代文本：

```
AddIcon (IMG. /icons/picture.gif) .gif .jpg .bmp
```

如果你想为目录显示图标，可以如下使用该指令：

```
AddIcon /path/to/your/directory/icon ^^DIRECTORY^^
```

同样地，如果你想为详细索引方案显示的每个空白行显示一个图标，可以使用：

```
AddIcon /path/to/your/blank/line/icon ^^BLANKICON^^
```

### AddIconByEncoding

AddIconByEncoding 指令允许你为 MIME 编码分配图标。换句话说，你可以将图标图像分配给 MIME 类型。

- **语法：** AddIconByEncoding icon_file MIME_encoding [MIME_encoding ...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下 AddIconByEncoding 指令告诉 Apache 对所有 x-gzip（即 .gz 扩展名）MIME 类型文件显示 /icons/zip.gif 图标。

```
AddIconByEncoding /icons/zip.gif x-gzip
```

### AddIconByType

AddIconByType 指令也允许你为一个或多个 MIME 类型分配图标。

- **语法：** AddIconByType icon_file MIME_type [MIME_type...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下 AddIconByType 指令告诉 Apache 为所有 text/html 文件显示 /icons/html.gif 图标。

```
AddIconByType (HTML,/icons/html.gif) text/html
```

### DefaultIcon

当没有为文件匹配任何 AddIcon、AddIconByEncoding 或 AddIconByType 时，可以显示默认图标。DefaultIcon 指令允许你设置该图标。

- **语法：** DefaultIcon URL
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令每当文件的图标关联未知时显示 idontknow.gif：

```
DefaultIcon /icon/idontknow.gif
```

### FancyIndexing

FancyIndexing 指令允许你启用或禁用目录的详细索引。你可以通过 IndexOptions 指令实现相同的效果。

- **语法：** FancyIndexing On | Off
- **上下文：** 服务器配置、虚拟主机、目录、每目录配置（.htaccess）
- **覆盖：** Indexes

### HeaderName

如果你使用 FancyIndexing，可以在索引列表的顶部插入文件内容。HeaderName 指令允许你指定用于此类插入的文件名。

- **语法：** HeaderName filename
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令告诉 Apache 在列表目录中查找名为 welcome 或 welcome.html 的文件；如果找到此类文件，内容将插入在实际列表之前：

```
HeaderName welcome
```

### IndexIgnore

如果你需要某些文件或文件扩展名在目录列表中不可见，可以使用 IndexIgnore 指令来实现这一点。

- **语法：** IndexIgnore file [file...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes

例如，以下指令确保 Apache 不在目录列表中列出 welcome、welcome.html 或每目录配置文件（.htaccess）：

```
IndexIgnore welcome welcome.html .htaccess
```

点号（.）字符自动包含在 IndexIgnore 列表中；因此，以该字符开头的文件不会被列出。然而，你可能仍倾向于将每目录配置文件（.htaccess）添加到列表中，只是为了让你感到更安全。

### IndexOptions

IndexOptions 指令指定自动生成的目录索引的行为。

- **语法：** IndexOptions option [option] [...]
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- **覆盖：** Indexes





## IndexOptions
表 5-7 展示了您可以与 `IndexOptions` 配合使用的选项。

| 选项 | 作用 |
|---|---|
| `FancyIndexing` | 开启目录的花式索引。注意，`FancyIndexing` 和 `IndexOptions` 指令会**相互覆盖**。 |
| `IconHeight[=pixels]` | 允许 Apache 在图标的 `IMG` 标签中包含 `HEIGHT=pixels` 属性，这使得大多数浏览器加载图标时速度更快。如果您未指定像素值，则使用标准默认值。 |
| `IconsAreLinks` | 使图标成为文件名锚点的一部分，用于花式索引。 |
| `IconWidth[=pixels]` | 允许 Apache 在图标的 `IMG` 标签中包含 `WIDTH=pixels` 属性，这使得大多数浏览器加载图标时速度更快。如果您未指定像素值，则使用标准默认值。 |
| `ScanHTMLTitles` | 如果您希望 Apache 读取 HTML 文档的标题（由 `<TITLE>` 和 `</TITLE>` 标签对标识）以进行花式索引，请使用此选项。但是，如果您已使用 `AddDescription` 指令指定了描述，则不会使用此选项。请注意，读取每个文件的内容并搜索标题信息是一个耗时任务，可能会减慢目录列表的生成速度。我不推荐此选项。 |
| `SuppressColumnSorting` | 默认情况下，Apache 会为花式目录索引创建可点击的列标题，这允许用户对该列中的信息进行排序。此选项将禁用该功能。 |
| `SuppressDescription` | 如果您不想在花式目录列表中显示文件描述，请使用此选项。 |
| `SuppressHTMLOreamble` | 如果目录确实包含由 `HeaderName` 指令指定的文件，该模块通常会在标准 HTML 前导内容（`<HTML>`、`<HEAD>` 等）之后包含该文件的内容。`SuppressHTMLOreamble` 选项会禁用此行为。 |
| `SuppressLastModified` | 抑制在花式索引列表中显示最后修改日期。 |
| `SuppressSize` | 抑制在花式索引列表中显示文件大小。 |

## IndexOrderDefault

IndexOrderDefault 指令允许您通过排序名称、日期、大小和描述等各个字段来更改目录列表视图，这些目录是使用 FancyIndexing 功能显示的。

- **语法：** IndexOrderDefault Ascending | Descending Name | Date | Size | Description
- **上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (.htaccess)
- **覆盖：** Indexes

## ReadmeName

如果您希望在花式目录列表的末尾插入一个文件，请使用 ReadmeName 指令。

- **语法：** ReadmeName filename
- **上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (.htaccess)
- **覆盖：** Indexes

例如，以下设置使 Apache 查找名为 readme.html（默认扩展名）或 readme 的文件并将其插入到列表末尾：

```
ReadmeName readme
```

## Response Header Modules

Apache 允许您在发送数据时发送自定义 HTTP 响应头。本节中的模块如表 5-8 所示，允许您配置各种自定义响应头。

表 5-8 响应头模块

| 模块 | 用途 |
| --- | --- |
| mod_alias | 发送包含自身 HTTP 头的文件。 |
| mod_headers | 为资源添加任意 HTTP 头。 |
| mod_expires | 为资源应用 Expires 头。 |
| mod_cern_meta | 支持 HTTP 头元文件。 |

### mod_asis

*mod_asis* 模块默认已编译。此模块允许您原样发送文档——也就是说，文档在不带 HTTP 头的情况下发送给客户端。这在不需要脚本帮助的情况下重定向客户端时非常有用。要原样发送文件，您需要确保 *httpd.conf* 文件包含如下条目：

```
AddType httpd/send-as-is .asis
```

这将 *httpd/send-as-is* MIME 类型分配给文件扩展名 *.asis*。如果您创建一个名为 *foobar.asis* 的文件并且客户端请求它，该文件将在没有 HTTP 头的情况下发送给客户端。您需要在文件中包含适当的头。例如，如果您想通过 *.asis* 文件提供重定向机制，您可以创建具有如下头的文件：

```
Status: 301 Text Message
Location: new-URL
Content-type: text/html
```

清单 5-2 展示了一个名为 *redirect.asis* 的文件，它将客户端重定向到新位置。

清单 5-2: *redirect.asis*

```
Status: 301 We have moved.
Location: http://www.our-new-site/
Content-type: text/html
<H1>Notice to Visitors</H1>
Please update your bookmark to point to <A HREF="http://www.our-new-site/ "> www.our-new-site/ </A><BR>
<BR>
Thanks.
```

当客户端请求此文件时，301 状态消息告诉客户端使用位置信息来重定向请求。您不需要添加 *Date:* 和 *Server:* 头，因为服务器会自动添加它们。但是，服务器不提供 *Last-Modified* 头。

### mod_headers

此模块默认未编译。*mod_headers* 允许您操作 HTTP 响应头，它提供了一个名为 *Header* 的指令，使您能够操作 HTTP 响应头。

语法: Header action header value

上下文: 服务器配置，虚拟主机，目录，每目录访问控制文件 (.htaccess)

覆盖: FileInfo

允许的操作如下：

| 操作 | 作用 |
|---|---|
| Set | 设置一个头。如果存在同名旧头，其值将更改为新值。 |
| Add | 添加一个头。如果一个或多个同名头已存在，这可能导致出现多个同名头。 |
| Append | 将值追加到现有头的值后面。 |
| Unset | 移除一个头。 |

例如，以下指令添加了值为 "Mohammed J. Kabir" 的 Author 头：

```
Header add Author "Mohammed J. Kabir"
```

以下行移除相同的头：

```
Header unset Author
```

## mod_expires

mod_expires 模块在 Apache 中默认未编译。它让您决定 Apache 如何处理服务器对请求的响应中的 Expires HTTP 头。Expires HTTP 头提供了一种告诉客户端请求的资源何时失效的方法。当文档被客户端缓存且需要再次请求时，这很有用。大多数智能客户端通过检查由 Expires HTTP 头提供的缓存文档的过期时间来确定请求文档的有效性。此模块允许您控制 Expires HTTP 头的设置。

### ExpiresActive

ExpiresActive 指令启用或禁用 Expires 头的生成。它并不保证会生成 Expires 头。如果条件不满足，则不会发送头。

**语法：** *ExpiresActive* On | Off

**上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (`.htaccess`)

**覆盖：** Indexes

### ExpiresByType

*ExpiresByType* 指令指定特定 *MIME 类型* 文档的 *Expires* HTTP 头的值。过期时间以秒为单位指定。您可以以两种方式定义时间。如果您选择使用 *Mseconds* 格式指定过期时间，则使用文件的最后修改时间作为基准时间。也就是说，*M3600* 意味着您希望文件在最后修改后一小时过期。另一方面，如果您使用 *Aseconds* 格式，则使用客户端的访问时间作为基准时间。以下是一些示例。

**语法 1：** *ExpiresByType* *MIME 类型* *Mseconds* | *Aseconds*

**语法 2：** *ExpiresByType* *MIME 类型* "*base_time* [plus] *num* *Years* | *Months* | *Weeks* | *Days* | *Hours* | *Minutes* | *Seconds*"

**上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (`.htaccess`)

**覆盖：** Indexes

以下操作使所有纯文本文件在客户端缓存中一小时后过期：

```
ExpiresByType text/plain A3600
```

以下操作使所有 GIF 文件在最后一次修改时间一周后过期：

```
ExpiresByType image/gif M604800
```

如果您想使用第二种语法来指定过期时间，您需要使用以下选项确定 *base_time* 的适当值：

| 值 | 含义 |
| :--- | :--- |
| Access | 客户端访问文件的时间。 |
| Now | 当前时间。这与访问时间相同。 |
| Modification | 文件最后更改的时间。 |

例如，以下指令告诉 Apache 发送头以告知浏览器 HTML 文档应在访问日期七天后过期，而 GIF 图像应在文件更改后或三小时十分后过期。





## ExpiresByType

```text
ExpiresByType text/html "access plus 7 days"
ExpiresByType image/gif "modification plus 3 hours 10 minutes"
```

### ExpiresDefault

`ExpiresDefault` 指令为指定上下文中的所有文档设置默认的过期时间。例如，如果该指令在虚拟主机上下文中指定，它仅适用于通过该虚拟主机可访问的文档。类似地，你可以在每目录上下文中指定此指令，这将允许该目录中的所有文档在指定的时间间隔内过期。有关语法的详细信息，请参阅 `ExpiresByType`。

- **语法 1：** `ExpiresDefault Mseconds | Aseconds`
- **语法 2：** `ExpiresDefault "base_time [plus] num Years|Months|Weeks|Days|Hours|Minutes|Seconds"`
- **上下文：** 服务器配置、虚拟主机、目录、每目录访问控制文件 (`.htaccess`)
- **可覆盖：** Indexes

以下是两个示例：

```text
ExpiresDefault M3600
ExpiresDefault "access plus 2 days"
```

第一个示例将过期时间设置为文档最后修改时间后一小时。第二个示例将过期时间设置为客户端访问后两天。

## mod_cern_meta

`mod_cern_meta` 模块默认未编译。它提供对元信息的支持。这些信息可以是额外的 HTTP 头部，例如：

```text
Expires: Saturday, 19-May-01 12:00:00 GMT
```

也可以是其他任何信息，如下例所示，元信息存储在文件中，并随 HTTP 响应头一起出现：

```text
Foo=Bar
```

### MetaFiles

`MetaFiles` 指令启用或禁用元头文件处理。

- **语法：** `MetaFiles On | Off`
- **默认设置：** `MetaFiles Off`
- **上下文：** 每目录访问控制文件 (`.htaccess`)

### MetaDir

MetaDir 指令指定存储元头文件的目录名称。例如，如果你有一个名为 `/www/mycompany/public/htdocs` 的目录，并希望为该目录存储元信息文件，且你使用 MetaDir 指令的默认值，则你需要创建一个名为 `.web` 的子目录。`.web` 目录存储元头文件。

- **语法：** `MetaDir directory`
- **默认设置：** `MetaDir .web`
- **上下文：** 每目录访问控制文件 (`.htaccess`)

### MetaSuffix

MetaSuffix 指令指定元信息文件的文件扩展名。例如，如果你有一个名为 `mypage.html` 的 HTML 文件，那么你需要创建 `mypage.html.meta`（使用此指令的默认值）来存储你的元头。`mypage.html.meta` 文件必须位于 MetaDir 指令指定的目录中。

- **语法：** `MetaSuffix suffix`
- **默认设置：** `MetaSuffix .meta`
- **上下文：** 每目录访问控制文件 (`.htaccess`)

若要使 Apache 为名为 `/www/mycompany/public/htdocs` 的目录发送元信息，你需要执行以下操作：

1.  在 `/www/mycompany/public/htdocs` 的每目录配置文件 (`.htaccess`) 中设置 MetaFiles 指令为开启状态。你也可以在此文件中设置 MetaDir 和 MetaSuffix 指令。
2.  创建一个名为 `.web` 的子目录（假设你使用的是 MetaDir 指令的默认值）。
3.  创建一个扩展名为 `.meta` 的文本文件（假设你使用的是 MetaSuffix 指令的默认值）。
4.  将你想要提供的所有 HTTP 头放入此文件中。

例如，要为名为 `/www/mycompany/public/htdocs/mypage.html` 的文件提供元头，你需要创建一个名为 `/www/mycompany/public/htdocs/.web/mypage.html.meta` 的文件。该文件可以包含如下行：

```text
Expires: Saturday, 19-May-01 12:00:00 GMT
Anything=Whatever
```

# 服务器信息和日志模块

本节中的模块，如表 5-9 所示，使你能够记录访问、报告服务器状态和配置信息，并跟踪使用 cookie 的用户。

表 5-9

**服务器信息和日志模块**

| 模块 | 用途 |
| :--- | :--- |
| **mod_log_config** | 提供可定制的访问日志。详细信息请参见第 8 章。 |
| **mod_status** | 显示状态信息。详细信息请参见第 8 章。 |
| **mod_info** | 显示服务器配置信息。详细信息请参见第 8 章。 |
| **mod_usertrack** | 通过 HTTP Cookie 提供用户跟踪。详细信息请参见第 8 章。 |

## mod_log_config

本模块在第 8 章中详细讨论。请参阅本章节中的“创建日志文件”部分，以了解有关本模块及其指令的更多信息。

## mod_status

本模块在第 8 章中详细讨论。请参阅本章节中的“使用 `mod_status` 启用状态页面”部分，以了解有关本模块及其指令的更多信息。

## mod_info

本模块在第 8 章中详细讨论。请参阅本章节中的“使用 `mod_info` 访问配置信息”部分，以了解有关本模块及其指令的更多信息。

## mod_usertrack

本模块在第 8 章中详细讨论。请参阅本章节后面部分的“记录 Cookie”部分，以了解有关本模块及其指令的更多信息。

# URL 映射模块

本节中的模块，如表 5-10 所示，使你能够将各种 URL 映射到特定的物理目录，创建复杂的重写规则、别名，以及自动化虚拟主机 URL 到物理目录的映射。

表 5-10

**URL 映射模块**

| 模块 | 用途 |
| :--- | :--- |
| `mod_userdir` | 允许你访问存储在用户主目录中的个人网站。 |
| `mod_rewrite` | 使用此模块创建 URL 重写规则。详细信息请参见第 9 章。 |
| `mod_alias` | 用于将文档树中主机文件系统的不同部分映射以及进行 URL 重定向。 |
| `mod_speling` | 自动纠正 URL 中的小拼写错误。 |
| `mod_vhost_alias` | 支持动态配置的大量虚拟托管。 |

## mod_userdir

`mod_userdir` 模块使 Apache 能够启用用户特定的 Web 目录，这些目录可通过 `http://your_server_name/~username` 访问。如果你不打算支持此类网站，则不需要此模块。

UserDir 指令（此模块中唯一的指令）允许你设置 Apache 应作为用户 Web 站点文档根目录的目录。

- **语法：** `UserDir directory_filename`
- **默认设置：** `UserDir public_html`
- **上下文：** 服务器配置、虚拟主机

例如，如果你保留默认值，每当 Apache 注意到请求 URL 中服务器名称后的 `~username` 路径时，它将 `~username` 转换为 `user_home_directory/public_html`。如果用户主目录存储在 `/home` 中，则转换后的路径为 `/home/username/public_html`。

> **注意** 你应该添加 `UserDir disabled root` 以禁止将此指令设置为指向根目录的功能。

你使用此指令设置的目录名称必须对 Web 服务器可访问。换句话说，如果 `/home/username` 是主目录，并且你保留 `UserDir` 设置为 `public_html`，那么 `/home/username/public_html` 必须对 Web 服务器可访问。实际上，Apache 还要求对 `/home` 和 `/home/username` 目录具有读取和执行权限。一些注重安全的系统管理员不喜欢在用户主目录中创建 Web 目录的想法，因此你可以将 `UserDir` 设置为其他路径，例如：

```text
UserDir /www/users
```

这样，当请求 `http://your_server_name/~username` 时，Apache 会将其转换为 `/www/users/username`。通过这种方式，你可以通过创建一个新的顶级目录，并为每个用户创建一个目录，从而将用户的 Web 文件保留在主目录（`/home/username`）之外。请记住确保 Apache 对这些目录中的每一个都有读取和执行权限。

## mod_alias

`mod_alias` 模块默认在 Apache 中编译。它提供了各种指令，可用于将服务器文件系统的一部分映射到另一部分，甚至执行 URL 重定向服务。

### Alias

`Alias` 指令允许你将路径映射到系统文件系统的任何位置。

- **语法：** `Alias URL-path path`
- **上下文：** 服务器配置、虚拟主机

例如，以下指令将 `/data/` 映射到 `/web/data/`；因此，当收到如 `http://www.yoursite.com/data/`

```text
Alias /data/ "/web/data/"
```

`http://data/datafile.cvs` 这样的请求时，将返回名为 `/web/data/datafile.cvs` 的文件。

> **注意：** 别名路径不必位于你的文档根树内，因此创建别名时要小心——你可能会不小心向全世界暴露文件系统的某一部分。

> **说明：** 如果你在定义别名时使用尾随 `/`（斜杠），则能够访问别名目录的请求也必须包含尾随 `/`。





## AliasMatch

AliasMatch 指令类似于 Alias 指令，不同之处在于它可以使用正则表达式。

语法：AliasMatch regex path

上下文：服务器配置，虚拟主机

例如，以下指令将 www.yoursite.com/data/index.html 匹配到文件 /web/data/index.html：

```
AliasMatch  ^/data(.*)  /web/data$1
```

## Redirect

Redirect 指令将 URL 请求重定向到另一个 URL。如果您已将网站的一部分移动到新目录，甚至新的网站，可以使用此指令确保那些收藏了旧网站链接的人仍然能够找到它。

语法：Redirect [status_code] old_URL new_URL

上下文：服务器配置，虚拟主机，目录，每目录访问控制文件（.htaccess）

例如，以下指令将所有包含 /data 路径的 URL 请求重定向到新的 URL。因此，对 www.yoursite.com/data/some-file.txt 的请求将被重定向到 www.your-new-site.com/data/some-file.txt：

```
Redirect /data  www.your-new-site.com/data
```

Redirect 指令优先于 Alias 和 ScriptAlias 指令。默认情况下，发送到客户端的状态码是 Temp（HTTP 状态码 302）。如果您想指定不同的状态码，请使用以下方法：

| 状态码 | 作用 |
| :--- | :--- |
| Permanent | 告知客户端该重定向是永久的。返回 HTTP 状态码 301。 |
| Temp | 返回临时重定向状态（302）。这是默认值。 |
| See other | 返回“See Other”状态（303），表示资源已被替换。 |
| Gone | 返回“Gone”状态（410），表示资源已被永久移除。使用此状态时，应省略 URL 参数。 |

![](img/e11fcbd2818a3495ac70085e5d8d1c26_177_0.png)

您也可以以数字格式提供有效的 HTTP 状态码。如果您提供的状态码在 500 到 399 之间，则必须存在 new-URL；否则，必须省略它。您可能对使用不同状态码有疑问。将来，客户端可能会足够智能，以便更有意义地识别状态码。例如，如果代理服务器接收到永久重定向状态码，它可以将其信息存储在缓存中，以便在后续请求中直接访问新资源。

## RedirectMatch

`RedirectMatch` 指令类似于 `Redirect` 指令，但它接受正则表达式，而不是简单的旧 URL。

**语法：** `RedirectMatch [status_code] regex URL`

**上下文：** 服务器配置，虚拟主机

例如，以下指令将所有以 `.htm` 结尾的请求重定向到相同请求的 `.html` 版本：

```
RedirectMatch (.*)\.html$ www.yourserver.com$1.html
```

为了说明其工作原理，假设以下请求：

```
http://www.yoursite.com/some/old/dos/files/index.htm
```

将被重定向到：

```
http://www.yoursite.com/some/old/dos/files/index.html
```

有关 `status_code` 的信息，请参阅 `Redirect` 指令（上一节）。

## RedirectTemp

`RedirectTemp` 指令类似于 `Redirect` 指令。它告知客户端该重定向仅是临时的。请注意，`Redirect` 指令默认也会产生临时状态。

**语法：** `RedirectTemp old_URL new_URL`

**上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件（`.htaccess`）

## RedirectPermanent

`RedirectPermanent` 指令类似于 `Redirect` 指令。它告知客户端该重定向是永久的。请注意，`Redirect` 指令默认产生临时状态，但您可以使用状态码 301 或关键字 `permanent` 作为状态，效果与该指令相同。

**语法：** `RedirectPermanent old_URL new_URL`

**上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件（`.htaccess`）

### ScriptAlias

`ScriptAlias` 指令为物理目录路径创建别名。此外，请求中提供的任何文件名都被视为 CGI 脚本，服务器将尝试运行该脚本。

**语法：** `ScriptAlias alias "physical_directory_path"`

**上下文：** 服务器配置，虚拟主机

例如，以下指令可用于处理诸如 `www.nitec.com/cgi-bin/somescript.pl` 的请求。如果权限验证正确，服务器会尝试运行 `somescript.pl`。请注意，`ScriptAlias` 目录是不可浏览的：

```
ScriptAlias /cgi-bin/ "/www/nitec/public/cgi-bin/"
```

### ScriptAliasMatch

`ScriptAliasMatch` 指令与 `ScriptAlias` 指令等效，不同之处在于它使用正则表达式，允许您定义动态别名规则，而不是固定别名。

**语法：** `ScriptAliasMatch regex directory`

**上下文：** 服务器配置，虚拟主机

例如，以下两个指令执行完全相同的功能：

```
ScriptAliasMatch "~/cgi-bin(.*)" "/www/nitec/public/cgi-bin$1"
ScriptAlias /cgi-bin/ "/www/nitec/public/cgi-bin/"
```

### mod_speling

`mod_speling` 模块在 Apache 中默认未编译。它允许您处理拼写错误或大小写错误的 URL 请求。它会将请求的（拼写错误或大小写错误的）文档名称与请求目录中所有文档名称进行比较，以查找一个或多个紧密匹配项。

如果是拼写错误的文档请求，该模块允许单个拼写错误，如额外字符插入、字符遗漏或字符换位。如果是大小写错误的文档请求，则执行不区分大小写的文件名比较。无论哪种情况，如果该模块定位到一个与请求紧密相似的文档，它会向客户端发送重定向请求。如果存在多个匹配项，它会将列表发送给客户端供选择。此模块提供的唯一指令称为 `CheckSpelling`。

`CheckSpelling` 指令启用或禁用 `mod_speling` 模块。请注意，当拼写更正功能开启时，由于提供拼写错误文档请求所需的额外搜索，服务器可能会经历性能损失。

- 语法：`CheckSpelling On | Off`
- 默认设置：`CheckSpelling Off`
- 上下文：服务器配置，虚拟主机

> `mod_speling` 模块仅适用于文件和目录名称。

### mod_vhost_alias

`mod_vhost_alias` 模块允许您创建动态配置的虚拟主机。此模块仅适用于需要大量虚拟主机的 Apache 安装环境。例如，使用 Apache 的互联网服务提供商（ISP）可以利用此模块减少为每个新虚拟主机客户所需的配置工作。

此模块使您能够使用虚拟网站的 IP 地址或主机名来创建服务网站所需的物理目录路径，从而创建动态虚拟主机配置。

### VirtualDocumentRoot

`VirtualDocumentRoot` 指令允许您使用插值目录路径为虚拟主机设置文档根目录。

- 语法：`VirtualDocumentRoot interpolated_directory`
- 上下文：服务器配置，虚拟主机

例如，在以下指令中，当 Apache 接收到对 `http://www.domain.com/somepage.html` 的请求时，它将请求转换为 `/www.domain.com/htdocs/somepage.html`：

```
UseCanonicalName              Off
VirtualDocumentRoot      /www/%0/htdocs
```

将 `UseCanonicalName` 设置为 `off`，以便 Apache 依赖由所有现代 Web 客户端提供的主机头来确定主机名。`VirtualDocumentRoot` 适用于基于名称的虚拟托管场景，在这种场景中，您有一个 IP 地址负责许多虚拟网站。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_180_0.png)

**注意**

`%0` 被转换为完整的主机名（**即**，`www.domain.com`）。如果需要，您可以使用主机名的部分。主机名（或 IP 地址）被点分隔成部分。例如，使用 `%1`（**第一部分** = `www`）、`%2`（**第二部分** = `domain`）或 `%-$i`（**最后一部分** = `com`）可以为该模块提供的指令创建适当的插值目录。您还可以使用 `%N.P` 约定，其中 `N` 代表部分（**由点分隔**），`i` 代表该部分的字符数。例如，`%1.2` 将从 `www.domain.com` 中获取 `ww`。

### VirtualDocumentRootIP

`VirtualDocumentRootIP` 指令允许您使用使用网站 IP 地址构建的插值目录路径为虚拟主机设置文档根目录。如果您使用基于 IP 的虚拟托管，因为每个虚拟网站都有唯一的 IP 地址，所以此方法适用。

**语法：** `VirtualDocumentRootIP interpolated_directory`

**上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件（`.htaccess`）

例如，在以下指令中，当 Apache **接收到**对 `http://www.domain.com/somepage.html` 的**请求时**，它将**请求转换为** `/www/IP_address_of_.www.domain.com/htdocs/somepage.html`

```
VirtualDocumentRootIP  /www/%0/htdocs
```

### VirtualScriptAlias

`VirtualScriptAlias` 指令允许定义脚本别名（如使用 `ScriptAlias` 指令所做的那样），该别名使用插值目录路径。

**语法：** `VirtualScriptAlias alias interpolated_directory`

**上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件（`.htaccess`）

例如，在以下指令中，当 Apache 接收到对 `http://www.domain.com/cgi-bin/script_name` 的请求时，它将请求转换为 `/www/www.domain.com/cgi-bin/script_name`：

```
UseCanonicalName     Off
VirtualScriptAlias   /cgi-bin/  /www/%0/cgi-bin
```

将 `UseCanonicalName` 设置为 **off**，要求 Apache 依赖由所有现代 Web 客户端提供的主机头来确定主机名。`VirtualDocumentRoot` 适用于基于名称的虚拟托管场景，在这种场景中，您有一个 IP 地址负责许多虚拟网站。




## VirtualScriptAliasIP

`VirtualScriptAliasIP` 指令允许您定义一个使用插值目录路径的脚本别名（类似于使用 `ScriptAlias` 指令所做的那样）。

-   **语法：** `VirtualScriptAliasIP alias interpolated_directory`
-   **上下文：** 服务器配置，虚拟主机

例如，在以下指令中，当 Apache 接收到对 `http://www.domain.com/cgi-bin/script_name` 的请求时，它会将该请求转换为 `/www/IP_address/cgi-bin/script_name`

```
VirtualScriptAliasIP /cgi-bin/ /www/%0/cgi-bin
```

## 其他模块

本节中的模块（如表 5-11 所示）不属于任何特定类别。

表 5-11
其他模块

| 模块 | 用途 |
| :--- | :--- |
| mod_so | 支持在运行时加载模块。 |
| mod_imap | 图像映射文件处理程序。 |
| mod_proxy | 将 Apache 变为缓存代理服务器。详情参见第 10 章。 |
| mod_isapi | Windows ISAPI 扩展支持。详情参见第 21 章。 |
| mod_file_cache | 在内存中缓存文件以加快响应速度。 |
| mod_dav | 提供 1 类和 2 类基于 Web 的分布式创作和版本管理（WebDAV）功能。 |
| mod_example | 供模块开发者学习如何编写 Apache 模块的示例。对除 C 程序员外的其他人没有用处。 |

## mod_so

`mod_so` 模块允许 Apache 加载其他模块所需的可执行代码，或在服务器启动期间加载其他模块。除了该模块本身，您可以将所有模块编译为 DSO（动态共享对象）模块。

### LoadFile

`LoadFile` 指令在启动期间加载指定的文件。通常，使用此指令加载其他模块所需的动态链接库（DLL）文件（仅限 Windows）。

-   **语法：** `LoadFile filename [filename...]`
-   **上下文：** 服务器配置

### LoadModule

`LoadModule` 指令加载已编译为 DSO 的模块。

-   **语法：** `LoadModule module_filename`
-   **上下文：** 服务器配置

## mod_imap

`mod_imap` 模块在 Apache 中默认编译。它提供图像映射支持，该功能曾由 CGI 程序 `imagemap` 提供。您可以使用 `AddHandler` 指令为任何文件扩展名指定 `imap-file` 处理程序（内置于该模块中）。例如，以下指令使 Apache 将所有 `.map` 扩展名的文件视为图像映射，并使用 `mod_imap` 模块处理这些文件：

```
AddHandler imap-file map
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_182_0.png)

`mod_imap` 模块仍支持旧格式：

```
AddType application/x-httpd-imap map
```

但是，不建议使用旧格式，因为未来可能会取消对其支持。

图像映射文件的内容可以具有以下任一语法：

```
directive value [x,y ...]
directive value "Menu text" [x,y ...]
directive value x,y ... "Menu text"
```

图像映射文件中允许的指令如下：

-   `base` — 映射文件中使用的相对 URL 被视为相对于此指令值。请注意，如果在映射文件中找到 `ImapBase` 指令设置，则会被此指令覆盖。默认值为 `http://server_name/`。`base_uri`，与 `base` 同义。
-   `default` — 指定当坐标不符合任何多边形、圆形或矩形，且未给出任何 point 指令时要采取的操作。此指令的默认值为 nocontent，表示告知客户端保持显示当前页面。
-   `poly` — 使用至少 3 个点到最多 100 个点的多边形来定义。如果用户提供的坐标落在多边形内，则此指令被激活。
-   `circle` — 使用中心坐标和圆上一点来定义圆形。如果用户提供的坐标落在圆内，则此指令被激活。
-   `rect` — 使用两个对角坐标来定义矩形。如果用户提供的坐标落在矩形内，则此指令被激活。
-   `point` — 定义单个点坐标。当不满足其他指令时，使用距离用户提供坐标最近的 point 指令。

值为绝对或相对 URL，或以下列表中的特殊值之一。坐标 $(x,y)$ 由空白字符分隔。双引号内的文本（如第二种语法所示）在生成图像映射菜单时用作链接文本。任何以 # 字符开头的行都被视为注释，并被 Apache 忽略。

坐标以 $x,y$ 格式书写，每个坐标由空白字符分隔。引号内的文本字符串在生成菜单时用作链接。如果没有这样的字符串，则 URL 即为链接，如下面的图像映射文件所示：

```
# Comments go here
# Version 1.0.0
base http://www.yoursite.com/some/dir
rect thisfile.html "Customer info" 0,0 100,200
circle http://download.yoursite.com/index.html 295,0 100,22
```

如果该图像映射文件名为 `imap.map`，则可以从其他 HTML 文件中以如下方式引用：

```
<A HREF="/path/to/imap.map"><IMG ISMAP SRC="/path/to/imap.gif"></A>
```

### ImapMenu

`ImapMenu` 指令确定在请求没有有效坐标的图像映射文件时的操作。

-   **语法：** `ImapMenu (None, Formatted, Semi-formatted, Unformatted)`
-   **上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (.htaccess)
-   **覆盖：** Indexes

`ImapMenu` 允许以下操作：

| 操作 | 执行内容 |
|---|---|
| None | 不生成菜单，并执行默认操作。 |
| Formatted | 生成最简单的菜单。忽略注释。打印一级标题，然后是一条水平线，接着是链接——每个链接占一行。 |
| Semi-formatted | 在半格式化菜单中，打印注释，将空行转换为 HTML 换行符，且不打印标题或水平线。 |
| Unformatted | 在未格式化菜单中，打印注释，并忽略空行。 |

### ImapDefault

`ImapDefault` 指令定义图像映射的默认操作。此默认设置可以使用图像映射文件中的 `default` 指令进行覆盖。

-   **语法：** `ImapDefault {Error, Nocontent, Map, Referer, URL}`
-   **上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (.htaccess)
-   **覆盖：** Indexes

下表显示了 `ImapDefault` 指令每个可能值的含义。

| 值 | 执行内容 |
|---|---|
| URL | 相对或绝对 URL。相对 URL 相对于基准解析。 |
| Map | 与图像映射文件自身的 URL 相同。除非 ImapMenu 设置为 none，否则将创建菜单。 |
| Menu | 与 Map 相同。 |
| Referer | 与引用文档的 URL 相同。如果不存在 Referer: 头，则默认为 http://servername/。 |
| Nocontent | 发送状态代码 204 以告知客户端保持显示当前页面。对于 base 无效。 |
| Error | 发送状态代码 500 以告知客户端服务器错误。 |

### ImapBase

`ImapBase` 指令设置图像映射文件中使用的默认基准。此 `base` 设置可以使用图像映射文件内的 `base` 指令进行覆盖。如果不存在此指令，`base` 默认为 `http://servername/`。

-   **语法：** `ImapBase { Map, Referer, URL }`
-   **上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (.htaccess)
-   **覆盖：** Indexes

## mod_file_cache

`mod_file_cache` 模块允许 Apache 缓存经常使用且不太经常更改的静态文件。使用此模块，您可以将文件加载到内存中或预先打开文件，从而减少每次请求的磁盘 I/O。这意味着 Apache 无需为每个请求从磁盘读取文件。此模块并非在所有平台上都有效，并且仅当您确定频繁请求的文件不会更改时，才应使用它。如果缓存文件或预先打开的文件发生更改，在重启服务器之前，Apache 服务器无法处理该更改。

### MMapFile

`MMapFile` 指令允许您通过 `mmap()` 系统调用将文件加载到内存中。文件加载到内存后，服务器将无法检测到物理文件中的任何更改。因此，使用此指令时要小心。如果您更改了已加载到内存中的文件，请务必重启 Apache 服务器。

-   **语法：** `MMapFile filename [filename] [...]`
-   **上下文：** 服务器配置

### CacheFile

`CacheFile` 指令预先打开文件并缓存文件句柄，这样当请求到来时，Apache 无需执行系统调用来打开和读取文件。文件缓存后，对该文件的任何更改都需要重启 Apache 服务器。

-   **语法：** `CacheFile filename [filename] [...]`
-   **上下文：** 服务器配置

## mod_dav

`mod_dav` 模块允许您使用 HTTP 1.1 协议的 WebDAV 扩展。要了解有关这些扩展的更多信息，请访问 `www.webdav.org`。





# Dav

`Dav` 指令用于启用或禁用 `mod_dav` 模块。如果您希望在目录容器中 **使用** WebDAV 功能，必须将其设置为 `On`。

-   **语法：** `Dav On | Off`
-   **上下文：** 目录

# DavLockDB

`DavLockDB` 指令设置锁数据库文件的完全限定路径名。

-   **语法：** `DavLockDB filename`
-   **上下文：** 服务器配置，虚拟主机

# DavMinTimeout

`DavMinTimeout` 指令设置资源锁的最小超时间隔（以秒为单位）。默认值确保服务器不会因任何超时问题而自动锁定 WebDAV 客户端。

-   **语法：** `DavMinTimeout seconds`
-   **默认设置：** `DavMinTimeout 0`
-   **上下文：** 目录

# DavDepthInfinity

`DavDepthInfinity` 指令启用将 Depth 头设置为无穷大的 PROPFIND 请求。推荐默认设置。

-   **语法：** `DavDepthInfinity On | Off`
-   **默认设置：** `DavDepthInfinity Off`
-   **上下文：** 目录

# Web 站点管理

管理 Web 站点涉及诸如管理虚拟 Web 站点、控制对您的 Web 站点的访问、监控和分析访问及错误日志、在必要时将流量重定向到不同的 URL、设置代理服务，以及通常只需执行运行完美 Web 站点所必需的一切操作等任务。本部分专门介绍所有这些任务。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_187_0.png)

## 本部分包含

-   **第 6 章**
    托管虚拟 Web 站点
-   **第 7 章**
    验证和授权 Web 站点访问者
-   **第 8 章**
    监控对 Apache 的访问
-   **第 9 章**
    重写您的 URL
-   **第 10 章**
    设置代理服务器
-   **第 11 章**
    运行完美的 Web 站点

# 托管虚拟 Web 站点

![](img/e11fcbd2818a3495ac70085e5d8d1c26_189_0.png)

Apache 可以从单台服务器提供多个 Web 站点。例如，一家 Web 托管公司可能有一台运行 Apache 的单台 Web 服务器机器，它为数百个客户端 Web 站点提供服务。此类系统拥有一个主主机名和许多 IP 别名或虚拟主机名。通过这种虚拟主机提供的 Web 站点称为 **虚拟 Web 站点**。Apache 对虚拟 Web 站点（称为虚拟主机）的支持非常令人印象深刻。本章讨论如何创建各种类型的虚拟主机以及如何使用各种技术进行管理。

## 了解 Apache 的虚拟托管功能

当您在 Internet 主机上设置 Apache 时，它可以响应针对该主机的 HTTP 请求。例如，如果您在一台名为 `server1.domain.com` 的主机上设置 Apache，Apache 将为主机服务 HTTP 请求。然而，如果您设置 DNS 记录，使得另外两个主机名（例如 `www.mycompany-domain.com` 和 `www.friendscompany-domain.com`）指向同一台机器，您可以让 Apache 将这些两个域作为虚拟 Web 站点提供服务。在这种情况下，`www.mycompany-domain.com` 被视为主 Web 主机名（主服务器），其余的将被视为虚拟 Web 站点或虚拟主机。

Apache 允许虚拟主机从主服务器继承配置，这使得在大型安装中，某些内容可以共享，从而使得虚拟主机配置易于管理。例如，如果您决定只拥有一个中央 CGI 库，并允许虚拟主机使用存储在那里的脚本，您无需在每个虚拟主机容器中创建 `ScriptAlias` 指令。只需在主服务器配置中使用一个即可。每个虚拟主机都可以使用该别名，就好像它是其自身的一部分一样。

**本章简介**

-   了解两种类型的虚拟主机
-   创建基于 IP 的虚拟主机
-   创建基于名称的虚拟主机
-   为虚拟主机配置 DNS
-   使用自己的用户和组权限运行虚拟 Web 站点
-   使用 `mod_perl` 在单个 Apache 服务器上管理大量虚拟主机
-   使用 `makesite` 脚本简化创建新虚拟主机的过程
-   使用 `mod_v2h` 和 MySQL 数据库管理虚拟主机

Apache 的配置文件 httpd.conf 使用 `<VirtualHost>` 容器将虚拟主机配置与主服务器配置分开。例如，请查看列表 6-1 中的 httpd.conf 文件。

## 列表 6-1: httpd.conf

```
# httpd.conf file

ServerName main.server.com
Port 80
ServerAdmin mainguy@server.com
DocumentRoot "/www/main/htdocs"

ScriptAlias /cgi-bin/ "/www/main/cgi-bin/"
Alias /images/ "/www/main/htdocs/images/"

<VirtualHost 192.168.1.100>
ServerName vhost1.server.com
ServerAdmin vhost1_guy@vhost1.server.com
DocumentRoot "/www/vhost1/htdocs"
ScriptAlias /cgi-bin/ "/www/vhost1/cgi-bin/"
</VirtualHost>

<VirtualHost 192.168.1.110>
ServerName vhost2.server.com
ServerAdmin vhost2_guy@vhost2.server.com
DocumentRoot "/www/vhost2/htdocs"
ScriptAlias /cgi-bin/ "/www/vhost2/cgi-bin/"
Alias /images/ "/www/vhost2/htdocs/images/"
</VirtualHost>
```

列表 6-1 显示了两个称为 vhost1.server.com 和 vhost2.server.com 的虚拟 Web 站点，它们定义在各自的 `<VirtualHost>` 容器中。包含在每个 `<VirtualHost>` 容器中的所有指令仅适用于其服务的虚拟主机。因此，当 Web 浏览器请求 http://vhost1.server.com/index.html 时，Apache Web 服务器会在 /www/vhost1/htdocs 目录中查找 index.html 页面。类似地，当 Web 浏览器请求 http://vhost2.server.com/cgi-bin/hello.pl 时，脚本将从 /www/vhost2/cgi-bin 目录运行。

然而，主服务器配置中的许多指令（即 `<VirtualHost>` 容器外的任何指令）仍然适用于未覆盖它们的虚拟主机。例如，列表 6-1 中的 vhost1.server.com 没有针对 /images/ 目录别名的 Alias 指令。因此，当 Web 浏览器请求 http://vhost1.server.com/images/prett_y_pic.gif 文件时，图片是从 /www/main/htdocs/images 目录提供的。由于 vhost2.server.com 用自己的 /images/ 别名覆盖了主配置，类似的请求是从 /www/vhost2/htdocs/images 目录提供的。

# 设置虚拟主机

使用 Apache 创建虚拟 Web 站点有三种方法，如下列表所述：

-   **基于名称：** 基于名称的虚拟 Web 站点非常常见。此类配置要求将多个主机名指向单个系统。您可以在 DNS 中创建多个 CNAME 或 A 记录以指向单个主机。由于此方法在 Apache 配置中不使用 IP 地址，因此如果您更改 Web 服务器的 IP 地址，很容易迁移。
-   **基于 IP：** 此方法在 Apache 配置中需要 IP 地址，因此当需要更改 IP 地址时，很容易迁移。
-   **多个主服务器：** 此方法涉及使用多个主要 Web 服务器配置。只有当您必须为每个虚拟主机保持单独的配置文件时，才推荐此方法。这是最不推荐的方法，很少使用。

## 基于名称的虚拟主机

创建虚拟主机的此方法是最推荐的。它只需要一个 IP 地址即可托管数百个虚拟 Web 站点。

> **注意**
> 基于名称的虚拟托管中您可能遇到的唯一问题是，此方法不适用于不支持 HTTP 1.1 协议的 Web 浏览器。只有非常早期的 Web 浏览器，如 Microsoft IE 1.x 或 Netscape Navigator 1.x，不支持 HTTP 1.1。因此，这真的不再是一个大问题。大多数人使用的是 3.x 或更高版本的 Web 浏览器，这些浏览器与基于名称的虚拟托管技术兼容。

例如，假设您拥有 IP 地址 192.168.1.100，并希望在同一服务器上托管 vhost1.domain.com 和 vhost2.domain.com。您可以按如下方式操作：

1.  首先，在您的 DNS 服务器上创建适当的 DNS 记录，将 vhost1.domain.com 和 vhost2.domain.com 指向 192.168.1.100。有关详细信息，请参阅“为虚拟主机配置 DNS”部分。
2.  在 httpd.conf 文件中创建类似于以下内容的配置段。

```
NameVirtualHost 192.168.1.100

<VirtualHost 192.168.1.100>
    ServerName vhost1.domain.com
    ServerAdmin someone@vhost1.domain.com
    DocumentRoot "/www/vhost1/htmldocs"

    #
    # 您需要的任何其他指令都可以放在这里
```





# 基于 IP 的虚拟主机

这种方法要求你在创建虚拟主机时使用 IP 地址。IP 地址需要硬编码在配置文件的每个 `<VirtualHost>` 容器标签中。如果你频繁更改 IP 地址，这可能会带来维护上的麻烦。与之前描述的基于名称的虚拟主机方法相比，使用此方法没有优势。以下示例展示了三个基于 IP 的虚拟主机。

```
<VirtualHost 192.168.1.1>
    ServerName vhost1.server.com
    # Other directives go here
</VirtualHost>

<VirtualHost 192.168.1.2>
    ServerName vhost2.server.com
    # Other directives go here
</VirtualHost>

<VirtualHost 192.168.1.3>
    ServerName vhost3.server.com
    # Other directives go here
</VirtualHost>
```

这些 IP 地址中的每一个都必须绑定到服务器上的相应以太网接口。例如，上述配置要求托管上述站点的系统在其 DNS 服务器配置文件中具有以下 DNS 记录。

```
: Address Records
vhost1.server.com. IN A 192.168.1.1
vhost2.server.com. IN A 192.168.1.2
vhost3.server.com. IN A 192.168.1.3

: Reverse DNS records
1     IN PTR vhost1.server.com.
2     IN PTR vhost2.server.com.
3     IN PTR vhost3.server.com.
```

这些地址中的每一个都必须绑定到服务器上的一个或多个以太网接口。在 Linux 系统上，通常可以使用 IP 别名技术绑定多个 IP 地址。例如：

```
/sbin/ifconfig eth0    192.168.1.1 up
/sbin/ifconfig eth0:0 192.168.1.2 up
/sbin/ifconfig eth0:1 192.168.1.3 up
```

在以上示例中，所有三个 IP 地址都绑定到以太网接口 `eth0` 及其两个别名 `eth0:0` 和 `eth0:1`。因此，系统将响应每个 IP 地址。

## 多个主服务器作为虚拟主机

只有在你被要求（通常出于非技术原因）维护不同的 `httpd.conf` 文件时，才建议使用多个主服务器作为虚拟主机。例如，假设你有 16 个 IP 地址，并希望为 16 个不同的客户（或部门）提供它们自己的 httpd.conf 文件，以便每个实体可以独立管理所有内容，甚至可以在其自己的 httpd.conf 中使用 <VirtualHost> 容器创建虚拟主机。

> **注意**
> 在实际执行此方法之前，请仔细考虑是否可以通过使用 <VirtualHost> 容器来避免创建多个主服务器实例。

列表 6-2 展示了 httpd.conf 的一个简化版本（称为 httpd-100.conf），它使用 Listen 指令告诉 Apache 仅处理与其运行所在的系统关联的 192.168.1.100 IP 地址。这实现了单个虚拟主机。

# 列表 6-2: httpd-100.conf

```
ServerType standalone
ServerRoot "/usr/local/apache"
PidFile /usr/local/apache/logs/httpd-192.168.1.100.pid
ScoreBoardFile /usr/local/apache/logs/httpd-192.168.1.100.scoreboard
Timeout 300
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 15
MinSpareServers 60
MaxSpareServers 100
StartServers 50
MaxClients 200
MaxRequestsPerChild 0
Port 80
Listen 192.168.1.100:80
User prod
Group prod
ServerName prod.domain.com
ServerAdmin kabi@prod.domain.com
DocumentRoot "/www/prod/htdocs"
```

请注意，Listen 指令也接受端口号作为参数。在列表 6-2 中，告知 Apache 监听给定 IP 地址的 80 端口。Port 指令仍然是必要的，因为其值用于 Apache 生成的自引用 URL。

列表 6-3 展示了另一个简化的 httpd.conf 文件（称为 httpd-101.conf），它告诉 Apache 仅监听 192.168.1.101 地址。这使用创建虚拟主机的多个主服务器方法实现了另一个虚拟主机。

# 列表 6-3: httpd-101.conf

```
ServerType standalone
ServerRoot "/usr/local/apache"
PidFile /usr/local/apache/logs/httpd-192.168.1.101.pid
ScoreBoardFile /usr/local/apache/logs/httpd-192.168.1.101.scoreboard
Timeout 300
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 15
MinSpareServers 5
MaxSpareServers 10
StartServers 5
MaxClients 10
MaxRequestsPerChild 0
Port 80
Listen 192.168.1.101:80
User stage
Group stage
ServerAdmin lance@stage.domain.com
DocumentRoot "/www/stage/htdocs"
```

想要使用列表 6-2 和 6-3 中的配置文件运行两个主要 Apache 服务器的系统必须满足以下条件：

- 一个或多个对应于命名 IP 地址的以太网接口。例如，在 Linux 系统上，你可以使用 IP 别名命令将以太网接口 eth0 绑定到 192.168.1.100 和 192.168.1.101，如所示：

```
/sbin/ifconfig eth0 192.168.1.100 up
/sbin/ifconfig eth0:0 192.168.1.101 up
```

- IP 地址必须具有关联的主机名。对于上述配置文件，192.168.1.100 与 prod.domain.com 关联，192.168.1.101 与 stage.domain.com 关联。

具有此类绑定到其接口的 IP 地址的系统现在可以使用以下命令运行两个主要 Apache 守护进程：

```
/usr/local/apache/bin/httpd -f conf/httpd-100.conf
/usr/local/apache/bin/httpd -f conf/httpd-101.conf
```

如果你运行 `ps auwww | grep httpd | grep root | grep conf` 命令，你将看到两个作为 root 用户运行的主要 Apache 服务器。

# 为虚拟主机配置 DNS

在大多数情况下，你的 ISP 负责为域名提供 DNS 服务。如果是这种情况，你可以跳过这一节。然而，如果你在 Linux 或其他类 Unix 系统上自行运行 BIND（最广泛使用的 DNS 服务器），我将在这里向你展示如何为你的虚拟主机配置 DNS。

Windows 用户：请阅读 *Configuring Apache for Win32* 章节，以了解如何配置你的 Windows DNS 服务器详情。

## 理解区域文件

要为虚拟主机设置 DNS，需要一个区域文件。区域文件是你 DNS 记录的文本文本描述。此文件由 DNS 服务器加载，以实现单一区域的 DNS 服务，该区域通常称为互联网域。

下面是一个区域文件的示例。在此示例中，假设你要设置的新虚拟主机名为 www.newdomain.com，DNS 服务器主机名分别为 ns1.domain.com（主）和 ns2.domain.com（从），且你的 Web 服务器主机名为 www.idadines.com (192.168.1.100)。请确保根据你的设置相应地更改主机名和 IP 地址。www.newdomain.com 的区域文件称为 /var/named/newdomain.zone，包含以下行：

```
@ IN SOA newdomain.com. hostmaster.newdomain.com.(
20011201001 : Serial YYYYMMDDXXX
7200 : refresh
3600 : (1 hour) retry
1728000 : (20 days) expire
3600) : (1 hr) minimum ttl
: Name Servers
IN NS ns1.domain.com.
IN NS ns2.domain.com.
: A Records for IP-based virtual hosting
www.newdomain.com. IN A 192.168.1.100
: CNAME for name-based virtual hosting
www.newdomain.com. IN CNAME www.domain.com.
```

上述 DNS 配置假设你将不会使用基于 IP 的虚拟主机，因此没有为 www.newdomain.com 创建 A 记录。A 记录行被注释掉了。因为如果你使用基于 IP 的虚拟主机方法，可以取消注释它。由于基于名称的虚拟主机不需要唯一的 IP 地址，创建了一个 CNAME 记录，将 www.newdomain.com 指向 www.domain.com（这是主要的 Web 服务器）。




### 为新虚拟主机设置 DNS

你可以按以下方式在 Linux 上为每个新虚拟主机设置 DNS：

- 1. 为新域名创建一个区域文件。（有关区域文件的更多信息，请参阅上一节。）

- 2. 在 `/etc/named.conf` 文件中，添加以下行以启用 newdomain 区域。

```
zone "newdomain.com" IN {
    type master;
    file "newdomain.zone";
    allow-update { none; };
};
```

这告诉 named（DNS 守护进程），newdomain.com 的区域文件是 /var/named/newdomain.zone，并且它是该区域的主（master）DNS 服务器。

- 3. 运行 `killall -HUP named` 命令，强制名称服务器重新加载 `/etc/named.conf` 和新的区域文件。

- 4. 尝试 ping www.newdomain.com。如果没有收到响应，请检查 `/var/log/messages` 文件，查看名称服务器（named）是否在 `/etc/named.conf` 或 `/var/named/newdomain._zone` 文件中报告了任何类型或其他错误。在这种情况下，请更正这些类型或错误，并如前一步所述重启服务器。

- 5. 一旦能够 ping 通 www.newdomain.com，你就可以按照本章前面章节的描述为该虚拟主机创建 Apache 配置了。

## 提供虚拟邮件服务

为了为你添加的新虚拟主机提供虚拟邮件服务，你需要修改 `newdomain.zone` 文件并添加一个或多个适当的 MX 记录。例如，假设你的邮件服务器是 `mail.domain.com`，并且它被配置为接受针对 `newdomain.com` 的邮件。在这种情况下，你可以修改 `/var/named/newdomain.zone` 如下所示：

```
@ IN SOA newdomain.com. hostmaster.newdomain.com.
20011201002 ; Serial YYYYMMDDXXX
7200 ; refresh
3600 ; (1 hour) retry
1728000 ; (20 days) expire
3600 ; (1 hr) minimum ttl

; Name Servers
IN NS ns1.domain.com.
IN NS ns2.domain.com.
IN MX 10 mail.domain.com.

; CNAME for name-based virtual hosting
www.newdomain.com. IN CNAME www.domain.com.
```

请注意，如果你有多个邮件服务器，你可以使用简单的优先级方案来添加它们。例如，假设你希望 newdomain.com 的所有邮件都流向 `mail.domain.com`，如果该邮件服务器不可用，你希望使用 `bkupmail.domain.com`。你可以简单地添加第二个 MX 记录，如下所示：

```
IN MX 10 mail.domain.com.
IN MX 20 bkupmail.domain.com.
```

`mail.domain.com` 前面的较小数字使其成为比 `bkupmail.domain.com` 优先级更高的邮件服务器。请确保你的邮件服务器软件已配置以支持虚拟邮件域。

## 按虚拟主机设置用户和组

如果你使用 `Perchild MPM` 模块编译了 Apache，你可以按虚拟主机设置用户和组，这里对此进行了讨论。但与基于多个 `httpd.conf` 的邮件服务器设置相比，使用此方法的最大好处是配置简单。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_199_0.png)

这种方法比运行具有不同 IP 地址和不同 `User` 和 `Group` 指令的多个主 Apache 服务器更慢。速度降低是由于内部请求处理复杂性的增加。该方法背后的概念如下：你指示 Apache 运行一组具有给定用户 ID 和组 ID 的子进程集群。当虚拟主机的请求进来并且一个子进程被分配该请求时，该子进程首先确定它是否能够处理该请求。如果该子进程不负责请求的虚拟主机，它必须通过 socket 调用将请求传递给适当的子进程，这会导致请求处理变慢。由于这是一个新概念，未来版本的 Apache 可能会解决或减少速度问题。

以下材料假设你想设置两个名为 `vhost1.domain.com` 和 `vhost2.domain.com` 的虚拟主机。请确保将它们替换为你需要使用的任何主机名。表 6-1 显示了用于这些虚拟域的用户 ID 和组 ID。

| | 表 6-1 虚拟主机用户和组 ID |
|---|---|
| 虚拟主机 | 用户 ID | 组 ID |
| `vhost1.domain.com` | `vh1user` | `vh1group` |
| `vhost2.domain.com` | `vh2user` | `vh2group` |

可以按照以下方式配置 Apache 以支持每个虚拟主机的不同用户和组 ID：

- 1. 将以下行添加到 `httpd.conf`：

```
ChildPerUserID 10 vh1user vh1group
ChildPerUserID 10 vh2user vh2group
```

`ChildPerUser` 指令告诉 Apache 将十个子进程（每个都是服务请求的多个线程）与 `vhost1.domain.com` 站点的用户和组 ID 关联。类似地，第二行将另外十个子进程与 `vhost2.domain.com` 站点的用户和组 ID 关联。

- 2. 将以下行添加到 `httpd.conf`：

```
NameVirtualHost 192.168.1.100

<VirtualHost 192.168.1.100>
    ServerName vhost1.domain.com
    AssignUserID vh1user vh1group
    #
    # Other directives go here
    #
</VirtualHost>

<VirtualHost 192.168.1.100>
    ServerName vhost2.domain.com
    AssignUserID vh2user vh2group
    #
    # Other directives go here
    #
</VirtualHost>
```

在每个虚拟主机配置中使用的 *AssignUserID* 指令告诉 Apache 将每个虚拟主机与适当的用户和组 ID 关联。别忘了根据需要更改 IP 地址。

- 3. 使用 /usr/local/apache/bin/apachectl restart 命令重启 Apache 服务器，然后完成即可。

## 管理大量虚拟主机

如果你维护大量虚拟主机，*httpd.conf* 文件可能会变得非常长且难以管理。一个简单的解决方案是将每个虚拟主机配置放在单独的文件中，并使用 *Include* 指令包含每个文件。例如，清单 6-4 显示了一个 *httpd.conf* 文件，其中包含两个外部于主配置文件的虚拟主机配置。

### 清单 6-4：包含两个外部虚拟主机配置的 httpd.conf

```
ServerType standalone
ServerRoot "/usr/local/apache"
PidFile /usr/local/apache/logs/httpd.pid
ScoreBoardFile /usr/local/apache/logs/httpd.scoreboard
Timeout 300
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 15
MinSpareServers 5
MaxSpareServers 10
StartServers 5
MaxClients 10
MaxRequestsPerChild 0
Port 80
User httpd
Group httpd
ServerName www.domain.com
ServerAdmin webmaster@domain.com
DocumentRoot "/www/mysite/htdocs"

# Name Virtual Hosts
NameVirtualHost 192.168.1.100
Include vhost1.domain.com.conf
Include vhost2.domain.com.conf
```

请注意，**NameVirtualHost** 指令后面跟着 **Include** 指令，它告诉 Apache 读取 **vhost1.domain.com.conf** 和 **vhost2.domain.com.conf** 文件以加载虚拟主机配置。这些文件可以只包含你通常放在 **httpd.conf** 中的 <VirtualHost> 容器。这种方法的优点是你可以为每个虚拟主机创建非常复杂的配置，而不会使 **httpd.conf** 变得杂乱无章。

### 使用 mod_perl 自动化虚拟主机配置

虽然使用 **Include** 指令（如上一节所述）有助于使 **httpd.conf** 易于管理，但对于使用许多 Web 服务器（进而运行许多虚拟 Web 站点）的网站来说，这仍然不是一个足够好的解决方案。理想情况下，如果可以的话，你希望使用程序或脚本来编写 Apache 配置，以便自动创建许多常见的配置选项。

如果你在 Apache 中使用了 **mod_perl** 模块（在第 16 章中讨论），你可以编写 Perl 代码来生成你的 Apache 配置。由于 **mod_perl** 的编译和安装在第 16 章中已经涵盖，我将不在这里重复。我接下来将讨论如何使用 Perl 代码来生成 Apache 配置。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_201_0.png)

> 如果你仍然需要编译和在 Apache 中安装 **mod_perl** 支持，请参阅第 16 章。请记住，在按照第 16 章中的说明编译 **mod_perl** 时，必须在配置脚本中使用 **EVERYTHING=1** 选项或 **PERL_SECTIONS=1** 选项。




## 使用 makesite 脚本生成虚拟主机配置

**使用 makesite 脚本**

如果您为 ISP 或大型组织工作，且市场部经常创建新的产品网站，导致添加虚拟主机成为每日或每周的常规任务，那么您需要 `makesite`。这是一个我多年前编写的简单 Perl 脚本，我至今仍在用它来创建新的虚拟主机。该脚本随 CD-ROM 提供，也可以从 http://sourceforge.net/projects/mkweb/ 下载。

例如，要创建一个新的名为 `newsite.com` 的虚拟主机，您只需运行 `makesite newsite.com`，该脚本就会创建并追加必要的 `httpd.conf` 配置。它还会通过两个模板文件创建必要的 DNS 配置文件。要使用 `makesite`，请遵循以下步骤：

1. 将 `makesite` 脚本、`named.template` 和 `httpd.template` 文件复制到服务器上的合适位置。我通常将 `makesite` 放在 `/usr/bin` 目录中，使其位于常规路径下。我建议创建 `/var/makesite` 目录，并将 `named.template` 和 `httpd.template` 文件移动到该目录中。在以下步骤中，我假设您将执行相同的操作。

2. 使用您喜欢的文本编辑器修改 `makesite` 脚本。您需要修改以下一行或多行：

```perl
my $MAKESITE_DIR = '/var/makesite';
my $USER = 'httpd';
my $GROUP = 'httpd';
my $PERMISSION = '2770';
my $BASE_DIR = '/www';
my $HTDOCS = '/htdocs';
my $CGIBIN = '/cgi-bin';
my $NAMED_PATH = '/var/named';
my $NAMED_FILE_EXT = '.zone';
my $NAMED_TEMPLATE = "${MAKESITE_DIR}/named.template";
my $NAMED_CONF     = '/etc/named.conf';
my $HTTPD_CONF     = '/usr/local/apache/conf/httpd.conf';
my $VHOST_TEMPLATE = "${MAKESITE_DIR}/httpd.template";
my $LOG_FILE       = "${BASE_DIR}/makesite.log";
```

您可能需要按以下方式进行修改：

- 如果您遵循了我的建议并创建了存放 `named.template` 和 `httpd.template` 的 `/var/makesite` 目录，则无需更改 `${MAKESITE_DIR}`。
- 如果您使用不同于 `httpd` 的用户/组来运行 Apache，请更改 `${USER}` 和 `${GROUP}` 的值。如果希望默认 Web 目录权限不是 `2770`，请更改 `${PERMISSION}` 的值。
- `${BASE_DIR}` 设置为 `/www`，这是虚拟主机站点目录的创建位置。虚拟主机站点目录将为 `/www/ virtual_hostname`，其下将有 `htdocs`（由 `${HTDOCS}` 设置）和 `cgi-bin`（由 `${CGIBIN}` 设置）子目录。根据需要更改这些值。
- 如果您希望文档根目录不是 `htdocs`，请更改 `${HTDOCS}`。
- 类似地，如果您不使用传统的 `/cgi-bin/` 别名作为 `ScriptAlias`，请相应更改 `${CGIBIN}`。
- 在 Linux 系统上，默认的 DNS 记录目录是 `/var/named`；如果您已将其更改为其他路径，请确保更改 `${NAMED_PATH}`。
- 如果您将 `httpd.conf` 保存在不同于 `/usr/local/apache` 的路径下，请更改 `${HTTPD_CONF}` 的值。

3. 修改 `/var/makesite/named.template` 文件，使其反映您系统的主名称服务器和 Web 服务器主机名。默认的 `named.template` 文件假设您的主名称服务器和从名称服务器分别为 `ns1.domain.com` 和 `ns2.domain.com`；您的邮件服务器为 `mail.domain.com`；您的 Web 服务器为 `www.domain.com`。请确保相应更改这些主机名。

4. 确保 `/var/makesite/httpd.template` 包含您想要通过此脚本添加到每个新虚拟主机中的所有指令。

现在，您已准备好运行脚本来创建新的虚拟主机。作为预防措施，请备份您的 `/etc/named.conf` 和 `/usr/local/apache/httpd.conf` 文件。要创建名为 `vhost1.com` 的新虚拟主机，请运行 `makesite vhost1.com` 命令。查看 `/usr/local/httpd.conf` 文件；您应该会看到：




## www.vhost1.com 的域名配置

```apache
<VirtualHost www.vhost1.com>
    ServerName www.vhost1.com
    ServerAdmin webmaster@vhost1.com
    DocumentRoot /tmp/vhost1/htdocs
    ScriptAlias /cgi-bin/ /tmp/vhost1/cgi-bin/
    ErrorLog logs/www.vhost1.com.error.log
    TransferLog logs/www.vhost1.com.access.log
</VirtualHost>
```

这是 makesite 脚本创建的 `<VirtualHost>` 配置。

> **提示** | 如果你是第一次创建名称虚拟主机，请在首次运行 makesite 脚本之前，确保在 `httpd.conf` 文件的最后一行添加了 `NameVirtualHost IP_Address`。

还请检查 `/etc/named.conf` 文件；你应该能看到以下内容：

```bind
// vhost1.com was created on 2001-04-25-17-25
zone "vhost1.com" {
    type master;
    file "vhost1.zone";
};
```

如你所见，脚本为虚拟主机创建了相应的区域配置信息。你可以在 `/var/named/vhost1.zone` 文件中找到 DNS 区域信息，其显示内容如下：

```dns
@       IN  SOA vhost1.com. hostmaster.vhost1.com. (
                20010425000         ; serial YYYYMMDDXXX
                7200                ; refresh
                3600                ; (1 hour) retry
                1728000             ; (20 days) expire
                3600)              ; (1 hour) minimal TTL
: Name Servers
IN  NS  ns1.domain.com.
IN  NS  ns2.domain.com.
IN  MX  10 mail.domain.com.
: CNAME records
www   IN  CNAME  www.domain.com.
```

查看 `/www`（或 `$BASE_DIR` 指向的任何目录）；你应该看到一个名为 `vhost1` 的目录，其中包含以下文件和子目录：

- `./vhost1`
- `./vhost1/htdocs`
- `./vhost1/htdocs/index.html`
- `./vhost1/cgi-bin`

使用 `killall -HUP named` 命令重启名称服务器。同样，使用 `/usr/local/apache/bin/apachectl restart` 命令重启 Apache 服务器。你应该能够通过使用 `www.vhost1.com/` 访问新的虚拟网站。默认的 `index.html` 页面旨在帮助你通过 Web 识别该域名。

### 使用 MySQL 和 mod_v2h 模块管理虚拟主机

`mod_v2h` 模块是一个大规模虚拟主机模块，支持从 MySQL 数据库执行 URL 转换路径。该模块可以将 URL 转换路径缓存到内存中以提高性能。你需要在服务器上安装 MySQL。要了解 MySQL，请访问 `www.mysql.com`。

在安装好 MySQL 后，请按照以下步骤编译和安装 `mod_v2h`：

1.  从 `www.fractal.net/mod_v2h.tm` 下载 `mod_v2h` 的最新版本。
2.  以 root 身份，在 Apache 源代码树的 modules 子目录中使用 `tar xVZF mod_v2h.tar.gz` 命令解压源发行版。例如，如果你的 Apache 源码保存在 `/usr/local/src/httpd_2_0_16` 目录中，请在 `/usr/local/src/httpd_2_0_16/modules` 目录中解压 `mod_v2h.tar.gz` 文件。这将创建一个新的名为 `mod_v2h` 的子目录。
3.  将当前目录更改为 `/usr/local/src/httpd_2_0_16/modules/v2h` 并编辑 `config.m4` 文件。

只有在你发现 MySQL 文件的 `include` 和 `lib` 目录路径不正确时，才需要编辑此文件。例如，在我的 Linux 系统中，MySQL 包含文件安装在 `/usr/include/mysql` 目录中，库文件位于 `/usr/lib/mysql` 目录中。默认的 `config.m4` 分别指向包含文件和库文件的 `/usr/local/include/mysql` 和 `/usr/local/lib/mysql`；因此，我必须更正路径。只需在需要时编辑路径即可。我还需要在 LDFLAGS 行中添加 `-lz`，使其看起来像 `LDFLAGS="*$LDFLAGS -L/usr/lib/mysql -lz -Wl,-R,/usr/lib/mysql*"`。

4.  更改目录到 `/usr/local/src/httpd_2_0_16` 并运行 autoconf 命令以创建必要的配置文件。
5.  运行 `./configure` 并附带你在第 2 章中显示的任何所需选项，然后运行 `make && make install` 命令以编译和安装支持 `mod_v2h` 的 Apache。例如，我运行了 `./configure --prefix=/usr/local/httpd --disable-module=cgi` 来配置 Apache 源代码，然后运行 `make && make install` 命令以在 `/usr/local/httpd` 中安装支持 `mod_v2h` 但不支持 `mod_cgi` 的 Apache。（你可以通过不运行 `./configure` 而是运行 `./config.status` 来使用之前使用的任何选项。）

编译完支持 `mod_v2h` 的 Apache 后，你需要在 `httpd.conf` 中使用新的 `mod_v2h` 指令，如表 6-2 所示。

**表 6-2 mod_v2h 指令**

# 第 7 章
# 验证和授权网站访问者

# 本章内容

- 使用用户名和密码验证用户
- 使用主机名或 IP 地址授权访问
- 使用 RDBM 进行验证
- 使用 MySQL 数据库进行验证
- 使用 `/etc/passwd` 密码文件进行验证
- 使用 Cookie 进行验证

Apache 中对基本 HTTP 验证的支持已经存在相当一段时间了。已经编写了许多模块来为 Apache 提供基本 HTTP 验证。在本章中，你将了解验证和授权访问 Web 服务器的各种方法，如何使用密码文件、数据库服务器等验证用户，以及如何通过限制 IP 地址或用户名来控制访问。

## 验证与授权

许多人混淆了验证（authentication）和授权（authorization），有些人甚至认为它们是同义词，但其实不然。为了理解两者的区别，请考虑以下示例。当你想要访问一个国家时，你需要什么？护照和签证。护照是向外国证明你身份的文件。它告诉对方你确实是你所声称的那个人。所以，当你出示护照时，你是在向外国官员验证自己的身份。接下来，你必须证明你被允许（即被授权）进入该外国。这就是签证文件。

现在，用计算机术语来说，*验证*通常涉及提交用户名和密码。用户名和密码成功提交并被接受，表明你就是你所声称的那个人。换句话说，你已经*验证*了自己。

你试图访问的某个给定资源可能除了验证之外还需要授权。例如，如果你在凌晨 4 点访问计算机，由于系统管理员决定你在那个时间没有被授权访问，计算机可能会拒绝让你进入。同样，你可能被授权从办公室访问受限网站，但不能从家访问，因为公司政策规定网络管理员必须在场地内进行所有受限访问。

### 了解验证是如何工作的

基本 HTTP 验证其实相当简单。使用挑战 - 响应机制来验证用户。步骤如图 7-1 所示并在下面讨论：

1.  当 Web 浏览器请求由 HTTP 验证方案保护的 URL 时，验证开始。这在图中显示为 (1)。
2.  Web 服务器随后返回一个 401 状态头部，以及一个 WWW-Authenticate 响应头部，这意味着访问该 URL 需要验证。头部包含正在使用的验证方案（目前仅支持基本 HTTP 验证）和 realm 名称。这在图中是 (2)。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_212_0.png)

3.  此时，会出现一个 Web 浏览器对话框，要求用户输入用户名和密码。这在图中是 (3)。
4.  用户输入所需用户名和密码并点击确定。然后，浏览器将用户名和密码与之前的 URL 请求一起发送到服务器。服务器检查用户名和密码是否有效。这在图中是 (4)。

> **注意**
>
> 当密码从客户端系统（运行 Web 浏览器的托管主机）发送时，它既不是以明文发送，也不是加密的。相反，它经过 uuencode 编码并通过 Internet 传输。这对于这种验证方法来说是不利的，因为任何拥有网络流量嗅探硬件和软件的人都有可能检索到携带 uuencoded 密码的 IP 数据包。由于 uuencode 是一种广泛使用的数据编码方案，解码器 uudecode 也广泛可用，因此实际上任何人都可以解码 uuencoded 密码并可能滥用它。确实，数据包嗅探器必须能够找到正确的数据包才能进行解码，但技术上是可能的。这就是为什么你绝对不应该将基本 HTTP 验证用于任何关键应用程序的原因。例如，不要使用此方案来保护你国家的秘密。但是，如果你已经允许 Telnet 或 ftp 访问你的系统，那么你已经在这些服务中使用了与基本 HTTP 验证非常相似的验证方法。如果你信任你的服务器连接到 Internet，并且允许任何人尝试 Telnet 进入，那么你也没有理由不信任这种方法。

5.  如果用户名和密码有效（即真实），服务器返回请求的页面。这在图中是 (5a)。如果用户名和密码无效，服务器以 401 状态响应，并将相同的 WWW-Authenticate 响应头部发送到浏览器。这在图中是 (5b)。
6.  在浏览器会话期间对同一服务器的每个后续请求中，浏览器都会发送用户名和密码对，这样服务器就不必为落入网站同一区域下的调用生成 401 状态头部。例如，如果 URL `/apache.nitcc.com/protected/` 需要基本 HTTP 验证，那么对 `http://apache.nitcc.com/protected/a=page.html` 和 `http://apache.nitcc.com/protected/b=page` 的后续调用也需要用户名和密码。这就是为什么浏览器在服务器发出另一个验证挑战（即 401 状态头部和 WWW-Authenticate 响应头部）之前发送这两个信息的原因。这比为每个请求生成挑战并让用户重复输入用户名和密码要快且更实用。





## 通过 mod_auth 模块对用户进行身份验证

_mod_auth_ 模块是 Apache 的默认身份验证模块。该模块允许你验证存储在文本文件中的用户凭据。通常，系统会使用包含用户名和加密密码的文本文件。你还可以使用文本文件创建用户组，这些用户组可用于创建授权规则（将在本章稍后讨论）。建议对少量用户采用基于 _mod_auth_ 的身份验证。通常，当文本文件中的用户名达到数千个时，查找性能就会大幅下降。因此，如果你拥有非常大的用户群，则不建议使用此模块。但是，该模块非常适合大约几百名用户的情况。

你可以使用 _/usr/local/apache/bin/httpd -l_ 来验证此模块是否已编译到你的 Apache 二进制文件中。如果没有，则需要在 _configure_ 脚本中使用 _--enable-module=auth_ 选项，并重新编译和重新安装你的 Apache 发行版。

### 理解 mod_auth 指令

_mod_auth_ 模块提供了 Apache 指令 _AuthUserFile_、_AuthGroupFile_ 和 _AuthzAuthoritative_。让我们看看这些指令以及使用该模块的一些示例。

#### AuthUserFile 指令

此指令设置用于基本 HTTP 身份验证的用户名和密码所在的文本文件的名称。此指令要求你提供要使用的文件的完全限定路径。

- **语法：** _AuthUserFile filename_
- **上下文：** Directory, 每目录访问控制文件 (_.htaccess_)
- **覆盖：** _AuthConfig_

例如，以下指令将 _/www/mobidac/secrets/.htpasswd_ 设置为用户名和密码文件：

```apache
AuthUserFile /www/mobidac/secrets/.htpasswd
```

用户名和密码文件通常使用名为 _htpasswd_ 的工具创建，该工具作为支持程序包含在标准 Apache 发行版中。此文件的格式非常简单。每行包含一个用户名和一个加密密码。密码使用标准 _crypt()_ 函数进行加密。

> **注意**
> 重要的是，`AuthUserFile` 指定的文件必须位于 Web 站点的文档树之外。如果将其放在 Web 可访问的目录内，可能会允许某人下载该文件。

#### AuthGroupFile 指令

此指令指定用于基本 HTTP 身份验证的用户组列表的文本文件。文件名是组文件的绝对路径。你可以使用任何文本编辑器创建此文件。

- **语法：** `AuthGroupFile filename`
- **上下文：** Directory, 每目录访问控制文件 (`.htaccess`)
- **覆盖：** `AuthConfig`

此文件的格式为：

```text
groupname: username username username [...]
```

例如：

```text
startrek: kirk spock picard data
```

这将创建一个名为 `startrek` 的组，其中包含四个用户：`kirk`、`spock`、`picard` 和 `data`。上一节中的注意图标也适用于此指令。

#### AuthAuthoritative 指令

如果你对同一目录使用多个身份验证方案，可以将此指令设置为 `off`，这样当用户名/密码对在第一方案中失败时，它会传递到下一个（较低）级别。

- **语法：** `AuthAuthoritative On | Off`
- **默认值：** `AuthAuthoritative On`
- **上下文：** Directory, 每目录访问控制文件 (`.htaccess`)
- **覆盖：** `AuthConfig`

例如，如果你使用 `mod_auth_mysql`（将在本章稍后讨论）和标准 `mod_auth` 模块来提供身份验证服务，并且其中一个模块的用户名/密码对失败，则在可能的情况下，下一个模块将用于验证用户。当用户名/密码对在所有模块中均失败时，服务器会重新发出 401 状态标头并发送 `WWW-Authenticate` 响应标头以进行重新身份验证。然而，如果某个模块成功验证了用户名/密码对，较低级别的模块将不会收到该用户名/密码对。

建议保持默认值不变，因为你不应设计一种逐级下传的身份验证方案，即用户可能在一个模块中失败但在另一个模块中通过。

## 在你的 Web 站点中创建仅限成员的区域

通过使用 `mod_auth` 指令，你可以在你的 Web 站点上创建仅限成员的区域，该区域需要基于用户名/密码的身份验证。例如，假设你想创建一个名为 `http://your_server_name/memberonly` 的仅限成员的区域。以下是操作方法。

1. 确定你想要限制访问的物理目录。大多数人使用 `DocumentRoot` 指定目录内的一个目录，但你可以使用任何目录，只要 Apache 用户（由 `User` 指令设置）被允许读取目录的内容即可。这里，假设你的 `DocumentRoot` 设置为 `/www/mysite/htdocs`，并且你想要限制访问名为 `/www/mysite/htdocs/memberonly` 的目录。

2. 修改 `httpd.conf` 文件以创建一个名为 `/memberonly/` 的新别名，如下所示：

   ```apache
   Alias /memberonly/ "/www/mysite/htdocs/memberonly/"
   ```

3. 接下来，将以下指令添加到 `httpd.conf` 文件中，以将 `/memberonly/` 设置为需要用户身份验证的限制区域。

   ```apache
   <Location /memberonly/>
       AuthName "Member-Only Access"
       AuthType Basic
       AuthUserFile /www/secrets/.members
       require valid-user
   </Location>
   ```

   这里，`AuthName` 指令只是创建一个标签，该标签由 Web 浏览器显示给用户。该标签应该是某种有意义的东西，以便用户知道正在请求什么。请务必使用如上所示的双引号。`AuthType` 始终设置为 `Basic`，因为 HTTP 默认仅支持 `Basic` 身份验证。`AuthUserFile` 指向一个名为 `.members` 的密码文件。`Require` 指令声明只有有效用户才被允许访问。

4. 现在，使用 `htpasswd` 工具创建密码文件。假设你已将 Apache 安装在 `/usr/local/apache`，`htpasswd` 命令应仅在第一次运行时按如下方式执行：

   ```bash
   /usr/local/apache/bin/htpasswd -c path_to_password_file
   username
   ```

   `-c` 选项仅用于创建文件，并且应仅使用一次。例如，要为上述 `/memberonly/` 配置创建第一个名为 `mrbert` 的用户，请运行：

   ```bash
   /usr/local/apache/bin/htpasswd -c /www/secrets/.members mrbert
   ```

5. 为确保用户已创建在密码文件中，请使用文本编辑器查看其内容。此外，请确保只有 Apache 用户（使用 `User` 指令设置）可以访问此文件。例如，如果你以 `httpd` 用户身份运行 Apache，你可以运行 `chown httpd:httpd /www/secrets/.members && chmod 750 /www/secrets/.members` 命令，以确保只有 httpd 用户（和组）可以读取此文件。

6. 使用 `/usr/local/apache/bin/apachectl restart` 命令重启 Apache 服务器。

7. 现在，使用 `http://your_server_name/memberonly/` 访问仅限成员的区域；你应该会被要求输入用户名和密码。你应该在显示的对话框中看到 `AuthName` 的值（“`Member-Only Access`”）。

8. 输入无效的用户名和密码，你应该看到拒绝消息。

9. 最后，再次尝试访问该站点，然后输入由 `htpasswd` 工具创建的有效用户名和密码。你应该能够访问受限区域。

> **注意**：如果你使用默认的通用日志格式来记录访问，你可以在日志文件中看到已登录的用户名。

### 使用 `.htaccess` 文件创建仅限成员的区域

对于诸如互联网服务提供商 (ISP) 和在同一 Web 服务器上运行虚拟 Web 站点的许多部门的大型公司之类的组织，在 `httpd.conf` 中添加仅限成员的配置（在上一节中已讨论）可能不是一个可管理的解决方案，因为你必须根据各种用户（在 ISP 设置中）请求此类变更的速度来添加或移除配置。然而，通过使用基于 `.htaccess` 的身份验证，你可以允许用户或部门创建任意多的仅限成员区域，而无需你的参与——这对于忙碌的系统管理员来说是一种福音。

要对仅限成员的身份验证使用基于 `.htaccess` 的身份验证，请遵循以下步骤。

1. 在你的 `httpd.conf` 文件中添加以下指令：

   ```apache
   AccessFileName .htaccess
   ```

   > **注意**：如果你希望仅为虚拟主机启用基于 `.htaccess` 的身份验证，请在此指令放在适当的 `<VirtualHost>` 容器内。

2. 更改以下默认配置：

   ```apache
   <Directory />
    Options FollowSymLinks
    AllowOverride None
   </Directory>
   ```

   改为：





```
<Directory />
Options FollowSymlinks
AllowOverride AuthConfig
</Directory>
```

这允许在 .htaccess 文件中使用授权指令（AuthDBMGroupFile、AuthDBMUserFile、AuthGroupFile、AuthName、AuthType、AuthUserFile、Require 等）。

3. 使用 `/usr/local/apache/bin/apachectl` restart 命令重启 Apache 服务器。

4. 现在，您可以在任何可访问的 Web 目录中创建一个 .htaccess 文件，并控制对该目录的访问。您需要在 .htaccess 文件中包含以下指令：

```
AuthName "在此输入适当的标签"
AuthType Basic
AuthUserFile 用户密码文件路径
Require valid-user
```

例如，假设您有一个名为 `/www/mysite/htdocs/asb` 的目录，并希望将对该目录的访问限制为列在 `/www/mysite/secrets/users.pwd` 中的用户。为此，您可以使用以下配置：

```
AuthName "仅限 ASB 成员访问"
AuthType Basic
AuthUserFile /www/mysite/secrets/users.pwd
Require valid-user
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_218_0.png)

> 请确保 .htaccess 文件仅可读给 Apache 用户（通过 user 指令设置）。例如，如果您以 httpd 身份运行 Apache，则可以在存放该文件的目录下运行 `chown httpd:httpd .htaccess && chmod 750 .htaccess` 命令。请注意，创建或修改 .htaccess 文件不需要重启 Apache 服务器，因此您可以尝试网站的受限部分，以确定认证过程是否正常工作。

## 将用户分组以限制对不同 Web 部分的访问

如果您不同的用户需要访问网站的不同部分，您有多种选择。除了仅仅要求 valid-user 配置（这将向所有有效用户开放受限部分）之外，您还可以使用特定的用户名。例如：

```
<Location /financial>
AuthName "仅限成员"
AuthType Basic
AuthUserFile /www/mysite/secrets/.users.pwd
require cgdoave jolson
</Location>

<Location /sales>
AuthName "仅限成员"
AuthType Basic
AuthUserFile /www/mysite/secrets/.users.pwd
require esmith jkirk
</Location>
```

这里只有 cgodsavе 和 jolson 可以访问 /financial 部分，而 esmith 和 jkirk 可以访问 /sales 部分。然而，在配置中命名所有用户是一项繁琐且往往难以管理的工作。一种方法是创建单独密码文件，这将使上述配置段看起来如下：

```
<Location /financial>
AuthName "仅限成员"
AuthType Basic
AuthUserFile /www/mysite/secrets/.financial-team.pwd
require valid-user
</Location>

<Location /sales>
AuthName "仅限成员"
AuthType Basic
AuthUserFile /www/mysite/secrets/.sales-team.pwd
require valid-user
</Location>
```

现在，只将应添加的用户添加到 `/www/mysite/secrets/.financial-team.pwd` 中，在本例中是 cgodsavе 和 jolson，并只将应添加的用户添加到 `/www/mysite/secrets/.sales-team.pwd` 中，在本例中是 esmith 和 jkirk。

然而，如果维护多个密码文件并不吸引人，还有另一种方法。例如，看看以下配置段：

```
<Location /financial>
AuthName "仅限成员"
AuthType Basic
AuthUserFile /www/mysite/secrets/.members.pwd
AuthGroupFile /www/mysite/secrets/.groups
require group financial
</Location>

<Location /sales>
AuthName "仅限成员"
AuthType Basic
AuthUserFile /www/mysite/secrets/.members.pwd
AuthGroupFile /www/mysite/secrets/.groups
require group sales
</Location>
```

这里两个位置都使用相同的密码文件 .members.pwd，但每个位置使用不同的组。组文件是通用的，因为组文件可以包含多个组。组文件 /www/mysite/secrets/.groups 是一个简单的文本文件，对于上面的示例，其外观如下：

```
financial: cgodsav jolson
sales: esmith jkirk
```

现在，要向组中添加新用户，无需修改 httpd.conf 文件（或者，如果您使用 .htaccess 文件，则无需修改 `<Location>` 容器）。在创建用户账户后（使用 httpasswd 命令），您可以直接将用户添加到组文件中的适当组中。

# 通过主机名或 IP 地址授权访问

在这种授权方案中，由主机名或主机的 IP 地址控制访问。当对某个资源发出请求时，Web 服务器检查请求主机是否被允许访问该资源，并根据其发现采取行动。

标准的 Apache 发行版包含一个名为 `mod_access` 的模块，该模块允许基于 Web 客户端的 Internet 主机名进行访问控制。主机名可以是完全限定域名 (FQDN)，例如 `blackhole.mobicad.com`，也可以是 IP 地址，例如 `192.168.1.100`。该模块通过以下 Apache 指令提供此访问控制支持：`allow`、`deny`、`order`、`allow from env-variable` 和 `deny from env-variable`。

## allow 指令

此指令允许您定义一个允许访问特定目录的主机列表（包含一个或多个主机或 IP 地址）。当指定多个主机或 IP 地址时，它们应该用空格字符分隔。表 7-1 显示了该指令的可能值。

**语法：** Allow from host1 host2 host3 ...

**上下文：** Directory, location, per-directory access control file (.htaccess)

**覆盖：** Limit

表 7-1
allow 指令的可能值

| 值 | 示例 | 描述 |
|-------|---------|-------------|
| All | `allow from all` | 此保留关键字允许所有主机访问。示例展示了如何使用此选项。 |
| 主机的 FQDN | `allow from wormhole.mobidac.com` | 只有具有指定域名 (FQDN) 的主机被允许访问。示例中的 `allow` 指令只允许 `wormhole.mobidac.com` 访问。请注意，这比较的是完整组件；`toys.com` 不会匹配 `etoys.com`。 |
| 主机的部分域名 | `allow from .mainoffice.mobidac.com` | 只有匹配部分主机名的主机被允许访问。示例允许 `.mainoffice.mobidac.com` 网络中的所有主机访问该站点。例如，`developer1.mainoffice.mobidac.com` 和 `developer2.mainoffice.mobidac.com` 可以访问该站点。然而，`developer3.baoffice.mobidac.com` 不被允许访问。 |
| 主机的完整 IP 地址 | `allow from 192.168.1.100` | 只允许指定的 IP 地址访问。示例显示了被允许访问的完整 IP 地址（存在 IP 的所有四个八位组），`192.168.1.100`。 |
| 部分 IP 地址 | 示例 1: `allow from 192.168.1`<br>示例 2: `allow from 130.86` | 当 `allow` 指令中 IP 地址的八位组少于四个时，部分 IP 地址从左到右进行匹配，具有匹配 IP 地址模式（即属于同一子网）的主机被允许访问。在第一个示例中，IP 地址在 `192.168.1.1` 到 `192.168.1.255` 范围内的所有主机都有访问权限。在第二个示例中，来自网络的所有主机都被允许访问。 |
| 网络/ 子网掩码对 | `allow from 192.168.1.0/ 255.255.255.0` | 这允许您使用网络和子网掩码地址指定 IP 地址范围。示例只允许 IP 地址在 192.168.1.1 到 192.168.1.255 范围内的主机访问。 |
| 网络/nnn CIDR 规范 | `allow 206.171.50.0/24` | 与前面的条目类似，只不过子网掩码由 nnn 个高位 1 位组成。示例等效于允许 IP 地址在 206.171.50.0/255.255.255.0 范围内的主机访问。 |

## deny 指令

此指令是 `allow` 指令的完全相反。它允许您定义一个被拒绝访问指定目录的主机列表。与 `allow` 指令一样，它可以接受表 7-1 中显示的所有值。

- **语法：** `deny from host1 host2 host3 [...]`
- **上下文：** `Directory, location, per-directory access control file (.htaccess)`
- **覆盖：** `Limit`

## order 指令

此指令控制 Apache 如何评估 `allow` 和 `deny` 指令。

- **语法：** `order deny, allow | allow, deny | mutual-failure`
- **默认值：** `order deny, allow`
- **上下文：** `Directory, location, per-directory access control file`
- **覆盖：** `Limit`

例如，以下指令拒绝主机 `myboss.mycompany.com` 的访问，同时允许所有其他主机访问该目录。`order` 指令的值是一个逗号分隔的列表，指示哪个指令具有优先权：





## 允许来自环境变量=变量指令

```
<Directory /Mysite/myboss/rants>
order deny, allow
deny from myboss.mycompany.com
allow from all
</Directory>
```

通常，影响所有主机的指令优先级最低。在上面的示例中，由于`allow`指令影响所有主机，因此它的优先级较低。

尽管`allow`、`deny`和`deny, allow`是`order`指令最常用的值，但你也可以使用另一个值`mutual-failure`，以表明只有那些出现在`allow`列表中但未出现在`deny`列表中的主机才能访问。在所有情况下，每一个`allow`和`deny`指令都会被评估。

### 拒绝来自环境变量=变量

此指令是`deny`指令的一种变体，它拒绝所有设置了指定环境的主机的访问权限。

**语法**: `deny from env=variable`

**上下文**: 目录、位置、目录级访问控制文件（.htaccess）

**覆盖**: 限制

例如，如果你想拒绝所有使用微软Internet Explorer的主机访问，你可以使用`BrowserMatch`指令，每当浏览器向服务器标识自己并包含字符串"MSIE"时，设置一个名为`ms_browser`的变量。

```
BrowserMatch "MSIE" ms_browser
```

现在你可以使用`<Directory>`容器来指定`deny`指令，如下所示：

```
<Directory /path/to/vbscript_directory>
    order deny,allow
    allow from all
    deny from env=ms_browser
</Directory>
```

如果你有兴趣阻止对特定HTTP请求方法（如GET、POST或PUT）的访问，你可以使用`<Limit>`容器来实现。例如：

```
<Location /cgi-bin>
    <Limit POST>
        order deny,allow
        deny from all
        allow from yourdomain.com
    </Limit>
</Location>
```

此示例允许对`cgi-bin`目录的POST请求，仅当请求来自`yourdomain.com`域中的主机时。换句话说，如果该网站有一些HTML表单通过HTTP POST方法发送用户输入数据，那么只有yourdomain.com的用户才能有效使用这些表单。通常，CGI应用程序存储在`cgi-bin`目录中，许多网站都提供使用POST方法向CGI应用程序提交数据的HTML表单。使用上述基于主机的访问控制配置，网站可以允许任何人运行CGI脚本，但只允许特定网站（在此情况下为yourdomain.com）实际向一个或多个CGI脚本发布数据。这使得该网站的CGI访问具有一定的只读特性。每个人都可以运行生成输出的应用程序而不接受任何用户输入，但只有特定域的用户才能提供输入。

### 组合身份验证与授权

mod_auth中的基本HTTP用户身份验证支持和mod_access中的访问授权支持可以结合起来实现实际的身份验证问题。例如，假设你希望允许一组用户仅在他们通过AOL连接浏览网站时才能访问你网站的/aolbuddies/部分。以下是你可以在httpd.conf中添加的配置，在适当替换路径和文件名之后：

```
Alias /aolbuddies/    "/path/to/web/directory/for/aolbuddies/"

<Location /aolbuddies/>
    Deny from all
    Allow from .aol.com

    AuthName "AOL Buddies Only"
    AuthType Basic
    AuthUserFile /path/to/.myusers.pwd
    AuthGroupFile /path/to/.mygroups
    Require group aolbuddies

    Satisfy all
</Location>
```

Satisfy all指令告知Apache仅允许通过身份验证和授权测试的用户访问。当AOL用户通过AOL连接到http://your_server/aolbuddies/时，系统会提示用户输入用户名和密码。如果用户输入属于aolbuddies组的用户名且用户密码正确，则允许用户访问。

> **注意** 你必须将所有你的AOL好友添加为/path/to/.myusers.pwd中的用户，并在/path/to/.mygroups中创建一个名为aolbuddies的组，该组中列出所有AOL好友（你之前添加的/path/to/.aol中的用户）。

### 使用关系数据库进行身份验证

如果你在网络（甚至Web服务器）上运行关系数据库服务器，并且有大量的用户（即超过1,000名用户）需要通过Web进行身份验证，你可以使用数据库服务器替代前文讨论的基于文本文件的（mod_auth）身份验证。使用数据库服务器处理大量用户有几个优点；主要优点如下：

- 当大量用户存储在文本文件中时，mod_auth身份验证会变得非常缓慢。
- 如果你允许用户通过Web使用自定义应用程序更改密码，文本文件是不安全的，因为你必须确保对文件的写访问正确地加锁和解锁。将数据存储在数据库服务器中消除了脚本中的这种额外负担，并提供了更好的整体数据完整性。

在关系数据库中，你可以存储大量关于用户的信息，这些信息可以被你的Web应用程序使用。因此，使用MySQL等数据库服务器集中用户数据库对长期来看是有意义的。

### 注意事项

你可以使用大多数现代关系数据库服务器（如MySQL、Postgres、DB2、Oracle和Microsoft SQL）作为用户数据库。安装这些数据库服务器中的任何一个超出了本书的范围。我假设你已经在你的网络或Web服务器上安装了这些数据库服务器之一。

### 提示

对于拥有许多用户的网站，你可能希望创建一个专用的数据库服务器，使其在你的Web网络上可访问。理想情况下，数据库服务器应通过后端网络而不是互联网进行访问。大多数情况下，最好在每台服务器系统上有一个额外的以太网接口，并创建一个仅局域网内的服务器可访问的LAN。（有关如何创建此类网络的详细信息，请参阅第23章。）

### 使用MySQL数据库服务器进行身份验证

MySQL是开源社区中最广泛使用的免费数据库服务器；它在GNU公共许可下可用。安装和设置你的服务器作为用户身份验证数据库服务器非常容易。使用Linux平台，你可以简单地下载并安装服务器、客户端和开发RPM包，几分钟内即可就绪！MySQL服务器可在www.mysql.com下载。

### 在MySQL服务器中创建用户身份验证数据库

要将MySQL服务器用作身份验证数据库，你需要在数据库中的表中至少包含用户名和密码信息。如果你已经有了包含此类信息的现有数据库表，则无需遵循此处给出的步骤。

1. 使用`mysql -u root -p`命令登录到MySQL服务器。你将需要输入数据库的root密码。

### 警告

MySQL服务器的root密码应始终与你的Unix系统上的root密码不同。它们服务于不同的目的，因此应保持分开。

2. 登录到MySQL后，运行`create database auth;`命令，这将创建一个名为`auth`的数据库。





## 创建数据库和表

3. 使用以下命令将当前数据库切换到新创建的 auth 数据库：

   ```sql
   use auth;
   ```

4. 现在，在 MySQL 命令提示符中输入以下行来创建一个名为 wwwusers 的表。

   ```sql
   create table wwwusers (
   username varchar(40) not null primary key,
   passwd varchar(20) not null
   );
   ```

该表中的每一行由三个字段组成：username、passwd 和 groups。username 字段是主键，这意味着 MySQL 使用此字段对表进行索引，使得使用 username 进行的查找非常快。该字段限制为 40 个字符。使用 varchar（可变字符）而不是固定 char 类型，如果用户名并非总是 40 个字符，可以节省空间。由于该字段也是主键，因此 username 字段不能为空（即不能为空值）。密码字段称为 passwd，其长度最大为 20 个字符，类型为 varchar。它不能为空。

5. 现在输入 `describe wwwusers;` 命令，应显示以下输出：

   ```text
   mysql> describe wwwusers;
   +----+-----+------+-----+---------+-------+
   | Field | Type | Null | Key | Default | Extra |
   +----+-----+------+-----+---------+-------+
   | username | varchar(40) | | PRI | | |
   | passwd | varchar(20) | | | | |
   +----+-----+------+-----+---------+-------+
   2 rows in set (0.00 sec)
   ```

这是对表 *wwwusers* 已按预期创建的事实进行验证。

6. 现在您需要向表中添加用户。若要手动添加用户，您需要运行以下 SQL 语句：

   ```sql
   insert into wwwusers (username , passwd)
   values ('user_name',
   'user_password');
   ```

例如：

   ```sql
   insert into wwwusers (username , passwd)
   values ('esmith', 'sale007');
   ```

这里添加了一个名为 esmith 的用户，密码为 sale007，属于 sales 组。您可以添加任意数量的用户。有关如何使用实用脚本管理用户的详细信息，请参见 [在任意 RDBM 中管理用户和组](https://www.example.org/managing_users)。

7. 如果您计划使用用户组进行身份验证，请创建以下表。

   ```sql
   create table wwwgroups ( username  varchar(40), groupname  varchar(40) );
   ```

8. 现在输入 `describe wwwgroups;` 命令，应显示以下输出：

   ```text
   +------------+------------+------+-----+--------+
   | Field      | Type       | Null | Key | Default |
   +------------+------------+------+-----+--------+
   | username   | varchar(40)| YES  |     | NULL   |
   | groupname  | varchar(40)| YES  |     | NULL   |
   +------------+------------+------+-----+--------+
   2 rows in set (0.00 sec)
   ```

这是对表 *wwwgroups* 已按预期创建的事实进行验证。

9. 您可以使用以下 SQL 语句将现有用户添加到新组中：

   ```sql
   insert into wwwgroups (username , groupname)
      values ('user_name',
              'name_of_the_group'
      );
   ```

例如：

   ```sql
   insert into wwwgroups (username , groupname)
      values ('kabir',
              'www_wheel'
      );
   ```

这将用户 *Kabir* 添加到一个名为 *www_wheel* 的新组中。请注意，您可以将同一用户添加到多个组中。

## 授予 Apache 服务器访问 MySQL 中的用户身份验证数据库

与大多数现代 RDBM 服务器一样，MySQL 自身使用基于用户名和密码的身份验证来允许访问其存储的数据库。因此，在使用 Apache 配合 MySQL 之前，您应该创建一个名为 *httpd* 的 MySQL 用户，该用户应能访问您计划与 Apache 一起使用的任何数据库。以下是如何为 Apache 创建 MySQL 用户：

1. 使用 `mysql -u root -p` 命令登录到 MySQL 服务器。系统会提示您输入数据库的 root 密码。

2. 登录 MySQL 后，您可以发出如下 *grant* 语句：

   ```sql
   grant all privileges on name_of_database
   to username@hostname identified by 'user_password'
   with GRANT option;
   ```

例如，要授予名为 `httpd` 的用户（即 `httpd.conf` 文件中 `user` 指令指定的用户名）对名为 `auth` 的数据库的所有权限，当使用 `2manyscrets` 密码从 localhost 连接时，请运行：

   ```sql
   grant all privileges on auth
       to httpd@localhost identified by '2manyscrets'
       with GRANT option;
   ```

这允许 `httpd` 用户从 localhost 访问 `auth` 数据库。此操作假设 MySQL 服务器和 Apache 服务器运行在同一台机器上。如果数据库位于另一台机器上，您应使用相应的主机名替换 localhost。

如果您不打算添加需要向用户身份验证数据库写入的 Web 应用程序，请勿授予 Web 服务器用户 `all privileges`。例如，如果您只是想验证用户身份，但从不通过 Web 服务器（即使用 CGI 脚本或其他 Web 应用程序）更新或删除用户，请将 `all privileges` 替换为 `select`。这确保 Web 服务器用户仅允许对数据库执行 `select` 查询，相当于只读访问。

3. 输入 `flush privileges` 命令，指示 MySQL 服务器重新加载授权表。

4. 现在您应该通过输入 `exit` 退出 MySQL 监控程序。

现在，通过输入 `mysql -u httpd -p` 命令并提供适当的密码（在此情况下为 `2manysecrets`）登录 MySQL。在 `mysql>` 提示符下，您应该能够通过输入 `use auth;` 访问数据库 `auth`。如果您无法访问数据库，请确保您位于早期发出的 grant 语句中指定的主机上。

## 编译和安装 mod_auth_mysql 模块

MySQL 数据库服务器在开源社区中的良好声誉促成了一个名为 `mod_auth_mysql` 的 Apache 模块的开发。该模块可用于与 MySQL 服务器接口以进行身份验证。您可以从 www.mysql.com/Downloads/Contrib/ 下载此模块的最新版本。以下是如何编译和安装 `mod_auth_mysql`。

1. 以 root 身份在 `/usr/local/src` 目录中提取 `mod_auth_mysql` 源代码发行版。这将创建一个名为 `mod_auth_mysql-version` 的新子目录。切换到该目录并运行：

   ```bash
   ./configure --with-apache=/usr/local/src/apache_version
       --with-mysql=/usr
   ```

请务必将 `/usr/local/src/apache_version` 更改为 Apache 源代码发行版的路径，并将 `/usr` 更改为 MySQL 头文件安装的路径。如果您使用默认配置安装了 MySQL，头文件安装在 `/usr/local/mysql`，并且提供 `--with-mysql=/usr` 是正确的值，因为 `mod_auth_mysql` 脚本通过将 `/local/mysql` 附加到 `/usr` 来生成 `/usr/local/mysql`。

2. 运行 `make`，然后切换到 Apache 源代码发行版目录，并运行 `./config.status --activate-module=src/modules/auth_mysql/libauth_mysql.a`（如果您已经编译了 Apache）或 `./configure --activate-module=src/modules/auth_mysql/libauth_mysql.a --prefix=/usr/local/apache`（如果您第一次编译 Apache）。

3. 最后，运行 `make && make install` 来编译并安装带有 `mod_auth_mysql` 支持的 Apache。

4. 现在使用 `/usr/local/apache/bin/apachectl restart` 命令重启 Apache 服务器。

### 使用 `mod_auth_mysql` 模块对用户进行身份验证

在您编译并安装了 `mod_auth_mysql`，创建了包含用户和组表的数据库，并且为 Apache 创建了访问这些表的数据库级用户之后，您可以按如下方式配置 Apache：

1. 在 `httpd.conf` 中，在任何 `<VirtualHost>` 或其他类型的容器（如 `<Directory>`、`<Location>` 等）外部添加以下行。

   ```apache
   Auth_MySQL_Info db_hostname db_username db_password
   Auth_MySQL_General_DB database_name
   ```

   第一个指令告诉 Apache 使用哪个数据库用户名和密码连接哪个数据库服务器。数据库用户名和密码是在 MySQL 中创建的。此用户名密码对必须与您系统上的任何交互式用户账户不匹配。

   第二个指令说明要连接哪个数据库。如果您使用单个数据库来满足所有用户身份验证需求，可以在此处直接设置数据库名称。这样可以避免在每个身份验证配置段中重复输入数据库名称。

2. 若要要求对文档根目录下名为 `protected_dir` 的子目录进行身份验证，您可以在 `httpd.conf` 中创建 `<Directory>` 或 `<Location>` 容器，或者使用 `.htaccess` 文件（假设您已在 `httpd.conf` 中将 `AllowOverride AuthConf` 设置为主服务器或适当的虚拟主机），使其具有以下配置段：

   ```apache
   AuthName "Members Only"
   AuthType Basic
   require valid-user

   Auth_MySQL on
   ```





```
Auth_MySQL_DB database_name
Auth_MySQL_Password_Table password_table_name
Auth_MySQL_Username_Field username_field_name
Auth_MySQL_Password_Field password_field_name

Auth_MySQL_Group_Table group_table_name
Auth_MySQL_Group_Field group_field_name

Auth_MySQL_Empty_Passwords off
Auth_MySQL_Encrypted_Passwords on
Auth_MySQL_Encryption_Types Crypt_DES
Auth_MySQL_Scrambled_Passwords off
Auth_MySQL_Authoritative on
Auth_MySQL_Non_Persistent off
```

**注意**

别忘了将 `database_name`、`password_table_name`、`username_field_name`、`password_field_name`、`group_table_name` 和 `group_field_name` 替换为相应的具体信息。

- `Auth_MySQL` 指令用于开启或关闭 `mod_auth_mysql`。
- `Auth_MySQL_DB` 指令指定数据库名称，该数据库包含由 `Auth_MySQL_Password_Table` 指定的密码表和由 `Auth_MySQL_Group_Table` 指定的组表。
- `Auth_MySQL_Username_Field` 和 `Auth_MySQL_Password_Field` 指令指定用于在密码表中存储用户名和密码的字段名称。
- `Auth_MySQL_Group_Field` 指令指定组名称字段。
- `Auth_MySQL_Empty_Passwords` 设置为 off，因为空密码不适合大多数认证需求。
- 使用 `Auth_MySQL_Encrypted_Passwords` 开启加密密码支持，并通过使用 `Auth_MySQL_Encryption_Types` 将加密类型设置为传统的 Unix 风格 `Crypt_DES`。

**注意**

虽然你可以从 `Plaintext`、`Crypt_DES` 和 `MySQL` 加密类型中任选一种，但我从不推荐使用明文密码。由于 `Auth_MySQL_Scrambled_Passwords` 在大多数场景下并不适用，因此支持该功能的选项已被关闭。

- 由于允许一种“降级认证”方案（即如果一种方案未能允许用户访问，则可以使用另一种方案来允许访问）并非好主意，因此开启了 `Auth_MySQL_Authoritative` 指令。这告诉 Apache 忽略用于同一目录的所有其他认证方案。如果 `mod_auth_mysql` 无法允许用户访问受限目录，Apache 将简单地重新发出认证请求。

- 最后一个指令 `Auth_MySQL_Non_Persistent` 告诉 Apache 不要针对每个认证请求断开与数据库服务器的连接。针对每个请求断开连接意味着 Apache 必须为每个新的认证请求重新建立连接，这对性能不利。因此，建议使用默认值（off）。

3. 如果你将上述配置添加到 `httpd.conf` 中的 `<Directory>` 或 `<Location>` 容器内，你需要使用 `/usr/local/apache/bin/apachectl restart` 命令重启 Apache 服务器。另一方面，如果你在上述配置中使用了 `.htaccess` 文件，则无需重启服务器即可使用。

## 使用其他数据库进行用户认证

你可以使用 Postgres、IBM DB2、Oracle 或其他服务器作为数据库，而不是使用 MySQL 服务器来为 Apache 进行用户认证。虽然你可能找不到适用于你特定关系型数据库管理系统（RDBM）的 Apache 模块（如 `mod_auth_mysql`），但你可以在 `mod_perl` 中使用 `Apache::AuthDBI` 模块（有关如何安装 `mod_perl` 的详细信息，请参阅第 16 章，该章讨论了 `mod_perl` 的使用）来与你的数据库服务器通信并执行用户认证。请按照以下步骤操作：

1. 确保已安装随你的数据库服务器包提供的所有必要库和头文件。通常，这意味着你需要为你的 RDBM 安装软件开发套件（SDK）。

2. 使用 `perl -MCPAN -e 'install DBI'` 命令安装最新版本的 DBI 模块。

3. 使用 `perl -MCPAN -e 'install DBD:database'` 命令安装 Perl（DBD）的相应数据库驱动器的最新版本。例如，要安装 IBM DB2 的数据库驱动器，你需要运行 `perl -MCPAN -e 'install DBD::db2'`。

4. 使用 `perl -MCPAN -e 'install Apache::AuthDBI'` 命令安装最新版本的 `Apache::AuthDBI`。

5. 创建一个数据库用户账户，供 Apache 连接数据库服务器使用。这不是用于访问系统（如 Linux 服务器本身）的账户。它是数据库引擎上的一个账户，授予 Apache 访问用户数据库及其表的权限。

6. 接下来，你需要创建前面“在 mysql 服务器中创建用户认证数据库”一节中讨论的 auth 数据库和 wwwuser 表。此外，务必使用本章后面“在任何 RDBM 中管理用户和组”一节中讨论的 `manage_users.pl` 脚本创建一个或多个测试用户。

7. 在 `httpd.conf` 中添加以下行：

```
PerlModule Apache::AuthenDBI
```

这告诉 Apache 你希望使用 `Apache::AuthenDBI` 模块。

8. 创建一个名为 `/memberonly/` 的别名，指向你希望限制访问的目录，使用以下 `Alias` 指令：

```
Alias /memberonly/ "path_to_restricted_access_directory"
```

例如：

```
Alias /memberonly/ "/usr/local/apache/htdocs/protected/"
```

这里 `/memberonly/` 别名指向 `/usr/local/apache/htdocs/protected/` 目录。

9. 现在在 `httpd.conf` 中创建以下配置段：

```
<Location /memberonly/>  
AuthName "Home" 
AuthType Basic 
PerlAuthenHandler Apache::AuthenDBI
PerlSetVar Auth_DBI_data_source dbi:mysql:database=auth
PerlSetVar Auth_DBI_username httpd 
PerlSetVar Auth_DBI_password 2manysecrets
PerlSetVar Auth_DBI_pwd_table wwwusers
PerlSetVar Auth_DBI_uid_field user
PerlSetVar Auth_DBI_pwd_field passwd
PerlSetVar Auth_DBI_encrypted on 
require valid-user 
</Location>
```

以下列表帮助你快速了解上述配置中正在发生的事情：

- 上述配置告诉 Apache 使用 `Apache::AuthenDBI` 作为 `/memberonly/` 别名对应的处理器。
- `PerlSetVar` 指令用于设置该模块所需的关键-值对。
  - `Auth_DBI_data_source` 键设置数据库 DSN，告诉模块使用哪个 Perl DBD 连接到哪个数据库。在这里，值设置为连接到名为 `auth` 的 MySQL 数据库。你应该将驱动器设置为你正在使用的任何 RDBM。例如，如果你使用的是 IBM DB2，你的数据库源名称（DSN）可能是 `dbi:db2:database=auth`。
- `Auth_DBI_username` 和 `Auth_DBI_password` 键设置用于连接到命名用户数据库（即 `auth`）的数据库用户名和密码。
  - 密码表的名称由 `Auth_DBI_pwd_table` 键指定；类似地，用户名和密码字段分别由 `Auth_DBI_uid_field` 和 `Auth_DBI_pwd_field` 键指定。
  - `Auth_DBI_encrypted` 键设置为 `on`，因此假设存储在数据库中的密码是使用名为 `crypt` 的传统 Unix 风格单向哈希加密函数加密的。
- 最后，`require valid-user` 指令告诉 Apache 仅允许通过认证测试的用户访问。

10. 你可以通过使用 `/usr/local/apache/bin/apachectl restart` 命令重启 Apache 服务器，并尝试访问 `http://your_server_name/memberonly` 目录，以查看是否可以使用无效的用户名和密码访问该目录。如果你输入有效的用户名和密码，你应该能够完成认证。

## 在任何 RDBM 中管理用户和组

手动管理数据库中的用户和组非常繁琐。幸运的是，你不必处理这类任务。你可以使用一组 Perl 脚本来相当高效地处理这些杂务。方法如下。

1. 你需要从 Perl 综合存档网络（CPAN）安装 **DBI** 包和相应的 **DBD::database** 模块。例如，如果你安装了 MySQL 数据库，你可以作为 root 用户通过命令行安装 **DBI** 和 **DBD** 模块，如下所示：

```
perl -MCPAN -e 'install DBI'
perl -MCPAN -e 'install DBD::mysql'
```

2. 检查你的已安装 Perl 发行版中是否有名为 **HTTPD::UserAdmin** 和 **HTTPD::GroupAdmin** 的两个 CPAN 模块。你可以运行 `locate UserAdmin.pm` 和 `locate GroupAdmin.pm` 命令来确定你是否有它们。通常，这两个模块作为标准发行版的一部分安装。例如，在我的系统中，这些模块显示如下：

```
/usr/lib/perl5/site_perl/5.6.0/HTTPD/UserAdmin.pm
/usr/lib/perl5/site_perl/5.6.0/HTTPD/GroupAdmin.pm
```

如果你没有这两个模块中的一个或两个，请如下安装：作为 root 从 CPAN 下载 **HTTPD::UserAdmin** 和 **HTTPD::GroupAdmin** CPAN 模块。在 Linux 系统上，你可以简单地运行以下命令来安装它们：

```
perl -MCPAN -e 'install HTTPD::UserAdmin'
perl -MCPAN -e 'install HTTPD::GroupAdmin'
```

**提示**
你可能想要安装 **HTTPD::Tools** 包，因为它除了包含这两个模块外，还包含其他对 Web 服务器普遍有用的模块。

3. 将 **manage_users.pl** 脚本从配套光盘复制到 `/usr/bin` 目录（有关如何找到 `/usr/bin` 的信息，请参阅光盘附录）。更改文件权限以允许你运行它。使用 `chmod 750 /usr/bin/manage_users.pl` 命令设置权限。

4. 使用你喜欢的文本编辑器修改脚本中的以下几行。

```
my $DB_HOST     = 'localhost';
my $DB_PORT     = ':';
my $DATABASE    = 'auth';
my $DB_DRIVER    = 'mysql';
```




my $DB_USER = 'kabin';
my $DB_PASSWORD = 'dbpwd';
my $ENCRYPTION = 'crypt';
my $USER_TABLE = 'wwwusers';
my $USERNAME_FIELD = 'username';
my $PASSWORD_FIELD = 'passwd';
my $GROUP_TABLE = 'wwwgroups';
my $GROUP_FIELD = 'groupname';
my $MAXSZ_USER = 40;
my $MAXSZ_PWD = 20;
my $MAXSZ_GRP = 40;

在上面的代码中，您需要设置以下变量：

-   $DB_HOST 变量应设置为您想要连接到的数据库服务器。如果数据库服务器与 Web 服务器位于同一台机器上，则默认值 'localhost' 可以保持不变。

-   $DB_PORT 变量应设置为数据库服务器端口。除非您在数据库服务器上用于客户端连接的端口非传统端口，否则端口会自动选择。

-   $DATABASE 变量应设置为数据库名称。默认数据库名称为 'auth'，只有按照本章前面章节的说明操作时才有效。

-   $DB_DRIVER 变量应设置为您连接数据库服务器所需的数据库驱动。对于 MySQL 数据库服务器，该驱动称为 mysql，因此默认值仅在使用 MySQL 数据库时有效。

-   $DB_USER 变量应设置为被授予在 $DATABASE 指定的表中创建、修改或删除记录权限的用户。关于如何授予用户访问 MySQL 数据库的权限，请参阅本章前面的“授予 Apache 服务器访问用户身份验证数据库”部分。

-   出于安全考虑，$DB_PASSWORD 有意未存储在脚本中。每次运行 manage_users.pl 脚本时，您必须使用命令行选项 -dbpwd=database_password 提供访问数据库所需的密码。您可以硬编码密码，但我建议在使用完脚本后移除硬编码的密码。

-   $ENCRYPTION 变量可以设置为 none、crypt（默认值）或 MD5。设置为 none 时，密码以纯文本形式存储；使用 crypt 时，密码使用传统 Unix 环境中使用的一次性哈希算法进行加密；使用 MD5 时，密码以信息摘要（MD5）值的形式存储。

-   $USER_TABLE 变量应设置为数据库中的用户表。该表必须包含 $USERNAME_FIELD 指定的用户名字段，以及 $PASSWORD_FIELD 指定的密码字段。

-   $GROUP_TABLE 变量应设置为数据库中的组表。该表必须包含 $USERNAME_FIELD 指定的用户名字段，以及 $GROUP_FIELD 指定的组名字段。

-   $USERNAME_FIELD 的最大大小通过使用 $MAXSZ_USER 字段设置，这应与您创建 $USER_TABLE 过程中使用的大小相对应。$PASSWORD_FIELD 的大小通过类似的方式使用 $MAXSZ_PWD 字段控制。最后，$GROUP_FIELD 的大小通过使用 $MAXSZ_GRP 字段控制。

5.  保存更改。

### 向用户表添加新用户

要向用户表添加新用户，请运行以下命令：

```
manage_user.pl -db=user \
-action=add \
-user=user_name \
-password=user_password \
-dbpwd=database_password
```

例如，要添加一个名为 `kabil`、用户密码为 `go#forward` 的用户，您可以运行以下命令：

```
manage_user.pl -db=user \
-action=add \
-user=kabil \
-password=go#forward \
-dbpwd=mydbpwd
```

请注意，这里的 `mydbpwd` 是写入数据库所需的数据库密码。

### 从用户表中删除现有用户

要从用户表和组表中删除用户，请运行以下命令：

```
manage_user.pl -db=user \
-action=del \
-user=user_name \
-dbpwd=database_password \
-auto=on
```

例如，要从用户表和组表中删除名为 `kabil` 的用户，并使用数据库访问密码 `mydbpwd`，您可以运行以下命令：

```
manage_user.pl -db=user \
-action=del \
-user=kabil \
-dbpwd=mydbpwd \
-auto=on
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_237_0.png)

设置 -auto 选项可确保用户从组表中的所有组中移除。

### 更新用户表中现有用户的密码

要更新用户表中用户的密码，请运行以下命令：

```
manage_user.pl -db=user \
-action=update \
-user=user_name \
-dbpwd=database_password
```

例如，使用数据库密码 mydbpwd 将用户 kabir 的密码更新为 mydbpwd，请运行以下命令：

```
manage_user.pl -db=user \
-action=update \
-user=kabir \
-dbpwd=mydbpwd
```

### 将用户添加到组

要将现有用户添加到新组或现有组，请运行以下命令：

```
manage_user.pl -db=group \
-action=add \
-user=user_name \
-group=group_name \
-dbpwd=database_password
```

例如，要将名为 kabir 的用户添加到名为 administrators 的组，请运行以下命令：

```
manage_user.pl -db=group \
-action=add \
-user=kabir \
-group=administrators \
-dbpwd=mydbpwd
```

这里的 mydbpwd 是写入组表所需的数据库密码。

### 从组中删除用户

要从组中删除用户，请运行以下命令：

```
manage_user.pl -db=group \
-action=del \
-user=user_name \
-group=group_name \
-dbpwd=database_password
```

例如，要从名为 administrators 的组中删除名为 `kabir` 的用户，请运行：

```
manage_user.pl -db=group \
-action=del \
-user=kabir \
-group=administrators \
-dbpwd=mydbpwd
```

这里的 `mydbpwd` 是更新组表所需的数据库密码。

## 使用 Cookie 保护身份验证会话

正如本章前面提到的，*基本 HTTP* 身份验证要求 Web 浏览器每次请求受限部分下的页面时，始终传递用户名和编码（非加密）的密码。这使得*中间人*攻击变得过于容易。这种攻击涉及黑客利用基本 HTTP 身份验证在 Web 服务器和 Web 浏览器之间拦截数据包，从而确定密码。

中间人攻击的解决方案是使用安全套接字层（SSL）连接和基于会话的身份验证方案，其中用户通过*基本 HTTP*身份验证进行一次认证，随后对受限资源的所有请求都使用安全的（加密的）会话 Cookie 而不是编码密码进行授权。

本节讨论了一种使用 MySQL 数据库（当然，您也可以使用其他任何 RDBMS）和 CPAN 上的 `mod_perl` 模块的解决方案。以下是如何实现该解决方案。

-   如果尚未安装，请按照第 16 章的说明安装 `mod_perl` 模块。

-   使用以下命令以 root 身份为 Apache 安装两个 CPAN 模块：

```
perl -MCPAN -e 'install Apache::AuthCookie'
perl -MCPAN -e 'install Apache::AuthTicket'
```

-   安装上述模块后，您需要创建本章前面“在 *mysql server* 中创建用户身份验证数据库”部分讨论的 auth 数据库和 wwwuser 表。您还需要添加以下两个表。

```
CREATE TABLE tickets (
 ticket_hash CHAR(32) NOT NULL,
 ts INT NOT NULL,
 PRIMARY KEY ( ticket_hash )
);

CREATE TABLE ticketsecrets (
 sec_version  BIGINT,
 sec_data     TEXT NOT NULL
);
```

按照本章前面“在 mysql server 中创建用户身份验证数据库”部分给出的说明，在 auth 数据库中添加这些表。

-   创建上述表后，您必须在 ticketsecrets 表中添加一个密钥。添加密钥最简单的方法是登录到数据库服务器，连接到 auth 数据库，并执行以下插入语句：

```
insert into ticketsecrets (sec_version, sec_data) values
('number', 'random_data');
```

-   确定您要限制访问并发放会话 Cookie 的 Web 目录位置。在本示例中，我将此位置称为 /protected。将以下配置添加到您的 httpd.conf 文件中：

```
PerlModule Apache::AuthTicket
PerlSetVar ProtectedTicketDB
DBI:mysql:database=auth:host=localhost
PerlSetVar ProtectedTicketDBUser httpd
PerlSetVar ProtectedTicketDBPassword secret1
PerlSetVar ProtectedTicketTable tickets:ticket_hash:ts
PerlSetVar ProtectedTicketUserTable wwwusers:username:passwd
PerlSetVar ProtectedTicketSecretTable
ticketsecrets:sec_data:sec_version
PerlSetVar ProtectedTicketPasswordStyle crypt
```

以下列表说明了上述配置中的各项内容：

-   这里的 `PerlModule` 指令告诉 Apache，您希望使用 `Apache::AuthTicket` 模块。

-   `PerlSetVar` 指令用于设置该模块所需的各个键值对。

-   `ProtectedTicketDB` 键设置数据库的数据源名称（DSN）。

-   示例值 `DBI:mysql:database=auth:host=localhost` 告诉 `AuthTicket` 模块，我们想使用 MySQL 数据库驱动（`mysql`）并连接到名为 `auth` 的数据库，该数据库位于本地主机（与 Web 服务器相同的机器）上。如果您未在与 Apache Web 服务器相同的机器上运行 MySQL 数据库服务器，请确保将此更改为适当的主机名。

-   `ProtectedTicketDBUser` 和 `ProtectedTicketDBPassword` 指令告诉 `AuthTicket` 模块访问数据库服务器所需的数据库用户名和密码。





-   `ProtectedTicketTable`、`ProtectedTicketUserTable` 和 `ProtectedTicketSecretTable` 键用于告诉模块在数据库中使用哪些票据和用户表以及需要哪些字段。
-   `ProtectedTicketPasswordStyle` 设置加密类型。您有三种选择：传统的 Unix 风格单向哈希加密（即 `crypt()`）、明文（不推荐）或 MD5。

6.  接下来添加以下配置行：

```
PerlSetVar ProtectedTicketExpires 30
PerlSetVar ProtectedTicketLogoutURI /protected/index.html
PerlSetVar ProtectedTicketLoginHandler /protected/login
PerlSetVar ProtectedTicketIdleTimeout 15
PerlSetVar ProtectedPath /
PerlSetVar ProtectedDomain .domain_name
PerlSetVar ProtectedSecure 1
PerlSetVar ProtectedLoginScript /protected/loginform
```

以下列表说明了上述配置的作用：

-   `ProtectedTicketExpires` 键设置会话（票据）的过期时间（以分钟为单位）。
-   `ProtectedTicketLogoutURI` 键设置用户注销后显示的 URL。
-   `ProtectedTicketLoginHandler` 设置登录处理程序的路径，该路径必须对应于一个 `<Location>` 容器，如后文所述。
-   `ProtectedTicketIdleTimeout` 设置会话允许空闲的分钟数。
-   `ProtectedPath` 设置 cookie 的路径。默认值 `/` 确保 cookie 随所有请求返回。您可以通过将 `/` 更改为 `/protected`（或您正在保护的任何位置）来限制 cookie 仅用于受保护区域。
-   `ProtectedDomain` 设置 cookie 的域名。前面的点号确保 cookie 发送到同一域名中的所有 Web 主机。例如，将此设置为 `.mobilac.com` 将允许在 `web1.Mobilac.com` 或 `web2.Mobilac.com` 中查看该 cookie。您也可以通过在此处指定完全限定主机名来将 cookie 限制为单个主机。
-   `ProtectedSecure` 设置为 1 以确保 cookie 的安全性。
-   `ProtectedLoginScript` 设置登录表单的位置，该表单由模块生成。

7.  现在，您需要按照以下方式为 `/protected` 目录创建一个 `<Location>` 容器：

```
<Location /protected>
    AuthType Apache::AuthTicket
    AuthName Protected
    PerlAuthHandler Apache::AuthTicket->authenticate
    PerlAuthzHandler Apache::AuthTicket->authorize
    require valid-user
</Location>
```

在此，Apache 被要求需要有效的用户凭证，这些凭证将由 `Apache::AuthTicket` 模块进行身份验证。

8.  现在，您需要按照以下方式为模块的登录屏幕、登录脚本和注销功能设置处理程序：

```
<Location /protectedloginform>
    AuthType Apache::AuthTicket
    AuthName Protected
    SetHandler perl-script
    PerlHandler Apache::AuthTicket->login_screen
</Location>

<Location /protectedlogin>
    AuthType Apache::AuthTicket
    AuthName Protected
    SetHandler perl-script
    PerlHandler Apache::AuthTicket->login
</Location>

<Location /protected/logout>
    AuthType Apache::AuthTicket
    AuthName Protected
    SetHandler perl-script
    PerlHandler Apache::AuthTicket->logout
</Location>
```

9.  创建上述配置后，请确保您已至少向 `wwwusers` 表添加了一个用户。有关如何在数据库中管理用户的详细信息，请参阅本章前面“在任意 RDBM 中管理用户和组”部分。

10. 使用 `/usr/local/apache/bin/apachectl restart` 命令重启 Apache Web 服务器。

11. 为确保看到 cookie，请将 Web 浏览器设置为提示接收 cookie。对于 Netscape Navigator，您可以使用“编辑” > “偏好” > “高级” > “Cookie” 选项勾选“在存储 cookie 前警告我”。对于 Microsoft IE，您必须使用“工具” > “Internet 选项” > “安全” > “自定义级别” > “Cookie” > “提示”选项。

12. 现在访问 `http://your_server_name/protected/` 目录，您应该会看到一个要求输入用户名和密码的 Web 表单。输入一个有效用户名和一个无效密码，Web 表单应仅仅重新显示自身。现在输入一个有效的用户名/密码对，您的 Web 浏览器将询问您的许可以存储 cookie。下面显示了一个示例会话（票据）cookie：

```
Cookie Name: Apache::AuthTicket_Protected
Cookie Domain: nitec.com
Path: /
Expires: End of session
Secure: Yes
Data: expires:988390493:version:::user:kabir2:hash:bf5ac94173071cde94489ef79f24b158::time:988389593
```

13. 允许 Web 浏览器存储该 cookie，您就应该能够访问受限的 Web 部分。

14. 接下来，您应该验证 `tickets` 表中是否有新的票据。您可以登录到数据库服务器并查看 `tickets` 表的内容。例如，在运行 MySQL 服务器的 Linux 系统上，我在通过 `mysql -u httpd -p auth` 命令登录到 MySQL 后，可以运行 `select * from tickets` 命令。示例输出如下所示：

```
mysql> select * from tickets;
+--------------------------------+----------+
| ticket_hash                   | ts       |
+--------------------------------+----------+
| 145e12ad47da87791ace99036e35357d | 988393278 |
| 6e115d1679b8a78f9b0a6f92898e1cd6 | 988393401 |
+--------------------------------+----------+
2 rows in set (0.00 sec)
```

在此，MySQL 报告当前有会话连接到 Web 服务器。

15. 您可以通过删除存储在该表中的 `tickets` 来强制 Web 浏览器重新登录。例如，在数据库服务器上发出 `delete from tickets` 命令将删除 `tickets` 表中的所有记录，并强制每个人都重新登录。

# 第 8 章

# 本章内容

-   监控 Apache 状态
-   启用日志记录
-   自定义日志记录
-   归档日志
-   跟踪用户
-   分析日志文件
-   维护日志文件

## 监控对 Apache 的访问

您是否曾好奇谁在访问您的网站？或者您的 Apache 服务器在您的系统上的表现如何？监控、记录和分析 Apache 服务器可以为您提供大量信息，这些信息对于 Web 服务器的顺畅系统管理至关重要，并且还可以帮助您的网站的市场推广方面。在本章中，我将向您展示如何监控和记录 Apache 服务器上的信息，以满足您的了解需求。

除其他事项外，在本章中，我将向您展示如何：

-   快速访问 Apache 服务器配置
-   监控正在运行的 Apache 服务器的状态
-   以 CLF 和自定义格式创建日志文件
-   使用第三方应用程序分析日志文件

### 监控 Apache

Apache 允许您通过 Web 监控两种非常有价值的信息：

-   **服务器配置信息：** 这些信息是静态的，但能够快速访问运行中服务器的配置信息非常有用，当您想要了解服务器上安装了哪些模块时尤其如此。
-   **服务器状态：** 这些信息不断变化。使用 Apache 基于 Web 的服务器状态监控功能，您可以监控诸如服务器运行时间、处理的总请求数、总数据传输量、子进程状态和系统资源使用率等信息。

我将在以下各部分讨论这两种类型的信息。

### 使用 mod_info 访问配置信息

可以通过 `mod_info` 模块访问系统配置信息。该模块提供了服务器配置的综合概述，包括配置文件中所有已安装的模块和指令。该模块包含在 `mod_info.c` 文件中。默认情况下未将其编译到服务器中。您必须使用 `configure` 脚本的 `--enable-info` 选项进行编译。例如：

```
./configure --prefix=/usr/local/apache \
            --with-mpm=prefork \
            --enable-info
```

此命令配置 Apache 安装在 `/usr/local/apache` 目录，配置源代码作为预派生服务器运行，并启用 `mod_info` 模块。运行 `make` 和 `make install` 以编译并安装新构建的 Apache 服务器。

安装此模块到服务器后，您可以通过向 `httpd.conf` 文件添加以下配置来通过 Web 查看服务器配置信息：

```
<Location /server-info>
    SetHandler server-info
    Order deny,allow
    Deny from all
    Allow from 127.0.0.1 .domain.com
</Location>
```

这允许本地主机（`127.0.0.1`）和您域名下的每个主机访问服务器信息。不要忘记用您的顶级域名替换 `.domain.com`。例如，如果您的网站是 `www.nitec.com`，您需要添加：

```
Allow from 127.0.0.1 .nitec.com
```

域名前的点号允许域内的任何主机访问服务器信息。但是，如果您希望将此限制为单个名为 `sysadmin.domain.com` 的主机，请将 Allow from 行更改为：

```
Allow from 127.0.0.1 sysadmin.domain.com
```

在服务器配置并重启后，可以通过从本地主机访问 `http://localhost/server-info` 来获取服务器信息（即，在服务器本身上运行诸如 lynx 这样的 Web 浏览器）。





这将返回服务器及其所有模块的完整配置页面。如果你希望从其他位置访问它，请使用完整的服务器名称来代替 `localhost`。例如，如果你的 Web 服务器名为 `www.nitec.com`，你可以通过使用 `http://www.nitec.com/server-info` 来访问服务器信息。

`mod_info` 模块还提供了一个名为 `AddModuleInfo` 的指令，它允许你在由 `mod_info` 模块提供的模块列表中添加描述性文本。这些描述性文本可以是任何内容，包括 HTML 文本。`AddModuleInfo` 的语法如下：

```
AddModuleInfo module_name descriptive_text
```

例如：

```
AddModuleInfo mod_info.c 'See <a href="http://localhost/manual/mod/mod_info.html">man mod_info</a>'
```

这会在 `mod_info.c` 的列表旁边显示一个 HTML 链接，提供从 Apache 在线手册中快速获取该模块更多信息的途径，如下所示。

```
Module Name: mod_info.c
Content handlers: (code broken)
Configuration Phase Participation: Create Server Config, Merge Server Configs
Module Directives:
  AddModuleInfo - a module name and additional information on that module
Current Configuration:
  AddModuleInfo mod_info.c 'man mod_info'
Additional Information:
  man mod_info
```

你还可以限制屏幕上显示的信息如下：

- **仅服务器配置**。使用 `http://server/server-info?server`，这将显示以下信息：
```
Server Version: Apache/2.0.14 (Unix)
Server Built: Mar 14 2001 12:12:28
API Version: 20010224:1
Hostname/port: rhat.nitec.com:80
Timeouts: connection: 300 keep-alive: 15
MPM Information: Max Daemons: 20 Threaded: no Forked: yes
Server Root: /usr/local/apache
Config File: conf/httpd.conf
```

- **单个模块的配置**。使用 `http://server/server-info?module_name.c`。例如，要仅查看 `mod_cgi` 模块的信息，请运行 `http://server/server-info?mod_cgi.c`，这将显示以下信息：
```
Module Name: mod_cgi.c
Content handlers: (code broken)
Configuration Phase Participation: Create Server Config. Merge Server Configs
Module Directives:
  ScriptLog - the name of a log for script debugging info
  ScriptLogLength - the maximum length (in bytes) of the script debug log
  ScriptLogBuffer - the maximum size (in bytes) to record of a POST request
Current Configuration:
```

- **当前已编译模块列表**。使用 `http://server/server-info?list`，这将显示以下信息：
```
mod_cgi.c
mod_info.c
mod_asis.c
mod_autoindex.c
mod_status.c
prefork.c
mod_setenvif.c
mod_env.c
mod_alias.c
mod_userdir.c
mod_actions.c
mod_imap.c
mod_dir.c
mod_negotiation.c
mod_log_config.c
mod_mime.c
http_core.c
mod_include.c
mod_auth.c
mod_access.c
core.c
```

当然，根据你的源配置期间启用的模块不同，你的列表会有所不同。现在，让我们看看如何监控正在运行的 Apache 服务器的状态。

## 使用 mod_status 启用状态页面

`mod_status` 模块使 Apache 管理员能够通过 Web 监控服务器。它会创建一个包含服务器统计信息的 HTML 页面。它还生成另一个对程序友好的页面。这两个页面上显示的信息包括：

- 服务器系统的当前时间
- 服务器上次重启的时间
- 服务器启动并运行后经过的时间
- 迄今为止提供的总访问次数
- 迄今为止传输的总字节数
- 处理请求的子进程数量
- 空闲子进程数量
- 每个子进程的状态、该子进程执行的请求数以及该子进程提供的总字节数
- 平均值，包括每秒请求数、每秒提供字节数以及每个请求的平均字节数
- 每个子进程当前使用的 CPU 百分比以及 Apache 总共使用的百分比
- 当前正在处理的主机和请求

![](img/e11fcbd2818a3495ac70085e5d8d1c26_247_0.png)

上述部分信息只有在你使用本小节稍后介绍的 `ExtendedStatus` 指令启用此类信息显示时才可用。

与 `mod_info` 模块类似，该模块在标准 Apache 发行版中默认也不进行编译，因此你需要在 `configure` 脚本中使用 `--enable-status` 选项并编译和安装 Apache。

## 查看状态页面

在将 `mod_status` 模块编译并集成到你的 Apache 服务器后，你需要定义 Apache 应使用哪个 URL 位置来显示信息。换句话说，你需要告诉 Apache 哪个 URL 会在你的 Web 浏览器中显示服务器统计信息。

假设你的域名是 `domain.com`，并且你想使用以下 URL：

```
http://www.domain.com/server-status
```

使用 `<Location ...>` 容器，你可以告诉服务器你希望它使用在 `mod_status` 模块中找到的 `server-status` 处理程序来处理此 URL。以下配置即可完成此任务：

```
<Location /server-status>
  SetHandler server-status
  Order deny,allow
  Deny from all
  Allow from 127.0.0.1 .domain.com
</Location>
```

在这里，`SetHandler` 指令为前面提到的 URL 设置了处理程序（`server-status`）。在将配置添加到 `httpd.conf` 后，重启服务器并从浏览器访问该 URL。`<Location ...>` 容器允许你从域内的任何主机或从服务器本身访问状态信息。别忘了将 `domain.com` 更改为你的真实域名，也别忘了包含前导点。

你还可以使用 `http://server/server-status?refresh=N` URL 让状态页面自动更新，每 `N` 秒刷新一次页面。

要查看扩展状态信息，请在服务器配置上下文中添加 `ExtendedStatus On` 指令。例如，你在 `httpd.conf` 中完整的服务器状态相关配置可能如下所示：

```
ExtendedStatus On
<Location /server-status>
  SetHandler server-status
  Order deny,allow
  Deny from all
  Allow from 127.0.0.1 .domain.com
</Location>
```

扩展状态信息的示例如下：

```
Apache Server Status for rhcat.netfix.com
Server Version: Apache/2.0.14 (Unix)
Server Built: Mar 14 2001 12:12:28
────────────────────────────────────────────────────────────────────

Current Time: Thursday, 15-Mar-2001 11:05:08 PST
Restart Time: Thursday, 15-Mar-2001 11:02:40 PST
Parent Server Generation: 0
Server uptime: 2 minutes 28 seconds
Total accesses: 17807 – Total Traffic: 529 kB
CPU Usage: ul/3.4 s. 0.3 cu0 cs0 – 117% CPU load
120 requests/sec – 3660 B/second – 30 B/request
4 requests currently being processed, 8 idle servers
_WKKK_………
……

Scoreboard Key:
"W" Waiting for Connection, "S" Starting up, "R" Reading Request,
"W" Sending Reply, "K" Keepalive (read), "D" DNS Lookup,
"L" Logging, "G" Gracefully finishing, "." Open slot with no current process
```

| Srv | PID | Acc | M | CPU | SS | Req | Conn | Child | Slot | Client | Vhost | Request |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | 0 | | 0.0 | 087/87_ | 0.07 | 1726072572 | 0 | 0 | 0.0 | 0.10 | 0.10 |
| 0 | -0 | 0 | | 105/105/W | 0.00 | 1726072572 | 0 | 50.5 | 0.0 | 0.05 | (unavailable) | |
| 0 | -0 | 0 | | 166/166/K | 0.02 | 1726072572 | 0 | 233.5 | 0.23 | 0.23 | (unavailable) | |
| 0 | -0 | 0 | | 49/49/49 | K | 0.01 | 1726072572 | 0 | 25.2 | 0.02 | 0.02 |
| 0 | -0 | 0 | | 77/77/K | 0.08 | 1726072572 | 0 | 116.6 | 0.11 | 0.11 | (unavailable) | |
| 4 | -0 | 0 | | 0.10/17323_ | 173.25 | 1726072572 | 0 | 0.0 | 0.00 | 0.00 | (unavailable) | |

```
Srv  Child Server number - generation
PID  OS process ID
Acc  Number of accesses this connection / this child / this slot
M    Mode of operation
CPU  CPU usage, number of seconds
SS   Seconds since beginning of most recent request
Req  Miliseconds required to process most recent request
Conn Kilobytes transferred this connection
Child Megabytes transferred this child
Slot Total megabytes transferred this slot
Apache/2.0.14 Server at rhat.nitec.com Port 80
```

## 简化状态显示

由 `mod_status` 模块显示的状态页面提供了额外信息，使其不适合作为任何数据分析程序的数据文件使用。例如，如果你想使用电子表格程序从服务器状态数据中创建图表，你需要手动清理数据。然而，该模块提供了一種方法，通过修改 URL 使用 `?auto`（如 `http://server/server-status?auto`）来从同一 URL 创建机器可读的输出。状态输出的示例如下：

```
Total Accesses: 17855
Total kBytes: 687
CPULoad: 14.1982
Uptime: 1221
ReqPerSec: 14.6233
BytesPerSec: 576.157
BytesPerReq: 39.4001
BusyServers: 8
IdleServers: 8
Scoreboard: _KWKKKKKK.................................................................
........................................................................................
........................................................................................
........................................................................................
........................................................................................
........................................................................................
........................................................................................
........................................................................................
........................................................................................
......
```




## 存储服务器状态信息

Apache 附带一个名为 `log_server_status` 的 Perl 脚本（位于源码发行版的支持目录中），可用于定期将服务器状态信息（使用 `auto` 选项）存储在纯文本文件中。

你可以将此脚本作为 `cron` 任务运行，以按所需的时间频率获取状态信息。不过，在使用该脚本之前，你可能需要编辑脚本源代码，修改 `$where`、`$port`、`$server` 和 `$request` 变量的值。默认值如下：

```perl
$where = "/var/log/graph/"; # 日志文件将类似于 "/var/log/graph/19960312"
$server = "localhost"; # 服务器名称，可以是 "www.foo.com"
$port = "80"; # 服务器端口
$request = "/status/?auto"; # 要发送的请求
```

对于大多数站点，以下内容应该有效：

```perl
$where = "/var/log/apache/";
$server = "localhost";
$port = "80";
$request = "/server-status?auto"
```

你可能需要进行以下更改：

- 将 `$where` 的值更改为你希望存储脚本创建的文件的路径。确保该路径已经存在，或者使用 `mkdir -p pathname` 创建它。例如，`mkdir -p /var/log/apache` 将确保所有目录（`/var`、`/var/log`、`/var/log/apache`）在需要时创建。

- `$port` 变量应为你想要监控的服务器的端口号。如果你的服务器运行在标准的 `HTTP` 端口上，默认值 `80` 就可以了。

- `$server` 变量应赋值为你服务器的域名。如果脚本和服务器运行在同一个系统上，默认值 `localhost` 就可以了。然而，如果服务器位于另一台机器上，请指定完全限定域名（例如，`www.mydomain.com`）作为该值。

- `$request` 变量应设置为你在 `<Location ...>` 指令中使用的任何内容加上 `?auto` 查询字符串。

如果你不喜欢脚本使用的记录格式，你可以修改以下行以适应你的需求：

```perl
print OUT "$time:$requests:$idle:$number:$cpu\n";
```

脚本使用 `socket` 连接到 Apache 服务器来发送 URL 请求；因此，你需要确保你有 `Perl` 的 `socket` 支持。例如，在 `Linux` 系统中，`Perl socket` 代码位于 `socket.ph` 中。你可以使用 `locate socket.ph` 来确定该文件是否存在于你的系统中。

## 创建日志文件

了解服务器的状态和配置信息对于管理服务器很有帮助，但了解谁或什么正在访问你的网站也很重要，而且令人兴奋。你可以通过使用 Apache 服务器的日志记录功能来学习这些信息。以下部分讨论了日志记录是如何工作的，以及如何充分利用 Apache 日志记录模块。

随着 Web 服务器软件开始出现在市场上，许多 Web 服务器日志分析程序也开始出现。这些程序成为许多 Web 管理员日常工作和生活的一部分。伴随着这一切而来的是日志文件不兼容的时代，这使得日志分析变得困难且繁琐；单一的分析程序无法在所有日志文件上工作。随后出现了通用日志格式（CLF）规范。这使得所有 Web 服务器能够以相对相似的方式写入日志，使从一个服务器到另一个服务器的日志分析变得更加容易。

默认情况下，标准的 Apache 发行版包含一个名为 `mod_log_config` 的模块，它负责基本的日志记录，并且默认写入 CLF 日志文件。你可以使用 `LogFormat` 指令来改变这种行为。然而，CLF 涵盖了大多数环境中的日志记录需求。以下段落解释了 CLF 日志文件中每行内容的含义。

CLF 日志文件为每个请求包含单独的一行。一行由几个用空格分隔的标记组成：

```
host ident authuser date request status bytes
```

如果一个标记没有值，则它用连字符 (-) 表示。这些标记的含义如下：

- `authuser`: 如果请求的 URL 需要成功的 Basic HTTP 身份验证，则该标记的值是用户名。

- `bytes`: 返回给客户端的对象中的字节数，不包括所有 HTTP 头部。

- `date`: 请求的日期和时间。

- `host`: 客户端的完全限定域名或其 IP 地址。

- `ident`: 如果 `IdentityCheck` 指令已启用并且客户端机器运行 identd，则这是由客户端报告的身份信息。

- `request`: 客户端的请求行，用双引号 (“”) 包围。

- `status`: 返回给客户端的三位数字 HTTP 状态码。

请参阅附录 A 以获取所有 HTTP/1.1 状态码的列表。

日期字段可以具有此格式：

```
date = [day/month/year:hour:minute:second zone]
```

日期字段的大小如表 8-1 所示。

**表 8-1：日期字段大小**

| 字段 | 值 |
| --- | --- |
| 日 | 2 位数字 |
| 月 | 3 个字母 |
| 年 | 4 位数字 |
| 时 | 2 位数字 |
| 分 | 2 位数字 |
| 秒 | 2 位数字 |
| 时区 | ('+' \| '-)*digit |

以下部分介绍可以与 `mod_log_config` 一起使用的指令。该模块有四个可用的指令。

### TransferLog 指令

*TransferLog* 设置日志信息要发送到的日志文件或程序的名称。默认情况下，日志信息采用 CLF 格式。可以使用 *LogFormat* 指令定制此格式。请注意，当 *TransferLog* 指令位于虚拟主机容器内时，日志信息将使用在该上下文中找到的最后一个 *LogFormat* 指令进行格式化。然而，如果在同一上下文中未找到 *LogFormat* 指令，则使用服务器的日志格式。

**语法:** *TransferLog* *filename* | "*"*path_to_external/program*"*

**默认设置:** 无

**上下文:** *server* config, *virtual* host

*TransferLog* 指令接受日志文件路径或指向*外部*程序的*管道*作为参数。如果找不到前导 / 字符，则假定日志 *filename* 相对于 *ServerRoot* 设置。例如，如果 *ServerRoot* 设置为 `/etc/httpd`，则以下命令告诉 Apache 将日志信息发送到 `/etc/httpd/logs/access.log` 文件：

```
TransferLog logs/access.log
```

当参数是到外部程序的管道时，日志信息被发送到外部程序的标准输入 (STDIN)。

**注意**

如果 VirtualHost 从主服务器继承 `TransferLog`，则不会为其启动新程序。如果使用程序，则它将在启动 httpd 的用户下运行。如果服务器是由 root 启动的，则这是 root。务必确保程序是安全的。

### LogFormat 指令

LogFormat 设置由 `TransferLog` 指令指定的默认日志文件的格式。如果你在指令行中为格式包含一个昵称，你可以在其他 `LogFormat` 和 `CustomLog` 指令中使用它，而不是重复整个格式字符串。定义昵称的 `LogFormat` 指令没有其他作用；也就是说，它仅定义昵称，并不实际应用该格式。

**语法:** LogFormat `format` [nickname]

**默认设置:** LogFormat "%h %l %u %t "%r" %>s %b"

**上下文:** Server config, virtual host

有关可用的格式选项的详细信息，请参阅本章后面“自定义你的日志文件”部分。

### CustomLog 指令

与 `TransferLog` 指令类似，此指令允许你将日志信息发送到日志文件或外部程序。然而，与 `TransferLog` 指令不同的是，它允许你使用可以作为参数指定的自定义日志格式。

**语法:** CustomLog `file` | `pipe` [format | nickname] [env=[!]environment_variable]

**默认设置:** None

**上下文:** Server config, virtual host

例如，在下面的例子中，访问日志文件中的每一行都将使用给定的格式说明符写入。格式指定了日志文件每一行的格式：

```
CustomLog logs/access.log "%h %l %u %t \"%r\" %>s %b"
```

可用于格式的选项与 `LogFormat` 指令的参数完全相同。如果格式包含空格（在几乎所有情况下都会包含），则应将其包围在双引号中。代替实际的格式字符串，你可以使用由 `LogFormat` 指令定义的格式昵称。例如：

```
LogFormat "%h %t \"%r\" %>s" myrecfmt
CustomLog logs/access.log myrecfmt
```




此处 `access.log` 将包含 `myrcfmt` 格式的行。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_254_0.png)

> `TransferLog` 和 `CustomLog` 指令可以在每个服务器中多次使用，以便将每个请求记录到多个文件中。例如：
> CustomLog logs/access1.log common
> CustomLog logs/access2.log common
>
> 此处，服务器将为每个请求创建两个日志条目，并将每个条目分别存储在 `access1.log` 和 `access2.log` 中。除非你在每个日志中使用不同的格式，并且因为不同的原因需要每种格式，否则这真的没什么用。

最后，如果你使用 `mod_setenvif`（默认已安装）或 URL 重写模块（`mod_rewrite`，默认未安装）根据请求的 URL 设置环境变量，你可以使用 `CustomLog` 指令的 `env=[!]environment_variable` 选项来创建条件日志记录。例如，假设你允许用户下载 PDF 白皮书，并希望将所有章节记录到名为 `whitepaper.log` 的日志文件中，该文件位于你常用的日志目录中。以下是必要的配置：

```
SetEnvif Request_URI \.pdf$ whitepaper
CustomLog logs/whitepaper.log common env=whitepaper
CustomLog logs/access.log common env=!whitepaper
```

第一行设置环境变量 `whitepaper`，每当请求的 URL 以 .pdf 扩展名结尾时。然后，当需要记录日志条目时，Apache 使用第一个 `CommonLog` 指令的 `env=whitepaper` 设置来确定它是否已设置。如果已设置，则使用通用格式将日志条目写入 `logs/whitepaper.log` 文件。当未设置 `whitepaper` 环境变量时，日志条目将像往常一样写入 `logs/access.log` 文件。

## CookieLog 指令

`CookieLog` 允许你在相对于 `ServerRoot` 指令所指路径的文件中记录 cookie 信息。不建议使用此指令，因为它在 Apache 中可能不会长期得到支持。要记录 cookie 数据，请改用用户跟踪模块（`mod_usertrack`）。用户跟踪模块将在本章稍后讨论。

语法：`CookieLog filename`

默认设置：无

上下文：服务器配置，虚拟主机

### 自定义日志文件

虽然默认的 CLF 格式满足大多数日志需求，但有时自定义日志数据是有用的。例如，你可能希望记录访问你网站浏览器类型，以便你的 Web 设计团队确定应避免或使用哪种浏览器特定的 HTML。或者，也许你想知道哪些网站正在（即推荐）访客访问你的网站。这在 Apache 中非常容易实现。默认日志记录模块 `mod_log_config` 支持自定义日志记录。

自定义格式通过该模块的 `LogFormat` 和 `CustomLog` 指令设置。`string` 是 `LogFormat` 和 `CustomLog` 的格式参数。此格式字符串可以包含字面字符和特殊的 `%` 格式说明符。当在此字符串中使用字面值时，它们会针对每个请求复制到日志文件中。然而，`%` 说明符将被替换为相应的值。特殊的 `%` 说明符如表 8-2 所示。

表 8-2
**日志条目的特殊 % 说明符**

| % 说明符 | 描述 |
| :--- | :--- |
| %a | 客户端 IP 地址 |
| %A | 服务器 IP 地址 |
| %B | 发送的字节数，不包括 HTTP 头；未发送字节时为 0 |
| %b | 发送的字节数，不包括 HTTP 头；未发送字节时为 \"-\" |
| %C | 响应完成时的连接状态。如果响应完成前客户端中止了连接，则写入 \"X\" 字符。如果客户端使用 keep-alive 协议，则写入 \"+\" 以显示响应后连接保持激活直至超时。写入 \"-\" 以表示响应后连接已关闭 |
| %[mycookie]C | 名为 `mycookie` 的 cookie 的内容 |
| %D | 完成响应所花费的时间（微秒） |
| %[myenv]e | 名为 `myenv` 的环境变量的内容 |
| %f | 请求的文件名 |
| %h | 发起请求的远程主机 |
| %H | 请求协议（例如，HTTP 1/1） |
| %[IncomingHeader]i | IncomingHeader 的内容；即发送到服务器的请求中的头部行。末尾的 i 字符表示这是客户端（传入）头部 |
| %I | 如果启用了 `IdentityCheck` 指令且客户机运行 identd，则这是客户端报告的身份信息 |
| %m | 请求方法（GET、POST、PUT 等） |
| %i[ModuleNote] | 来自其他模块的注释 ModuleNote 的内容 |
| %i[OutgoingHeader] | OutgoingHeader 的内容；即回复中的头部行。末尾的 `o` 字符表示这是服务器（传出）头部 |
| %p | 请求服务的端口 |
| %P | 服务请求的子进程 ID |
| %q | 查询字符串 |
| %r | 请求的第一行 |
| %s | 服务器响应请求时返回的状态。请注意，当请求被重定向时，此格式说明符的值仍然是原始请求状态。如果你想存储重定向请求的状态，请使用 `%>s` 代替 |
| %t | 请求时间。时间格式与 CLF 格式相同 |
| %i[format]t | 由 format 指定的格式的时间。（你也可以查看 Unix 系统上 strftime 的手册页。） |
| %T | 处理请求所花费的时间，单位为秒 |
| %u | 如果请求的 URL 需要成功的 Basic HTTP 身份验证，则用户名是该格式说明符的值。如果身份验证尝试后服务器返回 401 状态（需要身份验证），则值可能是虚假的 |
| %U | 请求的 URL 路径 |
| %v | 接收请求的服务器或虚拟主机的名称 |
| %V | 根据 UseCanonicalName 指令指定的服务器名称 |

有可能在先前每个说明符中包含条件信息。这些条件可以是某些 HTTP 状态码的存在（或不存在）。例如，假设你想记录所有将用户指向不存在页面的推荐 URL。在这种情况下，服务器会产生一个 404 状态（未找到）头部。因此，要记录推荐 URL，你可以使用以下格式说明符：

```
'%404[Referer]'
```

类似地，要记录导致异常状态的推荐 URL，你可以使用：

```
'%|200,304,302|Referer|i'
```

请注意使用 ! 字符来表示服务器状态列表的不存在。

类似地，要在 CLF 格式说明符的末尾包含额外信息，你可以扩展 CLF 格式，该格式由以下格式字符串定义：

```
"%h %l %u %t "%r"" %s %b"
```

例如：

```
"%h %l %u %t "%r" %s %b "%{Referer}i|" "%{User-agent}i"".
```

此格式说明记录了 CLF 格式数据，并在每个日志条目中添加了在客户端提供的头部中发现的 Referrer 和 User-agent 信息。

你学习了如何向日志文件添加自定义字段，但如果你需要将此数据存储到多个日志文件中怎么办？下一节讨论如何使用多个日志文件。

### 创建多个日志文件

有时，有必要创建多个日志文件。例如，如果你使用的日志分析程序无法处理非 CLF 数据，你可能希望将非 CLF 数据写入不同的文件。使用 *mod_log_config* 模块的 *TransferLog* 和/或 *CustomLog* 指令可以很容易地创建多个日志文件。只需重复这些指令以创建一个以上的日志文件。

例如，如果你想创建一个标准的 CLF 访问日志和一个所有推荐 URL 的自定义日志，你可以使用类似以下内容：

```
TransferLog logs/access_log
CustomLog   logs/referer_1og          "%{Referer}i"
```

如果在主要服务器配置中定义了 *TransferLog* 或 *CustomLog*，并且定义了虚拟主机，则与虚拟主机相关的日志记录也会在这些日志中执行。例如：

```
TransferLog logs/access_log
CustomLog   logs/agent_1og         "%{User-agent}i"

<Virtual Host 206.171.50.51>
```





ServerName reboot.nitec.com
DocumentRoot  "/www/reboot/public/htdocs"
ScriptAlias "/cgi-bin/" "/www/reboot/public/cgi-bin/"
</VirtualHost>

这里，虚拟主机 *reboot.nitec.com* 在虚拟主机容器标签内没有定义 *TransferLog* 或 *CustomLog* 指令。所有日志信息将存储在 *logs/access_log* 文件中。如果你在日志页面看到虚拟主机 *reboot.nitec.com* 的所有日志都记录在 *vhost_logs/reboot_access_log* 文件中，那么 *logs/access_log* 和 *logs/agents_log* 文件将不会用于名为 *reboot.nitec.com* 的虚拟主机。

TransferLog vhost_logs/reboot_access_log

## 记录 Cookie

到目前为止，讨论的日志选项无法唯一地识别访问者。唯一地识别访问者非常重要，因为如果你知道每个访问者发出的请求，你就能更好地了解你的内容是如何被使用的。例如，假设你的网站上有一个非常酷页面，并且你有办法在日志中识别访问者。如果你查看日志页面，发现许多访问者必须从一页跳到另一页才能找到最后那个酷页面，你可能会重新考虑站点设计，让那个酷页面在点击流中更早出现。Apache 有一个名为 *mod_usertrack* 的模块，它允许你通过记录 HTTP cookie 来跟踪你的网站访问者。

### HTTP Cookie……没有巧克力豆

HTTP cookie 不是由饼干面团制成的。它只是服务器提供给 Web 浏览器的一小段信息。这些信息通常存储在键=值对中，可以与整个网站或网站上的特定 URL 相关联。Cookie 由服务器发出并被 Web 浏览器接受后，该 cookie 将驻留在 Web 浏览器系统中。每次 Web 浏览器请求相同的 URL，或任何属于该 cookie URL 范围的 URL 时，cookie 信息都会返回给服务器。在设置 cookie 时，服务器可以告知 Web 浏览器在特定时间后使该 cookie 过期。时间可以指定为 cookie 在后续会话中永不被使用，或者可以使用很长一段时间。

关于 cookie 的使用存在很多争议。许多人认为 cookie 是对隐私的侵犯。使用 cookie 来跟踪用户行为非常流行。事实上，互联网上的几家广告公司大量使用 cookie 来跟踪用户。需要强调的是，cookie 本身不会造成任何伤害。

Cookie 数据通常以文本文件的形式写入你的浏览器软件的目录中。例如，使用标准日志模块中的 `CustomLog` 指令，你可以将 cookie 存储在一个单独的文件中：

CustomLog logs/clickstream "%{cookie}C %r %t"

现在，让我们来看看新的 `mod_usertrack` 模块。

请记住，`mod_usertrack` 并不保存 cookie 的日志；它只是为每个访问者生成唯一的 cookie。你可以使用 `CustomLog`（如前所述）将这些 cookie 存储在日志文件中以供分析。

`mod_usertrack` 指令并未编译到 Apache 的标准发行版中，因此你需要在使用该选项之前使用 `--enable-usertrack` 选项进行编译。该模块提供了以下各节中讨论的指令。

### **CookieExpires 指令**

该指令用于设置由模块生成的 cookie 的过期时间。过期时间可以定义为秒数，或者定义为如“1 month 2 days 3 hours”这样的格式。

**语法：** `CookieExpires expiry-period`

**上下文：** 服务器配置，虚拟主机

在以下示例中，第一个指令以秒为单位定义过期时间，第二个指令使用特殊格式定义过期时间。请注意，当过期时间未以数字形式定义时，将假设使用特殊格式。但是，特殊格式要求你用双引号将格式字符串括起来。如果未使用此指令，cookie 仅持续当前浏览器会话。

CookieExpires  3600
CookieExpires  "2 days 3 hours"

### **CookieTracking 指令**

该指令启用或禁用自动 cookie 的生成。当设置为 on 时，Apache 开始为所有新请求发送用户跟踪 cookie。该指令可用于按服务器或按目录基础开启或关闭此行为。默认情况下，编译 `mod_usertrack` 不会激活 cookie。

**语法：** `CookieTracking On | Off`

**上下文：** 服务器配置，虚拟主机，目录，按目录访问控制文件（`.htaccess`）

**重写：** `FileInfo`

## 使用错误日志

本章讨论了记录每个 Web 事务的请求和响应阶段各种有趣数据的几种方法。你收集关于访问者的数据越多，你的营销部门就会越高兴。然而，作为系统管理员，如果一切运行顺利你会很高兴。Apache 通过编写错误日志来让你知道哪里出了问题。如果不记录错误，你无法确定出了什么问题以及错误发生在哪里。毫不奇怪，错误日志记录是在核心 Apache 中支持的，而不是在像 `mod_log_config` 这样的模块中支持的。

`ErrorLog` 指令使你可以记录 Apache 遇到的所有错误。本节探讨如何将 Apache 错误日志整合到几乎所有 Unix 平台上广泛使用的 `syslog` 设施中。

`Syslog` 是记录由守护进程（服务器）进程发送的消息的传统方式。你可能会问：“Apache 是一个守护进程，为什么它不能写入 syslog？”实际上它可以。你所需要做的就是在配置文件中用以下内容替换现有的 `ErrorLog` 指令：

ErrorLog syslog

然后重启 Apache。使用 Web 浏览器访问你的 Web 服务器上的一个不存在的页面，并监视 `syslog` 日志文件，查看是否显示了 httpd 条目。你应该查看你的 `/etc/syslog.conf` 文件，以了解 httpd 消息将出现的位置。

例如，列表 8-1 显示了 Linux 系统的 `/etc/syslog.conf`。

### 列表 8-1: /etc/syslog.conf

# Log all kernel messages to the console.
# Logging much else clutters up the screen.
*kern.*				/dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none		/var/log/messages

# The authpriv file has restricted access.
authpriv.*			/var/log/secure

# Log all the mail messages in one place.
mail.*				/var/log/maillog

# Everybody gets emergency messages, plus log
# them on another machine.
*.emerg				*

# Save mail and news errors of level err and higher in a
# special file.
uucp,news.crit				/var/log/spooler

# Save boot messages also to boot.log
local7,local0,local1,local2,local3,local4,local5,local6,local7.*
				/var/log/boot.log

就 Apache 而言，此列表中有两行很重要，我在上面用**粗体**标出了它们。

第一行（以 `*,info;mail.none;` 开头）告诉 *syslog* 将所有信息类型的消息（除邮件和私有认证外）写入 `/var/log/messages` 文件，第二行（以 `*,emerg` 开头）规定所有紧急消息应写入所有日志文件。使用 `LogLevel` 指令，你可以指定 Apache 应发送给 *syslog* 的消息类型。例如：

ErrorLog syslog
LogLevel debug

这里，Apache 被指示将调试消息发送给 *syslog*。如果你希望通过 *syslog* 将调试消息存储在不同的文件中，则需要修改 `/etc/syslog.conf`。例如：

*.debug					/var/log/debug

在 `/etc/syslog.conf` 中添加这一行，并重启 *syslogd*（`kill -HUP syslogd_PID`）和 Apache，就可以将所有 Apache 调试消息存储到 `/var/log/debug` 文件中。有几种日志级别设置：

- **Alert：** 警报消息
- **Crit：** 严重消息
- **Debug：** 以调试级别记录的消息还包括生成该消息的源文件和行号，以帮助调试和代码开发
- **Emerg：** 紧急消息
- **Error：** 错误消息
- **Info：** 信息消息
- **Notice：** 通知消息
- **Warn：** 警告




**提示**
如果你想实时查看 `syslog` 或其他日志文件的更新，可以使用大多数 Unix 系统上常见的 `tail` 实用工具。例如，如果你想实时查看名为 `/var/log/messages` 的日志的更新，请使用：
`tail -f /var/log/messages`

# 分析你的日志文件

到目前为止，你已经学会了如何创建基于标准 CLF 的日志和自定义日志。现在，你需要一种方法来分析这些日志，以便利用记录的数据。你的日志分析需求可能各不相同。有时你可能需要生成详细的报告，或者你可能只是想对日志进行简单的检查。对于简单的任务，最好使用手头现有的工具。大多数 Unix 系统都有足够的实用工具和脚本工具来完成这项工作。

使用 Unix 实用工具，你可以快速获取所需信息；然而，这种方法需要一些 Unix 知识，而且并不总是方便的，因为你的老板可能想要一份“漂亮”的报告，而不是枯燥的文本列表。在这种情况下，你可以开发自己的分析程序，或使用第三方分析工具。

让我们使用一个 Unix 实用工具来获取所有主机的列表。如果你使用默认日志记录功能或支持 CLF 的自定义日志，你可以轻松找到所有主机的列表。例如：
`cat /path/to/httpd/access_log | awk '{print $1}'`
这会打印出所有主机的 IP 地址（如果你启用了 DNS [域名服务器] 查找，则会显示主机别名）。`cat` 实用工具列出 `access_log` 文件，生成的输出通过管道传递给 `awk` 解释器，后者使用 `print` 语句只打印每行的第一个字段。这会打印所有主机；但如果你想要排除你网络中的主机呢？在这种情况下，你可以使用：

```
cat /path/to/httpd/access_log | awk '{print $1}' | egrep -v '^206.171.50.*'
```

其中 `206.171.50` 应替换为你的网络地址。在这里，我假设你使用的是 C 类网络。如果你使用的是 B 类网络，你只需要使用 IP 地址的前两个八位组。此版本允许你使用 `egrep` 实用工具排除你自己的主机，该工具被指示（通过 `-v`）仅显示不以 `206.171.50` 网络地址开头的主机。然而，这可能仍然不够令人满意，因为很可能存在重复项。因此，最终版本是：
`cat /path/to/httpd/access_log | awk '{print $1}' | uniq | egrep -v '^206.171.50.*'`

在这里，`uniq` 实用工具过滤掉重复项，每个主机只显示一条记录。当然，如果你想要查看访问你的 Web 站点的唯一主机总数，你可以将最终结果传递给带有 -l 选项的 `wc` 实用工具，如下所示：

```
cat /path/to/httpd/access_log | awk '{print $1}' | \
uniq | egrep -v '^206.171.50.*' | wc -l
```

这给出了总行数（即唯一主机访问的数量）。

有许多可用的第三方 Web 服务器日志分析工具。其中大多数工具期望日志文件为 CLF 格式，因此请确保你的日志中使用了 CLF 格式。表 8-3 列出了一些此类工具及其获取方式。

表 8-3：**第三方日志分析工具**

| **产品名称** | **产品 URL** |
|---|---|
| WebTrends | www.webtrends.com/ |
| Usage | www.bouteil.com/usage/ |
| wwwstat | www.lcs.uc.edu/pub/websoft/wwwstat/ |
| Analog | www.statslab.cam.ac.uk/~sret1/analog/ |
| http-analyze | www.netstore.de/Supply/http-analyze/ |
| Pwebstats | www.unimelb.edu.au/pwebstats.html |
| WebStat Explorer | www.webstat.com/ |
| AccessWatch | http://netpresence.com/accesswatch/ |

了解哪个工具适合你的最好方法是尝试所有这些工具，或者至少访问它们的网站，以便你可以比较它们的功能。我发现非常有用的两个实用工具是 Usage 和 wwwstat。

Usage 是我最喜欢的商业日志分析应用程序。它具有高度可配置性，并使用该公司著名的 GD 图形库生成出色的图形报告。Usage 以二进制格式分发。许多 Unix 和 Windows 平台都免费提供 Usage 的评估副本。

**wwwstat** 是我偏爱的自由软件分析程序之一。它用 Perl 编写，因此你需要在运行此应用程序的系统上安装 Perl。**wwwstat** 的输出摘要可以被 `gwstat` 读取，以生成汇总统计的精美图表。

在 Apache 中创建日志既简单又有用。创建日志使你能更多地了解你的 Apache 服务器的运行情况。日志可以帮助你检测和识别站点的问题，了解站点最佳功能等。如此有益的东西难道没有代价吗？如果你说没有，那你就猜错了。日志文件占用大量宝贵的磁盘空间，因此必须定期维护。

# 日志维护

通过启用日志记录，你可能会节省大量工作，但日志本身也会增加一些额外的工作：它们需要维护。在具有高访问率或许多虚拟域名的 Apache 站点上，日志文件可能在很短的时间内变得巨大，这很容易导致磁盘危机。当日志文件变得非常大时，你应该轮转它们。

你有两个选项来轮转日志：你可以使用 Apache 自带的名为 *rotatelog* 的实用工具，或者使用 *logrotate*，这是大多数 Linux 系统上可用的功能。

## 使用 rotatelog

Apache 附带一个名为 *rotatelog* 的支持实用工具。你可以如下使用此程序：

```
TransferLog "| /path/to/rotatelog logfile rotation_time_in_seconds"
```

例如，如果你想每 86,400 秒（即 24 小时）轮转一次访问日志，请使用以下行：

```
TransferLog "| /path/to/rotatelog /var/logs/httpd 86400"
```

每天的访问日志信息将存储在一个名为 /var/logs/httpd.nnnn 的文件中，其中 *nnnn* 代表一个长数字。

## 使用 logrotate

*logrotate* 实用工具可以轮转、压缩并通过电子邮件发送日志文件。它旨在简化日志文件的系统管理。它可以根据每日、每周、每月或大小基准自动轮转、压缩、删除并通过电子邮件发送日志文件。通常，*logrotate* 作为每日 *cron* 作业运行。阅读 *logrotate* 的 *man* 手册页以了解更多信息。

如果你的系统支持 *logrotate* 功能，你应该创建一个名为 /etc/logrotate.d/apache 的脚本，如清单 8-2 所示。

清单 8-2: /etc/logrotate.d/apache

```
# 请注意，此脚本基于以下假设：
#
# a. 你已将 Apache 安装在 /usr/local/apache
# b. 你的日志路径是 /usr/local/apache/logs
# c. 你的访问日志名为 access_log（Apache 中的默认值）
# d. 你的错误日志名为 error_log（Apache 中的默认值）
# e. Apache 的 PID 文件 httpd.pid 存储在日志
# 目录中（Apache 中的默认值）
#
# 如果上述任何假设错误，请相应地修改
# 路径或文件名。
#
/usr/local/apache/logs/access_log {

missingok

compress
rotate 5
mail webmaster@yourdomain.com
errors webmaster@yourdomain.com
size=10240K

postrotate

/bin/kill -HUP `cat /usr/local/apache/logs/httpd.pid 2>/dev/null` 2>/dev/null || true
endscript

}

/usr/local/apache/logs/error_log {

missingok

compress
rotate 5
mail webmaster@yourdomain.com
errors webmaster@yourdomain.com
size=10240K

postrotate

/bin/kill -HUP `cat /usr/local/apache/logs/httpd.pid 2>/dev/null` 2>/dev/null || true
endscript

}
```

此配置指定，每当 Apache 访问日志和错误日志文件的大小超过 10MB（10,240K）时，都要对其进行轮转，并且旧的日志文件在经过五次轮转后会被压缩并通过电子邮件发送给 webmaster@yourdomain.com，而不是被删除。在处理日志文件期间发生的任何错误都会通过电子邮件发送给 root@yourdomain.com。

## 使用 logresolve

出于性能原因，你应该通过将 HostNameLookups 指令设置为 off 来禁用主机名查找。这意味着你的日志条目将显示远程客户端的 IP 地址而不是主机名。在分析日志时，拥有主机名有助于你轻松确定谁从哪里来。例如，以下是我的 /usr/local/apache/logs/access_log 文件中的几个示例日志条目。

```
207.183.233.19 - - [15/Mar/2001:13:05:01 -0800] "GET /book/images/back.gif HTTP/1.1" 304 0
207.183.233.20 - - [15/Mar/2001:14:45:02 -0800] "GET /book/images/forward.gif HTTP/1.1" 304 0
207.183.233.21 - - [15/Mar/2001:15:30:03 -0800] "GET /book/images/top.gif HTTP/1.1" 304 0
```

如果你开启了 HostNameLookups，Apache 会将客户端 IP 地址 207.183.233.19、207.183.233.20 和 207.183.233.21 解析为相应的主机名；并且如果你保留默认的 LogFormat，如下所示：

```
LogFormat "%h %l %u %t \"%r\" %>s %b" common
```

并且在记录日志时使用通用格式 CustomLog logs/access_log common，这些示例日志条目将如下所示：

```
nano.nitcc.com - - [15/Mar/2001:13:05:01 -0800] "GET /book/images/back.gif HTTP/1.1" 304 0
rhat.nitcc.com - - [15/Mar/2001:14:45:02 -0800] "GET /book/images/forward.gif HTTP/1.1" 304 0
r2d2.nitcc.com - - [15/Mar/2001:15:30:03 -0800] "GET /book/images/top.gif HTTP/1.1" 304 0
```

由于开启 DNS 查找会导致 Apache 服务器花费更多时间来完成响应，因此广泛建议通过单独使用 logresolve 实用工具来进行主机名查找，该实用工具位于你的 Apache bin 目录中 (/usr/local/apache/bin)。清单 8-3 中显示的 log_resolver.sh 脚本可以运行此实用工具。

清单 8-3: log_resolver.sh

```
#!/bin/sh

# 请根据你的路径修改以下路径名称
```




# 您的 Apache 安装

# 日志解析器工具的完全限定路径名 (FQPN)
LOGRESOLVER=/usr/local/apache/bin/logresolve

# 由该工具生成的统计文件
STATFILE=/tmp/log_stats.txt

# 您的 Apache 日志文件
LOGFILE=/usr/local/apache/logs/access_log

# 已解析 IP 地址的新日志文件
OUTFILE=/usr/local/apache/logs/access_log.resolved

# 运行该命令
$LOGRESOLVER -s $STATFILE < $LOGFILE > $OUTFILE

exit 0;

当从命令行或作为 *cron* 任务运行此脚本时，它将创建一个名为 /usr/local/apache/logs/access_log.resolved 的文件，该文件将所有 IP 地址解析为其相应的主机名。此外，该脚本还会生成一个名为 /tmp/log_stats.txt 的统计文件，其中显示了您的缓存使用情况信息、已解析的 IP 地址总数以及解析器工具报告的其他信息。此类统计文件的示例如下所示：

```
logresolve Statistics:
Entries: 3
With name     : 0
Resolves      : 3
Cache hits    : 0
Cache size    : 3
Cache buckets :       IP number * hostname
130   207.183.233.19 -  nano.nitec.com
131   207.183.233.20 -  rhat.nitec.com
132   207.183.233.21 -  r2d2.nitec.com
```

请注意，由于该工具解析的所有三个 IP 地址（对应于上面示例日志条目）都是唯一的，因此该工具无法利用缓存。然而，如果您的日志文件包含来自同一主机的 IP 地址，缓存将被用于解析它们，而不是盲目地发起 DNS 请求。

如果您认为可以使用此脚本，我建议您将其作为 *cron* 任务运行。例如，在我运行在 Linux 上的 Apache Web 服务器上，我只是将脚本添加到 /etc/cron.daily，以每天创建日志的已解析版本。

## 重写您的 URL

URL 将访客带到您的网站。作为 Apache 管理员，您需要确保指向您网站的所有可能 URL 都是功能正常的。你要怎么做？您需要持续监控服务器错误日志中的损坏 URL 请求。如果您看到以 404 Not Found 状态码返回的请求，是时候调查这些 URL 了。通常，当 HTML 文档作者升级网站时，他们会忘记重命名现有目录可能会导致许多访客收藏的 URL 失效。

作为管理员，您如何解决此类问题？好消息是，有一个名为 `mod_rewrite` 的模块可以解决这些问题，并允许您使用 URL 重写规则创建非常有趣的解决方案。本章讨论该模块，并提供 URL 重写的实用示例。

### Apache 的 URL 重写引擎

当 Apache 接收到 URL 请求时，它会通过将文件传输给客户端（Web 浏览器）来处理该请求。如果您想介入此过程以将 URL 映射到不同的文件甚至不同的 URL 该怎么办？这就是 `mod_rewrite` 显示其价值的地方。它为您提供了一种灵活的机制，使用自定义 URL 重写规则将请求的 URL 重写为新的 URL。URL 重写规则的形式如下：

```
regex_pattern_to_be_matched
regex_substitution_pattern
```

# 本章内容

-   * 使用 Apache 的 URL 重写引擎
-   * 理解 URL 布局
-   * 处理内容
-   * 限制访问

然而，也可以向规则添加条件（例如更多的 *regex_patterns_to_be_matched*），使得只有当满足条件时才应用替换。Apache 可以将替换后的 URL 作为内部子请求处理，或者作为外部重定向发送回 Web 浏览器。图 9-1 展示了一个请求示例以及 `mod_rewrite` 规则的结果。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_270_0.png)

该图显示了向 Apache 服务器发起的对 `http://blackhole.nitec.com/~kibir` 的请求。服务器接收该请求，并在处理请求的 URL 转换阶段将其传递给 `mod_rewrite` 模块。`mod_rewrite` 模块应用由名为 *RewriteRule* 的指令定义的重写规则。在这个特定示例中，规则指出，如果发现诸如 `/~([^{\}])/?(.*)` 这样的模式，应将其替换为 `/users/$1/$2`。由于规则中包含重定向 `[R]` 标志，因此还应将外部 URL 重定向响应发送回 Web 浏览器。输出显示重定向位置为 `http://blackhole.nitec.com/users/kibir`。

如您所见，这种类型的重定向在许多情况下都非常有用。让我们看看赋予您重写 URL 能力的指令。您还应该熟悉表 9-1 中显示的服务器变量，它们可用于许多重写规则和条件。

### 表 9-1：服务器变量

| 服务器变量 | 说明 |
| :--- | :--- |
| SERVER_NAME | Web 服务器的主机名 |
| SERVER_ADMIN | Web 服务器管理员的电子邮件地址 |
| SERVER_PORT | Web 端口的端口地址 |
| SERVER_PROTOCOL | Web 服务器正在使用的 HTTP 协议版本 |
| SERVER_SOFTWARE | Web 服务器供应商的名称 |
| SERVER_VERSION | Web 服务器软件的版本 |
| DOCUMENT_ROOT | 网站的顶级文档目录 |
| HTTP_ACCEPT | Web 客户端可接受的 MIME 类型 |
| HTTP_COOKIE | 从 Web 客户端接收的 Cookie |
| HTTP_FORWARDED | 转发 URL |
| HTTP_HOST | Web 服务器的主机名 |
| HTTP_PROXY_CONNECTION | HTTP 代理连接信息 |
| HTTP_REFERER | 指向当前 URL 的引用 URL |
| HTTP_USER_AGENT | 关于 Web 客户端的信息 |
| REMOTE_ADDR | Web 客户端的 IP 地址 |
| REMOTE_HOST | Web 客户端的主机名 |
| REMOTE_USER | 经过身份验证的用户的用户名 |
| REMOTE_IDENT | 关于远程用户身份的信息 |
| REQUEST_METHOD | 用于请求当前 URL 的 HTTP 请求方法 |
| SCRIPT_FILENAME | 请求脚本文件的物理路径 |
| PATH_INFO | 请求 URL 的路径 |
| QUERY_STRING | 随请求 URL 一起发送的查询数据 |
| AUTH_TYPE | 使用的身份验证类型 |
| REQUEST_URI | 请求的 URL |
| REQUEST_FILENAME | 与 SCRIPT_FILENAME 相同 |
| THE_REQUEST | 请求的 URL |
| TIME_YEAR | 当前年份 |
| TIME_MON | 当前月份 |
| TIME_DAY | 当前日期 |
| TIME_HOUR | 当前小时 |
| TIME_MIN | 当前分钟 |
| TIME_SEC | 当前秒 |
| TIME_WDAY | 当前星期 |
| TIME | 当前时间 |
| API_VERSION | 使用的 API 版本 |
| IS_SUBREQ | 如果请求是子请求，则设置 |

### RewriteEngine

该指令为您提供 `mod_rewrite` 模块中 URL 重写引擎的开关。默认情况下，所有重写都是关闭的。要使用重写引擎，您必须通过将该指令设置为 `on` 来打开引擎。

**语法**：`RewriteEngine On | Off`

**默认值**：`RewriteEngine Off`

**上下文**：服务器配置，虚拟主机，每目录访问控制文件 (`.htaccess`)

当在每目录配置文件 (`.htaccess`) 中启用 URL 重写时，您必须在该每目录配置文件中启用（即将其设置为 `On`）此指令，并确保您已为该目录在适当上下文中启用了以下指令：

`Options FollowSymLinks`

换句话说，如果该目录属于虚拟主机站点，请确保在适当的虚拟主机容器内启用了此选项。同样，如果相关目录是主服务器 Web 文档空间的一部分，请确保在主服务器配置中启用了此选项。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_272_0.png)

在每目录配置中启用重写规则可能会降低您的 Apache 服务器性能。这是因为 `mod_rewrite` 采用一种技巧来支持每目录重写规则，而这种技巧涉及增加服务器的处理负载。因此，只要可能，您应避免在每目录配置文件中重写规则。

### RewriteOptions

该指令使您可以指定用于更改重写引擎行为的选项。目前，唯一可用的选项是 `Inherit`。通过将该指令设置为 `Inherit` 选项，您可以强制下级配置继承上级配置。

**语法**：`RewriteOptions option1 option2 [...]`

**默认值**：无

**上下文**：服务器配置，虚拟主机，每目录访问控制文件 (`.htaccess`)

例如，如果您在主服务器配置区域设置此指令，配置文件中定义的虚拟主机将继承所有重写配置，例如重写规则、条件、映射等。

同样，当此指令在每目录配置文件 (`.htaccess`) 中设置时，它将继承父目录的重写规则、条件和映射。默认情况下，重写引擎不允许继承重写配置，但此指令允许您更改默认设置。

### RewriteRule

该指令使您可以定义重写规则。规则必须有两个参数。第一个参数是必须满足才能应用替换字符串的搜索模式。搜索模式使用正则表达式编写（有关正则表达式的基础知识，请参见附录 B）。替换字符串可以由纯文本、搜索模式中的子串的回溯引用、服务器变量的值甚至映射函数构建。标志列表可以包含一个或多个由逗号分隔的标志字符串，以通知重写引擎接下来如何处理该替换。

**语法**：`RewriteRule search_pattern substitution_string [flag_list]`

**默认值**：无

**上下文**：服务器配置，虚拟主机，每目录访问控制文件 (`.htaccess`)

让我们看一个示例：

```
RewriteRule /-([^\ /]*)+/(.*) /users/$1/$2 [R]
```

在这里，搜索模式是 `/~([^\ /]*)+/(.*)`，替换字符串是 `/users/$1/$2`。注意替换字符串中回溯引用的使用。该

第一个反向引用字符串 $1 对应于第一组括号（从左侧开始）中匹配到的字符串。因此，$1 会被设置为在 `(\*/J+)` 中匹配到的内容，而 $2 则被设置为在 `(.*)` 中匹配到的下一个字符串。当 URL 请求如下所示时：

```
http://blackhole.evokew.org/~kabir/welcome.html
```

$1 的值为 `kabir`，$2 的值为 `welcome.html`；因此，替换字符串看起来像这样：

```
/users/kabir/welcome.html
```

当指定了**多个 `RewriteRule`** 时，第一个 `RewriteRule` 操作的是原始 URL，如果发生匹配，第二个规则将不再操作原始 URL。相反，它获取由第一个规则替换后的 URL，并在此 URL 上应用规则。在每一步都发生匹配的场景中，一组三个重写规则将按如下方式运作：

```
RewriteRule search-pattern-for-original-URL substitution1
    [flags]
RewriteRule search-pattern-for-substitution1 substitution2
    [flags]
RewriteRule search-pattern-for-substitution2 substitution3
    [flags]
```

通过使用 `C` 标志指示重写引擎将多个规则链接起来，可以对原始 URL 应用多个规则。在这种情况下，您可能希望在所有规则都匹配时才进行替换，以便您可以使用特殊的替换字符串来禁用规则中的替换。

表 9-2 列出了可能标志的详细信息。

| **标志** | **含义** |
| :--- | :--- |
| `C \| chain` | 此标志指定当前规则与下一个规则链接。当通过 `C` 标志链接时，只有当前一个链接中的规则产生匹配时，才会查看该规则。链接中的每个规则都必须包含此标志，如果第一个规则不匹配，则整个规则链将被忽略。 |
| `E=var:value` | 您可以使用此指令设置环境变量。该变量可以从重写条件、服务器端包含、CGI 脚本等地方访问。 |
| `F \| forbidden` | 当使用此标志的规则匹配时，会向浏览器发送一个名为 `FORBIDDEN`（状态码 403）的 HTTP 响应头。这实际上禁止了请求的 URL。 |
| `G \| gone` | 当使用此标志的规则匹配时，会向浏览器发送一个名为 GONE（状态码 410）的 HTTP 响应头。这通知浏览器请求的 URL 在此服务器上不再可用。 |
| `L \| last` | 这告诉重写引擎立即结束规则处理，从而不再将其他规则应用于最后一次替换后的 URL。 |
| `N \| next` | 这告诉重写引擎从第一个规则重新开始。然而，第一个规则不再尝试匹配原始 URL，因为它现在操作的是最后一次替换后的 URL。这实际上创建了一个循环。您必须在循环中具有终止条件，以避免无限循环。 |
| `NC \| nocase` | 这告诉重写引擎在模式匹配时变得不区分大小写。 |
| `NS \| nosubreq` | 使用此标志避免在内部生成的 URL 请求上应用规则。 |
| `P \| proxy` | 使用此标志将 URL 请求内部转换为代理请求。只有当 Apache 编译时包含了 `mod_proxy` 模块并配置为使用代理模块时，此功能才有效。 |
| `QSA \| qsaappend` | 此标志允许您将数据（例如 key=value 对）附加到替换 URL 的查询字符串部分。 |
| `R [= HTTP code] \| redirect` | 在替换字符串前添加 `http://server[:port]/` 前缀，强制对客户端进行外部重定向。如果未给出 HTTP 响应代码，则使用默认的重定向响应代码 302（MOVED TEMPORARILY）。此规则应与 L 或 last 标志一起使用。 |
| `S=n \| skip=n` | 跳过接下来的 n 个规则。 |
| `T=MIME-type \| file type=MIME-type` | 强制指定的 MIME 类型成为请求目标的 MIME 类型。 |

注意 您可以通过在规则前添加一个或多个 `RewriteCond` 指令来为规则添加条件，这些指令将在下一节中讨论。

### RewriteCond

当您希望为 `RewriteRule` 指令指定的重写规则添加额外条件时，`RewriteCond` 指令非常有用。每个 `RewriteRule` 可以有多个 `RewriteCond` 指令。所有重写条件都必须在规则本身之前定义。

**语法：** `RewriteCond _test_string_ condition_pattern [_flag-list_]`

**默认值：** 无

**上下文：** 服务器配置、虚拟主机、每目录配置（`.htaccess`）

测试字符串可以由纯文本、服务器变量或来自当前重写规则和最后一个重写条件的反向引用构建而成。要访问来自最后一个 `RewriteRule` 指令的第 *n* 个反向引用，使用 `$n`；要访问来自最后一个 `RewriteCond` 指令的第 *n* 个反向引用，使用 `%n`。

要访问服务器变量，请使用 `${_variable name_}` 格式。例如，要访问 `REMOTE_USER` 变量，请在测试字符串中指定 `%{REMOTE_USER}`。

表 9-3 列出了几种特殊的数据访问格式。

| 格式说明符 | 含义 |
| :--- | :--- |
| `%{ENV:_variable_}` | 使用此方法访问任何可供 Apache 进程使用的环境变量。 |
| `%{HTTP:_header_}` | 使用此方法访问请求中使用的 HTTP 头。 |
| `%{LA-U:_variable_}` | 使用此方法访问在当前处理阶段不可用的变量值。例如，如果您需要在存储在服务器配置文件（`httpd.conf`）中的重写条件中使用 `REMOTE_USER` 服务器变量，则不能使用 `%{REMOTE_USER}`，因为该变量仅在服务器执行身份验证阶段后才被定义，而该阶段在 `mod_rewrite` 的 URL 处理阶段之后。若要预看成功认证用户的用户名，您可以改用 `%{LA-U:REMOTE_USER}`。但是，如果您从每目录配置文件的 `RewriteCond` 中访问 `REMOTE_USER` 数据，可以使用 `%{REMOTE_USER}`，因为授权阶段已经完成，服务器变量已像往常一样可用。查找是通过生成基于 URL 的内部子请求来完成的。 |
| `%{LA-F:_variable_}` | 在大多数情况下与 `%{LA-U:_variable_}` 相同，但查找是使用基于文件名的内部子请求完成的。 |

条件模式除了可以是正则表达式外，还可以使用一些特殊表示法。例如，您可以通过在条件模式前加上 `<`、`>` 或 `=` 字符，在测试字符串和条件模式之间执行词法比较。在这种情况下，条件模式作为纯文本字符串与测试字符串进行比较。

有时您可能希望检查测试字符串是否为文件、目录或符号链接。在这种情况下，您可以将条件模式替换为表 9-4 中显示的特殊字符串。

| 条件选项 | 含义 |
| :--- | :--- |
| `-d` | 测试指定的目录是否存在 |
| `-f` | 测试指定的文件是否存在 |
| `-s` | 测试指定的非零大小文件是否存在 |
| `-l` | 测试指定的符号链接是否存在 |
| `-F` | 测试指定文件的可访问性和可访问性 |
| `-U` | 测试指定 URL 的有效性和可访问性 |

您可以在上述条件前面使用 `!` 来否定其含义。可选标志列表可以由一个或多个逗号分隔的字符串组成，如表 9-5 所示。

| 标志 | 含义 |
| :--- | :--- |
| `NC` | nocase：执行不区分大小写的条件测试。 |
| `OR` | ornext：通常，当您对 `RewriteRule` 指令有超过一个 `RewriteCond` 时，这些条件会通过 AND 连接以进行最终替换。但是，如果您需要在两个条件之间创建 OR 关系，请使用此标志。 |




## RewriteMap

*RewriteMap* 指令通过映射表实现键值查找。可以将映射表想象为一个数据表，其中每一行都包含一个键和一个值。通常，映射表存储在文件中。不过，映射表可以是文本文件、DBM 文件、内部 Apache 函数或外部程序。映射表的类型对应于映射表的来源。表 9-6 列出了适用的映射表类型。

-   语法：`RewriteMap name_of_map type_of_map:source_of_map`
-   默认值：无
-   上下文：服务器配置，虚拟主机

### 表 9-6 RewriteMap 指令的标志选项

| 映射表类型 | 描述 |
|---|---|
| txt | 纯文本文件，包含键值行，其中每个键值对位于同一行，并由至少一个空白字符分隔。文件可以包含以 # 字符开头的注释行，也可以包含空行。注释和空行均会被忽略。例如：<br>`Key1    value1`<br>`Key2    value2`<br>这定义了两个键值对。请注意，基于文本文件的映射表在 Apache 启动时读取，只有在服务器已经启动并运行且文件已被更新后才会重新读取。文件也会在服务器重启时重新读取。 |
| rnd | 一种特殊的纯文本文件，具有 txt 类型的所有限制，但在定义值方面更具灵活性。每个键的值可以定义为使用 \|（竖线）字符连接的“或”逻辑值集合。例如：<br>`Key1   first_value_for_key1 \| second_value_for_key1`<br>`Key2   first_value_for_key2 \| second_value_for_key2`<br>这定义了两个键值对，其中每个键都有多个值。选定的值是随机决定的。 |
| int | 内部 Apache 函数 `toupper(key)` 或 `tolower(key)` 可用作映射表源。第一个函数将键转换为全大写字符，第二个函数将键转换为全小写字符。 |
| dbm | DBM 文件可用作映射表源。当拥有大量键值对时，这非常有用且速度快（与文本文件相比）。请注意，基于 DBM 文件的映射表在 Apache 启动时读取，只有在服务器已经启动并运行且文件已被更新后才会重新读取。文件也会在服务器重启时重新读取。 |
| prg | 外部程序可以生成值。当使用外部程序时，该程序会在 Apache 启动时启动，数据（键，值）通过标准输入（stdin）和标准输出（stdout）在 Apache 和程序之间传输。使用外部程序时，请确保使用 RewriteLock 指令定义锁定文件。在构建此类程序时，也请确保以非缓冲 I/O 模式从 stdin 读取输入并将其写入 stdout。 |

## RewriteBase

如果您在每目录配置文件中重写规则，此指令才更有用。它仅适用于未映射到目标文件物理目录的 URL 路径。将此指令设置为您为该目录使用的任何别名。这将确保 mod_rewrite 在最终（替换后的）URL 中使用别名而不是物理路径。

-   语法：`RewriteBase base_URL`
-   默认值：每目录配置（`.htaccess`）的当前目录路径
-   上下文：每目录访问控制文件（`.htaccess`）

例如，当别名设置如下：

```plain
Alias /icons/ "/www/nitec/htdocs/icons/"
```

并且在 /www/nitec/htdocs/icons/.htaccess 文件中启用重写规则时，RewriteBase 指令应设置如下：

```plain
RewriteBase /icons/
```

## RewriteLog

如果您希望记录重写规则的应用情况，请使用此指令设置日志文件名。与其他所有日志指令一样，它假定没有前导斜杠（/）的路径表示您希望将日志文件写入服务器的根目录。

-   语法：`RewriteLog path_to_logfile`
-   默认值：无
-   上下文：服务器配置，虚拟主机

例如，以下指令在服务器根目录下的 logs 子目录中写入日志文件：

```
RewriteLog logs/rewrite.log
```

如前所述，服务器写入的日志应仅允许服务器用户写入。

## RewriteLogLevel

此指令允许您指定在日志文件中记录的内容。默认值 0 表示不记录任何内容。实际上，日志级别 0 表示模块内部没有执行与日志相关的处理。因此，如果您想禁用日志记录，请将其保持为 0。

-   语法：`RewriteLogLevel level`
-   默认设置：`RewriteLogLevel 0`
-   上下文：服务器配置，虚拟主机

**注意** 如果您将 `RewriteLog` 指令设置为 `/dev/null` 并将 `RewriteLogLevel` 设置为非零值，内部与日志相关的处理仍会执行，但不会生成日志。这会浪费系统的计算资源，因此如果您不想记录日志，请保持此指令为默认值。您可以选择 10 个日志级别，范围从 0 到 9。级别越高，写入的日志数据越多。

## RewriteLock

RewriteLock 指令允许您指定用于创建重写映射表的外部映射程序。使用 `RewriteLock` 指令时需要指定一个文件名。该文件用作锁定文件，以同步与外部映射程序的通信。

-   语法：`RewriteLock filename`
-   默认值：无
-   上下文：服务器配置，虚拟主机

## URL 布局

本节提供了处理 URL 布局的 URL 重写示例。通常，您需要将 URL 请求重定向或扩展到另一个 URL。以下示例展示了 `mod_rewrite` 如何在此类情况下提供帮助。

### 将请求的 URL 扩展为规范 URL

提供用户主页的网站通常支持此类 URL 方案：

```
http://hostname/~username
```

这是一个快捷 URL，需要映射到规范 URL。您可能还有其他快捷或内部 URL 需要扩展到其规范 URL。本示例展示了 `~username` 如何转换为 `/u/username`。图 9-2 说明了需要发生什么。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_281_0.png)

**图 9-2：** 将请求的 URL 扩展为规范 URL

当在（1）中接收到对 `http://hostname/~username` 的请求时，重写规则会将其转换为 `/u/username`，并将新 URL 重定向到浏览器（2）。然后，浏览器在（3）中重新请求 `http://hostname/u/username` URL，常规的 Apache 请求处理完成该请求。

外部 HTTP 重定向是必需的，因为后续的任何请求都必须使用转换后的规范 URL，而不是 `~username`。执行此操作所需的规则是：

```
RewriteRule ^~([^/]+)?(.*) /u/$1/$2 [R,L]
```

> **注意** 注意使用了 R 标志进行重定向，并使用 L 标志指示不能对替换后的 URL 应用其他重写规则。

拥有数千名用户的许多 ISP 网站使用结构化的主目录布局：即每个主目录位于一个子目录中，该子目录以，例如，用户名的第一个字符开头。因此，`/~foo/anypath` 是 `/home/f/foo/www/anypath`，而 `/~bar/anypath` 是 `/home/b/bar/www/anypath`。在这种情况下，为了实现从快捷 URL 到规范 URL 的转换方案，可以使用以下规则：

```
RewriteRule ^~([a-z][a-z0-9]+)(.*) /home/$2/$1/www/$3 [R,L]
```

### 将用户主目录重定向到新的 Web 服务器

如果您在 Web 服务器上有很多用户主页，并且由于某种原因需要将它们迁移到新机器，您需要一个类似于图 9-3 中所示的重定向规则。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_282_0.png)

使用 `mod_rewrite`，解决方案很简单。当浏览器请求如图（1）中所示的 `http://hostname/~username/anypath` 时，Web 服务器将其转换为如图（2）中所示的 `http://newhost/~username/anypath`，并将浏览器重定向到此新位置。在旧的 Web 服务器（即重定向 URL 的那个）上，只需将所有 `/~user/anypath` URL 重定向到 `http://new-host/~user/anypath`，如下所示：

```
RewriteRule   ^/–(.+)   http://newhost/$1   [R,L]
```

### 在多个目录中搜索页面

有时，需要让 Web 服务器在一个以上的目录中搜索页面。在这里，`MultiViews` 或其他技巧无法提供帮助。例如，假设您希望处理对 `http://hostname/filename.html` 的请求，以便如果 Web 服务器的 `dir1` 目录中没有 `filename.html`，服务器则尝试名为 `dir2` 的子目录。图 9-4 说明了需要发生什么。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_283_0.png)





## 实现此功能所需的规则如下：

```apache
RewriteCond   /your/docroot/dir1  %{REQUEST_FILENAME} -f
RewriteRule   ^(.+)  /your/docroot/dir1%1 [L]
RewriteCond   /your/docroot/dir2  %{REQUEST_FILENAME} -f
RewriteRule   ^(.+)  /your/docroot/dir2%1 [L]
RewriteRule   ^(.+)  - [PT]
```

如果请求的文件存在于 `your/docroot/dir1/` 子目录中，第一条规则才将请求的 URL 替换为 `/your/docroot/dir1/$1`（其中 `$1` 是请求中的目标文件）。如果满足条件，这就是应用于此 URL 的最后一条规则。但是，如果未找到匹配项，则应用下一条规则。这条规则的作用与第一条相同，但此次使用 dir2 子目录作为路径。如果找到匹配项，此规则也是最终的。如果没有任何规则匹配，则不会替换请求，而是将其传递给常规处理流程。

若要使用日志来验证该规则，首先通过在上述规则之前添加以下指令来启用重写日志记录。

```apache
RewriteLog logs/rewrite.log
RewriteLogLevel 5
```

重写日志 `rewrite.log` 将写入 `ServerRoot` 目录下的 `logs` 子目录中。日志级别设置为 `5`，以便包含相当多的信息。假设您的 `DocumentRoot` 指令设置为 `/usr/local/apache/htdocs`，且 `ServerRoot` 设置为 `/usr/local/apache`，您需要在 `httpd.conf` 中使用以下针对重写规则的特定指令。

```apache
RewriteLog logs/rewrite.log
RewriteLogLevel 5

RewriteCond   /usr/local/apache/htdocs/dir1  %{REQUEST_FILENAME} -f
RewriteRule   ^(.+)  /usr/local/apache/htdocs/dir1%1 [L]

RewriteCond   /usr/local/apache/htdocs/dir2  %{REQUEST_FILENAME} -f
RewriteRule   ^(.+)  /usr/local/apache/htdocs/dir2%1 [L]

RewriteRule   ^(.+)  - [PT]
```

重启 Apache 后，执行以下操作：

1. 以 root 身份运行 `tail -f /usr/local/apache/logs/rewrite.log`。此命令使您能够查看添加到 `rewrite.log` 文件中的日志条目。
2. 运行 `mkdir -p /usr/local/apache/htdocs/dir1` 和 `chmod -R a+t /usr/local/apache/htdocs/dir1`，以在文档目录下创建 `dir1` 目录，并将其所有权更改为 httpd 用户和组。这里还假设您是以 httpd 用户身份运行 Apache。对 *dir2* 执行相同操作。
3. 运行 `lynx -dump -head http://localhost/kabir.html` 命令。这将启动 Lynx Web 浏览器，并指示其仅显示 Web 服务器返回的响应头。现在，假设您在 */usr/local/apache/dir1*、*/usr/local/apache/dir2* 或 */usr/local/apache* 目录下都没有名为 *Kabir.html* 的文件，您应该看到类似以下的响应：

   ```http
   HTTP/1.1 404 Not Found
   Date: Fri, 16 Mar 2001 06:06:51 GMT
   Server: Apache/2.0.14 (Unix)
   Connection: close
   Content-Type: text/html; charset=iso-8859-1
   ```

4. 现在查看下方显示的 *rewrite.log* 条目。为了简洁，我去除了 IP 地址、时间戳和其他一些字段。

   ```log
   (2) init rewrite engine with requested uri /kabir.html
   (3) applying pattern '^(.+)' to uri '/kabir.html'
   (4) RewriteCond:
   input='/usr/local/apache/htdocs/dir1/kabir.html' pattern='.-f'
   > not-matched
   (3) applying pattern '^(.+)' to uri '/kabir.html'
   (4) RewriteCond:
   input='/usr/local/apache/htdocs/dir2/kabir.html' pattern='.-f'
   > not-matched
   (3) applying pattern '^(.+)' to uri '/kabir.html'
   (2) forcing '/kabir.html' to get passed through to next API
   URI-to-filename handler
   ```

   请注意，*mod_rewrite* 尝试在 *dir1* 和 *dir2* 中查找 *kabir.html* 文件，然后放弃了查找，由于请求是 *http://localhost/kabir.html*，结果导致 Apache 在文档根目录中查找相同文件。

5. 现在在 *dir1* 或 *dir2* 子目录中创建此测试文件 *kabir.html*，并更改文件的所有权，以便 Apache（httpd 用户）可以读取它。然后再次运行相同的 *lynx -dump -head http://localhost/kabir.html* 命令，并查看 *rewrite.log* 的内容。您将看到，根据您将文件放置的位置（*dir1* 或 *dir2*），其中一条规则已成功匹配。
6. 如果在所有三个目录——*/usr/local/apache/htdocs/dir1*、*/usr/local/apache/htdocs/dir2* 和 */usr/local/apache/htdocs* 中都有该测试文件，重写规则将选择 *dir1* 子目录中的文件，因为作为 [L]（最后）标志的结果，第一个匹配的条件获胜。

## 根据 URL 设置环境变量

您可能希望在请求之间保持状态信息，并使用 URL 对其进行编码。但您可能不希望仅为提取此信息而对所有页面使用 CGI 包装脚本。您可以使用重写规则来剥离状态信息，并通过环境变量存储它，以便之后在 SSI 或 CGI 内部引用。这样，`http://foo/?s=java/bar/` 将被转换为 `/foo/bar/`，并将名为 `STATUS` 的环境变量设置为值 `java`。图 9-5 说明了发生的情况。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_286_0.png)

### 图 9-5：从 URL 设置环境变量

当检测到对 `http://hostname/foo/?s=java/bar/` 的请求时，Apache 服务器将 $1 分配给 `foo`，$2 分配给 `java`，$3 分配给 `bar`，如图 9-5 所示。$2 的值用于设置环境变量 `STATUS`，Web 服务器执行到 `/foo/bar` 位置的重定向。图 9-5 中显示的重写步骤可以使用以下重写规则实现：

```apache
RewriteRule ^(.*)/S=([^/]+)/(.*)$ $1/$3 [E=STATUS:$2]
```

在这里，$2 的值使用 E 标志存储在名为 STATUS 的环境变量中。当此规则就位并且发起如 `lynx -dump -head http://localhost/dir1/S=value/kabir.html` 这样的请求时，重写日志（如果已启用）将显示：

```log
(2) init rewrite engine with requested uri /dir1/S=value/kabir.html
(3) applying pattern '^(.*)/S=([^/]+)/(.*)' to uri '/dir1/S=value/kabir.html'
(2) rewrite '/dir1/S=value/kabir.html -> /dir1/kabir.html
(5) setting env variable 'STATUS' to 'value'
(2) local path result: /dir1/kabir.html
(2) prefixed with document_root to /usr/local/apache/htdocs/dir1/kabir.html
(1) go-ahead with /usr/local/apache/htdocs/dir1/kabir.html [OK]
```

为了简洁，我缩短了重写日志的输出。请注意 mod_rewrite 已将 STATUS 变量设置为 'value'，因此现在如果基于 Perl 的 CGI 脚本想要访问 STATUS 环境变量的值，它可以使用 $ENV{STATUS}。同样，服务器端包含（SSI）指令也可以访问此环境变量。

## 创建 www.username.domain.com 站点

假设您有一些朋友希望在您的服务器上拥有 Web 站点。您决定不给他们 `http://www.domain.com/~username` 类型的站点，而是为每个人创建 `http://username.domain.com` 类型的站点。自然地，您会在 DNS 中添加每个基于用户名的主机名（例如，`www.kabir.domain.com`），使用指向您的 Web 服务器的简单 CNAME 记录。例如，在您的 DNS 中可能有：

```dns
www.domain.com IN A 192.168.1.100
```

要为名为 Joe 和 Jennifer 的两位朋友创建 Web 站点，您需要 domain.com 的以下 DNS 记录：

```dns
www.domain.com IN A 192.168.1.100
www.joe.domain.com IN CNAME www.domain.com
www.jennifer.domain.com IN CNAME www.domain.com
```

DNS 就绪并测试完毕后，您希望配置 Apache 以使用 `/home/username/www` 目录为这些站点提供服务，其中每个 username 是您朋友的用户账户名。

可以使用以下重写规则集将 `http://www.username.domain.com/any-path` 内部重写为 `/home/username/www/any-path`：

```apache
RewriteCond %{HTTP_HOST} ^www\.[^.]+\.domain\.com$
RewriteRule ^(.+) %1 [C]
RewriteRule ^www\.(.+)\.domain\.com/(.*) /home/$1/www/$2
```

图 9-6 说明了此工作原理。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_288_0.png)

### 图 9-6：每个用户名的虚拟主机

这是一个链式规则集的例子。第一条规则有一个条件，检查环境变量 `HTTP_HOST` 是否匹配诸如 `www.username.domain.com` 这样的模式。如果匹配，则应用该规则。换句话说，对于诸如 `http://www.username.domain.com/anypath` 这样的请求，`www.username.domain.com/anypath` 将被替换。这可能会让人有点困惑，因为替换并不十分明显。进行此替换是为了能够使用第二条规则提取用户名。第二条规则从替换后的请求中提取用户名部分，并为内部子请求创建新的 URL `/home/username/www/anypath`。




## 将失效 URL 重定向到另一台 Web 服务器

如果你拥有一个多服务器 Web 网络，并且经常在服务器之间移动内容，你可能会面临需要将 Web 服务器 A 上的失效 URL 请求重定向到 Web 服务器 B 的问题。实现这一点有很多种方法：你可以使用 `ErrorDocument` 指令，编写 CGI 脚本，或者使用 `mod_rewrite` 将失效的 URL 重写为指向另一台服务器的 URL。与使用 `ErrorDocument` 指令或 CGI 脚本相比，使用基于 `mod_rewrite` 的方案不太推荐。`mod_rewrite` 方案的性能最好，但灵活性较差，且对错误的防护性较低：

```apache
RewriteCond /your/docroot/%{REQUEST_FILENAME} !-f
RewriteRule ^(.+) http://Web serverB.dom/$1
```

问题在于，此解决方案仅对 `DocumentRoot` 指令内的页面有效。虽然你可以添加更多条件（例如处理主目录），但存在一个更优的变体：

```apache
RewriteCond    %{REQUEST_URI} !-U
RewriteRule    ^(.+)        http://Web serverB.dom/$1
```

此变体利用了 `mod_rewrite` 的 URL 前瞻功能，适用于所有类型的 URL。然而，这会对 Web 服务器产生性能影响，因为每个请求都会触发一个额外的内部子程序。如果你的 Web 服务器运行在强大的 CPU 上，请使用此解决方案；如果是速度较慢的机器，请使用第一种方法，或者更好的是，使用 `ErrorDocument` 指令或 CGI 脚本。

## 创建访问多路复用器

本示例向你展示如何创建一组规则，根据域名类型（如 .com、.net、.edu、.org、.uk、.de 等）重定向请求。其理念是将访问者重定向到地理位置最近的 Web 站点。许多大型企业采用此技术，将国际客户重定向到合适的 Web 站点或 FTP 服务器。

创建此类解决方案的第一步是创建一个映射文件。例如，下面显示了一个基于文本的映射文件，名为 `site-redirect.map`：

```
com    http://www.mydomain.com/download/
net    http://www.mydomain.com/download/
edu    http://www.mydomain.com/download/
org    http://www.mydomain.com/download/
uk     http://www.mydomain.uk/download/
de     http://www.mydomain.de/download/
ch     http://www.mydomain.ch/download/
```

当收到来自名为 dialup001.demon.uk 的主机对 http://www.mydomain.com/download/any path 的请求时，该请求需要重定向到 Web 站点 www.mydomain.uk/download/；类似地，来自属于顶级域名 .com、.net、.edu 和 .org 的主机的任何请求都会路由到 www.mycompany.com/download/ 站点。

以下是上述设置所需的规则：

```
RewriteMap     sitemap       txt:path/to/site-redirect.map
RewriteRule     ^/download/(.*)  %{REMOTE_HOST}:$1   [C]
RewriteRule     ^\.\+ ([. -z-A -z])+: (::)\* % {site map: $1} www.mydomain.com/download/$2 [R,L]
```

图 9-7 说明了此规则的使用情况。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_290_0.png)

如图 9-7 所示，当 dialup001.demon.uk 这样的主机请求 www.mydomain.com/download/index.html 页面时（1），第一条规则通过使用该请求主机的主机名来重写请求，如下所示：

```
dialup001.demon.uk::index.html
```

然后应用链中的下一条规则。当搜索模式匹配且通过查找映射文件中的顶级域名创建替换 URL 时，将应用此规则。如果未找到匹配项，则使用默认的 www.mydomain.com。这是通过在替换 URL 字符串中使用 |（或）运算符完成的。也许使用列表 9-1 中所示的算法更容易理解第二条规则。

### 列表 9-1：第二条重写规则的算法

```
if(current URL matches a fully-qualified-hostname::anything)
then

# substitute the current URL using the domain type information
# stored in $1 perform a lookup in the map file.
If (map file has a key that matches the domain type) then
#use the key's value as follows:

Substituted URL = value-of-the-key$2
#where $2 is anything after
#fully-qualified-hostname:: pattern

Else

# Use default value www.mydomain.com/download/$2
Substituted URL = www.mydomain.com/download/$2

endif
Endif
```

R 标志使其成为外部 URL 重定向，L 标志使其成为替换 URL 的最后一条规则。由规则 #2 创建的新位置在（2）中发送给 Web 浏览器，并在图 9-7 所示的（3）中获取页面。

## 创建时间敏感的 URL

你是否曾想过是否可能拥有一个根据时间指向不同文件的 URL？好吧，mod_rewrite 使得创建这样的 URL 变得很容易。有许多名为 TIME_xxx 的重写条件变量。使用特殊的字典序比较模式 `<STRING`、`>STRING` 和 `=STRING`，你可以执行基于时间的重定向，例如：

```
RewriteCond %{TIME_HOUR}%{TIME_MIN} >0700
RewriteCond %{TIME_HOUR}%{TIME_MIN} <1900
RewriteRule ^foo.html$ foo.day.html
RewriteRule ^foo.html$ foo.night.html
```

这会在 07:00 到 19:00 期间通过 URL foo.html 提供 foo.day.html 的内容，而在其余时间提供 foo.night.html 的内容。

## 内容处理

本节的示例涉及与内容相关重写规则。我将向你展示如何创建向后兼容的 URL、基于浏览器内容的重写、对终端用户透明的 HTML 到 CGI 重定向等。

### 在 URL 中添加向后兼容性

假设你最近将页面 *bar.html* 重命名为 *foo.html*，现在你想为向后兼容性提供旧 URL。此外，你不想让使用旧 URL 的用户意识到页面已被重命名。该怎么做？方法如下：

```
RewriteRule    ^foo\.html$  bar.html
```

如果你想让浏览器知道变更，你可以执行外部重写，以便浏览器显示新 URL。你只需按如下方式添加 *R 标志* 即可：

```
RewriteRule    ^foo\.html$  bar.html [R]
```

### 创建基于浏览器匹配的内容 URL

你可以使用重写规则向不同的浏览器分发不同的内容（使用内部子请求）。你不能为此使用内容协商，因为浏览器不会以那种形式提供它们的类型。相反，你必须对 HTTP 头 *User-Agent* 进行操作。例如，如果浏览器的 *User-Agent* 头匹配 *Mozilla/5*，则你可以发送一个支持 Netscape Navigator 5（或更高版本）特性的页面，或者如果浏览器是旧版本的 Navigator 或其他类型的浏览器，你可以发送一个不同的页面。

如果 HTTP 头 *User-Agent* 以 *Mozilla/5* 开头，则页面 *foo.html* 会被重写为 *foo.ns.html*，并且重写停止。如果浏览器是 Lynx 或 Mozilla 1 到 4 版本，则 URL 变为 *foo.dull.html*。所有其他浏览器都会收到页面 *foo.cool.html*。这是通过以下规则完成的：

```
RewriteCond %{HTTP_USER_AGENT}    "Mozilla/5.*
RewriteRule ^foo\.html$         foo.cool.html  [L]

RewriteCond %{HTTP_USER_AGENT}    "Lynx/. *       [OR]
RewriteCond %{HTTP_USER_AGENT}    "Mozilla/[1234].*
RewriteRule ^foo\.html$           foo.dull.html  [L]
```

当收到对诸如 *http://hostname/foo.html* 这样的 URL 的请求时，第一个条件测试环境变量 *HTTP_USER_AGENT* 是否包含字符串 *Mozilla/5*。如果包含该字符串，则应用第一条规则。此规则将 *foo.cool.html* 替换为原始 URL，并完成所有重写；然而，当第一条规则未应用时，将调用第二条规则。有两个 OR 条件。换句话说，在应用此规则之前，这些条件中必须有一个匹配。

第一个条件测试环境变量中是否包含子串 Lynx/，第二个条件测试环境变量中是否包含子串 Mozilla/1* 到 Mozilla/4/。如果满足这些条件中的任何一个，则应用该规则。该规则用 foo.dull.html 替换原始 URL。替换后的 URL 会被转换为子请求，并由 Apache 按常规处理。

### 创建 HTML 到 CGI 网关

如果你想将静态页面 foo.html 无缝转换为动态变体 foo.cgi——也就是说，不通知浏览器或用户——方法如下：

```
RewriteRule ^foo\.html$ foo.cgi [T=application/x-http-cgi]
```

该规则将对 foo.html 的请求重写为对 foo.cgi 的请求。它还强制使用正确的 MIME 类型，以便作为 CGI 脚本运行。对 http://hostname/foo.html 这样的请求会在内部转换为对 CGI 脚本的请求。浏览器并不知道其请求已被重定向。

## 访问限制

这些示例涉及访问控制问题。在本节中，我将向你展示如何使用 URL 重写模块来控制对 Web 站点特定区域的访问。

### 屏蔽爬虫

屏蔽烦人的 Web 爬虫程序（也称为 robots）检索特定 Web 站点的页面很容易。你可能尝试过包含机器人排除协议（Robot Exclusion Protocol）条目的 /robots.txt 文件，但这通常不足以摆脱此类爬虫。一个示例解决方案是：

```
RewriteCond %{HTTP_USER_AGENT} ^NameOfBadRobot.*
RewriteCond %{REMOTE_ADDR} ^123\.45\.67\.[879]$
RewriteRule ^/not/to/be/indexed/by/robots/.+ - [F]
```

此规则有两个条件：

```
If (`HTTP_USER_AGENT of the robot matches a pattern "NameOfBadRobot"` ) and
(`REMOTE_ADDR of the requesting host is 123.45.67.8 to 123.45.67.9` ) then
    No substitution but send a HTTP "Forbidden" header (status code 403)
endif
```




如你所见，机器人的 User-Agent 标头已匹配，同时还检查了其使用的主机 IP 地址。上述条件允许检查多个 IP 地址（123.45.67.8 和 123.45.67.9）。

## 创建基于 HTTP 推荐人的 URL 重定向器

你可以编写一个灵活的 URL 重定向器，使其作用于 Referrer HTTP 标头，并配置任意数量的推荐页面。方法如下：

```apache
RewriteMap  deflector txt:path/to/deflector.map
RewriteRule  ^/(.*)
  $1deflector:&(HTTP_REFERER)|/$1
RewriteRule .*DEFLECTED  &[HTTP_REFERER] [R,L]
RewriteRule .* - [PT]
```

这需要与相应的重写映射配合使用，如下所示：

| http://www.badguys.com/bad/index.html | DEFLECTED |
|----------------------------------------|-----------|
| http://www.badguys.com/bad/index2.html | DEFLECTED |
| http://www.badguys.com/bad/index3.html | http://somewhere.com/ |

如果 URL 匹配映射文件中的 DEFLECTED 值，这将自动将请求重定向回推荐页面。在其他所有情况下，请求将被重定向到指定的 URL。

## 设置代理服务器

![](img/e11fcbd2818a3495ac70085e5d8d1c26_295_0.png)

代理服务器是位于客户端主机与需要访问的服务器之间的系统。当客户端主机使用 URL 请求某个远程资源时，代理服务器接收该请求并获取资源以满足客户端的请求。从广义上讲，代理服务器对客户端主机而言像是一个服务器，而对远程服务器而言则是一个客户端。

在典型的代理场景中，该过程使代理服务器能够存储请求的内容到缓存中。任何请求已在缓存中的信息的新请求，不再需要从远程服务器获取数据进行服务。相反，新请求将从缓存数据中服务。这使得代理服务器能够缓解网络瓶颈。然而，代理服务器所做的不仅仅是这些。

本章教你如何将 Apache 转换为可以执行多种服务的代理服务器。你将学习如何将 Apache 转换为缓存（正向）代理服务器。在网络瓶颈处部署此类服务器可以减少响应时间的延迟，节省带宽，并有助于降低整体通信成本。由于代理通常用于拥有大量用户社区的网络，我还涵盖了客户端配置的各个方面，包括自动代理配置。

### 谁应该使用代理服务器？

该代理服务器的目的是从远程服务器获取请求的资源，将其返回给请求用户，并在本地驱动器中缓存。代理服务非常适合多个用户访问网络的场景。许多组织拥有多台通过单个互联网连接（如 ISDN 路由器或其他专用或按需连接）访问互联网的主机计算机。在此类网络中，代理可能非常有用。

**本章内容**

- 理解代理服务器类型
- 配置 Apache 作为代理服务器
- 为代理设置 Web 浏览器

通过为互联网和内部网络资源使用代理，你可以获得以下好处：

- 代理转发：如果内部网络出于安全或成本原因使用不可路由的 IP 地址，你可以使用代理服务器为通常无法访问互联网的主机提供互联网资源。本章将教你如何做。
- 缓存：使用如 Apache（配合 mod_perl）这样的缓存代理，你可以为本地用户提供看似更快的互联网资源访问。这不仅会增强用户对网络性能的感知，还会减少带宽使用成本。
- 日志记录和访问控制：通过使用代理服务器，你可以监控员工或学生对互联网（甚至内部网络）的使用。你可以阻止访问某些网站以保护公司免受潜在诉讼的影响，并可以制止公司时间的滥用。通过分析代理服务器的访问日志和错误日志，你可以识别使用模式并制定更好的网络使用策略。

### 理解代理服务器类型

在讨论将 Apache 用作代理服务器之前，让我们先讨论代理服务器的类型及其工作原理。有两种类型的代理服务器：

- 正向代理服务器：使用这种类型的代理服务器时，用户将请求传递给代理服务器，代理服务器从请求的目标主机获取预期的响应。正向代理通常在用户程序（如 Web 浏览器）中显式定义。
- 反向代理服务器：使用这种类型的代理服务器时，用户通常对其无感知，因为他们认为自己正在访问预期的资源。用户发出的所有请求都发送到反向代理，反向代理从缓存提供服务响应，或向另一台主机请求信息。

#### 正向代理

正向代理服务器通常位于用户主机与他们想要访问的远程资源之间。资源可以是互联网资源，如图 10-1 所示，也可以是内部网络资源。如果数据未过期，对相同资源的下一个请求将从缓存数据中服务。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_297_0.png)

图 10-1：正向代理服务器

用户主机知道它们正在使用代理服务器，因为每台主机都必须配置为使用代理服务器。例如，在浏览器可以使用代理服务器之前，必须告知 Web 浏览器使用代理服务器。所有远程请求都通过正向代理服务器进行信道传输，如图 10-1 所示，为减少带宽使用和实施用户访问策略提供了可管理和成本效益的解决方案。

这种类型的代理服务器也称为缓存代理服务器。反向代理服务器也缓存数据，但其作用与正向代理服务器相反。

#### 反向代理

反向代理服务器位于互联网资源之前，如图 10-2 所示，或位于内部网络资源之前。在此配置中，反向代理从原始服务器获取请求的资源并将其返回给用户主机。

连接代理服务器的用户主机并不知道自己正在连接代理服务器而不是直接连接到资源服务器，这与使用正向代理服务器时的情况不同。就最终用户而言，请求的资源是被直接访问的。

图 10-2 显示，来自互联网的用户无法绕过反向代理连接到 Web 服务器。由于这是反向代理，用户对其无感知，并以为自己在直接连接到 Web 服务器。局域网用户可以从内部网络直接连接到 Web 服务器，如图所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_298_0.png)

例如，如果为一个名为 `www.csus.edu` 的网站使用反向代理服务器，那么加州州立大学萨克拉门托分校（CSUS）的学生只需要将浏览器指向 `www.csus.edu`，而不需要告知浏览器任何关于代理配置的内容。浏览器向名为 `www.csus.edu` 的服务器发出请求。浏览器毫不知情，`www.csus.edu` 服务器实际上是一个反向代理服务器，它在内部将请求转换为名为 `internal-www.csus.edu` 的 Web 服务器以获取请求的内容。这种设置带来了什么好处？由于数据从每个请求中缓存，代理服务器可以为幕后真实服务器提供某种负载均衡支持。

> Apache 目前不支持反向代理服务；然而，这将在 `mod_proxy` 模块的下一个版本中实现。

## mod_proxy 指令

Apache 中的代理支持来自 `mod_proxy` 模块。此模块默认未编译。你必须使用 `./config.status --enable-module=proxy` 从 Apache 源代码分发目录重新配置 Apache，并运行 `make && make install` 以重新编译和重新安装更新的 Apache 服务器。目前，它仅在 Apache 中实现了缓存代理服务器。它支持 HTTP 1.1、HTTPS（通过 SSL 的 CONNECT）和 FTP 协议。该模块还可配置为连接这些及其他协议的其他代理模块。它提供了以下部分讨论的指令。





## ProxyRequests

ProxyRequests 允许您启用或禁用缓存代理功能。但它不会影响 ProxyPass 指令的功能。

- 语法：ProxyRequests On | Off
- 默认设置：ProxyRequests Off
- 上下文：服务器配置、虚拟主机

## ProxyRemote

ProxyRemote 允许您将您的代理服务器与其他代理服务器进行互连。

- 语法：ProxyRemote match remote_proxy_server_URL
- 默认设置：无
- 上下文：服务器配置、虚拟主机

match 的值可以是以下之一：

- 远程服务器支持的 URL 协议名称
- 一个部分 URL，对于该部分 URL 应使用远程服务器
- 指示服务器应联系以处理所有请求

remote_proxy_server_URL 可以指定为 http://hostname::port。请注意，目前仅支持 HTTP 协议。换句话说，您只能指定处理 HTTP 协议的代理服务器；但是，您可以按照以下方式将来自您的代理服务器的 FTP 请求转发到同时支持 HTTP 和 FTP 协议的服务器：

```
ProxyRemote ftp http://ftp.proxy.evoknow.com:8000
```

这将所有到达本地代理服务器的 FTP 请求发送到 ftp://ftp.proxy.evoknow.com。请求通过 HTTP 发送，因此实际的 FTP 事务发生在远程代理服务器上。

如果您只想将针对特定网站的代理请求直接转发到其代理服务器，可以使用此指令。例如：

```
ProxyRemote http://www.bigisp.com/ http://web-proxy.bigisp.com:8000
```

这将所有匹配 www.bigisp.com 的请求发送到 web-proxy.bigisp.com。然而，如果您希望将所有代理请求转发到另一个代理，可以使用星号作为匹配短语。例如：

```
ProxyRemote * http://proxy.domain.com
```

这将所有本地代理请求发送到 proxy.domain.com 的代理服务器。

## ProxyPass

ProxyPass 允许您将 Web 服务器的文档树映射到代理服务器的文档空间。

- 语法：ProxyPass relative_URL destination_URL
- 上下文：服务器配置、虚拟主机

例如：

```
ProxyPass /internet/microsoft www.microsoft.com/
```

如果在名为 proxy.evoknow 的代理服务器的 httpd.conf 文件中找到了 ProxyPass，它将允许该代理服务器的用户使用以下 URL 访问 Microsoft 网站：

```
http://proxy.evoknow.com/internet/microsoft
```

这就像远程网站的镜像一样工作。任何使用 <relative-URL> 的请求都会在内部转换为针对 <destination-URL> 的代理请求。

如果远程站点包含绝对引用，图像可能不会显示，链接也可能无法工作。此外，您不能将此指令与 SSL 目标服务器一起使用。

## ProxyBlock

ProxyBlock 指令允许您阻止访问指定的主机或域名。

- 语法：ProxyBlock partial_or_full_hostname [ . . .]
- 上下文：服务器配置、虚拟主机

例如：

```
ProxyBlock gates
```

阻止访问名称中包含单词 gates 的任何主机。这样，对 http://gates.ms.com 或 http://gates.friendsOfBill.com 的访问就会被阻止。您也可以指定多个主机。例如：

```
ProxyBlock apple orange.com banana.com
```

阻止所有访问匹配上述任何单词或域名名的主机。mod_proxy 模块会在服务器启动时尝试确定这些主机的 IP 地址，并将其缓存以备后续匹配。

要阻止访问所有主机，请使用：

```
ProxyBlock *
```

这实际上禁用了您的代理服务器。

## NoProxy

NoProxy 为在局域网环境中控制 ProxyRemote 指令提供一些控制。

- 语法：NoProxy Domain_name| Subnet | IP_Address | Hostname
- 默认设置：无
- 上下文：服务器配置、虚拟主机

您可以指定一个域名、子网、IP 地址或主机名，使其不由 ProxyRemote 指令中指定的代理服务器提供服务。例如：

```
ProxyRemote * http://firewall.yourcompany.com:8080
NoProxy .yourcompany.com
```

这里，所有针对 <anything>.yourcompany.com（例如 www.yourcompany.com）的请求都由本地代理服务器处理，而其他所有请求都去 firewall.yourcompany.com 代理服务器。

## ProxyDomain

ProxyDomain 指定代理服务器的默认域名。

- 语法：ProxyDomain Domain
- 默认设置：无
- 上下文：服务器配置、虚拟主机

当此指令设置为局域网中的本地域名时，任何不包含域名的请求都将附加此域名；例如：

```
ProxyDomain .evoknow.com
```

当 evoknow.com 域的用户发送一个针对 http://marketing/us.html 这样的 URL 的请求时，该请求会重新生成为以下 URL：

```
http://marketing.evoknow.com/us.html
```

请注意，您在 ProxyDomain 指令中指定的域名必须有一个前导点。

### CacheRoot

CacheRoot 允许您启用磁盘缓存。您可以指定一个目录名，代理服务器可以在其中写入缓存文件。

- 语法：CacheRoot directory
- 默认设置：无
- 上下文：服务器配置、虚拟主机

运行代理模块的 Apache 服务器必须具有该目录的写权限，例如：

```
CacheRoot /www/proxy/cache
```

这告诉 Apache 将代理缓存数据写入 /www/proxy/cache 目录。请注意，在代理服务器开始使用此目录进行缓存之前，您需要使用 CacheSize 指令指定缓存的大小。您可能还需要使用其他缓存指令（稍后讨论）来创建可用的磁盘缓存代理方案。

### CacheSize

CacheSize 指定用于磁盘缓存的磁盘空间量（以千字节为单位）。缓存文件写入 CacheRoot 指令指定的目录中。

- 语法：CacheSize kilobytes
- 默认设置：CacheSize 5
- 上下文：服务器配置、虚拟主机

> **注意**
> 虽然代理服务器写入的数据量可能超过指定限制，但代理服务器的垃圾回收方案将删除文件，直到使用量达到或低于此设置。默认设置（5K）是不现实的；我建议根据用户负载在 10MB 到 1GB 之间。

### CacheGcInterval

CacheGcInterval 指定 Apache 应检查缓存目录以删除过期文件的时间（以小时为单位）。这也是 Apache 强制执行 CacheSize 指令指定的磁盘空间使用限制的时间。

- 语法：CacheGcInterval hours
- 默认设置：无
- 上下文：服务器配置、虚拟主机

### CacheMaxExpire

CacheMaxExpire 指定所有缓存文档过期的时间（以小时为单位）。此指令覆盖文档本身指定的任何过期日期；因此，如果文档的过期日期晚于此指令指定的最大值，该文档仍会被移除。

- 语法：CacheMaxExpire hours
- 默认设置：CacheMaxExpire 24
- 上下文：服务器配置、虚拟主机

默认值允许缓存文档在 24 小时后过期。如果您希望文档更晚过期，请更改此值。

### CacheLastModifiedFactor

CacheLastModifiedFactor 指定当原始 Web 服务器未提供文档的过期日期时，用于计算过期时间的因子。

- 语法：CacheLastModifiedFactor floating_point_number
- 默认设置：CacheLastModifiedFactor 0.1
- 上下文：服务器配置、虚拟主机

计算使用此公式进行：

```
expiry_period = (last modification time for the document) *
(floating point number)
```

因此，如果一个文档最后一次修改于 24 小时前，那么默认的因子 0.1 使 Apache 计算该文档的过期时间为 2.4 小时。如果计算的过期期长于 CacheMaxExpire 设置的值，则 CacheMaxExpire 的过期期优先。




## CacheDirLength

当磁盘缓存开启时，Apache 会在 *CacheRoot* 指令指定的目录下创建子目录。该指令指定了用于创建子目录名称的字符数。你通常不需要更改此指令的默认值。对于想了解这些子目录是如何或为何被创建的好奇用户，下面给出了简化的解释。

- **语法：** CacheDirLength *length*
- **默认设置：** CacheDirLength 1
- **上下文：** 服务器配置、虚拟主机

Apache 在创建 URL 数据的缓存路径和文件名时使用了一种哈希方案。例如，当缓存开启且通过代理 Apache 服务器访问一个 URL（例如 *www.microsoft.com*）时，服务器会对该 URL 进行哈希处理，以便日后能快速检索数据。该哈希值可能类似于 1Y5RxSmB2OQ_HkqkTuXeqvw。如果 CacheDirLength 和 CacheDirLevels 指令都使用默认值，Apache 会将 *www.microsoft.com* 上找到的数据存储在一个名为：

%CacheRoot%/*/1/Y/5/RxSmB2OQ_HkqkTuXeqvw

的文件中。

这里的 %CacheRoot% 是由 *CacheRoot* 指令指定的目录。*1/Y/S* 目录之所以被创建，是因为 *CacheDirLevels* 指令的默认值。当再次使用相同的 URL 请求此文档时，Apache 只需重新计算哈希值即可从指定路径检索页面。

## CacheDirLevels

CacheDirLevels 指定了 Apache 创建用于存储缓存数据文件的子目录数量。相关信息请参阅上一节。

- **语法：** CacheDirLevels *levels*
- **默认设置：** CacheDirLevels 3
- **上下文：** 服务器配置、虚拟主机

## CacheDefaultExpire

CacheDefaultExpire 提供了一个默认时间（以小时为单位），当文件最后修改时间未知时，用于使缓存文件过期。*CacheMaxExpire* 不会覆盖此设置。

- **语法：** CacheDefaultExpire *hours*
- **默认设置：** CacheDefaultExpire 1
- **上下文：** 服务器配置、虚拟主机

## NoCache

- **语法：** NoCache _Domain_name_ | _Subnet_ | _IP_Address_ | _Hostname_ . . .
- **默认设置：** 无
- **上下文：** 服务器配置、虚拟主机

NoCache 指令指定了一个以空格分隔的主机、域名和 IP 地址列表，对于列表中的项目，不执行缓存。该指令应用于禁用对内部网络中本地 Web 服务器的缓存。请注意，代理服务器也会匹配主机的部分名称。如果你想完全禁用缓存，请使用以下配置：

```apache
NoCache *
```

# 配置 Apache 代理服务器

在本节中，我将展示如何将 Apache（使用 _mod_proxy_）配置为正向代理服务器。在你已将 _mod_proxy_ 模块编译进 Apache（如前文所述）之后，设置代理服务器就相当简单了。

要启用代理服务器，你需要在 _httpd.conf_ 文件中将 _ProxyRequests_ 设置为 _On_。额外的配置取决于你希望代理服务器执行什么操作。无论你对代理服务器做何打算，任何你想要用于控制代理服务器行为的指令都应放在一个特殊的 `<Directory ...>` 容器中，格式如下：

```apache
<Directory proxy:*>
<.dir>
</Directory>
```

星号（*）是请求 URL 的通配符。换句话说，当对 _www.evoknow.com_ 的请求由 Apache 服务器处理时，其形式如下：

```apache
<Directory proxy:http://www.evoknow.com>
<.dir>
</Directory>
```

你也可以使用 `<Directory ~ /RE/>` 容器，该容器使用正则表达式，允许你在定义代理配置时拥有更大的灵活性。例如：

```apache
<Directory ~ proxy:http://[a-z]+.*/.*>
<.dir>
</Directory>
```

现在让我们查看几种常见的代理配置。

## 场景 1：将私有 IP 网络连接到互联网

在此场景中，该网络中只有一台计算机被分配了互联网可路由的 IP 地址，如**图 10-3**所示。该计算机运行 Apache 代理服务器，将 `ProxyRequests` 设置为 `On`，且无需额外的代理配置。该代理服务器处理所有请求。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_306_0.png)

在这种配置中，代理服务器需要多宿主；也就是说，它需要能够同时访问不可路由的私有网络（`192.168.1.0`）和可路由的 IP 网络（`206.171.50.0`）。在某种程度上，虽然所选的不可路由 IP 池已经实现了类似功能，但该代理充当了私有 IP 网络的防火墙。代理允许主机访问互联网服务，例如 Web、FTP 等。

## 场景 2：缓存远程 Web 站点

由于互联网和内部网络上的大量 Web 内容很可能是静态的，在本地代理服务器上缓存它们可以节省宝贵的网络带宽。启用缓存的代理服务器仅当缓存中包含已过期文档或请求的文档不存在于缓存中时，才会获取请求的文档。要在你的代理服务器上启用缓存，你需要在特殊的目录容器中指定缓存指令。例如：

```apache
<Directory proxy:*>
CacheRoot /www/cache
CacheSize 1024
CacheMaxExpire 24
</Directory>
```

此配置定义了一个缓存代理服务器，它将缓存文件写入 `/www/cache` 目录。它允许写入 1024K 的数据（1MB），并且缓存必须在每天（24 小时）后过期。

如果你不想允许外部人员滥用你的代理服务器，你可以通过主机限制或用户名/密码认证来限制代理服务器的访问。

要控制哪些主机可以访问代理服务器，你可以创建如下配置：

```apache
<Directory proxy:*>
AuthType Basic
AuthName Proxy
order deny,allow
deny from all
allow from myhost.evoknow.com
</Directory>
```

此配置拒绝了除 `myhost.evoknow.com` 之外的所有访问。如果你想要使用用户名/密码认证，可以使用类似于以下的配置：

```apache
<Directory proxy:*>
AuthType Basic
AuthName Proxy
AuthUserFile /path/to/proxy/.htpasswd
require valid-user
</Directory>
```

**交叉参考** 如果你不确定如何创建必要的密码文件，请参阅第 7 章。

限制对特定协议的访问也是可能的。例如：

```apache
<Directory proxy:http:>
.
</Directory>
```

使你能够控制你的代理服务器如何处理 HTTP 请求。类似地，你可以使用以下配置来控制代理服务器如何处理每个协议：

```apache
<Directory proxy:ftp:*>
.
</Directory>
```

或者

```apache
<Directory proxy:https:*>
...
</Directory>
```

你还可以为代理服务器创建一个专用虚拟主机。在这种情况下，指令应放在代理主机的 `<VirtualHost>` 容器内：

```apache
<VirtualHost proxy.host.com:*>
...
</VirtualHost>
```

## 场景 3：镜像 Web 站点

镜像 Web 站点是远程 Web 站点的本地副本。例如，如果你希望镜像 `www.apache.org` Web 站点，以便你的用户能够快速访问 Apache 信息，你可以使用代理服务器创建这样一个镜像，如下所示：

```apache
ProxyPass / www.apache.org/
CacheRoot /www/cache
CacheDefaultExpire 24
```

这将使代理服务器成为 `www.apache.org` Web 站点的镜像。例如，此配置将我的代理服务器 `blackhole.evoknow.com` 变成了一个 Apache 镜像。当用户输入 `http://blackhole.evoknow.com` 作为 URL 时，用户会收到 Apache 镜像的索引页面，就好像她访问了 `www.apache.org` 一样。

在镜像他人的 Web 站点之前，获得许可至关重要，因为可能涉及版权问题。

# 设置 Web 浏览器使用代理

在配置好代理服务器后，你准备好在客户机主机上设置 Web 浏览器了。流行的 Web 浏览器使得使用代理服务器变得非常容易。在接下来的部分中，我将展示如何为代理配置 Netscape Navigator 6 和 Microsoft Internet Explorer (IE) 5.5。为这些浏览器设置代理服务器有两种方式：手动或自动代理配置。

手动配置 Web 浏览器使用代理并不难。但是，如果你有很多需要配置的用户计算机，那么每次你需要更改代理配置时，这可能都会变成一个巨大的麻烦。这就是自动代理配置对于浏览器变得有用的地方。

## 手动代理配置

当只有少数几台客户机且代理配置不经常更改时，你希望进行手动代理配置。如果你的


需求各不相同，例如，如果你拥有数百台客户端机器，你应该跳至“自动代理配置”部分。

## 手动配置 Netscape

以下步骤将引导你完成 Netscape 的手动代理配置：

1. 从导航器菜单栏中选择“编辑->首选项”。你应该会看到如图 10-4 所示的对话框窗口。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_309_0.png)

2. 点击“高级”类别。

3. 点击“代理”类别。

4. 点击“手动代理配置”选项。

5. 在 HTTP、FTP 和安全 (HTTPS) 数据输入字段中输入代理服务器 URL，以及端口信息。由于我为所有这些协议使用单一代理服务器，因此 URL (`http://proxy.evknow.com/`) 和端口 (8080) 是相同的。如果你为这些服务中的每一项使用不同的代理服务器，你应该相应地指定它们。

6. 输入信息后，请求一个远程文档以确定你的代理是否按预期工作。判断情况的一种好方法是监控代理服务器的访问日志和错误日志。在大多数 Unix 系统上，你可以使用如下命令查看写入文件的日志条目：

```
tail -f /path/to/access/log
```

## 手动配置 Internet Explorer

现在让我们配置 Windows 平台的 Microsoft Internet Explorer。要手动配置 Internet Explorer 使用代理，请遵循以下步骤：

1. 选择工具 `->` Internet 选项。这将弹出如图 10-5 所示的对话框窗口。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_310_0.png)

**图 10-5：** Microsoft Internet Explorer 手动代理设置窗口

2. 点击“连接”选项卡，然后点击“局域网设置”按钮。假设你正在使用局域网网关/路由器连接到 Internet。

3. 选择“使用代理服务器”选项。

4. 在提供的字段中输入代理服务器 URL 和端口号。

5. 点击“确定”以完成配置。

如果你想为不同的协议指定不同的代理服务器信息，你可以使用“高级”按钮弹出如图 10-6 所示的窗口。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_310_1.png)

**图 10-6：** Internet Explorer 高级代理设置窗口。

在这里，与 Netscape Navigator 一样，你可以指定不同的代理服务器设置。点击“确定”并点击“应用”按钮以应用新设置后，你的浏览器就被配置为使用代理服务器了。

## 自动代理配置

Netscape Communications 的善心人士考虑到了为多个客户端计算机手动配置代理所涉及的问题，并想出了一种绕过这种麻烦的方法。当 Web 浏览器启动时，它会加载来自 JavaScript 文件的功能（该文件如何提供给 Web 浏览器将在后面讨论），并为每个 URL 请求调用 `FindProxyForURL`。浏览器向该函数提供主机和 URL 参数，以便它可以返回最合适的代理配置。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_311_0.png)

> Microsoft 也赶上了 Internet Explorer 的自动配置选项。不幸的是，Microsoft 使自动配置稍微难以集成到浏览器中。你必须获得 Internet Explorer Administrator Kit (IEAK) 才能创建自动配置文件。由于获得 IEAK 需要一份许可协议，该协议要求每个 IEAK 许可用户每季度向 Microsoft 报告与 IEAK 相关的使用情况，因此本作者未获取该工具。然而，我从一个可靠来源确认 IEAK 文档讨论了类似 Netscape 的自动代理配置场景，甚至可以使用相同的脚本。本节适用于 IE 和 Navigator。唯一的区别是，如果你希望这在 IE 中起作用，你必须弄清楚如何使用 IEAK 创建适当的文件。

代理自动配置是使用特殊的 JavaScript 完成的。对于 Netscape Navigator 和 IE 都是如此。这种特殊的 JavaScript 具有以下要求：

代理自动配置 JavaScript 必须实现一个名为 `FindProxyForURL` 的函数。该函数具有以下框架：

```javascript
function FindProxyForURL(url, host) {
    // java script code goes here

    return "proxy to use for servicing the URL";
}
```

该函数接收的参数是 `url` 和 `host`。`url` 是请求的完整 URL，而 `host` 是从 URL 中提取的主机名。例如，当 Web 浏览器检测到对网页的请求时，它调用该函数：

```javascript
ret = FindProxyForURL("http://www. evoknow.com/index.html", "www.evoknow.com");
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_311_1.png)

> 函数调用中的 host 参数实际上是 `://` 和第一个 `:` 或 `/` 之间的子串。端口号不包含在此参数中。

该函数必须返回一个字符串，其中包含特定 URL 请求所需的代理配置。表 10-1 展示了表示代理配置的可接受字符串值。

**表 10-1 代理配置的可接受字符串值**

| 字符串 | 含义 |
| :--- | :--- |
| NULL | 当返回 NULL 值（不是字符串 NULL）时，它告诉浏览器不要使用任何代理来处理此请求。 |
| DIRECT | 应直接建立连接，不使用任何代理。 |
| PROXY host:port; | 应使用指定的代理。 |
| SOCKS host:port; | 应使用指定的 SOCKS 服务器。 |

### 设置 FindProxyForURL 的返回值

如表 10-1 所述，有四种潜在的返回值。显然，真正有趣的返回值是 DIRECT 和 PROXY。当你有多个代理或 SOCKS 服务器时，你可以返回一个列表，而不是单个 host:port 对。例如，以下代理配置：

```
PROXY best-proxy.evoknow.com:8080; PROXY good-proxy.evoknow.com:8081; PROXY soso-proxy.evoknow.com:8082
```

告诉浏览器先尝试 `best-proxy.evoknow.com`，如果失败，则尝试下一个（`good-proxy.evoknow.com`），以此类推。请注意，每个 host:port 对由分号分隔，并且关键字 PROXY 在每个对之前重复。如果所有代理服务器都失败，在尝试直接连接之前会询问用户。

当所有代理都失败且未指定 DIRECT 选项时，浏览器会询问用户是否应暂时忽略代理并尝试直接连接。

为了避免用户交互，可以用以下内容替换该配置：

```
PROXY best-proxy.evoknow.com:8080; PROXY good-proxy.evoknow.com:8081; PROXY soso-proxy.evoknow.com:8082; DIRECT
```

由于直接连接已指定为最后手段，如果在代理完全失败的情况下，用户将不会被询问是否建立此类连接。你也可以混合使用 PROXY 和 SOCKS。例如：

```
PROXY best-proxy.evoknow.com:8080; SOCKS socks4.evoknow.com:1080; DIRECT
```

在这里，当主代理服务器 `best-proxy.evoknow.com` 未响应时，将使用基于 SOCKS 的代理。

当代理未响应时，Web 浏览器会在 30 分钟后重试该代理。每次后续失败，间隔都会延长 30 分钟。

### 在 FindProxyForURL 中使用预定义函数

为了帮助 Web 管理员（他们必须也懂得 JavaScript 编程），提供了一组预定义函数。这些函数及其描述列在表 10-2 中。

| 函数名 | 说明 | 示例 |
| :--- | :--- | :--- |
| `isPlainHostName( host )` | 如果主机中没有点，则返回 true。换句话说，如果未包含域名。 | `isPlainHostName( "blackhole" )` 返回 true。 <br>`isPlainHostName( "blackhole.evoknow.com" )` 返回 `false`。 |
| `DnsDomainIs( host, domain )` | 如果主机属于该域，则返回 true。注意，域名必须包含前导点。 | `dnsDomainIs( "www.evoknow.com", ".evoknow.com" )` 返回 true。 <br>`dnsDomainIs( "www.apache.org", ".evoknow.com" )` 返回 `false`。 |
| `localHostOrDomainIs( host, fqdnhost )` | 如果 `fqdnhost`（完全限定主机名）的主机部分与 host 匹配，则返回 true。 | `localHostOrDomainIs( "a.b.com", "a.b.com" )` 返回 true。 <br>`localHostOrDomainIs( "a.b", "a.b.com" )` 返回 true。 <br>`localHostOrDomainIs( "a.b.org", "a.c.com" )` 返回 `false`。 |




## 表 10-2（续）

| 函数名称 | 说明 | 示例 |
|---|---|---|
| `isResolvable(host)` | 如果 DNS 服务器能够将主机名解析为 IP 地址，则返回 `true`；否则，返回 `false`。使用此功能可能会减慢浏览器的速度，因为执行测试需要发出 DNS 查询。 | `isResolvable("hyperlink")` 返回 `true`（因为 `[hyperlink]` 拥有 DNS 记录）。 |
| `isInNet(host, IP address pattern, netmask)` | 如果主机的 IP 地址与第二个参数中指定的模式匹配，则返回 `true`。匹配操作使用子网掩码进行，规则如下：如果掩码的某组八位组为 `255`，则主机 IP 地址的同一组八位组必须匹配。如果掩码的某组八位组为 `0`，则忽略主机 IP 地址的同一组八位组。使用此功能可能会减慢浏览器的速度，因为执行测试需要发出 DNS 查询。 | 如果主机的 IP 地址为 `206.171.50.51`，`isInNet(host, "206.171.50.50", "255.255.255.0")` 返回 `true`，因为根据子网掩码，仅前三个八位组必须匹配，最后一个八位组应被忽略。 |
| `dnsResolve(host)` | 如果成功，返回主机的 IP 地址。请注意，使用此功能可能会减慢浏览器的速度，因为执行测试需要发出 DNS 查询。 | `dnsResolve("proxy.evoknow.com")` 返回 `"206.171.50.50"`。 |
| `myIpAddress()` | 返回运行 Web 浏览器的主机的 IP 地址。使用此功能可能会减慢浏览器的速度，因为执行测试需要发出 DNS 查询。 | `var hostIP = myIpAddress()` 返回 Web 浏览器主机的 IP 地址并将其存储在一个名为 `hostIP` 的变量中。 |
| `dnsDomainLevels(host)` | 返回主机名中的域名层级数。 | `dnsDomainLevels("www.nitec.com")` 返回 `2`。 |
| `shExpMatch(string, shellExpression)` | 如果 `string` 匹配 `shellExpression`，则返回 `true`。 | `shExpMatch("path/to/dir", "*/to/*")` 返回 **true**。<br><br>`shExpMatch("abcdef", "123*")` 返回 **false**。 |
| `weekdayRange(weekday1, weekday2, gmt)` | 仅第一个参数 `weekday1` 是必需的。如果执行此函数的当天等于 `weekday1` 或在 `weekday1` 到 `weekday2` 的范围内，则返回 `true`。如果第三个参数 `gmt` 为 GMT，则使用 GMT 时间代替本地时间。`weekday1` 或 `weekday2` 可接受的星期值为 SUN, MON, TUE, WED, THU, FRI 或 SAT。 | `weekdayRange("FRI")` 如果本地时间的当天是星期五，则返回 `true`。<br><br>`weekdayRange("MON", "FRI", "GMT")` 如果 GMT 时间的当天在周一到周五的范围内，则返回 `true`。 |
| `dateRange(day)`<br>`dateRange(day1, day2)`<br>`dateRange(month)`<br>`dateRange(month1, month2)`<br>`dateRange(year)`<br>`dateRange(year1, year2)`<br>`dateRange(day1, month1, day2, month2)`<br>`dateRange(month1, year1, month2, year2)`<br>`dateRange(day1, month1, year1, day2, month2, year2, gmt)` | 如果当前日、月、年或三者均在指定范围内，则返回 `true`。`day` 的值可以是 1-31；`month` 可以是 JAN, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV 或 DEC；`year` 是一个四位数；`gmt` 是 “GMT” 或留空（表示本地时间）。 | `dateRange(31)` 如果当前日期是 31 号，则返回 **true**。<br><br>`dateRange("JAN", "APR")` 如果当前月份在 1 月到 4 月的范围内，则返回 `true`。<br><br>`dateRange(1995)` 如果当前年份是 1995 年，则返回 **true**。 |
| `timeRange(hour)`<br>`timeRange(hour1, hour2)`<br>`timeRange(hour1, min1, hour2, min2)`<br>`timeRange(hour1, min1, sec1, hour2, min2, sec2)`<br>`timeRange(hour1, min1, sec1, hour2, min2, sec2, gmt)` | 如果指定的 **小时、分钟** 或 **秒** 为当前时间单位，则返回 **true**。如果指定了一个范围，则当当前对应的时间单位在指定范围内时，返回 **true**。`hour` 的值可以是 0-23；`min` 可以是 0-59；`second` 可以是 0-59；`gmt` 是 "**GMT**" 或留空（表示本地时间）。 | `timeRange(9, 17)` 如果当前时间在上午 9 点到下午 5 点之间，则返回 **true**。 |

借助预定义函数和你的自定义函数，你可以编写 `FindProxyForURL`，使其为每个请求返回适当的代理配置字符串。

以下是一些示例场景，在这些场景中，`FindProxyForURL` 函数可以以不同的方式编写。

### 场景 1：仅为远程 URL 请求使用代理

在此场景中，想法是告知 Web 浏览器，代理应仅用于远程 URL 请求，如图 10-7 所示。这里，来自主机 **A** 对 `http://www.microsoft.com` 的请求由 `FindProxyForURL()` 方法评估，该方法返回 `proxy.nitec.com:8080` 作为代理服务器，并指示如果代理宕机则尝试直接访问。同样，主机 **B** 上的 Web 浏览器使用 `FindProxyForURL()` 方法来评估如何访问 `http://www.nitec.com`。图示表明 `FindProxyForURL()` 方法指示浏览器直接访问该网站。

列表 10-1 是一个这样的 `FindProxyForURL` 函数的简单示例。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_317_0.png)

**图 10-7：** 仅为远程 URL 请求使用代理

### 列表 10-1：仅为远程 URL 请求使用代理

```javascript
function FindProxyForURL(url, host) {
    // 检查主机是否为本地主机。
    // 如果是本地
    // 主机，指定 DIRECT 连接（即，不使用代理）
    // 否则使用代理。

    if (isPlainHostName(host) || dnsDomainIs(host, ".nitec.com")) {
        return "DIRECT";
    }

    else {
        return "PROXY proxy.nitec.com:8081; DIRECT";
    }
}
```

当 Web 浏览器用户发出对 URL `http://www.domain.com` 的请求时，浏览器调用 `FindProxyForURL`，其中 `url` 参数设置为 `http://www.domain.com`，`host` 设置为 `www.domain.com`。该函数首先调用 `isPlainHostName` 函数，以查看请求是否针对普通主机（仅 www）。因为不是，`isPlainHostName` 返回 `false`。现在调用 `dnsDomainIs` 函数来测试是否属于 `.nitec.com` 域。这也返回 `false`。由于这两个测试都返回 `false`，条件语句的 `else` 部分被执行。换句话说，对 `http://www.domain.com` 的 URL 请求向 Web 浏览器返回以下代理配置：

```
PROXY proxy.nitec.com:8081; DIRECT
```

这告诉 Web 浏览器，如果名为 `proxy.nitec.com` 的代理服务器在端口 `8081` 上未宕机，则使用该代理服务器。如果宕机，请求应由直接 HTTP 请求到 `http://www.domain.com` 来处理。对于大多数代理服务器安装，这种配置就足够了。让我们来看一下更复杂的场景。

### 场景 2：使用多个代理服务器

在此场景中，存在多个代理服务器。图 10-8 说明了一个网络，其中有三个代理服务器：`http-proxy.nitec.com` 用于所有远程 HTTP URL 请求；`ftp-proxy.nitec.com` 用于所有远程 FTP URL 请求；`ssl-proxy.nitec.com` 用于所有远程 HTTPS URL 请求。所有其他使用 Gopher、News 等协议的远程 URL 请求均直接连接。所有类型的本地请求也直接处理。

为了实现此配置，`FindProxyForURL` 变得稍微复杂，外观类似于列表 10-2。

该函数首先检查 URL 请求是否为本地请求。如果是本地的，则直接处理。如果请求针对远程服务器，则匹配 URL 协议以定位适当的代理服务器。但是，仅识别 HTTP、FTP 和 HTTPS 协议，并使用这些协议请求远程资源的 URL 会被引导至代理服务器。当远程 URL 请求不匹配上述任何协议时，它将直接连接。

### 场景 3：使用 CGI 脚本动态生成 FindProxyForURL

也可以根据访问代理服务器的主机来自定义代理服务器配置。这可以通过 CGI 脚本实现，该脚本根据 `REMOTE_HOST`（浏览器主机）不同输出不同的 `FindProxyForURL`。列表 10-3 显示了一个这样的用 Perl 编写的脚本，`proxy.pl`。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_318_0.png)





![](img/e11fcbd2818a3495ac70085e5d8d1c26_319_0.png)

**图 10-8：**使用多个代理服务器

### 列表 10-2：用于多代理服务器配置的 FindProxyForURL

```javascript
function FindProxyForURL(url, host) {
    //
    // Is the URL local? If it is, then use a
    // DIRECT connection
    //
    if (isPlainHostName(host) ||
        dnsDomainIs(host, ".nitec.com")) {
        return "DIRECT";
    } else {
        // OK, the URL is remote so check which proxy to use.
        if (url.substring(0, 5) == "http:") {
            return "PROXY http-proxy.nitec.com:8080";
        } else if (url.substring(0, 4) == "ftp:") {
            return "PROXY ftp-proxy.nitec.com:8080";
        } else if (url.substring(0, 6) == "https:") {
            return "PROXY ssl-proxy.nitec.com:8080";
        } else {
            return "DIRECT";
        }
    }
}
```

### 列表 10-3：proxy.pl

```perl
#!/usr/bin/perl
#
# A Perl script that outputs proxy server configuration.
# $Author$
# $Revision$
# $Id$

# Get the remote host IP from the CGI environment variable
# REMOTE_HOST
my $client = $ENV[REMOTE_HOST];

# Print out the necessary content-type to let the browser know that this is a proxy configuration.
print "Content-type: application/x-ns-proxy-autoconfig\n\n";

# If the request came from a host with IP address
# 206.171.50.51 then output proxy configuration from subroutine &specialClient
# 
if ($client =~ /206\.171\.50\.51/){

    &specialClient;
} else {

    # If the request came from any other clients, then
    # send proxy configuration for all other clients
    &otherClients;
}

exit 0;

sub specialClient{
#
# This subroutine outputs a proxy server configuration
#
    print <<FUNC;

        function FindProxyForURL(url, host)
        {
            if (isPlainHostName(host) ||
               dnsDomainIs(host, "*.nitec.com"))
               return "DIRECT";
            else if (shExpMatch(host, "*.com"))
               return "PROXY com-proxy.nitec.com:8080; "
            else if (shExpMatch(host, "*.edu"))
               return "PROXY edu-proxy.nitec.com:8080; "
            else
               return "DIRECT";
        }
    FUNC
}

sub otherClients{
#
# This subroutine outputs a proxy server configuration
#
    print <<FUNC;

        function FindProxyForURL(url, host)
        {
            return "DIRECT";
        }
    FUNC
}
```

此脚本为 IP 地址为 206.171.50.51 的主机输出特殊的代理服务器配置；所有其他主机都会获得不同的配置。要访问此代理配置，我可以将 Netscape Navigator 或 IE 设置为指向位于 `http://www.nitec.com/cgi-bin/proxy.pl` 的此脚本。例如，在 IE 中，你可以将上述 URL 之类的地址指定为“工具”→“Internet 选项”→“连接”→“局域网设置”→“使用自动配置脚本”选项中的自动代理配置脚本地址，只是你是在要求浏览器请求一个 CGI 脚本，而不是一个 .pac 文件。但由于该脚本发送了 .pac 文件的内容类型，浏览器不会质疑为什么它从 CGI 脚本而不是 .pac 文件获取代理配置。虽然示例脚本功能不多，但你可以使用类似的脚本进行复杂的代理配置。

✦ ✦ ✦

# 第 11 章

## 运行完美的网站

到现在为止，你很可能已经在新的 Apache Web 服务器上运行了一个或多个网站。你组织中的每个人都在称赞你做得很棒。你正处于 Web 的天堂，对吗？错！很快，你的许多同事可能会问你如何更新他们在网站上的页面。例如，市场部可能会打电话来询问如何更新价格信息，或者法务部可能会询问如何在其中一个网站中添加更多的法律内容。

这就是中大型组织的 Web 管理员所面临的情况。这些管理员很快发现自己处于大量更新请求和愿望清单的中心。那么，你现在该如何管理你的 Web？在本章中，你将学习如何创建一个专业的 Web 管理环境，使你和你的 Web 开发者保持理智并与 Web 保持同步。

本章讨论与开发完美网站相关的各种问题。一个完美的网站表现出以下特征：

- 高质量的内容——当然！如果你没有有用的或娱乐性的内容，人们为什么要访问你的网站？然而，什么内容适合你取决于网站的目的。
- 一致的外观和感觉——在整个所有页面中拥有一致主题的网站更具吸引力，并且通常表明经过深思熟虑的过程。创建一致的外观和感觉需要工具和系统化的流程。本章向你介绍一种称为 Web 周期的流程，该流程要求你使用三个阶段（开发、暂存和生产）来管理你的网站。

# 本章内容

- 为你的组织创建 Web 周期
- 通过使用 makepage 生成基于模板的网站
- 通过使用 HTTP PUT 方法在内网上发布
- 标准化你的标准
- 使你的 Web 用户友好
- 在互联网上推广你的网站
- 自动化发布——我的经验是，不断开发新且令人兴奋的内容本身就是一个巨大的挑战。如果你将手动内容展示任务添加到流程中，事情很快就会失控。例如，如果你有三位内容作者正在为网站编写实际的 HTML 页面，你们可能会从对共同外观和感觉的理解开始，但随着时间的推移会逐渐偏离它。为了执行严格的展示规则，你必须使用 HTML 模板并通过自动化流程整合内容。本章讨论了几个这样的流程。
- 遵循标准实践——为了保持网站的用户友好性，有许多需要遵循的指导原则。我在本章中讨论了一些更重要的指导原则。

## 什么是 Web 开发周期？

不幸的是，典型的 Web 开发项目并不是从设计可管理的 Web 开始的。在大多数项目中，大部分时间都花在让服务器运行和开发内容上；很少有时间去担心 Web 的长期管理方面的问题。讽刺的是，一旦所有看似正常运行，由于缺乏清晰、可维护的周期，事情开始分崩离析。在这一节中，你将了解 Web 周期，它使你能创建一个高度可管理的 Web 解决方案。

Web 周期由三个阶段组成：开发、暂存和生产。通过实施每个阶段，你可以创建一个可维护、可管理的 Web。图 11-1 显示了 Web 周期的高级示意图。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_324_0.png)

如该图所示，Web 周期从开发阶段开始，继续到暂存阶段，并在生产阶段结束。然而，当周期重新启动时，它从生产阶段开始并重复之前的周期路径。周期中的阶段是：

1. **开发阶段**——在这个阶段，你开始开发你的 Web 内容。内容，无论是 HTML 文档还是 CGI 脚本或其他东西，都在这个阶段完全开发和测试。当开发人员完全确定他们的工作准备好与网站集成时，新开发的内容将进入下一个阶段。
2. **暂存阶段**——暂存阶段允许将新开发的内容与现有内容集成，并允许执行测试循环。一旦进入暂存阶段，开发人员不再参与暂存过程。在这个过程中，你引入了非开发人员的测试人员，以消除开发人员的偏见——换句话说，开发人员可能由于过度自信内容被正确编写而不会完全测试内容。此时，你要么发现问题，要么最终成功完成一系列测试。在后一种情况下，你准备好将新开发的、经过暂存和测试的内容移动到生产阶段。如果新内容引起问题，你需要在开发人员在开发区域修复问题后，从开发阶段重新开始。不允许开发人员修复暂存区域中的问题。
3. **生产阶段**——这个阶段包括内容备份和内容部署任务。首先，你备份现有的（功能正常的）内容，然后将暂存内容移动到你的生产 Web 空间。切换必须尽可能快速进行，以减少访问者的中断并防止丢失 Web 收集的数据。

当你准备好开始另一个开发周期（重新启动整个流程）时，将生产阶段的内容复制并在开发阶段中提供，以便开发人员可以对其进行处理。每当需要时，周期以相同的方式继续。

这一切给你带来了什么？它为你带来了可靠性和管理选项。例如，如果你目前正在开发内容并在完整测试套件之前直接将其倾泻到生产系统中，你正在冒险。在大多数情况下，内容开发人员声称已在他们的本地环境中测试了新内容，并迅速贴上完成的标签。由于开发人员的本地环境通常缺乏当前内容与新内容的集成，测试并不总是现实的。只有通过将现有和新内容集成在一起，你才能检测到潜在的不兼容性。例如，如果没有暂存阶段，从开发阶段直接倾泻到生产系统可能会导致以下任一错误：


生产系统中的文件可能会被新内容覆盖。这种情况通常发生在图像文件上，原因可能是缺乏标准的文件命名规范，或者是因为使用了常见的图像文件目录。

实时（生产）系统上的数据文件可能会被覆盖，因为 CGI 开发者在开发内容时使用了旧的数据文件。

当涉及多名开发者时，由于每位开发者可能在不同时间点开始基于副本工作，一些旧文件可能会重新出现在生产服务器上。一位开发者提交了他的副本，然后另一位开发者提交了她的副本，结果往往是一团混乱。

如果有多名开发者参与且他们的项目相互关联，可能会出现许多其他问题。如果你无法承担生产服务器出现此类问题的风险，就需要引入预发布（staging）阶段。Apache 可以帮助你实现这些阶段。

当你习惯了这种循环流程后，你会发现它使跟踪开发和集成问题变得容易，同时也确保你的所有生产站点始终处于可用状态。

## 付诸实施 Web 循环

你已经准备好将你的 Web 循环付诸实施了。理想情况下，你并不希望在生产服务器系统上进行任何开发工作。然而，如果你的预算不允许部署多台机器用于 Web，你仍应使用你唯一的服务器来实现这个循环。

首先，你需要为你的 Web 循环设置服务器。虽然有很多方法可以做到这一点，但我仅讨论以下三种方法。以下是这三种方法的简要说明。

- 一台计算机，带有两个虚拟主机，分别用于开发和预发布。生产服务器是主 Apache 服务器。在此配置中修改任何 Apache 配置时要格外小心，因为更改可能会影响生产服务器的行为。
- 一台计算机，带有三个主 Apache 服务器，分别用于开发、预发布和生产。使用这种方法，你会为每个（主）Apache 服务器创建独立的配置，这样你就可以在开发站点中试验 Apache 配置，而不会干扰生产配置。
- 至少三台不同的计算机，分别作为开发、预发布和生产 Apache 服务器。这三台计算机都在端口 80 上运行 Apache 服务器。

## 设置 Web 循环

你可以通过两种方式设置 Web 循环：你可以使用两个新的虚拟主机在生产服务器上实现开发和预发布站点，或者你可以为生产服务器、开发服务器和预发布服务器创建三个独立的 Apache 配置。

如果你的开发工作包括调整 Apache 配置文件或测试新发布的 Apache 服务器，你应该为生产 Apache 服务器和其他两个 Apache 服务器使用独立的配置文件。然而，如果你的常规 Web 开发不包括与 Apache 相关的变更，你可以使用虚拟主机方法。

良好的 Web 循环需要精心规划的 Web 目录结构。图 11-2 展示了一个用于 Web 循环的目录结构示例。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_327_0.png)

**图 11-2：** 用于“my company”公共、预发布和开发站点的目录结构

该图展示了一个良好的目录结构示例，因为它允许你将每个 Web 站点的公共、预发布和开发站点保存在一个单一的一级目录下（在本例中为 mycompany）。添加新的 Web 站点意味着为其创建类似的目录结构。

在后续章节讨论的示例配置中，我假设你已建立了上述目录结构。我还假设你的 Web 服务器主机名为 `www.mycompany.com`，且其 IP 地址为 `206.171.50.50`。请确保将这些值替换为适合你自己配置的值。

## 为每个阶段创建虚拟主机

如果你计划在开发过程中修改 Apache 配置文件，请勿使用此方案；在此配置中你只需一套 Apache 配置文件，并且出于实验目的更改文件可能会影响你的生产服务器。在这种情况下，你仍然可以使用单台机器，但需要运行多个 Apache（主）服务器。这种方法将在下一节中描述。

如果你决定不需要对配置文件进行与 Apache 相关的更改，你可以使用此方案为每个阶段创建虚拟主机。为此，你应该创建两个具有相同 ServerName 但运行在不同端口地址上的虚拟主机。表 11-1 展示了此类设置的示例端口分配。

**表 11-1**
**Web 循环中 Apache 服务器的端口分配**

| 端口 | 服务器类型 |
|:-----|:------------|
| 80 | 生产服务器（主服务器） |
| 1080 | 预发布服务器（虚拟主机） |
| 8080 | 开发服务器（虚拟主机） |

你可以选择任何其他端口分配，只要你不使用已被占用的端口地址或大于 65535 的端口即可。生产服务器端口不应从 80 更改，因为默认的 HTTP 请求是发送到该端口地址的。

要按照表 11-1 中所示的端口分配创建这些虚拟主机，你需要编辑 Apache 服务器的 `httpd.conf` 文件，操作如下。

- 1. 为了让 Apache 服务器监听这些端口，使用 `Listen` 指令：

```
Listen 80  
Listen 1080  
Listen 8080
```

- 2. 按以下方式创建两个虚拟主机：

```
# Do not forget to change the IP address, ServerName, 
# DocumentRoot, ScriptAlias,
# TransferLog, and ErrorLog directive values with whatever is
# appropriate for your
# actual configuration setup.
<VirtualHost 206.171.50.5:1080>
ServerName www.mycompany.com
DocumentRoot "www/mycompany/staging/htdocs"
ScriptAlias /cgi-bin/ "/www/mycompany/staging/cgi-bin/"
TransferLog logs/staging-server.access.log
ErrorLog logs/staging-server.error.log
</VirtualHost>

<VirtualHost 206.171.50.5:8080>
ServerName www.mycompany.com
DocumentRoot "www/mycompany/developer/htdocs"
ScriptAlias /cgi-bin/ "/www/mycompany/developer/cgi-bin/"
TransferLog logs/developer-server.access.log
ErrorLog logs/developer-server.error.log
</VirtualHost>
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_329_0.png)

在上面的示例中，两个虚拟主机使用了相同的 IP 地址，但在 <VirtualHost . . . > 容器中指定了不同的端口。该 IP 地址与主服务器相同，即 www.mycompany.com。ServerName 指令也设置为主服务器名称。你的主服务器配置将保持常规状态。

可以使用 http://www.mycompany.com:1080 URL 访问预发布站点；要访问开发站点，可以使用此 URL：http://www.mycompany.com:8080。

## 使用多个 Apache（主）服务器进程

如果你计划在 Web 开发阶段试验 Apache 本身，你应该使用多于一个（主）服务器进程。创建三套配置文件，每套指向不同的 DocumentRoot 和 ScriptAlias。完成此操作后，你可以从安装 Apache 的主目录（例如 /usr/local/apache）按以下方式启动三个 Apache（主）服务器进程：

```
httpd -f conf/httpd.conf
httpd -f conf/staging/httpd.conf
httpd -f conf/developer/httpd.conf
```

当你决定编译新版本 Apache 并在开发服务器下运行时，你可以简单地传入开发服务器的配置文件。例如，如果你决定添加一个新模块并希望查看该模块对内容的影响，你可以简单地使用该可执行文件运行开发和预发布服务器，而不是生产服务器可执行文件（httpd）。在编译新的可执行文件后，你可能想将其重命名为类似 httpd_xx80 的名称，以确保不会意外地用它覆盖生产服务器可执行文件。

要实施此循环，请遵循以下说明。

- 1. 在你的 Apache 配置目录中创建两个分别名为 `staging` 和 `developer` 的子目录，操作如下：

```
mkdir /path/to/Apache/server/root/conf/staging
mkdir /path/to/Apache/server/root/conf/developer
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_330_0.png)

> 别忘了将 `/path/to/Apache/server/root/conf` 替换为你服务器配置目录的实际路径。

- 2. 将所有 `*.conf` 文件复制到 `staging` 和 `developer` 子目录中，操作如下：

```
cp /path/to/Apache/server/root/conf/*.conf /path/to/Apache/server/root/conf/staging/
cp /path/to/Apache/server/root/conf/*.conf /path/to/Apache/server/root/conf/developer/
```

- 3. 修改 `staging` 子目录中的 `httpd.conf` 文件，使其监听端口 1080 而不是默认的 80。你可以使用 `Port` 或 `Listen` 指令来做到这一点。类似地，你需要修改 `developer` 子目录中的 `httpd.conf`，使 `Port` 或 `Listen` 指令设置为 8080。

- 4. 修改 `staging` 和 `developer` 子目录中的 `srm.conf`（或 `httpd.conf`）文件，使它们的 `DocumentRoot` 和 `ScriptAlias` 指令指向适当的路径。例如，针对图 11-2 所示的目录结构，此处所需的更改为：

```
DocumentRoot   "www/mycompany/staging/htdocs"
ScriptAlias    "/cgi-bin/" "www/mycompany/staging/cgi-bin/"
```

用于预发布站点配置。对于开发站点配置文件，它是：

```
DocumentRoot   "www/mycompany/developer/htdocs"
ScriptAlias    "/cgi-bin/" "www/mycompany/developer/cgi-bin/"
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_330_1.png)

> 如果你的生产服务器使用了包含绝对路径信息的特殊配置，你可能需要进一步编辑 `staging` 和 `developer` 子目录中的新配置文件。

## 使用多台 Apache 服务器计算机进行 Web 循环

如果你能够负担多台 Apache 服务器计算机（即一台用于开发，一台用于预发布，一台用于生产）来创建 Web 循环环境，那么你就无需创建特殊的 Apache 配置。你只需在所有相关主机上安装 Apache，并将一台主机视为开发站点主机，第二台主机视为预发布站点主机，第三台主机视为生产站点。由于你现在有三台不同主机上运行着 Apache 服务器，你


也可以在 80 端口上运行每个服务器。这就是为多主机 Web 周期环境所做的一切。

## 实现 Web 周期

为了启动你的 Web 周期，请从生产服务器的文档根目录将生产内容复制到你的开发站点。例如，如果你的配置是上述列表中的前两种之一，你可以轻松使用以下 Unix 命令将整个 Web 内容复制到开发站点：

```
cd /path/to/production/docroot/dir
tar cvf - . | ( cd /path/to/development/site/docroot/dir ;
tar xvf - )
```

这将把生产服务器中的所有文件和目录复制到开发站点的文档根目录。只需确保将路径信息更改为适合你系统的内容即可。

对于多计算机 Web 周期环境，你可以为生产服务器创建 tar 归档，并通过 FTP 将其复制到开发站点。

设置文件权限，以便 Apache 能够读取所有文件并执行 CGI 脚本。如果你有需要 Apache 具有写权限的目录（用于写入数据的 CGI 脚本），你也应该设置这些权限。完成后，启动或重启 Apache 以服务于开发站点。

现在，确保开发站点（通过 Web 浏览器）与生产站点完全相同。进行一些手动比较和抽查。确保脚本也能正常工作。

如果你的任何 CGI 脚本为你的生产服务器生成了硬编码的 URL，它们也会为你的开发站点这样做。你可以忽略这些 URL，或者修复它们使其使用 `SERVER_NAME` 环境变量的和 `SERVER_PORT` 端口地址。

## 测试 Web 周期

当一切如预期般工作时，你就成功创建了一个 Web 周期环境。现在你可以让开发人员将新内容和脚本放入开发站点并进行测试。每当新内容开发完成时，你首先应该在开发区域进行测试。测试应关注以下问题：

- 它是否实现了其目的？换句话说，新内容提供的功能是否满足你的规范？
- 新内容是否有任何副作用？例如，如果新内容实际上是一个新的 CGI 脚本，你应该使用 Apache 的脚本调试支持来监控脚本的工作方式。

## 将新站点移至生产服务器

在你满意测试结果后，避免通过停止对新内容的进一步开发而无需执行另一组功能测试。当生产站点更新时，制作你生产站点的副本并将其放置在你的预发布站点上。以下是这样做的建议：

- 确保预发布站点与生产站点完全相同。在执行手动检查以确保一切看起来和感觉相同之后，你可以将新内容和脚本移动到预发布站点并进行集成。
- 一次移动一个项目，以便你可以分阶段发现和解决问题。例如，如果你向开发系统添加了三个新的 CGI 脚本，请一次移动一个脚本到预发布区域。执行功能测试和站点集成测试。如果脚本通过测试，请将下一个新脚本移动到预发布区域。在你移动所有新内容之后，你可以执行站点级集成测试。仔细监控你的预发布站点日志。你是否注意到错误日志中有任何异常？如果没有，那么你就准备好对生产站点进行更新了。然而，你必须非常小心。例如，如果你在 production 服务器上有创建生产区域数据文件的 CGI 脚本，你不想用预发布区域中的数据文件覆盖这些文件。
- 更新生产站点的最佳时间是当你预计生产服务器最闲的时候。此时，你可以从生产服务器获取数据文件并将其应用于站点预发布版本的相应目录。这样可以将你的预发布站点与生产站点同步。此时，你必须快速将预发布站点转储到生产区域。这可能非常棘手，因为生产站点是实时的，你永远不知道何时会有访客访问页面或使用需要读取或写入数据文件的 CGI 脚本。

为了最小化切换时间（至少在单服务器设置中），你可以创建一个执行以下操作的 shell 脚本：

1. 将所有实时数据文件复制到预发布站点的相应区域。
2. 将你的顶层生产目录（如图 11-2 中的 public 目录）重命名为类似 `public.old` 的名称。
3. 将你的顶层预发布目录（如图 11-2 中的 staging 目录）重命名为你之前称为顶层生产目录的名称——例如，`public`。
4. 将旧的生产目录（如 public.old）重命名为你之前称为预发布顶层目录的名称——例如，`staging`。

这样，预发布站点只需几步即可成为生产站点，而不需要进行大量的文件复制操作。对应于图 11-2 所示环境的此类脚本示例见列表 11-1。

## 列表 11-1：**stage2production.sh** 脚本

```
#!/bin/sh
# Purpose: a simple shell script to copy live data files
# to staging area and to rename the staging area into a live
# production site. It also renames the old production
# area into a staging area.
#
# Copyright (c) 2001 Mohammed J. Kabir
# License: GNU Public License

# You will need to change these variables to use this script.
DATA_FILES="/www/mycompany/public/htdocs/cgi-data/*.dat";
TEMP_DIR="/www/mycompany/public.old";
PRODUCTION_DIR="/www/mycompany/public";
STAGE_DIR="/www/mycompany/staging";

# Copy the live data to the staging directory.
/bin/cp $DATA_FILES $STAGE_DIR

# Temporarily rename current production directory to TEMP_DIR
/bin/mv $PRODUCTION_DIR $TEMP_DIR

# Rename the current staging site to
# production directory
/bin/mv $STAGE_DIR $PRODUCTION_DIR

# Rename the temporary (old) production directory
# to staging directory
/bin/mv $TEMP_DIR $STAGE_DIR

# To be safe, change the current production directory's
# permission setting so that the Apache user (httpd)
# and Apache group (httpd) can read all files.
# If you use some other user and group for Apache, you
# have to modify this command according to
# your setup.

/bin/chown -R httpd:httpd $PRODUCTION_DIR

# Change the file permission so that the owner
# (httpd in this case) has read, write, and
# execute permission, the group (httpd in this case)
# has read and execute permission, and everyone no
# one else has permission to see the production
# directory files

/bin/chmod -R 750 $PRODUCTION_DIR
```

运行此脚本后，你应该进行一次快速检查，以确保一切正常。如果出现问题，你可以将当前生产目录重命名为其他名称，并将预发布目录名称改回你的生产目录名称，以恢复你上次的生产站点。

## 使用模板和 makepage 构建网站

维持严格的 Web 周期为你提供了一套可重复的流程来发布优秀的网站。然而，你仍然需要一个高度自动化且几乎不需要人工干预的内容呈现流程。

许多昂贵的软件程序声称有助于这一流程。有些人使用 Microsoft Front Page 来管理内容开发；有些人使用 Dreamweaver；有些人使用其他产品。有些人使用 Web 开发公司提供的方法，这些方法可能需要数十万美元。以下是我认为有效（并且多年来一直有效）的解决方案，用于维护从几页到几百页不等规模的网站。此解决方案的要求是：

- 创建一种简单机制，使内容作者能够发布具有统一外观和感觉的 Web 页面。
- 尽可能减少内容作者的工作量，使大部分工作自动化。
- 假设内容开发者对 HTML 知之甚少，并希望以文本格式提交内容。

为了实现这种解决方案，我编写了 *makepage*，这是一个包含在此书 CD-ROM 上的脚本。该脚本使用一组 HTML 模板和一个正文（内容）页面来构建网站上的每个页面。当我开始这个项目时，我希望通过使用 CGI 或 mod_perl 实时生成每个页面，但后来我决定每天生成一次内容，因为我的站点每天只更新一到两次。然而，正如你将在本节中了解到的，增加更新频率非常容易。*makepage* 脚本假设每个页面由以下部分组成：

- 左侧导航栏
- 右侧导航栏
- 底部导航菜单
- 容纳页面内容的主体区域

每当在给定目录上运行 *makepage* 脚本时，它会查找所有以 .txt 扩展名结尾的文件，并创建相应的 .html 页面。例如，如果你在包含名为 *index.txt* 的文本文件的目录中运行 *makepage* 脚本，该脚本将运行并产生类似以下的输出：





## 使用 HTTP PUT 进行内网 Web 发布

脚本的输出显示它正在处理当前目录（用点字符表示）中的 index.txt 文件。然后它显示对于 index.html 使用的是哪个 RSB（右侧导航栏）模板文件。脚本首先查找名为 index-rsb.html 的 RSB 模板文件，如果找不到与该文本文件特定的 RSB 文件，它使用整个目录的默认 RSB 文件，碰巧是 default-rsb.html。它对选择 LSB（左侧导航栏）模板重复相同的流程。然后它将当前的 index.html（上次运行的输出）备份为 index.html.bak，并使用默认正文模板 default-tmpl.html 来创建 index.html 页面。如果它找到名为 index-tmpl.html 的正文模板，它使用该模板而不是目录的默认正文模板。这使你在设计每个 Web 页面时具有灵活性。你可以简单创建一个目录范围的模板集，使目录中的所有页面看起来相同。或者你可以定制目录中的单个页面，拥有其自己的 RSB、LSB 和 BODY 模板。

如果你使用命令 `makepage path_to_document_root` 在文档根目录中运行该脚本，脚本会自动在文档根下的所有子目录中创建页面。因此，你可以将此脚本设置为 cron 任务，每小时、每天、每周甚至每分钟运行一次，具体取决于你的更新需求。内容作者只需放下他们的文本文件，页面就会自动创建。当放入新的文本文件时，如果你未提供页面特定的 RSB、LSB 或 BODY 模板，页面将使用目录的默认模板创建，这使得添加新页面极其简单。只需在你喜欢的文本编辑器中编辑一个页面，并通过 FTP 将该文件传输到你 Web 站点的正确目录，它应该会在下一次通过 cron 运行的 makepage 中发布。

随附光盘上提供的 makepage 包包含默认模板，你可以研究它们来构建自己的模板。

Apache 支持 PUT 方法，它允许你发布 Web 页面。然而，如果实施不谨慎，此功能会带来重大的安全风险。毕竟，你并不希望允许任何人更改你的 Web 站点。我只建议将此功能用于无法从 Internet 访问的内网。

你需要 `mod_put` 模块，它实现了 HTTP 1.1 中的 `PUT` 和 `DELETE` 方法。`PUT` 方法允许你将内容上传到服务器，`DELETE` 方法允许你从服务器删除资源。你可以从 http://hppwww.ec-lyon.fr/~vincent/apache/mod_put.html 下载此模块。

### 理解 mod_put 模块中的指令

`mod_put` 模块提供三个指令来控制基于 `PUT` 和 `DELETE` 的发布。

#### EnablePut

`EnablePut` 启用或禁用 `PUT` 方法。要使用 `PUT` 方法，你必须通过将此指令设置为 `On` 来启用它。

-   **语法：** `EnablePut On|Off`
-   **默认设置：** `EnablePut Off`
-   **上下文：** Directory, location

#### EnableDelete

`EnableDelete On | Off` 启用或禁用 `DELETE` 方法，该方法允许你通过 HTTP 删除 Web 页面。要使用 `DELETE` 方法，你必须通过将此指令设置为 `On` 来启用它。

-   **语法：** `EnableDelete On | Off`
-   **默认值：** `EnableDelete Off`
-   **上下文：** Directory, location

#### umask

`umask octal_value` 为目录设置默认的权限掩码（即 `umask`）。`007` 的默认值确保目录中的每个文件都以 `770` 权限创建，这仅允许文件所有者和组读取、写入和执行该文件。

-   **语法：** `umask octal_value`
-   **默认值：** `umask octal_007`
-   **上下文：** Directory, location

### 编译和安装 mod_put

下载 `mod_put` 后，你需要执行以下步骤来编译和安装它：

1.  提取 `mod_put.tar.gz` 源文件，并将它创建的目录移动到 Apache 源发行版的 modules 子目录内。
2.  使用 `configure` 脚本（如果你之前已经编译过 Apache，则使用 `config.status`）将 `mod_put` 模块添加到 Apache 中。使用 `add --enable-module=put` 选项运行任一脚本。
3.  使用 `make && make install` 命令编译和安装 Apache。
4.  使用 `/usr/local/apache/bin/apachectl restart` 命令重启 Apache。

### 设置启用 PUT 的 Web 目录

Netscape、AOLPress 和 Amaya 等 Web 客户端可以通过 PUT 方法发布 Web 页面。本节教你如何设置 `httpd.conf` 以在文档根树下的单个 Web 目录中启用基于 PUT 的发布。

> **警告**
>
> 如果你计划在内网之外使用 PUT 方法，请非常小心。在 Internet 上可访问的 Web 站点上使用 PUT 可能会极大地增加你的安全风险，因为如果这里描述的基于 Web 的身份验证过程被攻破，某人可以毁坏你的 Web 站点。我只建议将 PUT 方法用于内部使用。

1.  在 `httpd.conf` 中创建以下配置：

```text
Alias location_alias
"physical_directory_under_document_root"

<Location location_alias>
    EnablePut On
    AuthType Basic
    AuthName "Name of the Web section"
    AuthUserFile path_to_user_password_file

    <Limit PUT>
        require valid-user
    </Limit>

</Location>
```

上述代码中发生了什么（要了解有关这些身份验证相关指令的更多信息，请阅读第 7 章）：

-   名为 `loc_alias` 的别名与名为 `physical_directory_under_document_root` 的物理路径关联。
-   `<Location>` 目录为此别名设置指令。
-   `EnablePut` 指令启用 `mod_put` 模块。
-   `AuthType` 指令将身份验证类型设置为 `Basic HTTP authentication`。
-   `AuthName` 指令为该部分设置标签。此标签显示在 Web 浏览器向用户显示的身份验证对话框中，因此务必确保此标签有意义。
-   `AuthUserFile` 指定用于对用户进行身份验证的用户密码文件。
-   `<Limit>` 容器为 `PUT` 方法设置限制。它告诉 Apache 当 Web 客户端提交 `PUT` 请求时要求有效用户。

以下是上述配置的一个示例：

```text
Alias  /publish/  "/www/mysite/htdocs/publish/"

<Location  /publish>
      EnablePut  On
      AuthType  Basic
      AuthName  "Web Publishing Section"
      AuthUserFile  /www/mysite/sects/.users
      <Limit  PUT>
          require  valid-user
      </Limit>
</Location>
```

在上面的示例中，物理目录 `/www/mysite/htdocs/publish` 为 `/www/mysite/secrets/.users` 文件中的所有用户启用了 `PUT` 方法。

2.  使用 `/usr/local/apache/bin/apachectl` restart 命令重启 Apache 服务器，并使用支持 PUT 的 Web 浏览器在 `http://your_web_server/loc_alias` 目录中发布文档。对于示例配置，此 URL 是 `http://server/publish`。

当使用 `PUT` 方法发布文件时，它将具有使用 `mod_put` 模块的 `umask` 指令设置的权限设置。该文件将由运行 Apache 的用户拥有。例如，如果你在 `httpd.conf` 中将 `User` 和 `Group` 指令设置为 `httpd`，则文件由用户 `httpd` 拥有，组所有权也由 `httpd` 拥有。





## 配置使用 mod_put 模块的虚拟主机

httpd.conf 中 User 指令设置的用户将拥有 mod_put 创建的文件的所有权。对于许多不同用户的网站，这是一个问题，因为现在每个人都可以通过使用 PUT 方法覆盖其他人的文件。你可以轻松通过为每个用户使用单独的虚拟主机来解决这个问题，如下所示。

1.  将以下行添加到 httpd.conf：

```
ChildPerUserID number_of_child_servers username1 groupname1
```

其中 username1 和 groupname1 是用于虚拟主机的用户和组。将这些名称更改为你实际使用的用户名和组名。根据需要创建任意数量的 ChildPerUserID 行。num_of_child_servers 是 Apache 用于启动与此虚拟主机相关的子进程的数量。例如，如果你有两个名为 carol 和 john 的用户，并希望为每个虚拟主机分配 10 个 Apache 子进程，则在 httpd.conf 中添加以下行：

```
ChildPerUserID 10 carol carol_group
ChildPerUserID 10 john john_group
```

确保这些用户和组分别实际存在于 /etc/passwd 和 /etc/group 中。

2.  为每个需要 PUT 发布功能的用户创建 VirtualHost，如下所示：

```
NameVirtualHost IP_Address
```

```
<VirtualHost IP_Address>
```

```
    ServerName vhost_domain_name
    AssignUserID user_name group_name
```

```
    Alias location_alias
    "physical_directory_under_document_root"
```

```
    <Location location_alias>
        EnablePut On
        AuthType Basic
        AuthName "Name_of_the_Web_section"
        AuthUserFile path_to_user_password_file
    <Limit PUT>
        require username
    </Limit>
```

```
</Location>
```

```
# 站点所需的其他指令
</VirtualHost>
```

示例：

```
NameVirtualHost 192.168.1.100

<VirtualHost 192.168.1.100>
  ServerName carol.domain.com
  AssignUserID carol carol_group
  DocumentRoot /www/intranet/htdocs/carol
  Alias /publish/ "/www/intranet/htdocs/carol/publish/"

  <Location /publish>
    EnablePut On
    AuthType Basic
    AuthName "Carol's Publishing Site"
    AuthUserFile /www/intranet/secrets/.users

    <Limit PUT>
      require carol
    </Limit>

  </Location>
</VirtualHost>
```

用户 carol 可以使用她自己的用户帐户在 http://carol.domain.com/publish 目录中发布内容。由于文件属于用户 carol，Web 服务器创建的文件也允许她通过 FTP 或其他途径访问。

3.  为每个用户创建虚拟主机后，使用 /usr/local/apache/bin/apachectl restart 命令重启 Apache 服务器，并通过使用相应的 URL 发布测试页面来测试每个用户的配置。

## 维护你的网站

在你实施了 Web 周期并建立了内容生成流程之后，维护你的网站至关重要。典型的 Web 维护任务包括服务器监控、日志记录和备份。网站维护中的服务器监控和日志记录方面将在第 8 章中讨论。本节讨论数据备份。如果可能的话，你应该有两种类型的备份——在线和离线——我在以下章节中进行了描述。

### 在线备份

在紧急情况下，在线备份非常有用。你可以相当快地访问备份数据，并且在大多数情况下，可以在几分钟内完成必要的恢复任务。要获得在线备份解决方案，你可以寻找商业在线备份供应商或与你的 ISP 联系。然而，如果你在自己的网络上托管 Web 服务器，你可以将备份保存在网络上的另一台主机上。在大多数 Unix 系统上，你可以运行一个名为 *rdim* 的程序来在其他的 Unix 站点上创建你 Web 站点的镜像目录（第 23 章有一个基于 *rdist* 的站点镜像应用程序示例）。

在 Web 服务器本身保存 Web 数据的压缩版本甚至可能是一个好主意。在 Unix 系统上，你可以设置一个 *cron* 任务，以所需的频率创建 Web 数据的压缩 *tar* 文件。例如：

```
# for system V-ish Unix, weekday range is 0-6 where 0=Sunday
# For BSD-ish system use weekday range 1-7 where 1=Monday
# This example is for a Linux system (System V-ish crond)
30 2 * * 0,1,3,5, root /bin/tar czf /backup/M-W-F-Sun.tgz /www/*
30 2 * * 2,4,6 root /bin/tar czf /backup/T-TH-Sat.tgz /www/*
```

如果这两个 *cron* 条目保留在 /etc/crontab 中，将会创建两个文件。每周一、周三、周五和周日，第一个 *cron* 任务将在凌晨 2:30 运行，以创建 /www 中所有内容的备份，并将压缩备份文件存储在 /backup/M-W-F-Sun.tgz 文件中。类似地，在周二、周四和周六的早上（凌晨 2:30），第二个 *cron* 条目将在同一备份目录中创建一个名为 T-TH-Sat.tgz 的文件，包含相同的数据。拥有两个备份确保你在两个压缩文件中至少有最近两天的备份。

### 离线备份

你还应该在可移动媒体上进行备份，并将其存放在安全的地方。从这种备份中恢复通常是一个耗时的操作。你可以使用磁带驱动器、可移动硬盘（如 Jazz 磁盘）来执行此备份。我更喜欢基于 8mm 磁带的备份，因为它提供 8GB 的数据存储容量；此外，8mm 磁带驱动器在市场上存在的时间比新的紧凑型可移动媒体要长得多。

随着你的 Web 站点内容变得更加丰富，可用的 Web 空间正在迅速填满。这通常是未使用但出于担心某些东西（如链接）会在某处断开而从未删除的文件的结果。如果你认为这对你的 Web 站点适用，并且你在 Unix 平台上，你可能想考虑运行 *find* 实用程序来定位长期未被访问的文件。例如：

```
find /www -name "*.bak" -type f -atime +10 -exec ls -l {} \;
```

这列出了 /www 目录下所有以 *.bak* 扩展名结尾且在最近 10 天内未被访问的文件。如果你想删除这些文件，你可以用 *find* 替换 *ls* -l 命令，例如：

```
find /www -name "*.bak" -type f -atime +10 -exec rm -f {} \;
```

如果这有帮助，也许你可以创建一个 cron 条目，定期运行此命令。

### 标准化标准

有了 Web 周期，你就拥有一个可以容纳许多开发者的环境；然而，仅仅创建 Web 周期并不能确保高质量的 Web 生产。高质量的 Web 需要高质量的内容，并且你应遵循关于内容开发的准则。这里的主题是标准化你的标准。

每个 Web 站点都应提供独特的内容，以吸引潜在访客。所有类型的 Web 内容都可以归类为静态或动态。*静态内容* 通常由 HTML 文件创建，而 *动态内容* 通常是 CGI 或其他服务器端或客户端应用程序的输出。大多数站点使用静态内容和动态内容的混合来发布其信息；因此，静态和动态内容开发都需要标准。

#### HTML 文档开发策略

虽然你可以通过多种方式提供静态内容，例如纯文本或 PDF 文件，但大多数 Web 站点使用 HTML 文档作为主要信息存储库。为了指导你的 HTML 作者，你应该创建一套 HTML 开发策略。以下是你可以为你的组织适应的一些准则。

**始终使用标准 HTML 标签**

HTML 开发人员应始终使用最新的标准 HTML。使用依赖浏览器的 HTML 可能会使页面在一种类型的浏览器上看起来很棒，但在另一种上则显得糟糕。

例如，以下显示了一个满足最小 HTML 文档标准的骨架 HTML 文档。

```html
<HTML>
<HEAD><TITLE> 文档标题放在这里 </TITLE> </HEAD>
<BODY>
  文档主体放在这里
</BODY>
</HTML>
```

你的每个文档应至少包含这些 HTML 标签。

**保持内联图像与文档在一起**

文档的内联图像应位于文档目录的子目录中。对这些图像的源引用应该是相对的，因此如果



当文档随图像目录从一个位置移动到另一个位置时，图像的渲染方式与之前完全相同。

**注意** 这条规则有一个例外：如果您的某些图像是可重用的，您应考虑将它们放入中央图像目录。一个典型的例子是使用图像文件实现的标准导航栏。由于导航栏可以在多个文档中重复使用，您可能希望将这些图像存储在中央目录中，而不是与每个文档一起存放。这提供了更好的控制，并节省了磁盘空间。

以下示例向您展示了如何创建一个便携式 HTML 文档，该文档链接了多个图形文件。假设您要发布两个 HTML 文档（$mydoc1.html$ 和 $mydoc2.html$），它们包含三个图像（$image1.gif$、$image2.gif$ 和 $image3.gif$）。您可以首先在文档根目录下或任何其他适当的子目录下创建一个有意义的子目录。假设您在服务器的文档根目录（$ /www/mycompany/htdocs$）下创建了这个目录，并将其命名为 $mydir$。

现在，在 $mydir$ 目录下创建一个名为 $images$ 的子目录，并将您的三个图像存储在该目录中。编辑您的 HTML 文档，使所有指向图像的链接都使用如下所述的 SRC 属性：

```
SRC="/images/image1.gif"
SRC="/images/image2.gif"
SRC="/images/image3.gif"
```

image3 的图像内联链接示例可能如下所示：

```
<IMG SRC="images/images3.gif" HEIGHT="20" WIDTH="30" ALT="Image 3 Description">
```

上述行中的 SRC 属性不包含任何绝对路径信息。如果文档连同 images 子目录一起从 $mydir$ 移动到 $otherdir$，图像不会损坏。然而，如果链接包含诸如以下的路径信息：

```
<IMG SRC="mydir/images/images3.gif" HEIGHT="20" WIDTH="30"
ALT="Image 3 Description">
```

或者

```
<IMG SRC="/mydir/images/images3.gif" HEIGHT="20" WIDTH="30"
ALT="Image 3 Description">
```

那么这些文档在移动后需要修复。许多网站在文档根目录下（如 $images$）的中央图像目录中存储图像，并使用如下所示的 IMG 标签来链接文档：

```
<IMG SRC="/images/images3.gif" HEIGHT="20" WIDTH="30"
ALT="Image 3 Description">
```

这是可行的，但当您要删除 HTML 文档时，必须确保同时也删除中央图像目录中相应的图像。如果未这样做，最终您的图像目录中会消失大量磁盘空间。因此，将图像保存在中央目录中并不是一个好主意。您应该将图像与其链接一起保存在子目录中。

## 在每个文档上显示清晰的版权声明

每个文档都应包含一个嵌入的（注释形式的）版权声明，明确列出文档及其所有图像的所有者。类似的版权声明也应显示在每个页面上。为了方便更新版权声明，您可能需要考虑使用 SSI 指令，如下所示：

```
<!--#include file=/copyright.html -->
```

现在，您只需要创建一个名为 copyright.html 的 HTML 页面，并将其放置在服务器的文档根目录下。由于此 HTML 页面的内容会被插入到调用此 SSI 指令的 SSI 启用文档中，因此您不应在此文档中使用 <HTML>、<HEAD>、<TITLE> 或 <BODY> 标签。使用这种 SSI 调用会在您需要更新版权声明中的年份或进行其他更改时让事情变得更简单。

## 动态应用程序开发策略

动态内容通常由 CGI 脚本或实现 CGI 或其他服务器端接口的其他应用程序生成。绝大多数动态内容是使用基于 Perl 的 CGI 脚本生成的。由于 CGI 脚本和应用程序通常生命周期很短，许多 CGI 开发人员不会花时间开发高质量的应用程序。

如果您计划使用基于 FastCGI 或 mod_perl 的脚本和应用程序，务必以正确的方式开发它们。在为动态内容实现脚本和应用程序时，应考虑以下策略。

### 始终使用版本控制

CGI 开发人员必须使用版本控制，这样如果新开发并部署的版本包含错误，您可以回退到应用程序的较旧版本。在大多数 Unix 系统上，您可以使用并发版本系统（CVS）软件来实现受版本控制的环境。您可以在 ftp://prep.ai.mit.edu 找到最新版本的 CVS 软件。

### 不要在 CGI 脚本或应用程序中使用绝对路径

CGI 脚本中不应使用绝对路径。这确保了脚本可以在多个网站上无需修改即可使用。如果出于特殊目的需要绝对路径，则应为脚本提供配置文件；这样，可以通过修改文本配置文件来更新路径。

### 提供用户级和代码级文档

源代码需要有良好的文档，以便未来的开发人员可以更新脚本，而无需花费大量时间试图弄清楚其工作原理。

### 避免在脚本或应用程序中嵌入 HTML 标签

CGI 脚本的输出应该是模板驱动的。换句话说，CGI 脚本读取输出页面模板并替换动态数据字段（这些字段可以用自定义标签表示）。这使得 HTML 开发人员更容易更新输出页面，因为 HTML 不在 CGI 脚本内。事实上，CGI 脚本应尽可能少地包含 HTML。

### 不要信任用户输入数据

为降低安全风险，请确保在使用用户输入数据之前对其进行检查。您可以在第 18 章中了解有关检查用户输入的更多信息，该章详细讨论了与输入相关的安全风险和解决方案。

### 避免在基于 Perl 的 CGI 脚本中使用全局变量

在用 Perl 开发 CGI 脚本时，应避免使用全局变量。限制变量的作用域是消除不可预测脚本行为的一种方法。Perl 程序员应使用以下方式进行变量声明：

`my $variable;`

而不是：

`local $variable;`

因为前者创建了一个仅在其创建的作用域内可用的变量。而后者的定义只是创建一个全局变量的本地实例，这会造成极大的混淆。Perl 6 很可能会将关键字 'local' 重命名为 'temp'，以使程序员更清楚地理解这一概念。

## 为您的网站提供用户友好的界面

使用标准 HTML 和编写良好的 CGI 脚本/应用程序确实可以使您的网站优于现有的许多网站。然而，网站设计还有另一个方面需要考虑——用户界面。

将网站视为一个在 Web 浏览器中可见的图形用户界面（GUI）的交互式应用程序。GUI 需要具有用户友好性，以便用户在访问您的网站时拥有愉快的 Web 体验。

本节讨论了开发用户友好 GUI 的关键问题。除了使您的 GUI 用户友好外，您还需要注意断链或对已删除文件的请求。使用您的服务器错误日志来检测此类问题。您还应该有一种让访问者给您反馈的方式。大多数网站使用简单的基于 HTML 表单的反馈 CGI 脚本。您可以开发一个适合您需求的脚本。收集反馈是了解您的访问者如何看待您网站的一个好方法。

### 使您的站点易于导航

用户必须能够在不让自己头疼的情况下从一个页面转到另一个页面。他们应该能够找到按钮或菜单栏，以便他们来回移动或跳转到相关信息。

许多 Web 页面设计师认为，由于流行的 Web 浏览器已经包含“后退”和“前进”按钮，因此在页面上放置“后退”或“前进”按钮是多余的。错了！想象一下，用户从搜索引擎的输出结果进入您的某个页面（主页除外）。用户仅仅搜索了一个或多个关键词，搜索引擎提供了您网站上某个页面的 URL。用户非常想了解您网站上该主题的相关信息，因此用户希望从文档的开头开始——但用户无法做到这一点，因为浏览器的“后退”按钮会将用户带回搜索引擎的输出页面！

唉，如果该页面有一个指向上一页的链接（或按钮），用户就可以轻松地回到上一页。那些不喜欢额外按钮的 Web 页面设计师坚持认为，用户本应稍微操作一下 URL 就能回到主页并从那里开始。好吧，这假设主页上有一个指向该页面（匹配搜索关键词）的明确链接，但这并不总是事实。

实现一个菜单栏是个好主意，它可以让用户来回移动，还可以让用户跳转到相关位置，甚至跳转到主页。

### 创建吸引人的设计

将网站视为全天候活跃的彩色且交互式演示文稿。如果此演示文稿的外观和感觉不太合适，您的访问者会从您的网站（或站点）点击离开。在开发具有吸引力的站点设计时，请考虑以下指南。

### 适当的前景色和背景色

确保您在选择颜色时不过分。使用极端颜色会使您的网站显得不专业且沉闷。要有颜色意识，并使用适当的配色方案。例如，如果您的网站是关于儿童玩具的，它应该是一个色彩斑斓的网站。然而，如果您的网站是关于数字信号处理器基准测试的，您可能不需要太多明亮的颜色或花哨的背景。




## 适当的文本大小

尽量让主要内容以正常字体显示。使用特殊字体（如通过 `<FONT FACE="myVerySpecialFont">`）可能会让你的网页在*你的* Web 浏览器中看起来不错（因为你恰好拥有该字体），但在其他人的浏览器中，页面可能看起来完全不同，甚至难以阅读。此外，要注意文本的大小；不要将其设置得过大或过小。请记住，如果访问者无法阅读你在网页上所说的话，他们就无法喜欢你所表达的内容。

## 减少图像和动画的使用

警惕不必要的图像。图像会使你的 Web 页面下载速度变慢。记住，并非所有人都通过 ADSL 或 ISDN 线路连接到你的网站；大多数人仍然使用 56K 或 28.8K 调制解调器进行互联网连接。页面下载缓慢可能会导致潜在客户点击离开你的页面。

此外，对使用动画也要谨慎。即使是*最可爱*的动画在头几次访问后也会变得乏味，所以确保不要让你的页面因动画而过于拥挤。

## 移除晦涩的错误信息

使用 *ErrorDocument* 指令配置 Apache，这样用户就不会收到难以理解的服务器错误信息（至少对普通用户而言）。例如，当请求的 URL 在服务器上未找到时，服务器可能会显示一个晦涩的错误信息。为了让这个错误信息更友好，你可以添加类似 *ErrorDocument* 的指令：

```
ErrorDocument 404 /sorry.html
```

将其添加到 *httpd.conf* 文件中，这样普通 Web 访问者就能轻松理解该错误信息。

## 测试你的 Web GUI

测试 Web 界面的最佳方法之一，是使用一套类似于普通互联网用户或潜在客户的计算机的系统。如果你认为你的客户都拥有高性能计算机和快速连接，那么你可能就不需要担心使用较少的图形或客户端应用程序（如 Java applets 和 Shockwave 动画）。

在大多数情况下，你不知道潜在客户计算机和网络规范，所以你应该按照普通用户的设置来操作。使用一台低端 Pentium 计算机，配备 16MB 内存和 28.8K 调制解调器连接，通过 ISP 账户测试你的网站。尝试较低的监视器分辨率，例如 640×480 或 800×600 像素；如果你的目标访问者使用 Web-TV 系统，请尝试 550×400 像素的分辨率。

如果你浏览自己的网站时感到愉快，其他人可能也会感到愉快。另一方面，如果你不喜欢你看到的内容，其他人可能也不喜欢！

> **提示**
> 如果你愿意，可以让第三方测试你的网站。例如，Netscape.com 在 http://websitergarage.netscape.com 提供基于 Web 的免费调优服务。Netscape 的后端应用程序可以检查任何 Web 站点的页面下载时间、HTML 质量、死链、拼写错误、HTML 设计质量和链接流行度。要试用它，只需访问上述网站，输入你的网站地址和电子邮件地址，等待几秒钟到几分钟。你将获得对你网站的免费诊断报告。

# 推广你的网站

如果没人知道，完美的网站又有什么好处呢？你应该考虑在网络上推广你的网站。你可以雇用广告代理机构来在这方面帮助你，尽管网络广告可能费用高昂。如果预算是障碍，你可以自行推广。以下列表提供了一些正确推广你站点的建议。

- **搜索引擎**：在采取任何措施推广你的网站之前，问自己：“我如何在网络上查找信息？” 答案是：通过搜索引擎。你的公司是否列在搜索引擎中？如果没有，这就是推广你网站的第一步。
  - 几乎所有搜索引擎都允许你将你的 URL 提交到它们的搜索机器人数据库中，以便它们将来可以遍历你的 Web。你应该列出你认为重要的搜索引擎，并将你网站的 URL 提交到这些引擎。这个过程可能需要几天或几周。

- **META 标签**：你可以在内容中添加 META 信息，以便在潜在客户进行搜索时，帮助你的 URL 出现在不错的位置。例如，你可以添加类似的 META 信息：
  ```html
  <META NAME="KEYWORD" CONTENT="keyword1 keyword2 keyword3 ...">
  <META NAME="DESCRIPTION" CONTENT="Description of your company">
  ```

- **链接交换**：为了增加流量，你还可以参与诸如 www.Linkexchange.com 这样的链接交换。链接交换要求你在网页中放置一组特殊的 HTML 标签；这些标签会将广告图形（横幅广告）文件拉入你的页面。作为回报，你的横幅广告图形也会显示在其他同意在其页面上展示他人横幅的网站上运营的网站中。这种广告分享方式在个人和小型商业网站中非常流行。

无论你是购买 Yahoo、AltaVista 或 Netscape 等高知名度网站上的广告空间，还是使用链接交换方法，你都应通过自己生成搜索查询，定期检查你的网站在搜索引擎输出中的排名。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_349_0.png)

# 运行 Web 应用程序

提供静态 HTML 页面的做法几乎已成为过去。如今，大多数受欢迎的网站都有大量动态内容。人们不会访问那些不经常变化的网站。因此，了解如何使用 CGI 脚本、服务器端包含（SSI）、FastCGI 应用程序、PHP、mod_perl 脚本和 Java  Servlets 来启用动态内容至关重要。本部分展示了如何使用 Apache 结合所有这些技术。

## 本部分包含

- **第 12 章**：运行 CGI 脚本
- **第 13 章**：服务器端包含（SSI）
- **第 14 章**：配置 Apache 以支持 FastCGI
- **第 15 章**：PHP 和 Apache
- **第 16 章**：使用 Perl 与 Apache
- **第 17 章**：使用 Tomcat 运行 Java Servlets 和 JSP 页面

# 12 运行 CGI 脚本

![](img/e11fcbd2818a3495ac70085e5d8d1c26_351_0.png)

动态内容驱动着 Web。如果没有动态、可个性化的内容，Web 将成为一个“去过、做过”类型的地方。毕竟，人们为什么要一次又一次地回来查看和体验同样的旧内容？动态内容借助一项名为通用网关接口（CGI）的规范，从概念变成了现实。CGI 规范告诉 Web 服务器如何与外部应用程序交互。运行 CGI 应用程序的 Web 服务器实际上允许任何人在服务器上按需运行选定的程序列表。本章讨论 CGI 的基础知识，以便你对其有清晰的理解，并详细介绍配置 Apache 以支持 CGI 执行的细节。

**本章包含**
- 了解通用网关接口（CGI）的基础知识
- 为 CGI 配置 Apache
- 为个人用户提供 cgi-bin 访问
- 运行常用的 CGI 应用程序
- 配置 Apache 以调试 CGI 应用程序

## 什么是 CGI？

为了在 Web 上提供动态、交互式的内容，许多流行的网站使用 CGI 应用程序。很可能你已经在 Web 上使用过一个或多个 CGI 应用程序。例如，当你填写 Web 表单时，它很可能由用 Perl 或其他语言编写的 CGI 脚本处理。

当然，随着越来越多的 Web 技术出现，通过网络传递动态内容的新方法变得可用。这些解决方案大多是语言特定的，或者依赖于操作系统或商业软件。另一方面，CGI 是一个语言独立的网关接口规范，可以使用几乎任何流行应用程序开发语言实现，包括 C、C++、Perl、Shell 脚本语言和 Java。

本节展示了 CGI 程序如何工作（参见图 12-1）。基本概念是，Web 服务器获取某个 URL，该 URL——至少目前是这样——告诉 Web 服务器它必须运行一个外部应用程序，称为





![](img/e11fcbd2818a3495ac70085e5d8d1c26_352_0.png)

图 12-1：CGI 程序的工作原理。

helloworld.cgi。Web 服务器启动应用程序，等待其完成，并返回输出。然后，它将应用程序的输出传输给另一端的 Web 客户端。

当你希望客户端能够与应用程序交互时会发生什么？好吧，客户端的输入数据必须提供给应用程序。同样，当应用程序产生输出时，服务器或客户端如何知道要返回哪种类型的输出？程序可以产生文本消息、用于进一步交互的 HTML 表单、图像等等。正如你所见，不同应用程序的输出差异很大，因此必须有一种方式让应用程序告知 Web 服务器和客户端输出的类型。

CGI 定义了一组标准方法，用于服务器将客户端输入传递给外部应用程序，它还定义了外部应用程序如何返回输出。任何遵守这些既定标准的应用程序都可以被称为 CGI 应用程序/程序/脚本。为了简洁起见，我使用术语 CGI 程序来指代任何（例如 Perl 脚本或 C 程序）符合 CGI 规范的东西。在下一节中，我将讨论 CGI 输入/输出过程是如何工作的。

## CGI 输入和输出

Web 服务器有多种方式可以从客户端（如 Web 浏览器）接收信息。HTTP 协议定义了 Web 服务器和客户端交换信息的方式。向 Web 服务器传输请求数据的最常见方法是 GET 请求和 POST 请求，我将在以下各节中对其进行描述。

### GET 请求

GET 请求是发送 HTTP 请求最简单的方法。每当你在 Web 浏览器中输入网站地址时，它会生成一个 GET 请求并将其发送到目标 Web 服务器。例如，如果你在 Web 浏览器中输入 `http://www.hungryminds.com`，它会发送诸如以下的 HTTP 请求：

```
GET /
```

到 `www.hungryminds.com` Web 服务器。此 GET 请求要求 Hungry Minds Web 服务器返回 Web 文档树的顶层文档。该文档通常被称为*主页*，通常指的是顶层 Web 目录中的 `index.html` 页面。此外，HTTP 允许你在 GET 请求中编码额外信息。例如：

```
http://www.mycompany.com/cgi-bin/search.cgi?books=cgi&author=kabir
```

在这里，GET 请求是：

```
GET www.mycompany.com/cgi-bin/search.cgi?books=cgi&author=kabir
```

这告诉服务器执行 `/cgi-bin/search.cgi` CGI 程序，并将 `books=cgi` 和 `author=kabir` 输入数据传递给它。

当 Apache 等符合 CGI 规范的 Web 服务器收到此类请求时，它遵循 CGI 规范并将输入数据传递给应用程序（在这种情况下，是 `cgi-bin` 目录中的 `search.cgi`）。当通过 HTTP GET 请求方法请求 CGI 资源时，Apache：

- 为 CGI 程序设置环境变量，这包括将 HTTP 请求方法名称存储在名为 `REQUEST_METHOD` 的环境变量中，并将从客户端接收到的数据存储在名为 `QUERY_STRING` 的环境变量中。
- 执行请求的 CGI 程序。
- 等待程序完成并返回输出。
- 如果它不是非解析头程序，则解析 CGI 程序的输出。（*非解析头 CGI 程序创建自己的 HTTP 头，因此服务器无需解析头。*）
- 创建必要的 HTTP 头。
- 将程序的头和输出发送到请求的客户端。

图 12-2 说明了这个过程。

现在让我们看看 CGI 程序必须做什么才能检索输入并将其用于内部目的。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_354_0.png)

**图 12-2：** CGI 服务器处理。

如图 12-3 所示，一个 CGI 程序

- 读取 *REQUEST_METHOD* 环境变量。
- 通过使用存储在 *REQUEST_METHOD* 变量中的值来确定是否使用了 *GET* 方法。
- 如果使用 *GET* 方法，则检索存储在 *QUERY_STRING* 环境变量中的数据。
- 解码数据。
- 按自己的意愿处理解码后的数据。
- 处理完成后，将输出的 Content-Type 写入其标准输出设备（*STDOUT*）。
- 将输出数据写入 *STDOUT* 并退出。

Web 服务器读取应用程序的 *STDOUT* 并解析它以定位输出的 Content-Type。然后，它在将输出传输到客户端之前传输适当的 HTTP 头和 Content-Type。CGI 程序退出，整个 CGI 事务完成。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_355_0.png)

图 12-3：CGI 程序处理。

> 如果 CGI 程序需要自己提供所有必要的 HTTP 头和 Content-Type 信息，其名称必须以 **nph** 为前缀（代表 nonparsed header，即非解析头）。**nph** CGI 程序的输出不会被服务器解析，而是直接传输给客户端；大多数 CGI 程序让服务器编写 HTTP 头，因此是解析头程序。

使用 **GET** 请求方法将输入数据传递给 CGI 程序在许多方面都有限制，包括以下方式：

- 作为 URL 一部分传输的数据总大小受客户端的 URL 长度限制。许多流行的 Web 浏览器对 URL 的长度有硬性限制，因此，通过编码 URL 可以发送的总数据量相当有限。然而，偶尔通过 URL 向 CGI 程序传递数据可能是一个好主意。例如，如果你有一个使用 **GET** 方法将数据发送到 CGI 程序的 HTML 表单，提交的 URL 可以被书签以便稍后使用，而无需再次通过数据输入表单。这对数据库查询应用程序来说是一个用户友好的功能。

- 单个环境变量（QUERY_STRING）的值长度是有限的。许多甚至所有操作系统都限制环境变量值可以包含的字节数。这实际上限制了可以存储为输入数据的总字节数。

这些限制对于需要极少或不需要用户输入的 CGI 程序可能无关紧要。然而，对于需要大量用户输入数据的程序，另一种 HTTP 请求方法——POST——更适用。POST 请求方法将在下一节中讨论。

### POST 请求

HTTP POST 请求方法广泛用于向 CGI 程序传递数据。此方法的典型用途可以在你在网络上填写的许多 HTML 表单中找到。例如，清单 12-1 显示了这样一个表单。

#### 清单 12-1：使用 HTTP POST 请求方法的 HTML 表单

```html
<HTML>
<HEAD>
<TITLE> Apache Server 2.0 - Chapter 12 Listing 12-1</TITLE>
</HEAD>

<BODY>
<H1>Listing 12-1</H1>
<H2>An Example HTML Form Using the HTTP POST Request Method</H2>
<HR>
<FORM ACTION="/cgi-bin/search.cgi" METHOD="POST">

<PRE>
Type of Book <INPUT TYPE="TEXT" NAME="book" SIZE="10" MAXSIZE="20">
Author's Name <INPUT TYPE="TEXT" NAME="author" SIZE="10" MAXSIZE="20">
</PRE>
<INPUT TYPE=SUBMIT VALUE="Search Now">
</FORM>

</BODY>
</HTML>
```

请注意，清单中有一个 `<FORM> </FORM>` 部分。HTML 表单通常有一个起始的 `<FORM>` 标签，它定义表单的 ACTION 和请求 METHOD。在上例中，动作是 `/cgi-bin/search.cgi` CGI 程序，方法是 POST。

在起始的 `<FORM>` 标签之后，通常有一个或多个 INPUT 实体；INPUT 实体可能包括文本输入框、下拉菜单和列表。在我们的例子中，有三个输入实体。第一个允许用户为 book 变量输入值。下一个类似，允许用户为 author 变量输入值。第三个有点特殊；它允许用户提交表单。当用户提交表单时，客户端软件向 ACTION（即 `/cgi-bin/search.cgi`）资源发送 POST 请求到服务器，并且以编码格式传输 `book=<用户输入的值>` 和 `author=<用户输入的值>`。

## 比较 GET 和 POST

GET 和 POST 请求有什么区别？POST 数据不会存储在 CGI 程序的 QUERY_STRING 环境变量中。相反，它存储在 CGI 程序的标准输入（STDIN）中。REQUEST_METHOD 变量被设置为 POST，而编码数据存储在 CGI 程序的 STDIN 中，并且一个新名为 CONTENT_LENGTH 的环境变量被设置为存储在 STDIN 中的字节数。

现在，CGI 程序必须检查 REQUEST_METHOD 环境变量的值。如果对于 HTTP POST 请求它被设置为 POST，程序应首先从 CONTENT_LENGTH 环境变量的值确定输入数据的大小，然后从 STDIN 读取数据。请注意，Web 服务器不负责在 STDIN 中插入文件结束（EOF）标记，这就是为什么将 CONTENT_LENGTH 变量设置为数据长度（以字节为单位），这使得 CGI 程序更容易确定数据的总字节数。

可以同时使用 GET 和 POST。下面是一个示例 HTML 表单，它正式使用 POST 方法，但也悄悄地将查询字符串 `username=joe` 作为 CGI ACTION 的一部分混入其中。

```html
<FORM ACTION="/cgi-bin/edit.cgi?username=joe" METHOD=POST>
<input TYPE=TEXT NAME="PhoneNumber"> 
</FORM>
```

在这个示例中，`username=joe` 查询将是 URL 的一部分，但其他字段（`PhoneNumber`）将是 POST 数据的一部分。效果：最终用户可以书签该 URL，并始终作为 joe 运行 edit.cgi 脚本，而无需为任何其他字段设置值。这对于在线数据库应用程序和搜索引擎非常有用。

无论你使用 GET 还是 POST，或者两者兼用，数据都会被编码，解码它取决于 CGI 程序。下一节讨论解码编码数据所涉及的步骤。




## 解码输入数据

原始 HTTP 协议的设计者计划让该协议在任何系统上都能轻松实现。此外，他们还使数据编码方案变得简单。

该方案将某些字符定义为特殊字符。例如，等号（=）有助于创建键值对；加号（+）替代空格字符，而和号字符（&）用于分隔两个键值对。

如果数据本身包含具有特殊含义的字符，你可能会疑惑传输的是什么。在这种情况下，会使用一种三字符编码方案，它可以编码任何字符。百分号（%）表示一个由两个十六进制数字组成的编码字符序列的开始。

十六进制是一种基数为 16 的计数系统，其中 0 到 9 与十进制中的 0 到 9 代表相同的值，但它还有一组额外的数字。这些数字是 A（=10）、B（=11）、C（=12）、D（=13）、E（=14）和 F（=15）。例如，十六进制的 20 等于十进制的 32。转换方案如下：

```
20 = 2 x (16^1) + 0 x (16^0)
```

这两个十六进制数字构成的值可以映射到 ASCII（针对英语）表中以获取对应的字符。例如，%20（十六进制）是 32（十进制），并映射为 ASCII 表中的空格字符。

## Apache CGI 变量

Apache 有两种方式可以实现对 CGI 的支持。标准的 Apache 发行版包含一个 CGI 模块，用于实现传统的 CGI 支持；然而，有一个新的模块（FastCGI）实现了对高性能 CGI 应用程序的支持。本节讨论标准 CGI 支持问题。

在之前的章节中，你了解到符合 CGI 标准的 Web 服务器使用环境变量、标准输入（STDIN）和标准输出（STDOUT）来向 CGI 程序传输信息并从其获取信息。Apache 为 CGI 程序开发人员提供了一套灵活的环境变量。使用这些环境变量，CGI 程序不仅可以检索输入数据，还可以识别它所处理的客户端和服务器的类型。

在以下各节中，我将讨论从编译到 Apache 中的标准 CGI 模块中可用的环境变量。

> **注意**
> Apache 2.xx 源码发行版支持 configure 脚本的 --enable-cgid 选项。此选项强制 Apache 使用脚本服务器（称为 CGI 守护进程）来管理 CGI 脚本进程，从而增强 Apache 的整体性能。

### 服务器变量

这些变量由 Apache 设置，以告知 CGI 程序关于 Apache 的信息。使用服务器变量，CGI 程序可以确定各种服务器特定的信息，例如 Apache 软件的版本、管理员的电子邮件地址等。

#### **SERVER_SOFTWARE**

SERVER_SOFTWARE 由 Apache 设置，其值通常具有以下形式：

```
Apache/Version (OS Info)
```

这里，Apache 是运行 CGI 程序的服务器软件名称，Version 是 Apache 的版本号。一个示例值如下：

```
Apache/2.0.14 (Unix)
```

当 CGI 程序需要利用新版本 Apache 中的新功能，同时仍需在旧版本上正常运行时，这很有用。

GATEWAY_INTERFACE 告诉 CGI 程序服务器当前支持哪个版本的 CGI 规范。一个示例值如下：

```
CGI/1.1
```

CGI 程序可以确定此变量的值，并根据不同版本的 CGI 规范中可用的不同功能进行条件性使用。例如，如果值是 CGI/1.0，程序可能不会使用任何 CGI/1.1 功能，反之亦然。

小数点前的第一个整数称为主要版本号，小数点后的整数称为次要版本号。由于这两个整数被视为独立的数字，CGI/2.2 是比 CGI/2.15 更旧的版本。

#### **SERVER_ADMIN**

如果你使用 httpd.conf 文件中的 ServerAdmin 指令设置站点管理员的电子邮件地址，此变量将设置为反映该值。此外，请注意，如果在虚拟主机配置容器中有 ServerAdmin 指令，并且被访问的 CGI 程序属于该虚拟主机，则 SERVER_ADMIN 变量将设置为该地址。

#### **DOCUMENT_ROOT**

此变量设置为被访问的 Web 站点的 DocumentRoot 指令的值。

### 客户端请求变量

Apache 从请求 CGI 程序的客户端接收的 HTTP 请求头中创建一组环境变量。它通过创建以下一组环境变量向 CGI 程序提供此信息。

#### **SERVER_NAME**

此变量告知 CGI 程序正在访问哪个主机。其值是一个 IP 地址或完全限定主机名，如下所示：

```
SERVER_NAME = 192.168.1.100
SERVER_NAME = www.domain.com
```

#### **HTTP_HOST**

参见 **SERVER_NAME** 变量。

#### **HTTP_ACCEPT**

此变量设置为客户端能够接受的 MIME 类型列表，包括以下类型：

```
HTTP_ACCEPT = image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, image/png, */*
```

在这里，客户端声称能够处理 GIF、JPEG、PNG 和其他图像。这使得 CGI 程序能够确定什么样的输出对客户端最理想。例如，CGI 程序可以生成 GIF 或 JPEG，并收到如下的 **HTTP_ACCEPT**：

```
HTTP_ACCEPT = image/gif, */*
```

然后，因为客户端更偏好 GIF 而非 JPEG，它可以发送 GIF 输出而不是 JPEG。

#### **HTTP_ACCEPT_CHARSET**

此变量指定客户端可接受的字符集，例如：

```
HTTP_ACCEPT_CHARSET = iso-8859-1,*,utf-8
```

#### **HTTP_ACCEPT_ENCODING**

此变量指定客户端可接受的编码方案，例如：

```
HTTP_ACCEPT_ENCODING = gzip
```

在这种情况下，客户端接受 gzip（压缩）文件。因此，CGI 脚本可以使用 gzip 压缩来压缩大型页面并发送它，Web 客户端能够对其进行解压缩。

#### **HTTP_ACCEPT_LANGUAGE**

此变量指定客户端可接受的语言，例如：

```
HTTP_ACCEPT_LANGUAGE = en
```

在这种情况下，客户端接受 en（英语）语言内容。

#### **HTTP_USER_AGENT**

此变量指定请求系统正在运行的客户端软件以及其运行的操作系统，例如：

```
HTTP_USER_AGENT = Mozilla/4.04 [en] (WinNT; I)
```

上述内容等同于以下内容：

```
Client Software = Netscape Navigator ()
Client Software Version = 4.04 (English version)
Operating System = Windows NT (Intel)
```

请注意，Mozilla 是 Netscape 用于 Navigator 代码库的关键字。虽然最初只有 Netscape 浏览器使用“Mozilla”这个词，但许多其他供应商已开始使用 Mozilla 作为 HTTP 头的一部分。例如，从同一台机器运行时，Microsoft Internet Explorer (IE) 5.5 会产生如下的 **HTTP_USER_AGENT** 数据：

```
HTTP_USER_AGENT = Mozilla/5.5 (compatible; MSIE 5.5; Windows NT)
```

许多 Web 站点大量使用此用户代理信息。一个为 Netscape Navigator 优化的站点（即，它使用在 Netscape Navigator 中运行良好的 HTML、JavaScript 或插件功能）可能会使用 **HTTP_USER_AGENT** 信息为使用 IE 或其他不太流行的浏览器访问该站点的用户返回不同的页面。然而，我建议你坚持使用标准 HTML（当前标准 HTML 规范可在 **www.w3.org** 获取），并且完全不实现浏览器特定的功能。虽然为你的页面针对单一浏览器进行优化可能使其在该浏览器中看起来很酷，但并不是每个人都使用该特定浏览器。这意味着你的浏览器特定的 HTML 标签或插件可能会使其他人（不使用你首选浏览器的人）访问你的 Web 站点变得更加困难。

#### **HTTP_REFERER**

此变量设置为将请求转发到被调用的 CGI 程序的统一资源标识符（URI）。通过使用此变量，你可以判断请求是来自你的某个 Web 页面上的链接，还是来自远程 URL。请注意，变量名的拼写错误是不幸的，经常让正确拼写该变量但在应用程序和脚本中发现其无法工作的 CGI 开发者感到困惑。因此，如果你计划使用此变量，请按照此处所述的拼写方式进行拼写。



## HTTP_CONNECTION

`HTTP_CONNECTION` 变量设置为客户端和服务器正在使用的连接类型。例如：

```
HTTP_CONNECTION = Keep-Alive
```

这表示客户端能够处理使用 Keep-Alive 的持久连接，并且当前正在使用它。

## SERVER_PORT

`SERVER_PORT` 变量的值告诉 CGI 程序当前正在使用哪个服务器端口来访问该程序。一个示例如下：

```
SERVER_PORT = 80
```

如果 CGI 程序创建了指向服务器的 URL，将端口地址（即此变量的值）包含在 URL 中可能很有用。

## REMOTE_HOST

`REMOTE_HOST` 变量告诉 CGI 程序客户端的 IP 地址或 IP 名称，如下所示：

```
REMOTE_HOST = dsl-666.isp24by7.net
```

请注意，如果 Apache 服务器是使用 MINIMAL_DNS 选项编译的，则此变量不会被设置。

## REMOTE_PORT

此端口号用于套接字连接的客户端一侧：

```
REMOTE_PORT = 1163
```

我尚未见过此变量的任何用途。

## REMOTE_ADDR

`REMOTE_ADDR` 变量是客户端系统的 IP 地址：

```
REMOTE_ADDR = 192.168.1.100
```

在此变量中为 CGI 程序设置。然而，CGI 程序将无法识别用于访问它的密码。如果此变量被设置为用户名，CGI 程序可以安全地假设该用户提供了适当的密码来访问它。

## SERVER_PROTOCOL

SERVER_PROTOCOL 是客户端用于向 CGI 程序发送请求的协议和版本号：

```
SERVER_PROTOCOL = HTTP/1.1
```

## REQUEST_METHOD

REQUEST_METHOD 变量设置为客户端请求 CGI 程序时使用的 HTTP 请求方法。典型的值是：GET、POST 和 HEAD。

```
REQUEST_METHOD=GET
```

当请求方法是 GET 时，输入数据存储在 QUERY_STRING 变量中。当方法是 POST 时，输入数据存储在 CGI 程序的 STDIN 中。

## REQUEST_URI

REQUEST_URI 变量设置为请求的 URI。

```
REQUEST_URI = /cgi-bin/printenv2
```

## REMOTE_IDENT

只有当 IdentityCheck 指令被设置时，REMOTE_IDENT 才会被设置。此变量存储由远程 identd（identification daemon，识别守护进程）返回的用户身份验证信息。由于许多系统不运行此类守护进程，因此不应将 REMOTE_IDENT 视为识别用户的可靠手段。我建议你在内部网或外部网环境中使用此变量，且你或你的组织正在运行一个 identd 服务器。

## AUTH_TYPE

如果 CGI 程序存储在需要身份验证才能访问的网站部分中，则此变量被设置为指定使用的身份验证方法。

## CONTENT_TYPE

此变量指定附加在请求头中的数据的内容 MIME 类型。例如：

```
CONTENT_TYPE = application/x-www-form-urlencoded
```

在使用 HTML 表单和 POST 请求方法时，你可以使用 <FORM> 标签的 TYPE 属性在 HTML 表单中指定内容类型，如下所示：

```
<FORM ACTION="/cgi-bin/search.cgi"
      METHOD="POST"
      TYPE="application/x-www-form-urlencoded">
```

## CONTENT_LENGTH

当使用 HTTP POST 请求方法时，Apache 将输入数据（附加在请求中）存储在 CGI 程序的 STDIN 中。然而，服务器不会在 STDIN 中插入文件结束（EOF）标记。相反，它将总字节计数设置为该变量的值。例如，如果

```
CONTENT_LENGTH = 21
```

则相关的 CGI 程序应从其 STDIN 中读取 21 字节的数据。

## SCRIPT_NAME

SCRIPT_NAME 是请求的 CGI 程序的 URI：

```
SCRIPT_NAME = /cgi-bin/search.cgi
```

## SCRIPT_FILENAME

SCRIPT_FILENAME 是请求的 CGI 程序的物理、完全限定路径名：

```
SCRIPT_FILENAME = /www/kabir/public/cgi-bin/search.cgi
```

## QUERY_STRING

如果 Web 客户端（如 Web 浏览器）使用 HTTP GET 请求方法并在问号 (?) 后提供输入数据，则数据将作为此变量的值存储。例如，对以下 CGI 程序的请求：

```
http://apache.domain.com/cgi-bin/search.cgi?key1=value1&key2=value2
```

将使 Apache 设置：

```
QUERY_STRING = key1=value1&key2=value2
```

CGI 程序 /cgi-bin/search.cgi 可以在使用前读取并解码此值。

## PATH_INFO

如果 CGI 程序的输入数据是 URI 的一部分，额外的路径（实际上是为被调用的程序准备的一些数据）将作为变量的值存储。例如：

http://apache.domain.com/cgi-bin/search.cgi/argument1/argument2

将使 Apache 设置：

PATH_INFO = /argument1/argument2

> **注意**
> PATH_INFO 不会包含任何属于查询字符串的部分。换句话说，如果 URL 在 ? 后包含查询字符串，则此部分数据将存储在 QUERY_STRING 变量中。例如：
>
> http://apache.domain.com/cgi-bin/search.cgi/CA/95825?book=apache&author=kabir
>
> 将使 Apache 设置以下变量：
>
> PATH_INFO = /CA/95825
> QUERY_STRING = book=apache&author=kabir

## PATH_TRANSLATED

这是请求文件的绝对路径。例如，当 Web 客户端（如 Web 浏览器）请求 http://server/cgi-bin/script.cgi 时，脚本的实际路径可以是 path_to_cgi_alias/script.cgi。

## 为 CGI 配置 Apache

本节讨论如何配置 Apache 以处理 CGI 请求。配置过程包括告诉 Apache 你存储 CGI 程序的位置，为特定文件扩展名设置 CGI 处理程序，以及指示哪些文件扩展名应被视为 CGI 程序。将 CGI 程序保存在一个中央目录中是个好主意。这允许对 CGI 程序进行更好的控制。将 CGI 程序分散在整个 Web 空间中可能会使该网站变得难以管理，并且也可能创建难以追踪的安全漏洞。

### 为你的 CGI 程序目录设置别名

创建一个中央 CGI 程序目录是设置安全 CGI 环境的第一步。最好将这个中央 CGI 程序目录保存在 DocumentRoot 目录之外，这样 CGI 程序就不能被 Web 浏览器等 Web 客户端直接访问。为什么？好吧，就 CGI 程序而言，你希望向外部世界尽可能少地提供信息。这将确保你的站点具有更好的安全性。黑客关于你的 CGI 程序物理位置了解得越少，那个人能造成的伤害就越小。

首先，你需要在 DocumentRoot 目录之外创建一个目录。例如，如果 /www/mycompany/public/htdocs 是某个网站的 DocumentRoot 目录，那么 /www/mycompany/public/cgi-bin 是 CGI 程序目录的一个良好候选者。要为你的 CGI 程序目录创建别名，你可以使用 ScriptAlias 指令。

如果你正在为主 Web 服务器设置 CGI 支持，请编辑 `httpd.conf` 文件并插入一行 `ScriptAlias`，语法如下：

```
ScriptAlias /alias/ “/fully/qualified/path/to/cgi/scripts/dir/”
```

例如：

```
ScriptAlias /cgi-bin/ “/www/mycompany/public/cgi-bin/”
```

如果你正在为虚拟站点设置 CGI 支持，请在定义虚拟主机的 `<VirtualHost . . . >` 容器中添加一行 `ScriptAlias`。例如：

```
NameVirtualHost 192.168.1.100
<VirtualHost 192.168.1.100>
   ServerName blackhole.domain.com
   DocumentRoot “/www/blackhole/public/htdocs”
   ScriptAlias /apps/ “/www/blackhole/public/cgi-bin/”
</VirtualHost>
```

这里使用 /apps/ 别名来创建 CGI 程序目录别名。如果在 `/www/blackhole/public/cgi-bin` 目录中有一个名为 `feedback.cgi` 的 CGI 程序，则只能通过以下 URL 访问它：

```
http://blackhole.domain.com/apps/feedback.cgi
```

设置 `ScriptAlias` 指令后，请确保目录权限允许 Apache 读取和执行目录中找到的文件。

`ScriptAlias` 指向的目录应具有非常严格的权限设置。除了 CGI 程序开发者或服务器管理员之外，任何人都不应拥有该目录的完全权限（读、写和执行）。你可以定义多个 CGI 程序目录别名，使得 `ScriptAlias` 指定的目录默认情况下不可浏览（出于安全原因）。

当被请求时，Apache 将尝试运行在 `ScriptAlias` 目录中找到的任何可执行文件（在文件权限意义上）。例如：

```
http://blackhole.domain.com/apps/foo.cgi
http://blackhole.domain.com/apps/foo.pl
http://blackhole.domain.com/apps/foo.bak
http://blackhole.domain.com/apps/foo.dat
```

上述所有 URL 请求都将促使 Apache 尝试运行各种 `foo` 文件。




## 选择特定的 CGI 文件扩展名

我并不喜欢 `ScriptAlias` 指定目录中的任意文件都作为 CGI 程序运行的想法。我更倾向于一种能够限制 CGI 程序名称的解决方案，使得只有具有特定扩展名的文件才被当作 CGI 程序处理。下面讨论如何通过使用 `mod_cgi` 模块中找到的 Apache 处理程序来实现这一目标，并包含一个示例配置，其中我通过 `AddHandler` 处理程序启用一组选定的文件扩展名，使其被当作 CGI 程序。

在这个示例中，假设 Apache 服务器名称为 `www.domain.com`，且其 `DocumentRoot` 目录设置为 `/www/website/public/htdocs`；CGI 程序目录为 `/www/nitec/public/cgi-bin`。请注意，CGI 程序目录是故意保留在 `DocumentRoot` 指定目录之外的。这确保了没有人可以浏览该目录，因为 Apache 只能通过别名看到它。

请按照以下步骤设置 Apache，以从目录中运行给定扩展名的 CGI 脚本：

- 1. 通过完全从 `httpd.conf` 中移除现有的 `ScriptAlias` 指令，或者在该行开头插入井号（#）将其变成注释行，来禁用现有的 `ScriptAlias` 指令。
- 2. 为 CGI 程序目录创建一个别名。由于 CGI 程序目录位于文档树之外，如果没有别名（或符号链接），就无法访问它。可以使用 `Alias` 指令定义别名，其语法如下：
    ```
    Alias /alias/ "/path/to/cgi/dir/outside/doc/root/"
    ```
    按照此语法，所需的 `Alias` 指令看起来如下：
    ```
    Alias /cgi-bin/ "/www/website/public/cgi-bin/"
    ```
- 3. 通过为该特殊目录定义 `<Directory>` 容器，指示 Apache 从此目录执行 CGI 程序。使这一切发生（即将该目录转变为 CGI 程序目录）所需的目录容器定义如下：
    ```
    <Directory "/path/to/cgi/dir/outside/doc/root/">
        Options ExecCGI -Indexes
        AddHandler cgi-script extension-list
    </Directory>
    ```

`Options` 指令为 `/path/to/cgi/dir/outside/doc/root` 目录设置了两个选项。首先，设置了 `ExecCGI` 选项，它告诉 Apache 允许从此目录内部执行 CGI 程序。其次，`-Indexes` 选项告诉 Apache 不允许目录列表，因为允许访客查看 CGI 脚本目录的内容不是一个好主意。接下来，`AddHandler` 指令为该目录中发现的一组文件扩展名设置 cgi-script 处理程序。列表中具有指定扩展名的任何文件都将被视为 CGI 程序。当 Web 客户端请求此类文件时，程序将运行并将输出返回给 Web 客户端。我们当前示例中的实际指令如下所示：

```
<Directory "/www/mysite/public/cgi-bin">
    Options ExecCGI -Indexes
    AddHandler cgi-script .cgi .pl
</Directory>
```

在此处，你已启用 `.cgi` 和 `.pl` 作为 CGI 程序扩展名，因此，当发起诸如以下请求时：

```
http://www.domain.com/cgi-bin/anything.cgi
http://www.domain.com/cgi-bin/anything.pl
```

Apache 将尝试将这些文件作为 CGI 程序执行。当然，如果这些文件实际上不是可执行文件或不存在，Apache 将显示并记录错误消息。

前面提到的 CGI 程序目录权限设置仍然适用于此配置。相同的配置也适用于虚拟主机站点。例如，在以下示例中，www.client01.com 的 `/cgi-bin/` 别名被设置为在 /www/client01/public/cgi-bin 目录中执行 CGI 程序：

```
<VirtualHost 192.168.2.100>
    ServerName www.client01.com
    DocumentRoot "/www/client01/public/htdocs"
    CustomLog logs/www.client01.com.access.log
    ErrorLog logs/www.client01.com.errors.log
    Alias /cgi-bin/ "/www/client01/public/cgi-bin/"
    <Directory "/www/client01/public/cgi-bin">
        Options ExecCGI -Indexes
        AddHandler cgi-script .cgi .pl
    </Directory>
</VirtualHost>
```

在这里，www.client01.com 的 `/cgi-bin/` 别名被设置为在 /www/client01/public/cgi-bin 目录中执行 CGI 程序。

## 为用户启用 cgi-bin 访问

许多互联网服务提供商（ISP）提供带有用户账户的网站空间。这些网站通常拥有这样的 URL：

```
http://www.isp.net/~username
```

这些站点通常会收到用户通过其客户端（浏览器）发出的 cgi-bin 访问请求。术语 cgi-bin 访问是一个通用术语，用于指示 Web 服务器上的 CGI 功能。传统上，CGI 程序目录已被别名为 /cgi-bin/，因此产生了这个术语。另一个变得非常流行的常见术语是主页（home page），它指的是用户 Web 目录的顶级索引页。

以下部分讨论在 Apache Web 服务器中为用户提供 cgi-bin 访问的两种方式。你只需要实施这些方法中的任何一种。

### Directory 或 DirectoryMatch 容器

当 `UserDir` 指令设置为目录名称时，Apache 将其视为用户网站的顶级目录，例如：

```
ServerName www.domain.com
UserDir public_html
```

现在，当对 `http://www.domain.com/~username` 的请求到来时，Apache 会定位指定用户的家庭目录（通常通过检查 Unix 系统上的 /etc/passwd 文件），然后附加 `UserDir` 指定的目录以创建顶级用户 Web 目录的路径名。例如，URL

```
http://www.domain.com/~joe
```

使 Apache 寻找 /home/joe/public_html（假设 /home/joe 是 Joe 的家庭目录）。如果该目录存在，则该目录的索引页将发送给请求客户端。

为每个用户添加 CGI 支持的一种方法是在 `httpd.conf` 文件中添加以下配置：

```
<Directory ~ "/home/[a-z]+/public_html/cgi-bin">
Options ExecCGI
AddHandler cgi-script .cgi .pl
</Directory>
```

或者你可以使用此配置：

```
<DirectoryMatch "/home/[a-z]+/public_html/cgi-bin">
Options ExecCGI
AddHandler cgi-script .cgi .pl
</DirectoryMatch>
```

在这两种方法中，Apache 将 `http://www.yourcompany.com/~username/cgi-bin/` 请求转换为 `/home/username/public_html/cgi-bin/`，并允许具有正确扩展名（.cgi 或 .pl）的任何 CGI 程序执行。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_370_0.png)

> 为了使这正常工作，所有用户名必须由全小写字母组成。如果你有字母数字用户名，你必须使用不同的正则表达式。例如，如果你有 *stev01* 或 *stev02* 这样的用户名，你需要使用 `[a-z0-9]`+ 修改 `[a-z]`+ 字符集以包含数字，或者如果你还允许大写的用户名，则使用 `[a-zA-Z0-9]`+ 作为正则表达式。

### ScriptAliasMatch

通过使用 *ScriptAliasMatch* 指令，你可以为每个用户支持 CGI 程序目录。例如：

```
ScriptAliasMatch ^~([a-z]+)/cgi-bin/(.*) /home/$1/public_html/cgi-bin/$2
```

将 *username* 匹配到反向引用变量 $1，其中 $1 等于 --*username*，且 *username* 是一个小写字符串，例如 *joe* 或 *stev01*，然后 Apache 将 `/cgi-bin/` 之后的所有内容匹配到反向引用变量 $2。接着，Apache 使用 $1 和 $2 变量创建实际的 CGI 程序路径。例如：

```
http://www.domain.com/~joe/cgi-bin/search.cgi?author=kabir
```

在此处，`([a-z]+)` 将波浪号标记 `(~)` 之后的一个或多个小写字母映射到 $1。换句话说，这个正则表达式使我们能够捕获波浪号 `(~)` 和用户名后的尾部斜杠 `(/)` 之间的所有内容。因此，在上面的示例中，$1 被设置为 *joe*。请注意，`^` 确保该指令仅应用于以 `~` 开头的 URL，如上例所示。

指令中的下一个正则表达式是 `(.*)`，它将 `/cgi-bin/` 之后的所有内容映射到 $2。因此，$2 被设置为 *search.cgi?author=kabir*。

现在，Apache 可以使用以下内容创建 CGI 程序目录的物理路径：

```
/home/$1/public_html/cgi-bin/$2
```

对于前面的示例，此正则表达式得出以下路径：

```
/home/joe/public_html/cgi-bin/search.cgi?author=kabir
```

因为这是存储 CGI 程序 *search.cgi* 的位置，所以它会执行并将输出返回给 Web 客户端。

如果你不喜欢将 CGI 程序目录放在 *public_html*（即 *UserDir* 指定的目录）之下，你可以通过从表达式中移除 *public_html* 部分来将其保留在该目录之外，如下所示：

```
ScriptAliasMatch ^~([a-z]+)/cgi-bin/(.*) /home/$1/cgi-bin/$2
```





这将映射以下示例 URL 请求：

```
http://www.domain.com/~joe/cgi-bin/search.cgi?author=kabir
```

到以下物理文件：

```
/home/joe/cgi-bin/search.cgi?author=kabir
```

当然，如果你不喜欢将用户子目录设置为全局可读（即 public_html），你可以通过为用户创建一个 Web 分区（或目录）并为他们提供独立的目录来托管他们的个人主页，从而解决此问题。以下是一个示例：

```
ScriptAliasMatch ^~([a-z]!+)/cgi-bin/(.*) /www/$1/cgi-bin/$2
```

这匹配针对 www/username/cgi-bin/scriptname 的请求。由于此目录不在用户的家庭目录（/home/username）中，作为系统管理员，你可能能够对其进行更好的控制。

## 使用 AddType 创建新的 CGI 扩展名

如果你想在特定目录中创建新的 CGI 程序扩展名，也可以使用 .htaccess（或 AccessFileName 指令指定的文件）。

在你能使用基于目录的访问控制文件（.htaccess）添加新扩展名之前，必须如下创建 <Directory> 容器：

```
<Directory "/path/to/your/directory">  
  Options ExecCGI -Indexes  
  AllowOverride FileInfo  
</Directory>
```

目录容器内的第一条指令告诉 Apache，你希望在此目录中启用 CGI 程序执行，并出于安全考虑禁用目录列表功能。第二条指令告诉 Apache 在基于目录的访问控制文件（.htaccess）中启用 FileInfo 功能。此功能允许你在基于目录的访问控制文件中使用 AddType 指令。

要添加一个新的 CGI 程序扩展名（.wizard），你需要做的就是在目录中创建一个 .htaccess（或你在 AccessFileName 指令中指定的任何名称）文件，内容如下：

```
AddType application/x-http-cgi .wizard
```

然后，将该目录中现有的 CGI 程序重命名为带有 .wizard 扩展名，并通过浏览器请求它。请确保目录和 CGI 程序的所有文件权限设置都配置为允许 Apache 读取和执行。

## 运行 CGI 程序

如果你是一位 Apache 管理员，你很可能需要设置 CGI 程序，甚至可能知道如何编写它们。在本节中，我将讨论创建非常简单的 CGI 程序的基础知识。由于这不是一本 CGI 编程书，我不提供关于 CGI 编程的深入覆盖。我的重点在于揭示有关 CGI 程序的内容，以帮助 Apache 管理员更好地管理其支持 CGI 的网站。

本节中的许多示例使用 Perl。如果你的系统上没有 Perl，你可以从 **www.perl.com** 获取源代码，或者可能获取二进制文件。尽可能为系统编译二进制文件，而不是信任由他人创建的二进制文件，这是一种好的做法。

## 使用 Perl 编写 CGI 脚本

CGI 脚本编写等同于 Perl 脚本编写；依我拙见，Perl 是各种脚本语言中的王者，正是 Perl 推广了 CGI 脚本编写，因为它因 Perl 而广受欢迎。作为又一名 Perl 黑客，自 1995 年以来我一直在编写基于 Perl 的 CGI 脚本，并且我仍继续使用 Perl 来处理中小型的 Web 解决方案。由于这不是一本 Perl 编程书，我不会介绍如何一般性地编写 Perl 脚本。相反，我将讨论如何使用 Perl 编写 CGI 脚本。如果你不熟悉 Perl，我建议尽快阅读一本 Perl 编程书籍。

在使用 Perl 编写 CGI 脚本时，应遵循以下一系列准则或编程风格。具体如下：

- **分离内容与逻辑——将内容排除在脚本之外。** 使用 HTML 或 XML 模板来确保 CGI 脚本的界面方面不在脚本本身中。这将确保非程序员用户（例如图形或 HTML 专家）可以轻松地更改界面。
- **使用配置文件——切勿在脚本中硬编码可自定义信息。** 使用配置文件来读取信息。这将使你的脚本更具灵活性。
- **规范化用户数据——在收集用户数据以供将来使用时，确保在将数据存储在文件或数据库中之前规范化数据。** 例如，如果你收集访问者的电子邮件地址，将每个电子邮件地址规范化为指定的大小写（大写或小写），并修复用户遗漏和数据输入错误是个好主意。我见过许多案例，AOL 用户在网络表单中书写电子邮件地址时漏掉了 .com，或者在 @ 和名称或主机名之间多加了空格。我还见过数千个案例，用户将他们的名字输入为大写或小写。试想一下，当你使用未规范化的名字（用户自己在你的网络表单中输入的）来定制时事通讯时，会给他们留下什么样的印象，或者当你的邮件列表系统发现数千个“@AOL”或“user @ aol”类型的数据错误时，你会收到多少退信。
- **对用户数据进行合理性检查——CGI 脚本经常是许多安全攻击的目标。** 如果你的 CGI 脚本接受用户输入，请确保在使用用户数据之前对其进行验证。

**提示**：在你开始重新发明轮子之前，检查综合 Perl 档案网络（CPAN）网站 http://cpan.perl.com 以查找现有的 Perl 模块，你可以使用它们来解决当前问题，或通过重用现有 CPAN 模块来减少开发工作量。在本节中，我使用了许多 CPAN 模块来构建 CGI 脚本。每当你在本文讨论的任何脚本中看到列出的模块时，你可以使用随标准 Perl 一起发布的 CPAN 模块将该模块添加到你的系统中。

**注意**：Windows 版的 Apache 用户应查阅 Perl 文档了解如何使用 CPAN 模块，因为这不同于本文讨论的标准方法。有关详细信息，请参阅本书中 Windows 特定部分。

例如，假设你看到一个脚本列出了一个名为 HTML::Template 的模块，你希望安装此模块以便运行使用它的脚本。要安装 CPAN 模块，请以 root 用户身份从命令行提示符运行 `perl -MCPAN -e shell`。

**注意**：如果你是第一次运行 `perl -MCPAN -e shell` 命令，系统将要求你配置当前的 CPAN.pm 模块，该模块用于安装其他 CPAN 模块。只需按照说明和提示配置 CPAN.pm 模块，然后继续以下讨论。

在到达 CPAN 提示符后，运行 `install HTML::Template` 命令来安装该模块。CPAN 模块将为你安装此模块。如果它对依赖性发出警告，你可能需要在安装依赖其他 CPAN 模块的模块之前先安装其他一些模块。完成后，从 CPAN 提示符运行 `quit` 返回 shell。

**提示**：如果你不想使用 `perl -MCPAN -e shell` 运行交互式 CPAN shell 来安装模块，可以改为运行 `perl -MCPAN -e ‘CPAN::Shell->install(module_name)’`。例如，`perl -MCPAN -e shell ‘CPAN::Shell->install(HTML::Template)’` 将安装 HTML::Template 模块。你也可以从 shell 脚本中运行此命令。

## 分析一个简单的 CGI 脚本

CGI 脚本通常用于获取用户输入并根据输入执行一个或多个操作，然后在 HTML 页面中返回结果。在本节中，我将向你展示如何创建一个简单脚本来入门并理解 CGI 脚本编写的概念。我们将在这里开发的脚本将执行单一任务：它将获取用户的完整姓名，正确地格式化它，并返回个性化的问候消息。列表 12-2 展示了执行上述功能的 greetings.pl 脚本。

## 列表 12-2: greetings.pl

```
#!/usr/bin/perl
#
#    Name: greetings.pl
#
#    Purpose:
#
#    Show a greeting message
#
######################################################

use strict;
use CGI;

#
# Get user data
#
my $query = new CGI;
my $name = $query->param('name');

#
# Process data
#
$name         = lc($name);
my @strArray = ();


foreach my $str (split(/ ,.$name)) {
    push(@strArray, ucfirst($str));
}

my $formattedName = join(' ', @strArray);

#
# Display results
#
print $query->header;
print $query->start_html('Greetings');
print $query->p('Hello ' . $formattedDName . ',');
print $query->p('Thanks for coming to our Web site.');
print $query->end_html;

#
# Terminate
#
exit 0;
```





现在，让我们仔细研究一下这个脚本。第一行是一个特殊的行：

```
#!/usr/bin/perl
```

这一行告诉系统在执行此脚本时运行 Perl。如果你将 Perl 安装在了非标准目录中，则必须相应地修改这一行。例如，如果你将 Perl 安装在 /usr/local/bin/perl，则必须将此行修改为反映该路径。除了第一行外，所有以 # 符号开头的行都会被注释掉，并被 Perl 忽略。

下一个代码段是：

```
use strict;
use CGI;
```

`use strict` 是一个 Perl 编译指令（可以将 pragma 视为指令），它告诉 Perl 评估脚本中是否存在不安全的编程习惯。下一行告诉 Perl 加载一个非常流行的模块，该模块现在是标准 Perl 发行版的一部分，名为 CGI.pm 的模块，它使得编写 CGI 程序变得非常简单。该模块处理所有底层细节，包括获取由 Apache 服务器通过 STDIN 传递给脚本的输入数据、解析和解码输入字段、提供用于显示内容头、创建 HTML 内容等方法。它简直就是为你提供的超强力 CGI 模块。任何人如果不使用 CGI.pm 模块就不应该编写 Perl CGI 脚本。该规则唯一的例外是，如果你受限于资源，不希望每次调用脚本时都加载一个大模块。但在大多数情况下，这都不是问题，尤其是考虑到我不建议在高流量网站上使用 CGI 解决方案。

下一个代码段是：

```
my $query = new CGI;
my $name = $query->param('name');
```

这里创建了一个名为 `$query` 的新 CGI 对象，并调用 `$query` CGI 对象的 `param()` 方法来获取用户输入 `'name'` 的值。该输入值存储在 `$name` 变量中。例如，如果 greetings.pl 脚本按以下方式调用：

```
http://www.domain.com/cgi-bin/greetings.pl?name=kabir
```

那么 CGI 对象将从 Apache 服务器接收 `name=kabir` 作为用户输入，并且脚本能够通过 `$query->param('name')` 方法调用访问该值（'kabir'），就像在这个脚本中所做的那样。

下一个代码段是脚本的核心；它是下面显示的处理块：

```
$name = lc($name);
my @strArray = ();
foreach my $str (split(// , $name)) {
    push(@strArray, ucfirst($str));
}
my $formattedName = join(' ', @strArray);
```

在这里处理 `$name` 变量。第一行使用 Perl 内置的 `lc()` 函数，该函数将给定的字符串转换为小写。由于将 `$name` 字符串作为参数传给 `lc()`，它返回名字的小写值，我们将其存储回 `$name` 变量中。我们将名字转换为小写，以便仅将每个名字的首字母大写。例如，名为 Carol Godsave 的用户可能输入其名字的许多不同组合。例如：

- Carol Godsave
- CAROL GODSAVE
- carol godsave
- carol GODSAVE
- cAROL GoDSave
- carol GoDsAvE

如你所见，用户可以输入这些字母组合中的任意一种或许多其他组合来表示她的名字。然而，我们希望显示 “Carol Godsave”，因为这是她名字的规范格式。因此，我们的处理代码块使用以下算法：

1.  将名字转换为小写。这实际上将 Carol 输入的任何名字内容都变成 `carol godsave`。
2.  按空格字符拆分每个单词。这给我们 `carol` 和 `godsave`。
3.  仅将每个部分的首字母大写。这给我们 `Carol` 和 `Godsave`。
4.  通过空格字符将各部分连接起来。这返回 `Carol Godsave`，正是我们想要的结果。

在这个代码段中，我们使用了一个名为 `@strArray` 的数组，我们将其初始化为空列表。然后使用 foreach 循环遍历使用 Perl 中找到的 `split()` 函数拆分的名字各部分。`split()` 函数以两个参数调用：分隔符，在这种情况下是正则表达式格式 `/ /` 表示的空白字符，以及需要拆分的字符串，在这种情况下是 `$name`。`split()` 函数在数组中返回拆分后的各部分。因此，实际上，在 Carol 的情况下，foreach 循环看起来像这样：

```
foreach my $str ('carol', 'godsave') {
    push(@strArray, ucfirst($str));
}
```

该循环遍历每个部分，并使用内置的 `ucfirst()` 函数调用将每个部分的首字母大写。当给 `ucfirst()` 一个字符串参数时，它仅将首字母大写并返回修改后的字符串。例如 `ucfirst('carol')` 将返回 `Carol`；同样，`ucfirst('godsave')` 返回 'Godsave'。每个修改后的名字部分都存储在名为 `@strArray` 的数组中。例如，在处理完 Carol 的名字后，`@strArray` 是一个数组 = ('Carol', 'Godsave')。最后，我们将名字的每一部分连接到一个名为 `$formattedName` 的新变量中以形成完整的名字。使用内置的 `join()` 函数在 `join(' ', @strArray)` 调用中通过空白字符连接 `@strArray` 的每个元素。现在我们有一个格式化后的名字存储在 `$formattedName` 变量中，只需要显示它即可。

```
print $query->header;
print $query->start_html('Greetings');
print $query->p('Hello ', $formattedName, '.');
print $query->p('Thanks for coming to our Web site.');
print $query->end_html;
```

该段中的第一行设置内容头。需要 Content-Type 头。客户端使用此头来确定如何显示服务器发送的内容。由于 CGI 脚本生成内容，它必须告诉服务器它传递给服务器以发送给客户端的内容类型是什么。

CGI 模块提供了一个名为 `header()` 的方法，它创建适当的 Content-Type 头。例如，`$query->header;` 返回 `Content-Type: text/html; charset=ISO-8859-1`。当在不带特定类型参数的情况下调用 `header()` 时，它默认为 `text/html` Content-Type。然而，如果你的脚本需要输出其他类型，例如 `text/plain`，你可以使用 `header(-type => 'text/plain')` 参数代替。例如：

```
#!/usr/bin/perl
use CGI;
my $query = new CGI;
print $query->header(-type=>'image/gif');
open(GIF, "/tmp/weather.gif");
while(<GIF>){ print;}
close(GIF);
```

这个小脚本使用 `Content-Type: image/gif` 头显示一个名为 /tmp/weather.gif 的 GIF 文件。现在回到 greetings.pl 脚本。在显示默认内容头之后，脚本使用 CGI 模块的 HTML 方法，如 `start_html()`、`p()` 和 `end_html()`，来创建 HTML 内容。例如，假设 Carol 输入以下 URL：

```
http://server/cgi-bin/greetings.pl?name=carol godsave
```

她的 Web 浏览器会自动将 carol 和 godsave 之间的空格编码为 %20（十六进制数 20，等同于十进制数 32，即 ASCII 空格字符）。CGI 模块的一个优点是它处理了解码，并给脚本提供 `Carol Godsave` 作为名字。脚本显示的页面如 图 12-4 所示。

```
Hello Carol Godsave.
Thanks for coming to our Web site.
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_378_0.png)

`p()` 方法创建一对 HTML 段落标签，用于包裹其接收的参数。例如，第一个 `p()` 调用：

```
print $query->p( 'Hello ' . $formattedName . ',');
```

转化为：

```
<p>Hello Carol Godsave,</p>
```

发送到 Web 浏览器的整个输出文档看起来像这样：

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE html
      PUBLIC "-//W3C//DTD XHTML Basic 1.0//EN"
      "http://www.w3.org/TR/xhtml-basic/xhtml-basic10.dtd">

<html xmlns="http://www.w3.org/1999/xhtml"
      lang="en-US">

<head>
   <title>Greetings</title>
</head>
<body>

<p>Hello Carol Godsave,</p>
<p>Thanks for coming to our Web site.</p>

</body></html>
```

`start_html()` 方法产生以下内容：

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE html
      PUBLIC "-//W3C//DTD XHTML Basic 1.0//EN"
      "http://www.w3.org/TR/xhtml-basic/xhtml-basic10.dtd">

<html xmlns="http://www.w3.org/1999/xhtml"
      lang="en-US">

<head>
```




请注意传递给该方法的标题 `Greetings`。这两个 `p()` 方法生成了以下内容：

```html
<p>Hello Carol Godsave.</p>
<p>Thanks for coming to our Web site.</p>
```

最后，`end_html()` 方法生成了以下内容：

```html
</body></html>
```

这标志着 HTML 文档的结束。

细心的读者会注意到，我们违反了第一条 CGI 编程风格指南，该指南指出我们应该将内容与逻辑分离。这个小脚本在脚本内部包含了 HTML，这使得非程序员更难以对其进行修改。但这个脚本仅被用作一个练习。在下一节中，我将介绍一个有用的、生产级别的脚本，它符合风格指南的要求。

## 创建一个基础的 Web 表单处理器

大多数常见的 CGI 脚本被用作 Web 表单的后端。几乎每个 Web 网站都有一个 Web 表单，用于获取用户输入并将其存储在文件或数据库中。在以下部分，我将介绍一个高度可定制的 CGI 脚本，它可以处理几乎所有单页 Web 表单。

## 基础 Web 表单处理 CGI 脚本的特性

假设你的网站有一个或多个 Web 表单，需要从 Web 访客那里收集数据并将其存储在文件或数据库中。基于 CGI 脚本的一种解决方案具有以下特性：

- **支持多个 Web 表单：** 单个脚本即可处理多个单页 Web 表单。单页 Web 表单在一页中询问所有问题。有时你会被要求构建多页 Web 表单，这属于自定义表单处理应用程序的范畴。此类表单处理应用程序通常使用自定义业务逻辑来显示多个表单，超出了本书的范围。根据多年的 Web 开发经验，我的个人建议是避免使用多页 Web 表单，因为当被要求回答一长串问题时，人们往往会感到气馁。此外，在设计单页 Web 表单时，不要问太多的问题。在获取新潜在客户时，将数据收集控制在最少限度是一种良好的做法。经验告诉我，巨大的表单或多页表单会话往往会让新潜在客户和潜在客户失去兴趣，甚至决定完全放弃与该网站做生意。
- **集中配置所有 Web 表单：** 该脚本使用一个支持多个 Web 表单的配置文件。每个 Web 表单的配置可以单独存储在这个标准配置文件中，这意味着你可以集中管理表单配置信息——这对于繁忙的系统管理员来说是一件非常好的事。
- **使用逗号分隔值 (CSV) 文件进行数据存储：** 该脚本允许你将数据保存在 CSV 文件中。每个表单都可以拥有自己的 CSV 文件。你还可以指定字段的顺序以及你想要存储哪些字段。

为了使学习这个 CGI 脚本的过程更简单且更贴近实际，我将假设你有一个名为 `register.html` 的用户注册 Web 表单，如清单 12-3 所示。

### 清单 12-3: register.html

```html
<html>

<body bgcolor="white">

<font face="Arial" size=+1>User Registration Form</font><br>
<p>
<form action="/cgi-bin/formwizard.pl" method="POST">

<table border=0
    cellpadding=3
    cellspacing=0
    bgcolor="#000000">
<tr>
<td>

<table border=0
    cellpadding=5
    cellspacing=5
    bgcolor="#abcdef">

<tr>
<td> Name </td>
<td> <input name="name" type=text size=30 maxsize=50> </td>
</tr>

<tr>
<td> Email </td>
<td> <input name="email" type=text size=30 maxsize=50> </td>
</tr>

<tr>
<td> Zipcode</td>
<td> <input name="zipcode" type=text size=30 maxsize=50> </td>
</tr>

<tr>
<td> Can we send you junk mail?</td>
<td>
<input type=radio name="opt-in" value="yes">Yes, Please!
<input type=radio name="opt-in" value="no">No, Never!
</td>
</tr>

<tr>
<td align=center> <input type-submit value="Register Me"</td>
<td align=center> <input type=reset> </td>
</tr>

</table>
</td>
</tr>
</table>
</form>
<p>
</html>
```

该 Web 表单显示效果如图 12-5 所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_381_0.png)

**图 12-5：** Web 浏览器中的 register.html 表单。

这个示例 Web 表单有四个数据字段：name、email、zipcode 以及一个选择问题。这是一个典型的用户注册表单，除了大多数网站不会像这个表单中（诚实地）那样提出选择问题外。当用户填写完此表单后，数据必须存储在文件中，并且向用户显示感谢消息或将其导向一个新页面。例如，如果上述表单被填写，它可以显示如图 12-6 所示的感谢消息。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_382_0.png)

**图 12-6：** 填写 *register.html* 后的感谢消息。

## 使用 Perl 开发 Web 表单处理器 CGI 脚本

现在让我们开发一个 Perl CGI 脚本，使你能够创建如图 12-7 所示的 Web 表单处理解决方案。图 12-7 展示了此类 CGI 解决方案的流程图。

*formwizard.pl* 脚本随 CDROM 一起提供。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_382_1.png)

当该脚本作为 *register.html* 中的表单操作被调用时，如下所示：

```html
<form action="/cgi-bin/formwizard.pl" method="POST">
```

该脚本执行以下任务：

1. 加载所有外部标准（即标准 Perl 发行版的一部分）以及其他 CPAN 模块。
2. 加载中央配置文件，该文件应包含针对向其提交数据的特定 Web 表单的配置。
3. 创建一个 CGI 对象，使其能够检索提交的数据并访问 Web 服务器提供的其他信息。
4. 确定激活该脚本的 Web 表单是否在中央配置文件中拥有配置。如果没有，则简单地显示一条错误消息，说明该表单无法由此脚本处理。如果存在配置，则开始处理表单。
5. 作为第一步处理，脚本验证用户数据。这一步涉及根据配置文件中列出的要求检查数据的有效性，并对用户提供的数据字段进行健全性检查。
6. 如果验证步骤没有返回错误，数据将存储在数据文件中。另一方面，如果数据验证步骤因用户错误而失败，则会显示特定于错误类型的错误消息并中止处理。
7. 如果上一步成功，脚本将显示感谢消息或将用户重定向到另一个 URL，然后终止。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_383_0.png)

**图 12-7：** CGI Web 表单处理流程图。

## 查看 formwizard.pl

*formwizard.pl* 脚本实现了此流程图。在 *formwizard.ini* 配置文件中，*register.html* 的字段具有以下限制：

- *name* 字段是必填项，长度设置为 3 到 50 个字符。字段值必须由 a 到 z 的字母和句点组成。如果字段值通过长度和模式测试，它将被存储为一个字符串，其中每个单词的首字母大写。
- *email* 字段也是必填项，长度必须在 6 到 100 个字符之间。电子邮件地址中可接受的字符包括 a 到 z、0 到 9、破折号 (-)、下划线 (_)、句点和 at 符号 (@)。*email* 模式测试应用于该字段的值，如果所有（长度、字符集和模式）测试均通过，则值以小写格式存储。
- zipcode 字段被视为可选的数字字段，如果用户输入了值，则必须通过 us_zipcode 模式测试。us_zipcode 模式测试仅检查输入的数字是五位数，还是由一个五位数和一个四位数组成的邮政编码，如 95825-1234。仅允许使用的字符是 0 到 9 和破折号。
- 最后，opt-in 字段被视为必填的文本字段，其值只能是 'yes' 或 'no'。

## 清单 12-4: formwizard.ini 配置文件

```ini
# --------------------------------------------------------
#
# Web Form Configuration for *** register.html *** form
#
# --------------------------------------------------------

[register.html]
template_dir = /www/asb2/ch12/forms/register

# --------------------------------------------------------
# After the form is processed, the script must acknowledge to
# the user that the system received the data. This is done
# using a "Thank You" (called thankyou hereafter)
# message.
#
# Set the name of the thankyou template here
# --------------------------------------------------------
thankyou_template = thanks.html

#
# --------------------------------------------------------
# If you wish to redirect the user to another URL,
# set the URL here. Do not set this to any URL
# if you wish to show the thankyou message instead
#
# If the URL is set, it is always used instead of
# showing the thankyou message.
# --------------------------------------------------------
thankyou_redirect_url = /asb2/ch12/forms/feedback.html

#
# --------------------------------------------------------
# The script will either show the thankyou message or
# redirect the user to another URL.
# If you wish to send data to the redirect URL via GET method
# set this to 'yes'; otherwise, set it to 'no'.
# --------------------------------------------------------
send_data_on_redirect = no

#
# --------------------------------------------------------
# Having a specific list of form fields
# ensures that we only use what we need.
# We will ignore any additional field(s)
# --------------------------------------------------------
```




### 分析 formwizard.ini

现在，让我们更仔细地查看此脚本，以便你可以根据具体需求进行配置。

第一行是一个特殊行：

```
#!/usr/bin/perl
```

此行告知系统在执行此脚本时运行 Perl。如果你将 Perl 安装在非标准目录中，则必须相应地更改此行。例如，如果你将 Perl 安装在 /usr/local/bin/perl，则需将此行修改以反映该路径。

下一段代码块是：

```
use strict;
use Config::IniFiles;
use File::Basename;
use HTML::Template;
use Fcntl qw(:DEFAULT :flock);
use CGI;
```

这将加载所有必要的标准模块和 CPAN 模块。此脚本使用的 CPAN 模块包括 `Config::IniFiles`、`HTML::Template` 和 `CGI`。实际上，`CGI` 模块现在作为标准 Perl 模块发行，但你必须使用 `CPAN` 模块安装其他两个模块。以下是两个快速命令，可以在 *root* shell 中为你安装这些模块：

```
perl -MCPAN -e 'CPAN::Shell->install('Config::IniFiles')'
perl -MCPAN -e 'CPAN::Shell->install('HTML::Template')'
```

你也可以运行

```
perl -MCPAN -e 'CPAN::Shell->install('CGI')'
```

以确保你的 `CGI.pm` 模块是 CPAN 网络上的最新版本。

下一段代码是

```
my $cfg      = new Config::IniFiles -file => "formwizard.ini";
my $query    = new CGI;
my $formName = get_form_name($ENV{HTTP_REFERER});
```

此段代码创建了一个名为 `$cfg` 的配置对象，该对象加载了 `formwizard.ini` 文件。`formwizard.ini` 文件是此脚本的核心配置文件，它必须与 CGI 脚本 *formwizard.pl* 位于同一目录中。如果你希望将其保存在与 CGI 脚本不同的目录中，你需要更改路径。例如，若要将在目录 /www/myscripts/conf 中存储配置文件，请按如下方式修改脚本：

```
my $cfg      = new Config::IniFiles
                 -file => "/www/myscripts/conf/formwizard.ini";
```

确保 Apache 用户（即在 `httpd.conf` 文件中 *User* 指令中使用的用户）可以读取该配置文件。脚本创建的 `CGI` 对象称为 `$query`。接下来，脚本调用一个名为 `get_form_name()` 的子例程，以获取调用它的 Web 表单的名称。该子例程为：

```
sub get_form_name {
    my $referrer = shift;

    # If the HTTP referrer has a query string in it
    # return only the non-query string part of it
    #
    if ($referrer =~ /\?/) {
        ($referrer, undef) = split(/\?/,$referrer);
    }

    return basename($referrer);
}
```

调用此子例程时，它会从 CGI 环境变量 `HTTP_REFERER` 获取值。此变量被设置为调用该脚本的 URL。例如，如果 `register.html` 表单可以通过 `http://rhat.mitec.com/asb2/chi2/forms/register.html` 这样的 URL 访问，那么当它被提交给 `/cvs.dll/formwizard.pl` 脚本时，CGI 对象 $query 会将 `HTTP_REFERER` 设置为 `http://rhat.mitec.com/asb2/chi2/forms/register.html`。`get_form_name()` 代码返回 URL 中的 `register.html` 部分。

然后，脚本将 Web 表单名称存储在一个名为 `$formName` 的全局变量中。

下一段代码是：

```
my $templateDir = $cfg->val($formName, 'template_dir');
my @fieldInfo = $cfg->val($formName, 'form_field_info');
```

此段代码将 Web 表单名称作为节名传递给配置对象，并检索当前 Web 表单的模板目录和表单字段信息的配置信息。这些信息分别存储在 `$templateDir` 和 `@fieldInfo` 数组中。配置文件示例 `formwizard.ini` 在列表 12-4 中展示，该列表显示了名为 `register.html` 的 Web 表单的示例配置。配置文件格式非常简单：

```
[section1]
key1 = value
key2 = value
key3 = value

key4 = <<MULTIPLE_VALUES
value1
value2
value3
...
valueN
MULTIPLE_VALUES
...
keyN = value
[section2]
```

这种类型的配置文件在 Windows 世界中很常见，通常被称为 “.ini” 文件。因此，我们在此使用的模块称为 `Config::IniFiles`。在我们的示例 `formwizard.ini` 文件中，节名实际上是 Web 表单 `register.html` 的名称。`$templateDir` 变量和 `@fieldInfo` 数组是从以下配置行设置的：

```
[Register.html]

template_dir = /www/asb2/chi2/forms/register
form_field_info=<<FORM_FIELDS
name,text,required,max_chars=50,min_chars=3,case=ucfirst,exclude_regex=[^a-z .],pattern=none
email,text,required,max=100,min=6,case=lowerall,exclude_regex=[^a-z0-9._@],pattern=email
zipcode,number,optional,pattern=us_zipcode,exclude_regex=[^0-9]
opt_in,text,required,case=lower,pattern=none,valid_data=yes||no
FORM_FIELDS

# When data entry error(s) occur, a pop-up message is displayed.
# The message lists the field(s) that are missing or invalid.
#
# You can personalize the ACTION of the message. In other words,
# enter text tells the user to
# make corrections and resubmit.

data_error_msg = Please enter missing data and resubmit.

# Specify the
data_directory=/tmp
data_filename=registration.csv
data_field_separator=,
data_field_order=email,name,zipcode,opt-in
```

配置文件中的 template_dir 行被设置为一个目录，其中保存了此 Web 表单 (register.html) 的 HTML 模板。在脚本的当前版本中，我们唯一使用的模板是感谢页面的 HTML 模板，因此它保存在此目录中。

form_field_info 配置是键值对概念的扩展版本。在这里，单个键 form_field_info 具有许多值。这些值是位于 FORM_FIELDS 字符串之间的行。每个值行包含多个字段。例如：

```
name, text, required, max_chars=50, min_chars=3, case=ucfirst, exclude_regex=[^a-z .],
 pattern=none
```

在这里，表单字段名称在 register.html 中可见，如下所示：

```
<input name="name" type=text size=30 maxsize=50>
```

为了控制用户输入，脚本为每个输入字段使用一组参数。这些参数在表 12-1 中讨论。每个参数用逗号分隔，并如下存储在配置文件中：

```
form_field_info=< FORM_FIELDS
  fieldName1, parameter1, parameter2, parameter3, ..., parameterN
  fieldName2, parameter1, parameter2, parameter3, ..., parameterN
  fieldName3, parameter1, parameter2, parameter3, ..., parameterN
  ...
  fieldNameN, parameter1, parameter2, parameter3, ..., parameterN
FORM_FIELDS
```

**表 12-1**
**配置文件中的用户输入控制参数**

| 参数 | 示例 | 说明 |
|---|---|---|
| text | name, text | 此参数表示命名字段是一个字符字符串。 |
| number | zipcode, number | 此参数表示命名字段是一个数字。 |
| required | name, required | 此参数表示命名字段是一个必填输入字段。如果此字段缺少值，或值无效，则需要显示错误消息，并且必须终止表单处理。 |
| optional | zipcode, optional | 此参数表示命名字段是一个可选输入字段。如果此字段缺失，表单处理仍将继续。 |
| max_chars=n | name, max_chars=50 | 允许用于命名输入字段的最大字符数。如果用户输入的字符数超过指定数量，将显示错误消息。 |
| min_chars=n | name, min_chars=3 | 允许用于命名输入字段的最小字符数。如果用户输入的字符数少于指定数量，将显示错误消息。 |
| case= ucfirst \| upper \| lower \| lcfirst | name, case=ucfirst | 在存储命名字段之前，脚本使用指定功能格式化该字段。例如：<br>`ucfirst`：将表单字段的值格式化为仅首字符大写。这在存储姓名时很有用。<br>`upper`：将表单字段的值格式化为全大写。<br>`lower`：将表单字段的值格式化为全小写。<br>`lcfirst`：将表单字段的值格式化为仅首字符小写。 |
| exclude_regex=[character set] | name, exclude_regex=[^a-z .] | 允许作为命名表单字段值的唯一字符。其他所有字符都被排除。<br>当值包含被排除的字符时，会生成错误消息。 |





### 表 12-1（续）

| 参数 | 示例 | 说明 |
| :--- | :--- | :--- |
| pattern-none | *email*, pattern=*email* | pattern 参数指定了需要考虑的特殊模式，针对具名的表单字段。如果字段值与指定的模式不匹配，则会被拒绝并生成错误消息。e-mail 模式指定了具名字段（*email*）的值将被检查是否为有效的电子邮件地址。支持的模式有：`none`、`email`、`us_zipcode` 和 `large_plain_text`。你可以向脚本中添加一个新的模式检查子例程，称为 `sub check_newpattern ( # 你的检查代码 )`，以支持其他类型表单字段的新型模式。 |
| valid_data=*value1*\|*value2* | opt-in, valid_data=*yes*\|*no* | 此参数用于只能具有指定值之一的文本字段，这些值由 `\|` 字符分隔。在此处，*opt-in* 字段只能具有 '`yes`' 或 '`no`' 的值。 |

在表单字段信息被加载到 `@fieldInfo` 数组后，下一个代码段如下所示，它检查配置文件是否包含模板目录（即 `$templateDir` 变量的值），或者 `@fieldInfo` 数组是否为空。

```perl
if ($templateDir eq '' || @fieldInfo < 1) {
    print $query->header;
    print alert("Sorry, $formName is not managed by this script.");
    exit 0;
}
```

执行这些测试是为了确定当前表单是否在 `formwizard.ini` 文件中配置。如果未配置，脚本将返回一条错误消息，指出该具名表单未由脚本管理，并终止程序。如果 Web 表单在 `formwizard.ini` 文件中配置正确，脚本将继续执行下一个代码段：

```perl
my @errors = validate_data(\@fieldInfo);
if ($#errors >= 0) {
    print $query->header;
    print alert(join("\n", @errors) . "\n\n");
    exit 0;
}
```

在此，脚本调用 `validate_data()` 子例程，将 `@fieldinfo` 数组引用传递给它，以验证输入的用户数据没有错误。该子例程执行以下操作：

- 1. 它遍历在 `@fieldinfo` 数组中（作为引用传递给子例程）找到的每个表单字段的具体信息，并获取字段名称、字段类型、字段要求等。
- 2. 对于每个表单字段，它使用 `$query->param($fieldname)` 方法从 `$query` 对象中获取值。该值存储在 `$value` 变量中。
- 3. 如果该字段是必需的且值为空，则错误消息被存储在 `@errors` 数组中，循环继续处理下一个字段。如果该字段是可选的且用户未输入值，循环继续处理下一个字段。
- 4. 当存在值时（无论是必需字段还是可选字段），都会调用 `check_data_field()` 子例程，以验证该值是否符合配置文件中陈述的字段要求。
- 5. 如果字段值通过了由 `check_data_field()` 子例程执行的验证检查，则根据配置要求更改该值的大小写。换句话说，该值要么转换为大写，要么转换为小写，要么保持混合大小写，并使用 `$query->param()` 方法存储在 CGI 对象中。`check_data_field()` 例程返回一个错误列表（如果有）。
- 6. 如果 `check_data_field()` 子例程返回了错误，脚本使用 `alert()` 子例程显示错误消息并中止。另一方面，如果没有错误需要报告，脚本继续使用 `write_data()` 子例程将数据写入磁盘。`write_data()` 使用配置文件中的数据文件名。完全限定的数据文件路径基于配置参数 `data_directory` 和 `data_filename`。该例程按照 `data_field_order` 配置参数中给出的顺序，使用 `data_field_separator` 参数中命名的字段分隔符，写入用户输入的大写修改后的数据。请注意，数据文件仅以追加模式打开，并且在文件操作期间它是独占锁定的，以便在此期间没有其他 `formwizard.pl` 副本可以访问它。
- 7. 然后，脚本使用在 `formwizard.ini` 中发现的 `thankyou_redirect_url` 配置选项来确定是否应将用户重定向到另一个 URL，或是否应向用户显示致谢消息。如果配置文件中的 `thankyou_redirect_url` 不为空，脚本使用 `redirect_data()` 子例程将用户重定向到指定的 URL。`redirect_data()` 子例程将所有表单字段作为键值对打包在 URL 中，并将用户的 Web 浏览器重定向到该 URL。例如，如果 `register.html` 填写为 name=محمد كبريت, zipcode=95833, email=MRKABILRO@gmail.com 和 optin=yes，并且 `thankyou_redirect_url` 设置为 http://www.domain.com/friends.pl，那么 `redirect_data()` 子例程将 Web 浏览器重定向到：

`http://www.domain.com/friends.pl?name=Mohammed%20Kabir&zipcode=95833&email=mrkabir@hotmail.com&opt-in=yes`

这使得远程站点能够通过 HTTP GET 方法接收清理过的用户数据。请注意，如果你只是想将用户重定向到另一个页面而不通过 GET 提交数据，请将配置文件中的 `send_data_on_redirect` 参数设置为 `no`。

- 8. 如果未设置 `thankyou_redirect_url`，脚本使用 `thankyou_template` 配置参数从配置文件中加载**致谢模板文件名**。假设该模板位于由 `template_dir` 配置参数指向的模板目录中。脚本使用 `show_thanks()` 子例程显示致谢页面。`show_thanks()` 子例程通过用用户输入（但已清理）的数据字段值替换特殊标记来个性化**致谢**内容。这是通过创建一个 `HTML::Template` 对象实例来实现的，该对象通过 `thankyou_template` 参数指向的模板页面进行初始化。称为 `$template` 的 `HTML::Template` 对象使用其 `$template->param()` 方法用通过 `$query->Vars()` 方法创建的哈希来替换特殊标记。最后，显示脚本的输出，脚本终止。

此示例中使用的致谢模板如清单 12-5 所示。

### 清单 12-5: thankyou.html 页面

```html
<html>
<body bgcolor="white">
<font face="Arial" size=+1>User Registration Complete</font><br>
<p>
<form action="CTMPL_VAR name=REFERER" method="GET">
<table border=0 cellpadding=3 cellspacing=0 bgcolor="#000000">
<tr>
<td>
<table border=0 cellpadding=5 cellspacing=5 bgcolor="#abcdef">
<tr>
<td>
<TMPL_VAR NAME=name>, <p>
Thank you for taking the time to register. We will send you information via
<TMPL_VAR NAME=email>.  
</td>
<tr>
<td align=center> <input type=submit value="Return"</td>  
</tr>
</table>
</td>
<tr>
</table>
</form>
<p>  
</html>
```

请注意此 HTML 模板中的 `<TMPL_VAR NAME=name>` 和 `<TMPL_VAR NAME=email>` 标记。这两个标记将被用户输入的 **name** 和 **email** 字段值替换。请记住，在数据验证期间，脚本会更新用户输入字段的大小写，以便显示的实际值格式良好，这在向用户显示信息时非常有用。因此，用户可以在名称字段中输入 **carol godsave**，但致谢页面将显示 **Carol Godsave**，这应该比按原样显示数据让用户更满意。这是四次 `register.html` 表单提交后的一个示例数据文件。

```text
kahir@domain.com,Mohammed J. Kabir,12345,no
carol@domain.com,Carol Godsave,95833,yes
joegunchy007@aol.com,Joe Gunchy,07024,yes
jennygunchy007@aol.com,Jennifer Gunchy,07024,no
```

## 使用 formwizard.ini 管理 Web 表单

如前几节所述，使用 `formwizard.ini` 配置文件的 `formwizard.pl` 脚本非常可配置，并且允许你使用单个脚本和单个集中配置文件来管理许多单页 Web 表单。要管理新的 Web 表单，只需复制 `register.html` 的配置文件，并在 `formwizard.ini` 文件中创建一个新的部分。以下是使用此脚本管理名为 **feedback.html** 的 Web 表单所需执行的步骤。

- 1. 在 `formwizard.ini` 文件中创建一个新的部分，称为 `[feedback.html]`，如下所示：

```ini
[register.html]
template_dir        = /path/to/feedback/template/dir
```



thankyou_template = thanks.html
send_data_on_redirect = no
form_field_info=<<FORM_FIELDS
#
# insert field info here
#
FORM_FIELDS

data_error_msg = 请输入缺失的数据并重新提交。
data_directory=//feedback/data/directory
data_filename=feedback.csv
data_field_separator=,
data_field_order=此处填写逗号分隔的字段列表

通过查看 [register.html] 部分进行必要的更改。

2. 将反馈表单的 action 行更改为

<form action="/c/s.dll/formwizard.pl" method="POST">

3. 在 [feedback.html] 部分中由 template_dir 参数指定的目录中创建 thanks.html 模板。该模板文件应使用 <TMPL_VAR name=fieldname> 标签来个性化感谢信息。

这就是使用 formwizard.pl 管理新 Web 表单的全部内容。对于大多数网站而言，Web 表单管理是 CGI 工作量的重要组成部分，而 formwizard.pl 脚本有助于您集中管理 Web 表单，从而轻松支持这些表单。

**提示** 在开发该脚本期间，我让许多人试用。他们不断发现该脚本的新功能和酷调整。我创建了一个 SourceForge 项目站点，用于发布我在 GNU 通用公共许可证 (GPL) 下发布的所有 CGI 脚本，因此你应该随时可以在 https://sourceforge.net/projects/mkweb/ 上获取此脚本的最新版本。[MK01]

## 创建通过电子邮件发送页面的脚本

许多热门网站都具有让用户通过电子邮件向朋友或同事发送 Web 页面的功能。这类功能有助于网站增加流量，并且经常被市场部门视为一种优秀的病毒营销工具。在本节中，我将向您展示如何在您的网站上添加一个 CGI 脚本，使您的访问者能够通过电子邮件将您的任何 Web 页面发送给其他人。首先，让我们看看其工作原理。

用户可以输入朋友或同事的电子邮件地址，然后单击发送按钮将此 Web 页面发送给可能对此感兴趣的人。页面的实际 HTML 内容并不重要；重要的是这里显示的小嵌入式 HTML 表单：

```html
<form action="/cgin-bin/mime-mail.pl" method="POST">
  <input type=text name="name"   value="your-name" size=12
         maxsize=50>&nbsp;<br>
  <input type=text name="email"  value="friend-email" size=12
         maxsize=100>&nbsp;
  <input type=submit value="Send">
</form>
```

当用户输入其姓名以及朋友或同事的电子邮件地址并单击“发送”时，将调用 /c/s.dll/mime-mail.pl 脚本，该脚本如列表 12-6 所示。

### 列表 12-6: /cgin-bin/mime-mail.pl

```perl
#!/usr/bin/perl -w
#
#
  Name: mime-mail.pl
#
#  Purpose:
#
#  Sends the referrer page via email
#
############################################

use strict;

use CGI;
use MIME::Lite;
use MIME::Lite::HTML;
use Config::IniFiles;
use File::Basename;

#
# Create a CGI object
#
my $query = new CGI;

#
# Create a configuration object by loading the mime-mail.ini
#  file from the physical directory pointed by /cgin-bin/
#
my $cfg     = new Config::IniFiles -file => "mime-mail.ini";

#
# Get the referrer URL
#
my $referrerURL = $ENV[HTTP_REFERER];

#
# Get the referrer page name from the referrer
# information
my $pageName = get_form_name($referrerURL);

#
# Print content type header to be text/html
#
print $query->header;

#
# If the referrer page does not have a [section] in
# the mime-mail.ini file, then use default section
$pageName = 'defaults' if ($cfg->val($pageName, 'from') eq '');

#
# Get the e-mail address. If no e-mail address is supplied,
# show error message
#
my $to = ( $query->param('email') eq '' ||
	! check_email($query->param('email'), 'email')) ?
	abort('Email address is missing.') : $query->param('email');

my $senderName = ( $query->param('name') eq '') ?
	abort('Your name is missing.') : $query->param('name');

$senderName = format_name($senderName);

#
# Create a MIME::Lite::HTML object and initialize
# it with referrer, an
my $mailHTML = new MIME::Lite::HTML 	From: => $senderName . '<' .
			$cfg->val($pageName, 'from') . '>',
			To 	=> $to,
			Subject => $cfg->val($pageName, 'subject');

#
# Parse the referrer URL and create a MIME mail object
#
my $MIMEEmail = $mailHTML->parse($referrerURL);

#
# Send the MIME mail
#
$MIMEEmail->send;

#
#
# Check error string for errors
#
my @errors = $mailHTML->errstr;

#
# If no error found, tell the user that page was
# sent to her friend; otherwise, show error message
#
if ($#errors > -1 ) {
  print abort("Error(s) found: ' . join('\n', @errors));
} else {
  print abort("Page sent to $to.\nThank you.")
}

#
# Terminate
#
exit 0;

sub abort {
  # Print javascript abort message
  print sprintf("<script>alert('$s');history.go(-1);
</script>",shift));
  exit 0;
}

sub get_form_name {
  my $referrer = shift;

  # If the HTTP referrer has a query string in it
  # return only the nonquery string part of it
  #
  if ($referrer =~ /^/()) {
     ($referrer, undef) = split(//?, $referrer);
  }

  return basename($referrer);
}

sub format_name {
  my @str = ();
  foreach my $part (split(\//,shift)) {
    push(@str, ucfirst(lc($part)));
  }
  return join(' ',@str);
}

sub check_email {
    my $email = shift;
    my $fieldName = shift;

    # Special note
    # This e-mail checker routine might return false (0)
    # for some rarely used RFC-compliant e-mail addresses
    # that are not common. For example, bob&sandra@domain.com
    # will fail. If you wish to allow such "technically" valid
    # e-mails, you must modify the regular expressions used
    # in this routine.

    # Untaint e-mail address
    $email =~ /(\S+)@([\w.-]+)/;
    $email = $1 . '@' . $2;

    # Store untainted value in query object
    $query->param($fieldName, $email);

    # Split the user@host e-mail into user and host
    my ($user, $host) = split(@, $email);

    # Return false if host part does not have
    # hostname.domain.tld or domain.tld format
    #
    return ($host !~ /(^[a-z0-9._-]+\.[a-z][2,3])$/i) ? 0 : 1;
}
```

此脚本中正在进行以下操作：

- 该脚本创建一个名为 $query 的 CGI 对象，并在另一个名为 $cfg 的对象中加载 mime-mail.ini 配置文件。然后，它将 HTTP 来源信息存储在名为 $referrerURL 的变量中，并使用 get_form_name() 子例程确定调用此脚本的页面名称。页面名称存储在 $pageName 变量中。
- 使用 $query->header 方法打印默认内容头（text/html）。然后检查该命名页面是否存在配置部分。它使用 $cfg->val($pageName, 'from') 方法在 mime-mail.ini 配置文件中定位名为 'from' 的参数。此参数必须在页面的相应部分中设置。以下是一个 mime-mail.ini 配置文件的示例。

[default]  
subject = A Web page forwarded by a friend
from = webmaster@domain.com

[mybooks.html]  
subject = Check out Kabir's linux books!
from = webmaster@domain.com

例如，如果 CGI 脚本是从类似 http://www.domain.com/mybooks.html 的 URL 调用的，那么脚本将把 $pageName 设置为 ‘mybooks.html’，并使用 $cfg->val($pageName, ‘from’) 方法调用在 [mybooks.html] 部分中查找 ‘from’ 参数。如果该参数因未设置或该部分缺失而缺失，则它将 $pageName 设置为 ‘default’，从而允许它使用 [default] 部分中的参数。因此，如果您不希望为显示通过电子邮件发送页面表单的每个页面定义单独的部分，那么拥有一个 [default] 部分是个好主意。

接下来，脚本确定用户是否输入了电子邮件地址，如果输入了，则检查电子邮件地址是否为 user@host 格式。如果电子邮件缺失或无效，则显示错误消息，脚本使用 abort() 子例程终止。如果接受电子邮件地址，它会检查用户是否在 Web 表单的名称字段中输入了其姓名。如果缺少姓名，则终止。

如果电子邮件地址和姓名均被接受，脚本使用 format_name() 子例程格式化用户名，并创建 MIME::Lite::HTML 对象。此对象使用 From、To 和 Subject 信息初始化。From 地址由用户名和从配置文件读取的电子邮件信息组成。例如，如果名为 John Olson 的用户在 http://www.domain.com/mybooks.html 页面上填写通过电子邮件发送页面表单，脚本将创建 From 头为 John Olson <webmaster@domain.com>。用户的电子邮件地址用于名称中，以告知接收电子邮件的朋友或同事是谁发起了该电子邮件。如果我们还收集了用户的电子邮件地址，我们也可以使用它来设置 From 头。但在两个小文本框中收集用户的电子邮件和朋友们的电子邮件地址可能会变得太令人困惑，如果没有适当的标签，这将占用页面的大量空间；因此，避免使用这种方案。

然后，$mailHTML 对象用于解析来源 URL。在此阶段，CGI 脚本实际上充当嵌入式 Web 客户端，获取来源 Web 页面并创建发送电子邮件所需的 MIME 内容。使用 $mailHTML->send 方法发送电子邮件。使用 $mailHTML->errorstr 方法检测错误并将其存储在 @errors 中。如果没有错误，脚本显示页面已发送的消息并终止；如果有错误，则显示错误消息并终止。




# 在 Apache 中启用 CGI 调试支持

为了帮助 CGI 开发人员，Apache 提供了 CGI 输出日志。对于每个 CGI 程序错误，日志文件包含几行日志条目。前两行包含请求时间、请求 URL、HTTP 状态码、CGI 程序名称等信息。如果 CGI 程序无法运行，会有额外的两行包含错误信息。或者，如果错误是由于脚本返回了错误的头部信息，则信息会记录为：所有 HTTP 请求头部、CGI 程序输出的所有头部，以及 CGI 程序的 STDOUT（标准输出）和 STDIN（标准输入）。如果脚本未能输出任何内容，则不包含 STDOUT。

要在 Apache 中记录 CGI 输出，请使用以下部分中描述的 `mod_cgi` 模块（它是标准发行版的一部分）中的指令。通过这些指令，您可以设置对您正在开发或尝试在系统上安装的 CGI 程序的记录。

## ScriptLog

`ScriptLog` 指令设置 CGI 程序错误的日志文件名。如果日志文件是相对路径（即，不以 / 开头），则被视为相对于由 `ServerRoot` 指令设置的服务器根目录的相对路径。

- 语法：`ScriptLog filename`
- 上下文：Resource config

![](img/e11fcbd2818a3495ac70085e5d8d1c26_400_0.png)

使用此指令时，请确保日志目录可由 `UserDir` 指令指定的用户写入。出于效率或性能考虑，日常使用此指令可能不是一个好主意。我建议仅在需要时使用它，并在调试完成后将其关闭。

## ScriptLogLength

`ScriptLogLength` 指令限制由 `ScriptLog` 指令指定的日志文件的大小。脚本日志文件可以为每个 CGI 错误记录大量信息，因此可能会迅速增长。通过使用此指令，您可以限制日志大小，以便当文件达到最大长度时，不再记录更多信息。

- 语法：`ScriptLogLength size`
- 默认：`ScriptLogLength 10385760`
- 上下文：Resource config

## ScriptLogBuffer

`ScriptLogBuffer` 指令限制被记录的 POST 或 PUT 数据的大小。

- 语法：`ScriptLogBuffer size`
- 默认：`ScriptLogBuffer size 1024`
- 上下文：Resource config

# 调试您的基于 Perl 的 CGI 脚本

如果您使用基于 Perl 的 CGI 脚本，如本章前面所述，除了 Apache 提供的 CGI 日志外，您在故障排除方面还有很多其他帮助。您可以使用著名的 CGI.pm 模块从命令行调试基于 Perl 的 CGI 脚本。或者，您可以将调试消息写入标准错误日志（STDERR）文件，Apache 会自动将其重定向到 Apache 错误日志。我将在以下部分讨论这些技术。

## 从命令行进行调试

如果您使用著名的 CGI 模块，如我在此章中讨论的所有实用 CGI 脚本中所做的那样，那您就很幸运了。CGI 模块使您能够从命令行对 CGI 脚本进行故障排除，这使得调试脚本变得非常方便。让我们看一个名为 badcalc.pl 的示例 CGI 脚本，如清单 12-7 所示。

### 清单 12-7: badcalc.pl

```perl
#!/usr/bin/perl -w
use CGI;

my $query = new CGI;
my $num1 = $query->param('num1');
my $num2 = $query->param('num2');
my $sum = $num1 + $num2;

#print $query->header;
print "$num1 + $num2 = $sum";
exit 0;
```

当通过诸如 http://www.domain.com/cgi-bin/notready.pl 这样的 URL 访问此脚本时，它会返回一个内部服务器错误消息，并在服务器错误日志文件中记录一条错误消息。您想知道为什么这个小脚本不起作用。以下是一个典型的调试会话。

1. 通过将 `use CGI` 行更改为以下内容，启用 CGI 模块的命令行调试：
   `use CGI qw(-debug);`
   这启用了该模块的命令行调试。

2. 作为 root，`su` 切换到 Apache 用户（即您设置 `User` 指令所指向的用户），并从命令行运行该脚本。您将看到此消息：
   `(offline mode: enter name=value pairs on standard input)`
   并且脚本将等待您的输入。

3. 在命令行模式下，在每一行输入 `key=value` 对，以模拟来自 Web 的输入。例如，为了向上述脚本提供输入，一个示例命令行会话看起来类似于这样：
   `(offline mode: enter name=value pairs on standard input)`
   `num1=100`
   `num2=200`
   上述将 `num1` 输入字段设置为 100，将 `num2` 输入字段设置为 200。每个字段在单独的一行中设置一个值。

4. 输入完所有输入后，按 Ctrl+D 终止调试的输入部分，并观察脚本的执行情况。上述输入的完整调试会话如下所示：
   `(offline mode: enter name=value pairs on standard input)`
   `num1=100`
   `num2=200`
   `[control+d]`
   `100 + 200 = 100`
   如您所见，脚本将这两个数字相加并如预期般打印了数据。那么，为什么这个脚本在从 Web 运行时崩溃了呢？嗯，您看到输出之前有任何 `Content-Type` 头部了吗？没有。如果您查看脚本，您会注意到 `print $query->header;` 行被注释掉了。如果您移除注释并在命令行模式下重新运行脚本，您将看到以下内容：
   `(offline mode: enter name=value pairs on standard input)`
   `num1=100`
   `num2=200`
   `Content-Type: text/html; charset=ISO-8859-1`
   `100 + 200 = 100`

## 通过记录日志和调试打印进行调试

这种命令行调试对于小型、不太复杂的脚本非常有用，但如果您有一个相当大的脚本，例如 formwizard.pl，命令行调试就太繁琐了。在这种情况下，您需要结合使用记录日志和调试打印。这是一个名为 calc.pl 的示例脚本，它使用了记录日志和调试打印：

```perl
#!/usr/bin/perl -w

use CGI qw(-debug);

use constant DEBUG => 1;

my $query = new CGI;

my $num1 = $query->param('num1');
my $num2 = $query->param('num2');

print $query->header;

if ($num1 == $num2) {
    # do something useful
    DEBUG and print STDERR "num1 and num2 are same.\n";
} elsif ($num1 > $num2 ) {
    # do something useful
    DEBUG and print STDERR "num1 is greater than num2.\n";
} elsif ($num1 < $num2 ) {
    # do something useful
    DEBUG and print STDERR "num1 is less than num2\n";
}

print $query->start_html('Calculator');
print $query->h1('Calculator');
print $query->p("Number 1: $num1");
print $query->p("Number 2: $num2");
print $query->end_html;

exit 0;
```

当通过诸如 http://www.domain.com/cgi-bin/calc.pl?num1=100&num2=300 这样的 URL 调用此脚本时，它会在该站点的标准错误日志中打印信息。对于上述 URL，错误日志中的条目将类似于：

```
[Tue Mar 20 20:04:26 2001] [error] [client 207.183.233.19] num1 is less than num2
```

以下语句打印此错误消息：

```
DEBUG and print STDERR "num1 is less than num2\n";
```

关于这一行有趣的地方在于，它使用了一个名为 `DEBUG` 的常量，该常量在脚本开头通过以下这行设置：

```
use constant DEBUG => 1;
```

`DEBUG` 和 `print` 语句中的逻辑如下：

- 当 `DEBUG` 设置为 1 或任何非零数字时，它相当于 `DEBUG` 在逻辑运算中获得的“真”值。
- 内置的 `print` 函数在成功打印时总是返回一个非零值。
- 因此，当 Perl 评估 `DEBUG` 和 `print` 时，它会执行 `print` 语句。
- 当 `DEBUG` 设置为 0 时，`DEBUG` 和 `print` 语句不会执行。

这使得您能够插入可以成为代码一部分的 `print` 语句，但在调试完成后可以将其关闭。请注意，`print` 语句写入 `STDERR`，它始终将数据写入网站的错误日志。

要关闭这些语句，您只需将 `DEBUG` 常量设置为 0。现在，有些人可能会认为，当您准备将脚本交给生产环境时，应该完全从脚本中删除这些 `DEBUG` 语句。这种论点的理由是，即使这些 `DEBUG` 语句没有打印任何内容，Perl 仍然会评估它们，从而减慢脚本速度。事实是，在 CGI 解决方案中，速度差异可能并不重要，因为 CGI 脚本本来就比 `mod_perl` 或其他持久化解决方案有更高的开销。但如果您担心这一点，那么在将脚本发送到生产环境之前删除 `DEBUG` 语句。

## 使用 CGI::Debug 进行调试

现在让我们看看另一种调试解决方案。使用 `CGI::Debug` 模块可以在调试您的 CGI 脚本方面获得很多帮助。只需在脚本中的 `use CGI;` 语句后紧接着添加此模块，您就能捕捉到所有类型的错误。例如：

```perl
#!/usr/bin/perl -w
use CGI;
use CGI::Debug;

my $query = new CGI;
```





```perl
my $num1 = $query->param('num1');
my $num2 = $query->param('num2');
```

```perl
#print $query->header;

print $query->start_html('Calculator');
print $query->h1("Calculator");
print $query->p("Number 1: $num1");
print $query->p("Number 2: $num2");
print $query->end_html;

exit 0;
```

我故意注释掉了 `$query->header` 这一行，因为该行通常会在 Web 浏览器上生成内部服务器错误消息。但是，由于我在这个脚本中添加了 `use CGI::Debug;` 语句，当通过 `http://www.domain.com/c/s.dll/cgidebug.pl?num1=1&num2=200` 访问该脚本时，它将显示以下内容：

```text
/cgi-bin/cgidebug.pl

Malformed header!

--- Program output below  ----------------------
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE html
  PUBLIC "-//W3C//DTD XHTML Basic 1.0//EN"
  "http://www.w3.org/TR/xhtml-basic/xhtml-basic10.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en- US"><head><title>Calculator</title>
</head><body><h1>Calculator</h1><p>Number 1: 1</p><p>Number 2: 200</p></body></html>
-----------------------------------------------

This program finished in 0.078 seconds.

Parameters
----------
num1 -- 1[1]
num2 -- 3[200]

Cookies
-------

Environment
-----------
DOCUMENT_ROOT   -- 15[/home/kabir/www]
GATEWAY_INTERFACE = 7[CGI/1.1]
HTTP_ACCEPT = 133[image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, applica]... 
HTTP_ACCEPT_ENCODING = 13[gzip, deflate]
HTTP_ACCEPT_LANGUAGE = 5[en-us]
HTTP_CONNECTION = 10[Keep-Alive]
HTTP_HOST = 14[rhat.nitec.com]
HTTP_USER_AGENT = 50[Mozilla/4.0 (compatible; MSIE 5.5; Windows NT 5.0)]
PATH = 60[/usr/bin:/bin:/usr/sbin:/sbin:/X11R6/bin:/home/kabir/bin]
QUERY_STRING = 15[num1=1&num2=200]
REMOTE_ADDR = 14[207.183.233.19]
REMOTE_PORT = 4[2841]
REQUEST_METHOD = 3[GET]
REQUEST_URI = 36[/cgi-bin/cgidebug.pl?num1=1&num2=200]
SCRIPT_FILENAME = 37[/home/kabir/www/asb2/ch12/cgidebug.pl]
SCRIPT_NAME = 20[/cgi-bin/cgidebug.pl]
SERVER_ADDR = 14[207.183.233.20]
SERVER_ADMIN = 16[you@your.address]
SERVER_NAME = 14[rhat.nitec.com]
SERVER_PORT = 2[80]
SERVER_PROTOCOL = 8[HTTP/1.1]
SERVER_SIGNATURE = 66[<ADDRESS>Apache/2.0.14 Server at rhat.nitec.com Port 80</ADD>... 
SERVER_SOFTWARE = 20[Apache/2.0.14 (Unix)]
```

如您所见，这里有大量的信息，可帮助您快速排查问题并修复脚本。例如，上述程序输出中的一行指出请求头格式错误。

## 13 章

# 服务器端包含 (SSI)

在第 12 章中，我讨论了如何使用 CGI 程序创建动态 Web 内容；然而，有些任务可能不需要开发完整的 CGI 程序，但依然需要一定的动态干预。

例如，假设您希望向所有 HTML 页面添加标准的版权声明；您将如何实现这一点？嗯，您有两种解决方案：

- 将版权声明的内容添加到每个 HTML 页面中。
- 编写一个 CGI 程序，将消息添加到每个 HTML 页面中。

这两个选项都不够优雅。第一个选项要求每当您修改版权声明时，必须手动更新所有文件。第二个选项要求您找到一种方法，在将每个页面发送到 Web 浏览器之前运行您的 CGI 程序。这也意味着每个页面上的每个链接都必须调用这个 CGI 程序，以便它可以向下一个页面附加该消息。像这样的情况需要一个更简单的解决方案。**服务器端包含** (SSI)，即本章的主题，就是那个更简单的解决方案。

### 什么是服务器端包含？

通常，SSI 页面是包含嵌入式命令的 HTML 页面，这些命令用于 Apache Web 服务器。Web 服务器通常不会在将 HTML 页面提供给 Web 浏览器（或任何其他 Web 客户端）之前解析这些页面。但是，在提供之前，Web 服务器始终会解析启用了 SSI 的 HTML 页面，如果发现页面中有任何特殊的 SSI 命令，就会执行该命令。图 13-1 展示了 Web 服务器简化后的 HTML 页面和启用 SSI 的 HTML (SHTML) 页面的传输周期。

# 本章内容

- 理解服务器端包含
- 为服务器端包含配置 Apache
- 在 Web 页面中应用服务器端包含

### 简化的 HTML 传输周期

![](img/e11fcbd2818a3495ac70085e5d8d1c26_408_0.png)

### 简化的 SHTML 传输周期

![](img/e11fcbd2818a3495ac70085e5d8d1c26_408_1.png)

图 13-1：HTML 页面和 SHTML 页面的简化传输周期示意图

如您所见，HTML 页面的 SSI 版本首先会被解析以查找 SSI 命令。这些命令被执行，然后新的输出会被传输到 Web 浏览器（即 Web 客户端）。

Apache 将 SSI 实现为 `INCLUDES` 过滤器。在配置 Apache 以支持 SSI 之前，您需要检查当前的 Apache 可执行文件（`httpd`），以确保其中包含了 `mod_include` 模块。我将在下一节中展示如何执行此操作。

## 为 SSI 配置 Apache

在使用 Apache 进行 SSI 之前，您需要确保已启用 SSI 支持。要了解当前的 Apache 二进制文件中是否内置了 `mod_include`，请从 `/usr/local/apache/bin` 目录或您安装 Apache 二进制文件的任何其他位置运行 `httpd -l | grep include` 命令。这将使您能够查看用于构建 Apache 可执行文件的所有模块列表。默认情况下，应该已经编译了该模块；如果没有，您需要使用 `-enable-include` 选项配置 Apache 源代码，然后重新编译并重新安装 Apache。

虽然标准的 Apache 发行版中默认编译了 `mod_include` 模块，但默认情况下并未启用 HTML 页面的解析。您可以如下一节所述，为整个目录或单一文件类型启用 SSI。

### 为整个目录启用 SSI

若要为名为 `/www/mysite/htdocs/parsed` 的目录启用 SSI，请将以下配置添加到 `httpd.conf` 中：

```apache
<Directory "/www/mysite/htdocs/parsed">
Options +Includes
SetOutputFilter INCLUDES
</Directory>
```

在这里，`Options` 指令设置为 `+Includes`，这启用了该目录中的 SSI 解析。`SetOutputFilter` 指令指示 Apache 解析来自该目录的所有页面以查找 SSI 命令。这意味着该目录中具有任何扩展名的文件都将进行服务器端解析。

例如，假设您具有以下虚拟主机配置：

```apache
<VirtualHost 192.168.1.100>
ServerName wh1.domain.com
DocumentRoot "/www/mysite/htdocs"
ScriptAlias "/cgi-bin/" "/www/mysite/htdocs/cgi-bin/"
<Directory "/www/mysite/htdocs/parsed">
Options +Includes
SetOutputFilter INCLUDES
</Directory>
</VirtualHost>
```

现在，如果 `/www/mysite/htdocs/parsed` 目录中包含任何 `.txt`、`.any`、`.html` 或任何 `.shtml` 文件，以下 URL 请求将被解析：

```text
http://wh1.domain.com/parsed/any.txt
http://wh1.domain.com/parsed/any.shtml
```

在大多数情况下，不需要解析文本文件（`.txt`）或 HTML 文件（`.html`），因为通常不会在这些文件中用于 SSI 命令。因此，除非您有意要解析所有类型的文件，否则上述配置会让 Apache 执行额外的工作。现在让我们看看如何将 SSI 解析限制为特定的文件类型。

### 为特定文件类型启用 SSI

若要限制目录中 SSI 解析的范围，只需使用 `AddType` 指令为启用了 SSI 的文件类型设置所需的 Content-Type 头，然后将 `INCLUDES` 过滤器包裹在 `FilesMatch` 容器中。例如：

```apache
Options +Includes
AddType text/html .shtml

<FilesMatch "\.shtml[.$]">
SetOutputFilter INCLUDES
</FilesMatch>
```

在这里，`Options` 指令设置为 `+Includes`，这启用了 SSI 解析。`AddType` 指令用于将名为 `.shtml` 的文件类型的 Content-Type 头设置为 `text/html`。然后，使用 `FilesMatch` 指令和正则表达式 `"\.shtml[.$]"` 将 `SetOutputFilter` 指令针对 `.shtml` 文件设置为 `INCLUDES`。现在再次查看上一节中的虚拟主机示例。这次让我们添加 `FilesMatch` 容器，如所示：

```apache
<VirtualHost 192.168.1.100>

ServerName vhl.domain.com
DocumentRoot "/www/mysite/htdocs"
ScriptAlias "/cgi-bin/" "/www/mysite/htdocs/cgi-bin/"

<Directory "/www/mysite/htdocs/parsed">
Options +Includes

AddType text/html .shtml

<FilesMatch ".shtml[.$]">
SetOutputFilter INCLUDES
</FilesMatch>

</Directory>

</VirtualHost>
```

现在，如果 `parsed` 子目录中有任何 `.txt`、`.html` 或 `.shtml` 文件，只有以下 URL 请求会告诉 Apache 解析 `.shtml` 文件的输出。

```text
http://vhl.domain.com/parsed/any.shtml
```

服务器不会解析另外两个 URL，即 `http://vhl.domain.com/parsed/any.txt` 和 `http://vhl.domain.com/parsed/any.html`，以查找 SSI 命令。这是大多数网站的首选配置，因为出于性能和站点组织的目的，您希望将服务器端解析限制在特定类型的文件上。





## 对 .htm 或 .html 文件使用 XBitHack

如前所述，为整个目录启用 SSI 解析会降低服务器性能。你应尽量避免在 SSI 中使用 `.htm` 或 `.html` 扩展名；如果必须使用，则使用 `mod_include` 模块中的 `XBitHack`。`XBitHack` 指令控制服务器对与 MIME 类型 `text/html` 关联的文件的解析：

- 语法：XBitHack On | Off | Full
- 默认值：XBitHack Off
- 上下文：服务器配置、虚拟主机、目录、每目录访问控制文件（.htaccess）
- 可覆盖选项：Options

通常，只有 .htm 和 .html 文件与 text/html 关联。默认值 off 告诉服务器不要解析这些文件。当设置为 on 时，任何对文件所有者具有执行权限的 HTML 文件都被视为 SSI 文件并会被解析。当该指令设置为 full 时，它使服务器检查文件权限设置中所有者和组的可执行位。如果设置了组可执行位，则 Apache 将返回文件的最后修改日期设置为文件的最后修改时间。如果未设置，则不发送最后修改日期。设置此位使客户端和代理能够缓存请求的结果。不建议对解析和处理后会产生不同输出的 SSI 页面使用 full 值。

**注意**

如果你计划禁用通过 SSI 命令执行外部程序，你可以将 `IncludesNOEXEC` 选项与 `Options` 指令一起使用。这会禁用外部程序的执行。然而，它也会禁用通过 SSI 命令 `Include` 加载外部文件。

**备注**

在使用 XBitHack 指令启用 SSI 支持时，你仍须使用 Options +Includes。

如果你使用每目录访问控制文件（.htaccess）来启用 SSI 支持，请确保拥有该目录的站点的 AllowOverride 指令允许此类操作。此类站点的 AllowOverride 指令必须允许覆盖 Includes 选项。例如，如果某站点的 AllowOverride 设置为 None，则不会进行 SSI 解析。

**备注**

如果你在上例的 Options 行中不使用 + 号，除了 Includes 以外的所有选项将被禁用。

现在你知道了如何在 Apache 中启用 SSI 支持，下一节将详细讨论 SSI 命令。

## 使用 SSI 命令

SSI 命令以注释的形式嵌入到 HTML 页面中。基础命令结构如下所示：

```
<!--#command argument1=value argument2=value argument3=value -->
```

值通常用双引号括起来；许多命令只允许单个属性-值对。请注意，注释结束符 --> 前面应有空白字符，以确保它不被视为 SSI 命令的一部分。

以下各节将介绍所有可用的 SSI 命令。

### config

`config` 命令允许你配置显示的 `parse error`（解析错误）消息，以及用于显示时间和文件大小信息的格式。通过以下代码行实现：

```
config errmsg="error message"
config sizefmt=["bytes" | "abbrev"]
config timefmt=format string
```

`config errmsg="error message"` 向你展示如何创建自定义错误消息，该消息在发生解析错误时显示。例如，列表 13-1 展示了一个名为 `config_errmsg.shtml` 的文件。

#### 列表 13-1: config_errmsg.shtml

```
<HTML>
<BODY>
<TITLE> Apache Server 2 - Chapter 13 </TITLE>
</HEAD>

<BODY BGCOLOR="white">

<FONT SIZE=+1 FACE="Arial"> Simple SSI Example #1</FONT>
<HR SIZE=1>

<P> Example of the SSI <STRONG>config errmsg</STRONG> command:
</P> Embedded commands: <BR><BR>

<CODE>
&lt;!--#config errmsg="SSI error! Please notify the webmaster." -&gt; <BR>
&lt;!--#config badcommand="whatever" -&gt;
</CODE>
</P>

<P> Result: <BR>
<!--#config errmsg="SSI error! Please notify the Web master." -->
<BR>
<!--#config badcommand="whatever" -->
</P>

</BODY>
</HTML>
```

在此示例文件中，有两个 SSI 命令：

```
<!--#config errmsg="SSI error! Please notify the webmaster." -->
```

以及

```
<!--#config badcommand="whatever" -->
```

第一个是有效的 SSI `config errmsg` 命令，它将错误消息设置为字符串 “SSI error! Please notify the Web master.”。第二个命令是无效的 SSI 命令，我有意将其输入到该文件中，以便你看到当 Apache 解析它时会发生什么。图 13-2 展示了服务器解析此页面时返回给浏览器的内容。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_413_0.png)

**图 13-2：`config errmsg` 命令示例**

如图所示，第二个命令导致了解析错误，并因此显示了错误消息。消息出现在找到该命令的位置。

**备注**

你可以在错误消息的字符串中输入 HTML 标签，甚至插入客户端脚本。例如，以下内容显示一个带有错误消息的弹出式 JavaScript 警报窗口：

```
<!--#config errmsg="<SCRIPT LANGUAGE=JavaScript> alert('An error occurred. \n Please report to webmaster@domain.com');<\SCRIPT>" -->
```

`config sizefmt=["bytes" | "abbrev"]` 允许你选择文件大小的输出格式。可接受的格式说明符是 `"bytes"` 或 `"abbrev"`。例如：

```
<!--#config sizefmt="bytes" -->
```

以字节为单位显示文件大小。若要显示千字节或兆字节，请使用：

```
<!--#config sizefmt="abbrev" -->
```

`config timefmt=format string` 让你选择时间的显示格式：

```
config timefmt=format string
```

格式字符串的常用值可以包含表 13-1 中所示的标识符。

**表 13-1 config timefmt 的格式标识符**

| 标识符 | 含义 |
| :--- | :--- |
| %a | 根据当前区域设置的缩写星期名称 |
| %A | 根据当前区域设置的完整星期名称 |
| %b | 根据当前区域设置的缩写月份名称 |
| %B | 根据当前区域设置的完整月份名称 |
| %c | 当前区域设置首选的日期和时间表示 |
| %d | 月份中的日期，十进制数（范围 01 到 31） |
| %H | 小时，十进制数，使用 24 小时制（范围 00 到 23） |
| %I | 小时，十进制数，使用 12 小时制（范围 01 到 12） |
| %j | 一年中的第几天，十进制数（范围 001 到 366） |
| %m | 月份，十进制数（范围 01 到 12） |
| %M | 分钟，十进制数 |
| %p | 根据给定时间值或区域设置的 a.m. 或 p.m. |
| %S | 秒，十进制数 |
| %w | 星期几，十进制数，周日为 0 |
| %x | 当前区域设置首选的日期表示，不含时间 |
| %X | 当前区域设置首选的时间表示，不含日期 |
| %y | 年份，十进制数，不含世纪（范围 00 到 99） |
| %Y | 年份，十进制数，包含世纪 |
| %Z | 时区名称或缩写 |
| %% | 字面量 % 字符 |

例如，以下内容设置时间格式，使时间显示为类似 Sat Mar 17 00:31:58 2001 的格式：

```
<!--#config timefmt="%c" -->
```

以下内容设置时间格式，使时间显示为类似 03/17/2001 的格式：

```
<!--#config timefmt="%m/%d/%Y" -->
```

### echo

echo 命令打印其中一个 Include 变量（稍后定义）或任一 CGI 环境变量。语法如下：

```
echo var="variable_name"
```

如果变量的值不可用，它打印 (none) 作为值。打印的任何日期都受当前配置的时间格式影响。例如：

```
<!--#config timefmt="%m/%d/%Y" -->
<!--#echo var="DATE_LOCAL" -->
```

按照指定的 timefmt 字符串，打印类似 03/17/2001 的日期。

### exec

exec 命令允许你执行外部程序。外部程序可以是 CGI 程序或其他类型的可执行文件，如 shell 脚本或本地二进制文件。CGI 程序的语法如下：

```
exec cgi="path_to_cgi_program"
```





其他程序的语法如下：

```
exec cmd="path_to_other_programs"
```

> **注意**：如果你在使用 **Options** 指令时使用了 `includesNOEXEC` 值，则此命令会被禁用。

让我们来看看如何使用这些选项中的每一个。

### cgi

`cgi` 值指定了到 CGI 脚本的（经过 %-编码的）URL 相对路径。如果路径不以斜杠（/）开头，则默认它是相对于当前文档的。由该路径引用的文档将被作为 CGI 脚本执行，即使服务器通常不会将其识别为 CGI 脚本。但是，包含该脚本的目录必须已启用 CGI 脚本支持（通过 `ScriptAlias` 或 `ExecCGI` **Option** 设置）。

原始客户端请求中的 `PATH_INFO` 和查询字符串（**QUERY_STRING**）会被传递给 CGI 脚本；这些不能在 URL 路径中指定。除了标准的 CGI 环境变量外，Include 变量也可在脚本中使用。

列表 13-2 展示了一个名为 `colors.pl` 的简单 CGI 脚本，该脚本在一个 HTML 表格中显示常见颜色的列表。

**列表 13-2: colors.pl**

```perl
#!/usr/bin/perl -w

use strict;

my @COLOR_LIST = qw(red blue brown yellow green gray white black);

print "Content-type: text/html\n\n";
print '<table border=1 cellpadding=3 cellspacing=0>';

foreach my $color (sort @COLOR_LIST) {
    print <<TABLE_ROW;
<tr><td>$color</td>
<td bgcolor="$color"> &nbsp; &nbsp; &nbsp; &nbsp; </td>
</tr>
TABLE_ROW
}
print '</table>';
exit 0;
```

现在，请注意该脚本是如何从 `exec_cgi1.shtml` 文件中被调用的，如列表 13-3 所示。

**列表 13-3: exec_cgi1.shtml**

```html
<HTML>
<TITLE> Apache Server 2 - Chapter 13 </TITLE></HEAD>

<BODY BGCOLOR="white">
<FONT SIZE=+1 FACE="Arial">SSI Example #2</FONT>
<HR SIZE=1>

<P> Example of the SSI <STRONG>exec cgi</STRONG> command: </P>
<P> Embedded commands: <BR><BR>
<CODE> &lt;!--#exec cgi="/cgi-bin/colors.pl" -&gt; </CODE>
</P>
<P> Result: <BR> <!--#exec cgi="/cgi-bin/colors.pl" --> </P>
</BODY>
</HTML>
```

通过使用 `<!--#exec cgi="/cgi-bin/colors.pl" -->` 命令，`exec_cgi1.shtml` 生成了如图 13-3 所示的输出。

使用上述之类的 SSI 调用来嵌入 CGI 脚本的好处在于，从客户端的视角来看，无法得知该页面是通过静态和动态（即 CGI 脚本内容）数据组合而成的。

### SSI 示例 #2

SSI exec cgi 命令示例：

嵌入的命令：

```
<!--#exec cgi="/cgi-bin/colors.pl" -->
```

结果：

| 颜色   | 色样 |
|--------|------|
| 黑色   |      |
| 蓝色   |      |
| 棕色   |      |
| 灰色   |      |
| 绿色   |      |
| 红色   |      |
| 白色   |      |
| 黄色   |      |

**图 13-3: exec_cgi1.shtml 文件的输出**

请注意，如果 CGI 脚本返回 `Location` 头而不是输出内容，该头会被转换为一个 HTML 锚点。例如，列表 13-4 展示了一个名为 `relocate.pl` 的简单 Perl CGI 脚本，它输出一个 `Location:` 头作为结果。

**列表 13-4: relocate.pl**

```perl
#!/usr/bin/perl -w

print 'Location: http://apache.nitetc.com' . "\n\n";

exit 0;
```

当 Web 浏览器请求 `exec_cgi2.shtml` 文件时（如列表 13-5 所示），服务器会将 `Location:` 头转换为一个 HTML 锚点，而不是将浏览器重定向到 `http://apache.nitetc.com` 站点。

**列表 13-5: exec_cgi2.shtml**

```html
<HTML>
  <HEAD> <TITLE> Apache Server 2 - Chapter 13 </TITLE></HEAD>
  <BODY BGCOLOR="white">
  <FONT SIZE=+1 FACE="Arial">SSI Example #3</FONT>
  <HR SIZE=1>
  <P> Example of the SSI <STRONG>exec cgi</STRONG> command: </P>
  <P> Embedded commands: <BR><BR>

  <CODE> &lt;!--#exec cgi="/cgi-bin/relocate.pl" --&gt; <BR>
  </CODE>
  </P>

  <P> Result: <BR>  <!--#exec cgi="/cgi-bin/relocate.pl" --> </P>
  </BODY>
  </HTML>
```

在该列表中，文件中唯一的 SSI 调用是：

```
<!--#exec cgi="/cgi-bin/relocate.pl" -->
```

其输出是一个 HTML 锚点，如图 13-4 所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_419_0.png)

**图 13-4: `exec_cgi2.shtml` 文件的输出**

### cmd

当调用非 CGI 程序时，你可以使用 `exec` 调用的 `cmd` 版本。服务器会使用 `sh` shell（在大多数 Unix 系统上为 `/bin/sh`）来执行给定的字符串。Include 变量对此命令可用。例如，列表 13-6 展示了一个名为 `exec_cmd.shtml` 的文件。

**列表 13-6: `exec_cmd.shtml`**

```html
<HTML>
<HEAD> <TITLE> Apache Server 2 - Chapter 13 </TITLE></HEAD>
<BODY BGCOLOR="white">
<FONT SIZE=+1 FACE="Arial"> Simple SSI Example #4</FONT>
<HR SIZE=1>

<P> Example of the SSI <STRONG>exec cmd</STRONG> command: </P>
<P> Embedded commands: <BR><BR>

<CODE>
&lt;!--#exec cmd="/bin/date +%m/%d/%y" --&gt; <BR>
&lt;!--#exec cmd="/bin/ls -l ./" --&gt; <BR>
</CODE>

</P>

<P> Result: <BR>

&lt;!--#exec cmd="/bin/date +%m/%d/%y" --&gt; <BR>

</PRE>

&lt;!--#exec cmd="/bin/ls -l ./*.html" --&gt; <BR>

</PRE>

</P>
</BODY>
</HTML>
```

此文件有两个 cmd 调用：

```
<!--#exec cmd="/bin/date +%%/%%d/%%y" -->
<!--#exec cmd="/bin/ls -l ./*.html" -->
```

第一个调用 Unix 的 `/bin/date` 工具，参数为 `+%%/%%d/%%y`；第二个调用 Unix 的 `ls` 工具，参数为 `./*.html`。该文件的输出如图 13-5 所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_420_0.png)

请注意，`ls` 的输出使用 `<PRE>` 和 `</PRE>` 标签对进行了美观的格式化。如果你希望输出包含换行的内容，可能需要使用 `<PRE>` 标签以保持输出的可读性，如图 13-5 所示。

### fsize

此命令打印指定文件的大小。你使用此命令的语法取决于目录路径是相对的还是虚拟的：

```
fsize file="path"
fsize virtual="URL"
```

当使用第一种语法时，路径假定是相对于包含当前正在解析的 SSI 文档的目录。路径中不能使用 `../`，也不能使用绝对路径。你不能用这种方式访问 CGI 脚本。但是，你可以访问另一个被解析的文档。例如：

```
<!--#fsize file="download.zip" -->
```

如果使用第二种语法，*virtual* 路径被假定是一个（%-编码的）URL 路径。如果路径不以斜杠（\/）开头，则默认它是相对于当前文档的。你必须以这种方式访问普通文件，但不能以这种方式访问 CGI 脚本。不过，同样地，你可以访问另一个被解析的文档。例如：

```
<!--#fsize virtual="/download/free_software.zip" -->
```

输出格式受 *sizemft* 格式规范的影响。详情请参见 *config* 命令。

### lastmod

`lastmod` 命令打印指定文件的最后修改日期。同样，根据目录路径的不同，有两种语法选项：

```
lastmod file="path"
lastmod virtual="URL"
```

输出受 *timemft* 格式规范的影响。例如：

```
<!--#lastmod file="free_software.zip" -->
<!--#lastmod virtual="/download/free_software.zip" -->
```

如果你对语法差异感到困惑，请参见 *fsize* 命令作为例子。要控制修改日期的打印方式，请参见 *config* 命令。

### include

`include` 指令将一个文档的文本插入到正在处理的 SSI 文档中。语法取决于目录路径：

- **语法 1:** `include file="path"`
- **语法 2:** `include virtual="URL"`

关于 file 模式和 virtual 模式的区别，请参考前面几个部分的 `fsize` 命令。

任何包含的文件都受通常的访问控制约束。如果包含被解析文件的目录设置了 `Option IncludesNOEXEC`，并且包含该文档会导致执行程序，则该文档不会被包含。这防止了 CGI 脚本的执行。否则，CGI 脚本将像往常一样被调用，使用命令中给出的完整 URL，包括任何查询字符串。例如：

```
<!--#include file="copyrights.html" -->
```

在当前文档中包含 `copyrights.html` 文件。此命令对于在文件中添加可重复的 HTML 代码非常有用。许多网站在每个页面上使用标准的菜单栏；如果将此菜单栏放入一个名为 `menu.html` 的 HTML 文件中，就可以通过类似的 `include` 文件调用从所有 SSI 页面中调用它，如前例所示。将来，当需要对菜单进行更改时，站点管理员只需要更新 `menu.html` 页面即可。如果网站中有许多文件，这将节省大量工作。

递归包含会被检测到，并在第一遍之后生成错误消息。例如，如果 `a.shtml` 有一个 SSI 调用如下：

```
<!--#include file="b.shtml" -->
```

并且 `b.shtml` 有一个调用如下：

```
<!--#include file="a.shtml" -->
```

那么 Apache 会记录并显示一个错误，指出已检测到递归包含。

### printenv

`printenv` 命令打印所有现有变量及其值的列表。语法如下：

```
printenv
```





### printenv

`<!--#printenv -->`

输出所有可用的 Include 和 CGI 环境变量。为了提高输出的可读性，建议使用 `<PRE>` 标签对。

### set

`set` 命令用于设置用户定义变量的值。其语法如下：

```
set var="variable name" value="value of the variable"
```

示例如下：

```
<!--#set var="home" value="index.shtml" -->
```

## SSI 变量

除了 CGI 环境变量（参见第 12 章）之外，SSI 模块还为所有 SSI 文件提供了一组变量。这些变量被称为 `include` 变量。它们可以被 SSI 命令（如 `echo`、`if`、`elif` 等）以及由 SSI 命令调用的任何程序所使用。`include` 变量列表见表 13-2。

| 变量 | 含义 |
| :--- | :--- |
| DATE_GMT | 格林尼治标准时间（GMT）下的当前日期。 |
| DATE_LOCAL | 本地时区下的当前日期。 |
| DOCUMENT_NAME | 当前 SSI 文件的文件名。 |
| DOCUMENT_URI | 文档的（% 解码后的）URL 路径。 |
| LAST_MODIFIED | 当前文件的最后修改日期。该日期受 config 命令中 timefmt 格式的影响。 |

`include` 变量和 CGI 变量是预设的，并可供使用。任何预设变量都可以用作其他命令的参数。使用已定义变量的语法如下：

```
<!--#command argument1="$variable1" argument2="$variable2" ...-->
```

如您所见，变量名称前有一个 $ 符号。以下是另一个示例：

```
<!--#config errmsg="An error occurred in $DOCUMENT_NAME page." -->
```

当在 `var="variable"` 字段中使用变量时，不需要 $ 符号。例如：

```
<!--#echo var="DOCUMENT_NAME" -->
```

> 如果您需要在变量值中插入字面量美元符号，可以使用反斜杠转义来插入美元符号。例如：

```
<!--#set var="password" value="\$cheese" -->  <!--#echo var="password" -->
```

这将把 `$cheese` 作为变量 `"password"` 的值输出。

此外，如果您需要在一个可能被单独视为有效标识符的字符序列中间引用变量名，请在变量名周围使用一对大括号。例如：

```
<!--#set var="uniqeid" value="${DATE_LOCAL}_${REMOTE_HOST}" -->
```

这将把 `uniqeid` 设置为类似 `Saturday, 17-Mar-2001 13:02:47 PST_207.183.233.19` 的值，具体取决于 `timefmt` 设置以及 Web 客户端的 IP 地址。

## 流程控制命令

与许多编程语言一样，SSI 模块也支持程序流程控制。通过使用流程控制命令，您可以有条件地生成不同的输出。最简单的流程控制（即条件）语句是：

```
<!--#if expr="test_expression" -->  <!--#endif -->
```

在此处，`test_expression` 会被求值，如果结果为真，则直到 `endif` 命令之前的所有文本都会包含在输出中。`test_expression` 可以是一个*字符串*（如果字符串非空则为真），或者是一个比较两个字符串值的表达式。

允许使用的比较运算符有 `=`、`!=`、`<`、`>`、`<=` 或 `>=`。此类 SSI 语句的一般形式如下：

```
<!--#if expr="string1 operator string2" -->  <!--#endif -->
```

请注意，*string2* 可以是 `/regular expression patterns/` 形式的正则表达式。有关正则表达式的详细信息，请参见附录 B。

让我们看一个单独字符串的示例：

```
<!--#if expr="foobar" -->
This test is always successful.
<!--#endif -->
```

此语法总是输出 *This test is successful*。因为当 *test_expression* 不是空字符串时，该表达式为 *真*。然而，如果将 *expr*="*foobar*" 更改为 *expr*=""* 或 *expr*="'*'*，则 `if-endif` 块内的文本永远不会成为输出的一部分。

现在让我们看一个字符串相等测试的示例：

```
<!--#set var="quicksearch" value="yes" -->
<!--#if expr="$quicksearch = yes" -->

Quick search is requested.
<!--#endif -->
```

在此处，名为 *quicksearch* 的*变量*被*设置为* *值 yes*，随后与 *yes* 进行比较。由于*设置的值*和*比较的值***相等**，因此 *Quick search is requested* 这一行将被输出。

使用 *逻辑运算符* 如 `!`、`&` 和 `||`，您可以创建更复杂的 *test_expressions*。*例如*：

```
<!--#if expr="${REMOTE_ADDR} = /207.183.233/
&& ${DOCUMENT_NAME} = /timesheet/" -->
<!--#include virtual="/cgi-bin/timecard.pl" -->
<!--#endif -->
```

在此处，*test_expression* 由两个较小的*表达式*组成。*第一个子表达式*，`${REMOTE_ADDR} = /207.183.233/`，被*求值以确定服务器定义的变量* *REMOTE_ADDR* *是否匹配 207.183.233 网络地址*。请注意，该地址使用*简单正则表达式* `/207.183.233/` 书写，其中每个 *`.`*（*句号*）都*使用 \（反斜杠）字符进行了转义*。这是*为了消除 `\.` 字符在正则表达式中的特殊含义***所必需的**。有关*正则表达式*的更多*详细信息*，请参见*附录 C*。

*第二个子表达式*，`${DOCUMENT_NAME} = /timesheet/`，被*求值以确定当前正在处理的 SSI 文件是否具有* 与字符串 `timesheet` 匹配的名称。最后，`&&`（逻辑与）要求两个子表达式都为真，整个表达式才为真。如果最终表达式为真，则使用 `include virtual` 命令运行 `/cgi-bin/timecard.pl` 脚本。

您可以对 `test_expression` 执行的其他逻辑操作包括：

```
<!--#if expr="! test_expression" -->  
This is printed only when the test_expression is false.  
<!--#endif -->
```

以及

```
<!--#if expr="test_expression1 || test_expression2" -->  
This is printed when at least one of the test_expressions is  
true.  
<!--#endif -->
```

`=`（等于）和 `!=`（不等于）运算符的优先级高于 `&&`（与）和 `||`（或）运算符。`!`（非）运算符具有最高优先级。您可以使用一对括号来提高优先级。例如：

```
<!--#if expr="($win = yes && $loss = false) != ($profit = yes)" -->
```

在此处，`($win = yes && $loss = false)` 在 `!=` 运算符被求值之前先被求值。

任何未被识别为变量或运算符的内容都被视为字符串。字符串也可以像这样加引号：`'string'`。未加引号的字符串不能包含空白（空格和制表符），因为它们用于分隔诸如变量之类的标记。如果连续找到多个字符串，它们将使用空格进行拼接。

如果您需要更复杂的流程控制结构，可以使用以下结构：

```
<!--#if expr="test_condition1" -->

    Do something specific to the first test condition.

<!--#elif expr="test_condition2" -->

    Do something specific to the second condition.

<!--#else -->

    Do something as default.

<!--#endif -->
```

`elif` 使您能够创建 `else-if` 条件。例如：

```
<!--#if expr="$[HTTP_USER_AGENT] = /MSIE/" -->
  <!--#set var="browser" value="MicrosoftIE" -->
  <!--#include file="mypage.asp" -->

<!--#else -->
  <!--#set var="browser" value="Others" -->
  <!--#include file="mypage.html" -->

<!--#endif -->
```

在此处，检查 `HTTP_USER_AGENT` 变量以确定其是否包含字符串 `MSIE`（Microsoft Internet Explorer 浏览器使用的字符串）。如果包含此字符串，则 browser 变量被设置为 `MicrosoftIE`，并且名为 `mypage.asp` 的文件被插入到当前文档中。另一方面，如果 `HTTP_USER_AGENT` 不包含 `MSIE` 字符串，则假设它是另一种浏览器（如 Netscape Navigator、Lynx），因此 browser 变量被设置为 `Others`，并且 `mypage.html` 文件被插入到当前文档中。通过使用 `if-then-else` 结构，此示例为同一变量设置了不同的值并加载了不同的文件。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_427_0.png)




# 14 配置 Apache 使用 FastCGI

本章探讨 FastCGI 及其如何解决 CGI 固有的性能问题，同时不会引入专有 API 的开销和复杂性。FastCGI 快速、开放且易于维护。它提供诸如内存缓存、持久连接和分布式架构等功能。从 CGI 迁移到 FastCGI 的路径也相对简单。

## 什么是 FastCGI？

简而言之，FastCGI 应用程序表现得像一个服务器应用程序，在 Unix 世界中通常被称为守护进程（daemon）。与 CGI 脚本不同，FastCGI 应用程序是持久的，它使用单个实例服务所有传入请求，从而消除了像 CGI 版本那样每个请求启动新进程的开销。例如，如果你需要使用数据库中的内容生成一组动态页面，CGI 脚本每次按请求运行时都必须连接到数据库。另一方面，FastCGI 应用程序可以连接一次并保持连接存活，以处理所有后续请求，这种时间节省带来了更高的性能。因此，FastCGI 被认为是 CGI 的高性能替代方案，用于用多种语言编写 Web 服务器应用程序，包括 Perl、C、C++、Java 和 Python。

CGI、FastCGI 和服务器 API 的存在给开发人员和服务器管理员带来了大量的困惑。为了阐明这一晦涩的主题，表 14-1 提供了这些技术之间的一些关键特性比较。

# 本章内容

- 解释 FastCGI
- 描述 FastCGI 应用程序的基本架构
- 编译和安装 Apache 的 FastCGI 模块
- 配置 httpd.conf 以运行 FastCGI 应用程序

表 14-1：比较 CGI、服务器 API 和 FastCGI

| 特性 | CGI | 服务器 API | FastCGI |
| :--- | :--- | :--- | :--- |
| 编程语言依赖性 | 语言无关。CGI 应用程序几乎可以用任何编程语言编写（通常是 C/C++）。 | 应用程序必须使用支持该供应商 API 编程语言的编程语言编写。 | 语言无关。与 CGI 一样，FastCGI 应用程序可以用任何编程语言编写。 |
| 进程隔离 | 应用程序具有独立的进程；有缺陷的应用程序无法使 Web 服务器崩溃或访问服务器的私有内部状态从而破坏安全性。 | 不支持此功能。因为 FastCGI 应用程序在服务器的地址空间中运行，有缺陷的应用程序可能会损坏核心服务器。（注：原文此处逻辑似有误，通常指 Server API 在内存中运行导致风险，但表格对应列为 Server API，原文描述为 "Feature not supported... Because the FastCGI applications..." 这里存在明显的原文错误，按原文直译并保留其意指的对比逻辑，或者根据上下文推测原文意在对比 Server API 缺乏隔离。*修正理解*：原文表格第三列是 FastCGI，第二列是 Server API。原句 "Feature not supported. Because the FastCGI applications run in the server’s address space..." 这句话放在 Server API 列下明显是原文的笔误，或者是指 Server API *没有* 提供进程隔离，因为它们在内存中运行。但原文写的是 "Because the FastCGI..." 这可能是文档错误。作为翻译员，我将忠实翻译原文内容，即使原文存在逻辑矛盾。*再次阅读*：表格头是 Feature, CGI, Server API, FastCGI。当前行是 Process isolation。CGI 列：独立进程。Server API 列："Feature not supported. Because the FastCGI applications run in the server’s address space..." 这显然是原文错误，应该写的是 API applications。FastCGI 列："A buggy application cannot crash..."。我将忠实于原文翻译，但需注意原文可能有误。*决定*：忠实翻译原文文字。 | 有缺陷的应用程序无法使核心服务器或其他应用程序崩溃或损坏。 |
| 标准类型 | 开放标准。某种形式的 CGI 已在所有 Web 服务器上实现。 | 专有。将你的应用程序编码为特定 API 会将你锁定在该供应商的服务器上。 | 非专有，拟议的开放标准。其他 Web 服务器（包括 Microsoft 和 Netscape 的商业服务器）的支持正在开发中。Apache 目前支持 FastCGI 作为第三方模块。 |
| 平台依赖性 | 平台无关。CGI 不依赖于任何特定的服务器架构（单线程、多线程、线程化等）。 | 与服务器架构绑定。API 应用程序必须与服务器共享相同的架构。如果 Web 服务器是多线程的，应用程序必须是线程安全的。如果 Web 服务器使用单线程进程，多线程应用程序不会获得任何性能优势。 | 平台无关。FastCGI 不依赖于任何特定的服务器架构。任何 Web 服务器都可以实现 FastCGI 接口。 |
| 性能 | 每个请求都会创建一个新进程，无论请求是否完成，该进程都会被丢弃；效率低下。 | 应用程序在服务器进程中运行，并在请求间持久存在。不存在 CGI 启动/初始化问题。 | FastCGI 进程是持久的；它们被重用以处理多个请求。不存在 CGI 启动/初始化问题。 |
| 复杂性 | 易于理解。 | 非常复杂。供应商 API 引入了陡峭的学习曲线，增加了实现和维护成本。 | 简单，易于从 CGI 迁移。 |
| 分布式架构 | 不支持。要在远程系统上运行 CGI 应用程序，该系统上需要一个 Web 服务器，因为 CGI 应用程序由 Web 服务器运行。 | 取决于供应商。 | 支持。FastCGI 应用程序可以在任何支持 TCP/IP 的主机上运行。 |

### 通过使用缓存实现高性能

FastCGI 有多快？答案取决于应用程序。如果应用程序从文件读取数据，并且这些数据可以缓存到内存中，那么该应用程序的 FastCGI 版本比 CGI 或基于 API 的 Web 服务器应用程序提供更高的性能。根据规范，CGI 应用程序不能使用内存缓存，因为每个请求都会运行应用程序的新实例，并在请求处理完成后退出。同样，大多数广泛使用的基于 API 的 Web 服务器应用程序运行在不共享内存的子进程中，因此无法应用缓存。即使在这种模型中为每个子进程实现了内存缓存，其效果也非常差，因为每个子进程都必须在内存中拥有一份缓存副本，这会浪费大量内存。

FastCGI 旨在实现有效的内存缓存。请求从任何子进程路由到 FastCGI 应用程序服务器。FastCGI 应用程序进程维护一个内存缓存。请注意，在某些情况下，单个 FastCGI 应用程序服务器可能无法提供足够的性能。使用多线程，你可以运行设计用于同时处理多个请求的应用程序进程。处理并发请求的线程共享进程内存，因此它们都可以访问相同的缓存。

### 通过分布式应用程序实现可扩展性

与 CGI 应用程序不同，FastCGI 应用程序不从其进程环境表获取 CGI 环境变量。相反，应用程序与 Web 服务器之间的全双工连接用于传递环境信息、标准输入和输出以及错误。这使得 FastCGI 应用程序能够通过 TCP/IP 连接到 Web 服务器，并在远程机器上运行，如图 14-1 所示。该图显示，来自 Internet 的请求由 www.nitec.com（Web 服务器）处理，它通过 TCP 连接远程连接到 fcgi.nitec.com，然后请求由 FastCGI 脚本处理。

## 让 FastCGI 接受考验

FastCGI 的开发者进行了测试，使用了应用程序的三种版本（分别基于 CGI、FastCGI 和一种流行的基于 Web 服务器的 API 规范），这些应用程序与数据库服务器交互。开发者发现，当应用程序的 FastCGI 版本使用内存缓存和到数据库服务器的持久连接时，其性能远超 CGI 和基于 API 的应用程序版本。

当 FastCGI 应用程序禁用了内存缓存，而基于 API 的应用程序使用持久连接时，基于 API 的应用程序性能略高于 FastCGI 版本。这意味着，只有在公平竞争的情况下（即禁用了 FastCGI 的优势，如内存缓存功能），API 版本才会获胜。但是，为什么要禁用缓存呢？换句话说，只要你不编写功能受限的 FastCGI 应用程序，它很可能会比 CGI 和 API 版本的表现更好。

测试表明，基于 FastCGI 的应用程序在架构上的优势使其性能比对应的 API 版本快三倍。如果应用程序必须连接到远程资源（如远程数据库服务器），这一因素可能会更加显著。然而，他们还指出，能够为其 API 应用程序线程维护缓存和持久连接的多线程 Web 服务器，很可能比 FastCGI 应用程序表现更好。这是由于线程环境中不存在进程间通信开销。开发多线程应用程序需要非常细致的设计和编程，因为一个有故障的线程可能会使整个 Web 服务器系统宕机。

另一方面，FastCGI 进程利用了进程隔离模型，它们作为外部进程运行。这为 Web 服务器系统提供了一张安全网。如果有故障的 FastCGI 应用程序，Web 服务器仍将运行。如果你非常热爱多线程并且离不开它，你始终可以以多线程模型编写你的 FastCGI 应用程序，这样仍然可以利用进程隔离模型的优势。





![](img/e11fcbd2818a3495ac70085e5d8d1c26_433_0.png)

## 图 14-1：位于远程机器上的 FastCGI

当基于 CGI 和 APL 的应用程序因负载过重而成为性能瓶颈时，典型的解决方案是获取更强大的 Web 服务器或更多的 Web 服务器来运行它们。通过使用 FastCGI，FastCGI 应用程序可以在网络上的专用应用程序服务器上运行，从而释放 Web 服务器以处理其最擅长的任务——处理 Web 请求。Web 服务器可以经过专门调整以更好地执行 Web 服务，同时 FastCGI 应用程序服务器也可以经过专门调整以高效地运行应用程序。Web 管理员再也不必担心如何平衡同一台机器上 Web 服务器和应用程序的资源需求了。这为 Web 服务器端以及应用程序端提供了更具灵活性的配置。

许多组织希望在其网站上提供数据库访问功能。然而，由于 CGI 和供应商 API 的限制，他们必须在 Web 服务器上复制数据库的有限版本才能提供此服务。这给管理员带来了相当繁重的工作量。使用远程 FastCGI，应用程序可以在内部网络上运行，从而简化管理员的工作。当配合适当的防火墙配置和审计使用时，这种方法提供了一种安全、高性能且可扩展的方式，将内部应用程序和数据带到互联网上。

远程 FastCGI 连接存在两个安全问题：身份验证和隐私。FastCGI 应用程序应只接受来自其信任的 Web 服务器的连接（应用程序库包含对 IP 地址验证的支持）。该协议的后续版本可能会包括支持应用程序对 Web 服务器进行身份验证，以及支持在安全协议（如安全套接层 (SSL)）上运行远程连接。

## 理解 FastCGI 的工作原理

FastCGI 应用程序使用单个连接与 Web 服务器通信。该连接用于向应用程序传递环境变量和 STDIN 数据，并将 STDOUT 和 STDERR 数据传递给 Web 服务器。使用这种简单的通信协议还允许 FastCGI 应用程序驻留在与 Web 服务器不同的机器（或多台机器）上，从而使应用程序能够扩展到单个系统之外，并提供与现有系统更容易集成。对于本地应用程序，服务器使用全双工管道连接到 FastCGI 应用程序进程。对于远程应用程序，服务器使用 TCP/IP 连接。

Web 服务器与应用程序之间通信所用的 FastCGI 协议采用简单的数据包记录格式。大多数应用程序开发人员将使用 FastCGI 应用程序库，而无需担心协议细节。但是，专门的应用程序可以直接实现 FastCGI 协议。

由于 CGI 与 FastCGI 非常相似，让我们回顾一下 CGI 请求处理过程。图 14-2 显示了简化的 CGI 请求处理模型。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_434_0.png)

**图 14-2：** CGI 请求处理模型

对于每个 CGI 请求，会发生以下情况（请参阅上图）：

- 1. 客户端系统向 Web 服务器发送请求。Web 服务器确定该请求是否需要由 CGI 程序处理。
- 2. Web 服务器创建一个新的 CGI 进程，该进程初始化自身。
  - Web 服务器通过环境变量向程序传递各种与请求相关的信息。根据请求方法（GET 或 POST），用户数据存储在名为 QUERY_STRING 的环境变量中，或者放入进程的标准输入中。
- 3. CGI 应用程序执行其任务并将其所有输出发送到标准输出，Web 服务器读取并解析这些输出（除非是标准非解析头应用程序）。
- 4. CGI 程序退出，服务器将 CGI 输出返回给客户端。
- 5. CGI 程序的输出发送到客户端系统。

FastCGI 进程是持久的。完成请求后，它们不会退出，而是等待新的请求，如图 14-3 所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_435_0.png)

图 14-3：FastCGI 请求处理模型

对于非解析头应用程序，CGI 应用程序负责生成适当的 HTTP 头，而在其他所有情况下，Web 服务器根据在程序的 `STDOUT` 中找到的内容类型生成适当的 HTTP 头。Web 服务器记录写入 CGI 程序标准错误的任何错误信息。

Web 服务器创建 FastCGI 应用程序进程以处理请求。这些进程可以在启动时或按需创建。FastCGI 程序初始化自身并等待来自 Web 服务器新连接。单线程 FastCGI 应用程序中的客户端请求处理流程如下：

- 1. 当客户端请求到达时，Web 服务器决定该连接是否需要由 FastCGI 程序处理。
- 2. 如果请求需要由 FastCGI 程序处理，Web 服务器随后将打开一个到已在运行的 FastCGI 进程的连接。
- 3. 服务器通过连接发送 CGI 环境变量信息和标准输入。FastCGI 进程通过同一连接将标准输出和错误信息发送回服务器，然后 FastCGI 进程关闭该连接。
- 4. Web 服务器使用由 FastCGI 进程发送的数据响应客户端，完成请求。然后 FastCGI 进程等待来自 Web 服务器的另一个连接。

## FastCGI 应用程序的基本架构

正如您已经知道的，与 CGI 程序不同，FastCGI 程序在处理完请求后会继续运行。这使它能够一旦有未来请求到达就立即处理，也使得 FastCGI 程序的架构与 CGI 程序不同。CGI 程序按顺序执行并退出，而 FastCGI 程序按顺序执行并永远循环。图 14-4 显示了 FastCGI 应用程序的基本架构。

如图所示，FastCGI 程序通常包含一段初始化代码和一段响应循环代码，后者封装了程序的主体。初始化代码在应用程序初始化时恰好执行一次。初始化代码通常执行耗时操作，例如打开数据库或计算表格值。

响应循环持续运行，等待客户端请求到达。循环以对 FastCGI 库中 `FCGI_Accept` 例程的调用开始。`FCGI_Accept` 例程会阻塞程序执行，直到客户端请求 FastCGI 应用程序为止。当客户端请求到达时，`FCGI_Accept` 解除阻塞，运行一次响应循环主体，然后再次阻塞，等待另一个客户端请求。只有当系统管理员或 Web 服务器终止 FastCGI 应用程序时，循环才会终止。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_437_0.png)

图 14-4：FastCGI 应用程序的基本架构

程序主体在响应循环的每次迭代中执行。换句话说，对于每个请求，主体执行一次。FastCGI 在每次主体代码迭代之前设置请求信息，例如环境变量和输入数据。当主体代码执行时，随后的对 *FCGI_Accept* 的调用会通知服务器该程序已完成一个请求并准备好处理下一个。此时，*FCGI_Accept* 会阻塞执行，直到接收到新请求为止。

FastCGI 应用程序可以是单线程的或多线程的。对于单线程应用程序，Web 服务器维护一个 FastCGI 进程池（如果应用程序在本地运行）来处理客户端请求。池的大小可由用户配置。多线程 FastCGI 应用程序可以接受来自 Web 服务器的多个连接，并可以在单个进程中同时处理它们。

## 不同类型的 FastCGI 应用程序

FastCGI 的另一个重要方面是它支持应用程序的角色（类型）。与 CGI 应用程序不同，FastCGI 应用程序是持久的，因此它可以用于在基于 CGI 的应用程序中不实际的目的。接下来的段落讨论 FastCGI 支持的两个新类型的应用程序。

FastCGI 应用程序可以执行 CGI 应用程序能够执行的所有操作，因此典型的 FastCGI 应用程序与其 CGI 对应物相同。以下列表展示了在 FastCGI 支持下可用的应用程序新角色：



**过滤器：** 您可以创建一个 FastCGI 过滤应用程序，在文件返回给客户端之前对其进行预处理。例如，假设您希望为 Web 服务器返回的每个 HTML (.html) 页面应用一组标准的页眉和页脚。使用 FastCGI 过滤应用程序可以实现这一目标。当服务器收到对 .html 文件的请求时，它会向负责添加页眉和页脚的 FastCGI 过滤器发送文件请求。FastCGI 应用程序将生成的 HTML 页面返回给服务器，服务器随后将其传输给客户端。

通过缓存过滤器结果，FastCGI 过滤应用程序可以显著提高性能（服务器会在请求信息中提供修改时间，以便应用程序在服务器文件被修改时刷新缓存）。过滤器应用程序在开发解析器（用于处理包含嵌入式 SQL 语句的 HTML 页面）、即时文件格式转换器等场景中非常有用。

**外部认证应用程序：** 使用 FastCGI 支持开发的其他新型应用程序包括外部认证程序和通往第三方认证应用程序的网关。例如，如果您使用外部数据库服务器来存储认证信息（如用户名、密码或其他特定权限数据），您可以创建一个 FastCGI 应用程序来保持与数据库服务器的持久连接，并执行查询以验证访问请求。这可以用 CGI 应用程序实现吗？可以，但 CGI 应用程序在每次运行时都必须重新打开与数据库服务器的连接。从资源（CPU、网络）利用的角度来看，这可能代价高昂。

相反，同一应用程序的 FastCGI 版本仅保持与数据库服务器的单个连接，执行查询，并根据查询结果返回相应的 HTTP 状态码。例如，当访问请求附带有效的用户名/密码对时，FastCGI 应用程序会查询数据库服务器以确定该对是否有权访问所请求的资源。如果数据库服务器返回指示允许访问的特定值，FastCGI 应用程序将返回 200 OK HTTP 状态码；当授权失败时，它可以发送不同的 HTTP 状态码，如 401 Unauthorized。

## 从 CGI 迁移到 FastCGI

FastCGI 的主要优势之一是从 CGI 到 FastCGI 的迁移路径相对简单。使用 CGI.pm 模块的特殊基于 Perl 的 CGI 脚本可以轻松地转换为 FastCGI 应用程序。任何其他语言（如 C、C++、Tcl 或 Java）编写的 CGI 程序也可以使用 FastCGI 软件开发工具包（SDK）进行转换。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_439_0.png)

FastCGI 规范的开发者提供了一个免费可用的软件开发工具包（SDK），以帮助简化 FastCGI 应用程序开发过程。SDK 也包含在随附的光盘中。此工具包以压缩的 tar 文件形式提供，可帮助您用 C、C++、Perl、Tcl 和 Java 编写 FastCGI 应用程序。解压缩并提取 tar 文件后，它会创建名为 fcgi-dev-kit 的目录。其中的 index.html 文件提供了关于该工具包中包含内容的信息。您也可以在 www.fastcgi.com/applibs 的 FastCGI 网站上获取该工具包。

## 迁移时需留意的要点

以下列表提供了一些在迁移 CGI 应用程序时需要牢记的建议：

-   需要注意的另一个问题是：如果正在迁移的 CGI 应用程序中包含可能会干扰 body 代码第二次运行的代码，则必须修复它。解决此问题的方法可能简单到只需添加代码重新初始化某些变量、数组等即可。应用程序必须确保处理一个请求时创建的任何状态不会对后续请求产生意外影响。

-   对于 CGI 开发者来说，将大型应用程序细分为较小的 CGI applets 是一种常见的做法，以此作为弥补 CGI 应用程序初始化开销的一种方式。使用 FastCGI 时，最好将相关功能放在单个可执行文件中，这样需要管理的进程更少，且应用程序可以利用跨函数共享缓存信息的优势。

-   为了便于迁移到 FastCGI，使用 FCGI 模块构建的可执行文件可以作为 CGI 或 FastCGI 程序运行，具体取决于调用方式。该模块会检测执行环境，并自动选择 FastCGI 或常规 I/O 例程，具体视情况而定。

-   许多 CGI 应用程序编写时不尝试执行任何内存管理操作。这是因为 CGI 应用程序在执行后会退出，在大多数情况下，操作系统能够恢复内存供其他用途。除此之外，许多 CGI 应用程序甚至不尝试关闭文件，因为该责任在退出时移交给操作系统。

在这种情况下，在迁移到 FastCGI 版本时修复这类应用程序至关重要。请记住，只要 Web 服务器或管理员不终止 FastCGI 应用程序，它就会一直驻留在内存中。如果一个存在内存泄漏的 CGI 应用程序在未解决内存问题的情况下被转换为 FastCGI，那么 FastCGI 版本可能会随时间推移不断泄漏内存，最终导致资源故障。为了避免在办公室度过漫长的周末（即避免长时间停机或故障），请提前审视此问题。如果 CGI 应用程序非常复杂，且为了使其行为正常（在内存使用方面）所需的时间和工作量代价过高，还有另一种解决方案可供使用。

您可以记录该存在内存泄漏的应用程序处理请求的次数，并通过围绕其编程来终止它。列表 14-1 展示了一个简单的示例，说明如何在简单的基于 C 的 FastCGI 应用程序中保持请求处理计数。如该列表所示，当处理的最大请求数达到时，FastCGI 应用程序将退出。

**列表 14-1: memory\_hog.c**

```c
#include <fcgi_stdio.h>
void main(void){
    int maxRequests = 100;         // maximum num of request
    before exiting.
    int requestCount = 0;          // used to keep count of
    requests processed so far.

    while(FCGI_Accept() >= 0) {    // start of response loop
        /* body code */

        printf("Content-type: text/html\r\n");
        printf("\r\n");
        printf("Number of requests processed so far is %d.", requestCount++);

        /* some memory leaking code could go here */

        /* end of application code */

        if(requestCount >= maxRequests) {
            /* clean-up code goes here */
            exit(0);
        }

        /* end of body code */
    }

    /* termination or clean-up code (if any) */
    exit(0);
}
```

## 迁移示例脚本

本节演示如何迁移 `fontsize.cgi`，一个简单的 CGI 脚本（用 Perl 编写），该脚本列于列表 14-2 中。

**列表 14-2: fontsize.cgi**

```perl
#!/usr/bin/perl  -w

# Variables
my $MAX = 10;
my $i;

# Content Header
print "Content-type: text/html\n\n";

# Main loop
for ($i=0; $i < $MAX; $i++){

    print "<FONT SIZE=$i>Font Size = $i</FONT><BR>";
}

exit 0;
```

此 CGI 应用程序产生的输出如图 14-5 所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_441_0.png)

**图 14-5：** `fontsize.cgi` 脚本的输出

现在让我们将其转换为 FastCGI 应用程序。首先，您需要确保通过综合 Perl 存档网络（CPAN）站点安装 FCGI 模块，请遵循以下步骤：

1.  作为 `root`，在命令行运行以下命令：
    ```perl
    perl -MCPAN -e shell
    ```

2.  在 `cpan>` 提示符下输入 `install FCGI` 命令，如果您尚未拥有最新版本，这将安装该 CPAN 模块的最新版本。

3.  在上述脚本的第二行添加以下行：
    ```perl
    use FCGI;
    ```
    这指示 Perl 在运行脚本时加载 FCGI 模块。

4.  确定 CGI 应用程序的初始化块。对于此脚本，初始化块由以下两个变量声明组成：
    ```perl
    my $MAX = 10;
    my $i;
    ```

5.  确定 CGI 应用程序的响应循环和 body 块。由于每个请求都必须以适当的 Content-Type 头响应，主代码的 body 从以下行开始：
    ```perl
    print "Content-type: text/html\n\n";
    ```
    负责实际处理的 for 循环是 body 的其余部分。

6.  既然 body 代码已识别，您需要将其周围加上响应循环。使用以下代码完成：
    ```perl
    while(FCGI::accept() >= 0) {
    # body code goes here
    }
    ```
    现在 body 看起来像这样：
    ```perl
    while(FCGI::accept() >= 0) {
    print "Content-type: text/html\n\n";

    for ($i=0; $i < $MAX; $i++){
    print "<FONT SIZE=$i>Font Size = $i</FONT><BR>";
    }
    }
    ```

FastCGI 应用程序像服务器应用程序一样运行，因此以下行仅在 Web 服务器或管理员向应用程序发送终止信号时执行：
```perl
exit 0;
```

整个应用程序的 FastCGI 版本列于列表 14-3 中。





## 列表 14-3：fontsize.fcgi

```perl
#!/usr/bin/perl

# Load the FCGI module
use FCGI;

# Global variables
my $MAX = 10;
my $i;

# FastCGI Loop
while (FCGI::accept() >= 0) {

    # Content Header
    print "Content-type: text/html\n\n";

    # Main Loop
    for ($i=0; $i < $MAX; $i++){
        print "<FONT SIZE=$i>Font Size = $i</FONT><BR>";
    }
}

exit 0;
```

## 为 Apache 配置 FastCGI

要在 Apache 中安装 `mod_fastcgi`，请按照以下步骤操作：

- 1. 从 www.fastcgi.com 下载适用于 Apache 的最新 `mod_fastcgi` 模块。
- 2. 在 `/usr/local/src` 目录中提取源文件。会创建一个新的目录，名为 `mod_fastcgi_version`。阅读此新目录中的 INSTALL 文件以了解安装该模块的详细信息，因为安装方式会不时变化。
- 3. 将新目录复制到 Apache 源代码树中 modules 目录下的名为 fastcgi 的子目录中。
- 4. 在 Apache 源代码发行版目录中，运行 `configure --enable-module=fastcgi` 以及你想要为 `configure script` 指定的任何其他选项。（有关 `configure script` 可用其他选项的详细信息，请参阅第 3 章。）如果你已经编译了 Apache，可以将前一条命令中的 `configure` 替换为 `config.status`，以确保在最后一次运行 configure 时指定的所有选项都再次被应用。
- 5. 运行 `make` 和 `make install` 来编译并安装支持 `mod_fastcgi` 的 Apache。
- 6. 使用 /usr/local/apache/bin/apachectl restart 命令重启 Apache。

## Apache 的 FastCGI 指令

*mod_fastcgi.c* 模块提供了一组指令来控制如何使用 FastCGI 应用程序。这些指令讨论如下：

### AppClass 指令

该指令允许你启动 FastCGI 应用程序。

**语法：** `AppClass path_to_FastCGI_application [-processes N] [-listen-queue-depth N] [-restart-delay N] [-priority N] [-port N] [-socket sock-name] [-initial-env key=value]`

**上下文：** 服务器配置

例如，以下指令启用 *mod_fastcgi* 加载 */www/development/fcgi-devel-kit/echo.fcgi* **FastCGI 应用程序**：

```apache
AppClass /www/development/fcgi-devel-kit/echo.fcgi -port 9000
```

应用程序在端口 9000 上监听。当通过此指令加载的 FastCGI 应用程序停止运行时，*mod_fastcgi* 会重启该应用程序并在错误日志文件中写入日志条目。AppClass 指令的可选参数如下：

- *processes* — 此选项指定要创建多少个 FastCGI 进程。在高负载场景中，加载同一 FastCGI 应用程序的多个实例可以提供更好的性能。默认值为 1。
- *listen-queue-depth* — 此选项指定通过该指令加载的 FastCGI 应用程序的监听队列深度。默认值在大多数情况下就足够了，但在高负载场景中，你可以增加队列的深度。这可以减少因应用程序繁忙而导致请求被拒绝的可能性。然而，如果你预期会有高负载，并且你的服务器能够运行额外的几个 FastCGI 进程，请增加进程数量而不是监听队列的深度。默认值为 5。
- *restart-delay* — 此选项指定用于延迟重启已停止的 FastCGI 进程的时间（以秒为单位）。仅当使用同一 FastCGI 应用程序的多个实例时才有用。对于单个 FastCGI 应用程序，它会立即重启，此选项无效。默认值为 5。你可能会疑惑为什么需要这个延迟。通常，FastCGI 应用程序不应该停止运行；如果它正在停止运行，说明可能存在某些问题。在这种情况下，该延迟允许你的服务器执行其他有用的任务，而不是反复重启有故障的应用程序。
- *priority* — 此选项设置 FastCGI 应用程序的进程优先级。默认值使 FastCGI 应用程序具有与 Apache 服务器本身的相同优先级。其他合适的值由操作系统的 `setpriority` 系统调用定义。在 Red Hat Linux 系统中，`setpriority` 系统调用允许的值范围为 –20 到 20。数字越小，用于该进程的调度越有利。但是，`mod_fastcgi` 不允许负值，这意味着你不能将 FastCGI 进程的优先级设置得高于 Apache 服务器本身。因此，你只能使用正整数来降低应用程序的优先级。默认值为 0。
- *port* — 此选项指定 FastCGI 应用程序将监听的 TCP 端口。由于低于 1024 的端口用于标准服务，因此你必须使用较高的端口号。使用此选项允许你从另一个系统访问该应用程序。默认情况下不提供环境变量。
- *socket* — 此选项指定应用程序监听的 Unix 域套接字的路径名。该模块在由 `FastCgiIpcDir` 指令指定的目录中创建此套接字。默认值为 `DefaultSocket`。如果你未提供端口或套接字选项，模块将由应用程序本身创建一个 Unix 域套接字。
- *initial-env* — 此选项可用于在 FastCGI 应用程序的环境表中插入环境变量（带值）。你可以多次使用此选项以在应用程序的环境中插入多个键值对。默认情况下不提供环境变量。

请注意，`-socket` 和 `-port` 选项是互斥的。路径名不得等于先前 `AppClass` 或 `ExternalAppClass` 指令提供的路径名。

### ExternalAppClass 指令

当你在另一个系统上运行 FastCGI 应用程序时，请使用此指令。

- **语法：** `ExternalAppClass FastCGI_application_name [-host host[:port]] [-socket sock_name]`
- **上下文：** 服务器配置

在以下示例中，`echo.fcgi` 应用程序正在名为 `fcgi.nitc.com` 的主机上运行，并监听端口 9090。`<FastCGI-application-name>` 只是一个标识符，可用于描述在远程主机上运行的应用程序，因此可以是任何你想要的名称。确保你选择的名称尚未在另一个 `AppClass` 或 `ExternalAppClass` 指令中使用。

```apache
ExternalAppClass echo.fcgi -host fcgi.nitc.com:9090
```

ExternalAppClass 指令的可选参数如下：

- *host* — 此选项允许你指定在另一个系统上运行的 FastCGI 应用程序的主机和 TCP 端口号。使用 host:port 格式指定主机和端口。你可以使用主机名或 IP 地址。
- *socket* — 此选项允许你指定 FastCGI 应用程序正在使用的 Unix 域套接字的路径名。

### FastCgiIpcDir 指令

此指令指定由模块创建的 Unix 域套接字的默认路径。只要你没有设置定时任务（cron jobs）定期清理 /tmp 目录，默认的 /tmp 位置就没问题。

**语法：** `FastCgiIpcDir path_to_UNIX_domain_socket`
**默认：** `FastCgiIpcDir /tmp`
**上下文：** 服务器配置

套接字名称具有以下格式：

```
OM_WS_n_.pid
```

n 是一个数字，pid 是主 Apache 进程的进程 ID。如果你将此指令设置为路径，请确保只有 Apache 具有对该目录的读写权限。

## 配置 httpd.conf 以支持 FastCGI

为了配置 FastCGI 应用程序，你需要结合使用 mod_fastcgi 指令和 Apache 服务器提供的指令。

使用 AppClass 指令启动你希望由此 Web 服务器管理的 FastCGI 应用程序。这里的“管理”是指当受管理的进程停止运行时，服务器会记录错误消息，并尝试重启那些停止运行的受管理进程。

使用 AppClass 和/或 ExternalAppClass 指令来定义路径名与 FastCGI 应用程序连接信息之间的关联。连接信息可以是 Unix 域套接字的路径名，也可以是 TCP 端口的 IP 地址和端口号。这两个指令的区别在于：单个 AppClass 指令既启动应用程序又设置与其通信的关联，而 ExternalAppClass 仅定义关联。对于 AppClass，关联中使用的路径名始终是应用程序可执行文件的路径名；而对于 ExternalAppClass，路径名是任意的。




如果要让 mod_fastcgi 处理 HTTP 请求，该请求的处理程序必须是 `fastcgi-script`，或者请求的 MIME 类型必须是 `application/x-httpd-fcgi`。Apache 提供了多种方式来设置请求的处理程序和 MIME 类型：

- `SetHandler`（在 Location 或 Directory 部分或按目录访问控制文件的上下文中）可以将处理程序 `fastcgi-script` 关联到特定文件或目录中的所有文件。
- `AddHandler` 可以根据文件扩展名将处理程序 `fastcgi-script` 关联到文件。
- `ForceType`（在 Location 或 Directory 部分或 `.htaccess` 文件的上下文中）可以将 MIME 类型 `application/x-httpd-fcgi` 关联到特定文件或目录中的所有文件。
- `AddType` 可以根据文件扩展名将 MIME 类型 `application/x-httpd-fcgi` 关联到文件。

配置好 mod_fastcgi 模块后，它按以下方式处理请求：

1. 检索与所请求的路径名相关的连接信息。如果没有与该路径名关联的连接信息，服务器将返回错误代码 404 Not Found。
2. mod_fastcgi 模块连接到 FastCGI 应用程序进程。如果连接尝试失败，服务器将返回 500 Server Error。
3. 请求被传输到 FastCGI 应用程序进程，该进程生成响应。
4. 接收应用程序的响应并将其转换为 HTTP 响应。服务器将此响应发送回客户端。

你应该备份现有的 `httpd.conf` 文件，但不要立即使用清单 14-4 中的示例配置文件。这是一个最小化配置，仅用于测试目的，只使用 `httpd.conf` 文件。请使用此配置进行 FastCGI 的初始测试，当你验证该配置有效后，将此配置中与 FastCGI 相关的部分与你自己的配置进行合并。

### 清单 14-4: 示例 httpd.conf 配置文件

```apache
# httpd.conf-minimal for mod_fastcgi

Port 80

# You should replace the User/Group directive with appropriate
# user/group name
User $HTTP_USER
Group $HTTP_GROUP

# Configure just one idle httpd child process, to simplify
# debugging
StartServers 1
MinSpareServers 1
MaxSpareServers 1

# Tell httpd where it should live, turn on access and error
# logging
ServerRoot        $APACHE
ErrorLog          logs/error.log
TransferLog       logs/access.log
ScoreBoardFile    logs/httpd.scoreboard

# Tell httpd where to get documents
#
DocumentRoot $FASTCGI

# This is how you'd place the Unix-domain socket files in the
# logs directory (you'd probably want to create a subdirectory
# for them.)
# Don't do this until you've verified that everything works
# with the socket files stored locally, in /tmp/
# FastCgiIpcDir $APACHE/logs
# Start the echo app
#
AppClass $FASTCGI/examples/echo -initial-env SOMETHING=NOTHING

# Have mod_fastcgi handle requests for the echo app
# (otherwise the server will return the app's binary as a
# file!)
<Location /examples/echo>
   SetHandler fastcgi-script
</Location>

# Start a FastCGI application that's accessible from other
# machines
AppClass $FASTCGI/examples/echo.fcg -port 8978

<Location /examples/echo.fcg>
   SetHandler fastcgi-script
</Location>

# Connect to "remote" app started above. Because the app is
# actually local, communication will take place using TCP
# loopback.
# To test true remote operation, start one copy of this Web
# server on one machine, and then start another copy with
# "localhost" in the line below changed to the host name of the
# first machine.
#
#ExternalAppClass remote-echo -host localhost:8978

<Location /examples/remote-echo>
    SetHandler fastcgi-script
</Location>

# This is how you'd have mod_fastcgi handle any request
# for a file with extension .fcg:
  AddHandler fastcgi-script fcg

# End of httpd.conf
```

请确保你已使用包含 mod_fastcgi 模块的新 httpd 进行构建，并且 FastCGI 开发工具包已正确构建。我在示例目录中使用了 FastCGI 开发工具包附带的 echo 程序。不要忘记在将清单 14-4 中的新 `httpd.conf` 文件放入 `$APACHE/conf` 目录后重启 Apache。使用浏览器访问 `http://$YOUR_HOST/examples/echo`。

`$YOUR_HOST` 是运行 httpd 的主机的 IP 地址。在 echo 显示的初始环境中查找 `SOMETHING=NOTHING`。每次重新加载页面时，请求计数器都应该递增。在使用此配置之前，你必须进行一些替换，如表 14-5 所示。

**表 14-5：示例配置的替换项**

| 关键字 | 替换为 |
| :--- | :--- |
| `$APACHE` | 包含 Apache 的目录的完全限定路径名 |
| `$FASTCGI` | 包含你的 FastCGI 开发工具包的目录的完全限定路径名 |
| `$HTTP_USER` | 你用于 `User` 指令的用户名 |
| `$HTTP_GROUP` | 你用于 `Group` 指令的组名 |

## PHP 和 Apache

仅仅几年前，PHP（PHP 超文本预处理器）刚开始作为 HTML 宏语言出现。如今，它部署在全球百分之六或更多的网站中，并成为具有数据库连接性的服务器端脚本处理的事实标准方法。PHP 是一种完全成熟的编程语言，专注于动态 Web 应用程序。它可以作为独立脚本运行以执行系统管理任务，类似于 Perl 和其他 shell 编程语言，但其主要目标是渲染来自 MySQL、Postgres、Oracle、DB2 和 MS SQL Server 等关系型数据库中数据的动态 Web 页面。

尽管 PHP 与微软的 ASP、Allaire 的 Cold Fusion、Sun 的 JSP 甚至一个名为 mod_perl 的开源表亲竞争，但它实际上比其几乎所有竞争对手早至少一年！由于 PHP 易于部署、易于使用、支持跨平台并且具有原生数据库连接性，它在易于学习和实施方面有着令人印象深刻的记录。

在本章中，你将学习如何编译、安装和配置 Apache 以使用 mod_php（Apache 的 PHP 模块）。你还将学习如何保护 PHP 并使用许多 PHP 应用程序。

如果你在 Windows 上使用 Apache，我将在第 21 章中向你展示如何在 Windows 版 Apache 上运行 PHP 脚本。

### 理解 PHP 的工作原理

PHP 是一种解释型语言，传统上用于服务器端脚本。HTML 页面中嵌入了 PHP 代码，这些代码由服务器模块或 CGI 脚本解析以产生所需的输出，然后发送到 Web 客户端；Web 客户端永远不会看到任何 PHP 代码。以下是一个简单的嵌入式 PHP 页面示例。

# 本章内容

- 处理 PHP
- 编译和安装 PHP
- 使用 `php.ini` 文件配置 PHP
- 配置 Apache 以支持 PHP
- 创建命令行 PHP 脚本
- 创建 PHP 脚本
- 使用 PHP 对目录进行索引
- 使用 PHP 处理缺失页面
- 使用 PHP 脚本管理用户会话
- 使用 PHP 访问 MySQL 数据库
- 保护 PHP 包含文件
- 使用 PHP 和 MySQL 数据库进行用户身份验证

```html
<HTML>
<HEAD><TITLE> Simple PHP Example </TITLE></HEAD>
<BODY>

    <?php echo "Welcome to PHP"; ?>

</BODY>
</HTML>
```

此 PHP 页面在服务器端的 PHP 引擎解析后，会在 Web 浏览器中打印出字符串“Welcome to PHP”。

这种在 HTML 页面中嵌入代码的方法并非没有争议。许多传统软件开发人员不喜欢这种做法，因为它将代码与展示混合在一起。如果你将 HTML 视为数据的展示载体，那么在展示中混合代码似乎非常短视。然而，数百万 PHP 用户似乎并不在意。PHP 及其类似产品的反对者经常认为，在展示中混合代码会让展示专家的工作变得更困难。在 Web 领域，展示专家实际上是 HTML 或图形设计师，他们不太可能具有编程知识。因此，在 HTML 页面中嵌入脚本可能会使 HTML 设计师的生活变得艰难。然而，PHP 提供了各种库，可与页面模板配合使用来解决这个问题，提供高效的开发方法和更简单的维护过程。这样，开发人员可以专注于业务逻辑，而页面设计师可以在不涉及开发人员或不干扰 PHP 代码的情况下更改动态页面的布局。超过三百万个网站发现这很有价值，使 PHP 成为一个快速应用程序开发（RAD）平台。

PHP 不必仅用于 Web 开发。它也可以编译为独立的脚本解释器，并且可以处理简单的系统管理任务。PHP 的最新版本（第 4 版）已将核心语言引擎 Zend 解析器抽象化到足以考虑用于其他技术的程度，在这些技术中，PHP 可以作为嵌入式语言平台，就像 VBA 之于微软 Office 套件一样。

### 将 PHP 引入你的公司

虽然像 Linux、MySQL 和 Perl 这样的开源软件在企业环境中变得越来越普遍，但通常仍然需要向上级管理层推销这些技术。以下是当 PHP 符合需求，但管理层需要一份 PHP 是正确解决方案的理由清单时，在许多场合对我行之有效的做法：

- 快速 Web 开发——使用 PHP 脚本快速上手非常容易。用 PHP 编写 Web 和数据库集成应用程序只需几小时到几天，而 C/C++ 和 Java 等编程语言可能需要数月。与大多数通用编程语言不同，PHP 是一种脚本语言，对动态 Web 页面开发有特定的亲和力和重点。





- **跨主要操作系统平台可移植** — PHP 可在所有主要平台上运行，包括 Unix、Linux、Windows、OS/2 和 Mac OS。
- **跨主要 Web 服务器平台可移植** — 在 PHP 4.0 中，Web 服务器接口（Server API，或 SAPI）已被抽象化，使其能够与包括 Apache、IIS、IPanet/Netscape Enterprise Server 和 Zeus 在内的不同 Web 服务器良好集成。
- **内置对主要数据库的支持** — PHP 为所有主要数据库实现了原生接口，包括 MySQL、Postgres、Oracle、DB2 和 MS SQL Server，这使其成为数据库驱动 Web 开发的理想选择。
- **高性能** — PHP 4 为高性能进行了重新设计；它比 PHP 3 快许多倍。Zend Technologies 提供的一个免费附加模块称为 Zend Optimizer，可以将应用程序优化到比未优化的快 40 到 100 倍。许多大型 Web 站点正在使用 PHP；你可以在 www.php.net 的 PHP 官方网站上了解它们。
- **对新开发者易于学习** — PHP 是一种类似 C 的语言，具有自动内存管理（即，无需担心指针）。PHP 还具有 Perl、Java 和 C++ 的元素。任何熟悉这些主要语言的人都可以在数小时到数天内学会 PHP。
- **支持互联网标准** — 支持互联网标准，包括 IMAP、FTP、POP、XML、W3DX、LDAP、NIS 和 SNMP。这意味着 PHP 可以轻松地与不同的标准和技术进行接口对接——全部通过一个通用的工具集完成，无需昂贵的第三方模块。
- **对企业友好** — 许多大型企业已经采用了 Java 平台，而这些公司中的许多 Java 布道者往往总是想方设法将 Java 变成即使是最小项目的“理想”平台，这通常会导致漫长的开发周期。此类公司通常倾向于对其它技术说“不”，理由是其他核心业务逻辑已经用 Java 实现，因此没有 PHP 或其同类技术的空间。现在你可以说，别着急！PHP 4 支持在任何拥有 Java 虚拟机（JVM）的系统上直接访问 Java 对象。它甚至支持 Windows 平台上的分布式 COM（DCOM）。PHP 正积极整合 Java 和其他企业技术，使得拒绝 PHP 变得越来越困难。
- **开源社区** — 开源已被证明是一种非常有效的软件开发方法。作为 Apache 软件基金会的一个开源项目，PHP 享受这一方法带来的益处。PHP 核心开发者参与了许多开源支持论坛，如 Usenet 新闻组和 IRC 频道。许多 Web 软件咨询公司也提供商业支持。

## PHP 的前置条件

大多数使用 PHP 的网站同时也使用 MySQL 作为数据库。如果你计划使用 MySQL，你应该从 www.mysql.com/downloads/index.html 下载 MySQL 的源代码或二进制发行版。阅读安装文档以了解如何在你系统上安装 MySQL。你还需要 MySQL 开发包。覆盖所有平台的 MySQL 安装超出了本书的范围。

在我运行 Apache 的 Linux 系统上，我安装了：

- i386 系统的服务器 RPM
- i386 系统的客户端程序 RPM
- i386 系统的开发用包含文件和库 RPM
- i386 系统的客户端共享库 RPM

如果你想编译支持 MySQL 的 PHP，则需要这些包含文件和库。

# 编译和安装 PHP

当前版本的 PHP 是 4.0。你可以从 `www.php.net` 下载 PHP 的源代码或二进制发行版。本节假设你已下载了最新的 PHP 源代码发行版，`php-4.1.0.tar.gz`。

> 如果你在 Windows 平台上，请阅读第 21 章“运行 PHP 脚本”以了解如何为 Apache 安装 PHP。

下载源代码发行版后，使用 `tar xvzf php-4.1.0.tar.gz` 命令在目录中提取源代码。我建议你将其安装在与安装 Apache 源代码相同的目录中。例如，如果你将 Apache 源代码安装在 `/usr/local/src/httpd-2.0.16` 目录中，那么请将 PHP 提取到 `/usr/local/src` 目录中。将会创建一个名为 `php-4.1.0` 的新子目录。

此时，你必须决定你计划如何运行 PHP。PHP 可以作为 Apache 模块运行（嵌入在服务器本身中或作为 DSO 模块），也可以作为 CGI 解决方案。CGI 解决方案意味着你在使用 PHP 脚本时不会比常规 CGI 脚本获得任何性能优势，因为每次处理 CGI 模式的 PHP 脚本时都会加载一个 PHP 解释器。

## 将 PHP 构建为 CGI 解决方案

与 Perl 类似，PHP 既可以用于独立脚本，也可以嵌入在 Web 页面中。要构建用于 CGI 模式操作的 PHP 解释器，请执行以下操作：

1. 以 root 用户身份切换到 PHP 源代码发行版目录并运行：
   `./configure --enable-docs-path`
2. 现在运行 `make && make install` 以在你的系统上编译和安装 PHP 解释器。

## 将 PHP 构建为 Apache 模块

你可以将 PHP 模块存储在 Apache 二进制文件中，或者将其作为 DSO 模块安装在 Apache 上。DSO 模块的一个优点是，只需在 `httpd.conf` 中注释掉一行配置即可将其卸载，从而节省一些内存。

### 将 PHP 构建为静态 Apache 模块

我假设你已将 Apache 源代码安装在 `/usr/local/src/httpd-version` 目录中，并将 PHP 源代码安装在 `/usr/local/src/php-version` 目录中。以下是如何编译和安装静态 Apache 模块的 PHP：

1. 如果你尚未安装 Apache，请以 root 用户身份从 Apache 源代码发行版目录运行以下命令：

   ```
   ../configure --prefix=/usr/local/web/apache
   ```
   
   如果需要，你可以添加其他选项。运行 `./configure --help` 以确定是否有其他适合你需求的选项。

2. 现在从 PHP 源代码发行版目录运行：

   ```
   ./configure --with-apache=../httpd-version \
   --with-mysql=/usr
   ```
   
   这里 `--with-mysql` 选项设置为 `/usr`，是因为 MySQL RPM 包将包含文件安装在 `/usr/include/mysql` 目录中。如果你的系统 MySQL 包含文件位于其他位置，你应该使用不同的目录名。你可以使用 `locate mysql.h` 命令来查找 MySQL 包含文件存放的位置，该命令在大多数具有 locate 数据库功能的 Unix 系统上都可用。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_455_0.png)

如果你不打算使用 MySQL 配合 PHP，或者希望使用 PHP 内置的 MySQL 支持（这仅在你不打算使用 `mod_perl` 或其他 Apache 模块配合 MySQL 时推荐），则不需要 `--with-mysql` 选项。

3. 运行 `cp php.ini-dist /usr/local/lib/php.ini` 命令，将 `php.ini-dist` 文件复制到 `/usr/local/lib` 并命名为 `php.ini`。这是稍后在“使用 php.ini 配置 PHP”部分中讨论的 PHP 配置文件。
4. 运行 `make && make install` 以编译和安装 PHP 部分的源代码。
5. 现在切换到 Apache 源代码发行版目录并运行：

   ```
   ./configure --prefix=/usr/local/apache
   --activate-module=modules/php4/libphp4.a
   ```
   
   你可以在上述命令行中添加任何其它选项。运行 `./configure --help` 命令以获取有关其他选项的信息。

6. 运行 `make && make install` 以编译和安装支持 PHP 的 Apache。
7. 运行 `/usr/local/apache/bin/apachectl restart` 命令以重新启动（或启动）Apache。

# 将 PHP 构建为动态共享对象（DSO）模块

在你将 PHP 作为 DSO 模块使用之前，必须已在 Apache 中启用 DSO 支持。要重新编译具有 DSO 支持的 Apache，请执行以下操作：

1. 以 root 用户身份从 Apache 源代码发行版目录运行以下命令：

   ```
   ./configure --prefix=/usr/local/apache --enable-so
   ```
   
   你可以根据需要添加其他选项。

2. 你可以使用 `make && make install` 命令编译和安装 Apache。

在你拥有一个启用 DSO 支持的 Apache 服务器后，你可以执行以下操作来为 PHP 创建一个 DSO 模块：

1. 以 root 用户身份从 PHP 源代码发行版目录运行以下命令：

   ```
   ./configure --with-apxs2=/usr/local/apache/bin/apxs \
       --with-mysql=/usr
   ```
   
   这里 `--with-mysql` 选项设置为 `/usr`，是因为 MySQL RPM 包将包含文件安装在 `/usr/include/mysql` 目录中。如果你的系统 MySQL 包含文件位于其他位置，你应该使用不同的目录名。你可以使用 `locate mysql.h` 命令来查找 MySQL 包含文件存放的位置，该命令在大多数具有 locate 数据库功能的 Unix 系统上都可用。

2. 现在运行 `make && make install` 以编译和安装 Apache 的 PHP DSO 版本模块。
3. 运行 `/usr/local/apache/bin/apachectl restart` 命令以重新启动（或启动）Apache。

# 配置 Apache 以支持 PHP

在你已安装 Apache 的 `mod_php` 模块并配置了前面讨论过的 `php.ini` 之后，你就可以配置 Apache 以支持 PHP 如下：

1. 如果你已将 PHP 编译并安装为 Apache 的 DSO 模块，请将以下行添加到 `httpd.conf` 文件中：

   ```
   LoadModule php4_module    modules/libphp4.so
   ```

2. 将以下行添加到 `httpd.conf` 文件中

   ```
   <Files *.php>
     SetOutputFilter  PHP
     SetInputFilter   PHP
   </Files>
   ```
   
   这告诉 Apache 任何带有 `.php` 扩展名的文件都必须被视为 PHP 脚本，并应使用 PHP 输入和输出过滤器进行处理。





没有必要为 PHP 脚本使用不同的扩展名。例如，你可以将上面的 AddType 指令设置为 `AddType application/x-httpd-php .html`，从而使你的所有 HTML 页面都被当作 PHP 脚本处理。我不建议使用 `.html` 扩展名，因为你的许多 HTML 页面可能并不是 PHP 脚本，你也不希望服务器因解析每个页面中的 PHP 脚本而变慢。

- 保存 `httpd.conf` 文件，并按常规重启 Apache Web 服务器。

现在你可以开始为你的网站创建 PHP 脚本了。你可以创建 PHP 脚本并将其存储在网站文档树的任何位置，Apache 会自动将它们作为 PHP 脚本处理。

## 使用 php.ini 配置 PHP

PHP 配置文件名为 `php.ini`，存储在 `/usr/local/lib` 目录中。当加载 PHP 模块时，它会读取 `php.ini` 文件。该模块会在当前工作目录、环境变量 `PHPRC` 指定的路径以及 `/usr/local/lib` 中查找 `php.ini`。

如果你使用 PHP 作为 CGI 解决方案，每次运行 PHP CGI 时都会读取 `php.ini`。另一方面，当 PHP 作为 Apache 模块加载时，它只读取一次。如果你修改了 `php.ini` 文件，必须使用 `/usr/local/apache/bin/apachectl restart` 命令重启 Apache 服务器才能重新加载这些更改。

## httpd.conf 中的 PHP 指令

在 PHP 4 版本中，`httpd.conf` 中仅允许使用以下章节中显示的四个特定的 `mod_php` 指令。所有其他 PHP 指令必须位于 `php.ini` 文件中。

### php_admin_flag

`php_flag` 指令允许你为配置参数设置布尔值（On 或 Off）。此指令不能出现在目录容器或逐目录的 .htaccess 文件中。

- **语法：** `php_admin_flag name On | Off`
- **上下文：** 服务器配置，虚拟主机

### php_admin_value

`php_admin_value` 指令允许你为配置参数设置值。此指令不能出现在目录容器或逐目录的 .htaccess 文件中。

- **语法：** `php_admin_value name value`
- **上下文：** 服务器配置，虚拟主机

### php_flag

`php_flag` 指令允许你为配置参数设置布尔值（On 或 Off）。

- **语法：** `php_flag name On | Off`
- **上下文：** 服务器配置，虚拟主机，目录，逐目录（.htaccess）

例如：

```
php_flag display_errors On
```

### php_value

`php_value` 指令允许你为配置参数设置值。

- **语法：** `php_value name value`
- **上下文：** 服务器配置，虚拟主机，目录，逐目录（.htaccess）

例如：

```
php_value error_reporting 15
```

## php.ini 中的 PHP 指令

`php.ini` 文件具有简单的 *directive = value*（指令 = 值）结构语法。以分号开头的行或仅包含空格的行将被忽略。区段名称包含在括号中。你可以在 `www.php.net/manual/en/configuration.php` 上了解 `php.ini` 中所有可用的指令。以下章节讨论了一些最有用的指令。

### auto_append_file

`auto_append_file` 指令允许你为每个经过 PHP 解析的页面设置一个页脚文档。

- **语法：** `auto_append_file filename`

### auto_prepend_file

`auto_prepend_file` 指令允许你为每个经过 PHP 解析的页面设置一个页眉文档。

- **语法：** `auto_prepend_file filename`

下面的示例显示 `preload.php` 页面将在每个 PHP 页面处理之前加载。这个页面是建立数据库连接的好地方。

```
auto_prepend_file preload.php
```

### default_charset

`default_charset` 指令设置默认字符集。

- **语法：** `default_charset char_set`

以下示例将默认字符集设置为 8 位 UTF：

```
default_charset = "UTF-8"
```

### disable_functions

`disable_functions` 指令允许你出于安全原因禁用一个或多个函数。

- **语法：** `disable_functions function_name [function_name]`

你可以指定以逗号分隔的 PHP 函数列表，如下所示：

```
disable_functions = fopen, fwrite, popen
```

在上面的例子中，负责打开文件、写入文件或管道的函数被禁用了。

> **注意**：此指令不受 `safe_mode` 指令的影响。

### display_errors

`display_errors` 指令启用或禁用屏幕上错误消息的打印。此功能仅建议在开发系统上使用，而不建议在生产服务器上用于生产环境。对于生产系统，你应该使用 `log_errors` 和 `error_log` 指令将错误消息记录到文件或 syslog 服务器中。

- **语法：** `display_errors On | Off`

### enable_dl

`enable_dl` 指令启用或禁用动态加载 PHP 扩展的功能。

- **语法：** `enable_dl On | Off`
- **默认设置：** `enable_dl On`

### error_append_string

`error_append_string` 指令设置附加到错误消息末尾的字符串。请参阅上面的 `error_prepend_string` 指令。

- **语法：** `error_append_string string`

### error_log

`error_log` 指令设置 PHP 错误日志的路径。你可以指定日志文件的完整限定路径名，或者在 Unix 系统上指定关键字 `syslog` 以使用 syslog 设施记录日志。在 Windows 系统上，将此指令设置为 `syslog` 会将日志条目写入 Windows 事件日志。

- **语法：** `error_log filepath`

### error_prepend_string

`error_prepend_string` 指令设置前置到错误消息开头的字符串。此指令与 `error_append_string` 配合使用。

- **语法：** `error_prepend_string string`

如果你不记录错误，则错误消息将显示在屏幕上。例如，通过使用这两个指令，你可以用红色字体打印错误消息：

```
error_prepend_string = "<font color=red>"
error_append_string = "</font>"
```

### error_reporting

`error_reporting` 指令允许你指定一个位域来指定错误报告级别。位域可以使用表 15-2 中显示的预定义常量构造。

- **语法：** `error_reporting [bit field] [predefined constant]`

| 常量 | 含义 |
| :--- | :--- |
| `E_ALL` | 显示所有错误、警告和通知 |
| `E_ERROR` | 仅显示致命运行时错误 |
| `E_WARNING` | 显示运行时警告 |
| `E_PARSE` | 显示解析错误 |
| `E_NOTICE` | 显示代码中可能存在问题的通知 |
| `E_CORE_ERROR` | 显示 PHP 初始启动期间发生的致命错误 |
| `E_CORE_WARNING` | 显示 PHP 初始启动期间发生的警告 |
| `E_COMPILE_ERROR` | 显示致命的编译时错误 |
| `E_COMPILE_WARNING` | 显示编译时警告（非致命错误） |
| `E_USER_ERROR` | 用户生成的错误消息 |
| `E_USER_WARNING` | 用户生成的警告消息 |
| `E_USER_NOTICE` | 用户生成的通知消息 |

你可以使用位域运算符，如 `~`（取反）、`&`（按位“与”）和 `|`（按位“或”）来创建自定义错误报告级别。例如：

```
error_reporting = E_ALL & ~E_WARNING & ~E_NOTICE
```

这告诉 PHP 引擎显示除了警告和通知以外的所有错误。不推荐在生产服务器上显示错误消息。你应该仅在开发系统上或生产服务器的开发阶段显示错误。在生产服务器上，使用 `log_errors` 和 `error_log` 指令将日志写入文件或 syslog 设施。

### extension

`extension` 指令允许你为 PHP 本身加载动态扩展模块。

- **语法：** `extension module_name`

例如，以下指令通过 extension 指令为 Windows 上的 PHP 加载图形库 GD 扩展。PHP 引擎在服务器启动时加载此类动态模块。

```
extension=php_gd.dll
```

同样，以下指令在支持 DSO 的 Unix 平台上为 Apache 加载 MySQL DSO 模块：

```
extension=mysql.so
```

你可以根据需要重复使用 `extension` 来加载不同的模块。




## extension_dir

`extension_dir` 指令定义了动态加载 PHP 模块的存储目录。默认值适用于大多数 PHP 安装环境。

**语法：** `extension_dir` *directory*

**默认设置：** `extension_dir` ./

## implicit_flush

`implicit_flush` 指令启用或禁用脚本输出的隐式刷新，当使用 print、echo 和 HTML 块进行输出时生效。开启此指令后，每次 `print()`、`echo` 或 HTML 块输出后都会触发 `flush()` 调用。这对于调试非常有用，但在生产环境中会严重影响性能。仅建议用于开发系统。

**语法：** `implicit_flush` On | Off

**默认设置：** `implicit_flush` Off

## include_path

`include_path` 指令设置了 `include()` 和 `require()` 函数的路径。您可以列出多个目录。

**Unix 语法：** `include_path` *path*[:*path*]

**Windows 语法：** `include_path` *path*;[*path*]

例如，以下指定 PHP 应首先在 /usr/local/lib/php 目录中查找包含文件，然后在当前目录中查找：

```
include_path = /usr/local/lib/php:..
```

在 Windows 上，此指令设置如下：

```
include_path = /usr/local/lib/php;..
```

## log_errors

`log_errors` 指令启用或禁用 PHP 错误日志记录。您必须使用 `error_log` 指令指定日志路径或 `syslog` 文件。

**语法：** `log_errors` On | Off

## magic_quotes_gpc

`magic_quotes_gpc` 指令启用或禁用 GET、POST 和 cookie 数据中引号（单引号、双引号、null 和反斜杠字符）的转义。

**语法：** `magic_quotes_gpc` `On` | `Off`

**默认设置：** `magic_quotes_gpc` `On`

## magic_quotes_runtime

`magic_quotes_runtime` 指令启用或禁用内部生成文本的自动引用。换句话说，如果您从数据库中检索一条记录，其中嵌入了 `<?php` ... `?>` 类型的标签，标签内的内容（属于数据的一部分）将被转义（即不会处理），而不会被当作 PHP 代码执行。

**语法：** `magic_quotes_runtime` `On` | `Off`

**默认设置：** `magic_quotes_runtime` = `Off`

## max_execution_time

`max_execution_time` 指令设置脚本产生输出所能运行的最大时间。当脚本运行时间超过指定的秒数后，PHP 将使该脚本超时。除非您计划运行耗时很长的 PHP 脚本，否则默认值在大多数情况下都是可接受的。

**语法：** `max_execution_time` `seconds`

**默认设置：** `max_execution_time` `30`

## memory_limit

`memory_limit` 指令设置 PHP 脚本可消耗的最大 RAM 内存量。默认值 8MB 对于中小型 PHP 脚本来说已经足够。您也可以以字节为单位指定内存大小。

**语法：** `memory_limit` `bytes` `[nM]`

**默认设置：** `memory_limit` `8M`

例如，以下两者是等效的：

```
memory_limit 8M
memory_limit 8388608
```

## output_buffering

`output_buffering` 指令允许您启用或禁用输出缓冲。当设置为 `On` 时，您可以在 PHP 脚本的任何位置打印 HTTP 头。即使在打印其他内容后，仍能在脚本中间输出头部信息，这意味着即使脚本之前部分成功，也可以显示错误页面。

**语法：** `output_buffering` `On` | `Off`

**默认设置：** `output_buffering` `On`

您也可以使用**内置**的 `ob_start()` 和 `ob_end_flush()` 指令直接开始和结束内容刷新。**例如**：

```php
<?php
ob_start();  // Buffer all output
echo "Buffered contents \n";
ob_end_flush(); // Page rendered. flush the output buffer.
?>
```

在此处，输出被缓冲。

## safe_mode

`safe_mode` 指令在将 PHP 用作 CGI 解决方案时设置 PHP 的安全模式。当设置为 `On` 时，此指令确保由 PHP 解释器在 CGI 模式下运行的 PHP 脚本不允许访问超出 Web 站点文档根目录的范围。

- **语法：** `safe_mode On | Off`
- **默认设置：** `safe_mode Off`

## safe_mode_allowed_env_vars

`safe_mode_allowed_env_vars` 指令允许您为所有用户通过使用 `putenv()` 函数可以更改的环境变量设置前缀。默认值允许用户更改任何以 `PHP_` 前缀开头的环境变量。

- **语法：** `safe_mode_allowed_env_vars prefix`
- **默认设置：** `safe_mode_allowed_env_vars PHP_`

## safe_mode_protected_env_vars

`safe_mode_protected_env_vars` 指令允许您设置一个逗号分隔的环境变量列表，任何使用 `putenv()` 函数的 PHP 脚本都不能更改这些变量。

- **语法：** `safe_mode_protected_env_vars environment_variable [environment_variable ...]`
- **默认设置：** `safe_mode_protected_env_vars = LD_LIBRARY_PATH`

如果您希望保护所有以 `HTTP_` 前缀开头的环境变量，可以使用：

```
safe_mode_protected_env_vars = HTTP_
```

## track_errors

`track_errors` 指令启用或禁用将错误消息存储在名为 $php_errormsg 的 PHP 变量中。

**语法：** `track_errors On | Off`

## upload_max_filesize

`upload_max_filesize` 指令设置通过 PHP 可上传的文件的最大大小。默认限制为 2MB (2M)。或者，您可以仅指定千字节数。

**语法：** `upload_max_filesize kilobytes`

**默认设置：** `upload_max_filesize 2M`

例如，以下两者是等效的：

```
upload_max_filesize = 2M
upload_max_filesize = 2097152
```

## upload_tmp_dir

`upload_tmp_dir` 指令定义通过 PHP 上传文件的临时目录位置。在 Unix 系统上，习惯上将其设置为 /tmp；在 Windows 系统上，通常设置为 /temp 或保持默认，在这种情况下，PHP 使用系统默认值。

**语法：** `upload_tmp_dir directory`

# 处理 PHP

本节介绍了一些示例，展示如何使用 PHP 脚本生成动态 Web 内容。

## 创建简单的命令行 PHP 脚本

配置好 PHP 后，您可以像运行 Perl 脚本一样从命令行运行 PHP 脚本。默认情况下，PHP 解释器在 Unix 系统中安装在 /usr/local/bin 目录；在 Windows 系统中，它安装在该发行版解压缩的目录中。您可以创建一个名为 `test.php` 的简单 PHP 脚本，如清单 15-1 所示。

### 清单 15-1: test.php

```php
#!/usr/local/bin/php -q
# For Windows change the above line to:
#D:/path/to/php -q
#

<?php

echo "Welcome to the PHP World\n";
?>
```

您可以使用 /usr/local/bin/php test.php 从命令行运行此脚本，或者通过 chmod +x test.php 更改脚本的文件权限，然后在脚本目录中使用 ./test.php 执行它。这里使用的 -q 选项告诉 PHP 抑制 HTTP 内容类型头，否则它会打印输出以使符合 Web 标准。

## 创建简单的 PHP Web 页面

为您的网站创建 PHP 脚本就像上一节中的示例一样简单。清单 15-2 展示了一个名为 hello.php 的简单脚本。

### 清单 15-2: hello.php

```html
<html>
    <head><title>Hello World Script</title>
<body>

    <?php echo "Hello World from PHP"; ?>
</body>
</html>
```

当您将此脚本保存在 Web 服务器文档树中的某个目录内时，您可以通过 http://your_web_server/path/to/hello.php 访问它。如果如您在此前本章节“为 PHP 配置 Apache”部分中指示的那样使用了诸如 AddType application/x-httpd-php .php 之类的指令，那么 PHP 模块将解析并执行这个单行 PHP 脚本，打印出“Hello World from PHP”这句话。请注意，PHP 会自动打印适当的 Content-Type 头 (text/html)。




让我们编写一个更有用的脚本，如列表 15-3 所示，该脚本显示安装在 Web 服务器上的 PHP 信息。

## 列表 15-3：info.php

```html
<html>
  <head><title>Hello World Script</title>
  <body>
    <?php
      phpinfo();
    ?>
  </body>
</html>
```

此页面调用名为 `phpinfo()` 的 PHP 函数，根据当前使用 `php.ini` 配置的参数，显示大量的 PHP 选项。

## 使用 PHP 脚本作为服务器端包含

如果您希望在服务器端包含（SSI）调用中使用 PHP 脚本，可以使用以下 SSI 标签调用您的 PHP 脚本：

```
<!--#include virtual="/path/script_name.php"-->
```

例如：

```
<!--#include virtual="/phppssi/test.php"-->
```

此处，名为 `/phppssi/test.php` 的 PHP 脚本将从使用上述 SSI 调用的页面中加载。要使 PHP 脚本与 SSI 配合工作，您必须执行以下操作：

- 在包含需要通过 SSI 调用运行的 PHP 脚本的目录中启用 **ExecCGI** 选项。
- 确保相同目录中的 **IncludesNoExec** 选项已禁用。例如：

```apache
DocumentRoot  "/www/mysite/htdocs"
<Directory  "/www/mysite/htdocs/parsed">
    Options +Includes

    AddType text/html .shtml

    <FilesMatch "\\.shtml[.$]">
        SetOutputFilter INCLUDES
    </FilesMatch>

</Directory>

<Directory "/www/mysite/htdocs/php">
    Options +ExecCGI

    <Files *.php>
        SetOutputFilter PHP
        SetInputFilter PHP
    </Files>

</Directory>
```

在上述配置片段中，/www/mysite/htdocs/parsed 目录中所有以 .shtml 扩展名结尾的文件都被视为 SSI 页面，而 /www/mysite/htdocs/php 目录中的所有文件都被视为可以通过 SSI 调用运行的 PHP 脚本。现在，/www/mysite/htdocs/parsed 目录中的 SSI 页面可以通过以下 SSI 调用调用 /www/mysite/htdocs/php 目录中的脚本：

```
<!--#include virtual="/php/script_name.php"-->
```

## 使用 PHP 页面作为目录索引

如果之前正如“配置 Apache 以支持 PHP”中所述，您已在 httpd.conf 中启用了 PHP 支持，也可以使用 PHP 脚本作为目录索引页面。例如：

```
DirectoryIndex index.html index.php
```

这里指令将 index.html 设置为目录的首选索引页面，但如果缺少 index.html，则使用 index.php 代替。

然而，如果您希望使用 PHP 脚本作为默认索引，请反转文件名的顺序，使 index.php 位于其他文件名之前。例如：

```
DirectoryIndex index.php index.html
```

这样，Apache 将首先查找 index.php 脚本。

## 使用包含文件

PHP 允许您在脚本中包含外部 PHP 代码库文件或普通 HTML 文件。例如：

```html
<html>
<head>
  <title> PHP Resource Site </title>
</head>
<body>
<h1>PHP Resource</h1>
<hr>
<p>Welcome to PHP Resource Site. </p>
<?php
  include('/www/mysite/htdocs/global/copyright.html');
?>
</body>
</html>
```

这里简单的 PHP 脚本是一个单一的函数调用 `include('/www/mysite/htdocs/global/copyright.html');`，它告诉 PHP 包含名为 /www/mysite/htdocs/global/copyright.html 的文件。这个 copyright.html 页面被包含在当前页面中，就像 `<!--#include virtual="/path/filename"-->` 服务器端包含（SSI）标签一样。但是，被包含的文件本身也可以是 PHP 脚本。例如：

```php
include('/www/mysite/htdocs/global/copyright.php');
```

从给定目录加载名为 copyright.php 的 PHP 脚本。包含文件中的脚本将被执行。包含文件中的任何代码都可以访问父脚本中的变量。例如，copyright.php 脚本可以访问 $year 变量。

```php
<?php
  $year = '2001';
  include('/www/mysite/htdocs/global/copyright.php');
?>
```

因此，`copyright.php` 脚本可以包含诸如 `echo "The current year is: $year \n";` 这样的语句。您可以包含多个文件，或者多次包含同一个文件。每次被包含的脚本都会被执行。例如：

```php
<?php
    $year = '2001';
    include('/www/mysite/htdocs/global/copyright.php');
    $year = '2002'
    include('/www/mysite/htdocs/global/copyright.php');
?>
```

如果 `copyright.php` 脚本由一个简单的 PHP 脚本组成，例如 `<?php echo "The current year is: $year\n"; ?>`，那么上述脚本将显示：

```
The current year is: 2001
The current year is: 2002
```

您还可以使用 `include_once()` 来包含 PHP 脚本或静态 HTML 文件。然而，如果您使用 `include_once()` 代替 `include()`，包含脚本中的代码只执行一次。例如：

```php
<?php
    $year = '2001';
    include_once('/www/mysite/htdocs/global/copyright.php');
    $year = '2002'
    include_once('/www/mysite/htdocs/global/copyright.php');
?>
```

这里相同的 `copyright.php` 的输出是：

```
The current year is: 2001
```

第二次 `include_once()` 不会再次执行 `copyright.php`。您可以使用 `include()` 或 `include_once()` 函数来集中管理多个 PHP 页面所需的通用代码或 HTML 文件。

您还可以类似地使用 require() 和 require_once() 函数。require() 函数用指定文件的内容替换自身。此替换发生在 PHP 引擎编译代码期间，而不是在调用脚本执行期间。require_once() 函数仅插入所需脚本的内容一次。

> **注意** include()、include_once()、require() 和 require_once() 函数可以访问文件系统中的任何文件，只要用于运行 Web 服务器的用户 ID 对该文件具有读取访问权限。

## 使用 PHP 增强错误处理

Apache 提供了一个名为 ErrorDocument 的指令，它允许您显示服务器错误的自定义错误页面。例如：

```
ErrorDocument 404 /missing.html
```

每当服务器遇到缺失文件或目录的请求时，它都会发送 Status: 404 Not Found 响应，然后显示 /missing.html 页面。您可以将其更改为：

```
ErrorDocument 404 /missing.php
```

这会导致每当 Apache 遇到相同错误时执行名为 missing.php 的 PHP 脚本。但是，Microsoft IE 会检测 40x 响应并显示其生成的自定义错误消息。为了绕过此类页面，您可以使 missing.php 页面返回 Status: 200 OK 响应，而不是其他。例如，使用此代码：

```php
<?php
   header("Status: 200 OK\n");
   header("Location: /missing.html");
?>
```

missing.php 脚本显示 HTTP 成功头部，然后指示 Apache 将 Web 客户端重定向到 /missing.html。

## 使用 PHP 处理 Web 表单

PHP 使 Web 表单处理变得简单。您可以在 PHP 脚本中将 Web 表单数据字段作为变量访问。列表 15-4 显示了一个简单的 Web 表单，其中有一个名为 keywords 的单个输入字段。

```html
<html>
<head><title>Simple HTML Form</title>
</head>

<body>

<form action="form.php">
<input type="text" name="keywords" size=30>
<input type=submit>

</form>
</body>
</html>
```

当用户通过 Web 浏览器提交此表单时，浏览器会发送类似 http://server/form.php?keywords=value_entered_in_the_form 的 GET 请求。

例如，如果您输入关键字 makesite 并提交上述表单到 www.domain.com，Web 服务器将收到对 http://www.domain.com/form.php?keywords=makesite 的请求。

负责处理此 Web 表单的 form.php 脚本如列表 15-5 所示。

```php
<?php

    echo "You have entered $keywords keyword(s).\n";

?>
```

这个简单的 PHP 脚本打印出在名为 form.html 的 HTML 表单的 keywords 字段中输入的关键字。

**对于以下请求：**

http://www.domain.com/form.php?keywords=makesite

**脚本打印：**

You have entered makesite as keyword(s).




在此处，变量 `$keywords` 被赋值为 `makesite`，因为通过 GET 方法传递给服务器的查询字符串为 `keywords=makesite`。如果将 Web 表单中的 `<form action="form.php">` 行修改为 `<form action="form.php" method="POST">`，那么将使用 HTTP POST 方法，`keywords=makesite` 数据将由 PHP 模块读取，并自动作为脚本变量 `$keywords` 的值提供给脚本。

如果 Web 表单包含多个字段，所有字段都会被转换为相应命名的脚本变量。例如，`simple_form.html` 的修改版如清单 15-6 所示。

### 清单 15-6: modified_simple_form.html

```html
<html>
    <head>
        <title>Simple HTML Form</title>
    </head>
    <body>
        <form action="modified_form.php" method="POST">

            <input type="text" name="keywords" size=30>

            <select name="case">
                <option value="lower">Lower case</option>
                <option value="upper">Upper case</option>
                <option value="dontcare">Don't Care</option>
            </select>

            <input type=submit>

        </form>
    </body>
</html>
```

在此处，该表单有两个输入字段（`keywords` 和 `case`）。

当通过 POST 方法提交此 Web 表单时，清单 15-7 中显示的 `modified_form.php` 将接收所有数据。

### 清单 15-7: modified_form.php

```php
<?php
    print "You entered:<br>Keywords: $keywords <br>Case: $case\n";
?>
```

例如，当用户输入 `makesite` 作为关键字字段的值，并从下拉列表中选择 `dontcare` 大小写选项时，脚本（`modified_form.php`）将显示以下内容：

You entered:
Keywords: makesite
Case: upper

## 使用 PHP 创建会话

PHP 4 引入了原生会话管理，这使得创建用户会话变得简单。这意味着你可以在用户从一个页面移动到另一个页面时跟踪用户。在 PHP 中维护会话有两种方式。

### 使用 HTTP  cookies 创建用户会话

这是默认方法。要创建会话，你需要在 PHP 页面中调用 `session_start()` 函数。例如，查看一个名为 `start.php` 的简单 PHP 页面，如清单 15-8 所示。

### 清单 15-8: start.php

```php
<?php
session_start();
session_register('count');
$count++;
?>
<html>
<head><title>Start Session</title>
</head>
<body bgcolor="Red">

<?php echo "You have visited this page $count time(s)."; ?>

<p>
<a href="/next_page.php">Next</a>
</p>
</body>
</html>
```

在清单中你可以看到两个 PHP 脚本。第一个脚本通过调用 `session_start()` 函数创建会话。它还使用 `session_register()` 函数注册了一个名为 `count` 的会话变量，并将该变量递增 1。注意，该脚本被保留在 `<html>` 标签之外。这是必需的，因为该脚本设置了会话 cookie，而 cookie 是一个 HTTP 头，必须出现在任何内容之前。上述 PHP 页面假设你在 `php.ini` 中将输出缓冲设置为 Off。这是默认设置，因为输出缓冲会导致 PHP 页面速度变慢。如果你在 `php.ini` 中通过设置 `output_buffering = On` 来启用输出缓冲，你可以将 PHP 脚本放在页面的任何位置。

第二个脚本只是打印 `$count` 的值。现在，如果你第一次使用 Web 浏览器加载此页面，`session_start()` 函数将创建一个新的基于 HTTP cookie 的会话。发送到你的 Web 浏览器的 cookie 将具有以下类似属性：

Cookie 名称: `PHPSESSID`
域名: `192.168.1.100`
路径: `/`
过期时间: `会话结束`
安全: `否`
数据: `3de4aa1f73e33dd8f2c8b8d9f69e442e`

发送到 Web 浏览器的 cookie 名称为 `PHPSESSID`。这是在 `php.ini` 中通过以下行设置的默认名称：

`session.name = PHPSESSID`

如果你愿意，可以将其更改为其他名称。默认情况下，cookie 仅对 Web 服务器本身有效。上述示例 cookie 显示 cookie 的域字段设置为 Web 服务器的 IP 地址。如果你希望会话 cookie 在域名内的多个 Web 服务器之间有效，你可以将 `php.ini` 文件中的 `session.cookie_domain` 指令设置为你的 Web 站点的顶级域名。例如，如果你有 三个 Web 站点——`corp.domain.com`、`www.domain.com` 和 `extranet.domain.com`——并希望会话 cookie 在这三个站点中均有效，你可以如下设置 `session.cookie_domain`：

`session.cookie_domain = .domain.com`

注意顶级域名（`domain.com`）前的前导点；它使 cookie 在该域名下的所有主机上有效。

默认情况下，会话 cookie 在会话结束时过期。换句话说，当 Web 浏览器关闭时，会话 cookie 过期。这种默认行为通过 `php.ini` 文件中的 `session.cookie_lifetime` 指令设置。默认情况下设置为 0，这使 cookie 在会话结束时（即用户关闭浏览器时）过期：

`session.cookie_lifetime = 0`

> **注意** PHP 不在 cookie 中存储任何用户数据。Cookie 只是一个指向服务器端用户数据的标识符。

在清单 15-8 中的第一个脚本创建会话后，你可以在其他页面中轻松访问会话变量。例如，清单 15-9 显示了 `next_page.php`，它使用了在 `start.php` 中创建的名为 `$count` 的会话变量。

### 清单 15-9: next_page.php

```html
<html>
<head><title>Using Session Variables</title>
</head>
<body bgcolor="Red">
<?php
    session_start();
    $count++;
    echo "You have visited this page $count time(s).";
?>

</body>
</html>
```

每当你想在新页面中使用当前会话时，你必须使用 `session_start()` 方法。这有点令人困惑，因为它可能会让你以为正在创建一个新的会话。实际上，`session_start()` 检测现有会话并使用它。在发出 `session_start()` 函数调用后，会话变量变得可用。注意，在此页面中，我们不将脚本放在内容之前。换句话说，我们没有将脚本放在 `<html>` 标签之前，因为我们不再发出新的会话，因此不需要设置新的 cookie。然而，这假设你有一个现有的会话。为了能够在不存在时创建新会话，请将脚本移出内容之外，例如像 `start.php` 页面那样，或在 `php.ini` 中启用 output_buffering。此外，如果你计划允许在任何页面上创建会话，你必须使用 `session_register()` 方法来注册变量，如 `start.php` 中所示。

在任何使用 `session_start()` 选择当前会话的页面中，你也可以使用 `session_register()` 向用户会话添加新变量。

### 使用 URL 编码创建用户会话

如果你不希望依赖 cookies 来维护会话，可以使用 URL 编码的会话。在 `php.ini` 中将 `session.use_cookies` 指令设置为 0 可以启用此模式。然而，与 cookie 模式不同，此模式要求你通过 `<?=SID?>` 作为页面中 URL 的一部分来传递会话 ID（通过 `php.ini` 中的 `session_name` 设置）。例如，清单 15-10 显示了一个名为 `start_url_encoded_session.php` 的页面。

### 清单 15-10: start_url_encoded_session.php

```php
<?php
    session_start();
    session_register('count');
    $count++;
?>

<html>
<head><title>Session Management</title>
</head>
<body bgcolor="Red">

<p>
<?php echo "You have visited this page $count time(s)."; ?>
</p>

<p>
<a href="/next_page.php?<?=SID?>">Next Page</a>
</body>
</html>
```

注意标题为“Next Page”的链接。当用户点击此链接时，浏览器请求 `/next_page.php`，并将名为 `PHPSESSID=session_identifier` 的查询字符串传递给 Web 服务器。这是一个示例 URL 请求：

`http://207.183.233.21/next_page.php?PHPSESSID=6b2cee31528316080ff88fe81ef800bF8`

这使得 PHP 脚本（`next_page.php`）能够知道用户属于哪个会话，并避免使用 HTTP cookies。如果你希望使用此方法维护会话，PHP 页面中的所有链接都必须附加 `<?=SID?>` 标签；否则，会话将无法在每个 PHP 页面上可用。

### 终止用户会话

结束会话与创建会话一样简单。例如，以下 PHP 脚本将终止当前用户会话：

```php
<?php
    session_start();
    $sessionArray = $HTTP_SESSION_VARS;
    session_destroy();

    foreach ($sessionArray as $session_name => $session_value) {
        unset($$session_name);
    }
    unset($sessionArray);
?>
```

在这里，`session_start()` 用于将脚本页面连接到当前会话。然后，`$sessionArray` 被赋值为存储在 global 变量 `$HTTP_SESSION_VARS` 中的会话变量。调用 `session_destroy()` 函数以从服务器删除会话数据。`foreach` 循环显式取消设置每个会话变量。最后，`$sessionArray` 变量也被取消设置，以完全移除会话。




## 注意事项

默认情况下，会话数据存储在文件中（因为 `php.ini` 中设置了 `session.save_handler = files`），并且默认情况下数据存储在 `/tmp` 目录中的会话文件中（前缀为 `sess_identifier`）。如果您希望更改会话文件目录，请在 `php.ini` 中将 `session.save_path` 指令设置为指向另一个目录。请确保除了 Web 服务器用户之外，其他人无法读取会话文件。

# 在 PHP 中使用 MySQL

PHP 与 MySQL、Postgres、Oracle 以及其他流行数据库配合使用效果非常好。MySQL 是 PHP 中应用最广泛的数据库平台。如果您尚未在系统中安装 MySQL，您可以访问 www.mysql.com 了解如何安装。

## 创建一个简单的 PHP 页面以访问 MySQL 数据库

要访问 MySQL 数据库，您需要一个 MySQL 接受的用户名和密码以访问目标数据库。例如，列表 15-11 显示了一个名为 `simple_query.php` 的 PHP 脚本，该脚本以用户 `httpd` 和密码 `nosecret` 从本地主机访问名为 `www` 的 MySQL 数据库。

**列表 15-11: simple_query.php**

```php
<?php
    $host = 'localhost';
    $user = 'httpd';
    $passwd = 'nosecret';
    $database_name = 'www';
    $table = 'users';

    $dbh = mysql_connect($host, $user, $passwd);
    mysql_select_db($database_name, $dbh);
?>
<html>
<head><title>Simple Query Script</title></head>
<body>
<table border=1>
<tr><th>Name</th> <th>Password</th></tr>
<?php
    $result = mysql_query("SELECT * from $table", $dbh);
    while ($myRow = mysql_fetch_row($result)) {
        printf("<tr><td>%s</td><td>%s</td></tr>", $myRow[0],
               $myRow[1]);
    }
?>
</table>
</body>
</html>
```

上述列表中的内容说明如下：

1.  该脚本定义了 `$host`、`$user`、`$passwd`、`$database` 和 `$table` 变量，这些变量可以设置为相应的 MySQL 服务器主机名、用户名、密码、数据库名和表名。
2.  然后，该脚本使用 `mysql_connect()` 函数在每次请求页面时创建到数据库服务器的连接。连接句柄存储在名为 `$dbh` 的另一个变量中。
3.  `mysql_select_db()` 函数选择使用 `$database` 指定的数据库。此时，`$dbh` 句柄已连接到数据库服务器，并在指定的数据库上运行。
4.  脚本输出一个常规的 HTML 文档，其中嵌入了另一个小型 PHP 脚本，该脚本通过使用 `mysql_query()` 函数对连接的数据库执行 SQL 查询。查询作为该函数的参数提供，并附带数据库句柄（`$dbh`）。
5.  查询完成后，脚本使用 `mysql_fetch_row()` 方法从结果数据集中提取数据行。该函数为返回的每行数据返回一个列数组。
6.  使用 `printf()` 函数打印 `$myRow` 数组中的两个元素。请注意，`$myRow` 数组的第一个元素的索引为 0。
7.  while 循环继续执行，直到 `mysql_fetch_row` 没有更多行可获取为止，此时脚本完成，并打印其余的 HTML 文档。使用某些样本数据时，生成的页面如下所示：

```html
<html>
<head><title>Simple Query Script</title></head>
<body>
<table border=1>
<tr><th>Name</th> <th>Password</th></tr>
<tr><td>kabir</td><td>mysecret1</td></tr>
<tr><td>esmith</td><td>sale007</td></tr>
</table>
</body>
</html>
```

8.  如您所见，嵌入的 PHP 脚本被解析出来，浏览器端的最终用户甚至不知道使用的是哪个数据库或哪个用户/密码来生成此页面。

如果您有许多页面使用相同的 MySQL 数据库并通过各种查询显示数据元素，您应该使用 `include()` 函数来简化代码管理任务。例如，列表 15-12 显示了 `simple_query.php` 脚本的修改版本，其中包含了 `include()` 函数。

**列表 15-12: simple_query2.php**

```php
<?php include('/usr/local/apache/secrets/mysql/header.inc'); ?>
<html>
<head><title>Simple Query Script</title></head>
<body>
<table border=1>
<tr><th>Name</th> <th>Password</th></tr>
<?php
    $sth = mysql_query("SELECT * from $table", $dbh);
    while ($myRow = mysql_fetch_row($sth)) {
        printf("<tr><td>%s</td><td>%s</td></tr>", $myRow[0],
               $myRow[1]);
    }
?>
</table>
</body>
</html>
```

通过 Web 访问上述脚本时，生成的页面与 `simple_query.php` 生成的页面相同。但是，这里脚本使用了一个包含数据库连接脚本的头部文件，如下所示：

```php
<?php
    $host = 'localhost';
    $user = 'httpd';
    $passwd = 'nosecret';
    $database_name = 'www';
    $table = 'users';
    $dbh = mysql_connect($host, $user, $passwd);
    mysql_select_db($database_name, $dbh);
?>
```

通过将此脚本从使用它的每个页面中移除，您可以非常轻松地更改主机名、用户名、密码、数据库名和表名。如果您有 20 个页面使用相同的数据库和表，您现在只需在 `header.inc` 文件中更新一次密码即可完成！

## 保护 PHP include 文件

如果您使用 include 文件（如上一节所示）来存储用户名、密码以及其他不应被用户查看的信息（例如数据库主机名、数据库名和表名），请确保将 include 文件保存在 Web 浏览器无法浏览的安全目录中。最好的位置是 Web 站点文档树之外。如果文档根目录是 `/www/mysite/htdocs`，则创建一个名为 `/www/mysite/secret/mysql` 的目录，并将 include 文件存放在那里。

如果您必须在文档根目录内创建 include 文件，请使用以下 `httpd.conf` 配置来禁止 Web 浏览：

```apache
<Directory /path/to/include_files>
<Limit>
Order Deny,Allow
Deny from all
</Limit>
</Directory>
```

别忘了将 `/path/to/include_files` 替换为 include 文件实际目录的路径。如果您将整个 Web 站点的 include 文件分散存放，您仍可以使用 `httpd.conf` 中的以下配置段来禁用对它们的 Web 访问：

```apache
<Files ~ "*.inc*">
Order allow,deny
Deny from all
</Files>
```

只有当您始终确保所有 PHP include 文件都以 `.inc` 扩展名命名时，此方法才有效。

# 使用 PHP 和 MySQL 对用户进行身份验证

您可以使用 PHP 脚本通过 MySQL 数据库对用户进行身份验证。列表 15-13 显示了一个使用 MySQL 数据库对用户进行身份验证的简单脚本。

**列表 15-13: auth.php**

```php
<?php
ob_start();
include('/usr/local/apache/htdocs/mysql/header.inc');
function show_dialog($realm = "Restricted Section") {
    header("WWW-Authenticate: Basic realm=$realm");
    header('HTTP/1.0 401 Unauthorized');
    echo 'Authorization Required.';
    exit;
}

if ((!isset($PHP_AUTH_USER)) || (!isset($PHP_AUTH_PW))) {
    show_dialog();
} else if ((!isset($PHP_AUTH_USER)) && (!isset($PHP_AUTH_PW))) {
    $sth = mysql_query("SELECT 1 from $table WHERE
                        username = '$PHP_AUTH_USER'
        and
        passwd = '$PHP_AUTH_PW'",
        $dbh);

    $success = mysql_fetch_row($sth);
    if ($success[0] == '1') {
        show_dialog();
    } else {
        echo "<p>You're authorized!</p>";
        # Do something here
    }
}
ob_end_flush();
?>
```

当请求此脚本时，它使用 `isset()` 函数检查名为 `$PHP_AUTH_USER` 和 `$PHP_AUTH_PW` 的两个变量是否已设置。如果用户响应基本身份验证质询输入了用户名和密码，PHP 就会设置这两个变量。

由于首次使用的用户尚未看到身份验证质询对话框，因此这两个变量为空，并调用了 `show_dialog()` 函数。此函数仅打印 *基本 HTTP* 身份验证头，这迫使 Web 浏览器显示一个对话框，要求用户输入用户名和密码。

当用户输入用户名和密码对时，该对通过身份验证响应头发送到 Apache 服务器，**PHP** 会看到它。**PHP** 然后相应地设置 `$PHP_AUTH_USER` 和 `$PHP_AUTH_PW` 变量。在身份验证响应请求中再次自动调用脚本后，该脚本使用 *MySQL* 数据库验证用户名/密码对是否存在。如果用户凭据（用户名/密码对）有效，脚本显示消息“You’re authorized”（您已获授权）并终止。另一方面，如果凭据无效，则会重新发出身份验证质询。

请注意，`include('/usr/local/apache/htdocs/mysql/header.inc')` 调用隐藏了所有数据库连接代码。`header.inc` 文件显示如下：

```php
<?php
    $host = 'localhost';
    $user = 'httpd';
    $passwd = 'nosecret';
    $database_name = 'www';
    $table = 'users';
    $dbh = mysql_connect($host, $user, $passwd);
    mysql_select_db($database_name, $dbh);
?>
```

这里的 *MySQL* 数据库名为 `www`，位于 `localhost` 上，可以使用密码 `nosecret` 由名为 `httpd` 的用户访问。`www` 数据库有一个名为 `users` 的表。您可以根据需要更改这些参数，以连接到本地主机或远程 *MySQL* 数据库服务器上的相应数据库。此 include 文件打开到指定主机上的命名数据库的连接，并返回一个名为 `$dbh` 的连接句柄，该句柄可用于 `auth.php`。

在 `auth.php` 脚本中，请注意以下行：

```php
    $sth = mysql_query("SELECT 1 from $table
        WHERE username = '$PHP_AUTH_USER' and
               passwd  = '$PHP_AUTH_PW'",
        $dbh);
```

此行执行一个 SQL 查询，如果用户提供的凭据（由 **PHP** 自动存储在 `$PHP_AUTH_USER` 和 `$PHP_AUTH_PW` 中）分别匹配 `users` 表中的 `username` 和 `passwd` 字段，则返回 1。





## 注意

如果你的用户表对 `username` 或 `passwd` 使用了不同的字段名，请务必修改查询语句以反映这些名称。

`$success = mysql_fetch_row($sth)` 语句返回一个名为 `$success` 的数组，如果查询成功，该数组的第一个元素 `$success[0]` 的值应为 `1`。否则，该元素将未定义。

通过使用第一个元素 `$success[0]`，决定是否使用 `show_challenge()` 来显示（或不显示）身份验证质询。

用户通过身份验证后，这个简单的 `auth.php` 脚本除了打印一条消息表明用户已成功通过身份验证外，不做其他任何事情。当然，你可以让脚本执行更多操作。例如，你可以使用 `Header("Location:/path/to/subdirectory");` 将用户重定向到受保护的子目录。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_484_0.png)

# 第 16 章
## 将 Perl 与 Apache 结合使用

Apache/Perl 集成项目的主要目标之一是将 Perl 编程语言的全部功能引入 Apache 服务器。这导致了 mod_perl 的开发，你可以将 Apache 和 Perl 一起编译并链接，以提供面向对象的 Perl 接口来访问服务器的 C 语言 API。这使 Perl 程序员能够用 Perl 编写 Apache 模块。Apache-Perl 模块可以在请求的处理、头部解析、URI 转换、身份验证、授权、访问、类型检查、修复、日志记录和清理阶段介入。

mod_perl 模块与 Apache 广泛结合使用以创建动态内容。mod_perl 是将 Perl 与 Apache 结合使用的非常高效的方式；你不再需要运行基于 Perl 的 CGI 脚本，这些脚本速度慢、资源消耗大，且通常不适合每秒接收大量并发请求的网站。本章讨论如何编译、安装和配置用于 mod_perl 的 Apache，如何使用 mod_perl 运行旧的 CGI 脚本，以及如何开发 mod_perl 模块以充分利用 Apache API。

# 本章内容

- 编译和安装 mod_perl
- 通过 mod_perl 运行 CGI 脚本
- 编写 mod_perl 模块
- 预加载模块
- 共享内存
- 使用 mod_perl 编写数据库应用程序

### 编译和安装 mod_perl

以下是如何在你的系统上下载、编译和安装 mod_perl 的方法：

1. 从 `http://perl.apache.org/dist` 站点或官方镜像站点下载最新版本的 mod_perl 源代码到 `/usr/local/src` 目录。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_485_0.png)

请确保在进行编译之前阅读源发行版中的安装说明和 README 文件。随着 mod_perl 和/或新版本的 Apache 更新，下面讨论的步骤可能会发生变化。

2. 以 **root** 身份使用 `tar xvfz mod_perl-version.tar.gz` 命令解压 *mod_perl* 源发行版。本节假设你将 Apache 源发行版解压到了 `/usr/local/src`。

3. 切换到 `/usr/local/src/mod_perl-version` 目录并运行：

```
Perl Makefile.PL APACHE_SRC=../apache-version \
  DO_HTTPD=1 \
  USE_APACHE=1 \
  PERL_MARK_WHERE=1 \
  EVERYTHING=1
```

别忘了将 `../apache-version` 更改为适当的路径名。

4. 运行 `make && make test && make install` 命令，将 *mod_perl* 库编译、测试并安装到 Apache 源发行版中。

5. 切换到 Apache 源发行版目录并运行 `make install`，以支持 *mod_perl* 的方式编译和安装 Apache。

6. 使用 `/usr/local/apache/bin/apachectl start` 命令启动新编译的 Apache 服务器。如果你已经运行了以前版本的 Apache 服务器，请使用 `/usr/local/apache/bin/apachectl stop` 命令停止它，然后运行 `start` 命令以重新启动具有 *mod_perl* 功能的新服务器。如果你在 Unix 系统上，可以运行 `lynx -dump -head http://localhost/` 命令来转储服务器显示的头部。如果 *mod_perl* 安装正确，你将看到头部信息中的 `mod_perl/version` 信息。

### 使用 *mod_perl* 运行 CGI 脚本

由于 CGI 脚本速度慢且在重负载下占用更多资源，在理想情况下，当 *mod_perl* 在你的系统上工作时，你不会运行 CGI 脚本。然而，现实是系统管理员很忙，移植已经正常运行的东西通常会被忽略，因为其他地方有更重要、更严重的工作等待处理。幸运的是，*mod_perl* 允许你使用名为 `Apache::Registry.pm` 的默认 *mod_perl* 模块来运行你的 CGI 脚本。因此，你可以立即在 *mod_perl* 下运行你的 CGI 脚本。方法如下。

1. 在 `httpd.conf` 文件中，通过添加以下行创建一个名为 `/apps/` 的别名，指向你的 CGI 脚本目录：

```
Alias /apps/ "/www/mysite/cgi-bin"
```

请确保将 `/www/mysite/cgi-bin` 更改为你系统上适当的 CGI 脚本目录。

2. 通过在 `httpd.conf` 中添加以下行，告诉 Apache 在启动时加载 `Apache::Registry` 模块：

```
PerlModule Apache::Registry
```

3. 通过在 `httpd.conf` 中添加以下配置段，告诉 Apache 对 `/apps/` 目录下的所有脚本通过 `Apache::Registry` 运行：

```apache
<Location /apps>
    SetHandler perl-script
    PerlHandler Apache::Registry
    Options ExecCGI
</Location>
```

4. 使用 `/usr/local/apache/bin/apachectl` restart 命令重启 Apache 服务器。

5. 使用 `http://your_server_name/apps/script_name.` 通过 Web 浏览器访问 CGI 脚本。如果你设置了 `ScriptAlias` 指令将 `/cgi-bin/` 指向 `/www/mysite/cgi-bin`（或你系统上称为 CGI 脚本目录的任何名称），那么你可以使用 `http://your_server_name/cgi-bin/script_name.` 将 CGI 脚本作为“CGI”脚本访问，或者你可以使用 `http://your_server_name/apps/script_name.` 通过 `mod_perl` 访问相同的脚本。后者的优势是不会为每个请求生成一个新的 CGI 进程，从而使其运行更快。注意，`mod_perl` 环境变量可以区分脚本是如何运行的（CGI 或 `mod_perl`）。例如，考虑以下代码段：

```perl
if ($ENV{MOD_PERL} ne '') {
    # 作为原生 mod_perl
    # 模块或 Apache::Registry 运行脚本，
    # 以 mod_perl 脚本身份运行
} else {
    # 通过 mod_cgi 作为
    # 独立进程运行的 CGI 脚本
}
```

上面的条件语句检测脚本是如何运行的。`apps` 目录中的脚本将通过 `Apache::Registry` 模块运行。这意味着你可以通过使用 `--disable-module=cgi` 选项重新编译 Apache，从你的系统中完全移除 `mod_cgi` 模块。

### 不要重造轮子

在你开始为 Web 服务器编写一个很酷的 `mod_perl` 模块之前，请先考虑在 CPAN 上查找现有的可能解决你问题的模块。截至写作本文时，CPAN 上大约有 500 个特定的 `mod_perl` Perl 模块。你可以按以下方式查看 CPAN 上可用的模块：

1. 运行 `perl -MCPAN -e shell` 命令。
2. 在 `cpan>` 提示符下，输入 `i /Apache/`。你应该会收到所有可用的 Apache 相关模块列表。

### 使用 Apache 的 Perl API 创建 mod_perl 模块

当你在系统上安装 mod_perl 时，你也安装了一个非常强大的 Apache Perl 应用程序接口（API）。通过使用这个 API，你可以开发利用 mod_perl 的“原生”方式的 mod_perl 脚本。虽然你可以使用 mod_perl 运行 CGI 脚本，但它们并非为使用 Perl API 的 mod_perl 设计，因此无法完全利用 mod_perl 的强大功能。以下材料展示了如何开发使用 Apache 的 Perl API 编写的脚本，以充分利用 mod_perl 模块。

原生的 mod_perl 脚本作为一个 Perl 模块编写，具有以下架构：

```perl
package MODULE_NAME;

sub handler {
    # 使用 Apache API 提供的请求
    # 对象做一些有用的事情
}

sub module_method_1 { # 做某件有用的事 }
sub module_method_2 { # 做某件有用的事 }
sub module_method_3 { # 做某件有用的事 }
...
sub module_method_N { # 做某件有用的事 }

1;
```

这里，模块文件以一个包名开始。包名必须与模块文件名匹配。例如，如果你将包（即模块）命名为：

```perl
package MyModule;
```

那么你必须将包含此模块的文件命名为 MyModule.pm。通常，Perl 模块文件保存在由 @INC 数组指向的目录列表中的某个子目录中。你可以运行以下命令来查找 @INC 指向哪些目录：

```perl
perl -le 'print join("\n", @INC)'
```

你可能会看到类似以下的输出：

```
/usr/lib/perl5/5.6.0/i386-linux
/usr/lib/perl5/5.6.0
/usr/lib/perl5/site_perl/5.6.0/i386-linux
/usr/lib/perl5/site_perl/5.6.0
/usr/lib/perl5/site_perl
.
```



如果你使用的 Perl 版本不是 5.6.0，那么路径应反映该版本。当 mod_perl 遇到对某个模块的第一个请求时，它会查看目录以定位该模块。由于将自定义模块与 Perl 和 mod_perl 提供的标准模块混在一起并不是个好主意，因此你应在 `/usr/lib/perl5/site_perl` 中创建一个名为 Development 的新目录，并将自定义模块保存在该目录中。这样，当需要自定义模块时，mod_perl 就能在 `/usr/lib/perl5/site_perl/Development` 目录中找到它们。此外，请确保为此新目录设置文件权限，以便 Apache 用户（通过 httpd.conf 中的 User 指令设置）能够读取该目录及其中的文件。你可以使用以下命令创建新目录并设置文件权限：

```bash
mkdir -p /usr/lib/perl5/site_perl/Development
chown -R Apache_User:Apache_Group /usr/lib/perl5/site_perl/Development
chmod -R 750 /usr/lib/perl5/site_perl/Development
```

别忘了将 Apache_User 和 Apache_Group 更改为在 httpd.conf 中通过 User 和 Group 指令分别设置的相应用户和组名。

创建目录后，你可以创建如图 16-1 所示的简单模块。将此模块保存为 `/usr/lib/perl5/site_perl/Development/SimpleAPI.pm`。

### 图 16-1: Apache 的 Perl API 简单示例

```perl
package Development::SimpleAPI;

use strict;

use Apache::Constants qw(:common);

my $callCounter = 0;

sub handler {
    my $r = shift;

    $r->send_http_header('text/html');

    print <<HTML_DOC;
    <html>
    <head><title>Simple Perl API Example Script</title> </head>
    <body>
    <h1>Simple Perl API Example Script</h1>
    <hr>
    <p>Process ID: $$ </p>
    <p>Request count: $callCounter </p>
    <hr>
  </body>
</html>
HTML_DOC

    $callCounter++;

    return OK;
}

1;
```

模块名称是 `Development::SimpleAPI`。这告知 `mod_perl` 从由 `@INC` 指向的目录下的名为 `Development` 的子目录中加载模块。由于你在 `/usr/lib/perl5/site_perl` 目录中创建了 `Development` 子目录，`mod_perl` 将从此目录加载 `SimpleAPI.pm` 模块。该模块的目的是演示 `mod_perl` 的功能。

该模块的工作方式如下：

- `use strict;` 行告知 Perl 强制检查不安全结构。这对于 `mod_perl` 模块来说非常重要。例如，如果脚本中使用了某个变量但未通过 `my` 语句正确声明它，Perl 会对此提出警告，并强制你在使用前声明该变量。
- `use Apache::Constants qw(:common);` 行只是加载 `Constants.pm` 模块，该模块定义了一组常量，如 `OK`、`REDIRECT` 和 `DONE`，这些常量可以直接在脚本中使用。
- 下一行定义 `$callCounter` 变量并将其设置为零。该变量对整个脚本都是全局的，并且其值对于 Apache 子进程内的所有脚本调用都是可用的。此外，请注意，该变量在模块最初加载后设置为零。
- 接下来，定义了 `handler()` 方法。该方法将 Apache 请求对象（`$r`）作为参数传入，并使用内置的 `send_http_header()` 方法来写入 `Content-Type` 头部。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_490_0.png)

- handler() 方法随后打印一个最小化的 HTML 文档，该文档显示 Apache 子进程的流程 ID（$$）并使用 $callCounter 变量请求计数。之后，$callCounter 变量会递增。该方法以 OK 状态返回，请求处理终止。
- 最后一行 1; 对于 Perl 模块是必需的，模块必须返回一个非零数字才能被视为有效的模块。

以下步骤展示了如何运行 SimpleAPI.pm 模块。

- 首先，将以下配置段添加到 httpd.conf 文件中：

```apache
# Configuration for running mod_perl modules
PerlModule Development::SimpleAPI

<Location /firstone>
SetHandler perl-script
PerlHandler Development::SimpleAPI
</Location>
```

上述配置段的作用如下：

- PerlModule 指令在 Apache 服务器启动时加载 Development::SimpleAPI 模块。
- <Location> 指令为位置 /firstone 设置类型为 perl-script 的处理程序。
- PerlHandler 指令告知 Apache，/firstone 位置的 perl-script（即 mod_perl）处理程序是 Development::SimpleAPI 模块，该模块可以在 @INC 数组指向的目录下的 Development/SimpleAPI.pm 文件中找到。

- 使用 /usr/local/apache/bin/apachectl restart 命令重启 Apache 服务器。
- 使用 http://your_server_name/firstone URL 首次运行 SimpleAPI.pm 模块。

如果你不断刷新页面，请求计数将从 0 开始并增加。此外，Apache 子进程的 PID 很少改变。为了确信你知道 mod_perl 模块是如何工作的，你必须理解以下几点：

- 在服务器启动期间，每个子进程都可以共享访问 SimpleAPI.pm 代码的一个副本。这消除了 CGI 成本（即每次请求时调用 CGI 脚本的成本），因为模块已经加载到内存中，并且可供每个子进程以及每个子进程内的线程（如果有的话）使用。
- 首次访问 http://your_server_name/firstone 时，模块首次运行，$callCounter 变量递增。后续的调用（通过浏览器的刷新按钮）会增加请求计数。然而，计数仅对于处理你请求的子进程增加。另一个子进程将从零开始计数；$callCounter 实际上并不在子进程之间共享。换句话说，虽然模块代码在 Apache 子进程之间共享，但数据并不共享。
- 每次调用 SimpleAPI.pm 模块时，Apache 都会将一个名为 $r 的请求对象传递给 handler() 方法。handler() 方法充当模块的入口点。方法外的代码仅在 handler() 方法直接或间接需要时才会执行。例如，在以下代码中，调用 method_one() 和 method_two()，因为 handler() 需要它们：

```perl
sub handler {

my $r = shift;

method_one();
method_two();


return OK;
}
sub method_one {
# something useful
}
sub method_two {
# something useful
}
```

- handler() 方法必须返回 Apache 状态代码，如 OK、DECLINED、DONE、NOT_FOUND、FORBIDDEN、AUTH_REQUIRED 或 SERVER_ERROR。你可以在随 mod_perl 提供的 Constants.pm 文件中找到完整的 Apache 状态常量列表。使用 locate Constants.pm 命令定位该文件，或使用系统的文件查找工具来定位它。在运行 Perl 5.6.0 的 Linux 系统上，文件路径为 /usr/lib/perl5/site_perl/5.6.0/i386-linux/Apache/Constants.pm。

## 使用 CGI.pm 编写 mod_perl 模块

大多数使用 Perl 和 Apache 的人都知道如何使用 CGI.pm 模块用 Perl 编写 CGI 脚本。幸运的是，CGI.pm 的作者意识到，习惯使用此模块的人可能希望在非 CGI 环境（如 mod_perl）中继续使用它，因此该模块的作者确保该模块在 mod_perl 下非常易用。例如，图 16-2 显示了 SimpleAPI.pm 模块的 CGI.pm 版本，现在名为 SimpleAPIUsingCGI.pm。

### 图 16-2: 使用 CGI.pm 模块在 mod_perl 模块中的简单示例

```perl
package Development::SimpleAPIUsingCGI;

use strict;

use Apache::Constants qw(:common);
use CGI ( -compile: all );

my $callCounter = 0;

sub handler {

    my $query = new CGI;

    print $query->header;
    print $query->start_html('Simple Perl API Example Using CGI.pm').
        $query->h1('Simple Perl API Example Using CGI.pm
        Module').
        $query->hr.
        $query->p("Process ID: $$"),
        $query->p("Request count: $callCounter"),
        $query->hr.
        $query->end_html;

    $callCounter++;

    return OK;

}

1;
```

资深的 CGI.pm 开发者会注意到，我在告知 Perl 我想使用 CGI.pm 模块时使用了 -compile: all 选项。这里，Perl 被告知在服务器启动期间模块最初加载时编译一次所有 CGI.pm 代码。这确保了所有 CGI.pm 功能都可以直接用于 SimpleAPIUsingCGI.pm 模块。在请求循环期间，不再需要编译任何特定于 CGI.pm 的代码。当然，如果你不使用 CGI.pm 的很多功能，你可以使用




## 预加载 Perl 模块以节省内存

使用 `CGI qw(-compile :standard)` 或 `CGI qw(-compile :standard :html3)` 等方式，以减小编程接口（CGI.pm）本身占用的内存。请记住，在内存中保留大量未使用的代码会浪费系统资源。

还要注意，CGI 对象 `$query` 是在 `handler()` 方法中创建的。这是必要的，因为如果你在该模块的全局部分（例如 `$callCounter` 所在的区域）而不是在 `handler()` 方法内部创建 CGI 对象，该对象只会在第一次请求时创建一次，并且只包含该请求的信息。例如，如果你将 `my $query = new CGI;` 这一行移出 `handler()` 方法，并放置在 `my $callCounter = 0;` 行之后，脚本会将初始请求后的每个后续请求都视为同一个请求。因此，如果你需要使用 `$query->param()` 方法访问查询字符串信息，你只能获取到第一次请求的数据，因为 `$query` 对象并没有为每个请求创建。这就是为什么在 Listing 16-2 所示的 `handler()` 方法中创建针对特定请求的 `$query` 对象非常重要。

`SimpleAPIUsingCGI.pm` 模块提供了与 `SimpleAPI.pm` 相同的功能，在将以下行添加到 `httpd.conf` 并重启服务器后，可以通过 `http://your_server_name/cgim_example` URL 运行该模块：

```
# Configuration for running mod_perl modules
PerlModule Development::SimpleAPIUsingCGI

<Location /cgim_example>
  SetHandler perl-script
  PerlHandler Development::SimpleAPIUsingCGI
</Location>
```

如果你大量使用 CGI 或 DBI 等 CPAN 模块，或者为你的 Apache 服务器开发了许多自定义模块，你可能希望在服务器启动时使用 `PerlModule` 指令预加载它们。这样做可以节省此类模块首次请求时的时间，并增加在 Apache 子进程之间共享代码页（内存）的可能性。例如，如果你在一个或多个 `mod_perl` 模块中使用了标准的 CGI、DBI 和 `Digest::MD5` 模块，你可以通过在 `httpd.conf` 中放置以下指令来简单地预加载这些模块：

```
PerlModule CGI
PerlModule DBI
PerlModule Digest::MD5
```

另一种方法是使用 `PerlRequire` 指令。该指令可以设置为一个外部 Perl 脚本，该脚本加载你想预加载并可能在 Apache 子进程之间共享的所有模块。例如：

```
PerlRequire /usr/local/apache/apps/startup.pl
```

这告诉 Apache 在启动时加载 `/usr/local/apache/apps/startup.pl` 脚本。该脚本会被加载到内存中，进而加载必要的模块。例如，该脚本可以如下所示：

```perl
#!/usr/bin/perl

use CGI ();
use DBI ();
use Digest::MD5 ();
1;
```

每个 `use module_name ()` 行加载特定的模块。空括号确保不会从这些模块中默认导入符号，从而节省一些内存。

> **注意**
>
> 如果你使用 `CGI.pm` 模块的所有功能，可以在 `startup.pl` 脚本中添加 `CGI->compile('all')` 来编译它们，这可以节省请求处理时的时间。

此外，确保 `startup.pl` 脚本对 Apache 用户（在 `httpd.conf` 文件中通过 `User` 指令设置）是可访问且可执行的。

## 跟踪内存中的 mod_perl 模块

能够跟踪你的 Web 服务器正在使用哪些 `mod_perl` 模块对系统管理有很大帮助。通过使用随 `mod_perl` 提供的 `Apache::Status` 模块，你可以跟踪已加载的模块并获取关于它们的许多信息。为此，请遵循以下步骤：

1. 以 root 身份，必须使用以下命令从 CPAN 镜像站点安装 `perl::Syndump` 模块：
   ```
   perl -MCPAN -e 'install perl::Syndump'
   ```
2. 在任何其他 `PerlModule` 指令之前，将以下配置段添加到 `httpd.conf` 中。
   ```
   PerlModule Apache::Status

   <Location /perl-status>
     SetHandler perl-script
     PerlHandler Apache::Status
   </Location>
   ```
   此代码确保在加载其他任何模块之前加载 `Apache::Status` 模块。如果你使用 `PerlRequire` 指令通过外部启动脚本加载模块，则不需要 `PerlModule Apache::Status` 行。相反，应在启动脚本中先加载 `Apache::ASP` 模块（注：原文此处可能是指先加载 `Apache::Status`，根据上下文逻辑应为 Status），在任何其他模块之前加载 `Apache::Status` 模块。
3. 重启 Apache 服务器，并使用 `http://your_server_name/perl-status` 访问已加载的 `mod_perl` 模块信息。该页面显示一组选项（链接），如下所示：

   - Perl 配置
   - 已加载模块
   - 继承树
   - 启用的 `mod_perl` 钩子
   - 环境
   - Perl 请求文件
   - 信号处理程序
   - 符号表转储
   - ISA 树
   - 已编译注册脚本

4. 点击 `Loaded Modules` 链接以查看所有已加载的 `mod_perl` 模块。其他链接也提供关于 `mod_perl` 特定内容的有价值状态信息。

## 使用 Apache::ASP 模块实现 ASP

活动服务器页面（ASP）是 Windows 世界中常见的脚本平台。然而，它不再是一个仅限 Windows 的脚本平台。通过使用 `mod_perl` 和 `Apache::ASP` CPAN 模块，你可以创建嵌入基于 Perl 的 ASP 脚本的 ASP 页面。方法如下：

1. 作为 `root`，运行以下命令：
   ```
   perl -MCPAN -e 'install Apache::ASP'
   ```
   该 CPAN 模块从本地 CPAN 镜像站点安装 `Apache::ASP` 模块。如果由于某些原因失败，请调查原因并解决问题。通常安装是成功的，除非缺少先决模块。在这种情况下，以相同方式安装缺失的先决模块，然后安装 `Apache::ASP`。

2. 安装 `Apache::ASP` 模块后，在文档根目录中创建一个名为 `asp` 的子目录。假设你的 `DocumentRoot` 指令设置为 `/www/mysite/htdocs`，并且你创建了 `/www/mysite/htdocs/asp` 目录。

3. 创建一个名为 `test.asp` 的测试脚本，如下所示，并将其存储在 `/www/mysite/htdocs/asp` 目录中。
   ```html
   <html>
   <head><title>ASP Example</title></head>
   <body>

   <%          
   $Application->Lock();
   $Application->{Count}++;
   $Application->Unlock();
   %>
   <h1> ASP Page </h1>
   <hr>
   <p>
   This page has been called <%- $Application->{Count} %> times.
   </p>
   </body>
   </html>
   ```
   这个简单的 `test.asp` ASP 页面只是每次调用该页面时，将 ASP Application 对象增加 1。

4. 将以下行添加到 `httpd.conf` 文件：
   ```
   Alias /asp/ "/www/mysite/htdocs/asp"

   <Location /asp/>
     SetHandler perl-script
     PerlHandler Apache::ASP
     PerlSetVar Global /tmp
   </Location>
   ```
   以下是前面代码中发生的情况：
   - `/asp/` 别名指向 `/www/mysite/htdocs/asp` 目录。请确保更改此设置，使其指向你系统中的相应目录。
   - `<Location>` 容器告诉 Apache 使用 `Apache::ASP` 模块来处理该目录中的所有文件；它还设置 `Global` 变量为 `/tmp` 目录。
   - `Apache::ASP` 模块创建一个名为 `/tmp/.state` 的目录，并在其中存储状态信息，以便即使你关闭并重启服务器，状态信息也不会丢失。

5. 更改 `asp` 目录及其内容的文件权限，以允许 Apache 用户（即允许你在 `httpd.conf` 中设置的 `User` 指令所指定的用户）访问文件。例如，使用 `chown -R httpd:httpd /www/mysite/htdocs/asp` 和 `chmod -R 750 /www/mysite/htdocs/asp` 命令，以确保 Apache 用户（httpd）和 Apache 组（httpd）可以访问目录及其中存储的文件。

6. 使用 `/usr/local/apache/bin/apachectl` restart 命令重启 Apache 服务器，并使用 `http://your_server_name/asp/test.asp` 访问 `test.asp` 页面。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_497_0.png)

要了解如何在 Perl 中编写 ASP 脚本，请访问 www.apache-asp.org 上的 ASP 网站。




# 17 使用 Tomcat 运行 Java Servlets 和 JSP 页面

在过去几年里，Java 已成为企业级 Web 开发需求的主要 Web 应用程序平台。许多大公司拒绝考虑在 Web 开发中使用除 Java 以外的任何平台。幸运的是，Apache 对 Java 的处理非常出色。通过使用 Apache 适配器（模块），它可以与 Tomcat 交互，Tomcat 是 Java servlet 2.2 和 JSP 1.1 规范的官方参考实现。

*Servlet* 是一个在 Web 服务器系统的 Java 虚拟机（JVM）中运行的 Java 程序。当收到对 servlet 的请求时，会从已加载的 servlet 中创建一个新的线程。因此，与 CGI 脚本相比，servlet 的启动要求要小得多。就像 CGI 程序一样，servlet 可以与来自 Web 浏览器的 HTTP 请求、诸如 Oracle、Postgres 和 MySQL 的关系数据库、或其他外部应用程序进行交互，然后以 HTTP 响应形式写出结果。正如 CGI 程序一样，servlet 可以访问用户提供的数据，如 cookie、浏览器信息、主机信息等 HTTP 头。

Tomcat 是一个开源的 Java 运行环境（称为 Java servlet 的*容器*），它在处理 servlet 请求方面表现出色，但你可以在 Tomcat 和 Apache 之间建立一种折中方案。你可以使用一个名为 mod_jk（以前称为 mod_jserv）的 Apache 模块来与 Tomcat 交互，使 Tomcat 负责处理 servlet 请求，而 Apache 处理其他所有事务。

# 本章内容

- 安装 JDK
- 安装 Tomcat
- 为 Apache 安装 mod_jk 模块
- 为 Apache 配置 Tomcat
- 为 Apache 配置 servlets
- 配置你自己的 servlets 或 JSP 页面
- 配置 Tomcat 以使用 Java 安全管理器
- 通过 Tomcat 运行 Java servlets
- 禁用 Tomcat 的 HTTP 服务

Tomcat 还实现了 Java 服务器页面（JSP）支持，允许你在带有 `.jsp` 扩展名的 HTML 页面中放置 Java 代码。带有此类扩展名的页面由服务器解析，其方式与解析 PHP 或 ASP 页面非常相似。这使得 JSP 与 PHP 或 Active Server Pages（ASP）非常相似——并额外拥有 Java 的可移植性和 Java 应用程序编程接口（API）的健壮性。实际上，JSP 具备 Java servlets 的所有功能，但对于小的编程任务来说，编写 Java 代码更为容易。当 JSP 脚本首次被引用时，Tomcat 实际上会自动将其转换为 servlets，并在 servlet 容器中编译和实例化它们。

本章讨论了如何让 Tomcat 和 `mod_jk` 与 Apache 协同工作，以便你可以使用 servlets 和 JSP。

> 注意：如果你不熟悉 Java servlets 或 JSP，建议在继续本章之前先阅读相关书籍。关于 servlet 或 JSP 的详细讨论超出了本书的范围。

## 为什么使用 Servlets？

与 CGI 脚本，甚至 `mod_perl` 或 FastCGI 应用程序相比，运行 servlets 的优势在于：

- Servlets 真正是平台无关的，因此具有极高的可移植性。所有现代服务器平台都支持 Java。因此，在混合网络中部署 servlets 比任何其他 Web 应用程序平台都要容易得多。

- 由于启动足迹更小，比 CGI 程序具有更少的开销。无需生成新进程来服务请求。只需创建一个新线程来服务新请求，这比启动新进程的资源成本低得多。

- 通过 Java 数据库连接（JDBC）进行的数据库连接优于通过 Perl DBI 进行的连接，后者在高负载环境中存在严重的性能问题。CGI 脚本每次启动时都会连接数据库；`mod_perl` 脚本可以缓存数据库连接，但没有管理连接的好方法。运行 50 个子进程的 Apache 服务器可能会打开 50 个数据库连接。由于高性能网站拥有许多 Web 服务器，单是这种数据库连接要求对于目前大多数可用的关系型数据库管理系统（RDBMS）来说都是难以管理的。最好的方法是连接池，这在 `mod_perl` 环境中可以通过大量自定义代码实现，但在 servlet 环境中则相当简单。

- Java servlets 在 Java“沙箱”（JVM）中运行，使其成为比其它 Web 应用程序平台更安全的选择——不再需要担心缓冲区溢出。

## 安装 Tomcat

要在你的服务器上安装 Tomcat，你需要有一个 Java 运行环境（JRE），如果你计划开发 servlets，那么你还需要 Java 开发工具包（JDK）。此外，要将 Tomcat 与 Apache 一起使用，你需要 mod_jk 模块。在本节中，我将讨论如何安装这些组件以创建 Tomcat 服务器环境。

### 为 Tomcat 安装最新版的 JDK

在安装 Tomcat 之前，你需要一个合适的 Java 运行环境（JRE）。如果你要编写和编译自己的 Java servlets，则需要完整的软件开发工具包（SDK）。Java 开发工具包（JDK）可免费从 Sun Microsystems（http://java.sun.com/）获得，它包含 JRE 和开发包。你可以通过以下步骤为 Linux 系统安装 JDK：

1. 从官方 Java 网站下载最新版本的 JDK（即 SDK）。截至本文撰写时，最新版本是 1.3，它作为一个自解压 shell 脚本提供，该脚本会创建一个二进制 RPM 包。你可以在一个目录中下载 `j2sdk-1_3_0_02-linux-rpm.bin`（如果有更新版本则下载更新版本）。

2. 以 root 身份运行 `sh j2sdk-version-linux-rpm.bin`。例如，对于 1.3 版本，你可以运行：`sh j2sdk-1_3_0_02-linux-rpm.bin`。当此脚本运行时，它会显示许可证，你应该选择同意。该脚本解包并创建一个名为 `j2sdk-version-linux-rpm` 的 RPM 包（对于 JDK 1.3，它是 `j2sdk-1_3_0_02-linux-rpm`）。

3. 运行 `rpm -ihv j2sdk-version-linux.rpm` 来安装 JDK。例如，要安装 JDK 1.3，请运行 `rpm -ihv j2sdk-1_3_0_02-linux.rpm` 命令。

4. JDK 安装在 `/usr/java/jdkversion` 目录中。例如，1.3 版 JDK 安装在 `/usr/java/jdk1.3_0_02` 目录中。该目录是 `JAVA_HOME` 目录。你应该设置一个名为 `$JAVA_HOME` 的环境变量指向此目录。如果你使用 bash shell，可以在 `~/.bashrc` 文件中按如下方式设置：`export JAVA_HOME=/usr/java/jdkversion`。例如：`export JAVA_HOME=/usr/java/jdk1.3_0_02`。在 shell 提示符中输入 `echo $JAVA_HOME` 以确定是否已设置此环境变量。如果你刚刚将其添加到 `.bashrc` 文件中，则必须运行 `source ~/.bashrc` 来导出变量。

### 安装 Tomcat 和 mod_jk 模块

在你从官方 Java 网站安装了最新版本的 JDK（如上一节所述）之后，你就可以按如下步骤安装 Tomcat 和 mod_jk 模块了：

从位于 http://jakarta.apache.org 的官方 Tomcat 网站下载最新的 Tomcat 二进制包。截至本文撰写时，Tomcat 的最新版本是 3.2，这本书上市时会变成 4.0。因此，请确保更改下文说明中提到的版本号。

对于 Linux，最新的二进制 RPM 包可以从 `http://jakarta.apache.org/builds/jakarta-tomcat/release/v3.2.1/rpms` 目录下载。你应为 Linux 下载以下包：

- `tomcat-version.noarch.rpm`（当前版本：`tomcat-3.2.1-1.noarch.rpm`）。这是 Tomcat 的二进制发行版。
- `tomcat-mod-version.i386.rpm`（当前版本：`tomcat-mod-3.2.1-1.i386.rpm`）。这包含 `mod_jk` 和较旧的 `mod_jserv` 模块的 Apache 二进制发行版。这将在 `/usr/lib/apache` 目录中安装 `mod_jk.so` 模块。由于这是一个 Apache 动态共享对象（DSO）模块，你必须使用共享对象支持编译 Apache。你可以快速检查你正在运行的 Apache 二进制文件是否具有 `mod.so` 支持。运行 `/usr/local/apache/bin/httpd -l` 命令以列出当前编译到 Apache 二进制文件中的所有模块。如果没有列出 `mod_so.c`，你需要使用 Apache 源发行版中 configure 脚本中的 `--enable-module=so` 选项重新编译 Apache，然后运行 `make && make install` 命令重新安装带有 DSO 支持的 Apache。
- `tomcat-manual-version.noarch.rpm`（当前版本：`tomcat-manual-3.2.1-1.noarch.rpm`）。这是 Tomcat 文档包。

> 注意：如果你使用不同的 shell，如 `tcsh` 或 `csh`，请使用 `setenv JAVA_HOME /usr/java/jdkversion` 命令代替前面的 `export` 命令。

5. 在 `~/.bashrc` 文件中添加以下行，将 `$JAVA_HOME` 目录添加到你的 `$PATH` 环境变量中。

```bash
export PATH=$PATH:$JAVA_HOME/bin
```

此行必须跟在上一节讨论的 `$JAVA_HOME` 行之后。

6. 通过运行 `java -version` 命令来测试 JDK 安装。你应该看到类似以下输出：

```bash
java version "1.3.0_02"
Java(TM) 2 Runtime Environment, Standard Edition (build 1.3.0_02)
Java HotSpot(TM) Client VM (build 1.3.0_02, mixed mode)
```




将所有上述文件下载到一个新建的临时目录中，并以 root 用户身份从该目录运行 `rpm -ivh tomcat*.rpm` 命令来安装所有软件。

默认情况下，Tomcat 安装在 `/var/tomcat` 目录中。你需要在 `~/.bashrc` 文件中添加以下环境变量：

```bash
export TOMCAT_HOME=/var/tomcat
```

通过运行 `source ~/.bashrc` 命令在当前 shell 中加载该变量。

## 配置 Tomcat

在本节中，我将讨论如何为 Apache 配置 Tomcat，以及如何使用 Java Security Manager 工具管理 Tomcat 的安全性。

### 为 Apache 配置 Tomcat

Tomcat 的主要配置文件是 `/var/tomcat/server.xml`。从扩展名可以看出，它是一个 XML 文件。

Tomcat 可以使用两种类型的连接处理器：Ajp13 和 Ajp12 协议。Ajp13 协议是较新的协议，提供了更好的性能，并且支持安全套接层（SSL）连接。

要在 Tomcat 中激活基于 Ajp13 协议的连接处理器，你应该确保 `server.xml` 文件中的以下连接器配置未被注释掉：

```xml
    <Connector className="org.apache.tomcat.service.PoolTcpConnector" > 
        <Parameter name="handler" 
            value="org.apache.tomcat.service.connector.Ajp13ConnectionHandler"/>
        <Parameter name="port" value="8009"/>
    </Connector>
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_503_0.png)

`server.xml` 文件应该已经包含了一大块用于 8007 端口上 Ajp12 连接的类似代码。即使你计划使用基于 Ajp13 的连接器，也不应删除此连接器。这是关闭 Tomcat 所必需的。

名为 worker 的 Tomcat 实例属性定义在 `/var/tomcat/conf/workers.properties` 文件中。默认文件（不含注释）包含列表 17-1 中显示的属性。

### 列表 17-1：默认的 Tomcat (worker) 属性

```properties
workers.tomcat_home=c:\jakarta-tomcat
workers.java_home=c:\jdk1.2.2
ps=\
worker.list=ajp12, ajp13

    worker.ajp12.port=8007
    worker.ajp12.host=localhost
    worker.ajp12.type=ajp12
    worker.ajp12.lbfactor=1

    worker.ajp13.port=8009
    worker.ajp13.host=localhost
    worker.ajp13.type=ajp13
    worker.ajp13.lbfactor=1

    worker.loadbalancer.type=lb
    worker.loadbalancer.balanced_workers=ajp12, ajp13

    worker.inprocess.type=jni
    worker.inprocess.class_path=$(workers.tomcat_home)\(ps)\lib\classes

    worker.inprocess.class_path=$(workers.tomcat_home)\(ps)\lib\ps\ajp.jar
    worker.inprocess.class_path=$(workers.tomcat_home)\(ps)\lib\ps\parser.jar

    worker.inprocess.class_path=$(workers.tomcat_home)\(ps)\lib\ps\jasper.jar
    worker.inprocess.class_path=$(workers.tomcat_home)\(ps)\lib\ps\servlet.jar
    worker.inprocess.class_path=$(workers.tomcat_home)\(ps)\lib\ps\webserver.jar

    worker.inprocess.class_path=$(workers.java_home)\(ps)\lib\(ps)tools.jar

    worker.inprocess.cmd_line=-config
    worker.inprocess.cmd_line=$(workers.tomcat_home)/conf/jni_server.xml
    worker.inprocess.cmd_line=-home
    worker.inprocess.cmd_line=$(workers.tomcat_home)

    worker.inprocess.jvm_lib=$(workers.java_home)\(ps)\jre\bin\classic\jvm.dll

    worker.inprocess.stdout=$(workers.tomcat_home)\(ps)inprocess.stdout
    worker.inprocess.stderr=$(workers.tomcat_home)\(ps)inprocess.stderr
    worker.inprocess.sysprops=tomcat.home=$(workers.tomcat_home)
```

该默认属性文件定义了一个 ajp12 worker、一个 ajp13 worker、一个 jni worker 和一个 lb worker。这些 worker 类型之间的区别如表 17-1 所示。

| **Worker 类型** | **描述** |
|---|---|
| ajp12 | 此 worker 使用 ajp12 协议将请求转发给使用 ajp12 协议的进程外 Tomcat worker。 |
| ajp13 | 此 worker 使用 ajp13 协议将请求转发给使用 ajp12 协议的进程外 Tomcat worker。由于 ajp13 是比 ajp12 更新的协议，ajp13 类型的 worker 可以实现比 ajp12 类型 worker 更好的性能。此外，ajp13 提供 SSL 支持。 |
| jni | 通过使用 Java Native Interface (JNI)，这种类型的 worker 可以将请求转发给进程内 Tomcat worker。进程内 worker 运行在 Apache 自身内存空间中打开的 JVM 内。 |
| lb | 通过使用简单的轮询负载均衡方案，此 worker 可以转发请求。 |

`workers.properties` 文件有一些对所有类型 worker 都是“全局”的设置。例如：

```properties
workers.tomcat_home=c:\jakarta-tomcat
workers.java_home=c:\jdk1.2.2
ps=\
worker.list=ajp12, ajp13
```

这些设置是全局的。第一个设置 Tomcat 的主目录。这应该设置为环境变量 `$TOMCAT_HOME` 的值。由于 Tomcat 的默认安装在 Linux 系统下创建 `/var/tomcat` 作为目录，你应该将默认值（`c:\jakarta-tomcat`）修改为如下所示：

```properties
workers.tomcat_home=/var/tomcat
```

类似地，`workers.java_home` 设置 JDK 安装目录的顶层路径，在 Linux 下是 `/usr/java/jdkversion`（例如，对于 JDK 1.3，这是 `/usr/java/jdk1.3.0_02`）。因此，应将其设置为：

```properties
workers.java_home=/usr/java/jdk1.3.0_02
```

下一行告诉 Tomcat 使用什么分隔符来分隔目录元素。默认值 `\` 适用于 Windows 系统，因为在 Windows 平台上目录名是用 `\` 分隔的。在 UNIX 系统上，应该是 `/`。因此，将此行设置为如下所示：

```properties
ps=/
```

`worker.list` 告诉 Tomcat 你想定义多少个 worker。默认列表将 `ajp12` 和 `ajp13` 定义为两个 worker。

这些 worker 中的每一个都可以通过 `worker.<worker_name>.properties=value` 行设置自己的属性。例如，在默认文件中，`ajp13` worker 设置了以下属性：

```properties
worker.ajp12.port=8007
worker.ajp12.host=localhost
worker.ajp12.type=ajp12
worker.ajp12.lbfactor=1
```

第一行设置端口号，这是 `ajp12` worker 用于监听请求的。第二行定义此 worker 监听连接的主机名。第三行定义 worker 的类型。我认为将 worker 命名为 `ajp12` 而它的类型也是 `ajp12` 是一个糟糕的选择。只要名称由字母和数字组成，你可以将 worker 命名为任何名称。第四行为负载均衡目的给 worker 赋予一个权重评分。较高的数字表示功能更强大的机器，当多个机器参与负载均衡场景时，负载均衡 worker 会首先选择具有最高 lbfactor 的 worker。

`workers.properties` 文件中的接下来四行定义了 `ajp13` worker 的相同属性。

接下来的两行定义了一个名为 `loadbalancer` 的 worker，其类型为 `lb`，并使用轮询模式平衡 `ajp12` 和 `ajp13` worker。这两行是：

```properties
worker.loadbalancer.type=lb
worker.loadbalancer.balanced_workers=ajp12, ajp13
```

接下来的两行定义了一个类型为 `jni` 的名为 `inprocess` 的 worker。在 Linux 系统上，通过将该行设置为 `/var/tomcat/classes` 来定义此 worker 的 `class_path`：

```properties
worker.inprocess.type=jni
worker.inprocess.class_path=${workers.tomcat_home}${ps}${ps}classes
```

接下来的六行将六个库文件添加到类路径中：

```properties
worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}jaxp.jar
worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}parser.jar
worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}jasper.jar
worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}servlet.jar
worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}webserver.jar
worker.inprocess.class_path=${workers.java_home}${ps}lib${ps}tools.jar
```

inprocess worker 的最终类路径（在 Linux 上）看起来如这里所示：

```text
/var/tomcat/classes:/var/tomcat/lib/jaxp.jar:/var/tomcat/lib/parser.jar:/var/tomcat/lib/jasper.jar:/var/tomcat/lib/servlet.jar:/var/tomcat/lib/webserver.jar:/usr/java/jdk1.3.0_02/lib/tools.jar
```

如下所示的接下来四行为 inprocess worker 定义了一组命令行选项：

```properties
worker.inprocess.cmd_line=-config
worker.inprocess.cmd_line=${workers.tomcat_home}/conf/jni_server.xml
worker.inprocess.cmd_line=-home
worker.inprocess.cmd_line=${workers.tomcat_home}
```

下一行定义了 JVM 库路径：

```properties
worker.inprocess.jvm_lib=$(workers.java_home)$(ps)jre$(ps)bin$(ps)classic$(ps)jvm.dll
```

JVM 库路径（在 Linux 上）是 /usr/java/jdk1.3.0_02/jre/lib/i386/classic/libjvm.so。因此你必须将上述 jvm_lib 行更改为：

```properties
worker.inprocess.jvm_lib=$(workers.java_home)$(ps)jre$(ps)lib$(ps)i386$(ps)classic$(ps)libjvm.so
```

接下来的两行定义了用于写入 inprocess worker 的 STDOUT 和 STDERR 的文件名：

```properties
worker.inprocess.stdout=${workers.tomcat_home}$(ps)inprocess.stdout
worker.inprocess.stderr=${workers.tomcat_home}$(ps)inprocess.stderr
```

在 Linux 系统上，STDOUT 写入 /var/tomcat/inprocess.stdout，STDERR 写入 /var/tomcat/inprocess.stderr。

最后一行定义了 inprocess worker 的一个系统属性。以下行设置的默认属性是在 Linux 上值为 /var/tomcat 的 tomcat.home：

```properties
worker.inprocess.sysprops=tomcat.home=${workers.tomcat_home}
```

## 配置 Tomcat 以使用 Java Security Manager

Java Security Manager 强制实施所有 Java 相关对象的安全限制，包括 applet、servlet、JSP，甚至 Tomcat 本身。通过使用 Java Security Manager，你可以控制每个应用程序可以做或不能做什么。表 17-2 显示了你可以设置的权限类型。




## 表 17-2 Java 安全管理器权限类型

| 权限类型 | 含义 |
| :--- | :--- |
| `java.util.PropertyPermission` | 控制对 JVM 属性（如 `java.home`）的读/写访问权限。 |
| `java.lang.RuntimePermission` | 控制某些系统或运行时功能（如 `exit()` 和 `exec()`）的使用。 |
| `java.io.FilePermission` | 控制文件和目录的权限。 |
| `java.net.SocketPermission` | 控制网络套接字的使用。 |
| `java.net.NetPermission` | 控制多播网络连接的使用。 |
| `java.lang.reflect.ReflectPermission` | 控制使用反射进行类内省的操作。 |
| `java.security.SecurityPermission` | 控制对安全方法的访问。 |
| `java.security.AllPermission` | 允许所有操作，这实际上等同于不使用 Java 安全管理器。 |

Tomcat 的安全策略在 `/var/tomcat/conf/tomcat.policy` 文件中定义。该文件通常使用以下语法来授予权限：

```
grant codebase code_source {
    permission_type_class [name [, action_list]];
};
```

例如，默认的 `/var/tomcat/conf/tomcat.policy` 文件授予以下权限：

```
// Example webapp policy
// By default we grant read access to webapp dir and
// write to workdir
grant codebase "file:${tomcat.home}/webapps/examples" {
    permission java.net.SocketPermission "localhost:1024-",
        "listen";
    permission java.util.PropertyPermission "*", "read";
};
```

`${tomcat.home}/webapps/examples`（即 `/var/tomcat/webapps/examples`）中的文件被授予权限，可以使用网络套接字在本地主机（localhost）上监听 1024 或更高的端口，并且仅允许对所有 JVM 属性进行读访问。

如果你希望名为 `/var/tomcat/webapps/your_app_name` 的应用程序通过 TCP 端口 389 连接到轻量级目录访问协议（LDAP）服务器，你需要授予以下权限：

```
grant codeBase "file:${tomcat.home}/webapps/your_app_name" {
    permission java.net.SocketPermission "localhost:389",
        "connect";
    permission java.util.PropertyPermission "*", "read";
};
```

默认情况下，Tomcat 的 Java 安全管理器是禁用的。你必须按以下方式启用它：

- 在 `/var/tomcat/conf/server.xml` 文件中，你应该找到以下内容：

```
<!-- Uncomment out if you have JDK1.2 and want to use policy

    <ContextInterceptor
        className="org.apache.tomcat.context.PolicyInterceptor" />
    -->
```

此默认设置禁用了安全管理器，因此你必须移除注释，使其变为以下内容：

```
<ContextInterceptor
    className="org.apache.tomcat.context.PolicyInterceptor" />
```

- 使用 `-security` 选项重启 Tomcat。例如，运行 `/usr/bin/tomcat -security` 将在启用 Java 安全管理器的情况下重启 Tomcat。

当 Java 安全管理器拦截到违反安全策略的操作时，JVM 会抛出 `AccessControlException` 或 `SecurityException`。

### 为 Servlet 和 JSP 配置 Apache

启动 Tomcat 时，它会创建一个名为 `/var/tomcat/conf/mod_jk.conf-auto` 的配置文件。为了让 Apache 与 Tomcat 进行交互，你需要让 Apache 加载此文件。为此，请修改 `httpd.conf` 并添加以下行：

```
Include /var/tomcat/conf/mod_jk.conf-auto
```

自动生成的 `mod_jk.conf-auto` 文件存在一个问题。它指示 Apache 从服务器根目录（由 `httpd.conf` 中的 `ServerRoot` 指令指定）下名为 `libexec` 的子目录中加载 `mod_jk.so` 模块。不幸的是，该目录并不存在，而 `mod_jk.so` 安装在 `/usr/lib/apache` 目录中。因此，你有两个选择：

你可以不通过 `Include` 指令指向 `/var/tomcat/conf/mod_jk.conf-auto` 文件，而是将此文件复制为另一个名称（例如 `mod_jk.conf`），并使用：

```
Include /var/tomcat/conf/mod_jk.conf
```

然后，修改 `mod_jk.conf` 文件，将 `LoadModule jk_module libexec/mod_jk.so` 行更改为 `LoadModule jk_module /usr/lib/apache/mod_jk.so`。

或者，你可以简单地在你的 Apache 服务器根目录中创建一个名为 `libexec` 的子目录，并将 `mod_jk.so` 放入其中。在这种情况下，你必须先启动 Tomcat 再启动 Apache，因为 `/var/tomcat/conf/mod_jk.conf-auto` 是每次 Tomcat 启动时生成的。

假设你选择了第一种方法，因为它更易于管理。第一行配置是：

```
LoadModule jk_module /usr/lib/apache/mod_jk.so
```

`LoadModule` 指令加载 `mod_jk.so` DSO 模块，使 Apache 能够与 Tomcat 交互。

```
JkWorkersFile /var/tomcat/conf/workers.properties
```

此行设置 `JkWorkersFile` 指令，使其指向 `/var/tomcat/conf/workers.properties`。该文件为 `mod_jk` 提供连接不同 Tomcat 实例（也称为工作者/workers）所需的信息。请勿更改此指令。

```
JkLogFile /var/tomcat/logs/mod_jk.log
```

此处使用 `JkLogFile` 指令定义日志文件路径。

```
JkLogLevel error
```

上述行设置用于记录日志文件中错误的日志级别。可能的日志级别包括 `debug`、`warn`、`error` 和 `emerg`，但 `warn` 应该是你的默认选择。

```
JkMount /*.jsp ajp12
JkMount /servlet/* ajp12
```

上面显示的两行将 `/*.jsp` 和 `/servlet/*` URL 前缀分配给名为 `ajp12` 的 Tomcat 工作者。这意味着任何具有 `<anything>.jsp`（例如，`/foo.jsp`、`/bar.jsp` 或 `/servlet/<anything>`，例如，`/servlet/foo`、`/servlet/bar`）的 URL 请求都将被分配给 `ajp12` 工作者。建议将这两行更改为使用 `ajp13`（更快），如下所示：

```
JkMount /*.jsp ajp13
JkMount /servlet/* ajp13
```

此处显示的指令是典型的 Apache 指令：

```
Alias /examples "/var/tomcat/webapps/examples"  
<Directory "/var/tomcat/webapps/examples">  
    Options Indexes FollowSymLinks  
</Directory>
```

创建了一个名为 /examples 的别名，它指向一个名为 /var/tomcat/webapps/examples 的物理目录。该目录容器启用了别名目录中的目录列表和符号链接。

下面显示的下两个指令将 /examples/servlet/* 和 /examples/*.jsp 分配给 Tomcat 工作者 ajp12：

```
JkMount /examples/servlet/* ajp12  
JkMount /examples/*.jsp ajp12
```

如果你愿意，可以将它们更改为 ajp13。因为这只是示例，所以并不关键。

下面显示的一组指令禁用了示例树下的 WEB-INF 和 META-INF 目录的访问权限。这两个目录不应可浏览，因此采取此措施是恰当的：

```
<Location "/examples/WEB-INF/">  
    AllowOverride None  
    deny from all  
</Location>  

<Location "/examples/META-INF/">  
    AllowOverride None  
    deny from all  
</Location>
```

下面显示的一组指令创建了与 /examples 完全相同的配置。

```
Alias /admin "/var/tomcat/webapps/admin"  
<Directory "/var/tomcat/webapps/admin">  
    Options Indexes FollowSymLinks  
</Directory>  

JkMount /admin/servlet/* ajp12  
JkMount /admin/*.jsp ajp12  

<Location "/admin/WEB-INF/">  
    AllowOverride None  
    deny from all  
</Location>  

<Location "/admin/META-INF/">
    AllowOverride None
    deny from all
</Location>
```

你可以将 /admin/servlet/* 和 /admin/*.jsp 的工作者更改为 ajp13，以利用这种新的、更快的协议。最后，对 /test 重复相同的配置：

```
Alias /test /var/tomcat/webapps/test
<Directory "/var/tomcat/webapps/test">
  Options Indexes FollowSymLinks
</Directory>

JkMount /test/servlet/* ajp12
JkMount /test/*.jsp ajp12

<Location "/test/WEB-INF/*">
  AllowOverride None
  deny from all
</Location>

<Location "/test/META-INF/*">
  AllowOverride None
  deny from all
</Location>
```

完成修改上述配置并保存 **httpd.conf** 文件后，重启 Apache 服务器。你可以通过使用 http://your_web_server/examples/ 来访问 Servlet 和 JSP 示例。你也可以通过使用 http://your_web_server/admin/ 来访问管理工具。但是，如果你想使用基于 Web 的管理工具查看上下文（即虚拟目录）信息，你必须在 /var/tomcat/conf/tomcat-users.xml 文件中创建一个名为 admin 的用户。此文件如下所示：

```
<tomcat-users>
  <user name="tomcat" password="tomcat" roles="tomcat" />
  <user name="role1" password="tomcat" roles="role1" />
  <user name="both" password="tomcat" roles="tomcat,role1" />
</tomcat-users>
```

在以下示例中，我添加了一个名为 admin 的用户，密码为 mypwd。

```
<tomcat-users>
  <user name="tomcat" password="tomcat" roles="tomcat" />
  <user name="role1" password="tomcat" roles="role1" />
  <user name="both" password="tomcat" roles="tomcat,role1" />
  <user name="admin" password="mypwd" roles="admin" />
</tomcat-users>
```





对于此用户，如果为管理上下文启用 `trusted = true`，如图所示，你就可以通过 Web 界面查看上下文：

```
<Context  path="/admin"
              docBase="webapps/admin"
              crossContext="true"
              debug="0"
              reloadable="true"
              trusted="true" >
</Context>
```

默认的管理上下文配置将 `trusted` 属性设置为 `false`。如果你将其设置为 `true` 以便通过 Web 界面创建、删除或查看上下文，则必须重启 Tomcat 才能使更改生效。还要注意，使用完毕后永远不要保留 `trusted` 属性设置为 `true`。始终将此设置为 trusted 会使你的服务器面临严重的安全风险。例如，当管理上下文被信任（即设置 `trusted="true"`）时，你可以创建通过 `http://your.server.hostname/admin` 暴露整个文件系统的上下文。要利用这一点，攻击者需要一个 Tomcat 系统，其管理上下文设置为 trusted，并且有一个包含管理用户名和密码的明文 XML 文件 `/var/tomcat/conf/tomcat-users.xml`。处理这种情况的最佳方法是完全移除管理上下文，或者至少确保你将其设置为 untrusted（即 `trusted="false"`）。

## 使用 Tomcat

配置完 Tomcat 后，你可以开始使用它。在本节中，我将向你展示如何禁用 Tomcat 的默认 Web 服务（在端口 80 上），该服务旨在提供静态页面，因为 Apache 在处理静态页面方面做得更好。然后，我将向你展示如何启动和停止 Tomcat 服务器，最后，我将讨论一个可用于自动化 Tomcat 启动过程的 shell 脚本。

### 禁用 Tomcat 的默认 HTTP 服务

默认情况下，Tomcat 在端口 8080 上处理 HTTP 请求。然而，在使用 `mod_jk.so` 模块将 Apache 和 Tomcat 集成后，不需要让 Tomcat 在端口 8080 上处理 HTTP 请求。你可以在 `/var/tomcat/conf/server.xml` 文件的以下部分中修复此问题：

```
<!-- Normal HTTP -->
<Connector
  className="org.apache.tomcat.service.PoolTcpConnector">
<Parameter name="handler"
value="org.apache.tomcat.service.http.HttpConnectionHandler"/>
<Parameter name="port"
value="8080"/>
</Connector>
```

> 你必须确保 Apache 没有监听 8007 或 8080 端口。检查 *httpd.conf* 中的 *Listen* 和 *Port* 指令以确保这一点。

你可以通过删除上述配置或将其注释掉来禁用此服务，如下所示：

```
<!-- *** DISABLED Normal HTTP on Port 8080

<Connector
className="org.apache.tomcat.service.PoolTcpConnector">
<Parameter name="handler"
value="org.apache.tomcat.service.http.HttpConnectionHandler"/>
<Parameter name="port"
value="8080"/>
</Connector>
*** DISABLED Normal HTTP Service on Port 8080 -->
```

### 启动和停止 Tomcat

在启动或停止 Tomcat 之前，你必须确保环境变量，如 *$JAVA_HOME* 和 *$TOMCAT_HOME*，已设置，并且 *$PATH* 变量包含 *$JAVA_HOME/bin* 路径。你可以使用 *echo* 命令检查这些变量是否已在你的 shell 中设置。如果你按照上述安装章节进行操作，你应该已在 *~/.bashrc* 文件中设置了这些变量。

如果你已经设置了这些环境变量，只需运行 */usr/bin/tomcat start* 命令或 *tomcatCtl start* 命令即可启动 Tomcat。你可以使用 */usr/bin/tomcat stop* 命令来停止它。你还可以运行 */usr/bin/tomcat run* 命令以在前景中运行它。只有在需要查看控制台上的 Tomcat 错误消息以进行故障排除时，才建议在前景中运行它。

### 使用 shell 包装脚本启动 Tomcat

在 shell 脚本中创建必要的环境并使用名为 */usr/bin/tomcatCtl* 的 shell 包装脚本运行这些命令是非常有用的，如清单 17-2 所示。这节省了大量输入，并有助于避免输入错误。

### 清单 17-2: /usr/bin/tomcatctl

```
#!/bin/sh

# Change the version number below if your
# JDK is not 1.3.0_02
# VERSION=1.3.0_02

export JAVA_HOME=/usr/java/jdk$VERSION
export PATH=${PATH}:${JAVA_HOME}/bin
export TOMCAT_HOME=/var/tomcat

/usr/bin/tomcat $1

# end
```

将此脚本存储在 /usr/bin 中，并通过运行 `chmod 755 /usr/bin/tomcatctl` 命令启用执行权限后，你可以在不担心环境变量的情况下启动或停止 Tomcat。例如，要启动 Tomcat，你可以运行 `tomcatctl start` 命令；要停止，运行 `tomcatctl stop` 命令；要在前景中运行，运行 `tomcatctl run` 命令。

二进制 RPM 包还会安装 `/etc/rc.d/init.d/tomcat` 脚本。该脚本被符号链接到适当的运行级别，以便每次重新启动系统时，Tomcat 都会自动启动和停止。但是，`/etc/rc.d/init.d/tomcat` 中 `JAVA_HOME` 的默认值和 JDK 路径可能并不适合所有人。例如，该脚本中为这两个变量设置的默认值如下所示：

```
export PATH=$PATH:/opt/IBMJava2-13/bin:/opt/IBMJava2-13/jre/bin
export JAVA_HOME=/opt/IBMJava2-13
```

这些似乎是 RPM 开发人员自己的设置。如果你按照我之前的说明从 Sun Microsystems 的 Web 站点下载 JDK，你的 JDK 安装路径将不同。因此，务必修改 `/etc/rc.d/init.d/tomcat` 脚本中的这两个设置。例如，正确的值是：

```
export PATH=$PATH:/usr/java/jdk1.3.0_02/bin:/usr/java/jdk1.3.0_02/jre/bin
export JAVA_HOME=/usr/java/jdk1.3.0_02
```

### 运行 Java Servlet

在本节中，我将讨论如何设置 Tomcat 以运行随附的示例 Servlet，并向你展示如何运行你开发或从 Internet 下载的自己编写的 Servlet 或 JSP 页面。

## 运行 Web 应用程序

> **注意** 永远不要以 root 身份运行 Tomcat。创建一个名为 **tomcat** 的新用户和组，并使用 `chmod -R 755 /var/tomcat` 命令更改 `/var/tomcat` 的文件和目录权限。

### 通过 Tomcat 运行 Java 示例 Servlet

要运行 Java Servlet，你不需要 Apache。你可以使用 Tomcat，它是一个名为 **容器** 的开源 Java 运行时环境，用于 Java Servlet。Tomcat 可以与你的 Web 服务器并行安装，它可以处理静态和 Servlet 请求。然而，当涉及到配置和提供静态请求时，Tomcat 的通用性要低得多。它并不是高度可配置的 Apache Web 服务器的替代品。不过，如果你想使用 Tomcat，本节就是为你准备的。

默认情况下，当 Tomcat 启动时，它从端口 8080 处理 Servlet 请求。启动 Tomcat 后，如果你在 Tomcat 服务器上运行 Web 浏览器，你应该能够使用 `http://localhost:8080` 访问示例 Servlet 和 JSP 页面。或者，你可以使用 `http://your_web_server_hostname:8080` 从另一台机器访问它。当你访问默认的 Tomcat 服务器时，该页面看起来类似于图 17-1。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_516_0.png)

单击 JSP 示例链接，你将看到一个如图 17-2 所示的页面。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_517_0.png)

有许多 JSP 示例页面可以尝试，以测试你的安装。例如，单击日期 JSP 页面的“执行”链接。你应该看到一个类似于图 17-3 所示的输出页面。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_517_1.png)

此 JSP 页面的 JSP 代码存储在 `/var/tomcat/webapps/examples/jsp/dates/date.jsp` 中，如清单 17-3 所示。

### 清单 17-3: date.jsp

```
<html>
<!--
 Copyright (c) 1999 The Apache Software Foundation. All rights
 reserved.
-->
<%@ page session="false"%>

<body bgcolor="white">
<jsp:useBean id="clock" scope="page" class="dates.JspCalendar" type="dates.JspCalendar" />

<font size=4>
<ul>
<li> Day of Month: is  <jsp:getProperty name="clock" property="dayOfMonth"/>
<li> Year: is    <jsp:getProperty name="clock" property="year"/>
<li> Month: is   <jsp:getProperty name="clock" property="month"/>
<li> Time: is    <jsp:getProperty name="clock" property="time"/>
<li> Date: is    <jsp:getProperty name="clock" property="date"/>
<li> Day: is     <jsp:getProperty name="clock" property="day"/>
<li> Day Of Year: is <jsp:getProperty name="clock" property="dayOfYear"/>
<li> Week Of Year: is <jsp:getProperty name="clock" property="weekOfYear"/>
<li> era: is     <jsp:getProperty name="clock" property="era"/>
<li> DST Offset: is  <jsp:getProperty name="clock" property="DSTOffset"/>
<li> Zone Offset: is  <jsp:getProperty name="clock" property="zoneOffset"/>
</ul>
</font>

</body>
</html>
```

你可以看到，JSP 代码使用 `<jsp:getProperty name="name" property="property_name" />` 标签嵌入在 HTML 中。

如果你返回到顶级页面并单击 Servlet 示例链接，你将看到一个如图 17-4 所示的页面。

单击“Hello World” Servlet 的“执行”链接，你应该看到一个如图 17-5 所示的输出页面。

使用 Web 浏览器的后退按钮返回前一页，并单击“Hello World”的“源代码”链接以查看此 Servlet 的简化源代码。源代码如图 17-6 所示。




图 17-4：Servlet 列表示例。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_519_0.png)

图 17-5：`/examples/servlet/HelloWorldExample` 的输出。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_519_1.png)

如你所见，这是一个相当简单的 servlet——它只是打印出一堆 HTML 标签以创建输出。

### 运行你自己的 Servlet 或 JSP

本节教你配置自己的 servlet 以通过 `mod_jk` 运行。假设你的 servlet 名为 `myapp`。以下是让 Apache 和 Tomcat 协同工作所需完成的步骤：

1. 在 `/var/tomcat/conf/server.xml` 中创建以下配置：

```xml
<Context path="/myapp"
    docBase="/var/tomcat/webapps/myapps"
    debug="0"
    reloadable="true" >
  </Context>
```

path 属性指定了 URL 中用于引用名为 myapp 的 servlet 的路径。docBase 属性指定了查找此 servlet 的路径。这可以是绝对路径，也可以是相对于 Tomcat 上下文管理器（默认为 $TOMCAT_HOME/webapps）的路径。debug 属性指定了调试日志消息的级别，而 reloadable 属性指定了当 servlet 发生变化时，Tomcat 是否会自动重新加载它。

2. 使用 `/usr/bin/tomcat stop ; /usr/bin/tomcat start` 命令停止并重启 Tomcat。这将生成一个新的 `/var/tomcat/conf/mod_jk.conf.auto` 文件，其中应包含以下配置段：

```apache
Alias /myapp "/var/tomcat/webapps/myapp"

<Directory "/var/tomcat/webapps/myapp">
    Options Indexes FollowSymLinks
</Directory>

JkMount /myapp/servlet/* ajp12
JkMount /myapp/*.jsp ajp12

<Location "/myapp/WEB-INF/">
    AllowOverride None
    deny from all
</Location>

<Location "/myapp/META-INF/">
    AllowOverride None
    deny from all
</Location>
```

3. 创建 `/var/tomcat/webapps/myapp`、`/var/tomcat/webapps/myapp/WEB-INF`、`/var/tomcat/webapps/myapp/WEB-INF/classes` 和 `/var/tomcat/webapps/myapp/META-INF` 目录。

4. 将 myapp servlet 的 web.xml 配置文件存储在 `/var/tomcat/webapps/myapps/WEB-INF` 目录中。

5. 将 myapps 的 servlet 类复制到 `/var/tomcat/webapps/myapps/WEB-INF/classes` 目录中。

6. 确保 Tomcat 用户（即用于运行 Tomcat 的用户 ID）可以访问新的 `/var/tomcat/webapps/myapps` 目录（包括所有子目录和文件）。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_521_0.png)

**图 17-6：** /examples/servlet/HelloWorldExample 的简化源代码。

就是这样！你应该能够通过 http://your_web_server/myapps 访问该 servlet。

♦ ♦ ♦

# 保护您的网站

确保网站安全是 Web 管理员工作的重要组成部分。在本部分中，我将讨论在 Apache 中可能出现的各种安全问题，以及如何通过使用各种工具、技术和策略或指南来解决这些问题。我还将向您展示如何使用 mod_ssl 或 Apache-SSL 模块将您的 Apache 服务器转变为具备安全套接字层（SSL）功能的 Web 服务器。

# 第四部分

# 本部分简介

- 第 18 章 Web 安全
- 第 19 章 使用 SSL 保护 Apache

# 18

# 章节

# Web 安全

**T**he need for security is often unclear to novice administrators. 许多新手管理员对安全性的需求往往感到模糊不清。许多管理员只有在安全违规发生后才会考虑安全问题——为时已晚！本章提供了关于那些使安全至关重要的隐藏风险的大致了解。

# 理解 Web 安全

当你的 Web 服务器启动并运行，向全世界开放的那一刻，你就为他人进入你的网络打开了一扇窗口。这是你打算做的，对吧？大多数人会使用你网站上可用的信息，但有些人可能会寻找这扇窗户的漏洞，以便获取他们本不应访问的信息。这些人中有些是想制造尴尬局面的破坏者，有些则是信息窃贼。无论哪种情况，如果有人成功找到了那个漏洞，你可能会发现你的网站被添加了淫秽内容，甚至可能丢失机密数据。有时攻击并不直接针对你的网站。入侵者可能会利用你的服务器和其他资源来进入另一个网络，使你面临法律风险。这些场景都不是我们想要的。

为了避免这种风险和尴尬，本章向你展示如何保护你的网站。我假设以下安全要求适用于你的网站：

- 维护你在 Web 上发布的信息的完整性。
- 防止你的 Web 服务器主机被用作进入你组织网络的入侵点（这可能导致信息资源的机密性、完整性或可用性遭到破坏）。
- 防止你的 Web 服务器主机被用作入侵其他网络的准备区域（这可能导致你的组织对损害承担责任）。

# 本章简介

理解 Web 安全

了解安全检查点

选择管理安全策略

识别并最小化 CGI 和 SSI 安全风险

保护你的 Web 内容

大多数 Web 安全事件发生的原因在于，由于软件配置不当，机密信息变得易受攻击。该软件可能是 Web 服务器本身，也可能是由 Web 服务器运行的应用程序（如 CGI 程序、服务器端包含和服务器 API 应用程序）。这可能导致机密信息无意间泄露。随后的攻击可以利用这些机密信息发起。

如果你的 Web 服务器配置严格，并且由 Web 服务器运行的应用程序相当安全，你就完成了吗？不，因为攻击可能通过不同的路径针对 Web 服务器。你的 Web 服务器可能通过完全无关的应用程序、操作系统漏洞或糟糕的网络架构而遭到破坏。

为了安全，你必须审视每一个细节。这可能是一项艰巨的任务；但请记住，不可能拥有一个完全安全的环境。对于所有安全问题，从来没有万无一失的解决方案，因为并非所有问题都是已知的。你的目标是尽可能提高安全性。

## 安全检查点

保护你的 Web 服务器免受破坏者攻击的第一步是理解并识别所涉及的风险。就在不久前，网站只提供静态 HTML 页面，这使得它们较不容易受到安全风险的影响。破坏者侵入这些网站的唯一方法是非法访问并闯入服务器。这通常是通过使用弱密码或欺骗其他守护进程（服务器）软件来实现的。然而，大多数网站不再仅提供静态 HTML 页面；它们提供动态内容，通常经过个性化处理以提供丰富的用户体验。许多网站将应用程序集成在一起，以提供有价值的客户服务或执行电子商务活动。这时，风险开始变得越来越重。是的，Web 应用程序是 Web 安全问题的核心。大多数被破坏者黑入的网站并非因为 Web 服务器软件本身而受损。它们是因为 Web 服务器软件运行的应用程序或脚本中的一个或多个漏洞而被黑入的。

为了改进你的公共网站的安全性，你需要审查几个安全检查点；图 18-1 展示了整体安全检查点图。该图表列出了在考虑将连接互联网的网络视为安全之前必须彻底审查的安全检查点。

有三个主要检查点：

- 你的网络：这是最外层的检查点，需要非常强大。你的网络通过路由器、防火墙系统或网关服务器连接到互联网。因此，你的网络是主要的安全检查点。保护你的网络应该是你主要的安全关切。





你的操作系统：你为 Web 服务器使用的操作系统非常重要。如果你运行 Apache 的操作系统版本（无论是 Linux、Windows 还是 Solaris）已知存在安全风险，那么你的服务器就可能遭受攻击。运行最新的操作系统是必须的。

你的 Web 服务器软件：这是你的第三个安全检查点。确保你运行的 Apache 版本没有已知的安全风险。

我将在以下章节中讨论这些检查点。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_527_0.png)

## 检查点 1：你的网络

需要考虑的第一个检查点是你的网络，以及它如何连接到互联网。真正的问题在于你将 Web 服务器放置在哪里。一般思路是隔离你的内部网络，尽可能避免被窥探。务必考虑在你的互联网到局域网（LAN）路由器中安装防火墙。如果防火墙不是可行的选项，你可以考虑代理服务器方案。代理服务器处理一个网络向另一个网络的请求，而从不直接连接这两个网络。这可能是一个好的解决方案，因为它也提供了出色的日志记录功能。

如你所见，你应该更关注你的内部网络，而非 Web 服务器本身。因为网络引入了互联网可访问的 Web 服务器，它们更有可能通过利用 Web 服务器软件中的安全漏洞，或利用运行在 Web 服务器上的应用程序（如 CGI 程序）中的漏洞而被入侵。通过选择将局域网与 Web 服务器隔离的网络架构，可以降低这种情况发生的可能性。

如果你有一个网络配置，例如图 18-2 所示，你的网络几乎处于无保护状态。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_528_0.png)

图 18-2：具有互联网连接的简单网络。

为了保持简单，讨论假设你只有一个互联网连接。在这个网络模型中，所有互联网流量都可以路由到和你的网络以及从你的网络发出。换句话说，互联网上的任何人都可以访问你网络中的任何主机，反之亦然。这也意味着互联网上的黑客可以找到你网络中众多主机之一的弱点。当然，并非所有这些主机都是启用了供他人使用的服务的服务器；但是，即使你有一台启用了文件共享的 Windows 机器，它也是一个潜在的目标。因为整个网络使用 TCP/IP，Windows 工作站机器上简单的文件共享选项可能导致入侵。这个网络几乎是在邀请那些想入侵的犯罪分子。

如果你有这种配置，请查阅你的路由器文档以确定是否可以启用基于 IP 的限制。我建议在可能的情况下避免这种配置。

> 请参阅本章稍后的“选择安全配置”一节，了解你可以使用的一些网络配置。

## 检查点 2：操作系统

Apache 几乎在所有 Unix 平台上运行，并且已开始运行在 Windows 2000、Windows 95 以及新的 Macintosh 操作系统 Mac OS X 上。但仅仅因为 Apache 几乎在任何平台上都能运行，并不意味着你应该使用任何操作系统来运行 Apache。选择合适的操作系统（OS）可以是系统安全的一个重要因素。众所周知的 Unix 和类 Unix 操作系统包括 Mac OS X、BSDI、FreeBSD、SunOS、Solaris、HP-UX、Digital Unix 和 Linux。互联网服务器管理员偏爱这些操作系统。虽然这些操作系统的质量和可靠性可能有所不同，但它们都是设计用作服务器操作系统的。

如果你不喜欢 Unix，请研究 Windows 2000 服务器平台。Windows 2000 是一个非常有实力的 Unix 竞争对手，未来很可能使 Unix 受到挑战；然而，Windows 2000 在互联网领域是新人。大多数 Unix 和类 Unix 操作系统已经存在足够长的时间，承受了无数的黑客攻击。它们是幸存者——尽管从未做到完全防黑客——但依然屹立不倒。

**提示** 选择操作系统后，你应该禁用在该操作系统运行的 Web 服务器机器上你不打算使用的额外功能。例如，如果你不需要 SMTP/POP 邮件或 FTP 服务，请禁用它们或从系统中完全删除邮件服务器程序。如果你不需要大量的强大系统工具，请删除它们。确保你的 Web 服务器只是一个 Web 服务器，并且只有所需的服务。

**交叉参考** 你可以通过浏览 www.cert.org 来了解你的操作平台中存在的漏洞。CERT（计算机应急响应团队）与互联网社区合作，促进对安全问题的认识和响应。该组织还开展旨在提高计算机系统安全性的研究。

## 检查点 3：Web 服务器软件

显然，你使用 Apache 作为 Web 服务器软件，否则你也不会读这本书。然而，请确保你使用适合你系统的 Apache 2 服务器最新稳定版。自行编译 Apache 二进制文件而不是使用二进制发行版的二进制文件是个好主意。

Apache 是自由软件，因此从可靠来源获取它很重要。切勿从随意的 Web 或 FTP 站点下载 Apache 二进制文件或源代码。首先务必查看官方站点 www.apache.org。Apache 源代码是经过 PGP（Pretty Good Privacy）签名的。还要注意，当前的 Apache 发行版包含一个 PGP 密钥环文件，其中包含大多数活跃 Apache 开发者的 PGP 密钥。

Apache 组的 PGP 签名位于 Apache 顶级发行版中的 `KEYS` 文件中。如果你信任获取发行版的站点，可以将这些密钥添加到你自己的密钥环中。如果你不知道如何在系统上使用 PGP，请通过 `www.pgp.com` 了解它。

每个 Apache 源代码发行版都是经过 PGP 签名的，这些签名存储在具有 `.asc` 扩展名的文件中（例如，`apache_2_0_tar_gz` 的签名存储在 `apache_2_0_tar_gz_asc` 中）。如果你已将 `KEYS` 文件的内容添加到你的密钥环中，可以使用这些文件来验证发行版的有效性。

最新稳定版的 Apache 没有已知的错误；然而，其整合外部第三方模块的能力引发了一种安全问题：你是否信任第三方模块？世界各地的人们编写了许多 Apache 模块。请确保你只使用在官方 Apache 网站或位于 `http://modules.apache.org/` 的 Apache 模块注册表中登记的模块。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_530_0.png)

切勿在生产站点中使用实验性模块。事实上，确定你真正需要哪些模块，然后相应地配置和编译 Apache 是个好主意。这样，你就拥有了一个更小、更快的服务器，并可能具有更好的安全性。

在配置 Apache 时，请高度重视安全配置问题。基本思路是禁用你不使用的任何功能。这样，你就是在采取预防性安全措施，并有可能降低风险。

## 选择安全配置

有许多方法可以在增强整体 Web 安全性的同时配置 Apache。在你选择一种适合你的配置之前，你需要制定一个安全策略，然后选择一种满足你策略要求的配置。说到安全，你有可能高估风险而变得过于偏执，或者低估你的安全需求而让系统过于开放。在以下部分中，我将讨论几种适合不同环境的配置。

### 安全策略考量

行政安全策略确定了对于实现强健网络安全至关重要的实践。如果你还没有一个安全策略，请考虑将以下一些内容添加到行政安全策略中作为一个开始。




## 记录一切
- 我无法再强调得更多了。服务器日志文件记录了服务器响应每个请求时的行为信息。对日志的分析可以提供业务信息（例如，哪些网页最受欢迎）和安全信息。请确保你配置 Apache 同时记录访问日志和错误日志。借助日志文件，你可以追踪谁在访问什么。养成随时浏览日志的习惯——如果你发现任何异常情况，请仔细查看。你的错误日志可能是最需要密切监控的日志。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_531_0.png)

有关日志记录的更多信息，请参阅本章稍后部分的“日志记录与安全”以及我描述使用 Apache 进行日志记录的第 8 章。

## 维护网站（们）的权威副本
- 将网站的权威副本保存在更安全的服务器上。如果 Web 服务器上公开信息的完整性遭到破坏，你需要一个权威副本用于恢复。通常，权威副本保存在可被网站管理员访问（以及可能包括你组织中负责创建和维护 Web 内容的人员）的主机上。它通常保存在组织的内部网络上。

为了确保安全性，使用健壮的加密校验和技术为每个文件生成校验和。将文件的权威副本和校验和保存在物理安全位置的写保护或只读介质上。你可以使用 MD5 加密为你的文件生成加密校验和。

## 通过 Web 主机控制台管理你的站点
- 你应该从 Web 主机的控制台管理你的 Web 站点。这样做消除了 Web 服务器和管理员工作站之间网络流量的需求。然而，在许多情况下这是不可行的（例如，在 Web 服务器无法轻松被管理员访问的组织中）。当你必须进行远程管理时，请务必使用强身份验证方案登录 Web 服务器。如果你使用基于 Web 的管理工具，请确保它不使用基本 HTTP 身份验证。换句话说，你需要确保密码不是以未加密的格式从你的工作站传输到 Web 服务器。此外，你应该配置 Web 服务器系统，使其仅接受来自你内部网络中单个主机的连接。

## 注意公共领域的 CGI 应用程序
- 每当使用公共领域 CGI 时，请确保你或你组织中的某人（或外部顾问）完全理解该代码。切勿从非真实来源获取应用程序的副本。搜索 USENET 新闻组，查看是否有人发现你打算在 Web 服务器上安装的应用程序存在问题。如果可能，将该应用程序安装在暂存服务器上并自行测试。在测试期间持续监控你的日志文件，查找由应用程序产生的错误和警告。如果应用程序使用邮件服务，也要监控邮件日志。

## 比较内容
- 破坏者通常会替换、修改或损坏他们获得访问权限的系统上的文件。为了重新获得系统的非法访问权限，他们经常修改系统程序，使程序看起来运行正常，但为破坏者预留了后门。破坏者还会修改系统日志文件以消除其活动的痕迹。破坏者甚至可能在你的系统上创建新文件。

因此，为了避免这种情况，将文件和目录的属性及内容与权威副本进行比较是一个好主意。如果你已为文件创建了加密校验和，你可以比较当前副本和真实副本的校验和，以确定是否存在任何差异。你应该查看 **Tripwire** 及其网站 **www.tripwire.com** 上的详细信息，了解如何使用校验和来确保内容安全。

## 使用 MD5 验证文件内容的完整性
- **MD5** 程序生成一个唯一的、128 位的加密消息摘要值，该值由文件内容导出。这个值被认为是一个高度可靠的指纹，可用于验证文件内容的完整性。如果文件中哪怕只有一个比特值被修改，该文件的 MD5 校验和也会改变。以导致 MD5 生成与原文件相同结果的方式伪造文件被认为是非常困难的。

为关键系统、应用程序和数据文件生成的一组 MD5 校验和提供了一种紧凑的方式来存储信息，用于对这些文件进行定期完整性检查。如果任何更改无法归因于授权活动，你应该认为你的系统已被入侵，并立即采取行动。如果发现更改是有效的，请重新创建你的权威副本和校验和。

- **RFC 1321** 中提供了 MD5 加密校验和程序的详细信息。源代码和附加信息可在 **www.faqs.org/rfcs/rfc1321.html** 上获取。

## 为 Apache 设置合理的.security 配置
- 合理的（即不那么偏执的）**Apache** 安全配置使用专用的非特权用户和组用于 **Apache**，为 Web 文档和日志文件定义良好的目录结构，以及适当的文件和目录权限，仅允许 Web 服务器读取和/或写入文件和目录。此配置还默认禁用对所有内容的访问，并仅通过明确规则启用对资源（如目录）的访问。此配置的详细信息将在以下各节中讨论。

## 为 Apache 使用专用用户和组
- **Apache** 可以作为独立进程运行，也可以作为 **inetd** 守护进程运行服务。如果你选择将 **Apache** 作为 **inetd** 服务运行，你不必担心 **User** 和 **Group** 指令。然而，如果你将 **Apache** 作为独立服务器运行，请确保你为 **Apache** 创建了专用的用户和组。不要使用 nobody 用户或 nogroup 组，特别是如果你的系统已经定义了这些。很可能系统在其他服务或地方正在使用它们。这可能会导致管理上的麻烦。相反，为 Apache 创建一个新的用户和组，并使用上述指令使用它们。

当你为 Apache 使用专用用户和组时，针对权限管理你的 Web 内容就变得简单了。你所需要做的只是确保只有 Apache 用户拥有 Web 内容的读取权限。如果你需要创建某些 CGI 脚本可能写入数据的目录，你只需要仅为 Apache 用户启用写入权限。

## 使用安全的目录结构
- 在大多数 Apache 安装中，有四个主要目录：
  - 由 ServerRoot 指定的目录，存储服务器配置（conf 子目录）、二进制文件（bin 子目录）和其他特定于服务器的文件。
  - 由 DocumentRoot 指定的目录，存储你的 Web 站点内容，如 HTML 页面、Java 脚本和图片。
  - 由 ScriptAlias 指定的目录，存储你的 CGI 脚本。
  - 由 CustomLog 或 ErrorLog 指定的目录，存储访问日志和错误日志文件。你可以为每个指令指定不同的目录，但长期来看，为所有日志文件保留单个日志目录可能更容易管理。

我建议你使用一种目录结构，其中四个主要目录中的每一个都是独立的，即上述目录中没有任何一个是另一个目录的子目录。ServerRoot 应指向一个只有 root 用户才能访问的目录。DocumentRoot 目录需要能够被维护你 Web 站点的用户以及 Apache 用户或组（通过在 httpd.conf 文件中指定 User 和 Group 指令）访问。由 ScriptAlias 指定的脚本目录应仅能被脚本开发人员和 Apache 用户或组访问。由 CustomLog 或 ErrorLog 指定的目录应仅能被 root 用户访问。甚至 Apache 用户或组也不应有权访问日志目录。下面展示了这种目录结构的示例。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_533_0.png)




## 适当的文件和目录权限

```
├---cgi-bin (ScriptAlias)
└---logs (CustomLog 和 ErrorLog)
```

上述目录结构在许多方面都是安全的。为了理解其原因，首先查看 **httpd.conf** 中针对上述目录结构的以下 Apache 配置。

```
ServerRoot     "/home/httpd"
DocumentRoot     "/www/htdocs"
ScriptAlias     /cgi-bin/ "/www/cgi-bin/"
CustomLog     /www/logs/access.log common
ErrorLog     /www/logs/error.log
```

由于这些主要目录中的每一个都是独立的（即没有一个目录是另一个目录的子目录），因此它们彼此之间是安全的。在一个目录中的权限错误不会影响另一个目录。如果你不认为这是件大事，请数一下你参与用户和 Linux 工作的年限，然后通读所有的墨菲定律。

需要为上述目录结构设置适当的权限。

由 **ServerRoot** 指定的目录应仅对 root 用户可访问，因为除了 root 之外，没有人需要配置或运行 Apache。**DocumentRoot** 应该对管理你网站内容的一个或多个用户以及 Apache 用户（通过使用 **User** 指令指定）或 Apache 组（通过使用 **Group** 指令指定）可访问。例如，如果你想让一个名为 **htmlguru** 的用户在你的网站上发布内容，并且你以 **httpd** 用户身份运行 Apache，你可以通过以下步骤让 Apache 和指定用户都能访问 **DocumentRoot** 目录：

- 1. 创建一个新的名为 webteam 的组：
  `groupadd webteam`
- 2. 将 **htmlguru 用户** 添加到 webteam 组：
  `usermod -G webteam htmlguru`
- 3. 更改 **DocumentRoot** 目录（及其下面所有子目录）的所有者：
  `chown -R httpd.webteam /www/htdocs`

此命令将目录所有者设置为 Apache（即 `httpd` 用户），将组所有者设置为 `webteam`，其中包含 `htmlguru` 用户。换句话说，Apache 和 `htmlguru` 都将拥有访问文档树的权限。

- 4. 更改 `DocumentRoot` 目录（及其下面所有子目录）的权限，如下所示：

```bash
chmod -R 2570 /www/htdocs
```

此命令确保 `DocumentRoot` 下的文件和子目录可被 Apache 用户读取和执行，并且 `webteam` 组可以读取、写入和执行所有内容。它还确保每当在文档树中创建新文件或目录时，`webteam` 组都将拥有访问权限。

这种方法的一个巨大优点是，将新用户添加到 webteam 就像运行以下命令一样简单：

```bash
usermod -G webteam new_username
```

同样，如果你希望将现有用户从 `webteam` 组中移除，只需运行：

```bash
usermod -G username [group1,group2,group3,...]
```

其中 `group1`、`group2`、`group3` 等是该用户所属的组（不包括 `webteam` 组）。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_535_0.png)

> 你可以通过运行 `groups username` 命令来了解用户属于哪些组。

由 `ScriptAlias` 指定的目录应仅对 CGI 开发人员和在 `httpd.conf` 中使用 `User` 指令指定的 Apache 用户可访问。我建议你为开发人员创建一个新的名为 `webdev` 的组。尽管开发组（如 `webdev`）需要对该目录具有读取、写入和执行权限，但 Apache 用户只需要读取和执行权限。不要允许 Apache 用户在此目录中写入文件。例如，假设你的 `httpd.conf` 中有以下 `ScriptAlias`：

```bash
ScriptAlias /cgi-bin/ "/www/cgi-bin/"
```

如果 `httpd` 是你的 Apache 用户，`webdev` 是你的开发组，你应该按如下方式为 `/www/cgi-bin` 设置权限：

```bash
chown -R httpd.webdev /www/cgi-bin
chmod -R 2570 /www/cgi-bin
```

或者，如果你只想允许单个用户（例如 `cgiguru`）开发 CGI 脚本，你可以按如下方式设置文件和目录权限：

```bash
chown -R cgiguru.httpd /www/cgi-bin
chmod -R 750 /www/cgi-bin
```

这里，用户 `cgiguru` 拥有该目录，而用于 Apache 服务器的组（由 `Group` 指令指定）是该目录及其文件的组所有者。

最后，`CustomLog` 和 `ErrorLog` 指令中使用的日志目录应仅允许 `root` 用户写入。对此类目录（例如 `/www/logs`）推荐的权限设置如下：

```
chown -R root.root /www/logs
chmod -R 700 /www/logs
```

> 不要允许任何人（包括 Apache 用户或组）读取、写入或执行在 `CustomLog` 和 `ErrorLog` 指令中指定的日志目录中的文件。

始终确保你对通过 Web 可访问的新目录采用最小化方法授予访问权限。还要确保你不允许 Web 访客查看任何目录列表。你可以使用后面讨论的方法隐藏目录列表。

## 目录索引文件

每当用户请求通过 Web 访问某个目录时，Apache 会执行以下操作之一：

- 1. 检查该目录是否可访问。如果是，则继续；否则，显示错误消息。
- 2. 在确定目录可访问后，它查找通过使用 `DirectoryIndex` 指令指定的目录索引文件。默认情况下，该文件是 `index.html`。如果它能读取请求目录中的此文件，则显示文件内容。如果不存在此类文件，Apache 将检查是否可以为该目录创建动态列表。如果允许创建动态列表，它将创建该列表并向用户显示目录内容。

由于 Apache 创建的动态生成的目录列表会为潜在的不良分子提供关于你的目录结构的线索，因此你不应该允许此类列表。避免创建动态目录列表的最简单方法是创建一个文件名在 `DirectoryIndex` 指令中指定的文件。例如，如果你将 `DirectoryIndex` 设置如下：

```
DirectoryIndex index.html index.htm
```

Apache 将首先在 URL 请求的目录中查找 `index.html`，如果 `index.html` 缺失，则查找 `index.htm`。

然而，许多网站暴露目录的一个常见原因是，当创建新目录时，创建者忘记创建索引文件或上传了大小写错误的索引文件，例如 `INDEX.HTML` 或 `INDEX.HTM`。

如果这种情况经常发生，你可以使用 CGI 脚本自动将用户重定向到你的主页或内部搜索引擎界面。只需修改 *DirectoryIndex* 指令如下：

```
DirectoryIndex index.html index.htm /cgi-bin/index.pl
```

现在，在 *ScriptAlias* 指定的目录中添加一个 CGI 脚本，例如清单 18-1 中所示的那个。

### 清单 18-1: **index.pl**

```perl
#!/usr/bin/perl
# Purpose: this script is used to redirect
# users who enter a URL that points to
# directories without index.html page.
use CGI qw(:standard);

# Set the automatically redirect URL
my $AUTO_REDIRECT_URL = '/';

# Get the current URL path
my $curDir = $ENV{REQUEST_URI};

# If the current URL path is not home page (/)
# then redirect user to home page
if ($curDir ne '/') {
    print redirect($AUTO_REDIRECT_URL);
    # If the home page is also missing the index page,
    # we can't redirect back to home page (to avoid
    # recursive redirection), so display an error message.
} else {
    print header;
    print "HOME PAGE NOT FOUND!";
}
exit 0;
```

此脚本在 Apache 未能找到目录索引文件（*index.html* 或 *index.htm*）后运行。该脚本只是将 URL 指向没有索引文件的目录的用户重定向到网站的主页。

如果你使用不同的别名名称，请确保更改上述指令中的 /cgi-bin/ 路径。如果你根本不想显示任何目录列表，你可以简单地通过设置以下配置来禁用目录列表：

```
<Directory />
  Options -Indexes
</Directory>
```

*Options* 指令告诉 Apache 禁用所有目录索引处理。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_538_0.png)

> 告诉 Apache 不要跟随符号链接也是一个好主意，因为这些链接可能会意外地暴露你不希望公开的部分磁盘空间。要禁用 Apache 跟随符号链接，请将 *Options* 指令设置为 -FollowSymLinks。

## 禁用默认访问

一个好的安全模型规定不存在默认访问权限，因此要养成首先不允许任何访问权限的习惯。仅向特定目录允许特定访问。要实施无默认访问，请在 `httpd.conf` 中使用以下配置段：

```
<Directory />
  Order deny,allow
  Deny from all
</Directory>
```

这会首先禁用所有访问。现在，如果你需要启用对特定目录的访问，请再次使用 `<Directory ...>` 容器来打开该目录。例如，如果你想允许访问 /www/htdocs，请添加以下配置：

```
<Directory "/www/htdocs">
  Order deny,allow
  Allow from all
</Directory>
```

这种方法——只打开你需要的——是一种预防性安全措施，并高度推荐。此外，不要允许用户使用每目录配置文件（.htaccess）来更改开放访问的目录中的任何目录级配置选项。

## 禁用用户覆盖

要在任何目录中使用每目录配置文件（.htaccess）禁用覆盖配置设置，请执行以下操作：

```
<Directory />
  AllowOverride None
</Directory>
```




此举禁止用户覆盖设置，并且实际上会加快服务器速度，因为服务器不再需要为每个请求查找目录级访问控制文件（.htaccess）。

此处讨论的 Apache 配置问题及解决方案有助于你创建一个安全的 Web 服务器。然而，一些管理员希望在安全性方面更进一步（在偏执狂的领域里）。

## 替罪羊配置

在这种配置中，Web 服务器被放置在防火墙和内部局域网之外。内部局域网中的主机通过防火墙主机接收或发送 Internet 数据包。这样，内部主机便受到保护，免受外部攻击（至少在理论上是这样）。另一方面，Web 服务器则完全暴露于攻击之下；这就是为什么这种配置被称为“替罪羊”配置的原因。图 18-3 展示了替罪羊配置。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_539_0.png)

在这种配置下，以下情况是成立的：

- 入侵者无法观察或捕获流经内部主机之间的网络流量。此类流量可能包括认证信息、专有商业信息、人事数据以及许多其他类型的敏感数据。
- 入侵者无法触及内部主机，或获取关于它们的详细信息。

替罪羊配置防范了这两种威胁，并使 Web 服务器与内部网络及其流量隔离开来。

在此配置中，明智的做法是在路由器上关闭源路由。这样，Web 服务器主机就不能被用来将数据包转发到内部网络中的主机。

有些人喜欢将 Web 服务器放在防火墙后面。在这种配置中，防火墙成为内部局域网和 Web 流量的网关，而防火墙配置变得复杂。我认为，这种复杂性可能会导致防火墙出现安全漏洞，从而使其初衷落空。

### 偏执狂配置

这种配置适用于对安全性极度多疑的 Apache 管理员。它是本章讨论的配置中限制最严格的一种。

以下是我认为适用于 Apache 的偏执狂配置。

- **不支持通用网关接口（CGI）脚本。** 如前所述，CGI 脚本通常是大多数 Web 安全事件的根源，因此在偏执狂配置中没有任何位置。
- **不支持 SSI。** 与 CGI 脚本类似，SSI 页面经常有问题，因此在偏执狂配置中没有立足之地。
- **允许每用户 Web 站点。** 使用 `http://www.domain.com/~username` URL 方案会带来许多安全问题，例如用户未采取适当措施来降低向外界暴露文件系统信息的风险；用户错误操作使得服务器上的非公共磁盘区域变为公开可访问；等等。因此，每用户 Web 站点在偏执狂配置中没有位置。
- **不通过网络提供状态信息。** Apache 提供了一个状态模块，通过 Web 提供有关服务器的有价值状态信息。如果破坏者能够访问这些信息，它们可能会提供线索。确保他们无法访问此类信息的偏执方式是首先根本不安装该模块。

可以通过使用以下配置命令来实现偏执狂配置：

```bash
./configure --prefix=/home/apache\
--disable-module=include\
--disable-module=cgi\
--disable-module=userdir\
--disable-module=status
```

当你从 Apache 源发行版的 `src` 目录运行上述配置命令后，你便可以以偏执狂配置构建并安装 Apache（位于 `/home/apache`）。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_541_0.png)

曾见过许多偏执狂管理员运行 Apache 在非标准端口上，例如 8080 或 9000。如果你想在此类端口上运行 Apache，请更改 `httpd.conf` 中的 Port 指令。但请注意，破坏者通常使用端口扫描软件来检测 HTTP 端口，而使用非标准端口会让正常用户更加费力，因为他们必须在首次用于进入你的 Web 站点的 URL 末尾输入 :端口号（`http://www.domain.com:port/`）。

## 保护你的 Web 内容

你的 Web 内容是你的资产，因此需要保护它们免受破坏和黑客攻击。糟糕或缺失的内容发布策略可能会导致你的内容面临安全风险。在本节中，我将讨论一个以安全为重点的内容发布策略。此外，如果你的某些 Web 内容不应被 Web 搜索引擎（即其机器人）索引，那么之前讨论的机器人或蜘蛛程序控制技术可能会证明非常有用。

### 内容发布准则

制定内容发布策略是一回事，强制执行它是另一回事。在你制定了自己的发布策略后，与应该使用它的人讨论此事。获取他们对每个策略条款的反馈，并如有必要，完善你的策略使其实用。

内容发布人员和脚本开发人员应了解并遵守以下准则：

- 在存储内容文件（如 HTML 文件、图像文件、声音文件、视频片段等）时，发布者必须确保该文件可被 Web 服务器读取（即 `user` 指令指定的用户名）。除了发布者用户外，不应允许任何人写入文件和目录。
- 任何因为包含通过应用程序或脚本间接访问的信息而无法直接在 Web 浏览器中显示的文件或目录，都不应位于 DocumentRoot 指定的目录中。例如，如果你的脚本之一需要访问一个不应从 Web 直接访问的数据文件，请不要将数据文件保存在文档树内。将文件保存在文档树外，并让脚本从那里访问它，因为即使没有任何可显示内容指向这些文件的链接，它们仍可能对其他人可访问。
- 动态内容生成器（如 CGI 应用程序）创建的任何临时文件都应驻留在一个子目录中，该子目录赋予生成器写入权限。此目录必须位于内容区域之外，以确保应用程序中的错误不会意外擦除任何现有内容文件。换句话说，不要在你的文档树中放置可被 Web 服务器写入的目录。这可以确保脚本中的错误不会意外覆盖文档树中的现有文件。
- 为了在内容上明确版权，内容页面上应同时包含可见和嵌入的版权声明。嵌入的版权信息应尽可能放在文档的开头。例如，在 HTML 文件中，你可以使用一对注释标签将版权信息嵌入文件开头。例如，`<!-- Copyright (c) 2001 by YourCompany; All rights reserved. -->` 可以嵌入在每个页面中。如果你计划经常更新版权信息，你可以考虑使用 `#include` 指令的 SSI 解决方案。
- 如果你拥有大量想要保护以免于版权盗窃的图形内容（图像），请考虑使用水印技术。这项技术不可见地嵌入图像中以保护版权。其想法是，如果你检测到某个网站未经许可使用你的图形内容，你可以通过查看隐藏信息来验证盗窃。如果信息匹配你的水印 ID，你可以清楚地识别窃贼并采取法律行动。目前可用的水印工具的强度存疑，因为许多程序可以轻松移除原始版权持有者的水印。不过，如果你担心你的图形内容，这项技术仍值得研究。

### 保护你的内容免受机器人和蜘蛛的影响

如果你认真保护你的 Web 内容，你应该了解 Web 蜘蛛和机器人。所有搜索引擎，如 Yahoo!、AltaVista、Excite 和 Infoseek 都使用自动化机器人应用程序来搜索 Web 站点并索引内容。这通常是期望的，但有时你可能会希望阻止这些机器人访问你 Web 站点的一部分。

如果你 Web 站点某个部分的内容经常过期（例如每天），你不希望搜索机器人索引它们。为什么不呢？嗯，当搜索引擎站点的用户找到一个指向旧内容的链接并点击它，结果发现该链接不存在时，用户不会高兴。该用户可能会跳过你的站点，直接去下一个链接，而不再回来。





在某些情况下，您可能希望禁用内容（或其部分内容）的索引功能。这些机器人在遍历网络和网站时，可能会产生预期和未预期的影响。有时，搜索机器人会因请求过多文档且速度过快而导致网站不堪重负。目前，制定网络机器人行为标准的努力正在进行中。当前的协议版本——机器人排除协议（Robot Exclusion Protocol）——允许网站管理员在其网站上放置一个 `robots.txt` 文件，以指示机器人不应访问的位置。例如，对于试图索引 HTML 页面的机器人来说，一个大型位图图像档案毫无用处。向这些机器人提供这些文件，既是对您服务器端资源的不必要消耗，也是对机器人端资源的不必要消耗。

当前的机器人排除协议是自愿执行的，随着机器人部署经验的积累，机器人开发者的礼仪规范也在逐步演变。大多数主流搜索引擎都遵守该协议。

当遵守标准的网络机器人访问名为 `www.somesite.com` 的网站时，它首先检查是否存在 URL `http://www.somesite.com/robots.txt`。

如果该 URL 存在，机器人将解析其内容中包含的指令，这些指令告知机器人如何索引该网站。作为 Web 服务器管理员，您可以创建适合您网站的指令。请注意，一个网站只能有一个 `/robots.txt` 文件。该文件包含的记录可能如下所示：

```
User-agent: *
Disallow: /cgi-bin/
Disallow: /tmp/
Disallow: /~sam/
```

第一条指令 `User-agent` 告知机器人，以下指令应被所有机器人考虑。接下来的三条 `Disallow` 指令告知机器人不要访问指令中提到的目录。请注意，对于您想要排除的每个 URL 前缀，都需要单独的一行 `Disallow` 语句——您不能使用以下写法：

```
Disallow: /cgi-bin/ /tmp/ /~sam/
```

此外，记录中也不允许有空行，因为空行用于分隔多个记录。`User-agent` 和 `Disallow` 行均不支持正则表达式。`User-agent` 字段中的 `*` 是一个特殊值，表示任何机器人。具体来说，您不能拥有如下的行：

```
Disallow: /tmp/*
```

或

```
Disallow: *.gif
```

未被明确禁止的任何内容都被视为机器人可访问的（以下是一些示例配置）。

### 排除所有机器人

要将所有机器人从整个服务器中排除，请使用以下配置：

```
User-agent: *
Disallow: /
```

### 允许所有机器人完全访问

要允许所有机器人完全访问，请使用以下配置：

```
User-agent: *
Disallow:
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_544_0.png)

您也可以通过删除 `robots.txt` 文件来达到相同的效果。

### 排除单个机器人

要排除名为 `WebCrawler` 的单个机器人访问该网站，请使用以下配置：

```
User-agent: WebCrawler
Disallow: /
```

### 允许单个机器人

要允许名为 `WebCrawler` 的单个机器人访问该网站，请使用以下配置：

```
User-agent: WebCrawler
Disallow:
```
```
User-agent: *
Disallow: /
```

### 禁止单个文件

要禁止名为 `/daily/changes_to_often.html` 的单个文件被机器人索引，请使用以下配置：

```
User-agent: *
Disallow: /daily/changes_to_often.html
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_544_1.png)

目前，机器人没有 `Allow` 指令。

## 日志记录与安全

优秀的 Web 管理员会密切关注服务器日志，这有助于发现异常的访问模式。在本节中，我将讨论如何保护您的日志文件免受未授权访问，以及当您在日志文件中检测到异常访问时应采取的措施。

**注意** 日志非常有用，但如果捣乱者能够修改它们，它们就毫无用处了。因此，请务必保护日志文件。我建议将日志文件放在独立的分区上，除了 root 用户外，任何人都无权对其进行更改。

### CustomLog 和 ErrorLog

通过使用 `CustomLog` 和 `ErrorLog` 指令（我在第 8 章中有所介绍），Apache 允许您将成功的访问请求和导致错误的访问请求记录在不同的日志文件中。例如：

```
CustomLog /logs/access.log common
ErrorLog /logs/error.log
```

第一条指令 `CustomLog` 记录传入您网站的每个请求，而第二条指令 `ErrorLog` 仅记录产生错误状态的条件请求。`ErrorLog` 文件是密切监控您的 Web 服务器报告的问题的理想位置。您可以使用精美的日志分析程序（如 Wasage，www.boutei.com）定期分析和监控日志文件。

确保由 `ServerRoot`、`CustomLog` 和 `ErrorLog` 指令指定的目录只能由 root 用户写入。您不需要赋予 Apache 用户/组在日志目录中读取或写入的权限。允许 root 用户以外的任何人写入日志目录中的文件可能会导致重大安全漏洞。为确保只有 root 用户才能访问名为 `/logs` 的目录中的日志文件，请遵循以下步骤：

- 1. 使用以下命令将该目录及其内部所有文件的所有权更改为 root 用户和 root 组：
    `chown -R root:root /logs`
- 2. 使用以下命令更改目录的权限：
    `chmod -R 750 /logs`

### 如果在日志文件中看到异常访问该怎么做

如果您注意到异常访问，例如有人试图向您的 CGI 脚本提供异常参数，您应将其视为敌对尝试并立即调查此事。以下是在此类情况下您可以使用的流程：

- 1. 获取用于试图欺骗 CGI 脚本的完整 URL。
- 2. 如果您没有编写该脚本，请询问脚本作者当有人向脚本传递这样的 URL（即 URL 中 `?` 之后的参数）时会发生什么。如果有理由担心，请继续前进或在此处停止调查，但请在 `POSSIBLE-ATTACKS.txt` 文件中记录 IP 地址、URL 以及时间戳和日期。
- 3. 如果该 URL 导致脚本执行其不应执行的操作，请考虑在该 URL 不再对系统构成威胁之前将脚本离线，直到修复为止。
- 4. 使用 host 程序检测捣乱者 IP 地址的主机名。有时 host 无法找到主机名。在这种情况下，请尝试使用 traceroute 并识别拥有该 IP 地址的 ISP。
- 5. 对 ISP 执行 whois 域名查询，并查找 whois 输出中列出的技术联系人信息。如果您未安装 whois 程序，可能需要访问域名注册机构的网站执行 whois 查询。尝试从 www.internic.net 网站找到合适的域名注册机构。
- 6. 向 ISP 的技术联系人地址发送关于该事件的电子邮件，并提供日志片段供其审阅。请以非常礼貌和友好的方式撰写电子邮件。请记住，另一端的 ISP 是此时您唯一的防线。礼貌地请求快速解决或回应。
- 7. 如果由于您的网站中其他人重度使用该脚本而无法将其离线，您可以禁止捣乱者使用它。例如，假设您的脚本在脚本别名 `\`/some/path/to/cgi/scripts/`\` 下运行，该别名设置为：

```
ScriptAlias /ext/ "/some/path/to/cgi/scripts/"
```

将上述配置更改为：

```
<Location /ext>

    SetHandler cgi-script
    Options -Indexes +ExecCGI

    AllowOverride None
    Order allow,deny
    Allow from all
    Deny from 192.168.1.100

</Location>
```

将 `192.168.1.100` 替换为捣乱者的 IP 地址。此配置将对除 `Deny from` 行中指定的 IP 地址上的用户之外的所有人正常运行您的脚本。但是，如果捣乱者的 ISP 为其客户使用动态分配的 IP 地址，那么锁定确切的 IP 地址将毫无用处，因为捣乱者可以使用不同的 IP 地址返回。在这种情况下，请考虑锁定整个 IP 网络。例如，如果 ISP 使用 `192.168.1.0` 网络，您只需从 `Deny from` 行中移除 `\`\.100\` 即可阻止整个 ISP。这是一种激烈的手段，可能会阻止该 ISP 上大量无辜用户使用此脚本。在考虑是否阻止 ISP 上的所有人时，请谨慎行事。





8.  等待几天，让互联网服务提供商（ISP）作出回应。如果你没有收到其回复，请尝试通过其网站与 ISP 取得联系。如果问题依然存在，请联系法务部门，以确定你可以采取哪些法律手段来要求 ISP 采取行动。

## 保护你的 CGI 实现

大多数 Web 安全专家认为，最大的安全风险因素是在 Web 服务器上运行的、用于生成动态内容的脚本或应用程序。由于 CGI 脚本通常负责创建动态内容，因此它们往往造成了最大的损害。本节重点讨论与 CGI 脚本相关的安全风险，并展示如何降低这些风险。

### 通过智能编程防范 CGI 风险

根据 SANS（www.sans.org）的说法，CGI 脚本相关的安全风险在其十大互联网安全问题分析中排名第二。然而，CGI 本身并不是不安全的；编写拙劣的 CGI 脚本才是 Web 安全漏洞的主要来源。实际上，CGI 规范的简单性使得许多没有经验的程序员也能编写 CGI 脚本。这些缺乏经验的程序员由于不了解互联网络的安全方面，创建了一些能正常工作的应用程序或脚本，同时也无意中在系统中留下了后门和漏洞。

接下来的章节将首先讨论 CGI 应用程序或脚本所构成的风险类型，然后讨论解决这些风险的方法。

> 术语*CGI 应用程序*和*CGI 脚本*可以互换使用。

### 信息泄露

许多 CGI 脚本会被破坏者诱导，从而泄露关于用户或 Web 服务器上可用资源的信息。此类泄露有助于破坏者入侵系统。破坏者掌握的系统信息越多，其入侵系统的能力就越强。例如，如果使用以下 URL 通过 *showpage.cgi* 脚本显示 /doc/article1.html 页面：

```http://unsafe-site.com/cgi-bin/showpage.cgi?pg=/doc/article1.html```

破坏者可能会尝试如下操作：

```http://unsafe-site.com/cgi-bin/showpage.cgi?pg=/etc/passwd```

这将显示整个系统的 /etc/passwd（用户密码文件）。只有当 *showpage.cgi* 的作者没有保护该脚本免受此类泄露时，这种情况才会发生。

编写拙劣的 CGI 脚本可能被破坏者利用，使服务器消耗系统资源，从而导致服务器几乎无响应。例如，以下 URL 允许网站访客查看网站上分类广告的列表：

`http://unsafe-site.com/cgi-bin/showlist.pl?start=1&stop=15`

`start=1` 和 `stop=15` 参数用于控制显示记录的数量。如果 `showlist.pl` 脚本仅依赖提供的 start 和 stop 值，那么破坏者可以编辑 URL，并为 stop 参数提供更大的数值，使 `showlist.pl` 显示比平时更大的列表。这会怎样？破坏者可以利用这一知识，通过发送处理时间更长的请求来使 Web 服务器过载，这会让真实用户等待，并可能导致他们转向竞争对手的网站。

## 通过 CGI 脚本伪造系统命令

在许多情况下，破坏者已成功诱导基于 HTML 表单的邮件脚本运行系统命令或泄露机密系统信息。例如，假设你有一个 Web 表单，用户可以使用它来注册你的服务或提供反馈。拥有此类 Web 表单的大多数网站都会通过电子邮件向用户发送一封感谢信。使用 CGI 脚本处理该表单。该脚本可能执行类似以下操作来发送电子邮件：

`system("/bin/mail -s $subject $emailAddress < $thankYouMsg");`

系统调用运行 `/bin/mail` 邮件程序，并将变量 `$subject` 的值作为主题头，将变量 `$emailAddress` 的值作为用户的电子邮件地址，并重定向由 `$thankYouMsg` 变量指定的文件的内容。这可以正常工作，通常不应该有人知道你的应用程序使用了这样的系统调用。然而，破坏者总是试图破坏系统，因此，对破坏你的网站感兴趣的破坏者可能会调查破坏者可以访问的一切，并尝试为你的 Web 表单输入不寻常的值。例如，如果破坏者输入 `vandal@emailaddr < /etc/passwd;` 作为电子邮件地址，脚本将被欺骗，将 `/etc/passwd` 文件发送到破坏者指定的电子邮件地址！

> 提示
> 如果你在 CGI 脚本中使用 `system()` 函数，你应该在 `#!/path/to/perl` 行中使用 `-T` 选项来启用 Perl 的污点检查模式。你还应使用 `set $ENV{PATH} = '/path/to/commands:/you/call/via/system'` 设置 `PATH`（环境变量）以增加安全性。

## 用户输入使某些系统调用不安全

某些系统调用在 CGI 脚本中使用是不安全的。例如，在 Perl（一种广泛使用的 CGI 编程语言）中，可以使用 `system()`、`exec()`、`piped open()` 和 `eval()` 函数进行此类调用。类似地，在 C 语言中，`popen()` 和 `system()` 函数也是潜在的安全隐患。所有这些函数/命令通常都会调用一个子进程（如 `/bin/sh`）来处理用户命令。

即使使用 `system()` 或 `exec()` 调用的 shell 脚本也可能会为破坏者打开一个入口。shell 解释器和 Perl 中可用的反引号引号（用于将程序的输出捕获为文本字符串）也是危险的。

为了说明仔细使用系统调用的重要性，请考虑以下看似无害的 Perl 代码段：

```perl
#!/usr/bin/perl -w
#
# 目的：演示编写拙劣的 CGI 脚本中的安全风险。
#
# 从查询字符串获取域名
# 环境变量。
#

my $domain = $ENV{'QUERY_STRING'};

# 打印适当的内容类型。
# 因为 whois 输出是纯文本，
# 我们在这里选择使用 text/plain 作为内容类型。
#
print "Content-type: text/plain\n\n";

# 这里是不好的系统调用：
system("/usr/bin/whois $domain");

# 这里是用反引号进行的另一个不好的系统调用：
#
# my $output = `/usr/bin/whois $domain`;
#
# print $output;

exit 0;
```

这个小 Perl 脚本旨在成为一个基于 Web 的 WHOIS 网关。如果这个脚本名为 `whois.pl`，并且存储在名为 `unsafe-site.com` 的网站的 `cgi-bin` 目录中，用户可以按如下方式调用该脚本：

`http://unsafe-site.com/cgi-bin/script.pl?domain=anydomain.com`

该脚本将通过 `QUERY_STRING` 变量将 `anydomain.com` 作为 `$domain` 变量，并以 `$domain` 值作为参数启动 `/usr/bin/whois` 程序。这会返回 InterNIC 维护的 WHOIS 数据库中的数据。这看起来非常无辜且良好，但该脚本是一个等待发生的灾难。考虑以下行：

`http://unsafe-site.com/cgi-bin/script.pl?domain=nitec.com;ps`

这会对名为 `nitec.com` 的域名执行 WHOIS 查询，并提供 Unix `ps` 实用程序（显示进程状态）的输出。这揭示了本不应该提供给请求方的系统信息。使用这种技术，任何人都可以了解你的大量系统信息。例如，用 `df`（一个常见的 Unix 实用程序，打印磁盘空间摘要）替换 `ps` 命令，任何人都可以确定你有哪些分区以及它们有多满。这个安全漏洞可能带来巨大危险。

教训是什么？不要信任任何输入，并且不要让系统调用成为容易被滥用的目标。如何实现这些目标是下一节要讨论的主题。

## 用户可以修改 HTML 页面中的隐藏数据

你可能已经知道，HTTP 是一个无状态协议。许多 Web 开发者将状态信息或其他重要数据保存在 cookies、临时文件中，或者使用所谓的隐藏标签中。因为用户可以关闭 cookies，而且为每个用户创建唯一的临时文件很麻烦，所以隐藏标签通常被使用。隐藏标签看起来类似于以下内容：

`<input type="hidden" name="dataKey" value="dataValue">`

例如：

`<input type="hidden" name="state" value="CA">`

这里，隐藏标签存储了 "state=CA"，可以在后续调用中由同一应用程序检索。隐藏标签在多屏 Web 应用程序中很常见。因为用户可以手动更改隐藏标签，所以它们不应该被信任。保护被篡改数据有两种方式：开发人员可以在每次使用前验证隐藏数据，或者开发人员可以使用安全方案来确保数据没有被用户篡改。列表 18-2 中显示的 CGI 脚本演示了使用 RSA Data Security MD5 消息摘要算法来保护隐藏数据。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_550_0.png)

MD5 算法的细节定义在 RFC 1321 中。

## 列表 18-2: hidden-md5,eg

```perl
#!/usr/bin/perl -w
#
# 目的：此脚本演示了在多屏幕
# Web 应用程序中使用
# MD5 消息摘要。
#
# CVS: $Id$
# #####################################################################################
use strict;
```





# **示例 18-2**

```perl
use CGI qw( :standard );
use Digest::MD5;

my $query = new CGI;

# Call the handler subroutine to process user data
&handler;

# Terminate
exit 0;

sub handler{

    #
    # Purpose: Determine which screen to display
    #          and call the appropriate subroutine to
    #          display it.
    #

    # Get user-entered name (if any) and e-mail address
    # (if any) and initialize two variables using given
    # name and e-mail values. Note: first time we will
    # not have values for these variables.
    my $name   = param('name');
    my $email  = param('email');

    # Print the appropriate Content-Type header and
    # also print HTML page tags
    print header,
        start_html( -title => 'Multi-Screen Web Application
    Demo' );

    # If we do not have value for the $name variable,
    # we have not yet displayed screen one so show it.
    if ($name eq ''){

        &screen1;

    # If we have value for the $name variable but the
    # $email variable is empty then we need to show
    # screen 2.
    } elsif($email eq '') {

        &screen2($name);

    # We have value for both $name and $email so
    # show screen 3.
    } else {
        &screen3($name, $email);
    }

    # Print closing HTML tag for the page
    print end_html;
}

sub screen1{
#
# Purpose: print an HTML form that asks the
# user to enter his or her name.
#

  print h2("Screen 1"),
    hr(1 => 0, -color => 'black'),
    start_form,
    'Enter name: ',
    textfield(-name => 'name', -size => 30),
    submit(-value => ' Next '),
    end_form;

}

sub screen2{
#
# Purpose: print an HTML form that asks the
# user to enter her email address. It also
# stores the name entered in the previous screen.
#

# Get the name
my $name = shift;

# Create a MD5 message digest for the name
my $digest = &create_message_digest($name);

# Insert the digest as a new CGI parameter so
# that we can store it using CGI.pm's hidden()
# subroutine.
param('digest', $digest);

# Now print the second screen and insert
# the $name and $digest values as hidden data.
print h2("Screen 2"),
hr([-size=>0,-color=>'black']),
start_form,
'Enter email: ',
textfield(-name=>'email', -size=>30),
hidden('name'),
hidden('digest'),
submit(-value => ' Next '),
end_form;
}

sub screen3
{
# # Purpose: Print a message based on the
# # data gathered
# # in screen 1 and 2. However, print the message
# # only if the entered data has not been altered.
#
# Get name and email address
my ($name, $email) = @_;

# Get the digest of the $name value
my $oldDigest = param('digest');

# Create a new digest of the value of the $name variable
my $newDigest = &create_message_digest($name);

# If both digests are not same then (name) data has been
altered
# in screen 2. Display an alert message and stop processing
# in such case.
if ($oldDigest ne $newDigest){
return (0, alert('Data altered. Aborted!'));
}

# Since data is good, process as usual.
print h2("Screen 3"),
hr([-size=>0,-color=>'black']),
p('Your name is ',b($name)
, and your email address is ',b($email),'.'),
a([-href=>"$ENV{SCRIPT_NAME}"],'Restart');
}

sub create_message_digest{
# # Purpose: Create a message digest for the
# # given data. To make the digest hard
# # to reproduce by a vandal, this subroutine
# # uses a secret key.
#
my $data = shift;
my $secret = 'ID10t' ;  # Change this key if you like.

# We need the following line to tell Perl that
# we want to use the Digest::MD5 module.
use Digest::MD5;

# Create a new MD5 object
my $ctx = Digest::MD5->new;

# Add data
$ctx->add($data);

# Add secret key
$ctx->add($secret);

# Create a Base64 digest
my $digest = $ctx->b64digest;

# Return the digest
return $digest;
}

sub alert{
#
# Purpose: Display an alert dialog box
#          using Java Script.
#

# Get the message that we need to display
my $msg = shift;

# Create a java script that uses the alert()
# dialog box function to display a message
# and then return the browser to previous screen.
print <<JAVASCRIPT;

<script language="JavaScript">
alert("$msg");
history.back();
</script>

JAVASCRIPT
}
```

示例 18-2 是一个简单的多屏幕 CGI 脚本，它要求用户在第一个屏幕输入姓名，然后在下一个屏幕输入电子邮件地址，最后打印出一条消息。当用户从一个屏幕切换到另一个屏幕时，使用隐藏标签将前一个屏幕的数据传递到下一个屏幕。该脚本的工作方式在以下段落中进行了讨论。

在脚本的最开始，使用了两个外部模块 —— CGI 和 Digest::MD5。第一个是使用 Perl 编写 CGI 脚本变得非常容易的最受欢迎的 CGI 模块。第二个模块为我们提供了 MD5 摘要算法的接口。

脚本首先创建一个名为 `$query` 的 CGI 对象。然后，它为每个请求调用 `handler()` 子程序。`handler()` 子程序是脚本的驱动器。查看 `handler()` 子程序内部，你会发现它将用户输入的姓名和电子邮件字段（从 Web 表单中收集）分别赋值给 `$name` 和 `$email`。然后，它使用 CGI 模块中的 `header()` 方法打印 Content-Type 头消息，并使用 CGI 模块中的 `start_html()` 方法创建 HTML 文档的开头。

如果用户尚未输入姓名，该程序将通过使用 `screen1()` 子程序显示屏幕 1。如果 `$name` 变量具有值，`handler()` 子程序将通过使用 `screen2()` 子程序显示屏幕 2。当 `$name` 和 `$email` 都具有值时，使用 `screen3()` 子程序显示屏幕 3。最后，该程序使用 CGI 模块中的 `end_html()` 方法打印页面的结束标签。

现在查看 `screen1()` 子程序，它非常简单。它只是显示一个 Web 表单，其中有一个名为 name 的字段需要用户填写。请注意，整个 Web 表单是使用 CGI 模块中的 `start_form()`、`textfield()`、`submit()` 和 `end_form()` 方法创建的。表单的 action 未定义，这意味着生成该 Web 表单的脚本将被调用。换句话说，当显示屏幕 1 的表单且用户输入其姓名并点击 Submit（提交）时，相同的脚本将被调用，且 name 字段设置为用户定义的数据。

`screen2()` 子程序将全局变量 `$name` 作为参数，并使用 `create_message_digest()` 子程序为用户输入的姓名创建一个名为 `$digest` 的 MD5 摘要。然后，使用 `param('digest', $digest)` 将该摘要添加到 CGI 对象中，然后通过 CGI 模块中的 `hidden('digest')` 方法将其输入到屏幕 2 的 Web 表单中。屏幕 2 的 Web 表单是使用 CGI 模块中的 `start_form()`、`textfield()`、`hidden()`、`submit()` 和 `end_form()` 方法创建的。`hidden('argument')` 方法简单地创建一个 `<input type=hidden name=argument value=value_found in_CGI_object_for_argument>` 标签。创建摘要并将其与姓名一起隐藏在 Web 表单中的目的是，这允许我们确定隐藏的姓名字段是否被篡改。

当调用 `screen3()` 子程序时，它接收全局变量 `$name` 和 `$email` 作为参数。它还分配局部变量 `$oldDigest` 为存储在 CGI 对象中的隐藏摘要。然后，它使用 `$name` 变量的值调用 `create_message_digest()` 子程序创建一个新摘要。然后，它比较旧摘要和新摘要，以确定姓名是否在屏幕 2 中被篡改。请记住，姓名是在屏幕 1 中输入的，并且使用 HTML 隐藏标签在屏幕 2 中隐藏了。因此，存在有人在传输过程中篡改姓名值的可能性。

如果摘要不匹配，则使用 `alert()` 子程序打印警告消息，该子程序显示一个 JavaScript 弹出消息。否则，姓名和电子邮件地址将被打印在屏幕上。

最有趣的子程序是 `create_message_digest()`。它将任何内容作为参数，并使用名为 `$ctx` 的 Digest::MD5 对象通过 Digest::MD5 对象的 `add()` 方法添加给定的数据和一个秘密短语（存储在 `$secret` 中）。然后，它使用 `b64digest()` 方法创建一个 Base64 MD5 摘要，并将其返回给调用的子程序。

当首次运行 CGI 脚本时，它会产生一个屏幕，要求用户输入其姓名。在用户输入姓名后，用户继续到下一个屏幕，在那里用户被要求输入电子邮件地址。该屏幕的 HTML 源代码在示例 18-3 中显示。

# **示例 18-3：hidden-md5.eg 中屏幕 2 的 HTML 源代码**

```html
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML//EN">
<HTML>
	<HEAD>
		<TITLE>Multi-Screen Web Application Demo</TITLE>
	</HEAD>

	<BODY>
		<H2>Screen 2</H2>
		<HR SIZE="0" COLOR="black">
		<FORM METHOD="POST"
			ENCTYPE="application/x-www-form-urlencoded">

	Enter email:
		<INPUT TYPE="text"
			NAME="email"
			SIZE=30>

		<INPUT TYPE="hidden"
			NAME="name"
			VALUE="Cynthia">

		<INPUT TYPE="hidden"
			NAME="digest"
			VALUE="IzrSj/lrsWlYHfshrKw/A">

		<INPUT TYPE="submit"
```





```
NAME=".submit"
VALUE=" Next ">

</FORM>
</BODY>
</HTML>
```

隐藏数据是通过以下代码行存储的：

```
<INPUT TYPE="hidden"
NAME="name"
VALUE="Cynthia">

<INPUT TYPE="hidden"
NAME="digest"
VALUE="1zrSjLLrsWlYHNfshrKw/A">
```

第一个隐藏数据标签行存储 name=Cynthia，第二个隐藏数据标签行存储 digest=1zrSjLLrsWlYHNfshrKw/A。第二组数据是针对屏幕 1 中输入的名称生成的消息摘要。当用户在第二个屏幕中输入电子邮件地址并继续操作时，将显示最终屏幕。

然而，在生成最终屏幕之前，会对屏幕 1 中的名称字段计算一个消息摘要。该摘要将与之前创建的摘要进行比较，以验证屏幕 1 中名称字段的值在屏幕 2 中未被篡改。由于 MD5 算法为给定的数据集创建相同的消息摘要，新旧摘要之间的任何差异都会引发警告，脚本将显示警报消息并拒绝完成处理。换言之，如果恶意用户决定篡改存储在屏幕 2（如清单 18-3 所示）中的数据并提交数据进行最终处理，摘要不匹配将使脚本能够检测到篡改并采取相应措施。在实际世界的 CGI 脚本（用 Perl 编写）中，您可以使用 `create_message_digest()` 子例程为任何内容创建消息摘要。

> 您可以使用 `perl -MCPAN -e shell` 命令从 CPAN 下载并安装 Digest::MD5 的最新版本，然后在 CPAN shell 提示符下执行 `install Digest::MD5` 命令。

## 保持用户输入安全

如您所见，CGI 脚本造成的大多数安全漏洞都是由于不当的用户输入引起的。下一节将讨论一些常见问题及其解决方案。

确保用户输入安全有两种方法：

- 扫描输入中的非法字符并将其替换或移除。例如，对于 `whois.pl` 脚本，您可以添加以下行：
  ```perl
  $domain =~ s/[:\[\]{}<>&\t/]/g;
  ```
  这会移除非法的元字符。这是一种常见但不建议采用的方法，因为它要求程序员知晓所有可能导致问题的字符组合。如果用户使用了程序员未预测到的输入，程序可能会被以程序员未预期的方式使用。

- 定义一个可接受字符列表，并替换或移除任何*非*可接受的字符。有效输入值的列表通常是一个可预测、定义明确且规模可控的集合。

我更倾向于上述第二种方法，因为它不需要程序员捕捉所有不可接受的字符，从而没有错误余地。推荐的方法只需程序员确认可接受字符被识别出来；因此，程序员可以较少担心攻击者可能尝试用于绕过安全检查的字符。

基于这一概念，前面介绍的 `whois.pl` 程序可以被净化，使其*仅*包含允许的字符；例如：

```perl
#!/usr/bin/perl -w
#
# Purpose: This is a better version of the previous
# whois.pl script.
#
# Assign a variable the acceptable character
# set for domain names.
#
my $DOMAIN_CHAR_SET="-a-zA-Z0-9_.";

# Get the domain name from query string
# environment variable.
#
my $domain = $ENV{'QUERY_STRING'};

# Now remove any character that does not
# belong to the acceptable character set.
#
$domain =~ s/[^$DOMAIN_CHAR_SET]//g;

# Print the appropriate content type.
# Because whois output is in plain text, we
# choose to use text/plain as the content-type here.
#
print "Content-type: text/plain\n\n";

# Here is the system call:
system("/usr/bin/whois $domain");

# Here is another system call using back-ticks:
#
# my $output = `/usr/bin/whois $domain`;
#
# print $output;

exit 0;
```

`$DOMAIN_CHAR_SET` 变量保存了可接受的字符集，而用户输入变量 `$domain` 会被搜索，任何不属于该集合的内容都会被移除。不可接受的字符将被删除。

处理用户输入的最佳方法是针对每个输入建立规则（即，您期望什么以及如何确定所接收的内容是可接受的）。例如，如果您期望输入是一个电子邮件地址（而不是盲目地扫描 shell 元字符），可以使用如下正则表达式来检测输入作为潜在电子邮件地址的有效性：

```perl
$email = param('email-addr');
if ($email =~ /^[\w-]+@[\w-]+$/) {
    print "Possibly valid address.\n";
}
else {
    print "Invalid email address.\n";
}
```

仅仅净化用户输入是不够的。您需要小心调用外部程序的方式（例如，在 Perl 中有许多调用外部程序的方法）。其中一些方法包括使用反引号捕获外部程序的输出，例如：

```perl
$list = `/bin/ls -l /etc`;
```

这会捕获 /etc 目录的列表。或者，您可以向程序打开一个管道，例如：

```perl
open (FP, " | /usr/bin/sort");
```

您也可以调用外部程序并使用 `system()` 等待其返回：

```perl
system "/usr/bin/lpr data.dat";
```

或者您可以调用外部程序且永远不返回，使用 `exec()`：

```perl
exec "/usr/bin/sort < data.dat";
```

如果这些构造涉及可能包含 shell 元字符的用户输入，它们都是危险的。对于 `system()` 和 `exec()`，有一个较为晦涩的语法特性，使您可以直接调用外部程序，而不必通过 shell。如果您将外部程序的参数作为列表中的独立元素传递，而不是作为一个长字符串传递，Perl 将不通过 shell，shell 元字符将不会产生任何不想要的副作用。例如：

```perl
    system "/usr/bin/sort", "data.dat";
```

您可以利用此特性在不通过 shell 的情况下打开管道。调用字符序列 `|` 会 fork 一个 Perl 副本并打开到该副本的管道。然后，子副本立即使用 `exec` 函数调用的第一个参数 fork 另一个程序。

要在不打开 shell 的情况下从管道读取，您可以对序列 `-|` 做类似的操作：

```perl
    open(GREP, "-|") || exec "/usr/bin/grep", $userpattern, $filename;
    while (<GREP>) {
        print "match: $_\n";
    }
    close GREP;
```

这些 `open()` 的形式比管道 `open()` 更安全，因此，只要可能，您应该使用这些形式。

请注意，Perl 中还有许多其他晦涩的特性，使您可以调用外部程序并对它关于其名称进行欺骗。这对于调用根据调用名称表现不同的程序非常有用。语法如下：

```perl
    system $real_name, "fake_name", "argument1", "argument2";
```

恶意用户使用的一种技巧是修改 `PATH` 环境变量，使其指向他们希望您的脚本执行的程序，而不是您预期的程序。您应该使用完整路径名来调用程序，而不是依赖 `PATH` 环境变量。也就是说，不要使用这段 Perl 代码片段：

```perl
    system("cat /tmp/shopping.cart.txt");
```

而应使用这个：

```perl
    system "/bin/cat", "/tmp/shopping.cart.txt";
```

如果您必须依赖 `PATH` 变量，请在 CGI 脚本的开头自行设置它，如下所示：

```perl
    $ENV{'PATH'}="bin:/usr/bin:/usr/local/bin";
```

即使您在调用外部程序时不依赖 PATH 变量，调用的程序也可能依赖它；因此，当您使用污点检查时，需要在脚本顶部附近包含上一行代码。您需要调整该行的目录列表以反映您希望搜索的目录。此外，一般来说，将当前目录（`.`）放入路径中不是一个好主意。

## 封装 CGI 脚本

减少与 CGI 相关风险的最好方法是根本不要运行任何 CGI 脚本；然而，在动态 Web 内容的时代，这是不现实的。或许您可以将所有 CGI 脚本集中到一个位置，并密切监控其开发，以确保它们编写良好。

在许多情况下，特别是在 ISP 系统上，所有拥有 Web 站点的用户都希望拥有 CGI 访问权限。在这种情况下，以拥有 CGI 脚本的用户 ID (UID) 来运行 CGI 脚本可能是一个好主意。默认情况下，Apache 运行的 CGI 脚本使用 Apache 的 UID。如果您使用所有者的 UID 来运行这些应用程序，所有可能的损害将限制在 UID 允许访问的范围内。换言之，使用非 Apache 服务器 UID 运行的不良 CGI 脚本只能损害该用户的文件。负责 CGI 脚本的用户会更加小心，因为可能的损害将仅影响其内容。一举两得，您增加了用户责任感和意识，同时限制了潜在损害的波及范围。要使用非 Apache 服务器用户的 UID 运行 CGI 脚本，您需要一种称为*包装器*（wrapper）的特殊类型程序，它使您能够以文件所有者的身份而非 Apache 服务器用户的身份运行 CGI 脚本。一些 CGI 包装器在运行请求的 CGI 脚本之前还会执行其他安全检查。以下部分讨论两个流行的 CGI 包装器。

### suEXEC

Apache 附带一个名为 suEXEC 的支持应用程序，它提供 Apache 用户在不同于 Apache UID 的 UID 下运行 CGI 和 SSI 程序的能力。suEXEC 是一个 setuid 包装器程序，当管理员指定以非 Apache 服务器 UID 运行 CGI 或 SSI 程序并发起 HTTP 请求时被调用。当此类请求发出时，Apache 提供程序名称、UID 和 GID 给 suEXEC 包装器。suEXEC 使用给定的 UID 和 GID 运行程序。

在运行 CGI 或 SSI 命令之前，suEXEC 包装器执行一系列测试以确保请求有效。除其他事项外，此测试过程确保 CGI 脚本由被允许运行包装器的用户所有，并且 CGI 目录或 CGI 脚本除所有者外对任何人都不可写。安全检查成功后，suEXEC 包装器分别通过 setuid 和 setgid 调用，将 UID 和组 ID (GID) 更改为目标 UID 和 GID。组访问列表也通过该用户所属的所有组进行初始化。suEXEC 通过建立安全的执行 PATH（在配置期间定义）以及仅传递……来清理进程的环境


那些变量名称列在安全环境列表（同样在配置过程中创建）中的变量。然后，suEXEC 进程将成为目标 CGI 脚本或 SSI 命令并执行。这看起来工作量很大——确实如此——但这同样提供了很高的安全系数。

## 配置和安装 suEXEC

如果您对在 Apache 中安装 suEXEC 支持感兴趣，请按照以下运行 `configure`（或 `config.status`）脚本：

```
./configure --prefix=/path/to/apache \
    --enable-suexec \
    --suexec-caller=httpd \
    --suexec-userdir=public_html\
    --suexec-uidmin=100 \
    --suexec-gidmin=100
    --suexec-safepath="/usr/local/bin:/usr/bin:/bin"
```

以下是此配置的详细说明：

-   - `--enable-suexec`：启用 suEXEC 支持。
-   - `--suexec-caller=httpd`：将 httpd 更改为您在 Apache 配置文件中使用 *User* 指令时所用的 UID。这是唯一被允许运行 suEXEC 程序的用户。
-   - `--suexec-userdir=public_html`：定义用户主目录下存放 suEXEC 可执行文件的子目录。将 *public_html* 更改为您用作 *UserDir* 指令的值，该指令指定了用户 Web 站点的文档根目录。
-   - `--suexec-uidmin=100`：定义允许运行基于 suEXEC 的 CGI 脚本的最低 UID。换句话说，低于此数字的 UID 无法通过 suEXEC 运行 CGI 或 SSI 命令。查看您的 `/etc/passwd` 文件，确保所选范围不包含通常位于 100 以下的系统账户 UID。
-   - `--suexec-gidmin=100`：定义允许作为目标组的最低 GID。换句话说，低于此数字的 GID 无法通过 suEXEC 运行 CGI 或 SSI 命令。查看您的 `/etc/group` 文件，确保所选范围不包含通常位于 100 以下的系统账户组 GID。
-   - `--suexec-safepath="/usr/local/bin:/usr/bin:/bin"`：定义 suEXEC 为 CGI 脚本和 SSI 命令执行的 PATH 环境变量。

## 启用和测试 suEXEC

安装 suEXEC 包装器和新的 Apache 可执行文件到正确位置后，重启 Apache，它将写入类似以下的消息：

`[notice] suEXEC mechanism enabled (wrapper: /usr/local/sbin/suexec)`

这告诉您 suEXEC 已处于活动状态。现在，测试 suEXEC 的功能。在 `httpd.conf` 文件中，添加以下行：

```
UserDir public_html
AddHandler cgi-script .pl
```

第一个指令（UserDir）将用户 Web 站点的文档根设置为 `~username/public_html`，其中 username 可以是系统上的任何用户。第二个指令将 cgi-script 处理程序与 .pl 文件关联起来。这样做是为了让扩展名为 .pl 的 Perl 脚本可以作为 CGI 脚本运行。对于此测试，您需要一个用户账户。在这个示例中，我使用主机 wormhole.nitec.com 和一个名为 kabir 的用户。将清单 18-4 中显示的脚本复制到名为 test.pl 的文件中，并将其放入用户的 public_html 目录中。在我的情况下，我将文件放在 `~kabir/public_html` 目录中。

### 清单 18-4：用于测试 suEXEC 支持的 CGI 脚本

```perl
#!/usr/bin/perl
#
# Make sure the preceding line is pointing to the
# right location. Some people keep perl in
# /usr/local/bin.

my ($key,$value);
  print "Content-type: text/html\n\n";
  print "<h1>Test of suEXEC<h1>";

  foreach $key (sort keys %ENV){
    $value = $ENV{$key};
    print "$key = $value <br>";
  }

  exit 0;
```

要通过 Web 浏览器访问该脚本，我请求以下 URL：http://wormhole.nitec.com/~kabir/test.pl。

CGI 脚本只有在通过 suEXEC 执行的所有安全检查后才会被执行。suEXEC 还会在其日志文件中记录脚本请求。我的请求的日志条目如下所示：

`[2001-03-29 16:00:22]: uid: (kabir/kabir) gid: (kabir/kabir) cmd: test.pl`

如果您真的想知道脚本是否在用户的 UID 下运行，请在 `foreach` 循环内部插入一个 sleep 命令（例如 `sleep(10)`），这将减慢执行速度，并允许您在 Web 服务器控制台上运行诸如 `top` 或 `ps` 之类的命令来了解运行 test.pl 的进程的 UID。您也可以通过使用 `chown` 命令更改脚本的所有权；在更改所有权后，尝试通过 Web 浏览器访问该脚本，并查看 suEXEC 记录的错误消息。例如，当我将 `~kabr/public_html` 目录中 `test.pl` 脚本的所有权更改为如下：

```
chown root test.pl
```

我收到了服务器错误，日志文件显示了以下行：

```
[2001-03-29 16:00:22]: uid/gid (500/500) mismatch with directory (500/500) or program (0/500)
```

在这里，程序的所有者是 UID 0，组仍然是 `kabr`（500），因此 suEXEC 拒绝运行它，这意味着 suEXEC 正在执行其应有的功能。

为了确保 suEXEC 在其他目录中也能运行 `test.pl`，我在 `~kabr/public_html` 中创建了一个 `cgi-bin` 目录，并将 `test.cgi` 放入该目录中。在确定新目录和文件的用户和组所有权已设置为用户 ID `kabr` 和组 ID `kabr` 之后，我使用以下命令访问了脚本：

```
http://wormhole.nitec.com/~kabr/cgi-bin/test.pl
```

如果您有虚拟主机并希望使用 suEXEC 运行 CGI 程序和/或 SSI 命令，则必须使用 `<VirtualHost . . .>` 容器内部的 User 和 Group 指令。将这些指令设置为不同于 Apache 服务器当前使用的用户和组 ID。如果仅为一个或一个都没有指定这些指令，则假定使用服务器用户 ID 或组 ID。

出于安全和效率原因，所有 suEXEC 请求必须保持在虚拟主机请求的一级文档根或 userid 请求的一个一级个人文档根内部。例如，如果您配置了四个虚拟主机，您需要将所有虚拟主机文档根构建在一个主要的 Apache 文档层次结构之上，以便为虚拟主机利用 suEXEC。

## CGIWrap

CGIWrap 与 suEXEC 程序类似，因为它允许用户在不损害 Web 服务器安全性的情况下使用 CGI 脚本。CGI 程序以文件所有者的权限运行。此外，CGIWrap 对 CGI 脚本进行多项安全检查，如果任何检查失败则不执行。

Nathan Neulinger 编写了 CGIWrap；CGIWrap 的最新版本可以从主要 FTP 站点 `ftp://ftp.cc.umr.edu/pub/cgi/cgiwrap/` 获取。CGIWrap 通过 HTML 文档中的 URL 使用。在分发状态下，CGIWrap 被配置为运行位于 `~/public_html/cgi-bin/` 目录中的用户脚本。

CGIWrap 以 gzip 压缩的 tar 文件形式分发。您使用 `gzip` 解压缩它，并使用 `tar` 实用程序提取它。

运行 `Configure` 脚本，它会提示您回答许多问题。这些问题中大多数都是不言自明的。还要注意，此包装器中有一个功能与 suEXEC 不同。它允许您创建 allow 和 deny 文件，可用于限制对您的 CGI 脚本的访问。这两个文件都具有相同的格式，如下所示：

```
User ID
mailto:Username@subnet1/mask1,subnet2/mask2...
```

您可以只有一个用户名（非数字 UID）或一个用户 `mailto:ID@subnet/mask` 行，其中可以定义一个或多个子网/掩码对。例如，如果在 allow 文件中（您指定文件名）找到以下行：

```
mailto:kabir@192.168.1.0/255.255.255.0
```

用户 kabir 的 CGI 脚本允许属于 192.168.1.0 网络且子网掩码为 255.255.255.0 的主机运行。

运行 `Configure` 脚本后，您必须运行 `make` 实用程序以创建 CGIWrap 可执行文件。

要使用包装器应用程序，请将 CGIWrap 可执行文件复制到用户的 `cgi-bin` 目录。此目录必须与您配置过程中指定的目录匹配。启动的最简单方法是保持 `~/username/public_html/cgi-bin` 类型的目录结构作为 CGI 脚本目录。

复制 CGIWrap 可执行文件后，按如下方式更改所有权和权限位：

```
chown root CGIWrap
chmod 4755 CGIWrap
```

在 `cgi-bin` 目录中，创建名为 `nph-cgiwrap`、`nph-cgiwrapd` 和 `cgiwrapd` 的三个硬链接或符号链接指向 CGIWrap，如下所示：

```
ln [-s] CGIWrap cgiwrapd
ln [-s] CGIWrap nph-cgiwrap
ln [-s] CGIWrap nph-cgiwrapd
```





在我的 Apache 服务器上，我仅将 cgi 扩展名指定为 CGI 脚本；因此，我将 CgiWrap 可执行文件重命名为 cgiwrap.cgi 以使其正常工作。如果你也有类似的限制，可以尝试这种方法，或者创建一个链接。

现在，按照以下方式执行 CGI 脚本：

```
http://www.yourdomain.com/cgi-bin/cgiwrap/username/scriptname
```

例如，要访问 wormhole.nitec.com 网站上用户 kabir 的 CGI 脚本 test.cgi，我会使用以下地址：

```
http://wormhole.nitec.com/cgi-bin/cgiwrap/kabir/test.cgi
```

如果你想查看 CGI 的调试输出，请指定使用 cgiwrapd 而不是 cgiwrap，如下面的 URL 所示：

```
http://www.yourdomain.com/cgi-bin/cgiwrapd/username/scriptname
```

如果该脚本是 nph 风格的脚本，你必须使用以下 URL 来运行它：

```
http://www.yourdomain.com/cgi-bin/nph-cgiwrap/username/scriptname
```

## 隐藏关于 CGI 脚本的线索

当破坏者扫描网站以寻找可能的安全漏洞时，他们会寻找那些能揭示网站底层硬件和软件的小细节。因此，你提供的系统线索越少，你的网站成为破坏者下一个受害者的可能性就越低。有几种方法可以隐藏一些可能成为重要线索的细节。

### 使用非标准的脚本别名

使用 cgi-bin 别名非常流行。一旦看到带有 cgi-bin 的 URL，你就知道该网站运行某种 CGI 脚本。此别名是在 Apache 的 httpd.conf 文件中通过 ScriptAlias 指令设置的。例如：

```
ScriptAlias "/cgi-bin/" "/path/to/real/cgi/directory/"
```

但很少有人意识到，你可以使用任何内容来创建这样的别名。例如：

```
ScriptAlias "/apps/" "/path/to/real/cgi/directory/"
```

现在，URL 中的 apps 起到了与 cgi-bin 相同的作用。因此，如果你使用类似于以下的内容：

```
ScriptAlias "/dcon/" "/path/to/real/cgi/directory/"
```

这无疑会混淆一些破坏者，因为 dcon（或者你实际使用的任何名称）是非标准的。此外，请记住许多破坏者使用自动程序来扫描网站的功能和其他线索。像上面这样的非标准脚本别名不太可能被纳入任何自动程序中。

## 为 CGI 脚本使用无扩展名名称

许多网站大胆地展示它们运行什么类型的 CGI 脚本。例如：

```
http://www.domain.com/cgi-bin/show-catalog.pl
```

上述 URL 提供了关于该网站的两个线索。首先，它告诉我们该网站支持 CGI 脚本；其次，该网站将 Perl 脚本作为 CGI 脚本运行。如果上述网站改为使用：

```
http://www.domain.com/ext/show-catalog
```

则更难确定该网站的任何信息。应避免使用 .pl 或 .cgi 扩展名，因为这些扩展名会提供有关你系统的线索。要将现有脚本的扩展名从 .pl、.cgi 等更改为无扩展名，只需重命名脚本即可。切换到无扩展名名称时，你不需要更改或添加任何新的 Apache 配置。

与 CGI 脚本类似，SSI 脚本也带来一些安全风险。下文将对此进行讨论。

## 使用 CGI 扫描器

CGI 扫描器用于扫描 Web 服务器中与 CGI 脚本相关的漏洞。我喜欢两个扫描器：cgichk.pl 和 Whisker。

### cgichk.pl

这是一个用 Perl 编写的简单 CGI 扫描器。你可以从 www.packetstormsecurity.com 下载源代码。使用 `perl cgichk.pl` 命令从命令行运行时，它会要求你输入要扫描的 Web 服务器的主机名和端口号（默认 80）。你还可以选择将结果记录到文件中。

cgichk.pl 首先检查 Web 服务器使用的 HTTP 协议版本。例如，以下示例会话显示 cgichk.pl 正在扫描名为 rhat.nitec.com 的主机。

```
CGI scanner [in Perl] v1.1
Host: rhat.nitec.com
HTTP Port [80]:
Log Session? (y/n)
Log File [rhat.nitec.com.scan]:
```

```
Press [Enter] to check the httpd version...

HTTP/1.1 200 OK
Date: Tue, 27 Mar 2001 04:50:47 GMT
Server: Apache/2.0.14 (Unix)
Last-Modified: Mon, 26 Mar 2001 20:23:13 GMT
ETag: "1ba42-1000-c65eee40"
Connection: close
Content-Type: text/html; charset=ISO-8859-1
```

检测到协议版本后，cgichk.pl 将要求你按回车键以开始检查 CGI 漏洞。以下输出是在运行 Apache 2.0 的 rhat.nitec.com Web 服务器上扫描 CGI 安全问题的示例。

```
Searching for /cgi/ - backdoor    : Not Found
Searching for /TC - backdoor       : Not Found
Searching for phf                  : Not Found
Searching for Count.cgi            : Not Found
Searching for test.cgi             : Not Found
Searching for nph-test-cgi         : Not Found
Searching for nph-publish          : Not Found
Searching for php.cgi              : Not Found
Searching for handler              : Not Found
Searching for webgais              : Not Found
Searching for websendmail          : Not Found
Searching for webdist.cgi          : Not Found
Searching for faxsurvey            : Not Found
Searching for /htmlscript          : Not Found
Searching for /per/displpay        : Not Found
Searching for perl.exe             : Not Found
Searching for wwwboard.pl          : Not Found
Searching for www-sql              : Not Found
Searching for /view-source         : Not Found
Searching for campas               : Not Found
Searching for /gl1mpse             : Not Found
Searching for gl1mpse              : Not Found
Searching for /nirw.man.sh         : Not Found
Searching for AT-admin.cgi         : Not Found
Searching for /filenaill.pl        : Not Found
Searching for /mailist.pl          : Not Found
Searching for /jj                  : Not Found
Searching for info2www             : Not Found
Searching for /files.pl            : Not Found
Searching for finger               : Not Found
Searching for /bninorm.cgi         : Not Found
Searching for /survey.cgi          : Not Found
Searching for /AnycForm2           : Not Found
Searching for txtcounter.pl        : Not Found
Searching for /classfields.cgi     : Not Found
Searching for /eniron.cgi          : Not Found
Searching for /wrup                : Not Found
Searching for /cglwrap            : Not Found
Searching for guestbook.cgi        : Not Found
```

```
Searching for edit.pl : Not Found
Searching for perlshop.cgi : Not Found
Searching for anyboard.cgi : Not Found
Searching for webbbs.cgi : Found!
Searching for environ.cgi : Not Found
Searching for whois_raw.cgi : Not Found
Searching for _vti_inf.html : Not Found
Searching for service.pwd : Not Found
Searching for users.pwd : Not Found
Searching for authors.pwd : Not Found
Searching for administrators : Not Found
Searching for shtml.dll : Not Found
Searching for shtml.exe : Not Found
Searching for args.bat : Not Found
Searching for uploader.exe : Not Found
Searching for rguest.exe : Not Found
Searching for wguest.exe : Not Found
Searching for bd1r - samples : Not Found
Searching for CGImail.exe : Not Found
Searching for newsn.exe : Not Found
Searching for fpcount.exe : Not Found
Searching for counter.exe : Not Found
Searching for visadmin.exe : Not Found
Searching for openfile.cfm : Not Found
Searching for expcalc.cfm : Not Found
Searching for disposedfile : Not Found
Searching for sendmail.cfm : Not Found
Searching for codebrws.asp : Not Found
Searching for codebrws.asp 2 : Not Found
Searching for showcode.asp : Not Found
Searching for search97.vts : Not Found
Searching for carco.dll : Not Found
Server may have CGI vulnerabilities.
```

注意加粗的那一行。扫描发现了一个潜在的 CGI 安全风险。webbbs.cgi 脚本可能被脚本小子和想当黑客的人滥用来入侵系统。如果你的扫描识别出一个或多个安全风险，请考虑删除这些脚本或使用适当的修复方法更新它们。

### Whisker

Whisker 是一个基于 Perl 的 CGI 扫描器，我非常喜欢它。你可以从 www.filesearch.ru 下载源发行版。下载后，在目录中提取源代码，并运行 whisker.pl 脚本，命令为 `perl whisker.pl -h hostname`。例如，`perl whisker -rh at.nitec.com` 命令会在名为指定主机的 Apache Web 服务器上运行扫描器。结果如下所示：

```
Host: rhat.nitec.com
= Server : Apache/2.0.14 (Unix)
+ 200 OK: HEAD /cgi-bin/webbbs.cgi
+ 200 OK: HEAD /manual/
+ 200 OK: HEAD /temp/
```




有趣的是，扫描输出使用 HTTP 状态码（如 200、303、403 和 404）来指示安全风险。例如，上述扫描结果显示在该服务器上发现了三个潜在风险（200）。如果你需要更多信息，请运行带有 `-i` 和 `-v` 选项的 whisker。例如，`perl whister.pl -h www.domain.com -i -v` 命令会在 www.domain.com 上运行它。以下是一个扫描输出的示例：

```
============
= Host: www.domain.com
- Directory index: /

= Server: Apache/1.3.12 (Unix) mod_oasis/5.1/

- www.apache.org
+ 302 Found: GET /scripts/
+ 403 Forbidden: GET /cgi-bin/
+ 200 OK: HEAD /cgi-bin/upload.pl
+ 403 Forbidden: HEAD /~root/
+ 403 Forbidden: HEAD /apps/
+ 200 OK: HEAD /shop/
+ 200 OK: HEAD /store/
```

请注意，有几行 200 OK，这意味着存在可利用的资源；403 表示对可利用资源的访问被拒绝，但该资源仍然存在——这既是好事也是坏事。说是好事，是因为按照服务器当前的配置，该可利用资源无法访问；但说它是坏事，是因为如果未来配置发生变化，该可利用资源可能会变得可用，这就是为什么 403 既是好消息也是坏消息。302 行表示误报。这是因为许多服务器被配置为在请求的 URL 缺失时返回自定义错误消息，从而生成 302 HTTP 状态码。

你还可以使用 -I n（其中 n = 0 到 9）选项来启用规避模式，以绕过 Web 服务器上的入侵检测系统（IDS）。如果你使用任何 IDS 解决方案，也可以测试你的 IDS 的有效性。例如，如果你的 IDS 知道 /cgi-bin/php（一种已知的 CGI 风险），那么使用 -I 1 将尝试欺骗你的 IDS，使其使用 URL 编码，从而将 /cgi-bin/php 请求以编码 URL 的形式发送，而不是直接在请求中使用 /cgi-bin/php。类似地，-I 2 将尝试通过在 URL 中使用额外的 ../ 模式来混淆 IDS。有关详细信息，请不带任何参数运行 whisker。

## 降低 SSL 风险

如果你使用 SSL 运行外部应用程序，例如使用 exec 命令，那么安全风险与 CGI 脚本几乎相同。然而，在 Apache 下你可以使用 Options 指令非常轻松地禁用此命令，如下所示：

```
<Directory />
    Options IncludesNOEXEC
</Directory>
```

这会在你的整个 Web 空间中禁用 `exec` 和包含 SSI 命令；但是，你可以通过定义范围更窄的目录容器来在需要时启用这些命令，例如：

```apache
<Directory />
    Options IncludesNOEXEC
</Directory>

<Directory "/ssi*">
    Options +Includes
    SetOutputFilter INCLUDES
</Directory>
```

此配置片段在全局范围内禁用了 `exec` 命令，但在 `/ssi` 目录中除外。

还要避免使用 `printenv` 命令，该命令会打印出所有现有环境变量及其值。例如，命令：

```bash
<--#printenv -->
```

会显示 Web 服务器可用的所有环境变量。在可公开访问的页面上显示此类信息肯定会为破坏者提供线索。因此，仅在调试 SSI 调用时使用此命令，而在生产环境中不要使用。

为了确保 Web 安全，你需要做出许多配置和政策决策（允许什么以及如何允许）。在实施了一系列安全措施后，许多人感到沮丧，因为他们不知道还需要做什么来进一步增强安全性。在实施了诸如前面提到的受控 CGI 和 SSI 请求等措施之后，你应该将精力集中在日志记录上。

# 第 19 章

## 使用 SSL 保护 Apache

就在几年前，互联网仍然是它最初设想的那样——一个面向科学家和工程师的全球网络。然而，借助 Web，互联网现在已成为面向所有人的网络。如今，似乎每个人和每件事都在互联网上。它也是新经济的前沿；成千上万家大小企业都建立了电子商务网站，以向世界各地的客户敞开大门。然而，客户们变得谨慎起来，因为他们知道并非互联网的所有部分都是安全的。

为了消除这种在*新前沿*中的不安全感，Netscape Communications（现为 AOL Time Warner 的子公司）发明了一种安全协议，确保客户 Web 浏览器与 Web 服务器之间的安全事务。Netscape 将该协议命名为安全套接字层（SSL）。很快，SSL 在许多其他互联网应用程序中找到了位置，如电子邮件、远程访问等。由于 SSL 现在是现代计算机安全基础设施的基础部分，因此了解如何将 SSL 集成到你的 Apache 服务器中是很重要的。

Apache 默认不附带任何 SSL 支持。但是，你可以为 Apache 编译和安装一个 SSL 模块以启用 SSL 功能。针对 Apache，有两种开源解决方案可用：`mod_ssl` 和 Apache-SSL。这两种解决方案都使用一种名为 OpenSSL 的 SSL 开源实现。在本章中，我将讨论如何编译和安装 OpenSSL，然后使用 `mod_ssl` 或 Apache-SSL 设置 Apache。

### 介绍 SSL

使用对称和非对称加密方案（在本章后面“理解加密”一节中有描述），Netscape 开发了一种开放的、非专有协议，称为安全套接字层（SSL），用于为基于 TCP/IP 的通信提供数据加密、服务器身份验证、数据完整性和客户端身份验证。图 19-1 展示了 SSL 如何与应用交互。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_574_0.png)

SSL 协议运行在 TCP/IP 之上，低于更高级的应用层协议，如 HTTP、FTP、IMAP 等。它代表应用层协议使用 TCP/IP，在此过程中允许启用了 SSL 的服务器向启用了 SSL 的客户端进行身份验证，允许客户端向服务器进行身份验证，并允许两台机器建立加密连接。下一节提供了对 SSL 工作原理的更近距离但简化的观察。

### SSL 如何工作

SSL 的基础是加密。SSL 定义了用于保护网络通信的加密类型和使用方式。在接下来的各节中，我将讨论不同的加密类型及其在 SSL 中的应用。

### 理解加密

当数据从互联网的一个点传输到另一个点时，它会经过多个计算机，如路由器、网关和其他网络设备。例如，当访问 www.nitec.com 网站的用户在该网站的 HTML 表单中输入其或她的信用卡号时，该信息很可能沿着与图 19-2 所示类似的路径传输。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_575_0.png)

**图 19-2：** 数据在互联网上从一个点传输到另一个点。

从图中可以看出，数据必须通过许多节点，因此有可能被其中一个节点上的某人拦截。虽然数据包的传输速度非常快（通常以毫秒计），但拦截仍然是一种可能性。这就是为什么我们需要一种安全的机制来交换敏感数据。这种安全性是通过加密实现的。

从技术上讲，*加密* 是一种数学编码方案，确保只有预期的接收者才能访问数据；它向窃听者隐藏数据。加密方案被广泛用于限制对资源的访问。例如，当你登录 Unix 或 Windows 2000/NT 系统时，你使用的密码或密钥通常以加密格式存储在服务器计算机中。在大多数 Unix 系统中，用户的密码被加密，并与存储在 `/etc/passwd` 文件中的加密密码进行匹配。如果此比较成功，用户将被授予对所请求资源的访问权限。

- **对称加密：** 此方案类似于你日常生活中可能使用的钥匙和锁。你用钥匙解锁汽车，并用同一把钥匙锁上它。同样，在对称加密中，单个密钥用于锁定和解锁目的。图 19-3 展示了此类方案的一个示例。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_576_0.png)

**图 19-3：** 对称加密方案的示例。

由于在此方案中使用了单个密钥，因此所有参与方都必须知道此密钥是什么才能使方案生效。

- **非对称加密：** 顾名思义，非对称加密的工作方式与对称加密略有不同。在此方案中，有两个密钥：一个公钥和一个私钥。额外的密钥是公钥——因此该方案也被称为公钥加密。图 19-4 展示了此加密方案工作原理的示例。




## 非对称加密原理

如图所示，当数据使用公钥加密时，只能使用私钥进行解密，反之亦然。与对称加密不同，这种方案不要求发送方知道接收方解锁数据所需的私钥。公钥被广泛分发，因此任何希望发起安全数据通信的人都可以使用它。私钥从不分发；它必须始终保密。

## 理解证书

*证书*是加密信息，它将公钥与个人、服务器或其他实体（称为主题）的真实身份关联起来。它还包含证书颁发机构的识别信息和签名。颁发机构被称为证书颁发机构（Certificate Authority, CA）。此类证书可能包含其他信息，如序列号、证书有效的时间段等，这有助于 CA 管理证书。使用支持 SSL 的 Web 浏览器，如 Netscape Navigator 和 Microsoft Internet Explorer，您可以很容易地查看服务器证书。证书中被标识的实体使用 X509 标准中定义的区分名（distinguished name）字段来表示。表 19-1 显示了证书中的区分名字段。

### 表 19-1

**表 19-1：区分名字段**

| DN 字段 | 缩写 | 含义 |
| :--- | :--- | :--- |
| 通用名 (Common Name) | CN | 被认证实体的名称 |
| 组织或公司 (Organization or Company) | O | 该实体与此组织有关联 |
| 组织单位 (Organizational Unit) | OU | 该实体与此组织单位有关联 |
| 城市/地区 (City/Locality) | L | 该实体位于此城市 |
| 州/省 (State/Province) | ST | 该实体位于此州或省 |
| 国家 (Country) | C | 位于此国家（2位 ISO 国家代码） |

证书通常以二进制或编码文本格式传输。

## 基于证书的事务

在基于 SSL 的事务中，如图 19-5 所示，服务器向客户系统发送证书。

一个众所周知的供应商，即证书颁发机构（CA），通常会颁发证书。证书使用证书颁发机构的私钥进行加密。客户端使用证书颁发机构的公钥解密证书。

由于证书包含服务器的公钥，客户端现在可以解密服务器发送的任何加密数据。此时，服务器发送一段标识自身为证书中提到的实体的数据。然后，服务器创建之前用于标识自身的相同数据的摘要消息。该摘要使用服务器的私钥加密。现在，客户端拥有来自知名 CA 的证书（陈述服务器的公钥应该是多少）、来自服务器的身份消息以及该身份消息的加密摘要。

使用服务器的公钥，客户端可以解密摘要消息。然后客户端创建身份消息的摘要，并将其与服务器发送的摘要进行比较。如果匹配，则意味着服务器就是它声称的那个身份。为什么？嗯，服务器最初发送了由知名 CA 签名的证书，因此客户端完全确定这个公钥属于谁。然而，客户端需要证明服务器没有发送它声称身份的那个证书，因此服务器发送了一个简单的标识消息以及该相同消息的公钥加密摘要。如果服务器没有适当的私钥，它将无法生成客户端从标识消息计算出的相同摘要。

## SSL 事务示例

**图 19-5：** 一个 SSL 事务的例子。

如果这看起来是一件复杂的事情，确实如此——而且事情并没有到此结束。现在，客户端可以通过使用服务器的公钥加密对称加密密钥，将其发送给服务器。然后，服务器可以使用这个新密钥来加密数据并将其传输给客户端。为什么要这样做？嗯，事实证明，对称加密比非对称加密快得多。你可以这样看：非对称加密（私钥/公钥）用于安全地传输从客户端到服务器随机生成的对称密钥；该密钥随后用于提供快速、安全的通信通道。

如果冒牌货坐在客户和服务器系统之间，并且能够拦截传输的数据，它会造成损害吗？嗯，它不知道客户端和服务器使用的秘密对称密钥，因此无法确定数据的内容；然而，它可以通过向数据包中注入自己的数据来在数据中引入垃圾。

为了避免这种情况，SSL 协议允许使用消息认证码（MAC）。MAC 只是通过使用对称密钥和要传输的数据计算出来的一块数据。因为冒牌货不知道对称密钥，它无法计算正确的 MAC 值。例如，一种由 RSA Data Security, Inc. 开发的名为 MD5 的众所周知的加密摘要算法，可用于为每个要传输的数据包生成 128 位的 MAC 值。通过这种方式成功猜测正确的 MAC 值所需的计算能力和时间几乎是不存在的。SSL 使互联网上的安全商务成为可能。

## 定义证书颁发机构

CA 是一个为服务器和客户端（即用户）颁发证书的可信组织。要理解此类组织的必要性，请考虑以下场景。

客户端想要安全地访问你外网 Web 服务器上的 Web 应用程序。客户端使用 HTTPS 协议访问你的外网服务器，例如 `https://extranet.domain.com/login.srvlet`。

客户端的 Web 浏览器发起 SSL 连接请求。你的外网 Web 服务器使用其私钥加密它发送到客户端 Web 浏览器的数据，浏览器使用你的 Web 服务器的公钥解密数据。因为 Web 服务器还将公钥发送到 Web 浏览器，所以无法确定该公钥是否真实。换句话说，没有什么能阻止恶意计算机黑客拦截来自你外网服务器的信息并向你的客户端发送黑客的公钥。这就是 CA 发挥作用的地方。在核实了有关你公司的离线信息后，CA 会向你颁发证书。此服务器证书由 CA 自己的公钥签名，该公钥是众所周知的。在这种情况下，当 Web 浏览器收到服务器证书时，它可以使用众所周知的 CA 公钥解密证书信息。这确保了服务器证书的真实。然后，Web 浏览器可以验证真实证书中使用的域名与它正在通信的域名相同。

类似地，如果你需要确保客户端确实是它声称的那个身份，你可以实施客户端证书限制，这将使整个交易变成一个闭环的安全过程。

其思想是，如果每一方都有一个验证对方身份、确认公钥并由可信机构签名的证书，那么双方都能确保他们正在与其认为正在通信的对象进行通信。

有两种类型的证书颁发机构：商业 CA 和自认证私有 CA。

## 商业 CA

商业 CA 的主要工作是验证其他希望在互联网上建立真实性的商业或非营利公司。CA 通过检查各种法律记录（如官方公司注册文件或成立证书、公司高层管理人员的官方信函等）来验证公司的离线真实性，从而可以签署证书。只有少数几家商业 CA。Versign (www.versign.com) 和 Thawte (www.thawte.com) 是最知名的 CA。Versign 已经收购了 Thawte Consulting。

## 自认证、私有 CA

私有 CA 非常类似于根级别的商业 CA。它是自认证的。然而，私有 CA 通常用于 LAN 或 WAN 环境，或者用于实验 SSL。例如，一个通过 WAN 互连各部门的美国大学可能决定使用私有 CA 而不是商业 CA。只要你不期望未知用户信任你的私有 CA，你就可以使用它。在接下来的部分中，我将展示如何为你的组织创建私有 CA。之后，我将展示如何从商业 CA 获取证书，或者创建自己的 CA 来认证你的服务器和客户端。

## 为 Apache 设置 SSL

在使用 Apache 时，你有两个开源选择来使用 SSL。你可以使用 mod_ssl 模块或 Apache-SSL 发行版。这两种解决方案都需要 OpenSSL，它是 SSL 库的开源实现。在本节中，我将讨论如何为 Apache 设置 OpenSSL 以及 mod_ssl 和 Apache-SSL 解决方案。

## SSL 选择

OpenSSL 项目是一个开源社区协作，旨在开发商业级 SSL、传输层安全性（TLS）以及全强度通用密码学库包。SSL 的当前实现也称为 OpenSSL。OpenSSL 基于 Eric A. Young 和 Tim J. Hudson 开发的 SSLeay 库。OpenSSL 软件包许可证允许该软件自由用于商业和非商业用途。

有两个可自由使用的与 Apache 配合使用的 OpenSSL 软件包：

- 在 [www.apache-ssl.org](http://www.apache-ssl.org) 找到的基于 OpenSSL 的 Apache-SSL 补丁。
- 在 [www.modssl.org](http://www.modssl.org) 找到的基于 OpenSSL 的用于 Apache 的 mod_ssl 模块。

这两种选择都导致相同的功能。有些人喜欢 Apache-SSL，有些人喜欢 mod_ssl。它们都能工作，但在代码风格、文档和一些次要功能上有所不同。我倾向于 mod_ssl，因为我喜欢 Ralf S. Engelfall 的其他模块，如 mod_rewrite。




# 设置 OpenSSL

在 www.openssl.org 找到的 OpenSSL 包对于 Apache-SSL 和 mod_ssl 解决方案（用于为 Apache Web 服务器引入 SSL）都是必需的。在本节中，您将学习如何为您的 Unix 系统设置 OpenSSL。我使用 Linux 系统进行说明。OpenSSL 网站提供以 gzip 压缩的 tar 文件形式编译的 OpenSSL 源代码。撰写本文时的最新版本是 openssl-0.9.6.tar.gz。

## OpenSSL 先决条件

在开始编译过程之前，您必须确保您的系统满足 OpenSSL 的先决条件。OpenSSL 源代码发行版要求您拥有 Perl 5 和一个 ANSI C 编译器。本章假设在您设置 Linux 系统时已安装了 Perl 5 和 gcc（C 编译器）。

## 获取 OpenSSL

多年来，SSL 一直存在于商业 Linux 软件中，例如基于 Apache 的商业 Web 服务器 Stronghold。然而，由于某些专利和美国的出口限制，Linux 在很长一段时间内没有开源的 SSL 版本。Open SSL Project 现在提供 SSL 的 Linux 版本，您可以从官方 OpenSSL 网站 www.openssl.org/source 下载。

> **提示**  
> Red Hat Linux 发行版目前以 RPM 包形式提供 OpenSSL 二进制文件。因此，您可以使用 Red Hat Linux 提供的 RPM 版本，也可以下载源代码发行版进行编译和安装。

我倾向于从真实的 Web 或 FTP 站点下载源代码发行版来安装安全软件。我假设您也偏好这样做。因此，下面部分将讨论从 OpenSSL 网站下载的官方源代码发行版编译和安装 OpenSSL 的细节。

> **注意**  
> 如果您必须从 RPM 安装 OpenSSL，请使用可信赖的二进制 RPM 发行版，例如在官方 Red Hat CD-ROM 上找到的那个。要从 RPM 包安装 OpenSSL 二进制文件，请运行 `rpm -ihv openssl-packagename.rpm` 命令。

## 编译和安装 OpenSSL

编译 OpenSSL 是一项非常简单的任务；只需遵循以下步骤：

- 从控制台以 root 身份登录到 Linux 系统。
- 将 OpenSSL 源代码 tar 包复制到 `/usr/src/redhat/SOURCES` 目录。
- 通过运行 `tar xvzf openssl-version.tar.gz` 命令解压源代码发行版。例如，要解压 `openssl-0.9.6.tar.gz` 文件，请运行 `tar xvzf openssl-0.9.6.tar.gz` 命令。`tar` 命令会创建一个名为 `openssl-version` 的目录，在我的例子中是 `openssl-0.9.6`。
- 如果磁盘空间是个问题，此时您可以删除 tar 包。不过，我建议您在 OpenSSL 成功编译和安装后再删除它。
- 将当前目录更改为新创建的目录。

此时，请随意阅读发行版中包含的 README 或 INSTALL 文件。在编译软件之前，您应该配置安装选项。要在默认的 /usr/local/ssl 目录中安装 OpenSSL，请运行：

```bash
./config
```

但是，如果您必须将其安装在不同的目录中，请将 `--prefix` 和 `-openssldir` 标志附加到上述命令。例如，要在 `/opt/security/ssl` 目录中安装 OpenSSL，命令行如下：

```bash
./config --prefix=/opt/security
```

还有许多其他选项可以配合 `config` 或 `Configure` 脚本使用，以准备源代码发行版进行编译。这些选项在表 19-2 中讨论。

**表 19-2**  
**编译 OpenSSL 的配置选项**

| 配置选项 | 目的 |
| :-------------------- | :--------------------------------------------------------------- |
| `--prefix=DIR` | 将 OpenSSL 安装在 DIR 目录中。会创建如 DIR/lib、DIR/bin、DIR/include/openssl 等子目录。除非使用 -openssldir 选项指定该目录，否则配置文件将存储在 DIR/ssl 中。 |
| `--openssldir=DIR` | 指定配置文件目录。如果未使用 `--prefix` 选项，所有文件将存储在此目录中。 |
| `rsaref` | 此选项将强制构建 RSAREF 工具包。如果您希望使用 RSAREF 工具包，请确保您的默认库搜索路径中有 RSAREF 库（`librsaref.a`）。 |
| `no-threads` | 此选项禁用对多线程应用程序的支持。 |
| `threads` | 此选项启用对多线程应用程序的支持。 |
| `no-shared` | 此选项禁用创建共享库。 |
| `shared` | 此选项启用创建共享库。 |
| `no-asn` | 此选项禁用源代码树中汇编代码的使用。仅当您在编译 OpenSSL 时遇到问题时才使用此选项。 |
| `386` | 仅在您在 Intel 386 机器上编译 OpenSSL 时使用。不推荐用于较新的 Intel 机器。 |
| `no-<cipher>` | OpenSSL 使用许多加密算法，如 bf, cast, des, dh, dsa, hmac, md2, md5, mdc2, rc2, rc4, rc5, rsa 和 sha。如果您希望不在编译的二进制文件中包含特定的算法，请使用此选项。 |
| `-Dxxx, -Lxxx, -Ixxx, -fxxx, -Kxxx` | 这些选项允许您指定各种系统依赖选项，例如在命令行上指定的动态共享对象（DSO）标志，如 -fpic、-fPIC 和 -KPIC。这样，OpenSSL 库就可以使用位置无关代码（PIC）进行编译，这是将其链接到 DSO 中所需的。 |

您可能不需要添加这些选项来编译 OpenSSL。但是，如果您在编译时遇到问题，可能需要尝试使用适当的值来使用这些选项。例如，如果由于 OpenSSL 抱怨缺少库文件而无法编译，请尝试使用 -L 选项指定系统库路径。

在运行 config 脚本没有错误后，运行 make 实用程序。如果 make 命令成功，运行 `make test` 来测试新构建的二进制文件。最后，运行 `make install` 将 OpenSSL 安装到您的系统中。如果编译遇到问题，请尝试理解问题的原因。在大多数情况下，问题是在非常旧的 Linux 系统上尝试安装像 OpenSSL 这样最新版本的软件时，由库文件不匹配引起的。或者问题可能由您在命令行中指定的某个选项引起。例如，如果您的系统上没有安装 RSAREF 库（Red Hat Linux 发行版不包含该库），而您正试图使用 `rsaref` 选项，则在尝试构建二进制文件时编译将失败。因此，确保在使用特定选项时知道自己在做什么。如果您仍然无法解决问题，请尝试在 www.openssl.org/support/faq.html 的 OpenSSL FAQ 页面上搜索解决方案。或者，简单地安装 OpenSSL 的二进制 RPM 包。

## 为 SSL 支持选择 mod_ssl 模块

只有当选择不使用 Apache-SSL 来提供 SSL 支持时，您才应使用 mod_ssl。该模块可以作为 Apache 的 DSO 模块使用，并且也适用于 Windows 平台。

### 编译和安装 mod_ssl

要编译和安装此模块，请遵循以下步骤：

- 从 www.modssl.org 下载 `mod_ssl` 模块的最新源代码发行版。在某个目录中解压源代码。
- 以 root 身份运行 *Configure* 脚本，从新创建的 *mod_ssl-version* 目录中执行如下操作：
    ```text
    ./configure --with-apache=../httpd_version
    ```
    确保将 `../httpd_version` 替换为 Apache 源代码发行版目录的适当路径。例如，如果您将 `mod_ssl` 源代码安装在 `/usr/local/src/mod_ssl-2.9.0-2.0.19` 目录中，并将 Apache 源代码发行版安装在 `/usr/local/src/httpd_2.0.19` 目录中，则从 `/usr/local/src/mod_ssl-2.9.0-2.0.19` 目录运行以下命令：
    ```text
    ./configure --with-apache=../httpd_2.0.19
    ```
- 设置一个名为 `SSL_BASE` 的环境变量，指向系统中的 OpenSSL 目录。例如，如果您使用的是 *bash* shell，您可以运行 `export SSL_BASE=path_to_openssl`，其中 *path_to_openssl* 应替换为 OpenSSL 安装目录的实际路径。
- 转到顶层 Apache 源目录，并使用 `--enable-module=ssl` 选项以及 Apache 所需的其他常规选项运行 *configure* 脚本。如果您已经编译了 Apache，可以使用 `config.status --enable-module=ssl` 自动重用您之前的所有命令行选项。
    **提示** 如果您计划将 `mod_ssl` 作为共享模块使用，则在 *configure* 脚本中使用 `--with-apxs --enable-shared=ssl --enable-so` 而不是 `--enable-module=ssl`。
- 使用 *make* 命令编译和安装带有 `mod_ssl` 支持的 Apache 服务器。
- 如果您没有服务器证书，可以使用 *make certificate TYPE=dummy* 命令创建一个虚拟证书。
- 运行 *make install* 安装启用了 `mod_ssl` 的 Apache 服务器。如果您在步骤 6 中创建了服务器证书，它将被复制到 Apache 服务器安装路径的 *conf* 子目录中。
- 如果 Apache 正在运行，请使用 `/usr/local/bin/apachectl stop` 命令停止它，并使用 `/usr/local/bin/apachectl start ssl` 命令重新启动 Apache 以支持 HTTP[S 协议。



## 为基于 mod_ssl 的 SSL 配置 Apache

如果你已在之前构建过一次 Apache 之后，再编译带有 **mod_ssl** 的 Apache，那么 SSL 相关的配置指令将存储在 **httpd.conf.default** 中，而不是 **httpd.conf** 中。基本上，当你在现有的 Apache 服务器上添加 **mod_ssl** 时，**httpd.conf** 文件会被保留。你必须通过从 **httpd.conf.default** 中复制必要的信息来手动配置 SSL 相关指令。在以下内容中，我假设你正在按照上一节所示，通过重新编译支持 **mod_ssl** 的 Apache，将 **mod_ssl** 添加到现有的 Apache 系统中。要使用 **mod_ssl** 为 Apache 配置 SSL，请按照以下步骤操作：

- 1. 如果你将 **mod_ssl** 作为共享模块安装，请在 **httpd.conf** 中添加以下行：
  
  ```
  AddModule _ssl_module modules/libssl.so
  ```

- 2. 修改 **httpd.conf** 使其包含以下指令：
  
  ```
  <IfDefine SSL>
      Listen 80
      Listen 443
  </IfDefine>
  ```
  
  这个 **<IfDefine>** 容器告诉 Apache 仅在 Apache 使用 **-DSSL** 选项启动或使用了 **apachectl startssl** 时，才考虑其中的指令。在 SSL 模式下，Apache 被指示监听标准 **HTTP** 端口 80 上的连接，同时也监听标准 **HTTPS** 端口 443。

- 3. 在 **httpd.conf** 中添加以下行，以告知 Apache 为 **.crt** 和 **.crl** 扩展名添加两种 MIME 类型。第一种扩展名表示证书文件，第二种表示证书吊销列表（CRL）文件。这两行确保 Apache 在发送带有这些扩展名的文件时发送适当的头部信息。
  
  ```
  <IfDefine SSL>
      AddType application/x-x509-ca-cert .crt
      AddType application/x-pkcs7-crl .crl
  </IfDefine>
  ```

- 4. 在 **httpd.conf** 中添加以下行，以定义 SSL 会话缓存数据库路径、缓存超时值、SSL 启用子进程用于通信的 SSL 互斥文件路径、SSL 随机种子生成方法、SSL 日志路径以及 SSL 日志级别信息。
  
  ```
  <IfModule mod_ssl.c>

      SSLPassPhraseDialog builtin

      SSLSessionCache dbm:/usr/local/apache/logs/ssl_scache
      SSLSessionCacheTimeout 300

      SSLMutex file:/usr/local/apache/logs/ssl_mutex

      SSLRandomSeed startup builtin
      SSLRandomSeed connect builtin
      SSLLog /usr/local/apache/logs/ssl_engine_log
      SSLOgLevel info
  </IfModule>
  ```

- 5. 在 `httpd.conf` 中创建如下所示的兜底默认虚拟主机配置：

  ```
  <IfDefine SSL>
  <VirtualHost _default_:443>
  DocumentRoot path_to_ssl_document_root
  ServerName ssl_server_hostname

  SSLEngine on

  SSLCipherSuite
  ALL:+ADH:+EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP:+eNULL
  SSLCertificateFile conf/ssl.crt/server.crt
  SSLCertificateKeyFile conf/ssl.key/server.key
  </VirtualHost>
  </IfDefine>
  ```
  
  这个 `default_` 虚拟主机可以防止任何 SSL 请求（端口 443）被主服务器处理。它会捕获所有无法映射到 `httpd.conf` 中定义的其他任何虚拟主机的 SSL 请求。

  - 你应该将 `path_to_ssl_document_root` 更改为 SSL 服务器的适当文档根目录。你可以使用与你的 HTTP（端口 80）站点相同的文档根目录。
  - 服务器名称 `ssl_server_hostname` 需要根据实际情况进行设置。你可以为 HTTP 和 HTTPS 使用相同的主机名。
  - `SSLEngine` 指令为此虚拟主机启用 SSL 模块。
  - `SSLCipherSuite` 定义了此虚拟主机中可以使用的加密算法。
  - `SSLCertificateFile` 指令定义了服务器证书文件的路径。请确保该路径对于你的站点是正确的。
  - `SSLCertificateKeyFile` 定义了证书对应的密钥文件。同样，请确保在此处定义了正确的路径。

- 6. 如果你运行 `mod_perl` 脚本、CGI 脚本、SSI 或 PHP 页面，并且希望访问标准的 SSL/TLS 相关环境变量（以 `SSL_*` 为前缀），则必须明确指示 Apache 为 `mod_perl`、CGI、SSI 或 PHP 请求创建这些变量。使用 `SSLOptions +StdEnvVars` 来告知 Apache 为这些请求生成 `SSL_*` 环境变量。不过，最好在 `<File>` 容器中启用此选项，如下所示：
  
  ```
  <Files ~ "\.(pl|cgi|shtml|php)$">
      SSLOptions +StdEnvVars
  </Files>
  ```
  
  这里只为 `.pl`（Perl 脚本）、`.cgi`（典型 CGI 脚本）、`.shtml`（SSI 页面）或 `.php`（PHP 页面）的文件创建 `SSL_*` 环境变量。你可以将此 `<File>` 容器放在第 5 步中定义的虚拟主机内部。

- 7. 同样地，如果你使用标准的 `/cgi-bin/` 别名来访问 CGI 脚本，你可以使用以下 `<Directory>` 容器为其开启 `SSL_*` 环境变量创建功能：
  
  ```
  <Directory "physical_path_to_cgi_bin_directory">
      SSLOptions +StdEnvVars
  </Directory>
  ```
  
  请确保将 `physical_path_to_cgi_bin_directory` 替换为 CGI 目录的实际路径。

- 8. 使用 `/usr/local/apache/bin/apachectl startssl` 命令启动 Apache。

## 选择 Apache-SSL 而非 mod_ssl 用于 SSL 支持

可以从 www.apache-ssl.org 网站下载 Apache-SSL 源代码补丁包。Apache-SSL 源代码补丁包可将 Apache 转变为基于 SSLeay 或 OpenSSL 的 SSL 服务器。

### 编译和安装 Apache 的 Apache-SSL 补丁

你需要确保已在系统中安装了 OpenSSL。以下内容讨论如何编译和安装带有 Apache-SSL 补丁的 Apache。

以下内容假设你已在 `/usr/local/ssl` 目录中安装了 OpenSSL，并且已将 Apache 源代码树解压到 `/usr/local/src/http_version` 目录。例如，Apache 2.0.16 的源代码路径将为 `/usr/local/src/http_2.0.16`。要设置支持 SSL 的 Apache，请遵循以下步骤：

- 1. 以 root 身份进入 Apache 源代码分发目录（`/usr/local/src/http_version`）。
- 2. 将 Apache-SSL 补丁包（`apache_version+ssl_version.tar.gz`）文件复制到当前目录，并使用 `tar xvzf apache_version+ssl_version.tar.gz` 命令解压它。
- 3. 运行 `patch -p1 < SSLpatch` 来修补源文件。
- 4. 进入 `src` 目录，并编辑 `Configuration.tmp1` 文件，使其包含以下行以及其他未更改的行。
  
  ```
  SSL_BASE=/usr/local/ssl
  SSL_APP_DIR=($SSL_BASE)/bin
  SSL_APP=/usr/local/ssl/bin/openssl
  ```

- 5. 运行 `cd ..` 命令将当前目录变回 `src`。
- 6. 运行 `./configure` 命令，并附上你通常使用的任何命令行参数。例如，如果你想将 Apache 安装到 `/usr/local/apache`，请使用 `--prefix=/usr/local/apache` 选项运行此脚本。
- 7. 运行 `make && make install` 命令来编译和安装 Apache。
  
  这将编译并安装标准（httpd）和启用 SSL（httpsd）的 Apache。现在你需要为 Apache 创建一个服务器证书。

### 为 Apache-SSL 服务器创建证书

若要创建一个临时证书以便快速开始，请遵循以下步骤：

- 1. 进入 Apache 源代码分发目录下的 `src`（例如 `/usr/local/src/httpd_version/src`）子目录。
- 2. 进入 `src` 目录后，运行 `make certificate` 命令以创建一个仅用于测试目的的临时证书。`make certificate` 命令使用 `/usr/local/ssl/bin/openssl` 程序为你创建一个服务器证书。你会被问到几个不言自明的问题。以下是此命令的一个会话示例：

  ```
  ps > /tmp/ssl-rand; date >> /tmp/ssl-rand ;\
  RANFILE=/tmp/ssl-rand /usr/local/ssl/bin/openssl req -config
  ../SSLconf/conf/ssl.cnf \\
  -new -x509 -nodes -out ../SSLconf/conf/httpsd.pem \\
  -keyout ../SSLconf/conf/httpsd.pem ; \\
  In -sf httpsd.pem ../SSLconf/conf/ \usr/local/ssl/bin/openssl
  \
  x509 -noout -hash < ../SSLconf/conf/httpsd.pem ; .0; \\
  rm /tmp/ssl-rand
  Using configuration from ../SSLconf/conf/ssl.cnf
  Generating a 1024 bit RSA private key
  ..........................................+++++
  .................................................+++++
  writing new private key to '../SSLconf/conf/httpsd.pem'
  -----
  You are about to be asked to enter information that will be
  incorporated
  into your certificate request.
  ```



您即将输入的是所谓的**区别名称**（Distinguished Name，简称 DN）。
字段有很多，但您可以留空其中一些。
某些字段会有默认值。
如果您输入“.”，该字段将被留空。
-----
国家名称（2 位代码）[GB]:US
州或省名称（全称）[Some-State]:California
所在地名称（例如，城市）[]:Sacramento
组织名称（例如，公司）[]:MyORG
组织单位名称（例如，部门）[]:CS
服务器名称（例如 ssl.domain.tld；必填!!!）
[]:Shea_evoknow.com
电子邮件地址 []:kabi@evoknow.com

名为 `httpd.pem` 的证书创建在您的 Apache 源分布目录的 `SSLConf/conf` 子目录中。

现在您已准备好配置 Apache。

## 配置使用 Apache-SSL 的 Apache

当您在“编译和安装 Apache-SSL 补丁以适配 Apache”部分运行 `make install` 时，它在您的 Apache 安装目录的 `conf` 子目录中创建了一个 `httpd.conf` 文件。例如，如果您使用 `--prefix=/usr/local/apache` 来配置 Apache，您将在 `/usr/local/apache/conf` 目录中找到 `httpd.conf` 文件。您需要使用 `mv` 命令将其重命名为 `httpd.conf`。如果您将在其他目录中安装 Apache，请确保将 `/usr/local/apache/conf/` 替换为适当的路径名。

在使用 Apache 中的 SSL 时，您有两种选择。您可以为主服务器启用 SSL，或者为一个或多个虚拟 Web 站点启用它。在这里，我将向您展示如何为主 Apache 服务器启用 SSL，并讨论您需要执行哪些操作才能为虚拟 Web 站点启用 SSL。请按照以下步骤修改 `httpd.conf` 文件：

- 默认情况下，Web 浏览器会将 SSL 请求发送到您的 Web 服务器的 443 端口，因此，如果您希望将主 Apache 服务器转换为支持 SSL 的服务器，请将 `Port` 指令行更改为：
  ```
  Port 443
  ```
- 添加以下行，以告知 Apache 如何生成加密 SSL 连接所需的随机数据：
  ```
  SSLRandomFile file /dev/urandom 1024
  SSLRandomFilePerConnection file /dev/urandom 1024
  ```
- 如果您希望拒绝除 https（即 SSL 请求）以外的所有请求，请插入以下指令：
  ```
  SSLRequireSSL
  ```
- 要启用 SSL 服务，请添加以下指令：
  ```
  SSLEnable
  ```
- 默认情况下，支持 SSL 的 Apache 所使用的缓存服务器创建在 Apache 源分布的 `src/modules/ssl` 目录中。请设置此目录，如下所示：
  ```
  SSLCacheServerPath \
  `/path/to/apache_version`/src/modules/ssl/gcache
  ```
- 添加以下指令以启用缓存服务器端口和缓存超时值：
  ```
  SSLCacheServerPort logs/gcache_port
  SSLSessionCacheTimeout 15
  ```
- 现在您需要告知 Apache 保存服务器证书文件的位置。如果您按照之前的 OpenSSL 安装说明创建了服务器证书，您的服务器证书应该位于 `/usr/local/ssl/certs` 目录中。但是，如果您决定暂时使用测试证书（通过之前讨论的 make_certificate 命令创建），那么您的测试证书位于 `/path/to/apache_version/SSLconf/conf` 目录中，名为 `httpd.pem`。请设置以下指令为您的服务器证书的完全限定路径，如下所示：
  ```
  SSLCertificateFile \
  `/path/to/apache_version`/SSLconf/conf/httpd.pem
  ```
- 设置以下指令并保存 `httpd.conf` 文件：
  ```
  SSLVerifyClient 3
  SSLVerifyDepth 10
  SSLFakeBasicAuth
  SSLBanCipher NULL-MD5:NULL-SHA
  ```
- 要在 443 端口上为名为 `myvhost.Evoknow.com` 的虚拟主机启用 SSL，我需要以下配置：
  ```
  Listen 443
  <VirtualHost myvhost.evoknow.com:443>
    SSLEnable
    SSLCertificateFile `/path/to/myvhost.certificate.cert`
  </VirtualHost>
  ```

您的支持 SSL 的 Apache 服务器已准备就绪，可以进行测试。

## 测试您的 SSL 连接

在使用 `/usr/local/apache/bin/apache -k startssl` 命令启动 Apache 服务器后，您应该能够使用 `http://localhost` 或 `https://your_server_hostname/` 从本地（在 Web 服务器本身）或远程 Web 客户端访问您的 SSL 站点。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_592_0.png)

> 大多数人在测试他们的 SSL 服务器时忘记使用 `https` 而使用了 `http`，当他们看不到 SSL 连接时就会惊慌失措（通常由大多数流行 Web 浏览器状态栏中的一个小锁图标显示）。

## 获取证书

在您使用 SSL（通过 mod\_ssl 或 Apache-SSL）使用 Apache 之前，您必须创建适当的服务器证书。您可以从商业证书颁发机构（CA）获取服务器证书，或者您可以创建自己的证书颁发机构，然后为您的服务器和客户端创建证书。后一种方法通常用于希望在校区之间内部管理证书的大型组织。

### 从商业 CA 获取服务器证书

要从商业 CA 获取签名证书，您必须满足其要求。有两种类型的要求：

- 您（请求者）必须证明您就是您声称的实体。
- 您必须提交电子形式的证书签名请求（CSR）。

第一个要求通常是通过遵循 CA 验证个人或组织指南来满足的，因此您必须咨询您选择的 CA 以了解如何继续。通常，如果您计划为 Web 服务器认证，请准备好提交法律文件副本，如商业登记或注册文件。或者，您可以使用 OpenSSL 创建 CSR。

创建 CSR 的第一步是为服务器创建私钥。然后您需要创建一个证书签名请求，该请求需要发送到商业证书颁发机构。在您获得商业证书颁发机构的批准后，您可以将证书安装到您的服务器上，并在 Apache 中使用 SSL。我将在以下部分中详细讨论这些步骤。

### 生成私钥

要为名为 `www.domain.com` 的 Web 服务器主机生成加密的私钥，请运行：

```
openssl genrsa -des3 -out www.domain.com.key 1024 -rand /dev/random
```

当您运行此命令时，您会被要求输入一个密码短语（即密码）来加密私钥。由于私钥是使用 `des3` 密码加密的，每次启动服务器时您都被要求输入密码短语。如果这是不理想的，您可以通过从上述命令行中移除 `-des3` 选项来创建非加密版本的私钥。我强烈建议您使用加密的私钥以确保高水平的安全性。毕竟，您不希望其他有权访问您服务器的人能够看到您的私钥。清单 19-1 显示了 www.domain.com.key 文件的内容。

**清单 19-1：www.domain.com.key 文件的内容**

```
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: DES-EDE3-CBC, C4B89F2F597AF68

47f4qGkrffT7NEyqEs/uYaPoeAqksOnALTkUVvADHKL7BbA+BB+rT/aaM7hhwEzU

jjaRd1XfkIej3qH6d/2I0AwFfyIAY0H13w082pI15uxui2sm7ZRyUDpRMjxzI
/srhn/DU+dlq1lpH3vJRw2hhNVJHUBOcuCsz8Z8GOhICa5MF6s2xDR+ckPOT2Uvf5
jLGiyrRoBzNQOFDv8wqZeOSOSuKHU9ZKda/PCb+wfyDWZfr8H9PNT1mlajMGt
19LWZkzBw2mmw79Pq6X5ycq+7dKMxiQL6d/dY1HOZUYHJm3jtqUlPI7NXjd4TG
k8xXbvxjPioVyFKoqhmVPq7Wd9enYU72RuVo+a105oTG2Gp15y37GkUnTy
1W8JFH5BuscSrP+95SKTKvOwOLnOjRtgxK/YEZTQEza4qPCsz6eiyAw4fFTaw
6q/G3ZJCpJBJ2YLmwvua3dpv9bucSCxmB0oX9vjEBB/yvj9pLbu5pSBKxA4th
fZcZB94wxrr/EM6GDs2xgnNh+SwF5F3c/bpURMCq/0t6FF/H47jVnUf1t7d0tTT7
UbdQvAAsr9tKSfzsRKMOGB4OvneuD5C2UI/3O/NaXS5/Efu9HGlctcRKwZEVI/+
MSJBe3JYDmB6mGDGNJUEXp64hv4jKo0NdkAjKE6K2E2w2o2al1F8u12PNotW6YD
T5hgoISm5mqQQLCfs5JH5TAbKxLejsygO5RzvPJS0KznWaHcLoFic14pDSor4ghM
6YEdaSBu1vSf3tn2vKsHueZHqFov51GcjBvEyAE0Y4QL0k9EznMBw=
-----END RSA PRIVATE KEY-----
```

### 生成证书签名请求

现在您需要使用您的私钥如下所示生成 CSR：

```
openssl req -new -key www.domain.com.key -out www.domain.com.csr
```

如果您之前加密了私钥，您会被要求输入私钥的密码短语。输入适当的密码短语。然后，您会被要求输入国家名称、州、城市、组织名称、组织单位（部门名称、通用名称（即，如果证书请求是为您自己，则是您的名字，或者是您的服务器的主机名）、电子邮件地址以及一些可选信息，如挑战密码和可选的公司名称。

在此阶段，您需要将您的 CSR 提交给像 Thawte 这样的 CA。因为认证过程涉及验证您的个人或业务身份文件，所以在您收到证书之前可能需要几天到几周甚至几个月的时间。以下部分使用 Thawte 作为选定的 CA。





如果您急于获取证书以开始测试，或者有其他原因需要快速获取临时证书，请咨询您的 CA。他们可能提供某种方式来为您发放临时、不受信任的证书。例如，Thawte 允许您通过 Web 提交 CSR 以获取临时证书，您将在几分钟内通过电子邮件收到该证书。

从商业 CA 获取服务器证书后，您可以按照其说明安装证书文件。这一步通常相当简单。您可能会被要求将文件复制到某个目录并重启服务器。

如果您对获取来自商业 CA 的签名证书不感兴趣，您可以创建自己的 CA，并随时对服务器或用户等实体进行认证。我将在以下章节中向您展示操作方法。

## 创建私有证书颁发机构

如前所述，私有自签名证书不适合用于 Internet 场景，因为广大用户不应信任此类证书。然而，如果您希望向各部门颁发内部、全公司范围的证书，又不想经历第三方商业 CA 验证的麻烦，您必须使用私有 CA。

**注意**

您可能能够从商业 CA 获得您私有 CA 的交叉签名证书。在这种情况下，您的私有 CA 将与商业 CA 链接，因此每个人都应该信任您签发的任何证书。但是，商业 CA 可能会限制您的证书颁发权限，使其仅限于您自己的组织，以确保您不与 CA 竞争。

请遵循以下步骤，使用 OpenSSL 创建私有自认证 CA：

1.  从 OpenSSL 网站的用户贡献软件部分（`www.openssl.org/contrib`）下载 `ssl.ca-version.tar.gz` 脚本发行版的最新版本。将此文件解压到您选择的目录中。将创建一个名为 `ssl.ca-version` 的子目录。您将在目录中找到一组 `sh` 脚本。
2.  运行 `new-root-ca.sh` 脚本为您的私有 CA 创建自签名根证书。系统将提示您输入密码短语。此密码短语对于签署未来的证书是必需的。
3.  要创建服务器证书，运行 `new-server-cert.sh www.domain.com` 脚本来创建服务器的私钥和公钥。系统将提示您输入新服务器证书的区分名域。该脚本还将生成一个 CSR，如果您愿意，之后可以将其发送给商业 CA。
4.  运行 `sign-server-cert.sh` 脚本批准并签署您使用 `new-server-cert.sh` 脚本创建的服务器证书。
5.  运行 `new-user-cert.sh` 脚本创建用户证书。当由商业证书颁发机构签署时，用户证书可以与 Web 浏览器一起用于向远程服务认证用户。然而，由于对它们的理解不足以及可用的客户端和服务器软件缺乏，用户证书并不常见。
6.  运行 `sign-user-cert.sh` 脚本签署用户证书。此外，运行 `p12.sh` 脚本将私钥、签名密钥和 CA 的公钥打包到扩展名为 `.p12` 的文件中。然后可以将此文件导入到电子邮件客户端等应用程序中使用。

现在，您已准备好在各种应用程序中使用 OpenSSL。OpenSSL 是安全的重要组成部分。您越是使用 OpenSSL，就会越发发现将其集成到许多服务中很容易。

## 访问 SSL 页面

如果您在 `/usr/local/apache` 目录中安装了 Apache，请运行 `/usr/local/apache/bin/httpsdctl start` 命令以启动启用了 SSL 的 Apache 服务器。如果收到错误消息，请检查日志文件以获取详细信息。`httpd.conf` 文件中的拼写错误或路径缺失是常见错误原因，因此请留意这些情况。服务器启动后，您可以使用 HTTPS 协议访问它。例如，要访问名为 `shea.evoknow.com` 的启用 SSL 的 Apache 服务器，我可以将 Web 浏览器指向 `https://shea.evoknow.com`。如果您使用的是测试证书或自有 CA 签发的证书，Web 浏览器将显示一条警告消息，指出证书无法验证。这是正常的，因为没有已知的 CA 签署该证书。您应该接受该证书并浏览您启用了 SSL 的网站。

✦ ✦ ✦

# 在 Windows 上运行 Apache

Windows 平台上的 Apache 2 比以往任何时候都更加稳定。这一部分专门介绍 Windows 平台上的 Apache。我将向您展示如何在 Windows 平台上安装和配置 Apache，以及如何使用仅有的几个 Windows 专属 Apache 指令。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_597_0.png)

### 本部分包含内容

- **第 20 章** 在 Windows 上安装和运行 Apache
- **第 21 章** 为 Windows 配置 Apache

![](img/e11fcbd2818a3495ac70085e5d8d1c26_599_0.png)

## 在 Windows 上安装和运行 Apache

# 本章内容

- 在 Windows 上运行 Apache 的系统要求
- 在 Windows 上安装 Apache
- 启动、停止和重启 Apache

尽管 Apache 很久以前就被移植到了 Windows 平台，但 **Apache 2.0** 是第一个能够利用原生 Windows 系统调用的版本。所有之前版本的 Apache 都使用了 POSIX 抽象层，这在 Windows 上运行 Apache 时会降低性能。现在，Apache 终于可以与其他原生 Web 服务器（如 Microsoft IIS 和 Netscape Enterprise 服务器）进行正面竞争了。

在本章中，您将了解在 Windows XP、Windows 2000、Windows NT 和 Windows 9x/ME 等流行 Windows 平台下运行 Apache 的系统要求；您还将学习如何安装 Apache 并进行配置，以便您可以快速启动运行。

### 系统要求

Apache 要求您的 Windows 系统启用 **TCP/IP**。您应该确保为您的 Windows 平台安装了最新的 **TCP/IP 堆栈**（*Winsock*）。启用了 TCP/IP 的 Windows 2000 用户可以在没有其他 Windows 特定要求的情况下安装 Apache。Windows NT 4.0 用户应确保已安装最新的服务包。

Windows 2000 Advanced Server 是运行生产级 Apache Web 服务器的理想平台。Windows 2000 Advanced Server 针对网络服务进行了优化，因此它应该能为 Apache 以及其它 Internet 服务带来最佳性能。

> 注意
>
> 我使用 Windows 2000 Advanced Server 作为本书中 Windows 特定章节的 Windows 平台。

您还需要 Microsoft Installer 版本 1.10 或更高版本来安装 Apache。Windows 2000 和 Windows ME 都内置了 Microsoft Installer。对于其他版本的 Windows，您需要查阅手册或访问 Microsoft 网站以获取详细信息。

### 下载 Windows 版 Apache

Windows 版 Apache 可以以源代码发行版或二进制发行版的形式下载。不幸的是，与大多数 Unix 平台不同，Windows 并不附带开发功能，例如像 GCC 这样的标准 C 编译器。因此，实际上只有拥有 Microsoft Visual Studio 等开发工具的 Windows 开发人员才能编译 Apache。对于大多数人来说，二进制发行版是唯一可行的下载选项。虽然 gcc 在 Windows 上可用，但 Apache 源代码无法使用 Windows 版本的 gcc 编译。

Windows 版 Apache 二进制文件的官方下载站点是 `http://httpd.apache.org/dist/httpd/binaries/win32/`。二进制发行版的命名为 `httpd_version-win32-no_src-rrumber.msi`（例如，`httpd_2_0_16-win32-no_src-r1.msi`）。源代码发行版的命名为 `httpd_version-win32-wint_src.msi`。请下载最新、稳定的二进制发行版。

> 注意
>
> 如果您是一位计划下载并编译 Apache 源代码发行版的 Windows 开发人员，则可以下载源代码发行版的 zip 版本，而不是 _msi 安装程序版本。您将需要解压缩程序（例如 PKWARE 的 PKUNZIP 或 WinZip）来提取源文件，这些源文件具有 MS-DOS 行尾。不要下载以 .tar.gz 或 .tar.Z 结尾的源代码发行版，因为它们是 Unix 软件包，其行尾仅适用于 Unix 平台。

### 安装 Apache 二进制文件

双击下载的 `httpd_version-win32-no_src.msi` 文件将启动 Microsoft Installer 和 Apache 安装程序。单击“下一步”以开始安装。系统会提出一系列问题，下面将对此进行讨论。

- 阅读并接受图 20-1 中显示的许可协议。

您必须点击标记为“I accept the terms in the license agreement”的单选按钮以启用“下一步”按钮。单击“下一步”继续到下一个屏幕。





![](img/e11fcbd2818a3495ac70085e5d8d1c26_601_0.png)

**图 20-1：许可协议**

- 2. 将出现一个类似图 20-2 的屏幕。该屏幕显示最新信息（README）。浏览这些信息，准备好后，点击**下一步**继续。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_601_1.png)

**图 20-2：请先阅读通知**

- 3. 下一个屏幕类似图 20-3，要求您输入网络域名、服务器名称和管理员电子邮件地址。默认情况下，安装程序会根据当前的 Windows 设置确定这些名称。如果合适，请更改默认值。除非主机实际上具有适当的 DNS 和网络配置，否则请勿更改服务器名称或域名。换句话说，不能任意选择域名或服务器主机名。此信息对于正在安装 Apache 的主机必须是有效的。点击**下一步**继续。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_602_0.png)

**图 20-3：输入您的服务器信息**

- 4. 选择是通过“完整”安装（安装所有程序功能，占用最多磁盘空间）还是“自定义”安装（仅安装选定的程序和文件）来安装 Apache，如图 20-4 所示。我建议您选择自定义安装选项，因为它可以让您更了解正在安装的内容。在自定义安装中，您可以始终选择所有项目以获得完整安装。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_602_1.png)

**图 20-4：选择安装方法**

- 5. 如果您选择进行自定义安装，您将看到类似图 20-5 所示的屏幕。显示了一个选项树。您可以点击每个项目来决定是否要安装它。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_603_0.png)

**图 20-5：为您的站点定制 Apache**

例如，点击 Apache httpd Server 项目会弹出如图 20-6 所示的选项菜单。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_603_1.png)

**图 20-6：安装选项菜单**

选择将功能（即 Apache 服务器）安装到本地硬盘或网络驱动器。如果磁盘空间是个问题，且您不想安装在线文档，可以通过点击该选项来取消选中此功能，从而选择不安装文档。

默认情况下，Apache 安装在 `C:\Program Files\Apache Group` 目录中。若要更改此设置，请点击 `Change` 按钮，在下一个对话框窗口中输入不同的目录，然后点击 OK 返回此屏幕。点击 Next 继续。

- 6. 安装程序显示一个屏幕，提示已准备好安装 Apache。点击 **Next**，并在安装 Apache 时等待。安装完成后，点击 **Finish** 结束安装程序。

默认情况下，安装程序会启动 Apache，因此您应该能够通过使用 Web 浏览器查看系统上的默认 Web 站点。将浏览器指向 http://localhost 或 http://127.0.0.1，您应该能看到类似图 20-7 所示的 Web 站点。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_604_0.png)

## 运行 Apache

您可以在 Windows 下通过控制台窗口中的命令行，或在 Windows 2000 或 Windows NT 系统下作为服务来运行 Apache。在 Windows 2000 或 NT 系统上，您应该将 Apache 作为自动服务运行。事实上，默认安装程序会检测您的 Windows 版本，并针对这两个平台选择将其作为服务安装。

> **注意** 在 Windows 9x 系统上，没有很好的方法将 Apache 作为服务运行。对于 9x 平台，最佳方法是在控制台窗口中运行 Apache。

### 将 Apache 自动作为 Windows 服务运行

安装程序会自动检测您的 Windows 平台，并在 Windows 2000 和 NT 系统上将 Apache 作为服务安装。在 Windows 2000（或 NT 系统）上，若要在服务器重启时自动（或不自动）运行 Apache，请执行以下操作：

- 1. 选择 开始 → 设置 → 控制面板 → 管理工具 → 服务，以显示类似图 20-8 所示的屏幕。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_605_0.png)

- 2. 双击服务名称“Apache”，将出现一个对话框，如图 20-9 所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_605_1.png)

- 3. 在“常规”选项卡下，您将看到一个标记为“启动类型”的下拉菜单。选择 **Automatic**（重启时自动启动）、**Manual**（重启时手动启动）或 **Disabled**（重启时禁用）选项。

- 4. 如果您希望启动或停止 Apache 服务，请点击相应的按钮。

- 5. 默认情况下，Apache 使用本地系统账户在 **Windows 2000** 或 **Windows NT** 下运行。如果您希望将此用户 ID 更改为其他用户，请点击 **Log On** 选项卡并选择 **This account** 选项。然后输入相应的用户名和密码。请确保该用户名和密码是您 Windows 网络上有效的用户凭证。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_606_0.png)

默认情况下，Apache 以 LocalSystem（“System”）账户运行，这是一个非常强大的本地账户，不与任何用户名或密码关联。此账户不能用于登录机器或连接到同一 Windows 网络上的其他机器。如果您选择更改 Apache 服务的用户，请确保创建一个适当的用户账户，该账户可以作为服务（即作为操作系统的一部分）运行，能够登录到服务，能够备份和还原文件和目录，对文档根目录具有读取访问权限，并且对 Apache 日志目录具有读取、写入和删除访问权限。默认的用户名对于大多数系统应该是足够的。

- 6. 在 Windows 2000 Advanced Server 下，若要定义 Apache 服务失败时的操作，请选择“恢复”选项卡并为第一次、第二次及后续故障选择适当的操作。例如，您可以选择在 Apache 服务失败时自动重启服务或重启机器，甚至运行外部程序以执行一些有用的操作，例如呼叫系统管理员。图 20-10 显示，当 Apache 服务第一次运行失败时，它将自动重启；在第二次故障时，服务器将自动重启；对于任何后续故障，一个程序将呼叫系统管理员。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_606_1.png)

**图 20-10：Windows 2000 Advanced Server 上 Apache 服务的恢复选项**

- 7. 服务配置完成后，点击“应用”以完成设置。

- 您也可以随时通过控制台使用 **net start apache** 或 **net stop apache** 命令来启动或停止 Apache 服务。

与许多 Windows 服务不同，Apache 将其错误记录在自带的错误日志文件中。默认情况下是 `logs\error.log`，它位于默认的 `C:\Program Files\Apache Groups\Apache` 目录中。只有 Apache 服务初始启动期间发生的错误才会记录在 Windows 2000 和 NT 下可用的事件日志功能中。

### 通过开始菜单管理 Apache

默认情况下，Apache 安装程序会在 Windows 开始菜单中添加菜单项，您可以使用这些菜单项来启动、重启和停止 Apache，方法如下：

- 若要启动 Apache，选择 开始 程序-Apache httpd Server Control Apache Server Start。
- 若要重启 Apache，选择 开始 程序-Apache httpd Server Control Apache Server Restart。
- 若要停止 Apache，选择 开始 程序-Apache httpd Server Control Apache Server stop。
- 您还可以编辑和测试 `httpd.conf` 配置文件，方法如下：

    - 若要编辑 `httpd.conf` 文件，选择 开始 程序-Apache httpd Server Configure Apache Server Edit Configuration。
    - 若要测试 `httpd.conf` 文件，选择 开始 程序-Apache httpd Server Configure Apache Server Test Configuration。这等同于从 Apache 二进制目录运行 `Apache -t` 命令。将会弹出一个控制台窗口，您将能够查看配置语法。

### 通过命令行管理 Apache

如果您不将 Apache 作为服务运行，您可以使用以下命令从控制台（通常称为 DOS 窗口）启动、停止或重启 Apache。

- 若要启动 Apache，请从 Apache 二进制目录（默认为 `C:\Program Files\Apache Group\Apache`）运行 `Apache -k start`。
- 若要优雅重启 Apache，请从 Apache 二进制目录（默认为 `C:\Program Files\Apache Group\Apache`）运行 `Apache -k restart`。
- 若要停止 Apache，请从 Apache 二进制目录（默认为 `C:\Program Files\Apache Group\Apache`）运行 `Apache -k stop`。您也可以使用 `Apache -shutdown` 命令来达到相同的效果。
- 若要使用非默认配置文件运行 Apache，请使用 `-f` 选项指定文件名。例如，若要使用 `c:\test\new-httpd.conf` 运行 Apache，请从包含 Apache 二进制的目录运行 `Apache -f "c:\test\new-httpd.conf" -k start` 命令。





## 运行多个 Apache 服务

在 Windows 系统中，Apache 通常只运行两个进程：一个使用多个线程来处理所有 HTTP 请求，另一个用于监控第一个进程。如果第一个进程终止，第二个进程（即负责监控第一个进程的进程）将重启第一个进程。

然而，你仍然可以从 Apache 二进制目录的命令行运行多个主 Apache 服务器，使用不同的 httpd.conf 文件（默认目录为 `C:\Program Files\Apache Group\Apache`），方法如下：

```apache
Apache -f "path_to_httpd.conf"
```

例如，你可以创建两个主 Apache 服务，一个响应端口 80，另一个响应端口 8080，方法是创建两个 httpd.conf 文件。你可以使用上述命令运行这些服务中的每一个。但是，在 Windows 2000 或 NT 系统中，已经安装了一个默认的 Apache 服务，因此你只需修改 `C:\Program Files\Apache Group\Apache\conf\httpd.conf` 以反映端口更改，并将其另存为另一个文件。然后，你只需使用上述命令运行一个 Apache 实例即可。默认的 Apache 配置仍然可以在端口 80 上运行。

要创建一个新的 Apache 服务，请从 Apache 二进制目录（默认为 `C:\Program Files\Apache Group\Apache`）运行以下命令：

```apache
Apache -n new_service_name -f "path_to_httpd.conf" -k install
```

运行此命令将安装一个新服务，名为 new_service_name，它将使用 path_to_httpd.conf 路径。

你也可以使用 `Apache -n existing_service_name -k uninstall` 命令移除现有的 Apache 服务。

## 配置 Windows 下的 Apache

前面章节中找到的大多数信息也适用于 Windows 上的 Apache。然而，由于 Unix 系统和 Windows 系统在底层工作方式上的差异，Windows 版 Apache 和 Unix 版 Apache 之间存在某些区别。本章将讨论这些区别。

### Windows httpd.conf 语法

Unix 系统和 Windows 系统的 httpd.conf 文件之所以不同，是因为 Windows 处理路径名的方式不同。
区别如下：

- 在 Windows 系统中，路径中的目录和文件名使用反斜杠分隔。例如，c:\temp 是一个有效的目录路径。但是，Apache 内部仍然使用前斜杠作为路径分隔符，因此你仍然必须使用前斜杠。例如，在 httpd.conf 文件中 c:/temp 是正确的，但 c:\temp 是错误的。

- Windows 路径通常包含空格。例如，c:\Program Files\Apache Group\Apache\htdocs 在 Windows 环境中是一个可接受的路径。在 httpd.conf 文件中使用此类路径名时，请用双引号将整个路径括起来。例如：
  ```apache
  ServerRoot "C:/Program Files/Apache Group/Apache"
  ```
  
  这里，ServerRoot 指令被设置为指向 C:/Program Files/Apache Group/Apache 目录。

# 第 21 章：配置 Windows 下的 Apache

- Windows 上的 httpd.conf 与 Unix 上的 httpd.conf 有何不同
- 调整 Apache 以优化性能
- 测试 Apache 配置
- 使用 Comanche 管理 Apache
- 为基于 Perl 的 CGI 脚本配置 Apache
- 如何在 Windows 上使用 mod_perl
- 如何在 Windows 上使用 PHP
- 如何在 Apache 中使用 ISAPI 扩展
- 如何在 Windows 上使用 UserDir

## 调整 Apache 性能

早在 Apache 2.0 之前，Windows 上的 Apache 就已经是多线程的。这是因为像 Windows 2000 和 Windows NT 这样的 Windows 系统在使用线程时比使用由多个子进程组成的服务表现更好。

在 Windows 系统中，Apache 仅使用两个进程运行。父进程监控子进程，后者负责使用多个线程处理所有请求。

为了控制在 Windows 下 Apache 可以同时处理多少个请求，你需要调整 `ThreadsPerChild` 指令。有关此指令的详细信息，请参见第 4 章。此指令控制负责所有请求的唯一 Apache 子进程可以创建的线程数。默认值 50 对于大多数网站来说应该足够了。

如果你需要更高的响应率，请确保你有适当的系统资源，例如足够的 RAM 和快速的 CPU 来支持你的速率需求。根据 `winnt_MPM` 模块的源代码，你应该可以将此值设置为最大 4096 个线程。对于大多数 Web 网站，低于 256 的数值可能更合适。

`MaxRequestsPerChild` 指令限制了子进程可以处理的请求数（有关此指令的详细信息，请参见第 4 章）。由于在 Windows 下单个子进程通过线程处理所有请求，因此此指令应设置为非常高的数值或 0，这意味着子进程将永不退出。

## 测试 Apache 配置

每次修改 `httpd.conf` 文件时，你都可以从 Apache 二进制目录（默认为 `C:\Program Files\Apache Group\Apache`）运行以下命令，以确定是否创建了任何语法错误。

```apache
Apache -t
```

你也可以选择 `开始\程序\Apache httpd Server\Configure Apache Server\` 下的 Test Configuration 选项来执行相同操作。

如果发现错误，你可以在使用 `Apache -k restart` 命令重启服务器之前修复它。

## 使用 Comanche 管理 Apache

如果你主要是 Windows 用户，你可能会想知道 Apache 的 GUI 管理程序在哪里。抱歉，Apache 并不附带这样的程序。但有很多第三方的开发中项目甚至商业项目，你可以在 `http://gui.apache.org` 上了解更多信息。

然而，Comanche（*ApaCHe 的配置管理工具*）是我最喜欢的，因为它支持多平台、非侵入式、可扩展且非常容易设置。你可以从 `http://www.covalent.net/projects/comanche/` 下载 Comanche。

下载 Comanche 的二进制发行版后，解压并单击可执行文件图标即可开始配置 Apache。运行 `comanche.exe` 程序时，会出现一个带有标有 Comanche 的按钮的小窗口，如 Figure 21-1 所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_611_0.png)

单击标有 Comanche 的按钮以启动 Comanche。你应该看到与下面 Figure 21-2 中所示类似的屏幕。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_611_1.png)

你可以单击左侧的树元素来选择不同的配置选项。例如，单击左侧树菜单底部的 Default Web Server 选项会显示与 Figure 21-3 中所示类似的屏幕。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_612_0.png)

单击右侧的默认 Web 站点属性链接会调出实际的配置屏幕。

在这里，你可以使用树菜单中的 Basic configuration、Module management、Server identification、Server options、Environment、Indexing、Proxy、Apache Jserv Settings、Alias 或 CGI Settings 选项进行配置。

例如，要将 Port 指令更改为非默认值（即除了 80 之外的值），你可以展开 Basic Configuration 子选项树，单击 Listening 选项，将其设置为 8080 等值，如 Figure 21-4 所示。

同样，要创建一个名为 /cgi-bin/ 的 CGI 脚本别名，指向 “C:\Program Files\Apache Group\Apache\cgi-bin/” 目录，我可以展开 Alias 选项树，单击 CGI 选项，并使用 Add 按钮添加别名，如 Figure 21-5 所示。

新创建的别名将显示在主 Alias CGI 屏幕上。

在配置默认 Web 服务器或新的虚拟主机时，你可以通过选中左侧的 Default Web Server 选项并右键单击来快速访问选项，而无需展开它，如 Figure 21-6 所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_613_0.png)

![](img/e11fcbd2818a3495ac70085e5d8d1c26_613_1.png)

![](img/e11fcbd2818a3495ac70085e5d8d1c26_613_2.png)

如你所见，一旦你习惯了导航左侧的选项树，并知道哪些功能可以被创建、启用或禁用，你就可以使用此工具通过 GUI 管理 Apache。但是，请记住 Comanche 是一个正在开发中的项目。现在可以使用它，并留意可用的更新版本。

## 配置 Apache 以处理动态内容

与 Unix 版本的 Apache 类似，你可以使用 Windows 上的 Apache 通过 CGI、PHP、SSI 脚本生成动态内容。然而，某些动态内容生成方案的配置存在一些差异，本节将对此进行讨论。

> **注意**
> 这里讨论的大多数指令在第 4 章和第 5 章中也有讨论。你可以在这些章节中找到所有语法选项。

### 运行基于 Perl 的 CGI 脚本

要在 Windows 上的 Apache 中运行基于 Perl 的 CGI 脚本，你必须在系统上安装 Perl。你可以从 `http://www.activestate.com` 下载 Windows 版的 Perl。

正确安装 Perl 后，你可以像往常一样使用 `ScriptAlias` 指令配置 Apache 以运行 CGI 脚本。通常，脚本别名创建如下：

```apache
ScriptAlias /cgi-bin/ "C:/Program Files/Apache Group/Apache/cgi-bin/*"
```

你也可以使用 `Options ExecCGI` 指令在目录中启用 CGI 脚本。现在，为了让 Apache 调用适当的 Perl 解释器，你必须确保脚本的第一行如下：

```perl
#!d:/rive:/path_of_perl_interpreter
```

这被称为*shebang 行*。例如，如果你将 Perl 安装在 `c:\perl\bin` 目录中，你可以创建第一行设置为以下内容的 Perl 脚本：

```perl
#!c:/perl/bin
```

创建用于 CGI 的 Perl 脚本还有另一种方法。默认情况下，Perl 在 Windows 注册表中注册 `.pl` 扩展名，以便由 Perl 解释器执行。如果在 `httpd.conf` 的主服务器配置部分设置了 `ScriptInterpreterSource` 注册表指令，你就可以正确运行任何具有 `.pl` 扩展名的脚本。Apache 将从 Windows 注册表中获取解释器路径，而不是从第一行 shebang 行获取。

> **交叉引用**
> 阅读第 12 章以了解许多其他适用于 Windows 平台 Apache 的 CGI 相关问题详情。





## 运行 mod_perl 脚本

要运行 `mod_perl` 脚本，你必须安装 `mod_perl` 模块。在安装 `mod_perl` 二进制模块之前，你需要在系统中安装 Perl，因此请确保你拥有来自 http://www.activestate.com 的最新版本的 Windows Perl。

安装 Perl 后，你可以从命令行运行以下命令来下载并安装 `mod_perl` 模块：

```
ppm install http://theoryx5.uwinnipeg.ca/ppmpackages/mod_perl-version.ppd
```

例如，要安装 `mod_perl` 的 1.25 版本，请运行：

```
ppm install http://theoryx5.uwinnipeg.ca/ppmpackages/mod_perl-1.25_1.3.19.ppd
```

在安装过程中，系统会提示你输入 Apache modules 目录的完全限定路径名。安装过程中显示的提示如下所示：

```
Which directory should mod_perl.so be placed in?
(enter q to quit) [C:/Apache/Modules]
```

如果你将 Apache 安装在默认目录 `C:\Program Files\Apache Group\Apache` 中，请输入 `C:\Program Files\Apache Group\Apache\Modules`。`mod_perl.so` 模块应安装在此目录中。

现在，你需要在 `httpd.conf` 中添加以下指令以加载 `mod_perl.so` 模块。

```
LoadModule perl_module modules/mod_perl.so
```

你还应按以下方式在 `httpd.conf` 中设置 `PATH` 变量：

```
PerlSetEnv PATH "C:\WINNT\system32;C:\WINNT;C:\perl;C:\perl\bin"
```

我假设你在 `C:\WINNT` 中安装了 Windows，在 `C:\WINNT\system32` 中有 `system32` 目录，并且你在 `C:\perl` 目录中安装了 Perl，Perl 解释器存储在 `C:\perl\bin` 目录中。如果这些假设中的任何一项（它们是 Windows 2000 或 NT 系统的默认值）不正确，请相应地进行更改。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_615_0.png)

默认情况下，`Windows` 目录要么是 `C:\WINDOWS`（对于 Windows 9x），要么是 `C:\WINNT`（对于 Windows 2000 和 Windows NT 系统）。如果你不确定，请打开一个控制台窗口（通常称为 DOS 窗口），输入 `echo %windir%` 命令来显示 `windir` 环境变量的值，该值指向 Windows 操作系统目录。你还可以在提示符下运行 `set` 命令来显示其他所有环境变量，例如 `path`，其中通常既包含 `OS` 目录，也包含 `system32` 目录。

要在启动时加载一组 mod_perl 模块，请使用名为 `startup.pl` 的启动脚本（你可以使用其他任何名称），并使用以下指令：

```
PerlRequire "Drive:/your_path/startup.pl"
```

别忘了将 `Drive:/your_path/startup.pl` 更改为 `startup.pl` 的实际路径。在 `startup.pl` 中，使用 `use module_name ();` Perl 语句加载你的模块。例如，以下 `startup.pl` 脚本加载了 CGI 模块、DBI（数据库独立接口）模块以及允许缓存数据库连接的 Apache::DBI 模块：

```
#!/c:/perl/bin/perl

use CGI ();
use DBI ();
use Apache::DBI ();
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_616_0.png)

关于许多仍然适用于 Windows 平台上的 Apache 的其他 mod_perl 相关事项，请参阅第 16 章以获取详细信息。请记住，要从 CPAN 下载模块，你必须使用 `ppm` 命令，而不是第 16 章中使用的 `perl -MCPAN -e` shell 命令。例如，要安装 Apache::DBI 模块，你必须运行：

```
ppm install http://theoryx5.uwinnipeg.ca/ppmpackages/Apache-DBI.ppd
```

同样，要安装 Apache::ASP，你必须运行：

```
ppm install http://theoryx5.uwinnipeg.ca/ppmpackages/Apache-ASP.ppd
```

## 运行 PHP 脚本

要在 Windows 上的 Apache 中运行 PHP 脚本，请遵循以下步骤：

- 1. 从 http://www.php.net/distributions/ 下载最新的 PHP 二进制分发包
- 2. 在 `c:\php` 目录中解压分发包。将 `c:\php\php4ts.dll` 复制到 Windows system32 目录。对于 Windows 2000 和 NT 系统，默认目录为 `C:\WINNT\system32`。另外，将 `c:\php.ini-dist` 复制到 Windows 目录，在 Windows 2000 或 NT 中默认为 `C:\WINNT`。
- 3. 默认的 `php.ini` 对大多数站点有效，但如果你愿意，可以对其进行编辑。默认情况下，Windows 平台上的 PHP 内置了 MySQL 和 ODBC 支持，因此你不需要为其启用任何扩展。但是，你应该查看 `extension=module_name.dll` 行，以确定是否需要启用其中的任何行。例如，如果你计划使用 GD 库（用于生成 PNG 图像）配合 PHP，那么你需要通过删除行首的分号字符来取消注释 `extension=php_gd.dll` 行。
- 4. 将以下行添加到 `httpd.conf` 中：

```
LoadModule php4_module c:/php/sapi/php4apache.dll
AddType application/x-httpd-php .php
AddType application/x-httpd-php .php4
```

- 5. 使用 `net stop apache` 命令，随后使用 `net start apache` 命令，从控制台重启 Apache Web 服务器。
- 6. 将一个名为 `hello.php` 的小型 PHP 脚本（如下所示）放置在你的 Web 服务器的文档根目录中。

```
<html>
<head>
<title>Hello World from PHP</title>
</head>
<body>
<?php echo "Hello World from PHP"; ?>
</body>
</html>
```

- 7. 通过运行 `http://your_server_name/hello.php` 命令来测试该脚本。如果你看到“Hello World from PHP”消息，则说明你已成功配置 PHP。
- 现在，你可以按照第 15 章中的说明为你的网站创建 PHP 脚本。

## 使用 mod_isapi 运行 ISAPI 扩展

Windows 版的 Apache 默认编译时包含 `mod_isapi`。该模块使 Apache 能够加载基于 Internet 服务器应用程序编程接口 (ISAPI) 的应用程序，这些应用程序可以用任何语言编写，从而使其能够通过 Apache 运行。ISAPI 最初是为 Microsoft Internet 信息服务器 (IIS) 设计的；Apache 通过使用 `mod_isapi` 模块来实现 ISAPI。然而，Apache 目前仅允许 ISAPI 扩展，因此，ISAPI 过滤器无法在 Apache 中工作。要使用 ISAPI 扩展（通常是 DLL，或数据定义语言），请将以下行添加到你的 `httpd.conf` 文件中：

```
AddHandler isapi-isa .dll
```

这使得 Apache 能够加载具有 .dll 扩展名的 ISAPI 扩展程序。`mod_isapi` 模块具有以下指令。

### ISAPIReadAheadBuffer

`ISAPIReadAheadBuffer` 指令设置读取前向缓冲区的最大大小，该缓冲区可供 ISAPI 扩展 DLL 使用。例如，当需要读取超出默认 49152 字节的数据时，需要使用 `ReadClient` 回调方法。

- **语法：** ISAPIReadAheadBuffer `size`
- **默认设置：** ISAPIReadAheadBuffer `49152`
- **上下文：** Server config

### ISAPILogNotSupported

`ISAPILogNotSupported` 指令启用或禁用记录来自 ISAPI 扩展 DLL 的所有不支持功能请求。这仅有助于隔离与运行异常的 ISAPI 扩展相关的问题。

- **语法：** ISAPILogNotSupported `On` | `Off`
- **默认设置：** ISAPILogNotSupported `on`
- **上下文：** Server config

### ISAPIAppendLogToErrors

`ISAPIAppendLogToErrors` 指令启用或禁用将来自 ISAPI 扩展 DLL 的请求存储在错误日志中。

- **语法：** ISAPIAppendLogToErrors `On` | `Off`
- **默认设置：** ISAPIAppendLogToErrors `Off`
- **上下文：** Server config

### ISAPIAppendLogToQuery

`ISAPIAppendLogToQuery` 指令启用或禁用将查询数据记录到服务器的访问日志中。

- **语法：** ISAPIAppendLogToQuery `On` | `Off`
- **默认设置：** ISAPIAppendLogToQuery `Off`
- **上下文：** Server config

## Windows 中的 UserDir

Apache 目前不与 Windows 用户账户一起工作，因此它无法检测 Windows 用户的主目录。如果你希望为用户提供的网站，可以使用以下解决方法：

- 1. 选择一个目录作为所有用户的顶级主目录。
- 例如，你可以创建一个名为 `C:\home` 的目录并用于此目的。





## 用户Web目录配置

2. 在此顶级目录中为每个用户创建一个子目录。使用每个用户的用户名来命名这些目录。例如，如果你有一个名为 `john` 的用户，请创建 `C:\home\john`。

3. 将以下配置添加到 `httpd.conf` 中：

```
<IfModule mod_userdir.c>
  UserDir "C:/home/"
</IfModule>
```

4. 设置每个用户目录 (`C:/home/username`) 的权限，以便系统上的各个用户可以读取和写入其各自Web目录中的文件。

5. 重启Apache服务器。
现在，你可以通过使用 `http://your_server_name/~username` 来访问用户Web站点。例如，`http://your_server_name/~john` 将访问 `C:/home/john` 目录。

## 性能与可扩展性调优

与任何良好的应用程序一样，Apache可以进行微调，以超越初始配置，获得更高的性能。在这一部分中，我将向你展示如何通过调优配置来加快Apache的速度，你还将学习如何使用多个Apache Web服务器系统来创建一个可扩展的Web服务器网络。

# PART VI

## 本部分包括

**第22章**  
加快Apache的速度

**第23章**  
创建高可用性Web网络

## 加快Apache的速度

如果让我为性能写一个最简单的数学公式，我会写 Performance = f(hardware, software, network, content)，用英语的意思是，性能是硬件、软件、网络和内容的一个函数。虽然这是一个非常广泛的陈述，但它强调了Web服务器的性能无法改进，除非确保你的硬件（即服务器计算机）、软件（Apache服务器、Web应用程序、操作系统）、网络（带宽、延迟）和内容（大小、类型）都经过调优。

本章讨论了如何调优这些性能方面，以便你可以改善整体系统性能。

### 使用高性能硬件

Apache运行在各种计算机上。尽管架构可能大相径庭，但导致性能瓶颈的硬件组件几乎是一样的。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_623_0.png)

顺便说一下，既然你正在阅读关于性能的章节，我假设你当前的Apache系统是一台现代机器。如果你告诉我你使用PC兼容机作为Web服务器，并担心性能问题，我会假设你有一台Pentium级计算机，而不是基于i386的系统。

#### CPU

在分析你的硬件性能需求时，你应该问自己的第一个问题就是：“我的Apache计算机需要一个快速的CPU吗？”答案取决于你如何使用你的Apache服务器。

##### 本章包括

- 受益于高性能硬件
- 调整你的硬盘
- 调整文件系统
- 编译和安装自定义内核
- 调整你的网络
- 调整你的Apache配置
- 为速度而缓存
- 调整基于Perl的Web应用程序

如果服务器主要提供静态HTML页面，你的CPU很可能不会成为一个显著的性能因素。另一方面，如果你使用服务器端包含（SSI）、CGI脚本等生成大量动态内容，你的Apache服务器很可能能很好地利用快速处理器。在这种情况下，获得更快的处理器是明智的。

多快才算够快？没有足够的快：越快越好！然而，你应该知道，如果你处理大量动态内容，仅仅获得一个快速的CPU并没有任何好处。在这种场景中，最可能的性能瓶颈候选者是RAM（在下一节中讨论）。

### RAM

你永远不会拥有足够的RAM，但RAM需要钱。因此，问题就变成了多少RAM能为你带来最佳的性能？你可以通过在负载期间定期监控系统来回答这个问题。例如，在大多数Unix系统上，你可以运行实用程序来监控你的系统性能。图22-1显示了一个广泛可用的名为 `top` 的Unix实用程序的输出。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_624_0.png)

**图22-1**: `top` 程序的输出

像 `top` 这样的程序显示了关于运行系统的大量信息。在这个特定的样本输出中，计算机几乎使用了所有的物理内存（256MB），但尚未使用任何虚拟内存。

> **注意**  
> 如果你在Windows平台上运行Apache，请使用任务管理器程序来监控内存、虚拟内存和CPU使用情况。

在大多数Unix系统上你可以使用的另一个检查系统虚拟内存使用情况的程序是vmstat。图22-2显示了在同一台计算机上一个vmstat会话的样本输出。当你看到你的Web服务器计算机正在使用虚拟内存——即交换空间——你就有内存短缺了！这是一个投资RAM的好时机。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_625_0.png)

**图22-2**: vmstat程序的输出

如果购买更多内存不是一个选项，或者你认为你已经有足够的内存，那么你需要寻找减少RAM使用量的方法。

### 硬盘

你应该考虑的下一个硬件因素，作为影响Web服务器性能的主要因素，是硬盘。Web服务器花费大量时间访问硬盘，而且由于硬盘仍然非常慢，它们往往是糟糕性能的主要原因。

硬盘通常是系统性能的限制因素。因此，为你的系统选择合适的硬盘很重要。一般来说，你有三种驱动技术需要考虑，包括以下内容：

- **EIDE/IDE/ATA:** EIDE/IDE/ATA是最常见的硬盘类型。它们也是我在本部分讨论的三大主要类型中最便宜的。它们也是表现最差的，通常用于家庭或桌面环境，在这些环境中大量的磁盘I/O并不常见。幸运的是，EIDE驱动器正在变得更快，所以这不是一个停滞的技术。

- **SCSI:** SCSI在服务器市场占据主导地位。没有SCSI驱动器的服务器系统对我来说和许多其他经验丰富的服务器管理员来说是不可想象的。

- **光纤通道磁盘:** 光纤通道磁盘是最热门和最新的驱动技术，但由于价格高和互操作性问题，它没有被广泛使用。然而，光纤通道驱动器正在企业或高端存储领域从SCSI那里夺取市场份额。如果你需要光纤通道磁盘，你应该考虑一个非常高端的驱动子系统，例如存储区域网络（SAN）或存储设备。

**注意** 在本章中，我假设你是EIDE或SCSI用户。

#### 理解缩写词

由于驱动技术市场中流行语的变化多端，为系统（桌面或服务器）选择硬盘变得不必要地困难。表22-1定义了一些常见的缩写词和术语，帮助你了解各种技术之间的差异，这些差异通常被市场营销的喧嚣所掩盖。

**表22-1**  
硬盘技术常见缩写词或术语

| 常见缩写词或术语 | 含义 | 标准名称 |
| --- | --- | --- |
| IDE | Integrated Disk Electronics | ATA-1 |
| ATA | AT Attachment。ATA是IDE规范的超集。 |  |
| Fast-IDE或Fast-ATA | 第二代IDE | ATA-2 |
| EIDE | Enhanced IDE - 它提供了对更大驱动器、更多驱动器（四个而不是两个）以及其他大容量存储单元（如磁带和CD-ROM）的支持。 | ATA-3 |
| UltraDMA/33或UDMA/33 | 通过使用快速直接内存访问（DMA）控制器，这种类型的驱动器提供了更快且更不依赖CPU的传输速率。 | ATA-4 |
| ATAPI | ATA Packet Interface - 它是EIDE磁带和CD-ROM驱动器使用的协议；在许多方面类似于SCSI协议。 |  |
| SCSI或窄SCSI | Small Computer System Interface—SCSI的初始实现主要为窄（8位）、单端、同步或异步硬盘设计，与当今的SCSI相比非常有限。它包括以高达5MB/秒的速度进行的同步和异步数据传输。 | SCSI-1 |
| Fast SCSI或Fast-10 | Fast SCSI使用10 MHz总线，而不是窄SCSI使用的5 MHz总线。在8位（窄）SCSI总线上，这将理论最高速度从5MB/秒增加到10MB/秒。在16位（宽）总线上，传输速率可高达20MB/秒。 | SCSI-2 |
| Ultra或Fast-20 SCSI | 同步数据传输选项，允许在总线上进行高达20 MHz的数据时钟，对于16位（宽）总线则为40MB/秒，这被称为Ultra Wide SCSI。 | SCSI-3 |
| Ultra 2或Fast-40 SCSI | 同步数据传输选项，允许在总线上进行高达40 MHz的数据时钟，对于16位（宽）总线则为80MB/秒，这被称为Ultra2 Wide SCSI。 | SCSI-3 |

大多数人要么使用IDE/EIDE硬盘，要么使用SCSI驱动器。很少有人在同一台机器中同时保留这两种类型，这并不是一个问题。

#### 选择硬盘的提示

硬盘性能对Web服务器至关重要，因此，如果你计划运行高需求量的Web服务，你应该考虑高端SCSI磁盘控制器和驱动器。硬盘的可靠性也非常重要；磁盘故障可能是一个恢复起来非常耗时且灾难性的事件。以下是选择Web服务器硬盘时应记住的一些提示。





请确保你的 Web 服务器使用的是高端 SCSI 硬盘控制器以及一套高端 SCSI 硬盘。最新的超宽 SCSI 硬盘是最佳选择。在 Web 服务器上使用多块硬盘是个好主意——例如，你不应该将操作系统和 Web 数据保留在同一块硬盘上。至少使用两块硬盘：一块用于操作系统，另一块用于数据。将操作系统特定的软件与 Web 服务器隔离也是一种良好的安全措施。

硬盘也是常见的故障点。如果你担心硬盘故障，建议定期备份数据。如果预算允许，可以考虑使用廉价磁盘冗余阵列（RAID）子系统，这值得深入研究。RAID 本质上是由一组较小的硬盘组成的集群，它们协同工作以模拟一块大型硬盘。如果其中一块硬盘发生故障，其他硬盘会分担负载，直到故障硬盘被更换。使用 RAID 子系统可以为你的 Web 服务器带来高性能的硬盘 I/O 和合理的数据安全性。

不要误以为慢速硬盘没问题。许多人从供应商那里购买 PC 服务器，被供应商以套餐交易吸引，这些套餐通常配备大容量 IDE 或 EIDE 硬盘。如果你希望服务器不仅仅是个玩具，我强烈建议你避免在 Web 服务器上使用 IDE/EIDE 硬盘。

## 在 Linux 中调整 EIDE/IDE 硬盘

如果你的 Apache 服务器不使用 Linux，可以跳过本节。无论你选择使用 SCSI 还是 IDE 硬盘，如果你重视性能，都必须考虑使用多块硬盘。最低限度，你应该使用两块硬盘——一块用于操作系统和软件，另一块用于数据。对于 Web 服务器，我推荐至少使用三块硬盘，第三块用于存储托管在该机器上的网站生成的日志。将硬盘 I/O 分散在多个设备上可以确保等待时间最小化。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_628_0.png)

> 如果有预算，你可以使用光纤通道硬盘或采用存储区域网络（SAN）解决方案。后者通常用于对数据存储有较高需求的企业。你也可以选择硬件/软件 RAID 解决方案，本章对此进行了讨论。

你可以从现代 EIDE 硬盘中获得更好的性能。首先，在任何调整之前，你必须确定硬盘当前的性能状况，因此你需要一个工具来测量当前硬盘子系统的性能。`hdparm` 工具正适合这项工作；你可以从 http://metalab.unc.edu/pub/Linux/system/hardware 下载该工具的源代码发行版。按照以下步骤编译并安装它：

- 以 root 身份，将源代码发行版解压到合适的目录，例如 /usr/local/src。例如，我在 /usr/local/src 目录下运行 `tar xvzf hddparm-3.9.tar.gz` 命令来解压 hddparm 版本 3.9 的源代码发行版。
- 进入新创建的子目录，运行 `make install` 命令来编译并安装 `hddparm` 二进制文件和手册页。默认情况下，二进制文件安装在 /usr/local/sbin 目录中，并被命名为 `hddparm`。

**注意**

因为 `hdparm` 允许你更改 IDE/EIDE 硬盘子系统的行为，所以不当使用或配置错误有时会导致系统挂起。我强烈建议在使用 `hdparm` 之前备份你的数据。此外，在单用户模式下测试 `hdparm` 是个非常好的主意，这样在你操作时就没有其他用户在使用硬盘。你可以在启动时，在 lilo 提示符下输入 `linux single` 来重启系统并强制其进入单用户模式。

## 使用 hdparm 检查硬盘设置

安装 `hdparm` 工具后，你就可以开始调查硬盘子系统的性能状态。假设你的 IDE 或 EIDE 硬盘是 `/dev/hda`，运行以下命令来检查硬盘配置的状态：

```bash
hdparm /dev/hda
```

你应该看到类似这样的输出：

```
/dev/hda:
 multcount    = 0 (off)
 I/O support  = 0 (default 16 bit)
 unmaskirq    = 0 (off)
 using_dma    = 0 (off)
 keepsettings = 0 (off)
 nowerr       = 0 (off)
 readonly     = 0 (off)
 readhead     = 8 (on)
 geometry     = 2494/255/63, sectors = 40079088, start = 0
```

如你所见，默认模式下几乎所有设置都是关闭的。为了提高硬盘性能，需要更改其中一些默认值。在继续之前，还需要从硬盘获取更多信息。运行以下命令：

```bash
hdparm -i /dev/hda
```

上述命令显示上次系统启动时可用的硬盘标识信息（如果有）。稍后你将使用此命令显示的部分信息。这里，该命令报告了型号、配置、硬盘几何参数（柱面、磁头、扇区）、轨道大小、扇区大小、缓冲区大小、支持的 DMA 模式、PIO 模式等。使用以下命令测试硬盘子系统：

```
/dev/hda:
 Model=WDC WD205AA, FwRev=05.05B05, SerialNo=WD-WMAA015136037
 Config| HardSector NotMFM HdSig>15/15Sec SpinMotCtl1 Fixed DTR>5MB FmtGapReq |
 RawCHS=16383/16/63, TrkSize=57600, SektSize=600, ECCbytes=40
 BuffType=DualPortCache, BuffSize=2048KB, MaxMultSect=16, MultSect=16
 CurCHS=16383/16/63, CurSects=16514064, LBA=yes, LBAsects=40079088
 IORDY=on/off, tPID=[min:120,w/IORDY:120], tDMA=[min:120,rec:120]
 PIO modes: pio0 pio1 pio2 pio3 pio4
 DMA modes: mdma0 mdma1 *mdma2 udma0 udma1 udma2 udma3 udma4
```

这里该命令报告了型号、配置、硬盘几何参数（柱面、磁头、扇区）、轨道大小、扇区大小、缓冲区大小、支持的 DMA 模式、PIO 模式等。现在，让我们使用以下命令测试磁盘子系统：

```bash
/usr/local/sbin/hdparm -Tt /dev/hda
```

你将看到类似这样的结果：

```
/dev/hda:
Timing buffered-cache reads: 128 MB in 1.01 seconds = 126.73 MB/sec
Timing buffered disk reads: 64 MB in 17.27 seconds = 3.71 MB/sec
```

当然，根据你的硬盘和控制器子系统不同，你的数值会有所不同。但是，这是你的硬盘子系统的未调整状态。`-T` 选项告诉 `hdparm` 测试缓存子系统（即内存、CPU 和缓冲区缓存）。`-t` 告诉 `hdparm` 通过读取不在缓存中的数据来报告硬盘（`/dev/hda`）的统计数据。多运行几次此命令，并计算报告的硬盘 MB/sec 的平均值。这大致是你的硬盘子系统的性能状态。在这个例子中，3.71 MB/sec 是读取性能，这个值相当低。

## 调整硬盘的多扇区模式

回顾 `hdparm -i /dev/hda` 命令的输出，查找 `MaxMultiSect` 值。在这个例子中，它是 16。回想一下，`hdparm /dev/hda` 命令显示 `multcount` 值为 `0`（关闭）。这意味着多扇区模式（即 IDE 块模式）是关闭的。

> **注**
>
> *多扇区模式是大多数现代 IDE 硬盘的一项功能。它允许硬盘在每次 I/O 中断时传输多个扇区。默认情况下它是关闭的。然而，大多数现代硬盘可以在每次 I/O 中断时传输 2、4、8 或 16 个扇区。因此，如果你将此模式设置为硬盘支持的最大值（由 `MaxMultiSect` 值显示），你应该看到吞吐量增加 5% 到 50% 甚至更多。此外，你还可以将操作系统开销减少 30% 到 50%。*

在这个例子中，`MaxMultiSect` 值为 16，因此我们可以使用 `hdparm` 工具的 `-m` 选项来设置该值，并查看性能如何提升。运行以下命令：

```bash
/usr/local/sbin/hdparm -m16 /dev/hda
```

通过使用 `hdparm` 的 `-t` `/dev/hda` 命令运行性能测试来显示变化。对于示例系统，变化如下：

```
/dev/hda:
Timing buffer-cache reads:   128 MB in  1.01 seconds = 126.73 MB/sec
Timing buffered disk reads:  64 MB in 16.53 seconds =   3.87 MB/sec
```

硬盘的性能从 3.71 MB/sec 提升到了 3.87 MB/sec。提升不多，但也不算差。也许你也类似地看到了一些变化。如果你的硬盘和控制器比较新，你完全有可能获得比这好得多的性能。你可能会达到 20 到 30MB/秒！然而，请预先警告，在使用 `hdparm` 进行探索时，你可能会损坏数据，因此，如前所述，在测试下文讨论的硬盘硬件特定选项之前，请备份你的数据。

如果 `hdparm` 报告你的系统 I/O 支持设置为 16 位，且你拥有较新的（一两年内购买的）硬盘子系统，你应该尝试 32 位 I/O 支持。你可以使用 `hdparm` 的 `-c` 选项来设置此功能。该选项有三个值：

- `0`—启用默认 16 位 I/O 支持
- `1`—启用 32 位支持
- `3`—启用 32 位支持，并附带许多 IDE/EIDE 芯片组所需的特殊同步序列。这也是大多数系统兼容性较好的值。

按以下方式设置选项：

```bash
/usr/local/sbin/hdparm -m16 -c3 /dev/hda
```

注意使用了之前的 `-m16` 选项，并添加了启用 32 位 I/O 支持的 `-c3`。使用 `-t` 选项运行该程序显示以下结果：

```
/dev/hda:
Timing buffered disk reads:  64 MB in  8.96 seconds =   7.14 MB/sec
```

硬盘子系统的性能几乎翻倍了！

## 为硬盘启用直接内存访问（DMA）

如果你的硬盘支持直接内存访问（DMA），你可能可以使用 `-d` 选项来启用 DMA 模式。

通常，`-d1 -X32` 选项或 `-d1 -X66` 选项一起使用，以利用你硬盘子系统的 DMA 功能。第一组选项（`-d1 -X32`）为硬盘启用多字 DMA 模式 2，下一组选项



选项（-d -X66）为支持 UltraDMA 突发时序特性的驱动器启用 UltraDMA 模式 2。这些选项可以显著提高驱动器性能。我在各种新的 EIDE/ATA 驱动器上使用这些选项时，曾看到 20 MB/sec 的传输速率。

还有另一个选项 -u，它对提高整体系统性能非常有用。该选项允许驱动器驱动程序在处理驱动器中断期间屏蔽其他中断，这意味着操作系统可以在等待基于驱动器的数据传输完成的同时，处理其他中断，例如网络 I/O 或串行 I/O。

你可以使用 hdparm 设置和实验许多其他选项；然而，对大多数选项务必非常谨慎，因为很有可能会损坏数据。在玩弄 hdparm 工具之前，始终先备份数据。此外，当你发现一组选项效果良好后，你应该将带有选项的 hdparm 命令放入 /etc/rc.d/rc.local 脚本中，以便每次启动系统时都会设置这些选项。例如，在我较新的一个 Linux 系统的 /etc/rc.d/rc.local 文件中，我添加了以下行：

```
hdparm -m16 -c3 -u -d -X66 /dev/hda
```

现在你已经优化了硬盘以获得更好的性能，让我们看看如何优化作为驱动器接口的文件系统。由于 Red Hat Linux 使用 ext2 文件系统，我将在下面“调整 Linux 的 ext2 文件系统”一节中讨论其调整问题。

## 以太网卡

驻留在你的计算机系统中且可能影响服务器性能的最后一个硬件部件是网络适配器卡。我假设你的 Web 服务器将连接到某个以太网网络。你使用的适配器卡应该是质量较高且速度快的。例如，如果你将 Web 服务器连接到处理 10Mbps 或 100Mbps 节点的以太网，请从知名厂商获取一张 100Mbps 适配器卡。

本章网络部分将讨论可能影响服务器性能的其他硬件。

## 调整 Linux 的 ext2 文件系统

如果你不使用 Linux 作为 Apache 服务器，可以跳过本节。它不是世界上最好的文件系统，但工作还算合理。多年来，ext2 文件系统一直是 Linux 事实上的标准文件系统，因此本书涵盖的就是这个文件系统。

### 更改 ext2 文件系统的块大小

提高 ext2 文件系统性能的方法之一是将默认块大小从 1024 更改为 1024 的倍数（通常小于 4096），适用于主要包含大文件的服务器。要了解特定 ext2 分区上有哪些类型的文件，请执行以下操作：

- 1. 以 root 身份登录，切换到 ext2 分区的顶层目录。
- 2. 运行以下命令，这实际上是一个使用 `find` 和 `awk` 实用程序的小型脚本。此命令行脚本将显示所有文件及其大小，并最终提供整个分区的总大小和平均大小。

```
find . -type f -exec ls -l {} \; | \
awk 'BEGIN {tsize=0;fcnt=1;} \
{ printf("%03d File: %6d size: %d bytes\n",fcnt++, $9,
$5); \
tsize += $5;} \
END { printf("Total size = %d\nAverage file size = %.02f\n",
tsize, tsize/fcnt);}'
```

- 3. 知道了文件系统的平均大小后，你可以决定是否应该更改块大小。如果你发现平均文件大小为 8192，即 $2 \times 4096$，你可以将块大小更改为 4096。
- 4. 不幸的是，如果不重建现有 ext2 文件系统，你就无法更改其块大小。因此，你必须备份文件系统上的所有文件，然后使用 `/sbin/mke2fs /dev/partition -b 4096` 命令重建文件系统。例如，如果你已经备份了 `/dev/hda7` 分区并希望将块大小更改为 4096，请使用 `/sbin/mke2fs /dev/hda7 -b 4096` 命令。

将块大小更改为比默认值（1024）更大的数值可能会因寻道次数减少而显著提高原始读取速度，还因为启动期间的 `fsck` 会话可能更快，文件碎片可能更少，以及其他原因。然而，盲目地增加块大小（即在没有了解平均文件大小的情况下）可能会导致空间浪费。如果平均文件大小为 2010 字节，而系统使用 4096 字节的块，则每个文件平均将浪费 2086 字节（4096 − 2010）！所以在折腾块大小之前要清楚你的文件大小。

### 使用 e2fsprogs 调整 ext2 文件系统

可以使用 e2fsprogs 套件调整默认 ext2 文件系统。在本节中，我将讨论如何安装这套程序以及如何使用它们进行调整、执行例常检查和修复磁盘。

### 安装 *e2fsprogs*

为了调整 ext2 文件系统，你需要如下安装 *e2fsprogs* 实用程序包：

- 1. 从 `www.rpmfind.net` 下载 `e2fsprogs-version.src.rpm`（将 `version` 替换为最新版本号）源分发版。我下载了 `e2fsprogs-1.19-0.src.rpm` 包。你也可以从 *e2fsprogs* 项目站点 `http://e2fsprogs.sourceforge.net` 获取源代码。
- 2. 运行 `rpm -ivh e2fsprogs-version.src.rpm` 命令将源代码提取到 `~/usr/src/redhat/SOURCES/` 目录中。源代码 RPM 会生成一个 `e2fsprogs-version.tar.gz` 文件，需要使用 `tar xvzf e2fsprogs-version.tar.gz` 命令进行解包。这将创建一个名为 `e2fsprogs-version` 的子目录。
- 3. 切换到新的子目录。
- 4. 运行 `mkdir build` 创建一个新子目录，然后切换到该目录。
- 5. 运行 `../configure` 脚本以配置源树。
- 6. 运行 `make` 实用程序以创建二进制文件。
- 7. 运行 `make check` 命令以确保所有组件正确构建。
- 8. 运行 `make install` 命令以安装二进制文件。

安装 *e2fsprogs* 实用程序后，你就可以开始使用它们，如下节所述。

### 使用 `tune2fs` 调整你的文件系统

你可以使用 `tune2fs` 实用程序来调整 ext2 文件系统的各个方面。

> 你永远不应在已挂载的 ext2 文件系统上应用 ext2 实用程序，并且在修改属于文件系统的任何内容时，始终应备份你的数据。

下面部分讨论了如何使用 `tune2fs` 实用程序（*e2fsprogs* 包的一部分）来调整名为 `/dev/hda7` 的未挂载 ext2 文件系统。如果你使用下面讨论的一个或多个设置，请别忘了将分区名称（`/dev/hda7`）更改为适当的名称。首先，让我们运行以下命令来查看 `tune2fs` 显示的未挂载 `/dev/hda7` 的当前设置：

```
/sbin/tune2fs -l /dev/hda7
```

输出应与以下内容类似：

```
tune2fs 1.19, 13-Jul-2000 for EXT2 FS 0.5b, 95/08/09
Filesystem volume name:   <none>
Last mounted on:          <not available>
Filesystem UUID: 5d06c65b-dd11-4df4-9230-a10f2da783f8
Filesystem magic number: 0xEF53
Filesystem revision #: 1 (dynamic)
Filesystem features: filetype sparse_super
Filesystem state: clean
Errors behavior: Continue
Filesystem OS type: Linux
Inode count: 1684480
Block count: 13470471
Reserved block count: 673523
Free blocks: 13225778
Free inodes: 1674469
First block: 1
Block size: 1024
Fragment size: 1024
Blocks per group: 8192
Fragments per group: 8192
Inodes per group: 1024
Inode blocks per group: 128
Last mount time: Thu Feb 15 17:51:19 2001
Last write time: Thu Feb 15 17:51:51 2001
Mount count: 1
Maximum mount count: 20
Last checked: Thu Feb 15 17:50:23 2001
Check interval: 155520000 (6 months)
Next check after: Tue Aug 14 18:50:23 2001
Reserved blocks uid: 0 (user root)
Reserved blocks gid: 0 (group root)
First inode: 11
Inode size: 128
```

我在以下列表中讨论的设置在上述部分中以粗体显示：

- **错误处理行为（Errors behavior）：** 此设置决定了内核在检测到文件系统**错误**时的行为。此设置有三个可能的值——*继续（continue）*、*重新挂载为只读（remount-ro）*。换句话说，默认设置是即使有错误也继续运行。
- **挂载计数（Mount count）：** 你挂载此文件系统的次数。
- **最大挂载计数（Maximum mount count）：** 这意味着在达到最大读/写模式挂载次数后，文件系统将在下一个启动周期中接受 *fsck* 检查会话。
- **最后检查（Last checked）：** 此设置显示执行 *fsck 检查* 的最后日期。这是两次连续 *fsck 会话* 之间的检查间隔。
- **检查间隔（Check interval）：** 这仅用于在间隔期间未达到最大读/写挂载计数的情况。换句话说，如果你 6 个月不卸载文件系统，那么即使挂载计数仅为 2，*fsck* 检查也将被强制执行，因为文件系统超过了检查间隔。
- **下次检查日期（Next check after）：** 这是**下次 fsck** 检查日期。





## 保留块 UID 和保留块 GID
这些设置显示了文件系统的保留部分由哪个用户和组所有。默认情况下，保留部分由 root（UID = 0，GID = 0）使用。

对于未挂载的文件系统（如 /dev/hda7），你可以通过使用 tune2fs 的 -c 选项将最大读写挂载计数更改为更适合你需求的值。例如，`/sbin/tune2fs -c 1 /dev/hda7` 将在每次启动系统时强制对文件系统执行 fsck 检查。你还可以使用 -i 选项更改基于时间的 fsck 检查强制执行计划。例如，`/sbin/tune2fs --itd /dev/hda7` 命令确保如果文件系统在一周后以读写模式重新挂载，则强制执行 fsck 检查。类似地，`/sbin/tune2fs --i0 /dev/hda7` 命令禁用了基于时间的 fsck 检查。

## 使用 e2fsck 检查和修复 ext2 文件系统
如果你的 ext2 文件系统已损坏，你可以使用 e2fsck 工具尝试修复它。要使用 e2fsck 检查分区，你必须先卸载该分区，并运行 `/sbin/e2fsck /dev/device` 命令，其中 /dev/device 是你的硬盘设备。例如，要强制对名为 /dev/hda7 的设备执行 fsck 检查，请使用 `/sbin/e2fsck -f /dev/hda7` 命令。此类检查可能会显示如下所示的输出：

```
e2fsck 1.19, 13-Jul-2000 for EXT2 FS 0.5b, 95/08/09
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/hda7: 12/1684256 files (0.0% non-contiguous), 52897/3367617 blocks
```

e2fsck 工具会询问修复问题，你可以通过使用 -p 选项来避免这些问题。

# 调优你的操作系统

Apache 运行在许多不同的操作系统上。你应该查阅操作系统的用户手册，了解如何对其进行微调以获得更高的性能。由于 Apache 在 Linux 平台上是最流行的组合，我将讨论如何调优 Linux 以获得更高的性能。如果你不使用 Linux，应该跳过本节。

如果你安装的是 Red Hat 提供的原始内核，那么它很可能没有针对你的系统进行优化。通常，当你安装供应商提供的内核时，它是为了支持大多数安装场景而创建的。例如，一个原始内核可能同时支持 EIDE 和 SCSI 驱动，而你可能只需要 SCSI 支持或 EIDE 支持。这就是为什么从供应商提供的内核开始启动系统是个好主意，并且一旦你有时间，就可以进行自定义内核编译和安装过程，这正是本章的主题。

## 编译和安装自定义内核
构建自定义内核的目标是细调你的内核，使其完全满足你的需求。感谢 Linux 内核开发人员，在 Linux 中创建自定义内核易如反掌。Linux 内核在设计上是模块化的，这意味着你想要的大部分内容都可以作为单独的内核模块安装。但是重新编译内核超出了本书的范围。如果你需要知道如何重新编译内核，请参见 `http://www.kernel.org` 获取详细信息。

## 为具有挑战性的 Web 应用程序调优系统
精简且高效的内核可能是运行大量使用资源且具有挑战性应用程序的良好候选者。根据我的经验，这类应用程序通常不适合原始内核或其他资源配置。

例如，多线程邮件服务器可以从消息队列中打开成千上万个文件，并可能耗尽文件句柄或启动过多的线程以达到系统的并发进程容量。这两个问题经常出现，因此我将展示如何克服它们。

### 控制最大打开文件句柄数
*文件句柄* 是用于指向已打开文件的系统资源。任何系统只能拥有特定数量的打开文件句柄。可以同时打开的文件句柄的最大数量通常控制着你的系统在高负载场景下的行为。在接下来的章节中，我将讨论如何确定并设置基于 Linux 的 Web 服务器的最大文件句柄数。

### 发行版版本和内核版本的混淆
许多 Linux 新手会感到困惑，因为发行版版本和内核版本不同。例如，我经常被问到为什么我谈论 Linux 2.4，而市场上提供的是 7x。得益于 Red Hat Linux 等流行发行版，许多新手认为 Red Hat Linux 7.x *发行版* 是 Linux 的最新版本，并因此认为该发行版内的一切也是 7x。2.4 是 Linux 内核的最新版本，因此每当我提到 2.4 时，我会说“Linux 内核 2.4”以便尽可能清晰。

## 确定系统的文件句柄限制
要确定整个系统可以拥有的文件句柄数量，请运行 `cat /proc/sys/fs/file-max` 命令。你应该看到诸如 4096 或 8192 这样的数字。要将文件句柄（通常称为文件描述符）数量增加到 *n*nn，只需将以下行添加到你的 `/etc/rc.d/rc.local` 脚本中：

```bash
# Don't forget to replace nn with an appropriate number
echo nn > /proc/sys/fs/file-max
```

例如：

```bash
echo 10240 > /proc/sys/fs/file-max
```

此处，系统范围内的文件句柄总数现在将是 10240（10K）。

## 设置每处理器的文件句柄限制
例如，将每进程文件句柄限制设置为 8192，将确保当用户登录时，该用户可以在用户控制的程序中打开多达 8,192 个文件。要设置每进程文件句柄限制，请执行以下操作：

1. 编辑 `/etc/security/limits.conf` 文件并向其中添加以下行：
   - `soft    nofile   1024`
   - `hard    nofile   8192`
2. 确保你的 `/etc/pam.d/system-auth` 文件包含如下所示的行：
   - `session   required   /lib/security/pam_limits.so`

## 允许用户运行更少的进程
例如，要允许用户运行更少的进程（最多 8,192 个），请将以下行添加到 `/etc/security/limits.conf` 文件。

```
*      soft    nproc    4096
*      hard    nproc    8192
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_638_0.png)

此设置将应用于进程以及每个进程打开的子线程。你还可以使用同一文件中的 `soft` 和 `hard` 限制设置来配置用户可以消耗多少内存。内存消耗通过使用 `data`、`memlock`、`rss`、`stack` 和类似的指令来控制。你还可以控制用户的 CPU 使用率。有关详细信息，请参见文件中的注释。

## 让你的 Apache 服务器精简且高效
当你确定在强大的硬件上运行了一个精简且高效的操作系统后，你可以开始查看其他软件“位置”以寻找性能瓶颈。Apache 服务器本身呢？它可能成为你的 Web 服务的瓶颈吗？确实有可能。如果你没有从源代码自定义编译和构建 Apache 服务器，那么你可能内置了不必要的模块，这些模块占用内存并浪费你的系统资源。

## 了解单个用户能使用的资源
每个系统都有有限数量的可用系统资源。能够控制单个用户可以使用多少资源非常重要，这样你就可以根据需要限制或扩展他们的资源容量。要查看用户可以消耗哪些类型的系统资源，请运行 ulimit -a（假设你正在使用 bash shell）。下面显示了一个示例输出（打开文件句柄和最大用户进程行以粗体显示）：

```
core file size (blocks)             1000000
data seg size (kbytes)             unlimited
file size (blocks)                 unlimited
max locked memory (kbytes)         unlimited
max memory size (kbytes)           unlimited
open files                         1024
pipe size (512 bytes)              8
stack size (kbytes)                8192
cpu time (seconds)                 unlimited
max user processes                 12287
virtual memory (kbytes)            unlimited
```

如第 2 章所述，获取 Apache 有两种方式。你可以下载二进制发行版并将其安装到你的系统中，或者你可以编译自己的 Apache 二进制文件并安装。强烈建议采用后一种方法，因为它允许你从一开始就细调 Apache。检查你当前拥有的二进制文件，并确定你是否需要它提供的所有功能。运行诸如

```
httpd -l
```

这样的命令，这将显示已内置到你的当前 Apache 可执行文件中的所有模块。如果你看到你不需要的东西，请通过运行带有适当命令行选项的 `configure` 脚本将其移除。例如，如果你不打算使用 CGI 脚本或 SSLs，你可以安全地从 Apache 中移除这些选项，首先从源代码发行版目录运行以下命令：

```bash
./configure --prefix=/usr/local/apache \
--disable-cgi --disable-cgid \
--disable-include
```

然后使用 `make && make install` 命令重新编译和重新安装 Apache。如果你的操作系统允许你从可执行文件中移除不必要的符号信息并将其剥离，那么你可以节省更多内存。例如，以下命令

```
strip httpd
```




## 调优您的网络

当您已经将服务器硬件、操作系统以及 Apache 服务器本身针对性能进行了调优之后，下一个典型的瓶颈领域就是网络本身。

要调优您的网络，您必须了解网络架构。大多数 Web 服务器都运行在以太网环境中——无论是在办公室网络中，还是在 ISP 的托管设施中。该网络的配置方式会带来巨大的差异。例如，如果您将一台 Apache 服务器连接到一个以太网集线器，而该集线器又连接到其他连接到工作站或服务器的集线器，那么您就创造了一个主要瓶颈的温床。每台机器都会看到网络上的所有流量；数据包冲突的数量增加，网络变慢的情况也更为常见。然而，这种瓶颈很容易通过使用网络交换机来替代集线器得到解决。

连接到以太网交换机的设备不需要特殊的硬件。用于共享介质 10Base-T 集线器的相同网络接口也能与以太网交换机配合使用。从该设备的角度来看，连接到交换端口就像它是网络段中唯一的计算机一样。

以太网交换机的一个常见用途是将大型网络划分为不同的段。虽然可以将每台单独的计算机连接到以太网交换机上的每个端口，但也可以连接其他设备，例如集线器。如果您的网络大到需要多个集线器，您可以将每个集线器连接到一个交换机端口，这样每个集线器就是一个独立的段。请记住，如果您只是直接级联集线器，那么组合后的网络就是一个单一的逻辑以太网段。

### 使用快速以太网

传统的以太网速度为 10MB/sec，这显然不足以应对包含基于电子邮件的通信、互联网访问、视频会议以及其他带宽密集型操作的现代商业环境。100MB/sec 的以太网是前进的方向。然而，如果您决定采用快速交换机，100 MB/sec 或“快速”以太网仍然相当昂贵。我建议您从现在开始转向交换式快速以太网，除非您已经这样做了。如果您网络中有大量计算机，从 10MB/sec 迁移到 100MB/sec 可能会相当昂贵。您网络中的每台计算机都必须安装具备 100MB/sec 能力的网卡，这在成本、人员和时间方面可能都很昂贵。对于拥有几百或更多用户的大型局域网（LAN），您应该一次升级一个段。您可以先购买 10/100MB 双速网卡，这将使您能够无缝支持现有的 10MB/sec 和即将部署的 100MB/sec 基础设施。

将快速以太网与交换硬件结合使用可以为您的局域网带来高性能。如果可能，您应该肯定考虑这一选项。如果您有多个部门需要互连，请考虑在部门之间使用更快的解决方案：新兴的 Gbit/sec 以太网标准非常适合将局域网连接起来以形成广域网（WAN）。

## 理解并控制网络流量

理解您的网络流量是如何流动的，是确定如何调优它以获得更好性能的主要关键。请查看图 22-3 中显示的网络段。

## 区分您的集线器和交换机

以太网集线器与交换机之间的主要区别在于，交换机上的每个端口都是其自身的逻辑段。连接到以太网交换机端口的计算机拥有完整的带宽，无需与其他计算机竞争。购买交换机而非集线器的一个主要原因在于其地址处理能力。集线器不会查看数据包的地址，只是将数据转发到网络上的所有设备；而交换机则应该读取每个数据包的地址，并将数据正确地转发给预期的接收者。如果交换机不能正确读取数据包地址并正确转发数据，那么它相对于集线器就没有优势。下表列出了集线器和交换机之间的主要区别。

| 特性 | 以太网集线器 | 以太网交换机 |
| :--- | :--- | :--- |
| **带宽** | 整个网络的带宽受限于集线器的速度，即，10Base-T 集线器提供 10MB 的带宽，无论存在多少个端口。 | 整个网络的带宽由交换机上的端口数量决定，即，12 端口的 100MB 交换机最多可以支持 1200MB/sec 的带宽——这被称为交换机的最大聚合带宽。 |
| **双工能力** | 支持半双工通信，将连接限制在端口的速度，即，10MB 端口提供 10MB 的链路。 | 支持全双工通信的交换机提供了将每个链路的速度从 100MB 翻倍到 200MB 的能力。 |
| **互连** | 跳数规则限制了两个计算机之间可以互连的集线器数量。 | 允许用户极大地扩展网络；两个计算机之间可以互连的交换机数量没有限制。 |
| **成本** | 比交换机便宜。 | 比集线器贵，但性能/价格比值得这个较高的价格。 |

![](img/e11fcbd2818a3495ac70085e5d8d1c26_642_0.png)

图 22-3：一个低效的 Web 网络

在这里，三台 Web 服务器正在向互联网提供 Web 服务，它们与一个 NFS 服务器和一个数据库服务器共享网络。这张图中有什么错误？嗯，有几个地方不对。首先，这些机器仍然在使用笨集的集线器而不是交换机。其次，NFS 和数据库流量正在与传入和传出的 Web 流量竞争。如果一个 Web 应用程序需要响应 Web 请求而访问数据库，它会产生一个或多个数据库请求，进而占用了其他传入或传出 Web 请求可用的带宽，实际上使得网络不必要地繁忙或响应速度变慢。

如何解决这个问题？当然通过流量控制机制！首先确定在此网络中可以隔离哪些流量。自然，数据库和 NFS 流量仅用于服务 Web 服务器。在这种情况下，应隔离 NFS 和数据库流量，以免它们与 Web 流量竞争。图 22-4 显示了相同网络的修改后的网络图。

在这里，数据库和 NFS 服务器连接到交换机，该交换机又连接到每台 Web 服务器的第二网卡。每台 Web 服务器的另一个网卡连接到交换机，该交换机进而连接到负载均衡硬件。现在，当 Web 请求到达 Web 服务器时，该服务器提供服务，而不会占用其他 Web 服务器的带宽。结果是网络效率的巨大提升，进而带来更积极的用户体验。

在您有了良好的网络设计之后，您的调优重点应转移到您提供的应用程序和服务上。根据网络负载，您可能需要考虑部署多台同类型的服务器以实现更具响应性的服务。对于 Web 来说，情况肯定如此。下一节将讨论如何通过使用 DNS 技巧来部署简单的负载均衡方案。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_643_0.png)

图 22-4：改进后的 Web 网络

## 使用 DNS 服务器进行负载均衡

其思想是在同类型的多台服务器之间共享负载。这通常用于在多台 Web 服务器之间平衡 Web 流量。这种技巧称为轮询域名服务（round-robin Domain Name Service）。

假设您有两台 Web 服务器，www1.yourdomain.com (192.168.1.10) 和 www2.yourdomain.com (192.168.1.20)，您想使用轮询 DNS 技巧在这两台服务器上平衡 www.yourdomain.com 的负载。请在您的 yourdomain.com 区域文件中添加以下行：

```
www1    IN    A    192.168.1.10
www2    IN    A    192.168.1.20

www     IN    CNAME    www1
www     IN    CNAME    www2
```

重新启动您的名称服务器并对 www.yourdomain.com 主机进行 ping。您将看到 ping 输出中的 192.168.1.10 地址。停止并重新启动对同一主机的 ping，您会看到正在 ping 的是第二个 IP 地址，因为前面的配置告诉名称服务器循环遍历 www 的 CNAME 记录。换句话说，www.yourdomain.com 主机既是 www1.yourdomain.com 也是 www2.yourdomain.com。

现在，当有人输入 www.yourdomain.com 时，名称服务器发出第一个地址一次，然后对下一个请求发出第二个地址，并持续在这些地址之间循环。





![](img/e11fcbd2818a3495ac70085e5d8d1c26_644_0.png)

轮询 DNS 技巧的一个缺点是，名称服务器无法得知哪个系统负载较重，哪个系统负载较轻——它只是盲目地轮询。如果其中一台服务器崩溃或因某些原因变得不可用，轮询 DNS 技巧仍会定期返回该故障服务器的 IP 地址。这可能会导致相当混乱的情况，因为有些人可能能够访问该站点，而有些人则无法访问。

## 使用负载均衡硬件

如果你的负载需求更智能的负载分配，并且检查服务器健康状况非常重要，那么最好的选择是获取使用新型调度器产品的硬件解决方案，例如 Web Director (www.radware.com)、Ace Director (www.alteon.com) 或 Local Director (www.cisco.com)。

图 22-5 展示了一个 Web 网络，该网络由两台 CISCO Local Director 组成；一组代理服务器；Apache Web 服务器；`mod_perl`、PHP、Java Servlet 应用程序服务器；以及数据库服务器。

此网络中托管的所有 Web 域名都指向一个虚拟 IP 地址，该地址解析到 Local Director。Local Director 利用其配置和它收集的服务器健康信息，来确定从何处获取内容。第二台 Local Director 仅作为备份，以防主服务器故障。当两台 Local Director 通过专用电缆连接时，Local Director 允许执行状态恢复。如果主服务器故障，则备用服务器可以接管，而外部世界任何人都不会察觉或收到任何错误。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_644_1.png)

如果你非常看重 Web 网络的可靠性，请确保没有单点故障。例如，如果你使用数据库服务器，请确保你有另一个数据库服务器，它尽可能接近实时地复制数据，以便你能够从数据库崩溃中恢复。

## 调优 Apache 配置

在配置好硬件、操作系统、网络和 Apache 软件本身（所有这些过程都在本章前面讨论过）之后，你准备就绪，可以调优 Apache 配置。以下部分讨论了一些你可以轻松应用的调优选项，以提高服务器性能。

### 最小化 DNS 查找

如果将 `HostnameLookups` 指令设置为 `On`，Apache 将对每个请求执行 DNS 查找，以将 IP 地址解析为主机名。这会大大降低你的服务器性能。因此，你应该认真考虑不针对每个请求使用主机查找。请在 `httpd.conf` 中将 `HostnameLookups` 设置为 `Off`。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_645_0.png)

图 22-5：使用 Local Director 进行负载均衡的 Web 网络。

如果你必须出于日志处理目的将 IP 地址解析为主机名，请改用 logresolve 工具。详见第 8 章。

## 加速静态文件服务

尽管所有人都在高喊关于动态 Web 内容的话题，这些内容由数据库驱动或由花哨的应用程序服务器提供，但静态 Web 页面依然存在。事实上，在不久的将来，动态内容不太可能完全取代静态 Web 页面，因为提供静态页面通常比提供动态页面更快。一些动态内容系统甚至动态且定期生成静态 Web 页面作为缓存内容，以实现更快的交付。本节讨论如何使用 Apache 和 Linux 内核 HTTP 模块来提高静态页面交付速度。

### 减少磁盘 I/O 以实现更快的静态页面交付

当 Apache 收到对静态 Web 页面的请求时，它会执行目录树搜索以查找 .htaccess 文件，以确保所请求的页面可以交付给 Web 浏览器。例如，如果运行在 www.nitec.com 上的 Apache 服务器收到诸如 `http://www.nitec.com/training/linux/sysad/intro.html` 这样的请求，Apache 将执行以下检查：

```text
/.htaccess
%DocRoot%/.htaccess
%DocRoot%/training/.htaccess
%DocRoot%/training/linux/.htaccess
%DocRoot%/training/linux/sysad/.htaccess
```

*%DocRoot* 是 httpd.conf 文件中由 *DocumentRoot* 指令设置的文档根目录。因此，如果该目录是 /www/nitec/htdocs，则进行以下检查：

```text
/.htaccess
/www/.htaccess
/www/nitec/.htaccess
/www/nitec/htdocs/.htaccess
/www/nitec/htdocs/training/.htaccess
/www/nitec/htdocs/training/linux/.htaccess
/www/nitec/htdocs/training/linux/sysad/.htaccess
```

Apache 在所请求文件（intro.html）的已翻译（从所请求的 URL 翻译而来）路径中的每个目录中查找 .htaccess 文件。正如你所见，请求单个文件的 URL 可能会导致多个磁盘 I/O 请求以读取多个文件。对于高流量站点，这可能是一个性能消耗因素。在这种情况下，你最好的选择是完全禁用 .htaccess 文件检查。例如，当以下配置指令放置在 httpd.conf 文件的主服务器部分（即不在 *VirtualHost* 指令内）时，它将禁用每个 URL 请求的 .htaccess 检查。

```text
<Directory />
  AllowOverride None
</Directory>
```

使用上述配置时，Apache 将仅执行一次磁盘 I/O 来读取所请求的静态文件，从而在高流量访问场景中提升性能。

### 减少符号链接的系统调用和磁盘 I/O

在运行 Apache 的 Unix 和类 Unix 系统上，符号链接存在危险。通过使用放置不当的符号链接，Web 用户可以查看本不应通过 Web 访问的文件和目录。这就是为什么 Apache 提供了一种方法来禁用符号链接，或者仅在符号链接的 user ID 与服务器自身的 user ID 匹配时才跟随符号链接。例如，在 `httpd.conf` 的主服务器部分（即在任何虚拟主机配置之外）使用以下配置将指示 Apache 不跟随符号链接，从而有效地禁用了通过 Web 的所有符号链接访问。

```text
<Directory />
    Options -FollowSymLinks
</Directory>
```

不幸的是，这伴随着巨大的性能代价。对于每个请求，Apache 会执行额外的系统调用 `lstat()`，以确保它没有违反你不跟随符号链接的策略。

为了在拥有符号链接和良好安全性的同时提高性能，请执行以下操作：

- 1. 寻找一种方法在你的 Web 文档树中不使用任何符号链接。你可以使用 `find your_top_web_directory -type l -print` 命令来查找你的顶级 Web 目录中所有现存的符号链接；然后你可以想出如何避免它们。

- 2. 在 `httpd.conf` 的主服务器部分使用以下配置来启用符号链接：

```text
<Directory />
    Options FollowSymLinks
</Directory>
```

- 3. 如果你必须禁用符号链接，请考虑使用特定的目录名来缩小目录范围。例如，如果你想在名为 `my_dir` 的目录中禁止符号链接，但在其他地方允许（为了性能），你可以使用此配置：

```text
<Directory />
    Options FollowSymLinks
</Directory>

<Directory /my_dir>
    Options -FollowSymLinks
</Directory>
```

- 4. 同样，你可以使用 `SymlinksIfOwnerMatch`：

```text
<Directory />
    Options FollowSymLinks
</Directory>

<Directory /my_dir>
    Options -FollowSymLinks +SymlinksIfOwnerMatch
</Directory>
```

在此情况下，如果 `/my_dir` 目录中的符号链接的所有者 ID 与服务器的用户 ID 匹配，Apache 将跟随这些符号链接。

## 使用 ApacheBench 调优配置

Apache 服务器附带一个名为 ApacheBench (ab) 的工具，它默认安装在 Apache 安装目录的 bin 目录中。通过使用这个实用工具，你可以调优你的服务器配置。

根据你多处理模块（MPM）的选择（prefork、threaded、perchild），你需要调优以下默认配置的值：

```text
<IfModule prefork.c>  StartServers 5  MinSpareServers 5  MaxSpareServers 10  MaxClients 20  MaxRequestsPerChild 0  </IfModule>
```

```text
<IfModule threaded.c>  StartServers 3  MaxClients 8  MinSpareThreads 5  MaxSpareThreads 10  ThreadsPerChild 25  MaxRequestsPerChild 0  </IfModule>
```

```text
<IfModule perchild.c>  NumServers 5  StartThreads 5  MinSpareThreads 5  MaxSpareThreads 10  MaxThreadsPerChild 20  MaxRequestsPerChild 0  </IfModule>
```

随机调优这些指令不是一个好主意。因为你的 Web 站点及其流量模式和应用可能与其他站点不同，所以没有一个通用的公式来计算这些指令的适当值。然而，我将向你展示一种使用 ApacheBench 来确定适当值的技术。

**注意** 你应该在与 Web 服务器不同的系统（或多个系统）上使用 ApacheBench 工具，因为试图使用客户端/服务器模型在同一台服务器上进行基准测试会给你提供虚假信息。基准测试工具 ab 本身会从服务器中占用资源，从而篡改你的结果。因此，你必须在另一台机器上运行 ab。我推荐你在多台机器上运行 ab，以更好地模拟负载。

**提示** 你需要在其他机器上编译 Apache，以在非 Web 服务器系统上安装 ab 二进制文件。你可以在这样的系统上安装 Apache 的二进制 RPM 包，并在调优完成后将其卸载。有关如何安装和配置 Apache 的详细信息，请参阅第 2 章和第 3 章。




确定服务器的目标。估算（或猜测）你希望 Web 服务器能够处理多少请求。将其写在一个目标陈述中，例如：“我希望每秒处理 $N$ 个请求。”

重启你的 Web 服务器，并在除 Web 服务器以外的系统上运行 `ab` 命令，方法如下：

```
./ab -n number_of_total_requests \
   -c number_of_simultaneous_requests \
      http://your_web_server/page
```

例如：

```
./ab -n 1000 -c 50 http://www.domain.com/
```

ApacheBench 工具将发起 50 个并发请求，总请求数为 1,000 个。示例输出如下所示：

```
Server Software:        Apache/2.0.16
Server Hostname:        localhost
Server Port:            80

Document Path:          /
Document Length:        1311 bytes

Concurrency Level:      50
Time taken for tests:   8.794 seconds
Complete requests:      1000
Failed requests:        0
Total transferred:      1754000 bytes
HTML transferred:       1311000 bytes
Requests per second:    113.71
Transfer rate:          199.45 kb/s received

Connection Times (ms)
              min     avg     max
Connect:        0      0       5
Processing:   111   427     550
Total:        111   427     555
```

请注意，访问 http://www.domain.com 站点主页时，每秒请求数（Requests per second）为 113.71。将并发请求数改为更高的数值，观察服务器如何处理额外的并发负载。

现在，根据你的 MPM 更改 MaxClients、ThreadsPerChild 和 MaxThreadsPerChild 等值，重启 Apache，并像之前一样使用 `ab` 应用相同的基准测试。你应该会看到，根据你尝试的数字，每秒请求数会有所升降。当你通过更改指令值来调整数字时，请确保记录这些值和性能，以便你确定什么设置适合你。

# 通过缓存提升速度

缓存 Web 内容并不是一个新概念。大多数繁忙的 Web 站点都通过代理服务器或其他机制来实现缓存。这里我将讨论两个可供选择的选项。你还应该研究使用第 10 章中讨论的 `mod_proxy` 模块来利用 Apache 的代理功能。

# 使用 mod_fcache 将常用文件缓存在内存中

Apache 的 `mod_fcache` 模块将特定类型的文件缓存在内存中。缓存的文件存储在服务器的主内存空间中，并且可被所有 Apache 子进程访问。你可以从 www.fractal.net/mod_fcache.tm 下载此模块。要编译和安装此模块，请遵循以下步骤：

- 以 root 身份使用 `tar xvfz mod_fcache.tar.gz` 命令解压缩模块源代码，并将新创建的目录复制到你的 Apache 源代码分布的 modules 子目录中。例如，如果你将 Apache 源代码安装在 `/usr/local/src/httpd_2.0.16`，将 `fcache` 安装在 `/usr/local/src/fcache`，那么你可以通过使用 `cp -r /usr/local/src/fcache /usr/local/src/httpd_2.0.16 modules` 命令复制模块文件。
- 更改目录到 Apache 源代码分布的 `modules/fcache` 子目录。查看 `config.m4` 文件，看看是否需要对系统进行修改。通常你不需要做任何更改。如果你确实需要更改，你应该知道自己在做什么。
- 运行 `autoconf` 来配置所有内容。
- 将目录更改回顶层 Apache 源代码分布，并运行 Apache 的 `configure` 脚本，加上你通常使用的所有选项（参见 `config.status` 文件）以及 `--enable-fcache` 选项。
- 使用 `make && make install` 命令如常编译和安装 Apache。
- 使用 `/usr/local/httpd/apachectl restart` 命令重启 Apache Web 服务器。

现在你可以准备使用此模块了。例如，要缓存从名为 `common_images` 的目录提供的 GIF 图像，你在 `httpd.conf` 中使用以下配置段：

```
<Directory /common_images>
  fcache              On
  fcache_CacheTypes   image/gif
  fcache_MaxSize      10240
  fcache_RecomputeTables 600
</Directory>
```

关于上述配置段，有一些注意事项：

- `fcache` 开启缓存模块。
- `fcache.CacheTypes` 指令设置用于缓存的 MIME 类型。示例配置将其设置为 `image/gif`。如果你希望缓存所有类型的图像，可以使用 `image/*` 代替。
- `fcache.MaxSize` 设置缓存的 `size`（大小）。这里内存缓存设置为 10MB（1024KB × 10）。请记住，你必须拥有足够的内存来缓存文件。
- `fcache.RecomputeTables` 指令设置重新计算缓存表的时间（以秒为单位）。默认的 10 分钟对于大多数用途来说已经足够了。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_651_0.png)

要查看缓存统计信息，你可以创建以下配置：

```
<Location /fcache-stats>
SetHandler fcache-stats-handler
</Location>
```

然后访问 http://your_web_server/fcache-stats 页面。

# 使用 Squid 代理缓存服务器进行优化

Squid 是一个开源的符合 HTTP 1.1 标准的代理缓存服务器，你可以使用它来增强用户的 Web 浏览体验。你可以从 www.squid-cache.org 下载最新稳定版的 Squid 源代码分布。

理想情况下，你希望使用两个网络接口运行代理缓存服务器。一个接口将其连接到 Internet 网关或路由器，另一个接口将其连接到内部网络。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_651_1.png)

在代理缓存系统上禁用 IP 转发，可以确保没有人可以绕过代理服务器直接访问 Internet。

以下部分讨论如何安装和配置 Squid。

# 编译和安装 Squid 代理缓存服务器

要编译和安装 Squid，请遵循以下步骤：

1. 以 root 身份使用 `tar xvfz squid-version.tar.gz` 命令解压缩源代码分布（其中 *version* 是 Squid 软件的最新版本号）。
2. 运行 `./configure --prefix=/usr/local/squid` 命令以根据你的系统配置 Squid 源代码。
3. 运行 `make all; make install` 将 Squid 安装到 `/usr/local/squid` 目录中。

安装 Squid 后，你需要对其进行配置（参见下一节）。

# 配置 Squid

要配置 Squid，请遵循以下步骤：

- 使用 `groupadd nogroup` 命令创建一个名为 *nogroup* 的组。这个组将被 Squid 使用。
- 运行 `chown -R nobody:nogroup /usr/local/squid` 命令，将 `/usr/local/squid` 目录及其所有子目录的所有权赋予 nobody 用户和名为 nogroup 的组。这使得 Squid（以 *nobody* 用户身份运行）能够创建缓存目录和文件并写入日志。按照以下步骤修改 `/usr/local/squid/etc/squid.conf` 文件。
- 确定你希望运行代理缓存的端口。由于大多数站点在 8080 端口上运行代理缓存，这里我使用此值。在 `squid.conf` 中添加以下行：

```
http_port 8080
```

这告诉 Squid 监听 8080 端口以处理代理请求。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_652_0.png)

如果你更喜欢其他端口，请在此处使用。务必不要使用已被其他服务器占用的端口。理想情况下，你希望使用 1024 以上的端口号以避免与标准服务冲突，但如果你知道你没有在 80 端口上运行 Web 服务器，并希望在该端口上运行你的代理缓存，你可以这样做。另外，检查端口是否可用的快速方法是运行 `telnet localhost port_number` 命令，其中 *port_number* 是你希望用于代理缓存的端口号。如果你收到连接失败消息，则当前未使用该端口。

- 你需要定义希望将缓存数据保存在哪里。在 `squid.conf` 中定义以下行：

```
cache_dir ufs /usr/local/squid/cache 100 16 256
```

这告诉 Squid 你希望将缓存数据存储在 `/usr/local/squid/cache` 中。如果你的用户基数非常大且将使用此代理缓存，在跨越不同驱动器的多个缓存目录中是很好的主意。这减少了驱动器 I/O 相关的等待，因为多个独立的驱动器总是比单个驱动器快。

- 默认的 Squid 配置不允许来自任何地方的连接；这是一种安全特性，通常被称为“拒绝所有人，只允许那些应该拥有访问权限的人”。因此，你必须创建一个访问控制列表（ACL），以便你的网络能够访问代理缓存。例如，如果你的网络地址是 192.168.1.0，子网掩码为 255.255.255.0，那么你可以在 `squid.conf` 中定义以下行来为你的网络创建 ACL：

```
acl local_net src 192.168.1.0/255.255.255.0
```



6. Squid 需要知道您希望允许 `local_net` ACL 中的机器访问代理缓存，这通过在 `squid.conf` 中紧接在 `http_access deny all` 行之前的位置添加以下一行来完成：
   ```
   http_access allow local_net
   ```
7. 您需要告诉 Squid 缓存管理用户的用户名。如果您希望使用 `webmaster@yourdomain.com` 作为缓存管理用户，请在 `squid.conf` 中定义以下一行：
   ```
   cache_mgr webmaster
   ```
8. 要告知 Squid 应该以哪个用户和组运行，请在 `squid.conf` 中添加以下行：
   ```
   cache_effective_user nobody
   cache_effective_group nogroup
   ```
   这里，Squid 被指示以 `nobody` 用户身份运行，并使用名为 `nogroup` 的组的权限。
9. 保存 `squid.conf` 文件并运行以下命令以创建缓存目录：
   ```
   /usr/local/squid/squid -z
   ```

## 先生们，启动你们的 Squid

在配置好 Squid 后，您可以运行 `/usr/local/squid/bin/squid` 命令来首次启动 Squid。您可以通过多种方式验证其是否正在工作：

-   Squid 会出现在 `ps -x` 列表中。
-   运行 `client www.nitec.com` 会将网页文本转储到您的终端。
-   `/usr/local/squid/logs` 目录中的 `cache.log` 和 `store.log` 文件显示 Squid 正在运行。
-   运行 `squid -k check && echo "Squid is running"` 会告诉您 Squid 处于活动状态。

现在来进行真正的测试：如果您将客户端机器上的 Web 浏览器配置为使用 Squid 代理，您应该能看到结果。在 Netscape Navigator 中，选择“编辑偏好设置”，然后在“高级”类别中选择“代理”。通过选择“手动代理配置”并点击“查看”，您可以指定 Squid 服务器的 IP 地址作为 http、FTP 和 Gopher 代理服务器。默认代理端口是 3128，因此除非您在 `squid.conf` 文件中更改了它，否则将该数字填入端口字段。

> 注意
> 如果您使用 Microsoft Internet Explorer，可以通过选择“工具 -> Internet 选项 -> 连接 -> 局域网设置”将 Squid 服务器设置为您的 http、FTP 和 Gopher 代理。然后勾选“使用代理服务器”选项，这将启用“高级”按钮。点击“高级”按钮，并在 HTTP、FTP 和 Gopher 相应的输入框中输入 Squid 服务器地址和端口号。多次点击“确定”以关闭所有对话框。

此时，您应该能够像没有代理一样浏览任何网站。您可以通过检查代理服务器上的日志文件 `/usr/local/squid/logs/access.log` 并确认您正在查看的网站出现在其中，来再次确认 Squid 是否正常工作。

## 调整 Squid 以符合您的需求

现在 Squid 已经启动并运行，您可以自定义它以满足您的需求。最终，像 Squid 这样的工具对于您的用户来说应该是完全透明的。这种“不可见性”将用户从管理的复杂性中解放出来，使他们能够像没有 Web 代理服务器一样浏览网络。虽然我在这里没有详细说明如何实现这一点，但您可以参阅 `http://squid.nlanr.net/Squid/FAQ/FAQ.html` 上的 Squid 常见问题解答。该网站的第 17 节详细说明了如何使用 Squid 作为透明代理。

> 本节向您展示了使用 Squid 作为 Web 代理的基础知识。Squid 具有许多超出此处讨论范围的功能。如果您对使 Squid 具备基础功能之外的功能感兴趣，请访问 `http://squid.nlanr.net` 上的 Squid 网页。

## 为 Squid 设置规则

默认情况下，Squid 不限制您的用户访问任何站点。您可以在 `squid.conf` 文件中定义规则，以设置访问控制列表（ACL），并根据这些列表允许或拒绝访客；例如：

```
acl BadWords url_regex foo bar
```

通过添加上面这一行，您定义了一个名为 `BadWords` 的 ACL 规则，它匹配包含单词 `foo` 或 `bar` 的任何 URL。

> 这适用于 `http://foo.deepwell.com/pictures` 和 `http://www.thekenneddycompound.com/ourbar.jpg`，因为它们都包含属于 `BadWords` 成员的单词。

通过添加以下内容：

```
http_access deny BadWords
```

到 `squid.conf` 中，您阻止用户访问匹配此规则的任何 URL。

> 几乎每个使用基于单词的 ACL 的管理员都有一个故事，讲述他们是如何没有考虑到单词可以使用的多种方式。您应该意识到，如果您禁止用户访问包含单词“sex”的网站，您同时也禁止他们访问 `www.buildersexchange.com` 以及可能落入该类别的其他网站。

## 更改 Squid 的缓存内存设置

您可以控制 Squid 在缓存内存中保留的网页数量。

## 使用重定向器而不是规则

如果您发现自己正在 squid.conf 文件中管理一个大型的“黑名单”站点列表，您应该考虑使用一种称为重定向器的程序。大量的 ACL 规则列表可能会开始减慢高负载 Squid 代理的速度。通过使用重定向器完成同样的工作，您可以提高 Squid 根据过滤规则允许或拒绝 URL 的效率。您可以从 www.senet.com.au/squirm 获取有关 Squirm（一个功能齐全且可与 Squid 配合使用的重定向器）的更多信息。

cachemgr.cgi 文件包含在 Squid 发行版中。它是一个 CGI 程序，允许您查看代理的统计信息，并关闭和重启 Squid。安装只需要花您几分钟时间，但它提供了关于代理性能的具体细节。如果您想要调整您的 Web 缓存，这个工具会很有帮助。

例如，通过添加这一行

```
cache_mem 16 MB
```

您允许 Squid 使用 16MB 的内存来在内存中保存网页。通过反复试验，您可能会发现您需要不同的数量。

> **注意** cache_mem 不是 Squid 消耗的内存量；它只是设置 Squid 用于保存网页、图片等内容的最大内存量。Squid 文档指出，您可以预期 Squid 消耗的量可达此值的三倍。

## 以 Apache 日志格式写入 Squid 日志

Apache 以通用日志格式（CLF）写入日志。如果您有 Apache 日志分析工具，能够使用相同的工具解析 Squid 日志岂不是很棒？您可以让 Squid 以 CLF 格式写入日志来实现这一点。

通过使用这一行

```
emulate_httpd_log on
```

/var/log/squid 中的文件将以类似于 Web 服务器日志文件的格式写入。这种安排使您可以使用 Analog 或 Webtrends 等 Web 统计程序来分析您的日志，并检查用户正在查看的网站。

## 避免负面缓存

如果您输入一个 URL 并发现页面不存在，该页面临时在不久的将来可能都不会存在。通过设置 negative_ttl 为所需的分钟数，如下一个示例所示，您可以控制 Squid 记住之前尝试中未找到页面的时长。这被称为负面缓存。

```
negative_ttl 2 minutes
```

负面缓存并不总是好事。默认值是五分钟，但我建议将其缩短为两分钟，甚至一分钟，或者干脆禁用它。为什么要这样做？您希望您的代理尽可能透明。如果用户正在寻找一个已知存在的页面，您不希望 URL 出现与您用户能够访问它之间存在短暂的滞后时间。

## 使用 mod_backhand 构建 Web 服务器集群

如果您有一个 Web 服务器集群（即 Web 服务器农场），并希望使用原生 Apache 模块在服务器之间重定向请求，请考虑使用 `mod_backhand`。例如，如果您有一个由三个类似配置的 Apache 服务器组成的 Web 服务器集群，并希望将高负载的 CGI 或 `mod_perl` 请求分发到请求时不忙的服务器，您可以充分利用此模块。该模块使用集群中所有服务器的资源状态信息，并将请求重定向到比其他人更准备处理特定请求的服务器。

以下是如何使用 Apache 下载、编译、安装和配置此模块的方法。

1.  从 `http://www.backhand.org/mod_backhand` 下载模块源代码。
2.  以 root 身份提取源发行版到一个目录中，在新创建的 `mod_backhand` 子目录中运行 `./precompile path_to_apache_source` 命令。请记住将 `path_to_apache_source` 更改为实际的 Apache 源发行版路径。
3.  使用 `--enable-backhand` 或 `--enable-modules=backhand` 选项以及所有您通常使用的选项，从 Apache 源发行版目录中的 `configure` 脚本配置 Apache 源。
4.  像往常一样运行 `make && make install`。
5.  将以下配置段添加到您的 `httpd.conf` 中：
   ```apache
   <IfModule mod_backhand.c>
     UnixSocketDir /var/backhand/backhand
     MulticastStats 192.168.1.254:4445
     AcceptStats 192.168.1.0/24
   </IfModule>
   ```
   上述示例配置假设您的 IP 广播地址是 `192.168.1.254`，并且您有一个 C 类网络 `192.168.1.0/24`，它承载了您所有的 Web 服务器。请确保根据您的网络更改这些 IP 地址。`UnixSocketDir` 必须仅对 Apache 用户可访问。

> `mod_backhand` 模块使用以太网广播地址或 IP 多播地址来通告每个服务器的资源状态。上述例子使用的是以太网广播地址；您也可以使用多播地址。





现在你需要决定要在所有 Web 服务器之间进行负载均衡（即重定向）的目录。通常，这是 CGI 目录。例如，以下配置显示 `/www/mysite/cgi-bin` 将由 `mod_backhand` 接管：

```
<Directory "/www/mysite/cgi-bin">
 Backhand byAge
 Backhand byRandom
 Backhand byLoginWindow
 Backhand byLoad
</Directory>
```

6. 使用 `/usr/local/apache/bin/apachectl` restart 命令重启 Apache Web 服务器。
7. 对每个 Web 服务器重复上述所有步骤。

`mod_backhand` 模块创建一个守护进程，以促进 Web 服务器集群内资源统计信息的收集和传输。为了确保该守护进程获得公平的系统资源份额，请以高优先级运行它。例如，你可以使用大多数 Unix 和类 Unix 系统中提供的 `renice` 实用工具将其优先级设置为 `-20`。

> **注意** 在使用此模块时，还有其他一些需要您考虑的 `mod_backhand` 特有的调优问题。请访问 www.backhand.org/mod_backhand 以获取更多信息。

## 调整 Web 应用程序性能

Web 应用程序通常是主要的性能瓶颈。配置不当或编写不良的应用程序很容易让服务器不堪重负。确保你的 Web 应用程序没有引发问题非常重要。本节讨论了几种你可以用来最大限度地减少 Web 应用程序相关问题的技巧。然而，由于 Web 应用程序可以用许多语言和多种架构编写，因此不可能涵盖所有类型的 Web 应用程序。所以，这里的讨论仅限于基于 Perl 的 Web 应用程序问题。

### 加速 `mod_perl` 脚本

`mod_perl` 脚本通过一次性加载并可在无需重新加载的情况下随时运行来加速你的 Web 应用程序性能。以下是一些技巧，可以使你的 `mod_perl` 脚本运行得更快或更具性能效率。

### 预加载你的 `mod_perl` 模块

如果你的网站使用了大量的 `mod_perl` 模块，请考虑使用 `httpd.conf` 中的 `PerlRequire` 指令预加载模块。简单来说，创建一个 Perl 脚本来加载你的常用模块。例如，下面是一个名为 `startup.pl` 的简单 Perl 脚本，它加载了我经常使用的一些模块。

```
#!/usr/bin/perl
use CGI ();
use Apache::DBI ();
use Digest::MD5 ();

1;
```

空括号禁用了模块变量的默认导入，直到需要时才导入。这节省了内存空间，因为你可能不需要预加载的所有模块的所有功能。现在，可以使用 `PerlRequire /path/to/startup.pl` 指令在服务器启动时预加载此脚本。

当你使用诸如 `startup.pl` 这样的脚本预加载模块时，子进程至少可以共享这些模块使用的许多代码页，从而节省 RAM，有助于你的系统健康。

### 缓存数据库连接

如果你使用 Perl DBI 从 `mod_perl` 脚本中访问关系数据库，你可以通过更改一行代码来显著提高数据库连接的性能。如果你的 `mod_perl` 脚本当前使用 `use DBI;` 调用来直接使用 DBI 模块，请将其更改为 `use Apache::DBI;`，这将缓存你应用程序的数据库连接并显著提高性能。还有一些其他你应该考虑的编程技巧：

- 如果你对每个请求都连接到同一个数据库，请考虑在请求处理器外部打开数据库连接。例如：

```perl
sub handle {
    my $r = shift;

    my $q = new CGI;

    my $id = $q->param('id');

    # Connect to database

    my $dbh;

    eval {

        $dbh = DBI->connect($dataSource,
                            $dbUser,
                            $dbPassword, { AutoCommit => 1 })
            or die;
    };

    if ($@) {
        # die "Can't connect to database $DBI::errstr";
        # connect failed do something

        print STDERR "Can not connect to $dataSource \n";
        print STDERR "DB2 Server Error: $DBI::errstr \n";
    }

    my $statement = "SELECT myfield from mytable where ID = $id";

    my $sth = $dbh->prepare($statement);
    my $rv             = $sth->execute;
    if(! $rv ){
        # No record found. Do something
    }

    while ( my @fields = $sth->fetchrow_array){
        print STDOUT "ID $id shows: ", join(', ', @fields),
        "<br>";
    }

    $sth->finish;

}
```

请注意，数据库连接是在 handle 中执行的，但由于连接使用的是相同的数据库和用户凭证，因此可以在处理器外部执行。

- 如果可能，请准备一次 SQL 语句并复用已准备的语句以节省时间。之前的示例可以更高效地编写如下：

```perl
my $APP_RUN_COUNT = 0;
my ($dbh, $sth);

sub init {
    eval {

        $dbh = DBI->connect($dataSource,
                             $dbUser,
                             $dbPassword, { AutoCommit => 1 }) ||
            die;

    };

    if ($@) {
        # die "Can't connect to database $DBI::errstr";
        # connect failed do something

        print STDERR "Can not connect to $dataSource \n";
        print STDERR "DB2 Server Error: $DBI::errstr \n";
    }
}

sub prepare_statement {
    my $dbh = shift;

    my $statement = "SELECT myfield from mytable where ID = ?";
    $sth = $dbh->prepare($statement);
}

sub handle {
    my $r = shift;

    if ($APP_RUN_COUNT++ == 0) {
        init();
        prepare_statement($dbh);
    }

    my $q = new CGI;
    my $id = $q->param('id');
    my $rv = $sth->execute($id);
    if (! $rv ) {
        # No record found. Do something
    }

    while ( my @fields = $sth->fetchrow_array){
        print STDOUT "ID $id shows: ", join(',', @fields), "<br>";
    }

    $sth->finish;
}
```

在此，handler 方法调用 `init()` 和 `prepare_statement()` 例程，为子服务器进程的整个生命周期创建一次全局数据库和语句句柄。这使得脚本比之前的版本高效得多。

### 在部分 Apache 子进程上运行 mod_perl 应用程序

当你开始使用许多 mod_perl 脚本时，你会注意到你的 Apache 子服务器进程体积变大。你可以使用 `top` 命令来见证这种现象。只要你有足够的 RAM，就应该没问题。然而，没有人拥有足够的 RAM，因此不依赖大量内存作为解决方案，而是考虑如何更有效地解决此问题，这是一个好主意。

如果你发现由于加载了许多 mod_perl 脚本导致 Apache 子进程越来越大，请考虑拥有一个专门服务于动态内容的脚本服务器。图 22-6 展示了这是如何运作的。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_661_0.png)

当用户请求名为 www.domain.com 的站点的主页时，负责静态页面的 Apache 服务器将 index.html 页面返回给客户端。该页面包含嵌入的静态和动态内容链接。图中显示了两个这样的链接：**login** 和 *privacy*。当最终用户点击 **login** 链接时，它请求 `http://myapps.domain.com/login`，这是一个不同于 `www.domain.com` 服务器的 Apache 服务器。事实上，在理想世界中，这两个应该是两个不同的 Linux 系统。然而，并非每个人都有能力像这样拆分动态和静态内容，因此此解决方案并不适用于所有人。

如果你必须在运行 Apache 的同一 Linux 系统上保留 `mod_perl` 和静态内容，你仍然可以确保肥大的 Apache 子进程不提供静态页面。这里是一个我喜欢的解决方案：

1. 为你的 Apache Web 服务器编译并安装 `mod_proxy` 模块。
2. 将现有的 `httpd.conf` 文件复制为 `httpd-8080.conf`，并将 `Port` 指令修改为 `Port 8080` 而不是 `Port 80`。从 `httpd.conf` 中移除所有 `mod_perl` 特定的配置，以便所有 `mod_perl` 配置都在 `httpd-8080.conf` 文件中。
3. 修改 `httpd.conf` 文件以包含以下代理指令：

   ```
   ProxyPass /myapps http://127.0.0.1:8080/myapps
   ```

   你可以将 `myapps` 更改为你喜欢的任何内容。如果你更改了这一点，请确保在此讨论中提到的其他位置也进行更改。这里，提供静态页面的 Apache 服务器被告知所有到 `/myapps` URL 的请求都应通过代理模块提供服务，该模块应从运行在同一 Linux 系统（127.0.0.1 是本机）但端口为 8080 的 Apache 服务器获取响应。
4. 在 `httpd-8080.conf` 中添加以下配置以创建 `mod_perl` 脚本位置。

   ```
   <Location /myapps>
   SetHandler perl-script
   PerlHandler MyApp!
   </Location>
   ```

   别忘了将 `MyApp!` 更改为你的脚本名称。
5. 如果在 `httpd-8080.conf` 中有 `KeepAlive On`，请将其更改为 `Off`。这确保 Apache 不会为 `KeepAliveTimeout` 指定的秒数保持连接打开，以期望从相同的 TCP 连接服务新客户端。
6. 像往常一样使用 `apachectl` 命令启动（或重启）Apache 服务器（监听端口 80）。但是，你必须使用 `/usr/local/apache/bin/httpd -f /usr/local/apache/conf/httpd-8080.conf` 命令启动端口 8080 上的 Apache。这假设你已经安装了 `/usr/local/apache` 目录；如果不是这样，请确保更改路径。





现在，你拥有两个 Apache 父守护进程（即以 root 用户身份运行），它们运行着两组子进程：一组用于处理静态页面，另一组使用代理模块通过 `ProxyPass` 指令获取动态的 mod_perl 脚本页面。这样，你就可以使用一组完全不运行任何 Perl 代码的子服务器来处理静态页面。另一方面，端口 8080 上的服务器仅处理动态请求；因此，你实际上拥有了一个非常利于性能的配置。

## 选择 FastCGI 而非 mod_perl

在 mod_perl 下运行的脚本之所以运行速度快，是因为它们被加载到每个子服务器的代码空间中。与 CGI 不同，mod_perl 脚本可以维持与外部数据库服务器的持久连接。这意味着，使用 mod_perl 脚本生成数据库驱动的动态内容会非常快。

然而，如果你运行一个非常大的 Web 服务器，就会引入一个新问题。当你运行 50 个或更多的 Apache 服务器进程来服务许多并发请求时，Apache 最终可能会打开那么多数据库连接，并且在每个子进程的生命周期内保持每个连接持久。假设你运行一个 Web 服务器系统，其中运行了 50 个 Apache 子进程，以便你可以每秒处理大约 50 个请求，并且你恰好有一个基于 mod_perl 的脚本在初始化阶段打开数据库连接。当请求到达你的数据库脚本时，Apache 通过使用其每个子进程来服务这些请求，从而打开 50 个数据库连接。由于许多数据库服务器基于每个连接分配昂贵的资源，这在数据库端可能会成为一个重大问题。

例如，当连接到在远程 Linux 系统上运行的 IBM Universal Database Server (UDB) 企业版时，每个 Apache 子进程在数据库服务器上都有一个对应的连接相关进程。如果此类环境使用负载均衡硬件在多个支持 mod_perl 的 Apache Web 服务器之间平衡传入请求，那么很可能出现这种情况：每个运行 50 个 Apache 子进程的 Web 服务器系统的所有子进程都打开并连接到数据库服务器。例如，如果此类环境由负载均衡硬件下的 10 台 Web 服务器组成，那么到数据库服务器的总可能连接数为 10 × 50，即 500 个连接，这可能会在数据库服务器上造成大量的资源负载。

针对这种场景的一种可能解决方案是找到一种方法来让数据库使空闲连接超时，让 mod_perl 脚本代码检测陈旧连接，并使代码重新建立连接。另一种解决方案是创建一个持久数据库代理守护进程，每个 Web 服务器使用它从数据库获取数据。

幸运的是，FastCGI 或 Java Servlets 对这些问题有更原生的解决方案，对于数据库驱动的大量使用的应用程序应考虑使用它们。下一节将讨论另一种称为 FastCGI 的性能提升 Web 技术。

与 `mod_perl` 脚本一样，FastCGI 应用程序在初始加载后一直运行，因此与 CGI 脚本相比具有显著的性能优势。表 22-3 解释了 FastCGI 应用程序与 `mod_perl` 脚本之间的区别。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_664_0.png)

要了解有关 FastCGI 的更多信息，请参见第 14 章。

**表 22-3**
**FastCGI 应用程序与 `mod_perl` 脚本之间的区别**

| 主题 | FastCGI 应用程序 | `mod_perl` 脚本 |
| :--- | :--- | :--- |
| 依赖 Apache 平台 | 否。FastCGI 应用程序可以在非 Apache Web 服务器（如 IIS、Netscape Web Server 等）上运行。 | 是。只有 Apache 支持 `mod_perl` 模块。 |
| 仅限 Perl 的解决方案 | 否。FastCGI 应用程序可以用多种语言开发，包括 C、C++ 和 Perl。 | 是 |
| 作为外部进程运行 | 是 | 否 |
| 可以在远程机器上运行 | 是 | 否 |
| 运行应用程序/脚本的多个实例 | 通常，运行单个 FastCGI 应用程序来响应排队的许多请求。但是，如果负载很高，会运行同一应用程序的多个实例。 | 运行的 `mod_perl` 脚本实例数量等于 Apache 子服务器进程的数量。 |
| 广泛的支持 | 是。然而，我有时感觉 FastCGI 开发正在放缓，但我无法验证或证实这一点。 | 是。互联网上有大量 `mod_perl` 站点，并且可以通过 Usenet 或 Web 获得支持。 |
| 数据库连接 | 因为所有请求都发送给单个 FastCGI 应用程序，所以您只需要维护与后端数据库服务器的单个数据库连接。然而，当 Apache FastCGI 进程管理器由于负载过重而生成额外的 FastCGI 应用程序实例时，这种情况可能会改变。尽管如此，应用程序的 FastCGI 实例数量可能少于 Apache 子进程的数量。 | 因为每个 Apache 子进程都运行 `mod_perl` 脚本，所以每个子进程都可能拥有与后端数据库的数据库连接。这意味着即使是单个 Apache 服务器系统也可能产生数百个数据库连接。 |

![](img/e11fcbd2818a3495ac70085e5d8d1c26_667_0.png)

# 章节

# 创建高可用性网络

# 本章内容

在本章中，你将学习构建 Web 网络的设计考虑因素。Web 网络是一个由 Web 服务器节点组成的网络，它们共同创建 Web 服务。例如，Yahoo! 使用大量 Web 服务器、应用服务器和数据库服务器来创建众多 Yahoo! Web 服务。

- 理解 Web 网络的功能
- 增强 DNS 可靠性
- 对 Web 网络进行负载均衡
- 管理 Web 存储
- 创建用于维护的后端网络
- 加固你的 Web 网络

如果你已经决定将 Web 集成到你的业务中，你必须考虑一种可以超越单个 Web 服务器或 ISP 上的共享 Web 驱动空间的 Web 解决方案。Web 网络是其中一种解决方案。在本章中，你将学习使用经过验证的网络和系统管理概念，以及构建成功 Web 网络的设计考虑因素。虽然本章侧重于基于 Apache-on-Linux 的解决方案，但大多数解决方案也适用于其他平台。

## 高端 Web 网络的功能

高端 Web 网络每天提供数千到数百万个页面。为了服务大量的 Web 请求，它必须具备以下功能：

- **可靠的 DNS 服务器。** 如果你的域名系统 (DNS) 服务器宕机，没有人可以轻松访问你的 Web 站点。因此，可靠的 DNS 是 Web 网络设计中的一个重要考虑因素。
- **负载均衡的 Web 访问。** 用户连接到一个或多个 Web 服务器，这些服务器基于系统负载和可用性自动选择。
- **可管理的存储架构。** 任何考虑 Web 网络的人都可能拥有大量内容，这些内容需要以可靠和可管理的方式在所有 Web 服务器上可用。没有适当的规划和坚实的存储架构，管理许多 Web 服务器和每个服务器的硬盘可能会是一场噩梦。
- **高效的后端网络。** 大型 Web 站点运行许多应用程序，执行数百万次数据库查询以及许多其他后端任务，以为其访问者生成高质量的个性化内容。因此，坚实的后端网络是必需的。*后端网络*是一个对 Web 访问者不可访问但作为骨干网络，用于保持每个服务器更新并与最新内容同步的网络。后端网络还允许管理员执行各种系统管理任务，如备份、软件升级等。
- **高度安全性。** 设计师在设计 Web 网络时必须密切关注安全问题，因为黑客通常会瞄准容易突破的 Web 网络，并以此作为攻击其他站点的平台。这可能导致严重的法律麻烦。

## 增强 DNS 可靠性

当站点的 DNS 宕机时，大多数用户无法访问它。是的，如果你知道一个 Web 站点的 IP 地址，你通常可以访问它，但大多数人甚至不知道如何找到 Web 站点的 IP 地址，因此期望用户在你的 DNS 宕机时访问是不现实的。

这就是为什么注册新域名需要两个 DNS 服务器。然而，你应该将此要求视为绝对最低限度，你应该使用两个以上的服务器来增加冗余并提高 DNS 服务的可靠性。以下是我经常推荐的 DNS 策略：

- 部署至少两个用于你的 Web 站点的 DNS 服务器，这是大多数域名注册商的要求，最好多于两个。
- 部署一个异地辅助 DNS 服务器。这意味着如果你的本地 DNS 服务器宕机，异地辅助 DNS 服务器仍然应该可访问。例如，如果你的主 DNS 服务器位于暂时故障的网络上，异地辅助服务器将响应并将流量引导至适当的资源。如果你不想部署并自行维护异地 DNS 服务器，可以考虑使用 secondary.com 之类的服务。
- 如果可能，请使用至少一个专用 DNS 服务器，因为运行多种服务的系统比运行单一服务的系统更容易频繁宕机。




## 均衡你的 Web 网络负载

在 Web 网络中部署多个 Web 服务器节点的目的是在它们之间平衡负载，以确保高性能和稳定性。在服务器之间平衡负载主要有两种方式：轮询 DNS（Round-Robin DNS）和硬件负载均衡器。这两种方法将在下面的章节中讨论。

### 使用轮询 DNS 分发 HTTP 请求

仅当没有基于硬件的负载均衡解决方案时，才建议使用轮询 DNS 方案。轮询 DNS 是一种机制，用于循环使用单个 Web 主机名的一组 Web 服务器 IP 地址列表。

假设你有两台 Web 服务器，`www1.yourdomain.com`（192.168.1.10）和 `www2.yourdomain.com`（192.168.1.20），并且你想通过轮询 DNS 技巧在这两台服务器上平衡 `www.yourdomain.com` 的负载。只需遵循以下步骤：

- 1. 将以下行添加到你的 yourdomain.com 区域文件中：

```
www1  IN  A 192.168.1.10
www2  IN  A 192.168.1.20
www   IN  CNAME www1
www   IN  CNAME www2
```

- 2. 重启你的 DNS 服务器并 ping `www.yourdomain.com` 主机。你将在 ping 输出中看到 `192.168.1.10` 地址。

- 3. 停止 ping，然后重新开始 ping 同一主机，你会看到正在 ping 第二个 IP 地址，因为前面的配置告诉名称服务器循环使用 www 的 CNAME 记录。换句话说，`www.yourdomain.com` 主机既是 `www1.yourdomain.com`，又是 `www2.yourdomain.com`。

当有人输入 `www.yourdomain.com` 时，名称服务器先给出第一个地址一次，然后为下一个请求给出第二个地址，并持续在这些地址之间循环。

> **注意**
> 轮询技巧的一个缺点是，DNS 服务器无法知道哪个系统负载较重，哪个较轻——它只是盲目地循环。如果某台服务器崩溃或因某种原因变得不可用，轮询 DNS 技巧仍会定期返回故障服务器的 IP 地址。这意味着有些人能够访问网站，而有些人则不能。

### 使用硬件负载均衡器分发 HTTP 请求

如今，硬件负载均衡器非常常见。与上一节讨论的轮询 DNS 解决方案相比，硬件负载均衡方案通常要智能得多。硬件负载均衡设备可以通过响应时间、发送的请求数量以及发起自生成的 HTTP 测试请求等 ways，以各种方式监控每个 Web 服务器的网络负载、性能和可用性。因此，这些设备为你的负载均衡方案提供了更大的控制权。

一些负载均衡设备还允许你创建服务器池，其中一些服务器的优先级高于其他服务器。例如，如果你有一台 Pentium 4 1.3 GHz 系统，内存为 2GB，还有一台 Pentium III 550 MHz 系统，内存为 512GB，你可以赋予 Pentium 4 系统更高的优先级，因为它更强大，更有可能比 Pentium III 系统处理更多的请求。Local Director（CISCO）和 Web Director（Radware）是硬件负载均衡解决方案，对我来说效果很好。

图 23-1 显示了一个简单的负载均衡解决方案，其中每个客户端请求都会到达负载均衡硬件。

负载均衡器决定使用哪个 Web 服务器节点来服务该请求，并将请求传递给最合适的 Web 服务器，该服务器像往常一样响应请求。Web 服务器的选择标准可以取决于优先级、可用性和可靠性。

敏锐的读者会注意到，此解决方案有一个进入 Web 网络的单点入口。例如，针对 `http://www.domain.com` 的请求必须到达负载均衡器，负载均衡器内部将此请求翻译为网络中某个 Web 服务器节点的服务请求。图 23-2 展示了一个示例负载均衡 Web 网络。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_671_0.png)

**图 23-1：** 一个简单的负载均衡解决方案

![](img/e11fcbd2818a3495ac70085e5d8d1c26_671_1.png)

**图 23-2：** www.domain.com 的一个示例负载均衡解决方案

针对 `http://www.domain.com` 的请求被发送到负载均衡器，因为 `www.domain.com` 解析为负载均衡器的 IP 地址。换句话说，你必须设置 DNS 记录，将 `www.domain.com` 指向你的负载均衡器系统。然后，负载均衡器决定哪个 `www[i-N].domain.com` Web 服务器将响应该请求。

查看图 23-2，你可能会注意到除了内部 Web 网络交换机外，还有一个第二负载均衡器连接，以及主负载均衡器（左侧）和次要负载均衡器（右侧）之间的直接连接。直接连接通常是一根交叉网线或 RS232 串行连接。此连接用于在硬件设备之间维护状态。换句话说，次要负载均衡器跟踪主负载均衡器执行的每个操作。如果主负载均衡器因硬件故障而变得不可用，次要负载均衡器开始响应与主负载均衡器相同的 IP 地址并接管工作。交叉连接确保次要负载均衡器可以访问网络状态，因此能够恢复站点与客户端之间的当前连接状态。

另外请注意，如果你使用负载均衡硬件的 NAT 转换功能（如果配备此功能），则不需要为你的每个 Web 服务器都使用可路由 IP 地址。

## 管理 Web 存储

作为 Web 网络开发人员，你必须有一个清晰且定义明确的存储策略。适当的存储管理对于 Web 网络至关重要。需要考虑许多技术，并且在为你的 Web 网络创建稳固的存储架构时需要解决许多性能问题。本节讨论了一些主要的存储技术，以及实用的性能技巧，以提升 Linux 平台下的存储性能。

### RAID、SAN 还是存储设备

廉价（或独立）磁盘冗余阵列（RAID）、存储区域网络（SAN）或存储设备是最常用的存储技术。它们都承诺要么提高可靠性，要么提高可靠性和性能。选择适合你需求的正确解决方案需要更好地理解这些技术，这些技术在下面的章节中进行了讨论。

#### 硬件 RAID

硬件 RAID 解决方案通常使用带有内部 RAID 控制器卡的 SCSI 驱动器。无论你使用哪种 RAID（硬件或软件），你都必须选择一个适合你需求的 RAID 级别。最常见的 RAID 级别是 1 和 5。RAID 1 纯粹是驱动器镜像。如果你想使用驱动器镜像 RAID 1 并希望拥有 100GB 的总空间，你需要投资 200GB 的驱动器空间。虽然 RAID 级别 2 到 4 也是可用的，但 RAID 5 几乎总是最佳选择。如果你使用 N 个设备，最小设备的尺寸为 S，则整个阵列的大小为 (N-1)*S。缺少的空间用于奇偶校验（冗余）信息。建议使用相同尺寸的介质，以确保由于最小磁盘用于计算 RAID 5 下的可用磁盘空间，驱动器空间不会被浪费。

#### 存储区域网络（SAN）

存储区域网络（SAN）是存储解决方案的新圣杯。EMC、IBM、Compaq 和 Storage Networks 等公司是 SAN 提供商。通常，SAN 解决方案由你放置在光纤通道网络中的专用存储设备组成，存储通过专用交换硬件和光纤通道接口卡向你的 Linux 系统提供。一般来说，SAN 适用于企业世界，对于中小型企业来说尚未准备好。

但是，如果你将你的 Linux 系统共置于知名数据中心，例如 Exodus 和 Globix 等大型 ISP 提供的中心，你很可能会发现 SAN 是一种增值服务。这可能是一种无需支付昂贵的 SAN 硬件费用，但仍能访问它的方式。我知道在某些主要 ISP 地点提供此类服务的存储网络。它们还在美国各地拥有光纤环，这意味着你可以使纽约的驱动器在加利福尼亚出现，延迟可忽略不计。

#### 存储设备

如今，对于一切事物都有专用硬件，因此存储设备（即专用存储系统）对网络/系统管理员来说并不陌生。如今，你可以购买专用的存储设备，它们可以连接到你的 10 或 100 或 1000Mbits 以太网，并提供 RAID 存储服务。这些设备通常通过 Web 进行远程管理。它们非常适合中小型企业，而且通常配置和管理起来非常简单。

#### 调整你的硬盘

无论你为你的 Web 网络选择哪种类型的存储解决方案，你都不得不处理硬盘。你很可能使用光纤通道、SCSI 或 IDE 驱动器来实现你的存储解决方案。事实上，在当今的计算机世界中，SCSI 和 IDE 是最常见的硬盘类型。SCSI 驱动器和 SCSI 控制器比 IDE 驱动器贵得多，因为它们提供了更高的性能和灵活性。IDE 或 IDE 的增强版本称为 EIDE 的驱动器在个人计算机和非密集型磁盘 I/O 计算中更为常见。SCSI 和 IDE 世界的区别在于，SCSI 驱动器控制器处理将数据传入和传出驱动器的大部分工作，而 CPU 本身控制 IDE 驱动器。因此，在繁忙的系统中，SCSI 驱动器对 CPU 增加的负载不如 IDE 驱动器多。此外，SCSI 驱动器具有更宽的数据传输能力，而 IDE 驱动器仍然通过 16 位总线连接到系统。如果你需要高性能，SCSI 是首选方向。购买名牌 SCSI 适配器和超宽、10K RPM 或更快的 SCSI 驱动器，你就已经做了几乎所有能做的事情来提高你的驱动器子系统。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_673_0.png)

当然，如果你有预算，你可以使用光纤通道驱动器或选择 SAN 解决方案。后者通常用于具有高数据存储需求的企业。你也可以选择硬件/软件 RAID 解决方案，这些在本章中进行了讨论。




无论你选择 SCSI 还是 IDE 驱动器，如果你真的在意性能，就必须考虑使用多块驱动器。最低限度来说，你应该使用两块驱动器——一块用于操作系统和软件，另一块用于数据。对于 Web 服务器，我通常建议至少使用三块驱动器。第三块驱动器用于存放机器上托管的 Web 站点生成的日志。将驱动器 I/O 分散到多个设备上，可以确保将等待时间降至最低。

> **注意**
> 如果你为你的 Linux 系统配备了现代超宽 SCSI 驱动器组，你已经领先于行业趋势，并且应该能从你的驱动器中获得良好的性能。

## 获取 hdparm

为了从你现代的 EIDE 驱动器中获得更好的性能，在进行任何调优之前，你首先必须确定驱动器当前的性能状况。因此，你需要一个工具来衡量驱动器子系统的性能状态。`hdparm` 工具正是为此而生；你可以从 `http://metalab.unc.edu/pub/Linux/system/hardware/` 下载该工具的源码发行版。要编译并安装 `hdparm` 工具，请遵循以下步骤：

1. 切换为 root 用户。
2. 在合适的目录中解压源码发行版，例如 `/usr/local/src`。例如，我在 `/usr/local/src` 中运行了 `tar xvzf hdparm-3.9.tar.gz` 命令，以解压 hdparm 3.9 版本的源码发行版。
3. 进入新建的子目录并运行 `make install` 命令来编译和安装 hdparm 二进制文件及手册页。默认情况下，二进制文件安装在 `/usr/local/sbin` 目录中，其名称为 `hdparm`。

> **警告**
> 由于 `hdparm` 允许你改变 IDE/EIDE 驱动器子系统的行为，如果使用不当或配置错误，有时可能会导致系统挂起。我强烈建议你在 `hdparm` 之前备份你的数据。此外，在单用户模式下实验 `hdparm` 也是一个非常好的主意。你可以通过在启动过程中在 `li` 提示符下输入 `linux single` 来重启系统并强制进入单用户模式。

## 衡量你的驱动器性能

安装 `hdparm` 工具后，你就可以着手调查驱动器子系统的性能状态了。假设你的 IDE 或 EIDE 硬盘是 `/dev/hda`，运行以下命令查看硬盘配置的状态：

```
hdparm /dev/hda
```

你应该会看到类似的输出：

```
/dev/hda:
multcount       - 0 (off)
I/O support     - 0 (default 16-bit)
unmaskirq       - 0 (off)
using_dma       - 0 (off)
keepsettings    - 0 (off)
nowerr          - 0 (off)
readonly        - 0 (off)
readhead        - 8 (on)
geometry        - 2494/255/63, sectors - 40079088, start - 0
```

如你所见，默认模式下的几乎所有设置都被关闭了。你可以更改其中的一些默认设置，以提升驱动器性能。但在继续之前，你需要从硬盘获取更多信息。运行以下命令：

```
hdparm -i /dev/hda
```

此命令将返回类似以下的信息：

```
/dev/hda:
Model=WDG WD205AA,  FwRev=05.05B05,  SerialNo=WD-WMAW15J6037
Config: HardSect NotMFM HdSw>150Sec SptUnCxl Fixed DTR>5MBs FmtGapReq)
RawCHS=16383/16/63,  TrkSize=5760,  SectSize=600,  ECCbytes=40
BuffType=DualPortCache,  BuffSize=2048KB,  MaxMultSect=16, MultSect=16
CurCHS=16383/16/63,  CurSects=16514064, LBA=yes, LBASects=40079088
IORDY=on/off,  tPIO={min:120,w:IORDY:120},  tDMA={min:120,rec:120}
PIO modes: pio0 pio1 pio2 pio3 pio4
DMA modes: mdma0 mdma1 *mdma2 udma0 udma1 udma2 udma3 udma4
```

上述命令显示了上次启动系统时可获得的驱动器识别信息（如果有的话）。你稍后将会使用其中的一些信息。该命令报告了型号、配置、驱动器几何结构（柱面、磁头、扇区）、磁道大小、扇区大小、缓冲区大小、支持的 DMA 模式、PIO 模式等。为了测试驱动器子系统，请运行以下命令：

```
/usr/local/sbin/hdparm -Tt /dev/hda
```

你会看到类似以下的结果：

```
/dev/hda:
Timing buffer-cache reads:   128 MB in  1.01 seconds - 126.73 MB/sec
Timing buffered disk reads:  64 MB in 17.27 seconds - 3.71 MB/sec
```

当然，基于你的驱动器和控制器子系统，你的数值会有所不同。然而，这是你驱动器子系统的未调优状态。-T 选项告诉 hdparm 测试缓存子系统（即内存、CPU 和缓冲区缓存）。

-t 选项告诉 hdparm 通过读取不在缓存中的数据来报告驱动器（/dev/hda）的统计数据。多次运行此命令并计算你的驱动器报告的 MB/sec 的平均值。这大致就是你驱动器子系统的性能状态。在这个例子中，3.71 MB/sec 是读取性能，这相当低。

## 提升你的驱动器性能

现在让我们尝试提升驱动器的性能。回到 `hdparm -i /dev/hda` 命令的输出（如果你不知道我在说什么，请参见上一节），寻找 MaxMultSect 值。在这个例子中，它是 16。`hdparm /dev/hda` 命令显示 multcount 值为 0（关闭）。这意味着多扇区模式（即 IDE 块模式）被关闭了。

多扇区模式是现代大多数 IDE 硬盘的一个特性。它允许驱动器在每次 I/O 中断时传输多个驱动器扇区。默认情况下，它是关闭的。然而，大多数现代驱动器可以在每次 I/O 中断时执行 2、4、8 或 16 个扇区的传输。因此，如果我们将此模式设置为你的驱动器的最大可能值（由 MaxMultSect 值表示），你应该会看到吞吐量增加 5% 到 50% 甚至更多。此外，你还可以减少 30 到 50% 的操作系统开销。在这个例子中，MaxMultSect 值为 16，因此我们可以使用 hdparm 工具的 -m 选项来设置它，并查看性能是否提升。运行以下命令：

```
/usr/local/sbin/hdparm -m16 /dev/hda
```

现在，使用 `hdparm -tt /dev/hda` 命令运行性能测试，以查看变化。对于示例系统，变化如下：

```
/dev/hda:
  Timing buffer-cache reads:   128 MB in  1.01 seconds = 126.73 MB/sec
  Timing buffered disk reads:  64 MB in 16.53 seconds =  3.87 MB/sec
```

驱动器的性能从 3.71 MB/sec 提升至 3.87 MB/sec。提升不多，但也不算差。你很可能会看到类似的变化。如果你的 I/O 和控制器相当新，你可以做得好得多。你很可能可以达到 20 到 30 MB/sec！但请记住：在使用 hdparm 随意摆弄时，你可能会损坏数据，因此在尝试下面讨论的更多与驱动器硬件相关的选项之前，务必备份数据。

如果 hdparm 报告你的系统的 I/O 支持设置为 16 位，并且你拥有一个相当新（一两年左右）的驱动器子系统，你应该尝试 32 位 I/O 支持。你可以通过使用 hdparm 的 -c 选项来设置它，该选项有三个值：

- 0—启用默认的 16 位 I/O 支持。
- 1—启用 32 位支持。
- 3—启用 32 位支持，并包含许多 IDE/EIDE 芯片组所需的特殊同步序列。这也是大多数系统运行良好的值。

你按以下方式设置选项：

```
/usr/local/sbin/hdparm -m16 -c3 /dev/hda
```

请注意，为了启用 32 位 I/O 支持，同时使用了 -m16 选项和 -c3 选项。使用 -t 选项运行程序会显示以下结果：

```
/dev/hda:  
Timing buffered disk reads:  64 MB in  8.96 seconds -  7.14 MB/sec
```

如你所见，驱动器子系统的性能几乎翻了一番！然而，你应该能够进一步提升性能。例如，如果你的驱动器支持直接内存访问（DMA），操作系统可以使用 -d 选项，该选项启用 DMA 模式。

通常，-d1 -X32 选项或 -d1 -X66 选项一起使用，以利用你驱动器子系统的 DMA 能力。第一组选项（-d1 -X32）为驱动器启用多字 DMA 模式 2，下一组选项（-d1 -X66）为支持 UltraDMA 突发定时特性的驱动器启用 UltraDMA 模式 2。这些选项可以显著提高你驱动器的性能。我在使用各种新型 EIDE/ATA 驱动器时，通过这些选项看到了 20 MB/sec 的传输速率。

还有另一个选项 -u1，它可以极大地提高整体系统性能。此选项允许磁盘驱动程序在处理磁盘中断期间解除其他中断的掩码，这意味着在等待基于磁盘的数据传输完成时，操作系统可以处理其他中断，如网络 I/O、串行 I/O 等。

还有许多其他 hdparm 选项供你设置和实验；然而，对大多数选项要非常谨慎，因为你很可能会损坏数据。在操作 hdparm 工具之前，始终备份数据。此外，一旦你发现一组选项运行良好，你就应该将这些选项的 hdparm 命令放入 /etc/rc.d/rc.local 脚本中，以便每次启动系统时都会设置它们。例如，我在我较新的 Red Hat Linux 系统之一的 /etc/rc.d/rc.local 文件中添加了以下行：

```
hdparm -m16 -c3 -u1 -d1 -X66    /dev/hda
```

既然你的硬盘已针对更好的性能进行了调优，让我们来看看如何调优充当磁盘接口的文件系统。因为 Linux 使用 ext2 文件系统，我将在下一节讨论该文件系统的调优问题。

## 调优 ext2 文件系统

多年来，ext2 文件系统一直是 Linux 事实上的文件系统。它不是世界上最优秀的文件系统，但它运行得相当好。你可以改进 ext2 文件系统性能的方法之一是更改默认块


对于主要以大文件为主的服务器，建议将大小设置为 1024 到 1024 的倍数（通常小于 4096）。让我们看看如何更改块大小。

## 更改 ext2 文件系统的块大小

要了解特定 ext2 分区上有哪些类型的文件（就大小而言），请执行以下操作：

- 1. 切换至 root 用户并进入 ext2 分区根目录。
- 2. 运行以下命令，该命令实际上是一个使用 find 和 awk 实用工具的小型脚本。此命令行脚本将显示所有文件及其大小，最后提供整个分区的总大小和平均大小。

```bash
find . -type f -exec ls -l {} \; | \
awk 'BEGIN {tsize=0;fcnt=1;} \
| printf("%03d File: % 60.5s size: %d bytes\n",fcnt++, $9, $5); \
tsize += $5; } \
END { printf("Total size = %d\nAverage file size = %.02f\n", tsize, tsize/fcnt); }'
```

- 3. 知道文件系统的平均文件大小后，您可以确定是否应更改块大小。假设您发现平均文件大小为 8192，即 2 × 4096。您可以将块大小更改为 4096。
- 4. 不幸的是，如果不重建现有 ext2 文件系统，无法更改其块大小。因此，您必须备份文件系统上的所有文件，然后使用 /sbin/mke2fs /dev/partition -b 4096 命令重建它。例如，如果您已备份 /dev/hda7 分区并希望将块大小更改为 4096，请使用 /sbin/mke2fs /dev/hda7 -b 4096 命令。

> **注意**
> 将块大小更改为高于默认值（1024）的数字可能会因寻道次数减少而显著提高原始读取速度，同时还可能加快启动期间的 fsck 会话，减少文件碎片等。然而，盲目增加块大小（即不知道平均文件大小）会导致空间浪费。如果平均文件大小为 2010 字节，而系统使用 4096 字节的块，那么每个文件平均将浪费 2086 字节（4096 − 2010）！因此在调整块大小之前，请务必了解您的文件大小。

## 安装 e2fsprogs 以调优 ext2 文件系统

为了调优 ext2 文件系统，您需要按照以下步骤安装 e2fsprogs 实用工具包：

- 1. 从 www.rpmfind.net 下载 e2fsprogs-version_src.rpm（将 version 替换为最新版本号）源发行版。我下载了 e2fsprogs-1.19-0.src.rpm 包。您也可以从 e2fsprogs 项目网站 http://e2fsprogs.sourceforge.net 获取源码。切换至 root 用户。
- 2. 运行 `rpm -ivh e2fsprogs-version.src.rpm` 命令，将源提取到 `/usr/src/redhat/SOURCES/` 目录。源 RPM 会放下一个 `e2fsprogs-version.tar.gz` 文件，需要使用 `tar xzvf e2fsprogs-version.tar.gz` 命令进行解压。这将创建一个名为 `e2fsprogs-version` 的子目录。
- 3. 进入新的子目录 `e2fsprogs-version`。
- 4. 运行 `mkdir build` 创建一个新子目录，然后切换到该子目录。
- 5. 运行 `.../configure` 脚本以配置源树。然后运行 `make` 实用程序生成二进制文件。接着运行 `make check` 以确保所有构建都正确。最后，运行 `make install` 命令安装二进制文件。

安装 e2fsprogs 实用工具后，您可以开始使用它们，具体方法见下一节。

## 使用 tune2fs 实用程序进行文件系统调优

您可以使用 `tune2fs` 实用程序来调优 ext2 文件系统的各个方面。但是，切勿在已挂载的 ext2 文件系统上应用 tune2fs 实用程序，并且在修改任何属于文件系统的内容时，务必备份您的数据。在本节中，我将讨论如何使用 `tune2fs` 实用程序（它是 e2fsprogs 包的一部分）来调优未挂载的名为 `/dev/hda7` 的 ext2 文件系统。如果您使用下面讨论的一个或多个设置，请记得将分区名称（`/dev/hda7`）更改为合适的名称。首先，运行以下命令以确定 `tune2fs` 显示未挂载的 `/dev/hda7` 的当前设置：

```
/sbin/tune2fs -l /dev/hda7
```

输出应类似于以下内容：

```
tune2fs 1.19, 13-Jul-2000 for EXT2 FS 0.5b, 95/08/09
Filesystem volume name:   <none>
Last mounted on:              <not available>
Filesystem UUID:     5d06c65b-dd11-4df4-9230-a10f2da783f8
Filesystem magic number:      0xEF53
Filesystem revision #:    1 (dynamic)
Filesystem features:    filetype sparse_super
Filesystem state:    clean
Errors behavior:    Continue
Filesystem OS type:    Linux
Inode count:    1684480
Block count:    13470471
Reserved block count:  673523
Free blocks:    13225778
Free inodes:    1674469
First block:    1
Block size:    1024
Fragment size:    1024
```

以下列表中讨论的设置在上述输出中以粗体显示。

- **错误处理**（**Errors behavior**）设置决定了内核在文件系统检测到错误时的行为。此设置有三个可能的值：continue（继续）、remount-ro（只读重新挂载）和 panic（内核恐慌）。默认设置是在即使有错误的情况下继续。
- **挂载计数**（**Mount count**）设置是您挂载此文件系统的次数。
- **最大挂载计数**（**Maximum mount count**）设置意味着，在达到最大读写模式挂载次数（在本例中为 20 次）之后，文件系统将在下一个启动周期中接受 fsck 检查会话。
- **上次检查**（**Last checked**）设置显示了上次执行 fsck 检查的日期。
- **检查间隔**（**Check interval**）设置显示了两个连续 fsck 会话之间的时间差。仅当间隔期间未达到最大读写挂载次数时，才使用检查间隔。换句话说，如果您在 6 个月内没有卸载文件系统，即使挂载计数仅为 2，由于文件系统超过了检查间隔，fsck 检查也将被强制触发。
- 下次 fsck 检查日期显示在 **下次检查**（**Next check after**）设置中。
- **保留块 uid**（**Reserved blocks uid**）和 **保留块 gid**（**Reserved blocks gid**）设置显示了哪个用户和组拥有此文件系统的保留部分。默认情况下，保留部分由超级用户（UID = 0, GID = 0）使用。

对于未挂载的文件系统（如 /dev/hda7），您可以使用 tune2fs 的 -c 选项将最大读写挂载计数设置更改为更适合您需求的值。例如，/sbin/tune2fs -c 1 /dev/hda7 将强制每次启动系统时都对文件系统执行 fsck 检查。您还可以使用 -i 选项更改基于时间的 fsck 检查强制策略。

例如，`/sbin/tune2fs -i 7d /dev/hda7` 命令确保如果文件系统在一周后以读写模式重新挂载，则强制执行 `fsck` 检查。类似地，`/sbin/tune2fs -i 10 /dev/hda7` 命令禁用基于时间的 `fsck` 检查。

## 使用 e2fsck 实用程序检查和修复文件系统

如果您有损坏的 `ext2` 文件系统，可以使用 `e2fsck` 实用程序尝试修复它。要使用 `e2fsck` 检查分区，必须首先卸载它，然后运行 `/sbin/e2fsck /dev/device` 命令，其中 `/dev/device` 是您的磁盘驱动器。例如，要在名为 `/dev/hda7` 的设备上强制 `fsck` 检查，请使用 `/sbin/e2fsck -f /dev/hda7` 命令。这样的检查可能会显示如下所示的输出：

```
e2fsck 1.19, 13-Jul-2000 for EXT2 FS 0.5b, 95/08/09
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/hda7: 12/1684256 files (0.0% non-contiguous), 52897/3367617 blocks
```

`e2fsck` 实用程序会询问您修复问题，您可以通过使用 `-p` 选项来避免这些问题。

# 通过日志文件系统提高 Linux 的可靠性

Linux 文件系统领域新的热门话题是日志文件系统（journaling file system）。*日志文件系统*  simply 是一个基于事务的文件系统。每个更改文件系统的文件系统活动都会记录在事务日志中。在发生崩溃的情况下，文件系统可以重放必要的事务，在非常短的时间内恢复到稳定状态。这是一种许多广泛使用的数据库引擎（如 IBM DB2 和 Oracle）使用的技术，以确保文件系统始终处于已知且可恢复的状态。

`ext2` 文件系统的问题在于，不幸发生崩溃时，文件系统可能处于如此不干净的状态，以至于可能损坏到无法有意义地恢复。用于检查和潜在修复文件系统的 `fsck` 程序往往无法解决此类问题。对于日志文件系统而言，这样的噩梦已成为过去！因为事务日志记录了文件系统中的所有活动，崩溃恢复迅速且数据损失最小。

> 日志文件系统不会在日志中记录数据；它仅记录与磁盘操作相关的元数据，因此重放日志仅使文件系统在结构关系和资源分配方面保持一致。因此，可能会有少量数据丢失。此外，记录也和其他活动一样受媒体错误的影响。因此，如果媒体损坏，日志记录也无济于事。




# 日志文件系统

日志文件系统对 Linux 来说是新事物，但已可用于其他平台。虽然日志文件系统支持功能对 Linux 而言非常新颖，但它吸引了企业对使用 Linux 进行企业级应用的巨大关注；因此，日志文件系统将快速走向成熟。我强烈建议您在实验层面开始使用这种日志文件系统类型，并习惯于其缺点和特性。

目前有多种实验性的日志文件系统可供选择。本节讨论 ReiserFS，因为它包含在 Linux 内核 2.4.1（或更高版本）中，但如果我不列出其他也可用的主要日志文件系统，那将是一种失职。它们是：

- IBM 为 Linux 开源的 JFS。JFS 是从 AIX 移植而来的，AIX 是 IBM 自己的操作系统平台，但它尚未完全准备好用于生产环境。您可以在 http://oss.software.ibm.com/developworks/open_source/jfs 找到有关 JFS 的更多信息。
- Red Hat 自有的 ext3 文件系统 ext2+，具有日志记录功能。它也尚未准备好用于生产环境。您可以在 ftp://ftp.linux.org.uk/pub/linux/sct/fs/jfs/ 下载 ext3 的 alpha 版本。
- ReiserFS，由 Namesys 开发，目前包含在 Linux 内核源代码发行版中。在 Linux 上，它比其他日志文件系统更广泛地得到使用。目前，它似乎正在 Linux 日志文件系统领域中处于领先地位。ReiserFS 由 Hans Reiser 开发，他从诸如 MP3、BigStorage.com、SuSe 和 Eciela.com 等商业公司获得了开发资金。这些公司都迫切希望拥有更好、更灵活的文件系统，并且可以立即将早期 beta 用户的体验反馈给开发者。您可以在 www.namesys.com 找到有关 ReiserFS 的更多信息。
- XFS 日志文件系统，由 Silicon Graphics, Inc. (SGI) 开发。您可以在 http://oss.sgi.com/projects/xfs/ 找到有关 XFS 的更多信息。XFS 是一个快速、稳健的 64 位文件系统，这意味着它可以支持大文件（900 万 TB）以及更大的文件系统（1800 万 TB）。

> **注意**
> 截至本文撰写之时，ReiserFS 文件系统不能在不打补丁的情况下与 NFS 一起使用，而这些补丁并未正式提供给内核 2.4.1 或更高版本。

## 编译和安装 ReiserFS

在您使用 ReiserFS 之前，您需要编译并安装它。请按照以下步骤在内核 2.4.1 或更高版本的 Linux 内核中编译和安装 ReiserFS (reiserfs) 支持：

1. 以 root 身份从 www.kernel.org 获取最新的 Linux 内核源代码，并将其解压到 `/usr/src/linux-version` 目录中，其中 `version` 是当前内核的版本。以下步骤假设最新内核为 2.4.1。
2. 在 `/usr/src/linux-2.4.1` 目录中运行 `make menuconfig`。
3. 选择 **Code maturity level options** 子菜单，并使用空格键选择 **Prompt for development and/or incomplete code/drivers** 选项。退出子菜单。
4. 选择 **File systems** 子菜单。使用空格键选择 **Reiserfs support**，将其包含在内核模块中，然后退出子菜单。
   > **不要** 在 ReiserFS 支持选项下选择 **Have reiserfs do extra internal checking** 选项。如果将此设置为 Yes，则 reiserfs 将在运行期间执行广泛的内部一致性检查，这会使其速度非常慢。
5. 确保所有您使用的其他内核功能也按照惯例被选中。
6. 退出主菜单并保存内核配置。
7. 按照 menuconfig 程序的建议运行 `make dep` 命令。
8. 运行 `make bzImage` 创建新内核。然后运行 `make modules` 和 `make modules_install` 将新模块安装到适当的位置。
9. 将目录更改为 `arch/i386/boot`。如果您的硬件架构是 Intel，则需要将 i386 替换为您的架构，并且可能需要从内核使用指南文档中获取更多说明来编译和安装您的内核版本。我假设大多数读者的系统都是基于 i386 的，并继续往下。
10. 将 `bzImage` 复制到 `/boot/vmlinuz-2.4.1`，并编辑 `/etc/lilo.conf` 文件以包含如下的新配置：
    ```
    image=/boot/vmlinuz-2.4.1
    label=linux2
    read-only
    root=/dev/hda1
    ```
11. 运行 `/sbin/lilo` 命令重新配置 lilo，然后重启您的系统。在 lilo 提示符下输入 `linux2` 并启动新内核。如果遇到任何问题，您应该能够重启到标准的 Linux 内核，它应该是默认的。在您启动新内核后，现在就可以使用 ReiserFS (reiserfs) 了。

## 挂载 ReiserFS 文件系统

由于 ReiserFS (reiserfs) 仍处于“实验性”类别，我强烈建议您在系统的非关键部分使用它。理想情况下，您希望将整块磁盘或一个或多个分区专门用于 ReiserFS，以便您可以安全地使用它并看看您是否喜欢它。

要将 ReiserFS 用于名为 `/dev/hda7` 的新分区，请执行以下操作：

1. 以 root 身份确保该分区被设置为 Linux native (83)，方法是使用 `fdisk` 或其他磁盘分区工具。
2. 使用 `/sbin/mkreiserfs /dev/hda7` 命令在新分区上创建 ReiserFS (reiserfs) 文件系统。
3. 接下来为新文件系统创建一个挂载点。例如，我可以使用 `mkdir /jfs` 命令创建一个名为 `/jfs` 的挂载点。
4. 最后，使用 `mount -t reiserfs /dev/hda7 /jfs` 命令挂载文件系统。现在您可以从 `/jfs` 挂载点访问它。

要了解日志文件系统与 ext2 文件系统相比如何，您可以使用下一节中的基准测试。

## ReiserFS 基准测试

本材料假设您已在 `/dev/hda7` 上创建了一个全新的 ReiserFS 文件系统，并且可以将其挂载到 `/jfs`。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_684_0.png)

> 要进行此基准测试，您必须不在该分区中存储任何数据。因此，请备份 `/jfs` 中的所有内容，因为在此过程中您将擦除 `/jfs` 上的所有内容。

要对 ReiserFS 进行基准测试，请遵循以下步骤：

1. 在 `/tmp` 目录中创建一个名为 `reiserfs_vs_ext2.bash` 的 shell 脚本。此脚本列在清单 23-1 中。

### 清单 23-1: /tmp/reiserfs_vs_ext2.bash

```bash
#!/bin/bash
#
# This script is created based on the file_test script
# found in the homegrown benchmark found at http://www.namesys.com
#

if [ $# -lt 6 ]
then

    echo Usage: file_test dir_name device nfiles size1 size2 log_name
    exit

fi

TESTDIR=$1
DEVICE=$2
LOGFILE=$6

/bin/umount $TESTDIR
/sbin/mkreiserfs $DEVICE
mount -t reiserfs $DEVICE $TESTDIR

echo 1. reiserfs 4KB creating files ...

echo "*reiserfs 4KB create" $3 "files of size: from " $4 "to" $5 >> $LOGFILE
(time -p ./mkfile $TESTDIR $3 $4 $5)>> $LOGFILE 2>&1
echo done.
sync
df >> $LOGFILE

/bin/umount $TESTDIR
/sbin/mk2fs $DEVICE -b 4096
mount -t ext2 $DEVICE $TESTDIR

echo 2. ext2fs 4KB creating files ...
echo "*ext2fs 4KB create" $3 "files of size: from " $4 "to" $5 >> $LOGFILE
(time -p ./mkfile $TESTDIR $3 $4 $5)>> $LOGFILE 2>&1
echo done.
sync
df >> $LOGFILE

/bin/umount $TESTDIR
```

2. 此外，从 `www.namesys.com/filetest/mkfile.c` 下载 ReiserFS 团队开发的一个小型 C 程序 `mkfile.c` 到 `/tmp`。
3. 从 `/tmp` 目录使用 `gcc -o mkfile mkfile.c` 命令编译 `mkfile.c`。
4. 使用 `chmod 755 reiserfs_vs_ext2.bash mkfile` 命令更改 `reiserfs_vs_ext2.bash` 和 `mkfile` 程序的权限。
5. 以 root 身份运行以下命令：
   ```
   ./reiserfs_vs_ext2.bash /jfs /dev/hda7 100000 1024 4096 log
   ```
6. 系统会提示您确认是否要丢失 `/dev/hda7` 中的所有数据。由于您已经清空该分区用于测试，请说“是”并继续。此测试将在 ReiserFS (reiserfs) 和 ext2 文件系统中创建 100,000 个各种大小的文件，大小范围为 1K 到 4K，方法是依次在 `/dev/hda7` 中创建这两种文件系统。结果将记录在 `/tmp/log` 文件中。以下是 `/tmp/log` 文件的一个示例：
   ```
   reiserfs 4KB create 100000 files of size: from   1024 to 4096
   real  338.68
   user  2.83
   sys  227.83
   Filesystem           1k-blocks     Used Available Use% Mounted on
   /dev/hda1             135600     135600   847452  14% /
   /dev/hda5             4134868    2318896  1605928  60% /usr
   /dev/hda7             1347048     332940 13137108   3% /jfs
   ext2fs 4KB create 100000 files of size: from   1024 to 4096
   real  3230.40
   user  2.87
   sys  3119.12
   ```



## 与 NFS 服务器共享驱动器空间

虽然你可以通过网络文件系统（NFS）共享静态内容，但我之前建议使用静态文件的本地副本。除非你选择高端 SAN 解决方案，否则存储在本地驱动器上的文件访问时间会比任何网络存储解决方案都快得多。

我强烈建议你只将在 NFS 分区上放置需要共享、频繁更改或必须在所有 Web 节点间使用相同数据的文件。例如，你的 Web 应用程序可以在所有节点间共享，这样你只需保留一份软件副本。然而，更重要的是，这些应用程序创建的数据也应共享。例如，如果你有一个 CGI 脚本为购物车写入磁盘会话数据，当用户发起下一个请求时，你所使用的负载均衡方案可能会将用户引导到网络中的另一个 Web 服务器，这意味着会话数据必须对其他 Web 服务器可用，否则用户将不得不重新开始他们的购物车。

创建一个目录，在其中保存所有必须共享的数据。例如，在 NFS 服务器上创建 `/www/cgi-data` 作为你的 CGI 脚本数据目录。你可以为每个 CGI 应用程序创建子目录，并配置每个应用程序在其 `/www/cgi-data` 内的专属目录中写入数据。然后，通过 NFS 挂载此目录，它将对网络中的所有 Web 服务器可用。以下部分将展示如何操作。

### 设置 NFS 服务器

NFS 服务器需要运行一个名为 portmapper（也称为 portmap 或 rpc.portmap）的程序，它通常由 rc 脚本启动。要检查 portmapper 是否已在运行，请使用以下命令：

```
ps auxw | grep portmap
```

在 RedHat Linux 下，portmapper 会自动由 `/etc/rc.d/rc3.d/S4/portmap` 脚本（即 `/etc/rc.d/init.d/portmap` 初始化脚本）启动，因此无需手动启动。

下一步是修改 `/etc/exports` 文件，以告知系统哪些文件系统或目录需要导出给 NFS 客户端。由于 XC News 只需将 `/www/cgi-data` 目录导出给 Web 服务器，`ns.xcnews-lan.com` 主机上的导出文件看起来如下：

```
/www/cgi-data www1.xcnews-lan.com(rw) www2.xcnews-lan.com(rw)
```

这一行指示 NFS 服务器允许 `www1.xcnews-lan.com` 和 `www2.xcnews-lan.com` 对 `/www/cgi-data` 目录进行读写访问。

> 导出文件的语法在所有 Unix 品牌中可能并不相同。

必须运行的下一个程序是 mountd（rpc.mountd）和 nfsd（rpc.nfsd）。这两个程序也是由 /etc/rc.d/rc3.d 中的 rc 脚本自动启动的。然而，每当 /etc/exports 文件发生变更时，需要告知这两个程序该变更。名为 exportfs 的脚本可以重启这两个程序，如下所示：

```
exportfs
```

如果系统中缺少 exportfs，则可以使用如下脚本代替：

```
#!/bin/sh
killall -HUP /usr/sbin/rpc.mountd
killall -HUP /usr/sbin/rpc.nfsd
echo re-exported file systems
```

此脚本使用大多数 Linux 系统中存在的 killall 程序；如果该程序不可用，你始终可以运行 ps 命令，找到这些进程的 PID，并手动对每个进程执行 kill -HUP。现在，为确保 mountd 和 nfsd 正在正常运行，请运行名为 rpcinfo 的程序，如下所示：

```
rpcinfo -p
```

输出如下：

| 程序 | 版本 | 协议 | 端口 | 服务 |
|---------|------|-------|------|---------|
| 100000  | 2    | tcp   | 111  | rpcbind |
| 100000  | 2    | udp   | 111  | rpcbind |
| 100005  | 1    | udp   | 635  | mountd  |
| 100005  | 2    | udp   | 635  | mountd  |
| 100005  | 1    | tcp   | 635  | mountd  |
| 100005  | 2    | tcp   | 635  | mountd  |
| 100003  | 2    | udp   | 2049 | nfs     |
| 100003  | 2    | tcp   | 2049 | nfs     |

这表明 portmapper、mountd 和 nfsd 已通告其服务并运行正常。在 Web 服务器上设置 NFS 客户端之前，务必解决安全问题，正如我在下一节中讨论的那样。

### 服务器安全问题

portmapper 与 `nfsd` 结合使用可能会受到欺骗，使得无需任何权限即可访问 NFS 服务器上的文件。幸运的是，Linux 使用的 portmapper 相对安全，抵御攻击的能力较强，并且可以通过在 `/etc/hosts.deny` 文件中添加以下行来提高其安全性：

```
portmap: ALL
```

系统将拒绝所有人访问 portmapper。现在需要修改 `/etc/hosts.allow` 文件如下：

```
portmap: 192.168.1.0/255.255.255.0
```

这使得 `192.168.1.0` 网络中的所有主机能够访问由 portmapper 管理的程序，如 `nfsd` 和 `mountd`。

> **警告** 切勿在 `/etc/hosts.allow` 中的 `portmap` 行中使用主机名，因为使用主机名查找可能会间接引发 `portmap` 活动，从而在循环中触发主机名查找。

服务器端另一个安全问题是是否允许客户端的 root 账户在服务器端被当作 root 处理。默认情况下，Linux 禁止 NFS 客户端端的 root 在服务器端被当作 root 处理。换句话说，服务器上由 root 拥有的导出文件不能由客户端的 root 用户修改。若要显式强制执行此规则，可以按如下方式修改 `/etc/exports` 文件：

```
/www/cgi-data www1.xcnews-lan.com(rw, root_squash) www2.xcnews-lan.com(rw, root_squash)
```

现在，如果客户端上一个 UID 为 0（root 用户）的用户尝试访问（读取、写入或删除）文件系统，服务器会用服务器“nobody”账户的 UID 替代该 UID。这意味着客户端的 root 用户无法访问或更改仅服务器 root 可以访问或更改的文件。

> **提示** 若要授予对 NFS 文件系统的 root 访问权限，请改用 `no_root_squash` 选项。

至此，NFS 服务器已设置并配置好安全，现在让我们设置 NFS 客户端主机。

### 设置 NFS 客户端

默认情况下，Red Hat Linux 支持 NFS 文件系统，因此无需折腾内核。要挂载由 `ns.xcnews-lan.com` 主机导出的 `/www/cgi-data` 目录，请在两台 Web 服务器的 `/etc/fstab` 文件中添加以下行：

```
ns.xcnews-lan.com:/www/cgi-data /www/cgi-data nfs
```

此行会在任何 Web 服务器重启时自动挂载 /www/cgi-data 目录。

接下来，在两个系统上创建 /www/cgi-bin 目录，并使用 mount 命令手动挂载该目录，如下所示：

```
ns.xcnews-lan.com:/www/cgi-data nfs
```

> **警告**
>
> 一个典型的 NFS 挂载问题发生的原因是，许多开发者在修改 NFS 服务器上的 /etc/exports 文件后，忘记了运行 **exportfs**（即**重启 rpc.mountd 和 rpc.nfsd**）。

卸载 NFS 文件系统与卸载本地文件系统完全相同。请注意，也可以通过不太信任 NFS 服务器来增强 NFS 客户端的安全性。例如，你可以使用 **nosuid** 选项禁用 suid 程序在 NFS 文件系统上运行。这意味着服务器的 root 用户无法在文件系统中创建一个 suid-root 程序，登录客户端作为普通用户，然后使用该 suid-root 程序在客户端上也成为 root。还可以使用 **noexec** 选项完全禁止在挂载的文件系统上执行文件。你可以在 /etc/fstab 文件中描述你的 NFS 挂载点的那一行的选项列中输入这些选项。

此时，文件分发方案和基于 NFS 的 CGI 数据目录都已就绪。现在是配置 Apache 并确保其安全的时候了。

NFS 环境中的主要瓶颈是 NFS 服务器的磁盘 I/O 速度。磁盘 I/O 速度取决于你为 NFS 服务器使用何种磁盘子系统。对于大多数情况，使用 IDE 磁盘运行 NFS 服务器的性能不如使用具有高转速的 ultra-wide SCSI 驱动器的服务器。每秒的最大 I/O 操作次数将决定你的 NFS 服务器表现如何。我使用过一台配备 10 块 ultra-wide SCSI 磁盘组 RAID 5 的 Intel Xeon 500 系统作为 NFS 服务器，为大约 50 名用户提供服务，取得了很好的成功。

在确定了良好的磁盘子系统（例如使用 10K RPM ultra-wide SCSI 磁盘阵列和带有大容量内置磁盘缓存的磁盘控制器的 RAID 5）之后，你的下一个硬件瓶颈就是网络本身。将高带宽流量隔离到其专用网络中是减少性能损失的好方法。因此，我建议你使用专用的 100Mbits 以太网连接 NFS 服务器和 NFS 客户端。换言之，创建一个仅传输 NFS 数据包的 NFS 骨干网。这将实现一个高性能的 NFS 网络。

可以帮助你调整 NFS 服务器性能的软件配置选项将在以下部分中介绍。

### 优化读写块大小

NFS 的默认读写块大小为 4096 字节（4K），这对所有情况来说可能并不最优。你可以执行测试来确定更改块大小是否会提高性能。执行此类测试的方法如下。





本测试假设您在 Linux 系统上运行着一个 NFS 服务器，并且拥有一个基于 Linux 的 NFS 客户端系统。该测试还假设客户端挂载了来自 NFS 服务器的名为 `/mnt/nfs1` 的文件系统。

1. 在 NFS 客户端机器上 `su` 切换到 root 用户。
2. 首先，您需要了解系统的总内存量。您应该知道默认值，因为这是您的系统，但如果您记得不太清楚，可以运行 `cat /proc/meminfo` 命令查看系统的内存信息。这将产生如下所示的显示：

```
    total:   used:   free:  shared: buffers:  cached:
Mem:   263720960  260456448  3264512  30531584  228245504
6463488
Swap:  271392768  6209536  265183232
MemTotal:   257540 kB
MemFree:     3188 kB
MemShared:   29816 kB
Buffers:     222896 kB
Cached:      6312 kB
BigTotal:    0 kB
BigFree:     0 kB
SwapTotal:   265032 kB
SwapFree:    258968 kB
```

3. 系统总内存量显示在 total 列标题下；将此数字除以 1,048,576（1024×1024）即可得到总（近似）内存大小（单位为 MB）。在上面的示例中，该数值为 251MB。有趣的是，大多数 PC 系统的 BIOS 都不会准确报告总内存，因此您必须根据对总内存的了解对数字进行四舍五入。在我的示例中，我知道系统应该有 256MB 的 RAM，因此我将使用 256MB 作为此测试中的内存大小。
4. 现在切换到当前已挂载的 /mnt/nfs1 NFS 文件目录。运行 `du` 命令检查 NFS 目录上是否至少有 512MB（2× 总 RAM）的可用空间。如果没有，您无法继续此实验。
5. 下一个任务是通过在 /mnt/nfs1 目录中写入一个名为 512MB.dat 的文件（16K/块 × 32,768 块），来测量当前 NFS 设置的写入性能。请使用以下命令执行此操作：

```
time dd if=/dev/zero \
    of=/mnt/nfs1/512MB.dat \
    bs=16k count=32768
```

此命令运行 `time` 命令，该命令记录名为第一个参数的程序的执行时间。在这种情况下，正在计时的是 `dd` 命令。给 `dd` 命令一个输入文件（使用 `if` 选项），名为 `/dev/zero`。这是一个特殊设备，读取时返回 0（零）字符。换句话说，如果您打开此文件进行读取，它将不断返回 0 字符，直到您关闭文件。这为我们提供了一个填充输出文件（使用 `of` 选项指定，名为 `/mnt/nfs1/512MB.dat`）的便捷来源；`dd` 命令被指示使用 16K 的块大小（使用 `bs` 选项指定）并总共写入 32,768 个块（使用 `count` 选项指定）。由于 16K/块 乘以 32,768 块等于 512MB，您将创建预期的文件。执行此命令后，它会打印几行内容，例如以下所示：

```
32768+0 records in
32768+0 records out
1.610u 71.800s 1:58.91  61.7%  0+0k  0+0io 202pf+0w
```

这里，`dd` 命令从 `/dev/zero` 设备读取了 32,768 条记录，并向 `/mnt/nfs1/512MB.dat` 文件写回了相同数量的记录。第三行表明复制操作耗时 1 分 58.91 秒。请按如下方式将此行记录在文本文件中：

```
Write, 1, 1.610u, 71.800s, 1:58.91, 61.7%
```

这里您正在记录这是第一次 (1) 写入实验。

6. 要测量当前 NFS 设置的读取性能，您只需读取步骤 5 中创建的 512MB 文件，看看读取它需要多长时间。要读取该文件并对读取访问进行计时，请运行以下命令：

```
time dd if=/mnt/nfs1/512MB.dat \
     of=/dev/null \
     bs=16k count=32768
```

这里，`dd` 命令再次被计时，它将 `/mnt/nfs1/512MB.dat` 文件作为输入读取，并将文件内容输出到 `/dev/null`，后者是 Linux 中官方的无底深渊。与此前一样，您应该在记录读取性能记录的同一文件中记录使用的时间。例如，在我的系统上，使用上述命令进行的读取测试显示了以下输出。

请按如下方式记录第三行：

```
Read, 1, 1.970u, 38.970s, 2:10.44, 31.3%
```

这里您正在记录这是第一次 (1) 读取实验。

7. 现在从 /mnt/nfs1 中删除 512MB.dat 文件，并使用 `umount /mnt/nfs1` 命令卸载该分区。卸载 NFS 目录可确保磁盘缓存不会影响您下一组测试。
8. 重复写入和读回测试（步骤 5 到 7）至少五次。您应该有如下所示的一组记录：

```
Read,   1. 1.971u, 38.970s,  2:10.44, 31.3%
Read,   2. 1.973u, 38.970s,  2:10.49, 31.3%
Read,   3. 1.970u, 38.971s,  2:10.49, 31.3%
Read,   4. 1.978u, 38.970s,  2:10.49, 31.3%
Read,   5. 1.978u, 38.971s,  2:10.49, 31.3%

Write, 1. 1.610u, 71.800s,  1:58.91, 61.7%
Write. 2. 1.610u, 71.801s, 1:58.92, 61.7%
Write. 3. 1.610u, 71.801s, 1:58.92, 61.7%
Write. 4. 1.610u, 71.801s, 1:58.92, 61.7%
Write. 5. 1.611u, 71.809s, 1:58.92, 61.7%
```

9. 现在从第五列（以粗体显示）计算平均读取和写入时间。

此测试的第一阶段现在已完成。您发现了 512MB 文件的平均读取和写入访问时间。对于测试的第二阶段，请遵循以下步骤：

1. 使用 `umount /mnt/nfs1` 命令在 NFS 客户端系统上卸载 /mnt/nfs1 目录。
2. 修改 NFS 客户端系统上的 `/etc/fstab` 文件，使 `/mnt/nfs1` 文件系统使用 `size=8192, wsize=8192` 选项挂载，如下所示。

```
nfs-server-host:/nfs1 /mnt/nfs1 nfs \
size=8192,wsize=8192 0 0
```

3. 使用 `mount /mnt/nfs1` 命令重新挂载 /mnt/nfs1 目录。
4. 执行实验第一阶段中的步骤 4 到 9。
5. 比较测试阶段 1 和阶段 2 的读取和写入访问平均值。如果测试阶段 2（此部分）的结果看起来更好，那么更改读取和写入块提高了您的 NFS 性能。如果没有，请从 `/etc/fstab` 中的该行移除 `size=8192, wsize=8192` 选项。读取和写入块大小的更改很可能会提高 NFS 性能。您还可以尝试其他块大小。建议使用 1024 的倍数作为块大小，因为 1024 是实际的文件系统块大小。此外，不要使用大于 8192 字节的数字。如果块大小更改对您有效，请在 `/etc/fstab` 中 `/mnt/nfs1` 定义的行中保留 `size=8192, wsize=8192`（或通过进一步实验找到的最佳值）。

## 设置适当的最大传输单元

最大传输单元 (MTU) 值决定了单个数据包传输可以有多大。如果 MTU 设置得太小，NFS 性能会严重受损。要发现合适的 MTU 设置，请执行以下操作：

1. 在 NFS 客户端系统上 `su` 切换到 root 用户。
2. 运行 `trac-path nfsserver/2049` 命令，其中 `nfsserver` 是您的 NFS 服务器的主机名。该命令将报告该路径的 MTU。
3. 检查用于访问 NFS 服务器的网络接口的当前 MTU。您可以简单运行 `ifconfig` 命令列出所有正在运行的网络接口的信息。
4. 如果您发现适当网络接口的 MTU 设置与 `trac-path` 命令报告的不一致，请使用带有 `mtu` 选项的 `ifconfig` 命令进行设置。例如，`ifconfig eth0 mtu 512` 命令将网络接口 `eth0` 的 MTU 设置为 `512` 字节。

## 运行最优数量的 NFS 守护进程

默认情况下，您运行八个 NFS 守护进程。如果您想查看每个 `nfssd` 线程的使用强度，请运行 `cat /proc/net/rpc/nfsd` 命令。该文件中 `th` 行的最后十个数字表示 `nfssd` 线程使用率处于该百分比（最大允许值）的秒数。如果前三个十分位数中有较大的数字，您可能希望增加 `nfssd` 实例的数量。要更改服务器启动时启动的 NFS 守护进程数量，请执行以下操作：

1. 作为 root，如果您当前正在运行它，请使用 `/etc/rc.d/init.d/nfs stop` 命令停止 `nfssd`。
2. 修改 `/etc/rc.d/init.d/nfs` 脚本，将 `RPCNFSDCOUNT=8` 设置为适当数量的 NFS 守护进程。
3. 使用 `/etc/rc.d/init.d/nfs start` 命令重启 `nfssd`。

## 控制套接字输入队列大小

默认情况下，Linux 使用 `65535` 字节（`64KB`）的套接字输入队列。如果您在系统上运行 8 个 NFS 守护进程（`nfssd`），每个守护进程获得 `8K` 缓冲区来在输入队列中存储数据。您应该将队列大小增加到至少 `256KB`，如下所示：

1. 作为 root，如果您当前正在运行它，请使用 `/etc/rc.d/init.d/nfs stop` 命令停止 `nfssd`。
2. 修改 `/etc/rc.d/init.d/nfs` 脚本，使得在通过守护进程行 `rpc.nfsd $RPCNFSDCOUNT` 启动 NFS 守护进程（`nfssd`）之前，添加以下行：
   ```
   echo 262144 > /proc/sys/net/core/rmem_default
   echo 262144 > /proc/sys/net/core/rmem_max
   ```
3. 在守护进程行 `rpc.nfsd $RPCNFSDCOUNT` 之后立即添加以下行：
   ```
   echo 65536 > /proc/sys/net/core/rmem_default
   echo 65536 > /proc/sys/net/core/rmem_max
   ```
4. 使用 `/etc/rc.d/init.d/nfs start` 命令重启 NFS 守护进程。

现在，由 `/etc/rc.d/init.d/nfs` 脚本启动的每个 NFS 守护进程将使用套接字输入队列中的 `32K` 缓冲空间。




## 监控数据包碎片

Linux 内核使用从高到低的范围来控制其能够处理的未处理 UDP 数据包碎片数量。当未处理的 UDP 数据包碎片大小达到高阈值（通常为 262144 字节或 256K）时，内核会丢弃传入的数据包碎片。换句话说，当 UDP 数据包碎片达到高阈值时，就开始出现丢包。数据包碎片的丢失会持续，直到未处理碎片的总大小达到低阈值（通常为 196608 字节或 192K）。

由于 NFS 协议使用分片的 UDP 数据包，Linux 使用的上述从高到低的阈值对 NFS 性能有很大影响。你可以通过运行 `cat /proc/sys/net/ipv4/ipfrag_high_thresh` 命令来查看当前高阈值大小的值。同样，你可以通过运行 `cat /proc/sys/net/ipv4/ipfrag_low_thresh` 命令来查看低阈值的值。你可以通过运行 `echo high_number > /proc/sys/net/ipv4/ipfrag_high_thresh` 来更改高值，类似地，运行 `echo low_number > /proc/sys/net/ipv4/ipfrag_low_thresh` 可更改低数值。

## 在 Web 服务器之间复制内容

通常，内容是在单个（主）服务器上开发和放置的，然后分发到参与 Web 网络的所有其他 Web 服务器。在本节中，我将讨论一个名为 `rdist` 的工具，它允许你将内容从一个 Linux 系统分发到其他系统。

### 使用 rdist 分发文件

`rdist` 程序使你可以在多台主机上维护文件的相同副本。它使用 `rcmd` 函数调用或远程 shell（`rsh`）来访问每个目标主机计算机。

让 `rdist` 运行的最简单方法是在所有涉及的机器上创建一个通用账户，并为每个目标 Web 服务器系统创建 `.rhosts` 文件，以便命名服务器主机上的通用用户被允许运行 `rsh` 会话。为此，请在所有三个涉及的系统上创建一个名为 `httpd` 的用户。在每个 Web 服务器系统上，在 `httpd` 用户的主目录中添加一个 `.rhosts` 文件。此文件包含 `rdist` 服务器的主机名，位于单行中。

`.rhosts` 文件必须由 root 用户拥有，并且对其他所有人只读。这允许在 `rdist` 服务器上名为 `httpd` 的用户在每个 Web 服务器系统上运行远程 shell 会话。如果你按照前面的章节说明创建了后端网络，你应该使用与后端网络接口关联的 `rdist` 服务器主机名，这使你能够将 `rdist` 生成的文件流量保留在后端网络中；因此，数据包不会与你的 Web 流量竞争。下一步是为 `rdist` 创建一个 distfile。distfile 是一个文本文件，其中包含 `rdist` 如何执行文件分发任务的指令。列表 23-2 显示了这样一个 distfile，`rdist_distfile`。

#### 列表 23-2：rdist_distfile

```
# Distfile for rdist
#
# This is used to distribute files from ns.domain.com
# to www[12].domain.com systems
#
# $Author$ (kabir@ntec.com)
# $Version$
# $Date$
# $Id$

# List all the hosts that need to be updated.
# The list is created using user@hostname entries where each
# entry is separated by a whitespace character.
#
HOSTS = (httpd@www1.domain.com httpd@www2.domain.com)

# List the directories that need to be updated.
#
FILES = (//www)

# list the directories that need to be excluded from
# the update process.
EXCLUDE_DIR = (//www/cgi-data/ //www/apache //www/secured)

# Here are the commands:
# Install all directories listed in FILES for all hosts
# listed in HOSTS except for the directories that are
# listed in EXCLUDE_DIR
#
#!/FILES/ -> ${HOSTS}
install :
    except ${EXCLUDE_DIR};
```

这确实是一个非常简单的 distfile。它定义了一个名为 HOSTS 的变量，该变量有两个条目作为值：httpd@www1.domain.com 和 httpd@www2.domain.com。这告诉 rdist 使用 www1.domain.com 和 www2.domain.com 上的 httpd 用户账户进行连接。下一个变量 FILES 定义了 rdist 要分发的文件和目录。此脚本假设暂存服务器将所有文件保留在 /www 目录或分区中。你可以更改此路径或添加多个路径（以空格分隔）。

第三个变量是 EXCLUDE_DIR。该变量设置为列出我们希望从分发过程中排除的所有文件和目录。示例中看到的值很重要。第一个目录 /www/cgi-data/ 是 CGI 数据目录，所有 CGI 脚本都将数据写入此目录。此目录将通过 NFS 导出到 Web 服务器主机，因此无需通过 rdist 复制到每个 Web 服务器。`/www/apache` 目录是 makesite 写入 `/www/apache/conf/httpd.conf` 文件的位置，该文件需要复制，因为每个 Web 服务器在其本地的 `/www/apache` 目录中都有其自己的 Apache 配置文件。最后一个值是 `/www/secured`，它由 secure 服务器用作文档根目录，需要复制到 Web 服务器上。文件的其余部分描述了一个简单命令：

```shell
$ {FILES} -> ${HOSTS}
    install ;
    except ${EXCLUDE_DIR};
```

此命令获取 FILES 变量指向的所有文件和目录，并将它们安装到 HOSTS 变量指示的主机上。它还告诉 rdist 排除 EXCLUDE_DIR 变量指定的文件和目录。要以 httpd 身份运行 rdist，请使用以下命令行：

```shell
/usr/bin/rdist -p /usr/sbin/rdistd \
     -oremove,quiet \
     -f /usr/local/rdist/ rdist_distfile
```

-p 选项指定 rdist 所需的 rdist 程序的位置；-o 选项指定一个或多个选项将跟随——在这种情况下，是 `remove` 和 `quiet`。`remove` 选项告诉 rdist 删除目标系统中目标目录中发现的任何错误文件。这提供了一种简单的方法来维护每个 Web 服务器上暂存区域的相同副本。`quiet` 选项告诉 rdist 在操作期间尽可能保持安静。最后一个选项 -f 指定 distfile 的位置。

为了减少运行此命令时的人为错误，请创建一个名为 `rdistribute.sh` 的 sh 脚本，如列表 23-3 所示。

#### 列表 23-3：rdistribute.sh 脚本

```shell
#!/bin/sh
#
# This script runs rdist to update Web servers via the
# non-routable lan domain.com. The script is run
# by cron at a fixed interval.
#
# /etc/rc/rc.local starts the script to clean up
# left-over tempfiles that might have been left
# at shutdown. This process also removes the
# log file.
#
# Authors (kabor@evoknow.com)
# $Version$
# $Id$
# $Date$
# $Status

RDIST=/usr/bin/rdist
RDISTD=/usr/sbin/rdistd
DIST_FILE=/usr/local/rdist/rdist_distfile
RDIST_OPTIONS='remove,nochkgroup,nochkmode,nochkowner,quiet'
RDIST_LOCK_FILE=/tmp/rdist.lck
RDIST_LOG_FILE=/tmp/rdist.log
TOUCH_BIN=/bin/touch
DATE=`date`

# If the script is called with an argument, then
case "$1" in
    boot)
        # Because the argument is 'boot', the script is being
        # called at system start-up, so remove all old lock
        # files and logs.
        echo -n "Cleaning up distribute.sh tmp files: "
        rm -f $RDIST_LOCK_FILE
        rm -f $RDIST_LOG_FILE
        echo "complete."
        exit 0;
    ;;

    # Because the argument is 'restart,' the script
    # needs to clean up as if the system just booted.
    restart)
    $0 boot
    ;;

esac

# If the lock file exists, then don't do anything.
if [ -f $RDIST_LOCK_FILE ]; then
    exit 0
fi

# Otherwise, create the lock file using touch
$TOUCH_BIN $RDIST_LOCK_FILE

# Run rdist
$RDIST -p $RDISTD -o$RDIST_OPTIONS -f $DIST_FILE

# Remove the lock file
rm -f $RDIST_LOCK_FILE

# Write the time and date in the log file
echo $DATE >> $RDIST_LOG_FILE

# Exit the script.

exit 0
```

此脚本足够智能，可以通过使用锁定文件检测正在进行的 `rdistribute.sh` 进程，从而判断之前的 `rdistribute.sh` 是否已经在进行中并继续运行。当大量文件在多台服务器上更新时，可能会发生这种情况。该脚本还接受一个名为 `boot` 的参数，可用于在启动过程中清理其创建的锁定文件和日志文件。该脚本应从 `/etc/rc.d/rc.local` 按以下方式调用：

```text
/usr/local/rdistribute.sh boot
```

此脚本可以通过 `/etc/crontab` 中的 cron 条目计划运行。例如，每 10 分钟运行一次此脚本，可以在 `/etc/crontab` 中添加以下 cron 条目：

```text
0,10,20,30,40,50 * * * * httpd /usr/local/rdistribute.sh > /dev/null
```

cron 守护程序将以 `httpd` 身份运行该脚本。

## 创建基于 RAM 的文件系统

你可以在 RAM 中创建一个临时的、小的文件系统以实现高速访问。之所以说这是一个小的文件系统，是因为默认情况下，ramfs 能使用的最大 RAM 量是你系统总 RAM 的一半。所以，如果你拥有 2GB 的 RAM，ramfs 只能使用 1GB。由于我还没有见过拥有超过 4GB RAM 的系统，即使是 2GB 的 ramfs 与今天基于大型驱动器的文件系统相比仍然非常小。ramfs 非常适合需要快速访问的许多小文件。例如，我将 ramfs 用于一个在访问量很大的网站上使用的一小组小图像。

### 启用基于 RAM 的文件系统

要使用 ramfs，你必须按以下方式在 kernel 中启用 ramfs 支持：

- 1. 从 www.kernel.org 获取最新的 Linux 内核源代码，并以 root 身份将其解压到 `/usr/src/linux-version` 目录，其中 `version` 是当前的内核版本。对于此材料，我假设这是 2.4.1。
- 2. 选择文件系统子菜单。通过使用空格键，选择 Simple RAM-based file system support 作为内核模块包含在内，并退出子菜单。
- 3. 确保你使用的其他所有内核功能也按常规被选中。
- 4. 退出主菜单并保存内核配置。
- 5. 按 `menuconfig` 程序的建议运行 `make dep` 命令。
- 6. 现在运行 `make bzimage` 来创建新的内核。然后运行 `make modules` 和 `make modules_install` 将新模块安装到适当的位置。





7. 将目录更改为 `arch/i386/boot`。如果硬件架构是 Intel，则需要替换 `i386`，并且可能还需要参考内核使用说明文档来编译和安装你的内核版本。我假设大多数读者的系统是基于 i386 的，并以此继续说明。

8. 将 `bzImage` 复制到 `/boot/vmlinuz-2.4.1`，并编辑 `/etc/lilo.conf` 文件以包含新的配置，如下所示：
```text
image=/boot/vmlinuz-2.4.1
label=linux3
read-only
root=/dev/hda1
```

9. 运行 `/sbin/lilo` 命令重新配置 `lilo` 并重启系统。在 `lilo` 提示符下输入 `linux3` 以启动新内核。如果遇到问题，你应该能够重启到标准的 Linux 内核，这应该是默认选项。

10. 启动新内核后，你就准备好使用 ramfs 了。使用 `mkdir /ramdrive` 命令创建一个名为 `ramdrive` 的目录。

11. 现在使用 `mount -t ramfs none /ramdrive` 命令挂载 ramfs 文件系统。

一切就绪；你现在可以像往常一样向 `/ramdrive` 写入文件了。

> **注意**
>
> 请预先知悉，当系统重启或你卸载文件系统时，所有内容将丢失。这就是为什么它应该用作高速访问的临时空间。此外，请注意，由于 ramfs 实际上并不是一个块设备，诸如 `df` 和 `du` 等程序无法看到它。你可以通过运行 `cat /proc/mounts` 命令并找到如下条目来验证你确实正在使用 RAM：
> ```text
> none /ram ramfs rw 0 0
> ```

> **提示**
>
> 在挂载文件系统时，你可以使用 `-o` 选项来指定选项，就像挂载基于常规磁盘的文件系统一样。例如，要将 ramfs 文件系统挂载为只读，你可以使用 `-o ro` 选项。你還可以指定特殊选项，例如 `maxsize=n`，其中 `n` 是为 RAM 中文件系统分配的千字节数；`maxfiles=n`，其中 `n` 是文件系统允许的文件总数；以及 `maxnodes=n`，其中 `n` 是 inode 的最大数量（默认为 `0` = 无限制）。

# 利用基于 RAM 的文件系统

如果你运行 Web 服务器，基于 RAM 的文件系统将有多种用途。网站上的常见图片和文件，只要不是太大（不超过几 KB），都可以保存在 ramfs 文件系统中。你可以编写一个简单的 shell 脚本，在每次重启时从原始位置复制内容。列表 23-4 是一个执行此操作的简单脚本。

## 列表 23-4: _make_ramfs.sh_

```sh
#!/bin/sh
#
# Simply script to create a ramfs file system
# on $MOUNTPONT (which must exists).
#
# It copies files from $ORIG_DIR to $MOUNTPONT
# and changes ownership of $MOUNTPONT to
# $USER and $GROUP
#
# Change values for these variables to suit
# your needs.

MOUNTPONT=/ram
ORIG_DIR=/www/commonfiles

USER=httd
GROUP=httpd

MOUNTCMD=/bin/mount
CHOWN=/bin/chown
CP=/bin/cp

echo -n "Creating ramfs file system in $MOUNTPONT ":
$MOUNTCMD -t ramfs none $MOUNTPONT
echo "done."

echo -n "Copying $ORIG_DIR to $MOUNTPONT ... ":
$CP -r $ORIG_DIR $MOUNTPONT
echo "done."

echo -n "Changing ownership to $USER:$GROUP for $MOUNTPONT ...":
$CHOWN -R $USER:$GROUP $MOUNTPONT
echo "done."
```

要在系统上使用该脚本，请执行以下操作：

- 1. 在 `/usr/local/scripts` 目录中创建 `make_ramfs.sh`。如果没有该目录，请创建 `/usr/local/scripts` 目录。
- 2. 编辑 `/etc/rc.d/rc.local` 文件并在其中追加以下行：
  `/usr/local/scripts/make_ramfs.sh`
- 3. 使用 `mkdir ram` 命令创建一个名为 `ram` 的目录。如果你想将加载到 RAM 中的文件保存在 `/www/commonfiles` 以外的任何位置，请修改脚本中 `ORIG_DIR` 变量的值。例如，如果你的文件位于 `/www/mydomain/htdocs/common` 目录中，请将此变量设置为指向该目录。
- 4. 如果你使用除 `httpd` 以外的用户名或组来运行 Web 服务器，则相应地修改 `USER` 和 `GROUP` 变量的值。例如，如果你以 `nobody`（用户和组）运行 Apache，则设置 `USER=nobody` 和 `GROUP=nobody`。
- 5. 如果你正在使用 Apache Web 服务器，请在 `httpd.conf` 文件中创建一个别名，如下所示：

```text
Alias /commonfiles/ "/ram/commonfiles/"
```

每当 Apache Web 服务器需要访问 `/commonfiles/*` 时，它将使用 RAM 中的版本，这应该比存储在原始位置的文件快得多。请记住，基于 RAM 的版本会在你重启或卸载文件系统时消失。因此，除非你同时也将内容复制回基于磁盘的目录，否则永远不要更新那里的任何内容。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_701_0.png)

如果你使用类似 `mount -t ramfs none /ram` 的命令挂载了 `ramfs` 文件系统并将内容复制进去，之后重新运行相同的挂载命令，则重新运行该命令会清除内容并重新挂载 `ramfs`。`/proc/mounts` 文件显示同一个挂载点有多个条目，这会导致卸载设备时出现问题。如果你必须重新获得内存以作他用，则必须重启。希望此问题很快能得到解决。

# 创建可靠的后端网络

典型的 Web 网络由一组 Web 服务器、代理服务器、应用服务器、数据库服务器等组成。在大多数情况下，只有 Web 服务器和代理服务器（如果有）需要位于 Web 网络的前端。图 23-3 显示了一个具有前端和后端网络的 Web 网络示例。

每个 Web 服务器节点有两个网络接口。一个接口连接到前端网络 `207.185.233.0/24`，另一个接口连接到后端网络 `192.168.1.0/24`。前端网络由 Web 服务器和负载平衡硬件组成；后端网络由 Web 服务器、应用服务器和数据库服务器组成。

当请求到达活动（主）负载均衡器时，将执行以下一系列操作：

- 负载均衡器确定处理请求的最佳 Web 服务器，并将请求传递给相应的 Web 服务器。
- Web 服务器决定请求是否需要额外资源。例如，如果请求是在应用服务器上运行应用程序，Web 服务器将选择合适的应用服务器和/或数据库服务器，并执行完成请求所需的任务。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_702_0.png)

**图 23-3：** 具有前端和后端网络的 Web 网络

应用服务器和数据库服务器不需要通过 Web 直接访问，因为只有前端网络中的 Web 服务器才与它们联系。这确保了良好的安全性，因此，对于连接到 Web 网络的所有后端网络，使用不可路由的 192.168.x.x 网络地址是一个好主意。

然而，大型 Web 网络要求对应用服务器和数据库服务器也进行负载平衡，否则应用或数据库的使用将成为非常繁忙站点的重大瓶颈。图 23-4 显示了一个高度平衡的 Web 网络，它对前端和后端网络都使用了负载平衡硬件。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_703_0.png)

**图 23-4：** 具有前端和后端负载均衡器的 Web 网络

# 加强你的 Web 网络

黑客发现 Web 网络或构成 Internet 服务的任何节点集群都是攻击的理想目标。这是因为如果他们能够入侵计算机网络，该网络就可以用作攻击其他系统的跳板。基本上，安全防护薄弱但连接良好（高带宽）的 Web 网络为黑客提供了攻击他人的巨大资源。这可能导致 Web 网络管理员面临严重问题。因此，至关重要的是，你必须采取所有可能的预防措施来降低被攻击的风险。有关如何保护 Web 服务器的详细信息，请参见第 18 章。本节提供了适合 Web 网络以及单服务器系统的其他安全相关信息。





## 使用 Tripwire 保护您的 Web 内容

作为向开源软件迈出的一大步，Tripwire 在通用公共许可证（GPL）下发布了 Tripwire 开源版 Linux 版本。简而言之，Tripwire 是一个文件和目录完整性检查器，它针对所有文件和目录创建签名数据库，并将它们存储在单个文件中。当再次运行 Tripwire 时，它会计算当前文件和目录的新签名，并将其与数据库中原有的签名进行比较。如果存在差异，该文件或目录的名称将连同差异信息一起被报告。

现在你可以明白，为什么 Tripwire 可以帮助确定入侵期间哪些文件被修改，成为一个非常出色的工具。当然，要做到这一点，你必须确保应用程序所使用的数据库的安全性。在设置新的服务器系统时，许多经验丰富的系统管理员会按照以下顺序执行以下操作：

- 1. 确保新系统未连接到任何网络，以保证尚未有人在其系统安全中安装木马程序、病毒程序或其他威胁。
- 2. 运行 Tripwire 创建所有重要系统文件的签名数据库，包括所有系统二进制文件和配置文件。
- 3. 将数据库写入可重写 CD-ROM。这可以确保高明的恶意攻击者无法修改 Tripwire 数据库来隐藏木马，或阻止程序识别已修改的文件。监控文件数量较少的管理员通常使用软盘来存储数据库。将数据库写入软盘后，软盘将被设置为写保护状态，如果 BIOS 允许，硬盘将被配置为只读设备。
- 4. 设置一个 cron 任务，定期（每日、每周、每月）运行 Tripwire，使应用程序使用 CD-ROM 版本的数据库。

### 获取 Tripwire

Red Hat Linux 附带了 Tripwire 的二进制 RPM 文件。但是，你始终可以从 RPM 镜像站点（如 `http://fr.rpmfind.net`）下载免费的（LGPL）Tripwire 版本。我使用该站点通过 `http://fr.rpmfind.net/linux/rpm2html/search.php?query=Tripwire` 下载了 Tripwire 的源代码和二进制文件。我下载的源代码 RPM 缺少一些安装脚本，因此我从位于 `http://sourceforge.net/projects/tripwire/` 的 Tripwire 开源开发站点再次下载了源代码。我下载的源代码名为 `tripwire-2.3.0-src.tar.gz`。当你阅读本文时，你可能会在那里发现更新的版本。

### 编译 Tripwire

本节向你展示如何从 `tripwire-2.3.0-src.tar.gz` 文件编译、配置和安装 Tripwire。在执行这些步骤时，请确保将你下载的版本替换为 Tripwire 的实际版本号。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_705_0.png)

**注意**

如果你希望从二进制 RPM 包安装 Tripwire，只需从 Tripwire RPM 所在的目录运行 `rpm -ivh tripwire-version.rpm` 命令即可。你仍然需要通过运行 `twininstall.sh` 来配置 Tripwire。请从 `/etc/tripwire` 目录运行此脚本，并跳转到下一节的第 7 步。

要从源码发行版进行编译，请执行以下操作：

- 1. 作为 root 用户，使用 `tar xzvf tripwire-2.3.0-source.tar.gz` 命令解压 tar 包。这将创建一个名为 `/usr/src/redhat/SOURCES/tripwire-2.3.0-src` 的子目录。将当前目录更改为 `/usr/src/redhat/SOURCES/tripwire-2.3.0-src/src` 目录。
- 2. 运行 `make release` 命令编译所有必要的 Tripwire 二进制文件。这需要一点时间，所以最好在喝咖啡前执行。编译完成 Tripwire 后，你需要安装二进制文件。将目录更改为 `/usr/src/redhat/SOURCES/tripwire-2.3.0-src/install`。使用 `cp install.* ..` 命令将 `install.cfg` 和 `install.sh` 文件复制到父目录。
- 3. 在运行安装脚本之前，可能需要编辑 `install.cfg` 文件，如列表 23-5 所示。例如，如果你不是 vi 编辑器的粉丝，而是支持 emacs，你需要将文件中的 `TWEDITOR` 字段更改为指向 emacs，而不是 `to /usr/bin/vi`。我不建议更改 `CLOBBER`、`TWBIN`、`TWPOLICY`、`TWMAN`、`TWDOC`、`TWDOCSDIR`、`TWSITEKEYDIR` 或 `TWLOCALKEYDIR` 设置的值。但是，你可能需要更改 `TWLATEPROMPTING`、`TWLOOSEDIRCHKS`、`TWMAILNOTIFICATIONS`、`TWMAILREPORTLEVEL`、`TWREPORTLEVEL`、`TWSYSLOG`、`TWMAILMETHOD` 和 `TWMAILPROGRAM` 的值。

**列表 23-5: install.cfg**

```
#
# install.cfg
#
# default install.cfg for:
# Tripwire(R) 2.3 Open Source for Linux
#
# NOTE:  This is a Bourne shell script that stores installation
#  parameters for your installation.  The installer will
#  execute this file to generate your config file and also to
#  locate any special configuration needs for your install.
#  Protect this file, because it is possible for
#  malicious code to be inserted here.
#
# This version of Tripwire has been modified to conform to the FHS
# standard for Unix-like operating systems.
#
# To change the install directory for any tripwire files, modify
# the paths below as necessary.
#
#------------------------------------------------

# If CLOBBER is true, then existing files are overwritten.
# If CLOBBER is false, existing files are not overwritten.
CLOBBER=false

# Tripwire binaries are stored in TWBIN.
TWBIN="/usr/sbin"

# Tripwire policy files are stored in TWPOLICY.
TWPOLICY="/etc/tripwire"

# Tripwire manual pages are stored in TWMAN.
TWMAN="/usr/man"

# Tripwire database files are stored in TWDB.
TWDB="/var/lib/tripwire"

# Tripwire documents directory
TWDOCS="/usr/doc/tripwire"

# The Tripwire site key files are stored in TWSITEKEYDIR.
TWSITEKEYDIR="${TWPOLICY}"

# The Tripwire local key files are stored in TWLOCALKEYDIR.
TWLOCALKEYDIR="${TWPOLICY}"

# Tripwire report files are stored in TWREPORT.
TWREPORT="${TWDB}/report"

# This sets the default text editor for Tripwire.
TWEDITOR="/bin/vi"

# TWLATEPROMPTING controls the point when tripwire asks for a password.
TWLATEPROMPTING=false

# TWLOSEDIRCHK selects whether the directory should be monitored for
# properties that change when files in the directory are monitored.
TWLOOSDIRCHK=false

# TWMAILNOVIOLATIONS determines whether Tripwire sends a no violation
# report when integrity check is run with - email-report but no rule
# violations are found. This lets the admin know that the integrity
# was run, as opposed to having failed for some reason.
TWMAILNOVIOLATIONS=true

# TWEMAILREPORTLEVEL determines the verbosity of e-mail reports.
TWMAILREPORTLEVEL=3

# TWREPORTLEVEL determines the verbosity of report printouts.
TWREPORTLEVEL=3

# TWSYSLOG determines whether Tripwire will log events to the system log
TWSYSLOG=false

######################################################################
# Mail Options - Choose the appropriate
# method and comment the other section
######################################################################
#
#####################
# SENDMAIL options - DEFAULT
#
# Either SENDMAIL or SMTP can be used to send reports via TWMAILMETHOD.
# Specifies which sendmail program to use.
################################################################

TWMAILMETHOD=SENDMAIL
TWMAILPROGRAM="/usr/lib/sendmail -oi -t"

######################################################################
# SMTP options
#
# TWSMTPHOST selects the SMTP host to be used to send reports.
# TWSMTPPORT selects the SMTP port for the SMTP mail program to use.
######################################################################

# TWMAILMETHOD=SMTP
# TWSMTPHOST="mail.domain.com"
# TWSMTPPORT=25

###############################################################################################################################################
# Copyright (C) 1998-2000 Tripwire (R) Security Systems, Inc. Tripwire (R) is a
# registered trademark of the Purdue Research Foundation and is licensed
# exclusively to Tripwire (R) Security Systems, Inc.
###############################################################################################################################################
```

- 4. 运行 `./install.sh` 命令。此命令将引导你完成安装过程。你需要按 Enter 键以接受 GPL 许可协议，并同意文件将复制到的位置。
- 5. 文件复制完成后，系统将提示你输入站点口令短语。此口令短语用于加密 Tripwire 配置和政策文件。请输入一个强口令短语（即不易被猜出且长度至少为 8 个字符的短语），以确保这些文件不会被任何未知方修改。接下来，选择一个本地口令短语。此口令短语用于加密 Tripwire 数据库和报告文件。同样，请在此处选择一个强口令短语。




6. 输入站点密码短语，安装程序将使用您的密码短语对配置文件进行签名。Tripwire 配置文件的明文版本将被创建在 `/etc/tripwire/twcfg.txt` 中。Tripwire 使用的加密二进制版本的配置文件将存储在 `/etc/tripwire/tw.cfg` 中。创建明文版本是为了供你检查。安装程序建议你检查完此文件后手动删除它。

7. 输入站点密码短语，以便安装程序可以将其用于对策略文件进行签名。安装程序会在 `/etc/tripwire/twpol.txt` 中创建一个明文策略文件，加密版本则保存在 `/etc/tripwire/tw.pol` 中。稍后你将学会如何修改策略文件的文本版本，并能够创建 Tripwire 使用的二进制加密版本。

软件安装工作就此全部完成。

## 配置 Tripwire 策略

策略文件定义了 Tripwire 用于执行完整性检查的规则。每条规则定义了要检查哪些文件和目录，以及应该执行何种类型的检查。此外，每条规则还可以包含名称和严重级别等信息。规则语法如下所示：

```
(attribute-value attribute-value ...)
{
    /path/to/a/file/or/directory    -> mask;
}
```

表 23-1 列出了可用的属性及其含义。

**表 23-1 可用属性列表**

| **属性** | **含义** |
| :--- | :--- |
| `rulename=name` | 该属性将名称与规则关联。这使得 Tripwire 报告更具可读性，并便于按命名规则排序。 |
| `emailto=emailaddress` | 当规则被违反时，作为该属性值的电子邮件地址将接收违规报告。 |
| `severity=number` | 该属性允许你为规则关联一个严重级别，即重要程度。这使得 Tripwire 报告更易于管理。 |
| `recurse=true \| false` | 该属性确定是否自动递归遍历目录。如果设置为 true（或 -1），则递归遍历所有子目录；另一方面，如果设置为 false（或 0），则不遍历子目录。介于 -1 到 1000000 之间的任何数值（不包括 -1 和 0）指定了递归遍历子目录的深度。例如，`recurse=3` 表示递归遍历深度至 3 级的子目录。 |

这是一个示例规则：

```
(Rulename= "OS Utilities", severity=100)
{
  /bin/ls    -> +pintugtsdrbамcCMSH-l;
}
```

在这里，所定义的规则称为“OS `Utilities`”规则；其严重级别评级为 100，这意味着违反此规则将被视为主要问题；会检查 `/bin/ls` 的 `+pintugtsdrbамcCMSH-l` 属性。表 23-2 说明了这些属性/掩码字符中每个字符的含义。

## 表 23-2
**Tripwire 策略文件中使用的属性/掩码字符**

| 属性或掩码 | 描述 |
| :--- | :--- |
| a | 文件或目录的访问时间戳 |
| b | 分配给文件的块数 |
| c | inode 时间戳 |
| d | inode 所在磁盘的 ID |
| g | 所有者组 |
| i | inode 编号 |
| l | 文件大小正在增加 |
| m | 修改时间戳 |
| n | inode 引用计数或链接数 |
| p | 文件或目录的权限位 |
| r | 属于设备文件的 inode 所指向设备的 ID |
| s | 文件大小 |
| t | 文件类型 |
| u | 所有者的用户 ID |
| C | CRC-32 值 |
| H | Haval 值 |
| M | MD5 值 |
| S | SHA 值 |
| + | 记录并检查该字符后面的属性 |
| - | 忽略该字符后面的属性 |

编写上一条规则的另一种方式是：

`/bin/ls -> +pinctstsdramcCM$H-l (Rulename= "OS Utilities", severity=100);`

然而，第一种方法更受推荐，因为它允许你将许多文件和目录分组在一个单一规则下。例如：

```
SEC_CRIT  = +pinctstsdramcCM$H -l;

(Rulename= "OS Utilities", severity=100)
{
	/bin/ls		-> $(SEC_CRIT);
	/bin/login		-> $(SEC_CRIT);
	/bin/ls		-> $(SEC_CRIT);
	/bin/mail		-> $(SEC_CRIT);
	/bin/more		-> $(SEC_CRIT);
	/bin/mt		-> $(SEC_CRIT);
	/bin/mv		-> $(SEC_CRIT);
	/bin/netstat	-> $(SEC_CRIT);
}
```

在这里，列出的所有实用程序都归入同一个策略。注意变量 SEC_CRIT 的使用，它在规则中被使用之前先进行了定义。该变量被设置为 `+pinctstsdramcCM$H-l`，并使用 `$(SEC_CRIT)` 在规则语句中替换。这使得你可以定义一个包含一组属性的单一变量，将其应用于大数量的文件和/或目录。当你想要添加或移除属性时，只需更改变量的掩码值；该更改将在使用该变量的所有地方生效。表 23-3 中展示了一些内置变量。

**表 23-3**
**Tripwire 策略文件的内置变量**

| 变量 | 含义 |
| :--- | :--- |
| ReadOnly | `+pInugtsdbcmR-lacRSH.` 适用于应保持只读状态的文件。 |
| Dynamic | `+pInugtd-srlbmcCmSH.` 适用于动态变化的用户目录和文件。 |
| Growing | `+pInugd1-srbamcCmSH.` 适用于尺寸在增长的文件。 |
| Device | `+pugSdr-intlbamcCmSH.` 适用于设备文件。 |
| IgnoreAll | `-pInugtsdrIbmcCmSH.` 仅检查文件是否存在，但不检查其他任何内容。 |
| IgnoreNone | `+pInugtsdrbamacCmSH-l.` 与 IgnoreAll 相反。检查所有属性。 |

创建规则时，你必须考虑以下事项：

- 不要创建多个应用于同一文件或目录的规则。例如：

```
/usr         -> $(ReadOnly);
/usr         -> $(Growing);
```

Tripwire 会抱怨上述策略。

- 最具体的规则将被优先执行。例如：

```
/usr           -> $(ReadOnly);
/usr/local/home  -> $(Dynamic);
```

当检查文件 /usr/local/home/filename 时，将检查由变量 $(Dynamic) 替换的属性。

如果你创建或修改了规则，你需要运行 `/usr/sbin/twadmin --create-polfile /etc/twpol.txt` 命令来生成加密的 `/etc/tripwire/tw.pol` 策略文件。系统会提示你输入用于对策略文件进行签名（即加密）所需的站点密码短语。

## 创建 Tripwire 数据库

在初始化 Tripwire 数据库文件之前，请绝对确定黑客尚未修改当前系统上的文件。这就是为什么创建此数据库的最佳时机是在系统尚未连接到互联网或任何其他网络的时候。在你确定文件未被篡改后，运行以下命令：

```
/usr/sbin/tripwire --init
```

此命令应用了 `/etc/tripwire/tw.pol` 文件中列出的策略，并在 `var/lib/tripwire/k2.intevo.com` 中创建一个数据库。

创建数据库后，如果可能，请将其移动至只读介质，如 CD-ROM 或写保护的软盘。

## 保护 Tripwire 本身

黑客可能会修改 Tripwire 二进制文件（`/usr/sbin/tripwire`）或 `/etc/tripwire/tw.pol` 策略文件，以掩盖他们的痕迹。为了帮助防止这种情况，你可以运行 `/usr/sbin/sigen` 实用程序来为这些文件创建一组签名。要为 `/usr/sbin/tripwire` 二进制文件生成签名，请运行 `/usr/sbin/sigen -a /usr/sbin/tripwire` 命令。

你在屏幕上会看到类似以下内容：

```
Signatures for file: /usr/sbin/tripwire
RCR32 BmL3L0L
MD5 BrP2JB03uAzdbRc67iC1l6l
SHA Fl1H/HW3pb+tDhKSweOnKvFUxk
HAVAL CBLCgpPtUq2QrHurQ+sTa5tV
```

你可以通过重定向到文件来将签名保存在文件中。例如，`/usr/sbin/sigen -a /usr/sbin/tripwire > /tmp/sig.txt` 将签名存储在 `/tmp/sig.txt` 文件中。你还应该打印出签名。不要忘记也生成 `sigen` 实用程序本身的签名。如果你怀疑 Tripwire 没有正常工作，请在每个这些文件上运行 `sigen` 实用程序并比较签名。如果其中任何一个不匹配，你不应该信任那些文件；相反，你应该用新的副本替换它们，并调查差异发生的原因。

## 以交互模式运行 Tripwire 检测完整性

要以交互模式运行，请执行 `/usr/sbin/tripwire --check --interactive` 命令。在此模式下，会生成报告文件并加载到首选编辑器中。此命令生成的 Tripwire 示例报告的摘要部分如图 23-6 所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_712_0.png)

```
Tripwire(R) 2.3.0 Integrity Check Report

Report generated by:		root
Report created on:		Fri Dec 22 02:31:25 2000
Database last updated on:	Fri Dec 22 02:13:44 2000
```




## 报告摘要

```
主机名: k2.intevo.com
主机 IP 地址: 172.20.15.1
主机 ID: 无
使用的策略文件: /etc/tripwire/tw.pol
使用的配置文件: /etc/tripwire/tw.cfg
使用的数据库文件: /var/lib/tripwire/k2.intevo.com.twd
使用的命令行: /usr/sbin/tripwire --check --interactive
```

## 规则摘要

### 部分: Unix 文件系统

| 规则名称 | 严重级别 | 新增 | 移除 | 修改 |
|---|---|---|---|---|
| 不变目录 | 66 | 0 | 0 | 0 |
| 临时目录 | 33 | 0 | 0 | 0 |
| * Tripwire 数据文件 | 100 | 0 | 0 | 1 |
| 关键设备 | 100 | 0 | 0 | 0 |
| 用户二进制文件 | 66 | 0 | 0 | 0 |
| Tripwire 二进制文件 | 100 | 0 | 0 | 0 |
| * 关键配置文件 | 100 | 0 | 0 | 1 |
| 库 | 66 | 0 | 0 | 0 |
| Shell 二进制文件 | 100 | 0 | 0 | 0 |
| 文件系统和磁盘管理程序 | 100 | 0 | 0 | 0 |
| 内核管理程序 | 100 | 0 | 0 | 0 |
| 网络程序 | 100 | 0 | 0 | 0 |
| 系统管理程序 | 100 | 0 | 0 | 0 |
| 硬件和设备控制程序 | 100 | 0 | 0 | 0 |
| 系统信息程序 | 100 | 0 | 0 | 0 |
| 应用程序信息程序 | 100 | 0 | 0 | 0 |
| Shell 相关程序 | 100 | 0 | 0 | 0 |
| 关键实用符号链接 | 100 | 0 | 0 | 0 |
| 关键系统启动文件 | 100 | 0 | 0 | 0 |
| 系统启动更改 | 100 | 0 | 0 | 0 |
| OS 可执行文件和库 | 100 | 0 | 0 | 0 |
| 安全控制 | 100 | 0 | 0 | 0 |
| 登录脚本 | 100 | 0 | 0 | 0 |
| 操作系统实用程序 | 100 | 0 | 0 | 0 |
| Root 配置文件 | 100 | 0 | 0 | 0 |

```
扫描的对象总数: 14862
发现的违规总数: 2
```

存在两个违规项，它们由行左侧的 * 符号标记。第一个违规项发生在 Tripwire 数据文件规则中。报告还指出，关键配置文件规则也存在另一个违规项。在这两种情况下，都有一个文件被修改了，而这本不应该被修改。报告的“对象摘要”部分显示了以下行：

```
对象摘要:
---------------------------------------------------------------
---------------------------------------------------------------
# 部分: Unix 文件系统
---------------------------------------------------------------
---------------------------------------------------------------
---------------------------------------------------------------
规则名称: Tripwire 数据文件 (/etc/tripwire/tw.pol)
严重级别: 100
---------------------------------------------------------------
---------------------------------------------------------------
移除相邻方框中的 "x" 以防止使用此对象的新值更新数据库。
---------------------------------------------------------------
---------------------------------------------------------------
修改:
[x] "/etc/tripwire/tw.pol"
---------------------------------------------------------------
---------------------------------------------------------------
---------------------------------------------------------------
---------------------------------------------------------------
---------------------------------------------------------------
规则名称: 关键配置文件 (/etc/cron.daily)
严重级别: 100
---------------------------------------------------------------
---------------------------------------------------------------
---------------------------------------------------------------
---------------------------------------------------------------
移除相邻方框中的 "x" 以防止使用此对象的新值更新数据库。
---------------------------------------------------------------
---------------------------------------------------------------
修改:
[x] "/etc/cron.daily"
---------------------------------------------------------------
---------------------------------------------------------------
```

正如您所见，Tripwire 准确显示了哪些文件被修改以及这些文件属于哪些规则。如果这些修改是可以接受的，您可以保留报告中相应部分的 'x' 标记（表示选中）并退出编辑器。Tripwire 将会更新数据库。例如，如果您保留这两个文件的 x 标记，当下次运行完整性检查器时，它将不会发现这些违规，因为 Tripwire 数据库已经更新以纳入这些修改过的文件。然而，如果上述某个修改并非预期且看起来可疑，那么 Tripwire 就完成了它的工作！

**提示** 如果您想查看 `/var/lib/tripwire/report` 目录中的报告，您可以随时运行 `/usr/sbin/twprint -m r --twfile reportfilename` 命令。

## 以自动化方式运行 Tripwire 以检测完整性

您还可以通过创建一个小的脚本来将 Tripwire 作为 cron 任务运行，例如清单 23-7 中所示的脚本。

### 清单 23-7: /etc/cron.daily/tripwire-check

```
#!/bin/sh
HOST_NAME=`uname -n`
if [ ! -e /var/lib/tripwire/${HOST_NAME}.twd ]; then
    echo "***     错误: 未找到 $HOST_NAME 的 Tripwire 数据库。 ***"
    echo "*** 请运行 \"/etc/tripwire/twinstall.sh\" 和/或 \"tripwire --init\"。 ***"
else
    test -f /etc/tripwire/tw.cfg &&  /usr/sbin/tripwire --check
fi
```

该脚本检查 Tripwire 数据库文件是否存在；如果存在，脚本然后查找配置文件，找到后以非交互模式运行 `/usr/sbin/tripwire` 命令。这将生成一个报告文件，如果您配置了一个或多个使用 `emailto` 属性的规则，电子邮件将会发送给相应的人员。

## 更新 Tripwire 数据库

每当文件系统中发生更改，若不同步更新数据库将产生误报时，您需要更新 Tripwire 数据库。例如，如果您修改了配置文件，或移除了 Tripwire 正在为您“监控”的程序，Tripwire 将生成违规报告。因此，每当您有意更改某些内容时，必须通过重新初始化数据库（使用 `/usr/sbin/tripwire --init` 命令）或使用 `/usr/sbin/tripwire --update` 命令简单更新数据库来更新数据库。更新方法应该能为您节省一些时间，因为它不需要重新创建整个数据库。

同样，当您更改 Tripwire 策略文件 `/etc/tripwire/tw.pol` 时，需要更新数据库。再次，与其使用 `--init` 选项重新初始化整个数据库，您可以使用 `/usr/sbin/tripwire --update-policy /etc/tripwire/tw.pol` 命令指示程序应用策略更改并更新数据库。

在创建 Tripwire 数据库后，每次更新策略文件时都需要更新数据库。与其每次更改（或实验）策略文件时都重新初始化数据库，您可以运行 `tripwire --update-policy /etc/tripwire/tw.pol` 命令来更新数据库。这将节省大量时间。

## 通过电子邮件获取 Tripwire 报告

如果您在规则中使用 emailto 属性，您可以从 Tripwire 接收违规（甚至非违规）报告。如果您将 Tripwire 检查作为 cron 任务运行，这特别有用（参见本章前面“以自动化方式运行 Tripwire 以检测完整性”部分）。

在从 Tripwire 接收电子邮件之前，您必须配置 `/etc/tripwire/twcq.txt` 文件中的电子邮件设置，并使用 `/usr/sbin/twadmin --create-cfgfile /etc/tripwire/twcq.txt` 命令重建配置文件。控制电子邮件的设置在表 23-4 中有解释。

| 属性 | 含义 | |
|---|---|---|
| MAILMETHOD = SMTP \| SENDMAIL | 默认: MAILMETHOD = SENDMAIL | 此属性用于设置 Tripwire 使用的邮件传输方法。默认设置允许 Tripwire 使用 Sendmail 守护进程，这必须使用稍后讨论的 MAILPROGRAM 属性指定。由于大多数流行的 Sendmail 替代邮件守护程序（如 qmail 和 postfix）的工作方式与 Sendmail 非常相似，您仍然可以将此项设置为 SENDMAIL，并使用 MAILPROGRAM 指定您的替代守护程序的路径。然而，如果您在运行 Tripwire 程序的机器上没有运行 Sendmail 或类似 Sendmail 的守护程序，您可以将此属性设置为 SMTP，并指定 SMTPHOST 和 SMTPPORT 编号属性。假设 SMTPHOST 允许您的系统中继消息，Tripwire 将通过 SMTP 端口连接到主机并传递消息，这些消息稍后将由主机传递到适当的目的地。 |
| SMTPHOST = 主机名 \| IP 地址 | 默认: 无 | 此属性允许您指定邮件服务器的主机名。仅当在运行 Tripwire 的同一系统中没有邮件功能时才使用此属性。您可以使用 `nslookup -qmx yourdomain.in` 命令查找邮件服务器的 IP 或主机名。 |
| SMTPPORT = 端口号 | 默认: 无 | 此属性指定远程邮件服务器的 TCP 端口号。通常，应将其设置为 25。只有当您将 MAILMETHOD 设置为 SMTP 时才需要此属性。 |





| 属性 | 含义 |
| --- | --- |
| MAILPROGRAM = /path/to/mail/program | 默认：MAILPROGRAM = /usr/sbin/sendmail -oi -t |

该属性指定邮件守护进程的路径以及运行它所需提供的任何参数。只有在使用 MAILMETHOD = SENDMAIL 时，此属性才有意义。

| 属性 | 含义 |
| --- | --- |
| EMAILREPORTLEVEL = 0 - 4 | 默认：EMAILREPORTLEVEL = 3 |

该属性指定通过电子邮件报告的信息级别。请保持默认设置不变。

| 属性 | 含义 |
| --- | --- |
| MAILNOVIOLATIONS = true | false | 默认：MAILNOVIOLATIONS = true |

如果您希望在不检测到违规行为时不接收电子邮件，请将其设置为 false。

要测试您的电子邮件设置，您可以运行 Tripwire，并使用 `/usr/sbin/tripwire -m t -email your@emailaddr` 命令。别忘了将 `your@emailaddr` 更改为您自己的电子邮件地址。

## 使用 Linux 入侵检测系统 (LIDS) 保护 Apache

*Root（根用户）是所有恶意的根源。* 上述陈述可能只对全世界的 Unix/Linux 系统管理员有意义。一旦确认存在未授权的 root 访问，损害控制似乎就无望了，或者完全取决于入侵者的仁慈。

在标准的 Linux 系统中，几个子系统通常处于未受保护状态。文件系统往往像西部荒野一样开放。系统中有许多重要文件，如 `/bin/login`，因为未受保护，常被黑客利用。如果黑客入侵，他可以上传修改后的登录程序版本作为 `/bin/login`，以便未来自由访问系统。但事实是，像 `/bin/login` 这样的文件（即程序）不需要频繁变更（如果变更的话）；因此，它们绝不能处于未受保护状态。与文件系统类似，运行中的进程也未受保护。许多进程以 root 权限运行，这意味着当使用缓冲区溢出等技巧进行利用时，入侵者将获得系统的完全 root 访问权限。

降低 root 用户的权限可以增强系统安全性。LIDS 做到了这一点。实际上它还做了很多其他事情。它在内核中实现了一个非常低级别的安全模型，以提供安全防护、事件检测和事件响应功能。例如，LIDS 可以：

- 保护重要文件和目录免受未授权访问，无论它们位于哪种本地文件系统上。选定的文件和目录可以保护，防止 root 用户修改，这意味着未授权的 root 访问不会将入侵者变成我们所有人都害怕的超级大恶。
- 保护重要进程，防止任何人（包括 root 用户）终止它们。同样，这降低了 root 用户的能力。
- 防止未授权程序进行原始 I/O 操作。它还可以保护硬盘的主引导记录 (MBR)。

LIDS 可以检测某人使用端口扫描器扫描您的系统，并可通过电子邮件通知系统管理员扫描事件。LIDS 还可以在注意到任何施加规则的违规时通知系统管理员。当某人违反此类规则时，LIDS 可以在 LIDS 保护的防篡改日志文件中记录关于违规的详细消息。事实上，LIDS 不仅可以记录并发送关于检测到违规的电子邮件，它还可以立即关闭用户的交互式会话！

LIDS 是一个内核补丁和管理工具套件，从 Linux 操作系统内核内部增强安全性。因为在 LIDS 安全模型中，主体、对象和访问类型都在内核中，所以它被称为参考监视器。LIDS 项目网站是 www.lids.org/about.html。

LIDS 使 Linux 系统能够运行定制的内核，您必须从可靠的内核网站（如 www.kernel.org）获取最新的内核源代码。在下载并将内核解压到 /usr/src/linux 后，下载适用于您想要使用的特定内核的 LIDS 补丁。例如，如果您使用的是内核 2.4.1，请确保从 LIDS 项目网站下载 LIDS 补丁。通常 LIDS 补丁和管理工具包被称为 lids-x.x.x.y.y.tar.gz，其中 x.x.x 代表 LIDS 版本号，y.y.y 代表内核版本（例如，lids-1.0.5-2.4.1）。在以下说明中，我针对内核 2.4.1 使用 LIDS 1.0.5。请根据需要更改版本号。使用 tar xvfz lids-1.0.5-2.4.1.tar.gz 命令将 LIDS 源发行版解压到 /usr/local/src 目录。现在您可以准备修补内核了。

> 确保 /usr/src/linux 指向您下载的最新内核源代码发行版。您可以简单运行 ls -l /usr/src/linux 来查看符号链接指向哪个目录。如果它指向旧的内核源代码，使用 rm -f /usr/src/linux 删除链接，并使用 ln -s /usr/src/linux-version /usr/src/linux 重新链接，其中 version 是您下载的内核版本。例如，ln -s /usr/src/linux-2.4.1 /usr/src/linux 将最新的内核 2.4.1 源代码链接到 /usr/src/linux。

### 使用 LIDS 修补、编译和安装内核

要为您的系统编译 LIDS，您需要应用 LIDS 补丁后重新编译 Linux 内核。此过程描述如下：

1. 作为 root，将 LIDS 补丁包解压到您选择的合适目录。我通常将在本地编译软件的源代码放在 `/usr/local/src` 目录中。在这些步骤中，我假设您也这样做；如果不使用相同的目录，请对说明进行适当修改。因此，从 `/usr/local/src` 目录，运行 tar `xzvt lids-1.0.5-2.4.1.tar.gz` 命令。这将创建一个名为 `lids-1.0.5-2.4.1` 的新子目录。
2. 更改目录到 `/usr/src/linux`，并运行 `patch -p < /usr/local/src/lids-1.0.5-2.4.1.patch` 命令来修补内核源代码发行版。
3. 从 `/usr/src/linux` 目录运行 `make menuconfig` 命令以启动基于菜单的内核配置程序。您也可以使用 `make config` 或 `make xconfig` 命令来配置内核，但我更喜欢第一个，并假设您也使用它。
4. 从主菜单选择 Code maturity level options 子菜单，通过按空格键选择 Prompt for development and/or incomplete code/drivers 选项。退出此子菜单。
5. 转到 General setup 子菜单，选择 Sysctl support 并退出子菜单。
6. 从主菜单选择 Linux Intrusion Detection System 子菜单，只有完成第 4 步和第 5 步时才会出现此子菜单。此子菜单应列在主菜单底部，因此您可能需要向下滚动一点。
7. 从 LIDS 子菜单选择 Linux Intrusion Detection System support (EXPERIMENTAL) (NEW) 选项。您将看到如下所示的选项列表。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_719_0.png)

8. 对于受管理对象、受保护对象、ACL 主体/对象和受保护进程的默认限制，对于大多数系统应该是合适的。因此，请保持原样。
9. 如果您希望 LIDS 在用户违反安全规则时断开控制台，请选择 Hang up console when raising a security alert 选项。
10. LIDS 在启动过程中启用，因此您可能会先运行其他程序。如果您希望在 LIDS 保护启用之前执行程序时发出安全警报，请选择 Security alert when executing unprotected programs before sealing LIDS 选项。选择此选项后，您可以通过使用 Do not execute unprotected programs before sealing LIDS 选项来选择完全禁用未保护程序的执行机会。我不建议在启动期间完全禁止未保护程序，除非您绝对确定您在启动期间想要运行的所有内容（即所有工具、守护进程等）都受保护，并且不会停止正常的启动过程。
11. 启用 Try not to flood logs (NEW) 选项，并保持两个相同条目日志记录之间的默认 60 秒延迟，以维护日志文件的理智和大小。
12. （可选）如果您想允许切换 LIDS 保护，请选择 Allow switching LIDS protections 选项。如果这样做，您可以通过选择 Number of attempts to submit password、Time to wait after a fail (seconds)、Allow remote users to switch LIDS protections、Allow any program to switch LIDS protections 或 Allow reloading config. file 的值进一步自定义。我的偏好如下所示。

    - [*]  Allow switching LIDS protections (NEW)
    - (3)  Number of attempts to submit password (NEW)
    - (3)  Time to wait after a fail (seconds) (NEW)
    - [*]  Allow remote users to switch LIDS protections (NEW)
    - [ ]  Allow any program to switch LIDS protections (NEW)
    - [*]  Allow reloading config. file (NEW)

13. 您肯定要选择 Port Scanner Detector in kernel 选项，以便您可以检测潜在入侵者的端口扫描，以及 Send security alerts through network 选项。保持第二个选项的默认值不变。
14. 保存您的内核配置，并运行以下命令来编译新内核及其模块（如果有的话）。

    ```
    make depend
    make bzImage
    make modules
    make modules_install
    ```




**注意** 如果您编译的内核版本比当前系统运行的版本更新，那么您可能需要备份 `/bin/modules/current-version` 目录，其中 `current-version` 是指当前内核版本。例如，如果您正在编译版本 2.4.1，并且系统已经在运行 2.4.1，那么您应该运行 `cp -r /lib/modules/2.4.1 /lib/modules/2.4.1.bak` 命令来备份当前模块。如果新内核出现问题，您可以删除损坏内核的模块，并将该目录重命名回原始名称。

1. 现在使用 `cp /usr/src/linux/arch/i386/boot/bzImage /boot/vmlinuz-lids-1.0.5-2.4.1` 命令，将新创建的 `/usr/src/linux/arch/i386/boot/bzImage` 内核映像复制到 `/boot/vmlinuz-lids-1.0.5-2.4.1`。
2. 向 `/etc/lilo.conf` 文件添加以下内容：

   ```
   image=/boot/vmlinuz-lids-1.0.5-2.4.1
      label=lids
      read-only
      root=/dev/hda1
   ```

   如果 `/dev/hda1` 不是根设备，请确保将其更改为适当的设备。
3. 运行 `/sbin/lilo` 以重新配置 `lilo`。

内核部分的配置已完成，现在可以进行 LIDS 配置了。

## 编译、安装和配置 LIDS

要编译和安装 LIDS 管理程序 `lidsadm`，请遵循以下步骤：

1. 假设您已经将 LIDS 源代码安装在 `/usr/local/src` 目录中，请切换到 `/usr/local/src/lids-1.0.5-2.4.1/lidsadm-1.0.5`。
2. 运行 `make; make install` 命令，将 `lidsadm` 程序安装在 `/sbin` 中，并在 `/etc/lids` 中创建必要的配置文件（`lids.cap`、`lids.conf`、`lids.net`、`lids.pw`）。
3. 运行 `/sbin/lidsadm -P` 命令并为 LIDS 系统输入密码。此密码以 RIPEMD-160 加密格式存储在 `/etc/lids/lids.pw` 文件中。
4. 运行 `/sbin/lidsadm -U` 命令以更新 inode/dev 编号。
5. 配置 `/etc/lids/lids.net` 文件。以下是默认 `/etc/lids/lids.net` 文件的简化版本：

   ```
   MAIL_SWITCH= 1
   MAIL_RELAY=127.0.0.1:25
   MAIL_SOURCE=lids.sinocuster.com
   MAIL_FROM= LIDS_ALERT@lids.sinocuster.com
   MAIL_TO= root@localhost
   MAIL_SUBJECT= LIDS Alert
   ```

   - `MAIL_SWITCH` 选项可以为 1 或 0，其中 1 开启电子邮件警报功能，0 关闭该功能。请保持默认设置不变。
   - **MAIL_RELAY** 选项应设置为 LIDS 用于发送警报消息的邮件服务器的 IP 地址。如果您在配置 LIDS 的同一台机器上运行邮件服务器，请保持默认设置不变。端口号 `25` 是默认的 SMTP 端口，除非您的邮件服务器运行在其他端口上，否则请勿更改。
   - **MAIL_SOURCE** 选项应设置为正在配置的机器的主机名。将默认值更改为您系统的主机名。
   - **MAIL_FROM** 选项应设置为一个地址，用于告知警报来自哪个系统。默认值应更改以反映您系统的主机名。您不需要创建真实的邮件账号来使发件人地址生效。
   - **MAIL_TO** 选项应设置为正在配置的系统的管理员的电子邮件地址。由于 root 地址 `root@localhost` 是默认的管理员账户，您可以保持不变。
   - **MAIL_SUBJECT** 选项是显而易见的，应根据需要进行更改。
6. 要查看默认受保护的内容，运行 `/sbin/lidsadm -L` 命令，应该会显示类似以下的输出：

   LIST

   | 主题 | 访问类型 | 对象 |
   | --- | --- | --- |
   | 任何文件 | READ | /sbin |
   | 任何文件 | READ | /bin |
   | 任何文件 | READ | /boot |
   | 任何文件 | READ | /lib |
   | 任何文件 | READ | /usr |
   | 任何文件 | DENY | /etc/shadow |
   | /bin/login | READ | /etc/shadow |
   | /bin/su | READ | /etc/shadow |
   | 任何文件 | APPEND | /var/log |
   | 任何文件 | WRITE | /var/log/wtmp |
   | /sbin/fsck.ext2 | WRITE | /etc/mtab |
   | 任何文件 | WRITE | /etc/mtab |
   | 任何文件 | WRITE | /etc |
   | /usr/sbin/sendmail | WRITE | /var/log/sendmail.st |
   | /bin/login | WRITE | /var/log/lastlog |
   | /bin/cat | READ | /home/xhg |
   | 任何文件 | DENY | /home/httpd |
   | /usr/sbin/httpd | READ | /home/httpd |
   | 任何文件 | DENY | /etc/httpd/conf |
   | /usr/sbin/httpd | READ | /etc/httpd/conf |
   | /usr/sbin/sendmail | WRITE | |
   | /usr/X11R6/bin/XF86_SVG | NO_INHERIT | RAMID |
   | /usr/sbin/in.ftpd | READ | /etc/shadow |
   | /usr/sbin/httpd | NO_INHERIT | HIDDEN |

   因为您不太可能拥有 `/home/xhg`（LIDS 作者的 home 目录），您可以通过使用以下命令移除其配置：

   ```
   /sbin/lidsadm -D -s /bin/cat -o /home/xhg
   ```

   您可以保持其他所有内容不变，因为稍后可以按需更改它们。
7. 在 `/etc/rc.d/rc.local` 文件中添加以下行，以在启动周期结束时封印内核：

   ```
   /sbin/lidsadm -I
   ```
8. 重启系统，并在 `lilo` 提示符下输入 `lids` 选择 LIDS 启用内核。当系统启动并运行 `/etc/rc.d/rc.local` 脚本中的 `/sbin/lidsadm -I` 命令时，它将封印内核，并且系统将由 LIDS 保护。

## 管理 LIDS

除了 `/etc/lids/lids.net` 文件外，您必须使用 `/sbin/lidsadm` 程序来修改 LIDS 配置文件 `/etc/lids/lids.conf`、`/etc/lids/lids.pw` 和 `/etc/lids/lids.cap`。

`/etc/lids/lids.conf` 文件存储访问控制列表 (ACL) 信息。`/etc/lids/lids.cap` 文件包含系统的所有能力规则。您可以通过使用 `/sbin/lidsadm` 命令编辑此文件来配置要在系统上启用或禁用的能力。您只需在能力名称前设置 **+** 来启用系统，或设置 **−** 来禁用该能力。

`/etc/lids/lids.net` 文件配置发送警报电子邮件所需的邮件设置。您可以使用 vi、emacs 或 pico 等常规编辑器来编辑此文件。

如果您需要停止 LIDS 以执行系统管理任务，则应使用 `/sbin/lidsadm -S -- -LIDS` 或 `/sbin/lidsadm -S -- -LIDS_GLOBAL` 命令。您还需要提供 LIDS 密码来关闭 LIDS。在使用 `lidsadm` 命令对 LIDS 配置文件进行任何更改后，通过运行 `/sbin/lidsadm -S -- + RELOAD_CONF` 命令将更新的配置重新加载到内核中。

要向 `/etc/lids/lids.conf` 文件添加新的 ACL，您按如下方式使用 `/sbin/lidsadm` 命令：

```
/sbin/lidsadm -A [-s subject] [-t | -d | -i] -o object -j TARGET
```

上述命令中的选项在以下列表中解释：

- **-A** 选项告知 `/sbin/lidsadm` 程序添加新的 ACL。
- **-s _subject_** 选项指定 ACL 的主题。主题可以是任何程序，例如 `/bin/cat`。当不指定主题时，ACL 将适用于所有内容。
- **-t**、**-d**、**-i** 选项通常不需要。
- **-o _object_** 选项用于指定对象的名称，可以是文件、目录或能力。每个 ACL 都需要一个命名的对象。
- **-j TARGET** 选项指定 ACL 的目标。当新 ACL 的对象是文件或目录时，目标可以是 **READ, WRITE, APPEND, DENY, 和 IGNORE**。如果对象是 Linux 能力，则目标只能是 **INHERIT 或 NO_INHERIT**，这定义了对象的子进程是否具有相同的能力。

## 保护文件和目录

您可以使用 **lidsadm** 来保护重要文件和目录。您可以使文件或目录只读，控制写访问，控制追加模式文件访问，并拒绝访问。LIDS 为文件或目录提供以下类型的保护：

- **READ**——使文件或目录只读
- **WRITE**——允许修改文件或目录
- **IGNORE**——忽略为文件或目录设置的所有其他保护
- **APPEND**——允许向文件添加内容
- **DENY**——拒绝访问文件或目录的所有权限

## 使文件或目录只读

要使名为 `/path/filename` 的文件只读，请运行：

```
sbin/lids -A -o /path/filename -j READ
```

要使名为 `/my/path` 的目录只读，请运行：

```
sbin/lids -A -o /my/path -j READ
```

请注意，由于您在上述任何命令中都没有指定主题，ACL 适用于所有程序。因此，没有程序可以写入上述文件或目录。如果您指定了主题，则该命令仅适用于指定的文件或目录。

## 拒绝访问文件或目录

要拒绝访问名为 `/etc/shadow` 的文件，请运行：

```
sbin/lids -A -o /etc/shadow -j DENY
```

运行上述命令并重新加载 LIDS 配置后，您可以运行诸如 `ls -l /etc/shadow` 和 `cat /etc/shadow` 等命令，以查看是否可以访问该文件。由于您隐含指定主题为系统内的所有程序，因此这些程序都将无法看到该文件。但是，如果您需要允许诸如 `/bin/login` 之类的程序访问 `/etc/shadow` 文件，您可以通过创建新的 ACL 来赋予其读取权限，例如：

```
sbin/lids -A -s /bin/login -o /etc/shadow -j READ
```




## 允许追加访问

通常，程序只需要对诸如 /var/log/messages 或 /var/log/secure 等关键系统日志进行追加访问。您可以使用以下命令为这两个文件启用追加模式：

```
/sbin/lids -A -o /var/log/messages -j APPEND
/sbin/lids -A -o /var/log/secure -j APPEND
```

## 允许仅写访问

若要允许名为 /usr/local/apache/bin/httpd 的程序能够向名为 /home/httpd 的保护目录写入数据，请运行以下命令：

```
/sbin/lids -A -o /home/httpd -j DENY
/sbin/lids -A -s /usr/local/apache/bin/httpd -o /home/httpd -j READ
```

## 删除 ACL

若要删除所有 ACL 规则，请运行 /sbin/lidsadm -Z 命令。若要删除单独的 ACL 规则，只需指定该 ACL 的主体（如果有）和/或对象。例如，如果您运行 /sbin/lidsadm -D -o /bin 命令，则以 /bin 为对象的所有 ACL 规则都会被删除。但是，如果您运行 /sbin/lidsadm -D -s /bin/login -o /bin 命令，则只有指定 /bin/login 为主体且 /bin 为对象的 ACL 会被删除。

> **注意** 不带任何参数指定 -Z 或 -D 选项会删除您所有的 ACL 规则。

## 一种良好的文件和目录保护方案

在本节中，我将向您展示一种您可以与 LIDS 配合使用的良好保护方案。该方案允许您将 /boot 目录（或分区）设为只读，这意味着内核不能被入侵者修改；它还将系统库目录 /lib、root 用户的家庭目录 /root、系统配置目录 /etc、系统守护程序二进制文件目录 /sbin 和 /usr/sbin，以及标准二进制文件目录 /usr/bin 和 /bin 设为只读。它还仅允许对 /var/log 目录中的文件进行追加操作，从而确保日志文件不会被任何入侵者破坏。该配置如下所示：

```
# 将 /boot 目录或分区设为只读
/sbin/lidsadm -A -o /boot -j READ

# 将系统库目录设为只读
# 这也保护了 lib/modules
/sbin/lidsadm -A -o /lib -j READ

# 将 root 用户的家庭目录设为只读
/sbin/lidsadm -A -o /root -j READ

# 将系统配置目录设为只读
/sbin/lidsadm -A -o /etc -j READ

# 将守护程序二进制文件目录设为只读
/sbin/lidsadm -A -o /sbin -j READ

# 将其他守护程序二进制文件目录设为只读
/sbin/lidsadm -A -o /usr/sbin -j READ

# 将通用二进制文件目录设为只读
/sbin/lidsadm -A -o /bin -j READ

# 将其他通用二进制文件目录设为只读
/sbin/lidsadm -A -o /usr/bin -j READ

# 将通用库目录设为只读
/sbin/lidsadm -A -o /lib -j READ

# 将系统日志目录设为追加模式
/sbin/lidsadm -A -o /var/log -j APPEND

# 将 X Windows 二进制文件目录设为只读
/sbin/lidsadm -A -o /usr/X11R6/bin -j READ
```

除了使用上述技术保护您的文件和目录外，LIDS 还可以使用 Linux Capabilities（能力）来限制正在运行的程序（即进程）的能力。在传统的 Linux 系统中，root 用户（即 UID 和 GID 设置为 0 的用户）拥有所有的“能力”或执行任何任务（通过运行任何进程）的能力。LIDS 使用 Linux Capabilities 将 root 的所有权力（或由 root 用户运行的进程）分解为碎片，以便您可以精确调整特定进程能做或不能做什么。要了解可用的 Linux Capabilities，请参见 /usr/include/linux/capability.h 头文件。表 23-5 列出了所有 Linux Capabilities 及其在默认 LIDS Capabilities 配置文件 /etc/lids/lids.cap 中的状态（开启或关闭）。

| Capability ID | Capability Name | Meaning | Status in /etc/lids/lids.cap |
| :-- | :-- | :-- | :-- |
| 0 | CAP_CHOWN | 允许/禁止更改文件所有权 | 允许 |
| 1 | CAP_DAC_OVERRIDE | 允许/禁止覆盖所有 DAC 访问限制 | 允许 |
| 2 | CAP_DAC_READ_SEARCH | 允许/禁止覆盖所有有关读取和搜索的 DAC 限制 | 允许 |
| 3 | CAP_FOWNER | 允许/禁止以下限制：在文件中设置 `S_ISUID` 和 `S_ISGID` 位时，有效用户 ID 必须与文件所有者 ID 匹配；在文件中设置该位时，有效组 ID 必须与文件所有者 ID 匹配 | 允许 |
| 4 | CAP_FSETID | 允许/禁止在有效用户 ID 不等于所有者 ID 时访问 | 允许 |
| 5 | CAP_KILL | 允许/禁止向属于其他用户的进程发送信号 | 允许 |
| 6 | CAP_SETGID | 允许/禁止更改 GID | 允许 |
| 7 | CAP_SETUID | 允许/禁止更改 UID | 允许 |
| 8 | CAP_SETPCAP | 允许/禁止将当前集合的转移和移除给任何 PID | 允许 |
| 9 | CAP_LINUX_IMMUTABLE | 允许/禁止修改不可变文件和追加文件 | 禁止 |
| 10 | CAP_NET_BIND_SERVICE | 允许/禁止绑定到 1024 以下的端口 | 禁止 |
| 11 | CAP_NET_BROADCAST | 允许/禁止广播/监听组播 | 允许 |
| 12 | CAP_NET_ADMIN | 允许/禁止网络管理以执行接口配置、管理 IP 防火墙、设置伪装、设置 IP 记账、在套接字上设置调试选项、修改路由表、在套接字上设置任意进程/进程组所有权、为透明代理绑定任何地址、设置服务类型 (TOS)、设置混杂模式等 | 禁止 |
| 13 | CAP_NET_RAW | 允许/禁止使用原始套接字 | 禁止 |
| 14 | CAP_IPC_LOCK | 允许/禁止锁定共享内存段 | 允许 |
| 15 | CAP_IPC_OWNER | 允许/禁止 IPC 所有权检查 | 允许 |
| 16 | CAP_SYS_MODULE | 允许/禁止插入和移除内核模块 | 禁止 |
| 17 | CAP_SYS_RAWIO | 允许 ioperm(2)/fiopl(2) 访问 CAP_SYS_CHROOT chroot(2) | 禁止 |
| 18 | CAP_SYS_CHROOT | 允许/禁止 chroot 系统调用 | 禁止 |
| 19 | CAP_SYS_PTRACE | 允许/禁止 ptrace | 允许 |
| 20 | CAP_SYS_PACCT | 允许/禁止配置进程记账 | 允许 |
| 21 | CAP_SYS_ADMIN | 允许/禁止各种系统管理任务 | 允许 |
| 22 | CAP_SYS_BOOT | 允许/禁止重新启动 | 允许 |
| 23 | CAP_SYS_NICE | 允许/禁止使用 *nice* 命令更改进程优先级 | 允许 |
| 24 | CAP_SYS_RESOURCE | 允许/禁止设置系统资源限制 | 允许 |
| 25 | CAP_SYS_TIME | 允许/禁止设置系统时间 | 允许 |
| 26 | CAP_SYS_TTY_CONFIG | 允许/禁止伪终端 (TTY) 配置 | 允许 |
| 27 | CAP_MKNOD | 允许/禁止 *mknod*() 系统调用的特权方面 | 允许 |
| 28 | CAP_LEASE | 允许/禁止获取文件租约 | 允许 |
| 29 | CAP_HIDDEN | 允许/禁止将进程对系统的其余部分隐藏 | 允许 |
| 30 | CAP_INIT_KILL | 允许/禁止程序终止 *init* 进程（PID = 1）的子进程的能力 | 允许 |

上述 Linux Capabilities 的默认设置存储在 */etc/lids/lids.cap* 文件中，如列表 23-8 所示。

### 列表 23-8: */etc/lids/lids.cap*

```
+0:CAP_CHOWN
+1:CAP_DAC_OVERRIDE
+2:CAP_DAC_READ_SEARCH
+3:CAP_FOWNER
+4:CAP_FSETID
+5:CAP_KILL
+6:CAP_SETGID
+7:CAP_SETUID
+8:CAP_SETPCAP
-9:CAP_LINUX_IMMUTABLE
-10:CAP_NET_BIND_SERVICE
+11:CAP_NET_BROADCAST
-12:CAP_NET_ADMIN
-13:CAP_NET_RAW
+14:CAP_IPC_LOCK
+15:CAP_IPC_OWNER
-16:CAP_SYS_MODULE
-17:CAP_SYS_RAWIO
-18:CAP_SYS_CHROOT
+19:CAP_SYS_PTRACE
+20:CAP_SYS_PACCT
-21:CAP_SYS_ADMIN
+22:CAP_SYS_BOOT
+23:CAP_SYS_NICE
+24:CAP_SYS_RESOURCE
+25:CAP_SYS_TIME
+26:CAP_SYS_TTY_CONFIG
+27:CAP_MKNOD
+28:CAP_LEASE
+29:CAP_HIDDEN
+30:CAP_INIT_KILL
```

加号 (+) 启用该能力，减号 (-) 禁用该能力。例如，在上述列表中，最后一个名为 `CAP_INIT_KILL` 的 Linux Capability 是启用的，这意味着由 root 拥有的进程可以终止由 `init` 进程创建的任何子进程（通常是守护程序）。您可以使用文本编辑器来启用或禁用 Linux Capabilities。

## 通过使用 LIDS 管理的 Linux Capabilities 保护您的系统

您可以使用 LIDS 提供的能力来保护您的系统。在本节中，我将向您展示如何利用由 LIDS 管理的 Linux Capabilities。您将了解如何保护守护程序（例如 Apache Web 服务器）不被 root 用户终止，如何从 `ps` 等程序中隐藏进程，如何禁用对设备的原始访问，以及如何保护 ext2 不可变标志。

## 保护守护程序不被 root 终止

通常，守护进程（例如 Sendmail 邮件传输代理和 Apache Web 服务器）是由 `init` 进程启动的。如果您希望保护它们不被 root 用户终止，请将 `/etc/lids/lids.cap` 中的 `CAP_INIT_KILL` 设置修改为：

```
-30:CAP_INIT_KILL
```




重载 LIDS 配置（使用 `/sbin/lidsadm -S - + RELOAD_CONF` 命令）或重启系统并密封内核（在 `/etc/rc.d/rc.local` 脚本中使用 `/sbin/lidsadm -i` 命令）之后，你（作为 root）将无法终止 init 的子进程。这确保了即使系统被入侵且入侵者获得了 root 权限，入侵者也无法终止守护进程并用特洛伊木马版本替换它们。

## 向所有人隐藏进程

默认情况下，`CAP_HIDDEN` 能力在 `/etc/lids/lids.cap` 配置文件中是开启的。你可以使用以下命令将进程对所有人隐藏：

```
lidsadm -A -s /path/to/binary -t -o CAP_HIDDEN -j INHERIT
```

其中 `/path/to/binary` 是你希望隐藏时运行的可执行文件的完全限定路径。例如，要隐藏正在运行的 Apache 服务器进程 `/usr/local/apache/bin/httpd`，只需运行以下命令：

```
lidsadm -A -s /usr/local/apache/bin/httpd -t -o CAP_HIDDEN -j INHERIT
```

这将把进程标记为内核中的隐藏状态，无法使用任何用户空间工具（如 `ps` 或 `top`）找到它，甚至无法通过探索 `/proc` 文件系统中的文件来发现它。

## 禁用进程对原始设备的访问

通常，只有特殊进程才需要访问原始设备。因此，禁用对原始设备的访问并在需要时启用它们是个好主意，这符合“全部关闭，仅开放所需”的整体安全概念。

原始设备访问由 `CAP_SYS_RAWIO` 能力控制，该能力在 `/etc/lids/lids.cap` 配置文件中默认是禁用的。如果启用了它，进程就可以访问 `/dev/mem`、`/dev/port`、`/dev/mem`、`/dev/kmem` 以及其他原始块设备。例如，当此能力关闭时（如默认情况），`/sbin/lilo` 程序无法正常工作，因为它需要对硬盘进行原始设备级别的访问。

但是一些特殊程序，如 `XF86_SVGA`，可能需要此能力才能正常运行。在这种情况下，你可以按如下方式将该程序添加到例外列表中：

```
lidsadm -A -s /usr/X11R6/bin/XF86_SVGA -t -o CAP_SYS_RAWIO -j INHERIT
```

### 禁用网络管理任务

默认情况下，`CAP_NET_ADMIN` 能力是关闭的，这意味着网络管理员（通常是 root 用户）无法再执行以下网络管理任务：

- 配置以太网接口
- 管理 IP 防火墙、伪装（masquerading）和会计
- 设置套接字的调试选项
- 修改路由表
- 在套接字上设置任意的进程/进程组所有权
- 绑定到任何地址以进行透明代理
- 设置服务类型 (TOS)
- 设置混杂模式
- 清除驱动程序统计信息
- 组播
- 设置特定设备寄存器的读写

强烈建议保持默认设置。如果你确实需要执行上述任一任务，只需使用 `/sbin/lidsadm -S -- -LIDS` 命令临时关闭 LIDS 即可。

### 保护文件的 Linux 不可变标志

ext2 文件系统具有一个扩展功能，允许你将文件标记为不可变。这是通过 `chattr` 命令完成的。例如，`chattr +i /path/to/myfile` 会将 `/path/to/myfile` 变为不可变文件。具有不可变属性的文件不能被修改、删除或重命名，也不能创建符号链接。然而，root 用户可以使用 `chattr -i /path/to/myfile` 命令来更改该标志。你可以通过禁用 `CAP_LINUX_IMMUTABLE` 能力来保护不可变文件，使其即使对超级用户（root）也安全。请注意，`CAP_LINUX_IMMUTABLE` 在 `/etc/lids/lids.cap` 中默认是禁用的。

### 检测扫描器

如果你按照前面讨论的 LIDS 安装部分中的建议，在内核编译时启用了内置端口扫描器，就可以检测端口扫描器。该扫描器可以检测半开放扫描、SYN 隐蔽端口扫描、Stealth FIN、Xmas 或 Null 扫描等。诸如 `nmap` 和 Satan 或 Scan 等工具可以被检测器检测到。当原始套接字（`CAP_NET_RAW`）被禁用时，这是很有用的。

> **注意**
> 当 `CAP_NET_RAW` 关闭时，一些基于嗅探的用户空间扫描器将无法正常工作。但 LIDS 提供的基于内核的扫描器不使用任何套接字，这使其更加安全。你可能需要考虑使用 LIDS 提供的扫描器。

## 对入侵者的响应

当 LIDS 检测到任何 ACL 规则违规时，可以通过以下方法对该行为做出响应。

- **记录消息。** 当有人违反 ACL 规则时，LIDS 将使用内核日志守护程序 (klogd) 记录一条消息。
- **向适当的权限发送电子邮件。** 当发生违规时，LIDS 可以发送电子邮件。此功能由 `/etc/lids/lids.net` 文件控制，该文件在本章前面“编译、安装和配置 LIDS”部分的第 5 步中进行了讨论。
- **挂起控制台。** 如果你按照 LIDS 安装部分第 9 步中讨论的内容，在 LIDS 的内核补丁应用中启用了此选项，当用户违反 ACL 规则时，控制台将被断开。

LIDS 的另一个类似系统是 OpenWall 项目 (www.openwall.com/linux)。OpenWall 项目包含一些与 LIDS 中找到的不同的安全特性，其中一个特定的 OpenWall 补丁使进程的堆栈区域不可执行。你应该看看这个正在进行中的项目。

# HTTP 1.1 状态代码

对于来自 Web 客户端的每个请求，Web 服务器必须向客户端返回一个 HTTP 状态代码，由三位数字组成。Web 客户端可以通过查看 HTTP 状态行（Status-Line）头部中发送的此状态代码来尝试理解服务器的响应。代码附带一个简短的短语，称为*原因短语*，旨在为用户提供简要解释。例如，HTTP 状态行头部可能如下所示：

```
HTTP/1.1 404 Not Found
```

在这里，**404** 是状态代码，**Not Found** 是原因短语。在典型的 Web 客户端上，Web 浏览器将在浏览器窗口中显示 Not Found 短语。最新的 HTTP 1.1 规范提供了五种不同类别的状态代码；这些类别在以下部分中进行讨论。

## 信息性状态代码 (100–199)

这种类型状态代码的目的是让客户端知道服务器正在处理请求。这些状态代码仅是信息性的；客户端无需对其中任何一项采取行动。请注意，HTTP 1.0 未定义 1xx 状态代码，因此不得向 HTTP 1.0 客户端发送 1xx 状态代码。当前定义的 1xx 状态代码如下：

- **100 Continue** — 服务器发送此代码以告知客户端它已准备好接收请求的其余部分。
- **101 Switching Protocol** — 当服务器愿意将应用协议切换为客户端提供的 Upgrade 请求头部中指定的协议时，服务器会发送此代码。仅当新协议比现有协议具有优势时才应进行切换。例如，客户端可能请求服务器使用比当前正在使用的新版 HTTP 协议。在这种情况下，服务器应尽可能进行切换。

## 客户端请求成功 (200–299)

返回的 200–299 范围内的状态代码表示客户端的请求已被成功接收和接受。当前定义的 2xx 状态代码如下：

- **200 OK** — 服务器成功处理了请求，且请求的文档已附带。
- **201 Created** — 服务器成功创建了一个新的 URL，该 URL 在 Location 头部中指定。
- **202 Accepted** — 请求已被接受处理，但服务器尚未完成处理。
- **203 Non-Authoritative Information** — 响应头部中的元信息并非源自服务器；它是从另一台服务器复制的。
- **204 No Content** — 请求已完成，但无需发送新信息。客户端应继续显示当前文档。
- **205 Reset Content** — 客户端应重置当前文档。当 HTML 表单需要重置以清除所有输入字段的现有值时，这非常有用。
- **206 Partial Content** — 服务器已满足对资源的分部分 GET 请求。此代码用于响应 Range 请求。服务器发送 Content-Range 头部以指示附带的数据段。

## 请求重定向 (300–399)

300–399 范围内的状态代码被发送给客户端，以告知其需要执行进一步的操作来完成请求。当前定义的 3xx 状态代码如下：

- **300 Multiple Choices** — 请求的资源对应于一组文档。服务器可以发送关于每个文档的信息，包括其特定位置和内容协商信息，以便客户端可以选择其中一个。
- **301 Moved Permanently** — 请求的资源在服务器上不存在。发送 Location 头部将客户端重定向到新 URL。客户端将所有未来的请求指向新 URL。




302 临时移动——请求的资源已临时移动。服务器发送 Location 头，将客户端重定向到新 URL。客户端在后续请求中继续使用旧的 URI。

303 查看其他位置——请求的资源位于由 Location 头指示的其他位置，客户端应使用 GET 方法获取该资源。

304 未修改——服务器使用此代码响应 If-Modified-Since 请求头。这表明自指定日期以来，请求的文档未被修改，客户端应使用其缓存副本。

305 使用代理——客户端应使用由 Location 头指定的代理来获取请求的资源。

307 临时重定向——请求的资源被临时重定向到其他位置。服务器发送 Location 头，将客户端重定向到新 URL。客户端在后续请求中继续使用旧的 URI。

## 客户端请求不完整（400–499）

400–499 范围内的状态码用于指示客户端请求不完整，需要更多信息来完成资源请求。当前定义的 4xx 状态码如下：

400 坏请求——服务器检测到客户端请求中存在语法错误。

401 未授权——请求需要用户身份验证。服务器发送 WWW-Authenticate 头，以指示请求资源的身份验证类型和域。

402 需要支付——此代码保留供将来使用。

403 禁止访问——禁止访问请求的资源。客户端不应重复该请求。

404 未找到——请求的文档在服务器上不存在。

405 方法不被允许——客户端使用的请求方法不可接受。服务器发送 Allow 头，说明访问请求资源时可接受的方法。

406 不可接受——根据服务器接收到的 Accept 头，请求的资源不可用客户端可接受的格式。如果请求不是 HEAD 请求，服务器可以发送 Content-Language、Content-Encoding 和 Content-Type 头，以指示可用的格式。

407 需要代理身份验证——对代理服务器的未授权访问请求。客户端必须首先与代理进行身份验证。服务器发送 Proxy-Authenticate 头，指示请求资源的身份验证方案和域。

408 请求超时——客户端未能在服务器使用的请求超时时间内完成其请求。但是，客户端可以重复该请求。

409 冲突——客户端请求与其他请求发生冲突。服务器可以随状态码添加有关冲突类型的信息。

410 永久消失——请求的资源已从服务器永久删除。

411 需要长度——客户端必须在请求中提供 Content-Length 头。

412 前置条件失败——当客户端发送带有 个或多个 If... 头的请求时，如果这些头中指定的条件中有一个或多个为假，服务器使用此代码进行指示。

413 请求实体过大——由于消息体过大，服务器拒绝处理该请求。服务器可以关闭连接，以阻止客户端继续发送请求。

414 请求 URI 过长——由于指定的 URI 过长，服务器拒绝处理该请求。

415 不支持的媒体类型——由于不支持消息体的格式，服务器拒绝处理该请求。

417 期望失败——服务器未能满足 Expect 请求头的要求。

## 服务器错误（500-599）

当服务器遇到错误且无法处理请求时，会返回 500-599 范围内的状态码。当前定义的 5xx 状态码如下：

- 500 内部服务器错误 — 服务器配置设置或外部程序导致错误。
- 501 未实现 — 服务器不支持处理请求所需的功能。
- 502 错误网关 — 服务器从上游服务器或代理接收到了无效响应。
- 503 服务不可用 — 服务暂时不可用。服务器可以发送 Retry-After 头，以指示服务何时可能再次可用。
- 504 网关超时 — 网关或代理已超时。
- 505 HTTP 版本不受支持 — 客户端使用的 HTTP 版本不受支持。

# 附录 B
# 理解正则表达式

![](img/e11fcbd2818a3495ac70085e5d8d1c26_739_0.png)

![](img/e11fcbd2818a3495ac70085e5d8d1c26_739_1.png)

*正则表达式*通常由普通字符和特殊字符组成，以创建模式。该模式用于匹配一个或多个子字符串，或匹配整个字符串。例如：

```
([a-z]+)\.([a-z])\.([a-z])+
```

这是一个匹配 `www.idgbooks.com`、`www.apache.org` 等的正则表达式。正则表达式中使用的特殊字符通常称为元字符。表 B-1 展示了常用的元字符。

| 元字符 | 用途 |
| :--- | :--- |
| . | 匹配任何字符（换行符除外） |
| ^ | 匹配字符串的开头 |
| $ | 匹配字符串的结尾 |
| \b | 匹配单词边界 |
| x? | 匹配 0 或 1 个 x，其中 x 是任何正则表达式 |
| x* | 匹配 0 个或多个 x |
| x+ | 匹配 1 个或多个 x |
| foo\|bar | 匹配 foo 或 bar 之一 |
| [abc] | 匹配集合 abc 中的任意字符 |
| [A-Z] | 匹配范围 A 到 Z 中的任意字符。 |
| [^xyz] | 匹配集合 xyz 中不存在的任意单个字符 |
| \w | 匹配字母数字字符（例如 [a-zA-Z0-9_]） |
| \s | 匹配空白字符 |
| \t | Tab 字符 |
| \n | 换行字符 |
| \r | 回车字符 |
| \f | 换页字符 |
| \v | 垂直制表符 |
| \a | 响铃字符 |
| \e | 转义字符 |
| \077 | 八进制字符 |
| \x9f | 十六进制字符 |
| \c[ | 控制字符 |
| \l | 下一个字符转为小写 |
| \L | 转换为小写，直到 \E |
| \U | 转换为大写，直到 \E |
| \E | 结束大小写修改 |
| \Q | 保留元字符，直到 \E |
| \u | 下一个字符转为大写 |

*注：原始 OCR 表格中“元字符”存在重复列和错误标记的行（例如，\Q 被标记为“下一个字符转为大写”，而 \u 在某些上下文或标准中被标记为“保留元字符直到 \E”，反之亦然。标准的 Perl/PCRE 行为是 \u 表示下一个字符转为大写，\Q 表示保留直到 \E。OCR 文本中的描述可能互换或有误。此处将“modifification”更正为“modification”，并按要求将表格结构清理为单列。*

| 元字符 | 用途 |
| :--- | :--- |
| . | 匹配任何字符（换行符除外） |
| ^ | 匹配字符串的开头 |
| $ | 匹配字符串的结尾 |
| \b | 匹配单词边界 |
| x? | 匹配 0 或 1 个 x，其中 x 是任何正则表达式 |
| x* | 匹配 0 个或多个 x |
| x+ | 匹配 1 个或多个 x |
| foo\|bar | 匹配 foo 或 bar 之一 |
| [abc] | 匹配集合 abc 中的任意字符 |
| [A-Z] | 匹配范围 A 到 Z 中的任意字符。 |
| [^xyz] | 匹配集合 xyz 中不存在的任意单个字符 |
| \w | 匹配字母数字字符（例如 [a-zA-Z0-9_]） |
| \s | 匹配空白字符 |
| \t | Tab 字符 |
| \n | 换行字符 |
| \r | 回车字符 |
| \f | 换页字符 |
| \v | 垂直制表符 |
| \a | 响铃字符 |
| \e | 转义字符 |
| \077 | 八进制字符 |
| \x9f | 十六进制字符 |
| \c[ | 控制字符 |
| \l | 下一个字符转为小写 |
| \L | 转换为小写，直到 \E |
| \U | 转换为大写，直到 \E |
| \E | 结束大小写修改 |
| \Q | 保留元字符，直到 \E |
| \u | 下一个字符转为大写 |

如果需要在正则表达式中将元字符作为普通字符使用，可以使用 \metachar 格式来取消特殊含义。一个例子是 \$，它是一个普通的美元符号字符。表 B-2 展示了正则表达式中使用的标准量词。

| 量词 | 含义 |
| :--- | :--- |
| * | 匹配 0 次或多次 |
| + | 匹配 1 次或多次 |
| ? | 匹配 1 次或 0 次 |
| {n} | 恰好匹配 $n$ 次 |
| {n,} | 至少匹配 $n$ 次 |
| {n, m} | 至少匹配 $n$ 次但不超过 $m$ 次 |

\| 字符被视为 OR（或）运算符。一对圆括号 () 允许您定义正则表达式中用于搜索匹配字符串的区域。一对方括号 [ ] 创建字符类或范围。

让我们重新审视第一个例子：

```
(([a-z])+)\.([a-z])+\.([a-z])+
```

如前所述，该表达式可用于匹配诸如 `www.hungryminds.com` 之类的字符串。第一个 `[a-z]+` 指定需要匹配 a 到 z 范围内的一个或多个字符，以匹配由第一对圆括号指定的组。如果找到匹配项，可以使用 $1 访问匹配到的内容。该表达式中有三对圆括号。第一对（从左开始）是 $1，第二对是 $2，第三对是 $3。请注意，使用 \ 来转义组之间的点 (.) 元字符。

这里还有两个例子：

- `^foo\.htm$`—这将匹配字符串 `foo.htm`。它不会匹配 `afoo.htm`，因为使用了 `^` 元字符来指定匹配字符串必须以字符 f 开头。它也不会匹配 `foo.html`，因为使用了 $ 元字符来指定匹配字符串必须以字符 m 结尾。




`^www\.([^\.]+)\.host\.`\com(.*)` — **这将匹配一个字符串，例如 `www.username.host.com STATUS=java`，并且 **$1** 将被赋给 host，而 **$2** 将包含 `www.username.host.com` 部分之后的所有内容。 **$2** 将包含 `STATUS=java`。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_742_0.png)

![](img/e11fcbd2818a3495ac70085e5d8d1c26_742_1.png)

![](img/e11fcbd2818a3495ac70085e5d8d1c26_742_2.png)

# 在线 Apache 资源

本附录列出了与 Apache 相关且您可能觉得有用的网站、Usenet 新闻组以及邮件列表地址。

## 免费资源

与 Apache 一样，许多最好的 Apache 资源都在互联网上免费获得。以下部分介绍了其中一些免费的 Apache 互联网资源。

### 网站

以下是一些较好的 Apache 网站：

- 官方 Apache 网站 — www.apache.org
- Apache 模块注册中心 — http://modules.apache.org
- Apache/Perl 集成项目 — http://perl.apache.org
- Apache-SSL — www.apache-ssl.org
- Jakarta 项目 — http://jakarta.apache.org
- Apache GUI 项目 — http://gui.apache.org
- Apache Today — www.apachetoday.com
- Apache Week — www.apacheweek.com

## Usenet 新闻组

Usenet 新闻组是任何人都可以从中学习世界各地人士的个人经验和专业知识的一流资源。当您在 Apache、CGI 脚本或 Java Servlet 遇到问题时，很有可能某人也遇到了同样的问题。在 Usenet 中搜索答案是大多数成功的系统管理员常见的研究过程。如果您通过 ISP 可以访问 Usenet 服务器，那么您就可以访问和发布到任何公共新闻组。

如果您无法通过 ISP 访问 Usenet，您始终可以使用 `http://groups.google.com` 上的 Google Groups。Google Groups 允许您浏览所有 Usenet 新闻组并参与发帖。如果您希望执行复杂搜索，可以使用 `http://groups.google.com/advanced_group_search`。

避免通过发布诸如“IE 比 Netscape Navigator 好吗？”这样的问题来制造不必要的争论（称为 *flame wars*），因为不同的人有不同的个人偏好，这些偏好往往会阻碍对此类主题的客观分析。提出建设性的问题，并且如果您能回答，请不要忘记回复。

## Web 服务器相关新闻组

这些新闻组是关于各种 Web 服务器的信息的良好来源。您可以在*这里合适的平台特定组*中提出关于 Apache 的问题或关注讨论。例如，如果您运行的是 Windows 版本的 Apache，那么您可以在 `comp.infosystems.www.servers.ms-windows` 组中提出问题。

**comp.infosystems.www.servers.mac**

该新闻组讨论 Macintosh (MacOS) 平台的 Web 服务器。主题包括配置问题/解决方案、安全问题、目录结构和错误报告。

**comp.infosystems.www.servers.misc**

该新闻组讨论其他平台的 Web 服务器，如 Amiga 和 VMS，以及其他平台。主题包括配置问题/解决方案、安全问题、目录结构和错误报告。

**comp.infosystems.www.servers.ms-windows**

该新闻组涵盖 MS Windows 和 NT 平台的 Web 服务器。主题包括配置问题/解决方案、安全问题、目录结构和错误报告。

**comp.infosystems.www.servers.unix**

该新闻组讨论 UNIX 平台的 Web 服务器。主题包括配置问题/解决方案、安全问题、目录结构和错误报告。

## 编写相关新闻组

此类新闻组涉及 Web 内容创作工具和技术。您可以提出关于 CGI 编程、HTML 标签、图像等的问题，或关注讨论。

**comp.infosystems.www.authoring.cgi**

该新闻组讨论通用网关接口 (CGI) 脚本的开发及其与网页编写的关系。主题包括如何处理表单结果、如何即时生成图像以及如何组装其他交互式 Web 提供物。

**comp.infosystems.www.authoring.html**

该新闻组讨论超文本标记语言 (HTML) 及其与网页编写的关系。主题包括 HTML 编辑器、格式化技巧以及当前和提议的 HTML 标准。

**comp.infosystems.www.authoring.images**

该新闻组讨论图像的创建和编辑及其与网页编写的关系。可能的主题包括如何最好地利用 Web 的图像显示能力，以及放置图像地图的常见问题和解决方案。

**comp.infosystems.www.authoring.misc**

该新闻组涵盖未由其他 comp.infosystems.www.authoring.* 组涵盖的各种 Web 编写问题。主题包括音频和视频的使用等。

**comp.infosystems.www.authoring.site-design**

该新闻组涵盖站点设计问题。您可以了解他人使用过的好的和坏的站点设计。

**comp.infosystems.www.authoring.stylesheets**

该新闻组涵盖在网页开发中使用的样式表。

**comp.infosystems.www.authoring.tools**

该新闻组讨论 Web 工具，范围从允许您创建 Web 内容的编写工具到完整的 Web 发布引擎。

## Web 浏览器相关新闻组

如果您对各个平台上的 Web 浏览器感兴趣，您可以浏览或在此类新闻组中发布问题。

**comp.infosystems.www.browsers.misc**

该新闻组涵盖所有其他平台的 Web 浏览器。主题包括配置问题/解决方案、外部查看器（辅助应用程序）和错误报告。包含的平台有 Amiga、DOS、VMS 和 Unix 文本模式。

**comp.infosystems.www.browsers.mac**

该新闻组讨论 Macintosh 平台的 Web 浏览器。主题包括配置问题/解决方案、外部查看器和错误报告。

**comp.infosystems.www.browsers.ms-windows**

该新闻组讨论 MS Windows 和 NT 平台的 Web 浏览器。主题包括配置问题/解决方案、外部查看器（辅助应用程序）和错误报告。

**comp.infosystems.www.browsers.x**

该新闻组讨论 X Window 系统的 Web 浏览器。主题包括配置问题/解决方案、外部查看器和错误报告。

## 公告新闻组

此类新闻组由各种组织用于发布软件版本、关于 Web 软件的安全警报以及其他重要事项。除非您有与该组相关的信息要发布，否则您不应在这些新闻组中发布内容。

**comp.infosystems.www.announce**

这是一个可以发布新的 Web 相关资源的新闻组。

## 其他 WWW 新闻组

此类新闻组是 Web 倡导组织以及与不隶属于其他任何类别事项相关的组织。

**comp.infosystems.www.advocacy**

该新闻组用于评论、辩论、争论和讨论哪种 Web 浏览器、服务器、外部查看器程序和其他软件比其他软件更好或更差。

**comp.infosystems.www.misc**

comp.infosystems.www.misc 为一般性讨论 WWW 相关主题提供了一个论坛，这些主题未由层级中的其他新闻组涵盖。该组可能包括关于 Web 结构未来变化以及影响客户端和服务器两者之 Web 协议的讨论。

## Perl 新闻组

由于 Perl 在 CGI、mod_perl 和 FastCGI 编程中大量使用，以下 Perl 新闻组可能非常有益。

**comp.lang.perl.announce**

在此处发布新版本、FAQ 和新模块。

**comp.lang.perl.misc**

该新闻组致力于讨论 Perl；它包括从错误报告到新功能，再到历史、幽默和琐事的一切。这是任何与 Perl 相关事项的最佳信息来源，尤其是关于 Perl 5 的新内容。

## 邮件列表

如果您希望接收有关 Apache 基金会及其活动的 Apache 公告，请订阅 `announce-subscribe@apache.org`。请记住，这不是一个讨论邮件列表。它仅由 Apache 基金会用于发布值得报道的事项。请勿在那里发布问题或评论。

如果您对 Apache 会议感兴趣，这对于认真的 Apache 管理员来说是一个很好的资源，您可以订阅 `announce-subscribe@apachecon.com` 列表。这也是一个公告列表，不适合发布任何问题或评论。

如果您对新的 Apache 开发相关主题感兴趣，那么您可以订阅 `new-httpd-subscribe@apache.org`。

您还可以订阅 `http://groups.yahoo.com/group/new-httpd`，这是一个专门针对 Apache 服务器的 Yahoo! 小组。

## 商业资源

越来越多的 Apache 用户（尤其是企业用户）一直在寻找提供 Apache 软件或服务的商业资源。一些著名的 Apache 商业资源包括：

- Stronghold - www.c2.net
- Covalent Raven - http://raven.covalent.net
- Roris - www.rovis.com/warpaint/





## 其他相关资源

有许多网站对 Web 开发者或管理员大有裨益。下面列出了一份此类资源的简短清单。

- 万维网联盟— `www.w3.org/`
- Netcraft 调查报告网站— `www.netcraft.co.uk/Survey/`
- Server Watch— `www.serverwatch.com`
- Search Engine Watch— `www.searchenginewatch.com`
- Browser Watch— `www.browsewatch.com`
- Web Compare— `www.webcompare.com`
- Web Developer— `www.webdeveloper.com`
- Web Reference— `www.webreference.com`
- 互联网上的电子商务— `http://e-comm.internet.com`
- ISP 购买指南— `www.TheList.com`
- 互联网新闻— `www.InternetNews.com`
- CGI 规范— `http://hoohoo.ncsa.uiuc.edu/cgi/interface.html`
- FastCGI 网站— `www.fastcgi.com`
- Perl 语言站点— `www.perl.com`
- Perl 爱好者（Perl Mongers）— `www.perl.org`

## CD-ROM 上有什么？

**随**书附带的 CD-ROM 中包含许多优秀的软件程序和文件，在您阅读本书时能为您节省大量时间。若要快速浏览 CD-ROM，请使用文件浏览程序，例如在 X Windows 系统下的 **文件管理器（File Manager）** 或在 Windows 系统下的 **Windows 资源管理器（Windows Explorer）**。

若要查看 CD-ROM 的内容，Unix 和 Linux 用户必须使用 `mount` 命令挂载 CD-ROM。Windows 用户只需将 CD-ROM 插入 CD-ROM 驱动器并刷新其 Windows 资源管理器窗口（按 F5 键）。

以下章节描述了 CD 上可找到的内容。

### Apache 服务器发行版

此 CD 中包含了 Apache 服务器源代码发行版的最新版本。由于 Windows 2000/NT/9x 平台的操作系统并未附带编译和构建 Windows 平台上 Apache 所需的适当 C 编译器及其他开发工具，我们还为这些平台提供了 Apache 服务器的 **二进制发行版（binary distribution）**。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_749_0.png)

随书附带的 CD-ROM 包含由 Apache 软件基金会（`http://www.apache.org` ）开发的软件。

### 可搜索 PDF 格式的书籍章节

本书的所有章节均以 PDF 格式包含在内，以便您搜索并打印其中仅供个人使用的信息。为方便起见，我们在 CD 中为 Windows 平台提供了 Acrobat Reader 5.0。

**注意**
Unix/Linux 用户必须使用相应平台的 Acrobat Reader，而不是其他可能无法在可搜索 PDF 文档上正常工作的 PDF 阅读器。

### 文本格式的书籍示例脚本

作者开发的所有示例脚本均以文本格式包含在 CD 中。请从相应目录复制每个脚本，并根据需要对其进行修改。

**注意**
请确保为 Web 服务器用户启用执行权限，以便通过 Apache 运行这些脚本。

### MySQL

MySQL 是一个免费的、广泛用于 Web 应用程序数据库服务器的关系型数据库服务器。CD 中包含了 MySQL 数据库服务器的版本。该目录中同时包含了服务器在 Linux（和 Unix）以及 Windows 上的版本。要了解如何在您的系统上安装 MySQL 数据库，请访问 http://www.mysql.com 查看详情。

### OpenSSL

OpenSSL 是安全套接字层（SSL）协议的开源实现。Apache-SSL 发行版和 Apache 的 mod_ssl 模块需要 OpenSSL 源代码发行版。CD 中包含了 OpenSSL 源代码发行版。

**注意**
随书附带的 CD-ROM 包含由 Ben Laurie 为 Apache-SSL HTTP 服务器项目开发的软件。

### PHP

CD 中包含了 PHP 源代码发行版。要在您的 Unix/Linux 系统上安装 PHP，请遵循第 15 章中的说明。

**注意** 随书附带的 CD-ROM 包含由 PHP 开发团队编写的软件。

### Perl 及相关模块

CD 中包含了 Perl 脚本语言的源代码发行版。要在您的 Unix/Linux 系统上安装 Perl，请在硬盘上的目录（例如 `/usr/local/src`）中解压源代码发行版，并阅读 INSTALL 文件以获取详细信息。

**注意** Windows 2000/NT/9x 用户应改为从 `http://www.activeperl.com` 下载二进制发行版。

CD 中包含的 Perl 模块有 `HTML::Template`、`Config::IniFiles`、`LWP`、`CGI`、`MIME::Lite`、`MIME::Lite::HTML`、`DBI`、`DBD::MySQL`、**以及** `FCGI`。将这些模块中的任意一个解压到诸如 `/usr/local/src` 的目录中，并阅读 INSTALL 和/或 README 文件以获取详细的安装说明。

此外，CD 中还包含了 Apache 模块 `mod_perl` 的源代码发行版。有关如何在您的系统上安装 `mod_perl` 的信息，请参阅第 16 章。

### Tomcat

CD 中包含了名为 Tomcat 的 Java  servlet 容器软件。有关如何在您的系统上安装 Tomcat 的详细信息，请参阅第 17 章。

# 故障排除

如果您在安装或使用随书 CD 上的任何材料时遇到困难，请尝试以下解决方案：

- **关闭您可能正在运行的任何防病毒软件。** 安装程序有时会被误认为病毒活动，这可能使您的计算机错误地认为它感染了病毒。（请务必稍后重新开启防病毒软件。）
- **关闭所有正在运行的程序。** 运行的程序越多，可用于其他程序的内存就越少。安装程序通常还会更新文件和程序；如果您让其他程序继续运行，安装可能无法正常工作。
- **参考 ReadMe：** 请参阅位于 CD-ROM 根目录的 ReadMe 文件，以获取出版时的最新产品信息。

如果 CD 仍存在问题，请致电 Hungry Minds 客户关怀电话：(800) 762-2974。在美国以外地区，请致电 1 (317) 572-3994。您也可以通過電子郵件 techsupdum@hungryminds.com 聯繫 Hungry Minds 客服。Hungry Minds 仅针对安装和其他一般质量控制项目提供技术支持；对于应用程序本身的技术支持，请咨询该程序的供应商或作者。

# 索引

- **符号和数字**
  - 双与号 (`&&`) 逻辑运算符，395–396
  - 与号 (`&`) 键值对分隔符，328
  - 星号 (`*`)
    - 正则表达式标准量词，711
    - 通配字符，77, 79
  - 反斜杠 (`\\`)
    - 路径分隔符，579
    - 正则表达式转义字符，711
  - 括号
    - `<>` (`<angle>`) URL (统一资源定位符) 重写条件模式分隔符，247
    - `[ ]` (方括号) 正则表达式元字符集分隔符，710, 711
  - 脱字符 (`^`) 正则表达式元字符，710
  - 冒号 (`:`) `DBM` 文件字段分隔符，114
  - 逗号 (`,`)
    - `DBM` 文件组名分隔符，115
    - 统一资源定位符 (URL) 重写标志字符串分隔符，243
  - 美元符号 (`$`)
    - 正则表达式元字符，710
    - 变量前缀，393–394
    - 变量值，插入，394
  - 等号 (`=`)
    - 比较运算符，394, 396
    - 键值对运算符，328
    - 统一资源定位符 (URL) 重写条件模式前缀，247
  - 等号，逗号 (`,`)
    - 比较运算符，394
  - 感叹号 (!)
    - CLF (通用日志格式) 缺省服务器标记，227
    - 条件语句前缀，63, 64
    - 逻辑运算符，395–396
    - 变量运算符，108
  - 感叹号，等号 (!=)
    - 比较运算符，394, 396
  - 大于号，等号 (> )
    - 比较运算符，394
  - 大于号 (`>`) 比较运算符，394
  - 连字符 (`-`) 日志文件空标记，221
  - 小于号 (`<`) 比较运算符，394
  - 小于号 (`<`) 比较运算符，394
  - 减号 (`-`) 指令开关，66, 67
  - 井号 (`#`)
    - 注释前缀，31, 345
    - 用户 ID 号前缀，97
  - 百分号 (`%`)
    - 编码字符序列前缀，328
    - 日志条目说明符前缀，225
    - 变量前缀，246
  - 句点 (`.`)
    - 目录前缀，47, 115
    - 正则表达式元字符，710, 715
  - 双竖线 (`| |`) 逻辑运算符，395–396
  - 竖线 (`|`) `OR` 运算符，261, 711
  - 加号 (`+`)
    - 指令开关，66, 67
    - 超文本传输协议 (HTTP) 空格字符标记，328
    - 正则表达式标准量词，711
  - 双引号 (`""`) 身份验证标签分隔符，186
  - 斜杠 (`/`)
    - 别名定义中，145
    - 路径分隔符，579
  - 问号 (`?`)
    - 正则表达式标准量词，711
    - 通配字符，79
  - 波浪号 (`~`) 扩展正则表达式前缀，77

- **A**
  - `a` (`ApacheBench`) 实用工具，10, 28, 618–619
  - 访问多个 URL (统一资源定位符) 重写规则，259–261

- **A**
  - `AccessFileName` 指令，47, 59–60
  - `AccessWatch` 日志分析工具，233
  - `Ace` (Direct, 614
  - `ACL` (访问控制列表)，622–623, 624, 625, 689–694, 695
  - `action` 命令，622, 624
  - `action` 指令，118–121
  - 禁用动作触发，22
  - Active Server Pages, 参见 **ASP**
  - `ActiveState` 网站，584, 585, 221
  - `AddAlt` 指令，131
  - `AddAltByEncoding` 指令，131–132
  - `AddAltByType` 指令，132
  - `AddCharset` 指令，124–125
  - `AddDefaultCharset` 指令，50, 60
  - `AddDescription` 指令，132
  - `AddEncoding` 指令，125
  - `AddHandler` 指令，125, 152, 337, 417
  - `AddIcon` 指令，133
  - `AddIconByEncoding` 指令，133
  - `AddIconByType` 指令，134
  - `AddLanguage` 指令，125–126
  - `AddModule` 指令，76
  - `AddModuleInfo` 指令，215
  - `AddType` 指令，126, 128, 341,
  - 管理员界面，6
  - `Ajp12` 连接处理程序协议，473, 475
  - `Ajp12` 工作器类型，473, 476
  - `Ajpl3` 连接处理程序协议，473, 475
  - `ajp13` 工作器类型，473, 476
  - `Alias` CGI 屏幕，582
  - `alias` 指令，49, 62, 145 别名
    - CGI (通用网关接口) 中的，49, 335–336, 502–504, 505–506, 536–537 创建，145–146 指令，49–50, 42, 49, 145–146, 335–336 脚本别名，148, 150–151, 159 安全考虑，145 服务器别名，82
    - 在定义中使用通配符，82
  - `AliasMatch` 指令，146
  - `Allow` 指令，41, 194–199
  - `allow` 来自 `env var table` 指令，193





# 索引

### A
- AllowOverride 指令，43，59，86–87，381
- Alteon Acat 引导程序，614
- 双与号（`&&`）逻辑运算符，395–396
- 与号（`&`）键值对分隔符，328
- 模拟日志分析工具，233
- 匿名用户访问，21，110–112
- Anonymous.Authenticate 指令，111
- Anonymous.Logfile，111
- Anonymous.MustGiveEmail 指令，111
- Anonymous.NosUserID 指令，111
- Anonymous.VerifyEmail 指令，111–112
- Apache 基金会，439，717
- Apache 小组，5
- Apache 小组项目，573
- Apache CGI 网站，581，713
- Apache `-r` 重启命令，577
- Apache `-k start` 命令，577
- Apache `-k stop` 命令，577
- Apache 模块索引，500，713
- Apache `-shutdown` 命令，577
- Apache `-t` 命令，580
- Apache Today 网站，71，713
- Apache 网站
  - 从中下载 Apache，14，18–19，30，499–500
  - 镜像站点，18，278
  - 模块注册表，500，713
  - PGP（Pretty Good Privacy）签名，499–500
- Apache 网站，30，713
- Apache 2.0.tar.gz 文件，500
- Apache-ASP 模块，466–467，586
- Apache:ASP 网站，467
- Apache:AuthnDBI 模块，202
- Apache:AuthnDBI 模块，202–203
- ApacheBench 实用工具，参见 ab
- apachectl configtest 命令，175
- apachectl restart 命令，52
- apachectl 脚本，28
- apachectl stop 命令，53
- Apache:DBI 模块，586，628
- Apache:Perl 集成项目网站，455，713
- Apache:Registry 模块，456–457
- Apache:SSL
  - 缓存服务器位置，
  - 拼接，561
  - 证书创建，559–560
  - 编译，558–559
  - 下载，558
  - 启用，561
  - httpd.conf 设置，560–561
  - 安装，558–559
  - 需要 OpenSSL 软件包，552，558
  - 补丁工具包，551，559
  - 随机数据生成，560
- Apache:SSL 网站，551，713
- APL（应用程序语言）
- ASP（Java Server Pages），470
- mod_perl 模块，458
- Server API，CGI（通用网关接口）
  - 比较，400–401
  - Server API 与 FastCGI 比较，400–401，402
- API_VERSION 变量，242
- AppCatalase，414–415，416
- APR（Apache 可移植运行时），10，27
- apxs 实用工具，28
- arayz
  - CGI（通用网关接口），346–347，357
  - Perl，346–347，357
  - PHP：超文本预处理器，447，449
- .alic 文件，500
- .asis 文件，138
- ASP（活动服务器页面），466–470，470
  - asp 指令，467
- assignedrid 指令，498
- 星号 (*) 指令，98
  - 正则表达式标准量词，711
  - 通配符字符，77，79
- ATA（AT 附件）硬盘，596。另见 hard drive
- ATA 包接口硬盘，596。另见 hard drive
- AuthnDBI.username PerlSetVar 指令键，203
- AuthnDBI.GroupFile 指令，114–116，188
- AuthnDBIUserFile 指令，114，188
- AuthnDBIUserFile 指令，116
- 身份验证。另见 password；security
  - 授权，与身份验证结合使用，195
  - 身份验证与授权的区别，181–182
  - Basic 身份验证，87
  - 使用 Berkley DB 文件，109，112，116–117
  - 其中的浏览器类型评估，194
  - CGI（通用网关接口）脚本访问，194
  - 使用 cookie 进行会话身份验证，208–212
  - 使用数据库，109，112–114，195–204
  - Digest 身份验证，87，109
  - 目录特定的仅成员网页，186–187，209
  - 通过 AuthName 指令实现目录特定身份验证，87
  - 通过 AuthType 指令实现目录特定身份验证，87
  - 通过 mod_auth_mysql 模块实现目录特定身份验证，200–201
  - 通过多种身份验证方案实现目录特定身份验证，185
  - 通过 Require 评估实现目录特定身份验证，90–91
  - 环境变量评估，193–194
  - 环境变量存储方法，333
  - FastCGI 外部身份验证，403，408
  - 通过主机名允许访问，109，190–194
  - 通过主机名拒绝访问，192，194
  - 基于 .htaccess 文件的身份验证，47，59，185–188
  - HTTP（超文本传输协议）身份验证，6，29，87，182–183，501
  - 通过 HTTP（超文本传输协议）请求方法阻止访问，194
  - 使用 IBM DB2 数据库服务器，202
  - 通过 IP（互联网协议）地址进行身份验证，109，190–194
  - 通过 mod_auth 模块进行身份验证，109，184–190
  - 通过 mod_auth_mysql 模块进行身份验证，200–202
  - 模块，身份验证，105，109–118
  - 使用多种方案，115，185
  - 使用 MySQL 数据库服务器，196–202
  - 使用 Oracle 数据库服务器，202
  - 密码在其中的作用，181，183
  - 使用 PHP：超文本预处理器脚本，451–454
  - 使用 Postgres 数据库服务器，202
  - 代理服务器，277
  - 设置 realm 名称，87
  - 指定充分的要求，91–92
  - 会话身份验证，208–212
  - 级联（trickle-down），185，201
  - 用户组，185，188–190，198，204–208
  - 用户名在其中的作用，181，183
  - 使用身份验证限制网站目录访问，186–187，209
- AuthGroupFile 指令，185，188
- Auth_MySQL_directive，201
- Auth_MySQL_Authoritative 指令，201
- Auth_MySQL_DB_directive，201
- Auth_MySQL_Empty_Passwords 指令，201
- Auth_MySQL_Encrypted_Passwords 指令，201
- Auth_MySQL_Encryption_Types 指令，201
- Auth_MySQL_Group_Field 指令，201
- Auth_MySQL_Non_Persistent 指令，201
- Auth_MySQL_Password_Field 指令，201
- Auth_MySQL_Username_Field Passwords 指令，201
- Auth_MySQL_Username_Field 指令，201
- AuthName 指令，87，186，188，308
- 授权
  - 与身份验证结合使用，195
  - 身份验证与授权的区别，181–182
  - auth.php 脚本，452
- AuthTicket 模块，209
- AuthType 指令，87，188
- Auth_TTPE_variable，241，333
- authuser 日志文件标记，221
- AuthUserFile 指令，184–185，208
- auto_append_file 指令，428
- auto_prepend_file 指令，428–429
- awk 实用工具，603，648

### B
- bbd(2ext ) 方法，526
- 反斜杠（`\`）
  - 路径分隔符，579
  - 正则表达式转义字符，711
- 备份
  - 通过 cron 作业运行，311
  - 在文件系统更改之前，604，649
  - 在使用 hdiran 实用工具之前，509，602，644
  - 介质，311
  - 网站，310–312
- backup.gz 文件，125
- badcalc.pl 脚本，371
- Badwords ACL（访问控制列表）角色，624
- bak.files，311
- 计算带宽需求，17–18
- 横幅广告，318
- base 指令，152
- bashrc 文件，471，484
- 基准测试，28
- 使用 Berkeley DB 文件进行身份验证，109，112，116–117
- bin 目录，27
- BIND DNS（域名服务）服务器，166
- 块
  - NFS（网络文件系统），659–662
  - 预留，606，650
  - 大小优化，603，648，659–662
- BootLeg 网站，233
- 括号
  - `<>`（尖括号）URI（统一资源定位符）重写条件模式分隔符，247
  - `[]`（方括号）正则表达式元字符集分隔符，710，711
- BrowserWatch 网站，718
- BrowserMatch 指令，107–108，194
- BrowserMatchNoCase 指令，107–108
- bytes 日志文件标记，221

### C
- `\c/`（反斜杠，小写 c，方括号）正则表达式元字符，710
- CA（证书颁发机构），547，550–551，562，564–565
- 缓存管理。另见 memory management
  - DNS（域名服务），167，639
  - 数据库连接，628–630
  - 启用缓存，21，22，129，155
  - FastCGI，401–402，408
  - 文件句柄，155，607–608
  - 文件系统，分配给缓存，623–624
  - 检查硬盘子目录，600，645
  - MySQL，625
  - 负缓存，625–626
  - 为速度优化，600，620–627
  - 代理服务器，269，272–275，276–278，621–626
  - SSL（安全套接层），556，561
  - Squid 代理缓存服务器，624–625
  - 统计信息，621
  - 生存时间设置，556，561，625
- CacheDefaultExpire 指令，274
- CacheDirLength 指令，274
- CacheDirLevels 指令，274
- CacheFile 指令，155
- CacheGclInterval 指令，273
- CacheGclMaxFileFactor 指令，273
- CacheMaxExpire 指令，273
- cache_mem 命令，625
- cachemgr.cgi 文件，625
- CacheNegotiatedDocs 指令，129
- CacheRoot 指令，272
- 加州州立大学萨克拉门托分校网站。参见 CSUS 网站
- 规范名称记录。参见 CNAME 记录
- CAP_CHOWN 入侵检测能力，696
- CAP_DAC_OVERRIDE 入侵检测能力，696
- CAP_DAC_READ_SEARCH 入侵检测能力，696
- CAP_FOWNER 入侵检测能力，697





# 索引

- CAP_FSET：入侵者检测功能，697
- CAP_HIDDEN：入侵者检测功能，699，701
- CAP_INI_KILL：入侵者检测功能，699，700–701
- CAP_IPC_LOCK：入侵者检测功能，698
- CAP_KILL：入侵者检测功能，697
- CAP_LEASE：入侵者检测功能，699
- CAP_LINUX_IMMUTABLE：入侵者检测功能，697
- CAP_MKNOD：入侵者检测功能，699
- CAP_NET_ADMIN：入侵者检测功能，698，702
- CAP_NET_BIND_SERVICE：入侵者检测功能，697
- CAP_NET_BROADCAST：入侵者检测功能，697
- CAP_NET_RAW：入侵者检测功能，698，702
- CAP_SETGID：入侵者检测功能，697
- CAP_SETFCAP：入侵者检测功能，697
- CAP_SETUID：入侵者检测功能，697
- CAP_SYS_ADMIN：入侵者检测功能，698
- CAP_SYS_BOOT：入侵者检测功能，698
- CAP_SYS_CHROOT：入侵者检测功能，698
- CAP_SYS_MODULE：入侵者检测功能，698
- CAP_SYS_NICE：入侵者检测功能，699
- CAP_SYS_PACCT：入侵者检测功能，698
- CAP_SYS_PTRACE：入侵者检测功能，698
- CAP_SYS_RAWIO：入侵者检测功能，698，701
- CAP_SYS_RESOURCE：入侵者检测功能，699
- CAP_SYS_TIME：入侵者检测功能，699
- CAP_SYS_TTY_CONFIG：入侵者检测功能，699
- 脱字符（^）正则表达式元字符，710
- 大小写转换操作，248，346–347
- 大小写敏感性
  - URL（统一资源定位符）重写规则，忽略大小写，245，247
  - 用户名，110
- cat 实用工具，232–233
- 随书附带的光盘
  - CGI 模块，721
  - 便携式文档格式（PDF）章节，720
  - config::infilters 模块，721
  - DBI::MySQL 模块，204，721
  - DBI 模块，202，628，721
  - FastCGI SDK（软件开发工具包），408–409
  - FCGI 模块，411–412，721
  - fcrm2zard::pl 脚本，352，364
  - HTML::Template 模块，721
  - LWP 模块，721
  - make::papa 脚本，304–305
  - MIME::Lite 模块，721
  - MIME::Lite::HTML 模块，721
  - mod_perl 源代码发行版，721
  - 挂载，719
  - MySQL 数据库服务器，720
  - OpenSSL，720
  - Perl 源代码发行版，721
  - PHP：Hypertext Preprocessor 源代码发行版，721
  - 脚本示例，720
  - 服务器源代码发行版，719
  - Tomcat，721
  - 故障排除，721–722
- 中央处理单元，参见 CPU
- CERT（计算机应急响应团队），499
- 证书颁发机构。参见 CA
- 证书吊销列表。参见 CRL
- 证书签名请求。参见 CSR
- 证书。另见 加密
  - Apache::SSL 服务器，创建，559–560
  - 交叉链接，564
  - 文件路径，定义，557，561
  - 颁发者，547，550–551，562
  - 密钥文件，557
  - 名称，可区分名称，547–548
  - 签名请求，562，563–564
  - 交易流程，548–550
- cgi 命令，386–389
- CGI（通用网关接口）。另见 Perl
  - 架构，分布式支持，401
  - 数组，操作，346–347，357
  - 身份验证，194，333
  - 大小写转换操作，346–347
  - cgi-bin 访问，339
  - cgi-bin 模块，使用其编写脚本，345，346–349，356
  - 字符集，获取，330
  - 非法字符，528
  - 子进程，交互，9
  - 客户端软件信息，获取，331
  - 注释，545
  - 连接信息，获取，332
  - 内容，与脚本分离，342
  - Content-Type 头，创建，347，525
  - CPU（中央处理单元）使用率，控制，74
  - 守护进程，9–10，23，328
  - 脚本调试，370–376
  - 描述，321–322
  - 目录，在目录中启用/禁用，66，67
  - DirectoryMatch 容器，为其定义，339–340
  - 文档根目录，脚本分离，49，503–504
  - 文档根目录信息，获取，329
  - 脚本文档化，315
  - 电子邮件地址标准化，342–343
  - 站点管理员的电子邮件地址，获取，329
  - 使用其发送电子邮件网页，364–369
  - 启用/禁用，23，66，67，338–341，510
  - 编码模式，获取，330
  - 使用其生成错误消息，63，352，353，360，361
  - eval() 调用，518
  - exec() 调用，518–519，529–530
  - FastCGI，迁移至，408–413
  - 与 FastCGI 对比，399–401，402
  - 文件扩展名，分配，337–338，341
  - 文件扩展名，出于安全考虑避免使用，537
  - 过滤器脚本，118–121
  - 表单，集中管理，350，364
  - 表单，创建 CGI 对象，352，353，356
  - 表单，数据存储，350，352，353
  - 表单，生成错误消息，352，353，360，361
  - 表单，加载模块，352，353，355–356
  - 表单，使用单个脚本使用多个，349
  - 表单，模板，356，357–358，360，362
  - 表单，显示感谢消息，352，358，361，362–363
  - 表单，用户数据验证，352，353，358–360，361
  - 表单，用户重定向，361–362
  - 表单配置文件，加载，352，356
  - 表单配置文件，在其中定位 Web 表单，352，353，356–357，360
  - GET 请求，323–326，327
  - 避免硬编码可定制信息，342
  - HTML（超文本标记语言）内容创建，315，347–349，325
  - HTTP（超文本传输协议）头解析，323，325
  - HTTP（超文本传输协议）请求处理，122，333，334
  - httpd.conf 设置，329，336，337，339，356
  - 索引守护进程信息，333
  - 索引默认值，指定脚本作为默认值，131
  - 信息泄露，517
  - 入侵者检测，515–517
  - IP（互联网协议）地址信息，获取，330，332
  - 与 Java  Servlets 对比，469，470
  - 语言信息，获取，331
  - 生命周期考虑因素，314
  - 循环，346，361，412
  - 内存需求，17
  - 模块使用，控制，74，409
  - MIME（多用途互联网邮件扩展）类型，将脚本与之关联，118–121
  - MIME（多用途互联网邮件扩展）类型，获取，330，333–334
  - mod_perl 模块，使用其运行脚本，456–457
  - 模块，动态内容生成，105，117–124
  - 输出，322–328
  - 脚本所有权，更改，534
  - 路径名，避免使用绝对路径，314
  - Perl，将 CGI 脚本标识为 Perl，345，355
  - Perl，用其编写脚本，342–343
  - 权限，301，505
  - PHP：Hypertext Preprocessor 作为解释器，424，427，434
  - pipe(open()) 调用，518
  - 计划依赖，400
  - 端口信息，获取，332
  - POST 请求，326–327
  - 进程，9，400，401
  - 程序目录，28，49
  - 程序目录，别名，338–336
  - 编程语言依赖，400
  - 使用其配置代理服务器，288–290
  - 公共领域应用程序，501
  - 查询字符串信息，获取，334
  - 远程主机信息，获取，332
  - 请求处理模型，404–405
  - 重命名，537–540
  - 脚本别名，49，503–504，505–506，536–537
  - 脚本执行描述，9–10
  - 脚本封装，531–536
  - 与 Server API（应用程序编程接口）对比，400–401
  - 服务器处理，获取，329
  - 服务器处理，324
  - 服务器协议，获取，333
  - shebang 行，584
  - 套接字连接，10
  - 支持的规范，获取，329
  - SSI（服务器端包含），从中调用脚本，386–389
  - 标准，开放，400
  - 子程序，356–357
  - SUexec 支持，使用其测试，533
  - 支持，6，23
  - system() 调用，518–519，529–530
  - 系统调用，重用，518–520
  - 系统命令欺骗，518
  - 系统资源过载攻击，518
  - 临时文件位置，512
  - 测试脚本，501
  - 文本，操作，346–347
  - UID（用户 ID）所有者的，在该用户下运行脚本，531
  - URL（统一资源标识符）信息，获取，331，334–335
  - URL（统一资源定位符），操作，263，325，368–369
  - 用户数据，标准化，342–343
  - 用户输入，322–328，345，518–520，527–531
  - 用户重定向，脚本，507–508
  - 用户名，使用字母数字时的考虑因素，340
  - 用户名，获取，332–333
  - 验证，数据，343，352，353，358–360，361
  - 变量，避免在基于 Perl 的脚本中使用全局变量，315
  - 变量，客户端请求，330–335
  - 变量，自定义，345
  - 变量，环境，106–107，323，326，328–335
  - 变量，服务器，329
  - 版本控制，314
  - 虚拟主机支持，配置，336
  - Windows，在该环境下运行基于 Perl 的脚本，384
- CGI 模块（光盘上），328，347–348，356，521
- CGI 规范网站，718
- cgi-bin 访问，339
- cgi-bin 目录，28
- cgcchk.pl 扫描器，537–539
- CGI::Debug 模块，374–376
- CGI::pm 模块，345，346–349，356，462–464
- CGIWrap 封装器，534–536
- cgiwrapper，534–536
- CGI（通用网关接口）脚本，在其中进行操作，330
- Content-Header，60
  - 文件扩展名，映射到，124–125
  - PHP：Hypertext Preprocessor 默认值，429
  - 服务器默认值，50
  - 相关变量，529
- CheckHeader 指令，149–150
- 校验和，501，502
- ChildPerDir 指令，169
- ChildPerUser 指令，98–99
- cd 命令，455
- chown 命令，45，254，436，486，487
- Circle 指令，153





- CISCO 本地负载均衡器，614, 615, 640
- class_path 设置，476
- ClearModuleList 指令，76
- 逗号（通用日志格式），221, 227
- CLF 文件，221
- CNAME（规范名称）记录，68, 166, 257
- 冒号（:）DBM 文件字段分隔符，114
- colors.pl 脚本，386–387
- Commona，使用其管理 Apache，581–584
- 逗号（,）
    - DBM 文件组名分隔符，115
    - URL（统一资源定位符）重写标志字符串分隔符，243
- 逗号分隔值文件。参见 CSV 文件
- 注释
- CGI（通用网关接口）脚本，345
- 配置文件，31
- Perl 脚本，345
- 通用网关接口（CGI）。参见 CGI
- 通用日志格式。参见 CLF
- comp.infostytems.www.advocacy 新闻组，716
- comp.infostytems.www.announce 新闻组，716
- comp.infostytems.www.authoring.cgi 新闻组，715
- comp.infostytems.www.authoring.html 新闻组，715
- comp.infostytems.www.authoring.images 新闻组，715
- comp.infostytems.www.authoring.misc 新闻组，715
- comp.infostytems.www.authoring.sitedesign 新闻组，715
- comp.infostytems.www.authoring.stylesheets 新闻组，715
- comp.infostytems.www.authoring.tools 新闻组，715
- comp.infostytems.www.browsers.mac 新闻组，716
- comp.infostytems.www.browsers.msvc 新闻组，716
- comp.infostytems.www.browsers.ms-windows 新闻组，716
- comp.infostytems.www.browsers.x. 新闻组，716
- comp.infostytems.www.msvc 新闻组，716
- comp.infostytems.www.servers.mac 新闻组，714
- comp.infostytems.www.servers.misc 新闻组，714
- comp.infostytems.www.servers.ms-windows 新闻组，714
- comp.infostytems.www.servers.unix 新闻组，714
- comp.lang.perl.announce 新闻组，717
- comp.lang.perl.misc 新闻组，717
- 综合 Perl 归档网络（CPAN）模块。参见 CPAN 模块
- 计算机应急响应小组。参见 CERT
- config 目录，27
- config 命令，382–385
- confg 指令，29
- config error 命令，383
- config 错误，382–383
- Config::Inflates 模块
- Config：（光盘上），356, 721
- cfg.status 脚本，179
- 配置文件。另见
    - httpd.conf 文件
    - 注释，31
    - 条件式，63
    - 默认值，31
    - 目录访问控制文件，47, 59–60
    - 外部，65, 170–171
    - 转发，101, 354–355
    - 高性能。另见 htpmperformance.conf，29
    - httpd-100.conf，164
    - httpd-101.conf，165
    - httpd-8080.conf，632
    - httpd-stld.conf，29
    - httpd.conf，560
    - install.cfg，675–677
    - 介绍，6
    - limits.conf，693
    - vhosts.conf，632, 669, 691
    - 位置，27, 503
    - new_httpd.conf，577
    - 下一个目录，58–59, 242, 249
    - Perl 代码，使用其生成，171–175
    - php，425, 427, 428–435, 586
    - php.ini，27, 581, 624
    - php_ini，586
    - php.ini，425, 427, 428–435, 586
    - php.ini，27, 581, 624
    - php_ini，586
    - 服务器，31–36
    - smf.conf，300, 622, 624
    - smf.conf，300
    - SSL（安全套接字层），指定其位置，553
    - 因错误导致的启动失败，50
    - syslog.conf，230–231
    - Tomcat，473, 479, 482, 490
    - tc.cfg，678
    - 虚拟主机，160, 163–165, 170–171
- 配置脚本，19–24, 179, 214
- ConditionStatus 指令，99
- Constants.pm 模块，460
- 容器。 56
    - 指令容器，56
    - 指令，57–58
    - 指令。容器，43–44, 76–80
- 容器（目录），57, 58, 60
    - `<DirectoryMatch>`，57, 78
    - `<Files>`，57, 58, 78–79
    - `<FilesMatch>`，71, 79
    - `<IFDefine>`，63, 556
    - `<JModVhost>`，38, 47–48, 64
        - Java 运行时环境（JRE），469
    - `<LIMIT>`，58, 59, 88–89
    - `<LimitExcept>`，89
    - `<Location>`，57, 58
    - `<LocationsMatch>`，57, 80
        - Perl 脚本，使用其定义，173
    - cvpce proccedure，58
    - `<virtualHost>`，57, 58, 65, 68, 82–83
        - WebDAV（Web 分布式创作与版本控制），在其中使用，186
- ContentBig 指令，60–61
- CONTENT-LENO 变量，327, 334
- 内容协商文档，128–129
- CONTENT_TYPE 变量，333–334
- COOKIE Expires 指令，229
- COOKIE-LID 指令，224
- Cookie
    - 浏览器与服务器交互，228
    - 取消/禁用，229
    - 加密，209, 210, 224
    - 过期，229, 445
    - 存储于其中的文件，229
    - HTTP（超文本传输协议）Cookie，228
    - 记录 Cookie 信息，224, 225, 228–229
    - Mysql，在其中工作，212
    - PHP：超文本预处理器
        - 基于此的会话，88
        - 提示选项，211
        - 使用此进行会话身份验证，208–212
        - 使用此进行用户跟踪，228–229
        - CookTracking 指令，229
- 版权
    - 成为内容发布政策的一部分，512
    - 图像水印化，通过此方式，512
    - PHP：超文本预处理器
        - 使用其生成脚本，438–440
    - SSI（服务器端包含），使用其嵌入，314
- CoreDumpDirectory 指令，92
- Covalent Commache 网站，581
- Covalent RawN 网站，717
- CPanel（综合 Perl 归档网络）模块，204, 204, 356, 343, 356, 457
- CPanel 模块，204, 356
- CPanel pm 模块，343
- CPU（中央处理单元）
    - CGI（通用网关接口），控制使用量，74
    - 速度，593–594
- 创建数据库命令，196
- 创建表命令，197
- CRL（证书吊销列表），556
    - .crl 文件，556
- 计划任务（cron jobs）
    - 通过其运行备份，311
    - 通过其运行日志脚本，220, 224, 227
    - 通过其运行 makepage 脚本，305
    - 通过其运行 ride / 脚本，468
    - 通过其运行 tripwire，674, 685, 686
- .crt 文件，556
- crypt 函数，114, 116, 184
- CSR（证书签名请求），562, 563–564
- CSUL（加利福尼亚大学萨克拉门托分校）网站，268
- CSV（逗号分隔值）文件，350, 352, 353
- 当前 index.html，305
- CustomLog 指令，48, 223–224, 227, 515
- 守护进程
    - 通用网关接口（CGI），5–10, 23, 328
    - identd，333
    - 标识守护进程，586
    - 内核日志（klogd），703
    - 针对 NFS（网络文件系统）优化，663
    - root，保护其免受杀死，708–701
- Danak PGP 公共服务器网站（www.pgp.net），14
- DATABASE 变量，205
- 日期日志文件标记，221
- DATE_GMT 变量，393
- date . isp 文件，487–488
- DATE_LOCAL 变量，393
- DAV 指令，156
    - 启用 DAV 提供程序，22
    - DavDepthInfinity 指令，156
    - DavGroup 指令，156
    - DavMimeTType 指令，156
- DB（MySQL）模块（光盘上），204, 721
    - DB_DRIVER 变量，205
    - DB_HOST 变量，205
- DBI 模块（光盘上），202, 628, 721
- DBM 文件，109, 112–114, 249
    - DB_PASSWORD 变量，205
    - DB_PORT 变量，205
    - DB_USER 变量，205
- DCOM（分布式 COM），423
- add 命令，568–601
- Default 指令，153
- Default . charset 指令，429
- Default icon 指令，134
- DefaultLanguage 指令，126
- default-Tmpl .html，308
- DefaultType 指令，47, 61
- dele te from tickets 命令，222
- DELETE 方法，启用/禁用，306
- 拒绝服务。参见 DOS
- Deny 指令，44, 192, 194
- describe 命令，197
- Devel-Syndump 模块，465
- Device 变量，681
- Digest-mods 模块，525, 526, 527
- 直接内存访问。参见 DMA
- 指令。另见特定指令
    - 容器上下文，57–58
    - 容器指令，43–45, 76–80
    - 核心，56
    - descend，31
    - 目录，应用于，57, 77–78
    - 禁用，337
    - FastCGI，414–416
    - 文件，应用于，57, 78–79
    - HTTP（超文本传输协议）方法，应用于，88–89
    - hot-perl 模块，mod_perl 模块脚本，458–459
    - override，允许，44, 59, 60, 86, 87, 388
    - 每目录上下文，56, 58–59
    - PHP：超文本预处理器，428–435
    - 服务器配置上下文，56
    - URI（统一资源标识符），应用于，57, 73–80
    - 虚拟主机配置指令，35, 55, 57, 80–83
- 目录。另见特定目录
    - 访问控制文件，47, 59–60
    - 别名，42–49, 145–146
    - 身份验证，335–356
    - 容器访问
        - 使用其进行目录访问限制，186–187, 209
    - 通过 AuthName 指令进行身份验证，87
    - 通过 AuthType 指令进行身份验证，87
    - 通过 mod_auth_mysql 模块进行身份验证，200–201
    - 通过多种身份验证方案进行身份验证，185
    - 通过 Require 指令进行身份验证，90–91
    - CGI（通用网关接口），在其中启用/禁用，66, 67
    - CGI（通用网关接口）程序目录，28
    - 容器，335–336
    - 容器。另见 43
    - 核心转储目录，92
    - 删除目录，27–28
    - 指令，应用于，57, 77–78
    - 文档树，映射到代理服务器，270
    - handler，为其分配/取消分配，127–128




# 索引 ♦ D

### 目录
- 隐藏，47
- 主目录，144–145, 252–253
- 索引，在其中显示替代文本，131–132, 133
- 索引，作为CGI（通用网关接口）脚本，131
- 索引，列设置，136
- 索引，其中的图标选项，133–134, 136
- 索引，在顶部/底部插入文件内容，135, 137
- 索引，在其中使文件类型不可见，135
- 索引，自动生成的选项，135–136
- 索引，在其中抑制文件描述显示，136
- 索引，抑制文件修改日期显示，136
- 索引，抑制HTML（超文本标记语言）前言显示，136
- 索引，使用PHP：Hypertext Preprocessor）页面作为索引，438
- 请求地址未找到时的索引显示，43, 66, 506–507
- 索引文件，默认，46
- 索引文件，指定，45–46
- 索引文件，未找到时的用户重定向，507
- 索引排序选项，137
- 语言默认，关联，126
- 链接，符号链接，42, 43–44, 66, 617
- MIME（多用途互联网邮件扩展）类型强制，127
- 模块，目录列表，105, 130–137
- **MySQL** 文件，178
- **NFS**（网络文件系统）目录，检查可用空间，666
- 权限，45, 509, 504–506
- 使用 **MultiViews** 功能跨多个目录搜索，252–255
- 安全性，141, 503–504, 688, 694–700
- **服务器** 目录结构，36–37, 41–43, 505–504
- **SSI**（服务器端包含），在其中启用/禁用，66, 67, 379, 381

### Tomcat
473, 475, 479–480, 481

### 虚拟
62

### Web
41–42, 44–46, 114, 144–145, 297

### Windows
- Apache 默认结构，573
- 目录结构，588–589

### <Directory>
作为容器，57, 58, 60

### <DirectoryIndex>
指令，45–46, 438, 507

### <DirectoryMatch>
容器，57, 78

### disable_functions
指令，429

### Disallow
指令，513–514

### 磁盘缓存模块
启用，22

### display_errors
指令，429

### _dist_files
31

### distribute
文件，664–665

### 区分名称字段
547–548

### 分布式组件对象模型
参见 **DCOM**

### DMA（直接内存访问）
601–602, 647

### DNS（域名服务）
- 缓存，本地，639
- 缓存过期时间，167
- **http://** 设置，614
- 查找，启用/禁用，48, 87–88
- 查找，最小化，614–615
- **mod_access** 模块
  - 磁盘考虑因素，88
  - 监控，639
  - 性能，优化，613–615
  - 记录，166, 167
  - 刷新率，167
  - 重试值，167
  - 轮询，613, 639–640
  - 辅助服务，第三方，167
- **序列号**，166
- **服务器**，BIND，166
- **服务器**，专用，638
- **服务器**，主机名，68, 166
- **服务器**，使用其进行负载均衡，613–614, 639–640
- **服务器**，异地，638
- **服务器**，主用，167
- **服务器**，冗余，638
- **服务器**，备用，167, 638

### SOA（起始地址记录）
- 信息，167
- 模板，使用其配置，175–176
- 生存时间值，167

### 基于用户名的地址解析
257

### 虚拟主机
为其设置，166–168, 175, 177

### Web 网络
637, 638–639

### 区域文件
166, 639

### 文档根目录
- 应用程序，与其保持分离，49, 503–504
- **asp** 子目录，466
- 默认，28
- 描述，41

### 文档根目录
- 安全，使用其设置，41, 45–46
- **image** 子目录，313
- **PHP**: Hypertext Preprocessor 包含文件，与其保持分离，434
- **PHP**: Hypertext Preprocessor 脚本操作，限制于，434
- **安全**，41, 49, 503, 512

### SSL（安全套接层）
- 服务器，557
- **UserDir** 指令，使用其设置，44, 144

### 相关变量
176, 241, 329

### Virtual DocumentRoot
指令，使用其设置，149

### Virtual DocumentRootIP
指令，使用其设置，150

### DOCUMENT 名称变量
393

### DOCUMENTROOT
指令，41–42, 61–62, 503

### DOCUMENT (ROOT) 变量
241, 329

### DOCUMENT_URI 变量
393

### 域符号（5）
- 正则表达式元字符，710
- 变量前缀，392–394
- 插入变量值，394

### 域名值
参见 **DNS**

### DOMAIN_CHAR $v 变量
529

### DOS（拒绝服务）
94.
另见 安全性

### 下载软件
- Apache，13–14, 18–19, 30, 499–500, 570
- Apache-SSL，558
- **Linux** 入侵检测 **系统**（LIDS），688
- **Linux** 内核源代码，652
- **mod_perl** 模块，455, 585
- **mod_ssl** 模块，551, 555
- **MySQL**，196, 429–424
- **Perl**，113
- **PHP**: Hypertext Preprocessor，424, 586
- **Tomcat**，472

### DSO（动态共享对象）模块
- 作为其加载，151, 152
- **MySQL** 模块，431
- 由其引起的 **性能** 拖慢，16
- **PHP**: Hypertext Preprocessor 模块 DSO 版本，426

## E

- `(backslash, lowercase e)` 正则表达式元字符，710
- `\E` `(backslash, uppercase E)` 正则表达式元字符，710
- `ezfssck` 实用工具，606, 651
- `Ezpgrops SourceForge.net` 网站，604, 648
- `ezfsgrops` 实用工具包，603–606, 648–651
- `ezfsgrops-1.19:0.src.rpm` 文件，604, 648
- `ezfsgrops-version .tar.gz` 文件，604, 648
- `echo` 命令，385
- `ECHO` 服务器，启用，22
- `Edit-as-Preference =Advanced (=)` Cookies 选项，211
- `EIDE`（增强型 IDE）硬盘，596, 598–599, 644. *另见* 硬盘。
- `Electronic Commerce on Internet` 网站，718
- `elf` 测试语句，396–397
- `elseif` 语句，396–397
- `e-mail`
  - 管理员地址设置，329, 571
  - `Cgi`（通用网关接口），在其中规范化，342–343
  - 地址中可接受的字符，353
  - 错误消息，通过电子邮件发送，41, 68
  - `LIDS`（Linux 入侵检测系统）设置，688, 691–692, 693, 703
  - `Tripwire` 设置，678, 685, 686–687
  - `virtual host` 主机服务器，168
  - `Web` 页面，通过电子邮件发送，364–369
- `EnableBullets` 指令，306
- `enable.cgi` 指令，429
- `EnableInput` 指令，306
- `encryption. 另见` 安全套接层（`SSL`）；安全性。
  - 非对称，546–547, 549
  - 证书，交叉链接，564
  - 为 `Apache-SSL` 创建证书，559–560
  - 证书区分名称，547–548
  - 证书文件路径，定义，557, 561
  - 证书颁发者，547, 550–551, 562
  - 证书密钥文件，557
  - 证书撤销列表（`CRL`），556
  - 证书签名请求，562, 563–564
  - 证书交易过程，548–550
  - `checksum`，501
  - `cookie`，208, 209, 210
  - `cryptographic` 密码设置，554, 557
  - `decryption`，546, 547, 548
  - `described`，546
  - `digest` 消息组件，548
  - `identity` 消息组件，548
  - `key, private`，546–547, 548, 562–563
  - `key, public`，546, 548, 550
  - `key` 文件，定义，557
  - `message` 认证代码（`MAC`）值，550
  - `password`，114, 116, 183, 201, 205
  - `random` 数据生成，560
  - `symmetric`，546, 549
  - `Tripwire`，677, 678, 681
  - `types`，201
  - `unpack`，183
  - `ENCRYPT()` 变量，205
  - `end_form()` 方法，525
  - `end_html()` 方法，347
  - `Engelhard, Ralf S.`，551
  - `environment` 变量。*另见* 特定变量。
    - 认证，在其中评估，193–194
    - 包含认证信息，333
    - `Cgi`（通用网关接口），在其中协同工作，106–107, 323, 326, 328–335
    - 包含字符集信息，330
    - 包含客户端软件信息，331
    - 使用客户端信息进行条件判断，106, 107
    - 包含连接信息，332
    - `custom`，107–109
    - `displaying`，585
    - `document` 根信息，包含，329
    - 包含站点管理员的 `e-mail` 地址，329
    - 包含 `encoding` 模式信息，330
    - `FastCGI`，在其中协同工作，415
    - `HTTP`（超文本传输协议），在其中协同工作，107–109, 333, 334
    - 包含 `identity` 守护进程信息，333
    - 包含 `IP`（互联网协议）地址信息，330, 332
    - 包含 `language` 信息，331
    - `length` 限制，326
    - `logging`，基于，224
    - `logging` 内容，225
    - 包含 `MIME`（多用途互联网邮件扩展）类型，330, 333–334
    - `PHP`（Hypertext Preprocessor），在其中协同工作，434
    - 包含 `port` 信息，332
    - `programs`，传递给外部程序，106–107
    - 包含 `query` 字符串信息，334
    - 包含 `remote` 主机信息，332
    - `removing`，108
    - 包含 `server` 名称，329, 330
    - 包含 `server` 协议，333
    - 与 `SSL`（安全套接层）相关，555, 558
    - `Tomcat`，471–472, 473, 475, 484, 485
    - 包含 `URI`（统一资源标识符）信息，331, 334–335
    - `URL`（统一资源定位符）重写规则，在，107, 224, 244, 246, 254–257
    - 包含 `username`，332–333
  - `Windows` 上的 `Apache` 安装，585
- `equals` 符号（`=`）
  - `comparison` 运算符，394, 396
  - `key-value` 对运算符，328
  - `URL`（统一资源定位符）重写条件模式前缀，247
- `equals` 符号，逗号（`=`），比较运算符，394



# 索引

### E

- 错误消息，218
- CGI（通用网关接口）脚本，63, 352, 353, 360, 361
- 自定义，62-63, 317
- 电子邮件发送，41, 68
- 表单处理消息，352, 353, 360, 361
- PHP：超文本预处理器消息，自定义，430
- PHP：超文本预处理器消息，存储在 `php_errormsg` 变量中，435
- SSI（服务器端包含）解析错误，382-384
- error_append_string 指令，430
- ErrorDocument 指令，62-63, 259, 317
- error_dir 指令，48, 230, 515
- error_log 指令，430
- error_log_file，577
- error_prepend_string 指令，430
- error_reporting 指令，430-431
- Ethernut 卡，602
- 配置访问，禁用，702
- 快速以太网，610-611
- 集线器，611
- 交换机，610, 611
- eval() 函数，518
- Eval Log 设施，577
- 感叹号 (!) CLF（通用日志格式）缺失服务器标记，227
- 条件语句前缀，63, 64
- 逻辑运算符，395-396
- 变量运算符，108
- 感叹号、等号 (!=) 比较运算符，394, 396
- exec() 函数，518-519, 529-530
- exec 命令，385-390, 540-541
- exec_cgi1.shtml 文件，387
- exec_cgi2.shtml 文件，388-389
- exec_cmd.shtml 文件，389-390
- Executable 指令，139-140
- ExpressType 指令，140-141
- ExpressDefault 指令，141
- export 命令，471
- exports 脚本，657
- exports 文件，656-657
- ext2 文件系统，优化，602-606, 647-650。另见 文件系统
- ExtendedStatus 指令，217
- extension 指令，431
- extensions_dir 指令，432
- ExternalAppJasc 指令，415-416
- ExtFilterDefine 指令，123
- ExtFilterOptions 指令，124

### F

- f（反斜杠，小写 f）正则表达式元字符，710
- FancyIndexing 指令，134
- FastCGI
  - 应用服务器，专用，403
  - 应用程序，分布式，401, 402-403
  - 应用程序，本地，414
  - 应用程序，加载，404, 416
  - 应用程序，远程，402-403, 404, 415-416
  - 缓存内存使用，401-402, 408
  - CGI（通用网关接口），从……迁移，408-413
  - CGI（通用网关接口）对比，399-401, 402
  - 连接持久性，399, 401, 402, 408
  - 数据库连接，633, 635
  - 描述，399
  - 指令，414-416
  - 环境变量，处理，415
  - 过滤，408
  - httpd.conf 设置，416-419
  - 初始化代码，406
  - 监听队列深度，414
  - mod_perl 模块，对比，633-635
  - 多线程，401-402, 407
  - 平台依赖性，400
  - 端口设置，415
  - 进程，401, 402, 414, 415
  - 编程语言依赖性，400
  - 响应处理，404-407
  - 请求循环，406-407
  - 重启延迟，414
  - 例程，406
  - 可扩展性，402-403
  - 脚本，403
  - Server API（应用程序接口）对比，400-401, 402
  - 套接字设置，415, 416
  - 软件开发工具包（光盘中），408-409
  - 速度，402
  - 实用工具，311, 614, 648
  - 变量，处理，328
  - Web 服务器角色，405-406
- FastCGI 网站，409, 417
- FastScriptIpdI 指令，415, 416
- FastScriptDir 请求处理程序，417
- FCGI 模块（光盘中），411-412, 721
- FCGI_AcceptIpdI，例程，406-407
- 内核进程已结束，1-3
- 文件句柄管理，155, 607-608
- 文件系统
  - 在内部进行修改前的备份，604, 649
  - 基准测试，654-656
  - 块预留，606, 650
  - 块大小，优化，603, 648
  - ext2 文件系统，优化，602-606, 647-650
  - ext3 文件系统，632
  - 文件不可变标志，保护，702
  - fsck 检查，605, 650
  - 日志记录系统，651-656
  - 内核对其中错误的响应，在控制中，655, 650
  - 挂载计数，605, 650
  - 挂载，635-654, 671
  - nfci，660
  - RAM（随机存取存储器），668-671
  - 基于内存的，668-671
  - 重建，603, 648
  - 修复，606, 651
  - 安全性，687
  - 基于事务的，651
  - 卸载，659
- 文件传输协议代理服务器
  - 另见 FTP 代理服务器
  - file_mx 命令，636
  - files> 容器，57, 58, 78-79
  - filesMatch() 容器，57, 79
  - files，I/O（输入/输出），9, 70, 118-121, 121-122, 124, 408
  - FindProxyForURL() 方法，286
  - FindProxyForURL 函数，284-287, 288, 290
  - 防火墙，275, 497, 509-510, 702。另见 安全性
  - Fire Channel 磁盘，596。另见 硬盘
  - flash 命令，391
  - flush() 函数，432
  - flush privileges 命令，189
  - followSymbolics 指令，617
  - fontsici.cgi 脚本，411
  - fontsiz.fcg! 脚本，413
  - foo|bar 正则表达式元字符，710

### G

- ForceType 指令，127, 417
- foreach 命令，346
- 使用 CGI（通用网关接口）进行表单处理
  - 配置文件，网关，352, 356
  - 配置文件，在其中定位 Web 表单，352, 353, 356-357, 360
  - 数据存储，350, 352, 353
  - 错误消息生成，352, 353, 360, 361
  - 管理，集中化，350, 364
  - 模块加载，352, 353, 355-356
  - 使用单个脚本处理多个表单，349
  - 对象创建，352, 353, 356
  - 模板，356, 357-358, 360, 362
  - 感谢消息显示，352, 358, 361, 362-363
  - 用户数据验证，352, 353, 358-360, 361
  - 用户重定向，361-362
- 通过 PHP：超文本预处理器进行表单处理，441-444
- form.php 脚本，442
- formmail，382, 384, 385, 393
- formmail.pl 文件（光盘中），382, 384
- fractal.net 网站，178, 620
- fsck 实用工具，605, 650
- fsize 命令，391
- FTP（文件传输协议）代理服务器，269, 623
- 函数
  - crypt( )，114, 116, 184
  - eval( )，518
  - exec( )，518-519, 529-530
  - FindFirstOrDir( )，281-287, 288-292
  - flush( )，432
  - include( )，432, 439-441, 450
  - include_once( )，440-441
  - isset( )，452
  - join( )，347
  - lcs( )，346, 347
  - rcmd 函数调用，664
  - require( )，432, 441
  - require_once( )，441
  - session_destroy( )，447
  - session_register( )，444, 446
  - session_start( )，444-445, 446
  - show_challenge( )，453
  - split( )，348
  - system( )，518-519, 529-530
  - tolower( )，248
  - toupper( )，248
  - ucfirst( )，346

### H

- GATEWAY_INTERFACE 变量，329
- GDBM 文件，112-113
- GET 请求，72, 122, 323-326, 327
- GID（组 ID）名称，40
- GPL（GNU 通用许可协议），10
- grant 命令，198-199
- 大于号 ( > ) 运算符，394
- greetings.pl 脚本，344-345, 503
- grep 实用工具，50, 51
- group 指令，40, 53, 342-503
- groupanim 命令，504
- GROUP_TABLE 变量，206
- 在线增长，681
- GUI（图形用户界面），6, 581
  - 多扇区模式，600-601, 646
  - NFS（网络文件系统）服务器，共享驱动器空间，656-664
  - 性能，优化，598-602, 646-647
  - RAID（独立磁盘冗余阵列），598, 642, 659
  - 可靠性，597
  - SAN（存储区域网络），598, 643
  - SCSI（小型计算机系统接口），596, 597, 598, 643-644
  - 设置，检查，599-600
  - 类型，选择，597-598
  - UltraDMA 模式，647
  - UltraMA55，596
  - Web 网络，为……配置，643-647
  - Web 服务器，598
- HARD_SERVER_LIMIT 设置，24-26
- HARD_THREAD_LIMIT 设置，24-26
- httpd_limit，599, 602, 644-647
- Header: 3.9, tar.gz 文件，358
- header( ) 方法，247, 525
- HeaderName 指令，125
- help.php 脚本，436
- 十六进制数，328
- hidden-mus，611
- highperformance.conf 文件，29, 576
- hiperfame-sto 配置文件，29
- Apache 历史，5
- host，虚拟，另见 虚拟主机
- 主机日志文件，221
- HostMinConnects 指令，48, 87-88, 236, 614
- .htaccess 文件，47, 59, 187-188, 508-509
- httpd 实用工具，28
- htdocs 目录，28。另见 文档根目录指令
- HTML（超文本标记语言）
  - 通过 SSI（服务器端包含）创建锚点，388-389
  - CGI（通用网关接口）脚本，通过……创建上下文，315, 347-349, 525
  - CGI（通用网关接口）脚本，315, 347-349, 525
  - 目录索引 HTML，681, 685, 690, 691
  - 表单，326
  - 隐藏标签，安全考虑，520-527
  - INPUT 实体，327
  - JSP（Java 服务器页面），嵌入在……中，488
  - PHP：超文本预处理器
    - 代码，嵌入在 HTML 文件中，422, 427
    - 超文本预处理器页面，在其中包含 HTML 文件，439-441
  - 标准，制定，312
  - HTTP::Template 模块（光盘中），356, 321
- htpasswd 实用工具，29, 184, 186
- HTTP（超文本协议）
  - 身份验证，6, 29, 87, 182-183, 501
  - 使用虚拟主机时的浏览器支持考虑，161
  - CGI（通用网关接口）处理程序，228
  - cookies，323
  - 数据编码方案，328
  - DELETE 方法，启用/禁用，306
  - 指令，应用于，88-89
  - 禁用，22
  - 文档过期，139-141
  - 环境变量，处理，107-109, 333, 334
  - GET 请求，72, 122, 323-326, 327
  - metaheader 选项，141-142
  - PHP：超文本预处理器，在其中抑制内容类型头，436
  - POST 请求，72, 122, 194, 326-327
  - PUT 方法用于 intranet Web 发布，308-310
  - 请求，与 CGI（通用网关接口）脚本关联，122
  - 请求，按类型阻止身份验证，194
  - 请求，CGI（通用网关接口）处理，122, 333, 334
  - 请求，基于此的自定义环境变量，107-109
  - 请求，通过硬件负载均衡器分发，640-642
  - 请求，通过轮询 DNS（域名服务）分发，639-640
  - 请求，其中的表达式匹配，107-109
  - 请求，限制，89-90
  - 请求，mage tokens for，108
  - 请求，magic ID，106, 109
  - 响应头，处理，23, 137-142, 244-245, 246
  - 状态代码，147, 705-708
  - Tomcat，禁用默认 HTTP 文件服务，483-484
  - URL（统一资源定位符）重写规则，在响应头中处理，244-245, 246, 262, 264
  - User-Agent 头，107-108
  - 版本 1.1 支持，5-6
- HTTP_ACCEPT 变量，330
- HTTP_ACCEPT_CHARSET 变量，330
- HTTP_ACCEPT_ENCODING 变量，330
- HTTP_ACCEPT_LANGUAGE 变量，331
- httpd-analyze 日志分析工具，323
- HTTP_CONNECTION 变量，332
- HTTP_COOKIE 变量，241
- httpd.script，59, 51, 52, 63, 69
- httpd_2.0.4.tar.gz 文件，18
- httpd_2.3b3.win32.exe 文件，18
- httpd_100.conf 文件，164
- httpd_101.conf 文件，165
- httpd_3030.conf 文件，632
- httpd.conf 文件，另见特定指令
  - Apache:AuthnBBi 设置，202
  - Apache:SSL 设置，560-561
  - CGI（通用网关接口）设置，329, 336, 337, 338, 356
  - 配置部分，35-36
  - 容器作用域条目，58
  - 定义，6, 31-35
  - DNS（域名服务）设置，614
  - 编辑，6
  - FastCGI 设置，416-419
  - hassock-based 身份验证设置，187
  - ISAPI（Internet 服务器 API）扩展设置，587-588
  - 仅限成员 Web 页面设置，186
  - mod_asis 设置，138
  - mod_auth_mysql 设置，200
  - mod_backhand 设置，626
  - mod_cache 设置，620
  - mod_perl 设置，456-457, 461, 464-465, 467, 585
  - mod_url 设置，309-310
  - mod_sql 设置，556-558
  - mod_status 设置，217-218
  - 路径分隔符字符，579
  - PHP：超文本预处理器设置，426, 427-428, 451, 587
  - 代理服务器设置，270, 275, 632
  - pub-based 发布设置，307-308
  - 部分分隔符，35
  - SetHandler 设置，457
  - SSI（服务器端包含）设置，379
  - SSL（安全套接字层）设置，556-558
  - Tomcat 设置，479-482, 484
  - URL（统一资源定位符）重写设置，254
  - 虚拟主机设置，160-161, 163-164, 170-171, 173-175, 177
  - Windows 上的 Apache 安装，577, 578, 579, 580
- HTTPD::ApacheAdmin 模块，204
- httpd-studio 文件，29
- httpd.template 文件，175
- HTTPD::Tools 模块，204
- HTTPD::UserAdmin 模块，204
- httpd_version -win32-no-src -number，581
- HTTP_FORWARDED 变量，241
- HTTP_HOST 变量，241, 330
- HTTP_PROXY_CONNECTION 变量，241
- HTTP_PROXY_VARIABLE，241, 331
- HTTPS（安全超文本传输协议），550, 555, 556, 565
- httpsd.conf 文件，560
- httpd.pem 证书，560
- HTTP_USER_AGENT 变量，241, 331
- hub，Ehrner，611
- Hudson, Tim J.，551
- Hugh Minda 联系方式，722
- 超文本传输协议。另见 HTTP
- 连字符 (-) 逻辑空标记，221



## ibiblio 网站
- http://metalab.unc.edu/pub/Linux/system/hardware, 598

## IBM DB2 数据库服务器
- 202

## IBM JFS 文件系统
- 652

## 图标
- 在目录列表中关联文件, 133–134

## icons 指令
- 28

## IDE (Integrated Disk Electronics, 集成磁盘电子) 硬盘
- 596, 598–599. 另见 硬盘

## ident(4) 文件令牌
- 221

## ident 守护进程
- 88, 333

## IdentityCheck 指令
- 88, 225, 333

## IEEE 802.11 无线标准
- 346–348, 352–354

## IEEE 1394
- 另见 火线接口

## ieeefile 命令
- 662–663

## ifdef 指令
- 439

## if 语句
- 389–390, 395

## ifconfig 命令
- 662–663

## ifndef 指令
- 439, 441, 450

## in 关键字
- 400

## include_path 指令
- 378

## include(4) 文件
- 65, 170–171, 391–392

## include 指令
- 27

## 包含文件
- 432, 434, 439–441, 451. 另见 PHP: 超文本预处理器

## include_variables
- 385, 386, 389, 393

## include_once( ) 函数
- 440–441

## index.html
- 305

## index.php 脚本
- 437

## index(.htaccess
- 609

## init 方法
- 630

## insert into 命令
- 197

## install.cfg 文件
- 675–677

## 在 Unix/Linux 上安装 Apache
- 来自二进制包, 13–14, 30, 498, 609
- 编译, 26–29
- 调试, 开启, 21
- 安装软件, 18–19
- 许可协议, 10–12
- 日志文件, 23
- 来自源代码, 10–29
- 系统要求, 14–18

## 在 Windows 上安装 Apache
- 二进制安装, 570–574
- 自定义安装, 572
- 目录, 默认, 573
- 域名, 571
- 下载软件, 570
- 功能, 选择, 573
- 许可协议, 570–571
- 服务器名称, 571
- 系统要求, 569–570
- Windows 2000 高级服务器, 569–570

## 安装 Apache/SSL
- 585–589

## 安装自定义内核
- 667

## 安装 LIDS (Linux 入侵检测系统)
- 691–693

## 安装 mod_perl 模块
- 455–456, 585

## 安装 mod_ssl 模块
- 555

## 安装 PHP: 超文本预处理器
- 424–426

## 安装 Tmcat
- 471–473

## 集成 Tripwire
- 674–678

## 集成磁盘电子硬盘
- 另见 IDE 硬盘

## Internet Explorer 管理员套件
- 另见 IEAK

## Internet Explorer 代理设置
- 280–281

## Internet FAQ 存档网站
- 502

## Internet News 网站
- 718

## InterNIC 网站
- 516, 519

## 入侵者检测
- 另见 LIDS (Linux 入侵检测系统); 安全性

## i/o (输入, 输出)
- 过滤器, 9, 70, 118–121, 122–124, 498
- 硬盘支持, 启用 32 位, 601, 646–647
- NFS (网络文件系统) 支持, 659
- 通过最小化请求进行性能优化, 616–617
- 安全防止未授权访问, 688

## IP (互联网协议)
- 通过 IP 地址进行身份验证, 109, 190–194
- 环境变量, 688
- 地址, 限制, 330, 332
- 路由器地址限制, 498
- 虚拟主机, 基于 IP, 161, 162–163
- 虚拟主机寻址, 83, 161–162

## ipfrag_high_thresh 命令
- 664

## ipfrag_low_thresh 命令
- 664

## ISAPI (互联网服务器应用程序接口)
- 扩展, 587–588
- ISAPIAppendLogFilters 指令, 588
- ISAPIAppendLogToQuery 指令, 588
- ISAPILogFileSupported 指令, 588
- ISAPIReadLogBufferSize 指令, 587–588

## ISP 买家指南网站
- 718

## ISP (互联网服务提供商)
- 封锁, 516

## isset( ) 函数
- 452

## is.subset 变量
- 242

## Jakarta 项目网站
- 713

## Java 安全管理器
- 477–479

## Java Server Pages
- 另见 JSP

## Java 服务器
- 另见 Tomcat
- 与 CGI (通用网关接口) 脚本相比, 469, 470
- 数据库并发性, 470
- 描述, 469
- 与 JSP (Java Server Pages) 相比, 470
- 与 JVM (Java 虚拟机) 的交互, 470

## Java  servlets
- 与 mod_perl 相比, 470
- 开销, 470
- 路径, 490
- 平台无关性, 470
- 线程创建, 469
- Tomcat, 为此配置, 479–483
- Tomcat, 通过其进行交互, 469
- Tomcat, 通过其运行, 485–491
- 编写, 471

## java -version 命令
- 472

## Java 虚拟机
- 另见 JVM

## JAVA_HOME 变量
- 471, 484, 485

## java.io.FilePermission
- 权限类型, 478

## java.lang.reflect
- ReflectPermission 权限类型, 478

## java.lang.RuntimePermission
- 权限类型, 478

## java.net.NetPermission
- 权限类型, 478

## java.net.SocketPermission
- 权限类型, 478

## JavaScript
- 弹出窗口, 384
- 代理自动配置, 281

## javascript 变量
- 108

## java.security.AllPermission
- 权限类型, 478

## java.security.SecurityPermission
- 权限类型, 478

## java.util.PropertyPermission
- 权限类型, 478

## JDBC (Java 数据库连接)
- 470

## JDK (Java 开发套件)
- 471

## JFS 文件系统
- 652. 另见 文件系统

## JFS 开源项目网站
- 652

## jKoolFile 指令
- 480

## jKMount 指令
- 480–481

## jKMoreFile 指令
- 480

## JNI (Java 本地接口)
- 475

## jni 工作线程类型
- 475

## JRE (Java 运行时环境)
- 469, 471

## .jsp 文件
- 470

## JSP (Java Server Pages)
- 另见 Tomcat
- API (应用程序编程接口), 470
- 与 ASP (活动服务器页面) 相比, 470
- date.jsp, 487–488
- HTML (超文本标记语言) 代码, 嵌入其中, 488
- 与 Java servlets 相比, 470
- 与 PHP: 超文本预处理器相比, 470
- 支持, 6
- Tomcat, 为此配置, 479–483
- Tomcat, 通过其进行交互, 470
- Tomcat, 通过其运行, 485–491
- JVM (Java 虚拟机), 469, 470, 477

## K

## KeepAlive 指令
- 38, 73, 632

## KeepAliveTimeout 指令
- 38, 73

## 内核
- 绑定, 653, 688, 690
- 配置程序, 689
- 自定义, 配置, 607
- 自定义, 安装, 607
- LIDS (Linux 入侵检测系统), 在启动周期结束时密封, 693
- LIDS (Linux 入侵检测系统), 为其设置, 688–691
- Linux 系统, 控制到内核的错误, 文件系统错误, 605, 630
- Linux 内核, 优化, 607–608
- Linux 内核, Red Hat 对比供应商提供, 606–607
- Linux 内核, 源代码, 下载, 682
- 日志守护进程, 703
- 重新编译, 689
- Sysctl 支持, 689
- 版本, 607, 691

## kill 命令
- 52, 53, 657

## killall 实用工具
- 657

## klogd 日志守护进程
- 703

## L

## \l (反斜杠, 小写 l) 正则表达式元字符
- 710

## \L (反斜杠, 大写 L) 正则表达式元字符
- 710

## 语言
- 内容协商, 129
- 默认, 设置, 48, 126
- 目录, 关联默认语言, 126
- 环境变量, 331
- 文件扩展名, 映射到, 125–126
- Multiviews 搜索, 在其中设置语言优先级, 129

## LanguagePriority 指令
- 49, 129

## LAST_MODIFIED 变量
- 393

## Laure, Ben
- 720

## lb 工作线程类型
- 475

## \l( \l ( ) 函数
- 346

## 小于号, 等于号 (<=) 比较运算符
- 394

## 小于号 (<) 比较运算符
- 394

## lib 目录
- 27

## libexec 目录
- 479–480

## 库
- DB 库, 116
- JVM (Java 虚拟机) 库路径, 477
- SSL (安全套接字层) 库安装, 23
- SSL (安全套接字层) 库共享, 553
- SSLEay, 551

## 授权
- 10–12, 570–571

## LIDS (Linux 入侵检测系统)
- 另见 安全性
- ACL (访问控制列表), 与其配合使用, 693–694, 695
- 启动选项, 690
- 能力规则, 693, 696–699
- 编译, 691–693
- 安全警报时断开控制台, 690, 703
- 保护免受 root 用户终止守护进程, 700–701
- 目录保护, 688, 694–700
- 下载, 688
- 服务器统计数据清除, 禁用, 702
- 电子邮件设置, 688, 691–692, 693, 703
- 文件不可变标志, 保护, 702
- 文件保护, 688, 694–700
- 节点/网关成员更新, 691
- 安装, 691–693
- 入侵者检测, 响应, 703
- I/O (输入/输出) 操作, 防止未授权, 688
- 内核, 在启动周期结束时密封, 693
- 内核设置, 688–691
- lilo.conf 设置, 691
- 日志文件泛滥, 避免其, 690
- 日志文件保护, 688
- 多播, 禁用, 702

- 网络管理任务, 禁用, 702
- 密码, 691
- 权限分配, 通过其, 694–695
- 端口扫描器检测, 688, 690, 702
- 进程隐藏, 701
- 进程原始设备访问, 禁用, 701
- 进程终止, 防止未授权, 688
- 混杂模式, 禁用, 702
- 保护, 默认, 692
- 寄存器读/写设置更改, 禁用, 702
- root 用户, 保护免受其修改, 688, 706–707
- 路由表更改, 禁用, 702
- 套接字任意进程所有权, 禁用, 702
- 套接字调试更改, 禁用, 702
- 源代码发行版, 688
- 停止, 693
- 切换保护选项, 690
- TQS (服务类型) 更改, 禁用, 702
- 版本号, 688

- lsnl.0.5.2.4.1.tar.gz 文件, 689
- listsidm 程序, 691–692, 693–694
- lids.cfg 文件, 693, 699–700
- lids.conf 文件, 693
- lids.net 文件, 691, 693
- lids.pvf 文件, 691
- fileo 命令, 685, 689
- file.conf 文件, 653, 669

## <Limit> 容器
- 58, 59, 88–89

## <LimitExcept> 容器
- 89

## LimitRequestBody 指令
- 89
- 89–90
- 90

## LimitRequestField 指令
- 90

## limits.conf 文件
- 698

## LinkExchange 网站
- 318

## 链接, 符号链接
- 42, 43–44, 66, 617

## Linux 入侵检测系统
- 另见 LIDS

## Linux 内核存档网站
- 607, 652

## linux single 命令
- 599

## Listen 指令
- 93, 164

## ListenBacklog 指令
- 94

## in 命令
- 52

## 负载均衡
- DNS (域名服务) 服务器, 通过其, 613–614, 639–640
- 硬件平衡器, 通过其, 614, 615, 640–642
- 轮询, 475, 476, 613–614, 639–640
- Tomcat, 475, 476
- Web 网络, 638, 639–642, 671–672

## Load 指令
- 152

## LoadModule 指令
- 152, 480

## Local 指令
- 614, 615, 640

## LocalSystem 账户
- 576

## locate 命令
- 204

## <Location> 容器
- 57, 58

## <LocationMatch> 容器
- 57, 80

## LockFile 指令
- 94

## log_errors 指令
- 432

## logFormat 指令
- 222, 223

## 日志记录
- 访问日志, 48, 53, 111
- 使用第三方实用工具进行分析, 232–234
- CFL (通用日志格式), 221, 227
- 条件日志, 224, 226
- 配置, 禁用, 222
- cookie 信息, 224, 225, 228–229
- cron 作业, 通过其运行, 220, 234, 237
- 自定义日志, 224–227
- 数据字段, 222
- 相关指令, 83–86
- 磁盘专用, 用于日志, 48
- 环境变量内容, 225
- 错误日志, 54, 230–232, 501, 503, 557
- 导出日志信息, 223–224
- 文件系统, 来自日志, 651
- 格式, 默认, 48, 223
- 安装日志, 23
- 简介, 7
- 入侵者检测, 日志, 516, 703
- IP (互联网协议) 地址解析, 29, 236–237
- ISAPI (互联网服务器应用程序接口) 扩展, 588
- 内核日志守护进程, 703
- 级别, 指定, 48, 84–85, 231, 250
- LIDS (Linux 入侵检测系统), 避免其泛滥, 690
- 日志文件, 大小考量, 17
- 缺失日志, 50
- modFileNope 内容, 226
- 负责模块, 105, 143, 221
- 多个日志文件, 配合使用, 227–228
- 命名日志文件, 222–223
- PHP: 超文本预处理器, 430, 625
- 轮转日志文件, 29, 234–236
- 保护日志文件, 48, 503, 515–517, 688
- 安全性, 其中的作用, 501
- 服务器, 代理, 266
- 服务器日志, 指定, 48
- 安全性, 其中的作用, 501
- Squid 代理缓存服务器, 624, 625
- SSL (安全套接字层), 556
- 令牌, 221
- Tomcat, 480, 490
- URL (统一资源定位器) 重写, 249–250, 254
- 用户名, 远程, 88
- 查看, 53
- Wusago 日志分析工具, 233, 515

## 逻辑运算符
- 395–396

## 日志文件安全性
- 687

## logi 脚本
- 211

## LogLevel 指令
- 48, 84–85

## logresolve 实用工具
- 29, 236

## logresolaver.c 脚本
- 236–237

## logrotate 实用工具
- 234–236

## logs 目录
- 28

## log_server_status 脚本
- 220

## log stats.txt 文件
- 237

## ls 实用工具
- 390

## lstat (系统调用)
- 617

## LwP 模块 (该 CD)
- 721

## MAC (消息认证码)
- 550

## magic 文件
- 29, 128

## magic_quotes_gpc 指令
- 432–433

## magic_quotes_runtime 指令
- 433

## 邮件列表, Apache 相关
- 717

## make b2make 模块
- 653, 668, 690

## make 命令
- 26, 554

## make dep 命令
- 668

## make depdnd 模块
- 690

## make distall 命令
- 27, 554

## make menconfi 命令
- 689

## make modules.conf
- 653, 668, 690

## make modules.install 命令
- 653, 668, 690




# 索引

- make release 命令，675
- make xconfig 命令，689
- mapcache 脚本（光盘上），304–305
- make ramsfs 脚本，670
- Makefile 脚本，175–178, 666
- manage user pl 命令，206–208
- manage users pl 脚本，202
- MaxClients 指令，39, 94–95
- max_execution_time 指令，433
- Maximum Transmission Unit. 参见 MTU
- MaxKeepAliveRequests 指令，38, 73
- MaxRequestPerChild 指令，39, 95, 580
- MaxRepeaServers 指令，102
- MaxRepeaThreads 指令，39, 95
- MaxRepeaPerChild 指令，100
- MD5（消息摘要）校验和使用，501, 502
  - 创建，28, 60–61
  - Digest 认证使用，109
  - ENCRYPTION 变量，205
  - 隐藏数据，使用保护，520–524
- MAC（消息认证码）
  - 值生成，550
  - 由此造成的性能拖累，60–61
  - 用户代码，502
  - 更新，28
- mininfo 命令，660
- 内存管理
  - 缓存，分配文件类型，620–621
  - 缓存，检查硬盘子系统，600, 645
  - 缓存，数据库连接，628–630
  - 缓存，DNS（域名服务），167, 639
  - 缓存，启用，21, 22, 129
  - 缓存，FastCGI，401–402, 408
  - 缓存，文件句柄，155, 607–608
  - 缓存，MySQL，179
  - 缓存，负缓存，625–626
  - 缓存，优化速度，600, 620–627
  - 缓存，代理服务器选项，209, 272–276, 278–279, 621–626
  - 缓存，Squid 代理缓存服务器，624–625
  - 缓存，SSL（安全套接字层）设置，556, 561
  - 缓存，生存时间，556, 561, 625
  - 查看缓存统计信息，621
  - CGI（通用网关接口）脚本，74, 409
  - 显示总可用内存，660
  - DMA（直接内存访问），601–602
  - GAW（随机存取存储器）-基于，668–671
  - 监控，17, 594
  - PHP: 超文本预处理器，423, 433–434
  - 控制进程内存使用，39, 74, 608
  - TCP（传输控制协议）发送缓冲区大小，96
- memory c 脚本，410
- memory limit 指令，433
- message authentication code. 参见 MAC
- message digest. 参见 MD5
- Meta dfiles 指令，142
- MetaFiles 指令，141
- META INFO 指令，481
- Meta suffix 指令，142
- 方法
  - backend()，526
  - DELETE，306
  - end_form()，525
  - end_html()，347
  - find_form()，525
  - handler()，460–461, 462, 464, 525
  - header()，347, 525
  - init()，630
  - mysql fetch row()，449
  - p()，347, 348
  - param()，345, 464
  - read_file，387
  - send_file，460
  - start_form()，525
  - start_html()，347, 348–349, 525
  - submit()，525
  - text field()，525
- MIME（多用途互联网邮件扩展）
  - CGI（通用网关接口），在其中获取类型，330
  - CGI（通用网关接口）脚本，与类型关联，118–124
  - 配置文件，29, 47, 128
  - 使用类型进行内容协商，129
  - 指令，强制使用类型，127
  - 启用/禁用，22
  - 相关环境变量，330, 333–334
  - 文件内容，通过检查分配类型，128
  - 文件扩展名，为定义处理器，125
  - 文件扩展名，为未知定义类型，47, 61
  - 文件扩展名，无论扩展名如何强制类型，127
  - 文件扩展名，映射字符集，124–125
  - 文件扩展名，映射编码方案，125
  - 文件扩展名，映射语言，125–126
  - 图标，分配给类型，133–134
  - 魔术文件，29, 128
  - URL（统一资源定位符）重写，强制类型，245
- MIME Lite 模块（光盘上），721
- MIME Lite: HTML 模块（光盘上），369, 721
- Mime MagicFile 指令，128
- MimeMap pl 脚本，365–368
- MIME 类型文件，29, 47
- MimeServers 指令，104
- MimeSign(s) 指令，39, 95–96
- minus sign ( ) 指令开关，66, 67
- 通过 RAID（廉价磁盘冗余阵列）镜像硬盘，642
  - 网站，278, 311
- 缺失的 php 脚本，441
- mk dir 命令，45
- mkfile 实用工具，655
- mkscripts 命令，654
- mmap 系统调用，155
- MMapFile 指令，155
- mod access 模块，88, 109
- mod actions 模块，118
- mod aliases 模块，14, 145
- mod as 模块，137, 138
- mod auth 模块，109, 184–190, 195
- mod auth anon 模块，109, 110, 112–114, 116
- mod auth dbm 模块，109, 110, 116
- mod auth digest 模块，109
- mod_auth_digest 模块，195–202
- mod autoindex 模块，131
- mod backhand 模块，626–627
- mod backhand 网站，626–627
- mod cern meta 模块，137, 141
- mod cgi 模块，6, 118
- mod_cgid 模块，9
- mod_dav 模块，155–156
- mod_dir 模块，62, 130–131
- mod_env 模块，106
- mod_expgml 模块，151
- mod_expires 模块，137, 139
- mod_ext_filter 模块，118, 122–123
- mod_fastcgi 模块，413–414, 417
- mod_fcgi 模块，620–621
- mod_file_cache 模块，151, 155
- mod_headers 模块，137, 138–139
- modified_simple.fmpl 文件，443
- modified_form.php 脚本，443–444
- mod_imap 模块，151, 152–153
- mod_include 模块，118, 378–379
- mod_info 模块，143, 214–216
- mod_info.c 文件，214, 215
- mod_isapi 模块，151, 587–588
- mod_j 模块，469, 472–473
- mod_jj.conf-auto 文件，479–480, 490
- mod_jj.x 模块，480
- mod_jserv 模块，469, 472
- mod_log_config 模块，143, 221–222
- mod_mime 模块，124
- mod_mime_magic 模块，29, 47–48, 124, 128
- mod_negotiation 模块，124, 128–129
- mod_perl 模块。另参见 Perl。
  - Apache::AuthDBI 模块，202
  - 用于认证，202
  - API（应用程序接口），作为，458
  - ASP（Active Server Page）
    - 使用实现，466–467
  - CGI（通用网关接口）脚本，
    - 使用运行，456–457
  - CGI.pm 模块，编写
    - 使用 mod_perl 脚本，462–464
  - 子进程，461, 631–633
  - 代码，评估安全性，460
  - 编译，455–456
  - 定义常量，460
  - 计数器，460, 461–462
  - 数据库连接，628–630, 633–635
  - 下载，455, 585
  - 与 FastCGI 的对比，633–635
  - 处理器方法，460–461, 462, 464
  - httpd_conf 设置，455–457, 461, 464–465, 467, 585
  - 安装，455–456, 585
  - 与 Java Servlets 的对比，470
  - 内存管理，463–466
  - 包名，458
  - 优化性能，627–633
  - 预加载，627–628
  - 访问查询字符串信息，464
  - 请求对象，462, 464
  - 脚本编写者，458–464
  - 音频分发（光盘上），721
  - 优化速度，627–633
  - 自动虚拟主机配置，使用，171–175
  - 在 Windows 下运行 mod_perl 脚本，585–586
- mod_perl，变量，在其下运行，585–586
- mod_php 模块，6, 421, 427
- mod_proxy 模块，151, 268, 275, 622
- mod_put 模块，306–307, 309–310
- mod_put.tar.gz 文件，307
- mod_rewrite 模块。另参见 URL（统一资源定位符）重写规则
  - mod_rewrite 模块，144, 249–249
- mod_selectv 模块，106, 107, 224
- mod_so 模块，151, 472
- mod_spelling 模块，144, 148–149
- mod_ssl 模块。另参见 SSL（安全套接字层）
  - 编译，555
  - 启用，557
  - 启用/禁用，551, 555
  - 安装，555
  - 介绍，7
  - 与 OpenSSL 的关系，543
  - 所需的 OpenSSL 包，552
  - 作为共享模块运行，556
- mod_sl 模块，226
- mod_Web Project 网站，551, 555
- mod_status 模块，143, 216–220
- ModuleName 模块，226

### 模块

- 模块，在其中构建，609
- Apache 模块，105, 109–117
  - 列出活跃的，76, 216
- Apache 可执行文件内置，713
- 认证模块，105, 109–118
- 条件测试，64
- 内容类型配置模块，105, 124–129
- CPAN（Comprehensive Perl Archive Network）模块，204, 343, 356, 457
- 自定义，测试可用性，64
- 目录列表面模块，105, 130–137
- 动态内容生成模块，105, 117, 377–378
- 扩展相关，105, 106–109
- 扩展模块，28, 431
- 来自其他模块的输入，9
- 动态加载，75–76
- 作为 DSO（Dynamic Shared Object）加载，151, 152
- 定位，204
- 监控配置信息，215–216
- 加载 Perl 模块，460, 461, 586
- Perl 模块，位置，458–459
- Perl 模块，内存管理，463–466
- Perl 模块，预加载，464–465, 627–628
- 编写 PHP 模块，458–464
- PHP：超文本预处理器，使用扩展模块，431
- PHP：超文本预处理器模块，构建为 DSO（Dynamic Shared Object）版本，426
- PHP：超文本预处理器模块，构建为静态，425
- PHP：超文本预处理器模块，构建为模块，定位，指定，432
- 响应头模块，105, 137–142
- 在下载源选择中的安全性，500
- 服务器信息模块，105, 143
- 服务器日志模块，105, 143
- 启用共享，21
- 来源，543, 557, 580
- URL（统一资源定位符）映射模块，105, 144–151
- mod_unique_id 模块，106, 109
- mod_userdir 模块，144–145
- mod_usertrack 模块，143, 228–229
- mod_v2h.tar.gz 文件，178
- mod_v2h 模块，178–179





## M
- mod_ghost_alias 模块，144, 149
- 监控。**另请参阅**日志记录
- DNS（域名服务），639
- 错误日志，501
- 模块配置
  - 数据包，信息，215–216
  - 端口，220, 226
  - 进程，217, 226
  - 服务器配置
    - 信息，213, 214–216
    - 服务器状态，7, 99, 213, 216–220, 510
    - 线程，23
    - Web，源自，214–215
- mount 命令，654, 671
- mount 实用工具，657
- MPM（多处理模块）
  - **另请参阅**进程
  - 描述，7
  - 相关指令，38–39
  - 硬性限制，24–26
  - perchild，8
  - prefork，7, 8, 102–104
  - 要求，设置最大并发数，39
  - ScoreBoardFile 指令，37–38, 85–86
  - 线程，8
  - threaded（线程化），8
  - 最小值/最大值
    - 空闲数量，39, 95–96
    - 线程，最小值/最大值
      - 生成数量，34, 39
  - winnt，8, 9, 101–102, 580
- mpmdefault，3, 生命周期，95
- MTU（最大传输单元），662–663
- 组播，禁用，702
- Multipurpose Internet Mail Extension（多用途互联网邮件扩展）。**另请参阅 MIME**
- 扩展，**另请参阅 MIME**
- MultiViews 搜索，129, 255–256
- MySQL
  - 使用 MySQL 数据库服务器进行身份验证，196–202
  - 二进制发行版，196, 423–424
  - CD-ROM，随本书附带，包含在，720
  - Cookies，处理，212
  - 下载，196, 423–424
  - DSO（动态共享对象）模块，431
  - 文件位置，178
  - 密码，179
  - PHP：Hypertext Preprocessor（超文本预处理器），结合使用，423–424, 425, 431, 448–454
  - 端口，179
  - 权限，190
  - 使用其配置虚拟主机，178–179
- mysql 数据库驱动，205
- MySQL 网站，1, 196–197, mysql_web，com，196
- mysql_connect() 函数，449
- mysql_fetch_row() 方法，449
- mysql_query() 函数，449
- mysql_select_db() 函数，449

## N
- \n（反斜杠，小写 n）正则表达式元字符，710
- 命名模板文件，175
- NameVirtualHost 指令，80–82, 171
- NCSA（国家超级计算应用中心），5
- NDBM 文件，112
- negative.ttl 指令，625
- net start apache 命令，576
- net stop apache 命令，576
- Netcraft Survey Report 网站，3–4, 7, 718
- NetPresence AccessWatch 日志分析工具，233
- Netscape Navigator 代理设置，279
- Nestore 网站，233
- 网络 Web
  - 后端，638, 671–673
  - 描述，637–638
  - DNS（域名服务），637, 638–639
  - 负载均衡，638, 639–642, 641–672
  - 安全性，638, 673
  - 存储，硬盘优化，646–647
  - 存储，规划，638
  - 存储，通过 RAID（廉价磁盘冗余阵列），642
  - 存储，通过专用设备，643
- 网络管理任务，禁用，702
- Network File System（网络文件系统）。**另请参阅 NFS**
- 网络接口，共享信息，662–663
- 网络性能，优化，610–614
- Networks Associates 网站（www.naps.com），500
- Neulinger, Nathan，534
- 新的 http.conf 文件，577
- new-root.sh 脚本，574
- new-server-cert.sh 脚本，564
- 新闻组，与 Apache 相关，714–717
- new-user-cert.sh 脚本，565
- next php 脚本，446
- NFS（网络文件系统），661–662
  - 访问平均值，计算，661–662
  - 块大小，优化，659–662
  - 当前状态，658–659
  - 守护进程，优化，663
  - 空闲空间，检查，660
  - I/O（输入/输出）速度，659
  - MTU（最大传输单元）值，设置，662–663
  - 数据包碎片监控，664
  - 读取性能，测量，661
  - 服务器，658–659
  - 卸载，659
- nfs 文件系统，660。**另请参阅**文件系统
- nmop 实用工具，702
- NoCache 指令，275
- NoProxy 指令，271
- Null scan 端口扫描器，702
- 井号（#）
  - 注释前缀，31, 345
  - UID（用户 ID）数字前缀，97
- NoServers 指令，100–101

## O
- ob.end_flush 指令，434
- ob.start 指令，434
- Open source FJS 项目网站，652
- OpenSSL 实现，543, 551–554, 558, 720
- OpenSSL 项目网站，552, 554
- openssl_0_0_0.tar.gz 文件，552
- OpenWall 项目，703
- 操作系统
  - 优化，606–610
  - 安全性，487, 499
- 优化。**另请参阅**性能，优化
- Options 指令，43–44, 65–67, 129, 327, 373
- Options ExecCGI 指令，584
- Oracle 数据库服务器，使用其进行身份验证，202
- order 指令，192–193
- output_buffering 指令，433–434, 444–445

## P
- p
  - p() 方法，347, 348
  - p12 文件，565
  - p12.sh 脚本，565
  - .package 命令，458
  - parent() 方法，345, 464
- 分区
  - e2fsck，使用其进行检查，606, 651
  - 卸载，661
- Pass\*\*\*\* 指令，106
- 密码。**另请参阅**身份验证；安全性
  - 身份验证，其在其中扮演的角色，181, 183
  - 数据库存储，114, 115, 116–117, 195–196
  - 匿名访问的电子邮件地址密码，111–112
  - 加密，114, 116, 183, 201, 205
  - 创建存储于文件中的密码，184, 186
  - 存储于文件中的密码，与数据库存储对比，195–196
  - 保护存储于文件中的密码，517
  - 使用多个存储于文件中的密码，189–190
  - LIDS（Linux 入侵检测系统），691
  - 用于 MySQL 数据库访问，179
  - 明文，201
  - 更新用户表，207
- PATH 变量，472, 484, 518, 530–531, 585
- PATH_INFO 变量，118, 122, 241, 334–335
- PATH_TRANSLATED 变量，118, 122, 335
- 百分号（%），204
  - 编码字符序列前缀，528
  - 日志条目规范前缀，225
  - 变量前缀，246
- Perl\*\*\*\*h 模块，169
- 性能，优化
  - ACL（访问控制列表），625
  - Apache 可执行文件，剥离符号，609–610
  - 块大小，603, 648, 659–662
  - 缓存，600, 620–627
  - CPU（中央处理单元）速度，599–604
  - DMA（直接内存访问），601–602, 647
  - DNS（域名服务）查找，最小化，647
  - DSO（动态共享对象）注意事项，16
  - 以太网组件，602, 610–611
  - ext2 文件系统，602–606, 647–651
  - 硬盘，598–602, 646–647
  - 集线器与交换机，611
  - I/O（输入/输出）请求，最小化，616–617
  - Linux 文件系统，602–606
  - 负载均衡，475, 476, 613–614
  - 消息摘要注意事项，60–61
  - mod_perl 脚本，627–633
  - 网络，610–614
  - NFS（网络文件系统），565, 683
  - 操作系统，606–610
  - 服务器配置，608–610, 618–619
  - 静态文件服务，615–617
  - 系统调用，最小化，616–617
  - URL（统一资源定位符）重写注意事项，242
- 句号（.）
  - 目录前缀，47, 135
  - 正则表达式元字符，713
- Perl。**另请参阅**CGI（通用网关接口）；mod_perl 模块
  - 数组，346–347, 357
  - 二进制文件，编译，342
  - 大小写转换操作，348–349
  - CGI（通用网关接口）脚本，识别为，345, 355
  - CGI（通用网关接口）脚本，编写，315, 342–343
  - CGI.pm：使用模块编写脚本，345, 346–349, 356, 462–464
  - 编码，评估不安全性，345, 460
  - 注释，345
  - 常量，定义，460
  - 使用其定义容器，173
  - 容器，与脚本分离，342
  - Content-Type 头部，创建，345
  - 计数器，460, 461–462
  - CPAN（综合 Perl 归档网络）模块，204, 343, 356, 457
  - 数据库连接，缓存，628–630
  - 数据库驱动，202
  - DBM（数据库管理器）支持，113
  - 调试脚本，370–376
  - 加载，113
  - 电子邮件地址规范化，342–343
  - 环境变量，传递给 mod_perl 脚本，106
  - 全局变量，避免使用，315
  - handler 方法，460–461, 462, 464
  - 避免硬编码自定义信息，342
  - 哈希，172–173
  - HTML（超文本标记语言）内容创建，347–349
  - 解释器，15
  - 循环，346, 381
  - 模块加载，460, 461
  - 模块位置，458–459
  - 模块内存管理，463–466
  - 模块预加载，464–465, 627–628
  - 模块编写，458–464
  - 相关新闻组，717
  - 包名，458
  - 惯例（pragmas），345
  - 使用其配置代理服务器，290–292
  - 查询字符串信息，访问，464
  - 查询对象，462, 464
  - shebang 行，584
  - 源代码发行版（在 CD 上），721
  - 支持，6
  - 语法检查，175
  - 文本检查模式，178
  - 测试，处理，346–347
  - 用户数据，规范化，342–343
  - 用户组管理命令，204–208
  - 用户输入，345
  - 变量，处理，315, 345
  - 使用其配置虚拟主机，171–175
  - 针对 Windows，584
- Perl 语言网站，342, 718
- Perl MCPAN 命令，202, 204
- Perl Mongers 网站，718
- PerlHandler 指令，461
- PerlModule 指令，209, 464
- PerlRequire 指令，627
- PerlSetVar 指令，233, 209–210
- PGP（Pretty Good Privacy，漂亮好隐私），14, 499–500





## PHP：超文本预处理器
- 数组，447，449
- 使用进行身份验证，451–454
- 二进制描述符设置，424，586，721
- 字符集，设置默认值，429
- 命令行执行，435–436
- 编译，424–426
- 配置文件，425，427，428–435
- 使用生成版权声明，439–440
- 数据库支持，421，423–424
- DCOM（分布式组件对象模型）支持，422
- 描述，421–422
- 开发，便捷性，422
- 指令，428–435
- 目录索引，使用 PHP 页面作为，438
- 文档根目录，将包含文件与其分离，434
- 文档根目录，将脚本操作限制在，434
- 下载，424，586
- 环境变量，处理，434
- 错误处理，441
- 错误消息，自定义，430
- 错误消息，存储在 php_errormsg 变量中，435
- 错误报告级别，指定，430–431
- 转义选项，432–433
- 执行时间，设置最大值，433
- 扩展模块，与其配合使用，431
- 文件扩展名，426–427
- 文件权限，436
- 文件上传参数，435
- 页脚文档插入，428
- 函数，禁用，429
- 页眉文档插入，428–429
- HTML（超文本标记语言），在其中嵌入 PHP 代码，422，427
- HTML（超文本标记语言），在 PHP 页面中包含，439–441
- HTTP（超文本传输协议）内容类型头，抑制，436
- http_conf 设置，426，427–428，451，587
- 包含文件，432，434，439–441，451
- 安装，424–426
- 互联网标准支持，421，423
- 解释器，作为 CGI（通用网关接口），424，427，434
- 解释器位置，435
- Java 支持，423
- 与 JSP（Java 服务器页面）对比，470
- Linux（Unix）平台，424，432，435
- 动态加载，429
- 日志文件，430，432
- 循环，447，449
- 内存管理，423，433–434
- 模块，构建为 DSO（动态共享对象）版本，426
- 模块，构建为静态版本，425
- 模块位置，指定，432
- MySQL，配合使用，423–424，425，431，448–454
- 开源，423
- 输出，隐式刷新，432
- 输出缓冲，433–434，444–445
- 平台支持，421，423
- 普及程度，421，422
- 引号转义选项，432–433
- 安全模式，434
- 脚本，运行，436–437
- 脚本，编写，435–437
- 脚本解释器，作为独立解释器，422
- 会话，429，451
- 服务器端，421
- 会话，基于 Cookie，444–446
- 会话，URL（统一资源定位符）编码，446–447
- 会话创建，444–447
- 会话 ID，446
- 会话名称，445
- 会话注册，444，446
- 会话终止，447–448
- 会话变量，444–446，447
- 源代码分发（在 CD 上），424，721
- 速度，423
- SSI（服务器端包含），PHP 脚本作为，437–438
- 独立脚本，作为，421
- 系统要求，424
- 临时目录，435
- Web 表单处理，441–444
- Windows，在其下运行脚本，430，432，435，586–587

### .php 文件
426–427，428

### PHP 网站
423，428

### php4-4.1.0.tar.gz 文件
424

### php4ts.dll
586

### php_admin_flag 指令
427

### php_admin_value 指令
427–428

### php_errormsg 变量
435

### php_flag 指令
428

### php_info() 函数
437

### php_ini 文件
425，427，428–435，586

### php_ini-dist 文件
425，586

### php_info() 函数
437

### php_url_rewriter 扩展
428

### php variable 指令
428

### PID（进程 ID）
- ID 文件路径，37
- 服务器，37，53，85

### Pipe file 指令
37，53，85

### pipe
- 双（||）逻辑运算符，395–396
- 不打开 Shell 进行读取，530
- (||) 运算符，261，711
- open (|) 函数，518

### p1 文件
584

### 加号 (+)
- 指令开关，66，67
- HTTP（超文本传输协议）空格字符标记，528
- 正则表达式标准量词，511

### point 指令
153

### poly 指令
153

### popen() 函数
518

### port 指令
40，67–68

### port 变量
220

### postmaster 实用工具
656，658

### ports
- 使用指令进行分配，67–68
- 查看标准分配，67
- 使用 telnet localhost 检查可用性，622
- 数据库服务器，205
- 相关的环
量变量，332
- 以太网交换机，610
- FastCGI 应用程序，415
- HTPPS（安全超文本传输协议），556
- 监听，93–94
- 监控，220，226
- MySQL 服务器，179
- 代理服务器，622，623，632
- 扫描器检测，688，690，702
- 扫描软件，511
- 通过非标准端口实现安全，511
- 服务器，40，53，93
- SMTP（简单邮件传输协议），686，692

### SSL（安全套接层）
556，557，560，561

### Tcl/Tk
473，476，478–479，483–484，486

### 虚拟主机
68，298

### Web 服务器
296，298

### Windows Apache 服务
578，582–583

### POSSIBLE-ATTACKS.txt 文件
516

### POST 请求
72，122，194，704–708

### Postgres 数据库服务器
使用进行身份验证，202

### #pragma
345

### Pretty Good Privacy
参见 PGP

### print() 函数
432

### printw 脚本
28，392

### printf() 函数
449

### 权限
参见 权利

### 进程 ID
参见 PID

### 进程
- CGI（通用网关接口），9，400，401
- 子进程，与虚拟主机用户/组 ID 关联，169，309
- child_database 连接控制，633
- 子进程，显示相关统计信息，217
- 子进程，以 root 用户运行，40
- 子进程，设置来自每个子进程的最大请求数，39，94–95
- 子进程，设置最大同时创建数，100–101
- 子进程，设置每个用户最大同时数，75
- 子进程，设置分配给虚拟主机的数量，38–39
- 子进程，设置启动时创建的数量，36
- 子进程，设置每个子进程的线程数，39，97，100，101，580
- 子进程单线程，82
- 子进程，备用，103–104
- 子进程，用户 ID，97–98
- mod_perl 模块中的子进程，461，631–633
- CPU（中央处理器）使用率，控制，74
- 设备访问，禁用原始，701
- 相关指令，71–72
- FastCGI，400，401，402，414，415
- 文件句柄管理，155，607–608
- 进程创建，限制，75
- 隐藏，701
- 识别守护进程，88
- 终止，52，53，657
- LIDS（Linux 入侵检测系统），使用其进行保护，688，701
- 内存使用，控制，39，74，608
- 使用的模型，在安装时指定，23
- 监控，217，326
- 数量，控制，75，96，104–101，608–609
- scoreBoard 文件，32–38，85–96
- 安全，688
- 套接字任意进程所有权，禁用，702
- 系统资源考虑，71
- 终止，防止未授权的，688
- Web 服务器，299–300
- Windows，在其下，578

### ProtectedTicketUserTable
- PerlSetVar 指令键，209，210

### 代理服务器
参见 服务器，代理

### ProxyBlock 指令
270–271

### ProxyDNS 指令
271–272

### ProxyPass 指令
270

### proxy.pl 脚本
290–292

### ProxyPass 指令
269–270，271

### ProxyRequests 指令
269，275

### px_awox (grep httpd 命令)
50

### PUT 方法
用于内网 Web 发布，305–310

### putenv() 函数
434

### Q
- webstats 日志分析工具，233

### Q\* (反斜杠，大写 Q)
- 正则表达式元字符，710

### QUERY_STRING 变量
241，323，324，327，334

### 问号 (?), 正则表达式标准量词
711

### 通配符
78

### 引号，双引号 (" ") 身份验证标签分隔符
186

### R
- \r (反斜杠，小写 r) 正则表达式元字符，710
- RadarWeb Directive，614，640
- RAID（独立磁盘冗余阵列），598，642，659
- ramfs（基于 RAM 的文件系统），658–671
- rc.local 脚本，602，608，693
- read 函数调用，664
- rdist 实用工具，311，664–665
- rdist.distfile 文件，664–665
- rdist.distfile 脚本，665–668
- Read1line 方法，587
- ReadLine name 指令，137
- ReadOnly 变量，681
- rect 指令，153
- Redirect 指令，146–147
- 指令，49–50，138
- 减少，URL（统一资源定位符）
  - ACL（访问控制列表）访问，625
  - CGI（通用网关接口）脚本，到，263

### 重定向，URL（统一资源定位符）（续）
- 基于域类型，259–261
- 外部，240，245
- mod_alias 模块，使用，138
- Redirect 指令，使用，146–147
- RedirectMatch 指令，使用，147
- RedirectPermanent 指令，使用，147–148
- RedirectTemp 指令，使用，147
- 通过扩展将请求重定向到规范 URL（统一资源定位符），251–252
- 无需脚本，138
- Squid 代理缓存服务器实用工具，325
- Web 服务器，到新的，252–253，259

### RedirectMatch 指令
147

### RedirectPermanent 指令
147–148

### RedirectTemp 指令
147

### 独立磁盘冗余阵列
参见 RAID

### 寄存器读/写设置更改
禁用，702

### register.html
350–351

### 正则表达式 (regexp)
57，77，78，394，709–712

### ReiSerf 日志文件系统
652–656。另见 文件系统

### refereris
与 ext2.bash 脚本对比，513

### relocate.pl 脚本
388

### REMOTE_ADDR 变量
241，332

### REMOTE_HOST 变量
87，241，332

### REMOTE_IDENT 变量
241，333

### REMOTE_PORT 变量
332

### REMOTE_USER 变量
241，246，332–333

### RemoveHandler 指令
127–128

### remove_util
627

### 请求日志文件标记
221

### 请求变量
220

### REQUEST_FILENAME 变量
241

### REQUEST_METHOD 变量
241，323，324，327，333

### REQUEST_URI 变量
241，333

### require() 函数
432，441

### Require 指令
90–91

### Require valid user 指令
203

### require_once() 函数
441

### 重新启动服务器
50，52

### RewriteBase 指令
249

### RewriteCond 指令
245–247，254

### RewriteLock 指令
250

### RewriteLog 指令
249–250

### rewrite.log 文件
254

### RewriteLogPrefix 指令
250

### RewriteMap 指令
248–249

### RewriteOptions 指令
243

### RewriteRule 指令
243–245，252，254

### .rhosts 文件
664

### 权利
- ASP（活动服务器页面）目录，467
- CGI（通用网关接口）权限，301，505
- 默认拒绝，502
- 目录权限，45，306，504–506
- 文件权限，504–506
- Java Security Manager 权限类型，478
- LIDS（Linux 入侵检测系统），通过其分配权限，694–695
- MySQL_database，199
- 权限掩码默认值，设置，306
- PHP：超文本预处理器脚本，更改文件权限为，436
- Web 应用程序，199
- Web 站点权限，301

### RLimitCPU 指令
74

### RLimitMEM 指令
74

### RLimitNPROC 指令
75

### 机器人排除协议
263–264，513

### 机器人
263–264，512–514

### robots.txt 文件
513

### rotate.log 实用工具
234

### rotatelogs 实用工具
29

### Roxos 网站
717

### rpcinfo 实用工具
637

### rpc.mount 实用工具
637

### rpc.nfsd 实用工具
657，658

### rpc.portmap 实用工具
656

### rpm 命令
30

### RPM 资源：Trippower 网站
674

### RpmFind.Net 网站
30

### RSA Data Security, Inc.
550

### RSAREF 工具包
553，554

### S
- \s (反斜杠，小写 s) 正则表达式元字符，710
- Sacriental LAMP 配置，508–510。另见 安全
- safe_mode 指令，429，434
- safe_mode_allowed_env_vars 指令，434
- safe_mode_protected_env_vars 指令，434
- SAINT 实用工具，702
- SAN（存储区域网络），598，643
- SANS Institute 网站，517
- Satan 实用工具，702
- Satisfy all 指令，91，195
- Satisfy 指令，91–92
- ScoreBoardFile 指令，37–38，85–86
- Script 指令，122
- ScriptAlias 指令，49，148，335–336，503，505
- ScriptAliasMatch 指令，148，340–341
- SCRIPT_FILENAME 变量，241，334
- ScriptInterpreter 指令，92，584
- SCRIPT_NAME 变量，334

### 脚本
- apache11，28
- auth.php，452
- badcalc.pl，371
- 随本书附带 CD-ROM，包含在，720
- colors.pl，386–387
- config.status，179
- configure，19–24，179，214
- conf2.cfg，411
- fontz.cfg，413
- formdward，442
- formwizard.pl，332，364
- gretings.php，344–345
- hello.php，436
- hidden-md5，50，520–527
- http，29，51，52，63，609
- index.pl，507–508
- info.php，437
- 解释器检测，92
- login，211
- log_server.sh，236–237
- log-server-status，220
- makepkg，304–305
- make.runs，85，670
- maketips，175–178，666
- manager-users.php，202
- memory_hog.c，410
- mime-mail.pl，365–368
- missing_form，441
- modified_form.cgi，443–444
- new_root-ca.sh，564
- new-server-cert.sh，564
- new-server-cert.sh，565
- next_page.php，446
- piz.sh，565
- prince，28，392
- proxy.pl，290–292
- rc.local，602，608，693




# 索引

-   redistribute.sh, 666–668
-   reisersfs_vs.ext2.bash, 654–655
-   relocate.pl, 388
-   sign-server-cert.sh, 564
-   sign-user-cert.sh, 565
-   simple-query2.php, 450
-   simple-query.php, 448–449
-   stage2Production.sh, 303
-   start.php, 444
-   startup.pl, 586, 627–628
-   start_url, encoded_session.php, 446–447
-   test-cgi.sh, 28
-   test.php, 438–439
-   textfilter.pl, 119–121
-   tomcat, 485
-   tomcat11, 484–485
-   tripwire-check, 685
-   SCSI (Small Computer System Interface) 硬盘, 596, 597, 598, 643–644。另见 硬盘。
-   536–537
-   SEARCH 文件, 112
-   Search Engine Watch 网站, 718
-   搜索引擎
    -   解析，允许/禁止, 512–514
    -   向搜索引擎提交文件, 318
-   SEC_CRIT 变量, 680
-   Secondary web, Site. 另见 167
-   Second Hypertext Transfer Protocol. 另见 HTTPS

-   [CGI (通用网关接口) 脚本](https://example.org/cgi-script)
    -   与文档根目录分离, 49, 503–504
    -   通过其进行的系统命令欺骗, 518
    -   通过其进行的系统资源过载攻击, 518
    -   不安全的系统调用, 518–520
    -   封装, 531–536
    -   文件名扩展名，避免, 537
    -   信息泄露点, 517
    -   来源, 501, 517
    -   扫描器, 537–540
    -   支持，禁用, 510
    -   临时文件位置, 512
    -   用户输入, 518–520, 527–531
-   CGI (通用网关接口) 别名, 49, 503–504, 505–506, 536–537
-   以 root 用户身份运行的子进程, 40
-   在入侵者尝试连接时断开控制台, 690, 703
-   root 用户杀死守护进程, 511–512
-   目录, 700–701, 694–700
-   文档根目录, 41, 49, 503, 512
-   DOS (拒绝服务) 攻击
    -   驱动程序统计信息，禁用
    -   清除, 702
    -   以太网配置访问，禁用, 702
    -   exec 命令，禁用, 540–541
    -   FastCGI, 403
    -   功能，禁用未使用的, 499
    -   文件保护, 688, 694–700
    -   文件系统, 687
    -   文件，不可变标志保护, 702
    -   文件，完整性检查, 502, 674, 678–685
    -   文件，临时文件位置, 512
    -   防火墙, 276, 497, 509–510, 702
    -   主机控制台，限制管理操作, 501
    -   HTML (超文本标记语言) 隐藏标签, 520–527
    -   信息泄露, 517
    -   入侵者检测，响应, 515–517, 703
    -   I/O (输入/输出) 操作，防止未授权访问, 688
    -   ISP (互联网服务提供商)，阻止, 516
    -   Java 安全管理器, 477–479
    -   锁文件位置, 49
    -   日志文件，其在攻击中的作用, 501
    -   日志文件，保护, 48, 503, 515–517, 688
    -   登录文件, 687
    -   中间人攻击, 208
    -   模块，仅从认可来源下载, 590
    -   组播，禁用, 702
    -   网络, 496, 497–498
    -   网络管理任务，禁用, 702
    -   NFS (网络文件系统) 服务器, 688
    -   操作系统, 497, 499
    -   概述, 498–499
    -   数据包嗅探, 183
    -   密码文件, 517
    -   PATH 环境变量, 518, 530–531
    -   Perl 污点检查模式, 518
    -   PGP (Pretty Good Privacy), 14, 489–500
    -   PHP: HyperText Preprocessor (超文本预处理器), 429, 451
    -   策略，制定, 500–502, 511–514
    -   端口扫描检测, 688, 690, 702
    -   安全性 (续)
        -   partmapper 工具, 658
        -   端口，使用非标准端口, 511
        -   进程终止
            -   防止未授权终止, 688
        -   混杂模式，禁用, 702
        -   代理服务器, 266
        -   PUT 方法注意事项, 307
        -   寄存器读/写设置更改，禁用, 702
        -   robots, 512–514
        -   root, 144, 687, 700–701
        -   root 用户，禁用其修改操作, 688
        -   路由器 IP (互联网协议) 地址限制, 498
        -   路由表更改，禁用, 702
        -   替罪羊配置, 509–510
        -   Script 别名指定目录, 503, 505
        -   搜索引擎解析，允许/禁止, 512–514
        -   服务器信息显示注意事项, 70
        -   服务器令牌, 70
        -   server root 指定目录, 503
        -   socket 任意进程所有权，禁用, 702
        -   socket 调试更改，禁用, 702
        -   备份, 512–514
        -   Squid 代理缓存服务器, 622
        -   SSI (服务器端包含), 510, 540–541
        -   独立模式, 502–503
        -   状态信息，通过 Web 提供, 510
        -   系统调用，不安全, 518–520
        -   系统资源过载攻击, 518
        -   TCP SYN 洪泛攻击, 94
        -   Tomcat, 478, 483
        -   TOS (服务类型) 更改，禁用, 702
        -   传输日志，按虚拟主机的用户交互, 223
        -   Tripwire, 682
        -   特洛伊木马, 674
        -   URL (统一资源定位符) 重写，使用其进行访问限制, 263–264
        -   用户输入, 315, 518–520, 527–531
        -   用户覆盖，禁用, 508–509
        -   uuencode, 183
        -   Web 文档树，在其中存储数据库文件, 114
        -   Web 文档树，在其中存储用户文件, 116, 185
        -   Web 网络, 628, 673
        -   Web 服务器，放置在防火墙外, 509–510
        -   Web 服务器软件, 497, 499–500
        -   使用指令进行 Web 服务器访问控制, 58
        -   网站，动态与静态, 496
        -   网站，按用户划分, 510
        -   select * from tickets
            -   send http_header() 方法, 460
    -   服务器。另见 服务器，代理
        -   别名定义, 82
        -   apacherrchmod (1) 工具，使用其调整, 10, 28, 618–619
        -   基准测试, 28
        -   检查是否正在运行, 50–51
        -   配置文件, 31–36
        -   压缩，持久性, 38, 72–73
        -   指定核心转储目录, 92
        -   CPU (中央处理单元) 使用率，控制, 74
        -   数据库服务器, 196, 202, 205
        -   目录容器, 43–44
        -   目录结构, 36–37, 41–45, 503–504
        -   定义特定目录的功能, 65–67
        -   ECHO 服务器，启用, 22
        -   工程师卡, 602
        -   组 (GID) 名称, 40
        -   inetd 服务，作为其运行, 502
        -   保持连接行为, 38
        -   监听, 93–94
        -   本地文件, 94
        -   日志文件，指定, 48
        -   名称，在通用网关接口 (CGI) 脚本中获取, 330
        -   net，设置, 68–69, 571
        -   path，遗留统一资源定位符 (URL), 82
        -   性能，优化, 608–610, 618–619
        -   进程 ID (PID), 57, 53, 85
        -   每秒请求数，最大化, 618–619
        -   根目录，设置, 36–37, 69
        -   脚本解释器检测, 92
        -   签名显示, 48, 69
        -   独立模式, 96, 502–503
        -   测试, 53–54
        -   时间，显示, 216
        -   上次重启时间，显示, 216
        -   运行时间，显示, 217
        -   超时, 38, 72
        -   令牌，标识符, 69–70
        -   流量信息，显示, 217
        -   Unix/Linux 与 Windows, 4, 499, 578
        -   Web 浏览器，通过其访问, 53
    -   服务器，代理
        -   访问控制, 266, 270–271, 277
        -   缓存, 265, 266, 267
            -   目录选项, 272, 274
            -   启用/禁用, 269, 272, 275, 276–277
            -   过期设置, 273, 274
            -   文件选项, 272–273, 274
            -   Squid 代理缓存服务器, 621–626
        -   缓存远程 GIN 表, 276–278
        -   CGI (通用网关接口)，使用其进行配置, 288–290
        -   描述, 265–266
        -   ${directory} 容器，在其中定位代理指令, 275
        -   文档树，映射至, 270
        -   域名，指定默认值, 271–272
        -   启用/禁用, 275
        -   防火墙, 276, 497, 509–510
        -   正向代理服务, 266–267
        -   FTP (文件传输协议) 代理, 269, 623
        -   主机列表，使用其限制访问, 277
        -   http.conf 设置, 270, 275, 632
        -   互联网环境, 266, 267–268, 271
        -   日志记录, 265
        -   多个服务器, 282–283, 288, 289–292
        -   Port 脚本，使用其进行配置, 280–282
        -   端口, 622, 623, 632
        -   私有 IP (互联网协议) 网络，连接至互联网, 276
        -   协议处理限制，设置, 277–278




# 服务器 API
- 应用程序接口，400–401
- 服务器变量，220
- Server Watch 网站，718
- ServerAdmin 指令，41, 68
- SERVER_ADMIN 变量，241, 329
- ServerAlias 指令，82
- ServerName 指令，68–69
- SERVER_NAME 变量，241, 301, 330
- ServerPath 指令，82
- SERVER_PORT 变量，67, 241, 332
- SERVER_PROTOCOL 变量，241, 333
- ServerRoot 指令，36–37, 69, 503
- 服务器端包含。参见 SSI
- ServerSignature 变量，48, 69
- ServerSoftware 变量，241, 329
- serverTokens 指令，69–70
- SERVER_VERSION 变量，241
- server.xml 文件，473, 479, 483–484
- services 文件，67
- 会话跟踪，启用，23
- session_destroy( ) 函数，447
- session.name 指令，446
- session_register( ) 函数，444, 446
- session_start( ) 函数，444–445, 446
- session.use_cookies 指令，446
- set 命令，393
- SetEnv 指令，107, 472
- SetEnvIf 指令，108
- SetEnvIfNoCase 指令，109
- SetHandler 指令，127, 217–218, 417, 457
- SetInputFilter 指令，70
- SetOutputFilter 指令，70, 379, 380
- SIG (Silicon Graphics, Inc.)，652
- shebang 行，584
- show_challenge( ) 函数，453
- sSign 工具，682
- sign-server-cert.sh 脚本，564
- sign-user-cert.sh 脚本，565
- sig.txt 文件，682
- simple_form.html，442
- simple.query2.php 脚本，450
- simple_query.php 脚本，448–449

### 斜杠 ( / )
- 别名定义中，145
- 路径分隔符，579

- Sleepycat Software 网站，116

### 小型计算机系统接口
- 硬盘。参见 SCSI

### SMTP (简单邮件传输协议)
- 禁用，499
- 端口，686, 692
- Twitter 设置，686, 692

- SourceForge.net 网站，364, 604, 648, 674
- SpeakEasy.Rosymind.Net 服务器网站，604
- special_command_line_param 选项，63
- 速度，针对其优化。参见 性能，优化
- 网络爬虫，阻止，263–264
- split( ) 函数，346

### Squid 代理缓存服务器
- 621–626
- squid.conf 文件，622, 623, 624
- sm_rnd，300
- S$.* 变量，558

### SSI (服务器端包含)
- CGI (通用网关接口) 脚本，调用，386–389
- 命令结构，382
- 比较运算，394–397
- config_errmsg.shtml，382–383
- 版权声明，使用其嵌入，314
- 描述，377–378
- 指令，在其中启用/禁用，60, 67, 379, 381
- elseif 语句，396–397
- 环境变量，传递给，106–107
- exec_cgi1.shtml，387
- exec_cgi2.shtml，388–389
- exec_cmd.shtml，389–390
- 文件扩展名通常解析用于，379, 381
- 通过其打印文件修改日期，391
- 文件星号，通过其显示，384, 391
- 文件类型，为特定类型启用，380–381
- 流程控制，394–397
- HTML (超文本标记语言) 锚点通过其创建，388–389
- http.conf 设置，379
- if 语句，394–395, 396
- INCLUDES 过滤器，作为其实现，378
- 逻辑运算符，395–396
- 模块，动态内容生成，105, 117, 377–378
- 解析错误消息格式化，382–384
- PHP: 超文本预处理器脚本作为，437–438
- 程序，禁用外部，381
- 程序，执行外部，385–390
- 正则表达式，在其中使用，394
- 安全性，510, 540–541
- SHTML (支持 SSI 的 HTML)，377–378
- 语句，条件，394
- 支持，7
- 文本，通过处理插入到文档中，391–392
- 时间显示格式化，384–385
- 变量，处理，106–107, 385, 392–394, 395
- 虚拟主机配置，379, 380
- 支持 SSI 的 HTML。参见 SHTML

### 安全套接字层 (SSL)
另参见 加密；mod_ssl 模块；安全性
- 访问启用 SSL 的页面，565
- 应用程序，交互，544
- 应用程序代码，在源代码树中禁用，553
- 缓存设置，556, 561
- 证书，交叉链接，564
- 为 Apache-SSL 创建证书，559–560
- 证书区分名称，547–548
- 定义证书文件路径，557, 561
- 证书颁发者，547, 550–551, 562
- 证书密钥文件，557
- 证书签名请求，562, 563–564
- 证书交易过程，548–550
- 配置文件目录，指定，553
- 连接，测试，561–562
- CRL (证书吊销列表)，556
- 加密算法设置，554, 557
- 描述，543–544
- 文档根目录，指定，557
- DSO (动态共享对象) 标志，554
- 启用，557, 561
- 环境变量，555, 558
- 出口限制，552
- httpd.conf 设置，556–558
- 在其使用中，HTTPS (安全超文本传输协议)，550, 562, 565
- Intel 386 机器，为其编译，554
- 库安装，23
- 库共享，553
- 日志记录选项，556
- MAC (消息认证码)，550
- 多线程，启用/禁用，553
- 复用文件路径，556
- OpenSSL 安装，543, 551–554
- 端口，556, 557, 560, 561
- 随机数生成，560
- 随机种子方法定义，556
- 会话缓存数据库路径，556
- 支持，7, 23
- 测试，561–562
- Tomcat，473
- 事务，基于证书，548–550
- 虚拟主机配置，557, 560, 561
- SSLCaServerPort 指令，561
- SSLCACertificateFile 指令，557, 561
- SSLClientCertificateFile 指令，557
- SSLCipherSuite 指令，557
- SSLEx 库，551
- SSLEnable 指令，561
- SSLEngine 指令，557
- SSLRandomFile 指令，560
- SSLRequireSSL 指令，560
- SSLSessionCacheTimeout 指令，561
- stage2Production.sh 脚本，303

### 开始 > 程序 > Apache httpd 服务器
- 配置
- 编辑配置，577
- 开始 > 程序 > Apache httpd 服务器 > 测试配置，577
- 开始 > 程序 > Apache httpd 服务器 > 重启，577
- 开始 > 程序 > Apache httpd 服务器 > 控制 Apache 服务器 > 启动，577
- 开始 > 程序 > Apache httpd 服务器 > 控制 Apache 服务器 > 停止，577
- 开始 > 设置 > 控制面板 > 管理工具 > 服务，575

- start.html
- start-form( ) 方法，525
- start_htmlp( ) 方法，347, 348–349, 525

### 启动 Apache
- 文件，在启动时加载，152
- Unix，50–52

- 启动 Tomcat，484–485, 490
- start.php 脚本，444
- StartServers 指令，39, 72, 96
- StartScripts 指令，101
- start_up.pl 脚本，586, 627–628
- start_url_encoded_session.php 脚本，446–447
- 状态日志文件标记，221
- Stealth FIN 端口扫描仪，702

### 停止 Apache
- Unix，52–53
- Windows，576

- 停止 Tomcat，484, 490
- 存储区域网络。参见 SAN
- strip -i21 命令，609–610
- Stronghold 网站，717
- submit( ) 方法，525
- SUEEx 封装器，29, 98, 531–534
- Sun Microsystems 网站，471
- Syntek Stealthport 扫描仪，702
- SysCtl，689
- syslog 关键字，230–232, 430

### 系统
- log.conf，230–232
- 日志函数，518–519, 529–530

### 系统调用
- CGI (通用网关接口) 调用，不安全，518–520
- static{ }，617
- 最小化，616–617
- mmap( )，155

### 系统要求
- ANSI (美国国家标准学会) C 编译器，15
- CPU (中央处理单元) 硬盘，15, 395–596
- 内存，594–595
- Perl 5 解释器，15
- PHP: 超文本预处理器，424–425
- Unix，14–18
- Windows，569–570

- system32 目录，585

### T
- t (反斜杠，小写 t) 正则表达式元字符，710
- tail 实用程序，53, 232
- TCP SYN 泛洪攻击。另参见 安全性
- TCP (传输控制协议) 协议缓冲区大小，96
- telnet (localhost 命令，622

### 模板
- DNS (域名服务)，304–305
- 表单模板，356, 357–358, 360, 362
- 在网站管理中，304–305

- test -cgi 脚本，28
- test.php 脚本，335–336
- textfield( ) 方法，525
- textfile.p 脚本，119–121
- thankyou.html，262–263
- Thawte Consulting 证书颁发机构，551, 563
- THE_REQUEST 变量，241

### 威胁处理
- 子进程，单线程，82
- FastCGI 多线程，401–402, 407
- 文件句柄管理，155, 607–608




Java servlets 线程创建，469
多处理模块（MPs），7–8, 24–26, 37–39, 85–86, 95–96
SSL（安全套接字层）多线程支持，启用/禁用，553
Windows 安装，580
winit 模块，8–9, 101–102, 580
线程监控，启用，23
threadsPerChild 指令，39, 97, 580
tide() – 扩展正则表达式前缀，77
time 变量，242
TIME_DAY 变量，241
TIME_HOUR 变量，242
TIME_MIN 变量，242
TIME_MON 变量，241
超时
  服务器，38, 72
SSL（安全套接字层）
  缓存，556, 561
WebDAV（Web 分布式创作和版本控制），156
TimeOut 指令，38, 72
TIME_SEC 变量，242
TIME_WEEKDAY 变量，242
TIME_YEAR 变量，241
标记，日志文件，221。另见 日志记录
tolower() 函数，248
Tomcat。另见 Java servlets；JSP（Java 服务器页面）
  管理工具，482
  管理员用户，482–483
  类路径，476–477
  配置文件，473, 479, 482, 490
  连接处理器，473, 475
  Context Manager（上下文管理器），480
  描述，469–470
  目录元素分隔符，指定，475
  目录设置，473, 475, 479–480, 481
  下载，472
  环境变量，471–472, 473, 475, 484, 485
  HTTP（超文本传输协议）服务，禁用默认，483–484
  http.conf 文件设置，479–482, 484
  安装，471–473
  实例，473
  Java Security Manager（Java 安全管理器），为此设置，479–483
  Java servlets，与其交互，469
  Java servlets，运行，485–491
  Java servlets，为此设置，479–483
  JRE（Java 运行时环境），471
  JSP（Java 服务器页面），与其交互，470
  JSP（Java 服务器页面），运行，485–491
  JSP（Java 服务器页面），为此设置，479–483
  JVM（Java 虚拟机）
    库路径，477
    负载均衡，475, 476
    日志文件设置，480, 490
    mod_jk 模块，与其交互，469
    端口，473, 476, 478–479, 483–484, 486
    请求处理，475, 486
    root，以 root 身份运行，486
    安全性，478, 484, 486
    服务器页面，默认，486
    关闭，473
    SSL（安全套接字层）支持，487
    启动，484–485, 490
    停止，484, 490
    工作进程，473–477, 480, 482
    tomcat run 命令，484
    tomcat 脚本，485
    tomcat start 命令，484
    tomcat stop 命令，484
    Tomcat 网站，472
    tomcat|t| run 命令，485
    tomcat|t| 脚本，484–485
    tomcat|t| start 命令，484, 485
    tomcat|t| stop 命令，485
    TOMCAT_HOME 变量，473, 475, 484
    tomcat.policy 文件，478
    tomcat-users.xml 文件，482

工具 = Internet 选项 = 安全性 > 自定义级别 >  Cookie > 提示选项，211
Top Server 统计信息网站，3–4
top 实用工具，17, 594
TOS（服务类型），702
toupper() 函数，248
track errors 指令，435
跟踪
  会话，启用，23
  使用 Cookie 的用户，228–229
Transfission 指令，22–223, 224, 227
Tripwire
  自动化，685
  编译，674–678
  配置文件，677–678
  cron 任务，通过其运行，674, 685, 686
  数据库创建，681–682
  数据库更新，685
  文档，674
  目录创建，679
  下载，674
  电子邮件设置，678, 685, 686–687
  加密，677, 678, 681
  文件完整性检查，502, 674, 678–685
  安装，674–678
  交互模式，682–684
  许可协议，674
  掩码字符，679–680
  密码短语，677
  策略文件，678, 679–680, 681, 682
  属性字符，679–680
  报告，678, 682–684, 686–687
  规则，将多个应用于同一目录，681
  规则，将多个应用于同一文件，681
  规则，在目录下分组目录，680
  规则，在目录下分组文件，680
  规则，最具体的优先，681
  规则，名称，678
  规则，严重级别，678
  规则，语法，678
  保护，682
  签名数据库，674
  SMTP（简单邮件传输协议）设置，686, 692
  变量，内置，680–681
  网站，502
Tripwire 开源开发网站，674
Tripwire 2.3.0 Secure.tar.gz 文件，674, 675
tripwire-check 脚本，685
twinefs 实用工具，604–606, 649–651
twadmin 命令，681, 686
tw.cfg 文件，678
tw.cfg.txt 文件，678, 686
tw.install.sh 脚本，675, 677
tw_pol 文件，678, 681, 682
服务类型。见 TOS
TypeConfig 指令，47, 128
\（反斜杠，小写 u）正则表达式元字符，710
\U（反斜杠，大写 U）正则表达式元字符，710
`ucfirst()` 函数，346
UID（用户 ID）名称，40
`ulimit` 实用工具，609
UltraDMA 模式 2 硬盘，647。另见 硬盘
`ultradma`，333 硬盘，596。另见 硬盘
`umask` 指令，306
unmount 命令，661
统一资源特性。见 URC
统一资源标识符。见 URI
统一资源定位符。见 URL
统一资源名称。见 URN
`uniq` 实用工具，233
`UNIVOLD_10` 变量，109
密苏里大学 FTP（文件传输协议）站点，534
Unix 系统
  从二进制包安装 Apache，13-4, 30, 499, 609
  编译，26-29
  调试，开启，21
  下载软件，13-14, 18-19
  日志文件，23
  源代码，来自，19-29
  系统要求，14-18
`UseEnv` 指令，107
`upload_tmp_filesize` 指令，435
`upload_tmp_dir` 指令，435
URC（统一资源特性），57
URI（统一资源标识符），57
URL（统一资源定位符）
  向后兼容，262
  CGI（公共网关接口），在其中工作，263, 325, 368-369
  指令，应用于，57, 79-80
  处理器，为特定地址分配/取消分配，127-128
  主目录，144-145, 252-253
  长度限制，90, 325
  模块映射，105, 144-151
  PHP：超文本预处理器会话，URI 编码，446-447
  `seller-referring`，47, 75
  `server legacy URL` 路径，82
  拼写纠正，自动，148-149
  时间敏感，261
URL 重定向 ACL（访问控制列表）对比，625
URL（统一资源定位符）
  CGI（公共网关接口）脚本，至，263
  域类型，基于，259-261
  `external`，240, 245
  `mod_asis` 模块，使用，138
  请求生成，绕过，146-147
  `RedirectMatch` 指令，使用，147
  `RedirectPermanent` 指令，使用，147-148
  `RedirectTemp` 指令，使用，147
  请求，通过扩展至规范 URL，251-252
  脚本，不使用，138
  `sudo` 代理缓存服务器实用工具，625
  Web 服务器，至新的，252-253, 259
URL（统一资源定位符）引用规则
  访问多路复用器，259-261
  使用其进行访问限制，263-264
  附加到替换地址，245
  反向引用，243-244, 246
  通过其实现向后兼容，262
  浏览器类型，将其匹配到内容，使用，262-263
  大小写敏感性，忽略，245, 247
  CGI（公共网关接口）脚本，将 HTML 请求重定向至，263
  链式，244, 258
  条件，245-247, 254
  `defining`（定义），243-245
  偏转请求，264
  指令，跨多个搜索，253-255
  域类型，基于，259-261
  `enabling`（启用），22, 242
  `filename-based internal subrequest`（基于文件名的内部子请求），246
  `flags`（标志），243, 244-245, 247
  `HTTP`：超文本传输协议）响应头，与其工作，244-245, 246, 262, 264
  `httpd.conf` 设置，254
  继承，243
  `logging`（日志记录），249-250, 254
  maps（映射），与其工作，248-249, 250, 259-260, 264
  MIME（多用途互联网邮件扩展）类型，强制，245
  `multi` `ltif` `aws` 搜索，253-255
  `per-directory`（按目录），242, 249
  性能考虑，242
  处理，以最后一个替换结束，245
  请求，强制外部，245
  请求转换为代理，245
  请求生成，在内部绕过，245
  `restarting` 从第一条规则重新开始，245
  `short` 通过其阻止，263-264
  `search pattern`（搜索模式），243-244
  `robot` 扩展至规范 URL（统一资源定位符），251-252
  跳过指定数量的，245
  `substitution` 字符串，243
  `test-strings` 测试，247
  时间依赖，261
  `username-based` 地址，257-258
  `variables`，环境，107, 224, 244, 246, 256-257
  `variables`，服务器，241-242, 246
  `Web` 蜘蛛使用其阻止，263-264
URN（统一资源名称），57
`use command`，197
`use strict Perl` 声明，345, 460
`UseCanonical` 指令，47, 75, 150
`User` 指令，40, 50, 97-98, 172, 502-503
`user` 组，183-188, 190, 198, 204-208, 505
`user` ID 名称。见 UID 名称
`user` 请求，映射，禁用，22
`user` 使用 Cookie 跟踪，228-229
`UserId` 指令，44-45, 144, 532, 588-589
`usermod` 命令，505
`username`
  `alphanumeric`（字母数字），340
  `authentication`（身份验证），其中的角色，181, 183
  大小写敏感性，110
  CGI（公共网关接口）注意事项，340




## 实用工具
- ab (ApacheBench)，10, 28, 618–619
- AccessWatch，233
- admin tool（管理工具），482
- Analog 日志分析工具，233
- apxs，28
- awk，603, 648
- cat，232–233
- ezfsck，606, 651
- ezfsprogs 软件包，603–606, 648–651
- find，311, 603, 648
- fsck，605, 650
- grep，50–51
- hdparm，599, 602, 644–647
- httpd，28
- htpasswd，29, 184, 186
- http-analyze，233
- killall，657
- logsolve，29, 236
- logrotate，234–236
- ls，390
- mkfile, c，655
- mountd，657
- nsd，657, 658
- nmop，702
- portmapper，656, 658
- Rewebstats，233
- rdist，311, 664–668
- renice，627
- rotatelog，234
- rotatelogs，29
- rcfind，657
- Saint，702
- Satan，702
- sigen，682
- tail，232
- top，17, 394
- tune2fs，604–606, 649–651
- ulimit，609
- uniq，233
- vmstat，395
- WebStat Explorer，233
- WebTrends，233
- Wusage，233, 515
- wstat 日志分析工具，233

## V
- \ (反斜杠，小写 v) 正则表达式元字符，710
- v2h 指令，179
- v2h_DecLinitURI 指令，179
- v2h_EscapePath 指令，179
- v2h_Mysql_Db 指令，179
- v2h_Mysql_Env_Fld 指令，179
- v2h_Mysql_Host 指令，179
- v2h_Mysql_Pass 指令，179
- v2h_Mysql_Path_Fld 指令，179
- v2h_Mysql_Port 指令，179
- v2h_Mysql_Serv_Fld 指令，179
- v2h_Mysql_Tbl 指令，179
- v2h_Mysql_User 指令，179
- v2h_PathHead 指令，179
- v2h_UseMetrica 指令，179
- 变量。另请参见环境变量
    - API_VERSION，242
    - AUTH_TYPE，241, 333
    - CGI（通用网关接口），与其相关的工作，315, 328–335, 345
    - 字符集设置，与此相关，529
    - cf，30–35
    - cf，28
    - cf_content，179
    - date，179
    - v2h_Tbl，179
    - documentation，179
    - server，179
    - HTTP_ACCEPT，330
    - HTTP_ACCEPT_CHARSET，330
    - HTTP_ACCEPT_ENCODING，330
    - HTTP_ACCEPT_LANGUAGE，331
    - HTTP_CONDITION，332
    - HTTP_COOKIE，241
    - HTTP_FORWARDED，241
    - HTTP_HOST，241, 330
    - HTTP_PROXY_CONNECTION，241
    - HTTP_REFERER，241, 331
    - HTTP_USER_AGENT，241, 331
    - ignoreall，681
    - ignorelnk，681
    - 包含变量，385, 386, 389, 393
    - IS_SUBDIR，242
    - JAVA_HOME，471, 484, 485
    - javadoc.jsp，108
    - LAST_MODIFIED，393
    - mod_perl，457
    - PATH，472, 484, 518, 530–531, 585
    - PATH_INFO，118, 122, 241, 334–335
    - PATH_TRANSLATED，118, 122, 335
    - Perl，与其相关的工作，315, 345
    - PHP: Hypertext Preprocessor 会话变量，444–446, 447
    - php_errors，435
    - PHPC，427
    - port，220
    - QUERY_STRING，241, 323, 324, 327, 334
    - ReadOnly，681
    - REMOTE_ADDR，241, 332
    - REMOTE_HOST，87, 241, 332
    - REMOTE_IDENT，241, 333
    - REMOTE_PORT，332
    - REMOTE_USER，241, 246, 332–333
    - request，220
    - REQUEST_FILENAME，241
    - REQUEST_METHOD，241, 323, 324, 327, 333
    - REQUEST_URI，241, 333
    - SCRIPT_FILENAME，241, 334
    - SCRIPT_NAME，334
    - sec_crit，680
    - server，220, 241–242, 246, 329
    - SERVER_ADMIN，241, 329
    - SERVER_NAME，241, 301, 330
    - SERVER_PROTOCOL，331, 333
    - SERVER_PORT，330, 241, 332
    - SERVER_SOFTWARE，241, 329
    - 服务器变量，241
    - SS. *. * 变量，558
    - SSL (Server-Side Include)，与其相关的工作，106–107, 385, 392–394, 395

### 变量（续）
- SSL_BASE，555
- THE_REQUEST，241
- TIME，242
- TIME_DAY，241
- TIME_HOUR，242
- TIME_MIN，242
- TIME_MON，241
- TIME_SEC，242
- TIME_WDAY，242
- TIME_YEAR，241
- Topcat_HOME，473, 475, 484
- Tripleware 变量，内置，680–681
- UNIQUE_ID，109
- USER_TABLE，205
- VHE_EXTRA，179
- wherolog，220
- windir，585

- Versign 证书颁发机构，551
- 可用的 Apache 版本，18
- VHE_EXTRA 变量，179

## 虚拟主机
- 浏览器 HTTP（超文本传输协议）支持注意事项，161
- CGI（通用网关接口）支持，配置，336
- 配置，动态，149–151
- 配置文件，160, 163–165, 170–171
- 容器，51, 58, 65, 68, 82–83
- 创建，161–165, 288–299, 309–310
- 默认，83
- 描述，159
- 开发服务器，298
- 特定指令，35, 57, 80–83
- DNS（域名服务）设置，166–168, 175, 177
- 文档根目录，149–150, 176
- 组 ID 设置，169–170, 309
- 基于 .htaccess 的认证，187
- httpd.conf 设置，160–161, 163–164, 170–171, 173–175, 179
- IP（互联网协议）寻址，83, 161–162
- IP（互联网协议）基础，161, 162–163
- 邮件服务，168
- makefile 脚本，使用其配置，175–178
- mod_put 模块，为其设置，309–310
- MySQL 脚本，使用其配置，178–179
- 基于名称的，80–82, 161–162, 177
- Perl 脚本，使用其配置，171–175
- 端口，68, 298
- 进程，将子进程与用户/组 ID 关联，169, 309
- 进程，指定分配给子进程的数量，98–99
- 代理服务器，为其创建，278
- 通过别名共享脚本，150–151, 159
- 服务器，使用多个，161, 162–165
- SSI（服务器端包含），为其配置，379, 380
- SSL（安全套接字层），为其配置，557, 560, 561
- 预生产服务器，298
- 支持，6
- TransferLog 操作，其中的用户继承，223
- 用户 ID 设置，169–170, 309
- 用户名，为其分配，398
- 基于用户名的地址，258
- Windows 安装，582–583
- Virtual Web Sites，159
- VirtualDocumentRoot 指令，149–150
- VirtualDocumentRootIP 指令，150
- <VirtualHost> 容器，51, 58, 65, 68, 82–83
- VirtualHost 别名指令，150
- VirtualScriptAliasIP 指令，151
- wma stat 实用工具，595

## W
- \ (反斜杠，小写 w) 正则表达式元字符，710
- 图像加水印，512
- Web Compare 网站，718
- Web Developer 网站，718
- Web Director，614, 640
- 使用 CGI（通用网关接口）处理 Web 表单
    - 加载配置文件，352, 356
    - 在配置文件中定位 Web 表单，352, 353, 356–357, 360
    - 数据存储，350, 352, 353
    - 错误消息生成，352, 353, 360, 361
    - 管理，集中化，350, 364
    - 模块加载，352, 353, 355–356
    - 使用单个脚本处理多个表单，349
    - 对象创建，352, 353, 356
    - 模板，356, 357–358, 360, 362
    - 显示感谢消息，352, 358, 361, 362–363
    - 用户数据验证，352, 353, 358, 360, 361
    - 用户重定向，361–362
- 使用 PHP: Hypertext Preprocessor 处理 Web 表单，141–444
- Web 网络
    - 后端，638, 671–673
    - 描述，637–638
    - DNS（域名服务），637, 638–639
    - 负载均衡，638, 639–642, 671–672
    - RAID（独立磁盘冗余阵列），642
    - 安全性，638, 673
    - 存储，硬盘优化，646–647
    - 存储，规划，638
    - 存储，由专用设备提供，643
- Web Reference 网站，718
- Web 安全性，参见“安全性”
- 网站，虚拟，参见“虚拟主机”
- Web site Garage 网站，318
- 网站管理
    - 动画，317
    - 认证，186–187, 209
    - 备份，310–312
    - 横幅广告，318
    - 颜色，316
    - 设计一致性，293, 304
    - 使用 makepage 脚本更新内容，304–308
    - 内容发布策略，511–512
    - 副本，维护权威性，501
    - 版权信息，314
    - 开发周期，294–304
    - 开发服务器，297, 298, 300
    - 开发工具，304
    - 目录结构，36–37, 41–45, 114, 144–145, 297–298
    - 通过电子邮件发送 Web 页面，364–369
    - 错误消息，自定义，317
    - 文件管理，296
    - 主机控制台，从该处进行管理，501
    - HTML（超文本标记语言）标准，312
    - 图像，296–313
        - 用于图像的目录，296, 312–313
        - 下载时间考量，317
        - 文件命名约定，296
        - 使用水印指示版权，312
        - 内联，312–314
        - 可重用，313
    - 参与链接交换，318
    - 记录，301
    - 仅限成员区域，186–187, 209
    - META 信息，318
    - 镜像，278, 311
    - 导航元素，316
    - 权限，301
    - 策略，312, 314–315
    - 端口，296, 298
    - 生产阶段，295
    - 生产服务器，298, 302–304
    - 推广，318
    - 发布内容，294, 305–310, 511
    - PUT 方法，用于互联网使用，304
    - Web 发布，305–310
    - 搜索引擎，允许/禁止解析，512–514
    - 向引擎提交，318
    - 服务器设置，296–301
    - 预生产阶段，295–296
    - 预生产服务器，297, 298
    - 标准，312–315
    - 其中的模板，304–305
    - 测试，301, 317–318
    - 文本大小，317
    - 用户界面设计，315–318
- Web 蜘蛛，阻止，263–264
- WebDAV（基于 Web 的分布式创作和版本控制）
    - 使用容器，156
    - 启用/禁用，22, 155–156
    - 锁数据库文件，156
    - 超时，156
- WEB-INF 目录，481
- WebStat Explorer 日志分析工具，233
- WebTrends 日志分析工具，233
- where log 变量，220
- Whisker 扫描器，539–540
- 路径名称中的空白字符，580
- WHOIS 数据库，516, 519
- 通配符
    - 在别名定义中，82
    - 匹配字符序列，77, 79
    - 匹配单个字符，79
- wildw 变量，585
- Windows 2000 Advanced Server，569–570, 576
- Windows 系统，585
- 在 Windows 系统上安装 Apache
    - 二进制安装，570–574
    - 自定义安装，572
    - 目录，默认，573
    - 域名，571
    - 下载软件，570
    - 选择功能，573
    - 许可协议，570–571
    - 服务器名称，571
    - 系统要求，569–570
- Windows 2000 Advanced Server，569–570
- 在 Windows 系统上运行 Apache
    - CGI（通用网关接口）脚本，584
    - Comanche，使用其进行管理，581–584
    - 命令行，577
    - 测试配置，580
    - 目录结构，588–589
    - 环境变量，585
    - httpd.conf 文件，577, 578, 579, 580
    - ISAPI（互联网服务器 API）扩展，587–588
    - 内存监控，584
    - mod_perl 脚本，585–586
    - 多线程，580
    - 路径分隔符，579
    - PHP, Hypertext Preprocessor 脚本，586–587
    - 端口，578, 582–583
    - 进程，578
    - 服务，作为服务运行 Apache，574–577, 578
    - 开始菜单选项，577
    - 启动 Apache，574–577
    - 停止 Apache，576
    - 系统要求，569–579
    - 任务管理器，594
    - 与 Unix 的区别，4, 489, 578
    - 虚拟主机，582–583
    - WINNT 目录，585
- winnlt 模块，9, 101–102, 580
- worker.list 文件，476
- workers，473–477, 480, 482, 580
    - 另请参见 Tomcat
- workers.properties 文件，473–477
- 世界 Wide 网页联盟（World Wide Web Consortium），718
- Wusage 日志分析工具，233, 515
- www.domain.com.key 文件，563
- wwwstat 日志分析工具，233

## X
- x* (小写 x, 星号) 正则表达式元字符，710
- x+ (小写 x, 加号) 正则表达式元字符，710
- x? (小写 x, 问号) 正则表达式元字符，710
- \x9f (反斜杠, x9f) 正则表达式元字符，710
- Xfbthack 指令，381
- XFS6_SVGA 程序，701
- XFS 日志记录文件系统，652
    - 另请参见文件系统
- Xmas 端口扫描器，702

## Y
- Young, Eric A., 551

## Z
- zero, seven, seven (\0\7\7) 正则表达式元字符，710
- zone 文件，166, 639
    - 另请参见 DNS（域名服务）




## Hungry Minds, Inc. 最终用户许可协议

**请阅读此内容。** 在打开随本书（“本书”）提供的软件包装之前，您应仔细阅读以下条款和条件。这是您与 Hungry Minds, Inc.（“HMI”）之间的许可协议（“协议”）。通过打开随附的软件包装，您确认已阅读并接受以下条款和条件。如果您不同意且不愿受此类条款和条件的约束，请立即将本书及未开封的软件包装退还至购买处，以获取全额退款。

-   **1. 许可授权。** HMI 授予您（个人或实体）一项非独家许可，允许您在单台计算机上（无论是标准计算机还是多用户网络的工作站组件）将随附的一个或多个软件程序（统称“软件”）仅用于您自己的个人或业务目的。当软件被加载到临时内存（RAM）或安装到永久内存（硬盘、CD-ROM 或其他存储设备）时，即视为正在该计算机上使用。HMI 保留本条款中未明确授予的所有权利。

-   **2. 所有权。** HMI 拥有记录在磁盘或 CD-ROM（“软件介质”）上的软件汇编的所有权利、所有权和利益，包括版权。软件介质上记录的各个独立程序的版权归每个程序作者或其他授权的版权所有者所有。软件及其相关所有专有权利的所有权保留在 HMI 及其许可方手中。

-   **3. 使用和转让限制。**
    -   (a) 您只能 (i) 制作一份软件副本用于备份或存档目的，或 (ii) 将软件传输到单个硬盘，前提是您保留原始副本用于备份或存档目的。您不得 (i) 出租或租赁软件，(ii) 通过局域网（LAN）或其他网络系统，或通过任何计算机订户系统或电子公告板系统复制或复制软件，或 (iii) 修改、改编或基于软件创建衍生作品。
    -   (b) 您不得对软件进行反向工程、反编译或反汇编。您可以永久性转让软件及用户文档，前提是受让人同意接受本协议的条款和条件，且您不保留任何副本。如果软件是更新版本或已更新，任何转让人必须包含最新的更新版本及所有先前版本。

-   **4. 对个人程序使用的限制。** 您必须遵守本书附录 D 中为每个独立程序规定的个人要求和限制。这些限制也包含在记录于软件介质上的各个许可协议中。这些限制可能包括要求用户在指定时间段使用程序后，必须支付注册费或停止使用。通过打开软件包装，您即同意遵守附录 D 及软件介质中所述的这些个人程序的许可和限制。软件介质上的任何材料或本书中列出的任何内容，无论以原始形式还是修改形式，均永远不得用于商业用途进行再分发。

-   **5. 有限保修。**
    -   (a) HMI 保证，在自购买本书之日起六十（60）天的正常使用期间内，软件及软件介质不存在材料或工艺缺陷。如果 HMI 在保修期内收到有关材料或工艺缺陷的通知，HMI 将更换有缺陷的软件介质。
    -   (b) HMI 及本书作者否认除上述以外的所有其他明示或暗示的保修，包括但不限于适销性及特定用途适用性的暗示保修，涉及软件、程序、其中包含的源代码和/或本书中描述的技术。HMI 不保证软件中包含的功能将满足您的需求，也不保证软件的操作无错误。
    -   (c) 此有限保修为您提供特定的法律权利，您可能还享有因司法管辖区而异的其他权利。

-   **6. 补救措施。**
    -   (a) HMI 的全部责任以及您针对材料或工艺缺陷的唯一补救措施，应仅限于更换软件介质。您可以附上购货凭证，将软件介质退回至以下地址的 HMI：Software Media Fulfillment Department, Attn.: Apache Server 2 Bible, Hungry Minds, Inc., 10475 Crosspoint Blvd., Indianapolis, IN 46256，或拨打 1-800-762-2974。请允许四周至六周的交付时间。如果软件介质的故障是由事故、滥用或误用造成的，则本有限保修无效。任何更换的软件介质将在原保修期的剩余时间内或三十（30）天内（以较长者为准）获得保修。
    -   (b) 在任何情况下，HMI 或作者均不对因使用或无法使用本书或软件而引发的任何损害负责（包括但不限于商业利润损失、业务中断、业务信息损失或任何其他经济损失），即使 HMI 已被告知此类损害的可能性。
    -   (c) 由于某些司法管辖区不允许排除或限制对后果性或附带损害的赔偿责任，上述限制或排除条款可能不适用于您。

-   **7. 美国政府限制权利。** 代表美利坚合众国及其各机构和/或部门使用、复制或披露软件（“美国政府”），须遵守 DFARS 252.227-7013 中“技术数据和计算机软件权利”条款第 (c)(1)(ii) 款所述的限制，或 FAR 52.227-19 中“计算机软件 - 限制权利”条款第 (c)(1) 和 (2) 小款，以及 NASA FAR 补充条款中的类似条款（以适用者为准）。

-   **8. 一般条款。** 本协议构成各方的全部理解，撤销并取代各方之间先前达成的一切口头或书面协议，且除非由本协议双方签署并专门提及本协议的书面文件，否则不得修改或修订。本协议优先于任何可能与本协议冲突的其他文件。如果本协议中的任何一条或多条条款被任何法院或仲裁机构认定为无效、非法或不可执行，其余每一条款应继续完全有效。

Version 2, June 1991

Copyright © 1989, 1991 Free Software Foundation, Inc.
59 Temple Place, Suite 330, Boston, MA 02111-1307, USA

允许任何人复制和分发本许可文件的原样副本，但不允许更改。

# 前言

大多数软件的许可证旨在剥夺您共享和修改它们的自由。相比之下，GNU 通用公共许可证旨在保证您共享和修改自由软件的自由——确保软件对所有用户都是自由的。本通用公共许可证适用于自由软件基金会的多数软件，以及任何其作者承诺使用该许可证的其他程序。（自由软件基金会的某些其他软件由 GNU 库通用公共许可证覆盖。）您也可以将其应用于您的程序。

当我们谈论自由软件时，我们指的是自由，而非价格。我们的通用公共许可证旨在确保您拥有分发自由软件副本的自由（如果您愿意，可以为此服务收费），确保您能够获得源代码（如果您想要），确保您可以修改软件或在新自由程序中使用其部分代码；并且确保您知道您可以做这些事情。

为了保护您的权利，我们需要制定限制，禁止任何人剥夺这些权利或要求您放弃这些权利。如果您分发软件副本或修改软件，这些限制将转化为您需承担的特定责任。

例如，如果您分发此类程序的副本，无论免费还是收费，您必须给予接收者您所拥有的所有权利。您必须确保他们也能获得或获取源代码。您还必须向他们展示这些条款，以便他们了解其权利。

我们通过两步来保护您的权利：(1) 对软件进行版权保护，(2) 向您提供本许可证，该许可证给予您复制、分发和/或修改软件的法律许可。

此外，为了保护每位作者以及我们自身的利益，我们希望确保每个人都知道，此自由软件没有任何保修。如果软件被他人修改并传递下去，我们希望接收者知道他们所拥有的并非原始版本，以便由他人引入的问题不会反映在原始作者的名声上。

最后，任何自由程序都不断受到软件专利的威胁。我们希望避免自由程序的再分发者单独获得专利许可的风险，从而实际上使程序变为专有。为了防止这种情况，我们已明确表明，任何专利必须为所有人的自由使用进行授权，或者完全不授权。

复制、分发和修改的具体条款和条件如下。





# 复制、分发和修改条款与条件

0. 本许可证适用于任何包含版权声明的程序或其他作品，该声明由版权持有人发布，表明其可以依据本通用公共许可证的条款进行分发。下文中的“程序”指任何此类程序或作品，“基于程序的作品”是指程序本身，或根据版权法定义的任何衍生作品：也就是说，包含程序或其一部分的作品，无论是逐字复制、经过修改和/或翻译成另一种语言。（在此后文中，翻译被包含在“修改”这一术语中，不作任何限制。）每位被许可人被称为“你”。

除复制、分发和修改以外的活动不受本许可证覆盖：它们超出了其范围。运行程序的行为不受限制，只有当程序的输出内容构成基于程序的作品（无论是否由运行程序产生）时，才受其覆盖。这是否成立取决于程序的功能。

1. 你可以逐字复制并分发你收到的程序源代码的副本，可以以任何介质，前提是你必须在每份副本上显著且适当地发布适当的版权声明和免责声明；保留所有提及本许可证及无保修的声明；并随程序向其他接收者提供本许可证的副本。

你可以对物理传输副本的行为收取费用，并且你可以选择以费用为交换提供保修保护。

2. 你可以修改你拥有的程序或其任何部分的副本，从而形成一个基于程序的作品，并根据上述第 1 节的条款复制和分发这些修改或作品，前提是你还满足以下所有条件：

- a) 你必须使修改后的文件携带显著通知，说明你更改了文件及任何更改的日期。
- b) 你必须确保你分发或发布的任何作品，无论是全部还是部分包含或衍生自程序或其任何部分的，都必须作为一个整体，无偿地按照本许可证的条款向所有第三方授权。
- c) 如果修改后的程序在通常运行时交互式读取命令，你必须使其在以最普通的方式进行此类交互式使用的运行时，打印或显示一个公告，其中包含适当的版权声明和没有保修的通知（或者，如果你提供保修，则说明此点），并告知用户可以在这些条件下重新分发程序，以及如何查看本许可证的副本。（例外：如果程序本身是交互式的，但通常不打印此类公告，则基于程序的作品不需要打印公告。）

这些要求适用于修改后的作品整体。如果该作品中可识别的部分未从程序衍生，并且可以合理地被视为独立且分离的作品本身，则当你将它们作为独立作品分发时，本许可证及其条款不适用于这些部分。但是，当你将这些部分作为基于程序的作品的整体的一部分进行分发时，整个作品的分发必须符合本许可证的条款，该许可证对任何其他被许可人的许可扩展至整个整体，因此扩展到每个部分，无论由谁编写。

因此，本节的意图并非主张权利或质疑你完全由你编写的作品的权利；相反，其意图是行使控制基于程序的衍生或集体作品的分发的权利。

此外，仅仅是将未基于程序的另一作品与程序（或基于程序的作品）聚合在存储或分发介质的一卷上，并不会使该另一作品进入本许可证的范围。

3. 你可以按照上述第 1 节和第 2 节的条款，以目标代码或可执行形式复制和分发程序（或根据第 2 节基于程序的作品），前提是你还执行以下任一操作：

- a) 随附完整的相应机器可读源代码，这些源代码必须按照上述第 1 节和第 2 节的条款，在通常用于软件交换的介质上进行分发；或者，
- b) 随附一份书面要约，有效期至少为三年，向任何第三方提供一份完整的机器可读的相应源代码副本，费用不得超过你物理执行源代码分发的成本，该副本必须按照上述第 1 节和第 2 节的条款，在通常用于软件交换的介质上进行分发；或者，
- c) 随附你收到的关于分发相应源代码要约的信息。（此替代方案仅允许非商业分发，且仅当你收到的是目标代码或可执行形式的程序，并且附带了上述 b 款所述的要约时。）

对于作品而言，源代码是指对该作品进行修改的首选形式。对于可执行作品，完整源代码是指其包含的所有模块的所有源代码，加上任何相关的接口定义文件，以及用于控制可执行文件编译和安装的脚本。但是，作为特殊例外，分发的源代码无需包含通常与可执行文件运行的操作系统的主要组件（编译器、内核等）一起分发的任何内容（无论是源形式还是二进制形式），除非该组件本身随附在可执行文件中。

如果通过提供从指定位置复制的机会来分发可执行文件或目标代码，则提供从相同位置复制源代码的同等访问权也算作源代码的分发，即使第三方不被强制要求随目标代码一起复制源代码。

4. 除本许可证明确规定的情况外，你不得复制、修改、再许可或分发程序。任何其他试图复制、修改、再许可或分发程序的行为均无效，并将自动终止你根据本许可证享有的权利。但是，根据本许可证从你这里收到副本或权利的各方，只要这些各方保持完全合规，其许可证将不会终止。

5. 你无需接受本许可证，因为你尚未签署。但是，其他任何事物都不授予你修改或分发程序或其衍生作品的权限。如果你不接受本许可证，这些行为将违反法律。因此，通过修改或分发程序（或任何基于程序的作品），你表示你接受本许可证以执行这些操作，以及所有关于复制、分发或修改程序或基于程序作品的条款和条件。

6. 每次你重新分发程序（或任何基于程序的作品）时，接收者自动从原始许可人处获得一份许可证，允许其根据这些条款和条件复制、分发或修改程序。你不得对接收者行使本文件中授予的权利施加任何进一步限制。你无需对第三方遵守本许可证的行为负责。

7. 如果作为法院判决或专利侵权指控或任何其他原因（不限于专利问题）的结果，向你施加了条件（无论是通过法院命令、协议还是其他方式），而这些条件与本许可证的条件相矛盾，这些条件并不能免除你遵守本许可证条件的义务。如果你无法分发以同时满足你在本许可证下和其他相关义务下的责任，那么作为后果，你完全不得分发程序。例如，如果专利许可不允许所有直接或间接通过你收到副本的人无版税地重新分发程序，那么满足专利许可和本许可证的唯一方法就是完全停止分发程序。

如果本节的任何部分在特定情况下被裁定无效或不可执行，本节其余部分旨在适用，且本节整体旨在在其他情况下适用。

本节的意图并非诱导你侵犯任何专利或其他财产权主张，或质疑任何此类主张的有效性；本节的唯一目的是保护自由软件分发系统的完整性，该系统通过公共许可证实践得以实现。许多人依赖该系统的一致应用，对该系统分发的广泛软件做出了慷慨贡献；是否愿意通过其他系统分发软件由作者/捐赠者决定，被许可人不能强加这种选择。

本节旨在彻底阐明被视为本许可证其余部分后果的内容。

8. 如果程序在某些国家因专利或受版权保护的界面而受到分发和/或使用的限制，将程序置于本许可证下的原始版权持有人可以添加明确的地理分发限制，排除这些国家，以便分发仅允许在未被如此排除的国家之间或内部进行。在这种情况下，本许可证将该限制作为仿佛写在本许可证正文中的内容纳入。

9. 自由软件基金会可能会不时发布通用公共许可证的修订版和/或新版本。此类新版本在精神上与当前版本相似，但在细节上可能有所不同，以解决新问题或关切。

每个版本都有一个区分版本编号。如果程序指定了适用于它的本许可证版本编号以及“任何后续版本”，你有选择遵循该版本或自由软件基金会发布的任何后续版本的条款和条件的权利。如果程序未指定本许可证的版本编号，你可以选择自由软件基金会发布的任何版本。

10. 如果你希望将程序的部分纳入分发条件不同的其他自由软件中，请写信给作者请求许可。对于由自由软件基金会拥有版权的软件，我们有时对此做出例外处理。我们的决定将由两个目标指导：保护我们所有自由软件衍生物的自由地位，以及促进软件的一般共享和重用。





## 无保修

- **11.** 由于该程序是免费许可的，因此在适用法律允许的范围内，该程序不提供任何保修。除书面另行声明外，版权持有人和/或其他各方以“按原样”的方式提供该程序，不提供任何形式的明示或暗示保证，包括但不限于对适销性和特定用途适用性的暗示保证。有关程序质量和性能的全部风险均由您承担。如果证明程序有缺陷，您将承担所有必要的服务、维修或纠正的成本。

- **12.** 在任何情况下，除非适用法律要求或书面协议同意，任何版权持有人或任何可能按照上述允许修改和/或重新分发程序的其他方，均不对您承担损害赔偿责任，包括因使用或无法使用程序而导致的任何一般、特殊、偶然或后果性损害（包括但不限于数据丢失、数据被渲染为不准确、您或第三方遭受的损失或程序与任何其他程序无法协同工作的故障），即使该持有人或其他方已被告知此类损害的可能性。

## 条款和条件结束

