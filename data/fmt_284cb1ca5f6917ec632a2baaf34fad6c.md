
如果你正在处理 LaTeX 文档，Kite 或 Lyx 处理器的便利性是无可比拟的。Kite 是一个基于 KDE 的应用程序，为标准 LaTeX 文档提供了一个极其完备的编辑环境，为创建各种文档元素提供了向导（表格向导尤其令人印象深刻），提供了公式的快速设置（在哪里以及何时结束），以及一个非常实用的工具箱，你可以通过简单的鼠标点击选择并插入 LaTeX 结构。如果你是 LaTeX 的初学者，无论你使用的是 Ubuntu 还是 Kubuntu，我都强烈推荐使用 Kile。在我看来，在标准的 GNOME-Ubuntu 系统上安装 Kile 的要求是非常值得的。图 16-3 显示了在 Kite 中相同的 LaTeX 文档。

作为一个 KDE 应用程序，Kile 配置为使用其他基于 KDE 的 TeX 和 LaTeX 应用程序。其中最重要的是 `kdvi`，它是 KDE DVI 文件查看器。虽然你可以配置 Kile 使用标准的 xdv DVI 查看器（通过选择 Settings > Configure Kite 菜单项并修改在 Tools > Build > ViewDVI 中定义的查看 DVI 文件的命令），但如果你正在使用 Kile，可能可能在你的系统上安装 `kdvi` 软件包。图 16-4 显示了我们在使用 Kile 的 `QuickBuild` 命令生成后，在 `kdvi` 中预览的示例 LaTeX 文档！

# 创建与发布文档

## 关于 TEX 和 LaTeX 的更多信息

因为 TEX 和 LaTeX 已经在各种系统中使用了多年，网络上有大量关于它们的信息。简单的互联网搜索就能带给你超出预期的信息。为了方便，我最喜欢的关于 TEX 和 LaTeX 的网站如下：

