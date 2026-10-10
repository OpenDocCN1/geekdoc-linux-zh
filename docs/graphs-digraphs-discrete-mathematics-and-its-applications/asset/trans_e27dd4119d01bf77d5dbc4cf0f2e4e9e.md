
## 21.1. 概率构造法

**证明。** 当 $k = 2$ 时，任何长度大于 $\ell$ 的偶环都具有所需的性质。因此，我们可以假设 $k \geq 3$。设 $\Theta$ 为满足 $0 < \Theta < \frac{1}{2}$ 的实数，对于固定的整数 $n \geq 3$，令 $p = n^{\Theta-1}$。考虑概率空间 $S$，其元素是顶点集为 $\{v_1, v_2, \ldots, v_n\}$ 的 $2 \binom{n}{2}$ 个不同的有标号图。通过设定 $P[v_i v_j \in E(G)] = p$ 并使这些事件相互独立，从而确定 $S$ 中图 $G$ 的概率。因此，每个大小为 $m$ 的 $2 \binom{m}{2}$ 个不同的有标号图出现的概率为 $p^m(1-p)^{\binom{n}{2}-m}$。

设 $X$ 为定义在 $S$ 上的随机变量，表示图 $G \in S$ 中长度至多为 $\ell$ 的 $i$-环的数量。对于固定的整数 $i$，$3 \leq i \leq \ell$，$\{v_1, v_2, \ldots, v_n\}$ 有 $\binom{n}{i}$ 个 $i$ 元子集。对于每个这样的子集 $U$，对应于 $G$ 中可能的 $i$-环，$U$ 中顶点有 $\frac{(i-1)!}{2}$ 种不同的循环排列。我们通过以下方式得出这个界限。对于 $U$ 中的每个顶点 $u$，以 $u$ 为起始顶点的 $U$ 中顶点的排列共有 $(i-1)!$ 种，这些排列可以形成 $G$ 中的一个 $i$-环。由于这些顶点的反向排列产生相同的环，因此由 $U$ 的顶点组成的可能的 $i$-环有 $\frac{(i-1)!}{2}$ 个。因此，有

$$\binom{n}{i} \frac{(i-1)!}{2} = \frac{n(n-1) \cdots (n-i+1)}{2i}$$

个潜在的 $i$-环，所以 $X$ 可以表示为

$$\sum_{i=3}^{\ell} \frac{n(n-1) \cdots (n-i+1)}{2i}$$

个示性变量之和。此外，由于 $i$-环出现的概率为 $p^i$，由期望的线性性质可知

$$E[X] = \sum_{i=3}^{\ell} \frac{n(n-1) \cdots (n-i+1)}{2i} p^i. \tag{21.9}$$

由于 $p = n^{\Theta-1}$，由 (21.9) 可得

$$
\begin{aligned} E[X] \quad = \quad & \sum_{i=3}^{\ell} \frac{n(n-1) \cdots (n-i+1)}{2i} (n^{\Theta-1})^i \\ = \quad & \sum_{i=3}^{\ell} \frac{n(n-1) \cdots (n-i+1) n^{\Theta i}}{2i \ n^i} < \sum_{i=3}^{\ell} \frac{n^{\Theta i}}{2i}. \end{aligned}
$$

根据 $\Theta$ 的选取，可知 $\Theta \ell = 1-\epsilon$，其中 $\epsilon$ 为满足 $0 < \epsilon < 1$ 的某个实数。因此，

$$\frac{E[X]}{n/2} \leq \sum_{i=3}^{\ell} \frac{n^{\Theta i}}{ni} \leq \sum_{i=3}^{\ell} \frac{n^{\Theta i}}{ni} = \frac{K}{n^\epsilon}$$

其中 $K = \sum_{i=3}^{\ell} \frac{1}{i}$，所以 $\lim_{n\rightarrow\infty} \frac{E[X]}{n/2} \leq \lim_{n\rightarrow\infty} \frac{K}{n^\epsilon} = 0$。

由 (21.8) 中的马尔可夫不等式，

