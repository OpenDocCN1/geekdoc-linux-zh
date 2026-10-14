
随着故事的继续，最终的赢家可能是终端用户，因为这实际上创建了三个相互竞争的办公套件。目前，LibreOffice 拥有最多的开发者、最强大的社区以及最成熟的软件，新增或改进功能的添加最快。

## Ubuntu 的其他办公套件

如前所述，LibreOffice 是 Ubuntu 的默认应用程序套件。然而，正如开源世界的常见情况，你会发现有很多 LibreOffice 无法满足你特定要求的替代方案。这些包括流行的 GNOME Office 以及 KDE 的默认生产力套件 KOffice。你可能会听到更多关于 LibreOffice 的特别是特别是越来越多的人意识到它通常兼容 Microsoft Office 文件格式。有趣的是，马萨诸塞州不久前决定采用两种文件格式作为政府标准：Adobe Acrobat PDF 格式和 OASIS OpenDocument 格式，两者在 LibreOffice 中都得到了原生支持。

> 马萨诸塞州决定将 PDF 和 OpenDocument 标准化对开源世界产生了巨大影响。这是 OpenDocument 这种开放标准第一次以这样被规定。这意味着任何想与州政府做生意的人必须使用基于 OpenDocument 的文件格式，而不是微软使用的专有格式。对微软来说，遗憾的是，它的任何应用程序中都没有对 OpenDocument 的支持，这使得它们对任何想要与州政府合作的人来说都是徒劳的。尽管微软是 OASIS 的创始成员，而 OASIS 正开发并批准了 OpenDocument 标准。

## 使用 GNOME Office

适用于 Ubuntu 的另一个办公套件是 GNOME Office，它是一系列应用程序的集合。与 LibreOffice 不同，GNOME Office 并没有一个连贯的应用套件，这意味着你必须使用一个与电子表格没有集成且无法直接处理演示文稿的文字处理器。然而，如果你只需要一两个组件，研究一下 GNOME Office 是值得的。

## GTK 组件集

开源开发者总是试图让人们更容易构建应用程序并帮助开发。为此，有许多组件或工具包供开发者可以使用快速创建和部署 GUI 应用程序。这些组件控制着下拉列表、另存为对话框、窗口按钮和整体视觉效果。遗憾的是，Windows 和 Apple 开发者只需要考虑一组组件，而 Linux 有许多不同的组件，包括 GTK+、QT 和 Motif。更糟糕的是这些组件之间是不兼容的，导致很难从一个组件轻松构建出一个完成的应用程序。

GTK 是 GIMP Tool Kit 的缩写。GIMP（GNU 图像处理程序）是一个与 Adobe Photoshop 非常类似的图形应用程序。通过使用基于 GTK 的术语，我们节省了数百字的输入量，并有助于我们对 GNOME Office 的讨论。在这些章节中，你可能还会看到对 QT 和 Motif 以及其他组件集的引用。

以下是 GNOME Office 套件的一些主要组件

在 Ubuntu 中提供了以下程序：

+   AbiWord—此文字处理程序允许你编写、格式化和组织文本文档，并与 Microsoft Word 文件格式具有某些兼容性。它使用插件（添加语言翻译等功能的程序）来增强其功能。

+   Gnumeric—此电子表格程序允许你以电子表格的格式操作数字。它支持除最生僻的 Microsoft Excel 函数以外的所有函数，这意味着用户在与 Excel 用户之间交换电子表格时不应遇到什么大问题。

+   GIMP—此图形应用程序允许你创建通用的图像。它可以导入和导出所有常见的图形文件格式。GIMP 类似于 Adobe 的 Photoshop 应用，并将在第 6 章“多媒体应用”中进行描述。

+   Evolution—Evolution 是一个邮件客户端，界面类似于 Microsoft Outlook，提供电子邮件、调度和日历功能。它它在第 4 章“在网上”中进行了描述。

被称为 GNOME Office 的应用程序散乱包含了一些额外的应用程序，这些程序重复了 Ubuntu 已经提供的应用程序的功能。这些额外的 GNOME 程序未包含在 Ubuntu 的默认安装中，以消除冗余。它们都可以从 GNOME Office 网站（www.gnome.org/gnome-office/）以及 Ubuntu 软件仓库获取。

## 使用 KOffice

