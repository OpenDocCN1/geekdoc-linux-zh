
- Breitenberg, V., and Schwab, A., 1991. Neural Coding: The Statistics and Geometry; Berlin: Springer-Verlag, 1068–1069.

- Buesch, T., and Hochreiter, S., 1998. The integration of deep learning. Neural Networks, 11(3),265–262.

- Erdmann, E., and Gunther, J., 1991. A mathematical theory of visual perception. Vision Research, 34:137–150.

- Fries, E. L., and Seelinger, P., 1997. Learning of brightness. Comput. Vis., 3:227–239.

- Horn, G. A., and Mallot, H., 1988. Dynamics of attention in space. Neural Networks, 5(4),127–140.

- Mallot, H., Saul, V., and Ganakakopoulos, P., 1992. Neural processing of vision: A dynamical model from cortical hierarchy. Vision Research, 54,341–355.

- Murray, D. J., 1988, Mathematical Biology; Berlin: Springer-Verlag, 49–50.

- Peters, A., 1985. Visual cells of the retina, in Cortex, vol. 3, Vision (A. Peters and E. G. Jones), New York: Plenum Press, pp. 12.

- Schwartz, E., 1980. Functional anatomy of the visual cortex. Vision, 25:645–669.

# 讨论

在性层中关系的解释行为。其他可用于某些目的的特征是非线性激活动力学和神经映射。一些解释包括以下：

- 1. 侧向连接。层内活动之间的侧向交互可以产生协同或抑制效应，导致引导或相关的类型的活动模式（Murray, 1988）。该原理的一个应用是通过映射场中的协作动力学解决对应问题（参见 Blake and Wilson, 1991；参见 Chipchiatti and Arbib, 1998，以及 STEREO CORRESPONDENCE）。侧向交互的其他示例还包括人工神经网络中广泛使用的水平或非求和方案。

- 2. 拓扑。虽然感受野的连续性是邻域操作的前提，但拓扑映射引入的分布平滑可以简化后续的信息任务。示例包括视觉系统不同皮层部分（黄斑/边缘）的分配，以及对具有空间变异的图像的处理，例如光流模式。平面平移产生的光流可以通过所谓的反向视角映射输入障碍物来补偿。这种以服务器引导的方式会导致流场发生意想不到的变化，这些变化很容易被检测。Mallot 等 (2020) 给出了拓扑处理问题应用的综述。

- 3. 特征图和种群编码。虽然目前为止给出的示例是感觉输入，分析结果对于运动更好。在这里，运动层中的活动分布以运动的“场”来表示。

带有一个时空狄拉克 $\delta(x, t)$，它是系统中一个短时间闪烁的光点。如果系统是线性的、不变的且平稳的，则对任意刺激的响应可以通过适当偏移的加权脉冲的叠加来产生。位于 $y$ 处的皮层单元的感受野 $p_y(x, t)$ 描述了在每个时刻每个输入位置 $x$ 对单元 $y$ 的影响。线性的、不变的且平稳的点扩散感受野（例如，$p_y$ “向后看时间轴”，“p_x$ “向前看时间轴”）。在线性系统中，这些是伴随算子的核（Mallick, 1994）。

点像和感受野在线性系统中最为用，在这些系统中，它们通过叠加描述刺激-响应行为。在非线性系统中，则需要对这些属性进行功能性操作测量。可能的选择有 (1) 具有平稳映射的系统的线性近似，(2) 维-Volterra 方程（通常在二阶后进行近似），以及 (3) 如方程 1–3 所示的非线性方程。

# 感受野属性

图 2 显示了感受野模型中实现真实性的四个步骤。图 4 说明了系统与不变性的前馈系统，其中可以解释线性系统的时空特征（Korn and von Seelen, 1972）。关于节肢动物髓质诱导的一些早期工作，描述了许多后来的功能（感受野是高斯函数的导数，Gabor 函数）。这些现在被用于许多线性系统。在正馈的情况下，“视网膜”的空间特征和时间特征被认为是唯一感兴趣的特征。通过添加几个此类特征可以实现这种简单性（例如，对于视网膜的中心性细胞和离中心细胞；Kriger and Briggs, 1990）。时空特征的一个计算应用是视觉系统的处理（Hofmann, 1972）。可以发现，文中还描述了专门对其他刺激参数（方向、速度、光谱等）做出响应的感受野（Adelson and Bergen, 1991; Muller 等, 1990）。