$P[X \geq n/2] \leq \frac{E[X]}{n/2}.$

因此，对于足够大的 $n$，有 $P[X \geq n/2] < 1/2$。

令 $t = \lceil 3(\ln n)/p \rceil$。给定的 $V(G) = \{v_1,v_2,\ldots,v_n\}$ 的 $t$ 元子集是独立集的概率为 $(1-p)^{\binom{t}{2}}$。由于有 $\binom{n}{t}$ 个这样的集合，因此

$P[\alpha(G) \geq t] \leq \binom{n}{t} (1-p)^{\binom{t}{2}}.$

然而，$1-p < e^{-p}$（由 21.1 可知），所以

$P[\alpha(G) \geq t] \leq \binom{n}{t} e^{-p\binom{t}{2}} < \left(ne^{-p(t-1)/2}\right)^t.$

由于

$t = \left\lceil \frac{3\ln n}{p} \right\rceil = \left\lceil \frac{3\ln n}{n^{\Theta-1}} \right\rceil = \lceil 3(\ln n) n^{1-\Theta} \rceil$

且 $1-\Theta > 0$，可知 $\lim_{n\rightarrow\infty} t = \infty$。因此，$\lim_{n\rightarrow\infty} \left(\frac{1}{e}\right)^{p(t-1)/2} = 0$。于是，根据 (21.2) 的推广，我们有 $\lim_{n\rightarrow\infty} n e^{-p(t-1)/2} = 0$，并且可以选取 $n$ 使得 $P[\alpha(G) \geq t] < \frac{1}{2}$ 且 $P[X \geq n/2] < \frac{1}{2}$。因此，存在一个图 $G \in S$，其长度至多为 $\ell$ 的环的数量少于 $n/2$，且 $\alpha(G) < t$。由于

$t = \lceil 3(\ln n)/p \rceil = \lceil 3(\ln n) n^{1-\Theta} \rceil$

且对于正实数 $\alpha$，$\lim_{n\rightarrow\infty} \frac{\ln n}{n^\Theta} = 0$（参见 (21.3)），我们可以假设 $n$ 足够大，以确保 $t < \frac{n}{2k}$。

从 $G$ 中每个长度至多为 $\ell$ 的环中移除一个顶点，并将所得图记为 $G_1$。那么 $G_1$ 的围长大于 $\ell$，即 $g(G_1) > \ell$。此外，

$\alpha(G_1) \leq \alpha(G) < \frac{n}{2k}.$

而且，由定理 14.9，

$\chi(G_1) \geq \frac{|V(G_1)|}{\alpha(G_1)} \geq \frac{n/2}{n/(2k)} = k.$

最后，如有必要，从 $G_1$ 中移除顶点，产生一个图 $G_2$，使得 $g(G_2) > \ell$ 且 $\chi(G_2) = k$。$\blacksquare$

我们在本节中展示的证明表明，可以使用概率证明法建立图论许多领域的定理。此外，我们只使用了非常简单的概率概念和结果。使用更强大的工具，如二阶矩法、鞅或 Lovász 局部引理，可以获得更多例子。

## 21.2 随机图

在 21.1 节中，我们发现定义适当的概率空间对于确立具有某些所需性质的图的*存在性*非常有用。在本节中，我们提供了随机图的正式模型，并回答了关于随机图具有某些感兴趣性质（如非平面图，或对于某个正整数 $k$ 是 $k$-连通的）的概率问题。

### 随机图简介

对于正整数 $n$ 和实数 $p$（满足 $0 < p < 1$），**随机图** $G(n, p)$ 指概率空间，其元素是顶点集为 $\{v_1, v_2, \ldots, v_n\}$ 的 $2^{\binom{n}{2}}$ 个不同的有标号图。通过设定 $P[v_{uv} \in E(G)] = p$，且这些事件相互独立，从而确定 $G \in G(n, p)$ 中图的概率。因此，任何大小为 $m$ 的此类图的概率为 $p^m(1-p)^{\binom{n}{2}-m}$。重要的是要记住，当我们谈论“一个随机图”时，我们实际上指的是概率空间 $G(n, p)$。

