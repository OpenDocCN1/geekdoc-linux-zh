
$ `groff -man -T waycool.1`

```
![](img/a123b4f2456cac935474ae2401b95b01_589_0.png)
```
图 21-4：man 页格式添加标题并布局了文本页面。

表 21-1 列出了你可以在 man 页上使用的宏。这些宏在 `man(7)` 手页中有描述（输入 `man 7 man` 查看该页面）。

## 表 21-1
Man 宏

| 宏 | 描述 |
|---|---|
| `.B` | 粗体。 |
| `.BI` | 粗体，后接斜体（交替）。 |
| `.BR` | 粗体，后接正（交替）。 |
| `.DT` | 设置默认制表。 |
| `.HP` | 开始悬挂缩进。 |
| `.I` | 斜体。 |
| `.IB` | 斜体，后接粗体（交替）。 |
| `.IP` | 开始悬挂标签。选项使用 `.TP`。 |
| `.IR` | 斜体，后接罗马（交替）。 |
| `.LP` | 开始段落。 |
| `.PD` | 设置段落之间的距离。 |
| `.PP` | 开始段落。 |
| `.RB` | 罗马，后接粗体（交替）。 |
| `.RE` | 结束相对缩进（在 `.RS` 之后）。 |
| `.RI` | 罗马，后接斜体（交替）。 |
| `.RS` | 开始相对缩进（使用 `.RE` 结束缩进）。 |
| `.SB` | 小号字体，后接粗体（交替）。 |
| `.SM` | 小号字体。用于显示全大写单词。 |
| `.SH` | 节标题。 |
| `.SS` | `.SH` 标题内的子标题。 |
| `.TH` | 标题标题。在 man 页开头使用一次。 |
| `.TP` | 开始悬挂标签。在下一行开始文本，不与标签在同一行。 |

## 使用 Groff 创建信件、备忘备忘录或白皮书

备忘录宏（配合 `groff` 的 `-mm` 选项使用）曾曾在 UNIX 用户中非常流行，用于制作技术文档、信件和备忘录。尽管带有各种 WYSIWYG 模板的现代文字处理器已让 `mm` 宏变得过时，但在紧急关头，它们仍然是在文本环境中创建排版风格文档的快速方法。

要使用 `mm` 宏格式化并打印（到 PostScript 打印机）文档，请使用以下命令：

```
$ groff -Tps -1 letter.mm
```

这里是如何使用 `mm` 宏制作信件的简单示例：

```
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

In reference to our telephone conversation on the 4th, I am calling to confirm our upcoming appointment on the 18th. 

I look forward to discussing the merger. I believe we have a ***win-win* situation here.

.FC "Yours Truly,"

.SG
```

使用以下命令格式化文档并将输出保存到命名的 `letter.ps` 中：

```
$ groff -Tps -1 letter.mm > letter.ps
```

输出将类似于图 21-5。

> 如果你从 `groff` 命令获得的输出显示 `letter.mm:15: warning 'title' not defined`，你可以安全地忽略它。或者，在第一行尾添加一组空引号。即，将 `letter.mm` 的第一行改为 `.WA "Christopher T. Craft" ""`

![](img/a123b4f2456cac935474ae2401b95b01_592_0.png)

图 21-5：使用 `mm` 宏创建简单的信件。

`mm` 宏经常被用于制作备忘录。以下是一个可能放在大型备忘录开头的签签字页示例：

```
.TL

Merger Technical Specifications

.AF "ABC Corporation"

.AU "Christopher Craft"

.AT "President"

.AS

This memo details the specifications for the planned merger.

.AE

.MT "Merger Description and Orders"

As a result of our talks with XYZ, we plan to go forward with the merger. This document contains the following:

.BL

Schedule and tables.

.LI

Financial statements.

.LI

Asset allocations.

.LE

SP

Please add any corrections, then sign the approval line indicated at the bottom.

```

`FC`
`.SG`
`.AV "John W. Doe, XYZ President"`
`.AV "Sylvia Q. Public, XYZ CFO"`
`.NS`
`Everyone in the corporation.`
`.NE`

图 21-6 显示了此备忘录的输出。

![](img/a123b4f2456cac935474ae2401b95b01_593_0.png)

图 21-6：在备忘录中添加标题和批准行。

## 添加方程、表格和图片

要解释用于方程、表格和线条图的特殊宏，你必须在运行 `groff` 命令之前，在源文件上运行单独的命令（`eqn`、`tbl` 和 `pic`）。或者，你可以在 `groff` 行中添加选项，以便由任何命令对文件进行预处理（`-e` 用于 `eqn`，`-t` 用于 `tbl`，`-p` 用于 `pic`）。

以下是 `Groff` 文档中 `EQ`、`TBL` 和 `PIC` 标记的一些示例。第一个示例显示了一个可以被 `eqn` 处理的方程：

```
.EQ
a = 30
.EN
.SP
.EQ
a = 2
.SP
.EQ
x + y = 14
.EN
```

如果这出现在 `memoeqn.mm` 中，该内存将被 `eqn` 预处理并使用以下命令发送到打印机：

```
$ groff -Tps -1 -e memoeqn
```

`.EQ` 和 `.EN` 之间的所有数据将被解释为方程。产生的输出如图 21-7 所示。

![](img/a123b4f2456cac935474ae2401b95b01_594_0.png)

图 21-7：使用 `eqn` 的 `.EQ` 和 `.EN` 宏在文档生成方程。

要在 `Groff` 文档中创建表格，使用 `tbl` 处理器的 `.TS` 和 `.TE` 宏。以下是制作简单表格的标记示例：

```
.TS
center, box, tab();
cs s
c c | c
c | 1 | 1.
Mergers and Acquisitions Team
=
Employee:Title:Location
Jones, James:Manager:New York Office
Smith, Charles:Sales Manager:Los Angeles Office
Taylor, Sarah:R&D Manager:New York Office
Walters, Mark:Information Systems Manager:Salt Lake City
Zurk, Mike:Distribution Manager:Portland Office
.TE
```

`TS` 宏开始表格，下一行指示表格应在页面居中（`center`）并被线框包围，使用冒号（`:`）分隔数据单元（`Tab()`）。第三行显示标题应居中并跨两个单元（`s`）。第四行显示每个单元的标题应居中（`| c | c`），第五行指示随后的数据单元将对齐（`| l | l`）。

> 表格定义的结尾必须有一个句号。在示例中，在 `| l | l |` 行之后。如果没有句号，`tbl` 会尝试将文本解释为表格定义，失败并停止表格；表格不会打印。

表格中的其余信息是数据。注意制表符（`:`）。使用 `.TE` 宏结束表格。

# 第 21 章 ✦ 处理文字与图像 565

`PIC` 宏（`.PS` 和 `.PE`）允许你在 `Groff` 中创建简单的图表和流程图。`PIC` 实际上仅擅长创建简单的方框、圆形、椭圆、线条、弧、脊线和一些文本。以下是可能出现在 `Groff` 文档中的 `PIC` 代码：

```
.PS
box "Start" "Here"; arrow
box "Step 1"; arrow
circle "Step 2"; arrow
elipse "Step 3"; arrow
box "Step 4"; arrow
box "End"
.PE
```
