
其中 $e = \min_{i \neq j} w_{ij}$，$b \in \{1, \dots, n\}$，$||W||_1 = \sum_{i,j} |w_{ij}|$，且 $||b||_1 = \sum_i |b_i|$。

证明。根据定理1，对于任何 $k \in \{1, \dots, n\}$，$\Delta E \leq \frac{1}{2}\min w_{ii}$。另一方面，$|E(t)| \leq \frac{1}{2}b$。从前面的不等式我们得到了 $\Delta E$ 和 $\tau(W,b)$ 的界。

## 并行更新

我们支持以下网络：

$x(t+1) = \sum_j w_{ij}x_t(j) - b_i \geq 0$ 对于 $i \in \{1, \dots, n\}$。

在此背景下，我们有有界的能量：

### 定理 3 (Goles et al., 1985)
令 `W` 为 $n \times n$ 对称矩阵。则能量

$\Delta E(t) = -\frac{1}{2}\sum_{i,j} w_{ij}x_t(i)x_t(j) - \sum_i b_ix_t(i) + E(t+1) \leq 0$

是并行更新下的能量减少。

证明。令 $\Delta E = E(t) - E(t-1)$。由于 `W` 是对称的，我们得到：

$\Delta E = -\sum_i b_i(x_t(i) - x_{t-1}(i)) - \frac{1}{2}\sum_{i,j} w_{ij}x_t(i)x_{t-1}(j)$

根据阈值的定义，$\Delta E \leq 0$，且当 $x(t) \neq x(t-1)$ 时它非零。□

### 推论 1
对于对称矩阵 `W`，并行更新收敛到固定点或二周期循环。

证明。假设 $\{x(0), \dots, x(T-1)\}$ 是周期为 $T$ 的循环。由此得出 $T$ 必然是常数。如果 $T > 2$，$x(0) \neq x(2)$，并行更新将是 $E(0)$，这是一个矛盾。□

### 推论 2
对于正定矩阵 `W`，并行更新收敛到固定点。

证明。从定理11足以证明不存在双周期。如果 $x(t)$ 是双周期，则 $x(t) = x(t-2)$。由于 `W` 是对称的，$a(t) - a(t-1) = Wx(t-1) - Wx(t-2) = 0$，仅当 $x(t) = x(t-1)$ 时成立。从方程4和

$ax(t) - x(t-1) = Wx(t-1) - Wx(t-2) = \Delta E + \Delta a$。

根据定理3，我们知道 $\Delta E \leq 0$ 且 $\Delta a \leq 0$，因此 $a=0$。如果 $x(t) = x(t-2)$，则不存在双周期。

# 404 III：文章

来自对称性，带有能量功率。然而，对称性的变分是可能的。

可以将该结果推广到准对称矩阵类。我们称一个矩阵 `W = (w_{ij})` 是对称的，如果存在一个正向量 $(u_1, \dots, u_n)$，使得对于 $i, j \in \{1, \dots, n\}$，有 $w_{ij}u_i = w_{ji}u_j$。我们有如下结论：

**定理 4.** (Goles and Martinez, 1990)。假设 `W` 为对称矩阵。那么能量 $E(t) = -\frac{1}{2}\sum_{i,j}w_{ij}x_i(t)x_j(t) + \sum_i u_ix(t)$ 是异步更新和并行更新的能量。

量 $E(t) = -\frac{1}{2}\sum_{i,j}w_{ij}x_i(t)x_j(t-1) + \sum_i u_ix(t-1)$ 是并行更新的能量。

## 连续离散时间漂移模型

考虑一个实值函数 `f: R -> R`，它在区间 `I = [-a, b]` 上严格递增，且 `f(-a) = f(b) = 0`；在 `I` 之外，当 `x < -a` 时 `f(x) = -a`，当 `x > b` 时 `f(x) = b`。这可以被 Hopfield (1984) 使用并经典地应用于多层网络。一个例子是 BSS 模型 (1986)，其中 `f` 关于 `S` 是线性的。

$$
y_i = \text{arg}(x_i) \quad i=1\dots n
$$

