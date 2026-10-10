
> 提示：使用 `man2html` 可以 man 页转换为 HTML 格式并在浏览器中显示。`zcat /usr/share/man/man/chown.1.gz | man2html > /tmp/chown.htm`

## 第二部分：使用 Fedora RHEL

### 使用 Groff 创建映射

在 HOW-TOs 和 info 文件之前，man 页是关于 UNIX（以及类 UNIX）系统信息的字体。每个命令、文件格式、设备或其他组件要么有自己的 man 页，要么与相似的组件分组在一个 man 页中。创建你自己的 man 页需要你学习一些宏（特别是 man 宏）。图 6-3 显示了一个用于命令良好布局的虚构映射源码。

> **提示：**大多数 man 页存储在 `/usr/share/man` 的子目录下。在创建 man 页之前，请参考类似的 man 页以查看它们的标记和包含的页眉。`man1` 是命令；`man2` 是系统调用；`man3` 是库函数；`man4` 是特殊文件 (`/dev/*`)；`man5` 是格式；`man6` 是游戏；`man7` 是杂项组件；`man8` 是管理命令。

man 页中使用了几类宏。`.IP` 宏用于格式化缩进段落等等内容。man 页还包含一些低级请求；例如，`\B` 表示将当前字体更改为**粗体**，`\f` 将字体更改为*斜体*，`\R` 将其恢复为正体。（这种标记比请求特定类型更好，因为它只是改变当前字体的粗体、斜体或正体。）图 6-4 显示了 `wecol` 映射在用 `groff` 格式化后的样子：

```bash
$ groff -man -Tps -l wecol.1
wecol.1 - the document processor for the wecol command
# man1 "May 12, 2002" "Linux Programmer's Manual"
# SH AUTHOR
# my cool command
wecol.1
# SH SECTION
# \fB[\f-abcVR\R] [ \f file ... \R]
# This man page documents the Groff manual version X.XX
# SH NAME
# wecolVR is a cool command.
# SH DESCRIPTION
# This version ofwecolVR is better than the less one.
# SH OPTIONS
Run all options with it.
# -p align
# effect indent lines instead of any reflowed
(enable only on systems that can change the
#capability of alignment)
# - print the line number with the command,
# COMMENTS
# If you like the command, don't tell me. It will just hurt my feelings.
# SH ENRICHMENT VARIABLES
# These environment variables are used by
```

图 6-6 显示了此备录的输出。

![](img/c7605e408543e0a1829c1fd0cf2f687d_301_0.png)

**图 6-6：** 自动为备录添加标题和批准行。

> **注意：** 有关 `mm` 宏的完整列表，请参见 `groff mm` 手页。存在超过 100 个宏。此外，几十个定义的字符串允许你设置和召回信息（例如图形名称、表格、图形、目录信息和文本），这些信息将使用不同的标题打印。

### 添加公式、表格和图片

为了解释用于公式、表格和线条图的特殊宏，你可以在运行 `groff` 命令之前，在文件上运行单独的命令（`eqn`、`tbl` 和 `pic` 命令）。或者，你也可以为 `groff` 命令添加选项，以便通过任何一个命令对文件进行预处理（`-e eqn`、`-t tbl` 和 `-p pic`）。

以下是 Groff 文档中包含的一些 `EQN`、`TBL` 和 `PIC` 标记示例：第一个示例显示可以使用 Groff 文档处理的公式：

```
.EQ
a ~ - mark = ~ 30
.EN
.sp
.EQ
a sup 2 ~ + ~ b sup 2-lineup = ~ 1000
.EN
.sp
```

.EQ

x sup 3 - + y sup 3 - + z sup 3-lineup = - 1400

.EN

如果这出现在名为 `memoeqn.mm` 的备录中，该备录将先由 `eqn` 预处理，然后使用以下命令发送到打印机：

```
$ groff -Tps -l -mm -e memoeqn.mm
```

`EQ.` 和 `EN` 宏之间的所有数据都被解释为公式。公式生成的输出将如图 6-7 所示。

![](img/c7605e408543e0a1829c1fd0cf2f687d_302_0.png)

**图 6-7：** 使用 `eqn` 命令的 `.EQ` 和 `.EN` 宏在文档中生成公式。

要在 Groff 文档中创建表格，使用 `tbl` 预处理器的 `.TS` 和 `.TE` 宏。以下是生成简单表格的标记示例。

```
.TS
center, box, tab(:);
c c s s
c c | c | c
l1 | l1 | l1.
```

合并收购团队

员工：职位：市场经理

```
Jones, James:Marketing Manager:New York Office
Smith, Charles:Sales Manager:Los Angeles Office
Taylor, Sarah:RaD Manager:New York Office
Walters, Mark:Information Systems Manager:Salt Lake City Office
Zik, Mike:Distribution Manager:Portland Office
.TE
```

在 `.TS` 宏开始表格后，该行表示标题应该在 `(center)` 处居中，并用线框包围，使用冒号将数据分隔到单元格中 `(tab(:))`。该行显示标题应该在框内居中 `(c)`，并且应该跨越接两个单元格 `(s s)`。随后的行表示每个单元格的标题应该居中 `(c | c)`，随后的数据单元格应该左对齐 `(l 1 | l | 1)`。

> 警告：表格定义行的末尾必须有一个句号。在这种情况下，它在 `l | line.` 之后。如果没有句号，`tbl` 将尝试将文本解释为表格定义的一部分。在这种情况下，`tbl` 将失败并停止处理表格，因此表格不会打印。

表格中的其余信息是数据。注意制表符是冒号字符 `(:)`。表格完成后，使用 `.TE` 宏结束。如果表格位于名为 `metobl .mm` 的备录中，`tbl` 可以预处理该备录，然后使用以下命令将其发送到打印机：

```
$ groff -Tps -1 -mm -t metobl.mm
```

`.TS` 和 `.TE` 宏之间的数据被解释为表格。图 6-8 显示了此示例。

| 员工 | 位置 |

| :--- | :--- |

| Jones, James Smith, Charles | Marketing Manager Sales Manager R&D Manager Information Systems Manager Distribution Manager |

| Taylor, Sarah Walters, Mark Zur, Mike | Jones, James Smith, Charles Taylor, Sarah Mark Mike |

图 6-8：使用命令 `.TS` 和 `.TE` 宏设置文本对齐方式并分列。

`PIC` 宏（`.PS` 和 `.PE`）允许你在 Groff 中创建简单的图形和流程图。`PIC` 别适合创建简单的框、圆、椭圆、线、样线和一些文本。以下是可能位于 Groff 文档中的某些 `PIC` 代码：

```
.PS
box invis "Start "Here"; arrow
box "Step 1"; arrow
circle "Step 2"; arrow
elipse "Step 3"; arrow
box "Step 4"; arrow
box invis "End"
.PE
```

在 `.PS` 之后，第一行表示一个包含 Start Here 字样的隐藏框 `(invis)`，后面是一个箭头。该箭头连接到下一个框 `(Step 1)`。圆 `(Step 2)`、椭圆 `(Step 3)`、框 `(Step 4)` 和另一个隐藏框 `(End)`。如果这些出现在名为 `memoeqn.mm` 的备录中，该备录将先由 `eqn` 预处理，然后使用以下命令发送到打印机：

```
$ groff -Tps -l -mm -e memoeqn.mm
```
