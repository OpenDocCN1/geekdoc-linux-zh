
Employee:Title:Location```
Jones, James:Marketing Manager:New York Office
Smith, Charles:Sales Manager:Los Angeles Office
Taylor, Sarah:R&D Manager:New York Office
Walters, Mark:Information Systems Manager:Salt City Office
Zur, Mike:Distribution Manager:Portland Office
.TE
```

在 `.TS` 宏开始表格后，下一行表示表格应在页面上居中（`center`），并用线框包围，冒号将用于将数据分隔到单元格中 `[tab(:)]`。接下来的行显示标题应该在框内居中（`c`），并跨越接下来两个单元格（`s`）。随后的行表示每个单元格的标题应该居中（`c | c | c`），随后的数据单元格应该左对齐（`l | l | l`）。

**注意：** 表格行定义末尾必须有一个句号。在这种情况下是 `1|1..`。如果没有句号，`tbl` 将文本解释为表格定义的一部分。在这种情况下，`tbl` 将失败并停止处理表格，因此表格将无法打印。

表格中的其余信息是数据。注意制表符分隔符是冒号字符（`:`）。当表格完成后，使用 `.TE` 宏结束它。如果表格在一个名为 `memtbl` 的备忘录中，`tbl` 可以预处理该备忘录并使用以下命令将其发送到打印机：

```
$ groff -Tps -mm -t memtbl.mm
```

`.TS` 和 `.TE` 宏之间的数据被解释为表格（见图 6-8）。

| Employee | Title | Location |
| --- | --- | --- |
| Jones, James | Marketing Manager | New York Office |
| Smith, Charles | Sales Manager | Los Angeles Office |
| Taylor, Sarah | R&D Manager | New York Office |
| Walters, Mark | Information Systems Manager | Salt City Office |
| Zur, Mike | Distribution Manager | Portland Office |

**图 6-8：** 使用 `tbl` 命令的 `.TS` 和 `.TE` 宏设置文本对齐方式并分列。

`PIC` `.PS` 和 `.PE` 宏允许你在 Groff 中创建简单的图形和流程图。`PIC` 确实适用于创建简单的形状、圆形、椭圆、线条、弧、样线和一些文本。以下是用于 Groff 文档的 `PIC` 代码：

```
.PS
box invis "Start" "Here"; arrow
box "Step 1"; arrow
circle "Step 2"; arrow
elipse "Step 3"; arrow
box "Step 4"; arrow
box invis "End"
```

# 第 6 章：使用 Fedora 和 RHEL 发布 267

在 `.PS` 之后，第一行表示一个不可见的框（`invis`），其中包含“Start Here”（在此开始）字样，随后是一个箭头。箭头指向下一个包含“Step 1”（第一步）的框。后续元素（通过箭头连接）是一个圆（Step 2）、一个椭圆（Step 3）、另一个框（Step 4）以及另一个不可见的框（End）。`.PE` 表示绘图的结束。

如果这些行出现在名为 `mempic.mm` 的文档中，可以使用以下命令对 `PIC` 代码进行预处理并打印文件：

```
$ groff -Tps -1 -mm -p mempic.mm
```

图 6-9 显示了这种图的示例。

![](img/ec54a77854df1c8d0311d04a1e6b8d3c_308_0.png)

图 6-9：使用 `pic` 命令的 `.PS` 和 `.PE` 宏创建简单的流程图。

## 使用 TeX/LaTeX 进行文本处理

TeX（读音为 tech）是一系列命令，主要用于制作科学和数学排版文档。使用 TeX 的最方法是调用宏包。TeX 最流行的宏包是 LaTeX，它采用了一种更高层次的方法对 TeX 文档进行格式化。TeX 和 LaTeX 工具包含在 `texet-latex` 包中。

> 注意：使用本章所示 TeX 示例所需的 `texex-*` 软件包可以在随书的 DVD 上找到。

TeX 解释来自 `latex` 文件 (`latex.fmt`) 的 LaTeX 宏。默认情况下，只有 `latex.fmt` 和普通格式文件（plain format files）在安装 TeX 软件包时会自动构建。你可以与 TeX 一起使用的其他宏文件还包括：

