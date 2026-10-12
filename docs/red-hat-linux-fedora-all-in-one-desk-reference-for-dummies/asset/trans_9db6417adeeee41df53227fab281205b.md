
KDE 计算器比 GNOME 计算器功能更强大。例如，它可以以十六进制、十进制、八进制和二进制格式进行计算。从 KDE 桌面，你可以通过选择“主菜单→附件→科学计算器”启动 KDE 计算器。图 5-2 显示了 KDE 计算器。

Figure 5-2:
谁要算平方根？
在 KDE 计算器上算吧。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_208_0.png)

## 适用于 Linux 的商业办公应用程序

由于办公应用程序对许多企业和个人都很重要，我想简要介绍一些适用于 Red Hat Linux 的商业办公应用程序。这些商业产品包括 Anyware Office（前称 Applixware Office）和 StarOffice。这些产品确实需要付费，但费用通常低于 Microsoft Office——Windows 领先的办公套件。（如果您不知道，Microsoft Office 是一组应用程序的集合：用于文字处理的 Microsoft Word、用于电子表格的 Microsoft Excel、用于演示图形的 Microsoft PowerPoint 以及用于数据库的 Microsoft Access。）

另一款近期面向 Linux 的商业产品是 CodeWeavers 的 CrossOver Office。使用 CrossOver Office，您可以在 Linux 和 X Window 系统下运行现有的 Microsoft Office 应用程序，如 Word、Excel 和 PowerPoint。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_208_1.png)

本书的附带 DVD 未包含这些适用于 Red Hat Linux 的商业办公应用程序，但我在接下来的几节中简要介绍了它们。您可以在各厂商的网站上了解更多产品信息。

### Anyware Office

Anyware Office，前身为 Applixware Office，是适用于所有 Linux 发行版（包括 Red Hat Linux）的另一款知名办公套件。

2000 年 4 月，Applix, Inc. 成立了一个专门专注于 Linux 应用程序的独立部门——VistaSource, Inc.。

与其他办公套件类似，Anyware Office 包括 Words（文字处理）、Spreadsheets（电子表格）以及 Graphics and Presentations（演示图形）。此外，它还提供 Mail（电子邮件界面）和 Data（交互式关系数据库浏览工具）。Anyware Office 还可以读取和写入 Microsoft Office 和 Corel WordPerfect 格式的文档，以及多种其他文件格式。虽然不提供试用版，但整个 Anyware Office 套件在美国的售价目前低于 100 美元。

您可以在 VistaSource 网站（www.vistasource.com/products）了解更多关于 Applixware 的信息。

### StarOffice

StarOffice 是另一款商业办公套件；它由德国汉堡的 StarDivision 创建，并最近被 Sun Microsystems 收购。StarOffice 是一款跨平台解决方案——它可在 Linux、Windows 95/98/Me/NT/2000/XP、Sun Solaris SPARC 和 Sun Solaris x86 上运行。此外，StarOffice 提供多种语言版本：英语、法语、德语、西班牙语、意大利语和瑞典语。

StarOffice 的独特之处在于它将所有组件集成到一个通用桌面中，您可以从中打开新文档、将文档从一个应用程序拖放到另一个应用程序，并访问互联网。StarOffice 6.0 包含以下内容：

- 用于文字处理的 StarOffice Writer（兼容 Microsoft Word）
- 用于电子表格的 StarOffice Calc（兼容 Microsoft Excel）
- 用于演示的 StarOffice Impress（兼容 Microsoft PowerPoint）
- 用于矢量图形绘制的 StarOffice Draw
- 用于数据管理的 StarOffice Base

您可以从 www.sun.com/staroffice 购买 StarOffice。您也可以在同一网址找到 Sun 的 StarOffice 许可政策详情。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_209_0.png)

2000 年 10 月，Sun 在开源许可下发布了 StarOffice 的源代码。Sun 支持的开源项目 OpenOffice.org 于 2002 年 5 月发布了 OpenOffice.org 1.0 办公生产力套件。Red Hat Linux 附带 OpenOffice.org 1.0.2。要了解更多关于 OpenOffice.org 的信息，请参阅第三册，同时访问 www.openoffice.org。

