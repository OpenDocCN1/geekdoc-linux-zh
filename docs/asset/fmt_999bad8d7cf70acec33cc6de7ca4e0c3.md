
\{f'(x) > 0\} \text{ and } \{f'(x) < 0\}

在 $[a,b]$ 中都是稠密的。这类函数可能难以可视化。

1887年，Köpeke 提供了这种函数的构造。在 Denjoy 1915 年的工作中：

1887年，Köpeke 在《数学分析》中给出了一种函数，该函数在每一点（他认为）都有导数，且导数在其域的每个区间内消失并改变符号。[他] 反复这类情况[参考文献]，每次都包含了前一次中的错误。这个关于可微处非单调函数的问题为许多其他工作提供了基础[参考文献]。

Denjoy 所提到的各种构造非常复杂。在 Denjoy 论文的这一点，他已经给出了他自己的三个独立构造。他正准备获得清晰的“清晰与简洁”，在此之前，他提醒读者要从“Borel 和 Lebesgue 关于集合的内容”中借鉴想法。对于 Denjoy，他的构造是简单的，而且显然不是可怕的。

Hobson Peano 在他的书中对 Köpeke 的构造进行了修改。这在 Köpeke 第一次修正后约40年、Peano 修改后30年、以及 Denjoy 的“简单且清晰”的发展后12年出版。这需要了十页纸。

目前有许多证明可用。有些是构造性的，比这些早期证明更简单。我们提供了一个基于 Baire 范类的简单证明。它由 C. Weil 在 1976 年提出，需要两页纸。为了给出我们的证明，我们需要知道有界导数的一致收敛极限是导数。由于 Weil 的证明提供了最后两节中开发的几个思想，我们提供了必要的细节。

> A. Denjoy, "Sur les fonctions dérivées dénombrables," Bull. Soc. Math. France 43 (1915) pp. 161–248.

> E. Hobson, Theory of Functions of a Real Variable, II, Dover, New York, (1957) (reprinting of original book published in 1927).

> C. E. Weil, "On nowhere monotonic functions," Proc. Amer. Math. Soc., 56 (1976), 388–389.

# 10.6. 在函数空间的应用

`M\Delta'` 表示 `[0,1]` 上有界导数的空间，其满足：

```
$$\rho(f,g) = \sup_{x\in[a,b]} |f(x) - g(x)|.
```

现在 `M\Delta'` 是 `M[0,1]` 的闭空间，因此是完备的。现在令

```
$M\Delta'_0 = \{f \in M\Delta' : f = 0 \text{ 在稠密集上}\}$.
```

我们证明 `M\Delta'_0` 在加法下是闭的且是完备的。由于 `f,g \in M\Delta'_0`，意味着集合 `{x : f(x) = 0}` 和 `{x : g(x) = 0}` 是 `\mathcal{G}_\delta` 类型的。两个 `\mathcal{G}_\delta` 类型的稠集的交集也是稠密的，因此

```
\{x : f(x) + g(x) = 0\}
```

是稠密的。同样，如果 `[f_n]` 是来自 `M\Delta'_0` 的序列且 `f_n \to f`，那么 `f \in M\Delta'_0`。为了证明这一点，令

```
$A_n = \{x : f_n(x) = 0\}$
```

并令 `A = \cap_{n=1}^\infty A_n`。这些集合是稠密的且 `\mathcal{G}_\delta` 类型，因此 `A` 也是如此。

```
$A \subset \{x : f(x) = 0\}$.
```

得出 `f \in M\Delta'_0`。因此 `M\Delta'` 在 `M\Delta'` 中是闭的，从而是完备的。

参考示例 5.2。我们构造了一个严格递增的可微函数 `h`，使得 `h' \in M\Delta'_0 \neq 0`。令 `I` 为 `[0,1]` 中的一个区间，令

```
$P = \{f \in M\Delta' : \rho > 0 \text{ 在 } I 上\}$
```

那么 `P` 在 `M\Delta'_0` 中是闭的。我们证明 `P` 在 `M\Delta'_0` 中是稠密的。令 `B(f,\epsilon)` 为 `M\Delta'_0` 中的一个开球。如果 `f \notin P`，我们证明 `P \cap B(f,\epsilon) \neq \emptyset`。在 `P` 中，令 `x_0` 为 `f` 在区间 `I` 中的一个连续点。该点的存在于定理 10.13。显然 `f(x_0) = 0`，因为 `{x : f(x) = 0}` 在 `[0,1]` 中是稠密的。选择一个开区间 `J \subset I` 使得 `f < -\epsilon/2`。选择 `g \in M\Delta'_0` 使得 `g \in P` 且

