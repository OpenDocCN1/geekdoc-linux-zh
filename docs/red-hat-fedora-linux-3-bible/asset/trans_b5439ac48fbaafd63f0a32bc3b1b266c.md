

每个单元格的标题都应居中对齐 (c | c | c)，且随后出现的数据单元格应对左对齐 (l | l | l)。

> **警告：**表格定义行的末尾必须有一个句号。在本例中，句号位于 l | l | l. 行之后。如果缺少该句号，tbl 将尝试将该文本解释为表格定义的一部分。在这种情况下，tbl 会失败并停止处理文件，因此表格不会打印。

表格中的其余信息是数据。请注意，制表符分隔符是冒号字符 (:)。当表格完成后，使用 .TE 宏结束它。如果该表格位于名为 memotbl.mm 的备忘录中，tbl 可以预处理该备忘录，然后使用以下命令将其发送到打印机：

```
$ groff -Tps -mm -t memotbl.mm
```

位于 .TS 和 .TE 宏之间的数据被解释为表格。图 6-8 显示了此示例。

| 员工 | 职位 | 地点 |
|---|---|---|
| Jones, James<br>Smith, Charles<br>Taylor, Sarah<br>Walters, Mark<br>Zur, Mike | Marketing Manager<br>Sales Manager<br>R&D Manager<br>Information Systems Manager<br>Distribution Manager | Jones, James<br>Smith, Charles<br>Taylor, Sarah<br>Walters, Mark<br>Zur, Mike |

**图 6-8：** 使用 tbl 命令的 .TS 和 .TE 宏设置文本的对齐方式并将其放入列中。

PIC 宏（.PS 和 .PE）允许你在 Groff 中创建用于使用的简单图表和流程图。PIC 仅适用于创建简单的方框、圆形、椭圆、线、圆弧、样条曲线以及一些文本。以下是一段可以出现在 Groff 文档中的 PIC 代码：

```
::PS
box invis "Start" "Here"; arrow
box "Step 1"; arrow
circle "Step 2"; arrow
ellipse "Step 3"; arrow
box "Step 4"; arrow
box invis "End"
::PE
```

在 .PS 之后，第一行表示一个包含文字 Start Here 的不可见方框（invis），后跟一个箭头。该箭头连接到包含文字 Step 1 的下一个方框。下一个元素（由箭头连接）是一个圆形（Step 2）、一个椭圆（Step 3）、另一个方框（Step 4）以及另一个不可见方框（End）。.PE 表示 pic 绘图结束。

如果这些行出现在名为 memopic.mm 的文档中，你可以预处理 PIC 代码并使用以下命令打印该文件：

```
$ groff -Tps -mm -p memopic.mm
```

图 6-9 显示了此绘图的一个示例。

![](img/b22364e57409c2481ba806e4e6b9309c_259_0.png)

**图 6-9：** 使用 pic 命令的 .PS 和 .PE 宏创建简单的流程图。

## 使用 TeX/LaTeX 进行文本处理

TeX（发音为 *tech*）是一组主要用于生成科学和数学类型排版文档的命令。使用 TeX 最常见的方法是调用宏包。TeX 最流行的宏包是 LaTeX，它采用更高层的方法来格式化 TeX 文档。TeX 和 LaTeX 工具包含在 `tex-tex-latex` 包中。

> **注意：** 使用本章中显示的 TeX 示例所需的 `tex*` 包可以在随本书附带的 DVD 中找到。

TeX 从 latex 格式文件（`latex.fmt`）解释 LaTeX 宏。默认情况下，`latex.fmt` 和 `plain.fmt` 格式文件是安装 TeX 包时自动构建的唯一文件。你可以与 TeX 一起使用的其他宏文件包括：

- **amstex** --- 数学出版物，包括美国数学学会，将其作为官方排版系统使用。
- **explain** --- 包含用于索引和目录的宏。
- **texinfo** --- 由自由软件基金会用于生成软件手册的宏。来自这些宏的文本输出可与 `Linuxinfo` 命令一起使用。

你可以使用任何文本编辑器创建 TeX/LaTeX 文件。在创建文本和宏之后，你可以运行 `tex` 命令（或几种其他相关实用程序之一）来格式化文件。输入文件的格式为 `filename.tex`。输出通常由三个不同的文件组成：