其中 $x_i = \sum_j w_{ij}y_j - b_i$。对于该模型以及之前段落定义的迭代，我们有如下结论：

**定理 5.** (Goles and Martinez, 1990)。假设 `W` 是一个 $n \times n$ 对称矩阵。如果 `diag(W) = 0`，则异步更新或并行更新会降低能量。

此外，量

$$
E(t) = -\frac{1}{2}\sum_{i,j}w_{ij}x_i(t)x_j(t) + \sum_i \left( \int_{x_i(t-1)}^{x_i(t)} f^{-1}(s)ds + \int_{x_i(t)}^{x_i(t-1)} f(s)ds \right) + \sum_i b_ix_i(t)x_i(t) \quad (7)
$$

是并行更新的能量。

*证明。* 我们首先给出类似于（并行的）周期的证明。我们更新异质项，假设第 $k$ 个神经元为 $x^{(t)} = (x_1^{(t)}, \dots, x_n^{(t)})$，其中 $x_k^{(t)} = \text{arg}(\sum_j w_{kj}x_j^{(t-1)} - b_k)$，$z \in \mathbb{S}$。由于 `W` 是对称的，一次得到一个神经元，因此如果 $x_k = \text{arg}(z)$，则

$$
\Delta_E = -x_k - \sum_{j \neq k} w_{kj}\text{arg}(z) - \frac{1}{2}w_{kk}x_k^2 - \int_{\text{arg}(z)}^{x_k} f^{-1}(s)ds
$$

由于 $w_{kk} \geq 0$，二次项显然是负的。对于其他项，令 $u = \text{arg}(z)$  $v = x_k$，那么 $\Delta_E = -(f(u) + f^{-1}(v) - f_{0} - f^{-1}(u))$。根据定义，我们很容易得到：

$$
\int_{u}^{v} f^{-1}(s)ds = \alpha(u) - \int_{v}^{u} f(s)ds \quad (8)
$$

所以 $\Delta E = (u-v)f(v) + \int_{v}^{u} f(s)ds$。由于 `f` 是递增函数，对于并行更新，$\Delta E \leq 0$。

也可以证明，对于异步和并行更新，固定点或循环是可能的，而 `f` 非单调的推广以类似的方式进行了讨论。另一种方法支持局部激活函数在高维空间中。对于这一点，参见

## 连续时间动力学

许多作者引入了神经网络微分模型，使得连接时间和步是连续的。在这种背景下，Cohen 和 Grossberg (1983) 提出了：

$$
\frac{dx_i}{dt} = a_i f(\sum_j w_{ij}x_j - b_i) \quad i=1\leq n
$$

方程 (9)假设 `W` 是对称的。那么更新降低能量

$$
\frac{dE}{dt} = -\frac{1}{2}\sum_{i,j}w_{ij}x_i\frac{dx_j}{dt} - \frac{1}{2}\sum_{i,j}w_{ij}\frac{dx_i}{dt}x_j + \sum_i b_i\frac{dx_i}{dt} \quad (11)
$$

其中 $y_i = \text{arg}(\sum_j w_{ij}x_j - b_i)$。

**定理 6.** (Hopfield)

$$
E(t) = -\frac{1}{2}\sum_{i,j}w_{ij}x_ix_j + \sum_i b_ix_i
$$

是更新 11 的能量函数。

*证明。* 如果 `W` 是对称的，得到：

$$
\frac{dE}{dt} = -\frac{1}{2}\sum_{i,j}w_{ij}x_i\frac{dx_j}{dt} - \frac{1}{2}\sum_{i,j}w_{ij}\frac{dx_i}{dt}x_j + \sum_i b_i\frac{dx_i}{dt}
$$

从方程 11 得到：

$$
\frac{dE}{dt} = -\sum_i \frac{dx_i}{dt} \left( \sum_{j \neq i} w_{ij}x_j + b_i \right) \quad (2)
$$

由于 $g_i \geq 0$，递增得到 $dE/dt \leq 0 \square$。微分模型的良好综由 Grossberg (1988) 和 Hirsch (1989) 提供。

## 讨论

