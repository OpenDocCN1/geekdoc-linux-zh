
![](img/fa18693414a802b12c8add5f8c4be910_599_0.png)

man 页格式头部和横线将文本页面隔离开来。

| waycool(1) | Linux Programmer's Manual | waycool(1) |
|---|---|---|
| NAME | | | |
| waycool - cool command | | | |
| SYNTAX | | | |
| waycool [option] [ file ... ] | | | |
| VERSION | | | |
| This page documents the GNU waycool utility. | | | |
| DESCRIPTION | waycool is a cool command. This version of waycool is better than the last one. | | | |
| OPTIONS | | | | |
| -a All options with | | | |
| -s some options | | | | |
| - to affect help links of any reference it is unavailable only on systems that change the ownership of it. | | | | |
| - Print the output with the command. | | | | |
| COMMENT | If you don't like the command, don't tell us. It just hurts feelings. | | | |
| ENVIRONMENT VARIABLES | | | | |
| These variables are used by waycool: | | | | |
| DISPLAY sets the Display variable. | | | | |
| WAYCOOL | | | | |
| This determines the location of the man database. | | | | |
| AUTHOR | Created by (chisandhistory.com) | | | |
| REPORTING | Report bugs to chang-filit@hmroup.org. | | | |
| COPYRIGHT | Copyright (C) 2002 Free Software Foundation, Inc. | | | |
| This is free software; see source for copying conditions. There is no warrant not even for merchantability or fitness of a particular purpose. | | | | |
| DISCLAIMER | I'd like to thank all my friends. | | | |

# 第四部分 运行应用程序

请添加您的任何修改意见，然后在本表底部的指定批准行上签名。
`.PC`
`.SG`
`.AV "John W. Doe, XYZ 公司总裁"`
`.AV "Sylvia Q. Public, XYZ 公司首席财务官"`
`.NS`
公司范围内的每一个人。
`.NE`

图 21.6 显示了此备忘录的输出。

## 图 21.6
自动为备忘录添加标题和批准行。

![](img/fa18693414a802b12c8add5f8c4be910_603_0.png)

# 处理文字与图像

如需查看 `mm` 宏的完整列表，请参阅 `groff_mm` 手册页。存在 100 多个 `mm` 宏。此外，还有几十个定义的字符串，您可以使用它们设置并调用信息，例如插图名称、表格、目录信息以及带有不同标题自动打印的文本。

# 添加方程、表格和图片

为了解释用于方程、表格和线条图的特殊宏，您必须在运行 `groff` 命令之前，在源文件上运行单独的命令（`eqn`、`tbl` 和 `pic` 命令）。或者，您也可以向 `groff` 命令行添加选项，以便通过任何一个命令对文件进行预处理（`-e` 用于 `eqn`，`-t` 用于 `tbl`，`-p` 用于 `pic`）。

以下是包含在 Groff 文档中的 `EQ`、`TBL` 和 `PIC` 标记的某些示例。第一个示例显示了一个可以被 `eqn` 处理的方程：

```
.EQ

a ~ mark = ~ 30

.EN
```

`.sp`

```
.EQ

a sup 2 ~ + ~ b sup 2~lineup = ~ 1000

.EN
```

`.sp`

```
.EQ

x sup 3 ~ + ~ y sup 3 ~ + ~ z sup 3~lineup = ~ 1400

.EN
```

如果这出现在名为 `memoeqn.mm` 的备忘录中，该备忘录将通过 `eqn` 进行预处理，然后使用以下命令发送到打印机：

```
$ groff -Tps -l -mm -e memoeqn.mm
```

`EQ` 和 `.EN` 宏之间的所有数据都将被解释为方程。方程产生的输出将如图 21.7 所示。

## 图 21.7

使用 `eqn` 命令的 `.EQ` 和 `.EN` 宏在文档中生成方程。

![](img/fa18693414a802b12c8add5f8c4be910_604_0.png)

571

要在 Groff 文档中创建表格，使用 `tbl` 预处理器的 `.TS` 和 `.TE` 宏。以下是用于生成简单表格的标记示例：

```
.TS

center, box, tab();

c c s s

c c | c

1 | 1.

Mergers and Acquisitions Team

Employee:Title:Location=\Jones, James:Marketing Manager:New York Office

Smith, Charles:Sales Manager:Los Angeles Office

Taylor, Sarah:R&D Manager:New York Office

Walters, Mark:Information Systems Manager:Salt Lake City Office

Zur, Mike:Distribution Manager:Portland Office

.TE
```

`TS` 标记表格，下一行指示表格在页面上居中（`center`）并由线框包围，冒号将用于数据分隔到单元格中（`tab::`）。第三行显示标题在单元格中居中（`c`）并跨越接两个单元格（`s s`）。第四行说明每个单元格的标题应该居中（`c | c`），第五行指示数据单元格应该左对齐（`1 | 1 | 1`）。

> 定义行的末尾必须有一个句号。在示例中，它在表格 `1 | 1 | 1` 之后。如果没有该句号，`tbl` 将尝试将文本解释为表格定义的一部分，结果失败并停止处理表格：表格将不会打印。

表格中的其余信息都是数据。在表格中，分隔符是冒号字符（`()`）。使用 `TE` 宏结束表格。如果它出现在名为 `memotbl.mm` 的备忘录中，`tbl` 就可以预处理该备忘录并使用以下命令将其发送到打印机：

```
$ groff -Tps -1 -mm -t memotbl.mm
```

`.TS` 和 `.TE` 宏之间的数据被解释为表格。图 21.8 显示了此示例的输出。

## 图 21.8

使用 `tbl` 命令的 `.TS` 和 `.TE` 宏设置文本的对齐方式并分列。

| 员工 | 职位 | 位置 |
| :--- | :--- | :--- |
| Jones, James, Smith, Charles, Taylor, Sarah, Walters, Mark, Zur, Mike | 市场经理, 销售经理, 研发经理, 信息系统, 分销经理 | Jones, James, Smith, Charles, Taylor, Sarah, Walters, Mark, Zur, Mike |

# 处理文字与图像

`PIC` 宏（`PS` 和 `PE`）允许您在 Groff 中创建简单的图形和流程图。`PIC` 实际上仅适用于创建简单的框、圆、椭圆、线、弧、样条和某些文本。以下是可能位于 Groff 文档中的某些 `PIC` 代码。

```
.PS

box invis "Start" "Here"; arrow

box "Step 1"; arrow

circle "Step 2"; arrow

elipse "Step 3"; arrow

box "Step 4"; arrow

box invis "End"

.PE
```
