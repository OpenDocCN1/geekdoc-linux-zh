
$\mathbb{R}$ 上最重要的波尔测度是那些在有界集上有限的测度。荷兰数学家 T. J. Stieltjes (1856–1894) 他的积分（见第 1.19 节）在 Radon (1887–1956) 测度理论的发展中起了关键作用，在世纪的第二个十年被引入。由于相同的原因，它们被称为 Radon 测度。与第 3.8 节讨论的某些 Hausdorff 测度相反，它们在每个开集上是无限的。Lebesgue-Stieltjes 测度是 $\mathbb{R}$ 上的波尔测度，可以用于分布。一些例子可以在例 2.10 和习题 2.14、2.8 中找到。我们现在可以使用已经开发的工具来严格且符合直觉地得到这样的模型。在这里考虑一维情况，然后在第 3.7 节概述 $\mathbb{R}^n$ 的构造。

### 3.5. Stieltjes 测度的构造

假设对于每个 $x \in \mathbb{R}$，我们知道 $(0,x]$ 型或 $(x,0]$ 型的质量，且这些质量是有限的。设

$$f(x) = \begin{cases} \text{mass}(0,x], & \text{如果 } x > 0; 0, & \text{如果 } x = 0; -\text{mass}(x,0], & \text{如果 } x < 0. \end{cases}$$

那么 $f$ 是 $\mathbb{R}$ 上的递增函数。虽然 $f$ 不需要连续，但我们要求 $f$ 连续。由于单调函数在每个点都有左右极限，这以特定方式固定了 $f$ 在不连续点的值。我们现在进行与习题 2.4 平行的操作。我们处理的是 $\mathbb{R}$ 中的区间而非 $\mathbb{R}^2$。设 $\mathcal{T}$ 由 $(a,b]$ 型的半开区间、空集以及 $(-\infty, b]$ 和 $(a, \infty)$ 型的区间组成。对于预测度 $\tau: \mathcal{T} \to [0, \infty]$，我们将

$$\tau(T) = \begin{cases} 0, & \text{如果 } T = \emptyset; f(b) - f(a), & \text{如果 } T = (a,b]; \lim_{x\to-\infty} f(x), & \text{如果 } T = (-\infty,b]; \lim_{x\to\infty} f(x), & \text{如果 } T = (a,\infty). \end{cases}$$

这些极限存在（有限或无限），因为 $f$ 是递增的。继续该程序，设 $\mathcal{T}_1$ 是 $\mathcal{T}$ 生成的代数。一眼看出 $\mathcal{T}_1$ 由 $\mathcal{T}$ 的元素的有限并组成。我们希望将预测度 $\tau$ 扩展为加性函数 $\tau_1: \mathcal{T}_1 \to [0, \infty]$。对于 $T \in \mathcal{T}_1$，写下

$$\mathcal{T}_1 = T_1 \cup T_2 \cup \dots \cup T_n.$$

对于每个 $i = 1, \dots, n，$T_i \in \mathcal{T}$且当 $i \neq j$ 时 $T_i \cap T_j = \emptyset$。我们定义

$$\tau_1(T) = \tau(T_1) + \tau(T_2) + \dots + \tau(T_n).$$

引号表示我们必须验证 (12) 是明确的。（回想我们在 3.2 节中的正方形例子。）

## 3.16 *集函数 $\tau_1$ 在 $\mathcal{T}_1$ 上良定义。*

证明。考虑第一种情况 $T \in \mathcal{T}$。设

$$T = (a,b] = \sum_{i=1}^n (a_i, b_i].$$

其中 $a_1 = a, b_n = b$，且对于所有 $i = 1, \dots, n-1, a_{i+1} = b_i$。因此

$$\tau((a,b]) = f(b) - f(a) = \sum_{i=1}^n (f(b_i) - f(a_i)) = \sum_{i=1}^n \tau((a_i, b_i]).$$

类似的证明表明，如果无界区间 $T \in \mathcal{T}$ 被分解为有限个 $\mathcal{T}$ 中的集，则 (12) 成立。最后，任何 $T \in \mathcal{T}_1$ 都是 $\mathcal{T}$ 成员的有限并。这些成员在必要时可以适当组合成一个不交集

