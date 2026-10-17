
# Red Hat Linux 9 入门指南

## 作者简介

Sandip Bhattacharya 是一位独立技术顾问，专门研究开源技术。他是红帽认证工程师（`RHCE`），拥有工程学和管理学学位，并撰写了多本关于开源软件的书籍和文章。他目前经营 `Puroga Technologies`，这是一家初创公司，专注于帮助企业利用开源革命的优势。他可以通过 `sandip@puroga.com` 联系。`Sandip` 是印度各种开源社区的积极参与者，特别是他当地的 `LUG`，即德里印度 `Linux` 用户组（`ILUGD`）。

`Pancrazio "Ezio" de Mauro` 自 1996 年以来一直使用 `Red Hat Linux`。他是一位 `Linux` 顾问，专门从事系统集成、移动技术和培训。他积极支持和倡导使用自由软件。`Ezio` 大部分空闲时间都在旅行和背包徒步。他欢迎通过他的电子邮件地址 `pdm@demau.ro.net` 发表评论和提问。

`Shishir Gundavaram` 是 `MechanicNet Group` 的首席技术官，该公司专门提供面向汽车修理和维护行业的 `CRM` 服务。当他不处理汽车机械师和抛锚的汽车时，`Shishir` 为多家公司提供咨询，设计架构并提供专业技术支持。他在软件开发的各个方面拥有十多年经验，被认为是无线应用、分布式系统、电子商务和 `Web` 后端架构领域的顶尖专家。他还是多篇技术文章和书籍的作者，包括 `Professional Perl Development`、`CGI Programming on the World Wide Web` 和 `Scripting Languages: Automating the Web`，并经常受邀在全球各地的技术会议上演讲。

`Mark Mamone` 是英国 `Syntegra Ltd` 的解决方案专家，拥有 16 年的 `IT` 行业经验，涵盖汇编语言和 `MS-DOS`，目前专门使用多种技术开发企业级和移动系统，包括 `Microsoft .NET`、`Java` 和 `Linux`。我要感谢我的父母送给我一台 `Commodore Vic-20`，没有它，我的人生永远不会走上这条道路。我要感谢我的孩子——`Tanya`、`James` 和 `Cameron`——他们的爱是我的基石，最重要的是，我的女朋友 `Rachel`，她的支持、爱和永不停歇的动力使我完成了这本书！

`Kapil Sharma` 是一位互联网安全和 `Unix` 顾问，多年来一直从事各种 `Unix` 系统和互联网安全技术工作。他已部署了许多 `Unix`、高可用性、集群和互联网安全项目。`Kapil` 也是 `Sun` 认证系统管理员（`SCSA`）和 `Sun` 认证网络管理员（`SCNA`）。他喜欢在互联网安全、互联网架构设计以及各种 `Unix` 变体方面的新挑战中工作。他还热衷于技术写作并与社区分享知识。他积极参与开源社区，并撰写了许多关于系统和网络安全的技术文章。除了繁忙的技术生活外，`Kapil` 还喜欢夜生活、音乐和周游世界。`Kapil` 目前与其妻 `Usha Sharma` 居住在英国伦敦，可通过电子邮件 `kapil@linux4biz.net` 联系。他在 `www.linux4biz.net` 维护一家咨询公司和一个载有大量安全资源的网站。这本书献给我挚爱的妻子 `Usha Sharma`，感谢她持续的支持、爱以及夜晚的一杯杯咖啡，没有这些，这本书将只是一个梦想。我感谢我的父母 `Girdhari Lal Sharma` 和 `Bimla Devi Sharma`，他们在我生活中提供了持续的支持和激励。

`Deepak Thomas` 生活和工作在旧金山湾区。他的兴趣包括 `PHP`、`Linux` 和 `J2EE` 技术。他与 `Ansu` 共同撰写并审阅了 `Wrox` 在这些领域的几本书。在空闲时间，`Deepak` 和 `Ansu` 会沿着他们所在国家许多美丽的骑行小径骑自行车。

`Simon Whiting` 毕业于剑桥大学克莱尔学院，是 `AnlX Group Ltd` 的高级顾问，曾任 `Unix` 系统管理员。他是 `Linux`、存储区域网络（`SAN`）以及 `C`、`Perl` 和 `Korn Shell` 编程方面的专家。

