
因为这对于所有 $n \ge N$ 都成立，所以 $\mu_0^*(A) + \mu_0^*(B) \le \mu_0^*(A \cup B)$。因此 $\mu_0^*$ 是一个度量外测度。

## 第 3 章 度量外测度

让我们回到示例 3.4。我们之前关于用较小正方形覆盖正方形 $T$ 的讨论表明，对于每个正方形 $T$，都有 $\mu_n^*(T) = \infty$。事实上，情况确实如此。如果 $T$ 是一个边长为单位的开正方形，$\mu_n^*(T) = n\sqrt{2}$。

$$\mu^*(T) = \lim_{n\to\infty} \mu_n^*(T) = \infty.$$

类似的证明说明对于所有 $T \in T$，$\mu^*(T) = \infty$。这并不意外，因为我们使用了一个“一维”概念（直径）作为二维集合 $T$ 的预测度。回想方法一外测度 $\mu^*(T) = n\sqrt{2}$，所以我们可以很容易地用自身覆盖 $T$。在这个例子中，小正方形无法有效地覆盖大正方形，方法一的结果与方法二不同。我们的下一个结果，定理 3.9 表明，如果“小正方形可以高效地覆盖大正方形”，那么方法一和方法二是一致的。

### 定理 3.9
令 $\mu^*$ 为由预测度 $\tau$ 和族 $T$ 通过方法二确定的测度，令 $\mu^*$ 为从 $\tau$ 和 $T$ 通过方法一构造的测度。$\mu_n^* = \mu^*$ 的充分必要条件是对于每个选择的 $\varepsilon > 0, \varepsilon \in T$ 和 $n \in \mathbb{N}$，存在来自 $T$ 的序列 $\{T_k\}$，使得 $T \subset \bigcup_{k=1}^\infty T_k$。

### 证明
必要性显而易见。如果对于某些 $\varepsilon$、$T_n$ 和 $n$ 条件不成立，则 $\mu_n^*(T) > \mu^*(T)$。证明充分性，首先观察到对于所有 $n \in \mathbb{N}$，$T_n \subset T$，

$$\mu_n^* \le \mu^*.$$ (6)

为了验证该不等式，令 $A \subset X$ 并令 $\varepsilon > 0$。我们可以假设 $\mu^*(A) < \infty$。令 $\{T_i\}$ 是来自 $T$ 的集合序列，使得 $A \subset \bigcup T_i$。

$$\sum_{i=1}^\infty \tau(T_i) \le \mu_n^*(A \cup B) + \varepsilon.$$

$$\mu_n^*(A) \le \sum_{k \in \mathbb{N}_1} \tau(T_{nk}),$$

以及

$$\mu_n^*(B) \le \sum_{k \in \mathbb{N}_2} \tau(T_{nk}).$$

因此，

$$\mu_n^*(A) + \mu_n^*(B) \le \sum_{k=1}^{\infty} \tau(T_{nk}) \le \mu_n^*(A \cup B) + \varepsilon.$$

由于这对于每个 $\varepsilon > 0$ 都成立，我们对于 $n \ge N$ 有：

$$\mu_0^*(A) + \mu_0^*(B) \le \mu_0^*(A \cup B).$$

因为这对于所有 $n \ge N$ 都成立，所以 $\mu_0^*(A) + \mu_0^*(B) \le \mu_0^*(A \cup B)$。因此 $\mu_0^*$ 是一个度量外测度。

## 3.3. 方法二

这证明了 $\mu_0^*$ 是一个外测度。

剩下的只需证明如果 $A$ 和 $B$ 是分离的，那么

$$\mu_0^*(A \cup B) = \mu_0^*(A) + \mu_0^*(B).$$

显然，

$$\mu_0^*(A \cup B) \le \mu_0^*(A) + \mu_0^*(B),$$

因此只需建立反向不等式即可。我们可以假设 $\mu_0^*(A \cup B)$ 是有限的。假设 $dist(A, B) > 0$。选取 $N \in \mathbb{N}$ 使得 $dist(A, B) > 1/N$。令 $\varepsilon > 0$。对于任意 $n \in \mathbb{N}$，存在来自 $T_n$ 的序列 $\{T_{nk}\}$，使得 $T_{nk} \supset A \cup B$ 且

$$\sum_{k=1}^{\infty} \tau(T_{nk}) \le \mu_n^*(A \cup B) + \varepsilon.$$

那么，对于 $n \ge N$ 和 $K \in \mathbb{N}$，没有任何集合 $T_{nk}$ 能同时遇到 $A$ 和 $B$，因此 $T_{nk} \cap A = \emptyset$ 或者 $T_{nk} \cap B \neq \emptyset$。

$$\mathbb{N}_1 = \{k \in \mathbb{N} : T_{nk} \cap A \neq \emptyset\}$$

以及

$$\mathbb{N}_2 = \{k \in \mathbb{N} : T_{nk} \cap B \neq \emptyset\}.$$

那么

$$\mu_n^*(A) \le \sum_{k \in \mathbb{N}_1} \tau(T_{nk}),$$

以及

$$\mu_n^*(B) \le \sum_{k \in \mathbb{N}_2} \tau(T_{nk}).$$

因此，

