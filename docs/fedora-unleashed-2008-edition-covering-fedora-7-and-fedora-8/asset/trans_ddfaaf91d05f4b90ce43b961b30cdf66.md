

## 第 126 章 第 6 章 生产力应用

我们将向你介绍 Writer 和 Calc，这两个是 OpenOffice.org 中最受欢迎的组件。我们还会简要看看其他一些可用的基于 Linux 的办公套件。

### 使用 OpenOffice.org

对于大多数生产力套件的用戶来说，OpenOffice.org 应该能满足你的大部分甚至全部需求。然而，你需要克服的第一个障碍并不是它是否能做到你所要求的功能，而是它是否成功地导入和导出专有 Microsoft 格式。主要来说，OpenOffice.org 应该能轻松导入和导出，尽管可能会在一些更晦涩的 Office 格式上卡住。鉴于大多数用户很少超出制表符、列和表格的范围，这种兼容性水平应该就足够了。

但是，强烈建议你收集一批可能受到导入/导出过滤器影响的文档，并对其进行彻底测试（当然，保留原始文件的备份）。对于部署了新的生产力套件的系統管理員来说，没有什么比突然收到用户抱怨他们无法读取自己的文件更糟糕的了。这会迅速破坏从 OpenOffice.org 中其他实用功能中获得的任何好处，甚至可能导致专有格式和昂贵的办公套件的回归。许多用户不介意切换到 OpenOffice.org， largely 因为其用户界面与类似的 Microsoft 应用程序非常相似。这有助于用户适应其环境，并消除他们对切换的担忧。这种相似性使过渡到 OpenOffice.org 变得更加容易。

当然，仅仅看起来像 Microsoft 应用程序并不是唯一的直接好处。OpenOffice.org 支持大量文件格式，能够导出近 70 种不同类型的文档。如此广泛 的文件格式意味着你应该几乎能够在任何环境中成功使用 OpenOffice.org。

### OpenOffice.org 中有什么？

OpenOffice.org 包含许多用于创建文本文档、准备电子表格、组织演示文稿、管理项目等生产力应用程序。以下是 OpenOffice.org 软件包中随 Fedora 提供的组件：

- **Writer** — 这款文字处理程序允许你编写、格式化和组织文本文档。如果你习惯于使用 Microsoft Word，OpenOffice.org Writer 的功能会让你感到熟悉。你将在本章稍后学习如何开始使用 Writer。Writer 位于“应用程序”、“办公”、“文字处理器”下。

- **Calc** — 这款电子表格程序允许你在电子表格格式中操作数字。除了最晦涩的 Microsoft Excel 功能外，Calc 都提供支持，这意味着与 Excel 用户交换电子表格应该是成功的。Calc 提供有限的 Excel 宏兼容性，但这些宏通常需要重写。我们将在本章稍后介绍如何设置带有公式的基本电子表格，并展示如何构建基本的数据模型。Calc 位于“应用程序”、“办公”、“电子表格”下。

- **Impress** — 这款演示程序类似于 Microsoft PowerPoint，允许你创建包含图表、图解和其他图形的幻灯片演示。Impress 也能很好地处理 PowerPoint 文件。Impress 位于“应用程序”、“办公”、“演示文稿”下。

- **Math** — 这款数学公式编辑器允许你使用多种数学字体和符号编写数学公式，以便包含在文字处理文档中。这些符号非常专业化，不容易包含在文字处理器的基本功能中。这主要对数学和科学写作者感兴趣，但 Math 对任何需要在文本中包含复杂公式的人都有用。你使用“添加/删除软件”下载 Math。

- **Base** — 这款数据库随 OpenOffice.org 2.3 套件引入，并随 Fedora 提供。它提供了一个功能齐全的数据库应用程序。你使用“添加/删除软件”下载 Base。

- **Draw** — 这款图形应用程序允许你创建图像，以便包含在使用 OpenOffice.org 生成的文档中。它仅以 OpenOffice.org 格式保存文件，但可以导入大多数常见的图像格式。你使用“添加/删除软件”下载 Draw。

- **Dia** — 这款来自 GNOME 办公套件的工程绘图编辑器允许你创建测量绘图，如建筑师和工程师使用的绘图。其功能类似于 Microsoft Visio。你使用“添加/删除软件”下载 Dia。

- **Planner** — 你可以使用这款项目管理应用程序进行项目规划、调度和跟踪；此应用程序类似于但与 Microsoft Project 不兼容。它在“办公”菜单中作为“项目管理”项出现。