## 引言

`Linux` 正在迅速成为世界操作系统领域的主要力量——它速度快、稳定性高，而且最重要的是，它是免费可用的。在 `Linux` 市场中，`Red Hat Linux` 拥有最流行发行版的殊荣，而使用 `Red Hat Linux 9`，它的安装和使用比以往任何时候都更容易！

本书教你安装、配置、使用和维护 `Red Hat Linux` 系统所需知道的一切。它是专门为 `Red Hat Linux 9` 编写的，但如果你计划使用其较旧的版本 `Red Hat Linux 8.0` 以及任何后续版本的 `Red Hat Linux`，你会发现它也是一份非常实用的指南。

### 本书适合谁？

本书主要面向那些第一次使用（或计划使用）`Red Hat Linux` 操作系统的读者。它提供了简单、直白的指导，帮助你开始探索开源软件的巨大潜力。

我们假设读者在接触 `Linux` 之前已经熟悉使用操作系统，例如 `Apple` 的 `Macintosh`、`Unix` 或众多版本的 `Microsoft Windows` 操作系统。了解文件系统、应用程序以及用户和权限等概念会有帮助，但并非必需；本书将为那些尚未考虑过这些概念的读者提供见解。

本书不假设读者具备任何 `Linux` 的先前知识。

### 使用本书所需的条件

使用本书，你只需要一台**机器**和一份 `Red Hat Linux 9` **发行版**。最简单的选项（也是我们在本书中使用的选项）需要：

- 一台你可以专门用于安装 `Red Hat Linux 9` 的机器。`Red Hat` 建议最低配置为 `Pentium` 级别 `CPU`，配有 `650MB` 硬盘空间和 `128MB` 内存，但为了获得更好的性能，推荐 `200MHz Pentium` 处理器，配有 `2.5GB` 硬盘空间和 `192MB` 内存。它还表示，过去两年内制造的大多数工厂组装机器都兼容 `Red Hat Linux 9`，许多较旧的机器也兼容。（有关硬件兼容性的更多信息，请参见第 1 章和 `http://hardware.redhat.com`。）

- 随本书附带的一份 `Red Hat Linux 9` 副本。

### 其他替代方案

获取 `Red Hat Linux 9` 发行版还有其他方法。你可以：

- 通过 `FTP` 免费下载 `Red Hat Linux 9` 发行版镜像，并将其刻录到 `CD` 上。然而，这相当复杂——例如，你需要一个 `ISO` 刻录软件（这是一种在将 `ISO` 文件刻录到你选择的介质时解包 `ISO` 文件的软件）。如果你觉得有挑战性，请遵循 `http://www.redhat.com/download/howto_download.html` 上的指南；该发行版在全球多个镜像站点均可获得。

- 从第三方供应商处以低价购买安装光盘。然而，这些光盘通常不提供技术支持，也没有文档。

也可以将 `Red Hat Linux 9` 作为双启动设置的一部分安装在你的机器上。如果你只有一台机器，并且不想放弃你的 `Windows` 或其他操作系统，这将给你一个选择。

虽然欢迎探索这些替代方案，而且它们与你在本书中发现的内容完全兼容，但我们不会详细讨论它们。

# 什么是 Linux？

当你问一个 `Linux` 爱好者这个问题时，他们的答案几乎总会提到 `Linus Torvalds` 和开源社区。正如你将在我们简要的历史中看到的那样，`Linux` 在 `Linux` 的创建和发展中是一个关键角色，而 `Linux` 的开源根源是其受欢迎程度的核心。

## Linus Torvalds 和 Linux 的诞生

`Linus Benedict Torvalds` 当时在芬兰的赫尔辛基大学学习，他对计算的兴趣导致他对操作系统以及如何在当时的现有系统——特别是各种 `Unix` 衍生系统——上做出改进感到好奇。随着这一小步，`Linux` 内核（其核心）的开发开始了；并在 1991 年 10 月，版本 `0.02` 通过以下这一著名的帖子发布到互联网上：

