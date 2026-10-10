
```
.WA "Christopher T. Craft"
999 Anyway Way
Anytown, UT 84111 USA
.WS
.IA
John W. Doe
111 Notown Blvd.
Notown, UT 84111
.IE
.LO RN "Our telephone conversation"
.LO SA "Dear Mr. Doe:"
.IT
In reference to our telephone conversation on the 4th, I am calling to
confirm our upcoming appointment on the 18th. I look forward to
discussing the merger. I believe we have a win-win situation here.
.FC "Yours Truly,"
.SG
```

如果你使用上述代码示例前一段中提到的 `groff` 命令行，该信函的输出结果如图 6-5 所示。

![](img/fb202c163797a743c3c6cf236316bc96_298_0.png)

图 6-5：使用 `mm` 宏创建简单信函。

`mm` 宏通常用于生成技术备忘录。以下是一个签署页的示例，它可能出现在较大的技术备忘录的开头。

```
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
Please add any corrections you have, then sign the approval line indicated at the bottom of this sheet.
_FC
_SG
.AV "John W. Doe, XYZ Corporation President"
.AV "Sylvia Q. Public, XYZ Corporation CFO"
.NS
Everyone in the corporation.
.NE
```

图 6-6 展示了该备忘录的输出结果。

![](img/fb202c163797a743c3c6cf236316bc96_299_0.png)

图 6-6：自动为备忘录添加标题和批准行。

> 注意：要查看 `mm` 宏的完整列表，请参见 `groff mm` 手册页。存在 100 多个 `mm` 宏。此外，数十个已定义的字符串允许你设置和调用信息（如图形名称、表格、目录信息以及文本），这些信息将带有不同的标题自动打印出来。

## 添加方程、表格和图形

为了对用于方程、表格和线图的特殊宏进行解释，你可以在运行 `groff` 命令之前单独对该文件运行相应的命令 `eqn`, `tbl`, 和 `pic`。或者，你可以向 `groff` 命令行添加选项，以便文件由其中任何命令自动预处理（`eqn` 对应 `eqn`，`-t` 对应 `tbl`，`-P` 对应 `pic`）。

以下是一些包含在 Groff 文档中的 `EQN`、`TBL` 和 `PIC` 标记示例。第一个示例展示了可以由 `eqn` 处理的 Groff 文档中的方程：

```
.EQ
a = mark = - 30
.EN

.sp
.EQ
a sup 2 - + - b sup 2-lineup = - 1000
.EN
.sp
.EQ
x sup 3 - + - y sup 3 - + - z sup 3-lineup = - 1400
.EN
```

如果这些内容出现在名为 `memo.eqn.mm` 的备忘录中，该备忘录将首先由 `eqn` 预处理，然后使用以下命令发送到打印机：

```
$ groff -Tps -l -mm -e memo.eqn.mm
```

`.EQ` 和 `.EN` 宏之间的所有数据都被解释为方程。方程产生的输出结果如图 6-7 所示。

![](img/fb202c163797a743c3c6cf236316bc96_300_0.png)

**图 6-7：** 使用 `eqn` 命令的 `.EQ` 和 `.EN` 宏在文档中生成方程。

要在 Groff 文档中创建表格，请使用 `tbl` 预处理程序的 `.TS` 和 `.TE` 宏。以下是生成简单表格所使用的标记示例。

```
.TS
center, box, tab(:);
c s s
c | c | c
1   |  1   |  1.
Mergers and Acquisitions Team
-
Employee::Title::Location

Jones, James::Marketing Manager::New York Office
Smith, Charles::Sales Manager::Los Angeles Office
Taylor, Sarah::R&D Manager::New York Office
Walters, Mark::Information Systems Manager::Salt Lake City Office
Zur, Mike::Distribution Manager::Portland Office

.TE
```

在 `.TS` 宏启动表格后，下一行指示表格应在页面居中（`center`）并由线框包围，且使用冒号将数据分隔到单元格中 `[tab(:)]`。下一行显示标题应在框中居中（`c`）并跨下一行的两个单元格（`s s`）。再下一行指示每个单元格的标题应居中（`c c c`），且随后的数据单元格应左对齐（`1 1 1`）。

> **警告：** 表格定义行的末尾必须有一个句号。在这种情况下，它位于 `1 | 1 | 1.` 行之后。如果缺少句号，`tbl` 将尝试将文本解释为表格定义的一部分。在这种情况下，`tbl` 将失败并停止处理表格，因此表格无法打印。

表格中的其余信息是数据。注意制表符分隔符是冒号字符（`:`）。当表格完成时，使用 `.TE` 宏结束表格。如果该表格位于名为 `memotbl.mm` 的备忘录中，`tbl` 可以预处理该备忘录，然后使用以下命令将其发送到打印机：

```bash
$ groff -Tps -l -mm -t memotbl.mm
```

`.TS` 和 `.TE` 宏之间的数据被解释为表格（见图 6-8）。

| 员工 | 职位 | 地点 |

| :--- | :---: | :--- |

| Jones, James | 市场经理 | 纽约办事处 |

| Smith, Charles | 销售经理 | 洛杉矶办事处 |

| Taylor, Sarah | 研发经理 | 纽约办事处 |

| Walters, Mark | 信息系统经理 | 盐湖城办事处 |

| Zur, Mike | 配送经理 | 波特兰办事处 |

**图 6-8：** 使用 `tbl` 命令的 `.TS` 和 `.TE` 宏设置文本对齐方式并将其置于列中。

`PIC` 宏（`.PS` 和 `.PE`）允许你在 Groff 中创建简单的图表和流程图。`PIC` 实际上只适合创建简单的方框、圆形、椭圆、直线、圆弧、样条曲线以及一些文本。以下是可能出现在 Groff 文档中的一些 `PIC` 代码：

```
.PS
box invis  "Start" "Here"; arrow
box "Step 1"; arrow
circle "Step 2"; arrow
ellipse "Step 3"; arrow
box "Step 4"; arrow
box invis = "End"
.PE
```

在 `.PS` 之后，第一行指示一个包含文字 Start Here 的不可见方框（`invis`），后面跟着一个箭头。该箭头连接到下一个包含 Step 1 文字的方框。后续的元素（由箭头连接）包括一个圆形（Step 2）、一个椭圆（Step 3）、另一个方框（Step 4）以及另一个不可见方框（End）。`.PE` 表示 `pic` 绘图结束。

如果这些行出现在名为 `memopic.mm` 的文档中，你可以预处理 `PIC` 代码并使用以下命令打印该文件：

```
$ groff -Tps -l -mm -p memopic.mm
```

图 6-9 展示了此绘图的一个示例。

![](img/fb202c163797a743c3c6cf236316bc96_302_0.png)

## 使用 TeX/LaTeX 进行文本处理