### CrossOver Office

很可能您的 PC 上已安装 Windows 和 Microsoft Office。当您决定在 PC 上运行 Red Hat Linux 时，您仍可从 GNOME 或 KDE 桌面继续运行大多数 Microsoft Office 应用程序。在 Linux 中运行 Microsoft Office 的便利性来自一款名为 CrossOver Office 的商业产品。

来自 CodeWeavers 的 CrossOver Office 是一个软件包，可让您在 Linux 中安装 Microsoft Office 应用程序（仅限 Office 97 或 Office 2000，不支持 Office XP）。使用 CrossOver Office 运行 Office 应用程序无需 Microsoft Windows。您只需安装 CrossOver Office，然后从 CD-ROM 安装 Microsoft Office 即可。安装 Microsoft Office 后，Office 应用程序将直接从 GNOME 或 KDE 桌面可用。

CrossOver Office 使用 Wine——一个使用 X Window System 实现的 Windows Win32 和 Win16 应用程序编程接口（API）的开源实现，设计用于在 UNIX 和 Linux 系统中运行。Wine 包括 Wine loader 和 WineLib。Wine loader 可以加载和运行 Windows 应用程序。WineLib 用于在 Linux 中编译和链接 Windows 应用程序。Wine 可免费从 www.winehq.com 获取。

CodeWeavers 使用 Wine 的定制版本创建了 CrossOver Office，以确保 Microsoft Office 应用程序，尤其是来自 Office 97 或 Office 2000 的 Microsoft Word、Excel 和 PowerPoint 在 Wine 上正常运行。CodeWeavers 对 CrossOver Office 收取少量费用——单份的标价为 54.95 美元（多份购买费用更低）——但对 Wine 的所有更改都会返还给 Wine 项目。因此，Wine 开源项目从 CrossOver Office 的销售中受益。

您可以在 CodeWeavers 网站（www.codeweavers.com/products/office/）了解更多关于 CrossOver Office 的信息并购买它。

## aspell spelling checker

aspell 工具是一个交互式拼写检查器。您可以使用它检查文本文件中单词的拼写。为此，只需在终端窗口中输入以下命令：

```
aspell check filename
```

如果您想试用 aspell，请键入一些笔记并将其保存到名为 notes.txt 的文本文件中（文件名可以是任意的，但我在讨论中使用此文件名）。要对该文件运行拼写检查器，请在终端窗口中输入以下命令：

```
aspell check notes.txt
```

这条笔记描述了 8 月 16 日会议上达成的 *concensus*。
1) consensus      6) consensual
2) con census      7) consciences
3) con-census      8) incenses
4) condenses       9) consensus's
5) concerns        0) consensuses
i) Ignore          I) Ignore all
r) Replace         R) Replace all
a) Add             x) Exit
?

从第二行开始的所有内容都是 aspell 显示的内容。当 aspell 找到一个拼写错误的单词（不在其词典中的任何单词）时，它会显示包含该拼写错误单词（concensus）的句子，并通过用一对星号将其括起来来突出显示该单词。在该句子下方，aspell 列出可能的更正，并从 1 开始依次编号。在这种情况下，aspell 将 consensus——正确的选择——列为 concensus 的第一个更正。

在选项列表末尾，aspell 显示另外 16 个选项的列表——十个编号为 0 到 9，六个标记为单个字母 i、r、a、I、R 和 x——后面跟着一个问号提示。您必须按输出中显示的列表中的一个数字或字母，以指示您希望 aspell 执行的操作。编号选项显示拼写错误单词的十个可能的替换词。以下是字母选项的含义：

- 空格表示本次接受该词。
- i 表示忽略拼写错误的单词。
- I 表示忽略该单词的所有出现。
- r 表示替换此出现（您必须键入替换词）。
- R 表示替换所有出现（您必须键入替换词）。
- a 表示接受该词并将其添加到您的私人词典。
- x 表示保存文件的其余部分并退出，忽略拼写错误。

这些选项区分大小写。请确保未启用大写锁定。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_211_0.png)

## Databases

Red Hat Linux 附带两个关系数据库——PostgreSQL 和 MySQL。我将简要向您展示如何使用 MySQL。