在图 2B 中，当考虑反馈连接时，许多层展示了正馈系统的简单性（Korn, 1986）。反馈机制可以 (1) 锐化感受野，因为点可以通过反馈连接通过内部网络信号；(2) 实现感受野空间和时间方面的完全非特异性。这些效应中的第一个在从强度变化中检索光线的“视网膜”方案中得到了说明（图 4A）。这还引入了用于图像处理的感受网络的概念，包括层的连续创建，以及扩散类型的方程，其中空间交互通过偏导数而非核进行建模。

相比之下，正馈系统通过空间变异感受野匹配得到了扩展（Mallott 等, 1990）。图 2D 中映射与反馈的结合尚未在系统中使用。其激活由下文引用的方程 1–3 描述。

# 神经层的信息处理能力

其他层讨论了线性层中关系的解释行为。其他可用于某些目的的特征是非线性激活动力学和神经映射。一些解释包括以下：

- 1. 侧向连接。层内活动之间的侧向交互可以产生协同或抑制效应，导致引导或相关的类型的活动模式（Murray, 1988）。该原理的一个应用是通过映射场中的协作动力学解决对应问题（参见 Blake and Wilson, 1991；参见 Chipchiatti and Arbib, 1998，以及 STEREO CORRESPONDENCE）。侧向交互的其他示例还包括人工神经网络中广泛使用的水平或非求和方案。

- 2. 拓扑。虽然感受野的连续性是邻域操作的前提，但拓扑映射引入的分布平滑可以简化后续的信息任务。示例包括视觉系统不同皮层部分（黄斑/边缘）的分配，以及对具有空间变异的图像的处理，例如光流模式。平面平移产生的光流可以通过所谓的反向视角映射输入障碍物来补偿。这种以服务器引导的方式会导致流场发生意想不到的变化，这些变化很容易被检测。Mallot 等 (2020) 给出了拓扑处理问题应用的综述。

- 3. 特征图和种群编码。虽然目前为止给出的示例是感觉输入，分析结果对于运动更好。在这里，运动层中的活动分布以运动的“场”来表示。

# 学习与泛化：理论边界

## 参考文献

- Adelson, E., and Bergen, J., 1991. Functional function and elements of vision, in Computational Models of Vision (M. S. Land and J. A. Moskovitz), Cambridge: MIT Press, pp. 3.

- Almond, G. D., 1997. Dynamics of pattern formation in lateral-type neural networks. Feed. Biol., 27:77–78.

- Blake, R., and White, J. E., 1991. Stereoscopic vision. Nature, 350:793–796.

- Breitenberg, V., and Schwab, A., 1991. Neural Coding: The Statistics and Geometry; Berlin: Springer-Verlag, 1068–1069.

- Buesch, T., and Hochreiter, S., 1998. The integration of deep learning. Neural Networks, 11(3),265–262.

- Erdmann, E., and Gunther, J., 1991. A mathematical theory of visual perception. Vision Research, 34:137–150.

- Fries, E. L., and Seelinger, P., 1997. Learning of brightness. Comput. Vis., 3:227–239.

- Horn, G. A., and Mallot, H., 1988. Dynamics of attention in space. Neural Networks, 5(4),127–140.

- Mallot, H., Saul, V., and Ganakakopoulos, P., 1992. Neural processing of vision: A dynamical model from cortical hierarchy. Vision Research, 54,341–355.

- Murray, D. J., 1988, Mathematical Biology; Berlin: Springer-Verlag, 49–50.

- Peters, A., 1985. Visual cells of the retina, in Cortex, vol. 3, Vision (A. Peters and E. G. Jones), New York: Plenum Press, pp. 12.

- Schwartz, E., 1980. Functional anatomy of the visual cortex. Vision, 25:645–669.