- [Getting grips with LaTeX](https://andy-roberts.net/misc/latex/index.html) 是 Andrew Roberts 关于 LaTeX 的系列教程。
- [Introduction to LaTeX](https://math.uic.edu/~hildebr/detx/) 是伊利诺伊大学数学系准备的一个短期课程，提供了 TEX 的快速预览。
- [Text Processing with LaTeX](https://www.eng.cam.ac.uk/help/tpl/textprocessing) 是剑桥大学的一个优秀网站，提供了许多在线教程和示例。
- [The TEX HOWTO](https://tdp.org/HOWTO/TEX-HOWTO.html) 讨论了 Ubuntu 和 Kuhn 系统使用的旧版本 LaTeX。该 HOWTO 编写于几年前，但它涵盖了像 TEX 这样不会发生太大变化的软件的内容。本文档提供了许多关于创建 TEX 和 LaTeX 文档的信息，但你应该忽略任何关于 TEX 实现的具体信息。

有很多关于 TEX 和 LaTeX 的书籍，在 Amazon.com 上进行快速搜索可以提供多种选择。然而，如果没有识别以下书籍，任何关于 TEX 和 LaTeX 的讨论都是不完整的：

- *TEXbook* 作者 Donald E. Knuth (Addison-Wesley Professional, 1984, ISBN: 0201134489)
- *LaTeX: A Document Preparation System, 2nd Edition* 作者 Leslie Lamport (Addison-Wesley Professional, 1994, ISBN: 0201529831)

这些书籍的作者是各自系统的，你可以参考它们。虽然自 Lamport 很久以前创立 LaTeX 以来确实发生了一些变化，但它们仍然这两个文档准备系统的圣经。

### 第二部分：面向桌面用户的 Ubuntu 和 Kubuntu

购买 StarOffice 最初被视为一种利用 Sun（太阳公司）产品的方式（因为 StarOffice 和 OpenOffice.org 深度依赖 Java），同时也为了为 Sun 用户提供了一套可以在其工作站上直接运行的办公套件。

随后，Sun 根据 Sun 行业源许可证（SISL）条款，将当时的 StarOffice 源代码发布到了开源社区。随着 OpenOffice.org 2.0 版本的发布，所有源代码现在都已根据 GNU 较级通用公共许可证（LGPL）提供。Sun 仍在营销 StarOffice，它获得了支持并提供了由 OpenOffice.org 的某些功能——但这对大多数人来说没有，因为 StarOffice 无法在 Linux 上运行。

除了强大和免费之外，使用 OpenOffice Writer 的另一个真正具有吸引力的理由是使用了新的 OpenDocument 格式（ODF）来存储和交换文档（www.oasis-open/committees/tc_home?abbrev=office）。从历史上来看，所有的文字处理器都使用专有的二进制格式来存储文档，这使得在不同文字处理器之间切换，或者与使用不同处理器的朋友或同事交换文档时变得非常困难。OpenDocument 标准旨在为 XML 格式的标准文档提供基准，该格式可以被任何支持该格式的文字处理器使用。这看起来可能是一件小事，但在你尝试打开 StarOffice 文件后，你就会发现它的了——历史记录、短故事或其他很久以前编写的文档仍然可以使用它。

> 提示：如果你对文档标准感兴趣或正在阅读它们，你可能知道 ODF 和微软的 OOXML（Open Office XML）标准之间曾进行过一项获奖竞赛，最终后者被确定为官方文档标准。

OOXML “赢”了这场战斗，但在加入微软工具时使用 OOXML 是愚蠢的。在我看来，一个长达 5,000 页的“获胜”标准并算不上什么真正的标准。ODF 以及微软的这个最新版本在本文撰写时所符合的标准，与其说是他们工具和操作系统的成就，倒不如说是软件臃肿的另一种方式。

为了避免在节节剩余内容中过度重复“OpenOffice Writer”这个词组，我将 OpenOffice Writer 称为 Simply Writer（它对朋友的称呼），或者偶尔称为 `oowriter`（你用于从命令行界面执行 OpenOffice Writer 的应用程序名称）。

> 提示：在此时，OpenOffice 套件的 3.0 版本可用，但尚未集成到 Ubuntu 或 Kubuntu 中。OpenOffice.org 增加了许多新功能，其中最重要的可能可能是它对最新的微软“标准”和其他文件格式的支持。我确定它们会被集成的，但如果在你需要它们时它们还没有被集成，你可以自行安装。要安装此内容，请使用 `sudo` 命令和你喜喜欢的编辑器在 `/etc/apt/sources.list` 文件的最后一行添加以下内容：

```
deb http://ppa.launchpad.net/openoffice-pkgs/ubuntu \
Intrepid main
```

（你应该在一行内输入此内容，不要反斜杠）。保存文件并退出编辑器后，在你正在使用的任何包管理软件中更新可用软件包和源列表。你将可以在下一次更新时安装 OpenOffice 3.0 软件包。

## OpenOffice 文档的文件扩展名

随着 OpenDocument 格式的采用，OpenOffice.org Writer 更改了它的默认文件扩展名。以下列表了不同 OpenOffice.org 版本使用的文件扩展名：

- `odm`: OpenDocument 主文档
- `odt`: OpenDocument，OpenOffice.org 2.0 及更高
- `ott`: OpenDocument 模板，OpenOffice.org 2.0 及更高
- `sxw`: OpenOffice.org 2.0 之前的 Writer 文档
- `stw`: OpenOffice.org 2.0 之前的 Writer 模板
- `sxg`: OpenOffice.org 2.0 之前的 Writer 主文档

你最常见的文档是 ODT 和 OTT 文件扩展名。然而，在与长期使用 OpenOffice 用户交换文档时，你可能会遇到旧的 SXW 格式。SXW 文件非常，，它们实际上是包含 XML 文档文件和相关元数据的压缩包。你必须像本章“从其他文字处理器导入”章节中所解释的那样，使用 OpenDocument 转换向将旧格式的 SXW OpenOffice.org 文件导入新的 OpenDocument 格式中。

## 安装 Writer 的文件

如果你从 Live CD 安装 Ubuntu 或 Kub、从使用文本模式安装程序的 Alternate CD 安装、或从使用 OEM 模式安装程序的 Alternate CD 安装，则 Writer 是默认安装的。如果你想在具有图形界面的服务器系统上添加 Writer 或整个 OpenOffice.org，你可以按照第 23 章“添加、删除和更新软件”中的说明，使用 `apt-get`、`aptitude` 或 `Synaptic`（Ubuntu 系统上的 `Adept Manager`）进行安装。