### OpenOffice.org 简史

OpenOffice.org 办公套件基于一个名为 StarOffice 的商业套件。最初由一家德国公司开发，StarOffice 被美国的 Sun Microsystems 收购。对旧 StarOffice 的最大抱怨之一是，所有组件应用程序都集成在一个看起来非常像 Microsoft Windows 桌面的 StarOffice“桌面”下，包括开始按钮和菜单。这意味着要编辑一个简单的文档，必须加载不必要的 应用程序，使办公套件加载缓慢、运行缓慢，并且对系统资源要求很高。

收购 StarOffice 后，Sun Microsystems 在 GPL（GNU 公共许可证）下发布了 StarOffice 代码的大部分，并开始开发后来成为 OpenOffice.org 的项目，该版本在 GPL 下免费可用。Sun 继续开发 StarOffice，并发布了商业版本 StarOffice 6.0。软件免费版本和商业版本之间的显著区别在于，StarOffice 提供更多的字体，甚至比 OpenOffice.org 提供更多的导入/导出文件过滤器（由于许可证限制，GPL 版本无法提供这些过滤器），并且 StarOffice 提供其自己的关系数据库，即 Software AG 的 Adabas D 数据库。OpenOffice.org 2.3 的 StarOffice 对应版本是 StarOffice 8。

### 安装和配置 OpenOffice.org

Fedora 提供 OpenOffice.org 的 RPM 包。如果你没有在初始 Fedora 安装期间安装 RPM 包，你可以稍后使用“添加/删除软件”工具或从命令行使用 `yum install openoffice.org` 进行安装。

> OpenOffice.org 正在不断改善其生产力应用程序。你可以查看 OpenOffice.org 网站（http://www.openoffice.org/）以获取最新版本。该网站提供链接下载最新工作安装文件的源代码或预编译版本。较新的版本可能提供你所需的文件格式支持。如果你需要 Windows 兼容版本，你也会在该网站找到。

OpenOffice.org 的安装是在系统范围内进行的，这意味着所有用户都可以访问它。然而，用户必须进入 OpenOffice.org 以根据他们的个人需求进行配置。这种初始配置在你加载任何 OpenOffice.org 组件时透明地进行，因此应用程序可能需要更长的时间来加载。请耐心等待，你所需 的应用程序将会出现。

图 6.1 显示的是 OpenOffice.org Writer，一个空白文档已准备好供你创作你的杰作。OpenOffice.org 在所有相关应用程序中共享通用首选项，这意味着你只需要定义一次你的某些个人详细信息或保存文档的路径。

![](img/34e72348d53ca54c2a1d9c871316691b_157_0.png)

与许多 Linux 应用程序一样，你可能会被 OpenOffice.org 中提供的配置选项的巨大数量所压倒。值得庆幸的是，人们花了大量精力来组织这些选项，如果你点击“工具”菜单并选择“选项”即可访问它们。无论你使用哪个程序打开此对话框，它看起来都一样；无论从 Writer、Impress 还是 Calc 打开。它充当所有 OpenOffice.org 应用程序的中央配置管理工具。你可以使用它设置所有 OpenOffice.org 应用程序的全局选项，或为每个单独组件设置特定选项。例如，在图 6.2 中，你可以更改用户详细信息和信息，并反映到所有 OpenOffice.org 应用程序中。

![](img/34e72348d53ca54c2a1d9c871316691b_158_0.png)

**图 6.2** 你可以从该对话框中为所有 OpenOffice.org 应用程序设置用户详细信息。

### 提示

两个网站提供有关 OpenOffice.org 功能的额外信息。

- [https://lingucomponent.openoffice.org/download_dictionary.html](https://lingucomponent.openoffice.org/download_dictionary.html) — 该网站提供安装拼写和连字符词典的说明和文件，这些词典未随 OpenOffice.org 提供。
- [http://sourceforge.net/projects/ooxtras/](http://sourceforge.net/projects/ooxtras/) — 该网站提供模板、宏和剪贴画，这些未随 OpenOffice.org 提供。

OpenOffice.org 是一个持续进行中的项目，但当前发布版本与 Sun 版本的 StarOffice 8.0 持平。你可以浏览 OpenOffice.org 网站以获取文档和常见问题解答，并提供反馈。

### 使用 OpenOffice.org Writer

在构成 OpenOffice.org 的所有应用程序中，你最有可能经常使用的是 Writer，即 OpenOffice.org 的文字处理器。具有类似 Microsoft Word 的视觉风格，Writer 在一些方面优于其商业版和

