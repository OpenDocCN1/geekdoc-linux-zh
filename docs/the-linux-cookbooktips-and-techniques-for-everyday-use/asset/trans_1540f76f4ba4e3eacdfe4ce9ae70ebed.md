

## 《Linux 实用手册：日常使用的技巧与方法》：

下表列出了在“帮助”菜单中显示的手册名称，并描述了每本手册的内容：

| MANUAL | DESCRIPTION |
|---|---|
| Introduction | 介绍如何使用 LyX 手册，描述其内容以及如何查看和打印它们。 |
| Tutorial | 关于使用 LyX 编写文档的实践教程。 |
| User's Guide | LyX 主要使用手册，描述了所有常用命令、选项和功能。 |
| Extended Features | 这是《用户指南》的“第二部分”，描述了高级功能，例如参考文献、索引、多文件文档，以及在特殊情况下使用的技术，例如传真支持、SGML-Tools 支持，以及使用版本控制管理 LyX 文档。 |
| Customization | 显示 LyX 的哪些元素可以自定义以及如何进行自定义。 |
| Reference Manual | 描述所有菜单条目和内部函数。 |
| Known Bugs | LyX 正在积极开发中，像任何大型应用程序一样，已发现了一些错误。它们在此文档中列出并进行了描述。 |
| LaTeX Configuration | 该文档由 LyX 在安装到系统时自动生成。它是您 LaTeX 配置的清单，包括所使用的 LaTeX 版本、可用字体、可用文档类，以及可能安装在系统上的其他相关软件包。 |

最后，LyX 在 `/usr/X11R6/share/lyx/examples` 目录中包含示例文档。以下是这些文件的部分列表，并附带描述其内容：

| DOCUMENT FILE | DESCRIPTION |
|---|---|
| Foils.lyx | 描述如何使用 FoilTeX 包制作幻灯片——幻灯片或投影胶片。 |
| ItemizeBullets.lyx | 项目列表各种项目符号样式的示例。 |
| Literate.lyx | 使用 LyX 作为“ literate programming” 编排环境的示例。 |
| MathLabeling.lyx | 方程编号和标记的技术。 |
| Math_macros.lyx | 展示如何在数学模式中创建宏。 |
| Minipage.lyx | 展示如何编写双语双栏文档。 |
| TableExamples.lyx | LyX 中使用表格的示例。 |
| aa_head.lyx | 讨论并展示 LyX 在天文学领域的使用的文件。 |
| aa_paper.lyx |  |
| aas_sample.lyx |  |
| amsart-test.lyx | 使用美国数学学会格式编写的文档示例。 |
| amsbook-test.lyx |  |
| docbook_example.lyx | DocBook 文档示例。 |
| multicol.lyx | 多栏格式示例。 |
| scriptone.lyx | 好莱坞剧本示例。 |

## 16.4 使用 TeX 和朋友排版

```
@sf(Debian): `tetex-base`
@sf(Debian): `tetex-bin`
@sf(Debian): `tetex-doc`
@sf(Debian): `tetex-extra`
@sf(Debian): `tetex-lib`
@sf(WWW): http://www.tug.org/teTeX/
```

在 Linux 系统上使用最强大的排版工具是 TeX 排版系统及其相关软件。它是首屈一指的计算机排版系统——其输出优于或不逊于迄今为止的所有其他系统。它能够执行的先进的行和段落断行、连字符、字距调整和其他字体特征策略和算法，以及它能够执行的精度水平，至今尚未在文字处理器中得到匹配。

TeX 系统本身——不是文字处理器或单一程序，而是一大集合的文件和数据——以发行版的形式打包；teTeX 是为 Linux 设计的 TeX 发行版。

TeX 输入文档是用 TeX 格式语言编写的纯文本文件，TeX 工具可以处理这些文件并将其写入用于打印或查看的输出文件。这种方法对作者有很大的好处：纯文本输入文件可以用许多不同的计算机系统编写和交换，无论操作系统或编辑软件如何，并且这些输入文件不会因 TeX 软件的新版本而过时或无法使用。

Donald Knuth，世界上算法方面的权威，于 1984 年编写了 TeX，用来排版他的书籍，因为他对当时系统的质量不满意。自首次发布以来，对 TeX 格式语言进行了许多扩展——最著名的是 Leslie Lamport 的 LaTeX，它是用 TeX 格式语言编写的一组复杂的宏，旨在促进结构化文档的排版。LaTeX 可能比纯 TeX 格式的日常使用更多，但在我的经验中，这两种系统对于不同类型的文档都是有用的。

TeX 及相关程序的集合家族有时被称为“TeX 和朋友”，在某些 TeX 参考资料中缩写为 `texmf`；例如，随裸 TeX 系统提供的补充文件保存在 `/usr/lib/texmf` 目录树中。

以下配方描述了如何开始为 TeX 编写输入以及如何处理这些文件以供查看和打印。虽然不是每个人都想或需要用 TeX 和 LaTeX 编写文档，但这些格式被广泛使用——尤其是在 Linux 系统上——因此每个 Linux 用户都有可能遇到其中一个文件，并且应该知道如何处理它们。

注意：“TeX”听起来不像牛仔的名字，也不像“LaTeX”像一种油漆：字母 `T`、`E` 和 `X` 代表希腊字符 tau、epsilon 和 chi（来自希腊语 `techne`，意为艺术和科学）。因此，“TeX”中的最后一个音与 `Bach` 中的 `ch` 相同，而“LaTeX”根据当地方言，发音为 `lay-teck` 或 `lah-teck`。Knuth 将那些精通使用该系统的人称为“TeXnicians”。

