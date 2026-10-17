
### 索引功能说明

使用 `\index{entry@{bf entry}}` 创建索引条目。

执行 `\printindex` 命令。

```latex
% 在 \documentclass 之后，\begin{document} 之前配置

% {1} 用于索引中的斜体页码

% 普通索引条目

% 子条目

% 子条目

% 起始页码

% 结束页码

% 斜体页码

% 排序条目

% 排序条目

% Pi

% 正确排序

% 在 \document 之前
```

## 结论

综上所述，以下示例展示了索引的功能。您可以在书籍末尾的索引中查看结果。

```latex
\index{Index sample}

\index{Index sample!subentry}

\index{Index sample!subentry@{\t}}

\index{Index sample!special@{\verb?\}}

\index{Index sample!italic entry@{\it entry}}

\index{Index sample@italic page number}

\index{index@{\verb?index}}

\index{printindex@{\verb?printindex}}

\index{makeindex@{\verb?makeindex}}

\index{usage@{\verb?makeidx?}}

\index{Index (LaTeX)}

\index{Index}
```

![示例图片](img/dbea4db79a2d1f2183ab7081a3efe6a8_414_0.png)

## 12.4 数学公式

### 公式

在 LaTeX 中表示数学公式时，必须切换到数学模式。这里介绍的所有命令只能在数学模式下执行。

激活数学模式有三种方法：在行内使用两个 `$` 字符包裹公式；在独立段落中使用 `\[` 开始公式并以 `\]` 结束；或在 `equation` 环境中编写公式。在后两种变体中，公式以居中的形式表示在独立段落中；在 `equation` 环境中，它会自动编号。

| 语法 | 说明 |
| :--- | :--- |
| `$formula$` | 行内公式 |
| `\[ formula \]` | 独立公式 |
| `\begin{equation} formula \end{equation}` | 带有自动编号的独立公式 |

请注意，行内公式与独立段落中的公式略有不同：在 `$formula$` 中，LaTeX 使用了较小的字号，并尝试设置公式以尽可能少占用空间。特别是，上标和下标在某些数学符号（极限、积分、求和）中的位置不同。

在接下来的行中，你将看到同一个公式 $\int_{i=1}^{n} x^i dx$ 出现了三次：一次在正文中，被 `$` 包围的公式看起来像这样：$\int_{i=1}^{n} x^i dx$。被 `\[ \dots \]` 包围或在 `\begin{equation}` 和 `\end{equation}` 之间，会产生以下结果：

```latex
$$\int_{i=1}^{n} x^i dx$$
```

如果你希望单独的公式不居中而是左对齐，可以在 LaTeX 文档的开头使用 `\usepackage{flegno}` 指令。随后，你可以使用 `\mathindent2cm` 指定相对于左页边线的缩进（此处为 2 cm）。或者，你也可以使用 `\package{equation}` 来确保公式环境的 LaTeX 数字是左对齐而不是居中的。

在公式内部，文本通常设置为斜体。然而，对于变量，应该用正体字符表示。为了实现这一点，LaTeX 提供了它自己的命令，如 `\sin`。文本 $\sin(x^2)$ 会生成 $\sin(x^2)$。LaTeX 有以下命令用于：

```latex
\arccos, \arcsin, \arctan, \arg, \cos, \cosh, \cot, \coth, \csc, \deg

\det, \dim, \exp, \gcd, \hom, \inf, \ker, \lim, \liminf, \limsup

\ln, \log, \max, \min, \sup, \sec, \sin, \sinh, \tan, \tanh
```

如果在公式中使用了上述列表中没有的普通文本或函数名，必须用 `{\it varname}` 指定文本，`{\bf X}` 也允许输出较长的变量或突出显示的文本。

在某些情况下，LaTeX 使用间距非常吝啬。在公式 `$sin(xy)$` `$(\sin(x\ y))$` 中，你几乎无法识别出 `$x$` 和 `$y$` 是两个相乘的独立变量。为了增加间距，请使用三个命令：`\,`（小距离）、`\:`（平均距离）、`\;`（宽距离）：`$\sin(x \: y)$` 将变成 `$sin(xy)$`。

### 公式构建的重要命令

以下命令用于构建分式、根号、积分、和等。这些命令可以任意嵌入以获得分式中的根或类似的组合。LaTeX 会自动处理合适的大小以及其他格式细节。请记住，在指定上标或下标时，将相关表达式括在花括号中——否则 `^` 和 `_` 只作用于第一个字符。

```latex
$a^{\{b\}} \quad a^b \quad \sum_{\{a\}}^{b} c$

$a_{\{b\}} \quad a_b \quad b$

$\frac{a}{\{b\}} \quad \frac{a}{b} \quad \prod_{\{a\}}^{{b}} c \quad \Pi_c$

$\sqrt{a} \quad \sqrt{a} \quad \{a \choose b\} \quad \left(\frac{a}{b}\right)$

$\sqrt[n]{{a}} \quad \sqrt{{a}} \quad \overline{abc} \quad abc$

$\int_{\{a\}}^{{b}} c \quad \frac{b}{c} \quad \underline{abc} \quad abc$

$\int_{\{a\}}^{{b}} c \quad \frac{b}{a} \quad \overbrace{abc}^{\{d}} \quad d$

\quad \underbrace{abc}_{\{d\}} \quad d$
```

如果你对 LaTeX 自动选择的字体大小不满意，可以使用以下四个命令影响它们：

- `\displaystyle` 正常
- `\scriptstyle` 稍小（在 `$` 公式中使用的字体大小）
- `\scriptstyle` 更小（一阶下标和指数）
- `\scriptsstyle` 极小（二阶下标和指数）

以下公式说明了上述列出的命令之间的相互作用。公式还包含了一些将在后续章节中描述的命令。

```latex
$\frac{\frac{a+1}{\{b-1\}}}{\frac{c+1}{\{d-1\}}}\n\quad \mbox{\text{and}}\quad

\displaystyle\frac{a+1}{\{b-1}}}{\displaystyle\frac{c+1}{\{d-1}}} \quad
```

```latex
$$\frac{a+1}{b-1} \quad \text{and} \quad \frac{c+1}{d-1}$$
```

```latex
\int_C f(z), \ dz = \int_0^{2\pi} f(z) \frac{dz(t)}{dt} \quad with \quad z(t)=z+r(\cos(t) + I \sin(t))
```

```latex
\left[ {\begin{array}{c}

\displaystyle \frac{\{\partial\}}{\{\partial\}\}},

\rm f}(\{u,\v\}, \{z\}),{a\}), \sqrt{\rm sin}(\{v\}^{\{2\}} +\rm sin}(\{u,\v\}^{\{2\}}

\end{array} \right]
```
