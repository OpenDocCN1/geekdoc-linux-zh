
| `\partial` | `\partial` | `\in` | `\in` |

| `a\prime` | `a'prime` | `\approx` | `\approx` |

| `\not` | `\not` | `\times` | `\times` |

| `\nabla` | `\nabla` | `\Delta` | `\Delta` |

| `\dots` | `\dots` | `\vdots` | `:` |

| `\sum` | `\sum` | `\prod` | `\prod` |

| `\cup` | `\cup` | `\cap` | `\cap` |

| `\int` | `\int` | `\oint` | `\oint` |

| `\forall` | `\forall` | `\exists` | `\exists` |

| `\lfloor x \rfloor` | `[x]` | `\lceil x \rceil` | `[x]` |

### 分数与商

命令

`\frac{num}{denom}`

通过在给定的分子和分母之间绘制水平分割线来格式化分数。表 14.6 显示了涉及分数和乘积的构造。

### 向量与矩阵

向量符号通常在数学模式下设为粗体（使用 `\bf`），或通过 `\vec` 命令设置箭头重音（`\vec{v}`）。数学模式下的其他重音包括 `\hat{v}(\hat{v})`, `\bar{v}(\bar{v})`, `\dot{v}(\dot{v})`, `\tilde{v}(\tilde{v})`。

矩阵、行列式和向量也可以格式化为带有各种闭合括号（`(), [], {}`）的二维数组。`array` 环境与 `tabular` 环境非常相似。表 14.7 显示了不同的向量和矩阵。

## 第 14 章

## 文档准备工作

表 14.6 乘积与商

| 输入 | 输出输出 |
|--- |--- |
| `$\cos(x/3)+\frac\{a\}\{b\}}$` | `$\cos(x/3) + \frac{a}{b}$` |
| `\frac\{1\}\{1+1/x\}$` | `$1 + \frac{1}{1/x}$` |
| `\left\frac\{a\}\{b\}\right)^c$` | `$\frac{a^c}{b}$` |
| `\rm{width} \times \text{length}(2)=\rm{area}$` | `$\text{width} \times \text{length} = \text{area}$` |
| `\prod_{i=1}^n x_i$` | `$\prod_{i=1}^n x_i$` |
| `$x \cdot y$` | `$x \cdot y$` |
| `\sum_{i=0}^{n}\left\frac\{1\}\{2\}\right)^i$` | `$\sum_{i=0}^n(\frac{1}{2})^i$` |

表 14.7 向量与矩阵

| 输入 | 输出输出 |
|--- |--- |
| `$\nabla p \times \vec{r}$` | `$\nabla p \times \vec{r}$` |
| `\left[\begin{array}{cc}a\&b\&d\end{array}\right]$` | `$\begin{bmatrix}a & b & d \end{bmatrix}$` |
| `-10\left\begin{array}{cc}x\&y\&w\end{array}\right|$` | `$-10\begin{bmatrix}x & y & w \end{bmatrix}$` |
| `$A^T B = C^{-1}$` | `$A^T B = C^{-1}$` |
| `\left(\begin{array}{cc}c\&n/2\end{array}\right)$` | `$\begin{pmatrix}c & n/2 \end{pmatrix}$` |

### 导数与积分

表 14.8 显示了一些涉及导数和积分的公式。在表格中使用 `\left \right` 定符来平衡被积分函数，其中包含了 `\,`，这会添加细微的空间使公式看起来更好看。用于调整的可用小空间有：

- 窄空格 `thin space`
- 中等空格 `medium space`
- 宽空格 `thick space`
- 负窄空格 `negative thin space`

表 14.8 导数与积分

| 输入 | 输出输出 |
|---|---|
| `$\dot{x} = \ddot{y} + \frac{dx}{dt}$` | `$\dot{x} = \ddot{y} + \frac{dx}{dt}$` |
| `$f'(x)+\frac{\partial y}{\partial x}$` | `$f'(x) + \frac{\partial y}{\partial x}$` |
| `\left.\frac{\partial y}{\partial x}\right|_{x=a}$` | `$\frac{\partial y}{\partial x}_{x=\alpha}$` |
| `\lim_{x\rightarrow\infty}\int_{0} f(y)dy$` | `$\lim_{x\to\infty} f(y)dy$` |

表格还显示了与正文混合的公式。极限以及因此通过 `[ ]` 显示的内容是居中的，并以占据垂直空间的形式渲染。例如，表格中的相同的积分变为：