$$\{(a_i, b_i]\} = \bigcup_{j=1}^{\infty} T_j. \quad \text{其中 } b_i < a_{i+1}.$$

这里可能 $a_1 = -\infty$。假设 $T$ 被分解为 $T$ 的不交并，例如 $T = \bigcup_{j=1}^{\infty} T_j$。设

$$A_i = \{T_j : T_j \in (a_i, b_i]\}.$$

那么，集合 $\langle a_i, b_i \rangle$ (13)，12) 中的和不依赖于 $T$ 的表示。

由于定理 2.40，我们现在知道方法 I 导致测空间，其中 $\mathcal{T}$ 的每个成员都是可测的。这意味着每个波尔集都是可测的。为了证明这一点，注意开区间是半区间的可数并，

$$\langle a, b \rangle = \bigcup_{n=1}^{\infty} [a_n, b_n],$$

其中 $a < b_1 < b_2 < \dots < b$ 且 $\lim_{n \to \infty} b_n = b$。根据定理 3.7，$\mu^*$ 是外测度。从定理 2.36 看到每个集 $A \subset \mathbb{R}$ 都有波尔集作为可测覆盖。现在从定理 3.15 很容易地推出 $T$ 可以取为 $G_{\delta}$ 型（留作习题 35-1）。我们还不知道的是 $T_1$ 的测度，甚至是 $T$，我们得到了正确的测度；即 $\mu^*(\langle a, b \rangle) = \tau(a, b)$。为了得到这一点，只需证明 $\tau_1$ 在 $\mathcal{T}_1$ 上是 $\sigma$-加性的。我们可以调用定理 2.42。

## 3.17 *集函数 $\tau_1$ 在 $\mathcal{T}_1$ 上是 $\sigma$-加性的。*

证明。为了证明 $\tau_1$ 在 $\mathcal{T}_1$ 上是 $\sigma$-加性的，我们必须证明，如果 $\{T_n\}$ 是 $\mathcal{T}_1$ 中的一个不交集序列且其并 $T$ 也在 $\mathcal{T}_1$ 中，那么

$$\tau_1(T) = \sum_{n=1}^{\infty} \tau_1(T_n).$$

只需考虑 $T$ 是单个区间 $(a, b)$ 的情况。对于有限加性，我们的工作被以下事实简化了

### 3.5. 勒贝格-Stieltjes 度的构造

如果 $(a, b] = \bigcup_{i=1}^\infty (a_i, b_i]$，且集合 $\{(a_i, b_i]\}$ 两两不相交，

```
$f(b) - f(a) = \sum_{i=1}^n f(b_i) - f(a_i),$
```

因为这些区间必须形成 $(a, b]$ 的划分。当处理形式为 $(a, b] = \bigcup_{i=1}^\infty (a_i, b_i]$ 且集合 $\{(a_i, b_i]\}$ 两两不相交的无限分解时，这种和的消去法并不总是可能的。例如，考虑

```
$[-1, 1] = [-1, 0] \cup \bigcup_{n=1}^\infty (n+1)^{-1}, n^{-1}].
```

在这里，0 是集合中某个区间的右端点，但不是任何其他区间的左端点。仍然成立

但这需要 0 处的右极限。通常，如果 $t \in \mathbb{N}$，$b_t$ 是集合 $(a_j)_{j=1}^\infty$ 的极限点，则对于任何 $j \in \mathbb{N}$， $b_t \neq a_j$。我们无法获得在具有消去和时受益的这种抵消。此外，可能有无穷多个此类点需要处理。注意，只有右端点具有这种特征。

让我们详细观察一下这种情况。令 $A = \{a_i\}$，$B = \{b_i\}$。那么 $A \cup B$ 不一定包含在 $A$ 中。一个简单的图可以说明 $B \cup A$ 是无限的。

```
$[a, b] = \bigcup_k (a_k, b_k) \cup B \cup \{a\}$
```

由此得出 $A \cup B$ 是一个可数闭集。令 $J_0 = [f(a), f(b)]$，对于 $k \in \mathbb{N}$，$J_k = [f(a_k), f(b_k)]$。由于 $f$ 是单调不减的，$\bigcup_{k=1}^\infty J_k \subset J_0$，且区间 $J_k$ 没有公共的内点。因为 $f$ 在 $x=a$ 处右连续

