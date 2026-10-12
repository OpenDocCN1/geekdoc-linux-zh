
# 282 LaTeX

| \symbol{number} | 显示字符集中数字符号。 |

| \underline{text} | 下划线文本。 |

| \dots | 显示省略号（所有模式）。 |

# 节标题

| 命令 | 功能 |

| --- | --- |

| \section{heading-text} | 添加节标题。 |

| \subsection{heading-text} | 添加子节标题。 |

| \subsubsection{heading-text} | 添加三级节标题。 |

| \paragraph{heading-text} | 添加段落标题。 |

| \subparagraph{heading-text} | 添加子段落标题。 |

| \appendix | 添加附录。 |

| \part{part-title} | 添加部分标题。 |

| \chapter{chapter-title} | 添加章节标题。 |

| \tableofcontents | 使用标题创建目录。 |

# 标题

| 命令 | 功能 |

| --- | --- |

| \maketitle | 生成文档标题。 |

| \title{title-text} | 定义标题。 |

| \author{author-name} | 定义作者。 |

| \date | 生成日期。 |

# 数学

| 命令 | 功能 |

| --- | --- |

| \; | 插入宽空格。 |

| \: | 插入中等空格。 |

| \, | 插入窄空格。 |

| \! | 插入负窄空格。 |

| \cdots | 行中间水平省略号。 |

| \ddots | 显示对角省略号。 |

| \vdots | 显示垂直省略号。 |

| \dots | 显示省略号（所有模式）。 |

| \frac{num}{den} | 生成 `num` 除以 `den` 的分数。 |

# 282 LaTeX

| 命令 | 功能 |

| --- | --- |

| \overbrace{text} | 在文本上方生成大括号。 |

| \underbrace{text} | 在文本下方生成大括号。 |

| \overline{text} | 上划线文本。 |

| \underline{text} | 下划线文本（所有模式）。 |

| \sqrt[root]{arg} | 生成根参数 (`arg`) 的平方根。 |

# 环境

| 命令 | 功能 |

| --- | --- |

| \caption{text} | 插入标题。（配合 `figure` 和 `table` 环境使用。） |

| \begin{environment-name} | 开始环境并标记为 `environment-name`。将环境格式应用到后续文本。 |

| \end{environment-name} | 关闭环境。 |

# `tabular` 环境（表格）

| 命令 | 功能 |

| --- | --- |

| \cline{coli-colj} | 绘制跨越 `coli` 到 `colj` 范围列的水平线。 |

| \hline | 绘制跨所有列的水平线。 |

| \multicolumn{cols}{align}{text} | 创建跨指定列数的条目或自定义条目。`align` 是对齐方式（`l`, `r`, 或 `c`）。 |

| \vline | 绘制垂直线。 |

# `picture` 环境（图形）

| 命令 | 功能 |

| --- | --- |

| \put(x coord,y coord){objects} | 执行对象的实际绘制，将对象置于给定坐标处。 |

# 283

| 命令 | 功能 |

| --- | --- |

| \circle*{diameter} | 创建一个直径为 `diameter` 的圆。 |

| \oval(width,height)[position] | 创建一个宽为 `width`、`height` 的椭圆，并在其中放置任何文本。（可以使用 `position` 选项的 `t`, `b`, `l`, `r` 组合将文本放置在不同的象限。） |

| \line(x slope,y slope)(length) | 绘制指定长度和斜率的直线。 |

| \vector(x slope,y slope){length} | 绘制一条指定长度和斜率且末端带有箭头的线。 |

| \makebox(width,height)[position]{text} | 创建一个宽为 `width`、`height` 的框并在其中放置任何文本。（可以使用 `position` 选项的 `t`, `b`, `l`, `r` 组合将文本放置在不同的象限。） |

| \frame(width,height)[position]{objects} | 创建一个宽为 `width`、`height` 的框并将其放置在指定对象周围。可以使用 `position` 选项的 `t`, `b`, `l`, `r` 组合将文本放置在不同的象限。 |

| \dashboard(dash-length){width,height}{text} | 创建一个宽为 `width`、`height` 的虚线框并在其中放置任何文本。可以指定虚线的长度 (`dash-length`)。 |

| \frame{...} | 直接在对象周围放置一个框，中间不留空隙。绘制一个对象的多个副本。 |

# `letter` 环境（信件）

| 命令 | 功能 |

| --- | --- |

| \begin[letter]{name \\ city, state zip} | 创建一个信件环境，开始一封新信。（使用 `\. ` 分隔地址组件。） |

| \address{return-address} | 添加你的回信地址。 |

# 284 LaTeX

| 命令 | 功能 |

| --- | --- |

| \cc(name \\ etc.) | 创建抄送列表。使用 `\. ` 分隔条目。 |

| \closing(text) | 结束信件正文并指定结束语为 "Sincerely."。 |

| \encl{enclosure-list} | 添加附件列表。使用 `\. ` 分隔条目。 |

| \location(address) | 添加组织地址。（仅在使用 `firstpage` 页面样式时显示。） |

| \makelabels(number) | 生成地址标签。（标签在序言中输入。） |

| \name(name) | 添加一个包含在回信地址中的姓名。 |

| \opening(text) | 开始信件正文并指定开篇问候为 "Dear Sir."。 |

| \ps | 添加附言（postscript）。 |

| \signature(name) | 添加用于签名的打印姓名。 |

| \startsbreaks | 允许分页。 |

| \stopbreaks | 禁止分页。 |

| \telephone(number) | 添加电话号码。（仅在使用 `firstpage` 页面样式时显示。） |

# The `Bibliography` 环境（参考文献）

| 命令 | 功能 |

| --- | --- |

| \bibitem[label]{cite_key} | 使用标签创建一个参考文献条目。如果缺少标签，则使用编号的标签。（使用 `cite_key` 创建引用列表。） |

| \cite[text](key_list) | 引用参考文献条目。（`key_list` 是引用键列表。） |

| \nocite{key_list} | 添加 `key_list`。 |

# 定义新命令、环境和字体

| 命令 | 功能 |

| --- | --- |

| \newcommand(cmd)[args][default]{definition} | 定义新命令。 |

| \renewcommand(cmd)[args][default]{definition} | 修改现有命令的定义。 |

| \newenvironment{env_name}[args][default]{begin}{end} | 定义新环境。 |

| \newenvironment{env_name}[args]{begin}{end} | 修改现有环境的定义。 |

| \newtheorem[numbered_like]{caption} | 定义一个处理定理的新型环境。 |

| \newfont(cmd){font_name} | 创建一个引用字体的命令。 |

# 使用包和包含文件

| 命令 | 功能 |

| --- | --- |

| \usepackage{package} | 加载 `LaTeX` 包。 |

| \include{file} | 条件包含文件。 |

| \includeonly{file-list} | 确定哪些文件被包含。 |

| \input{file} | 无条件包含文件。 |

# 符号

- `!=` | 运算符，56, 76
- `~!` | 运算符，76
- `#` | 数字/井号符号，2-3, 71-72, 161
- `#!` | 脚本，3
- `#include` | 预处理命令，
- `$` | 运算符，8, 10-14, 114, 216
