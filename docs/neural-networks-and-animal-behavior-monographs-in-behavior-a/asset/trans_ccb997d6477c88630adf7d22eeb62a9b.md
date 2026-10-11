
可以使用公式 (2.11)，其中 $y(t) = \sum_j W_{ji} y_j(t)$（详见 2.1.3 节）。后者实际上是简单连续时间模型的离散时间近似（由于数字计算机是按时间步长运行的，因此在计算机模拟中，这种近似总是必要的）。另一种可能性如下。在每个时间步，我们随机确定节点的顺序。然后更新第一个选中的节点。当我们更新第二个节点时，我们使用第一个节点更新后的活动，依此类推对所有节点进行操作。由于每个时间步的随机顺序都不同，该过程模拟了真实神经系统中的无协调动力学，因此被称为*异步动力学*（Amit 1989）。通过这种方式获得的任何结果显然对更新操作顺序的变化具有鲁棒性。

## 2.3 实现特定的输入-输出映射

网络实现的输入-输出映射当然取决于权重的值。在实践中，与神经网络相关的大部分工作都涉及权重的设置。到目前为止，我们考虑过的问题中，合适的权重可以通过直觉或使用简单的数学方法来找到。在本节中，我们描述了一些强大的权重设置方法，这些方法可以处理更复杂的问题。在下一节中，我们将描述根据输入组织网络权重的程序，而不是寻求实现特定的输入-输出映射。

权重设置方法可以被视为现实世界现象的模型，即神经系统中突触如何变化，或者仅仅作为构建处理特定任务的工具，而不作其他额外声明。这里侧重于后者观点，而第 4 章涵盖生物学习。我们的目标是构建一个网络，该网络能产生 $\mu$ 个指定的输入-输出映射：

$$
m(\mathbf{x}_\alpha, \mathbf{W}) = \mathbf{d}_\alpha \quad \forall \alpha = 1, \dots, \mu \tag{2.21}
$$

其中 $m$ 是网络实现的输入-输出映射，$\mathbf{W}$ 表示所有网络权重，$\mathbf{d}_\alpha$ 是对输入 $\mathbf{x}_\alpha$ 的期望输出模式。公式 (2.21) 是一个由 $\mu$ 个方程组成的系统，其中未知数是网络权重。直接分析这些方程通常非常具有挑战性，或者根本不可行。唯一可以用简单数学彻底处理的情况是线性网络，即所有节点都具有线性传递函数的网络，例如公式 (2.6)。在介绍更通用的权重设置技术之前，我们将讨论这种情况（最后会对具有非线性输出节点的网络进行简要说明）。

### 2.3.1 线性网络中的权重设置

如果所有节点的传递函数都是线性的，则可以通过形式化方法找到满足公式 (2.21) 的权重，或者可以证明它们不存在。我们从一个线性感知机开始，即公式 (2.19)，以及单个输入-输出映射。这对应于 $\mu = 1$ 且 $m(\mathbf{x}_1, \mathbf{W}) = \mathbf{W} \cdot \mathbf{x}_1$ 的公式 (2.21)。在这种情况下，很容易检查出，单个要求 $\mathbf{W} \cdot \mathbf{x}_1 = d_1$ 由形式为

$$
\mathbf{W} = c_1 \mathbf{x}_1 \tag{2.22}
$$

的权重向量满足，其中 $c_1 = d_1 / (\mathbf{x}_1 \cdot \mathbf{x}_1)$。此外，如果我们向 $\mathbf{W}$ 添加一个向量 $\mathbf{u}$，使得 $\mathbf{u} \cdot \mathbf{x}_1 = 0$，结果不会改变。总之，该任务的一般解形式为

$$
\begin{cases} \mathbf{W} = \frac{d_1}{\mathbf{x}_1 \cdot \mathbf{x}_1}\mathbf{x}_1 + \mathbf{u} \\ \mathbf{u} \cdot \mathbf{x}_1 = 0 \end{cases} \tag{2.23}
$$

通过扩展这一推理，可以证明实现 $\mu$ 个输入-输出映射的权重向量可以写为

$$
\begin{cases} \mathbf{W} = \sum_{\alpha=1}^{\mu} c_\alpha \mathbf{x}_\alpha + \mathbf{u} \\ \mathbf{u} \cdot \mathbf{x}_\alpha = 0 \quad \forall \alpha = 1, \dots, \mu \end{cases} \tag{2.24}
$$

然而，$c_\alpha$ 的一般表达式并不像公式 (2.23) 中那样简单。我们将展示如何在有两个输入-输出映射的情况下解决此问题。这个简单的任务将贯穿本节，用于说明和比较不同的权重设置技术。可能有必要将其想象为一个判别任务，其中 $\mathbf{x}_1$ 需要映射到高输出，而 $\mathbf{x}_2$ 映射到低输出，尽管该过程对所有期望输出都是一样的。

根据公式 (2.24)，我们猜测 $\mathbf{W}$ 应该具有形式 $c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2$，因此我们的任务是找到满足要求 $\mathbf{W} \cdot \mathbf{x}_\alpha = d_\alpha$ 的 $c_1$ 和 $c_2$ 的值。如果我们用 $c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2$ 替换 $\mathbf{W}$，这些要求可以表示为

$$
\begin{aligned} (c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2) \cdot \mathbf{x}_1 &= c_1 \mathbf{x}_1 \cdot \mathbf{x}_1 + c_2 \mathbf{x}_2 \cdot \mathbf{x}_1 = d_1 \\ (c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2) \cdot \mathbf{x}_2 &= c_1 \mathbf{x}_1 \cdot \mathbf{x}_2 + c_2 \mathbf{x}_2 \cdot \mathbf{x}_2 = d_2 \end{aligned} \tag{2.25}
$$