# 讨论

在性层中关系的解释行为。其他可用于某些目的的特征是非线性激活动力学和神经映射。一些解释包括以下：

- 1. 侧向连接。层内活动之间的侧向交互可以产生协同或抑制效应，导致引导或相关的类型的活动模式（Murray, 1988）。该原理的一个应用是通过映射场中的协作动力学解决对应问题（参见 Blake and Wilson, 1991；参见 Chipchiatti and Arbib, 1998，以及 STEREO CORRESPONDENCE）。侧向交互的其他示例还包括人工神经网络中广泛使用的水平或非求和方案。

- 2. 拓扑。虽然感受野的连续性是邻域操作的前提，但拓扑映射引入的分布平滑可以简化后续的信息任务。示例包括视觉系统不同皮层部分（黄斑/边缘）的分配，以及对具有空间变异的图像的处理，例如光流模式。平面平移产生的光流可以通过所谓的反向视角映射输入障碍物来补偿。这种以服务器引导的方式会导致流场发生意想不到的变化，这些变化很容易被检测。Mallot 等 (2020) 给出了拓扑处理问题应用的综述。

- 3. 特征图和种群编码。虽然目前为止给出的示例是感觉输入，分析结果对于运动更好。在这里，运动层中的活动分布以运动的“场”来表示。

带有一个时空狄拉克 $\delta(x, t)$，它是系统中一个短时间闪烁的光点。如果系统是线性的、不变的且平稳的，则对任意刺激的响应可以通过适当偏移的加权脉冲的叠加来产生。位于 $y$ 处的皮层单元的感受野 $p_y(x, t)$ 描述了在每个时刻每个输入位置 $x$ 对单元 $y$ 的影响。线性的、不变的且平稳的点扩散感受野（例如，$p_y$ “向后看时间轴”，“p_x$ “向前看时间轴”）。在线性系统中，这些是伴随算子的核（Mallick, 1994）。

点像和感受野在线性系统中最为用，在这些系统中，它们通过叠加描述刺激-响应行为。在非线性系统中，则需要对这些属性进行功能性操作测量。可能的选择有 (1) 具有平稳映射的系统的线性近似，(2) 维-Volterra 方程（通常在二阶后进行近似），以及 (3) 如方程 1–3 所示的非线性方程。

# 感受野属性

图 2 显示了感受野模型中实现真实性的四个步骤。图 4 说明了系统与不变性的前馈系统，其中可以解释线性系统的时空特征（Korn and von Seelen, 1972）。关于节肢动物髓质诱导的一些早期工作，描述了许多后来的功能（感受野是高斯函数的导数，Gabor 函数）。这些现在被用于许多线性系统。在正馈的情况下，“视网膜”的空间特征和时间特征被认为是唯一感兴趣的特征。通过添加几个此类特征可以实现这种简单性（例如，对于视网膜的中心性细胞和离中心细胞；Kriger and Briggs, 1990）。时空特征的一个计算应用是视觉系统的处理（Hofmann, 1972）。可以发现，文中还描述了专门对其他刺激参数（方向、速度、光谱等）做出响应的感受野（Adelson and Bergen, 1991; Muller 等, 1990）。

在图 2B 中，当考虑反馈连接时，许多层展示了正馈系统的简单性（Korn, 1986）。反馈机制可以 (1) 锐化感受野，因为点可以通过反馈连接通过内部网络信号；(2) 实现感受野空间和时间方面的完全非特异性。这些效应中的第一个在从强度变化中检索光线的“视网膜”方案中得到了说明（图 4A）。这还引入了用于图像处理的感受网络的概念，包括层的连续创建，以及扩散类型的方程，其中空间交互通过偏导数而非核进行建模。

相比之下，正馈系统通过空间变异感受野匹配得到了扩展（Mallott 等, 1990）。图 2D 中映射与反馈的结合尚未在系统中使用。其激活由下文引用的方程 1–3 描述。

# 神经层的信息处理能力

其他层讨论了线性层中关系的解释行为。其他可用于某些目的的特征是非线性激活动力学和神经映射。一些解释包括以下：

