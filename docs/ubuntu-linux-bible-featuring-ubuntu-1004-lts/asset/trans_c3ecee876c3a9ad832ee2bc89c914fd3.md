

## 第 1 章：Ubuntu Linux 项目

国际化（Internationalization）是指制作能够以任何用户的母语言以及该语言使用的任何特定字符集显示所有提示、对话框、系统消息等的软件的过程。“国际化”这个词非常难读，因此经常被称为 i18n，因为 internationalization 一词由字母 i 开头，中间中间隔了 18 个字母，最后以 n 结尾。i18n 翻译的两个方面是：确保操作系统版本和应用程序消息提供其他语言版本；以及本地化（localization），它确保消息和文本可以在该语言的本地字符（集）中进行显示。有趣的是，本地化通常被称为 l10n。

Linux 及其应用程序多年一直关注 i18n，诸如 Linux 国际化倡议（www.i18n.net/，被称为 Li18n）和自由标准小组的开放国际化倡议（www.open18n.org/）等倡议，都关注于确保开源应用程序在开发、维护和增强代码时考虑到 i18n。GNOME 和 KDE 等桌面环境最近几个版本中的许多结构性增强都与确保这些环境及其应用程序支持不同的语言和字符集有关。

成功国际化的关键在于两个方面——不仅应用程序和图形环境需要支持多种语言和字符集，而且提示、对话框和系统消息的翻译也必须可用。Ubuntu 致力于为国际化受众提供一个真正实用的 Linux 发行版，这使其成为 Linux（www.ubuntu.org/community/participatei10n）和 GNOME（其主要的图形环境）翻译和本地化工作的家园——后来通过名为 Rosetta 的在线翻译系统（https://launchpad.net/rosetta）、文档工作、活跃的邮件列表等实现。

### 提示

关于 Linux 国际化的更多信息，请通过简单的网页搜索“Linux internationalization”查看额外的网络资源，这将找到诸如《Linux 国际化 HOWTO》等优秀文档，它可以在 http://folk.no.net/davidjo/i18n.p. 等网站在线获取。

尽管 GNOME 和 KDE 等桌面环境最近几个版本中的许多结构性增强与国际化有关，但 way了大量工作使 Linux 环境让残障人士更容易使用。确保图形应用程序为所有菜单命令和对话交互提供键盘或手势快捷键，是 GNOME、KDE 和图形应用程序开发日益关注的焦点。Ubuntu 对可用性的强调对所有计算机用户都是一种福音，无论他们是否有物理残障。

### 提示

关于 Linux 无障碍功能项目和可用性意识的更多信息，请查看额外的网络资源，如《Linux Accessibility HOWTO》（www.tldp.org/HOWTO/Accessibility_HOWTO/）、《Linux Developers Accessibility HOWTO》（www.faqs.org/docs/Linux-HOWTO/Accessibility-HOWTO.html）以及 Linux 无障碍资源网站（http://swiki.atrc.utoronto.ca/wiki/）。

## 第一部分：开始使用 Ubuntu

## Ubuntu 发布计划

考虑到开源软件的开发速度，对于任何依赖 Linux 发行版的任何人来说，获取最新、最强大的内核和软件包版本都是关重要的。内核及相关驱动程序的改进提供了底级安全修复，方便了最新硬件的使用，并通常在处理设备和协议时提供了性能改进。软件包的最新版本通常在功能和可用性方面都有改进。开源社区模型几乎保证了在任何时候都有成千上万的改进正在进行，交付一个经过测试的最新且最强大的 Linux 内核和支持的软件包的集成版本是一项复杂的任务，但对于任何 Linux 发行版的成功和广泛采用极其重要。

Ubuntu 每六个月发布一个全新的 Ubuntu 版本。这些定期发布提供了最新的、经过测试的内核以及一组经过良好测试的集成用户软件，包括来自 X.Org 的 X Window 系统版本、最新的 GNOME 桌面以及核心 Linux 和 GNOME 应用程序（包括 Ubuntu 特定的应用程序和定制）。