```
$$\lim_{x\to\infty} \int_{0}^{x} f(y)dy$$
```

### 显示公式

要将表 14.8 中的相同积分格式化为带编号公式，你可以使用 `equation` 环境：

```
\begin{equation}
\lim_{x\rightarrow\infty}\int_{0}^{x} f(y)dy \label{eq:a}
\end{equation}
```

结果显示为：

```
$$\lim_{x\to\infty} \int_{0}^{x} f(y)dy$$ (1.1)
```

标签是可选的，并允许通过 `\ref` 进行交叉引用。`eqarray` 环境用于包含多行的公式，其方式与 `tabular` 环境相同。例如：

```
\begin{eqnarray}
3x + 5y -6z &= 9
2x + 5y -9z &= 23
x - y +17z &= 94
\end{eqnarray}
```

不需要编号的行，可以在结束前添加 `\number` 命令。

## 14.15 原模式

有时必须包含无需格式化的材料。在 LaTeX 中可以使用 `verbatim` 环境来实现。只需将材料封装在 `\begin{verbatim}` 和 `\end{verbatim}` 之间。原模式的内容以 `\tt` 字体显示。

`verbatim` 环境产生独立的段落，并可以接受多行。行内原模式使用 `\verb` 命令。例如 `\verb{...}` 设置原模式内部的字符。定界符不需要是 `||`，可以是任何匹配的字符。因此代码 `\verb{Z}` 生成 `"Z"`。所有的原模式内容都被视为原始文本，不识别命令。

在 LaTeX 中，支持 `alltt` 环境。这与 `verbatim` 环境类似，只是可以用通常的方法引入其他命令和环境。

## 14.16 定义新命令

发明自己的命令作为常用文本、命令或构造组合的简写是非常方便的。使用 `\newcommand` 或 `\environment` 命令定义你的命令或环境。此类定义通常放在导言区。

例如，一些新命令：

```
\newcommand{oop}{Object-oriented Programming}
\newcommand{sac}{Symbolic and Algebraic Computation}
\newcommand{ww}{World-Wide Web}
\newcommand{bi}{\begin{itemize}}
\newcommand{el}{\end{itemize}}
\newcommand{spi}[3]{$1{#2}^{#3}}
```

前三个新命令使用了 `\oop`, `\sac` 和 `\ww`，可以让定义接下来的两个项目列表变得简单得多。最后一个新命令 `\spi` 定义了三个参数，代码 `\sp{\int}{}{0}\{1\}` 生成 `$f_0^1$`。

## 14.17 定义新环境

该命令

```
\newenvironment{name}{top}{bottom}
```

定义了一个新的环境名称，该环境由代表 *top* 的命令开始，并以代表 *bottom* 的命令结束。在环境定义中，参数的提供方式与命令定义中的提供方式相同。同样，`\newenvironment` 结构的各个部分之间不能有换行符，尽管每个部分的 `{}` 内部可以有换行符。例如，新环境 `cfg`：

```latex
\newcommand{capt{}
\newenvironment{cfg}[2]%
\begin{figure}[htb]
\begin{center}
\newcommand{capt}{#1\label{#2}}
}
{caption{capt}}
\end{center}
\end{figure}
```

这使得格式化一个带有标题并使用 `%` 消除行尾换行符的居中图片变得非常方便。`\capt` 命令对这很有帮助，因为你只能在 *top* 部分使用参数（如 `#1` 等）。通过这个新环境，我们可以使用

```latex
\begin{cfg}{文档准备概览}{fig:dpo}
```

...

```latex
\end{cfg}
```

来设置一个图片。

## 14.18 预览与打印

如前所述，外壳级命令

```
latex name.tex
```

会生成可打印的文件 `name.dvi`。在准备新文档时，在打印纸质副本之前先预览文件是一个良好的习惯。命令

```
xdvi name.dvi
```

使用 X Window 系统工具 `xdvi` 在屏幕上预览给定的文件。它还允许你在打印时打印整个文档或选定页面的纸质副本。此外，某些 `latex` 命令会自动为你调用预览器。

## 14.19 包含 PostScript 图片

要将 `.dvi` 文件直接发送到打印机

```
lpr -d dvi.name
```

其中 `-d` 选项告诉 `lpr` 打印 `.dvi` 文件。

如果你有一个 PostScript 打印机，可以在将其发送到 PostScript 打印机之前，将 `.dvi` 文件转换为 PostScript。命令*

```
dips -o name.ps name
```