```
$\sup(-g(x)) = \sup(-g(x)) = \epsilon,$
```

我们可以例如取 `-g` 为 5.2 中函数 `h'` 的适当修改。那么 `f+g \in M\Delta'_0`。在 `J` 上 `0 < f(x) < \epsilon/2`，所以 `g(x) > \epsilon/2` 且 `g(x) < -\epsilon/2`。`f(x) + g(x) < 0`。得出

```
$f+g \in B(f, \epsilon)$
```

且 `P` 在 `M\Delta'_0` 中是稠密的。以类似的方法，我们证明

```
$N = \{f \in M\Delta'_0 : f \leq 0 \text{ 在 } I 上\}$
```

在 `M\Delta'_0` 中是闭的。我们已经证明，对于任何区间 `I \subset [0,1]`，集合

```
$A(I) = \{f \in M\Delta'_0 : x_1, x_2 \in I \text{ 使得 } f(x_1) > 0 \text{ 且 } f(x_2) < 0\}$
```

是 `M\Delta'_0` 的稠子集。令 `(A_k)` 为 `[0,1]` 中具有有理端点的区间枚举。令 `A_k = A(I)`。那么 `\bigcup_{k=1}^{\infty} A_k` 在 `C[a,b]` 中是 `\mathcal{F}_\sigma` 类型，因此在完备集 `\mathcal{H}` 中是 `\mathcal{F}_\sigma` 类型。集合 `\mathcal{H} \setminus A` 在完备空间 `\mathcal{H}` 中是 `G_\delta` 类型。现在 `H` 由保持端点的 `[0,1]` 上非退化的连续函数组成，因此 `H \setminus A` 包含 `H` 的严格递增成员；即 `H \setminus A = H`。

**定义 10.26** 从 `[a,b]` 到 `[a,b]` 的满足 `h(a)=a` 且 `h(b)=b` 的同胚 `h` 称为 `[a,b]` 的*自同态*。

我们的讨论显示 `[0,1]` 自同态集 `H` 在 `H` 中是 `G_\delta` 类型，因此是完备的。练习 10.6.12 提供 `[0,1]` 自同态的一个简单例子，它映射了一个测度零的康特集。作为说明 `[0,1]` 的第一范类子集 `A` 可以映射到零测度集的例，我们通过对拓扑完备的自同态空间 `H` 应用 Baire 范类定理来实现。如果 `A` 是测度为的第一范类集，读者可能想要尝试构造这样的自同态。

## 自同态空间

令 `H` 表示保持端点的 `[0,1]` 上严格递增连续函数的族。由于 `H` 上函数的均匀极限不必是严格递增的，`H` 在 `C[0,1]` 中不是闭的。因此 `H` 对于度量

```
$\rho(f, g) = \max |f(x) - g(x)|.$
```

不是完备的。似乎我们的方法在研究这个空间时失效。我们证明 `H` 是 `\mathcal{G}_\delta` 类型，因此在拓扑上是完备的。因此，Baire 范类论仍然适用。

## 10.6 在函数空间的应用

令 `I` 为 `[0,1]` 中的闭退化区间，令

```
$A(I) = \{h \in \mathcal{H} : h \text{ 在 } I 上为常数}\}$
```

那么 `A(I)` 是 `C[a,b]` 的闭子空间。令 `{I_n}` 为 `[0,1]` 中具有有理端点的非退化子区间的枚举。集合

```
$$\bigcup_{n=1}^{\infty} A(I_n)$$
```

在 `C[a,b]` 中是 `\mathcal{F}_\sigma` 类型，因此在完备集 `\mathcal{H}` 中是 `\mathcal{F}_\sigma` 类型。集合 `\mathcal{H} \setminus A` 在完备空间 `\mathcal{H}` 中是 `G_\delta` 类型。现在 `H` 由保持端点的 `[0,1]` 上非退化的连续函数组成，因此 `H \setminus A` 包含 `H` 的严格递增成员；即 `H \setminus A = H`。

**定理 10.25** 令 `\Delta_0` 表示 `[0,1]` 上可微函数 `F` 的集合，使得 `F(0)=0` 且 `F' \in M\Delta'_0`。对于 `F, G \in \Delta_0`，令

```
$\rho(F, G) = \sup |F'(x) - G'(x)|.
```
