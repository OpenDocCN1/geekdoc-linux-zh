
# 用 LaTeX 编写书籍

用代码简化出版流程

![](img/2f9ef091d4813dbe86196f72ccfd0107_32_0.png)

## 07 代码格式化

LaTeX 会生成带有目录、插图列表和表格列表的页面。使用命令创建目录 (TOC)：

```latex
\tableofcontents
```

如果你只想包含章节和节的条目，请在第6 步中包含以下前缀：

```latex
\setcounter{tocdepth}(1)
```

为了包含插图列表，请插入以下命令：

```latex
\listofffigures
```

如果书中中有表格，你可以如下所示生成表格列表：

```latex
\listoftables
```

```latex
\usepackage{resize, color, fancyv}
\newenvironment{MyCode}[number,leftframe,rule=1pt,framecolor=blue]
```

创建一个良好的样式同样重要。此外，如果你想创建一个与现有样式相似的新样式，可以复制粘贴现有的样式定义，选择不同的名称和你需要的修改。

```latex
\newcommand{\headrule}{0.5pt width\height{-4pt}}
```

```latex
\fancyhead{RO}
\fancyhead{\thesection}{\LARGE}\normalsize}{\right}
\fancyhead{\right}
```

```latex
\fancyhead{LE}
\fancyhead{\thesection}{\LARGE}\normalsize}{\left}
\fancyhead{\left}
```

```latex
\fancypagestyle{plain}
\fancyfoot{\thepage}
\fancyfoot{\LARGE}
\fancyfoot{\center}
\newcommand{\headrulewidth}{0pt}
```

你现在可以使用以下方法在 LaTeX 中使用 `MyCode` 样式了：

## 10 包含页眉和页脚

以下 LaTeX 代码生成页面的页眉和页脚。右页 (`RO`) 与左页 (`LE`) 不同。还需要注意的是，每个章节的第一页 (`COI`) 有另一个规则，将页码放在页脚底部，并带有任何页眉信息。

## 12 生成索引

仪表板

- `apple-dashboard-region` CSS sass, 111
- `spejs`, 182
- `wgt`, 62
- `Alo`, 151
- `Ajax`, 6
- `alert`, 145
- `alert(function)`, 282
- `AllowAccessOutOfWidget`, 68
- `C+`, 0, 78, 122

## 1.1 章节

你可以在 LaTeX 代码中这样引用 `Kernighan8`：

> :Kernighan8

## 06 创建参考文献

LaTeX 提供了 `BibTeX` 来处理参考文献。所有的 `BibTeX` 条目将位于一个名为 `biblist.bib` 的文件中。每个 `BibTeX` 条目都遵循以下格式：

> @Kernaghan8
>
> author = (Brian W. Kernighan and Robert Pike)
> title = (The UNIX Programming Environment)
> year = (1983)
> isbn = (020193783)
> publisher = (Prentice Hall Technical Reference)

```latex
\begin{MyCode}[fontsize=\size{-1}]
#include <stdio.h>
int main (int argc, const char *argv[]) {
    printf("Hello, World!");
    return 0;
}
\end{MyCode}
```

以下 LaTeX 命令用于美化并将参考文献插入到此项目中：

如果你将值从 `-1` 更改为 `+1`，代码字体会变大。

- `\bibliography`
- `\addcontentsline{toc}{toc}(Bibliography)`

32 www.linuxux.co.uk
