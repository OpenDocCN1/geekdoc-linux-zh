
手册页中还使用了其他几种宏。`.IP`宏为选项等项目格式化了缩进段落。手册页还包含一些低级字体请求；例如，`\fB`表示将当前字体更改为粗体，`\fi`将字体更改为斜体，`\fR`将其改回常规字体。（这种标记比请求特定的字体类型更好，因为它只是将当前字体更改为粗体、斜体或常规。）图 6-2 显示了 `waycool` 手册页经过 `groff` 格式化后的外观：

```bash
$ groff -man -Tps -l waycool.1
```

![](img/1744bde8c889adfab3fc911e1687fecf_244_0.png)

图 6-2：手册页格式化添加了页眉并布局了文本页面。

表 6-1 列出了您可以在手册页中使用的宏。这些宏在 `man(7)` 手册页中有描述（输入 `man 7 man` 查看该页）。

### 表 6-1：Man 宏

| 宏 | 描述 | 宏 | 描述 |
| :---- | :---- | :---- | :---- |
| `B` | 粗体 | `BI` | 粗体，然后斜体（交替） |
| `BR` | 粗体，然后罗马体（交替） | `.DT` | 设置默认制表位 |
| `.HP` | 开始悬挂缩进 | `I` | 斜体 |
| `IB` | 斜体，然后粗体（交替） | `.IP` | 开始悬挂标签。用于选项。长标签使用 `.TP` |
| `.IR` | 斜体，然后罗马体（交替） | `.LP` | 开始段落 |
| `.PD` | 设置段落间距 | `.PP` | 开始段落 |
| `.RB` | 罗马体，然后粗体（交替） | `.RE` | 结束相对缩进（在 `.RS` 之后） |
| `RI` | 罗马体，然后斜体（交替） | `.RS` | 开始相对缩进（使用 `.RE` 结束缩进） |
| `.SB` | 小字号文本，然后粗体（交替） | `.SM` | 小字号文本。用于显示全大写字母。 |
| `.SH` | 节标题 | `.SS` | `.SH` 标题内的子标题。 |
| `.TH` | 标题页头。在手册页开头使用一次。 | `.TP` | 开始悬挂标签。文本从下一行开始，不与标签在同一行。 |

### 使用 Groff 创建信函、备忘录或白皮书

备忘录宏（使用 Groff 的 `-mm` 选项）曾一度在 UNIX 用户中很流行，用于生成技术文档、信函和备忘录。虽然具有各种所见即所得（WYSIWYG）模板的现代文字处理软件使 `mm` 变得过时，但在紧急情况下，`mm` 仍然可以在文本环境中快速创建排版风格文档。

要使用 `mm` 宏格式化并打印（到 PostScript 打印机）文档，请使用以下命令：

```bash
$ groff -mm -Tps -l letter.mm
```

以下是如何使用 `mm` 宏生成信函的简单示例：

```text
.WA "Christopher T. Craft"
999 Anyway Way
Anytown, UT 84111 USA
.WE
.IA
John W. Doe
111 Notown Blvd.
Notown, UT 84111
.IE
.LO RN "Our telephone conversation"
.LO SA "Dear Mr. Doe:"
.LT

In reference to our telephone conversation on the 4th, I am calling to
confirm our upcoming appointment on the 18th. I look forward to
discussing the merger. I believe we have a win-win situation here.
.FC "Yours Truly,"
.SG
```

如果您使用代码示例前一段中提到的 `groff` 命令行，信函的输出如图 6-3 所示。

![](img/1744bde8c889adfab3fc911e1687fecf_246_0.png)

`mm` 宏常用于生成技术备忘录。以下是一个签名页的示例，可能放置在较大的技术备忘录前面。

```text
.TL
Merger Technical Specifications
.AF "ABC Corporation"
.AU "Christopher Craft"
.AT "President"
.AS
This memo details the specifications for the planned merger.
.AE
.MT "Merger Description and Marching Orders"
As a result of our talks with XYZ corporation, we plan to go forward with the merger. This document contains the following:
.BL
.LI
Schedule and time tables.
.LI
Financial statements.
.LI
Asset allocations.
.LE
.SP
Please add corrections and sign the approval line.
.FC
.SG
.AV "John W. Doe, XYZ Corporation President"
.AV "Sylvia Q. Public, XYZ Corporation CFO"
.NS
Everyone in the corporation.
.NE
```

图 6-4 显示了此备忘录的输出。

![](img/1744bde8c889adfab3fc911e1687fecf_247_0.png)

**图 6-4**：自动在备忘录中添加标题和审批行。

> **注意：** 关于 `mm` 宏的完整列表，请参阅 `groff_mm` 手册页。存在 100 多个 `mm` 宏。此外，还有数十个已定义的字符串，可用于设置和调用信息（例如图形名称、表格、目录信息以及文本），这些信息会自动以不同的标题打印出来。

## 添加方程、表格和图片

若要解释用于方程、表格和线条图的特殊宏，可以在运行 `groff` 命令之前，在文件上运行单独的命令（`eqn`、`tbl` 和 `pic` 命令）。或者，你可以向 `groff` 命令行添加选项，以便通过任何这些命令自动预处理文件（`eqn` 为 `-e`，`tbl` 为 `-t`，`pic` 为 `-p`）。

以下是一些包含在 Groff 文档中的 `EQN`、`TBL` 和 `PIC` 标记示例。第一个示例展示了一个可以由 `eqn` 处理的 Groff 文档中的方程：

```groff
.EQ
a ~ mark = ~ 30
.EN
.EQ
a sup 2 ~ + ~ - b sup 2-lineup = ~ 1000
.EN
.EQ
x sup 3 ~ + ~ y sup 3 ~ + ~ - z sup 3-lineup = ~ 1400
.EN
```

如果这出现在一个名为 `memo_eqn.mm` 的备忘录中，该备忘录将先由 `eqn` 预处理，然后使用以下命令发送到打印机：

```bash
$ groff -Tps -l -mm -e memo_eqn.mm
```

`.EQ` 和 `.EN` 宏之间的所有数据都被解释为方程。方程生成的结果输出将如图 6-5 所示。

```text
a = 30

c$^{2}$ + b$^{2}$ = 1000

x$^{3}$ + y$^{2}$ + z$^{3}$ = 1600
```

**图 6-5**：使用 `eqn` 命令的 `.EQ` 和 `.EN` 宏在文档中生成方程。

要在 Groff 文档中创建表格，请使用 `tbl` 预处理程序的 `.TS` 和 `.TE` 宏。以下是用于生成示例表格的标记示例。

```groff
.TS
center, box, tab( | )
c s s
c c c
l l l.
Mergers and Acquisitions Team
*
Employee::Title::Location

Jones, James::Marketing Manager::New York Office
Smith, Charles::Sales Manager::Los Angeles Office
Taylor, Susan::R&D Manager::New York Office
Walters, Mark::Information Systems Manager::Salt Lake City Office
Zur, Mike::Distribution Manager::Portland Office
.TE
```

在 `.TS` 宏启动表格后，下一行指示表格应在页面中居中（`center`）并被线框包围，且使用冒号将数据分隔到单元格中（`tab (:)`）。下一行显示标题应在框中居中（`c`）并跨越接下来的两个单元格（`s s`）。再下一行指示每个单元格的标题应居中（`c c c`），且跟随的数据单元格应左对齐（`l l l`）。
