
$\quad \underbrace{abc\}_{\{d\}} \quad d$

如果你对 LaTeX 自动选择的字体大小不满意，可以使用以下四个命令影响它们：

- `\displaystyle` 正常
- `\scriptstyle` 稍小（在 $ 公式中使用的字体大小）
- `\scriptstyle` 更小（一阶下标和指数）
- `\scriptsstyle` 极小（二阶下标和指数）

以下公式说明了上述列出的命令之间的相互作用。公式还包含了一些将在后续章节中描述的命令。

```
$\frac{\frac{a+1}{\{b-1\}}}{\frac{c+1}{\{d-1\}}}\n\quad \mbox{\text{and}}\quad
\displaystyle\frac{a+1}{\{b-1}}}{\displaystyle\frac{c+1}{\{d-1}}} \quad
```

```
$$\frac{a+1}{b-1} \quad \text{and} \quad \frac{c+1}{d-1}$$
```

```
\int_C f(z), \ dz = \int_0^{2\pi} f(z) \frac{dz(t)}{dt} \quad with \quad z(t)=z+r(\cos(t) + I \sin(t))
```

```
\left[ {\begin{array}{c}
\displaystyle \frac{\{\partial\}}{\{\partial\}\}},
\rm f}(\{u,\v\}, \{z\}),{a\}), \sqrt{\rm sin}(\{v\}^{\{2\}} +\rm sin}(\{u,\v\}^{\{2\}}
\end{array} \right]
```

| $\frac{\partial}{\partial u}(u,v)$ | $\sqrt{\sin(v)^2+\sinh(u)^2}$ |
| :--- | :--- |
| $\frac{\partial}{\partial v}(u,v)$ | $\sqrt{\sin(v)^2+\sinh(u)^2}$ |

## 圆括号和中括号

圆括号和中括号主要通过 `( )` 直接生成。在公式 `$sin(xy)$` 或 `$(\sin(x\ y))$` 中，你几乎无法识别出 `$x$` 和 `$y$` 是两个相互相乘的独立变量。为了增加间距，请使用三个命令：`\,`（小距离）、`\:`（平均距离）、`\;`（宽距离）：`$\sin(x \: y)$` 将变成 `$sin(xy)$`。

`...` `\left` 和 `\right`。

## 矩阵

圆括号和中括号通常通过 `array` 环境生成，例如：

```
\begin{array}
text1 & text2 & text3
\end{array}
```

## 希腊字母和花体字母

希腊字母也通过 LaTeX 命令表示。命令名称对应字母名称，因此，例如 `\alpha` 代表小写字母，`\Delta` 代表大写字母。可用命令如下：

| $\alpha \alpha$ | $\kappa \kappa$ | $\Psi \Psi$ | $\Upsilon \Upsilon$ |
| :--- | :--- | :--- | :--- |
| $\beta \beta$ | $\lambda \lambda$ | $\omega \omega$ | $\varepsilon \varepsilon$ |
| $\chi \chi$ | $\Lambda \Lambda$ | $\Omega \Omega$ | $\varpi \phi$ |
| $\delta \delta$ | $\mu \mu$ | $\rho \rho$ | $\varpi$ |
| $\Delta \Delta$ | $\nu \nu$ | $\sigma \sigma$ | $\varro Ꮙ$ |
| $\epsilon \epsilon$ | $\phi \phi$ | $\Sigma \Sigma$ | $\varigma \gamma$ |
| $\eta \eta$ | $\Phi \Phi$ | $\tau \tau$ | $\vartheta ϑ$ |
| $\gamma \gamma$ | $\pi \pi$ | $\theta \theta$ | $\xi \xi$ |
| $\Gamma \Gamma$ | $\Pi \Pi$ | $\Theta \Theta$ | $\Xi \Xi$ |

花体字母仅大写形式可用。为了表示这些字母，必须通过 `\cal` 更改字体，例如，`{\cal A} \cup {\cal B}` 代表 `A \cup B`。

## 文本命令与间距

为了实现这一点，LaTeX 提供了它自己的命令，如 `\sin`。`$\sin(x^2)$` 是由文本 `$\sin(x^2)$` 生成的。LaTeX 有以下命令用于输出：

```
$\arccos, \arcsin, \arctan, \arg, \cos, \cosh, \cot, \coth, \csc, \dec$
\det, \dim, \exp, \gcd, \hom, \inf, \ker, \lim, \liminf, \lninsup$
\ln, \log, \max, \min, \prx, \sec, \sin, \sinh, \tan, \tanh$
```

如果在公式中使用普通文本或上述列表中没有的函数名，必须用 `{\it varname}` 指定文本，`{\bf X}` 也允许输出较长的变量或突出显示的文本。

在某些情况下，LaTeX 使用间距非常吝啬。在公式 `$sin(xy)$` 或 `$(\sin(x\ y))$` 中，你几乎无法识别出 `$x$` 和 `$y$` 是两个相互相乘的独立变量。为了增加间距，请使用三个命令：`\,`（小距离）、`\:`（平均距离）、`\;`（宽距离）：`$\sin(x \: y)$` 将变成 `$sin(xy)$`。

## 公式环境与对齐

在接下来的行中，你将看到同一个公式 `$\int_{i=1}^{n} x^i dx$` 出现了三次：一次在正文中，被 `$ $` 包围的公式看起来像这样：`$\int_{i=1}^{n} x^i dx$`。被 `\[ \dots \]` 包围或在 `\begin{equation}` 和 `\end{equation}` 之间，会产生以下结果：

```
$$\int_{i=1}^{n} x^i dx$$
$$\int_{i=1}^{n} x^i dx$$
```

如果你希望单独的公式不居中而是左对齐，可以在 LaTeX 文档的开头使用 `\usepackage{flegno}` 指令。随后，你可以使用 `\mathindent2cm` 指定相对于左页边线的缩进（此处为 2 cm）。或者，你也可以使用 `\package{equation}` 来确保公式环境的 LaTeX 数字是左对齐而不是居中的。

在公式内部，文本通常设置为斜体。然而，对于变量，应该用正体字符表示。为了实现这一点，LaTeX 提供了它自己的命令，如 `\sin`。`$\sin(x^2)$` 是由文本 `$\sin(x^2)$` 生成的。LaTeX 有以下命令用于输出：

```
$\arccos, \arcsin, \arctan, \arg, \cos, \cosh, \cot, \coth, \csc, \dec$
\det, \dim, \exp, \gcd, \hom, \inf, \ker, \lim, \liminf, \lninsup$
\ln, \log, \max, \min, \prx, \sec, \sin, \sinh, \tan, \tanh$
```