```
$J_0 \subset \bigcup_{k=1}^\infty J_k \cup f(b) \cup \{f(a)\}$
```

$B$ 是可数的，所以 $f(B)$ 也是可数的，因此 0，

## 第 3 章. 规外测度

其中，通常 $\lambda$ 表示勒贝格测度。由此得出

```
$$\sum_{k=1}^{\infty} (f(b_k) - f(a)) = \lambda \left( \bigcup_{k=1}^{\infty} J_k \right) \leq \lambda(J_0)$$
$$\leq \lambda \left( \bigcup_{k=1}^{\infty} J_k \cup f(B) \cup \{f(a)\} \right)$$
$$\sum_{k=1}^{\infty} \lambda(J_k) = \sum_{k=1}^{\infty} (f(b_k) - f(a_k)).$$
```

因此 $f(b) - f(a) = \lambda(J_0) = \sum_{k=1}^{\infty} (f(b_k) - f(a_k))$，使得

```
$$\tau_i((a,b)) = \sum_{k=1}^{\infty} \tau_i([a_k, b_k])$$
```

符合要求。我们现在完成了这个程序。我们最终通过应用方法 I 得出结论，我们将赋予外测度 $\mu_f'$ 然后赋予测度空间 $(X, \mathcal{M}_f, \mu_f)$，使得

```
$$\mu_f((a,b)) = f(b) - f(a).$$
```

我们将 $\mu_f$ 称为分布函数为 $f$ 的勒贝格-Stieltjes 测度。我们也会使用如 $\mu_f$ 是“由 $f$ 导出”或“与 $f$ 相关”等短语。对于任何 $c \in \mathbb{R}$，函数 $f+c$ 也可以作为 $\mu_f$ 的分布函数。在处理有限勒贝格-Stieltjes 测度时，选择 $f$ 使得 $\lim_{x\to-\infty} f(x) = 0$ 通常很方便。此外，当测度位于某个区间 $I_f$ 时，仅在 $I_f$ 上指定 $f$ 可能很方便（例如我们在练习 3.5.5 中所做的那）。技术上，这扩展到整个 $\mathbb{R}$，使得 $\mu_f'(\mathbb{R}) = 0$。（这种扩展对于...

**例 3.18** *概率空间*是一个总测度为 1 的测度空间。如果 $X = \mathbb{R}$，可以选择分布函数使得 $\lim_{x\to-\infty} f(x) = 0$，并满足 $\lim_{x\to\infty} f(x) = 1$。对于可测集 $A$，$\mu_f(A)$ 代表随机变量落在 $A$ 中的概率。作为一个具体的例子，如果 $\phi$ 是标准正态密度函数（钟形曲线），

```
$$\phi(x) = \frac{1}{\sqrt{2\pi}} e^{-\frac{x^2}{2}} \quad (-\infty < x < \infty),$$
```

那么 $\int_{-\infty}^{\infty} \phi(x) dx = 1$，可以取 $f(x) = \int_{-\infty}^{x} \phi(t) dt$ 作为相关的分布函数。

### 3.5. 勒贝格-Stieltjes 度的构造

在概率背景下，Borel 集合 $A$ 的“质量”被解释为“事件” $A$ 发生的概率。因此，标准正态变量 $Z$ 满足 $a < Z \le b$ 的概率为

$Pr(a < Z \le b) = f(b) - f(a) = \int_{a}^{b} \phi(x) \ dx.$。

更一般地，对于任何 Borel 集合 $A$，我们有

$Pr(Z \in A) = \mu_{f}(A) = \int_{A} \phi(x) \ dx,$，

其中积分必须在勒贝格意义上解释。（我们不得不等到第 5 章）。

### 习题

