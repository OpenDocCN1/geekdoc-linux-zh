
使用命令行 `groff -mm -Tps -l letter.mm`，输出将类似于图 20-5。

![](img/23f52a815d30c05fbbf68ff8ce6d21ac_546_0.png)

**图 20-5：** 使用 mm 宏创建简单的信件。

# 第 20 章 ✦ 文字与图像处理 517

`mm` 宏经常用于生成技术备忘录。以下是一个可能放在大型技术备忘录开头的签字页示例：

- `-TL`
- 合并技术规范
- `AF "ABC 公司"`
- `AU "Christopher Craft"`
- `AT "总裁"`
- `AS`
- 本备忘录详细说明了计划合并的规范。
- `AE`
- `MT "合并描述与行动指令"`
- 根据我们与 XYZ 公司的洽谈结果，我们计划进行合并。本文件包含以下内容：
- `BL`
- `LI`
- 进度和时间表。
- `LI`
- 财务报表。
- `LI`
- 资产分配。
- `LE`
- `SP`
- 请添加您的任何修改意见，然后在页面底部的指定的批准行签字。
- `FC`
- `SG`
- `AV "John W. Doe, XYZ 公司总裁"`
- `AV "Sylvia O. Public, XYZ 公司首席财务官"`
- `NS`
- 公司全体人员。
- `NE`

图 20-6 显示了该备忘录的输出。

![](img/23f52a815d30c05fbbf68ff8ce6d21ac_547_0.png)

如需 `mm` 宏的完整列表，请参 `groff_mm` 手页。存在超过 100 个 `mm` 宏。此外，几十个定义的字符串允许您设置和调用信息，如图形名称、表格、目录信息以及带有不同标题自动打印的文本。

# 518 第四部分 ♦ 运行应用程序

![](img/23f52a815d30c05fbbf68ff8ce6d21ac_548_0.png)

**图 20-6：** 自动为备忘录添加标题和批准行。

## 添加方程、表格和图片

为了解释方程、表格和线条图的特殊宏，您可以在运行 `groff` 命令之前对文件运行单独的命令 `eqn`、`tbl` 和 `pic`。或者，您可以在 `groff` 命令行中添加选项，让任何一个命令对文件进行自动预处理 `-e` 用于 `eqn`，`-t` 用于 `tbl`，`-p` 用于 `pic`。

以下是包含在 Groff 文档中的 `EQN`、`TBL` 和 `PIC` 标记示例。第一个示例显示了一个可以被 `eqn` 处理的方程：

```
.EQ

a- mark = ~ 30

.SP

.EQ

a sup 2 ~ + ~ b sup 2~lineup = ~ 1000
```

# 第 20 章 ✦ 文字与图像处理 519

`.EN`
`.sp`
`.EQ`
`x sup 3 ~ + ~ y sup 3 ~ + ~ z sup 3-lineup = ~ 1400`
`.EN`

如果这出现在名为 `memoqn.mm` 的备忘录，该备忘录将由 `eqn` 预处理，然后使用以下命令发送到打印机：

```
$ groff -Tps -1 -mm -e memoqn.mm
```

`EQ` 和 `.EN` 宏之间的所有数据都被解释为方程。方程生成的输出将如图 20-7 所示。

![](img/23f52a815d30c05fbbf68ff8ce6d21ac_549_0.png)

图 20-7：使用 `eqn` 命令的 `EQ` 和 `.EN` 宏在文档中生成方程。

要在 Groff 文档中创建表格，请使用 `tbl` 预处理器的 `.TS` 和 `.TE` 宏。以下是生成简单表格的标记示例：

```
.TS

center, box, tab(:);

c c s s

c c | c

1 | 1.

合并与收购团队

员工:职位:地点

=

Jones, James:Marketing Manager:New York Office

Smith, Charles:Sales Manager:Los Angeles Office

Taylor, Sarah:RD Manager:New York Office

Walters, Mark:Information Systems Manager:Salt Lake City

Zur, Mike:Distribution Manager:Portland Office

.TE
```

`.TS` 开始表格，行表示表格应在页面上居中 `center` 并被线框包围，且使用冒号将数据分隔到单元格中 `tab(:)`。第三行显示标题应该在框内居中 `c`，并跨越接两个单元格 `s s`。第四行说明每个单元格的标题应该居中 `c | c`，第五行表示随后的数据单元格应左对齐 `1 | 1 | 1`。

定义行的末尾必须有一个句号。如果在 `1 | 1 | 1.` 行之后如果没有句号，`tbl` 将尝试将文本解释为表格定义并失败，停止处理表格；`tbl` 则不会。

其余信息在表格数据中。注意 `tab` 分隔符是字符 `:`。用 `.TE` 宏结束表格。如果表格在名为 `memobl.mm` 的备忘录中，`tbl` 可以预处理该备忘录，然后使用以下命令发送到打印机：

```
$ groff -Tps -1 -mm -t memotbl.mm
```

`.TS` 和 `.TE` 宏之间的数据被解释为表格。图 20-8 显示了此示例的输出。

| 员工 | 地点 |
|---|---|
| Jones, James, Smith, Charles, Taylor, Sarah, Walters, Mark, Zur, Mike | Marketing Manager, Sales Manager, R&D Manager, Information Systems Manager, Distribution Manager, Jones, James, Smith, Charles, Taylor, Sarah, Walters, Mark, Zur, Mike |

**图 20-8：** 使用 `tbl` 命令的 `.TS` 和 `.TE` 宏设置文本的列方式。

`PIC` 宏 `PS` 和 `.PE` 允许您在 Groff 中创建简单的图形和流程图。`Pics` 仅用于创建简单的框、圆、椭圆、线、弧、样线和某些文本。以下是可在 Groff 文档使用的 `PIC` 代码：

```
.PS

box invis "Start" "Here"; arrow

box "Step 1": arrow

circle "Step 2": arrow

elipse "Step 3": arrow

box "Step 4": arrow

box invis "End"

.PE