> `From: torvalds@klaava.Helsinki.FI (Linus Benedict Torvalds)`
>
> `Newsgroups: comp.os.minix`
>
> `Subject: Free minix-like kernel sources for 386-AT`
>
> `Message-ID: <1991Oct5.054106.4647@klaava.Helsinki.FI>`
>
> `Date: 5 Oct 91 05:41:06 GMT`
>
> `Organization: University of Helsinki`
>
> `Do you pine for the nice days of minix-1.1, when men were men and wrote their own device drivers? Are you without a nice project and just dying to cut your teeth on an OS you can try to modify for your needs? Are you finding it frustrating when everything works on minix? No more all-nighters to get a nifty program working? Then this post might be just for you :-)`
>
> `As I mentioned a month(?) ago, I'm working on a free version of a minix-lookalike for AT-386 computers. It has finally reached the stage where it's even usable (though may not be depending on what you want), and I am willing to put out the sources for wider distribution. It is just version 0.02 (+1 (very small) patch already), but I've successfully run bash/gcc/gnu-make/gnu-sed/compress etc under it.`
>
> `Sources for this pet project of mine can be found at nic.funet.fi (128.214.6.100) in the directory /pub/OS/Linux.`
>
> `The directory also contains some README-file and a couple of binaries to work under linux (bash, update and gcc, what more can you ask for :-). Full kernel source is provided, as no minix code has been used. Library sources are only partially free, so that cannot be distributed currently. The system is able to compile "as-is" and has been known to work. Heh. Sources to the binaries (bash and gcc) can be found at the same place in /pub/gnu.`

这听起来并不像那种你可以用来处理家庭账户的系统，对吧？然而，关于这个软件发布有一个非常重要的一点：它是根据 `GNU 通用公共许可证` 发布的，该许可证允许源代码免费分发给任何想要它的人，并且允许这些人随意扩展它。

很快，感兴趣的程序员和测试员群体采用了 `Linus` 的原始代码，并以各种方式对其进行扩展。他们扩展了 `Linux` 可以运行的硬件配置范围，增加了为 `Linux` 编写的软件范围，并提高了整个 `Linux` 系统的稳定性。这种支持和开发一直持续到今天，遍布全球并涵盖了整个开发者社区。

## 简介

当然，这种现象及其潜力已在商业领域被注意到，如今 `Linux` 已拥有一批健康的商业供应商，他们实现了看似不可能的事情——通过销售本质上免费的产品来开展业务！当然，为了做到这一点，这些组织（包括 `SuSe`、`Debian`、`Mandrake`、`Red Hat` 等）不得不进行创新，并在基础 `Linux` 软件包中添加附加值。这些组织创建的各种发行版、软件包和附加组件已随着基础 `Linux` 操作系统本身一起成熟起来。

最新的 `Red Hat Linux` 发行版——第 9 版——正是这种创新的完美典范。虽然它可以免费下载，但 `Red Hat` 也以多种形式销售该软件包。对于家庭用户，有一套盒装光盘，其中包含 `Linux` 操作系统、大量开源生产力软件、`Red Hat` 专利的 `Bluecurve` 界面，以及 `Red Hat` 网络的演示订阅——这是供应商的支持、更新和信息网络。对于企业用户，交易方式大致相同，但更强调支持服务。

最后，通过个人开发者社区和发行版供应商的共同努力，现在已有 `Linux` 版本可以与 `Microsoft Windows` 等专有软件在公平的竞争环境中一较高下。这意味着 `Linux` 无论是在您的家庭 `PC` 还是大型生产环境中，都是一位有力的竞争者。

## 为什么选择 Linux？

您可能会因为什么而选择 `Linux` 作为您的操作系统，而不是其竞争对手呢？以下是您可能需要考虑的几个要点：

- `大小和速度`：基本的 `Linux` 安装可以占用尽可能少的 `475MB` 硬盘空间，并且可以非常流畅地运行在仅有 `64MB` 内存的系统上。将此与 `Unix`（通常要求超过 `500MB`）或 `Microsoft Windows 2000`（建议最低 `2GB` 硬盘和 `128MB` 内存）进行比较。这种差异归因于 `Linux` 操作系统的效率以及（大多数）运行在其上的应用程序。