KDE 套件 KOffice 的开发是为了提供与 KDE 桌面的紧密集成。这种集成允许通过拖放将一个应用程序中的对象插入到其他应用程序中，并且所有应用程序都相互通信，因此对象的更改会立即通知到其他应用程序。KDE 提供的应用程序集成是生产力的显著增强。（某些 GNOME 桌面应用程序之间也共享类似的通信设施。）如果你使用 KDE 桌面而不是默认的 GNOME 桌面，就可以享受这种集成带来的好处，以及 Konqueror 和文件浏览器的优势。

KOffice 的文字处理器是 KWord。KWord 是一个基于帧的文字处理器，这意味着文档页面可以在帧集中进行格式化，在封闭区域内保留文本、图形和对象。你可以使用帧集格式化页面上的文本，该页面包含文本和图像，文本需要环绕这些列流动，这使得 KWord 成为创建标准商务信函以外文档（如简报和手册）的绝选择。

KWord 和 KOffice 的其他组件是稳定的，但仍处于开发中，并且缺乏 LibreOffice 和 AbiWord 的所有精细功能。然而，它确实具有与 OpenDocument 格式工作的能力，以及与 Microsoft 文件格式的有限兼容性。

Office KSpread 客户端是一个功能性的电子表格程序，提供了图表功能以及所有其他标准的电子表格功能。

KDE 在 KOffice 中还包含了其他生产力选项。这些包括地址录、时间跟踪器、计算器、记事本和调度器。一个受欢迎的应用程序是 Kontakt，它提供了任务、待办列表和计划预约的每日、每周、工作周和每月视图，带有背景报警。

## 其他实用的生产力软件

本章已经讨论过的办公套件非常适合典型的以办公为中心的交互：创建基础文档、电子表格等。然而，我们中的有些人有更复杂或更精确的需求。本节涵盖了在这些情况下可以帮助你提高效率的一些选项。

## 使用 PDF

在 Ubuntu 中阅读 PDF 非常简单。得益于安装了 Evince 程序，该功能是默认可用的。打开 PDF，Evince 就会打开，你就可以阅读文档了。有时填写表单并不直观，因为表单可能是使用只有 Adobe 才有的功能创建的。你可以从 Ubuntu 软件中心从 Canonical 合作伙伴处安装 Adobe Reader。Adobe Reader 应该适用于任何使用 Adobe 软件创建的 PDF，无论它是在 Windows、Mac OS X 还是 Linux 上创建的。

偶尔你会发现自己有一个想要编辑的 PDF 文件。这稍微复杂一点，但不像以前那么困难了。Ubuntu 软件中心有一个专门为编辑 PDF 文件的程序。从表面上看，这个程序似乎足够简单，但它具有不言而易见的强大功能。高级用户可以学习在脚本中使用`pdfedit`来快速进行大规模更改。当然，对于大多数强大的工具，代价就是复杂性和学习如何使用它。

## 使用 XML 和 DocBook

DocBook 是 XML 的一种形式

像它的祖先 SGML 和兄弟 HTML 一样，XML 是一种标记语言。它是专门为文档设计的，标签包裹文本的特定部分以指示其显示方式。列表 5.1 包含一个示例

```
<?xml version="1.0"?>
<?xml-stylesheet type="text/css" href="book.css">
<book>
 <title>Ubuntu2013</title>
 <edition>8</edition>
 <chapter>
  <number>1</number>
  <title>安装 Ubuntu</title>
  <text>
   <paragraph><dropcap>N</dropcap>那个很久以来提到的...</paragraph>
   ...
  </text>
 </chapter>
...
</book>
```

这可以使用默认安装的简单文本编辑器（在 Ubuntu 软件中心可见）。然而，对于大多数人来说，这样做很乏味。更好的选择是使用专门为处理 XML 文件设计和设计的编辑器。由于 DocBook 是一种专为文档设计的开源 XML 标准，许多编辑器都可以处理它。如果你只需要快速做点事情，其中一个应该是合适的。从默认安装的 Gedit 开始。

如果你打算以仅Book 格式编写大量文档，Ubuntu 最常见的推荐是名为 Publican 的程序。Publican 不仅仅是一个编辑器，它还是 DocBook 发布系统。它测试你的 XML 以确保它是有效的，以便你的输出符合发布标准。它可以自动输出为 HTML 和 PDF 等多种格式，并允许对样式和格式进行完全控制。你可以从 Ubuntu 软件中心安装 Publican。
