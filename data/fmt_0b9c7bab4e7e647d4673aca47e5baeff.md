
LaTeX 分发版 `NTeX` 和 `TeTeX` 已经包含了英国英语、美国英语、德语以及其他几种语言的内置连字符文件。例如，德语连字符可以通过 `german` 宏包进行激活。

## 单词间距与水平间距

为了使段落的每行对齐，LaTeX 在（同一行内）所有单词之间插入相同数量的空间，并在句号（句子结束处）后留出稍宽的空格。如果句号后仅使用普通空格（例如缩写词），则必须在句号后指定 `\_`：例如 `Prof.\ Huber` 用于 `Prof. Huber`。（`u`）表示空格。）当两个单词不应被换行分隔时，可以使用 `\~` 指定固定空格，例如 `3~cm`。

可以通过 `\quad`、`\qquad` 或 `\hspace{distance}` 在两个单词之间插入额外空间。应避免在这些命令的前后出现多余空格，因为它们可能会无意中导致更宽的空格。

上述三个命令生成的空间具有精确预定义的宽度。`\fill` 命令则完全不同。该命令在当前位置插入行中所有可用的空间。如果在一行中多次使用 `\fill`，插入的空间将相应减少。如果在行尾使用 `\fill`，则行必须以 `\hbox{}` 结束。这创建了一个不可见的 LaTeX 对象，作为 `\fill` 的限制。示例：

```
\fill centered \fill{}
```

`centered` 居中

| \| | 标点符号后的单词间距 |
| :--- | :--- |
| `\quad` | 固定空格；行在此处不会断开 |
| `\qquad` | 宽度为 1 em 的额外空间（见下文） |
| `\hspace{distance}` | 宽度为 2 em 的额外空间（见下文） |
| `\hspace*{distance}` | 指定宽度的空间 |
| `\fill` | 同上，但也支持换行 |
| `\dotfill` | 同上，但使用虚线代替空格 |
| `\hfill` | 同上，但使用连续线 |
| `\hbox{}` | 不可见的 LaTeX 对象（作为 `\fill` 的限制） |

在 `\hspace` 等命令中的数值可以使用小数点或十进制逗号来指定。该值必须始终以测量单位结束（即使单位为 0）。LaTeX 允许以下单位：

| unit | 描述 |
| :--- | :--- |
| `mm` | 毫米 |
| `cm` | 厘米 |
| `pt` | 磅 (1 = 0.353 mm) |
| `ex` | 当前字符集中 `'x'` 的高度 |
| `em` | 当前字符集中一个破折号 (`--`) 的宽度 |

## 换行与垂直间距

在段落中，只有当当前行没有剩余空间时，LaTeX 才会开始新行。可以使用 `\\` 提前换行。如果在指定的指定了用方括号括的距离后，LaTeX 还会插入相应的垂直空间：`\\[1cm]`。如果在 `\\` 和距离指定之间放置一个 `*`，则在执行分页时也会插入该垂直空间。（这只在极罕见的情况下才有意义！）`\vspace{distance}` 可用于在两个段落之间插入额外空间。所有测量值都可以指定负值。

```
\\ line break 不带对齐的换行（行左对齐）

\\[distance] line break 增加到下一行间距的换行

\* \\[distance] 同上，但在分页时也适用

\linebreak line break 带对齐的换行

\vspace{distance} between two paragraphs 两个段落之间的额外空间

\vspace*{distance} between two paragraphs 同上，但在分页时也适用
```

## 强制分页

可以通过三个命令 `\newpage`、`\pagebreak` 和 `\clearpage` 获取强制分页。差异如下所示：

- `\newpage` 开始新页/新列，当前页其余部分留空
- `\pagebreak` 同上，但进行垂直对齐（段落之间的间距更大）
- `\clearpage` 开启新页，即使是双栏文本也是如此

## 用户自定义页眉

通常，LaTeX 处理页眉和页脚。你可以使用 `\pagestyle` 命令定义它们。常见的样式有 `plain`（普通）、`empty`（空）和 `headings`（标题）。`plain` 样式用于章节的第一页，而 `empty` 样式没有页眉页脚。`headings` 样式包含章节名称、节名称和页码。你也可以使用 `fancyhdr` 宏包自定义这些样式，它允许对页眉页脚进行完全控制。

```
\usepackage{fancyhdr}

\pagestyle{fancy}

\fancyhead[L]{Chapter Name}

\fancyhead[R]{Section Name}

\fancyfoot[C]{\thepage}

\fancyheadrulewidth
```
