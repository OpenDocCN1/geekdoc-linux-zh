
$E_{\mathbf{z} \sim \mathcal{D}^m} [|\hat{R}_m(h) - \mathcal{R}(h)|] \leq \sup_{h \in \mathcal{H}} |\hat{R}_m(h) - \mathcal{R}(h)| \leq 2\sqrt{\frac{d_c}{m}}$

其中 $d_c$ 是 $\mathcal{H}$ 的 VC 维度。

```
$d_c := \max \{m \in \mathbb{N} \mid \exists \mathbf{z} \in \mathcal{X}^m, \forall h_1, h_2 \in \mathcal{H}, h_1(\mathbf{z}) \neq h_2(\mathbf{z})\}$
```

零一损失 $l_0$ 的泛化界随之得出：对于随机抽取的训练样本 $\mathbf{z} \in \mathcal{X}^m$，概率至少为 $1-\delta$，对于所有 $h \in \mathcal{H}$，$\mathcal{R}(h) \leq \hat{\mathcal{R}}_m(h) + \dots$

```
$\ell_0(\mathbf{z}, d, \delta) := \hat{R}_m(h) + d\sqrt{\frac{2}{m}} + \frac{\ln(1/\delta)}{m}$
```

该界中的项是常数，可以通过 VC 维度 $d_c$ 易于估计。注意，对于一般的损失函数 $l: \mathcal{X} \times \mathcal{Y} \to \mathbb{R}^{+}$，通过研究函数族 $\{l(h, y) \mid h \in \mathcal{H}, y \in \mathcal{Y}\}$ 可以获得相似的结果。

有很多关于限制特定假设空间 VC 维度的结果（参见《神经网络的 VC 维度》）。在 PAC 学习框架下，无论选择何种假设空间，都可以为任何算法的泛化误差提供一个界。

我们可以通过对给定样本大小 $m \in \mathbb{Z}$ 需要覆盖的复杂度进行排序来放宽这种归纳。对于函数 $L: \mathcal{X}^m \times \mathcal{Y} \to \mathbb{R}$，它被称为“幸运性”（luckiness）（参见 Shaley-Taylor 等人，1999）。对于每种幸运性，都要求在训练样本上测得的值使得能够以高概率对假设的泛化误差进行界。

对于零一损失 $l_0$，主要结果（如上所述）如下：对于所有关于 $\omega$ 可能是光滑的损失函数 $L$，对于随机抽取的训练样本 $z \in \mathcal{Z}^m$，概率至少为 $1-\delta$；对于所有满足 $R[h, z] = 0$ 的 $h \in \mathcal{H}$，有 $R[h] \leq \delta$

```
$D_c(h, \omega, l, \delta) := \sqrt{\frac{2}{m}(\log(L(h, z), m) + \log(2/\delta))}$
```

### 有效复杂度

该结果也可以适用于非零误差和一般损失函数。通过使用 Schacher 平滑函数对假设空间 $\mathcal{H}$ 进行数据结构化 $\mathcal{H}(1) \subseteq \mathcal{H}(2) \dots \subseteq \mathcal{H}(m)$

```
$\mathcal{H}(z) := \{h \in \mathcal{H} \mid l(h, z), m \leq 2\}$
```

幸运性的选择不是唯一的；它基于分析中的先验选择（《贝斯方法与神经网络》）。

PAC-Bay 框架。PAC-Bay 学习算法。其核心思想是捕捉类似的幸运性。动机之一是捕捉依赖随机数据的置优势。

将不同因素的并集直接应用会导致以下结果：对于随机抽取的训练样本 $\mathbf{z} \in \mathcal{X}^m$，概率至少为 $1-\delta$，对于所有满足 $P(h, z) > 0$ 的 $h \in \mathcal{H}$，

```
$\ell_{pg}(h, z, \delta) := \hat{R}_m(z) + \sqrt{\frac{1}{m}(\ln(1/\delta) + \ln(m))}$
```

### 有效复杂度

如果似然性 $P(h, z)$ ，则 $\ell_{pg}(h, z, \delta)$ 很小。