- **filename.dvi** --- 这是与设备无关的输出文件，可以翻译用于几种不同类型的输出设备（例如 PostScript）。
- **filename.log** --- 这是一个包含诊断消息的日志文件。
- **filename.aux** --- 这是一个由 LaTeX 使用的辅助文件。

生成的 `.dvi` 文件可以针对特定设备进行格式化。例如，你可以使用 `dvips` 命令将结果 `.dvi` 文件输出到你的 PostScript 打印机（`dvips filename.dvi`）。或者你可以使用 `xdv` 命令在 X 中预览 `dvi` 文件。

## 创建和格式化 LaTeX 文档

由于 LaTeX 是使用 TeX 的最常见方式，本节描述如何创建和格式化 TeX 文档。LaTeX 宏（通常称为 *命令*）以以下两种形式之一出现在文档中：

- `\command[optional][required]` — 首先是一个反斜杠 (\)，后面跟着一串字符。（用命令名称替换 `\command`。）可选参数包含在大括号 ({ }) 中，必填参数包含在方括号 ([ ]) 中。
- `\!command[optional]!required \command` — 首先是一个反斜杠 (\)，后面跟着一个非字母的单字符。（用命令字符替换 `!`。）可选参数包含在大括号 ({ }) 中，必填参数包含在方括号 ([ ]) 中。

每个命令定义了一些要采取的操作。该操作可以控制页面布局、使用的字体、间距、段落布局或对文档的各种其他操作。LaTeX 文档可以包含的最少格式化内容如下：

```
\documentclass{name}
\begin{document}
    TEXT GOES HERE!
\end{document}
```

你应该用你要创建的文档类的名称替换 `{name}`。有效的文档类包括 *article*、*book*、*letter*、*report* 和 *slides*。文件的文本以及你的格式化命令位于 `\begin{document}` 和 `\end{document}` 命令之间。

开始使用 LaTeX 的最佳方法是使用 LyX 编辑器。LyX 提供了用于创建 LaTeX 文档的 GUI。它还包含各种模板，你可以使用它们而不是从头开始创建文档。图 6–10 显示了 LyX 编辑器的一个示例。

> **注意：** Fedora 不附带 LyX 编辑器。在 ftp://ftp.lyx.org/pub/lyx/bin 的 LyX 网站上查找 LyX 的 RPM 包。查找 Fedora 或 Red Hat RPM。

如果你想在普通文本编辑器中编辑 LaTeX，你需要熟悉 LaTeX 命令。要查看 LaTeX 命令的完整列表，请输入 `info latex`，然后转到“LaTeX 文档内的命令”部分。

![](img/b22364e57409c2481ba806e4e6b9309c_261_0.png)

**图 6-10：** 使用 LyX 编辑器以图形方式创建 LaTeX 文档。

## 使用 LyX LaTeX 编辑器

使用 LyX 命令启动 LyX LaTeX 编辑器。LyX 附带大量支持文档。点击帮助以选择教程、用户指南或其他信息。

为了开始你的第一个文档，我建议你选择 LyX 提供的模板之一。模板位于 `/usr/share/lyx/templates`。要打开模板，请单击文件 → 从模板新建。将出现可用模板列表。例如，你可以使用它们创建信件、幻灯片和文章。

除了提供标准的编辑功能（如剪切、复制和粘贴）之外，你还可以从“布局”菜单执行各种标记功能。至于数学功能，“数学”菜单允许你将分数、平方根、指数、求和和积分功能插入到你的文档中。完成后，你可以：

- 将文件打印到 PostScript 打印机或输出 PostScript (.ps) 文件。（点击文件 → 打印，选择打印方法，然后点击确定。）
- 将文件导出为 LaTeX、DVI、PostScript 或 ASCII 文本。（点击文件 → 导出，并从文件格式列表中选择。）

LyX 称自己为 WYSIWYM 编辑器—— What You Say Is What You Mean（所言即所意）。因此，你在编辑时屏幕上看到的内容与打印文档的外观并不完全一致。例如，按多次 Enter 键不会在行之间产生额外的空白。