-- `amstext` — 数学出版物，包括美国数学学会（AMS），该学会将其作为其官方排版系统。

- `eplain` — 包含用于索引和目录的宏。

- `texinfo` — 自由软件基金用于制作软件手册的宏。这些宏的文本输出可以配合 Linux `info` 命令使用。

你可以使用任何文本编辑器创建 TeX/LaTeX 文件。创建文本和宏后，你可以运行 `tex` 命令（或几个其他相关实用程序之一）来格式化文件。输入文件为 `filename.tex` 格式。输出通常是三个不同的文件：

268 第二部分：使用 Fedora 和 RHEL

- `filename.dvi` — 这是一个设备无关的输出文件，可以由不同类型的输出设备（如 PostScript）进行转换。

- `filename.log` — 这是一个包含诊断信息的日志文件。

- `filename.aux` — 这是 LaTeX 使用的辅助文件。

生成的 `.dvi` 可以针对特定设备进行格式化。例如，你可以使用 `dvips` 命令将结果 `.dvi` 文件输出到你的 PostScript 打印机（`dvips filename.dvi`）。或者你可以使用 `xvdi` 命令在 X 环境中预览 `.dvi` 文件。

## 创建和格式化 LaTeX 文档

由于 LaTeX 是使用 TeX 的常用方法，本节描述了如何创建和格式化 LaTeX 文档。LaTeX 宏（通常称为命令）在文档中以以下两种形式之一出现：

- `\{option}[required]` — 首先是一个反斜杠 (`\`)，后面跟着一串字符。（将字符串替换为命令名称）。可选参数包含在大括号 (`{}`) 中，必要参数包含在括号 `[]` 中。

- `\?option}[required]` — 首先是一个反斜杠 (`\`)，后面跟着一个不是字母的单个字符。（替换为命令字符）。可选参数包含在大括号 (`{}`) 中，必要参数包含在括号 `[]` 中。

每个命令都定义了要执行的操作。该操作可以控制页面布局、使用的字体、间距、段落布局以及文档上的各种其他操作。LaTeX 文档可以包含的最少格式内容如下：

```
\document{name}
\begin{document}
TEXT GOES HERE!
\end{document}
```

你应当将 `{name}` 替换为你正在创建的文档名称。有效的文档类包括 `article`、`book`、`letter`、`report` 和 `slides`。文件的文本以及你的格式化命令位于 `\begin document` 和 `\end document` 命令之间。

从开始学习 LaTeX 的最佳方法是使用 LyX 编辑器。LyX 提供了一个用于创建 LaTeX 文档的图形用户界面（GUI）。它还包含了各种你可以使用的模板，而无需从头创建文档。图 6-10 显示了 LyX 编辑器的示例。

> 注意：LyX 编辑器可在 Fedora 仓库获取；你可以通过输入 `yum install` 来安装它。

如果你想在普通的文本编辑器中编辑 LaTeX，你需要熟悉 LaTeX 命令。要查看 LaTeX 命令的完整列表，输入 `info latex` 并进入“Commands within a LaTeX document”部分。

第 6 章：使用 Fedora 和 RHEL 发布 269

![](img/ec54a77854df1c8d0311d04a1e6b8d3c_310_0.png)

欢迎使用 LyX！

## 使用 LyX 时需要知道的 N 件事

1. LyX 附带出色的文档——请使用它！从 Help -> Introduction 开始，这将为你提供关于文档的非常简短的介绍。通过 Help -> Tutorial 学习使用 LyX。

2. LyX 是我们所说的“文档处理器”。从设计上讲，它与普通的文字处理器不同——这种方式让编写文档变得容易，但仅略有不同，所以不要害怕。文档会让一切变得清晰。**图 6-10：使用 LyX 图形化创建 LaTeX 文档。

## LyX 编辑器

LyX 附带出色的文档——请使用它！从 Help -> Introduction 开始，这将为你提供关于文档的非常简短的介绍。通过 Help -> Tutorial 学习使用 LyX。

2. LyX 是我们所说的“文档处理器”。从设计上讲，它与普通的文字处理器不同——这种方式让编写文档变得容易，但仅略有不同，所以不要害怕。文档会让一切变得清晰。