定期发布计划在 Linux 领域是独一无二的，这导致了 Ubuntu 发布版本命名的一种独特方法。传统的软件发布根据主版本和次要版本进行编号，其中主版本号基本上是任意的，通常表示功能上的某些重大升级。例如，在传统的版本命名中，版本 4.2 是版本 4.1 之后的软件版本 4 的次要版本。然而，Ubuntu 使用主版本号来标识软件发布的年份，而看起来像次要版本的数字实际上代表发布的月份。因此，版本 8.04 是 2008 年第四个月发布的 Ubuntu 版本。按照典型的轻量级 Linux 风格，每个 Ubuntu 版本也有一个昵号。以下是目前为止的 Ubuntu 版本：

- 4.10: Warty Warthog（疣皮疣牛）
- 5.04: Hoary Hedgehog（苍老刺猬）
- 5.10: Breezy Badger（微风土拨）
- 6.06 LTS: Dapper Drake Long Term Support release（优雅龙类的长期支持版本）
- 6.10: Edgy Eft（锋利大鲵）
- 7.04: Feisty Fawn（活泼小鹿）
- 7.10: Gutsy Gibbon（勇敢长臂猿）
- 8.04 LTS: Hardy Heron Long Term Support release（硬朗白鹤长期支持版本）
- 8.10: Intrepid Ibex（探险山羊）
- 9.04: Jaunty Jackelope（活泼的山羚）
- 9.10: Karmic Koala（因果考拉）
- 10.04: Lucid Lynx Long Term Support release（明智猞猁长期支持版本）
- 10.10: Maverick Meerkat（无赖猫��）

## 第 1 章：Ubuntu Linux 项目

这是一种全新的版本命名方法，特别是在本质上处于持续开发的开源领域。它不仅让用户和系统管理员能够预测并调度系统更新，还使得在不查阅参考文本或网络的情况下，能够轻松识别已安装系统的年代。

## Ubuntu 更新与维护承诺

发行版的发布频率对于任何用户来说都非常重要，以确保他们能够获得最新、最强大的系统和应用程序软件。然而，对于任何对 Linux 的强大、成本效益和灵活性感兴趣的企业来说，版本获得更新和维护的时间跨更为重要。许多企业拥有数百或数千台计算机系统。在部署系统上有大量基础设施的企业在考虑推广之前，会花费大量测试更新和新版本。一旦测试完成，更新部署系统的物理操作需要大量时间，这在 IT 人员眼中直接意味着大量的分钟。

默认情况下，每个 Ubuntu 版本的安全更新将在发布日期后发布 18 个月——在那之后，现有的安全更新仍然可用，但无法保证为该版本提供新更新。为了满足商业用户的长期需求，Mark Shuttleworth 和 Ubuntu 的创始人兼赞助者 Canonical, Ltd. 于 2005 年中期成立并资助了 Ubuntu Foundation。Ubuntu Foundation 聘佣了一些 Ubuntu 社区成员来帮助保证 Ubuntu 开发和发布过程的成功和持续。Ubuntu Foundation 的一个方面是增加了维护和更新的承诺。Ubuntu 6.06 是第一个从此受益的 Ubuntu 版本，当时 Ubuntu Foundation 宣布 Ubuntu 6.06 在桌面端支持三年，服务器端支持五年，将标准的 18 个月承诺翻了一倍。LTS（长期支持）缩写被添加到其版本号中以强调这一事实。长期支持承诺对任何 Ubuntu 用户都有价值的，因为它们保证了在更长时间内提供支持和更新，但对于企业用户尤为重要，他们需要选择一个稳定且长期的平台来满足企业计算需求。

## Ubuntu 与 Debian 项目

Debian 是可用最长寿 Linux 发行版之一，也是 Ubuntu Linux 的概念父级 Linux 发行版。Debian 的读音为“Deb-yan”，e 发软音，是 Debian 项目创始人 Debra 和 Ian 名字的缩写。

