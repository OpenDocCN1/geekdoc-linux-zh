
StarOffice 被收购后，Sun Microsystems 在 GNU 公共许可证下发布了 StarOffice 代码的大部分，并开始开发后来成为 OpenOffice.org 的项目，后者可在 GPL 下免费获得。Sun 继续开发 StarOffice 并以 StarOffice 6.0 的形式发布了商业版本。免费版和商业版软件之间的显著区别在于，StarOffice 提供了更多字体，甚至更多导入/导出文件过滤器，而 OpenOffice.org 则没有（这些过滤器由于许可限制而无法在 GPL 版本中提供），并且 StarOffice 提供了自己的关系数据库，即 Software AG 的 Adabas D 数据库。OpenOffice.org 2.3 的 StarOffice 对应版本是 StarOffice 8。

## 配置 OpenOffice.org

OpenOffice.org 的安装是在系统范围内进行的，这意味着所有用户都可以访问它。然而，个人用户必须进入 OpenOffice.org 为其个人需求进行配置。这种初始配置在您首次加载任何 OpenOffice.org 组件时透明地进行，因此应用程序加载可能需要稍长时间。请耐心等待，您想要的应用程序就会出现。

> TIP
>
> OpenOffice.org 不断改进其生产力应用程序。您可以查看 OpenOffice.org 网站（http://www.openoffice.org/）获取最新版本。该网站提供下载源代码或最新工作安装文件的预编译版本的链接。更新的版本可能提供您需要的文档格式支持。如果您需要 Windows 兼容版本，您也可以在该网站上找到它。

如图 6.1 所示，Office 菜单位于 Applications 下。您可以看到 Database（Base）、Presentation（Impress）、Spreadsheet（Calc）和 Word Processor（Writer）的条目。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_154_0.png)

FIGURE 6.1 The OpenOffice.org suite provided by Ubuntu is simple to configure and use.

如图 6.1 所示，由 Ubuntu 提供的 OpenOffice.org 套件配置和使用都很简单。

与许多 Linux 应用程序一样，您可能会因 OpenOffice.org 中可用的配置选项数量之多而感到有些不知所措。值得庆幸的是，这些选项经过了大量思考进行了组织，您可以通过单击 Tools 菜单并选择 Options 来访问这些选项。无论您使用哪个程序调出此对话框，它的外观都相同；从 Writer、Impress 或 Calc 调出时都一样。它充当所有 OpenOffice.org 应用程序的中央配置管理工具。您可以使用它为所有 OpenOffice.org 应用程序设置全局选项，或为每个单独组件设置特定选项。例如，在图 6.2 中，您可以更改用户详细信息和信息，并且这会在所有 OpenOffice.org 应用程序中得到体现。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_155_0.png)

**图 6.2** 您可以在此对话框中为所有 OpenOffice.org 应用程序设置用户详细信息。

> **提示**
>
> 有两个网站提供有关 OpenOffice.org 功能的附加信息：
>
> http://lingucomponent.openoffice.org/download_dictionary.html——此网站提供拼写和断字词典的安装说明和文件，这些词典未包含在 OpenOffice.org 中。
>
> http://sourceforge.net/projects/ooextras/——此网站提供模板、宏和剪贴画，这些内容未随 OpenOffice.org 一起提供。

OpenOffice.org 是一个持续开发中的项目，但当前版本与 Sun 版本的 StarOffice 8 处于同一水平。您可以浏览 OpenOffice.org 网站获取文档、常见问题解答，并提供反馈。

## 使用 OpenOffice.org Writer

在组成 OpenOffice.org 的所有应用程序中，您最可能经常使用的是 Writer——OpenOffice.org 的文字处理器。Writer 的视觉风格与 Microsoft 的 Word 非常相似，并且相对于其商业且价格高得多的竞争对手，Writer 拥有多项优势。在本节中，您将学习如何开始使用 Writer，并利用其一些强大的格式和布局工具。

