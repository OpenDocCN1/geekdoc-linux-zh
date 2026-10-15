
并不是每一个由方法 I 构建的外测度都是正规的。例 2.28 和练习 2:8.3 说明了这一点。定理 2.36 有助于证明，当调用方法 I 来扩展我们已经提到的原始概念（长度、面积、体积和质量）时，所得的外测度将是正规的。

# 第 2 章 测度空间

## 定理 2.36
令 $\mu^*$ 由*方法 I* 从 $T$ 和 $\tau$ 构造。如果 $T$ 的所有成员都是 $\mu^*$-可测的，那么 $\mu^*$ 是正规的。

## 证明
令 $A \subset X$。我们找到 $A$ 的一个可测覆盖。如果 $\mu^*(A) = \infty$，则 $X$ 是一个可测覆盖。假设 $\mu^*(A) < \infty$。对于任意 $m \in \mathbb{N}$，令 $\{T_{mn}\}_{n=1}^\infty$ 是来自覆盖类 $T$ 的集合序列，使得

$$A \subset \bigcup_{n=1}^{\infty} T_{mn} \quad \sum_{n=1}^{\infty} \tau(T_{mn}) < \mu^*(A) + \frac{1}{m}$$

令

$$T_m = \bigcup_{n=1}^{\infty} T_{mn} \quad \text{且} \quad H = \bigcup_{n=1}^{\infty} T_m.$$

由于每个集合 $T_m$ 是可测的，因此 $H$ 是 $A$ 的一个可测覆盖。

显然，$A \subset H$ 且 $\mu^*(A) \le \mu(H)$。对于反不等式，对于 $m \in \mathbb{N}$，我们有

$$\mu^*(T_m) \le \mu^*(T_{mn}) \le \sum_{n=1}^{\infty}\tau(T_{mn}) \le \mu^*(A) + \frac{1}{m}$$

对于每个 $m \in \mathbb{N}$，$H \subset T_m$，所以

$$\mu(H) \le \mu^*(T_m) \le \mu^*(A) + \frac{1}{m}$$

该不等式对于所有 $m \in \mathbb{N}$ 都成立，因此 $\mu(H) \le \mu^*(A)$。因此 $\mu(H) = \mu^*(A)$，$H$ 是 $A$ 的一个可测覆盖。$\blacksquare$

## 推论 2.37
$\mathbb{R}$ 上的勒贝格外测度 $\lambda^*$。

## 证明
这里 $T$ 包含所有开区间，$\tau(T)$ 是区间 $T$ 的长度。根据定理 2.36，只需证明通过 Carathéodory 判别（定义 2.29）每个区间 $(a, b)$ 都是可测的。

令 $E \in \mathbb{R}$ 且 $\varepsilon > 0$。存在一个覆盖 $E$ 的序列 $(T_n) \subset T$， 使得

$$\sum_{n=1}^{\infty}\tau(T_n) \le \lambda^*(E) + \frac{\varepsilon}{2}$$

取

$$\mathcal{U}_1 = \{T_n \cap (a,b) : n \in \mathbb{N}\}, \quad \mathcal{U}_2 = \{T_n \cap (-\infty,a) : n \in \mathbb{N}\}, \quad \mathcal{U}_3 = \{T_n \cap (b,\infty) : n \in \mathbb{N}\}$$

以及

$$\mathcal{U}_4 = \{(a-\frac{\varepsilon}{2}, a+\frac{\varepsilon}{2}), (b-\frac{\varepsilon}{2}, b+\frac{\varepsilon}{2})\}.$$

## 2.9. 正规外测度

那么 $\mathcal{U}_1$ 覆盖 $E \cap (a,b)$，而 $\mathcal{U}_2 \cup \mathcal{U}_3 \cup \mathcal{U}_4$ 覆盖 $E \setminus (a,b)$。$\mathcal{U}_1, \mathcal{U}_2, \mathcal{U}_3$ 中区间的总长度与原始序列相同，来自 $\mathcal{U}_4$ 的额外长度总和为 $\varepsilon/2$。因此

$$\lambda^*(E \cap (a,b)) + \lambda^*(E \setminus (a,b)) \leq \sum_{n=1}^{\infty} \tau(T_n) + \varepsilon/2 \leq \lambda^*(E) + \varepsilon$$

由于 $\varepsilon$ 是任意的，我们对于任何 $E \in \mathbb{R}$ 都有

$$\lambda^*(E \cap (a,b)) + \lambda^*(E \setminus (a,b)) \leq \lambda^*(E)$$

由此得出 $(a,b)$ 必须是可测的。

让我们使用第 2.7 节和 2.9 节中的一些思想，只要它们与区间上勒贝格测度的情况有关。在开始，我们从开区间族和作为区间长度的原始概念 $\tau(T)$ 开始。在应用方法 I 后，这产生了一个外测度 $\mu^*$。我们随后应用 Carathéodory 过程得到一类可测集和一个在 $T$ 上等于 $\mu^*$ 的测度 $\mu$。但它并没有证明第 2.1 节的内外法。对于这一点，我们需要验证 $\lambda^*$ 是正规的，然后调用定理 2.35。

并不是每一个由方法 I 构建的外测度都是正规的。例 2.28 和练习 2:8.3 说明了这一点。定理 2.36 有助于证明，当调用方法 I 来扩展我们已经提到的原始概念（长度、面积、体积和质量）时，所得的外测度将是正规的。