使用量词引理工具，可以证明 Gibbs 分类策略，该策略对每个随机抽取日的新点使用：

```
$\hat{R}_{\text{Gibbs}}(z) = h \sim P_{\mathbf{z}}$
```

量词引理是并界的高概率版本：对于高概率 $\delta$（见公式 7）以及对于分布 $P$ ($1, \dots$)，可以证明以下结果：给定测度 $P$，对于随机抽取的训练样本 $\mathbf{z} \in \mathcal{X}^m$，概率至少为 $1-\delta$，对于所有 $h \in \mathcal{H}$，Gibbs 策略的泛化误差为：

```
$\hat{R}_{\text{Gibbs}}(z) \leq R[h] + \sqrt{\frac{1}{m}(\ln(1 + \ln(1/\delta))}$
```

### 有效复杂度

有效复杂度与 $P_n(H)$ 反比测量，在似然性 $P_n(x,y)=l(x,y)$ 下，贝斯后验 $P(h)$。值得提到的是，结果不仅适用于贝斯后验，还适用于所有 $h \in H$。如果在线算法在训练样本 $z$ 上出现错误，则其经验风险 $\hat{R}[h]$ 是很小的。这种方案允许确定在线学习的泛化误差（见 Cesa-Bianchi, 2007)。

## 与算法相关的界

我们总结了三种分析算法的不同相关方法，这些方法利用来自 $z$ 的性能。

压缩框架（Lloyd 和 Warmuth, 1995）基于学习算法仅使用训练样本的一部分来重构假设的想法。假设学习算法可以写为：

```
$\hat{h}(z) := \arg\min_{h \in H} \hat{R}_S(h)$
```

其中 $z = \{(x_i,y_i)\}_{i=1}^m$ 映射到 $z，$S = \{(x_i,y_i)\}_{i \in I}$ 是 $z$ 的子集，其中 $I = \{i_1, i_2, \dots, i_k\} \subset \{1, \dots, m\}$，$z_S$ 是训练模式。此类算法的一个典型例子是感知机学习算法（《感知机、反向传播》），它可以通过训练模式重构其假设。研究这类学习算法的数学工具是算法相关的界：

```
$\hat{R}_z(h) = \frac{1}{m} \sum_{i \in I} \ell(x_i, h(i)) + \frac{1}{m} \sum_{i \notin I} \ell(x_i, h(i)) \leq \hat{R}_S(h)$
```

对于任何输入样本 $z$，如果固定假设 $\hat{h}(z)$ 的期望风险与经验风险之间的差异很小。即，如果期望风险超过 $\epsilon$ 且错误不超过 $\delta$ ($\epsilon(m, \delta)$)，对于大小为 $m$ 的不同 $z$，这就是压缩框架的定义。

对于零一损失 $\ell_0$，任何可以写成公式 10 形式的学习算法，对于随机抽取的训练样本 $z \in Z$，概率至少为 $1-\delta$，$\hat{R}[\hat{h}(z)] \leq \epsilon(m, \delta)$，其中对于任何 $\epsilon(d,\delta)$

```
$\epsilon(d, \delta) = \frac{d}{m} + \sqrt{\frac{2}{m}(\ln\frac{m}{d} + \ln\frac{1}{\delta})}$
```

### 有效复杂度

对于一般损失函数可以得到类似的结果。在这种情况下，界取决于 $\ell(z)$、算法 $A$ 以及训练样本 $z \in Z$。

压缩框架基于在线学习理论（Litton, 1994）。在线学习算法通过试验进行。每次试验，算法接收一个训练样本 $x \in X$ 和一个目标 $y \in Y$。它接收输出 $\hat{y}$，如果 $\hat{y} \neq y$ 则产生错误。在线学习算法的性能衡量标准。

算法框架。在算法框架（Bosquet 和 Elisseeff, 2001）中，假设任何额外样本对所学信息以及任何可能的测试点的影响都是有限的。此类算法都是稳定的，并且具有对于所有 $i \in \{1, \dots, m\}$ 的以下性质：

```
$\forall z \in Z, \forall h, h' \in H: |\ell(z,h) - \ell(z,h')| \leq \beta(z)$
```
