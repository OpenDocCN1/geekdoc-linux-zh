
## 12.1.1A 有多少种着色方案？

- i. 使用两种颜色对标准的 $8 \times 8$ 棋盘进行着色
- ii. 使用三种颜色对立方体的面进行着色

## 12.1.1B
使用 $k$ 种颜色对 $n \times n$ 棋盘进行着色，有多少种着色方案？

## 12.1.2A
给出两个对 $2 \times 2$ 棋盘使用*三种*颜色的着色方案示例，使得其中一个可以通过*反射*从另一个获得，但不能通过*旋转*获得。

## 12.1.2B
是否存在两个对立方体的面使用两种颜色的着色方案，使得其中一个可以通过*反射*从另一个获得，但不能通过*旋转*获得？

![](img/eb401bf41900fd678cd9d368a197e486_262_0.png)

![](img/eb401bf41900fd678cd9d368a197e486_262_1.png)

![](img/eb401bf41900fd678cd9d368a197e486_263_0.png)

![](img/eb401bf41900fd678cd9d368a197e486_263_1.png)

## 12.2 群作用公理

我们想要描述这样一种一般情况：即一个群（例如 $G$）和一个集合（例如 $X$）之间存在相互作用。在这个抽象讨论中，你可能会觉得保持前一节中描述的“正方形的对称性”和“$2 \times 2$ 棋盘的着色”这一具体例子在脑海中会有所帮助。我们将经常引用这个例子。

在我们例子中，正方形的对称性与每个着色方案相互作用，产生一个（可能不同的）着色方案。例如，顺时针四分之一旋转，我们使用符号 `a` 来表示它，与着色 `C2` 相互作用产生着色 `C3`。我们通过写 `a \triangleright C2 = C3` 来表示这一点，并且通常，我们使用 `g \triangleright x` 来表示 `g` 作用于 `x` 的结果。为了发展一般理论，我们要求这种相互作用满足以下定义中给出的几个简单且自然的性质。

### 定义 12.1

设 `(G, \bullet)` 为一个群，设 `X` 为一个集合。如果说 `G` 作用于 `X`，是指对于每个 `g \in G` 和每个 `x \in X`，都定义了元素 `g \triangleright x \in X`，并且满足以下性质：

> **群作用条件**
>
> - GA1. 对于每个 `x \in X`，`e_G \triangleright x = x`，其中 `e_G` 是 `G` 的单位元。
> - GA2. 对于所有 `g1, g2 \in G` 和每个 `x \in X`，`g1 \triangleright (g2 \triangleright x) = (g1 \bullet g2) \triangleright x`。

每当一个群作用于一个集合时，我们说我们有一个*群作用*。

我们要强调指出，在群作用中，`G` 的元素通常与 `X` 的元素完全不同。因此，`g` 作用于 `x` 产生 `g \triangleright x` 的过程，与例如两个同类群元素的结合产生另一个群元素的过程非常不同。所以，虽然我们通常省略群运算的符号并写 `gh` 而不是 `g \bullet h`，但符号 `\triangleright` 绝不应该被省略。它有助于提醒我们 `g` 和 `x` 之间的差异。[在那些群 `G` 的元素是定义域为 `X` 的函数的情况下，有时用 `g(x)` 代替 `g \triangleright x` 可能是合适的。]

不难看出，如果 `G` 是某个图形的对称群，且 `X` 是该图形所有着色方案的集合，那么按前一节定义的作用满足性质 GA1 和 GA2。在这种情况下，GA1 相当于 `G` 的单位元是恒等映射 `I`，且对于每个着色 `x`，`I \triangleright x = I(x) = x`；而 GA2 则相当于 `g1 \triangleright (g2 \triangleright x) = g1(g2(x)) = g1 \circ g2(x) = (g1 \circ g2) \triangleright x`。因此，前一节的例子都是群作用。关于其他不同类型的例子，请见本节末尾的练习。

我们以一个简单的关于群作用的技术引理结束本节，稍后我们需要用到它。

### 引理 12.1

设 `G` 是一个作用于集合 `X` 的群。则对于每个 `g \in G` 和所有 `x \in X`，

$$g \triangleright x = y \Leftrightarrow g^{-1} \triangleright y = x.$$

**证明**

假设 `g \triangleright x = y`。那么，根据 (GA2)，`g^{-1} \triangleright y = g^{-1} \triangleright (g \triangleright x) = (g^{-1} \bullet g) \triangleright x`，根据 GA1，`= e \triangleright x = x`。

逆命题 `g^{-1} \triangleright y = x \Rightarrow g \triangleright x = y` 的证明类似。

## 练习

### 12.2.1A
设 `G` 为实数群，`(\mathbb{R}, +)`，运算为加法，设 `X` 为平面点集，`\mathbb{R}^{2}`。假设我们通过规定对于每个 `\theta \in \mathbb{R}` 和所有 `x \in \mathbb{R}^{2}`，`\theta \triangleright x =` `x` 绕原点逆时针旋转角度 `\theta` 后移动到的点，来定义 `\mathbb{R}` 在 `\mathbb{R}^{2}` 上的作用。[因此，`\theta \triangleright (x, y) = (x \cos \theta - y \sin \theta, x \sin \theta + y \cos \theta)`。] 证明这满足群作用条件。

### 12.2.1B
这个问题涉及一个更复杂的群作用例子。设 `G` 为任意群。我们通过以下方式定义群 `G` 在 `G` 上的作用：对于 `g \in G` 和 `x \in G, g \triangleright x = gxg^{-1}`。证明这满足群作用条件。在此情况下，该作用称为共轭作用，`gxg^{-1}` 称为 `x` 关于 `g` 的共轭元素。这在群论中起着重要作用，但从本书的角度来看并不十分重要。

### 12.2.2A
设 `n` 为一个正整数。我们通过以下方式定义群 `S_n`（集合 `{1,2,\dots,n}` 的所有排列群）在完全图 `K_n = (V_n, E_n)`（具有 `n` 个顶点，设 `V_n = {v_0(i), v_3}` [注：原文此处似有截断或笔误，保留原意]）的边集上的作用：对于 `\sigma \in S_n` 和 `{v_i, v_j} \in E_n, \sigma \triangleright {v_i, v_j} = {v_{\sigma(i)}, v_{\sigma(j)}}`。证明这满足群作用条件。这个群作用的例子在计算不同简单图的数量时起重要作用，我们将在第 14 章中这样做。

### 12.2.2B
设 `G` 为一个群，设 `g_0` 为 `G` 中的特定元素。我们按以下方式定义整数加群 `(Z, +)` 在 `G` 上的作用：对于 `n \in \mathbf{Z}` 和 `g \in G`，`n \triangleright g := g^{ng_0}`，其中我们将 `g^0` 解释为 `G` 的单位元 `e_G`，而对于 `n < 0`，我们将 `g^n` 解释为 `(g^{(-1)^n})^{-1}` [注：此处原文符号可能有误，通常负指数意味着逆元，这里严格保留原文表述]。证明这满足群作用条件。

### 12.2.3A
假设群 `G` 作用于集合 `X`。证明对于所有 `g, h \in G` 和所有 `x \in X`，`g \triangleright x = h \triangleright x \Leftrightarrow g^{-1}h \triangleright x = x`。

### 12.2.3B
考虑练习 12.2.1A 中描述的 `\mathbf{R}` 在 `\mathbf{R}^2` 上的群作用。确定集合

`{\theta \in \mathbf{R}: \theta \triangleright (1,0) = \frac{\pi}{4} \triangleright (1,0)}`.

## 12.3 轨道