- `安全性`：`Linux` 作为安全环境的卓越声誉的一个重大原因是其源代码完全可访问，并且持续受到许多双重视角的审视。`Linux` 的开源立场意味着*除了供应商以外*的人可以检查不完整或被篡改的源代码。研究 `Linux` 源代码的人越多，就能发现更多的错误（和安全漏洞）。当然，这只是故事的一半——另一半是基础设施已就位，便于错误报告、讨论和修复。所有这一切的结果是，*更多的错误*被*更快地*发现，并且修复得更快。

除了可用的众多安全应用（如防火墙）外，许多 `Linux` 发行版是*专门*创建以提供高度安全环境的。例子包括 `Immunix OS`（`http://www.immunix.com` – 一种商业可用的加固 `Linux`）和 `Bastille Linux`（`http://www.bastille-linux.org` – 一种可以在安装后在您的 `Linux` 机器上运行的加固脚本）。

- `标准和支持`：`Linux` 对 `Unix` 标准的符合使其能够与多种不同的操作系统和文件系统互操作。`Linux` 可以轻松与 `Netware`、`Macintosh` 和 `Windows` 网络通信。

- `GNU 软件支持`：通过 `GNU` 计划可以自由获得多种软件——包括开发软件、办公应用程序、系统管理工具等。`OpenOffice` 应用程序套件就是一个例子，并在第 5 章中详细讨论。您会在本书中遇到其他软件，我们在第 13 章中调查了一些开源应用程序的选择。

- `图形用户界面（GUI）支持`：如果您喜欢通过带有窗口、面板和菜单的精美图形用户界面（`GUI`）与操作系统通信，那么 `Linux` 将令您满意。无论您是使用 `GUI` 来提高生产力还是仅仅为了娱乐，您都可以从许多 `GUI` 中进行选择，包括 `Bluecurve`、`KDE` 和 `GNOME`。

此外，`Linux` 并不强制您使用操作系统 `GUI`，对于那些愿意探索命令行界面（`CLI`）的人来说，好处包括更大的灵活性和更低的开销。正是出于这个原因，许多严肃生产环境中的服务器管理员舍弃 `GUI`，以换取更好的灵活性和性能。

- `成本`：`Linux` 是免费可用的——您还能说什么呢？！如果您是企业客户，健康的供应商竞争使得支持合同价格非常合理。

## 什么是 Red Hat Linux 9？

如前所述，许多组织已经创建了 `Linux` 的发行版。通常，`Linux` 发行版包括特定版本的 `Linux` 内核、一组组件和应用程序、安装程序（通常与 `Windows` 平台关联的类型），以及某种支持安排。

最受欢迎的发行版之一来自 `Red Hat` 公司——事实上，根据您阅读的市场报告独立研究，`Red Hat` 目前占据 `Linux` 供应商市场 50% 以上的份额。

`Red Hat Linux` 有多种不同版本，包括：

- 个人版（目前为第 9 版）

- 专业版（目前为第 9 版）

- 高级服务器版（目前为 2.1 版）

- `Itanium` 版（64 位处理器 – 目前为 7.2 版）

每个版本都包含适合某些场景的功能；这些场景是：

- 小型办公室或家庭

- 小型或中型企业

- 企业或公司应用

以下矩阵展示了哪些版本适合哪些场景：

| | 家庭 | 小型企业 | 中型企业 | 大型企业 | 企业级 | 其他 |
|---|---|---|---|---|---|---|
| 个人版 | √ | √ | | | | |
| 专业版 | √ | √ | √ | | | |
| 高级服务器版 | | | √ | √ | √ | |
| Itanium | | | | | | √ |

注意：为简单起见，表格中的企业级条目是 `Red Hat` 提供的不同版本的合并；这些品牌被称为 `AS`、`ES` 和 `WS`。如需了解这些的更多信息，请查看 `http://www.redhat.com/software/rhel/`。

您会注意到我们使用勾号来表示某个版本适合特定场景，但表中没有放置任何叉号。这是故意的：如果您是那种拥有家庭网络并希望通过高级服务器版提供的某些高级功能来使用它们的强大用户，那么为什么不呢？`Linux` 的美妙之处在于它是开放的，并且对硬件要求远低于其他操作系统。

所以，您那台藏在桌子下面、注定要进垃圾堆的旧机器，也许还是有用的——把它拿出来，安装 `Red Hat Linux 9`，并将其用作 `Web` 服务器或打印服务器！

## 本书涵盖的内容？