将 `.dvi` 文件翻译为 `.ps` 文件。`-E` 选项导致 `dvips` 建立一个封装的 PostScript 文件 `(.eps)`，适合封装在其他文档中。`.eps` 文件通常不包含位置命令，并提供一个紧凑的边界（bounding box），任何包含文档都可以用它留出恰好的空间。要打印 `.ps` 文件

```
lpr -v name.ps
```

可以使用 `ghostview` 命令预览 PostScript 文件。（该程序以及许多其他与文档准备相关的程序可以从自由软件基金获得。）

此外，命令 `dvselect` 从 `.dvi` 文件中提取选定的页面。例如，命令

```
dvselect pages file1.dvi > file2.dvi
```

从 `file1.dvi` 中提取所需的页面并将其放入新文件 `file2.dvi` 中。页面可以指定为一系列由逗号分隔的页码和页码。示例范围包括 `5-43`、`-30`（从开始到第 30 页）以及 `76-`（从第 76 页到末尾）。

一图胜于千言，在文档中包含图片、图表或截图是非常容易。正如第 14.13 节讨论的，`picture` 环境支持带有线条、方框和箭头的绘图。为了创建更多图表，X Window 系统工具 `xfig` 允许对几乎任何线条和形状进行交互式绘制。你还可以在图中插入文本。这些将成为图片中的图形组件或对象。程序还帮助你移动、复制和删除对象，并对图进行更改。完成的图可以保存到文件 `(.fig)` 中，以便将来加载和编辑。

你也可以使用 `xfig` 将图片导出为存储在封装 PostScript `(.eps)` 格式的文件，准备好包含在 LaTeX 文件中。导出时，你可以选择一个放大倍数（80%），通常

* 可通过 `labrea.stanford.edu` 的 `ftp/pub` 公共 FTP 获取。

为了包含在典型的论文中，导出时选择纵向布局。

假设文件为 `mypic.eps`，那么以下代码

```latex
\begin{figure}[hbt]
\begin{centering}
\center{\psfig{figure=mypic.eps}}
\vspace*{3mm}
\end{centering}
\caption{我伟大的 PostScript 图片}
\label{fig:mypic}
\end{figure}
```

可以将文件 `mypic.eps` 包含到 LaTeX 文档中。`psfig` 命令由 TeX 宏包 `psfig.tex` 提供，该包在你的系统中应该是可用的。要使用上述代码，必须先在导言区放入行

```latex
\input{psfig}
```

以加载 `psfig.tex` 包。`/psfig` 命令还可以提供宽度和高度参数，以使包含的内容适应预定义的区域。例如：

```latex
\psfig{figure=mypic.eps,width=5.2in,height=3.5in}
```

对于窗口转储，Window 系统提供的提供的命令

```
xwd-frame -out .my.dump
```

会生成一个 `.dump` 文件，包含鼠标选定窗口的位图图像（以及窗口边框）。`.dump` 文件可以通过命令转换为 `.eps`

```
xpr-device -portrait -compact .my.dump |
sed /showpage/ > my.eps
```

此 `eps` 文件可以使用 `ghostview` 命令预览。（这以及许多其他与文档准备相关的程序是可用的。）

此外，命令 `dvselect` 可以从 `.dvi` 文件中提取选定的页面。

`/psfig` 命令也可以提供一个宽度和高度参数，以使包含的内容适应预定义的区域。例如：

```latex
\psfig{figure=mypic.eps,width=5.2in,height=3.5in}
```

对于窗口转储，Window 系统提供的命令

```
xwd-frame -out .my.dump
```

会生成一个 `.dump` 文件，包含鼠标选定窗口的位图图像（以及窗口边框）。`.dump` 文件可以通过命令转换为 `.eps`

```
xpr-device -portrait -compact .my.dump |
sed /showpage/ > my.eps
```

`/psfig` 命令也可以提供一个宽度和高度参数，以使包含的内容适应预定义的区域。例如：

```latex
\psfig{figure=mypic.eps,width=5.2in,height=3.5in}
```

`/psfig` 命令也可以提供一个宽度和高度参数，以使包含的内容适应预定义的区域。例如：

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。`/psfig` 命令也可以提供一个宽度和高度参数，以使包含的内容适应预定义的区域。例如：

```latex
\psfig{figure=mypic.eps,width=5.2in,height=3.5in}
```

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。

`/eps` 文件通常是封装的，可以包含在 LaTeX 文档中。

`/psfig` 命令也可以提供一个宽度和高度参数。