为了简洁起见，我们写 $\mathbf{x}_\alpha \cdot \mathbf{x}_\beta = X_{\alpha\beta}$：

$$
\begin{aligned} X_{11}c_1 + X_{12}c_2 &= d_1 \\ X_{12}c_1 + X_{22}c_2 &= d_2 \end{aligned} \tag{2.26}
$$

（注意 $X_{12} = X_{21}$）。上述是关于未知数 $c_1$ 和 $c_2$ 的二元线性方程组。它可以通过多种方法求解，得出

$$
\begin{aligned} c_1 &= \frac{d_1 X_{22} - d_2 X_{12}}{X_{11} X_{22} - X_{12}^2} \quad \quad c_2 &= \frac{d_2 X_{11} - d_1 X_{12}}{X_{11} X_{22} - X_{12}^2} \end{aligned} \tag{2.27}
$$

作为练习，读者可以检查这些表达式确实使得 $\mathbf{W} \cdot \mathbf{x}_1 = d_1$ 且 $\mathbf{W} \cdot \mathbf{x}_2 = d_2$。如果网络需要满足许多输入-输出映射，同样的技术也适用，但计算变得单调乏味。数值或形式化数学软件将派上用场，而线性代数教科书将提供理论基础。

注意，公式 (2.24) 用向量 $\mathbf{x}_\alpha$ 表示权重向量 $\mathbf{W}$。这为"$\mathbf{x}_\alpha$ 已被'存储在内存中'"这一直观陈述提供了具体的解释。此外，它允许人们理解对于一般输入 $\mathbf{x}$ 的输出，通过 $\mathbf{x}$ 与 $\mathbf{x}_\alpha$（以及向量 $\mathbf{u}$）的关系来解释。这将在第 3 章中讨论。

即使输出节点不是线性的，公式 (2.24) 也成立。这样的网络可以写为 $\mathbf{r} = f(\mathbf{W} \cdot \mathbf{x})$。我们提及这种情况，因为非线性输出节点常被用于将网络输出限制在 0 和 1 之间，并将其解释为响应概率。证明基于以下观察：要求 $d_\alpha = f(\mathbf{W} \cdot \mathbf{x}_\alpha)$ 可以写为 $d_\alpha = \mathbf{W} \cdot \tilde{d}_\alpha$，其中 $\tilde{d}_\alpha = f^{-1}(d_\alpha)$，$f^{-1}$ 是 $f$ 的反函数。因此，我们回到了线性问题，尽管 $d_\alpha$ 的值不同。这意味着 $f$ 的不同选择会导致 $c_\alpha$ 的值不同，但不改变权重向量的结构。

### 2.3.1.1 线性网络的局限性和能力

在这里，我们扩展关于感知机局限性的评论（第 40 页），通过询问公式 (2.21) 中的任务何时可以通过感知机解决。然后我们将推理扩展到一般线性网络。确定任务何时无法解决是很容易的。事实上，线性网络 $\mathbf{r} = \mathbf{W} \cdot \mathbf{x}$ 的定义意味着

$$
\mathbf{r}(\mathbf{x}_\alpha + \mathbf{x}_\beta) = \mathbf{r}(\mathbf{x}_\alpha) + \mathbf{r}(\mathbf{x}_\beta) \tag{2.28}
$$

因为 $\mathbf{W} \cdot (\mathbf{x}_\alpha + \mathbf{x}_\beta) = \mathbf{W} \cdot \mathbf{x}_\alpha + \mathbf{W} \cdot \mathbf{x}_\beta$（来自公式 2.8）。换言之，输入的总和的输出等于每个输入的输出之和（确实，这是线性的技术含义）。因此很清楚，如果一个输入-输出映射中，例如 $\mathbf{x}_\gamma = \mathbf{x}_\alpha + \mathbf{x}_\beta$ 但 $\mathbf{d}_\gamma \neq \mathbf{d}_\alpha + \mathbf{d}_\beta$，则该映射无法由线性网络实现。一般来说，如果在输入 $\mathbf{x}_1, \dots, \mathbf{x}_n$ 中，存在某个输入，例如 $\mathbf{x}_\beta$，可以写为其他输入的加权和，例如

$$
\mathbf{x}_\beta = \sum_{a \neq \beta} b_a \mathbf{x}_a \tag{2.29}
$$

（对于某些 $b_a$ 的选择），那么除非

$$
\mathbf{d}_\beta = \sum_{a \neq \beta} b_a \mathbf{d}_a \tag{2.30}
$$

否则不存在实现公式 (2.21) 中输入-输出映射的权重向量 $\mathbf{W}$。也就是说，输出之间必须保持与输入之间相同的关系。反之，如果无法将任何 $\mathbf{x}_a$ 写为公式 (2.29) 的形式，则公式 (2.21) 中的输入-输出映射可以由线性网络对任意选择的 $\mathbf{d}_a$ 实现。事实上，读者可能已经注意到，如果 $X_{11}X_{22} = X_{12}^2$（分式分母消失），公式 (2.27) 是没有意义的。这恰好发生在 $\mathbf{x}_1 = b\mathbf{x}_2$ 时，这是公式 (2.29) 的一个特例。事实上，在这种情况下我们有

$$
\begin{align*} X_{11} &= \mathbf{x}_1 \cdot \mathbf{x}_1 \\ X_{22} &= b^2 \mathbf{x}_1 \cdot \mathbf{x}_1 \\ X_{12} &= b \mathbf{x}_1 \cdot \mathbf{x}_1 \end{align*} \tag{2.31}
$$

因此 $X_{11}X_{22} = X_{12}^2 = b^2(\mathbf{x}_1 \cdot \mathbf{x}_1)^2$。关于此主题的更多信息可在线性代数教科书（线性方程组章节）中寻找。

