
在 HOW-TO 和输入文件之前，页面是关于 UNIX（以及类 UNIX）系统信息的字体。每个命令、文件格式、设备或其他组件都有它们自己的 man 页，或者被分组在具有相似组件的 man 页中。创建你的 man 页需要你学习几个宏（特别是 man 宏）。图 6-3 显示了一个名为 waycol 命令的虚构 man 页源码。

```
.macro1 - groff processor source for the waycol command
.TH man 1 "Man IT, 2" GNU "Linux Programmer's Manual"
.SH NAME
example, my cool command
.SH SYNOPSIS
\fbVR [fVR-abfVR] [f file ... [f VR]
This man page describes the GNU man page version X.XX
.SH SECTION
\fbVR is a cool command.
.SH DESCRIPTION
This version of \fbVR is better than the last one.
.SH OPTIONS
All options with it,
Run some options.
-f -p
effect affect symbols instead of any referred file
(only on options that can change the ownership of a symbolic link)
.SH COMMAND
If you like this command, don't tell me, it will just hurt my feelings.
.SH ENVIRONMENT VARIABLES
These variables are used by \fbVR:
.TP "DISPLAY"
This is the Display variable.
This contains the location of the waycol database.
.SH FILEPATH
/usr/local/man - Directory containing waycol
.SH AUTHOR
Chris Craft (chris@gnuhistory.com)
.SH REPORT
Report bugs to bug-help@gnu.org.
.SH SUPPORT
Copyright © 2001 Free Software Foundation, Inc.
.SH NOTES
This software is here for cooling conditions. There is NO
warrant even for HERABILITY or FITNESS FOR A PARTICULAR PURPOSE.
.SH RECOMMENDATION
I'd like to tell all my friends.
```

图 6-3：创建 man 页的简单标记。

> **提示：**大多数页面存储在`/usr/share/man`的子目录中。在你创建页面之前，参考类似的 man 页以查看它们包含的内容。`man1`是命令；`man2`是系统调用；`man3`是库函数；`man4`是特殊设备（`/dev/*`）；`man5`是文件格式；`man6`是游戏；`man7`是杂项；`man8`是管理命令。IP 格式用于这些内容的缩进。例如，`/B`将当前字体改为粗体，`/I`将字体改为斜体，`/R`改为普通。（这种标记更好，因为它只需要更改字体为粗体、斜体或普通。）图 6-4 显示了 weeway 格式化后的样子：

```
$ groff -man -Tps -1 weeway
```

![](img/6a)

6-4：创建 man 页的简单标记。

## 第 6 章：在 Fedora 和 RHEL 上发布

| 宏 | 描述 |
| :--- | :--- |
| -B | 粗体 |
| -I | 斜体 |
| -R | 普通 |

*(注：后续重复的表格行已根据要求省略)*

## 第二部分：使用 Fedora RHEL

- 日程表和时间表。
- 财务报表。
- 资产配置。

请添加您的任何修改意见，然后在在本表底部的指定批准行处签名。

AV: “John W. Doe，XYZ 公司总裁”

AV: “Sylvia Q. Public，XYZ 公司首席运营官”

公司全体人员。

图 6-6 显示了此备忘录的输出。

![](img/6a8f767dda2519b458f97c2e7f586576_305_0.png)

图 6-6：自动为备忘录添加标题和批准行。

> 注意：欲需 `mm` 宏的完整列表，请参阅 `gross_mm` 页面。超过 100 个 `mm` 宏和几十个定义的字符串允许您设置和召回信息（例如图形名称、表格、目录信息和文本），这些信息会自动带有不同的标题打印。

## 第 6 章：使用 Fedora 和 RHEL 进行发布

### 添加方程、表格和图片

为了解释方程、表格和线条图的特殊宏，您可以在运行 `groff` 命令之前对文件运行单独的命令（`eqn`、`tbl` 和 `pic`）。或者，您也可以向 `groff` 命令行添加选项，以便通过任何一个命令对文件进行自动处理（`-e` 用于 `eqn`，`-t` 用于 `tbl`，`-p` 用于 `pic`）。

以下是包含在 Groff 文档中的 EQN、TBL 和 PIC 标记的一些示例。第一个示例显示了一个可以被 `eqn` 处理的 Groff 文档中的方程：

```
.EQ
a - mark = 30
.EN
.SP
.EQ
a sup 2 - + b sup 2-lineup = 1000
.EN
.SP
.EQ
x sup 3 - + y sup 3 - + z sup 3-lineup = 1400
.EN
```

如果这些内容出现在名为 `memoeqn.mm` 的备忘录中，该备忘录将先由 `eqn` 预处理，然后使用以下命令发送到打印机：

```bash
$ groff -Tps -1 -mm -e memoeqn.mm
```

方程 `.EQ` 和 `.EN` 宏之间的所有数据都被解释为方程。方程生成的输出结果将如图 6-7 所示。

![](img/6a8f767dda2519b458f97c2e7f586576_306_0.png)

**图 6-7：** 使用 `eqn` 命令 `.EQ` 和 `.EN` 宏在文档中生成方程。

要在 Groff 文档中创建表格，使用 `tbl` 预处理器的 `.TS` 和 `.TE` 宏。以下是用于生成简单表格的标记示例。

```
.TS
center, box, tab();
cs s
c | | c
1 | 1 | 1.
Mergers and Acquisitions
Employee:Title:Location
```

## 第二部分：使用 Fedora 和 RHEL

Jones, James:市场经理:纽约办公室

Smith, Charles:销售经理:洛杉矶办公室

Taylor, Sarah:研发经理:纽约办公室

Walters, Mark:信息系统经理:盐湖市办公室

Zur, Mike:分销经理:波特兰办公室

TE

在 `TS` 宏开始表格后，下一行指示表格应该居中（`center`），并被线框包围，冒号将用于将数据划分为单元格 `[tab :]]`。下一行显示标题应该在框内居中（`c`），并应跨越接两个单元格（`s s`）。该行指示每个单元格的标题应该居中（`c | c | c`），且随后的数据应左对齐（`l | | 1`）。

> 警告：表格定义行末尾必须有一个句号。在这种情况下，如果是 `1 | 1.` 。如果没有这个句号，`tbl` 将尝试将文本解释为表格的一部分。在本文此例中 `tbl` 将失败并停止处理，因此表格将无法打印。

表格中的其余信息是数据。注意，表格分隔符是字符 `()`。当表格完成后，您使用 `.TE` 宏结束。如果有一个名为 `memotl.mm` 的备忘录，`tbl` 将预处理该备忘录，然后使用以下命令将其发送到打印机：

```bash
$ groff -Tps -1 -mm -t memotl.mm
```

数据 `.TS` 和 `TE` 宏被解释为表格（见图 6-8）。

| 员工 | 职位 | 位置 |
| :--- | :--- | :--- |
| Jones, James | 市场经理 | Jones, James |
| Smith, Charles | 销售经理 | Smith, Charles |
| Taylor, Sarah | 研发经理 | Taylor, Sarah |
| Walters, Mark | 信息系统经理 | Walters, Mark |
| Zur, Mike | 分销经理 | Zur, Mike |

**图 6-8：** 文字在 `tbl` 命令 `.TS` 和 `TE` 宏的列中如何进行对齐和对定位。

`PIC` 宏（`.PS` 和 `.PE`）允许您在 Groff 中创建简单的图表和流程图。`PIC` 非常适合创建简单的方框、圆、椭圆、线、弧、样条和一些文本。以下是可能包含的 PIC 代码：