- 1. 侧向连接。层内活动之间的侧向交互可以产生协同或抑制效应，导致引导或相关的类型的活动模式（Murray, 1988）。该原理的一个应用是通过映射场中的协作动力学解决对应问题（参见 Blake and Wilson, 1991；参见 Chipchiatti and Arbib, 1998，以及 STEREO CORRESPONDENCE）。侧向交互的其他示例还包括人工神经网络中广泛使用的水平或非求和方案。

- 2. 拓扑。虽然感受野的连续性是邻域操作的前提，但拓扑映射引入的分布平滑可以简化后续的信息任务。示例包括视觉系统不同皮层部分（黄斑/边缘）的分配，以及对具有空间变异的图像的处理，例如光流模式。平面平移产生的光流可以通过所谓的反向视角映射输入障碍物来补偿。这种以服务器引导的方式会导致流场发生意想不到的变化，这些变化很容易被检测。Mallot 等 (2020) 给出了拓扑处理问题应用的综述。

- 3. 特征图和种群编码。虽然目前为止给出的示例是感觉输入，分析结果对于运动更好。在这里，运动层中的活动分布以运动的“场”来表示。

通过零-一损失建模为 $l_0(\hat{y}, y) = \mathbb{1}_{\hat{y} \neq y}$。（此处表示指示函数。）通过使用代价矩阵 $C \in \mathbb{R}^{Y \times Y}$ 可以获得更复杂的损失函数。

在零-一损失 $l_0$ 的情况下，覆盖数 $N(1/m, \mathcal{G}, m)$ 等于由 $[0, 1]$ 诱导损失函数 $g \in \mathcal{G}$ 产生的不同损失函数 $g(z_1), \dots, g(z_m)$ 的数量。

函数学习。$\mathcal{Y} = \mathbb{R}$。经典回归利用平方损失，$l(\hat{y}, y) = (\hat{y} - y)^2$。其他损失函数包括 $\ell_1$ 损失 $l(f(x), y) = |f(x) - y|$ 以及 $\epsilon$ 损失 $l_{\epsilon}(f(x), y) = \mathbb{1}_{|f(x) - y| > \epsilon}$。学习问题的设定非常直接：

这种对 $l_{RM}$ 的表征在分类任务的证明中与 $S$ 是“自然”等价。需要注意的是，结果仅适用于 $l_{RM}$。分析其他算法的复杂度仍然是可能的，并且

$$h_{RM}(x) := \text{argmin}_{y \in \mathcal{Y}} \mathbb{E}_{Y} [l(y, Y)].$$

如果我们知道 $P$，那么它不仅在训练集上已知这一事实对于研究学习算法泛化误差的理论边界是有用的。然而，这些边界对于大多数训练样本的抽取都是有效的，如下所示：

## 理论边界

$$P_{RM}(R(h_{RM}) \geq \hat{R}_{RM}(h_{RM}) + \delta) \geq 1 - \delta.$$

在此类边界的分析中，考虑损失诱导的函数类非常方便：

$$L_{l} := \{h : x \mapsto l(h(x), y) \mid h \in \mathcal{H}\}.$$

此处呈现的所有分析的起点对于固定的假设 $h : x \mapsto \Upsilon$（以及诱导的损失函数 $g(x, y) := l(h(x), y)$），我们知道：

$$P(R(h) - \hat{R}(h) \geq c) = P(\mathbb{E}g - \hat{E}g \geq c) \leq \exp(-c^2m)$$

如果我们考虑该类的复杂性和零-一损失；函数学习类中的推理在概念上是简单的，如果损失 $g$ 是有界的，则 $c$ 是常数且 $c \in [0, 1]$。这是由于著名的集中偏离理论结果（Devroye, 2001）。

第二个边界是一致性边界，它考虑了发生在的事件

## 学习算法的一致性

一致性是学习算法的一种属性，保证在无限样本数据的极限情况下，学习算法将达到最小风险。其定义与经验空间 $\mathcal{H} \subset \mathcal{Y}^X$ 相关，并且