例如，如果 $p = \frac{1}{2}$，那么顶点集为 $\{v_1, v_2, \ldots, v_n\}$ 且大小为 $m$ 的每个 $2^{\binom{n}{2}}$ 个不同的有标号图都被赋予概率 $(\frac{1}{2})^m(\frac{1}{2})^{\binom{n}{2}-m} = (\frac{1}{2})^{\binom{n}{2}}$。因此，这些 $2^{\binom{n}{2}}$ 个图中每一个的概率为 $1/2^{\binom{n}{2}}$，这是符合预期的。另一方面，假设 $0 < p < 1$ 且 $p \neq 1/2$，例如 $p = 1/4$。那么，在 $G(n, p) = G(n, \frac{1}{4})$ 中，顶点集为 $\{v_1, v_2, \ldots, v_n\}$ 且大小为 $m$ 的每个 $2^{\binom{n}{2}}$ 个不同的图的概率为 $(\frac{1}{4})^m(\frac{3}{4})^{\binom{n}{2}-m}$。我们在下方展示了 $n = 3$ 且 $p = 1/4$ 时的概率空间 $G(n, p)$。

在这里，$G(3, \frac{1}{4})$ 表示概率空间，其元素是顶点集为 $\{v_1, v_2, v_3\}$ 的 $2^3 = 8$ 个不同的有标号图 $G_1, G_2, \ldots, G_8$。图 21.1 展示了这八个不同的有标号图。

![](img/598a6ae3fd44120830ada34717906f29_567_0.png)

我们写 $P[G]$ 表示 $P[G \in G(n, p)]$，其中

$P[G_1] = (\frac{3}{4})^3$，$P[G_2] = P[G_3] = P[G_4] = \frac{1}{4}(\frac{3}{4})^2$，$P[G_5] = P[G_6] = P[G_7] = (\frac{1}{4})^2 \frac{3}{4}$ 以及 $P[G_8] = (\frac{1}{4})^3$。

对于图 $G(n, p)$ 中边数 $m$ 的每个可能值，$0 \le m \le \binom{n}{2}$，有 $\binom{\binom{n}{2}}{m}$ 个具有 $m$ 条边的不同有标号图。正如我们之前提到的，每个这样的图的概率是 $p^m(1-p)^{\binom{n}{2}-m}$。因此，

$$
\begin{aligned}\sum_{G \in G(n, p)} P[G] &= (1-p)^{\binom{n}{2}} + \binom{n}{2}p(1-p)^{\binom{n}{2}-1} \\&+ \binom{n}{2}^2p^2(1-p)^{\binom{n}{2}-2} + \cdots + p^{\binom{n}{2}} \\&= \sum_{m=0}^{\binom{n}{2}}\binom{\binom{n}{2}}{m}p^m(1-p)^{\binom{n}{2}-m}.\end{aligned}
$$

根据二项式定理，可得

$$\sum_{G \in G(n, p)} P[G] = [p + (1-p)]^{\binom{n}{2}} = 1.$$

在本节中，我们讨论“几乎所有图”所具有的性质。具体而言，对于给定的图论性质 $Q$，如果我们说在 $G(n, p)$ 中**几乎所有图**都具有性质 $Q$，是指

$$\lim_{n \to \infty} P[G \in G(n, p) \text{ 具有性质 } Q] = 1.$$

例如，我们将在定理 21.6 中看到，对于任何小于 1 的正常数 $p$，在 $G(n, p)$ 中几乎所有图都是直径为 2 的连通图。

验证几乎所有图具有某个性质 $Q$ 的一个有用技巧是定义定义在 $G(n, p)$ 上的适当的整数值随机变量 $X$，使得如果 $X = 0$，则 $G \in G(n, p)$ 具有性质 $Q$。因此，对于 $G \in G(n, p)$，

$$P[X = 0] \le P[G \in G(n, p) \text{ 具有性质 } Q].$$

