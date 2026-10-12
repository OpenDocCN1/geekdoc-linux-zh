

![](img/1744bde8c889adfab3fc911e1687fecf_247_0.png)

**图 6-4**：自动在备忘录中添加标题和审批行。

> **注意：** 关于 mm 宏的完整列表，请参阅 **groff _mm** 手册页。存在 100 多个 mm 宏。此外，还有数十个已定义的字符串，可用于设置和调用信息（例如图形名称、表格、目录信息以及文本），这些信息会自动以不同的标题打印出来。

## 添加方程、表格和图片

若要解释用于方程、表格和线条图的特殊宏，可以在运行 **groff** 命令之前，在文件上运行单独的命令（**eqn**、**tbl** 和 **pic** 命令）。或者，你可以向 **groff** 命令行添加选项，以便通过任何这些命令自动预处理文件（**eqn 为 -e**，**tbl 为 -t**，**pic 为 -p**）。

以下是一些包含在 Groff 文档中的 EQN、TBL 和 PIC 标记示例。第一个示例展示了一个可以由 eqn 处理的 Groff 文档中的方程：

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

如果这出现在一个名为 `memo_eqn.mm` 的备忘录中，该备忘录将先由 eqn 预处理，然后使用以下命令发送到打印机：

```bash
$ groff -Tps -l -mm -e memo_eqn.mm
```

.EQ 和 .EN 宏之间的所有数据都被解释为方程。方程生成的结果输出将如图 6-5 所示。

```text
a = 30

c$^{2}$ + b$^{2}$ = 1000

x$^{3}$ + y$^{2}$ + z$^{3}$ = 1600
```

**图 6-5**：使用 eqn 命令的 .EQ 和 .EN 宏在文档中生成方程。

要在 Groff 文档中创建表格，请使用 tbl 预处理程序的 .TS 和 .TE 宏。以下是用于生成示例表格的标记示例。

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

在 .TS 宏启动表格后，下一行指示表格应在页面中居中（center）并被线框包围，且使用冒号将数据分隔到单元格中（tab (:)）。下一行显示标题应在框中居中（c）并跨越接下来的两个单元格（s s）。再下一行指示每个单元格的标题应居中（c c c），且跟随的数据单元格应左对齐（l l l）。

**警告：** 表格定义行末尾必须有一个句点。在这种情况下，它位于 l l l 行之后。如果没有这个句点，tbl 将尝试将文本解释为表格定义的一部分。在这种情况下，tbl 将失败并停止处理表格，因此表格将无法打印。

表格中的其余信息是数据。请注意，标签分隔符是冒号字符（ : ）。当表格完成后，使用 .TE 宏结束它。如果该表格位于名为 `memo.tbl.mm` 的备忘录中，tbl 可以预处理该备忘录，然后使用以下命令将其发送到打印机：

```bash
$ groff -Tps -l -mT -t memo.tbl.mm
```

.TS 和 .TE 宏之间的数据被解释为表格。图 6-6 显示了此示例。

| 员工 | 职位 | 地点 |
| :--- | :--- | :--- |
| Jones, James | 市场经理 | 纽约办公室 |
| Smith, Charles | 销售经理 | 洛杉矶办公室 |
| Taylor, Susan | 研发经理 | 纽约办公室 |
| Walters, Mark | 信息系统经理 | 盐湖城办公室 |
| Zur, Mike | 分销经理 | 波特兰办公室 |

**图 6-6**：使用 tbl 命令的 .TS 和 .TE 宏设置文本的对齐方式并放入列中。

PIC 宏（.PS 和 .PE）允许你创建简单的图表和流程图，用于 Groff。PIC 实际上只适合创建简单的方框、圆形、椭圆形、直线、弧线、样条曲线和一些文本。以下是 Groff 文档中可能包含的一些 PIC 代码：

```groff
.PS
box invis "Start" "Here"; arrow
box "Step 1"; arrow
circle "Step 2"; arrow
ellipse "Step 3"; arrow
box "Step 4"; arrow
box invis "End"
.PE
```

在 .PS 之后，第一行指示一个不可见的方框（invis），其中包含“Start Here”（此处开始）字样，随后是一个箭头。该箭头连接到下一个包含“Step 1”（步骤 1）字样的方框。下一个元素（由箭头连接）是一个圆形（Step 2）、一个椭圆形（Step 3）、另一个方框（Step 4）以及另一个不可见的方框（End）。.PE 表示 pic 绘图的结束。

如果这些行出现在名为 `memo_pic.mm` 的文档中，你可以使用以下命令预处理 PIC 代码并打印该文件：

```bash
$ groff -Tps -l -mm -p memo_pic.mm
```

**图 6-7** 展示了此绘图的一个示例：

![](img/1744bde8c889adfab3fc911e1687fecf_249_0.png)

**图 6-7**：使用 pic 命令的 .PS 和 .PE 宏创建简单的流程图。

## 使用 TeX/LaTeX 进行文本处理

TeX 是一组主要用于制作科学和数学排版文档的命令。使用 TeX 最常见的方法是调用宏包。TeX 最受欢迎的宏包是 **LaTeX**，它采用更高级的方式对 TeX 文档进行格式化。TeX 和 **LaTeX** 工具包含在 `tetex-latex` 软件包中。

**注意：** 本节中描述的 `tetex-*` 软件包未安装在 Red Hat Linux 工作站安装中。所需的软件包位于随本书提供的 CD-1 上；可选软件包位于 CD-2 上。

TeX 从 `latex` 格式文件（`latex.fmt`）中解释 **LaTeX** 宏。默认情况下，当安装 TeX 软件包时，`latex.fmt` 和 `plain.fmt` 格式文件是仅有的自动构建的文件。你可以与 TeX 配合使用的其他宏文件包括：

- **amstex** — 数学出版物，美国数学会将其用作其官方排版系统。
- **eplain** — 包含用于索引和目录的宏。
- **texinfo** — 自由软件基金会用于生成软件手册的宏。这些宏的文本输出可与 Red Hat Linux 的 `info` 命令一起使用。

你可以使用任何文本编辑器创建 TeX/**LaTeX** 文件。在创建文本和宏后，你可以运行 `tex` 命令（或几个其他相关实用程序之一）来格式化该文件。输入文件的形式为 `filename.tex`。输出通常是三个不同的文件：

- `filename.dvi` — 这是设备无关的输出文件，可以转换用于几种不同的输出设备（如 PostScript）。
- `filename.log` — 这是一个日志文件，包含诊断消息。
- `filename.aux` — 这是一个由 **LaTeX** 使用的辅助文件。

生成的 `.dvi` 文件可以为特定设备格式化。例如，你可以使用 `dvips` 命令将生成的 `.dvi` 文件输出到你的 PostScript 打印机（`dvips filename.dvi`）。或者，你可以使用 `xdvi` 命令在 X 中预览 `dvi` 文件。

### 创建和格式化 **LaTeX** 文档

由于 **LaTeX** 是使用 TeX 最常见的方式，本节介绍了如何创建和格式化 TeX 文档。**LaTeX** 宏（通常称为命令）在文档中以以下两种形式之一出现：

- `\string{option}[required]` — 首先是一个反斜杠 (\)，其后跟随一串字符。（用命令名称替换 *string*。）可选参数包含在花括号 ({}) 中，必需参数包含在方括号 ([]) 中。
- `\?{option}[required]` — 首先是一个反斜杠 (\)，其后跟随单个非字母字符。（用命令字符替换 *?*。）可选参数包含在花括号 ({}) 中，必需参数包含在方括号 ([]) 中。