> **注意**
>
> 您可能会有兴趣知道，Writer 是撰写和编辑本书时选择的主要文字处理器。

### 开始使用 Writer

您可以通过面板上的快捷方式或转到“应用程序”“办公”菜单并选择“文字处理”来访问 Writer。几秒钟后，Writer 会打开一个空白文档，光标闪烁等待您的命令。直接开始输入文档可能很诱人，但在开始工作之前进行一些初始配置是值得的。

首先，确保选项已按照您的需求设置。单击“工具”菜单并选择“选项”以打开“选项”对话框，如图 6.2 所示。初始屏幕允许您使用姓名、地址和联系信息个性化 OpenOffice.org，但还有一些功能配置选项，您可能也想更改。首先，通过单击“路径”选项检查默认路径是否正确。您可能希望将“我的文档”路径更改为比仅使用主目录更具体的位置，如图 6.3 所示。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_156_0.png)

图 6.3 单击“编辑”按钮选择默认文档目录。

您可能还想更改 OpenOffice.org 的设置，使其默认以 Microsoft Word 格式保存，如果需要的话。这可以在图 6.4 所示的“加载/保存”“常规”选项下完成。如果您重视自己的工作，建议更改自动恢复设置，使其每隔几分钟保存一次。

图 6.4 中还显示了一组特定于 Writer 的选项。从上到下依次为：

- 常规——指定影响 Writer 常规使用的选项。
- 视图——指定您希望 Writer 显示的内容。
- 格式辅助——指定是否要显示非打印字符。
- 网格——创建可用于对齐框架和图像的网格。
- 基本字体——在此处为文档选择默认字体。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_157_0.png)

图 6.4 确保您使用的是最适合自己的文件格式。

- 打印——精确指定打印文档时希望 Writer 输出的内容。
- 表格——设置在 Writer 中绘制表格的选项。
- 更改——定义 Writer 如何处理对文档的更改。
- 兼容性——Writer 使用的一组规则，以确保与早期版本的 Writer 保持高度兼容。
- 自动标题——为图像、图表和其他对象创建自动标题。

花一点时间检查这些选项，可以为您提供一个高度个性化且极其高效的工作环境。

### 使用样式和格式

使用 Writer 的重要优势之一是，您可以轻松地将格式和样式应用于非常复杂的文档。根据您处理的文档类型，您可能需要考虑在默认包含的 20 种样式之外创建自己的样式。您可以通过工具栏中的“样式”下拉框或图 6.5 所示的“样式和格式”窗口访问样式。如果看不到该窗口，请按 F11 键显示它。

使用“样式和格式”工具最简单的方法是突出显示要设置样式的文本，然后双击窗口中的所需样式。可供选择的样式有很多，但如果您有更专业的需求，可能会觉得它们有所限制。要开始定义自己的样式，请按 Ctrl+F11 打开“样式目录”，如图 6.6 所示，您可以在其中添加、修改和删除页面、段落、列表、字符和框架的样式。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_158_0.png)

图 6.5 Writer 的快速易用的样式和格式工具。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_158_1.png)

图 6.6 Writer 强大的样式目录让你能够控制样式的方方面面。

## 使用 OpenOffice.org Calc

OpenOffice.org 的电子表格组件名为 Calc，是一款功能非常强大的 Excel 替代品。

Calc 用于存储你需要以某种方式分析的数值信息。因此，例如，你可以用它来帮助你按月制定预算。它可以为你处理计算，只要你告诉 Calc 你想要它做什么。任何有 Excel 使用经验的人都会觉得 Calc 非常熟悉。

在本节中，我们将向你展示如何开始使用 Calc，包括输入公式和格式设置。我们还将查看 Calc 的一些更高级的功能，包括数据透视功能，它允许你轻松汇总信息。

### 开始使用 Calc

你可以点击位于顶部 GNOME 面板上的快捷图标，或者在应用程序主菜单下的 Office 菜单中选择电子表格。无论你选择哪种方式，结果都一样，Calc 开始加载。