在本文中我们回顾了接受能量函数的主要结果。这种存在

## 集成学习

### 引言

学习描述了许多活动，从强化学习到。最易理解的学习方法被称为监督学习（见统计推断）。在这种设置下，学习由一组特征 (`x`) 和一个标签 (`y`) 组成，假设对于每个训练数据 (`x`, `y`)，存在某个函数使得 `y=f(x)`。目标是找到 `f` 的近似值，使其能够应用于新值。学习器被称为分类器，它为标记的输入点分配类别。监督学习可以应用于许多问题，包括手写识别和语言处理中的词性标记。

在线机器学习涉及在可能的函数空间（称为假设）中搜索，然后通过优化找到 `h`，即对未知函数 `f` 的最佳近似。为了衡量 `h` 与训练数据的匹配程度，我们使用指标来评估 `h` 与关于问题的现有知识的一致性。

作为一个例子，考虑学习识别英语字母 k 的问题。考虑单词 *desk, think, hook* 和 *quick*，这些单词中 k 是发音的；在 *back* 和 *quick* 中 k 不发音，我们将假设 c 负责发音。定义一个特征向量，覆盖 k 之前的两个字母和之后的两个字母。这些单词每一个可以用以下数据点表示：

| $x_1$ | $x_2$ | $x_3$ | $x_4$ | $x_5$ | $y$ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| s | | | | | +1 |
| i | | | | | +1 |
| c | | | | | -1 |
| n | | | | | -1 |
| a | | | | | -1 |
| - | | | | | +1 |

其中如果 k 发音则 `y=+1`，如果 k 不发音则 `y=-1`，其中 - 表示单词的结束。

最有效且应用广泛的学习算法之一是搜索决策树的假设空间。图 1 显示了一个解释上述数据点的决策树。

为了构建一个新的决策树，我们从根节点（树的顶部）开始，首先检查 `x_5=c`。如果是，我们沿着左分支进入“左”节点，预测 k 不发音。如果不是，我们沿着右分支进入另一个节点：如果 `x_5=n`？如果是，我们遵循

在图像处理操作（如分量分析和傅里叶变换）。生成的集成分类器的准确性显著高于任何一个单个神经网络。

促进多样性的一种简单方法是操纵训练数据的输出。Dietrich 和 Baker (1995) 描述了一种名为“误差纠正输出”的方法。通过对类别进行划分，它们在不同的子集 `A_i` 和 `B_i` 上学习分类器。然后对这些数据进行标记，使得 `A_i` 中的原始类别被赋予派生标签 -1，而 `B_i` 中的原始类别被赋予派生标签 +1。接着，使用这些数据构建子集 `A_i` 和 `B_i` 的分类器 `h_i`，以及一个由 `K` 个分类器 `h_1, ..., h_K` 组成的集成。

现在，给定一个新的数据点 `x`，应该如何对其进行分类？答案是让每个分类器 `h_i` 对 `x` 进行分类。如果 `h_i(x) = 1`，它投下赞成票；如果 `h_i(x) = -1`，它投下反对票。在所有 `K` 个分类器投票后，得票数最多的类别被选为集成的预测结果。

考虑这种方法的一种有趣方式是，每个类别 `j` 都被视为一个误差纠正类。如果 `x=j`，我们认为 `B_j` 为 1；如果 `x != j`，则为 0。集成方法尝试将 `x` 分类为一个 0-1 二进制值。当应用分类器对点 `x` 进行分类时，它们的预测点被转换为一个 K 位的字符串。字符串中 1 的数量就是预测结果。这种方法提高了决策树和反向传播学习在各种分类问题上的性能。

在学习算法中还可以引入另一种收集多样性的方法。例如，可以通过随机化数据注入顺序来引入 Bag袋（Bagging）算法。同样，可以通过随机化特征和分裂阈值的选择来引入随机森林。正如 Dietrich (2000) 所示，随机森林在 33 个基准任务中的 14 个上优于其他方法（在其余 16 个任务上也是如此）。