$$\mu_n^*(A) + \mu_n^*(B) \le \sum_{k=1}^{\infty} \tau(T_{nk}) \le \mu_n^*(A \cup B) + \varepsilon.$$

由于这对于每个 $\varepsilon > 0$ 都成立，我们对于 $n \ge N$ 有，

$$\mu_0^*(A) + \mu_0^*(B) \le \mu_0^*(A \cup B).$$

因为这对于所有 $n \ge N$ 都成立，所以 $\mu_0^*(A) + \mu_0^*(B) \le \mu_0^*(A \cup B)$。因此 $\mu_0^*$ 是一个度量外测度。

## 3.4. 近似

并且这个集，$\bigcup_{i=1}^\infty K_i$，是 $\bigcup_{i=1}^\infty E_i$ 的闭子集。

我们提到，定理 3.19 将证明证明中的 $\sigma$-代数 $\mathcal{E}$ 并不需要包含所有可测集。另见习题 3.6.3。我们现在转向通过开集从外部近似。

### 定理 3.13
设 $X$ 为度量空间，$\mu$ 为 $X$ 上的波尔测度，$\varepsilon > 0$ 且 $B$ 为一个波尔集。如果 $\mu(X) < \infty$，更一般地说，如果 $B$ 包含在可数有限 $\mu$-测度开集 $O_i$ 的并中，则 $B$ 包含在一个开集 $G$ 中，使得 $\mu(G \setminus B) < \varepsilon$。

### 证明
该定理从前得出。选择每个闭集 $C_i \subset O_i \setminus B$，使得

$$\mu(O_i \setminus B) = \mu(O_i \setminus C_i) < \varepsilon 2^{-i}.$$

这里，$B \cap O_i$ 是开集 $O_i \setminus C_i$ 的子集。定义

$$G = \bigcup_{i=1}^\infty (O_i \setminus C_i).$$

那么 $G$ 是开集，$G$ 包含 $B$，且 $\mu(G \setminus B) < \varepsilon$。

为了参考，我们结合使用这两个定理推导出一个在有限测度空间中有效的推论。

### 推论 3.14
设 $X$ 为度量空间，$\mu$ 为 $\mu(X) < \infty$ 的波尔测度。对于每一个 $\varepsilon > 0$ 和每一个波尔集 $B$，存在一个闭集 $F$ 和一个开集 $G$，使得

$$\mu(B) - \varepsilon < \mu(F) \leq \mu(B) \leq \mu(G) < \mu(B) + \varepsilon.$$

其中

从这两点中，我们可以很容易推导出一个近似定理，其使用的集比开集和闭集稍大。

### 定理 3.15
设 $X$ 为度量空间，$\mu$ 为 $X$ 上的满足 $\mu(X) < \infty$ 的波尔测度。那么每个波尔集 $B \subset X$ 都有一个 $\mathcal{F}_\sigma$ 类型的子集 $K$ 和一个 $G_\delta$ 类型的超集 $H$，使得

$$\mu(K) = \mu(B).$$

习题 2.1.14 来说，$X$ 中的每个波尔集都有一个 $G_\delta$ 型的可测覆盖和一个 $\mathcal{F}_\sigma$ 型的可测核。定理 3.15 叙述中 $\mu(X) < \infty$ 的要求不能省略。另见习题 3.4.3。

推论 3.14 和定理 3.15 涉及到用更简单的集近似波尔集。如果我们知道可测集可以被波尔集近似，那么 3.14 和 3.15 的结论就可以被加强。例如，在定理 3.11 的假设下，如果 $\mathcal{T}$ 由波尔集组成，每个可测集 $M$ 都有一个覆盖 $H \in \mathcal{B}$。如果 $\mu(X) < \infty$，$H$ 有一个 $\mathcal{G}_\delta$ 型的覆盖 $H'$。因此 $H'$ 也是 $M$ 的覆盖。如果需要，可以将 3.11、3.14 和 3.15 的假设恰当地结合到关于关于可测集被波尔集、$\mathcal{G}_\delta$ 型集、开集等近似的各种结果中。

## 第3章 度量外测度

### 习题

- **3.4.1** 在 $\mu(X) < \infty$ 的最简单情况下证明定理 3.13。
- **3.4.2** 证明定理 3.15。
- **3.4.3** 设 $B$ 为 $\mathbb{R}$ 中的波尔集。记得 $\mathbb{R}$ 的贝尔范畴理论中部分指出，在某些区间内稠密的 $\mathcal{G}_\delta$ 型集不能表示为无处稠密集的可数并。对于 $E \in \mathcal{B}$，如果 $E$ 是如今稠密集的可数并，则 $\mu(E) = \lambda(E)$，否则 $\mu(E) = \infty$。证明 $(\mathbb{R}, \mathcal{B}, \mu)$ 是一个使得定理 3.15 结论失效的测空间。
- **3.4.4** $\mu$ 为度量空间 $X$ 上的有限波尔测度。证明对于每个波尔集 $B \subset X$，$\mu(B) = \inf \{\mu(G) : B \subset G, G \text{ 开}\}$且 $\mu(B) = \sup\{\mu(F) : F \subset B, F \text{ 闭}\}$。

## 3.5 Lebesgue-Stieltjes 测度的构造
