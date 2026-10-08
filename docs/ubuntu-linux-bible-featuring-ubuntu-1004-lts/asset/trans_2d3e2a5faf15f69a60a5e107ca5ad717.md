
OpenOffice 是 Web 上最强大且流行的开源项目之一，它的存在很大程度上归功于 Oracle 公司原甲骨微系统（Sun Microsystems）的成员。甲骨微系统总裁斯科特·麦尼利（Scott McNealy）与微软有着长期的竞争关系，因此 1999 年甲骨文收购了德国供应商 StarDivision（该公司拥有一名为 StarOffice 的办公软件套件），这并不令人意外。收购 StarOffice 最初被视为利用甲骨文 Java 产品的一种方式（因为 StarOffice 和 OpenOffice 都高度依赖 Java），并为用户提供一套可以在工作站上原生运行的办公套件。

甲骨文根据 Sun 行业标准源许可证（ISSL）的条款，将当时当前的 StarOffice 源码发布到了开源社区。从 OpenOffice.org 2.0 版本开始，所有代码现在都可以在 GNU 较小通用公共许可证（LGPL）下提供。甲骨文仍在销售 StarOffice，它既得到了支持，又提供了超出 OpenOffice.org 的功能——但那是我们他们的事了，因为 StarOffice 无法在 Ubuntu Linux 上运行。

除了强大和免费之外，使用 OpenOffice.org Writer 的一个真正吸引人的理由是它使用了新的 OpenDocument 格式（ODF）标准来存储和交换文档（www.oasis-org/committees/tc_home.php?wg_abbrev）。从历史上，所有的文字处理器都使用自己的专有格式存储文档，这使得在不同文字处理器之间切换，或者仅仅与使用不同文字处理器的朋友或同事交换文档变得变得困难。OpenDocument 标准旨在提供一种发布的标准，以 XML 格式存储文档，使其能够立即在支持该格式的任何其他文字处理器中使用。这看起来可能是一件小事，但当你尝试打开为家族史、短篇小说或其他很久以前写过但仍想使用的 WordStar 文件后，再来找我吧。

## 提示

如果你对文档标准感兴趣或偶尔阅读新闻，你可能知道 ODF 和微软的 OOXML（开放 XML）标准之间有一场“角跤”比赛，争夺谁能成为开放文档标准。OOXML “赢”了这场战斗，但我看来，使用 OOXML 是愚蠢的。一个超过 5,000 页的标准（而且在本书时甚至连微软自己的工具都不符合标准）在我来说并不算是一个真正的标准。使用 ODF 并拒绝微软的最新产品吧。他们的工具和操作系统是臃肿软件是一回事——

为了避免在本节其余部分中不必要地多次使用 OpenOffice.org Writer 这个短语，我通常会将 OpenOffice.org 称为 Writer（它对朋友的称呼），或者偶尔称为 owriter（你从命令行界面执行 OpenOffice.org Writer 时必须输入的应用程序名称）。

## 第二部分：面向桌面用户的 Ubuntu

## OpenOffice.org 文档的文件扩展名

随着 OpenDocument 格式的采用，OpenOffice.org Writer 修改了其默认文件扩展名以反映新格式。以下列表显示了不同 OpenOffice.org 版本使用的文件扩展名：

- odm: OpenDocument 主文档
- odt: OpenDocument 文档，适用于 OpenOffice.org 2.0 及更高版本
- ott: OpenDocument 模板，OpenOffice.org 2.0 及更高版本
- sxw: OpenOffice.org 2.0 之前的 Writer 文档
- stw: OpenOffice.org 2.0 之前的 Writer 主文档

你将看到并创建的最常见文档是带有 .odt 和 .ott 扩展名的文件。然而，在与长期用户交换文档时，你可能会遇到旧的 .sxw 格式。SXW 文件非常有趣，因为它们实际上是包含 XML 文档文件相关元数据的压缩包。你必须使用“文档转换向导”将旧格式的 SXW OpenOffice.org 文件导入新的 OpenDocument 格式，正如本章后面“从其他文字处理器导入文档”节所解释的那样。

## 安装 Writer 文件

如果你通过 Live CD 安装 Ubuntu，或者通过使用文本模式安装程序的备用安装 CD、OEM 模式安装程序安装 Ubuntu，则默认会安装 Writer。如果你想在具有图形界面的服务器系统上添加 Writer 或整个 OpenOffice.org 套件，你可以使用第 19 章中讨论的任何包管理工具进行安装。

Ubuntu 与其他 Linux 发行版的区别之一在于它们对用户极度的投入的奉献，特别是在国际化方面。如果你在单一语言环境下工作，默认的 Ubuntu 安装会带有适用于你物理位置的正确本地化包。然而，如果你安装 Writer 是为了创建多种语言的文档，你可能还想搜索并为你要编写的任何语言安装适当的连字符、本地化和词典包。你可以通过寻找代表你所寻找的国家代码的字符串来找到它们。例如，图 13-3 显示了通过在包管理工具中搜索字符串 -de 出的 OpenOffice.org 特定德语支持包。

## 第 13 章：创建和发布文档

## 提示

你可以通过安装适用于目标区域的适当语言支持元包（例如 `language-support-country-de`），为所有应用程序安装完整的语言支持（不翻译 GNOME 框架本身）——这些包的格式为 `language-support-country-code`，并包含指定区域的词典。要完全翻译 GNOME 界面和所有国际化应用程序，请选择格式为 `language-pack-country-code` 的适当语言包。一旦安装了多个词典，你就可以在 Office 应用程序中使用工具 ◇ 选项 ◇ 语言设置 ◇ 下拉菜单设置文档的默认语言。你还可以使用语言菜单中的命令设置文档各个部分的默认语言。

图 13-3

OpenOffice.org 套件的示例附加语言包

![](img/1a233c34336f5a8d6eb785e401709_508.png)

## 概览 Writer

你可以通过命令行执行 `writer` 命令来启动 Writer。更方便的是，应用程序 ◇ 菜单中安装了一个名为“OpenOffice.org 文字处理器”的菜单项。从菜单选择此项即可启动 Writer。应用程序启动并显示空白文档，如图 13-4 所示。

## 第二部分：面向桌面用户的 Ubuntu

## 图 13-4

启动 Writer

![](img/1a233c34336f5a8d6eb785e401709_509.png)

## 熟悉 Writer

Writer 提供了优秀的在线帮助，OpenOffice.org 套件中的所有工具也是如此，所以我不会通过带你遍历它包含的每个菜单和条目来让你。然而，作为 Writer 界面的快速概述，图 13-4 中的标记了以下区域：

- 菜单：Writer 中的下拉菜单组织方式与 Microsoft Word 类似，提供了熟悉的用户体验。右侧带有箭头的菜单项指向其他相关的菜单。
- 工具栏：Writer 默认显示标准工具栏和格式工具栏，点击相应的图标即可对特定命令进行一键访问。你可以通过点击位于最右侧的工具栏控件来修改工具栏上显示的图标列表。你可以通过“查看 ◇ 工具栏”子菜单显示其他工具栏或禁用默认工具栏。
- 标尺：这些标尺显示当前文档中文本插入点的水平和垂直位置。每个标尺的灰色部分反映了当前文档使用的页边距。你可以通过切换“查看 标尺”菜单命令来隐藏这些标尺。