另一种方法是使用随机子集法，通过选择决策树集合（“决策森林”）来促进多样性。该方法在每个节点处选择随机特征子集，并限制树生长算法改变其分裂规则。Breiman (2001) 证明，通过使用随机子集法，我们生成的决策森林提供了卓越的性能。

## 集成的构建方法

在上述所有方法中，集成中的每个 `h_i` 都是通过其他方法中的一种，通过操纵输入、输出、加权投票或注入噪声构建的。数据点的最终分类是各个分类器的加权和。

从集成的构建角度来看，它是一个加性模型，通过对一组组件取加权和来对新数据点的类别进行建模。这种观点暗示了选择模型和权重以使得加权和良好拟合的算法。在这种方法中，一个假设的选择会影响其他假设的选择以及分配给它们的权值。在统计学中，此类集成被称为广义加性模型（Hastie and Tibshirani, 1990）。

由 Freund 和 Schapire (1997) 引入的 AdaBoost 算法是一种通过一次添加一个假设来构建加性模型的有效方法。每个集成都学习最小化训练集上的分类误差。目标是最小化加权和，使得 `H(x) = sum w_i h_i(x)` 与 `x` 的正确标签 `y` 符号相同。

该算法的操作如下：令 `d(x_i)` 为第 `t` 次迭代中数据点 `i` 的权重。在每次迭代中，学习一个分类器 `h_t` 以最小化加权误差。加权误差为 `epsilon_t = d(h_t(x))`，其中 `h_t(x)` 是假设 `h_t` 预测的标签。该权重计算方式为：

`w_i = sqrt((1+epsilon_t)/(1-epsilon_t))`

为了计算下一次迭代的权重，使用数据点 `i` 的 `Z_i` 使 `d(x_i)` 之和为 1。

Breiman (1997) 表该算法是空间中的梯度下降，目标是最小化目标函数：

`J(H) = sum y h(x)`

在实验研究（Freiman and Schapire, 1996; Bagging and Kolac, 1999; Dietrich, 2000）中，算法（bagging 和 AdaBoost）在训练数据上表现良好，但在噪声测试数据集上表现较差。

主要集合是指包含大量错误标记数据的数据集。在这种情况下，与其他分类器相比，AdaBoost 在噪声数据集上的表现较差。

其原因是集成的完全构建基于 Vapnik (1995) 的边际分析，并由 Schap 等人 (1998) 扩展。这表明，集成在新数据点上的误差受训练数据中边际小于 `Phi>0` 的点比例的限制，公式如下：

`log(m) / sqrt(Theta)`

忽略了常数因子和一些对数项。在该公式中，`m` 是从中提取单个分类器的假设空间的表达式。`Theta` 的值选择是为了最小化其方差。

直观地说，这表明如果学习算法仅使用一个假设就能在每个数据点上获得一个“安全边际”，那么集成在测试数据上的表现将是有效的。AdaBoost 在噪声数据上的表现通常较差，因为它在训练数据上过度关注了错误点。然而，在集成方法中，AdaBoost 往往能产生很好的泛化能力。这表明它在测试数据上的表现可能优于其他方法。

## 参考文献

- Bauer, E., and Kohavi, R. (1999). An empirical analysis of classification algorithms: bagging, boosting.
- Breiman, L. (1996). Boosting, Machine Learning, 24:123–140.
- Breiman, L. (1997). 48th Annual Conference on Computer Applications, California, USA.
- Dietrich, T., Hastie, R., and Stone, C. J. (1994). Classification and Regression Trees, New York: Wadsworth.
- Hu, Y. Q. (1995). Random subspace method for constructing decision trees. IEEE Trans. Pattern Anal. Machine Intell., 7:2832–2844.
- Weiss, Y. output.
- Dietrich, T., and Babnik, V. (1995). Multiclass learning problems by random output codes. Journal of Artificial Intelligence Research, 2:223–268.
- Weiss, Y., and Schapire, R. (1999). A new approach to boosting with small classification sets. Proceedings of the 16th International Conference on Machine Learning.
- Freund, Y., and Schapire, R. (1997). A decision-theoretic generalization of ensemble learning and application to boosting. Journal of Comp. Syst. Sci., 9(1):195–199.