- 3.5.1 证明对于任何测度 $A$，都有类型为 $\mathcal{G}$ 的可测覆盖和类型为 $\mathcal{F}$ 的可测核。
- 3.5.2 使用定理 3.8 和 3.9 给出另一个勒贝格-Stieltjes 测度是规规的。
- 3.5.3 令 $X = \mathbb{R}$ 且 $f(x) = \begin{cases} 0, & \text{若 } x < 0 \\ 1, & \text{若 } 0 \le x < 1 \\ 2, & \text{若 } x \ge 1 \end{cases}$。证明 $\mu_f$ 是有界的。
- 3.5.4 令 $X = \mathbb{R}$ 且 $\mu(A) = \begin{cases} 0, & \text{若 } A = \emptyset \\ \infty, & \text{若 } A \neq \emptyset \end{cases}$。构造分布函数 $f$ 使得 $\mu = \mu_f$。
- 3.5.5 令 $f$ 是康托集且 $\mu_f$ 是勒贝格测度。计算 $\mu_f(K)$。
- 3.5.6 令 $\mu_f$ 是勒贝格-Stieltjes 测度。证明 $\mu_f((a,b)) = f(b) - f(a)$。
- 3.5.7 勒贝格-Stieltjes 术语常用于应用到有限变分函数。这指的是什么？

## 第 3 章. 规外测度

令 $\mu_f$ 为相关的勒贝格-Stieltjes 测度。计算 $\mu$ 的 Jordan 变分。

**3.5.8** 令 $(X, \mathcal{M}, \mu)$ 为一个测度空间。集合 $A$ 被称为原子，如果 $\mu(A) > 0$ 且对于所有可测的 $B \subset A$，$\mu(B) = 0$。（见 2.7。）

- (a) 给 $\mathbb{R}$ 的例子使得 $[0,1]$ 是原子。
- (b) 令 $(\mathbb{R}, \mu_f)$ 为勒贝格-Stieltjes 测度。证明，$A$ 在此空间包含一个相同测度的点。即存在 $a \in A$ 使得 $\mu_f(\{a\}) = \mu(A)$。人们也使用“点质量”来描述原子 $\mu_f$。
- (c) 如果测度 $\mu$ 是*非原子的*，如果没有原子。证明勒贝格-Stieltjes 测度是非原子的当且仅当其函数连续时。

### 3.6 勒贝格-Stieltjes 测度的性质

我们研究一维勒贝格-Stieltjes 测度的重要性质。第一个定理提供了这类测度的一般性。

**定理 3.19** 令 $f$ 在 $\mathbb{R}$ 上单调且右连续。令 $\mu_f^*$ 为相关的方法 I 外测度，并令 $(\mathbb{R}, \mathcal{M}_f, \mu_f)$ 为生成的测度空间 $\mu_f^*$ 是规测度，因此所有波尔集都是 $\mu_f$-可测的。

2. 如果 $A$ 是有界波尔集，则 $\mu_f(A) < \infty$。
3. 每个集合 $A \subset \mathbb{R}$ 都有一个类型为 $\mathcal{G}_\delta$ 的可测覆盖。
4. 对于每个半开 $[a,b)$，$\mu_f([a,b)) = f(b) - f(a)$。

相反，令 $\mu$ 为 $\mathbb{R}$ 上的外测度且 $(X, \mathcal{M}, \mu)$ 为生成的空间。如果条件 (1)(2)(3) 被 $\mu^*$ 和 $\mu$ 满足，则存在定义在 $\mathbb{R}$ 上的单调右连续函数 $f$，使得 $\mu_f^*(A) = \mu^*(A)$ 对于所有 $A \subset \mathbb{R}$。特别，对于所有 $A \in \mathcal{M}$，$\mu_f(A) = \mu(A)$。

证明。定理的前半部分包含在我们的推导中。反向方向需要一些证明，因为

### 3.6. 勒贝-Stieltjes 测度的性质

我们对“质量”的概念还没有精确化。在 $\mathbb{R}$ 上定义 $f$：

```
$f(x) = \begin{cases} \mu((0,x]), & \text{if } x > 0; \ 0, & \text{if } x = 0; -\mu(x,0]), & \text{if } x < 0. \end{cases}$
```

显然，$f$ 是单不减的。为了验证 $f$ 是右连续的，设 $x \in \mathbb{R}$，$\delta_n\}$ 为一个趋于零的正数序列。不失一般性假设 $x > 0$。那么

```
$[0,x) = \bigcup_{n=1}^{\infty} [0,x+\delta_n).$
```

由于 (2)，$\mu((0,x+\delta_n)) < \infty$，由定理 2.20 可知：

```
$\lim_{n\to\infty} \mu((0,x+\delta_n)),$
```
